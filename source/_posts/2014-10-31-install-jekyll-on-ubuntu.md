---
layout: post
title: Ubuntu 14.04搭建jekyll博客环境
categories: [jekyll]
tags: [jekyll, ruby, ubuntu]
---

重装了系统，又要重新搭jekyll环境，这里还是记一下。  

ubuntu 14.04 默认不安装 ruby 的，所以先安装ruby，顺便把 rake 一起安装：  

	sudo apt-get install ruby ruby-dev rake

安装 jekyll 时候遇到了问题，默认的 gem 源非常慢，导致安装失败，参考了这篇博客解决了：[ rubygem 国内镜像 解决gem install rails 连接超时的问题](http://blog.csdn.net/dazhi_100/article/details/38777323)  

	gem sources --remove https://rubygems.org/
	gem sources -a https://ruby.taobao.org/
	gem sources -l

确认源只有 ruby.taobao.org ，多出的都删掉。然后再安装 jekyll 和 rdiscount    
	
	sudo gem install jekyll
	sudo gem install rdiscount

gem insall 可以加 -V 来看安装过程，不加的话会反应很慢，等久一点久好了。  


#### 2014-11-19 更新
最近在没有 nodejs 环境的 ubuntu 按照上面的方法搭建 jekyll，结果运行的时候出现 `Could not find a JavaScript runtime.` 的错误。google了一下说是因为 jekyll 里面加了 CoffeeScript 等一些东西，所以需要 node环境。于是安装了 nodejs，我习惯用 nvm 来安装，结果 jekyll 还是报错，还是得运行 `apt-get install nodejs` 才能解决。应该是 nvm 方法安装 nodejs 时缺少了很多东西吧。

### jekyll 使用教程
可以去[jekyll的官网](http://jekyllrb.com/docs/home/)看文档，这里推荐一下[掌心的Jekyll系列博客](http://www.zhanxin.info/jekyll/)