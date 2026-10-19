# WanPhys Weekly Report (2026-10-19 09:13:38)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-10-19 09:13:55
- 统计截止: 2026-10-19 09:13:38
- 分析窗口: 2026-10-12 12:02:38 +0800 至 2026-10-19 09:13:38 +0800（左闭右开）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 5/10-Revert "sjtu: add lfm solver"（e7eac7a）
  - 提交者：Wei Wu
  - 提交时间：2026-10-12
  - 修改：wanphys/examples/catalog.py
  - 删除：wanphys/examples/fluids/fluid_grid_lfm_cavity.py
  - 删除：wanphys/examples/fluids/lfm_ghia.py

- 4/10-sjtu: add lfm solver（dd1c0d7）
  - 提交者：setsuna
  - 提交时间：2026-10-12
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/fluids/fluid_grid_lfm_cavity.py
  - 新增：wanphys/examples/fluids/lfm_ghia.py

#### 📊 提交分析
- 本周总提交: 6 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +37156 / -3116 行
- 主要贡献者: Wei Wu, Lei Lan, huangtaikai, setsuna

## 📈 趋势点评
本周更新高度聚焦于仓库既有的“确定性物理仿真”主线，并进一步将其从求解器层扩展到碰撞生成、归约与参考实现的完整链路：`06f82ad` 的 newton-1.0 确定性大规模落地、`d5e1ce6` 的原生确定性 Semi-Implicit Featherstone/XPBD 求解器体系、`28a26a6` 的 newton 可选确定性参考实现，三者共同延续并强化了基线中“确定性成为贯穿全栈设计原则”的长期趋势。同时，`d0f9eeb` 对确定性 Featherstone 输入与 XPBD 关节状态的修复，说明团队在快速扩张确定性能力的同时开始收敛数值一致性问题，这与基线中“功能开发与稳定性打磨并行”的节奏一致，未出现明显偏离。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-newton-1.0 deterministic（06f82ad）
  - 评分：9/10
  - 一句话总结：大规模落地 newton-1.0 确定性碰撞与求解路径，新增确定性碰撞排序、常量与接触容量等模块。
  - 提交时间：2026-10-13
  - 变更规模：+15881 / -976
  - 提交者：huangtaikai
  - 解决的问题：为 newton-1.0 提供端到端的确定性碰撞与求解实现，填补确定性流程在碰撞排序与接触容量管理上的空白。
  - 产品启示：确定性语义正式进入 newton-1.0 主路径，可作为机器人学习与仿真评测可复现基线的核心卖点对外呈现。

9/10-feat(wanphys): add native deterministic Semi-Implicit Featherstone and XPBD solvers（d5e1ce6）
  - 评分：9/10
  - 一句话总结：新增原生确定性 Semi-Implicit Featherstone 与 XPBD 求解器体系，并配套固定接触归约与窄相碰撞模块。
  - 提交时间：2026-10-15
  - 变更规模：+11072 / -28
  - 提交者：Lei Lan
  - 解决的问题：为刚体仿真提供原生确定性求解器，替代此前依赖外部或非确定性路径的实现。
  - 产品启示：原生确定性求解器体系强化了可复现性护城河，可作为高性能刚体仿真的差异化能力重点宣传。

8/10-feat(newton): add opt-in deterministic solver reference implementations（28a26a6）
  - 评分：8/10
  - 一句话总结：为 newton 增加可选的确定性求解器参考实现，含累加器、窄相与归约数学模块。
  - 提交时间：2026-10-15
  - 变更规模：+7653 / -27
  - 提交者：Lei Lan
  - 解决的问题：提供可对照的确定性参考实现，便于验证与对齐主求解器的数值行为。
  - 产品启示：opt-in 参考实现降低了用户迁移门槛，可作为确定性能力的渐进式采用路径与正确性背书。

### ⚙️ 性能/架构优化
- 本周无对应高价值提交。

### 🧰 Bug修复 / 其他
6/10-Fix deterministic Featherstone inputs and XPBD joint state（d0f9eeb）
  - 评分：6/10
  - 一句话总结：修复确定性 Featherstone 输入与 XPBD 关节状态的一致性问题，并补充对应测试。
  - 提交时间：2026-10-15
  - 变更规模：+484 / -19
  - 提交者：Wei Wu
  - 解决的问题：确定性求解器输入与 XPBD 关节状态存在不一致，影响确定性路径的数值正确性与可复现性。
  - 产品启示：确定性能力扩张后需同步补齐数值一致性修复与测试，提示应将确定性回归测试纳入常态化质量门禁。
