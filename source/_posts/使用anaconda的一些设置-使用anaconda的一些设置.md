---
title: 使用anaconda的一些设置
date: 2024-12-09 11:18:27.691
updated: 2024-12-09 11:20:24.663
url: /archives/使用anaconda的一些设置
categories: 
- 工具
tags: 
---

1. 添加PYTHONUSERBASE 环境变量即可修改anaconda自带的pip安装目录
2. 在用户根目录添加.condarc文件，修改anaconda的py虚拟环境和pkg安装目录，内容如下
```
channels:
  - defaults
envs_dirs:
  - D:\libs\python\envs
pkgs_dirs:
  - D:\libs\conda-pkgs
```
3. 网上那种修改site.py方法就不要用了，安装python都得修改一次很麻烦不如一劳永逸