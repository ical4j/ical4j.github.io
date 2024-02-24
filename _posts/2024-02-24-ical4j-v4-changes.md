---
layout: post
title: iCal4j v4 Changes
---

The following is a summary of the changes in iCal4j v4 that may present some challenges when upgrading from
v3 or earlier versions.

## Minimum Java 11

iCal4j v3 required a minimum of Java 8, due to the use of Java streams and time APIs. With iCal4j v4 we have
decided to implement Java modules (added in Java 9) and with Java 11 being the next LTS version following Java 8,
this will now be the new minimum.

## Java Modules

If you use Java modules you should see better support in iCal4j v4, however feedback is always appreciated if this
can be improved.

## New Date/Time API

iCal4j v4 is now based entirely on the new Date/Time API introduced in Java 8. This will have the biggest impact
on existing code using prior versions as it will need to be refactored to use the new APIs.

As always, please provide feedback on this release via Github [issues](https://github.com/ical4j/ical4j/issues)
and [discussions](https://github.com/orgs/ical4j/discussions).
