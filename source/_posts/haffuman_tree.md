---
title: 一句话解释哈夫曼树
date: 2021-09-16 15:30:34
tags:
  - 数据结构
categories:
  - 算法
---

<h3> <center> 一句话解释哈夫曼树 </center></h3>

我们考虑对于一棵叶子节点有权值的二叉树，设其总共的贡献是每个叶子节点的权值乘上深度。

那么我们需要构造一个使其贡献最小的二叉树，也就被称作最优二叉树。

我们考虑贪心对于每次选择权值和最小的两个点进行合并，之后其父亲，权值为两个节点的权值和即可。




