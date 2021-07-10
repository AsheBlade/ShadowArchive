---
layout: post
title: Data Structure Design
date: 2021-05-20
author: Shadow Walker
tags: [Algorithm, Interview]
toc: true
---

这一类题目比较综合, 在于构建数据结构, 通常的特点是同时使用多个, 或者多种数据结构进行解题. 

### 1429. First Unique Number

很喜欢的一道题, 简洁优雅, 难度在于理解需求. 其实这道题不需要记录元素, 只要是重复的元素一律是污染了的, 不需要记录. 也就是说我们只需要记录这个queue里独特的元素即可, 没必要记录重复的. 理解这一点之后这道题就不难了. 

```java
class FirstUnique {

  private Queue<Integer> queue = new ArrayDeque<>();
  private Map<Integer, Boolean> isUnique = new HashMap<>();

  public FirstUnique(int[] nums) {
    for (int num : nums) {
      // Notice that we're calling the "add" method of FirstUnique; not of the queue. 
      this.add(num);
    }
  }

  public int showFirstUnique() {
    // We need to start by "cleaning" the queue of any non-uniques at the start.
    // Note that we know that if a value is in the queue, then it is also in
    // isUnique, as the implementation of add() guarantees this.
    while (!queue.isEmpty() && !isUnique.get(queue.peek())) {
      queue.poll();
    }
    // Check if there is still a value left in the queue. There might be no uniques.
    if (!queue.isEmpty()) {
      return queue.peek(); // We don't want to actually *remove* the value.
    }
    return -1;
  }

  public void add(int value) {
    // Case 1: We need to add the number to the queue and mark it as unique. 
    if (!isUnique.containsKey(value)) {
      isUnique.put(value, true);
      queue.add(value);
    // Case 2 and 3: We need to mark the number as no longer unique.
    } else {
      isUnique.put(value, false);
    }
  }
}
```


### 146. LRU Cache

大名鼎鼎的146题LRU, 思路非常简单, 写对非常非常难.  这里放上符合自己习惯的写法, 虽然比较啰嗦, 但是方便自己看. 

```java
class LRUCache {
    private Map<Integer,Node> cache;
    private Node head;
    private Node tail;
    private int size;
    private int capacity;
    public LRUCache(int capacity) {
        head = new Node();
        tail = new Node();
        this.capacity = capacity;
        this.size = 0;
        cache = new HashMap<>();
        this.head.next = this.tail;
        this.tail.prev = this.head;
    }
    
    public int get(int key) {
        if(cache.containsKey(key)){
            Node node = cache.get(key);
            this.moveToHead(node);
            return node.value;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        Node node = cache.get(key);
        if(node!=null){
            node.value = value;
            this.moveToHead(node);
        }else{
            node = new Node();
            node.key = key;
            node.value = value;
            
            cache.put(key, node);
            this.addNode(node);
            size ++;
            if(this.size>this.capacity){
                Node tail = this.pop();
                cache.remove(tail.key);
                size--;
            }
        }
    }
    
    class Node{
        int key;
        int value;
        Node prev;
        Node next;
    }
    
    private void addNode(Node node){
        node.next = head.next;
        node.prev = head;
        
        head.next.prev = node;
        head.next = node;
    }
    
    private void removeNode(Node node){
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private Node pop(){
        Node node = this.tail.prev;
        this.removeNode(node);
        return node;
    }
    
    private void moveToHead(Node node){
        this.removeNode(node);
        this.addNode(node);
    }
}
```



## 1628. Design an Expression Tree With Evaluate Function

很喜欢的一道数据结构设计, 既考察构建tree, 又考察tree的 in order traverse. 知识点考察全面. 收录在 data structure design. 

很容易想到用stack, 但难点在于构建的时候用stack 记录 TreeNode, 而不是记录 Integer. 

```java
abstract class Node {
    
    public abstract int evaluate();
    // define your fields here
    String val;
    Node left;
    Node right;
}

class TreeNode extends Node{
    
    public int evaluate(){
        return inOrder(this);
    }
    
    private int inOrder(TreeNode tn){
        
        if(tn == null)
            return 0;
        
        if(tn.left == null && tn.right == null)
            return Integer.valueOf(tn.val);
        
        int num1 = inOrder(tn.left);
        int num2 = inOrder(tn.right);
        
        String s = tn.val;
        
        if(s.equals("*"))
            return num1*num2;
        else if(s.equals("/"))
            return num1/num2;
        else if(s.equals("+"))
            return num1+num2;
        else if(s.equals("-"))
            return num1-num2;
        
        throw new RuntimeException();
    }
    // define your fields here
    String val;
    TreeNode left;
    TreeNode right;
    
    public TreeNode(String val){
        this.val = val;
    }
    
    public TreeNode(String val, TreeNode left, TreeNode right){
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

class TreeBuilder {
    TreeNode root;
    Set<String> operations = new HashSet<>();
    String[] postfix;
    
    Node buildTree(String[] postfix) {
        operations.add("*");
        operations.add("/");
        operations.add("+");
        operations.add("-");
        
        Stack<TreeNode> stack = new Stack<>();
        for(String token: postfix){
            if(operations.contains(token)){
                // operator
                TreeNode n2 = stack.pop();
                TreeNode n1 = stack.pop();
                stack.push(new TreeNode(token, n1, n2));
            } else{
                // operand
                stack.push(new TreeNode(token));
            }
        }
        return stack.pop();
    }
    
    
    private int evaluate(){
        return this.root.evaluate();
    }
}
```