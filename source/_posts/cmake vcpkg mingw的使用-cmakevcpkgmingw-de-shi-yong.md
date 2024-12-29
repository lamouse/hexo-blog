---
title: cmake vcpkg mingw的使用
date: 2023-09-15 12:02:15.371
updated: 2023-09-15 12:48:11.702
url: /archives/cmakevcpkgmingw-de-shi-yong
categories: 
- c/c++
tags: 
---

1. vcpkg安装包的时候指定TRIPLET类似
```vcpkg install glm:x64-mingw-dynamic```
冒号后面确定了可以进行链接的工具mingw说明需要使用64位mingw链接
1. cmake 生成参数添加 
```-DVCPKG_TARGET_TRIPLET=x64-mingw-dynamic -DCMAKE_TOOLCHAIN_FILE=D:/Program/vcpkg/scripts/buildsystems/vcpkg.cmake```
1. 第二种方式在cmakelist.txt文件project()前面加入如下代码
```
if(WIN32)
        if(CMAKE_C_COMPILER MATCHES "gcc.exe" OR CMAKE_CXX_COMPILER MATCHES "g\\+\\+.exe")
                message(STATUS "Building with mingw")
                set(VCPKG_TARGET_TRIPLET "x64-mingw-dynamic" CACHE STRING "target triplet" FORCE)
        endif()
endif()
```