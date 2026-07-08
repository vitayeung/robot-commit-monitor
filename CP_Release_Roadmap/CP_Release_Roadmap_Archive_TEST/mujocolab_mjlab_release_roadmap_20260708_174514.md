# mujocolab/mjlab Release Roadmap

- 仓库: `mujocolab/mjlab`
- 统计窗口: 最近一年
- 最新版本: v1.5.0 (2026-06-29 07:09:19 CST)
- 纳入统计的最早版本: v0.1.0 (2025-09-29 18:00:45 CST)
- 版本概况: 最近一年共 8 个版本，其中正式版 7 个、预发布版 1 个
- 详细证据索引: `mujocolab_mjlab_release_roadmap_reference.md`

## 核心判断

- mjlab 在过去一年从早期 beta 版本（v0.1.0）快速演进为稳定的生产级框架（v1.5.0），核心定位是轻量级、GPU 加速的机器人学习框架。框架采用 Isaac Lab 风格的 manager-based API，但依赖关系更简洁，单命令即可安装，且直接暴露 MuJoCo 原生数据结构。

- 产品能力在一年内实现了跨越式增长：从基础仿真环境起步，逐步覆盖 RGB-D 相机传感器、域随机化系统、程序化地形生成、多种执行器模型（PD、直流电机、肌肉）、异构世界网格变体、以及完整的训练/可视化/云部署工具链。每个版本都显著扩展了支持的用例范围。

- 框架的工程成熟度持续提升：依赖管理从需要固定 git 修订版和自定义索引，演进为完全通过 PyPI 安装；MuJoCo 和 mujoco-warp 版本从 3.7 持续升级到 3.10；文档系统从无到有，现已包含教程、API 参考和多版本支持。

- 社区生态正在形成：v1.4.0 和 v1.5.0 的发布说明中出现了多位首次贡献者和回归贡献者，研究页面列出了多个基于 mjlab 的衍生项目（如 Unitree 官方 RL 环境、PAL Robotics 机器人任务），表明框架正在被外部团队采用。

## 产品演进主线

- **从基础仿真到完整训练工具链**：v0.1.0 仅提供基础仿真能力，v1.1.0 引入 RGB-D 相机和 MetricsManager，v1.2.0 完成域随机化重设计和云训练支持，v1.3.0 增加 RecorderManager 和终止条件课程学习，v1.5.0 添加运动跟踪修复和峰值指标报告。每个版本都在填补训练工作流中的关键缺口。

- **执行器模型持续丰富，覆盖更多机器人类型**：从最初的简单位置/速度执行器，到 v1.3.0 的简化配置和 XML 自动检测，v1.4.0 的原生隐式 PD 执行器，再到 v1.5.0 的直流电机执行器（支持电压/位置/速度输入模式、反电动势、热模型、LuGre 摩擦等）。这使框架能够支持从简单关节到复杂电机驱动系统的各种机器人。

- **仿真真实感与可复现性持续提升**：域随机化从简单的 `randomize_field` 接口演进为 v1.2.0 的类型化、自动依赖更新的 dr 模块；地形生成在 v1.3.0 引入预设系统，v1.5.0 实现确定性课程难度和一致的色彩映射；v1.4.0 的异构世界网格变体允许不同并行世界使用不同网格资产，大幅提升训练多样性。

- **开发者体验与调试能力系统化改进**：v1.2.0 重写查看器时序模型并增加单步模式、错误恢复、力箭头可视化；v1.3.0 的查看器新增奖励条面板、W&B 运行浏览、检查点热切换；v1.4.0 的 Manager 形状验证在计算时检查张量形状；v1.5.0 修复了无头 Linux 主机的视频录制崩溃和 GPU 选择问题。

## 版本演进解读

### v1.5.0（2026-06-29）

- 将 MuJoCo 和 mujoco-warp 升级到 3.10，并完全通过 PyPI 固定依赖，消除了之前夜间构建轮子被垃圾回收导致的依赖解析失败问题。`SimulationCfg.ls_parallel` 被弃用并忽略。

- 新增 `BuiltinDcMotorActuator`，封装 MuJoCo 原生 `<dcmotor>`，支持电压/位置/速度输入模式、反电动势、可选的积分、电感、LuGre 摩擦和齿槽效应扩展。这为需要精确电机建模的 sim-to-real 场景提供了原生支持。

- 地形生成实现确定性课程难度，高度场使用固定发散调色板按绝对高度着色，解决了低振幅噪声渲染为高对比度杂色的问题。`HfRandomUniformTerrainCfg` 新增 `scale_with_difficulty` 支持课程训练。

- 运动跟踪修复了中期重采样后锚定到过时机器人姿态的长期错误，`MotionCommand` 现在在计算相对身体姿态前刷新仿真状态。`MetricsTermCfg` 新增 `reduce="max"` 用于报告峰值指标。

### v1.4.0（2026-05-27）

- 引入异构世界网格变体（`VariantEntityCfg`），允许不同并行世界为同一逻辑实体使用不同网格资产（如立方体、球体、圆锥）。变体必须具有相同的运动学结构，但网格几何体可以不同。域随机化、查看器和离屏渲染器自动使用分配的变体。这是实现大规模多样化训练的关键能力。

- 新增 `BuiltinPdActuator`，作为原生 MuJoCo PD 控制执行器，同时支持位置和速度目标。与之前需要 Python 计算扭矩的 `IdealPdActuator` 相比，它利用隐式积分提供更好的稳定性。`effort_limit` 通过 `jnt_actfrcrange` 或 `tendon_actfrcrange` 强制执行。

- 新增 `mdp.projected_gravity_from_sensor` 观测项，从 IMU 站点的 `framezaxis` 传感器读取重力方向，反映 IMU 安装随机化（如 `dr.site_quat`）的影响。Go1 和 G1 机器人现已包含 `imu_upvector` 传感器。

- `RewardManager`、`TerminationManager` 和 `MetricsManager` 现在在计算时验证项的输出形状，每个项必须返回 `(num_envs,)` 形状的张量，否则会抛出命名违规项的 `ValueError`。这显著提升了调试效率。

- 破坏性变更：移除 `MujocoCfg.enableflags` 中的 `"multiccd"`；`CameraSensorData.segmentation` 从 `[B, H, W]` 几何体 ID 改为 `[B, H, W, 2]` 类型化 `(object_id, object_type)` 对。

### v1.3.0（2026-04-15）

- 查看器基于独立的 [mjviser](https://github.com/mujocolab/mjviser) 包重建，新增可视化选项卡（覆盖层控制）、分组选项卡（几何体和站点可见性）、奖励条面板、W&B 运行浏览、检查点热切换和运动参考进度条。查看器架构的解耦使 mjlab 和 mjviser 可以独立演进。

- 地形系统改为预设驱动，新增 `@terrain_preset` 装饰器用于组合可复用配置。课程模式现在每列分配一种地形类型，`proportion` 控制机器人分布而非列数。`STAIRS_TERRAINS_CFG` 预设提供开箱即用的渐进式楼梯课程。

- 执行器配置大幅简化：延迟配置现在内联在任何 `ActuatorCfg` 子类上，`DelayedActuator` 等类被移除；四个 XML 执行器配置类合并为单个 `XmlActuatorCfg`，自动从 XML 检测执行器类型。新增 `viscous_damping` 用于被动速度比例阻尼。

- 新增 `RecorderManager` 用于记录 rollout 期间的观测、动作或任意环境数据；`termination_curriculum` 支持在训练期间调度终止条件参数变化；`RelativeJointPositionAction` 实现相对于当前配置的关节位置控制。

- 新增完整的 cartpole 教程，从零开始构建环境，涵盖场景设置、动作和观测项、奖励、终止条件和训练。这降低了新用户的入门门槛。

### v1.2.0（2026-03-07）

- 域随机化模块完全重设计：用类型化、逐字段的随机化函数（如 `dr.geom_friction`、`dr.body_mass`）替代了之前的 `randomize_field` 接口。这些函数在修改参数时自动重新计算依赖的物理量（如修改质量时更新惯性），消除了手动 `set_const` 调用的需要和不一致物理状态的风险。

- 查看器时序模型重写：单个仿真预算累加器配合墙钟截止时间，确保物理和渲染在任何速度倍率下保持同步。新增单步模式、错误恢复（暂停并记录堆栈跟踪而非崩溃）、力箭头可视化和实时因子显示。

- 新增 `"step"` 事件模式，每个环境步骤触发而非仅在重置时触发。结合 `apply_body_impulse` 可在训练期间向机器人施加外部力，支持可配置的持续时间、大小和作用点。

- 集成 SkyPilot 实现云 GPU 训练，单命令即可在 Lambda Cloud 上训练。文档涵盖设置、监控和成本管理。W&B 扫描脚本支持跨多 GPU 实例分配代理。

- 破坏性变更：`randomize_field` 被移除；`EventTermCfg` 不再接受 `domain_randomization`；`RslRlModelCfg` 使用 `distribution_cfg` 字典替代 `stochastic`/`init_noise_std`/`noise_std_type`。

### v1.1.1（2026-02-15）

- 新增差分逆运动学（differential IK）动作空间，为需要末端执行器控制的机器人任务提供新的控制方式。视频录制从 `moviepy` 切换到 `mediapy`。

- 原生查看器新增奖励图可视化，Viser 查看器扩展为可绘制指标。修复了 Viser 深度图像显示问题。

### v1.1.0（2026-02-13）

- mjlab 及其所有依赖（包括 mujoco-warp）现在可直接从 PyPI 安装，不再需要固定特定 mujoco-warp 修订版或自定义索引。安装简化为 `pip install mjlab`。

- 新增 RGB 和深度相机传感器，使用 BVH 加速的光线投射。新增 MetricsManager 用于在训练期间记录自定义指标。新增地形可视化工具和多种新地形类型。

- rsl-rl-lib 升级到 4.0.0，支持原生 ONNX 导出。

### v1.0.0（2026-01-29）

- mjlab 正式发布稳定版。新增 RayCastSensor（地形和障碍物检测）、ContactSensor 历史跟踪、肌肉执行器支持（生物力学仿真）、传感器缓存（大规模训练性能优化）和改进的 NaN 处理。

- 新增创建新任务的 Jupyter notebook 教程和基准测试报告生成脚本。

### v0.1.0（2025-09-29）

- mjlab 首次公开发布，在 GitHub 和 PyPI 上可用。这是一个早期 beta 版本，API 可能随社区反馈演进。提供 Unitree G1 人形机器人的预训练运动模仿策略演示。

## 采用与规划提示

- **当前版本（v1.5.0）已具备生产级能力**，适合开始构建基于 GPU 加速的机器人学习工作流。框架覆盖了从场景定义、域随机化、地形课程到训练、可视化、云部署的完整链路。建议新项目直接基于 v1.5.0 开始，避免从旧版本迁移的成本。

- **迁移成本需要评估**：v1.2.0 到 v1.5.0 之间存在多次破坏性变更。如果从 v1.1.x 或更早版本升级，需要重写域随机化代码（`randomize_field` 被移除）、执行器配置（`DelayedActuator` 等被移除）、以及 XML 执行器配置类（合并为 `XmlActuatorCfg`）。v1.4.0 的 segmentation 数据格式变更也需要适配。

- **目标用户群体明确**：需要 GPU 加速机器人训练的研究团队和工程团队，特别是从事 sim-to-real 迁移学习、运动模仿、多机器人策略训练的团队。框架对 macOS 仅支持评估，训练需要 NVIDIA GPU（推荐 RTX 40 系列或 L40s/H100，CUDA 12.4+）。

- **生态发展值得关注**：研究页面列出了多个基于 mjlab 的衍生项目（Unitree 官方 RL 环境、PAL Robotics 机器人任务、LEAP Hand 灵巧操作等），表明框架正在被外部团队采用。v1.5.0 的 changelog 中提到了 `rsl-rl-lib` 升级到 5.4.0，建议关注上游 RL 库的演进方向。