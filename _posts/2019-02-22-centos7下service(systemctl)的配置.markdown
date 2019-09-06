---
layout:     post
title:      "centos7下service(systemctl)的配置"
subtitle:   ""
date:       2019-02-22 08:30:00
author:     "yan"
header-img: "img/bg_090602.jpg"
top-img: "/img/service.jpg"
catalog: true
tags:
    - 学习
    - centos7
---
#### service介绍
&emsp;&emsp;service命令用于对系统服务进行管理，比如启动（start）、停止（stop）、重启（restart）、查看状态（status）等。
在centos7之前，系统启动服务使用`service https start`的方式启动，此时其实是启动了存放在/etc/init.d目录下的脚本，在centos7中，服务管理修改了规则，centos7集成了RHEL 7的新的特性，例如强大的systemctl，而systemctl的使用也使得以往系统服务的/etc/init.d的启动脚本的方式就此改变，也大幅提高了系统服务的运行效率。但服务的配置和以往也发生了极大的不同，说实在的，变的简单而易用了许多。
#### service配置
&emsp;&emsp;centos7的服务配置文件默认位置在/usr/lib/systemd目录下，有系统和用户之分，需要开机不登录就能运行的程序，在系统服务里，即/usr/lib/systemd/system目录下。  
&emsp;&emsp;每一个服务均以.service结尾，文件分为三部分，[Unit], [Service]和[Install]，完成脚本后，以754权限保存在以上目录。  
&emsp;&emsp;以下为MongoDB集群的一个分片shard配置的服务示例mongo_shard1.service:
```
[Unit]
Description = mongodb service:shard1 Primary
After = syslog.target  network.target

[Service]
Type = forking
ExecStart = /usr/bin/mongod -f /data/config/primary.conf
ExecStop = /bin/kill -2 $MAINPID
KillMode = process
Restart = on-failure
User = root
Group = root

[Install]
WantedBy = multi-user.target
```
#### service启动
1. 启动  
`systemctl start mongo_shard1`
2. 设置开启自启  
`systemctl enable mongo_shard1`  
<img src="../../../../img/404-bg.jpg" style="width:50%" />
![hello](../../../../img/404-bg.jpg)
