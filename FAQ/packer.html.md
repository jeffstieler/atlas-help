---
title: "Packer, Artifacts, and Services"
---
## Where do my files go after Packer push?
As described in the [Packer push documentation](https://www.packer.io/docs/templates/push.html), the default settings for `packer push` will send to Atlas all files in the directory your Packer template is in. 

It is _very_ important to note that the files sent from `packer push` are  only available in the environment and local filesystem that Packer runs within Atlas, and will _not_ be on your artifact unless explicitly moved _from_ Atlas and _to the host_ which will be snapshotted to create a machine image.

![Atlas Packer Remote relationship](/help-images/atlas-packer-remote.png)

There are three environments that your files interact with: 1. The machine that runs `packer push` (usually your local development machine) 2. Atlas, which holds the files sent from `packer push` and 3. The remote host which will be snapshotted to create a machine image. Finally the last environment is the the new host which is created from the machine image. When a new host is provisioned from the machine image, it will have all the files that were on the original host.

Sometimes the remote host needs a file, such as a service configuration, moved over from Atlas. Here's an example code snippet which moves a file from Atlas to the host:

    "provisioners": [
        {
            "type": "file",
            "source": "files/authorized_keys",
            "destination": "~/.ssh/authorized_keys"
        }
    ]

This snippet tells Atlas to move the file with path "files/authorized_keys" from Atlas (source) and to the "~/.ssh/authorized_keys" path (destination) on the host to be snapshotted. Be very careful which files you move onto the host, as you could expose security vulnerabilities. 

If you are trying to move a file in a script, for example with the line `mv /ops/upstart/consul_bootstrap.conf /etc/init/consul.conf`, remember that the bash command is being run on the host, so the origin file must exist on the host.

Also note that if "vcs" is not set to false in your Packer push configuration, you must add any new files to source control in order for Packer to push them to Atlas.
