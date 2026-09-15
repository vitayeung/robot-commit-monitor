# mujocolab/mjlab Release Roadmap

- 仓库: `mujocolab/mjlab`
- 统计窗口: 最近一年
- 最新版本: v1.5.3 (2026-07-22 23:54:36 CST)
- 纳入统计的最早版本: v0.1.0 (2025-09-29 18:00:45 CST)
- 版本概况: 最近一年共 11 个版本，其中正式版 10 个、预发布版 1 个
- 详细证据索引: `mujocolab_mjlab_release_roadmap_reference.md`

## 核心判断

- mjlab 在 v1.5.0 之后连续发布三个补丁版本（v1.5.1、v1.5.2、v1.5.3），主要聚焦于修复大规模训练中的崩溃问题、提升与上游 MuJoCo Warp 的兼容性，以及完善可视化工具的可配置性。框架整体进入稳定维护期，未引入新的重大功能。

- v1.5.1 强制要求 MuJoCo Warp 3.10.0.2，修复了向量化环境中 `qfrc_constraint` 填充错误的关键问题，并新增 `MeshCfg` 网格资产编辑器和 `SimulationCfg.broadphase` 宽阶段碰撞算法配置。这些变更提升了框架在复杂场景下的稳定性和灵活性。

- v1.5.2 修复了多环境域随机化导致的 CUDA 非法内存访问（`actuator_acc0` 扩展问题）和 `MaterialCfg.reflectance` 被忽略的渲染缺陷，直接影响了大规模训练的可执行性和视觉保真度。

- v1.5.3 将 MuJoCo Warp 升级至 3.10.0.3，修复了特定 GPU 架构上因大规模域随机化引发的 CUDA 700 崩溃，并修复了射线传感器调试可视化滞后的问题。Viser 奖励条面板现在支持通过 `ViewerConfig.reward_bar_max_terms` 配置最大显示项数。

## 产品演进主线

- **从功能发布到稳定性修复**：v1.5.0 是功能密集的里程碑（直流电机执行器、确定性地形课程、材质随机化），而 v1.5.1 至 v1.5.3 全部为补丁版本，专注于修复上游依赖兼容性问题、多环境崩溃和边缘情况。这表明框架核心功能已趋于稳定，团队将精力转向生产环境的可靠性。

- **上游依赖锁定成为关键维护项**：v1.5.1 强制要求 MuJoCo Warp 3.10.0.2，v1.5.3 进一步升级至 3.10.0.3。每次升级都修复了向量化环境中的关键错误（`qfrc_constraint`、CUDA 700 崩溃），说明 mjlab 的稳定性高度依赖上游 MuJoCo Warp 的版本质量。用户必须保持依赖版本与框架要求一致。

- **域随机化和地形系统的持续打磨**：v1.5.2 修复了多环境域随机化的 CUDA 崩溃，v1.5.3 修复了地形课程在初始重置时的提升逻辑错误。这些修复表明域随机化和地形系统虽然是成熟功能，但在大规模并行训练场景下仍有边缘情况需要持续处理。

- **可视化工具的可配置性提升**：v1.5.3 使 Viser 奖励条面板的最大项数可配置，v1.5.1 新增天空盒渲染支持。这些改进降低了复杂环境下的可视化门槛，对调试和演示有实际价值。

## 版本演进解读

### v1.5.3（2026-07-22）

- 将 MuJoCo Warp 升级至 3.10.0.3，修复了特定 GPU 架构上因大规模域随机化引发的 CUDA 700 崩溃。修复了射线传感器调试可视化滞后一步的问题。
- Viser 奖励条面板的最大显示项数现在可通过 `ViewerConfig.reward_bar_max_terms` 配置，默认值为 20。环境奖励项超过 20 个时不再静默丢弃。
- 修复了地形课程在初始重置时忽略 `max_init_terrain_level=0` 的问题，以及速度任务中 `joint_pos` 观测未被偏置的缺陷。Go1 速度任务现在启用 `obs_normalization`，旧检查点需重新训练。

### v1.5.2（2026-07-18）

- 修复了多环境域随机化触发 `set_const` 时导致的 CUDA 非法内存访问，`actuator_acc0` 现在正确扩展。修复了 `MaterialCfg.reflectance` 在构建 MuJoCo 模型时被忽略的问题。
- 此版本为纯修复补丁，无新增功能或破坏性变更。对于使用域随机化和材质渲染的用户，建议升级以避免训练崩溃和视觉不一致。

### v1.5.1（2026-07-16）

- 强制要求 MuJoCo Warp 3.10.0.2，修复了向量化环境中 `qfrc_constraint` 填充错误的关键问题。早期 3.10.0.x 版本不再支持。新增 `MeshCfg` 网格资产编辑器，支持按名称匹配并编辑网格属性。
- 新增 `SimulationCfg.broadphase` 和 `SimulationCfg.broadphase_filter` 配置项，用于控制 MuJoCo Warp 的宽阶段碰撞算法。为相机传感器启用天空盒渲染。
- 修复了 `TorchArray` 在 MuJoCo Warp 3.10.0.2 下未正确扩展世界共享模型字段的问题，以及 `mdp.bad_orientation` 在 float32 舍入导致 NaN 时的崩溃。可融合执行器（理想 PD、直流电机）的命令延迟现在跨所有融合执行器共享一个延迟配置。

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

- **采用时机**：v1.5.3 是当前最新稳定版本，修复了多个大规模训练崩溃问题，建议新项目直接使用 v1.5.3。如果已在使用 v1.5.0，建议升级至 v1.5.3 以获得上游依赖修复和稳定性改进。v1.5.1 强制要求 MuJoCo Warp 3.10.0.2，v1.5.3 要求 3.10.0.3，升级时需同步更新依赖。

- **迁移成本**：v1.5.1 至 v1.5.3 均为补丁版本，无破坏性变更。从 v1.5.0 升级只需更新依赖版本。注意 v1.5.3 中 Go1 速度任务启用了 `obs_normalization`，旧检查点无法加载，需重新训练。如果使用自定义奖励项超过 20 个的环境，v1.5.3 的 Viser 奖励条面板需要显式配置 `reward_bar_max_terms`。

- **目标用户**：v1.5.1 至 v1.5.3 的修复主要惠及使用大规模并行训练（4096+ 环境）和域随机化的团队。如果训练中遇到 CUDA 崩溃、`qfrc_constraint` 错误或地形课程行为异常，这些版本提供了直接修复。使用自定义网格资产的用户可从 v1.5.1 的 `MeshCfg` 中受益。

- **生态系统观察点**：v1.5.1 新增的 `SimulationCfg.broadphase` 配置表明 mjlab 正在与 MuJoCo Warp 的碰撞检测演进保持同步。v1.5.3 修复的射线传感器调试可视化问题说明传感器系统仍在积极维护。建议关注上游 MuJoCo Warp 的版本更新，因为 mjlab 的稳定性高度依赖其修复。
