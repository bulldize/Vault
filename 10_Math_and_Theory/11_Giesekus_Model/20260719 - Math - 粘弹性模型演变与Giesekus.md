---
title: 粘弹性流体模型演变
type: ai-assisted-learning-note
status: requires-manual-verification
tags: ["#Math", "#Giesekus模型", "#理论草稿", "#Status/逻辑断点"]
---

> [!warning] 逻辑断点待人工核查
> 模型变量、参数符号、构成关系与边界条件必须以当前 Giesekus 原文为准，不能由本笔记的物理比喻替代。

> [!abstract]
> 从不可压 Navier-Stokes、Oldroyd-B 到 Giesekus 的概念性阅读笔记，用于建立模型演变与额外应力的直观联系。

# 粘弹性流体模型演变：从纯水到 Giesekus 模型

## 学习导航

- 阶段：1/9，连续模型背景。
- 后续：[[12_Functional_Analysis/20260719 - Math - 弱解速度场函数空间|弱解速度场函数空间]]。
- 路线：[[10_Math_and_Theory/20260719 - Math - Giesekus与混合有限元学习路线|Giesekus 与混合有限元学习路线]]。

在非牛顿流体力学中，为了准确描述高分子聚合物流体（如塑料熔体、洗发水、面团等）复杂的“既像水又像弹簧”的性质，科学家们对流体方程进行了逐步的升级。

以下是流体模型演化的三个核心阶段对比：

## 1. Navier-Stokes 方程

**物理图像**：流体由微小的“玻璃球”组成，微团之间只有简单的滑动摩擦（粘性），没有记忆，也没有弹性。推一下流一下，不推就慢慢停下。

**核心方程**：

1. **不可压缩条件 (质量守恒)**：

    $$\text{div}(v) = 0$$

    _(表示流体体积绝对不变，因此方程中没有任何与体积膨胀/压缩相关的受力项)_

2. **动量方程 (牛顿第二定律)**：

    $$\rho(\partial_t v + v \cdot \nabla v) = -\nabla p + \nu \Delta v$$
    - $\rho(\partial_t v + v \cdot \nabla v)$：流体的加速度（惯性项）

    - $-\nabla p$：压力梯度（驱使流体从高压流向低压）

    - $\nu \Delta v$：普通的粘性摩擦力（牛顿粘性）


## 2. Oldroyd-B 模型

**物理图像**：在水里加入了长链聚合物。我们可以把它想象成水里悬浮着无数根**理想的线性弹簧**。

**数学上的改变**：

1. **动量方程多了一个力（弹性应力）**：

    $$\rho(\partial_t v + v \cdot \nabla v) = -\nabla p + \nu \Delta v + \color{red}{\text{div}(\mu \mathbb{B})}$$
    - 新增的 $\text{div}(\mu \mathbb{B})$ 代表聚合物弹簧被拉伸后，反作用于水流的力。$\mathbb{B}$ 称为**构型张量**，记录了弹簧的拉伸和扭曲状态。

2. **多了一个“弹簧演化方程”**：

    $$\partial_t \mathbb{B} + (v \cdot \nabla)\mathbb{B} = (\nabla v)\mathbb{B} + \mathbb{B}(\nabla v)^\top \color{blue}{- \frac{\mu}{\lambda}(\mathbb{B} - \mathbb{I})}$$
    - **等式左边**：弹簧顺着水流移动。

    - **等式右边前两项**：水流的速度梯度在拉伸和旋转弹簧。

    - **蓝色线性弛豫项**：$\mathbb{I}$ 是弹簧放松时的原状。这个项表示弹簧试图以正比例的力缩回原状（遵循胡克定律）。


**⛔ 致命缺陷**： 如果水流拉伸速度过快，这个线性的回缩力会“拉不住”。在数学上，弹簧会被拉伸到**无限长**（$\mathbb{B} \to \infty$），导致物理失真和数值计算崩溃。

## 3. Giesekus 模型

**物理图像**：真实的聚合物链在拥挤的流体中不仅会被拉伸，相互之间还会发生强烈的摩擦和纠缠（各向异性阻力）。

**数学上的改变**： Giesekus 保留了 Oldroyd-B 的所有结构，**唯独修改了演化方程末尾的弛豫项，加入了一个“二次非线性项”**。

传统 Giesekus 演化方程（基于构型张量 $\mathbb{B}$）：

$$\partial_t \mathbb{B} + (v \cdot \nabla)\mathbb{B} = (\nabla v)\mathbb{B} + \mathbb{B}(\nabla v)^\top \color{red}{- \frac{\mu}{\lambda}(\mathbb{B}^2 - \mathbb{B})}$$

**本论文采用的替代形式（基于变形梯度** $\mathbb{F}$**，其中** $\mathbb{B} = \mathbb{F}\mathbb{F}^\top$**）**：

$$\partial_t\mathbb{F} + (v\cdot\nabla)\mathbb{F} = (\nabla v)\mathbb{F} \color{red}{- \frac{\mu}{2\lambda}(\mathbb{F}\mathbb{F}^\top\mathbb{F} - \mathbb{F})}$$

**✨ 二次项** $\mathbb{B}^2$ **(或** $\mathbb{F}\mathbb{F}^\top\mathbb{F}$**) 的作用：超级刹车系统**

- 当拉伸很小时，模型表现得像 Oldroyd-B。

- 当拉伸极大时，平方项会以几何级数爆炸式增长，产生巨大的阻力，**强制限制弹簧的无限拉伸**。


**🔥 数学与计算的代价**： 这个平方项在物理上非常完美，但在数学求解时是极度危险的。在**高 Weissenberg 数**（高弹性、大形变）情况下，这个高度非线性的项极易引起数值剧烈震荡。

> _这篇论文的核心成就，就是设计了一种算法并严格证明：即便存在这个讨厌的非线性项和高弹性，他们的计算方法依然能稳定收敛，绝对不会崩溃。_

## 4. 不可压缩约束 $\operatorname{div}(v) = 0$

- **物理上的简化**：因为聚合物流体（液体）难以压缩，体积不变。所以动量方程中不需要写出与体积膨胀/压缩摩擦相关的复杂应力项（如 $\lambda (\text{div} v)\mathbb{I}$）。

- **计算上的噩梦**：$\text{div}(v) = 0$ 成为了一个每时每刻必须死死卡住的**绝对约束条件**。在有限元计算中，压力 $p$ 其实不是一个独立的物理变量，而是一个数学上的“拉格朗日乘子”，专门用来惩罚速度场，迫使它满足不可压缩条件。为了处理这个约束，本文作者不得不使用了特殊的**泰勒-胡德混合有限元 (Taylor-Hood element)** 并在理论证明中耗费大量篇幅重构局部压力。
