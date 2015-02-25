---
title: "Packer, Artifacts, and Services"
---
## Where do my files go after Packer push?
As described in the [Packer push documentation](https://www.packer.io/docs/templates/push.html), the default settings for `packer push` will send to Atlas all files in the directory your Packer template is in. 

It is _very_ important to note that the files sent from `packer push` are just in Atlas, and will _not_ be on your artifact unless explicitly moved _from_ Atlas and _to the instance_ which will be snapshotted to create a machine image. 

There are three entities that send and share files: 1. The machine that runs `packer push` (usually your local development machine) 2. Atlas which holds the files sent from `packer push` and 3. The instance which will be snapshotted to create a machine image. 

An example code snippet which moves files from Atlas to the instance is below:

	"provisioners": [
		{   
		    "type": "file",
		    "source": ".",
		    "destination": "/ops"
		}
	]

This snippet tells Atlas to move files from the currect directory on Atlas (source) and to the "/ops" directory (destination) on the instance to be snapshotted.

Also note that if "vcs" is set to true in your Packer push configuration, you must add any new files to source control in order for Packer to push them to Atlas.
