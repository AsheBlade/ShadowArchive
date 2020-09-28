---
layout: post
title: Latex和 Photo List
date: 2020-09-25
Author: Shadow Walker
tags: [Tech]
comments: true
---

fork之后已经陆续加入了相册功能和加密功能, 还设置了评论区,影音播放和国内的镜像迁移. 

这大概是近期内最后一次加入新功能, latex和照片列表.   latex如下

## Latex

这里其实要说一下, 按照原作者的配置了一下, 发现根本出不来, 一开始还以为自己做错了, 反复看了好几遍.  然后查了一下[文档](https://github.com/mathjax/MathJax), 最后用官方的办法, 在head.html之中加入这一行:

```
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script> 
```
就很简单做到了


```
$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$

```

<!-- more -->

$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$


## PhotoList

照片列表的话, 其实没弄完. 但是可能不想在弄了.  本来想模仿原作者做一个跟[这个](https://opieters.github.io/jekyll-image-gallery-example/photography/)一样的, 结果只有[这个](https://easonback26.github.io/ShadowArchive/photo/).  不想反复调CSS了. 前端的东西很繁琐, 觉得很无聊. 

总结一下, 以便下次工作能够继续进行. 

原版的文件位于: 

1. `/layouts :  page2.html, default2.html`
2. `/css: main.scss`
3. `/sass: _base.scss,  _layout.scss,  _syntax-highlighting.scss`
4. `/includes: head2.html , footer2.html, header.html`

注意: /css: gallery.scss 与这个功能无关, 是有关相册的功能, 不要动也不要删除. 

如果想要看出区别的话, 只要把根目录下的photo.html, 最上面的page改成default2, 就会追随原版, 立刻就能看出区别. 
其实这里我们能看出来原版的CSS非常繁琐, 地点分布甚广.  相比之下, 原作者使用的CSS只有根目录下面的style.css. 

想要把这个相册列表功能完全嵌入无非只有两种办法. 

1. 根据原版的所有CSS逐行查找相关的字体设置, 然后粘贴到新版的`style.css`之中. 这一做法的缺陷也很明显, 有覆盖代码的风险, 污染了其他的部分. 
2. 复制style.css, 重命名, 然后再做第一项. 比较无风险. 缺陷是光改这个也是显然不够. 还要复制一套新的default.html, 或者还需要更多. 

总的来说并不是特别愿意做这种费时又无聊的工作. 本来觉得很简单, 结果却很耗时.  闲的时候可以玩玩. 

## 另

这个刚玩明白, 刚又看见[Hexo](https://www.npmjs.com/package/ayer?activeTab=readme)觉得好漂亮. 这个主题的优势就是简洁加载快. 要明确这个优势. 


## 09-28 更新

`footer.html` 是不会影响格式的, 这个加不加都无所谓. 但是新版和原版的footer代码并不兼容. 
