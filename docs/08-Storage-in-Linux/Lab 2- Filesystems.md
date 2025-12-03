
1. This lab requires some commands to be run as the root user. Always use sudo.

Bob's default password is caleston123

2. Which of the following filesystems does not use a journal?
```
EXT2 does not use a journal and hence has longer recovery boot time.
```
3. Out of the disks /dev/vdd and /dev/vde, which one has a filesystem created?

```
Run: sudo df -h

/dev/vdd is mounted at /mnt/backups. This is only possible if it has a filesystem.
```
4. Can you find out the type of filesystem created in /dev/vdd?

Use the blkid command with the disk name as the argument.

```
Run: sudo blkid /dev/vdd
```
5. Create an ext4 filesystem on the disk /dev/vde and mount it at /mnt/data

```
Run: sudo mkfs.ext4 /dev/vde

sudo mkdir /mnt/data

sudo  mount /dev/vde /mnt/data
```
6. What would happen to the mount /mnt/data after a system reboot?
```
The mount is not persistent in FSTAB yet. If the system is rebooted, the filesystem will not be mounted
```
7. Make the mount persistent across reboot.

Use rw option with the dump and pass numbers both set to 0

```
dd it in the FSTAB
Run: sudo vi /etc/fstab
Add the line /dev/vde /mnt/data ext4 rw 0 0
Save and Exit.
```






