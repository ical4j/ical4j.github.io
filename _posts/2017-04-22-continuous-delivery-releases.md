---
layout: post
title: iCal4j Continuous Delivery Releases
---

To support a move to a Continuous Delivery style release process we will be introducing a new Git branch as the 
development stream branch. This will allow us to support testing the integration of features and bugfixes prior to the 
automated release builds.

Release builds will occur automatically from the master branch, so for each merge to this branch a new release will be
generated. Hopefully this will provide a more regular release process that is more responsive to the community.
