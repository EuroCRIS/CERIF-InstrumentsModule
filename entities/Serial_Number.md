# Serial Number

## Definition
A serial number assigned to an [Instrument Instance](../entities/Instrument_Instance.md), typically by the manufacturer.

## Specialization of
[Instrument Instance Identifier](../entities/Instrument_Instance_Identifier.md)

## Attributes
Besides those of [Instrument Instance Identifier](../entities/Instrument_Instance_Identifier.md):

serial number : [String](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/String.md)

## Relationships
None besides those of [Instrument Instance Identifier](../entities/Instrument_Instance_Identifier.md).

## Constraints
The only admissible class for the target of the [Resource Identifier.is-assigned-to](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md#user-content-rel__is-assigned-to) relationship is [Instrument Instance](../entities/Instrument_Instance.md).
