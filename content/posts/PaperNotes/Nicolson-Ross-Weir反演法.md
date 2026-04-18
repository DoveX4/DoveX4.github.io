---
date: 2026-03-16
draft: false
title: 论文笔记 | NRW反演法
categories:
  - 微波网络
tags:
  - S矩阵
  - 等效媒质常数
---
本文为论文\[1]\[2]\[3]的阅读笔记
# 模型构建[1]
在一个特征阻抗为$Z_0$的同轴线内插入一段长度为$d$，特征阻抗为$Z$的圆环板，其截面图如下所示：
![](attachments/Pasted%20image%2020260316212045.png)
假设此时有一道左边传来的电磁波，由微波理论，有：$$\Gamma=\frac{Z-Z_0}{Z+Z_0}=\frac{\sqrt{\frac{\mu_r}{\varepsilon_r}}-1}{\sqrt{\frac{\mu_r}{\varepsilon_r}}+1} \tag{1}$$
表示从电磁波同轴线入射到插入介质中的反射系数，同理，从插入介质入射到同轴线中的反射系数便为$-\Gamma$
$$z=e^{-j\omega d\sqrt{\mu\varepsilon}}=e^{-j\frac{\omega}{c_0}d\sqrt{\mu_r \varepsilon_r}} \tag{2}$$
表示电磁波在介质中的传播因子。由于同轴线中的传播主模为TEM模，所以式中没有截止波数项。

由此，可以建立关于入射电压的信号流图：
![](attachments/Pasted%20image%2020260316213004.png)
其中，A'点表示从B点反射的回波到达的逻辑节点，其应当与A点处于相同的物理位置，为更清晰的物理表达，将两点在流图中分离

> [!tip] 对A和A'更深入的思考
> 我起初建立信号流图时想单纯按照介质的物理性质来建立。我是这样考虑的：
> 由于每个分界面都能够透射电磁波，电磁波将在整个介质中存在；由于每个分界面都能够反射电磁波，按照不同方向，电磁波将有以下四条路径：
> 1. 来自左边的波传到A点，反射回左边
> 2. 来自B点的波传到A点，反射回B点
> 3. 来自A点的波传到B点，反射回A点
> 4. 来自右边的波传到B点，反射回右边
> 
> 于是便能够以入射波$V_i$，A点，B点，出射波$V_o$四个节点建立信号流图。
> 但实际以这个思路建立，确定各路径的增益的时候会遇到巨大的困难。
> 
> 比如：从A到B这一前向路径的增益是多少？
> 如果只看路径3，即从A到B这一路径，应该是$z$；但如果考虑路径1，从左边透射过来的电磁波，应该是$(1+\Gamma)z$；如果考虑路径2的反射，则似乎应该是$-\Gamma z$。而且这三个增益作用的主语也不一样，它们依次是A处的总电磁波、从左边来的入射波和从B点来的反射波，它们一定是不能同时作用在一个节点上的。
> 
> 这一思路遇到困难的根本原因是，这种处理方法会导致不同方向的入射波和反射波同时存在于节点上，而且说明不了反射波产生的原因，也就是节点数少于变量数。
> 上图的方式之所以能解决这一困难，原因是它只从入射波$E_+$出发，依靠多个逻辑节点，逐步推出了每个物理节点上（最多4个）不同方向上的电磁波分量。

由S参数的定义，结合流图可以得出：$$S_{11}(\omega)=\frac{V_A}{V_{inc}}=\frac{(1-z^2)\Gamma}{1-\Gamma^2 z^2},\quad S_{21}(\omega)=\frac{V_B}{V_{inc}}=\frac{(1-\Gamma^2)z}{1-\Gamma^2 z^2} \tag{3}$$至此，我们已经有了$\Gamma$和$z$的二元方程组，接下来就要解出它们，并进一步得到$\varepsilon$和$\mu$
# Nicolson-Ross反演流程[1]
由于实际测量中测出的是S参数，下面将由S参数重新推出所求的介电常数和磁导率
略去推导过程，首先构造中间变量$X$：$$X=\frac{S_{11}^2-S_{21}^2+1}{2S_{11}} \tag{4}$$
此时有：$$\Gamma=X\pm \sqrt{X^2-1} \tag{5}$$$$z=\frac{S_{11}+S_{21}-\Gamma}{1-(S_{11}+S_{21})\Gamma} \tag{6}$$
由两者的定义，有：$$Z_r=\sqrt{\frac{\mu_r}{\varepsilon_r}}=\frac{1+\Gamma}{1-\Gamma},\quad c_r=\sqrt{\mu_r \varepsilon_r}=j\frac{c_0}{\omega d}\mathrm{Ln}~\frac{1}{z} \tag{7}$$
最后，有：$$\mu_r=Z_r c_r,\quad \varepsilon_r=\frac{c_r}{Z_r} \tag{8}$$
# 相位修正
在求$c_r$的时候，出现了$\mathrm{Ln}~\frac{1}{z}$，由于复变对数函数的多值性，求解等效常数时会有无穷多个可能的解。将传播因子表示为$z=|z|e^{j\phi}$，实际测量和计算出的$\varphi$是主值，其与真实相位相差$2\pi n$，即$\phi=\varphi+2\pi n$。

为了解决这一问题，可以选用很薄的样本来测量其等效常数，其长度需要满足$$L<\frac{\lambda}{2} \tag{9}$$才能保证不发生相位的跳变。
## Weir的群时延法[2]
另一方面，Weir提出了基于群延迟的解决方案，他定义了传播因子相位的群延迟，那么：$$\tau_g=\frac{1}{2\pi} \frac{\mathrm{d} (-\phi)}{\mathrm{d} f} \tag{10}$$对频率求导以后，$2\pi n$的影响就消失了，也就是说群延迟是与$n$无关的物理量，能够测量出唯一的、真实的群延迟（实际测量时，采用数值微分计算）。
而对于反演过程中解出的多组$(\varepsilon_r^{(n)},\mu_r^{(n)})$，如果有一个关系能够用等效常数表示群延迟，那么对每个$n$，都可以通过等效常数通过数值微分计算出群延迟$\tau_g^{(n)}$，当$$\tau_g^{(n)}-\tau_g\simeq 0 \tag{11}$$时，即可认为是正确的相位。为了得到这个关系，我们从色散方程出发，用$z=e^{-\gamma d}=e^{-(\alpha+j\beta)d}$表示传播常数，则：$$\gamma^2=k_c^2 -k^2=(\frac{2\pi}{\lambda_c})^2-(\frac{2\pi}{\lambda_0})^2\mu_r\varepsilon_r \tag{12}$$
其中$\lambda_c$为此传播模式的截止频率（对TEM模，这一变量为$\infty$）。用此式计算的相位为：$$-\phi=-j\gamma d=2\pi d\sqrt{\frac{\mu_r\varepsilon_r}{\lambda_0^2}-\frac{1}{\lambda_c^2}} \tag{13}$$因此，$$\tau_{g}^{(n)}=d\cdot\frac{\mathrm{d}}{\mathrm{d}f}\sqrt{\frac{ \mu_r^{(n)}\varepsilon_r^{(n)}}{\lambda_0^2}-\frac{1}{\lambda_c^2}} \tag{14}$$相位一旦确定，等效常数的虚部也能随之确定，由$\mu=\mu_0 (\mu'_r-j\mu''_r)$和$\varepsilon=\varepsilon_0 (\varepsilon'_r-j\varepsilon''_r)$可以计算损耗角正切：$$\tan \delta=\frac{\delta''_r}{\delta'_r}=\frac{\mu'_r \varepsilon''_r+\mu''_r \varepsilon'_r}{\mu'_r \varepsilon''_r-\mu''_r \varepsilon'_r} \tag{15}$$和衰减常数：$$\alpha=\frac{\pi\sqrt{2\delta'_r}}{\lambda_0}\sqrt{\sqrt{1+\tan^2 \delta}-1} \tag{16}$$
实际算法中不会真的像上述那样，用不同的$n$去试误差。通常的做法是，从一个很小的、接近0的频率开始计算——这个起始频率能够保证满足(9)的条件——再以一个小步长逐步增加频率，当计算出的相邻步长的等效常数发生了相位跳变，就在相位上加一个$2n\pi$。
## 基于两个样本厚度的相位修正[3]
然而，如果采用Weir的算法，通常很难从一个很低的频率开始计算/测量。为了解决这一问题，可以测量同一材料不同厚度的两个样本，通过引入更多的信息修正相位。对于一个给定的频率，两组测量结果只能有一个正确的相位。
假设对于$2n\pi$的相位分支，对于厚度$L_1$，有一组结果$(\varepsilon_{r1} (n, f),\mu_{r1} (n, f))$；对另一个厚度$L_2$的样本，有另一组结果$(\varepsilon_{r2} (n, f),\mu_{r2} (n, f))$，由于厚度不同，这两组结果相位跳变的频率也不一样。如果在一个足够大的$n$的范围内，这两组结果取到特定的$n_1$和$n_2$时，相位非常接近，那就可以认为此时相位是真实的。以两组结果的平方欧几里得距离作为其是否接近的量度：$$\mathrm{ERROR}(f_0)=(\varepsilon'_{r1}-\varepsilon'_{r2})^2+(\varepsilon''_{r1}-\varepsilon''_{r2})^2+(\mu'_{r1}-\mu'_{r2})^2+[\mu''_{r1}-\mu''_{r2}]^2 \tag{17}$$其中每个变量都同时是$n$和$f$的函数。
# 数值发散问题[3]
由公式(4)可见，反演算法会在$S_{11}=0$时失效。这一情况在实际测量过程中也会出现，先给出结论：当无损样本厚度恰好等于半波长及其整数倍时，反演算法会失效。
直接来考察$S_{11}$，由(3)，令$S_{11}=\frac{(1-z^2)\Gamma}{1-\Gamma^2 z^2}=0$，则：$$|\Gamma||1-e^{-2\gamma d}|=0 \tag{18}$$
假设反射系数不为0，$\gamma = \alpha+j \beta$，则有：$$|1-e^{-2\alpha d}(\cos (-2\beta d)+j\sin (-2\beta d))|=0$$对这个方程，其实部和虚部必须同时为0。从实部解出：$$d=\frac{k\lambda_g}{4},~k\in \mathbb{Z} \tag{19}$$其中$\lambda_g$是此时的频率对应的波长。从虚部进一步解出，只有$k=2n$时，方程才有解，即：$$d=\frac{n\lambda_g}{2}\tag{20}$$另外，从虚部同时解出$\alpha=0$，结论得证。
在工程上，对于一个给定的频率，其最佳样本长度应当满足：$d=(2n+1)\frac{\lambda_g}{4}$。此时$|S_{11}|$较大，NRW算法运行较为稳定。




[1] NICOLSON A M, ROSS G F. Measurement of the intrinsic properties of materials by time-domain techniques[J/OL]. IEEE Transactions on Instrumentation and Measurement, 1970, 19(4): 377-382. DOI:[10.1109/TIM.1970.4313932](https://doi.org/10.1109/TIM.1970.4313932).
[2] WEIR W B. Automatic measurement of complex dielectric constant and permeability at microwave frequencies[J/OL]. Proceedings of the IEEE, 1974, 62(1): 33-36. DOI:[10.1109/PROC.1974.9382](https://doi.org/10.1109/PROC.1974.9382).
[3] VICENTE A N, DIP G M, JUNQUEIRA C. The step by step development of NRW method[C/OL]//2011 SBMO/IEEE MTT-S International Microwave and Optoelectronics Conference (IMOC 2011). Natal, Brazil: IEEE, 2011: 738-742[2026-03-23]. [http://ieeexplore.ieee.org/document/6169318/](http://ieeexplore.ieee.org/document/6169318/). DOI:[10.1109/IMOC.2011.6169318](https://doi.org/10.1109/IMOC.2011.6169318).