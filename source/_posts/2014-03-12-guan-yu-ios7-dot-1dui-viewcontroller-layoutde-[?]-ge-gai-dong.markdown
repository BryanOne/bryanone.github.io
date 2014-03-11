---
layout: post
title: "关于iOS7.1对Viewcontroller layout的一个改动"
date: 2014-03-12 01:33:33 +0800
comments: true
categories: 
---

前言
=======

今天iOS7.1正式发布，更新完后突然发现我们的应用基本所有的页面都出现了UI的错位，立即着手寻找bug

问题点
---
寻找问题的过程这里不进行阐述了，直接通报结果，iOS7.1在页面布局中增加了一个逻辑，如果navigationBar的背景是不透明的，那么所有这个导航栏对应的UIViewController的View origin-X 会变成64，

如果导航栏背景有透明，那么还是全屏布局！

**吐槽：这样的改动没有出现在apple的API diff中！也没有出现在release note中！这是在坑爹！**