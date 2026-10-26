# RLinf/RLinf Release Roadmap Reference

- 仓库: `RLinf/RLinf`
- 对应主报告: `RLinf_RLinf_release_roadmap.md`
- 统计窗口: 最近一年
- 生成策略: GitHub release body + 外链文档摘录 + 相邻 release tag 的 GitHub compare 摘要 + tagged README/docs/examples/configs/高信号源码证据
- 版本总数: 3
- 正式版数量: 3
- 预发布版数量: 0
- 外链文档覆盖版本数: 3
- compare 摘要覆盖版本数: 2
- 最新版本: v0.3 (2026-07-15 21:33:16 CST)
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
- 2026-07-15 21:33:16 CST | v0.3 | 正式版
- 2026-03-26 23:06:12 CST | v0.2 | 正式版
- 2025-12-17 20:01:25 CST | v0.1 | 正式版

## 证据附录

### v0.3
- 标题: RLinf v0.3 Release
- 类型: 正式版
- 发布时间: 2026-07-15 21:33:16 CST
- 链接: https://github.com/RLinf/RLinf/releases/tag/v0.3
- GitHub release body:
🎉 Introducing RLinf v0.3.

This release completes an end-to-end real-world training pipeline, adds new real-world RL components and algorithms, and brings more simulators and SOTA models to simulation RL. All supported examples have been strictly validated for correctness and reproducibility (see the test results at the end).

# Embodied

## 1. Models

Continuing to expand the model ecosystem, 6 new embodied models are added, covering world models, VLA models, and system-level acceleration.

- Added **Dexbotic DM0** model support, with online RL fine-tuning using PPO on LIBERO. Link: [Dexbotic](https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/dexbotic.html)

- Added **DreamZero** model support: a VLA policy fine-tuned from the WAN2.1/2.2 video-generation world model, integrated into the SFT workflow, achieving nearly **4×** throughput improvement via FSDP2/CUDA Graph and other system-level acceleration. Link: [DreamZero SFT](https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/sft_dreamzero.html)

- Added **GR00T-N1.6 / N1.7** model RL fine-tuning support. Link: [GR00T](https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/gr00t.html)

- Added **ABot-M0** model support. Link: [ABot-M0](https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/abot_m0.html)

- Added **StarVLA** model support (GRPO on LIBERO). Link: [StarVLA](https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/starvla.html)

- Added **LingBot-VLA** model support (RoboTwin environment SFT/RL). Link: [LingBot-VLA](https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/lingbotvla.html)

## 2. Simulators

Broadening simulation-RL scene coverage, 5 new simulators are added, with refined...
- 外链文档摘录:
  - https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/dexbotic.html
    RLinf uses the Dexbotic π0and DM0 policies as LIBERO action-generation models, then fine-tunes them online with PPO.
    Fine-tune Dexbotic π0or DM0 on LIBERO with PPO.
    LIBERO Spatial · Object · Goal · 10
    1 node · 8 GPUs
    Dexbotic pi0/dm0 policies on spatial manipulation tasks.
    Dexbotic pi0 on object manipulation tasks.
    Option 1: Docker image— image tag
    dockerrun-it--rm--gpusall\--shm-size20g\--networkhost\--namerlinf\-v.:/workspace/RLinf\rlinf/rlinf:agentic-rlinf0.3-maniskill_libero# Mainland China mirror: docker.1ms.run/rlinf/rlinf:agentic-rlinf0.3-maniskill_libero# Inside the container, switch to the Dexbotic virtual environment:sourceswitch_envdexbotic
    Option 2: Custom environment— install bundle
    # Add --use-mirror for faster downloads in mainland China.bashrequirements/install.shembodied--modeldexbotic--envmaniskill_liberosource.venv/bin/activate
    # Method 1: git clonegitlfsinstall
    gitclonehttps://huggingface.co/Dexmal/DM0-libero# Method 2: huggingface-hub (set HF_ENDPOINT=https://hf-mirror.com in mainland China)pipinstallhuggingface-hub
    huggingface-clidownloadDexmal/libero-db-pi0--local-dirlibero-db-pi0
    huggingface-clidownloadDexmal/DM0-libero--local-dirDM0-libero
    π₀ checkpoint path → set
    DM0 checkpoint path → set both model paths to
    Action chunks → π₀ uses
    pythontoolkits/standalone_eval_scripts/dexbotic/libero_eval.py\--config_namedb_pi0_libero\--pretrained_path/path/to/checkpoint\--task_suite_namelibero_spatial\--num_trials_per_task50\--action_chunk5\--num_steps10
    For DM0, switch the evaluator config and action chunk:
    pythontoolkits/standalone_eval_scripts/dexbotic/libero_eval.py\--config_namedm0_libero\--pretrained_path/path/to/checkpoint\--task_suite_namelibero_spatial\--num_trials_per_task50\--action_chunk10\--num_steps10
  - https://rlinf.readthedocs.io/en/release-v0.3/rst_source/examples/embodied/sft_dreamzero.html
    1+ nodes · GPUs
    Backbones:WAN2.1 (e.g. DreamZero-DROID 14B), WAN2.2 (e.g. Wan2.2-TI2V-5B cold start).
    Option 1: SFT-only environment— install DreamZero without simulator dependencies:
    # Add --use-mirror for faster downloads in mainland China.bashrequirements/install.shembodied--modeldreamzerosource.venv/bin/activate
    Option 2: SFT + LIBERO evaluation— add LIBERO simulator dependencies:
    Installs only offline SFT dependencies by default, or adds LIBERO when you need simulator evaluation.
    DreamZero 14B (DROID / AgiBot):DreamZero-DROID,DreamZero-AgiBot— see
    RLinf 5B (LIBERO SFT):RLinf-DreamZero-WAN2.2-5B-LIBERO-SFT-Step18000— see
    YAML example (DROID + official 14B; see
    Train from Scratch (WAN2.2 Component Cold Start)#
    (not in the 5B repo)
    Training data must follow the LeRobot v2/v3 layout (
    # LIBEROpythontoolkits/lerobot/generate_dreamzero_metadata.py\--presetlibero_sim\--dataset-root/path/to/libero\--output-metadata/path/to/metadata.json# DROID (use --merge for multiple datasets)pythontoolkits/lerobot/generate_dreamzero_metadata.py\--presetoxe_droid\--dataset-root/path/to/droid\--output-metadata/path/to/metadata.json\--merge# Franka PnPpythontoolkits/lerobot/generate_dreamzero_metadata.py\--presetfranka_pnp\--dataset-root/path/to/franka_pnp\--output-metadata/path/to/franka_pnp_metadata.json
    Lazy-load mp4 videos.Must be ``True`` for ``multi_anchor`` sampling(otherwise anchor-based frame lookup fails).
    is a contiguous fixed window.
    ; affects lazy mp4 speed and compatibility.``torchcodec`` is recommended.
    (commonly4; official Groot DROID recipes may use5).
    :per-block action steps in DreamTransform / WAN(LIBERO 16, DROID 24), not the dataset macro stride.
    (e.g. LIBERO 64, DROID 96).
    in presets (DreamZero default 33 =
    UMT5 tokenizer path (required for training and collate).
    WAN image encoder; WAN2.2 must point toWAN2.1 CLIPweights.
    T5 text encoder weights.
    VAE weights; WAN2.2 uses
    Action steps per WAN temporal block (LIBERO 16, DROID 24).
    State rows per sample (usually 1, one state per macro anchor).
    Padding limits and max text sequence length in DreamTransform.
    WAN policy head target resolutionafter multi-view concat(5B preset e.g. 176×320; Libero often 160×320). Model-internal resize only;do notuse for per-view data transform resize.
    keepsoptimizer states and master weights in FP32(more stable), while FSDP runs forward/backward matmuls inBF16via
    : FSDP2 sharding, gradient checkpointing;
    # ---------- data (single dataset) ----------data:train_data_paths:/path/to/liberolazy_load:Truesampling_mode:multi_anchorvideo_backend:torchcodecnum_workers:8# ---------- data (mixture; see libero_franka_mix_sft_dreamzero_5b.yaml) ----------data:train_data_paths:-dataset_path:/path/to/liberoweight:4embodiment_tag:libero_simmetadata_json_path:/path/to/libero_metadata.json-dataset_path:/path/to/franka_pnpweight:1embodiment_tag:franka_pnpmetadata_json_path:/path/to/franka_metadata.json# ---------- model (resume from checkpoint) ----------actor:model:model_path:/path/to/DreamZero-DROIDtokenizer_path:/path/to/umt5-xxlembodiment_tag:oxe_droidaction_horizon:24metadata_json_path:/path/to/metadata.json# if no experiment_cfg/metadata.json
    # LIBERO + WAN2.1 (checkpoint, dreamzero_14b preset)bashexamples/sft/run_vla_sft.shlibero_sft_dreamzero_14b# LIBERO + WAN2.2 (cold start, dreamzero_5b preset)bashexamples/sft/run_vla_sft.shlibero_sft_dreamzero_5b# DROID + WAN2.1 (dreamzero_14b preset; model_path -> DreamZero-DROID)bashexamples/sft/run_vla_sft.shdroid_sft_dreamzero_14b# LIBERO + Franka mixture (WAN2.2; see libero_franka_mix_sft_dreamzero_5b.yaml)bashexamples/sft/run_vla_sft.shlibero_franka_mix_sft_dreamzero_5b
    Evaluation on LIBERO Spatial forRLinf-DreamZero-WAN2.2-5B-LIBERO-SFT-Step18000(
    For WAN2.2: input resolution and
    To train DreamZero SFT on anew robot or LeRobot dataset, add an
    → DreamZeroLeRobotDataset (reads parquet/mp4 via transform keys)
    Step 1: Implement the Embodiment Transform Module#
    (5B preset includes 17, 21, 26). Anew IDimplies random projector init or model config changes.
    Default per-block action steps (LIBERO 16, DROID 24); align with
    T5 prompt prefix describing the multi-view layout (consistent with Groot training templates).
    Step 2: Register in RLinf#
    Add a member to
    Option A (recommended): add an entry to
    Step 4: Author / Adjust the Training Config#
    data:train_data_paths:/path/to/your_lerobotlazy_load:True# required for multi_anchor with mp4sampling_mode:multi_anchoractor:model:embodiment_tag:"<your_tag>"metadata_json_path:/path/to/metadata.jsonaction_horizon:<match DEFAULT_ACTION_HORIZON># when resuming: verify action_loss_embodiment_ids includes your projector IDtarget_video_height:...target_video_width:...relative_action:...relative_action_keys:[...]
    For WAN cold start, add the new ID to
    Step 5: Validate with a Short Run#
    Run 50–200 SFT steps; ensure no
- Compare 摘要: v0.2 -> v0.3
  - commits: 231
  - files changed: 300+ returned files (GitHub compare API file list cap)
  - additions: 14226
  - deletions: 5207
  - top directories: .claude, .codex, .cursor, .github, .gitignore, .pre-commit-config.yaml
  - representative files:
    - docs/source-en/_static/svg/overview.svg (modified, +1/-2701)
    - docs/source-en/_static/css/sphinx-modal.css (modified, +483/-505)
    - docs/source-en/_static/js/ai-chat-service.js (modified, +466/-218)
    - .github/workflows/embodied-e2e-tests.yml (modified, +655/-24)
    - docs/source-en/_static/sphinx-modal-widget.js (modified, +234/-432)
    - docs/source-en/_static/css/custom.css (modified, +502/-0)
    - .claude/skills/test-install/driver.py (added, +430/-0)
    - .codex/skills/test-install/driver.py (added, +430/-0)

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
    - Fork602

# Tagged Repository Source Evidence

## v0.3
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
- [2026/07] 🎉 RLinf v0.3 is released with major upgrades in the real-world RL full pipeline (data collection → SFT → RL → deployment), more simulators and SOTA models, and system-level optimizations. Release notes: [RLinf v0.3](https://rlinf.readthedocs.io/en/lates...
- High-signal repository paths at this tag:
  - docs/README.md
  - docs/source-en/rst_source/examples/sft_index.rst
  - docs/source-zh/rst_source/examples/sft_index.rst
  - docs/source-en/rst_source/examples/real_world_index.rst
  - docs/source-zh/rst_source/examples/real_world_index.rst
  - docs/assistant/README.md
  - examples/sft/train_vla_sft.py
  - examples/sft/train_vlm_sft.py
  - examples/embodiment/collect_real_data.py
  - examples/reward/eval_realworld_teleop.py
  - examples/reward/realworld_collect_process_dataset.py
  - docs/source-en/rst_source/examples/embodied/franka.rst
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
    [RST grammar](https://zh-sphinx-doc.readthedocs.io/en/latest/rest.html)
  - [A] docs/source-en/rst_source/examples/real_world_index.rst
    Excerpt:
    RL with Real-World Robots
    =========================
    Use this section when your starting point is physical robot hardware. Start with Franka if you use a Franka arm or a Franka-based rig; use the other robot pages for GimArm, XSquare Turtle2, and Dexmal DOS-W1.
    Each section gives the setup path for teleoperation, data collection, sim-to-real transfer, deployment, or online RL.
    .. raw:: html
    <div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 20px; align-items: flex-start; justify-items: center; max-width: 980px; margin: 0 auto;">
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/franka.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/franka_arm_small.jpg"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/franka.html" style="text-decoration: underline; color: blue;">
    <b>Franka</b>
    Use the Franka section for base real-world RL, reward models, ZED + Robotiq, GELLO, VR / PICO, dual-arm rigs, dexterous hands, Pi0 SFT, and HG-DAgger
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/gim_arm.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/gim-arm.png"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/gim_arm.html" style="text-decoration: underline; color: blue;">
    Train a 6-DOF GimArm peg-insertion task over SocketCAN with Pinocchio-based FK
    <div style="flex: 1 1 30%; max-width: 300px; t...
  - [A] docs/source-en/rst_source/examples/sft_index.rst
    Excerpt:
    SFT for VLA / WAM Models
    ========================
    Supervised fine-tuning (SFT) is the standard cold-start step before embodied RL: a strong SFT checkpoint dramatically reduces RL exploration time and improves final policy quality. This category lists RLinf's recipes for full-parameter and LoRA SFT on VLA / WAM models, plus VLM SFT for multimodal post-training.
    After running SFT here, continue to :doc:`vla_wam_index` (model-centric RL) or :doc:`simulators_index` (benchmark-centric RL) to fine-tune the resulting checkpoint with RL.
    .. raw:: html
    <div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 20px; align-items: flex-start; justify-items: center; max-width: 980px; margin: 0 auto;">
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <!-- TODO(thumbnail): replace placeholder cover image URL for sft_openpi -->
    <a href="embodied/sft_openpi.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/pi0_icon.jpg"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/sft_openpi.html" style="text-decoration: underline; color: blue;">
    Run full-parameter and LoRA SFT for OpenPI before RL fine-tuning
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/sft_dreamzero.html" style="display: block;"><img src="https://dreamzero0.github.io/images/project_overview.png"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/sft_dreamzero.html" style="text-decoration: underline; co...
  - [A] docs/source-zh/rst_source/examples/real_world_index.rst
    Excerpt:
    真实机器人强化学习
    ========================================
    当你的出发点是真实机器人硬件时，请使用本节。如果你使用 Franka 机械臂或 Franka-based rig，请从 Franka 开始；GimArm、XSquare Turtle2 和 Dexmal DOS-W1 请进入对应机器人页面。
    每个章节都给出遥操作、数据采集、Sim-to-Real 迁移、部署或在线 RL 所需的配置路径。
    .. raw:: html
    <div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 20px; align-items: flex-start; justify-items: center; max-width: 980px; margin: 0 auto;">
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/franka.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/franka_arm_small.jpg"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/franka.html" style="text-decoration: underline; color: blue;">
    <b>Franka</b>
    进入 Franka 章节，查看基础真机 RL、reward model、ZED + Robotiq、GELLO、VR / PICO、双臂、灵巧手、Pi0 SFT 和 HG-DAgger
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/gim_arm.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/gim-arm.png"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/gim_arm.html" style="text-decoration: underline; color: blue;">
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/xsquare_turtle2.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/xsquare_turtle2_arm_small.jpg"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);"...
  - [A] docs/source-zh/rst_source/examples/sft_index.rst
    Excerpt:
    VLA / WAM 模型监督微调
    ========================================
    监督微调（SFT）是具身强化学习的标准冷启动步骤：一个良好的 SFT 检查点能显著缩短 RL 探索时间并提升最终策略效果。本类示例汇总了 RLinf 在 VLA / WAM 模型上的全量与 LoRA SFT 配方，以及面向多模态后训练的 VLM SFT。
    完成本节的 SFT 后，可继续阅读 :doc:`vla_wam_index`\ （以模型为主线的 RL 微调）或 :doc:`simulators_index`\ （以基准为主线的 RL 微调）以进一步用 RL 提升所得检查点。
    .. raw:: html
    <div style="display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 20px; align-items: flex-start; justify-items: center; max-width: 980px; margin: 0 auto;">
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <!-- TODO(thumbnail): replace placeholder cover image URL for sft_openpi -->
    <a href="embodied/sft_openpi.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/pi0_icon.jpg"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/sft_openpi.html" style="text-decoration: underline; color: blue;">
    支持 OpenPI 全量 SFT 与 LoRA 微调，作为强化学习前置阶段
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/sft_dreamzero.html" style="display: block;"><img src="https://dreamzero0.github.io/images/project_overview.png"
    style="width: 100%; height: 200px; object-fit: cover; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);" /></a>
    <p style="margin-top: 8px; font-size: 14px; line-height: 1.4;">
    <a href="embodied/sft_dreamzero.html" style="text-decoration: underline; color: blue;">
    面向 DreamZero 的全量与 mixture SFT（WAN2.1 / WAN2.2 主干）
    <div style="flex: 1 1 30%; max-width: 300px; text-align: center;">
    <a href="embodied/sft_vlm.html" style="display: block;"><img src="https://raw.githubusercontent.com/RLinf/misc/main/pic/release_0.2/...
  - [A] docs/assistant/README.md
    Excerpt:
    # RLinf Docs Assistant Runtime
    The assistant runtime is plain browser JavaScript because the docs are built by
    Sphinx. The canonical editable copies live under:
    ```text
    docs/source-en/_static/
    ```
    The zh docs tree carries the same runtime files so each Sphinx build can package
    its own static assets. After changing assistant JavaScript or CSS, run:
    node docs/assistant/sync-static.mjs
    node --test docs/tests/assistant-*.test.mjs
    Keep locale-specific text in Sphinx templates or runtime config. Keep shared
  - [A] docs/source-en/rst_source/examples/embodied/dual_franka.rst
    Excerpt:
    Using Dual Franka
    =================
    .. figure:: https://raw.githubusercontent.com/RLinf/misc/main/pic/franka_arm_small.jpg
    :align: center
    :width: 80%
    Franka arm hardware used as the basis for the dual-Franka GELLO collection and π₀.₅ deployment workflow.
    Run the supported dual-Franka workflow: collect joint-space demonstrations with GELLO, convert them to tcp_rot6d data, fine-tune OpenPI π₀.₅, and deploy the checkpoint back to the robot nodes.
    Overview
    Build a dual-arm dataset, train π₀.₅, and deploy on a two-node Franka rig.
    .. grid:: 2 4 4 4
    :gutter: 2
    OpenPI π₀.₅
    SFT · eval-only deployment
    2× Franka · 2 robot nodes · GELLO
    | **You'll do:** install franky deps → collect GELLO demos → convert rot6d data → run SFT → deploy eval config.
    | **Prerequisites:** :doc:`franka` · :doc:`franka_gello` · two Franka arms · OpenPI assets.
    :header-rows: 1
    :widths: 24 24 24
    - Config / entry point
    - Description
    - ``realworld_collect_data_gello_joint_dual_franka``
    - Collect dual-arm joint trajectories.
    * - SFT
    - ``realworld_sft_openpi_dual_franka_tcp_rot6d``
    - Fine-tune π₀.₅ on tcp_rot6d actions.
    - ``realworld_eval_dual_franka``
    - Run eval-only deployment on the robot nodes.
    :header-rows: 1
    :widths: 24 24
    - Description
    - Wrist/global camera views plus dual-arm robot state.
    - Dual-arm tcp_rot6d: ``[L_xyz, L_rot6d, L_grip, R_xyz, R_rot6d, R_grip]``.
    - Evaluation success signal or operator-gated deployment outcome.
    - Task text in the OpenPI data/config metadata.
    Robot Nodes
    Run the robot-node installation on both ``node 0`` and ``node 1``.
    Choose ``LIBFRANKA_VERSION`` from the official `Franka compatibility
    matrix <https://frankarobotics.github.io/docs/compatibility.html>`_; avoid
    libfranka ``0.18.0``.
    export LIBFRANKA_VERSION=0.15.0       # replace with your compatible version
    bash req...
  - [M] docs/source-en/rst_source/examples/embodied/franka.rst
    Excerpt:
    Real-World RL with Franka
    =========================
    .. |huggingface| image:: /_static/svg/hf-logo.svg
    :width: 16px
    :height: 16px
    :class: inline-icon
    .. figure:: https://raw.githubusercontent.com/RLinf/misc/main/pic/franka_arm_small.jpg
    :align: center
    :width: 80%
    Franka Emika Panda arm used for the base RLinf real-world RL workflow.
    Use RLinf to train and evaluate real-world policies on a Franka Emika Panda arm. You'll set up the controller and training nodes, collect demonstrations, run SAC/RLPD or PPO-style training, and monitor safe online updates on physical hardware.
    Related Franka Setups
    Explore alternative Franka hardware, sensors, and training recipes.
    .. grid:: 1 2 2 3
    :gutter: 2
    :link: franka_reward_model
    Train Franka with a learned reward model.
    .. grid-item-card:: ZED + Robotiq
    :link: franka_zed_robotiq
    Use ZED cameras and Robotiq grippers.
    :link: franka_gello
    :link: dual_franka
    Run a two-arm Franka setup.
    :link: franka_dexhand
    Drive a Franka with a dexterous hand end-effector.
    .. grid-item-card:: Pi0 SFT
    :link: franka_pi0_sft_deploy
    Deploy a π₀ SFT policy on Franka.
    Train a real-world manipulation policy from camera observations and robot feedback.
    .. grid:: 2 4 4 4
    :gutter: 2
    CNN policy · OpenPI π₀.₅
    SAC · Cross-Q · RLPD · PPO
    Franka · RealSense/ZED · gripper
    | **You'll do:** install controller deps → collect demos → start Ray → launch real-world training → watch ``env/reward`` and videos.
    | **Prerequisites:** :doc:`Installation </rst_source/start/installation>` · Franka firmware/libfranka match · local network · safety operator.
    :header-rows: 1
    :widths: 24 24 24
    - Config / entry point
    - Description
    - ``realworld_peginsertion_rlpd_cnn_async``
    - Insert a peg at a target end-effector pose.
    - ``realworld_charger_sac_cnn_async``
    - Align and insert a charger...
  - [A] docs/source-en/rst_source/examples/embodied/franka_dexhand.rst
    Excerpt:
    Using Dexterous Hand with Franka
    ================================
    .. figure:: https://raw.githubusercontent.com/RLinf/misc/main/pic/dexhand.jpg
    :align: center
    :width: 80%
    Franka arm paired with a Ruiyan five-finger dexterous hand for real-world manipulation.
    Adapt the Franka real-world workflow to a Ruiyan five-finger dexterous hand. You'll keep the same cluster and reward-model flow, then change the end effector, teleoperation input, action layout, and dex-hand configs.
    Overview
    Run the Franka real-world recipe with a dexterous hand end effector.
    .. grid:: 2 4 4 4
    :gutter: 2
    Franka · Ruiyan dex hand · glove
    | **You'll do:** install Franka deps → install dex-hand deps → configure glove/hand → collect data → train.
    | **Prerequisites:** :doc:`franka` · :doc:`franka_reward_model` · Ruiyan hand driver · glove device.
    :header-rows: 1
    :widths: 24 24 24
    - Config / entry point
    - Description
    - ``realworld_collect_dexhand_data``
    - Collect dexterous-hand demonstrations.
    - ``realworld_dexpnp_rlpd_cnn_async``
    - Train a CNN policy with dex-hand actions.
    - Franka reward-model workflow
    - Reuse the reward-model path for dexterous manipulation.
    :header-rows: 1
    :widths: 24 24
    - Description
    - Franka camera frames plus dex-hand/glove state when configured.
    - Arm action plus dexterous-hand joint or command vector.
    - Task completion or reward-model prediction.
    - Task text from the real-world env config.
    Install the base Franka dependencies from :doc:`franka`, then install the dexterous-hand runtime in the workflow below.
    - SpaceMouse for 6-D arm motion
    - a data glove for 6-D finger control
    - the SpaceMouse left button to enable relative glove control
    The reward-model path is the same as the Franka real-world reward-model workflow described in :doc:`franka_reward_model`.
    - the default rewar...
  - [A] docs/source-en/rst_source/examples/embodied/franka_gello.rst
    Excerpt:
    Using GELLO with Franka
    =======================
    .. figure:: https://raw.githubusercontent.com/RLinf/misc/main/pic/gello.jpeg
    :align: center
    :width: 80%
    GELLO joint-level teleoperation device used to collect Franka demonstrations.
    Use GELLO as a joint-level teleoperation device for Franka data collection. You'll install ``gello_teleop``, verify the serial device, update collection configs, and monitor saved episodes.
    Overview
    Collect Franka demonstrations with joint-level GELLO control instead of SpaceMouse.
    .. grid:: 2 4 4 4
    :gutter: 2
    Teleop collection · SFT/RL downstream
    Franka demonstration collection
    Franka · GELLO · gripper
    | **Prerequisites:** :doc:`franka` · GELLO hardware · Dynamixel permissions.
    :header-rows: 1
    :widths: 24 24 24
    - Config / entry point
    - Description
    - ``gello_expert``
    - Verify live joint and gripper readings.
    - ``realworld_collect_data_gello``
    - Save successful demonstrations from GELLO teleoperation.
    - ``collect_monitor.py``
    - Follow Ray worker collection progress from logs.
    :header-rows: 1
    :widths: 24 24
    - Description
    - Same camera/state layout as the target Franka collection config.
    - GELLO joint readings converted to Franka target pose or joint action.
    - Collection success flag or downstream task reward.
    - Inherited from the downstream Franka task config.
    1. ``gello`` — the low-level driver from `gello_software <https://github.com/wuphilipp/gello_software>`_.
    2. ``gello-teleop`` — the forward-kinematics and teleoperation agent used by RLinf.
    1. Install ``gello`` (gello_software)
    large repository of robot MJCF assets used only by the upstream mujoco
    ``gello-teleop`` which ships its own Franka MJCF, so the menagerie
    inside the GELLO device. Without it, the ``GelloAgent`` will not be able
    For additional hardware configuration (e.g. setting u...

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
    3. **Reinforcement Learning**: Optimizing the policy via SAC with real-env...
