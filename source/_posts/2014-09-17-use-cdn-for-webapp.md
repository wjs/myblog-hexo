---
layout: post
title: CND加速页面加载
categories: [web]
tags: [web, CDN]
---

之前听朋友说过用加载 jquery 之类的可以用一些国内的 cdn ，今天在自己的 github pages 上试了一下，发现 jquery.min.js 的加载速度由 100+ ms 降到了 20-30ms，效果很明显。  
我用的是 新浪的 cdn 加速点：

    <script src="http://lib.sinaapp.com/js/jquery/1.10.2/jquery-1.10.2.min.js"></script>
    <script type="text/javascript">
      !window.jQuery && document.write('<script src="/js/jquery-1.10.2.min.js"><\/script>');
    </script>

当 cdn加速点的js文件加载不了的时候，再使用本地的js。  
下面是国内一些加速点:   

- [新浪CDN加速点](http://lib.sinaapp.com/)
- [bootstrap中文网开放CDN服务](http://open.bootcss.com/)