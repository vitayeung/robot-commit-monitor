# isaac-sim/IsaacLab Release Roadmap

- 仓库: `isaac-sim/IsaacLab`
- 统计窗口: 最近一年
- 最新版本: v3.0.0-beta2.patch1 (2026-07-02 12:21:18 CST)
- 纳入统计的最早版本: v2.1.1 (2025-07-30 20:59:44 CST)
- 版本概况: 最近一年共 9 个版本，其中正式版 6 个、预发布版 3 个
- 详细证据索引: `isaac-sim_IsaacLab_release_roadmap_reference.md`

## 核心判断

- **Isaac Lab 在过去一年完成了从稳定迭代到架构级重构的跨越。** 从 v2.1.1 到 v3.0.0-beta2.patch1，产品经历了两个截然不同的阶段：前半年（v2.1.1 至 v2.3.2）以功能扩展和生态兼容性为主，后半年（v3.0.0-beta 系列）则彻底重构了物理后端架构，引入了多后端工厂模式、无 Kit 运行模式以及全新的可视化框架。对于产品经理而言，这意味着现有基于 v2.x 的项目需要评估迁移成本，而新项目应直接基于 v3.0 beta 系列规划。

- **v3.0 系列的核心价值在于解耦与灵活性，但当前仍处于 beta 阶段，稳定性与性能尚未达到生产级。** 多后端架构（PhysX、Newton、OVPhysX）允许用户在同一套 API 下切换物理引擎，Newton 后端甚至支持完全脱离 Isaac Sim 运行（kit-less 模式），大幅降低了部署门槛和硬件依赖。然而，官方明确警告 develop 分支仍存在 breaking changes、性能回退和错误信息变动，且已知限制清单较长。建议在 v3.0 正式版发布前，仅将 beta 版本用于技术验证和原型开发。

- **v2.3.x 系列是 v2 时代的收官之作，功能成熟度最高，适合当前生产环境。** v2.3.2 明确标注为“main 分支的最终版本”，后续开发已全部转向 develop 分支。该版本集成了多旋翼无人机支持、视觉触觉传感器、多网格 RayCaster、Haply 设备集成等重大新功能，且与 Isaac Sim 5.1 兼容。对于需要稳定运行环境的团队，v2.3.2 是最稳妥的选择。

- **生态兼容性变化剧烈，平台迁移成本不可忽视。** 过去一年中，Isaac Lab 先后适配了 Isaac Sim 4.5、5.0、5.1、6.0 和 6.0.1，Python 版本从 3.10 升级至 3.12，PyTorch 从 2.7.0 升级至 2.10.0，CUDA 支持从 12.8 扩展到 13.0。同时，Ubuntu 20.04 支持已正式终止，Windows 10 支持即将终止。任何采用决策都必须同步评估底层平台的生命周期和升级路径。

## 产品演进主线

- **从单一后端到多后端物理架构：这是过去一年最根本的产品变革。** v2.x 时代，Isaac Lab 仅支持 PhysX 后端，所有资产和传感器类直接绑定 PhysX 实现。v3.0 beta 引入了工厂模式，将 `Articulation`、`RigidObject`、`ContactSensor` 等核心类抽象为基类，后端实现分散到 `isaaclab_physx` 和 `isaaclab_newton` 等独立扩展包中。用户代码无需修改导入路径，工厂在运行时自动分派到激活的后端。这一架构为未来支持更多物理引擎（如 MuJoCo、Bullet）铺平了道路，也使得无 Isaac Sim 运行成为可能。

- **Newton 后端与 kit-less 模式：从“必须安装 Isaac Sim”到“可独立运行”的范式转变。** Newton 后端基于 MuJoCo-Warp，支持 MJWarp、XPBD 和 Featherstone 求解器，并具备 CUDA graph 加速能力。更重要的是，它允许用户在不启动 Isaac Sim 的情况下运行训练和推理（kit-less 模式），大幅降低了硬件要求和部署复杂度。v3.0 beta2 进一步扩展了 Newton 对射线投射器、IMU/PVA 传感器、接触传感器、关节扳手、可变形物体和 VBD 耦合的支持，并新增了四足和双足机器人的粗糙地形运动预设。

- **模仿学习与灵巧操作成为 v2.x 时代的功能增长主线。** v2.2.0 引入了 FORGE 和 AutoMate 接触丰富操作任务，以及 GR1 模仿学习环境。v2.3.0 推出了 DexSuite（基于 Kuka 臂和 Allegro 手的灵巧操作环境），支持自动域随机化和群体训练。同时，Mimic 管道集成了 SkillGen，引入 cuRobo 实现 GPU 加速的运动规划和技能分段数据生成。v2.3.2 进一步增加了视觉触觉传感器和 Haply 设备集成，使遥操作和模仿学习的硬件覆盖更加完整。

- **开发者体验与平台兼容性持续优化，但迁移成本也在累积。** v2.2.0 将 Python 从 3.10 升级到 3.11，并终止了对 Ubuntu 20.04 的官方支持。v3.0 beta 将 Python 升级到 3.12，PyTorch 升级到 2.10.0，并引入了 CUDA 13.0 对 aarch64 架构的支持。训练入口从分散的脚本统一为 `isaaclab.sh train --rl_library <name> --task <task>` 格式，`--headless` 标志被 `--viz` 替代。所有四元数统一为 XYZW 顺序。这些变化虽然提升了长期可维护性，但对现有代码库的迁移工作量不容忽视。

## 版本演进解读

### v3.0.0-beta2.patch1 (2026-07-02)

- 这是一个小型补丁版本，主要更新为支持 Isaac Sim 6.0.1。Isaac Sim 6.0.1 修复了 NuRec 工作流中的流式传输崩溃问题，并增加了对通过稀疏像素高斯图渲染的 NuRec 场景的遥操作支持。
- 同时修复了 Isaac Lab 依赖和 Docker 镜像的兼容性问题，将 h5py 版本提升至 >=3.16.0。对于使用 NuRec 或依赖 Docker 部署的团队，此补丁是必要的升级。

### v3.0.0-beta2 (2026-06-17)

- 这是 v3.0 beta 系列的稳定化版本，重点加固了多后端架构。PhysX、Newton、OVPhysX、Isaac RTX、OVRTX 和无 Kit 执行路径均得到了后端选择、场景数据路由、克隆计划处理、传感器重置行为和运行时兼容性检查的改进。当请求不支持的物理/渲染/可视化组合时，现在会给出更清晰的错误信息。
- Newton 后端功能大幅扩展：新增射线投射器、帧变换器、IMU/PVA 传感器、接触传感器、关节扳手、可变形物体和 VBD 耦合支持。新增四足和双足机器人的粗糙地形运动预设，以及 MJWarp 求解器比较文档。
- 安装和训练命令进一步简化，文档覆盖了 Newton 安装、支持功能、Warp 环境迁移等主题。对于计划评估 Newton 后端的团队，此版本是首个功能较为完整的 beta 版本。

### v3.0.0-beta (2026-03-17)

- 这是 Isaac Lab 3.0 的首个 beta 版本，引入了根本性的架构重构。核心变化是工厂模式的多后端架构：`Articulation`、`RigidObject`、`ContactSensor` 等类现在由抽象基类支持，后端实现分散到 `isaaclab_physx` 和 `isaaclab_newton` 扩展包中。用户代码无需修改导入路径。
- Newton 后端支持无 Isaac Sim 运行（kit-less 模式），支持关节、刚体、接触传感器、MuJoCo-Warp 求解器（可配置积分器和接触模型）以及 CUDA graph 加速。同时引入了可插拔的可视化框架，支持 USD 舞台、Newton Warp 渲染器、Rerun 和 Viser 四种后端。
- 这是一个重大 breaking change 版本。训练入口统一为 `isaaclab.sh train --rl_library <name> --task <task>`，`--headless` 被 `--viz` 替代。所有四元数统一为 XYZW 顺序。传感器数据现在返回 Warp 原生类型。URDF 和 MJCF 导入器已为 Isaac Sim 6.0 重写。官方提供了迁移指南和自动化工具。

### v2.3.2 (2026-02-03)

- 这是 v2.x 系列的最终版本，官方明确声明后续开发将转向 develop 分支。此版本引入了多项重大新功能：多旋翼/推进器支持（无人机）、多网格 RayCaster、视觉触觉传感器、Haply 设备集成，以及新的 OpenArm 环境。
- 核心 API 方面，`set_external_force_and_torque()` 方法被弃用，取而代之的是新的可组合扳手系统。对于需要稳定生产环境的团队，此版本是 v2 时代的推荐终点。

### v2.3.1 (2025-12-05)

- 这是一个小型补丁版本，修复了影响用户工作流的关键问题。终止日志记录行为发生变化：`get_done_term` 现在返回当前步长值而非上一轮值。
- 修复了 Isaac Sim 5.1 中 URDF 导入器的 breaking change（merge joints 标志不再支持），通过更新导入器至 2.4.31 恢复了原有行为。对于依赖 URDF 导入的团队，此补丁是必要的。

### v2.3.0 (2025-10-29)

- 基于 Isaac Sim 5.1，重点增强了灵巧操作、遥操作和模仿学习工作流。推出了 DexSuite（Kuka 臂 + Allegro 手的灵巧操作环境），支持自动域随机化和群体训练。
- Mimic 管道集成了 SkillGen，引入 cuRobo 实现 GPU 加速的运动规划和技能分段数据生成。注意 cuRobo 具有专有许可条款，需要单独审查。表面夹持器扩展至 Manager 工作流，新增 Franka、UR10、Galbot、Agibot 等机器人变体。

### v2.2.1 (2025-08-30)

- 这是一个功能增强型补丁版本。ContactSensor 新增接触点位置报告功能。Pink IK 控制器增加了零空间姿态控制能力。
- 新增 RSL-RL 对称性示例（Cartpole 和 ANYmal 运动）。环境动作/观察描述符导出功能上线，有助于策略部署和文档生成。应用设置方面，禁用了头戴式和头戴式渲染应用的速率限制，并将分析器后端默认设置为 NVTX。

### v2.2.0 (2025-08-08)

- 基于 Isaac Sim 5.0（同时向后兼容 4.5），引入了多项重大升级。物理引擎方面，更新了关节摩擦建模（使用最新 PhysX API），增加了空间肌腱支持，改进了表面夹持器交互。
- 新增 FORGE 和 AutoMate 接触丰富操作任务，以及两个 GR1 模仿学习环境。遥操作工具增加了可配置参数和 CloudXR 运行时更新（头部追踪和手部追踪）。性能方面，支持 Stage in Memory 和 Fabric 中的克隆，新增 OVD 记录器用于大规模场景 GPU 动画录制。
- Python 版本从 3.10 升级至 3.11，终止了对 Ubuntu 20.04 的官方支持。原生直播流支持被移除，`LIVESTREAM=1` 现在用于 WebRTC 流式传输。

### v2.1.1 (2025-07-30)

- 兼容 Isaac Sim 4.5，这是一个功能密集的版本，涵盖资产接口、传感器接口、MDP 项和基础设施的广泛更新。关键新增包括：在刚体不同位置设置外力和扭矩的能力、关节扳手数据字段、FrameTransformer 可视化改进、以及 CoM 观测项。
- 重要 breaking change：`enable_stabilization` 标志默认改为 False，因为 PhysX 求解器已改进，不再需要非物理启发式方法进行接触稳定化。PyTorch 更新至 2.7.0，支持 CUDA 12.8 Blackwell。

## 采用与规划提示

- **新项目建议直接基于 v3.0 beta 系列启动，但需预留迁移缓冲。** v3.0 的架构优势（多后端、kit-less、统一训练入口）对于新项目是显著的长期收益。然而，beta 阶段仍可能发生 breaking changes，建议将核心逻辑与后端特定代码严格分离，并密切关注 develop 分支的更新。如果项目时间线紧迫，可以考虑基于 v2.3.2 启动原型，待 v3.0 正式版发布后再迁移。

- **v2.3.2 是当前生产环境的推荐基线，但需规划迁移路径。** 官方已明确将开发重心转向 v3.0，v2.x 系列不再接收新功能。如果团队当前依赖 v2.x，建议在下一个产品周期内完成向 v3.0 的迁移规划。迁移成本主要来自：训练入口变更、四元数顺序调整、传感器数据格式变化、以及 URDF/MJCF 导入器重写。官方提供了迁移指南和自动化工具，建议提前进行技术评估。

- **Newton 后端和 kit-less 模式是降低部署成本的关键技术，但需验证场景适用性。** 对于需要大规模并行训练或边缘部署的场景，kit-less 模式可以显著降低硬件要求和运维复杂度。然而，Newton 后端目前的功能覆盖仍不完整（例如可变形物体支持有限），且性能调优仍在进行中。建议在采用前，使用自己的机器人模型和任务场景进行充分的基准测试。

- **关注 Isaac Sim 平台的生命周期变化对产品规划的影响。** Omniverse Launcher、Nucleus Workstation 和 Nucleus Cache 将于 2025 年 10 月 1 日后停止服务，Live Sync 功能已在 Isaac Sim 4.5 中弃用。Isaac Sim 6.0 是首个完全脱离 Omniverse Launcher 的版本。如果团队依赖这些组件，需要提前规划迁移至 Enterprise Nucleus Server 或直接使用 Isaac Sim 6.0 的独立安装方式。
