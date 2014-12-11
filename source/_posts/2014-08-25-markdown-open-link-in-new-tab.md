---
layout: post
title: Markdown在新标签页中打开连接
categories: [markdown]
tags: [markdown]
---

刚开始使用markdown写博客，貌似语法中添加链接的时候最多也就添加title，没有方法设置在新标签页中打开链接，因此网上搜了一下，参考了这篇文章：  
[在Octopress中为markdown的超链接加上target="_blank"](http://www.blogjava.net/lishunli/archive/2013/01/20/394478.html)

第一种方法：  
因为markdown支持html语法，一次可以直接使用  
 `<a href="http://blogjava.net/lishunli" target="_blank">my blog</a>`  
来达到要求。

第二种方法：  
使用js来给`<a>`标签加上`target="_blank"`。我的具体做法是在`_layout`里面的`_post.html`模板页中加入下面这段js：

	function addBlankTargetForLinks () {
	  $('a[href^="http"]').each(function(){
	    $(this).attr('target', '_blank');
	  });
	}

	$(document).bind('DOMNodeInserted', function(event) {
	  addBlankTargetForLinks();
	});

这样post页面中的链接都会在新标签也中打开了。