---
layout: post
title:  "IE7下使用onchange事件重复上传附件问题"
date:   2015-11-23 20:07:09
categories: IE
excerpt:  IE7下使用onchange事件重复上传附件问题
---

* content
{:toc}

## 问题

在IE7下使用的input type=file的onchange事件上传附件时会上传两条同样的附件，查找资料后发现是属于IE7本身的问题

> IE has an issue when when:
> onchange event fires, causing DOM structure/content to change (e.g. your .innerHTML change)
> which basically causes a race condition between 2 threads.... the one updating the content (the
> .innerHTML) and the one moving the focus to the new field.
> Since IE only supports a single GLOBAL event object instead of the W3C Event model where the
> events are linked to the things that fire them, there are chances for collissions like the one you are
> witnessing.
> Basically you have 1 event saying "give focus to this" and another saying "change the text content
> of this"... but they collide, and you end up with focus in the div.
> In all the other Standards based browsers, there is an event instance linked to the "i2" input box,
> of type "onchange" when you "leave" the input box, by clicking in the "i1" input box, which fires its
> own linked event for "onfocus".
> The flaw with the MS design is more apparent when you consider the other events (that you are
> not tracking) that are also firing

大概意思就是：

>  `IE7` 下对 `onchange` 事件的处理存在bug，即 `input` 的 `onchange` 事件触发时对应了两个线程，一个是 `value` 改变的 `change` ，一个是鼠标改变的 `change` ，`IE7` 无法处理这个问题就会变成一个 `onchange` 事件会触发两次

解决方法：

>设置一个全局的 `js` 变量，记录每一次触发 `onchange` 时的值同时对比上次记录的值即可。

---