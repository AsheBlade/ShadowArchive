---
layout: post
title: Interview 临场复习指南
date: 2020-08-25
author: Shadow Walker
tags: [Interview,  Algorithm]
toc: true
---

# Overview

经常会面临收到大场面试需要在两三天之内集中复习刷题的情况. 这个指南的意义就是为了应付这种情况. 即在短期之内把该刷的题目集中复习. 每一个类别挑几个典型题出来集中刷. 这样的话, 就不用在临近面试的时候再去网上搜题刷了. 

**2021-07-08更新:** 一年之后再回来看去年写的这些, 当时很多认识都极为幼稚, 于是重新更新, 大部分删除原有内容, 基本重写. 

**因为我想看看以前记了什么, 发现其实也没什么, 随便改改, 没改完. 就先放了吧. 不看这个.**

这个指南会比较详尽一点, 适合在很长时间都没碰题的时候, 在对相应算法比较生疏的时候拿出来用. 

# Syntax

Syntax的总结在这个[guide](https://easonback26.github.io/ShadowArchive/Java_Syntax/)之中.  

Syntax是需要刷一下的, 不然总当场google多少是会减分. 





# Linked Lists


# HashMap

这块是重点. 可以说是重点之中的重点, 而且比较灵活.   HashMap是提升RunTime的必备, 这一块必须掌握.  **但是其实HashMap是没什么规律可言的, 只能说一些题目会用到HashMap.**  所以其实HashMap这一块不适合做专题. 

两个月前还写了这么一个[guide]({% post_url  2020-08-19-HashMap %}), 现在看起来这个guide非常浅. 但毕竟是当时写的东西, 我又舍不得删. 放在这里吧. 可以扫一眼作为参考, 不过真是没多大价值. 

# Trees
 **关于Tree的问题都是递归问题.**    Tree的特点是没什么应用题, 只要是用到Tree的题基本都会明明白白告诉你用Tree, 所以跟HashMap不同, 不需要去思考用不用Tree的问题.  这部分解题思路抓住一个重点, 师傅说过, **90%以上的Tree题目都可以通过三种DFS和BFS解决**, 不过另外10%就真是初见杀了, 看运气吧. 主要看这个[guide]({% post_url 2020-08-19-Tree %}), 写的非常详细了. 一年之后再回来看当时写的这个guide写的真是好. 这是我这么多年为数不多写的非常非常好的guide. 
 

 
 
# Heaps, Stacks, Queues

# Graphs

图论不是重点. 美国考的可能性很低, 做几道基本类型题即可, 不需要多看. 

1. 对于基本概念的掌握. 这一块相比几个的话, 概念有很多. 基本的constructor构建, 还有一些变体, 有方向的edge, 和没方向的. 关于这一块可以看这个[guide]({% post_url  2020-08-20-Graph %}).  
2. 只掌握一个图还不行, 还要掌握各种最短路径的搜索方法. 最知名的当然是Dijkstra.  偏的有Prim和Tarjun. 
3. 熟练掌握前两项之后就可以刷题了. 

# Sorting

Sorting 这一块其实没什么多说的. 就看这个[guide]({% post_url 2020-08-20-Sorting %}), 写的非常详尽了. 

1. 英文描述, Bubble Sort, Insertion Sort, Select Sort, Merge Sort and Quick Sort. 这几类要熟, 做到张口就来不需要回忆. 
2. 第一项上面几个的 time complexity. 
2. QuickSort, MergeSort 整理的代码需要背, 能不用思考立刻写出来. 
3. QuickSelect (LC973)



# Dynamic Programming

DP 目前不是我这个水平的重点. 


