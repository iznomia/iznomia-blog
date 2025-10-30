---
title: 2025-10-20(#6)：能拯救他人的梦想
katex: true
tag:
  - 算法竞赛
categories:
  - 算法竞赛
  - 训练
abbrlink: 5d67ad62
date: 2025-10-20 00:00:00
updated: 2025-10-24 00:00:00
---

ナナツカゼ —— アリア

<!--more-->

trio <https://qoj.ac/contest/2551>，怎么马上就要打正赛了啊？

---

solo <https://qoj.ac/contest/1828>

## B. Birthday Gift

发现不太能做，转化成删除相邻两个不同的，这样 $2$ 就可以转化为 $0,1$，最后必定会删到只剩一个数的情况。

---

## qoj14572 Mex Hex

这个条件非常奇妙，不太能 DP。但是可以维护上一个保护范围终止点的可行区间，这样下一个区间的合法范围是可以简单地更新的。

## qoj4888 Decoding The Message

首先模 $65535$ 很诡异，注意到 $65535=3\times 5\times 7\times 257$，因此对于 $256$ 进制，前三个都是所有数的和（$256\bmod 3=1$），后面这个

---

做点杂题，感觉这个挺杂的：[2023 Multi-University Training Contest 1](https://qoj.ac/contest/1306)。

## A. Hide-And-Seek Game

不是你怎么能调这么久的。

## B. City Upgrading

直接 DP 就可以了。

## C. Mr. Liang play Card Game

比较简单。

## E. Cyclically Isomorphic

向模板库中添加了最小表示法。

## I. Assertion

你在搞笑吗。

## J. Easy Problem I

不是你怎么能调这么久的。

## K. Easy Problem II

不是你怎么能调这么久的。

不如 Today's Computer is very Fast.

## L. Play on Tree

AGC017D 的换根 DP 版。

## [ARC207B] Balanced Neighbors 2

先考虑 $n$ 为偶数，不难想到让 $i$ 无法到达 $n-i+1$。构造二分图容易做到这件事情，如果 $n$ 为奇数，那么 $n$ 可以在两步之内走到所有点。