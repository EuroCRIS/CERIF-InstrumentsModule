# Instrument Model Identifier

## Definition
An identifier used to identify an [Instrument Model](../entities/Instrument_Model.md).

## Specialization of
[Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md)

## Attributes
Besides those of [Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md):

model designation : [String](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/String.md)

## Relationships
None besides those of [Resource Identifier](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md).

## Constraints
The only admissible class for the target of the [Resource Identifier.is-assigned-to](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Resource_Identifier.md#user-content-rel__is-assigned-to) relationship is [Instrument Model](../entities/Instrument_Model.md).
