---
title: 信息论基础Ch1&2
date: 2017-10-2 17:06
updated: 2017-10-3 11:10
tags: 信息论
categories: 课程
mathjax: true
description: 
---

# 信息论基础

## 1. 绪论

临界数据压缩的值（熵）

临界通信传输速率的值 （信道容量）

熵，互信息，通信信道，相对熵

## 2. 熵、相对熵与互信息

### 2.1 熵

信息熵的三个公理：

1. 顺序无关 $H(p_1, …, p_k) = H[ \pi(p_1, …, p_k) ]$

2. 最大值 均匀分布熵值最大

3. 可加性

   设 $ p\_k = p\_{11} + p\_{12}+ …+p\_{1l} $ , 则:
   $$
   \begin{split}
   H(p_1, ..., p_{k-1}, p _{11}, p_{12}, … p_{1l}) 
   = H(p_1, p_2, ..., p_k)+ p_kH(\frac{p_{11}}{p_k}, \frac{p_{12}}{p_k}, ..., \frac{p_{1l}}{p_k})
   \end{split}
   $$

熵:    $H(X) = -\sum_{x \in X}p(x)\log_2{p(x)}$
<!--more-->

### 2.2 联合熵与条件熵

联合熵： $H(X,Y) = - \sum_{k=1}^K\sum_{j=1}^J p(a_k, b_j)log{p(a_k, b_j)}$

条件熵： $H(Y|X) = \sum_{x\in X}p(x)H(Y|X=x) = - \sum_{x\in X}\sum_{y\in Y}p(x, y)logp(y|x)$

**二者关系** 链式法则： $H(X, Y) = H(X) + H(Y|X) = H(Y) + H(X|Y)$

推论： $H(X, Y|Z) = H(X|Z) + H(Y|X, Z)$

独立时：$H(X, Y) = H(X) + H(Y) = H(Y) + H(X)$ 

​		联合熵等于单个随机变量熵之和

​		条件熵等于无条件熵（绝对熵）

平均意义下，条件熵不大于绝对熵

若X,Y有确定的函数关系，$H(Y|X) = H(X|Y) = 0$    $H(X,Y) = H(X)$ 或  $H(X,Y) = H(Y)$

### 2.3 相对熵与互信息

  





