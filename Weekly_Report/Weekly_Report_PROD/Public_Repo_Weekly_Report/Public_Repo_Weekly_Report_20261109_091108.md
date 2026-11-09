# 具身智能周报 (2026年11月09日 09:11:08)

- 统计窗口: 2026-11-02 09:06:37 +0800 至 2026-11-09 09:11:08 +0800（左闭右开）

## 行业风向总览

本周具身智能行业风向呈现“仿真底座加固、平台生态扩张”双线并行。技术焦点集中在物理引擎的数值正确性与执行器语义一致性：MuJoCo修复稀疏Cholesky超节点检测并优化射线包围球剔除，mjlab以测试固化延迟执行器reset后姿态语义，Warp修正内核内wp.zeros()原地清零与CUDA设备错配，IsaacLab则治理TF32相机精度并统一传感器数据来源。合成数据方面，本周无直接合成数据管线更新，但RLinf接入RoboDojo、GenieSim、SIMPLE等多元仿真环境，以及SO-101真机采集闭环，实质上在扩充“仿真+真机”数据来源矩阵，为后续合成数据生成与评测提供环境基础。产品经理需关注三个信号：一是多后端统一语义层正成为IsaacLab与RLinf的共同收敛点，传感器存储共享、rollout后端可插拔将降低新硬件/新环境接入成本；二是破坏性API清理与依赖迁移（IsaacLab移除3.1废弃API、OVStorage替换omni.client）提示下游需尽早对齐基线；三是插件加载容错与异构加速器适配（ROCm）扩张，意味着生态覆盖优先于性能基准，选型时应要求配套CI与性能基线，避免“可跑不可比”。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 2 条
- 高价值提交（≥6分）: 1 条
- 代码更新规模: +47 / -2 行
- 主要贡献者: Gijs de Jong, Louis LE LAY

## 🧭 趋势点评

本周唯一的高价值提交（#1308）延续了仓库近半年“执行器语义与重置一致性”这一主线：从 5 月引入 BuiltinDcMotorActuator/BuiltinPdActuator，到 11 月在部分重置间保留执行器延迟状态（dcdf6ce），再到本次在延迟位置执行器中保持 reset 后姿态，说明团队正系统性地补齐延迟执行器在 reset 场景下的状态语义，属于对既有演进方向的自然延伸而非偏离。该提交同时附带测试（tests/test_delayed_actuator.py）与 changelog 更新，符合仓库“以稳定性与可复现性为主线、性能优化为辅”的长期特征，也呼应了基线中提示的“执行器与重置语义改动可能引入训练可复现性偏差”的风险点——本次以测试固化行为，正是对该风险的正面回应。

## 🔍 关键更新解析

### 🚀 新功能/特性

无。

### ⚡️ 性能/架构优化

无。

### 🐛 Bug修复 / 其他

6/10-Hold the post-reset pose in delayed position actuators (#1308)（936f7a1）
  - 评分：6/10
  - 一句话总结：修复延迟位置执行器在 reset 后未能保持目标姿态的问题，使重置后的姿态与预期一致。
  - 链接：https://github.com/mujocolab/mjlab/commit/936f7a12537556416addff31babbb1512dd24d70
  - 变更规模：+45 -0
  - 提交者：Gijs de Jong
  - 解决的问题：延迟位置执行器在 episode reset 后姿态不一致，导致重置状态与预期目标偏离，影响训练/评测的可复现性与 reset 语义正确性。
  - 产品启示：执行器延迟与 reset 语义是仿真保真度的关键细节，应以测试（tests/test_delayed_actuator.py）固化行为并同步 changelog，降低后续执行器模型族扩展时的回归风险。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 160 条
- 高价值提交（≥6分）: 3 条
- 代码更新规模: +63413 / -35780 行
- 主要贡献者: Yuval Tassa, Matija Kecman, Michael Moss

## 🧭 趋势点评
本周三项高价值提交延续了仓库“内核数值稳定性 + 运行时健壮性 + 热点路径性能”三线并进的长期趋势：稀疏 Cholesky 超节点检测修复直接呼应 2026-10 以来对稀疏线性代数内核（b7fcf96、e3c0953）的密集优化，属于优化后的正确性补强；插件加载容错改造偏离了以往“失败即中止”的严格语义，转向更友好的生态集成策略，与 Studio/Web Viewer 平台化扩张方向一致；射线检测包围球剔除则延续了碰撞与查询管线（GJK/EPA、broadphase、NativeCCD）系统性提速的主线，并配套新增 benchmark，符合仓库“优化必带基准”的工程惯例。

## 🔍 关键更新解析

### 🚀 新功能/特性
6/10-Skip plugin libraries that fail to load in mj_loadAllPluginLibraries instead of aborting.（144ede9）
  - 评分：6/10
  - 一句话总结：`mj_loadAllPluginLibraries` 改为跳过加载失败的插件库而非直接中止，提升插件生态容错性。
  - 链接：https://github.com/google-deepmind/mujoco/commit/144ede9849c16844bac3a304eda0ddc54f92feac
  - 变更规模：+51 -43
  - 提交者：Matija Kecman
  - 解决的问题：此前任一插件库加载失败会导致整个批量加载流程中止，单个损坏或不兼容的插件即可阻断其余可用插件的注册。
  - 产品启示：降低第三方插件（Studio 插件、扩展库）接入门槛，利于生态扩张；但需在文档中明确失败插件的可观测性（日志/返回值），避免静默降级掩盖部署问题。

### ⚡️ 性能/架构优化
7/10-Cull non-SDF geoms by bounding sphere in mj_ray.（7b2ef80）
  - 评分：7/10
  - 一句话总结：`mj_ray` 对非 SDF 几何体增加包围球剔除，减少射线检测的无效精确求交。
  - 链接：https://github.com/google-deepmind/mujoco/commit/7b2ef804ae01b8bd62679ecda7eb0afdf73ad4f7
  - 变更规模：+371 -1
  - 提交者：Dmitry Nikulin
  - 解决的问题：射线查询对非 SDF 几何体缺少廉价的前置剔除，导致大量射线需进入昂贵的精确相交计算。
  - 产品启示：直接惠及传感器仿真（射线/测距）与大规模并行场景；新增 ray benchmark 与引擎测试为后续查询管线优化建立回归基线，符合仓库“优化配套基准”的实践。

### 🐛 Bug修复 / 其他
8/10-Fix supernode detection in sparse `mju_cholFactorNumeric`.（9ae9bad）
  - 评分：8/10
  - 一句话总结：修复稀疏 Cholesky 数值分解中的超节点检测错误，保障稀疏求解正确性。
  - 链接：https://github.com/google-deepmind/mujoco/commit/9ae9bad0100d586646ab69b7aef9050e63e2f878
  - 变更规模：+225 -97
  - 提交者：Yuval Tassa
  - 解决的问题：稀疏 `mju_cholFactorNumeric` 的超节点检测存在缺陷，可能在稀疏模型分解时产生错误的超节点划分，影响求解精度与稳定性。
  - 产品启示：该修复紧接 2026-10 稀疏 Cholesky 提速（b7fcf96）之后，说明性能重写后需强化数值正确性回归；对柔性体与稀疏 Newton 路径（8892bf4、0d8a109）的可靠性具有直接支撑作用，提示后续优化应持续配套收敛性与正确性测试。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 43 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +11748 / -8171 行
- 主要贡献者: isaaclab-bot[bot], Mustafa H, ooctipus

## 🧭 趋势点评
本周高价值提交延续了仓库“多后端并行演进 + 3.0 架构收敛 + 性能与精度守护”的长期主线，并进一步向纵深推进：一方面，Newton 后端从版本升级（1.9/MuJoCo 3.17）走向管理器重构（[2d/N]、[2d-ii/N]）与接触传感器迁移至求解器可观测项，配合跨后端共享传感器存储与能力，说明多后端抽象正从“可切换”迈向“统一数据与语义层”；另一方面，移除 3.1 计划废弃 API、以 OVStorage 替换 omni.client、修复 TF32 相机朝向精度问题，体现出 3.0 重构进入 API 收敛与正确性收尾阶段。整体与基线中“性能优化密集落地、后端注册表化、CI 与兼容性治理”的趋势高度一致，仅在个别提交上略微偏向清理与破坏性变更（API 移除、存储层替换），提示下游迁移成本需重点关注。

## 🔍 关键更新解析

### 🚀 新功能/特性
- 6/10-修复相机帧朝向转换中的 TF32 matmul 问题（1be7689）
  - 评分：6/10
  - 一句话总结：在相机帧朝向转换中规避 TF32 matmul，修复由此导致的相机朝向精度错误。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/1be7689096a718cdebcfcefad2e2cd5fe04dfdeb
  - 变更规模：+38 -57
  - 提交者：alexcastgonz
  - 解决的问题：TF32 低精度矩阵乘法在相机坐标系转换中引入数值误差，导致相机朝向计算不正确。
  - 产品启示：感知与相机管线的数值精度需显式治理，高保真渲染/感知场景应对精度敏感算子做精度隔离与回归测试。

### ⚡️ 性能/架构优化
- 7/10-[Core] 用 OVStorage 替换 omni.client 以访问远程资产（08eaa24）
  - 评分：7/10
  - 一句话总结：将远程资产访问从 omni.client 迁移至 OVStorage，统一存储访问路径。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/08eaa241f32e5d8c5824db1056d56ebd48a8a6cc
  - 变更规模：+467 -605
  - 提交者：Antoine RICHARD
  - 解决的问题：omni.client 作为远程资产访问依赖存在维护与一致性问题，需迁移到更统一的 OVStorage 抽象。
  - 产品启示：存储访问层抽象化有利于降低对单一 Omniverse 组件的耦合，但需同步更新许可证例外与文档，提示依赖治理要成体系。

- 6/10-将 Newton 接触传感器迁移至求解器可观测项（b0d88de）
  - 评分：6/10
  - 一句话总结：Newton 接触传感器改为从求解器可观测项读取，统一数据来源。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/b0d88de4e8440aa9c09a7bde81330a17fc0418fe
  - 变更规模：+176 -39
  - 提交者：ooctipus
  - 解决的问题：接触传感器此前独立采集数据，与求解器内部状态存在重复与不一致风险。
  - 产品启示：传感器数据应尽量复用求解器可观测输出，既降低开销又保证物理一致性，是后端统一语义层的关键一步。

- 7/10-升级 Newton 至 1.9、MuJoCo/MJWarp 至 3.17（bb4d991）
  - 评分：7/10
  - 一句话总结：同步升级 Newton 1.9 与 MuJoCo/MJWarp 3.17，跟进上游生态。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/bb4d9915f48e0529b6fc5c2982629aed0891b574
  - 变更规模：+71 -35
  - 提交者：ooctipus
  - 解决的问题：上游物理后端版本迭代带来新特性与修复，需保持依赖同步并更新渲染基准图。
  - 产品启示：高频版本跟进是多后端策略的必然成本，需配套 golden image 与回归测试以防行为漂移。

- 7/10-[Newton] 重构 Newton 管理器 [2d-ii/N]（0ff9d07）
  - 评分：7/10
  - 一句话总结：Newton 管理器重构第二阶段（ii），引入求解器实例化设计。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/0ff9d07521753d7e7e2f7175f8cba4bebd3bbee6
  - 变更规模：+311 -347
  - 提交者：Mustafa H
  - 解决的问题：原 Newton 管理器在求解器实例与可视化状态管理上耦合较重，需分阶段拆分。
  - 产品启示：管理器重构分阶段推进可降低风险，但下游扩展 Newton 求解器的开发者需同步适配新接口。

- 7/10-移除计划在 Isaac Lab 3.1 删除的 API（8a9e6eb）
  - 评分：7/10
  - 一句话总结：提前移除 3.1 计划废弃的 API，推进 API 收敛。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/8a9e6eba406bfeffb705464c2c39424d21294026
  - 变更规模：+66 -607
  - 提交者：Kelly Guo
  - 解决的问题：长期积累的废弃 API 增加维护负担与语义歧义，需按计划清理。
  - 产品启示：破坏性清理需配套迁移指南与 changelog 标注（major/removed），提示下游应尽早对齐 3.x API 基线。

- 7/10-[Newton] 重构 Newton 管理器 [2d/N]（b3ef9ce）
  - 评分：7/10
  - 一句话总结：Newton 管理器重构主阶段，引入捕获运行时（captured runtime）设计。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/b3ef9ce18ef640fe27fcd18c1527382897a94109
  - 变更规模：+506 -292
  - 提交者：Mustafa H
  - 解决的问题：Newton 管理器运行时状态与资产契约测试缺乏统一抽象，重构以明确运行时语义。
  - 产品启示：重构伴随契约测试（backends.py、runtime semantics）是保障多后端行为一致的有效手段。

- 8/10-跨后端共享传感器存储与能力（f644e1f）
  - 评分：8/10
  - 一句话总结：在 PhysX/Newton 等后端间共享传感器存储与能力抽象，大幅精简重复实现。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/f644e1f8f1103aa2c8c859aabd5eb877b3619484
  - 变更规模：+1081 -1693
  - 提交者：ooctipus
  - 解决的问题：各后端传感器数据存储与能力声明重复实现，导致行为差异与维护成本高。
  - 产品启示：以“能力拥有数据（capability-owned-data）”统一传感器层，是多后端可插拔架构的关键收敛点，显著降低新增后端的接入成本。

### 🐛 Bug修复 / 其他
- 6/10-修复任务空间动作项的 action clipping（0a02a29）
  - 评分：6/10
  - 一句话总结：修正任务空间动作项的裁剪逻辑，避免动作越界或裁剪错误。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/0a02a298dc759a8f771f2f8ec109ad10b4db0aa5
  - 变更规模：+323 -21
  - 提交者：Lynn
  - 解决的问题：任务空间动作项在裁剪时未正确处理边界，可能导致控制输出异常。
  - 产品启示：动作空间裁剪属于策略训练正确性基础环节，需覆盖配置层（actions_cfg）与管理器项配置的联动测试。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 29 条
- 高价值提交（≥6分）: 3 条
- 代码更新规模: +10280 / -537 行
- 主要贡献者: Eric Shi, Christopher Crouzet, Alain Denzler

## 🧭 趋势点评
本周高价值提交延续了仓库基线中“运行时/编译期性能与数值栈加固”的主线，但重心明显偏向**正确性与数值稳健性**：`wp.utils` CUDA 辅助函数的设备错配修复、内核内 `wp.zeros()` 原地清零语义修正，以及 FEM 块对角 Dirichlet 投影的新增，分别对应基线中“图/内存生命周期治理”“内建函数语义与代码生成”“稀疏/FEM 数值栈强化”三条演进方向。值得注意的是，本周未见直接的性能优化类提交，而是以修复底层语义缺陷和补齐 FEM 能力为主，这与基线中“优化触及 codegen、native 头文件易引入静默正确性回归”的风险判断相呼应——本周工作更像是在为后续性能与功能扩张清理地基，而非偏离长期趋势。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-Add in-place block-diagonal Dirichlet projection [GH-2118]（9e989f8）
  - 评分：7/10
  - 一句话总结：为 FEM 模块新增原地块对角 Dirichlet 投影能力，扩展约束处理路径。
  - 链接：https://github.com/NVIDIA/warp/commit/9e989f81e5a461c05f81a014a4105304c0bbe912
  - 变更规模：+503 -6
  - 提交者：Gilles Daviet
  - 解决的问题：此前 FEM 缺少块对角形式的 Dirichlet 边界条件投影支持，用户需自行拼装约束处理逻辑；该提交以原地方式实现投影，避免额外内存分配与数据拷贝。
  - 产品启示：直接强化基线中“稀疏与 FEM 数值栈”演进方向，配合已有的 block-Jacobi 预条件器与 CG/CR restart 支持，使 `warp.fem` 在需要刚性边界约束的仿真场景（如肌肉、软体）中更完整可用；原地语义也契合大规模仿真对内存占用的敏感需求。

### ⚡️ 性能/架构优化
- 本周无对应分类的高价值提交。

### 🐛 Bug修复 / 其他
6/10-Run wp.utils CUDA helpers on their arrays' device [GH-2262]（93e8027）
  - 评分：6/10
  - 一句话总结：修复 `wp.utils` 中 CUDA 辅助函数未在数组所属设备上执行的问题。
  - 链接：https://github.com/NVIDIA/warp/commit/93e80279a1c117a63a9d37bb79671511b0af6987
  - 变更规模：+332 -48
  - 提交者：Christopher Crouzet
  - 解决的问题：CUDA 辅助函数此前可能在错误设备上运行，导致多 GPU 或非默认设备场景下的设备错配错误；提交同时新增 `test_utils_device.py` 专项测试并纳入测试套件。
  - 产品启示：呼应基线中“图捕获与内存生命周期治理”和“多硬件池扩张”趋势，多设备正确性是 B200、RTX PRO 6000 等新硬件池与 ARM64 GPU CI 覆盖下的必要前提；新增专项测试也体现基线所述“CI 与回归信号体系趋于成熟”的工程纪律。

6/10-Zero-fill in-kernel wp.zeros() in place [GH-2214]（e505f13）
  - 评分：6/10
  - 一句话总结：修正内核内 `wp.zeros()` 的语义，使其在原地清零而非依赖旧有路径。
  - 链接：https://github.com/NVIDIA/warp/commit/e505f136824649cb83278ba3057f061aa161d141
  - 变更规模：+96 -25
  - 提交者：Alain Denzler
  - 解决的问题：内核内调用 `wp.zeros()` 时的清零行为与预期不一致，涉及 `builtins.py`、`codegen.py` 与 native `array.h` 的协同修改，属于基线中“内建函数语义与代码生成”层面的静默正确性缺陷。
  - 产品启示：正是基线风险提示中“优化触及 codegen 与 native 头文件易引入静默正确性回归”的典型修复案例；原地清零语义减少了内核内不必要的分配/拷贝路径，对强化学习与仿真中高频重置缓冲区的回路有实际收益，同时 `test_fixedarray.py` 的补充测试强化了回归护栏。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 13 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +18372 / -570 行
- 主要贡献者: Andy Lin, Hongzhi Zang, Chenghao-Yin

## 🧭 趋势点评
本周高价值提交延续了 RLinf 在基线中呈现的“功能扩张优先”主线，并进一步向真实世界与仿真生态两端同时加码：一方面通过 SO-101 真机采集与 OpenPI SFT 评测（1bf7898）把真机数据闭环落到具体硬件，另一方面密集接入 RoboDojo、GenieSim、Psi0+SIMPLE 等仿真环境与 PhyAI rollout 后端，使“多环境、多后端、多模型”的平台化定位更加清晰。同时，RoboTwin 对 AMD ROCm 的支持（3b35c5f）延续了基线中“国产/异构加速器适配矩阵扩张”的方向，与 Intel XPU、Biren、Kunlun 等适配形成呼应。值得注意的是，本周高价值提交全部为新功能类，未出现性能/架构优化或 Bug 修复类高价值项，这与基线中“性能/优化提交仅约 3.1%、修复类占比高但多为局部修补”的判断一致，说明项目仍处于以生态覆盖换取广度的阶段，系统性性能基准与回归治理尚未成为本周重点，后续多环境并行维护带来的测试矩阵与文档漂移风险需持续关注。

## 🔍 关键更新解析

### 🚀 新功能/特性

9/10-feat(embodiment): integrate Psi0 with SIMPLE (#1509)（cc6bd25）
  - 评分：9/10
  - 一句话总结：将 Psi0 VLA 模型与 SIMPLE 模拟器集成，打通模型与仿真环境的训练评测链路。
  - 链接：https://github.com/RLinf/RLinf/commit/cc6bd2588f2ef6e6e7e4da62c3fef96526a16cb1
  - 变更规模：+4103 -15
  - 提交者：Diddan2233
  - 解决的问题：Psi0 与 SIMPLE 此前各自独立，缺少端到端的模型-环境集成，用户无法直接在 SIMPLE 中训练/评测 Psi0。
  - 产品启示：模型与模拟器的成对集成是 VLA 平台的核心竞争力；建议将此类集成沉淀为标准“模型×环境”兼容矩阵，并纳入自动化回归，保障后续模型或环境升级不破坏组合可用性。

---

8/10-feat(realworld): add SO-101 collection and OpenPI SFT eval (#1749)（1bf7898）
  - 评分：8/10
  - 一句话总结：为 SO-101 机械臂新增真机数据采集与 OpenPI SFT 评测流程，并配套中英文文档与模型配置。
  - 链接：https://github.com/RLinf/RLinf/commit/1bf78980d9339cbc67497eddceb9a1e3a74e2acc
  - 变更规模：+2376 -111
  - 提交者：tuo3288
  - 解决的问题：此前真机能力集中在 Franka/Franky 等平台，缺少低成本 SO-101 的采集与 SFT 评测闭环，用户难以在轻量硬件上完成从数据采集到监督微调评测的全流程。
  - 产品启示：以低成本机械臂补齐真机数据入口，有助于扩大社区参与面；建议后续将 SO-101 采集数据格式与 replay buffer、DAgger 管线打通，形成可复用的真机数据资产标准。

8/10-feat(geniesim): add GenieSim training and evaluation (#1757)（a052a9a）
  - 评分：8/10
  - 一句话总结：新增 GenieSim 仿真环境的训练与评测支持，配套 Docker、文档与模拟器索引更新。
  - 链接：https://github.com/RLinf/RLinf/commit/a052a9ab1516cfa9a8dce7dfc04ed59651af0c9f
  - 变更规模：+4741 -1
  - 提交者：Chenghao-Yin
  - 解决的问题：平台缺少 GenieSim 这一仿真后端，用户在具身仿真选型与训练评测上少了一条可选路径。
  - 产品启示：单次提交即引入近 5k 行新环境代码，说明环境接入成本较高；建议抽象统一的环境适配接口与配置模板，降低后续新仿真器的接入边际成本。

8/10-feat(embodiment): add PhyAI rollout backend (#1587)（e2aeead）
  - 评分：8/10
  - 一句话总结：新增 PhyAI rollout 后端，并补充 rollout 引擎指南与 PPO 算法参考文档。
  - 链接：https://github.com/RLinf/RLinf/commit/e2aeeaddc09dbbdee179bde6bc6b03bb374e304b
  - 变更规模：+3291 -38
  - 提交者：Caspian Chen
  - 解决的问题：rollout 侧后端选择有限，缺少 PhyAI 这一执行后端，限制了不同物理仿真/执行链路的组合灵活性。
  - 产品启示：rollout 后端可插拔化是平台化的关键一步；建议明确各 rollout 后端的能力矩阵（支持环境、精度、并行方式），避免用户在多后端组合中试错。

7/10-feat(envs): add RoboDojo environment and evaluation (#1754)（46a39a9）
  - 评分：7/10
  - 一句话总结：新增 RoboDojo 仿真环境与评测支持，并纳入 embodied E2E 测试工作流与模拟器索引文档。
  - 链接：https://github.com/RLinf/RLinf/commit/46a39a96768cbb1807fde7f4216238d59640a1ae
  - 变更规模：+2014 -59
  - 提交者：qurakchin
  - 解决的问题：仿真环境生态缺少 RoboDojo 这一选项，用户在环境选型与横向评测时缺乏统一入口与 CI 覆盖。
  - 产品启示：将新环境直接接入 E2E 测试与模拟器索引，是把“环境接入”工程化的良好范式；建议同步补充该环境的资源占用与评测基线说明，避免文档与实现漂移。

6/10-feat(robotwin): support RoboTwin training on AMD ROCm GPUs (#1762)（3b35c5f）
  - 评分：6/10
  - 一句话总结：使 RoboTwin 训练可在 AMD ROCm GPU 上运行，并更新 Docker 镜像与中英文评测/示例文档。
  - 链接：https://github.com/RLinf/RLinf/commit/3b35c5f344d46ab139ca9dd1ebd2780e03101160
  - 变更规模：+670 -7
  - 提交者：Vivicai1005
  - 解决的问题：RoboTwin 训练此前主要面向 NVIDIA 生态，AMD ROCm 用户缺少可用的训练路径与镜像支持。
  - 产品启示：异构加速器适配矩阵继续扩张，有利于覆盖更多算力环境；但 ROCm 路径的 CI 覆盖与性能基线需同步建立，否则易形成“可跑但不可比”的碎片化支持。

