---
layout: post
title: Memcache 学习笔记（二）：telnet 操作 memcached 中的数据
categories: [memcache]
tags: [memcache]
---

memcached 由客户端和服务端组成，服务端安装配置好之后，可以通过 telnet 本地的 memcached 端口来进行测试是否安装成功，也可以练习一些基本的命令来操作数据。这篇主要是看了《Using memcached: How to scale your website easily》这本书里面的例子之后整理出来的，书中一些没有的命令式参考网上别人的博客，主要有这两篇：  
[memcached命令行参数说明](http://blog.csdn.net/wanghai__/article/details/8539435)
和
[memcached 命令操作详解](http://www.cnblogs.com/azheng007/p/3159345.html)    


### ubuntu 中安装 memcached 服务端

	sudo apt-get install memcached

当然也可以直接下载源码来便已安装。


### 配置 memcached 服务

ubuntu 中使用 apt-get 方法安装的话，可以通过 `memcached` 命令来启动 。不过一般会加一些参数来进行配置。配置的时候，可以使用 `memcached -h` 来查看帮助信息，常用的参数有：

- -p	: 使用的端口号，默认是 11211							
- -m	: 最大内存大小，默认是 64M								
- -vv	: 用very vrebose模式启动，调试信息和错误输出到控制台	
- -d	: 作为daemon在后台启动									

指定不同的端口，可以同时启动多个 memcached 服务。


### 使用 telnet 操作数据

在 memcached 服务端的机子上启动 memcached 服务之后，可以通过执行 `telnet 127.0.0.1 11211` 来连接。  
(telnet 操作最无法忍受的是左右方向键不能用、backspace 键不能用，这样命令一输错的话，只能重新来过，或许有有什么方法我不知道，查了也没有查到 >_<)  
往 memcached 中添加或更新数据时，会返回 STORED / NOT_STORED 来指明数据知否成功插入或更新。  
操作的基本形式是：

command &lt;key&gt; &lt;flags&gt; &lt;expiration time&gt; &lt;bytes&gt;
&lt;value&gt;

- key				：key 用于查找缓存值  
- flags				：可以包括键值对的整型参数，客户机使用它存储关于键值对的额外信息  
- expiration time	：在缓存中保存键值对的时间长度（以秒为单位，0 表示永远）  
- bytes				：在缓存中存储的字节点  
- value				：存储的值（始终位于第二行） 

set： 添加一个新条目或者更新已存在的条目。  

	set test1 0 0 10
	testing001
	STORED

add： 添加一个新条目，只有当插入的 key 不存在是才插入成功。  

	add test1 0 0 10
	testing002
	NOT_STORED
	add test2 0 0 10
	testing002
	STORED

replace： 更新一个条目，只有当更新的 key 存在的时候才更新成功。  

	replace test1 0 0 10
	testing003
	STORED
	replace test3 0 0 10
	testing003
	NOT_STORED

get： 通过 key 来取值。取单个key的时候，如果有值，返回三行，第一行以 VALUE 开头，指出是哪个key，第二行才是真的值，第三行以 END 结尾。如果没有值，则直接返回 END。 取多个值的时候，get 后面的多个key 用空格分开，返回结果是把有值的两行两行地拼起来，最后跟一个 END 结尾。  

	get test1
	VALUE test1 0 10
	testing003
	END
	get test4
	END
	get test1 test2
	VALUE test1 0 10
	testing003
	END

gets： 比 get 命令多返回一个int值，用来唯一标识该值，如果把值改掉，那这个int值就会改变。可以用来判断数据是否发生过改变。  

	gets test1
	VALUE test1 0 10 5
	testtest01
	END
	set test1 0 0 10
	test01test
	STORED
	gets test1
	VALUE test1 0 10 6
	test01test
	END

cas： 意思是 check and set ，只有当最后一个参数 与 gets 得到的那个int值相同的时候，才会设置成功，否则返回 EXISTS。  

	cas test1 0 0 10 5
	test02test
	EXISTS
	cas test1 0 0 10 6
	test03test
	STORED
	get test1
	VALUE test1 0 10
	test03test
	END

delete： 删除指定 key 对应的值。  

incr / decr ： 自增 / 自减。  

flush_all： 清空所有条目。  

append / prepend：  相当于 string 的 append 跟 prepend。