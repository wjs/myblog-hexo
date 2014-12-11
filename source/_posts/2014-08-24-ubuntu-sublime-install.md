---
layout: post
title: Ubuntu安装Sublime Text 3以及中文输入支持
categories: [ubuntu]
tags: [ubuntu, sublime]
---

编辑器什么的，用得顺手的才是王道，vim之类的会用就行了，平时还是Sublime为主。废话不多说，安装过程很简单，为了省事，ubuntu下我直接使用ppa安装；而中文输入法的处理，则参照网上别人的教程：
[http://www.360doc.com/content/14/0329/08/13087748_364608018.shtml](http://www.360doc.com/content/14/0329/08/13087748_364608018.shtml)


### 安装sublime text 3
	sudo add-apt-repository ppa:webupd8team/sublime-text-3
	sudo apt-get update
	sudo apt-get install sublime-text-installer

2014-08-30更新：
sublime text 3 正式版昨天发布了，官网上直接有 deb 包，可以去官网直接下载安装。

### 安装中文输入法
直接到官网下载linux搜狗拼音输入法
[http://pinyin.sogou.com/linux/](http://pinyin.sogou.com/linux/)


### 配置sublime text 3以支持中文输入法

1.保存一下代码到文件sublime-imfix.c

	/*
	 * sublime-imfix.c
	 * Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
	 * By Cjacker Huang <jianzhong.huang at i-soft.com.cn> *
	 *
	 * gcc -shared -o libsublime-imfix.so sublime_imfix.c  `pkg-config --libs --cflags gtk+-2.0` -fPIC
	 * LD_PRELOAD=./libsublime-imfix.so sublime_text
	 */
	#include <gtk/gtk.h>
	#include <gdk/gdkx.h>

	typedef GdkSegment GdkRegionBox;

	struct _GdkRegion
	{
	    long size;
	    long numRects;
	    GdkRegionBox *rects;
	    GdkRegionBox extents;
	};

	GtkIMContext *local_context;

	void
	gdk_region_get_clipbox (const GdkRegion *region,
	                        GdkRectangle    *rectangle)
	{
	    g_return_if_fail (region != NULL);
	    g_return_if_fail (rectangle != NULL);

	    rectangle->x = region->extents.x1;
	    rectangle->y = region->extents.y1;
	    rectangle->width = region->extents.x2 - region->extents.x1;
	    rectangle->height = region->extents.y2 - region->extents.y1;
	    GdkRectangle rect;
	    rect.x = rectangle->x;
	    rect.y = rectangle->y;
	    rect.width = 0;
	    rect.height = rectangle->height;

	    //The caret width is 2;
	    //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
	    if (rectangle->width == 2 && GTK_IS_IM_CONTEXT(local_context)) {
	        gtk_im_context_set_cursor_location(local_context, rectangle);
	    }
	}

	//this is needed, for example, if you input something in file dialog and return back the edit area
	//context will lost, so here we set it again.

	static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
	{
	    XEvent *xev = (XEvent *)xevent;

	    if (xev->type == KeyRelease && GTK_IS_IM_CONTEXT(im_context)) {
	        GdkWindow *win = g_object_get_data(G_OBJECT(im_context), "window");

	        if (GDK_IS_WINDOW(win)) {
	            gtk_im_context_set_client_window(im_context, win);
	        }
	    }

	    return GDK_FILTER_CONTINUE;
	}

	void gtk_im_context_set_client_window (GtkIMContext *context,
	                                       GdkWindow    *window)
	{
	    GtkIMContextClass *klass;
	    g_return_if_fail (GTK_IS_IM_CONTEXT (context));
	    klass = GTK_IM_CONTEXT_GET_CLASS (context);

	    if (klass->set_client_window) {
	        klass->set_client_window (context, window);
	    }

	    if (!GDK_IS_WINDOW (window)) {
	        return;
	    }

	    g_object_set_data(G_OBJECT(context), "window", window);
	    int width = gdk_window_get_width(window);
	    int height = gdk_window_get_height(window);

	    if (width != 0 && height != 0) {
	        gtk_im_context_focus_in(context);
	        local_context = context;
	    }

	    gdk_window_add_filter (window, event_filter, context);
	}

2.安装C/C++编译环境和gtk libgtk2.0-dev

	sudo apt-get install build-essential
	sudo apt-get install libgtk2.0-dev

3.编译成共享库

	gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC

4.测试运行

	LD_PRELOAD=./libsublime-imfix.so subl

5.copy共享库到 /opt/sublime_text 目录下

	sudo cp libsublime-imfix.so /opt/sublime_text/

6.修改 /usr/bin/subl

	sudo vim /usr/bin/subl
在第一行加入：

	export LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so

7.修改sublime-text.desktop

	sudo vim /usr/share/applications/sublime_text.desktop
把原本通过 /opt/sublime_text 执行的地方换成通过 subl 来执行。

	[Desktop Entry]
	Version=1.0
	Type=Application
	Name=Sublime Text
	GenericName=Text Editor
	Comment=Sophisticated text editor for code, markup and prose
	Exec=/usr/bin/subl %F
	Terminal=false
	MimeType=text/plain;
	Icon=sublime-text
	Categories=TextEditor;Development;Utility;
	StartupNotify=true
	Actions=Window;Document;

	X-Desktop-File-Install-Version=0.22

	[Desktop Action Window]
	Name=New Window
	Exec=/usr/bin/subl -n
	OnlyShowIn=Unity;

	[Desktop Action Document]
	Name=New File
	Exec=/usr/bin/subl --command new_file
	OnlyShowIn=Unity;


配置过程根据自己机子的安装环境而定，一般没多大问题，有问题再google

### Sublime text 3 package control
懒得每次装都要搜一下那段代码，现在贴到这里，找起来方便。  

	import urllib.request,os,hashlib; h = '7183a2d3e96f11eeadd761d777e62404' + 'e330c659d4bb41d3bdf022e94cab3cd0'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)  


2014-10-29 更新  
上面安装 package control 的代码可能随着版本不同而不同，因此推荐到下面这个网站那里粘贴安装的代码：[https://sublime.wbond.net/installation](https://sublime.wbond.net/installation)


---
### 2014-10-27 更新

sublime text 3 正式版已经推出，可以直接到 [sublime官网](http://www.sublimetext.com/) 下载 deb包 直接安装，省掉好多事。