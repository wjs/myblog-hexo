---
layout: post
title: Bandwagonhost VPS + Shadowsocks
categories: [vps]
tags: [vps]
---

今年五六月份开始google就被封了，虽然自己平时用goagent影响不太大，但是我的N7在收到4.4.4更新之后，一直无法下载，我又不想root，于是想整一个vpn。但是发现国内的各种梯子对我开说都还挺贵的，于是就想买一个便宜的vps来自己搭一个vpn，主要给自己的移动端翻墙用，于是就有了这篇博客。   

### 选择vps

最近常混 v2ex，上边牛人很多，找了 VPS 相关的节点看了看，大多都推荐 DO 跟 linone，但我就是单纯为了移动端翻墙建vpn，没必要整那个贵的，所以就先试了搬瓦工的，便宜的vps更推荐Ramnode和Hostigation，据说速度比较好，但是最便宜的套餐也是15-20刀/年，所以我还是选择了搬瓦工。  

- 64M内存 / 1.5G SSD硬盘/ G口 100G流量 / 年付3.99美元  
[http://bandwagonhost.com/aff.php?aff=316&pid=19](http://bandwagonhost.com/aff.php?aff=316&pid=19)  
- 96M内存 / 2.0G SSD硬盘/ G口 200G流量 / 年付4.99美元  
[http://bandwagonhost.com/aff.php?aff=316&pid=20](http://bandwagonhost.com/aff.php?aff=316&pid=20)  
- 128M内存 / 3G SSD硬盘/ G口 300G流量 / 年付5.99美元  
[http://bandwagonhost.com/aff.php?aff=316&pid=21](http://bandwagonhost.com/aff.php?aff=316&pid=21)  

我选择了第三个，平均一个月也就3块rmb，但是在购买的时候折腾了好久。显示注册paypal，结果不小心注册成果paypal贝宝，然后付不了款，浪费我一个邮箱，于是只能用另一个邮箱注册了paypal国际账户，这个可以用银联支付，所以付完款之后机子就很快就分配好了。这个也算是自己的第一次海淘吧，虽然之前应ebay的同学之邀，注册了一个paypal账户，但是都没用过，然后连正好都忘记了= =   

主机下来之后，来回重装了好几个系统来尝试搭openvpn，但都是连不上。最后试了 shadowsocks ，手机成功连上了。  

### 安装配置 shadowsocks  

v2ex上也有好多人用shadowsocks，遇到的问题也基本都可以再上面找到。  
我最后安装的系统是 centos 6 x86，然后跟着教程一步步弄，教程完全按照shadowsocks的github安装指南操作：  
[Shadowsocks-使用说明](https://github.com/clowwindy/shadowsocks/wiki/Shadowsocks-使用说明)  
然后为了让其可以再后台运行，用 Supervisor 运行 Shadowsocks，参考这个教程：  
[用-Supervisor-运行-Shadowsocks](https://github.com/clowwindy/shadowsocks/wiki/用-Supervisor-运行-Shadowsocks)  

- 安卓手机上安装 shadowsocks（影梭），填一下配置信息，搞定！  
- Chrome插件 Switchysharp 的设置：[Switchysharp 配置](http://switchysharp.com/setting.html)，直接下载 `.bak` 文件，然后按照教程配置。
- Ubuntu 下全局代理的设置（其实也并非全局），通过使用 [proxychains](http://proxychains.sourceforge.net/)，具体配置方法：[Using Shadowsocks with Command Line Tools](https://github.com/clowwindy/shadowsocks/wiki/Using-Shadowsocks-with-Command-Line-Tools)  

### 还有待解决的问题
- 我也是第一次使用vps，很多东西都还不太清楚，比如之前整openvpn为什么一直连不上，后面要好好研究一下。  
- 还有我在公司的 win7 下用 putty ssh连到 vps竟然连不上。用它管理界面上的那个 shell 简直太恶心了，之后一定要尝试连一下。