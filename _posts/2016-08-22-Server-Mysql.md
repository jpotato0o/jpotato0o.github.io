---
layout:            post
title:             "Server-building"
date:              2016-08-22 12:25:00 +0300
tags:              Server 
category:          server
author:            sjiang
---

Install JDK.

Install mysql.
Install tomcat/nginx.


### install mysql
	
- 初始化mysql设置（）【当中有个 不区分大小写 在mysql.ini
- 登录mysql 有个临时密码（在日志下）
- 存在密码过期的问题（如果过期需修改列：password_expired）
- % 所有地址登录
- 执行 .sql文件 构建表

### copy tomcat

### 启动web服务器
```bash
	sh startup.sh
	tail -f ./logs
```

程序在webapps下

地址：10.0.210.160：8080/upf

数据库重启：
```bash
	mysqld --defaults-file=../my.cnf --user=mysql &
```

修改host文件 域名解析：	
```bash
	vi /etc/hosts
```

10.0.3.207      sso.portal.unicom.local

10.0.3.208      www.portal.unicom.local

10.0.3.154      sit3.portal.unicom.local 

10.0.3.211   	name.portal.unicom.local

10.0.3.213 		intf2.portal.unicom.local

tomcat启动日志查看：
	
```bash
	tail -f catalina.out
```


linux命令:

ll  权限查看

free 命令显示系统使用和空闲的内存情况，包括物理内存、交互区内存(swap)和内核缓冲区内存。共享内存将被忽略

命令参数:

- b 　以Byte为单位显示内存使用情况
- k 　以KB为单位显示内存使用情况
- m 　以MB为单位显示内存使用情况
- g   以GB为单位显示内存使用情况
- o 　不显示缓冲区调节列
- s<间隔秒数> 　持续观察内存使用状况
- t 　显示内存总和列
- V 　显示版本信息

tail		循环查看文件内容

ps -ef|grep + 运行程序（java，mysql）可查看进程状态

fdisk -l		此命令可以查看到磁盘总空间、分区情况以及每个分区的大小

df -h		可以查看到已挂载的磁盘的大小以及挂载位置
