---
layout:     post
title:      "centos7安装mamcached"
subtitle:   ""
date:       2019-02-20 16:00:00
author:     "yan"
header-img: "img/post-bg-2019-02.jpg"
top-img: "/img/memcached.jpg"
catalog: true
tags:
    - 学习
    - centos7
    - python
    - mamcached
---
#### memcached介绍
memcached是一个高性能的分布式的内存对象缓存系统，原理是将数据调到内存中，然后从内存中读取，从而大大提高了读取速度。（用在动态应用中减少数据库负载，提高访问速度），数据只存储在内存中，不进行持久化。  
**分布式计算是将N颗cpu组装成一颗。**  
**分布式慢速存储是将N个硬盘组成一个大硬盘。**   
**memcached是将N个内存组装成一个大内存。**  
#### memcached安装
1. yum安装
```
yum install libevent libevent-devel
yum install memcached
```
2. 源代码安装
```
wget http://memcached.org/latest     ----->   下载
tar -zxvf memcached-1.x.tar.gz       ----->   解压
cd memcached-1.x
./configure  --prefix=/usr/local/memcached   ---->   配置
make && make test                 ----->     编译
make install                      ----->     安装
```

#### memcached运行
进入`/usr/local/bin/memcached`目录
1. 前台服务启动：  
`./memcached -p 11211 -m 64m -w`
2. 后台服务启动：
`./memcached -p 11211 -m 64m -d`  
或  
`./memcached -d -m 64m -u root -l 192.168.177.11 -p 11211 -c 256 -P /tmp/memcached.pid`
3. 启动参数详解：  
-d : 启动一个进程  
-m : 分配的内存数量  
-u : 用户  
-l : ip地址  
-p : 监听的端口  
-c : 最大运行的并发数  
-P : 设置保存memcached的pid文件  
#### python访问memcached
`pip install pymemchched`

```
from pymemcached.client.base import Client
mc = Client('192.168.177.11', 11211)
mc.set('name', 'yan')
mc.get('name')

mc.set_multi({'k1': 'v1', 'k2': 'v2'})
mc.get_multi(['k1', 'k2'])
mc.get_many(['k1', 'k2'])
mc.delete_multi(['k1', 'k2'])

mc.add('name', 'li')
mc.replace('name', 'w')
mc.delete('name')

mc.append('name', 'hello')
mc.prepend('name', 'hi')

mc.incr('age', 1)
mc.decr('age', 10)
```
