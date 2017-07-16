---
title: Resizing a VirtualBox Virtual Machine (Debian) hard disk with LVM
date: 2016-12-09 15:20:15
tags:
  - virtualbox
  - resize
  - hard disk
  - lvm
---

## 磁盘相关的一些命令
> fdisk -l
> 
> df

## Hard disk format: vmdk to vdi
```
VBoxManage clonehd disk.vmdk disk.vdi --format vdi
```

## Hard disk resize
```
vboxmanage modifyhd --resize 20000 ./New_VM.vdi
```

## Resize the partition

### Download Gparted.iso
[Download GParted](http://gparted.org/download.php)

> 启动时加载GParted.iso，就可以进行分区管理啦。。。

<font color=red>*资料：*</font>
>大家可以看下这里学习一下：
[LVM相关介绍](https://wiki.archlinux.org/index.php/LVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))