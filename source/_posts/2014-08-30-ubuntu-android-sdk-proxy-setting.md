---
layout: post
title: Xubuntu 设置 android sdk manager 的 shadowsocks 代理
categories: [android]
tags: [android, ubuntu]
---

  
由于在 android sdk manager 的 gui 界面中 Tools -> option 里面只能够设置 HTTP proxy，而 Shadowsocks 必须是 SOCKS5 的，因此不能在那里设置，首先想到了 shadowsocks 的 github wiki 上有方法说可以使用 proxychains 来从终端启动程序，这样程序就可以使用 shadowsocks 的代理，我自己试了一下，没成功，不知道为什么。  

于是想到了需要修改系统的全局代理，如果用的是 Ubunt 的话，在网络中有设置系统全局代理可以设置。但是我这次重装选则了 Xubuntu，没有 gui 设置全局代理的。google了好久发现 Xubuntu 下可是使用 tsocks 来设置 socks 代理，于是 `apt-get install` 安装了，然后配置了 `/etc/tsocks.conf` 文件，然后运行 `tsocks android`，发现好像还是不行，郁闷了好久，太晚了就先睡了，第二天重启之后再试试，竟然可以了 ><   

其实自己没注意看 Shadowsocks 的 github wiki，上面有介绍使用 polipo 把 Shadowsocks 的 socks 协议转换为 http 协议，地址在这里：  
[Convert Shadowsocks into an HTTP proxy](https://github.com/clowwindy/shadowsocks/wiki/Convert-Shadowsocks-into-an-HTTP-proxy)