---
title: "Using the AWS CLI with Eucalyptus"
date: 2018-07-05
tags:
- tools
- compatibility
---

The [AWS Command Line Interface](https://aws.amazon.com/cli/) is a unified tool to manage AWS
services. You would use the CLI to run EC2 instances, upload objects for storage in S3, and to
manage users in IAM.

In this post we examine how the CLI, and higher level tooling, can be used with your
Eucalyptus cloud.

<!--more-->


## Get started with the CLI
The first step is to get the latest AWS CLI. These instructions will differ depending on your OS,
we will assume that CentOS/RHEL 7 is in use as that is the OS used with Eucalyptus. You may need
to alter for your package manager, or to use `pip3` rather than `pip`.

The AWS CLI can be installed using pip, if you do not have pip available you can install it using 
yum (or apt-get, dnf, etc):

{{< highlight shell >}}
> yum install python-pip
>
> pip install awscli
{{< / highlight >}}

We then need to configure a few options to allow use of the CLI with Eucalyptus clouds:

{{< highlight shell >}}
> aws configure set s3.signature_version s3v4
> aws configure set region eucalyptus
> aws configure set output text
{{< / highlight >}}

We've used the region name `eucalyptus`, but you can use any region name for your Eucalyptus cloud.
We set the output of the CLI to text rather than the JSON default so it is easier to read.

The CLI comes with support for TAB completion of commands let's enable it for our current shell:

{{< highlight shell >}}
> complete -C aws_completer aws
{{< / highlight >}}

With this configuration we can run commands by specifying the `--endpoint` option and using
credentials from the environment. This is not very convenient, but fortunately we can do better by
making use of the endpoint plugin.


## Enter the Endpoint plugin
The [AWS CLI Endpoint plugin](https://github.com/wbingli/awscli-plugin-endpoint) can also be
installed using pip and allows us to configure the service endpoints we want to use for our
Eucalyptus cloud.

{{< highlight shell >}}
> pip install awscli-plugin-endpoint
>
> aws configure set plugins.endpoint awscli_plugin_endpoint
{{< / highlight >}}

This installs and enables the plugin.

Next we configure the endpoints, making use of a euca2ools command to generate environment
variables based on euca2ools existing configuration:

{{< highlight shell >}}
> eval $(euca-generate-environment-config)
>
> aws configure set autoscaling.endpoint_url ${AWS_AUTO_SCALING_URL}
> aws configure set cloudformation.endpoint_url ${AWS_CLOUDFORMATION_URL}
> aws configure set cloudwatch.endpoint_url ${AWS_CLOUDWATCH_URL}
> aws configure set ec2.endpoint_url ${EC2_URL}
> aws configure set elb.endpoint_url ${AWS_ELB_URL}
> aws configure set iam.endpoint_url ${AWS_IAM_URL}
> aws configure set s3.endpoint_url ${S3_URL}
> aws configure set s3api.endpoint_url ${S3_URL}
> aws configure set sts.endpoint_url ${TOKEN_URL}
{{< / highlight >}}

Here we have configured the default endpoints used by the various AWS CLI subcommands. A subcommand
is a little different from a service, notably we configure the Eucalyptus S3 endpoint for the `s3`
and `s3api` subcommands as these both use S3 compatible services.


## AWS CLI in action
Now that the CLI is fully configured let's try out a few of the services:

{{< highlight shell >}}
> aws ec2 describe-account-attributes
ACCOUNTATTRIBUTES	supported-platforms
ATTRIBUTEVALUES	EC2
ACCOUNTATTRIBUTES	default-vpc
ATTRIBUTEVALUES	none
>
> aws iam list-users
USERS	arn:aws:iam::000855590299:user/narwhal	2018-07-08T01:37:46.321Z	/	AIDAAMZJOPZULQOJTH5F5	narwhal
USERS	arn:aws:iam::000855590299:user/walrus	2018-07-08T01:37:22.949Z	/	AIDAAWRRN2HWUF3DKLQFP	walrus
USERS	arn:aws:iam::000855590299:user/admin	2018-07-08T01:36:29.632Z	/	AIDAAX6G7F7VLGONP3LJK	admin
>
> aws s3 ls
2018-07-07 18:39:04 narwhal
2018-07-07 18:39:15 walrus
>
> aws sts get-caller-identity
000855590299	arn:aws:iam::000855590299:user/admin	AIDAAX6G7F7VLGONP3LJK
>
{{< / highlight >}}

This shows examples of using the `ec2`, `s3`, and `iam` services without having to specify the
endpoint for each command.


## Using the shell
Now that we have the basics working we can try out the [AWS CLI shell](https://github.com/awslabs/aws-shell)

{{< highlight shell >}}
> pip install aws-shell
{{< / highlight >}}

The shell uses the AWS CLI and provides additional functionality such as command completion and
inline documentation.

<img alt="SVG animation, see more examples on the aws-shell site" width="100%" src="tools-awscli-shell.svg">

As shown here, the shell provides a more interactive experience.


## All the clouds
The basic configuration we have so far is a good start, but if you use multiple Eucalyptus clouds,
or if use both AWS and Eucalyptus you may need more control over your credentials and endpoints.

AWS CLI profiles offer a solution. When exporting the euca2ools configuration you can
use the `--region` option for `euca-generate-environment-config` to select the credentials and
endpoints for export. You then use the `--profile` option with the CLI:

{{< highlight shell >}}
> aws --profile euca-profile-1 configure
> 
> eval $(euca-generate-environment-config --region euca-region-1)
>
> aws configure --profile euca-profile-1 set s3.endpoint_url ${S3_URL}
> aws configure --profile euca-profile-1 set s3api.endpoint_url ${S3_URL}
{{< / highlight >}}

The initial configure command will interactively configure the region and credentials to use for
the profile. The endpoint configuration will then set up the endpoints for the profile, above we
only show configuration for the S3 endpoint.

If you have any issues with this configuration you may need to remove the `[plugins]` section from
the `~/.aws/config` file. If you do so, be sure to add it back in once the endpoints are configured.

With this configuration you can now specify the profile to use for each command or you can switch
between CLI profiles by setting an environment variable:

{{< highlight shell >}}
> aws --profile euca-profile-1 s3 ls
>
> export AWS_PROFILE=euca-profile-1
> aws s3 ls
{{< / highlight >}}

Using this approach to configuration you can more easily use the AWS CLI with both AWS and multiple
Eucalyptus clouds.
