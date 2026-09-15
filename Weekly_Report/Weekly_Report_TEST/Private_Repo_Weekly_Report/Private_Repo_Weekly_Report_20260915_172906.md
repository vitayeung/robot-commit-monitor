# WanPhys Weekly Report (2026-09-15 17:29:06)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-15 17:29:06
- 统计截止: 2026-09-15 17:29:06
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

- 6/10-example modification（9dd499c）
  - 提交者：syq
  - 提交时间：2026-09-08
  - 新增：wanphys/examples/fluid_grid_mpm_diff_skip_stone_mass.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

#### 📊 提交分析
- 本周总提交: 22 条
- 高价值提交（≥6分）: 14 条
- 代码更新规模: +30633 / -14576 行
- 主要贡献者: Wei Wu, give-lab, huangtaikai, syq

## 📈 趋势点评

本周（2026-09-08 ~ 2026-09-13）的更新高度延续了仓库自 2026-06 以来“碰撞管线重构 + Newton 解耦 + 性能/回归制度化”的主线，并进一步向纵深推进：一方面，`269f34d`、`e768cd2`、`4d99bd7`、`743935e` 等提交集中完成原生刚体模型构建器、资产管线与机器人集成，并移除刚体 Newton 转换与 VBD 适配器，标志着自研原生后端从“局部替换”走向“完整闭环”，与基线中“从 Newton 依赖迁移到自研原生后端”的长期趋势高度一致；另一方面，`07e9b09`、`c6c56d2`、`1ef04e0`、`680b90f`、`ddaef55` 等提交围绕 CCD 统一固定网格与凸查询、碰撞模块本地化、ContactData/Contacts 缓冲自持以及内核原生枚举化展开，属于接口级与所有权级的大规模重构，延续了 2026-09 基线中“碰撞与接触精度集中攻坚”的方向。同时，`34d0aad`、`6b8f6ab`、`814c21a` 三条 SDF/混合网格边距修复，以及 `27e010a` 补齐柔性接触面 SDF 构建，呼应了基线中“SDF 与混合网格碰撞的多次修复提示几何边界处理仍不稳定”的风险判断，说明数值精度仍是当前薄弱环节。此外，`9dd499c` 新增 MPM 可微耦合与示例，将流体求解器从纯仿真扩展到可微方向，略微偏离了此前以碰撞/刚体为主的演进重心，但符合基线“多物理场扩展”的预测。整体看，本周更新在架构治理与原生后端闭环上明显加速，但重构密度高、破坏性变更集中，回归风险与文档/示例滞后风险需持续关注。

## 📌 关键更新解析

### 🌟 新功能/特性

9/10-Complete native rigid scene and robot integration（269f34d）
  - 评分：9/10
  - 一句话总结：完成原生刚体场景与机器人集成，打通从场景构建到机器人仿真的完整链路。
  - 提交时间：2026-09-08
  - 变更规模：+6211 / -1135
  - 提交者：Wei Wu
  - 解决的问题：此前原生刚体能力分散、缺少端到端的场景与机器人集成，难以支撑完整机器人仿真工作流。
  - 产品启示：原生刚体闭环是替代 Newton 后端的关键里程碑，可作为对外展示与机器人示例生态的核心卖点。

9/10-Implement native rigid model builder and asset pipeline（e768cd2）
  - 评分：9/10
  - 一句话总结：实现原生刚体模型构建器与资产管线，为刚体资产提供统一构建与校验入口。
  - 提交时间：2026-09-08
  - 变更规模：+6063 / -1055
  - 提交者：Wei Wu
  - 解决的问题：刚体模型构建与资产导入缺乏原生管线，依赖外部后端且校验脚本分散。
  - 产品启示：资产管线是生态扩展的基础设施，配套的 check/validate 脚本可提升资产质量与可维护性。

7/10-fix: 补齐柔性接触面 SDF 构建并标注待重构范围（27e010a）
  - 评分：7/10
  - 一句话总结：补齐柔性接触面 SDF 构建，并显式标注待重构范围。
  - 提交时间：2026-09-13
  - 变更规模：+512 / -5
  - 提交者：give-lab
  - 解决的问题：柔性接触面缺少 SDF 构建支持，导致软体接触精度与覆盖不足。
  - 产品启示：显式标注待重构范围有助于控制技术债，软体接触 SDF 是提升软体仿真可信度的关键能力。

6/10-example modification（9dd499c）
  - 评分：6/10
  - 一句话总结：新增 MPM 可微耦合与示例，将流体求解器扩展到可微方向。
  - 提交时间：2026-09-08
  - 变更规模：+3451 / -2216
  - 提交者：syq
  - 解决的问题：流体 MPM 缺少可微耦合能力，难以支撑梯度优化与学习类任务。
  - 产品启示：可微物理是连接仿真与学习的桥梁，可拓展到机器人控制、参数辨识等下游场景。

### ⚙️ 性能/架构优化

8/10-ccd unify fixed mesh and convex queries, update BFS response（07e9b09）
  - 评分：8/10
  - 一句话总结：CCD 统一固定网格与凸查询，并更新 BFS 响应。
  - 提交时间：2026-09-13
  - 变更规模：+3508 / -5400
  - 提交者：huangtaikai
  - 解决的问题：固定网格与凸体查询路径分裂，CCD 查询逻辑重复且维护成本高。
  - 产品启示：查询统一可显著降低 CCD 维护复杂度，是碰撞管线收敛的重要一步。

8/10-collision localization, not totally refactor（c6c56d2）
  - 评分：8/10
  - 一句话总结：对碰撞模块进行大规模本地化重构，但保持整体结构不彻底重写。
  - 提交时间：2026-09-13
  - 变更规模：+5447 / -206
  - 提交者：give-lab
  - 解决的问题：碰撞模块对外部依赖与命名耦合较重，本地化程度不足。
  - 产品启示：渐进式本地化可在控制风险的同时推进架构治理，为后续彻底重构铺路。

7/10-Remove rigid Newton conversion hatches and VBD adapter（4d99bd7）
  - 评分：7/10
  - 一句话总结：移除刚体 Newton 转换通道与 VBD 适配器，进一步切断 Newton 耦合。
  - 提交时间：2026-09-09
  - 变更规模：+308 / -635
  - 提交者：Wei Wu
  - 解决的问题：刚体侧仍保留 Newton 转换与 VBD 适配逃生通道，阻碍原生后端闭环。
  - 产品启示：清理逃生通道是架构收敛的必要代价，需同步评估既有调用方的迁移成本。

6/10-Own ContactData and the Contacts-buffer writer（1ef04e0）
  - 评分：6/10
  - 一句话总结：接管 ContactData 与 Contacts 缓冲写入器，实现接触数据自持。
  - 提交时间：2026-09-09
  - 变更规模：+204 / -37
  - 提交者：Wei Wu
  - 解决的问题：接触数据与写入器依赖外部实现，所有权不清晰。
  - 产品启示：数据所有权自持是碰撞管线独立化的基础，利于后续性能与调试优化。

6/10-Own WanPhys Contacts buffers for collision pipelines（680b90f）
  - 评分：6/10
  - 一句话总结：为碰撞管线自持 WanPhys Contacts 缓冲。
  - 提交时间：2026-09-09
  - 变更规模：+187 / -21
  - 提交者：Wei Wu
  - 解决的问题：碰撞管线共享外部 Contacts 缓冲，存在耦合与生命周期管理问题。
  - 产品启示：缓冲自持可提升管线稳定性与可预测性，是性能调优的前置条件。

6/10-Point collision kernels at native enums and owned math helpers（ddaef55）
  - 评分：6/10
  - 一句话总结：碰撞内核改用原生枚举与自持数学助手。
  - 提交时间：2026-09-09
  - 变更规模：+120 / -84
  - 提交者：Wei Wu
  - 解决的问题：碰撞内核依赖外部枚举与数学工具，命名与语义不一致。
  - 产品启示：内核原生化为后续跨后端统一与性能优化提供一致语义基础。

### 🧰 Bug修复 / 其他

7/10-fix: 修正粗 SDF 边界的距离与梯度采样（34d0aad）
  - 评分：7/10
  - 一句话总结：修正粗 SDF 边界的距离与梯度采样错误。
  - 提交时间：2026-09-13
  - 变更规模：+140 / -24
  - 提交者：give-lab
  - 解决的问题：粗 SDF 边界处距离与梯度采样不准确，影响接触精度。
  - 产品启示：SDF 边界精度直接决定接触可信度，需配套回归测试防止回退。

6/10-Fix native rigid inertials and refresh self-regression pins（743935e）
  - 评分：6/10
  - 一句话总结：修复原生刚体惯量计算并刷新自回归基线。
  - 提交时间：2026-09-08
  - 变更规模：+175 / -26
  - 提交者：Wei Wu
  - 解决的问题：原生刚体惯量计算错误，且回归基线未同步更新。
  - 产品启示：惯量正确性是刚体仿真物理可信度的基础，回归基线刷新需纳入常规流程。

6/10-fix: 修正混合网格碰撞的边距重复计算（814c21a）
  - 评分：6/10
  - 一句话总结：修正混合网格碰撞中边距被重复计算的问题。
  - 提交时间：2026-09-13
  - 变更规模：+78 / -3
  - 提交者：give-lab
  - 解决的问题：混合网格碰撞边距重复累加，导致接触距离偏大。
  - 产品启示：边距计算是碰撞精度的细节关键，需在窄相与 SDF 接触间统一口径。

6/10-fix: 修正稀疏 SDF 边界的距离与梯度采样（6b8f6ab）
  - 评分：6/10
  - 一句话总结：修正稀疏 SDF 边界采样污染导致的距离与梯度错误。
  - 提交时间：2026-09-13
  - 变更规模：+105 / -17
  - 提交者：give-lab
  - 解决的问题：稀疏 SDF 边界采样被污染，距离与梯度结果不可靠。
  - 产品启示：稀疏 SDF 是大场景仿真的关键数据结构，其边界正确性直接影响地形与网格接触质量。
