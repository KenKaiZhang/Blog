# 2 Booting and System Management Daemons

Booting is a multistep process

1. Finding, loading, and running bootstrap code
2. Finding, loading, and running the OS kernel
3. Running startup scripts and system daemons
4. Maintaining process hygiene and managing system state transistions

`systemd`, the modern system manager daemon

- streamlines the boot process by adding dependency management, support concurrent startup process, and more

The Linux/Unix boot process can be summarized as:

1. Power on
2. Load BIOS/UEFI from NVRAM
3. Probe for hardware
4. Select boot device
5. Identify EFI system partition
6. Load boot loader
7. Determine kernel to boot
8. Load kernel
9. Instantiate kernel data structures
10. Start `init/systemd` as PID 1
11. Execute startup scripts

Filesystems are checked and mounted before system daemon starts

Boot codes are usually stored in ROM

To boot from a non default drive, the other disk must be set to highest priorit and made sure it is enabled as a boot medium

**BIOS** is the traditional PC firmware

- assumes the boot device starts with a record called the Master Boot Record which has two components
  - boot block (first stage boot loader)
  - primitive disk partitioning table

The boot block reads the "active" partition of the table and executes the second stage boot loader from there

**UEFI**, the modern BIOS

UEFI includes the GPT partitioning scheme and can understand File Allocation Tables which allows for EFI System Partition

- ESP is a special partition that stores crucial system files used for boot process
  - can be mounted, read, written, and maintained by any OS since its FAT

UEFI provides standard APIs for acessing system hardwares

**Boot loader**'s main job is to identify and load OS kernel

**GRand Unified Boot Loader** is the "officially" Linux boot loader

- allows configuration sush as boot option and boot menu customizations
- config stored in `grub.cfg` usually kept in `/boot/grub` and generated with `grub-mkconfig`

GRUB can find its way to the root filesystem since it understands most of the common ones

Must run `update-grub` to save the changes

## System Management

When the kernel is loaded, a spontaneous process is created in user space

**`init`** is the system management daemon

- makes sure the system runs the right complement of services and daemons at any given time
- basically a privilaged user-level program
- keeps knowledge of the system mode (single, multiuser, server)

`init` simply runs set of commands or scripts

**`systemd`** is the modernized `init` and can manage

- processes in parallel
- network connections
- kernel log entries

`systemd` is a collection of programs, daemons, libraries, technologies, and kernel components

**unit** is an entity managed, defined, and configured by `systemd` through a unit file

**`systemctl`** is the all purpose command for investigating the status and configuration of `systemd`

Unit files can have a few status:

- `bad`: usually a bad a unit file
- `disabled`: present in `systemd`'s directories but will not start autonomously
  - can be enabled with `systemctl start`
- `enabled`: present and starts autonomously
- `linked`: unit files available through a symlink
  - a link to a unit file somewhere else in the system
  - attached with `systemctl link`
  - not considered native to the system and will be deleted if treated as a native
- `static`: units without installation features so cannot be started autonomously

You can set unit dependency where a unit is dependent on another when enabled

Check out the target system boots into by default with `systemctl get-default`

- can easily be changed with `systemctl set-defaukt`

### `Systemd`'s Dependency System

1. Not all dependencies ar explicit
2. Makes some assumptions about the normal behavior of most kinds of units

`[UNIT]` section of the unit files indicates the dependencies between between 2 units

- other than `Conflicts` which indicate a unit cannot run at the same time as another unit

### `Systemd` Logging

**`journald`** daemon will capture and store all jernel and service messages from early boot to final shutdoen in `/run`

- access these logs with the **`journalctl`** command
- configure behaviors in `/etc/systemd/journald.conf`

## Reboot and Shutdown Procedures

The **`halt`** command will log the shutdown, kill nonessential processes, flushes cached filesystem blocks to disk, and then halt the kernel

**`reboot`** will do the same, but reboot instead

Avoid destroying your system with a **`shutdown`**
