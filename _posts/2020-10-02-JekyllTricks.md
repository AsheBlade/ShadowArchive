---
layout: post
title: Jekyll Tricks
date: 2020-10-02
author: Shadow Walker
tags: [Tech, Shortcuts, Jekyll]
comments: true
toc: true
---

I didn't start to realize this as a problem, until recently when I think about changing the domain name or use a custom server to hold my Github Pages and this problem comes out. 

In order to make my code extensible and viable for future use, I should comply with the Jekyll rules and stop freely do whatever I wanted to. 

## Jekyll Commands

### serve

```
bundle exec jekyll serve
```

## Front Matters
Since I always have to copy and paste this, I just put it here: 

### Simple One

```
---
layout: post
title: 
date: 2021
author: 
tags: []
---
```

### With toc & comments

```
---
layout: post
title: 
date: 2021
author: Shadow Walker
tags: []
toc: true
comments: true
---
```
## Templates

### WR

```
2021-Sprint0WR
---
layout: post
title: OPST Sprint 6 WR
date: 2021-
author: Shadow Walker
tags: [WR, Sprint]
comments: true
---
```

### 庖厨

```
---
layout: post
title: 
date: 2021-
author: Shadow Song
tags: [庖厨]
comments: true
toc: true
---
## 前面
## 材料采购
## 材料准备
## 步骤
## 调味
## 注意
## 点评
## 教学视频
## 成品
```

## 题目格式

题目格式是, 日期加题目.md, 例: `2020-10-02-JekyllTricks.md`

注意, 日期后面才是题目, 不允许有两个完全相同的题目, 比如2020-10-02-JekyllTricks.md 和 2020-12-31-JekyllTricks.md 虽然日期不同, 题目完全一样, 仍然视为是相同题目. 

## Internal Links

It's very important to use internal links, so we can use our website whenever we want. Also, the Gitee mirror page would benefit from internal links.  To use internal links, you have to use: 

I know it will take a while to get used to it. But it's better for continous work. 

```
// The stuff afer post_url is basically the md file name. 
{% raw %}
[Name of Link]({% post_url 2020-08-25-Java_Syntax %})
[]({% post_url  %})
{% endraw %}
```
[Name of Link]({% post_url 2020-08-25-Java_Syntax %})


When link to files, **Jekyll does not allow any file not directly under assets folder.**

For example: 

only this is allowed: 

- /assets/c.pdf

These are not allowed:

- /assets/photo/c.pdf
- /photo/c.pdf

## raw Liquid comment

```
{% raw %}
{% raw %}
{% endraw %}
```

## English

Should use English whenever possible. A blog is not a blog if people have trouble reading it. Should only use Chinese when it's better for understanding. 

## More resource about liquid formats

It's always helpful to learn more about liquid formats from [jekyll official site](https://jekyllrb.com/docs/liquid/tags/#linking-to-posts). 


