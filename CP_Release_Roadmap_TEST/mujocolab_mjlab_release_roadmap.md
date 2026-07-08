# mujocolab/mjlab Release Roadmap

- 仓库: `mujocolab/mjlab`
- 统计窗口: 最近一年
- 最新版本: v1.5.0 (2026-06-29 07:09:19 CST)
- 纳入统计的最早版本: v0.1.0 (2025-09-29 18:00:45 CST)
- 版本概况: 最近一年共 8 个版本，其中正式版 7 个、预发布版 1 个
- 详细证据索引: `mujocolab_mjlab_release_roadmap_reference.md`

## 核心判断

- mjlab 在过去一年从 beta 版本（v0.1.0）快速演进为稳定的生产级框架（v1.5.0），核心定位是轻量级、GPU 加速的机器人学习框架。框架采用 Isaac Lab 风格的 manager-based API，但依赖关系更简洁，单命令即可安装，启动开销低。

- 产品能力从基础仿真环境搭建扩展到完整的训练工作流支持，包括域随机化、地形生成、多类型执行器、RGB-D 相机传感器、云端训练和 ONNX 导出。v1.5.0 已支持 MuJoCo 3.10 和 MuJoCo Warp 3.10，依赖管理从自定义索引迁移到 PyPI 固定版本，大幅降低安装断裂风险。

- 框架的生态系统正在形成，v1.5.0 的文档中列出了多个外部项目（Unitree、PAL Robotics、LEAP Hand 等）基于 mjlab 构建的机器人环境和任务。这表明 mjlab 正在从单一项目向社区驱动的平台演进。

- 迁移成本在多个版本中持续存在，尤其是 v1.2.0 的域随机化 API 重写和 v1.3.0 的执行器配置简化。v1.4.0 和 v1.5.0 的破坏性变更较少，API 趋于稳定，适合新用户采用。

## 产品演进主线

- **从 beta 到稳定版的成熟度提升**：v0.1.0（2025年9月）作为早期 beta 发布，仅提供基础仿真能力。v1.0.0（2026年1月）宣布稳定，增加了 RayCastSensor、接触传感器历史追踪、肌肉执行器和 NaN 检测。v1.1.0 实现 PyPI 直接安装，移除了自定义索引依赖，大幅降低用户入门门槛。

- **域随机化从手动配置到类型安全的重构**：v1.2.0 用类型化的逐字段随机化函数（如 `dr.geom_friction`、`dr.body_mass`）替换了旧的 `randomize_field` 接口。新设计自动更新依赖的物理量（如质量变化时更新惯性），减少了不一致物理状态的风险。v1.5.0 进一步增加了材质相关的随机化函数（`dr.mat_emission`、`dr.mat_specular` 等）。

- **执行器体系从单一类型到多样化原生支持**：早期版本仅支持基础的位置/速度执行器。v1.3.0 简化了执行器配置，移除了 `DelayedActuator` 包装器，将延迟直接集成到配置中。v1.4.0 增加了 `BuiltinPdActuator`（原生 PD 控制，比 Python 实现的 `IdealPdActuator` 更稳定）。v1.5.0 增加了 `BuiltinDcMotorActuator`，支持电压/位置/速度输入模式、反电动势、热模型和 LuGre 摩擦等高级特性。

- **地形系统从基础生成到预设化课程体系**：v1.3.0 引入了 `@terrain_preset` 装饰器和预设配置（如 `STAIRS_TERRAINS_CFG`），使地形课程可组合和复用。v1.5.0 修复了地形生成的确定性问题，确保课程难度在行间可复现，并修复了多个边界情况（空边框、NaN 颜色、编译失败）。

## 版本演进解读

### v1.5.0（2026-06-29）

- 将 MuJoCo 和 MuJoCo Warp 升级到 3.10，依赖从自定义索引迁移到 PyPI 固定版本。这消除了夜间构建轮子被垃圾回收导致的依赖解析失败问题，安装更可靠。
- 新增 `BuiltinDcMotorActuator`，原生支持直流电机模型，包含电压/位置/速度输入模式、反电动势、热模型、LuGre 摩擦和齿槽效应。这对需要精确电机建模的 sim-to-real 场景（如四足机器人、机械臂）价值显著。
- 地形生成现在在课程模式下具有确定性的行间难度，高度场使用固定发散调色板按绝对高度着色。低振幅噪声不再渲染为高对比度杂乱，场景视觉一致性提升。
- 修复了运动跟踪中 mid-episode 重采样后锚定到过时机器人位姿的长期 bug。`MotionCommand` 现在在计算相对体位姿前刷新仿真状态。
- 域随机化中针对同一模型字段不同轴的事件现在正确组合而非静默覆盖。`MetricsTermCfg` 新增 `reduce="max"` 用于报告回合峰值（如峰值功率或接触力）。

### v1.4.0（2026-05-27）

- 引入每世界网格变体（`VariantEntityCfg`），允许在批量仿真中为同一逻辑实体使用不同网格资产。例如，世界 0 使用立方体，世界 1 使用球体，世界 2 使用碗。变体必须具有相同的运动学结构（相同的体、关节和关节类型），但网格几何体可以不同。域随机化、原生查看器和 Viser 查看器自动使用分配的变体。
- 新增 `BuiltinPdActuator`，作为原生 MuJoCo PD 控制实现，支持位置和速度目标。与 `IdealPdActuator`（在 Python 中计算扭矩并通过 `<motor>` 应用）相比，`BuiltinPdActuator` 利用隐式积分，稳定性更高。`dr.pd_gains` 和 `dr.effort_limits` 均支持新执行器。
- 新增 `mdp.projected_gravity_from_sensor` 观测，从 IMU 站点的 `framezaxis` 传感器读取重力方向。当 IMU 站点应用了 `dr.site_quat` 随机化时，该观测能正确反映重力方向的变化。Go1 和 G1 机器人已包含 `imu_upvector` 传感器。
- `RewardManager`、`TerminationManager` 和 `MetricsManager` 现在在计算时验证项的输出形状。每个项必须返回形状为 `(num_envs,)` 的张量，否则会引发 `ValueError` 并指明违规项，避免静默广播或训练时失败。
- 破坏性变更：从 `MujocoCfg.enableflags` 中移除 `"multiccd"`（上游已默认启用）。`CameraSensorData.segmentation` 从 `[B, H, W]` 几何体 ID 更改为 `[B, H, W, 2]` 类型化 `(object_id, object_type)` 对。

### v1.3.0（2026-04-15）

- Viser 查看器内部重构，基于独立的 `mjviser` 包重建。场景创建、网格转换和叠加渲染（接触、力、惯性、肌腱、关节、框架）移至 `mjviser`，mjlab 保留调试可视化和 Warp 张量转换。新增可视化选项卡（叠加控制）、分组选项卡（几何体和站点可见性）、奖励条面板、W&B 运行浏览、检查点热切换和运动参考进度条。
- 地形系统迁移到预设化配置，新增 `@terrain_preset` 装饰器用于组合可复用配置。课程模式现在每列分配一种地形类型，`proportion` 控制机器人分布而非列数。`STAIRS_TERRAINS_CFG` 预设提供渐进式楼梯课程。新增 `TerrainHeightSensor`（`RayCastSensor` 子类）计算每帧垂直间隙，替换了在粗糙地形上不正确的世界 Z 代理。
- 执行器配置简化：`DelayedActuator`、`DelayedActuatorCfg` 和 `DelayedBuiltinActuatorGroup` 被移除。延迟现在直接在任何 `ActuatorCfg` 子类上配置。四个 XML 执行器配置类合并为单个 `XmlActuatorCfg`，自动从 XML 检测执行器类型。新增 `viscous_damping` 用于被动速度比例阻尼。
- 新增 `RecorderManager` 用于记录 rollout 期间的观测、动作或任意环境数据。`termination_curriculum` 支持在训练期间调度终止项参数变化。`RelativeJointPositionAction` 提供相对于当前配置的关节位置控制。新增 cartpole 教程，从零开始构建环境。
- 破坏性变更：`DelayedActuator` 系列移除，`delay_target` 移除，`Xml*ActuatorCfg` 合并，`TerrainImporter` 别名移除，`EntityData.generalized_force` 移除，`ActuatorCfg.armature` 和 `.frictionloss` 默认值从 `0.0` 改为 `None`。

### v1.2.0（2026-03-07）

- 域随机化完全重写：用类型化的逐字段随机化函数（`dr.geom_friction`、`dr.body_mass`、`dr.mat_rgba` 等）替换旧的 `randomize_field` 接口。新设计自动更新依赖的物理量（如质量变化时更新惯性），减少不一致物理状态的风险。自定义操作和分布是一等公民，原生查看器在每次重置时同步所有随机化字段。
- 查看器时间模型重写：单个仿真预算累加器配合墙钟截止时间，在任何速度倍率（1/32x 到 8x）下保持物理和渲染同步。新增单步模式、错误恢复（暂停并记录回溯而非崩溃）、力箭头可视化和实时因子显示。Viser 查看器新增速度摇杆、改进的项绘图器和重新组织的控制面板。
- 新增 `"step"` 事件模式，在每个环境步触发（不仅限于重置）。结合 `apply_body_impulse` 可在训练期间向机器人施加外部力，支持可配置的持续时间、大小和作用点。
- 新增 SkyPilot 集成，支持单命令在云端 GPU（Lambda Cloud）训练。文档涵盖设置、监控和成本管理。W&B 扫描脚本支持在多 GPU 实例上每 GPU 分配一个代理。
- 破坏性变更：`randomize_field` 移除，`EventTermCfg` 不再接受 `domain_randomization`，`RslRlModelCfg` 使用 `distribution_cfg` 字典替代 `stochastic`/`init_noise_std`/`noise_std_type`（现有检查点自动迁移）。

### v1.1.1（2026-02-15）

- 新增差分 IK 动作空间，支持基于逆运动学的末端执行器控制。这对操作任务（如抓取、操控）特别有用，用户可以直接指定末端执行器位姿而非关节角度。
- 原生查看器新增奖励图可视化，Viser 查看器扩展支持指标绘图。视频录制从 `moviepy` 切换到 `mediapy`。
- 这是一个小补丁版本，主要修复 bug 并增加少量功能。无破坏性变更。

### v1.1.0（2026-02-13）

- mjlab 及其所有依赖（包括 mujoco-warp）现在可直接从 PyPI 安装。安装命令简化为 `pip install mjlab`，不再需要固定特定 mujoco-warp 修订版或使用自定义索引。
- 新增 RGB 和深度相机传感器，使用 BVH 加速的光线追踪。新增 `MetricsManager` 用于记录训练期间的自定义指标。新增地形可视化工具和多种新地形类型。Viser 查看器新增站点组可视化。
- `rsl-rl-lib` 升级到 4.0.0，支持原生 ONNX 导出。这对策略部署到生产环境（如边缘设备）至关重要。

### v1.0.0（2026-01-29）

- mjlab 宣布稳定。新增 `RayCastSensor`（地形和障碍物检测）、接触传感器历史追踪（改进接触动力学）、肌肉执行器支持（生物力学仿真）、传感器缓存（大规模训练性能优化）和更好的 NaN 处理（观测和传感器数据中的检测）。
- 新增 `notebooks/create_new_task.ipynb` 笔记本，指导用户创建新任务。`scripts/benchmarks/generate_report.py` 用于生成基准测试报告。

### v0.1.0（2025-09-29）

- mjlab 首次公开发布，作为早期 beta 版本。可通过 PyPI 安装，但需要固定 mujoco-warp 的 git 修订版。提供预训练的 Unitree G1 人形机器人运动模仿策略演示。
- API 可能随社区反馈演进。这是框架的起点，后续所有功能均在此基础上构建。

## 采用与规划提示

- **当前版本（v1.5.0）适合新项目启动**：API 趋于稳定，依赖管理简化（PyPI 固定版本），文档完善（包括 cartpole 教程和异构世界文档）。破坏性变更从 v1.3.0 的高峰期（执行器配置重写）减少到 v1.5.0 的少量弃用项（`SimulationCfg.ls_parallel`）。新用户应直接使用 v1.5.0。

- **从旧版本迁移需注意破坏性变更**：如果从 v1.1.x 或更早版本升级，需要处理 v1.2.0 的域随机化 API 重写（`randomize_field` 移除）和 v1.3.0 的执行器配置简化（`DelayedActuator` 移除）。v1.4.0 和 v1.5.0 的迁移成本较低，主要是 MuJoCo 版本升级和少量配置项调整。建议逐版本升级并参考每个版本的 changelog。

- **生态系统正在形成，但社区贡献仍需培育**：v1.5.0 文档列出了 Unitree、PAL Robotics、LEAP Hand 等多个外部项目，表明框架正在被行业采用。但首次贡献者数量在 v1.3.0 达到峰值（6 人）后有所下降。产品经理应关注社区活跃度，考虑提供更多教程、示例任务和贡献指南来维持增长。

- **产品方向明确聚焦于 GPU 加速的 sim-to-real 工作流**：从 v1.2.0 的域随机化重写、v1.3.0 的地形课程系统、v1.4.0 的异构世界到 v1.5.0 的直流电机执行器，mjlab 持续增强仿真保真度和策略泛化能力。云端训练（SkyPilot 集成）和 ONNX 导出支持表明框架正在覆盖从训练到部署的完整链路。建议关注 MuJoCo Warp 的更新节奏，因为 mjlab 的版本升级紧密跟随上游。
