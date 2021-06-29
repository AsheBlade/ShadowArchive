---
layout: post
title: Prefix Sum
date: 2021-06-25
author: Shadow Walker
tags: [Algorithm, Interview]
toc: true
---

304，1314，523

## 560. Subarray Sum Equals K

Prefix 最经典最基础的一道题目. 可以作为模板. 这个模板是反复推敲过的, 一行不多, 一行不少. 简单易读. 

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> hm = new HashMap<>();
        int sum = 0, count = 0; 
        hm.put(0,1);
        for(int num: nums){
            sum += num;
            count += hm.getOrDefault(sum-k, 0);
            hm.put(sum, hm.getOrDefault(sum,0) + 1);
        }
        return count;
    }
}
```

## 1248. Count Number of Nice Subarrays

另一道基本的Prefix Sum, 就不放代码了, 代码可以参照上面560. 只不过需要动动脑筋去思考sum的东西为何物. 


## 974. Subarray Sums Divisible by K

本质上跟560没有区别, 难点在于如何用数学去处理余数问题. 余数是不满足乘法交换律的, 要处理负数的问题. 除了数学之外跟560没有区别, 没必要反复刷. 

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        Map<Integer, Integer> hm = new HashMap<>();
        hm.put(0,1);
        int sum = 0, output = 0;
        for(int num: nums){
            sum = (sum + num) %k;
            if(sum < 0) sum += k;
            output+=hm.getOrDefault(sum%k, 0);
            hm.put(sum%k, hm.getOrDefault(sum%k,0)+1);
        }
        return output;
    }
}
```

## 325. Maximum Size Subarray Sum Equals k

一开始以为跟560是一样的, 其实不然, 是需要记录起点的一道题. 值得一提的是, 记录起点的题目, 一开始要放(0,-1). 不过一刷也过了. 

```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        Map<Integer, Integer> hm = new HashMap<>();
        int max = 0, sum = 0;
        hm.put(0, -1);
        for(int i=0; i<nums.length; i++){
            sum += nums[i];
            if(hm.containsKey(sum-k)){
                int index = hm.get(sum-k);
                max = Math.max(max, i-index);
            }
            if(hm.containsKey(sum)){
                int minIndex = Math.min(hm.get(sum),i);
                hm.put(sum,minIndex);
            }else{
                hm.put(sum,i);
            }
        }
        return max;
    }
}
```

## 304. Range Sum Query 2D - Immutable

304 是一道非常典型的matrix prefix sum.  关键在于最上面的公式, 如何用prefix sum去计算每一个点的sum, 记住这个公式之后其他就迎刃而解了.  

```java
class NumMatrix {
    
    // sum[x][y] = num[x][y] + sum[x-1][y] + sum[x][y-1] - sum[x-1][y-1]
    
    int[][] sum;
    public NumMatrix(int[][] matrix) {
        sum = new int[matrix.length][matrix[0].length];
        sum[0][0] = matrix[0][0];
        
        for(int i=1; i<matrix.length; i++){
            sum[i][0] = sum[i-1][0] + matrix[i][0];
        }
        for(int i=1; i<matrix[0].length; i++){
            sum[0][i] = sum[0][i-1] + matrix[0][i];
        }

        for(int i=1; i<matrix.length; i++){
            for(int j=1; j<matrix[0].length; j++){
                sum[i][j] = matrix[i][j] + sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1];
            }
        }
    }
    
    public int sumRegion(int row1, int col1, int row2, int col2) {
        int wholeRegion = sum[row2][col2];
        int rightRegion = 0, leftRegion=0, minusRegion = 0;
        if(row1!=0)
            rightRegion = sum[row1-1][col2];
        if(col1!=0)
            leftRegion = sum[row2][col1-1];
        if(row1!=0 && col1!=0)
            minusRegion = sum[row1-1][col1-1];
        
        return wholeRegion - rightRegion - leftRegion + minusRegion;
    }
}
```

## 437

## 523



