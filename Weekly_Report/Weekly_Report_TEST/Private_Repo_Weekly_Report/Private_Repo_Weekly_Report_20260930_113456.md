# WanPhys Weekly Report (2026-09-30 11:34:56)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-30 11:34:56
- 统计截止: 2026-09-30 11:34:56
- 分析窗口: 2026-09-21 07:02:00 +0800 至 2026-09-30 11:34:56 +0800（左闭右开）
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

- 9/10-feat: add regression mode to vbd/projective cloth and examples.（ed18394）
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

- 8/10-remove pre ccd and mtd, update resweep and motion check（40e28c5）
  - 提交者：huangtaikai
  - 提交时间：2026-09-22
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 2/10-docs(regression): clarify compared and restore-only state（97b3ba2）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/wanreg_fluid_onestep_manifests/README.md
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/README.md

- 6/10-feat(regression): track fluid keyframe pins and document workflows（4833758）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/keyframe_store.py
  - 修改：wanphys/examples/references/pinning.py
  - 修改：wanphys/examples/references/wanreg_fluid_onestep_manifests/README.md
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/README.md

- 4/10-test(regression): bound DFSPH keyframe velocity noise（e785154）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/wanreg_fluid_onestep_manifests/README.md
  - 修改：wanphys/examples/references/wanreg_fluid_onestep_manifests/fluids.fluid_dfsph_non_newtonian_jet.json

- 6/10-feat(regression): add native fluid keyframe mean pins（5911d9d）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 新增：wanphys/examples/references/keyframe.py
  - 新增：wanphys/examples/references/keyframe_store.py
  - 修改：wanphys/examples/references/manifests.py
  - 新增：wanphys/examples/references/wanreg_fluid_onestep_manifests/README.md
  - 新增：wanphys/examples/references/wanreg_fluid_onestep_manifests/fluids.fluid_dfsph_non_newtonian_jet.json
  - 新增：wanphys/examples/references/wanreg_fluid_onestep_manifests/fluids.fluid_pbf_non_newtonian_jet.json
  - 新增：wanphys/examples/references/wanreg_fluid_onestep_manifests/fluids.fluid_wcsph_non_newtonian_jet.json

- 3/10-test(regression): remove deferred one-step manifests（8394216）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/README.md
  - 删除：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_viewer.json
  - 删除：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_franka.json
  - 删除：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_h1.json
  - 删除：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_style3d.json
  - 删除：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_twist.json
  - 删除：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_g1.json

- 4/10-test(regression): set reviewed rigid one-step parity tolerances（127a64f）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/README.md
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_shapes.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_urdf.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_c_walk.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_d.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_h1.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_humanoid.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_ur10.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_articulations.json

- 4/10-fix(examples): synchronize authored MuJoCo parameters at initialization（e516bd2）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/robot/example_robot_h1.py
  - 修改：wanphys/examples/selection/example_selection_materials.py

- 3/10-fix(examples): preserve UR10 asset gravity（8460dfd）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/robot/example_robot_ur10.py

- 3/10-test(regression): relax full-frame cloth parity tolerances（a0c0ac2）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/one_step.py
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_bending.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_franka.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_h1.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_hanging.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_style3d.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_twist.json

- 3/10-fix(examples): keep cloth Franka finger drives independent（ce3cfa9）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/cloth/example_cloth_franka.py

- 3/10-fix(examples): align Style3D frame contact scheduling（db93cc2）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/cloth/example_cloth_style3d.py

- 3/10-fix(examples): remove obsolete angular passive-gain compensation（7afd04c）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/selection/example_selection_articulations.py
  - 修改：wanphys/examples/selection/example_selection_materials.py

- 4/10-fix(robot): observe root COM velocity in pretrained policies（6861023）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/robot/example_robot_anymal_c_walk.py
  - 修改：wanphys/examples/robot/example_robot_policy.py

- 3/10-fix(examples): align materials runtime angular damping with reference（403416d）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/selection/example_selection_materials.py

- 3/10-fix(regression): use explicit scenario lifecycle after dev rebase（3bce144）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_articulations.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_cartpole.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/sensors.example_sensor_contact.json

- 5/10-fix(regression): normalize body velocities for opt-in MuJoCo comparisons（5ca01b2）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/references/probes.py

- 8/10-feat(regression): add configurable Newton-initialized one-step comparisons（9e7ca94）
  - 提交者：FYTalon
  - 提交时间：2026-09-21
  - 修改：wanphys/examples/basic/example_basic_joints.py
  - 修改：wanphys/examples/basic/example_basic_pendulum.py
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/basic/example_basic_urdf.py
  - 修改：wanphys/examples/cloth/example_cloth_franka.py
  - 修改：wanphys/examples/cloth/example_cloth_h1.py
  - 修改：wanphys/examples/cloth/example_cloth_hanging.py
  - 修改：wanphys/examples/cloth/example_cloth_style3d.py
  - 修改：wanphys/examples/cloth/example_cloth_twist.py
  - 修改：wanphys/examples/references/__init__.py
  - 修改：wanphys/examples/references/execution.py
  - 修改：wanphys/examples/references/manifests.py
  - 修改：wanphys/examples/references/manifests/rigid.basic-shapes.xpbd.json
  - 修改：wanphys/examples/references/observation.py
  - 新增：wanphys/examples/references/one_step.py
  - 修改：wanphys/examples/references/performance.py
  - 修改：wanphys/examples/references/probes.py
  - 修改：wanphys/examples/references/registry.py
  - 修改：wanphys/examples/references/sources.py
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_joints.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_pendulum.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_shapes.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_viewer.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_bending.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_franka.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_h1.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_hanging.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_style3d.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_twist.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_humanoid.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_ur10.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_articulations.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_cartpole.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_materials.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/sensors.example_sensor_contact.json
  - 修改：wanphys/examples/robot/example_robot_cartpole.py
  - 修改：wanphys/examples/robot/example_robot_g1.py
  - 修改：wanphys/examples/robot/example_robot_h1.py
  - 修改：wanphys/examples/robot/example_robot_humanoid.py
  - 修改：wanphys/examples/robot/example_robot_policy.py
  - 修改：wanphys/examples/robot/example_robot_ur10.py
  - 修改：wanphys/examples/selection/example_selection_articulations.py
  - 修改：wanphys/examples/selection/example_selection_materials.py
  - 修改：wanphys/examples/sensors/example_sensor_contact.py

#### 📊 提交分析
- 本周总提交: 38 条
- 高价值提交（≥6分）: 12 条
- 代码更新规模: +53740 / -10734 行
- 主要贡献者: FYTalon, Wei Wu, dreliveam, huangtaikai

## 📈 趋势点评
本周高价值提交高度集中于 2026-09-21 至 2026-09-25 这一窗口，延续了仓库自 2026-07 以来“由功能扩张转向确定性收敛”的主线：一方面通过 `5f332cb`、`ed18394`、`9e7ca94`、`5911d9d`、`4833758` 等提交，把确定性模型、回归模式、可配置单步对比与流体关键帧固定点系统性地铺进 VBD、Style3D、projective cloth 与流体求解器，使数值回归从零散验证升级为可配置、可追踪的基础设施；另一方面通过 `dbaaceb`、`53f9ca1` 完成 PeriFEM 求解器替换旧 vbd_soft_body 并公开 API，配合 `1778c24` 扩展 heightfield 结构，继续推进求解器体系化与地形能力扩展。同时 `40e28c5` 删除 pre-CCD 与 MTD、`1c308ba` 复用共享碰撞与摩擦辅助、`e29c088` 将作者维护场景迁入 playgrounds、`e098be0` 采用公共 cloth API，体现出碰撞管线精简、模块解耦与接口收敛的架构治理意图。整体看，本周并未偏离长期趋势，而是把 2026-09 峰值月的“确定性 + 回归 + 求解器统一”方向进一步压实，性能/架构优化类提交虽数量不多但多为删减与复用型重构，风险在于 CCD 与求解器接口在短期内连续变更，向后兼容与行为一致性仍需回归框架持续兜底。

## 📌 关键更新解析

### 🌟 新功能/特性

9/10-feat: add deterministic model to newton solvers: vbd & style3d; feat: add regression tests for newton and wanphys vbd & style3d(projective cloth) solvers.（5f332cb）
  - 评分：9/10
  - 一句话总结：为 Newton 的 VBD 与 Style3D 求解器引入确定性模型，并同步补齐 Newton 与 WanPhys 两侧 VBD/Style3D（projective cloth）求解器的回归测试。
  - 提交时间：2026-09-25
  - 变更规模：+18986 / -0
  - 提交者：dreliveam
  - 解决的问题：此前求解器缺少确定性执行模型与对应回归验证，跨后端、跨运行结果难以复现和比对。
  - 产品启示：确定性求解器与回归测试绑定交付，可作为仿真结果可复现性的核心卖点，也为后续 CI 门禁与数值基准提供基础。

9/10-feat: add regression mode to vbd/projective cloth and examples.（ed18394）
  - 评分：9/10
  - 一句话总结：为 VBD/projective cloth 增加回归模式并配套示例，使布料求解可在回归场景下稳定复现。
  - 提交时间：2026-09-25
  - 变更规模：+7324 / -760
  - 提交者：dreliveam
  - 解决的问题：projective cloth 缺少专门的回归运行模式，碰撞、全局步与局部步等环节难以在回归中保持一致行为。
  - 产品启示：把回归模式下沉到求解器与示例层，有助于用户直接复用官方回归配置，降低数值验证门槛。

8/10-feat(regression): add configurable Newton-initialized one-step comparisons（9e7ca94）
  - 评分：8/10
  - 一句话总结：新增可配置的、以 Newton 初始化的单步对比能力，用于回归中逐帧比对求解行为。
  - 提交时间：2026-09-21
  - 变更规模：+8735 / -118
  - 提交者：FYTalon
  - 解决的问题：回归对比缺少可配置的单步初始化与比对机制，难以定位求解器在单步内的数值差异。
  - 产品启示：可配置单步对比提升了回归诊断粒度，可作为求解器迭代与去 Newton 耦合过程中的安全网。

8/10-Complete the public PeriFEM solver API（53f9ca1）
  - 评分：8/10
  - 一句话总结：完成 PeriFEM 求解器的公开 API，并同步更新 README 与核心导出。
  - 提交时间：2026-09-25
  - 变更规模：+171 / -85
  - 提交者：Wei Wu
  - 解决的问题：PeriFEM 求解器此前接口不完整，外部用户难以通过稳定公共入口调用。
  - 产品启示：公开 API 是求解器生态化的前提，有助于 PeriFEM 被示例、工具链与第三方集成直接采用。

8/10-feat: add peri-fem solver (delete old vbd_soft_body solver).（dbaaceb）
  - 评分：8/10
  - 一句话总结：新增 PeriFEM 求解器并删除旧 vbd_soft_body 求解器，完成软体求解路径的替换。
  - 提交时间：2026-09-25
  - 变更规模：+3636 / -1390
  - 提交者：dreliveam
  - 解决的问题：旧 vbd_soft_body 求解器与新的软体模型/状态抽象不一致，维护成本高且能力受限。
  - 产品启示：以新求解器替换旧实现可统一软体求解抽象，但需关注旧示例与资产的迁移兼容性。

8/10-feat: update heightfield structure to support more rigid solvers.（1778c24）
  - 评分：8/10
  - 一句话总结：更新 heightfield 结构以支持更多刚体求解器，并扩展 granular 耦合与数据模块。
  - 提交时间：2026-09-25
  - 变更规模：+3501 / -1215
  - 提交者：dreliveam
  - 解决的问题：原有 heightfield 结构对刚体求解器支持有限，颗粒与地形耦合能力不足。
  - 产品启示：heightfield 作为地形与颗粒仿真的公共基础，其结构扩展将直接放大刚体、颗粒与地形组合场景的可用性。

6/10-feat(regression): add native fluid keyframe mean pins（5911d9d）
  - 评分：6/10
  - 一句话总结：为原生流体回归新增关键帧均值固定点，用于稳定流体数值对比。
  - 提交时间：2026-09-21
  - 变更规模：+2645 / -8
  - 提交者：FYTalon
  - 解决的问题：流体回归缺少关键帧均值固定机制，长时间仿真中数值漂移难以被稳定捕捉。
  - 产品启示：关键帧固定点让流体回归更具可比性，为流体求解器的持续优化提供可量化锚点。

6/10-feat(regression): track fluid keyframe pins and document workflows（4833758）
  - 评分：6/10
  - 一句话总结：跟踪流体关键帧固定点并补充工作流文档，完善回归流程的可追溯性。
  - 提交时间：2026-09-21
  - 变更规模：+899 / -168
  - 提交者：FYTalon
  - 解决的问题：流体关键帧固定点缺少跟踪与文档说明，回归工作流难以被他人复现。
  - 产品启示：把回归工作流文档化，有助于团队与外部贡献者一致地执行流体数值验证。

### ⚙️ 性能/架构优化

8/10-remove pre ccd and mtd, update resweep and motion check（40e28c5）
  - 评分：8/10
  - 一句话总结：移除 pre-CCD 与 MTD，更新 resweep 与 motion check，精简 CCD 管线。
  - 提交时间：2026-09-22
  - 变更规模：+4221 / -5689
  - 提交者：huangtaikai
  - 解决的问题：pre-CCD 与 MTD 造成 CCD 流程冗余、代码路径复杂，影响可维护性与确定性。
  - 产品启示：CCD 管线精简有利于降低碰撞处理复杂度，但需回归验证确保移除后行为一致。

6/10-Move author-maintained scenarios into playgrounds（e29c088）
  - 评分：6/10
  - 一句话总结：将作者维护的场景迁入 playgrounds，并补充边界检查脚本与文档。
  - 提交时间：2026-09-25
  - 变更规模：+201 / -22
  - 提交者：Wei Wu
  - 解决的问题：作者维护场景与核心示例边界不清，依赖分层与所有权不明确。
  - 产品启示：场景分层有助于区分官方示例与实验性 playground，降低核心仓库耦合与维护负担。

6/10-Reuse shared collision contact and friction helpers（1c308ba）
  - 评分：6/10
  - 一句话总结：在 projective cloth 与 vbd_soft_body 中复用共享的碰撞接触与摩擦辅助函数。
  - 提交时间：2026-09-25
  - 变更规模：+7 / -145
  - 提交者：Wei Wu
  - 解决的问题：碰撞接触与摩擦逻辑在多个软体求解器中重复实现，存在不一致与维护成本。
  - 产品启示：共享辅助函数可统一接触与摩擦语义，减少求解器间行为差异。

6/10-Use public cloth APIs and refresh heightfield documentation（e098be0）
  - 评分：6/10
  - 一句话总结：改用公共 cloth API，并刷新 heightfield 文档。
  - 提交时间：2026-09-25
  - 变更规模：+378 / -90
  - 提交者：Wei Wu
  - 解决的问题：projective cloth 与 vbd_soft_body 构建器仍依赖非公共接口，文档与实现脱节。
  - 产品启示：采用公共 API 有助于冻结接口边界，提升外部用户与示例的可移植性。

### 🧰 Bug修复 / 其他
（本周高价值提交中无对应条目）
