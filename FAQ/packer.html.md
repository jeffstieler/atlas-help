---
title: "Packer, Artifacts, and Services"
---
## Where do my files go after Packer push?
As described in the [Packer push documentation](https://www.packer.io/docs/templates/push.html), the default settings for `packer push` will send to Atlas all files in the directory your Packer template is in. 

It is _very_ important to note that the files sent from `packer push` are  only available in the environment and local filesystem that Packer runs within Atlas, and will _not_ be on your artifact unless explicitly moved _from_ Atlas and _to the host_ which will be snapshotted to create a machine image. When a new host is provisioned from the machine image, it will have all the files that were on the original host. 

There are four environments that your files interact with: 1. The machine that runs `packer push` (usually your local development machine) 2. Atlas which holds the files sent from `packer push` 3. The host which will be snapshotted to create a machine image and 4. The new host which is created from the machine image. 

An example code snippet which moves files from Atlas to the host is below:

	"provisioners": [
		{   
		    "type": "file",
		    "source": ".",
		    "destination": "/ops"
		}
	]

This snippet tells Atlas to move files from the currect directory on Atlas (source) and to the "/ops" directory (destination) on the host to be snapshotted. Be very careful which files you move onto the host, as you could expose security vulnerabilities.

Also note that if "vcs" is set to true in your Packer push configuration, you must add any new files to source control in order for Packer to push them to Atlas.
