---
layout: post
title: 逻辑斯谛回归
date: 2022-01-17
author: zhaogs
header-img: img/post-bg-sky.jpg
catalog: true
tags:
      - 读书笔记
      - 统计学习方法
---

#### 1. 基本思想

logistic模型推导的出发点是建立在假设似然比的对数是一个线性判别函数，并因此可以推导出其后验概率比的对数也是线性判别函数，即


$$
\begin{aligned}
&\log \left(\frac{p(x|\omega_i)}{p(x|\omega_M)}\right)=\beta_{i,0}+\beta_i^Tx,\ i=1,2,...,M-1\\
\Rightarrow\ &\log \left(\frac{p(\omega_i|x)}{p(\omega_M|x)}\right)=w_{i,0}+w_i^Tx,\ i=1,2,...,M-1

\end{aligned}
$$


还有一个隐含条件，所有的后验概率和为1，即$$\sum_{i=1}^Mp(\omega_i\vert x)=1$$

因此可以解得


$$
\begin{aligned}
p(\omega_M|x)&=\frac{1}{1+\sum_{i=1}^{M-1}\exp(w_{i,0}+w_i^Tx)}\\
p(\omega_i|x)&=\frac{\exp(w_{i,0}+w_i^Tx)}{1+\sum_{i=1}^{M-1}\exp(w_{i,0}+w_i^Tx)},\ i=1,2,..,M-1\\
\end{aligned}
$$


对于二类问题则有


$$
\begin{aligned}
p(\omega_2|x)&=\frac{1}{1+\exp(w_{0}+w^Tx)}\\
p(\omega_1|x)&=\frac{\exp(w_{0}+w^Tx)}{1+\exp(w_{0}+w^Tx)}=\frac{1}{1+\exp(-(w_{0}+w^Tx))}\\
\end{aligned}
$$


这也就是常见的二类的逻辑斯谛回归的表达式，可以看出其后验概率分布是一个指数形式的分布，其判别函数可以推导出是线性的。该函数也就是sigmoid函数，在之后的学习中还会多次遇到该函数。

#### 2. 学习过程

有了以上的推导，在两类问题的实际应用中需要求出$$w_0,w$$才能对两类数据进行分类，对参数的求解可以使用最大似然法。对于两类分类问题，假设1类样本有$$N_1$$个，2类样本有$$N_2$$个，对数似然函数可以表示为


$$
L(\theta)=\ln \left(\prod_{k=1}^{N_1}p(x_k|\omega_1;\theta)\prod_{k=1}^{N_2}p(x_k|\omega_2;\theta)\right)
$$
 

由贝叶斯公式$$p(x_k\vert \omega_1;\theta)=\frac{p(\omega_1\vert x_k;\theta)p(x_k)}{p(\omega_1)}$$可以化简上式得到


$$
L(\theta)=\ln \left(\prod_{k=1}^{N_1}p(\omega_1|x_k;\theta)\right)+\ln \left(\prod_{k=1}^{N_2}p(\omega_2|x_k;\theta)\right)+\ln \left(\frac{\prod_{k=1}^Nx_k}{\prod_{m=1}^2p(\omega_m)^{N_m}}\right)
$$


对上进行$$\arg\max_\theta L(\theta)$$运算即可求解得到$$w_0,w$$。

#### 3. 总结

逻辑斯谛回归模型的主要思想就是在不知道数据的分布情况时，假定其满足线性判别函数，对其进行倒推得到参数，从而实现对数据的分类。