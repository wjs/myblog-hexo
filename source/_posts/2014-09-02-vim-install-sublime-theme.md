---
layout: post
title: Vim 设置使用 sublime 配色方案
categories: [vim]
tags: [vim]
---

Ubuntu 下使用 vim 来编辑各种配置文件还是很方便的，但是自带的配色感觉不是很好，于是想换个好点的配色，google 之后发现这边博客：  
[vim配置+插件](http://calefy.org/2012/10/30/the-config-of-my-vim.html)  
博主推荐的 [vim-monokai](https://github.com/sickill/vim-monokai) 配色确实非常不错，推荐的几款插件也很好，不过对我来说主编辑器不是vim，因此没装 = =  
配置的具体步骤：  

1.打开终端 `vim .vimrc`，粘贴下面的配置代码：  

	set encoding=utf-8
	set fileencoding=utf-8
	set fileencodings=ucs-bom,utf-8,chinese,cp936
	set guifont=Consolas:h15
	set number
	set tabstop=4
	set autochdir

	set shiftwidth=4
	set foldmethod=manual

	colorscheme monokai
	set nocompatible
	set nobackup

2.到 github 上下载 [vim-monokai](https://github.com/sickill/vim-monokai)，把 `.vim` 后缀的配色文件放到 `～/.vim/colors/`，保存退出即可。