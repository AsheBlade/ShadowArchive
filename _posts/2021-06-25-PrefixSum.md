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

## 437

## 523



