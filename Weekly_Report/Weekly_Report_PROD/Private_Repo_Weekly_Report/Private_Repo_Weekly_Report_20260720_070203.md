# WanPhys Weekly Report (2026-07-20 07:02:03)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-07-20 07:02:03
- 分析窗口: 最近 7 天
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 8/10-Migrate examples to native WanPhys lifecycle（e5b06b2）
  - 提交者：Wei Wu
  - 提交时间：2026-07-17
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/__init__.py
  - 新增：wanphys/examples/_lifecycle.py
  - 修改：wanphys/examples/broad_phase_benchmark.py
  - 新增：wanphys/examples/catalog.py
  - 修改：wanphys/examples/fluid_grid_apic.py
  - 修改：wanphys/examples/fluid_grid_basic.py
  - 修改：wanphys/examples/fluid_grid_complex_model.py
  - 修改：wanphys/examples/fluid_grid_liquid.py
  - 修改：wanphys/examples/fluid_grid_liquid_coupling.py
  - 修改：wanphys/examples/fluid_grid_liquid_robot.py
  - 修改：wanphys/examples/fluid_grid_mpm.py
  - 修改：wanphys/examples/fluid_grid_mpm_liquid_coupling.py
  - 修改：wanphys/examples/fluid_grid_resolution_particle.py
  - 修改：wanphys/examples/fluid_grid_resolution_voxel.py
  - 修改：wanphys/examples/fluid_grid_sparse.py
  - 修改：wanphys/examples/point_cloud_demo.py
  - 修改：wanphys/examples/rigid_basic_shapes.py
  - 修改：wanphys/examples/rigid_bunny_in_box.py
  - 修改：wanphys/examples/rigid_falling_bodies.py
  - 修改：wanphys/examples/rigid_fluid_gated_benchmark.py
  - 修改：wanphys/examples/rigid_mesh_ccd.py
  - 修改：wanphys/examples/rigid_pendulum.py
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
  - 修改：wanphys/examples/sensors/example_sensor_contact.py
  - 修改：wanphys/examples/sensors/example_sensor_frame_transform.py
  - 修改：wanphys/examples/sensors/example_sensor_imu.py
  - 修改：wanphys/examples/sensors/example_sensor_tactile_image.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_fluid.py
  - 修改：wanphys/examples/soft/vbd_cloth_bending.py
  - 修改：wanphys/examples/utils.py
  - 新增：wanphys/examples/validation.py

- 4/10-docs: refresh WanPhys documentation（a9a1be7）
  - 提交者：Wei Wu
  - 提交时间：2026-07-16
  - 修改：wanphys/examples/README.md

- 9/10-move soft collision to collision pipeline, update runtime func call（96e6314）
  - 提交者：huangtaikai
  - 提交时间：2026-07-14
  - 修改：wanphys/examples/broad_phase_benchmark.py
  - 修改：wanphys/examples/rigid_fluid_gated_benchmark.py

#### 📊 提交分析
- 本周总提交: 4 条
- 高价值提交（≥6分）: 3 条
- 代码更新规模: +7277 / -14982 行
- 主要贡献者: Wei Wu, huangtaikai

## 📈 趋势点评

本周的更新高度契合了仓库长期以来的核心演进方向，即“性能优化与架构重构并重”。将软碰撞移至碰撞管线（96e6314）是对碰撞检测模块的又一次重大重构，延续了自5月以来对CCD管线、资源管理和求解器解耦的持续优化趋势。同时，将示例迁移至原生生命周期（e5b06b2）以及更新Newton导入桥接（9c0f9be），则体现了团队在清理技术债务、减少模块耦合、提升代码可维护性方面的持续努力，这与仓库基线中“推进代码重构与模块解耦”的未来方向完全一致。

## 📌 关键更新解析

### ⚙️ 性能/架构优化

9/10-move soft collision to collision pipeline, update runtime func call（96e6314）
  - **评分**：9/10
  - **一句话总结**：将软碰撞逻辑整合到统一的碰撞管线中，并更新了运行时函数调用，是一次重大的架构重构。
  - **提交时间**：2026-07-14
  - **变更规模**：+2919 / -7051
  - **提交者**：huangtaikai
  - **解决的问题**：解决了软碰撞与现有碰撞管线分离、代码冗余及运行时调用效率低下的问题，通过统一管线提升了代码的可维护性和执行效率。
  - **产品启示**：此重构将显著提升软体与刚体交互场景的仿真性能与稳定性，为未来更复杂的软体-刚体耦合仿真（如机器人抓取软体物体）奠定了更坚实的基础。

8/10-Migrate examples to native WanPhys lifecycle（e5b06b2）
  - **评分**：8/10
  - **一句话总结**：将大量示例代码迁移至使用WanPhys原生的生命周期管理，影响范围广泛。
  - **提交时间**：2026-07-17
  - **变更规模**：+2463 / -605
  - **提交者**：Wei Wu
  - **解决的问题**：解决了示例代码与核心库生命周期管理不一致的问题，降低了用户学习和使用WanPhys的门槛，并减少了因生命周期不匹配导致的潜在错误。
  - **产品启示**：此举极大改善了开发者体验，使示例代码更具参考价值和可复用性，有助于吸引更多社区用户和贡献者，加速生态建设。

7/10-update newton import bridge and projective_cloth collision import（9c0f9be）
  - **评分**：7/10
  - **一句话总结**：更新了Newton求解器的导入桥接，并调整了projective_cloth碰撞模块的导入路径。
  - **提交时间**：2026-07-14
  - **变更规模**：+749 / -334
  - **提交者**：huangtaikai
  - **解决的问题**：解决了因代码重构导致的Newton依赖导入失败和模块引用错误问题，确保了碰撞模块与外部求解器（Newton）的兼容性。
  - **产品启示**：持续清理对第三方库（如Newton）的依赖，是提升项目独立性和可移植性的关键步骤。此更新确保了在移除依赖过程中的平稳过渡，避免功能回退。
