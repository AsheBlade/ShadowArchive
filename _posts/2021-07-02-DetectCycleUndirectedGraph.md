---
layout: post
title: Detect Cycle in undirected Graph
date: 2021-07-02
author: Shadow Walker
tags: [Interview, Algorithm, Graph]
toc: true
comments: true
---


相比较于directed graph, undirected比较局限, 目前只用DFS, 看leetcode最优解是Union find, 目前不学. 

这里就用经典的323题举例子, 代码一看就懂, 简单的DFS查重而已. 


##323. Number of Connected Components in an Undirected Graph

```java
class Solution {
    Set<Integer> visited = new HashSet<>();
    Map<Integer, List<Integer>> graph; 
    
    private void dfs(int start){
        if(visited.contains(start))
            return;
        
        visited.add(start);
        for(int num: graph.get(start)){
            dfs(num);
        }    
    }
    
    public int countComponents(int n, int[][] edges) {
        int output = 0;   
        this.graph = new HashMap<>();
        
        for(int i=0; i<n; i++){
            graph.put(i, new ArrayList<>());
        }
        
        for(int[] edge: edges){
            List<Integer> list = graph.get(edge[0]);
            list.add(edge[1]);
            graph.put(edge[0], list);
            list = graph.get(edge[1]);
            list.add(edge[0]);
            graph.put(edge[1], list);
        }
        
        for(int i=0; i<n; i++){
            if(!visited.contains(i)){
                output ++;
                dfs(i);
            }
        }
        return output;
    }
    

}
```

## 261. Graph Valid Tree

其实跟上面的323 基本是重复的, 只不过加了一行小技巧. 