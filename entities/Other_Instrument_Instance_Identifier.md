# Other Instrument Instance Identifier

## Definition
Any other identifier pertaining to an [Instrument Instance](../entities/Instrument_Instance.md), for instance an entry in some instrument database.

## Usage notes
This is the subtype used when the concrete kind of the identifier is none of the other kinds offered: [Serial Number](../entities/Serial_Number.md) or [Inventory Number](../entities/Inventory_Number.md).
The [name](#attributes) attribute tells which type that other identifier actually is.

## Specialization of
[Instrument Instance Identifier](../entities/Instrument_Instance_Identifier.md)

## Attributes
Besides those of [Instrument Instance Identifier](../entities/Instrument_Instance_Identifier.md):

value : [String](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/String.md) – the identifier itself

name : [String](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/String.md) – a supplementary name for the identifier type, typically the instrument database or registry the identifier is an entry in

## Relationships
None besides those of [Instrument Instance Identifier](../entities/Instrument_Instance_Identifier.md).

## Constraints
The only admissible class for the target of the [Resource Identifier.is-assigned-to](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md#user-content-rel__is-assigned-to) relationship is [Instrument Instance](../entities/Instrument_Instance.md).
