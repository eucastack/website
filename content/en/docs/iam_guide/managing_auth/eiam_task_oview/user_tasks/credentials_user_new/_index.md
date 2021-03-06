+++
title = "Generating User Credentials"
weight = 40
+++

The first time you get credentials using the *clcadmin-assume-system-credentials* command, a new secret access key is generated. On each subsequent request to get credentials, an existing active secret key is returned. You can also generate new keys using the *euare-useraddkey* command. 

{{% alert title="Note" color="success" %}}
Each request to get a user's credentials generates a new pair of a private key and X.509 certificate.. 
{{% /alert %}}

To generate a new key for a user by an account administrator, enter the following 

    euare-useraddkey USER_NAME

To generate a private key and an X.509 certificate pair, enter the following: 

    euare-usercreatecert USER_NAME

The cloud administrator can obtain temporary access credentials for any cloud user via the *clcadmin-impersonate-user* command.
