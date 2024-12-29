---
title: openJDK 在fedora的构建
date: 2020-03-01 17:26:34.0
updated: 2022-09-05 23:50:58.438
url: /archives/openjdk在fedora的构建
categories: 
- java
tags: 
---



##### 通过hg下载源代码

```
hg clone http://hg.openjdk.java.net/jdk/jdk11
```

<!-- more -->

如果没有openjdk10或者11到openjdk官网下载一个即可
如果因为出现编译失败添加参数--disable-warnings-as-errors

##### 执行如下脚本

```
./configure --with-boot-jdk="openjdk10或者11的安装目录" --disable-warnings-as-errors
```