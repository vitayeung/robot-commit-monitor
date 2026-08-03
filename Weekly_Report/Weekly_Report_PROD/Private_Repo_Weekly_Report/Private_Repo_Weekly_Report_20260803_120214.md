# WanPhys Weekly Report (2026-08-03 12:02:14)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-08-03 12:02:14
- 分析窗口: 最近 7 天
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 9/10-mpm diff（8bf10c2）
  - 提交者：syq
  - 提交时间：2026-07-30
  - 新增：wanphys/examples/fluid_grid_mpm_diff_skip_stone.py
  - 新增：wanphys/examples/fluid_grid_mpm_fish_drift.py

- 8/10-add heightfield wave and granule algorithm modules to WanPhys（f3c3573）
  - 提交者：dreliveam
  - 提交时间：2026-07-30
  - 新增：wanphys/examples/heightfield/__init__.py
  - 新增：wanphys/examples/heightfield/dynamic_heightfield.py
  - 新增：wanphys/examples/heightfield/granular_balls_rigid.py
  - 新增：wanphys/examples/heightfield/granular_hill_bunny_rigid.py
  - 新增：wanphys/examples/heightfield/granular_png_hill_rigid.py
  - 新增：wanphys/examples/heightfield/granular_png_terrain_rigid.py

- 5/10-improve tactile sensor cascade example（d996305）
  - 提交者：FYTalon
  - 提交时间：2026-07-28
  - 修改：wanphys/examples/sensors/example_sensor_tactile_image.py

- 6/10-replace sensor example Newton dependencies（93a13e9）
  - 提交者：FYTalon
  - 提交时间：2026-07-28
  - 修改：wanphys/examples/sensors/example_sensor_contact.py
  - 修改：wanphys/examples/sensors/example_sensor_frame_transform.py
  - 修改：wanphys/examples/sensors/example_sensor_imu.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_fluid.py

- 8/10-refactor native sensors and soft tactile sensing（7c03a6c）
  - 提交者：FYTalon
  - 提交时间：2026-07-28
  - 修改：wanphys/examples/sensors/example_sensor_tactile_image.py

#### 📊 提交分析
- 本周总提交: 5 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +13630 / -4700 行
- 主要贡献者: FYTalon, syq, dreliveam

## 📈 趋势点评

本周更新延续了 WanPhys 在 2026 年 6 月至 7 月期间的核心演进方向——性能优化与架构解耦，同时也在新功能模块上持续发力。具体来看，`8bf10c2` 新增 MPM 可微求解器，与前期流体算法（非牛顿流体、表面张力、APIC 优化）的扩展路径一脉相承，进一步丰富了流体仿真能力；`f3c3573` 新增高度场波动与颗粒算法模块，呼应了此前对地形与颗粒物理的探索，属于新物理域的横向拓展。在架构层面，`7c03a6c` 对传感器模块进行大规模重构并引入光线追踪，延续了 3 月以来传感器模块持续迭代的长期趋势，而 `93a13e9` 移除传感器示例对 Newton 的依赖，则与 6 月以来反复出现的“去 Newton 化”主线高度一致。整体来看，本周提交既保持了新功能的高频输出，也坚定推进了性能优化与依赖解耦的长期战略，未出现偏离主线的异常动向。

## 📌 关键更新解析

### 🌟 新功能/特性

9/10-mpm diff（8bf10c2）
- **评分**：9/10
- **一句话总结**：新增 MPM 可微求解器，扩展流体仿真能力。
- **提交时间**：2026-07-30
- **变更规模**：+4661 / -193
- **提交者**：syq
- **解决的问题**：此前 WanPhys 的流体仿真主要基于 APIC 和粒子显式方法，缺乏可微的 MPM（Material Point Method）求解能力，限制了梯度信息在流体仿真中的获取与利用。该提交新增了 MPM 可微求解器，填补了这一空白。
- **产品启示**：可微物理仿真能力是具身智能中“可学习物理引擎”的关键基础设施。MPM 可微求解器的引入，使得下游任务（如策略优化、轨迹规划、参数辨识）可以直接利用流体仿真的梯度信息，为机器人操作液体、颗粒物等场景提供了更强大的仿真支撑，有望显著提升仿真到现实的迁移效率。

8/10-add heightfield wave and granule algorithm modules to WanPhys（f3c3573）
- **评分**：8/10
- **一句话总结**：新增高度场波动与颗粒算法模块，丰富地形仿真能力。
- **提交时间**：2026-07-30
- **变更规模**：+3975 / -0
- **提交者**：dreliveam
- **解决的问题**：此前 WanPhys 缺乏对高度场地形和颗粒介质的原生支持，机器人在复杂地形（如沙地、碎石坡）上的仿真场景难以构建。该提交新增了高度场波动和颗粒算法模块，填补了地形与颗粒物理仿真的空白。
- **产品启示**：高度场与颗粒模块的加入，使 WanPhys 能够覆盖更多非结构化环境（如沙滩、矿山、农田等）的仿真需求。对于足式机器人、轮式机器人在松软地形上的通过性分析、轨迹优化等应用，该模块提供了关键的物理支撑，拓展了仿真平台的场景覆盖面。

### ⚙️ 性能/架构优化

8/10-refactor native sensors and soft tactile sensing（7c03a6c）
- **评分**：8/10
- **一句话总结**：重构传感器模块，引入光线追踪，提升传感器模拟性能。
- **提交时间**：2026-07-28
- **变更规模**：+4428 / -4138
- **提交者**：FYTalon
- **解决的问题**：此前传感器模块（尤其是触觉图像传感器）依赖 Newton 后端，且仿真效率存在瓶颈。该提交对传感器模块进行原生重构，引入光线追踪技术，并优化了触觉传感的几何计算（如包围盒计算），提升了传感器模拟的性能与精度。
- **产品启示**：触觉传感器是具身智能中“灵巧操作”的核心感知来源。通过原生重构和光线追踪加速，传感器模拟的实时性和精度得到显著提升，使得大规模触觉数据采集和仿真训练成为可能，为机器人精细操作（如抓取、装配）的策略学习提供了更高质量的感知反馈。

6/10-replace sensor example Newton dependencies（93a13e9）
- **评分**：6/10
- **一句话总结**：移除传感器示例对 Newton 的依赖，促进模块解耦。
- **提交时间**：2026-07-28
- **变更规模**：+175 / -80
- **提交者**：FYTalon
- **解决的问题**：传感器示例代码中仍存在对 Newton 后端的依赖，与项目“去 Newton 化”的长期方向不符，增加了维护成本和集成复杂度。该提交将传感器示例中的 Newton 依赖替换为 WanPhys 原生实现，推动模块独立。
- **产品启示**：减少对特定第三方后端的依赖，意味着 WanPhys 的传感器模块可以更独立地运行和演进，降低了用户集成的门槛。对于外部开发者而言，更纯净的依赖关系意味着更低的编译成本和更少的兼容性问题，有助于吸引更多社区贡献者参与传感器生态的建设。
