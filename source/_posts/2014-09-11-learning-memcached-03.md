---
layout: post
title: Memcache 学习笔记（三）：ubuntu 14.04 + php 下使用 memcached
categories: [memcache]
tags: [memcache]
---

虽然关于 memcached 的书还没看完，但是还是想通过一些小例子来体验一下。而且书中关于 memcached API 都是用的 perl 或者 C# 来介绍的，perl 我还没时间学，C# 不想用 = =，于是搜了一下其他语言的使用，发现 digitalocean 的社区里面有个教程： 
[How To Install and Use Memcache on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-memcache-on-ubuntu-14-04)
里面介绍得很详细，英文没那么差的话推荐点上面的链接去看原文。


### 安装 memcached 以及 它对应的php扩展模块

	sudo apt-get update
	sudo apt-get install mysql-server php5-mysql php5 php5-memcached memcached

我的 ubuntu 之前配好了 LAMP 环境的，所以我直接安装 `php5-memcached memcached` 这两个就够了。  
注意：其实是有 `php5-memcache` 和 `php5-memcached` 两个不同的扩展模块的，后者是比较稳定而且实现了更多 feature，所以这里使用了后者。  
安装好之后需要重启 apache service。  


### 检查安装是否成功

	sudo vim /var/www/html/info.php

基本配置 php 环境的时候都回用这个来检查是否安装成功，以及php扩展是否安装成功。info.php 里面写：

	<?php
	phpinfo();
	?>

Esc, :wq 保存退出之后打开浏览器访问该页面。http://server_domain_name_or_IP/info.php  
我是在本机弄的，所以直接访问  localhost/info.php  
在页面中搜索 memcached 字样，查看扩展是否安装成功。  

使用命令 `ps aux | grep memcached` 来查看 memcached 是否运行，使用 `sudo service memcached start | stop | restart` 来开启|关闭|重启 memcached 服务。  


### 测试 memcached 是否可以缓存数据

打开终端 `sudo vim /var/www/html/cache_test.php`，然后输入下面的内容，保存。

	<?php
		$mem = new Memcached();
		$mem->addServer("127.0.0.1", 11211);

		$result = $mem->get("blah");

		if ($result) {
		    echo $result;
		} else {
		    echo "No matching key found.  I'll add that now!";
		    $mem->set("blah", "I am data!  I am held in memcached!") or die("Couldn't save anything to memcached...");
		}
	?>

逻辑很简单，new 出一个 memcached 实例，然后添加本地 memcached server，就可以用 get 方法从本地 memcached server 中取值，如果有值则 echo 出值。如果没有，则 echo 错误信息，并把一个值 cache 进本地的 memcached server 中。  
这样的效果是，第一次访问页面的时候，memcached server 中没有 key 是 blah 的键值对，页面出现 "No matching key found.  I'll add that now!"。 而当第二次访问页面的时候，就可以看到 "I am data!  I am held in memcached!"  


### 测试 memcached 能否缓存数据库中得到的数据

首先先在 mysql 中添加简单的数据。  

	mysql -u root -p

再建一个数据库。  
	
	CREATE DATABASE mem_test;
	USE mem_test;

再创建一个用户叫 test， 密码是 testing123，并给他赋予 mem_test 数据库权限。  

	GRANT ALL ON mem_test.* TO test@localhost IDENTIFIED BY 'testing123';

创建表并添加数据。  
	
	CREATE TABLE sample_data (id int, name varchar(30));
	INSERT INTO sample_data VALUES (1, "some_data");

退出mysql后，再创建一个 php 页面来进行测试。

	sudo vim /var/www/html/database_test.php

内容如下：  
	
	<?php
	$mem = new Memcached();
	$mem->addServer("127.0.0.1", 11211);

	mysql_connect("localhost", "test", "testing123") or die(mysql_error());
	mysql_select_db("mem_test") or die(mysql_error());

	$query = "SELECT name FROM sample_data WHERE id = 1";
	$querykey = "KEY" . md5($query);

	$result = $mem->get($querykey);

	if ($result) {
	    print "<p>Data was: " . $result[0] . "</p>";
	    print "<p>Caching success!</p><p>Retrieved data from memcached!</p>";
	} else {
	    $result = mysql_fetch_array(mysql_query($query)) or die(mysql_error());
	    $mem->set($querykey, $result, 10);
	    print "<p>Data was: " . $result[0] . "</p>";
	    print "<p>Data not found in memcached.</p><p>Data retrieved from MySQL and stored in memcached for next time.</p>";
	}
	?>

也是非常简单，这里直接把 $query 语句 md5 之后再拼接一个 KEY 作为 memcached 的 key，首次 get 里面没有值，回进入 else 里面，然后从数据库中取数据，再调用 set 方法把数据库中的值放到 memcached 中。这里设置了 10 秒钟过期，因此效果是：第一次访问，没有cache，从数据库中取数据。之后的10秒内刷新界面，返回的数据都是 cache 中拿到的，10秒之后 cache 中的数据过期，又从新进入 else ，到数据库中取数据。


### 结论

这两个例子虽然很小，但是对初步了解 memcached 还是很有帮助的。