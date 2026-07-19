---
title: 麻醉TCI能力地图
date: 2026-07-19
type: capability-map
status: maintained
last_verified: 2026-07-19
tags:
  - "#Anesthesia"
  - "#PK_PD建模"
  - "#PINNs"
  - "#Status/已提炼"
---

# 麻醉 TCI 能力地图

> [!abstract]
> 麻醉方向聚焦药代/药效模型、TCI 离线仿真回放、影子自适应评估和 PINN 代理建模。所有内容限于研究与仿真语境，不生成真实硬件控制、剂量策略或临床建议。

## 方法与模型

- **PK/PD 建模**：丙泊酚与顺阿曲库铵的多房室模型、效应室模型、参数辨识和个体差异建模。
- **TCI 仿真**：目标浓度输注系统的离线回放、模型对比、输出记录和实验复核。
- **PINN 研究**：将房室动力学约束、观测数据与神经网络代理模型结合，评估模型拟合与泛化。
- **影子评估**：以离线、非干预方式比较候选方法，明确不进入真实患者或硬件闭环。

## 项目入口

- [[31_PK_PD_Modeling/31_PK_PD_Modeling|PK/PD 建模]]
- [[32_PINN_Research/32_PINN_Research|PINN 研究]]
- [[33_Simulation_Evaluation/33_Simulation_Evaluation|仿真与影子评估]]

## 维护规则

- PK/PD 参数、模型有效性和临床相关结论必须回链原始文献或复现实验，不在本页作最终断言。
- 离线仿真需记录模型版本、输入数据边界、评价指标和随机性控制方式。
- 任何涉及真实控制或临床给药的材料只保留风险标注和待确认建议。

## 项目源路径

- `/Users/bulldize/Desktop/华西麻醉_TCI/01_References/参考文献`
- `/Users/bulldize/Desktop/华西麻醉_TCI/02_Training_and_Simulation/TCI练习`
- `/Users/bulldize/Desktop/华西麻醉_TCI/03_Applications/tci-web`
- `/Users/bulldize/Desktop/华西麻醉_TCI/README_项目台账.md`
