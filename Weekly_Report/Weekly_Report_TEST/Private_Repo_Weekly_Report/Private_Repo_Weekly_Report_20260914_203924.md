# WanPhys Weekly Report (2026-09-14 20:39:24)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-14 20:39:24
- 统计截止: 2026-09-14 20:39:24
- 分析窗口: 最近 7 天（截止上述时间）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 8/10-ccd unify fixed mesh and convex queries, update BFS response（07e9b09）
  - 提交者：huangtaikai
  - 提交时间：2026-09-13
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 8/10-collision localization, not totally refactor（c6c56d2）
  - 提交者：give-lab
  - 提交时间：2026-09-13
  - 修改：wanphys/examples/robot/example_robot_panda_hydro.py

- 6/10-Own WanPhys Contacts buffers for collision pipelines（680b90f）
  - 提交者：Wei Wu
  - 提交时间：2026-09-09
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 7/10-Remove rigid Newton conversion hatches and VBD adapter（4d99bd7）
  - 提交者：Wei Wu
  - 提交时间：2026-09-09
  - 修改：wanphys/examples/rigid_fluid_gated_benchmark.py
  - 修改：wanphys/examples/robot/example_robot_g1.py

- 6/10-Fix native rigid inertials and refresh self-regression pins（743935e）
  - 提交者：Wei Wu
  - 提交时间：2026-09-08
  - 修改：wanphys/examples/_lifecycle.py
  - 修改：wanphys/examples/robot/example_robot_cartpole.py

- 9/10-Complete native rigid scene and robot integration（269f34d）
  - 提交者：Wei Wu
  - 提交时间：2026-09-08
  - 新增：wanphys/examples/_bunny_asset.py
  - 修改：wanphys/examples/basic/example_basic_joints.py
  - 修改：wanphys/examples/basic/example_basic_pendulum.py
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/basic/example_basic_urdf.py
  - 修改：wanphys/examples/basic/example_basic_viewer.py
  - 修改：wanphys/examples/broad_phase_benchmark.py
  - 修改：wanphys/examples/cloth/_style3d_assets.py
  - 修改：wanphys/examples/cloth/example_cloth_bending.py
  - 修改：wanphys/examples/cloth/example_cloth_franka.py
  - 修改：wanphys/examples/cloth/example_cloth_h1.py
  - 修改：wanphys/examples/cloth/example_cloth_hanging.py
  - 修改：wanphys/examples/cloth/example_cloth_style3d.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_dam_break.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_non_newtonian_jet.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluids/fluid_dfsph_surface_tension_jeske2023.py
  - 修改：wanphys/examples/fluids/fluid_grid_apic.py
  - 修改：wanphys/examples/fluids/fluid_grid_basic.py
  - 修改：wanphys/examples/fluids/fluid_grid_complex_model.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid_coupling.py
  - 修改：wanphys/examples/fluids/fluid_grid_liquid_robot.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_liquid_coupling.py
  - 修改：wanphys/examples/fluids/fluid_grid_resolution_particle.py
  - 修改：wanphys/examples/fluids/fluid_grid_resolution_voxel.py
  - 修改：wanphys/examples/fluids/fluid_pbf_coupling_dam.py
  - 修改：wanphys/examples/fluids/fluid_pbf_coupling_float.py
  - 修改：wanphys/examples/fluids/fluid_pbf_dam_break.py
  - 修改：wanphys/examples/fluids/fluid_pbf_emitter_corals.py
  - 修改：wanphys/examples/fluids/fluid_pbf_non_newtonian_jet.py
  - 修改：wanphys/examples/fluids/fluid_pbf_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluids/fluid_pbf_surface_tension_jeske2023.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_coupling_dam.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_coupling_float.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_dam_break.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_non_newtonian_jet.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_surface_tension_akinci2013.py
  - 修改：wanphys/examples/fluids/fluid_wcsph_surface_tension_jeske2023.py
  - 修改：wanphys/examples/point_cloud_demo.py
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
  - 修改：wanphys/examples/runner.py
  - 修改：wanphys/examples/selection/example_selection_articulations.py
  - 修改：wanphys/examples/selection/example_selection_cartpole.py
  - 修改：wanphys/examples/selection/example_selection_materials.py
  - 修改：wanphys/examples/sensors/example_sensor_contact.py
  - 修改：wanphys/examples/sensors/example_sensor_frame_transform.py
  - 修改：wanphys/examples/sensors/example_sensor_imu.py
  - 修改：wanphys/examples/sensors/example_sensor_tactile_image.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_fluid.py
  - 修改：wanphys/examples/soft/pd_cloth_drape.py
  - 修改：wanphys/examples/soft/pd_cloth_dummy.py
  - 修改：wanphys/examples/soft/pd_clothes_drape_dragon.py
  - 修改：wanphys/examples/soft/pd_clothes_throw_dragon.py
  - 修改：wanphys/examples/soft/vbd_ball_and_bricks.py
  - 修改：wanphys/examples/soft/vbd_cloth_drape.py
  - 修改：wanphys/examples/soft/vbd_cloth_hanging.py
  - 修改：wanphys/examples/soft/vbd_rigid_body_to_cloth.py
  - 修改：wanphys/examples/utils.py

- 9/10-Implement native rigid model builder and asset pipeline（e768cd2）
  - 提交者：Wei Wu
  - 提交时间：2026-09-08
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 2/10-Fix PR75 scenario asset path and catalog classification（ad3b62e）
  - 提交者：Wei Wu
  - 提交时间：2026-09-08
  - 修改：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 5/10-example modification（9dd499c）
  - 提交者：syq
  - 提交时间：2026-09-08
  - 新增：wanphys/examples/fluid_grid_mpm_diff_skip_stone_mass.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

- 5/10-remove pre ccd owns domain（02b15d7）
  - 提交者：huangtaikai
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 7/10-Refactor CCD into pre and post two APIs（28d4245）
  - 提交者：huangtaikai
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 6/10-Simplify CCD pipeline ownership and event sweep（efd25b1）
  - 提交者：huangtaikai
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/rigid_mesh_ccd.py

#### 📊 提交分析
- 本周总提交: 28 条
- 高价值提交（≥6分）: 16 条
- 代码更新规模: +33429 / -16570 行
- 主要贡献者: Wei Wu, give-lab, huangtaikai, syq

## 📈 趋势点评
本周更新高度延续了仓库自 2026-07 以来“碰撞管线收敛 + 原生后端解耦 + 性能回归工程化”的长期主线，并在此基础上出现明显加速：一方面，CCD 被正式拆分为 pre/post 双 API（28d4245）并统一固定网格与凸体查询（07e9b09），配合 collision 模块大规模本地化（c6c56d2）与管线归属简化（efd25b1），说明碰撞子系统正从“功能堆叠”走向“接口收敛与所有权清晰化”；另一方面，原生刚体构建器与资产管线（e768cd2、269f34d）以及移除 Newton 转换逃生通道与 VBD 适配器（4d99bd7）等提交，标志着项目正坚定地降低对 Newton 后端的耦合，向自持的 WanPhys 原生栈迁移。同时，稀疏/粗 SDF 边界采样修复（6b8f6ab、34d0aad）、混合网格碰撞边距重复计算修复（814c21a）与柔性接触面 SDF 构建补齐（27e010a）表明几何与接触精度仍是当前重点打磨方向。整体来看，本周并未偏离长期趋势，而是将此前分散的 CCD、SDF、原生刚体与接触数据所有权等线索集中推进，进一步夯实平台化物理仿真基础设施。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-Complete native rigid scene and robot integration（269f34d）
  - 评分：9/10
  - 一句话总结：完成原生刚体场景与机器人集成，推动刚体仿真全面转向 WanPhys 原生栈。
  - 提交时间：2026-09-08
  - 变更规模：+6211 / -1135
  - 提交者：Wei Wu
  - 解决的问题：此前刚体场景与机器人示例仍依赖外部后端与转换路径，缺乏端到端的原生集成能力。
  - 产品启示：原生刚体场景与机器人集成落地后，可支撑更完整的机器人仿真与操作场景，减少对外部后端的依赖，提升平台自主可控性。

9/10-Implement native rigid model builder and asset pipeline（e768cd2）
  - 评分：9/10
  - 一句话总结：实现原生刚体模型构建器与资产管线，为刚体资产导入与构建提供统一入口。
  - 提交时间：2026-09-08
  - 变更规模：+6063 / -1055
  - 提交者：Wei Wu
  - 解决的问题：刚体模型构建与资产导入缺乏原生、统一的管线，导致示例与场景构建依赖零散路径。
  - 产品启示：原生构建器与资产管线可显著降低刚体场景搭建成本，为后续机器人、地形与多物理耦合场景提供可复用的资产基础。

6/10-add hfield-mesh contact vertex and sdf mode switch（ed1c934）
  - 评分：6/10
  - 一句话总结：新增 hfield-mesh 接触顶点与 SDF 模式切换，增强高度场与网格碰撞的表达能力。
  - 提交时间：2026-09-07
  - 变更规模：+62 / -4
  - 提交者：huangtaikai
  - 解决的问题：hfield 与 mesh 之间的接触处理缺少顶点级支持与 SDF 模式切换，限制了地形与网格碰撞的精度与灵活性。
  - 产品启示：该能力可提升地形、月面 DTM/DEM 等场景下的接触仿真质量，为户外与崎岖地形机器人仿真提供支撑。

6/10-fix: 补齐柔性接触面 SDF 构建并标注待重构范围（27e010a）
  - 评分：6/10
  - 一句话总结：补齐柔性接触面 SDF 构建，并标注后续待重构范围。
  - 提交时间：2026-09-13
  - 变更规模：+512 / -5
  - 提交者：give-lab
  - 解决的问题：柔性接触面缺少 SDF 构建能力，导致软体与刚体/环境之间的接触建模不完整。
  - 产品启示：补齐柔性接触面 SDF 构建后，软体与复杂几何的接触仿真更完整，为软体机器人、柔性抓取等场景提供基础能力。

### ⚙️ 性能/架构优化
8/10-ccd unify fixed mesh and convex queries, update BFS response（07e9b09）
  - 评分：8/10
  - 一句话总结：统一 CCD 固定网格与凸体查询，并更新 BFS 响应逻辑。
  - 提交时间：2026-09-13
  - 变更规模：+3508 / -5400
  - 提交者：huangtaikai
  - 解决的问题：CCD 中固定网格与凸体查询路径分散、重复，BFS 响应逻辑不统一，增加维护与性能开销。
  - 产品启示：查询路径统一后，CCD 的可维护性与性能一致性提升，为后续碰撞检测的持续优化与回归验证奠定基础。

8/10-collision localization, not totally refactor（c6c56d2）
  - 评分：8/10
  - 一句话总结：对 collision 模块进行大规模本地化，而非完全重构。
  - 提交时间：2026-09-13
  - 变更规模：+5447 / -206
  - 提交者：give-lab
  - 解决的问题：collision 模块对外部依赖与命名耦合较重，缺乏本地化组织，影响可维护性与演进。
  - 产品启示：本地化后 collision 模块边界更清晰，有利于后续独立演进、测试与性能治理。

7/10-Refactor CCD into pre and post two APIs（28d4245）
  - 评分：7/10
  - 一句话总结：将 CCD 重构为 pre 与 post 两套 API，明确阶段职责。
  - 提交时间：2026-09-07
  - 变更规模：+694 / -735
  - 提交者：huangtaikai
  - 解决的问题：CCD 原有 API 阶段划分不清，pre/post 职责混杂，影响调用与扩展。
  - 产品启示：pre/post 双 API 使 CCD 流程更清晰，便于集成到不同仿真管线并支持后续性能与回归测试。

7/10-Remove rigid Newton conversion hatches and VBD adapter（4d99bd7）
  - 评分：7/10
  - 一句话总结：移除刚体 Newton 转换逃生通道与 VBD 适配器，进一步解耦外部后端。
  - 提交时间：2026-09-09
  - 变更规模：+308 / -635
  - 提交者：Wei Wu
  - 解决的问题：刚体中残留的 Newton 转换与 VBD 适配器造成接口耦合与维护负担。
  - 产品启示：移除逃生通道后，原生刚体栈更纯粹，降低长期维护成本，但需关注短期接口兼容性。

6/10-Simplify CCD pipeline ownership and event sweep（efd25b1）
  - 评分：6/10
  - 一句话总结：简化 CCD 管线归属与事件扫描逻辑。
  - 提交时间：2026-09-07
  - 变更规模：+709 / -984
  - 提交者：huangtaikai
  - 解决的问题：CCD 管线归属不清、事件扫描逻辑冗余，增加复杂度与潜在性能损耗。
  - 产品启示：管线归属简化后，CCD 更易维护与调优，为后续性能清单与回归覆盖提供稳定基础。

6/10-Own ContactData and the Contacts-buffer writer（1ef04e0）
  - 评分：6/10
  - 一句话总结：接管 ContactData 与 Contacts 缓冲区写入器，实现接触数据自持。
  - 提交时间：2026-09-09
  - 变更规模：+204 / -37
  - 提交者：Wei Wu
  - 解决的问题：接触数据与缓冲区写入依赖外部实现，缺乏自主控制。
  - 产品启示：自持接触数据与写入器后，接触管线更可控，便于性能优化与回归验证。

6/10-Own WanPhys Contacts buffers for collision pipelines（680b90f）
  - 评分：6/10
  - 一句话总结：为碰撞管线自持 WanPhys Contacts 缓冲区。
  - 提交时间：2026-09-09
  - 变更规模：+187 / -21
  - 提交者：Wei Wu
  - 解决的问题：碰撞管线中的 Contacts 缓冲区依赖外部管理，影响一致性与性能。
  - 产品启示：自持缓冲区后，碰撞管线数据流更统一，有利于后续性能与内存优化。

6/10-Point collision kernels at native enums and owned math helpers（ddaef55）
  - 评分：6/10
  - 一句话总结：将碰撞内核指向原生枚举与自有数学助手。
  - 提交时间：2026-09-09
  - 变更规模：+120 / -84
  - 提交者：Wei Wu
  - 解决的问题：碰撞内核仍引用外部枚举与数学工具，造成耦合与不一致。
  - 产品启示：内核改用原生枚举与数学助手后，碰撞计算路径更统一，降低外部依赖风险。

### 🧰 Bug修复 / 其他
7/10-fix: 修正稀疏 SDF 边界的距离与梯度采样（6b8f6ab）
  - 评分：7/10
  - 一句话总结：修正稀疏 SDF 边界的距离与梯度采样精度问题。
  - 提交时间：2026-09-13
  - 变更规模：+105 / -17
  - 提交者：give-lab
  - 解决的问题：稀疏 SDF 在边界处的距离与梯度采样不准确，影响接触精度。
  - 产品启示：修复后接触仿真在稀疏 SDF 场景下更可靠，提升几何精度与稳定性。

7/10-fix: 修正粗 SDF 边界的距离与梯度采样（34d0aad）
  - 评分：7/10
  - 一句话总结：修正粗 SDF 边界的距离与梯度采样精度问题。
  - 提交时间：2026-09-13
  - 变更规模：+140 / -24
  - 提交者：give-lab
  - 解决的问题：粗 SDF 边界采样误差导致接触计算偏差。
  - 产品启示：修复后粗 SDF 场景下的接触精度提升，有利于大规模场景的性能与精度平衡。

6/10-Fix native rigid inertials and refresh self-regression pins（743935e）
  - 评分：6/10
  - 一句话总结：修复原生刚体惯量计算并刷新自回归基线。
  - 提交时间：2026-09-08
  - 变更规模：+175 / -26
  - 提交者：Wei Wu
  - 解决的问题：原生刚体惯量计算存在偏差，且回归基线未同步更新。
  - 产品启示：惯量修复提升刚体动力学正确性，回归基线刷新保障后续变更可验证。

6/10-fix: 修正混合网格碰撞的边距重复计算（814c21a）
  - 评分：6/10
  - 一句话总结：修正混合网格碰撞中边距重复计算的问题。
  - 提交时间：2026-09-13
  - 变更规模：+78 / -3
  - 提交者：give-lab
  - 解决的问题：混合网格碰撞边距被重复计算，导致接触行为异常。
  - 产品启示：修复后混合网格碰撞更准确，提升复杂几何场景下的仿真可信度。
