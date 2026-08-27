### Hi, I'm Rick 👋

I'm a master's student working on **embodied AI / Vision-Language-Action (VLA) models**: rigorous evaluation, per-episode failure attribution, and RL post-training. My earlier background is in LLM engineering.

This summer I built two projects on a shared 3×A800 server:

- **[vla-libero-eval](https://github.com/Rick0525/vla-libero-eval)**: evaluates open-source VLA models (SmolVLA, π0.5, OpenVLA-OFT) on LIBERO-Spatial under one fixed protocol, with a same-scale leaderboard, per-episode failure attribution (perception / planning / control, every failure episode reviewed on video), and the MuJoCo version-sensitivity finding below. Headline: **87.4 / 94.4 / 97.4** (SmolVLA 0.45B / π0.5 3.3B / OpenVLA-OFT 7.5B) under one protocol, MuJoCo 3.2.7.
- **[vla-rl-post-training](https://github.com/Rick0525/vla-rl-post-training)**: reproduces the SimpleVLA-RL GRPO recipe (originally 8×A800 full-parameter) on **2×A800 + LoRA** via [RLinf](https://github.com/RLinf/RLinf): **56.0 → 93.8** on LIBERO-Spatial using ~23% of the official data budget; the official checkpoint scores 96.4 on the same evaluator. Includes a preregistered controlled experiment on a dealing-strategy intervention (speedup confirmed, score gain unproven).

#### Upstream contributions

Findings from those projects, reported back to the stacks I build on:

- [huggingface/lerobot#4314](https://github.com/huggingface/lerobot/pull/4314): PR fixing a dataloader regression where delta queries on `datasets ≥ 4.4` fall back to full-row decode (including all image columns); cached column views make it **46× faster per sample**, cutting a 30k-step SmolVLA training run from ~4h to ~1.9h. Root-cause analysis in [#2895](https://github.com/huggingface/lerobot/issues/2895#issuecomment-5060174507), acknowledged by the HF `datasets` lead.
- [huggingface/lerobot#4390](https://github.com/huggingface/lerobot/issues/4390): MuJoCo version drift silently collapses LIBERO-Spatial task 5 on the same checkpoint (**98% → 12%** success): a box-box collision bugfix in MuJoCo 3.4.0 breaks the benchmark's pre-3.4 initial states. Verified with a policy-free physics probe ([gist](https://gist.github.com/Rick0525/6e6db2d1fe5f4358c980b569b123fde8)) and same-physics A/B evals; cross-reported to [LIBERO#141](https://github.com/Lifelong-Robot-Learning/LIBERO/issues/141#issuecomment-5231993900) and [RLinf#1460](https://github.com/RLinf/RLinf/issues/1460).
- [HuggingFaceVLA/libero · discussion #10](https://huggingface.co/datasets/HuggingFaceVLA/libero/discussions/10): full audit backing a community bug report on the LIBERO dataset re-release; 1690/1693 episodes carry wrong meta pointers, with complete per-split stats plus a working parquet-level workaround.

#### Contact

📫 rick0525@163.com
💼 Open to embodied-AI / robot-learning internships starting **Sept 2026** (part-time during the semester).
