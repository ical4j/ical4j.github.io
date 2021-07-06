---
layout: post
title: Support for non-Gregorian recurrence rules
---
The latest release of iCal4j (3.0.28) now includes partial support for [RFC7529], a.k.a. non-Gregorian
recurrence rules.

This specification allows for recurrences using alternative calendaring systems, by introducing notation for a
"leap month", and specification of "skip" behaviour when the recurrence rule isn't applicable for a subset of dates
(e.g. February 29th isn't applicable for non-leap years, etc.).

The specification also provides support for specifying the chronology of the recurrence rule, which iCal4j uses
to provide extra validation of BY* rules (i.e. check valid range for the specified chronology).

The release of iCal4j v4 will provide complete support for the specification as it will allow for alternate chronologies
when calculating the recurrence instances (iCal4j v3.x only supports Gregorian instance calculation).

NOTE: As iCal4j v3.x cannot support the leap month concept entirely, skip behaviour will always be used when calculating
recurrence instances (e.g. `BYMONTH=5L;SKIP=FORWARD` will always evaluate to `June` in the current implementation).

[RFC7529]: https://datatracker.ietf.org/doc/html/rfc7529
