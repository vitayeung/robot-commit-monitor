# 具身智能周报 (2026年07月28日 21:32:32)

## 行业风向总览

### 具身智能行业风向总结（本周）

**技术焦点**：本周技术演进呈现“仿真精度与训练效率双轨并行”态势。**MuJoCo** 聚焦柔性体（flex）仿真稳定性，修复了父体旋转导致的刚度基计算错误与数值发散问题，并新增网络渲染支持，强化Web端远程可视化能力。**Warp** 则重点提升图捕获（Graph Capture）能力，支持CPU端HashGrid和BVH更新回放，并引入NumPy风格的tile切片与花式索引，显著降低编程门槛。**RLinf** 大规模扩展具身智能训练范式，新增pi0.5行为SFT与评估路径、OpenVLA-OFT OPD训练，以及基于SGLang的VLM奖励服务器，推动多模态基础模型与强化学习的深度集成。

**合成数据相关动态**：**mjlab** 为Warp渲染器新增灯光领域随机化功能，允许用户通过配置自动改变灯光属性（颜色、强度、衰减），直接增强仿真环境的视觉多样性，为视觉导航、抓取等任务生成更具泛化性的合成数据。**IsaacLab** 新增与Arena环境的互操作支持，扩展了模仿学习数据生成和训练工作流的兼容性。

**产品经理关注信号**：
1.  **平台成熟化**：**IsaacLab** 准备将稳定版本设为默认分支，标志着核心功能趋于稳定，可降低生产环境风险。**RLinf** 引入分布式追踪与性能分析，向工业级应用迈进。
2.  **硬件生态扩展**：**RLinf** 新增对Intel XPU和昆仑芯硬件的支持，**IsaacLab** 修复ARM平台问题，表明具身智能框架正加速适配多样化硬件，降低对单一GPU的依赖。
3.  **调试工具链完善**：**MuJoCo** 修复射线缓存与Web Viewer UI闪烁问题，**Warp** 修复Jacobian绘图错误，**RLinf** 修复全局解释方差计算，这些改进直接提升开发者调试效率与模型训练监控的准确性。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 7 条
- 高价值提交（≥6分）: 2 条
- 代码更新规模: +339 / -192 行
- 主要贡献者: Kevin Zakka, Pedro Morais

## 🧭 趋势点评

本周的更新延续了仓库在2026年1月至7月期间的核心演进方向：**功能扩展与生态集成**以及**基础设施与文档完善**。新增灯光领域随机化功能（f643d24）直接呼应了仓库长期对“领域随机化”能力的强化，而修复射线缓存bug（d247f38）则体现了对仿真精度和调试工具链的持续打磨。这两项更新均未偏离基线中总结的“提升仿真精度、训练效率与可复现性”的核心价值，且与2-3月的高频开发期相比，当前提交量虽少但质量较高，符合项目进入稳定维护期的特征。

## 🔍 关键更新解析

### 🚀 新功能/特性

8/10-Add missing light cfg fields supported by warp renderer, and dr functions (#1118)（f643d24）
  - **评分**：8/10
  - **一句话总结**：为Warp渲染器新增了缺失的灯光配置字段，并实现了对应的领域随机化（DR）函数。
  - **链接**：https://github.com/mujocolab/mjlab/commit/f643d245303ff439a90f37151056ff987bdb95f7
  - **变更规模**：+208 -0
  - **提交者**：Pedro Morais
  - **解决的问题**：此前Warp渲染器支持的灯光属性（如颜色、强度、衰减等）在配置和随机化接口中缺失，导致用户无法通过DR系统灵活控制灯光效果，限制了视觉多样性和仿真真实感。
  - **产品启示**：该功能直接增强了仿真环境的视觉随机化能力，对于需要高视觉多样性的具身智能训练（如视觉导航、抓取）至关重要。它使用户能够通过简单的配置实现灯光属性的自动变化，从而提升模型在真实世界光照条件下的泛化性。

### 🐛 Bug修复 / 其他

7/10-Invalidate raycast sensor cache after sense to fix stale debug rays (#1114)（d247f38）
  - **评分**：7/10
  - **一句话总结**：修复了射线投射传感器在每次感知后未清除缓存，导致调试射线显示陈旧数据的问题。
  - **链接**：https://github.com/mujocolab/mjlab/commit/d247f38de798a5c3238d19ff4c5897382357cf7c
  - **变更规模**：+14 -2
  - **提交者**：Kevin Zakka
  - **解决的问题**：在调试模式下，射线投射传感器（RaycastSensor）的缓存未在每次感知步骤后失效，导致可视化调试射线显示的是上一次感知的结果，而非当前帧的真实射线路径，严重干扰了调试和验证工作。
  - **产品启示**：该修复直接提升了开发者的调试体验。对于依赖射线传感器进行碰撞检测、距离测量或环境感知的任务（如避障、地图构建），准确的调试可视化是定位问题的关键。此修复确保了调试信息的实时性和准确性，降低了开发与排错成本。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 31 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +17031 / -985 行
- 主要贡献者: Michael Moss, Matija Kecman, Haroon Qureshi

## 🧭 趋势点评
本周的更新紧密延续了仓库在2026年上半年的核心趋势，即对柔性体（flex）仿真稳定性的深度优化。提交 `55b4341` 和 `fe9dc58` 分别修复了flex在旋转父体下的刚度基和旋转不稳定性问题，这与长期路线中“深化flex仿真性能优化”的方向高度一致。同时，`dd4d058` 修复了碰撞和驱动中的计时器遗漏，呼应了此前对性能分析工具（如Studio profiler）的持续改进。此外，`ca53371` 和 `e23b504` 分别新增网络渲染支持和修复Web渲染闪烁，体现了对WASM/Web平台和远程可视化能力的持续投入，这与仓库在WASM内存扩展和MJX/Warp集成方面的长期努力一脉相承。

## 🔍 关键更新解析

### 🚀 新功能/特性

6/10-Export netimgui files in MuJoCo Copybara configuration for use with the upcoming Web Viewer（ca53371）
  - **评分**: 6/10
  - **一句话总结**: 新增网络渲染支持，为即将推出的Web Viewer导出netimgui文件。
  - **链接**: https://github.com/google-deepmind/mujoco/commit/ca5337161dea4e6c7780c0e2be8c7d618a7679ac
  - **变更规模**: +15483 -0
  - **提交者**: Matija Kecman
  - **解决的问题**: 为MuJoCo的Web Viewer提供网络渲染基础设施，支持远程可视化。
  - **产品启示**: 该功能将显著提升MuJoCo在Web端的交互能力，使用户能够通过网络远程查看和调试仿真，这对于机器人远程操作和云端仿真场景具有重要价值。

### 🐛 Bug修复 / 其他

9/10-Fix flexcomp instability when parent body has non-identity quaternion（fe9dc58）
  - **评分**: 9/10
  - **一句话总结**: 修复了当父体具有非单位四元数时flexcomp的不稳定性问题。
  - **链接**: https://github.com/google-deepmind/mujoco/commit/fe9dc584772bf618144542682b10aa2c8d4a0120
  - **变更规模**: +146 -13
  - **提交者**: Alessio Quaglino
  - **解决的问题**: 当flex的父体旋转为非单位四元数时，flexcomp计算出现数值不稳定，导致仿真发散。
  - **产品启示**: 该修复是柔性体仿真稳定性的关键改进，确保了在复杂旋转场景下flex的鲁棒性，对于需要精确模拟柔性体在动态环境中的行为（如机器人抓取、软体机器人）具有重要意义。

---

8/10-Fix stretch stiffness basis for flexes in rotated parent bodies（55b4341）
  - **评分**: 8/10
  - **一句话总结**: 修复了flex在旋转父体中的拉伸刚度基计算错误。
  - **链接**: https://github.com/google-deepmind/mujoco/commit/55b43414dde2587416e5519d535cd82d9f7492cc
  - **变更规模**: +123 -8
  - **提交者**: Alessio
  - **解决的问题**: 当flex的父体具有旋转时，拉伸刚度基计算错误导致仿真行为异常。
  - **产品启示**: 该修复确保了柔性体在复杂装配体中的物理准确性，对于需要精确模拟柔性部件（如机器人关节、软体材料）的应用至关重要。

6/10-Change how ImGui clip rect scaling and scissor computation works in imgui_bridge to fix flickering and clipping errors in the web viewer（e23b504）
  - **评分**: 6/10
  - **一句话总结**: 修复了Web Viewer中因裁剪矩形缩放和剪刀计算错误导致的闪烁和裁剪问题。
  - **链接**: https://github.com/google-deepmind/mujoco/commit/e23b5042013a1f7219d2950bf913ac981627bc61
  - **变更规模**: +24 -15
  - **提交者**: Matija Kecman
  - **解决的问题**: Web Viewer中ImGui界面出现闪烁和裁剪错误，影响用户交互体验。
  - **产品启示**: 该修复提升了Web Viewer的UI稳定性和可用性，是MuJoCo向Web平台迁移过程中的关键用户体验改进。

6/10-Fix missing timer end calls on early returns in collision and actuation（dd4d058）
  - **评分**: 6/10
  - **一句话总结**: 修复了碰撞和驱动模块中因提前返回导致计时器未正确结束的问题。
  - **链接**: https://github.com/google-deepmind/mujoco/commit/dd4d0585ee42a185a0626e3ad39abf6f4e241e89
  - **变更规模**: +2 -0
  - **提交者**: Sam Haves
  - **解决的问题**: 在碰撞检测和驱动计算的某些提前返回路径中，性能计时器未被正确结束，导致性能分析数据不准确。
  - **产品启示**: 该修复确保了性能分析工具的准确性，为开发者提供可靠的性能数据，有助于后续的性能优化工作。

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 5 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +531 / -606 行
- 主要贡献者: Kelly Guo, isaaclab-bot[bot], peterd-NV

## 🧭 趋势点评
本周的更新延续了IsaacLab仓库在2026年上半年的核心趋势：从大规模性能调优与功能扩展，转向为稳定版本发布做准备。提交活动显著减少，但质量很高，聚焦于修复关键平台问题（如ARM构建）、锁定CI依赖版本以提升测试可靠性，以及准备稳定分支。这标志着项目从快速迭代期进入成熟稳定期，与基线中“稳定版本准备”的预测方向一致。同时，新增的Arena互操作功能表明，社区集成与生态扩展仍是长期重点。

## 🔍 关键更新解析

### 🚀 新功能/特性

6/10-Add Isaac Lab Arena interop for imitation learning scripts (#6650) (#6690)（640cfe7）
  - **评分**: 6/10
  - **一句话总结**: 新增Isaac Lab Arena与模仿学习脚本的互操作支持。
  - **链接**: https://github.com/isaac-sim/IsaacLab/commit/640cfe75f2dc219e62db0d0d607ef3eff9159980
  - **变更规模**: +36 -8
  - **提交者**: peterd-NV
  - **解决的问题**: 使模仿学习脚本能够与Isaac Lab Arena环境无缝集成，扩展了数据生成和训练工作流的兼容性。
  - **产品启示**: 该功能降低了用户在不同仿真框架间迁移的门槛，有助于吸引更多使用Arena的社区用户，并促进模仿学习数据管线的标准化。

### ⚡️ 性能/架构优化

8/10-Prepare stable release as default branch (#6678)（88d3977）
  - **评分**: 8/10
  - **一句话总结**: 准备将稳定版本设为默认分支，标志着项目进入发布候选阶段。
  - **链接**: https://github.com/isaac-sim/IsaacLab/commit/88d39772f095ae6f4b87f7543d7ec75b84e4347f
  - **变更规模**: +237 -423
  - **提交者**: Kelly Guo
  - **解决的问题**: 通过更新PR模板、CI工作流和文档，为将稳定版本分支设为默认分支做准备，确保发布流程的规范性和可维护性。
  - **产品启示**: 这是项目成熟度的重要里程碑，意味着核心功能已趋于稳定，用户可以期待更可靠的长期支持版本，降低生产环境中的风险。

### 🐛 Bug修复 / 其他

7/10-Backport ARM nlopt install fix to 3.0.0-beta2 (#6723)（af1bab4）
  - **评分**: 7/10
  - **一句话总结**: 修复ARM平台上的nlopt安装问题，并回传到beta2版本。
  - **链接**: https://github.com/isaac-sim/IsaacLab/commit/af1bab4dc173ba69b08fab779c14ead61d13fd33
  - **变更规模**: +150 -140
  - **提交者**: Kelly Guo
  - **解决的问题**: 解决了在ARM架构（如NVIDIA Jetson）上构建Docker镜像时nlopt库安装失败的问题，确保跨平台兼容性。
  - **产品启示**: 修复ARM平台问题直接扩展了IsaacLab的硬件支持范围，对边缘计算和机器人部署场景至关重要，体现了对多样化用户环境的重视。

7/10-Fix Franka paths and pin CI OVRTX to 0.3 (#6695)（418ca31）
  - **评分**: 7/10
  - **一句话总结**: 修复Franka机器人路径问题，并固定CI中OVRTX版本至0.3。
  - **链接**: https://github.com/isaac-sim/IsaacLab/commit/418ca31b47a8eb27db8aefcfc134e4c4f1d2b6f3
  - **变更规模**: +73 -16
  - **提交者**: Kelly Guo
  - **解决的问题**: 修复了Franka机器人资产路径错误，并通过固定OVRTX版本避免CI因依赖更新而出现不兼容问题，提升测试稳定性。
  - **产品启示**: 路径修复确保了Franka机器人相关教程和示例的正确运行；固定CI版本是基线中“降低CI假阳性”趋势的延续，有助于维护者快速识别真正的问题，而非依赖变更导致的失败。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 29 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +9610 / -1066 行
- 主要贡献者: Eric Shi, Zach Corse, Eliot Xing

## 🧭 趋势点评
本周的更新紧密延续了仓库在2026年上半年的核心演进方向，即“性能优化与功能增强并重”。提交内容高度聚焦于提升图捕获（Graph Capture）的CPU端能力（如HashGrid和BVH更新回放）、优化运行时效率（如缓存内核mangled名称）、以及扩展NumPy风格的tile操作，这与基线中强调的“增强图捕获与条件图执行功能”和“扩展tile操作”趋势完全吻合。同时，对APIC内存加载的加固和Jacobian绘图的修复，体现了项目在快速迭代中对稳定性和正确性的持续关注，符合基线中“强化运行时效率、内存安全”的长期目标。

## 🔍 关键更新解析

### 🚀 新功能/特性

9/10-Add NumPy-style tile slicing and fancy indexing (GH-1176)（c07653a）
  - **评分**: 9/10
  - **一句话总结**: 为tile操作引入了NumPy风格的切片和花式索引，极大提升了数组操作的直观性和灵活性。
  - **链接**: https://github.com/NVIDIA/warp/commit/c07653a0759e48e58afb78fcd93ca41a5944cd75
  - **变更规模**: +1885 -59
  - **提交者**: Zach Corse
  - **解决的问题**: 此前tile操作缺乏高级索引能力，用户需要编写复杂循环来实现数据选择，降低了开发效率。
  - **产品启示**: 该功能显著降低了Warp中tile编程的学习门槛，使其更接近Python原生数组操作，有助于吸引更多科学计算和AI领域的开发者。

9/10-Support CPU HashGrid graph replay [GH-1664]（17e26ef）
  - **评分**: 9/10
  - **一句话总结**: 支持在CPU图捕获中回放HashGrid操作，扩展了图执行在物理模拟等场景的应用范围。
  - **链接**: https://github.com/NVIDIA/warp/commit/17e26ef1e78a6c98dde24978d1c19578591003e2
  - **变更规模**: +935 -76
  - **提交者**: Eric Shi
  - **解决的问题**: 此前CPU图捕获不支持HashGrid，导致依赖空间哈希的算法（如粒子模拟）无法利用图执行带来的性能优势。
  - **产品启示**: 此功能是图捕获能力的重要补充，使得更多CPU端计算密集型任务能够被图优化，提升了Warp在物理仿真领域的竞争力。

8/10-Replay BVH updates in CPU graph capture [GH-1665]（0956d10）
  - **评分**: 8/10
  - **一句话总结**: 实现了在CPU图捕获中回放BVH（包围体层次结构）更新，进一步增强了图执行对动态场景的支持。
  - **链接**: https://github.com/NVIDIA/warp/commit/0956d106b75ebab1c6e238e194d4f72a150daed4
  - **变更规模**: +315 -0
  - **提交者**: Nicolas Capens
  - **解决的问题**: 动态场景中BVH需要频繁更新，此前无法在图捕获中处理，限制了图执行在光线追踪和碰撞检测中的应用。
  - **产品启示**: 结合CPU HashGrid图回放，Warp的图捕获能力已覆盖更多核心数据结构，为构建复杂的、可重用的计算管线奠定了基础。

7/10-Add JAX kernel block sizes [GH-1436]（a05b533）
  - **评分**: 7/10
  - **一句话总结**: 为JAX互操作内核添加了块大小配置能力，提升了与JAX生态集成的灵活性和性能调优空间。
  - **链接**: https://github.com/NVIDIA/warp/commit/a05b5333c1bf3f214b6c3b325efb9f9cea5600db
  - **变更规模**: +232 -12
  - **提交者**: Eric Shi
  - **解决的问题**: 此前Warp与JAX互操作时，内核块大小是固定的，无法针对特定硬件或计算负载进行优化。
  - **产品启示**: 该特性强化了Warp作为JAX后端的能力，允许用户更精细地控制计算资源，有助于在AI和科学计算混合工作负载中取得更好性能。

6/10-Add locked CUDA toolkit setup（91e590b）
  - **评分**: 6/10
  - **一句话总结**: 添加了锁定CUDA工具包版本的CI配置，确保构建环境的一致性和可复现性。
  - **链接**: https://github.com/NVIDIA/warp/commit/91e590b440060861a4bb8a667c63e385d766f277
  - **变更规模**: +1921 -70
  - **提交者**: Eric Shi
  - **解决的问题**: 此前CI中CUDA工具包版本可能浮动，导致不同构建环境下的编译结果不一致，增加了调试和回归测试的难度。
  - **产品启示**: 这是对项目基础设施的重要加固，通过锁定工具链版本，降低了因环境差异引入的偶发问题，提升了开发效率和发布质量。

### ⚡️ 性能/架构优化

8/10-Cache kernel mangled names [GH-1589]（cbafd19）
  - **评分**: 8/10
  - **一句话总结**: 通过缓存内核的mangled名称，减少了重复计算，加速了内核启动过程。
  - **链接**: https://github.com/NVIDIA/warp/commit/cbafd196f1f46b3e93979fbb80f02ff96a3fe1e6
  - **变更规模**: +78 -9
  - **提交者**: Eric Shi
  - **解决的问题**: 每次内核启动时都需要重新计算其mangled名称，这在频繁调用小内核的场景下造成了不必要的开销。
  - **产品启示**: 这是一个典型的“小改动、大收益”优化，直接降低了内核启动的延迟，尤其利好那些需要大量启动小内核的迭代算法。

7/10-Improve batched reduction accuracy [GH-1700]（cb9dc55）
  - **评分**: 7/10
  - **一句话总结**: 提升了批处理归约操作的数值精度，减少了累积误差。
  - **链接**: https://github.com/NVIDIA/warp/commit/cb9dc5596f33060f1c9a86bab2bb7fecf9225d78
  - **变更规模**: +418 -57
  - **提交者**: Gilles Daviet
  - **解决的问题**: 在优化器或线性求解器中，批处理归约可能因浮点运算顺序导致精度损失，影响收敛稳定性。
  - **产品启示**: 该优化直接提升了Warp在科学计算和机器学习优化中的可靠性，对于需要高精度的应用（如物理仿真）至关重要。

### 🐛 Bug修复 / 其他

7/10-Harden APIC memory region loading（ed58c11）
  - **评分**: 7/10
  - **一句话总结**: 加固了APIC（Affine Particle-In-Cell）内存区域的加载逻辑，提升了稳定性和安全性。
  - **链接**: https://github.com/NVIDIA/warp/commit/ed58c1118ecb862b17368a51388a7f39d0ddafd7
  - **变更规模**: +211 -71
  - **提交者**: Eric Shi
  - **解决的问题**: 此前APIC内存加载可能存在边界条件处理不当或数据竞争问题，导致偶发的崩溃或数据损坏。
  - **产品启示**: 此修复增强了Warp在流体模拟等APIC应用中的健壮性，减少了因底层内存问题导致的调试困难。

6/10-Fix Jacobian plotting for functions and typed kernels [GH-1672]（41f0ccd）
  - **评分**: 6/10
  - **一句话总结**: 修复了在函数和类型化内核中绘制Jacobian矩阵时的错误。
  - **链接**: https://github.com/NVIDIA/warp/commit/41f0ccdb0b38f4f0698bcc8b2c22f4545560f34f
  - **变更规模**: +345 -62
  - **提交者**: Eric Shi
  - **解决的问题**: 调试工具中的Jacobian绘图功能在特定场景下（如使用类型化内核）无法正确工作，影响了自动微分调试的效率。
  - **产品启示**: 该修复完善了Warp的调试工具链，使得开发者能够更直观地验证梯度计算的正确性，对复杂模型的开发至关重要。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 11 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +16605 / -314 行
- 主要贡献者: Peihong Wang, aasivas, 石乐同

## 🧭 趋势点评

本周更新延续了仓库在2026年1月至7月期间的核心演进方向，即**大规模扩展具身智能与真实世界机器人支持**，并**深度集成多模态基础模型与训练范式**。新增的OpenVLA-OFT OPD训练、pi0.5 SFT+评估路径、SGLang VLM奖励服务器以及RoboCasa365支持，直接呼应了基线中“强化仿真环境与真实世界部署的融合”与“多模态基础模型与机器人策略的深度集成”两大预测方向。同时，对Intel XPU和昆仑芯硬件的支持，体现了对多平台兼容性的持续投入，这与基线中“依赖更新和社区反馈响应”的趋势一致。值得注意的是，本周提交中性能优化类缺失，而新功能占比极高，这延续了项目“功能丰富度提升显著”的快速迭代期特征，但也加剧了基线中提及的“性能优化提交数量相对较少”的风险。

## 🔍 关键更新解析

### 🚀 新功能/特性

10/10-feat(openpi_pytorch): add pi0.5 behavior sft + eval path (#1254)（60165be）
  - **评分**：10/10
  - **一句话总结**：新增pi0.5行为SFT与评估路径，大幅扩展了具身智能训练能力。
  - **链接**：https://github.com/RLinf/RLinf/commit/60165be54d840e91840ed2a02a453adcc5457866
  - **变更规模**：+10546 -1
  - **提交者**：Xzxuan
  - **解决的问题**：pi0.5是Physical Intelligence发布的重要机器人基础模型，此前RLinf缺乏对其SFT和评估的完整支持。
  - **产品启示**：pi0.5的完整支持是RLinf在具身智能领域的重要里程碑，将吸引大量从事真实世界机器人研究的用户，巩固框架在机器人基础模型训练领域的领先地位。

9/10-feat: add distributed tracing and profiling (#1396)（e7609d4）
  - **评分**：9/10
  - **一句话总结**：引入分布式追踪与性能分析功能，为大规模训练提供可观测性。
  - **链接**：https://github.com/RLinf/RLinf/commit/e7609d4c9e2f33c5ffc10b67c61c8e4b73208b45
  - **变更规模**：+571 -25
  - **提交者**：aasivas
  - **解决的问题**：在分布式训练场景下，开发者难以定位性能瓶颈和通信延迟，该功能提供了系统级的性能追踪能力。
  - **产品启示**：分布式追踪是大型RL框架走向工业级应用的必备能力，有助于用户快速诊断训练效率问题，提升框架的易用性和可维护性。

9/10-feat(embodiment): add OpenVLA-OFT OPD training (#1377)（f469f9a）
  - **评分**：9/10
  - **一句话总结**：新增OpenVLA-OFT OPD训练支持，扩展了视觉-语言-动作模型的训练范式。
  - **链接**：https://github.com/RLinf/RLinf/commit/f469f9a5d0b8d0439ded3f420b93ed80fff845bb
  - **变更规模**：+1251 -50
  - **提交者**：Zhennan Jiang
  - **解决的问题**：OpenVLA是当前具身智能领域的热门基础模型，OPD训练范式允许在离线数据上进行策略蒸馏，降低了对在线交互的依赖。
  - **产品启示**：紧跟OpenVLA等前沿模型，使RLinf成为VLA研究者的首选平台，有助于构建从仿真到真实世界的完整训练闭环。

8/10-feat(embodiment): support SGLang VLM reward server (#1314)（6add8b4）
  - **评分**：8/10
  - **一句话总结**：新增SGLang VLM奖励服务器，支持基于视觉语言模型的奖励计算。
  - **链接**：https://github.com/RLinf/RLinf/commit/6add8b419ed667eada204ac81c9d5913706cd6cc
  - **变更规模**：+1175 -130
  - **提交者**：Shuaihang Chen
  - **解决的问题**：传统奖励函数难以处理复杂视觉任务，VLM奖励服务器使框架能利用多模态模型生成更智能的奖励信号。
  - **产品启示**：VLM奖励服务器是连接视觉理解与强化学习的关键桥梁，将吸引更多从事视觉-语言-动作（VLA）研究的用户，拓展框架在复杂机器人任务中的应用边界。

8/10-feat(embodiment): add RoboCasa365 support (#1349)（d9f3d8a）
  - **评分**：8/10
  - **一句话总结**：新增RoboCasa365仿真环境支持，扩展了可用的机器人训练场景。
  - **链接**：https://github.com/RLinf/RLinf/commit/d9f3d8a9db4d7aad1d641029293295503dd3eb2c
  - **变更规模**：+2514 -15
  - **提交者**：Diddan2233
  - **解决的问题**：RoboCasa365提供了丰富的家庭机器人仿真场景，此前RLinf缺乏对该环境的集成。
  - **产品启示**：RoboCasa365的加入丰富了框架的仿真环境库，使用户能更方便地进行家庭服务机器人任务的训练和评估，提升框架在服务机器人领域的吸引力。

7/10-fix: support intel xpu (#1389)（9c575b9）
  - **评分**：7/10
  - **一句话总结**：支持Intel XPU硬件，扩展了框架的硬件兼容性。
  - **链接**：https://github.com/RLinf/RLinf/commit/9c575b9303ecbb89db81b1bc915c254931709d93
  - **变更规模**：+66 -1
  - **提交者**：beckwen
  - **解决的问题**：用户无法在Intel XPU加速器上运行RLinf，限制了框架在非NVIDIA硬件生态中的使用。
  - **产品启示**：支持Intel XPU有助于降低对单一GPU厂商的依赖，吸引更多使用Intel硬件的数据中心和科研机构用户，提升框架的生态覆盖度。

7/10-feat(device): add Kunlunxin hardware support (#1399)（2005d39）
  - **评分**：7/10
  - **一句话总结**：新增昆仑芯硬件支持，进一步扩展硬件生态。
  - **链接**：https://github.com/RLinf/RLinf/commit/2005d39598322fafc3f93d9843d6409598f6201f
  - **变更规模**：+147 -0
  - **提交者**：DearFishi
  - **解决的问题**：国内用户无法在昆仑芯AI加速器上使用RLinf，限制了框架在国内市场的推广。
  - **产品启示**：支持国产芯片（昆仑芯）是RLinf本土化战略的重要一步，有助于获取国内科研和工业用户，同时响应国产替代的政策趋势。

### 🐛 Bug修复 / 其他

7/10-fix: compute critic explained variance globally (#1386)（0f9ea98）
  - **评分**：7/10
  - **一句话总结**：修复全局解释方差计算，提升训练监控指标的准确性。
  - **链接**：https://github.com/RLinf/RLinf/commit/0f9ea98c7a6d9e3ade24e8f4846c64d3b135dbcc
  - **变更规模**：+325 -58
  - **提交者**：Peihong Wang
  - **解决的问题**：此前解释方差计算仅在局部进行，无法准确反映全局训练状态，导致用户对模型收敛情况的误判。
  - **产品启示**：准确的训练监控指标是用户判断模型训练效果的核心依据，该修复提升了框架的可信度和调试效率。

---

6/10-fix(maniskill): remove unsafe force_gc_tensor from offload cleanup (#1404)（2617980）
  - **评分**：6/10
  - **一句话总结**：修复Maniskill环境卸载清理中的内存泄漏问题。
  - **链接**：https://github.com/RLinf/RLinf/commit/26179807d701950cf2933554bfb9bb596e662b68
  - **变更规模**：+0 -26
  - **提交者**：石乐同
  - **解决的问题**：`force_gc_tensor`调用可能导致内存泄漏或崩溃，移除该不安全操作以提升环境卸载的稳定性。
  - **产品启示**：内存泄漏是长期运行训练任务的致命问题，该修复直接提升了框架在长时间训练场景下的可靠性，是保障用户体验的关键优化。

