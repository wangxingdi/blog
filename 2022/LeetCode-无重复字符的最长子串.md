---
title: LeetCode-无重复字符的最长子串
categories: 
  - Tech
tags: 
  - Algorithm
keywords: 
description: LeetCode-无重复字符的最长子串
date: 2022-07-15 00:25:19
abbrlink: 20220715
---

题目：
给定一个字符串`s`，请你找出其中**不含有重复字符**的**最长子串**的长度。

> 示例 1：
>
> 输入：s = "abcabcbb"
> 输出：3 
> 解释：因为无重复字符的最长子串是 "abc"，所以其长度为 3。



> 示例 2：
>
> 输入：s = "bbbbb"
> 输出：1
> 解释：因为无重复字符的最长子串是 "b"，所以其长度为 1。



> 示例 3：
>
> 输入：s = "pwwkew"
> 输出：3
> 解释：因为无重复字符的最长子串是 "wke"，所以其长度为 3。请注意，你的答案必须是子串的长度，"pwke" 是一个子序列，不是子串。



```java
public int lengthOfLongestSubstring(String s) {
    if(null==s || s.length()==0){
        return 0;
    }
    int left = 0;
    Map<Character, Integer> map = new HashMap();
    int max = 0;
    for(int right=0;right<s.length();right++){
        if(map.containsKey(s.charAt(right))){
            left = Math.max(left, map.get(s.charAt(right)) + 1);
        }
        map.put(s.charAt(right), right);
        max = Math.max(max, right - left + 1);
    }
    return max;
}
```

