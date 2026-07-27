# mujocolab/mjlab Release Roadmap Reference

- 仓库: `mujocolab/mjlab`
- 对应主报告: `mujocolab_mjlab_release_roadmap.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要 + tagged README/docs/examples/configs/高信号源码证据
- 版本总数: 10
- 正式版数量: 9
- 预发布版数量: 1
- 外链文档覆盖版本数: 3
- compare 摘要覆盖版本数: 9
- 最新版本: v1.5.2 (2026-07-18 00:59:02 CST)
- 最早纳入统计版本: v0.1.0 (2025-09-29 18:00:45 CST)

## 分析策略决策
- 请求模式: `auto`
- 最终策略: `L2: Source-enhanced`
- 证据充分性评分: 2/6
- 触发规则: linked_docs_weak, migration_risk_high
- 决策说明:
  - 采用条件、生态信号和破坏性变更更依赖仓库内证据，默认启用源码增强。
  - 证据充分性评分 2/6，触发规则: linked_docs_weak, migration_risk_high。
  - 因此主脚本自动升级为 L2，补充 tagged README/docs/examples/configs/高信号源码证据。

## Release 时间线
- 2026-07-18 00:59:02 CST | v1.5.2 | 正式版
- 2026-07-16 01:15:38 CST | v1.5.1 | 正式版
- 2026-06-29 07:09:19 CST | v1.5.0 | 正式版
- 2026-05-27 06:52:20 CST | v1.4.0 | 正式版
- 2026-04-15 06:05:30 CST | v1.3.0 | 正式版
- 2026-03-07 06:22:37 CST | v1.2.0 | 正式版
- 2026-02-15 09:55:52 CST | v1.1.1 | 正式版
- 2026-02-13 13:41:02 CST | v1.1.0 | 正式版
- 2026-01-29 13:38:09 CST | v1.0.0 | 正式版
- 2025-09-29 18:00:45 CST | v0.1.0 | 预发布版

## 证据附录

### v1.5.2
- 标题: mjlab v1.5.2
- 类型: 正式版
- 发布时间: 2026-07-18 00:59:02 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.5.2
- GitHub release body:
Fixes multi-env domain-randomization crashes (`actuator_acc0`) and ignored `MaterialCfg.reflectance`.
- Compare 摘要: v1.5.1 -> v1.5.2
  - commits: 3
  - files changed: 8
  - additions: 54
  - deletions: 9
  - top directories: CITATION.cff, docs/source, pyproject.toml, src/mjlab, tests, uv.lock
  - representative files:
    - tests/test_events.py (modified, +29/-0)
    - docs/source/changelog.rst (modified, +14/-1)
    - CITATION.cff (modified, +3/-3)
    - src/mjlab/managers/event_manager.py (modified, +3/-2)
    - docs/source/randomization.rst (modified, +2/-1)
    - pyproject.toml (modified, +1/-1)
    - uv.lock (modified, +1/-1)
    - src/mjlab/utils/spec_config.py (modified, +1/-0)

### v1.5.1
- 标题: mjlab v1.5.1
- 类型: 正式版
- 发布时间: 2026-07-16 01:15:38 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.5.1
- GitHub release body:
This is a small compatibility and bugfix release. The headline is that mjlab now requires MuJoCo Warp 3.10.0.2, which fixes `qfrc_constraint` being populated incorrectly across vectorized environments (#1086). Earlier 3.10.0.x releases are no longer supported.

Full changelog: https://github.com/mujocolab/mjlab/compare/v1.5.0...v1.5.1
- Compare 摘要: v1.5.0 -> v1.5.1
  - commits: 15
  - files changed: 37
  - additions: 1596
  - deletions: 108
  - top directories: .github, CITATION.cff, README.md, docs/source, pyproject.toml, src/mjlab
  - representative files:
    - tests/test_fused_group.py (added, +364/-0)
    - src/mjlab/actuator/fused_group.py (added, +223/-0)
    - tests/test_rl_exporter.py (modified, +164/-1)
    - tests/test_domain_randomization.py (modified, +121/-0)
    - tests/test_spec_config.py (modified, +104/-0)
    - src/mjlab/actuator/dc_actuator.py (modified, +56/-33)
    - src/mjlab/actuator/actuator.py (modified, +58/-8)
    - src/mjlab/rl/exporter_utils.py (modified, +52/-9)

### v1.5.0
- 标题: mjlab v1.5.0
- 类型: 正式版
- 发布时间: 2026-06-29 07:09:19 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.5.0
- GitHub release body:
This release moves mjlab onto MuJoCo and MuJoCo Warp 3.10, gives procedural terrain generation a broad pass for determinism and visual consistency, and corrects a longstanding staleness bug in motion tracking.

## MuJoCo 3.10

mjlab now depends on `mujoco` and `mujoco-warp` 3.10, both pinned from PyPI. The `py.mujoco.org` nightly index and the `mujoco-warp` git pin are gone, so dependency resolution no longer breaks when nightly wheels are garbage collected. `SimulationCfg.ls_parallel` is deprecated and now ignored, following the removal of parallel linesearch upstream.

## Terrain generation

Curriculum difficulty is now deterministic across rows and reaches its configured endpoints, making terrain curricula reproducible. Heightfields color by absolute height on a fixed diverging palette, so scenes read consistently across terrain types and low-amplitude noise no longer renders as high-contrast clutter. A family of difficulty-0 edge cases that produced empty borders, NaN colors, or outright compile failures is resolved, and `HfRandomUniformTerrainCfg` can now scale its noise with difficulty for curriculum training.

## Actuation and domain randomization

A new `BuiltinDcMotorActuator` wraps MuJoCo's native `<dcmotor>` with voltage, position, and velocity input modes, back-EMF, and optional thermal, LuGre, cogging, and inductance extensions. Material randomization gains `dr.mat_emission`, `dr.mat_specular`, `dr.mat_shininess`, and `dr.mat_texrepeat` for RGB rendering. Per-axis randomization events that target the same model field now compose instead of silently overwriting one another.

## Motion tracking

Motion tracking no longer re-anchors to a stale robot pose after a mid-episode resample. `MotionCommand` now refreshes simulation state before computing relative b...
- Compare 摘要: v1.4.0 -> v1.5.0
  - commits: 26
  - files changed: 66
  - additions: 4818
  - deletions: 1594
  - top directories: .github, CITATION.cff, Makefile, docs/source, pyproject.toml, scripts
  - representative files:
    - typings/mujoco/_enums.pyi (modified, +1722/-669)
    - tests/test_builtin_dcmotor_actuator.py (added, +653/-0)
    - typings/mujoco/_structs.pyi (modified, +203/-96)
    - src/mjlab/actuator/builtin_actuator.py (modified, +255/-11)
    - src/mjlab/terrains/primitive_terrains.py (modified, +173/-85)
    - uv.lock (modified, +149/-86)
    - tests/test_domain_randomization.py (modified, +142/-2)
    - typings/mujoco/_specs.pyi (modified, +131/-8)

### v1.4.0
- 标题: mjlab v1.4.0
- 类型: 正式版
- 发布时间: 2026-05-27 06:52:20 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.4.0
- GitHub release body:
mjlab 1.4.0 adds per-world mesh variants, a native implicit PD actuator, sensor-frame projected gravity, and stricter shape validation in reward, termination, and metrics managers. It also updates MuJoCo and mujoco-warp to 3.8 and fixes several issues around actuator delay, multi-node seeding, contact sensor frames, rough-terrain videos, and tracking metrics.

## MuJoCo 3.8

mjlab now uses MuJoCo 3.8 and requires mujoco-warp 3.8.0.3 or newer within the 3.8 series. The `multiccd` enable flag was removed upstream because it is now always enabled. If your config includes `"multiccd"` in `MujocoCfg.enableflags`, remove it.

## Per-World Mesh Variants

Batched simulations can now use different mesh assets for the same logical entity in different worlds. Define a `VariantEntityCfg` with named spec callables, then choose how worlds are assigned to variants:

```python
VariantEntityCfg(
    variants={
        "cube": make_cube_spec,
        "sphere": make_sphere_spec,
        "bunny": make_bunny_spec,
    },
    assignment={"cube": 0.5, "sphere": 0.3, "bunny": 0.2},
)
```

`assignment` can be:

- `None`, for a uniform assignment across variants
- a `dict[str, float]`, for weighted assignment
- a `Callable[[int], Sequence[int]]`, for a custom world-to-variant mapping

Variants must have the same kinematic structure: the same bodies, joints, and joint types. Mesh geoms may differ. Mesh-derived constants such as collision bounds, body inertials, subtree mass, and inverse weights are compiled per-variant and stored as per-world arrays in the Warp model. Domain randomization, the native viewer, the offscreen renderer, and the Viser viewer all use the assigned variant automatically.

Per-variant materials and textures are supported. Each variant can reference its own named materia...
- 外链文档摘录:
  - https://mujocolab.github.io/mjlab/main/source/entity/per_world_mesh.html
    worlds use different mesh assets for the same logical entity. World 0
    may simulate a cube, world 1 a sphere, world 2 a bowl. All worlds
    share the same compiled scene and the same body and joint structure;
    importmujocofrommjlab.entityimportEntityCfg,VariantEntityCfgdefmake_sphere_spec()->mujoco.MjSpec:spec=mujoco.MjSpec()mesh=spec.add_mesh(name="visual")mesh.make_sphere(subdivision=3)mesh.scale[:]=(0.05,)*3body=spec.worldbody.add_body(name="prop")body.add_freejoint()body.add_geom(type=mujoco.mjtGeom.mjGEOM_MESH,meshname="visual")returnspecdefmake_cone_spec()->mujoco.MjSpec:spec=mujoco.MjSpec()mesh=spec.add_mesh(name="visual")mesh.make_cone(nedge=16,radius=0.04)body=spec.worldbody.add_body(name="prop")body.add_freejoint()body.add_geom(type=mujoco.mjtGeom.mjGEOM_MESH,meshname="visual")returnspecobject_cfg=VariantEntityCfg(variants={"sphere":make_sphere_spec,"cone":make_cone_spec,},assignment={"cone":2.0},# twice as many cones as spheresinit_state=EntityCfg.InitialStateCfg(pos=(0.0,0.0,0.2)),)
    dict default to weight 1.0; omit
    primitive (non-mesh) geoms, and any actuators / sensors / tendons /
    name prefix on any element. Variant entities
    (not per-world), so a slot’s role is fixed across worlds by
    has 1 visual mesh geom and 2 collision mesh
    has 1 visual mesh geom
    and 4 collision mesh geoms on the same body.
    [coll]   sphere_col_0            [coll]   cone_col_0
    [coll]   sphere_col_1            [coll]   cone_col_1
    slot 0 plus four collision slots (the union of sphere’s two and
    cone’s four). At merge time, every variant’s mesh asset is added to
    The merged scene compiles once into a single canonical
    world W picks which compiled mesh each slot points at.
    reference compile. So if sphere’s collision geoms have
    adds a body that
    body.The prop body in the merged spec carries variant 0’s
    slot variant 0 doesn’t fill, a synthesized padding geom that has
    . Padding contributes nothing to
    and never affect the host compile’s inertial
    Per-world overrides come from per-variant source compiles.Even with the above, the merged-scene compile’s prop body inertia
    is only correct for variant 0. For every other variant, mjlab
    compiles that variant’s original source spec in isolation (one
    default to weight 1.0.
    across batch sizes (e.g. “world 0 is always variant 0, world 1 is
    always variant 1, regardless of how many envs I launch”), use a
    Variant assignment is fixed at
    >>>env.sim.world_to_variant["object"]tensor([0, 0, 0, 1, 1, 1, 1, 1, 1, 1])
    Stratified halves- first half is variant 0, second half is
    the per-world default array by environment, so a 10% mass scale
    applied across a batch containing a 100 g sphere variant and a 1 kg
    cube variant produces 10% perturbationsaround each variant’s own
    mass, not 10% of a shared template mass.
    the pseudo-inertia matrix factorization ofRucker and Wensing (2022). It is exact for any
    called; it is appropriate only for modeling a point mass added at the
    The native viewer, offscreen renderer, and Viser viewer all sync the
    compiles the merged scene once to produce the canonical
    then compiles each variant’s original (un-merged) source spec in
    fields. Each per-variant compile sees only that variant’s single body
    compiles. With multiple variant entities, compiles
    decouple across entities: two variant entities of 5 variants each cost
    compile takes around 1-2 ms, so a scene with 100 variants pays a few
    hundred milliseconds at startup and a scene with 1000 variants pays
    joint. Fixed-base variants are rejected; mocap auto-wrapping that
    are restored per-world during compile, but the
- Compare 摘要: v1.3.0 -> v1.4.0
  - commits: 61
  - files changed: 86
  - additions: 7804
  - deletions: 807
  - top directories: .github, AGENTS.md, CITATION.cff, Makefile, README.md, docs/source
  - representative files:
    - tests/test_variants.py (added, +1772/-0)
    - src/mjlab/entity/variants.py (added, +1442/-0)
    - src/mjlab/viewer/viser/scene.py (modified, +588/-0)
    - docs/source/entity/per_world_mesh.rst (added, +490/-0)
    - tests/test_builtin_pd_actuator.py (added, +468/-0)
    - uv.lock (modified, +212/-215)
    - src/mjlab/sensor/contact_sensor.py (modified, +158/-84)
    - tests/test_projected_gravity_sensor.py (added, +213/-0)

### v1.3.0
- 标题: mjlab v1.3.0
- 类型: 正式版
- 发布时间: 2026-04-15 06:05:30 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.3.0
- GitHub release body:
TLDR: A packed release with a viewer rebuilt on [mjviser](https://github.com/mujocolab/mjviser), a preset-based terrain system, simplified actuator configuration, and new MDP primitives like `RecorderManager` and `termination_curriculum`.

## Physics engine bump

mjlab 1.3.0 uses mujoco-warp 3.7.0.1 and mujoco 3.7.0.

## Viewer: Rebuilt on mjviser

The Viser viewer internals have been replaced with the standalone [mjviser](https://github.com/mujocolab/mjviser) package. Scene creation, mesh conversion, and overlay rendering (contacts, forces, inertia, tendons, joints, frames) now live in mjviser, while mjlab keeps debug visualization and warp tensor conversion in its `MjlabViserScene` subclass. The viewer exposes a new Visualization tab for overlay controls and a Groups tab for geom and site visibility.

https://github.com/user-attachments/assets/b42b33a6-bdbf-4e08-b956-3569083073f3

New panels and tabs:
- **Reward bar panel** showing horizontal bars for each reward term with a running mean over ~1 second
- **W&B run tab** for browsing recent runs and pulling checkpoints
- **Checkpoints tab** in play for hot-swapping checkpoints without restarting, with support for local directories and W&B runs
- **Motion reference scrubber** for tracking tasks
- **Per-pixel segmentation** camera data type for geom ID output alongside RGB and depth, with a new `Mjlab-Multi-Cube-Seg-Yam` task that uses it

## Terrain System, Revamped

Terrain configuration moves to a preset-based system with a new `@terrain_preset` decorator for composing reusable configurations. Curriculum mode now assigns exactly one column per terrain type, with `proportion` controlling robot spawning distribution rather than column counts. A new `STAIRS_TERRAINS_CFG` preset provides a progressive stair curriculum...
- 外链文档摘录:
  - https://mujocolab.github.io/mjlab/main/source/tutorials/cartpole.html
    The entire task lives in two files: an XML model and a Python module. We
    Every environment starts with a MuJoCo XML that defines the physical
    <!-- A cart on a rail with a pole attached by a hinge. --><bodyname="cart"pos="0 0 1"><jointname="slider"type="slide"axis="1 0 0"limited="true"range="-1.8 1.8"damping="5e-4"/><geomname="cart"type="box"size="0.2 0.15 0.1"mass="1"/><bodyname="pole_1"childclass="pole"><jointname="hinge_1"/><geomname="pole_1"/></body></body><!-- A motor that pushes the cart along the rail. --><actuator><motorname="slide"joint="slider"gear="10"ctrllimited="true"ctrlrange="-1 1"/></actuator>
    The motor has gear ratio 10 and control range [-1, 1], so the maximum
    force is 10 N.
    The full XML is at
    Entity: wrapping the XML#
    XML and, optionally, actuator and initial state configurations. At
    function that loads the XML, an actuator configuration, and an initial
    # Load the XML._CARTPOLE_XML=Path(__file__).parent/"cartpole.xml"def_get_spec()->mujoco.MjSpec:returnmujoco.MjSpec.from_file(str(_CARTPOLE_XML))# Tell mjlab to use the motor defined in the XML as is._CARTPOLE_ARTICULATION=EntityArticulationInfoCfg(actuators=(XmlActuatorCfg(target_names_expr=("slider",)),),)
    group; they share the same terms here, but when you add noise later
    (asymmetric actor-critic11Pinto, L., Andrychowicz, M., Welinder, P., Zaremba, W., & Abbeel, P. (2018).Asymmetric Actor Critic for Image-Based Robot Learning.Robotics: Science and Systems XIV.).
    buffer, which clamps it to [-1, 1] and multiplies by the gear ratio:
    \[r = \underbrace{\frac{\cos\theta + 1}{2}}_{\text{upright}}
    \times \underbrace{\frac{1 + g(x)}{2}}_{\text{centered}}
    \times \underbrace{\frac{4 + q(u)}{5}}_{\text{small control}}
    \times \underbrace{\frac{1 + g(\dot\theta)}{2}}_{\text{small velocity}}\]
    Each factor is between 0 and 1. The product is high only when all four
    giving a 20 Hz control frequency.
    a small network of two 64 unit hidden layers is plenty. The full RL
    Mean reward over 5 seeds (shaded: one standard deviation).#
    Add observation noise.The current config has no noise, so the
    policy is brittle. Add noise to any observation term to train a more
- Compare 摘要: v1.2.0 -> v1.3.0
  - commits: 95
  - files changed: 184
  - additions: 10605
  - deletions: 4569
  - top directories: .claude, .github, .gitignore, CITATION.cff, CLAUDE.md, README.md
  - representative files:
    - src/mjlab/viewer/viser/scene.py (modified, +429/-1569)
    - src/mjlab/viewer/viser/conversions.py (removed, +0/-698)
    - src/mjlab/sensor/raycast_sensor.py (modified, +339/-303)
    - tests/test_domain_randomization.py (modified, +457/-117)
    - tests/test_raycast_sensor.py (modified, +416/-140)
    - src/mjlab/terrains/config.py (modified, +313/-158)
    - tests/test_recorder_manager.py (added, +462/-0)
    - docs/source/tutorials/cartpole.rst (added, +439/-0)

### v1.2.0
- 标题: mjlab v1.2.0
- 类型: 正式版
- 发布时间: 2026-03-07 06:22:37 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.2.0
- GitHub release body:
Our biggest release yet. 60+ pull requests from 12 contributors. A ground up redesign of domain randomization, major viewer improvements, cloud training support, and many bug fixes.

```bash
pip install mjlab
```

https://github.com/user-attachments/assets/18fe2bde-5fa3-4a61-ac19-4e464991aed3

_Domain randomization on the yam lift cube task: cube color, cube size, cube mass, link orientations, link inertias, camera FOV, and lighting all randomized per environment on every reset._

## Domain Randomization, Redesigned

Domain randomization is a key technique for sim-to-real transfer. The new dr module replaces the previous `randomize_field` interface with typed, per-field randomization functions. These functions automatically recompute dependent physical quantities when a parameter is modified. For example, if body mass is randomized, the corresponding inertia values are updated to remain physically consistent. Similarly, when geom size parameters change, the broadphase collision bounds are recomputed. This design removes the need for manual `set_const` calls and reduces the risk of introducing inconsistent physics states.

```python
import mjlab.envs.mdp.dr as dr

dr.geom_friction(env, cfg, operation=dr.scale, distribution=dr.uniform, ranges=(0.8, 1.2))
dr.pseudo_inertia(env, cfg, alpha_range=(-0.3, 0.3), d_range=(-0.3, 0.3))
dr.mat_rgba(env, cfg, operation=dr.add, distribution=dr.gaussian, ranges=(-0.1, 0.1))
```

The full lineup covers geometry, bodies, visuals, cameras, and lights. Custom operations and distributions are first class: define your own and pass them anywhere a string is accepted. The native viewer syncs all randomized fields from the GPU model on every reset, so DR changes are immediately visible.

## Viewer Overhaul

https://github.com/user-attachmen...
- 外链文档摘录:
  - https://skypilot.readthedocs.io/
    SkyPilot: Manage all your AI compute — SkyPilot DocsSkip to main content
    Back to top
    Ctrl+K
    You are viewing the latest developer preview docs.Click hereto
    view docs for the latest stable release.
    - Slack
    - Twitter
    - GitHub
    SkyPilot: Manage all your AI compute#
  - https://mujocolab.github.io/mjlab/main/index.html
    setup friction. It adopts the manager-based API introduced byIsaac Lab, where users compose
    - Sensors
    - API Reference
    - mjlab.sensor
    - Changelog
    mjlab is licensed under the Apache License, Version 2.0.
    @article{Zakka_mjlab_A_Lightweight_2026,author={Zakka, Kevin and Liao, Qiayuan and Yi, Brent and Le Lay, Louis and Sreenath, Koushil and Abbeel, Pieter},title={{mjlab: A Lightweight Framework for GPU-Accelerated Robot Learning}},url={https://arxiv.org/abs/2601.22074},year={2026}}
    mjlab would not exist without the excellent work of the Isaac Lab team, whose API design
- Compare 摘要: v1.1.1 -> v1.2.0
  - commits: 83
  - files changed: 208
  - additions: 13927
  - deletions: 3463
  - top directories: .claude, .dockerignore, .github, CITATION.cff, CONTRIBUTING.md, Dockerfile
  - representative files:
    - docs/source/randomization.rst (modified, +1101/-71)
    - src/mjlab/envs/mdp/events.py (modified, +196/-544)
    - src/mjlab/viewer/native/viewer.py (modified, +380/-142)
    - docs/source/actuators.rst (modified, +164/-324)
    - docs/source/environment_config.rst (added, +484/-0)
    - docs/source/entity/entity_data.rst (added, +481/-0)
    - src/mjlab/envs/mdp/dr/body.py (added, +456/-0)
    - src/mjlab/viewer/base.py (modified, +287/-146)

### v1.1.1
- 标题: mjlab v1.1.1
- 类型: 正式版
- 发布时间: 2026-02-15 09:55:52 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.1.1
- GitHub release body:
Minor patch release with bug fixes and small improvements. Highlights include a new differential IK action space, reward visualization in the native viewer, and a switch from `moviepy` to `mediapy` for video recording.

## What's Changed
* Enable reward plots in the native viewer. by @kevinzakka in https://github.com/mujocolab/mjlab/pull/629
* Extend Viser plotting to plot metrics by @saikishor in https://github.com/mujocolab/mjlab/pull/625
* Fix viser depth image display for vision example tasks by @pthangeda in https://github.com/mujocolab/mjlab/pull/627
* Add differential IK action space. by @kevinzakka in https://github.com/mujocolab/mjlab/pull/632
* fix(play): use MjlabOnPolicyRunner as default runner by @griffinaddison in https://github.com/mujocolab/mjlab/pull/626
* Remove unsafe body fields from domain randomization by @kevinzakka in https://github.com/mujocolab/mjlab/pull/631
* Replace moviepy with mediapy for video recording by @kevinzakka in https://github.com/mujocolab/mjlab/pull/637
* Use bleeding edge mujoco and mujoco_warp for dev. by @kevinzakka in https://github.com/mujocolab/mjlab/pull/638

## New Contributors
* @pthangeda made their first contribution in https://github.com/mujocolab/mjlab/pull/627
* @griffinaddison made their first contribution in https://github.com/mujocolab/mjlab/pull/626

**Full Changelog**: https://github.com/mujocolab/mjlab/compare/v1.1.0...v1.1.1
- Compare 摘要: v1.1.0 -> v1.1.1
  - commits: 10
  - files changed: 26
  - additions: 1711
  - deletions: 268
  - top directories: CITATION.cff, CLAUDE.md, Makefile, README.md, docs/source, pyproject.toml
  - representative files:
    - uv.lock (modified, +393/-124)
    - tests/test_differential_ik_action.py (added, +423/-0)
    - src/mjlab/envs/mdp/actions/differential_ik.py (added, +305/-0)
    - scripts/demos/differential_ik.py (added, +194/-0)
    - src/mjlab/viewer/native/viewer.py (modified, +94/-56)
    - tests/test_video_recorder.py (added, +83/-0)
    - docs/source/actuators.rst (modified, +66/-6)
    - src/mjlab/viewer/viser/term_plotter.py (renamed, +25/-23)

### v1.1.0
- 标题: mjlab v1.1.0
- 类型: 正式版
- 发布时间: 2026-02-13 13:41:02 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.1.0
- GitHub release body:
mjlab and all its dependencies (including mujoco-warp) are now available directly from [PyPI](https://pypi.org/project/mjlab/). Installation no longer requires pinning a specific mujoco-warp revision or custom indices and is now just:

```bash
pip install mjlab
```

or try it instantly with:

```bash
uvx --from mjlab demo
```

## What's new

- RGB and depth camera sensors with BVH-accelerated raycasting
- MetricsManager for logging custom metrics during training
- Terrain visualizer and many new terrain types
- Site group visualization in the Viser viewer
- Upgraded rsl-rl-lib to 4.0.0 with native ONNX export
- Various bug fixes

See the full [changelog](https://mujocolab.github.io/mjlab/source/changelog.html#version-1-1-0-february-12-2026) for details.
- Compare 摘要: v1.0.0 -> v1.1.0
  - commits: 111
  - files changed: 132
  - additions: 19695
  - deletions: 12836
  - top directories: .claude, .github, CITATION.cff, CLAUDE.md, Makefile, README.md
  - representative files:
    - typings/mujoco/_enums.pyi (modified, +9290/-6631)
    - typings/mujoco/_functions.pyi (modified, +973/-2741)
    - src/mjlab/terrains/primitive_terrains.py (modified, +1065/-32)
    - typings/mujoco/_render.pyi (modified, +482/-486)
    - typings/mujoco/__init__.pyi (modified, +103/-761)
    - typings/mujoco/_specs.pyi (modified, +758/-66)
    - scripts/benchmarks/generate_report.py (modified, +232/-288)
    - src/mjlab/scripts/visualize_terrain.py (added, +520/-0)

### v1.0.0
- 标题: mjlab v1.0.0
- 类型: 正式版
- 发布时间: 2026-01-29 13:38:09 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v1.0.0
- GitHub release body:
mjlab is now stable. Thank you to everyone who contributed code, reported issues, and provided feedback along the way. This release wouldn't have happened without you.

Some highlights:
  - RayCastSensor: Terrain and obstacle detection for navigation tasks
  - ContactSensor improvements: History tracking for better contact dynamics
  - Muscle actuator support: Biomechanical simulation capabilities
  - Sensor caching: Performance optimizations for large-scale training
  - Better NaN handling: Easier debugging with detection in observations and sensor data

v1.1 will follow shortly after mjwarp exits beta (imminent), adding RGB-D camera support (experimental https://github.com/mujocolab/mjlab/pull/511).

Cheers!
- Compare 摘要: v0.1.0 -> v1.0.0
  - commits: 662
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 15336
  - deletions: 2166
  - top directories: .claude, .dockerignore, .github, .gitignore, .pre-commit-config.yaml, CITATION.cff
  - representative files:
    - notebooks/create_new_task.ipynb (added, +863/-0)
    - scripts/benchmarks/generate_report.py (added, +852/-0)
    - src/mjlab/sensor/raycast_sensor.py (added, +803/-0)
    - src/mjlab/entity/entity.py (modified, +476/-150)
    - src/mjlab/sensor/contact_sensor.py (added, +602/-0)
    - docs/source/actuators.rst (added, +567/-0)
    - src/mjlab/envs/mdp/events.py (modified, +457/-57)
    - src/mjlab/managers/observation_manager.py (modified, +315/-46)

### v0.1.0
- 标题: v0.1.0 - Beta Release
- 类型: 预发布版
- 发布时间: 2025-09-29 18:00:45 CST
- 链接: https://github.com/mujocolab/mjlab/releases/tag/v0.1.0
- GitHub release body:
**mjlab is public and on PyPI! 🎉**

We're excited to announce the release of `mjlab`. It is available here on GitHub and on [PyPI](https://pypi.org/project/mjlab/).

### Quick Demo

See `mjlab` in action with a pre-trained motion imitation policy on the Unitree G1 humanoid:

```bash
uvx --from mjlab --with "mujoco-warp @ git+https://github.com/google-deepmind/mujoco_warp" demo
```

### Beta Release

This is an early beta release - we're actively implementing missing features and would love your feedback on what to prioritize! The API may evolve as we incorporate community input, add new features and squash bugs.

Thanks!

# Tagged Repository Source Evidence

## v1.5.2
- README / repo positioning excerpt:
![Project banner](https://raw.githubusercontent.com/mujocolab/mjlab/main/docs/source/_static/mjlab-banner.jpg)
# mjlab
[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/mujocolab/mjlab/ci.yml?branch=main)](https://github.com/mujocolab/mjlab/actions/workflows/ci.yml?query=branch%3Amain)
[![Documentation](https://github.com/mujocolab/mjlab/actions/workflows/docs.yml/badge.svg)](https://mujocolab.github.io/mjlab/)
[![License](https://img.shields.io/github/license/mujocolab/mjlab)](https://github.com/mujocolab/mjlab/blob/main/LICENSE)
[![MuJoCo Warp](https://img.shields.io/badge/MuJoCo_Warp-3.10.0.2-blue)](https://github.com/google-deepmind/mujoco_warp/releases/tag/v3.10.0.2)
[![Nightly Benchmarks](https://img.shields.io/badge/Nightly-Benchmarks-blue)](https://mujocolab.github.io/mjlab/nightly/)
[![PyPI](https://img.shields.io/pypi/v/mjlab)](https://pypi.org/project/mjlab/)
## Getting Started
mjlab requires an NVIDIA GPU for training. macOS is supported for evaluation only.
For alternative installation methods (PyPI, Docker), see the [Installation Guide](https://mujocolab.github.io/mjlab/main/source/installation.html).
## Training Examples
### 1. Velocity Tracking
Train a Unitree G1 humanoid to follow velocity commands on flat terrain:
uv run train Mjlab-Velocity-Flat-Unitree-G1 --env.scene.num-envs 4096
**Multi-GPU Training:** Scale to multiple GPUs using `--gpu-ids`:
uv run train Mjlab-Velocity-Flat-Unitree-G1 \
--gpu-ids "[0, 1]" \
--env.scene.num-envs 4096
uv run play Mjlab-Velocity-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
### 2. Motion Imitation
uv run train Mjlab-Tracking-Flat-Unitree-G1 --registry-name your-org/motions/motion-name --env.scene.num-envs 4096
uv run play Mjlab-Tracking-Flat-Unitree-G1 --wandb-run-path your-org/mjl...
- High-signal repository paths at this tag:
  - README.md
  - docs/conf.py
  - docs/index.rst
  - scripts/cloud/README.md
  - scripts/benchmarks/README.md
  - docs/source/faq.rst
  - docs/source/scene.rst
  - docs/source/events.rst
  - docs/source/actions.rst
  - docs/source/metrics.rst
  - docs/source/rewards.rst
  - docs/source/terrain.rst
- Changed high-signal files against previous included release:
  - [M] docs/source/changelog.rst
    Excerpt:
    =========
    Changelog
    =========
    Upcoming version (not yet released)
    -----------------------------------
    Added
    ^^^^^
    Changed
    Version 1.5.2 (July 17, 2026)
    - Fixed CUDA illegal memory accesses when domain randomization triggers
    ``set_const`` with multiple environments. ``actuator_acc0`` is now expanded
    - Fixed ``MaterialCfg.reflectance`` being ignored when building the MuJoCo
    Version 1.5.1 (July 15, 2026)
    - Added ``MeshCfg``, a spec editor that matches mesh assets by name and edits
    - Added ``SimulationCfg.broadphase`` and ``SimulationCfg.broadphase_filter``
    to configure MuJoCo Warp's broadphase collision algorithm and
    - Enabled skybox rendering for camera sensors. Contribution by @bd-pmorais.
    - Bumped the minimum ``mujoco-warp`` to 3.10.0.2, which fixes ``qfrc_constraint``
    being populated incorrectly across vectorized environments (:issue:`1086`).
    Earlier 3.10.0.x releases are no longer supported.
    - Command delay on fusable actuators (ideal PD, DC motor) now applies one shared
    lag per environment across all fused actuators sharing a delay config, matching
    (:issue:`1035`).
    - Fixed ``TerrainGenerator`` overwriting custom geom names set by sub-terrain
    - Fixed ``TorchArray`` not expanding world-shared model fields to ``nworld``
    with mujoco_warp 3.10.0.2, which allocates them as real size-1 arrays
    instead of stride-0 broadcast views. Multi-env indexing of fields like
    ``soft_joint_pos_limits`` raised ``IndexError`` during resets (:issue:`1093`).
    - Fixed ``mdp.bad_orientation`` returning NaN when float32 rounding in
    outside ``[-1, 1]``, making ``torch.acos`` return NaN and silently
    suppressing the termination for flipped robots. The argument is now clamped
    to ``[-1, 1]``.
    - Fixed a crash when using command delay on ideal PD (or other custom)
    config into a single gather, delay,...
  - [M] docs/source/randomization.rst
    Excerpt:
    .. _domain_randomization:
    Domain Randomization
    ====================
    Domain randomization varies physical parameters during training so that policies
    are robust to modeling errors and real-world variation. This guide shows
    how to attach randomization terms to an environment using ``EventTermCfg`` and
    the ``dr`` module.
    Quick Start
    from mjlab.managers.scene_entity_config import SceneEntityCfg
    "asset_cfg": SceneEntityCfg("robot", geom_names=[".*_foot.*"]),
    "ranges": (0.3, 1.2),
    automatically tracks the fields that need to be expanded for per-world
    model). For example, ``dr.geom_friction`` writes to ``sim.model.geom_friction``,
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``geom_friction``
    - Sliding, torsional, and rolling friction coefficients
    - Default axis: 0 (tangential only)
    - ``geom_pos``
    - Position of the geom in the parent body frame
    - ``geom_quat``
    - Orientation of the geom frame
    - Accepts roll/pitch/yaw ranges (radians); composes with default
    - ``geom_rgba``
    - Color and transparency (RGBA)
    - ``geom_size``
    - Geom-specific size parameters (radius, half-lengths, etc.)
    - Automatically recomputes ``geom_rbound`` and ``geom_aabb``
    - ``geom_matid``
    - Which baked material the geom renders with
    - Samples uniformly from ``asset_cfg.material_names``
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``body_mass``
    - Mass of the body
    - Triggers ``set_const`` recomputation
    - ``body_ipos``
    - Center of mass position relative to the body frame
    - Triggers ``set_const``
    - ``body_pos``
    - Position of the body frame in the parent frame
    - Triggers ``set_const_0``
    - ``body_quat``
    - Orientation of the body frame
    - Accepts roll/pitch/yaw ranges (radians); composes with default;
    triggers ``set_const_0``
    :header-rows: 1
    :widths: 28 1...
  - [M] src/mjlab/utils/spec_config.py
    Excerpt:
    Base class for all MuJoCo spec configurations.
    Classes: SpecCfg, TextureCfg, MaterialCfg, MeshCfg, CollisionCfg, LightCfg, CameraCfg

## v1.5.1
- README / repo positioning excerpt:
![Project banner](https://raw.githubusercontent.com/mujocolab/mjlab/main/docs/source/_static/mjlab-banner.jpg)
# mjlab
[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/mujocolab/mjlab/ci.yml?branch=main)](https://github.com/mujocolab/mjlab/actions/workflows/ci.yml?query=branch%3Amain)
[![Documentation](https://github.com/mujocolab/mjlab/actions/workflows/docs.yml/badge.svg)](https://mujocolab.github.io/mjlab/)
[![License](https://img.shields.io/github/license/mujocolab/mjlab)](https://github.com/mujocolab/mjlab/blob/main/LICENSE)
[![MuJoCo Warp](https://img.shields.io/badge/MuJoCo_Warp-3.10.0.2-blue)](https://github.com/google-deepmind/mujoco_warp/releases/tag/v3.10.0.2)
[![Nightly Benchmarks](https://img.shields.io/badge/Nightly-Benchmarks-blue)](https://mujocolab.github.io/mjlab/nightly/)
[![PyPI](https://img.shields.io/pypi/v/mjlab)](https://pypi.org/project/mjlab/)
## Getting Started
mjlab requires an NVIDIA GPU for training. macOS is supported for evaluation only.
For alternative installation methods (PyPI, Docker), see the [Installation Guide](https://mujocolab.github.io/mjlab/main/source/installation.html).
## Training Examples
### 1. Velocity Tracking
Train a Unitree G1 humanoid to follow velocity commands on flat terrain:
uv run train Mjlab-Velocity-Flat-Unitree-G1 --env.scene.num-envs 4096
**Multi-GPU Training:** Scale to multiple GPUs using `--gpu-ids`:
uv run train Mjlab-Velocity-Flat-Unitree-G1 \
--gpu-ids "[0, 1]" \
--env.scene.num-envs 4096
uv run play Mjlab-Velocity-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
### 2. Motion Imitation
uv run train Mjlab-Tracking-Flat-Unitree-G1 --registry-name your-org/motions/motion-name --env.scene.num-envs 4096
uv run play Mjlab-Tracking-Flat-Unitree-G1 --wandb-run-path your-org/mjl...
- High-signal repository paths at this tag:
  - README.md
  - docs/conf.py
  - docs/index.rst
  - scripts/cloud/README.md
  - scripts/benchmarks/README.md
  - docs/source/faq.rst
  - docs/source/scene.rst
  - docs/source/events.rst
  - docs/source/actions.rst
  - docs/source/metrics.rst
  - docs/source/rewards.rst
  - docs/source/terrain.rst
- Changed high-signal files against previous included release:
  - [M] README.md
    Excerpt:
    ![Project banner](https://raw.githubusercontent.com/mujocolab/mjlab/main/docs/source/_static/mjlab-banner.jpg)
    # mjlab
    [![GitHub Actions](https://img.shields.io/github/actions/workflow/status/mujocolab/mjlab/ci.yml?branch=main)](https://github.com/mujocolab/mjlab/actions/workflows/ci.yml?query=branch%3Amain)
    [![Documentation](https://github.com/mujocolab/mjlab/actions/workflows/docs.yml/badge.svg)](https://mujocolab.github.io/mjlab/)
    [![License](https://img.shields.io/github/license/mujocolab/mjlab)](https://github.com/mujocolab/mjlab/blob/main/LICENSE)
    [![MuJoCo Warp](https://img.shields.io/badge/MuJoCo_Warp-3.10.0.2-blue)](https://github.com/google-deepmind/mujoco_warp/releases/tag/v3.10.0.2)
    [![Nightly Benchmarks](https://img.shields.io/badge/Nightly-Benchmarks-blue)](https://mujocolab.github.io/mjlab/nightly/)
    [![PyPI](https://img.shields.io/pypi/v/mjlab)](https://pypi.org/project/mjlab/)
    ## Getting Started
    mjlab requires an NVIDIA GPU for training. macOS is supported for evaluation only.
    For alternative installation methods (PyPI, Docker), see the [Installation Guide](https://mujocolab.github.io/mjlab/main/source/installation.html).
    ## Training Examples
    ### 1. Velocity Tracking
    Train a Unitree G1 humanoid to follow velocity commands on flat terrain:
    uv run train Mjlab-Velocity-Flat-Unitree-G1 --env.scene.num-envs 4096
    **Multi-GPU Training:** Scale to multiple GPUs using `--gpu-ids`:
    uv run train Mjlab-Velocity-Flat-Unitree-G1 \
    --gpu-ids "[0, 1]" \
    --env.scene.num-envs 4096
    uv run play Mjlab-Velocity-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
    ### 2. Motion Imitation
    uv run train Mjlab-Tracking-Flat-Unitree-G1 --registry-name your-org/motions/motion-name --env.scene.num-envs 4096
    uv run play Mjlab-Tracking-Flat-Unitree-G1 --wandb-run-path your-org/mjl...
  - [M] docs/source/changelog.rst
    Excerpt:
    =========
    Changelog
    =========
    Upcoming version (not yet released)
    -----------------------------------
    Added
    ^^^^^
    Changed
    Version 1.5.1 (July 15, 2026)
    - Added ``MeshCfg``, a spec editor that matches mesh assets by name and edits
    - Added ``SimulationCfg.broadphase`` and ``SimulationCfg.broadphase_filter``
    to configure MuJoCo Warp's broadphase collision algorithm and
    - Enabled skybox rendering for camera sensors.
    - Bumped the minimum ``mujoco-warp`` to 3.10.0.2, which fixes ``qfrc_constraint``
    being populated incorrectly across vectorized environments (:issue:`1086`).
    Earlier 3.10.0.x releases are no longer supported.
    - Command delay on fusable actuators (ideal PD, DC motor) now applies one shared
    lag per environment across all fused actuators sharing a delay config, matching
    (:issue:`1035`).
    - Fixed ``TerrainGenerator`` overwriting custom geom names set by sub-terrain
    - Fixed ``TorchArray`` not expanding world-shared model fields to ``nworld``
    with mujoco_warp 3.10.0.2, which allocates them as real size-1 arrays
    instead of stride-0 broadcast views. Multi-env indexing of fields like
    ``soft_joint_pos_limits`` raised ``IndexError`` during resets (:issue:`1093`).
    - Fixed ``mdp.bad_orientation`` returning NaN when float32 rounding in
    outside ``[-1, 1]``, making ``torch.acos`` return NaN and silently
    suppressing the termination for flipped robots. The argument is now clamped
    to ``[-1, 1]``.
    - Fixed a crash when using command delay on ideal PD (or other custom)
    config into a single gather, delay, control-law evaluation, and control
    write, removing per-group host overhead (:issue:`1035`).
    Version 1.5.0 (June 28, 2026)
    - Added ``reduce="max"`` to ``MetricsTermCfg`` for reporting episode-peak values
    - Added ``BuiltinDcMotorActuator``, a native MuJoCo ``<dcmotor>`` wrapper.
    Sup...
  - [M] docs/source/randomization.rst
    Excerpt:
    .. _domain_randomization:
    Domain Randomization
    ====================
    Domain randomization varies physical parameters during training so that policies
    are robust to modeling errors and real-world variation. This guide shows
    how to attach randomization terms to an environment using ``EventTermCfg`` and
    the ``dr`` module.
    Quick Start
    from mjlab.managers.scene_entity_config import SceneEntityCfg
    "asset_cfg": SceneEntityCfg("robot", geom_names=[".*_foot.*"]),
    "ranges": (0.3, 1.2),
    automatically tracks the fields that need to be expanded for per-world
    model). For example, ``dr.geom_friction`` writes to ``sim.model.geom_friction``,
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``geom_friction``
    - Sliding, torsional, and rolling friction coefficients
    - Default axis: 0 (tangential only)
    - ``geom_pos``
    - Position of the geom in the parent body frame
    - ``geom_quat``
    - Orientation of the geom frame
    - Accepts roll/pitch/yaw ranges (radians); composes with default
    - ``geom_rgba``
    - Color and transparency (RGBA)
    - ``geom_size``
    - Geom-specific size parameters (radius, half-lengths, etc.)
    - Automatically recomputes ``geom_rbound`` and ``geom_aabb``
    - ``geom_matid``
    - Which baked material the geom renders with
    - Samples uniformly from ``asset_cfg.material_names``
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``body_mass``
    - Mass of the body
    - Triggers ``set_const`` recomputation
    - ``body_ipos``
    - Center of mass position relative to the body frame
    - Triggers ``set_const``
    - ``body_pos``
    - Position of the body frame in the parent frame
    - Triggers ``set_const_0``
    - ``body_quat``
    - Orientation of the body frame
    - Accepts roll/pitch/yaw ranges (radians); composes with default;
    triggers ``set_const_0``
    :header-rows: 1
    :widths: 28 1...
  - [M] tests/test_spec_config.py
    Excerpt:
    Tests for spec_config.py.
    Functions: simple_robot_xml, multi_geom_spec, test_collision_basic_properties, test_collision_regex_matching, test_collision_dict_field_resolution, test_collision_margin_gap_solmix, test_collision_margin_gap_solmix_dict, test_collision_disable_other_geoms, test_collision_validation, _sphere_points, multi_mesh_spec, _hull_numvert
  - [M] src/mjlab/utils/spec_config.py
    Excerpt:
    Base class for all MuJoCo spec configurations.
    Classes: SpecCfg, TextureCfg, MaterialCfg, MeshCfg, CollisionCfg, LightCfg, CameraCfg

## v1.5.0
- README / repo positioning excerpt:
![Project banner](https://raw.githubusercontent.com/mujocolab/mjlab/main/docs/source/_static/mjlab-banner.jpg)
# mjlab
[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/mujocolab/mjlab/ci.yml?branch=main)](https://github.com/mujocolab/mjlab/actions/workflows/ci.yml?query=branch%3Amain)
[![Documentation](https://github.com/mujocolab/mjlab/actions/workflows/docs.yml/badge.svg)](https://mujocolab.github.io/mjlab/)
[![License](https://img.shields.io/github/license/mujocolab/mjlab)](https://github.com/mujocolab/mjlab/blob/main/LICENSE)
[![Nightly Benchmarks](https://img.shields.io/badge/Nightly-Benchmarks-blue)](https://mujocolab.github.io/mjlab/nightly/)
[![PyPI](https://img.shields.io/pypi/v/mjlab)](https://pypi.org/project/mjlab/)
[![PyPI downloads](https://img.shields.io/pypi/dm/mjlab?color=blue)](https://pypistats.org/packages/mjlab)
## Getting Started
mjlab requires an NVIDIA GPU for training. macOS is supported for evaluation only.
For alternative installation methods (PyPI, Docker), see the [Installation Guide](https://mujocolab.github.io/mjlab/main/source/installation.html).
## Training Examples
### 1. Velocity Tracking
Train a Unitree G1 humanoid to follow velocity commands on flat terrain:
uv run train Mjlab-Velocity-Flat-Unitree-G1 --env.scene.num-envs 4096
**Multi-GPU Training:** Scale to multiple GPUs using `--gpu-ids`:
uv run train Mjlab-Velocity-Flat-Unitree-G1 \
--gpu-ids "[0, 1]" \
--env.scene.num-envs 4096
uv run play Mjlab-Velocity-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
### 2. Motion Imitation
uv run train Mjlab-Tracking-Flat-Unitree-G1 --registry-name your-org/motions/motion-name --env.scene.num-envs 4096
uv run play Mjlab-Tracking-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
### 3. Sanity-check with Du...
- High-signal repository paths at this tag:
  - README.md
  - docs/conf.py
  - docs/index.rst
  - scripts/cloud/README.md
  - scripts/benchmarks/README.md
  - docs/source/faq.rst
  - docs/source/scene.rst
  - docs/source/events.rst
  - docs/source/actions.rst
  - docs/source/metrics.rst
  - docs/source/rewards.rst
  - docs/source/terrain.rst
- Changed high-signal files against previous included release:
  - [M] docs/source/actuators.rst
    Excerpt:
    .. _actuators:
    Actuators
    =========
    Actuators convert high-level commands (position, velocity, effort) into
    low-level efforts that drive joints. They are configured through the
    ``articulation`` field of :ref:`EntityCfg <entity>`. mjlab provides
    **built-in** actuators that leverage the physics engine's implicit
    integration for best stability, and **explicit** actuators for custom
    robot_cfg = EntityCfg(
    spec_fn=lambda: load_robot_spec(),
    stiffness=80.0,
    damping=10.0,
    effort_limit=100.0,
    Add delay fields directly on any actuator config to model communication
    stiffness=80.0,
    damping=10.0,
    delay_min_lag=2,  # Minimum 2 physics steps
    delay_max_lag=5,  # Maximum 5 physics steps
    The key design decision when configuring actuators is whether to use
    All actuator configs share a few common fields inherited from
    - ``target_names_expr``: Tuple of regex patterns matched against joint
    - ``armature``: Reflected rotor inertia added to the target joint.
    - ``frictionloss``: Static friction (stiction) modeled as a constraint
    `frictionloss <https://mujoco.readthedocs.io/en/stable/XMLreference.html#body-joint-frictionloss>`_.
    `<dcmotor> <https://mujoco.readthedocs.io/en/stable/XMLreference.html#actuator-dcmotor>`_
    pins v_target = 0 (the kd term acts on raw velocity). Optional physics:
    thermal model with I^2R heating, cogging ripple, LuGre friction.
    # Mobile manipulator: PD for arm joints, velocity control for wheels.
    stiffness=100.0,
    damping=10.0,
    effort_limit=150.0,
    damping=20.0,
    effort_limit=50.0,
    # Ideal PD for hips, DC motor model with torque-speed curve for knees.
    stiffness=80.0,
    damping=10.0,
    effort_limit=100.0,
    stiffness=80.0,
    damping=10.0,
    effort_limit=25.0,       # Continuous torque limit
    saturation_effort=50.0,  # Peak torque at stall
    velocity_limit=30.0,     # No-load speed (rad/...
  - [M] docs/source/changelog.rst
    Excerpt:
    =========
    Changelog
    =========
    Upcoming version (not yet released)
    -----------------------------------
    Added
    ^^^^^
    Changed
    Version 1.5.0 (June 28, 2026)
    - Added ``reduce="max"`` to ``MetricsTermCfg`` for reporting episode-peak values
    - Added ``BuiltinDcMotorActuator``, a native MuJoCo ``<dcmotor>`` wrapper.
    Supports voltage / position / velocity input modes with back-EMF,
    configurable motor constants, and optional integral, slew, inductance,
    - Added ``scale_with_difficulty`` to ``HfRandomUniformTerrainCfg``. When
    enabled, the noise amplitude scales with difficulty (flat at 0, full
    ``noise_range`` at 1) so the terrain progresses in a curriculum. Defaults to
    - Added material domain randomization functions for MuJoCo Warp RGB rendering:
    - Bumped ``rsl-rl-lib`` from 5.2.0 to 5.4.0.
    - Bumped ``mujoco`` and ``mujoco-warp`` to 3.10, both pinned from PyPI. The
    - Curriculum-mode terrain difficulty is now deterministic across rows
    and reaches the configured ``difficulty_range`` endpoints
    (:issue:`1027`).
    - Heightfield terrains now color by absolute height with a diverging palette
    - ``BoxNestedRingsTerrainCfg`` now builds uniform-height concentric ridges
    - Terrain generation no longer prints timing information to stdout.
    - Fixed domain randomization events that target different ``axes`` of the same
    model field (e.g. two ``dr.geom_size`` events scaling axis 0 and axis 1
    the axes it targeted, so per-axis events compose (:issue:`1042`).
    - Regenerated the bundled MuJoCo type stubs, which had drifted from the
    (:issue:`1048`).
    - Fixed ``select_gpus`` crashing when ``CUDA_VISIBLE_DEVICES`` contains MIG
    - Fixed pyramid-stairs terrains (``BoxPyramidStairsTerrainCfg``,
    leaving an empty, geometry-free border at difficulty 0, where the step
    solid geometry flush with the ground (:issue:`1033...
  - [M] docs/source/randomization.rst
    Excerpt:
    .. _domain_randomization:
    Domain Randomization
    ====================
    Domain randomization varies physical parameters during training so that policies
    are robust to modeling errors and real-world variation. This guide shows
    how to attach randomization terms to an environment using ``EventTermCfg`` and
    the ``dr`` module.
    Quick Start
    from mjlab.managers.scene_entity_config import SceneEntityCfg
    "asset_cfg": SceneEntityCfg("robot", geom_names=[".*_foot.*"]),
    "ranges": (0.3, 1.2),
    automatically tracks the fields that need to be expanded for per-world
    model). For example, ``dr.geom_friction`` writes to ``sim.model.geom_friction``,
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``geom_friction``
    - Sliding, torsional, and rolling friction coefficients
    - Default axis: 0 (tangential only)
    - ``geom_pos``
    - Position of the geom in the parent body frame
    - ``geom_quat``
    - Orientation of the geom frame
    - Accepts roll/pitch/yaw ranges (radians); composes with default
    - ``geom_rgba``
    - Color and transparency (RGBA)
    - ``geom_size``
    - Geom-specific size parameters (radius, half-lengths, etc.)
    - Automatically recomputes ``geom_rbound`` and ``geom_aabb``
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``body_mass``
    - Mass of the body
    - Triggers ``set_const`` recomputation
    - ``body_ipos``
    - Center of mass position relative to the body frame
    - Triggers ``set_const``
    - ``body_pos``
    - Position of the body frame in the parent frame
    - Triggers ``set_const_0``
    - ``body_quat``
    - Orientation of the body frame
    - Accepts roll/pitch/yaw ranges (radians); composes with default;
    triggers ``set_const_0``
    :header-rows: 1
    :widths: 28 18 34 20
    - MuJoCo field
    - Description
    - Notes
    - ``dof_damping``
    - Velocity-proportional damping force (passive)
    - ``d...
  - [M] docs/source/research.rst
    Excerpt:
    .. _research:
    Research
    ========
    Citing mjlab
    ------------
    If you use mjlab in your research, please cite:
    .. code-block:: bibtex
    @article{Zakka_mjlab_A_Lightweight_2026,
    title = {{mjlab: A Lightweight Framework for GPU-Accelerated Robot Learning}},
    url = {https://arxiv.org/abs/2601.22074},
    year = {2026}
    :header-rows: 1
    :widths: 60 30 10
    - Authors
    - Year
    <https://arxiv.org/abs/2602.03205>`_
    - Han, Wang, Zhang, Liu, Luo, Bai, Li
    - 2026
    Trajectory Optimization <https://arxiv.org/abs/2602.06827>`_
    - Dhedin, Taouil, Omar, Yu, Tao, Dai, Khadiv
    - 2026
    Teleoperation <https://arxiv.org/abs/2602.15060>`_
    - Zhu, Cai, Yang, Ren, Xie, Wang, Wu, et al.
    - 2026
    :header-rows: 1
    :widths: 35 65
    - Description
    - Locomotion fork for the Asimov bipedal robot.
    - H1 locomotion across multiple tasks with robustness to upper body disturbances.
    - Musculoskeletal simulation integration with MyoSuite.
    - Velocity control for the Upkie wheeled biped.
    * - `unitreerobotics/unitree_rl_mjlab <https://github.com/unitreerobotics/unitree_rl_mjlab>`_
    - Official Unitree RL environments for Go2, G1, and H1\_2.
    * - `pal-robotics/pal_mjlab <https://github.com/pal-robotics/pal_mjlab>`_
    - PAL Robotics robots and tasks.
    - Sim to real RL for in hand cube rotation with the LEAP Hand.
    - mjlab version of Project-Instinct, a whole-body control toolchain to study Instinct-Level intelligence.
    * - `lzyang2000/twist2_mjlab <https://github.com/lzyang2000/twist2_mjlab>`_
    - mjlab port of `TWIST2 <https://arxiv.org/abs/2511.02832>`_.
    - In-hand cube reorientation on the Wuji Hand with sim-to-real deployment.
    - Configurable whole-body control — shared MDP with task configs, one policy for many skills.
  - [M] docs/source/terrain.rst
    Excerpt:
    .. _terrain:
    Terrain
    =======
    The terrain is the shared ground surface for all environments in a scene.
    mjlab supports two modes: a flat ground plane for tasks that do not need
    varying terrain, and a procedural terrain generator that assembles a grid
    of sub-terrain patches with configurable difficulty. Procedural terrain
    is particularly useful for training locomotion policies, where a
    Terrain is configured through ``TerrainEntityCfg`` and passed to the
    size=(8.0, 8.0),
    num_rows=10,
    border_width=20.0,
    "flat": terrain_gen.BoxFlatTerrainCfg(proportion=0.2),
    proportion=0.4,
    step_height_range=(0.0, 0.15),
    step_width=0.3,
    platform_width=2.0,
    proportion=0.4,
    noise_range=(0.02, 0.10),
    noise_step=0.02,
    max_init_terrain_level=5,
    controls robot spawning distribution across columns in curriculum mode,
    difficulty increases from row 0 (easiest) to row ``num_rows - 1``
    (hardest). The ``proportion`` field controls how robots are distributed
    that linearly interpolates the terrain's configurable ranges. For
    example, a ``BoxPyramidStairsTerrainCfg`` with
    ``step_height_range=(0.0, 0.2)`` produces flat ground at difficulty 0
    and 20 cm steps at difficulty 1.
    ``difficulty = lower + (upper - lower) * row / max(num_rows - 1, 1)``,
    where ``(lower, upper) = difficulty_range``. Row 0 is exactly
    ``lower``, row ``num_rows - 1`` is exactly ``upper``, and intermediate
    With ``num_rows=1`` and ``curriculum=True``, every patch is generated
    at ``difficulty = lower`` (the easiest configured difficulty). Use
    ``curriculum=False`` if you want a single grid of randomly sampled
    ``proportion`` weight and optional ``flat_patch_sampling`` configuration.
    .. grid:: 3
    .. grid:: 3
    Preset configurations
    ``mjlab.terrains.config``:
    A 10x20 random-mode grid with seven terrain types (flat, stairs,
    A 10-row curriculum gri...
  - [M] docs/source/api/actuator.rst
    Excerpt:
    mjlab.actuator
    ==============
    .. automodule:: mjlab.actuator
    .. rubric:: Classes
    .. hlist::
    :columns: 3
    - :class:`Actuator`
    - :class:`ActuatorCfg`
    - :class:`ActuatorCmd`
    - :class:`BuiltinActuatorGroup`
    - :class:`BuiltinMotorActuator`
    - :class:`BuiltinMotorActuatorCfg`
    - :class:`BuiltinPositionActuator`
    - :class:`BuiltinPositionActuatorCfg`
    - :class:`BuiltinVelocityActuator`
    - :class:`BuiltinVelocityActuatorCfg`
    - :class:`BuiltinPdActuator`
    - :class:`BuiltinPdActuatorCfg`
    - :class:`BuiltinDcMotorActuator`
    - :class:`BuiltinDcMotorActuatorCfg`
    - :class:`DcMotorInputMode`
    - :class:`DcMotorDatasheetParams`
    - :class:`DcMotorPhysicalParams`
    - :class:`BuiltinMuscleActuator`
    - :class:`BuiltinMuscleActuatorCfg`
    - :class:`XmlActuator`
    - :class:`XmlActuatorCfg`
    - :class:`IdealPdActuator`
    - :class:`IdealPdActuatorCfg`
    - :class:`DcMotorActuator`
    - :class:`DcMotorActuatorCfg`
    - :class:`LearnedMlpActuator`
    - :class:`LearnedMlpActuatorCfg`
  - [M] .github/workflows/docs.yml
    Excerpt:
    name: docs
    on:
    push:
    branches:
    - main
    tags:
    - 'v*'
    permissions:
    UV_FROZEN: "1"
    - uses: actions/checkout@v6
    fetch-depth: 0
    - uses: actions/setup-python@v5
    python-version: '3.13'
    - name: Install uv
    uses: astral-sh/setup-uv@v7
    - name: Build Sphinx Documentation
    run: uv run --group docs sphinx-multiversion docs docs/_build
    - name: Add root redirect
    run: echo '<meta http-equiv="refresh" content="0; url=main/index.html">' > docs/_build/index.html
    - name: Remove Sphinx build artifacts
    run: find docs/_build -type d -name .doctrees -exec rm -rf {} +
    - name: Deploy to GitHub Pages
    uses: peaceiris/actions-gh-pages@v4
    publish_dir: ./docs/_build/

## v1.4.0
- README / repo positioning excerpt:
![Project banner](https://raw.githubusercontent.com/mujocolab/mjlab/main/docs/source/_static/mjlab-banner.jpg)
# mjlab
[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/mujocolab/mjlab/ci.yml?branch=main)](https://github.com/mujocolab/mjlab/actions/workflows/ci.yml?query=branch%3Amain)
[![Documentation](https://github.com/mujocolab/mjlab/actions/workflows/docs.yml/badge.svg)](https://mujocolab.github.io/mjlab/)
[![License](https://img.shields.io/github/license/mujocolab/mjlab)](https://github.com/mujocolab/mjlab/blob/main/LICENSE)
[![Nightly Benchmarks](https://img.shields.io/badge/Nightly-Benchmarks-blue)](https://mujocolab.github.io/mjlab/nightly/)
[![PyPI](https://img.shields.io/pypi/v/mjlab)](https://pypi.org/project/mjlab/)
[![PyPI downloads](https://img.shields.io/pypi/dm/mjlab?color=blue)](https://pypistats.org/packages/mjlab)
## Getting Started
mjlab requires an NVIDIA GPU for training. macOS is supported for evaluation only.
For alternative installation methods (PyPI, Docker), see the [Installation Guide](https://mujocolab.github.io/mjlab/main/source/installation.html).
## Training Examples
### 1. Velocity Tracking
Train a Unitree G1 humanoid to follow velocity commands on flat terrain:
uv run train Mjlab-Velocity-Flat-Unitree-G1 --env.scene.num-envs 4096
**Multi-GPU Training:** Scale to multiple GPUs using `--gpu-ids`:
uv run train Mjlab-Velocity-Flat-Unitree-G1 \
--gpu-ids "[0, 1]" \
--env.scene.num-envs 4096
uv run play Mjlab-Velocity-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
### 2. Motion Imitation
uv run train Mjlab-Tracking-Flat-Unitree-G1 --registry-name your-org/motions/motion-name --env.scene.num-envs 4096
uv run play Mjlab-Tracking-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
### 3. Sanity-check with Du...
- High-signal repository paths at this tag:
  - README.md
  - docs/conf.py
  - docs/index.rst
  - scripts/cloud/README.md
  - scripts/benchmarks/README.md
  - docs/source/faq.rst
  - docs/source/scene.rst
  - docs/source/events.rst
  - docs/source/actions.rst
  - docs/source/metrics.rst
  - docs/source/rewards.rst
  - docs/source/terrain.rst
- Changed high-signal files against previous included release:
  - [M] README.md
    Excerpt:
    ![Project banner](https://raw.githubusercontent.com/mujocolab/mjlab/main/docs/source/_static/mjlab-banner.jpg)
    # mjlab
    [![GitHub Actions](https://img.shields.io/github/actions/workflow/status/mujocolab/mjlab/ci.yml?branch=main)](https://github.com/mujocolab/mjlab/actions/workflows/ci.yml?query=branch%3Amain)
    [![Documentation](https://github.com/mujocolab/mjlab/actions/workflows/docs.yml/badge.svg)](https://mujocolab.github.io/mjlab/)
    [![License](https://img.shields.io/github/license/mujocolab/mjlab)](https://github.com/mujocolab/mjlab/blob/main/LICENSE)
    [![Nightly Benchmarks](https://img.shields.io/badge/Nightly-Benchmarks-blue)](https://mujocolab.github.io/mjlab/nightly/)
    [![PyPI](https://img.shields.io/pypi/v/mjlab)](https://pypi.org/project/mjlab/)
    [![PyPI downloads](https://img.shields.io/pypi/dm/mjlab?color=blue)](https://pypistats.org/packages/mjlab)
    ## Getting Started
    mjlab requires an NVIDIA GPU for training. macOS is supported for evaluation only.
    For alternative installation methods (PyPI, Docker), see the [Installation Guide](https://mujocolab.github.io/mjlab/main/source/installation.html).
    ## Training Examples
    ### 1. Velocity Tracking
    Train a Unitree G1 humanoid to follow velocity commands on flat terrain:
    uv run train Mjlab-Velocity-Flat-Unitree-G1 --env.scene.num-envs 4096
    **Multi-GPU Training:** Scale to multiple GPUs using `--gpu-ids`:
    uv run train Mjlab-Velocity-Flat-Unitree-G1 \
    --gpu-ids "[0, 1]" \
    --env.scene.num-envs 4096
    uv run play Mjlab-Velocity-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
    ### 2. Motion Imitation
    uv run train Mjlab-Tracking-Flat-Unitree-G1 --registry-name your-org/motions/motion-name --env.scene.num-envs 4096
    uv run play Mjlab-Tracking-Flat-Unitree-G1 --wandb-run-path your-org/mjlab/run-id
    ### 3. Sanity-check with Du...
  - [M] docs/source/changelog.rst
    Excerpt:
    =========
    Changelog
    =========
    Version 1.4.0 (May 26, 2026)
    ----------------------------
    Added
    ^^^^^
    - Added ``BuiltinPdActuator``, the implicit-integration version of
    explicit Python PD would diverge, which matters when you want to
    ``jnt_actfrcrange`` (or ``tendon_actfrcrange``). Supported by
    - Added ``mdp.projected_gravity_from_sensor``, an observation that derives
    randomization (e.g. via ``dr.site_quat``). Go1 and G1 ship an
    - Added ``DebugVisualizer.add_box`` for drawing an axis-oriented box
    primitive, mirroring ``add_ellipsoid``. Supported by both the native
    and Viser viewers. ``size`` is the box half-extents (:issue:`992`).
    - Added ``--log-root`` CLI option to ``train``, ``play``, and ``evaluate``
    - ``RewardManager``, ``TerminationManager``, and ``MetricsManager`` now
    - Added ``ContactSensor.primary_names`` property to expose the resolved
    to the primary it belongs to (:issue:`914`).
    - Added per-world mesh variant support via ``VariantEntityCfg``. Each
    world in a batched simulation can now use a different mesh asset for
    the same logical entity (e.g. world 0 holds a cube, world 1 a
    spec callables; the optional ``assignment`` field controls how worlds
    per-world arrays in the Warp model, so domain randomization, the
    :ref:`heterogeneous_worlds` for usage. With help from @XiangruiJiang.
    - Per-world mesh variants now support per-variant materials and textures.
    ``geom_dataid`` table. Variants without a material get ``matid = -1``.
    - ``Entity`` now raises a clear error at construction when its spec contains
    - Changed ``compute_root_relative_mpkpe`` to re-anchor the reference to the
    robot's root each step, removing yaw drift as well as translation so it
    - Changed ``compute_joint_velocity_error`` from an L2 norm to a per-joint
    - Bumped ``mujoco`` to 3.8 and ``mujoco-warp``...
  - [M] docs/source/faq.rst
    Excerpt:
    .. _faq:
    FAQ & Troubleshooting
    =====================
    This page collects common questions about **platform support**, **performance**,
    **training stability**, and **visualization**, along with practical debugging
    tips and links to further resources.
    Platform Support
    ----------------
    - **Training is not recommended on macOS**, as it lacks GPU acceleration.
    - **Evaluation works**, but is significantly slower than on Linux with CUDA.
    - Windows support may **lag behind** Linux.
    - Windows will be **tested less frequently**, since Linux is the primary
    - Community contributions that improve Windows support are very welcome.
    Not all CUDA versions are supported by MuJoCo Warp.
    - See `mujoco_warp#101 <https://github.com/google-deepmind/mujoco_warp/issues/101>`_
    - **Recommended**: CUDA **12.4+** (for conditional execution support in CUDA
    on the GPU. See `issue #949
    <https://github.com/mujocolab/mjlab/issues/949>`_ for background.
    - **RTX 40-series GPUs** (or newer)
    - **L40s, H100**
    Does mjlab support multi-GPU training?
    Yes, mjlab supports **multi-GPU distributed training** using
    - Use ``--gpu-ids "[0, 1]"`` (or ``--gpu-ids all``) when running the ``train``
    - See the :doc:`training/distributed_training` for configuration details and examples.
    RuntimeError: normal expects all elements of std >= 0.0
    1. **For training stability** - NaN termination
    # In your ManagerBasedRlEnvCfg subclass:
    # Your other terminations...
    (for example, NaNs occur exactly when the agent tries to grasp an object),
    2. **For debugging** - NaN guard
    - Inspect the simulation state at the moment NaNs appear.
    - Build a minimal reproducible example (MRE).
    - Report potential framework bugs to the
    uv run export-scene g1 --output-dir /tmp/g1
    inspection or diffing. This is useful for verifying that task configuration...
  - [M] docs/source/entity/index.rst
    Excerpt:
    .. _entity:
    Entity
    ======
    An ``Entity`` represents a physical object in the simulation: a robot, a
    manipulated object, or a fixed fixture like a table. It is the central
    abstraction in mjlab's physics layer.
    A single ``Entity`` class covers all variants (contrast Isaac...
