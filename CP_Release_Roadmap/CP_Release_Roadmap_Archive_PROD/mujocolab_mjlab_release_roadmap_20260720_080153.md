# mujocolab/mjlab Release Roadmap

- 仓库: `mujocolab/mjlab`
- 统计窗口: 最近一年
- 最新版本: v1.5.0 (2026-06-29 07:09:19 CST)
- 纳入统计的最早版本: v0.1.0 (2025-09-29 18:00:45 CST)
- 版本概况: 最近一年共 8 个版本，其中正式版 7 个、预发布版 1 个
- 详细证据索引: `mujocolab_mjlab_release_roadmap_reference.md`

## 核心判断

- mjlab 在过去一年从早期 beta 版本快速演进为稳定的 GPU 加速机器人学习框架，核心定位是提供轻量级、可组合的环境和最小化设置摩擦。框架已从 v0.1.0 发展到 v1.5.0，依赖链从需要手动指定 git 修订版变为完全通过 PyPI 安装，大幅降低了用户入门门槛。

- 产品演进的核心驱动力是持续对齐上游 MuJoCo 和 MuJoCo Warp 的版本更新，同时围绕 sim-to-real 转移的关键技术（域随机化、地形生成、执行器建模）进行深度重构。v1.2.0 的域随机化重写和 v1.3.0 的地形系统重设计是两条最重要的产品主线。

- 框架已获得初步的生态系统认可，Unitree Robotics 和 PAL Robotics 等厂商已发布基于 mjlab 的官方 RL 环境。这表明 mjlab 正在从学术原型向行业可用的训练基础设施过渡，但 Windows 支持和 macOS 训练能力仍是明确的平台限制。

## 产品演进主线

- **从手动依赖管理到一键安装**：v0.1.0 需要用户手动指定 `mujoco-warp` 的 git 修订版，v1.1.0 实现所有依赖从 PyPI 直接安装，v1.5.0 进一步移除对 `py.mujoco.org` 夜间索引的依赖。这条主线显著降低了新用户的设置成本，使 `pip install mjlab` 成为唯一需要的安装命令。

- **域随机化从手动字段操作到类型化、自动一致的系统**：v1.2.0 用类型化的 `dr` 模块替换了旧的 `randomize_field` 接口，自动处理物理一致性（如质量变化后自动更新惯性）。v1.4.0 和 v1.5.0 持续扩展随机化覆盖范围，新增材质属性、几何对摩擦、以及每轴随机化事件的正确组合。这对 sim-to-real 转移的质量至关重要。

- **地形系统从基础生成到预设化、确定性课程**：v1.3.0 引入 `@terrain_preset` 装饰器和预设配置，v1.5.0 确保课程难度在行间确定且达到配置端点，并修复了多个边缘情况。这使得复杂地形训练可复现，对四足和人形机器人运动策略训练是核心能力。

- **执行器建模从基础 PD 到完整的电机模型**：v1.3.0 简化了执行器配置（延迟内联化、XML 类型自动检测），v1.4.0 添加原生隐式 PD 执行器，v1.5.0 引入完整的直流电机执行器（支持电压/位置/速度模式、反电动势、热模型、LuGre 摩擦）。这使 mjlab 能够更准确地模拟真实机器人硬件。

## 版本演进解读

### v1.5.0 (2026-06-29)

- 将 MuJoCo 和 MuJoCo Warp 升级到 3.10，完全从 PyPI 固定版本，移除了对 `py.mujoco.org` 夜间索引的依赖。`SimulationCfg.ls_parallel` 被弃用并忽略，因为上游已移除并行线搜索。
- 新增 `BuiltinDcMotorActuator`，原生封装 MuJoCo 的 `<dcmotor>`，支持电压、位置、速度输入模式，以及可选的积分、电感、LuGre 摩擦和齿槽效应扩展。这对需要精确电机建模的 sim-to-real 场景是重要补充。
- 地形生成实现确定性课程：难度在行间确定且达到配置端点，高度场使用固定发散调色板按绝对高度着色。修复了多个难度为 0 的边缘情况（空边框、NaN 颜色、编译失败）。
- 域随机化新增材质属性（发射、镜面、光泽、纹理重复）的随机化，修复了针对同一模型字段不同轴的随机化事件正确组合的问题。

### v1.4.0 (2026-05-27)

- 引入每世界网格变体（`VariantEntityCfg`），允许在批量模拟中为同一逻辑实体使用不同网格资产。变体必须具有相同的运动学结构，但网格几何体可以不同。域随机化、原生查看器和 Viser 查看器自动使用分配的变体。这对训练策略的泛化能力有直接价值。
- 新增 `BuiltinPdActuator`，原生 MuJoCo PD 控制，支持位置和速度目标。与 `IdealPdActuator` 不同，它通过隐式积分实现更稳定的控制，`effort_limit` 通过 `jnt_actfrcrange` 或 `tendon_actfrcrange` 强制执行。
- 新增 `mdp.projected_gravity_from_sensor` 观测，从 IMU 站点的 `framezaxis` 传感器读取，正确反映 IMU 安装随机化。Go1 和 G1 机器人已包含所需的 `imu_upvector` 传感器。
- 奖励、终止和指标管理器现在在计算时验证项的输出形状，返回错误形状时引发 `ValueError` 并命名违规项，避免静默广播或训练时失败。
- 破坏性变更：从 `MujocoCfg.enableflags` 中移除 `"multiccd"`；`CameraSensorData.segmentation` 从 `[B, H, W]` 几何体 ID 改为 `[B, H, W, 2]` 类型化 `(object_id, object_type)` 对。

### v1.3.0 (2026-04-15)

- Viser 查看器内部重构为基于独立的 `mjviser` 包，新增可视化标签页（叠加控制）、组标签页（几何体和站点可见性）、奖励条面板、W&B 运行浏览、检查点热切换和运动参考擦除器。查看器架构的模块化降低了维护成本。
- 地形系统全面重设计：引入 `@terrain_preset` 装饰器用于组合可重用配置，课程模式每列分配一种地形类型，`proportion` 控制机器人分布。新增 `STAIRS_TERRAINS_CFG` 预设和 `TerrainHeightSensor`（基于 `RayCastSensor` 的垂直间隙传感器）。
- 执行器配置简化：延迟字段内联到任何 `ActuatorCfg` 子类，移除 `DelayedActuator` 和相关类。四个 XML 执行器配置类合并为单个 `XmlActuatorCfg`，自动从 XML 检测执行器类型。
- 新增 `RecorderManager`（记录观测/动作/环境数据）、`termination_curriculum`（调度终止参数变化）、`RelativeJointPositionAction`（相对当前配置的关节位置控制）、`dr.pair_friction`（几何对摩擦随机化）。
- 新增 cartpole 教程，从零开始构建环境，涵盖场景设置、动作和观测项、奖励、终止和训练。
- 破坏性变更：移除 `DelayedActuator`、`DelayedActuatorCfg`、`DelayedBuiltinActuatorGroup`；`delay_target` 移除；四个 XML 执行器配置类合并为 `XmlActuatorCfg`；`TerrainImporter` 和 `TerrainImporterCfg` 别名移除；`EntityData.generalized_force` 移除；`ActuatorCfg.armature` 和 `.frictionloss` 默认值从 `0.0` 改为 `None`。

### v1.2.0 (2026-03-07)

- 域随机化全面重设计：用类型化的 `dr` 模块替换 `randomize_field` 接口，自动处理物理一致性（质量变化后更新惯性，几何体大小变化后更新碰撞边界）。覆盖几何体、刚体、视觉、相机和光照。自定义操作和分布是一等公民。
- 查看器时序模型重写：单一模拟预算累加器配合挂钟时间截止，保持物理和渲染在任何速度倍率下同步。新增单步模式、错误恢复、力箭头可视化、实时因子显示。Viser 新增速度摇杆、改进的项绘图器和重新组织的控制面板。
- 新增 `"step"` 事件模式（每环境步触发）和 `apply_body_impulse`（训练期间向机器人施加外部力，可配置持续时间、大小和作用点）。
- 新增 SkyPilot 集成，支持单命令在 Lambda Cloud 上训练，文档涵盖设置、监控和成本管理。W&B 扫描脚本支持多 GPU 实例。
- 文档完全重写，新增 `export-scene` CLI、`rsl-rl-lib` 升级到 5.0.1、Docker 镜像、接触传感器历史记录。
- 破坏性变更：`randomize_field` 移除；`EventTermCfg` 不再接受 `domain_randomization`；`RslRlModelCfg` 使用 `distribution_cfg` 字典替代 `stochastic`/`init_noise_std`/`noise_std_type`。

### v1.1.1 (2026-02-15)

- 新增差分 IK 动作空间，用于基于逆运动学的控制。
- 原生查看器新增奖励可视化，Viser 查看器扩展支持指标绘图。
- 视频录制从 `moviepy` 切换到 `mediapy`，减少依赖问题。
- 此版本为小补丁，无破坏性变更。

### v1.1.0 (2026-02-13)

- mjlab 及其所有依赖（包括 mujoco-warp）现在可直接从 PyPI 安装，安装命令简化为 `pip install mjlab`。这是从 beta 到稳定版的关键里程碑。
- 新增 RGB 和深度相机传感器（BVH 加速光线投射）、MetricsManager（训练期间记录自定义指标）、地形可视化工具和多种新地形类型。
- `rsl-rl-lib` 升级到 4.0.0，支持原生 ONNX 导出。

### v1.0.0 (2026-01-29)

- mjlab 正式宣布稳定。新增 RayCastSensor（地形和障碍物检测）、接触传感器历史跟踪、肌肉执行器支持（生物力学模拟）、传感器缓存（大规模训练性能优化）和改进的 NaN 处理。
- 此版本标志着框架从 beta 阶段毕业，API 进入稳定状态。

### v0.1.0 (2025-09-29)

- mjlab 首次公开发布，在 GitHub 和 PyPI 上可用。提供预训练的 Unitree G1 人形机器人运动模仿策略演示。
- 明确标记为早期 beta 版本，API 可能随社区反馈演进。

## 采用与规划提示

- **采用时机**：mjlab 已从 v1.0.0 开始稳定，依赖链已完全通过 PyPI 管理。对于需要 GPU 加速机器人学习框架的团队，当前版本（v1.5.0）已具备生产级能力，包括完整的域随机化、确定性地形课程和多种执行器模型。建议新项目直接从 v1.5.0 开始。

- **迁移成本**：从 v1.2.0 到 v1.5.0 的每个主要版本都包含破坏性变更。域随机化接口在 v1.2.0 完全重写，执行器配置在 v1.3.0 简化，XML 执行器配置类合并。如果从 v1.1.x 或更早版本迁移，需要重写域随机化代码和执行器配置。v1.4.0 和 v1.5.0 的破坏性变更较小（移除 `multiccd` 标志、分割数据类型变更）。建议参考每个版本的 changelog 进行逐步迁移。

- **目标用户**：mjlab 最适合需要大规模并行训练（4096+ 环境）的机器人学习团队，特别是四足和人形机器人运动控制。框架已获得 Unitree Robotics 和 PAL Robotics 的官方支持，表明在行业应用中有实际价值。macOS 仅支持评估，Windows 支持可能滞后，训练必须在 Linux 上使用 NVIDIA GPU 进行。

- **生态系统观察点**：v1.5.0 的 research.rst 列出了多个基于 mjlab 的衍生项目（Asimov 双足机器人、H1 运动、MyoSuite 肌肉骨骼集成、LEAP Hand 灵巧操作等），表明社区正在围绕框架构建工具链。建议关注 `unitreerobotics/unitree_rl_mjlab` 和 `pal-robotics/pal_mjlab` 等官方仓库的更新，它们反映了框架在真实机器人平台上的应用方向。
