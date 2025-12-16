---
title: 算法竞赛中的 python（一）
katex: true
tag:
  - 算法竞赛
categories:
  - 算法竞赛
abbrlink: 5c7f8dbe
date: 2025-12-15 00:00:00
updated: 2025-12-15 00:00:00
---

来简单学习一下 python 如何在算法竞赛中使用。寒假想拿学习更多的东西。

<!--more-->

## 创建一个二维数组

<https://www.luogu.com.cn/problem/P11450>.

做法很简单，看代码。

```python
if __name__ == "__main__":
    n, q = map(int, input().split())
    i = 0
    X = [[n] * n for _ in range(n)]
    Y = [[n] * n for _ in range(n)]
    Z = [[n] * n for _ in range(n)]
    ans = 0
    while i < q:
        x, y, z = map(int, input().split())
        X[y][z] -= 1
        Y[x][z] -= 1 
        Z[x][y] -= 1
        if X[y][z] == 0:
            ans += 1
        if Y[x][z] == 0:
            ans += 1
        if Z[x][y] == 0:
            ans += 1
        i += 1
        print(ans)
    
```

## 读入一个数组

<https://qoj.ac/contest/1427/problem/7810>.

记得要加上 `list()`。

```cpp
if __name__ == "__main__":
    n, d = map(int, input().split())
    v = list(map(int, input().split()))
    a = list(map(int, input().split()))
    ans = 0
    cnt = 0
    mn = 1e9
    for i in range(n - 1):
        if i:
            v[i] += v[i - 1]
        val = (v[i] - cnt * d + d - 1) // d
        cnt += val
        mn = min(mn, a[i])
        ans += val * mn
    print(ans)
```

## 让我们学会输出！

<https://www.luogu.com.cn/problem/P9750>.

分类讨论。

```python
from math import *

def solve():
    a, b, c = map(int, input().split())
    if a < 0:
        a, b, c = -a, -b, -c
    delta = b * b - 4 * a * c
    if delta < 0:
        print("NO")
        return
    x1 = ceil((-b + sqrt(delta)) / (2 * a))
    # print(x1)
    if a * x1 * x1 + b * x1 + c == 0:
        print(int(x1))
        return
    p, q = -b, 2 * a
    val = floor(sqrt(delta))
    if val * val == delta:
        delta = 0
        p += val
    g = gcd(p, q)
    p /= g
    q /= g
    if p:
        if p * q < 0:
            print('-', end = '')
        p, q = abs(p), abs(q)
        print(int(p), end = '')
        if q != 1:
            print('/', end = '')
            print(int(q), end = '')
        if delta:
            print('+', end = '')
    if delta:
        val = floor(sqrt(delta))
        while val >= 1:
            if delta % (val * val) == 0:
                delta /= val * val
                break
            val -= 1
        p, q = val, 2 * a
        g = gcd(p, q)
        p /= g
        q /= g
        if p != 1:
            print(int(p), end = '*')
        print("sqrt(", end = '')
        print(int(delta), end = ')')
        if q != 1:
            print('/', end = '')
            print(int(q), end = '')
    print('')


if __name__ == "__main__":
    T, M = map(int, input().split())
    for _ in range(T):
        solve()
```