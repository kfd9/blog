---
layout: post
title:  "20151123记录一些java方法"
date:   2015-11-23 21:11:39
categories: java
excerpt:  20151123记录一些java方法
---

* content
{:toc}

## 方法1-获取中文的拼音

包 `pinyin4j` 在 `maven` 里的引用：

	<dependency>
		  <groupId>com.belerweb</groupId>
		  <artifactId>pinyin4j</artifactId>
		  <version>2.5.0</version>
	</dependency>

根据中文获取对应的拼音：

	private boolean isChinese(char a) { 
	     int v = (int)a; 
	     return (v >=19968 && v <= 171941); 
	}
	
    private String getPyName(String chinese) { 
        StringBuffer pybf = new StringBuffer(); 
        char[] arr = chinese.toCharArray(); 
        HanyuPinyinOutputFormat defaultFormat = new HanyuPinyinOutputFormat(); 
        defaultFormat.setCaseType(HanyuPinyinCaseType.LOWERCASE); 
        defaultFormat.setToneType(HanyuPinyinToneType.WITHOUT_TONE); 
        for (int i = 0; i < arr.length; i++) { 
                if (arr[i] > 128) { 
                	if(isChinese(arr[i])){
                		try { 
                            pybf.append(PinyinHelper.toHanyuPinyinStringArray(arr[i], defaultFormat)[0]); 
	                    } catch (BadHanyuPinyinOutputFormatCombination e) { 
							e.printStackTrace(); 
	                    } 
                	}else{
                		pybf.append(arr[i]); 
                	}
                } else { 
                        pybf.append(arr[i]); 
                } 
        } 
        return pybf.toString(); 
    }
	
## 方法2-获取时间段内的随机时间：

代码：

	private long random(long begin, long end) {
		long rtn = begin + (long) (Math.random() * (end - begin));
		
		// 如果返回的是开始时间和结束时间，则递归调用本函数查找随机值
		if (rtn == begin || rtn == end) {
			return random(begin, end);
		}
		return rtn;
	}

	private Date randomDate(String beginDate, String endDate) {
		try {
			SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
			Date start = format.parse(beginDate);// 构造开始日期
			Date end = format.parse(endDate);// 构造结束日期

			// getTime()表示返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。
			if (start.getTime() >= end.getTime()) {
				return null;
			}
			long date = random(start.getTime(), end.getTime());
			return new Date(date);
		} catch (Exception e) {
			e.printStackTrace();
		}
		return null;
	}
	

---