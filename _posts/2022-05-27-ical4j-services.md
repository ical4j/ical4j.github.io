---
layout: post
title: iCal4j Services
---

The core focus of iCal4j has always been to provide libraries for Java that implement and support the iCalendar 
specifications (hence the "J" in iCal4j). With the introduction of iCal4j services it is hoped that some of that
benefit can now be extended to other languages also.

## What is iCal4j services?

In fact there is no single release for [iCal4j services], but rather just refers to some iCal4j libraries that
support deployment as a service. For example:

* iCal4j Validator
* iCal4j Serializer
* iCal4j FreeBusy
* iCal4j Query
* iCal4j User Agent
* ...

Each of these libraries are bundled with an HTTP Servlet and may be deployed either in a Web container or
standalone with an embedded Jetty server. They are stateless services and containerisation will be supported
to provide maximum choice in how they are deployed.

These services will extend some of the capabilities of iCal4j to non-Java applications, and mark the beginning
of a service-oriented focus for the iCal4j project.

[iCal4j Services]: https://www.ical4j.org/services.md
