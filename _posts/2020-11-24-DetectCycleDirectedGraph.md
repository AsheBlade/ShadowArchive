---
layout: post
title: Detect Cycle in a Directed Graph
date: 2020-11-24
author: Shadow Walker
tags: [Interview, Algorithm, Graph]
toc: true
comments: true
---


## Topological Sort

 2021-07-02 更新: 师傅教的最优解法. 下面都不用看了, 就看[Topological Sort]({% post_url 2021-07-02-TopologicalSort %})即可. 
 
## 笨办法

```
boolean hasDeadlock(int[][] connections) {
// 1. 从每个vertex做DFS
// 2. 如果traverse之中child出现了root, 即返回true, 最后都没有才是false. 
    Set<Integer> visited = new LinkedHashSet<>();
    Stack<Integer> stack = new Stack<>();

    for(int i=0; i<connections.length;i++)
    {
        stack.push(i);
        int root = i;
        
        while (!stack.isEmpty()) {
            int s = stack.pop();
            visited.add(s);
            
            for (int eachConnected : connections[s]){
                System.out.println(i + " - ");
                System.out.println(eachConnected);
                if(eachConnected== root){
                    return true;
                }
                else if (!visited.contains(eachConnected) ) {
                    //visited.add(eachConnected);
                    stack.push(eachConnected);
                }
            }
        }
        
        visited.clear();
        stack.clear();   
    }
    
    return false;
}
```

## 更多

2021-04-11

下面的reference 之中有简单办法, 这道题有聪明办法可以O(V), 但是已经不想研究了. 因为本来2020年11月的时候已经研究过了, 也看懂了, 但隔了几个月又忘光了. 

因为目前对于Graph的态度就是把进本的DFS, BFS掌握, 其他进阶的直接放掉. **这种题即使看懂了, 研究透了, 过几个礼拜不看也会完全忘光**. 目前的主要不是这个.   主要是掌握简单的DP和递归. 

总的来说, **是很遗憾的. 但此时的我一没有时间, 二没有精力去仔细研究掌握了. 希望有朝一日能够重新回到这里把这道题弄懂.**

## Reference

[Checking if a Java Graph has a Cycle](https://www.baeldung.com/java-graph-has-a-cycle)

[Detecting Cycles in a Directed Graph](https://www.baeldung.com/cs/detecting-cycles-in-directed-graph)

[graphcycledetection/domain/ code repo](https://github.com/eugenp/tutorials/tree/master/algorithms-miscellaneous-3/src/main/java/com/baeldung/algorithms/graphcycledetection/domain)

