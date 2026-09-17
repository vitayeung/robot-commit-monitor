# isaac-sim/IsaacLab Release Roadmap Reference

- 仓库: `isaac-sim/IsaacLab`
- 对应主报告: `isaac-sim_IsaacLab_release_roadmap.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要
- 版本总数: 7
- 正式版数量: 4
- 预发布版数量: 3
- 外链文档覆盖版本数: 5
- compare 摘要覆盖版本数: 6
- 最新版本: v3.0.0-EA (2026-09-17 06:34:03 CST)
- 最早纳入统计版本: v2.3.0 (2025-10-29 05:38:54 CST)

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
- 2026-09-17 06:34:03 CST | v3.0.0-EA | 正式版
- 2026-07-02 12:21:18 CST | v3.0.0-beta2.patch1 | 预发布版
- 2026-06-17 10:16:55 CST | v3.0.0-beta2 | 预发布版
- 2026-03-17 14:38:37 CST | v3.0.0-beta | 预发布版
- 2026-02-03 02:54:35 CST | v2.3.2 | 正式版
- 2025-12-05 06:26:35 CST | v2.3.1 | 正式版
- 2025-10-29 05:38:54 CST | v2.3.0 | 正式版

## 证据附录

### v3.0.0-EA
- 标题: v3.0.0-EA
- 类型: 正式版
- 发布时间: 2026-09-17 06:34:03 CST
- 链接: https://github.com/isaac-sim/IsaacLab/releases/tag/v3.0.0-EA
- GitHub release body:
# Isaac Lab 3.0 Early Access

**Isaac Lab 3.0 Early Access is ready.**

Isaac Lab 3.0 establishes the foundation for the next generation of robot learning in Isaac Lab: one task API across multiple physics, rendering, and visualization backends; kit-less execution; Warp-native data paths; and unified workflows from installation through training, evaluation, and deployment.

This release is built for **Isaac Sim 6.1**, Python 3.12, PyTorch 2.11, NVIDIA Warp 1.16, and Newton 1.5.2.

> [!NOTE]
> **Early Access status**
>
> The architecture and feature set for Isaac Lab 3.0 are ready for users to build on. From Early Access to General Availability, the `release/3.0.0` branch will focus only on bug fixes, stability, compatibility, and documentation improvements. General Availability is targeted toward the end of October 2026.
>
> We encourage you to start migrating, training, and testing now—and to tell us what you find.

## Try Isaac Lab 3.0 today

Install [`uv`](https://docs.astral.sh/uv/), clone the Early Access branch, and launch a kit-less Newton workflow:

```bash
git clone --branch release/3.0.0 https://github.com/isaac-sim/IsaacLab.git
cd IsaacLab

uv run isaaclab train \
    --rl_library rsl_rl \
    --task Isaac-Cartpole \
    physics=newton_mjwarp \
    --viz newton_gl
```

For a fully kit-less PhysX and RTX rendering workflow, use OVPhysX and OVRTX backends. The `ov` extra installs both optional runtimes; Isaac Sim is not installed or launched:

```bash
uv run --extra ov isaaclab train \
    --rl_library rsl_rl \
    --task Isaac-Cartpole-Camera-Direct \
    physics=ovphysx \
    renderer=ovrtx \
    presets=rgb \
    --viz newton_gl
```

For the full Isaac Sim experience with Isaac Sim PhysX, Isaac Sim RTX rendering, Isaac Sim ROS bridge, and other Kit integr...
- 外链文档摘录:
  - https://docs.astral.sh/uv/
    An extremely fast Python package and project manager, written in Rust.
    - 10-100x fasterthan
    - Runs scripts, with support forinline dependency metadata.
    - Installs and managesPython versions.
    - Runs and installstools published as Python packages.
    - Includes apip-compatible interfacefor a performance boost with a familiar
    - Supports Cargo-styleworkspacesfor scalable projects.
    - Installable without Rust or Python via
    - Supports macOS, Linux, and Windows.
    PS>powershell-ExecutionPolicyByPass-c"irm https://astral.sh/uv/install.ps1 | iex"
    uv manages project dependencies and environments, with support for lockfiles, workspaces, and more,
    $uvinitexampleInitialized project `example` at `/home/user/example`$cdexample$uvaddruffCreating virtual environment at: .venvResolved 2 packages in 170msBuilt example @ file:///home/user/examplePrepared 2 packages in 627msInstalled 2 packages in 1ms+ example==0.1.0 (from file:///home/user/example)+ ruff==0.5.4$uvrunruffcheckAll checks passed!$uvlockResolved 2 packages in 0.33ms$uvsyncResolved 2 packages in 0.70msChecked 1 package in 0.02ms
    uv also supports building and publishing projects, even if they're not managed with uv. See thepackaging guideto learn more.
    Create a new script and add inline metadata declaring its dependencies:
    $echo'import requests; print(requests.get("https://astral.sh"))'>example.py$uvadd--scriptexample.pyrequestsUpdated `example.py`
    $uvrunexample.pyReading inline script metadata from: example.pyInstalled 5 packages in 12ms<Response [200]>
    uv executes and installs command-line tools provided by Python packages, similar to
    $uvxpycowsay'hello world!'Resolved 1 package in 167msInstalled 1 package in 9ms+ pycowsay==0.0.0.2"""------------< hello world! >------------\   ^__^\  (oo)\_______(__)\       )\/\||----w |||     ||
    $uvtoolinstallruffResolved 1 package in 6msInstalled 1 package in 2ms+ ruff==0.5.4Installed 1 executable: ruff$ruff--versionruff 0.5.4
    uv installs Python and allows quickly switching between versions.
    Install multiple Python versions:
    Download Python versions as needed:
    Use a specific Python version in the current directory:
    $uvpythonpin3.11Pinned `.python-version` to `3.11`
    See theinstalling Python guideto get started.
    platform-independent resolutions, reproducible resolutions, alternative resolution strategies, and
    Migrate to uv without changing your existing workflows — and experience a 10-100x speedup — with the
    Compile requirements into a platform-independent requirements file:
    $uvpipcompilerequirements.in\--universal\--output-filerequirements.txtResolved 43 packages in 12ms
    $uvvenvUsing CPython 3.12.3Creating virtual environment at: .venvActivate with: source .venv/bin/activate
    $uvpipsyncrequirements.txtResolved 43 packages in 11msInstalled 43 packages in 208ms+ babel==2.15.0+ black==24.4.2+ certifi==2024.7.4...
  - https://isaac-sim.github.io/IsaacLab/release/3.0.0/source/setup/installation/index.html
    Python environment with Isaac Sim
    Isaac Lab Python package
    Download Isaac Sim and use the Python interpreter included with it.
    Provision a remote GPU workstation on a supported cloud provider.
    Full Isaac Sim workflows require Python 3.12 on Ubuntu 22.04+ or Windows 11. Use a recent NVIDIA
    production driver and a workstation with at least 32 GB RAM and 16 GB GPU VRAM. Rendering can
    require additional VRAM. Confirm your machine against theIsaac Sim system requirementsandOmniverse technical requirements.
    Isaac Sim 5.1 and older are not supported. Use Isaac Sim 6.1 with Python 3.12.
    Linux x86_64 and aarch64,
    Linux aarch64 and DGX Spark requirements
    DGX Spark requires CUDA 13 or newer and the corresponding PyTorch build. Install the build
    sudoaptinstallpython3.12-devlibgl1-mesa-devlibx11-devlibxcursor-dev\libxi-devlibxinerama-devlibxrandr-dev
    SkillGen, XR teleoperation, livestream, Hub Workstation Cache, Cosmos Transfer1, and RLinf are
    not currently supported or validated on DGX Spark. SkillGen depends on native CUDA/C++
    # Newton backend without Isaac Simuvrunisaaclabtrain--rl_libraryrsl_rl\--taskIsaac-Cartpole-Directphysics=newton_mjwarp# OV PhysX backenduvrun--extraovphysxisaaclabtrain--rl_libraryrsl_rl\--taskIsaac-Cartpole-Directphysics=ovphysx# Full Isaac Sim supportuvrun--extraisaacsimisaaclabtrain--rl_libraryrsl_rl\--taskIsaac-Cartpole-Directphysics=isaacsim_physx# Play a policyuvrunisaaclabplay--rl_libraryrsl_rl--taskIsaac-Cartpole-Direct--viznewton
    Linux aarch64 (DGX Spark)
    # Newton backenduvrunisaaclabtrain--rl_libraryrsl_rl\--taskIsaac-Cartpole-Directphysics=newton_mjwarp# OV PhysX backenduvrun--extraovphysxisaaclabtrain--rl_libraryrsl_rl\--taskIsaac-Cartpole-Directphysics=ovphysx# Full Isaac Sim supportuvrun--extraisaacsimisaaclabtrain--rl_libraryrsl_rl\--taskIsaac-Cartpole-Directphysics=isaacsim_physx# Play a policyuvrunisaaclabplay--rl_libraryrsl_rl--taskIsaac-Cartpole-Direct--viznewton
    For direct Python commands that import Isaac Sim on aarch64, prefix the
    Enable Windows long-path support before cloning. In an elevated PowerShell window, run:
    powershell -ExecutionPolicy ByPass -c"irm https://astral.sh/uv/install.ps1 | iex"
    :: Newton backend without Isaac Simuv run isaaclab train --rl_library rsl_rl^--task Isaac-Cartpole-Direct physics=newton_mjwarp:: OV PhysX backenduv run --extra ovphysx isaaclab train --rl_library rsl_rl^--task Isaac-Cartpole-Direct physics=ovphysx:: Full Isaac Sim supportuv run --extra isaacsim isaaclab train --rl_library rsl_rl^--task Isaac-Cartpole-Direct physics=isaacsim_physx:: Play a policyuv run isaaclab play --rl_library rsl_rl --task Isaac-Cartpole-Direct --viz newton
    Kit-less installation uses a Python 3.12 environment and does not install Isaac Sim. Clone Isaac
    uvvenv--python3.12--seedenv_isaaclabsourceenv_isaaclab/bin/activate
    uv venv --python 3.12 --seed env_isaaclab
    condacreate-nenv_isaaclabpython=3.12
    conda create -n env_isaaclab python=3.12
    python -m pip install --upgrade pip
    Teleoperation tools (Linux x86_64).
    OV runtime wheels. Select
    Python environment with Isaac Sim#
    Use this path when you want an editable Isaac Lab checkout with full Isaac Sim support and a
    Python environment you manage yourself. Create and activate the environment before installing
    Isaac Sim or Isaac Lab. Isaac Sim’s pip packages require GLIBC 2.35 or newer on Linux. EnableWindows long-path supportbefore installing on Windows.
    Create and activate a Python 3.12 environment:
    Install Isaac Sim and the CUDA-enabled PyTorch build for your platform:
    On aarch64 systems such as DGX Spark, install the required development packages before
    sudoaptinstallpython3.12-devlibgl1-mesa-devlibx11-devlibxcursor-devlibxi-dev\libxinerama-devlibxrandr-dev
    exportLD_PRELOAD=$(python-c"import sys,os;[print(os.path.join(p,'omni','client','libcarb.so')) for p in sys.path if os.path.isfile(os.path.join(p,'omni','client','libcarb.so'))]"2>/dev/null|head-1)${LD_PRELOAD:+:$LD_PRELOAD}
    isaaclab.bat -p scripts\tutorials\00_sim\create_empty.py --viz kit
    Isaac Lab Python package#
    Use this path when Isaac Lab is a dependency of an external Python project. The released
    Isaac Lab wheels are published for major releases, not every patch release.
    package; add optional capabilities only when your project needs them.
    uvinit--python3.12my_isaaclab_projectcdmy_isaaclab_project
    uvvenv--python3.12env_isaaclabsourceenv_isaaclab/bin/activate
    uv venv --python 3.12 env_isaaclab
    Add extras only when your project needs them. Most extras work with
    Isaac Lab Mimic / XR teleoperation. The wheel’s
- Compare 摘要: v3.0.0-beta2.patch1 -> v3.0.0-EA
  - commits: 1041
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 14501
  - deletions: 1970
  - top directories: .agents, .claude, .dockerignore, .gitattributes, .github, .gitignore
  - representative files:
    - .github/workflows/build.yaml (modified, +562/-248)
    - .github/workflows/license-exceptions.json (modified, +698/-17)
    - .github/actions/run-tests/run_tests.sh (added, +556/-0)
    - .github/workflows/license-check.yaml (modified, +487/-32)
    - .github/actions/run-tests/action.yml (modified, +153/-311)
    - .github/scripts/resolve_backport_conflicts.py (added, +425/-0)
    - .github/workflows/backport-release-3.0.yml (added, +387/-0)
    - docs/_extensions/isaaclab_docs.py (added, +360/-0)

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
    - Fork3.9k
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
    🎉29ZzzzzzS, qianl-nv, rthaker01, sheikh-nv, evanzijianhe, johnsutor, IvolgaDmitriy, seawee1, diegoferigo-rai, momo-van, and 19 more reacted with hooray emoji
    - 🎉29 reactions
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
    Migrating To 3.0 — Isaac Lab Documentation
    Choose the path that matches the code you are starting from. The Isaac Lab 2.x path is organized in
    the order most projects should migrate: install the new release, configure a backend, update task APIs,
    Migration from Isaac Lab 2.x to 3.0– update an existing
    Isaac Lab project for the new installation, APIs, and multi-backend architecture.
    Migration from Isaac Gym and IsaacGymEnvs– port an Isaac Gym
    Migration of deformables– move from the old soft-body API to
    Migration from Isaac Lab 2.x to 3.0
    Isaac Lab 3.0 separates backend-specific simulation code from the core API and introduces unified
    When you change it, update the skill so agent guidance stays in sync. SeeAgent Skills.
    Start from a fresh Isaac Lab 3.0 checkout and Python 3.12 environment instead of upgrading the
    packages inside an existing 2.x environment. The recommended workflow now uses
    condacreate-nenv_isaaclabpython=3.11
    for full Isaac Sim support. SeeAutomatic setup with uv (recommended)for platform-specific
    use a preset when an environment supports multiple backends.
    Isaac Lab 3.0 introduces afactory-based multi-backend architecturethat allows asset classes
    fromisaaclab.assetsimportArticulation,ArticulationCfg# The factory pattern creates the appropriate backend implementation.# No import changes are needed — the same isaaclab imports work regardless of backend.robot=Articulation(cfg=ArticulationCfg(...))
    seeBackend Architecture. To add a new backend, seeAdd a Physics Backend.
    ``isaaclab_physx``— PhysX-specific implementations of asset and sensor classes.
    ``isaaclab_newton``— Newton-specific implementations of supported asset classes, including
    Deformable object public APIs remain in the backend-neutral
    extension is installed automatically with Isaac Lab. No additional
    The following sensor classes also remain in the
    package with unchanged imports:
    These sensor classes now use factory patterns that automatically instantiate the appropriate backend
    sensor in Isaac Lab 3.0 isnotthe same as the
    sensor in 2.x.
    (full state sensor) has been renamed to
    is a lightweight sensor that only provides angular velocity
    and linear acceleration. SeeIMU Sensor Renamed to PVA; New Lightweight IMU Sensorbelow for details.
    If you need to import the PhysX sensor implementations directly (e.g., for type hints or subclassing),
    # Direct PhysX implementation importsfromisaaclab_physx.sensorsimportContactSensor,ContactSensorDatafromisaaclab_physx.sensorsimportImu,ImuDatafromisaaclab_physx.sensorsimportPva,PvaDatafromisaaclab_physx.sensorsimportFrameTransformer,FrameTransformerDatafromisaaclab_physx.sensorsimportJointWrenchSensor,JointWrenchSensorData
    ensuring a consistent API across backends. They use the same warp-based data conventions
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
    - Fork3.9k
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
