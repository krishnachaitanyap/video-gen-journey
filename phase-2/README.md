# Phase 2 — Diffusion Fundamentals

Assignments A6-A10 from the [learning webapp](../webapp/index.html#a6). Phase 2 is where diffusion stops feeling like magic — derive the loss from the ELBO, implement DDPM from scratch, then beat it with flow matching.

Planned subfolders:

- `a6-forward-process/` — DDPM forward-process visualization + cosine vs linear schedule
- `a7-ddpm-mnist/` — DDPM from scratch on MNIST (small U-Net, ε-prediction)
- `a8-ddim/` — DDIM sampling on the trained DDPM (no retraining; sampler is a free choice)
- `a9-cfg-cifar10/` — class-conditional CIFAR-10 with classifier-free guidance + full ablation set (guidance scale sweep, sampling steps, FID)
- `a10-flow-matching/` — rectified flow head-to-head with DDPM under matched compute (capstone; 2000-3000 word writeup)

**Compute reality**: Phase 2 is the first phase that costs real money. Budget ~$50 on RunPod / Colab Pro for A9 + A10.

**Phase 2 final checkpoint** (re-explain cold):
1. Derive L_simple from the ELBO on a whiteboard.
2. Explain DDPM vs DDIM samplers in 60 seconds.
3. Explain why CFG works mechanistically (not "it makes samples better").
4. Argue for or against flow matching vs DDPM, citing your own A10 results.
