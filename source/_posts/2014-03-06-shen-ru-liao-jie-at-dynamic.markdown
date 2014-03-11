---
layout: post
title: "深入了解@dynamic"
date: 2014-03-06 00:24:42 +0800
comments: true
categories: OC
---

前言
=============
 最近在看一些牛x的开源库，看到了一个@dynamic用法，让自己深入的了解了下这个关键字，下面和大家分享一下
 
思考问题
------
 一个class的categroy能添加property么？
 
 这个问题可能不少人在面试的时候会遇到，这里我们先放下，分析完@dynamic后再来解答
 
@dynamic用来做什么的？
------
 **@dynamic**和**@synthesize**是在class implementation时告诉编译器如何处理对应的property：
 
 *@synthesize：会自动根据property的attribute生成对应的getter、setter，在class 的propertylist中加入这个property的信息，并且在class的 ivar list中加入了对应的成员变量，xcode4开始编译器会默认使用@synthesize对声明的property进行处理，并自动生成 _propertyName 这样的ivar
 	
 *@dynamic：和**@synthesize**完全相反，它告诉编译器不对这个property进行任何的操作，在IDE中我们可以正常对property进行访问，但是如果要在app运行时不会出问题，我们需要手动合成对应的getter和setter方法，可以是自己写，可以通过消息转发来动态实现
 	
说了这么多，来举个例子：
-------
 
 	@interface NSObject (dynamic)

	@property (nonatomic, strong) NSObject *object;

	@end
	
	static char propertyName;
	
	@implementation NSObject (dynamic)
	
	@dynamic object;
	
	- (void)setObject:(NSObject *)object {
		objc_setAssociatedObject(self, &propertyName, object, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
	}
	
	- (NSObject *)object {
		return objc_getAssociatedObject(self, &propertyName);
	}
	
	@end
 
 这样是不是我们刚才思考的问题的答案已经很了然，这里的例子是手动合成方法给分类添加伪属性，因为这样的属性并不能通过class的property list中获取。