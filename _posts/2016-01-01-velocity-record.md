---
layout: post
title:  "velocity语法记录"
date:   2016-01-01 21:25:09
categories: velocity
excerpt:  velocity语法记录
---

* content
{:toc}

##	指令:

`#foreach`指令-用于循环:
	
	#foreach($list in $lists)

	#end

`$lists`可以是`List`、`Vector`、`HashTable`、数组等；其中在循环中有一个变量$velocityCount作为循环计数使用，该变量从1开始。

`#if`指令-用户判断:

	#if($value)##判断`value`值不为空

	#end

	#if($value && $value > 0)

	#elseif($value = 0)

	#else

	#end

`#if`的逻辑判断和一般的java判断没什么区别

`#set`指令-用户赋值:
	
	#set($value = `value`)


`#parse`指令-引入另外一个模板:

	#parse(demo.vm)

`#include`指令-引入文件(该页面只能我静态的):

	#include(soruce.vm)

`#stop`指令: