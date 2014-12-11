title: jekyll-to-hexo
date: 2014-12-11 21:30:50
tags: [hexo, jekyll]
---

记一下把博客从jekyll迁移到hexo中遇到的坑。最好仔细看[hexo的官方文档](http://hexo.io/docs/)。

1. 迁移之前先备份之前github pages的repo。只要备份就好了，不要把repo都删掉，我就很2b地删掉了原来的repo，然后之前的contributions都没了，都没了%>_<%。嘛，虽说我之前的提交大部分也都是修改样式，再说github上的repo主要还是看质量，提交数目也说明不了什么。

2. hexo跟jekyll不一样，不是把这个博客的代码放到github page的repo中，而是可以随便放其他，比如dropbox，我现在就是在github上又建了myblog-hexo的repo，专门存放博客的源码。而部署到github pages则是用hexo的两条命令即可。部署之前先按照下面配置 `_config.yml` ，然后执行 `hexo g` 和 `hexo d` 进行部署。如果要放到blog的源码也要放到github pages的repo的话，可以参考这一篇文章：[使用github管理hexo本地文件](http://youthyblog.com/2014/06/28/使用github管理hexo本地文件)

    '''
    url: http://weijinshi.github.io
    deploy:
      type: github
      repo: https://github.com/weijinshi/weijinshi.github.com.git

3. 博客没主题一两天了才发现，不过也没人访问，哈哈 - -，主题的话，自己写一个，现在先用[pacman](https://github.com/A-limon/pacman)的，自己的主题弄好了再换上。

4. 常用命令：
    '''
    hexo g == hexo generate
    hexo d == hexo deploy
    hexo s == hexo server
    hexo n == hexo new

5. 每次deploy都需要重复输入密码的问题，可以按照这篇文章来设置ssh key，[使用hexo搭建blog之五：部署hexo到github](http://www.studio2013.com/2013/07/21/hexo-github-deploy/)