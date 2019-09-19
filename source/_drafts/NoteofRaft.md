---
title: Raft学习笔记
date: 2019-07-19 14:00
updated: 2019-07-26 15:00
tags: [Raft]
categories: Raft
mathjax: true
description: 
---

# 概要

Paxos算法**核心思想**：

- 在抢占式访问权基础上引入多个Acceptor；
- 保证一个epoch，只有一个Proposal运行，Proposal按照epoch递增的顺序依次运行；
- 新epoch的Proposal采用“后者认同前者”的思路运行：
  - 在肯定旧的epoch无法生成确定性取值时，新的epoch会提交自己的取值，不会冲突；
  - 一旦旧的epoch行程确定性取值，新的epoch肯定可以获取到此取值，并且会认同此取值，不会破坏。