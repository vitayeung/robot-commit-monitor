# 具身智能周报 (2026年09月30日 15:56:36)

## 行业风向总览

# 具身智能行业风向周度总结

**技术焦点：物理引擎内核精进与多后端一致性。** MuJoCo 本周聚焦碰撞精度与渲染可编程性，新增胶囊体原生 CCD 多接触支持及凸体 Hausdorff 距离函数，并清理 flex 遗留碰撞路径；IsaacLab 推进异步渲染路径（ovrtx）与异构 OvPhysX 克隆，同时引入性能冒烟测试框架；Warp 则集中治理数值稳定性，修复 FEM QR 分解与 tile 扫描边界问题。mjlab 跟进 Python 3.14 + torch 2.14 + CUDA 13 新栈，并修复伪惯量域随机化对无质量刚体的处理。

**合成数据动态：** 本周无直接合成数据管线更新，但域随机化数值稳健性（mjlab 拒绝 log_uniform 采样）与触觉传感器类型在 MJX 中的补齐，为仿真数据生成的物理真实性提供底层支撑。

**产品经理关注信号：** ① IsaacLab 移除并行启动与预设机制属破坏性变更，需评估迁移成本；② RLinf 密集修复 FSDP 检查点 RNG 一致性与分片恢复，分布式训练稳定性仍是功能扩张的短板；③ Cosmos3 SFT/SGLang 示例修复表明世界模型生态接入尚处磨合期；④ 多仓库同步推进新工具链（CUDA 13、transformers 5），下游环境兼容压力上升，建议提前规划版本矩阵。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 5 条
- 高价值提交（≥6分）: 2 条
- 代码更新规模: +1605 / -1059 行
- 主要贡献者: Kevin Zakka, 상티 (윤상현)

## 🧭 趋势点评
本周的两条高价值提交延续了 mjlab 在 2026-09 阶段“物理正确性 + 平台兼容性”的双主线：一方面 f135c1d 针对 `dr.pseudo_inertia` 中无质量刚体的处理进行修复并拒绝 `log_uniform`，延续了此前对域随机化数值稳健性（如伪惯量、光照随机化、texid 随机化）的持续打磨；另一方面 4ac9df2 将运行时栈推进到 Python 3.14 + torch 2.14 + CUDA 13，与此前 mujoco/mujoco-warp 3.10→3.11、rsl-rl-lib 5.0.1→5.5.0 的依赖前移节奏一致，属于典型的“跟进上游生态、扩展兼容矩阵”动作。整体来看，本周更新并未偏离仓库长期“以修复与兼容为主、性能优化占比偏低”的演进特征，反而进一步强化了其在数值正确性与新平台支持上的投入方向。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-Add Python 3.14 support and move to torch 2.14 with CUDA 13. (#1194)（4ac9df2）
  - 评分：9/10
  - 一句话总结：为项目新增 Python 3.14 支持，并将运行时迁移至 torch 2.14 与 CUDA 13。
  - 链接：https://github.com/mujocolab/mjlab/commit/4ac9df2f1d67de4aad62c4a38b27c84b04268bbe
  - 变更规模：+1486 -1018
  - 提交者：Kevin Zakka
  - 解决的问题：解决项目在最新 Python 3.14 与 torch 2.14/CUDA 13 组合下无法直接运行的问题，同步更新 CI、nightly、Makefile、安装文档与 pyproject.toml，保持与上游深度学习与仿真栈的兼容性。
  - 产品启示：表明 mjlab 正主动扩展对新平台的支持边界，用户可更早迁移到新工具链；但较新的 Python/torch/CUDA 组合也意味着下游环境兼容与迁移成本上升，需关注生态覆盖与文档指引。

### ⚡️ 性能/架构优化
- 无

### 🐛 Bug修复 / 其他
6/10-Keep massless bodies unchanged in dr.pseudo_inertia and reject log_uniform. (#1199)（f135c1d）
  - 评分：6/10
  - 一句话总结：修复 `dr.pseudo_inertia` 对无质量刚体的处理，并拒绝不合理的 `log_uniform` 采样。
  - 链接：https://github.com/mujocolab/mjlab/commit/f135c1daa0f278bd19e323c2b9f256ca541ae2c5
  - 变更规模：+64 -11
  - 提交者：Kevin Zakka
  - 解决的问题：避免伪惯量域随机化在无质量刚体上产生错误修改，同时拒绝 `log_uniform` 这类不适用于该场景的分布，提升域随机化的数值正确性与稳定性。
  - 产品启示：反映团队对域随机化边界条件的持续关注，有助于减少训练中因随机化配置不当导致的异常；也提示配置项语义需与物理约束保持一致，避免用户误用。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 46 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +8564 / -5260 行
- 主要贡献者: Alessio Quaglino, Alessio, Kyle Bayes

## 🧭 趋势点评
本周更新延续了仓库“引擎内核精进 + Studio/Web 工具链扩张”的双主线格局，并进一步向碰撞检测的精细化与渲染管线的可编程性倾斜。新增的 nativeccd 胶囊体多接触支持与 mjc_hausdorff 距离函数，延续了此前 GJK/EPA、multicontact 最佳面选择与网格爬山种子优化的碰撞主线，表明凸体碰撞仍是核心投入方向；而 Filament 透明处理修复、调用方缓冲区支持与 Studio 画中画 Python 绑定，则延续了渲染栈向可配置、可嵌入方向演进的趋势。值得注意的是，本周出现了移除 flex 内部碰撞旧选项（5023a4a）这类架构清理动作，以及 mjSpec 帧 API 的大规模修复（b1ccf67），显示项目在快速扩张功能的同时开始偿还技术债、收敛历史遗留接口，这与基线中“重构/清理约 40 条”的节奏一致，但清理力度有所加强。整体看，本周并未偏离长期趋势，而是在碰撞精度、渲染灵活性与 API 稳定性三个既有方向上做了纵深推进。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Add nativeccd multicontact support for capsules.（6224e95）
  - 评分：8
  - 一句话总结：为胶囊体引入原生 CCD 多接触支持，扩展连续碰撞检测的几何覆盖范围。
  - 链接：https://github.com/google-deepmind/mujoco/commit/6224e95f6264b99790341f505f8528ece2b866ac
  - 变更规模：+300 -35
  - 提交者：Kyle Bayes
  - 解决的问题：此前 nativeccd 多接触能力未覆盖胶囊体，导致胶囊体在高速连续碰撞场景下接触生成不完整。
  - 产品启示：胶囊体是机器人肢体与关节的常用碰撞代理，该支持直接提升高速运动仿真的接触可靠性，利好强化学习训练与实时仿真场景。

7/10-Add the mjc_hausdorff function to engine_collision_convex to compute the lower bound of the directed Hausdorff distance between two convex (compact) geoms.（129fd8e）
  - 评分：7
  - 一句话总结：新增 mjc_hausdorff 函数，计算两个凸几何体间有向 Hausdorff 距离下界。
  - 链接：https://github.com/google-deepmind/mujoco/commit/129fd8efc70e2c58e9ec6b336dc7ce5f6296fa0b
  - 变更规模：+355 -0
  - 提交者：Kyle Bayes
  - 解决的问题：缺少凸体间距离下界的量化工具，难以评估碰撞检测精度与几何近似质量。
  - 产品启示：为碰撞检测质量评估与凸包近似误差分析提供量化基础，可服务于测试与算法调优。

6/10-Add SensorType.TACTILE support in MJX and update mujoco_warp visibility.（9db1ef8）
  - 评分：6
  - 一句话总结：在 MJX 中新增触觉传感器类型并同步 mujoco_warp 可见性。
  - 链接：https://github.com/google-deepmind/mujoco/commit/9db1ef85067a781235c46979905dd04588b48553
  - 变更规模：+1 -0
  - 提交者：Alessio Quaglino
  - 解决的问题：MJX 侧缺少触觉传感器类型定义，无法与主引擎的触觉传感能力对齐。
  - 产品启示：触觉感知是灵巧操作与接触密集型任务的关键，该支持强化了 JAX 生态下的触觉仿真能力。

6/10-Add Python bindings for Studio picture-in-picture.（adbc7d9）
  - 评分：6
  - 一句话总结：为 Studio 画中画功能新增 Python 绑定。
  - 链接：https://github.com/google-deepmind/mujoco/commit/adbc7d91f8b006750ddc1c6ebdd5d01594bf9851
  - 变更规模：+163 -6
  - 提交者：Taylor Howell
  - 解决的问题：画中画能力此前无法从 Python 侧调用，限制了脚本化与实验性使用。
  - 产品启示：降低 Studio 高级可视化功能的调用门槛，便于研究者在 Python 工作流中嵌入多视图调试。

6/10-Enable caller-provided buffer in Filament ReadPixelsRequest and Renderer.（4ce369a）
  - 评分：6
  - 一句话总结：允许调用方在 Filament 像素读取请求与渲染器中提供缓冲区。
  - 链接：https://github.com/google-deepmind/mujoco/commit/4ce369a4c02346ba0f17d35e3218ec2d2865a569
  - 变更规模：+305 -129
  - 提交者：Sam Haves
  - 解决的问题：像素读取此前由内部管理缓冲区，无法复用调用方内存，增加分配开销与集成难度。
  - 产品启示：提升渲染数据回读的灵活性与内存效率，利好需要高频截图或视觉反馈的训练管线。

### ⚡️ 性能/架构优化
7/10-Remove flex internal collision option and flex_evpair structures（5023a4a）
  - 评分：7
  - 一句话总结：移除 flex 内部碰撞选项及 flex_evpair 结构，精简柔体碰撞代码路径。
  - 链接：https://github.com/google-deepmind/mujoco/commit/5023a4a50cbb65bc539f954e00997de6127e62b6
  - 变更规模：+88 -491
  - 提交者：Alessio Quaglino
  - 解决的问题：遗留的 flex 内部碰撞选项与 evpair 结构增加维护负担与代码复杂度。
  - 产品启示：架构清理降低柔体模块的维护成本，为后续 flex 优化主线腾出空间，但需关注依赖旧选项的下游兼容性。

### 🐛 Bug修复 / 其他
7/10-Fix `site_quat` multiplication order in `refsite` transmissions.（fa3d0ee）
  - 评分：7
  - 一句话总结：修复 refsite 传动中 site_quat 的乘法顺序错误。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fa3d0ee90982f7a447cd5d31a7fcd512bb6d12d9
  - 变更规模：+21 -15
  - 提交者：Yuval Tassa
  - 解决的问题：refsite 传动中四元数乘法顺序错误导致姿态计算偏差，影响引擎与 MJX 一致性。
  - 产品启示：修正姿态计算精度，保障依赖 refsite 传动的机器人模型仿真正确性，并同步修复 MJX 侧。

7/10-Fix frames in the mjSpec API: mjs_delete and mjs_bodyToFrame.（b1ccf67）
  - 评分：7
  - 一句话总结：修复 mjSpec API 中 mjs_delete 与 mjs_bodyToFrame 的帧处理缺陷。
  - 链接：https://github.com/google-deepmind/mujoco/commit/b1ccf67964f03ef2b74221c02c7ea8b809d84bfc
  - 变更规模：+1050 -32
  - 提交者：Yuval Tassa
  - 解决的问题：mjSpec 帧相关 API 存在删除与坐标转换错误，影响模型编辑的正确性。
  - 产品启示：提升模型编辑 API 的可靠性，对依赖 mjSpec 进行程序化建模的用户至关重要。

6/10-Fix transparency handling in Filament renderer and expose set_options to Python.（fd37000）
  - 评分：6
  - 一句话总结：修复 Filament 渲染器透明处理并暴露 set_options 到 Python。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fd3700009fc39793161a40df71abc047582262ce
  - 变更规模：+11 -5
  - 提交者：Tom Erez
  - 解决的问题：Filament 渲染透明材质处理不正确，且渲染选项无法从 Python 配置。
  - 产品启示：改善可视化真实感并提升渲染配置的可编程性，利好需要精细视觉调试的场景。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 139 条
- 高价值提交（≥6分）: 10 条
- 代码更新规模: +63445 / -94142 行
- 主要贡献者: Mustafa H, ooctipus, isaaclab-bot[bot]

## 🧭 趋势点评
本周更新延续了仓库“多后端并行演进 + 大规模重构清理 + 持续性能治理”的长期主线：一方面，Newton 刚体集合精确匹配、Kamino P-ADMM 发散修复、异构 OvPhysX 克隆与 ADMM 碰撞容量控制等提交，继续夯实 PhysX/Newton/OvPhysX/Kamino 多物理后端的一致性与可扩展性；另一方面，移除并行启动与预设机制、升级 usd-exchange 3.0.0 并移除 OpenUSD 兼容逻辑，呼应了 3.0 版本化清理与依赖自动升级的既定方向。同时，异步渲染路径（ovrtx only）与性能冒烟测试框架的引入，将此前分散的渲染解耦与 CI 性能治理推进到可落地阶段，而双足腾空奖励平衡、多可视化器关闭挂起修复则体现了对既有任务基线与运行时稳定性的持续修正，整体未偏离基线趋势，但在渲染异步化与性能测试基础设施上有所加速。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-feat: Adds an opt-in asynchronous render path (ovrtx only) (#7075)（eb6617c）
  - 评分：9/10
  - 一句话总结：新增仅限 ovrtx 的可选异步渲染路径，为渲染与仿真解耦提供新能力。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/eb6617cdad62aec29b6dd6d1a43e9b4d1e4ca4a2
  - 变更规模：+722 -159
  - 提交者：Peter Verswyvelen
  - 解决的问题：渲染与仿真强耦合导致图像类任务开销高、难以异步流水线化。
  - 产品启示：异步渲染路径可作为视觉强化学习吞吐提升的关键抓手，但需关注 ovrtx 单一后端依赖带来的兼容性约束。

8/10-Support heterogeneous OvPhysX cloning (#7890)（d176bf0）
  - 评分：8/10
  - 一句话总结：支持异构 OvPhysX 克隆，扩展多后端下资产复制的灵活性。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/d176bf025ea5af1a2da9456cd3de46af41038957
  - 变更规模：+1021 -619
  - 提交者：Maximilian Krause
  - 解决的问题：原有 OvPhysX 克隆无法处理异构资产，限制了多环境并行与后端迁移场景。
  - 产品启示：异构克隆能力是规模化训练与后端可插拔体系的重要基础，需同步完善文档与测试覆盖。

7/10-Angehu/perf smoke integration (#7137)（eeb6e04）
  - 评分：7/10
  - 一句话总结：集成性能冒烟测试框架，将性能回归检测纳入 CI 流程。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/eeb6e0458cec52499f2719b325d7fabe584b0f93
  - 变更规模：+2002 -1
  - 提交者：angehu-nv
  - 解决的问题：此前性能优化分散、缺乏统一基准口径，回归难以及时发现。
  - 产品启示：性能冒烟框架为跨后端横向比较提供基础，但需持续维护阈值以避免误报与漂移。

6/10-Add internal ADMM collision capacity controls (#7912)（4d2c6b1）
  - 评分：6/10
  - 一句话总结：新增内部 ADMM 碰撞容量控制，提升耦合求解器接触处理的可配置性。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/4d2c6b16f80e15083f52a8d0f75be2ff2c628e2d
  - 变更规模：+184 -7
  - 提交者：Rebecca Zhang
  - 解决的问题：ADMM 耦合求解器在复杂接触场景下缺乏容量调节手段，易出现性能或稳定性问题。
  - 产品启示：碰撞容量控制为耦合求解器调优提供抓手，但内部参数暴露需谨慎管理默认值。

### ⚡️ 性能/架构优化
8/10-[Core] Remove parallel launch and preset mechanisms (#8112)（b744dbe）
  - 评分：8/10
  - 一句话总结：移除并行启动与预设机制，统一启动路径以简化核心架构。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/b744dbec94de3b27f2e39064c56f0b7581a2881c
  - 变更规模：+209 -501
  - 提交者：ooctipus
  - 解决的问题：并行启动与预设机制造成启动路径分叉、维护成本高且行为不一致。
  - 产品启示：单一启动机制降低认知负担，但属于破坏性变更，需配套迁移指南以降低下游适配成本。

### 🐛 Bug修复 / 其他
7/10-[VDR feedback] Fix shutdown hang on Ctrl+C with multiple visualizers (#7698)（389c12f）
  - 评分：7/10
  - 一句话总结：修复多可视化器场景下 Ctrl+C 关闭挂起问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/389c12f52f9f0bea607985fcc181a0f367229222
  - 变更规模：+167 -91
  - 提交者：matthewtrepte
  - 解决的问题：多可视化器同时运行时中断信号处理不当导致进程无法正常退出。
  - 产品启示：运行时中断与清理路径的健壮性直接影响开发体验，需纳入 CI 冒烟覆盖。

6/10-Match Newton rigid object collection bodies exactly (#8175)（998bf88）
  - 评分：6/10
  - 一句话总结：修复 Newton 刚体集合匹配逻辑，确保 body 精确对应。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/998bf887af42c46d13207fd0a95b47f2559f9259
  - 变更规模：+43 -79
  - 提交者：yusuf
  - 解决的问题：Newton 后端刚体集合匹配不精确，可能导致资产映射错误。
  - 产品启示：多后端一致性依赖此类精确匹配修复，需在测试中固化集合映射校验。

6/10-Counterbalance the biped air-time reward on Cassie/Go2/H1 (#7813)（9f95f70）
  - 评分：6/10
  - 一句话总结：对 Cassie/Go2/H1 的双足腾空奖励做反向平衡，修正奖励偏置。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/9f95f70efba082d2ccc7d94d3e58f68bd0126e99
  - 变更规模：+314 -4
  - 提交者：Henry Hu
  - 解决的问题：原有 air-time 奖励可能导致策略偏向异常腾空行为，影响训练稳定性。
  - 产品启示：奖励函数微调直接影响基线可复现性，需同步更新示例与教程避免过时。

6/10-Fix DR Legs Kamino P-ADMM divergence (#7638)（5eef1d7）
  - 评分：6/10
  - 一句话总结：修复 DR Legs 在 Kamino P-ADMM 求解器下的发散问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/5eef1d70f3c7f3af1e1c99eae85192b61cda52ac
  - 变更规模：+54 -6
  - 提交者：Antoine RICHARD
  - 解决的问题：Kamino 求解器在特定任务配置下出现数值发散，影响训练可用性。
  - 产品启示：新求解器早期需配套任务级回归测试，避免发散类问题扩散到其他环境。

6/10-[Bump] usd-exchange 3.0.0 and drop the OpenUSD work-thread-limit workaround (#7192)（225d58f）
  - 评分：6/10
  - 一句话总结：升级 usd-exchange 至 3.0.0 并移除 OpenUSD 工作线程限制兼容逻辑。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/225d58f546dde720cbf031ea382f0ecb1cd2a638
  - 变更规模：+47 -61
  - 提交者：hujc
  - 解决的问题：旧版 usd-exchange 需要 OpenUSD 工作线程限制绕过逻辑，增加维护负担。
  - 产品启示：依赖升级简化了兼容层，但需关注版本漂移与平台兼容性回归风险。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 25 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +1772 / -367 行
- 主要贡献者: Eric Shi, Gilles Daviet, Zhihui Du

## 🧭 趋势点评
本周更新延续了仓库近半年“高频迭代、稳步优化、以工程健壮性为主线”的演进特征，并进一步聚焦于底层数值稳定性与运行时开销削减。`Reduce Python built-in call overhead` 与 `Preserve BSR and FEM performance` 承接了 2026-09 以来对 Python 调用开销、BSR/FEM 性能的连续投入，属于既有性能主线的自然延伸；`Stabilize FEM QR decompositions` 与 `Fix tile min/max scans on float extremes and uint32` 则延续了 2026-07 以来对数值精度与边界条件（批量归约、四元数扭转角、FEM QR）的加固路径，体现出“性能优化与数值正确性并重”的一贯取向。`Restore mesh ray-query occupancy` 属于对 2026-06 mesh ray BVH 遍历优化的回归修复，说明底层性能改动带来的回归风险正在被持续监控与回补，整体未偏离仓库长期趋势，反而强化了“优化—回归—修复”的闭环。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周无符合评分≥6的新功能/特性类提交）

### ⚡️ 性能/架构优化
6/10-Reduce Python built-in call overhead [GH-1983]（7906779）
  - 评分：6/10
  - 一句话总结：通过降低 Python 内建调用开销，减少运行时解释层开销。
  - 链接：https://github.com/NVIDIA/warp/commit/79067793efd89e3bd69b960c73781ccc4ac13c7f
  - 变更规模：+93 -21
  - 提交者：Eric Shi
  - 解决的问题：Python 内建调用路径开销偏高，影响运行时性能。
  - 产品启示：直接降低仿真与 RL 场景中高频 Python 调用路径的延迟，提升框架在脚本化控制与大规模并行仿真中的响应效率。

6/10-Preserve BSR and FEM performance [GH-1918]（c59167b）
  - 评分：6/10
  - 一句话总结：在相关改动后保持 BSR 与 FEM 的性能不退化。
  - 链接：https://github.com/NVIDIA/warp/commit/c59167bbec2d78e1bd07e7af3d714ecce241d2ed
  - 变更规模：+10 -6
  - 提交者：Eric Shi
  - 解决的问题：BSR 与 FEM 路径在迭代中可能出现性能回退。
  - 产品启示：保障稀疏求解与 FEM 仿真常用负载的吞吐稳定性，对机器人仿真与物理求解场景的可持续性能至关重要。

### 🐛 Bug修复 / 其他
7/10-Stabilize FEM QR decompositions (GH-1985)（a596470）
  - 评分：7/10
  - 一句话总结：稳定 FEM QR 分解，提升数值稳定性。
  - 链接：https://github.com/NVIDIA/warp/commit/a596470bafe6805c10fb2ce83ba47857253d37dd
  - 变更规模：+344 -28
  - 提交者：Gilles Daviet
  - 解决的问题：FEM QR 分解在数值上不稳定，可能影响求解精度。
  - 产品启示：直接提升 FEM 求解器的数值可靠性，对依赖 FEM 的物理仿真与机器人建模场景具有关键价值。

6/10-Fix tile min/max scans on float extremes and uint32 [GH-2003]（13f9a11）
  - 评分：6/10
  - 一句话总结：修复 tile min/max 扫描在浮点极值与 uint32 下的错误行为。
  - 链接：https://github.com/NVIDIA/warp/commit/13f9a110a93daac987042a9e3dd213549d0e15c0
  - 变更规模：+158 -4
  - 提交者：Christopher Crouzet
  - 解决的问题：tile 扫描在浮点极值与 uint32 输入下结果不正确。
  - 产品启示：提升 tile 级归约在极端数值与无符号整型场景下的正确性，增强数值边界条件下的可靠性。

6/10-Restore mesh ray-query occupancy [GH-1840]（45c001d）
  - 评分：6/10
  - 一句话总结：恢复网格射线查询的占用率，修复此前优化带来的回退。
  - 链接：https://github.com/NVIDIA/warp/commit/45c001d47199f83ae11d8ae798ba7da3e7b2ce31
  - 变更规模：+29 -18
  - 提交者：Eric Shi
  - 解决的问题：mesh ray-query 占用率下降，影响空间查询性能。
  - 产品启示：保障空间查询在碰撞检测、射线投射等机器人仿真常用负载中的性能稳定性。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 14 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +1862 / -613 行
- 主要贡献者: liuke, Andy Lin, panhe1818

## 🧭 趋势点评
本周更新延续了 RLinf 在具身智能全栈能力上的快速扩张主线：Robotwin DAgger 的接入（7d2dfa7）与 Cosmos3 SFT/SGLang 评估示例的修复（010990e）继续拓宽仿真环境与模型覆盖范围，与基线中“新功能优先、生态接入密集”的演进特征高度一致；同时 FSDP 相关的两项修复（dec2377、20ad900）以及 VLM SFT 对 transformers 5 的适配（d1bf37c）则呼应了基线中反复出现的 FSDP 稳定性治理与依赖兼容性压力，说明项目在功能堆叠的同时正被动加大训练基础设施的修复投入。整体看，本周并未偏离长期趋势，但 FSDP 检查点与分片恢复类修复的集中出现，进一步印证了基线中“性能与稳定性治理滞后于功能扩张”的潜在风险。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-feat: support new Dagger in Robotwin (#1551)（7d2dfa7）
  - 评分：7/10
  - 一句话总结：为 Robotwin 仿真环境新增 DAgger 支持，扩展了真机/仿真数据采集闭环的覆盖范围。
  - 链接：https://github.com/RLinf/RLinf/commit/7d2dfa77faffa7887304670d5fcaed1128b84ae8
  - 变更规模：+265 -37
  - 提交者：renji555
  - 解决的问题：此前 DAgger 流程主要覆盖真实双 Franka 与在线 LeRobot 采集，Robotwin 侧缺乏对应支持，导致仿真环境下的交互式数据采集能力缺失。
  - 产品启示：Robotwin DAgger 的加入使仿真侧数据采集与真机流程对齐，有助于在低成本仿真中预训练与验证 DAgger 策略，建议后续补齐对应文档与示例配置以降低使用门槛。

### ⚡️ 性能/架构优化
- 无（本周高价值提交中未包含明确的性能/架构优化类条目）。

### 🐛 Bug修复 / 其他
7/10-fix(cosmos3): make the Cosmos3 SFT and SGLang eval examples run (#1602)（010990e）
  - 评分：7/10
  - 一句话总结：修复 Cosmos3 SFT 与 SGLang 评估示例无法运行的问题，并同步更新中英文文档与 CI。
  - 链接：https://github.com/RLinf/RLinf/commit/010990e5c81ae17d141d3eab584a3bd1791df950
  - 变更规模：+763 -60
  - 提交者：Andy Lin
  - 解决的问题：Cosmos3 的 SFT 与 SGLang 评估示例存在运行障碍，影响用户按文档复现世界模型训练与评测流程。
  - 产品启示：Cosmos3 作为世界模型主线之一，其示例可运行性直接影响生态接入体验，建议将 SFT/SGLang 评估示例纳入 e2e 测试，确保文档与代码同步演进。

---

6/10-fix(fsdp): preserve per-rank RNG in DCP checkpoints (#1570)（dec2377）
  - 评分：6/10
  - 一句话总结：修复 DCP 检查点未保留各 rank 随机数状态的问题，保障断点续训的随机性一致性。
  - 链接：https://github.com/RLinf/RLinf/commit/dec2377bb8fa726827b36b12bb99cbfba12657dd
  - 变更规模：+46 -6
  - 提交者：liuke
  - 解决的问题：DCP 检查点保存/恢复时未按 rank 保留 RNG 状态，可能导致恢复训练后各 rank 随机行为不一致，影响可复现性与训练稳定性。
  - 产品启示：RNG 一致性是分布式训练可复现性的基础，建议将 per-rank RNG 校验纳入自动化回归测试，避免类似问题在多卡大规模训练中隐性累积。

6/10-fix(fsdp2): restore local shards as distributed tensors (#1569)（20ad900）
  - 评分：6/10
  - 一句话总结：修复 FSDP2 恢复时将本地分片还原为分布式张量的问题，并同步更新 resume 文档。
  - 链接：https://github.com/RLinf/RLinf/commit/20ad900fb8350bb53c980cbdc761d8b5caabb99a
  - 变更规模：+79 -11
  - 提交者：liuke
  - 解决的问题：FSDP2 检查点恢复时本地分片未正确还原为分布式张量，可能导致恢复后参数布局错误或训练异常。
  - 产品启示：FSDP2 分片恢复是长周期训练的关键路径，建议结合基线中提到的 RLINF_TIMEOUT 与梯度范数分片归约，构建统一的 FSDP 恢复回归用例集。

6/10-fix(vlm): support transformers 5 in VLM SFT (#1610)（d1bf37c）
  - 评分：6/10
  - 一句话总结：适配 transformers 5 版本，修复 VLM SFT 在新版依赖下的运行问题。
  - 链接：https://github.com/RLinf/RLinf/commit/d1bf37cdc73bba24218d523b08c1c88fcffd9deb
  - 变更规模：+178 -301
  - 提交者：sherlockcooper
  - 解决的问题：transformers 5 引入的接口变更导致 VLM SFT 流程不兼容，同时涉及 CI 工作流与 mbridge 文档同步调整。
  - 产品启示：依赖大版本升级对 VLM SFT 影响面较大，建议在 pyproject 中明确 transformers 版本约束并补充兼容性矩阵文档，降低上游破坏性变更带来的维护成本。

