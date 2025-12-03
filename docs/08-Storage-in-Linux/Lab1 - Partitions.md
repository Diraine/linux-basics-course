
1. This lab requires some commands to be run as the root user. Always use sudo. <br> Bob's default password is caleston123

2. How many disk-type block devices are present in the system?
```
Run: lsblk and look for disk devices
```
3. What is the size of the disk /dev/vdd?

4. What is the major number for the devices beginning with vd?

5. How many maximum partitions (primary or extended ) can an MBR have?
  
```
4
```
6. How many partitions does the disk /dev/vda have currently?

```
Run: sudo fdisk -l /dev/vda or lsblk.
```
7. Create a GPT partition called vde1 of size 500M on the disk /dev/vde

```
Run: sudo gdisk /dev/vde
In the interactive prompt, enter n
Select parition number = 1 (for vde1)
Select default first sector = 2048
Select +500M when asked for last sector
Use default hex code = 8300
Finally type w to write to the partition table
```





