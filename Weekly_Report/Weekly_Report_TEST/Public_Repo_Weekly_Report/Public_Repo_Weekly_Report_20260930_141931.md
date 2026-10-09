# 具身智能周报 (2026年09月30日 14:19:31)

- 统计窗口: 2026-09-21 08:55:00 +0800 至 2026-09-30 14:19:31 +0800（左闭右开）

## 行业风向总览

# 具身智能行业风向总结（本周）

**技术焦点：数值正确性与工具链收敛。** 本周多仓库共同指向“功能扩张后的正确性打磨”。MuJoCo 修复 refsite 四元数乘法顺序、mjSpec 帧处理（+1050行），并新增胶囊体 multicontact 与 Hausdorff 距离下界；mjlab 修复伪惯量与 Jacobi 特征求解器边界；Warp 稳定 FEM QR 分解、修复 tile 极值扫描；IsaacLab 移除并行启动与预设机制，收敛启动栈。底层数值与 API 一致性成为跨栈协同重点。

**合成数据动态：渲染与感知管线可编程化。** MuJoCo Studio 新增画中画 Python 绑定、Filament 透明处理修复并暴露 set_options，ReadPixels 支持调用者缓冲区（利于零拷贝截图/录制）；IsaacLab 引入 ovrtx 异步渲染路径，为高吞吐感知数据生成提供性能上限。MJX 新增触觉传感器支持，为触觉模态合成数据铺路。

**产品经理关注信号：** ①破坏性变更密集（IsaacLab 启动 API、RLinf 移除 pi0_pytorch 并重命名 openpi），升级需迁移指南；②上游依赖演进成常态维护负担（Python 3.14/torch 2.14/CUDA 13、transformers 5）；③RLinf 补齐 PI0-FAST GRPO 与 Robotwin Dagger，VLA 强化学习与跨仿真后端能力矩阵持续扩张；④性能冒烟测试集成 CI，回归发现机制补强。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 6 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +1762 / -1077 行
- 主要贡献者: Kevin Zakka, 상티 (윤상현)

## 🧭 趋势点评
本周更新延续了 mjlab 在 2026 年 9-10 月“稳定性收敛 + 工具链升级”的主线：一方面通过修复 `dr.pseudo_inertia` 与 Jacobi 特征求解器的数值边界问题，继续强化域随机化与动力学计算的正确性，这与过去数月高频修复接触传感器、事件计时器、NaN/溢出等时序与数值稳定性问题的趋势一致；另一方面，Python 3.14 与 torch 2.14/CUDA 13 的迁移，延续了仓库持续跟进上游 MuJoCo、mujoco-warp、rsl-rl-lib 与 PyTorch 生态的长期节奏。地形课程改用 episode 行进距离判定，则体现出项目在课程学习与指标语义上进一步追求确定性与可量化，符合此前 metrics reduce、manager 形状校验、nightly benchmark 回归标记等可观测性建设方向。整体看，本周并未偏离长期趋势，而是在功能扩张后继续做正确性打磨与工具链同步。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-Add Python 3.14 support and move to torch 2.14 with CUDA 13. (#1194)（4ac9df2）
  - 评分：9/10
  - 一句话总结：新增 Python 3.14 支持，并迁移至 torch 2.14 与 CUDA 13，完成一次大规模工具链升级。
  - 链接：https://github.com/mujocolab/mjlab/commit/4ac9df2f1d67de4aad62c4a38b27c84b04268bbe
  - 变更规模：+1486 -1018
  - 提交者：Kevin Zakka
  - 解决的问题：解决项目在 Python 3.14、torch 2.14 与 CUDA 13 新生态下的兼容与安装支持问题，避免工具链落后影响用户部署与 CI 验证。
  - 产品启示：持续跟进 Python/PyTorch/CUDA 主线可降低用户环境迁移成本，但也意味着需要同步维护 CI、nightly、Makefile 与安装文档，后续应关注跨版本兼容性与回归测试覆盖。

7/10-Judge the terrain curriculum against the distance the episode commanded (#1188)（c2e1e06）
  - 评分：7/10
  - 一句话总结：地形课程改为依据 episode 实际指令行进距离进行判定，使课程推进更贴近任务语义。
  - 链接：https://github.com/mujocolab/mjlab/commit/c2e1e06400e309b6897a536693fe5d2aa772c5b2
  - 变更规模：+157 -18
  - 提交者：Kevin Zakka
  - 解决的问题：修复地形课程判定与速度命令脱节的问题，避免课程难度推进不能真实反映 episode 指令完成情况。
  - 产品启示：课程学习指标应尽量与任务目标一致，使用“指令距离”而非间接信号可提升训练稳定性与可解释性，并有利于后续基准对比。

### ⚡️ 性能/架构优化
- 无符合条件的提交。

### 🐛 Bug修复 / 其他
6/10-Keep massless bodies unchanged in dr.pseudo_inertia and reject log_uniform. (#1199)（f135c1d）
  - 评分：6/10
  - 一句话总结：修复 `dr.pseudo_inertia` 对无质量刚体的处理，并拒绝非法的 `log_uniform` 输入。
  - 链接：https://github.com/mujocolab/mjlab/commit/f135c1daa0f278bd19e323c2b9f256ca541ae2c5
  - 变更规模：+64 -11
  - 提交者：Kevin Zakka
  - 解决的问题：避免伪惯量随机化错误修改无质量刚体，并阻止 `log_uniform` 在不适用的伪惯量场景中产生非法或不可预期结果。
  - 产品启示：域随机化边界条件需要显式校验与拒绝策略，否则容易在训练中引入静默错误；对无质量刚体等特殊物理对象应保持语义不变。

6/10-Fix Jacobi eigensolver skipping rotation when diagonal entries are equal. (#1198)（c1b937f）
  - 评分：6/10
  - 一句话总结：修复 Jacobi 特征求解器在对角元素相等时跳过旋转的问题。
  - 链接：https://github.com/mujocolab/mjlab/commit/c1b937fc3038df9ce22c4fdf8132c4ef5f0cb304
  - 变更规模：+13 -2
  - 提交者：Kevin Zakka
  - 解决的问题：解决 Jacobi 特征求解器在特定对角元素相等情况下未执行必要旋转、导致特征分解结果不正确的数值问题。
  - 产品启示：伪惯量与动力学随机化依赖底层数值算法正确性，特征求解器这类基础组件的边界修复能减少难以复现的训练偏差，应配套测试覆盖。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 78 条
- 高价值提交（≥6分）: 10 条
- 代码更新规模: +12386 / -6680 行
- 主要贡献者: Kyle Bayes, Yuval Tassa, Alessio Quaglino

## 🧭 趋势点评
本周更新延续了仓库“引擎数值内核提速 + Studio/Web 可视化平台成型 + 构建测试基础设施现代化”的三线并行格局，但在具体落点上明显偏向碰撞与几何管线的能力扩展：新增胶囊体 multicontact 支持与 mjc_hausdorff 距离下界计算，配合移除 flex 内部碰撞选项，显示团队正在重构碰撞检测的抽象边界，把多接触与凸几何度量做成更通用、可复用的底层能力，这与过去数月 GJK/EPA 内存复用、multicontact 最佳面选择、mesh extrema 网格种子等优化一脉相承。与此同时，mjSpec 帧处理修复（+1050 行）与 refsite 四元数乘法顺序修复横跨 C 引擎与 MJX，说明模型编辑 API 与平滑动力学的一致性仍是跨栈协同的重点，也呼应了此前 mji 运行时断言、基础类型编译期大小断言等 API 演进方向。Studio 侧则通过画中画 Python 绑定、Filament 透明处理修复与调用者缓冲区支持，继续把可视化前端从“能用”推向“可编程、可嵌入”，与 FPS/GPU 帧时间追踪、PCSS 阴影等近期提交形成连续投入。整体看，本周没有偏离长期趋势，而是在碰撞几何、模型编辑 API 与渲染可编程性三个既有主线上做了纵深推进，MJX 触觉传感器支持也延续了 mujoco_warp/MJX 生态的同步演进节奏。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Add nativeccd multicontact support for capsules.（6224e95）
  - 评分：8/10
  - 一句话总结：为胶囊体新增 nativeccd 多接触支持，扩展了碰撞检测的几何覆盖范围。
  - 链接：https://github.com/google-deepmind/mujoco/commit/6224e95f6264b99790341f505f8528ece2b866ac
  - 变更规模：+300 -35
  - 提交者：Kyle Bayes
  - 解决的问题：此前 multicontact 能力对胶囊体支持不足，限制了胶囊体在复杂接触场景下的碰撞精度。
  - 产品启示：胶囊体是机器人与角色仿真中最常用的碰撞体之一，补齐其多接触支持可直接提升抓取、行走等接触密集任务的仿真可信度。
7/10-Add the mjc_hausdorff function to engine_collision_convex to compute the lower bound of the directed Hausdorff distance between two convex (compact) geoms.（129fd8e）
  - 评分：7/10
  - 一句话总结：在凸碰撞模块新增 mjc_hausdorff 函数，计算两个凸几何体有向 Hausdorff 距离的下界。
  - 链接：https://github.com/google-deepmind/mujoco/commit/129fd8efc70e2c58e9ec6b336dc7ce5f6296fa0b
  - 变更规模：+355 -0
  - 提交者：Kyle Bayes
  - 解决的问题：缺少对凸几何体间距离下界的快速估计手段，难以支撑碰撞剔除或近似度量需求。
  - 产品启示：Hausdorff 下界可用于快速碰撞预筛与几何相似度度量，为大规模场景的碰撞管线提供新的加速原语。
6/10-Add SensorType.TACTILE support in MJX and update mujoco_warp visibility.（9db1ef8）
  - 评分：6/10
  - 一句话总结：MJX 新增触觉传感器类型支持，并同步更新 mujoco_warp 可见性。
  - 链接：https://github.com/google-deepmind/mujoco/commit/9db1ef85067a781235c46979905dd04588b48553
  - 变更规模：+1 -0
  - 提交者：Alessio Quaglino
  - 解决的问题：MJX 侧缺少触觉传感器类型定义，导致触觉相关模型无法在 MJX 中正确表达。
  - 产品启示：触觉感知是具身智能操作任务的关键模态，MJX 支持触觉传感器为大规模并行触觉强化学习铺平了道路。
6/10-Add Python bindings for Studio picture-in-picture.（adbc7d9）
  - 评分：6/10
  - 一句话总结：为 Studio 画中画功能新增 Python 绑定，使可视化布局可编程控制。
  - 链接：https://github.com/google-deepmind/mujoco/commit/adbc7d91f8b006750ddc1c6ebdd5d01594bf9851
  - 变更规模：+163 -6
  - 提交者：Taylor Howell
  - 解决的问题：画中画此前只能通过 UI 手动操作，无法在脚本化流程中复用。
  - 产品启示：把 Studio 可视化能力暴露到 Python，有助于自动化调试、批量实验对比与远程可视化工作流。
6/10-Enable caller-provided buffer in Filament ReadPixelsRequest and Renderer.（4ce369a）
  - 评分：6/10
  - 一句话总结：Filament 的 ReadPixelsRequest 与 Renderer 支持调用者提供缓冲区。
  - 链接：https://github.com/google-deepmind/mujoco/commit/4ce369a4c02346ba0f17d35e3218ec2d2865a569
  - 变更规模：+305 -129
  - 提交者：Sam Haves
  - 解决的问题：像素读取此前由内部管理缓冲区，无法复用外部内存，增加了分配开销与集成难度。
  - 产品启示：调用者缓冲区支持便于零拷贝集成到既有渲染管线，对高频截图、视频录制与远程渲染场景尤为重要。

### ⚡️ 性能/架构优化
7/10-Remove flex internal collision option and flex_evpair structures（5023a4a）
  - 评分：7/10
  - 一句话总结：移除 flex 内部碰撞选项与 flex_evpair 结构，简化 API 并清理冗余代码。
  - 链接：https://github.com/google-deepmind/mujoco/commit/5023a4a50cbb65bc539f954e00997de6127e62b6
  - 变更规模：+88 -491
  - 提交者：Alessio Quaglino
  - 解决的问题：flex 内部碰撞选项与 evpair 结构长期存在但价值有限，增加了维护负担与 API 复杂度。
  - 产品启示：净删除约 400 行代码，表明团队在 flex 方向上从“堆功能”转向“收敛抽象”，有助于降低下游使用者的认知成本。

### 🐛 Bug修复 / 其他
8/10-Fix frames in the mjSpec API: mjs_delete and mjs_bodyToFrame.（b1ccf67）
  - 评分：8/10
  - 一句话总结：修复 mjSpec API 中 mjs_delete 与 mjs_bodyToFrame 的帧处理逻辑。
  - 链接：https://github.com/google-deepmind/mujoco/commit/b1ccf67964f03ef2b74221c02c7ea8b809d84bfc
  - 变更规模：+1050 -32
  - 提交者：Yuval Tassa
  - 解决的问题：mjSpec 在删除与 body 到 frame 转换时帧处理不正确，可能导致模型编辑结果与预期不符。
  - 产品启示：mjSpec 是程序化模型编辑的核心入口，帧处理正确性直接决定自动建模、域随机化等流程的可靠性。
7/10-Fix `site_quat` multiplication order in `refsite` transmissions.（fa3d0ee）
  - 评分：7/10
  - 一句话总结：修复 refsite 传动中 site_quat 的乘法顺序错误，同步修正 C 引擎与 MJX。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fa3d0ee90982f7a447cd5d31a7fcd512bb6d12d9
  - 变更规模：+21 -15
  - 提交者：Yuval Tassa
  - 解决的问题：refsite 传动中四元数乘法顺序有误，导致参考坐标系下的传动方向计算不正确。
  - 产品启示：此类跨 C 引擎与 MJX 的一致性修复，是保证 CPU 仿真与 GPU 并行仿真结果对齐的关键，直接影响 sim-to-real 可信度。
6/10-GitHub Pull Request: https://github.com/google-deepmind/mujoco/pull/3632（c90ba88）
  - 评分：6/10
  - 一句话总结：合并 PR #3632，涉及 mjData、mjxmacro 等核心数据结构与平滑计算。
  - 链接：https://github.com/google-deepmind/mujoco/commit/c90ba889b020c5353ccb86fb023b8dcad4befbb2
  - 变更规模：+404 -133
  - 提交者：Alessio Quaglino
  - 解决的问题：PR 涉及核心数据结构与 introspect 生成代码，修复了相关结构定义与平滑计算的一致性问题。
  - 产品启示：核心数据结构变更会波及 Python introspect 与 MJX 宏，提示下游绑定需关注此类跨层改动的兼容性。
6/10-Fix transparency handling in Filament renderer and expose set_options to Python.（fd37000）
  - 评分：6/10
  - 一句话总结：修复 Filament 渲染器透明处理，并将 set_options 暴露给 Python。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fd3700009fc39793161a40df71abc047582262ce
  - 变更规模：+11 -5
  - 提交者：Tom Erez
  - 解决的问题：Filament 渲染器透明材质处理不正确，且渲染选项无法从 Python 配置。
  - 产品启示：透明渲染正确性影响视觉真实感与合成数据质量，Python 侧可配置则提升了渲染管线的可调优性。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 160 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +68973 / -98398 行
- 主要贡献者: Mustafa H, ooctipus, isaaclab-bot[bot]

## 🧭 趋势点评
本周更新延续了仓库“架构收敛与性能攻坚并行”的长期主线，并进一步向核心启动栈与多后端抽象深化。`[Core]` 系列移除并行启动与预设机制、内联启动栈辅助函数，与基线中 3.0 核心子包重构、仿真作用域后端注册表的演进方向高度一致，属于典型的破坏性收敛动作；异步渲染路径（ovrtx only）与异构 OvPhysX 克隆则延续了多后端可插拔架构的扩展趋势。与此同时，性能冒烟测试工具集成、双足 air-time 奖励平衡、多可视化器关闭挂起修复，分别对应基线中“CI 与验证效率提升”“任务与 RL 生态完善”“运行时生命周期稳定性”三条支线，整体未偏离长期趋势，反而在启动机制精简与后端一致性上更进一步。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-feat: Adds an opt-in asynchronous render path (ovrtx only) (#7075)（eb6617c）
  - 评分：9/10
  - 一句话总结：引入仅限 ovrtx 的可选异步渲染路径，为渲染与仿真解耦提供新执行模式。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/eb6617cdad62aec29b6dd6d1a43e9b4d1e4ca4a2
  - 变更规模：+722 -159
  - 提交者：Peter Verswyvelen
  - 解决的问题：同步渲染路径限制吞吐，缺乏可选的异步执行机制来重叠渲染与仿真计算。
  - 产品启示：异步渲染作为 opt-in 特性可降低对现有用户的影响，同时为高吞吐感知与训练场景提供性能上限空间，需配套文档与测试覆盖以防隐性回归。

8/10-Support heterogeneous OvPhysX cloning (#7890)（d176bf0）
  - 评分：8/10
  - 一句话总结：为 OvPhysX 后端增加异构克隆能力，支持不同资产/配置的批量复制。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/d176bf025ea5af1a2da9456cd3de46af41038957
  - 变更规模：+1021 -619
  - 提交者：Maximilian Krause
  - 解决的问题：原有 OvPhysX 克隆仅支持同构场景，无法高效构建异构多资产环境。
  - 产品启示：异构克隆是多后端抽象成熟度的关键指标，可支撑更复杂的训练与评测场景，但需关注与 PhysX/Newton 行为一致性。

6/10-Counterbalance the biped air-time reward on Cassie/Go2/H1 (#7813)（9f95f70）
  - 评分：6/10
  - 一句话总结：对 Cassie/Go2/H1 双足任务的 air-time 奖励进行平衡修正。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/9f95f70efba082d2ccc7d94d3e58f68bd0126e99
  - 变更规模：+314 -4
  - 提交者：Henry Hu
  - 解决的问题：双足 air-time 奖励失衡导致策略行为偏差，影响训练稳定性与任务表现。
  - 产品启示：奖励配平直接影响 RL 任务可复现性与基准可信度，需同步更新实验配置与文档以避免结果不一致。

6/10-Angehu/perf smoke integration (#7137)（eeb6e04）
  - 评分：6/10
  - 一句话总结：将性能冒烟测试工具集成进 CI 工作流与基础镜像。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/eeb6e0458cec52499f2719b325d7fabe584b0f93
  - 变更规模：+2002 -1
  - 提交者：angehu-nv
  - 解决的问题：缺乏自动化性能冒烟检测，性能回归难以及早发现。
  - 产品启示：性能冒烟集成可弥补此前基准移除带来的回归发现缺口，但需平衡测试时长与 CI 稳定性。

### ⚡️ 性能/架构优化
7/10-[Core] Remove parallel launch and preset mechanisms (#8112)（b744dbe）
  - 评分：7/10
  - 一句话总结：移除并行启动与预设机制，统一为单一启动路径。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/b744dbec94de3b27f2e39064c56f0b7581a2881c
  - 变更规模：+209 -501
  - 提交者：ooctipus
  - 解决的问题：并行启动与预设机制增加维护复杂度与行为不一致风险。
  - 产品启示：属于 3.0 核心重构的破坏性收敛动作，需配套迁移指南，下游用户需关注启动 API 变更。

6/10-[Core] Inline launch-stack helpers that only restate or forward (#8111)（24e1b46）
  - 评分：6/10
  - 一句话总结：内联仅做转发或重述的启动栈辅助函数，精简调用层级。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/24e1b46ce8cf8fad61f182792708139c5beb70d3
  - 变更规模：+361 -484
  - 提交者：ooctipus
  - 解决的问题：冗余辅助函数增加阅读与维护成本，掩盖真实启动逻辑。
  - 产品启示：与移除并行启动机制形成配套清理，推动启动栈向单一、可读路径收敛。

### 🐛 Bug修复 / 其他
6/10-[VDR feedback] Fix shutdown hang on Ctrl+C with multiple visualizers (#7698)（389c12f）
  - 评分：6/10
  - 一句话总结：修复多可视化器场景下 Ctrl+C 关闭挂起问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/389c12f52f9f0bea607985fcc181a0f367229222
  - 变更规模：+167 -91
  - 提交者：matthewtrepte
  - 解决的问题：多可视化器同时运行时中断信号处理不当导致进程挂起。
  - 产品启示：运行时生命周期稳定性直接影响开发与调试体验，与基线中“关闭运行时前停止仿真”的收尾方向一致。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 28 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +3750 / -549 行
- 主要贡献者: Eric Shi, Gilles Daviet, Nicolas Capens

## 🧭 趋势点评
本周更新延续了仓库在“性能优化与数值正确性并重”的长期主线：`7906779` 与 `c59167b` 分别从 Python 运行时开销和 BSR/FEM 内核性能两端继续压缩开销，呼应了基线中 9 月“降低 Python 内建调用开销”“保持 BSR/FEM 性能”的优化节奏；`45c001d` 恢复网格射线查询占用率，则是对 6 月 mesh ray BVH 遍历优化（GH-1529/GH-1530）的后续调优，说明空间查询路径仍在持续打磨。与此同时，`13f9a11` 修复 tile 极值扫描在浮点极值与 uint32 上的正确性、`a596470` 稳定 FEM QR 分解，延续了 7 月以来对数值精度与自动微分正确性的高强度投入（如批量归约精度、四元数扭转角、eig3 梯度）。整体看，本周并未偏离基线趋势，而是集中在“性能不退化 + 数值边界正确”这一交叉地带，属于典型的收敛式加固而非方向性扩张。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周无符合评分≥6的新功能/特性类提交）

### ⚡️ 性能/架构优化

6/10-Reduce Python built-in call overhead [GH-1983]（7906779）
  - 评分：6/10
  - 一句话总结：削减 Python 内建调用开销，降低运行时解释层成本。
  - 链接：https://github.com/NVIDIA/warp/commit/79067793efd89e3bd69b960c73781ccc4ac13c7f
  - 变更规模：+93 -21
  - 提交者：Eric Shi
  - 解决的问题：Python 内建调用开销偏高，影响运行时性能。
  - 产品启示：面向大规模仿真与可微训练场景，持续压缩 Python 侧开销可提升端到端吞吐，并降低用户对“Python 慢”的感知。

6/10-Restore mesh ray-query occupancy [GH-1840]（45c001d）
  - 评分：6/10
  - 一句话总结：恢复网格射线查询的占用率，改善空间查询执行效率。
  - 链接：https://github.com/NVIDIA/warp/commit/45c001d47199f83ae11d8ae798ba7da3e7b2ce31
  - 变更规模：+29 -18
  - 提交者：Eric Shi
  - 解决的问题：网格射线查询占用率下降，影响 BVH/射线遍历性能表现。
  - 产品启示：空间查询是机器人、仿真与几何处理的高频路径，占用率恢复有助于维持此前 mesh ray BVH 优化的收益。

6/10-Preserve BSR and FEM performance [GH-1918]（c59167b）
  - 评分：6/10
  - 一句话总结：在相关改动中保持 BSR 与 FEM 性能不退化。
  - 链接：https://github.com/NVIDIA/warp/commit/c59167bbec2d78e1bd07e7af3d714ecce241d2ed
  - 变更规模：+10 -6
  - 提交者：Eric Shi
  - 解决的问题：BSR 与 FEM 路径存在性能回退风险，需要显式保持性能。
  - 产品启示：稀疏线性代数与 FEM 是可微物理求解核心，性能保持是避免优化收益被新功能抵消的关键防线。

### 🐛 Bug修复 / 其他

7/10-Stabilize FEM QR decompositions (GH-1985)（a596470）
  - 评分：7/10
  - 一句话总结：稳定 FEM QR 分解，提升数值鲁棒性。
  - 链接：https://github.com/NVIDIA/warp/commit/a596470bafe6805c10fb2ce83ba47857253d37dd
  - 变更规模：+344 -28
  - 提交者：Gilles Daviet
  - 解决的问题：FEM QR 分解在数值上不稳定，可能影响求解精度与收敛。
  - 产品启示：FEM 求解器稳定性直接关系到可微物理训练与大规模仿真的可信度，是数值内核加固的重点方向。

---

6/10-Fix tile min/max scans on float extremes and uint32 [GH-2003]（13f9a11）
  - 评分：6/10
  - 一句话总结：修复 tile 极值扫描在浮点极值与 uint32 上的正确性问题。
  - 链接：https://github.com/NVIDIA/warp/commit/13f9a110a93daac987042a9e3dd213549d0e15c0
  - 变更规模：+158 -4
  - 提交者：Christopher Crouzet
  - 解决的问题：tile min/max 扫描在浮点极值与 uint32 输入下结果不正确。
  - 产品启示：tile 归约是 GPU 并行内核的基础语义，边界值正确性直接影响仿真与数值计算的可靠性。

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 20 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +7879 / -5985 行
- 主要贡献者: Andy Lin, liuke, panhe1818

## 🧭 趋势点评
本周高价值提交延续了 RLinf 在 2026 年 7-8 月“功能扩张 + 基础设施重构”的双主线：一方面通过 PI0-FAST GRPO、Robotwin Dagger、Cosmos3 SFT/SGLang 评测等提交继续拓宽具身模型与训练范式覆盖，另一方面以 FSDP 梯度范数分片归约、移除 pi0_pytorch 并重命名 openpi 等动作深化分布式训练与代码架构治理，同时 transformers 5 适配与 Cosmos3 示例修复反映出上游依赖演进带来的兼容性压力正在成为常态化维护负担。整体看，本周并未偏离仓库“高频迭代、功能驱动、性能优化占比偏低”的长期特征，但 FSDP 与架构清理类提交的集中出现，说明项目正从单纯堆叠功能转向对既有并行训练与模型接入路径做收敛，这与基线中“权重同步与数据模块组件化、工程规范制度化”的预测方向一致。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-feat(embodied): support PI0-FAST GRPO (#1493)（b023deb）
  - 评分：8/10
  - 一句话总结：新增 PI0-FAST 模型的 GRPO 强化学习训练支持，覆盖 README、LIBERO 评测文档与 embodied e2e 测试工作流。
  - 链接：https://github.com/RLinf/RLinf/commit/b023deb7e90ceadfe18e0a528e862e3c630f7e0a
  - 变更规模：+2635 -57
  - 提交者：chenxj
  - 解决的问题：PI0-FAST 此前缺乏 GRPO 训练路径，无法在 RLinf 中对该模型进行基于组相对优势的强化学习调优。
  - 产品启示：模型支持面继续扩张，PI0-FAST 与 GRPO 的组合增强了 RLinf 在 VLA 强化学习方向的竞争力，但也会抬高测试矩阵与文档同步维护成本。

7/10-feat: support new Dagger in Robotwin (#1551)（7d2dfa7）
  - 评分：7/10
  - 一句话总结：为 Robotwin 仿真环境新增 Dagger 训练范式支持，并同步更新中英文 behavior 文档与 r1pro 环境配置。
  - 链接：https://github.com/RLinf/RLinf/commit/7d2dfa77faffa7887304670d5fcaed1128b84ae8
  - 变更规模：+265 -37
  - 提交者：renji555
  - 解决的问题：此前 Robotwin 缺少新版 Dagger 支持，限制了在该仿真后端上进行交互式模仿学习与在线纠错训练的能力。
  - 产品启示：Robotwin 作为仿真后端的能力矩阵进一步补齐，有助于降低跨环境（IsaacLab/LIBERO/Robotwin）迁移成本，强化 RLinf 作为统一具身 RL 基础设施的定位。

### ⚡️ 性能/架构优化
7/10-fix(fsdp): reduce the gradient norm over every shard (#1558)（b85c071）
  - 评分：7/10
  - 一句话总结：将 FSDP 梯度范数从全局归约改为逐 shard 归约，降低跨 rank 通信量并补充单元测试。
  - 链接：https://github.com/RLinf/RLinf/commit/b85c07175b10017bf58ab83e1b1eee99666d0626
  - 变更规模：+272 -5
  - 提交者：Andy Lin
  - 解决的问题：原全局梯度范数归约在大规模分片训练下产生不必要的跨 rank 通信开销，影响训练吞吐。
  - 产品启示：FSDP 通信层持续成为性能优化主战场，此类分片级归约有助于支撑更大规模分布式训练，但需关注异构硬件上的数值一致性回归。

7/10-refactor: remove pi0_pytorch and rename openpi_rlinf to openpi (#1580)（184ba07）
  - 评分：7/10
  - 一句话总结：移除 pi0_pytorch 模块并将 openpi_rlinf 重命名为 openpi，同步调整 README、文档与 e2e 工作流。
  - 链接：https://github.com/RLinf/RLinf/commit/184ba07f0a5b3a09a4696a4e3c8aa4b3c720fa86
  - 变更规模：+2055 -5261
  - 提交者：guozhen
  - 解决的问题：pi0_pytorch 与 openpi_rlinf 并存导致模型接入路径冗余、命名混乱，增加维护与用户理解成本。
  - 产品启示：属于破坏性变更，涉及导入路径与配置结构调整，升级时需注意兼容性；但长期看有助于统一 openpi 生态接入，降低文档与实现漂移风险。

### 🐛 Bug修复 / 其他
6/10-fix(vlm): support transformers 5 in VLM SFT (#1610)（d1bf37c）
  - 评分：6/10
  - 一句话总结：适配 transformers 5 版本以修复 VLM SFT 流程，并更新 mbridge 文档与 SFT/agent e2e 测试工作流。
  - 链接：https://github.com/RLinf/RLinf/commit/d1bf37cdc73bba24218d523b08c1c88fcffd9deb
  - 变更规模：+178 -301
  - 提交者：sherlockcooper
  - 解决的问题：transformers 5 上游变更导致 VLM SFT 训练流程不兼容，影响 SFT 与 agent 相关 e2e 测试通过率。
  - 产品启示：上游依赖演进是持续压力，需通过 e2e 覆盖与版本治理降低破坏性变更对训练流程的冲击。

6/10-fix(cosmos3): make the Cosmos3 SFT and SGLang eval examples run (#1602)（010990e）
  - 评分：6/10
  - 一句话总结：修复 Cosmos3 的 SFT 与 SGLang 评测示例，使其可正常运行，并补充中英文评测文档与 libero_spatial 配置。
  - 链接：https://github.com/RLinf/RLinf/commit/010990e5c81ae17d141d3eab584a3bd1791df950
  - 变更规模：+763 -60
  - 提交者：Andy Lin
  - 解决的问题：Cosmos3 SFT 与 SGLang 评测示例此前无法直接运行，阻碍用户复现与验证该模型能力。
  - 产品启示：新模型接入后示例可运行性是用户采纳的关键门槛，此类修复有助于降低 Cosmos3 的使用门槛，但也反映模型扩张带来的文档与实现漂移风险。

---

