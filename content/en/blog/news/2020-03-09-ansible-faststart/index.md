---
title: "Eucalyptus 5 FastStart Ansible Playbook"
date: 2020-03-09
tags:
- eucalyptus-5
---

A new Ansible based FastStart install for single host Eucalyptus clouds is now
available for early access to Eucalyptus 5 pre-releases.

A FastStart deployment requires a CentOS 7.5-7.7 host with 16G memory and 100G disk
as the recommended host minimums. Ansible FastStart installs Eucalyptus with
Walrus object storage, overlay block storage, and vpcmido network mode. The
deployment is from Eucalyptus 5 nightly builds, so will always have the latest
pre-release functionality.

<!--more-->

## FastStart install

To install Eucalyptus 5 using the Ansible FastStart run (as root):

{{< highlight shell >}}
> bash <(curl -Ls https://go.euca.me/5eav)
{{< / highlight >}}

The interactive installer will check system prerequisites and prompt for the one
required configuration item, the VPC public IP address CIDR. Currently the installer
requires between a `/24` (~256 addresses) and a `/28` (~16 addresses) block, for
example:

* `192.168.100.0/24` for addresses `192.168.100.1` - `192.168.100.254`
* `192.168.1.128/25` for addresses `192.168.1.129` - `192.168.1.254`
* `192.168.2.192/26` for addresses `192.168.2.193` - `192.168.2.254`
* `192.168.3.224/27` for addresses `192.168.3.225` - `192.168.3.254`
* `192.168.4.240/28` for addresses `192.168.4.241` - `192.168.4.254`

If the target hosts IP was `10.20.30.40/24` then the CIDR used could be
`10.20.30.240/28`.

These addresses should not currently be in use, they will be used by instances in
the deployment.

## Post install

Once the installation completes a few configuration items are listed as next
steps. You could install machine images (ami/emi) using the new wrapper script:

{{< highlight shell >}}
> eucalyptus-images
{{< / highlight >}}

or get started with the management console by configuring the administrator
login:

{{< highlight shell >}}
> euare-useraddloginprofile --as-account eucalyptus -u admin -p PASSWORD
{{< / highlight >}}

The installer also sets up the AWS CLI for use with Eucalyptus:

{{< highlight shell >}}
>
> aws s3 ls
2020-03-07 00:46:33 eucalyptus-service-image-v5.0.100
>
> aws ec2 describe-availability-zones
AVAILABILITYZONES	cloud-1	available	cloud-1a
>
> aws ec2 describe-account-attributes
ACCOUNTATTRIBUTES	supported-platforms
ATTRIBUTEVALUES	VPC
ACCOUNTATTRIBUTES	default-vpc
ATTRIBUTEVALUES	vpc-6b1e517c04915806c
>
{{< / highlight >}}

You might want to review the [Eucalyptus 5 beta 1 announcement]({{< ref "2019-04-01-eucalyptus-5b1-release.md" >}})
for more details on the release.

## Feedback

Please report any issues you find with the [installer](https://github.com/Corymbia/eucalyptus-ansible/issues)
or [Eucalyptus 5](https://github.com/Corymbia/eucalyptus/issues) to help
improve the final release.
