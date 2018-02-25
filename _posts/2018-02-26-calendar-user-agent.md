---
layout: post
title: Calendar User Agent
---

Calendar User Agent is the term applied to any application implementing support for the iCalendar and associated
interoperability specifications. Until now, iCal4j provided support for creating, parsing, and validating iCalendar
objects but didn't provide the full functionality required to implement a Calendar User Agent.

With the next release iCal4j improves support for the iCalendar Transport-Independent Interoperability
Protocol ([iTIP]), by providing User Agents to make it easier to interact with other CUAs.

## User Agents

There are User Agent implementation for each of the components support by the [iTIP] protocol, with each agent
implementing the applicable iCalendar methods. The User Agent will ensure the appropriate properties are set at
both calendar and component-level, providing a simpler and more consistent approach to calendar interoperability.

## Method Transformers

Behind the User Agent implementations are Transformer implementations for each of the iCalendar methods. Each
transformer applies the necessary transformations to the specificed iCalendar object to meet the requirements of the
iCalendar method interaction. These transformers may be used independently of the User Agents, offering more
flexibility to choose how to implement iTIP support.

## Examples

The following examples demonstrate some of the use-cases for User Agents.

### Publish an event

When publishing an event the user agent will ensure the calendar METHOD property is set to PUBLISH; each event
UID exists; and each event ORGANIZER is set to the current user.

```
VEventUserAgent userAgent = ...
ContentBuilder builder = ...

Calendar calendar = userAgent.publish(builder.vevent {
	summary 'Spring Equinox'
	dtstamp()
	dtstart '20090810', parameters: parameters { value 'DATE' }
	action 'DISPLAY'
	attach'http://example.com/attachment', parameters: parameters { value 'URI' }
});
```

### Initiate a meeting request

```
VEventUserAgent userAgent = ...
ContentBuilder builder = ...

Calendar calendar = userAgent.request(builder.vevent {
	uid '1'
	summary 'Spring Equinox'
	dtstamp()
	dtstart '20090810', parameters: parameters { value 'DATE' }
	action 'DISPLAY'
	attach'http://example.com/attachment', parameters: parameters { value 'URI' }
	attendee 'mailto:organizer@example.com'
});
```

[iTIP]: https://tools.ietf.org/html/rfc5546
