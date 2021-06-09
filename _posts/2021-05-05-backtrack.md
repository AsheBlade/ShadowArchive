---
layout: post
title: Backtrack
date: 2021-05-05
author: Shadow Walker
tags: [Algorithm, Interview, Backtrack]
comments: true
toc: true
---

## 题号

* 78 Subsets
* 90 Subsets II(必刷)
* 46 Permutations
* 47 Permutations II (必刷)
* 77 Combinations
* 39 Combination Sum
* 40 Combination Sum II (必刷)
* 216 Combination Sum III
* 377 Combination Sum IV (没做)
* 131 Palindrome Partition
* 132 Palindrome Partitioning II (DP没做)
* 1278 Palindrome Partitioning III (难题, 没做)
* 1745 Palindrome Partitioning IV (难题, 没做)
* 267 Palindrome Permutation II (和47题重复)
* 17 Letter Combinations of a Phone Number
* 698 Partition to K Equal Sum Subsets

关于一维的backTrack题目, 可以看[这个](https://www.evernote.com/shard/s573/sh/e5985fde-3141-4951-805b-0003add99310/c7a18290e35c0c7fbadea99acd429d5f). 这个总结虽然有的不是最优解, 但这个思路体系模板是非常值得学习的. 

二维: 
二维涉及matrix的统一不在这里总结, 在Matrix专题里总结. 

- LC79
- LC200

偏题/难题: 

- 60  Permutation Sequence

## 刷题顺序

### 核心

Backtrack的核心是三道题(都单独收录了). 

- 40 Combination Sum II  (组合)
- 47 Permutations II  (排列)
- 90 Subsets II  (组合). 

这三道题覆盖了很多其他题目.  刷题先刷这两道, 直到把这两道刷的滚瓜烂熟见到就能默写为止.    如果这三道能做到CC, 整个Backtrack这一块就基本通了.  这三道题就算平时不刷, 没事儿看两眼也是极好的. 

### 好题

好题是难度跟核心类似但普遍性稍差的题目. 

- 131 Palindrome Partition 这道本质不难. 就是复合题.  i+1组合复杂条件判断组合双指针. 
- 698 Partition to K Equal Sum Subsets. 跟上面的131一样, 也是i+1条件判断跳跃. 只不过这道更难更复杂. 目前在条件判断跳跃之中, 这道是最难的.   可以理解为更加复杂的40题. 40题如果刷熟了的话可以刷这道. 

## 技巧总结

### start++

和下面的start++一样, 都是组合(combinations).  区别是start++可以重复使用元素, ++start不可以.  会重复使用后面的元素, 但不会往前走, 例如不会出现2,1的情况. 

如下, 当使用[1,2,3]的时候start ++ 的结果, 看2,3的部分其实不会重复去查1的部分. 每个元素都是unique的, 可以通过list的长度提取自己需要的output: 

```java
[1]
[1, 1]
[1, 1, 1]
[1, 1, 2]
[1, 1, 3]
[1, 2]
[1, 2, 2]
[1, 2, 3]
[1, 3]
[1, 3, 3]
[2]
[2, 2]
[2, 2, 2]
[2, 2, 3]
[2, 3]
[2, 3, 3]
[3]
[3, 3]
[3, 3, 3]
```

### ++start

跟上面start++的区别就是不会重复使用元素.  其实这个不存在, 见下面的i+1

```java
[1]
[1, 2]
[1, 2, 3]
[1, 3]
[2]
[2, 3]
[3]
```

### i+1

i+1 在正常状态跟上面的++start是一样的. 如下. 但i+1的用途是用在查重过滤的情况的时候就会不一样.  换句话说, 在不是一个一个往前走(跳着走)的情况下, 使用i+1.   **这俩其实是包含关系, 所以++start都可以用i+1替代,但不是所有i+1都能用start替代.**

参考著名的40题和131题, 会使用条件判断跳跃. 

```java
[1]
[1, 2]
[1, 2, 3]
[1, 3]
[2]
[2, 3]
[3]
```

### start+1

这个很少见, 目前只见过46题的swap解法在使用. 没见过第二道. 就不总结了. 


## Complexity Analysis

这一系列题目complexity通常都是一样的.  下面这个来自40题的截图. 


![](https://lh3.googleusercontent.com/pw/ACtC-3c4oY-srWO5rgHXDog4EJgOwDgkPWm7KQZwc5BChp3HETIKyX42dHECkEOMOE16ogL2C0CC1qCIMk2sUAY9FvKvl8A5VJPIfzJjlUsVUdUcyuyXFFkP_XeX9ZTwZlsMZalm-Gh-0pYV4Q-acsbS-p0J=w635-h436-no?authuser=0)

![](https://lh3.googleusercontent.com/pw/ACtC-3cXpes0x0OomgMlI0v6fqanlpM5ywD-NaCTHarbHgOzkN72UOChrdXluAVLKPRsj9ABzzLArSGqjJBNVsJHTHPYidbJGmGLRwc_kAhOb0T9R3SW4nlql5zsCgeYyid8e2NSyYBsJGPZz4-3O7KG8FD0=w617-h576-no?authuser=0)

## Problems

### 78. Subsets

++start

自己写的答案, 一遍过. 比较基本的Backtrack.  要看我提交的答案, 写的比标准答案好. 



### 46. Permutations

这道是没有start的题. 我习惯用的是hashset的解法. 

5星. 单独收录了. 很经典的一道类型题. 值得多刷.  第二个解法记得不要觉得省事儿不用set, set可以节省算力. 

### 47. Permutations II

5星必刷. 完全覆盖了46题. 

### 77. Combinations

虽然中等, 但对我来说算是简单的backTrack. 一刷过了. 4星是因为这个阶段刷backTrack是有帮助的, 就算不刷看一眼也是好的, 以后可以降到3星. 没有收录. 


### 39. Combination Sum

一刷过了. 

### 40. Combination Sum II

5星.  单独收录了. 看起来跟之前那些思路类似, 实则完全不同, 而且要考虑去重的问题, 好题. 三刷终于领悟. 

### 216. Combination Sum III

和经典的77题combination基本是一道题. 虽然比77题多了一个sum判断条件, 但不算提升难度. 跟77一样, 一刷过了. 没有收录, 看我的答案. 我写的比标准答案更好. 


### 131. Palindrome Partitioning

i+1

好题. 五星, 单独收录. 

### 17. Letter Combinations of a Phone Number

Backtrack基本题, 两周之后一刷过了.  这种题从一开始烧脑, 到现在对我来说已经是简单题了, 非常自豪. 

自己写了100% code, 看提交记录,  比标准答案易读易懂. 


