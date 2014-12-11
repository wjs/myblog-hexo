---
layout: post
title: Jsonp小例子
categories: [js]
tags: [jsonp, js]
---

早就听说过 jsonp ，今天有空就研究了一下。在博客园上发现一篇不错的文章：[jsonp详解](http://www.cnblogs.com/lemontea/archive/2012/12/11/2812268.html)， 关于 jsonp 博主写的比较详细，但是实现的小例子讲的不是很清楚，于是我有找了另一篇博客： [一次关于JSONP的小实验与总结](http://www.cnblogs.com/vimsk/archive/2013/01/29/2877888.html)， 这个博客里实现的例子比较清楚，于是我照这上面的介绍写了个demo。这里就记录一下写这个 demo 的过程，关于 jsonp 的详细介绍就直接去看上面那两篇博客吧。要下载我的这个 demo 的话可以 [点这里下载](https://github.com/weijinshi/JsonpDemo)  

看第一篇博客的时候，以为只在一头就能搞定。看了第二篇才知道，原来要在另一个域的后台方法也要做相应处理才能够实现。