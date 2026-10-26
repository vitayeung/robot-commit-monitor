# 具身智能周报 (2026年10月26日 09:10:18)

- 统计窗口: 2026-10-19 09:04:07 +0800 至 2026-10-26 09:10:18 +0800（左闭右开）

## 行业风向总览

本周具身智能行业风向呈现“仿真内核深挖+训练栈扩张”双线并进。技术焦点上，MuJoCo 以稀疏/带状 Cholesky、稀疏矩阵平方等线性代数内核实现 1.2–2 倍加速，并集中修复 float32 椭圆锥线搜索、wrap_circle 等数值稳定性问题；Warp 将 ASV 基准挂载 main 分支形成性能门禁，并优化 Adjoint 树视图的 wp.static 替换以加速自动微分代码生成；IsaacLab 推进 3.0 克隆命名空间与场景绑定统一，渲染/可视化测试解耦任务环境，CI 预热 Warp 内核缩短反馈周期。合成数据方面，本周无直接合成数据管线提交，但 MuJoCo flex 被动接触、薄片单元剔除与重心坐标加权等语义完善，以及 Warp APIC 网格序列化扩展，实质提升了软体与网格场景的仿真保真度，为合成数据生成提供更可靠的物理底座。产品经理需关注：RLinf 新增 OpenPI 全量/梯度分片与 Orbbec RGB-D 支持，真机栈与显存适配能力增强；rollout 截止时间返回部分批次改变下游消费语义，需明确批次不完整约定；Warp 弃用 Python 3.10，升级前需核对环境兼容性。整体看，行业正从单点性能优化转向“数值正确性+多后端一致性+训练容错”的系统化工程阶段。

---

## 各仓库详细分析

### [mujocolab/mjlab] 本周无新提交。


---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 126 条
- 高价值提交（≥6分）: 13 条
- 代码更新规模: +70358 / -6648 行
- 主要贡献者: Yuval Tassa, Alessio Quaglino, Haroon Qureshi

## 🧭 趋势点评
本周更新高度延续了仓库“核心数值内核深度优化 + 平台化扩展”的双主线趋势，并进一步向 float32 精度稳定性与柔性体（flex）语义完善倾斜。性能侧，稀疏/带状 Cholesky、稀疏矩阵平方、mju_sqrMatTD 等线性代数内核继续获得 1.2–2 倍级加速，与 2026-10 的密集数值加速节奏一致；同时椭圆锥线搜索浮点抵消、wrap_circle 数值不稳定等修复，呼应了基线中“激进优化需数值一致性兜底”的风险判断。功能侧，flex 相关提交（被动接触、薄片单元剔除、重心坐标加权、雅可比丢项修复、配置组合限制）集中落地，显示软体建模正从性能优化转向语义正确性与表达能力补全，略微偏离此前以求解器/碰撞为主的优化重心。MJX/MuJoCo Warp 侧同步修复胶囊接触与 flex 接触加权，体现 C 引擎与 Warp 后端并行演进的耦合加深。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-Enable passive (metric-carried) contact (`<contact passive="true"/>`) for interpolated flexes (`dof="trilinear"` and `dof="quadratic"`, both volumetric and shell, with `dim >= 2`):（115907e）
  - 评分：7/10
  - 一句话总结：为插值 flex（三线性/二次、体/壳、dim≥2）启用度量承载的被动接触。
  - 链接：https://github.com/google-deepmind/mujoco/commit/115907e6d9ad0e0717527b1f63875a5961fe3b0a
  - 变更规模：+528 -26
  - 提交者：Alessio Quaglino
  - 解决的问题：此前插值 flex 缺乏被动接触支持，限制了软体与环境的真实交互建模。
  - 产品启示：扩展 flex 接触表达能力，利好软体抓取、穿戴等场景，同时需关注被动接触对求解器收敛与性能的额外开销。

7/10-MuJoCo: prune sliver cells as empty and extrapolate vertex coordinates from nearest active cell（1a2231b）
  - 评分：7/10
  - 一句话总结：将薄片单元视为空单元剔除，并从最近活跃单元外推顶点坐标。
  - 链接：https://github.com/google-deepmind/mujoco/commit/1a2231b7c0148777af3621ca759939eee3e7a6bc
  - 变更规模：+725 -91
  - 提交者：Alessio Quaglino
  - 解决的问题：退化薄片单元导致数值病态与顶点坐标异常，影响 flex 仿真稳定性。
  - 产品启示：提升退化网格鲁棒性，利好低质量网格导入场景，但外推策略可能改变接触结果，需数值一致性测试兜底。

7/10-Weight flex element contacts by barycentric coordinates.（f9f3ee6）
  - 评分：7/10
  - 一句话总结：按重心坐标对 flex 单元接触进行加权。
  - 链接：https://github.com/google-deepmind/mujoco/commit/f9f3ee653eb6468186326cfc7f5b556b001faebc
  - 变更规模：+452 -215
  - 提交者：Google DeepMind
  - 解决的问题：此前 flex 接触未按重心坐标加权，接触力分布不够物理准确。
  - 产品启示：提升软体接触力分布的真实性，同步覆盖 MJWarp 后端，体现双后端语义一致性投入。

6/10-Disallow 1D flex elasticity under implicit/implicitfast and disallow flex edge stiffness/damping under discrete.（c0e6b15）
  - 评分：6/10
  - 一句话总结：限制 flex 在隐式积分与离散模式下的非法弹性/边刚度配置组合。
  - 链接：https://github.com/google-deepmind/mujoco/commit/c0e6b15fdf2ad3c5ef0425580845fe2d96b272e6
  - 变更规模：+151 -66
  - 提交者：Alessio Quaglino
  - 解决的问题：避免 1D flex 弹性在 implicit/implicitfast 下、以及 flex 边刚度/阻尼在 discrete 下产生未定义或不稳定的物理行为。
  - 产品启示：通过显式禁止非法配置组合，降低用户误用导致的数值异常，提升软体仿真的可预期性，但需在文档与迁移指引中明确告知下游。

### ⚡️ 性能/架构优化
9/10-Optimize sparse Cholesky factor, solve, and rank-1 updates by 1.2-1.6x（b7fcf96）
  - 评分：9/10
  - 一句话总结：稀疏 Cholesky 分解、求解与秩一更新提速 1.2–1.6 倍。
  - 链接：https://github.com/google-deepmind/mujoco/commit/b7fcf964e9ae57e4d45e7add431a500933ec5223
  - 变更规模：+687 -207
  - 提交者：Yuval Tassa
  - 解决的问题：稀疏 Cholesky 是约束求解核心路径，此前存在性能瓶颈。
  - 产品启示：直接提升大规模仿真与 RL 训练吞吐，配套基准测试为回归防护提供基础。

8/10-Speed up sparse matrix squaring ~2x（e3c0953）
  - 评分：8/10
  - 一句话总结：稀疏矩阵平方运算约 2 倍加速。
  - 链接：https://github.com/google-deepmind/mujoco/commit/e3c0953f9f2b5a00a30d01b58f715f5e36d9a07d
  - 变更规模：+261 -94
  - 提交者：Yuval Tassa
  - 解决的问题：稀疏矩阵平方在动力学计算中频繁调用，此前效率不足。
  - 产品启示：与 Cholesky 优化形成数值内核组合提速，惠及整体仿真步进性能。

8/10-Optimize banded Cholesky and matrix routines.（75ba33d）
  - 评分：8/10
  - 一句话总结：优化带状 Cholesky 与相关矩阵例程。
  - 链接：https://github.com/google-deepmind/mujoco/commit/75ba33d552632520de6b66d8cc4f30163fe65d96
  - 变更规模：+278 -94
  - 提交者：Yuval Tassa
  - 解决的问题：带状 Cholesky 路径缺乏针对性优化，影响带状结构系统的求解效率。
  - 产品启示：补齐稀疏与带状两条线性代数路径的优化覆盖，提升不同模型结构下的性能一致性。

7/10-Unify and optimize `mju_sqrMatTD_impl` and add dense benchmarks.（2360605）
  - 评分：7/10
  - 一句话总结：统一并优化 mju_sqrMatTD_impl，新增稠密基准测试。
  - 链接：https://github.com/google-deepmind/mujoco/commit/23606050dada504a7180c1bd41964b55ccc42f7a
  - 变更规模：+109 -85
  - 提交者：Yuval Tassa
  - 解决的问题：实现分散且缺乏稠密场景基准，难以评估与防回归。
  - 产品启示：统一实现降低维护成本，基准补充强化性能回归防护。

6/10-Make improvements in mjc_advanceGeomPair.（d479606）
  - 评分：6/10
  - 一句话总结：改进连续碰撞几何对推进逻辑。
  - 链接：https://github.com/google-deepmind/mujoco/commit/d4796060d700d4a78de5f1f264b2ecd7b7021956
  - 变更规模：+118 -23
  - 提交者：Kyle Bayes
  - 解决的问题：连续碰撞几何对推进存在效率与正确性改进空间。
  - 产品启示：碰撞管线持续打磨，利好高速运动场景的碰撞检测可靠性。

### 🐛 Bug修复 / 其他
8/10-Fix floating-point cancellation in elliptic cone linesearch.（3ab3f0f）
  - 评分：8/10
  - 一句话总结：修复椭圆锥线搜索中的浮点抵消问题。
  - 链接：https://github.com/google-deepmind/mujoco/commit/3ab3f0f0c9f3472d982de29402efdd1b74a62b50
  - 变更规模：+221 -90
  - 提交者：Yuval Tassa
  - 解决的问题：椭圆锥线搜索在 float32 下出现浮点抵消，影响求解精度与稳定性。
  - 产品启示：直接呼应低精度部署可靠性诉求，C 引擎与 MJX/Warp 同步修复体现双后端一致性。

6/10-Fix numerical instability in `wrap_circle` at wrap onset.（8694cc9）
  - 评分：6/10
  - 一句话总结：修复 wrap_circle 在环绕起点处的数值不稳定。
  - 链接：https://github.com/google-deepmind/mujoco/commit/8694cc9ce359cd8547d0632a84d7aa6927a13848
  - 变更规模：+51 -16
  - 提交者：Taylor Howell
  - 解决的问题：环绕起点附近数值不稳定可能导致关节/约束行为异常。
  - 产品启示：边界数值稳定性修复降低长时仿真漂移风险，需持续补充边界测试。

6/10-MuJoCo: fix contact Jacobians of quadratic flexes dropping negative basis weights（9fb4eca）
  - 评分：6/10
  - 一句话总结：修复二次 flex 接触雅可比丢失负基权重的问题。
  - 链接：https://github.com/google-deepmind/mujoco/commit/9fb4eca48b71f3d0e958b99b90a3aaaf87dedb46
  - 变更规模：+91 -2
  - 提交者：Alessio Quaglino
  - 解决的问题：二次 flex 接触雅可比遗漏负基权重，导致接触力计算错误。
  - 产品启示：修正软体接触物理正确性，对高保真软体仿真场景至关重要。

6/10-Fix MJWarp capsule-capsule contacts for parallel and overhanging capsules.（0a7e88e）
  - 评分：6/10
  - 一句话总结：修复 MJWarp 中平行与悬垂胶囊的胶囊-胶囊接触。
  - 链接：https://github.com/google-deepmind/mujoco/commit/0a7e88ec4dc7682ca0818ca4270c30c3c996f822
  - 变更规模：+85 -94
  - 提交者：Google DeepMind
  - 解决的问题：平行/悬垂胶囊几何下 MJWarp 接触计算不正确。
  - 产品启示：保障 GPU/Warp 后端接触语义与 C 引擎一致，降低双轨并行的碎片化风险。

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 40 条
- 高价值提交（≥6分）: 11 条
- 代码更新规模: +11440 / -13640 行
- 主要贡献者: ooctipus, isaaclab-bot[bot], Kelly Guo

## 🧭 趋势点评
本周更新高度延续了仓库“多后端解耦 + 性能工程化 + 测试/CI 提速”的长期主线，并进一步向纵深推进：一方面，`[PR8]/[PR9]/[PR9C]/[PR10]` 系列提交将场景绑定、帧引用、克隆命名空间等抽象从传感器扩展到遥操作、XR 与 cuRobo 等消费者，配合渲染/可视化测试与任务环境解耦，说明 3.0 重构正从“核心子包”走向“跨模块消费者统一”；另一方面，CI 预热 Warp 内核、延迟 TorchScript 转换器导入、缩短最慢 PR 作业等改动，延续了 7-10 月性能提交占比近八成的趋势，把优化重心从单点内核扩展到启动时延与反馈周期。同时，传感器新鲜度、射线网格三角化、OVRTX 导出引用等密集修复，呼应了基线中“9 月前后进入发布前密集修复期”的判断，显示重构收尾阶段对正确性与稳定性的投入正在加强。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-Add keyboard input from the focused visualizer window (#8158)（88f4896）
  - 评分：7/10
  - 一句话总结：为聚焦的可视化窗口新增键盘输入能力，扩展可视化交互方式。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/88f48962e53c003b6eb331d8e70c76515ba724a1
  - 变更规模：+1246 -3
  - 提交者：rwiltz
  - 解决的问题：此前可视化窗口缺乏键盘输入通道，用户无法在聚焦窗口内直接进行交互控制。
  - 产品启示：补齐可视化交互输入能力，有助于遥操作调试与演示体验，配合文档更新可提升开发者上手效率。

### ⚡️ 性能/架构优化
8/10-Decouple renderer and visualizer tests from task environments (#6976)（c7d50a6）
  - 评分：8/10
  - 一句话总结：将渲染器与可视化测试从任务环境中解耦，大幅精简测试依赖。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/c7d50a61689c9e971b37f90a70fd9d4bc3ea9062
  - 变更规模：+3590 -7984
  - 提交者：ooctipus
  - 解决的问题：渲染/可视化测试强依赖任务环境，导致测试矩阵膨胀与启动开销高。
  - 产品启示：测试解耦降低回归成本并提升可维护性，是后端抽象化后测试体系同步演进的直接体现。

7/10-[PR10] Follow declared clone namespaces across scene consumers (#8803)（556e297）
  - 评分：7/10
  - 一句话总结：让场景消费者统一遵循声明的克隆命名空间，收敛跨消费者行为。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/556e29760fde5d3330e6b4240073ef696cedfbaf
  - 变更规模：+721 -769
  - 提交者：ooctipus
  - 解决的问题：不同场景消费者对克隆命名空间处理不一致，导致行为差异与潜在错误。
  - 产品启示：命名空间统一是 3.0 克隆/所有权重构的关键一环，为下游 API 收敛与多消费者一致性奠定基础。

7/10-[PR8] Share scene bindings for sensors and cuRobo (#8765)（8c9b995）
  - 评分：7/10
  - 一句话总结：为传感器与 cuRobo 共享场景绑定，减少重复绑定开销。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/8c9b995cb95c74ec81498ae948ce4c1d4e20ae00
  - 变更规模：+801 -910
  - 提交者：ooctipus
  - 解决的问题：传感器与 cuRobo 各自维护场景绑定，存在重复与不一致。
  - 产品启示：绑定共享是消费者统一架构的延伸，有助于降低多传感器场景的运行时开销。

6/10-[CI] Shorten the slowest PR jobs: warm Warp kernels, contrib on base image, more standalone workers (#8802)（2f44701）
  - 评分：6/10
  - 一句话总结：通过预热 Warp 内核、contrib 复用基础镜像、增加 standalone worker 缩短最慢 PR 作业。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/2f44701dd2a4b5d404bbc9f788b7bbd9f78b54e1
  - 变更规模：+30 -16
  - 提交者：Mustafa H
  - 解决的问题：最慢 PR 作业耗时过长，拖慢反馈周期。
  - 产品启示：CI 提速直接改善贡献者体验与合并吞吐，是高频依赖更新与重构并行推进的基础保障。

6/10-[Fix] Cut ~4 s from the first articulation spawn by deferring the TorchScript converter import (#8762)（84b8df5）
  - 评分：6/10
  - 一句话总结：延迟 TorchScript 转换器导入，为首次 articulation 生成节省约 4 秒。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/84b8df535bc1f8a976be8de5ec995e2e63f6e096
  - 变更规模：+5 -1
  - 提交者：hujc
  - 解决的问题：首次 articulation 生成时同步导入 TorchScript 转换器造成启动延迟。
  - 产品启示：小改动带来可感知的启动时延收益，延续了 lazy import 优化启动成本的既有方向。

### 🐛 Bug修复 / 其他
8/10-Fix sensor freshness, reset cadence, and native coverage (#8780)（1d1a808）
  - 评分：8/10
  - 一句话总结：修复传感器新鲜度、重置节奏与原生覆盖问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/1d1a8087cf7ed6b7f4a8397899eeeb993755ccd4
  - 变更规模：+673 -394
  - 提交者：ooctipus
  - 解决的问题：传感器观测新鲜度与重置节奏不一致，原生路径覆盖不足。
  - 产品启示：传感器正确性直接影响视觉类任务训练质量，是重构收尾期稳定性投入的重点。

6/10-Preserve USD references in OVRTX scene exports (#8769)（b03345b）
  - 评分：6/10
  - 一句话总结：修复 OVRTX 场景导出时丢失 USD 引用的问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/b03345bbf2c9a54eb03f9bd823ae19c0ca3a014e
  - 变更规模：+84 -4
  - 提交者：Maximilian Krause
  - 解决的问题：OVRTX 场景导出未保留 USD 引用，影响资产复用与序列化一致性。
  - 产品启示：导出正确性直接关系资产管线可信度，配合测试补充可降低下游复现风险。

6/10-Fix ray mesh triangulation and query shape validation (#8781)（e4df255）
  - 评分：6/10
  - 一句话总结：修复射线网格三角化与查询形状校验问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/e4df255fc38a2d1faf995774cfc4efbdf3b7936e
  - 变更规模：+111 -25
  - 提交者：ooctipus
  - 解决的问题：射线网格三角化与查询形状校验存在缺陷，影响 RayCaster 结果正确性。
  - 产品启示：射线查询是感知与导航基础能力，输入校验修复提升鲁棒性与可调试性。

6/10-[PR9C] Fix native frame reads and preserve live Fabric poses (#8782)（41480b9）
  - 评分：6/10
  - 一句话总结：修复原生帧读取并保留实时 Fabric 位姿。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/41480b9fca0b89b098ea35d0cd88a73f832007d6
  - 变更规模：+92 -197
  - 提交者：ooctipus
  - 解决的问题：原生帧读取与 Fabric 位姿在共享帧场景下丢失或不一致。
  - 产品启示：帧位姿一致性是跨后端（Newton/Fabric）正确性的关键，修复为多后端并存扫清障碍。

6/10-[PR9] Bind teleop and XR frame references during setup (#8773)（dee1edb）
  - 评分：6/10
  - 一句话总结：在初始化阶段绑定遥操作与 XR 帧引用。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/dee1edb8a7299ae34f20f179ef930e9c8dc330a6
  - 变更规模：+107 -121
  - 提交者：ooctipus
  - 解决的问题：遥操作与 XR 帧引用在运行时才解析，存在时序与一致性问题。
  - 产品启示：初始化期绑定提升遥操作/XR 稳定性，是消费者统一绑定架构向遥操作生态的延伸。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 39 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +12892 / -2450 行
- 主要贡献者: Eric Shi, Nicolas Capens, Alain Denzler

## 🧭 趋势点评

本周高价值提交延续了仓库“性能与正确性并重、工程基建同步推进”的长期主线，但在重心上出现了值得注意的偏移：一方面，`f5ef098` 对 Adjoint 树视图的静态值替换优化，直接接续了 6 月以来 GH-1486 系列的编译期加速链条，说明代码生成路径的优化仍在向更深层的自动微分结构渗透；另一方面，`f15ad57` 将 ASV 基准正式挂到 main 提交上运行，把此前分散的基准设施升级（RTX PRO 6000/B200 池、回归信号改进）收束为真正的性能门禁，这与基线中“性能收益可度量、可回归”的判断高度一致。同时，`ae6bef5` 重写 32 位纹理采样、`1fee698` 扩展 APIC 网格序列化，表明 APIC/CPU 图捕获与运行时数据通路仍在快速扩张，延续了 9 至 10 月图重放与内存生命周期治理的方向。略微偏离长期趋势的是 `9da67a8` 弃用 Python 3.10——这是一次明确的兼容性收缩，而非以往以新增能力为主的演进，意味着项目开始主动收敛支持矩阵以换取工具链现代化空间。整体看，本周更新没有出现 tile 与共享内存子系统的修复类提交，风险热点暂时让位于编译期优化与运行时特性扩展。

## 🔍 关键更新解析

### 🚀 新功能/特性

6/10-Run ASV benchmarks on main commits（f15ad57）
  - 评分：6/10
  - 一句话总结：将 ASV 基准测试接入 main 分支提交流程，使主分支每次提交都产生性能回归信号。
  - 链接：https://github.com/NVIDIA/warp/commit/f15ad57804f16ab4aad3180c1596f9448361da8c
  - 变更规模：+348 -161
  - 提交者：Eric Shi
  - 解决的问题：此前 ASV 基准主要面向 MR 或特定机器池，main 分支缺少持续的性能基线比对，性能回退难以在合入后第一时间被发现。
  - 产品启示：性能门禁从“评审期抽查”升级为“主分支常态监控”，配合已有的 RTX PRO 6000 与 B200 池，可让内核级优化的收益与回退都可量化追踪，强化了仓库作为高性能仿真底座的可靠性叙事。

6/10-Deprecate Python 3.10 support（9da67a8）
  - 评分：6/10
  - 一句话总结：正式弃用 Python 3.10，更新构建脚本、兼容性文档与弃用策略说明。
  - 链接：https://github.com/NVIDIA/warp/commit/9da67a8762abb00027689b3eedd09d49a731d6e9
  - 变更规模：+22 -0
  - 提交者：Eric Shi
  - 解决的问题：Python 3.10 已进入生命周期后段，继续维护会拖累工具链升级（LLVM 22、CUDA 13 构建）与新语法特性的采用。
  - 产品启示：支持矩阵收敛是性能与工具链现代化的必要代价，但需同步做好下游用户迁移提示；对机器人仿真与 RL 训练用户而言，应尽早核对自身 Python 环境，避免升级 Warp 版本时出现环境不兼容。

6/10-Revise 32-bit texture sampling [GH-2065]（ae6bef5）
  - 评分：6/10
  - 一句话总结：重写 32 位纹理采样实现，并新增纹理采样探针与 ASV 基准。
  - 链接：https://github.com/NVIDIA/warp/commit/ae6bef512833f9229f66669d4b5044eaeb64656d
  - 变更规模：+649 -407
  - 提交者：Eric Shi
  - 解决的问题：原有 32 位纹理采样路径在精度与行为一致性上存在不足，且缺少专门的基准与探针来观测采样质量与开销。
  - 产品启示：纹理采样是渲染、感知仿真与神经隐式表示工作负载的基础原语，重写并配套基准意味着该路径的数值行为将更可预期，对依赖纹理做传感器仿真或特征查询的用户是实质性改进。

6/10-Serialize meshes from APIC handle arrays [GH-2114]（1fee698）
  - 评分：6/10
  - 一句话总结：支持从 APIC 句柄数组序列化网格，扩展 APIC 捕获与 CPU 图的能力边界。
  - 链接：https://github.com/NVIDIA/warp/commit/1fee698952c60836ed604f9ebaab616bb171a03f
  - 变更规模：+624 -173
  - 提交者：Eric Shi
  - 解决的问题：APIC 捕获此前对网格类数据的序列化支持不完整，导致含网格的场景在图捕获与重放路径中受限。
  - 产品启示：网格是仿真场景的核心资产，补齐其序列化能力使 APIC/CPU 图捕获可覆盖更真实的机器人仿真与物理场景，配合 10 月以来的图重放加固，图捕获正从“可用”走向“可承载完整场景”。

### ⚡️ 性能/架构优化

7/10-Substitute wp.static values into a per-adjoint tree view [GH-1486]（f5ef098）
  - 评分：7/10
  - 一句话总结：在按伴随（adjoint）组织的树视图中替换 wp.static 值，减少自动微分代码生成阶段的重复遍历与源码处理。
  - 链接：https://github.com/NVIDIA/warp/commit/f5ef0985a8d1efe574a79fda31c321c103be387b
  - 变更规模：+461 -33
  - 提交者：Alain Denzler
  - 解决的问题：Adjoint 代码生成中静态值替换缺乏按伴随粒度的视图，导致引用查找与源码提取在复杂内核上重复开销偏高，是 GH-1486 系列编译期加速的延续。
  - 产品启示：编译期开销直接决定大规模内核与自动微分工作负载的迭代速度；该优化让含大量 wp.static 的内核在反向传播代码生成时更快，对 RL 训练中频繁重编译的场景有实际价值，也说明代码生成路径的优化正从“函数级”深入到“伴随树级”。

### 🐛 Bug修复 / 其他

本周高价值提交中无归入此板块的条目。

---

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 12 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +8314 / -1190 行
- 主要贡献者: guozhen, liyanghao, akushonkamen

## 🧭 趋势点评
本周更新延续了 RLinf 在 2026 年下半年“功能扩张与工程打磨并行”的主线，并进一步向真机栈与多后端训练范式倾斜：OpenPI 全量/梯度分片（30e0236）与 YAM 关节空间训练（196d40b）延续了 9-10 月对 openpi 训练链路的持续深化，Orbbec RGB-D 相机（d844e64）与双 Franka Pico 采集修复（4305707）则强化了基线中已显现的真机闭环与遥操作数据采集方向；rollout 截止时间返回部分解耦批次（fe626a0）与 agentic tokenizer 重构（b0a564b）分别对应分布式训练容错与 agent 能力扩展，前者呼应了基线中 FSDP 超时控制、replay 容错等稳定性治理脉络，后者则偏离了以 VLA/世界模型为主的既有重心，向 agentic 搜索类任务延伸。整体看，本周高价值提交仍以新功能为主（4 条），性能/架构优化类缺席，与基线“性能优化仅占约 3.2%、点状投入”的判断一致，说明项目当前仍处于能力覆盖优先、系统性性能基准滞后的阶段。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-feat(openpi): support full and gradient sharding (#1701)（30e0236）
  - 一句话总结：为 OpenPI 增加 full 与 gradient sharding 两种分片模式，降低显存占用并扩展大模型训练可行性。
  - 链接：https://github.com/RLinf/RLinf/commit/30e0236981c6a1dc19202de64116834c12673828
  - 变更规模：+161 -66
  - 提交者：cc
  - 解决的问题：OpenPI 训练在显存受限场景下缺乏灵活的分片策略，难以在 full 与梯度分片间按资源条件切换。
  - 产品启示：分片模式可选意味着用户可在单卡/多卡、小显存/大显存间平滑迁移，建议配套显存-吞吐对照文档与默认推荐配置，降低调参门槛。
8/10-feat(agent): agentic tokenizer refactor + glm search-r1 (#1549)（b0a564b）
  - 一句话总结：重构 agentic tokenizer 并接入 GLM search-r1，扩展 agent 类任务能力。
  - 链接：https://github.com/RLinf/RLinf/commit/b0a564b764449553d1a565cd02c7b1c1401e3839
  - 变更规模：+2040 -655
  - 提交者：sherlockcooper
  - 解决的问题：原有 tokenizer 难以适配 agentic 搜索类任务的输入输出结构，且缺少 GLM search-r1 示例与文档。
  - 产品启示：项目从纯具身 VLA 向 agentic 任务延伸，建议明确 agent 与 embodied 两条能力线的边界与共享组件，避免文档与配置体系割裂。
7/10-feat(robotics): add Orbbec RGB-D camera support (#1648)（d844e64）
  - 一句话总结：新增 Orbbec RGB-D 相机接入，补齐真机视觉感知硬件支持。
  - 链接：https://github.com/RLinf/RLinf/commit/d844e6485d9c00da497b1e1980996fe36da6fb1c
  - 变更规模：+1225 -12
  - 提交者：ZhichuCen
  - 解决的问题：此前真机栈缺少 Orbbec 系列 RGB-D 相机支持，限制了使用该硬件的 Franka 等真机数据采集与部署。
  - 产品启示：硬件支持矩阵持续扩张，需同步维护相机型号兼容列表与标定/驱动说明，避免用户因硬件差异踩坑。
7/10-feat(yam): add OpenPI joint-space training and evaluation (#1702)（196d40b）
  - 一句话总结：为 YAM 机器人新增 OpenPI 关节空间训练与评估支持。
  - 链接：https://github.com/RLinf/RLinf/commit/196d40b6dec6f7a4063edee31cfeaa6ca0ee435a
  - 变更规模：+932 -37
  - 提交者：Li Wenbo
  - 解决的问题：YAM 平台此前缺少 OpenPI 关节空间训练与评估的完整链路与示例文档。
  - 产品启示：关节空间与笛卡尔空间并存会增加配置复杂度，建议在示例中给出空间选择建议与迁移注意事项，提升新用户上手效率。

### ⚡️ 性能/架构优化
- 本周无符合该分类的高价值提交。

### 🐛 Bug修复 / 其他
7/10-fix(rollout): return partial decoupled batches at deadline (#1743)（fe626a0）
  - 一句话总结：在截止时间到达时返回部分解耦批次，避免 rollout 因等待完整批次而阻塞或超时失败。
  - 链接：https://github.com/RLinf/RLinf/commit/fe626a0e7dfd14ee3dbc543025e1b44321859183
  - 变更规模：+164 -36
  - 提交者：guozhen
  - 解决的问题：解耦批次在截止时间无法凑齐时缺乏降级路径，导致 rollout 卡顿或异常，影响训练稳定性。
  - 产品启示：部分批次返回会改变下游消费语义，需在文档中明确批次不完整的处理约定，并关注其对训练指标统计口径的影响。
6/10-fix(real): modify dual Franka Pico collection (#1693)（4305707）
  - 一句话总结：修复双 Franka Pico 遥操作数据采集流程，并同步更新相关文档。
  - 链接：https://github.com/RLinf/RLinf/commit/4305707f6ef08ad3cf738524a5bf8403c9675fe3
  - 变更规模：+1557 -306
  - 提交者：liyanghao
  - 解决的问题：双 Franka 在 Pico 采集场景下存在流程缺陷，影响真机遥操作数据采集的正确性与可用性。
  - 产品启示：真机采集链路变更规模大且涉及多份文档，建议建立硬件-流程-文档的联动检查清单，降低配置漂移风险。

---

