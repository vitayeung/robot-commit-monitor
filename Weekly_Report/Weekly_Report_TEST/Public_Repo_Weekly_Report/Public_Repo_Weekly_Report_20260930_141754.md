# 具身智能周报 (2026年09月30日 14:17:54)

- 统计窗口: 2026-09-21 08:54:25 +0800 至 2026-09-30 14:17:54 +0800（左闭右开）

## 行业风向总览

本周具身智能风向聚焦仿真训练底座的稳定性与工具链升级。技术焦点上，mjlab 修复伪惯量随机化与 Jacobi 特征求解器边界问题，强化域随机化数值可靠性；地形课程改按 episode 指令距离判定，推动课程学习向任务语义驱动演进。合成数据方面，本周无直接动态，但域随机化边界校验的完善间接提升合成训练数据质量。产品经理需关注：上游工具链（Python 3.14、torch 2.14、CUDA 13）迁移节奏加快，兼容性维护成本上升；课程设计应围绕任务目标语义而非仅环境反馈，以提升训练可解释性。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 📊 提交分析
- 本周总提交: 6 条
- 高价值提交（≥6分）: 4 条
- 代码更新规模: +1762 / -1077 行
- 主要贡献者: Kevin Zakka, 상티 (윤상현)

## 🧭 趋势点评
本周更新延续了 mjlab 在 2026-09 至 2026-10 期间“稳定性收敛与工具链升级并行”的主线：一方面，`dr.pseudo_inertia` 与 Jacobi 特征求解器的修复继续强化域随机化与数值计算的边界正确性，呼应了此前对 NaN、形状校验和缓存一致性的密集打磨；另一方面，Python 3.14、torch 2.14 与 CUDA 13 的迁移则延续了仓库高频跟进上游生态的长期策略，与此前 mujoco/mujoco-warp 3.10/3.11、rsl-rl-lib 5.5.0 的升级节奏一致。地形课程改用 episode 指令距离判定，则进一步体现了项目从“固定难度推进”向“任务语义驱动课程”的演进，符合近期对课程确定性、指标语义和训练可观测性的持续投入。整体来看，本周并未偏离基线趋势，而是在数值稳健性、平台兼容性和训练课程语义三个既有方向上继续深化。

## 🔍 关键更新解析

### 🚀 新功能/特性
9/10-Add Python 3.14 support and move to torch 2.14 with CUDA 13. (#1194)（4ac9df2）
  - 评分：9
  - 一句话总结：新增 Python 3.14 支持，并迁移至 torch 2.14 与 CUDA 13，覆盖 CI、nightly、Makefile、安装文档与 pyproject 配置。
  - 链接：https://github.com/mujocolab/mjlab/commit/4ac9df2f1d67de4aad62c4a38b27c84b04268bbe
  - 变更规模：+1486 -1018
  - 提交者：Kevin Zakka
  - 解决的问题：解决项目工具链滞后于 Python 3.14、torch 2.14 与 CUDA 13 生态的问题，避免用户在新平台上安装或运行受阻。
  - 产品启示：持续跟进上游工具链可提升仓库对最新研究环境的适配度，但大版本迁移需同步强化 CI 与安装文档，以降低兼容性断裂风险。

7/10-Judge the terrain curriculum against the distance the episode commanded (#1188)（c2e1e06）
  - 评分：7
  - 一句话总结：地形课程改为根据 episode 指令距离判定，而非仅依赖实际行进结果，并同步更新课程文档、速度指令与相关测试。
  - 链接：https://github.com/mujocolab/mjlab/commit/c2e1e06400e309b6897a536693fe5d2aa772c5b2
  - 变更规模：+157 -18
  - 提交者：Kevin Zakka
  - 解决的问题：修复地形课程判定与实际任务指令脱节的问题，使课程推进更符合速度任务中“指令距离”的语义。
  - 产品启示：课程学习应围绕任务目标语义设计，而非仅依赖环境反馈，这有助于提升训练稳定性和任务可解释性。

### ⚡️ 性能/架构优化
- 无符合条件的提交。

### 🐛 Bug修复 / 其他
6/10-Keep massless bodies unchanged in dr.pseudo_inertia and reject log_uniform. (#1199)（f135c1d）
  - 评分：6
  - 一句话总结：在 `dr.pseudo_inertia` 中保留无质量刚体不变，并拒绝 `log_uniform` 采样，避免非法伪惯量随机化。
  - 链接：https://github.com/mujocolab/mjlab/commit/f135c1daa0f278bd19e323c2b9f256ca541ae2c5
  - 变更规模：+64 -11
  - 提交者：Kevin Zakka
  - 解决的问题：修复伪惯量随机化对无质量刚体处理不当以及 `log_uniform` 可能产生非法输入的问题。
  - 产品启示：域随机化边界条件需要显式校验，否则容易在训练中引入静默错误，影响动力学一致性与复现性。

6/10-Fix Jacobi eigensolver skipping rotation when diagonal entries are equal. (#1198)（c1b937f）
  - 评分：6
  - 一句话总结：修复 Jacobi 特征求解器在对角元素相等时跳过旋转的问题，提升特征分解数值正确性。
  - 链接：https://github.com/mujocolab/mjlab/commit/c1b937fc3038df9ce22c4fdf8132c4ef5f0cb304
  - 变更规模：+13 -2
  - 提交者：Kevin Zakka
  - 解决的问题：解决 Jacobi 特征求解器在特定对角元素条件下跳过必要旋转、导致结果不准确的问题。
  - 产品启示：底层数值算法虽改动小，但会直接影响随机化与动力学计算可靠性，应持续通过测试覆盖边界条件。

---

