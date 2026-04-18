---
date: 2026-03-23
draft: false
title: 论文笔记 | 结合A矩阵的智能设计方法
categories:
  - 微波网络
tags:
  - MLP
  - S矩阵
  - A矩阵
---
本文为论文\[1\]的阅读笔记

# 研究对象
本文用嵌入物理信息的神经网络，对Frequency selective rasorber (FSR)建立了代理模型，并将其命名为neuro-TLT model
FSR是一种用FSS和吸波材料实现的一种电磁功能材料，中文名为“频率选择吸波体”。通过FSS和吸波材料的堆叠，能够实现传输特定频率的电磁波并吸收其他频段电磁波的功能
# 核心思想
本文所用的物理信息是A矩阵。
首先，对每一层，都能够根据多个参数样本计算出的S参数进行神经网络建模。对第$i$层，能够用神经网络预测出$\mathbf{S}_i$
然后，将S矩阵转换为可以级联的A矩阵，对第$i$层，有：$$D_i=\frac{(1-S_{11(i)})(1-S_{22(i)})-S_{12(i)} S_{21(i)}}{2\cdot S_{21(i)}},\quad \mathbf{A}_i=\begin{bmatrix} D_i & Z_c\cdot D_i \\ \frac{1}{Z_c}\cdot D_i & D_i \end{bmatrix}$$上式中，除$Z_c$表示特征阻抗以外，每个变量都是参数向量$\mathbf{x}_i$和频率$f$的函数
将每一层的$\mathbf{A}_i$乘起来得到总的$\mathbf{A}$以后，再用下式恢复到S参数上，计算材料电磁特性：$$S_{11}=\frac{A_{11}+\frac{A_{12}}{Z_0}-A_{21}\cdot Z_0-A_{22}}{A_{11}+\frac{A_{12}}{Z_0}+A_{21}\cdot Z_0+A_{22}},\quad S_{21}=\frac{2}{A_{11}+\frac{A_{12}}{Z_0}+A_{21}\cdot Z_0+A_{22}}$$这里由于对于FSR这个整体，周围的材料都是空气，所以特征阻抗改为$Z_0$
# 网络架构
每层的神经网络采用最简单的单隐藏层MLP架构，如下：
![](attachments/Pasted%20image%2020260323142740.png)
本文对每层训练时，把25个样本用于训练、16个样本用于测试，这样得到的总体的训练误差和测试误差在5%左右。另外列出拓扑数据以供参考：本文建模的FSS，其金属层的最小线宽是0.3mm，单元边长为36mm

[1] LI M Y, ZHANG J W, XU L Y, 等. Physics-embedded neural network approach to low-cost parametric modeling of multi-layer frequency-selective rasorbers[J]. 1-3.