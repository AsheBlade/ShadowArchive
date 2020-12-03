---
layout: post
title: Bridge in a graph
date: 2020-12-2
author: Shadow Walker
tags: [OPLC, Graph, Algorithm]
toc: true
comments: true
---

## 前面

看了大概五天了, 卡在这道题上面, 没看明白. 到现在也没想明白这道题, 没有完全理解low 和 dis 的概念. 

必须把这个issue关掉了, 不再干了. 也就说明之前OPLC制定的计划可以说完全失败. 

留下这些查的资料, 以便以后有可能重新打开这道题重新看. 

## 两个问题

这个问题可以分为两道题

1. 找 [articulation point](https://www.geeksforgeeks.org/articulation-points-or-cut-vertices-in-a-graph/), 这也是[Leetcode 1192题](https://leetcode.com/problems/critical-connections-in-a-network/)
2. 找 [bridige](https://www.geeksforgeeks.org/bridge-in-a-graph/)

## 比较靠谱的资料 from Baeldung

[这个](https://www.baeldung.com/cs/graph-articulation-points)写的很好, 可惜没有code,如果花时间钻研的话, 应该能看懂. 只不过这道题是没有普遍性的, 看懂了又如何呢? 

## 视频

[这个](https://www.youtube.com/watch?v=aZXi1unBdJA&ab_channel=WilliamFiset) 视频里面的图说的挺简单的, code是python的所以我没看. 这个视频就可以帮助理解low的概念

## Tarjan's Algorithm

整体来说, 这个都统称为 [Tarjan's Algorithm](https://www.geeksforgeeks.org/tarjan-algorithm-find-strongly-connected-components/).  这个里面也有提到 disc 和 low的概念. 

## 之前写的一些零碎笔记

> low[u] = min(disc[u], disc[v])   
> where v is an ancestor of u and there is a back edge from some descendant of u to v.

## 更多想法

这种没有普遍性的高级算法, 有没有学的必要呢? 这是个值得讨论的问题. 其实"学"这个说法是不准确的, 准确的说应该是背. 这种算法跟Dijkstra的话, 不是靠理解就能熟练运用的. 

所以说, 真的有背的必要吗? 

不过, 不管怎么说之前OPLC的计划是失败了. 需要去改变计划, 制定下一步的计划. 

