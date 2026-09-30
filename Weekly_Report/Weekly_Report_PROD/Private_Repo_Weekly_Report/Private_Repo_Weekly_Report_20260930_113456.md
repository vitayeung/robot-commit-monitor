# WanPhys Weekly Report (2026-09-30 11:34:56)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-30 11:34:56
- 统计截止: 2026-09-30 11:34:56
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

- 5/10-test(perf): restore fluid jet and surface tension manifests（9816b90）
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
本周（2026-09-25）的更新高度延续了仓库在 9 月“收敛与工程化”的长期趋势，并进一步强化了“求解器矩阵扩张 + 确定性回归 + 公共 API 稳定化”三条主线。PeriFEM 求解器的引入与公开 API 完成（dbaaceb、53f9ca1）标志着软体求解栈从旧 vbd_soft_body 向新架构的正式迁移，属于破坏性变更，与基线中“求解器收敛到公共 API 与 deterministic model 抽象”的预测方向一致。同时，5f332cb 与 ed18394 为 VBD/Projective Cloth 及 Newton 求解器加入确定性模型与回归模式，直接呼应了 2026-07 起建立的数值回归与性能框架，说明可复现性建设正从框架搭建走向求解器级覆盖。heightfield 结构扩展（1778c24）延续了 8 月以来地形与颗粒能力增强的趋势，而 e29c088、e098be0 则延续了示例解耦、公开 API 使用与文档刷新的工程化方向。整体看，本周并未偏离长期趋势，而是将 9 月集中爆发的集成工作推向 API 收口与回归验证阶段，风险点仍在于破坏性变更与大规模重构后的行为漂移。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-feat: add deterministic model to newton solvers: vbd & style3d; feat: add regression tests for newton and wanphys vbd & style3d(projective cloth) solvers.（5f332cb）
  - 评分：5/10
  - 一句话总结：为 Newton 求解器（VBD 与 Style3D）加入确定性模型，并补充 Newton 与 WanPhys VBD/Style3D（Projective Cloth）求解器的回归测试。
  - 提交时间：2026-09-25
  - 变更规模：+18986 / -0
  - 提交者：dreliveam
  - 解决的问题：求解器输出缺乏确定性保障，难以进行可复现的数值对比与回归验证。
  - 产品启示：确定性模型与回归测试是物理仿真产品可信度的基础，应作为求解器发布的标配能力。

8/10-Complete the public PeriFEM solver API（53f9ca1）
  - 评分：8/10
  - 一句话总结：完成 PeriFEM 求解器的公开 API，并同步更新 README 与核心模块。
  - 提交时间：2026-09-25
  - 变更规模：+171 / -85
  - 提交者：Wei Wu
  - 解决的问题：PeriFEM 求解器此前缺乏稳定的公开接口，外部调用方难以集成。
  - 产品启示：公开 API 的收口是求解器从内部实验走向可被外部依赖的关键一步，需配套文档与示例。

8/10-feat: add peri-fem solver (delete old vbd_soft_body solver).（dbaaceb）
  - 评分：8/10
  - 一句话总结：新增 PeriFEM 求解器并删除旧 vbd_soft_body 求解器，属于破坏性变更。
  - 提交时间：2026-09-25
  - 变更规模：+3636 / -1390
  - 提交者：dreliveam
  - 解决的问题：旧 vbd_soft_body 求解器架构陈旧，需要被更统一的 PeriFEM 求解器替代。
  - 产品启示：破坏性替换需提供迁移路径与回归验证，否则旧调用方将面临升级风险。

8/10-feat: add regression mode to vbd/projective cloth and examples.（ed18394）
  - 评分：8/10
  - 一句话总结：为 VBD/Projective Cloth 及示例增加回归模式，提升可复现性验证能力。
  - 提交时间：2026-09-25
  - 变更规模：+7324 / -760
  - 提交者：dreliveam
  - 解决的问题：VBD/Projective Cloth 缺少回归模式，难以在示例层面持续追踪数值退化。
  - 产品启示：将回归模式下沉到示例层，有助于在真实使用场景中及早发现求解器行为漂移。

8/10-feat: update heightfield structure to support more rigid solvers.（1778c24）
  - 评分：8/10
  - 一句话总结：更新 heightfield 结构以支持更多刚体求解器，并扩展 granular 耦合与数据模块。
  - 提交时间：2026-09-25
  - 变更规模：+3501 / -1215
  - 提交者：dreliveam
  - 解决的问题：原有 heightfield 结构对刚体求解器支持有限，限制了地形与刚体耦合场景。
  - 产品启示：地形与颗粒能力是具身智能仿真的重要基础，结构扩展应兼顾多求解器兼容性。

### ⚙️ 性能/架构优化
6/10-Move author-maintained scenarios into playgrounds（e29c088）
  - 评分：6/10
  - 一句话总结：将作者维护的场景迁入 playgrounds，并同步更新 AGENTS、README 与边界检查脚本。
  - 提交时间：2026-09-25
  - 变更规模：+201 / -22
  - 提交者：Wei Wu
  - 解决的问题：作者维护场景与核心示例混杂，边界不清，增加维护与依赖管理成本。
  - 产品启示：通过 playgrounds 隔离实验性场景，有助于保持核心示例的稳定性与依赖清晰度。

6/10-Use public cloth APIs and refresh heightfield documentation（e098be0）
  - 评分：6/10
  - 一句话总结：改用公开布料 API 并刷新 heightfield 文档，降低对内部实现的耦合。
  - 提交时间：2026-09-25
  - 变更规模：+378 / -90
  - 提交者：Wei Wu
  - 解决的问题：示例与构建器仍依赖非公开布料接口，文档与最新 heightfield 结构不同步。
  - 产品启示：推动公开 API 使用与文档同步，是降低外部集成门槛与维护成本的关键工程实践。

### 🧰 Bug修复 / 其他
- 本周无对应提交。
