# Instrument Model

## Definition
A model of a device or tool used for scientific purposes, including the study of both natural phenomena and theoretical research.<sup>[1](#fn1)</sup>

## Usage notes
This entity represents a class of devices of one type.\
Even a unique [Instrument Instance](../entities/Instrument_Instance.md) should have its Instrument Model to represent its important properties.

## Specialization of
[Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md)

## Attributes
None besides those of [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md).

## Relationships
Besides those of [Infrastructure](https://github.com/EuroCRIS/CERIF-Core/blob/main/entities/Infrastructure.md):

<a name="rel__has-instance">has-instance</a> / [is-instance-of](../entities/Instrument_Instance.md#user-content-rel__is-instance-of) : An Instrument Model can have any number of [Instrument Instances](../entities/Instrument_Instance.md).

<a name="rel__has-type">has-type</a> / [is-type-of](../entities/Instrument_Model_Type.md#user-content-rel__is-type-of) : An Instrument Model can have a number of [Instrument Model Types](../entities/Instrument_Model_Type.md).

---
## References
<a name="fn1">\[1\]</a> Source: Adapted from the Wikipedia *[Scientific Instruments](https://en.wikipedia.org/wiki/Scientific_instrument)* article as of 2026-09-28, which attributes the formulation to:\
Hessenbruch, Arne (2013). *Reader's Guide to the History of Science*. Taylor & Francis. pp. 675–77. ISBN 9781134263011.
