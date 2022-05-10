---
title: "Eucalyptus 4.4.5 Released"
date: 2018-12-31
tags:
- announcement
- release
---

Eucalyptus Cloud 4.4.5 has been released, updating our OS support to allow use of CentOS and RHEL 7.6 in addition to
the existing support for 7.3, 7.4, and 7.5.

This release has some important compatibility and functionality fixes and is recommended for all 4.4.x deployments.

<!--more-->

As with version 4.4.4, this release was tested using 2.9.0 qemu packages which should be installed when upgrading from
earlier versions.

Some fixes of note in this release are:

* The object storage gateway now supports version two object listing
* EC2 instances for some images could hang when starting

You can find the full list of
[resolved issues](https://docs.eucalyptus.cloud/eucalyptus/4.4.5/index.html#release-notes/4.4.5/4.4.5_rn_resolved.html)
in the release notes.

If upgrading from 4.4.2 or earlier, note that the RPM repository location has changed, updated Eucalyptus and Euca2ools
release RPMs should be installed as detailed in the
[install guide](https://docs.eucalyptus.cloud/eucalyptus/4.4.5/install-guide/installing_euca_release.html)
so that the new downloads.eucalyptus.cloud location is used.

