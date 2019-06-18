---
layout: post
title: iCal4j 4 and the new Java date/time API
---
[jsr310]: https://www.threeten.org/
[Date]: http://ical4j.github.io/docs/ical4j/api/3.0.4/net/fortuna/ical4j/model/Date.html
[DateTime]: http://ical4j.github.io/docs/ical4j/api/3.0.4/net/fortuna/ical4j/model/DateTime.html
[DateList]: http://ical4j.github.io/docs/ical4j/api/3.0.4/net/fortuna/ical4j/model/DateList.html
[Period]: http://ical4j.github.io/docs/ical4j/api/3.0.4/net/fortuna/ical4j/model/Period.html

iCal4j 4 will introduce some of the biggest changes since creation of the library, based on support for the 
[new Java date/time api](https://www.threeten.org/). This includes a number of API changes and inevitably some change to behaviour, 
hopefully for the better.

## Dates

The most notable change is the deprecation of custom date and date-time classes in favour of implementations of the 
`java.time.Temporal` interface. Whilst the ical4j [Date] class has an direct replacement in `java.time.LocalDate`, there are now multiple
types representing date-time values, previously supported by the [DateTime] class.

## Formats

Previously date formatting was encapsulated by the implementation in [Date] and [DateTime] classes. As Temporal types don't implement
formatting we have introducted a `CalendarDateFormat` class to support parsing and formatting of temporal string values.

## TemporalAdapter

Many date-based iCalendar properties also support additional information not captured by temporal types, such as timezone rules and
support for "floating" date-time values that apply the local timezone to calculating recurrences, etc.

To support consistent application of timezone rules the `TemporalAdapter` class provides additional temporal operations through 
encapsulation of a temporal instance.

## DateList

Some iCalendar properties support a list of date/time values, and so the [DateList] class has been enhanced to provide consistency of rules
across an entire temporal list.

## Period

A period of time is represented by either two dates or a date and a duration. A [Period] encapsulates both the formatting functions 
and operations across both temporal and duration types. NOTE: The ical4j [Period] is not to be confused with the Java `Period` which is
a representation of a time interval in days, months, etc.

## PeriodList

To provide consistency of rules across multiple periods the [PeriodList] class has been enhanced to support these changes to temporal types.

## Date properties

In addition to parsing and formatting string values, in older versions of ical4j an iCalendar property with a date/date-time value would
also encapsulate a date implementation that supports timezone rules for date-time values.

The introduction of Temporal support means that string parsing/formatting is no longer encapsulated by the date/time object. In order to
support string manipulation wrapper class for Temporal has been introduced in TemporalAdapter.
