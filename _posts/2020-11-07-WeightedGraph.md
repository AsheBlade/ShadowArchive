---
layout: post
title: Weighted Graph
date: 2020-11-07
author: Shadow Walker
tags: [Algorithm, Interview, Graph]
toc: true
comments: true
---

Graph只有引入了Weighted概念才有难度, 才会考虑最短路径的优化问题. 

这一篇的代码[在此](https://github.com/easonback26/Graph/blob/master/src/WeightedGraph.java).  
还写了一个[Integer版的](https://github.com/easonback26/Graph/blob/master/src/WeightedIntGraph.java), 不过应该用不上. 

## 关于背的问题

这一篇应该跟上一篇 [basic graph]({% post_url  2020-08-20-Graph %}) 做对比. 

就目前来看, 还是应该背这个, 因为基本没差几行代码. 而且weighted其实更加常用.  除了print方法可以不背, 其他都应该熟练背诵.
这个class也用了几次了, 应该没什么问题, 放心背吧. 

## 构建 

其实对比unweighted graph, 只不过就是引入了一个inner class Edge 而已, 很直观. 

```java
private static class Edge {
        /*
            ConnectedTo 就是连接到的那个Vertex. 可以是String也可以是Int
            As always we assume all Vertex holds DISTINCTIVE labels.
         */
        private String connectedTo;
        private int weight;

        public Edge(String connectedTo, int weight) {
            this.connectedTo = connectedTo;
            this.weight = weight;
        }

        // Helper method for printing
        @Override
        public String toString() {
            return "Edge{" +
                    "connectedTo='" + connectedTo + '\'' +
                    ", weight=" + weight +
                    '}';
        }
    }
```

## Traverse
 
DFS 和 BFS 都跟unweighted无差别, 没什么可说的. 

## Dijkstra

我没有在网上找到标准的Dijkstra答案, 用的是别人的算法, 然后根据自己改的.  我不完全确定自己写的是对的, 但这个算法已经至少测过三个graph了. 

Dijkstra可说的很多, 但这里没什么可说的了, 因为代码的注释已经足够详细了. 去看代码吧. 
