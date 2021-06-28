---
layout: post
title: Java Syntax
date: 2020-08-25
author: Shadow Walker
tags: [Interview, Algorithm, Java, Shortcuts]
toc: true
---


## Overview

总结一下 Java的常用Syntax, 方便查阅和背. 

## lenth/size 用法

- String 用 length()
- Array 用  length (无括号)
- 其他都用 size()

## Conversion

### String to Int

```java
Integer.parseInt(numString);
```

OR
```java
Integer.valueOf(numString);
```

### Int to String
```java
i = 99;
String s = “” + i;
```
Output:
```java
s = “99”
```

OR

```java
String s = String.valueOf(i);
```

### String to Char Array
```java
char[] charArray = str.toCharArray(); 
```

### Char Array to String
```java
String string = new String(charArray);
```

### String to char at certain index
```java
String s="hello";  
char c=s.charAt(0);//returns h  
```

### Char to String
```java
char c = ’s’;
String s = String.valueOf(c);
```

### Object to String
```java
Emp e=new Emp();  
String s=e.toString();  
String s2=String.valueOf(e);  
```

### Char to Int
```java
char c = ‘1’;
int i = Character.getNumericValue(c);  
```

### Char Array to Int

```java
char[] a;
int i = Integer.parseInt(new String(a));
```

### Int to Char
```java
int a = 65;
char c = (char)a;
```

### List<Integer> to Int[]

其实这两种是不应该互相转的.  你会发现有很多奇怪的方法, 比如下面这种, 但其实最快的就是直接traverse一遍, 直接带进去. 这样不会出错, 而且快捷. 

```java
int[] array = list.stream().mapToInt(i->i).toArray();
```

快就是慢, traverse最快, 省事: 

```java
for(int num: nums)
{
	arrayList.add(num);
}
```


## Array

**init**

```java
int[] arr = new int[n]; 
int[] arr = {1,2,3};
```

**Clone**

```java
int[] newArray = oldArray.clone();
```

**2D Array (Matrix)**

```java
int[][] multiples = new int[4][2];     // 2D integer array with 4 rows 
                                          and 2 columns
String[][] cities = new String[3][3];  // 2D String array with 3 rows 
                                          and 3 
```

**Traverse 2D**

```java
int[][] matrix = new int[rows][column];
// Loop through all rows 
for (int i = 0; i < mat.length; i++) 
{    
	// Loop through all elements of current row 
	for (int j = 0; j < mat[i].length; j++) 
	{
		System.out.print(mat[i][j] + " "); 
	}                
}
```


**fill**

fill an array with certain integer

```java
int[] list = new int[100]
Arrays.fill(list, 1);
```

## ArrayList

**Init**

```java
ArrayList<String> list = new ArrayList<>();
```

**Print**

```java
import java.util.*;
int[] i = new int[1];
System.out.println(Arrays.toString(i));
// ArrayList
System.out.println(Arrays.toString(sublist.toArray()));
```

**Swap**

```java
// swap the element at index first and second for list. 
Collections.swap(list, first, second);
```

**Conver to Array**

这个工作中不常见, 刷题却经常需要用到. 因为一些题目输出的array不知道需要多大, 这个时候就需要用到arraylist, 然后最后输出转换成Array. 

```
public static void main(String[] args) 
{
    ArrayList<String> list = new ArrayList<>(2);
    list.add("A");
     
    //Convert to string array
    String[] array = list.toArray(new String[list.size()]);
}
```

**注意!!!! Integer的ArrayList 不能用以上方法转换**

正确的方法: 

```java
int[] array = list.stream().mapToInt(i->i).toArray();
```

虽然很繁琐, 但是, 这是最快的方法. 详见[这里](https://stackoverflow.com/questions/960431/how-to-convert-listinteger-to-int-in-java). 


## Queue

First in, First out. 

### Init

```java
Queue<String> queue = new LinkedList<>();
```
### Method

Insert: `add(e)`  
Remove: `poll()`  remove head  
return: `peek()`  same as `poll()` but does not remove. 

### PriorityQueue
PriorityQueue也被称作heap, 优势是录入自动排序, Sorting神器. 

```java
// init heap 'the smallest element first'
PriorityQueue<Integer> heap = new PriorityQueue<Integer>((n1, n2) -> n1 - n2);
```

heap的三个方法, add,poll, peek和queue完全一样. 

**Complexity**: 把N个element加入一个size为k的heap, T(N) = (Ologk). space complexity: O(k)

## HashMap

### Init

```java
Map<Integer, Integer> map = new HashMap<>();

Map<Character, String> letters = Map.of(
        '2', "abc", '3', "def", '4', "ghi", '5', "jkl", 
        '6', "mno", '7', "pqrs", '8', "tuv", '9', "wxyz");
```



### Clone

```java
Map<Integer, Integer> cloneMap = new HashMap<>(oldMap);
```

### Contain

```java
map.containsKey(Object key)
map.containsValue(Object value)
```

### Put

```java
map.put("vishal", 10);   //for String key, Integer value. 
```

### get/remove

return/remove value based on key. 

```java
map.get(Object key)
map.remove(Object key)
```

### traverse

Both key and value

```java
for (Map.Entry mapElement : hm.entrySet()) { 
    String key = (String)mapElement.getKey(); 
  
    // Add some bonus marks 
    // to all the students and print it 
    int value = ((int)mapElement.getValue() + 10); 
  
    System.out.println(key + " : " + value); 
} 
```

Key: `hm.keySet()`  
Value: `hm.values()`

### Find max

```java
int max = Collections.max(set);
int maxKey = Collections.max(map.keySet());
int maxValue Collections.max(map.values());
```


## Initilization


### HashMap

```java
Map<Integer, Integer> map = new HashMap<>();
```
### Set

```java
Set<String> hash_Set = new HashSet<>(); 
```
### Queue

```java
Queue<String> queue = new LinkedList<>();
```

### Stack

```java
Stack<String> stack = new Stack<>();
```

### StringBuilder

```java
StringBuilder sb = new StringBuilder();

//init a StringBuilder with capacity of 10. 
StringBuilder sb = new StringBuilder(10);

//toString
String s = sb.toString();

//Remove char at certain Index in StringBuilder
sb.deleteCharAt(path.length() - 1);
```

## BuildIn Operation

### String Builder

> Since the String Class in Java creates an immutable sequence of characters, the StringBuilder class provides an alternative to String Class, as it creates a mutable sequence of characters. 

**Append**

combine and add strings together
```java
sb.append(“geek”);
```

**Reverse**<br>
```java
sbReverse = sb.reverse();
```

**To String** <br>
output StringBuilder content to String
```java
String s = sb.toString();
```

### Character

Judge if a character is a digit char. 

```java
Character.isDigit(c)
```

Judge if a character is white space. 

```java
Character.isWhitespace(c)
```

### String

String.substring(a,b). very important in Leetcode. 

- a is start
- b is end + 1

```java
String s = "ab";
System.out.println(s.substring(0,0));
System.out.println(s.substring(0,1));
System.out.println(s.substring(0,2));
```

String.startWith(s). This is used to judge if a String starts with s. 

```java
str.startsWith(s)
```

### Array

**Length**
```java
Array.length;
```

**Print**
```java
System.out.println(Arrays.toString(arr));
```




## Grammar

### For Each Loop
```java
public static int maximum(int[] numbers) 
    {  
        int maxSoFar = numbers[0]; 
          
        // for each loop 
        for (int num : numbers)  
        { 
            if (num > maxSoFar) 
            { 
                maxSoFar = num; 
            } 
        } 
    return maxSoFar; 
    } 
```


## Math

### Absolute value
int abs = Math.abs(i);

### Power
```java
double a = 30;
double b = 2;
Math.pow(a,b);
//output is 900
```

### MAX/MIN Value
Integer upper and lower bond. Use this to prevent overflow. 
```java
Integer.MAX_VALUE 
Integer.MIN_VALUE
```

### Compare MAX/MIN
It's a common technique used in DP. 
```java
int a = Integer.MIN_VALUE;
int b = input value 
int output = Math.max(a, b);
```

### Integer to Binary

Yes you will get a String, but this is the only way. You can always convert it back to integer. It is up to you. 

```java
String s = Integer.toBinaryString(n);
```

### Random

这一块例子可以参考LC380 和 LC384. 

```java
Random random = new Random();
int j = random.nextInt(high);  // generate random int between 0 and high (exclude high);
int i = random.nextInt(high-low) + low;  // get random int between low and high (exclude high);
```

## Length

### String
```java
String.length();
```


## Sorting

### Sort Array
```java
int[] list = {3,2,4,1};
Arrays.sort(list);

for (int num: list)
{
    System.out.print(num);
}
```

### Find average in Array

```java
double[] arr = {19, 12.89, 16.5, 200, 13.7};
double total = 0;

for(int i=0; i<arr.length; i++){
	total = total + arr[i];
}


/* arr.length returns the number of elements 
 * present in the array
 */
double average = total / arr.length;
    
/* This is used for displaying the formatted output
 * if you give %.4f then the output would have 4 digits
 * after decimal point.
 */
System.out.format("The average is: %.3f", average);
```

## Inner class

```java
public class Test {
    public static void main(String[] args) {
        A a = new A(
        System.out.println(a.getValue());
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