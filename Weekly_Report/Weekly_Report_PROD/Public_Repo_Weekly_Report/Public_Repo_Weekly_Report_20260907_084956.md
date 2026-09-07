# 具身智能周报 (2026年09月07日 08:49:56)

## 行业风向总览

## 具身智能行业风向总结（本周）

**技术焦点**：仿真引擎与训练框架双线并进。MuJoCo聚焦求解器数值优化（锥贡献折叠进Hessian）与碰撞检测精度修复（多接触边缘归属错误），持续巩固物理仿真基础设施；Warp则呈现从“重性能”向“正确性加固”的转向，密集修复整数除法语义、负归约轴、无效索引等边界问题，并新增`delaunay_edge_flip`几何原语，向几何处理平台延伸。

**合成数据动态**：MuJoCo修复`patch_radius=0`时地形采样坍缩问题，直接保障程序化生成地形的多样性与有效性，对依赖仿真数据训练的策略泛化至关重要。RLinf修复混合批次数据块对齐问题，增强真实世界+仿真数据混合训练管道的可靠性。

**产品经理关注信号**：① RLinf新增多智能体FSDP支持，标志分布式训练能力向多智能体场景（如SearchR1 agentic任务）扩展，工程门槛显著降低；② MuJoCo将mujoco_warp改为直接从GitHub导入，降低维护成本并加速Warp后端新特性（BVH加速、box-box碰撞）触达用户；③ 异步rollout权重同步的安全重叠优化，直接提升长周期真实世界数据采集场景的GPU利用率与吞吐。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 1 条
- 高价值提交（≥6分）: 1 条
- 代码更新规模: +22 / -4 行
- 主要贡献者: hadelan

## 🧭 趋势点评

本周更新延续了仓库在**仿真精度与稳定性**上的长期投入，同时体现了对**地形生成可靠性**的持续关注。从6个月基线看，项目在传感器精度、指标系统、渲染可视化等方向持续迭代，而本周的修复聚焦于地形采样崩溃问题，属于对仿真环境基础能力的加固。该提交虽为单一Bug修复，但直接关系到地形生成的正确性与训练数据的有效性，与仓库“强化仿真精度和训练稳定性”的核心价值一致。整体来看，本周更新未偏离长期趋势，仍处于稳步迭代、持续修复关键缺陷的节奏中。

## 🔍 关键更新解析

### 🚀 新功能/特性

（本周无高价值新功能提交）

### ⚡️ 性能/架构优化

（本周无高价值性能/架构优化提交）

### 🐛 Bug修复 / 其他

6/10-Fix flat patch sampling collapsing to the center when patch_radius=0 (#1173)（8ee51fb）
- **评分**：6/10
- **一句话总结**：修复了当 `patch_radius=0` 时平面补丁采样坍缩到中心点的问题，确保地形生成在边界条件下的正确性。
- **链接**：https://github.com/mujocolab/mjlab/commit/8ee51fbcf806a7419189f706d9e394cbeb7790fa
- **变更规模**：+22 -4（涉及4个文件）
- **提交者**：hadelan
- **解决的问题**：当 `patch_radius` 参数设为0时，平面补丁采样逻辑会将所有采样点坍缩到地形中心，导致生成的地形失去随机性与多样性，影响仿真环境的有效性与训练数据的质量。
- **产品启示**：边界条件（如参数为0）往往是仿真系统中最易被忽视的脆弱点。此类修复虽小，但直接保障了地形生成模块在极端配置下的鲁棒性，避免用户因参数设置不当而获得无效仿真环境。建议后续在参数校验层增加对边界值的显式处理与告警，从源头减少此类问题的发生。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 38 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +14891 / -8860 行
- 主要贡献者: Yuval Tassa, Haroon Qureshi, Kyle Bayes

## 🧭 趋势点评

本周更新延续了该仓库在求解器数值稳定性、碰撞检测精度与MJX生态扩展上的长期主线。`10eeb82`将锥贡献折叠进Hessian的优化策略，与过去6个月中PGS动量加速、CG线搜索重构等求解器算法级创新一脉相承，体现了对数值效率与精度平衡的持续追求；`bbb71a2`修复多接触边缘落在错误面的问题，呼应了此前GJK爬山、EPA内存复用等碰撞检测的深度打磨方向。同时，`34f099c`从GitHub导入mujoco_warp、`26d2bf2`启用MJX对Python 3.15的支持，延续了仓库在MJX/Warp集成与依赖更新上的既定路线，进一步巩固了MuJoCo作为机器人仿真与强化学习基础设施的生态位。整体来看，本周提交在核心引擎稳健性与外部生态扩展上双线并进，未偏离仓库的长期演进轨迹。

## 🔍 关键更新解析

### 🚀 新功能/特性

8/10-Import google-deepmind/mujoco_warp from GitHub.（34f099c）
- **评分**：8/10
- **一句话总结**：将mujoco_warp作为第三方依赖从GitHub导入仓库，大幅扩展MJX的Warp后端能力。
- **链接**：https://github.com/google-deepmind/mujoco/commit/34f099c7b86f4c527f5b48c1215d4921a18f1cf2
- **变更规模**：+5285 -4894
- **提交者**：Google DeepMind
- **解决的问题**：此前MJX的Warp集成依赖内部维护的副本，难以同步上游更新；通过直接从GitHub导入mujoco_warp，解决了代码同步滞后与维护成本高的问题，同时引入了更完整的碰撞检测（collision_convex、collision_core）与BVH加速结构。
- **产品启示**：对依赖上游开源项目的模块采用“直接导入”策略，可显著降低双份维护成本，并让用户更快获得Warp后端的新特性（如大规模场景支持、box-box碰撞等）。对依赖MJX进行大规模并行仿真的研究团队而言，这意味着更及时的功能更新与更低的版本漂移风险。

7/10-Publish passive flex contact as a metric rank-1 class（8489cf1）
- **评分**：7/10
- **一句话总结**：将被动flex接触发布为metric rank-1类，使导数计算与内省工具链可识别该约束类型。
- **链接**：https://github.com/google-deepmind/mujoco/commit/8489cf1962d976c2f9da3b49adf2d8d9f63bb6da
- **变更规模**：+257 -214
- **提交者**：Alessio
- **解决的问题**：此前被动flex接触在mjxmacro.h与engine_derivative.c中缺乏对应的rank-1类声明，导致导数计算、Python内省（introspect/structs.py）及文档生成（references.h）无法正确处理该约束类型，造成功能缺失与文档不一致。
- **产品启示**：将新约束类型纳入统一的“metric rank-1”分类体系，意味着用户可通过Python内省API直接查询被动flex接触的属性，并在基于导数的优化（如系统辨识、轨迹优化）中正确利用该约束。这对使用flex进行软体机器人或可变形物体仿真的用户尤为有价值，降低了自定义约束接入上层工具链的复杂度。

6/10-Enable MJX for Python 3.15 and update JAX dependencies.（26d2bf2）
- **评分**：6/10
- **一句话总结**：MJX启用Python 3.15支持并同步更新JAX依赖。
- **链接**：https://github.com/google-deepmind/mujoco/commit/26d2bf2c4d7ecf053cb46280d4845bc557911e53
- **变更规模**：+212 -118
- **提交者**：Michael Moss
- **解决的问题**：Python 3.15发布后，MJX的依赖约束（requirements.txt）尚未适配，导致新版本Python用户无法安装或运行MJX；本次更新调整了cuda_requirements与requirements中的版本上限，确保MJX在Python 3.15环境下的兼容性。
- **产品启示**：对依赖快速迭代的Python生态保持同步是开源仿真库用户留存的关键。此更新降低了MJX在新Python环境中的安装门槛，有助于吸引使用最新Python工具链的强化学习开发者，避免因环境不兼容而流失用户。

### ⚡️ 性能/架构优化

9/10-Fold cone contributions into the Hessian when full factorization is faster than multiple rank-1 updates.（10eeb82）
- **评分**：9/10
- **一句话总结**：在全因子分解快于多次rank-1更新时，将锥贡献直接折叠进Hessian矩阵，显著提升求解器性能。
- **链接**：https://github.com/google-deepmind/mujoco/commit/10eeb8289598421cbca0b39459652ed57ec3d2e6
- **变更规模**：+445 -4
- **提交者**：Yuval Tassa
- **解决的问题**：在求解带锥约束（cone constraint）的优化问题时，传统方法通过多次rank-1更新将锥贡献叠加到Hessian上；当锥数量较多时，rank-1更新的累积成本超过直接对完整Hessian做一次因子分解的成本。本次提交通过运行时判断选择更优路径，将锥贡献直接折叠进Hessian后做全因子分解，避免了重复的rank-1更新开销。
- **产品启示**：该优化直接降低了含大量锥约束场景（如多接触点、摩擦锥、flex接触）的求解耗时。对机器人运动规划与仿真中常见的密集接触场景，用户可感知到更快的仿真速度，尤其是在大规模批量仿真（如强化学习训练数据生成）中，累积的加速效果将显著缩短数据采集时间。新增的cone_benchmark_test也为后续性能回归提供了量化基准。

### 🐛 Bug修复 / 其他

8/10-Fix issue in multiccd where edge contact can be on the wrong face.（bbb71a2）
- **评分**：8/10
- **一句话总结**：修复多接触（multiccd）中边缘接触可能被分配到错误面的问题。
- **链接**：https://github.com/google-deepmind/mujoco/commit/bbb71a28a4d16db0d42f98da84e9e56ff663df5f
- **变更规模**：+70 -3
- **提交者**：Kyle Bayes
- **解决的问题**：在连续碰撞检测（CCD）的多接触生成过程中，当一条边同时邻近多个面时，原有逻辑可能将接触点错误地归属到非最优面上，导致接触法线方向错误、产生虚假的穿透或分离力，进而影响仿真稳定性。
- **产品启示**：接触点归属错误会直接导致物理仿真中的“抖动”或“弹跳”伪影，尤其在薄壁结构或尖锐几何体的碰撞中更为明显。此修复提升了多接触场景下接触几何的准确性，对使用CCD进行高速碰撞或薄物体仿真的用户（如机械臂抓取薄板、投掷物体）可带来更平滑、更可信的物理表现。

---

### [isaac-sim/IsaacLab] 本周无高价值更新（≥6分）。

#### 📊 提交分析
- 本周总提交: 1 条
- 高价值提交: 0 条
- 代码更新规模: +1 / -1 行
- 主要贡献者: Kelly Guo

#### 🧭 趋势点评
本周共有 1 条常规提交，主要涉及代码维护与小幅优化，无值得重点关注的功能或性能更新。


---

7/10-Fix uninitialized Y pattern in the discrete dual projection.（6ea1fc1）
- **评分**：7/10
- **一句话总结**：修复离散对偶投影中Y模式未初始化的问题。
- **链接**：https://github.com/google-deepmind/mujoco/commit/6ea1fc1ce375038a0145acc7a069f2920b8507d2
- **变更规模**：+81 -3
- **提交者**：Yuval Tassa
- **解决的问题**：在离散约束求解的dual projection步骤中，Y模式（pattern）数组未被正确初始化，可能导致求解器在迭代过程中读取未定义的内存值，产生不确定的求解结果或数值噪声，影响离散积分器（integrator="discrete"）的稳定性与可复现性。
- **产品启示**：未初始化内存是数值仿真中隐蔽的不确定源，可能导致同一场景在不同平台或运行次数下产生微小差异。此修复提升了离散求解路径的数值确定性，对依赖精确可复现仿真的研究与评测场景（如算法对比、回归测试）尤为重要。

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 35 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +7932 / -3515 行
- 主要贡献者: Eric Shi, Christopher Crouzet, Aamir Ahmed

## 🧭 趋势点评

本周更新延续了 NVIDIA/warp 在性能优化与功能扩展并重的长期主线，同时呈现出向“正确性加固”倾斜的短期特征。性能侧，运行时向下取整除法的优化（3735413）与语义修复（7784b3e）形成“优化+纠错”的配套组合，呼应了仓库在 2026-09 期间对整数运算精度的持续关注；功能侧，多维查询块（5cd53d5）与 `delaunay_edge_flip`（570534f）分别拓展了 BVH 查询的灵活性和几何处理能力，与前期新增的确定性原子模式、tile_scatter_masked 等特性一脉相承。值得注意的是，本周 Bug 修复类提交占比显著提升，且均围绕输入验证与边界条件处理（负归约轴、无效 OpenGL 索引、array_inner 形状校验），这与仓库长期“重性能、轻防御”的风格形成一定偏离，反映出项目在功能面扩大后开始系统性补齐输入健壮性短板——这一转向与 2026-08 以来测试套件收紧、文档标准化的趋势一致，可视为项目从快速迭代期进入成熟稳定期的信号。

## 🔍 关键更新解析

### 🚀 新功能/特性

9/10-Add warp.geometry.delaunay_edge_flip [GH-1797]（570534f）
- **评分**：9/10
- **一句话总结**：新增 `warp.geometry.delaunay_edge_flip` 几何核心功能，用于三角网格的 Delaunay 边翻转操作。
- **链接**：https://github.com/NVIDIA/warp/commit/570534f2410b993f9b71e092d8598b50c25082d1
- **变更规模**：+1334 -105（涉及 `warp/__init__.py`、`docs/api_reference/warp.rst`、`docs/api_reference/warp_geometry.rst`、`docs/index.rst` 及 changelog）
- **提交者**：Alec Jacobson
- **解决的问题**：为网格重网格化、质量改善和参数化等几何处理流程提供原生的 Delaunay 边翻转原语，填补了 Warp 在网格拓扑局部优化方面的空白。
- **产品启示**：该功能直接服务于物理仿真中的自适应网格重构和几何建模工作流，使 Warp 从纯计算库进一步向几何处理平台延伸，降低了用户对接外部网格库的集成成本。

8/10-Support multidimensional query blocks [GH-1864]（5cd53d5）
- **评分**：8/10
- **一句话总结**：为 BVH 和网格查询新增多维查询块支持，允许用户以多维 block 维度发起查询，提升查询调度的灵活性。
- **链接**：https://github.com/NVIDIA/warp/commit/5cd53d5e38b59fe950ca0a54c33ddc02b357d399
- **变更规模**：+13 -2（涉及 `warp/native/bvh.h`、`warp/native/mesh.h` 及 changelog）
- **提交者**：Eric Shi
- **解决的问题**：此前查询块仅支持一维布局，在多维 GPU 线程组织场景下需要手动展平索引，增加了内核编写复杂度并可能损失调度效率。该提交让查询块维度与启动配置自然对齐。
- **产品启示**：对依赖 BVH 射线查询的仿真与渲染工作负载，多维查询块可减少索引换算开销并改善占用率，尤其利好体素化、粒子-网格交互等三维规则访问模式。

### ⚡️ 性能/架构优化

7/10-Optimize runtime signed floor division [GH-1918]（3735413）
- **评分**：7/10
- **一句话总结**：优化运行时带符号向下取整除法的实现，提升内核中整数除法的吞吐。
- **链接**：https://github.com/NVIDIA/warp/commit/37354134eb630401940a8274de28850e1ed9a6b3
- **变更规模**：+157 -0（涉及 `warp/native/builtin.h` 及新增 ASV 基准 `asv/benchmarks/floordiv.py`）
- **提交者**：Eric Shi
- **解决的问题**：带符号向下取整除法在 CPU 路径上通常需要额外的符号修正分支，导致比无符号除法或截断除法更慢。该提交通过更优的位运算序列减少分支开销。
- **产品启示**：索引计算、归约逻辑和几何哈希中大量使用整数除法，此优化可无感提升所有 CPU 后端内核的算术吞吐，并配套 ASV 基准以量化收益、防止回归。

### 🐛 Bug修复 / 其他

8/10-Floor integer division toward negative infinity [GH-1918]（7784b3e）
- **评分**：8/10
- **一句话总结**：修复整数除法在负数场景下未按向下取整（floor）语义执行的问题。
- **链接**：https://github.com/NVIDIA/warp/commit/7784b3e365f0d09abd4d20bacee1ba7f86727696
- **变更规模**：+62 -1（涉及 `warp/native/builtin.h`、`warp/tests/test_arithmetic.py` 及 changelog）
- **提交者**：Aamir Ahmed
- **解决的问题**：C/C++ 中整数除法默认向零截断，与 Python 的 floor 语义不一致。此前 Warp 的运行时除法在负数场景下可能产生与 Python 端不一致的结果，导致跨语言逻辑偏差。
- **产品启示**：该修复与 3735413 配套，先纠语义再提性能，确保 Warp 在 CPU 与 GPU 后端、Python 与原生层之间保持一致的除法行为，对依赖索引映射和模运算的算法正确性至关重要。

7/10-Handle negative reduction axes [GH-1893]（f2e497e）
- **评分**：7/10
- **一句话总结**：修复归约操作对负轴（如 `axis=-1`）的处理，使其与 NumPy 风格语义对齐。
- **链接**：https://github.com/NVIDIA/warp/commit/f2e497e9d82c1049d5bc399671edf4582dfa2e83
- **变更规模**：+135 -12（涉及 `warp/_src/utils.py`、`warp/tests/test_apic.py`、`warp/tests/test_array_reduce.py` 及 changelog）
- **提交者**：Eric Shi
- **解决的问题**：此前负归约轴可能被错误解释或直接拒绝，与 Python 生态中通用的负索引约定不一致，导致跨框架代码迁移时出现隐蔽错误。
- **产品启示**：负轴支持是数组库的基本语义约定，此修复提升了 Warp 与 NumPy/PyTorch 生态的互操作性，降低了用户从既有 Python 代码迁移到 Warp 的认知负担。

---

6/10-Validate array_inner input shapes [GH-1903]（62730fe）
- **评分**：6/10
- **一句话总结**：为 `array_inner` 工具函数增加输入形状验证，提前捕获维度不匹配错误。
- **链接**：https://github.com/NVIDIA/warp/commit/62730fe6a295e3edcaa5962853c800276e3d1e04
- **变更规模**：+33 -17（涉及 `warp/_src/utils.py`、`warp/tests/test_utils.py` 及 changelog）
- **提交者**：Eric Shi
- **解决的问题**：此前 `array_inner` 在输入形状不兼容时可能产生隐晦的底层错误或未定义行为，增加了用户排查成本。
- **产品启示**：输入验证的增强降低了 API 误用的可能性，对库的工程化成熟度有正向意义，尤其惠及自动化批处理脚本中的数组拼接与重组操作。

6/10-Reject invalid OpenGL mesh indices [GH-1899]（305b908）
- **评分**：6/10
- **一句话总结**：在 OpenGL 渲染路径中拒绝越界或无效的网格索引，避免渲染异常或崩溃。
- **链接**：https://github.com/NVIDIA/warp/commit/305b90811109f6ade9577496c96773d7f80ac6a4
- **变更规模**：+198 -14（涉及 `warp/_src/render/render_opengl.py`、`warp/tests/test_render_opengl.py`、`warp/tests/unittest_suites.py` 及 changelog）
- **提交者**：Eric Shi
- **解决的问题**：无效网格索引可能导致 OpenGL 缓冲区越界访问，产生不可预测的渲染结果甚至驱动崩溃。该提交在进入渲染管线前主动校验索引合法性。
- **产品启示**：对依赖 Warp 进行实时可视化的仿真工具链，此修复增强了渲染健壮性，避免因网格数据异常导致的整个应用崩溃，提升了用户体验和调试效率。

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 10 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +2161 / -262 行
- 主要贡献者: Rusty Raven, panhe1818, Alune233

## 🧭 趋势点评

本周更新高度契合仓库长期演进主线：以多智能体 FSDP（MA-FSDP）支持为标志的分布式训练能力扩展，延续了 2026-09 以来对大规模多智能体场景的布局；异步 rollout 权重同步的安全重叠优化（d18786e）则呼应了仓库在权重同步机制上的持续重构与性能调优脉络（如 28eb0d4、534ed59、9689e48 等历史提交）。与此同时，多个 Bug 修复（调度器继承环境重发、critic 指标报告、PPO actor 指标归一化、混合批次对齐）聚焦于训练正确性与数据路径稳定性，体现了项目在快速迭代新功能的同时，对核心算法与调度逻辑的精度维护投入不减。整体来看，本周提交呈现“功能突破 + 正确性加固”双轮驱动格局，与仓库从仿真到真实世界、从单智能体到多智能体的完整 RL 框架建设方向保持一致。

## 🔍 关键更新解析

### 🚀 新功能/特性

9/10-feat(agent): add multi-agent FSDP (MA-FSDP) actor support (#1400)（3e90455）
- **评分**：9/10
- **一句话总结**：新增多智能体 FSDP（MA-FSDP）actor 支持，扩展大规模多智能体训练能力。
- **链接**：https://github.com/RLinf/RLinf/commit/3e904557263d8a09b0c18f9562e25531241f5e02
- **变更规模**：+1215 -147，涉及 CI 工作流、中英文文档、SearchR1 示例配置等
- **提交者**：SII-Yongkang Zhou
- **解决的问题**：此前 FSDP 训练主要面向单智能体或独立模型场景，多智能体强化学习（如 SearchR1 等 agentic 任务）缺乏统一的 FSDP 分片与同步机制，导致大规模多智能体训练时显存利用率和扩展性受限。
- **产品启示**：MA-FSDP 的落地意味着 RLinf 正式具备多智能体场景下的分布式训练能力，为 SearchR1 等 agentic 工作负载提供了与单智能体一致的 FSDP 体验，降低了用户在多智能体大规模训练中的工程门槛，是平台能力边界的重要扩展。

### ⚡️ 性能/架构优化

8/10-fix(embodied): safely overlap rollout weight sync in async runners (#1456)（d18786e）
- **评分**：8/10
- **一句话总结**：在异步 runner 中安全地重叠 rollout 与权重同步，减少训练等待时间。
- **链接**：https://github.com/RLinf/RLinf/commit/d18786ec4caabb5e1fe8bad3a7768fb174674e23
- **变更规模**：+619 -64，涉及 CI 工作流、中英文权重同步文档、配置文件及异步 runner 核心逻辑
- **提交者**：Yichen Wang
- **解决的问题**：在异步 embodied 训练中，rollout 阶段与权重同步阶段若串行执行，会造成 actor 侧空闲等待，降低整体训练吞吐；若直接并行则可能产生权重版本不一致或同步竞争等正确性问题。
- **产品启示**：该优化直接提升异步训练场景下的 GPU 利用率和端到端吞吐，对真实世界机器人或仿真环境中的长 rollout 任务尤为关键。同时配套更新了中英文 weight_syncer 文档，降低了用户理解和配置异步权重同步的门槛。

### 🐛 Bug修复 / 其他

7/10-fix(algorithms): normalize PPO actor metrics by mask width (#1475)（56e75bf）
- **评分**：7/10
- **一句话总结**：修复 PPO actor 指标未按 mask 宽度归一化的问题。
- **链接**：https://github.com/RLinf/RLinf/commit/56e75bf21297ddf051087f52cf6c9c726887cfbf
- **变更规模**：+40 -30，涉及 PPO actor 损失与指标计算逻辑
- **提交者**：Rusty Raven
- **解决的问题**：在变长轨迹或 padding 场景下，actor 的统计指标（如熵、KL 散度等）未按有效 token 数（mask 宽度）归一化，导致指标数值被 padding 稀释，无法反映真实策略行为。
- **产品启示**：指标归一化修复提升了训练监控数据的准确性，尤其在混合长度批次和真实世界数据场景下，用户可据此更可靠地评估策略更新质量，辅助算法调参决策。

6/10-fix(scheduler): avoid resending inherited env (#1532)（dc9b87c）
- **评分**：6/10
- **一句话总结**：修复调度器在集群配置中重复发送继承环境变量的问题。
- **链接**：https://github.com/RLinf/RLinf/commit/dc9b87cc49334c7516487ead68ebeb060fd7c090
- **变更规模**：+35 -1，涉及集群调度器核心逻辑及对应单元测试
- **提交者**：Alune233
- **解决的问题**：当集群配置中存在继承的环境变量时，调度器可能将其重复下发至 worker，导致环境变量冗余传递，极端情况下可能引发配置冲突或启动异常。
- **产品启示**：该修复提升了调度器在复杂集群配置下的稳健性，避免因环境变量重复注入导致的隐性启动故障，对大规模集群部署场景下的用户体验有直接改善。

6/10-fix(algorithms): report a live critic value_clip_ratio (#1530)（68feab9）
- **评分**：6/10
- **一句话总结**：修复 critic 的 value_clip_ratio 指标报告，使其反映实时值而非历史累积。
- **链接**：https://github.com/RLinf/RLinf/commit/68feab9f0a50764d75e42f12f837dbbb74775d15
- **变更规模**：+158 -2，涉及 PPO critic 损失实现及对应单元测试
- **提交者**：Rusty Raven
- **解决的问题**：此前 value_clip_ratio 指标可能基于过期或错误的统计口径上报，导致用户在训练监控中无法准确判断 critic 值函数裁剪频率，影响超参调优判断。
- **产品启示**：训练指标的可信度直接影响用户对模型收敛状态的判断。该修复让 value_clip_ratio 如实反映当前训练步的裁剪情况，有助于用户更精准地监控 PPO 训练的稳定性。

6/10-fix(data): align mixed batch chunks (#1501)（93a9a1c）
- **评分**：6/10
- **一句话总结**：修复混合批次中不同数据块未对齐的问题。
- **链接**：https://github.com/RLinf/RLinf/commit/93a9a1ca1b2e13e765dca6c1deab1b0c6823ef7b
- **变更规模**：+91 -2，涉及 embodied 轨迹构建器、嵌套字典处理工具及单元测试
- **提交者**：wang ke
- **解决的问题**：当混合批次包含不同来源或不同形态的数据块时，嵌套字典处理过程中可能出现维度或索引未对齐，导致训练数据错位或形状不匹配。
- **产品启示**：数据管道的正确性是训练稳定性的基石。该修复增强了混合数据场景下的鲁棒性，对多模态、多来源数据混合训练（如真实世界 + 仿真数据）的可靠性有直接保障作用。

---

