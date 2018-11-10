---
title: Deep Learning for Computer Vision with Python 勘误
date: 2018-11-10 17:06
updated: 2017-11-10 17:10
tags: [计算机视觉,勘误,Adrian Rosebrock]
categories: 计算机视觉
mathjax: true
description: 阅读 Adrian Rosebrock的书时发现的一些错误
---

# 写在前面
此为个人笔记，记录不如官网那么全，建议大家去官网查BUG

# 条目
1. P100 9.1.6 gradient_descent.py
```python
preds[preds > 0] = 1 # Wrong
preds[preds > 0.5] = 1 # Right

plt.scatter(testX[:, 0], testX[:, 1], marker='o', c=testY, s=30) # Wrong
plt.scatter(testX[:, 0], testX[:, 1], marker='o', c=testY[:, 0], s=30) # Right
```
2. 
