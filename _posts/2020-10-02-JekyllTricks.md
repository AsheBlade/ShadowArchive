---
layout: post
title: Jekyll Tricks
date: 2020-10-02
author: Shadow Walker
tags: [Tech, Shortcuts, Jekyll]
comments: true
---

I didn't start to realize this as a problem, until recently when I think about changing the domain name or use a custom server to hold my Github Pages and this problem comes out. 

In order to make my code extensible and viable for future use, I should comply with the Jekyll rules and stop freely do whatever I wanted to. 

## FrontHead
Since I always have to copy and paste this, I just put it here: 

```
layout: post
title: Jekyll Tricks
date: 2020-10-02
author: Shadow Walker
tags: [Tech, Shortcuts, Jekyll]
comments: true
```

## Internal Links

It's very important to use internal links, so we can use our website whenever we want. Also, the Gitee mirror page would benefit from internal links.  To use internal links, you have to use: 

```
{% raw %}
[Some Link]({% post_url 2010-07-21-name-of-post %})
{% endraw %}
```

[Some Link]({% post_url 2010-08-25-Java_Syntax %})

## raw liquid code

To comment, liquid code, you have to use raw code parts, such as: 

```
{% raw %}
{% raw %}
{% endraw %}
```


## English

Should use English whenever I can. A blog is not a blog if others cannot read it. Only use Chinese when it's better for understanding. 

