+++
title = "Use Ceph-RBD"
weight = 5
chapter = true
+++


# Use Ceph-RBD
This topic describes how to configure Ceph-RBD as the block storage backend provider for the Storage Controller (SC).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* You must execute the steps below as a administrator. 
* You must have a functioning Ceph cluster. 
* Ceph user credentials with the following privileges are available to SCs and NCs (different user credentials can be used for the SCs and NCs). 
* Hypervisor support for Ceph-RBD on NCs. Node Controllers (NCs) are designed to communicate with the Ceph cluster via libvirt. This interaction requires a hypervisor that supports Ceph-RBD. See to satisfy this prerequisite. 
**To configure Ceph-RBD block storage for the zone, run the following commands on the CLC** Configure the SC to use Ceph-RBD for EBS. 

    euctl ZONE.storage.blockstoragemanager=ceph-rbd

The output of the command should be similar to: 

    one.storage.blockstoragemanager=ceph-rbd

Verify that the property value is now `ceph-rbd` : 

    euctl ZONE.storage.blockstoragemanager

Check the SC to be sure that it has transitioned out of the `BROKEN` state and is in the `NOTREADY` , `DISABLED` or `ENABLED` state before configuring the rest of the properties for the SC. The ceph-rbd provider will assume defaults for the following properties for the SC: 

    euctl ZONE.storage.ceph
     
    PROPERTY        one.storage.cephconfigfile  /etc/ceph/ceph.conf
    DESCRIPTION     one.storage.cephconfigfile  Absolute path to Ceph configuration (ceph.conf) file. Default value is '/etc/ceph/ceph.conf'
     
    PROPERTY        one.storage.cephkeyringfile /etc/ceph/ceph.client.eucalyptus.keyring
    DESCRIPTION     one.storage.cephkeyringfile Absolute path to Ceph keyring (ceph.client.eucalyptus.keyring) file. Default value is '/etc/ceph/ceph.client.eucalyptus.keyring'
     
    PROPERTY        one.storage.cephsnapshotpools       rbd
    DESCRIPTION     one.storage.cephsnapshotpools       Ceph storage pool(s) made available to  for EBS snapshots. Use a comma separated list for configuring multiple pools. Default value is 'rbd'
     
    PROPERTY        one.storage.cephuser        eucalyptus
    DESCRIPTION     one.storage.cephuser        Ceph username employed by  operations. Default value is 'eucalyptus'
     
    PROPERTY        one.storage.cephvolumepools rbd
    DESCRIPTION     one.storage.cephvolumepools Ceph storage pool(s) made available to  for EBS volumes. Use a comma separated list for configuring multiple pools. Default value is 'rbd'

The following steps are optional if the default values do not work for your cloud: To set the Ceph username (the default value for Eucalyptus is 'eucalyptus'): 

    euctl ZONE.storage.cephuser=myuser

To set the absolute path to keyring file containing the key for the 'eucalyptus' user (the default value is '/etc/ceph/ceph.client.eucalyptus.keyring'): 

    euctl ZONE.storage.cephkeyringfile='/etc/ceph/ceph.client.myuser.keyring'


{{% alert title="Note" color="success" %}}
If cephuser was modified, ensure that cephkeyringfile is also updated with the location to the keyring for the specific cephuser: 
{{% /alert %}}
To set the absolute path to ceph.conf file (default value is '/etc/ceph/ceph.conf'): 

    euctl ZONE.storage.cephconfigfile=/path/to/ceph.conf

To change the comma-delimited list of Ceph pools assigned to Eucalyptus for managing EBS volumes (default value is 'rbd') : 

    euctl ZONE.storage.cephvolumepools=rbd,myvolumes

To change the comma-delimited list of Ceph pools assigned to Eucalyptus for managing EBS snapshots (default value is 'rbd') : 

    euctl ZONE.storage.cephsnapshotpools=mysnapshots

If you want to enable snapshot deltas for your Ceph backend: 
{{% alert title="Note" color="success" %}}
Snapshot deltas are supported only on Ceph-RBD. 
{{% /alert %}}

{{% alert title="Note" color="success" %}}

{{% /alert %}}
Verify that snapshots are enabled: 

    euctl ZONE.storage.shouldtransfersnapshots=true

Set the maximum number of deltas to be created before creating a new full snapshot: 

    euctl ZONE.storage.maxsnapshotdeltas=NON_ZERO_INTEGER


{{% alert title="Note" color="success" %}}
This variable applies to all Ceph volumes. 
{{% /alert %}}

{{% alert title="Note" color="success" %}}
If you need to create a non-Ceph volume from a Ceph snapshot, this value would need to be set to zero (at least temporarily). 
{{% /alert %}}
Every NC will assume the following defaults: 

    CEPH_USER_NAME="eucalyptus"
    CEPH_KEYRING_PATH="/etc/ceph/ceph.client.eucalyptus.keyring"
    CEPH_CONFIG_PATH="/etc/ceph/ceph.conf"

To override the above defaults, add/edit the following properties in the `/etc/eucalyptus/eucalyptus.conf` on the specific NC file: 

    CEPH_USER_NAME="ceph-username-for-use-by-this-NC"
    CEPH_KEYRING_PATH="path-to-keyring-file-for-ceph-username"
    CEPH_CONFIG_PATH="path-to-ceph.conf-file"

Repeat this step for every NC in the specific Eucalyptus zone. Your Ceph backend is now ready to use with Eucalyptus . 


