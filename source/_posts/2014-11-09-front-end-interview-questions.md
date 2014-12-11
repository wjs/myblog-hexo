---
layout: post
title: github上的前端面试题
categories: [web]
tags: [web, interview]
---

（事实证明，不是所有前端面试都会问基础而已，前沿的技术也多搞搞，至少要熟悉一种比较新的技术）github上有好多个关于前端面试的题目，这里稍微做一下。参考 [前端工作面试问题](https://github.com/darcyclarke/Front-end-Developer-Interview-Questions/tree/master/Translations/Chinese) 和 [2014年最新前端开发面试题（题目列表+答案 完整版）](https://github.com/markyun/My-blog/tree/master/Front-end-Developer-Questions/Questions-and-Answers)   

## 常见问题

- 请解释一下什么是“语义化的 HTML”。
  - [理解HTML语义化](http://www.cnblogs.com/freeyiyi1993/p/3615179.html)

- 你能描述一下渐进增强和优雅降级之间的不同吗?
  - [渐进增强与优雅降级是什么](http://www.cnblogs.com/yangjf/archive/2013/03/28/2986134.html)
  - [javascript 特性检测并非浏览器检测](http://www.jb51.net/article/21834.htm)

- 为什么利用多个域名来提供网站资源会更有效？
  - CDN缓存方便
  - 突破浏览器并发限制
  - cookieless, 节省带宽，尤其是上行带宽，一般比下行带宽要慢

- 请说出三种减少页面加载时间的方法。（加载时间指感知的时间或者实际加载时间）
  - 减少http请求，合并文件，合并图片
  - 压缩css，js，图片
  - CDN缓存静态资源

- Long-Polling, Websockets, SSE(Server-Sent Event) 之间有什么区别？
  - [Long-Polling, Websockets, SSE(Server-Sent Event), WebRTC 之间的区别](http://www.vipaq.com/Article/View/blog/419.html)



## HTML

- doctype（文档类型）的作用是什么？
  - 告知浏览器的解析引擎，用什么文档类型喝规范来解析这个文档。l

- 浏览器的严格模式喝混杂模式的区别？

- 使用 XHTML 的局限有哪些？如果页面使用 'application/xhtml+xml' 会有什么问题吗？
  - xhtml 要求严格，必须有 head body，标签必须都闭合。
  - 老浏览器不兼容

- data-属性的作用是什么？
  - 可以为标签提供自定义属性，这些自定义的属性可以通过 对象的dataset 属性获取，不支持该属性的浏览器可以使用 getAttribute 方法来获取。
  - 注意：data-之后的以连字符分割的多个单词组成的属性，获取的时候使用驼峰风格。如 <div data-comment-num="10"></div>，获取时候需要使用 div.dataset.commentNum

- 请描述一下 cookies，sessionStorage 和 localStorage 的区别？
  - cookie在浏览器和服务器间来回传递。 sessionStorage和localStorage不会
  - sessionStorage和localStorage的存储空间更大；
  - sessionStorage和localStorage有更多丰富易用的接口；
  - sessionStorage和localStorage各自独立的存储空间；
  - localStorage 长期存储数据，浏览器关闭后数据不丢失；sessionStorage 数据在浏览器关闭后自动删除

- 请描述一下 GET 和 POST 的区别?
  - [HTTP 方法：GET 对比 POST](http://www.w3school.com.cn/tags/html_ref_httpmethods.asp)



## CSS

- 描述下 “reset” CSS 文件的作用和使用它的好处。
  - 不同浏览器默认样式不一样，定义一个css reset可以使浏览器默认样式统一。
  - [normalize.css](http://necolas.github.io/normalize.css/3.0.2/normalize.css)


## JavaScript

- [关于Javascript模块化和命名空间管理](http://www.cnblogs.com/hongru/archive/2010/12/05/1897111.html)
- [关于JavaScript中apply与call的用法意义及区别(转)](http://www.cnblogs.com/treasurelife/archive/2008/03/05/1092251.html)
- [理解 JavaScript 中的 Function.prototype.bind](http://blog.jobbole.com/58032/)
