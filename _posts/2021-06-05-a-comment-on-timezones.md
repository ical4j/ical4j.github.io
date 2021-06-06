---
layout: post
title: A comment on timezones
---

You may be aware of some spirited discussion on the [iana.org/time-zones] mailing list regarding a recent change to
merge similar timezones (i.e. with common rules post-1970). 

This change has seen a lot of resistance and calls to
revert the decision, however if it does remain in place the following changes you can expect more aliases/redirects in
upcoming releases of the timezone definitions (and subsequently on sites such as [tzurl.org]):

The following list is indicative of how many timezones may be merged:

* africa (Africa/Abidjan, Ghana, Africa/Accra, Indian/Reunion)
  (Indian/Mahe)
* antarctica (Indian/Kerguelen, Antarctica/DumontDUrville)
  (Antarctica/Syowa, Antarctica/Vostok)
* asia (Asia/Brunei, Asia/Urumqi, NBorneo, Asia/Kuala_Lumpur)
  (Asia/Kuching, Indian/Maldives, Asia/Riyadh, Asia/Bangkok)
  (Asia/Dubai)
* australasia (Indian/Christmas, Indian/Cocos, Pacific/Gambier)
  (Pacific/Tahiti, Pacific/Tarawa, Pacific/Majuro, Pacific/Chuuk)
  (Pacific/Pohnpei, Pacific/Palau, Pacific/Port_Moresby)
  (Pacific/Guadalcanal, Pacific/Funafuti, Pacific/Wake)
  (Pacific/Wallis)
* europe (Denmark, Europe/Copenhagen, Iceland, Atlantic/Reykjavik)
  (Lux, Europe/Luxembourg, Europe/Monaco, Neth, Europe/Amsterdam)
  (Norway, Europe/Oslo, Europe/Stockholm)
* northamerica (America/Blanc-Sablon, America/Atikokan)
  (America/Creston, Bahamas, America/Nassau)
* southamerica (America/La_Paz, America/Curacao, America/Cayenne)
  (Atlantic/South_Georgia, America/Port_of_Spain)

The [iana.org/time-zones] mailing list included extensive discussion on the pros and cons of the change, but I think
it is worth considering that timezone rules are defined somewhat arbitrarily by governments of states and regions, and
as a result we cannot predict what the future will hold.

A simplification today might lead to more complexity in the future, but we'll have to see how it plays out on the
mailing list.

[iana.org/time-zones]: https://www.iana.org/time-zones
[tzurl.org]: http://www.tzurl.org/index.html
