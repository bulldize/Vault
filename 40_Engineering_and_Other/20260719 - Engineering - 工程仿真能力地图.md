---
title: 工程仿真能力地图
date: 2026-07-19
type: capability-map
status: maintained
last_verified: 2026-07-19
tags:
  - "#Engineering"
  - "#Simulink"
  - "#PID控制"
  - "#Status/已提炼"
---

# 工程仿真能力地图

> [!abstract]
> 工程方向覆盖核动力系统数值仿真与 PID 控制复现，以及 RCR 网络和 ADAS 架构调研。核工程知识仅记录 MATLAB/Simulink 数值模型与 PID 逻辑，强化学习材料保持隔离。

## 方法与项目经验

- **核工程仿真**：稳压器及相关系统的 MATLAB/Simulink 建模、数值求解器选择、参数扫描、仿真结果复盘与 PID 控制调试。
- **控制分析**：以模型假设、输入边界、参数版本和评价输出为单位记录模拟实验，避免将调试参数提升为最终控制结论。
- **自动驾驶调研**：RCR 网络、ADAS 系统架构、数据集、评价指标与复现路径的技术梳理。

## 项目入口

- [[41_Nuclear_Simulation/41_Nuclear_Simulation|核工程仿真]]
- [[42_Auto_Driving/42_Auto_Driving|自动驾驶]]
- [[43_Agent_and_Infra/43_Agent_and_Infra|代理与基础设施]]

## 维护规则

- Simulink 模型变更、求解器和 PID 参数调整必须保留版本与实验上下文。
- 不建立核工程与强化学习相关的关联笔记；相关材料仅作为隔离源处理。
- 工程结论应由可复现实验输出支持，不以会议材料或单次图表替代验证。

## 项目源路径

- `/Users/bulldize/Desktop/核反应堆控制项目/simulink复现`
- `/Users/bulldize/Desktop/核反应堆回环检测`
