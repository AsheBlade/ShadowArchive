---
layout: post
title: Java Interview Question By Parts
date: 2020-07-28
author: Shadow Walker
tags: [JAVA]
comments: true
toc: true
---

**原则说明**  
此文档存在的价值在于迅速检索有关Java的面试题, 应该录入知识要点, 不应讨论过分详尽信息. 详尽信息应另开文档. 


## Topics
**Concepts from core Java:**

* OOPS concepts (Data Abstraction, Encapsulation, Inheritance, Polymorphism)
* Basic Java constructs like loops and data types
* String handling
* Collection framework
* Multithreading
* Exception handling
* Generics
* Synchronisation
* Serialisation & De-serialisation
* Concurrent collection

**Advanced Java:**

* JDBC (Java Database Connectivity)
* Servlet
* JSP

**Popular Frameworks:**

* Spring (MVC, Core, JDBC, ORM, AOP)
* Hibernate ORM framework
* Struts
* JSF
* Web Services (SOAP & REST)

**Other:**

* Design patterns and design questions related to your projects.


## Stupid Why Questions

### Why MicroService
[Why MicroService](https://shadow-soft.com/why-microservice-architecture/)

---
<br><br>

### Why Lambda Expression

[Why Lambda Expressio](https://www.programcreek.com/2014/01/why-lambda-java-8/)

---
<br><br>

### Why Stream? What is the benefit of Stream? 

- Streams have a strong affinity with functions. 
- Streams encourage less mutability.
- Streams encourage looser coupling. 
- Streams can succinctly express quite sophisticated behaviour.
- Streams provide scope for future efficiency gains. 

---
<br><br>

### Why Spring? Advantage of Spring?

* **Spring is non invasive:** That means you no need to implements any interface or inherit any class from spring to your classes, so when ever you want to change from spring to any other technology then you no need to change the logics of your class.

* **Spring is light weight:** Spring is vast framework so spring people divide the whole spring in to different modules, they are designed in such a way that no module is dependent to other module , excep Spring core module, so accordingxto your requirement you can learn a particular module, you no need to learn whole total framework

* **.End to end Development:** Spring supports all aspects of application development, Business aspects, persistence aspects, etc, so we can develop a complete application using spring.

* **Spring supports All types of application development:** We can develop any type of applications using spring, eg: Core java, web Application, Distributed application, Enterprise application.

* **Spring is versatile:** We can integrate any technologies with spring , so we can say spring is versatile,

* **Spring supports dependency injection:** The dependency between classes are managed by spring .

* **Spring provides different modules** to achieve different services and functionality for development of application , some popular modules are:

	* Spring core.(Base module)
	* Spring JDBC(for persistence logic)
	* Spring AOP(for cross context logic)
	* Spring Transaction(For transaction support)
	* Spring ORM.
	* Spring MVC(Web aspect)

---
<br><br>


### Why Jenkins? Benefit? 

- Jenkins can automate the build process (Compile, Static Code analysis, Archiving)

---
<br><br>


### Why Spring Boot? Advantage of Spring Boot

---
<br><br>

---
<br><br>

---
<br><br>

---
<br><br>
## Pre

### Example

**Q1.**

A.  

For example:

```java

```
Output:

```java

```

------
<br><br>

### String

**Q1. What is the difference between “==” and “equals(…)” in comparing Java String objects?**

A. When you use “==” (i.e. shallow comparison), you are actually **comparing the two object references** to see if they point to the same object. When you use “equals(…)”, which is a “deep comparison” that **compares the actual string values**. 

For example:

```java
public class Player {
    public static void main(String[] args)  {
       //Singleton si = Singleton.getInstance();

        String s1 = "hello";
        String s2 = "hello";

        String s3 = new String("hello");
        String s4 = new String("hello");


        System.out.println(s1 == s2);
        System.out.println(s3 == s4);
        System.out.println(s3.equals(s4));
    }
}
```
Output:~

```java
true
false
true
```

------
<br><br>

**Q2.String vs StringBuffer vs StringBuilder**
- String
	1. String is immutable and final.
	2. Every time you try to modify a string, you create a new string. 
		By this way, you create lots of String garbages. 
- StringBufer
	1. StringBuffer is mutable. 
	2. You can modify a Stringbuffer without creating new objects. 
- StringBuffer vs StringBuilder

	StringBuffer | StringBuilder 
	---| ---- 
	Thread safe | Not thread safe
	Synchronized | Not synchronized
	Slower than StringBuilder | Faster than StringBuffer


### boolean
**Q1: Default value of boolean?**

A: false

For example:

```java
public class Player {
    static boolean bo;
    public static void main(String[] args)  {
        System.out.println(bo);
    }
}
```
Output:

```java
false
```
------
<br><br>

### Static
**Q1: What is static in Java?**

The static keyword in java is used for memory management mainly. We can apply java static keyword with variables, methods, blocks and nested class. The static keyword belongs to the class than instance of the class.

The static can be:

* variable (also known as class variable)
* method (also known as class method)
* block
* nested class

---
<br><br>

**Q2: What is static block?**

A static block helps to initialize the static data members, just like constructors help to initialize instance members. 

Example:
```java
public class Demo {
	 static int a;
	 static int b;
	 static {
	    a = 10;
	    b = 20;
	 }
 }
```

---
<br><br>

**Can we use static block to throw exceptions?**

Yes, static block can throw only Runtime exception or can use a try-catch block to catch checked exception.

---
<br><br>

### Abstract
**Q1: Difference between abstract class and interface**
- Abstract Class:

	- Abstract classes have a default constructor and it is called whenever the concrete subclass is instantiated. But, still you cannot initilize an abstract class. 
	- Contains Abstract methods as well as Non-Abstract methods.
	- The class which extends the Abstract class shouldn’t require implementing all the methods, only Abstract methods need to be implemented in the concrete sub-class.
	- Abstract Class contains instance variables (not static).
<br><br>

- Interface:

	- Doesn’t have any constructor and couldn’t be instantiated.
	- Abstract method alone should be declared.
	- Classes which implement the interface should provide the implementation for all the methods.
	- All variables in interface are public static final variables by default. 

---
<br><br>


**Q2: How to change abstract class value without using set method. Real Apple question**

```java
abstract class AB1{
    private static int i;

    public AB1(int i) {
        this.i = i;
    }

    public static int getI() {
        return i;
    }
}

class Player extends AB1 {

    Player(int i){
        super(i);
    }
    public static void main(String[] a) {
// implement the code

        Player p = new Player(10);
        System.out.println("i="+ getI());
    }
}
```

---
<br><br>


The interface contains only constants.

------

<br><br>

### Encapsulation

Map<Integer, Integer> map = new HashMap<>();

------
<br><br>

### Polymorphism
**Q2:What is Polymorphism**

Simple:

- Overloading = static binding
- Overriding = dynamic binding

------
<br><br>
**Q2:Why Polymorphism**

Definition: Parent reference refer to Child's Object or interface reference refer to its implementation instance <br>
Advantage:  <br>
- faster program development <br>
- better code organization <br>
- extensible programs -> decouple what from how <br>
- easier code maintenance <br>

------
<br><br>

**Q3: Is @Override necessary when using overriding?**

NO. You don't have to @Override. @Override is to ensure that the method is overriding, otherwise it doesn't compile. 

------
<br><br>

### Package

### Array

**Q1. Array vs List**

- In general (and in Java) an array is a data structure generally consisting of sequential memory storing a collection of objects.

- List is an interface in Java, which means that it may have multiple implementations. One of these implementations is ArrayList, which is a class that implements the behavior of the List interface using arrays as the data structure.

------
<br><br>

### Wrapper
**Q1. What are wrapper classes in Java?**

Wrapper classes convert the Java primitives into the reference types (objects). Every primitive data type has a class dedicated to it. These are known as wrapper classes because they “wrap” the primitive data type into an object of that class.

Example:
```java
// Convert an int value to an Integer object
Integer object = new Integer(1);
 
Integer anotherObject = Integer.valueOf(1);
```

Primitive Data Type | Wrapper Class
---|---
char | Character
byte | Byte
short | Short
long | Integer
float | Float
double | Double
boolean | Boolean

------
<br><br>

### Java

**java 7 new feature**
	
- multi-catch with one try

**java 8 new feature**
	
- Lambda Expression
- Stream
- predicate
	
**java 9 new feature**
	
- Factory Methods for Immutable List, Set, Map and Map.Entry
- Private methods in Interfaces

**java 11 new feature**
	
- no longer needs javac. Can run java and it will auto compile. 
- var in lambda expression.
- Reading and Writing Strings to and from the Files
	
- Example:
	
	```java
	Path path = Files.writeString(Files.createTempFile("test", ".txt"), "This was posted on JD");
	System.out.println(path);
	String s = Files.readString(path);
	System.out.println(s); //This was posted on JD
	```
	
**java 12 new feature**

- File.mismatch
- Compact Number Formatting
- Teeing Collectors in Stream API
- Java Strings New Methods – indent(), transform(), describeConstable(), and resolveConstantDesc()

---
<br><br>

**Advantage of Java**

- Simple
	- Java is straightforward to use, write, compile, debug, and learn than alternative programming languages. Java is less complicated than C++; as a result, Java uses automatic memory allocation and garbage collection.

- Object-Oriented
	- It permits you to form standard programs and reusable code.

- Platform-Independent
	- Java code runs on any machine that doesn’t need any special software to be installed, but the JVM needs to be present on the machine.

- Distributed computing
	- Distributed computing involves several computers on a network working together. It helps in developing applications on networks that can contribute to both data and application functionality.

- Secure
	- Java has no explicit pointer. Apart from this, it has a security manager that defines the access of classes.

- Memory allocation
	- In Java, memory is divided into two parts one is heap and another is stack. Whenever we declare a variable JVM gives memory from either stack or heap space. It helps to keep the information and restore it easily.

- Multithreaded
	- It has the potential for a program to perform many tasks at the same time.



---
<br><br>


**Disadvantage of Java**

- Performance
	-Java is memory-consuming and significantly slower than natively compiled languages such as C or C++.

- Look and Feel
	- The default look of GUI applications written in Java using the Swing toolkit is very different from native applications.

- Single-Paradigm Language
	- Static imports were added in Java 5.0. The procedural paradigm is better accommodated than in earlier versions of Java.

- Memory Management
	- In Java, Memory is managed through garbage collection, whenever the garbage collector runs, it affects the performance of the application. This is because all other threads in the have to be stopped to allow the garbage collector thread to work.

---
<br><br>



## Unclassifed
**Q1. Difference between break and continue**
break | continue
---| ---
can be used in switch and loop(for, while, do while) statemenets| can be only used with loop statemenets
casues the switch or loop to terminate | doesn’t terminate loop but causes the loop to jump to the next iteration
---
<br><br>
**Q2. Can you override a private or static method in java?**

No you cannot

---
<br><br>
**Q3. Why is main method public static and void in Java? Will the program compile, if the main method is not static?**

Java program's main method has to be declared static because keyword static allows main to be called without creating an object of the class in which the main method is defined. If we omit static keyword before main Java program will successfully compile but it won't execute.

---
<br><br>
**Q4. What is Java Serverlet**

Servlets are Java classes which service HTTP requests and implement the javax.servlet.Servlet interface. Web application developers typically write servlets that extend javax.servlet.http.HttpServlet, an abstract class that implements the Servlet interface and is specially designed to handle HTTP request

Sample Code:
```java
// Import required java libraries
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

// Extend HttpServlet class
public class HelloWorld extends HttpServlet {
 
   private String message;

   public void init() throws ServletException {
      // Do required initialization
      message = "Hello World";
   }

   public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException {
      
      // Set response content type
      response.setContentType("text/html");

      // Actual logic goes here.
      PrintWriter out = response.getWriter();
      out.println("<h1>" + message + "</h1>");
   }

   public void destroy() {
      // do nothing.
   }
}
```

---
<br><br>
**Q5. what is Object Oriented Programming (OOPs) Concept in Java**

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190717114649/Object-Oriented-Programming-Concepts.jpg)

---
<br><br>

## Collection

<br>
<p align="center">
<img width="680" src="https://media.geeksforgeeks.org/wp-content/uploads/java-collection.jpg" />
</p>
<br><br>


**Q1. Difference between Comparable and Comparator**

a.compareTo(b) | compare(a,b)
---|---
Comparable Interface | Comparator Interface
compare same object | compare two different objects
Use for String, wrapper classes, BigInteger | Use for TreeMap and TreeSets
 

- a.compareTo(b)
	- Comparable is meant for objects with natural ordering which means the object itself must know how it is to be ordered. For example Roll Numbers of students. Whereas, Comparator interface sorting is done through a separate class
	- If any class implements Comparable interface in Java then collection of that object either List or Array can be sorted automatically by using Collections.sort() or Arrays.sort() method and objects will be sorted based on there natural order defined by CompareTo method.

- compare(a,b)
	- sort() method invokes the compare() to sort objects. 
	- to sort a Person class by name, ID, age, height, ... You would define a Comparator(compare) for each of these to pass to the sort() method.

**To summarize, if sorting of objects needs to be based on natural order then use Comparable whereas if you sorting needs to be done on attributes of different objects, then use Comparator in Java.**


	
**Comparable Example:** 
```java
// A Java program to demonstrate use of Comparable 
import java.io.*; 
import java.util.*; 

// A class 'Movie' that implements Comparable 
class Movie implements Comparable<Movie> 
{ 
	private double rating; 
	private String name; 
	private int year; 

	// Used to sort movies by year 
	public int compareTo(Movie m) 
	{ 
		return this.year - m.year; 
	} 

	// Constructor 
	public Movie(String nm, double rt, int yr) 
	{ 
		this.name = nm; 
		this.rating = rt; 
		this.year = yr; 
	} 

	// Getter methods for accessing private data 
	public double getRating() { return rating; } 
	public String getName() { return name; } 
	public int getYear()	 { return year; } 
} 

// Driver class 
class Main 
{ 
	public static void main(String[] args) 
	{ 
		ArrayList<Movie> list = new ArrayList<Movie>(); 
		list.add(new Movie("Force Awakens", 8.3, 2015)); 
		list.add(new Movie("Star Wars", 8.7, 1977)); 
		list.add(new Movie("Empire Strikes Back", 8.8, 1980)); 
		list.add(new Movie("Return of the Jedi", 8.4, 1983)); 

		Collections.sort(list); 

		System.out.println("Movies after sorting : "); 
		for (Movie movie: list) 
		{ 
			System.out.println(movie.getName() + " " + 
							movie.getRating() + " " + 
							movie.getYear()); 
		} 
	} 
} 
```
**Comparator Example:**
```java
//A Java program to demonstrate Comparator interface 
import java.io.*; 
import java.util.*; 

// A class 'Movie' that implements Comparable 
class Movie implements Comparable<Movie> 
{ 
	private double rating; 
	private String name; 
	private int year; 

	// Used to sort movies by year 
	public int compareTo(Movie m) 
	{ 
		return this.year - m.year; 
	} 

	// Constructor 
	public Movie(String nm, double rt, int yr) 
	{ 
		this.name = nm; 
		this.rating = rt; 
		this.year = yr; 
	} 

	// Getter methods for accessing private data 
	public double getRating() { return rating; } 
	public String getName() { return name; } 
	public int getYear()	 { return year; } 
} 

// Class to compare Movies by ratings 
class RatingCompare implements Comparator<Movie> 
{ 
	public int compare(Movie m1, Movie m2) 
	{ 
		if (m1.getRating() < m2.getRating()) return -1; 
		if (m1.getRating() > m2.getRating()) return 1; 
		else return 0; 
	} 
} 

// Class to compare Movies by name 
class NameCompare implements Comparator<Movie> 
{ 
	public int compare(Movie m1, Movie m2) 
	{ 
		return m1.getName().compareTo(m2.getName()); 
	} 
} 

// Driver class 
class Main 
{ 
	public static void main(String[] args) 
	{ 
		ArrayList<Movie> list = new ArrayList<Movie>(); 
		list.add(new Movie("Force Awakens", 8.3, 2015)); 
		list.add(new Movie("Star Wars", 8.7, 1977)); 
		list.add(new Movie("Empire Strikes Back", 8.8, 1980)); 
		list.add(new Movie("Return of the Jedi", 8.4, 1983)); 

		// Sort by rating : (1) Create an object of ratingCompare 
		//				 (2) Call Collections.sort 
		//				 (3) Print Sorted list 
		System.out.println("Sorted by rating"); 
		RatingCompare ratingCompare = new RatingCompare(); 
		Collections.sort(list, ratingCompare); 
		for (Movie movie: list) 
			System.out.println(movie.getRating() + " " + 
							movie.getName() + " " + 
							movie.getYear()); 


		// Call overloaded sort method with RatingCompare 
		// (Same three steps as above) 
		System.out.println("\nSorted by name"); 
		NameCompare nameCompare = new NameCompare(); 
		Collections.sort(list, nameCompare); 
		for (Movie movie: list) 
			System.out.println(movie.getName() + " " + 
							movie.getRating() + " " + 
							movie.getYear()); 

		// Uses Comparable to sort by year 
		System.out.println("\nSorted by year"); 
		Collections.sort(list); 
		for (Movie movie: list) 
			System.out.println(movie.getYear() + " " + 
							movie.getRating() + " " + 
							movie.getName()+" "); 
	} 
} 
```
---
<br><br>


### ArrayList

**Q1: Difference Between Arraylist and array** 
 
- Array must be same elements. <br>
- Array's size is set when initilized. 

**Q2: What is the internal implementation of ArrayList**  

ArrayList inherits AbstractList class and implements List interface.

**Q3: Two ways to iterate over an ArrayList**

1. Looping using Java5 foreach loop.
2. Looping ArrayList using for loop and size() method.
3. Iterating ArrayList using Iterator.
4. Traversing ArrayList using ListIterator in Java.

------

### LinkedList

### Queue

1. Queue is an interface like List. 
2. Queue is **first in first out**.
3. You can init a Queue using either LinkedList or PriorityQueue, such as: 

	```java
	Queue<Obj> queue = new PriorityQueue<Obj> ();
	Queue<Obj> queue = new LinkedList<>();
	```
4. [More operation about Queue from GeeksforGeeks](https://www.geeksforgeeks.org/queue-interface-java/?ref=lbp)

### PriorityQueue

1. A PriorityQueue is used when the objects are supposed to be processed **based on the priority**. 
2. PriorityQueue doesn’t permit null.
3. We can’t create PriorityQueue of Objects that are non-comparable
4. Basically, **when we add() into PriorityQueue, we will compare first and then add**. 
5. [More operation about PriorityQueue from GeeksforGeeks](https://www.geeksforgeeks.org/priority-queue-class-in-java-2/)

### Set


### Iterator

### TreeSet
**Q1: Difference between HashSet and TreeSet**

HashSet	| TreeSet
---|---
Inserted elements are in random order	| Maintains the elements in the sorted order
Can able to store null objects	| Couldn’t store null objects
Performance is fast |	Performance is slow
---
<br><br>
### Map
**Q1: Difference between hashcode and equals**

**hashcode is only used in hashset, hashtable, hashmap.**. It's not used in linkedlist/Array. 
why hashcode?  Because it's more efficient. 

equal compares memory address. 

hashcode 用于去重,更快. 如果hashcode不同, 两者一定不同. 
equal 更慢, 依靠算法. 如果equal不同, 二者有可能相同. 
算法里最快的是hash

用于add方法, 去检测hash collection之中是否已经包含此元素. 
先用hashcode比较, 如果hashcode不同就肯定不同. 直接加进去.  如果hashcode相同, 再比较equal进一步确认是否一样. 

---
<br><br>
**Q2: Difference between HashMap and HashTable**

HashMap|	HashTable
---|---
Methods are not synchronized	| Key methods are synchronized
Not thread safety	| Thread safety
Iterator is used to iterate the values	| Enumerator is used to iterate the values
Allows one null key and multiple null values	| Doesn’t allow anything that is null
Performance is high than HashTable	| Performance is slow
<br>*Both allow duplicate value but not duplicate key.*
<br><br>
Example:
```java
// A sample Java program to demonstrate HashMap and HashTable 
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class has to be "Main" only if the class is public. */
class Player
{
    public static void main(String args[])
    {
        //----------hashtable ------------------------- 
        Hashtable<Integer,String> ht=new Hashtable<Integer,String>();
        ht.put(100,"Amit");
        ht.put(100,"Vmit");
        ht.put(104,"Amit");
        ht.put(101,"Vijay");
        ht.put(102,"Rahul");
        System.out.println("-------------Hash table--------------");
        for (Map.Entry m:ht.entrySet()) {
            System.out.println(m.getKey()+" "+m.getValue());
        }

        //----------------hashmap-------------------------------- 
        HashMap<Integer,String> hm=new HashMap<Integer,String>();
        hm.put(100,"Amit");
        hm.put(100,"Vmit");
        hm.put(104,"Amit");  // hash map allows duplicate values 
        hm.put(101,"Vijay");
        hm.put(102,"Rahul");
        System.out.println("-----------Hash map-----------");
        for (Map.Entry m:hm.entrySet()) {
            System.out.println(m.getKey()+" "+m.getValue());
        }
    }
} 
```
Output:
```java
-------------Hash table--------------
104 Amit
102 Rahul
101 Vijay
100 Vmit
-----------Hash map-----------
100 Vmit
101 Vijay
102 Rahul
104 Amit
```
---
<br><br>

**HashMap vs TreeMap**

HashMap | TreeMap
--- | ---
unsorted | sorted
implement Hasing | implements Red-Black Tree
Time Complexity O(n) | Time Complexity O(log n)


---
<br><br>


## High Level

### Predicate

**What is predicate in Java?**

- [GeeksforGeeks Java Predicate](https://www.geeksforgeeks.org/java-8-predicate-with-examples/)
- New feature in Java 8. 
- A Functional Interface is an Interface which allows only one Abstract method within the Interface scope. 
- There are some predefined functional interface in Java like Predicate, consumer, supplier etc. The return type of a Lambda function (introduced in JDK 1.8) is a also functional interface.

---
<br><br>



### Generics

### args

### Enum

### Annotation

### Reflection

### Java EE 6 Interceptor

- [The interceptor Example Application](https://javaee.github.io/tutorial/interceptors003.html)
- [Overview of Interceptors](https://docs.oracle.com/javaee/6/tutorial/doc/gkigq.html)


## Exception

**Q1.Difference between final, finally and finalize.**

1. final variable cannot be changed. final class cannot be extend. final method cannot be overrided. 
2. ‘finally‘ is used in a try/catch statement to almost always execute the code. finally block will run whatever exception throwed out or not finalize 
3. ‘finalize‘ is called when an object is garbage collected. You rarely need to override it.

------
<br><br>

**Clean up unused objecs in Java.**

- [How to clean up unused objects in java](http://journals.ecs.soton.ac.uk/java/tutorial/java/javaOO/garbagecollection.html)

------
<br><br>

**Q2.Difference between throws and throw**

throws is after method name.  throw is inside the method.  
```java
public void methodName() throws Exception {
	System.out.println(“exception is typical implementation of inheritance”);
	throw new Exception();
}
```
------
<br><br>
**Q3. What are the types of Exceptions?**

- Checked Exception
	- checked by the compiler at the time of compilation.
	- e.g. ClassNotFound Exception
<br><br>
- Unchecked Exception
	- are not checked during the compile time by the compiler. 
	- e.g. Arithmetic Exception, ArrayIndexOutOfBounds Exception. 
	
------
<br><br>

**Q4. What are different ways to handle exceptions?**

- try/catch:
```java
class Manipulation {
 public static void main(String[] args) {
  add();
 }
 Public void add() {
  try {
   addition();
  } catch (Exception e) {
   e.printStacktrace();
  }
 }
}
```
- throws:
```java
class Manipulation {
 public static void main(String[] args) {
  add();
 }
 public void add() throws Exception {
  addition();
 }
}
```
------
<br><br>

**Q5. Error vs Exception**

Errors	| Exceptions
---|---
Errors in java are of type java.lang.Error. | Exceptions in java are of type java.lang.Exception.
All errors in java are unchecked type.	| Exceptions include both checked as well as unchecked type.
Errors happen at run time. They will not be known to compiler. | Checked exceptions are known to compiler where as unchecked exceptions are not known to compiler because they occur at run time.
It is impossible to recover from errors. | You can recover from exceptions by handling them through try-catch blocks.

------
<br><br>

**Q6. What is Multi-Catch?**

New feature introduced in java 7. Alows one catch with multiple catches. s

------
<br><br>

**Q7. What is the parent calss of Exception?**

- Throwable

![](https://www.manishsanger.com/wp-content/uploads/2018/03/Exception-Hierarchy.png)

------
<br><br>

**Can you extend throwable in your exception class?** 

Fundamentally you should extends Exception class as you are creating Custom Exception. Exception and Error both extends Throwable, It really does not make sense extending Throwable.

------
<br><br>

**How to create custom exception class?**

- Simply extend the exception class. 

```java
public class IncorrectFileNameException extends Exception { 
    public IncorrectFileNameException(String errorMessage) {
        super(errorMessage);
    }
}
```

- [Create a Custom Exception in Java](https://www.baeldung.com/java-new-custom-exception)

------
<br><br>



## Stream

### Overview

**[Best Guide](https://stackify.com/streams-guide-java-8/) with common stream operations**

---
<br><br>

**Wat is Java 8 Stream?**

- Java 8 Stream = [java.util.stream](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)

- streams are wrappers around a data source, allowing us to operate with that data source and making bulk processing convenient and fast.

- A stream does not store data and, in that sense, is not a data structure. It also never modifies the underlying data source.

---
<br><br>


**Java8 Stream is not stream.io**

- Java 8 Streams should not be confused with Java I/O streams (ex: FileInputStream etc); these have very little to do with each other.


---
<br><br>


### FAQ

**Q1. Methods/Operations in Stream**

Intermediate Operations:

1. map: 
2. filter:
3. sorted

Terminal Operations:

1. collect
2. forEach
3. reduce

[More operation in here](https://stackify.com/streams-guide-java-8/)

---
<br><br>


**What is flatMap in Java 8 stream**

- A stream can hold complex data structures like Stream<List<String>>. In cases like this, **flatMap() helps us to flatten the data structure to simplify further operations**:

```java
@Test
public void whenFlatMapEmployeeNames_thenGetNameStream() {
    List<List<String>> namesNested = Arrays.asList( 
      Arrays.asList("Jeff", "Bezos"), 
      Arrays.asList("Bill", "Gates"), 
      Arrays.asList("Mark", "Zuckerberg"));

    List<String> namesFlatStream = namesNested.stream()
      .flatMap(Collection::stream)
      .collect(Collectors.toList());

    assertEquals(namesFlatStream.size(), namesNested.size() * 2);
}
```

- Notice how we were able to convert the Stream<List<String>> to a simpler Stream<String> – using the flatMap() API.

---
<br><br>

---
<br><br>

---
<br><br>

### Stream Coding Assignment


**Write a Java program to find the duplicate values of an array of integer values WITHOUT USING LOOPS.**
```java
import java.util.Arrays;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Test {

    public static void main(String[] args) {

        java.util.List<Integer> list = Arrays.asList(2,2,5,5,3);
        list.stream().collect(Collectors.groupingBy(Function.identity(),
                Collectors.counting()))
                .entrySet().stream()
                .filter(e -> e.getValue() > 1)
                .map(e -> e.getKey())
                .collect(Collectors.toList())
                .forEach(System.out::println);
    }


}
```
---
<br><br>

**Acronym: "united states of america" to USA**

```java
import java.util.*;
import java.util.stream.Collectors;

public class HelloWorld {

    public static void main(String[] args) {





        String input = "united states of armerica";
        String str = "";
        System.out.println(Arrays.stream(input.split(" "))
                //.filter(word -> Character.isUpperCase(word.charAt(0)))
                .filter(word -> !(word.equals("of") | word.equals("and")))
                .collect(Collectors.mapping(w -> Character.toString(w.charAt(0)).toUpperCase(), Collectors.joining(""))));
    }

}
```

---
<br><br>


## Java.io

### Serialization

- Custom class implemeting Serializable. 
	
	```java
	import java.io.Serializable;  
	public class Student implements Serializable{  
	 int id;  
	 String name;  
	 public Student(int id, String name) {  
	  this.id = id;  
	  this.name = name;  
	 }  
	}  
	```
	
---
<br><br>

---
<br><br>

---
<br><br>

## Thread
**Q1. How to make a thread in Java?**
- Extend Thread class and override the run method. 
	- Advantage: Java can only extend one class. Extend Thread prevent us extending other classes. 
	- Example:
		```java 
		Public class Addition extends Thread {
			public void run () {
			}	
		}
		```
- Implement Runnable interface
	- Example:
		```java
		Public class Addition implements Runnable {
			public void run () {
			}
		}
		```
---
<br><br>

**Q2. Difference between start() and run()**

- Start() method creates new thread and the code inside the run () method is executed in the new thread. 

- If we directly called the run() method then a new thread is not created and the currently executing thread will continue to execute the run() method.

---
<br><br>
**Q3. What is Synchronization?**

- Synchronization makes only one thread to access a block of code at a time. If multiple thread accesses the block of code, then there is a chance for inaccurate results at the end. To avoid this issue, we can provide synchronization for the sensitive block of codes.

---
<br><br>

**Difference between DaemonThread and Thread**
<br><br>

User Thread | Daemon Thread
---|---
JVM wait until user threads to finish their work. It never exit until all user threads finish their work.	| The JVM won't wait for daemon threads to finish their work. The JVM will exit as soon as all user threads finish their work.
JVM will not force to user threads for terminating, so JVM will wait for user threads to terminate themselves.	| If all user threads have finished their work JVM will force the daemon threads to terminate
User threads are created by the application.	| Mostly Daemon threads created by the JVM.
Mainly user threads are designed to do some specific task.	| Daemon threads are design as to support the user threads.
User threads are foreground threads.| 	Daemon threads are background threads.
User threads are high priority threads.	| Daemon threads are low priority threads.
Its life independent.	| Its life depends on user threads.


---
<br><br>

**Ways to make a class thead safe**

- synchronized
- atomic wrapper
- [volatile](https://www.geeksforgeeks.org/volatile-keyword-in-java/)


---
<br><br>

---
<br><br>

---
<br><br>

## Design Pattern

### Singleton

**需要默写**  

- eager loading : use when call is frequent 

  ```java
  class Singleton{
      private static Singleton instance = new Singleton();
      // when init this class, load immediately and it's thread safe and fast (no use of synchronized)
      //but no use of this class will waste space
  
      private Singleton() {  // private contructor
      }
  
      public static Singleton getInstance() {
          return instance;
      }
  }
  ```

- lazy loading : use when cost of creation is high

  ```java
  class Singleton {
  
      private static Singleton instance;
  
      private Singleton() {
  
      }
  
      public static synchronized Singleton getInstance() { //for concurrent issue to avoid multiple objects creation
          if (instance == null) {
              instance = new Singleton(); //load when use, save space but slow
          }
          return instance;
      }
  }
  ```

- use static inner class to implement : many products use this way

  ```java
  class Singleton {
  		    //outer class no static, won't load immediately 
      private static class SingletonClassInstance{
          private static final Singleton instance = new Singleton();
      }
      //only call this method will load static inner class and thread safe and final makes instance unique
      public static Singleton getInstance() {
          return SingletonClassInstance.instance;
      }
  
      private Singleton() {
      }
  }
  ```


### Lazy Loading

- Lazy loading is a design pattern where we delay the loading of object until the point where we need it.
- [GeeksforGeeks Tutorial](https://www.geeksforgeeks.org/lazy-loading-design-pattern/)





## Spring

### Dependency Injection (IOC)

**How is dependency injection achieved in Spring?**
- Dependency Injection in Spring can be done through constructors, setters or fields. (Setter injection, constructor injection or fiedls injection)

---
<br><br>

**4. what is IoC and AOP**

Inversion of Control (IoC) principle. IoC is also known as dependency injection (DI). It is a process whereby objects define their dependencies (that is, the other objects they work with) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.
<br>

Aspect-Oriented Programming (AOP)
AOP is used in the Spring Framework to:

1. provide declarative enterprise services, especially as a replacement for EJB declarative services. The most important such service is declarative transaction management.

2. allow users to implement custom aspects, complementing their use of OOP with AOP.

---
<br><br>

**5. how to connect DB**

connection, server, port. 

---
<br><br>




**8. Spring Concept List**
xx
---
<br><br>

### Bean

**6. What is Spring Bean**

Any normal java class that is initialized by Spring IoC container is called Spring Bean. We use Spring ApplicationContext to get the Spring Bean instance.

Spring IoC container manages the life cycle of Spring Bean, bean scopes and injecting any required dependencies in the bean.

---
<br><br>

**9. What is Bean wiring?**
The process of injection spring bean dependencies while initializing it is called Spring Bean Writing.

---
<br><br>

**10. What are different types off Spring Bean autowiring?**

1. autowire byName
2. autowire byType
3. autowire by constructor
4. autowire by @Autowired and @qualifer annotations

---
<br><br>

**11. Does Spring Bean provide thread safety?**

The default scope of Spring bean is singleton, so there will be only one instance per context. That means that all the having a class level variable that any thread can update will lead to inconsistent data. Hence, not thread safe. 

---
<br><br>

**12. What are different scopes of Spring Bean?**
 
- **singleton:** Only one instance of the bean will be created for each container. This is the **default scope** for the spring beans. While using this scope, make sure spring bean doesn’t have shared instance variables otherwise it might lead to data inconsistency issues because it’s not thread-safe.
- **prototype:** A new instance will be created every time the bean is requested.
- **request:** This is same as prototype scope, however it’s meant to be used for web applications. A new instance of the bean will be created for each HTTP request.
- **session:** A new bean will be created for each HTTP session by the container.
- **global-session:** This is used to create global session beans for Portlet applications.
	
---
<br><br>

**7. Different ways to configure a class as Spring Bean?**

1. XML Configuration

	This is the most popular configuration and we can use bean element in context file to configure a Spring Bean. For example:
	 
	 ```java
	 <bean name="myBean" class="com.journaldev.spring.beans.MyBean"></bean>
	 ```
<br>
2. Java Based Configuration

	If you are using only annotations, you can configure a Spring bean using @Bean annotation. This annotation is used with @Configuration classes to configure a spring bean. Sample configuration is:

	```java
	
	@Configuration
	@ComponentScan(value="com.journaldev.spring.main")
	public class MyConfiguration {
	
		@Bean
		public MyService getService(){
			return new MyService();
		}
	}
	
	```
	
	To get this bean from spring context, we need to use following code snippet:
	
	```java
	
	AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(
			MyConfiguration.class);
	MyService service = ctx.getBean(MyService.class);
	```
<br>	
3. Annotation Based Configuration

	We can also use @Component, @Service, @Repository and @Controller annotations with classes to configure them to be as spring bean. For these, we would need to provide base package location to scan for these classes. For example:
	
	```java
	
	<context:component-scan base-package="com.journaldev.spring" />
	```
---
<br><br>


---
<br><br>


### JPA

**JPA vs JDBC**

JPA|JDBC
---|---
Java Persistence API | Java Database Connectivity
ORM (access patterns: JPA, Hibernate, EclipseLink, OpenJPA, many others) | SQL (access patterns: JDBC, Spring JDBC, Apache DbUtils, jOOQ, many others)
JPA allows you to use an object model in your application which can make your life much easier. | JDBC allows you to do more things with the Database directly, but it requires more attention.
high level | low level

--- 
<br><br>


### JSP

JSP = Java Serv Pages

**Why JSP**

- **Coding in JSP is easy :**- As it is just adding JAVA code to HTML/XML.
- **Reduction in the length of Code :**- In JSP we use action tags, custom tags etc.
- **Connection to Database is easier :**-It is easier to connect website to database and allows to read or write data easily to the database.
- **Make Interactive websites :**- In this we can create dynamic web pages which helps user to interact in real time environment.
- **Portable, Powerful, flexible and easy to maintain :**- as these are browser and server independent.
- **No Redeployment and No Re-Compilation :**- It is dynamic, secure and platform independent so no need to re-compilation.
- **Extension to Servlet :**- as it has all features of servlets, implicit objects and custom tags

--- 
<br><br>

**Pass data from servlet to JSP**
- [How to pass data from servlet to JSP](https://www.programmergate.com/pass-data-servlet-jsp/)
- [Spring Boot Hello World Example – JSP](https://mkyong.com/spring-boot/spring-boot-hello-world-example-jsp/)

--- 
<br><br>

### Security
**这一部分需要的更多是项目经验, 或者tutorial, 而不是背题**

--- 
<br><br>

**What is OAuth2? What's the benefit? How to implement it?**

- OAuth (Open Authorization) is a simple way to publish and interact with protected data.
- It is an open standard for token-based authentication and authorization on the Internet. It allows an end user's account information to be used by third-party services, such as Facebook, without exposing the user's password.
- The OAuth specification describes five grants for acquiring an access token:
	- Authorization code grant
	- Implicit grant
	- Resource owner credentials grant
	- Client credentials grant
	- Refresh token grant
	- Consider the use case of Quora.
- Tutorials:
	- [Getting The Authorization Code](https://www.javainuse.com/spring/spring-boot-oauth-authorization-code)
	- [Getting The Access Token And Using it to fetch data](https://www.javainuse.com/spring/spring-boot-oauth-access-token)

--- 
<br><br>

### Ajax
AJAX = Asynchronous JavaScript and XML.

AJAX is a technique for creating fast and dynamic web pages. Mostly used with Jquery for submit forms.

- AJAX allows web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

- Classic web pages, (which do not use AJAX) must reload the entire page if the content should change.

- Examples of applications using AJAX: Google Maps, Gmail, Youtube, and Facebook tabs.


**Advantage of Ajax:**
- Ajax uses XML for content, CSS for presentation, along with Document Object Model and JavaScript for dynamic content display.

- Conventional web applications transmit information to and from the sever using synchronous requests. It means you fill out a form, hit submit, and get directed to a new page with new information from the server.

- With AJAX, when you hit submit, JavaScript will make a request to the server, interpret the results, and update the current screen. In the purest sense, the user would never know that anything was even transmitted to the server.

- XML is commonly used as the format for receiving server data, although any format, including plain text, can be used.

- AJAX is a web browser technology independent of web server software.

- Intuitive and natural user interaction. Clicking is not required, mouse movement is a sufficient event trigger.

- Read data from a web server - after a web page has loaded
- Update a web page without reloading the page
- Send data to a web server - in the background

--- 
<br><br>


**Ajax Example**

- [Spring Boot Ajax Jquery Example](https://www.jackrutorial.com/2018/09/spring-boot-ajax-jquery-example.html)
- [Spring Boot Ajax example](https://mkyong.com/spring-boot/spring-boot-ajax-example/)

---
<br><br>

## 杂

**1. Spring Core Concept**

- Dependency Injection
- Aspect Oriented Programming

---
<br><br>

**How to change Spring default configuration**

- By chaging the applicaiton.properties file. Like the server port address. 

---
<br><br>

**What is Spring actuator**

- Spring Boot Actuator is a sub-project of the Spring Boot Framework. It includes a number of additional features that help us to monitor and manage the Spring Boot application. 
- Three features: Endpoints, Metrics, Audit
	- **Endpoint**: The actuator endpoints allows us to monitor and interact with the application. Spring Boot provides a number of built-in endpoints. 
	- **Metrics**:  Spring Boot Actuator provides dimensional metrics by integrating with the micrometer. The micrometer is integrated into Spring Boot. It is the instrumentation library powering the delivery of application metrics from Spring. It provides vendor-neutral interfaces for timers, gauges, counters, distribution summaries, and long task timers with a dimensional data model.
	- **Audit**: Spring Boot provides a flexible audit framework that publishes events to an AuditEventRepository. It automatically publishes the authentication events if spring-security is in execution.

---
<br><br>

**2. joinPoint and pointCut**

Join point: a point during the execution of a program, such as the execution of a method or the handling of an exception. In Spring AOP, a join point always represents a method execution.
<br><br>
Pointcut: a predicate that matches join points. Advice is associated with a pointcut expression and runs at any join point matched by the pointcut (for example, the execution of a method with a certain name). The concept of join points as matched by pointcut expressions is central to AOP, and Spring uses the AspectJ pointcut expression language by 

---
<br><br>

**3. spring core (IoC and AOP)**

IoC Container, Events, Resources, i18n, Validation, Data Binding, Type Conversion, SpEL, AOP. <br>
Mainly IOC & 

---
<br><br>

**Application server vs Web server**

- web server is for static pages. 
- application server is for dynamic contentt. 

---
<br><br>

**What is ResponseEntity in Spring**

- [What is ResponseEntity in Spring](http://zetcode.com/springboot/responseentity/)

---
<br><br>

**Important annotations**

- **@Controller** – for controller classes in Spring MVC project.
- **@RequestMapping** – for configuring URI mapping in controller handler methods. This is a very important annotation, so you should go through Spring MVC RequestMapping Annotation Examples
- **@ResponseBody** – for sending Object as response, usually for sending XML or JSON data as response.
- **@PathVariable** – for mapping dynamic values from the URI to handler method arguments.
- **@Autowired** – for autowiring dependencies in spring beans.
- **@Qualifier** – with @Autowired annotation to avoid confusion when multiple instances of bean type is present.
- **@Service** – for service classes.
- **@Scope** – for configuring scope of the spring bean.
- **@Configuration, @ComponentScan and @Bean** – for java based configurations.
- AspectJ annotations for configuring aspects and advices, @Aspect, @Before, @After, @Around, @Pointcut etc.

---
<br><br>

**can you output both Xml and json file using Spring**

Yes we can, using @ResponseBody annotation. This is how we send JSON or XML based response in restful web services.

---
<br><br>

**What is caching in Spring?**

[Caching Data with Spring](https://spring.io/guides/gs/caching/)

---
<br><br>


## REST

[REST API Tutorial](https://restfulapi.net/)


### What is REST?

REST is acronym for REpresentational State Transfer. It is architectural style for distributed hypermedia systems 

**Guiding Principles of REST**

1. Client–server 

	- By separating the user interface concerns from the data storage concerns, we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components.
	
2. Stateless 

	- Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is therefore kept entirely on the client.

3. Cacheable 

	- Cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable. If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.

4. Uniform interface 

	- By applying the software engineering principle of generality to the component interface, the overall system architecture is simplified and the visibility of interactions is improved. In order to obtain a uniform interface, multiple architectural constraints are needed to guide the behavior of components. REST is defined by four interface constraints: identification of resources; manipulation of resources through representations; self-descriptive messages; and, hypermedia as the engine of application state.

5.Layered system 

	- The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior such that each component cannot “see” beyond the immediate layer with which they are interacting.

6.Code on demand (optional) 

	- REST allows client functionality to be extended by downloading and executing code in the form of applets or scripts. This simplifies clients by reducing the number of features required to be pre-implemented.

---
<br><br>

### Idempotent

	- In the context of REST APIs, when making multiple identical requests has the same effect as making a single request – then that REST API is called idempotent.

**POST:**

	- POST is NOT idempotent.  GET, PUT, DELETE are idempotent
	- When you invoke the same POST request N times, you will have N new resources on the server. So, POST is not idempotent. 

**PUT:**
	
	-  If you invoke a PUT API N times, the very first request will update the resource; then rest N-1 requests will just overwrite the same resource state again and again – effectively not changing anything. Hence, PUT is idempotent.

**DELETE:**

	- When you invoke N similar DELETE requests, first request will delete the resource and response will be 200 (OK) or 204 (No Content). Other N-1 requests will return 404 (Not Found). Clearly, the response is different from first request, but there is no change of state for any resource on server side because original resource is already deleted. So, DELETE is idempotent.

---
<br><br>

### PUT vs POST

PUT | POST
---|---
PUT method requests for the enclosed entity be stored under the supplied Request-URI. | The POST method is used to request that the origin server accept the entity enclosed in the request as a new subordinate of the resource identified by the Request-URI in the Request-Line.
PUT /questions/{question-id}|POST /questions
PUT method is idempotent. | POST is NOT idempotent
Use PUT to UPDATE operation | Use POST to CREATE operation
response is not cacheable | response is not cacheable

Example:

```
GET 	/device-management/devices : Get all devices
POST 	/device-management/devices : Create a new device

GET 	/device-management/devices/{id} : Get the device information identified by "id"
PUT 	/device-management/devices/{id} : Update the device information identified by "id"
DELETE	/device-management/devices/{id} : Delete device by "id"
```

---
<br><br>
 
### SOAP vs REST

[SOAP Vs. REST: Difference between Web API Services](https://www.guru99.com/comparison-between-web-services.html)

SOAP | REST
---|---
Simple Object Access Protocol | Representational State Transfer
SOAP is a protocol | REST is architectural pattern
exclusively on XML| can use XML, YAML or plain text, but prefer JSON
very strong messaging framework | widely adopted technologies, specifically HTTP
can only use HTTP POST | can use all HTTP methods
not cacheable | can be cacheable or not-cacheable
SOAP uses service interfaces to expose its functionality to client applications | REST uses Uniform Service locators to access to the components on the hardware device.
have standardized WS-SECUIRTY | very unsecure
SOAP cannot make use of REST since SOAP is a protocol and REST is an architectural pattern.|REST can make use of SOAP as the underlying protocol for web services, because in the end it is just an architectural pattern.
SOAP requires more bandwidth for its usage| REST does not need much bandwidth when requests are sent to the server. 



---
<br><br>


## Angular

**Advantage of Angular**

* Ability to add a custom directive
* Exceptional community support
* Facilitates client and server communication
* Features strong features, such as Animation and Event Handlers
* Follows the MVC pattern architecture
* Offers support for static template and Angular template
* Support for two-way data-binding
* Supports dependency injection, RESTful services, and validations

---
<br><br> 

**Tell me something about Angular ng CLi**

- ng new my-first-project
- ng serve

---
<br><br> 

---
<br><br> 
## AWS

- [Deploying a Spring Boot Application on AWS Using AWS Elastic Beanstalk](https://aws.amazon.com/blogs/devops/deploying-a-spring-boot-application-on-aws-using-aws-elastic-beanstalk/)





## Hibernate

**save vs persist**

save | persist
--- | ---
oudside transaction boundaries | inside transaction boundaries
does not return anything | returns unique identifier associated with provided transaction
return type is void | return type is Long Type value. 

---
<br><br>

**Different types of cache strategies in hibernate**

- First-level cache: 

	**By default**
	
	The first-level cache is the **Session cache** and is a mandatory cache through which all requests must pass. The Session object keeps an object under its own power before committing it to the database.
	
<br><br>
- Second-level cache:

	**Optional**
	
	The second level cache is responsible for caching objects across sessions. When this is turned on, objects will first be searched in the cache and if they are not found, a database query will be fired.
	
<br><br>	
- Query cache:

	Query Cache **is used to cache the results of a query**. 
	
	When the query cache is turned on, the results of the query are stored against the combination query and parameters. Every time the query is fired the cache manager  checks for the combination of parameters and query. If the results are found in the cache, they are returned, otherwise a database transaction is initiated.
	
	Example:
	```java
	Session session = SessionFactory.openSession();
	Query query = session.createQuery("from Order"); query.setCacheable(true);
	List users = query.list();
	SessionFactory.closeSession();
	```

---
<br><br>

**how to do many to many mapping in hibernate?**

[Tutorial](https://www.baeldung.com/hibernate-many-to-many)

Use @ManyToMany, @JoinTable and @JoinColumn annotations

- @ManyToMany annotation is used in both classes to create the many-to-many relationship between the entities.
- @JoinTable is used to define the join/link table.
- @JoinColumn annotation is used to specify the join/linking column with the main table

---
<br><br>

---
<br><br>

## SQL

**What is Database Normalization**

- Normalization is a database design technique which organizes tables in a manner that reduces redundancy and dependency of data.

- It divides larger tables to smaller tables and links them using relationships.

- [Tutorial link](https://www.guru99.com/database-normalization.html)
- [More Tutorial](https://www.sqlshack.com/what-is-database-normalization-in-sql-server/)

- 1NF (First Normal Form) Rules
	- Each table cell should contain a single value.
	- Each record needs to be unique.
- 2NF
	- Rule 1- Be in 1NF
	- Rule 2- Single Column Primary Key
- 3NF
	- Rule 1- Be in 2NF
	- Rule 2- Has no transitive functional dependencies


---
<br><br>



## Testing

### Junit

**Junit Testing in Spring**

- [Mocking Objects in Spring Testing. ](https://docs.spring.io/spring/docs/current/spring-framework-reference/testing.html#mock-objects)

---
<br><br>

**How to test exception in Junit**

- Use @Test(expected)

---
<br><br>

**Mocking Objects in Spring**

- [Mocking Objects in Spring Testing. ](https://docs.spring.io/spring/docs/current/spring-framework-reference/testing.html#mock-objects)

---
<br><br>

---
<br><br>

---
<br><br>

## Working Mode and Code Review

**How do you do code review?**

### Agile

<br>
<p align="center">
<img width="680" src="https://hackernoon.com/drafts/6t8232hs.png" />
</p>
<br><br>



## After Interview

4. Describe the culture of the company.

5. Where do you think the company is headed in the next 5 years?

6. Who do you consider your top competitor, and why?
