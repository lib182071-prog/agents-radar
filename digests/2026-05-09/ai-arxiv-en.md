# ArXiv AI Research Digest 2026-05-09

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-05-09 07:22 UTC

---

# ArXiv AI Research Digest
**Date:** 2026-05-09 | **Coverage:** 50 papers (cs.AI, cs.CL, cs.LG)

---

## Today's Highlights

This week's submissions reveal a strong shift toward **recursive and self-evolving agent architectures**, with multiple papers proposing systems that can spawn sub-agents, curate skills from experience, and engage in open-ended scientific discovery. **Mixture-of-Experts (MoE) research matures** beyond per-layer allocations—two papers introduce globally shared expert pools and emergent modularity through pretraining, potentially decoupling model scale from parameter count. A third major theme is the **deepening theoretical understanding of training dynamics**, with investigations into optimizer-model consistency, the structural origins of attention sinks, and the low-rank dynamics of RL with verifiable rewards. The convergence of these directions suggests the field is moving beyond scaling laws toward more principled, efficient, and autonomous systems.

---

## Key Papers

### 🧠 Large Language Models (architecture, training, alignment, evaluation)

1. **UniPool: A Globally Shared Expert Pool for Mixture-of-Experts**
   [http://arxiv.org/abs/2605.06665v1](http://arxiv.org/abs/2605.06665v1)
   *Minbin Huang, Han Shi, Chuanyang Zheng et al.*
   Challenges the rigid per-layer expert allocation in MoE by proposing a globally shared expert pool, promising to decouple depth scaling from linear expert-parameter growth.

2. **EMO: Pretraining Mixture of Experts for Emergent Modularity**
   [http://arxiv.org/abs/2605.06663v1](http://arxiv.org/abs/2605.06663v1)
   *Ryan Wang, Akshita Bhagia, Sewon Min*
   Demonstrates that MoE pretraining can induce emergent modular specialization, enabling applications to use only narrow subsets of model capabilities without full-model deployment.

3. **Optimizer-Model Consistency: Full Finetuning with the Same Optimizer as Pretraining Forgets Less**
   [http://arxiv.org/abs/2605.06654v1](http://arxiv.org/abs/2605.06654v1)
   *Yuxing Liu, Jianyu Wang, Tong Zhang*
   A simple but impactful observation: matching the finetuning optimizer to the pretraining optimizer significantly reduces catastrophic forgetting—a practical insight for LLM adaptation.

4. **The Structural Origin of Attention Sink: Variance Discrepancy, Super Neurons, and Dimension Disparity**
   [http://arxiv.org/abs/2605.06611v1](http://arxiv.org/abs/2605.06611v1)
   *Siquan Li, Kaiqi Jiang, Jiacheng Sun et al.*
   Provides a mechanistic explanation for attention sinks in LLMs, tracing the phenomenon to variance discrepancy and dimension disparity—foundational understanding for architectural improvements.

5. **PACZero: PAC-Private Fine-Tuning of Language Models via Sign Quantization**
   [http://arxiv.org/abs/2605.06505v1](http://arxiv.org/abs/2605.06505v1)
   *Murat Bilgehan Ertan, Xiaochen Zhu, Phuong Ha Nguyen et al.*
   Introduces a PAC-privacy framework that achieves membership-inference resistance without sacrificing utility, offering a practical alternative to differential privacy for fine-tuning.

---

### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

6. **Recursive Agent Optimization**
   [http://arxiv.org/abs/2605.06639v1](http://arxiv.org/abs/2605.06639v1)
   *Apurva Gandhi, Satyaki Chakraborty, Xiangjun Wang et al.*
   Proposes agents that recursively spawn and delegate sub-tasks, implementing an inference-time scaling algorithm that dramatically expands the effective computation available for complex problems.

7. **AI Co-Mathematician: Accelerating Mathematicians with Agentic AI**
   [http://arxiv.org/abs/2605.06651v1](http://arxiv.org/abs/2605.06651v1)
   *Daniel Zheng, Ingrid von Glehn, Yori Zwols et al.*
   A workbench for mathematicians to interactively leverage AI agents across the entire research workflow—ideation, literature review, and proof exploration—representing a concrete step toward AI-assisted scientific discovery.

8. **SkillOS: Learning Skill Curation for Self-Evolving Agents**
   [http://arxiv.org/abs/2605.06614v1](http://arxiv.org/abs/2605.06614v1)
   *Siru Ouyang, Jun Yan, Yanfei Chen et al.*
   Addresses the critical bottleneck of skill quality in self-evolving agents by learning to curate reusable skills from past experiences, enabling agents to improve autonomously over time.

9. **Verifier-Backed Hard Problem Generation for Mathematical Reasoning**
   [http://arxiv.org/abs/2605.06660v1](http://arxiv.org/abs/2605.06660v1)
   *Yuhang Lai, Jiazhan Feng, Yee Whye Teh et al.*
   Tackles the underexplored challenge of generating novel, challenging math problems via verifier-backed generation—essential for advancing LLM training and autonomous research.

10. **STALE: Can LLM Agents Know When Their Memories Are No Longer Valid?**
    [http://arxiv.org/abs/2605.06527v1](http://arxiv.org/abs/2605.06527v1)
    *Hanxiang Chao, Yihan Bai, Rui Sheng et al.*
    Identifies a critical failure mode: LLM agents cannot reliably detect when their stored beliefs become outdated, and introduces a benchmark for this underexplored capability.

---

### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

11. **Efficient Pre-Training with Token Superposition**
    [http://arxiv.org/abs/2605.06546v1](http://arxiv.org/abs/2605.06546v1)
    *Bowen Peng, Théo Gigant, Jeffrey Quesnelle*
    A simple drop-in method that significantly improves pre-training throughput by treating multiple tokens as superimposed representations, offering potential cost savings at scale.

12. **Long Context Pre-Training with Lighthouse Attention**
    [http://arxiv.org/abs/2605.06554v1](http://arxiv.org/abs/2605.06554v1)
    *Bowen Peng, Subho Ghosh, Jeffrey Quesnelle*
    A training-only hierarchical attention algorithm that wraps around standard attention to enable extreme sequence length training without quadratic time/memory costs.

13. **DINORANKCLIP: DINOv3 Distillation and Injection for Vision-Language Pretraining with High-Order Ranking Consistency**
    [http://arxiv.org/abs/2605.06592v1](http://arxiv.org/abs/2605.06592v1)
    *Shuyang Jiang, Nan Yu, Yiming Zhang et al.*
    Addresses two structural weaknesses of CLIP—discarding relative ordering and global pooling bottlenecks—by distilling DINOv3 features and enforcing ranking consistency.

14. **Are We Making Progress in Multimodal Domain Generalization? A Comprehensive Benchmark Study**
    [http://arxiv.org/abs/2605.06643v1](http://arxiv.org/abs/2605.06643v1)
    *Hao Dong, Hongzhao Li, Shupan Li et al.*
    A sobering benchmark study questioning whether reported gains in multimodal domain generalization reflect genuine progress or are artifacts of inconsistent evaluation protocols.

---

### 📊 Applications (domain-specific, multimodal, code generation)

15. **ActCam: Zero-Shot Joint Camera and 3D Motion Control for Video Generation**
    [http://arxiv.org/abs/2605.06667v1](http://arxiv.org/abs/2605.06667v1)
    *Omar El Khalifi, Thomas Rossi, Oscar Fossey et al.*
    Achieves zero-shot control over both character motion and camera trajectory in video generation, addressing a key requirement for artistic and cinematographic applications.

16. **NeuroAgent: LLM Agents for Multimodal Neuroimaging Analysis and Research**
    [http://arxiv.org/abs/2605.06584v1](http://arxiv.org/abs/2605.06584v1)
    *Lujia Zhong, Yihao Xia, Jianwei Zhang et al.*
    An agentic framework that coordinates complex, multi-step neuroimaging preprocessing workflows across heterogeneous toolchains, demonstrating AI's potential in scientific infrastructure.

17. **GlazyBench: A Benchmark for Ceramic Glaze Property Prediction and Image Generation**
    [http://arxiv.org/abs/2605.06641v1](http://arxiv.org/abs/2605.06641v1)
    *Ziyu Zhai, Siyou Li, Juexi Shao et al.*
    A novel domain-specific benchmark at the intersection of materials science and generative AI, providing a dataset and evaluation framework for ceramic glaze prediction and generation.

---

## Research Trend Signal

**Three converging trajectories define this week's submission set.** First, **MoE architectures are undergoing a fundamental redesign**: both UniPool and EMO move beyond the static per-layer expert paradigm toward globally shared pools and emergent modularity, suggesting a path to models that are simultaneously larger in capacity and more parameter-efficient. Second, **agentic systems are becoming recursively self-improving**: Recursive Agent Optimization, SkillOS, and the AI Co-Mathematician all propose agents that not only act but also learn to delegate, curate, and improve their own capabilities—a shift from reactive tools to autonomous research collaborators. Third, **the field is rediscovering the importance of training dynamics**: papers on optimizer-model consistency, the structural origins of attention sinks, and the low-rank dynamics of RLVR all point to a maturing understanding that how we train matters as much as what we train. A cautionary signal emerges from the multimodal domain generalization benchmark study, which suggests that evaluation inconsistency may be inflating reported progress. The presence of domain-specific benchmarks (GlazyBench, SpatialEpiBench) and safety-focused evaluations (benchmarkless safety scoring, market-alignment risk) indicates the community is broadening its notion of what constitutes meaningful validation.

---

## Worth Deep Reading

1. **Recursive Agent Optimization** ([2605.06639](http://arxiv.org/abs/2605.06639v1))
   *Reasoning:* This paper proposes a fundamentally new paradigm for agent scaling—recursive self-delegation. If the approach generalizes, it could unlock inference-time compute scaling without requiring larger models, making it one of the most consequential ideas in this batch.

2. **UniPool: A Globally Shared Expert Pool for Mixture-of-Experts** ([2605.06665](http://arxiv.org/abs/2605.06665v1))
   *Reasoning:* Challenges a decade-old assumption about MoE architecture. A successful globally shared expert pool could dramatically reduce the parameter overhead of deep MoE models while maintaining or improving capacity—a high-impact architectural innovation.

3. **Optimizer-Model Consistency: Full Finetuning with the Same Optimizer as Pretraining Forgets Less** ([2605.06654](http://arxiv.org/abs/2605.06654v1))
   *Reasoning:* A rare example of a simple, actionable finding with immediate practical implications. If validated across architectures, this insight could change finetuning practices across the industry at near-zero cost.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*