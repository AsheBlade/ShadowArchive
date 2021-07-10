---
layout: post
title: Topological Sort
date: 2021-07-02
author: Shadow Walker
tags: [OPLC, Algorithm, Graph, Sorting]
toc: true
comments: true
---

## Algorithm

1. 便利每一个节点，根据输入来.  
	a. 并记录每一个节点的入度map<节点，入度的值>.  
	b. 每一个节点指向的节点map<节点，［指向的节点］>.  
2. 把入度为0的节点放入queue中. 
3. BFS.   
	a. 从queue中pop元素，counter＋＋.  
	b. 查看当前节点指向的节点，并把指向的节点的入度的值减1，并把指向的节点的入度为0的元素放入queue中.  
	c. 重复i直到queue为空.  

## 207. Course Schedule

首先就看经典的207题, 下面代码是纯粹手敲的, 注释也是自己写的.  


```java
class Solution {
    
    public boolean canFinish(int numCourses, int[][] prereq) {
        if(prereq.length == 0)
            return true;
        
        // For graph key as node val, value as all the nodes it points to. 
        // 其实这里无论用set 还是 linkedlist都没有任何区别. 
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        // For hm, key as node val, value as its Node Indegree
        Map<Integer, Integer> hm = new HashMap<>();
        
        // 1. Traverse every Node. 
        for(int[] arr: prereq){
            // 1a. record every node and the nodes it points to. 
            Set<Integer> hs = graph.getOrDefault(arr[1],new HashSet());
            hs.add(arr[0]);
            graph.put(arr[1], hs);
            if(!graph.containsKey(arr[0]))
                graph.put(arr[0], new HashSet());
            // 1b. record every node and its Node Indegree
            hm.put(arr[0], hm.getOrDefault(arr[0],0) + 1);
            if(!hm.containsKey(arr[1]))
                hm.put(arr[1],0);
        }
        
        // 2. Init a Queue. Put all the nodes that have Node Indegree 0 into the queue. 
        Deque<Integer> q = new ArrayDeque<>();
        for(Map.Entry<Integer, Integer> entry: hm.entrySet()){
            if(entry.getValue() == 0)
                q.offer(entry.getKey());
        }
        
        int count = 0;
        
        // 3. While q is not empty, poll. 
        while(!q.isEmpty()){
            int pick = q.poll();
            count ++;
            for(int course: graph.get(pick)){
                // 3a. For polled element, reduce all its linked nodes' Node Indegree value by 1. 
                hm.put(course, hm.getOrDefault(course, 1)-1);
                if(hm.get(course)==0)
                    q.offer(course);
            }
        }

        // 4. If the nodes we polled is not equal to graph size(most likely less than or equal to), then false. 
        return count==graph.size();
    }
}
```


## 210. Course Schedule II

210 本质和207题没有区别, 但标准答案提供了另一种写法, 不用HashMap去记录 inDegree, 而用一个int[]去记录, 更加简洁, 但是不想用, 放在这里看看没有坏处. 

```java
class Solution {
  public int[] findOrder(int numCourses, int[][] prerequisites) {

    boolean isPossible = true;
    Map<Integer, List<Integer>> adjList = new HashMap<Integer, List<Integer>>();
    int[] indegree = new int[numCourses];
    int[] topologicalOrder = new int[numCourses];

    // Create the adjacency list representation of the graph
    for (int i = 0; i < prerequisites.length; i++) {
      int dest = prerequisites[i][0];
      int src = prerequisites[i][1];
      List<Integer> lst = adjList.getOrDefault(src, new ArrayList<Integer>());
      lst.add(dest);
      adjList.put(src, lst);

      // Record in-degree of each vertex
      indegree[dest] += 1;
    }

    // Add all vertices with 0 in-degree to the queue
    Queue<Integer> q = new LinkedList<Integer>();
    for (int i = 0; i < numCourses; i++) {
      if (indegree[i] == 0) {
        q.add(i);
      }
    }

    int i = 0;
    // Process until the Q becomes empty
    while (!q.isEmpty()) {
      int node = q.remove();
      topologicalOrder[i++] = node;

      // Reduce the in-degree of each neighbor by 1
      if (adjList.containsKey(node)) {
        for (Integer neighbor : adjList.get(node)) {
          indegree[neighbor]--;

          // If in-degree of a neighbor becomes 0, add it to the Q
          if (indegree[neighbor] == 0) {
            q.add(neighbor);
          }
        }
      }
    }

    // Check to see if topological sort is possible or not.
    if (i == numCourses) {
      return topologicalOrder;
    }

    return new int[0];
  }
}
```

## 444. Sequence Reconstruction

不如下面更经典的269题, 本身题目不复杂, 只是很难想到这个解题思路. 收录在topological sort. 

下面代码变量名都改成了我自己的习惯, 注释也是手打的, 看一会儿就懂, 不懂就再写几个例子吧. 就是常规的topological加一两个条件. 

```java
class Solution {
    
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        Map<Integer, Integer> indegree = new HashMap<>();
        
        for (List<Integer> seq : seqs) {
            // Built two maps. indegree map and graph map. 
            for (int i = 0; i < seq.size(); i++) {
                graph.putIfAbsent(seq.get(i), new ArrayList<Integer>());
                indegree.putIfAbsent(seq.get(i), 0);
                if (i > 0) {
                    graph.get(seq.get(i-1)).add(seq.get(i));
                    indegree.put(seq.get(i), indegree.get(seq.get(i)) + 1);
                }
            }
        }
        
        if (org.length != indegree.size())
            // 如果节点数小于org长度, 当然是false. 这里换成graph.size()也是一样的. 
            return false;

        Queue<Integer> q = new LinkedList<>();
        for (Map.Entry<Integer, Integer> entry : indegree.entrySet()) {
            // Add node with indegree == 0 to the queue. 
            if (entry.getValue() == 0) 
                q.add(entry.getKey());
        }

        int index = 0;
        while (!q.isEmpty()) {
            if (q.size() > 1) {
                // if size>1, it means that we can start from two nodes. Not Unique, false. 
                return false;
            }
            int curr = q.poll();
            if (org[index++] != curr) {
                // Since the result is unique, curr must equal to org[index], otherwise false. 
                return false;
            }
            for (int num : graph.get(curr)) {
                // Normal topological step, update the indegrees of the connected nodes. 
                // and put all other indgree 0 into the queue. 
                indegree.put(num, indegree.get(num) - 1);
                if (indegree.get(num) == 0) {
                    q.add(num);
                }
            }
        }
        return index == org.length;
    }
}
```


## 269. Alien Dictionary

这道题就是topological sort 加上两条条件判断. 直接想是想不出来的, 需要一点点记忆的. 

有两种情况是invalid input, 导致output 为空: 

1. 出现[abc, ab]这种情况. 即后一个本来应该比前一个小, 却被放在后面这种情况. 
2. 另一个情况是出现了环,  [a, b, a] . 因为这样其实就没法排序了. 

还有一种情况是 [abc, x, ab],  这个其实是跟第一种情况相似的, 我们代码中没有考虑, 不过也不用考虑因为这种情况直接回产生 a->x->a 的环.

```java
class Solution {
    public String alienOrder(String[] words) {

        // Step 0: Create data structures and find all unique letters.
        Map<Character, List<Character>> graph = new HashMap<>();
        Map<Character, Integer> indegree = new HashMap<>();

        for (String word : words) {
            for (char c : word.toCharArray()) {
                // init two maps. 
                indegree.put(c, 0);
                graph.put(c, new ArrayList<>());
            }
        }

        // Step 1: Find all edges.
        for (int i = 0; i < words.length - 1; i++) {
            String word1 = words[i];
            String word2 = words[i + 1];
            // Check that word2 is not a prefix of word1, otherwise input invalid. 
            if (word1.length() > word2.length() && word1.startsWith(word2)) {
                return "";
            }
            // Find the first non match and insert the corresponding relation.
            for (int j = 0; j < Math.min(word1.length(), word2.length()); j++) {
                if (word1.charAt(j) != word2.charAt(j)) {
                    graph.get(word1.charAt(j)).add(word2.charAt(j));
                    indegree.put(word2.charAt(j), indegree.get(word2.charAt(j)) + 1);
                    break;
                }
            }
        }

        // Step 2: Breadth-first search. 
        Queue<Character> queue = new LinkedList<>();
        for (Character c : indegree.keySet()) {
            // Typical topological stype, find nodes with indegree=0 and insert into the queue. 
            if (indegree.get(c).equals(0)) {
                queue.add(c);
            }
        }
        System.out.println(queue.size());
        StringBuilder sb = new StringBuilder();
        while (!queue.isEmpty()) {
            // Nothing fancy here. Typical topological sort. 
            // 这道题可以有很多解, 所以我们在这里不需要像444题一样check queue的size是否为1. 
            char pick = queue.poll();
            sb.append(pick);
            for (char c : graph.get(pick)) {
                indegree.put(c, indegree.get(c) - 1);
                if (indegree.get(c).equals(0)) 
                    queue.add(c);
            }
        }

        if (sb.length() != indegree.size()) 
            return "";
        else
            return sb.toString();
    }
}
```