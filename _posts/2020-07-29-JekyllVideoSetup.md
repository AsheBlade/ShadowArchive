---
layout: post
title: Jekyll Video and Audio Setup
date: 2020-07-29
author: Shadow Walker
tags: [Tech, Shortcuts]
comments: true
toc: true
youtubeId: H_nCw1WMFs4
driveId: 1_UJnBUCWiRBPRGRrqcrKy6V1ezrE1gtg/preview
driveMp3Id: 11HyVcPGeCBGMKBNobLiR7M3KXPMMEnZu/preview
---

## Overview
This page is about how to embed video and audios into Jekyll.   
Everything on this page is from nathancy's work from [here](https://github.com/nathancy/jekyll-embed-video#embed-google-drive)  
Please note that we should try to avoid using local or Youtube files as much as possible. Do use Google Drive!

## FrontHead

```
---
layout: post
title: Jekyll Video and Audio Setup
date: 2020-07-29
author: Shadow Walker
tags: [Tech, Shortcuts]
comments: true
toc: true
youtubeId: H_nCw1WMFs4
driveId: 1_UJnBUCWiRBPRGRrqcrKy6V1ezrE1gtg/preview
driveMp3Id: 11HyVcPGeCBGMKBNobLiR7M3KXPMMEnZu/preview
---
```

## Youtube
```
{% comment %}
{% include youtubePlayer.html id=page.youtubeId %}
{% endcomment %}
```

{% include youtubePlayer.html id=page.youtubeId %}

## Google Drive Video
```
{% include googleDrivePlayer.html id=page.driveId %}
```

{% include googleDrivePlayer.html id=page.driveId %}

### 重要

**不能按照教程之中说的那样, 直接把driveId放在等于号后边. 这样是行不通的, 必须init变量然后引用.** 

另: 关于以上黑体字的部分, 我已经尝试过各种相关的方法了(id之后加空格不加空格之类). 不可用!! 切莫继续尝试. 

另: 这个video是需要cookie的, chrome比较好用. safari和其他有时候没有允许cookie的话, 视频是放不出来的. 

## Google Drive Mp3
```
{% include googleDriveMp3Player.html id=page.driveMp3Id %}
```

{% include googleDriveMp3Player.html id=page.driveMp3Id %}