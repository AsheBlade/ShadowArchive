---
layout: post
title: 游标卡尺
date: 2020-09-03
author: Shadow Walker
tags: [Algorithm, Interview, TwoPointers]
toc: true
---

## Overview

2021-05-17 推翻之前的overview 说明.  SlidingWindow不是奇淫技巧, 是很常见的一类题型, 所以做专题总结. 

---

这一篇是关于sliding window这个奇淫技巧的. 现在其实对于Array的考察非常烦人. 这一块比较简单所以没什么可考的, 一旦考的话, 就是这种奇淫技巧. 其实这种技巧工作和学习之中用途基本没有, 而且适用的题型也很少. 

之所以想记录一下这个技巧是觉得其还是有一定的适用性, 也许以后能够用到. 

**方法总结**

一般游标卡尺类题目都是具有特殊性的. 一般都是两个指针, 从low和high, 头尾开始慢慢往里面卡. 这种题目通常都是array, 一般都具有一定特殊性. 

## 相向指针

相向指针的意思是两个指针从两端慢慢向中间走.  这种最常见.  有三种情况, 第一种是以两个指针相遇作为结尾, 第二种是以两个指针之间的元素去判断, 第三种是用sorted array, 只取两个指针的值来判断, 和两个指针之间的元素无关. 

### Longest Substring Without Repeating Characters LC_03

就是这道题其实当时baanyan第一天还跟老师怼上了. 因为我当时说我用hashmap能解而且算力上并不慢. 现在想想应该是我错了. 我今天想了半天也没想到hashmap怎么能做出和这个标准答案算力一样的解法. **所以说, 做人做学问还是应该虚心一点, 尾巴收起来**. 我当时之所以瞧不上老师的解法是因为我当时(其实现在也存在)打心底瞧不起这种只适用于一道或者几道题的奇淫技巧, 觉得这种东西花拳绣腿, 学的比较鸡肋. 

老师当时称这个解法为"双指针", LC称这个解法为Sliding Window, 我更喜欢称之为游标卡尺. 

**Problem Description**

Given a string s, find the length of the longest substring without repeating characters.

Example 1:

> Input: s = "abcabcbb"  
> Output: 3  
> Explanation: The answer is "abc", with the length of 3.

Example 2:

> Input: s = "bbbbb"  
> Output: 1  
> Explanation: The answer is "b", with the length of 1.

**Code**

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        Set<Character> hs = new HashSet<>();
        int answer=0, i=0, j=0;
        
        while(i<n && j<n)
        {
            if(!hs.contains(s.charAt(j)))
            {
                hs.add(s.charAt(j));
                j++;
                if(hs.size()>answer)
                {
                    answer = hs.size();
                }
            }
            else{
                hs.remove(s.charAt(i));
                i++;
            }
        }
        return answer;
    }
}
```

**Algorithm**

直接看以上这个code会比较迷, 我当时看答案也是看了很久没看明白. 其实自己在纸上写了一下很容易想明白. 

其实这个算法并不难, 也不玄乎, 反而比较实际, 容易理解.  把Set hs想象成一把游标卡尺, 卡尺的左端是i, 右端是j. 
假设我们有一个String  ABCDAE

从A点出发, i和j都在0, 也就是A, 只要下一个char没有重复, 游标卡尺的右端就不断往下一个char走. 如上面的例子, 游标卡尺走到ABCDA, j = 4的时候会停住.  这个时候从A点出发的不重复subString已经到了Max. 这个时候把尺子右端不动, 把卡尺左端往后挪一位. 我们得到 BCDA. 之后下一位还是不重复的E, 再挪右端j, 左端i不动. 得到BCDAE. 这个过程中keep tracking 卡尺的max长度. 最后得到答案5. 

两点: 

1. 一开始会考虑要不要向前track, 其实想一下完全没有必要. 这个理解就是和DP是一样的, 因为之前的元素已经被卡尺求过了, 没有必要向前. 所有的subString都是向后track. 
2. 一开始是在想是不是要在每个字母上卡一下, 是不是一旦出现了重复元素之后, 就立刻要把尺子收紧把左端右端合在一起然后重新测量, 会把else写成这样: 

	```java
	else{
	    hs = new HashSet<>();
	    i++;
	    j=i;
	}
	```
	
	举个例子: ABCBD 这个, 一开始尺子卡在ABC, 然后在B发现重复, 尺子收起来, 从B(i=1)开始重新卡. 我会这么想, 其实这么想也比较直观. 
	
	其实实际上没有必要. **关键在于这个尺子里面的元素是不可重复的**, 也就是说尺子内部的元素是绝对干净的. 这个时候没有必要收尺子, 尺子左端已经在正确的位置, 只要继续挪动右端就可以了. 
	
还有一些更快的解法, 游标卡尺加上hashmap的解法, 不想去学了. 这种奇淫技巧学的差不多就可以. 目前阶段没必要学最优解, 现在主要是大量刷. 

### Container With Most Water LC_011

**Problem Description**

题目不放了, 因为需要看图才能看懂, 直接去[LeetCode](https://leetcode.com/problems/container-with-most-water/)上面看吧. 

**Algorithm**

这道题我拿来首先想到的就是dynamic programming, 但越想越觉得不符合dynamic的求和原则, 因为需要考虑之前的所有边.   

算法是游标卡尺, 这一次的游标卡尺是从首尾两端开始卡, 慢慢往里面收. 由于题目的特殊性而使用木桶原理.  

**这种特殊的题目没什么好说的, 唯有刷脸.**

<br>

**Code**

```java
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0, left = 0, right = height.length -1;
        
        while(right>left)
        {
            maxArea = Math.max(maxArea, Math.min(height[left], height[right])*(right-left));
            //System.out.println(left + " , " + right + " , " + maxArea);
            if(height[left]>height[right])
            {
                right--;
            }
            else
            {
                left ++;
            }
        }
        return maxArea;
    }
}
```

### Two Sum II - Input array is sorted LC_167

**Problem Description**

[LC167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

**Algorithm**

又是一道很巧妙的游标卡尺题.  array是sorted. 难点是要想明白这个卡尺不会漏掉解. 其实这也算不上什么难点, 游标卡尺就是这样, 主要在于背, 见过了, 记下来, 就能写出来, 没见过, 没印象, 想死也写不出来. 

**Code**

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        
        int low = 0; 
        int high = numbers.length-1;
        
        while (high > low){
            if(numbers[low] + numbers[high]==target){
                return new int[] {low+1, high+1};
            }
            else if(numbers[low] + numbers[high] > target){
                high --;
                    
            }
            else{
                low ++;
            }
        }
        
        return new int[] {0,0};
        
    }
}
```

### 3Sums LC15

可以算是这个类型最高难度了.  不过没有普遍适用性, 所以其实不推荐. 

其实就是按照2SumII的双指针去进行的, 区别是要引入第三个量, 做一些相应的调整. 其实也就是用第三个量卡一下而已. 增加一层维度. 

需要注意的是, 下面加注释的部分, 其他看leetcode标准答案就好, 有动画, 说的很详细了, 不再赘述.

- 2021-05-07 2刷通过. 

**code**

```java
class Solution {
    List<List<Integer>> output;
    public List<List<Integer>> threeSum(int[] nums) {
        output = new ArrayList<>();
        Arrays.sort(nums);
        
        // nums[i]<=0 的这个条件是因为, 双指针是向右卡的, low 和high的相应值都大于i. 
        // 所以一旦大于0就不可能有解了, 没必要继续traverse下去. 
        for(int i=0; i<nums.length-1 && nums[i]<=0; i++){
            if(i==0 || nums[i]!=nums[i-1]){
           	    // 上面这个if只有一个目的, 就是去重. 去重的原因是这道题的条件不让重复. 
           	    // 去重的原理是之前的sort, 因为sort, 所以只要查相邻是不是重复即可. 
                twoSum(nums, i);
            }
        }
        return output;
    }
    
    private void twoSum(int[] nums, int i)
    {
        //System.out.println(nums[i]);
        
        int curr = nums[i];
        int low = i+1;
        int high = nums.length-1;
        //System.out.println(curr + " " + nums[low] + " " + nums[high]);
        
        
        while(low<high)
        {
            int sum = curr + nums[low] + nums[high];
            if(sum>0){
                high--;
            }else if(sum<0){
                low ++;
                //System.out.println(nums[low]);
            }else{
                List<Integer> list = new ArrayList<>();
                list.add(nums[i]);
                list.add(nums[low++]);
                list.add(nums[high--]);
                output.add(list);
                // 这个while loop是twoSumII里没有的. 
                // 加这个的原因是, 这道题不是唯一解的, 就算两个指针卡到了, 也可能往下继续卡有其他解. 
                // 之前twoSumII没有加这个while loop调整指针继续往下卡的原因是twoSumII的题就设定是单解. 
                while(low<nums.length-1 && nums[low] == nums[low-1]){
                    low++;
                }
            }
        }
    }
}
```

## 同向指针

两个指针走的方向一样. 跟上面的相向正好相反.  这种一般是两个指针之间卡着一个特定的值, 每次走了之后检测两个指针之间的元素是否符合标准. 

### LC438_Find All Anagrams in a String

这道题挺有意思的, 不算特别吧. 思路其实想想也不难, 看答案不到10分钟就能懂.  这道题关键的是这个思路, **HashMap是可以比较的**, 有了这个思路之后很多题都可以利用这个思路比,**尤其是那种乱序的比较, 只比较元素不比较顺序的, 都可以用这个思路**: 

- key 和 value完全一样的两个HashMap就是完全相同的, 
- key, value=0 和 没有这个key和value是两回事, 不相等. 

官方答案太啰嗦, 自己改了改, 放在下面. 

- 2021-05-17 第一次

```java
class Solution {
  public List<Integer> findAnagrams(String s, String p) {
    int ns = s.length(), np = p.length();
    if (ns < np) return new ArrayList();

    Map<Character, Integer> pMap = new HashMap();
    Map<Character, Integer> sMap = new HashMap();
    // build reference hashmap using string p
    for(char c: p.toCharArray()){
        pMap.put(c, pMap.getOrDefault(c,0) + 1);
    }

    List<Integer> output = new ArrayList();
    // sliding window on the string s
    for (int i = 0; i < ns; ++i) {
      // add one more letter 
      // on the right side of the window
      char c = s.charAt(i);
      sMap.put(c, sMap.getOrDefault(c,0) + 1);
      // remove one letter 
      // from the left side of the window
      if (i >= np) {
        char ch = s.charAt(i - np);
        if (sMap.get(ch) == 1) {
          sMap.remove(ch);
        }
        else {
          sMap.put(ch, sMap.get(ch) - 1);
        }
      }
      // compare hashmap in the sliding window
      // with the reference hashmap
      if (pMap.equals(sMap)) {
        output.add(i - np + 1);
      }
    }
    return output;
  }
}
```
## LC581_Shortest Unsorted Continuous Subarray

 上来基本思路是没错的. 自己写了双指针, 但发现有edge case解决不了. 看了答案调整之后crystal clear. 答案有用Stack做的最优解, 我没学, 看起来挺特殊的, 有时间的话, 可以学一下, 没时间就算了. 
 
 下面代码基本完全是自己写的, 比标准答案易读, 思路是一样的. 

```java
class Solution {
    private Integer low;
    private Integer high;
    int n;
    public int findUnsortedSubarray(int[] nums) {
        this.n = nums.length;
        int[] sNums = nums.clone();
        Arrays.sort(sNums);
        
        for(int i=0; i<n; i++)
        {
            if(nums[i]!=sNums[i]){
                low = i;
                break;
            }                
        }
        if(low == null)
            return 0;
        
        for(int i=low+1; i<n; i++)
        {
            if(nums[i]<sNums[i]){
                high = i;
            }  
        }

        
        return high-low+1;
    }
}
```

- Time complexity : O(nlogn). Sorting takes  nlogn time.

- Space complexity : O(n). We are making n copy of original array.




## 快慢针

### LC876_Middle of the Linked List

一道很纯粹的快慢针问题. 快针是慢针速度的两倍.  纯粹的太简单了.  有兴趣可以看一下148题, 比这个稍微复杂一些, 需要处理edge case. 

**code**

```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while(fast!=null && fast.next!=null)
    {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow; 
}
```

### LC19_Remove Nth Node From End of List

这道题严格意义上来说感觉应该不算快慢针. 其实这道题的指针是一个先走, 另一个后走.  以后可以考虑把这一道从这个归类之中移除. 

一道在LinkedList上的快慢指针. 一开始看很简单, 其实不然. 思路很简单, 但具体edge case很特殊, 不好处理. 需要考虑的是只有一个元素和remove head的情况, 所以加装这个dummy head. 

**19题, 1721题, 1474 这三道题同宗同源**. 其中最难的是19题, 需要考虑的稍微多一些.  如果要刷的话, 就可19题刷吧. 

**code**

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
	 // 这个dummyHead不是没有意义的. 加装dummyHead的意义是为了处理remove head和只有一个元素的情况. 
	 // 这个算法必须有三个元素的时候才有用.  加装dummyhead之后, 在有一个元素的情况下是, dummyHead, head, null(可以允许一个null)
	 // 本身思路并不难, edge case 很不好处理. 
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy;
    ListNode second = dummy;
    // Advances first pointer so that the gap between first and second is n nodes apart
    for (int i = 1; i <= n + 1; i++) {
        first = first.next;
    }
    // Move first to the end, maintaining the gap
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummy.next;
}
```

