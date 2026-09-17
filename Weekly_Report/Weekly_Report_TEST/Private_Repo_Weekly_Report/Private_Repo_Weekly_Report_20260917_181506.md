# WanPhys Weekly Report (2026-09-17 18:15:06)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-09-17 18:15:06
- 统计截止: 2026-09-17 18:15:06
- 分析窗口: 最近 7 天（截止上述时间）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 1/10-Import JointType from the public selection facade（3510a75）
  - 提交者：Wei Wu
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py

- 3/10-Promote Gaussian camera examples to current catalog smoke（0fa9f77）
  - 提交者：Wei Wu
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/catalog.py

- 5/10-Export Gaussian camera types from wanphys.sensors（66a5a2f）
  - 提交者：Wei Wu
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian_fluid.py

- 2/10-Fix native mesh loading in MPM skip-stone example（56b3209）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py

- 4/10-Make Gaussian plant interaction the default demo（30384da）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py

- 6/10-Download example assets as independent model packages（6816fc4）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/README.md
  - 修改：wanphys/examples/point_cloud_demo.py
  - 修改：wanphys/examples/utils.py

- 5/10-Fix example asset loading and smoke validation issues（f7f9502）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/fluid_grid_mpm_diff_skip_stone_mass.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_diff_skip_stone.py
  - 修改：wanphys/examples/fluids/fluid_grid_mpm_fish_drift.py
  - 修改：wanphys/examples/robot/example_task2_robot2.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_fluid.py
  - 修改：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py

- 5/10-Support grouped example asset packages with stable file names（c27d3d4）
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

- 9/10-Add native Gaussian sensor rendering and standalone demos（89a1d89）
  - 提交者：FYTalon
  - 提交时间：2026-09-15
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian.py
  - 新增：wanphys/examples/sensors/example_sensor_tiled_camera_gaussian_fluid.py

- 8/10-ccd unify fixed mesh and convex queries, update BFS response（07e9b09）
  - 提交者：huangtaikai
  - 提交时间：2026-09-13
  - 修改：wanphys/examples/rigid_mesh_ccd.py

- 7/10-collision localization, not totally refactor（c6c56d2）
  - 提交者：give-lab
  - 提交时间：2026-09-13
  - 修改：wanphys/examples/robot/example_robot_panda_hydro.py

#### 📊 提交分析
- 本周总提交: 25 条
- 高价值提交（≥6分）: 9 条
- 代码更新规模: +24166 / -26138 行
- 主要贡献者: Wei Wu, FYTalon, give-lab, huangtaikai

## 📈 趋势点评
本周（2026-09-13 至 2026-09-15）的高价值提交延续了仓库自 2026-09 以来“资产外置与性能基准规范化”的主线，并进一步向传感器原生渲染与碰撞管线统一两个方向深化。一方面，`89a1d89` 以超过一万行的新增代码落地原生 Gaussian 传感器渲染，标志着传感器栈从依赖 Newton 后端向自研后端迁移的关键一步，与基线中“原生传感器与渲染能力大幅扩展”的趋势高度一致；另一方面，`07e9b09`、`c6c56d2`、`cc12e3a` 等提交集中对 CCD 查询、碰撞定位与软体接触辅助进行统一与重构，呼应了基线中“碰撞检测体系持续重构与增强”以及“软体碰撞迁入碰撞管线”的长期方向。`f38ff15` 与 `6816fc4` 则延续了 9 月资产外置与原生包下载的工程化治理路径，大幅削减仓库体积。此外，`6b8f6ab`、`34d0aad`、`27e010a` 等 SDF 相关修复补齐了稀疏/粗 SDF 边界采样与柔性接触面构建，属于对既有几何与碰撞能力的精细化打磨。整体来看，本周更新未偏离仓库长期趋势，而是在传感器原生渲染、碰撞管线统一、资产解耦三条主线上同步推进，性能与架构优化类提交占比突出，符合基线中“能力扩张与性能治理并行”的判断。

## 📌 关键更新解析

### 🌟 新功能/特性
9/10-Add native Gaussian sensor rendering and standalone demos（89a1d89）
  - 评分：9/10
  - 一句话总结：新增原生 Gaussian 传感器渲染能力并配套独立演示，推动传感器栈向自研后端迁移。
  - 提交时间：2026-09-15
  - 变更规模：+10058 / -14
  - 提交者：FYTalon
  - 解决的问题：此前传感器渲染依赖 Newton 后端，缺乏原生 Gaussian 渲染支持与独立可运行示例。
  - 产品启示：原生高斯渲染的落地强化了 WanPhys 在传感器仿真与渲染一体化上的竞争力，为后续触觉、相机等多模态传感器原生后端扩展奠定基础。

6/10-fix: 补齐柔性接触面 SDF 构建并标注待重构范围（27e010a）
  - 评分：6/10
  - 一句话总结：补齐柔性接触面的 SDF 构建逻辑，并明确标注后续待重构范围。
  - 提交时间：2026-09-13
  - 变更规模：+512 / -5
  - 提交者：give-lab
  - 解决的问题：柔性接触面缺乏完整 SDF 构建支持，影响软体碰撞的几何表示完整性。
  - 产品启示：柔性接触 SDF 的补齐提升了软体仿真的几何精度，待重构标注也为后续模块化治理提供了清晰路径。

6/10-Download example assets as independent model packages（6816fc4）
  - 评分：6/10
  - 一句话总结：支持将示例资产作为独立模型包下载，改善示例资产分发体验。
  - 提交时间：2026-09-15
  - 变更规模：+180 / -79
  - 提交者：FYTalon
  - 解决的问题：示例资产此前耦合在仓库中，缺乏独立包下载机制，影响跨环境集成与仓库体积控制。
  - 产品启示：独立模型包下载机制降低了用户获取示例资产的门槛，配合资产外置策略提升了示例生态的可维护性。

### ⚙️ 性能/架构优化
8/10-ccd unify fixed mesh and convex queries, update BFS response（07e9b09）
  - 评分：8/10
  - 一句话总结：统一 CCD 中固定网格与凸体查询接口，并更新 BFS 响应逻辑。
  - 提交时间：2026-09-13
  - 变更规模：+3508 / -5400
  - 提交者：huangtaikai
  - 解决的问题：CCD 中固定网格与凸体查询接口分散、BFS 响应逻辑不统一，导致维护成本高且易产生不一致。
  - 产品启示：查询接口统一显著精简了 CCD 代码路径，为后续 TOI 回退与岛屿影响处理的进一步优化提供一致基础。

8/10-Externalize runtime assets and add native package downloads（f38ff15）
  - 评分：8/10
  - 一句话总结：将运行时资产外置并支持原生包下载，大幅削减仓库体积与加载开销。
  - 提交时间：2026-09-15
  - 变更规模：+1092 / -18025
  - 提交者：FYTalon
  - 解决的问题：运行时资产内嵌导致仓库体积庞大、加载路径耦合，影响分发与跨环境集成效率。
  - 产品启示：资产外置与原生包下载机制是仓库工程化治理的关键一步，有助于降低仓库体积并统一资产加载路径。

7/10-collision localization, not totally refactor（c6c56d2）
  - 评分：7/10
  - 一句话总结：对碰撞模块进行定位式重构，明确模块边界而非全面重写。
  - 提交时间：2026-09-13
  - 变更规模：+5447 / -206
  - 提交者：give-lab
  - 解决的问题：碰撞模块职责边界模糊，CCD 内核与接触逻辑分散，影响可维护性与扩展性。
  - 产品启示：定位式重构在控制风险的前提下理顺了碰撞模块结构，为后续统一碰撞管线调用路径提供支撑。

6/10-Share one particle-rigid contact helper in collision.soft（cc12e3a）
  - 评分：6/10
  - 一句话总结：在 collision.soft 中统一粒子-刚体接触辅助函数，消除重复实现。
  - 提交时间：2026-09-13
  - 变更规模：+17 / -280
  - 提交者：Wei Wu
  - 解决的问题：粒子-刚体接触逻辑在软体碰撞中重复实现，导致代码冗余与维护成本上升。
  - 产品启示：接触辅助函数的统一精简了软体碰撞代码，提升了软体与刚体接触处理的一致性。

### 🧰 Bug修复 / 其他
6/10-fix: 修正稀疏 SDF 边界的距离与梯度采样（6b8f6ab）
  - 评分：6/10
  - 一句话总结：修正稀疏 SDF 边界处的距离与梯度采样错误。
  - 提交时间：2026-09-13
  - 变更规模：+105 / -17
  - 提交者：give-lab
  - 解决的问题：稀疏 SDF 在边界处的距离与梯度采样不准确，影响碰撞检测精度。
  - 产品启示：采样修正提升了稀疏 SDF 在边界场景下的数值稳定性，对依赖 SDF 的碰撞与接触仿真有直接收益。

6/10-fix: 修正粗 SDF 边界的距离与梯度采样（34d0aad）
  - 评分：6/10
  - 一句话总结：修正粗 SDF 边界处的距离与梯度采样错误。
  - 提交时间：2026-09-13
  - 变更规模：+140 / -24
  - 提交者：give-lab
  - 解决的问题：粗 SDF 在边界处的距离与梯度采样不准确，可能导致接触检测偏差。
  - 产品启示：与稀疏 SDF 修正配套，共同提升 SDF 接触在多种分辨率下的数值可靠性。
