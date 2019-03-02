---
layout: blog
title: 2. Add Two Numbers
date: 2019年3月1日17:50:54
tags: linked-list math
categories: LeetCode
---
# 读题的时候不认真看题

写的时候就会完全按照自己**想象**中的题目去解题

这道题两个数字明明是已经逆向好给我做加法了

我还傻呵呵地先写了一遍 把两个链表逆向了一遍

另外

java也不太懂

# reflections
5+5的情况WA了一次

没有想到这样的情况

# myCode
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int carry = 0;
        boolean conti = true;
        ListNode ret = new ListNode(0), al1 = l1, al2 = l2;
        ListNode r = ret;
        while (conti) {
            int a1 = 0, a2 = 0;
            if (al1!=null) {
                a1 = al1.val;
                al1 = al1.next;
            }
            if (al2!=null) {
                a2 = al2.val;
                al2 = al2.next;
            }
            int sum = a1 + a2 + carry;
            if (sum>=10) {
                sum -= 10;
                carry = 1;
            }else {
                carry = 0;
            }
            ret.val = sum;
            if (al1==null && al2==null && carry==0) conti = false;
            if (conti) {
                ret.next = new ListNode(0);
                ret = ret.next;
            }
        }
        return r;
    }
}
```

# Official
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0);
    ListNode p = l1, q = l2, curr = dummyHead;
    int carry = 0;
    while (p != null || q != null) {
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;
}
```
真的是短小精悍啊！

