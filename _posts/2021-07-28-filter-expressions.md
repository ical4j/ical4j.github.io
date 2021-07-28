---
layout: post
title: Filter expressions
---
The next release of iCal4j will include some changes to how object filtering is supported.

Earlier versions of iCal4j provided basic support for filtering components and properties by value inspection, etc.
Since the release of Java 8, much of this support was made redundant by support for functional predicates included
in the JDK.

Along with deprecating the old implementation, the next release will include support for *Filter Expressions*, that
are basically a convenient way of building complex functional predicates that may be used to filter standard Java
collections.

For example, to create a predicate for filtering events with a specific organizer you can do the following:

    Predicate<VEvent> filter = new FilterExpression().equalTo('organizer', 'Mailto:B@example.com').toComponentPredicate();
    List<VEvent> events = calendar.getComponents("vevent").stream().filter(filter).collect(Collectors.toList());

Or you may want to filter all todos without a due date:

    Predicate<VToDo> filter = new FilterExpression().notExists('due').toComponentPredicate();
    List<VToDo> todos = calendar.getComponents("vtodo").stream().filter(filter).collect(Collectors.toList());

There is also a basic parser that allows you to construct complex filter expressions using a basic query language:

    // filter events without attendees..
    Predicate<VEvent> filter = FilterExpression.parse("organizer = Mailto:B@example.com and attendee not exists").toComponentPredicate();
    List<VEvent> events = calendar.getComponents("vevent").stream().filter(filter).collect(Collectors.toList());

The parser incorporates some common functions to assist with constructing temporal-relative filters:

    // filter events in the next week..
    Predicate<VEvent> filter = FilterExpression.parse("dtstart > now() and dtstart <= endOfDay(+P1W)").toComponentPredicate();
    List<VEvent> events = calendar.getComponents("vevent").stream().filter(filter).collect(Collectors.toList());

    // filter overdue todos..
    Predicate<VToDo> filter = FilterExpression.parse("due <= startOfDay()").toComponentPredicate();
    List<VToDo> todos = calendar.getComponents("vtodo").stream().filter(filter).collect(Collectors.toList());

There are likely to be bugs in the implementation, so feel free to make suggestions and provide feedback via
[Github Issues](https://github.com/ical4j/ical4j/issues).
