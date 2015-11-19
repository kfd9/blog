---
layout: post
title:  "EXTJS获取父子、兄弟容器的办法"
date:   2015-11-17 21:06:05
categories: jekyll
excerpt:  EXTJS获取父子、兄弟容器的办法
---

* content
{:toc}

# 根据当前对象获取其他对象

* 1

当前对象的父对象(上级对象):

	this.ownerCt;
	
* 2

当前对象的下一个相邻的对象:

	
	this.nextSibling();
	
* 3

当前对象的上一个相邻的对象:


	this.previousSibling();
	
* 4 

当前容器中的第一个子对象:

	
	this.get(0);
	this.items.first();
	
* 5 

当前容器中的最后一个子对象:

	
	this.items.last();
	
* 6 

查找当前对象的所有上级匹配的容器:

	
	this.findParentByType(String xtype);
	
* 7 

查找当前对象的所有下级匹配的组件:

	
	this.findByType(String xtype);
	
---
	
# 直接获取对象

##  `get` 方法:

>*  `get` 方法中只有一个参数，这个参数是混合参数，可以是 `DOM` 节点的 `id` 、也可以是一个 `Element` 、或者是一个 `DOM` 节点对象等。 
>*  `•get` 方法其实是 `Ext.Element.get` 的简写形式。	
	
##  `getDom` 方法:

>*  `getDom` 方法能够得到文档中的 `DOM` 节点，该方法中包含一个参数，该参数可以是 `DOM` 节点的 `id` 、 `DOM` 节点对象或 `DOM` 节点对应的 `Ext` 元素( `Element` )等。 
>*  与 `getElementById` 是一个效果

##  `getCmp`方法:

>*  `getCmp` 方法用来获得一个 `Ext` 组件，也就是一个已经在页面中初始化了的 `Component` 或其子类的对象， `getCmp` 方法中只有一个参数，也就是组件的 `id` 。
>*  `getCmp` 方法其实是 `Ext.ComponentMgr.get` 方法的简写形式。

---
