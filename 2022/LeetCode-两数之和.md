---
title: LeetCode-两数之和
categories: 
  - Tech
tags: 
  - Algorithm
keywords: 
description: LeetCode-两数之和
date: 2022-06-20 23:29:43
abbrlink: 20220620
---

题目：
给定一个整数数组`nums`和一个整数目标值`targe`，请你在该数组中找出**和**为目标值 `target` 的那两个整数，并返回它们的数组下标。

ps1：你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

ps2：你可以按任意顺序返回答案。

## 我的思路

1. 首先可以肯定一点：寻找整数数组`nums`中的某个或者某几个元素，必然需要通过下标，进行数组的遍历操作。

2. 假设这个数组中有两个元素的下标分别是`i`和`j`，正好满足`nums[i] + nums[j] == target `，那么我就可以说，`i`和`j`就是要寻找的答案。

3. 为了找到索引`i`和`j`，需要进行如下遍历：

   1. 假设遍历的索引为`i`，它需要从索引0开始，一直遍历到数组的最后一个元素，即`nums[nums.length - 1]`；
   2. 在第一次遍历过程中，每一次确定索引`i`的位置，都需要将索引`i`后面的元素分别与其相加，并判断是否等于target；

   ```java
   for(int i=0;i<nums.length-1;i++){
       for(int j=i+1;j<nums.length;j++){
           if(nums[i] + nums[j] == target){
               //i和j即为所求
           }
       }
   }
   ```

4. 全量的代码如下：

   ```java
   public int[] twoSum(int[] nums, int target) {
       for(int i=0;i<nums.length-1;i++){
           for(int j=i+1;j<nums.length;j++){
               if(nums[i] + nums[j] == target){
                   return new int[]{i,j};
               }
           }
       }
       return null;
   }
   ```

   当然，这属于一种暴力破解的方式。其核心逻辑在于，对数组中的元素进行数学逻辑上的**组合**，以穷尽遍历的方式找到符合要求的数据。

   其中，用到的变量只有固定的`i`和`j`，所以空间复杂度为：$O(1)$。

   由于采用的是循环嵌套循环的方式，所以时间复杂度为：$O(n^2)$。