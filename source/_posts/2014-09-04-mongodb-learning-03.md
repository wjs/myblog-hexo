---
layout: post
title: Mongodb学习笔记（三）：查询
categories: [mongodb]
tags: [mongodb]
---

第四章重点讲查询，好多，记着都混乱了，常用的还是得记一记。  

4.1  

- find，无条件是默认全部返回
- 查询条件也是个文档，多个条件逗号连接表示 `and`
- 返回结果 指定只显示某些键，或者剔除某些键
- 查询条件的值必须是常量

4.2  

- $lt, $lte, $gt, $gte, $ne
- $in, $or
- 使用 and 时，匹配结果最少的条件放在前； 使用 or 时，匹配结果多的放在前
- $not, $mod

4.3  

- 对 null 才查询，$exists
- 正则表达式
- 查询数组
	+ 默认精确匹配整个数组
	+ $all，顺序无关
	+ key.index 数组指定位置的元素
	+ $size
	+ $slice，返回前10，后10，偏移量
	+ 查询内嵌文档

4.4   

- $where

4.5  
- cursor
- next(), hasNext()
- limit, skip, sort
- 避免用 skip 略过大量结果
- $maxscan: integer, $min: document, $max: document, $hint: documemt, $explain: boolean, $snapshot: boolean
- 获取一致结果。取前100个文档，操作后放回去，文档体积增加，预留空间不足，则需要移至集合末尾；再往后面取文档会导致重复取。用 $snapshot 可以解决这个问题。