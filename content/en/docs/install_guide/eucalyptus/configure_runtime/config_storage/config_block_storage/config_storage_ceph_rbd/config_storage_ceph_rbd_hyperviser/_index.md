+++
title = "Configure Hypervisor Support for Ceph-RBD"
weight = 10
+++

This topic describes how to configure the hypervisor for Ceph-RBD support.The following instructions will walk you through steps for verifying and or installing the required hypervisor for Ceph-RBD support. **Repeat this process for every NC in the Eucalyptus zone** 

Verify if `qemu-kvm` and `qemu-img` are already installed. 

    rpm -q qemu-kvm qemu-img

Proceed to the preparing the RHEV qemu packages step if they are not installed. 

Verify qemu support for the `ceph-rbd` driver. 

    qemu-img --help
    qemu-img version 0.12.1, Copyright (c) 2004-2008 Fabrice Bellard
    ...
    Supported formats: raw cow qcow vdi vmdk cloop dmg bochs vpc vvfat qcow2 qed vhdx parallels nbd blkdebug host_cdrom 
    host_floppy host_device file gluster gluster gluster gluster rbd


{{% alert title="Note" color="success" %}}
If 'rbd' is listed as one of the supported formats, no further action is required; otherwise proceed to the next step. 
{{% /alert %}}
If the `eucalyptus-node` service is running, terminate/stop all instances. After all instances are terminated, stop the eucalyptus-node service. 

    systemctl stop eucalyptus-node.service

Prepare the RHEV qemu packages: 

* If this NC is a RHEL system and the RHEV subscription to qemu packages is available, consult the RHEV package procedure to install the qemu-kvm-ev and qemu-img-ev packages. Blacklist the RHEV packages in the repository to ensure that packages from the RHEV repository are installed. 
* If this NC is a RHEL system and RHEV subscription to qemu packages is unavailable, built and maintained qemu-rhev packages may be used. These packages are available in the same yum repository as other packages. Note that using built RHEV packages voids the original RHEL support for the qemu packages. 
* If this NC is a non-RHEL (CentOS) system, -built and maintained qemu-rhev packages may be used. These packages are available in the same yum repository as other packages. 
If you are *not* using the RHEV package procedure to install the `qemu-kvm-ev` and `qemu-img-ev` packages, install Eucalyptus -built RHEV packages: `qemu-kvm-ev` and `qemu-img-ev` , which can be found in the same yum repository as other Eucalyptus packages. 

    yum install qemu-kvm-ev qemu-img-ev

Start the `libvirtd` service. 

    systemctl start libvirtd.service

Verify `qemu` support for the `ceph-rbd` driver. 

    qemu-img --help
    qemu-img version 0.12.1, Copyright (c) 2004-2008 Fabrice Bellard
    ...
    Supported formats: raw cow qcow vdi vmdk cloop dmg bochs vpc vvfat qcow2 qed vhdx parallels nbd blkdebug host_cdrom 
    host_floppy host_device file gluster gluster gluster gluster rbd

Make sure the eucalyptus-node service is started. 

    systemctl start eucalyptus-node.service

Your hypervisor is ready for Eucalyptus Ceph-RBD support. You are now ready to [configure Ceph-RBD]({{< ref config_storage_ceph_rbd.md >}}) for Eucalyptus . 