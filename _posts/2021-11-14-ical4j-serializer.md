---
layout: post
title: iCal4j Serializer
---

Introducing the [iCal4j Serializer] library for conversion of iCalendar data to/from other formats. This library
is the successor to the `ical4j-json` library, and reflects the additional scope to include support for other
formats such as XML-based standards.

The [iCal4j Serializer] library aims to provide an implementation of specifications such as [jCal], [xCal] and 
[JSCalendar], such that the iCal4j object model can be easily converted to (and in some cases from) these other
representations.

The initial release is not yet a complete implementation, but feel free to provide feedback and additions to help
accelerate the development.

[iCal4j Serializer]: http://github.com/ical4j/ical4j-serializer
[jCal]: https://tools.ietf.org/html/rfc7265
[xCal]: https://www.rfc-editor.org/rfc/rfc6321.html
[JSCalendar]: https://tools.ietf.org/html/draft-ietf-calext-jscalendar-32
