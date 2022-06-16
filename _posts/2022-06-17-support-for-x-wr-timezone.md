---
layout: post
title: Support for X-WR-TIMEZONE
---

The question of how to interpret the `X-WR-TIMEZONE` calendar property has a very long history, and one that to
my knowledge has never been resolved. Unlike most other non-standard properties, the use of `X-WR-TIMEZONE` may 
impact the portability of iCalendar data depending on the assumptions made by the publisher and consumers.

Until now, iCal4j had no support for this non-standard property, apart from the `WrTimeZone` property included in
the ical4j-extensions library. But with iCal4j v4 there are two notable changes that improve support for a default
calendar timezone.

## Changes to Date properties in iCal4j v4

With earlier versions of iCal4j a `DateProperty` contained a reference to a Date (or DateTime) instance, as well as
an optional TimeZone. This timezone was actually just a reflection of the encapsulated DateTime timezone, but 
changing it could also alter the property `TZID` parameters also, which may be seen as an unexpected behaviour.

In iCal4j v4 this behaviour has been reversed, such that a change to the `TZID` parameter will automatically be
reflected in the rendering of the property value. This means that we no longer need to keep a reference to a timezone
(or ZoneId) at all, apart from the TzId parameter.

## Setting a default Timezone

But what happens when we remove the TzId parameter from a ZonedDateTime date property? Well the default behaviour
is to use the system default timezone to render the value, so in effect the property becomes a floating DATE-TIME
value. There is however another change coming in iCal4j v4 that will allow a date property to have a default timezone.

The new method `DateProperty.setDefaultTimeZone(ZoneId)` is provided for scenarios where properties may not have a
`TZID` parameter, but you don't want to use the system default timezone for rendering. The `X-WR-TIMEZONE` calendar
property is one example of this, where you may want to use this calendar-scoped timezone for rendering any floating
dates in that specific calendar instance.

There are still some further changes required to support parsing and building objects with a default calendar
timezone, but this should be ready for the next beta release (beta2).
