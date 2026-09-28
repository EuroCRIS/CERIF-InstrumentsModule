# TODO — implement the "Refactored CERIF" column of the PIDINST mapping

Source: [Mapping PIDINST to Refactored CERIF](https://docs.google.com/spreadsheets/d/1w67LH7OcDkDRgjHOj2PCJk0LG3Uj4YZyn8SpLjAttVo/edit?gid=0#gid=0)
Numbers below refer to the PIDINST item IDs in that spreadsheet.

Current state of the module: `Instrument_Instance` and `Instrument_Model` exist only as boilerplate skeletons (one relationship each: `is-instance-of` / `has-instance`). Everything else from the mapping is missing.

## 1. New entities to define

### Contribution types (subclasses of [Contribution_to_Infrastructure](../CERIF-Core/entities/Contribution_to_Infrastructure.md))
- [ ] **Infrastructure_Ownership** — for the legal owner (item 5)
- [ ] **Infrastructure_Operation** — for the operator (item 5); its `date range` carries the commissioned/decommissioned dates (item 11)
- [ ] **Manufacturing** — `actor` is the manufacturer (item 6)

### Identifier classes (subclasses of [Resource_Identifier](../CERIF-Core/entities/Resource_Identifier.md))
- [ ] **Instrument_Instance_Identifier** — base for alternate identifiers of an instance (item 13); note: record the context in which the identifier is meaningful, where available
- [ ] **Serial_Number** — `alternateIdentifierType=SerialNumber` (item 13.1)
- [ ] **Inventory_Number** — `alternateIdentifierType=InventoryNumber` (item 13.2)
- [ ] **Other_Instrument_Identifier** — `alternateIdentifierType=Other` (item 13.3)
- [ ] **Instrument_Model_Identifier** — `modelIdentifier` (item 7.2)
- [ ] Decide: PIDINST item 1 (the PID itself) — the general notes say CERIF maps it to a *specific subclass* of Resource_Identifier; decide whether to define that subclass here or keep it generic

### Other
- [ ] **Metadata_Set** (subclass of [Document](../CERIF-Core/entities/Document.md)) — target of `HasMetadata` related identifiers (item 12)
- [ ] **Instrument_Model_Type** (controlled-vocabulary class) — values for `Instrument_Model.type` (item 9)
- [ ] Open question (end of spreadsheet): **Group_of_Instruments** — possible intermediate entity for groups of instruments

## 2. New attributes

- [ ] `Instrument_Model.type : Instrument_Model_Type` (item 9)
- [ ] `Instrument_Model.measuredVariable` — free text, 0–n (item 10)
- [ ] **`description` gap**: item 8 maps to `Infrastructure.description`, but neither [Resource](../CERIF-Core/entities/Resource.md) nor [Infrastructure](../CERIF-Core/entities/Infrastructure.md) in Core has a `description` attribute. Decide: propose adding it to CERIF-Core, or add a module-level `description` attribute on Instrument_Model (and possibly Instrument_Instance)

## 3. Decisions / naming to resolve (document in entity files)

- [ ] Instance→model relationship: the spreadsheet maps items 6–10 to `Infrastructure_Instance.model`; the module currently names it `is-instance-of` / `has-instance`. Decide and document (rename, or note the discrepancy)
- [ ] `HasMetadata` (item 12): the spreadsheet says use `Resource.is-described-by` pointing at a Metadata_Set, while Core also has `has-metadata` / `is-metadata-of`. Follow the spreadsheet and document the choice
- [ ] Document explicitly unsupported / unmapped items:
  - item 2 SchemaVersion (fixed "1.0", no mapping)
  - item 7.2.1 modelIdentifierType (not mapped at this stage)
  - item 12 `References` (too generic, not supported)
  - item 12 `IsAttachedTo` (not supported at this stage)
  - providing access to the instrument via a Service (general note 2 — not covered by this module)
- [ ] Item 5.3/6.2 agent identifiers: the subtype of [Agent_Identifier](../CERIF-Core/entities/Agent_Identifier.md) encodes the `identifierType` (general note 3) — state this in the usage notes

## 4. Document the mappings that reuse existing Core mechanisms

### In Instrument_Instance usage notes
- [ ] item 1 Identifier → `Resource.has-identifier` (Resource_Identifier attached to the Resource ancestor)
- [ ] item 3 LandingPage → `Infrastructure.url`
- [ ] item 4 Name → `Infrastructure.title`
- [ ] item 5 Owner → `Infrastructure.has-contribution` with Infrastructure_Ownership / Infrastructure_Operation; owner is the `has-actor` Agent
- [ ] item 5.1 ownerName → name of the linked Agent (Group_or_Organisation_Unit.name, Person.name, or `display person name` of an [Affiliation_Statement](../CERIF-Core/entities/Affiliation_Statement.md) linked to the contribution)
- [ ] item 5.2 ownerContact → `contacts` of that Affiliation_Statement, using [Email_Address](../CERIF-Core/datatypes/Email_Address.md)
- [ ] item 5.3 ownerIdentifier → concrete subtype of Agent_Identifier assigned to the owner Agent
- [ ] item 11 Date → `date range` of the Operating (Infrastructure_Operation) contribution: startDate = Commissioned, endDate = DeCommissioned
- [ ] item 12 RelatedIdentifier:
  - `IsDescribedBy` → `Resource.has-description`
  - `IsNewVersionOf` → `Resource.is-new-version-of`
  - `IsPreviousVersionOf` → `Resource.is-previous-version-of`
  - `HasComponent` → `Resource.has-part`
  - `IsComponentOf` → `Resource.is-part-of`
  - `WasUsedIn` → [Resource_Usage_Statement](../CERIF-Core/entities/Resource_Usage_Statement.md) → `details` (Contribution_Statement) → `references` (Contribution, which is an Activity, i.e. the research activity the instrument was deployed in)
  - `IsIdenticalTo` → multiple Resource_Identifiers on the same Infrastructure
- [ ] item 13 AlternateIdentifier → Instrument_Instance_Identifier subtypes (see section 1)

### In Instrument_Model usage notes
- [ ] item 6 Manufacturer → Manufacturing contribution; `has-actor` is the manufacturer
- [ ] item 6.1 manufacturerName → Group_or_Organisation_Unit.name / Person.name / Affiliation_Statement `display person name`
- [ ] item 6.2 manufacturerIdentifier → concrete subclass of Agent_Identifier
- [ ] item 7.1 modelName → `Infrastructure.title`
- [ ] item 7.2 modelIdentifier → Instrument_Model_Identifier

## 5. Fill in the boilerplate entity documentation

- [x] `entities/Instrument_Instance.md` — replace the "The scope of the entity..." placeholders with real Definition / Usage notes, Constraints, and the mappings from section 4
- [x] `entities/Instrument_Model.md` — same

## 6. Module housekeeping (template leftovers)

- [ ] Remove placeholder files: `entities/XXX.md`, `datatypes/XXX.md`, `datatypes/YYY.md`
- [ ] Rewrite `diagrams/module.puml` (still shows the XXX template inheriting from Publication_Channel) with the real class hierarchy; regenerate `module.svg`
- [ ] Replace placeholder example `examples/01_XXX/` with a real example: a PIDINST record (instance + model info) serialized in CERIF (`.ttl` + `.puml` + `.svg`); update `examples/README.md`
- [ ] Update `README.md` listings (still references XXX/YYY data types)
- [ ] Generate `serializations/RDF/` (the Scholarly Publication Module ships generated OWL/RDF; this module has none)
- [ ] Add a `.gitignore` (`.idea/` is currently untracked)

## 7. Open questions from the spreadsheet (no decision yet)

- [ ] Possibly an intermediate entity `Group_of_Instruments`?
- [ ] Number of instruments (in a group?)
- [ ] Location (of the instrument instance?)
- [ ] Responsible person / organisation unit?
