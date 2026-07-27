# 具身智能周报 (2026年07月27日 08:57:32)

## 行业风向总览

### 具身智能行业风向总结（本周）

**技术焦点：** 本周技术演进呈现“仿真引擎深度优化”与“VLA模型训练闭环”双主线。MuJoCo与Warp聚焦底层：MuJoCo修复柔性体（flex）因父级旋转导致的数值不稳定关键Bug，并允许网格数据动态重上传；Warp则重点扩展图执行的可移植性，新增CPU端HashGrid与BVH回放支持，并修复条件子图内存释放错误。上层RLinf则全力推进VLA模型训练，新增pi0.5行为克隆SFT、OpenVLA在线策略蒸馏（OPD）及SGLang VLM奖励服务器，标志着从“仿真到训练”的完整链路打通。

**合成数据相关动态：** 本周无直接针对合成数据生成工具或管线的更新。但Isaac Lab新增与Arena平台的模仿学习互操作功能，以及RLinf集成RoboCasa365仿真环境，均间接强化了从仿真环境生成高质量训练数据的能力，为合成数据生态提供了更丰富的场景基础。

**产品经理关注信号：**
1.  **跨平台与硬件兼容性成为标配：** Isaac Lab修复ARM平台安装问题并准备稳定版发布；RLinf新增对Intel XPU和昆仑芯硬件的支持。这表明具身智能框架正从单一GPU生态向多架构、国产化硬件全面扩展，产品需提前规划硬件适配策略。
2.  **VLA模型训练工具链趋于成熟：** RLinf本周密集上线pi0.5 SFT、OpenVLA OPD及VLM奖励服务器，标志着VLA模型从“研究概念”进入“可工程化训练”阶段。产品经理应关注如何利用这些工具降低机器人策略开发门槛，例如提供“零代码”训练模板或预训练模型市场。
3.  **仿真稳定性与调试体验持续提升：** MuJoCo修复柔性体稳定性、Warp增强APIC内存健壮性、RLinf修复Maniskill内存泄漏，均指向仿真可靠性成为行业共识。同时，MuJoCo修复Web查看器UI闪烁、Warp修复雅可比绘图功能，表明开发者调试体验正被纳入核心优化项。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 7 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +190 / -196 行
- 主要贡献者: Kevin Zakka, Pedro Morais, Philipp Wu

## 🧭 趋势点评

本周更新延续了仓库在2026年下半年的维护与稳定化趋势。核心工作聚焦于修复关键Bug（如ONNX上传与W&B日志器的兼容性问题）以及持续进行安全依赖更新，这与基线中“项目在高速迭代后期仍持续关注性能改进”和“大量依赖更新可能引入兼容性问题”的观察一致。同时，对射线传感器缓存的修复体现了对调试工具链可靠性的持续打磨，符合仓库长期致力于提升仿真精度与开发者体验的方向。

## 🔍 关键更新解析

### 🚀 新功能/特性
*无*

### ⚡️ 性能/架构优化
*无*

### 🐛 Bug修复 / 其他

8/10-Fix ONNX upload with current W&B logger (#1107)（011a5ab）
  - **评分**: 8
  - **一句话总结**: 修复了ONNX模型上传至当前版本W&B日志器时失败的关键Bug。
  - **链接**: https://github.com/mujocolab/mjlab/commit/011a5ab441590a81664a813ff0160e99f5835aa6
  - **变更规模**: +59 -4
  - **提交者**: Philipp Wu
  - **解决的问题**: 解决了ONNX策略导出后无法通过W&B日志器正确上传的问题，确保模型部署流程的完整性。
  - **产品启示**: 对于依赖W&B进行实验追踪和模型管理的用户，此修复至关重要，保证了从训练到部署的闭环体验，提升了平台在MLOps流程中的可靠性。

7/10-Invalidate raycast sensor cache after sense to fix stale debug rays (#1114)（d247f38）
  - **评分**: 7
  - **一句话总结**: 修复了射线传感器在感知后未清除缓存，导致调试射线显示陈旧信息的问题。
  - **链接**: https://github.com/mujocolab/mjlab/commit/d247f38de798a5c3238d19ff4c5897382357cf7c
  - **变更规模**: +14 -2
  - **提交者**: Kevin Zakka
  - **解决的问题**: 解决了调试模式下射线可视化不准确的问题，确保开发者看到的射线状态与当前仿真帧一致。
  - **产品启示**: 提升了调试工具的准确性和可信度，对于依赖可视化进行传感器调试和策略分析的开发者来说，这是一个重要的体验改进，减少了调试过程中的误导。

6/10-Bump gitpython and setuptools for security fixes (#1113)（ef6d3d4）
  - **评分**: 6
  - **一句话总结**: 升级了`gitpython`和`setuptools`库以修复已知安全漏洞。
  - **链接**: https://github.com/mujocolab/mjlab/commit/ef6d3d447068a6400806c442e454d7f4110b0964
  - **变更规模**: +10 -8
  - **提交者**: Kevin Zakka
  - **解决的问题**: 修复了依赖库中的安全漏洞，降低了项目被攻击的风险。
  - **产品启示**: 体现了项目对供应链安全和用户数据保护的重视，是维持项目健康生态和用户信任的基础性工作。

6/10-Bump pillow, onnx, soupsieve for security fixes (#1112)（36ccc49）
  - **评分**: 6
  - **一句话总结**: 升级了`pillow`、`onnx`和`soupsieve`库以修复已知安全漏洞。
  - **链接**: https://github.com/mujocolab/mjlab/commit/36ccc49c898911e20c1d793e591173041239699d
  - **变更规模**: +79 -171
  - **提交者**: Kevin Zakka
  - **解决的问题**: 修复了多个核心依赖库中的安全漏洞，特别是与图像处理和模型导出相关的库。
  - **产品启示**: 持续的安全更新是项目长期稳定运行的基础，尤其对于涉及模型导出（ONNX）和可视化（Pillow）的功能，及时修复漏洞能有效防止潜在的安全事故。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 46 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +7108 / -2579 行
- 主要贡献者: Michael Moss, teerthsharma, Yuval Tassa

## 🧭 趋势点评
本周的更新紧密延续了仓库在性能优化、Bug修复和生态建设上的长期趋势。`fe9dc58` 对flex体稳定性的修复，以及 `dd4d058` 对计时器遗漏调用的修正，体现了团队对仿真精度和可靠性的持续打磨。`ba9a650` 允许网格数据重上传，是渲染管线灵活性的重要提升，符合仓库在功能丰富度上的演进方向。`59d84a7` 的依赖更新和 `e0224c6` 的ImGui上下文共享，则反映了团队在维护跨平台兼容性和提升Studio工具链用户体验上的持续投入。整体来看，本周工作以修复关键Bug和优化核心功能为主，未偏离既定的发展轨迹。

## 🔍 关键更新解析

### 🚀 新功能/特性

8/10-Allow mesh data to be reuploaded without having to recreate the mesh.（ba9a650）
  - **评分**：8/10
  - **一句话总结**：允许在不重新创建网格对象的情况下，直接更新其顶点和索引数据。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/ba9a65031b1d2d2064e64e0fb131757440f6bcf8
  - **变更规模**：+452 -304
  - **提交者**：Haroon Qureshi
  - **解决的问题**：解决了在运行时动态更新网格几何数据时，必须销毁并重新创建整个网格对象，导致性能开销和资源管理复杂的问题。
  - **产品启示**：此功能对需要实时变形或动态加载网格的应用（如可变形物体仿真、动态场景构建）至关重要，能显著提升渲染效率和开发灵活性。

### ⚡️ 性能/架构优化

6/10-studio: share ImGui and ImPlot contexts across python child extension modules.（e0224c6）
  - **评分**：6/10
  - **一句话总结**：在Studio的Python子扩展模块间共享ImGui和ImPlot上下文。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/e0224c6440cc4ab41af0656d90a44c7f7e986c34
  - **变更规模**：+54 -19
  - **提交者**：Matija Kecman
  - **解决的问题**：解决了多个Python扩展模块各自创建独立的ImGui上下文，导致UI状态不一致、资源浪费和潜在的渲染冲突问题。
  - **产品启示**：此优化是Studio工具链架构改进的一部分，通过共享上下文，可以确保UI组件间的状态同步，减少内存占用，并为未来更复杂的插件系统奠定基础。

### 🐛 Bug修复 / 其他

9/10-Fix flexcomp instability when parent body has non-identity quaternion（fe9dc58）
  - **评分**：9/10
  - **一句话总结**：修复了当柔性体（flex）的父级刚体具有非单位四元数（即存在旋转）时，柔性体组件出现数值不稳定的问题。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/fe9dc584772bf618144542682b10aa2c8d4a0120
  - **变更规模**：+146 -13
  - **提交者**：Alessio Quaglino
  - **解决的问题**：解决了柔性体在复杂运动链中因父级旋转导致的仿真发散或异常行为，这是一个影响仿真可靠性的关键Bug。
  - **产品启示**：此修复显著提升了柔性体仿真的鲁棒性，使其能更可靠地应用于机器人、生物力学等需要复杂关节和运动链的场景。

7/10-Change how ImGui clip rect scaling and scissor computation works in imgui_bridge to fix flickering and clipping errors in the web viewer（e23b504）
  - **评分**：7/10
  - **一句话总结**：修复了Web查看器中因裁剪矩形缩放和剪刀计算错误导致的闪烁和裁剪问题。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/e23b5042013a1f7219d2950bf913ac981627bc61
  - **变更规模**：+24 -15
  - **提交者**：Matija Kecman
  - **解决的问题**：解决了Web端MuJoCo查看器在渲染UI时出现的视觉闪烁和元素被错误裁剪的Bug，影响了用户体验。
  - **产品启示**：此修复直接提升了Web平台的可用性和视觉质量，对于推广MuJoCo在浏览器端的应用（如在线演示、教育）至关重要。

7/10-Fix cylinder bias stack overrun in XML parsing（d3166cb）
  - **评分**：7/10
  - **一句话总结**：修复了在XML解析圆柱体偏置（cylinder bias）参数时，可能发生的栈缓冲区溢出问题。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/d3166cb630483c26e19de6353ea72f66bdb1a25a
  - **变更规模**：+5 -3
  - **提交者**：Google DeepMind
  - **解决的问题**：修复了一个潜在的内存安全漏洞，该漏洞可能由恶意构造或格式错误的XML模型文件触发，导致程序崩溃或更严重的安全问题。
  - **产品启示**：此修复体现了项目对安全性的重视，特别是对于处理用户输入（如模型文件）的代码，防止了潜在的崩溃和安全风险。

---

6/10-Update dependencies ahead of the 3.11.0 release (retry).（59d84a7）
  - **评分**：6/10
  - **一句话总结**：为即将发布的3.11.0版本更新了项目依赖。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/59d84a714de93c85fcb1dd9028f60843639f90f5
  - **变更规模**：+102 -62
  - **提交者**：Michael Moss
  - **解决的问题**：确保新版本发布时，所有第三方库依赖（如Filament, Dear ImGui）均为兼容且稳定的版本，避免因依赖过时导致的构建或运行时问题。
  - **产品启示**：这是版本发布前的标准流程，体现了项目对稳定性和可维护性的重视，确保用户能获得一个开箱即用的可靠版本。

6/10-Fix missing timer end calls on early returns in collision and actuation（dd4d058）
  - **评分**：6/10
  - **一句话总结**：修复了在碰撞检测和驱动计算函数中，因提前返回而未调用计时器结束函数的问题。
  - **链接**：https://github.com/google-deepmind/mujoco/commit/dd4d0585ee42a185a0626e3ad39abf6f4e241e89
  - **变更规模**：+2 -0
  - **提交者**：Sam Haves
  - **解决的问题**：解决了性能分析计时器在特定代码路径下未正确停止，导致性能数据统计不准确的问题。
  - **产品启示**：此修复虽小，但确保了性能分析工具的准确性，对于开发者定位和优化仿真瓶颈至关重要。

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 5 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +531 / -606 行
- 主要贡献者: Kelly Guo, isaaclab-bot[bot], peterd-NV

## 🧭 趋势点评
本周的更新延续了仓库在2026年1月至7月期间形成的“稳定与兼容性优先”的长期趋势。具体表现为：通过修复ARM平台安装问题（af1bab4）和锁定CI版本（418ca31），持续降低跨平台部署的复杂度与测试的不稳定性，这与基线中“推进模块化安装与依赖管理”及“提升CI测试稳定性”的预测方向高度一致。同时，新增的Arena互操作功能（640cfe7）深化了与模仿学习管线的集成，呼应了基线中“深化对Mimic数据生成与模仿学习管线的性能调优”的演进路径。而准备稳定版本发布（88d3977）则标志着项目从高强度迭代期向成熟稳定期的过渡，这与基线中“准备稳定版本发布”的7月活动描述完全吻合。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-Add Isaac Lab Arena interop for imitation learning scripts (#6650) (#6690)（640cfe7）
  - **评分**：9/10
  - **一句话总结**：为模仿学习脚本新增了与Isaac Lab Arena的互操作功能。
  - **链接**：https://github.com/isaac-sim/IsaacLab/commit/640cfe75f2dc219e62db0d0d607ef3eff9159980
  - **变更规模**：+36 -8
  - **提交者**：peterd-NV
  - **解决的问题**：使Isaac Lab的模仿学习数据生成管线能够与Arena平台无缝协作，扩展了生态系统的互操作性。
  - **产品启示**：该功能降低了用户在不同机器人仿真平台间迁移模仿学习工作流的门槛，有助于吸引更广泛的开发者社区，并强化Isaac Lab作为机器人学习核心平台的地位。

### 🐛 Bug修复 / 其他
8/10-Prepare stable release as default branch (#6678)（88d3977）
  - **评分**：8/10
  - **一句话总结**：将稳定版本分支设置为默认分支，为正式发布做准备。
  - **链接**：https://github.com/isaac-sim/IsaacLab/commit/88d39772f095ae6f4b87f7543d7ec75b84e4347f
  - **变更规模**：+237 -423
  - **提交者**：Kelly Guo
  - **解决的问题**：通过调整CI工作流、模板和文档，将项目从开发分支切换到稳定发布分支，确保用户默认获取的是经过充分测试的版本。
  - **产品启示**：这是项目生命周期中的一个关键里程碑，标志着Isaac Lab从快速迭代阶段进入稳定交付阶段。此举能显著降低新用户的上手风险，增强企业级用户的采用信心。

7/10-Backport ARM nlopt install fix to 3.0.0-beta2 (#6723)（af1bab4）
  - **评分**：7/10
  - **一句话总结**：将ARM架构上nlopt安装问题的修复反向移植到3.0.0-beta2版本。
  - **链接**：https://github.com/isaac-sim/IsaacLab/commit/af1bab4dc173ba69b08fab779c14ead61d13fd33
  - **变更规模**：+150 -140
  - **提交者**：Kelly Guo
  - **解决的问题**：修复了在ARM平台（如NVIDIA Jetson）上安装nlopt依赖时失败的问题，确保了跨架构的兼容性。
  - **产品启示**：此修复直接提升了Isaac Lab在边缘计算设备上的可用性，对于希望在机器人本体上直接运行仿真或推理的用户至关重要，扩大了产品的硬件覆盖范围。

6/10-Fix Franka paths and pin CI OVRTX to 0.3 (#6695)（418ca31）
  - **评分**：6/10
  - **一句话总结**：修复了Franka机器人相关的路径问题，并将CI中的OVRTX版本锁定至0.3。
  - **链接**：https://github.com/isaac-sim/IsaacLab/commit/418ca31b47a8eb27db8aefcfc134e4c4f1d2b6f3
  - **变更规模**：+73 -16
  - **提交者**：Kelly Guo
  - **解决的问题**：解决了因路径变更导致的Franka机器人模型加载失败问题，并通过锁定OVRTX版本避免了因依赖更新引发的CI测试不稳定。
  - **产品启示**：路径修复确保了常用机器人模型（Franka）的可用性，而锁定CI版本则体现了对测试可靠性的持续投入。这有助于维护核心功能的稳定性，减少因外部依赖变动带来的意外中断。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 37 条
- 高价值提交（≥6分）: 10 条
- 代码更新规模: +12323 / -2189 行
- 主要贡献者: Eric Shi, Zach Corse, Eliot Xing

## 🧭 趋势点评

本周的更新延续了仓库在2026年上半年的核心演进方向，即**提升仿真与强化学习工作流的性能、可扩展性与可靠性**。具体表现为：通过支持CPU HashGrid和BVH的图回放（`17e26ef`、`0956d10`），深化了GPU图捕获与内存管理这一长期重点；通过修复图内存释放bug（`7c3dc52`）和增强APIC内存健壮性（`ed58c11`），持续强化稳定性；通过新增JAX内核块大小支持（`a05b533`）和NumPy风格切片（`c07653a`），扩展了与主流科学计算生态的互操作性。同时，新增的ARM64 GPU CI覆盖（`b64fbe5`）和锁定CUDA工具包设置（`91e590b`）体现了对平台扩展和开发者体验的重视，这与仓库文档与工具链改进的趋势一致。整体来看，本周提交在巩固已有性能优化成果的基础上，重点向**图执行的可移植性**和**生态集成**方向拓展，未出现偏离长期趋势的突变。

## 🔍 关键更新解析

### 🚀 新功能/特性

9/10-Add NumPy-style tile slicing and fancy indexing (GH-1176)（c07653a）
  - **评分**: 9/10
  - **一句话总结**: 为tile操作引入了NumPy风格的切片和花式索引功能。
  - **链接**: https://github.com/NVIDIA/warp/commit/c07653a0759e48e58afb78fcd93ca41a5944cd75
  - **变更规模**: +1885 -59
  - **提交者**: Zach Corse
  - **解决的问题**: 解决了用户无法使用直观的NumPy语法操作tile张量的问题，降低了学习成本。
  - **产品启示**: 大幅提升了Warp在数据预处理和科学计算场景下的易用性，吸引更多NumPy用户迁移至Warp进行高性能计算。

9/10-Support CPU HashGrid graph replay [GH-1664]（17e26ef）
  - **评分**: 9/10
  - **一句话总结**: 支持在CPU图捕获中回放HashGrid操作。
  - **链接**: https://github.com/NVIDIA/warp/commit/17e26ef1e78a6c98dde24978d1c19578591003e2
  - **变更规模**: +935 -76
  - **提交者**: Eric Shi
  - **解决的问题**: 解决了CPU图捕获无法记录和回放HashGrid（常用于粒子搜索）的问题，限制了CPU端图执行的完整性。
  - **产品启示**: 使得基于HashGrid的仿真（如SPH流体、N体模拟）能够在CPU图模式下高效执行，提升了Warp在无GPU环境下的可用性和性能。

8/10-Add ARM64 GPU CI coverage and diagnostics（b64fbe5）
  - **评分**: 8/10
  - **一句话总结**: 为ARM64 GPU架构添加了持续集成测试覆盖和诊断功能。
  - **链接**: https://github.com/NVIDIA/warp/commit/b64fbe5b2eed380f1c7f62508a1fa53b94df9e65
  - **变更规模**: +48 -2
  - **提交者**: Eric Shi
  - **解决的问题**: 填补了ARM64 GPU平台（如NVIDIA Jetson系列）的测试空白，确保Warp在该架构上的稳定运行。
  - **产品启示**: 扩展了对边缘计算和嵌入式设备的支持，使Warp能应用于更广泛的硬件场景，如机器人、自动驾驶等。

8/10-Replay BVH updates in CPU graph capture [GH-1665]（0956d10）
  - **评分**: 8/10
  - **一句话总结**: 支持在CPU图捕获中回放BVH（包围体层次结构）更新操作。
  - **链接**: https://github.com/NVIDIA/warp/commit/0956d106b75ebab1c6e238e194d4f72a150daed4
  - **变更规模**: +315 -0
  - **提交者**: Nicolas Capens
  - **解决的问题**: 解决了CPU图捕获无法记录和回放BVH更新（常用于碰撞检测）的问题，限制了CPU端图执行的适用范围。
  - **产品启示**: 使得依赖BVH的仿真（如刚体碰撞、光线追踪）能够在CPU图模式下高效执行，进一步扩展了Warp图执行的可移植性。

7/10-Add locked CUDA toolkit setup（91e590b）
  - **评分**: 7/10
  - **一句话总结**: 新增锁定CUDA工具包版本的功能，简化了CI/CD环境配置。
  - **链接**: https://github.com/NVIDIA/warp/commit/91e590b440060861a4bb8a667c63e385d766f277
  - **变更规模**: +1921 -70
  - **提交者**: Eric Shi
  - **解决的问题**: 解决了因CUDA工具包版本不一致导致的构建环境不稳定问题，降低了开发者配置环境的复杂度。
  - **产品启示**: 对于依赖特定CUDA版本的用户，此功能可确保构建环境的一致性，减少因环境差异引发的兼容性问题，提升开发效率。

7/10-Add JAX kernel block sizes [GH-1436]（a05b533）
  - **评分**: 7/10
  - **一句话总结**: 新增了在JAX互操作中指定内核块大小的功能。
  - **链接**: https://github.com/NVIDIA/warp/commit/a05b5333c1bf3f214b6c3b325efb9f9cea5600db
  - **变更规模**: +232 -12
  - **提交者**: Eric Shi
  - **解决的问题**: 解决了Warp与JAX互操作时无法精细控制CUDA内核块大小的问题，限制了性能调优能力。
  - **产品启示**: 增强了与JAX生态的集成深度，允许用户针对特定硬件和计算负载进行更精细的性能调优，提升混合框架工作流的效率。

### 🐛 Bug修复 / 其他

8/10-Fix graph memory deallocation during conditional child graph capture (GH-1641)（7c3dc52）
  - **评分**: 8/10
  - **一句话总结**: 修复了在条件子图捕获过程中图内存释放的错误。
  - **链接**: https://github.com/NVIDIA/warp/commit/7c3dc52baea2a4fd23bd5e6f26611204664c84ef
  - **变更规模**: +116 -8
  - **提交者**: Lukasz Wawrzyniak
  - **解决的问题**: 解决了在捕获包含条件分支的子图时，内存可能被错误释放或泄漏的问题，这是图执行稳定性的关键bug。
  - **产品启示**: 此修复对于构建复杂、动态的仿真图至关重要，能防止因内存管理错误导致的程序崩溃或性能下降，提升了图执行功能的可靠性。

7/10-Harden APIC memory region loading（ed58c11）
  - **评分**: 7/10
  - **一句话总结**: 增强了APIC（Affine Particle-In-Cell）内存区域加载的健壮性。
  - **链接**: https://github.com/NVIDIA/warp/commit/ed58c1118ecb862b17368a51388a7f39d0ddafd7
  - **变更规模**: +211 -71
  - **提交者**: Eric Shi
  - **解决的问题**: 修复了APIC内存加载过程中可能出现的边界条件或错误处理不足问题，提升了仿真稳定性。
  - **产品启示**: 对于使用APIC方法的流体或材料仿真用户，此修复能减少因内存错误导致的仿真崩溃或数据损坏，提升可靠性。

6/10-Fix Jacobian plotting for functions and typed kernels [GH-1672]（41f0ccd）
  - **评分**: 6/10
  - **一句话总结**: 修复了函数和类型化内核的雅可比矩阵绘图功能。
  - **链接**: https://github.com/NVIDIA/warp/commit/41f0ccdb0b38f4f0698bcc8b2c22f4545560f34f
  - **变更规模**: +345 -62
  - **提交者**: Eric Shi
  - **解决的问题**: 解决了调试工具中雅可比矩阵可视化功能失效的问题，影响了梯度调试体验。
  - **产品启示**: 修复了开发者调试自动微分结果的关键工具，有助于用户更高效地诊断和验证梯度计算的正确性。

6/10-Fix tile_matmul for strided tile operands [GH-1667]（2396730）
  - **评分**: 6/10
  - **一句话总结**: 修复了步长tile操作数在tile矩阵乘法中的错误。
  - **链接**: https://github.com/NVIDIA/warp/commit/2396730986d7f61a20e99fc8dd552d7cc5e66821
  - **变更规模**: +346 -46
  - **提交者**: Eliot Xing
  - **解决的问题**: 解决了当tile矩阵乘法的输入操作数在内存中非连续（有步长）时，计算结果不正确的问题。
  - **产品启示**: 修复了线性代数核心操作的一个边界情况，确保了在更广泛的数据布局下计算的正确性，提升了库的健壮性。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 10 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +17762 / -285 行
- 主要贡献者: Peihong Wang, 石乐同, Shuaihang Chen

## 🧭 趋势点评

本周更新延续了仓库在具身智能与强化学习领域的强劲演进势头，并进一步强化了其作为综合性机器人学习平台的核心定位。新增的SGLang VLM奖励服务器、OpenVLA-OFT OPD训练、pi0.5行为SFT等特性，与长期趋势中“多模态大模型在机器人任务中的应用”及“行为克隆与强化学习深度融合”高度吻合。同时，对Intel XPU和昆仑芯硬件的支持，以及RoboCasa365仿真环境的集成，体现了项目在硬件生态和仿真场景覆盖上的持续扩展，这与仓库基线中“支持多种仿真器和硬件”的战略方向一致。此外，修复Maniskill内存泄漏和全局解释方差等Bug，也反映了项目在快速迭代中兼顾稳定性的长期策略。

## 🔍 关键更新解析

### 🚀 新功能/特性

10/10-feat(openpi_pytorch): add pi0.5 behavior sft + eval path (#1254)（60165be）
  - **评分**：10/10
  - **一句话总结**：新增pi0.5模型的行为克隆SFT训练与评估完整流程，是本周规模最大的特性提交。
  - **链接**：https://github.com/RLinf/RLinf/commit/60165be54d840e91840ed2a02a453adcc5457866
  - **变更规模**：+10546 -1
  - **提交者**：Xzxuan
  - **解决的问题**：此前缺乏对pi0.5这一重要VLA模型的行为克隆训练支持，限制了用户在该模型上的应用。
  - **产品启示**：pi0.5作为轻量级VLA模型，其SFT路径的加入，使得用户可以在有限计算资源下，利用行为克隆快速训练机器人策略，为后续的RL微调或真实世界部署提供了坚实基础。

9/10-feat(embodiment): support SGLang VLM reward server (#1314)（6add8b4）
  - **评分**：9/10
  - **一句话总结**：新增基于SGLang的视觉语言模型奖励服务器，为具身智能任务提供更强大的奖励信号。
  - **链接**：https://github.com/RLinf/RLinf/commit/6add8b419ed667eada204ac81c9d5913706cd6cc
  - **变更规模**：+1175 -130
  - **提交者**：Shuaihang Chen
  - **解决的问题**：此前缺乏对VLM作为奖励模型的原生支持，限制了复杂视觉任务中奖励设计的灵活性。
  - **产品启示**：该特性使开发者能直接利用SGLang部署的VLM生成奖励，显著降低了在机器人操作、导航等视觉密集型任务中设计奖励函数的门槛，有望加速具身智能算法的迭代。

9/10-feat(embodiment): add OpenVLA-OFT OPD training (#1377)（f469f9a）
  - **评分**：9/10
  - **一句话总结**：新增OpenVLA模型的在线策略蒸馏（OPD）训练支持，扩展了策略学习范式。
  - **链接**：https://github.com/RLinf/RLinf/commit/f469f9a5d0b8d0439ded3f420b93ed80fff845bb
  - **变更规模**：+1251 -50
  - **提交者**：Zhennan Jiang
  - **解决的问题**：此前框架主要支持离线训练或在线RL，缺乏将预训练VLA模型通过在线交互进行高效蒸馏的路径。
  - **产品启示**：OPD训练允许用户利用强大的预训练模型（如OpenVLA）作为教师，通过在线交互高效训练轻量级学生策略，这对于在真实机器人上实现低延迟、高精度的控制至关重要。

8/10-feat(embodiment): add RoboCasa365 support (#1349)（d9f3d8a）
  - **评分**：8/10
  - **一句话总结**：新增对RoboCasa365仿真环境的支持，丰富了可用的机器人训练场景。
  - **链接**：https://github.com/RLinf/RLinf/commit/d9f3d8a9db4d7aad1d641029293295503dd3eb2c
  - **变更规模**：+2514 -15
  - **提交者**：Diddan2233
  - **解决的问题**：此前框架支持的仿真器有限，缺少面向家庭服务机器人的RoboCasa365环境。
  - **产品启示**：RoboCasa365提供了丰富的家庭场景和任务，其集成使得RLinf能够更好地服务于家庭服务机器人、人机交互等应用场景的研究与开发。

7/10-feat(dual-franka): add LeRobot merge and delete utilities (#1331)（4677808）
  - **评分**：7/10
  - **一句话总结**：为双Franka机器人平台新增LeRobot数据集的合并与删除工具，提升数据管理效率。
  - **链接**：https://github.com/RLinf/RLinf/commit/4677808adb9caa5fc3eaddeed0d5e360ed66070a
  - **变更规模**：+1732 -0
  - **提交者**：Code-Hit-ai
  - **解决的问题**：在双Franka机器人上进行数据采集后，缺乏便捷的工具来合并或清理LeRobot格式的数据集。
  - **产品启示**：该工具简化了真实机器人数据的管理流程，对于需要大量数据采集和清洗的DAgger、行为克隆等范式至关重要，提升了真实世界机器人研究的工程效率。

7/10-fix: support intel xpu (#1389)（9c575b9）
  - **评分**：7/10
  - **一句话总结**：新增对Intel XPU（如Intel GPU）的硬件支持，扩展了可用的计算平台。
  - **链接**：https://github.com/RLinf/RLinf/commit/9c575b9303ecbb89db81b1bc915c254931709d93
  - **变更规模**：+66 -1
  - **提交者**：beckwen
  - **解决的问题**：此前框架主要针对NVIDIA GPU优化，缺乏对Intel XPU的原生支持。
  - **产品启示**：支持Intel XPU降低了用户对特定硬件的依赖，使得更多使用Intel计算平台的开发者能够参与机器人学习研究，有助于扩大用户基础。

7/10-feat(device): add Kunlunxin hardware support (#1399)（2005d39）
  - **评分**：7/10
  - **一句话总结**：新增对昆仑芯硬件的支持，进一步丰富了硬件生态。
  - **链接**：https://github.com/RLinf/RLinf/commit/2005d39598322fafc3f93d9843d6409598f6201f
  - **变更规模**：+147 -0
  - **提交者**：DearFishi
  - **解决的问题**：此前框架不支持国产昆仑芯AI加速卡，限制了其在特定硬件环境下的部署。
  - **产品启示**：对昆仑芯的支持体现了项目对国产硬件生态的重视，有助于在信创和特定行业应用中推广RLinf，增强其在不同计算基础设施下的适应能力。

### ⚡️ 性能/架构优化

*本周无明确属于此分类的高价值提交。*

### 🐛 Bug修复 / 其他

8/10-fix: compute critic explained variance globally (#1386)（0f9ea98）
  - **评分**：8/10
  - **一句话总结**：修复Critic网络解释方差的计算方式，改为全局计算以提供更准确的模型评估指标。
  - **链接**：https://github.com/RLinf/RLinf/commit/0f9ea98c7a6d9e3ade24e8f4846c64d3b135dbcc
  - **变更规模**：+325 -58
  - **提交者**：Peihong Wang
  - **解决的问题**：此前解释方差的计算可能基于局部或错误的数据范围，导致评估指标失真，影响对Critic网络性能的判断。
  - **产品启示**：准确的评估指标是算法调优的基础。此修复确保了用户能获得可靠的Critic性能反馈，从而更有效地诊断和优化强化学习算法。

---

6/10-fix(maniskill): remove unsafe force_gc_tensor from offload cleanup (#1404)（2617980）
  - **评分**：6/10
  - **一句话总结**：修复Maniskill环境中卸载清理时的不安全强制垃圾回收操作，消除潜在的内存泄漏风险。
  - **链接**：https://github.com/RLinf/RLinf/commit/26179807d701950cf2933554bfb9bb596e662b68
  - **变更规模**：+0 -26
  - **提交者**：石乐同
  - **解决的问题**：此前在环境卸载清理时调用了不安全的`force_gc_tensor`，可能导致内存泄漏或程序崩溃。
  - **产品启示**：该修复提升了框架在长时间训练或复杂仿真场景下的稳定性，是保障大规模实验可靠运行的关键细节优化。

