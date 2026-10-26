# isaac-sim/IsaacLab Release Roadmap

- 仓库: `isaac-sim/IsaacLab`
- 统计窗口: 最近一年
- 最新版本: v3.0.0 (2026-10-20 10:05:51 CST)
- 纳入统计的最早版本: v2.3.0 (2025-10-29 05:38:54 CST)
- 版本概况: 最近一年共 9 个版本，其中正式版 5 个、预发布版 4 个
- 详细证据索引: `isaac-sim_IsaacLab_release_roadmap_reference.md`

## 核心判断

- **v3.0.0 正式发布，3.0 从 EA 转为推荐基线。** 官方明确 `v3.0.0` 是 Isaac Lab 3.0 的正式版本，也是新项目与 2.x 迁移的推荐基线，EA 阶段“只做缺陷修复与稳定性改进”的承诺已兑现为 GA。

- **“一套任务 API、多后端”从主张变为可交付形态。** Newton 作为 Warp 原生物理后端提供 MuJoCo-Warp、VBD、MPM 多条求解路径，覆盖刚体、形变体与粒子；OV 库把 `OVPhysX` 与 `OVRTX` 拆为独立库；Isaac Sim 保留为需要完整 PhysX/RTX、ROS bridge、XR、livestream 或 Kit 工具链时的可选路径。

- **安装与运行路径以 `uv` 为中心收敛为三条命令。** 默认环境为 Newton + PyTorch 训练环境，Isaac Sim 变为可选附加；`--extra ovphysx` 与 `--extra isaacsim` 分别对应 OV PhysX 与完整 Isaac Sim，`--viz newton_gl` 用于策略回放。

- **平台与依赖基线进一步收紧。** Python 3.12、Warp 1.17、默认 PyTorch CUDA 13.0；支持 Ubuntu 22.04+ x86_64、Linux aarch64（含 DGX Spark）与 Windows 11 x86_64；Isaac Sim 5.1 及更早版本不再受支持，Isaac Sim 侧 wheel 在 Linux 上要求 GLIBC 2.35+。

## 产品演进主线

- **3.0 主线由“架构定型”进入“正式交付”。** EA 确立的多后端任务 API、kit-less 执行、Warp 原生数据路径与统一工作流，在 GA 中成为推荐默认，而非可选实验路径。

- **物理后端从单一引擎扩展为求解器组合。** Newton 同时承载 MuJoCo-Warp、VBD、MPM，使刚体、形变体与粒子任务共用同一任务 API；OV 库则把 PhysX 与 RTX 渲染从 Kit 中解耦为可独立安装的组件。

- **Isaac Sim 的角色从“必需运行时”转为“按需能力包”。** 需要完整 PhysX/RTX 栈、ROS bridge、XR、livestream 或 Kit 工具链的工作流仍走 Isaac Sim，但默认安装不再包含它。

- **文档与演示资产继续作为独立交付线存在。** interactive-demos 的浏览器演示容器与 v3.0.0 的正式版本并行，前者不改变运行时依赖，后者定义新的安装与迁移基线。

## 版本演进解读

### v3.0.0（2026-10-20）

- 正式发布 Isaac Lab 3.0：一套任务 API 跨多种物理、渲染与可视化后端；Newton 后端提供 MuJoCo-Warp、VBD、MPM 多条求解路径，覆盖刚体、形变体与粒子；`OVPhysX` 与 `OVRTX` 作为独立库提供；Isaac Sim 变为可选，仅在需要完整 PhysX/RTX、ROS bridge、XR、livestream 或 Kit 工具链时安装。
- 对产品与用户价值在于迁移目标确定：官方将 `v3.0.0` 定位为新项目与 2.x 迁移的推荐基线，安装路径收敛为默认 Newton 训练环境、`--extra ovphysx` 与 `--extra isaacsim` 三条，训练、回放与可视化统一由 `isaaclab train` / `isaaclab play` 驱动。
- 迁移与兼容注意：需 Python 3.12、Warp 1.17 与默认 PyTorch CUDA 13.0（要求 Turing 及以上、compute capability 7.5+）；支持 Ubuntu 22.04+ x86_64、Linux aarch64（含 DGX Spark）与 Windows 11 x86_64；Isaac Sim 5.1 及更早版本不再受支持，Isaac Sim 侧 wheel 在 Linux 上要求 GLIBC 2.35+，x86_64 工作站建议至少 32 GB 内存与 16 GB 显存；DGX Spark 需 CUDA 13 或更新版本，且 SkillGen、XR 遥操作、livestream、Hub Workstation Cache、Cosmos Transfer1 与 RLinf 尚未在该平台支持或验证。

### interactive-demos（2026-10-16）

- 新增预构建的 Newton WebAssembly 仿真、浏览器查看器与导出器源码，作为 Isaac Lab 文档交互式演示的永久打包容器；后续更新在同一 release 追加资产，不创建新的编号版本，已有资产保持可用。
- 对用户价值在于演示与验证成本大幅降低：运行演示只需浏览器，解压归档后以本地静态服务器打开 `interactive/` 即可；归档内含 `exporters/`、场景与重建说明、许可证与 `tools/publish.py`。
- 兼容与使用注意：重建物理仿真需要固定版本的内置 Newton Web 编译器与 Emscripten；文档侧只引用经评审、以提交命名的归档并校验 SHA-256，更新时需同步修改归档 URL 与 SHA-256，并保留历史资产与兼容目录。该 release 与具体 Isaac Lab 版本的功能对应关系细节证据不足。

### v3.0.0-EA（2026-09-17）

- 这是 Isaac Lab 3.0 的 Early Access 版本，架构与功能集已定型：一套任务 API 跨多种物理、渲染、可视化后端，支持 kit-less 执行、Warp 原生数据路径，以及从安装到训练、评估、部署的统一工作流。构建基线为 Isaac Sim 6.1、Python 3.12、PyTorch 2.11、NVIDIA Warp 1.16、Newton 1.5.2。
- 对用户价值在于迁移目标明确化：官方声明从 EA 到 GA 期间 `release/3.0.0` 分支只做缺陷修复、稳定性、兼容性与文档改进，GA 目标为 2026 年 10 月底，因此现在开始迁移、训练与测试的返工风险低于 beta 阶段。官方同时提供三条可直接运行的路径：Newton 无 Isaac Sim、`--extra ov` 的 OVPhysX + OVRTX 完全 kit-less、以及 `--extra isaacsim` 的完整 Isaac Sim 体验。
- 迁移与兼容注意：Isaac Sim 5.1 及更早版本不再受支持，必须使用 Isaac Sim 6.1 与 Python 3.12；完整 Isaac Sim 工作流要求 Ubuntu 22.04+ 或 Windows 11、至少 32 GB 内存与 16 GB 显存；CUDA 13.0 的 PyTorch 构建支持 Blackwell GPU，DGX Spark 需要 CUDA 13 或更新版本。SkillGen、XR 遥操作、livestream、Hub Workstation Cache、Cosmos Transfer1 与 RLinf 目前在 DGX Spark 上未获支持或验证。

### v3.0.0-beta2.patch1（2026-07-02）

- 这是一个小型补丁版本，主要更新是支持 Isaac Sim 6.0.1，后者修复了 NuRec 工作流中的流式传输崩溃问题。同时将 h5py 版本提升至 >=3.16.0，并改进了 Docker 镜像的兼容性。
- 对于使用 NuRec（稀疏像素高斯渲染）进行遥操作的用户，此补丁直接修复了关键稳定性问题。Kit SDK 从 110.1.1 升级到 110.1.2，涉及多个底层组件版本更新。
- 迁移成本极低，仅需更新 Isaac Sim 版本和依赖版本。建议所有 v3.0.0-beta2 用户尽快升级。

### v3.0.0-beta2（2026-06-17）

- 这是 3.0 beta 系列的第二个版本，重点在于多后端架构的稳定化和功能补齐。Newton 后端新增了射线投射器、帧变换器、IMU/PVA、接触、关节力矩、形变物体和 VBD 耦合支持。同时增加了 Newton 粗糙地形运动预设（四足和双足）以及 MJWarp 集成。
- 对用户价值显著：Newton 后端的传感器覆盖度大幅提升，使得更多环境可以切换到高速的 kit-less 模式。新增的运行时兼容性检查和更清晰的错误提示降低了后端选型错误的调试成本。
- 迁移注意事项：此版本仍为 beta，官方明确表示开发分支可能继续引入破坏性变更。PyTorch 升级到 2.10.0，CUDA 12.8（x86_64）和 CUDA 13.0（aarch64）均得到支持。aarch64 和 DGX Spark 用户应特别关注安装文档更新。

### v3.0.0-beta（2026-03-17）

- 这是 Isaac Lab 3.0 的首个 beta 版本，引入了根本性的架构变革。核心变化包括：工厂模式多后端架构（PhysX 和 Newton）、可插拔可视化框架（Kit、Newton、Rerun、Viser 四种后端）、Warp 原生数据管线、无 Kit 运行模式、以及统一的 CLI 训练入口（`--viz` 标志替代已弃用的 `--headless`）。
- 对用户价值：Newton 后端支持 CUDA 图加速，可显著提升训练吞吐量；kit-less 模式降低了部署门槛；统一训练命令简化了工作流。四元数顺序从 WXYZ 改为 XYZW 以对齐 Warp/PhysX/Newton 标准。
- 迁移成本极高。官方提供了迁移指南和自动化工具，但涉及大量 API 变更：资产和传感器类导入路径不变但后端实现分离，模拟器配置类拆分为基础类和后端特定类，RL 训练入口统一为 `isaaclab.sh train --rl_library`。所有使用旧 API 的代码需要适配。建议在正式版发布前仅做评估性迁移。

### v2.3.2（2026-02-03）

- 这是 2.x 稳定分支的最终版本，官方明确表示后续开发将转向 3.0 的 develop 分支。此版本引入了多项重要新功能：多旋翼/推进器支持（无人机）、多网格射线投射器、视觉触觉传感器、Haply 设备集成、以及新的 OpenArm 环境。
- 对用户价值：无人机支持填补了空中机器人领域的空白；视觉触觉传感器为灵巧操作研究提供了新的感知模态；多网格射线投射器支持动态网格跟踪，提升了仿真真实感。
- 迁移注意事项：`set_external_force_and_torque()` 方法已被弃用，改用新的可组合力矩系统。这是 2.x 分支的最后一个版本，建议新项目直接评估 3.0 beta，但生产环境可继续使用此版本。

### v2.3.1（2025-12-05）

- 这是一个小型补丁版本，主要修复了影响用户工作流的关键问题。终止日志记录行为变更：`get_done_term` 现在返回当前步数值而非上一回合值。URDF 导入器更新到 2.4.31 以恢复对 merge-joints 标志的支持（该标志在 Isaac Sim 5.1 中被移除）。
- 对用户价值：URDF 导入器的修复直接影响了所有使用 URDF 导入机器人模型的用户。终止日志记录的行为变更可能影响依赖回合级统计的训练监控脚本。
- 迁移成本低，但需要检查训练脚本中是否依赖旧的终止日志行为。

### v2.3.0（2025-10-29）

- 此版本基于 Isaac Sim 5.1，重点强化了灵巧操作和模仿学习能力。核心新增包括：DexSuite（两个基于 Kuka 臂和 Allegro 手的灵巧操作环境，支持自动域随机化和群体训练）、SurfaceGripper 扩展（支持 Manager 工作流、新增 Franka/UR10 等机器人变体）、以及 SkillGen 集成（cuRobo GPU 运动规划与技能分段数据生成）。
- 对用户价值：DexSuite 为灵巧操作研究提供了开箱即用的基准环境；SkillGen 显著提升了模仿学习数据生成的效率和质量。新增的 G1 人形机器人环境结合了 RL 运动控制和 IK 操作。
- 迁移注意事项：cuRobo 具有专有许可条款，使用前需仔细审查。SurfaceGripper API 因 Isaac Sim 5.1 变更而调整。Windows 10 支持将在未来版本中移除。

### v2.2.1（2025-08-30）

- 这是一个功能增强型补丁版本。主要新增包括：ContactSensor 新增接触点位置报告、环境动作/观测描述符导出、RSL-RL 对称性示例（Cartpole 和 ANYmal 运动）。Pink IK 控制器增加了零空间姿态控制。
- 对用户价值：接触点位置报告为精细操作分析提供了新数据维度；动作/观测描述符导出有助于策略部署和文档生成；对称性示例展示了如何利用环境对称性加速 RL 训练。
- 迁移成本低，主要是增量功能添加。头戴式渲染和性能模式下的渲染预设调整可能影响视觉输出。

### v2.2.0（2025-08-08）

- 这是 2.x 系列的一个重要功能版本，兼容 Isaac Sim 5.0 并向后兼容 4.5。核心变化包括：增强的物理支持（关节摩擦建模、空间肌腱、改进的表面夹持器交互）、两个新的 GR1 模仿环境、FORGE 和 AutoMate 接触丰富操作任务集成、CloudXR 遥操作更新、以及 Stage in Memory 和 Fabric 克隆支持。
- 对用户价值：空间肌腱支持使得更真实的生物启发式机器人建模成为可能；FORGE/AutoMate 任务填补了精细接触交互学习的空白；Stage in Memory 和 Fabric 克隆显著加速了场景创建速度。
- 迁移注意事项：Python 版本从 3.10 升级到 3.11，Ubuntu 20.04 支持被放弃。`PhysicsMaterialCfg.improve_patch_friction` 属性被移除。原生直播流支持被移除，改用 WebRTC。资产路径发生变化（如 `Robots/Ant/ant_instanceable.usd` 移至 `Robots/IsaacSim/Ant/ant_instanceable.usd`）。

### v2.1.1（2025-07-30）

- 这是一个功能丰富的版本，兼容 Isaac Sim 4.5。核心新增包括：资产接口增强（支持在刚体不同位置设置外力/力矩、关节力矩数据字段、显式选择关节根 prim）、传感器接口增强（FrameTransformer 可视化连接线）、以及 MDP 项扩展（身体姿态、投影重力、关节力观测）。
- 对用户价值：外力位置参数支持使得更精细的接触模拟成为可能；关节力矩数据字段为力控策略提供了直接反馈。此版本不包含 Docker 镜像或 pip 包。
- 迁移注意事项：`enable_stabilization` 标志默认值改为 False，这可能导致接触力报告行为变化。PhysX 求解器改进后，旧的稳定化启发式不再适用于机器人应用。

## 采用与规划提示

- **新项目与 2.x 迁移直接以 v3.0.0 为目标基线。** 官方已将其定位为推荐版本，EA 到 GA 的稳定性窗口结束，继续停留在 EA 或 beta 不再有收益。

- **按工作流选择安装路径，而非默认全量安装。** 纯 Newton 训练与回放不需要 Isaac Sim；需要 ROS bridge、XR、livestream 或 Kit 工具链时再加 `--extra isaacsim`，需要 PhysX 但不要 Kit 时用 `--extra ovphysx`。

- **迁移前先核对平台与驱动基线。** 确认 Python 3.12、CUDA 13 驱动与 GPU 计算能力满足要求；aarch64 与 DGX Spark 用户需单独核对 PyTorch 构建与不受支持的功能清单；Windows 用户需先启用长路径支持。

- **interactive-demos 仍按文档资产对待。** 它不改变 v3.0.0 的运行时依赖或 API，团队无需为其调整环境；引用或自建浏览器演示时沿用其提交命名归档与 SHA-256 校验的发布纪律。
