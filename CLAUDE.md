# Video Generation AI Engineer — Learning Roadmap

> A self-directed curriculum for going deep on video generation and landing a role at a frontier AI lab (OpenAI/Sora, Google DeepMind/Veo, Runway, Pika, Luma, ByteDance, Tencent, Alibaba, Lightricks, Genmo, Higgsfield, Decart, World Labs).

---

## How to use this file with Claude Code

Drop this file into your project root as `CLAUDE.md`. Claude Code will read it automatically and use it as persistent context. Then use Claude Code in these modes:

### Modes

**Tutor mode** — "Explain DDPM forward process to me like I've taken multivariable calc but not measure theory. Then quiz me with 3 progressively harder questions and grade my answers."

**Paper companion** — "We're on Phase 2. Walk me through the DDPM paper section by section. Stop after each section, ask me what's confusing, and I'll respond. Don't move on until I get it."

**Code reviewer** — "Here's my from-scratch DDPM implementation. Don't fix bugs for me — point out where the math doesn't match the paper, ask me Socratic questions, and only give the answer if I'm stuck after two tries."

**Implementation pair** — "Help me implement a 3D causal VAE. I'll write the skeleton, you tell me what's wrong. Don't write more than 10 lines at a time without me asking."

**Experiment planner** — "I want to run an ablation on classifier-free guidance scale. Help me design the experiment: what to measure, what to vary, sample size, plotting strategy."

**Reading list curator** — "Given what I've read so far (see Progress Log below), what should I read this week?"

### Ground rules for Claude Code when using this file

- **No spoon-feeding.** When I'm learning, ask questions before answering. Test my understanding before moving on.
- **Be specific.** Cite paper sections, equation numbers, line numbers in code. Vague is useless.
- **Push back.** If I claim I understand something but my explanation is shaky, call it out.
- **Track progress.** Update the Progress Log at the bottom of this file at the end of each session.
- **Stay current.** The video generation field moves weekly. When relevant, suggest searching for newer papers/models.
- **Cost-aware.** Before any training run, estimate compute cost. Suggest cheaper alternatives (smaller model, smaller data, fewer steps) when appropriate.

---

## User profile (fill this in, update as you go)

```
Background: Software engineer. Major experience: microservices, frontend (Angular + React), databases.
            Last ~6 months (since ~Nov 2025): hands-on with RAG, Agentic AI, "vibe coding" — shipping LLM apps.
Current strengths: Production SWE, system design, APIs, app-level Python, LLM/agent tooling, RAG pipelines.
Current gaps: Never trained a model from scratch. Low-level PyTorch, training loops, diffusion math (ELBO,
              score matching), and ML systems (FSDP, sequence parallelism) are new territory.
Available compute: No local GPU. CPU laptop only. Will use Colab/Kaggle free tier for Phases 0-2,
                   then paid cloud GPU (RunPod likely) from Phase 3 onward. Monthly budget: TBD.
Time per week: [TBD]
Target role: Research/applied engineer at a frontier video-generation lab.
Target start date: [TBD]
```

---

## The path at a glance

| Phase | Focus | Duration | Cost estimate |
|---|---|---|---|
| 0 | Pre-flight & environment | 1-2 weeks | $0 |
| 1 | Deep learning foundations | 3-4 weeks | $0-50 |
| 2 | Diffusion fundamentals | 4-6 weeks | $50-300 |
| 3 | Image diffusion mastery | 3-4 weeks | $100-500 |
| 4 | Video diffusion core | 6-8 weeks | $300-1500 |
| 5 | Modern frontier models | 4-6 weeks | $200-1000 |
| 6 | Frontier skills (infra, evals, opt) | ongoing | varies |
| 7 | Portfolio capstone | 6-10 weeks | $1500-10000 |

Total realistic timeline: **6-10 months full-time-equivalent**. Most successful self-taught engineers I've seen hit this in 4-6 months of intense focused work, or 9-12 months alongside a job.

---

## Phase 0 — Pre-flight (1-2 weeks)

### Goals
- Working dev environment
- Honest self-assessment of starting point
- Tooling fluency

### Setup checklist
- [ ] Python 3.11+, conda/uv/poetry of choice
- [ ] PyTorch with CUDA working locally (even on a laptop GPU)
- [ ] `wandb` account for experiment tracking
- [ ] HuggingFace account, `huggingface-cli login`
- [ ] GitHub repo for this learning journey (make it public — recruiters look)
- [ ] Cloud GPU account: RunPod, Lambda, or Vast.ai (start with one)
- [ ] `tmux` or similar for long-running jobs
- [ ] Familiarity with `ffmpeg`, `imageio`, `decord`, `pyav` for video I/O

### Self-assessment quiz (have Claude Code grade you)
Ask Claude Code: "Quiz me on PyTorch fundamentals — 10 questions ranging from beginner (what's a Tensor) to intermediate (when would you use `torch.compile`, how does autograd track operations through `.detach()`)."

### Deliverable
A repo named something like `video-gen-journey` with a README declaring your goals publicly. Pin it on your GitHub profile.

---

## Phase 1 — Deep learning foundations (3-4 weeks)

### Goals
Understand transformers cold. Be able to implement one from scratch without looking up the formula.

### Required
- [ ] **Karpathy "Neural Networks: Zero to Hero"** — all 8 videos. Code along, don't just watch.
  - Special focus: makemore series, "Let's build GPT", "Let's reproduce GPT-2"
- [ ] **Implement attention from scratch** — single-head, then multi-head, then with KV cache
- [ ] **Read & re-implement**: "Attention Is All You Need", GPT-2 paper

### Math refresher (only what's needed)
- [ ] Linear algebra: matrix calculus, SVD, eigendecomposition
- [ ] Probability: change of variables, KL divergence, ELBO derivation
- [ ] **3Blue1Brown's neural network series** for intuition
- [ ] **Matrix Calculus for Deep Learning** (Parr & Howard) — skim, reference

### Project 1: nanoGPT replication
Implement, train on TinyShakespeare, then on a bigger dataset. Get a clean loss curve. Push to GitHub with a writeup explaining every design decision in your own words.

**Checkpoint**: Can you explain — without notes — why we use scaled dot-product attention (why divide by √d)? Why pre-norm beats post-norm at depth? What goes wrong without positional encoding?

---

## Phase 2 — Diffusion fundamentals (4-6 weeks)

### Goals
Diffusion models stop feeling like magic. You can derive the loss, explain the sampling process, and implement one from scratch.

### Core papers (read in this order)
1. **Sohl-Dickstein et al. 2015** — "Deep Unsupervised Learning using Nonequilibrium Thermodynamics" (the OG — skim)
2. **Ho et al. 2020** — "Denoising Diffusion Probabilistic Models" (DDPM — *master this one*)
3. **Song et al. 2021** — "Denoising Diffusion Implicit Models" (DDIM)
4. **Ho & Salimans 2022** — "Classifier-Free Diffusion Guidance"
5. **Karras et al. 2022** — "Elucidating the Design Space of Diffusion-Based Generative Models" (EDM)
6. **Lipman et al. 2023** — "Flow Matching for Generative Modeling"
7. **Liu et al. 2023** — "Flow Straight and Fast: Rectified Flow"

### Supplemental
- **Lilian Weng's "What are Diffusion Models?"** blog post — best free overview
- **Yang Song's blog** — score-based perspective, more rigorous
- **Sander Dieleman's blog posts** on diffusion — read all of them, they're treasures

### Project 2: DDPM from scratch
- Implement DDPM on MNIST → CIFAR-10
- Then implement DDIM sampling on top
- Then add classifier-free guidance with class conditioning
- **Ablations to run**: noise schedule (linear vs cosine), guidance scale sweep (0, 1, 3, 7, 15), # sampling steps (10, 50, 250, 1000)
- Write up findings with FID scores and sample grids

### Project 3: Flow matching from scratch
Same dataset, but with rectified flow. Compare sample quality and steps-to-convergence vs DDPM. Understand *why* flow matching is now preferred at the frontier.

**Checkpoint**: Derive the DDPM training objective from the ELBO on a whiteboard. Explain why CFG works mechanistically (not just "it makes samples better"). Have Claude Code grill you.

---

## Phase 3 — Image diffusion mastery (3-4 weeks)

### Goals
Understand Stable Diffusion and DiT architecturally. Be ready to extend to video.

### Core papers
1. **Rombach et al. 2022** — "High-Resolution Image Synthesis with Latent Diffusion Models" (Stable Diffusion)
2. **Peebles & Xie 2022** — "Scalable Diffusion Models with Transformers" (DiT — *master this*)
3. **Esser et al. 2024** — "Scaling Rectified Flow Transformers for High-Resolution Image Synthesis" (SD3 / MMDiT)
4. **FLUX.1 technical report** (Black Forest Labs)
5. **Stability AI's SDXL paper** for VAE design choices

### Concepts to nail
- VAE training (perceptual loss, adversarial loss, why latent diffusion works)
- Cross-attention conditioning vs in-context conditioning (MMDiT style)
- Text encoders: CLIP, T5, UMT5 — why bigger text encoders help
- Noise schedules: shifted, logSNR, why high-res needs different schedules
- Sampler design space: ancestral, DPM-Solver, DPM-Solver++, UniPC

### Project 4: Small DiT for images
- Train a 50-200M param DiT on a focused dataset (CelebA-HQ at 64x64, or a Pokemon dataset, or your own scraped niche)
- Use a pretrained VAE (don't train your own yet)
- Use T5-small as text encoder
- Implement classifier-free guidance, DDIM and DPM-Solver++ sampling
- **Budget**: ~$50-200 on RunPod with 1-2 H100s

### Project 5 (optional, but high-signal): Train your own VAE
Train a small image VAE end-to-end with perceptual + KL + adversarial loss. This teaches you things papers gloss over.

**Checkpoint**: Read the DiT paper. Without looking at it, sketch the architecture on paper. Explain what adaLN-Zero does and why it matters. Have Claude Code review.

---

## Phase 4 — Video diffusion core (6-8 weeks)

This is where the field gets you hired.

### Goals
Video-specific architecture mastery: 3D VAEs, spatiotemporal attention, conditioning for video, temporal coherence.

### Core papers (chronological — read for intuition)
1. **Ho et al. 2022** — "Video Diffusion Models" (Google, foundational)
2. **Singer et al. 2022** — "Make-A-Video" (Meta)
3. **Ho et al. 2022** — "Imagen Video"
4. **Blattmann et al. 2023** — "Stable Video Diffusion" (read the data curation appendix — gold)
5. **OpenAI 2024** — "Video generation models as world simulators" (Sora technical report)
6. **Yang et al. 2024** — "CogVideoX" (clean architectural exposition)
7. **Polyak et al. 2024** — "Movie Gen" (Meta — *read the whole 90-page paper*, most educational)
8. **Kong et al. 2024** — "HunyuanVideo" (Tencent — disclosed training recipes)
9. **HaCohen et al. 2024** — "LTX-Video" (real-time generation)
10. **Wan team 2024-2025** — "Wan 2.1" and "Wan 2.2" (Alibaba, MoE for video)

### Critical concepts
- **3D causal VAEs**: temporal compression, why causality matters for streaming
- **Spatiotemporal attention**: full 3D vs factorized space-time vs windowed
- **Patchification for video**: how patches map across time
- **Text-to-video vs image-to-video vs video-to-video** conditioning
- **Long video generation**: autoregressive chunking, sliding window, hierarchical
- **Camera/identity/motion control**: ControlNet for video, IP-Adapter style approaches
- **Sequence parallelism**: Ulysses, Ring Attention — required for long videos
- **VBench**: how the standard eval works and where it's blind

### Project 6: Tiny video DiT (the big one)
- Reproduce a small video DiT (~200M-500M params)
- Start with UCF-101 or a small subset of WebVid/Panda-70M
- Use a pretrained 3D VAE if you can (e.g., from CogVideoX or Open-Sora)
- 16-frame, 256x256, 8fps clips to start
- Goal: legible motion, not photoreal
- **Budget**: ~$300-1500. 1×8-H100 node for 3-10 days at spot pricing

### Project 7: Fork and contribute
Pick one open codebase and make a real contribution:
- **HunyuanVideo** — well-engineered, large community
- **Wan 2.2** — frontier MoE architecture
- **CogVideoX** — cleanest reference
- **Open-Sora** — community-driven
- **diffusers** (HuggingFace) — high-impact, easy to merge small things

What to contribute: a new sampler, a memory optimization, a controllability adapter, an eval, a bug fix. Get a PR merged.

**Checkpoint**: Pick any of the papers above at random and give a 10-minute talk to Claude Code on the architecture, training data, key contribution, and limitations. Get graded.

---

## Phase 5 — Modern frontier models deep dive (4-6 weeks)

### Goals
Be able to discuss the *current* state of the art at interview depth.

### Tasks
- [ ] Maintain a running comparison doc: HunyuanVideo vs Wan 2.2 vs Mochi-1 vs LTX-Video vs CogVideoX — architecture, VAE, training recipe, known weaknesses
- [ ] Read every major paper as it drops (the field moves weekly)
- [ ] Follow on X/Twitter: video model authors, Sander Dieleman, EMostaque, lab accounts
- [ ] Subscribe to: AK's tweets, Hugging Face daily papers, Arxiv Sanity for `cs.CV`

### Track these research threads
- **MoE for video** — Wan 2.2 launched this; expect more
- **Joint audio-video generation** — Veo 3, Movie Gen Audio
- **Real-time / streaming generation** — LTX, Decart
- **Controllability** — camera, identity, motion, physics
- **Distillation** — turning 50-step models into 4-step
- **Video as world models** — for robotics, agents (Wayve, 1X, World Labs)
- **Long-form coherence** — minute-plus videos with consistent characters

### Project 8: Position paper
Write a 3000-5000 word blog post: "The state of video generation in [month] [year] — what's solved, what's broken, where it's going." Post publicly. This is high-signal for recruiters and forces synthesis.

---

## Phase 6 — Frontier engineering skills (ongoing, parallel to above)

These are the skills that separate "researched diffusion" from "actually employable at a frontier lab."

### Distributed training
- [ ] FSDP fundamentals (read PyTorch docs, run examples)
- [ ] Sequence parallelism: implement Ring Attention or read Ulysses
- [ ] Activation checkpointing tradeoffs
- [ ] Tensor parallelism basics
- [ ] Communication primitives: all-gather, all-reduce, reduce-scatter

### Inference optimization
- [ ] Step distillation (consistency models, LCM)
- [ ] Quantization: FP8 for inference, when it hurts quality
- [ ] KV cache for autoregressive video
- [ ] Sparse attention patterns
- [ ] `torch.compile`, CUDA graphs

### Data engineering at scale
- [ ] Video pipelines: scene detection (PySceneDetect), dedup (perceptual hashing)
- [ ] Captioning at scale with a VLM (LLaVA, Qwen-VL, InternVL)
- [ ] Filtering: aesthetic scoring, motion scoring, text detection removal
- [ ] Storage: WebDataset format, sharding strategies

### Evals
- [ ] VBench: run it, understand each dimension
- [ ] Build a custom eval for something VBench misses (long-range identity, physics)
- [ ] Human eval pipelines (basic A/B preference framework)

### CUDA / kernel basics (optional but powerful)
- [ ] Read a Triton tutorial
- [ ] Understand FlashAttention at a high level
- [ ] Know what fusing operations does for memory bandwidth

---

## Phase 7 — Portfolio capstone (6-10 weeks)

### The bar
A single project that:
1. Demonstrates depth in video generation
2. Has a clear technical insight or novel result
3. Is reproducible (code public, weights released if possible)
4. Has a great writeup (blog post + arXiv preprint if quality is there)
5. Could be discussed for an hour in an interview

### Project ideas (pick one, scoped to your compute budget)

**Low compute ($500-3000):**
- Novel controllability adapter on top of an open model (camera control, identity preservation, motion transfer) — LoRA-scale finetune on Wan 2.2 or HunyuanVideo
- Distillation: turn an open 50-step model into a 4-step model. Ship a real-time demo
- An eval framework that exposes a specific failure mode (physics violations, identity drift in long clips) — benchmark all open models
- Domain-specific fine-tune with proper evals (medical imaging video, robotics sim, animation style)

**Medium compute ($3000-15000):**
- Clean reproduction of a recent paper with novel ablations the authors didn't run
- A small (~500M-1B) video model trained on a curated dataset with a specific architectural twist
- A novel conditioning scheme (e.g., pose-conditioned video, depth-conditioned video) trained on top of an existing base

**High compute ($15K+):**
- Only do this if you can get sponsored compute (grants, lab access, friendly cloud credits)
- A genuinely new training recipe at small scale with strong empirical results

### Deliverables
- [ ] GitHub repo with clean code, README, reproduction instructions
- [ ] Blog post (5000-10000 words) explaining the work
- [ ] Demo (HuggingFace Space, Gradio, or hosted video samples)
- [ ] Tweet thread / LinkedIn post — distribution matters
- [ ] Optional but high-leverage: a short video walkthrough on YouTube

### Application strategy (parallel)
- [ ] Identify 15-20 target companies, prioritize 5
- [ ] Find the right person (research engineer, hiring manager, not generic recruiter)
- [ ] Cold email with: 1-paragraph intro, link to capstone, specific reason for that company
- [ ] Open-source contributions to their codebases as warm intros
- [ ] Attend a conference if possible (NeurIPS, ICML, CVPR, ICLR)

---

## Recurring weekly rituals

- **Monday**: Plan the week. Update Progress Log with goals.
- **Daily**: 1 hour reading (paper, blog, codebase), 2+ hours hands-on
- **Friday**: "What did I learn this week?" writeup. Even one paragraph.
- **Sunday**: Read 1 new paper, summarize in 3 sentences in this file

---

## Progress Log

> Have Claude Code append to this section at the end of each session.

### Week 1 (date: ___)
- Phase:
- What I did:
- What I struggled with:
- What I'll do next:

### Papers read
| Date | Paper | Key insight | My summary (link to notes) |
|---|---|---|---|
|  |  |  |  |

### Projects shipped
| Project | Repo | Writeup | Date |
|---|---|---|---|
|  |  |  |  |

### Compute spent
| Date | Provider | Hours | Cost | Purpose |
|---|---|---|---|---|
|  |  |  |  |  |

---

## Resources directory

### Codebases to study (in order of pedagogical value)
- `karpathy/nanoGPT` — start here
- `huggingface/diffusers` — the swiss army knife
- `lucidrains/denoising-diffusion-pytorch` — clean DDPM
- `facebookresearch/DiT` — original DiT
- `THUDM/CogVideoX` — cleanest open video DiT
- `hpcaitech/Open-Sora` — community Sora reproduction
- `Tencent/HunyuanVideo` — production-grade
- `Wan-Video/Wan2.2` — frontier MoE
- `Lightricks/LTX-Video` — speed-optimized

### Channels / blogs / people
- Lilian Weng's blog (lilianweng.github.io)
- Sander Dieleman's blog (sander.ai)
- Yang Song's blog
- AK on X (@_akhaliq) for daily papers
- Hugging Face Daily Papers (huggingface.co/papers)
- Karpathy on YouTube

### Conferences (papers from these are highest-signal)
- NeurIPS, ICML, ICLR — general ML
- CVPR, ICCV, ECCV — vision specifically
- SIGGRAPH — graphics-adjacent video work

### Where to rent GPUs (cheapest first, roughly)
- Vast.ai (marketplace, cheapest spot)
- RunPod (good UX, spot + on-demand)
- Lambda Labs (reliable, single-GPU friendly)
- Crusoe / GMI / Nebius (for multi-node serious work)
- AWS/GCP/Azure (avoid for personal projects — 2-4x markup)

---

## Anti-patterns to avoid

- **Tutorial purgatory.** After Karpathy + a couple foundational papers, *stop watching tutorials*. Build things.
- **Reading without implementing.** A paper you haven't coded against is a paper you don't understand.
- **Hoarding compute credits.** Waiting for the "right" project means never starting. Run the bad first experiment.
- **Comparing to Sora/Veo.** Your goal is to demonstrate *capability and trajectory*, not match billion-dollar training runs.
- **Generic projects.** "I trained a small video model on UCF-101" is a starting point, not a portfolio piece. The portfolio version has a novel angle.
- **Not writing.** Every project needs a public writeup. Recruiters can't read your code, but they can read your blog.
- **Skipping evals.** "It looks good" is not a result. Quantify everything.

---

## Final note

The people who get hired at frontier video labs are not the ones who read the most papers or rented the most GPUs. They are the ones who:

1. Have shipped something publicly that demonstrates real understanding
2. Can discuss tradeoffs in their work with intellectual honesty
3. Have a perspective on where the field is going
4. Show momentum — are visibly better at month 6 than month 1

Use this file to maintain that momentum. Update it weekly. Be honest about what you don't know. Ask Claude Code hard questions, not easy ones.

Good luck. Ship things.