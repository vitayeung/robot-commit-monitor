# WanPhys Weekly Report (2026-09-30 15:58:34)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-30 15:58:34
- 统计截止: 2026-09-30 15:58:34
- 分析窗口: 最近 7 天（截止上述时间）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 6/10-Use public cloth APIs and refresh heightfield documentation（e098be0）
  - 提交者：Wei Wu
  - 提交时间：2026-09-25
  - 修改：wanphys/examples/soft/example_cloth_bending.py
  - 修改：wanphys/examples/soft/example_cloth_franka.py
  - 修改：wanphys/examples/soft/example_cloth_h1.py
  - 修改：wanphys/examples/soft/example_cloth_hanging.py
  - 修改：wanphys/examples/soft/example_cloth_style3d.py
  - 修改：wanphys/examples/soft/example_cloth_style3d_avatars.py
  - 修改：wanphys/examples/soft/example_cloth_twist.py

- 3/10-Restore validation for deterministic cloth comparisons（522f6a4）
  - 提交者：Wei Wu
  - 提交时间：2026-09-25
  - 修改：wanphys/examples/soft/regression_test/regression_test_newton_wanphys.py

- 8/10-Complete the public PeriFEM solver API（53f9ca1）
  - 提交者：Wei Wu
  - 提交时间：2026-09-25
  - 修改：wanphys/examples/soft/peri_fem_balls_in_box.py
  - 修改：wanphys/examples/soft/peri_fem_beam_twist.py
  - 修改：wanphys/examples/soft/peri_fem_cantilever.py
  - 修改：wanphys/examples/soft/peri_fem_rigid_mesh_sphere.py
  - 修改：wanphys/examples/soft/peri_fem_sheet_drop.py
  - 修改：wanphys/examples/soft/peri_fem_sheet_swing.py

- 6/10-Move author-maintained scenarios into playgrounds（e29c088）
  - 提交者：Wei Wu
  - 提交时间：2026-09-25
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py

- 9/10-feat: add deterministic model to newton solvers: vbd & style3d; feat: add regression tests for newton and wanphys vbd & style3d(projective cloth) solvers.（5f332cb）
  - 提交者：dreliveam
  - 提交时间：2026-09-25
  - 新增：wanphys/examples/references/manifests/soft.deterministic-cloth-bending.json
  - 新增：wanphys/examples/references/manifests/soft.deterministic-cloth-hanging-style3d.json
  - 新增：wanphys/examples/references/manifests/soft.deterministic-cloth-style3d.json
  - 新增：wanphys/examples/references/manifests/soft.deterministic-cloth-twist.json
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_avatars_for_style3d.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_bending_for_vbd.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_for_style3d.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_franka_for_vbd.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_h1_for_style3d.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_hanging_for_style3d.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_hanging_for_vbd.py
  - 新增：wanphys/examples/soft/regression_test/quick_test_cloth_twist_for_vbd.py
  - 新增：wanphys/examples/soft/regression_test/regression_test_newton_wanphys.py
  - 新增：wanphys/examples/soft/regression_test/regression_test_wanphys_vbd_and_pc.py

- 8/10-feat: add regression mode to vbd/projective cloth and examples.（ed18394）
  - 提交者：dreliveam
  - 提交时间：2026-09-25
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/soft/_kinematic_robot.py
  - 新增：wanphys/examples/soft/_style3d_assets.py
  - 新增：wanphys/examples/soft/example_cloth_bending.py
  - 新增：wanphys/examples/soft/example_cloth_franka.py
  - 新增：wanphys/examples/soft/example_cloth_h1.py
  - 新增：wanphys/examples/soft/example_cloth_hanging.py
  - 新增：wanphys/examples/soft/example_cloth_style3d.py
  - 新增：wanphys/examples/soft/example_cloth_style3d_avatars.py
  - 新增：wanphys/examples/soft/example_cloth_twist.py

- 4/10-Fix bugs.（9c177a4）
  - 提交者：dreliveam
  - 提交时间：2026-09-25
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/heightfield/lunar_dtm_landing_bunny.py
  - 修改：wanphys/examples/soft/pd_clothes_drape_dragon.py
  - 修改：wanphys/examples/soft/pd_clothes_throw_dragon.py
  - 修改：wanphys/examples/soft/peri_cloth_falling.py
  - 修改：wanphys/examples/soft/peri_cloth_hanging.py
  - 修改：wanphys/examples/soft/peri_cloth_test.py
  - 修改：wanphys/examples/soft/peri_cloth_twist.py
  - 修改：wanphys/examples/soft/peri_fem_balls_in_box.py
  - 修改：wanphys/examples/soft/vbd_ball_and_bricks.py

- 8/10-feat: add peri-fem solver (delete old vbd_soft_body solver).（dbaaceb）
  - 提交者：dreliveam
  - 提交时间：2026-09-25
  - 重命名：wanphys/examples/soft/peri_fem_balls_in_box.py
  - 新增：wanphys/examples/soft/peri_fem_beam_twist.py
  - 新增：wanphys/examples/soft/peri_fem_cantilever.py
  - 新增：wanphys/examples/soft/peri_fem_rigid_mesh_sphere.py
  - 新增：wanphys/examples/soft/peri_fem_sheet_drop.py
  - 新增：wanphys/examples/soft/peri_fem_sheet_swing.py

- 8/10-feat: update heightfield structure to support more rigid solvers.（1778c24）
  - 提交者：dreliveam
  - 提交时间：2026-09-25
  - 删除：wanphys/examples/heightfield/dynamic_heightfield.py
  - 新增：wanphys/examples/heightfield/dynamic_heightfield_bunny.py
  - 修改：wanphys/examples/heightfield/granular_balls_rigid.py
  - 修改：wanphys/examples/heightfield/granular_hill_bunny_rigid.py
  - 修改：wanphys/examples/heightfield/granular_lunar_surface_random.py
  - 修改：wanphys/examples/heightfield/granular_png_hill_rigid.py
  - 删除：wanphys/examples/heightfield/granular_png_terrain_rigid.py
  - 新增：wanphys/examples/heightfield/granular_sand_anymal_d.py
  - 新增：wanphys/examples/heightfield/granular_sand_anymal_d_mujoco.py
  - 新增：wanphys/examples/heightfield/lunar_aristarch13_landing_anymal_mujoco.py
  - 重命名：wanphys/examples/heightfield/lunar_dtm_landing_bunny.py

- 4/10-test(perf): restore fluid jet and surface tension manifests（9816b90）
  - 提交者：FYTalon
  - 提交时间：2026-09-24
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.dfsph-non-newtonian-jet.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.dfsph-surface-tension-akinci2013.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.dfsph-surface-tension-jeske2023.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.pbf-non-newtonian-jet.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.pbf-surface-tension-akinci2013.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.pbf-surface-tension-jeske2023.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-non-newtonian-jet.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-surface-tension-akinci2013.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-surface-tension-jeske2023.json

#### 📊 提交分析
- 本周总提交: 13 条
- 高价值提交（≥6分）: 7 条
- 代码更新规模: +34721 / -3748 行
- 主要贡献者: Wei Wu, dreliveam, FYTalon

## 📈 趋势点评
本周更新延续了仓库自 2026 年 6 月以来“从功能扩张转向工程化收敛”的长期趋势，并进一步强化了 9 月集中爆发的确定性求解与回归体系建设主线。5f332cb、ed18394 与 dbaaceb/53f9ca1 分别从 Newton 求解器确定性模型、VBD/投影布料回归模式、PeriFEM 公共 API 三个方向，把此前零散的求解器改动收敛为可复现、可回归的公共能力，与 7 月建立的数值回归与性能框架、9 月对齐 benchmark 与性能清单的路径高度一致。1778c24 对高度场结构的扩展则延续了 7 月以来 heightfield wave/granule 与地形数据接口的多物理场横向扩张趋势。e29c088 与 e098be0 属于架构与文档治理类改动，呼应了 9 月“外置运行时资产、降低示例私有耦合、刷新文档”的收敛方向，整体未偏离仓库长期路线，而是把 9 月的爆发式提交进一步沉淀为边界清晰、API 公共化的工程结构。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-feat: add deterministic model to newton solvers: vbd & style3d; feat: add regression tests for newton and wanphys vbd & style3d(projective cloth) solvers.（5f332cb）
  - 评分：9/10
  - 一句话总结：为 Newton 的 VBD 与 Style3D 求解器引入确定性模型，并配套 Newton 与 WanPhys 两侧 VBD/Style3D（投影布料）回归测试。
  - 提交时间：2026-09-25
  - 变更规模：+18986 / -0
  - 提交者：dreliveam
  - 解决的问题：此前求解器缺乏确定性保证与回归验证，难以复现数值结果、难以在重构后确认行为一致性。
  - 产品启示：确定性求解器与回归测试是物理仿真产品可交付、可维护的基础能力，应作为求解器公共 API 的标配而非附加项。

8/10-Complete the public PeriFEM solver API（53f9ca1）
  - 评分：8/10
  - 一句话总结：完成 PeriFEM 求解器的公共 API，并同步更新 README 与 core 导出。
  - 提交时间：2026-09-25
  - 变更规模：+171 / -85
  - 提交者：Wei Wu
  - 解决的问题：PeriFEM 求解器此前接口不完整、对外暴露不清晰，用户难以通过公共入口调用。
  - 产品启示：求解器能力需通过稳定的公共 API 对外交付，配套文档同步更新才能形成可被外部依赖的产品接口。

8/10-feat: add peri-fem solver (delete old vbd_soft_body solver).（dbaaceb）
  - 评分：8/10
  - 一句话总结：新增 peri-fem 求解器并删除旧的 vbd_soft_body 求解器，完成软体求解器替换。
  - 提交时间：2026-09-25
  - 变更规模：+3636 / -1390
  - 提交者：dreliveam
  - 解决的问题：旧 vbd_soft_body 求解器结构陈旧、维护成本高，需要以 PeriFEM 统一软体求解路径。
  - 产品启示：求解器迭代应采取“新增+删除旧实现”的替换策略，避免新旧并存造成维护面膨胀与用户选择困惑。

8/10-feat: add regression mode to vbd/projective cloth and examples.（ed18394）
  - 评分：8/10
  - 一句话总结：为 VBD/投影布料求解器及示例增加回归模式，支持确定性比较验证。
  - 提交时间：2026-09-25
  - 变更规模：+7324 / -760
  - 提交者：dreliveam
  - 解决的问题：布料求解器缺少回归模式，重构或优化后无法自动校验数值行为是否保持一致。
  - 产品启示：回归模式应下沉到求解器与示例层，使性能优化与重构可在 CI 中被持续验证，降低回归风险。

8/10-feat: update heightfield structure to support more rigid solvers.（1778c24）
  - 评分：8/10
  - 一句话总结：更新高度场结构以支持更多刚体求解器，并同步更新 API 文档与 granular 耦合模块。
  - 提交时间：2026-09-25
  - 变更规模：+3501 / -1215
  - 提交者：dreliveam
  - 解决的问题：原高度场结构仅适配有限刚体求解器，限制了地形与多求解器耦合场景的扩展。
  - 产品启示：地形/高度场作为多物理场耦合的基础设施，其结构设计需预留多求解器兼容性，避免后续重复改造。

### ⚙️ 性能/架构优化
6/10-Move author-maintained scenarios into playgrounds（e29c088）
  - 评分：6/10
  - 一句话总结：将作者维护的场景迁入 playgrounds，并补充依赖分层检查与边界测试脚本。
  - 提交时间：2026-09-25
  - 变更规模：+201 / -22
  - 提交者：Wei Wu
  - 解决的问题：作者维护场景与核心代码边界不清，示例与私有模块耦合，影响仓库结构清晰度与依赖分层。
  - 产品启示：通过目录边界与自动化依赖检查脚本约束示例与核心代码的耦合，是控制仓库长期可维护性的有效手段。

6/10-Use public cloth APIs and refresh heightfield documentation（e098be0）
  - 评分：6/10
  - 一句话总结：改用公共布料 API 并刷新高度场文档，减少对内部实现的直接依赖。
  - 提交时间：2026-09-25
  - 变更规模：+378 / -90
  - 提交者：Wei Wu
  - 解决的问题：布料构建与运行时仍依赖内部接口，文档与最新高度场结构不同步。
  - 产品启示：推动内部模块统一走公共 API，并同步刷新文档，可降低接口变更带来的连锁破坏，提升对外一致性。

### 🧰 Bug修复 / 其他
- 本周无对应高价值提交。
