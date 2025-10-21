---
title: 2025-10-05(#5)：不死的太阳耀斑
katex: true
tag:
  - 算法竞赛
categories:
  - 算法竞赛
  - 训练
abbrlink: 762e3621
date: 2025-10-05 00:00:00
updated: 2025-10-05 00:00:00
---

Ashrount —— Undying Macula

<!--more-->

10 月 2 日体验了 Arcaea 的新主线，也是我第一次跟着更新体验主线。确实好玩好吧。

隐藏曲我就这么翻译了，感觉这么粗暴的翻译比较有史诗感。

谢谢你回应我的呼唤。

---

duo <https://qoj.ac/contest/2539>

## F. Yet Another MST Problem

就你要注意到一个事情，两个区间连起来之后，新的区间相当于这两个区间的交集。

## E. Coffee Shops

## B. Domain Compression

## K. Robot Construction

---

trio <https://qoj.ac/contest/1741>，真补不完了啊。

## E. Building a Fence

考场上就应该直接写拍子。

## B. Bookshelf Tracking

注意到读书操作相当于左右两半段排序，因此直接模拟即可。

## C. Painting Fences

## D. Function with Many Maximums

## F. Teleports

## G. Exponent Calculator

## I. Marks Sum

萌萌的。

## K. Train Depot

## L. Array Spread

---

trio <https://qoj.ac/contest/1780>。

我觉得我就是菜。

## H. Permutation

事实证明小局部 DP，大范围按照 $2/3$ 来划分即可。

## E. Team Arrangement

我勒个直接枚举拆分数之后跑 $O(n^2)$ 暴力啊。

## L. Challenge Matrix Multiplication

考虑针对题目条件的势能的做法。每次找到一条路径然后删除这条路径上的所有边，使得起点出度减一，终点入度减一，因此找到这条路径之后暴力做即可，时间复杂度 $O(60(n+m))$。

---

trio <https://qoj.ac/contest/1901>。

我觉得需要好好训练一下。

## K. Knapsack

莫名其妙的科技题，这里稍微写点东西。

如果直接那个数少然后将当前数加到某个值里是没有道理的，因为你不会使这三个数的差值变小。于是你考虑每次将两个当前三元组 $(A,B,C)$ 合并，用 $A+C$ 来算值，这样大概率是可以减小差值的。

最终我也是不知道真遇到这种题怎么办，感觉只能听天由命。

## H. Have You Seen This Subarray?

这场为数不多的好题了，这个比赛给我的感觉非常愚人节。

相邻两个数靠在一起的时间为若干个连续段，因为交换随机，所以段数很少，询问的时候直接暴力合并段即可。

但是 $n$ 小的时候不满足这一点，需要暴力哈希做掉。