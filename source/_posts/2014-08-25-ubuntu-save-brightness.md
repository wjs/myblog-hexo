---
layout: post
title: Ubuntu保存屏幕亮度
categories: [ubuntu]
tags: [ubuntu]
---

参考了这篇文章：
[http://www.aichengxu.com/article/系统优化/25720_12.html](http://www.aichengxu.com/article/系统优化/25720_12.html)

文章里是直接把亮度设成了 5， 我这里稍微改了一下，可以记录之前调节的亮度。具体做法：

	sudo vim /etc/rc.local
原内容如下：

	#!/bin/sh -e
	#
	# rc.local
	#
	# This script is executed at the end of each multiuser runlevel.
	# Make sure that the script will "exit 0" on success or any other
	# value on error.
	#
	# In order to enable or disable this script just change the execution
	# bits.
	#
	# By default this script does nothing.

	exit 0

在 `exit 0` 之前添加两行代码，如下：

	#!/bin/sh -e
	#
	# rc.local
	#
	# This script is executed at the end of each multiuser runlevel.
	# Make sure that the script will "exit 0" on success or any other
	# value on error.
	#
	# In order to enable or disable this script just change the execution
	# bits.
	#
	# By default this script does nothing.
	
	bri=cat /sys/class/backlight/acpi_video0/actual_brightness
	echo $bri > /sys/class/backlight/acpi_video0/brightness
	
	exit 0

就是把原本的实际亮度写到启动时候加载的那个亮度里，不同电脑具体路径可能有所不同。

***
更新：不知道为什么上面的方法失效了，最终还是改用直接写入最低亮度的方法：   
	echo 0 > /sys/class/backlight/acpi_video0/brightness