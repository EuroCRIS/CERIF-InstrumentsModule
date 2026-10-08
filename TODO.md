# TODO — implement the "Refactored CERIF" column of the PIDINST mapping

Source: [Mapping PIDINST to Refactored CERIF](https://docs.google.com/spreadsheets/d/1w67LH7OcDkDRgjHOj2PCJk0LG3Uj4YZyn8SpLjAttVo/edit?gid=0#gid=0)
Numbers below refer to the PIDINST item IDs in that spreadsheet.

Current state of the module: the mapping is fully documented in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md); defined so far: `Instrument_Instance`, `Instrument_Model`, the identifier classes and the three contribution types below, and `Metadata_Set` in the [Core](../CERIF-Core/entities/Metadata_Set.md). Remaining: the open question `Group_of_Instruments`, the new attributes, and housekeeping.

## 1. New entities to define

### Contribution types (subclasses of [Contribution_to_Infrastructure](../CERIF-Core/entities/Contribution_to_Infrastructure.md))
- [x] **Infrastructure_Ownership** — for the legal owner (item 5)
- [x] **Infrastructure_Operation** — for the operator (item 5); its `date range` carries the commissioned/decommissioned dates (item 11)
- [x] **Manufacturing** — `actor` is the manufacturer (item 6)

### Identifier classes (subclasses of [Resource_Identifier](../CERIF-Core/entities/Resource_Identifier.md))
- [x] **Instrument_Instance_Identifier** — base for alternate identifiers of an instance (item 13); note: record the context in which the identifier is meaningful, where available
- [x] **Serial_Number** — `alternateIdentifierType=SerialNumber` (item 13.1)
- [x] **Inventory_Number** — `alternateIdentifierType=InventoryNumber` (item 13.2)
- [x] **Other_Instrument_Instance_Identifier** — `alternateIdentifierType=Other` (item 13.3)
- [x] **Instrument_Model_Identifier** — `modelIdentifier` (item 7.2)
- [x] Decide: PIDINST item 1 (the PID itself) — the general notes say CERIF maps it to a *specific subclass* of Resource_Identifier; decide whether to define that subclass here or keep it generic — resolved: the PID is a DOI, so the mapping uses the Core DOI_Identifier; other identifiers are not prohibited from appearing alongside

### Other
- [x] **Metadata_Set** (subclass of [Document](../CERIF-Core/entities/Document.md)) — target of `HasMetadata` related identifiers (item 12) — defined in the [Core](../CERIF-Core/entities/Metadata_Set.md), which also retargets `has-metadata` to it
- [x] **Instrument_Model_Type** (controlled-vocabulary class) — values for `Instrument_Model.type` (item 9)
- [ ] Open question (end of spreadsheet): **Group_of_Instruments** — possible intermediate entity for groups of instruments

## 2. New attributes

- [ ] `Instrument_Model.type : Instrument_Model_Type` (item 9)
- [ ] `Instrument_Model.measuredVariable` — free text, 0–n (item 10)
- [ ] **`description` gap**: item 8 maps to `Infrastructure.description`, but neither [Resource](../CERIF-Core/entities/Resource.md) nor [Infrastructure](../CERIF-Core/entities/Infrastructure.md) in Core has a `description` attribute. Decide: propose adding it to CERIF-Core, or add a module-level `description` attribute on Instrument_Model (and possibly Instrument_Instance)

## 3. Decisions / naming to resolve (document in entity files)

- [x] Instance→model relationship: the spreadsheet maps items 6–10 to `Infrastructure_Instance.model`; the module currently names it `is-instance-of` / `has-instance`. Decide and document (rename, or note the discrepancy) — discrepancy noted in the mapping
- [x] `HasMetadata` (item 12): the spreadsheet says use `Resource.is-described-by` pointing at a Metadata_Set, while Core also has `has-metadata` / `is-metadata-of`. Follow the spreadsheet and document the choice — choice documented in the mapping
- [x] Document explicitly unsupported / unmapped items:
  - item 2 SchemaVersion (fixed "1.0", no mapping)
  - item 7.2.1 modelIdentifierType (not mapped at this stage)
  - item 12 `References` (too generic, not supported)
  - item 12 `IsAttachedTo` (not supported at this stage)
  - providing access to the instrument via a Service (general note 2 — not covered by this module)
- [x] Item 5.3/6.2 agent identifiers: the subtype of [Agent_Identifier](../CERIF-Core/entities/Agent_Identifier.md) encodes the `identifierType` (general note 3) — stated in the mapping (general note 3)

## 4. Document the mappings

- [x] Complete PIDINST → CERIF mapping documented in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md)
- [ ] Synchronize the adjustments made in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md) back to the [Google Spreadsheet](https://docs.google.com/spreadsheets/d/1w67LH7OcDkDRgjHOj2PCJk0LG3Uj4YZyn8SpLjAttVo/edit?gid=0#gid=0)

## 5. Fill in the boilerplate entity documentation

- [x] `entities/Instrument_Instance.md` — replace the "The scope of the entity..." placeholders with real Definition / Usage notes, Constraints
- [x] `entities/Instrument_Model.md` — same

## 6. Module housekeeping (template leftovers)

- [ ] Remove placeholder files: `entities/XXX.md`, `datatypes/XXX.md`, `datatypes/YYY.md`
- [x] Rewrite `diagrams/module.puml` (still shows the XXX template inheriting from Publication_Channel) with the real class hierarchy; regenerate `module.svg`
- [x] Replace placeholder example `examples/01_XXX/` with a real example: a PIDINST record (instance + model info) serialized in CERIF (`.ttl` + `.puml` + `.svg`); update `examples/README.md`
- [ ] Update `README.md` listings (still references XXX/YYY data types)
- [ ] Generate `serializations/RDF/` (the Scholarly Publication Module ships generated OWL/RDF; this module has none)
- [ ] Add a `.gitignore` (`.idea/` is currently untracked)

## 7. Open questions from the spreadsheet (no decision yet)

- [ ] Possibly an intermediate entity `Group_of_Instruments`?
- [ ] Number of instruments (in a group?)
- [ ] Location (of the instrument instance?)
- [ ] Responsible person / organisation unit?
