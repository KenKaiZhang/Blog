# 10 Logging

A line of text with a few properties attached including a time stamp, tyep and severity, and a process name and ID

**Log management** involves a few major subtasks:

- collecting logs from a variety of sources
- providing a structured interface for querying, analyzing, filtering, and monitoring messages
- manageing the retention and expiration of messages

Log files are stored in **/var/log** by default and owned by the root

Log files not to manage:

- **wtmp**: contains a record of users' logins and logouts as well as system reboot or shut down
- **lastlog**: only the time of the last login for each user

**`journalctl`** allows users to view logs

- adding a `-f` flag allows new messages to be printing as they arrive

## Systemd Journal

**systemd** includes a logging daemon called **systemd-journald** which stores messages in binary format making it faster to search

Journal collects and indexes messages from several sources:

- **/dev/log** socket ot obtain messages from software that submits messages according to syslog conventions
- **/dev/kmsg** to collect messages from the kernel
- **/run/systemd/journal/stdout**, to service software that writes log messages to standard output
- **/run/systemd/journal/stdout**, to service software that wubmits messages through the **systemd** journal API
- Audit messages from the kernel's **auditd** daemon

The default journal configuration file is in **/etc/systemd/journal.conf** but should be customized in **/etc/systemd/journal.conf.d** directory with a **.conf** extension

`Storage` option controls whether to save journal to disk with options:

- `volatile`: stores the journal in memory only
- `persistent`: saves in **/var/log/journal**
- `auto`: saves in **/var/log/jorunal** but does not create the directory (default)
- `none`: don't save

`Seal` option will prevent journal modification without credentials

## Syslog

2 ways for it to get logging information:

1. Get logs forwarded from **sytemd** via a socket (**/run/systemd/journal/syslog**)
2. Directly from journal API, but requires explicit support from **syslogd**

Allows admins to sort messages by source and importance

**rsyslog (rsyslogd)** is the newer implementation

Runs continuously after boot and reads messages directly from socket (**/dev/log**), consults its configuration file on routing, and then sends the message off

- has the ability to listen for messages on network sockets

Can be configured in the **/etc/rsyslog.conf** but requires restart to take effect

Understands 3 configuration syntaxes:

1. Orginal syslog format
2. Legacy rsyslog directives that begin with a $ sign
3. RainerScript

Rsyslog supports modules that can extend the capabilities and allows:

- input and output configuration
- parse and mutate messages

Modules can be configured with legacy or RaineScript configuration formats

---

Kernel logging at boot time entries are stored in an internal buffer large enough for all the messages about kernel boot

**logrotate** utility implements a variety of log management policies

- allows log files to be moved around without interrupting their logging process
