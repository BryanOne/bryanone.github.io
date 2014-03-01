---
layout: post
title: "解决Octopress选装Greyshade主题Disqus失效的问题--深入了解jekyll模板"
date: 2014-03-01 23:03:05 +0800
comments: true
categories:
- web
- Octopress
- Greyshade
---

## 问题描述

在寻找漂亮的Octopress主题的时候，发现了一个不错的theme - [Greyshade](https://github.com/shashankmehta/greyshade "Github地址")，按照Github页面上的提示进行安装：

	$ git clone git@github.com:shashankmehta/greyshade.git .themes/greyshade
	$ echo "\$greyshade: color;" >> sass/custom/_colors.scss //Substitue 'color' with your highlight color
	$ rake "install[greyshade]"
	$ rake generate

preview了下，发现Disqus的comment功能不见了，下面开始解决问题。

## Jekyll模板结构

下面的内容是我对Jekyll结构的理解，当我们新建一个模板，下面主要有下面几个文件和目录：

	_config.yml

全局的配置文件，可以控制一些plugin的开关，比如Disqus，github，google+等

	sass/

里面是一堆的scss文件，负责页面UI区域规划，显示的颜色，文字排版等

	source/

出去sass干的，剩下的比如页面内容的组织，逻辑等就是由这个控制

	source/_posts

其中这个文件夹存放的就是blog的source，blog的内容在这里面用编辑器编辑即可。

## 解决Disqus无法工作的问题

首先查看了问题页面的源码，负责comment模块的代码如下

	<section id="comment">
	<h1 class="title">Comments</h1>
	<div id="disqus_thread" aria-live="polite"><noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
	</div>
	</section>
	
这里没有执行任何的逻辑调用，查看了下这段代码位于/_includes/post/disqus_thread.html中，而真正的需要的代码位于/_includes/disqus.html中，这样问题就看disqus原来在哪里调用即可
查看完，发现原来的classic theme是把disqus调用放在after_footer.html中，这个在新主题内没有被任何文件调用，查看文件修改记录，在_layouts/default.html中line 19加入代码

	{% include after_footer.html %}

问题解决

PS：解决这个问题也让自己进一步熟悉了页面组织结构，后面有时间可以尝试调出自己风格的页面出来