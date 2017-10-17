---
layout: post
title: TimeZone Caching
---

The latest release of iCal4j includes caching of VTimezone definitions
used to populate the TimeZoneRegistry. This will improve load times due to reduced
IO and network utilisation.

As a result of this caching a new dependency on the jcache API has been introduced.
This means you will need to include an implementation of a jcache CachingProvider in
your runtime dependencies. Typically this is as easy as adding one of the well-known
cache dependencies (e.g. ehcache, hazelcast, ignite, etc.), but you can also provide
more sophisticated caching configurations as required. Note that the ical4j timezone
cache is called "ical4j.timezones".

A list of possible caching provider implementations is available from the [JCACHE] website.

[JCACHE]: https://jcp.org/aboutJava/communityprocess/implementations/jsr107/index.html
