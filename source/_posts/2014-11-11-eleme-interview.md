---
layout: post
title: 前端面试经历
categories: [web]
tags: [web, interview]
---

今天去面了一个公司的前端开发职位，自己能力确实达不到要求吧，直接跪了。面试官人很好，基本答不上来的都会告诉我答案。稍微记一下被问到的问题。好多都忘记了，被问懵了。。。  

- 你当前工作都做些什么？
  - 我没回答对重点，说了好多，但自己做什么却没说清楚，结果被打断了问我做了哪些。所以要抓重点，面试官想了解你做了什么，而不是你在的公司做什么。

- jquery事件委托怎么写？
  - $('parent').delegate('target', 'click', function() {})
  - $.proxy 的使用
  - on 的使用

- 讲讲node的特性？然后提到了异步，然后异步嵌套过多怎么解决？延伸到ajax嵌套，要怎么解决？
  - [eventproxy](https://github.com/JacksonTian/eventproxy)， 参考：[一个前端工程师眼里的NodeJS](http://www.infoq.com/cn/articles/nodejs-in-front-end-engineer-view)

- angular好在哪里？或者讲特性。backbone出来很久了，用过么，跟angular比较一下

- single-page application 有了解么？还有h5有了解么，讲讲

- Grunt 构建，gulp用过么？一个前端工程，项目结构一般是怎样的？

- 不同子页面，引入css文件不同，但是子页面不包含 head 标签，怎样保证不同子页面引入的 css 文件不冲突？