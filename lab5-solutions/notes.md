# :note: To access VM from your local machine

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
# add note here





