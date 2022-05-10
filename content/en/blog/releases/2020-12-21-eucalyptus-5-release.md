---
title: "Eucalyptus 5 Released"
date: 2020-12-21
tags:
- announcement
- release
- eucalyptus-5
---

Eucalyptus Cloud 5 is now available, this major release includes a new Ansible based installer and
technical previews for Route53 and SQS (Simple Queue Service)

In addition to the headline features, there are many smaller changes to improve the AWS compatibility
and performance of Eucalyptus Cloud.

<!--more-->

## New in Eucalyptus 5

Some new features in Eucalyptus 5 are:

* Ansible [installer](https://docs.eucalyptus.cloud/eucalyptus/5/install_guide/automated_install/)
* Auto Scaling instance protection
* CloudFormation support for YAML templates
* EC2 iam instance profile association
* EC2 long resource identifiers
* [Route53 service](https://docs.eucalyptus.cloud/eucalyptus/5/user_guide/route53_intro/) technical preview
* S3 bucket policy support
* [SQS service](https://docs.eucalyptus.cloud/eucalyptus/5/user_guide/sqs_intro/) technical preview

Other notable changes in Eucalyptus 5 are:

* Cluster controller now part of main cloud service
* Java runtime updated to version 11
* Reporting service removed

Full details of changes in Eucalyptus 5 are available in the
[Corymbia github project](https://github.com/orgs/Corymbia/projects/3) and
[milestone](https://github.com/Corymbia/eucalyptus/milestone/3?closed=1)

## Try Eucalyptus 5

You can try Eucalyptus 5 with a FastStart install by running:

{{< highlight shell >}}
> bash <(curl -Ls https://get.eucalyptus.cloud)
{{< / highlight >}}

as root, on a CentOS/RHEL 7.9 minimal install with a few IP addresses to spare.

## Miss Eucalyptus 4.4.x?

Eucalyptus 5 look a little different from 4.4.x due to changes with instance types and long
identifiers. If you want to try Eucalyptus 5 but with a 4.4.x feel, you can make changes as
follows.

To disable EC2 long identifiers, run the following as an administrator:

{{< highlight shell >}}
> euctl cloud.short_identifier_prefixes='*'
{{< / highlight >}}

changing this setting will cause any new resources to be created with short identifiers (where
supported). You can have a mix of short and long identifiers depending on settings when those
resources were created.

To change instance types to be the same as 4.4.x, run the following as an administrator:

{{< highlight shell >}}
> euform-create-stack \
  --template-file /usr/share/eucalyptus/doc/ec2-instance-types-eucalyptus-4.yaml \
  eucalyptus-4-instance-types
> euctl cloud.vmtypes.default_type_name=m1.medium
> euctl services.imaging.worker.instance_type=m1.medium
> euctl services.loadbalancing.worker.instance_type=m1.medium
{{< / highlight >}}

this will enable 4.4.x instance types and disable the default Eucalyptus 5 instance types. The
default instance type and the types used for services are updated accordingly.

## Moving to Eucalyptus 5?

Upgrading from previous releases to Eucalyptus 5 is not supported. If moving to Eucalyptus 5
data such as S3 objects and EBS volumes can be copied from existing deployments before they
are retired.

# Thanks!

Thanks for giving Eucalyptus 5 a try and please use [github issues](https://github.com/Corymbia/eucalyptus/issues)
to report any problems you encounter to help improve Eucalyptus.
