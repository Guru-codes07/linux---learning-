# Linux File System

The Linux file system is a hierarchical directory structure that organizes files and directories starting from a single root directory (`/`).

Unlike Windows, which uses drive letters such as `C:\` and `D:\`, Linux stores everything under the root directory.

---

## File System Hierarchy

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var
```

---

## Root Directory (/)

The root directory is the top-level directory of the Linux file system.

All files, directories, devices, and partitions are mounted under this directory.

### Example

```bash
cd /
ls
```

---

## /home

Stores personal files and directories for regular users.

Each user gets their own home directory.

### Example Structure

```text
/home
└── guruprasad
    ├── Documents
    ├── Downloads
    ├── Pictures
    └── Projects
```

### Example Command

```bash
cd /home/guruprasad
```

---

## /root

Home directory of the root (administrator) user.

Do not confuse this with the root directory (`/`).

### Example

```bash
sudo ls /root
```

---

## /etc

Contains system-wide configuration files.

Most Linux configuration files are stored here.

### Common Files

```text
/etc/passwd
/etc/hosts
/etc/fstab
/etc/ssh
```

### Example Command

```bash
ls /etc
```

---

## /usr

Contains applications, libraries, documentation, and user utilities.

Most installed software resides here.

### Important Directories

```text
/usr/bin
/usr/lib
/usr/share
/usr/local
```

### Example Command

```bash
ls /usr/bin
```

---

## /bin

Contains essential commands required for system operation.

### Examples

```text
ls
cp
mv
rm
cat
pwd
```

### Example Command

```bash
ls /bin
```

---

## /sbin

Contains essential system administration commands.

These commands are generally used by the root user.

### Examples

```text
shutdown
reboot
fdisk
mkfs
```

### Example Command

```bash
ls /sbin
```

---

## /var

Stores variable data that changes frequently.

### Common Contents

```text
/var/log
/var/cache
/var/spool
/var/tmp
```

### Example Command

```bash
ls /var/log
```

### Why It Matters

System logs are stored inside `/var/log`, making this directory important for troubleshooting.

---

## /tmp

Stores temporary files created by programs.

Files may be automatically removed during reboot.

### Example Command

```bash
cd /tmp
```

### Example Use Case

Applications often store temporary data here while running.

---

## /boot

Contains files required for system startup.

### Common Contents

```text
Linux Kernel
GRUB Bootloader
Initial RAM Disk (initramfs)
```

### Example Command

```bash
ls /boot
```

---

## /dev

Contains device files.

Linux treats hardware devices as files.

### Examples

```text
/dev/sda
/dev/null
/dev/random
/dev/tty
```

### Example Command

```bash
ls /dev
```

---

## /proc

A virtual file system containing information about running processes and the Linux kernel.

### Useful Files

```text
/proc/cpuinfo
/proc/meminfo
/proc/version
```

### Example Commands

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

---

## /sys

Contains information about hardware devices and kernel subsystems.

Used by the Linux kernel to expose hardware information.

### Example Command

```bash
ls /sys
```

---

## /media

Mount point for removable storage devices.

### Examples

```text
USB Drives
External Hard Drives
DVDs
```

### Example Path

```text
/media/guruprasad/USB_DRIVE
```

---

## /mnt

Used for manually mounted file systems.

System administrators often use this directory when mounting partitions.

### Example

```bash
sudo mount /dev/sdb1 /mnt
```

---

## /opt

Used for optional and third-party software packages.

### Examples

```text
/opt/google
/opt/android-studio
/opt/vscode
```

### Example Command

```bash
ls /opt
```

---

## /run

Stores temporary runtime information.

This directory is recreated every time the system boots.

### Common Contents

```text
Process IDs (PIDs)
System Services
Runtime Data
```

---

## /srv

Contains data served by system services.

### Examples

```text
Web Server Files
FTP Server Files
```

### Example Path

```text
/srv/www
```

---

## Linux File System Navigation Example

```bash
pwd
cd /
ls
cd /home/guruprasad
pwd
```

### Output

```text
/home/guruprasad
/
bin boot dev etc home usr var
/home/guruprasad
```

---

## Linux vs Windows File System

| Linux                       | Windows                         |
| --------------------------- | ------------------------------- |
| Single root directory (`/`) | Multiple drives (`C:\`, `D:\`)  |
| Everything is a file        | Devices are handled differently |
| Uses `/` as separator       | Uses `\` as separator           |
| Case-sensitive              | Usually case-insensitive        |

---

## Summary

| Directory | Purpose                         |
| --------- | ------------------------------- |
| `/`       | Root directory                  |
| `/home`   | User home directories           |
| `/root`   | Root user's home directory      |
| `/etc`    | Configuration files             |
| `/usr`    | Applications and libraries      |
| `/bin`    | Essential user commands         |
| `/sbin`   | System administration commands  |
| `/var`    | Variable data and logs          |
| `/tmp`    | Temporary files                 |
| `/boot`   | Bootloader and kernel files     |
| `/dev`    | Device files                    |
| `/proc`   | Process and kernel information  |
| `/sys`    | Hardware and kernel information |
| `/media`  | Removable media                 |
| `/mnt`    | Temporary mount point           |
| `/opt`    | Third-party software            |
| `/run`    | Runtime information             |
| `/srv`    | Service data                    |

Understanding the Linux file system is fundamental to learning Linux because every command, configuration file, application, and device ultimately exists somewhere within this directory structure.

