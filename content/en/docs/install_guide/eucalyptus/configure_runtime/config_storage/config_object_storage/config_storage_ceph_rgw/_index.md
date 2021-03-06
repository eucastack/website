+++
title = "Use Ceph-RGW"
weight = 10
+++

This topic describes how to configure Ceph Rados Gateway (RGW) as the backend for the Object Storage Gateway (OSG).

## Prerequisites

* Successful completion of all the install sections prior to this section. 
* The UFS must be registered and enabled. 
* A Ceph storage cluster is available. 
* The ceph-radosgw service has been installed (on the UFS or any other host) and configured to use the Ceph storage cluster. recommends using civetweb with ceph-radosgw service. is a lightweight web server and is included in the ceph-radosgw installation. It is relatively easier to install and configure than the alternative option – a combination of Apache and Fastcgi modules.

For more information on Ceph-RGW, see the [Ceph-RGW documentation](http://docs.ceph.com/docs/master/radosgw/). 

## Configure Ceph-RGW object storage

You must execute the steps below as a administrator.

Configure **ceph-rgw** as the storage provider using the *euctl* command: 

```bash
euctl objectstorage.providerclient=ceph-rgw
```

Configure *objectstorage.s3provider.s3endpoint* to the **ip:port** of the host running the ceph-radosgw service: 

{{% alert title="Note" color="success" %}}
Depending on the front end web server used by ceph-radosgw service, the default port is 80 for apache and 7480 for civetweb. 
{{% /alert %}}

```bash
euctl objectstorage.s3provider.s3endpoint=<radosgw-host-ip>:<radosgw-webserver-port>
```

Configure *objectstorage.s3provider.s3accesskey* and *objectstorage.s3provider.s3secretkey* with the radosgw user credentials: 

```bash
euctl objectstorage.s3provider.s3accesskey=<radosgw-user-accesskey>
euctl objectstorage.s3provider.s3secretkey=<radosgw-user-secretkey>
```

The Ceph-RGW backend and OSG are now ready for production. 
