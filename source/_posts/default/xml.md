title: xml
categories:
  - default 
description: xml
author: Jade
date: 2020-07-14 14:15:00
---

## xml
	xmlns:
		定义标签，定义默认命名空间。
		命名空间可防止在任何元素的开始标签上。
	xmlsns:xsi
		xml schema instance
		使用dtd实现，用来描述xsd。
		业界默认使用"http://www.w3.org/2001/XMLSchema-instance"。
	xsi:schemaLocation
		指定xsd文件的位置。
		形式为“key value”，中间用空格分开，key为命名空间的值，value为xsd文件的位置。
	
## DTD
	document type definition
	验证xml文件的规范性。
	可内部定义，也可外部引入，也可内外结合。外部引入分为私有（SYSTEM）和公共（PUBLIC）。
	
## XSD
	xml schema definition
	基于XML的DTD代替者。
