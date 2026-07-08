# Release Roadmap Reference

- 仓库: `RLinf/RLinf`
- 对应主报告: `RLinf_RLinf_release_roadmap.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要 + tagged README/docs/examples/configs/高信号源码证据
- 版本总数: 2
- 正式版数量: 2
- 预发布版数量: 0
- 外链文档覆盖版本数: 2
- compare 摘要覆盖版本数: 1
- 最新版本: v0.2 (2026-03-26 23:06:12 CST)
- 最早纳入统计版本: v0.1 (2025-12-17 20:01:25 CST)

## 分析策略决策
- 请求模式: `auto`
- 最终策略: `L2: Source-enhanced`
- 证据充分性评分: 1/6
- 触发规则: release_count_low
- 决策说明:
  - 仓库最近一年 release 偏少，且高价值产品信息大量分布在 README/docs/源码信号里，默认启用源码增强。
  - 证据充分性评分 1/6，触发规则: release_count_low。
  - 因此主脚本自动升级为 L2，补充 tagged README/docs/examples/configs/高信号源码证据。

## Release 时间线
- 2026-03-26 23:06:12 CST | v0.2 | 正式版
- 2025-12-17 20:01:25 CST | v0.1 | 正式版

## 证据附录

### v0.2
- 标题: RLinf v0.2 Release
- 类型: 正式版
- 发布时间: 2026-03-26 23:06:12 CST
- 链接: https://github.com/RLinf/RLinf/releases/tag/v0.2
- GitHub release body:
🎉 Introducing RLinf v0.2, our second public release.

RLinf v0.2 focuses on two major directions: **Real-World RL** and **Multi-agent RL** systems. To support these goals, RLinf now supports real-world platforms including **XSquare Turtle2 Arms** and the **Franka Arm**, while offering a richer set of embodied benchmarks, simulators, models, algorithms, together with **native asynchronous training** designed for high-throughput workloads. This release also strengthens real-world deployment, sim-to-real, and co-training workflows, alongside more robust data and replay infrastructure and improved training stability. For multi-agent training, RLinf introduces **native multi-agent support** for extensible multi-agent RL algorithms and unified data interfaces, lowering the barrier to developing and scaling multi-agent workloads while enabling rapid reproduction of advanced training solutions such as **WideSeek-R1**.

## Embodied Intelligence

#### 1. Core Capability Upgrades (Real-World Robotics RL and World Models)

- Supported Real-World RL with [XSquare Turtle2 Arms](https://rlinf.readthedocs.io/en/release-v0.2/rst_source/examples/embodied/xsquare_turtle2.html).
- Supported World Models as simulators for RL training, including [OpenSora](https://rlinf.readthedocs.io/en/release-v0.2/rst_source/examples/embodied/opensora.html), [Wan](https://rlinf.readthedocs.io/en/release-v0.2/rst_source/examples/embodied/wan.html), and [WoVR](https://rlinf.readthedocs.io/en/release-v0.2/rst_source/publications/wovr.html).
- Vision-Language Model Supervised Fine‑Tuning adds supervised fine‑tuning (SFT) capabilities for vision‑language models (VLMs), supporting efficient fine‑tuning on custom datasets. Verified on Robo2VLM, achieving approximately 95% reproduction accuracy for [PR 708](ht...
- 外链文档摘录:
  - https://rlinf.readthedocs.io/en/release-v0.2/rst_source/examples/embodied/xsquare_turtle2.html
    Real-World RL with XSquare Turtle2 — RLinf  documentation
    Real-World RL with XSquare Turtle2#
    learning training on theXSquare Turtle2dual-arm robot platform using the
    Robot: XSquare Turtle2 – a dual-arm tabletop robot with up to 2 arms (left arm ID
    ) and up to 3 RGB cameras (IDs
    Task: Currently we support thebutton-pressingtask (
    Random resets add ±5 cm position noise and ±20° orientation noise to increase difficulty.
    RGB images (128 × 128) from one or more cameras, returned as
    Action Space: 7-dimensional continuous action per arm, stacked for dual-arm use:
    3D delta position (Δx, Δy, Δz)
    3D delta orientation (Δroll, Δpitch, Δyaw)
    A SAC variant that removes the target Q-network.
    Robot: XSquare Turtle2 dual-arm robot
    Cameras: Up to 3 RGB cameras mounted on the robot (IDs 0–2)
    Training / Rollout Node: A computer with GPU support for running the CNN policy
    The XSquare Turtle2 platform ships with its own SDK and ROS-based controller stack.Please ensure that you have entered the official Docker container of Xsquare before starting the following installation.. ContactXSquarefor the exact Docker image and startup instructions.
    # For mainland China users, you can use the following for better download speed:# git clone https://ghfast.top/github.com/RLinf/RLinf.gitgitclonehttps://github.com/RLinf/RLinf.gitcdRLinf
    Then install the RLinf Python dependencies for the embodied real-world setup:
    # For mainland China users, you can add the `--use-mirror` flag for better speed.bashrequirements/install.shembodied--envxsquare_turtle2source.venv/bin/activate
    Option 1: Docker Image
    # use maniskill_libero image for training / rollout nodesdockerrun-it--rm--gpusall\--shm-size20g\--networkhost\--namerlinf\-v.:/workspace/RLinf\rlinf/rlinf:agentic-rlinf0.2-maniskill_libero# For mainland China users, you can use the following for better download speed:# docker.1ms.run/rlinf/rlinf:agentic-rlinf0.2-maniskill_libero
    Option 2: Custom Environment
    # install openvla + maniskill_libero environment on training / rollout nodes# For mainland China users, you can add the `--use-mirror` flag for better speed.bashrequirements/install.shembodied--modelopenvla--envmaniskill_liberosource.venv/bin/activate
    # Method 1: Using git clonegitlfsinstall
    gitclonehttps://huggingface.co/RLinf/RLinf-ResNet10-pretrained# Method 2: Using huggingface-hub# For mainland China users:# export HF_ENDPOINT=https://hf-mirror.compipinstallhuggingface-hub
    a node, the current Python interpreter and environment variables are recorded and
    Source the correct virtual Python environment (see Dependency Installation above).
    exportPYTHONPATH=<path_to_your_RLinf_repo>:$PYTHONPATHexportRLINF_NODE_RANK=<node_rank_of_this_node>exportRLINF_COMM_NET_DEVICES=<network_device># Optional if only one NIC
    # On the head node (node rank 0)raystart--head--port=6379--node-ip-address=<head_node_ip_address># On worker nodes (node rank 1 ~ N-1)raystart--address='<head_node_ip_address>:6379'
    cluster:num_nodes:2# 1 training/rollout node + 1 controller nodecomponent_placement:actor:node_group:"gpu"placement:0rollout:node_group:"gpu"placement:0env:node_group:turtle2placement:0node_groups:-label:"gpu"node_ranks:0-label:turtle2node_ranks:1hardware:type:Turtle2configs:-node_rank:1env:train:override_cfg:is_dummy:Falseuse_arm_ids:[1]# 0=left arm, 1=right arm; use [0,1] for dual armuse_camera_ids:[2]# camera IDs to use (0, 1, or 2)target_ee_pose:# [[left_arm_pose], [right_arm_pose]], Euler [x,y,z,rz,ry,rx]-[0,0,0,0,0,0]-[0.3,0.0,0.15,0.0,1.0,0.0]actor:model:model_path:"/path/to/RLinf-ResNet10-pretrained"state_dim:6# 6 for single arm (xyz+euler); 12 for dual armaction_dim:6# 6 for single arm (xyz_delta+rpy_delta); 12 for dual armrollout:model:model_path:"/path/to/RLinf-ResNet10-pretrained"
    2. Key Metrics Tracked
    : Whether the robot succeeded at least once in the episode (0 or 1).
  - https://rlinf.readthedocs.io/en/release-v0.2/rst_source/examples/embodied/opensora.html
    Policy Improvement: Leveraging “imagined” trajectories generated by OpenSora to optimize the VLA policy using reinforcement learning methods such as PPO.
    Task: Command a 7-DoF robotic arm to perform a variety of household manipulation skills (pick-and-place, stacking, opening drawers, spatial rearrangement)
    Action Space: 7-dimensional continuous actions
    - 3D end-effector position control (x, y, z)
    - 3D rotation control (roll, pitch, yaw)
    Rewards: Provided by the reward classifier in the world model, ranging from 0 to 1
    1. Clone RLinf Repository#
    # For mainland China users, you can use the following for better download speed:# git clone https://ghfast.top/github.com/RLinf/RLinf.gitgitclonehttps://github.com/RLinf/RLinf.gitcdRLinf
    Option 1: Docker Image
    dockerrun-it--rm--gpusall\--shm-size20g\--networkhost\--namerlinf\-v.:/workspace/RLinf\rlinf/rlinf:agentic-rlinf0.2-opensora# For mainland China users, you can use the following for better download speed:# docker.1ms.run/rlinf/rlinf:agentic-rlinf0.2-opensora
    Option 2: Custom Environment
    # For mainland China users, you can add the `--use-mirror` flag to the install.sh command for better download speed.bashrequirements/install.shembodied--modelopenvla-oft--envopensorasource.venv/bin/activate
    # Download the model (choose either method)# Method 1: Using git clonegitlfsinstall
    gitclonehttps://huggingface.co/Haozhan72/Openvla-oft-SFT-libero10-traj1# Method 2: Using huggingface-hub# For mainland China users, you can use the following for better download speed:# export HF_ENDPOINT=https://hf-mirror.compipinstallhuggingface-hub
    rollout:model:model_path:Pathto/RLinf/RLinf-OpenVLAOFT-LIBERO-90-Base-Loraactor:model:model_path:Pathto/RLinf/RLinf-OpenVLAOFT-LIBERO-90-Base-Loraunnorm_key:libero_90_no_noops_trajall# or libero_130_no_noops_trajall for the RLinf-OpenVLAOFT-LIBERO-130-Base-Lora model
    In addition to the VLA model, you need to download the OpenSora weights and the dataset for simulation initialization.
    # Download the weights and initialization data# Method 1: Using git clonegitlfsinstall
    gitclonehttps://huggingface.co/RLinf/RLinf-OpenSora-LIBERO-Object# Method 2: Using huggingface-hubpipinstallhuggingface-hub
    ├── model-00001.safetensors              # World model weight files
    Please ensure you have activated the correct Python virtual environment (venv) before running the commands below.
    1. Key Parameters Configuration
    actor:model:model_path:"/path/to/model/Openvla-oft-SFT-libero-spatial-traj1/"# SFT model pathmodel_type:"openvla_oft"# Model type set to openvla_oftuse_proprio:False# Whether to use proprioceptive inputsnum_images_in_input:1# Number of input imagesnum_action_chunks:8# Number of action chunksunnorm_key:"libero_spatial_no_noops"# Action normalization key (match SFT). For RLinf-OpenVLAOFT-LIBERO-130-Base-Lora model, use libero_130_no_noops_trajall. For RLinf-OpenVLAOFT-LIBERO-90-Base-Lora model, use libero_90_no_noops_trajall.
    It is worth noting that since the world model does not provide proprioception, does not generate a wrist view, and uses a fixed chunk length,
    defaults to 1, and
    # Override in CHOSEN_CONFIG# Recommend opensora_libero_spatial for training and libero_spatial for evaluationenv/train:opensora_libero_spatialenv/eval:libero_spatialenv:train:opensora_wm_hf_ckpt_path:/Pathto/model/RLinf-OpenSora-LIBERO-Spatial/# In env/train/opensora_libero_spatial.yaml:env_type:opensora_wmwm_env_type:libero# Initial image path for world model initializationinitial_image_path:${env.train.opensora_wm_hf_ckpt_path}/dataset_for_rlinf_world_model_init/base_policy_rollout_buffer# It is not recommended to modify any parameters in world_model_cfgworld_model_cfg:# Path to dataset statistics for normalization in the world modelstats_path:/Pathto/model/RLinf-OpenSora-LIBERO-Spatial/best_wm_ckpt/base_policy/dataset_statistics.jsonchunk:8# Align with training and VLA inference length; default 8condition_frame_length:4# Align with training; context memory length, default 4model:# Pretrained weightsfrom_pretrained:/Pathto/model/RLinf-OpenSora-LIBERO-Spatial/best_wm_ckpt/base_policy/model
    We support theOpenVLA-OFTmodel with theGRPOalgorithm.
    2. Key Metrics Tracked
    : Explained variance of value function predictions; closer to 1 is better.
    : Chunk of reward (refer to L414 in libero_env.py).
    : Episode return. In LIBERO’s sparse-reward setting, this metric is not informative since the reward is almost always 0 until the terminal success step.
    : Step-level reward (0 for all intermediate steps and 1 only at successful termination).
    The logged value is normalized by the number of episode steps, which makes it difficult to interpret as real task performance during training.
    : Recommended metric to monitor training performance. It directly reflects the unnormalized episodic success rate and better represents the true performance of the policy.
    4. Train Log Tool Integration
    For each LIBERO suite, we evaluate every combination of task_id and trial_id. For the Object and Spatial...
- Compare 摘要: v0.1 -> v0.2
  - commits: 221
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 15402
  - deletions: 2713
  - top directories: .cursor, .github, .gitignore, AGENTS.md, CODE_OF_CONDUCT.md, README.md
  - representative files:
    - README.zh-CN.md (modified, +169/-476)
    - README.md (modified, +171/-471)
    - docs/source-en/rst_source/examples/embodied/robotwin.rst (added, +621/-0)
    - docs/source-en/rst_source/examples/embodied/pi0.rst (added, +572/-0)
    - docs/source-en/rst_source/examples/embodied/franka.rst (added, +551/-0)
    - .github/workflows/embodied-e2e-tests.yml (modified, +531/-2)
    - docs/source-en/rst_source/publications/wideseek_r1.rst (added, +462/-0)
    - docs/source-en/rst_source/tutorials/rlalg/async_ppo.rst (added, +446/-0)

### v0.1
- 标题: v0.1
- 类型: 正式版
- 发布时间: 2025-12-17 20:01:25 CST
- 链接: https://github.com/RLinf/RLinf/releases/tag/v0.1
- GitHub release body:
🎉 Introducing RLinf **v0.1**, our first public release.

Built on robust system-level scheduling and communication components, RLinf is a scalable and flexible framework for post-training via reinforcement learning in embodiment, reasoning, and agent scenarios. The framework has been validated on popular models and tasks and achieves state-of-the-art model performance and training throughput, showcasing its extensibility, versatility, and efficiency in diverse scenarios.

# Highlights

## System Design

- **Worker**: a flexible, schedulable abstraction for RL components, which endows components with adaptive communication and automatic resource management capabilities across heterogeneous **GPU**, **NPU**, and **CPU**, enabling LEGO-like composition of complex RL workflows.

- **Scheduler**: the manager of workers and hardware resources that enables easy scaling on large clusters, featuring **automatic GPU resource scheduling** and **dynamic scaling up/down of components**, eliminating painful tuning of GPU and parallelism configurations.

- **Channel**: an adaptive, high-performance communication utility that offers queue-like interactions among components and automatically selects the optimal communication backend (**zero-copy cudaIPC**, **NCCL**, **Gloo**, etc.) for maximum efficiency.

## Embodied RL

- Support end-to-end embodied RL training on multiple mainstream simulators (e.g., **ManiSkill**, **Libero**, **MetaWorld**, **CALVIN**), achieving **state-of-the-art performance** with multiple VLA models (e.g., **OpenVLA**, **OpenVLA-OFT**, **π₀**, **π₀.₅**, **GR00T**) and algorithms (**GRPO**, **PPO**), reaching a **success rate of up to 99%**.

- Up to **143.4% faster** training (**2.434× throughput**) compared to existing frameworks, with flexibly **allocated**...
- 外链文档摘录:
  - https://github.com/RLinf/RLinf/tree/release/v0.1/examples/embodiment
    RLinf/examples/embodiment at release/v0.1 · RLinf/RLinf · GitHub
    - NotificationsYou must be signed in to change notification settings
    - Fork578

# Tagged Repository Source Evidence

## v0.2
- README / repo positioning excerpt:
<div align="center">
<img src="https://github.com/RLinf/misc/raw/main/pic/logo_white.svg" alt="RLinf-logo" width="600"/>
</div>
<div align="center">
<a href="https://arxiv.org/abs/2509.15965"><img src="https://img.shields.io/badge/arXiv-Paper-red?logo=arxiv"></a>
<a href="https://huggingface.co/RLinf"><img src="https://img.shields.io/badge/HuggingFace-yellow?logo=huggingface&logoColor=white" alt="Hugging Face"></a>
<a href="https://rlinf.readthedocs.io/en/latest/"><img src="https://img.shields.io/badge/Documentation-Purple?color=8A2BE2&logo=readthedocs"></a>
<a href="https://rlinf.readthedocs.io/zh-cn/latest/"><img src="https://img.shields.io/badge/中文文档-red?logo=readthedocs"></a>
<a href="https://deepwiki.com/RLinf/RLinf"><img src="https://img.shields.io/badge/Ask%20DeepWiki-1DA1F2?logo=databricks&logoColor=white&color=00ADEF" alt="Ask DeepWiki"></a>
[![English](https://img.shields.io/badge/lang-English-blue.svg)](README.md)
[![简体中文](https://img.shields.io/badge/语言-简体中文-red.svg)](README.zh-CN.md)
<h1 align="center">
<sub>RLinf: Reinforcement Learning Infrastructure for Embodied and Agentic AI</sub>
</h1>
RLinf is a flexible and scalable open-source RL infrastructure designed for Embodied and Agentic AI. The 'inf' in RLinf stands for `Infrastructure`, highlighting its role as a robust backbone for next-generation training. It also stands for `Infinite`, symbolizing the system’s support for open-ended learning, continuous generalization, and limitless possibilities in intelligence development.
## What's NEW!
- [2026/03] 🔥 RLinf supports [FUSCO](https://github.com/infinigence/FUSCO) to accelerate the MoE All-to-All communication used in Megatron. Doc: [FUSCO](https://rlinf.readthedocs.io/en/latest/rst_source/examples/system/fusco.html), paper: [FUSCO: High-Performance D...
- High-signal repository paths at this tag:
  - docs/README.md
  - examples/sft/train_vla_sft.py
  - examples/sft/train_vlm_sft.py
  - examples/embodiment/collect_real_data.py
  - docs/source-en/rst_source/examples/embodied/franka.rst
  - docs/source-zh/rst_source/examples/embodied/franka.rst
  - docs/source-en/rst_source/examples/embodied/sft_vlm.rst
  - docs/source-zh/rst_source/examples/embodied/sft_vlm.rst
  - docs/source-en/rst_source/examples/embodied/opensora.rst
  - docs/source-en/rst_source/examples/embodied/robotwin.rst
  - docs/source-zh/rst_source/examples/embodied/opensora.rst
  - docs/source-zh/rst_source/examples/embodied/robotwin.rst
- Changed high-signal files against previous included release:
  - [M] docs/README.md
    Excerpt:
    # RLinf Documentations
    Welcome to the documentation for RLinf! This README provides detailed instructions on how to generate the project documentation locally using Sphinx. It covers the entire process, from setting up your environment to building and viewing the documentation. Additionally, it includes information on cleaning the build directory and an introduction to Sphinx and reStructuredText (RST).
    ---
    ## Setting Up Your Environment
    ### Step 1: Set Environment Variables
    Every time you open a new terminal session to work on the documentation, run these commands to set the locale for Sphinx:
    ```bash
    export LC_ALL=C.UTF-8
    export LANG=C.UTF-8
    These ensure proper character encoding with the `C.UTF-8` locale.
    ### Step 2: Install Dependencies
    bash requirements/install.sh docs --venv .docs-venv
    source .docs-venv/bin/activate
    ## Building the Documentation
    You can simply run the following command to build the English docs and open a server for preview and live reloading:
    To build the Chinese docs, run this:
    sphinx-build source-en build/html # change to source-zh for Chinese docs
    ## Viewing the Documentation
    ### With `sphinx-build`
    1. Go to the `build/html` directory.
    2. Open `index.html` in your browser.
    python -m http.server 8000
    Visit `http://localhost:8000` in your browser.
    ### With `sphinx-autobuild`
    Running `sphinx-autobuild` automatically hosts the documentation at `http://localhost:8000`. Open this URL to view it with live reloading.
    ## Cleaning the Build Directory
    ## Writing reStructuredText (RST)
    [RST grammer](https://zh-sphinx-doc.readthedocs.io/en/latest/rest.html)
  - [A] docs/source-en/rst_source/examples/embodied/franka.rst
    Excerpt:
    Real-World RL with Franka
    ============================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    This document provides a comprehensive guide to launching and managing the
    a CNN policy training task within the RLinf framework,
    focusing on training a ResNet-based CNN policy from scratch for robotic manipulation in the real world setup.
    The primary objective is to develop a model capable of performing robotic manipulation by:
    1. **Visual Understanding**: Processing RGB images from the robot's camera.
    2. **Action Generation**: Producing precise robotic actions (position, rotation), possibly with gripper control.
    3. **Reinforcement Learning**: Optimizing the policy via the SAC with environment feedback.
    **Real World Environment**
    - **Environment**: Real world setup.
    - Franka Emika Panda robotic arm
    - Realsense cameras
    - Possibly use spacemouse for teleoperation data collection or human intervention.
    - **Task**: Currently we support the peg-insertion task and the charger task.
    - **Observation**:
    - RGB images (128x128) from a wrist camera or a third-person camera.
    - **Action Space**: 6 or 7-dimensional continuous actions, depending on whether gripper control is included:
    - 3D position control (x, y, z)
    - 3D rotation control (roll, pitch, yaw)
    - Gripper control (open/close)
    - **Images**: RGB tensors ``[batch_size, 128, 128, 3]``
    - **Actions**: Normalized continuous values ``[-1, 1]`` for each action dimension
    - **Rewards**: Step-level rewards based on task completion
    1. **SAC (Soft Actor-Critic)**
    - Learning Q-values by Bellman backups and entropy regularization.
    - Learning policy to maximize entropy-regularized Q.
    - Learning temperature parameter for exploration-exploitation trade-off.
    2. **Cross-Q**
    - A variant of SAC...
  - [A] docs/source-en/rst_source/examples/embodied/frankasim.rst
    Excerpt:
    RL with Franka-Sim Benchmark
    ======================================================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    This document provides a complete guide to launching and managing
    **Vision-Language-Action Models (VLAs)** training tasks in the **RLinf** framework.
    It also explains how to fine-tune a VLA model in the **Franka-Sim** simulation environment
    to perform robotic manipulation tasks.
    1. **Visual understanding**: process RGB images captured from robot cameras;
    2. **Language understanding**: interpret natural language task descriptions;
    3. **Action generation**: produce accurate robot actions (position, rotation, gripper control);
    4. **Reinforcement learning**: optimize policies with PPO using environment feedback.
    The Franka-Sim environments are built on top of the
    `serl <https://rail-berkeley.github.io/serl/docs/sim_quick_start.html>`_ project.
    Two minimal Franka-Sim simulation tasks are provided:
    - ``PandaPickCube-v0``
    - ``PandaPickCubeVision-v0``
    - **Task**: control a Franka Panda robot arm to pick up a cube and move it to a target position;
    - **Observation**:
    - ``PandaPickCube-v0``: proprioceptive states + target position;
    - ``PandaPickCubeVision-v0``: multi-view RGB images (third-person + wrist camera) + proprioceptive states;
    - **Action Space**: 4D continuous actions
    - 3D end-effector position control (x, y, z)
    - gripper control (open/close)
    ``PandaPickCube-v0``
    - **States**: proprioceptive states and target location
    - end-effector 3D position
    - end-effector 3D velocity
    - gripper open/close state (1D)
    - cube 3D position
    ``PandaPickCubeVision-v0``
    - **Images**: RGB tensors from a third-person view and a wrist camera view
    - **States**: proprioceptive states
    - end-effector 3D position
    - end-e...
  - [A] docs/source-en/rst_source/examples/embodied/opensora.rst
    Excerpt:
    RL with OpenSora World Model
    ======================================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    This document provides a comprehensive guide to launching and managing the
    Vision-Language-Action Models (VLAs) training task within the RLinf framework,
    using the **Action-conditioned OpenSora World Model** (hereafter referred to as OpenSora)
    The primary objective is to train the policy in a closed-loop fashion without requiring real robots
    reinforcement learning training tasks in the OpenSora-based simulation environment,
    OpenSora aims to endow the model with the following capabilities:
    1. **Visual Understanding**: OpenSora generates future video frames from current observations and given action sequences, providing continuous visual feedback to the policy, enabling it to process RGB images from real robot cameras.
    2. **Language Comprehension**: Understanding natural-language task descriptions.
    3. **Action Generation**: Producing precise robotic actions (position, rotation, gripper control).
    4. **Policy Improvement**: Leveraging "imagined" trajectories generated by OpenSora to optimize the VLA policy using reinforcement learning methods such as PPO.
    As a world model, OpenSora can theoretically fit any environment for any task while maintaining a consistent interface. Using the **LIBERO environment** as an example, the environment interfaces and definitions are as follows:
    **OpenSora Simulating LIBERO Environment**
    - **Environment**: Visual generation model
    - **Task**: Command a 7-DoF robotic arm to perform a variety of household manipulation skills (pick-and-place, stacking, opening drawers, spatial rearrangement)
    - **Observation**: Images returned by the visual generation model
    - **Action Space**: 7-di...
  - [A] docs/source-en/rst_source/examples/embodied/robotwin.rst
    Excerpt:
    RL with RoboTwin Benchmark
    ===========================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    This document provides a comprehensive guide to launching and managing
    **Vision-Language-Action Models (VLAs)** training tasks within the RLinf framework,
    focusing on finetuning a VLA model for robotic manipulation in the RoboTwin environment.
    The primary objective is to develop a model capable of performing robotic manipulation by:
    1. **Visual Understanding**: Processing RGB images from the robot's camera.
    2. **Language Comprehension**: Interpreting natural-language task descriptions.
    3. **Action Generation**: Producing precise robotic actions (position, rotation, gripper control).
    4. **Reinforcement Learning**: Optimizing the policy via PPO and GRPO with environment feedback.
    RoboTwinEnv Environment
    **RoboTwinEnv Environment**
    - **Environment**: RLinf framework provides the RoboTwinEnv environment for reinforcement learning training based on the RoboTwin 2.0 simulation platform.
    - **Task**: Control a robotic arm to perform various manipulation tasks. RLinf RoboTwinEnv currently supports **46 tasks**, and users can select tasks for training as needed.
    - ``adjust_bottle``: Pick up the bottle on the table headup with the correct arm.
    - ``place_a2b_left``: Use appropriate arm to place object A on the left of object B.
    - ``place_a2b_right``: Use appropriate arm to place object A on the right of object B.
    - ``place_bread_basket``: If there is one bread on the table, use one arm to grab the bread and put it in the basket, if there are two breads on the table, use two arms to simultaneously grab up two breads and put them in the basket.
    - ``place_bread_skillet``: Use one arm to grab the bread on the table and put it into th...
  - [A] docs/source-en/rst_source/examples/embodied/sft_openpi.rst
    Excerpt:
    Supervised Fine-Tuning
    =======================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    This page explains how to run **full-parameter supervised fine-tuning (SFT)** and **LoRA fine-tuning** with the RLinf framework. SFT is typically the first stage before reinforcement learning: the model imitates high-quality examples so RL can continue optimization with a strong prior.
    Contents
    - How to configure full-parameter SFT and LoRA SFT in RLinf
    - How to launch training on a single machine or multi-node cluster
    - How to monitor and evaluate results
    Supported datasets
    RLinf currently supports datasets in the LeRobot format, selected via **config_type**.
    Supported formats include:
    - pi0_maniskill
    - pi0_libero
    - pi0_aloha_robotwin
    - pi05_libero
    - pi05_maniskill
    - pi05_metaworld
    - pi05_calvin
    1. In ``examples/sft/config/custom_sft_openpi.yaml``, set the data format.
    config_name: "pi0_custom"
    2. In ``rlinf/models/embodiment/openpi/__init__.py``, set the data format to ``pi0_custom``.
    TrainConfig(
    name="pi0_custom",
    model=pi0_config.Pi0Config(),
    data=CustomDataConfig(
    base_config=DataConfig(
    assets=AssetsConfig(assets_dir="checkpoints/torch/pi0_base/assets"),
    action_train_with_rotation_6d=False,  # User can add extra config in custom dataset
    pytorch_weight_path="checkpoints/torch/pi0_base",
    3. In ``rlinf/models/embodiment/openpi/dataconfig/custom_dataconfig.py``, define the custom dataset config.
    class CustomDataConfig(DataConfig):
    self.base_config = DataConfig(
    self.assets = AssetsConfig(assets_dir="checkpoints/torch/pi0_base/assets")
    self.action_train_with_rotation_6d = False
    Training configuration
    A full example lives in ``examples/sft/config/libero_sft_openpi.yaml``. Key fields:
    num_nodes: 1                 # number of...
  - [A] docs/source-en/rst_source/examples/embodied/sft_vlm.rst
    Excerpt:
    VLM Supervised Fine-Tuning
    ================================
    This document explains how to run **full-parameter supervised fine-tuning (Full-parameter SFT)** for VLM models in RLinf.
    This tutorial mainly focuses on two files:
    - Launch script: ``examples/sft/run_vlm_sft.sh``
    - Training config: ``examples/sft/config/qwen2_5_sft_vlm.yaml``
    Launch Script: ``examples/sft/run_vlm_sft.sh``
    - The script uses ``examples/sft/config/qwen2_5_sft_vlm.yaml`` by default.
    - Logs are redirected to: ``<repo>/logs/<timestamp>/``
    - Actual command:
    python examples/sft/train_vlm_sft.py \
    --config-path examples/sft/config/ \
    --config-name <your_config_name> \
    Config Template: ``examples/sft/config/qwen2_5_sft_vlm.yaml``
    If you intend to train models such as **qwen3_vl** or **qwen3_vl_moe**, please ensure that the version of `transformers` in your current environment is **greater than or equal to 4.57.1**.
    The VLM config structure is similar to other RLinf training configs.
    You mainly need to adapt ``data`` and ``actor.model`` for your VLM use case.
    1. Prepare the environment. Pull the RLinf Docker image:
    ``rlinf/rlinf:math-rlinf0.2-torch2.6.0-sglang0.4.6.post5-vllm0.8.5-megatron0.13.0-te2.1``.
    2. Prepare model weights:
    ``https://huggingface.co/Qwen/Qwen2.5-VL-3B-Instruct``.
    3. Prepare Robo2VLM dataset:
    ``https://huggingface.co/datasets/keplerccc/Robo2VLM-1``.
    4. Edit ``examples/sft/config/qwen2_5_sft_vlm.yaml`` and run
    ``examples/sft/run_vlm_sft.sh``.
    Example of Qwen2_5_VL_3B SFT
    Important note: after downloading Robo2VLM, train and eval parquet files are mixed in one directory
    (e.g., ``train-00000-of-00262.parquet`` and ``test-0000X-of-00003.parquet``).
    In the example below, fields you must modify are already commented.
    - override hydra/job_logging: stdout
    num_nodes: 1
    task_type: sft
    exper...
  - [A] docs/source-en/rst_source/examples/embodied/xsquare_turtle2.rst
    Excerpt:
    Real-World RL with XSquare Turtle2
    ====================================
    This document provides a comprehensive guide to launching real-world reinforcement
    learning training on the **XSquare Turtle2** dual-arm robot platform using the
    RLinf framework.
    The primary objective is to train a ResNet-based CNN policy from scratch for robotic
    manipulation tasks on a real robot by:
    1. **Visual Understanding**: Processing RGB images from up to three onboard cameras.
    2. **Action Generation**: Producing precise delta end-effector actions (position, rotation, and gripper) for one or two arms.
    3. **Reinforcement Learning**: Optimizing the policy via SAC with real-environment feedback.
    **Real-World Environment**
    - **Robot**: XSquare Turtle2 – a dual-arm tabletop robot with up to 2 arms (left arm ID ``0``, right arm ID ``1``) and up to 3 RGB cameras (IDs ``0``, ``1``, ``2``).
    - **Task**: Currently we support the **button-pressing** task (``ButtonEnv``):
    - The robot end-effector moves downward to press a button located at a target pose.
    - Random resets add ±5 cm position noise and ±20° orientation noise to increase difficulty.
    - The task description string: *"Press the button with the end-effector."*
    - **Observation**:
    - RGB images (128 × 128) from one or more cameras, returned as ``frames/wrist_<k>``.
    - TCP pose: position (xyz) + quaternion (xyzw) per active arm, concatenated as a flat vector.
    - Single arm: ``[batch_size, 7]``
    - Dual arm: ``[batch_size, 14]``
    - **Action Space**: 7-dimensional continuous action per arm, stacked for dual-arm use:
    - 3D delta position (Δx, Δy, Δz)
    - 3D delta orientation (Δroll, Δpitch, Δyaw)
    - Gripper width command (open/close)
    Single arm: ``(7,)`` — Dual arm: ``(14,)``; values normalized to ``[-1, 1]``.
    - **Images**: RGB tensors ``[batch_size, 128, 128,...
  - [A] docs/source-zh/rst_source/examples/embodied/franka.rst
    Excerpt:
    Franka真机强化学习
    ============================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    本文档给出在 RLinf 框架内启动在 Franka 机械臂真机环境中训练任务的完整指南，
    重点介绍如何从零开始训练基于 ResNet 的 CNN 策略以完成机器人操作任务。
    1. **视觉理解**：处理来自机器人相机的 RGB 图像。
    2. **动作生成**：产生精确的机器人动作（位置、旋转、夹爪控制）。
    3. **强化学习**：结合环境反馈，使用 SAC 优化策略。
    - **Environment**: 真机设置
    - Franka Emika Panda 机械臂
    - Realsense 相机
    - 可能使用空间鼠标进行数据采集和人类干预
    - **Task**: 目前支持插块插入（Peg Insertion）和充电器插电（Charger）任务
    - **Observation**: 腕部或第三人称相机的 RGB 图像（128×128）
    - **Action Space**: 6 维或 7 维连续动作，取决于是否包含夹爪控制：
    - 三维位置控制（x, y, z）
    - 三维旋转控制（roll, pitch, yaw）
    - 夹爪控制（开/合）
    - **Images**: RGB 张量 ``[batch_size, 128, 128, 3]``
    - **Actions**:归一化取值在 ``[-1, 1]`` 的连续值
    - **Rewards**: 基于任务完成度的逐步奖励
    1. **SAC (Soft Actor-Critic)**
    - 通过 Bellman 公式和熵正则化学习 Q 值。
    - 学习策略网络以最大化熵正则化的 Q 值。
    - 学习温度参数以平衡探索与利用。
    2. **Cross-Q**
    - SAC 的一种变体，去除了目标 Q 网络。
    - 在一个批次中连接当前观测和下一个观测，结合 BatchNorm 实现 Q 的稳定训练。
    3. **RLPD (Reinforcement Learning with Prior Data)**
    - SAC 的一种变体，结合离线数据和在线数据进行训练。
    - 使用较大的网络更新与数据更新比例，以提高数据效率。
    4. **CNN Policy Network**
    - 基于 ResNet 的视觉输入处理架构。
    - 使用 MLP 层融合图像和状态以输出动作。
    - 用多个 Q-head 实现 Critic 功能。
    - **机械臂**：Franka Emika Panda 机械臂。
    - **相机**：Intel RealSense 相机，用于采集 RGB 图像。
    - **计算节点**：一台带有 GPU 的计算机，用于训练 CNN 策略。
    - **机器人控制节点**：一台与机械臂处于同一局域网的小型计算机（不需要 GPU），用于控制 Franka 机械臂。
    - **空间鼠标（可选）**：用于远程操控数据采集或在训练过程中进行人工干预。
    1. 检查 Franka 固件版本
    在机器人管理网页（一般为 ``http://<robot_ip>/desk``）中，点击 ``SETTINGS`` 选项卡，在 ``DashBoard`` 中查看 ``Control`` 后面的版本号，如下所示。
    <div style="flex: 1; text-align: center;">
    <img src="https://github.com/RLinf/misc/blob/main/pic/franka_firmware.png?raw=true" style="width: 60%;"/>
    请确保 Franka 固件版本 ``<5.9.0`` 以保证与 serl_franka_controllers 的兼容性。
    推荐使用固件版本 5.7.2 以获得最佳兼容性。
    2. 实时内核安装
    推荐在实时内核（Real-time Kernel）上运行 Franka 控制程序，以获得更好的实时性。
    请参考 `Franka 官方文档 <https://frankarob...
  - [A] docs/source-zh/rst_source/examples/embodied/frankasim.rst
    Excerpt:
    基于 Franka-Sim 评测平台的强化学习训练
    ======================================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    本文档给出在 **RLinf** 框架内启动与管理 **Vision-Language-Action Models (VLAs)** 训练任务的完整指南，
    并介绍如何在 **Franka-Sim** 环境中微调 VLA 模型以完成机器人操作任务。
    1. **视觉理解**：处理来自机器人相机的 RGB 图像；
    2. **语言理解**：理解自然语言的任务描述；
    3. **动作生成**：产生精确的机器人动作（位置、旋转、夹爪控制）；
    4. **强化学习**：结合环境反馈，使用 PPO 优化策略。
    Franka-Sim 环境基于项目 `serl <https://rail-berkeley.github.io/serl/docs/sim_quick_start.html>`_ 构建，
    - ``PandaPickCube-v0``
    - ``PandaPickCubeVision-v0``
    - **Task**：控制 Franka Panda 机械臂抓取物块并移动至目标位置；
    - **Observation**：
    - ``PandaPickCube-v0``：本体感知状态 + 目标位置；
    - ``PandaPickCubeVision-v0``：多视角 RGB 图像（机器人视角 + 腕部相机）+ 本体感知状态；
    - **Action Space**：4 维连续动作
    - 三维位置控制（x, y, z）
    - 夹爪控制（开/合）
    ``PandaPickCube-v0``
    - **States**：本体感知与目标位置
    - 末端执行器三维位置
    - 末端执行器三维速度
    - 夹爪一维开合
    - 物块三维位置
    ``PandaPickCubeVision-v0``
    - **Images**：第三人称视角与腕部相机视角的 RGB 张量
    - **States**：本体感知
    - 末端执行器三维位置
    - 末端执行器三维速度
    - 夹爪一维开合
    - **Task Descriptions**：自然语言指令
    - **Actions**：归一化连续动作值
    - **Rewards**：基于任务完成度的逐步奖励
    1. **PPO（近端策略优化）**
    - 使用 GAE（广义优势估计）进行优势估计；
    - 带比例限制（clipping）的策略裁剪；
    - 价值函数裁剪；
    - 熵正则化。
    2. **SAC (Soft Actor-Critic)**
    - 通过 Bellman 公式和熵正则化学习 Q 值。
    - 学习策略网络以最大化熵正则化的 Q 值。
    - 学习温度参数以平衡探索与利用。
    1. 克隆 RLinf 仓库
    # 为提高国内下载速度，可以使用：
    # git clone https://ghfast.top/github.com/RLinf/RLinf.git
    2. 安装依赖
    **选项 1：Docker 镜像**
    使用 Docker 镜像运行实验：
    docker run -it --rm --gpus all \
    --shm-size 20g \
    rlinf/rlinf:agentic-rlinf0.2-frankasim
    # 如果需要国内加速下载镜像，可以使用：
    # docker.1ms.run/rlinf/rlinf:agentic-rlinf0.2-frankasim
    选项 2：自定义环境
    # 为提高国内依赖安装速度，可以添加 --use-mirror 到下面的 install.sh 命令
    bash requirements/install.sh embodied --model openvla --env frankasim

## v0.1
- README / repo positioning excerpt:
<div align="center">
<img src="docs/source-en/_static/svg/logo_white.svg" alt="RLinf-logo" width="600"/>
</div>
<div align="center">
<a href="https://arxiv.org/abs/2509.15965"><img src="https://img.shields.io/badge/arXiv-Paper-red?logo=arxiv"></a>
<a href="https://huggingface.co/RLinf"><img src="https://img.shields.io/badge/HuggingFace-yellow?logo=huggingface&logoColor=white" alt="Hugging Face"></a>
<a href="https://rlinf.readthedocs.io/en/latest/"><img src="https://img.shields.io/badge/Documentation-Purple?color=8A2BE2&logo=readthedocs"></a>
<a href="https://rlinf.readthedocs.io/zh-cn/latest/"><img src="https://img.shields.io/badge/中文文档-red?logo=readthedocs"></a>
<a href="https://deepwiki.com/RLinf/RLinf"><img src="https://img.shields.io/badge/Ask%20DeepWiki-1DA1F2?logo=databricks&logoColor=white&color=00ADEF" alt="Ask DeepWiki"></a>
[![English](https://img.shields.io/badge/lang-English-blue.svg)](README.md)
[![简体中文](https://img.shields.io/badge/语言-简体中文-red.svg)](README.zh-CN.md)
<h1 align="center">
</h1>
RLinf is a flexible and scalable open-source infrastructure designed for post-training foundation models via reinforcement learning. The 'inf' in RLinf stands for `Infrastructure`, highlighting its role as a robust backbone for next-generation training. It also stands for `Infinite`, symbolizing the system’s support for open-ended learning, continuous generalization, and limitless possibilities in intelligence development.
<img src="docs/source-en/_static/svg/overview.svg" alt="RLinf-overview"/>
## What's NEW!
- [2025/11] 🔥 RLinf supports reinforcement learning fine-tuning for [CALVIN](https://github.com/mees/calvin). Doc: [RL on CALVIN](https://rlinf.readthedocs.io/en/latest/rst_source/examples/calvin.html).
- [2025/11] 🔥 RLinf supports reinforcement learning fine...
- High-signal repository paths at this tag:
  - docs/README.md
  - rlinf/envs/robotwin/README.md
  - README.md
  - docs/source-en/rst_source/examples/pi0.rst
  - docs/source-zh/rst_source/examples/pi0.rst
  - docs/source-en/rst_source/examples/gr00t.rst
  - docs/source-en/rst_source/examples/index.rst
  - docs/source-zh/rst_source/examples/gr00t.rst
  - docs/source-zh/rst_source/examples/index.rst
  - docs/source-en/rst_source/examples/calvin.rst
  - docs/source-en/rst_source/examples/libero.rst
  - docs/source-zh/rst_source/examples/calvin.rst
