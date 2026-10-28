# Infrastructure Operation

## Definition
Operating an [Instrument Instance](../entities/Instrument_Instance.md) or providing access to it on behalf of its [owner](../entities/Infrastructure_Ownership.md).

## Usage notes
While the owner (= the [Agent](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Agent.md) in the [Infrastructure Ownership](../entities/Infrastructure_Ownership.md)) of an instrument is typically a research-performing organisation,
the operator (= this [Agent](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Agent.md) in this entity) is typically a subunit that has been made responsible for the instrument.
In case the instrument is lent, it may also be another organisation's subunit.
The [Activity](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Activity.md)'s (the ur-ancestor of the class hierarchy) [dateRange](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Activity.md) property may indicate when the recorded relationship between the [Agent](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Agent.md) and the [Instrument Instance](../entities/Instrument_Instance.md) is/was true.
In particular, a change of the operator does not imply that the instrument was decommissioned and commissioned again: the lifecycle (commissioned/decommissioned) dates are recorded with the [Infrastructure Ownership](../entities/Infrastructure_Ownership.md) contribution instead (cf. the [PIDINST mapping](../mappings/PIDINST-v1.0.md), item 11).

## Specialization of
[Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md)

## Attributes
None besides those of [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md).

## Relationships
None besides those of [Contribution to Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md).

## Constraints
The only admissible class for the target of the [Contribution to Infrastructure.has-target](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Contribution_to_Infrastructure.md#user-content-rel__has-target) relationship is [Instrument Instance](../entities/Instrument_Instance.md).
