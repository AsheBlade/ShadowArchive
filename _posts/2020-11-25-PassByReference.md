---
layout: post
title: Pass by Reference in Java
date: 2020-11-25
author: Shadow Walker
tags: [Java]
toc: true
comments: true
---

## 前面

Java 存在 Pass-by-Reference这个问题. 总结其实就一句话: **Primitive types pass by value, others pass by reference.**

下面试验几种, 可以看到Int 和 String都是pass by value不会改变原值.  值得注意的是, **Array 特别, 不属于primitive, pass-by-reference.**. Array 和其他的util type, hashmap, queue, 还有各种自定义objective都会被method改变值. 

## Integer


```java
public static void main(String[] args) {
    int i = 0;
    changeValue(i);
    System.out.println(i);
}

private static void changeValue(int i)
{
    i = 2;
}
```

**Output**

```java
0
```

## String

```java
public class Test {
    public static void main(String[] args) {
        String s = "a";
        changeValue(s);
        System.out.println(s);
    }

    private static void changeValue(String s)
    {
        s = "b";
    }
}
```

**Output**

```java
a
```
## Object

```java
public class Test {
    public static void main(String[] args) {
        A a = new A(1);
        changeValue(a);
        System.out.println(a.getValue());
    }

    private static void changeValue(A a)
    {
        a.setValue(2);
    }

    private static class A{
        int value;
        public A(int value){
            this.value = value;
        }
        public void setValue(int value){
            this.value = value;
        }
        public int getValue(){
            return value;
        }
    }
}
```

**Output**

```java
2
```
## Array

```java
import java.util.*;

public class Test {
    public static void main(String[] args) {
        int[] i = new int[1];
        i[0] = 1;
        changeValue(i);
        System.out.println(Arrays.toString(i));
    }

    private static void changeValue(int[] i)
    {
        i[0] = 3;
    }
}
```
**Output**

```java
[3]
```

## Queue

```java
import java.util.*; 
public class Test {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(1);
        queue.add(2);
        changeValue(queue);
        System.out.println(queue.poll());
    }

    private static void changeValue(Queue<Integer> queue)
    {
        int i = queue.poll();
    }
}
```

**Output**

```java
2
```


    
    