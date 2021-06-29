---
layout: post
title: 问 Binary Search
date: 2021-06-29
author: Shadow Walker
tags: [OPLC, BinarySearch]
toc: true
comments: true
---

这两天集中做了很多binary search, 发现其实这个系列的应用还是很多的, 发现了这个类型, 我觉得需要问一下. **问题在页面最底下**. 

这个类型我目前称之为区间取值问题, 我大概做了近8道题, 下面挑了两道有代表性的总结, 还有一道有问题的. 

这类问题的特点是根据条件可以选取一个最大值和最小值, 然后在这两个点之间选取满足题目条件的值.  满足条件的值肯定是min/max. 

- 这类问题给定的array一定是不含负数的, 不然判断不能用O(n)达成
- 在subarray上的取值一般是有连续性的, 但也有例外(1482题), 但即使不是连续取值, 但至少for loop的比较过程也一定是O(n). 

比较有代表性的有两道题(题本身没问题, 需要老师帮忙总结思路): 

- [410 Split Array Largest Sum  (Minimize Largest Sum)](https://leetcode.com/problems/split-array-largest-sum/)
- [1231 Divide Chocolate (Maximize Smallest Sum)](https://leetcode.com/problems/divide-chocolate/)

这两道题是没问题的, 是我总结的这个类型的两道代表性题目. 

有问题的一道难题: 

- [774 Minimize Max Distance to Gas Station](https://leetcode.com/problems/minimize-max-distance-to-gas-station/)

这个类型其他更多题目(没有问题):

![](https://lh3.googleusercontent.com/pw/AM-JKLUzp6X9j4UhPXByieq62dKf8hx0eDTDSGOb2CzlYOjwCd5QFClSsglsMOjGyI6cW1LzK-aWtbhk79_LkKJIOSeZ2888Q3zHXba4zytm0u-hVZ0Shl97-ztSzkow9hWS4sHOI8I77jmhzXjD1rbDorV8=w526-h209-no?authuser=2)

### [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)(对题目本身没有问题)

Minimize Largest Sum. 

这道题可以说是这个系列最典型的题目, 我下面写了两个binary search解法, 附带了答案中的DP解法. 

**我对这道题本身太多问题, 代码中有个小问题在中文注释之中, 我的问题是这个类型的特点是什么? 老师能不能帮我总结一下什么时候去要去想到能用binary search解这种题? 什么时候没法用binary search, 只能用DP?**

**left<=right解法**

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int left = 0, right = 0;
        for(int num: nums){
            left = Math.max(left, num);
            right += num;
        }
        
        if(m==1)
            return right;
        
        while(left<=right){
            int middle = left + (right-left)/2, curr = 0, count = 1;
            // count is 1, because in the for loop below, the last subarray is not counted. 
            for(int num: nums){
                curr += num;
                if(curr>middle){
                    curr = num;
                    count ++;
                }
            }
            if(count > m)
                left = middle + 1;
            else
                right = middle - 1;
        }
        return left;
    }
}
```

**left<right解法**

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int left = 0, right = 0;
        for(int num: nums){
            left = Math.max(left, num);
            right += num;
        }
        
        if(m==1)
            return right;
        
        while(left<right){
            int middle = left + (right-left)/2, curr = 0, count = 1;
            // count is 1, because in the for loop below, the last subarray is not counted. 
            for(int num: nums){
                curr += num;
                if(curr>middle){
                    curr = num;
                    count ++;
                }
            }
            if(count > m)
                left = middle + 1;
            else
                right = middle;
        }
        return left;
    }
}
```

**DP**

```java

class Solution {
    public int splitArray(int[] nums, int m) {
        int n = nums.length;
        int[][] f = new int[n + 1][m + 1];
        int[] sub = new int[n + 1];
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                f[i][j] = Integer.MAX_VALUE;
            }
        }
        for (int i = 0; i < n; i++) {
            sub[i + 1] = sub[i] + nums[i];
        }
        f[0][0] = 0;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                for (int k = 0; k < i; k++) {
                    f[i][j] = Math.min(f[i][j], Math.max(f[k][j - 1], sub[i] - sub[k]));
                }
            }
        }
        return f[n][m];        
    }
}
```

## [1231. Divide Chocolate](https://leetcode.com/problems/divide-chocolate/)(没有问题)

Maximize Smallest Sum. 

跟上一道题刚好是反的, 但其实比上一道题需要思考很多, 更难.  关于这道题我自己也想通了, 放在这里就是总结一下这种类型. 

一开始想了半天, 还是没想明白为什么是curr = 0.  直到看到评论区

> Since we are looking for minimum now, it is okay if subarray sum greater. In no. 410, if the sum of subarray section greater than target is forbidden, since the target is our maximum sum of subarray. However, in this problem, we look for the lower bound and make sure the number of splits is correct. Thus, when total > target we treat the new element in the same subarray so we reset total = 0. On the other hand, we need separate the new element in another subarray so we set total = num. 

**left<=right解法**

```java
class Solution {
    public int maximizeSweetness(int[] sweetness, int k) {
        // set our left and right boundary
        int left = Integer.MAX_VALUE, right = 0;
        for(int sweet: sweetness){
            left = Math.min(left, sweet);
            right += sweet;
        }
        // Two edge cases
        if(k==0)
            return right;
        if(sweetness.length<=k+1)
            return left;
        right = right/(k+1);
        
        // binary search and find the result. 
        while(left<=right){
            int middle = left + (right-left)/2, curr = 0, piece = 1;
            for(int sweet: sweetness){
                curr += sweet;
                if(curr > middle){
                // 这里curr = 0 是这道题的难点. 需要反复思考. 
                    curr = 0;
                    piece ++;
                }
            }
            if(piece > k+1)
                left = middle + 1;
            else
                right = middle - 1;
        }
        return left;
    }
}
```

**left<right解法**

```java
class Solution {
    public int maximizeSweetness(int[] sweetness, int k) {
        // set our left and right boundary
        int left = Integer.MAX_VALUE, right = 0;
        for(int sweet: sweetness){
            left = Math.min(left, sweet);
            right += sweet;
        }
        right = right/(k+1);
        
        // Two edge cases
        if(k==0)
            return right;
        if(sweetness.length<=k+1)
            return left;
        
        
        // binary search and find the result. 
        while(left<right){
            int middle = left + (right-left)/2, curr = 0, piece = 1;
            for(int sweet: sweetness){
                curr += sweet;
                if(curr > middle){
                    curr = 0;
                    piece ++;
                }
            }
            if(piece > k+1)
                left = middle + 1;
            else
                right = middle;
        }
        return left;
    }
}
```

## [774. Minimize Max Distance to Gas Station](https://leetcode.com/problems/minimize-max-distance-to-gas-station/)

774 可以算作这一个系列里面最难的了.  这道题基本思路没问题, 具体binary search 的实现方式是有问题的, 问题在下面代码的中文注释中. 

```java
class Solution {
    public double minmaxGasDist(int[] stations, int K) {
        double left = 0, right = stations[stations.length - 1] - stations[0];

        while (left +1e-6 < right) {
            // 我不太能理解这个binary search 的写法. 我知道这个1e-6是题目条件来的. 
            // 我也知道这个while loop括号中的意思是为了近似取值. 
            double mid = left + (right - left) / 2;
            int count = 0;
            for (int i = 0; i < stations.length - 1; ++i)
                count += (int)((stations[i + 1] - stations[i]) / mid);
            if (count > K) 
                // 这里, left 和 right都没有增减, 我没想通, 
                // 如果left 和right 没有增减的话, 
                // 如何保证最后left和right能够碰在一起结束这个while loop? 
                // 就是标准写法的话, 肯定要有left和right其中一个有增减的, 不能直接等于mid
                // 如果直接写等于mid的话, 会进入死循环. 
                left = mid;
            else 
                right = mid;
        }
        return left;
    }
}
```


## 问题

- 这个类型的特点是什么?
- 老师能不能帮我总结一下什么时候去要去想到能用binary search解这种题?
- 什么时候没法用binary search, 只能用DP?  或者现在没有时间, 可以放在DP的时候再讲也可以. 
- 774题的 binary search