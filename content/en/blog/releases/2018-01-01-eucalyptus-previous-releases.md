---
title: "Eucalyptus Previous Releases"
date: 2018-01-01
tags:
- release
---

We know how much you love Eucalyptus 4.4, but we also recognize that
sometimes a cloud is working well on an older version and upgrading can
wait.

In this post we take a look at how you can use the new
`downloads.eucalyptus.cloud` RPM repositories with older releases, and
where you can find the related documentation.

<!--more-->

## Documentation for previous releases
The [current documentation](https://docs.eucalyptus.cloud/) has release
notes that cover previous versions. Other documentation is available for
previous releases as follows:

|         |   |   |   |   |   |
|---------|---|---|---|---|---|
| Eucalyptus 4.0 | [Admin Guide](https://docs.eucalyptus.cloud/eucalyptus/4.0.2/admin-guide-4.0.2.pdf)  | [Console Guide](https://docs.eucalyptus.cloud/eucalyptus/4.0.2/console-guide-4.0.2.pdf) | [Image Guide](https://docs.eucalyptus.cloud/eucalyptus/4.0.2/image-guide-4.0.2.pdf) | [Install Guide](https://docs.eucalyptus.cloud/eucalyptus/4.0.2/install-guide-4.0.2.pdf) | [User Guide](https://docs.eucalyptus.cloud/eucalyptus/4.0.2/user-guide-4.0.2.pdf) |
| Eucalyptus 4.1 | [Admin Guide](https://docs.eucalyptus.cloud/eucalyptus/4.1.2/admin-guide-4.1.2.pdf) | [Console Guide](https://docs.eucalyptus.cloud/eucalyptus/4.1.2/console-guide-4.1.2.pdf) | [Image Guide](https://docs.eucalyptus.cloud/eucalyptus/4.1.2/image-guide-4.1.2.pdf) | [Install Guide](https://docs.eucalyptus.cloud/eucalyptus/4.1.2/install-guide-4.1.2.pdf) | [User Guide](https://docs.eucalyptus.cloud/eucalyptus/4.1.2/user-guide-4.1.2.pdf) |
| Eucalyptus 4.2 | [Admin Guide](https://docs.eucalyptus.cloud/eucalyptus/4.2.2/admin-guide-4.2.2.pdf) | [Console Guide](https://docs.eucalyptus.cloud/eucalyptus/4.2.2/console-guide-4.2.2.pdf) | [Image Guide](https://docs.eucalyptus.cloud/eucalyptus/4.2.2/image-guide-4.2.2.pdf) | [Install Guide](https://docs.eucalyptus.cloud/eucalyptus/4.2.2/install-guide-4.2.2.pdf) | [User Guide](https://docs.eucalyptus.cloud/eucalyptus/4.2.2/user-guide-4.2.2.pdf) |
| Eucalyptus 4.3 | [Admin Guide](https://docs.eucalyptus.cloud/eucalyptus/4.3.1/admin-guide-4.3.1.pdf) | [Console Guide](https://docs.eucalyptus.cloud/eucalyptus/4.3.1/console-guide-4.3.1.pdf) | [Image Guide](https://docs.eucalyptus.cloud/eucalyptus/4.3.1/image-guide-4.3.1.pdf) | [Install Guide](https://docs.eucalyptus.cloud/eucalyptus/4.3.1/install-guide-4.3.1.pdf) | [User Guide](https://docs.eucalyptus.cloud/eucalyptus/4.3.1/user-guide-4.3.1.pdf) |

The above guides are available in PDF format only.

## Repositories for previous releases
If using a release earlier than 4.4, please keep in mind that these
previous releases are no longer supported or maintained. RPMs are
available for previous releases at these locations:

Eucalyptus 4.0:
{{< highlight shell >}}
http://downloads.eucalyptus.cloud/software/eucalyptus/4.0/rhel/6/x86_64/
{{< / highlight >}}

Eucalyptus 4.1:
{{< highlight shell >}}
http://downloads.eucalyptus.cloud/software/eucalyptus/4.1/rhel/6/x86_64/
{{< / highlight >}}

Eucalyptus 4.2:
{{< highlight shell >}}
http://downloads.eucalyptus.cloud/software/eucalyptus/4.2/rhel/6/x86_64/
{{< / highlight >}}

Eucalyptus 4.3:
{{< highlight shell >}}
http://downloads.eucalyptus.cloud/software/eucalyptus/4.3/rhel/6/x86_64/
http://downloads.eucalyptus.cloud/software/eucalyptus/4.3/rhel/7/x86_64/
{{< / highlight >}}

The 4.3 release can be installed on CentOS/RHEL 6 or 7, so pick the
location appropriate for the distribution you are using.

### Repository Configuration
You would configure YUM to use the above locations. Here's an example of
a 4.1 Eucalyptus YUM configuration, you'd put this in a
`/etc/yum.repos.d/eucalyptus.repo` file:
{{< highlight shell >}}
[eucalyptus]
name=Eucalyptus 4.1
baseurl=http://downloads.eucalyptus.cloud/software/eucalyptus/4.1/rhel/6/x86_64/
gpgkey=https://downloads.eucalyptus.cloud/software/gpg/eucalyptus-release-key.pub
gpgcheck=1
enabled=1
{{< / highlight >}}

The `baseurl` would be one of the locations listed above.

On the first use after configuration, you may be prompted to confirm the
GPG key, which would look something like this:

{{< highlight shell >}}
warning: rpmts_HdrFromFdno: Header V3 RSA/SHA1 Signature, key ID c1240596: NOKEY
Retrieving key from https://downloads.eucalyptus.cloud/software/gpg/eucalyptus-release-key.pub
Importing GPG key 0xC1240596:
 Userid: "Eucalyptus Systems, Inc. (release key) <security@eucalyptus.com>"
 From  : https://downloads.eucalyptus.cloud/software/gpg/eucalyptus-release-key.pub
Is this ok [y/N]: y
{{< / highlight >}}

Accept the key and you're good to go!

## Conclusion
We hope this helps keep your Eucalyptus clouds running, but please
consider using the latest software and documentation from
https://eucalyptus.cloud/
