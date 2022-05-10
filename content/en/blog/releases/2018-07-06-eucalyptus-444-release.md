---
title: "Eucalyptus 4.4.4 Released"
date: 2018-07-06
tags:
- announcement
- release
---

Eucalyptus Cloud 4.4.4 has been released, updating our OS support to allow use of CentOS and RHEL 7.5 in addition to
the existing support for 7.3 and 7.4.

This release was tested using updated qemu packages which should be installed when upgrading. This updates qemu to 2.9.0
from the 2.6.0 version previously distributed.

<!--more-->

Some fixes of note in this release are:

* The object storage gateway is updated to use less resources for background maintenance when there are buckets with many objects
* The node controller would sometimes leave artifacts behind for terminated instances causing unnecessary disk use

You can find the full list of 
[resolved issues](https://docs.eucalyptus.cloud/eucalyptus/4.4.4/index.html#release-notes/4.4.4/4.4.4_rn_resolved.html) 
in the release notes.

If upgrading from 4.4.2 or earlier, note that the RPM repository location has changed, updated Eucalyptus and Euca2ools 
release RPMs should be installed as detailed in the 
[install guide](https://docs.eucalyptus.cloud/eucalyptus/4.4.4/install-guide/installing_euca_release.html)
so that the new downloads.eucalyptus.cloud location is used.
