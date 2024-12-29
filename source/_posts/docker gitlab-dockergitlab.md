---
title: docker gitlab
date: 2022-11-10 12:30:48.886
updated: 2022-11-10 14:27:29.25
url: /archives/dockergitlab
categories: 
- 工具
tags: 
---

做个备份[官方地址](https://docs.gitlab.com/ee/install/docker.html)，记得把部署命令中的ee版本改为ce版本, 因为懒得修改gitlab的ssh port所以修改了系统的sshd port
修改gitlab.rb中的
```
external_url '你的地址'
nginx['enable'] = true
nginx['listen_port'] = 8001
nginx['listen_https'] = false
```
之所以这样些而不是用url:port的方式主要是因为使用了nginxproxymanage代理了gitlab，并且启用了https，不希望gitlab中的http(s)克隆地址出现端口号
[官网说明](https://docs.gitlab.com/omnibus/settings/ssl/index.html#configure-https-manually)
重新部署gitlab
```
docker run --detach \
  --publish 8001:8001 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume /root/.docker/gitlab/config:/etc/gitlab \
  --volume /root/.docker/gitlab/logs:/var/log/gitlab \
  --volume /root/.docker/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
````
