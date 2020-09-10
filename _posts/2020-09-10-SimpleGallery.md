---
layout: gallery
title: A Very Basic Example
date: 2020-09-10
author: Shadow Walker
support: [jquery, gallery]
tags: [Tech]
---

之前一直想弄的相册功能, 没想到一次就实现了. 用的是这个[guide](https://easonback26.github.io/ShadowArchive/JekyllAlbumSetup/)

本文是一个基本的sample. 

git log: 

```
commit 003d0159f30e83550a0376c81ed8e80468e8fb16 (HEAD -> master, origin/master, origin/HEAD)
Author: easonback26 <easonback@gmail.com>
Date:   Thu Sep 10 10:56:01 2020 -0500

    lg2
    
```

需要的配置: 
主要的配置跟上面那个guide走, 这里主要说一下每次新建一个相册需要做的事情. 

1. Markdown 文档之中的插入 include 内容显示相册. 这里不写了因为会乱码, 可有看md文件的最后一行. 
2. yml 文件, 地址在这里: `_data/galleries/san-francisco.yml`要用`gallery_creator.py`处理之后生成
3. 图片要存在: `assets/photography/san-francisco`



更多: 

我看原作者那个 Gallery Overview Page 也挺好的, 可以直接加到根目录里, 所有相册的集合. 
    
At the end of our wonderful three week road trip at the West Coast of the US, we spent about four days in the wonderful city of San Francisco. The city's well known for the Golden Gate Bridge and it's fog, but has so much more up its sleeve!

{% include gallery-layout.html gallery=site.data.galleries.san-francisco %}