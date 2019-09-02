---
layout:     post
title:      "centos7下安装python扩展包管理工具pip"
subtitle:   "centos7环境下进行python扩展包管理工具的安装及使用"
date:       2019-02-18 10:00:00
author:     "yan"
header-img: "img/post-bg-2019-021.jpg"
top-img: "/img/exten.jpg"
catalog: true
tags:
    - 学习
    - linux
    - centos7
---
## 安装pip
1. 首先安装epel扩展源  
`yum -y install epel-release`
2. 更新成功之后，安装pip  
`yum -y install python-pip`
3. 安装后清除cache  
`yum clean all`
4. 安装失败之后可执行  
`pip install --upgrade pip`

## 安装python开发环境
```
yum install python-devel
yum install libevent-devel
pip install gevent
yum install groupinstall 'development tools'
pip install --upgrade setuptools
```

## 安装python依赖包
corsheaders ----> 跨域使用  
`pip install django-cors-middleware`
