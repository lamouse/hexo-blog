---
title: Hibernate-Validator使用注意事项
date: 2021-09-01 23:11:28.0
updated: 2022-09-05 23:49:25.36
url: /archives/hibernate-validator使用注意事项
categories: 
- java
tags: 
---



## 注意版本信息

1. `validator-6.x` uses `javax.validation:validation-api-2.0.x`.
1. `validator-5.x` uses `javax.validation:validation-api-1.1.Final`.

## 注意BindingResult顺序
1. 顺序一定要是@Validated 验证的参数 BindingResult bindingResult，否则会出现魔幻bug

## 配置相关
1. 不需要在spring的配置文件加入配置信息直接使用注解即可