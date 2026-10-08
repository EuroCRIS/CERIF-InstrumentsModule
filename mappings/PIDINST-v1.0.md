# Mapping of PIDINST v1.0 to Refactored CERIF

The complete mapping between the *PIDINST v.1.0* specification (DOI [10.15497/RDA00070](https://doi.org/10.15497/RDA00070)) and the CERIF data model: the [CERIF Core](https://github.com/EuroCRIS/CERIF-Core) plus this [Instruments Module](../README.md).

Source of record: [Mapping PIDINST to Refactored CERIF](https://docs.google.com/spreadsheets/d/1w67LH7OcDkDRgjHOj2PCJk0LG3Uj4YZyn8SpLjAttVo/edit?gid=0#gid=0) — Jan Dvořák, Dragan Ivanović. The development of this mapping was done in the framework of the [INST-DSpace project](https://eurocris.org/projects/inst-dspace-project/) led by euroCRIS with funding from the Vietsch Foundation.

Entity names in **bold** without a link are to be defined by this module (see [TODO.md](../TODO.md)).

## General notes

1. CERIF-InstrumentsModule implements the PIDINST specification v1.0 (DOI 10.15497/RDA00070).
2. In CERIF we distinguish between an instrument instance and an instrument model; an instance references its model. This allows for information normalization. In the ideal case, authoritative model information is made available by the instrument manufacturer.
3. PIDINST defines the identifierType property (items 1.1, 12.1 and 13.1) for identifiers. CERIF maps that to a specific subclass of Resource_Identifier. We do not make that explicit in this table, as it would clutter the other mapping info. Similar mechanisms apply to other identifier types (for instance, ownerIdentifierType maps to subclasses of Agent_Identifier).

## PIDINST record except model information → [Instrument Instance](../entities/Instrument_Instance.md)

The PIDINST record, except the model information (items 6–10), is mapped to Instrument Instance, a subclass of Core [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md).

| ID | Property | Obl | Occ | PIDINST definition (and constraints) | Refactored CERIF |
|----|----------|-----|-----|--------------------------------------|------------------|
| 1 | Identifier | M | 1 | Unique string that identifies the instrument instance | A [DOI Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/DOI_Identifier.md) attached to the Resource (ancestor of Instrument Instance) via [has-identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__has-identifier); other identifiers (item 13) may appear alongside |
| 2 | SchemaVersion | M | 1 | Version number of the PIDINST schema used in this record. Fixed value "1.0" | — (not mapped; the value is fixed) |
| 3 | LandingPage | M | 1 | A landing page that the identifier resolves to. URL | [Infrastructure.url](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md) |
| 4 | Name | M | 1 | Name by which the instrument instance is known. Free text | [Infrastructure.title](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md) |
| 5 | Owner | M | 1–n | Institution(s) responsible for the management of the instrument. This may include the legal owner, the operator, or an institute providing access to the instrument. | A [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md) via [has-contribution](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md#user-content-rel__has-contribution), where the concrete subtype is:<br>– [Infrastructure_Ownership](../entities/Infrastructure_Ownership.md) for the legal owner,<br>– [Infrastructure_Operation](../entities/Infrastructure_Operation.md) for the operator,<br>– providing access to the instrument is not covered here, it should happen through a Service.<br>The managed entity (Agent) is linked with the Contribution via [has-actor](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Activity.md#user-content-rel__has-actor) |
| 5.1 | ownerName | | 1 | Full name of the owner. Free text | The linked Agent (Contribution_to_Infrastructure.has-actor), which is most likely a [Group or Organisation Unit](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Group_or_Organisation_Unit.md) and includes the name. If the Agent is a Person, her/his name may be stated in *display person name* in an [Affiliation Statement](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Affiliation_Statement.md) linked with the Contribution_to_Infrastructure |
| 5.2 | ownerContact | | 0–1 | Contact address of the owner. Electronic mail address | One of *contacts* in the Affiliation Statement linked with the Contribution_to_Infrastructure. The Email_Address subtype of Contact_Information should be used |
| 5.3 | ownerIdentifier | | 0–1 | Identifier used to identify the owner. Free text, should be a globally unique identifier | A concrete subtype of [Agent Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Agent_Identifier.md) which is linked with the Agent linked from Contribution_to_Infrastructure |
| 5.3.1 | ownerIdentifierType | | 1 | Type of the identifier | The subtype of Agent_Identifier (see general note 3) |
| 6–10 | Model information | | | (see the model information section below) | [Instrument_Instance.is-instance-of](../entities/Instrument_Instance.md#user-content-rel__is-instance-of) → [Instrument_Model](../entities/Instrument_Model.md) (the spreadsheet writes this as `Infrastructure_Instance.model`) |
| 11 | Date | R | | – dateType=Commissioned<br>– dateType=DeCommissioned | The *date range* of the Operating (Infrastructure_Operation) Contribution to Infrastructure:<br>– dateType=Commissioned → Date_Range.startDate<br>– dateType=DeCommissioned → Date_Range.endDate |
| 12 | RelatedIdentifier | R | | Identifiers of related resources. Free text, must be globally unique identifiers | (see the relationType rows below) |
| 12 | relationType=IsDescribedBy | | 0–n | The linked resource is a document describing the instrument | [Resource.has-description](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__has-description) |
| 12 | relationType=IsNewVersionOf | | 0–n | If an instrument is substantially modified, a new PID may be attributed to the new version. In that case the old and the new PID should be linked to each other. IsNewVersionOf should be used in the new PID record to link the old instrument before the modification. | [Resource.is-new-version-of](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__is-new-version-of) |
| 12 | relationType=IsPreviousVersionOf | | 0–n | As above; IsPreviousVersionOf should be used in the old PID record to link the new instrument after the modification. | [Resource.is-previous-version-of](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__is-previous-version-of) |
| 12 | relationType=HasComponent | | 0–n | In the case of a complex instrument, having multiple components that may be considered as instruments in their own right, with their own PIDs, these PIDs should be linked. HasComponent should be used in the PID record of the compound instrument to link the components. | [Resource.has-part](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__has-part) |
| 12 | relationType=IsComponentOf | | 0–n | As above, from the PID records of the components to link the compound instrument. | [Resource.is-part-of](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__is-part-of) |
| 12 | relationType=References | | 0–n | This may be used in the generic case, if no other more specific relation type applies. | — (not supported, as this is very generic; not bearing enough information on the type of relationship) |
| 12 | relationType=HasMetadata | | 0–n | If there is additional metadata describing the instrument, possibly using a community specific metadata standard, that metadata record may be linked using HasMetadata. | [Resource.has-description](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__has-description) (written as `Resource.is-described-by` in the spreadsheet) with relation to a [Metadata_Set](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Metadata_Set.md) (a subtype of [Document](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Document.md)). Note: Core also offers [has-metadata](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__has-metadata) / is-metadata-of for metadata descriptions; this mapping follows the spreadsheet |
| 12 | relationType=WasUsedIn | | 0–n | If the instrument has been deployed in some research activity, such as a cruise of a research vessel, WasUsedIn may be used to link that activity. | [Resource.is-used-in](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md#user-content-rel__is-used-in) → [Resource Usage Statement](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Usage_Statement.md) → *details* → Contribution Statement → *references* → [Contribution](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution.md) (an Activity, i.e. the research activity the instrument was deployed in) |
| 12 | relationType=IsIdenticalTo | | 0–n | If multiple PIDs have been attributed to a single instrument (which should preferably be avoided in the first place), these PID records should be linked to each other using IsIdenticalTo. | When this happens, it can be represented through multiple Resource_Identifiers linked to the same Infrastructure resource |
| 12 | relationType=IsAttachedTo | | 0–n | If the instrument is permanently attached to another instrument, the PID records for both instruments should link to each other using IsAttachedTo. | — (not supported at this stage, as this is a very particular use-case, not likely to be found in real-world instrument metadata; not supported by DataCite Metadata Schema either) |
| 13 | AlternateIdentifier | R | | Identifiers other than PIDINST pertaining to the same instrument instance. This should be used if the instrument has a serial number. Other possible uses include an owner's inventory number or an entry in some instrument data base. Free text, should be unique identifiers. | Concrete subtypes of [Instrument_Instance_Identifier](../entities/Instrument_Instance_Identifier.md) (a subtype of Resource_Identifier), attached via has-identifier. Note: the identifiers are not likely to be globally unique, so care should be exercised — it would be nice to also record the context in which they are meaningful, where this information is available. |
| 13.1 | alternateIdentifierType=SerialNumber | | 0–n | | [Serial_Number](../entities/Serial_Number.md) as a subtype of Resource_Identifier |
| 13.2 | alternateIdentifierType=InventoryNumber | | 0–n | | [Inventory_Number](../entities/Inventory_Number.md) as a subtype of Resource_Identifier |
| 13.3 | alternateIdentifierType=Other | | 0–n | | [Other_Instrument_Instance_Identifier](../entities/Other_Instrument_Instance_Identifier.md) as a subtype of Resource_Identifier |

## Model information from PIDINST record → [Instrument Model](../entities/Instrument_Model.md)

The model information (items 6–10) is mapped to Instrument Model, a subclass of Core [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md), referenced from the instance via [is-instance-of](../entities/Instrument_Instance.md#user-content-rel__is-instance-of) / [has-instance](../entities/Instrument_Model.md#user-content-rel__has-instance).

| ID | Property | Obl | Occ | PIDINST definition (and constraints) | Refactored CERIF |
|----|----------|-----|-----|--------------------------------------|------------------|
| 6 | Manufacturer | M | 1–n | | [Manufacturing](../entities/Manufacturing.md) (a subtype of Contribution to Infrastructure); its actor (has-actor) is the manufacturer |
| 6.1 | manufacturerName | | 1 | | Group_or_Organisation_Unit.name or Person.name or *display person name* in an Affiliation Statement (where the Affiliation Statement is linked to this Contribution to Infrastructure) |
| 6.2 | manufacturerIdentifier | | 0–1 | Identifier used to identify the manufacturer. Free text, should be a globally unique identifier. | A concrete subclass of [Agent Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Agent_Identifier.md) |
| 6.2.1 | manufacturerIdentifierType | | 1 | Type of the identifier | The subclass of Agent_Identifier (see general note 3) |
| 7 | Model | R | 0–1 | Name of the model or type of device as attributed by the manufacturer | — (see 7.1 and 7.2) |
| 7.1 | modelName | | 1 | Full name of the model. Free text. | Infrastructure.title (of the Instrument Model) |
| 7.2 | modelIdentifier | | 0–1 | Identifier used to identify the model. Free text, should be a globally unique identifier. | [Instrument_Model_Identifier](../entities/Instrument_Model_Identifier.md) (subclass of Resource_Identifier) |
| 7.2.1 | modelIdentifierType | | 1 | Type of the identifier. Free text, see note. | — (not mapped at this stage; if meaningful concrete types of model identifiers are found, we may introduce them as subtypes of Instrument_Model_Identifier) |
| 8 | Description | | 0–1 | Technical description of the device and its capabilities. Free text. | Infrastructure.description — not yet defined in CERIF Core; to be added there, or as a module-level attribute (see [TODO.md](../TODO.md)) |
| 9 | InstrumentType | R | 0–n | Classification of the type of the instrument | [Instrument_Model.has-type](../entities/Instrument_Model.md#user-content-rel__has-type) → [Instrument_Model_Type](../entities/Instrument_Model_Type.md) (controlled vocabulary) |
| 9.1 | instrumentTypeName | | 1 | Full name of the instrument type. Free text, see note. | The `label` attribute of [Instrument_Model_Type](../entities/Instrument_Model_Type.md) |
| 9.2 | instrumentTypeIdentifier | | 0–1 | Identifier used to identify the type of the instrument. Free text, should be a globally unique identifier. | — (no individual mapping; the identifier is a property of the Instrument_Model_Type value) |
| 9.2.1 | instrumentTypeIdentifierType | | 1 | Type of the identifier. Free text, see note. | — |
| 10 | MeasuredVariable | R | 0–n | The variable(s) that this instrument measures or observes. Free text. | Instrument_Model.measuredVariable (free text, 0–n) |

## Unmapped and open items

- item 2 SchemaVersion — not mapped (fixed value "1.0")
- item 7.2.1 modelIdentifierType — not mapped at this stage
- item 12 relationType=References — not supported (too generic)
- item 12 relationType=IsAttachedTo — not supported at this stage
- providing access to the instrument via a Service (general note 2) — not covered by this module
- open questions from the spreadsheet (no decision yet):
  - possibly an intermediate entity **Group_of_Instruments**?
  - number of instruments (in a group?)
  - location (of the instrument instance?)
  - responsible person / organisation unit?
