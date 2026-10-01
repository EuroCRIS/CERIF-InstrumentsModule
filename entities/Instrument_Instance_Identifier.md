# Instrument Instance Identifier

## Definition
An identifier other than a PID that identifies an [Instrument Instance](../entities/Instrument_Instance.md).

## Usage notes
Besides its PID, an instrument instance can carry other identifiers, for instance a serial number, an owner's inventory number, or an entry in some instrument data base.
The concrete subtype of this class records the kind of the identifier: [Serial Number](../entities/Serial_Number.md), [Inventory Number](../entities/Inventory_Number.md), or [Other Instrument Identifier](Other_Instrument_Instance_Identifier.md).
Note that such identifiers are not likely to be globally unique; where available, the context in which the identifier is meaningful should be recorded together with it.

## Specialization of
[Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md)

## Attributes
None besides those of [Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md).

## Relationships
None besides those of [Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md).

## Constraints
The only admissible class for the target of the [Resource Identifier.is-assigned-to](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md#user-content-rel__is-assigned-to) relationship is [Instrument Instance](../entities/Instrument_Instance.md).
