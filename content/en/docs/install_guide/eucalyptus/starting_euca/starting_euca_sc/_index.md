+++
title = "Start the SC"
weight = 50
+++

**Prerequisites** 

You should have installed and configured Eucalyptus before starting the SC. 

{{% alert title="Note" color="success" %}}
If you are re-installing the SC, restart the tgt (iSCSI open source target) daemon. 
{{% /alert %}}

{{% alert title="Note" color="success" %}}
If you installed SC on the same host as the CLC, you can skip this. 
{{% /alert %}}

**To start the SC** 

Log in to the Storage Controller (SC) host machine. If you want the SC service to start at each boot-time, run this command: 

    systemctl enable eucalyptus-cloud.service

If you want the tgtd service to start at each boot-time, run this command: 

    systemctl enable tgtd.service

{{% alert title="Note" color="success" %}}
depends on tgtd to create and manage block storage volumes when the storage provider is either DAS or Overlay. 
{{% /alert %}}

Enter the following commands to start the SC: 

    systemctl start tgtd.service
    
    systemctl start eucalyptus-cloud.service

If you have a multi-zone setup, repeat this step on the SC in each zone. 
