# ArXiv AI Research Digest 2026-05-15

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-05-15 10:00 UTC

---

# ArXiv AI Research Digest — 2026-05-15

## Today's Highlights

Several papers today push toward **evaluating and improving consistency** in generative models: EntityBench introduces a rigorous benchmark for entity-consistent multi-shot video generation, while Quantitative Video World Model Evaluation proposes geometric consistency metrics for video world models. On the **agentic AI** front, FutureSim presents a grounded replay framework for evaluating adaptive agents, and OpenDeepThink explores parallel reasoning with Bradley–Terry aggregation to improve test-time compute scaling. A notable **safety cluster** emerges around LLM quantization and backdoors: MetaBackdoor reveals positional encoding as a novel attack surface, and Forgetting That Sticks demonstrates that quantization can reverse machine unlearning—raising critical questions for deployed model governance.

---

## Key Papers

### 🧠 Large Language Models

**When Are Two Networks the Same? Tensor Similarity for Mechanistic Interpretability**
http://arxiv.org/abs/2605.15183v1 | Nissen Gonzalez et al.
Introduces a basis-independent tensor similarity metric for verifying whether two neural network circuits implement the same computation, addressing a foundational gap in mechanistic interpretability.

**MetaBackdoor: Exploiting Positional Encoding as a Backdoor Attack Surface in LLMs**
http://arxiv.org/abs/2605.15172v1 | Wen et al.
Demonstrates that positional encodings can serve as backdoor triggers in LLMs, sidestepping content-based detection and revealing a critical vulnerability in transformer architectures.

**Forgetting That Sticks: Quantization-Permanent Unlearning via Circuit Attribution**
http://arxiv.org/abs/2605.15138v1 | Sadhu et al.
Shows that 4-bit post-training quantization can reverse machine unlearning, and proposes a circuit-attribution method to make unlearning persistent under quantization—vital for privacy compliance.

**Training ML Models with Predictable Failures**
http://arxiv.org/abs/2605.15134v1 | Schwarzer & Niekum
Presents a method to extrapolate rare failure rates from limited evaluation data, enabling more reliable pre-deployment safety assessment of ML systems.

**RoSHAP: A Distributional Framework and Robust Metric for Stable Feature Attribution**
http://arxiv.org/abs/2605.15154v1 | Xiang et al.
Proposes a distributional approach to SHAP values that quantifies and mitigates stochastic variation in feature attributions across different train-test splits, improving interpretability reliability.

### 🤖 Agents & Reasoning

**FutureSim: Replaying World Events to Evaluate Adaptive Agents**
http://arxiv.org/abs/2605.15188v1 | Goel et al.
Builds grounded simulations that replay real-world events chronologically, providing a realistic and efficient evaluation protocol for agents that must adapt to new information in dynamic environments.

**OpenDeepThink: Parallel Reasoning via Bradley–Terry Aggregation**
http://arxiv.org/abs/2605.15177v1 | Zhou et al.
Scales test-time compute breadth-wise by sampling multiple reasoning candidates in parallel and selecting the best via a learned Bradley–Terry preference model, offering a practical alternative to depth-only scaling.

**Self-Distilled Agentic Reinforcement Learning**
http://arxiv.org/abs/2605.15155v1 | Lu et al.
Introduces On-Policy Self-Distillation (OPSD) to augment RL with dense token-level supervision from a teacher model, addressing sparse reward bottlenecks in long-horizon agentic tasks.

**Natural Synthesis: Outperforming Reactive Synthesis Tools with Large Reasoning Models**
http://arxiv.org/abs/2605.15131v1 | Schmitt et al.
Applies large reasoning models to reactive synthesis—automatically constructing hardware circuits from logical specifications—achieving better results than specialized formal verification tools.

**CLOVER: Closed-Loop Value Estimation & Ranking for End-to-End Autonomous Driving Planning**
http://arxiv.org/abs/2605.15120v1 | Ang et al.
Bridges the training-evaluation mismatch in end-to-end driving planners by incorporating closed-loop safety metrics directly into the value estimation and ranking of trajectory candidates.

### 🔧 Methods & Frameworks

**EntityBench: Towards Entity-Consistent Long-Range Multi-Shot Video Generation**
http://arxiv.org/abs/2605.15199v1 | He et al.
Proposes a benchmark and evaluation protocol for maintaining consistent characters, objects, and locations across multiple video shots, addressing a key limitation in narrative video generation.

**ATLAS: Agentic or Latent Visual Reasoning? One Word is Enough for Both**
http://arxiv.org/abs/2605.15198v1 | Guo et al.
Introduces an efficient visual reasoning framework that uses a single learned token to switch between agentic (image-generating) and latent (representation-based) reasoning, avoiding the computational cost of full image generation.

**Eradicating Negative Transfer in Multi-Physics Foundation Models via Sparse Mixture-of-Experts Routing**
http://arxiv.org/abs/2605.15179v1 | Sharma & Sharma
Applies sparse MoE routing to prevent gradient conflict when co-training neural operators on disparate PDE regimes, enabling scalable scientific foundation models.

**Croissant Baker: Metadata Generation for Discoverable, Governable, and Reusable ML Datasets**
http://arxiv.org/abs/2605.15079v1 | Al Attrach et al.
Automates the generation of Croissant metadata (the emerging ML dataset standard) directly from datasets, lowering barriers to compliance and reproducibility for ML practitioners.

### 📊 Applications & Multimodal

**Evidential Reasoning Advances Interpretable Real-World Disease Screening**
http://arxiv.org/abs/2605.15171v1 | Lian et al.
Combines evidential deep learning with case-based reasoning for medical image screening, producing interpretable predictions with calibrated uncertainty and historical case references.

**Text Knows What, Tables Know When: Clinical Timeline Reconstruction via Retrieval-Augmented Multimodal Alignment**
http://arxiv.org/abs/2605.15168v1 | Kumar et al.
Aligns unstructured clinical narratives with structured temporal data to reconstruct precise patient timelines, improving trajectory modeling for complex conditions like sepsis.

**SpeakerLLM: A Speaker-Specialized Audio-LLM for Speaker Understanding and Verification Reasoning**
http://arxiv.org/abs/2605.15044v1 | Nam et al.
Develops an audio LLM specialized in speaker identification and verification reasoning, enabling user authorization and personalization in audio-first AI agents.

---

## Research Trend Signal

Three emerging directions stand out from today's submissions. **First**, a cluster of papers around "on-policy self-distillation" and "dense token-level supervision" (Self-Distilled Agentic RL; Learning from Language Feedback via Variational Policy Distillation) suggests the field is moving beyond sparse reward signals toward richer, more granular training signals for LLMs and agents. **Second**, the intersection of formal verification and LLMs is gaining traction: Natural Synthesis applies reasoning LLMs to reactive synthesis, while several papers examine quantization's effects on model safety (Forgetting That Sticks, Widening the Gap, MetaBackdoor), indicating a growing concern for provable properties in deployed systems. **Third**, evaluation itself is being rethought: FutureSim and EntityBench propose grounded, replay-based evaluations for agents and generative models, while Quantitative Video World Model Evaluation and Training ML Models with Predictable Failures push toward more rigorous and empirically grounded assessment of model capabilities and failure modes.

---

## Worth Deep Reading

1. **MetaBackdoor: Exploiting Positional Encoding as a Backdoor Attack Surface in LLMs** — This paper identifies a fundamentally new attack vector (positional encodings) that bypasses existing content-based defenses. The implications for model deployment and supply-chain security are significant, and the methodology for exploiting architectural components as triggers is likely to inspire follow-up work.

2. **Forgetting That Sticks: Quantization-Permanent Unlearning via Circuit Attribution** — As unlearning becomes a regulatory requirement (e.g., "right to be forgotten"), this paper's finding that standard quantization reverses unlearning is a practical crisis for deployed ML. The proposed circuit-attribution fix is technically grounded and addresses a concrete deployment problem.

3. **Natural Synthesis: Outperforming Reactive Synthesis Tools with Large Reasoning Models** — Demonstrates that LLM-based reasoning can outperform specialized formal verification tools on a classic hard problem (reactive synthesis). This result bridges two communities and suggests that reasoning LLMs may serve as viable alternatives to domain-specific algorithmic solvers in logic-heavy domains.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*