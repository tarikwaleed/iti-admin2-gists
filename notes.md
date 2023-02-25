# Cheat Sheet
## Storage Administration
```shell
df -h
```
- list all partitions on the system
```shell
lsblk
```
```shell
cat /proc/partitions
```
- To mount what's inside the `/etc/fstab` file
```shell
mount -a
```
- list block devices
```shell
lsblk
```
- pring block devices attributes
```shell
blkid
```
- manipulate disk partition table
```shell
fdisk
```
- list the partition table for specific device
```shell
fdisk -l /dev/sda
```
- create a filesystem on a partition
```shell
mkfs.fs_name /dev/partion_name      
```
- create a partition table on a disk
```shell
fdisk /dev/sda
```
## Swap
- to show RAM and Swap Size
```shell
free -h
```
- setup a linux swap area
```shell
mkswap
```
- Enable swap area
```shell
swapon -a /dev/sdc1
```
- dump 1024 blocks of zeros to a file
```shell
dd if=/dev/zero of=/swap bs=1M count=1024
```

- Generate uuid for a device
```shell
uuidgen /swap
```
## LVM
- create a physical volume
```shell
pvcreate
```
- summary for physical volumes
```shell
pvs
```
- display various attributes of physical volumes
```shell
pvdisplay
```















# To access VM from your local machine
**in Virtual Machine**
```shell
vim /etc/ssh/sshd_config
```
- edit the line
```shell
PermitRootLogin yes
```
- check VM ip address

```shell
ip addr show
```
**on your machine**

```shell
ssh root@{vm-ip-address}
```
---





