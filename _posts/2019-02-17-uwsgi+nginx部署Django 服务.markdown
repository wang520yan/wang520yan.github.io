---
layout:     post
title:      "uwsgi+nginx部署Django服务"
subtitle:   ""
date:       2019-02-17 14:00:00
author:     "yan"
header-img: "img/post-bg-2019-02.jpg"
top-img: "/img/uwsgi.jpg"
catalog: true
tags:
    - 学习
    - python
    - Django
---

## 前言

Django服务在开发阶段可以使用runserer的方式启动，在生产环境中推荐使用uwsgi+nginx的方式部署，将请求的日志按日期分割后进行保存，供开发人员进行维护和发现问题。

## 正文
1. 安装uwsgi  
&emsp;&emsp; `pip install uwsgi`  
安装完成之后，写一个test.py文件进行测试uwsgi服务是否正常。测试示例如下：  
`def application(env, start_response):`  
    &emsp;&emsp;`start_response('200, ok', ['content-Type', 'text/html'])`  
    &emsp;&emsp;`return ['Hello World']`  
该目录下运行uwsgi，命令如下：  
`uwsgi --http 127.0.0.1:9090 --uwsgi-file uwsgi-test.py`  
在浏览器中访问http://127.0.0.1:9090，即可看到‘Hello World’返回结果。
对于django服务，可使用配置文件的方式启动django服务，配置文件可命名为test_uwsgi.ini，配置文件如下所示：
```   
[uwsgi]  
    socket = :7008  
    chdir  = /home/test  
    module = test.usgi  
    master = true  
    processes = 4  
    vacuum = true  
    threads = 2  
    daemonize = /home/test/test_server.log  
```
配置写好之后，进入/home/test,执行命令：  
&emsp;&emsp;`uwsgi --ini test_uwsgi.ini`  
此时，uwsgi服务已启动。  
2. 安装nginx  
&emsp;&emsp;`yum install nginx`  
修改nginx的配置文件：
```
vi /etc/nginx/nginx.conf  
server {  
	listen: 7006  
	server_name:127.0.0.1  
	charset: utf-8  
	access_log: /var/log/nginx/test_access.log  
	error_log: /var/log/nginx/test_error.log  
	client_max_body_size: 75M;  

	location / {  
	    include  uwsgi_params;  
	    uwsgi_pass  127.0.0.1:7008;  
	    uwsgi_read_timeout: 2;  
    }  

    location /statics{  
        expires 30d;  
        autoindex. on;  
        add_header  Cache_Control private;  
        alias  /home/test/collected_static;  
    }  
}
```
重启nginx，nginx -s reload  
3. 配置Django的settings.py  
```
 (1)STATUC_URL = '/statics/'  
 (2)STATIC_ROOT = os.path.join(BASE_PATH, 'collected_static')  
 (3)STATICFILES_DIRS = (  
    &emsp;&emsp;os.path.join(BASE_DIR, 'task_app/templates/statics'),  
    )  
 (4)STATICFILES_FINDERS = (  
    &emsp;&emsp;"django.contrib.staticfiles.finders.FileSystemFinder",  
    &emsp;&emsp;"django.contrib.staticfiles.finders.AppDirectoriesFinder"  
    )
```
当执行命令`python manage.py collectstatic`收集静态文件时，会将所有（3）中文件夹下的文件和各app下的static中的文件都复制到（2）的目录下。  
在url.py中加入：  
urlpatterns = [] + static(settings.STATIC_URL, document_root = settings.STATIC_ROOT)  
至此uwsgi和nginx服务都已配置好，在浏览器中可正常访问django的服务。
## 后记
容易出问题的地方：  
- 在uwsgi的ini启动文件中的端口号需和nginx配置文件中的uwsgi_pass的端口保持一致，在外部访问django服务的时候访问的端口是nginx配置的listen端口。    
- 静态文件的路径配置问题，在nginx配置文件中的location配置statics时需要和django配置文件中的STATIC_URL保持一致。  
