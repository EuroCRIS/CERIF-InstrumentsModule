# Manufacturing

## Definition
The fact of producing a specific [Instrument Model](../entities/Instrument_Model.md) or even a particular [Instrument Instance](../entities/Instrument_Instance.md).

## Usage notes
If the target of the [Contribution to Infrastructure.has-target](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md#user-content-rel__has-target) relationship is [Instrument Model](../entities/Instrument_Model.md), then this entity records by whom a model of instruments is/was being manufactured. This can possibly be amended by the information about the time range this was/is true (as [Activity.dateRange](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Activity.md)).

If the target of the [Contribution to Infrastructure.has-target](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md#user-content-rel__has-target) relationship is [Instrument Instance](../entities/Instrument_Instance.md), it records by whom a particular instrument piece was produced. A production date can be recorded as [Activity.dateRange.endDate](https://github.com/EuroCRIS/CERIF-Core/blob/main/datatypes/Date_Range.md).

## Specialization of
[Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md)

## Attributes
None besides those of [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md).

## Relationships
None besides those of [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md).

## Constraints
The only admissible targets of the [Contribution to Infrastructure.has-target](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md#user-content-rel__has-target) relationship are [Instrument Model](../entities/Instrument_Model.md) or [Instrument Instance](../entities/Instrument_Instance.md).
