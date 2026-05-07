# ArXiv AI Research Digest 2026-05-07

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-05-07 09:44 UTC

---

# ArXiv AI Research Digest
**Date:** 2026-05-07

---

## Today's Highlights

A major cluster of papers today tackles the fundamental challenge of **hallucination detection in LLMs**, with at least four distinct approaches—from single-token confidence signals to dynamical system modeling and internal attention divergence—suggesting the field is converging on lightweight, single-pass methods that bypass costly sampling. Theoretical contributions stand out as well: an **impossibility theorem for long-context models** proves that efficiency, compactness, and recall cannot be simultaneously achieved, while another work systematically demonstrates a **predictive-causal gap** across thousands of neural network configurations, revealing that optimal encoders often track the environment rather than the system they intend to model. On the methods side, a new framework for **Wasserstein gradient flow analysis of drifting models** and a **proximal projection method for doubly sparse regularization** represent significant theoretical advances with practical implications for generative modeling and high-dimensional inference.

---

## Key Papers

### 🧠 Large Language Models

**The Impossibility Triangle of Long-Context Modeling**
Link: http://arxiv.org/abs/2605.05066v1
Authors: Yan Zhou
A fundamental proof that no model can simultaneously achieve per-step computation independent of sequence length, state size independent of sequence length, and the ability to recall arbitrary historical tokens—a crucial theoretical constraint for architecture designers.

**The Predictive-Causal Gap: An Impossibility Theorem and Large-Scale Neural Evidence**
Link: http://arxiv.org/abs/2605.05029v1
Authors: Kejun Liu
Across 2,695 configurations, this paper shows that predictive encoders systematically track environment dynamics rather than underlying system states, establishing a formal limitation on learning causal representations from prediction alone.

**The First Token Knows: Single-Decode Confidence for Hallucination Detection**
Link: http://arxiv.org/abs/2605.05166v1
Authors: Mina Gabriel
Proposes a lightweight method for hallucination detection using only the first decoded token's confidence signal, eliminating the need for repeated sampling while achieving competitive performance.

**Detecting Hallucinations in Large Language Models via Internal Attention Divergence Signals**
Link: http://arxiv.org/abs/2605.05025v1
Authors: Gijs van Dijk
A single-pass uncertainty quantification method that measures KL divergence between attention distributions across layers to detect hallucinations without external models or multiple samples.

**Low-Cost Black-Box Detection of LLM Hallucinations via Dynamical System Prediction**
Link: http://arxiv.org/abs/2605.05134v1
Authors: Dan Wilson, Mohamed Akrout
Treats LLM text generation as a dynamical system and detects hallucinations by predicting trajectory divergence, offering a computationally efficient alternative to consistency-based methods.

**Misaligned by Reward: Socially Undesirable Preferences in LLMs**
Link: http://arxiv.org/abs/2605.05003v1
Authors: Gayane Ghazaryan, Esra Dönmez
Demonstrates that current reward models used for LLM alignment can capture socially undesirable preferences, revealing a critical blind spot in existing evaluation benchmarks.

**On the Hardness of Junking LLMs**
Link: http://arxiv.org/abs/2605.05116v1
Authors: Marco Rando, Samuel Vaiter
Systematically analyzes the difficulty of jailbreaking LLMs, showing that attacks requiring explicit semantic structure face fundamental limitations compared to optimization-based approaches.

**The Pinocchio Dimension: Phenomenality of Experience as the Primary Axis of LLM Psychometric Differences**
Link: http://arxiv.org/abs/2605.05080v1
Authors: Hubert Plisiecki, Sabina Siudaj, Kacper Dudzic et al.
Administers 45 psychometric questionnaires to 50 LLMs and finds that the primary axis of between-model variance separates items describing phenomenal experience from factual knowledge.

---

### 🤖 Agents & Reasoning

**Adaptive Policy Selection and Fine-Tuning under Interaction Budgets for Offline-to-Online Reinforcement Learning**
Link: http://arxiv.org/abs/2605.05123v1
Authors: Alper Kamil Bozkurt, Xiaoan Xu, Shangtong Zhang et al.
Introduces a framework for selecting and fine-tuning policies under limited online interaction budgets, addressing a critical bottleneck in deploying offline-trained policies to real environments.

**Rollout Pass-Rate Control: Steering Binary-Reward RL Toward Its Most Informative Regime**
Link: http://arxiv.org/abs/2605.05112v1
Authors: Tianshu Zhu, Wenyu Zhang, Xiaoying Zuo et al.
Frames the inefficiency of binary-reward agentic RL as a pass-rate control problem, showing that adaptive rollout difficulty selection can substantially improve learning signal quality.

**Provable imitation learning for control of instability in partially-observed Vlasov–Poisson equations**
Link: http://arxiv.org/abs/2605.05081v1
Authors: Xiaofan Xia, Qin Li, Wenlong Mou
Offers provable guarantees for imitation learning in plasma stabilization, bridging the gap between ideal full-state controllers and practical partially-observed feedback—relevant to nuclear fusion.

---

### 🔧 Methods & Frameworks

**Understanding In-Context Learning for Nonlinear Regression with Transformers: Attention as Featurizer**
Link: http://arxiv.org/abs/2605.05176v1
Authors: Alexander Hsu, Zhaiming Shen, Wenjing Liao et al.
Provides a theoretical framework showing that in-context learning in transformers for nonlinear regression works by using attention to construct task-specific feature maps.

**Manifold Steering Reveals the Shared Geometry of Neural Network Representation and Behavior**
Link: http://arxiv.org/abs/2605.05115v1
Authors: Daniel Wurgaft, Can Rager, Matthew Kowal et al.
Intervenes along geometric paths in activation space to causally link neural representation geometry to behavioral outputs, offering a principled method for mechanistic interpretability.

**Continuous Knowledge Updating in LLM Systems: Learning Through Multi-Timescale Memory Dynamics**
Link: http://arxiv.org/abs/2605.05097v1
Authors: Andreas Pattichis, Constantine Dovrolis
Proposes biologically-inspired multi-timescale memory dynamics that allow LLM systems to continuously update knowledge without full retraining, addressing a critical deployment challenge.

**Preference-Based Self-Distillation: Beyond KL Matching via Reward Regularization**
Link: http://arxiv.org/abs/2605.05040v1
Authors: Xin Yu, Liuchen Liao, Yiwen Zhang et al.
Introduces a self-distillation framework that uses preference-based reward regularization rather than simple KL matching, enabling effective on-policy self-improvement without external teachers.

**Piper: Efficient Large-Scale MoE Training via Resource Modeling and Pipelined Hybrid Parallelism**
Link: http://arxiv.org/abs/2605.05049v1
Authors: Sajal Dash, Feiyang Wang
Presents a system for efficient Mixture-of-Experts training on HPC platforms that models resource constraints and uses pipelined hybrid parallelism to handle heterogeneous networks.

---

### 📊 Applications

**Gated Multimodal Learning for Interpretable Property Energy Performance Prediction and Retrofit Scenario Analysis**
Link: http://arxiv.org/abs/2605.05088v1
Authors: Yunfei Bai, Aaron Tesfa Tsion, Raul Rosales et al.
Develops an interpretable multimodal framework for building energy performance prediction that integrates different data types while providing actionable retrofit scenario analysis.

**Joint Treatment Effect Estimation from Incomplete Healthcare Data: Temporal Causal Normalizing Flows with LLM-driven Evolutionary MNAR Imputation**
Link: http://arxiv.org/abs/2605.05125v1
Authors: Olivia Jullian Parra, Sara Zoccheddu, David Catalan Cerezo et al.
Unifies causal estimation, missing data imputation, and temporal modeling in a single framework for healthcare, using LLMs to guide imputation of not-missing-at-random data.

**Beyond Semantics: An Evidential Reasoning-Aware Multi-View Learning Framework for Trustworthy Mental Health Prediction**
Link: http://arxiv.org/abs/2605.05121v1
Authors: Yucheng Ruan, Ling Huang, Qika Lin et al.
Introduces evidential reasoning to mental health text classification, producing uncertainty-aware predictions rather than overconfident outputs—critical for high-stakes clinical deployment.

**When Relations Break: Analyzing Relation Hallucination in Vision-Language Model Under Rotation and Noise**
Link: http://arxiv.org/abs/2605.05045v1
Authors: Philip Wootaek Shin, Ajay Narayanan Sridhar, Sivani Devarapalli et al.
Shows that even mild visual perturbations significantly increase relation hallucination rates in VLMs, identifying a systematic failure mode for inter-object reasoning.

**Direct Product Flow Matching: Decoupling Radial and Angular Dynamics for Few-Shot Adaptation**
Link: http://arxiv.org/abs/2605.05054v1
Authors: Hongxu Chen, Yanghao Wang, Bowei Zhu et al.
Proposes a flow matching approach that decouples radial and angular dynamics in cross-modal feature space, improving few-shot adaptation of vision-language models.

---

## Research Trend Signal

Two interconnected research directions dominate today's submissions and signal where the field is heading. **First, hallucination detection is undergoing a paradigm shift**: rather than expensive sampling-based methods, researchers are converging on lightweight, single-pass approaches that leverage internal model dynamics—whether from attention divergence, first-token confidence, or trajectory prediction in latent space. This suggests that production deployment of LLMs will soon incorporate real-time hallucination monitoring as a standard component. **Second, a maturing theoretical understanding of fundamental limitations** is emerging: impossibility theorems for long-context modeling and causal representation learning are no longer curiosities but are being backed by large-scale empirical evidence. The combination of these two trends—practical detection systems grounded in rigorous theory—points toward more reliable, auditable language models. Additionally, the application of psychometric methods to LLMs (50 models, 45 questionnaires) represents a novel approach to understanding model behavior that could complement existing evaluation frameworks. The increasing attention to **multiple-timescale memory systems** for continual learning and **preference-based self-distillation** suggests that the community is actively moving beyond static training paradigms toward adaptive, self-improving systems.

---

## Worth Deep Reading

1. **"The Impossibility Triangle of Long-Context Modeling"** (http://arxiv.org/abs/2605.05066v1)
   This is the most consequential theoretical result in today's batch. The proof that efficiency, compactness, and recall cannot be simultaneously achieved provides a fundamental constraint that should guide all future long-context architecture design. Practitioners and researchers evaluating new attention variants or state-space models should read this to understand the trade-offs inherent in any approach.

2. **"The Predictive-Causal Gap: An Impossibility Theorem and Large-Scale Neural Evidence"** (http://arxiv.org/abs/2605.05029v1)
   With experiments across 2,695 configurations, this paper delivers a systematic and sobering result: predictive encoders naturally track the environment, not the system they should model. This has profound implications for self-supervised learning, world models, and any approach that relies on prediction as a proxy for causal understanding.

3. **"Manifold Steering Reveals the Shared Geometry of Neural Network Representation and Behavior"** (http://arxiv.org/abs/2605.05115v1)
   This paper introduces a principled method for causal intervention in neural activation space, directly testing whether geometric structure in representations shapes behavior. It moves beyond correlational analysis of neural representations to establish causal links, which is exactly what the interpretability community needs.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*