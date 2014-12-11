---
layout: post
title: Memcache 学习笔记（一）：基本概念
categories: [memcache]
tags: [memcache]
---

这两天打算要看一下 memcached，网上搜了一下好多博客其实都是转载或者引用了《memcached全面剖析》里面的内容，于是我上皮皮书屋找了一下还真有这本书，这本书是由 charlee 翻译的 mixi两位工程师的文章，博主不仅翻译到自己博客中，还做成了非扫描版的pdf书籍分享出来，这种分享精神实在让人敬佩。  

《memcached全面剖析》这本书在讲 memcached 基本概念的部分还是非常容易理解的，虽然 ICS 这门课没学好，但是 cache 的概念还是有的，所以理解起来不费劲。不过到后面深入的部分就有点脑子不够用了，特别是第二章理解 memcached 的内存存储那部分，彻底暴露了 ICS 学得有多渣。同时，我在皮皮书屋上找到了另一本 memcached 相关的书《Using memcached: How to scale your website easily》，英文的，慢慢啃，发现这本书讲的比较细致，而且好理解，至少前面的是这样，后面的还没看 = =。

这篇的话我主要讲一些书中提到的概念性的东西，因为好多深入的概念我也没理解，所以还只能把这些基本的东西记一下。后面的 memcached 学习过程我打算通过学习例子之类的来慢慢理解。

### memcached 是什么

许多 web 应用都将数据保存到 RDBMS 中（虽然现在很多都直接用NoSQL），应用服务器从数据库中读取数据并在浏览器中显示。但随着数据量增大、访问集中，就回出现 RDBMS 负担过重，数据库相应恶化，网站延迟增大等。  

memcached 是高性能的分布式内存缓存服务器。一般的使用目的是：通过缓存数据库查询结果，减少数据库访问次数，以提高动态 web 应用的速度、提高可扩展性。  

memcached is a server that caches Name Value Pairs (NVPs) in
memory. The value in the NVP can be anything that fits in mem-
cached: rows of data, HTML fragments, binary objects.

同样是介绍 memcached 是什么，第一本书中没有提到 NVPs 这个词，着重讲了 memcached 可以缓解传统 web 应用程序中访问 RDBMS 的性能，第二本书则着重说读硬盘跟读内存的性能差别。其实都是一个道理。  

第二本书还讲了 memcached 不是什么  

首先，memcached 不是存储介质，不可以对里面的键值对做查询（只可以通过key取一个值），也不可以把内存里的东西转移到硬盘中。  
其次， memcached 不提供内置的安全机制，但可以通过其他方法实现。  
最后，memcached 部支持任何容错性以及高可用性的机制（fail-over/high-availability），如果一个 memcached server down机的话，里面的数据都会丢失。但因为它只是cache，所以原始数据不受影响。

### memcached 的特征

- 协议简单
- 基于 libevent 的事件处理
- 内置内存存储方式
- memcached 不互相通信的分布式

