---
layout: post
title: Timezone updates and tzurl.org
---

Starting with iCal4j releases 3.2.7 and 4.0.0-beta3 there are some minor changes with how the timezone update
functionality works. These changes include:

* The default update site will be changing to [https://www.tzurl.org]() (was previously [http://tzurl.org]())
* Additional configuration options support overriding the default update site
* Caching of timezone loaders to improve overall performance

## New timezone update site

The update site https://www.tzurl.org is hosted on 100% serverless architecture, which should improve
reliability and security of timezone updates. Whilst the default scheme is HTTPS, non-TLS requests are also
supported on the new site for backwards compatibility.

## Configuration for update site overrides

Three new configuration options are supported to override the scheme (i.e. HTTP/S), host and port of the update
site. This will allow iCal4j users to revert to non-TLS updates, or self-host a timezone update site.

For example, to revert to the old update site you can use the following configuration:

    net.fortuna.ical4j.timezone.update.scheme=http
    net.fortuna.ical4j.timezone.update.host=tzurl.org
    net.fortuna.ical4j.timezone.update.port=80


## Timezone loader caching

All timezone registries will now share a cache of timezone loaders that will reduce the number of update requests
and improve performance. Previously a new loader instance was created for each registry, whereby default timezones
would need to be reloaded and updated. This would happen by default for every new parsing of a calendar object.

With timezone loader caching the same loader is used across all timezone registries, resulting in faster object
parsing due to the timezones being loaded and updated only once.

Please provide feedback or bug reports if you see any issues with this new functionality.
