---
title: vcpkg的简单用法
date: 2024-12-16 11:32:05.768
updated: 2024-12-16 11:32:05.768
url: /archives/vcpkg-de-jian-dan-yong-fa
categories: 
- 工具
tags: 
---

 #### 获得基线（baseline）输入该命令即可
```
vcpkg x-update-baseline
```
 #### 在cmake中的使用
 ```
 find_package(glfw3 CONFIG REQUIRED)
 #如果在vcpkg.json配置的glfw3依赖，cmake会自动下载构建该项目构建目录在build/vcpkg_installed
 可以在cmakelist.txt加入以下配置
 if(NOT DEFINED CMAKE_TOOLCHAIN_FILE)
        set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake")
endif()
$ENV{VCPKG_ROOT} 
ENV要代表读取环境变量，VCPKG_ROOT是个人设置的环境变量，可以在vscode中设置也可以在系统或者用户环境变量中设置
 ```