### Hi, I'm Rick 👋

I'm a master's student working on **embodied AI / Vision-Language-Action (VLA) models**: rigorous evaluation, per-episode failure attribution, and RL post-training. My earlier background is in LLM engineering.

This summer I'm building two projects on 3×A800 (both go public in early September, currently being polished for release):

- **vla-eval-harness**: evaluates open-source VLA models (SmolVLA, π0.5, OpenVLA-OFT) on LIBERO-Spatial under one fixed protocol, with a same-scale leaderboard, per-episode failure attribution (perception / planning / control, every failure episode reviewed on video), and the MuJoCo version-sensitivity finding below.
  <!-- W7: 补 "Headline: 87.4 / 94.4 / 97.4 (SmolVLA / π0.5 / OpenVLA-OFT) under one protocol, MuJoCo 3.2.7" -->
- **vla-rl-post-training**: GRPO post-training of OpenVLA-OFT on [RLinf](https://github.com/RLinf/RLinf), adapted from the official 8-16 GPU recipe down to 2-3×A800, with both decoding protocols reported side by side.

#### Upstream contributions

Findings from those projects, reported back to the stacks I build on:

- [huggingface/lerobot#4314](https://github.com/huggingface/lerobot/pull/4314): PR fixing a dataloader regression where delta queries on `datasets ≥ 4.4` fall back to full-row decode (including all image columns); cached column views make it **46× faster per sample**, cutting a 30k-step SmolVLA training run from ~4h to ~1.9h. Root-cause analysis in [#2895](https://github.com/huggingface/lerobot/issues/2895#issuecomment-5060174507), acknowledged by the HF `datasets` lead.
- [huggingface/lerobot#4390](https://github.com/huggingface/lerobot/issues/4390): MuJoCo version drift silently collapses LIBERO-Spatial task 5 on the same checkpoint (**98% → 12%** success): a box-box collision bugfix in MuJoCo 3.4.0 breaks the benchmark's pre-3.4 initial states. Verified with a policy-free physics probe ([gist](https://gist.github.com/Rick0525/6e6db2d1fe5f4358c980b569b123fde8)) and same-physics A/B evals; cross-reported to [LIBERO#141](https://github.com/Lifelong-Robot-Learning/LIBERO/issues/141#issuecomment-5231993900) and [RLinf#1460](https://github.com/RLinf/RLinf/issues/1460).
- [HuggingFaceVLA/libero · discussion #10](https://huggingface.co/datasets/HuggingFaceVLA/libero/discussions/10): full audit backing a community bug report on the LIBERO dataset re-release; 1690/1693 episodes carry wrong meta pointers, with complete per-split stats plus a working parquet-level workaround.

#### Contact

📫 rick0525@163.com
💼 Open to embodied-AI / robot-learning internships starting **Sept 2026** (part-time during the semester).
