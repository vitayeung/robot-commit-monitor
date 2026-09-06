# WanPhys Weekly Report (2026-09-07 07:02:37)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-07 07:02:37
- 分析窗口: 最近 7 天
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 6/10-Align benchmark examples and performance manifest set（2f52bb9）
  - 提交者：FYTalon
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/basic/example_basic_urdf.py
  - 新增：wanphys/examples/cloth/_kinematic_robot.py
  - 修改：wanphys/examples/cloth/_style3d_assets.py
  - 修改：wanphys/examples/cloth/example_cloth_bending.py
  - 修改：wanphys/examples/cloth/example_cloth_franka.py
  - 修改：wanphys/examples/cloth/example_cloth_h1.py
  - 修改：wanphys/examples/cloth/example_cloth_hanging.py
  - 修改：wanphys/examples/cloth/example_cloth_style3d.py
  - 修改：wanphys/examples/cloth/example_cloth_twist.py
  - 删除：wanphys/examples/references/wanperf600_manifests/fluid.grid-liquid.json
  - 修改：wanphys/examples/robot/example_robot_anymal_d.py
  - 修改：wanphys/examples/robot/example_robot_g1.py
  - 修改：wanphys/examples/robot/example_robot_h1.py
  - 修改：wanphys/examples/robot/example_robot_humanoid.py
  - 修改：wanphys/examples/robot/example_robot_policy.py
  - 修改：wanphys/examples/selection/example_selection_articulations.py
  - 修改：wanphys/examples/selection/example_selection_materials.py
  - 修改：wanphys/examples/sensors/example_sensor_contact.py

- 5/10-Align cloth counterparts on projective dynamics（6659cae）
  - 提交者：FYTalon
  - 提交时间：2026-09-03
  - 新增：wanphys/examples/cloth/_style3d_assets.py
  - 修改：wanphys/examples/cloth/example_cloth_franka.py
  - 修改：wanphys/examples/cloth/example_cloth_h1.py
  - 修改：wanphys/examples/cloth/example_cloth_style3d.py

- 5/10-Align benchmark scenarios with deterministic graph paths（88abced）
  - 提交者：FYTalon
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/cloth/example_cloth_franka.py
  - 修改：wanphys/examples/cloth/example_cloth_h1.py
  - 修改：wanphys/examples/robot/example_robot_anymal_c_walk.py
  - 修改：wanphys/examples/robot/example_robot_anymal_d.py
  - 修改：wanphys/examples/robot/example_robot_g1.py
  - 修改：wanphys/examples/robot/example_robot_h1.py
  - 修改：wanphys/examples/robot/example_robot_humanoid.py
  - 修改：wanphys/examples/robot/example_robot_policy.py
  - 修改：wanphys/examples/sensors/example_sensor_contact.py

- 6/10-chore(examples): separate 600-second performance manifests（2d8262b）
  - 提交者：FYTalon
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/references/manifests/rigid.basic-shapes.xpbd.json
  - 新增：wanphys/examples/references/manifests/soft.vbd-cloth-hanging.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/basic.example_basic_joints.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/basic.example_basic_pendulum.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/basic.example_basic_shapes.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/basic.example_basic_urdf.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/basic.example_basic_viewer.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_bending.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_franka.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_h1.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_hanging.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_style3d.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_twist.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.dfsph-dam-break.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-apic.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-basic.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-complex-model.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-liquid-coupling.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-liquid-robot.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-liquid.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-mpm-liquid-coupling.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-mpm.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-resolution-particle.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-resolution-voxel.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.grid-sparse.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.particle-emitter.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.pbf-coupling-dam.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.pbf-coupling-float.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.pbf-dam-break.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.pbf-emitter-corals.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-coupling-dam.json
  - 新增：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-coupling-float.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-dam-break.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_anymal_c_walk.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_anymal_d.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_cartpole.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_g1.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_h1.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_humanoid.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_policy.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/robot.example_robot_ur10.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/selection.example_selection_articulations.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/selection.example_selection_cartpole.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/selection.example_selection_materials.json
  - 重命名：wanphys/examples/references/wanperf600_manifests/sensors.example_sensor_contact.json
  - 新增：wanphys/examples/rigid_basic_shapes.py
  - 新增：wanphys/examples/soft/vbd_cloth_hanging.py

- 8/10-feat(examples): organize benchmark scenario counterparts（ce3dcaa）
  - 提交者：FYTalon
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/README.md
  - 新增：wanphys/examples/basic/__init__.py
  - 新增：wanphys/examples/basic/example_basic_joints.py
  - 新增：wanphys/examples/basic/example_basic_pendulum.py
  - 重命名：wanphys/examples/basic/example_basic_shapes.py
  - 新增：wanphys/examples/basic/example_basic_urdf.py
  - 新增：wanphys/examples/basic/example_basic_viewer.py
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/cloth/__init__.py
  - 重命名：wanphys/examples/cloth/example_cloth_bending.py
  - 新增：wanphys/examples/cloth/example_cloth_franka.py
  - 新增：wanphys/examples/cloth/example_cloth_h1.py
  - 重命名：wanphys/examples/cloth/example_cloth_hanging.py
  - 新增：wanphys/examples/cloth/example_cloth_style3d.py
  - 重命名：wanphys/examples/cloth/example_cloth_twist.py
  - 新增：wanphys/examples/fluids/__init__.py
  - 重命名：wanphys/examples/fluids/fluid_dfsph_dam_break.py
  - 重命名：wanphys/examples/fluids/fluid_dfsph_diff_skip_stone.py
  - 重命名：wanphys/examples/fluids/fluid_dfsph_modern_block.py
  - 重命名：wanphys/examples/fluids/fluid_dfsph_non_newtonian_jet.py
  - 重命名：wanphys/examples/fluids/fluid_dfsph_surface_tension_akinci2013.py
  - 重命名：wanphys/examples/fluids/fluid_dfsph_surface_tension_jeske2023.py
  - 重命名：wanphys/examples/fluids/fluid_grid_apic.py
  - 重命名：wanphys/examples/fluids/fluid_grid_basic.py
  - 重命名：wanphys/examples/fluids/fluid_grid_complex_model.py
  - 重命名：wanphys/examples/fluids/fluid_grid_liquid.py
  - 重命名：wanphys/examples/fluids/fluid_grid_liquid_coupling.py
  - 重命名：wanphys/examples/fluids/fluid_grid_liquid_robot.py
  - 重命名：wanphys/examples/fluids/fluid_grid_mpm.py
  - 重命名：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 重命名：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py
  - 重命名：wanphys/examples/fluids/fluid_grid_mpm_liquid_coupling.py
  - 重命名：wanphys/examples/fluids/fluid_grid_resolution_particle.py
  - 重命名：wanphys/examples/fluids/fluid_grid_resolution_voxel.py
  - 重命名：wanphys/examples/fluids/fluid_grid_sparse.py
  - 重命名：wanphys/examples/fluids/fluid_particle_emitter.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_coupling_dam.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_coupling_float.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_dam_break.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_emitter_corals.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_modern_block.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_non_newtonian_jet.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_surface_tension_akinci2013.py
  - 重命名：wanphys/examples/fluids/fluid_pbf_surface_tension_jeske2023.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_coupling_dam.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_coupling_float.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_cross_modern_block.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_dam_break.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_diff_height.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_modern_block.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_non_newtonian_jet.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_rigid_coupling_modern_block.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_surface_tension_akinci2013.py
  - 重命名：wanphys/examples/fluids/fluid_wcsph_surface_tension_jeske2023.py
  - 新增：wanphys/examples/references/manifests/basic.example_basic_joints.json
  - 新增：wanphys/examples/references/manifests/basic.example_basic_pendulum.json
  - 新增：wanphys/examples/references/manifests/basic.example_basic_shapes.json
  - 新增：wanphys/examples/references/manifests/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/manifests/basic.example_basic_viewer.json
  - 新增：wanphys/examples/references/manifests/cloth.example_cloth_bending.json
  - 新增：wanphys/examples/references/manifests/cloth.example_cloth_franka.json
  - 新增：wanphys/examples/references/manifests/cloth.example_cloth_h1.json
  - 新增：wanphys/examples/references/manifests/cloth.example_cloth_hanging.json
  - 新增：wanphys/examples/references/manifests/cloth.example_cloth_style3d.json
  - 新增：wanphys/examples/references/manifests/cloth.example_cloth_twist.json
  - 新增：wanphys/examples/references/manifests/fluid.dfsph-dam-break.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-apic.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-basic.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-complex-model.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-liquid-coupling.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-liquid-robot.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-liquid.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-mpm-liquid-coupling.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-mpm.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-resolution-particle.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-resolution-voxel.json
  - 新增：wanphys/examples/references/manifests/fluid.grid-sparse.json
  - 新增：wanphys/examples/references/manifests/fluid.particle-emitter.json
  - 新增：wanphys/examples/references/manifests/fluid.pbf-coupling-dam.json
  - 新增：wanphys/examples/references/manifests/fluid.pbf-coupling-float.json
  - 新增：wanphys/examples/references/manifests/fluid.pbf-dam-break.json
  - 新增：wanphys/examples/references/manifests/fluid.pbf-emitter-corals.json
  - 新增：wanphys/examples/references/manifests/fluid.wcsph-coupling-dam.json
  - 修改：wanphys/examples/references/manifests/fluid.wcsph-coupling-float.json
  - 新增：wanphys/examples/references/manifests/fluid.wcsph-dam-break.json
  - 删除：wanphys/examples/references/manifests/rigid.basic-shapes.xpbd.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_humanoid.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_policy.json
  - 新增：wanphys/examples/references/manifests/robot.example_robot_ur10.json
  - 重命名：wanphys/examples/references/manifests/selection.example_selection_articulations.json
  - 重命名：wanphys/examples/references/manifests/selection.example_selection_cartpole.json
  - 重命名：wanphys/examples/references/manifests/selection.example_selection_materials.json
  - 新增：wanphys/examples/references/manifests/sensors.example_sensor_contact.json
  - 删除：wanphys/examples/references/manifests/soft.vbd-cloth-hanging.json
  - 删除：wanphys/examples/rigid_pendulum.py

- 7/10-Add native articulation selection views（1e12e34）
  - 提交者：FYTalon
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/references/manifests/selection.articulations.mujoco.json
  - 新增：wanphys/examples/references/manifests/selection.cartpole.mujoco.json
  - 新增：wanphys/examples/references/manifests/selection.materials.mujoco.json
  - 新增：wanphys/examples/selection/__init__.py
  - 新增：wanphys/examples/selection/example_selection_articulations.py
  - 新增：wanphys/examples/selection/example_selection_cartpole.py
  - 新增：wanphys/examples/selection/example_selection_materials.py

- 7/10-Complete scenario and surface-tension test migration（bd9e4da）
  - 提交者：Wei Wu
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/fluid_dfsph_diff_skip_stone.py
  - 删除：wanphys/examples/references/manifests/fluid.wcsph-surface-tension-benchmarks.json

- 7/10-Remove parked particle-fluid examples（d85720d）
  - 提交者：Wei Wu
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 删除：wanphys/examples/fluid_dfsph_diff_skip_stone.py
  - 删除：wanphys/examples/fluid_legacy/__init__.py
  - 删除：wanphys/examples/fluid_legacy/fluid_dfsph_dam_break.py
  - 删除：wanphys/examples/fluid_legacy/fluid_dfsph_diff_skip_stone.py
  - 删除：wanphys/examples/fluid_legacy/fluid_dfsph_surface_tension_benchmarks.py
  - 删除：wanphys/examples/fluid_legacy/fluid_particle_emitter.py
  - 删除：wanphys/examples/fluid_legacy/fluid_pbf_coupling_dam.py
  - 删除：wanphys/examples/fluid_legacy/fluid_pbf_coupling_float.py
  - 删除：wanphys/examples/fluid_legacy/fluid_pbf_dam_break.py
  - 删除：wanphys/examples/fluid_legacy/fluid_pbf_emitter_corals.py
  - 删除：wanphys/examples/fluid_legacy/fluid_pbf_surface_tension_benchmarks.py
  - 删除：wanphys/examples/fluid_legacy/fluid_wcsph_coupling_dam.py
  - 删除：wanphys/examples/fluid_legacy/fluid_wcsph_coupling_float.py
  - 删除：wanphys/examples/fluid_legacy/fluid_wcsph_dam_break.py
  - 删除：wanphys/examples/fluid_legacy/fluid_wcsph_non_newtonian_jet_buckling.py
  - 删除：wanphys/examples/fluid_legacy/fluid_wcsph_surface_tension_benchmarks.py

- 7/10-Complete the unified WCSPH rheology migration（fbb987d）
  - 提交者：Wei Wu
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/fluid_wcsph_cross_modern_block.py

- 6/10-Keep the scenario catalog synchronized（33f7c9b）
  - 提交者：Wei Wu
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py

- 5/10-[USTB] fix some bugs（c66cfb5）
  - 提交者：Zihang Zhong
  - 提交时间：2026-09-03
  - 修改：wanphys/examples/fluid_dfsph_dam_break.py
  - 修改：wanphys/examples/fluid_dfsph_non_newtonian_jet.py
  - 修改：wanphys/examples/fluid_dfsph_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluid_dfsph_surface_tension_jeske2023.py
  - 修改：wanphys/examples/fluid_pbf_dam_break.py
  - 修改：wanphys/examples/fluid_pbf_emitter_corals.py
  - 修改：wanphys/examples/fluid_pbf_non_newtonian_jet.py
  - 修改：wanphys/examples/fluid_pbf_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluid_pbf_surface_tension_jeske2023.py
  - 修改：wanphys/examples/fluid_wcsph_dam_break.py
  - 修改：wanphys/examples/fluid_wcsph_non_newtonian_jet.py
  - 修改：wanphys/examples/fluid_wcsph_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluid_wcsph_surface_tension_jeske2023.py

- 9/10-[USTB] Surface tension and non-Newtonian fluid implementation and examples（3176d05）
  - 提交者：Zihang Zhong
  - 提交时间：2026-09-03
  - 新增：wanphys/examples/fluid_dfsph_non_newtonian_jet.py
  - 新增：wanphys/examples/fluid_dfsph_surface_tension_akinci2013.py
  - 删除：wanphys/examples/fluid_dfsph_surface_tension_benchmarks.py
  - 新增：wanphys/examples/fluid_dfsph_surface_tension_jeske2023.py
  - 重命名：wanphys/examples/fluid_pbf_non_newtonian_jet.py
  - 新增：wanphys/examples/fluid_pbf_surface_tension_akinci2013.py
  - 删除：wanphys/examples/fluid_pbf_surface_tension_benchmarks.py
  - 新增：wanphys/examples/fluid_pbf_surface_tension_jeske2023.py
  - 新增：wanphys/examples/fluid_wcsph_non_newtonian_jet.py
  - 新增：wanphys/examples/fluid_wcsph_surface_tension_akinci2013.py
  - 删除：wanphys/examples/fluid_wcsph_surface_tension_benchmarks.py
  - 新增：wanphys/examples/fluid_wcsph_surface_tension_jeske2023.py

- 6/10-Add deterministic conveyor regression coverage（461a9b0）
  - 提交者：Wei Wu
  - 提交时间：2026-09-02
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/references/manifests/rigid.basic-conveyor.deterministic-xpbd.json
  - 新增：wanphys/examples/rigid_basic_conveyor_deterministic.py

#### 📊 提交分析
- 本周总提交: 16 条
- 高价值提交（≥6分）: 12 条
- 代码更新规模: +37269 / -28087 行
- 主要贡献者: Wei Wu, FYTalon, Zihang Zhong, Lei Lan

## 📈 趋势点评

本周（2026-09-02 ~ 2026-09-03）的更新高度契合仓库在2026年8月至9月间确立的“性能清单对齐与确定性求解器实现”阶段主线，并进一步加速推进。从长期趋势看，本周提交集中体现了三大延续性特征：其一，**确定性求解器与回归覆盖**（98d86c7、461a9b0）延续了9月初确立的确定性仿真方向，与基线中“提升仿真可复现性”的目标一致；其二，**性能清单与基准框架的深化**（2d8262b、2f52bb9、ce3dcaa）直接承接了8月建立的数值回归与性能工作流（f8b2d45），将性能管理从“建立框架”推进到“清单分离与对齐”的精细化阶段；其三，**流体求解器的大规模重构与迁移**（3176d05、498e7fa、fbb987d、bd9e4da、d85720d）延续了2026年6月以来对流体模块（非牛顿流体、表面张力、WCSPH）的持续深耕，但本周的迁移力度显著加大，涉及大量文件删除与重组，体现了从“功能验证”到“架构收敛”的工程化决心。值得注意的是，本周提交集中在9月2日至3日两天内完成，且多由核心维护者（Wei Wu、FYTalon）主导，提交规模普遍较大（多个提交超过千行变更），表明项目正处于一次集中的架构整理窗口期，而非渐进式迭代——这与2026年5月的大规模功能扩展（78次提交）形成呼应，但方向从“做加法”转向了“做整理与对齐”。

---

## 📌 关键更新解析

### 🌟 新功能/特性

9/10-Add atomic-free deterministic solver implementations（98d86c7）
- **评分**：9/10
- **一句话总结**：新增原子自由（atomic-free）确定性求解器实现，为仿真可复现性奠定核心基础。
- **提交时间**：2026-09-02
- **变更规模**：+15668 / -72
- **提交者**：Lei Lan
- **解决的问题**：传统求解器中原子操作会导致并行计算下的非确定性结果，影响仿真可复现性。该提交通过消除原子操作，确保同一输入在不同运行环境下产生完全一致的输出，对依赖精确复现的工业应用和学术研究至关重要。
- **产品启示**：确定性是仿真工具从“研究原型”走向“工程可信赖产品”的关键门槛。原子自由求解器将吸引对可复现性有硬性要求的用户群体（如机器人策略训练、自动驾驶仿真验证），可作为产品差异化的核心卖点。

9/10-[USTB] Surface tension and non-Newtonian fluid implementation and examples（3176d05）
- **评分**：9/10
- **一句话总结**：实现表面张力与非牛顿流体算法，并配套完整示例，大幅扩展流体物理覆盖范围。
- **提交时间**：2026-09-03
- **变更规模**：+5170 / -2763
- **提交者**：Zihang Zhong
- **解决的问题**：此前仓库虽在2026年6月新增非牛顿流体算法（2e08f8d）并修复表面张力问题（e296515），但缺乏系统性的实现与示例支撑。该提交补齐了表面张力模型与多种非牛顿流体本构的完整实现，使流体模块从“可用”迈向“完整”。
- **产品启示**：表面张力与非牛顿流体（如Oldroyd-B、幂律流体）是材料加工、生物流体、食品工业等垂直领域仿真的刚需能力。完整的流体物理覆盖将直接拓宽产品的行业适用面，配合示例降低用户上手门槛。

7/10-Add native articulation selection views（1e12e34）
- **评分**：7/10
- **一句话总结**：新增原生关节选择视图，提升对多关节机器人模型的选择与操控能力。
- **提交时间**：2026-09-03
- **变更规模**：+1803 / -4
- **提交者**：FYTalon
- **解决的问题**：在复杂多关节模型（如四足机器人、人形机器人）中，用户需要精确选择特定关节或连杆进行状态查询、力控或传感器挂载。此前缺乏原生选择视图，用户需依赖外部工具或繁琐的坐标变换。
- **产品启示**：关节级选择能力是机器人仿真工作流中的高频操作，直接关系到用户对复杂装配体的操控效率。该功能将增强WanPhys在机器人仿真场景中的竞争力，尤其对MuJoCo迁移用户具有吸引力。

6/10-Add deterministic conveyor regression coverage（461a9b0）
- **评分**：6/10
- **一句话总结**：新增确定性传送带场景的回归测试，覆盖碰撞与确定性求解器的集成行为。
- **提交时间**：2026-09-02
- **变更规模**：+957 / -54
- **提交者**：Wei Wu
- **解决的问题**：传送带场景涉及刚体碰撞、摩擦与持续驱动力的耦合，是测试确定性求解器在长时间仿真中数值稳定性的理想场景。此前缺乏针对该场景的回归覆盖，无法有效防止确定性求解器的回归。
- **产品启示**：回归测试是保障仿真工具长期可信赖的基石。针对典型工业场景（如传送带分拣）的确定性覆盖，向用户传递了“关键场景已被验证”的信号，有助于建立产品信任度。

### ⚙️ 性能/架构优化

8/10-feat(examples): organize benchmark scenario counterparts（ce3dcaa）
- **评分**：8/10
- **一句话总结**：大规模重组示例目录，为每个基准场景建立对应示例，统一示例与基准的组织结构。
- **提交时间**：2026-09-03
- **变更规模**：+6528 / -3791
- **提交者**：FYTalon
- **解决的问题**：此前基准场景与示例代码分散在不同目录，导致开发者难以将性能基准映射到具体示例，也增加了维护成本。该提交通过系统化重组，使每个基准场景都有对应的可运行示例，提升代码库的可导航性。
- **产品启示**：示例与基准的统一组织是“开发者体验”的重要组成。清晰的目录结构能显著降低新贡献者的上手成本，同时为自动化性能测试提供稳定的入口，是工程化成熟度的重要标志。

7/10-Complete scenario and surface-tension test migration（bd9e4da）
- **评分**：7/10
- **一句话总结**：完成场景目录与表面张力测试的迁移，使测试与新的场景组织架构对齐。
- **提交时间**：2026-09-03
- **变更规模**：+1286 / -921
- **提交者**：Wei Wu
- **解决的问题**：随着场景目录的持续演进（如ce3dcaa的重组），部分表面张力相关测试仍引用旧路径，导致测试与代码结构脱节。该提交完成迁移，确保测试套件与最新架构保持一致。
- **产品启示**：测试与架构的同步演进是防止技术债积累的关键。及时的测试迁移保证了持续集成（CI）的有效性，避免因路径失效导致的“假红”或“假绿”，维护了质量门禁的可信度。

7/10-Complete the unified WCSPH rheology migration（fbb987d）
- **评分**：7/10
- **一句话总结**：完成统一WCSPH流变学迁移，将多种非牛顿流体模型整合到统一求解框架中。
- **提交时间**：2026-09-03
- **变更规模**：+583 / -351
- **提交者**：Wei Wu
- **解决的问题**：此前不同非牛顿流体模型（Oldroyd-B、幂律等）可能分散在不同代码路径中，导致维护困难和行为不一致。该提交将其统一到WCSPH框架下，确保不同流变模型共享同一套求解核心。
- **产品启示**：统一求解框架降低了新增流变模型的边际成本，使产品能够快速响应不同行业对新材料模型的需求。对用户而言，统一的API意味着更短的学习曲线和更可预测的仿真行为。

7/10-Remove parked particle-fluid examples（d85720d）
- **评分**：7/10
- **一句话总结**：删除大量遗留的粒子流体示例（净删除超万行），清理代码库中的“停放”资产。
- **提交时间**：2026-09-03
- **变更规模**：+23 / -10292
- **提交者**：Wei Wu
- **解决的问题**：随着流体模块向统一WCSPH框架迁移（fbb987d），大量旧版粒子流体示例已不再适用或与新架构冲突。保留这些“停放”示例会增加维护负担并误导用户。
- **产品启示**：果断删除过时代码是保持代码库健康的重要决策。虽然短期内提交规模看似“倒退”，但长期看减少了维护成本、降低了用户困惑，为后续重构腾出了清晰的演进空间。

6/10-Keep the scenario catalog synchronized（33f7c9b）
- **评分**：6/10
- **一句话总结**：新增预提交钩子与检查脚本，确保场景目录始终与示例代码保持同步。
- **提交时间**：2026-09-03
- **变更规模**：+285 / -26
- **提交者**：Wei Wu
- **解决的问题**：场景目录（catalog）是示例与基准的索引，但开发者新增或删除示例时容易忘记更新目录，导致目录与实际代码脱节。该提交通过自动化检查在提交前拦截不一致。
- **产品启示**：自动化一致性检查是工程规范的“最后一道防线”。预提交钩子将质量保障左移到开发阶段，减少代码评审的琐碎负担，让审查者聚焦于实质性逻辑而非机械性遗漏。

6/10-Align benchmark examples and performance manifest set（2f52bb9）
- **评分**：6/10
- **一句话总结**：对齐基准示例与性能清单集合，确保每个基准示例都有对应的性能预期记录。
- **提交时间**：2026-09-03
- **变更规模**：+665 / -519
- **提交者**：FYTalon
- **解决的问题**：性能清单（manifest）记录了各示例的预期性能指标，但部分基准示例缺少对应清单，或清单与示例实际行为不匹配，导致性能回归检测出现盲区。
- **产品启示**：性能清单的完整对齐是自动化性能回归检测的前提。只有每个基准示例都有明确的性能基线，才能在代码变更后自动识别性能退化，为产品性能提供持续保障。

6/10-chore(examples): separate 600-second performance manifests（2d8262b）
- **评分**：6/10
- **一句话总结**：将运行时长超过600秒的重型性能清单分离到独立目录，与常规性能清单区分管理。
- **提交时间**：2026-09-03
- **变更规模**：+802 / -61
- **提交者**：FYTalon
- **解决的问题**：部分基准场景运行时间极长（超过10分钟），若与常规基准混在一起，会拖慢日常CI流水线，导致开发者不愿频繁运行完整性能测试。
- **产品启示**：分层级的性能测试策略（快速/慢速分离）是大型仿真项目的实用工程实践。它允许开发者在日常迭代中快速验证性能，同时在发布前运行完整清单，兼顾效率与覆盖。

### 🧰 Bug修复 / 其他

8/10-Fix Oldroyd-B constitutive state ownership（498e7fa）
- **评分**：8/10
- **一句话总结**：修复Oldroyd-B本构模型的状态所有权问题，确保状态在求解过程中被正确管理和传递。
- **提交时间**：2026-09-03
- **变更规模**：+739 / -53
- **提交者**：Wei Wu
- **解决的问题**：Oldroyd-B作为粘弹性流体模型，其本构状态（如应力张量）需要在求解步骤间正确持有和更新。此前存在所有权模糊的问题，可能导致状态被意外释放或错误共享，引发数值不稳定或内存错误。
- **产品启示**：状态管理是物理仿真引擎中最容易出错也最难调试的部分。该修复虽属Bug范畴，但直接关系到非牛顿流体仿真的数值稳定性——这是用户对仿真结果可信度的核心诉求。稳定的状态管理也为未来支持更复杂的本构模型（如粘弹塑性）奠定基础。
