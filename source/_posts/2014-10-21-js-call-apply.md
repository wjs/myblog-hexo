---
layout: post
title: js中call与apply的区别
categories: [js]
tags: [js]
---

昨天面试被问到了这个问题，虽说自己白天的时候临时抱佛脚看到了，但是根本就没搞懂，所以被问道的时候还是答不上来。今晚看了几篇文章之后，算是比较清楚了。其中知乎上的这个回答最直观了：[如何理解和熟练运用js中的call及apply？](http://www.zhihu.com/question/20289071), 还有这一篇讲得也很详细：[关于javascript中apply()和call()方法的区别](http://www.cnblogs.com/fighting_cp/archive/2010/09/20/1831844.html)。这里主要参考这两篇的观点，稍微整理一下。   

首先要call和apply存在的原因：在js oop中，我们经常定义

	function Cat() {}
	Cat.prototype = {
		food: 'fish',
		say: function() {
			alert('I love ' + this.food);
		}
	}

	var blackCat = new Cat();
	blackCat.say();

但是如果我们有一个对象 `whiteDog = {food: 'bone'}`,我们不想对它重新定义say方法，那么我们可以通过call或apply来使用blackCat的say方法：`blackCat.say.call(whiteDog)`  
所以可以看出，call和apply是为了动态改变this而出现的。当一个object没有某个方法，而其他obj有，我们可以借助call或apply来使用其他对象的方法。  

总结一下，区分call和apply就一句话：

	foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments)==this.foo(arg1, arg2, arg3)

call和apply的作用也是一句话：

	call，apply 作用都是 借别人的方法来调用，就像调用自己的一样