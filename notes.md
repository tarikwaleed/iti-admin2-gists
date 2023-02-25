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
- create volume group
```shell
vgcreate
```
- remove volume group
```shell
vgremove
```
- volume group summary
```shell
vgs
```
- create logical volume
```shell
lvcreate
```
- display info about logical volumes
```shell
lvdisplay
```
- extend logical volume (for ext4)
```shell
lvextend -r L +1G /dev/example/lv1
```
- extend logical volume (for xfs)
```shell
xfs_growfs /dev/example/lv1
```
- resize filesystem
```shell
resize2fs /dev/example/lv2 1G
```
- check filesystem
```shell
e2fsck
```
- reduce logical volume
```shell
lvreduce 
```
## Network Adminstration
Tools:
`nmcli` -> form permenant configuration
`ip addr` -> form temporary configuration (won't persist after reboot)
`nmtui` -> permenant configuration

- to show the ip addres
```shell
ip addr show
```
- to show network interfaces
```shell
ip link show
```
- to show the transimitted and received packets of a network interface
```shell
ip -s link show interface_name
```
- to add/del temporary ip to a network interface
```shell
ip addr add/del dev ens33 192.168.10.60/24
```
- to add/del new network 
```shell
ip route add/del 192.168.11.0/24 via 192.168.10.133
```
- show logical connections
```shell
nmcli connection show
```
- display all config settings for the active connection
```shell
nmcli con show connection_name
```
- display config settings for a network device / device status
```shell
nmcli dev show dev_name
```
- create static connection
```shell
nmcli connection add c0n-name "static-eth0" type ethernet ipv4.address 192.168.10.9/24 ipv4.gatewaw 192.168.10.2 ipv4.dns 192.168.10.2 ifname ens33
```
- modify a connection
```shell
nmcli con modify static-eth0 +ipv4.dns 8.8.8.8 
nmcli connection modify static-eth0 ipv4.method manual
nmcli con modify static-eth0 autoconnect yes
```
- up/down a connection
```shell
nmcli con up/down connection_name
```
- show name servers
```shell
ca /etc/resolv.conf
```
- display the current hostname
```shell
hostnamectl
```
**OR**
```shell
cat /etc/hostname
```
- change the hostname
```shell
hostnamectl set-hostname new_hostsame
```
- show network status
```shell
netstat -ntulp
```
n->numeric
t->TCP
u->UDP
l->listing
p->with processes

## Package Management
### dnf cheat sheet
```shell
dnf searhc {name}           # Search 
dnf list available | more	# List All Packages
dnf list installed 			# List Installed Packages
dnf info <package>			# View Package Information
sudo dnf repolist all		# List All Repositories
sudo dnf install <package>	# Install Package
sudo dnf remove <package>	# Remove Package
sudo dnf check-update 		# Check for Updates
sudo dnf upgrade --refresh  # Update All Packages
sudo dnf update <package>	# Update Package
sudo dnf autoremove			# Remove Orphan Packages
sudo dnf distro-sync		# Synchronise All Packages
dnf help					# Get Help
dnf group list
dnf group install
dnf group info
dnf group remove
dnf clean all
dnf makecache
dnf module list
```
### RPM Cheat sheet
```shell
#Install the package 	
rpm -ivh {rpm-file} 	
#Upgrade the package 	
rpm -Uvh {rpm-file} 	
#Erase/remove/ an installed package 	
rpm -ev {package} 	
#Erase/remove/ an installed package without checking for dependencies
rpm -ev --nodeps mozilla-mail
#Display or list all installed packages 	
rpm -qa 	
rpm -qa | less
#Display installed information along with package version and short description
rpm -qi mozilla-mail
rpm -qi {package} 	
# Find out what package owns the file 	
rpm -qf {/path/to/file} 	 
#Display list of configuration file(s) for a package 	
rpm -qc {package-name} 	
# list documentation of a packaeg
rpm -qd
# Verify signature of the package
rmp -Va
#Display list of configuration files for a command 	
rpm -qcf {/path/to/file} 	
#Display list of all recently installed RPMs 	
rpm -qa --last 	
#Find out what dependencies a rpm file has 	
rpm -qpR {.rpm-file}
rpm -qR {package} 	
rpm -qR bash
```
## Boot Process and systemd
### systemd
- check the content of initramfs image
```shell
lsinitrd
```
- display tree of process
```shell
pstree  
```
- see every process on the syste
```shell
ps aux
```
- view the current release of the kernel
```shell
uname -r
```
- show the systemd release
```shell
systemctl --version
```
- view the boot duration
```shell
systemd-analyze
```
- view each service duration
```shell
systemd-analyze blame
```
- To see the started services that depend on each other
```shell
systemd-analyze critical-chain
```
- To switch from runlevel to another we use init command and runlevel number, for example:
```shell
init 6
```
- to see the current target
```shell
cat /etc/systemd/system/default.target
```
- to list dependencies of a target/service
```shell
systemctl list-dependencies graphical.target/httpd.service
```
- To list the mount, socket, path:
```shell
systemctl list-units --type unit
```
- all available services enabled or disabled
```shell
systemctl list-unit-files --type service --all
```
- All available services active or inactive:
```shell
systemctl list-units --type service --all
```
- get the default target
```shell
systemctl get-default
```
- set the default target
```shell
systemctl set-default target_name.target
```
**OR, Manually symlink**
```shell
ln -sf /lib/systemd/system/target_name.target
/etc/systemd/system/default.target
```
- switch to a target immediately
```shell
systemctl isolate multi-user.target
```
- to start and enable the service in one command
```shell
systemctl enable --now service_name
```
- check service is active/enaled/failed
```shell
systemctl is-active/is-enabled/is-failed service_name
```
- show the service configuration details
```shell
systemctl show service_name
```
### GRUB (Grand Unified Bootloader)
- the grub2 script is at `/boot/grub2/grub2.cfg`

- to apply changes in this file, after editing run the commnad
```shell
grub2-mkconfig -o /boot/grub2/grub.cfg
```
- to set the grub passwor
```shell
grub2-set-password
```
```shell
grub2-mkconfig -o /boot/grub2/grub.cfg
```



## Service Masking
- mask/unmask a service
```shell
systemctl mask/unmask service_name
```




## To access VM from your local machine
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





