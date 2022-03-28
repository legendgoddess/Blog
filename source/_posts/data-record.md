---
title: 每日随记
date: 2022-3-21 21:21:21
categories:
  - 随笔
password: fuyimin
sticky: 2
---

其实有心的人都是可以看到这篇博客的，但是隐藏就是意思一下，表示说我有些话不能在明面上说。

---

$\tt 2022-3-26$

今天是 $\tt noi\ online$，我说一下往年的战绩吧。

- 我初二那年，刚学，不会打开网页，没错。我没有进去，结果保龄。

- 初三，来到 $\tt HL$ 打 $\tt online$ 的时候在家里，比较菜， 也不是很想打，就最简单的题目写了一个序列自动机。

话说今年题目比较简单。

$\tt T1$ 我想了 $\tt 2h$，最后发现就是直接考虑一个数的合法区间，之后离线询问维护区间和就行了。

$\tt T2$ 考虑区间按照长度排序之后有性质，从大到小做可以直接做，从小到大做需要建树做。

$\tt T3$ 三维偏序。

期望得分 $100 + 100 + 20$ 但是 $\tt T1$ 我 $n, m$ 写反了。

> 但是总归是高兴的，毕竟也算是一种进步了吧，或者说这个东西就是安慰了 /qd

听到机房之前口头 $\tt Ak$ 的大佬都伪了，比较离谱。



$\tt 2022-3-25$

好像变成每隔两天更新了。

打了一场模拟赛，其实别人基本上都是会 $2$ 题以上的，就我只会 $\tt T1$。但是问题尴尬的就是其他人全部挂分，就我 $\tt T1$ A 了，结果就是莫名其妙校内 $\tt rk 1$。我寻思着 $\tt T1$ 肯定是一个半幺群呀，为啥不用线段树直接整呢？

> [[IOI2015]horses 马 - 洛谷](https://www.luogu.com.cn/problem/P5874)
> 
> 说实话这题我所有的做法都是想到过了，显然是需要考虑 $x_i, y_i$ 的性质的，发现乘到大于 $\tt mod$ 了肯定更加优，假设马不会把自己搞死，所以 $x_i \ge 1$。那么显然我们只需要维护后缀乘积刚好 $\tt > mod$ 的情况就行了。
> 
> 可以直接对于乘积取 $\tt lg$ 变成加法，用线段树维护就行了。
> 
> 但是也是有用 $\tt set$ 维护最后几个有值的位置的，但是这玩意贼难写。

然后开心了一整天，难得不被别人吊打的日子。

$\tt 2022-3-24$

想不到吧，我是同一天写的两篇。

今天模拟赛，$\tt T1$ 直接建立反图就结束了，就是想不到呀。

$\tt T3$ 考虑决策树是一棵二叉树，二叉树本质上就是将一个数进行二进制拆分。就算之后直接进行小数的二进制拆分判环不懂，前面的 $\tt 40$ 分总是应该能拿到的吧。

$\tt T2$ 是考虑线段树维护那个位置是没有出现过的，之后维护树上一条链的情况。

晚上在复习网络流和二分图，昨天那篇说了很多了，放轻松压力永远不在我这边。

但是说实话看了 $\tt hgs, sk$ 的情况实际上还是不容乐观，据说 $\tt sk$ 首考不是特别好，$\tt hgs$ 文化课堪忧，省选有难度。想想当年在初中，刚刚认识 $\tt OI$ 的时候，$\tt hgs$ 在 $\tt Jc$，$\tt sk$ 在讲台上大喊不要打 $\tt slay$ 的时候，其实认为之后一切都是很好的。

$\tt sk$ 高一进了省队，高二失利，$\tt hgs$ 因为初赛问题少了一年比赛机会。

> 希望学长们可以考上 $\tt TP$，希望我还能和当年一样，能大喊接着走学长的道路，帮他们走完，帮他们将路走得更加平坦。

但是事实呢？

自己本事实力弱，学不进去东西，哎。

有梦想，但是不是每个梦想都能实现的。

---

$\tt 2022-3-23$

没错还是之后一天来补日记，感觉上昨天的状态不是很好，到八点钟之后基本上就没有效率了。

昨天主要是订正题目之后写数据结构的博客，但是看了各位大佬的博客之后发现自己仅仅线段树方面还是有很多很多要学习的。

> 可以确定有一点就是当初学习的时候也是很浅的，所以现在如果说要让我打一个线段树区间加，乘，我都不能有把握说是一定可以过的。

线段树，平衡树，动态树，分块，分治，这几个东西可以说是完全没有系统学过的。这个就是和其他同学比如杨队，徐队他们就有十分明显的差距。有些比较显然的东西，考场上却是完全没有想到的。

> 举个例子：我的理解上就是单纯的可以分成两部分，但是事实上我们这里可以把询问离线，之后考虑对于跨过区间的部分是可以计算，不然的话直接分治。

唯一可以抱怨的就是自己真正开始学学得太晚了，算算从 $2021$ 年初开始真正知道自己应该学什么，仅仅过去了一年，从认识 $\tt OI$ 已经过去了 $3$ 年了。我学了 $1$ 年成绩差是理所当然的，正是因为如此别人学了 $6$ 年，$7$ 年甚至 $8$ 年还是在这边挣扎，我又有什么压力吗？

> 我们可以算算，$\tt macecsuted$ 拿到市一等是在 $5$ 年级的时候，$\tt silhouette$ 初二就已经在小机房了预备省选了，很荣幸可以与他们一起学。

emmm，就这样吧。

---

$\tt 2022-3-22$

其实已经是下一天了，来补一下日记。

考试挂分有点惨烈，本来就没有多少分，一下挂分就基本没有了，晚上没有订完题目，心态有点爆炸。

学了一个 $\tt Dij$ 费用流。

---

$\tt 2022-3-21$ 

今天是开始这个的第一天，选了一个很好的时间，是这个月最 $\tt 21$ 的日子。

好吧，我们说点正经的。

昨天的 $\tt CF$ 属于上分场这个毋庸置疑吧，但是 $\tt D$ 的过于麻烦的实现以及不熟练的 $\tt STL$ 直接去世。最后甚至需要用一些阴间方法才能不下分，想一想 $\tt D$ 稍微快一点是前 $100$。换一句话说表现分太低了，和 $\tt VP$ 差距太远。

变菜了吗？

可能是吧。

没有心情做题目，整体感觉上都是一种颓废但是又不划水的感觉，假努力吧。

但凡少只猫陪我，我的心态就会发生微妙的变化了。

还有一个事情。

自己的东西都忘掉了对吧，学过的都不会了，会的都不会用了对吧，一点一点去复习吧。

思维**是不能短时间提升的**。

> 换句话说就是 **菜会一直菜下去**。
> 
> 不是很能接受这个事实，毕竟谁都想好，但是看到时间的减少但是实力却在下降，心态总是会发生微妙的变化的。

emmm，就先说这么多吧，希望今后可以好，希望省选之前不用上$\color{red}\text{红}$了，先不掉出$\color{purple}\text{紫}$好吧。