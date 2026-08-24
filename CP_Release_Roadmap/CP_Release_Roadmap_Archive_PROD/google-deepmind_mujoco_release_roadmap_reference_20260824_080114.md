# google-deepmind/mujoco Release Roadmap Reference

- 仓库: `google-deepmind/mujoco`
- 对应主报告: `google-deepmind_mujoco_release_roadmap.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要
- 版本总数: 12
- 正式版数量: 12
- 预发布版数量: 0
- 外链文档覆盖版本数: 11
- compare 摘要覆盖版本数: 11
- 最新版本: 3.11.0 (2026-07-28 09:17:52 CST)
- 最早纳入统计版本: 3.3.5 (2025-08-09 07:02:07 CST)

## 分析策略决策
- 请求模式: `auto`
- 最终策略: `L1: Release-first`
- 证据充分性评分: 2/6
- 触发规则: migration_risk_high, ecosystem_in_repo
- 决策说明:
  - MuJoCo 当前优先问题是窗口过滤与反推测质量控制，不默认用源码增强解决。
  - 证据充分性评分 2/6，触发规则: migration_risk_high, ecosystem_in_repo。
  - 因此主脚本保持 L1，避免在主流程里默认引入额外源码分析成本。

## Release 时间线
- 2026-07-28 09:17:52 CST | 3.11.0 | 正式版
- 2026-06-23 01:04:32 CST | 3.10.0 | 正式版
- 2026-05-27 22:46:14 CST | 3.9.0 | 正式版
- 2026-05-11 21:59:30 CST | 3.8.1 | 正式版
- 2026-04-25 07:03:38 CST | 3.8.0 | 正式版
- 2026-04-14 21:03:47 CST | 3.7.0 | 正式版
- 2026-03-11 09:53:34 CST | 3.6.0 | 正式版
- 2026-02-13 09:20:28 CST | 3.5.0 | 正式版
- 2025-12-06 07:17:44 CST | 3.4.0 | 正式版
- 2025-10-15 01:38:32 CST | 3.3.7 | 正式版
- 2025-09-16 22:28:40 CST | 3.3.6 | 正式版
- 2025-08-09 07:02:07 CST | 3.3.5 | 正式版

## 证据附录

### 3.11.0
- 标题: 3.11.0
- 类型: 正式版
- 发布时间: 2026-07-28 09:17:52 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.11.0
- GitHub release body:
# Version 3.11.0 (July 27, 2026)

## Engine

1. [4787c809](https://github.com/google-deepmind/mujoco/commit/4787c809) Added [geom/surfacevel](https://mujoco.readthedocs.io/en/stable/XMLreference.html#body-geom-surfacevel): the velocity of a geom's surface as seen by contacts, given as a velocity field with a constant component and a rotational component about the geom frame origin. This allows conveyor belts, treadmills and turntables to be modeled with static geoms and no degrees of freedom: friction drives touching bodies along the motion of the surface, with the field projected onto each contact's tangent plane. Surface velocities compose correctly with each other and with body motion. Note that the contact rows of `mjData.efc_vel`, and the constraint-state sensors that read them, report the velocity relative to the moving surface rather than to the geom, since that is the quantity the constraint acts on; for geoms without `surfacevel` the two are identical. Contact-point visualization draws an arrow along the surface velocity at contacts with moving surfaces.

   [![Watch video](https://img.youtube.com/vi/PdSdrqhSiZA/mqdefault.jpg)](https://youtu.be/PdSdrqhSiZA)

2. [a264d0bc](https://github.com/google-deepmind/mujoco/commit/a264d0bc) Added [geom/adhesion](https://mujoco.readthedocs.io/en/stable/XMLreference.html#body-geom-adhesion) and [pair/adhesion](https://mujoco.readthedocs.io/en/stable/XMLreference.html#contact-pair-adhesion): an adhesive force associated with a contact, useful for modeling sticky materials. Contacts can pull with up to the given force before breaking, and the friction budget becomes $\mu(f_N + \text{adhesion})$. Combined with [gap](https://mujoco.readthedocs.io/en/stable/XMLreference.html#body-geom-gap), adhesive contacts apply "adhesion a...
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/stable/XMLreference.html#body-geom-surfacevel
    XML Reference - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    This chapter is the reference manual for the MJCF modeling language used in MuJoCo.
    The dropdown below summarizes the XML elements and their attributes in MJCF. All information in MJCF is entered through
    An array of N integers. If N is omitted it equals 1.
    An array of N real-valued numbers. If N is omitted it equals 1.
    In addition to having a data type, attributes can be required or optional. Optional attributes can have internal
    This state is different from any valid setting that can be entered in the XML. This mechanism enables the compiler to
    appropriate action. Some attributes have internal defaults (usually 0) which are not actually allowed by the
    compiler. When such attributes become relevant in a given context, they must be set to allowed values.
    In the remainder of this chapter we describe all valid MJCF elements and their attributes. Some elements can be used in
    prefix in the documentation below.
    These elements are not strictly part of the low-level MJCF format definition, but rather instruct the compiler to
    saving the XML. There are currently six meta-elements in MJCF:
    schema, but serve to procedurally generate other MJCF elements.
    <mujoco><worldbody><framequat="0 0 1 0"><geomname="Alice"quat="0 1 0 0"size="1"/></frame><framepos="0 1 0"><geomname="Bob"pos="0 1 0"size="1"/><bodyname="Carl"pos="1 0 0">...</body></frame></worldbody></mujoco>
    <mujoco><worldbody><geomname="Alice"quat="0 0 0 1"size="1"/><geomname="Bob"pos="0 2 0"size="1"/><bodyname="Carl"pos="1 1 0">...</body></worldbody></mujoco>
    offsets, adding namespace suffixes to avoid name collisions. Appended suffix strings are integers in the
    replicating 200 times, suffixes will be
    The namespace separator. This optional string is prepended to the namespace suffix string. Note that for nested
    replicate elements, the innermost namespace suffixes are appended first.
    <mujoco><worldbody><replicatecount="2"offset="0 1 0"euler="90 0 0"><replicatecount="2"sep="-"offset="1 0 0"euler="0 90 0"><geomname="Alice"size=".1"/></replicate></replicate></worldbody><sensor><accelerometername="Bob"site="Alice"/></sensor></mujoco>
    <mujoco><worldbody><geomname="Alice-00"size="0.1"/><geomname="Alice-10"size="0.1"pos="1 0 0"quat="1 0 1 0"/><geomname="Alice-01"size="0.1"pos="0 1 0"quat="1 1 0 0"/><geomname="Alice-11"size="0.1"pos="1 1 0"quat="0.5 0.5 0.5 0.5"/></worldbody><sensor><accelerometername="Bob-00"site="Alice-00"/><accelerometername="Bob-10"site="Alice-10"/><accelerometername="Bob-01"site="Alice-01"/><accelerometername="Bob-11"site="Alice-11"/></sensor></mujoco>
    This element does not strictly belong to MJCF. Instead it is a meta-element, used to assemble multiple XML
    files in a single document object model (DOM) before parsing. The included file must be a valid XML file with a unique
    top-level element. This top-level element is removed by the parser, and the elements below it are inserted at the
    location of theincludeelement. At least one element must be inserted as a result of this procedure. Theincludeelement can be used wherever an XML element is expected in the MJCF file. Nested includes are allowed,
    however a given XML file can be included at most once in the entire model. After all the included XML files have been
    assembled into a single DOM, it must correspond to a valid MJCF model. Other than that, it is up to the user to decide
    The name of the XML file to be included. The file location is relative to the directory of the main MJCF file. If the
    file is not in the same directory, it should be prefixed with a relative path.
    The unique top-level element, identifying the XML file as an MJCF model file.
    adjust it properly through the XML.
    Simulation time step in seconds. This is the single most important parameter affecting the speed-accuracy trade-off
    real-time performance, the time step must be larger than the CPU time per step (or 4 times larger when using the RK4
    by the time step but also by theSolver parameters; in particular softer constraints can be simulated with larger time
    attribute. Settings larger than 1 cause friction forces to be “harder” than normal forces, having the general effect
    gravity:real(3), “0 0 -9.81”
    wind:real(3), “0 0 0”
    Velocity vector of the medium (i.e., wind). This vector is subtracted from the 3D translational velocity of each
    magnetic:real(3), “0 -0.5 0”
    Global magnetic flux. This vector is used by magnetometer sensors, which are defined as sites and return the magnetic
  - https://mujoco.readthedocs.io/en/stable/XMLreference.html#body-geom-adhesion
    XML Reference - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    This chapter is the reference manual for the MJCF modeling language used in MuJoCo.
    The dropdown below summarizes the XML elements and their attributes in MJCF. All information in MJCF is entered through
    An array of N integers. If N is omitted it equals 1.
    An array of N real-valued numbers. If N is omitted it equals 1.
    In addition to having a data type, attributes can be required or optional. Optional attributes can have internal
    This state is different from any valid setting that can be entered in the XML. This mechanism enables the compiler to
    appropriate action. Some attributes have internal defaults (usually 0) which are not actually allowed by the
    compiler. When such attributes become relevant in a given context, they must be set to allowed values.
    In the remainder of this chapter we describe all valid MJCF elements and their attributes. Some elements can be used in
    prefix in the documentation below.
    These elements are not strictly part of the low-level MJCF format definition, but rather instruct the compiler to
    saving the XML. There are currently six meta-elements in MJCF:
    schema, but serve to procedurally generate other MJCF elements.
    <mujoco><worldbody><framequat="0 0 1 0"><geomname="Alice"quat="0 1 0 0"size="1"/></frame><framepos="0 1 0"><geomname="Bob"pos="0 1 0"size="1"/><bodyname="Carl"pos="1 0 0">...</body></frame></worldbody></mujoco>
    <mujoco><worldbody><geomname="Alice"quat="0 0 0 1"size="1"/><geomname="Bob"pos="0 2 0"size="1"/><bodyname="Carl"pos="1 1 0">...</body></worldbody></mujoco>
    offsets, adding namespace suffixes to avoid name collisions. Appended suffix strings are integers in the
    replicating 200 times, suffixes will be
    The namespace separator. This optional string is prepended to the namespace suffix string. Note that for nested
    replicate elements, the innermost namespace suffixes are appended first.
    <mujoco><worldbody><replicatecount="2"offset="0 1 0"euler="90 0 0"><replicatecount="2"sep="-"offset="1 0 0"euler="0 90 0"><geomname="Alice"size=".1"/></replicate></replicate></worldbody><sensor><accelerometername="Bob"site="Alice"/></sensor></mujoco>
    <mujoco><worldbody><geomname="Alice-00"size="0.1"/><geomname="Alice-10"size="0.1"pos="1 0 0"quat="1 0 1 0"/><geomname="Alice-01"size="0.1"pos="0 1 0"quat="1 1 0 0"/><geomname="Alice-11"size="0.1"pos="1 1 0"quat="0.5 0.5 0.5 0.5"/></worldbody><sensor><accelerometername="Bob-00"site="Alice-00"/><accelerometername="Bob-10"site="Alice-10"/><accelerometername="Bob-01"site="Alice-01"/><accelerometername="Bob-11"site="Alice-11"/></sensor></mujoco>
    This element does not strictly belong to MJCF. Instead it is a meta-element, used to assemble multiple XML
    files in a single document object model (DOM) before parsing. The included file must be a valid XML file with a unique
    top-level element. This top-level element is removed by the parser, and the elements below it are inserted at the
    location of theincludeelement. At least one element must be inserted as a result of this procedure. Theincludeelement can be used wherever an XML element is expected in the MJCF file. Nested includes are allowed,
    however a given XML file can be included at most once in the entire model. After all the included XML files have been
    assembled into a single DOM, it must correspond to a valid MJCF model. Other than that, it is up to the user to decide
    The name of the XML file to be included. The file location is relative to the directory of the main MJCF file. If the
    file is not in the same directory, it should be prefixed with a relative path.
    The unique top-level element, identifying the XML file as an MJCF model file.
    adjust it properly through the XML.
    Simulation time step in seconds. This is the single most important parameter affecting the speed-accuracy trade-off
    real-time performance, the time step must be larger than the CPU time per step (or 4 times larger when using the RK4
    by the time step but also by theSolver parameters; in particular softer constraints can be simulated with larger time
    attribute. Settings larger than 1 cause friction forces to be “harder” than normal forces, having the general effect
    gravity:real(3), “0 0 -9.81”
    wind:real(3), “0 0 0”
    Velocity vector of the medium (i.e., wind). This vector is subtracted from the 3D translational velocity of each
    magnetic:real(3), “0 -0.5 0”
    Global magnetic flux. This vector is used by magnetometer sensors, which are defined as sites and return the magnetic
- Compare 摘要: 3.10.0 -> 3.11.0
  - commits: 226
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 19635
  - deletions: 9806
  - top directories: .github, .pre-commit-config.yaml, CMakeLists.txt, CONTRIBUTING.md, cmake, dist
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/constraint.py (modified, +4442/-1911)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_flex.py (modified, +3429/-560)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/solver.py (modified, +1041/-2403)
    - doc/changelog.rst (modified, +1461/-1151)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/io.py (modified, +906/-261)
    - doc/includes/references.h (modified, +526/-303)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/derivative.py (modified, +629/-112)
    - doc/APIreference/functions.rst (modified, +581/-4)

### 3.10.0
- 标题: 3.10.0
- 类型: 正式版
- 发布时间: 2026-06-23 01:04:32 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.10.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.10.0/changelog.html)
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.10.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.10.0 (June 22, 2026)#
    Addedmju_threadpool, a new function for creating a thread pool on an
    Added a unifiedlogging API:
    The legacy callbacksmju_user_errorandmju_user_warningare deprecated but remain functional.
    Addedmjs_numWarningsandmjs_getWarningfor retrieving all warnings accumulated during model
    compilation and attachment. Deprecatedmjs_isWarningin favor of
    Added thecompiler/conflictattribute for controlling how conflicting global attributes
    Future breaking API changes
    However, the default policy will change to “merge” in a future release.
    Improved primal solver convergence under float32. Improvements initially proposed by@n3binissue #2313and@adenzler-nvidiainMJWarppull request1374.
    TheCG solvernow uses the Hager-Zhang conjugate direction update instead of the
    Polak-Ribiere-Plus formula. This improves convergence and leads to a significant speedup under float32.
    Addedmjs_makeFlex, a new C API function equivalent to theflexcompelement for
    Added support for loading 1D flex components from OBJ line segments
    Significantly improved the quality of coarse convex hulls produced by themaxhullvertattribute by invoking Qhull’sQ9option.
    was removed along with the old engine threading API.
    Migration:Usemju_threadpoolto set number of worker threads for the engine.
    were removed from the arena and are now
    Changed the signature ofmj_fullMfrom
    Migration:For inertia matrix conversion, replace
    Fixed a vulnerability in the System Identification toolbox where loading a trajectory or time series called
    Fixed a bug in the
    Fixed a bug where the mesh compiler would produce non-unit convex hull polygon normals.
    Version 3.9.0 (May 27, 2026)#
    , the whitened constraint Jacobian\(Y = J M^{-1/2}\), allocated in the arena when
    dual solvers (PGS or NoSlip) are used or whendiagexactis enabled.
    Added thediagexactenable flag, which computes the exact diagonal of the
    constraint-space inertia matrix at the current configuration, replacing the default compile-time approximation.
    This improves solver quality for models with anisotropic inertias or complex kinematic coupling. SeeExact diagonalfor details.
    Added compiler timing diagnostics via the newmjtCTimerenum and themjs_getTimerC API. Aftermj_compile, per-category timings (total, assets, mesh loading, convex hull, normals, inertia, BVH, octree,
    . Thecompilesample prints a detailed timing
    AddedmjtBoolto represent boolean variables, replacingmjtByteacross all boolean fields inmjModel,mjData, and public C API function signatures.
    efc_address=-1
    , the behavior is unchanged.
    Migration:Models that use the default
    (the vast majority) require no changes. For models with
    should be changed to
    Thetactilesensor now reports raw depth instead of an estimated pressure.
    MJX: Removed the deprecated
    Maybe-breaking: Addedmjassert.h, a new header containing
- Compare 摘要: 3.9.0 -> 3.10.0
  - commits: 217
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 14006
  - deletions: 3253
  - top directories: .github, CMakeLists.txt, cmake, dist, doc/APIreference, doc/XMLreference.rst
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/solver.py (modified, +2983/-1028)
    - mjx/mujoco/mjx/warp/forward.py (modified, +868/-289)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/sleep.py (added, +1032/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/render.py (modified, +523/-448)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/history.py (added, +925/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/island.py (modified, +825/-19)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/io.py (modified, +494/-112)
    - include/mujoco/mjspecmacro.h (added, +604/-0)

### 3.9.0
- 标题: 3.9.0
- 类型: 正式版
- 发布时间: 2026-05-27 22:46:14 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.9.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.9.0/changelog.html)
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.9.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.9.0 (May 27, 2026)#
    , the whitened constraint Jacobian\(Y = J M^{-1/2}\), allocated in the arena when
    dual solvers (PGS or NoSlip) are used or whendiagexactis enabled.
    Added thediagexactenable flag, which computes the exact diagonal of the
    constraint-space inertia matrix at the current configuration, replacing the default compile-time approximation.
    This improves solver quality for models with anisotropic inertias or complex kinematic coupling. SeeExact diagonalfor details.
    Added compiler timing diagnostics via the newmjtCTimerenum and themjs_getTimerC API. Aftermj_compile, per-category timings (total, assets, mesh loading, convex hull, normals, inertia, BVH, octree,
    . Thecompilesample prints a detailed timing
    AddedmjtBoolto represent boolean variables, replacingmjtByteacross all boolean fields inmjModel,mjData, and public C API function signatures.
    efc_address=-1
    , the behavior is unchanged.
    Migration:Models that use the default
    (the vast majority) require no changes. For models with
    should be changed to
    Thetactilesensor now reports raw depth instead of an estimated pressure.
    MJX: Removed the deprecated
    Maybe-breaking: Addedmjassert.h, a new header containing
    compile-time assertions that verify the sizes of MuJoCo’s public types for ABI stability. This is a first step
    with strongly-typed enums in the public API. If these assertions fail on your compiler or
    platform, please report the issue on GitHub.
    Version 3.8.1 (May 11, 2026)#
    Added island support for thePGS solver.
    ThePGS solvernow iterates over constraints in pseudo-random order, improving performance by
    Added support forelastic2dfor trilinear and quadratic flexdofs.
    Addedmjs_getOriginSpec, returning the spec that originally defined an element, prior to attachment. This is
    Addedmju_sym2dense, converting a lower-triangular, implicitly symmetric CSR matrix to a dense symmetric
    Future breaking API changes
    The introduction ofmju_sym2denseis a step towards the removal of the legacy-format
    . This removal will involve a future breaking change tomj_fullM(which
    Fixed default for multiccd inmjcPhysics.
    Python binding to interact with the Virtual File System directly from Python.
    removed in an upcoming release. You cannot specify both the
    Version 3.8.0 (April 24, 2026)#
    Added support for Python 3.14.
    Addedmulti-cell supportfor trilinear and quadratic flexes. Note that the implicit
    integrator uses a dense solver for the flex degrees of freedom, which can be slow for multi-cell flexes.
    Added newmj_maxContactfunction to get the maximum number of possible contacts returned by
    is now enabled by default. The new implementation (as opposed to the legacy pipeline) has little performance
    overhead and improves stability.
    Version 3.7.0 (April 14, 2026)#
- Compare 摘要: 3.8.1 -> 3.9.0
  - commits: 85
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 9546
  - deletions: 5087
  - top directories: .github, .readthedocs.yml, CMakeLists.txt, cmake, dist, doc/APIreference
  - representative files:
    - doc/includes/references.h (modified, +848/-820)
    - doc/images/modeling/margin_gap_dark.svg (added, +782/-0)
    - doc/images/modeling/margin_gap_light.svg (added, +781/-0)
    - src/engine/engine_collision_driver.c (modified, +396/-212)
    - include/mujoco/mjtype.h (added, +579/-0)
    - include/mujoco/mjmodel.h (modified, +25/-455)
    - src/engine/engine_core_constraint.c (modified, +274/-187)
    - src/xml/mjz/mjz_encoder.cc (added, +421/-0)

### 3.8.1
- 标题: 3.8.1
- 类型: 正式版
- 发布时间: 2026-05-11 21:59:30 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.8.1
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.8.1/changelog.html)
- Compare 摘要: 3.8.0 -> 3.8.1
  - commits: 108
  - files changed: 218
  - additions: 8838
  - deletions: 4193
  - top directories: CMakeLists.txt, cmake, dist, doc/APIreference, doc/XMLreference.rst, doc/_static
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/constraint.py (modified, +580/-465)
    - src/engine/engine_passive.c (modified, +554/-298)
    - mjx/mujoco/mjx/codegen/generate_warp_types.py (added, +570/-0)
    - mjx/mujoco/mjx/codegen/generate_warp_shim.py (added, +546/-0)
    - src/experimental/filament/compat/scene_geom_util.cc (modified, +146/-310)
    - src/engine/engine_core_constraint.c (modified, +284/-167)
    - src/engine/engine_solver.c (modified, +245/-135)
    - src/experimental/filament/filament/renderable.cc (modified, +276/-91)

### 3.8.0
- 标题: 3.8.0
- 类型: 正式版
- 发布时间: 2026-04-25 07:03:38 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.8.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.8.0/changelog.html)
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.8.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.8.0 (April 24, 2026)#
    Added support for Python 3.14.
    Addedmulti-cell supportfor trilinear and quadratic flexes. Note that the implicit
    integrator uses a dense solver for the flex degrees of freedom, which can be slow for multi-cell flexes.
    Added newmj_maxContactfunction to get the maximum number of possible contacts returned by
    is now enabled by default. The new implementation (as opposed to the legacy pipeline) has little performance
    overhead and improves stability.
    Version 3.7.0 (April 14, 2026)#
    Added thedcmotoractuator for modeling DC motors. Supports optional
    These are applied during the passive force and inertia computations, respectively, and are scaled by gear2(“reflected” damping/inertia).
    Stiffness injointsandtendonsand damping injointsandtendonsnow support nonlinear polynomialforce profiles. New
    , etc.) continue to hold the linear coefficient and are unchanged.
    The polynomial order is defined by the new constantmjNPOLY. A future breaking C-API change
    Addedmidpoint integrationfor standalone free bodies in
    Added the centripetal/Coriolis acceleration term\(\dot{J}v\)to the constraint solver bias forconnectandweldequality constaints. This significantly improves the
    decoders are now included as source when building MuJoCo with CMake. This fixes the
    field inmjsFlexhas been removed. It is no longer required sinceMuJoCo Warpsupports native flex collisions.
    mjPLUGIN_LIB_INITmacro now requires a name argument to avoid initialization function name collisions.
    When building with MSVC, we now use the C runtime initialization section to initialize plugins instead of
    . Seeplugin registrationfor more details.
    is removed. Exhaustion of visual geoms is now handled
    URDF parsing no longer hardcodesstrippathto “true”. The setting is now respected and
    Migration:Setstrippathto “true” in MJCF or programmatically using
    The compiler now correctly accounts for negative scaling when loading user specified mesh data.
    Version 3.6.0 (March 10, 2026)#
    but at compile time.
    Addedmjs_getCompilerC API function and a
    read-only property to all Python spec element types.
    This allows querying the compiler settings (e.g.,
    compiler preserved after attachment.
    Flexes now support collisions with SDF geoms.
    Improved memory requirements for
    Add batch rendering support for MJX-Warp. See theMJX-Warp batch renderingsection for
    Fixed a bug wheremjs_attachsilently dropped spatial tendons with wrapping geometries that had no
    attribute (issue #3119, reported by@tomstewart89).
    Version 3.5.0 (February 12, 2026)#
    Added a newSystem Identificationtoolbox (Python), seeREADMEfor details.
    Actuators and sensors now support arbitrary delays via history buffers, and sensor values can be computed at
    Added newflexvertequality constraints that enable cloth simulations with coarser meshes.
    This adds a new attribute value
- Compare 摘要: 3.7.0 -> 3.8.0
  - commits: 76
  - files changed: 219
  - additions: 8081
  - deletions: 5973
  - top directories: .github, CMakeLists.txt, cmake, dist, doc/APIreference, doc/XMLreference.rst
  - representative files:
    - mjx/mujoco/mjx/warp/forward.py (modified, +809/-808)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/smooth.py (modified, +471/-471)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/sensor.py (modified, +442/-442)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/constraint.py (modified, +400/-400)
    - src/engine/engine_core_constraint.c (modified, +250/-441)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/solver.py (modified, +324/-324)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_primitive.py (modified, +248/-248)
    - model/flex/gripper_2d.xml (added, +429/-0)

### 3.7.0
- 标题: 3.7.0
- 类型: 正式版
- 发布时间: 2026-04-14 21:03:47 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.7.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.7.0/changelog.html)
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.7.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.7.0 (April 14, 2026)#
    Added thedcmotoractuator for modeling DC motors. Supports optional
    These are applied during the passive force and inertia computations, respectively, and are scaled by gear2(“reflected” damping/inertia).
    Stiffness injointsandtendonsand damping injointsandtendonsnow support nonlinear polynomialforce profiles. New
    , etc.) continue to hold the linear coefficient and are unchanged.
    The polynomial order is defined by the new constantmjNPOLY. A future breaking C-API change
    Addedmidpoint integrationfor standalone free bodies in
    Added the centripetal/Coriolis acceleration term\(\dot{J}v\)to the constraint solver bias forconnectandweldequality constaints. This significantly improves the
    decoders are now included as source when building MuJoCo with CMake. This fixes the
    field inmjsFlexhas been removed. It is no longer required sinceMuJoCo Warpsupports native flex collisions.
    mjPLUGIN_LIB_INITmacro now requires a name argument to avoid initialization function name collisions.
    When building with MSVC, we now use the C runtime initialization section to initialize plugins instead of
    . Seeplugin registrationfor more details.
    is removed. Exhaustion of visual geoms is now handled
    URDF parsing no longer hardcodesstrippathto “true”. The setting is now respected and
    Migration:Setstrippathto “true” in MJCF or programmatically using
    The compiler now correctly accounts for negative scaling when loading user specified mesh data.
    Version 3.6.0 (March 10, 2026)#
    but at compile time.
    Addedmjs_getCompilerC API function and a
    read-only property to all Python spec element types.
    This allows querying the compiler settings (e.g.,
    compiler preserved after attachment.
    Flexes now support collisions with SDF geoms.
    Improved memory requirements for
    Add batch rendering support for MJX-Warp. See theMJX-Warp batch renderingsection for
    Fixed a bug wheremjs_attachsilently dropped spatial tendons with wrapping geometries that had no
    attribute (issue #3119, reported by@tomstewart89).
    Version 3.5.0 (February 12, 2026)#
    Added a newSystem Identificationtoolbox (Python), seeREADMEfor details.
    Actuators and sensors now support arbitrary delays via history buffers, and sensor values can be computed at
    Added newflexvertequality constraints that enable cloth simulations with coarser meshes.
    This adds a new attribute value
    equality typeflexvert. Uses the method described inChen, Kry and Vouga, 2019.
    Added implicit integration support for deformable objects (flex) in
    Rangefinder sensors can now be attached to a camera using therangefinder/cameraattribute. In this case, the sensor respects thecamera/resolutionattribute and casts
    Ray-cast functions now optionally compute the surface normal at the ray intersection. This is a breaking change
    due to the addition of the
    argument. In Python, in all functions exceptmj_multiRay, it defaults to
    MJCF attribute for cameras has been renamed tocamera/projectionand now accepts the values
- Compare 摘要: 3.6.0 -> 3.7.0
  - commits: 183
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 9655
  - deletions: 3186
  - top directories: .github, CMakeLists.txt, README.md, cmake, dist, doc/APIreference
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/constraint.py (modified, +1166/-470)
    - doc/dcmotor/dcmotor.tex (added, +1412/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/smooth.py (modified, +877/-383)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/io.py (modified, +689/-245)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_flex.py (added, +834/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/bvh.py (modified, +365/-234)
    - doc/XMLreference.rst (modified, +459/-115)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_primitive_core.py (modified, +504/-0)

### 3.6.0
- 标题: 3.6.0
- 类型: 正式版
- 发布时间: 2026-03-11 09:53:34 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.6.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.6.0/changelog.html)
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.6.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.6.0 (March 10, 2026)#
    but at compile time.
    Addedmjs_getCompilerC API function and a
    read-only property to all Python spec element types.
    This allows querying the compiler settings (e.g.,
    compiler preserved after attachment.
    Flexes now support collisions with SDF geoms.
    Improved memory requirements for
    Add batch rendering support for MJX-Warp. See theMJX-Warp batch renderingsection for
    Fixed a bug wheremjs_attachsilently dropped spatial tendons with wrapping geometries that had no
    attribute (issue #3119, reported by@tomstewart89).
    Version 3.5.0 (February 12, 2026)#
    Added a newSystem Identificationtoolbox (Python), seeREADMEfor details.
    Actuators and sensors now support arbitrary delays via history buffers, and sensor values can be computed at
    Added newflexvertequality constraints that enable cloth simulations with coarser meshes.
    This adds a new attribute value
    equality typeflexvert. Uses the method described inChen, Kry and Vouga, 2019.
    Added implicit integration support for deformable objects (flex) in
    Rangefinder sensors can now be attached to a camera using therangefinder/cameraattribute. In this case, the sensor respects thecamera/resolutionattribute and casts
    Ray-cast functions now optionally compute the surface normal at the ray intersection. This is a breaking change
    due to the addition of the
    argument. In Python, in all functions exceptmj_multiRay, it defaults to
    MJCF attribute for cameras has been renamed tocamera/projectionand now accepts the values
    than 1. Relatedly, frustum visualization also works fororthographiccameras.
    Unused by the renderer, it serves as a convenient location to store a camera’s supported output types.
    Addedmj_mountVFSandmj_unmountVFSfunctions for mounting a custom VFS provider. Mounting allows
    The optimization whereby sequentialcollision sensorswith identical attributes shared
    computation has been removed. This results in a (likely minor) performance regression for models which exploited
    this optimization. To recover the performance, use thefromtoand compute the other values
    Parsing has been moved out of experimental into a mjpDecoder plugin. (documentation pending)
    if you have a pre-built USD
    environment variable, MuJoCo should load USD plugins
    (signature) argument ofmj_stateSizeand related functions has been changed from
    . Before this change, invalid negative arguments passed to this function would result
    Allocation sizes inmjModelnow use 64-bit rather than 32-bit integers to accommodate larger scenes.
    to support multiple Warp graph capture modes.
    General improvements to theProgramming/Simulationchapter. Notably, the main discussion ofstatehas been moved there, and the section onmjModel changeshas been
    The usability of theMJCF schemais improved with a collapsible dropdown menu with links to elements
    Fixed a bug inimplicit integratorderivatives where actuator velocity derivatives were
    Fixed a bug inimplicit integratorderivatives where actuator velocity derivatives did not
- Compare 摘要: 3.5.0 -> 3.6.0
  - commits: 192
  - files changed: 278
  - additions: 10326
  - deletions: 3030
  - top directories: .github, .pre-commit-config.yaml, CMakeLists.txt, README.md, cmake, dist
  - representative files:
    - src/experimental/platform/gui_spec.cc (added, +886/-0)
    - src/engine/engine_collision_sdf.c (modified, +628/-30)
    - doc/mjx.rst (modified, +443/-197)
    - src/engine/engine_core_constraint.c (modified, +432/-60)
    - src/experimental/platform/spec_editor.cc (added, +377/-0)
    - src/engine/engine_forward.c (modified, +211/-139)
    - python/mujoco/rendering/classic/renderer.py (added, +339/-0)
    - python/mujoco/renderer.py (modified, +5/-324)

### 3.5.0
- 标题: 3.5.0
- 类型: 正式版
- 发布时间: 2026-02-13 09:20:28 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.5.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.5.0/changelog.html).
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.5.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.5.0 (February 12, 2026)#
    Added a newSystem Identificationtoolbox (Python), seeREADMEfor details.
    Actuators and sensors now support arbitrary delays via history buffers, and sensor values can be computed at
    Added newflexvertequality constraints that enable cloth simulations with coarser meshes.
    This adds a new attribute value
    equality typeflexvert. Uses the method described inChen, Kry and Vouga, 2019.
    Added implicit integration support for deformable objects (flex) in
    Rangefinder sensors can now be attached to a camera using therangefinder/cameraattribute. In this case, the sensor respects thecamera/resolutionattribute and casts
    Ray-cast functions now optionally compute the surface normal at the ray intersection. This is a breaking change
    due to the addition of the
    argument. In Python, in all functions exceptmj_multiRay, it defaults to
    MJCF attribute for cameras has been renamed tocamera/projectionand now accepts the values
    than 1. Relatedly, frustum visualization also works fororthographiccameras.
    Unused by the renderer, it serves as a convenient location to store a camera’s supported output types.
    Addedmj_mountVFSandmj_unmountVFSfunctions for mounting a custom VFS provider. Mounting allows
    The optimization whereby sequentialcollision sensorswith identical attributes shared
    computation has been removed. This results in a (likely minor) performance regression for models which exploited
    this optimization. To recover the performance, use thefromtoand compute the other values
    Parsing has been moved out of experimental into a mjpDecoder plugin. (documentation pending)
    if you have a pre-built USD
    environment variable, MuJoCo should load USD plugins
    (signature) argument ofmj_stateSizeand related functions has been changed from
    . Before this change, invalid negative arguments passed to this function would result
    Allocation sizes inmjModelnow use 64-bit rather than 32-bit integers to accommodate larger scenes.
    to support multiple Warp graph capture modes.
    General improvements to theProgramming/Simulationchapter. Notably, the main discussion ofstatehas been moved there, and the section onmjModel changeshas been
    The usability of theMJCF schemais improved with a collapsible dropdown menu with links to elements
    Fixed a bug inimplicit integratorderivatives where actuator velocity derivatives were
    Fixed a bug inimplicit integratorderivatives where actuator velocity derivatives did not
    Multi-threaded mesh processing, enabled by theusethreadcompiler flag (on by default),
    was in fact disabled by the flag. Fixing this bug speeds up compilation of mesh-heavy models by (up to) the number
    Fixedgravcompbeing ignored for bodies with no joints nested inside jointed parent bodies
    (issue #3066, reported by@Alex108306).
    Version 3.4.0 (December 5, 2025)#
    Added “quadratic” option toflexcomp/dof. This type of fastdeformableflex object is similar to the “trilinear” option, but it includes curved deformations.
    Increase Windows stack size to 16MB to enable models with deep nested body hierarchies.
    Added a new pipeline component functionmj_fwdKinematicsthat combines all kinematics-like sub-components.
    Relatedly, added a clarifying table at the top of theSimulation Pipelinechapter.
    Added a newmj_copyStatefunction that copies state components from one
    Tendon paths can now be queried from Python via
- Compare 摘要: 3.4.0 -> 3.5.0
  - commits: 298
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 18006
  - deletions: 4837
  - top directories: .github, .readthedocs.yml, CMakeLists.txt, README.md, VERSIONING.md, cmake
  - representative files:
    - doc/XMLschema.rst (modified, +6114/-1705)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_convex.py (modified, +857/-656)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/io.py (modified, +1218/-156)
    - doc/XMLreference.rst (modified, +903/-306)
    - doc/images/modeling/delay_buffer_dark.svg (added, +1129/-0)
    - doc/images/modeling/delay_buffer_light.svg (added, +1127/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/bvh.py (added, +1013/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_gjk.py (modified, +434/-367)

### 3.4.0
- 标题: 3.4.0
- 类型: 正式版
- 发布时间: 2025-12-06 07:17:44 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.4.0
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.4.0/changelog.html).
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.4.0/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.4.0 (December 5, 2025)#
    Added “quadratic” option toflexcomp/dof. This type of fastdeformableflex object is similar to the “trilinear” option, but it includes curved deformations.
    Increase Windows stack size to 16MB to enable models with deep nested body hierarchies.
    Added a new pipeline component functionmj_fwdKinematicsthat combines all kinematics-like sub-components.
    Relatedly, added a clarifying table at the top of theSimulation Pipelinechapter.
    Added a newmj_copyStatefunction that copies state components from one
    Tendon paths can now be queried from Python via
    optional dependency is updated to 1.10.0.
    now works with MuJoCo Warp from MJX.
    large array. This may break certain use-cases with Madrona MJX, but we are no longer supporting this codepath.
    We will be migrating users to a Warp-based batch renderer.
    Fixed a bug in the box-box distance computation. Reported by@nvtw.
    Version 3.3.7 (October 13, 2025)#
    The mjSpec C API fieldsmeshdirandtexturedirhave been
    moved tocompiler.meshdirandcompiler.texturedirrespectively. For backwards compatibility, the old fields are still available in the Python API but will be
    removed in a future release.
    Addedmju_getXMLDependenciesfor computing a list of unique asset dependencies from an MJCF file.
    Added the code sample
    which provides command line utility for printing the result ofmju_getXMLDependencies.
    The minimum C++ standard required to compile MuJoCo is now C++20, this has been the case within Google since 2023
    was unused and has been removed.
    Fixissue #2508,
    Fixissue #2881,fitaabbwas adding an offset to the mesh and applying an incorrect frame
    Version 3.3.6 (September 15, 2025)#
    a strict improvement over the monolithic constraint solver, please let us know if you experience any issues.
    Contact sensorsubtree1/subtree2specification is now available for any body, not
    was moved from the end of the solver call (mj_fwdConstraint) to
    the end ofmj_step, and is now updated with all other state variables. This change makesmj_forwardfully idempotent.
    Before this change, callingmj_forwardrepeatedly would make the constraint solver converge,
    Migration:If your code depended on this behavior, you can recover it by updating manually after eachmj_forward:
    Furthermore, this change has a numerical impact on the output of theRK4integrator.
    Before this change, due to the
    the solver convergence of RK4 was faster, at the cost of unprincipled integration. This change makes the RK4
    integration principled and well-defined. Since this change to RK4 is effectively a bug fix, migration to the
    flag for disabling passive forces was removed and replaced bymjDSBL_SPRINGandmjDSBL_DAMPERwith correspondingmjcfattributes. Each flag disables only joint and tendon
    compensation, fluid forces, forces computed by themjcb_passivecallback, and forces computed bypluginswhen passed themjPLUGIN_PASSIVEcapability flag.
    Added support for shells with a curved reference configuration. See thisexample.
    Added experimental option forpassivecontacts involving flexes.
    to the public MJX API. Add Warp support for
    Fixed a latent bug where MjData objects were not serialized correctly by the Python bindings when islanding was
- Compare 摘要: 3.3.7 -> 3.4.0
  - commits: 282
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 8449
  - deletions: 6079
  - top directories: .github, .gitignore, .readthedocs.yml, CMakeLists.txt, README.md, STYLEGUIDE.md
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/io.py (modified, +1017/-1931)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_primitive.py (modified, +602/-514)
    - include/mujoco/experimental/usd/mjcPhysics/tendon.h (added, +816/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_convex.py (modified, +594/-204)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_gjk_legacy.py (removed, +0/-715)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/sensor.py (modified, +241/-317)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/smooth.py (modified, +212/-276)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/support.py (modified, +380/-89)

### 3.3.7
- 标题: 3.3.7
- 类型: 正式版
- 发布时间: 2025-10-15 01:38:32 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.3.7
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.3.7/changelog.html).
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.3.7/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - API
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.3.7 (October 13, 2025)#
    The mjSpec C API fieldsmeshdirandtexturedirhave been
    moved tocompiler.meshdirandcompiler.texturedirrespectively. For backwards compatibility, the old fields are still available in the Python API but will be
    removed in a future release.
    Addedmju_getXMLDependenciesfor computing a list of unique asset dependencies from an MJCF file.
    Added the code sample
    which provides command line utility for printing the result ofmju_getXMLDependencies.
    The minimum C++ standard required to compile MuJoCo is now C++20, this has been the case within Google since 2023
    was unused and has been removed.
    Fix#2508,
    Fix#2881,fitaabbwas adding an offset to the mesh and applying an incorrect frame
    Version 3.3.6 (September 15, 2025)#
    a strict improvement over the monolithic constraint solver, please let us know if you experience any issues.
    Contact sensorsubtree1/subtree2specification is now available for any body, not
    was moved from the end of the solver call (mj_fwdConstraint) to
    the end ofmj_step, and is now updated with all other state variables. This change makesmj_forwardfully idempotent.
    Before this change, callingmj_forwardrepeatedly would make the constraint solver converge,
    Migration:If your code depended on this behavior, you can recover it by updating manually after eachmj_forward:
    Furthermore, this change has a numerical impact on the output of theRK4integrator.
    Before this change, due to the
    the solver convergence of RK4 was faster, at the cost of unprincipled integration. This change makes the RK4
    integration principled and well-defined. Since this change to RK4 is effectively a bug fix, migration to the
    flag for disabling passive forces was removed and replaced bymjDSBL_SPRINGandmjDSBL_DAMPERwith correspondingmjcfattributes. Each flag disables only joint and tendon
    compensation, fluid forces, forces computed by themjcb_passivecallback, and forces computed bypluginswhen passed themjPLUGIN_PASSIVEcapability flag.
    Added support for shells with a curved reference configuration. See thisexample.
    Added experimental option forpassivecontacts involving flexes.
    to the public MJX API. Add Warp support for
    Fixed a latent bug where MjData objects were not serialized correctly by the Python bindings when islanding was
    Version 3.3.5 (August 8, 2025)#
    Added theinsidesitesensor, for checking if an object is inside the volume of a site.
    Added thecontactsensor, for reporting contact information according to user-defined
    The purpose of thecontactsensor is to report contact-related information in a fixed-size array. This is
    Added thetactilesensor, for measuring the penetration depth between two objects at given
    points and the sliding velocities in the tangent frame. The sensor reports tactile data only when colliding with
    Removed the SdfLib plugin and the dependency onSdfLib. SDFs are now
    supported natively in mjModel.
    Added the functionality to create a builtin meshes, seemesh/builtin.
    combines the Composite Rigid Body algorithm inmj_crband additional terms related totendon armature. Code that usesmj_crbto compute the inertia should now usemj_makeMinstead.
    Fixed a bug that caused object lists in the child to have missing elements after attaching an mjSpec. This was
    caused by adding to the lists only the objects that belong to the tree of the requested body, but this causes to
- Compare 摘要: 3.3.6 -> 3.3.7
  - commits: 137
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 6936
  - deletions: 11234
  - top directories: .readthedocs.yml, CMakeLists.txt, README.md, STYLEGUIDE.md, cmake, dist
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_primitive.py (modified, +952/-2170)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_primitive_core.py (added, +1433/-0)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/sensor.py (modified, +753/-266)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/io.py (modified, +799/-154)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_driver_test.py (removed, +0/-906)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_gjk.py (modified, +433/-293)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_sdf.py (modified, +474/-163)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_convex.py (modified, +413/-194)

### 3.3.6
- 标题: 3.3.6
- 类型: 正式版
- 发布时间: 2025-09-16 22:28:40 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.3.6
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.3.6/changelog.html).
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.3.6/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - MJX
    - OpenUSD
    - File Format Plugin
    - Changelog
    3.3.6 (September 15, 2025)#
    a strict improvement over the monolithic constraint solver, please let us know if you experience any issues.
    Contact sensorsubtree1/subtree2specification is now available for any body, not
    was moved from the end of the solver call (mj_fwdConstraint) to
    the end ofmj_step, and is now updated with all other state variables. This change makesmj_forwardfully idempotent.
    Before this change, callingmj_forwardrepeatedly would make the constraint solver converge,
    Migration:If your code depended on this behavior, you can recover it by updating manually after eachmj_forward:
    Furthermore, this change has a numerical impact on the output of theRK4integrator.
    Before this change, due to the
    the solver convergence of RK4 was faster, at the cost of unprincipled integration. This change makes the RK4
    integration principled and well-defined. Since this change to RK4 is effectively a bug fix, migration to the
    flag for disabling passive forces was removed and replaced bymjDSBL_SPRINGandmjDSBL_DAMPERwith correspondingmjcfattributes. Each flag disables only joint and tendon
    compensation, fluid forces, forces computed by themjcb_passivecallback, and forces computed bypluginswhen passed themjPLUGIN_PASSIVEcapability flag.
    Added support for shells with a curved reference configuration. See thisexample.
    Added experimental option forpassivecontacts involving flexes.
    to the public MJX API. Add Warp support for
    Fixed a latent bug where MjData objects were not serialized correctly by the Python bindings when islanding was
    Version 3.3.5 (August 8, 2025)#
    Added theinsidesitesensor, for checking if an object is inside the volume of a site.
    Added thecontactsensor, for reporting contact information according to user-defined
    The purpose of thecontactsensor is to report contact-related information in a fixed-size array. This is
    Added thetactilesensor, for measuring the penetration depth between two objects at given
    points and the sliding velocities in the tangent frame. The sensor reports tactile data only when colliding with
    Removed the SdfLib plugin and the dependency onSdfLib. SDFs are now
    supported natively in mjModel.
    Added the functionality to create a builtin meshes, seemesh/builtin.
    combines the Composite Rigid Body algorithm inmj_crband additional terms related totendon armature. Code that usesmj_crbto compute the inertia should now usemj_makeMinstead.
    Fixed a bug that caused object lists in the child to have missing elements after attaching an mjSpec. This was
    caused by adding to the lists only the objects that belong to the tree of the requested body, but this causes to
    Fixed a bug where the convex hull of a collision mesh was not being computed if the mesh could only collide via acontact pair.
    On Linux, built distribution packages (wheels) now target the
    based on CentOS 7, which reached end-of-life in June 2024.
    Add Warp as a backend implementation for MJX. The implementation can be specified via
    a CUDA device and
    Version 3.3.4 (July 8, 2025)#
    In the mjSpec C API, directly setting an element’s name usingmjs_setStringhas been replaced with a new
    functionmjs_setNamewhich allows checking for naming collisions at set-time rather than compile-time, for
    attribute has been removed from all mjs elements. Known issue:
    Added support for setting the initial camera in the viewer usingvisual/global/cameraid.
    Added support to only sync the state in the Pythonpassive viewer’s
- Compare 摘要: 3.3.5 -> 3.3.6
  - commits: 96
  - files changed: 240
  - additions: 6232
  - deletions: 4667
  - top directories: .github, CMakeLists.txt, cmake, dist, doc/APIreference, doc/OpenUSD
  - representative files:
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/solver.py (modified, +780/-1298)
    - src/engine/engine_core_util.c (added, +961/-0)
    - mjx/mujoco/mjx/warp/forward.py (modified, +96/-302)
    - python/mujoco/introspect/structs.py (modified, +170/-211)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_hfield.py (modified, +166/-162)
    - mjx/mujoco/mjx/third_party/mujoco_warp/_src/collision_driver.py (modified, +164/-160)
    - src/engine/engine_core_constraint.c (modified, +154/-165)
    - model/plugin/sdf/asset/die.obj (added, +296/-0)

### 3.3.5
- 标题: 3.3.5
- 类型: 正式版
- 发布时间: 2025-08-09 07:02:07 CST
- 链接: https://github.com/google-deepmind/mujoco/releases/tag/3.3.5
- GitHub release body:
See the [changelog](https://mujoco.readthedocs.io/en/3.3.5/changelog.html).
- 外链文档摘录:
  - https://mujoco.readthedocs.io/en/3.3.5/changelog.html
    Changelog - MuJoCo Documentation
    - XML Reference
    - API Reference
    - Python
    - MJX
    - OpenUSD
    - File Format Plugin
    - Changelog
    Version 3.3.5 (August 8, 2025)#
    Added theinsidesitesensor, for checking if an object is inside the volume of a site.
    Added thecontactsensor, for reporting contact information according to user-defined
    The purpose of thecontactsensor is to report contact-related information in a fixed-size array. This is
    Added thetactilesensor, for measuring the penetration depth between two objects at given
    points and the sliding velocities in the tangent frame. The sensor reports tactile data only when colliding with
    Removed the SdfLib plugin and the dependency onSdfLib. SDFs are now
    supported natively in mjModel.
    Added the functionality to create a builtin meshes, seemesh/builtin.
    combines the Composite Rigid Body algorithm inmj_crband additional terms related totendon armature. Code that usesmj_crbto compute the inertia should now usemj_makeMinstead.
    Fixed a bug that caused object lists in the child to have missing elements after attaching an mjSpec. This was
    caused by adding to the lists only the objects that belong to the tree of the requested body, but this causes to
    Fixed a bug where the convex hull of a collision mesh was not being computed if the mesh could only collide via acontact pair.
    On Linux, built distribution packages (wheels) now target the
    based on CentOS 7, which reached end-of-life in June 2024.
    Add Warp as a backend implementation for MJX. The implementation can be specified via
    a CUDA device and
    Version 3.3.4 (July 8, 2025)#
    In the mjSpec C API, directly setting an element’s name usingmjs_setStringhas been replaced with a new
    functionmjs_setNamewhich allows checking for naming collisions at set-time rather than compile-time, for
    attribute has been removed from all mjs elements. Known issue:
    Added support for setting the initial camera in the viewer usingvisual/global/cameraid.
    Added support to only sync the state in the Pythonpassive viewer’s
    useful to improve performance. The default behavior is unchanged and copies the entire model and data.
    Added missing item documentation and clarified the nature of breaking changes in the 3.3.3 changelog.
    See items 3 and 4 below.
    Version 3.3.3 (June 10, 2025)#
    Refactored island implementation so that island data is memory-contiguous. This speeds up island processing in the
    solver and clears the way for the addition of the Newton and PGS solvers (currently only CG is supported).
    Removed theshellplugin. This is now supported byflexcompand is active depending on
    theelastic2dattribute (off by default).
    Replaced thedirectional(boolean) field for lights with atypefield (of typemjtLightType) to allow for additional lighting
    Migration:Replace light/directional=”false/true” with light/type=”spot/directional”, respectively.
    AddedmjtColorSpaceenum and associatedcolorspaceattribute that allows
    Migration:Setcolorspaceto “linear” for all textures that should look like
    they did before this change.
    Added new sub-componentmj_makeMwhich combines themj_crbcall with additional logic to support the
    introduction in 3.3.1 oftendon armature. In addition to the traditional
    Added a new functionmj_copyBackto copy real-valued arrays in an mjModel to a compatible mjSpec.
    Removed the limitation offusestaticto models which contain no references. The
