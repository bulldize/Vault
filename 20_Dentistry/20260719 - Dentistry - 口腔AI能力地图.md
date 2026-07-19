---
title: 口腔AI能力地图
date: 2026-07-19
type: capability-map
status: maintained
last_verified: 2026-07-19
tags:
  - "#Dentistry"
  - "#CBCT分割"
  - "#IOS处理"
  - "#Status/已提炼"
---

# 口腔 AI 能力地图

> [!abstract]
> 口腔 AI 工作覆盖 CBCT/IOS 数据处理、牙齿分割、CEJ/ABC 曲线提取与牙科生物力学有限元分析。医学影像、标注与患者相关数据继续留在原项目中，本页不保存其副本。

## 方法与工具

- **CBCT 分割**：三维体素数据预处理、掩膜表示、分割网络、评价指标与实验复核。
- **IOS 处理**：点云和三角网格的清洗、牙齿实例分割、标注格式和后处理。
- **几何特征提取**：CEJ 与 ABC 曲线的无监督几何提取、曲线平滑、拓扑约束、可视化与误差分析。
- **牙科生物力学**：正畸相关基础、材料参数、网格、载荷和边界条件下的有限元分析。
- **工程工具**：Python、PyTorch、MONAI 及医学影像/几何数据处理工具链。

## CEJ 与 PDL 曲线

- CEJ 项目分别维护 CEJ 曲线与 PDL 曲线两条目标线，避免将两者的解剖定义和评价指标混合。
- 当前 PDL 曲线提取路线可用，见 [[24_Curve_Extraction/20260719 - Dentistry - PDL曲线提取技术路线|PDL 曲线提取技术路线]]；CEJ 曲线的具体路线另行沉淀。

## IOS 方法学习状态

- **已学习的主方法线**：蒋福林博士论文归档中的两阶段 IOS 实例分割，涵盖统一方向 3D-to-2D 特征表示、牙齿候选区定位与编号、单牙局部分割、图卷积、扩散和注意力机制。
- **初步了解的基准参考**：`3DTeethSeg'22` 的冠军方法仅作概览性学习，用于理解 IOS 牙齿定位、实例分割、FDI 编号和公开评测语境；不标注为已掌握或已复现。
- **当前工程主线**：Seg22Based 的 FPS + BDL 已可用，并围绕 ROI 和 PointNet++ 的单牙分割与 FDI 识别继续调试；网络与冠军方案的具体方法学细节尚待系统阅读。见 [[23_IOS_Segmentation/20260719 - Dentistry - IOS分割当前技术路线|IOS 分割当前技术路线]]。
- 资料身份、相对路径与 SHA-256 在原项目台账中维护：`/Users/bulldize/Desktop/口腔IOS分割/README_资料台账.md`。

## 项目入口

- [[22_CBCT_Segmentation/22_CBCT_Segmentation|CBCT 分割]]
- [[23_IOS_Segmentation/23_IOS_Segmentation|IOS 分割]]
- [[24_Curve_Extraction/24_Curve_Extraction|CEJ/ABC 曲线提取]]
- [[25_Dental_Biomechanics/25_Dental_Biomechanics|牙科生物力学]]

## 维护规则

- 将数据处理流程、模型版本、评价协议和结果分别记录，避免由单次实验推导临床结论。
- 含未脱敏医学数据、患者资料或来源不明影像的内容不迁入正式目录。
- 新论文的创新点、损失函数和网络改动先进入精读笔记，再回链至本页。

## 项目源路径

- `/Users/bulldize/Desktop/华西口腔_CEJ_ABC`
- `/Users/bulldize/Desktop/口腔IOS分割/01_Core_Methods/01_JiangFulin_IOS_Instance_Segmentation`
- `/Users/bulldize/Desktop/口腔IOS分割/01_Core_Methods/02_Segment_pretrain_3DTeethSeg22`
- `/Users/bulldize/Desktop/口腔IOS分割/README_资料台账.md`
