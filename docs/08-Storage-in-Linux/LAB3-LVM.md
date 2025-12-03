
1. This lab requires some commands to be run as the root user. Always use sudo.

Bob's default password is caleston123

2. Is LVM installed on this machine?

Try out commands such as pvdisplay or lvs

3. LVM is installed on this machine and you will find that a physical volume has already been created.

What is the name of this physical volume?

```
Run: pvdisplay
```

4. What is the size of this physical volume?

```
Run: pvdisplay and lsblk to verify the size
```

5. What is the name of the volume group created using this PV?

```
Run: pvdisplay or vgdisplay
```

6. Now, we will create a new VG. To do this we will make use of the disks /dev/vde and /dev/vdf

What are the size of these disks individually?

```
Run: sudo lsblk and inspect the size of disks. /dev/vde is 1G and /dev/vdf is 1G.
```
7. Create PV's using /dev/vde and /dev/vdf.

```
Run: sudo pvcreate /dev/vde and sudo pvcreate /dev/vdf
```

8. Create a new volume group called caleston_vg using the newly created PV's

```
Run: sudo vgcreate caleston_vg /dev/vde /dev/vdf
```
9. Create a new logical volume called data from the caleston_vg.


Size of the volume should be 1G

```
Run: sudo lvcreate -L 1G -n data caleston_vg
```

10. Create an ext4 filesystem on this logical volume and mount it at /mnt/media

````
Run: sudo mkdir /mnt/media
sudo mkfs.ext4 /dev/mapper/caleston_vg-data
sudo mount /dev/mapper/caleston_vg-data /mnt/media/
````

11. Add 500M to the logical volume called data.

Do not unmount the filesystem.

```
Run: sudo lvresize -L +500M /dev/mapper/caleston_vg-data
sudo resize2fs /dev/mapper/caleston_vg-data
```






