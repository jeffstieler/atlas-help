---
title: "How to Create a Share"
---

# How to Create a Share

<div class="alert-infos">
  <div class="row alert-info">
    Heads up! You'll need <a href="/help/intro/updating-tools">the latest version of Vagrant</a> installed
    to use this feature.
  </div>
</div>

## HTTP

Share the active HTTP server in your environment.

1. Run `vagrant login` and enter your Atlas by HashiCorp details
2. Boot a Vagrant environment and verify it's running an HTTP server
3. Run `vagrant share`. You're done!

## SSH

Share SSH access to your environment.

1. Run `vagrant login` and enter your Atlas by HashiCorp details
2. Boot a Vagrant environment
3. Run `vagrant share --ssh`
4. Enter a password for encrypting the SSH key
5. Give your Share name and the password to a friend and have them
run `vagrant connect --ssh [SHARE NAME]`

## Connect

Share any port in your environment.

1. Run `vagrant login` and enter your Atlas by HashiCorp details
2. Boot a Vagrant environment
3. Run `vagrant share --disable-http`
4. Give your Share name to a friend and have them run `vagrant connect [SHARE NAME]`
