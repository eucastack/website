+++
title = "Access Object Storage"
weight = 10
+++

You can use your favorite S3 client (for example, ) to interact with Eucalyptus.To access object storage: 

Replace your S3_URL with the IP address of the OSG you wish to interact with and the service path with `/services/objectstorage` instead of `/services/Walrus` . For example: 

    S3_URL = http://<OSG IP>:8773/services/objectstorage


{{% alert title="Note" color="success" %}}
If you have DNS enabled, you may use the "objectstorage" prefix to access your object storage. Eucalyptus will return a list of IPs that correspond to OSGs that are in the state. 
{{% /alert %}}
