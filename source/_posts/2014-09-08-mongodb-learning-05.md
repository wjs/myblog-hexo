---
layout: post
title: Mongodb学习笔记（五）：聚合函数
categories: [mongodb]
tags: [mongodb]
---

- count
- distinct， db.runCommand({"distinct": "people", "key": "age"})
- group，例子：每天有多条股票的记录，每个记录有一个时间戳，现在要取出每一天最后的一条记录。用 group 对天分组，然后再取出每组中包含最新时间戳的记录。  

	db.runCommand({"group": {
		"ns": "stocks",
		"key": "day",
		"initial": {"time": 0},
		"$reduce": function (doc, prev) {
			if (doc.time > prev.time) {
				prev.price = doc.price;
				prev.time = doc.time;
			}
		}
	}})

- group 还有好多参数， condition, count, retval, keys, ok， finalizer 等
- 完成器 finalizer，用来精简返回结果。
- 将函数作为键使用， $keyf 
- MapReduce，好难没看懂。。。。