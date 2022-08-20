---
title: socket编程中的问题
date: 2022-08-20 14:27:07
tags:
---

## accept
accept的第三个参数在《unix网络编程》中代码没有进行初始化，在mac的man accept中明确要求初始化，如果未初始化便会出现accept第二个参数sockaddr未正确设置的问题
```
 The address_len is a value-result parameter; it should initially contain
     the amount of space pointed to by address; on return it will contain the actual
     length (in bytes) of the address returned.
```
