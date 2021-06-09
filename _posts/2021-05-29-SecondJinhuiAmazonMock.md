---
layout: post
title: Second Jinhui Amazon Mock Interview
date: 2021-05-29
author: 
tags: [Interview]
---

## 前面

25天之后和jinhui第二次进行Amazon mock. 

## 过程

自我介绍, LP, 问了SQL, 我实在不知道实话相告, 然后问了Spring, 之后开始coding, 问了一道典型的backtrack, LC39题(居然没问更难的40题). 

coding的过程在下面代码. 

感觉挺好的. 至少coding这一块真的不错. 

## 反馈

- 自我介绍和LP有时候语速还是太快.  不自然.
- LP question不要说当时的感情, 就说如何处理工作不要带有感情色彩
- SQL index提高搜索效率
- SQL transaction update 保证数据原始性  隔离级别最高

## 之后

暂时没有之后, 目前还不知道结果, 自我感觉良好. 

这一次无论成败, 都是成功的. 这是我自2018年以来coding面试感觉最好最成功的的一次. 对方也对我的coding进行了肯定, 至少说明之前25天的努力没有白费, 提升是肉眼可见的. 

做梦感觉这个代码不对, 醒来用39题测了一下, 结果还真不对....  总之老师的评价是思路很清晰, 也就还可以吧... 这个目前也是无法解决的, 脑子里不能跑代码. 

## 原版代码

[1,3,4] target = 8, return: [1,3,4]

array is not sorted and it element is unique return one valid result


1. use DFS to find all the combinations or permutations. 
2. By finding all, we use an boolean to set done after we find one.  When done then break. 


```java

 1-2-3-4
 1-2-4
 1-3-4
 1-4
 2-3-4

[1,2,3, -4]
[1,3,4] 8   1-3 sum = 1,4  i=2 numList(1,4)
[] 0
[1] 1
[2,-3,4] 6
[-3,2,4] -1

List<Integer> output = new LinkedList<>();
//boolean done = false;
private List<Integer> solution(int[] list, int target){
	 Arrays.sort(list);
   dfs(list, target, 0, new LinkedList<>(), 0);
   return output;
}

private void dfs(int[] list, int target, int start, LinkedList<Integer> numList , int sum){
	//if(done)
  	//return;
  
  // 1. either there is no element to add. 
  if(start==list.length){
  	return;
  }
  
  for(int i=start; i<list.length; i++){
  	sum += list[i];
    if(sum>target){
    	return;
    if(sum == target){
    	output.add(new LinkedList<>(numList));
      return;
    }
  	numLIst.addlist[i]);
    dfs(list, target, i+1, numList, sum);
    numList.removeLast();
  }
  
}








private List<Integer> solution(int[] list, int target){
	Arrays.sort(list);
  int low, high;
  high = list.length-1;
  while(low<=high){
  	int sum = list[low] + list[high];
    if(sum == target){
    	return new int[]{
    if(sum > target){
    	high--;
    }
    
  }
}
```


## 修改代码

睡醒之后用39题测试修改的代码

```java
class Solution {
    List<List<Integer>> output = new LinkedList<>();
    //boolean done = false;
    public List<List<Integer>> combinationSum(int[] list, int target){
        Arrays.sort(list);
       dfs(list, target, 0, new LinkedList<>(), 0);
       return output;
    }

    private void dfs(int[] list, int target, int start, LinkedList<Integer> numList , int sum){
        //if(done)
        //return;

      // 1. either there is no element to add. 
        //System.out.println(start);
          // if(start==list.length){
          //   return;
          // }
        
            if(sum == target){
                System.out.println("bingo");
                output.add(new LinkedList<>(numList));
              return;
            }

          for(int i=start; i<list.length; i++){
             
            sum += list[i];
               System.out.println(list[i] + " " + start + " " + i + " " + sum);
              
            if(sum>target)
                break;
             numList.addLast(list[i]);
              System.out.println(numList.toString());
 
              // System.out.println(list[i] + " " + start + " " + i + " " + sum);
            
            dfs(list, target, start++, numList, sum);
            sum = sum - list[i];
            numList.removeLast();
          }

    }
    
}
```
