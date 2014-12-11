---
layout: post
title: Mongodb学习笔记（二）：基本操作
categories: [mongodb]
tags: [mongodb]
---


常用的操作，书看起来很容易懂，但是估计一段时间不用肯定忘记，复习的时候，看到下面列的这些操作，要想起能够想起写法。想不起来翻书，书上的例子很好记。
> * 插入文档 （insert）
> * 批量插入，性能，大小限制， 原理
> * 删除文档，性能 （remove）（drop_collection）
> * 更新 （update）
> * 修改器，PHP注意转义问题 （$set）（$inc）
> * 数组修改器 （$push）（$addToSet）（$each）（$pop）（$pull）
> * 数组的定位修改器 （通过位置后者定位操作符$）
> * 修改器的性能  
> * upsert
> * save
> * 更新多个文档 （注意，默认是只更新匹配到的第一个文档）
> * findAndModify  
	+ db.runCommand(....)
	+ findAndModify： 字符串，集合名
	+ query： 文档，查询条件
	+ sort： 排序
	+ update： 修改器
	+ remove： bool，是否删除
	+ new： bool，返回更新前的文档还是更新后的文档
	+ update和remove有且只有一个；不能执行upsert操作，只能更新已有文档；耗时更久。
