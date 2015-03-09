---
title: "Command-line Login"
---
## Command-line Login

To access and download private resources from Atlas, such as Vagrant boxes, you must authorize with Atlas. You can authoize by either logging in with your Atlas username and password, or by setting your Atlas token as an enviornment variable. You can generate a token for use by multiple users in your [organization's account page](/settings/tokens).

Username and password login:

	$ vagrant login
	# ...
	Atlas username:
	Atlas password:

Vagrant will use the ATLAS_TOKEN environment variable whenever authorization is needed. Export your Atlas token as an environment variable:

	$ export ATLAS_TOKEN=YOUR_TOKEN_HERE

You can read more about `vagrant login` and its options in the [Vagrant documentation](https://docs.vagrantup.com/v2/cli/login.html). 
