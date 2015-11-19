---
layout: post
title:  "GitHub常用指令"
date:   2015-11-18 21:06:05
categories: github
excerpt:  GitHub常用指令
---

* content
{:toc}

## 常用指令

指令	|描述
------- |  ---------
$git init	|对文件夹进行git初始化
$git checkout --orphan gh-pages	|创建一个没有父节点的分支gh-pages(该分支下的文件会生成网页文件)
$git add .<br>$git commit -m '备注'	|把内容加入本地git库
$git remote add origin https://github.com/username/rponame.git<br>$git push origin gh-pages	|把本地内容推送到GITHUB上的库里
$git pull origin gh-pages  |push前先将远程repository修改pull下来
$git remote rm origin<br>$git remote add origin https://github.com/username/rponame.git  |更改远程repository地址

---

---

