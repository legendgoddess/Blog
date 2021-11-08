---
title: CF1375E Inversion SwapSort
date: 2021-10-01 07:58:04
tags:
  - 贪心
  - 构造
categories:
  - CF题解
---


<h3><center>CF1375E Inversion SwapSort</center></h3>

> [CF1375E Inversion SwapSort](https://www.luogu.com.cn/problem/CF1375E)

发现逆序对不是很好入手，考虑最终构成的序列是单调递增的情况。

不妨考虑这是一个排列的情况。

> 显然离散化一下答案不会改变。

发现 $n$ 肯定是在最后面，那么对于一开始的序列我们不妨考虑将 $n$ 放到最后面之后转化成一个子问题。

那么对于一个合法的子问题，我们必须保证对于原来 $a_u < a_v$ 的情况，还有 $a_u < a_v$。

不妨考虑之前最后一个位置是 $x$，那么对于 $\ge x$ 的数我们可以进行一次循环移位，这样可以保证位置 $n$ 肯定是在正确的位置的。

具体来说就是 $x + 1$ 和 $x$ 交换位置， $x + 2$ 和 $x + 1$ 交换位置。也就是向后进行循环移位，可以发现肯定是合法的。

之后直接根据子问题去做即可复杂度 $O(n^2)$。

