---
layout: post
title: Lowest Common Ancestor
date: 2021-05-21
author: Shadow Walker
tags: [Algorithm, Interview, Tree]
comments: true
toc: true
---

## Overview

- Lowest Common 家族题目
	* 236. Lowest Common Ancestor of a Binary Tree
	* 1644. Lowest Common Ancestor of a Binary Tree II
	* 1650. Lowest Common Ancestor of a Binary Tree III
	* 1676. Lowest Common Ancestor of a Binary Tree IV
	* 865/1123. Smallest Subtree with all the Deepest Nodes

- 其他

	* 235. Lowest Common Ancestor of a Binary Search Tree
	* 1302. Deepest Leaves Sum

- 更多: 

	* 1430. Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree
	* 1379. Find a Corresponding Node of a Binary Tree in a Clone of That Tree

## 刷题思路

上面 lowest common家族之中236题是核心. 其实只刷236和1676即可, 其他家族题目都是重复.  

235是一道BST特殊题, 可以刷一下拓宽思路.  目前就只有这三道值得做. 

## 整体思路

Lowest Common 家族题目整体来说有两个解法, 这两个解法都值得学, 拓宽递归思路: 

1. Flag解法. 

	Flag解法目前是有局限性的, 解不了1676题. 我之所以说目前有局限性的意思是我认为是能解的, 只是我还没写出来. Flag解法的优势是简单粗暴明了, 不怕无解的情况. 可以同时解236和1644题. 
2. Recursion解法
	
	这个recursion是不完全recursion, 和一般的recursion不太一样. 这个解法的问题是不能处理无解的情况, 题目必须保证存在解. 比如1644题要求必须有解, 就不能用这个解法.  这个解法可以用在236, 1676 和 865题. 

## 236. Lowest Common Ancestor of a Binary Tree

非常喜欢这个flag解法, 很精妙. 可以直接给下面的1644用, 考虑了无解的情况. 

```java
class Solution {
    
    private TreeNode answer;
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        answer = null;
        if(DFS(root,p,q)){
            return answer;
        }
       
        return answer;
    }
    
    private boolean DFS(TreeNode root, TreeNode p, TreeNode q){
        if(root == null){
            return false;
        }
        int flag = 0;
        
        if(DFS(root.left, p, q)){
             flag++;
        }
        
        if(DFS(root.right, p,q)){
            flag++;
        }
        
        if(root.val==p.val || root.val==q.val){
            flag++;
        }
        
        if(flag>=2)
            answer = root;
        
        if(flag>0)
            return true;
        else{
            return false;
        }
    }
}
```

另一个recursion解法, 这个解法不考虑无解的情况. 但适用度更广. 

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root.val==p.val || root.val==q.val) {
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if(left != null && right != null) {
            return root;
        }
        
        return (left != null)? left: right;
    }

}
```

## 1644. Lowest Common Ancestor of a Binary Tree II

跟上面的236是一道题. 只不过236是保证有解的, 这道不是. 可以直接用上面236的flag解法. 

## 1650. Lowest Common Ancestor of a Binary Tree III

名字虽然一样, 但其实不属于这个家族. 

伪中等题, 不算浪费时间, 但是太简单了. Tree的双指针. 我写的稍微复杂一点为了节省那一丁点的算力. 如果不追求算力还可以更简单. 一刷通过, 没有收录. 

## 1676. Lowest Common Ancestor of a Binary Tree IV

这是看到目前公认最快的解法

```java
class Solution {
    private Set<TreeNode> nodesSet;
    
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode[] nodes) {
        nodesSet = new HashSet(Arrays.asList(nodes));
        return lcaHelper(root);
    }
    
    private TreeNode lcaHelper(TreeNode root) {
        if(root == null || nodesSet.contains(root)) {
            return root;
        }
        TreeNode left = lcaHelper(root.left);
        TreeNode right = lcaHelper(root.right);
        
        if(left != null && right != null) {
            return root;
        }
        
        return (left != null)? left: right;
    }
}
```

## 235. Lowest Common Ancestor of a Binary Search Tree

这道题算是236题加上特殊条件. 用236题的解法也是可以解的. 最优解需要考虑BST的特殊条件去写, 解法很容易理解, 但不容易想. 


```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        int pVal = p.val;
        int qVal = q.val;
        
        while(root!=null)
        {
            if(pVal>root.val&& qVal>root.val){
                root = root.right;
            }
            else if(pVal<root.val&&qVal<root.val){
                root = root.left;
            }else{
                return root;
            }
            
        }
        return null;
    }
}
```

## 1302. Deepest Leaves Sum

我发现我经常能把Tree的问题想复杂, 这道题其实就是简单的BFS by level而已, 没有取巧的地方. 

```java
class Solution {
    public int deepestLeavesSum(TreeNode root) {
        
        Queue<TreeNode> q = new LinkedList<>();
        Queue<TreeNode> last = new LinkedList<>();
        
        if(root == null)
            return 0;
        
        q.add(root);
        
        while(!q.isEmpty()){
            last = new LinkedList<>(q);
            int n = q.size();
            for(int i=0; i<n; i++)
            {
                TreeNode pick = q.poll();
                //System.out.println(pick.val);
                if(pick.left!=null)
                    q.offer(pick.left);
                if(pick.right!=null)
                    q.offer(pick.right);
            }
        }
        int sum = 0;
        while(!last.isEmpty()){
            //System.out.println(last.poll().val);
            sum+=last.poll().val;
        }
        return sum;
        
    }
}
```

## 865/1123. Smallest Subtree with all the Deepest Nodes

是一道好题, 但这道题是前面1302题和1676的组合, 其实就是分两步走, 找到deepest nodes, 然后再找他们的共同root. 只要做好前面的1302题和1676题, 这道题就没有任何难度了. 换句话说, 只要刷好前面两道题即可. 

```java
class Solution {
    private Set<TreeNode> nodesSet;
    public TreeNode subtreeWithAllDeepest(TreeNode root) {
        this.nodesSet = new HashSet<>();
        this.deepestLeavesSum(root);
        return lcaHelper(root);
    }
    
    private TreeNode lcaHelper(TreeNode root) {
        if(root == null || nodesSet.contains(root)) {
            return root;
        }
        TreeNode left = lcaHelper(root.left);
        TreeNode right = lcaHelper(root.right);
        
        if(left != null && right != null) {
            return root;
        }
        
        return (left != null)? left: right;
    }
    
    private void deepestLeavesSum(TreeNode root) {
        
        Queue<TreeNode> q = new LinkedList<>();
        Queue<TreeNode> last = new LinkedList<>();
        
        if(root == null)
            return;
        
        q.add(root);
        
        while(!q.isEmpty()){
            last = new LinkedList<>(q);
            int n = q.size();
            for(int i=0; i<n; i++)
            {
                TreeNode pick = q.poll();
                //System.out.println(pick.val);
                if(pick.left!=null)
                    q.offer(pick.left);
                if(pick.right!=null)
                    q.offer(pick.right);
            }
        }
        while(!last.isEmpty()){
            //System.out.println(last.poll().val);
            this.nodesSet.add(last.poll());
        }
    }
}
```