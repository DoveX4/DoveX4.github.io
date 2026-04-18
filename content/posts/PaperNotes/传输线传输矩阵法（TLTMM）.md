---
date: 2026-03-14
draft: false
title: 论文笔记 | 传输线传输矩阵法（TLTMM）
categories:
  - 微波网络
tags:
  - TLTMM
  - 多层介质
---
本文为论文\[1]的阅读笔记
# 核心思想
![](attachments/Pasted%20image%2020260314152027.png)
对于上图所示的多层介质结构，将其等效为下图所示的多层传输线模型：
![](attachments/Pasted%20image%2020260314152128.png)
对于每一层和每一个分界面，都可以定义层间传输矩阵$L$和分界面不连续矩阵$I$：$$\begin{bmatrix} E_{(\ell+1)}^+  \\ E_{(\ell+1)}^-\end{bmatrix}=L_{(\ell+1)}\begin{bmatrix} {E'}^+_{(\ell+1)} \\ {E'}_{(\ell+1)}^-\end{bmatrix},\quad \begin{bmatrix} E_{(\ell+1)}^+  \\ E_{(\ell+1)}^- \end{bmatrix}=I_{{(\ell+1)}\ell} \begin{bmatrix} E_{\ell}^+  \\ E_{\ell}^- \end{bmatrix}$$
其中等式两侧变量的定义如下图所示：
![](attachments/Pasted%20image%2020260314152925.png)
我们发现，如此定义的$L$和$I$和微波网络理论中的矩阵$[A]$完全一致。
# 算法流程
0：极化类型$\text{TE/TM}$、入射角度$\theta$、各层厚度$h_{\ell}$、各层损耗角正切$\tan\delta_{\ell}$、随频率变化的各层的等效常数（等效介电常数$\varepsilon_{\ell}$、等效磁导率$\mu_{\ell}$、等效电导率$\sigma_{\ell}$）
1：求传播常数$$\gamma_{\ell}=j\omega \sqrt{\mu_\ell \varepsilon_\ell}$$
2：求层内传输矩阵$$L_{(\ell+1)}=\begin{bmatrix} e^{-\gamma_{(\ell+1)_z} h_{(\ell+1)}} & 0 \\ 0 & e^{\gamma_{(\ell+1)_z}h_{(\ell+1)}} \end{bmatrix}$$
3：求单层波阻抗$$\eta_\ell=\sqrt{\frac{\mu_\ell}{\varepsilon_\ell}}$$
4：求TE/TM对应的偏振因子$$p_{(\ell+1)\ell}^{\text{TE}}=\frac{\eta_{(\ell+1)}\sec \theta_{(\ell+1)}}{\eta_{\ell}\sec \theta_{\ell}},\quad p_{(\ell+1)\ell}^{\text{TM}}=\frac{\eta_{\ell}\cos\theta_{\ell}}{\eta_{(\ell+1)}\cos\theta_{(\ell+1)}}$$
5：求层间传输矩阵$$I_{(\ell+1)\ell}^{\text{TE/TM}}=\frac{1}{2}\begin{bmatrix}1+p_{(\ell+1)\ell}^{\text{TE/TM}} & 1-p_{(\ell+1)\ell}^{\text{TE/TM}} \\ 1-p_{(\ell+1)\ell}^{\text{TE/TM}} & 1+p_{(\ell+1)\ell}^{\text{TE/TM}}\end{bmatrix}$$6：计算一整层的传输矩阵$$T_{(\ell+1)\ell}=L_{(\ell+1)}I_{(\ell+1)\ell}$$
7：计算全部层级联后的传输矩阵$$T_{(N+1)0}=T_{(N+1)N}T_{N(N-1)}\cdots T_{(\ell+1)\ell}\cdots T_{10}$$
8：由以下方程解出反射系数和透射系数$$\begin{bmatrix}S_{21}\\0\end{bmatrix}=T_{(N+1)0}\begin{bmatrix}1\\S_{11}\end{bmatrix}$$
具体地，有：$$S_{11}=-\frac{T_{21}}{T_{22}}, \quad S_{21}=\frac{\text{det}(T)}{T_{22}}$$
[1] ORAIZI H, AFSAHI M. ANALYSIS OF PLANAR DIELECTRIC MULTILAYERS AS FSS BY TRANSMISSION LINE TRANSFER MATRIX METHOD (TLTMM)[J/OL]. Progress In Electromagnetics Research, 2007, 74: 217-240. DOI:[10.2528/PIER07042401](https://doi.org/10.2528/PIER07042401).