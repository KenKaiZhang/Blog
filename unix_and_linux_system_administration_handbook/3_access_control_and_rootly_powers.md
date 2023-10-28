# Access Control and Rootly Powers

Rules to follow by:

1. Access control decisions depend on which user is attempting to perform an operation
2. Objects have owners and owners have broad control over them
3. You own the objects you make
4. **Root** user is the owner of any project
5. Only root users can perform certain sensitive operations

Every file has a owner and or a group(defined in `/etc/group`)

- only owners can change what groups are allowed
- authorized users identified through UIDs defined in `/etc/passwd` and `/etc/groups`

The UID and GID of users and groups can only be changed by the root

Root operations are not recorded

**`su`** commands allows user root privilages until exit

- or another user if provided

**`sudo`** executes the command as a root without having to become the root

- logs will be kept in a log of your choice

_Example configuration_

```
Host_Alias  CS = tigger, anchor, piper, moet, sigi
Host_Alias  PHYSICS = eprince, pprince, icarus

Cmnd_Alias  DUMP = /sbin/dump, /sbin/restore
Cmnd_Alias  WATCHDOG = /usr/local/bin/watchdog
Cmnd_Alias  SHELLS = /bin/sh, /bin/dash, /bin/bash

# Permissions
mark, ed    PHYSICS = ALL
herb        CS = /usr/sbin/tcpdump  :   PHYSICS = (operator) DUMP
lynda       ALL = (ALL) ALL, !SHELLS
%wheel      ALL, !PHYSICS = NOPASSWD: WATCHDOG
```

1. mark and ed on the machines in the `PHYSICS` group are allowed to run any commands
2. herb is allowed to run `tcpdump` on `CS` machies and dump-related commands on `PHYSICS` machines but only as a operator (not root)
3. lynda can run commands as anyuser on any machines but not allowed to run several common commands
4. Anyone in the wheel group is allowed to run `watchdog` as root on all CS machines

In the `Permissions`, each line includes

- the users that the line applies to
- the hosts on which the line should be heeded
- the commands that the specified users can run
- the users as whom the commands can be executed on

You can have one master sudoer file for the whole system (recommended)

**`passwd -l`** will lock an account by adding a `!` in front of the encrypted password stored in `/etc/shadow`
