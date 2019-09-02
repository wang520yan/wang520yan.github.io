---
layout:     post
title:      "linux定时任务crontab"
subtitle:   ""
date:       2019-02-18 19:00:00
author:     "yan"
header-img: "img/post-bg-2019-02.jpg"
top-img: "/img/crontab.jpg"
catalog: true
tags:
    - 学习
    - linux
---
#### 定时任务
1. 系统任务调度
系统周期性所要执行的工作，在/etc下的一个crontab文件，就是系统任务调度的配置文件。
2. 用户任务调度
用户定期要执行的工作，所有用户定义的crontab文件都保存在/var/spool/cron目录下，其文件名与用户名一致。
3. crontab安装  
`yum install crontabs`  
启动：  
`/sbin/service crond start|stop|restart|reload|status`  
设置开机自启：  
`chkconfig -level 35 crond on`
4. crontab命令格式
minute hour day month week command
0~59   0~23 1~31 1~12 0~7  命令
特殊字符：  
`*`:代表可能的值  
`,`:用逗号隔开的值指定一个列表范围，‘1，2，3，4，5’，  
`-`:用中杠表示一个整数范围  
`/`:用正斜线指定时间的间隔频率  `*/10`  
5. crontab命令
```
crontab [ -u user ] file
crontab [ -u user ] [ -e| -l | -r ]
```
-u : 指定用户的crontab任务  
file：命令文件的名字，将file作为crontab的任务列表文件并载入crontab  
-e：编辑用户的crontab文件内容  
-l：现实某个用户的crontab文件内容  
-r：从/var/spool/cron目录中删除某个用户的crontab文件，不指定用户时默认删除当前用户的文件  
-i：删除crontab文件时给出提示。  
