---
layout: post
title:  "mysql自定义的一些函数"
date:   2015-11-19 21:06:05
categories: mysql
excerpt:  mysql自定义的一些函数
---

* content
{:toc}

## 函数1

获取字符串内根据子字符串切割后的字符串长度：

	DELIMITER $$
	DROP FUNCTION IF EXISTS `test`.`getArrayStrLength`$$
	CREATE FUNCTION `test`.`getArrayStrLength`(str varchar(8000),split varchar(10)) RETURNS int
	BEGIN
		DECLARE location INT;
		DECLARE start INT;
		DECLARE length INT;
		SET str = ltrim(rtrim(str));
		SET location=LOCATE(split,str);
		SET length=1;
		myloop:LOOP
			SET start = location + 1;
			SET location = LOCATE(split,str,start);
			SET length = length + 1;
			IF location = 0 THEN LEAVE myloop;
			END IF;
		END LOOP myloop;
		RETURN length;
	END $$
	DELIMITER ;

## 函数2

在数组坐标下查询对应的子字符串：

	DELIMITER $$
	DROP FUNCTION IF EXISTS `test`.`getArrayStrOfIndex`$$
	CREATE FUNCTION `test`.`getArrayStrOfIndex`(str varchar(8000),split varchar(10),dex INT) RETURNS INT
	BEGIN
		DECLARE location INT;
		DECLARE start INT;
		DECLARE next INT;
		DECLARE seed INT;
		SET str = ltrim(rtrim(str));
		SET start = 1;
		SET next = 1;
		SET seed = LENGTH(split);
		SET location=LOCATE(split,str);
		myloop:LOOP
			IF location = 0 OR dex = next THEN LEAVE myloop;
			END IF;
			SET start = location + seed;
			SET location = LOCATE(split,str,start);
			SET next = next + 1;
		END LOOP myloop;
		IF location = 0 THEN SET location = LENGTH(str) + 1;
		END IF;
		RETURN SUBSTRING(str,start,location-start);
	END $$
	DELIMITER ;
	
---