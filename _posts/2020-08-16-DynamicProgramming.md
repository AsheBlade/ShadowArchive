---
layout: post
title: Dynamic Programming
date: 2020-08-16
author: Shadow Walker
tags: [Algorithm, Interview]
comments: true
toc: true
---

## Overview

DP相关的问题一直是我比较吃力和难以理解的一块. 希望通过总结知识点和相关题目能够增强对DP问题的理解. 

特点: 

1. DP 有一个basic case, 从basic case扩展出一个general case
2. DP从头递增/递减才能够计算. 不存在从中间或者什么奇怪的地方突然冒出来的DP
3. DP基本都会涉及到Max 和 Min, 在Java之中用的是: `Math.max(a,b)`

## Fibonacci 类问题

Fibonacci类的DP有一系列问题. 这种问题的特点有几点: 

1. 都是那种通过前后叠加去解决. 就是上楼梯问题. 
2. 可以通过 Divide-Conquer 化解成 basic problem, 然后解决. 
3. 表面上第一想到的通常用递归解决, 但用递归的话, 有指数复杂度. 


### Fibonacci 

**Description**

The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

> F(0) = 0,   F(1) = 1  
> F(N) = F(N - 1) + F(N - 2), for N > 1.

Given N, calculate F(N).

**Solution**

```java
class Solution {
    public int fib(int N) {
        
        if (N == 0)
        {
            return 0;
        }
        
        if (N == 1)
        {
            return 1;
        }
        
        int[] dp = new int[N+1];
        dp[0] = 0;
        dp[1] = 1;
        
        for (int i=2; i<N+1; i++)
        {
            dp[i] = dp[i-1] + dp[i-2];
        }
        
        return dp[N];
    }
}
```

### Climbing Stairs

**Description**

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Example 1:

> Input: 2  
> Output: 2  
> Explanation: There are two ways to climb to the top.  
> 1. 1 step + 1 step  
> 2. 2 steps  

Example 2:

> Input: 3  
> Output: 3  
> Explanation: There are three ways to climb to the top.  
> 1. 1 step + 1 step + 1 step  
> 2. 1 step + 2 steps  
> 3. 2 steps + 1 step  

**Algorithm**

As we can see this problem can be broken into subproblems, and it contains the optimal substructure property i.e. its optimal solution can be constructed efficiently from optimal solutions of its subproblems, we can use dynamic programming to solve this problem.

One can reach ith step in one of the two ways:

1. Taking a single step from (i-1)th step.
2. Taking a step of 22 from (i-2)th step.

So, the total number of ways to reach ith is equal to sum of ways of reaching (i-1)th step and ways of reaching (i-2)th step.

Let dp[i]dp[i] denotes the number of ways to reach on ith step:

dp[i]=dp[i-1]+dp[i-2]



**Solution**

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```

