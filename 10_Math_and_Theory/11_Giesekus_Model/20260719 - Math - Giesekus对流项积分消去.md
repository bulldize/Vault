---
title: Giesekus对流项积分消去
type: ai-assisted-learning-note
status: requires-manual-verification
tags: ["#Math", "#Giesekus模型", "#理论草稿", "#Status/逻辑断点"]
---

> [!warning] 逻辑断点待人工核查
> 对流项消失需明确 $v$ 的无散性、边界通量或无滑移条件，以及 $F$、$\log\det F$ 的可积性和链式法则适用范围。

> [!abstract]
> 单独展开形变梯度对流项与能量测试函数的积分处理，定位链式法则、分部积分和不可压缩条件的作用。

# 深度解密：对流项积分如何完美消零

## 学习导航

- 阶段：5/9，对流项核查。
- 前置：[[20260719 - Math - Giesekus能量推导关键结构|能量推导关键结构]]。
- 后续：[[20260719 - Math - Giesekus无量纲化与弱解定义|无量纲化与弱解定义]]。
- 路线：[[10_Math_and_Theory/20260719 - Math - Giesekus与混合有限元学习路线|Giesekus 与混合有限元学习路线]]。

在推导 Giesekus 模型的能量耗散定律时，我们要计算对流项 $(v \cdot \nabla)\mathbb{F}$ 与测试函数 $\mu(\mathbb{F} - \mathbb{F}^{-\top})$ 的内积积分。

该积分 $\int_{\Omega} (v \cdot \nabla)\mathbb{F} : \mu(\mathbb{F} - \mathbb{F}^{-\top}) \, dx$ 可拆成两部分，并在满足链式法则、分部积分、边界项消失和不可压缩条件 $\operatorname{div}(v)=0$ 时消去。

以下是去掉了常数 $\mu$ 后的详细推导过程：

## 第一半：对流项 $\times$ 前半个测试函数 $\mathbb{F}$

我们要算的是：

$$\int_{\Omega} (v \cdot \nabla)\mathbb{F} : \mathbb{F} \, dx$$

**第 1 步：用链式法则把“冒号”吃掉** 这里的 $(v \cdot \nabla)\mathbb{F}$ 就是矩阵 $\mathbb{F}$ 顺着水流 $v$ 方向的方向导数。 根据微积分求导法则 $x \cdot x' = \frac{1}{2}(x^2)'$，在矩阵双点积里完全一样：

$$(v \cdot \nabla)\mathbb{F} : \mathbb{F} = \frac{1}{2} v \cdot \nabla (\vert{}\mathbb{F}\vert{}^2)$$

> _注：_$\vert{}\mathbb{F}\vert{}^2$ _就是矩阵所有元素的平方和，现在它变成了一个标量数字！_

**第 2 步：分部积分（散度定理）** 现在积分变成了 $\int_{\Omega} \frac{1}{2} v \cdot \nabla (\vert{}\mathbb{F}\vert{}^2) \, dx$。 遇到“速度点乘梯度的积分”，标准操作就是把梯度 $\nabla$ 扔到速度 $v$ 身上（也就是分部积分）：

$$\int_{\Omega} v \cdot \nabla (\vert{}\mathbb{F}\vert{}^2) \, dx = - \int_{\Omega} (\nabla \cdot v) \vert{}\mathbb{F}\vert{}^2 \, dx + \int_{\partial \Omega} (v \cdot \vec{n}) \vert{}\mathbb{F}\vert{}^2 \, ds$$

- **边界项（最后那个积分）**：因为水在一个封闭水池里，边界上没有水流出（或者在边界上速度 $v=0$），所以边界项 $= 0$。

- **内部项**：因为水是不可压缩的，所以散度 $\nabla \cdot v = 0$（也就是我们常写的 $\text{div}(v) = 0$）！这就导致内部项也 $= 0$。


**结论 1：在上述前提下，第一部分积分为** $0$**。**

## 第二半：对流项 $\times$ 后半个测试函数 $(-\mathbb{F}^{-\top})$

我们要算的是：

$$-\int_{\Omega} (v \cdot \nabla)\mathbb{F} : \mathbb{F}^{-\top} \, dx$$

**第 1 步：雅可比公式 (Jacobi's formula)** 这里要用到线性代数里一个极其经典的恒等式（也就是对数惩罚项的来源）：对于任何可逆矩阵 $A$，它的行列式的对数的微分为：

$$d(\ln \det A) = A^{-\top} : dA$$

所以，把 $(v \cdot \nabla)$ 当作导数算子，上面那坨双点积可以直接合并成：

$$(v \cdot \nabla)\mathbb{F} : \mathbb{F}^{-\top} = v \cdot \nabla (\ln \det \mathbb{F})$$

> _注：你看，原本复杂的矩阵乘法，又被压缩成了一个标量数字的梯度！_

**第 2 步：如法炮制的分部积分** 积分变成了 $\int_{\Omega} v \cdot \nabla (\ln \det \mathbb{F}) \, dx$。 按照跟上面一模一样的套路，把 $\nabla$ 扔给 $v$：

$$\int_{\Omega} v \cdot \nabla (\ln \det \mathbb{F}) \, dx = - \int_{\Omega} \underbrace{(\nabla \cdot v)}_{=0} (\ln \det \mathbb{F}) \, dx = 0$$

**✅ 结论 2：第二半的积分也完美等于** $0$**。**

## 物理解释

在数学上费了这么大劲算出来全是 0，这其实印证了流体力学中“对流（Convection）”的本质：**随波逐流不消耗总能量。**

弹簧被水流裹挟着漂动（即 $(v \cdot \nabla)\mathbb{F}$），因为水池是不可压缩的且无泄漏，能量只是在水池内部搬了个家，它对整个水池的“总能量积分”没有任何增减贡献。物理常识与数学推导在此达成了极度完美的统一！
