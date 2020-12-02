---
layout: post
title: Dijkstra For Matrix Graph
date: 2020-11-25
author: Shadow Walker
tags: [Graph]
toc: true
comments: true
---

## 题目

[原题地址](https://app.codesignal.com/interview-practice/task/QTirmApTj7sWaidLk/description)

Graph 有两种构建方法, 一种用Hashmap, 另一种是Matrix. 我觉得第一种容易理解容易做, 就学了第一种. 结果发现实际上, 其实很多coding题都给的是matrix. Matrix其实更简单, 因为只能用Int, 不可能String. 只是需要熟悉. 这道题, 今天做的, 用的是之前Dijkstra代码直接用一样的算法改过来的. 不想传Github了. 这里记录一下, 也许以后用得着呢. **这也从侧面说明我们的Dijkstra代码写的是准确无误的. 有这道题16个test case为证.**

原题截图. 不抄了, 懒了. 

![](https://lh3.googleusercontent.com/lMsMM5ER3JLLL4FrYXJRZAXQFxmZvcfdAR2w1XYkGTzubwA62i1R1smnX-JrO2EnhZy35XCBGhqokGTWI9Cw4A0uyLRA1Fb4P-bU3UxJJB_huwth45k0zTbOwvRKNXd4VyUXtxde9xh_ZZORr7q2m0Qi_TD85UBzFbMzF_-DmW8lpIATuYSOvxQyBF08N1U3nTEyAOgsj3kQDCd70J6gJsb8rykDLevN0CWHawWpYUXPKX8-FGrz65aJiNRU7Wg9pCLH4PovNnfWa5YSUh49D1Mq6NOR-yjR2tdhyqr-ctHHlKaspbkZ1qz9zSlJlPicp4XAFwIIfXMXyPaoINFat3jru6Po1cl_or6PhSnaIZc-TIJUKJ6vU4r2K-mVZ9iEsa4_12qddSD04uzBgem6R3OqVSigTxGSV-qLjS9fZD_GkRyk-yR-n7FoRXouD4EP3Iglz4hsgGtpg55QIhnHWmKtkK7jGD28Zm2GcldKbmzoDRpdmMD_cKv5-CcLXj9OUWF1N5DSHOKLEZzZOH1Ip2WJt5ofAAfDEA4GjyORiuRj91LaNwnIVnrJ6hw4LGfGDMMuWqfYMWCNJ7MYJf21So-d5rhusANLig1yTj_KymCZal8Wfoh8kdPk2mmm-EMgQr4eELFkFFEHgSDifOcrbkSG7uRHnucachQTnsjEkUNqpQZDl2f5cb-VlSDnow=w500-h730-no?authuser=0)

## 解法

```java
private static class minDistance {
    private int distance;
    private int label;

    public minDistance(int label, int distance)
    {
        this.distance = distance;
        this.label = label;
    }
}

int[] graphDistances(int[][] g, int s) {
    
    int[] distance = new int[g.length];
    Set<Integer> visited = new LinkedHashSet<>();
    for(int i=0; i<distance.length; i++){
        distance[i] = Integer.MAX_VALUE;
    }
    
    distance[s] = 0;
    
    PriorityQueue<minDistance> minPq = new PriorityQueue<>((dis1, dis2) -> {
    /*
        Here we use lambda to do comparison. This is same as using a comparator.
        It basically compare the distance and make sure the queue goes from vertex with smallest distance to largest distance.
        */
        int mindis1 = dis1.distance;
        int mindis2 = dis2.distance;
        return mindis1-mindis2;
    });
    
    minPq.add(new minDistance(s,0));
    
    while(!minPq.isEmpty()) {
        minDistance curr = minPq.poll();
        int currNodeDistance = curr.distance;
        int currNodeLabel = curr.label;
        
        if(visited.contains(currNodeLabel)){
            continue;
        }else{
            visited.add(currNodeLabel);
        }
        
        for(int i=0; i<g.length;i++) {
            // traverse for each connected edge.
            
            int weight = g[currNodeLabel][i];
            int newDistance = currNodeDistance + weight;
            
            if(weight == -1){
                continue;
            }else if( newDistance < distance[i]){
                // If the newDistance is smaller than the previous stored one. update the distance.
                distance[i] = newDistance;
                minPq.add(new minDistance(i, newDistance));
            }
        }
    }
        
    return distance;
}
```