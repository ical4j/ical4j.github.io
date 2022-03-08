---
layout: post
title: iCal4j Validation changes
---

The latest [iCal4j release] (v3.2.0) includes some major refactoring of the validation framework in order
to switch from exception-based reporting (i.e. via `ValidationException`) to a cumulative reporting approach
(via `ValidationResult`).

If you rely on validation please ensure you check the new method signatures and adjust your code accordingly.

See the [iCal4j User Guide] for more details.

[iCal4j release]: https://ical4j.github.io/docs/ical4j/api/
[iCal4j User Guide]: http://www.ical4j.org/validation/
