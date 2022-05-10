---
title: "Announcing the AWS CLI plugin for Eucalyptus"
date: 2020-03-06
tags:
- announcement
- release
- tools
---

A new AWS CLI plugin with support for Eucalyptus Cloud deployments is now
available.

The initial release of the plugin simplifies using the AWS CLI with your
cloud deployment by removing the need to specify the endpoint with each
command or using other plugins with more complex configuration.

<!--more-->

## Getting started

To get started with the plugin, the first step is installation. 

You can either install using the [pypi package](https://pypi.org/project/awscli-plugin-eucalyptus/):

{{< highlight shell >}}
> pip install awscli-plugin-eucalyptus
{{< / highlight >}}

or if using a Eucalyptus 5 early access release then you can install the RPM package:

{{< highlight shell >}}
> yum install eucalyptus-awscli-plugin
{{< / highlight >}}

Either way, the plugin will be installed and ready to for the next step.

Configuration tells the AWS CLI to use the new plugin and also controls which
profiles it is active for. 

The simplest approach is to enable for the default profile:

{{< highlight shell >}}
> cat .aws/config 
[plugins]
eucalyptus = awscli_plugin_eucalyptus

[default]
ufshost = euca-10-10-10-10.euca.me
ufsport = 8773
verify_ssl = yes
output = text
region = eucalyptus
{{< / highlight >}}

The `ufshost` identifies the domain for the cloud and is used along with
other configuration settings to derive the service endpoints such as `https://ec2.euca-10-10-10-10.euca.me:8773/`.

Change `verify_ssl` to `no` if your Eucalyptus deployment does not have a valid HTTPS certificate.

## Using the CLI

Once configured you can use the AWS CLI as you would against AWS:

{{< highlight shell >}}
> aws ec2 describe-availability-zones
AVAILABILITYZONES	cloud-1	available	cloud-1a
{{< / highlight >}}

## Next steps

As covered in the earlier post on using the [AWS CLI with Eucalyptus ]({{< ref "2018-07-05-tools-awscli.md" >}})
you can set up command completion for the AWS CLI:

{{< highlight shell >}}
> complete -C aws_completer aws
{{< / highlight >}}

which makes it easier to discover commands and their options.

## Thanks!

Thanks for giving the AWS CLI plugin for Eucalyptus a try and please use [github issues](https://github.com/corymbia/eucalyptus-awscli-plugin/issues)
to report any problems you encounter to help improve the plugin.
