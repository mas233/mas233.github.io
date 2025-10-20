---
title: "Introduction to ChatGPT & Machine Learning"
description: "Machine Learning 2023 Spring By Hung-Yi Lee #1"
date: 2025-10-20 14:00:00 +0800
author: mas
categories: [Machine Learning 2023 Spring]
tags: [Generative AI,Machine Learning, AI]
math: true
---

# ChatGPT概览
ChatGPT是一个巨大的语言模型（类似函数），作用是猜测下一个词汇（或token）并输出。
\\
GPT: **Generative Pretrained Transformer**

## 预训练
GPT到ChatGPT是从自监督学习到监督学习的成果。自监督学习过程被称为预训练，训练出的模型称作基石模型。例如，从“世界第一高峰是喜马拉雅山”中训练出能够在“世界第一高峰是”后面猜出“喜马拉雅山”的训练过程。
![alt text](assets/img/post-imgs/25-10-20-ml-1/pretrain1.png)

Multi-BERT在多种语言上做预训练后，只需要教某一个语言的某个任务，就可以自动学会其它语言的同样任务。

# 机器学习概览
机器学习的目标是找一个函数，使得它对于给定的输入，能够给出期望的输出。

## 分类
- 回归(Regression)：函数的输出是一个数值。
- 分类(Categorization)：函数的输出是一个类别。
- 生成式学习(Generative Learning)：生成结构化的输出，如图片、文字等。

\\
ChatGPT实际做的事情是一个分类问题，但使用者的感受是生成式学习。

## 三阶段之一-设定范围(Model)
找出候选函数的集合，深度学习中的神经网络结构（如CNN，RNN，Transformer等）就是不同的候选函数集合。通常以$$\mathcal{H}$$来表示。

> Deep Learning(CNN, Transformer), Decision Tree, etc.

## 三阶段之二-评价函数好坏(Loss Function)
函数的输出和标准答案之间的差距大小，可以用来评价函数好坏。一般以Loss function来定义函数评价函数。（传入一个函数，输出这个函数的好坏）函数分为训练和测试两个过程（拟合、过拟合、欠拟合）。

> Supervised Learning, Semi-supervised Learning, RL, etc.

## 三阶段之三-找出最好的函数(Optimization)
通过一些数学手段找出最好的函数。通过枚举的方式不现实。通过设置超参数(Batch Size, Learning Rate, Initialization...)来获得某组模型下最理想的函数。

> Gradient Descent(Adam, AdamW, ...), Generic Algorithm, etc.

