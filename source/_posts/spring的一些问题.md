---
title: spring的一些问题
date: 2020-11-09 15:23:20
tags:
---

如果你的Spring boot项目不小心被引入了Spring web，但是没有人需要的时候，这时你需要做一些修改

<!-- more -->

## 方案一：在application.yml Spring配置加入如下信息
```yml
spring:
    main:
      web-application-type: none
```

## 方案二：修改你的main方法,使用如下写法
```java
     SpringApplication springApplication = new SpringApplication(YourMain.class);
        springApplication.setWebApplicationType(WebApplicationType.NONE);
        springApplication.run(args);
```
## 方案三：在maven排除web依赖，但这个方法可能会导致问题

# 记录一些遇到该问题坑的框架
1. [一个分布式事务框架 seata](https://github.com/seata/seata),PS:分布式事务这个东西个人很不喜欢，还是在设计的时候避免这个玩意儿吧，太坑，要及时更新代码，别希望靠这玩意儿解决技术债。
1. 待补充