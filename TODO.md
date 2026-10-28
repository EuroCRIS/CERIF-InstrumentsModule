# TODO — implement the "Refactored CERIF" column of the PIDINST mapping

Source: [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md)
Numbers below refer to the PIDINST item IDs in that document.

Current state of the module: the mapping is fully documented in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md); defined: `Instrument_Instance`, `Instrument_Model`, the identifier classes and the three contribution types below, and `Metadata_Set` in the [Core](../CERIF-Core/entities/Metadata_Set.md). All items in this list are done; possible extensions are tracked in [IDEAS.md](IDEAS.md).

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

## 2. New attributes

- [x] `Instrument_Model.type : Instrument_Model_Type` (item 9) — implemented as the `has-type` / `is-type-of` relationship to the controlled-vocabulary class `Instrument_Model_Type` (carrying a `label` attribute)
- [x] `Instrument_Model.measuredVariable` — free text, 0–n (item 10) — implemented as a `List<Multilingual_String>` attribute
- [x] **`description` gap**: item 8 maps to `Infrastructure.description`, but neither [Resource](../CERIF-Core/entities/Resource.md) nor [Infrastructure](../CERIF-Core/entities/Infrastructure.md) in Core has a `description` attribute. Decide: propose adding it to CERIF-Core, or add a module-level `description` attribute on Instrument_Model (and possibly Instrument_Instance) — resolved: `description` attribute added to [Resource](../CERIF-Core/entities/Resource.md) in CERIF-Core (inherited by Infrastructure and thus by Instrument_Model / Instrument_Instance)

## 3. Decisions / naming to resolve (document in entity files)

- [x] Instance→model relationship: the original mapping had items 6–10 mapped to `Infrastructure_Instance.model`; the module names it `is-instance-of` / `has-instance`. Decide and document (rename, or note the discrepancy) — discrepancy noted in the mapping
- [x] `HasMetadata` (item 12): the original mapping pointed at a Metadata_Set via `Resource.is-described-by`, while Core also has `has-metadata` / `is-metadata-of`. Use has-description and document the choice — choice documented in the mapping
- [x] Document explicitly unsupported / unmapped items:
  - item 2 SchemaVersion (fixed "1.0", no mapping)
  - item 7.2.1 modelIdentifierType (not mapped at this stage)
  - item 12 `References` (too generic, not supported)
  - item 12 `IsAttachedTo` (not supported at this stage)
  - providing access to the instrument via a Service (general note 2 — not covered by this module)
- [x] Item 5.3/6.2 agent identifiers: the subtype of [Agent_Identifier](../CERIF-Core/entities/Agent_Identifier.md) encodes the `identifierType` (general note 3) — stated in the mapping (general note 3)

## 4. Document the mappings

- [x] Complete PIDINST → CERIF mapping documented in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md)
- [x] Retire the Google Spreadsheet as a parallel source of record (2026-10-15) — the mapping is maintained in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md) only

## 5. Fill in the boilerplate entity documentation

- [x] `entities/Instrument_Instance.md` — replace the "The scope of the entity..." placeholders with real Definition / Usage notes, Constraints
- [x] `entities/Instrument_Model.md` — same

## 6. Module housekeeping (template leftovers)

- [x] Remove placeholder files: `entities/XXX.md`, `datatypes/XXX.md`, `datatypes/YYY.md`
- [x] Rewrite `diagrams/module.puml` (still shows the XXX template inheriting from Publication_Channel) with the real class hierarchy; regenerate `module.svg`
- [x] Replace placeholder example `examples/01_XXX/` with a real example: a PIDINST record (instance + model info) serialized in CERIF (`.ttl` + `.puml` + `.svg`); update `examples/README.md`
- [x] Update `README.md` listings (still references XXX/YYY data types)
- [x] Generate `serializations/RDF/` (the Scholarly Publication Module ships generated OWL/RDF; this module has none)
- [x] Add a `.gitignore` (`.idea/`) — done in 8f0891a

## 7. Open questions (no decision yet)

Moved to [IDEAS.md](IDEAS.md).

## 8. Review

Review by Dragan Ivanović, 2026-10-22. Scope: coverage of [PIDINST v1.0 mapping](mappings/PIDINST-v1.0.md) by the entity definitions and RDF/OWL serialization, including the updated local CERIF-Core dependency.

1. **Other identifier value:** Define where `Other_Instrument_Instance_Identifier` stores the actual identifier string. Neither this class nor its parent classes currently define a value attribute.
   - [x] Add Other_Instrument_Instance_Identifier.value — resolved: `value : String` added to the entity definition; the mapping (item 13) documents where the identifier string lands for each subtype
2. **Instrument lifecycle dates:** Distinguish commissioned/decommissioned dates from the period of an operator's relationship with an instrument. A change of operator must not imply that the instrument was decommissioned and commissioned again.
   - [x] Map this to Ownership instead of Operating. — resolved: the mapping (item 11) now targets the Ownership contribution, documented in the [Infrastructure_Ownership](entities/Infrastructure_Ownership.md) and [Infrastructure_Operation](entities/Infrastructure_Operation.md) usage notes
   - [x] Document this better in the mapping description: CERIF is a bit more detailed here by also recording the owner, but also PIDINST itself allows for multiple commission/decommission dates. — resolved: note added to the mapping row 11 (multiple periods ⇒ one Ownership contribution each); illustrated in the Ocean Surveyor example
3. **Alternate identifier type name:** Define where to store `alternateIdentifierName` (PIDINST item 13.2), the optional supplementary name of the identifier type, especially when `alternateIdentifierType` is Other. For instance, we can add `name` attribute into `Other_Instrument_Instance_Identifier.md`.
   - [x] Add Other_Instrument_Instance_Identifier.name — resolved: `name : String` added to the entity definition; the mapping (item 13.2) targets it for `alternateIdentifierName`
4. Distinction betweeen PIDINST Identifier and AlternateIdentifier is not mapped in CERIF, both of these become Instrument_Instance_Identifiers. Should it be marked somehow?
   - [x] Add `principal` boolean flag in Resource_Identifier. — resolved: `principal : Boolean` added to [Resource_Identifier](../CERIF-Core/entities/Resource_Identifier.md) in CERIF-Core; the mapping (items 1 and 13) documents the distinction: Identifier → True, AlternateIdentifiers → False

Additional light review by Jan Dvořák, 2026-10-28.

5. The Identifier ([mapping](mappings/PIDINST-v1.0.md) row 1) need not be just a DOI; it could be a Handle or some other type of identifier.
   - [ ] Fix the description of the target in mapping row 1, allowing a general [Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md).
