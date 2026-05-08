# ArXiv AI Research Digest 2026-05-08

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-05-08 06:18 UTC

---

# 🧠 ArXiv AI Research Digest — 2026-05-08

## Today's Highlights

Today's submissions reveal a strong pivot toward **modular and agentic architectures**, with multiple papers rethinking the Mixture-of-Experts paradigm for efficiency and emergent specialization. **Agentic AI for scientific discovery** is accelerating rapidly, with dedicated systems for mathematics, computational fluid dynamics, and neuroimaging analysis—suggesting a maturation from toy demonstrations to real research workflows. A cluster of papers addresses the **evaluation crisis** in LLMs, exposing fundamental flaws in global leaderboards and proposing rigorous alternatives for safety assessment. Additionally, **reinforcement learning for long-horizon reasoning** receives renewed theoretical attention, with work establishing expressiveness as the key bottleneck in scaling RL for LLMs.

---

## Key Papers

### 🧠 Large Language Models (architecture, training, alignment, evaluation)

**UniPool: A Globally Shared Expert Pool for Mixture-of-Experts**
http://arxiv.org/abs/2605.06665v1
Minbin Huang, Han Shi, Chuanyang Zheng et al.
Challenges the rigid per-layer expert allocation in MoE architectures, proposing a globally shared expert pool that decouples depth scaling from parameter growth—potentially unlocking far more parameter-efficient LLMs.

**EMO: Pretraining Mixture of Experts for Emergent Modularity**
http://arxiv.org/abs/2605.06663v1
Ryan Wang, Akshita Bhagia, Sewon Min
Demonstrates that pretraining MoE models can induce emergent modularity, enabling the extraction of narrow-capability subnetworks (e.g., code-only, math-only) without full-model deployment.

**Why Global LLM Leaderboards Are Misleading: Small Portfolios for Heterogeneous Supervised ML**
http://arxiv.org/abs/2605.06656v1
Jai Moondra, Ayela Chughtai, Bhargavi Lanka et al.
Analyzes ~89K pairwise comparisons across 52 LLMs in 116 languages, showing that global Bradley-Terry rankings are fundamentally misleading—nearly 2/3 of comparisons defy the global model.

**When No Benchmark Exists: Validating Comparative LLM Safety Scoring Without Ground-Truth Labels**
http://arxiv.org/abs/2605.06652v1
Sushant Gautam, Finn Schwall, Annika Willoch Olstad et al.
Formalizes the problem of benchmarkless comparative safety scoring, providing a contractual framework for scenario-based audits when labeled safety data is unavailable.

**The Structural Origin of Attention Sink: Variance Discrepancy, Super Neurons, and Dimension Disparity**
http://arxiv.org/abs/2605.06611v1
Siquan Li, Kaiqi Jiang, Jiacheng Sun et al.
Provides a mechanistic explanation for the attention sink phenomenon, tracing it to variance discrepancy between initial and non-initial tokens and the emergence of "super neurons."

**Cited but Not Verified: Parsing and Evaluating Source Attribution in LLM Deep Research Agents**
http://arxiv.org/abs/2605.06635v1
Hailey Onweller, Elias Lumer, Austin Huber et al.
Exposes the unreliability of citations in LLM-generated research reports, proposing methods for parsing and verifying source attribution in deep research agents.

---

### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

**AI Co-Mathematician: Accelerating Mathematicians with Agentic AI**
http://arxiv.org/abs/2605.06651v1
Daniel Zheng, Ingrid von Glehn, Yori Zwols et al.
Introduces an interactive workbench where mathematicians collaborate with AI agents for open-ended research, supporting ideation, literature review, and hypothesis generation—a significant step toward AI-assisted discovery.

**StraTA: Incentivizing Agentic Reinforcement Learning with Strategic Trajectory Abstraction**
http://arxiv.org/abs/2605.06642v1
Xiangyuan Xue, Yifan Zhou, Zidong Wang et al.
Addresses the credit assignment problem in long-horizon agentic tasks by abstracting trajectories into strategic segments, improving both exploration and reward attribution for LLM-based agents.

**Recursive Agent Optimization**
http://arxiv.org/abs/2605.06639v1
Apurva Gandhi, Satyaki Chakraborty, Xiangjun Wang et al.
Trains agents that can recursively spawn and delegate sub-tasks to new instantiations of themselves, implementing a natural inference-time scaling algorithm that could generalize to complex hierarchical problems.

**Can RL Teach Long-Horizon Reasoning to LLMs? Expressiveness Is Key**
http://arxiv.org/abs/2605.06638v1
Tianle Wang, Zhaoyang Wang, Guangchen Lan et al.
Introduces ScaleLogic, a synthetic reasoning framework showing that the expressiveness of the reward signal—not just RL algorithm choice—is the critical bottleneck for scaling reasoning with RL.

**SkillOS: Learning Skill Curation for Self-Evolving Agents**
http://arxiv.org/abs/2605.06614v1
Siru Ouyang, Jun Yan, Yanfei Chen et al.
Addresses the challenge of agents learning from past interactions by proposing a skill curation mechanism that distills reusable skills from streaming tasks, enabling continuous self-improvement.

**MASPO: Joint Prompt Optimization for LLM-based Multi-Agent Systems**
http://arxiv.org/abs/2605.06623v1
Zhexuan Wang, Xuebo Liu, Li Wang et al.
Tackles the non-trivial problem of jointly optimizing prompts across interacting agents in multi-agent systems, showing significant improvements over individually-optimized prompts.

**Superintelligent Retrieval Agent: The Next Frontier of Information Retrieval**
http://arxiv.org/abs/2605.06647v1
Zeyu Yang, Qi Ma, Jason Chen et al.
Frames retrieval-augmented agents as active, strategic information seekers rather than black-box query issuers, proposing a new paradigm for knowledge base interaction.

---

### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

**Verifier-Backed Hard Problem Generation for Mathematical Reasoning**
http://arxiv.org/abs/2605.06660v1
Yuhang Lai, Jiazhan Feng, Yee Whye Teh et al.
Introduces a method for generating valid, novel, and challenging mathematical problems using verifier feedback—critical for advancing LLM training and autonomous scientific research.

**Beyond Negative Rollouts: Positive-Only Policy Optimization with Implicit Negative Gradients**
http://arxiv.org/abs/2605.06650v1
Mingwei Xu, Hao Fang
Proposes a novel RLVR approach that eliminates the need for negative rollouts by computing implicit negative gradients from correct trajectories alone, simplifying the training pipeline for reasoning LLMs.

**Optimizer-Model Consistency: Full Finetuning with the Same Optimizer as Pretraining Forgets Less**
http://arxiv.org/abs/2605.06654v1
Yuxing Liu, Jianyu Wang, Tong Zhang
Presents a simple but impactful finding: maintaining the same optimizer between pretraining and finetuning significantly reduces catastrophic forgetting in LLMs.

**Are We Making Progress in Multimodal Domain Generalization? A Comprehensive Benchmark Study**
http://arxiv.org/abs/2605.06643v1
Hao Dong, Hongzhao Li, Shupan Li et al.
A much-needed critical evaluation of MMDG methods, revealing that many reported gains are artifacts of inconsistent evaluation rather than genuine algorithmic progress.

**Transformers Efficiently Perform In-Context Logistic Regression via Normalized Gradient Descent**
http://arxiv.org/abs/2605.06609v1
Chenyang Zhang, Yuan Cao
Provides theoretical grounding for in-context learning by showing that Transformers can implement normalized gradient descent for logistic regression, bridging algorithmic and mechanistic understanding.

**Inductive Venn-Abers and related regressors**
http://arxiv.org/abs/2605.06646v1
Ivan Petej, Vladimir Vovk
Generalizes Venn-Abers predictors from binary classification to unbounded regression, expanding the applicability of provably valid probabilistic predictions.

---

### 📊 Applications (domain-specific, multimodal, code generation)

**NeuroAgent: LLM Agents for Multimodal Neuroimaging Analysis and Research**
http://arxiv.org/abs/2605.06584v1
Lujia Zhong, Yihao Xia, Jianwei Zhang et al.
Introduces an LLM-based agent system that orchestrates complex neuroimaging preprocessing, quality control, and downstream analysis across heterogeneous toolchains—a concrete contribution to medical AI.

**AI CFD Scientist: Toward Open-Ended Computational Fluid Dynamics Discovery with Physics-Aware AI Agents**
http://arxiv.org/abs/2605.06607v1
Nithin Somasekharan, Rabi Pathak, Manushri Dhanakoti et al.
Extends the agentic science loop to high-fidelity physical simulation, addressing the unique challenge that solver completion does not guarantee physical validity.

**DINORANKCLIP: DINOv3 Distillation and Injection for Vision-Language Pretraining with High-Order Ranking Consistency**
http://arxiv.org/abs/2605.06592v1
Shuyang Jiang, Nan Yu, Yiming Zhang et al.
Addresses fundamental weaknesses in CLIP by distilling DINOv3's fine-grained visual representations and enforcing ranking consistency among unmatched pairs.

**Automated Clinical Report Generation for Remote Cognitive Remediation: Comparing Knowledge-Engineered Templates and LLMs in Low-Resource Settings**
http://arxiv.org/abs/2605.06594v1
Yongxin Zhou, Fabien Ringeval, François Portet
Compares template-based and LLM-based approaches for generating clinical reports from remote therapy data, addressing a practical bottleneck in cognitive rehabilitation.

**Patch2Vuln: Agentic Reconstruction of Vulnerabilities from Linux Distribution Binary Patches**
http://arxiv.org/abs/2605.06601v1
Isaac David, Arthur Gervais
Demonstrates that LLM-based agents can reconstruct vulnerability details from binary patches alone, a significant capability for security operations in resource-constrained settings.

---

## Research Trend Signal

Two converging trends dominate today's batch. First, **Mixture-of-Experts is being reimagined from the ground up**: rather than treating MoE as a fixed architectural choice, papers like UniPool and EMO explore dynamic expert allocation and emergent modularity, pointing toward models that can adapt their computational graph to the task at hand. Second, **agentic AI for scientific discovery is becoming a concrete subfield**: the AI Co-Mathematician, AI CFD Scientist, and NeuroAgent each address the full research workflow—not just isolated tasks—and grapple with issues of validity, verification, and human collaboration. A subtler but important signal is the growing **skepticism toward evaluation practices**: papers on leaderboard flaws, benchmarkless safety scoring, and citation verification suggest that the field is beginning to take its measurement infrastructure as seriously as its models. Finally, the theoretical work on attention sinks and in-context learning mechanisms reflects a maturation toward understanding *why* models work, not just *that* they work.

---

## Worth Deep Reading

1. **AI Co-Mathematician** (http://arxiv.org/abs/2605.06651v1) — One of the most comprehensive treatments of AI-assisted scientific discovery to date, addressing the full iterative workflow rather than narrow problem-solving. The design decisions around human-in-the-loop interaction and open-ended exploration are likely to influence the next generation of research tools.

2. **The Structural Origin of Attention Sink** (http://arxiv.org/abs/2605.06611v1) — Provides the first rigorous mechanistic explanation for a phenomenon observed in virtually every deployed LLM. Understanding why attention sinks emerge is essential for both architectural improvements and interpretability research.

3. **Why Global LLM Leaderboards Are Misleading** (http://arxiv.org/abs/2605.06656v1) — With nearly 90K comparisons across 116 languages, this paper delivers empirical evidence that our primary method for comparing LLM quality is fundamentally broken. Essential reading for anyone who trains, evaluates, or deploys language models.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*