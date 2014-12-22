title: 最简单的jquery页内锚点平滑跳转代码
date: 2014-12-18 21:27:32
tags: [web, jquery]
---

看到一些网站的页内跳转做了平滑滚动的处理，觉得不错，搜了一下实现方法，发现这篇文章： [最简单的jquery页内锚点平滑跳转代码](http://www.solagirl.net/jquery-jump-through-anchor.html),转过来记一下。  

    $("html,body").animate({scrollTop: $("#elementid").offset().top}, 1000);

自己再实际写的时候，因为 点击跳转链接的时候，跳转链接上使用了 `href="#elementid"`，这个再chrome会有页面跳动的现象，然后才平滑滚动到锚点处。这个以前也遇到过，把 href 去掉用其他属性替代就好了。    

    <ul class="nav navbar-nav">
      <li class="active"><a target="#page1" class="">page1</a></li>
      <li><a target="#page2" class="">page2</a></li>
      <li><a target="#page3" class="">page3</a></li>
    </ul>

    $('.navbar-nav li a').click(function(event) {
      switch ($(this).attr('target')) {
        case '#page1': $("body").animate({scrollTop: $("#page1").offset().top}, 700); break;
        case '#page2': $("body").animate({scrollTop: $("#page2").offset().top}, 700); break;
        case '#page3': $("body").animate({scrollTop: $("#page3").offset().top}, 700); break;
      }
    });

关于 a 元素设置 href 属性后进行页内跳转回出现跳动的现象，[segmentfault上有个回答](http://segmentfault.com/q/1010000000339082)很详细，下面直接贴原回答吧：  

***

修正一个说法上的bug吧。对于IE6来说，点击后gif暂停bug仅仅发生在“javascript:伪协议未加分号”的情形下。
我再来提供一个视角吧。

给`<a>`标签增加href属性，就意味着以下事情：

:link选择器可以选择到它
这个a标签可以获得焦点（可以通过`tab`按键访问到）
在浏览器的默认样式表中，有href属性的`<a>`标签才有`cursor:pointer`的效果（尤其是在低版本的IE上）。  

绑定了onclick事件的`<a>`标签，尤其是它的作用是ajax请求时，基本上我们就用不上这个标签的默认行为，也连接不到的实际页面，一般而言也会在CSS里给予了这个元素的cursor等样式。这时候还要加上href属性，是为了：

- 让`<a>`够响应键盘事件并获得焦点（从而屏幕阅读器能够读出背后的内容，增强可访问性）
- 优雅降级，在网络连接很差，还没有加载到CSS的时候，<a>依然有手型与正常的link样式。  

给`<a>`标签以href属性，并不连接到实际的页面的方案有：

    <a href="#"></a>
    <a href="#nogo"></a>
    <a href="##"></a>
    <a href="###"></a>
    <a href="javascript:void(0);"></a>
    <a href="javascript:void(0)"></a>
    <a href="javascript:;"></a>
    <a href="javascript:"></a>
他们的体验有细微的差别。

- 1，点击这个链接后，会让页面跳到头部，window.location.href末尾增加#（若window.location.href末尾没有#），除非在js里面捕获onclick事件并阻止默认事件。
- 2有了初步的语义。但是，如果页面里面有id为nogo的元素，点击这个链接后，锚点机制会作用，页面贴齐这个元素上缘。更详细的，详见张鑫旭的《[URL锚点HTML定位技术机制、应用与问题](http://www.zhangxinxu.com/wordpress/?p=3591)》
- 3在chrome中不再默认跳转到页面头部，4在IE11中不再跳转到页面头部。见下方测试。
- 5~8作用相同，但使用了javascript伪协议。在IE6下面，未加分号的方案6和方案8被点击后，IE6会使得页面中的gif暂停，并且触发onbeforeunload事件(详情参考[这里](http://www.w3help.org/zh-cn/causes/BX2047))，IE6认作这个页面有了重定向，并abort之后所有的请求（参考[这里](http://blog.163.com/dingpeng_2002/blog/static/180746462010913530706/)）。所以假如你在此之后替换了一个<img>的src，IE6完全不会完成这个新的请求。
我更倾向于使用方案4。

至于语义上LZ这种`<a href="javascript:void(0)">`使用方式，这个贴里已经有了足够详细的回答。我再补充一点，这种情形依然可以做到支持无障碍应用，方法请参考《[WAI-ARIA无障碍网页应用属性](http://www.zhangxinxu.com/wordpress/?p=2277)》。

更新，我做了如下的测试：

        <p>
            <a href="#">#</a>
        </p>
        <p>
            <a href="##">##</a>
        </p>
        <p>
            <a href="###">###</a>
        </p>
        <p>
            <a href="####">####</a>
        </p>
        <p>
            <a href="#####">#####</a>
        </p>
        <script type="text/javascript">
            var n = 0 ;
            window.onhashchange = function(){
                alert(++n) ;
            }
        </script>

- 在IE11中，点击###、####和#####时，页面不再跳转到头部
- 在chrome中，点击##、###、####和#####时，页面不再跳转到头部。
- 但是在IE11和chrome中，点击所有的`<a>`都会造成地址栏的修改，并触发hashchange事件。  
所以之前说的“###不会造成地址栏的改变”是错误的。

没有大规模测试其他的浏览器，这里做初步猜想：###的意义在于，这是字符数最少的，在所有的浏览器中不会导致跳转到页面头部的锚点。