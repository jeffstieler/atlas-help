---
title: "Authentication with Atlas"
---

# Authentication with Atlas

Atlas requires a username and password to sign up and login. However,
there are several ways to authenticate with your Atlas account.

### Authentication Tokens

Authentication tokens are keys used to access your account via tools
or over the various APIs used in Atlas.

You can create new tokens in the [token section](/settings/tokens)
of your account settings. It's important to keep tokens secure,
as they are essentially a password and can be used to access your
account or resources. Additionally, token authentication
bypasses two factor authentication.

### Authenticating Tools

All HashiCorp tools look for the `ATLAS_TOKEN` environment variable:

    $ export ATLAS_TOKEN=TOKEN

This will automatically authenticate all requests with Atlas against
this token. This is the recommended way to authenticate with our various
tools. Care should be given to how this token is stored, as it is
as good as a password.

### Two Factor Authentication

You can optionally enable Two Factor authentication, requiring an
SMS or TOTP one-time code every time you log in, after entering
your username and password.

You can enable Two Factor authentication in the [security section](/settings/security)
of your account settings.

Be sure to save the generated recovery codes to


### Vagrant Login

Only Vagrant allows for a `vagrant login` command, but it can be
used to login and automatically create an authentication token from Vagrant.

	$ vagrant login
	# ...
	Atlas username:
	Atlas password:

You can read more about `vagrant login` and its options
in the [Vagrant documentation](https://docs.vagrantup.com/v2/cli/login.html). You
cannot use Vagrant login with Two Factor authentication.
