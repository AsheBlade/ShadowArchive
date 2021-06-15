---
layout: post
title: Matrix Traverse
date: 2021-06-09
author: Shadow Walker
tags: [Algorithm, Matrix]
---

这部分主要考虑三个问题

- BFS 和 DFS的选取, 哪个更快? 
- DFS的要去写递归解法
- 具体的一些其他解题思路. 

## 题号

490. The Maze
200. Number of Islands
353. Design Snake Game

## 200

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