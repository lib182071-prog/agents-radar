# ArXiv AI Research Digest 2026-05-05

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-05-05 07:32 UTC

---

Here is the structured ArXiv AI Research Digest for 2026-05-05.

---

### 1. Today's Highlights

Today's submissions reveal a strong focus on making large language models (LLMs) more efficient and reliable through advanced inference-time techniques like speculative decoding and structured planning, moving beyond simple scaling laws. A significant cluster of papers tackles the emerging challenges of **multi-agent** and **agentic AI**, specifically addressing safety, security, and coordination in agentic workflows, including zero-trust architectures and detection of misalignment "contagion." The intersection of AI with high-stakes domains—healthcare, drug discovery, and robotics—is dominated by work on **explainability, data efficiency, and domain-specific grounding**, such as causal models for drug safety and multimodal models for molecular reasoning. Finally, a notable signal is the use of **evolutionary game theory** and **causal inference** to theoretically underpin and solve persistent problems like shortcut learning and invariance conflicts in trustworthy AI.

### 2. Key Papers

#### 🧠 Large Language Models (architecture, training, alignment, evaluation)

- **SpecKV: Adaptive Speculative Decoding with Compression-Aware Gamma Selection** ([Link](http://arxiv.org/abs/2605.02888v1))
  Shikhar Shukla et al.
  Proposes a compression-aware method to dynamically select the speculation length (gamma) in speculative decoding, a critical hyperparameter that directly impacts the efficiency of LLM inference.
- **Mitigating Misalignment Contagion by Steering with Implicit Traits** ([Link](http://arxiv.org/abs/2605.02751v1))
  Maria Chang et al.
  Addresses the underexplored risk of "misalignment contagion" in multi-agent settings, where a compromised model can influence others, and proposes steering using implicit traits to maintain value alignment.
- **ContextualJailbreak: Evolutionary Red-Teaming via Simulated Conversational Priming** ([Link](http://arxiv.org/abs/2605.02647v1))
  Mario Rodríguez Béjar et al.
  Demonstrates a powerful new attack vector: multi-turn jailbreaks that use conversational priming to covertly bias later replies, and introduces an evolutionary red-teaming framework to generate them.

#### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

- **Reinforcement Learning for LLM-based Multi-Agent Systems through Orchestration Traces** ([Link](http://arxiv.org/abs/2605.02801v1))
  Chenchen Zhang
  Extends RL to optimize not just individual agent actions but the entire orchestration of work (delegation, communication, aggregation) in LLM-based multi-agent teams, a critical step for scaling agentic systems.
- **U-Define: Designing User Workflows for Hard and Soft Constraints in LLM-Based Planning** ([Link](http://arxiv.org/abs/2605.02765v1))
  Christine P Lee et al.
  Studies how end-users can effectively represent both rigid (hard) and flexible (soft) constraints in LLM-based task planners, a key usability challenge for real-world planning tools.
- **Hybrid Inspection and Task-Based Access Control in Zero-Trust Agentic AI** ([Link](http://arxiv.org/abs/2605.02682v1))
  Majed El Helou et al.
  Proposes a zero-trust security framework for LLM-driven agents that combines task-based access control with real-time inspection, directly addressing security risks in dynamic, multi-turn agent tool use.
- **The Design and Composition of Structural Causal Decision Processes** ([Link](http://arxiv.org/abs/2605.02681v1))
  Sebastian Benthall et al.
  Introduces new causal models of decision-making agents (Structural Causal Decision Processes) that can model endogenous cognitive limits and value discounting, relevant for composing subsystems in computational economics.
- **ORPilot: A Production-Oriented Agentic LLM-for-OR Tool for Optimization Modeling** ([Link](http://arxiv.org/abs/2605.02728v1))
  Guangrui Xie
  Translates real-world, messy business problems into solver-ready optimization models by handling ambiguous specifications and embedded data, bridging a key gap between academic LLM-for-OR tools and production use.

#### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

- **Deciphering Shortcut Learning from an Evolutionary Game Theory Perspective** ([Link](http://arxiv.org/abs/2605.02658v1))
  Xiayang Li et al.
  Provides a formal definition and theoretical understanding of shortcut learning using evolutionary game theory, showing how models converge on non-essential features, which is foundational for building more robust models.
- **A decoupled diffusion planner that adapts to changing cost limits by using cost-conditioned generation for safety and reward gradients for performance** ([Link](http://arxiv.org/abs/2605.02777v1))
  Rufeng Chen et al.
  Proposes a new offline safe RL planner that uses a decoupled diffusion process to handle dynamically changing safety budgets, a significant advance for flexible safe deployment in robotics.
- **FlexSQL: Flexible Exploration and Execution Make Better Text-to-SQL Agents** ([Link](http://arxiv.org/abs/2605.02815v1))
  Quang Hieu Pham et al.
  Moves beyond fixed pipeline Text-to-SQL agents by enabling agents to dynamically explore the database schema and data during execution, improving performance on complex, analytical queries.
- **SCPRM: A Schema-aware Cumulative Process Reward Model for Knowledge Graph Question Answering** ([Link](http://arxiv.org/abs/2605.02819v1))
  Jiujiu Chen et al.
  Addresses the "risk compensation effect" in process reward models for KGQA by introducing a cumulative, schema-aware model that provides more faithful step-wise supervision for LLM reasoning.

#### 📊 Applications (domain-specific, multimodal, code generation)

- **An explainable hypothesis-driven approach to Drug-Induced Liver Injury with HADES** ([Link](http://arxiv.org/abs/2605.02669v1))
  Maciej Wisniewski et al.
  Moves beyond binary classification for drug safety to a hypothesis-driven framework that provides mechanistic insight, a paradigm shift for translational bioinformatics and reducing clinical trial attrition.
- **Bolek: A Multimodal Language Model for Molecular Reasoning** ([Link](http://arxiv.org/abs/2605.02745v1))
  Frederic Grabowski et al.
  Introduces a multimodal model that fuses molecular structure input with textual reasoning to provide auditable explanations for property predictions, crucial for trustworthy AI in drug discovery.
- **Learning Equivariant Neural-Augmented Object Dynamics From Few Interactions** ([Link](http://arxiv.org/abs/2605.02699v1))
  Sergio Orozco et al.
  Combines equivariant neural networks with graph-based particle dynamics to model object motion (including deformable objects) from very few physical interactions, addressing a critical data-efficiency problem in robotic manipulation.
- **AcademiClaw: When Students Set Challenges for AI Agents** ([Link](http://arxiv.org/abs/2605.02661v1))
  Junjie Yu et al.
  Proposes a novel, bilingual benchmark of 80 complex, long-horizon academic-level tasks sourced from university students, evaluating agent capabilities beyond simple assistant-level tasks.

### 3. Research Trend Signal

A prominent trend visible today is the **convergence of "safety" and "coordination"** in agentic AI. Research is moving from single-model alignment to multi-agent safety (contagion risks in paper 22), zero-trust architectures for agent tool use (paper 41), and adaptive task allocation between humans and AI (paper 7). Simultaneously, the **rise of causal and game-theoretic frameworks** to explain model behavior is notable. Papers are moving beyond descriptive statistics to provide formal theoretical underpinnings for issues like shortcut learning (paper 47 via evolutionary game theory) and to propose structural causal models for decision-making (paper 42). This suggests a maturation of the field, where empirical results are increasingly backed by rigorous theoretical models, particularly for ensuring robustness and trustworthiness in deployment.

### 4. Worth Deep Reading

1.  **Mitigating Misalignment Contagion by Steering with Implicit Traits** ([Link](http://arxiv.org/abs/2605.02751v1))
    This paper tackles a critical and largely unaddressed vulnerability in the rapidly expanding field of multi-agent LLM systems. Understanding how misaligned behavior can spread within a network of models is foundational for designing robust and safe agent swarms, making this a must-read for anyone working on agentic systems.

2.  **Deciphering Shortcut Learning from an Evolutionary Game Theory Perspective** ([Link](http://arxiv.org/abs/2605.02658v1))
    Shortcut learning is a fundamental obstacle to robustness and generalization. Providing a formal, game-theoretic model for this phenomenon offers a powerful new lens for understanding and potentially mitigating it. This paper is likely to be highly influential in moving the field beyond empirical observations towards principled solutions.

3.  **Enhancing RL Generalizability in Robotics through SHAP Analysis of Algorithms and Hyperparameters** ([Link](http://arxiv.org/abs/2605.02867v1))
    While many papers introduce new algorithms, this one provides a systematic and practical method (SHAP analysis) to understand *why* certain RL algorithms and hyperparameters generalize better. This offers actionable insights for practitioners and a rigorous framework for future research on RL generalization, making it highly valuable for the robotics community.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*