+++
title = "Create a Security Group"
weight = 30
+++

Security groups let you control network access to instances by applying network rules to instances associated with a group. 

To create a security group: 

Enter the following command: 

    euca-add-group -d <description> <group_name>

{{% alert title="Note" color="success" %}}
You can also create a security group you run an instance. Use the command with the option. Security group rules only apply to incoming traffic thus all outbound traffic is permitted. 
{{% /alert %}}

The following example creates a new security group named `mygroup` and described as `newgroup` . 

    euca-add-group -d "newgroup" mygroup

