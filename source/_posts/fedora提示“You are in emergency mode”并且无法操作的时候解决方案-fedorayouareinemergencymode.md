---
title: fedora提示“You are in emergency mode”并且无法操作的时候解决方案
date: 2022-11-09 00:09:22.335
updated: 2022-11-09 00:09:52.141
url: /archives/fedorayouareinemergencymode
categories: 
- Linux系统相关
tags: 
---

1. 原因：因为自己把一块挂载到fedora硬盘取下做其他用途，导致fedora开始无法进入系统并提升You are in emergency mode， 并且无法进行任何操作，如歌可以操作按照正常流程操作即可
1. 解决：
	1. 在fedora启动的时候，在看到GRUB菜单时，快速按下键盘的‘E’建
	1. 将箭头移动到rhgb quiet所在的行 
	1. 将rhgb quiet修改为rd.break enforcing=0 （enforcing=0避免执行完整的系统SELinux）
	1. 按下Ctrl+x启动系统 
	1. 现在fedora处于紧急模式，使用读写权限挂载硬盘
	```# mount -o remount, rw /sysroot```
    1. 执行chroot访问系统```# chroot /sysroot```
    1. 使用vi 编辑/etc/fstab ```# vi /etc/fstab```
    1. 删除挂载的硬盘，也可以使用umount ```# umount -v "挂载目录"```
    1. 一直执行exit知道系统执行后续流程并启动 