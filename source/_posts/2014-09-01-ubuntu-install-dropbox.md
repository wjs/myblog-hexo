---
layout: post
title: Ubuntu 安装 dropbox 卡死解决方法
categories: [ubuntu]
tags: [ubuntu, dropbox]
---

话说 dropbox 被封已经有几个月了，不过万幸的是刚好是在我毕业答辩之后，我的毕业论文当时全放 dropbox 上。之后好久没登上去过，尝试用了国内的几个同步盘，还是觉得 dropbox 好用，而且长期在 linux 下，能用的也之有金山快盘，但不知是我网络问题还是怎样，很小的文件同步都好好久，于是放弃了。最近配好了 vpn，于是把 dropbox 重新用起来。  

以前也在 ubuntu 上装过，只是忘记了 软件中心 的版本有问题，这次不小心在那里安装，结果就一直卡死在 Applying Change 那里，重启之后也没用，终端使用 apt-get 提示被锁住。网上查了找到了这篇博客：  
[Ubuntu12.04 64bit 安装 Dropbox](http://www.cnblogs.com/lovedeeply/p/3691512.html)  
他遇到了同样的问题，按照他的做法最终解决了。具体步骤：  

	sudo rm /var/cache/apt/archives/lock
	sudo rm /var/lib/dpkg/lock
	sudo apt-get clean
	sudo apt-get update
	sudo apt-get --purge remove nautilus-dropbox
	sudo apt-get --purge autoremove

这样就可以彻底卸载掉通过 软件中心 安装的 dropbox，然后到 [dropbox官网](https://www.dropbox.com) (现阶段需要翻) 下载对应的 deb 包，安装之后，不要直接打开，因为我没设置全局代理，打开之后是无法在线安装的。于是通过通过命令行 proxychains 来打开就就可以了，前提是 proxychains 已经配置好了。

	proxychains dropbox start -i

首次运行需要加 `-i` 参数来在线安装。安装完成之后再在软件的界面进行代理设置，以后启动就都走代理了。

***
另外，软件中心的 virtualbox 好像也有问题，最好直接从官网下载。