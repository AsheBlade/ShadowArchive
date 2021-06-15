---
layout: post
title: Next Greater Element
date: 2021-06-14
author: Shadow Walker
tags: [OPLC, HashMap, LinkedList, Stack]
toc: true
---

这是一个类型, 因为涉及的比较多, 特此总结一下, 核心是496题但太简单被后面覆盖了, 最好的题目就是1019题, 做这一道就够了.   556题的思路跟其他都不一样, 其实是另一道题. 

## 496. Next Greater Element I

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Stack<Integer> stack = new Stack<>();
        Map<Integer, Integer> hm = new HashMap<>();
        int[] output = new int[nums1.length];
        for(int i=0; i<nums2.length; i++){
            while(!stack.isEmpty() && nums2[i]>stack.peek()){
                hm.put(stack.pop(), nums2[i]);
            }
            stack.add(nums2[i]);
        }
        while(!stack.isEmpty()){
            hm.put(stack.pop(), -1);
        }
        int index = 0;
        for(int num: nums1){
            output[index++] = hm.get(num);
        }
        return output;
    }
}
```


## 1019. Next Greater Node In Linked List

```java
class Solution {
    public int[] nextLargerNodes(ListNode head) {
        if(head == null)
            return new int[]{};
        
        Map<Integer,Integer> hm = new HashMap<>();
        Stack<int[]> stack = new Stack<>();
        int index = 0;
        while(head!=null){
            while(!stack.isEmpty() && head.val>stack.peek()[1]){
                hm.put(stack.pop()[0], head.val);
            }
            stack.add(new int[]{index++, head.val});
            head = head.next;
        }
        while(!stack.isEmpty()){
            hm.put(stack.pop()[0], 0);
        }
        int[] output = new int[hm.size()];
        for(int i=0; i<hm.size(); i++){
            output[i] = hm.get(i);
        }
        return output;
    }
}
```
## 503. Next Greater Element II

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        Map<Integer, Integer> hm = new HashMap<>();
        Stack<int[]> stack = new Stack<>();
        int[] output = new int[nums.length];
        for(int i=0; i<nums.length; i++){
            while(!stack.isEmpty() && nums[i]>stack.peek()[1]){
                hm.put(stack.pop()[0], nums[i]);
            }
            stack.add(new int[]{i,nums[i]});
        }
        for(int i=0; i<nums.length && !stack.isEmpty(); i++){
            while(!stack.isEmpty() && nums[i]>stack.peek()[1]){
                hm.put(stack.pop()[0], nums[i]);
            }
        }
        while(!stack.isEmpty()){
            hm.put(stack.pop()[0], -1);
        }
        for(int i=0; i<output.length; i++){
            output[i] = hm.get(i);
        }
        return output;
    }
}
```


## 556. Next Greater Element III

```java

public class Solution {
    public int nextGreaterElement(int n) {
        char[] a = ("" + n).toCharArray();
        int i = a.length - 2;
        while (i >= 0 && a[i + 1] <= a[i]) {
            i--;
        }
        if (i < 0)
            return -1;
        int j = a.length - 1;
        while (j >= 0 && a[j] <= a[i]) {
            j--;
        }
        swap(a, i, j);
        reverse(a, i + 1);
        try {
            return Integer.parseInt(new String(a));
        } catch (Exception e) {
            return -1;
        }
    }
    private void reverse(char[] a, int start) {
        int i = start, j = a.length - 1;
        while (i < j) {
            swap(a, i, j);
            i++;
            j--;
        }
    }
    private void swap(char[] a, int i, int j) {
        char temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
}
```