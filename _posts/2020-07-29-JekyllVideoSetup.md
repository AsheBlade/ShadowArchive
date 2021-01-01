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

## 2020-12-31 最新更新

其实这个办法基本没用. 其实可以直接embed code, 用不着这一套. 但无论是直接embed code, 还是用这个都存在移动端格式的问题. 

目前在移动端这个东西并不好用. 格式会发生视频太长, 右端跳出屏幕边缘的问题. 虽然不影响使用, 终归是不好看的. 暂时没时间, 也没兴趣去解决这个问题. 

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
{% raw %}
{% include youtubePlayer.html id=page.youtubeId %}
{% endraw %}
```

{% include youtubePlayer.html id=page.youtubeId %}

## Google Drive Video
```
{% raw %}
{% include googleDrivePlayer.html id=page.driveId %}
{% endraw %}
```

{% include googleDrivePlayer.html id=page.driveId %}

### 重要

**不能按照教程之中说的那样, 直接把driveId放在等于号后边. 这样是行不通的, 必须init变量然后引用.** 

另: 关于以上黑体字的部分, 我已经尝试过各种相关的方法了(id之后加空格不加空格之类). 不可用!! 切莫继续尝试. 

另: 这个video是需要cookie的, chrome比较好用. safari和其他有时候没有允许cookie的话, 视频是放不出来的. 

## Google Drive Mp3
```
{% raw %}
{% include googleDriveMp3Player.html id=page.driveMp3Id %}
{% endraw %}
```

{% include googleDriveMp3Player.html id=page.driveMp3Id %}