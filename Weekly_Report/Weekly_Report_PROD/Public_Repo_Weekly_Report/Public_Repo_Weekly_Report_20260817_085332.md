# 具身智能周报 (2026年08月17日 08:53:32)

## 行业风向总览

### 具身智能行业风向总结（本周）

**技术焦点**：物理仿真精度与模型架构创新双线并进。MuJoCo 重写 box-box 碰撞检测（SAT+多边形裁剪）并为可变形体新增连续碰撞基础设施，显著提升接触真实性与柔性体仿真可靠性；RLinf 则新增 DeepseekV3/Kimi-K2 MoE 架构支持，并将 OpenPI 迁移至 JAX-aligned PyTorch Pi0.5，拓展了 VLA 模型的选择空间与跨框架兼容性。

**合成数据动态**：本周无直接相关提交。但 MuJoCo 对纹理坐标的支持及 Warp 新增 FDTD 电磁仿真示例，间接提升了仿真场景的视觉保真度与领域覆盖，为高质量合成数据生成提供了更逼真的物理与视觉基础。

**产品经理关注信号**：
1. **柔性体仿真能力跃升**：MuJoCo 连续碰撞基础设施为医疗仿真、软体机器人操作等新兴场景铺路，值得评估相关产品机会。
2. **国产硬件生态布局**：RLinf 新增 MUSA 支持，释放出适配多元化算力平台的信号，对面向特定区域市场的产品具有战略价值。
3. **真实世界数据采集安全性**：RLinf 的平滑干预功能提升了 DAgger 流程的实用性与安全性，是具身智能从仿真走向部署的关键一步，建议关注其在数据飞轮产品中的应用潜力。
4. **框架互操作性与稳定性**：Warp 修复 PyTorch Tape 互操作梯度问题并稳定代码生成，降低了混合框架开发风险，对构建跨平台工具链的产品经理是利好。

---

## 各仓库详细分析

### [mujocolab/mjlab] 本周无新提交。


---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 13 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +4613 / -1379 行
- 主要贡献者: Yuval Tassa, Sam Haves, Matija Kecman

## 🧭 趋势点评

本周更新延续了该仓库在碰撞检测算法深度优化与渲染能力扩展上的长期主线，同时呈现出向“可变形体连续碰撞”这一前沿方向发力的新趋势。box-box 碰撞检测的完全重写（SAT + 多边形裁剪 + 真实边-边接触）与 GJK 多点接触 witness point 修复，均是对核心物理引擎精度与鲁棒性的根本性投入，与过去六个月中 GJK 网格爬山加速、EPA 内存复用等优化脉络一脉相承。与此同时，为可变形体新增的连续碰撞基础设施（+1496 行全新代码）标志着 MuJoCo 在柔性体仿真能力上的战略性加码，与近期 flex 性能优化、2D 膜弹性等提交形成呼应。纹理坐标支持与资产预取优化则延续了渲染与 Web Viewer 体验的持续打磨。整体来看，本周提交在“物理精度”与“功能广度”两个维度上均实现了显著推进，且未偏离仓库以性能优化和仿真能力扩展为核心的发展轨迹。

## 🔍 关键更新解析

### 🚀 新功能/特性

10/10-Rewrite box-box collision: SAT + polygon clipping + true edge-edge contacts.（86e9860）
- **评分**：10/10
- **一句话总结**：完全重写 box-box 碰撞检测算法，采用 SAT（分离轴定理）+ 多边形裁剪 + 真实边-边接触，取代原有实现。
- **链接**：https://github.com/google-deepmind/mujoco/commit/86e98601069a346036c7a518d75bd7fb647fc77c
- **变更规模**：+2297 -807，涉及 5 个文件
- **提交者**：Yuval Tassa
- **解决的问题**：旧版 box-box 碰撞在边-边接触场景下缺乏真实接触几何，导致接触点/法线不准确，影响仿真稳定性和物理真实性。
- **产品启示**：显著提升涉及箱体交互的仿真场景（如抓取、堆叠、操作任务）的物理保真度，为机器人操作和物流仿真提供更可靠的接触建模基础。

9/10-Add continuous-collision infrastructure for deformables（b924ac6）
- **评分**：9/10
- **一句话总结**：为可变形体新增连续碰撞检测基础设施，包含全新的 `engine_collision_continuous.c/h` 模块及配套测试。
- **链接**：https://github.com/google-deepmind/mujoco/commit/b924ac66bdf3251e2192c153de2280f6f8d3ecfc
- **变更规模**：+1496 -0，涉及 5 个文件
- **提交者**：Alessio Quaglino
- **解决的问题**：可变形体（flex）在高速运动或大变形场景下存在隧穿（tunneling）问题，离散碰撞检测无法捕捉帧间穿透，需要连续碰撞检测来保证物理正确性。
- **产品启示**：为柔性体仿真（如布料、软组织、线缆）在高速交互场景下的可靠性奠定基础，拓展 MuJoCo 在医疗仿真、机器人软体操作等领域的应用边界。

7/10-Add texture coordinates to primitive shape types.（cc7fb98）
- **评分**：7/10
- **一句话总结**：为基本几何体（primitive shapes）新增纹理坐标支持，覆盖 Filament 与 Classic 渲染路径。
- **链接**：https://github.com/google-deepmind/mujoco/commit/cc7fb98cf45ed697589c06e7e1d12b338ca53e98
- **变更规模**：+556 -372，涉及 5 个文件
- **提交者**：Sam Haves
- **解决的问题**：此前基本几何体无法正确映射纹理，限制了视觉真实感和场景定制能力。
- **产品启示**：提升仿真场景的视觉质量与真实感，对需要高保真视觉反馈的应用（如数字孪生、自动驾驶仿真、机器人遥操作界面）具有直接价值。

### ⚡️ 性能/架构优化

6/10-Optimize and robustify asset prefetching and material loading.（fca913b）
- **评分**：6/10
- **一句话总结**：优化并加固 Web Viewer 的资产预取与材质加载流程，提升加载可靠性与效率。
- **链接**：https://github.com/google-deepmind/mujoco/commit/fca913b4f544f4a1ebe2b722b4158b8975bccd17
- **变更规模**：+95 -54，涉及 5 个文件
- **提交者**：Matija Kecman
- **解决的问题**：Web Viewer 在加载复杂场景时存在资产预取失败或材质加载不稳定的问题，影响用户体验和场景加载速度。
- **产品启示**：提升 MuJoCo Web Viewer 在浏览器端的场景加载速度与稳定性，改善远程协作、教学演示和 Web 端机器人仿真的用户体验。

### 🐛 Bug修复 / 其他

6/10-Compute correct witness point info for multicontact.（ab1af24）
- **评分**：6/10
- **一句话总结**：修复 GJK 碰撞检测中多点接触（multicontact）场景下 witness point 信息计算错误的问题。
- **链接**：https://github.com/google-deepmind/mujoco/commit/ab1af24911c331b4445cc6e6be0c948d7888103e
- **变更规模**：+28 -18，涉及 1 个文件
- **提交者**：Kyle Bayes
- **解决的问题**：多点接触时 witness point 计算不准确，可能导致接触点位置偏差，进而影响接触力的分布和仿真稳定性。
- **产品启示**：提升复杂接触场景（如多面体互锁、密集堆叠）下接触信息的准确性，对依赖精确接触力反馈的强化学习训练和机器人控制应用具有积极意义。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 2 条
- 高价值提交（≥6分）: 1 条
- 代码更新规模: +244 / -0 行
- 主要贡献者: Kelly Guo

## 🧭 趋势点评

本周更新延续了 IsaacLab 在 CI/CD 自动化与基础设施稳定性上的长期投入方向。过去六个月中，项目持续优化 CI 流水线（如修复超时、减少 flakiness、改进 Docker 清理），本周新增的 nightly Isaac Sim 镜像自动更新工作流正是这一趋势的进一步深化——将依赖更新从手动操作转为自动化流程，与仓库此前频繁手动更新 Isaac Sim 版本（如 6.0.1）的节奏形成互补。该提交虽为单一 CI 功能，但体现了项目从"被动修复"向"主动预防"的运维理念转变，与整体 roadmap 中"增强 CI/CD 流水线的稳定性与效率"的预测方向高度一致。

## 🔍 关键更新解析

### 🚀 新功能/特性

6/10-[CI] Add nightly Isaac Sim image updater (#6994)（941d48f）
- **评分**：6/10
- **一句话总结**：新增 nightly CI 工作流，自动更新 Isaac Sim 镜像至最新版本。
- **链接**：https://github.com/isaac-sim/IsaacLab/commit/941d48f0d9e331643b1b28dae905a2540659dd07
- **变更规模**：+243 -0（新增 .github/workflows/nightly-isaacsim-image.yml）
- **提交者**：Kelly Guo
- **解决的问题**：此前 Isaac Sim 版本更新依赖手动提交（如 2026-06 的 fa0fa7a 更新至 6.0.1），流程繁琐且容易滞后。该自动化工作流可每日检查并更新 Isaac Sim 镜像，减少人工干预，确保仓库始终跟踪上游最新版本，降低因版本滞后导致的兼容性问题。
- **产品启示**：自动化依赖更新是提升项目长期可维护性的关键投资。对用户而言，这意味着更及时的 Isaac Sim 兼容性保障；对维护者而言，减少了重复性手动工作，可将精力聚焦于核心功能开发。该模式值得推广至其他频繁更新的依赖项（如 URDF Importer、Mocks 等）。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 27 条
- 高价值提交（≥6分）: 13 条
- 代码更新规模: +5924 / -1989 行
- 主要贡献者: Eric Shi, Zach Corse, Alec Jacobson

## 🧭 趋势点评

本周更新延续了 NVIDIA/warp 仓库在自动微分正确性、代码生成稳定性与互操作性方面的长期投入，与基线中“新功能与问题修复占比最大”的整体特征高度一致。本周提交高度集中于 `wp.autograd` 梯度检查与 tape 记录语义的修复（如 1168a56、4cb1423、c4675e0），这与 2026-07 以来对自动微分精度与自定义梯度兼容性的持续强化一脉相承；同时，26992cb 与 9bf50af 对模块代码生成稳定性的加固，呼应了基线中“编译优化可能影响代码生成稳定性”的风险预判，体现了项目在快速迭代中对底层可靠性的重视。此外，77969e3 按 LLVM 版本区分 CPU 缓存，延续了基线中“依赖更新（如 LLVM）需持续验证稳定性”的工程化思路；80d448d 新增 FDTD 示例与 e37c454 的 PyTorch Tape 互操作文档，则进一步落实了基线中“通过新增 API 和文档降低使用门槛”的生态建设方向。整体来看，本周更新未偏离仓库长期趋势，而是在自动微分、代码生成与文档互操作三个关键维度上进行了深度加固。

## 🔍 关键更新解析

### 🚀 新功能/特性

7/10-Add single-GPU FDTD Luneburg lens example [GH-1772]（80d448d）
- **评分**：7/10
- **一句话总结**：新增单 GPU FDTD Luneburg 透镜示例，展示了 Warp 在电磁仿真领域的应用能力。
- **链接**：https://github.com/NVIDIA/warp/commit/80d448d623b9c98a346ffbe3f1180d14a72ee783
- **变更规模**：+564 -2
- **提交者**：Sheel Nidhan
- **解决的问题**：缺乏面向电磁仿真场景的完整示例，新用户难以快速上手相关领域应用。
- **产品启示**：通过提供领域示例（如 FDTD），降低了物理仿真用户的使用门槛，有助于吸引更广泛的科学计算社区，并验证 Warp 在高性能计算场景下的实际表现。

6/10-Expand debug-mode test suite coverage（18866f0）
- **评分**：6/10
- **一句话总结**：扩展了调试模式下的测试套件覆盖范围，增强了对调试路径的验证能力。
- **链接**：https://github.com/NVIDIA/warp/commit/18866f004d3a2e17ee0a953569f1f55ba2648cc4
- **变更规模**：+337 -13
- **提交者**：Eric Shi
- **解决的问题**：调试模式下测试覆盖不足，可能导致调试路径中的回归未被及时发现。
- **产品启示**：提升调试模式下的测试覆盖有助于在开发阶段更早暴露问题，降低用户在使用调试功能时遇到未预期行为的风险，增强框架在开发与生产环境中的一致性体验。

### ⚡️ 性能/架构优化

7/10-Key CPU cache by LLVM version [GH-1759]（77969e3）
- **评分**：7/10
- **一句话总结**：将 CPU 缓存键与 LLVM 版本关联，避免因 LLVM 升级导致的缓存失效或误用。
- **链接**：https://github.com/NVIDIA/warp/commit/77969e3c7bcf49017771bca0c099ac54fbf7d1e0
- **变更规模**：+80 -32
- **提交者**：Eric Shi
- **解决的问题**：不同 LLVM 版本生成的代码可能存在差异，统一缓存键可能导致版本间缓存冲突或错误复用。
- **产品启示**：该优化提升了多版本环境下的构建稳定性与缓存命中率，减少因依赖升级带来的重复编译开销，对依赖频繁更新的用户尤为友好。

### 🐛 Bug修复 / 其他

8/10-Fix tape-recorded copy adjoint: accumulate into source, consume destination [GH-1728]（4cb1423）
- **评分**：8/10
- **一句话总结**：修复 tape 记录的复制操作伴随梯度计算，改为累加到源变量并消费目标变量。
- **链接**：https://github.com/NVIDIA/warp/commit/4cb14232712edb6a69e8e7dffaa7fc4da68c3ad2
- **变更规模**：+522 -6
- **提交者**：Zach Corse
- **解决的问题**：此前 tape 记录复制操作的梯度方向错误，导致梯度计算不正确。
- **产品启示**：修复自动微分核心语义问题，确保基于 tape 的互操作场景（如 PyTorch 集成）中梯度计算正确性，增强框架在混合框架工作流中的可靠性。

8/10-Stabilize Module Codegen [GH-1738]（26992cb）
- **评分**：8/10
- **一句话总结**：稳定模块代码生成流程，修复了代码生成中的不确定性问题。
- **链接**：https://github.com/NVIDIA/warp/commit/26992cb1d2cda20e45b2818fd72312e20756f4fb
- **变更规模**：+180 -22
- **提交者**：Eric Shi
- **解决的问题**：模块代码生成存在不稳定性，可能导致生成的代码在不同环境下行为不一致。
- **产品启示**：代码生成稳定性是编译型框架可信赖的基础，该修复降低了跨平台、跨版本环境下的行为差异风险，提升了框架的可复现性。

8/10-Fix wp.autograd gradient checks for input-mutating functions and mixed precision [GH-1726]（1168a56）
- **评分**：8/10
- **一句话总结**：修复了输入修改函数与混合精度场景下的自动梯度检查逻辑。
- **链接**：https://github.com/NVIDIA/warp/commit/1168a568714ffd63d3d561b326e668da5b3d5359
- **变更规模**：+461 -148
- **提交者**：Zach Corse
- **解决的问题**：梯度检查在输入被修改或使用混合精度时可能产生误报或漏报。
- **产品启示**：提升梯度检查的准确性，帮助开发者在复杂数值场景下更可靠地验证梯度实现，降低自动微分使用中的调试成本。

7/10-Improve verify_autograd_array_access overwrite warnings: consumed read flags and call-site attribution [GH-1727]（c4675e0）
- **评分**：7/10
- **一句话总结**：改进了自动梯度数组访问覆盖警告，新增已消费读标志与调用点归因。
- **链接**：https://github.com/NVIDIA/warp/commit/c4675e0c4c3e14fea07829f8853ca6e4c82a9bde
- **变更规模**：+262 -10
- **提交者**：Zach Corse
- **解决的问题**：原有警告信息不够精确，难以定位数组被覆盖的具体调用位置，且未区分读标志的消费状态。
- **产品启示**：更精准的警告信息能帮助开发者快速定位自动微分中的潜在错误，减少调试时间，提升开发体验。

7/10-Fail the module when a kernel fails to build [GH-1713]（9bf50af）
- **评分**：7/10
- **一句话总结**：当内核构建失败时，模块加载将直接失败，而非静默忽略。
- **链接**：https://github.com/NVIDIA/warp/commit/9bf50af2139982db0aa566cd8670132b2beab00c
- **变更规模**：+222 -149
- **提交者**：Eric Shi
- **解决的问题**：此前内核构建失败可能被静默吞掉，导致后续运行出现难以排查的异常行为。
- **产品启示**：将构建失败显式化有助于快速定位问题根因，避免用户在不稳定状态下继续执行，提升框架的健壮性与可诊断性。

7/10-Fix autograd backward options [GH-1718]（dc57433）
- **评分**：7/10
- **一句话总结**：修复了自动梯度反向传播选项的处理逻辑。
- **链接**：https://github.com/NVIDIA/warp/commit/dc57433ee49e9863a355fefa6dae56fd3612b085
- **变更规模**：+218 -4
- **提交者**：Eric Shi
- **解决的问题**：自动梯度反向传播选项在特定场景下未正确生效，导致梯度计算行为与预期不符。
- **产品启示**：修复反向传播选项的语义一致性，确保用户自定义梯度行为可预期，增强自动微分功能的灵活性与可控性。

7/10-Fix JAX FFI cache identity [GH-1215]（66d354f）
- **评分**：7/10
- **一句话总结**：修复 JAX FFI 缓存标识问题，避免缓存误命中。
- **链接**：https://github.com/NVIDIA/warp/commit/66d354fe3278c57a1b4ffc17e72a89307026e56c
- **变更规模**：+254 -4
- **提交者**：Eric Shi
- **解决的问题**：JAX FFI 缓存标识不唯一，可能导致不同内核间缓存错误复用。
- **产品启示**：修复跨框架互操作中的缓存一致性问题，提升 JAX 集成场景下的稳定性与性能表现。

7/10-Document PyTorch Tape interop [GH-1737]（e37c454）
- **评分**：7/10
- **一句话总结**：新增 PyTorch Tape 互操作文档，并同步更新相关示例与实现。
- **链接**：https://github.com/NVIDIA/warp/commit/e37c45487ed688ad11df9f0a350fc943e4c492a5
- **变更规模**：+494 -134
- **提交者**：Zach Corse
- **解决的问题**：PyTorch Tape 互操作缺乏系统性文档，用户难以理解与使用该功能。
- **产品启示**：完善互操作文档降低了混合框架开发的学习成本，有助于吸引 PyTorch 用户群体，扩大 Warp 在深度学习与仿真结合场景中的影响力。

---

6/10-Fix compile-time optimizer eval staging and scan（bb8bb04）
- **评分**：6/10
- **一句话总结**：修复编译期优化器的评估暂存与扫描逻辑。
- **链接**：https://github.com/NVIDIA/warp/commit/bb8bb047a6352d936695e2e17df7954f136bedeb
- **变更规模**：+187 -124
- **提交者**：Eric Shi
- **解决的问题**：编译期优化器在评估暂存与扫描阶段存在逻辑缺陷，可能影响优化效果。
- **产品启示**：修复编译期优化器逻辑有助于提升生成代码的质量，间接改善运行时性能与资源利用效率。

6/10-Ignore trailing BSR capacity [GH-1769]（57846fd）
- **评分**：6/10
- **一句话总结**：修复稀疏矩阵 BSR 格式中尾部容量处理问题。
- **链接**：https://github.com/NVIDIA/warp/commit/57846fd89a8e37264465596314a18c896b01796a
- **变更规模**：+87 -2
- **提交者**：Eric Shi
- **解决的问题**：BSR 稀疏矩阵的尾部容量可能被错误计入，导致内存或计算行为异常。
- **产品启示**：修复稀疏矩阵边界情况，提升大规模稀疏计算场景下的稳定性与内存使用效率。

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 10 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +9418 / -1377 行
- 主要贡献者: Andy Lin, 上坂 茅羽耶, sherlockcooper

## 🧭 趋势点评

本周更新高度契合仓库长期演进方向，并进一步加速了“全栈具身智能平台”的构建进程。一方面，`EmbodiedFSDPActor` 模块拆分、CUDA-EGL 映射修复等提交延续了近期对分布式训练稳定性和硬件适配的持续投入；另一方面，新增 MoE 架构（DeepseekV3/Kimi-K2）支持、OpenPI 迁移至 JAX-aligned PyTorch Pi0.5、MUSA 硬件支持以及 ManiSkill 中 RLT TD3 策略的引入，标志着项目正从单一 RL 框架向覆盖多模型架构、多硬件平台、多机器人环境的综合生态迈进。尤其值得关注的是，平滑干预（smooth intervention）功能的加入，进一步深化了真实世界部署中的人机交互能力，与仓库此前在 VR/HG-DAgger 方向的工作形成连贯的技术积累。整体来看，本周提交在功能扩展与架构优化上双线并进，未偏离长期趋势，反而在模型多样性和硬件兼容性上实现了显著突破。

## 🔍 关键更新解析

### 🚀 新功能/特性

8/10-feat: add DeepseekV3/Kimi-K2 MoE architecture support (#1437)（3d01d7e）
- **评分**：8/10
- **一句话总结**：新增对 DeepseekV3 和 Kimi-K2 两款 MoE（混合专家）大模型架构的支持。
- **链接**：https://github.com/RLinf/RLinf/commit/3d01d7eb25bfb516b88a7091e0e6f25b224f12b5
- **变更规模**：+1518 -79
- **提交者**：sherlockcooper
- **解决的问题**：此前框架主要支持稠密模型，无法利用 MoE 架构在推理效率与模型容量上的优势，限制了在 agentic 场景下对前沿大模型的接入。
- **产品启示**：支持 MoE 架构使 RLinf 能够适配当前最具性价比的大模型，显著扩展了语言模型作为策略骨干或奖励模型的选择空间，对 agentic AI 与具身智能结合的应用场景具有重要价值。

8/10-feat(rlt): migrate OpenPI to JAX-aligned PyTorch Pi0.5 (#1435)（c704688）
- **评分**：8/10
- **一句话总结**：将 OpenPI 迁移至与 JAX 对齐的 PyTorch Pi0.5 模型实现。
- **链接**：https://github.com/RLinf/RLinf/commit/c704688c9fafe7dfd7267011c3a241adcd8cd203
- **变更规模**：+740 -103
- **提交者**：上坂 茅羽耶
- **解决的问题**：原 OpenPI 基于旧版 Pi0 实现，与 JAX 生态的模型权重和训练流程不对齐，导致用户在跨框架迁移时遇到困难。
- **产品启示**：通过对齐 JAX 生态的 Pi0.5，降低了用户在 PyTorch 与 JAX 之间的迁移成本，同时提升了模型性能上限，有助于吸引更多 VLA 研究者将 RLinf 作为训练与评估的统一平台。

7/10-feat(rlt): add RLT TD3 MLP policy in ManiSkill (#1465)（13e5b65）
- **评分**：7/10
- **一句话总结**：在 ManiSkill 环境中新增 RLT TD3 MLP 策略支持，扩展了算法库的覆盖范围。
- **链接**：https://github.com/RLinf/RLinf/commit/13e5b652349cc0715267a560004af23e2925489c
- **变更规模**：+1015 -10
- **提交者**：上坂 茅羽耶
- **解决的问题**：此前 ManiSkill 示例仅支持 AC MLP 策略，缺乏 TD3 等 off-policy 算法的参考实现，限制了用户在连续控制任务上的算法选择。
- **产品启示**：通过提供 TD3 策略的完整配置与文档，降低了用户在 ManiSkill 上尝试不同 RL 算法的门槛，有助于吸引更多研究者基于该平台进行算法对比与复现，增强生态吸引力。

7/10-feat(musa): add e2e tests, install and docker support (#1464)（f636e93）
- **评分**：7/10
- **一句话总结**：新增对 MUSA 硬件加速器的端到端测试、安装脚本及 Docker 镜像支持。
- **链接**：https://github.com/RLinf/RLinf/commit/f636e9322b84fae174fbd984e7e5e9f967e25cae
- **变更规模**：+1357 -115
- **提交者**：Andy Lin
- **解决的问题**：MUSA 作为国产 GPU 加速器，此前缺乏官方支持，导致使用该硬件的用户无法顺利部署 RLinf。
- **产品启示**：主动适配国产硬件生态，体现了项目对多元化算力平台的前瞻性布局，有助于扩大用户基础并降低对单一 GPU 厂商的依赖，提升在特定区域市场的竞争力。

7/10-feat: add smooth intervention function (#1432)（3feaaa3）
- **评分**：7/10
- **一句话总结**：新增平滑干预功能，用于真实世界 DAgger 数据采集过程中的人机交互控制。
- **链接**：https://github.com/RLinf/RLinf/commit/3feaaa35ef4e53396c2ec34f751bd52a9c3f0281
- **变更规模**：+853 -156
- **提交者**：tiny
- **解决的问题**：在真实机器人（双 Franka）上进行 DAgger 数据采集时，操作者直接干预可能导致机器人动作突变，影响数据质量与安全性。
- **产品启示**：平滑干预机制显著提升了真实世界数据采集的实用性和安全性，是具身智能从仿真走向实际部署的关键一环，有助于增强工业与科研用户对真实世界实验的信心。

### ⚡️ 性能/架构优化

8/10-refactor(workers): split EmbodiedFSDPActor into its own module (#1478)（9ad4439）
- **评分**：8/10
- **一句话总结**：将 EmbodiedFSDPActor 从 workers 模块中拆分至独立模块，完成核心架构重构。
- **链接**：https://github.com/RLinf/RLinf/commit/9ad44393d15b0e93461d7415591110678ae17ef6
- **变更规模**：+879 -778
- **提交者**：石乐同
- **解决的问题**：EmbodiedFSDPActor 作为分布式训练的核心组件，原先与其他 worker 逻辑耦合，导致模块职责不清、扩展困难，且影响 CI 测试效率。
- **产品启示**：模块化拆分提升了代码可维护性与可测试性，为后续独立优化 actor 的显存管理与通信策略奠定基础，是保障分布式训练长期稳定性的关键架构投资。

### 🐛 Bug修复 / 其他

6/10-fix(scheduler): map CUDA devices to EGL indices in the accelerator (#1458)（2af0a8b）
- **评分**：6/10
- **一句话总结**：修复调度器中 CUDA 设备与 EGL 索引的映射问题。
- **链接**：https://github.com/RLinf/RLinf/commit/2af0a8b5049704e904fdcbea111a3904966d56e1
- **变更规模**：+658 -3
- **提交者**：Yichen Wang
- **解决的问题**：在多 GPU 环境下，CUDA 设备编号与 EGL 渲染设备的索引可能不一致，导致仿真环境（如 robosuite）在特定 GPU 上无法正确初始化或渲染异常。
- **产品启示**：该修复提升了多 GPU 场景下仿真与渲染的可靠性，对依赖视觉输入的机器人学习任务至关重要，减少了用户在复杂硬件环境下的配置成本。

---

