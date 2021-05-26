---
layout: post
title: Dynamic Programming
date: 2020-08-16
author: Shadow Walker
tags: [Algorithm, Interview, DP]
comments: true
toc: true
---

## Overview

DP相关的问题一直是我比较吃力和难以理解的一块. 希望通过总结知识点和相关题目能够增强对DP问题的理解. 

窍门: 

**如果写不出通式的话, 就从basic case一个一个写下去, 1,2,3,4, 多写几个就会有思路.**

## Fibonacci 类问题

Fibonacci类的DP有一系列问题. 这种问题的特点有几点: 

1. 都是那种通过前后叠加去解决. 就是上楼梯问题. 
2. 可以通过 Divide-Conquer 化解成 basic problem, 然后解决. 
3. 表面上第一想到的通常用递归解决, 但用递归的话, 有指数复杂度. 
4. 这一类我归结为单纯叠加, 不涉及Max和Min之类的问题, 相对来说比较简单. 

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

1. Taking a single step from `(i-1)th` step.
2. Taking a step of 22 from `(i-2)th` step.

So, the total number of ways to reach ith is equal to sum of ways of reaching `(i-1)th` step and ways of reaching `(i-2)th` step.

Let `dp[i]` denotes the number of ways to reach on ith step:

`dp[i]=dp[i-1]+dp[i-2]`



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

## 叠加后求Max/Min问题

特点: 

1. DP 有一个basic case, 从basic case扩展出一个general case
2. 这一类可以算是Fibonacci之上扩展出求Max/Min的问题
2. DP从头递增/递减才能够计算. 不存在从中间或者什么奇怪的地方突然冒出来的DP
3. DP基本都会涉及到Max 和 Min, 在Java之中用的是: `Math.max(a,b)`
4. 基于第三点, DP的Max和Min存在叠加性, 即上一轮的Max可以保证这一轮的Max, 不存在诡异的地方影响. 这一点要牢记

### House Robber

**Description**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night.**

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police.**

Example 1:

> Input: nums = [1,2,3,1]  
> Output: 4  
> Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).  
>              Total amount you can rob = 1 + 3 = 4.  
             
Example 2: 

> Input: nums = [2,7,9,3,1]  
> Output: 12  
> Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).  
>              Total amount you can rob = 2 + 9 + 1 = 12.  

**Algorithm**

This problem is equal to given an array, the solution is to find the maximum sum subsequence where no two selected elements are adjacent. So the approach to the problem is a recursive solution. So there are two cases.

Basic case:
1. no element, return 0;
2. one element, return it. 
3. 2 element, return max(first element, second element. 

General:
Two ways to reach max for ith element. 
1. `nums[i] + dp[i-2]`
2. `dp[i-1]`

比较这两种方法, 求二者之中的最大值, 即为`dp[i].` 

**Solution**

```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if (n == 0) 
        return 0; 
        if (n == 1) 
            return nums[0]; 
        if (n == 2) 
            return Math.max(nums[0], nums[1]); 
   
        // dp[i] represent the maximum value stolen 
        // so far after reaching house i. 
        int[] dp = new int[n]; 
   
        // Initialize the dp[0] and dp[1] 
        dp[0] = nums[0]; 
        dp[1] = Math.max(nums[0], nums[1]); 
   
        // Fill remaining positions 
        for (int i = 2; i<n; i++) 
            dp[i] = Math.max(nums[i]+dp[i-2], dp[i-1]); 
   
        return dp[n-1]; 
    }
}
```

**分析**

这道题的话, 我自己做的话, 第一次是想不到标准答案那么完美的情况. 
如下图, 我会考虑从D点出发,为了避免相邻, 有四种情况, 我会从四种情况之中求max. 

![](../uploads/img/Screen Shot 2020-08-31 at 12.41.14 PM.png)

如下, 是考虑了三中情况(图中1,3,4)而写出的答案.  但其实标准答案之中只考虑了三个量, 没有考虑A的存在, 因为A已经被其他dp包含了. **但其实并不用过度担心这种多写**. 因为Max这个方法是不会增加算力的. 即便多考虑几种情况放到max之中, 在LC之中依然是比100%的人跑得快.  所以这里也是DP的一个特点, **DP看起来都很吓人, 但多动笔写写base case其实很容易出来**. 

另, **这也就是Max问题和单纯Fibonacci的区别.**  Fibonacci类需要考虑所有情况, 而Max类只需要考虑Max就可以. 

```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if (n == 0) 
        return 0; 
        if (n == 1) 
            return nums[0]; 
        if (n == 2) 
            return Math.max(nums[0], nums[1]); 

   
        // dp[i] represent the maximum value stolen 
        // so far after reaching house i. 
        int[] dp = new int[n]; 
   
        // Initialize the dp[0] and dp[1] 
        dp[0] = nums[0]; 
        dp[1] = Math.max(nums[0], nums[1]); 
        dp[2] = Math.max(nums[2]+dp[0], dp[1]);
   
        // Fill remaining positions 
        for (int i = 3; i<n; i++) 
            //dp[i] = Math.max(nums[i]+dp[i-2], dp[i-1]);
            // 以上为标准答案的dp通式, 下面写的这个冗长, 考虑了三种, 但是不会增加算力. 
            dp[i] = Math.max(nums[i]+dp[i-3], Math.max(nums[i]+dp[i-2], dp[i-1]));
   
        return dp[n-1]; 
    }
}
```

### 213. House Robber II

基础的House robber加闭环特殊条件, 关键在于如何处理这个特殊条件. 其实就是走两次, 知道如何处理的话, 其实没啥难度, 再见应该不存在做不出来的问题. 代码写的很难看, 但也是100%, 对于我自己来说比标准答案容易理解, 不收录了, 看我在05/22/2021 12:46提交的答案. 

### 256. Paint House

目前见到House robber家族里最好的一道题. 算是完全覆盖了基础的house robber. 属于House robber问题, 其实就是加了一层维度变成了二维dp而已. 思路并不复杂. 下面答案是按我的习惯自己写的, 没有最优解的dp快, 但基本是一样的. 最优解的会比我省很多space time, 暂时不学. 

```java
class Solution {
    public int minCost(int[][] costs) {
        if (costs.length == 0) 
            return 0;  
        int N = costs.length;
        int[][] dp = new int[N][3];
        dp[0][0] = costs[0][0];
        dp[0][1] = costs[0][1];
        dp[0][2] = costs[0][2];
        for(int i=1; i<N;i++){
            dp[i][0] = costs[i][0] + Math.min(dp[i-1][1],dp[i-1][2]);
            dp[i][1] = costs[i][1] + Math.min(dp[i-1][0],dp[i-1][2]);
            dp[i][2] = costs[i][2] + Math.min(dp[i-1][0],dp[i-1][1]);
        }
        return Math.min(dp[N-1][0],Math.min(dp[N-1][1], dp[N-1][2]));
    }
}
```

### 746. Min Cost Climbing Stairs

我觉得这道题的难点不在于题本身, 而在于条件稀缺.  因为不知道起点的cost是多少, 题目没告诉是0.  这个目前算是一道四星题目, 是值得刷的. 

```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] dp = new int[cost.length+1];

        for(int i=2; i<cost.length + 1; i++)
        {
            dp[i] = Math.min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2]);
        }
        
        return dp[dp.length-1];
    }
}
```

## Boolean dp 问题

这一类的特点是用dp 存储boolean, 进行是否判断. 

### LC139_Word Break

第一眼看上去就知道不会. 一开始想学BFS的解法, 但看了半天觉得复杂. 往下看DP, 豁然开朗. 

**是一道很适合DP的题目**. 跟大部分dp一样, 看起来并不难, 第一次遇见写出来却不容易. 

**code**

没有用标准答案之中的set, 以为测试之后发现算力是一样的. 直接list也可以用contains. 

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
    
    	 // dp size 用s.length()+1 是因为s.substring这个方法, 这个必须用多一位.  这个语法特殊. 例如: 
    	 // String s = "hello"    s.substring(0, s.length()) = s = "hello" ; 
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        
        for(int i=1; i<s.length() + 1; i++)
        {
        	  // 这个double loop看起来很吓人, 其实很容易理解, 就是在每个点去查之前每个点到这个点的可能性. 
        	  // 因为已经用 dp 对之前的点进行了记录, 所以查起来很方便. 
            for(int j=0; j<i; j++)
            {
                if(dp[j] && wordDict.contains(s.substring(j,i))){
                		// dp[i] 为真的条件是dp[j]为真且, i 和 j之间存在legal词汇. 很容易理解. 
                    dp[i] = true;
                    break;
                }
                    
            }
        }
        
        return dp[s.length()];
    }
}
```

## Matrix dp 问题

这个类型的dp, 我还没想好是否单独分一个类. 其主要的特点就是由一个matrix dp去解决, 出现了二维化, 而不仅仅是前面的一维. 

这一块是比较难了. 即使能想明白, 也不一定能写对, 即使能写对也不一定能在规定的时间内写对.  对这一块目前来说还是学习和了解为主, 不需要完全掌握. 

其实如果真理解的话, 其实这一套和一维的也不见得有很大区别.**最大区别也就是多了一个capacity的给定量**. 上边的题目没有限制, 只要去max就可以了, 而这个不同, 在一个有限的范围内给出max. 从而要不断去track这个给定量. 只要抓住这个关键点, 思路就清晰了很多. 

### Non-Fractional Knapsack

关于这个问题, 这个[guide](https://www.educative.io/courses/grokking-dynamic-programming-patterns-for-coding-interviews/RM1BDv71V60#bottom-up-dynamic-programming)写的最好了. 我下面的东西基本都是从这个guide里面来的, 改动很小. 

**Problem Description**

Given the weights and profits of ‘N’ items, we are asked to put these items in a knapsack which has a capacity ‘C’. The goal is to get the maximum profit from the items in the knapsack. Each item can only be selected once, as we don’t have multiple quantities of any item.

Constraints: 

1. an item cannot be used more than twice.    
2. In the list, there is only one item for each weights.    
3. If you take an item, you have to take it as a whole (non-fractional).    

Example:    

Items: { Apple, Orange, Banana, Melon }   
Weights: { 2, 3, 1, 4 }   
Profits: { 4, 5, 3, 7 }   
Knapsack capacity: 5   

We can have the following combinations:   

Apple + Orange (total weight 5) => 9 profit   
Apple + Banana (total weight 3) => 7 profit   
Orange + Banana (total weight 4) => 8 profit   
Banana + Melon (total weight 5) => 10 profit   

**Algorithm**

Essentially, we want to find the maximum profit for every sub-array and for every possible capacity. **This means, `dp[i][c]` will represent the maximum knapsack profit for capacity `‘c’` calculated from the first `‘i’` items.**

So, for each item at index `‘i’ (0 <= i < items.length)` and capacity`‘c’ (0 <= c <= capacity) `, we have two options:

1. Exclude the item at index ‘i’. In this case, we will take whatever profit we get from the sub-array excluding this `item => dp[i-1][c]`
2. Include the item at index ‘i’ if its weight is not more than the capacity. In this case, we include its profit plus whatever profit we get from the remaining capacity and from remaining `items => profits[i] + dp[i-1][c-weights[i]]`

其实从这里我们就可以看出, 二维和一维的情况是一样的, 无非两种情况, 选或者不选.  只不过多了一个capacity的量而已, 需要根据不同的capacity去track而已, 多了一个维度. 

Finally, our optimal solution will be maximum of the above two values:

    dp[i][c] = max (dp[i-1][c], profits[i] + dp[i-1][c-weights[i]]) 
    
  
  Given input of :        ` int[] profits = {1, 6, 10, 16};   int[] weights = {1, 2, 3, 5};`, we have a matrix dp of such: 
  
  ![](../uploads/img/Screen Shot 2020-09-02 at 8.51.32 PM.png)
  
  **Code**
  
  1. 这个code没有递归的, 我觉得是我看过的比较简洁易懂的, 只用一个方法. traverse一遍而已. 没有浪费memory
  2. 这个方法是从前往后走, 即从前往后走. 
  3. 这个guide之中给的例子的两个list都是sorted, 我不确定unsorted的时候这个方法还能不能用. 应该是不行. 
  2. basic case 分为三步,  
 
  	- check edge case, 各种等于0. 
	- set column 0, 
	- set row 0. 
	
  3. general case 就像前面说过的, 无非两种情况, traverse 到 ith item的时候只有两种情况: 选或者不选, 然后取max. 
  4. 代码很吓人, 但像之前说的其实只有两种情况, 多看几分钟结合那个图看自然就看懂了. 可以去[guide](https://www.educative.io/courses/grokking-dynamic-programming-patterns-for-coding-interviews/RM1BDv71V60#bottom-up-dynamic-programming)看一眼, 里面有动画. 


  
  ```java
  public class KnapSack {

    public int solveKnapsack(int[] profits, int[] weights, int capacity) {
        // dp[i][c] will represent the maximum knapsack profit for capacity ‘c’ calculated from the first ‘i’ items.

        // basic checks
        if (capacity <= 0 || profits.length == 0 || weights.length != profits.length)
            return 0;

        int n = profits.length;
        int[][] dp = new int[n][capacity + 1];

        // populate the capacity=0 columns, with '0' capacity we have '0' profit
        for(int i=0; i < n; i++)
            dp[i][0] = 0;
	
	  // Set row 0, i=0 means we are only allowed to take 0th item which is the first itme. 
        // if we can only take the first item, we will take it if it is not more than the capacity
        if(weights[0] <= capacity)
        {
            for(int c=weights[0] ; c <= capacity; c++) {
                dp[0][c] = profits[0];
            }
        }


        // process all sub-arrays for all the capacities
        for(int i=1; i < n; i++) {
            for(int c=1; c <= capacity; c++) {
                int profit1= 0, profit2 = 0;
                // include the item, if it is not more than the capacity
                if(weights[i] <= c)
                    profit1 = profits[i] + dp[i-1][c-weights[i]];
                // exclude the item
                profit2 = dp[i-1][c];
                // take maximum
                dp[i][c] = Math.max(profit1, profit2);
            }
        }

        // maximum profit will be at the bottom-right corner.
        return dp[n-1][capacity];
    }

    public static void main(String[] args) {
        KnapSack ks = new KnapSack();
        int[] profits = {1, 6, 10, 16};
        int[] weights = {1, 2, 3, 5};

        int maxProfit = ks.solveKnapsack(profits, weights, 7);
        System.out.println("Total knapsack profit ---> " + maxProfit);

        maxProfit = ks.solveKnapsack(profits, weights, 6);
        System.out.println("Total knapsack profit ---> " + maxProfit);
    }
}
```

### Longest Palindromic Substring LC_005

**Problem Description**

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.  

Example 1:

> Input: "babad"  
> Output: "bab"  
> Note: "aba" is also a valid answer.  

Example 2:

> Input: "cbbd"  
> Output: "bb"

**Algorithm**

code来自于[GeeksforGeeks](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/). 

这一道的难点在于这个DP general case即使从一开始一个一个从base case开始写也想不出来.  不过其实这种问题很多Matrix DP都是存在的. 上一道其实还容易想一点, 因为是先把column0, row0 都set之后才开始做general case, 不用担心不存在的情况. 这道的话, 是从对角线开始set的, 如果从矩阵的层面去思考的话, 想半天可能都想不明白为什么能保证后面的dp一定被set. 

换个思路, 这么想: **先set所有长度是1的, 然后是所有长度是2的.** 后面从3开始, 自然会track以前1和2的, 然而1和2的都已经被set了. 4的话从3开始track, 而3都被set了.  这么想就容易很多.  这道的切入点是从每个subString的length, 这个思路很难想到. 

最后想说这个不管怎么说还是没有递归的, 拿笔写几下会想的会更清楚. 干看的话看半天也不一定能看明白. 

**Solution**

```java
// Java Solution 
public class LongestPalinSubstring { 
	// A utility function to print 
	// a substring str[low..high] 
	static void printSubStr( 
		String str, int low, int high) 
	{ 
		System.out.println( 
			str.substring( 
				low, high + 1)); 
	} 

	// This function prints the longest 
	// palindrome substring of str[]. 
	// It also returns the length of the 
	// longest palindrome 
	static int longestPalSubstr(String str) 
	{ 
		// get length of input string 
		int n = str.length(); 

		// table[i][j] will be false if 
		// substring str[i..j] is not palindrome. 
		// Else table[i][j] will be true 
		boolean table[][] = new boolean[n][n]; 

		// All substrings of length 1 are palindromes 
		// 把对角线set, 每个dp[i][i] 里面只有一个元素肯定是true的
		int maxLength = 1; 
		for (int i = 0; i < n; ++i) 
			table[i][i] = true; 

		// check for sub-string of length 2. 
		// 一个元素的set之后, 去set二元素的, 因为一个元素都解决了, 两个元素都是在一个元素基础之上的, 肯定是存在的. 
		int start = 0; 
		for (int i = 0; i < n - 1; ++i) { 
			if (str.charAt(i) == str.charAt(i + 1)) { 
				table[i][i + 1] = true; 
				start = i; 
				maxLength = 2; 
			} 
		} 

		// Check for lengths greater than 2. 
		// k is length of substring  k是长度

		for (int k = 3; k <= n; ++k) { 
			// Fix the starting index 
			// 这个算法比较特别, 是从每个string的长度去track的. 长度从小到大. 简而言之是check每个给定长度的所有可能的substring. 
			for (int i = 0; i < n - k + 1; ++i) { 
				// Get the ending index of substring from 
				// starting index i and length k 
				int j = i + k - 1; 

				// checking for sub-string from ith index to 
				// jth index iff str.charAt(i+1) to 
				// str.charAt(j-1) is a palindrome 
				if (table[i + 1][j - 1] 
					&& str.charAt(i) == str.charAt(j)) { 
					table[i][j] = true; 

					if (k > maxLength) { 
						start = i; 
						maxLength = k; 
					} 
				} 
			} 
		} 
		System.out.print("Longest palindrome substring is; "); 
		printSubStr(str, start, 
					start + maxLength - 1); 

		// return length of LPS 
		return maxLength; 
	} 

	// Driver program to test above functions 
	public static void main(String[] args) 
	{ 

		String str = "forgeeksskeegfor"; 
		System.out.println("Length is: " + longestPalSubstr(str)); 
	} 
} 

// This code is contributed by Sumit Ghosh 

```



### Coin Machine

## DP & DFS

这一部分的特点是DP组合其他的问题, DFS, 递归, Backtrack都能和DP组合. 这一部分对我来说挺难的.  目前是绝对不可能写出来的. 

### LC416_Partition Equal Subset Sum

这道题我一开始的思路是BackTrack, 发现写不出来, 看答案发现是DP+DFS.  这道题的DP有几个难点: 
- 用Boolean 构建nums, 因为Boolean的default value是null, 可以查是否赋值. 
- 把点选取的问题简化成subSum选取的问题. 因为这道题是不需要考虑具体一个index的选取的, 只要考虑subSum在这个点选不选即可. 
- 一些小技巧, 比如totalSum必须是偶数. 

下面的DFS模板可以看一下, 可以背, 能用很多地方.  这种题目前对我来说还是太难了, 暂时不考虑掌握, 这个阶段不看DP, 下面的答案是我根据标准答案改的, 更易懂, 标准答案那个不容易看懂. 2021-05-11

**Follow Up:** 698题是这道题的进阶版, 而且用的是我喜欢的backtrack, 可以看一眼. 理论上这道题也可以不用DP用backtrack的. 

```java
class Solution {
    Boolean[][] memo;
    int[] nums;
    public boolean canPartition(int[] nums) {
        int totalSum = 0;
        // find sum of all array elements
        for (int num : nums) {
            totalSum += num;
        }
        // if totalSum is odd, it cannot be partitioned into equal sum subset
        if (totalSum % 2 != 0) return false;    
        int subSetSum = totalSum / 2;

        memo = new Boolean[nums.length][subSetSum + 1];
        this.nums = nums;
        return dfs(0, subSetSum);
    }

    public boolean dfs(int n, int subSetSum) {
        // Base Cases
        if (subSetSum == 0)
            return true;
        // nums.length-1 返回, 因为下面是计算n+1的. nums[nums.length-1]的两种可能都已经算过了. 也是为了防止overflow. 
        if (n == nums.length-1 || subSetSum < 0)
            return false;
        // check if subSetSum for given n is already computed and stored in memo
        if (memo[n][subSetSum] != null)
            return memo[n][subSetSum];
        // n的TF取决于n+1, 在n+1只有两种情况, 或者选取, 或者不选n+1. 如果两种都不行的话, n一定是F. 
        	  // 因为是OR, 所以只要找到一个true, 就会自动断开, 不必担心浪费算力的问题. 
        boolean result = dfs(n + 1, subSetSum - nums[n + 1]) ||
                dfs(n + 1, subSetSum);
        // store the result in memo
        memo[n][subSetSum] = result;
        return result;
    }
}
```

## 特殊

### [LC152_Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

这个解法很特殊的, 一开始刚看到题目的时候以为是跟53题Maximum Subarray一样, 结果跑了一遍才发现需要考虑负数. 

我不知道这个解法是否能用在别的DP上. 第一次看见不需要array的DP.  目前最怕的其实就是这种题, 很特殊, 我解不了, 对其他题目没有帮助, 而且第二次遇见也不能保证做出来. 标准答案的解法就是最佳, 看那个图解, 看几眼就能懂. 其实就是一直track最小值. 

**难点在于** 理解为什么会以一个点去保存连续值. 特别是currMax=tempMax那一行.  因为其实这道题max是保持所有整个array的最大值, currMax是保持当前index可能的最大值, currMax是会经由pointer移动的, max不会. 理解这点也就能完全理解这道题目. 

```java
class Solution {
    public int maxProduct(int[] nums) {
         
        int currMax = nums[0];
        int currMin = nums[0];
        int max = nums[0];
        
        for(int i=1; i<nums.length; i++)
        {
            int curr = nums[i];
            int tempMax = Math.max(curr, Math.max(curr*currMax, curr*currMin));
            currMin = Math.min(curr, Math.min(curr*currMax, curr*currMin));
            currMax = tempMax;
            
            max = Math.max(currMax, max);
        }
        
        return max;
    }
}
```

- 2021-05-10

	第二天早上起来一遍刷出来了, 但还是晕乎乎的. 这道题很特殊, 目前还做不到crystal clear. 估计一个月之后是做不出来的. 
