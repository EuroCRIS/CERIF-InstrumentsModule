# CERIF Instruments Module
This module contains classes and properties for modeling scientific instruments
in line with the *PIDINST v.1.0* specification (DOI [10.15497/RDA00070](https://doi.org/10.15497/RDA00070)).
The mapping is described in the document [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md).
The development of this module was done in the framework of the [INST-DSpace project](https://eurocris.org/projects/inst-dspace-project/) 
led by [euroCRIS](https://eurocris.org/) with funding from the [Vietsch Foundation](https://www.vietsch-foundation.org/).

## Status
2026-10-15 — for review

Some ideas of possible extensions in the future are listed in a [separate file](./IDEAS.md).

## Overview
Instruments – or more specifically [Instrument Instances](./entities/Instrument_Instance.md) – are [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md).
Instrument instances link information about their [models](./entities/Instrument_Model.md): several instrument instances can share a single model information record.
Instrument models can be classified by one or more [Instrument Model Types](./entities/Instrument_Model_Type.md).
Instrument instances are identified by [Instrument Instance Identifiers](./entities/Instrument_Instance_Identifier.md) — such as [Serial Numbers](./entities/Serial_Number.md), [Inventory Numbers](./entities/Inventory_Number.md) and other [identifiers](./entities/Other_Instrument_Instance_Identifier.md) — while models are identified by [Instrument Model Identifiers](./entities/Instrument_Model_Identifier.md).

An instrument instance can be linked with agents in the role of [owner](./entities/Infrastructure_Ownership.md) or [operation](./entities/Infrastructure_Operation.md); 
an instrument model is linked to its [maker](./entities/Manufacturing.md).

## Listings

### Entities
The Instruments Module consists of the following entities:
* [Resource](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource.md) (imported from [the CERIF Core](https://github.com/EuroCRIS/CERIF-Core))
  * [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md) (imported from [the CERIF Core](https://github.com/EuroCRIS/CERIF-Core))
    * [Instrument Instance](./entities/Instrument_Instance.md)
    * [Instrument Model](./entities/Instrument_Model.md)
  * [Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md) (imported from [the CERIF Core](https://github.com/EuroCRIS/CERIF-Core))
    * [Instrument Instance Identifier](./entities/Instrument_Instance_Identifier.md)
      * [Serial Number](./entities/Serial_Number.md)
      * [Inventory Number](./entities/Inventory_Number.md)
      * [Other Instrument Instance Identifier](./entities/Other_Instrument_Instance_Identifier.md)
    * [Instrument Model Identifier](./entities/Instrument_Model_Identifier.md)
* [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md) (imported from [the CERIF Core](https://github.com/EuroCRIS/CERIF-Core))
  * [Infrastructure Ownership](./entities/Infrastructure_Ownership.md)
  * [Infrastructure Operation](./entities/Infrastructure_Operation.md)
  * [Manufacturing](./entities/Manufacturing.md)
* [Instrument Model Type](./entities/Instrument_Model_Type.md)

## Illustrative Diagrams
![The module diagram](./diagrams/module.svg)

## Usage note
This module cannot be used without the core.

The module includes a [set of examples](./examples/README.md).

## Development

This module relies on the [CERIF-Core](https://github.com/EuroCRIS/CERIF-Core): we include some shared [entities](https://github.com/EuroCRIS/CERIF-Core/tree/main/entities) and [datatypes](https://github.com/EuroCRIS/CERIF-Core/tree/main/datatypes) from it and we also re-use the [building environment](https://github.com/EuroCRIS/CERIF-Core/tree/main/tools) for the diagrams. This module is developed in line with the [guidelines](https://github.com/EuroCRIS/CERIF-Core/tree/main/guidelines).
