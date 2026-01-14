---
title: 2026-01-13(#10)：いとし調べ乗せ光る風
katex: true
tag:
  - 算法竞赛
categories:
  - 算法竞赛
  - 训练
abbrlink: ef8530e1
date: 2026-01-13 00:00:00
updated: 2026-01-13 00:00:00
---

BlackY feat. Risa Yuzuki —— 華神樂

<!--more-->

## 10 P14960 「KWOI R1」XOR and Sliding Window

不难发现每一位是独立的，因此考虑 01 怎么做。

把 $b$ 做一遍前缀异或和，发现 $n/\gcd(n,k)$ 个元素会被绑定在一起，也就是说你能修改 $a_i$ 和 $a_{i+k}$。每一组是可以直接异或在一起的，因为这样一定比做加法更优。

我们还能对 $k$ 个同余类做翻转操作，而只有 $\gcd(n,k)$ 个同余类，因此只有 $2\mid (k/g)$ 时才能实现翻转。

## 11 