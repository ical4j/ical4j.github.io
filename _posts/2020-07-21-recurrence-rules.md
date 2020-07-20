---
layout: post
title: Recurrence Rules with iCal4j v4
---

Whilst iCal4j v4 introduces many visible (and breaking!) changes to the [API], there are also some underlying behavioural
changes that should also be noted. These changes may not always be (syntactically) obvious, so it is important to ensure
you have good unit test coverage prior to upgrading to capture any introduced bugs.

## Recurrence Rules

The logic underlying calculation of recurring instances was heavily refactored in iCal4j 3.x, which has made the process
of adopting the new Java date/time API more manageable. However, differences in how the old and new Java date/time APIs
work means that some calculations of recurrence instances will produce different results.

### BYWEEKNO

In particular the `BYWEEKNO` rule has a history of multiple interpretations regarding [edge-cases] and how they should
be handled. In adopting the new Java date/time API we are also changing the definition of the first week of the year,
as defined by [ISO 8601] as:

        * the week with the year's first Thursday in it (the formal ISO definition),
        * the week with 4 January in it,
        * the first week with the majority (four or more) of its days in the starting year, and
        * the week starting with the Monday in the period 29 December – 4 January.  

_NOTE:_ As an iCalendar recurrence rule can specify the starting day of the week (WKST) this can have further impact
on the first week of the year.

As is demonstrated in the iCal4j unit tests, the results for a number of edge-case tests is quite different in iCal4j v4
as compare to iCal4j 3.x. So if you do anticipate some of those edges cases ensure you provide good test coverage and
verify the expected results.
 
As usual, these changes are now available in [iCal4j Alpha6]. We welcome any feedback and bug reports via the Github 
issues page.

[iCal4j Alpha6]: https://search.maven.org/artifact/org.mnode.ical4j/ical4j

[API]: http://ical4j.github.io/docs/ical4j/api/4.0.0-alpha6/

[release notes]: http://ical4j.github.io/docs/ical4j/release-notes

[edge-cases]: https://github.com/ical4j/ical4j/pull/243

[ISO 8601]: https://en.wikipedia.org/wiki/ISO_8601#Week_dates