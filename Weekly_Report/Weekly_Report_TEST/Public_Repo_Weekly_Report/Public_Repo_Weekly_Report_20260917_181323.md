# 具身智能周报 (2026年09月17日 18:13:23)

## 行业风向总览

本周具身智能行业风向呈现“仿真底座加固、训练栈收敛、真机奖励闭环”三条主线。技术焦点上，MuJoCo 修复焊接约束力矩与 Hessian 主元舍入问题，IsaacLab 修复 OVPhysX 静态属性重复读取与 Newton VBD 图着色挂起，Warp 为 tile_matmul 接入 cuBLASDx 对齐算子并约束图着色平衡，显示底层求解器与 GPU 执行路径正从“能跑”转向“稳定可预测”。合成数据方面，本周无直接合成数据管线更新，但 MuJoCo Warp 碰撞代码并入 MJX、IsaacLab 升级 Newton 1.6.0 与 OvStage 兼容层，实质是在为大规模并行仿真生成训练数据铺路；RLinf 的 QwenTrend 奖励流水线与 Franka Qwen VLM 奖励模型，则把 VLM 奖励建模推向真机闭环。产品经理需关注：一是 MuJoCo Studio 移除经典渲染器、IsaacLab 弃用 isaaclab.sh，旧工作流迁移成本上升；二是 IsaacLab 锁定 PyTorch 栈、Warp 保留 PyTorch 视图别名，跨框架内存语义与依赖锁定成为可复现性关键；三是 RLinf 功能扩张快于性能优化，分布式通信与权重同步可能成为下一阶段瓶颈。

---

## 各仓库详细分析

### [mujocolab/mjlab] 本周无新提交。


---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 52 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +13740 / -5837 行
- 主要贡献者: Yuval Tassa, Matija Kecman, Haroon Qureshi

## 🧭 趋势点评
本周更新延续了该仓库“核心引擎数值稳健性 + 生态工具链扩张”的双主线：一方面，`ac329bd` 修复焊接约束力矩、`35c0631` 处理 Hessian 主元舍入丢失，延续了 2026 年 6-9 月以来对求解器与约束数值稳定性的持续投入（如 Nesterov 动量、CG 线搜索重构、Hessian 锥贡献折叠）；另一方面，`71d430c` 将 MuJoCo Warp 核心碰撞代码导入 MJX 第三方目录，进一步落实了基线中“MJX/MuJoCo Warp 生态持续扩展”的预测方向。`95eb305` 移除 Studio 经典渲染器则与基线中“Studio/Web Viewer 成为主要交互入口并持续重构为平台化架构”的趋势一致，属于渲染路径收敛的架构清理动作。整体看，本周更新未偏离长期趋势，而是对既有求解器稳定性、GPU 后端集成与 Studio 平台化三条主线的具体推进。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Import google-deepmind/mujoco_warp from GitHub.（71d430c）
  - 评分：8/10
  - 一句话总结：将 MuJoCo Warp 的核心碰撞相关代码导入 MJX 第三方目录，强化 GPU 后端碰撞能力。
  - 链接：https://github.com/google-deepmind/mujoco/commit/71d430c71f8593a977136485e81314ec19a66e7e
  - 变更规模：+138 -32
  - 提交者：Google DeepMind
  - 解决的问题：MJX 侧此前缺少与 MuJoCo Warp 同步的凸碰撞、GJK、约束与导数实现，导致 GPU 后端碰撞路径与主仓库能力脱节。
  - 产品启示：MuJoCo Warp 正从独立实验项目向 MJX 内置能力收敛，未来 GPU 加速仿真与碰撞检测将成为 MJX 的默认能力之一，需关注其与主引擎碰撞语义的一致性。

### ⚡️ 性能/架构优化
6/10-Remove classic renderer support from Studio.（95eb305）
  - 评分：6/10
  - 一句话总结：从 Studio 中移除经典渲染器支持，收敛到 Filament 渲染路径。
  - 链接：https://github.com/google-deepmind/mujoco/commit/95eb3057a9eefd7cbac85a3a87d9e13172d0562d
  - 变更规模：+22 -430
  - 提交者：Haroon Qureshi
  - 解决的问题：Studio 同时维护经典渲染器与 Filament 两套路径，带来代码冗余、行为不一致与维护成本。
  - 产品启示：Studio 渲染架构正式向 Filament 单一路径收敛，与基线中“Filament 渲染、Web Viewer 平台化”方向一致，后续需关注经典渲染器移除对旧用户工作流与跨平台（WASM/headless）行为的影响。

### 🐛 Bug修复 / 其他
8/10-Fix the torque of weld constraints in mj_rnePostConstraint.（ac329bd）
  - 评分：8/10
  - 一句话总结：修复 `mj_rnePostConstraint` 中焊接约束的力矩计算错误。
  - 链接：https://github.com/google-deepmind/mujoco/commit/ac329bd17456ac4a9cf5f0c95ab452f7e11e70a6
  - 变更规模：+288 -9
  - 提交者：Yuval Tassa
  - 解决的问题：焊接约束在逆动力学后处理阶段产生的力矩不正确，影响含焊接约束模型的动力学一致性与仿真可信度。
  - 产品启示：焊接约束是刚体装配与机器人建模的高频特性，该修复直接关系到仿真结果的物理正确性，需同步关注 MJX 与 MuJoCo Warp 侧 `smooth.py` 的一致性回归。

8/10-Clamp and decouple a Hessian pivot lost to rounding instead of aborting Newton.（35c0631）
  - 评分：8/10
  - 一句话总结：在 Newton 求解中，对因舍入丢失的 Hessian 主元进行钳制与解耦，而非直接中止。
  - 链接：https://github.com/google-deepmind/mujoco/commit/35c0631dea406b2c8a0c71b427051b0879f01340
  - 变更规模：+109 -17
  - 提交者：Yuval Tassa
  - 解决的问题：Hessian 主元因浮点舍入丢失时，原逻辑会中止 Newton 迭代，导致求解器在病态或大规模模型下提前失败。
  - 产品启示：延续了基线中“求解器数值稳定性与速度联合改进”的方向，提升了 Newton 求解在 float32 与病态问题下的鲁棒性，需关注其对收敛轨迹与既有回归基准的影响。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 44 条
- 高价值提交（≥6分）: 10 条
- 代码更新规模: +13652 / -3225 行
- 主要贡献者: Kelly Guo, Mustafa H, isaaclab-bot[bot]

## 🧭 趋势点评
本周更新延续了 IsaacLab 在基线周期内确立的“多物理后端并行演进 + 性能与测试基础设施加固”主线，并进一步向依赖锁定与运行时稳定性收敛。Newton 升级至 1.6.0、RSL-RL 升至 5.5.1、PyTorch 栈固定，说明项目在快速扩张后正主动收紧版本边界以降低环境漂移风险；同时 OVPhysX 静态属性重读修复、Newton VBD 图着色挂起规避、视频捕获间持续渲染抑制等提交，表明性能优化已从零散修补转向针对具体后端与运行时路径的系统性治理。弃用 isaaclab.sh 与旧版 RSL-RL 配置、OvStage 0.2.0 兼容层引入，则延续了架构清理与后端抽象统一的长期方向，整体未偏离基线，而是在多后端兼容性与工程可复现性上继续深化。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-[Bump] Bump Newton to 1.6.0 (#7842)（94a8ad5）
  - 评分：7/10
  - 一句话总结：将 Newton 物理后端升级至 1.6.0，并同步更新依赖锁定与 CI 安装覆盖文件。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/94a8ad5ea37b214857f5d7b670d1d7637c8b8094
  - 变更规模：+19 -17
  - 提交者：Kelly Guo
  - 解决的问题：解决 Newton 后端版本滞后问题，确保与最新 Newton 1.6.0 特性及修复对齐。
  - 产品启示：多后端生态需持续跟进上游版本，版本升级应配套 CI 覆盖与 wheel 构建校验，降低下游适配成本。

6/10-Add OvStage compat for GPU_INCREMENTAL in OvStage 0.2.0 (#7855)（2867f6b）
  - 评分：6/10
  - 一句话总结：为 OvStage 0.2.0 新增 GPU_INCREMENTAL 兼容层，支持 GPU 层级计算路径。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/2867f6b1fa97ebeb9fc5774d0e4797eb08fb2984
  - 变更规模：+268 -7
  - 提交者：r-schmitt
  - 解决的问题：解决 OvStage 0.2.0 引入 GPU_INCREMENTAL 后旧接口不兼容的问题。
  - 产品启示：渲染/Stage 后端升级需提供兼容层与测试，保障用户平滑迁移。

6/10-[RL] Update RSL-RL to 5.5.1 (#7825)（480398d）
  - 评分：6/10
  - 一句话总结：将 RSL-RL 依赖升级至 5.5.1，并更新 uv.lock。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/480398dd84bfe45f5cbe16b0696de02d972ecaa9
  - 变更规模：+7 -15
  - 提交者：Mustafa H
  - 解决的问题：解决 RL 训练栈版本落后问题，保持与 RSL-RL 最新发布同步。
  - 产品启示：RL 工具链需持续跟进上游，版本升级应同步锁定文件以保证可复现性。

### ⚡️ 性能/架构优化
7/10-Fix OVPhysX re-reading static joint and body properties every step (#7800)（416a1d1）
  - 评分：7/10
  - 一句话总结：修复 OVPhysX 每步重复读取静态关节与刚体属性的问题，减少运行时开销。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/416a1d146d9de293e22e7775af125b9d2cad7516
  - 变更规模：+131 -10
  - 提交者：Antoine RICHARD
  - 解决的问题：解决 OVPhysX 在每步仿真中重复读取静态属性导致的性能浪费。
  - 产品启示：后端性能优化需关注静态数据缓存，避免每步重复读取造成隐性开销。

6/10-Deprecate isaaclab.sh and legacy RSL-RL configs (#7820)（243659e）
  - 评分：6/10
  - 一句话总结：弃用 isaaclab.sh 与旧版 RSL-RL 配置，推动用户迁移至新工作流。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/243659ee0a6929c91998119f408488280e06007e
  - 变更规模：+27 -3
  - 提交者：Mustafa H
  - 解决的问题：解决旧启动脚本与遗留 RSL-RL 配置长期维护负担问题。
  - 产品启示：架构清理需配套弃用提示与迁移文档，降低用户升级阻力。

6/10-Avoid continuous rendering between video captures (#7642)（270ef40）
  - 评分：6/10
  - 一句话总结：在视频捕获间隔避免持续渲染，降低无头模式下的空闲渲染开销。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/270ef409eed379377aaf7c6846fe4d52649f4928
  - 变更规模：+111 -1
  - 提交者：Antoine RICHARD
  - 解决的问题：解决无头视频录制期间持续渲染导致的资源浪费问题。
  - 产品启示：渲染路径优化应关注空闲态行为，避免不必要的 GPU 占用。

### 🐛 Bug修复 / 其他
7/10-Fix Newton joint positions in DOF space, and enable the Digit velocity tasks (#7520)（9d1896d）
  - 评分：7/10
  - 一句话总结：修复 Newton 中 DOF 空间关节位置计算，并启用 Digit velocity 任务。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/9d1896d3e4ee9438807ea2d953f24ec0c2c0ae8b
  - 变更规模：+731 -71
  - 提交者：Henry Hu
  - 解决的问题：解决 Newton 后端球关节 DOF 空间位置错误，并恢复 Digit velocity 任务可用性。
  - 产品启示：后端正确性修复需同步启用相关任务，验证修复效果并扩展可用任务集。

6/10-Avoid Newton VBD graph coloring hangs (#7826)（0c12bab）
  - 评分：6/10
  - 一句话总结：修复 Newton VBD 图着色挂起问题，提升仿真稳定性。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/0c12babce3226144fa5da987c77352197721346f
  - 变更规模：+15 -9
  - 提交者：Maximilian Krause
  - 解决的问题：解决 Newton VBD 图着色过程中可能出现的挂起问题。
  - 产品启示：实验性后端需加强边界条件测试，避免挂起类问题影响用户体验。

6/10-Pin the published PyTorch stack to the supported versions (#7821)（538a409）
  - 评分：6/10
  - 一句话总结：将已发布 PyTorch 栈固定到受支持版本，避免环境漂移。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/538a4093c54ec32341d2bcc76489d70c71185c8b
  - 变更规模：+29 -40
  - 提交者：Mustafa H
  - 解决的问题：解决 PyTorch 版本未锁定导致的安装环境不一致问题。
  - 产品启示：依赖锁定是保障可复现性的关键，发布流程应固定核心栈版本。

6/10-Fix implicit effort submission in ovphysx (#7782)（e86463d）
  - 评分：6/10
  - 一句话总结：修复 ovphysx 中隐式力提交问题，并更新 golden images 跳过标记。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/e86463df8a8d8dff275e50fdcfd892e10ba32ec1
  - 变更规模：+69 -21
  - 提交者：Alesiani Marco
  - 解决的问题：解决 ovphysx 隐式力提交错误导致的执行器控制异常。
  - 产品启示：后端执行器控制需与渲染 golden 测试联动，确保修复不引入视觉回归。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 48 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +25991 / -6596 行
- 主要贡献者: Eric Shi, Christopher Crouzet, Zach Corse

## 🧭 趋势点评

本周更新延续了 Warp 在“编译/运行时底层优化 + 生态互操作加固 + 新硬件平台适配”三条主线上的长期演进路径，但重心略有偏移：一方面，cuBLASDx 算子对齐（84a08e1）与图着色平衡（1bf6520）继续强化 tile 计算与图执行这两大性能敏感环节，呼应了基线中“性能优化集中于编译期与内存管理”的判断；另一方面，PyTorch 视图别名保持（90a3dc1）、Python 作用域 identity dtype 修复（8bd895a）与 32 位整数纹理采样拒绝（a46feac）表明项目正从单纯追求性能转向语义正确性与跨框架行为一致性，这与基线中“PyTorch/JAX 互操作”方向高度吻合。Windows ARM64 CUDA 13.4 wheel 构建（c796004）则直接延续了 CUDA 13.x 工具链与 ARM64 平台覆盖的密集适配趋势。整体看，本周未出现偏离长期趋势的重大转向，而是对既有方向的精细化收尾与稳健性补强。

## 🔍 关键更新解析

### 🚀 新功能/特性

8/10-Set cuBLASDx Alignment and StaticBlockDim operators for tile_matmul() [GH-1938]（84a08e1）
  - 评分：8/10
  - 一句话总结：为 tile_matmul 设置 cuBLASDx 的 Alignment 与 StaticBlockDim 算子，提升 tile 矩阵乘法性能。
  - 链接：https://github.com/NVIDIA/warp/commit/84a08e12e3909d5eb7552c1f2c0f6c5cc4d59dba
  - 变更规模：+637 -53
  - 提交者：Zach Corse
  - 解决的问题：tile_matmul 在 cuBLASDx 后端缺少对齐与静态块维度配置，导致无法充分利用硬件矩阵运算能力。
  - 产品启示：tile 抽象与 cuBLASDx 深度绑定，意味着 Warp 正把高性能矩阵运算作为仿真与 RL 训练的核心卖点，后续 tile 相关 API 的稳定性与文档一致性需同步跟进。

6/10-Build Windows ARM64 wheels with CUDA 13.4（c796004）
  - 评分：6/10
  - 一句话总结：新增 Windows ARM64 平台下基于 CUDA 13.4 的 wheel 构建支持。
  - 链接：https://github.com/NVIDIA/warp/commit/c796004251adecd133944d1a16956a0b48752642
  - 变更规模：+58 -22
  - 提交者：Eric Shi
  - 解决的问题：此前 Windows ARM64 平台缺少 CUDA 13.4 的预编译 wheel，用户需自行编译，部署门槛高。
  - 产品启示：ARM64 + CUDA 13.4 的组合覆盖表明 Warp 正积极适配新一代边缘与异构硬件，跨平台可复现构建能力成为生态扩展的前置条件。

### ⚡️ 性能/架构优化

7/10-Bound graph color balancing [GH-1964]（1bf6520）
  - 评分：7/10
  - 一句话总结：为图着色平衡引入上界约束，防止着色结果导致性能退化。
  - 链接：https://github.com/NVIDIA/warp/commit/1bf652059b9e7f8b391123b4a118e2b02ec1b8be
  - 变更规模：+371 -20
  - 提交者：Eric Shi
  - 解决的问题：图着色平衡缺乏边界控制，可能生成极端不平衡的着色方案，反而拖慢图执行性能。
  - 产品启示：图执行与内存管理是 Warp 大规模仿真的瓶颈之一，此类“防退化”约束说明优化已从单纯提速进入稳定性与可预测性并重阶段。

### 🐛 Bug修复 / 其他

7/10-Preserve PyTorch view aliasing [GH-1908]（90a3dc1）
  - 评分：7/10
  - 一句话总结：修复 Warp 与 PyTorch 互操作时视图别名关系丢失的问题。
  - 链接：https://github.com/NVIDIA/warp/commit/90a3dc13c72d7bf520a80bb4da6edae3db670832
  - 变更规模：+163 -28
  - 提交者：Eric Shi
  - 解决的问题：Warp 数组与 PyTorch 张量互转时未保留 view 别名，可能导致原地修改不同步或内存语义错误。
  - 产品启示：PyTorch 互操作是 Warp 进入 RL 训练栈的关键通道，别名语义正确性直接影响用户对零拷贝与内存共享的信任。

6/10-Honor dtype in Python-scope identity built-ins [GH-1839]（8bd895a）
  - 评分：6/10
  - 一句话总结：修复 Python 作用域下 identity 内建函数未遵循输入 dtype 的问题。
  - 链接：https://github.com/NVIDIA/warp/commit/8bd895a2a28ca5698e83d35605bcc43189504118
  - 变更规模：+369 -52
  - 提交者：Christopher Crouzet
  - 解决的问题：Python 作用域调用 identity 类内建函数时忽略 dtype，导致类型推断与内核行为不一致。
  - 产品启示：类型系统一致性是 Warp 作为 DSL 的根基，此类修复降低了用户在内核与 Python 作用域间切换时的隐式陷阱。

6/10-Refuse to sample 32-bit integer textures [GH-1731]（a46feac）
  - 评分：6/10
  - 一句话总结：明确拒绝采样 32 位整数纹理，避免不支持的采样行为。
  - 链接：https://github.com/NVIDIA/warp/commit/a46feaceb4dac5761500d063d32f20ae4db7ec62
  - 变更规模：+304 -47
  - 提交者：Christopher Crouzet
  - 解决的问题：此前对 32 位整数纹理的采样行为未定义或静默失败，易引发难以排查的渲染/仿真错误。
  - 产品启示：显式拒绝而非静默容错，体现了 Warp 在图形与仿真交叉场景中对行为可预测性的重视，也提示纹理 API 的边界条件需在文档中同步澄清。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 13 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +14552 / -4001 行
- 主要贡献者: Andy Lin, zhengjia, wolf

## 🧭 趋势点评
本周更新延续了 RLinf 在“多模型/多后端横向扩张 + 系统架构重构”这一长期主线：FastWAM 评测与 FSDP SFT、QwenTrend 奖励流水线、OpenPI LIBERO 的 ApxInf 后端、Franka 上的 Qwen VLM 奖励模型，均属于基线中反复出现的“模型与算法覆盖持续扩张”“真实世界与仿真环境并行推进”方向；而 openpi_rlinf 的大规模重构与算法迁移，则与 2026-09 基线中“重构 openpi_rlinf 并迁移算法（025b8b3）”的模块化收敛趋势高度一致。值得注意的是，本周高价值提交中性能/架构优化仅 1 条、其余均为新功能，进一步印证了基线所指出的“性能优化提交占比偏低（约 3.0%）”这一结构性特征——功能扩张速度仍明显快于系统性性能打磨，分布式通信、权重同步与内存管理等关键路径的优化压力可能继续累积。

## 🔍 关键更新解析

### 🚀 新功能/特性

9/10-feat(embodied): add FastWAM evaluation and FSDP SFT support (#1398)（ee2cab6）
  - 评分：9/10
  - 一句话总结：为 FastWAM 补齐评测与 FSDP SFT 训练支持，扩展具身模型的训练与评估闭环。
  - 链接：https://github.com/RLinf/RLinf/commit/ee2cab65adfc836305b258da44fab2679179e1ae
  - 变更规模：+2339 -10
  - 提交者：wolf
  - 解决的问题：此前 FastWAM 缺乏配套的评测流程与 FSDP SFT 训练路径，难以纳入统一流水线。
  - 产品启示：将新模型接入标准化 SFT/评测链路，可降低后续模型接入成本，强化“模型即插即用”的平台定位。

8/10-feat(reward): add QwenTrend reward pipeline (#1395)（c9e8067）
  - 评分：8/10
  - 一句话总结：新增 QwenTrend 奖励流水线，为 VLM 奖励建模提供端到端配置与文档。
  - 链接：https://github.com/RLinf/RLinf/commit/c9e80673265b88a3eaf97d8dd3726d081ad3a889
  - 变更规模：+3234 -134
  - 提交者：NLC2004
  - 解决的问题：奖励模型侧缺少统一的 VLM 趋势类奖励管线，跨任务（LIBERO、ManiSkill）配置分散。
  - 产品启示：奖励建模正成为独立可复用能力，标准化 pipeline 有助于 RL 训练与真实世界任务共享同一奖励基础设施。

7/10-feat(eval): add ApxInf backend for OpenPI LIBERO evaluation (#1537)（1dcbc56）
  - 评分：7/10
  - 一句话总结：为 OpenPI 在 LIBERO 上的评测新增 ApxInf 推理后端。
  - 链接：https://github.com/RLinf/RLinf/commit/1dcbc56b4e25401c89f19f691f809a6369a167a0
  - 变更规模：+1042 -2
  - 提交者：Chenxi He
  - 解决的问题：OpenPI LIBERO 评测后端单一，缺少可切换的推理适配层与对应配置。
  - 产品启示：评测后端可插拔化有利于跨推理引擎对比，提升基准结论的可信度与复现性。

7/10-feat(franka): support qwen vlm franka reward model (#1428)（9092957）
  - 评分：7/10
  - 一句话总结：在 Franka 真机场景中支持 Qwen VLM 奖励模型。
  - 链接：https://github.com/RLinf/RLinf/commit/90929570efd7f42958de410a98e040578b822781
  - 变更规模：+1107 -68
  - 提交者：yang
  - 解决的问题：真实世界 peg insertion 等任务缺少 VLM 奖励模型支持，奖励信号依赖人工或简单函数。
  - 产品启示：将 VLM 奖励引入真机 RL，是仿真到真机闭环的关键一环，也强化了真实世界数据与奖励建模的协同。

### ⚡️ 性能/架构优化

8/10-feat: refactor openpi_rlinf and migrate algorithms (#1512)（025b8b3）
  - 评分：8/10
  - 一句话总结：重构 openpi_rlinf 模块并迁移相关算法，统一代码边界与配置结构。
  - 链接：https://github.com/RLinf/RLinf/commit/025b8b32ca402e268b190742d8c4d3b906fdb1d2
  - 变更规模：+3940 -2527
  - 提交者：guozhen
  - 解决的问题：openpi_rlinf 相关算法与配置分散、职责不清，维护与扩展成本高。
  - 产品启示：模块化重构是支撑多模型、多后端快速接入的前提，但需配套回归测试以防重构期引入行为回归。

### 🐛 Bug修复 / 其他
本周高价值提交中无 Bug 修复 / 其他类条目。

---

