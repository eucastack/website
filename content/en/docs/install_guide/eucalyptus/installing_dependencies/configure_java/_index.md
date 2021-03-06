+++
title = "Configure Java"
weight = 40
+++

For the supported version of the Java Virtual Machine (JVM), see the Compatibility Matrix in the Release Notes . 

As of Eucalyptus 4.3, JVM 8 is required. Eucalyptus RPM packages require java-1.8.0-openjdk, which will be installed automatically. 


{{% alert title="Note" color="success" %}}
If your network mode is VPCMIDO, MidoNet will install JVM 1.7 as a dependency (it is acceptable to have both JVM 1.7 and JVM 1.8 installed). 
{{% /alert %}}


**To use Java with Eucalyptus cloud:** 

Open the */etc/eucalyptus/eucalyptus.conf* file. Verify that the CLOUD_OPTS setting does not set --java-home , or that --java-home points to a supported JVM version. 
{{% alert title="Note" color="success" %}}
Although it is possible to set , we do not recommend it unless there is a specific reason to do so. 
{{% /alert %}}
If you are upgrading to Eucalyptus 4.3, note that Java 8 does not have permanent generation memory. Remove any JAVA_OPTS MaxPermSize settings at upgrade time. Save and close the file. Repeat on each host machine that will run a Eucalyptus service. 
