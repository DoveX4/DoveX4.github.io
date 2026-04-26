---
title: 论文笔记 | 定义在多模式微波网络矩阵上的Redheffer星积
date: 2026-04-26
categories:
  - 微波网络
draft: false
math: true
tags:
  - 极化
  - 传播模式
  - S矩阵
---
本文为论文\[1]的阅读笔记。


# 研究对象
在研究多层周期性材料时，往往会存在这样的情况：已知每一层的S矩阵，需要根据它们计算出多层材料整体的S矩阵。这种情况通常会用微波网络中的理论，将每一层看作一个二端口网络，将每层的S矩阵转换成T矩阵或A矩阵，通过矩阵乘法来表示网络的级联——即多层的堆叠——再将多层的T矩阵换回S矩阵。
然而，这种情况有一些弊端：其一是计算过程冗余，完全可以提出一种等价的、简化了的运算方法来避免由S到T再由T到S的运算过程；其二是这种方法只能定义在单模式二端口的模型上，无法描述多模式之间的耦合现象。
# 单模式二端口散射矩阵的表述

![](attachments/Pasted%20image%2020260426142635.png)

[1] RUMPF R C. Improved formulation of scattering matrices for semi-analytical methods that is consistent with convention[J/OL]. Progress In Electromagnetics Research B, 2011, 35: 241-261. DOI:10.2528/PIERB11083107.
