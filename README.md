# CERIF Instruments Module
This module contains classes and properties for modeling scientific instruments.
The development started in the framework of the [INST-DSpace project](https://eurocris.org/projects/inst-dspace-project/)
led by [euroCRIS](https://eurocris.org/) with funding from the [Vietsch Foundation](https://www.vietsch-foundation.org/).

The module implements the *PIDINST v.1.0* specification (DOI [10.15497/RDA00070](https://doi.org/10.15497/RDA00070)),
the mapping is documented in [mappings/PIDINST-v1.0.md](mappings/PIDINST-v1.0.md). 
It was developed by [Jan Dvořák](https://orcid.org/0000-0001-8985-152X) and [Dragan Ivanović](https://orcid.org/0000-0002-9942-5521), assisted by Qwen3.8-27B run by the Computing and Information Centre of the Czech Technical University in Prague, CZ (https://ror.org/03kqpb082).

## Status
2026-10-15 — for internal review

Some ideas of possible extensions in the future are listed in [IDEAS.md](./IDEAS.md) file.

## Overview
Instruments – or more specifically, [Instrument Instances](./entities/Instrument_Instance.md) – are [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md).
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

## Usage notes
This module relies on the [CERIF-Core](https://github.com/EuroCRIS/CERIF-Core): we include some shared [entities](https://github.com/EuroCRIS/CERIF-Core/tree/main/entities) and [datatypes](https://github.com/EuroCRIS/CERIF-Core/tree/main/datatypes) from it.

The module includes a [set of examples](./examples/README.md).

## Development
This module is developed in line with the [guidelines](https://github.com/EuroCRIS/CERIF-Core/tree/main/guidelines).
It re-uses the [building tools](https://github.com/EuroCRIS/CERIF-Core/tree/main/tools).