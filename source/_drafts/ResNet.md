---
title: ResNet学习
date: 2018-12-7 14:00
updated: 2018-12-8 11:00
tags: [ResNet,CV]
categories: CV
mathjax: true
description: 
---

深度：
AlexNet：5层卷积层
VGGNet：19层
GoogleNet：22层
ResNet：152层

增加网络的深度容易带来梯度消失/爆炸的问题，ResNet引入了“恒等映射”(Identity Shortcut Connection)，通过跳过一层或多层，以解决这个问题。

如果identity mapping是最优的，那么残差应该是0



related work

Residual Representations

偏微分方程 -> 多重网格方法(Multigrid method)

Shortcut Connections



Deep Residual Learning

