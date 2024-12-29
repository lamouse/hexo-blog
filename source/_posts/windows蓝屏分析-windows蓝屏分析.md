---
title: windows蓝屏分析
date: 2021-03-24 14:09:35.0
updated: 2022-09-05 23:49:57.923
url: /archives/windows蓝屏分析
categories: 
- windows
tags: 
---




## windows蓝屏分析流程

1. [下载](https://developer.microsoft.com/zh-cn/windows/downloads/windows-10-sdk/)win10sdk
1.使用下载的安装包仅安装WinDbg 
1.使用administrator权限启动WinDbg 
<!-- more -->
1.ctrl+s设置符号位置
1.ctrl+d打开蓝屏dmp文件，文件在C:/Windows/Minidump下
1.等待加载出现 !analyze -v,单机
1.主要查看最下面的内容看看发生模块
1.检查STACK_TEXT部分，如果出现例如Netwtw10+0x57486类似'+'连接的部分，搜索Netwtw10(这里是英特尔网卡驱动)表明这个驱动有问题，需要更新驱动，或者回退旧版本。如果是其他类型就得根据实际情况分析了.