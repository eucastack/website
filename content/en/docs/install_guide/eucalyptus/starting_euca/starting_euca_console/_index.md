+++
title = "Start the Management Console"
weight = 70
+++

{{% alert title="Note" color="success" %}}
If you plan on running multiple Management Console host machines, we recommend turning off the default memcached in your console.ini file.
{{% /alert %}}

Log in to the Management Console host machine. If you want the console service to start at each boot-time, run this command: 

    systemctl enable eucaconsole.service

Enter the following command to start the console: 

    systemctl start eucaconsole.service

Repeat for each Management Console host machine. 
