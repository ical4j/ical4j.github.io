---
layout: post
title: iCal4j JavaScript Object Notation Library
---

Whilst there are a number of iCalendar implementations available across many different languages, sometimes we may
want a convenient way to pass calendar information without needing a full compliant iCalendar parser.

JavaScript Object Notation (JSON) has become a common means for data transfer and is well-supported across many
languages. As such, there are a couple of specification that define translations of iCalendar data to/from JSON.

The [iCal4j JSON] library aims to provide an implementation of the [jCal] and [JSCalendar] specifications such that the iCal4j
object model can be easily converted to (and from) JSON representations.

The initial release is not yet a complete implementation, but feel free to provide feedback and additions to help
accelerate the development.

[iCal4j JSON]: http://github.com/ical4j/ical4j-json
[jCal]: https://tools.ietf.org/html/rfc7265
[JSCalendar]: https://tools.ietf.org/html/draft-ietf-calext-jscalendar-32
