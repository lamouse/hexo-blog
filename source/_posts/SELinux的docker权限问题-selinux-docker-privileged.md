---
title: SELinux的docker权限问题
date: 2022-11-10 01:13:00.548
updated: 2022-11-10 10:14:54.543
url: /archives/selinux-docker-privileged
categories: 
- Linux系统相关
tags: 
---

[说明](https://www.redhat.com/sysadmin/container-permission-denied-errors)
在不能关闭SELinux的情况下可以在dockers启动命令中加入 --privileged
在使用--privileged Container无法重启，依旧提示没有权限，暂时先关闭SELinux
```# getenforce```可以查看SELinux状态，如果是Enforcing，修改/etc/sysconfig/selinux中的```SELINUX=enforcing```为```SELINUX=disabled```
