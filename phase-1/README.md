# Phase 1 — Deep Learning Foundations

Assignments A1-A5 from the [learning webapp](../webapp/index.html#a1). Each subfolder contains code + a short README on what worked and what didn't.

Planned subfolders:

- `a1-pytorch-warmup/` — tensors, autograd, MNIST MLP (~97% test acc target)
- `a2-bigram/` — char-level bigram language model on TinyShakespeare
- `a3-attention/` — single-head scaled dot-product attention from scratch
- `a4-transformer/` — multi-head attention + full transformer block (pre-norm)
- `a5-nanogpt/` — nanoGPT replication (capstone; 1500-2000 word writeup)

**Phase 1 final checkpoint** (re-explain cold, no notes):
1. Why we use scaled dot-product attention (why divide by √d).
2. Why pre-norm beats post-norm at depth.
3. What goes wrong without positional encoding and which modern variants exist.
4. The transformer block, sketched on paper from memory.
