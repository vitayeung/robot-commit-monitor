# 具身智能周报 (2026年09月30日 14:24:21)

## 行业风向总览

# 具身智能行业风向周度总结

**技术焦点：仿真内核精度与训练稳定性并重。** MuJoCo 本周补齐胶囊体 nativeccd 多接触支持、新增凸几何 Hausdorff 距离下界，并修复 refsite 四元数跨后端一致性问题；Warp 则集中稳定 FEM QR 分解、修复 tile 扫描极值错误，物理求解器的数值稳健性成为共同攻坚点。IsaacLab 推出 ovrtx 异步渲染路径与异构 OvPhysX 克隆，推动渲染与仿真解耦；mjlab 跟进 Python 3.14 / torch 2.14 / CUDA 13 工具链迁移。

**合成数据动态：域随机化与交互式数据采集双线推进。** mjlab 修复 `dr.pseudo_inertia` 对无质量刚体的处理并拒绝不适用分布，提升域随机化数值正确性；RLinf 在 Robotwin 中新增 Dagger 支持，强化仿真侧交互式纠错数据闭环，与真机 DAgger 形成互补，降低真机采集成本。

**产品经理关注信号：** ①IsaacLab 移除并行启动与预设机制、MuJoCo 删除 flex 内部碰撞选项，均为破坏性变更，需排查既有模型与启动脚本兼容性；②RLinf 密集修复 FSDP 检查点 RNG 保留与分片恢复，分布式训练可复现性正成为 RL 框架竞争要素；③IsaacLab 集成性能冒烟测试、RLinf 修复 replay 预取静默失败，提示高频重构下性能守护与数据管线可观测性已成刚需。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 5 条
- 高价值提交（≥6分）: 2 条
- 代码更新规模: +1605 / -1059 行
- 主要贡献者: Kevin Zakka, 상티 (윤상현)

## 🧭 趋势点评
本周的两项高价值更新延续了 mjlab 在 2026 年 9 月所展现的“面向新工具链与训练稳定性”的演进主线：一方面通过 Python 3.14、torch 2.14 与 CUDA 13 的迁移（4ac9df2）继续紧跟上游生态，与过去数月 mujoco/mujoco-warp、rsl-rl-lib 的连续升级节奏一致；另一方面通过修复 dr.pseudo_inertia 中无质量刚体的处理逻辑（f135c1d），延续了项目在域随机化数值正确性与管理器语义打磨上的持续投入，整体未偏离“高频迭代、以修复与依赖维护为主”的长期特征。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-Add Python 3.14 support and move to torch 2.14 with CUDA 13. (#1194)（4ac9df2）
  - 评分：9/10
  - 一句话总结：新增 Python 3.14 支持并整体迁移至 torch 2.14 与 CUDA 13，同步更新 CI、nightly、Makefile、安装文档与 pyproject 配置。
  - 链接：https://github.com/mujocolab/mjlab/commit/4ac9df2f1d67de4aad62c4a38b27c84b04268bbe
  - 变更规模：+1486 -1018
  - 提交者：Kevin Zakka
  - 解决的问题：解决运行时与工具链落后于上游生态的问题，使项目能够在最新的 Python、PyTorch 与 CUDA 组合下构建与运行。
  - 产品启示：表明项目将持续跟进上游运行时栈，用户需关注新版本组合带来的环境兼容性与安装流程变化。

### ⚡️ 性能/架构优化
- 无

### 🐛 Bug修复 / 其他
6/10-Keep massless bodies unchanged in dr.pseudo_inertia and reject log_uniform. (#1199)（f135c1d）
  - 评分：6/10
  - 一句话总结：在 dr.pseudo_inertia 中保留无质量刚体不被修改，并拒绝 log_uniform 采样方式。
  - 链接：https://github.com/mujocolab/mjlab/commit/f135c1daa0f278bd19e323c2b9f256ca541ae2c5
  - 变更规模：+64 -11
  - 提交者：Kevin Zakka
  - 解决的问题：修复伪惯量随机化对无质量刚体的错误处理，并避免 log_uniform 在不适用场景下被误用。
  - 产品启示：域随机化的数值正确性持续被重视，配置项需明确适用边界，避免用户在不支持的分布下产生非预期物理行为。

---

### [google-deepmind/mujoco] 具身智能周报

#### 📊 提交分析
- 本周总提交: 47 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +8625 / -5260 行
- 主要贡献者: Alessio Quaglino, Kyle Bayes, Alessio

## 🧭 趋势点评
本周更新延续了仓库在求解器/碰撞内核与 Studio/Web 工具链双线并进的长期趋势：`6224e95` 为胶囊体补齐 nativeccd multicontact 支持、`129fd8e` 新增凸几何 Hausdorff 距离下界，均属于基线中“凸碰撞与多接触算法显著优化”主线的自然延伸；`adbc7d9` 的 Studio 画中画 Python 绑定与 `c90ba88` 的 mjData 字段扩展，则呼应了“Studio 与渲染栈大幅演进”和“API 现代化”方向。`fa3d0ee` 修复 refsite 四元数乘法顺序、`b1ccf67` 修复 mjSpec 帧处理，属于基线中持续存在的稳定性维护，但前者同时触及 MJX 与 C 引擎，说明跨后端一致性仍是关注点。`5023a4a` 移除 flex 内部碰撞选项与 `flex_evpair` 结构（-491 行），偏离了此前“flex 专项优化密集出现”的加法式演进，转向架构精简与遗留路径清理，可能预示 flex 内部碰撞能力被重新定位或由其他机制替代，需关注其对既有模型兼容性的影响。

## 🔍 关键更新解析

### 🚀 新功能/特性
8/10-Add nativeccd multicontact support for capsules.（6224e95）
  - 评分：8
  - 一句话总结：为胶囊体新增 nativeccd 多接触支持，扩展凸碰撞管线的几何覆盖范围。
  - 链接：https://github.com/google-deepmind/mujoco/commit/6224e95f6264b99790341f505f8528ece2b866ac
  - 变更规模：+300 -35
  - 提交者：Kyle Bayes
  - 解决的问题：此前 nativeccd 的 multicontact 能力未覆盖胶囊体，导致胶囊与其他几何的接触生成可能退化或走非最优路径。
  - 产品启示：胶囊是机器人肢体与障碍物建模的高频几何，补齐该支持可提升接触稳定性与仿真精度，并同步更新 changelog 与 computation 文档，利于用户理解碰撞管线行为。
7/10-Add the mjc_hausdorff function to engine_collision_convex to compute the lower bound of the directed Hausdorff distance between two convex (compact) geoms.（129fd8e）
  - 评分：7
  - 一句话总结：新增 mjc_hausdorff 函数，计算两个凸紧致几何间有向 Hausdorff 距离的下界。
  - 链接：https://github.com/google-deepmind/mujoco/commit/129fd8efc70e2c58e9ec6b336dc7ce5f6296fa0b
  - 变更规模：+355 -0
  - 提交者：Kyle Bayes
  - 解决的问题：凸碰撞管线缺少几何间距离下界的快速估计手段，难以支撑保守剔除或接触质量评估。
  - 产品启示：该函数可作为碰撞检测的预筛选与稳健性判据，配合测试文件落地，为后续 GJK/EPA 优化提供可复用的几何度量基础。

6/10-Add Python bindings for Studio picture-in-picture.（adbc7d9）
  - 评分：6
  - 一句话总结：为 Studio 画中画功能提供 Python 绑定，使实验性 GUI 能力可从 Python 侧调用。
  - 链接：https://github.com/google-deepmind/mujoco/commit/adbc7d91f8b006750ddc1c6ebdd5d01594bf9851
  - 变更规模：+163 -6
  - 提交者：Taylor Howell
  - 解决的问题：Studio 画中画此前缺乏 Python 接口，限制了在脚本化与实验性工作流中的复用。
  - 产品启示：配合 SKILL 文档与 headless_ui 改动，进一步降低 Studio 实验特性的使用门槛，强化 Python 作为 MuJoCo 主要交互入口的定位。
6/10-GitHub Pull Request: https://github.com/google-deepmind/mujoco/pull/3632（c90ba88）
  - 评分：6
  - 一句话总结：扩展 mjData 结构体字段，并同步更新头文件、内省与 Python 结构定义。
  - 链接：https://github.com/google-deepmind/mujoco/commit/c90ba889b020c5353ccb86fb023b8dcad4befbb2
  - 变更规模：+404 -133
  - 提交者：Alessio Quaglino
  - 解决的问题：现有 mjData 字段不足以支撑新增的引擎计算需求，需要扩展数据结构并保持 Python 内省一致。
  - 产品启示：mjData 属于核心公共数据结构，字段扩展会波及 mjxmacro、introspect 与文档，提示下游绑定与序列化工具需同步跟进。
### ⚡️ 性能/架构优化
6/10-Remove flex internal collision option and flex_evpair structures（5023a4a）
  - 评分：6
  - 一句话总结：移除 flex 内部碰撞选项与 flex_evpair 结构，净删减约 400 行代码。
  - 链接：https://github.com/google-deepmind/mujoco/commit/5023a4a50cbb65bc539f954e00997de6127e62b6
  - 变更规模：+88 -491
  - 提交者：Alessio Quaglino
  - 解决的问题：flex 内部碰撞路径与 flex_evpair 结构长期存在维护成本与冗余，需要清理以简化模型与 XML 语义。
  - 产品启示：涉及 mjmodel.h、XMLreference 与 changelog 的同步修改，属于潜在破坏性变更，用户需检查依赖 flex 内部碰撞选项的既有模型并迁移。

### 🐛 Bug修复 / 其他
7/10-Fix frames in the mjSpec API: mjs_delete and mjs_bodyToFrame.（b1ccf67）
  - 评分：7
  - 一句话总结：修复 mjSpec API 中 mjs_delete 与 mjs_bodyToFrame 的帧处理逻辑。
  - 链接：https://github.com/google-deepmind/mujoco/commit/b1ccf67964f03ef2b74221c02c7ea8b809d84bfc
  - 变更规模：+1050 -32
  - 提交者：Yuval Tassa
  - 解决的问题：mjSpec 在删除元素与 body 到 frame 转换时帧处理不正确，影响模型编辑的正确性。
  - 产品启示：改动覆盖 user_api.cc、API 参考文档与 Python specs 测试，说明模型编辑 API 正被系统性加固，是 mjSpec 走向稳定可用的重要一步。

---

6/10-Fix `site_quat` multiplication order in `refsite` transmissions.（fa3d0ee）
  - 评分：6
  - 一句话总结：修正 refsite 传动中 site_quat 的乘法顺序，并同步修复 MJX 侧实现。
  - 链接：https://github.com/google-deepmind/mujoco/commit/fa3d0ee90982f7a447cd5d31a7fcd512bb6d12d9
  - 变更规模：+21 -15
  - 提交者：Yuval Tassa
  - 解决的问题：refsite 传动的四元数乘法顺序错误，导致参考坐标系姿态计算偏差，且 C 引擎与 MJX 行为需保持一致。
  - 产品启示：同时修改 engine_core_smooth.c 与 mjx smooth.py 并补充两侧测试，体现跨后端数值一致性是质量保障重点，用户升级后可获得更准确的传动参考系姿态。
### [isaac-sim/IsaacLab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 138 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +68236 / -115341 行
- 主要贡献者: Mustafa H, ooctipus, isaaclab-bot[bot]

## 🧭 趋势点评
本周更新延续了该仓库“多后端并行演进 + 大规模重构清理 + 测试与 CI 提速”的长期主线，并进一步向渲染与仿真解耦、后端抽象统一的方向深化：异步渲染路径（ovrtx）与异构 OvPhysX 克隆的引入，呼应了基线中 2026-09 相机管线重构与多后端注册机制的趋势；性能冒烟测试集成则延续了 CI 基础设施持续强化、量化性能退化风险的路径。与此同时，移除并行启动与预设机制、内联冗余启动栈辅助函数等改动，明显偏离了此前“功能叠加”的扩张节奏，转向对启动栈的收敛与简化，体现出 core subpackage 3.0 重构进入收尾阶段后对 API 边界与维护成本的主动控制；而多可视化器 Ctrl+C 挂起修复则延续了对稳定性与运行时守卫的持续投入。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-feat: Adds an opt-in asynchronous render path (ovrtx only) (#7075)（eb6617c）
  - 评分：9/10
  - 一句话总结：新增仅限 ovrtx 的可选异步渲染路径，推动渲染与仿真解耦。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/eb6617cdad62aec29b6dd6d1a43e9b4d1e4ca4a2
  - 变更规模：+722 -159
  - 提交者：Peter Verswyvelen
  - 解决的问题：同步渲染路径阻塞仿真步进，限制渲染与物理并行效率。
  - 产品启示：异步渲染为轻量化训练与部署提供新路径，但 opt-in 属性意味着成熟度仍需验证，需配套基准守护。

8/10-Support heterogeneous OvPhysX cloning (#7890)（d176bf0）
  - 评分：8/10
  - 一句话总结：支持异构 OvPhysX 克隆，扩展多后端下资产复制能力。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/d176bf025ea5af1a2da9456cd3de46af41038957
  - 变更规模：+1021 -619
  - 提交者：Maximilian Krause
  - 解决的问题：同构克隆无法覆盖异构场景，限制 OvPhysX 在复杂任务中的适用性。
  - 产品启示：异构克隆能力增强多后端生态灵活性，但会加大测试矩阵与兼容性负担。

6/10-Angehu/perf smoke integration (#7137)（eeb6e04）
  - 评分：6/10
  - 一句话总结：集成性能冒烟测试工具，强化 CI 性能退化预警。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/eeb6e0458cec52499f2719b325d7fabe584b0f93
  - 变更规模：+2002 -1
  - 提交者：angehu-nv
  - 解决的问题：此前性能冒烟基准被移除，缺乏对性能退化的早期预警。
  - 产品启示：性能冒烟集成弥补基准覆盖缺口，是高频重构路径下必要的守护机制。

### ⚡️ 性能/架构优化
7/10-[Core] Remove parallel launch and preset mechanisms (#8112)（b744dbe）
  - 评分：7/10
  - 一句话总结：移除并行启动与预设机制，简化启动栈。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/b744dbec94de3b27f2e39064c56f0b7581a2881c
  - 变更规模：+209 -501
  - 提交者：ooctipus
  - 解决的问题：并行启动与预设机制增加启动路径复杂度与维护成本。
  - 产品启示：启动栈收敛降低理解与维护门槛，但属破坏性变更，需配套迁移指南。

6/10-[Core] Inline launch-stack helpers that only restate or forward (#8111)（24e1b46）
  - 评分：6/10
  - 一句话总结：内联仅做转发或重述的启动栈辅助函数，减少冗余抽象。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/24e1b46ce8cf8fad61f182792708139c5beb70d3
  - 变更规模：+361 -484
  - 提交者：ooctipus
  - 解决的问题：冗余辅助函数增加调用层级与阅读负担。
  - 产品启示：内联清理提升代码可读性，是 3.0 重构收尾阶段 API 边界收敛的体现。

### 🐛 Bug修复 / 其他
6/10-[VDR feedback] Fix shutdown hang on Ctrl+C with multiple visualizers (#7698)（389c12f）
  - 评分：6/10
  - 一句话总结：修复多可视化器场景下 Ctrl+C 退出挂起问题。
  - 链接：https://github.com/isaac-sim/IsaacLab/commit/389c12f52f9f0bea607985fcc181a0f367229222
  - 变更规模：+167 -91
  - 提交者：matthewtrepte
  - 解决的问题：多可视化器同时运行时中断信号无法正常终止进程，导致挂起。
  - 产品启示：运行时中断与清理路径的稳定性直接影响开发体验，需持续覆盖多可视化器组合场景。

---

### [NVIDIA/warp] 具身智能周报

#### 📊 提交分析
- 本周总提交: 25 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +1772 / -367 行
- 主要贡献者: Eric Shi, Gilles Daviet, Zhihui Du

## 🧭 趋势点评
本周高价值提交延续了仓库“性能与数值稳健性双主线”的长期演进路径：一方面继续在运行时与底层内核层面削减开销（Python 内建调用、网格射线占用率、BSR/FEM 性能保持），呼应了基线中“编译期与运行时开销削减为抓手”的趋势；另一方面集中修复数值与几何计算的正确性问题（tile 扫描极值、FEM QR 分解稳定性），与 7 月“强化数值精度与运行时稳健性”的方向高度一致。整体看，本周更新并未偏离长期趋势，而是把优化落点进一步收敛到稀疏/FEM、网格查询与运行时调用路径这些既有热点上，体现出“优化—验证—修复”闭环的常态化推进。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周高价值提交中无归入此类别的条目）

### ⚡️ 性能/架构优化

7/10-Reduce Python built-in call overhead [GH-1983]（7906779）
  - 评分：7/10
  - 一句话总结：通过降低 Python 内建调用开销，减少运行时解释层负担。
  - 链接：https://github.com/NVIDIA/warp/commit/79067793efd89e3bd69b960c73781ccc4ac13c7f
  - 变更规模：+93 -21
  - 提交者：Eric Shi
  - 解决的问题：Python 内建调用路径开销偏高，影响运行时效率。
  - 产品启示：直接降低内核启动与运行时调用延迟，有助于提升大规模并行仿真与强化学习场景下的整体吞吐。

6/10-Restore mesh ray-query occupancy [GH-1840]（45c001d）
  - 评分：6/10
  - 一句话总结：恢复网格射线查询的占用率，改善 BVH 遍历效率。
  - 链接：https://github.com/NVIDIA/warp/commit/45c001d47199f83ae11d8ae798ba7da3e7b2ce31
  - 变更规模：+29 -18
  - 提交者：Eric Shi
  - 解决的问题：mesh ray-query 占用率下降导致查询性能退化。
  - 产品启示：延续 mesh_query_ray/BVH 遍历优化主线，保障机器人仿真中射线查询类负载的性能稳定。

6/10-Preserve BSR and FEM performance [GH-1918]（c59167b）
  - 评分：6/10
  - 一句话总结：在相关改动后保持 BSR 与 FEM 的性能不退化。
  - 链接：https://github.com/NVIDIA/warp/commit/c59167bbec2d78e1bd07e7af3d714ecce241d2ed
  - 变更规模：+10 -6
  - 提交者：Eric Shi
  - 解决的问题：避免稀疏（BSR）与 FEM 路径在迭代中引入性能回退。
  - 产品启示：体现稀疏/FEM 数值内核作为持续优化与守护热点的定位，保障求解器吞吐稳定。

### 🐛 Bug修复 / 其他

7/10-Stabilize FEM QR decompositions (GH-1985)（a596470）
  - 评分：7/10
  - 一句话总结：稳定 FEM QR 分解，提升数值稳健性。
  - 链接：https://github.com/NVIDIA/warp/commit/a596470bafe6805c10fb2ce83ba47857253d37dd
  - 变更规模：+344 -28
  - 提交者：Gilles Daviet
  - 解决的问题：FEM QR 分解在数值上不稳定，可能影响求解精度与收敛。
  - 产品启示：强化 FEM 求解的数值稳健性，为物理仿真与求解器长期稳定运行提供保障。

---

6/10-Fix tile min/max scans on float extremes and uint32 [GH-2003]（13f9a11）
  - 评分：6/10
  - 一句话总结：修复 float 极值与 uint32 下 tile min/max 扫描的错误。
  - 链接：https://github.com/NVIDIA/warp/commit/13f9a110a93daac987042a9e3dd213549d0e15c0
  - 变更规模：+158 -4
  - 提交者：Christopher Crouzet
  - 解决的问题：tile 归约在浮点极值和 uint32 类型下结果不正确。
  - 产品启示：提升 tile 语义在边界数值下的正确性，降低下游数值计算出现静默错误的概率。

### [RLinf/RLinf] 具身智能周报

#### 📊 提交分析
- 本周总提交: 14 条
- 高价值提交（≥6分）: 6 条
- 代码更新规模: +1862 / -613 行
- 主要贡献者: liuke, Andy Lin, panhe1818

## 🧭 趋势点评
本周更新延续了 RLinf 在“功能扩张 + 分布式训练稳定性修复”双主线上的长期趋势，但明显更偏向于修复与兼容性收敛，而非新增模型能力。Robotwin 新增 Dagger 支持（#1551）继续扩展仿真环境与交互式数据采集链路，符合过去数月从仿真到真机闭环的演进方向；而 FSDP 检查点 RNG 保留（#1570）、分片恢复（#1569）、replay 预取失败传播（#1571）等修复，则延续了 2026-09 以来围绕 FSDP 正确性与数据管线健壮性的密集投入。VLM SFT 支持 transformers 5（#1610）与 Cosmos3 SFT/SGLang 评测修复（#1602）体现出对上游依赖升级和新模型链路可用性的快速响应，这与仓库长期依赖更新频繁、生态对接活跃的特征一致。整体看，本周偏离了“新功能占比最高”的基线节奏，转向以修复和兼容性为主，说明在模型与后端矩阵快速扩张后，团队正优先偿还稳定性债务。

## 🔍 关键更新解析

### 🚀 新功能/特性
7/10-feat: support new Dagger in Robotwin (#1551)（7d2dfa7）
  - 评分：7/10
  - 一句话总结：在 Robotwin 中新增 Dagger 支持，扩展了仿真环境下的交互式数据采集与训练能力。
  - 链接：https://github.com/RLinf/RLinf/commit/7d2dfa77faffa7887304670d5fcaed1128b84ae8
  - 变更规模：+265 -37
  - 提交者：renji555
  - 解决的问题：此前 Robotwin 环境缺乏 Dagger 支持，无法在该仿真平台中利用交互式纠错数据进行策略改进。
  - 产品启示：强化了仿真侧 DAgger 数据闭环，与真实世界 VR/HG-DAgger 形成互补，有助于降低真机数据采集成本并加速策略迭代。

### ⚡️ 性能/架构优化
- 无（本周高价值提交中未包含该分类条目）

### 🐛 Bug修复 / 其他
7/10-fix(vlm): support transformers 5 in VLM SFT (#1610)（d1bf37c）
  - 评分：7/10
  - 一句话总结：使 VLM SFT 兼容 transformers 5，跟进上游重大版本升级。
  - 链接：https://github.com/RLinf/RLinf/commit/d1bf37cdc73bba24218d523b08c1c88fcffd9deb
  - 变更规模：+178 -301
  - 提交者：sherlockcooper
  - 解决的问题：transformers 5 升级后 VLM SFT 链路出现不兼容，影响基于新版本库的 SFT 训练。
  - 产品启示：保持与主流生态同步，降低用户因依赖升级导致的迁移成本，同时通过精简代码（-301）减少维护负担。

7/10-fix(cosmos3): make the Cosmos3 SFT and SGLang eval examples run (#1602)（010990e）
  - 评分：7/10
  - 一句话总结：修复 Cosmos3 SFT 与 SGLang 评测示例，使其可实际运行。
  - 链接：https://github.com/RLinf/RLinf/commit/010990e5c81ae17d141d3eab584a3bd1791df950
  - 变更规模：+763 -60
  - 提交者：Andy Lin
  - 解决的问题：Cosmos3 的 SFT 与 SGLang 评测示例此前无法正常运行，阻碍用户复现与使用该模型链路。
  - 产品启示：提升新模型示例的可用性，配合 e2e 测试工作流，有助于 Cosmos3 在社区中的推广与落地。

---

6/10-fix(data): propagate replay prefetch sampling failures (#1571)（edca3a5）
  - 评分：6/10
  - 一句话总结：修复 replay 预取采样失败未向上传播的问题，避免静默错误影响训练数据质量。
  - 链接：https://github.com/RLinf/RLinf/commit/edca3a56ab396e9388aa1d1665ff55413b0d3287
  - 变更规模：+104 -52
  - 提交者：liuke
  - 解决的问题：replay 预取采样失败时错误未被正确传播，可能导致训练使用不完整或错误数据而无感知。
  - 产品启示：提升数据管线可观测性与容错性，减少因静默失败导致的训练结果偏差，增强用户对 replay 机制的信任。

6/10-fix(fsdp): preserve per-rank RNG in DCP checkpoints (#1570)（dec2377）
  - 评分：6/10
  - 一句话总结：在 DCP 检查点中保留各 rank 的 RNG 状态，保证恢复训练时随机性一致。
  - 链接：https://github.com/RLinf/RLinf/commit/dec2377bb8fa726827b36b12bb99cbfba12657dd
  - 变更规模：+46 -6
  - 提交者：liuke
  - 解决的问题：FSDP 检查点未保存 per-rank RNG，导致断点续训后随机数序列不一致，影响实验可复现性。
  - 产品启示：提升分布式训练断点续训的确定性，对需要严格复现的 RL 实验尤为关键。

6/10-fix(fsdp2): restore local shards as distributed tensors (#1569)（20ad900）
  - 评分：6/10
  - 一句话总结：修复 FSDP2 恢复时将本地分片还原为分布式张量的问题，确保检查点加载正确。
  - 链接：https://github.com/RLinf/RLinf/commit/20ad900fb8350bb53c980cbdc761d8b5caabb99a
  - 变更规模：+79 -11
  - 提交者：liuke
  - 解决的问题：FSDP2 检查点恢复时本地分片未按分布式张量处理，可能导致加载后模型状态不一致。
  - 产品启示：保障大规模 FSDP 训练的可恢复性，降低长周期训练因中断而重跑的成本。

