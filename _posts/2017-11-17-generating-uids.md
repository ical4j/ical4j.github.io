---
layout: post
title: Generating UIDs
---

In the [RFC5545] iCalendar specification on which the iCal4j library is based, it provides the following guidelines
for generating unique identifiers (UIDs):

      The "UID" itself MUST be a globally unique identifier.
      The generator of the identifier MUST guarantee that the identifier
      is unique.  There are several algorithms that can be used to
      accomplish this.  A good method to assure uniqueness is to put the
      domain name or a domain literal IP address of the host on which
      the identifier was created on the right-hand side of an "@", and
      on the left-hand side, put a combination of the current calendar
      date and time of day (i.e., formatted in as a DATE-TIME value)
      along with some other currently unique (perhaps sequential)
      identifier available on the system (for example, a process id
      number).  Using a DATE-TIME value on the left-hand side and a
      domain name or domain literal on the right-hand side makes it
      possible to guarantee uniqueness since no two hosts should be
      using the same domain name or IP address at the same time.  Though
      other algorithms will work, it is RECOMMENDED that the right-hand
      side contain some domain identifier (either of the host itself or
      otherwise) such that the generator of the message identifier can
      guarantee the uniqueness of the left-hand side within the scope of
      that domain.

In the more recent specification for iCalendar extensions ([RFC7986]) the following advice for generating UIDs is offered:

     The description of the "UID" property in [RFC5545] contains some
     recommendations on how the value can be constructed.  In particular,
     it suggests use of host names, IP addresses, and domain names to
     construct the value.  However, this is no longer considered good
     practice, particularly from a security and privacy standpoint, since
     use of such values can leak key information about a calendar user or
     their client and network environment.  This specification updates
     [RFC5545] by stating that "UID" values MUST NOT include any data that
     might identify a user, host, domain, or any other security- or
     privacy-sensitive information.  It is RECOMMENDED that calendar user
     agents now generate "UID" values that are hex-encoded random
     Universally Unique Identifier (UUID) values as defined in
     Sections 4.4 and 4.5 of [RFC4122].

     The following is an example of such a property value:

     UID:5FC53010-1267-4F8E-BC28-1D7AE55A7C99


To support freedom of choice iCal4j will soon support both of the approaches listed above.

* `FixedUidGenerator` - renamed from `UidGenerator`
* `RandomUidGenerator` - a new implementation to support the [RFC7986] approach

[RFC5545]: https://tools.ietf.org/html/rfc5545
[RFC7986]: https://tools.ietf.org/html/rfc7986
