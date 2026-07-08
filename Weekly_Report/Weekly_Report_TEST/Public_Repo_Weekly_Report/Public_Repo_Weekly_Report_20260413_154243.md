# 具身智能周报 (2026年04月13日 15:42:43)

## 行业风向总览

本周具身智能行业的技术焦点主要集中在仿真环境的性能提升与功能增强上。在`mujocolab/mjlab`仓库中，新增了对执行器粘性阻尼的支持，增强了物理模型的真实性和可控性，同时通过增加自动重置配置标志和简化API设计，提高了用户体验。而`google-deepmind/mujoco`则引入了稀疏雅可比矩阵的时间导数计算方法，大幅提升了复杂动力学问题的处理效率，并且通过重构代码结构进一步优化了系统架构。此外，尽管没有直接提到合成数据相关动态，但上述改进间接促进了更高效、更真实的仿真数据生成能力。对于产品经理而言，这些变化意味着可以期待更加灵活、高效及易于使用的仿真工具，有助于加速产品迭代周期并提高最终产品的质量。

---

## 各仓库详细分析

### [mujocolab/mjlab] 具身智能周报

#### 趋势点评
本周的更新延续了mjlab仓库长期聚焦于提升仿真环境性能、稳定性和功能丰富性的趋势。特别是通过引入新的配置选项和改进执行器的行为，进一步增强了系统对于复杂机器人行为的支持能力。此外，这些改动也体现了项目团队致力于提高代码质量和用户体验的一贯努力。

#### 关键更新解析
##### 🚀 新功能/特性
- <font color="red">**[8分]** 添加`viscous_damping`到`ActuatorCfg`：[https://github.com/mujocolab/mjlab/commit/1e2ffa0240f702c51123dfcf082b3e4f2f4e9705]</font>
  - 变更规模: +3696 -3133 行
  - 提交者: @Kevin Zakka
  - 解决的问题: 此提交增加了对执行器粘性阻尼的支持，使得模拟更加真实且可控。
  - 产品启示: 这一增强为研究者提供了更多调整物理模型参数的空间，有助于开发出更加逼真的仿真场景。

- **[6分]** 增加自动重置配置标志：[https://github.com/mujocolab/mjlab/commit/cda6e9dd1a9eab555bbec38019a4aee99d60ad76]
  - 变更规模: +230 -24 行
  - 提交者: @Kevin Zakka
  - 解决的问题: 该功能允许用户自定义何时重置仿真环境，提高了灵活性。
  - 产品启示: 自动化与个性化设置相结合，可以简化实验流程并加速迭代过程。

- **[6分]** 默认将执行器臂架和摩擦损失设为None：[https://github.com/mujocolab/mjlab/commit/72e2ee0c49276e396195993b916dc403ae3b7e63]
  - 变更规模: +167 -35 行
  - 提交者: @Kevin Zakka
  - 解决的问题: 通过移除不必要的默认值设置，减少了潜在的混淆点，并简化了API。
  - 产品启示: 更简洁明了的设计有助于降低新用户的入门门槛，同时保持高级功能的可用性。

（由于本周没有明显的性能优化或示例/环境更新类别的提交，故省略相关部分。）

---

以上就是本周[mujocolab/mjlab]仓库的关键进展概览。可以看出，该项目正持续地向着成为更强大、灵活的研究工具方向前进。

---

### [google-deepmind/mujoco] 具身智能周报

#### 趋势点评
本周的更新延续了 `google-deepmind/mujoco` 仓库长期专注于提升物理引擎性能与渲染技术的趋势，同时进一步增强了用户体验和系统兼容性。通过优化核心算法、重构代码结构以及新增功能特性，项目团队不仅提升了系统的运行效率，还简化了开发者的使用流程，为未来的扩展打下了坚实的基础。

#### 关键更新解析
##### 🚀 新功能/特性
- <font color="red">**[8分]** 实现稀疏雅可比矩阵时间导数：[https://github.com/google-deepmind/mujoco/commit/025ba59fab44294e2bd90a05d7307b0a500192d3]</font>
  - 变更规模: +220 -18 行
  - 提交者: @Yuval Tassa
  - 解决的问题: 通过引入稀疏雅可比矩阵的时间导数计算方法，显著提高了物理模拟中的计算效率。
  - 产品启示: 此次改进将使得Mujoco在处理复杂动力学问题时更加高效，有助于提高模拟精度和速度，从而为用户提供更好的体验。

- [7分] 暴露Drawable Material以允许用户直接操作：[https://github.com/google-deepmind/mujoco/commit/26fb65c7a7a22dc2856ae3135e9d2adaf4fe17d1]
  - 变更规模: +25 -30 行
  - 提交者: @Haroon Qureshi
  - 解决的问题: 为开发者提供了更灵活的方式来定制材质属性，增强了图形渲染的自定义程度。
  - 产品启示: 这一变化意味着用户能够更容易地调整视觉效果，增加了软件的灵活性和可用性，对于追求高质量可视化效果的应用场景尤为重要。

- [7分] 在Mujoco Warp shims中添加`com_pos`：[https://github.com/google-deepmind/mujoco/commit/cc0933af8b4c73b6a06fc32d0595fbf13e520bd9]
  - 变更规模: +204 -0 行
  - 提交者: @Tom Power
  - 解决的问题: 扩展了mujoco_warp的功能集，使其能够支持更多类型的物理计算。
  - 产品启示: 增加了对质心位置的支持，这将有利于需要精确控制物体平衡或运动轨迹的应用程序。

##### ⚡️ 性能/架构优化
- [6分] 优化`mj_tendonBias`函数：[https://github.com/google-deepmind/mujoco/commit/f114ea803819cc3181a3b9d304c1936c330819f1]
  - 变更规模: +22 -34 行
  - 提交者: @Yuval Tassa
  - 解决的问题: 通过直接计算Jdot * qvel代替原有方法，减少了不必要的计算步骤，提升了执行效率。
  - 产品启示: 此类微小但重要的优化累积起来可以显著改善整体性能，确保了即使在高负载下也能保持流畅运行。

- <font color="red">**[8分]** 将SceneView拆分为两个部分：SceneView和SceneBridge：[https://github.com/google-deepmind/mujoco/commit/edc807895f065d454b6c99214edff3dceeba7945]</font>
  - 变更规模: +680 -445 行
  - 提交者: @Haroon Qureshi
  - 解决的问题: 通过分离关注点，使得代码更加模块化，便于维护及后续开发。
  - 产品启示: 代码结构上的改进通常不会直接影响最终用户，但它对于长期项目健康至关重要，有助于吸引贡献者并加快新特性的开发速度。

- [6分] 移除Material对象对ObjectManager的依赖：[https://github.com/google-deepmind/mujoco/commit/f6baacfa86a73a395c7689297778e2ed4a5f7250]
  - 变更规模: +99 -66 行
  - 提交者: @Haroon Qureshi
  - 解决的问题: 简化了材料管理机制，减少了不必要的间接引用，提高了代码清晰度。
  - 产品启示: 更简洁的设计有助于降低学习曲线，使新手更容易上手，同时也方便了现有用户的日常使用。

- [6分] 将flex/skin网格创建移至ModelObjects内：[https://github.com/google-deepmind/mujoco/commit/c6a434a408d7cb8a7ff679c9bffbc3e7d9a8cf4f]
  - 变更规模: +135 -180 行
  - 提交者: @Haroon Qureshi
  - 解决的问题: 通过集中相关逻辑到一个地方，增强了代码的一致性和可读性。
  - 产品启示: 统一资源管理方式有助于减少潜在错误的发生率，并且使得API更加直观易用。

- [6分] 将UpdateMeshData移动到model_objects.cc文件中：[https://github.com/google-deepmind/mujoco/commit/87b0ea785e18f4230a3a3379ed71cc3ee0a911cf]
  - 变更规模: +364 -395 行
  - 提交者: @Haroon Qureshi
  - 解决的问题: 重新组织了数据更新流程，使得整个过程更加透明可控。
  - 产品启示: 改进后的架构有助于提高开发效率，同时也有利于未来的扩展工作。

##### 🧪 示例/环境更新
- [6分] 更新dcmotor相关的文档和示例：[https://github.com/google-deepmind/mujoco/commit/81720071b816d57598bbb438383e3ff259faabb9]
  - 变更规模: +335 -85 行
  - 提交者: @Yuval Tassa
  - 解决的问题: 为新加入的dcmotor执行器提供了详尽的操作指南和参考案例。
  - 产品启示: 高质量的文档是促进社区增长的关键因素之一，它可以帮助新用户快速掌握如何利用这些新功能来实现自己的创意。

- [6分] 重构Flex相关字段直接暴露于mjx.Model上：[https://github.com/google-deepmind/mujoco/commit/05e26e961c3c9e61dceb4f0c0fe7ca94d8e4ffe0]
  - 变更规模: +12 -19 行
  - 提交者: @Tom Power
  - 解决的问题: 通过直接访问模型内的Flex属性，简化了编程接口。
  - 产品启示: 减少不必要的封装层级可以使代码更加直观易懂，从而提高开发效率。

---

### [isaac-sim/IsaacLab] 本周无高价值更新（≥6分）。

#### 📊 提交分析
- 本周总提交: 2 条
- 高价值提交: 0 条
- 代码更新规模: +39 / -1 行
- 主要贡献者: bixiong wang, Kelly Guo

#### 🧭 趋势点评
本周共有 2 条常规提交，主要涉及代码维护与小幅优化，无值得重点关注的功能或性能更新。


---

