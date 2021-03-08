
---
title: Python 程序以查找两个列表的交集
author: 知识铺
date: 2021-03-08 10:34:46+08:00
tags: []
---


交叉操作意味着，我们必须从列表 1 和列表 2 中接收所有常见元素，并将所有元素存储在另一个第三个列表中。

List1::[1,2,3]
List2::[2,3,6]
List3::[2,3]

## 算法

Step 1: input lists.
Step 2: first traverse all the elements in the first list and check with the elements in the second list.
Step 3: if the elements are matched then store in third list.

## 示例代码

```
#Intersection of two lists 
def intertwolist(A, B):
   C = [i for i in A if i in B]
   return C
# Driver Code
A=list()
B=list()
n=int(input("Enter the size of the List ::"))
print("Enter the Element of first list::")
for i in range(int(n)):
   k=int(input(""))
   A.append(k)
print("Enter the Element of second list::")
for i in range(int(n)):
   k=int(input(""))
   B.append(k)
print("THE FINAL LIST IS ::>",intertwolist(A, B))
```
## 输出
```
Enter the size of the List ::5
Enter the Element of first list::
12
23
45
67
11
Enter the Element of second list::
23
45
88
11
22
THE FINAL LIST IS ::> [23, 45, 11]
```
