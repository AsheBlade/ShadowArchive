---
layout: post
title: Jekyll Post_url Bug
date: 2020-11-21
author: Shadow Walker
tags: [Bug]
toc: true
comments: true
---

今天发生了一个很有意思的bug,  就是关于Internal Link
```
// The stuff afer post_url is basically the md file name. 
{% raw %}
[Name of Link]({% post_url 2020-08-25-Java_Syntax %})
[]({% post_url  %})
{% endraw %}
```

突然发现之前所有的internal link都不能正常打开了, 全是404. 

于是, 我看了一下Local环境, 都没问题啊. 问题在哪里呢? 

1. 我去查了Jekyll 的官方文档, 又测试了几次, 发现miss掉了baseurl, 于是我去查config, 发现也没问题呀
2. 我去Google, Stack Overflow告诉我要升级Jekyll到4.0. 我在local升级, 结果还是local没问题, github-page部署之后就出问题. 
3. 我去看Github官方的文档, 看了半天, 得出结论还是一样, 我不可能去升级github内部的jekyll版本. 
4. 最后我看到了这个: 

![](https://lh3.googleusercontent.com/pw/ACtC-3d25uWnC5aPz4QCtXTTDQSCPXBaXRBBpiGGfL3_KxOe5AzUKvfXaf-VG9BlSMilHCHlbvUVmtNq4Hl1yjBg8TuZorC4V0hCcQ4v6gULf5ANrBc0JZ1Ogo_qZ_F7WYzUrYfc_LQDVmKPI-CgY06AJ6PD=w621-h360-no?authuser=0)

![](https://lh3.googleusercontent.com/pw/ACtC-3cUnF_850CHqGW6zVi3XQvkQYE3wAJYzcwc8-GZ4fDErqJqlgLA7tdZtzDTwqqq5OZXWtq7qU4VXgraC8LuO9tJlOukaIU1ayfBY6l48Kcn0os_hdqe_-hXF16G7ds3KMg8_8gMNnnyTp5R0-jOs_wA=w912-h455-no?authuser=0)

瞬间气乐了, Jekyll在一年前就公布了4.0, 但Github现在还在用3.9, 难怪我在Local测试没问题, 一deploy到github 就出错. 

一个可行的解决办法, 就是用旧的syntax, 在前面加site.baseurl, 不过这个办法其实没法根本上解决. 

```
{% raw %}
// 这个解决方式使用3.9版本, 4.0版的解决方式在Jekyll Tricks
[xyx]({{site.baseurl}}{%link _posts/2020-11-06-UphillDownhill.md %})
{% endraw %}
```

**因为经过local测试, 新的4.0不接受这个旧的syntax, 但3.9不接受新的syntax**

也就是说, 如果改过来之后以后github更新了4.0, 这些就都用不了了.  所以, 也就只能先这么放着了. 长远看, 这么写还是好的, Github以后肯定还是会更新的.  现在于是只能用local部署去看文档, 以解决link失效的问题



这个故事告诉我们: 

**Production 和 development的环境一致是多么重要啊!**

