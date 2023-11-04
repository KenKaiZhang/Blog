# 6 Software Installation and Management

**Localization** is the process of configuring an off the shelf distribution or software package to conform to your needs

Typical installation involves booting from external USB storage

Possible install through network to install OS on multiple systems at once

- mostly use DHCP and TFTP to boot
- OS retreived via HTTP, NFS, or FTP

Common to find a **Preboot Execution Environment (PXE)** on the ROM of the network card

- allows network capabilites enabling network boot

PXE process involves:

1. DHCP requeest with PXE options
2. DHCP server responds with a boot server and its boot file
3. PC asks for the data from the boot server over TFTP
4. Boot server responsds with boot image, files, and configurations
5. PC executes the files

Debian and Ubuntu use the **debian-installer** to install the OS

- relys on the **debconf** utility to decide questions and default answers

## Management

UNIX and Linux software assets are now distributed as **packages** which includes all the files needed ot run a piece of software

- pretty good at avoiding overwriting other files
- can add new users and groups, run sanity checks, and more

**.deb** is the most common Debian and Ubuntu package format and can be installed, uninstalled, and query with **`dpkg`**

`dpkg` includes a `--install`, `--remove`, and `-l` to add, remove, and list packages

- if a package has been installed, it gets updated

High level package management systems will:

- locate and download packages
- automate the updating and upgrading process
- facilitate the management of interpackage dependencies

**Advanced Package Tool** is the most mature package management system and should be used over **dselect**

- can be triggered with the **`apt`** command
- knows where to get packages via the `/etc/apt/sources.list` file

`deb http://ports.ubuntu.com/ubuntu-ports/ jammy-updates main restricted`

- the URL indicates the location APT will grab packages from
- `jammy-updates` indicates the working title or root distributions
- `main` and `restricted` are the components

The distribution and components help APT navigate through the filesystem heirarchy which has a defined layout

You can use **cron** to schedule regular `apt` runs

**`apt update && apt upgrade -y`** will update the system

You can just download packages and not install them with the `--download-only` flage

- anything downloaded will be stored in `/var/cache/apt`
