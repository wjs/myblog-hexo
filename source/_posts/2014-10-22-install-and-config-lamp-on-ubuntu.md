---
layout: post
title: Ubuntu 14.04安装配置LAMP
categories: [php]
tags: [php, ubuntu]
---

我比较懒，所以就直接用一条命令安装了：

	sudo apt-get install lamp-server^

注意最后有一个^。配置的话，使用上面的命令安装，配置文件一般都在对应的`/etc/`目录下，即

	/etc/apache2/
	/etc/php5
	/etc/mysql

apache 2.4.7 版本的配置跟老版本有一些区别，得先把`/etc/apache2/apache2.conf`里面的`/`目录的访问权限改一下，由`denied`变成`granted`。如果配置虚拟主机出现`127.0.0.1`不能访问的情况，可能在改配置文件的最底下加一句`ServerName  127.0.0.1`。  

接下来是配置虚拟主机，进入 `/etc/apache2/sites-available/`目录下，把`000-default.conf`复制一份并重命名，然后在里面编辑对应的目录以及ServerName。最后到 `/etc/apache2/sites-enabled/`目录下建立软连接，把刚才新添加的虚拟主机模块链接过来，重启apache服务。  

测试php时echo中文发现会乱码，则可以到`/etc/php5/`目录下找`php.ini`（可能在子目录下），修改`default_charset = "utf-8"`。  

如果还是没搞懂的话，建议去慕课网找一下教程，那个老师讲得挺好的。