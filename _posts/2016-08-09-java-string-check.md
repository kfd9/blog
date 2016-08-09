---
layout: post
title:  "判断字符串是否相等"
date:   2016/8/9 14:11:09 
categories: java
excerpt:  判断字符串是否相等
---

* content
{:toc}

当字符串`"驼1;驼2;23;24；25;"`和`"23;24；25;驼1;驼2;"`根据分隔符`";"`或`"；"`分割后的各个字符串如果相同那么这两个字符串就是相等的，使用java方法来快速判断:

	public long getStringHashCode(String split, String str){
		long hash = 0l;
		StringTokenizer st = new StringTokenizer(str.trim(),split);
		while(st.hasMoreElements()){
			hash += st.nextToken().trim().hashCode();
		}
		return hash;
	}

	public boolean checkTwoStringBySplit(String str1, String str2) throws RdmsException{
		long hash1 = getStringHashCode("[；;]", str1);
		long hash2 = getStringHashCode("[；;]", str2);
		if(hash1 == hash2){
			return true;
		}
		return false;
	}

其他总结：
-直接比较字符串相等可以使用`hashcode`值比较比`equals`更快(都为非空)

	long t1 = System.currentTimeMillis();
	if("字符串1".equals("字符串2")){
		System.out.println(true);
	}
	long t2 = System.currentTimeMillis();
	System.out.println(t2-t1);
	
	long t3 = System.currentTimeMillis();
	if("字符串1".hashCode() == "字符串2".hashCode()){
		System.out.println(true);
	}
	long t4 = System.currentTimeMillis();
	System.out.println(t4-t3);