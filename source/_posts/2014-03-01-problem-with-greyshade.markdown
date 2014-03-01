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