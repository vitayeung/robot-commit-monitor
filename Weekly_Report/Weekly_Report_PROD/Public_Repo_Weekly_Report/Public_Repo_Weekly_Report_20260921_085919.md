# 具身智能周报 (2026年09月21日 08:59:19)

## 行业风向总览

本周具身智能行业呈现“仿真引擎收敛稳定性、训练框架扩张异构算力”的双主线。

**技术焦点**：MuJoCo 进入功能扩展后的稳定性收敛期，重点修复 MIMO 执行器控制历史、椭球流体力学归一化、flex 弹簧阻尼标志等跨后端数值一致性问题，MJX 与 C 引擎语义对齐成为治理重点。IsaacLab 则处于 3.0 发布前收口阶段，大规模清理 isaaclab_rl 与 isaaclab_tasks 接口，弃用旧物理 schema，同时新增 TorchRL 环境包装器与 Newton OpenCV 镜头畸变渲染。Warp 将自动微分检查点机制落地到流体仿真，并接入 cuBLASDx 算子优化 tile_matmul。

**合成数据动态**：本周无直接合成数据管线更新，但 IsaacLab 的镜头畸变渲染缩小了仿真与真实相机差距，Warp 的流体检查点反向传播为可微仿真数据生成提供内存优化范式，均间接增强合成数据真实性。

**产品经理关注信号**：RLinf 密集落地 Ascend NPU、Biren SUPA、昆仑芯、ROCm/MUSA 等异构算力支持，并统一世界模型后端、重构权重同步，Franky 成为默认 Franka 配置，FastWAM、QwenTrend 奖励流水线接入——多算力平台适配与全链路生态覆盖正成为具身 RL 框架的核心竞争力。同时 IsaacLab 3.0 破坏性变更与 PyTorch 2.12 升级需提前规划迁移。

---

## 各仓库详细分析

### [mujocolab/mjlab] 本周无高价值更新（≥6分）。

#### 📊 提交分析
- 本周总提交: 1 条
- 高价值提交: 0 条
- 代码更新规模: +213 / -129 行
- 主要贡献者: Guilhem Saurel

#### 🧭 趋势点评
本周共有 1 条常规提交，主要涉及代码维护与小幅优化，无值得重点关注的功能或性能更新。


---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 58 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +8626 / -5160 行
- 主要贡献者: Yuval Tassa, Haroon Qureshi, Alessio Quaglino

## 🧭 趋势点评
本周更新延续了仓库“核心引擎数值精进 + 生态集成扩展”的双主线，但在方向上出现了值得注意的偏移：一方面，MIMO 执行器控制历史（dc8bb13）与归档资源提供者（2fec922）分别从建模能力与资产管线两端扩展了 API 边界，呼应了基线中“模型编辑与资产管线增强”的预测方向；另一方面，椭球流体力学归一化（b9ff593）、flex 拉伸力禁用标志（35b8d7c）与 MJX 伺服旋转设定点环绕（857e15a）三项修复/特性同时覆盖 C 引擎与 MJX/Warp 第三方路径，表明项目正在加强对跨后端数值一致性的治理，这与基线中“MJX/Warp 与 Python 生态扩展”的趋势高度吻合。值得注意的是，本周高价值提交中未出现求解器或碰撞检测的性能突破，性能优化节奏较 2026-06 至 2026-09 的密集期有所放缓，重心转向正确性修复与 API 语义完善，属于典型的“功能扩展后的稳定性收敛期”。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Support multi-input (MIMO) actuators in control history buffers and mj_readCtrl.（dc8bb13）
  - 评分：8/10
  - 一句话总结：为控制历史缓冲与 `mj_readCtrl` 增加多输入（MIMO）执行器支持，补齐了执行器控制读取的语义完整性。
  - 链接：https://github.com/google-deepmind/mujoco/commit/dc8bb13649fa7d5b6c54403e5d3dc58fda84d820
  - 变更规模：+372 -67
  - 提交者：Yuval Tassa
  - 解决的问题：此前控制历史缓冲与 `mj_readCtrl` 无法正确处理多输入执行器，导致 MIMO 场景下控制信号读取不完整或不一致。
  - 产品启示：强化了 MuJoCo 对复杂执行器拓扑（如多自由度驱动、耦合执行器）的建模能力，为下游 RL 与机器人控制工作流提供更精确的控制接口。

8/10-Introduce archive resource providers.（2fec922）
  - 评分：8/10
  - 一句话总结：引入归档资源提供者，使 MuJoCo 可直接从压缩包/归档中加载模型与资产。
  - 链接：https://github.com/google-deepmind/mujoco/commit/2fec922375a5e001a4d844c06ebfdb0f5c5e823b
  - 变更规模：+999 -251
  - 提交者：Sam Haves
  - 解决的问题：此前资源提供者仅支持文件系统等直接路径访问，无法从归档中读取模型资源，限制了模型分发与部署场景。
  - 产品启示：显著增强资产管线能力，便于模型打包分发、云端加载与嵌入式部署，是资源管理抽象层的重要扩展。

6/10-MJX: Implement rotational setpoint wrapping for servos on 3D rotational transmissions.（857e15a）
  - 评分：6/10
  - 一句话总结：在 MJX 中为 3D 旋转传动的伺服实现设定点环绕，修复了角度跨越 ±π 时的控制跳变。
  - 链接：https://github.com/google-deepmind/mujoco/commit/857e15aec960ba3be44e90f211a6a05f83f0b01e
  - 变更规模：+97 -3
  - 提交者：Yuval Tassa
  - 解决的问题：3D 旋转传动伺服在设定点跨越角度周期边界时缺乏环绕处理，导致 MJX 与 C 引擎行为不一致及控制异常。
  - 产品启示：提升 MJX 与主引擎在旋转伺服语义上的一致性，对 GPU 加速的机器人控制训练稳定性有直接价值。

### ⚡️ 性能/架构优化
- 无（本周高价值提交中未包含明确归类为性能/架构优化的条目）

### 🐛 Bug修复 / 其他
6/10-Normalize velocity and semi-axes in ellipsoid fluid forces and derivatives.（b9ff593）
  - 评分：6/10
  - 一句话总结：对椭球流体力学力及其导数中的速度与半轴进行归一化修正，统一了 C 引擎与 MJX/Warp 的计算语义。
  - 链接：https://github.com/google-deepmind/mujoco/commit/b9ff593b71146f9eb9a4b40a96594c362bb8fb53
  - 变更规模：+170 -86
  - 提交者：Yuval Tassa
  - 解决的问题：椭球流体力学力与导数在速度与半轴处理上缺乏归一化，导致数值偏差及 C 引擎与 MJX/Warp 后端结果不一致。
  - 产品启示：提升流体仿真在跨后端（C 引擎、MJX、MuJoCo Warp）下的一致性与数值可靠性，对水下机器人等流体交互场景尤为关键。

6/10-Honor the spring and damper disable flags in flex stretch forces and the discrete metric.（35b8d7c）
  - 评分：6/10
  - 一句话总结：修复 flex 拉伸力与离散度量未遵循弹簧/阻尼禁用标志的问题，使柔性体行为与配置语义一致。
  - 链接：https://github.com/google-deepmind/mujoco/commit/35b8d7c8658c9c2a978e5700d2239d0c70c20504
  - 变更规模：+262 -53
  - 提交者：Alessio Quaglino
  - 解决的问题：flex 拉伸力与离散度量计算忽略了弹簧与阻尼的禁用标志，导致用户禁用相关力后仍被施加，行为与 XML 配置不符。
  - 产品启示：保证柔性体建模中配置标志的语义一致性，避免用户因标志失效而得到非预期仿真结果，提升建模可信度。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 69 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +17484 / -19274 行
- 主要贡献者: Mustafa H, Kelly Guo, ooctipus

## 🧭 趋势点评
本周更新高度契合仓库在 3.0 发布前“接口收敛 + 后端多元化”的长期主线：`isaaclab_rl` 与 `isaaclab_tasks` 的大规模统一清理、旧物理 schema 的弃用，延续了此前数月持续进行的模块合并与 API 精简趋势，属于典型的发布前收口动作；TorchRL 环境包装器与 Newton OpenCV 镜头畸变渲染则延续了 RL 框架扩展与渲染/感知能力增强的方向，进一步丰富多后端生态；PyTorch 升级至 2.12 则延续了依赖与运行时快速迭代的节奏。整体看，本周并未偏离基线，而是把“清理重构”与“新能力引入”两条线同时推进，风险仍集中在破坏性变更与依赖漂移上。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Add TorchRL environment wrapper for isaaclab_rl (#7502)（5c91e9b）
  - 评分：8
  - 一句话总结：为 isaaclab_rl 新增 TorchRL 环境包装器，扩展 RL 框架支持面。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/5c91e9b1e3c79933b3e62c494fb596ab7b7031dd
  - 变更规模：+1141 -43
  - 提交者：theap06
  - 解决的问题：此前 isaaclab_rl 缺少对 TorchRL 的原生适配，用户难以直接接入 TorchRL 训练/回放工作流。
  - 产品启示：RL 接口层向多框架统一收敛，有助于降低用户迁移成本并扩大生态兼容性，是 3.0 训练工作流统一的重要拼图。

7/10-Add OpenCV lens distortion rendering to Newton (#6851)（a68caff）
  - 评分：7
  - 一句话总结：为 Newton 渲染器新增 OpenCV 镜头畸变渲染能力。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/a68caff3dab4e0d45506dbd4b16ca2b75bcbb2f4
  - 变更规模：+287 -28
  - 提交者：Lior Ben Horin
  - 解决的问题：Newton 后端此前无法模拟真实相机镜头畸变，视觉仿真与感知数据真实性受限。
  - 产品启示：渲染与感知能力持续增强，有利于缩小仿真与真实相机差距，提升视觉策略训练与回归验证的可信度。

### ⚡️ 性能/架构优化
9/10-[RL] Unify and cleanup isaaclab_rl for 3.0 release (#7923)（4b1234b）
  - 评分：9
  - 一句话总结：面向 3.0 发布对 isaaclab_rl 进行统一与清理。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/4b1234ba23f80a11f4c5592365f6f0232ebe254a
  - 变更规模：+2674 -3636
  - 提交者：Mustafa H
  - 解决的问题：isaaclab_rl 长期存在接口冗余与不一致，阻碍 3.0 统一训练/回放工作流。
  - 产品启示：RL 模块收敛为单一稳定接口，是 3.0 发布的关键前置条件，但大规模删改也意味着下游用户需同步迁移。

8/10-[Tasks] Final isaaclab_tasks cleanup pass for 3.0 (#7919)（0c5dcbc）
  - 评分：8
  - 一句话总结：对 isaaclab_tasks 进行 3.0 前的最终清理。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/0c5dcbcc6dbe12218bee42d4cb79b60946f74362
  - 变更规模：+2231 -2982
  - 提交者：Mustafa H
  - 解决的问题：任务模块存在冗余配置与不一致模板，影响 3.0 任务体系一致性。
  - 产品启示：任务模板统一精简有助于降低维护成本与用户上手门槛，但任务 ID 与配置变更可能影响既有脚本兼容性。

6/10-Deprecate the legacy physics schema cfgs and writers (#7839)（5889bae）
  - 评分：6
  - 一句话总结：弃用旧版物理 schema 配置与写入器。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/5889bae6e8de7a2b5a6e3ff099f82236d251cd19
  - 变更规模：+1259 -204
  - 提交者：vidurv-nvidia
  - 解决的问题：遗留物理 schema 配置与新 USD 数据类体系并存，造成维护负担与使用混淆。
  - 产品启示：物理 schema 向新体系迁移是资产管线标准化的必要步骤，但弃用会带来向后兼容风险，需配套迁移指南。

### 🐛 Bug修复 / 其他
6/10-Bump PyTorch to 2.12 (#7674)（4269c29）
  - 评分：6
  - 一句话总结：将 PyTorch 升级至 2.12。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/4269c29a39e463dd07c74a9704d890d7a5c01e08
  - 变更规模：+221 -510
  - 提交者：ooctipus
  - 解决的问题：依赖版本落后，需跟进 PyTorch 2.12 以适配新特性与生态兼容性。
  - 产品启示：依赖快速升级保持生态同步，但也带来环境脆弱性与版本漂移风险，需持续验证 CI 与 Docker 稳定性。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 30 条
- 高价值提交（≥6分）: 3 条
- 代码更新规模: +6134 / -1535 行
- 主要贡献者: Eric Shi, Christopher Crouzet, Zhihui Du

## 🧭 趋势点评
本周高价值提交延续了仓库“编译器/运行时底层优化 + 生态互操作增强”的长期主线，但重心明显向**应用层示例与框架集成**偏移：`example_fluid_checkpoint.py` 将自动微分与检查点机制落到流体仿真这一具体场景，`tile_matmul` 接入 cuBLASDx 算子则把此前 tile 系列内建函数的性能优化延伸到库级算子对接，而 PyTorch 视图别名保留修复进一步强化了与主流深度学习框架的内存语义一致性。这与基线中“性能优化多集中在 native/CUDA 底层、文档与 API 快速演进”的趋势一致，但本周更强调**可用的端到端能力**而非单纯内核加速，说明项目正从底层 DSL 向“仿真 + 强化学习基础设施”的成熟期推进。

## 🔍 关键更新解析

### 🚀 新功能/特性

7/10-Add custom fluid checkpoint backward pass [GH-1963]（b1922eb）
- 评分：7/10
- 一句话总结：新增流体仿真检查点反向传播示例，展示自定义梯度与内存-计算权衡的端到端用法。
- 链接：https://github.com/NVIDIA/warp/commit/b1922eba85bd32af5e393c829c0b22e70ea7abea
- 变更规模：+998 -71
- 提交者：Eric Shi
- 解决的问题：为流体仿真这类高内存开销的可微场景提供检查点（checkpointing）反向传播范式，降低训练/优化时的显存占用。
- 产品启示：可作为可微仿真与强化学习工作流的参考模板，推动 warp 在物理 AI 训练管线中的落地。

7/10-Set cuBLASDx Alignment and StaticBlockDim operators for tile_matmul() [GH-1938]（84a08e1）
- 评分：7/10
- 一句话总结：为 `tile_matmul()` 接入 cuBLASDx 的 Alignment 与 StaticBlockDim 算子，提升 tile 矩阵乘法在库级路径上的性能与可控性。
- 链接：https://github.com/NVIDIA/warp/commit/84a08e12e3909d5eb7552c1f2c0f6c5cc4d59dba
- 变更规模：+637 -53
- 提交者：Zach Corse
- 解决的问题：此前 tile 矩阵乘法缺少与 cuBLASDx 算子对齐/静态块维度相关的配置能力，难以充分利用库级优化。
- 产品启示：强化 tile 系列内建函数与 NVIDIA 数学库的协同，为高性能仿真与数值计算提供更优默认路径。

### 🐛 Bug修复 / 其他

6/10-Preserve PyTorch view aliasing [GH-1908]（90a3dc1）
- 评分：6/10
- 一句话总结：修复 PyTorch 视图别名在 warp 互操作路径中丢失的问题，保证张量视图语义一致。
- 链接：https://github.com/NVIDIA/warp/commit/90a3dc13c72d7bf520a80bb4da6edae3db670832
- 变更规模：+163 -28
- 提交者：Eric Shi
- 解决的问题：PyTorch 视图（view）别名关系在 APIC 捕获与类型转换过程中未被保留，可能导致内存语义错误或数据不一致。
- 产品启示：提升与 PyTorch 生态的内存语义兼容性，降低下游用户在混合框架工作流中的调试成本。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 18 条
- 高价值提交（≥6分）: 12 条
- 代码更新规模: +16191 / -6654 行
- 主要贡献者: Andy Lin, Rusty Raven, GanDing

## 🧭 趋势点评
本周更新延续了 RLinf 近半年“多硬件后端扩张 + 世界模型/VLA 生态统一 + 分布式训练基础设施重构”的主线：一方面 Ascend NPU、Biren SUPA、昆仑芯、ROCm/MUSA 等异构算力支持密集落地（#1582、#1581、#1579、#1578、#1525），与基线中“从单一 CUDA 走向异构算力平台”的判断高度一致；另一方面 world models backend 统一（#1518）与 weight-sync placement/reshard 重构（#1520）呼应了基线预测的“世界模型后端收敛”与“集合通信/权重同步优化成为性能主线”。同时，Franky 默认化（#1457）与 FastWAM、QwenTrend、ApxInf 等新模型/评测/奖励流水线接入，进一步强化了真机部署与全链路生态覆盖。值得注意的是，本周出现了熵奖励缩放修复（#1565）这类训练正确性修复，印证了基线中“快速扩张带来回归与配置脆弱性”的风险判断；整体看，本周在延续扩张趋势的同时，也开始在训练稳定性与架构收敛上补课，未偏离长期方向。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-feat(wan): add Ascend NPU support for Wan (#1582)（f26caaa）
  - 评分：8/10
  - 一句话总结：为 Wan 世界模型新增昇腾 NPU 支持，扩展国产算力适配范围。
  - 链接：https://github.com/RLinf/RLinf/commit/f26caaa02597113bb533d459dd2c8a4f7b19946b
  - 变更规模：+346 -12
  - 提交者：GanDing
  - 解决的问题：Wan 此前仅支持 CUDA 生态，无法在 Ascend NPU 上运行。
  - 产品启示：多硬件后端从训练框架向具体模型下沉，NPU 适配成为模型可用性的关键卖点。
8/10-feat(accel): add Biren SUPA accelerator support (#1581)（7b3d874）
  - 评分：8/10
  - 一句话总结：新增壁仞 SUPA 加速器支持，纳入统一加速器抽象层。
  - 链接：https://github.com/RLinf/RLinf/commit/7b3d874945454acfd0785c7c4837a0ad795c391d
  - 变更规模：+248 -50
  - 提交者：Yiming Hu
  - 解决的问题：调度层缺少对 Biren SUPA 硬件的识别与依赖安装支持。
  - 产品启示：加速器抽象层持续扩容，是平台化多算力战略的核心抓手。
8/10-feat(kunlun): support install, docker and ccl for kunlun (#1579)（9f497c5）
  - 评分：8/10
  - 一句话总结：为昆仑芯补齐安装脚本、Docker 镜像与 CCL 集合通信支持。
  - 链接：https://github.com/RLinf/RLinf/commit/9f497c52e626e04c21e79f97d90e90f3903c4fb6
  - 变更规模：+194 -21
  - 提交者：DearFishi
  - 解决的问题：昆仑芯平台缺乏端到端的安装与通信支持，难以落地部署。
  - 产品启示：国产加速器支持需覆盖“安装—镜像—通信”全链路，才能形成可用闭环。
8/10-feat(franka): make Franky the default setup (#1457)（3f71bda）
  - 评分：8/10
  - 一句话总结：将 Franky 设为默认 Franka 配置，统一真机默认工作流。
  - 链接：https://github.com/RLinf/RLinf/commit/3f71bda5fed2f40f27f8c4f238e1a29213085299
  - 变更规模：+2327 -2762
  - 提交者：pear-tree
  - 解决的问题：Franka 配置分散、默认路径不清晰，影响真机上手与 CI 一致性。
  - 产品启示：真机默认配置收敛有助于降低 sim-to-real 门槛并统一测试基线。
8/10-feat(embodied): add FastWAM evaluation and FSDP SFT support (#1398)（ee2cab6）
  - 评分：8/10
  - 一句话总结：新增 FastWAM 评测与 FSDP SFT 训练支持。
  - 链接：https://github.com/RLinf/RLinf/commit/ee2cab65adfc836305b258da44fab2679179e1ae
  - 变更规模：+2339 -10
  - 提交者：wolf
  - 解决的问题：FastWAM 缺少评测与 SFT 训练路径，无法纳入统一流水线。
  - 产品启示：新模型接入需同时覆盖评测与训练，才能形成完整可用链路。
8/10-feat(reward): add QwenTrend reward pipeline (#1395)（c9e8067）
  - 评分：8/10
  - 一句话总结：新增 QwenTrend 奖励流水线，扩展 VLM 奖励建模能力。
  - 链接：https://github.com/RLinf/RLinf/commit/c9e80673265b88a3eaf97d8dd3726d081ad3a889
  - 变更规模：+3234 -134
  - 提交者：NLC2004
  - 解决的问题：缺少趋势型 VLM 奖励建模能力，限制复杂任务奖励设计。
  - 产品启示：奖励模型流水线化是具身 RL 从任务定制走向可复用能力的关键。
7/10-fix: support and test VLAs on Ascend, ROCm and MUSA (#1578)（805858b）
  - 评分：7/10
  - 一句话总结：在 Ascend、ROCm、MUSA 多平台支持并测试 VLA 模型。
  - 链接：https://github.com/RLinf/RLinf/commit/805858b84a33e74b6c8e3a05b5c96379a61224cf
  - 变更规模：+763 -112
  - 提交者：Andy Lin
  - 解决的问题：VLA 模型在非 CUDA 平台上缺乏支持与回归测试。
  - 产品启示：多平台 VLA 支持与 CI 覆盖是异构算力可信度的关键保障。
7/10-feat(starvla): add Ascend support for StarVLA (#1525)（717dfb2）
  - 评分：7/10
  - 一句话总结：为 StarVLA 新增昇腾 NPU 支持并补充文档与 E2E 测试。
  - 链接：https://github.com/RLinf/RLinf/commit/717dfb2cb9e59927fb9f5ea207ab63f43b119f1d
  - 变更规模：+550 -95
  - 提交者：GanDing
  - 解决的问题：StarVLA 无法在 Ascend 平台运行，限制国产算力用户使用。
  - 产品启示：模型级 NPU 适配与文档同步，是扩大用户覆盖的必要动作。
7/10-feat(eval): add ApxInf backend for OpenPI LIBERO evaluation (#1537)（1dcbc56）
  - 评分：7/10
  - 一句话总结：为 OpenPI LIBERO 评测新增 ApxInf 推理后端。
  - 链接：https://github.com/RLinf/RLinf/commit/1dcbc56b4e25401c89f19f691f809a6369a167a0
  - 变更规模：+1042 -2
  - 提交者：Chenxi He
  - 解决的问题：OpenPI LIBERO 评测缺少 ApxInf 后端支持，评测路径受限。
  - 产品启示：评测后端多样化有助于提升推理部署灵活性与横向对比能力。

### ⚡️ 性能/架构优化
8/10-feat(envs): unify world models backend (#1518)（db66ac5）
  - 评分：8/10
  - 一句话总结：统一世界模型后端架构，收敛 OpenSora/Wan 等实现。
  - 链接：https://github.com/RLinf/RLinf/commit/db66ac56d1aa4a9c8441c4026e4212b21811970d
  - 变更规模：+1459 -1948
  - 提交者：zhengjia
  - 解决的问题：世界模型后端分散、配置与文档重复，维护成本高。
  - 产品启示：后端统一是模型生态扩张后必然的架构收敛动作，利于后续扩展。
8/10-feat(weight-sync): refactor placement and weight reshard (#1520)（5468a5e）
  - 评分：8/10
  - 一句话总结：重构权重同步的 placement 与 reshard 逻辑，提升分布式同步效率。
  - 链接：https://github.com/RLinf/RLinf/commit/5468a5e06afcefd9211baa11418198427594dec2
  - 变更规模：+2004 -892
  - 提交者：sherlockcooper
  - 解决的问题：权重同步与重分片逻辑耦合、扩展性差，影响大规模训练吞吐。
  - 产品启示：权重同步是 RL 训练性能主线，重构为后续通信优化奠定基础。

### 🐛 Bug修复 / 其他
7/10-fix(embodied): stop scaling the entropy bonus by micro-batch size (#1565)（ce4d821）
  - 评分：7/10
  - 一句话总结：修复熵奖励被 micro-batch size 错误缩放的问题。
  - 链接：https://github.com/RLinf/RLinf/commit/ce4d821780d0e431d90f43d028fc93cac61f8fe0
  - 变更规模：+244 -39
  - 提交者：Rusty Raven
  - 解决的问题：熵奖励随 micro-batch 大小缩放，导致训练目标不一致与不稳定。
  - 产品启示：训练正确性修复需配套单元测试，避免分布式配置差异引发隐性回归。

---

