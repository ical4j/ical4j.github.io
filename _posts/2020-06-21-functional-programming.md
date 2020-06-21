---
layout: post
title: Support for Functional Programming
---

In addition to support for the new Java date/time [API], iCal4j v4 will also aim to improve support for Functional
Programming patterns and features included since Java 8.

## Immutable Collections

In earlier releases we introduced custom collections (i.e. lists) for parameters, properties and components. The
primary purpose was to support custom string representations and other convenience methods. 

To improve support for Java 8 features like Lambda functions and streaming APIs, the following changes to these
collections will be introduced in iCal4j v4:

* Lists will no longer inherit from `ArrayList` - instead a new method `getAll()` provides access the underlying collection
* The underlying collections are now "Unmodifiable" - any mutation operations will now return a new instance of the
 list instead of modifying inline
* Convenience methods on property, component and calendar classes replace direct collection mutation

So as an example, thia approach to modify property parameters with earlier iCal4j versions will now fail:

    property.getParameters().add(newParam); // throws UnsupportedOperationException

Instead, this can be replaced with:

    property.add(newParam); // more concise and Thread-safe

Also, accessor methods have been deprecated in favour of new methods added to collection classes:

    property.getParameter(Parameter.VALUE); // old method: now Deprecated
    property.getParameters().getFirst(Parameter.VALUE); // new method: improves consistency of APIs
 
Similar methods are also available on calendar and component classes.


## Deep vs Shallow Copies

Often when modifying hierarchical data structures a deep copy is required to create new instances that don't impact
the original instances.

A common way to create a deep copy of a component, property or parameter is to use the corresponding `copy()` method.
In previous versions the implementations of this method haven't always been a true deep copy, and could result in shared
references across multiple instances.

With iCal4j v4 the deep copy implementation will ensure copies cannot impact the source instance, improving the support
for FP patterns.

For example, with iCal4j v3:

    VEvent eventCopy = event.copy(); // creates a new instance with a new property list and new alarm list
    
The concern here is that whilst the underlying collections have been replicated, the property and alarm instances
contained in them are not. This can be problematic if the properties in the copy are modified, as changes
will also reflect in the source instance.

With iCal4j v4:

    VEvent eventCopy = event.copy(); // creates a new instance with a new property list and new alarm list
    
Whilst the method signature is the same, underlying properties and alarms will also be copied to construct the new instance.
So any changes to properties and alarms in the copy won't be reflected in the source instance.

Sometimes however a shallow copy is sufficient and provides improved performance, especially with large data structures.

As a general rule, a shallow copy of iCal4j content is sufficient when mutation occurs only via direct mutator methods.

    VEvent copy = new VEvent(event.getProperties());
    copy.replace(new Summary("updated summary")); // safe
    
    copy.getProperties().getRequired(DTSTART).replace(new TzId("Australia/Melbourne")); // not safe!!
    
    DtStart dtstart = new DtStart(copy.getProperties().getRequired(DTSTART).getParameters());
    dtstart.replace(new TzId("Australia/Melbourne")); // safe
    copy.replace(dtstart);
    
The above example can be written slightly more succinctly using the `copy()` method:

    DtStart dtstart = copy.getProperties().getRequired(DTSTART).copy();
    dtstart.replace(new TzId("Australia/Melbourne")); // safe
    copy.replace(dtstart);


## Practical Examples

In practice these changes will have the greatest impact on how object instances are retrieved, copied and modified.
The following examples demonstrate some of the most significant changes.

### Change VEVENT summary

    calendar.getComponents().getRequired(VEVENT).replace(new Summary("updated summary"));
    
The above example retrieves the first `VEVENT` component from the calendar and creates a new property list instance
including the new summary and other existing properties.

### Change DTSTART timezone

    calendar.getComponents().getRequired(VEVENT).getProperties().getRequired(DTSTART).replace(new TzId("Australia/Melbourne"));
    
This example will create a new parameter list for the `DTSTART` property that includes the new timezone identifier.

These changes are available from [iCal4j Alpha4]. We welcome any feedback and bug reports via the Github issues page.

[iCal4j Alpha4]: https://search.maven.org/artifact/org.mnode.ical4j/ical4j

[API]: http://ical4j.github.io/docs/ical4j/api/4.0.0-alpha4/

[release notes]: http://ical4j.github.io/docs/ical4j/release-notes
