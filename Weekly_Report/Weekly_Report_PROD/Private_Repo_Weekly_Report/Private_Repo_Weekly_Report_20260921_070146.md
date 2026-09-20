# WanPhys Weekly Report (2026-09-21 07:01:46)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-21 07:01:46
- 统计截止: 2026-09-21 07:01:46
- 分析窗口: 最近 7 天（截止上述时间）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 9/10-Remove Domain wrappers and make simulation lifecycle ownership explicit（049df72）
  - 提交者：Wei Wu
  - 提交时间：2026-09-19
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/basic/example_basic_joints.py
  - 修改：wanphys/examples/basic/example_basic_pendulum.py
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/basic/example_basic_urdf.py
  - 修改：wanphys/examples/broad_phase_benchmark.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_dam_break.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_modern_block.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_non_newtonian_jet.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_surface_tension_jeske2023.py
  - 修改：wanphys/examples/fluids/fluid_grid_apic.py
  - 修改：wanphys/examples/fluids/fluid_grid_cirrus.py
  - 修改：wanphys/examples/fluids/fluid_grid_cirrus_render.py
  - 修改：wanphys/examples/fluids/fluid_grid_complex_model.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid_robot.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm.py
  - 修改：wanphys/examples/fluids/fluid_grid_resolution_particle.py
  - 修改：wanphys/examples/fluids/fluid_grid_resolution_voxel.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse_liquid.py
  - 修改：wanphys/examples/fluids/fluid_particle_emitter.py
  - 修改：wanphys/examples/fluids/fluid_pbf_coupling_dam.py
  - 修改：wanphys/examples/fluids/fluid_pbf_coupling_float.py
  - 修改：wanphys/examples/fluids/fluid_pbf_dam_break.py
  - 修改：wanphys/examples/fluids/fluid_pbf_emitter_corals.py
  - 修改：wanphys/examples/fluids/fluid_pbf_modern_block.py
  - 修改：wanphys/examples/fluids/fluid_pbf_non_newtonian_jet.py
  - 修改：wanphys/examples/fluids/fluid_pbf_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluids/fluid_pbf_surface_tension_jeske2023.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_coupling_dam.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_coupling_float.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_cross_modern_block.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_dam_break.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_diff_height.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_modern_block.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_non_newtonian_jet.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_rigid_coupling_modern_block.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_surface_tension_jeske2023.py
  - 修改：wanphys/examples/heightfield/dynamic_heightfield.py
  - 修改：wanphys/examples/heightfield/granular_balls_rigid.py
  - 修改：wanphys/examples/heightfield/granular_hill_bunny_rigid.py
  - 修改：wanphys/examples/heightfield/granular_lunar_surface_random.py
  - 修改：wanphys/examples/heightfield/granular_png_hill_rigid.py
  - 修改：wanphys/examples/heightfield/granular_png_terrain_rigid.py
  - 修改：wanphys/examples/heightfield/lunar_dtm_nac.py
  - 修改：wanphys/examples/references/manifests/fluid.wcsph-coupling-float.json
  - 修改：wanphys/examples/references/manifests/rigid.basic-conveyor.deterministic-xpbd.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.dfsph-dam-break.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.particle-emitter.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.pbf-coupling-dam.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.pbf-coupling-float.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.pbf-dam-break.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.pbf-emitter-corals.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-coupling-dam.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-coupling-float.json
  - 修改：wanphys/examples/references/wanperf600_manifests/fluid.wcsph-dam-break.json
  - 修改：wanphys/examples/rigid_basic_conveyor_deterministic.py
  - 修改：wanphys/examples/rigid_basic_shapes.py
  - 修改：wanphys/examples/rigid_bunny_in_box.py
  - 修改：wanphys/examples/rigid_falling_bodies.py
  - 修改：wanphys/examples/rigid_fluid_gated_benchmark.py
  - 修改：wanphys/examples/rigid_mesh_ccd.py
  - 修改：wanphys/examples/robot/example_robot_allegro_hand.py
  - 修改：wanphys/examples/robot/example_robot_anymal_c_walk.py
  - 修改：wanphys/examples/robot/example_robot_anymal_c_walk_multi.py
  - 修改：wanphys/examples/robot/example_robot_anymal_d.py
  - 修改：wanphys/examples/robot/example_robot_cartpole.py
  - 修改：wanphys/examples/robot/example_robot_g1.py
  - 修改：wanphys/examples/robot/example_robot_h1.py
  - 修改：wanphys/examples/robot/example_robot_humanoid.py
  - 修改：wanphys/examples/robot/example_robot_panda_hydro.py
  - 修改：wanphys/examples/robot/example_robot_policy.py
  - 修改：wanphys/examples/robot/example_robot_ur10.py
  - 修改：wanphys/examples/robot/example_task2_robot.py
  - 修改：wanphys/examples/robot/example_task2_robot2.py
  - 修改：wanphys/examples/robot/example_task2_robot3.py
  - 修改：wanphys/examples/selection/example_selection_articulations.py
  - 修改：wanphys/examples/selection/example_selection_cartpole.py
  - 修改：wanphys/examples/selection/example_selection_materials.py
  - 修改：wanphys/examples/sensors/example_sensor_contact.py
  - 修改：wanphys/examples/sensors/example_sensor_frame_transform.py
  - 修改：wanphys/examples/sensors/example_sensor_imu.py
  - 修改：wanphys/examples/sensors/example_sensor_tactile_image.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_fluid.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian_fluid.py
  - 修改：wanphys/examples/soft/peri_cloth_falling.py
  - 修改：wanphys/examples/soft/peri_cloth_hanging.py
  - 修改：wanphys/examples/soft/peri_cloth_test.py
  - 修改：wanphys/examples/soft/peri_soft_balls_in_box.py
  - 修改：wanphys/examples/soft_fluid_collision.py

- 7/10-Add explicit grid-fluid solver preparation and reset（a510c72）
  - 提交者：Wei Wu
  - 提交时间：2026-09-17
  - 修改：wanphys/examples/fluid_grid_mpm_diff_skip_stone_mass.py
  - 修改：wanphys/examples/fluids/fluid_grid_basic.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse_liquid_city.py

- 4/10-Read MPM C and J from the solver in deferred scenarios（5ceeb24）
  - 提交者：Wei Wu
  - 提交时间：2026-09-17
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 7/10-Port the large-city flood scenario onto shared grid types（80e2960）
  - 提交者：Wei Wu
  - 提交时间：2026-09-17
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/fluids/fluid_grid_sparse_liquid_city.py

- 7/10-Port Cirrus two-level smoke onto SparseHierarchy（959d549）
  - 提交者：Wei Wu
  - 提交时间：2026-09-17
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/fluids/fluid_grid_cirrus.py
  - 新增：wanphys/examples/fluids/fluid_grid_cirrus_render.py

- 10/10-Unify grid fluid on GridStorage, one Model/State, and sparse FLIP（35709b0）
  - 提交者：Wei Wu
  - 提交时间：2026-09-17
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluid_grid_mpm_diff_skip_stone_mass.py
  - 修改：wanphys/examples/fluids/fluid_grid_apic.py
  - 修改：wanphys/examples/fluids/fluid_grid_basic.py
  - 修改：wanphys/examples/fluids/fluid_grid_complex_model.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid_coupling.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid_robot.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_liquid_coupling.py
  - 修改：wanphys/examples/fluids/fluid_grid_resolution_particle.py
  - 修改：wanphys/examples/fluids/fluid_grid_resolution_voxel.py
  - 修改：wanphys/examples/fluids/fluid_grid_sparse.py
  - 新增：wanphys/examples/fluids/fluid_grid_sparse_liquid.py
  - 新增：wanphys/examples/fluids/fluid_grid_sparse_liquid_coupling.py

- 2/10-Import JointType from the public selection facade（3510a75）
  - 提交者：Wei Wu
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py

- 4/10-Promote Gaussian camera examples to current catalog smoke（0fa9f77）
  - 提交者：Wei Wu
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py

- 5/10-Export Gaussian camera types from wanphys.sensors（66a5a2f）
  - 提交者：Wei Wu
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian_fluid.py

- 3/10-Fix native mesh loading in MPM skip-stone example（56b3209）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py

- 4/10-Make Gaussian plant interaction the default demo（30384da）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py

- 5/10-Download example assets as independent model packages（6816fc4）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/point_cloud_demo.py
  - 修改：wanphys/examples/utils.py

- 4/10-Fix example asset loading and smoke validation issues（f7f9502）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/fluid_grid_mpm_diff_skip_stone_mass.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py
  - 修改：wanphys/examples/robot/example_task2_robot2.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_fluid.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py

- 4/10-Support grouped example asset packages with stable file names（c27d3d4）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/fluids/fluid_grid_complex_model.py
  - 修改：wanphys/examples/point_cloud_demo.py
  - 修改：wanphys/examples/utils.py

- 8/10-Externalize runtime assets and add native package downloads（f38ff15）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/point_cloud_demo.py
  - 修改：wanphys/examples/rigid_fluid_gated_benchmark.py
  - 修改：wanphys/examples/rigid_mesh_ccd.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian_fluid.py
  - 修改：wanphys/examples/utils.py

- 8/10-Add native Gaussian sensor rendering and standalone demos（89a1d89）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py
  - 新增：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian_fluid.py

#### 📊 提交分析
- 本周总提交: 26 条
- 高价值提交（≥6分）: 8 条
- 代码更新规模: +32679 / -24570 行
- 主要贡献者: Wei Wu, FYTalon

## 📈 趋势点评
本周更新高度延续了仓库在 2026-09 确立的“资产外置、生命周期清晰化与原生渲染”主线，并进一步将重心推向网格流体求解器的统一架构与稀疏化重构。以 `35709b0` 为代表的提交将 grid fluid 统一到 GridStorage、单一 Model/State 与 sparse FLIP，配合 `86fe181` 解耦 MlsMpmSolver 与 FluidGridApicSolver、`a510c72` 显式化求解器准备与重置，说明流体模块正从多求解器并存走向共享网格类型与统一生命周期，这与基线中“网格流体求解器准备与重置”“原生求解栈解耦”的预测方向一致。`049df72` 移除 Domain 包装并明确仿真生命周期所有权，直接呼应了基线中“移除 Domain 包装并重划仿真生命周期所有权”的破坏性重构趋势。`89a1d89` 原生高斯传感器渲染与 `f38ff15` 运行时资产外置则延续了传感器原生化与资产外部化的既定路线。整体看，本周并未偏离长期趋势，而是在 9 月重构高峰上继续深化，且提交高度集中于流体架构与生命周期治理，性能/架构优化与新功能并行推进。

## 📌 关键更新解析

### 🌟 新功能/特性
8/10-Add native Gaussian sensor rendering and standalone demos（89a1d89）
  - 评分：8/10
  - 一句话总结：新增原生高斯传感器渲染能力并配套独立 demo，扩展传感器渲染栈。
  - 提交时间：2026-09-15
  - 变更规模：+10058 / -14
  - 提交者：FYTalon
  - 解决的问题：此前传感器渲染依赖非原生路径，缺少高斯表示的原生渲染与可独立运行的演示，限制了视觉传感器能力的完整性与可验证性。
  - 产品启示：原生高斯渲染与 standalone demo 可提升传感器模块的独立可用性，为触觉/视觉传感器进一步原生化与示例 catalog 化提供支撑。

8/10-Externalize runtime assets and add native package downloads（f38ff15）
  - 评分：8/10
  - 一句话总结：将运行时资产外置并支持原生包下载，显著缩减仓库内资产体积。
  - 提交时间：2026-09-15
  - 变更规模：+1092 / -18025
  - 提交者：FYTalon
  - 解决的问题：大量运行时资产内嵌导致仓库臃肿、分发与版本管理困难，示例可复现性受资产耦合影响。
  - 产品启示：资产外置与原生包下载强化了示例分发与版本化能力，但需配套网络可用性与版本一致性保障，避免引入外部依赖风险。

7/10-Port Cirrus two-level smoke onto SparseHierarchy（959d549）
  - 评分：7/10
  - 一句话总结：将 Cirrus 双层烟雾场景迁移到 SparseHierarchy，验证稀疏层级结构在烟雾仿真中的适用性。
  - 提交时间：2026-09-17
  - 变更规模：+668 / -0
  - 提交者：Wei Wu
  - 解决的问题：原有 Cirrus 烟雾示例未接入稀疏层级结构，难以复用统一网格类型与稀疏化能力。
  - 产品启示：示例向 SparseHierarchy 迁移有助于统一流体示例架构，为大规模稀疏流体场景提供可复用范式。

7/10-Port the large-city flood scenario onto shared grid types（80e2960）
  - 评分：7/10
  - 一句话总结：将大城市洪水场景迁移到共享网格类型，推动大规模流体示例架构统一。
  - 提交时间：2026-09-17
  - 变更规模：+1871 / -0
  - 提交者：Wei Wu
  - 解决的问题：大城市洪水场景此前未使用共享网格类型，导致示例间架构不一致、复用性差。
  - 产品启示：共享网格类型在大规模场景中的落地，验证了统一网格架构的可扩展性，利于后续 benchmark 与性能清单对齐。

7/10-Add explicit grid-fluid solver preparation and reset（a510c72）
  - 评分：7/10
  - 一句话总结：为网格流体求解器新增显式准备与重置流程，明确求解器生命周期。
  - 提交时间：2026-09-17
  - 变更规模：+701 / -84
  - 提交者：Wei Wu
  - 解决的问题：网格流体求解器缺少显式的准备与重置接口，生命周期不清晰，影响复用与状态管理。
  - 产品启示：显式 prepare/reset 是求解器生命周期清晰化的重要一步，与移除 Domain 包装的方向一致，利于仿真状态可控与回归测试。

### ⚙️ 性能/架构优化
10/10-Unify grid fluid on GridStorage, one Model/State, and sparse FLIP（35709b0）
  - 评分：10/10
  - 一句话总结：将网格流体统一到 GridStorage、单一 Model/State 与 sparse FLIP，完成流体架构的大一统重构。
  - 提交时间：2026-09-17
  - 变更规模：+12677 / -2165
  - 提交者：Wei Wu
  - 解决的问题：网格流体此前存在多套存储与模型状态，架构分散、维护成本高，且缺乏稀疏 FLIP 支持。
  - 产品启示：统一存储与单一 Model/State 显著降低流体模块复杂度，sparse FLIP 为大规模稀疏流体仿真奠定基础，是流体求解栈走向成熟的关键里程碑。

9/10-Remove Domain wrappers and make simulation lifecycle ownership explicit（049df72）
  - 评分：9/10
  - 一句话总结：移除 Domain 包装并显式化仿真生命周期所有权，推进核心架构去包装化。
  - 提交时间：2026-09-19
  - 变更规模：+4218 / -3382
  - 提交者：Wei Wu
  - 解决的问题：Domain 包装层导致仿真生命周期归属模糊，增加耦合与理解成本，阻碍模块所有权清晰化。
  - 产品启示：生命周期所有权显式化是架构治理的重要一步，与基线中“移除 Domain 包装”的破坏性变更趋势一致，利于后续模块解耦与文档同步。

8/10-Decouple MlsMpmSolver from FluidGridApicSolver（86fe181）
  - 评分：8/10
  - 一句话总结：解耦 MlsMpmSolver 与 FluidGridApicSolver，降低求解器间耦合。
  - 提交时间：2026-09-17
  - 变更规模：+427 / -84
  - 提交者：Wei Wu
  - 解决的问题：MlsMpmSolver 与 FluidGridApicSolver 之间存在耦合，影响求解器独立演进与复用。
  - 产品启示：求解器解耦是原生求解栈独立化的关键，配合统一网格架构可提升流体模块的可维护性与扩展性。

### 🧰 Bug修复 / 其他
- 本周高价值提交中无 Bug修复 / 其他 类别的提交。
