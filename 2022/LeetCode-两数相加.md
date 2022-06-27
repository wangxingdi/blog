---
title: LeetCode-两数相加
categories: 
  - Tech
tags: 
  - Algorithm
keywords: 
description: LeetCode-两数相加
date: 2022-06-27 23:11:34
abbrlink: 20220627
---

题目：
给你两个**非空**的链表，表示两个非负的整数。它们每位数字都是按照**逆序**的方式存储的，并且每个节点只能存储**一位**数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

> 输入：l1 = 2->4->3 = [2,4,3], l2 = 5->6->4 = [5,6,4]
> 输出：[7,0,8]
> 解释：342 + 465 = 807

## 我的思路

感觉这道题目，考察细心多于算法，因为这个题目的编码逻辑，就是数学加法运算的抽象。

1. 从个位开始，将两个个位数进行相加，得出结果为个位，如果有进位，则记录进位；
2. 然后是十位，继续上述逻辑；
3. 直到两个数字的所有位都计算完毕，得出最终结果。

需要特别注意的是：

* 两个数字的长度很可能不一致，所以需要用0来补位计算；
* 计算完毕之后，需要注意是否有进位；

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode result = new ListNode(0);
    ListNode step = result;
    //进位
    int carry = 0;
    while(l1!=null || l2!=null){
        int a = null==l1 ? 0 : l1.val;
        int b = null==l2 ? 0 : l2.val;
        int sum = a + b + carry;
        carry = sum / 10;

        step.next = new ListNode(sum % 10);
        step = step.next;

        l1 = null==l1 ? null : l1.next;
        l2 = null==l2 ? null : l2.next;
    }
    if(carry!=0){
        step.next = new ListNode(carry);
    }
    return result.next;
}
```

