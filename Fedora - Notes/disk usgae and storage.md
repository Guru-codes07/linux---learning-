# Disk Usage and Storage

Linux provides several tools to monitor disk space, storage devices, partitions, and file system usage.

---

# Check File System Usage

## df

Displays disk space usage.

### Syntax

```bash
df
```

### Human Readable Format

```bash
df -h
```

### Example

```bash
df -h
```

Output:

```text
Filesystem      Size Used Avail Use%
/dev/sda1        50G  20G   28G  42%
```

---

# Check Directory Size

## du

Displays file and directory sizes.

### Syntax

```bash
du
```

### Human Readable Format

```bash
du -h
```

---

## Size of Current Directory

```bash
du -sh .
```

Example Output:

```text
120M .
```

---

## Size of Specific Directory

```bash
du -sh Downloads
```

---

# View Storage Devices

## lsblk

Lists block devices.

### Example

```bash
lsblk
```

Output:

```text
NAME   SIZE TYPE
sda    500G disk
├─sda1 100G part
└─sda2 400G part
```

---

# View Partition Information

## fdisk

Display partition table.

### Command

```bash
sudo fdisk -l
```

---

# Mount File Systems

### Syntax

```bash
sudo mount <device> <directory>
```

### Example

```bash
sudo mount /dev/sdb1 /mnt
```

---

# Unmount File Systems

### Syntax

```bash
sudo umount <directory>
```

### Example

```bash
sudo umount /mnt
```

---

# View Mounted File Systems

```bash
mount
```

---

# Disk Usage of Top Directories

```bash
du -sh *
```

Useful for finding large directories.

---

# Find Largest Files

```bash
find . -type f -exec du -h {} + | sort -rh | head
```

---

# Check Available Inodes

```bash
df -i
```

Useful when a disk appears full despite free space.

---

# Summary

| Command  | Purpose                   |
| -------- | ------------------------- |
| df       | Display disk usage        |
| df -h    | Human-readable disk usage |
| du       | Directory size            |
| du -sh   | Directory summary         |
| lsblk    | List storage devices      |
| fdisk -l | View partitions           |
| mount    | Mount file system         |
| umount   | Unmount file system       |
| mount    | View mounted file systems |
| df -i    | Display inode usage       |

Understanding storage and disk usage is important for system administration, troubleshooting, and managing Linux servers.

