---
layout: post
title: 游标卡尺
date: 2020-09-03
author: Shadow Walker
tags: [Algorithm, Interview]
toc: true
---

## Overview

这一篇是关于sliding window这个奇淫技巧的. 现在其实对于Array的考察非常烦人. 这一块比较简单所以没什么可考的, 一旦考的话, 就是这种奇淫技巧. 其实这种技巧工作和学习之中用途基本没有, 而且适用的题型也很少. 

之所以想记录一下这个技巧是觉得其还是有一定的适用性, 也许以后能够用到. 

## Longest Substring Without Repeating Characters LC_03

就是这道题其实当时baanyan第一天还跟老师怼上了. 因为我当时说我用hashmap能解而且算力上并不慢. 现在想想应该是我错了. 我今天想了半天也没想到hashmap怎么能做出和这个标准答案算力一样的解法. **所以说, 做人做学问还是应该虚心一点, 尾巴收起来**. 我当时之所以瞧不上老师的解法是因为我当时(其实现在也存在)打心底瞧不起这种只适用于一道或者几道题的奇淫技巧, 觉得这种东西花拳绣腿, 学的比较鸡肋. 

老师当时称这个解法为"双指针", LC称这个解法为Sliding Window, 我更喜欢称之为游标卡尺. 

**Problem Description**

Given a string s, find the length of the longest substring without repeating characters.

Example 1:

> Input: s = "abcabcbb"  
> Output: 3  
> Explanation: The answer is "abc", with the length of 3.

Example 2:

> Input: s = "bbbbb"  
> Output: 1  
> Explanation: The answer is "b", with the length of 1.

**Code**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> hs = new HashSet<>();
        int answer=0, i=0, j=0;
        
        while(i<n && j<n)
        {
            if(!hs.contains(s.charAt(j)))
            {
                hs.add(s.charAt(j));
                j++;
                if(hs.size()>answer)
                {
                    answer = hs.size();
                }
            }
            else{
                hs.remove(s.charAt(i));
                i++;
            }
        }
        return answer;
    }
}
```

**Algorithm**

直接看以上这个code会比较迷, 我当时看答案也是看了很久没看明白. 其实自己在纸上写了一下很容易想明白. 

其实这个算法并不难, 也不玄乎, 反而比较实际, 容易理解.  把Set hs想象成一把游标卡尺, 卡尺的左端是i, 右端是j. 
假设我们有一个String  ABCDAE

从A点出发, i和j都在0, 也就是A, 只要下一个char没有重复, 游标卡尺的右端就不断往下一个char走. 如上面的例子, 游标卡尺走到ABCDA, j = 4的时候会停住.  这个时候从A点出发的不重复subString已经到了Max. 这个时候把尺子右端不动, 把卡尺左端往后挪一位. 我们得到 BCDA. 之后下一位还是不重复的E, 再挪右端j, 左端i不动. 得到BCDAE. 这个过程中keep tracking 卡尺的max长度. 最后得到答案5. 

两点: 

1. 一开始会考虑要不要向前track, 其实想一下完全没有必要. 这个理解就是和DP是一样的, 因为之前的元素已经被卡尺求过了, 没有必要向前. 所有的subString都是向后track. 
2. 一开始是在想是不是要在每个字母上卡一下, 是不是一旦出现了重复元素之后, 就立刻要把尺子收紧把左端右端合在一起然后重新测量, 会把else写成这样: 

	```java
	else{
	    hs = new HashSet<>();
	    i++;
	    j=i;
	}
	```
	
	举个例子: ABCBD 这个, 一开始尺子卡在ABC, 然后在B发现重复, 尺子收起来, 从B(i=1)开始重新卡. 我会这么想, 其实这么想也比较直观. 
	
	其实实际上没有必要. **关键在于这个尺子里面的元素是不可重复的**, 也就是说尺子内部的元素是绝对干净的. 这个时候没有必要收尺子, 尺子左端已经在正确的位置, 只要继续挪动右端就可以了. 
	
还有一些更快的解法, 游标卡尺加上hashmap的解法, 不想去学了. 这种奇淫技巧学的差不多就可以. 目前阶段没必要学最优解, 现在主要是大量刷. 

## Container With Most Water LC_011

**Problem Description**

题目不放了, 因为需要看图才能看懂, 直接去[LeetCode](https://leetcode.com/problems/container-with-most-water/)上面看吧. 

**Algorithm**

这道题我拿来首先想到的就是dynamic programming, 但越想越觉得不符合dynamic的求和原则, 因为需要考虑之前的所有边.   

算法是游标卡尺, 这一次的游标卡尺是从首尾两端开始卡, 慢慢往里面收. 由于题目的特殊性而使用木桶原理.  

**这种特殊的题目没什么好说的, 唯有刷脸.**

<br>

**Code**

```java
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0, left = 0, right = height.length -1;
        
        while(right>left)
        {
            maxArea = Math.max(maxArea, Math.min(height[left], height[right])*(right-left));
            //System.out.println(left + " , " + right + " , " + maxArea);
            if(height[left]>height[right])
            {
                right--;
            }
            else
            {
                left ++;
            }
        }
        return maxArea;
    }
}
```
