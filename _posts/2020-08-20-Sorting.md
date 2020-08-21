---
layout: post
title: Sorting
date: 2020-08-20
author: Shadow Walker
tags: [Algorithm, Interview]
toc: true
---

## Overview

Sorting 这一块就很搞笑. 学了多少次, 至少学了有3-4次了. 然后名字都知道, 就是记不住, 学了忘,忘了学. 最后就记住insertion和selection.   
这一次全部总结一下, 以后也就不用查了, 直接到这里看. 

## Selection Sort

就是brutal,  两个for loop, 从头到尾刷一遍, 找最小, 塞到第一个, 然后再找最小, 塞到第二个, 以此类推. 

## Insertion Sort

也很brutal, 整个array从头到尾刷一遍, 如果后一个比前一个小, 就用while loop跟上一个比较往前挪, 直到挪到适当的位置为止. 

**Algorithm**

To sort an array of size n in ascending order:  

1. Iterate from arr[1] to arr[n] over the array.
2. Compare the current element (key) to its predecessor.
3. If the key element is smaller than its predecessor, compare it to the elements before. Move the greater elements one position up to make space for the swapped element.

![](https://media.geeksforgeeks.org/wp-content/uploads/insertionsort.png)

**Code**

```java
    void sort(int arr[]) 
    { 
        int n = arr.length; 
        for (int i = 1; i < n; ++i) { 
            int key = arr[i]; 
            int j = i - 1; 
  
            /* Move elements of arr[0..i-1], that are 
               greater than key, to one position ahead 
               of their current position */
            while (j >= 0 && arr[j] > key) { 
                arr[j + 1] = arr[j]; 
                j = j - 1; 
            } 
            arr[j + 1] = key; 
        } 
    } 
```

## Bubble Sort

## Merge Sort

## Quick Sort

