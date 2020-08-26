---
layout: post
title: Java Syntax
date: 2020-08-25
author: Shadow Walker
tags: [Interview, Algorithm, Java]
toc: true
---


## Overview

总结一下 Java的常用Syntax, 方便查阅和背. 

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
String s = String.valueOf(s);
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

### Int to Char
```java
int a = 65;
char c = (char)a;
```

### List<Integer> to Int[]
```java
int[] array = list.stream().mapToInt(i->i).toArray();
```




## Initilization

### Array
```java
int[] arr = new int[n]; 
int[] arr = {1,2,3};
```

### 2D Array (Matrix)

```java
int[][] multiples = new int[4][2];     // 2D integer array with 4 rows 
                                          and 2 columns
String[][] cities = new String[3][3];  // 2D String array with 3 rows 
                                          and 3 
```

**Traverse**

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

### HashMap
```java
Map<Integer, Integer> map = new HashMap<>();
```

### ArrayList
```java
List<Integer> intArray = new ArrayList<Integer>();

```

### StringBuilder
```java
StringBuilder sb = new StringBuilder();

//init a StringBuilder with capacity of 10. 
StringBuilder sb = new StringBuilder(10);
```

## BuildIn Operation

### String Builder
	> Since the String Class in Java creates an immutable sequence of characters, the StringBuilder class provides an alternative to String Class, as it creates a mutable sequence of characters. 
**Append**<br>
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

### HashMap

**Find max**

```java
int max = Collections.max(set);
int maxKey = Collections.max(map.keySet());
int maxValue Collections.max(map.values());
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

## Length

### String
```java
String.length();
```

### Array
```java
Array.length;
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

### Find max in Array

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