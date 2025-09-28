---
title: 2025-09-22(#3)：让我们再次解答 对着那被吞噬的黑暗
katex: true
tag:
  - 算法竞赛
categories:
  - 算法竞赛
  - 训练
abbrlink: ec78c757
date: 2025-09-22 00:00:00
updated: 2025-09-22 00:00:00
---

ARForest feat. Sennzai —— 星になって

<!--more-->

队友太强了！！

<https://qoj.ac/contest/2534>

## G. 序列与整数对

这个复杂度怎么拿不等式写出来啊qwq

多做点数据结构。由队长的建议，要补区域赛的数据结构题。

## A. 整点正方形计数2

赛时队友写了一个非常诡异的做法过掉了，赛后看来想复杂了。



## M. 并行计算

为啥能不去想这个题啊。

首先先把前缀和算出来，然后再减去上一个最近是 $1$ 的位置的前缀和值，也就是 $y_i\times s_i$ 的前缀最大值。

由于 $1024=32^2$，因此直接将序列分块，即可比分治更优地完成前缀操作。

## C. 造桥与砍树

## F. 连线博弈

Fun Fact：我之前做过 SG 函数的递推式长得跟这个一样得题，但是一点瞪不出 SG 函数的规律。感谢队友神力了。

## H. 教师

---

trio <https://qoj.ac/contest/1252>

也算是勉强打上金牌线了，主要是我的 I 分类讨论讨错了，我在干什么🤣

## I. Linear Fractional Transformation

硬解方程，由于 $c,d$ 中至多只有一个是零，分别尝试将所有数用 $c,d$ 表示即可。

---

来打 CF，用的小号，打 Div.2，<https://codeforces.com/contest/2151>。

怎么 C 都不会了，还是要充满决心啊！

## C. Limited Edition Shop

其实一开始想的就是对的，唉。

---

搞了新的小号来打 Div.3。james2StormEye！

<https://codeforces.com/contest/2149>

无语了，怎么能卡 F。

---

补 <https://qoj.ac/contest/2238>。

## G. 矩阵

```cpp
for (int i = 1; i <= n; ++i)
    for (int j = 1; j <= n; ++j)
        cout << j + (i - 1) * p << " \n"[j == n];
```

$p>n$。

---

vp [The 2025 ICPC German Collegiate Programming Contest](https://qoj.ac/contest/2535)

---

唉怎么每天都有一万道题需要做。

感觉是时候寻找一些全新的可能性了，iznomia。