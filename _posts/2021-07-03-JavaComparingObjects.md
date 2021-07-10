---
layout: post
title: Java Comparing Objects
date: 2021-07-03
author: Shadow Walker
tags: [Java]
toc: true
---

## Overview

记一下Java 比较 object的方式. 因为经常能用到. 

```java
Node dummyHead = new Node(-1);
Node prev = dummyHead;
prev.equals(dummyHead);   True // Object class 的default 只比较地址, 不比较值. 
prev == dummyHead;  True // Object class 的default 跟上面这一行是一样的. 
```

- 地址一样, Object class 的default hashcode 就一样. 
- Object class equal 的 default比较方法只是比较hashcode, 没有任何其他的比较. 如果需要比较其他是需要重写的. 

## 138. Copy List with Random Pointer

这里就涉及到著名的138题. 其中prev.next = hm.get(head), 这里的hm.get是直接比较的地址. 

如下我们在138题下面加入以下方法, 即便我们改变n1的值, n1的reference还是不变的, 所以两次打印的结果都是n1原来的value.

不过尽管如此, 不建议把mutable value作为hashmap的key, 建议用unmutable value, 也就是primitive values. 

```java
private void test(){
    Node n1 = new Node(1);
    Map<Node, String> hm = new HashMap<>();
    hm.put(n1, "n1 node");
    System.out.println(hm.get(n1));    // “n1 node”
    n1.val = 10;
    System.out.println(hm.get(n1));  //  “n1 node”
}
```


