---
title: socket编程中的问题
date: 2022-08-20 14:27:07.0
updated: 2022-09-05 23:49:14.935
url: /archives/socket编程中的问题
categories: 
- linux编程相关
tags: 
---



## accept
accept的第三个参数在《unix网络编程》中代码没有进行初始化，在mac的man accept中明确要求初始化，如果未初始化便会出现accept第二个参数sockaddr未正确设置的问题
```
 The address_len is a value-result parameter; it should initially contain
     the amount of space pointed to by address; on return it will contain the actual
     length (in bytes) of the address returned.
```

<!-- more -->

##socket address
自己储存socket address的时候使用sockaddr_storage这个结构体并加上数据的长度，如果使用struct sockaddr这个结构体存储的话，当协议地址长度大于sockaddr的时候，多余的部分将会被忽略，例如ipv6的地址结构s struct sockaddr_in6的长度大于sockaddr的长度，导致使用类似bind， connect时候出现异常