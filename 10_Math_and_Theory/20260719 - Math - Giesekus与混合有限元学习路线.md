---
title: Giesekus与混合有限元学习路线
date: 2026-07-19
type: learning-roadmap
status: requires-manual-verification
tags:
  - "#Math"
  - "#Giesekus模型"
  - "#有限元_FEM"
  - "#Status/逻辑断点"
---

# Giesekus 与混合有限元学习路线

> [!warning] 逻辑断点待人工核查
> 下列笔记来自 AI 辅助学习。它们可作为阅读导航，但不能替代原论文的假设、弱解定义、离散空间和完整证明。

> [!abstract]
> 本路线将 Inbox 内的数学笔记排列为连续模型、能量结构、弱形式和混合有限元离散两条链。所有笔记暂保留 Inbox，待逐条核对原文后再决定是否迁入正式理论目录。

## 阅读顺序

| 阶段 | 笔记 | 目标 |
| --- | --- | --- |
| 1. 模型背景 | [[11_Giesekus_Model/20260719 - Math - 粘弹性模型演变与Giesekus|粘弹性模型演变]] | 建立 Navier-Stokes、Oldroyd-B 与 Giesekus 的建模关系。 |
| 2. 弱解空间 | [[12_Functional_Analysis/20260719 - Math - 弱解速度场函数空间|弱解速度场函数空间]] | 明确速度空间、无散约束、边界条件与时间正则性。 |
| 3. 能量恒等式 | [[11_Giesekus_Model/20260719 - Math - Giesekus能量估计与耗散定律|能量估计与耗散定律]] | 对照原文确认总能量和耗散项。 |
| 4. 能量机制 | [[11_Giesekus_Model/20260719 - Math - Giesekus能量推导关键结构|能量推导关键结构]] | 分解测试函数、行列式对数和耦合项抵消。 |
| 5. 对流项 | [[11_Giesekus_Model/20260719 - Math - Giesekus对流项积分消去|对流项积分消去]] | 单独核对对流项消失的正则性与边界前提。 |
| 6. 无量纲与弱形式 | [[11_Giesekus_Model/20260719 - Math - Giesekus无量纲化与弱解定义|无量纲化与弱解定义]] | 连接模型参数、弱解定义和后续离散化。 |
| 7. 混合问题基础 | [[13_Finite_Element_Method/20260719 - Math - 混合有限元理论基础|混合有限元理论基础]] | 从泊松问题进入 Stokes 鞍点结构。 |
| 8. 离散稳定性 | [[13_Finite_Element_Method/20260719 - Math - Taylor-Hood元与Inf-Sup条件|Taylor-Hood 元与 inf-sup 条件]] | 核对连续/离散 inf-sup 条件与网格假设。 |
| 9. 论文离散设置 | [[13_Finite_Element_Method/20260719 - Math - Giesekus论文Taylor-Hood离散设置|论文 Taylor-Hood 设置]] | 对照论文的实际速度、压力和形变梯度离散空间。 |

## 核查主线

1. 连续模型：$Omega$ 的正则性、$v$ 的边界条件、$operatorname{div} v=0$、$det F>0$ 和所需光滑性。
2. 能量链：测试函数是否可作为允许测试函数、分部积分是否成立、耦合项符号和耗散平方恒等式。
3. 弱解链：Bochner 空间、时间导数空间、初值意义和弱形式测试函数。
4. 离散链：速度/压力对、协调网格、离散 inf-sup 常数、压力归一化和张量变量离散。

## 资料入口

- 当前方向原文：`/Users/bulldize/Desktop/有限元方法/02_Research_Direction/方向/2026-Convergent numerical schemes for the viscoelastic Giesekus model in two dimensions-arXiv.pdf`
- 原始资料台账：`/Users/bulldize/Desktop/有限元方法/README_资料台账.md`
- 正式能力入口：[[10_Math_and_Theory/20260719 - Math - 数学与数值分析能力地图|数学与数值分析能力地图]]
