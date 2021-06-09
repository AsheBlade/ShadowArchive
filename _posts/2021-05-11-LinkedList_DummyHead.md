---
layout: post
title: LinkedList DummyHead 换头问题
date: 2021-05-11
author: Shadow Walker
tags: [OPLC, Algorithm, LinkedList]
toc: true
comments: true
---

换头问题是LinkedList基本每一道都会遇见的, 这里总结一下.  关于换头问题, 主要就看LC21, LC24和LC138的笔记, 足够了. 

## Basic LC21

LC21 是换头问题最简单的形式, 简单直观, 一看就懂, 如下:  

换头问题一开始就毫不犹豫把preHead 和 prev写出来(有的人习惯写dummyHead).  preHead是用来保值的, prev是用来赋值的. 最后返回preHead.next. 

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        
        ListNode preHead = new ListNode(-1);
        ListNode prev = preHead;
        
        while(l1!=null && l2!=null){
            if(l1.val>l2.val){
                prev.next = new ListNode(l2.val);
                l2 = l2.next;
            }else{
                prev.next = new ListNode(l1.val);
                l1 = l1.next;
            }
             prev = prev.next;
        }

        if(l1!=null){
            prev.next = l1;
        }else if(l2!=null){
            prev.next = l2;
        }
            
        return preHead.next;
    }
}
```

## 复杂 LC24

LC24是五星必刷题目, 如果LinkedList只刷一道题, 就刷LC24吧. 它的换头本身并不复杂, 其实跟LC21 是一样的. 复杂的是每一个loop都涉及重新映射的转换问题.  LC24的Iteration解法才涉及到换头, Recursion没有换头. 

一句话: **如果LC24能做到Crystal Clear, 换头问题和LinkedList相关基本就通了.**


```java
class Solution {
    public ListNode swapPairs(ListNode head) {

        // Dummy node acts as the prevNode for the head node
        // of the list and hence stores pointer to the head node.
        ListNode dummy = new ListNode(-1);
        dummy.next = head;

        ListNode prevNode = dummy;

        while ((head != null) && (head.next != null)) {

            // Nodes to be swapped
            ListNode firstNode = head;
            ListNode secondNode = head.next;

            // Swapping
            prevNode.next = secondNode;
            firstNode.next = secondNode.next;
            secondNode.next = firstNode;

            // Reinitializing the head and prevNode for next swap
            prevNode = firstNode;
            head = prevNode.next; // jump
        }

        // Return the new head node.
        return dummy.next;
    }
}
```

## 保值 LC138

又一道五星必刷题目. 

LC138比LC24还要复杂一些. LC24是那种你知道应该怎么做, 但是差一点点想不出的题目, LC138是压根没思路.  但LC138的换头处理并不复杂. LC138 的换头要看我自己笔记的最后一个个人答案, 其他答案对换头的应用都不多. 

这里用了两次DummyHead.   为的是traverse这个LinkedList两遍.  LinkedList traverse两遍的问题就是head会到结尾, 没法回到第一个index, 我们这里用DummyHead为head进行保值, 让head能够迅速回去. 

- 第一次DummyHead用于保值, DummyHead.next= head. 这样, 我们把head traverse到结尾的时候, 可以用head = DummyHead.next让head重新回到第一个. 
- 第二次把dummyHead重新清空成new, 然后用之前LC21的常规方法进行最后一次traverse. 

```java
class Solution {
    HashMap<Node, Node> visitedHash = new HashMap<Node, Node>();
    public Node copyRandomList(Node head) {
        
        if(head == null)
            return null;
        
        Node dummyHead = new Node(-1);
        dummyHead.next = head;
        
        //Traverse 两次
        
        // 1. 第一次把每个旧head放进hashmap
        while(head!=null)
        {
            visitedHash.put(head, new Node(head.val));
            head = head.next;
        }
        
        head = dummyHead.next;
        dummyHead = new Node(-1);
        Node output = dummyHead; // 问. 这里为什么不能用output = dummyHead.next, 然后下面用output, 反复尝试这个就是不行.
        
        //2. 第二次用hashmap之中的新copy复制random和next. 
        while(head!=null)
        {
            output.next = visitedHash.get(head);

            if(head.random!=null){
                output.next.random = visitedHash.get(head.random);

            }
            output = output.next;
            head = head.next;
        }
        
        return dummyHead.next;
    }
}
```



