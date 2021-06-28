---
layout: post
title: DarkMode and JavaScript
date: 2021-06-28
author: Shadow Walker
tags: [JavaScript, Jekyll]
toc: true
comments: true
---

本来是打算给blog加一个darkmode的, 结果弄了半天没弄出来, 后来在网上找了个darkmode的demo, 弄了半天最后只是把demo弄出来.

**第一次在html里面直接放javascript, 记个笔记, 以后也许会用到这里的小技巧.** 

整个文件是可以用chrome直接跑的, 非常简单有效. 

## Project

A button to set dark mode. 

This webiste is deployed at [here](http://shadowdasher.100webspace.net/DarkMode/themeSwitch.html). 

[Github repository](https://github.com/AsheBlade/DarkModeButton)

This is not my code, the code is from [here](https://codepen.io/sashatran/pen/rPaLgG).

## JavaScript

```javascript

// 这一行必须放在最开头, 要用javascript的话, 必须调用这一行, 不然会有“$ is not defined- $function()” error
// You must not have made jQuery available to your script. So we have to add this line to the top. 
<script type="text/javascript" src="http://code.jquery.com/jquery-1.7.1.min.js"></script>

<head>
  // 这一行link到css去, 唯一要注意的就是文件名写对. 
  <link rel="stylesheet" href="themeSwitch.css" type="text/css">
</head>

<div class="container">
  <div class="theme-switch">
    <div class="switch"></div>
  </div>
  <div class="navigation">
    <ul>
      <a href="http://www.sashatran.com/" class="active" target="_blank">Home</a>
      <a href="https://codepen.io/sashatran/" target="_blank">About</a>
      <a href="https://instagram.com/sasha.codes/" target="_blank">Instagram</a>
      <a href="https://twitter.com/sa_sha26" target="_blank">Twitter</a>
    </ul>
  </div>
</div>

// 下面这个是我们要用的javascript, 原作者是创立了一个新的file, 我觉得太短了没必要就放在这里了. 
// 位置不重要, 也可以整体剪切放在container里面. 不影响. 
<script>
  $(".theme-switch").on("click", () => {
    $("body").toggleClass("light-theme");
  });
</script>
```

## 之后

这个做好了的话, 距离在blog里直接加这个按钮还有很长的路要走.  一个显而易见的问题就是如何确保 点击按钮之后能一次改变所有页面的颜色? 

## 更多

[JavaScript/jQuery - “$ is not defined- $function()” error](https://stackoverflow.com/questions/10779148/javascript-jquery-is-not-defined-function-error)