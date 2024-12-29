---
title: docker部署mongo
date: 2022-11-10 10:45:29.165
updated: 2022-11-10 10:45:29.165
url: /archives/docker-bu-shu-mongo
categories: 
- 数据库相关
tags: 
---

基本的docker命令就不说了，按照下面的-v参数创建目录即可，需要注意的是mongodb.conf需要填写mongo的配置，下面是一个例子
```
systemLog:
	destination: file
	path: /var/log/mongodb/mongodb.log
storage:
	dbPath: /data/db
net:
	bindIP: 0.0.0.0,::
	port: 27017
# 这里一开始不要填写，设置完管理员用户再填上
security: 
	authorization: enabled

```
```
# docker pull mongo:latest
# ocker run --name mongodb -d -p 27017:27017 -v /root/.docker/mongodb/db:/data/db -v /root/.docker/mongodb/logs:/var/log/mongodb -v /root/.docker/mongodb/conf/mongodb.conf:/etc/mongo.conf mongo:latest
```
[一个新的创建默认管理员方案](https://www.mongodb.com/compatibility/docker), 个人部署偷懒使用