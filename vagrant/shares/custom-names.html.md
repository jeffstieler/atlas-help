---
title: "Custom Share Names"
---

# Custom Share Names

Custom share names allow you to specify custom names in the URL
to your Vagrant Share, like `hello-atlas.vagrantshare.com`. You can view
names and recycle previously used names on the
[Vagrant](/vagrant) page of Atlas.

If security is a concern, we recommend using complex or uncommon words for
custom share names. You can read more about security of shares in
the [Vagrant Share security](http://docs.vagrantup.com/v2/share/security.html)
documentation.

## How to Use a Custom Name

1. Run Vagrant share with the `--name` flag, specifiying the name you
want to use
2. The share should be created with that name as the leading subdomain
3. Share names are recycled when they expire automatically, meaning they
can be used again (by any user, if not on a custom domain)
4. If a share doesn't expire correctly, you can visit the [shares page](/shares)
and manually recycle the name by clicking the "Recycle name" link

### Uniqueness

When using the `vagrantshare.com` domain, the name chosen must be globally
unique. This is to ensure Atlas only routes to one share for one machine at
 a time.

### Custom Names with Custom Domains

You can use custom names with custom domains. Uniqueness will be verified
within the scope of the domain. The process is otherwise the same.
