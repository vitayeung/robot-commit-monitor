# Release Roadmap Reference

- 仓库: `NVIDIA/warp`
- 对应主报告: `NVIDIA_warp_release_roadmap_v6.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要
- 版本总数: 12
- 正式版数量: 11
- 预发布版数量: 1
- 外链文档覆盖版本数: 7
- compare 摘要覆盖版本数: 11
- 最新版本: v1.14.0 (2026-06-01 23:29:00 CST)
- 最早纳入统计版本: v1.8.1 (2025-08-02 01:41:44 CST)

## Release 时间线
- 2026-06-01 23:29:00 CST | v1.14.0 | 正式版
- 2026-05-04 12:52:26 CST | v1.13.0 | 正式版
- 2026-04-06 14:17:55 CST | v1.12.1 | 正式版
- 2026-03-07 04:21:37 CST | v1.12.0 | 正式版
- 2026-02-04 05:20:35 CST | v1.11.1 | 正式版
- 2026-01-02 21:26:06 CST | v1.11.0 | 正式版
- 2025-12-01 21:13:27 CST | v1.10.1 | 正式版
- 2025-11-02 22:11:50 CST | v1.10.0 | 正式版
- 2025-10-01 15:37:06 CST | v1.9.1 | 正式版
- 2025-09-05 11:54:40 CST | v1.9.0 | 正式版
- 2025-08-20 23:59:11 CST | v1.9.0rc1 | 预发布版
- 2025-08-02 01:41:44 CST | v1.8.1 | 正式版

## 证据附录

### v1.14.0
- 标题: v1.14.0
- 类型: 正式版
- 发布时间: 2026-06-01 23:29:00 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.14.0
- GitHub release body:
# Warp v1.14.0

Warp v1.14 expands serialized CPU capture support: captured graphs can now include backward launches, tiled kernels, richer launch arguments, and `.wrp` files with arrays nested inside structs or `wp.indexedarray` arguments. This release also adds multi-environment FEM support for batched simulations, reusable and batched linear solvers, pluggable logging, portable tile FFT and solver fallbacks, stable JAX integration APIs, and relaxed CPU/GPU array access for Heterogeneous Memory Management (HMM) and Address Translation Services (ATS) systems.

## New features

### API Capture expands to cover more workflows

Building on the initial API Capture serialization support in [Warp v1.13](https://github.com/NVIDIA/warp/releases/tag/v1.13.0), Warp v1.14 primarily broadens the set of CPU graph patterns that can be saved and replayed. CPU captures can now include forward execution and reverse-mode passes from `wp.Tape().backward()`, `wp.launch_tiled()` kernels, and scalar parameters of any size (#1431). The shared `.wrp` serialization format also now supports `@wp.struct` arguments that contain arrays and `wp.indexedarray` arguments that carry data, gradient, and index buffers.

> [!IMPORTANT]
> **Upgrade impact for APIC users:**
>
> - Recapture `.wrp` files saved by Warp v1.13. Warp v1.14 writes APIC format version 10 and rejects the previous format.
> - Update native C/C++ APIC handle declarations to explicit pointers such as `APICState*` and `APICGraph*`. Ownership and destroy calls are unchanged. See the [APIC migration diff](#rn-v114-apic-migration).

Saved APIC graphs can still be consumed from standalone C++ through the C API declared in `warp/native/apic.h`. Native replay behavior is unchanged apart from the explicit pointer spelling for APIC handles....
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/releases/tag/v1.13.0
    Release v1.13.0 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    github-actionsreleased this04 May 04:52
    Warp v1.13 introduces experimental graph capture serialization with CPU replay, letting captured simulations roundtrip through a portable
    file and load from standalone C++ on either GPU or CPU. It also adds an experimental cuBQL BVH backend for
    scalar type, a pluggable CUDA allocator interface with built-in RAPIDS Memory Manager (RMM) integration, scoped memory tracking with C++-layer call-site attribution, and a batch of new tile primitives (
    This is an experimental feature. The API may change without a formal deprecation cycle.
    Warp v1.13 introduces a portable serialized-graph format. Operations recorded during
    and replayed from either Python or standalone C++ via
    , enabling cross-process and cross-language graph reuse (#1349). CPU graph capture is also new in this release: the same
    , and the underlying APIC operation log is what gets serialized. A new
    importwarpaswpwithwp.ScopedDevice("cpu"):a=wp.zeros(64,dtype=float)b=wp.zeros(64,dtype=float)wp.capture_begin(apic=True)wp.copy(b,a)graph=wp.capture_end()wp.capture_save(graph,"demo",inputs={"a":a},outputs={"b":b})# Later (in the same process or a fresh one): replay from disk.withwp.ScopedDevice("cpu"):loaded=wp.capture_load("demo")loaded.set_param("a",wp.array([1.0]*64,dtype=float))wp.capture_launch(loaded)
    Loading and replaying from standalone C++ (CPU device shown). The full example also walks the
    APICGraph graph = wp_apic_load_graph(nullptr,"demo.wrp",1);//1 = CPU device//(Walk demo_modules/, load each .o, and register kernels. See linked example.)wp_apic_set_param(graph,"a", a_buffer, a_size);wp_apic_cpu_replay_graph(graph);//For CUDA: cudaGraphLaunch(wp_apic_get_cuda_graph_exec(graph), stream)wp_apic_get_param(graph,"b", b_buffer, b_size);wp_apic_destroy_graph(graph);
    warp/examples/cpp/02_apic_visualization
    warp/examples/cpp/03_apic_visualization_cpu
    <hash>.cubin / .meta  # one per CUDA kernel module, arch-pinned
    registers named bindings so the consumer side can swap in fresh inputs and read outputs by name without touching the graph topology.
    support replay on both CPU and CUDA. Loaded graphs expose
    for each registered binding, plus
    remaplet kernels accept mesh handles whose underlying objects are reconstructed on load. APIC walks
    API Capture is experimental, and we plan to keep adding capabilities and closing gaps over future releases (tracker:#1388). For now, regenerate
    artifacts when upgrading Warp. The current operation set, handle types, and platform constraints are documented in theGraphs section of the user guide.
    to build its acceleration structure withcuBQL, an Apache 2.0-licensed header-only CUDA library for fast BVH construction and traversal (#1286). For ray-heavy workloads on dense static meshes, where the existing SAH builder's exhaustive construction dominates setup time and where ray traversal sits on the simulation hot path, cuBQL typically delivers faster ray queries alongside consistently lower build times than the SAH, median, and LBVH builders. As one specific data point, a Warp-based renderer benchmark on an RTX 4090 (Franka Emika Panda visual mesh, 8192 parallel worlds) saw simulation time drop from 1.41 s to 0.98 s after switching the constructor with no other changes. Speedups depend heavily on mesh size, query mix, and how much of the frame the mesh queries occupy, so benchmark on your own scene before relying on a particular win.
    through cuBQL's traversal kernels. Extending it to point queries, AABB queries, grouped queries, and winding-number support is future work. Today, passing
    importwarpaswpmesh=wp.Mesh(points=points,# wp.array of wp.vec3indices=tri_indices,# wp.array of wp.int32, shape (num_tris * 3,)bvh_constructor="cubql",
    Pluggable CUDA allocator and RMM integration
    CUDA device-memory allocations can now be routed through any object implementing the
    delegates to RAPIDS Memory Manager so Warp can share a memory pool with PyTorch, CuPy, or any other RMM-aware framework, eliminating duplicate caching on GPUs that train and simulate in the same process.
    importrmmimportwarpaswprmm.reinitialize(pool_allocator=True,initial_pool_size=2**30)wp.set_cuda_allocator(wp.utils.AllocatorRmm())a=wp.zeros(1024,dtype=wp.float32,device="cuda:0")# served from the RMM pool
    flag enable allocation tracking with call-site attribution and per-category reports across GPU, host, and pinned-host memory (#1269). Tracking is implemented in the C++ native layer by intercepting all
    calls, so internal allocations from BVH, hash-grid, mesh, volume, and sparse subsystems show up alongside Python-originated arrays, labeled with their subsystem (e.g.
    importwarpaswp@wp.kerneldeffill(x:wp.array[float]):i=wp.tid()x[i]=float(i)withwp.ScopedMemoryTracker("training step"):a=wp.zeros(1_000_000,dtype=wp.float32,device="cuda:0")b=wp.zeros(2_000_000,dtype=wp.float32,device="cuda:0")wp.launch(fill,dim=a.s...
  - https://clang.llvm.org/docs/AddressSanitizer.html
    AddressSanitizer — Clang 23.0.0git documentation
    AddressSanitizer is a fast memory error detector. It consists of a compiler
    Typical slowdown introduced by AddressSanitizer is2x.
    for the use/testing of AddressSanitizer:
    Simply compile and link your program with
    AddressSanitizer run-time library should be linked to the final executable, so
    shared libraries, the AddressSanitizer run-time is not linked, so
    may cause link errors (donât use it with AddressSanitizer). To
    get a reasonable performance add
    in error messages add
    %catexample_UseAfterFree.ccint main(int argc, char **argv) {int *array = new int[100];delete [] array;return array[argc];  // BOOM}#Compileandlink%clang++-O1-g-fsanitize=address-fno-omit-frame-pointerexample_UseAfterFree.cc
    #Compile%clang++-O1-g-fsanitize=address-fno-omit-frame-pointer-cexample_UseAfterFree.cc#Link%clang++-g-fsanitize=addressexample_UseAfterFree.o
    exit with a non-zero exit code. AddressSanitizer exits on the first detected error.
    This approach allows AddressSanitizer to produce faster and smaller generated code
    Fixing bugs becomes unavoidable. AddressSanitizer does not produce
    If your process is sandboxed and you are running on OS X 10.10 or earlier, you
    the ASan library that is packaged with the compiler used to build the
    To make AddressSanitizer symbolize its output
    %ASAN_OPTIONS=symbolize=0./a.out2>log%projects/compiler-rt/lib/asan/scripts/asan_symbolize.py/<log|c++filt==9442== ERROR: AddressSanitizer heap-use-after-free on address 0x7f7ddab8c084 at pc 0x403c8c bp 0x7fff87fb82d0 sp 0x7fff87fb82c8READ of size 4 at 0x7f7ddab8c084 thread T0#00x403c8cinmainexample_UseAfterFree.cc:4#10x7f7ddabcac4din__libc_start_main??:0...
    file:line info in the AddressSanitizer reports.
    AddressSanitizer can optionally detect dynamic initialization order problems,
    Note that this option is not supported on macOS.
    AddressSanitizer can optionally detect stack use after return problems.
    : Adds the code for detection, but it can be disabled via the
    AddressSanitizer can detect overflows in containers with custom allocators
    (such as std::vector) where the library developers have added calls into the
    AddressSanitizer runtime to indicate which memory is poisoned etc.
    If the binary is partially AddressSanitizer instrumented, these
    For more information on leak detector in AddressSanitizer, seeLeakSanitizer. The leak detection is turned on by default on Linux,
    however, it is not yet supported on other platforms.
    AddressSanitizer is not expected to produce false positives. If you see one,
    Runtime interposition allows AddressSanitizer to find bugs in code that is
    not being recompiled. If you run into an issue in external libraries, we
    gets addressed. However, you can use the following suppression mechanism
    does not work on code recompiled with AddressSanitizer. To suppress errors
    AddressSanitizer is enabled.__has_featurecan be used for
    #if defined(__has_feature)#  if __has_feature(address_sanitizer)// code that builds only under AddressSanitizer#  endif#endif
    Some code should not be instrumented by AddressSanitizer. One may use
    particular function. This attribute may not be supported by other
    compilers, so we suggest to use it together with
    The same attribute used on a global variable prevents AddressSanitizer
    from adding redzones around it and detecting out of bounds accesses.
    function will not be inlined heuristically by the compiler into a sanitized function.
    is not supported, and will often lead to unexpected results. To avoid mixing these attributes, use:
    // Note, __has_feature test for sanitizers is deprecated, and Clang will support __SANITIZE_<sanitizer>__ similar to GCC.#if __has_feature(address_sanitizer) || defined(__SANITIZE_ADDRESS__) || ... <other sanitizers>#define ALWAYS_INLINE_IF_UNINSTRUMENTED#else#define ALWAYS_INLINE_IF_UNINSTRUMENTED __attribute__((always_inline))#endif
    conditionally execute code depending on whether AddressSanitizer checks are
    void__asan_load8(void*);inline__attribute__((always_inline))voidmy_helper(void*addr){if(__builtin_allow_sanitize_check("address"))__asan_load8(addr);// ... actual logic, e.g. inline assembly ...asmvolatile("..."::"r"(addr):"memory");}voidinstrumented_function(){...my_helper(buf);// checks are active...}__attribute__((no_sanitize("address")))voiduninstrumented_function(){...my_helper(buf);// checks are skipped...}
    can be used at compile time to
- Compare 摘要: v1.13.0 -> v1.14.0
  - commits: 137
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 14473
  - deletions: 3402
  - top directories: .claude, .codex, .github, .gitignore, .gitlab-ci.yml, .gitlab
  - representative files:
    - design/hardware-coherent-memory-access.md (added, +1076/-0)
    - notebooks/core_01_basics.ipynb (removed, +0/-797)
    - .claude/skills/release-notes/references/style-rules.md (added, +663/-0)
    - .codex/skills/release-notes/references/style-rules.md (added, +663/-0)
    - docs/user_guide/runtime.rst (modified, +540/-57)
    - .claude/skills/release-notes/scripts/list_contributors.py (added, +596/-0)
    - .codex/skills/release-notes/scripts/list_contributors.py (added, +596/-0)
    - notebooks/core_04_meshes.ipynb (removed, +0/-554)

### v1.13.0
- 标题: v1.13.0
- 类型: 正式版
- 发布时间: 2026-05-04 12:52:26 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.13.0
- GitHub release body:
# Warp v1.13.0

Warp v1.13 introduces experimental graph capture serialization with CPU replay, letting captured simulations roundtrip through a portable `.wrp` file and load from standalone C++ on either GPU or CPU. It also adds an experimental cuBQL BVH backend for `wp.Mesh` that accelerates ray-heavy mesh queries, the `wp.bfloat16` scalar type, a pluggable CUDA allocator interface with built-in RAPIDS Memory Manager (RMM) integration, scoped memory tracking with C++-layer call-site attribution, and a batch of new tile primitives (`tile_dot`, `tile_axpy`, `tile_stack`, scatter helpers).

## New features

### Graph capture serialization and CPU replay

> [!IMPORTANT]
> This is an experimental feature. The API may change without a formal deprecation cycle.

Warp v1.13 introduces a portable serialized-graph format. Operations recorded during `wp.capture_begin(apic=True)` / `wp.capture_end()` can be saved to a `.wrp` file with `wp.capture_save()` and replayed from either Python or standalone C++ via `wp.capture_load()`, enabling cross-process and cross-language graph reuse (#1349). CPU graph capture is also new in this release: the same `wp.Graph` object now replays on CPU through `wp.capture_launch()`, and the underlying APIC operation log is what gets serialized. A new `wp.handle` (a `uint64` alias) carries `wp.Mesh` handles across save and load so kernels can keep referencing meshes after deserialization.

```python
import warp as wp

with wp.ScopedDevice("cpu"):
    a = wp.zeros(64, dtype=float)
    b = wp.zeros(64, dtype=float)

    wp.capture_begin(apic=True)
    wp.copy(b, a)
    graph = wp.capture_end()

    wp.capture_save(graph, "demo", inputs={"a": a}, outputs={"b": b})

# Later (in the same process or a fresh one): replay from disk.
with wp.ScopedDevice("cp...
- Compare 摘要: v1.12.1 -> v1.13.0
  - commits: 349
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 6156
  - deletions: 27007
  - top directories: .coderabbit.yml, .gitattributes, .github, .gitignore, .gitlab-ci.yml, .gitlab
  - representative files:
    - exts/omni.warp/data/scenes/prim_flocking.usda (removed, +0/-14512)
    - exts/omni.warp.core/docs/CHANGELOG.md (removed, +0/-2129)
    - docs/user_guide/interoperability.rst (modified, +106/-1831)
    - docs/user_guide/interoperability_pytorch.rst (added, +881/-0)
    - docs/user_guide/interoperability_jax.rst (added, +834/-0)
    - docs/user_guide/tiles.rst (modified, +680/-14)
    - docs/user_guide/runtime.rst (modified, +578/-87)
    - exts/omni.warp/data/scenes/wave_deformation.usda (removed, +0/-615)

### v1.12.1
- 标题: v1.12.1
- 类型: 正式版
- 发布时间: 2026-04-06 14:17:55 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.12.1
- GitHub release body:
# Warp v1.12.1

Warp v1.12.1 is a bugfix release following v1.12.0. For a complete list of changes, see the [changelog](https://github.com/NVIDIA/warp/blob/v1.12.1/CHANGELOG.md).

## Highlights

- **Tile Correctness**: Fixed several tile kernel issues, including kernel dispatch using incorrect `block_dim` across devices (#1254), `wp.tile_matmul()` and `wp.tile_fft()` ignoring module-level `enable_backward` (#1320), and `@wp.func` with tile parameters failing to compile with shared-memory tiles (#1313). Tile parameters in `@wp.func` are now passed by reference for both register and shared storage, matching Python's semantics for mutable objects.

- **Silent Correctness Bugs**: Fixed compile-time constants silently losing precision when passed to 64-bit scalar constructors like `wp.float64()` (#485), `wp.HashGrid` neighbor queries missing results for negative coordinates (#1256), and augmented assignments with subscript or attribute targets (e.g., `s.field += expr`, `arr[i] *= expr`) double-evaluating the target expression (#1233).

- **Type System and Tooling**: Fixed struct field assignments converting Warp scalar types to plain Python types (#1288), `wp.array[dtype]` not being recognized by mypy (#1278), and array annotation `repr()` displaying raw internal class paths (#1341).

- **Kit Extensions Removed**: The Omniverse Kit extensions have been removed from this repository (#1296).

- **New Examples**: Added a differentiable 2-D Navier-Stokes optimization example and three `warp.fem` examples for Taylor-Green vortex, Kelvin-Helmholtz instability, and shallow water equations.

## Announcements

### Upcoming removals

The following deprecations will be finalized in **Warp 1.13.0**:

- **Python 3.9 support will be removed.** Python 3.10 becomes the minimum supported...
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/blob/v1.12.1/CHANGELOG.md
    warp/CHANGELOG.md at v1.12.1 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    2390 lines (2048 loc) · 155 KB
    - Remove the Kit extensions from this repository (GH-1296).
    - Fix silent precision loss in compile-time constants passed to 64-bit scalar type constructors
    - Fix
    - Fix augmented assignments double-evaluating sub-expressions for subscript and attribute targets
    with tile parameters failing to compile when called with shared-memory tiles
    - Fix kernel dispatch using incorrect
    exceeds the tile element count (GH-1133).
    - Fix a potential crash when multiple processes compile CUDA kernels concurrently with a shared kernel cache
    for Warp builds using CUDA Toolkit 12.8/12.9 (GH-1284).
    and other complex type annotations (GH-1300).
    - Fix struct field assignment converting Warp scalar types (e.g.,
    to plain Python types, causing subsequent reads to return
    - Fix element assignment for boolean vectors (e.g.,
    - Fix array annotation
    - Add differentiable 2-D Navier-Stokes example (
    for optimal initial perturbation, complementing the solver in
    - Add
    - Fix internal module path
    - Fix spectral Poisson solver in 2-D Navier-Stokes examples using incorrect modified wavenumbers
    - Experimental: Add
    for hardware-accelerated texture sampling on CUDA devices,
    Includes CUDA interop APIs for array↔texture copies and surface handle access
    while keeping libmathdx available for Cholesky/FFT (GH-1228).
    - Add subscript-style type hints for array and tile types (e.g.,
    - Add support for
    for element-wise and broadcast multiplication (GH-1006).
    for element-wise and broadcast division (GH-1009).
    - Add differentiability support for
    - Add optional
    to ensure FFI calls are always executed by JAX (GH-1240).
    including software versions, CUDA info, build flags, and devices (GH-1221).
    to query CUDA versions
    ) suffixes to the
    for CUDA devices (GH-1243).
    - Add quaternion and spatial transformation helpers (
    ) on GPU. Only floating-point types are supported;
    falls back to exact arithmetic on CPU (GH-1199).
    - Add public API for marching cubes lookup tables as class attributes on
    for advanced use cases like sparse volume extraction (GH-1151).
    to the public API for graph coloring (GH-1145).
    : Add B-spline shape functions with
    (3D), supporting degrees 1-3. Use via
    skipping CUDA toolkit detection and
    - Remove deprecated support for constructing matrices from vectors via
- Compare 摘要: v1.12.0 -> v1.12.1
  - commits: 90
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 908
  - deletions: 32532
  - top directories: .github, .gitignore, .gitlab-ci.yml, .gitlab, .greptile, .nspect-allowlist.toml
  - representative files:
    - exts/omni.warp/data/scenes/prim_flocking.usda (removed, +0/-14512)
    - exts/omni.warp.core/docs/CHANGELOG.md (removed, +0/-2129)
    - exts/omni.warp/omni/warp/nodes/_impl/kernel.py (removed, +0/-787)
    - exts/omni.warp/data/scenes/wave_deformation.usda (removed, +0/-615)
    - exts/omni.warp/omni/warp/nodes/_impl/OgnSamplePrimFlocking.py (removed, +0/-560)
    - exts/omni.warp/data/scenes/ocean.usda (removed, +0/-518)
    - exts/omni.warp/omni/warp/nodes/tests/test_api_from_omni_graph.py (removed, +0/-444)
    - exts/omni.warp/omni/warp/nodes/_impl/OgnWaveSolve.py (removed, +0/-415)

### v1.12.0
- 标题: v1.12.0
- 类型: 正式版
- 发布时间: 2026-03-07 04:21:37 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.12.0
- GitHub release body:
# Warp v1.12.0

Warp v1.12 adds experimental hardware-accelerated texture sampling on CUDA GPUs, extends tile programming with element-wise arithmetic operators and differentiable FFT, and broadens JAX interoperability with `jax.vmap` support. This release also introduces subscript-style type hints for better IDE integration, new quaternion and approximate-math builtins, B-spline shape functions in `warp.fem`, and a collection of utility and diagnostics APIs.

## New features

### Hardware-accelerated textures

> **Experimental.** This API may change without a formal deprecation cycle.

Warp v1.12 introduces `wp.Texture1D`, `wp.Texture2D`, and `wp.Texture3D` classes that leverage CUDA texture memory for hardware-accelerated interpolation directly inside Warp kernels. On GPU, texture reads are routed through dedicated texture units that perform filtered lookups in a single instruction, making them ideal for rendering, volume sampling, signed-distance-field queries, and simulation lookup tables. On CPU, a software fallback provides identical semantics so the same kernel code runs on both devices.

```python
import warp as wp
import numpy as np

wp.init()

# 64x64 single-channel height map
data = np.random.rand(64, 64).astype(np.float32)

# Create a 2D texture with bilinear filtering
tex = wp.Texture2D(data, filter_mode=wp.Texture.FILTER_LINEAR)

@wp.kernel
def sample_texture(tex: wp.Texture2D, coords: wp.array[wp.vec2f], out: wp.array[float]):
    i = wp.tid()
    # Coordinates are in [0, 1]; bilinear interpolation is automatic
    out[i] = wp.texture_sample(tex, coords[i], dtype=float)

coords = wp.array(np.random.rand(1024, 2).astype(np.float32), dtype=wp.vec2f)
result = wp.zeros(1024, dtype=float)
wp.launch(sample_texture, dim=1024, inputs=[tex, coords, result])

pr...
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/blob/v1.12.0/CHANGELOG.md
    warp/CHANGELOG.md at v1.12.0 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    2324 lines (1991 loc) · 150 KB
    - Experimental: Add
    for hardware-accelerated texture sampling on CUDA devices,
    Includes CUDA interop APIs for array↔texture copies and surface handle access
    - Add
    while keeping libmathdx available for Cholesky/FFT (GH-1228).
    - Add subscript-style type hints for array and tile types (e.g.,
    - Add support for
    for element-wise and broadcast multiplication (GH-1006).
    for element-wise and broadcast division (GH-1009).
    - Add differentiability support for
    - Add optional
    to ensure FFI calls are always executed by JAX (GH-1240).
    including software versions, CUDA info, build flags, and devices (GH-1221).
    to query CUDA versions
    ) suffixes to the
    for CUDA devices (GH-1243).
    - Add quaternion and spatial transformation helpers (
    ) on GPU. Only floating-point types are supported;
    falls back to exact arithmetic on CPU (GH-1199).
    - Add public API for marching cubes lookup tables as class attributes on
    for advanced use cases like sparse volume extraction (GH-1151).
    to the public API for graph coloring (GH-1145).
    : Add B-spline shape functions with
    (3D), supporting degrees 1-3. Use via
    skipping CUDA toolkit detection and
    - Remove deprecated support for constructing matrices from vectors via
    at the Python and kernel scopes
    : Remove the deprecated
    - Deprecate Python 3.9 support. A
    when using Python 3.9. Support will be removed in Warp 1.13.
    - Deprecate the implicit conversion of scalar values to composite types (vectors, matrices, etc.)
    : Add deprecation warnings for the
    (scheduled for removal in 1.14).
    - Breaking: Return Warp scalar types (
    ) continue to return Python
    - Allow NVRTC compilation without a CUDA driver, enabling
    particularly when source arrays fit within L2 cache (GH-1239).
    by passing a tuple of 2D arrays
    - Change
    - Fix kernel code generation silently ignoring invalid namespace paths
    - Fix
    support for assigning register tiles (e.g.,
    and fix reverse-mode gradients for overwritten destinations (GH-1232).
    causing wrong kernel execution (GH-1211).
- Compare 摘要: v1.11.1 -> v1.12.0
  - commits: 440
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 18294
  - deletions: 16115
  - top directories: .coderabbit.yml, .github, .gitignore, .gitlab-ci.yml, .gitlab, .pre-commit-config.yaml
  - representative files:
    - docs/modules/functions.rst (removed, +0/-7928)
    - warp/__init__.pyi (modified, +2501/-1788)
    - warp/_src/builtins.py (modified, +2734/-1397)
    - exts/omni.warp/docs/CHANGELOG.md (modified, +3/-1902)
    - warp/_src/context.py (modified, +1516/-266)
    - uv.lock (modified, +1141/-497)
    - .gitlab-ci.yml (modified, +1031/-0)
    - docs/generate_reference.py (added, +755/-0)

### v1.11.1
- 标题: v1.11.1
- 类型: 正式版
- 发布时间: 2026-02-04 05:20:35 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.11.1
- GitHub release body:
# Warp v1.11.1

Warp v1.11.1 is a bugfix release following v1.11.0. For a complete list of changes, see the [changelog](https://github.com/NVIDIA/warp/blob/v1.11.1/CHANGELOG.md).

## Highlights

This is primarily a bugfix release with no major new features. Key fixes include:

- **Tile Operations**: Fixed `wp.tile_matmul()` sometimes producing NaN results when using the `c = wp.tile_matmul(a, b)` form due to reading uninitialized output memory (#1180). Also fixed tile multiplication with scalar constants when one operand is a vector or matrix type (#1175), and enabled scalar, vector, and matrix arguments in `wp.tile_map()` (#1136).

- **Code Generation**: Fixed `wp.static()` incorrectly resolving loop variables to same-named global Python variables when used for static loop unrolling in kernels (e.g., `wp.static(i)` inside `for i in range(n)` would use a global `i` if one existed, instead of the loop iteration value) (#1139). Also fixed a segfault in conditional expressions (ternary `if`/`else`) when one branch accesses an array element and the other branch is taken.

- **CUDA Graphs**: Fixed CUDA graphs with multiple temporary allocations using more memory than necessary. Previously, memory freed during graph capture wasn't properly sequenced for reuse by later allocations, causing memory to accumulate (e.g., three sequential 1GB allocations would consume 3GB instead of reusing the same 1GB).

- **Developer Experience**: Fixed `@wp.func` decorated functions showing generic `_Wrapped` types in Pyright/Pylance instead of their actual signatures on Python 3.10+. Also fixed multiple issues with IDE autocomplete stubs that caused type checker errors in mypy and Pyright, including incorrect `@overload` usage, shadowed `bool` type references, and missing `Literal[]` syntax...
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/blob/v1.11.1/CHANGELOG.md
    warp/CHANGELOG.md at v1.11.1 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    2175 lines (1855 loc) · 140 KB
    - Fix
    - Fix tile * constant multiplication when one operand is a vector or matrix type (GH-1175).
    - Fix CPU kernel assertions in debug mode not aborting the program.
    incorrectly capturing global Python variables instead of loop variables when used inside for-loops
    - Fix excessive memory usage in CUDA graphs with multiple allocations/deallocations
    - Fix a segfault in conditional expressions (ternary
    and the other branch is taken (GH-1094).
    support for kernels involving arrays with data types
    other than single-precision floats (GH-1113).
    - Raise a clear error when a kernel has a return type annotation (GH-1109).
    signatures on Python 3.10+ (GH-1163).
    - Fix IDE autocomplete stubs to show all valid signatures for functions that have both Python API
    definitions where appropriate (GH-1156).
    - Fix JAX FFI deadlock when using cached graphs across multiple GPUs
    - Fix inverted
    retain stale values instead of being set to zero (GH-1170).
    - Add
    - Add a Random Number Generation section to the runtime documentation, describing seed management strategies
    to avoid correlated random number sequences (GH-1043).
    - Add missing docstrings across the API Reference and Language Reference documentation, including built-in
    - Add group-aware construction and queries for
    to support multi-environment workloads,
    - Add tiled query functions for cooperative thread-block parallel queries in tiled kernels on CUDA devices.
    ) are also available (GH-1005).
    for ray any-hit queries with group-aware support
    - Add a
    ray–triangle intersection counting (GH-938).
    - Add in-place variants of tile linear algebra functions to reduce shared memory usage in kernels:
    - Add support for
    to support generating tiles of random numbers
    decorator to specify CUDA
    or a tuple of 1-2 integers for
    - Add type introspection functions to query Warp types (e.g.,
    - Add support for the unpack operator (
    and 1D array slices into individual arguments, enabling syntax like
    kernel compile time and runtime performance. Can be configured globally or per-module. Currently only affects
    kernels compiled for GPU devices (GH-1084).
    - Add support for parallel module compilation and loading via
    - Add support forprecompiled headersin CUDA compilation,
    - Add staged graph capture modes (
    re-capturing graphs when input/output buffer addresses change between calls
    - Drop support for Python 3.8. Python 3.9 is now the minimum supported version
    - Remove
    (deprecated since 1.8.1).
- Compare 摘要: v1.11.0 -> v1.11.1
  - commits: 79
  - files changed: 168
  - additions: 10057
  - deletions: 7616
  - top directories: .github, .gitlab-ci.yml, .gitlab, .pre-commit-config.yaml, AGENTS.md, CHANGELOG.md
  - representative files:
    - warp/__init__.pyi (modified, +1788/-1686)
    - warp/_src/builtins.py (modified, +1967/-1289)
    - exts/omni.warp/docs/CHANGELOG.md (modified, +3/-2014)
    - warp/_src/types.py (modified, +433/-269)
    - warp/_src/context.py (modified, +486/-90)
    - warp/native/tile.h (modified, +306/-231)
    - .gitlab-ci.yml (modified, +127/-204)
    - warp/examples/optim/example_particle_repulsion.py (added, +327/-0)

### v1.11.0
- 标题: v1.11.0
- 类型: 正式版
- 发布时间: 2026-01-02 21:26:06 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.11.0
- GitHub release body:
# Warp v1.11.0

Warp v1.11 introduces group-aware spatial queries for multi-world workloads, provides new options for managing JIT compilation overhead, and expands differentiation capabilities with `wp.grad()`. This release also includes expanded tile operations, the unpack operator in kernels, C++ integration examples, and a major API cleanup clarifying public versus internal interfaces.

## New features

### Group-aware spatial queries

Warp v1.11 introduces group-aware construction and queries for `wp.Bvh` and `wp.Mesh` data structures, enabling efficient spatial queries across multiple independent environments. This feature allows you to build a single acceleration structure containing geometry from multiple worlds or scenes, then query each world independently without traversing primitives from other worlds.

When constructing a BVH or Mesh, assign each primitive to a group using the `groups` parameter. Warp builds isolated sub-trees for each group within a unified structure:

```python
# Build a BVH in Python containing multiple worlds
lowers = wp.array(...)  # Shape bounds for all worlds
uppers = wp.array(...)
world_ids = wp.array([0, 0, 1, 1, 2, 2, ...], dtype=int)

bvh = wp.Bvh(lowers, uppers, groups=world_ids)

@wp.kernel
def raycast_world(
    bvh_id: wp.uint64,
    world_id: int,
    ray_origin: wp.vec3,
    ray_dir: wp.vec3
):
    # Get the root node for this world's sub-tree
    root = wp.bvh_get_group_root(bvh_id, world_id)

    # Query only intersects geometry from this world
    query = wp.bvh_query_ray(bvh_id, ray_origin, ray_dir, root)

    # Process hits
    shape_idx = int(0)
    while wp.bvh_query_next(query, shape_idx):
        # Handle intersection with shape_idx
        pass

# Launch kernel to query world 2
wp.launch(raycast_world, dim=1, i...
- Compare 摘要: v1.10.1 -> v1.11.0
  - commits: 400
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 14243
  - deletions: 12414
  - top directories: .clang-format, .coderabbit.yml, .github, .gitignore, .gitlab-ci.yml, .gitlab
  - representative files:
    - docs/modules/functions.rst (removed, +0/-7088)
    - uv.lock (modified, +1165/-1814)
    - warp/_src/builtins.py (modified, +1814/-397)
    - warp/__init__.pyi (modified, +1283/-266)
    - warp/_src/context.py (modified, +668/-235)
    - docs/generate_reference.py (added, +735/-0)
    - warp/_src/codegen.py (modified, +548/-161)
    - docs/api_reference/warp.rst (added, +550/-0)

### v1.10.1
- 标题: v1.10.1
- 类型: 正式版
- 发布时间: 2025-12-01 21:13:27 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.10.1
- GitHub release body:
# Warp v1.10.1

Warp v1.10.1 is a bugfix release following v1.10.0. For a complete list of changes, see the [changelog](https://github.com/NVIDIA/warp/blob/v1.10.1/CHANGELOG.md).

## Highlights

This is primarily a bugfix release with no major new features. Key fixes include:

- **Module reuse with `module="unique"`**: Fixed kernels using `@wp.kernel(module="unique")` to properly reuse existing module objects when the kernel is defined multiple times, avoiding unnecessary module creation overhead.
- **Kernel-local arrays**: Fixed several issues with arrays created using `wp.zeros()` inside kernels, including `.ptr` access, indexing for subarrays, and accepting single integers for the `shape` parameter.
- **Custom gradients**: Fixed a code-generation ordering bug that could prevent custom gradient functions (`@wp.func_grad`) from compiling when used with nested function calls.
- **FEM improvements**: Fixed invalid reads when using `wp.fem.TemporaryStore` during tape capture and resolved reference cycles in `wp.fem.Temporary` and `wp.fem.ShapeBasisSpace`.

## Announcements

### Upcoming removals

The following feature is deprecated and will be removed in **v1.11** (planned for January 2026):

- **`graph_compatible` parameter in `jax_callable()`**: The boolean `graph_compatible` flag has been deprecated in favor of the new `graph_mode` parameter which accepts `GraphMode` enum values. Use `GraphMode.JAX`, `GraphMode.WARP`, or `GraphMode.NONE` instead.

  ```python
  # Deprecated (v1.10.1, will be removed in v1.11)
  callable = wp.jax_experimental.jax_callable(func, graph_compatible=True)

  # Use instead
  from warp.jax_experimental import GraphMode
  callable = wp.jax_experimental.jax_callable(func, graph_mode=GraphMode.JAX)
  ```

### Platform support

- **Python 3.8**...
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/blob/v1.10.1/CHANGELOG.md
    warp/CHANGELOG.md at v1.10.1 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    2018 lines (1714 loc) · 128 KB
    - Fix type inference errors when passing reference arguments (such as array elements) to built-in functions
    - Fix
    avoiding unnecessary module creation overhead (GH-995).
    - Fix for loops containing
    ensure loop variables are available as compile-time constants within static
    - Add validation in
    - Fix compilation error in
    - Fix multiple issues with kernel-local arrays (arrays created with
    - Fix shape parameter to accept a single integer (e.g.,
    - Fix code-generation ordering for custom gradient functions (
    - Fix invalid reads when using
    - Fix reference cycles introduced by
    - Improve documentation and error messages about requiring a BVH for
    - Add more examples to the Tiles and SIMT code documentation, demonstrating caveats when switching between
    - Add an in-place
    captured in CUDA graphs (GH-826).
    - Add atomic bitwise operations
    - Add
    - Add support for error functions:
    , which fills a tile with a constant value (GH-973).
    - Add axis-reduction overloads for
    , demonstrating how to implement a Monte Carlo Laplace solver.
    - Add support for recording and waiting for external events in CUDA graphs
    - Add support for querying CPU memory information (requires
    to query supported CUDA compute architectures for compilation targets
    - Add runtime version verification to detect native library mismatches.
    - Add kernel-level functions
    - Add adjoint for
    - Add a double-precision overload for
    - Add support for
    - Add automatic differentiation support with
    - Add support for limiting the graph cache size of JAX callables (GH-989).
    - Add PyTorch-Warp interop deferred gradient allocation case study to documentation
    - Remove
    package with a new API. For migration guidance, see theNewton migration guideand the original GitHub announcement
    - Remove support for passing lists, tuples, and other non-Warp array arguments when calling built-ins at the Python
    scope (deprecated since v0.11.0). Use explicit type constructors instead (e.g.,
    - Remove support for Intel-based macOS (x86_64). Apple Silicon-based Macs (ARM64) continue to be supported with the CPU
    directing them to use Warp 1.9.x or earlier
    (deprecated since 1.7). Use
    - Remove the
    - Deprecate constructing a matrix from vectors at the Python scope (e.g.
    wp.mat22(wp.vec2(1, 2), wp.vec2(3, 4))
    wp.matrix_from_rows(wp.vec2(1, 2), wp.vec2(3, 4))
- Compare 摘要: v1.10.0 -> v1.10.1
  - commits: 53
  - files changed: 69
  - additions: 3349
  - deletions: 712
  - top directories: .gitlab-ci.yml, .gitlab, CHANGELOG.md, PUBLICATIONS.md, README.md, VERSION.md
  - representative files:
    - warp/tests/test_coloring.py (added, +542/-0)
    - warp/tests/aot/test_module_aot.py (added, +478/-0)
    - warp/tests/test_grad_customs.py (modified, +300/-0)
    - warp/tests/test_module_aot.py (removed, +0/-287)
    - warp/_src/context.py (modified, +200/-17)
    - warp/tests/test_unique_module.py (added, +196/-0)
    - asv/benchmarks/atomics.py (added, +168/-0)
    - warp/_src/build_dll.py (modified, +141/-25)

### v1.10.0
- 标题: v1.10.0
- 类型: 正式版
- 发布时间: 2025-11-02 22:11:50 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.10.0
- GitHub release body:
# Warp v1.10.0

Warp v1.10 expands JAX integration with automatic differentiation support and multi-device `jax.pmap()` compatibility. The tile programming model has been enhanced with axis-specific reductions, component-level indexing, and convenience functions for creating tiles.

Performance has been significantly improved in several areas: BVH operations now support in-place rebuilding for CUDA graphs and configurable leaf sizes, built-in function calls from Python are up to 70× faster, and additional sparse matrix and FEM operations can now be captured in CUDA graphs.

Additional usability improvements include negative indexing and slicing for arrays, atomic bitwise operations, and new built-in functions including error functions and type casting.

**Important**: This release removes the `warp.sim` module (deprecated since v1.8), which has been superseded by the [Newton physics engine](https://github.com/newton-physics/newton). See the Announcements section below for migration guidance and other upcoming changes.

For a complete list of changes, see the [full changelog](https://github.com/NVIDIA/warp/blob/v1.10.0/CHANGELOG.md).

## New features

### JAX automatic differentiation (experimental)

Warp now supports experimental automatic differentiation with JAX, allowing kernels to participate in JAX automatic differentiation workflows. This feature is contributed by @mehdiataei and builds on earlier work by @jaro-sevcik. It enables computing gradients through Warp kernels using `jax.grad()` by passing `enable_backward=True` to `jax_kernel()`.

Key capabilities include:

- **Single and multiple output kernels**: Compute gradients for kernels with one or more output arrays
- **Static input auto-detection**: Scalar inputs are automatically treated as static (non-dif...
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/blob/v1.10.0/CHANGELOG.md
    warp/CHANGELOG.md at v1.10.0 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    1982 lines (1683 loc) · 126 KB
    - Add an in-place
    captured in CUDA graphs (GH-826).
    - Add atomic bitwise operations
    - Add
    - Add support for error functions:
    , which fills a tile with a constant value (GH-973).
    - Add axis-reduction overloads for
    , demonstrating how to implement a Monte Carlo Laplace solver.
    - Add support for recording and waiting for external events in CUDA graphs
    - Add support for querying CPU memory information (requires
    to query supported CUDA compute architectures for compilation targets
    - Add runtime version verification to detect native library mismatches.
    - Add kernel-level functions
    - Add adjoint for
    - Add a double-precision overload for
    - Add support for
    - Add automatic differentiation support with
    - Add support for limiting the graph cache size of JAX callables (GH-989).
    - Add PyTorch-Warp interop deferred gradient allocation case study to documentation
    - Remove
    package with a new API. For migration guidance, see theNewton migration guideand the original GitHub announcement
    - Remove support for passing lists, tuples, and other non-Warp array arguments when calling built-ins at the Python
    scope (deprecated since v0.11.0). Use explicit type constructors instead (e.g.,
    - Remove support for Intel-based macOS (x86_64). Apple Silicon-based Macs (ARM64) continue to be supported with the CPU
    directing them to use Warp 1.9.x or earlier
    (deprecated since 1.7). Use
    - Remove the
    - Deprecate constructing a matrix from vectors at the Python scope (e.g.
    wp.mat22(wp.vec2(1, 2), wp.vec2(3, 4))
    wp.matrix_from_rows(wp.vec2(1, 2), wp.vec2(3, 4))
    - Breaking:Change the default implementation of
    , but it is not supported
    with JAX v0.8 and newer (GH-974).
    - Breaking:Raise
    any Warp kernels, functions, or structs (GH-920).
    - Improve performance when calling built-in functions from the Python scope
    - Improve efficiency of struct instance creation and attribute access (GH-968).
    for performance tuning. The default is now 1 for
    , changed from a hardcoded value of
    enabling CUDA subgraph capture for
    geometry and function space partitions is now possible in CUDA graphs by passing an explicit
    - Improve efficiency for
    This fixes a performance regression introduced in Warp 1.6.0 (GH-758).
    - Fix segmentation faults on AArch64 CPUs when using tiles. The fix uses stack memory for tile storage
- Compare 摘要: v1.9.1 -> v1.10.0
  - commits: 385
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 13210
  - deletions: 7381
  - top directories: .github, .gitignore, .gitlab-ci.yml, .gitlab, .pre-commit-config.yaml, CHANGELOG.md
  - representative files:
    - uv.lock (added, +3823/-0)
    - warp/__init__.pyi (modified, +2302/-307)
    - docs/modules/functions.rst (modified, +1003/-215)
    - warp/_src/autograd.py (added, +1077/-0)
    - asv/benchmarks/spatial_query.py (added, +693/-0)
    - docs/modules/interoperability.rst (modified, +535/-152)
    - exts/omni.warp/omni/warp/nodes/_impl/OgnClothSimulate.py (removed, +0/-673)
    - exts/omni.warp/omni/warp/nodes/_impl/OgnParticlesSimulate.py (removed, +0/-593)

### v1.9.1
- 标题: v1.9.1
- 类型: 正式版
- 发布时间: 2025-10-01 15:37:06 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.9.1
- GitHub release body:
# Warp v1.9.1

Warp 1.9.1 is a bugfix release that follows our recent feature update. For a full list of changes, see the [changelog](https://github.com/NVIDIA/warp/blob/v1.9.1/CHANGELOG.md).

## Highlights

- **GPU Compatibility**: Support for older NVIDIA GPU architectures (Maxwell, Pascal, Volta) was unintentionally dropped in the pre-built wheels distributed for Warp 1.9.0 on PyPI. These architectures have been added back.
- **Documentation Improvements**: We have corrected the documentation for `wp.mesh_query_aabb()` and `wp.mesh_query_aabb_next()`, added a caveat concerning the use of `__cuda_array_interface__` on a system with multiple GPUs, and fixed the labeling of built-in functions that were incorrectly labeled as differentiable.
- **Corrected Slice Behavior**: Empty slices (e.g. `arr[i:i]`) are now handled correctly at the Python scope, returning an empty array instead of raising an error.
- **Tile Stability and Correctness**: A critical memory management issue with shared tiles has been fixed to prevent unpredictable crashes and memory leaks. Additionally, functions like `wp.copy()` and `wp.where()` now work with tiles and compute correct gradients (adjoints).
- **Tuple Type Hints**: Resolved a `TypeError` that occurred when using modern tuple type hints (e.g., `tuple[int, int]`) with `@wp.func`-decorated functions on Python 3.9 and 3.10.

## Announcements

### Known limitations

- **CPU Kernels on ARM**: Launching CPU kernels on Linux ARM systems, such as NVIDIA Jetson Thor and Grace Hopper, may result in segmentation faults. A fix for this issue is planned for the v1.10 release. GPU kernels are not affected.

### Upcoming removals

The following features have been deprecated in prior releases and will be removed in v1.10 (early November):

- `warp.sim`...
- 外链文档摘录:
  - https://github.com/NVIDIA/warp/blob/v1.9.1/CHANGELOG.md
    warp/CHANGELOG.md at v1.9.1 · NVIDIA/warp · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork557
    1868 lines (1580 loc) · 117 KB
    - Add documentation describing Python
    - Fix crash when radix sort is used on multiple streams (e.g., when using hash grids on multiple streams)
    - Fix empty slice operations
    - Fix
    with tuple type annotations on Python 3.10
    - Fix memory management issues with shared tiles, including double frees and memory leaks
    - Fix use of
    - Fix invalid
    - Restore support for older GPU architectures (Maxwell, Pascal, Volta) when building with CUDA 12
    - Fix conditional graph compilation on newer GPU architectures by using PTX fallback when CUBIN is not supported
    - Fix scaling not being correctly applied to rendered meshes in some cases
    - Fix handling of generic kernels with
    - Add support for building Warp with CUDA 13.
    - Add
    to extract a triangular mesh from a 3D scalar field
    to support basic ahead-of-time compilation workflows
    - Add support for retrieving the memory address of a Warp array in kernels as
    - Add support for using struct types in the
    - Add support for initializing fixed-size arrays inside kernels using
    - Add support for
    inside Warp kernels (GH-529).
    for performance optimization. When set to
    improving performance (defaults to
    - Add optional
    - Add support for displaying and editing Warp vector and array types in ImGui
    - Remove support for building Warp with CUDA 11.
    - Deprecate support for Intel-based macOS (x86_64) with removal targeted in late 2025.
    We will continue to support Apple Silicon-based Macs with the CPU backend.
    - Enforce strict argument matching for user-function calls from the Python scope, mirroring built-in function behavior.
    prefix for all exported, C-style symbols to prevent name conflicts
    in pure Warp for cross-platform support and differentiability
    computations when beneficial (GH-838).
    in CUDA kernels on Linux systems. This feature is not supported on Windows due to
    CUDA-GDB Linux-target-only support (GH-795).
    - Define and re-export Warp's public Python-scope API in
    using typing re-export conventions to improve
    static type checker support (GH-864).
    - Improve error messages for MathDx-based tile operations that fail to compile (e.g.,
    Failed to compile LTO
    - Improve error detection and reporting in conditional graphs (GH-866).
    - Fix ARM64 CPU kernel argument passing issues by packaging arguments into a structure to work around a
    implementations missing for scalar types at the Python scope
    - Fix issue with calling user functions from the Python scope with
    - Fix 2D shared tile allocation/de-allocation bug inside Warp functions
- Compare 摘要: v1.9.0 -> v1.9.1
  - commits: 33
  - files changed: 55
  - additions: 3771
  - deletions: 578
  - top directories: .gitlab-ci.yml, .gitlab, CHANGELOG.md, PUBLICATIONS.md, README.md, VERSION.md
  - representative files:
    - warp/__init__.pyi (modified, +1420/-2)
    - warp/tests/interop/test_jax.py (modified, +608/-28)
    - warp/build_dll.py (modified, +322/-72)
    - warp/builtins.py (modified, +289/-23)
    - warp/context.py (modified, +243/-32)
    - docs/modules/functions.rst (modified, +36/-177)
    - warp/native/tile.h (modified, +188/-13)
    - warp/tests/test_tuple.py (modified, +96/-0)

### v1.9.0
- 标题: v1.9.0
- 类型: 正式版
- 发布时间: 2025-09-05 11:54:40 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.9.0
- GitHub release body:
Warp 1.9 ships with a rewritten marching cubes implementation, compatibility with the CUDA 13 toolkit, and new functions for ahead-of-time module compilation. The programming model has also been enhanced with more flexible indexing for composite types, direct `IntEnum` support, and the ability to initialize local arrays in kernels.

## New Features

### Differentiable marching cubes

A fully differentiable `wp.MarchingCubes` implementation, contributed by @mikacuy and @nmwsharp, has been added. This version is written entirely in Warp, replacing the previous native CUDA C++ implementation and enabling it to run on both CPU and GPU devices. The implementation also addresses a long-standing off-by-one bug (#324). For more details, see the [updated documentation](https://nvidia.github.io/warp/modules/runtime.html#marching-cubes).

### Functions for module compilation and loading

We have added `wp.compile_aot_module()` and `wp.load_aot_module()` for more flexible ahead-of-time (AOT) compilation.

These functions include a `strip_hash=True` argument, which removes the unique hashes from compiled module and function
names. This change makes it possible to distribute pre-compiled modules without shipping the original Python source code.

See the documentation on [ahead-of-time compilation workflows](https://nvidia.github.io/warp/codegen.html#ahead-of-time-compilation-workflows) for more details. In future releases, we plan to continue to expand Warp's support for ahead-of-time workflows.

## CUDA 13 Support

[CUDA Toolkit 13.0](https://developer.nvidia.com/blog/whats-new-and-important-in-cuda-toolkit-13-0/) was released in early August.

**PyPI Distribution**: Warp wheels on PyPI and NVIDIA PyPI will continue to be built with CUDA 12.8 to provide a transition period for us...
- Compare 摘要: v1.9.0rc1 -> v1.9.0
  - commits: 22
  - files changed: 37
  - additions: 804
  - deletions: 323
  - top directories: .gitignore, .gitlab-ci.yml, CHANGELOG.md, README.md, VERSION.md, docs/_static
  - representative files:
    - docs/installation.rst (modified, +175/-0)
    - docs/modules/runtime.rst (modified, +153/-7)
    - README.md (modified, +24/-61)
    - docs/index.rst (modified, +54/-29)
    - docs/codegen.rst (modified, +49/-28)
    - CHANGELOG.md (modified, +39/-34)
    - exts/omni.warp.core/docs/CHANGELOG.md (modified, +40/-32)
    - exts/omni.warp/docs/CHANGELOG.md (modified, +40/-32)

### v1.9.0rc1
- 标题: v1.9.0rc1
- 类型: 预发布版
- 发布时间: 2025-08-20 23:59:11 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.9.0rc1
- GitHub release body:
Release candidate for Isaac Lab testing.
- Compare 摘要: v1.8.1 -> v1.9.0rc1
  - commits: 287
  - files changed: 221
  - additions: 14064
  - deletions: 6112
  - top directories: .coderabbit.yml, .github, .gitlab-ci.yml, .gitlab, CHANGELOG.md, PUBLICATIONS.md
  - representative files:
    - warp/native/exports.h (modified, +1842/-1908)
    - warp/context.py (modified, +1360/-800)
    - warp/native/mat.h (modified, +1911/-117)
    - warp/native/nanovdb/NanoVDB.h (modified, +517/-895)
    - warp/builtins.py (modified, +959/-138)
    - warp/marching_cubes.py (added, +708/-0)
    - warp/__init__.pyi (modified, +486/-111)
    - warp/codegen.py (modified, +327/-209)

### v1.8.1
- 标题: v1.8.1
- 类型: 正式版
- 发布时间: 2025-08-02 01:41:44 CST
- 链接: https://github.com/NVIDIA/warp/releases/tag/v1.8.1
- GitHub release body:
This patch release primarily contains bug fixes as expected.

However, to support the adoption of Warp by the MuJoCo MJX physics engine, it also includes new features and deprecations limited to the `jax_experimental` module. We are flagging this deviation from our standard versioning practices to ensure clarity. Normal versioning practices will resume with the next release.

## Full  Changelog

### Deprecated

- This is the final release that will provide builds for or support the CUDA 11.x Toolkit and driver. Starting with v1.9.0, Warp will require CUDA 12.x or newer.
- Deprecate the `graph_compatible` boolean flag in `jax_callable()` in favor of the new `graph_mode` argument with `GraphMode` enum (#848).

### Added

- Add documentation for creating and manipulating Warp structured arrays using NumPy (#852)
- Add documentation for `wp.indexedarray()` (#468).
- Support input-output aliasing in JAX FFI (#815).
- Support capturing `jax_callable()` using Warp via the new `graph_mode` parameter (`GraphMode.WARP`), enabling capture of graphs with conditional nodes that cannot be used as subgraphs in a JAX capture (#848).

### Fixed

- Fix `tape.zero()` to correctly reset gradient arrays in nested structs (#807).
- Fix incorrect adjoints for `div(scalar, vec)`, `div(scalar, mat)`, and `div(scalar, quat)`, and other miscellaneous issues with adjoints (#831).
- Fix a module-hashing issue for functions or kernels using static expressions that cannot be resolved at the time of declaration (#830).
- Fix a bug in which changes to `wp.config.mode` were not being picked up after module initialization (#856).
- Fix a bug where CUDA modules could get prematurely unloaded when conditional graph nodes are used.
- Fix compile time regression for kernels using matmul, Cholesky, and FFT...
