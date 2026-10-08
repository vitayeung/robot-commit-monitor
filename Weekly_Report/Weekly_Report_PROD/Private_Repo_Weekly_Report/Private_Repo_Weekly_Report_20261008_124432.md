# WanPhys Weekly Report (2026-10-08 12:44:32)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-10-08 12:44:32
- 统计截止: 2026-10-08 12:44:32
- 分析窗口: 最近 7 天（截止上述时间）
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

- 5/10-Keep fish training in playground and type rigid controls（128bbe3）
  - 提交者：Wei Wu
  - 提交时间：2026-10-03
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 6/10-add example diff fish（96b787e）
  - 提交者：syq
  - 提交时间：2026-10-03
  - 新增：wanphys/examples/fluids/fluid_grid_mpm_diff_fish_swim.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 3/10-refactor(fluid): keep large-city migration scoped（22cab76）
  - 提交者：sjtu_dalab
  - 提交时间：2026-10-02
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse_liquid_city.py

- 5/10-feat(fluid): migrate task3 large-city scene onto dev（ebdc575）
  - 提交者：sjtu_dalab
  - 提交时间：2026-10-02
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse_liquid_city.py

#### 📊 提交分析
- 本周总提交: 13 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +29405 / -18649 行
- 主要贡献者: huangtaikai, syq, Wei Wu, sjtu_dalab

## 📈 趋势点评
本周（2026-10-06 前后）的更新高度延续了仓库自 2026-09 以来“由快速扩张转向稳定收敛”的长期趋势，并进一步聚焦于确定性仿真与碰撞管线重构这一核心主线。8d43350、215b28a、387de2f 三条高价值提交集中落地了刚体-颗粒、AVBD、Style3D 以及 hydroelastic 的确定性接触生成与归约，3dfc3cc 与 af3f1fd 则通过大规模重构和代码精简推动碰撞管线向更清晰的确定性流程收敛，这与基线中“2026-10 确定性碰撞与高度场收尾阶段”的判断完全吻合。f1e5cba 新增原生 heightfield 构建与碰撞支持，延续了 2026-07 至 2026-08 以来地形与地理数据能力的扩展方向；96b787e 新增 diff fish 示例则延续了流体/MPM 可微仿真能力的补齐。整体看，本周并未偏离长期趋势，而是将 9 月峰值期开启的确定性、回归与管线统一主题推进到落地阶段，性能/架构优化类提交占比明显提升，体现出项目在功能铺设后进入接口稳定与可复现性建设的收敛期。

## 📌 关键更新解析

### 🌟 新功能/特性

9/10-Implement deterministic collision generation and reduction for rigid-particle, AVBD, and Style3D contact（8d43350）
- 评分：8/10
- 一句话总结：为刚体-颗粒、AVBD 与 Style3D 接触实现确定性碰撞生成与归约，是确定性仿真主线的关键落地。
- 提交时间：2026-10-06
- 变更规模：+5309 / -730
- 提交者：huangtaikai
- 解决的问题：此前接触生成与归约在不同求解器路径下缺乏确定性，导致仿真结果难以复现、回归验证困难。
- 产品启示：确定性接触能力是仿真可信度的基础，可支撑数值回归与 CI 门禁，提升多求解器场景下的结果一致性。

8/10-Implement deterministic hydroelastic collision（215b28a）
- 评分：8/10
- 一句话总结：实现确定性 hydroelastic 碰撞，扩展了确定性碰撞在软接触/弹性接触场景的覆盖。
- 提交时间：2026-10-06
- 变更规模：+1578 / -67
- 提交者：huangtaikai
- 解决的问题：hydroelastic 碰撞此前缺少确定性保证，接触归约与排序存在不确定性。
- 产品启示：将确定性能力延伸至 hydroelastic，有助于软体与刚柔耦合场景的可复现仿真与回归测试。

8/10-Implement deterministic rigid collisions and remove legacy serial paths（387de2f）
- 评分：8/10
- 一句话总结：实现确定性刚体碰撞并移除遗留串行路径，统一了刚体碰撞的确定性流程。
- 提交时间：2026-10-06
- 变更规模：+2057 / -441
- 提交者：huangtaikai
- 解决的问题：遗留串行路径与新的确定性流程并存，造成行为不一致与维护负担。
- 产品启示：清理遗留路径可降低接口分叉风险，为刚体碰撞的长期稳定与性能优化奠定基础。

7/10-Add native heightfield construction and collision support.（f1e5cba）
- 评分：7/10
- 一句话总结：新增原生 heightfield 构建与碰撞支持，扩展了地形碰撞能力。
- 提交时间：2026-10-06
- 变更规模：+329 / -143
- 提交者：huangtaikai
- 解决的问题：此前高度场构建与碰撞依赖外部或非原生实现，集成度与可控性不足。
- 产品启示：原生 heightfield 支持为大规模地形、颗粒与波算法场景提供统一碰撞基础，延续地形数据能力扩展方向。

6/10-add example diff fish（96b787e）
- 评分：6/10
- 一句话总结：新增可微鱼游示例，补齐流体/MPM 可微仿真示例生态。
- 提交时间：2026-10-03
- 变更规模：+6792 / -4094
- 提交者：syq
- 解决的问题：缺少面向可微流体耦合的完整示例，用户难以理解 diff coupling 与 MPM 梯度能力。
- 产品启示：可微仿真示例有助于展示前向/差分能力，推动流体与软体算法多样化落地。

### ⚙️ 性能/架构优化

9/10-Refactor collision pipelines for clearer deterministic flows（3dfc3cc）
- 评分：9/10
- 一句话总结：大规模重构碰撞管线，使确定性流程更加清晰统一。
- 提交时间：2026-10-06
- 变更规模：+1993 / -2121
- 提交者：huangtaikai
- 解决的问题：碰撞管线在多次迭代后结构复杂、确定性流程不清晰，CCD 与颗粒碰撞路径耦合。
- 产品启示：管线重构是确定性仿真收敛的核心步骤，可降低模块耦合与维护成本，为后续统一抽象铺路。

6/10-Simplify collision code and reuse shared resources.（af3f1fd）
- 评分：6/10
- 一句话总结：精简碰撞代码并复用共享资源，减少冗余实现。
- 提交时间：2026-10-06
- 变更规模：+376 / -757
- 提交者：huangtaikai
- 解决的问题：CCD 核函数中存在重复逻辑与资源浪费，影响可维护性与性能。
- 产品启示：代码精简与资源共享有助于降低维护成本，提升碰撞模块的长期可演进性。

### 🧰 Bug修复 / 其他
（本周高价值提交中无对应分类条目）
