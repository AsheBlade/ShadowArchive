---
layout: post
title: Trie Prefix Tree
date: 2021-07-07
author: Shadow Walker
tags: [OPLC, Tree]
toc: true
comments: true
---

## 和DP的关联性

WordSearch, WordBreak题目主要考虑的方向就是两个: Trie和DP. 需要总结一下二者的区别和应用场景. 

从目前看来认为DP的应用更广.  能用Trie解的题都能用DP解. 但能用DP解的不一定能用Trie解, 或者解起来反而更麻烦, 加一层DFS. 

- 但Trie的优势是在查连续的word之中更适用, word之间不存在跳跃关系, 必须连续查找. (LC211, LC79) 
- 而DP更适合非连续无序的查找. (LC139)

## 211. Design Add and Search Words Data Structure

看了211 才知道之前208的写法过于复杂了, 直接用一个简单的HashMap就可以实现. 

```java
class TrieNode {
    Map<Character, TrieNode> links = new HashMap();
    boolean isEnd = false;
    public TrieNode() {}
}

class WordDictionary {
    TrieNode trie;

    /** Initialize your data structure here. */
    public WordDictionary() {
        trie = new TrieNode();
    }

    /** Adds a word into the data structure. */
    public void addWord(String word) {
        TrieNode node = trie;

        for (char ch : word.toCharArray()) {
            if (!node.links.containsKey(ch)) {
                node.links.put(ch, new TrieNode());
            }
            node = node.links.get(ch);
        }
        node.isEnd = true;
    }

    /** Returns if the word is in the node. */
    public boolean searchInNode(String word, TrieNode node) {
        for (int i = 0; i < word.length(); ++i) {
            char ch = word.charAt(i);
            if (!node.links.containsKey(ch)) {
                // if the current character is '.'
                // check all possible nodes at this level
                if (ch == '.') {
                    for(TrieNode tn: node.links.values()){
                        if(searchWord(word.substring(i+1), tn))
                            return true;
                    }
                }
                // if no nodes lead to answer
                // or the current character != '.'
                return false;
            } else {
                // if the character is found
                // go down to the next level in trie
                node = node.links.get(ch);
            }
        }
        return node.isEnd;
    }

    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        return searchInNode(word, trie);
    }
}
```

## 1268. Search Suggestions System

没有什么意外的地方, 很明显的Trie, 只不过加了一个DFS. 难度比上面的211要略难. 这个DFS一看就懂, 但不是随便就能写出来的. 

难点主要有两个: 

- Char 的traverse, 从a到z. 
- DFS递归. 

```java
class Solution {
    List<List<String>> output = new ArrayList<>();
    TrieNode root = new TrieNode();
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        // Add all words to trie.
        for(String product: products){
            this.insert(product);
        }
        
        String prefix = "";
        for (char c : searchWord.toCharArray()) {
            prefix += c;
            output.add(this.searchPrefix(prefix));
        }
        
        return output;
    }
    
    private List<String> searchPrefix(String word){
        List<String> resultList = new ArrayList<>();
        TrieNode curr = root;
        
        // Move curr to the end of prefix in its trie representation.
        for(char c: word.toCharArray()){
            if(curr.links.get(c)==null)
                return resultList;
            curr = curr.links.get(c);
        }
        
        searchRelated(word, curr, resultList);
        return resultList;
    }
    
        // Runs a DFS on trie starting with given prefix and adds all the words in the resultBuffer, limiting result size to 3
    private void searchRelated(String word, TrieNode curr, List<String> list){
        if(list.size() == 3)
            return;
        if(curr.isEnd)
            list.add(word);
         // Run DFS on all possible paths.
        for(char c= 'a'; c<='z'; c++){
            if(curr.links.get(c)!=null){
                searchRelated(word + c, curr.links.get(c), list);
            }
        }
    }

    private void insert(String word){
        TrieNode tn = root;
        for(char c: word.toCharArray()){
            if(!tn.links.containsKey(c)){
                tn.links.put(c, new TrieNode());
            }
            tn = tn.links.get(c);
        }
        tn.isEnd = true;
    }
}

class TrieNode{
    Map<Character, TrieNode> links = new HashMap<>();
    boolean isEnd;
    public TrieNode(){}
}
```

## 588. Design In-Memory File System

其实588严格上来说不能算作一道难题. 其实难度甚至略低于上面的1268.  588的难更多体现在对题目条件的理解, 难度不在于复杂度, 而在于这道题的对题目繁杂条件的理清. 难度不在复杂, 而在繁琐.  亚马逊高频50. 需要刷穿. 

- 2021-07-08 初见

```java
class FileSystem {
    
    TrieNode root;
    public FileSystem() {
        this.root = new TrieNode();
    }
    
    // 难点都在这个方法. 
    public List<String> ls(String path) {
        TrieNode tn = root;
        List<String> output = new ArrayList<>();
        // 输入只有一个/的时候是特殊情况, 要特殊考虑. 
        if(!path.equals("/")){
            String[] pathArr = path.split("/");
            for(int i=1; i<pathArr.length; i++){
                tn = tn.links.get(pathArr[i]);
            }
            if(tn.isFile){
                // If path is a file path, returns a list that only contains this file's name.
                // 这里是难点, 注意!!! 需要加file name, 不是加content. 而file name只能从path之中提取. 
                output.add(pathArr[pathArr.length-1]);
                return output;
            }
        }
        
        // If path is a directory path, returns the list of file and directory names in this directory.
        output = new ArrayList<>(tn.links.keySet());
        // sort lexicographic order.
        Collections.sort(output);
        return output;
    }
    
    // 从这个方法入手看.  其实这个方法就是常规的Trie insert 方法. 
    public void mkdir(String path) {
        TrieNode tn = root;
        String[] pathArr = path.split("/");
        // 需要从1开始, 因为d[0]是空格. 
        for(int i=1; i<pathArr.length; i++){
            if(!tn.links.containsKey(pathArr[i]))
                tn.links.put(pathArr[i], new TrieNode());
            tn = tn.links.get(pathArr[i]);
        }
    }
    
    // 跟上面是一样, 只不过跟Trie一样, 最后加了一个断点. 
    public void addContentToFile(String filePath, String content) {
        TrieNode tn = root;
        // If path is a file path, returns a list that only contains this file's name.
        String[] pathArr = filePath.split("/");
        for(int i=1; i<pathArr.length; i++){
            if(!tn.links.containsKey(pathArr[i]))
                tn.links.put(pathArr[i], new TrieNode());
            tn = tn.links.get(pathArr[i]);
        }
        tn.isFile = true;
        tn.content = tn.content + content;
    }
    
    // 就是很简单的Trie search方法. 不需要考虑太多条件判断, 因为这道题不存在无效输入. 
    public String readContentFromFile(String filePath) {
        TrieNode tn = root;
        String[] pathArr = filePath.split("/");
        for(int i=1; i<pathArr.length; i++){
            tn = tn.links.get(pathArr[i]);
        }
        return tn.content;
    }
}

class TrieNode{
    Map<String, TrieNode> links = new HashMap<>();
    String content = "";
    boolean isFile;
    public TrieNode(){}
}
```

## 208. Implement Trie (Prefix Tree)

我是先学的208, 后学的211. 208这个构建太啰嗦了. 不需要学. 其实就是用一个array去替代hashmap, 没有意义. 

下面是官方答案, 一看就懂. 

```java

class Trie {
    
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            char currentChar = word.charAt(i);
            if (!node.containsKey(currentChar)) {
                node.put(currentChar, new TrieNode());
            }
            node = node.get(currentChar);
        }
        node.setEnd();
    }
    
    // search a prefix or whole key in trie and
    // returns the node where search ends
    private TrieNode searchPrefix(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
           char curLetter = word.charAt(i);
           if (node.containsKey(curLetter)) {
               node = node.get(curLetter);
           } else {
               return null;
           }
        }
        return node;
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
       TrieNode node = searchPrefix(word);
       return node != null && node.isEnd();
    }
    
        // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode node = searchPrefix(prefix);
        return node != null;
    }
    
    class TrieNode {

        // R links to node children
        private TrieNode[] links;

        private final int R = 26;

        private boolean isEnd;

        public TrieNode() {
            links = new TrieNode[R];
        }

        public boolean containsKey(char ch) {
            return links[ch -'a'] != null;
        }
        public TrieNode get(char ch) {
            return links[ch -'a'];
        }
        public void put(char ch, TrieNode node) {
            links[ch -'a'] = node;
        }
        public void setEnd() {
            isEnd = true;
        }
        public boolean isEnd() {
            return isEnd;
        }
    }
}
```

