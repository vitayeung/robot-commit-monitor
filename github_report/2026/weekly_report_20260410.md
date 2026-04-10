# 具身智能周报 (2026年04月10日)

## 行业风向总览

本周具身智能行业的技术焦点主要集中在运控和仿真加速上。在mujocolab/mjlab仓库中，新增了`viscous_damping`到ActuatorCfg，增强了执行器行为的控制精度；同时引入RecorderManager简化数据收集流程，提升了研究工具的价值。google-deepmind/mujoco则通过优化物理计算、支持多插件集成等措施进一步强化了用户体验与系统兼容性。合成数据方面，虽然没有直接更新，但上述改进为生成更高质量的合成数据提供了基础。对于产品经理而言，这些更新不仅提高了系统的稳定性和效率，还增加了定制化选项，使得仿真环境更加贴近实际应用需求，特别是在机器人设计和复杂任务训练场景中尤为重要。此外，isaac-sim/IsaacLab针对多GPU训练问题提供了详细的故障排除文档，这有助于降低技术门槛，提升开发者的使用体验。

---

### [mujocolab/mjlab] 具身智能周报

#### 趋势点评
本周的更新延续了仓库长期聚焦于性能优化、功能丰富性和用户体验改进的趋势。通过引入新的actuator配置选项、数据收集管理器以及增强训练策略等新特性，同时对现有代码进行优化和清理，这些提交不仅提升了系统的稳定性和效率，还为用户提供了更多定制化和研究的可能性。

#### 关键更新解析
##### 🚀 新功能/特性
- **新增`viscous_damping`到ActuatorCfg**：[链接](https://github.com/mujocolab/mjlab/commit/1e2ffa0240f702c51123dfcf082b3e4f2f4e9705)
  - 解决的问题：允许用户更精细地控制执行器的行为，特别是在模拟真实世界中的阻尼效应时。
  - 产品启示：这使得仿真环境更加贴近实际物理情况，对于需要高度逼真度的应用场景（如机器人设计）尤为重要。

- **添加RecorderManager用于下游数据收集**：[链接](https://github.com/mujocolab/mjlab/commit/9423e02ed6ff45b87c3437398140e582d084bbb0)
  - 解决的问题：简化了实验过程中数据记录的过程，并提高了数据管理的一致性和可访问性。
  - 产品启示：增强了平台作为研究工具的价值，特别是对于那些依赖大量实验数据来验证假设或训练模型的研究者来说非常有用。

- **引入终止课程表以实现分阶段终止参数调度**：[链接](https://github.com/mujocolab/mjlab/commit/f7fdb163b590e980865e59a5633ff5e1143553bd)
  - 解决的问题：提供了一种灵活的方法来调整学习过程中的终止条件，有助于提高强化学习算法的学习效率。
  - 产品启示：这种灵活性可以加速某些类型任务的学习曲线，对于开发高效且适应性强的AI系统至关重要。

- **在dr.pair_friction中增加isotropic参数**：[链接](https://github.com/mujocolab/mjlab/commit/a0971d4a13e0c828fee336ce1c6a3f163e38b69e)
  - 解决的问题：扩展了摩擦力随机化的范围，使模拟环境能够更好地反映现实世界的多样性。
  - 产品启示：这对于测试机器人的鲁棒性和泛化能力特别有帮助，确保它们能够在各种条件下表现良好。

##### ⚡️ 性能/架构优化
- **将默认actuator armature和frictionloss设置为None**：[链接](https://github.com/mujocolab/mjlab/commit/72e2ee0c49276e396195993b916dc403ae3b7e63)
  - 解决的问题：通过减少不必要的默认值设置，简化了代码逻辑并可能略微提高了性能。
  - 产品启示：虽然这是一个小改动，但它体现了项目团队致力于持续改善代码质量和运行效率的态度。

- **修复ghost geom过滤逻辑以使用视觉alpha而不是碰撞标志**：[链接](https://github.com/mujocolab/mjlab/commit/76aca41d57eaed335934b92a5b6a4643cde0a5ec)
  - 解决的问题：解决了之前版本中存在的视觉显示问题，使得仿真环境看起来更加自然。
  - 产品启示：良好的视觉效果对于提升用户体验非常重要，尤其是在涉及到复杂图形渲染的应用中。

- **当实体XML <option>字段在场景附加期间被丢弃时发出警告**：[链接](https://github.com/mujocolab/mjlab/commit/1676703d3e8d36e2a1de0d487ed9d3c8d14ad7fa)
  - 解决的问题：通过及时通知用户潜在的数据丢失风险，提高了系统的透明度。
  - 产品启示：这种类型的反馈机制可以帮助开发者更快地识别并解决问题，从而加快开发周期。

- **清理文档字符串**：[链接](https://github.com/mujocolab/mjlab/commit/c139f9fa8d4d050cc7a7b3afdc6e1580fae0361a)
  - 解决的问题：改善了代码库内部文档的质量，使其更容易理解和维护。
  - 产品启示：清晰的文档是任何开源项目成功的关键因素之一，它促进了社区参与和技术传播。

- **更新mujoco-warp至最新版本**：[链接](https://github.com/mujocolab/mjlab/commit/984d54b91410eda2b60dff414e66dbeb7e9ac13c)
  - 解决的问题：保持与上游库同步，确保能够利用最新的性能改进和bug修复。
  - 产品启示：定期更新依赖项有助于维持项目的竞争力，并确保其能够支持最前沿的技术发展。

---

### [google-deepmind/mujoco] 具身智能周报

#### 趋势点评
本周的更新延续了`google-deepmind/mujoco`仓库长期专注于提升物理引擎性能与渲染技术的趋势，同时进一步增强了用户体验和系统兼容性。通过引入稀疏雅可比矩阵时间导数、优化物理计算以及重构部分代码结构等措施，项目团队继续深化其在高性能计算领域的探索，并为用户提供更加流畅且功能丰富的模拟体验。

#### 关键更新解析
##### 🚀 新功能/特性
- **允许用户直接操作Drawable Material**：[链接](https://github.com/google-deepmind/mujoco/commit/26fb65c7a7a22dc2856ae3135e9d2adaf4fe17d1)
  - 解决的问题：增加了用户对材质属性的控制能力。
  - 产品启示：这使得开发者能够更灵活地定制视觉效果，从而提高模拟场景的真实感与吸引力。
  
- **支持同一编译单元中的多个插件**：[链接](https://github.com/google-deepmind/mujoco/commit/f2461f9ce65f80a725457caabad9491a4a1a3e26)
  - 解决的问题：简化了多插件集成过程。
  - 产品启示：降低了扩展Mujoco功能时的技术门槛，促进了社区创新。

- **添加com_pos到Mujoco Warp shims**：[链接](https://github.com/google-deepmind/mujoco/commit/cc0933af8b4c73b6a06fc32d0595fbf13e520bd9)
  - 解决的问题：增强了Warp接口的功能完整性。
  - 产品启示：有助于开发人员利用Warp进行更复杂的物理仿真任务。

- **暴露flex相关字段**：[链接](https://github.com/google-deepmind/mujoco/commit/05e26e961c3c9e61dceb4f0c0fe7ca94d8e4ffe0)
  - 解决的问题：提高了API的透明度。
  - 产品启示：便于开发者理解和使用Flex相关的高级功能。

- **更新dcmotor文档和功能**：[链接](https://github.com/google-deepmind/mujoco/commit/81720071b816d57598bbb438383e3ff259faabb9)
  - 解决的问题：完善了dcmotor执行器的说明及其实现。
  - 产品启示：帮助用户更好地理解和应用这一新型执行器。

- **将Mesh创建移到ModelObjects**：[链接](https://github.com/google-deepmind/mujoco/commit/c6a434a408d7cb8a7ff679c9bffbc3e7d9a8cf4f)
  - 解决的问题：改善了模型对象管理逻辑。
  - 产品启示：简化了模型构建流程，提升了开发效率。

- **重命名RenderTargetAndTextures为RenderTarget**：[链接](https://github.com/google-deepmind/mujoco/commit/f7fd5fc58bd214638f91592338f18c2c4dd04ecb)
  - 解决的问题：统一了命名规范。
  - 产品启示：减少了混淆，使代码更易于理解。

- **对dcmotor进行小改进**：[链接](https://github.com/google-deepmind/mujoco/commit/382474bb9dd1bd5fa248cba28bf965c5854e74c5)
  - 解决的问题：微调了dcmotor的行为。
  - 产品启示：确保了该组件在各种应用场景下的稳定表现。

##### ⚡️ 性能/架构优化
- **优化mj_tendonBias**：[链接](https://github.com/google-deepmind/mujoco/commit/f114ea803819cc3181a3b9d304c1936c330819f1)
  - 解决的问题：提高了肌腱偏置计算的速度。
  - 产品启示：加快了复杂生物力学模型的仿真速度。

- **实现稀疏雅可比矩阵时间导数**：[链接](https://github.com/google-deepmind/mujoco/commit/025ba59fab44294e2bd90a05d7307b0a500192d3)
  - 解决的问题：增强了求解器处理大规模问题的能力。
  - 产品启示：对于需要高精度仿真的工业级应用来说，这是一个重大进步。

- **防止已附加mjSpec的删除**：[链接](https://github.com/google-deepmind/mujoco/commit/6b724616c0d129aca57bf36778957d31e463a2fc)
  - 解决的问题：避免了潜在的数据丢失风险。
  - 产品启示：增强了系统的健壮性和可靠性。

- **改进CMake构建流程**：[链接](https://github.com/google-deepmind/mujoco

---

### [isaac-sim/IsaacLab] 具身智能周报

#### 趋势点评
本周的更新主要集中在文档改进上，特别是关于多GPU训练时遇到的问题解决方案。虽然这与项目长期聚焦于增强仿真环境稳定性和功能性、强化学习算法集成等核心技术的发展方向略有不同，但通过改善开发者体验和减少技术障碍，间接支持了这些核心目标的实现。这种类型的更新反映了项目对社区反馈的关注以及致力于提高整体用户体验的努力。

#### 关键更新解析
##### 🚀 新功能/特性
- 无

##### ⚡️ 性能/架构优化
- 无

##### 🧪 示例/环境更新
- 无

##### 📚 文档更新
- **添加NCCL故障排除笔记以帮助解决多GPU训练问题**：[链接](https://github.com/isaac-sim/IsaacLab/commit/4df6560e187f2cc66685b41b21b259f4485d0c22)
  - 解决的问题：为那些在使用NVIDIA Collective Communications Library (NCCL)进行多GPU训练时遇到困难的用户提供指导。
  - 产品启示：随着越来越多的研究者和工程师采用更复杂的硬件配置来加速模型训练过程，提供清晰且易于理解的技术支持变得尤为重要。此更新不仅有助于现有用户解决问题，还可能吸引更多潜在用户尝试利用IsaacSim平台的强大功能。

---

