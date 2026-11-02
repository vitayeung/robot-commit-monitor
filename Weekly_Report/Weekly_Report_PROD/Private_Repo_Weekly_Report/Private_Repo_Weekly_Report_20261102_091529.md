# WanPhys Weekly Report (2026-11-02 09:15:29)

- 仓库: WanPhysTeam/WanPhys
- 生成时间: 2026-11-02 09:15:50
- 统计截止: 2026-11-02 09:15:29
- 分析窗口: 2026-10-26 09:18:43 +0800 至 2026-11-02 09:15:29 +0800（左闭右开）
- 扫描分支: dev

### [WanPhysTeam/WanPhys] 具身智能周报

#### 🧩 Example 文件变更分析
- 3/10-Release liquid coupling bodies from first frame（8772d04）
  - 提交者：FYTalon
  - 提交时间：2026-10-31
  - 修改：wanphys/examples/fluids/fluid_grid_liquid_coupling.py

- 2/10-Disable the TCP debug print by default（b5fddfc）
  - 提交者：yiyang-zju
  - 提交时间：2026-10-29
  - 修改：wanphys/examples/robot_fold_cloth1.py

- 7/10-Add dual-arm T-shirt folding demo（9aa49fa）
  - 提交者：yiyang-zju
  - 提交时间：2026-10-29
  - 新增：wanphys/examples/robot_fold_cloth1.py

- 6/10-Expand dev benchmark list to 16 non-fluid cases（682a67a）
  - 提交者：FYTalon
  - 提交时间：2026-10-27
  - 修改：wanphys/examples/TEST_README.md
  - 新增：wanphys/examples/references/main16/one_step/basic.example_basic_heightfield.json
  - 新增：wanphys/examples/references/main16/one_step/basic.example_basic_joints.json
  - 新增：wanphys/examples/references/main16/one_step/basic.example_basic_pendulum.json
  - 新增：wanphys/examples/references/main16/one_step/basic.example_basic_shapes.json
  - 新增：wanphys/examples/references/main16/one_step/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/main16/one_step/cloth.example_cloth_bending.json
  - 新增：wanphys/examples/references/main16/one_step/contacts.example_nut_bolt_hydro.xpbd.json
  - 新增：wanphys/examples/references/main16/one_step/contacts.example_nut_bolt_sdf.xpbd.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_policy.json
  - 新增：wanphys/examples/references/main16/one_step/robot.example_robot_ur10.json
  - 新增：wanphys/examples/references/main16/one_step/selection.example_selection_articulations.json
  - 新增：wanphys/examples/references/main16/perf600/basic.example_basic_heightfield.json
  - 新增：wanphys/examples/references/main16/perf600/basic.example_basic_joints.json
  - 新增：wanphys/examples/references/main16/perf600/basic.example_basic_pendulum.json
  - 新增：wanphys/examples/references/main16/perf600/basic.example_basic_shapes.json
  - 新增：wanphys/examples/references/main16/perf600/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/main16/perf600/cloth.example_cloth_bending.json
  - 新增：wanphys/examples/references/main16/perf600/contacts.example_nut_bolt_hydro.xpbd.json
  - 新增：wanphys/examples/references/main16/perf600/contacts.example_nut_bolt_sdf.xpbd.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_policy.json
  - 新增：wanphys/examples/references/main16/perf600/robot.example_robot_ur10.json
  - 新增：wanphys/examples/references/main16/perf600/selection.example_selection_articulations.json
  - 修改：wanphys/examples/references/wanperf600_manifests/cloth.example_cloth_bending.json
  - 修改：wanphys/examples/references/wanperf600_manifests/selection.example_selection_articulations.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/README.md

- 2/10-Simplify main14 test commands（41404e3）
  - 提交者：FYTalon
  - 提交时间：2026-10-27
  - 修改：wanphys/examples/TEST_README.md

- 8/10-Add Newton 1.0 one-step parity and main14 benchmarks（ba04ca3）
  - 提交者：FYTalon
  - 提交时间：2026-10-27
  - 新增：wanphys/examples/TEST_README.md
  - 新增：wanphys/examples/basic/example_basic_conveyor.py
  - 新增：wanphys/examples/basic/example_basic_heightfield.py
  - 修改：wanphys/examples/basic/example_basic_pendulum.py
  - 修改：wanphys/examples/basic/example_basic_shapes.py
  - 修改：wanphys/examples/basic/example_basic_urdf.py
  - 修改：wanphys/examples/catalog.py
  - 新增：wanphys/examples/contacts/__init__.py
  - 新增：wanphys/examples/contacts/_nut_bolt_common.py
  - 新增：wanphys/examples/contacts/example_nut_bolt_hydro.py
  - 新增：wanphys/examples/contacts/example_nut_bolt_sdf.py
  - 新增：wanphys/examples/references/main14/one_step/basic.example_basic_heightfield.json
  - 新增：wanphys/examples/references/main14/one_step/basic.example_basic_joints.json
  - 新增：wanphys/examples/references/main14/one_step/basic.example_basic_pendulum.json
  - 新增：wanphys/examples/references/main14/one_step/basic.example_basic_shapes.json
  - 新增：wanphys/examples/references/main14/one_step/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/main14/one_step/contacts.example_nut_bolt_hydro.xpbd.json
  - 新增：wanphys/examples/references/main14/one_step/contacts.example_nut_bolt_sdf.xpbd.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_policy.json
  - 新增：wanphys/examples/references/main14/one_step/robot.example_robot_ur10.json
  - 新增：wanphys/examples/references/main14/perf600/basic.example_basic_heightfield.json
  - 新增：wanphys/examples/references/main14/perf600/basic.example_basic_joints.json
  - 新增：wanphys/examples/references/main14/perf600/basic.example_basic_pendulum.json
  - 新增：wanphys/examples/references/main14/perf600/basic.example_basic_shapes.json
  - 新增：wanphys/examples/references/main14/perf600/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/main14/perf600/contacts.example_nut_bolt_hydro.xpbd.json
  - 新增：wanphys/examples/references/main14/perf600/contacts.example_nut_bolt_sdf.xpbd.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_policy.json
  - 新增：wanphys/examples/references/main14/perf600/robot.example_robot_ur10.json
  - 修改：wanphys/examples/references/one_step.py
  - 新增：wanphys/examples/references/wanperf600_manifests/basic.example_basic_heightfield.json
  - 修改：wanphys/examples/references/wanperf600_manifests/basic.example_basic_joints.json
  - 修改：wanphys/examples/references/wanperf600_manifests/basic.example_basic_pendulum.json
  - 修改：wanphys/examples/references/wanperf600_manifests/basic.example_basic_shapes.json
  - 修改：wanphys/examples/references/wanperf600_manifests/basic.example_basic_urdf.json
  - 新增：wanphys/examples/references/wanperf600_manifests/contacts.example_nut_bolt_hydro.xpbd.json
  - 新增：wanphys/examples/references/wanperf600_manifests/contacts.example_nut_bolt_sdf.xpbd.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_anymal_c_walk.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_anymal_d.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_cartpole.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_g1.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_h1.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_policy.json
  - 修改：wanphys/examples/references/wanperf600_manifests/robot.example_robot_ur10.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/README.md
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_conveyor.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_heightfield.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_joints.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_pendulum.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_shapes.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/basic.example_basic_urdf.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_bending.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/cloth.example_cloth_hanging.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/contacts.example_nut_bolt_hydro.mujoco.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/contacts.example_nut_bolt_hydro.xpbd.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/contacts.example_nut_bolt_sdf.mujoco.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/contacts.example_nut_bolt_sdf.xpbd.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_allegro_hand.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_c_walk.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_c_walk.mujoco-external.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_d.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_anymal_d.mujoco-external.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_cartpole.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_g1.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_g1.mujoco-external.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_h1.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_h1.mujoco-external.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_humanoid.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.anymal-mjw.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.anymal-physx.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.g1_23dof-mjw.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.g1_23dof-physx.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.go2-mjw.json
  - 新增：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.go2-physx.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_policy.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/robot.example_robot_ur10.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_articulations.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_cartpole.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/selection.example_selection_materials.json
  - 修改：wanphys/examples/references/wanreg_onestep_manifests/sensors.example_sensor_contact.json
  - 修改：wanphys/examples/robot/example_robot_allegro_hand.py
  - 修改：wanphys/examples/robot/example_robot_anymal_c_walk.py
  - 修改：wanphys/examples/robot/example_robot_anymal_d.py
  - 修改：wanphys/examples/robot/example_robot_cartpole.py
  - 修改：wanphys/examples/robot/example_robot_g1.py
  - 修改：wanphys/examples/robot/example_robot_h1.py
  - 修改：wanphys/examples/robot/example_robot_policy.py

#### 📊 提交分析
- 本周总提交: 7 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +92577 / -340 行
- 主要贡献者: FYTalon, yiyang-zju

## 📈 趋势点评

本周高价值提交延续了仓库“碰撞/求解内核确定性收敛 + 基准回归体系化 + 机器人操作示例扩展”的长期主线，并进一步向跨引擎一致性验证倾斜：Newton 1.0 单步 parity 与 main14/main16 基准的引入，把此前分散的数值回归与性能清单工作（b0cfe9e、f8b2d45、2d8262b）推进为可对照上游实现的常态化基准矩阵，属于对既有趋势的强化而非偏离。双臂 T 恤折叠演示及其资产补齐则延续了触觉级联、流体耦合等复杂操作示例的扩张路径，但单次引入 8.7 万行资产也放大了仓库体积与资产外置策略之间的张力，提示示例生态扩张需与 f38ff15 的资产外置、原生包下载机制更好协同。

## 📌 关键更新解析

### 🌟 新功能/特性

8/10-Add Newton 1.0 one-step parity and main14 benchmarks（ba04ca3）
- 评分：8/10
- 一句话总结：新增 Newton 1.0 单步一致性校验与 main14 基准集，为跨引擎数值对齐提供可复现基线。
- 提交时间：2026-10-27
- 变更规模：+3906 / -304
- 提交者：FYTalon
- 解决的问题：此前缺乏与 Newton 1.0 的单步 parity 对照，跨引擎数值一致性无法量化验证，基准用例口径也不统一。
- 产品启示：可将单步 parity 作为 CI 门禁的跨引擎一致性检查项，配合 main14 基准形成分层基准矩阵，强化“仿真结果可复现”的产品卖点。

7/10-Add dual-arm T-shirt folding demo（9aa49fa）
- 评分：7/10
- 一句话总结：新增双臂 T 恤折叠核心演示脚本，扩展机器人柔性物体操作示例覆盖。
- 提交时间：2026-10-29
- 变更规模：+1544 / -0
- 提交者：yiyang-zju
- 解决的问题：仓库缺少双臂协同操作可变形衣物的端到端演示，柔性操作场景验证不足。
- 产品启示：双臂折衣可作为高保真操作示例沉淀为回归用例，向用户展示复杂柔性操作能力，但需关注其运行开销与基准清单的纳入方式。

6/10-Add dual-arm T-shirt folding demo with required assets（4ef018c）
- 评分：6/10
- 一句话总结：补齐双臂折衣演示所需的 T 恤与 Franka 机械臂网格资产，体量巨大。
- 提交时间：2026-10-29
- 变更规模：+87045 / -0
- 提交者：yiyang-zju
- 解决的问题：演示脚本缺少配套网格与材质资产，无法开箱运行。
- 产品启示：大体积二进制资产应优先走 f38ff15 的资产外置与原生包下载路径，避免仓库膨胀，同时需明确资产版本与下载失败时的降级策略。

### ⚙️ 性能/架构优化

6/10-Expand dev benchmark list to 16 non-fluid cases（682a67a）
- 评分：6/10
- 一句话总结：开发基准列表扩展至 16 个非流体用例，并新增 main16 单步参考结果。
- 提交时间：2026-10-27
- 变更规模：+77 / -16
- 提交者：FYTalon
- 解决的问题：原有基准覆盖不足，非流体用例的数值回归缺乏足够样本与参考快照。
- 产品启示：基准扩容提升回归灵敏度，但会改变历史可比口径，需在 TEST_README 中明确版本化基准集，避免跨版本性能数据误比。

### 🧰 Bug修复 / 其他

本周无评分≥6的 Bug修复/其他类提交。
