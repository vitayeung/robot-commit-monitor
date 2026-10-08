# 具身智能周报 (2026年10月08日 12:42:36)

## 行业风向总览

# 具身智能行业风向周度总结（5仓库）

**技术焦点：从功能扩张转向稳定性收敛。** 本周五个仓库共同呈现“深水区打磨”特征：mjlab 全部高价值提交集中于速度命令与延迟缓冲的时序/状态一致性修复；mujoco 在 CG 求解器引入稠密分块预条件（9分）并修复 GJK 见证点、执行器继承语义；IsaacLab 修复 ANYmal 对称增强在非 PhysX 后端的关节顺序问题；Warp 修复 eig3 梯度、tile_map 伴随梯度等自动微分正确性缺陷；RLinf 修复调度器并发建组中止。多后端一致性（Newton/Kamino）、可微分正确性、并发调度稳定性成为共性风险点。

**合成数据动态：** 本周无直接合成数据管线更新，但域随机化基础设施持续加固——mjlab 修复 DelayBuffer 在部分重置、共享 lag、首步采样下的语义漂移，直接决定观测延迟随机化的训练效果；mujoco 修复 autoreset 关闭时警告重复计数，提升随机化诊断可信度。这些是合成数据质量与可复现性的底层保障。

**产品经理关注信号：** ①命令生成、奖励累积、延迟缓冲等模块的“重置契约”需显式定义，否则跨 episode 状态泄漏会扭曲训练信号；②多物理后端切换时任务层逻辑（如对称增强）存在隐性错误风险，选型需配套回归测试；③Warp 新增 NumPy dtype 与 CPU LLVM 编译选项，跨平台部署与生态互操作门槛降低；④RLinf 并发建组中止提示分布式训练启动路径仍是稳定性短板，需加强压力测试。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 8 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +400 / -36 行
- 主要贡献者: Kevin Zakka, vssingh, 상티 (윤상현)

## 🧭 趋势点评
本周更新延续了仓库近期“稳定性收敛”的主线，全部 6 条高价值提交均归入 Bug修复/其他 类别，且高度集中在速度命令语义（velocity_command）与延迟缓冲（DelayBuffer）两大模块，与 2026-10 基线中“聚焦命令与延迟缓冲语义修正”的方向完全一致。值得注意的是，本周修复呈现出明显的“时序与状态一致性”特征——无论是 init_velocity_prob 前的规则应用顺序、rel_forward_envs 的覆盖保护，还是 DelayBuffer 在部分重置、共享 lag、首次采样等边界场景下的行为，都指向同一类系统性风险：多环境并行与部分重置下的状态语义漂移。这偏离了 4-6 月以新功能（执行器封装、域随机化、MeshCfg/GeomCfg）为主的扩张节奏，说明项目已进入对既有复杂机制（命令生成、观测延迟）的深度打磨期，测试文件（test_velocity_command、test_delay_buffer、test_velocity_rewards）的同步更新也反映出对回归防护的重视。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周无此类提交）

### ⚡️ 性能/架构优化
（本周无此类提交）

### 🐛 Bug修复 / 其他

7/10-Apply standing, heading and world-frame rules before init_velocity_prob (#1215)（bd37751）
  - 评分：7/10
  - 一句话总结：将站立、朝向与世界坐标系规则的应用时机提前到 init_velocity_prob 之前，修正速度命令初始化顺序。
  - 链接：https://github.com/mujocolab/mjlab/commit/bd37751b15af90863c5a84cbbc24653a4edd985c
  - 变更规模：+88 -17
  - 提交者：Kevin Zakka
  - 解决的问题：此前 init_velocity_prob 在规则应用前执行，导致初始化概率逻辑与站立/朝向/世界坐标系规则产生顺序错位，命令生成结果不符合预期。
  - 产品启示：命令生成管线中的执行顺序是隐式契约，需通过显式排序与测试固化，避免后续插入新逻辑时再次破坏语义。

7/10-Keep the shared DelayBuffer lag and schedule across partial resets. (#1206)（4f73291）
  - 评分：7/10
  - 一句话总结：在部分重置场景下保持共享 DelayBuffer 的 lag 与调度一致。
  - 链接：https://github.com/mujocolab/mjlab/commit/4f7329183f097baa93af6e21e7e9241fc45bf978
  - 变更规模：+34 -4
  - 提交者：Kevin Zakka
  - 解决的问题：部分重置（partial reset）会破坏共享 DelayBuffer 的 lag 与调度状态，导致观测延迟在不同环境间不一致。
  - 产品启示：共享状态组件在部分重置语义下必须显式定义“保留什么、重置什么”，否则并行环境间会出现难以复现的观测偏差。

6/10-Stop heading and world frame commands from overriding rel_forward_envs (#1214)（c5adfae）
  - 评分：6/10
  - 一句话总结：阻止朝向与世界坐标系命令覆盖 rel_forward_envs 的配置。
  - 链接：https://github.com/mujocolab/mjlab/commit/c5adfae3a61fe2c81e4b84d066da8f0c80faf7a2
  - 变更规模：+48 -0
  - 提交者：vssingh
  - 解决的问题：heading 与世界坐标系命令会意外覆盖 rel_forward_envs 的设置，导致部分环境的速度命令语义被错误改写。
  - 产品启示：多模式命令共存时需明确优先级与互斥边界，防止某一模式的全局规则污染其他模式的局部配置。

6/10-Share the hold decision across envs in shared-lag DelayBuffer (#1191)（58ad841）
  - 评分：6/10
  - 一句话总结：在共享 lag 的 DelayBuffer 中跨环境共享 hold 决策。
  - 链接：https://github.com/mujocolab/mjlab/commit/58ad84162acb91b7dac3dfbc4ba646b74c009431
  - 变更规模：+45 -8
  - 提交者：상티 (윤상현)
  - 解决的问题：共享 lag 模式下各环境独立做出 hold 决策，导致延迟行为不一致，破坏了共享缓冲的语义一致性。
  - 产品启示：共享缓冲的“共享”应贯穿决策层而非仅数据层，否则名义共享、实际分裂，会削弱延迟随机化的训练效果。

6/10-Sample DelayBuffer lags on the first step after creation or reset (#1203)（fb32300）
  - 评分：6/10
  - 一句话总结：在创建或重置后的第一步即采样 DelayBuffer 的 lag。
  - 链接：https://github.com/mujocolab/mjlab/commit/fb32300d93042695452bdce8bdab86eff840bad5
  - 变更规模：+48 -2
  - 提交者：Edson
  - 解决的问题：DelayBuffer 在创建或重置后的首步未及时采样 lag，导致初始阶段延迟行为缺失或使用陈旧值。
  - 产品启示：随机化组件的采样时机需与生命周期严格对齐，首步遗漏会系统性削弱域随机化在 episode 早期的覆盖。

6/10-Clear feet_swing_height peak_heights on environment reset (#1205)（e52098a）
  - 评分：6/10
  - 一句话总结：在环境重置时清空 feet_swing_height 的 peak_heights 状态。
  - 链接：https://github.com/mujocolab/mjlab/commit/e52098a48630485e07f97e17d735407efb103b36
  - 变更规模：+74 -3
  - 提交者：vssingh
  - 解决的问题：环境重置后 feet_swing_height 奖励的 peak_heights 未清零，残留上一 episode 的峰值导致奖励计算被污染。
  - 产品启示：奖励函数中的跨步累积状态必须纳入重置契约，否则会引入跨 episode 的状态泄漏，扭曲训练信号。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 115 条
- 高价值提交（≥6分）: 8 条
- 代码更新规模: +33070 / -7436 行
- 主要贡献者: Yuval Tassa, Michael Moss, Alessio Quaglino

## 🧭 趋势点评
本周更新延续了仓库“引擎数值内核持续提速 + 模型编辑/API 语义精修 + 碰撞稳定性修复”的长期主线：CG 求解器引入稠密分块预条件（ad127e8）直接呼应过去数月对求解器精度与速度的常态化投入，而 GJK 见证点交换与低容差距离保留（dcdfe84、ed357ff）则延续了碰撞管线在边界与退化情形上的鲁棒性打磨。与此同时，执行器快捷标签的保存与继承规则修正（d4595d0、ab7f005、fcb83a1）以及附着 skin/tendon/mesh 名称材质修复（3a35e77）表明模型编辑与 mjSpec/XML 语义一致性正成为与性能并行的另一重心，这与基线中“模型编辑与 API 演进”方向高度吻合。整体看，本周未偏离长期趋势，而是在求解器预条件、碰撞数值稳定与模型语义正确性三个既有方向上继续深化。

## 🔍 关键更新解析

### 🚀 新功能/特性
6/10-Save actuators and actuator defaults with their shortcut tags.（d4595d0）
  - 评分：6/10
  - 一句话总结：支持执行器及其默认值随快捷标签一并保存，完善模型序列化语义。
  - 链接：https://github.com/google-deepmind/mujoco/commit/d4595d020ad50a4e3f4f85918878f5ae42a22829
  - 变更规模：+1251 -396
  - 提交者：Yuval Tassa
  - 解决的问题：此前执行器快捷标签在保存时未被保留，导致模型往返读写后丢失快捷方式信息。
  - 产品启示：提升 MJCF/模型编辑的往返一致性，降低用户因保存丢失配置而重复配置的成本。
6/10-Actuators with fixed or affine gain declare what their control is, and saved models keep it.（fcb83a1）
  - 评分：6/10
  - 一句话总结：固定或仿射增益的执行器显式声明其控制类型并在保存后保留。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fcb83a1736e9eb6aa5818d00bc7c596365970ea9
  - 变更规模：+330 -69
  - 提交者：Yuval Tassa
  - 解决的问题：执行器控制语义在固定/仿射增益下不明确，且保存后无法保留该声明。
  - 产品启示：增强执行器语义可解释性与模型可移植性，利于下游绑定与 MJX/mujoco_warp 一致性。

### ⚡️ 性能/架构优化
9/10-Precondition the non-flex dofs with dense per-component blocks in the CG solver.（ad127e8）
  - 评分：9/10
  - 一句话总结：在 CG 求解器中对非 flex 自由度采用稠密逐分量块预条件，加速收敛。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ad127e886fd07f860f5f62259f7be6f9d5d95546
  - 变更规模：+1035 -50
  - 提交者：Alessio Quaglino
  - 解决的问题：CG 求解器在非 flex 自由度上缺乏有效预条件，收敛速度受限。
  - 产品启示：直接提升大规模仿真与强化学习训练的求解吞吐，延续求解器数值内核提速主线。

### 🐛 Bug修复 / 其他
6/10-Fix warning double-counting when autoreset is disabled.（03b1594）
  - 评分：6/10
  - 一句话总结：修复禁用自动重置时警告被重复计数的问题。
  - 链接：https://github.com/google-deepmind/mujoco/commit/03b15943bce177431ead94db7ca7b09c2baa1644
  - 变更规模：+52 -8
  - 提交者：Yuval Tassa
  - 解决的问题：autoreset 关闭场景下警告重复计数，干扰诊断信息准确性。
  - 产品启示：提升引擎告警可信度，避免用户被误导性重复警告干扰调试。
6/10-Actuator shortcuts inherit their parameters from a default written with the same shortcut or with general, not from another shortcut.（ab7f005）
  - 评分：6/10
  - 一句话总结：修正执行器快捷参数继承规则，仅从同快捷或 general 默认继承。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ab7f005c91fc8798a05d18a9a0a6664f37ebbef1
  - 变更规模：+620 -137
  - 提交者：Yuval Tassa
  - 解决的问题：执行器快捷参数错误地从其他快捷方式继承，导致默认值语义混乱。
  - 产品启示：明确模型默认值继承语义，减少用户因隐式继承产生的建模错误。
6/10-Fix witness points swapping in edge collision when polygonClip return 0 witness points in multicontact. Fixes #3654.（dcdfe84）
  - 评分：6/10
  - 一句话总结：修复 multicontact 中 polygonClip 返回 0 见证点时边碰撞见证点交换问题。
  - 链接：https://github.com/google-deepmind/mujoco/commit/dcdfe84a48ed14394df36ad17828b85a45a55eaf
  - 变更规模：+71 -42
  - 提交者：Kyle Bayes
  - 解决的问题：多接触边碰撞在特定裁剪情形下见证点顺序错乱（issue #3654）。
  - 产品启示：提升接触求解输入的正确性，间接改善碰撞响应与仿真稳定性。
6/10-Fix the names and materials of attached skins, tendons and meshes, and deletion in a compiled spec.（3a35e77）
  - 评分：6/10
  - 一句话总结：修复编译 spec 中附着 skin/tendon/mesh 的名称、材质及删除行为。
  - 链接：https://github.com/google-deepmind/mujoco/commit/3a35e7712982e36b92724d7208d50cb486abb41d
  - 变更规模：+163 -2
  - 提交者：Yuval Tassa
  - 解决的问题：附着对象的名称与材质在编译 spec 中不正确，且删除操作存在缺陷。
  - 产品启示：提升模型编辑 API 的可靠性，保障可视化与资产引用的一致性。
6/10-Preserve GJK distance and witnesses on distance queries below ccd_tolerance.（ed357ff）
  - 评分：6/10
  - 一句话总结：在低于 ccd_tolerance 的距离查询中保留 GJK 距离与见证点。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ed357ff8c887dd92caeb46829ea2b1c4d8092f68
  - 变更规模：+48 -16
  - 提交者：Yuval Tassa
  - 解决的问题：距离低于 ccd_tolerance 时 GJK 距离与见证点被丢弃，影响接触精度。
  - 产品启示：增强碰撞检测在临界距离下的数值稳定性，延续碰撞管线鲁棒性打磨方向。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 90 条
- 高价值提交（≥6分）: 2 条
- 代码更新规模: +28226 / -44762 行
- 主要贡献者: Mustafa H, Antoine RICHARD, Zeng Qingcheng

## 🧭 趋势点评
本周的两项高价值更新延续了仓库近期“多后端并行演进 + 核心路径稳定性攻坚”的主线：一方面，ANYmal 对称增强针对非 PhysX 关节顺序的修复，呼应了基线中 Newton/Kamino 等多物理后端扩展带来的行为一致性与回归面扩大的风险，属于在多后端抽象推进过程中补齐任务层正确性的典型动作；另一方面，OVRTX 相机产物与场景光照的共享，直接承接了 2026-09 相机任务与观测管线大规模提速、以及异步渲染路径（ovrtx）引入的趋势，将优化从“减少核启动与主机同步”进一步推进到“跨相机复用渲染产物与光照资源”的架构层面。整体看，本周更新并未偏离长期方向，而是沿着渲染/相机提速与多后端一致性两条主线继续深化，且均带有 changelog 片段，符合仓库规范化发布节奏。

## 🔍 关键更新解析

### 🚀 新功能/特性
- 7/10-Share OVRTX camera products and scene lighting (#8319)（912a294）
  - 评分：7
  - 一句话总结：在 OVRTX 渲染路径中共享相机渲染产物与场景光照，减少重复渲染开销。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/912a2942cb70bf04349609e8b3f5d3d4c3084a62
  - 变更规模：+325 -316
  - 提交者：ooctipus
  - 解决的问题：多相机场景下 OVRTX 相机产物与场景光照被重复构建/渲染，造成资源浪费与性能开销。
  - 产品启示：为多相机感知与训练场景提供更高效的渲染复用机制，强化 OVRTX 异步渲染路径的可用性，是渲染后端解耦与相机管线提速的重要一步。

### ⚡️ 性能/架构优化
- 无

### 🐛 Bug修复 / 其他
6/10-Fix ANYmal symmetry augmentation for non-PhysX joint orders (#8205)（abe7db4）
  - 评分：6
  - 一句话总结：修复 ANYmal 对称增强在非 PhysX 关节顺序下的错误行为。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/abe7db4f38174a8ed4e4f843b28d6fe68f34b578
  - 变更规模：+110 -48
  - 提交者：Zeng Qingcheng
  - 解决的问题：ANYmal 对称增强逻辑依赖 PhysX 关节顺序，在 Newton/Kamino 等非 PhysX 后端下关节顺序不同导致增强结果错误。
  - 产品启示：保障多物理后端下任务层增强逻辑的一致性，降低下游用户切换后端时的隐性错误风险，并配套测试用例防止回归。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 21 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +2784 / -699 行
- 主要贡献者: Eric Shi, Nicolas Capens, songyinggoh

## 🧭 趋势点评
本周更新延续了 Warp 在“性能与正确性并重、工程化持续加深”的长期主线：一方面通过限制 SAH BVH 深度、支持 CPU LLVM 编译选项等提交，继续强化编译期与运行时基础设施的可控性，呼应了基线中“编译期与代码生成路径持续提速”“CUDA/LLVM 工具链与后端可移植性扩展”的预测方向；另一方面，eig3 梯度、捕获值属性访问、tile_map 伴随梯度等修复，精准落在基线指出的“数值精度与可微分正确性”以及“图捕获与内存管理”两大高风险领域，说明自动微分与代码生成路径仍是缺陷高发区。新增 NumPy dtype 支持则延续了与 Python 数值生态互操作的演进趋势。整体看，本周提交量虽少但质量集中，未偏离仓库长期轨迹，反而在数值正确性与后端可配置性上做了针对性加固。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-Add NumPy dtype support for Warp scalars (GH-2038)（b5ea466）
  - 评分：7/10
  - 一句话总结：为 Warp 标量类型新增 NumPy dtype 支持，打通与 NumPy 数值生态的类型互操作。
  - 链接：https://github.com/NVIDIA/warp/commit/b5ea46659b86efb8f1b511904a3b5c254cd13d70
  - 变更规模：+217 -7
  - 提交者：Nicolas Capens
  - 解决的问题：此前 Warp 标量与 NumPy dtype 之间缺乏直接映射，用户在数组互操作与类型转换时需手动适配，增加了使用成本。
  - 产品启示：强化了 Warp 作为 Python 数值计算生态一员的兼容性，降低用户从 NumPy 迁移或混合使用的门槛，有利于吸引更广泛的科学计算用户群。

- 7/10-Support CPU LLVM compiler options (GH-2004)（1411ff5）
  - 评分：7/10
  - 一句话总结：为 CPU 后端新增 LLVM 编译选项支持，允许用户自定义 CPU 编译行为。
  - 链接：https://github.com/NVIDIA/warp/commit/1411ff5d3694e34ffb694c1d6881a8588b77c897
  - 变更规模：+421 -19
  - 提交者：Nicolas Capens
  - 解决的问题：此前 CPU 后端编译选项不可配置，用户无法针对特定 CPU 架构或优化需求调整编译参数，限制了 CPU 路径的性能调优空间。
  - 产品启示：提升了 CPU 后端的可移植性与可调优性，配合基线中 LLVM 22 支持、Windows on Arm CUDA 等方向，表明多平台后端覆盖正持续加强，为跨平台部署提供更细粒度控制。

### ⚡️ 性能/架构优化
（本周无符合评分≥6 的性能/架构优化类提交）

### 🐛 Bug修复 / 其他
7/10-Fix eig3 eigenvalue-only gradients [GH-2010]（109b6fa）
  - 评分：7/10
  - 一句话总结：修复 eig3 在仅需特征值时的梯度计算错误，保证自动微分正确性。
  - 链接：https://github.com/NVIDIA/warp/commit/109b6fa2a22680fb129580cb3bbb1b6bb26721a5
  - 变更规模：+178 -5
  - 提交者：Eric Shi
  - 解决的问题：eig3 在仅计算特征值梯度时存在错误，导致依赖该分解的可微分仿真或优化流程产生不正确的梯度，影响训练收敛与结果可信度。
  - 产品启示：直接关系到可微物理与基于梯度的优化场景的正确性，是 Warp 作为可微分仿真平台的核心能力保障，凸显数值精度与自动微分正确性仍是重点投入方向。

6/10-Cap SAH BVH depth [GH-1991]（416985f）
  - 评分：6/10
  - 一句话总结：对 SAH BVH 构建深度施加上限约束，防止过深递归导致的栈溢出风险。
  - 链接：https://github.com/NVIDIA/warp/commit/416985fed1f214c71c7f29ca6013a222b574549c
  - 变更规模：+130 -3
  - 提交者：Eric Shi
  - 解决的问题：SAH BVH 在特定几何分布下可能构建出过深的树结构，引发栈溢出或遍历性能退化，影响网格射线查询的稳定性。
  - 产品启示：提升了 BVH 构建在极端场景下的鲁棒性，配合基线中 mesh ray BVH 遍历优化，表明空间查询路径在性能与稳定性上同步加固，有利于大规模仿真场景的可靠性。

6/10-Fix attribute access on captured values [GH-2023]（5ccf0e6）
  - 评分：6/10
  - 一句话总结：修复代码生成中对捕获值进行属性访问时的错误，保证闭包捕获语义正确。
  - 链接：https://github.com/NVIDIA/warp/commit/5ccf0e6222c8afa28a50a0fd2b2fd662fc30b261
  - 变更规模：+173 -1
  - 提交者：Gilles Daviet
  - 解决的问题：在 kernel 中访问被捕获对象的属性时，代码生成路径存在缺陷，导致编译错误或运行时行为异常，影响用户使用闭包捕获复杂对象的场景。
  - 产品启示：提升了代码生成路径对 Python 语义的还原度，降低用户编写复杂 kernel 时的踩坑概率，是开发者体验与语言表达能力的重要补强。

6/10-Fix tile_map adjoints that need the result (GH-2031)（67bce43）
  - 评分：6/10
  - 一句话总结：修复 tile_map 在伴随计算中需要结果值时的梯度错误，保证 tile 操作的自动微分正确。
  - 链接：https://github.com/NVIDIA/warp/commit/67bce43490f596e737e79080161c33730eaf53ae
  - 变更规模：+101 -2
  - 提交者：songyinggoh
  - 解决的问题：tile_map 的伴随（adjoint）在需要前向结果参与反向计算时存在缺陷，导致 tile 级别操作的梯度不正确，影响依赖 tile 编程的可微分内核。
  - 产品启示：tile 编程是 Warp 面向高性能 GPU 计算的重要抽象，其自动微分正确性直接决定可微分 tile 算法的可用性，该修复巩固了 Warp 在细粒度并行可微计算上的能力。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 3 条
- 高价值提交（≥6分）: 1 条
- 代码更新规模: +383 / -302 行
- 主要贡献者: Andy Lin, Ruslan Rakhimov, cyanseek

## 🧭 趋势点评
本周唯一的高价值提交聚焦于调度器并发组创建的中止问题修复，延续了仓库在 2026-09 至 2026-10 期间“工程化收敛与稳定性治理”的主线趋势——即在功能与模型支持面快速扩张之后，回头修补并发调度、集合通信等基础设施层的长尾缺陷。该提交同时补充了中英文 FAQ 文档与单元测试，呼应了仓库近期强化 AGENTS.md 规则、DCO、lint/test 命令等工程规范的走向，属于典型的“修复+文档+测试”三位一体收敛动作，而非新功能扩张，与整体“功能驱动、性能优化占比偏低”的长期特征保持一致。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周无符合条件的新功能/特性类提交）

### ⚡️ 性能/架构优化
（本周无符合条件的性能/架构优化类提交）

### 🐛 Bug修复 / 其他
7/10-fix(scheduler): avoid aborts in concurrent group creation (#1645)（c70606f）
  - 评分：7/10
  - 一句话总结：修复调度器在并发创建通信组时可能被中止的问题，并补充 FAQ 文档与单元测试。
  - 链接：https://github.com/RLinf/RLinf/commit/c70606f08cdca259b8dec03d4430926b5b8fac9d
  - 变更规模：+232 -24
  - 提交者：cyanseek
  - 解决的问题：并发场景下多个通信组同时创建时会触发中止（abort），影响多通道 process group 的稳定建立，进而可能中断分布式训练任务的启动与集合通信初始化。
  - 产品启示：并发组创建是分布式训练启动的关键路径，此类中止问题会直接放大为任务级失败；本次同步更新中英文 FAQ 与单元测试，说明团队正将并发调度类缺陷纳入可复现、可回归的治理流程，建议后续持续加强 multi_channel_pg 相关的并发压力测试与超时/中止路径覆盖。

---

