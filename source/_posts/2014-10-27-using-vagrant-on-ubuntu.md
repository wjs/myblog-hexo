---
layout: post
title: Ubuntu 14.04 下安装使用 vagrant
categories: [vagrant]
tags: [vagrant, ubuntu]
---

虽然xubuntu已经作为主系统，但是配开发环境之后，开机就变得好慢，最近开始弄php，不想在真机上直接搭lamp，于是就想用一下vagrant，之前在win7上装过，挺好用的。网上搜了一下，有一篇博客写的很详细：[vagrant使用简介](http://xuclv.blog.51cto.com/5503169/1239250)   


### 安装

先安装 virtualbox，然后到 [vagrant官网](http://www.vagrantup.com/) 下载对应的linux版本安装。  
之后到 [http://www.vagrantbox.es/](http://www.vagrantbox.es/) 下载已经做成vagrant box的虚拟机镜像。

然后建一个 vagrant 的工作目录（比如 `~/vagrant`），把下载的虚拟机镜像放到该目录下，然后执行：  

	vagrant box add base XXXX.box

base 表示指定默认的box，也可以为box指定名称，比如 centos63 ，使用base时，之后可以直接使用 vagrant init 进行初始化，如果自行指定名称，则初始化的时候需要指定box的名称。之后执行：

	vagrant init

就会在该目录下生成对应的 Vagrantfile。可以直接修改 Vagrantfile 里的配置。  
注意： linux下，virtualbox 不允许把host小于 1024 的端口映射到虚拟机中，因此下面这样配置是无效的：

	config.vm.network :forwarded_port, guest: 80, host: 8080

这个问题可以在stackoverflow上找到答案。  


### 常用命令  

	$ vagrant box add NAME URL    #添加一个box
	$ vagrant box list            #查看本地已添加的box
	$ vagrant box remove NAME virtualbox #删除本地已添加的box，如若是版本1.0.x，执行$ vagrant box remove  NAME
	$ vagrant init NAME          #初始化，实质应是创建Vagrantfile文件
	$ vagrant up                   #启动虚拟机
	$ vagrant halt                 #关闭虚拟机
	$ vagrant destroy            #销毁虚拟机
	$ vagrant reload             #重启虚拟机
	$ vagrant package            #当前正在运行的VirtualBox虚拟环境打包成一个可重复使用的box
	$ vagrant ssh                 #进入虚拟环境

