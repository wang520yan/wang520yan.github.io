---
layout:     post
title:      "docker集群管理技术--swarm"
subtitle:   ""
date:       2019-02-20 20:30:00
author:     "yan"
header-img: "img/post-bg-2019-021.jpg"
top-img: "/img/swarm.jpg"
catalog: true
tags:
    - 学习
    - docker
---
#### swarm介绍
swarm是用来部署服务的docker Engine集群。
#### swarm
1. 创建一个swarm
```
docker swarm init --advertise-addr 192.179.177.11
```
2. 查看swarm状态
```
docker info
```
3. 第一步执行后会生成加入新节点的swarm命令，执行命令后加入的新节点作为manager或worker
4. `docker node ls`
5. 加入节点命令
`docker swarm join --token 192.168,177.11:2377`
6. 查询添加节点的命令
`docker swarm join-token worker`
7. `docker node ls`

#### 服务service
1. 部署服务
`docker service create --replicas 3 | --name hello -p 80:80 nginx`  ---> 启动一个副本数为3的nginx服务
`docker service ls`
2. 查询服务的详细信息
`docker service inspect --pretty hello`
`docker service ps hello`
3. 扩容缩容
`docker service scale hello=5`
4. 删除服务
`docker service rm hello`
5. 滚动更新
`docker service create --replicas 3 --name redis --update-deloy 10s redis:3.0.6`
`docker service update --image redis:3.0.7 redis`
6. 下线节点
`docker node update --availability drain worker1`
7. 上线节点
`docker node update --availability active worker1`
8. 发布服务器端口
-publish 80：80
TCP -p 53:53/tcp
UDP -p 53:53/udp
9. 升级或降级节点
`docker node promote node-2 w->m`
`docker node demote node-12`
