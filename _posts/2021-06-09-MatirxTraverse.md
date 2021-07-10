---
layout: post
title: Matrix Traverse
date: 2021-06-09
author: Shadow Walker
tags: [Algorithm, Matrix]
---

这部分主要考虑三个问题

- BFS 和 DFS的选取, 哪个更快? 
- DFS的要去写递归解法. DFS 和 BFS 的区别就是DFS有递归, 更灵活. 而BFS只要记一套模板就一劳永逸了. 
- 具体的一些其他解题思路. 

## 题号

490. The Maze
200. Number of Islands
353. Design Snake Game

## 200. Number of Islands

首先是经典的200题. **这道题应该做到无障碍随便就能写出来.**

```java
class Solution {
    char[][] grid;
    int ROW;
    int COL;
  private void dfs(int row, int col) {
    if (row < 0 || col < 0 || row >= ROW || col >= COL || grid[row][col] == '0') {
      return;
    }

    grid[row][col] = '0';
    dfs(row - 1, col);
    dfs(row + 1, col);
    dfs(row, col - 1);
    dfs(row, col + 1);
  }

  public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) {
      return 0;
    }
    this.grid = grid;
    this.ROW = grid.length;
    this.COL = grid[0].length;
    int num_islands = 0;
    for (int row = 0; row < ROW; ++row) {
      for (int col = 0; col < COL; ++col) {
        if (grid[row][col] == '1') {
          num_islands++;
          dfs(row, col);
        }
      }
    }

    return num_islands;
  }
}
``` 

## 547. Number of Provinces

其实思想上和经典的200题完全是相同的, 只是因为本身数据结构的实现方式不同, 所以code有所不同. 

这道题的dfs搜索方式是比较特殊的, 是只查row的方式, 需要想一会儿, 看一下我写的注释, 里面会解答相应疑问. 

```java
public class Solution {
    int[][] grid;
    int ROW;
    boolean[] visited;
    public void dfs(int i) {
        for (int j = 0; j < ROW; j++) {
            if (grid[i][j] == 1 && !visited[j]) {
                // if grid[i][j] is 1 and j row is not visited, we dfs row j. 
                visited[j] = true;
                dfs(j);
            }
        }
    }
    public int findCircleNum(int[][] grid) {
        this.grid = grid;
        this.ROW = grid.length;
        this.visited = new boolean[ROW];
        
        int count = 0;
        for (int i = 0; i < ROW; i++) {
            if (!visited[i]) {
                dfs(i);
                // we don't have to check anything to give count ++
                // Because in this problem, it guarantees that if one row exists, there will be a node.
                // In other words, it guarantees that there exists one 1 in each row.  
                count++;
            }
        }
        return count;
    }
}
```