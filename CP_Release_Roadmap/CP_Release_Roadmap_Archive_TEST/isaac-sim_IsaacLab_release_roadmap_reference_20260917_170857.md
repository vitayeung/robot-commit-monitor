# isaac-sim/IsaacLab Release Roadmap Reference

- 仓库: `isaac-sim/IsaacLab`
- 对应主报告: `isaac-sim_IsaacLab_release_roadmap.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要
- 版本总数: 9
- 正式版数量: 6
- 预发布版数量: 3
- 外链文档覆盖版本数: 6
- compare 摘要覆盖版本数: 8
- 最新版本: v3.0.0-beta2.patch1 (2026-07-02 12:21:18 CST)
- 最早纳入统计版本: v2.1.1 (2025-07-30 20:59:44 CST)

## 分析策略决策
- 请求模式: `auto`
- 最终策略: `L1: Release-first`
- 证据充分性评分: 1/6
- 触发规则: migration_risk_high
- 决策说明:
  - 常规高层路线图默认保持 L1，仅在证据明显不足时升级到 L2。
  - 证据充分性评分 1/6，触发规则: migration_risk_high。
  - 因此主脚本保持 L1，避免在主流程里默认引入额外源码分析成本。

## Release 时间线
- 2026-07-02 12:21:18 CST | v3.0.0-beta2.patch1 | 预发布版
- 2026-06-17 10:16:55 CST | v3.0.0-beta2 | 预发布版
- 2026-03-17 14:38:37 CST | v3.0.0-beta | 预发布版
- 2026-02-03 02:54:35 CST | v2.3.2 | 正式版
- 2025-12-05 06:26:35 CST | v2.3.1 | 正式版
- 2025-10-29 05:38:54 CST | v2.3.0 | 正式版
- 2025-08-30 01:58:55 CST | v2.2.1 | 正式版
- 2025-08-08 03:42:33 CST | v2.2.0 | 正式版
- 2025-07-30 20:59:44 CST | v2.1.1 | 正式版

## 证据附录

### v3.0.0-beta2.patch1
- 标题: v3.0.0-beta2.patch1
- 类型: 预发布版
- 发布时间: 2026-07-02 12:21:18 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-beta2.patch1
- GitHub release body:
# Isaac Lab 3.0 Beta 2 - Patch 1

This is a small patch release on top of the previous Isaac Lab 3.0.0 Beta 2 release, including an update to support Isaac Sim 6.0.1, which includes fixes and improvements for NuRec workflows (https://docs.isaacsim.omniverse.nvidia.com/6.0.1/overview/release_notes.html). Additionally, some fixes were introduced for Isaac Lab dependencies and docker image to better support compatibility with Isaac Sim.

## What's Changed
* Bump h5py version to >=3.16.0 by @peterd-NV in https://github.com/isaac-sim/IsaacLab/pull/6266
* Updates Isaac Sim to version 6.0.1 by @kellyguo11 in https://github.com/isaac-sim/IsaacLab/pull/6277
* [Fix] Cherry-pick Isaac Sim 6.0 streaming crash fix by @hujc7 in https://github.com/isaac-sim/IsaacLab/pull/6295

**Full Changelog**: https://github.com/isaac-sim/IsaacLab/compare/v3.0.0-beta2...v3.0.0-beta2.patch1
- 外链文档摘录:
  - https://docs.isaacsim.omniverse.nvidia.com/6.0.1/overview/release_notes.html
    Updated to Kit SDK 110.1.1 -> 110.1.2
    Added teleoperation support for NuRec scenes that render through Sparse Pixel Gaussian (SPG) graphs, plus volume NuRec detection in addition to particle scenes.
    Changed: 110.1.1 -> 110.1.2
    Kit SDK Dependency Version Changes#
    omni.usd.metrics.assembler.usdgeom: 0.1.0
    isaacsim.app.compatibility_check: 1.1.3 -> 1.1.4
    isaacsim.exp.full: 6.0.0 -> 6.0.1
    isaacsim.replicator.agent.core: 1.6.7 -> 1.6.8
    isaacsim.sensors.rtx.calibration: 0.3.9 -> 0.3.10
    isaacsim.sensors.rtx.placement: 0.16.9 -> 0.16.10
    isaacsim.util.debug_draw: 3.2.2 -> 3.2.3
    omni.anim.behavior.ui: 110.1.3 -> 110.1.4
    omni.cip.core: 2.0.17 -> 2.0.23
    omni.cip.mega: 2.0.14 -> 2.0.18
    omni.cip.mega.scenario_payload_ui: 2.0.5 -> 2.0.6
    omni.cip.mega.ui: 2.0.14 -> 2.0.18
    omni.cip.mega.waypoints_ui: 2.0.4 -> 2.0.5
    omni.cip.pip: 2.0.1 -> 2.0.5
    omni.cip.ui: 2.0.3 -> 2.0.5
    omni.cip.workspace: 2.0.1 -> 2.0.3
    omni.cip.wrapp_ui: 2.0.1 -> 2.0.2
    omni.convexdecomposition: 110.1.11 -> 110.1.13
    omni.cuopt.examples: 1.4.1 -> 1.4.2
    omni.cuopt.service: 1.3.2 -> 1.3.3
    omni.cuopt.visualization: 1.4.1 -> 1.4.2
    omni.graph.action_nodes: 2.10.3 -> 2.11.0
    omni.graph.action_nodes_core: 2.10.2 -> 2.11.0
    omni.graph.examples.cpp: 2.10.3 -> 2.11.0
    omni.graph.nodes: 2.11.1 -> 2.12.0
    omni.graph.nodes_core: 2.10.3 -> 2.11.0
    omni.graph.telemetry: 3.10.3 -> 3.11.1
    omni.graph.ui_nodes: 2.10.5 -> 2.11.1
    omni.kit.asset_converter: 5.1.4 -> 6.0.1
    omni.kit.converter.dgn: 510.1.4 -> 510.1.5
    omni.kit.converter.dgn_core: 512.3.0 -> 512.3.3
    omni.kit.converter.hoops_core: 511.3.0 -> 511.3.2
    omni.kit.converter.jt_core: 510.1.0 -> 510.1.1
    omni.kit.property.physics: 110.1.11 -> 110.1.13
    omni.kit.stagerecorder.bundle: 110.0.0 -> 110.0.2
    omni.kit.stagerecorder.core: 110.0.9 -> 110.0.14
    omni.kit.stagerecorder.ui: 110.0.0 -> 110.0.2
    omni.kit.tool.asset_exporter: 4.0.7 -> 5.0.1
    omni.kit.tool.asset_importer: 5.2.0 -> 6.0.1
    omni.kit.variant.presenter: 107.1.3 -> 107.1.6
    omni.physics: 110.1.11 -> 110.1.13
    omni.physics.isaacsimready: 110.1.11 -> 110.1.13
    omni.physics.physx: 110.1.11 -> 110.1.13
    omni.physics.physx.ui: 110.1.11 -> 110.1.13
- Compare 摘要: v3.0.0-beta2 -> v3.0.0-beta2.patch1
  - commits: 10
  - files changed: 31
  - additions: 262
  - deletions: 127
  - top directories: .github, README.md, docker, docs/_extensions, docs/conf.py, docs/source
  - representative files:
    - source/isaaclab/isaaclab/cli/commands/install.py (modified, +87/-43)
    - source/isaaclab/docs/CHANGELOG.rst (modified, +39/-0)
    - source/isaaclab/test/cli/test_install.py (modified, +33/-0)
    - docker/Dockerfile.base (modified, +15/-16)
    - docker/Dockerfile.curobo (modified, +15/-14)
    - source/isaaclab/test/cli/test_install_commands.py (modified, +10/-13)
    - source/isaaclab/setup.py (modified, +4/-5)
    - source/isaaclab_mimic/docs/CHANGELOG.rst (modified, +9/-0)

### v3.0.0-beta2
- 标题: v3.0.0-beta2
- 类型: 预发布版
- 发布时间: 2026-06-17 10:16:55 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-beta2
- GitHub release body:
# Isaac Lab 3.0 Beta 2 🚀

Isaac Lab 3.0 Beta 2 is a stabilization and enablement release for the Isaac Lab 3.0 beta development. It builds on [v3.0.0-beta](https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-beta) with additional features and improvements on Newton support (VBD, solver coupling, Kamino, rough terrain, sensors), multi-backend physics, simplified training and installation commands, kit-less workflows, visualizers, rendering, teleoperation, learning exports, installation, CI, and documentation.

This release is compatible with the latest release of [Isaac Sim 6.0](https://docs.isaacsim.omniverse.nvidia.com/6.0.0/installation/download.html).

> This is a beta release. The develop branch is still under active development and may continue to receive breaking changes, error-message changes, or performance tuning before the final 3.0 release. Please check out the `develop` branch for the latest development updates.

---

## ✨ Highlights

### Multi-Backend Stabilization

The multi-backend architecture introduced in the first 3.0 beta has been hardened across PhysX, Newton, OVPhysX, Isaac RTX, OVRTX, and kit-less execution paths. This release improves backend selection, scene-data routing, clone-plan handling, sensor reset behavior, runtime compatibility checks, and error reporting when unsupported physics, renderer, or visualizer combinations are requested.

### Newton Physics & Kit-Less Workflows

Newton and OVPhysX support have been expanded and stabilized for larger kit-less training and visualization workflows:

* Adds Newton ray-caster, frame-transformer, IMU/PVA, contact, joint-wrench, deformable, and VBD-coupling support across the relevant packages.
* Adds Newton rough-terrain locomotion presets for quadrupeds and bipeds, plus additional MJWarp...
- 外链文档摘录:
  - https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-beta
    Release v3.0.0-beta · isaac-sim/IsaacLab · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork3.7k
    kellyguo11released this17 Mar 06:38
    Isaac Lab 3.0 Beta 🚀
    branch is under active development and may experience breaking changes, error messages, or performance regressions in some use cases.
    Isaac Lab 3.0 introduces afactory-based multi-backend architecturethat separates simulation backend–specific code from the core API. Asset and sensor classes (e.g.,
    — Full PhysX backend (default), including deformable objects, surface grippers, contact sensors, IMU, and frame transformers.
    — New Newton physics backend powered by MuJoCo-Warp, supporting MJWarp, XPBD, and Featherstone solvers with CUDA-graph acceleration.
    extension enables running Isaac Lab environmentswithout Isaac Sim(kit-less mode). Newton support includes:
    - Contact sensors
    - MuJoCo-Warp solver with configurable integrators (
    - CUDA graph support for high-throughput stepping
    - Newton-compatible presets for 20+ environments (locomotion, manipulation, classic control)
    abstraction supports multiple rendering backends via a factory pattern:
    Full sensor fidelity, photorealistic rendering
    Isaac Lab 3.0 introduces a newpluggable visualizer framework(
    ) with four interchangeable backends, all decoupled from the physics engine and renderer:
    USD stage, visual markers, live training plots
    Browser-based via Newton Warp renderer, public share URLs,
    flag (replaces the deprecated
    python train.py --task Isaac-Cartpole-v0 --viz kit,newton,rerun
    python train.py --task Isaac-Cartpole-v0 --viz newton
    python train.py --task Isaac-Cartpole-v0 --viz viser
    python train.py --task Isaac-Cartpole-v0
    properties on asset and sensor classes now return
    ), and fused GPU kernels replace Python-level loops for state extraction, velocity transforms, and data write-back. Convert back to torch with
    python train.py task=Isaac-Ant-v0 presets=newton
    python train.py task=Isaac-Ant-v0
    All packages now use lazy exporting with .pyi stubs, so importing a top-level module (e.g., import isaaclab.sensors) no longer eagerly pulls in heavyweight dependencies. Config fields like class_type store references as resolvable strings that are resolved only after SimulationApp is initialized, enabling automatic physics-backend selection.
    All quaternions throughout Isaac Lab now use XYZW ordering to align with Warp, PhysX, and Newton conventions. Hard-coded quaternion values must be updated. A quaternion finder tool is provided to help locate and fix quaternions.
    for PyTorch compatibility. An automated migration tool is available at
    - Sensor
    URDF & MJCF Importers Updated
    Both importers have been rewritten for Isaac Sim 6.0. Several configuration settings have been removed, renamed, or replaced. See theMigration Guidefor details.
    - Python 3.12
    - PyTorch 2.10.0+cu128
    - NumPy 2.3.1
    - Isaac Sim 6.0
    - Ubuntu only — The develop branch is currently available on Ubuntu. Windows support and Isaac Lab pip wheels will be available soon.
    - Performance regressions may be observed in some use cases as the multi-backend architecture stabilizes.
    - Breaking changes may still occur on the develop branch before the final 3.0 release.
    For a comprehensive guide on migrating from Isaac Lab 2.x to 3.0, including code examples, API rename tables, and automated tooling, see theMigration Guide.
    🎉28ZzzzzzS, qianl-nv, rthaker01, sheikh-nv, evanzijianhe, johnsutor, IvolgaDmitriy, seawee1, diegoferigo-rai, momo-van, and 18 more reacted with hooray emoji
    - 🎉28 reactions
  - https://docs.isaacsim.omniverse.nvidia.com/6.0.0/installation/download.html
    Omniverse Launcher, Nucleus Workstation, and Nucleus Cache will be deprecated and will no longer be available starting October 1, 2025.
    For those who want to use Nucleus and Live Sync after October 1, 2025, please useEnterprise Nucleus Server.
    Using the latest version of Isaac Sim is recommended to receive the latest security patches and bug-fixes.
    Complete (Part 1 of 5)
    Complete (Part 2 of 5)
    Complete (Part 3 of 5)
    Complete (Part 4 of 5)
    Complete (Part 5 of 5)
    The Complete Pack is split into five parts. Use the MD5 checksums above with theLocal Assets PacksAria2 example to resume interrupted downloads and verify each part, then combine and extract them.
- Compare 摘要: v3.0.0-beta -> v3.0.0-beta2
  - commits: 420
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 14040
  - deletions: 3341
  - top directories: .dockerignore, .gitattributes, .github, .gitignore, AGENTS.md, CONTRIBUTORS.md
  - representative files:
    - docs/source/overview/environments.rst (modified, +895/-422)
    - .github/workflows/build.yaml (modified, +574/-610)
    - docs/source/migration/migrating_to_isaaclab_3-0.rst (modified, +848/-54)
    - docs/source/overview/core-concepts/visualization.rst (added, +684/-0)
    - docs/source/overview/imitation-learning/teleop_imitation.rst (modified, +350/-173)
    - docs/source/how-to/cloning.rst (modified, +306/-173)
    - docs/source/features/visualization.rst (removed, +0/-464)
    - docs/source/features/isaac_teleop.rst (modified, +391/-17)

### v3.0.0-beta
- 标题: v3.0.0-beta
- 类型: 预发布版
- 发布时间: 2026-03-17 14:38:37 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-beta
- GitHub release body:
# Isaac Lab 3.0 Beta 🚀

Isaac Lab 3.0 Beta is the next major release of Isaac Lab, built on **Isaac Sim 6.0** and introducing a ground-up architectural overhaul. This release brings multi-backend physics, a pluggable renderer system, Warp-native data pipelines, and a kit-less installation mode — enabling faster, more flexible robot learning research.

> ⚠️ **This is a beta release.** The `develop` branch is under active development and may experience breaking changes, error messages, or performance regressions in some use cases.

---

## ✨ Highlights

### Multi-Backend Physics Architecture
Isaac Lab 3.0 introduces a **factory-based multi-backend architecture** that separates simulation backend–specific code from the core API. Asset and sensor classes (e.g., `Articulation`, `RigidObject`, `ContactSensor`) are now backed by abstract base classes, with backend-specific implementations in dedicated extension packages:

- **`isaaclab_physx`** — Full PhysX backend (default), including deformable objects, surface grippers, contact sensors, IMU, and frame transformers.
- **`isaaclab_newton`** — New Newton physics backend powered by MuJoCo-Warp, supporting MJWarp, XPBD, and Featherstone solvers with CUDA-graph acceleration.

Your existing imports from `isaaclab.assets` and `isaaclab.sensors` continue to work — the factory automatically dispatches to the active backend at runtime.

### Newton Physics Backend
The new `isaaclab_newton` extension enables running Isaac Lab environments **without Isaac Sim** (kit-less mode). Newton support includes:

- Articulations, rigid objects, and rigid object collections
- Contact sensors
- MuJoCo-Warp solver with configurable integrators (`implicitfast`, `euler`) and contact models (`pyramidal`, `elliptic`)
- CUDA graph support for high-thro...
- 外链文档摘录:
  - https://isaac-sim.github.io/IsaacLab/develop/source/migration/migrating_to_isaaclab_3-0.html
    Migrating to Isaac Lab 3.0 — Isaac Lab Documentation
    Migrating to Isaac Lab 3.0
    Migrating to Isaac Lab 3.0#
    Isaac Lab 3.0 introduces a multi-backend architecture that separates simulation backend-specific code
    from the core Isaac Lab API. This allows for future support of different physics backends while
    maintaining a consistent user-facing API.
    This guide covers the main breaking changes and deprecations you need to address when migrating
    from Isaac Lab 2.x to Isaac Lab 3.0.
    In Isaac Lab 3.0, the
    argument is deprecated. Instead, use
    is deprecated (still supported) and overrides
    Isaac Lab 3.0 provides unified reinforcement learning entrypoints for training
    # Isaac Lab 2.x/deprecated./isaaclab.sh-pscripts/reinforcement_learning/rsl_rl/train.py--taskIsaac-Cartpole# Isaac Lab 3.0./isaaclab.shtrain--rl_libraryrsl_rl--taskIsaac-Cartpole
    Supported reinforcement learning libraries are
    remain available as deprecated compatibility entrypoints and emit a
    For distributed launchers that execute a Python script directly, use the unified
    python-mtorch.distributed.run--nproc_per_node=2scripts/reinforcement_learning/train.py\--rl_libraryrsl_rl--taskIsaac-Cartpole--distributed
    Isaac Lab 3.0 introduces afactory-based multi-backend architecturethat allows asset classes
    fromisaaclab.assetsimportArticulation,ArticulationCfg# The factory pattern creates the appropriate backend implementation.# No import changes are needed — the same isaaclab imports work regardless of backend.robot=Articulation(cfg=ArticulationCfg(...))
    by default. Newton backend support is being
    For a comprehensive overview of the factory pattern, backend selection, and how to add a new
    ``isaaclab_physx``— PhysX-specific implementations of asset and sensor classes.
    ``isaaclab_newton``— Newton-specific implementations of supported asset classes, including
    Deformable object public APIs remain in the backend-neutral
    extension is installed automatically with Isaac Lab. No additional
    In Isaac Lab 3.0, the spawner schema cfg classes are split into solver-commonbase classes(in
    the same asset cfg portable across PhysX and Newton backends, and adds slots
    The following 2.x class names are kept as deprecated aliases. They forward to
    the new location and will be removed in 4.0.
    Existing 2.x code continues to work via the deprecation aliases (with a
    ; removed in 4.0):
    # Isaac Lab 2.ximportisaaclab.simassim_utilsrigid_props=sim_utils.RigidBodyPropertiesCfg(disable_gravity=True,linear_damping=0.1)
    Recommended 3.0 pattern when targeting PhysX:
    # Isaac Lab 3.0 — PhysX backendfromisaaclab_physx.sim.schemasimportPhysxRigidBodyPropertiesCfgrigid_props=PhysxRigidBodyPropertiesCfg(disable_gravity=True,linear_damping=0.1)
    Backend-portable 3.0 pattern (universal-physics fields only):
    # Isaac Lab 3.0 — backend-portablefromisaaclab.sim.schemasimportRigidBodyBaseCfgrigid_props=RigidBodyBaseCfg(rigid_body_enabled=True,disable_gravity=True)
    USD camelCase attribute names. The old names remain as deprecated dataclass
    scheduled for removal in 4.0.
    Isaac Lab 2.x style still works (emits
    Recommended 3.0 pattern, backend-portable:
    Recommended 3.0 pattern, PhysX-targeted:
    For the Newton backend (and Newton’s MuJoCo solver), new cfg classes are
    (body-level gravity compensation, MuJoCo solver only)
    . SeeGravity compensation (MuJoCo solver)for details.
    USD, seeSchema Configuration Classes.
    name is kept as a deprecated alias.
    For most users, the only change needed is updating imports:
    physics backend. The deprecated
- Compare 摘要: v2.3.2 -> v3.0.0-beta
  - commits: 309
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 10995
  - deletions: 5735
  - top directories: .gitattributes, .github, .gitignore, .pre-commit-config.yaml, .vscode, AGENTS.md
  - representative files:
    - docs/source/migration/migrating_to_isaaclab_3-0.rst (added, +1406/-0)
    - docs/source/how-to/cloudxr_teleoperation.rst (modified, +334/-925)
    - docs/source/features/isaac_teleop.rst (added, +836/-0)
    - docs/source/overview/imitation-learning/teleop_imitation.rst (modified, +162/-634)
    - isaaclab.sh (modified, +18/-760)
    - docs/source/overview/imitation-learning/humanoids_imitation.rst (added, +777/-0)
    - .github/workflows/build.yaml (added, +776/-0)
    - isaaclab.bat (modified, +20/-659)

### v2.3.2
- 标题: v2.3.2
- 类型: 正式版
- 发布时间: 2026-02-03 02:54:35 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v2.3.2
- GitHub release body:
## What's Changed

This release focuses on stability, infrastructure improvements, workflow refinements, and incremental feature expansions, along with some significant new features, including **Multirotor and thruster support for drones**, **Multi-mesh RayCaster**, **Visual-based tactile sensor**, **Haply device integration**, and new **OpenArm environments**.

This release also includes improvements to training workflows, teleoperation and Mimic pipelines, Ray integration, simulation utilities, and developer tooling, along with a large number of robustness and quality-of-life fixes.

https://github.com/user-attachments/assets/19624490-b9ef-41d4-8a74-67ccf96fdaed

https://github.com/user-attachments/assets/3222f88d-46ee-4816-8d73-d8910b83d4a8

**Full Changelog**: https://github.com/isaac-sim/IsaacLab/compare/v2.3.1...v2.3.2

> [!NOTE]
>This will be the final release from the current main branch as we shift our development focus to the develop branch.
>
> Significant restructuring is planned on [`develop`](https://github.com/isaac-sim/IsaacLab/tree/develop) as we work toward Isaac Lab 3.0. We welcome continued community
> contributions, but active development will primarily occur on develop going forward.
>
> If you have an open PR, please retarget it to develop to ensure it remains aligned with the latest changes.

## ✨ New Features

### Core & Simulation

* Adds Raycaster with tracking support for dynamic meshes by @renezurbruegg in #3298
* Adds visual-based tactile sensor with shape sensing example by @JuanaDd in #3420
* Adds wrench composers allowing the composition of multiple wrenches on the same bodies by @AntoineRichard in #3287
* Adds multirotor/thruster actuator, multirotor asset and manager-based ARL drone task #3760 by @mihirk284 @grzemal @Zwoelf12
* Adds...
- Compare 摘要: v2.3.1 -> v2.3.2
  - commits: 216
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 12796
  - deletions: 2376
  - top directories: .dockerignore, .flake8, .gitattributes, .github, .gitignore, .pre-commit-config.yaml
  - representative files:
    - scripts/imitation_learning/locomanipulation_sdg/generate_data.py (added, +774/-0)
    - scripts/benchmarks/benchmark_xform_prim_view.py (added, +631/-0)
    - docs/source/policy_deployment/02_gear_assembly/gear_assembly_policy.rst (added, +605/-0)
    - docs/source/refs/release_notes.rst (modified, +586/-3)
    - scripts/benchmarks/benchmark_view_comparison.py (added, +512/-0)
    - docs/source/migration/comparing_simulation_isaacgym.rst (added, +503/-0)
    - docs/source/setup/installation/binaries_installation.rst (modified, +19/-420)
    - docs/licenses/dependencies/ruff-license.txt (added, +430/-0)

### v2.3.1
- 标题: v2.3.1
- 类型: 正式版
- 发布时间: 2025-12-05 06:26:35 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v2.3.1
- GitHub release body:
## What's Changed

This is a small patch release with a few critical fixes that impacted user workflows.

Key fixes include:
* The behavior of termination logging has changed in the manager-based workflow, where `get_done_term` now returns the current step value instead of the last episode value.
* Additionally, a breaking change in the URDF importer was introduced in Isaac Sim 5.1, where the merge joints flag is no longer supported. We have now introduced a patch in the importer to return the behavior. Moving forward, we plan to deprecate this flag in favor of preserving asset definitions from URDFs directly without performing additional processing during the import process.

## 🐛 Bug Fixes

* Updates URDF importer to 2.4.31 to continue support for merge-joints by @kellyguo11 in #4000
* Separates per-step termination and last-episode termination bookkeeping by @ooctipus in #3745
* Uses effort_limit from USD if not specified in actuator cfg by @JuanaDd in #3522
* Fixes type name for tendon properties in from_files config by @KyleM73 in #3941
* Fixes duplicated text in pip installation docs by @shryt in #3969
* Pins python version of pre-commmit.yaml workflow by @hhansen-bdai in #3929

## 📜 Documentation

* Updates the mimic teleop doc to link to the locomotion policy training by @huihuaNvidia2023 in #4053

**Full Changelog**: https://github.com/isaac-sim/IsaacLab/compare/v2.3.0...v2.3.1
- Compare 摘要: v2.3.0 -> v2.3.1
  - commits: 9
  - files changed: 34
  - additions: 303
  - deletions: 57
  - top directories: .github, CITATION.cff, CONTRIBUTORS.md, README.md, VERSION, apps
  - representative files:
    - source/isaaclab/test/managers/test_termination_manager.py (added, +140/-0)
    - source/isaaclab/docs/CHANGELOG.rst (modified, +31/-0)
    - source/isaaclab/test/assets/test_articulation.py (modified, +25/-6)
    - docs/source/refs/release_notes.rst (modified, +28/-0)
    - source/isaaclab/isaaclab/actuators/actuator_base.py (modified, +20/-4)
    - source/isaaclab/isaaclab/managers/termination_manager.py (modified, +12/-7)
    - docs/source/overview/imitation-learning/teleop_imitation.rst (modified, +10/-0)
    - source/isaaclab/test/actuators/test_ideal_pd_actuator.py (modified, +3/-5)

### v2.3.0
- 标题: v2.3.0
- 类型: 正式版
- 发布时间: 2025-10-29 05:38:54 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v2.3.0
- GitHub release body:
## What's Changed

The Isaac Lab 2.3.0 release, built on Isaac Sim 5.1, delivers enhancements across dexterous manipulation, teleoperation, and learning workflows. It introduces new dexterous environments with advanced training capabilities, expands surface gripper and teleoperation support for a wider range of robots and devices, and integrates SkillGen with the Mimic imitation learning pipeline to enable GPU-accelerated motion planning and skill-based data generation with cuRobo integration.

Key highlights of this release include:

- **Dexterous RL (DexSuite)**:  Introduction of two new dexterous manipulation environments using the Kuka arm and Allegro hand setup, with addition of support for Automatic Domain Randomization (ADR) and PBT (Population-Based Training).
- **Surface gripper updates**: Surface gripper has been extended to support Manager-based workflows, including the addition of `SurfaceGripperAction` and `SurfaceGripperActionCfg`, along with several new environments demonstrating teleoperation examples with surface grippers and the RMPFlow controller. New robots and variations are introduced, including Franka and UR10 with robotiq grippers and suction cups, and Galbot and Agibot robots.
- **Mimic - SkillGen**: SkillGen support has been added for the Mimic Imitation Learning pipeline, introducing cuRobo integration, integrating GPU motion planning with skill-segmented data generation. Note that cuRobo has proprietary licensing terms, please review the [cuRobo license](https://github.com/isaac-sim/IsaacLab/blob/main/docs/licenses/dependencies/cuRobo-license.txt) carefully before use.
- **Mimic - Locomanipulation**: Added a new G1 humanoid environment combining RL-based locomotion with IK-based manipulation. A full robot navigation stack is integrated to...
- 外链文档摘录:
  - https://github.com/isaac-sim/IsaacLab/blob/main/docs/licenses/dependencies/cuRobo-license.txt
    - NotificationsYou must be signed in to change notification settings
    - Fork3.7k
    93 lines (47 loc) · 17.1 KB
    NVIDIA ISAAC LAB ADDITIONAL SOFTWARE AND MATERIALS LICENSE
    1. License Grant. The Software made available by NVIDIA to you is licensed, not sold. Subject to the terms of this Agreement, NVIDIA grants you a limited, non-exclusive, revocable, non-transferable, and non-sublicensable (except as expressly granted in this Agreement), license to install and use copies of the Software together with NVIDIA Isaac Lab in systems with NVIDIA GPUs ("Purpose").
    2. License Restrictions. Your license to use the Software is restricted as stated in this Section 2 ("License Restrictions"). You will cooperate with NVIDIA and, upon NVIDIA's written request, you will confirm in writing and provide reasonably requested information to verify your compliance with the terms of this Agreement. You may not:
    2.1 Use the Software for any purpose other than the Purpose, and for clarity use of NVIDIA cuRobo apart from use with Isaac Lab is outside of the Purpose;
    2.2 Sell, rent, sublicense, transfer, distribute or otherwise make available to others (except authorized users as stated in Section 3 ("Authorized Users")) any portion of the Software, except as expressly granted in Section 1 ("License Grant");
    2.3 Reverse engineer, decompile, or disassemble the Software components provided in binary form, nor attempt in any other manner to obtain source code of such Software;
    2.4 Modify or create derivative works of the Software;
    2.6 Bypass, disable, or circumvent any technical limitation, encryption, security, digital rights management or authentication mechanism in the Software;
    2.7 Use the Software in any manner that would cause them to become subject to an open source software license, subject to the terms in Section 7 ("Components Under Other Licenses"); or
    2.8 Use the Software in violation of any applicable law or regulation in relevant jurisdictions.
    3. Authorized Users. You may allow employees and contractors of your entity or of your subsidiary(ies), and for educational institutions also enrolled students, to internally access and use the Software as authorized by this Agreement from your secure network to perform the work authorized by this Agreement on your behalf. You are responsible for the compliance with the terms of this Agreement by your authorized users. Any act or omission that if committed by you would constitute a breach of this Agreement will be deemed to constitute a breach of this Agreement if committed by your authorized users.
    4. Pre-Release. Software versions identified as alpha, beta, preview, early access or otherwise as pre-release ("Pre-Release") may not be fully functional, may contain errors or design flaws, and may have reduced or different security, privacy, availability and reliability standards relative to NVIDIA commercial offerings. You use Pre-Release Software at your own risk. NVIDIA did not design or test the Software for use in production or business-critical systems. NVIDIA may choose not to make available a commercial version of Pre-Release Software. NVIDIA may also choose to abandon development and terminate the availability of Pre-Release Software at any time without liability.
    5. Updates. NVIDIA may at any time and at its option, change, discontinue, or deprecate any part, or all, of the Software, or change or remove features or functionality, or make available patches, workarounds or other updates to the Software. Unless the updates are provided with their separate governing terms, they are deemed part of the Software licensed to you under this Agreement, and your continued use of the Software is deemed acceptance of such changes.
    6. Components Under Other Licenses. The Software may include or be distributed with components provided with separate legal notices or terms that accompany the components, such as open source software licenses and other license terms ("Other Licenses"). The components are subject to the applicable Other Licenses, including any proprietary notices, disclaimers, requirements and extended use rights; except that this Agreement will prevail regarding the use of third-party open source software, unless a third-party open source software license requires its license terms to prevail. Open source software license means any software, data or documentation subject to any license identified as an open source license by the Open Source Initiative (http://opensource.org), Free Software Foundation (http://www.fsf.org) or other similar open source organization or listed by the Software Package Data Exchange (SPDX) Workgroup under the Linux Foundation (http://www.spdx.org).
    7. Ownership. The Software, including all intellectual property rights, is and will remain the sole and exclusive property of NVIDIA or its licensors. Except as expressly granted in this Agreement, (a) NVIDIA reserves all rights, interests and remedies in connection with the Software, and (b) no other licen...
  - https://docs.omniverse.nvidia.com/kit/docs/omni_physics/107.3/dev_guide/guides/gripper_tuning_example.html
    Joint Parameter Tuning Example: Robotiq 2F-85 — Omni Physics
    Joint Parameter Tuning Example: Robotiq 2F-85#
    The purpose of this document is to provide an example of tuning physics parameters for articulation joints, specifically joint drives, in the context of robotic gripper assets. The focus will be on joint drives based on a spring/damper model. This tuning example is geared towards using PhysX as the simulation backend, however, some of the recommendations likely apply to other simulators too. The robot gripper chosen for this tuning example is the Robotiq 2F-85 gripper.
    Please note that this document is not intended as a comprehensive tuning guide. Corresponding information is available already (see theLinkssection). This document simply demonstrates an application of some of that knowledge. Additionally, there are some helper tools available, such as the gain tuner extension (see theLinkssection).
    Note that all the parameter estimation helpers used in this document are very crude. They are not intended to provide precise results but to get a rough understanding of the value range from which to choose your parameters. With that in mind, a value of 10 m/s2will be used for gravity in all computations.
    When tuning something like a gripper, it is often helpful to first create a set of very simple scenes that only contain the gripper (or just the hand part for a full humanoid robot) and one object to grasp. One testing sequence could involve starting with an open gripper and placing the object to grip between the pincers or fingers. Begin with gravity disabled on the object to grip. Let the gripper close around the object and observe for any instabilities or penetration. Once the gripping action reaches a steady state, enable gravity on the gripped object and check again for instabilities, penetration and whether the gripper can maintain its grip in the presence of gravity. An additional force can be applied on the grasped object to emulate a lifting movement.
    For the object to grasp, choose a primitive shape, such as a box or cylinder. Use 2-3 versions of this object to check the gripperâs behavior at different levels of closing. For example, use a thick box so that the gripper is almost fully open when gripping, a thin box so that the gripper is nearly fully closed, and a third setup where the gripper is somewhere between fully open and fully closed when gripping.
    Figure 8Example scenarios for testing the gripper.#
    The gripper chosen for this example is the Robotiq 2F-85. The joints relevant to this exercise are shown in the image below.
    Figure 9Joint setup for the Robotiq 2F-85.#
    Six revolute joints were used to model the degrees of freedom of the gripper. It is a simplified version that does not use loop-closing joints. Joint J0is the only joint with a drive. The other five joints are all mimic joints of joint J0and are driven indirectly through that joint. The gearing value for all mimic joints is 1 (or -1), and the offset is 0. Joint J0has a motion range from 0 to 47 degrees, with 0 degrees resulting in the gripper being fully open and 47 degrees resulting in the gripper being fully closed.
    The Robotiq gripper has a useful example in the specifications, stating that it can hold a 5 kg box, assuming a friction coefficient of 0.3. Letâs use that setup and estimate how it translates to the joint drive at J0. Holding 5 kg with a friction coefficient of 0.3 requires a force of roughly
    (1)#\[\frac{mass \cdot gravity}{0.3} = \frac{5 \; kg \cdot 10 \; m/s^2}{0.3} \approx 166 \; N\]
    That is the sum of the forces from both gripper fingers, so the force per finger is 83 N. However, we need to determine the torque at the joint, not the force at the contact point. The relationship between torque and force is given by:
    (2)#\[\tau = F \cdot r\]
    To calculate the torque\(\tau\), the âlever armâ r must be estimated. By examining the dimensions of the link that contains the finger pads, a rough estimate can be made. We will use a value of 0.04 m. As a result, the torque will be:
    (3)#\[\tau = F \cdot r = 83 \; N \cdot 0.04 \; m \approx 3.3 \; Nm\]
    Letâs round the value up and use 4 Nm to allow for a bit of a margin. Note that the link containing the finger pad is not directly connected to joint J0, which has the drive. However, all the joints are connected via a mimic to the driven joint J0, and as such, all joints are considered to be driven here. Furthermore, the gearing ratio for all mimic joints is 1. Thus, we can make the generous assumption that each joint will experience the same torque from the drive. To summarize, the estimated torque of 4 Nm is considered to be the maximum drive force for each joint.
    One last important consideration before using this value to set the maximum drive force on joint J0: the estimated torque is per joint, but joint J0has to drive all six joints (itself plus the five mimic joints). Consequently, the maximum drive force on joint J0is set to:
    (4)#\[J_0 \; maxDriveForce = 6...
- Compare 摘要: v2.2.1 -> v2.3.0
  - commits: 168
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 13286
  - deletions: 2323
  - top directories: .github, .gitignore, CITATION.cff, CONTRIBUTORS.md, README.md, VERSION
  - representative files:
    - scripts/imitation_learning/locomanipulation_sdg/generate_data.py (added, +774/-0)
    - source/isaaclab/test/controllers/test_controller_utils.py (added, +662/-0)
    - source/isaaclab/isaaclab/ui/xr_widgets/scene_visualization.py (added, +609/-0)
    - docs/source/overview/imitation-learning/skillgen.rst (added, +548/-0)
    - source/isaaclab/isaaclab/devices/openxr/manus_vive_utils.py (added, +509/-0)
    - source/isaaclab/test/controllers/test_local_frame_task.py (added, +481/-0)
    - docs/source/setup/installation/binaries_installation.rst (modified, +19/-420)
    - docs/source/setup/installation/pip_installation.rst (modified, +54/-337)

### v2.2.1
- 标题: v2.2.1
- 类型: 正式版
- 发布时间: 2025-08-30 01:58:55 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v2.2.1
- GitHub release body:
## 👀 Overview

This is a minor patch release with some improvements and bug fixes.

**Full Changelog**: https://github.com/isaac-sim/IsaacLab/compare/v2.2.0...v2.2.1

## ✨ New Features

* Adds contact point location reporting to ContactSensor by @jtigue-bdai in https://github.com/isaac-sim/IsaacLab/pull/2842
* Adds environments actions/observations descriptors for export by @AntoineRichard in https://github.com/isaac-sim/IsaacLab/pull/2730
* Adds RSL-RL symmetry example for cartpole and ANYmal locomotion by @Mayankm96 in https://github.com/isaac-sim/IsaacLab/pull/3057

## 🔧 Improvements

### Core API

* Enhances Pink IK controller with null-space posture control and improv… by @michaellin6 in https://github.com/isaac-sim/IsaacLab/pull/3149
* Adds periodic logging when checking USD path on Nucleus server by @matthewtrepte in https://github.com/isaac-sim/IsaacLab/pull/3221
* Disallows string value written in sb3_ppo_cfg.yaml get evaluated in process_sb3_cfg by @ooctipus in https://github.com/isaac-sim/IsaacLab/pull/3110

### Infrastructure

* **Application Settings**
  * Disables rate limit for headless and headless rendering app by @matthewtrepte, @kellyguo11  in https://github.com/isaac-sim/IsaacLab/pull/3219, https://github.com/isaac-sim/IsaacLab/pull/3089
  * Disables `rtx.indirrectDiffuse.enabled`  in render preset balanced and performance modes by @matthewtrepte in https://github.com/isaac-sim/IsaacLab/pull/3240
  * Sets profiler backend to NVTX by default by @soowanpNV, @rwiltz in https://github.com/isaac-sim/IsaacLab/pull/3238, https://github.com/isaac-sim/IsaacLab/pull/3255
* **Dependencies**
  * Adds hf-xet license by @hhansen-bdai in https://github.com/isaac-sim/IsaacLab/pull/3116
  * Fixes new typing-inspection dependency license by @kellyguo11 in https://g...
- Compare 摘要: v2.2.0 -> v2.2.1
  - commits: 46
  - files changed: 191
  - additions: 8245
  - deletions: 1064
  - top directories: .github, CITATION.cff, CONTRIBUTORS.md, README.md, VERSION, apps
  - representative files:
    - source/isaaclab/isaaclab/envs/mdp/events.py (modified, +490/-307)
    - docs/source/_static/policy_deployment/01_io_descriptors/isaac_velocity_flat_g1_v0_IO_descriptors.yaml (added, +724/-0)
    - source/isaaclab/test/controllers/test_pink_ik.py (modified, +305/-151)
    - source/isaaclab/isaaclab/envs/utils/io_descriptors.py (added, +372/-0)
    - docs/source/_static/policy_deployment/01_io_descriptors/isaac_velocity_flat_anymal_d_v0_IO_descriptors.yaml (added, +349/-0)
    - source/isaaclab/test/controllers/test_null_space_posture_task.py (added, +339/-0)
    - docs/source/policy_deployment/01_io_descriptors/io_descriptors_101.rst (added, +281/-0)
    - source/isaaclab_tasks/isaaclab_tasks/manager_based/locomotion/velocity/mdp/symmetry/anymal.py (added, +271/-0)

### v2.2.0
- 标题: v2.2.0
- 类型: 正式版
- 发布时间: 2025-08-08 03:42:33 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v2.2.0
- GitHub release body:
## 👀 Overview

**Isaac Lab 2.2** brings major upgrades across simulation capabilities, tooling, and developer experience. It expands support for advanced physics features, new environments, and improved testing and documentation workflows. This release includes full compatibility with **Isaac Sim 5.0** as well as backwards compatibility with **Isaac Sim 4.5**.

Key highlights of this release include:

- **Enhanced Physics Support**: Updated [joint friction modeling using the latest PhysX APIs](https://nvidia-omniverse.github.io/PhysX/physx/5.6.1/docs/Articulations.html#articulation-joint-friction), added support for [spatial tendons](https://nvidia-omniverse.github.io/PhysX/physx/5.6.1/docs/Articulations.html#spatial-tendons), and improved surface gripper interactions.
- **New Environments for Imitation Learning**: Introduction of two new GR1 mimic environments, with domain randomization and visual robustness evaluation, and improved pick-and-place tasks.
- **New Contact-Rich Manipulation Tasks**: Integration of [FORGE](https://noseworm.github.io/forge/) and [AutoMate](https://bingjietang718.github.io/automate/) tasks for learning fine-grained contact interactions in simulation.
- **Teleoperation Improvements**: Teleoperation tools have been enhanced with configurable parameters and CloudXR runtime updates, including head tracking and hand tracking.
- **Performance & Usability Improvements**: Includes support for Stage in Memory and Cloning in Fabric for faster scene creation, new OVD recorder for large-scene GPU-based animation recording, and FSD (Fabric Scene Delegate) for improved rendering speed.
- **Improved Documentation**: The documentation has been extended and updated to cover new features, resolve common issues, and streamline setup, including updates to te...
- 外链文档摘录:
  - https://nvidia-omniverse.github.io/PhysX/physx/5.6.1/docs/Articulations.html#articulation-joint-friction
    Articulations provide an alternative, often superior approach to simulating mechanisms over addingjointsto rigid bodies. Typically, we achieve higher simulation fidelity with articulations as they have zero joint error by design, and can handle larger mass ratios between the jointed bodies. PhysX simulates articulations in reduced-coordinates, where the configuration of the articulation is determined by its root-body pose and the joint angles instead of the world pose of each body involved.
    It is often possible to turn jointed rigid bodies into an articulation given that they do not contain unsupported joints, seeArticulation Jointsbelow, and making sure thatloopsare resolved appropriately.
    Fixed Tendonsthat can create constraints on joint angles, for example to enforce mirrored motion of two joints, or
    The robot arm is afixed-basearticulation: Its root or base is fixed to the world frame. The fixed-base property can be set with a flag on the articulationat creation. Setting this flag is advantageous over constraining the root link using aFixed Jointbecause the immoveable property of the root link is solved perfectly.
    While articulations natively only support tree-structures, it is possible to create loops in the articulation by adding rigid-bodyJointsbetween articulation links. For example, we could tie the ragdoll’s hands together by adding aDistance Jointbetween the two hand spheres.
    The articulation links also do not have individual sleep states or solver iteration counts because they are simulated as a unit in the articulation. Those properties are set on the articulation instead. For the same reason, the links do not support force thresholding.
    Otherwise, articulation links can be treated as rigid bodies; for example, they use the same mass and collision-shape setup API, or we can apply a spatial force to them, or we can query their world pose and velocity (querying is ok, setting is not). In particular, links are also compatible with rigid-bodyJointsthat can be used to close loops.
    Performance-wise, the simulation cost is generally proportional to the number of degrees of freedom, rather than the number of links (assuming few contacts that need resolving). Therefore, in common robotics applications, where most joints have 0-1 degrees of freedom, the simulation cost of reduced-coordinate articulations is often lower than using rigid-bodies with joints.
    Set the articulation to be fixed-base, if applicable, and any other optional configuration options (see the API doc of
    Then add links one by one, each time specifying a parent link (
    joint->setJointType(PxArticulationJointType::eREVOLUTE);// revolute joint that rotates about the z axis (eSWING2) of the joint framesjoint->setMotion(PxArticulationAxis::eSWING2,PxArticulationMotion::eLIMITED);PxArticulationLimitlimits;limits.low=-PxPiDivFour;// in rad for a rotational motionlimits.high=PxPiDivFour;joint->setLimitParams(PxArticulationAxis::eSWING2,limits);
    Note how the axis must be specified consistently for both setting the motion and limit. In addition to limits, you may add a joint drive (i.e. motor):
    PxArticulationDriveposDrive;posDrive.stiffness=driveStiffness;// the spring constant driving the joint to a target positionposDrive.damping=driveDamping;// the damping coefficient driving the joint to a target velocityposDrive.maxForce=actuatorLimit;// force limit for the driveposDrive.driveType=PxArticulationDriveType::eFORCE;// make the drive output be a force/torque (default)// apply and set targets (note again the consistent axis)joint->setDriveParams(PxArticulationAxis::eSWING2,posDrive);joint->setDriveVelocity(PxArticulationAxis::eSWING2,0.0f);joint->setDriveTarget(PxArticulationAxis::eSWING2,targetPosition);
    You may also set joint friction, armature, etc; see the API doc of
    for details. At creation, you can also addArticulation Tendons:
    Finally, add the articulation to the scene (seecaveatbelow about changing articulation topology after scene insertion):
    In order to allow for pre-computing and optimization of simulation data, it is not possible to make changes to an articulation that change its topology after the articulation has been added to the scene. Topological changes include:
    adding and removing links ortendons
    adding/removing tendon attachments or joints.
    If you need to make topology changes, simply remove and re-add the articulation to the scene:
    scene->removeArticulation(*articulation);// make topology changesscene->addArticulation(*articulation);
    The articulation state (i.e. pose and velocities) is preserved through the remove and re-add cycle, so you do not have to store and reapply the state. In case of link removal, the corresponding joint state is removed as well; the state of joints of new links may be set with
    . Note that any changes to the articulation topology, in particular changes affecting degrees-of-freedom, typically require recreating the articulation’sPxArticulationCacheand recomputinglow-level indices to the cache.
    - a f...
  - https://nvidia-omniverse.github.io/PhysX/physx/5.6.1/docs/Articulations.html#spatial-tendons
    Articulations provide an alternative, often superior approach to simulating mechanisms over addingjointsto rigid bodies. Typically, we achieve higher simulation fidelity with articulations as they have zero joint error by design, and can handle larger mass ratios between the jointed bodies. PhysX simulates articulations in reduced-coordinates, where the configuration of the articulation is determined by its root-body pose and the joint angles instead of the world pose of each body involved.
    It is often possible to turn jointed rigid bodies into an articulation given that they do not contain unsupported joints, seeArticulation Jointsbelow, and making sure thatloopsare resolved appropriately.
    Fixed Tendonsthat can create constraints on joint angles, for example to enforce mirrored motion of two joints, or
    The robot arm is afixed-basearticulation: Its root or base is fixed to the world frame. The fixed-base property can be set with a flag on the articulationat creation. Setting this flag is advantageous over constraining the root link using aFixed Jointbecause the immoveable property of the root link is solved perfectly.
    While articulations natively only support tree-structures, it is possible to create loops in the articulation by adding rigid-bodyJointsbetween articulation links. For example, we could tie the ragdoll’s hands together by adding aDistance Jointbetween the two hand spheres.
    The articulation links also do not have individual sleep states or solver iteration counts because they are simulated as a unit in the articulation. Those properties are set on the articulation instead. For the same reason, the links do not support force thresholding.
    Otherwise, articulation links can be treated as rigid bodies; for example, they use the same mass and collision-shape setup API, or we can apply a spatial force to them, or we can query their world pose and velocity (querying is ok, setting is not). In particular, links are also compatible with rigid-bodyJointsthat can be used to close loops.
    Performance-wise, the simulation cost is generally proportional to the number of degrees of freedom, rather than the number of links (assuming few contacts that need resolving). Therefore, in common robotics applications, where most joints have 0-1 degrees of freedom, the simulation cost of reduced-coordinate articulations is often lower than using rigid-bodies with joints.
    Set the articulation to be fixed-base, if applicable, and any other optional configuration options (see the API doc of
    Then add links one by one, each time specifying a parent link (
    joint->setJointType(PxArticulationJointType::eREVOLUTE);// revolute joint that rotates about the z axis (eSWING2) of the joint framesjoint->setMotion(PxArticulationAxis::eSWING2,PxArticulationMotion::eLIMITED);PxArticulationLimitlimits;limits.low=-PxPiDivFour;// in rad for a rotational motionlimits.high=PxPiDivFour;joint->setLimitParams(PxArticulationAxis::eSWING2,limits);
    Note how the axis must be specified consistently for both setting the motion and limit. In addition to limits, you may add a joint drive (i.e. motor):
    PxArticulationDriveposDrive;posDrive.stiffness=driveStiffness;// the spring constant driving the joint to a target positionposDrive.damping=driveDamping;// the damping coefficient driving the joint to a target velocityposDrive.maxForce=actuatorLimit;// force limit for the driveposDrive.driveType=PxArticulationDriveType::eFORCE;// make the drive output be a force/torque (default)// apply and set targets (note again the consistent axis)joint->setDriveParams(PxArticulationAxis::eSWING2,posDrive);joint->setDriveVelocity(PxArticulationAxis::eSWING2,0.0f);joint->setDriveTarget(PxArticulationAxis::eSWING2,targetPosition);
    You may also set joint friction, armature, etc; see the API doc of
    for details. At creation, you can also addArticulation Tendons:
    Finally, add the articulation to the scene (seecaveatbelow about changing articulation topology after scene insertion):
    In order to allow for pre-computing and optimization of simulation data, it is not possible to make changes to an articulation that change its topology after the articulation has been added to the scene. Topological changes include:
    adding and removing links ortendons
    adding/removing tendon attachments or joints.
    If you need to make topology changes, simply remove and re-add the articulation to the scene:
    scene->removeArticulation(*articulation);// make topology changesscene->addArticulation(*articulation);
    The articulation state (i.e. pose and velocities) is preserved through the remove and re-add cycle, so you do not have to store and reapply the state. In case of link removal, the corresponding joint state is removed as well; the state of joints of new links may be set with
    . Note that any changes to the articulation topology, in particular changes affecting degrees-of-freedom, typically require recreating the articulation’sPxArticulationCacheand recomputinglow-level indices to the cache.
    - a f...
- Compare 摘要: v2.1.1 -> v2.2.0
  - commits: 159
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 11867
  - deletions: 2439
  - top directories: .aws, .github, .pre-commit-config.yaml, CITATION.cff, CONTRIBUTORS.md, README.md
  - representative files:
    - scripts/tools/record_demos.py (modified, +306/-206)
    - source/isaaclab/test/devices/test_device_constructors.py (added, +461/-0)
    - source/isaaclab/isaaclab/assets/articulation/articulation.py (modified, +406/-47)
    - docs/source/overview/augmented_imitation.rst (added, +431/-0)
    - scripts/demos/pick_and_place.py (added, +412/-0)
    - source/isaaclab/isaaclab/assets/surface_gripper/surface_gripper.py (added, +393/-0)
    - docs/source/how-to/cloudxr_teleoperation.rst (modified, +302/-36)
    - scripts/imitation_learning/robomimic/robust_eval.py (added, +334/-0)

### v2.1.1
- 标题: v2.1.1
- 类型: 正式版
- 发布时间: 2025-07-30 20:59:44 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v2.1.1
- GitHub release body:
## 👀 Overview

This release has been in development over the past few months and includes a significant number of updates, enhancements, and new features across the entire codebase. Given the volume of changes, we've grouped them into relevant categories to improve readability. This version is compatible with [NVIDIA Isaac Sim 4.5](https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/download.html).

We appreciate the community’s patience and contributions in ensuring quality and stability throughout. We're aiming for more frequent patch releases moving forward to improve the developer experience.

**Note:** This minor release does not include a Docker image or pip package.

**Full Changelog**: https://github.com/isaac-sim/IsaacLab/compare/v2.1.0...v2.1.1

## ✨ New Features

* **Asset Interfaces**
  * Adds `position` argument to set external forces and torques at different locations on the rigid body by @AntoineRichard in https://github.com/isaac-sim/IsaacLab/pull/1680
  * Adds `body_incoming_joint_wrench_b` to ArticulationData field by @jtigue-bdai in https://github.com/isaac-sim/IsaacLab/pull/2128
  * Allows selecting articulation root prim explicitly by @lgulich in https://github.com/isaac-sim/IsaacLab/pull/2228
* **Sensor Interfaces**
  * Draws connection lines for FrameTransformer visualization by @Mayankm96 in https://github.com/isaac-sim/IsaacLab/pull/1754
  * Uses visualization marker for connecting lines inside FrameTransformer by @bikcrum in https://github.com/isaac-sim/IsaacLab/pull/2526
* **MDP Terms**
  * Adds `body_pose_w` and `body_projected_gravity_b` observations by @jtigue-bdai in https://github.com/isaac-sim/IsaacLab/pull/2212
  * Adds joint effort observation by @jtigue-bdai in https://github.com/isaac-sim/IsaacLab/pull/2211
  * Adds CoM...
- 外链文档摘录:
  - https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/download.html
    Omniverse Launcher, Nucleus Workstation, and Nucleus Cache will be deprecated and will no longer be available starting October 1, 2025.  Functionality may be reduced If these applications are used after this date.
    Isaac Sim 4.5.0 will be the last release on Omniverse Launcher. SeeLatest Releaseinstead.
    The Live Sync feature is deprecated in Isaac Sim 4.5.0.
    Using the latest version of Isaac Sim is recommended to receive the latest security patches and bug-fixes.
    Pack 1 of 3(33.5 GB)
    Pack 2 of 3(28.6 GB)
    Pack 3 of 3(24.1 GB)
    Pack 1 of 4(13.7 GB)
    Pack 2 of 4(18.2 GB)
    Pack 3 of 4(14.5 GB)
    Pack 4 of 4(22.6 GB)
  - https://isaac-sim.github.io/IsaacLab/main/source/api/lab/isaaclab.sim.html#isaaclab.sim.PhysxCfg.enable_stabilization
    Define and modify various schemas on USD prims
    Converters to obtain USD file from other file formats (such as URDF, OBJ, STL, FBX)
    Currently, only a subset of all possible schemas and prims in Omniverse are supported.
    Sub-module containing converters for converting various file types to USD.
    Utilities built around USD operations.
    Configuration for PhysX solver-related parameters.
    Configuration for Omniverse RTX Renderer.
    and the physics solver parameters (for more information, see
    adding and removing callbacks to different simulation events such as physics stepping, rendering, etc.
    adds additional functionalities such as setting up the simulation context with a configuration object,
    Since we only support thePyTorchbackend for simulation, the
    Standalone python script: In this mode, the user has full control over the simulation and
    Based on above, for most functions in this class there is an equivalent function that is suffixed
    functions are used in the standalone python script mode.
    Returns whether the simulation has any RTX-rendering related sensors.
    Change the current render mode of the simulation.
    : No rendering, where only 1 is updated at a lower rate.
    : Partial rendering, where only 1 and 2 are updated.
    : Full rendering, where everything (1, 2, 3) is updated.
    The parameter is set to True when instances of RTX-related sensors (cameras or LiDARs) are
    created using Isaac Lab’s sensor classes.
    True if the simulation has RTX sensors (such as USD Cameras or LiDARs).
    When fabric interface is enabled, USD read/write operations are disabled. Instead all applications
    that occurs during USD read/write operations.
    Major version: This is the year of the release (e.g. 2022).
    Minor version: This is the half-year of the release (e.g. 1 or 2).
    Patch version: This is the patch number of the release (e.g. 0).
    This function is deprecated and will be removed in the future.
    change the render mode.
    mode.(SimulationContext's _sphinx_paramlinks_isaaclab.sim.SimulationContext.set_render_mode.mode is changed to the new)
    ValueError– If the input mode is not supported.
    The prim path where the USD PhysicsScene is created.
    The gravity vector (in m/s^2).
    Enable/disable scene query support for collision shapes.
    The prim path where the USD PhysicsScene is created. Default is “/physicsScene”.
    "cuda:0"
    : Use GPU, where N is the device ID. For example, “cuda:0”.
    The physics simulation time-step (in seconds). Default is 0.0167 seconds.
    The number of physics simulation steps per rendering step. Default is 1.
    The gravity vector (in m/s^2). Default is (0.0, 0.0, -9.81).
    If set to (0.0, 0.0, 0.0), gravity is disabled.
    Enable/disable scene query support for collision shapes. Default is False.
    functionality will not be available. However, this provides some performance speed-up.
    When running the simulation, updates in the states in the scene is normally synchronized with USD.
    When using GPU simulation, it is required to enable Fabric to visualize updates in the renderer.
    Transform updates are propagated to the renderer through Fabric. If Fabric is disabled with GPU simulation,
    the renderer will not be able to render any updates in the simulation, although simulation will still be
    PhysX solver settings. Default is PhysxCfg().
