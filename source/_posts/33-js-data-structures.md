---
title: 33-js-data-structures
date: 2019-06-12 21:55:30
tags: 33-js-concepts
keywords: js 数据结构, js data Structures, javascript 数据结构, javascript Data Structures, js最全的数据结构讲解.
---
### js的数据结构
#### 前言 (preface)
> 在一定水平上，有三种基本的数据结构, 栈（Stacks）和队列（Queues)是类数组（array-like)的对象. 区别是插入和取出的顺序。 这里都知道栈是先进后出，后进先出。 队列是先进先出，后进后出。
> 链表（linkedList) 和 树（Trees) 是一种有节点指向其它节点的数据结构。

#### 栈（Stack)
> 栈在js中最重要的应用是当我们将function调用时候会push这个函数及作用域进栈，然后再调用栈 (call Stack)。 函数进栈和出栈是 执行 `push` 和 `pop` 操作。原则是先进后出（Last In, Frist Out. 缩写：LIFO)

#### 队列（Queue)
> js 是事件型驱动语言这也是支持非阻塞型操作成为可能性。js作为单线程语言，这就需要用队列来将要执行的事件进行排队。然后事件循环来执行队列里面的事件。队列的进出时 执行 `unshift` 和 `pop` 。原则是 先进先出(First In, Frist Out, 缩写 FIFO)

#### 链表(LinkedList)
> 就像数组（array）一样， 链表也是有序的存储数据。不同的是数组用index来做指针，链表的第一个节点叫做head最后一个叫tail. 在单链表里面(singly-linked-list),单链接表是单向的 只有指向下一个节点的指针。 双链表（doubly-linked-list)是双向的，有指向下一个节点的指针，下一个节点也有指向上一个节点的指针。可以双向走。

#### 树(Tree)
> 树是非线性的，分层存储的数据结构。可以用来存储文件或者有序的列表。树都有一个根节点（root node) 下面的子节点称呼上一层的节点为父节点。查找和删除的速度比链表要快。查询的时候有深度优先查询（Depth Frist Traversal）DFT，广度优先查询(Breadth Frist Traversal)BFT

#### Graph
> 如果树有超过一个父节点，就变成了graph

#### Hash Table
> 有键值对和对应的值，成员是无序的，而且不允许存在两个相同名字的成员（key键相同）

**reference doc**
原文写得非常好。极力推荐看原文（需要科学上网）。这一篇偏向于翻译得不太好的翻译文，翻译不到位~ 英文原意表达的到位感觉找词找不到。也尽力在翻译~ 
> [Thon Ly 原文链接](https://medium.com/siliconwat/data-structures-in-javascript-1b9aed0ea17c)
