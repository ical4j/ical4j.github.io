---
layout: post
title: iCal4j and Groovy
---
Did you know you can use Groovy to build iCal4j objects? It can drastically reduce the amount of code you need to write.

Here is an example:
{% highlight groovy %}
ContentBuilder builder = []
def calendar = builder.calendar {
            prodid('-//Ben Fortuna//iCal4j 1.0//EN')
            version('2.0')
            vevent {
                uid('1')
                dtstamp()
                dtstart('20110919T150000Z')
                dtend('20110921T100000Z')
            }
		}
{% endhighlight %}