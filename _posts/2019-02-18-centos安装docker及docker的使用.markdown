---
layout:     post
title:      "centos安装docker及docker的使用"
subtitle:   ""
date:       2019-02-18 10:30:00
author:     "yan"
header-img: "img/post-bg-2019-01.jpg"
top-img: "/img/s3.jpg"
catalog: true
tags:
    - 学习
    - linux
    - docker
---
### 安装
1. centos6  
  `yum install http://mirrors.yun-idc.com/epel/6/i386/epel-release-6-8.normal.rpm\`  
  `yum install docker-io`  
2. centos7  
  `yum install docker`  

### 设置docker服务开机自启
`service docker start` >> 启动  
`chkconfig docker on`  >> 设置自启
### docker概念介绍
**容器**：容器是独立运行的一个或一组应用。  
**镜像**：Docker 镜像是用于创建 Docker 容器的模板  
**仓库**:Docker 仓库用来保存镜像，可以理解为代码控制中的代码仓库。Docker Hub(https://hub.docker.com) 提供了庞大的镜像集合供使用    
### 使用原理
&emsp;&emsp;在centos镜像的基础上，建立一个容器，在该容器中部署系统服务所需的运行环境，即安装各种服务和运行所需的包，并在创建容器时将系统代码挂载到容器内，一切安装完之后，在工程目录下创建启动脚本，然后提交产生新的镜像，此时新的镜像已具备了运行服务的能力，在部署系统时使用此镜像建立一个容器，创建命令如下：  
 &emsp;&emsp;`docker run -d --name docker-demo --net=host -v /home/wy/demo:/home/demo wang/demo:v1 sh /home/demo/start.sh`  
此时的容器已启动了系统服务，可通过命令：  
&emsp;&emsp;`docker logs docker-demo`  
查看系统的访问日志。
### 镜像相关操作
获取镜像：  
  &emsp;&emsp;`docker pull  镜像名`  
创建（提交）镜像：  
  &emsp;&emsp;`docker commit -m 'new msg' -a 'new reason' 容器名 wang/task:v1`  
  -m：指定提交的说明信息  
  -a：指定更新的用户信息  
存出镜像：  
  &emsp;&emsp;`docker save -o wang_task.tar wang/task:v1`  
载入镜像：  
  &emsp;&emsp;`docker load --input wang_task.tar`  
  或  
  &emsp;&emsp;`docker load < wang_task.tar`  
移除镜像：  
  &emsp;&emsp;`docker rmi wang/task:v1`  
### 容器相关操作  
创建容器：  
  &emsp;&emsp;`docker run -i -t --name test centos /bin/bash`  
  -d:守护式运行，后台运行  
启动容器：  
  &emsp;&emsp;`docker start test`  
停止容器：  
  &emsp;&emsp;`docker stop test`  
删除容器：  
  &emsp;&emsp;`docker rm test`  
导出容器：  
  &emsp;&emsp;`docker export test > test.tar`  
导入容器：  
  &emsp;&emsp;`cat test.tar | docker import - test/test:v1`  
  导入一个容器快照，没有所有的历史记录和元数据信息  
进入容器：  
  &emsp;&emsp;`docker attach test`  
  &emsp;&emsp;`docker exec -it test /bin/bash`  
查看日志：  
  &emsp;&emsp;`docker logs test`  
### 容器与主机间的文件拷贝
1. 容器到宿主机   
docker cp 容器名:文件路径      宿主机路径  
&emsp;&emsp;`docker cp test:/home/test   /home/wy/test`  
2. 宿主机到容器   
docker cp 宿主机路径     容器名:文件路径  
&emsp;&emsp;`docker cp /home/test     test:/home/wy/test`   

### docker容器日志清理
1. `docker inspect 容器id或容器名`
2. 找到log的位置，即/var/log/...log-json.log
3. `cat /dev/null > /var/log/...log-json.log`

### docker容器中文编码问题
1. 进入容器，编辑/etc/profile文件
2. 在最后面加上：
  `export LANG = en_US.UTF-8`
