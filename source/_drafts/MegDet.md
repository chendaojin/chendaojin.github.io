---
title: MegDet学习
date: 2018-12-7 14:00
updated: 2018-12-8 11:00
tags: [MegDet,Obeject Detection,CV]
categories: CV
mathjax: true
description: 
---
# Related Work

## two-stage

R-CNN： 基于CNN，先检测，后分类

SPPNet： 提升分类精度。使用Spatial Pyramid Pooling代替调整原始图大小

Fast-RCNN：将SPP简化为ROIPooling (Region of Interest Pooling)

Faster-RCNN：使用Region Proposal Network(RPN)代替传统的region proposal method。当proposal过大时，将耗费大量时间

R-FCN：Region-based Fully Convolutional Networks 对位置敏感

Deformable ConvNets：关注目标。学习offset，对不同location of feature maps做卷积

FPN：对小目标检测有重要意义，feature pyramid technique

Mask R-CNN：在目标检测和实体分割中都很有用 ROIAlign

## one-stage

one-stage通常比two-stage快，精度一般低于two-stage

YOLO：将输入图像分成7×7的网格，卷积层之后跟着FC

SSD：presents a fully convolutional network with different feature layers targeting different anchor scales

RetinaNet：focal loss which can reduce false positives in one-stage detectors

# Approach

小批量会导致学习过程太慢，而大批量需要大的学习率，所以首先要解决学习率的问题。

图像分类中的gradient equivalence未必适用于目标检测，所以作者提出了Variance Equivalence。经公式推导，当`batch_size`由$N$变成$k*N$时，学习率也要变成$\hat{r} = k*r$。为了保证收敛性，作者引用了*Linear Gradual Warmup*中的策略，使$r$以常数增长的方式逐渐增加到$\hat{r}$

批归一化(BN)通常用于图像分类，可以减少训练时间和保证收敛精度。本文作者大胆的将BN引入目标检测问题中，提出了Cross-GPU Batch Normalization

- [ ] TODO 记录一下算法



# Experiments

- 使用ImageNet已训练好的ResNet-50作为backbone network

- 使用FPN检测framework
- SGD优化 momentum=0.9 
- ……

- 训练策略有normal和long两种：normal策略在epoch 8和epoch 10时，将学习率乘以0.1，并结束于epoch 11；long策略在epoch 11和epoch 14时，将学习率乘以0.1，在epoch 17时将学习率减半，并结束于epoch 18

不加入BN：mini-batch size达到32就会开始出现问题，但确实加快了训练速度，同时低学习率会导致精度严重损失。即使使用warmup策略，在大批量和大学习率下，模型也变得难以训练。

加入BN：i. 与16-base的batch size相比，随着batch size的增大，精度与16-base的差不多， ii.  最好的BN size是32， iii. long策略下，最好的batch size是32