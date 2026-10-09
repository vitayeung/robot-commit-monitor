# 具身智能周报 (2026年10月08日 12:37:09)

- 统计窗口: 2026-09-30 14:19:31 +0800 至 2026-10-08 12:37:09 +0800（左闭右开）

## 行业风向总览

# 具身智能行业风向周度总结

**技术焦点：仿真内核提速与语义收敛并行。** MuJoCo 为 CG 求解器引入稠密分块预条件（+1035行），延续求解器性能常态化投入；同时密集修复执行器快捷标签继承与控制类型声明，推动 MJCF 模型语义规范化。Warp 本周 10 项高价值提交聚焦数值正确性——修复 eig3 梯度、tile 归约初始化、tile_map 伴随等自动微分缺陷，并新增 CPU LLVM 编译选项与 NumPy dtype 互操作，可微分仿真精度成为重点。IsaacLab 推进 OVRTX 相机产品与场景光照共享，渲染后端解耦持续深化。

**合成数据动态：** 本周无直接合成数据管线更新，但 mjlab 对 DelayBuffer 时序一致性的系列修复（部分重置保持 lag、首步采样、跨环境共享 hold 决策）实质影响观测延迟语义，对依赖延迟观测的 sim-to-real 策略训练与数据回放质量有间接支撑。

**产品经理关注信号：** ①多后端兼容性风险显性化——IsaacLab 修复 ANYmal 对称增强在非 PhysX 关节顺序下的错误，提示关节顺序等后端假设需显式解耦；②命令系统优先级规则需产品化——mjlab 修复 heading/世界坐标系命令覆盖相对前向语义，建议配置层增加冲突校验；③分布式训练稳定性制度化——RLinf 修复并发通信组创建中止并配套 FAQ 与单测，长时训练鲁棒性成工程标配。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 8 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +400 / -36 行
- 主要贡献者: Kevin Zakka, vssingh, 상티 (윤상현)

## 🧭 趋势点评
本周的更新延续了仓库在 2026-10 期间的核心主线——围绕速度命令语义与延迟缓冲（DelayBuffer）时序一致性进行密集的 Bug 修复，这与基线中“2026-10 聚焦命令与延迟缓冲语义修正”的判断高度吻合。具体来看，本周提交集中在 `velocity_command.py` 与 `delay_buffer.py` 两个模块，分别修正了站立/朝向/世界坐标系规则在 `init_velocity_prob` 之前的应用顺序、防止 heading 与世界坐标系命令覆盖 `rel_forward_envs`，以及 DelayBuffer 在部分重置、共享 lag 保持决策和首次采样时机上的一致性缺陷。这些修复并非新功能扩张，而是对既有观测/命令/延迟机制的边界条件打磨，反映出项目在功能快速迭代后正进入语义收敛与正确性加固阶段。值得注意的是，本周所有高价值提交均归类为 Bug修复/其他，未出现新功能或性能优化类提交，这与基线中“2026-10 仅 8 条提交且全部归入其他类”的观察一致，说明近期活动强度与分类粒度有所下降，但修复质量与针对性较强，集中在命令初始化顺序与延迟缓冲状态机这两个对训练稳定性影响较大的环节。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周无新功能/特性类提交）

### ⚡️ 性能/架构优化
（本周无性能/架构优化类提交）

### 🐛 Bug修复 / 其他

7/10-Apply standing, heading and world-frame rules before init_velocity_prob (#1215)（bd37751）
  - 评分：7/10
  - 一句话总结：修正速度命令初始化顺序，确保站立、朝向与世界坐标系规则在 `init_velocity_prob` 之前应用。
  - 链接：https://github.com/mujocolab/mjlab/commit/bd37751b15af90863c5a84cbbc24653a4edd985c
  - 变更规模：+88 -17
  - 提交者：Kevin Zakka
  - 解决的问题：此前站立、朝向与世界坐标系规则可能在 `init_velocity_prob` 之后才应用，导致初始速度命令的概率初始化与坐标系规则产生顺序错乱，影响速度任务训练初期的命令语义正确性。
  - 产品启示：命令生成流程中的规则应用顺序对训练稳定性有实质影响，应在 API 或文档中明确各规则的执行时序，避免用户在自定义任务时因顺序假设错误而引入难以排查的训练偏差。

7/10-Keep the shared DelayBuffer lag and schedule across partial resets. (#1206)（4f73291）
  - 评分：7/10
  - 一句话总结：在部分重置间保持共享 DelayBuffer 的 lag 与调度一致。
  - 链接：https://github.com/mujocolab/mjlab/commit/4f7329183f097baa93af6e21e7e9241fc45bf978
  - 变更规模：+34 -4
  - 提交者：Kevin Zakka
  - 解决的问题：部分重置（partial reset）时共享 DelayBuffer 的 lag 与调度状态未保持一致，导致观测延迟语义在重置后出现偏差，影响依赖延迟观测的策略训练。
  - 产品启示：延迟缓冲作为观测管理器的关键组件，其状态在重置语义下必须明确定义；建议在文档中补充部分重置对延迟状态的影响说明，并提供测试用例作为回归防护。

6/10-Stop heading and world frame commands from overriding rel_forward_envs (#1214)（c5adfae）
  - 评分：6/10
  - 一句话总结：防止 heading 与世界坐标系命令覆盖 `rel_forward_envs` 的相对前向语义。
  - 链接：https://github.com/mujocolab/mjlab/commit/c5adfae3a61fe2c81e4b84d066da8f0c80faf7a2
  - 变更规模：+48 -0
  - 提交者：vssingh
  - 解决的问题：当同时使用 heading 或世界坐标系命令与 `rel_forward_envs` 时，前者会错误覆盖后者的相对前向命令，导致速度任务中相对前向控制失效。
  - 产品启示：多命令模式共存时需要明确的优先级与互斥规则，建议在配置层面对冲突的命令组合进行校验或告警，降低用户误配置风险。

6/10-Share the hold decision across envs in shared-lag DelayBuffer (#1191)（58ad841）
  - 评分：6/10
  - 一句话总结：在共享 lag 的 DelayBuffer 中跨环境共享 hold 决策。
  - 链接：https://github.com/mujocolab/mjlab/commit/58ad84162acb91b7dac3dfbc4ba646b74c009431
  - 变更规模：+45 -8
  - 提交者：상티 (윤상현)
  - 解决的问题：共享 lag 模式下各环境的 hold 决策未统一，导致同一延迟配置在不同环境间行为不一致，破坏批量训练中的延迟语义一致性。
  - 产品启示：共享延迟配置应保证跨环境行为一致，建议在 DelayBuffer 的设计中明确“共享”与“独立”两种模式的语义边界，避免用户对共享范围产生误解。

6/10-Sample DelayBuffer lags on the first step after creation or reset (#1203)（fb32300）
  - 评分：6/10
  - 一句话总结：修复 DelayBuffer 在创建或重置后首步未采样 lag 的问题。
  - 链接：https://github.com/mujocolab/mjlab/commit/fb32300d93042695452bdce8bdab86eff840bad5
  - 变更规模：+48 -2
  - 提交者：Edson
  - 解决的问题：DelayBuffer 在创建或重置后的第一步未进行 lag 采样，导致初始阶段的延迟行为与后续步骤不一致，可能引入训练早期的观测时序偏差。
  - 产品启示：延迟缓冲的初始化语义应与稳态行为对齐，建议在缓冲区生命周期文档中明确“创建/重置后首步”的行为约定，并纳入单元测试覆盖。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 126 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +35185 / -7957 行
- 主要贡献者: Yuval Tassa, Michael Moss, Alessio Quaglino

## 🧭 趋势点评
本周高价值提交延续了仓库“引擎数值内核持续提速 + 模型语义/API 精细化”的双主线：一方面，CG 求解器引入稠密分块预条件（ad127e8）直接呼应过去数月围绕 PGS/CG 求解器精度与速度的连续优化（如 Nesterov 动量、线搜索重构），属于求解器性能投入的进一步深化；另一方面，执行器快捷标签保存与继承、控制类型声明（d4595d0、ab7f005、fcb83a1）则偏离了纯性能叙事，转向 MJCF/模型语义与 API 表达力的精细化，体现出项目在高速数值迭代之外，开始系统性收敛模型定义与序列化行为的一致性。同时，mujoco_warp 的同步导入（ff70616）延续了 MJX/Warp 生态集成与依赖同步的长期节奏，整体呈现“内核提速 + 语义规范 + 生态同步”并行推进的格局。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-Precondition the non-flex dofs with dense per-component blocks in the CG solver.（ad127e8）
  - 一句话总结：为 CG 求解器引入按组件稠密块的预条件，提升非 flex 自由度的求解收敛效率。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ad127e886fd07f860f5f62259f7be6f9d5d95546
  - 变更规模：+1035 -50
  - 提交者：Alessio Quaglino
  - 解决的问题：原有 CG 求解器在非 flex 自由度上缺乏针对性的预条件，收敛速度受限。
  - 产品启示：强化学习训练与大规模仿真中约束求解吞吐有望提升，需关注数值稳定性回归测试。

6/10-Save actuators and actuator defaults with their shortcut tags.（d4595d0）
  - 一句话总结：执行器及其默认值在保存时携带快捷标签，保证模型往返序列化语义一致。
  - 链接：https://github.com/google-deepmind/mujoco/commit/d4595d020ad50a4e3f4f85918878f5ae42a22829
  - 变更规模：+1251 -396
  - 提交者：Yuval Tassa
  - 解决的问题：执行器快捷标签在保存/加载过程中丢失，导致模型语义不一致。
  - 产品启示：提升 MJCF 模型可移植性与可复现性，利好模型共享与工具链集成。

6/10-Actuator shortcuts inherit their parameters from a default written with the same shortcut or with general, not from another shortcut.（ab7f005）
  - 一句话总结：明确执行器快捷参数继承规则，仅从同快捷或 general 默认继承，避免跨快捷误继承。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ab7f005c91fc8798a05d18a9a0a6664f37ebbef1
  - 变更规模：+620 -137
  - 提交者：Yuval Tassa
  - 解决的问题：执行器快捷参数继承来源不明确，可能从其他快捷错误继承参数。
  - 产品启示：减少模型定义歧义，降低用户调试成本，提升 XML 语义可预测性。

6/10-Actuators with fixed or affine gain declare what their control is, and saved models keep it.（fcb83a1）
  - 一句话总结：固定或仿射增益的执行器显式声明其控制类型，并在保存模型中保留。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fcb83a1736e9eb6aa5818d00bc7c596365970ea9
  - 变更规模：+330 -69
  - 提交者：Yuval Tassa
  - 解决的问题：执行器控制类型在固定/仿射增益下未显式声明，保存后语义丢失。
  - 产品启示：增强模型自描述能力，利于下游控制器与绑定正确解释执行器行为。

### ⚡️ 性能/架构优化
- 9/10-Precondition the non-flex dofs with dense per-component blocks in the CG solver.（ad127e8）
  - 一句话总结：通过稠密分块预条件优化 CG 求解器非 flex 自由度收敛性能。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ad127e886fd07f860f5f62259f7be6f9d5d95546
  - 变更规模：+1035 -50
  - 提交者：Alessio Quaglino
  - 解决的问题：非 flex 自由度预条件不足导致求解迭代偏多。
  - 产品启示：延续求解器性能常态化投入，需配套基准与回归验证收益。

### 🐛 Bug修复 / 其他
6/10-Import google-deepmind/mujoco_warp from GitHub.（ff70616）
  - 一句话总结：从 GitHub 同步导入 mujoco_warp，更新 MJX 第三方依赖代码。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ff706165bdbcaf5acdaf2b148adc6c2453c23914
  - 变更规模：+203 -490
  - 提交者：Google DeepMind
  - 解决的问题：MJX 内置 mujoco_warp 依赖与上游不同步。
  - 产品启示：保持 MJX/Warp 生态一致性，降低下游集成与兼容性风险。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 117 条
- 高价值提交（≥6分）: 3 条
- 代码更新规模: +33048 / -50789 行
- 主要贡献者: Mustafa H, Sylvester Kaczmarek, Maximilian Krause

## 🧭 趋势点评
本周更新延续了 IsaacLab 在“多后端并行演进 + 核心架构收敛”主线上的长期趋势：`[6Aii] Share OVRTX camera products and scene lighting` 直接呼应基线中 OVRTX/异步渲染与相机管线提速的持续投入，把渲染产品与场景光照从单实例推向共享复用，属于渲染后端解耦与性能优化的自然延伸；`[Tools] Add stubbed content and consolidate task templates` 则延续了工具链现代化与任务/配置层清理重构的方向，通过模板生成器整合与桩内容降低新任务接入成本，与基线中 uv 工作流、kitless 导入、任务重构等轻量化趋势一致；`Fix ANYmal symmetry augmentation for non-PhysX joint orders` 虽属局部修复，但契合基线中“多后端（PhysX、Newton、Kamino、OVRTX）并行导致行为一致性与回归面扩大”的风险判断，说明团队正在主动修补非 PhysX 路径下的兼容性缺口。整体看，本周并未偏离长期趋势，而是在渲染共享、工具链标准化与多后端兼容性三个既有方向上继续做深。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-[6Aii] Share OVRTX camera products and scene lighting (#8319)（912a294）
  - 评分：7/10
  - 一句话总结：在 OVRTX 路径下共享相机渲染产品与场景光照，减少重复渲染资源开销。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/912a2942cb70bf04349609e8b3f5d3d4c3084a62
  - 变更规模：+325 -316
  - 提交者：ooctipus
  - 解决的问题：多相机或多视角场景下 OVRTX 相机产品与场景光照可能被重复创建与维护，造成渲染资源浪费与一致性风险。
  - 产品启示：共享透视渲染产品与光照是渲染后端解耦与性能优化的重要一步，为后续多相机训练、XR 与异步渲染路径的统一资源管理奠定基础。

6/10-[Tools] Add stubbed content and consolidate task templates (#8296)（aa95c6b）
  - 评分：6/10
  - 一句话总结：整合任务模板生成器并引入桩内容，降低新任务与项目模板的创建门槛。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/aa95c6b8185358da6ebefa7a6b8bd59fdabf0d82
  - 变更规模：+1624 -985
  - 提交者：Anthony Clark
  - 解决的问题：原有任务模板分散、生成流程不统一，开发者创建新任务或项目时缺乏标准化桩内容，导致接入成本高且易出现结构不一致。
  - 产品启示：模板生成器与桩内容的整合有助于统一任务脚手架、提升社区贡献效率，是工具链现代化与任务层接口收敛的重要基础设施。

### ⚡️ 性能/架构优化
- 无（本周高价值提交中未包含该分类条目）

### 🐛 Bug修复 / 其他
6/10-Fix ANYmal symmetry augmentation for non-PhysX joint orders (#8205)（abe7db4）
  - 评分：6/10
  - 一句话总结：修复 ANYmal 对称增强在非 PhysX 关节顺序下的兼容性问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/abe7db4f38174a8ed4e4f843b28d6fe68f34b578
  - 变更规模：+110 -48
  - 提交者：Zeng Qingcheng
  - 解决的问题：ANYmal 对称增强逻辑默认依赖 PhysX 关节顺序，在非 PhysX 后端下关节顺序不一致会导致对称增强错误，影响 velocity 任务训练正确性。
  - 产品启示：随着 Newton、Kamino 等多物理后端并行推进，关节顺序等后端相关假设需显式解耦，此类修复有助于保障多后端行为一致性与任务可移植性。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 20 条
- 高价值提交（≥6分）: 10 条
- 代码更新规模: +2712 / -696 行
- 主要贡献者: Eric Shi, Nicolas Capens, songyinggoh

## 🧭 趋势点评
本周更新延续了仓库在 2026 年 9-10 月“性能与正确性并重、工程化持续加深”的主线：一方面通过限制 SAH BVH 深度、支持 CPU LLVM 编译选项、增强 NumPy dtype 互操作，继续推进后端可移植性与编译期控制能力；另一方面密集修复 eig3 梯度、tile 归约初始化、BSR 缩行置零、tile_map 伴随、捕获值属性访问等数值与代码生成正确性问题，与基线中“数值精度与可微分正确性仍是重点投入方向”的判断高度一致。整体看，本周没有偏离长期趋势，而是将前期在 BVH、稀疏/FEM、代码生成与自动微分路径上的优化与修复进一步收尾和加固，体现出项目在功能扩张后进入稳定性与精度收敛阶段。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Support CPU LLVM compiler options [GH-2004]（1411ff5）
  - 评分：8/10
  - 一句话总结：新增 CPU LLVM 编译选项支持，扩展 CPU 后端编译控制能力。
  - 链接：https://github.com/NVIDIA/warp/commit/1411ff5d3694e34ffb694c1d6881a8588b77c897
  - 变更规模：+421 -19
  - 提交者：Nicolas Capens
  - 解决的问题：此前 CPU 后端缺乏细粒度 LLVM 编译选项配置，用户难以针对特定 CPU 场景调优编译行为。
  - 产品启示：增强 CPU 后端可配置性，配合基线中 LLVM 22 支持与多平台后端覆盖趋势，有助于提升跨平台部署灵活性。

7/10-Add NumPy dtype support for Warp scalars (GH-2038)（b5ea466）
  - 评分：7/10
  - 一句话总结：为 Warp 标量新增 NumPy dtype 支持，增强与 Python 数值生态的互操作性。
  - 链接：https://github.com/NVIDIA/warp/commit/b5ea46659b86efb8f1b511904a3b5c254cd13d70
  - 变更规模：+217 -7
  - 提交者：Nicolas Capens
  - 解决的问题：此前 Warp 标量类型与 NumPy dtype 之间缺乏直接映射，用户在互操作场景中需手动转换，增加使用成本。
  - 产品启示：提升与 NumPy 生态的兼容性，有利于降低用户接入门槛，强化 Warp 作为 Python 数值/仿真工作流组件的定位。

### ⚡️ 性能/架构优化
8/10-Cap SAH BVH depth [GH-1991]（416985f）
  - 评分：8/10
  - 一句话总结：对 SAH BVH 深度进行上限约束，防止过深递归导致栈溢出。
  - 链接：https://github.com/NVIDIA/warp/commit/416985fed1f214c71c7f29ca6013a222b574549c
  - 变更规模：+130 -3
  - 提交者：Eric Shi
  - 解决的问题：SAH BVH 在特定几何分布下可能构建出过深树结构，引发栈溢出或遍历性能退化。
  - 产品启示：提升 BVH 构建与遍历的鲁棒性，直接利好网格射线查询等空间查询场景的稳定性。

### 🐛 Bug修复 / 其他
8/10-Fix eig3 eigenvalue-only gradients [GH-2010]（109b6fa）
  - 评分：8/10
  - 一句话总结：修复 eig3 仅计算特征值时的梯度错误。
  - 链接：https://github.com/NVIDIA/warp/commit/109b6fa2a22680fb129580cb3bbb1b6bb26721a5
  - 变更规模：+178 -5
  - 提交者：Eric Shi
  - 解决的问题：eig3 在仅需特征值梯度时计算结果不正确，影响依赖该路径的可微分仿真与优化。
  - 产品启示：强化自动微分正确性，对可微物理与基于梯度的优化工作流至关重要。

7/10-Fix attribute access on captured values [GH-2023]（5ccf0e6）
  - 评分：7/10
  - 一句话总结：修复对捕获值进行属性访问时的错误。
  - 链接：https://github.com/NVIDIA/warp/commit/5ccf0e6222c8afa28a50a0fd2b2fd662fc30b261
  - 变更规模：+173 -1
  - 提交者：Gilles Daviet
  - 解决的问题：代码生成阶段对捕获值的属性访问处理有误，导致编译或运行期异常。
  - 产品启示：提升代码生成路径的健壮性，减少用户在内核编写中的隐性陷阱。

7/10-Fix tile_map adjoints that need the result (GH-2031)（67bce43）
  - 评分：7/10
  - 一句话总结：修复需要结果的 tile_map 伴随计算。
  - 链接：https://github.com/NVIDIA/warp/commit/67bce43490f596e737e79080161c33730eaf53ae
  - 变更规模：+101 -2
  - 提交者：songyinggoh
  - 解决的问题：tile_map 在伴随计算需要前向结果时处理有误，影响梯度正确性。
  - 产品启示：强化 tile 级自动微分正确性，对可微仿真与基于梯度的优化意义重大。

---

6/10-Fix multi-environment nanogrid cell lookup [GH-2017]（b657cd6）
  - 评分：6/10
  - 一句话总结：修复多环境下 nanogrid 单元查找错误。
  - 链接：https://github.com/NVIDIA/warp/commit/b657cd6c83872ea138e909fc062760d7bb4e4820
  - 变更规模：+49 -4
  - 提交者：Junnosuke Kamohara
  - 解决的问题：多环境场景中 nanogrid 单元查找结果不正确，影响 FEM 多环境仿真精度。
  - 产品启示：提升 FEM 多环境场景正确性，支撑更复杂的仿真与训练任务。

6/10-Fix wp.static() hashing of built-ins (GH-2014)（d3c56b3）
  - 评分：6/10
  - 一句话总结：修复 wp.static() 对内建对象的哈希处理。
  - 链接：https://github.com/NVIDIA/warp/commit/d3c56b3a65cc98eed3f557be63a89e84e6f0675b
  - 变更规模：+33 -1
  - 提交者：songyinggoh
  - 解决的问题：wp.static() 在哈希内建对象时行为异常，可能导致缓存或编译不一致。
  - 产品启示：保障静态表达式与编译缓存的一致性，提升编译期行为可预期性。

6/10-Initialize conditionally-assigned locals in tile reductions (GH-1995)（4abf141）
  - 评分：6/10
  - 一句话总结：修复 tile 归约中条件赋值局部变量未初始化问题。
  - 链接：https://github.com/NVIDIA/warp/commit/4abf141fbc7834765197d03367d100434602de23
  - 变更规模：+6 -6
  - 提交者：Zhihui Du
  - 解决的问题：tile 归约中条件赋值的局部变量可能未初始化，导致归约结果不确定。
  - 产品启示：提升 tile 归约数值确定性，对可复现仿真与训练尤为重要。

6/10-Fix padded `bsr_set_zero` after shrinking rows [GH-2036]（5a0c33d）
  - 评分：6/10
  - 一句话总结：修复 BSR 缩行后填充区域置零错误。
  - 链接：https://github.com/NVIDIA/warp/commit/5a0c33d17d847d0be07ae1003263b572aae0729a
  - 变更规模：+22 -1
  - 提交者：Alain Denzler
  - 解决的问题：BSR 矩阵缩行后填充区域未被正确置零，可能污染后续稀疏计算。
  - 产品启示：保障稀疏矩阵操作正确性，支撑大规模稀疏线性代数与 FEM 求解。

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 4 条
- 高价值提交（≥6分）: 1 条
- 代码更新规模: +417 / -310 行
- 主要贡献者: Andy Lin, Ruslan Rakhimov, cyanseek

## 🧭 趋势点评
本周唯一的高价值提交聚焦于调度器并发组创建的稳定性修复，延续了仓库在 2026-09 至 2026-10 期间“工程化收敛与稳定性维护”的长期趋势。该提交通过修复并发组创建中止问题并补充 FAQ 文档与单元测试，呼应了此前 FSDP 集合通信超时控制（f1b2ee1）、gloo 回退 pinned memory（bd13deb）等分布式基础设施鲁棒性投入，也印证了基线中“并发调度、缓存、数据回放等稳定性问题反复出现”的风险判断。值得注意的是，本次更新未涉及新模型接入或性能优化，与仓库近期功能扩张节奏相比略显收敛，符合 10 月提交量骤降、进入维护阶段的整体特征。

## 🔍 关键更新解析

### 🐛 Bug修复 / 其他
7/10-fix(scheduler): avoid aborts in concurrent group creation (#1645)（c70606f）
  - 评分：7/10
  - 一句话总结：修复调度器在并发创建通信组时可能触发中止的问题，并补充 FAQ 文档与单元测试覆盖。
  - 链接：https://github.com/RLinf/RLinf/commit/c70606f08cdca259b8dec03d4430926b5b8fac9d
  - 变更规模：+232 -24
  - 提交者：cyanseek
  - 解决的问题：并发场景下多个通信组同时创建时可能引发中止（abort），影响分布式训练任务的稳定性与可复现性；同时通过 FAQ 文档补充说明，降低用户排查成本。
  - 产品启示：并发组创建是分布式训练调度的关键路径，此类修复直接提升长时训练的鲁棒性；配套的 FAQ 与单元测试（tests/unit_tests/test_comm.py）表明项目正将稳定性问题制度化处理，符合基线中“可观测性与工程规范将制度化”的预测方向。

---

