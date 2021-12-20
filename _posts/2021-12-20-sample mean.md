---
layout: post
title: 样本与整体的关系
date: 2021-12-20
author: zhaogs
header-img: img/post-bg-mma-0.png
catalog: true
tags:
      - 读书笔记
      - 统计学习方法
---

样本的均值是整体均值的无偏估计，样本的方差是整体方差的有偏估计，这里所谓的有偏估计与无偏估计是针对通过样本计算出的均值与方差的期望而言的，而不是针对某次抽取样本所得到的样本的均值与方差而言，即某次抽样得到的样本，并计算得到的样本的均值与方差是并不严格等于实际整体的均值与方差，因此在实际应用中也可以发现在整体的方差无偏估计与有偏估计时，二者对结果往往不会造成较大的影响。

#### 1. 样本的均值是整体均值的无偏估计

假设抽样得到的样本为数据集$\{x_1,x_2,...,x_n\}$，$X$表示整体，即对于每一个样本$x_i\sim X$，$\overline x$表示样本的均值，$\mu$表示整体的均值。因此有如下推导
$$
\begin{aligned}
\overline x &= \frac{1}{n}\sum_{i=1}^nx_i\\
\mu &= \Bbb E(x_i),\ x_i\sim X\\
\Rightarrow\  E(\overline x) &=\Bbb E\left( \frac{1}{n} \sum_{i=1}^nx_i\right)\\
&=\frac{1}{n}\sum_{i=1}^n\Bbb E(x_i)\\
&=\mu
\end{aligned}
$$
因此可以得到样本的均值是整体均值的无偏估计。

#### 2. 样本的方差是整体方差的有偏估计

假设$s^2$表示样本的方差，$\sigma^2$表示整体的方差。因此有如下推导
$$
\begin{aligned}
s^2 &= \frac{1}{n}\sum_{i=1}^n(x_i-\overline x)^2\\
\sigma ^2 &= \Bbb E(x_i-\mu)^2=\Bbb D(x_i),\ x_i\sim X\\
\Bbb D(\overline x)&= \Bbb D(\frac{1}{n}\sum_{i=1}^nx_i)=\frac{1}{n^2}n\Bbb D(x_i)=\frac{1}{n}\Bbb D(x_i),\ x_i\sim X\\
\Rightarrow\ \Bbb E(s^2) &= \Bbb E\left( \frac{1}{n}\sum_{i=1}^n(x_i-\overline x)^2\right)\\
&=\Bbb E\left( \frac{1}{n}\sum_{i=1}^n(x_i-\mu+\mu-\overline x)^2 \right)\\
&=\Bbb E\left( \frac{1}{n}\sum_{i=1}^n\left((x_i-\mu)^2+2(x_i-\mu)(\mu-\overline x)+(\mu-\overline x)^2\right) \right)\\
&=\Bbb E\left( \frac{1}{n}\sum_{i=1}^n(x_i-\mu)^2+\frac{2}{n}\sum_{i=1}^n(x_i-\mu)(\mu-\overline x)+\frac{1}{n}\sum_{i=1}^n(\mu-\overline x)^2\right) \\
&=\Bbb E\left( \frac{1}{n}\sum_{i=1}^n(x_i-\mu)^2-\frac{1}{n}\sum_{i=1}^n(\mu-\overline x)^2\right) \\
&=\Bbb E\left( \frac{1}{n}\sum_{i=1}^n(x_i-\mu)^2\right)-\Bbb E\left(\frac{1}{n}\sum_{i=1}^n(\mu-\overline x)^2\right) \\
&=\Bbb D(x_i)-\Bbb D(\overline x)\\
&=\sigma^2-\frac{1}{n}\sigma^2\\
&=\frac{n-1}{n}\sigma^2

\end{aligned}
$$
因此样本的方差的期望并不等于整体的方差，即样本的方差是整体方差的有偏估计，对上述式子进行如下修正即可得到整体方差的无偏估计。
$$
\begin{aligned}
s'^2&=\frac{n}{n-1}\left(\frac{1}{n}\sum_{i=1}^n(x_i-\overline x)^2\right)=\frac{1}{n-1}\sum_{i=1}^n(x_i-\overline x)^2\\
\Bbb E(s'^2) &= \frac{n}{n-1}\Bbb E(s^2)=\sigma^2

\end{aligned}
$$
