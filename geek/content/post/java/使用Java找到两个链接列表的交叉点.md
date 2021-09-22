
---
title: 使用Java找到两个链接列表的交叉点
author: 知识铺
date: 2021-03-08 10:24:44+08:00
tags: []
---

链接列表是一个线性数据结构，其中每个Node有两个块，这样一个块包含Node的值或数据，而另一个块包含下一个字段的地址。

让我们假设我们有一个链接列表，以便每个Node都包含指向列表中其他Node的随机指点。任务是找到两个链接列表相互交集的Node。如果他们不相交，然后返回空或空作为输出。

**例如**

**输入-1：**

**![](https://www.tutorialspoint.com/assets/questions/media/48701/1.png)**

**输出：**

2

**说明：**由于给定的链接列表在Node与值"2"相交，我们将将值"2"返回为输出。

**输入-2：**

**          ![](https://www.tutorialspoint.com/assets/questions/media/48701/1.1.png)**

**输出：**

NULL

**说明：**由于没有共同点，在这种情况下，我们将返回空。

## 解决这个问题的方法

我们有两个链接列表，它们彼此相交的一个共同点。要找到交汇点，我们将通过两个链接列表，直到我们发现它们同样指向相同的值。在某些时候，链接列表下一个Node的指点将相同。因此，我们将返回这一点的价值。

*   拿两个链接列表与数据和指点到下一个Node。
*   函数常用点（列表Node*headA、列表Node*headB）分别采用链接列表的两个指点，并返回链接列表的共性或交叉点的值。
*   查找链接列表长度的整数函数将从列表的头返回两个链接列表的长度。
*   现在创建一个指向两个列表的标题的指点，并穿过其长度较大的列表，直到（第一个列表的长度 - 第二个列表的长度）。
*   现在通过列表，直到我们发现下一个指点是相等的。
*   返回该特定Node的值，其中两个列表相交。

## 例子

[实时演示](https://zshipu.com/t?url=http://tpcg.io/Mb2SPXCS)
```
public class Solution {
   static listnode headA,
   headB;
   static class listnode {
      int data;
      listnode next;
      listnode(int d) {
         data = d;
         next = null;
      }
   }
   int count(listnode head) {
      int c = 0;
      while (head != null) {
         c++;
         head = head.next;
      }
      return c;
   }
   int commonPoint(listnode headA, listnode headB) {
      listnode p1 = headA;
      listnode p2 = headB;
      int c1 = count(headA);
      int c2 = count(headB);
      if (c1 > c2) {
         for (int i = 0; i < c1 - c2; i++) {
            if (p1 == null) {
               return - 1;
            }
            p1 = p1.next;
         }
      }
      if (c1 < c2) {
         for (int i = 0; i < c2 - c1; i++) {
            if (p2 == null) {
               return - 1;
            }
            p2 = p2.next;
         }
      }
      while (p1 != null &amp;&amp; p2 != null) {
         if (p1.data == p2.data) {
            return p1.data;
         }
         p1 = p1.next;
         p2 = p2.next;
      }
      return - 1;
   }
   public static void main(String[] args) {
      Solution list = new Solution();
      list.headA = new listnode(5);
      list.headA.next = new listnode(4);
      list.headA.next.next = new listnode(9);
      list.headA.next.next.next = new listnode(7);
      list.headA.next.next.next.next = new listnode(1);
      list.headB = new listnode(6);
      list.headB.next = new listnode(7);
      list.headB.next.next = new listnode(1);
      System.out.println(list.commonPoint(headA, headB));
   }
}
```
运行上述代码将生成输出，

## 输出

7

**说明**：给定的链接列表在 7 点相交。

![](https://www.tutorialspoint.com/assets/questions/media/48701/1.e.png)

