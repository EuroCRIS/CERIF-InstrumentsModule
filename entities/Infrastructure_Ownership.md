# Infrastructure Ownership

## Definition
Ownership of an [Instrument Instance](../entities/Instrument_Instance.md).

## Usage notes
The [date range](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Activity.md) of this contribution may carry the lifecycle dates of the [Instrument Instance](../entities/Instrument_Instance.md): the dates when it was commissioned ([Date Range.startDate](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/Date_Range.md)) and decommissioned ([Date Range.endDate](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/Date_Range.md)); see the [PIDINST mapping](../mappings/PIDINST-v1.0.md), item 11.
If there are multiple such periods, each of them is represented by its own Infrastructure Ownership contribution.

## Specialization of
[Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md)

## Attributes
None besides those of [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md).

## Relationships
None besides those of [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md).

## Constraints
The only admissible class for the target of the [Contribution to Infrastructure.has-target](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md#user-content-rel__has-target) relationship is [Instrument Instance](../entities/Instrument_Instance.md).

