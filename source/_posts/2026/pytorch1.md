---
title: PyTorch 深度学习简论（一）：初探茅庐
katex: true
tag:
  - PyTorch
  - 深度学习
  - 机器学习
categories:
  - 计算机科学
topic: pytorch
abbrlink: d259e7d7
date: 2026-01-18 00:00:00
updated: 2025-01-18 00:00:00
cover: https://pic1.imgdb.cn/item/696b686761bfebba12605d56.jpg
description: 来玩深度学习！本文初步介绍了机器学习的概念，来为学习 PyTorch 做一些准备。
---

参考的教材：

- 《Pytorch 深度学习简论》：https://m-tob.jd.com/ebook/30806450
- 《机器学习》：西瓜书

## 1. 猴王出世

首先一个观点是，“智能”和“自我意识”没什么关联，不要去思考这个问题。

深度学习的目的是用数学手段，使用大量数据来近似输入和输出差距很远的函数。比如输入一张图片，输出一段文字来描述这个图片。

### 1.1 绪论

机器学习是从数据中产生模型（model）的算法，即 learning algorithm。

数据集 $D=\{\bm{x_1},\cdots,\bm{x_n}\}$ 包含了 $m$ 个示例（instance）或样本（sample），或者叫“特征向量”（feature vector），每个示例是 $d$ 维样本空间 $\mathcal X$ 中的一个元素，$d$ 称为维数（dimensionality）。

学得模型对应了关于数据的某种潜在规律，称为“假设”（hypothesis），规律自身称为“真相”（ground-truth），学习的过程是在逼近真相。
 
$(\bm x_i,\bm y_i)$ 表示一个“样例”（example），$\bm y_i$ 称为“标记”（label），$\bm y_i\in \mathcal Y$，如果 $\mathcal Y$ 是离散的，那么这个工作称为“分类”（classification），连续的则称为“回归”（regression），这两者都属于“监督学习”。

若没有标记信息，我们可以对样本进行“聚类”（clustering），即将样本分成若干组，每组称为一个“簇”（cluster），这是“无监督学习”的一种。

学得模型能适用于新样本的能力称为“泛化”（generalization）能力。

假设空间 $\mathcal H$ 指的是模型 $f$ 的集合，而版本空间指符合样例的模型集合。版本空间大概率不只一个元素，那么我们应该选择哪个作为我们的模型呢？

“奥卡姆剃刀”是一种常用的原则，即选择最简单的那个。但事实上，总存在一种样本空间，使得那些看上去非常离谱的拟合实际上是更优秀的。

这就是“没有免费的午餐”的定理。NFL 定理的前提是每个问题出现的概率相同。

### 1.2 模型评估与选择

我们偏向于选择泛化误差尽可能小的模型。

1. 留出法：$2/3\sim 4/5$ 的样本用于训练，剩下的用于测试。
2. 交叉验证法：将数据集 $D$ 划为大小相似的 $k$ 个互斥子集，进行 $m$ 次，称为“$m$ 次 $k$ 折交叉验证”，常见的有 $k=m=10$；当 $k=m$ 时得到“留一法”，训练出的模型往往与直接用 $D$ 训练出的模型很相似。
3. 自助法：在数据集较小时，可以将取出的样本再扔回数据集，重复 $m$ 次得到一个 $D'$。

我们用均方误差描述学习器 $f$ 的性能：

$$
E(f;\mathcal D)=\int_{\bm x\sim \mathcal D} (f(\bm x)-y)^2p(\bm x)\d x
$$

---

接下来我们介绍 classification 时常用的性能度量。

错误率 $E(f;\mathcal D)=\int_{\bm x\sim \mathcal D}\mathbb I(f(\bm x)\ne y)p(\bm x)\d x$，精度 $\operatorname{acc}(f;\mathcal D)=1-E(f;\mathcal D)$。

对于二分类问题，将样例根据其真实类别和学习器预测的类别划分为真正例、假正例、真反例和假反例（$TP,FP,TN,FN$）。查准率 precision 定义为 $P=\frac{TP}{TP+FP}$，查全率 recall 定义为 $R=\frac{TP}{TP+FN}$。一般来说，两者时矛盾的，除非任务非常简单。

很多情形下最终会对预测结果进行排序，从前到后我们认为其是正例的概率越低。这样，以查准率为纵轴、查全率为横轴可以绘制 P-R 曲线，将 $R=P$ 的点视为平衡点（Break-Event Point, BEP），可以通过比较 BEP 来判断学习器性能。

但是 BEP 有点过于简单了，常用的是 $F1=\dfrac{2PR}{P+R}=\dfrac{2TP}{2TP+FN+FP}$，即 $P,R$ 的调和平均数。

F1 度量的一般形式是 $F_{\beta}=\dfrac{(1+\beta^2)PR}{\beta^2 P+R}$，当 $\beta>1$ 时查全率影响更大，$\beta<1$ 时查准率影响更大。

如果对所有 $P,R$ 取平均值，可以算得“宏 F1”（$\operatorname{macro}-F1$），对所有 $TP,FP,TN,FN$ 取平均值可以算得“微 F1”（$\operatorname{micro}-F1$）。

“排序”本身的质量好坏很大程度上决定了学习器的“期望泛化性能”，预测概率越大说明我们的模型认为其更可能是正例。纵轴为真正例率（True Positive Rate）$\operatorname{TPR}=\dfrac{TP}{TP+FN}$，横轴为假正例率 $\operatorname{FPR}=\dfrac{FP}{TN+FP}$，得到 ROC 曲线。在绘制 ROC 曲线时，假定有 $m^+$ 个正例和 $m^-$ 个反例，首先会把所有样例预测为反例，得到坐标 $(0,0)$，然后扫描排序后的序列作为预测阈值，当前为真正例则得到坐标 $(x,y+\frac 1{m^+})$，当前为假正例得到坐标 $(x+\frac 1{m^-},y)$。比较模型的好坏就会计算 ROC 曲线下的面积，即 $\displaystyle\operatorname{AUC}=\frac 1 2\sum_{i=1}^m(x_{i+1}-x_i)(y_i+y_{i+1})$。模型的损失为 $\displaystyle\ell_{rank}=\frac{1}{|D^+||D^-|}\sum_{\bm x^+\in D^+}\sum_{\bm x^-\in D^-}\left(\mathbb I(f(\bm x^+)<f(\bm x^-))+\frac 1 2 \mathbb I(f(\bm x^+)=f(\bm x^-))\right)$，不难发现 $\ell_{rank}=1-\operatorname{AUC}$。

## 2. 线性模型

