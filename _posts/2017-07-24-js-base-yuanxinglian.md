---
layout: post
title:  "js基础知识-原型链"
date:   2017-07-24 23:25:09
categories: js
excerpt:  js基础知识-原型链
---

* content
{:toc}

# `js`基础知识-原型链

## `js`的原型链是什么
    
> 原型链是实现继承的主要方法。其基本思想是：利用原型让一个引用类型继承另一个应用类型的属性和方法。

### `_proto_`和`prototype`

> `js`通过使用`_proto_`和`prototype`来标示对象或函数的原型，其中`_proto_`作为对象的内置原型对象，`prototype`作为函数的内置原型对象。

> 一般来说`_proto_`是用来给对象使用，`prototype`给函数使用。

## 如何实现`js`的继承

### 方式1

> 使用`_proto_`来实现继承

```
var log = console.log;
var A = function(){
	this.printA = function(){
		log('this is A!');
	}
}
var B = function(){
	this.printB = function(){
		log('this is B!');
	}
	this.__proto__ = new A();// 指定原型来实现继承
}
var a = new A();
a.printA();//this is A!
var b = new B();
b.printB();//this is B!
b.printA();//this is A!
```

### 方式2

> 使用`prototype`来实现继承

```
var log = console.log;
var A = function(){
	this.printA = function(){
		log('this is A!');
	}
}
var B = function(){
	this.printB = function(){
		log('this is B!');
	}
}
B.prototype = new A();// 指定原型来实现继承
var a = new A();
a.printA();//this is A!
var b = new B();
b.printB();//this is B!
b.printA();//this is A!
```

### 方式3

> 使用call来实现继承，即用父对象替换当前对象，`call([thisObj[,arg1[, arg2[,   [,.argN]]]]]) `，当传入`this`对象时，还可以传入可变参数

```
var log = console.log;
var A = function(){
	this.printA = function(){
		log('this is A!');
	}
}
var B = function(){
	this.printB = function(){
		log('this is B!');
	}
	A.call(this);// 代表使用A的对象替换当前对象来实现继承
}
var a = new A();
a.printA();//this is A!
var b = new B();
b.printB();//this is B!
b.printA();//this is A!
```
### 方式4

> 使用call来实现继承，即用父对象替换当前对象，`apply([thisObj[,argArray]]) `，当传入`this`对象时，只能传入数组对象或者`arguments`

```
var log = console.log;
var A = function(){
	this.printA = function(){
		log('this is A!');
	}
}
var B = function(){
	this.printB = function(){
		log('this is B!');
	}
	A.apply(this);// 使用
}
var a = new A();
a.printA();//this is A!
var b = new B();
b.printB();//this is B!
b.printA();//this is A!
```

## `js`创建函数的三种方式

### 第一种直接创建

```
function fun(){
    console.log('this is a function!');
}
```

### 第二种匿名函数赋值

```
var fun = function(){
    console.log('this is a function!');
}
```

### 第三种通过new来创建

```
var fun = new Function('','console.log("this is a function!");');
```

## `markdown`语法记录
### `markdown`创建表格

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

### `markdown`的代码块

```
if(true){
    console.log('this is a code!');
}
```
