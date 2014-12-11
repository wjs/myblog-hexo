title: jekyll-to-hexo
date: 2014-12-11 21:30:50
tags:
---

记一下把博客从jekyll迁移到hexo中遇到的坑。最好仔细看[hexo的官方文档](http://hexo.io/docs/)。

1. 迁移之前先备份之前github pages的repo。只要备份就好了，不要把repo都删掉，我就很2b地删掉了原来的repo，然后之前的contributions都没了，都没了%>_<%。嘛，虽说我之前的提交大部分也都是修改样式，再说github上的repo主要还是看质量，提交数目也说明不了什么。

2. hexo跟jekyll不一样，不是把这个博客的代码放到github page的repo中，而是可以随便放其他，比如dropbox，我现在就是在github上又建了myblog-hexo的repo，专门存放博客的源码。而部署到github pages则是用hexo的命令: `hexo deploy`, 即可。部署之前首先线配置 `_config.yml` 里面的：

    '''
    url: http://weijinshi.github.io
    deploy:
      type: github
      repo: https://github.com/weijinshi/weijinshi.github.com.git

