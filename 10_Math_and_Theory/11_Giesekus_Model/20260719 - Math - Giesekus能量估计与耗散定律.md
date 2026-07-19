---
title: Giesekus模型的能量估计与耗散定律
type: ai-assisted-learning-note
status: requires-manual-verification
tags: ["#Math", "#Giesekus模型", "#收敛性证明", "#Status/逻辑断点"]
---

> [!warning] 逻辑断点待人工核查
> 能量恒等式的形式推导要求足够正则性、$det F>0$、允许的测试函数和使边界项消失的条件。弱解层面的不等式或等式形式须对照原文核对。

> [!abstract]
> 汇总 Giesekus 模型的总能量、耗散项和测试函数直观，为后续逐项验证能量机制提供入口。

# Giesekus 模型的能量估计与耗散定律

## 学习导航

- 阶段：3/9，能量恒等式总览。
- 前置：[[12_Functional_Analysis/20260719 - Math - 弱解速度场函数空间|弱解速度场函数空间]]。
- 后续：[[20260719 - Math - Giesekus能量推导关键结构|能量推导关键结构]]。
- 路线：[[10_Math_and_Theory/20260719 - Math - Giesekus与混合有限元学习路线|Giesekus 与混合有限元学习路线]]。

在偏微分方程（PDE）的数学分析和数值计算中，能量耗散律提供关键的先验估计与稳定性结构；其适用范围和严格形式取决于解的正则性及边界条件。

这篇论文的核心数学基石，就是原论文第 3 页的 **公式 (1.6)**。作者通过这一公式，给所有的物理变量套上了一层“紧箍咒”。

## 核心公式 (1.6)

$$\underbrace{ \int_{\Omega} \left( \frac{\rho}{2}\vert{}v(t)\vert{}^2 + \frac{\mu}{2}\vert{}\mathbb{F}(t)\vert{}^2 - \frac{\mu}{2}\ln \det(\mathbb{F}(t)\mathbb{F}(t)^\top) \right) }_{\text{当前时刻 } t \text{ 的系统总能量}}$$$$+ \underbrace{ \int_0^t \int_{\Omega} \left( \nu\vert{}\nabla v\vert{}^2 + \frac{\mu^2}{2\lambda}\vert{}\mathbb{F}\mathbb{F}^\top - \mathbb{I}\vert{}^2 \right) }_{\text{从 } 0 \text{ 到 } t \text{ 时刻累积消耗掉的能量 (耗散项)}}$$$$= \underbrace{ \int_{\Omega} \left( \frac{\rho}{2}\vert{}v_0\vert{}^2 + \frac{\mu}{2}\vert{}\mathbb{F}_0\vert{}^2 - \frac{\mu}{2}\ln \det(\mathbb{F}_0\mathbb{F}_0^\top) \right) }_{\text{初始时刻 } t=0 \text{ 的系统总能量}}$$

_(注：原公式中的等式关系，说明系统是一个**纯消耗**过程，没有任何外部能量注入。当前能量一定小于或等于初始能量。)_

## 测试函数的选取与函数空间

在阅读论文第 3 页时，作者写道："Formally, testing (1.1a) with $v$ and (1.1c) with $\mu(\mathbb{F} - \mathbb{F}^{-\top})$..."。这里的测试函数选取大有玄机。

### 1. 测试函数可以“自定义”吗？

**答案是：定义方程弱解时可以随便选，但推导能量定律时绝对不行！**

- **一般弱形式（可以自定义）**：如果只是为了定义什么是 PDE 的“弱解”（如论文第 5 页 Definition 2.1），测试函数可以使用通用的 $\mathbb{G}$。

- **能量推导（专属定制）**：为了得到系统的能量衰减公式，必须用系统自带的“变分导数”去测试方程。作者精挑细选的 $\color{red}{\mu(\mathbb{F} - \mathbb{F}^{-\top})}$ 是一把被“逆向工程”强行定制出来的专属钥匙，换成任何其他函数都无法凑出完美的能量守恒定律。


### 2. 为什么选择 $\mu(\mathbb{F} - \mathbb{F}^{-\top})$？

将这把钥匙插进形变梯度方程 (1.1c) 中，它能完美拆解出两部分能量：

- **前半部分** $\mathbb{F}$：当它与方程里的时间导数 $\partial_t \mathbb{F}$ 结合做内积时，根据微积分 $\mathbb{F} \cdot \partial_t \mathbb{F} = \frac{1}{2}\partial_t \vert{}\mathbb{F}\vert{}^2$。这完美凑出了弹簧的**弹性势能** $\frac{\mu}{2}\vert{}\mathbb{F}\vert{}^2$。

- **后半部分** $-\mathbb{F}^{-\top}$ **(逆转置矩阵)**：在线性代数和矩阵微积分中，矩阵行列式的对数的导数，刚好等于它的逆转置（即 $\frac{d}{dt} \ln(\det \mathbb{F}) = \mathbb{F}^{-\top} : \partial_t \mathbb{F}$）。因此，这部分极其精妙地凑出了那个保命的**对数惩罚项** $-\frac{\mu}{2}\ln \det(\mathbb{F}\mathbb{F}^\top)$。


### 3. 测试函数所在的数学空间与 "Formally" 的深意

这个测试函数到底属于哪个数学空间？为什么作者在推导前特意加了 **"Formally"（形式上地）** 这个免责词？

- **常规空间**：在连续空间中，普通的测试函数 $\mathbb{G}$ 以及形变梯度 $\mathbb{F}$ 本身，都属于 Sobolev 空间 $H^1(\Omega; \mathbb{R}^{d \times d})$（即函数本身和它的一阶空间导数都是平方可积的）。

- **致命的隐患**：测试函数的后半部分 $\mathbb{F}^{-\top}$ 的存在，要求 $\det(\mathbb{F})$ 绝对不能等于 0。如果在逼近计算的过程中 $\det(\mathbb{F}) \to 0$，那么 $\mathbb{F}^{-\top}$ 会瞬间爆炸到无穷大。**一旦爆炸，它就根本不再属于合法的** $H^1$ **测试函数空间！**


**结论**：作者在这里得出能量守恒定律，是基于“解足够光滑且行列式严格大于 0”的理想物理状态假设。但在后续几十页的严谨数学证明中，作者**根本不敢**直接把这个具有爆炸风险的函数当测试函数用。他们不得不使用极其复杂的替代手段（如离散化近似、局部压力重构、Aubin-Lions 紧致性引理等）来侧面证明能量确实是耗散的。这也是这篇论文能够发表的硬核成就之一。

## 公式逐项拆解与物理意义

### 1. 当前时刻的总能量 (Energy at time $t$)

这一部分评估了在任意时刻 $t$，流体内部还剩下多少能量。它由三项组成：

- **动能 (Kinetic Energy)**： $\frac{\rho}{2}\vert{}v(t)\vert{}^2$

    - 这就是我们熟知的 $\frac{1}{2}mv^2$ 的连续介质版本，代表水流运动所携带的能量。

- **弹性势能 (Elastic Energy)**： $\frac{\mu}{2}\vert{}\mathbb{F}(t)\vert{}^2$

    - 代表高分子聚合物（橡皮筋）被拉伸和变形所储存的势能。

- **🚨 对数惩罚项 (Logarithmic Penalty)**： $-\frac{\mu}{2}\ln \det(\mathbb{F}(t)\mathbb{F}(t)^\top)$

    - 物理上要求流体微团不能被压缩到没有体积（即 $\det(\mathbb{F}) > 0$）。

    - 如果在数值计算中，某个点的 $\det(\mathbb{F})$ 快要跌到 $0$ 了，$-\ln(0)$ 会瞬间变成**正无穷大**。系统总能量被等式右边的“初始能量”死死压住，数学上绝不允许左边的能量飙升。因此，这个对数项强制把 $\det(\mathbb{F})$ 锁定在安全区，防止了程序的物理崩溃。


### 2. 累积耗散的能量 (Dissipation terms)

这部分代表了随着时间流逝，系统内部转化为热能等不可逆形式的能量。它保证了系统的波动最终会平息下来。

- **粘性耗散 (Viscous Dissipation)**： $\int \nu\vert{}\nabla v\vert{}^2$

    - 流体因为自身的粘性（内部摩擦）而不断消耗的动能。速度梯度（$\nabla v$）越大，摩擦发热越多。

- **弹性弛豫耗散 (Elastic Relaxation Dissipation)**： $\int \frac{\mu^2}{2\lambda}\vert{}\mathbb{F}\mathbb{F}^\top - \mathbb{I}\vert{}^2$

    - **Giesekus 模型的灵魂所在。** 聚合物在被拉伸后，会试图回缩。在这个回缩的过程中，聚合物链之间的剧烈摩擦和纠缠消耗了大量的能量。

    - 这个**平方项**来自于方程里的二次非线性项（超级刹车系统）。当聚合物形变偏离初始状态（$\mathbb{I}$）越大，能量消耗得就越疯狂，从而有效阻止了无限拉伸。


### 3. 初始总能量 (Initial Energy)

等式的右边，完全由系统在 $t=0$ 时刻给定的初始条件决定。

- 它是一个**固定常数**（只要初始数据是合理且有界的）。

- 它的存在，为左边的所有变量提供了一个不可逾越的**上限（Upper Bound）**。这就是“先验估计 (A priori estimate)”的核心：无论怎么演化，速度和形变都不会无限增大。
