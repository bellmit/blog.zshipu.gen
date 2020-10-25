---
title: JavaScript基础：为初学者学习 JavaScript 中的数据结构
author: 知识铺
date: 2020-10-25 13:32:14+08:00
tags: [js]
---

# <font _mstmutation="1" _msthash="33358" _msttexthash="5211505">介绍</font>

<font _mstmutation="1" _msthash="28236" _msttexthash="1179803599">它是 JavaScript 中学习数据结构的注释。我研究了长途跋涉[的](https://zshipu.com/t?url=https://github.com/trekhleb)Github 存储库的源代码表单。对于JavaScript开发人员和初学者来说，这是一个很好的材料来学习数据结构。</font>

<font _mstmutation="1" _msthash="34632" _msttexthash="758505358">除了[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github， 我还提到[《离开： 乌迪米编程](https://zshipu.com/t?url=https://www.udemy.com/course/break-away-coding-interviews-1/)和编码采访》和哈克兰克的视频。本课程使用 Java 实现和解释数据结构。</font>

<font _mstmutation="1" _msthash="23283" _msttexthash="59199426">本文总结并包括以下数据结构。</font>

1. [链接列表](#06d3)
2. [双链接列表](#4087)
3. [队列](#505b)
4. [堆栈](#bf9b)
5. [哈希表](#8804)
6. [二进制搜索树](#de8c)
7. [二进制堆](#f25c)

<font _mstmutation="1" _msthash="33475" _msttexthash="489009352">下表显示了常见操作的时间复杂性。堆栈和队列的实现基于链接列表。它们允许用户有效地插入或删除节点。</font>

<font _mstmutation="1" _msthash="39650" _msttexthash="523313804">为了具有更好的遍历整个容器的性能，我们可以考虑使用哈希表或二进制搜索树。这取决于您是否要订购数据。</font>

+---+-----------------+-----------------+-----------------+
|   |     Insert      |     Delete      |    Traverse     |
+---+-----------------+-----------------+-----------------+
| 1 | O(1)            | O(1)            | O(n)            |
| 2 | O(1)            | O(1)            | O(n)            |
| 3 | O(1)            | O(1)            | O(n)            |
| 4 | O(1)            | O(1)            | O(n)            |
| 5 | O(1)~O(n)       | O(1)~O(n)       | O(1)~O(n)       |
| 6 | O(log n)~O(n)   | O(log n)~O(n)   | O(log n)~O(n)   |
| 7 | O (log n)       | O (log n)       | O(n)            |
+---+-----------------+-----------------+-----------------+

# <font _mstmutation="1" _msthash="28314" _msttexthash="16240692">1\. 链接列表</font>

<font _mstmutation="1" _msthash="27677" _msttexthash="47718164">单个链接列表是单向列表。</font>

<font _mstmutation="1" _msthash="22581" _msttexthash="197178332">链接**列表**的优点是允许用户在恒定时间有效地插入或删除节点。</font>

<font _mstmutation="1" _msthash="27612" _msttexthash="602649359">但是，链接**列表不善于访问数据**。我们不允许访问链接列表中具有索引的数据。我们只能通过遍历容器来查找目标数据。</font>

+-------------+----------+---------+----------+-------------------+
|  operations |  Insert  |  Delete | Traverse | Search and Delete |
+-------------+----------+---------+----------+-------------------+
|  complexity |   O(1)   |   O(1)  |   O(n)   |         O(n)      |
+-------------+----------+---------+----------+-------------------+

<font _mstmutation="1" _msthash="34593" _msttexthash="286714363">在本节中，我参考源代码[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github，并用我个人的想法进行一些修改。</font>

## <font _mstmutation="1" _msthash="28860" _msttexthash="25170626">JavaScript 中的实现</font>

1. <font _mstmutation="1" _msthash="27248" _msttexthash="72790497">在 JavaScript 中创建链接列表结构</font>

<font _mstmutation="1" _msthash="40768" _msttexthash="370088394">单个链接列表具有头节点和尾部节点。每个节点都有一个值字段和一个指向下一个节点的指针</font>

![Image for post](https://miro.medium.com/max/60/1*s2BtOpXw92Y9qG-PEMgOsA.png?q=20)

![Image for post](https://miro.medium.com/max/1132/1*s2BtOpXw92Y9qG-PEMgOsA.png)

<noscript>![Image for post](https://miro.medium.com/max/2264/1*s2BtOpXw92Y9qG-PEMgOsA.png)</noscript>

<font _mstmutation="1" _msthash="3440060" _msttexthash="17203927">复制right@A莱曼</font>

<font _mstmutation="1" _msthash="39624" _msttexthash="37142183">数据结构的实现：</font>
```
class Node {
    constructor(value = null) {    
        this.value = value;    
        this.next = null;  
    }
}
class LinkedList {
    constructor() {
        this.head = null;    
        this.tail = null;     
    }
}
```
<font _mstmutation="1" _msthash="22464" _msttexthash="5707962">2.插入</font>

<font _mstmutation="1" _msthash="34905" _msttexthash="68291301">有两种不同的方法来插入新节点。</font>

* <font _mstmutation="1" _msthash="27742" _msttexthash="372751405">将新节点放在尾部节点后面。如果我们没有尾节点指针，我们必须转到链接列表的末尾。</font>
* <font _mstmutation="1" _msthash="29133" _msttexthash="232914669">时间复杂性为 O（1） 或 O（n）。这取决于我们如何实现链接列表。</font>

![Image for post](https://miro.medium.com/max/60/1*--2RceE3ISEZB-AuipUYiw.png?q=20)

![Image for post](https://miro.medium.com/max/1502/1*--2RceE3ISEZB-AuipUYiw.png)

<noscript>![Image for post](https://miro.medium.com/max/3004/1*--2RceE3ISEZB-AuipUYiw.png)</noscript>

<font _mstmutation="1" _msthash="3440061" _msttexthash="17203927">复制right@A莱曼</font>
```
append(value) {    
    const newNode = new node(value);    
    if (!this.head) {      
       this.head = newNode;      
       this.tail = newNode;       
       return this;    
    }    
    this.tail.next = newNode;    
    this.tail = newNode;     
    return this;  
}
```
*   <font _mstmutation="1" _msthash="34619" _msttexthash="143043836">从头节点插入新节点（复杂性：O（1））</font>
```
prepend(value) {    
    const newNode = new Node(value);
    newNode.next = this.head  
    this.head = newNode;     
    if (!this.tail) {      
        this.tail = newNode;    
    }     
    return this;  
}
```
<font _mstmutation="1" _msthash="24206" _msttexthash="118492946">3.删除头节点（复杂度：O（1））</font>
```
deleteHead() {   
    if (!this.head) {
        return null;
    }const delete = this.head;
    if (this.head.next) {
        this.head = this.head.next;
    } else {
        this.head = null;
        this.tail = null;
    }return delete;
}
```
<font _mstmutation="1" _msthash="22984" _msttexthash="144191411">4.搜索/访问/遍历（复杂度：O（n））</font>

<font _mstmutation="1" _msthash="32968" _msttexthash="168380342">浏览整个列表并返回目标节点，目标值或回调函数返回 true</font>
```
find({value = undefined, callback = undefined}) {   
    if (!this.head) {
        return null;
    }let currentNode = this.head;
    while (currentNode && currentNode.next) {
        if (callback && callback(currentNode.value)) {
            return currentNode;
        }if (currentNode.value === value) {
            return currentNode;
        }
        currentNode = currentNode.next;
    }
    return null;
}
```
<font _mstmutation="1" _msthash="33137" _msttexthash="117819949">5.搜索和删除（复杂性：O（n））</font>

<font _mstmutation="1" _msthash="37284" _msttexthash="258634415">删除操作必须遵循这些顺序，因为链接列表没有指向上一个节点的指针。</font>

* <font _mstmutation="1" _msthash="39338" _msttexthash="80177838">如果值等于目标值，则删除头节点</font>
* <font _mstmutation="1" _msthash="23972" _msttexthash="89500801">如果值等于目标值，则删除直接节点</font>
* <font _mstmutation="1" _msthash="22711" _msttexthash="90824435">如果值等于目标值，则删除尾部节点</font>

```
delete(value) {    
    if (!this.head) {      
        return null;    
    }

    //Check the head node if the value is the target value
    let deletedNode = null;
    if (this.head.value === value) {
        deletedNode = this.head;
        this.head = this.head.next;
    }    

    //Check immediate node if the value is the target value
    let currentNode = this.head;     
    while (currentNode.next) {        
        if (currentNode.next.value === value) {                       
            deletedNode = currentNode.next;    
            currentNode.next = currentNode.next.next;        
        } else {          
            currentNode = currentNode.next;        
        }      
    }

    //Check the tail node if the value is the target value
    if (this.tail.value === value) {      
        this.tail = null;    
    }     
    return deletedNode;  
}
```

## <font _mstmutation="1" _msthash="33098" _msttexthash="5334199">引用</font>

* [数据结构：链接列表](https://zshipu.com/t?url=https://www.youtube.com/watch?v=njTh_OwMljA&index=2&t=1s&list=PLLXdhg_r2hKA7DPDsunoDZ-Z769jWn4R8)

# <font _mstmutation="1" _msthash="23426" _msttexthash="20305285">2\. 双链接列表</font>

<font _mstmutation="1" _msthash="30186" _msttexthash="800125794">双链接列表是双向列表。它有一个额外的指针，称为**上一个指针来链接上一个节点。链接列表和双重列表之间的主要区别是搜索和删除操作。**</font>

+-------------+----------+---------+----------+-------------------+
|  operations |  Insert  |  Delete | Traverse | Search and Delete |
+-------------+----------+---------+----------+-------------------+
|  complexity |   O(1)   |   O(1)  |   O(n)   |         O(n)      |
+-------------+----------+---------+----------+-------------------+

<font _mstmutation="1" _msthash="34099" _msttexthash="334395451">在本节中，我参考[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github 上的源代码，并用我个人的想法进行一些修改。</font>

## <font _mstmutation="1" _msthash="24037" _msttexthash="25170626">JavaScript 中的实现</font>

<font _mstmutation="1" _msthash="28626" _msttexthash="79747616">1.在 JavaScript 中创建链接列表结构</font>

<font _mstmutation="1" _msthash="29497" _msttexthash="755907503">双链接列表具有头和尾部节点。节点具有一个值、指向下一个节点的指针**以及指向上一个节点的上一个与链接列表不同的上一个节点的指针**。</font>

![Image for post](https://miro.medium.com/max/60/1*u1VQwgxt8WiRPxlE5HcQTw.png?q=20)

![Image for post](https://miro.medium.com/max/1410/1*u1VQwgxt8WiRPxlE5HcQTw.png)

<noscript>![Image for post](https://miro.medium.com/max/2820/1*u1VQwgxt8WiRPxlE5HcQTw.png)</noscript>

<font _mstmutation="1" _msthash="3981601" _msttexthash="17203927">复制right@A莱曼</font>
```
 class Node {
    constructor(value = null) {    
        this.value = value;    
        this.next = null;    
        **this.previous = previous;**
    }
}class DoublyLinkedList {
    constructor() {
        this.head = null;    
        this.tail = null;     
    }
}
```
<font _mstmutation="1" _msthash="22867" _msttexthash="87770423">2.插入（复杂度：O（1））</font>

<font _mstmutation="1" _msthash="22568" _msttexthash="68291301">有两种不同的方法来插入新节点。</font>

* <font _mstmutation="1" _msthash="28002" _msttexthash="427680045">将新节点放在尾部节点后面。它与链接列表相同。**区别在于将新节点的上一个指针设置为尾部节点。**</font>

```
append(value) {    
    const newNode = new node(value);    
    if (!this.head) {      
       this.head = newNode;      
       this.tail = newNode;       
       return this;    
    }    
    this.tail.next = newNode;
    **newNode.previous = this.tail;   ** 
    this.tail = newNode;     
    return this;  
}
```

* <font _mstmutation="1" _msthash="28431" _msttexthash="351929318">从头节点插入新节点。它与链接列表相同。**区别在于将头节点的上一个指针设置为新节点。**</font>

```
prepend(value) {    
    const newNode = new LinkedListNode(value);
    newNode.next = this.head 
    **if (this.head) {
        this.head.previous = newNode;
    }**
    this.head = newNode;     
    if (!this.tail) {      
        this.tail = newNode;    
    }     
    return this;  
}
```

<font _mstmutation="1" _msthash="28106" _msttexthash="118093807">3.从头部删除（复杂度：O（1））</font>

**区别在于将头节点的上一个指针设置为 null。**

```
deleteHead() {   
    if (!this.head) {
        return null;
    }const delete = this.head;
    if (this.head.next) {
        this.head = this.head.next;
        **this.head.previous = null;**
    } else {
        this.head = null;
        this.tail = null;
    }return delete;
}
```

<font _mstmutation="1" _msthash="24531" _msttexthash="144191411">4.搜索/访问/遍历（复杂度：O（n））</font>

**它与链接列表相同**

<font _mstmutation="1" _msthash="29900" _msttexthash="117819949">5.搜索和删除（复杂性：O（n））</font>

<font _mstmutation="1" _msthash="28925" _msttexthash="283085634">**与链接列表**不同，删除操作不必遵循顺序，因为双链接列表具有上一个指针。</font>
```
delete(value) {    
    if (!this.head) {      
        return null;    
    }    
    //Check the head node if the value is the target value
    let deletedNode = null;  
    let currentNode = this.head;while (currentNode) {
        if (currentNode === value) {
            deleteNode = currentNode;
            if (deleteNode === this.head) {
                this.head = this.head.next;
                if (this.head) {
                    this.head.previous = null;
                }
            } else if (deleteNode === this.tail) {
                this.tail = this.tail.previous;
                this.tail.next = null;
            } else {
                const previousNode = currentNode.previous;
                const nextNode = currentNode.next;
                previousNode.next = nextNode;
                nextNode.previous = previousNode;
            }
        }
        currentNode = currentNode.next;
    } 
    return deletedNode;  
}
```
# <font _mstmutation="1" _msthash="28756" _msttexthash="7237802">3\. 队列</font>

<font _mstmutation="1" _msthash="37791" _msttexthash="341501680">队列是基于链接列表的线性数据结构。队列的字符是它是一个 FIFO（先出）数据结构。</font>

+------------+------------------+-------------------+----------+
| operations | Insert (enqueue) | Delete  (dequeue) | Traverse |
+------------+------------------+-------------------+----------+
| complexity | O(1)             | O(1)              | O(n)     |
+------------+------------------+-------------------+----------+

<font _mstmutation="1" _msthash="32916" _msttexthash="334395451">在本节中，我参考[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github 上的源代码，并用我个人的想法进行一些修改。</font>

## <font _mstmutation="1" _msthash="43719" _msttexthash="25170626">JavaScript 中的实现</font>

<font _mstmutation="1" _msthash="28327" _msttexthash="81188328">1.在 JavaScript 中创建队列结构：</font>

<font _mstmutation="1" _msthash="37518" _msttexthash="396804421">我们可以使用链接列表来实现队列。我们将从尾部节点推送新节点，然后从头节点弹出节点。</font>

![Image for post](https://miro.medium.com/max/60/1*TsXXTI6mpet0pR5ZRNOmig.png?q=20)

![Image for post](https://miro.medium.com/max/1282/1*TsXXTI6mpet0pR5ZRNOmig.png)

<noscript>![Image for post](https://miro.medium.com/max/2564/1*TsXXTI6mpet0pR5ZRNOmig.png)</noscript>

<font _mstmutation="1" _msthash="3440062" _msttexthash="17203927">复制right@A莱曼</font>

<font _mstmutation="1" _msthash="38259" _msttexthash="37142183">数据结构的实现：</font>
```
class LinkedList {
    constructor() {
        this.head = null;    
        this.tail = null;     
    }
}class Queue {  
    constructor() {
        this.linkedList = new LinkedList();
    }
    isEmpty() {    
        return !this.linkedList.head;  
    }
    peek() {    
        if (!this.linkedList.head) {      
            return null;    
        }     
        return this.linkedList.head.value;  
    }
}
```
<font _mstmutation="1" _msthash="32565" _msttexthash="149135610">2\. 队列：将新节点添加到尾部节点（背面）</font>

![Image for post](https://miro.medium.com/max/60/1*E68JPnePhhRct2cbSDa7Qg.png?q=20)

![Image for post](https://miro.medium.com/max/1508/1*E68JPnePhhRct2cbSDa7Qg.png)

<noscript>![Image for post](https://miro.medium.com/max/3016/1*E68JPnePhhRct2cbSDa7Qg.png)</noscript>

<font _mstmutation="1" _msthash="3440063" _msttexthash="17203927">复制right@A莱曼</font>enqueue(value) {
this.linkedList.append(value);
}

<font _mstmutation="1" _msthash="28444" _msttexthash="162049862">3.取消队列：删除链接列表的头节点（正面）</font>

dequeue() {
const removedHead = this.linkedList.deleteHead();
return removedHead ? removedHead.value : null;
}

## <font _mstmutation="1" _msthash="22737" _msttexthash="5334199">引用</font>

* [数据结构：堆栈和队列](https://zshipu.com/t?url=https://www.youtube.com/watch?v=wjI1WNcIntg&list=PLLXdhg_r2hKA7DPDsunoDZ-Z769jWn4R8&index=3)

# <font _mstmutation="1" _msthash="38935" _msttexthash="6108154">4\. 堆栈</font>

<font _mstmutation="1" _msthash="38415" _msttexthash="451811113">与队列一样，堆栈是基于链接列表的数据结构。堆栈的特性是它是一个 LIFO（最后一个出）数据结构。</font>

+------------+------------------+-------------------+----------+
| operations | Insert (push)    | Delete  (pop)     | Traverse |
+------------+------------------+-------------------+----------+
| complexity | O(log 1)         | O(log 1)          | O(n)     |
+------------+------------------+-------------------+----------+

<font _mstmutation="1" _msthash="43459" _msttexthash="334395451">在本节中，我参考[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github 上的源代码，并用我个人的想法进行一些修改。</font>

## <font _mstmutation="1" _msthash="39780" _msttexthash="25170626">JavaScript 中的实现</font>

<font _mstmutation="1" _msthash="33840" _msttexthash="55265223">1.在 JavaScript 中创建堆栈结构</font>

<font _mstmutation="1" _msthash="38714" _msttexthash="394204642">我们可以使用链接列表来实现堆栈。我们将从尾部节点推送新节点，然后从头节点弹出节点。</font>

![Image for post](https://miro.medium.com/max/60/1*AJPFN7H2EqlBm3laPCNhzQ.png?q=20)

![Image for post](https://miro.medium.com/max/1276/1*AJPFN7H2EqlBm3laPCNhzQ.png)

<noscript>![Image for post](https://miro.medium.com/max/2552/1*AJPFN7H2EqlBm3laPCNhzQ.png)</noscript>

<font _mstmutation="1" _msthash="3440064" _msttexthash="17203927">复制right@A莱曼</font>

<font _mstmutation="1" _msthash="22360" _msttexthash="37142183">数据结构的实现：</font>
```
class LinkedList {
    constructor() {
        this.head = null;    
        this.tail = null;     
    }
}class Stack{  
    constructor() {
        this.linkedList = new LinkedList();
    }
    isEmpty() {    
        return !this.linkedList.head;  
    }
    peek() {    
        if (this.isEmpty()) {      
            return null;    
        }     
        return this.linkedList.head.value;  
    }
}
```
<font _mstmutation="1" _msthash="31265" _msttexthash="120087539">2.推送：将新节点追加到头节点上链接列表</font>

![Image for post](https://miro.medium.com/max/60/1*4S263aiULoySgpUb0SJdcA.png?q=20)

![Image for post](https://miro.medium.com/max/1476/1*4S263aiULoySgpUb0SJdcA.png)

<noscript>![Image for post](https://miro.medium.com/max/2952/1*4S263aiULoySgpUb0SJdcA.png)</noscript>

<font _mstmutation="1" _msthash="3440065" _msttexthash="17203927">复制right@A莱曼</font>
```
push(value) {    
    this.linkedList.prepend(value);  
}

<font _mstmutation="1" _msthash="29692" _msttexthash="78023868">3.弹出：删除链接列表的头节点</font>

pop() {
const removedHead = this.linkedList.deleteHead();
return removedHead ? removedHead.value : null;
}

```
# <font _mstmutation="1" _msthash="23296" _msttexthash="10672415">5.哈希表</font>

<font _mstmutation="1" _msthash="28847" _msttexthash="193576422">哈希表是基于数组的线性数据结构。它是值的关联列表的数组。</font>

+------------+-----------------+-----------------+-----------------+
| operations |     Insert      |     Delete      |    Traverse     |
+------------+-----------------+-----------------+-----------------+
| complexity | O(1) ~ O(n)     | O(1) ~ O(n)     | O(1) ~ O(n)     |
+------------+-----------------+-----------------+-----------------+

<font _mstmutation="1" _msthash="23166" _msttexthash="201186921">哈希**表**的优点是允许用户以恒定时间通过索引高效访问数据。</font>

key => lookup
"John" => Person(20, "man")
"merry" => Person(22, "woman")
...

<font _mstmutation="1" _msthash="40092" _msttexthash="250431571">它使用哈希键对数据进行索引，并使用不同的类型方法处理冲突问题。</font>

string -> hash code -> indexex. merry-> hash code -> 0hashTable[0] = Person(22, "woman")

<font _mstmutation="1" _msthash="34372" _msttexthash="334395451">在本节中，我参考[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github 上的源代码，并用我个人的想法进行一些修改。</font>

## <font _mstmutation="1" _msthash="23608" _msttexthash="10310521">哈希函数</font>

1.  <font _mstmutation="1" _msthash="34736" _msttexthash="107744767">预哈希： 使用 ASCII 代码将键转换为数字键</font>
2.  <font _mstmutation="1" _msthash="28405" _msttexthash="50053575">减少哈希数字以适应表大小</font>
```

hash(key) {
const hash = Array.from(key).reduce(
(hashAccumulator, keySymbol) => (hashAccumulator + keySymbol.charCodeAt(0)),0,);return hash % this.buckets.length;
}

```
## <font _mstmutation="1" _msthash="23609" _msttexthash="25170626">JavaScript 中的实现</font>

<font _mstmutation="1" _msthash="29432" _msttexthash="46059806">1.在 JavaScript 中创建哈希表</font>

*   <font _mstmutation="1" _msthash="34918" _msttexthash="148938478">使用数组将值存储在不同的链接列表中（链接）</font>
*   <font _mstmutation="1" _msthash="33514" _msttexthash="73814585">将**原始键****和值存储**到链接列表节点</font>
```

export default class HashTable {
constructor(hashTableSize = defaultHashTableSize) {
this.buckets = Array(hashTableSize).fill(null).map(() => new LinkedList());
this.keys = {};
}
}

```
 ![Image for post](https://miro.medium.com/max/60/1*TcULoQcv-VujZWljCoNgvQ.png?q=20)

![Image for post](https://miro.medium.com/max/1550/1*TcULoQcv-VujZWljCoNgvQ.png)

<noscript>![Image for post](https://miro.medium.com/max/3100/1*TcULoQcv-VujZWljCoNgvQ.png)</noscript>

<font _mstmutation="1" _msthash="3440066" _msttexthash="17203927">复制right@A莱曼</font>

<font _mstmutation="1" _msthash="36049" _msttexthash="131127061">2\. 插入（复杂度：O（1） = O（n））</font>

*   <font _mstmutation="1" _msthash="27821" _msttexthash="195284271">处理哈希冲突：使用链接列表存储具有相同原始密钥的新节点</font>
*   <font _mstmutation="1" _msthash="23322" _msttexthash="119051205">首先，我们使用哈希键来决定要存储哪个存储桶</font>
*   <font _mstmutation="1" _msthash="33423" _msttexthash="100976395">其次，我们使用原始键追加到链接列表中</font>
```

set(key, value) {
const keyHash = this.hash(key);
this.keys[key] = keyHash;
const bucketLinkedList = this.buckets[this.hash(key)];
const node = bucketLinkedList.find({callback: nodeValue => nodeValue.key === key});if (!node) {
bucketLinkedList.append({'key':key, 'value':value});
} else {
node.value.value = value;
}
}

```
<font _mstmutation="1" _msthash="34541" _msttexthash="132591420">3.搜索（复杂度：O（1） = O（n））</font>

*   <font _mstmutation="1" _msthash="28457" _msttexthash="77176489">首先，我们选择带哈希键的存储桶</font>
*   <font _mstmutation="1" _msthash="28418" _msttexthash="110170203">其次，我们使用原始键搜索链接列表中的值</font>
```

get(key) {
const bucketLinkedList = this.buckets[this.hash(key)];
const node = bucketLinkedList.find({callback: nodeValue => nodeValue.key === key});return node ? node.value.value : undefined;
}

```
<font _mstmutation="1" _msthash="33476" _msttexthash="132893423">4.删除（复杂度：O（1） = O（n））</font>

*   <font _mstmutation="1" _msthash="23270" _msttexthash="77176489">首先，我们选择带哈希键的存储桶</font>
*   <font _mstmutation="1" _msthash="24038" _msttexthash="110665763">其次，我们使用原始键删除链接列表中的值</font>

delete(key) {
    const bucketLinkedList = this.buckets[this.hash(key)];
    const node = bucketLinkedList.find({callback: nodeValue => nodeValue.key === key});return node ? node.value.value : undefined;
}
## <font _mstmutation="1" _msthash="32643" _msttexthash="5334199">引用</font>

*   [数据结构：哈希表](https://zshipu.com/t?url=https://www.youtube.com/watch?v=shs0KM3wKv8&list=PLLXdhg_r2hKA7DPDsunoDZ-Z769jWn4R8&index=4)

# <font _mstmutation="1" _msthash="39026" _msttexthash="24419798">6.二进制搜索树</font>

+------------+-----------------+-----------------+-----------------+
| operations |     Insert      |     Delete      |    Traverse     |
+------------+-----------------+-----------------+-----------------+
| complexity | O(log n) ~ O(n) | O(log n) ~ O(n) | O(log n) ~ O(n) |
+------------+-----------------+-----------------+-----------------+

<font _mstmutation="1" _msthash="38715" _msttexthash="334395451">在本节中，我参考[Trekhleb](https://zshipu.com/t?url=https://github.com/trekhleb)的 Github 上的源代码，并用我个人的想法进行一些修改。</font>

## <font _mstmutation="1" _msthash="33592" _msttexthash="25170626">JavaScript 中的实现</font>

<font _mstmutation="1" _msthash="36114" _msttexthash="75098439">1.在 JavaScript 中创建二进制树结构</font>

*   <font _mstmutation="1" _msthash="27300" _msttexthash="116281529">单个节点具有左子节点、右子节点、父节点和值</font>

 ![Image for post](https://miro.medium.com/max/60/1*gnvGSsGYwcw-ntd-cvwSfw.png?q=20)

![Image for post](https://miro.medium.com/max/1336/1*gnvGSsGYwcw-ntd-cvwSfw.png)

<noscript>![Image for post](https://miro.medium.com/max/2672/1*gnvGSsGYwcw-ntd-cvwSfw.png)</noscript>

<font _mstmutation="1" _msthash="3440067" _msttexthash="17203927">复制right@A莱曼</font>
```

class BinaryTreeNode {
constructor(value = null) {
this.left = null;
this.right = null;
this.parent = null;
this.value = value;
}
setValue(value) {
this.value = value;
return this;
}
setLeft(node) {
if (this.left) {
this.left.parent = null;
}
this.left = node;
if (this.left) {
this.left.parent = this
}
}
setRight(node) {
if (this.right) {
this.right.parent = null;
}
this.right = node;
if (this.right) {
this.right.parent = this
}
}
copy(source, target) {
target.setValue(source.value)
target.setLeft(source.left)
target.setRught(source.right)
}
removeChild(node) {
if (this.left && this.left.value === node.value) {
this.left = null;
return true;
}

```
    if (this.right && this.right.value === node.value) {
        this.right = null;
        return true;
    }
    return false;
}
replaceChild(targetNode, newNode) {
    if (!targetNode || !newNode) {
        return false;
    }

    if (this.left && this.left.value === targetNode.value) {
        this.left = newNode;
        return true;
    }if (this.right && this.right.value === targetNode.value) {
        this.right = newNode;
        return true;
    }return false;
}
```

}

```
<font _mstmutation="1" _msthash="34216" _msttexthash="280727642">2.将新节点插入二进制搜索树（复杂性：O（日志 n） = O（n））</font>
```

insert(value) {
if (this.value === null) {
this.value = value;
return this;
}if (this.value > value) {
if (this.left) {
return this.left.insert(value)
}
const newNode = new BinaryTreeNode(value);
this.setLeft(newNode);
return newNode;
}if (this.value < value) {
if (this.right) {
return this.right.insert(value)
}
const newNode = new BinaryTreeNode(value);
this.setRight(newNode);
return newNode;
}

```
return this;
```

}

```
<font _mstmutation="1" _msthash="28445" _msttexthash="312421356">3.在二进制搜索树中搜索特定节点（复杂性：O（日志 n） = O（n））</font>

*   <font _mstmutation="1" _msthash="38987" _msttexthash="227926023">检查节点的值。如果值小于目标值，则搜索到左侧节点，反之亦然。</font>
```

find(targetValue) {
if (this.value === targetValue) {
return this;
}if (this.value > targetValue && this.left) {
return this.left.find(targetValue);
}if (this.value > targetValue && this.right) {
return this.right.find(targetValue);
}return null;
}

<font _mstmutation="1" _msthash="32357" _msttexthash="221100633">4.在二进制搜索树中搜索最小节点（复杂性：O（n））</font>

findMin() {
if (!this.left) {
return this;
}return this.left.findMin();
}

```
<font _mstmutation="1" _msthash="34060" _msttexthash="362002316">5.搜索并删除二进制搜索树中的特定节点（复杂性：O（日志 n）= O（n））</font>
```

remove(value) {
const targetNode = this.find(value);
if (!targetNode) {
return false;
}// Get the parent for removing the child
const { parent } = targetNode;// Check if there are children under the target node
if (!targetNode.left && !targetNode.right) {
// There is no child under the target node
if (parent) {
parent.removeChild(targetNode);
} else {
targetNode.setValue(null);
}
} else if (targetNode.left && targetNode.right) {
const nextBiggerNode = targetNode.right.findMin();
if (nextBiggerNode.value !== targetNode.right.value) {
this.remove(nextBiggerNode.value);
targetNodeToRemove.setValue(nextBiggerNode.value)
} else {
targetNode.setValue(targetNode.right.value);
targetNode.setRight(targetNode.right.right);
}
} else {
// There is only one child  the node to remove
const childNode = targetNode.left || targetNode.right;
if (parent) {
// replace the target node with the child
parent.replaceChild(targetNode, childNode);
} else {
// root node
BinaryTreeNode.copy(childNode, targetNode)
}
}
}

```
## <font _mstmutation="1" _msthash="29939" _msttexthash="5674149">性能</font>

<font _mstmutation="1" _msthash="33138" _msttexthash="7797023">1.高度</font>

*   <font _mstmutation="1" _msthash="28107" _msttexthash="110245473">节点的高度表示右子树或左子树的最大深度。</font>
```

// The height of a node means the max value between the left sub-tree and the right-sub-tree
get height() {
return Math.max(this.leftHeight, this.rightHeight)
}// Get the height of the left sub-tree: the height of the left child node +1
get leftHeight() {
if (!this.left) {
return 0;
}
return this.left.height + 1;
}// Get the height of the right sub-tree: the height of the right child node +1
get rightHeight() {
if (!this.right) {
return 0;
}
return this.right.height + 1;
}
``
<font _mstmutation="1" _msthash="32969" _msttexthash="7376967">2.平衡</font>

* <font _mstmutation="1" _msthash="32786" _msttexthash="163964957">对于平衡二进制树，左子树之间的高度差应小于或等于 1。</font>

get balanceFactor() {
return this.leftHeight - this.rightHeight;
}

## <font _mstmutation="1" _msthash="39195" _msttexthash="5334199">引用</font>

* [类中函数前的"get"关键字是什么？](https://zshipu.com/t?url=https://stackoverflow.com/questions/31999259/what-is-the-get-keyword-before-a-function-in-a-class)
* [吸气](https://zshipu.com/t?url=https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
* [静态](https://zshipu.com/t?url=https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Classes/static)

# <font _mstmutation="1" _msthash="33553" _msttexthash="13674817">7\. 二进制堆</font>

<font _mstmutation="1" _msthash="34671" _msttexthash="226369000">堆只是一个树**，具有特殊****属性或**约束其节点的值，称为**堆属性约束**</font>

+------------+----------+----------+----------+-------------------+
| operations |  Insert  | Delete   | Traverse | Heapify down / up |
+------------+----------+----------+----------+-------------------+
| complexity | O(log n) | O(log n) | O(n)     | O(log n)          |
+------------+----------+----------+----------+-------------------+

<font _mstmutation="1" _msthash="27352" _msttexthash="266241183">在本节中，我学习实现数据结构从[中断：编程和编码访谈](https://zshipu.com/t?url=https://www.udemy.com/course/break-away-coding-interviews-1/)与轻微的修改。</font>

## <font _mstmutation="1" _msthash="38493" _msttexthash="11242634">形状属性</font>

<font _mstmutation="1" _msthash="34074" _msttexthash="316392375">1.堆中二进制树的每个级别都已填充，除了最后一个。堆应形成一个完整的**二进制树**</font>

<font _mstmutation="1" _msthash="38974" _msttexthash="85698652">2.按数组**实现。**如果索引 i**有**一个**节点。**</font>

* <font _mstmutation="1" _msthash="37622" _msttexthash="50277539">它在索引时**有一**个左子： **2i = 1**</font>
* <font _mstmutation="1" _msthash="23153" _msttexthash="72227584">它在索引上**有**一个合适的孩子： **2i = 2**</font>
* <font _mstmutation="1" _msthash="27118" _msttexthash="73420646">它在索引**时有**父级： **（i = 1）/2**</font>

```
export default class Heap {
    constructor() {
        this.heapContainer = [];
    }

    getLeftChildIndex(index) {
        var leftIndex = 2 * i + 1;
        if (leftIndex >= this.heapContainer.length) {
            return -1;
        }
    }getRightChildIndex(index) {
        var rightIndex = 2 * i + 2;
        if (rightIndex >= this.heapContainer.length) {
            return -1;
        }
    }getParentIndex(index) {
        if (index < 0 || index >= this.heapContainer.length) {
             return -1;
        }
        return (index - 1) / 2
    }getNode(index) {
        if (index < this.heapContainer.length){
            return this.heapContainer[index];
        } else {
            return 'undfined'
        }}}
```

## <font _mstmutation="1" _msthash="29549" _msttexthash="7389733">堆属性</font>

<font _mstmutation="1" _msthash="23725" _msttexthash="19568107">1.最小堆：</font>

* <font _mstmutation="1" _msthash="33319" _msttexthash="67547805">每个节点的值应为_<=_其子节点的值</font>
* <font _mstmutation="1" _msthash="33267" _msttexthash="54792894">值最小的节点应该是树的根</font>

<font _mstmutation="1" _msthash="33709" _msttexthash="24371464">2.最大堆数：</font>

* <font _mstmutation="1" _msthash="23010" _msttexthash="60319961">每个节点值应为 >= 其子节点的值</font>
* <font _mstmutation="1" _msthash="44226" _msttexthash="59001423">具有最大值的节点应是树的根</font>

## <font _mstmutation="1" _msthash="28419" _msttexthash="25170626">JavaScript 中的实现</font>

<font _mstmutation="1" _msthash="22958" _msttexthash="119023346">1.向下堆（复杂性：每个呼叫的 O（log n）</font>

* <font _mstmutation="1" _msthash="23452" _msttexthash="7486934">最小堆</font>

```
heapifyDown(index) {
    var leftIndex = getLeftChildIndex(index),
        rightIndex = getRightChildIndex(index),
        smallerIndex = -1;if (leftIndex !== -1 && rightIndex !== -1) {
        smallerIndex = getNode(leftIndex) < getNode(rightIndex) ? leftIndex : rightIndex;
    } else if (leftIndex !== -1) {
        smallerIndex = leftIndex;
    } else {
        smallerIndex = rightIndex;
    }if (smallerIndex === -1) {
         return
    }if (getNode(smallerIndex) < getNode(index)) {
        swap(smallerIndex, index);
        heapifyDown(smallerIndex);
    }
}
```

<font _mstmutation="1" _msthash="34775" _msttexthash="109865301">2.向上（复杂性：每个呼叫的 O（log n）</font>

* <font _mstmutation="1" _msthash="34957" _msttexthash="7486934">最小堆</font>

```
heapifyUp(index) {
    var parentIndex = getParentIndex(index);
    if (parentIndex !== -1 &&
        getNode(index) < getNode(parentIndex)) {
        swap(parentIndex, index);
        heapifyUp(parentIndex);
    }
}
```

<font _mstmutation="1" _msthash="32825" _msttexthash="103346711">3.插入（复杂度：O（日志 n））</font>

insert(value) {
this.heapContainer.push(value);
this.heapifyUp(this.heapContainer.length - 1);
return this;
}

<font _mstmutation="1" _msthash="33540" _msttexthash="89319217">4.搜索（复杂性：O（n））</font>
```
find(value)    
    const foundItemIndices = [];
    for (let itemIndex = 0; itemIndex < this.heapContainer.length; itemIndex++) {
        if (value === this.heapContainer[itemIndex]) {
            foundItemIndices.push(itemIndex);
        }
     }

```
 return foundItemIndices;
```

}

```
<font _mstmutation="1" _msthash="32890" _msttexthash="112215285">5.删除（复杂性：每个呼叫的 O（log n）</font>

*   <font _mstmutation="1" _msthash="24271" _msttexthash="63421384">将目标节点替换为最后一个节点</font>
*   <font _mstmutation="1" _msthash="38740" _msttexthash="41318329">向下堆或堆起目标节点</font>

```

remove(value) {
const numberOfItemsToRemove = this.find(value).length;
for (let iteration = 0; iteration < numberOfItemsToRemove; iteration ++) {
const indexToRemove = this.find(value).pop();
if (indexToRemove === (this.heapContainer.length) - 1) {
this.heapContainer.pop();
} else {
this.heapContainer[indexToRemove] = this.heapContainer.pop();
}const parentNode = getNode(getParentIndex(iteration));
if (this.getLeftChildIndex(indexToRemove) !== -1 && parentNode !== 'undefined') {
this.heapifyDown(indexToRemove);
} else {
this.heapifyUp(indexToRemove);
}
}return this;
}

```
```
