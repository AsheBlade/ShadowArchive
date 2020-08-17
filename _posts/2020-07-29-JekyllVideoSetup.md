---
layout: post
title: Jekyll Video and Audio Setup
date: 2020-07-29
author: Shadow Walker
tags: [Tech]
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

## Youtube
{% include youtubePlayer.html id=page.youtubeId %}

## Google Drive Video
{% include googleDrivePlayer.html id=page.driveId %}

### 重要

**不能按照教程之中说的那样, 直接把driveId放在等于号后边. 这样是行不通的, 必须init变量然后引用.** 

## Google Drive Mp3
{% include googleDriveMp3Player.html id=page.driveMp3Id %}

## test
{% include googleDrivePlayer.html id= 1_UJnBUCWiRBPRGRrqcrKy6V1ezrE1gtg/preview %}

{% include googleDrivePlayer.html id=1_UJnBUCWiRBPRGRrqcrKy6V1ezrE1gtg/preview %}