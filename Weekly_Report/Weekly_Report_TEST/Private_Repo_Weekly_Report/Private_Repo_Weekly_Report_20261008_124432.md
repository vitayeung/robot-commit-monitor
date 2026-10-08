# WanPhys Weekly Report (2026-10-08 12:44:32)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-10-08 12:44:32
- 统计截止: 2026-10-08 12:44:32
- 分析窗口: 2026-09-30 11:34:56 +0800 至 2026-10-08 12:44:32 +0800（左闭右开）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 9/10-Refactor collision pipelines for clearer deterministic flows（3dfc3cc）
  - 提交者：huangtaikai
  - 提交时间：2026-10-06
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/cloth/example_cloth_hanging.py
  - 修改：wanphys/examples/rigid_fluid_gated_benchmark.py

- 9/10-Implement deterministic collision generation and reduction for rigid-particle, AVBD, and Style3D contact（8d43350）
  - 提交者：huangtaikai
  - 提交时间：2026-10-06
  - 修改：wanphys/examples/cloth/example_cloth_hanging.py
  - 修改：wanphys/examples/cloth/example_cloth_style3d.py

- 2/10-Annotate the fish scene rigid solver with its native contract（25a36f4）
  - 提交者：Wei Wu
  - 提交时间：2026-10-03
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 6/10-Keep fish training in playground and type rigid controls（128bbe3）
  - 提交者：Wei Wu
  - 提交时间：2026-10-03
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 7/10-add example diff fish（96b787e）
  - 提交者：syq
  - 提交时间：2026-10-03
  - 新增：wanphys/examples/fluids/fluid_grid_mpm_diff_fish_swim.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 4/10-refactor(fluid): keep large-city migration scoped（22cab76）
  - 提交者：sjtu_dalab
  - 提交时间：2026-10-02
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse_liquid_city.py

- 6/10-feat(fluid): migrate task3 large-city scene onto dev（ebdc575）
  - 提交者：sjtu_dalab
  - 提交时间：2026-10-02
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse_liquid_city.py

#### 📊 提交分析
- 本周总提交: 13 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +29405 / -18649 行
- 主要贡献者: huangtaikai, syq, Wei Wu, sjtu_dalab

## 📈 趋势点评
本周（2026-10 初）的更新高度延续了仓库自 2026-09 以来确立的“确定性仿真收敛”主线，并进一步将其推向碰撞管线的核心：8d43350、215b28a、387de2f 与 3dfc3cc 集中落地了刚体、颗粒、AVBD、Style3D 及水弹性接触的确定性生成与归约，同时以大规模重构（+1993/-2121）清理了旧有串行路径与碰撞流程，标志着项目从“功能快速堆叠”正式转入“可复现管线统一”阶段。与此同时，f1e5cba 的原生高度场碰撞、96b787e 的可微鱼示例与 ebdc575 的大城市场景迁移，说明地形、可微流体与大规模场景能力仍在横向扩展，而 af3f1fd 与 128bbe3 的精简复用与类型化则呼应了长期存在的去耦与接口稳定诉求。整体看，本周并未偏离基线趋势，而是把 2026-09 峰值期提出的“确定性碰撞 + 回归/性能框架”从规划推进为具体实现，风险仍集中在多轮重构带来的接口漂移与行为差异验证上。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-Implement deterministic collision generation and reduction for rigid-particle, AVBD, and Style3D contact（8d43350）
  - 评分：8/10
  - 一句话总结：为刚体-颗粒、AVBD 与 Style3D 接触实现确定性生成与归约，是确定性碰撞主线在多种接触类型上的关键落地。
  - 提交时间：2026-10-06
  - 变更规模：+5309 / -730
  - 提交者：huangtaikai
  - 解决的问题：此前接触生成与归约在不同求解器/接触类型间缺乏统一确定性保证，导致仿真结果难以复现。
  - 产品启示：确定性接触是仿真可信度与回归测试的基础，应作为对外承诺的核心能力进行文档化与基准覆盖。

8/10-Implement deterministic hydroelastic collision（215b28a）
  - 评分：8/10
  - 一句话总结：实现确定性水弹性碰撞，补齐了软体/流体交互场景下的确定性接触能力。
  - 提交时间：2026-10-06
  - 变更规模：+1578 / -67
  - 提交者：huangtaikai
  - 解决的问题：水弹性接触此前缺少确定性归约与排序机制，难以在回归框架中稳定比对。
  - 产品启示：水弹性确定性能力可支撑软体机器人、触觉交互等高价值场景的可复现仿真。

8/10-Implement deterministic rigid collisions and remove legacy serial paths（387de2f）
  - 评分：8/10
  - 一句话总结：实现确定性刚体碰撞并移除遗留串行路径，统一了刚体碰撞的确定性执行流程。
  - 提交时间：2026-10-06
  - 变更规模：+2057 / -441
  - 提交者：huangtaikai
  - 解决的问题：旧串行路径与确定性流程并存，造成行为不一致与维护负担。
  - 产品启示：移除遗留路径可降低长期维护成本，但需配套回归验证以防行为漂移。

7/10-add example diff fish（96b787e）
  - 评分：7/10
  - 一句话总结：新增可微鱼示例，扩展了 MPM/流体网格的可微仿真演示能力。
  - 提交时间：2026-10-03
  - 变更规模：+6792 / -4094
  - 提交者：syq
  - 解决的问题：缺少面向可微流体-刚体耦合的完整示例，用户难以快速上手 diff 能力。
  - 产品启示：可展示示例是推广可微仿真能力的关键入口，应配套文档与性能清单。

7/10-Add native heightfield construction and collision support.（f1e5cba）
  - 评分：7/10
  - 一句话总结：新增原生高度场构建与碰撞支持，强化了地形类场景的物理仿真基础。
  - 提交时间：2026-10-06
  - 变更规模：+329 / -143
  - 提交者：huangtaikai
  - 解决的问题：此前高度场依赖外部或非原生实现，碰撞与构建流程不统一。
  - 产品启示：原生高度场是地形、月面 DTM、颗粒等场景的公共底座，应优先稳定其接口。

6/10-feat(fluid): migrate task3 large-city scene onto dev（ebdc575）
  - 评分：6/10
  - 一句话总结：将 task3 大城市场景迁移至 dev 分支，验证了稀疏液体求解器在大规模场景下的可用性。
  - 提交时间：2026-10-02
  - 变更规模：+889 / -113
  - 提交者：sjtu_dalab
  - 解决的问题：大城市场景此前未在开发主线集成，缺乏大规模稀疏液体仿真示例。
  - 产品启示：大规模场景示例有助于暴露性能与内存瓶颈，应纳入性能清单持续跟踪。

### ⚙️ 性能/架构优化
9/10-Refactor collision pipelines for clearer deterministic flows（3dfc3cc）
  - 评分：9/10
  - 一句话总结：大规模重构碰撞管线以形成更清晰的确定性流程，是本周架构收敛的核心提交。
  - 提交时间：2026-10-06
  - 变更规模：+1993 / -2121
  - 提交者：huangtaikai
  - 解决的问题：碰撞管线流程混杂，确定性路径不清晰，CCD 与颗粒/刚体模块耦合度高。
  - 产品启示：管线清晰化是后续确定性扩展与性能优化的前提，但需警惕重构期的接口兼容风险。

6/10-Keep fish training in playground and type rigid controls（128bbe3）
  - 评分：6/10
  - 一句话总结：将鱼类训练保留在 playground 并对刚体控制进行类型化，改善了示例与耦合代码的组织性。
  - 提交时间：2026-10-03
  - 变更规模：+4265 / -4307
  - 提交者：Wei Wu
  - 解决的问题：训练逻辑与核心库耦合、刚体控制缺少类型约束，影响可维护性。
  - 产品启示：示例与核心库解耦、类型化接口有助于降低外部贡献者的接入成本。

6/10-Simplify collision code and reuse shared resources.（af3f1fd）
  - 评分：6/10
  - 一句话总结：精简碰撞代码并复用共享资源，减少了 CCD 内核中的重复实现。
  - 提交时间：2026-10-06
  - 变更规模：+376 / -757
  - 提交者：huangtaikai
  - 解决的问题：CCD 内核中候选、凸体、网格重叠等逻辑存在重复，维护成本高。
  - 产品启示：共享资源复用是碰撞管线长期可维护的关键，应作为重构的持续原则。

### 🧰 Bug修复 / 其他
- 本周高价值提交中无对应 Bug修复 / 其他 分类的条目。
