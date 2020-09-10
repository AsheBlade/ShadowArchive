---
layout: gallery
title: Madison 骑行拍照
date: 2020-09-10
author: Shadow Song
support: [jquery, gallery]
tags: [手记, Album]
---



需要的配置: 
主要的配置跟上面那个guide走, 这里主要说一下每次新建一个相册需要做的事情. 

1. Markdown 文档之中的插入: 

	```
	{% include gallery-layout.html gallery=site.data.galleries.san-francisco %}
	```
2. yml 文件, 地址在这里: `_data/galleries/san-francisco.yml`要用`gallery_creator.py`处理之后生成
3. 图片要存在: `assets/photography/san-francisco`


    


{% include gallery-layout.html gallery=site.data.galleries.Madison-Bike %}