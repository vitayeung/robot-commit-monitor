# WanPhys Weekly Report (2026-09-14 07:02:26)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-14 07:02:26
- 分析窗口: 最近 7 天
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 8/10-Own WanPhys Contacts buffers for collision pipelines（680b90f）
  - 提交者：Wei Wu
  - 提交时间：2026-09-09
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 8/10-Remove rigid Newton conversion hatches and VBD adapter（4d99bd7）
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

- 5/10-remove pre ccd owns domain（02b15d7）
  - 提交者：huangtaikai
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 8/10-Refactor CCD into pre and post two APIs（28d4245）
  - 提交者：huangtaikai
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 7/10-Simplify CCD pipeline ownership and event sweep（efd25b1）
  - 提交者：huangtaikai
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 8/10-Remove WanPhys test suite and legacy particle-fluid implementations（bea6e5d）
  - 提交者：Wei Wu
  - 提交时间：2026-09-07
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py

#### 📊 提交分析
- 本周总提交: 19 条
- 高价值提交（≥6分）: 13 条
- 代码更新规模: +21813 / -38215 行
- 主要贡献者: Wei Wu, huangtaikai, syq

## 📈 趋势点评
本周更新延续了仓库自 2026 年 7 月以来“去 Newton 依赖、原生内核接管、性能与回归工程化”的主线，并出现明显加速：一方面，原生刚体构建器、资产管线与机器人集成在两天内以超过 1.2 万行新增代码集中落地，配合移除 Newton 转换逃生通道与 VBD 适配器，标志着刚体栈从“桥接迁移”正式转入“自有实现”阶段；另一方面，CCD 被拆分为 pre/post 双 API、管线所有权与事件扫描被简化、碰撞内核改用原生枚举与自有数学工具，说明碰撞体系正从功能铺开转向接口收敛与结构清理。同时，删除近 2.9 万行遗留粒子流体与旧测试套件、将刚体测试纳入 unittest 组织，体现出团队在快速扩张后主动偿还架构债、压缩维护面。整体看，本周并未偏离长期趋势，而是把“原生接管 + 基准回归 + 模块瘦身”三条线同时推进到了更彻底的执行层面，风险点仍在于高频重构下的接口稳定性与回归 pin 的持续维护成本。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-Complete native rigid scene and robot integration（269f34d）
  - 评分：9/10
  - 一句话总结：完成原生刚体场景与机器人集成，打通从场景构建到机器人装配的完整链路。
  - 提交时间：2026-09-08
  - 变更规模：+6211 / -1135
  - 提交者：Wei Wu
  - 解决的问题：此前刚体场景与机器人集成依赖 Newton 桥接，缺乏原生统一入口，导致场景装配与机器人导入割裂。
  - 产品启示：原生刚体场景与机器人一体化是具身智能仿真的基础能力，直接决定机器人示例与训练环境的可复现性，应作为对外主推能力持续打磨。

9/10-Implement native rigid model builder and asset pipeline（e768cd2）
  - 评分：9/10
  - 一句话总结：实现原生刚体模型构建器与资产管线，为刚体资产提供统一构建与校验流程。
  - 提交时间：2026-09-08
  - 变更规模：+6063 / -1055
  - 提交者：Wei Wu
  - 解决的问题：刚体模型构建与资产导入缺少原生管线，资产格式与校验脚本分散，难以保证一致性。
  - 产品启示：资产管线是仿真平台规模化的关键基础设施，统一构建器与校验脚本可显著降低外部资产接入成本，应配套文档与示例形成标准接入路径。

6/10-add hfield-mesh contact vertex and sdf mode switch（ed1c934）
  - 评分：6/10
  - 一句话总结：新增 hfield-mesh 接触顶点与 SDF 模式切换，扩展地形与网格混合接触能力。
  - 提交时间：2026-09-07
  - 变更规模：+62 / -4
  - 提交者：huangtaikai
  - 解决的问题：地形（heightfield）与网格（mesh）之间的接触缺少顶点级处理与 SDF 模式选择，限制复杂地形场景精度。
  - 产品启示：地形-网格混合接触是户外与崎岖地形仿真的刚需，SDF 模式切换提供了精度与性能的折中手段，可作为地形仿真卖点。

6/10-example modification（9dd499c）
  - 评分：6/10
  - 一句话总结：新增 MPM 差分耦合与相关示例，扩展流体网格耦合能力。
  - 提交时间：2026-09-08
  - 变更规模：+3451 / -2216
  - 提交者：syq
  - 解决的问题：流体网格缺少差分耦合与梯度函数支持，MPM 与其他求解器的耦合示例不足。
  - 产品启示：MPM 差分耦合是软体、颗粒与流体统一仿真的重要拼图，示例化有助于用户快速验证耦合效果并降低上手门槛。

### ⚙️ 性能/架构优化
8/10-Remove WanPhys test suite and legacy particle-fluid implementations（bea6e5d）
  - 评分：8/10
  - 一句话总结：删除旧测试套件与遗留粒子流体实现，大幅削减近 2.9 万行代码。
  - 提交时间：2026-09-07
  - 变更规模：+511 / -28982
  - 提交者：Wei Wu
  - 解决的问题：遗留粒子流体实现与旧测试套件长期占用维护成本，与原生架构并存造成混淆。
  - 产品启示：主动删除过时实现是架构收敛的必要手段，可显著降低新贡献者的认知负担，但需确保回归覆盖已迁移至新框架。

8/10-Refactor CCD into pre and post two APIs（28d4245）
  - 评分：8/10
  - 一句话总结：将 CCD 重构为 pre/post 两套 API，明确连续碰撞检测的阶段边界。
  - 提交时间：2026-09-07
  - 变更规模：+694 / -735
  - 提交者：huangtaikai
  - 解决的问题：CCD 原有单一 API 混合预处理与后处理逻辑，职责不清，难以独立优化与复用。
  - 产品启示：pre/post 双 API 拆分提升了 CCD 的可组合性与可测试性，是碰撞管线走向模块化的关键一步，但需注意接口稳定性与下游适配。

8/10-Remove rigid Newton conversion hatches and VBD adapter（4d99bd7）
  - 评分：8/10
  - 一句话总结：移除刚体 Newton 转换逃生通道与 VBD 适配器，彻底切断刚体栈对 Newton 的依赖。
  - 提交时间：2026-09-09
  - 变更规模：+308 / -635
  - 提交者：Wei Wu
  - 解决的问题：刚体仍保留 Newton 转换入口与 VBD 适配器，形成隐性耦合，阻碍原生实现统一。
  - 产品启示：移除逃生通道是“去依赖”真正完成的标志，可避免双轨维护，但需以回归 pin 保证数值一致性。

8/10-Own ContactData and the Contacts-buffer writer（1ef04e0）
  - 评分：8/10
  - 一句话总结：WanPhys 自主持有 ContactData 与 Contacts 缓冲写入器，掌握接触数据所有权。
  - 提交时间：2026-09-09
  - 变更规模：+204 / -37
  - 提交者：Wei Wu
  - 解决的问题：接触数据与缓冲写入依赖外部实现，导致数据布局与生命周期不可控。
  - 产品启示：接触数据所有权是碰撞管线自主可控的核心，直接影响性能调优与调试能力，是架构自主化的关键节点。

8/10-Own WanPhys Contacts buffers for collision pipelines（680b90f）
  - 评分：8/10
  - 一句话总结：碰撞管线全面使用 WanPhys 自有 Contacts 缓冲，统一缓冲管理。
  - 提交时间：2026-09-09
  - 变更规模：+187 / -21
  - 提交者：Wei Wu
  - 解决的问题：碰撞管线缓冲归属分散，CCD 与 rigid 管线各自管理，易产生不一致与冗余拷贝。
  - 产品启示：统一缓冲所有权可减少数据搬运与内存开销，为后续批处理与性能基准提供一致基础。

7/10-Simplify CCD pipeline ownership and event sweep（efd25b1）
  - 评分：7/10
  - 一句话总结：简化 CCD 管线所有权与事件扫描逻辑，降低复杂度。
  - 提交时间：2026-09-07
  - 变更规模：+709 / -984
  - 提交者：huangtaikai
  - 解决的问题：CCD 管线所有权与事件扫描逻辑冗余，配置与内核定义分散，维护成本高。
  - 产品启示：净删除代码的简化重构有助于降低回归风险，事件扫描简化对 CCD 性能与可调试性均有正向作用。

7/10-Fix native rigid inertials and refresh self-regression pins（743935e）
  - 评分：7/10
  - 一句话总结：修复原生刚体惯量计算并刷新自回归基线 pin。
  - 提交时间：2026-09-08
  - 变更规模：+175 / -26
  - 提交者：Wei Wu
  - 解决的问题：原生刚体惯量计算存在偏差，且回归 pin 未同步更新，影响数值一致性校验。
  - 产品启示：惯量正确性直接决定刚体动力学可信度，及时刷新回归 pin 是保证基准有效性的必要动作。

7/10-Point collision kernels at native enums and owned math helpers（ddaef55）
  - 评分：7/10
  - 一句话总结：碰撞内核改用原生枚举与自有数学工具，消除对外部枚举与数学库的依赖。
  - 提交时间：2026-09-09
  - 变更规模：+120 / -84
  - 提交者：Wei Wu
  - 解决的问题：碰撞内核仍引用外部枚举与数学辅助，造成命名与语义不一致。
  - 产品启示：内核层统一到原生枚举与数学工具有助于长期可维护性与跨模块一致性，是去依赖的收尾工作。

6/10-Organize rigid tests under unittest and remove bespoke guard（eb1e964）
  - 评分：6/10
  - 一句话总结：将刚体测试纳入 unittest 组织并移除专用守卫脚本。
  - 提交时间：2026-09-08
  - 变更规模：+1748 / -1984
  - 提交者：Wei Wu
  - 解决的问题：刚体测试组织分散，依赖专用守卫脚本，测试入口不统一。
  - 产品启示：测试组织标准化有利于 CI 集成与贡献者上手，移除专用守卫可减少脚本维护负担。

### 🧰 Bug修复 / 其他
- 7/10-Fix native rigid inertials and refresh self-regression pins（743935e）
  - 评分：7/10
  - 一句话总结：修复原生刚体惯量并刷新回归 pin，保障数值一致性。
  - 提交时间：2026-09-08
  - 变更规模：+175 / -26
  - 提交者：Wei Wu
  - 解决的问题：原生刚体惯量计算错误导致动力学结果偏差，回归基线未同步。
  - 产品启示：惯量修复属于底层正确性问题，配合回归 pin 刷新可形成可追踪的数值保障机制。
