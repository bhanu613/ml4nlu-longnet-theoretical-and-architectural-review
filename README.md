# LongNet: A Theoretical and Methodological Review

**Course:** ML4NLU — Machine Learning for Natural Language Understanding  
**Institution:** Universität Trier, Fachbereich II — Computerlinguistik und Digital Humanities  
**Lecturer:** Prof. Dr. Achim Rettinger  
**Semester:** Winter Semester 2025/26  
**Authors:** Bhanu Agarwal (1805320) · Morteza Abdollahi (17883075)  
**Seminar Presentation:** 18 December 2025

---

> **Official LongNet paper and code (original authors):**  
> Ding et al. (2023) — *LongNet: Scaling Transformers to 1,000,000,000 Tokens*  
> arXiv:2307.02486 · https://aka.ms/LongNet

---

## What this repository is

This repository collects the material for our term paper in the ML4NLU course at Universität Trier.
The paper focuses on a **theoretical and methodological analysis** of LongNet — a Transformer
variant that uses dilated attention to scale sequence length to one billion tokens while keeping
computation linear in the sequence length.

We deliberately avoided implementation and instead tried to understand the architecture deeply
enough to assess both what LongNet genuinely achieves and where its current limits are.
Working through fourteen primary papers from the efficient Transformer literature alongside the
LongNet paper itself shaped the analysis significantly.

---

## Repository contents

| Path | What it contains |
|---|---|
| `paper/` | Final term paper (PDF) |
| `slides/` | Seminar presentation slides (December 2025) |
| `figures/` | Diagrams illustrating the architecture and complexity trade-offs |
| `tables/` | Markdown comparison table of long-context Transformer architectures |

---

## Paper overview

The term paper is structured around four research questions:

1. **How does dilated attention achieve O(Nd) computation and O(log N) token dependency** while
   still allowing information to flow across the entire sequence?

2. **How does LongNet compare to prior long-context architectures** — Sparse Transformer,
   Reformer, Longformer, Transformer-XL, Performers, Memorizing Transformers, and Recurrent
   Memory Transformer — and what limitations remain?

3. **How does LongNet's distributed training strategy enable billion-token scaling**, and what
   infrastructure assumptions does that claim depend on?

4. **Given that the evaluation is code-only**, what can reasonably be concluded about LongNet's
   suitability for natural language understanding tasks like legal document analysis,
   question answering, and long-form dialogue?

The analysis covers the full architecture (segmentation, geometric dilation, multi-head offsets,
MAGNETO backbone, XPOS encodings, FlashAttention integration), a detailed complexity derivation,
a review of the reported experimental results, and a critical discussion of limitations and
future directions.

---

## Key figures in this repository

### Dilated vs Dense Attention
A side-by-side sketch comparing the full N×N dense attention matrix with the structured sparse
pattern of dilated attention across multiple scales.

### Complexity Comparison
A conceptual plot showing O(N²) vs O(N) attention cost as sequence length grows — the core
trade-off that motivates the entire paper.

### Long-Context Timeline
A timeline of Transformer context length milestones from Vaswani et al. (2017) to LongNet (2023),
showing how the field has pushed the boundary from ~512 tokens to one billion.

### Architecture Overview
A simplified schematic of how segmentation, dilation, and multi-head offsets combine in a single
dilated attention layer.

---

## Comparative table of long-context architectures

See [`tables/long_context_models.md`](tables/long_context_models.md) for a full comparison of:

| Model | Complexity | Max Context | Coverage Type | Key Limitation |
|---|---|---|---|---|
| Vanilla Transformer | O(N²d) | ~2K–8K | Dense, full | Quadratic cost |
| Sparse Transformer | O(N^{3/2}·d) | ~16K–64K | Fixed sparse | Content-independent patterns |
| Reformer | O(N log N·d) | ~64K | LSH approximate | Approximation errors |
| Longformer | O(Nd) | ~16K–32K | Sliding window + global | Global token bottleneck |
| Transformer-XL | O(N²d) per segment | ~8K–16K | Segmented recurrence | Quadratic within segment |
| Memorizing Transformers | O(Nd) + retrieval | ~262K | Dense + kNN memory | Retrieval infrastructure |
| RMT | O(Nd) per segment | ~1M | Recurrent memory slots | Memory compression loss |
| LongNet | O(Nd) | ~1B | Multi-scale dilated | Code-only evaluation so far |

---

## Personal motivation

Many of the texts we study in computational linguistics at Universität Trier, just for example- legal
documents, parliamentary debates, long historical sources — are far longer than what standard
Transformers can process in a single pass. This made LongNet a natural choice for a term paper:
we wanted to understand, at a technical level, what it would take to handle such texts as unified
sequences rather than disconnected chunks.

The paper is not about proposing improvements. It is about building a well-informed, critical
understanding of one concrete attempt to break the attention bottleneck.

---

## How to cite

If you want to reference this student project:

> Agarwal, B. & Abdollahi, M. (2026). *LongNet: Scaling Transformers to 1 Billion Tokens —
> A Theoretical and Methodological Review.* Term paper, Universität Trier, ML4NLU,
> Winter Semester 2025/26.

Please always cite the **original LongNet paper** (Ding et al., 2023) and the other primary
sources when discussing technical contributions. This repository is a student project and is
not affiliated with the original authors.

---

## References (primary)

- Ding et al. (2023). LongNet. arXiv:2307.02486. https://aka.ms/LongNet
- Vaswani et al. (2017). Attention Is All You Need. NeurIPS 2017.
- Child et al. (2019). Sparse Transformer. arXiv:1904.10509.
- Beltagy et al. (2020). Longformer. arXiv:2004.05150.
- Kitaev et al. (2020). Reformer. ICLR 2020.
- Dai et al. (2019). Transformer-XL. ACL 2019.
- Choromanski et al. (2021). Performers. ICLR 2021.
- Wu et al. (2022). Memorizing Transformers. ICLR 2022.
- Bulatov et al. (2022). Recurrent Memory Transformer. NeurIPS 2022.
- Dao et al. (2022). FlashAttention. NeurIPS 2022.
- Kaplan et al. (2020). Scaling Laws. arXiv:2001.08361.
- Brown et al. (2020). GPT-3. NeurIPS 2020.
- Rajpurkar et al. (2016). SQuAD. EMNLP 2016.
- Tay et al. (2022). Efficient Transformers: A Survey. ACM Computing Surveys.
