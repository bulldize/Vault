
---
title: Giesekus模型PDE能量推导核心技巧
type: ai-assisted-learning-note
status: requires-manual-verification
tags: ["#Math", "#Giesekus模型", "#理论草稿", "#Status/逻辑断点"]
---

> [!warning] 逻辑断点待人工核查
> 行列式对数、测试函数和耦合项抵消的形式计算需要 $F$ 可逆、足够正则性及适当边界条件；不能直接当作弱解层面的严格证明。

> [!abstract]
> 拆解 Giesekus 能量推导中的测试函数、Jacobi 公式、耗散平方和动量/形变耦合项抵消。

# Giesekus 模型 PDE 能量推导核心技巧与公式总结

## 学习导航

- 阶段：4/9，能量机制拆解。
- 前置：[[20260719 - Math - Giesekus能量估计与耗散定律|能量估计与耗散定律]]。
- 后续：[[20260719 - Math - Giesekus对流项积分消去|对流项积分消去]]。
- 路线：[[10_Math_and_Theory/20260719 - Math - Giesekus与混合有限元学习路线|Giesekus 与混合有限元学习路线]]。

在非牛顿流体力学的 PDE 理论分析中，能量耗散律的形式推导依赖若干明确的代数恒等式、测试函数选择和边界项处理。以下整理五个关键结构。

## 1. 方程 1.1c 测试函数的真实来源（逆向工程）

在论文中，用来测试弹簧形变方程 (1.1c) 的测试函数是 $\mu(\mathbb{F} - \mathbb{F}^{-\top})$。这个函数绝不是数学家凭空猜出来的，而是**先确立目标能量，再求变分导数**“逆向定制”出来的专属钥匙。

- **目标弹性能量泛函**：高分子物理学家先给出了系统应该具有的弹性自由能密度：

    $$E(\mathbb{F}) = \frac{\mu}{2}\vert{}\mathbb{F}\vert{}^2 - \frac{\mu}{2}\ln \det(\mathbb{F}\mathbb{F}^\top)$$
- **求变分导数 (Gateaux Derivative)**：对这个能量泛函 $E(\mathbb{F})$ 关于形变张量 $\mathbb{F}$ 求导：

    $$\frac{\delta E}{\delta \mathbb{F}} = \mu(\mathbb{F} - \mathbb{F}^{-\top})$$
- **逻辑闭环**：因为测试函数是能量的导数，所以当它乘上方程里的时间导数 $\partial_t \mathbb{F}$ 并积分时，利用链式法则刚好能积出**总弹性能量随时间的变化率**。


## 2. 矩阵行列式对数的导数法则（雅可比公式）

推导对数惩罚项时，最核心的代数公式是**雅可比公式 (Jacobi's formula)**。它打通了张量微积分中“对数”、“行列式”与“矩阵双点积”的桥梁。

- **核心公式**：对于任意可逆矩阵 $A$，它的行列式的对数的微分为：

    $$d(\ln \det A) = A^{-\top} : dA$$
- **在推导中的应用**： 当处理测试函数的后半部分 $-\mathbb{F}^{-\top}$ 乘以时间导数 $\partial_t \mathbb{F}$ 时：

    $$-\mathbb{F}^{-\top} : \partial_t \mathbb{F} = - \partial_t (\ln \det \mathbb{F}) = - \frac{1}{2} \partial_t \ln \det (\mathbb{F}\mathbb{F}^\top)$$

    这完美凑出了能量等式中那个防止体积压缩到 $0$ 的“保命对数惩罚项”。


## 3. 张量双点积与矩阵迹 (Trace) 的转换关系

方程 1.1c 是张量（矩阵）方程，测试时使用的是**矩阵双点积 (**$:$**)**。将双点积转化为线性代数中最熟悉的“迹 ($\text{tr}$)”，是所有代数化简的基石。

- **核心转换关系**：两个矩阵 $A$ 和 $B$ 的双点积，等于它们相乘后的迹：

    $$A : B = \text{tr}(A B^\top) = \text{tr}(A^\top B)$$
- **常用性质**：

    - $A : A = \text{tr}(A A^\top) = \vert{}A\vert{}^2$ （矩阵所有元素的平方和，即 Frobenius 范数的平方）

    - $\mathbb{I} : \mathbb{I} = \text{tr}(\mathbb{I}) = d$ （$d$ 为空间维度，通常为 2 或 3）


## 4. 1.1a 和 1.1c 能量形式的物理归属

整个流体系统的总能量和总耗散，由动量方程 (1.1a) 和形变方程 (1.1c) **平分秋色**。它们各自管辖着不同的物理领域：

|方程来源|测试函数|贡献的能量项 (积分内)|贡献的耗散项 (积分内)|物理意义|
|---|---|---|---|---|
|**1.1a (动量方程)**|$v$ (速度向量，用**点乘** $\cdot$)|$\frac{\rho}{2}|v|^2$|
|**1.1c (形变方程)**|$\mu(\mathbb{F} - \mathbb{F}^{-\top})$ (张量，用**双点积** $:$)|$\frac{\mu}{2}|\mathbb{F}|^2 - \frac{\mu}{2}\ln \det(\mathbb{F}\mathbb{F}^\top)$|

## 5. 推导中的三个关键机制

### 机制 A: 对流项的消去

不管是速度的对流 $(v \cdot \nabla)v \cdot v$ 还是形变的对流 $(v \cdot \nabla)\mathbb{F} : \mu(\mathbb{F} - \mathbb{F}^{-\top})$，计算逻辑一致：

1. **链式法则**：将对流项化为标量的梯度，例如 $\frac{1}{2}v \cdot \nabla(\vert{}\mathbb{F}\vert{}^2)$ 和 $v \cdot \nabla(\ln \det \mathbb{F})$。

2. **分部积分 (扔** $\nabla$**)**：把梯度转移到前面的速度 $v$ 上，出现速度散度 $\nabla \cdot v$。

3. **不可压缩条件**：在边界项为零且 $\nabla \cdot v = \operatorname{div}(v) = 0$ 时，相关体积分为 $0$。


### 机制 B: 松弛项的平方耗散结构

如何证明非线性刹车项是一个纯耗散（永远大于0）？ 计算 $\frac{\mu^2}{2\lambda}(\mathbb{F}\mathbb{F}^\top\mathbb{F} - \mathbb{F}) : (\mathbb{F} - \mathbb{F}^{-\top})$。利用双点积转迹的公式将其展开为 4 项：

1. $(\mathbb{F}\mathbb{F}^\top\mathbb{F}) : \mathbb{F} = \text{tr}(\mathbb{F}\mathbb{F}^\top\mathbb{F}\mathbb{F}^\top) = \vert{}\mathbb{F}\mathbb{F}^\top\vert{}^2$

2. $-(\mathbb{F}\mathbb{F}^\top\mathbb{F}) : \mathbb{F}^{-\top} = -\text{tr}(\mathbb{F}\mathbb{F}^\top\mathbb{F}\mathbb{F}^{-1}) = -\text{tr}(\mathbb{F}\mathbb{F}^\top) = -\vert{}\mathbb{F}\vert{}^2$

3. $-\mathbb{F} : \mathbb{F} = -\vert{}\mathbb{F}\vert{}^2$

4. $(-\mathbb{F}) : (-\mathbb{F}^{-\top}) = \text{tr}(\mathbb{F}\mathbb{F}^{-1}) = \text{tr}(\mathbb{I}) = d$


四项相加：$\vert{}\mathbb{F}\mathbb{F}^\top\vert{}^2 - 2\vert{}\mathbb{F}\vert{}^2 + d$，这刚好是完全平方式 $\vert{}\mathbb{F}\mathbb{F}^\top - \mathbb{I}\vert{}^2$ 的展开！

### 机制 C: 动量与形变方程的耦合项抵消

水流克服弹力做功的能量去哪了？

- **1.1c 产生**：拉伸项 $(\nabla v)\mathbb{F}$ 乘以测试函数前半部分 $\mathbb{F}$，利用双点积转迹得出 $\int \mu(\nabla v) : (\mathbb{F}\mathbb{F}^\top)$。

- **1.1a 产生**：弹性应力项 $\text{div}(\mu\mathbb{F}\mathbb{F}^\top)$ 乘以测试函数 $v$，**利用分部积分**（将 $\text{div}$ 扔给 $v$ 变成 $\nabla v$）升维得出 $-\int \mu(\mathbb{F}\mathbb{F}^\top) : (\nabla v)$。


两者在相同正则性与边界前提下大小相等、符号相反，因而在总能量计算中抵消；系统总能量的变化仍需同时计入粘性与松弛耗散。
