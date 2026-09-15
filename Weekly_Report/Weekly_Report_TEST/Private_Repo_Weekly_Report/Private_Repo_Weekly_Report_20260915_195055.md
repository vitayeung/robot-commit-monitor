# WanPhys Weekly Report (2026-09-15 19:50:55)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-15 19:50:55
- 统计截止: 2026-09-15 19:50:55
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

- 7/10-Fix native rigid inertials and refresh self-regression pins（743935e）
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
本周更新延续了仓库自 2026-08 以来“碰撞管线收敛与去 Newton 耦合”的主线，并进一步向原生刚体资产管线与场景集成推进：269f34d、e768cd2 两条超大提交（合计超 1.2 万行变更）标志着原生刚体构建器与机器人集成进入收尾阶段，而 4d99bd7、1ef04e0、680b90f、ddaef55 等提交则系统性地移除了 Newton 转换通道、接管 ContactData 与 Contacts 缓冲、将碰撞内核切换到原生枚举，与基线中“移除 Newton 后端耦合逃生通道（fad5602）”的长期方向高度一致。同时，07e9b09、c6c56d2 对 CCD 与碰撞模块进行统一查询与本地化重构，配合 34d0aad、6b8f6ab、814c21a 对 SDF 边界与混合网格边距的连续修复，说明碰撞精度与数值稳定性仍是持续投入的薄弱环节，与基线中“稀疏/粗 SDF 边界修复反复出现”的风险判断吻合。此外，9dd499c 新增 MPM 可微耦合示例、27e010a 补齐柔性接触面 SDF 构建，显示软体/流体与可微仿真方向仍在扩张，整体节奏与基线预测的“碰撞深化 + 性能回归常态化 + 软体流体扩展”方向一致，未出现明显偏离。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-Complete native rigid scene and robot integration（269f34d）
  - 评分：9/10
  - 一句话总结：完成原生刚体场景与机器人集成，打通从资产到场景的完整链路。
  - 提交时间：2026-09-08
  - 变更规模：+6211 / -1135
  - 提交者：Wei Wu
  - 解决的问题：原生刚体此前缺乏端到端的场景与机器人集成能力，难以直接支撑机器人仿真场景搭建。
  - 产品启示：原生刚体管线已具备可交付的场景级能力，可作为机器人仿真与基准示例的统一入口。

9/10-Implement native rigid model builder and asset pipeline（e768cd2）
  - 评分：9/10
  - 一句话总结：实现原生刚体模型构建器与资产管线，配套校验与导入脚本。
  - 提交时间：2026-09-08
  - 变更规模：+6063 / -1055
  - 提交者：Wei Wu
  - 解决的问题：刚体模型构建与资产导入长期依赖外部后端，缺少原生、可校验的构建与资产管线。
  - 产品启示：资产管线是生态扩展的基础设施，可显著降低新机器人/场景的接入成本。

7/10-fix: 补齐柔性接触面 SDF 构建并标注待重构范围（27e010a）
  - 评分：7/10
  - 一句话总结：补齐柔性接触面 SDF 构建，并明确标注后续待重构范围。
  - 提交时间：2026-09-13
  - 变更规模：+512 / -5
  - 提交者：give-lab
  - 解决的问题：柔性接触面缺少 SDF 构建支持，导致软体接触场景无法正确生成符号距离场。
  - 产品启示：软体接触精度依赖 SDF 构建完整性，补齐后可为软体-刚体耦合场景提供基础。

6/10-example modification（9dd499c）
  - 评分：6/10
  - 一句话总结：新增 MPM 可微耦合示例，扩展流体网格与耦合模块。
  - 提交时间：2026-09-08
  - 变更规模：+3451 / -2216
  - 提交者：syq
  - 解决的问题：缺少 MPM 与可微耦合的示例，用户难以理解流体网格耦合与梯度计算的使用方式。
  - 产品启示：可微耦合示例有助于吸引研究型用户，强化仓库在可微物理仿真方向的差异化定位。

### ⚙️ 性能/架构优化
8/10-ccd unify fixed mesh and convex queries, update BFS response（07e9b09）
  - 评分：8/10
  - 一句话总结：统一 CCD 中固定网格与凸体查询接口，并更新 BFS 响应逻辑。
  - 提交时间：2026-09-13
  - 变更规模：+3508 / -5400
  - 提交者：huangtaikai
  - 解决的问题：CCD 中网格与凸体查询接口分裂，导致调用路径重复、维护成本高。
  - 产品启示：查询接口统一可降低 CCD 使用门槛，为后续 pre/post 双 API 拆分奠定基础。

8/10-collision localization, not totally refactor（c6c56d2）
  - 评分：8/10
  - 一句话总结：对碰撞模块进行大规模本地化，减少对外部实现的依赖。
  - 提交时间：2026-09-13
  - 变更规模：+5447 / -206
  - 提交者：give-lab
  - 解决的问题：碰撞模块长期依赖外部后端实现，接口与行为难以自主控制。
  - 产品启示：本地化是去 Newton 耦合的关键一步，可提升碰撞管线的可控性与可演进性。

7/10-Remove rigid Newton conversion hatches and VBD adapter（4d99bd7）
  - 评分：7/10
  - 一句话总结：移除刚体 Newton 转换通道与 VBD 适配器，简化核心枚举与刚体入口。
  - 提交时间：2026-09-09
  - 变更规模：+308 / -635
  - 提交者：Wei Wu
  - 解决的问题：残留的 Newton 转换通道与 VBD 适配器造成接口冗余与行为不一致。
  - 产品启示：清理转换通道可减少维护负担，但需注意对依赖旧接口用户的破坏性影响。

6/10-Own ContactData and the Contacts-buffer writer（1ef04e0）
  - 评分：6/10
  - 一句话总结：接管 ContactData 与 Contacts 缓冲写入器，减少对 Newton 导入的依赖。
  - 提交时间：2026-09-09
  - 变更规模：+204 / -37
  - 提交者：Wei Wu
  - 解决的问题：ContactData 与缓冲写入器仍依赖 Newton 导入，阻碍碰撞管线自主化。
  - 产品启示：自持接触数据结构是碰撞管线独立演进的前提，利于后续性能与精度优化。

6/10-Own WanPhys Contacts buffers for collision pipelines（680b90f）
  - 评分：6/10
  - 一句话总结：为碰撞管线自持 WanPhys Contacts 缓冲，覆盖 CCD 引擎与预处理路径。
  - 提交时间：2026-09-09
  - 变更规模：+187 / -21
  - 提交者：Wei Wu
  - 解决的问题：碰撞管线共享外部 Contacts 缓冲，导致生命周期与所有权不清晰。
  - 产品启示：缓冲自持可提升内存与生命周期可控性，为性能基准稳定提供保障。

6/10-Point collision kernels at native enums and owned math helpers（ddaef55）
  - 评分：6/10
  - 一句话总结：将碰撞内核切换到原生枚举与自有数学辅助函数。
  - 提交时间：2026-09-09
  - 变更规模：+120 / -84
  - 提交者：Wei Wu
  - 解决的问题：碰撞内核仍引用外部枚举与数学工具，存在耦合与不一致风险。
  - 产品启示：内核层去耦可提升数值行为一致性，是碰撞精度修复的基础。

### 🧰 Bug修复 / 其他
7/10-Fix native rigid inertials and refresh self-regression pins（743935e）
  - 评分：7/10
  - 一句话总结：修复原生刚体惯量计算并刷新自回归基线。
  - 提交时间：2026-09-08
  - 变更规模：+175 / -26
  - 提交者：Wei Wu
  - 解决的问题：原生刚体惯量计算错误，导致 MJCF/URDF 导入后动力学行为异常。
  - 产品启示：惯量正确性是刚体仿真可信度的基础，回归基线刷新可防止问题复发。

7/10-fix: 修正稀疏 SDF 边界的距离与梯度采样（6b8f6ab）
  - 评分：7/10
  - 一句话总结：修正稀疏 SDF 边界的距离与梯度采样错误。
  - 提交时间：2026-09-13
  - 变更规模：+105 / -17
  - 提交者：give-lab
  - 解决的问题：稀疏 SDF 在边界处距离与梯度采样不准确，影响接触精度。
  - 产品启示：SDF 边界采样是接触稳定性的薄弱点，需持续以回归测试覆盖。

7/10-fix: 修正粗 SDF 边界的距离与梯度采样（34d0aad）
  - 评分：7/10
  - 一句话总结：修正粗 SDF 边界的距离与梯度采样错误，并补充测试说明。
  - 提交时间：2026-09-13
  - 变更规模：+140 / -24
  - 提交者：give-lab
  - 解决的问题：粗 SDF 边界采样偏差导致接触力计算不准确。
  - 产品启示：粗/稀疏 SDF 修复反复出现，说明几何边界条件仍是稳定性薄弱环节。

6/10-fix: 修正混合网格碰撞的边距重复计算（814c21a）
  - 评分：6/10
  - 一句话总结：修正混合网格碰撞中边距被重复计算的问题。
  - 提交时间：2026-09-13
  - 变更规模：+78 / -3
  - 提交者：give-lab
  - 解决的问题：混合网格碰撞边距重复计算导致接触距离偏大、接触行为异常。
  - 产品启示：边距计算需统一入口，避免多路径重复叠加引发精度问题。
