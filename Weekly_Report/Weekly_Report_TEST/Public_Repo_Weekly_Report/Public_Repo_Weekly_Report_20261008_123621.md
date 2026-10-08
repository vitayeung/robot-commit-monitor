# 具身智能周报 (2026年10月08日 12:36:21)

- 统计窗口: 2026-09-30 14:17:54 +0800 至 2026-10-08 12:36:21 +0800（左闭右开）

## 行业风向总览

本周具身智能风向聚焦仿真训练中的“静默错误”治理：mjlab 集中修复速度命令初始化顺序、坐标系规则覆盖及 DelayBuffer 在部分重置、共享 lag、首步采样等边界场景的一致性，强调时序与数值稳定。合成数据方面无直接新增，但延迟缓冲与命令语义的精细化修正，实质提升 sim-to-real 观测建模的可复现性。产品经理应关注：命令模块需显式定义规则应用顺序与多模式优先级；缓冲组件须明确共享粒度与首步契约，并将部分重置一致性纳入回归测试。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 8 条
- 高价值提交（≥6分）: 5 条
- 代码更新规模: +400 / -36 行
- 主要贡献者: Kevin Zakka, vssingh, 상티 (윤상현)

## 🧭 趋势点评
本周的更新高度聚焦于**速度命令（velocity command）与延迟缓冲（DelayBuffer）的语义与时序正确性修复**，这与仓库长期趋势中“问题修复占比高、时序与数值稳定性是持续投入方向”的判断完全一致。具体来看，`bd37751` 与 `c5adfae` 延续了 2026-10 以来对命令初始化顺序和坐标系规则覆盖问题的修正主线，而 `4f73291`、`58ad841`、`fb32300` 三条提交则集中打磨 DelayBuffer 在部分重置、共享 lag 与首步采样等边界场景下的一致性，呼应了此前 `4f73291` 所代表的“保持共享 DelayBuffer 的 lag 与 schedule 在部分重置间一致”的演进方向。整体上，本周并未偏离仓库基线，而是继续在观测/命令/缓冲这类“静默错误高发区”做精细化收敛，且每条修复均配套测试文件变更，体现出对回归防护的重视。

## 🔍 关键更新解析

### 🚀 新功能/特性
（本周无符合该分类的高价值提交）

### ⚡️ 性能/架构优化
（本周无符合该分类的高价值提交）

### 🐛 Bug修复 / 其他

7/10-Apply standing, heading and world-frame rules before init_velocity_prob (#1215)（bd37751）
  - 评分：7/10
  - 一句话总结：将站立、朝向与世界坐标系规则的判定提前到 `init_velocity_prob` 之前应用，修正速度命令初始化顺序。
  - 链接：https://github.com/mujocolab/mjlab/commit/bd37751b15af90863c5a84cbbc24653a4edd985c
  - 变更规模：+88 -17
  - 提交者：Kevin Zakka
  - 解决的问题：此前速度命令的初始化顺序有误，导致站立、朝向与世界坐标系规则在 `init_velocity_prob` 之后才生效，可能产生不符合预期的初始速度指令。
  - 产品启示：命令初始化顺序直接影响策略训练初期的行为分布，此类顺序性修复能显著降低训练早期的不稳定性，建议将“规则应用顺序”纳入命令模块的显式契约与测试覆盖。

7/10-Keep the shared DelayBuffer lag and schedule across partial resets. (#1206)（4f73291）
  - 评分：7/10
  - 一句话总结：确保共享 DelayBuffer 的 lag 与调度在部分重置（partial resets）之间保持一致。
  - 链接：https://github.com/mujocolab/mjlab/commit/4f7329183f097baa93af6e21e7e9241fc45bf978
  - 变更规模：+34 -4
  - 提交者：Kevin Zakka
  - 解决的问题：部分重置场景下共享 DelayBuffer 的 lag 与调度状态未能保持一致，可能造成观测延迟语义在环境间错位。
  - 产品启示：延迟缓冲是 sim-to-real 观测建模的关键组件，其在部分重置下的状态一致性直接关系到训练与部署的可复现性，应作为回归测试的固定项。

6/10-Stop heading and world frame commands from overriding rel_forward_envs (#1214)（c5adfae）
  - 评分：6/10
  - 一句话总结：阻止 heading 与世界坐标系命令覆盖 `rel_forward_envs` 的相对前向设置。
  - 链接：https://github.com/mujocolab/mjlab/commit/c5adfae3a61fe2c81e4b84d066da8f0c80faf7a2
  - 变更规模：+48 -0
  - 提交者：vssingh
  - 解决的问题：heading 与世界坐标系命令会错误地覆盖 `rel_forward_envs` 的相对前向语义，导致相对前向任务的命令被污染。
  - 产品启示：多命令模式共存时需明确优先级与互斥规则，避免不同坐标系语义相互覆盖，这对多任务/多模式速度控制的可组合性至关重要。

6/10-Share the hold decision across envs in shared-lag DelayBuffer (#1191)（58ad841）
  - 评分：6/10
  - 一句话总结：在共享 lag 的 DelayBuffer 中，将 hold 决策在多个环境间共享。
  - 链接：https://github.com/mujocolab/mjlab/commit/58ad84162acb91b7dac3dfbc4ba646b74c009431
  - 变更规模：+45 -8
  - 提交者：상티 (윤상현)
  - 解决的问题：共享 lag 模式下各环境的 hold 决策不一致，破坏了共享延迟语义的一致性。
  - 产品启示：共享缓冲的“决策共享”语义需与 lag 共享保持一致，否则会引入难以复现的观测偏差，提示缓冲模块需明确共享粒度。

6/10-Sample DelayBuffer lags on the first step after creation or reset (#1203)（fb32300）
  - 评分：6/10
  - 一句话总结：在创建或重置后的第一步即对 DelayBuffer 的 lag 进行采样。
  - 链接：https://github.com/mujocolab/mjlab/commit/fb32300d93042695452bdce8bdab86eff840bad5
  - 变更规模：+48 -2
  - 提交者：Edson
  - 解决的问题：创建或重置后的首步未及时采样 lag，导致延迟缓冲在首个时间步使用陈旧或未初始化的延迟值。
  - 产品启示：缓冲类组件的“首步语义”常被忽视，却直接影响 episode 起始阶段的观测正确性，建议将首步采样纳入初始化契约。

---

