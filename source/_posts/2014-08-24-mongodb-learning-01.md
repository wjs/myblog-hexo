---
layout: post
title: Mongodb学习笔记（一）：基本概念
categories: [mongodb]
tags: [mongodb]
---

老早就想系统地学一下mongodb，结果一直拖到现在，终于开始看《MongoDB权威指南中文版》，今天才看了第二章，稍微记一下。


### 几个重要的概念

- 文档 （相当于row），类似json的键值对，区分类型和大小写（不一样的类型或大小写算不同的文档），不能有重复键
- 集合 （相当于没有schema的表），命名规则（4个不能）
- 子集合 （命名空间的概念）
- 数据库 （命名规则）


### 使用mongodb shell

由于使用ubuntu安装的mongodb，安装好之后mongodb的服务默认是启动了的（手动安装的得执行 `./mongod` 来启动service，查看服务是否开启： [localhost:28017](localhost:28017)），打开mongodb shell直接敲 `mongo` 即可。

mongodb shell是一个JavaScript shell，由于js中只有64位浮点数，因此在用mongodb shell处理数字相关的文档时候要注意。
一般操作（CRUD）

- db.blog.insert(doc)
- db.blog.find() / db.blog.findOne()
- db.blog.update({title : 'aaa'}, newDoc)
- db.blog.remove({title : 'aaa'})

忘记命令可以使用 `help` 来查看


### 数据类型

mongodb的文档类似json，但是json仅包含6中数据类型(null, bool, number, string, array, object)，没有日期类型，只有一种数字类型，无法区分整型和浮点数。
mongodb支持的数据结构：

- null
- bool
- 32 int
- 64 int
- double
- string
- 符号
- ObjectId
- Date
- 正则表达式
- 代码（function）
- 二进制数据
- MAX
- MIN
- array
- 内嵌文档

重点看： 数字，日期，数组，内嵌文档，ObjectId  


***
2014-09-06 update：
ubuntu下的安装，直接使用压缩包的方式，解压到 /opt/mongodb，然后新建 /data/db 并赋予读写权限，最后在 ～.bashrc 里面添加 path。