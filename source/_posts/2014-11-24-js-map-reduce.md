---
layout: post
title: js中的map和reduce方法
categories: [js]
tags: [js]
---

虽然老早就听说够 underscore，但是都没有用过也没有好好研究过，今天被问到了 map 和 reduce 这两个方法，然后就都不会了。。。 这两天得看看API文档， [underscore](http://underscorejs.org/) 和 [lodash](https://lodash.com/docs)   


简单说，map就是遍历 list 里面的每一个值，对每一个值进行相应操作，然后可以产生一个新的数组，返回这个数组。  

reduce则是给一个初始值，然后也是遍历list，把初始值跟list里面的每一个值做响应操作，比如累加，然后返回累加的结果；如果没有给初始值，则遍历时候第一个元素跳过操作，把第一个元素当做初始值，往下遍历执行操作，返回结果。  

网上看到一片文章自己用js 实现了这两个方法，也可以参考一下： [
JavaScript实现Map、Reduce和Filter](http://www.oschina.net/code/snippet_111708_16208)  


下面是这两个方法的官方文档解释：  

map  
`_.map(list, iteratee, [context])` Alias: collect   
Produces a new array of values by mapping each value in list through a transformation function (iteratee). If list is a JavaScript object, iteratee's arguments will be (value, key, list).

    _.map([1, 2, 3], function(num){ return num * 3; });
    => [3, 6, 9]
    _.map({one: 1, two: 2, three: 3}, function(num, key){ return num * 3; });
    => [3, 6, 9]

reduce  
`_.reduce(list, iteratee, [memo], [context])` Aliases: inject, foldl   
Also known as inject and foldl, reduce boils down a list of values into a single value. Memo is the initial state of the reduction, and each successive step of it should be returned by iteratee. The iteratee is passed four arguments: the memo, then the value and index (or key) of the iteration, and finally a reference to the entire list.

If no memo is passed to the initial invocation of reduce, the iteratee is not invoked on the first element of the list. The first element is instead passed as the memo in the invocation of the iteratee on the next element in the list.

    var sum = _.reduce([1, 2, 3], function(memo, num){ return memo + num; }, 0);
    => 6
   

