---
layout: post
title: Detect Cycle in a Directed Graph
date: 2020-11-24
author: Shadow Walker
tags: [Interview, Algorithm, Graph]
toc: true
comments: true
---

## 笨办法

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

## Reference

[Checking if a Java Graph has a Cycle](https://www.baeldung.com/java-graph-has-a-cycle)

[Detecting Cycles in a Directed Graph](https://www.baeldung.com/cs/detecting-cycles-in-directed-graph)

[graphcycledetection/domain/ code repo](https://github.com/eugenp/tutorials/tree/master/algorithms-miscellaneous-3/src/main/java/com/baeldung/algorithms/graphcycledetection/domain)

