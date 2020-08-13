---
layout: docker swarm
title: Docker Swarm
date: 2020-08-13 08:01:40
tags: Docker Swarm
keywords: Docker Swarm
categories: Docker Swarm
---
# Docker Swarm
<!--more-->

### 集群

```bash
##### 初始化集群
> docker swarm init --advertise-addr <MANAGER-IP>

##### 检索工作程序的加入命令(管理器节点上运行)
> docker swarm join-token [OPTIONS] (worker|manager)
> docker swarm join-token manager
> docker swarm join-token worker

##### 加入集群
> docker swarm join --token <your_token> <your_ip_address>:2377

##### 查看集群节点信息（需Manager)
> docker node ls

##### 将 node2 提升为 manager
> docker node promote node2

##### 将 node2 降级为 worker
> docker node demote node2

##### 脱离集群
> docker swarm leave
> docker swarm leave -f -- 强制该节点离开群，忽略警告

##### 驱逐节点并显示它的新可用性
> docker node update --availability drain node13
> docker node inspect node13 --pretty

##### 恢复在线状态并显示它的新可用性
> docker node update --availability active node13
> docker node inspect node13 --pretty

##### 更新swarm
###### 节点证书的有效期
> docker swarm update --cert-expiry 720h
```

### 服务

```bash
##### 查看服务
> docker service ls
> docker service ps web01
> docker service inspect --pretty web01

##### 部署服务
> docker service create -p 80:80 --name web nginx:latest
> docker service create --replicas 1 --name web01 nginx
> docker service create --replicas=3 --name web01 -p 88:80 nginx:1.12

##### 删除服务
> docker service rm web

##### 检查服务
> docker service inspect <serviceName>
> docker service inspect web

##### 扩展服务
> docker service scale web=15
> docker service ls
> docker service ps web

##### 滚动更新
> docker service create --replicas 3 --name redis --update-delay 10s redis:3.0.6
> docker service update --image redis:3.0.7 redis
```

### Docker Engine API

- [#Develop with Docker Engine API](https://docs.docker.com/engine/api/)
