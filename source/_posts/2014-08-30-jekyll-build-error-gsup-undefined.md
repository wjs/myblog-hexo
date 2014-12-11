---
layout: post
title: jekyll中gsub未定义的错误
categories: [jekyll]
tags: [jekyll]
---

刚重装Xubunt，配置了 jekyll 环境之后，第一次执行 `jekyll serve` 编译 竟然报下面这个错：
    
    Liquid Exception: undefined method `gsub' for nil:NilClass in feed/index.html
    error: undefined method `gsub' for nil:NilClass. Use --trace to view backtrace
google 了一下发现这篇：  
[jekyll中gsub未定义的错误](http://hi.barretlee.com/2014/04/26/gsup-error-in-atom-file/)  
按照他的方法，把页面中用到 \{\{ ... }} 的地方都用 \\{\\{ ... }} 代替了，可以build通过，可是之后我把改动的地方改回来，发现好像也可以 build 了，好奇怪，不知道为什么