---
layout: post
title: Ubuntu常用软件安装脚本
categories: [ubuntu]
tags: [ubuntu, 装机]
---

重装系统后一个个安装这些软件很麻烦，写个脚本可以省很多事儿。

	# 压缩解压相关的软件
	sudo apt-get -y install unace unrar zip unzip p7zip-full p7zip-rar sharutils rar uudeview mpack arj cabextract file-roller
	
	sudo add-apt-repository -y ppa:tualatrix/ppa 
	sudo add-apt-repository -y ppa:linrunner/tlp
	sudo apt-get update

	sudo apt-get -y install ubuntu-tweak dconf-tools tlp tlp-rdw
	sudo apt-get -y install chromium-browser vlc
	sudo apt-get -y install git
	
	# 安装系统工具
	#sudo apt-get -y install yakuake htop lrzsz sysstat sshpass curl nmap nload tree lynx iptraf

	# 安装vim代替vi
	sudo apt-get -y install vim
	echo "alias vi=vim " >> ~/.bashrc
	source ~/.bashrc

自带 openjdk 有写问题，所以还是换回 oracle 的 jdk，java 安装脚本，去官网下载相应的 tar.gz 包之后，保存下面代码到一个 sh 文件中，然后执行即可。下面是以 jdk8 为例：  
	
	#!/bin/sh

	tar -xvf jdk-8*
	sudo mkdir /usr/lib/jvm
	sudo mv ./jdk1.8* /usr/lib/jvm/jdk1.8.0
	sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.8.0/bin/java" 1
	sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.8.0/bin/javac" 1
	sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.8.0/bin/javaws" 1
	sudo chmod a+x /usr/bin/java
	sudo chmod a+x /usr/bin/javac
	sudo chmod a+x /usr/bin/javaws
	java -version

安装 flash

 	sudo apt-get install flashplugin-installer

然后会出现一段下载地址，下载 `tar.gz`后缀的文件， 终端下载会失败，从终端复制那个下载的链接到浏览器下载。然后执行： 

	sudo dpkg-reconfigure flashplugin-installer 

按提示输入下载的包所在的文件夹的路径即可。参考： [经过几天的摸索，终于得出安装flashplugin-installer的方法](http://forum.ubuntu.org.cn/viewtopic.php?t=387865)  