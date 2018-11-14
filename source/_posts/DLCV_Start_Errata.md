---
title: Deep Learning for Computer Vision with Python 勘误
date: 2018-11-10 17:06
updated: 2017-11-14 17:10
tags: [计算机视觉,勘误,Adrian Rosebrock]
categories: 计算机视觉
mathjax: true
description: 阅读 Adrian Rosebrock的书时发现的一些错误
---

# 写在前面
此为个人笔记，记录不如官网那么全，建议大家去官网查BUG

# 条目
1. P100 9.1.6 `gradient_descent.py`

   ```python
   preds[preds > 0] = 1 # Wrong
   preds[preds > 0.5] = 1 # Right
   
   plt.scatter(testX[:, 0], testX[:, 1], marker='o', c=testY, s=30) # Wrong
   plt.scatter(testX[:, 0], testX[:, 1], marker='o', c=testY[:, 0], s=30) # Right
   ```

2. P107 `sgd.py` 同上

3. P154 `keras_mnist.py` 中，若是第一次使用`datasets.fetch_mldata（"MNIST Original")`，且始终无法下载该数据集，可以手动下载数据集 [mnist-original.mat](https://www.kaggle.com/avnishnish/mnist-original/version/1)，再指定存放位置

   ```python
   # 可参考路径
   # |- pyimagesearch
   # | |- datasets 
   # |    |- mldata
   # |       |- mnist-original.mat
   # |- keras_mnist.py
   
   # 修改代码
   dataset = datasets.fetch_mldata（"MNIST Original", data_home="./pyimagesearch/datasets")
   ```
