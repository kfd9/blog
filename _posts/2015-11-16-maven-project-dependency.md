---
layout: post
title:  "maven项目依赖问题"
date:   2015-11-16 21:06:05
categories: jekyll
excerpt:  maven项目依赖问题
---

* content
{:toc}

### 排除全部jar包影响

如 `project1` 需要依赖 `project2` ,但是不想要 `project2` 引用的 `jar` 包。所以在 `project1` 中需要排除 `project2` 内引用的 `jar` 包。当 `project2` 中引用的 `jar` 包太多，一个个排除显然太过麻烦。直接使用 `*` 即可排除引用的 `jar` 包:

	<dependency>
		<groupId>com.xxx.xxxx</groupId>
		<artifactId>xxxx</artifactId>
		<version>1.0</version>
		<exclusions>
		   <exclusion>
			 <groupId>*</groupId>
			 <artifactId>*</artifactId>
		   </exclusion>
		</exclusions>
	</dependency>
	
---