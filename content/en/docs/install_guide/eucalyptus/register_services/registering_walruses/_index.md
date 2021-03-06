+++
title = "Register the Walrus Backend"
weight = 20
+++

This topic describes how to register the Walrus Backend service with the Cloud Controller (CLC).

**Prerequisites** 

* You must be using the Walrus Backend service as your object storage provider. 
* The Cloud Controller must be properly installed and started. 

**To register the Walrus Backend service with the Eucalyptus cloud** 

{{% alert title="Note" color="success" %}}
This task is not necessary if you are using Riak CS instead of Walrus. 
{{% /alert %}}

On the CLC host machine, run the following command: 

    euserv-register-service -t walrusbackend -h IP SVCINSTANCE

where: 

* `SVCINSTANCE` is the IP of the Walrus Backend you are registering with this CLC. 
* must be a unique name for the Walrus Backend service. We recommend that you use a short-hand name of the hostname or IP address of the machine.

For example: 

    euserv-register-service -t walrusbackend -h 10.111.5.182 walrus-10.111.5.182

Copy the security credentials from the CLC to each machine running a Walrus Backend service. Run this command on the CLC host machine: 

    clcadmin-copy-keys HOST [HOST ...]

For example: 

    clcadmin-copy-keys 10.111.5.182

Verify that the Walrus Backend service is registered with the following command: 

    euserv-describe-services SVCINSTANCE

The registered Walrus Backend service is now ready for your cloud. 

