---
title: "Resolving Conflicts in Atlas Remote State"
---

## Resolving Conflicts in Atlas Remote State

The best way to resolve conflicts in Atlas remote state
is to merge and conflicted copies locally by inspecting the
raw state available in the path `.terraform/terraform.tfstate`.

When making state changes, it's important to make backup copies in
order to avoid losing any data.

Atlas will reject any state that is pushed with a serial that is lower
than the known serial when the MD5 of the state does not match.

The serial is embedded in the state file:

    {
        "version": 1,
        "serial": 555,
        "remote": {
            "type": "atlas",
            "config": {
                "name": "acmeinc/production"
            }
        },
        ...
    }

Once a conflict has been resolved locally by editing the state file,
the serial can be incremented past the current version in Atlas and
pushed:

    terraform remote push

This will upload the manually resolved state and set it as the head
version in Atlas.
