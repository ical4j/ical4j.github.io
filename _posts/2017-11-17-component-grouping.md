---
layout: post
title: Component Grouping
---

An iCal4j `Calendar` object maintains list of component instances such as VEVENT, VTODO, VFREEBUSY, etc. Although each of these
component instances are defined independently, some of the may be linked as either revisions or exceptions to the original definition.
In the [RFC5545] specification this is defined as follows:

      When a calendar component is created, its sequence
      number is 0.  It is monotonically incremented by the "Organizer's"
      CUA each time the "Organizer" makes a significant revision to the
      calendar component.

      The "Organizer" includes this property in an iCalendar object that
      it sends to an "Attendee" to specify the current version of the
      calendar component.

      The "Attendee" includes this property in an iCalendar object that
      it sends to the "Organizer" to specify the version of the calendar
      component to which the "Attendee" is referring.

      A change to the sequence number is not the mechanism that an
      "Organizer" uses to request a response from the "Attendees".  The
      "RSVP" parameter on the "ATTENDEE" property is used by the
      "Organizer" to indicate that a response from the "Attendees" is
      requested.

      Recurrence instances of a recurring component MAY have different
      sequence numbers.
      
To support processing multiple linked components as a single entity the `ComponentGroup` class was recently added. This class allows
grouping of linked component instances to perform operations such as calulated recurrences, etc.

[RFC5545]: https://tools.ietf.org/html/rfc5545#section-3.8.5.1
