# ArXiv AI 研究日报 2026-05-05

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-05-05 07:32 UTC

---

# ArXiv AI 研究日报 — 2026-05-05

## 今日速览

今日投稿呈现出三大趋势：**LLM 推理效率**与**对齐安全**仍是核心议题，**多智能体系统**从理论走向实际基准测试，**医疗 AI** 领域涌现出大量面向特定模态的大模型与新资源。值得关注的工作包括：一种自适应推测解码长度选择机制 SpecKV；通过进化式对话上下文攻击的 ContextualJailbreak；以及首个以学生科研任务为基准的多智能体评测集 AcademiClaw。此外，多篇论文从因果视角挑战可信 AI 的“不变性”假设，提出新的解决方案。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **SpecKV: Adaptive Speculative Decoding with Compression-Aware Gamma Selection**  
   [http://arxiv.org/abs/2605.02888v1](http://arxiv.org/abs/2605.02888v1)  
   作者: Shukla et al.  
   **一句话说明**：提出根据压缩感知动态调整推测长度的自适应解码方法，显著提升 LLM 推理吞吐量。

2. **ContextualJailbreak: Evolutionary Red-Teaming via Simulated Conversational Priming**  
   [http://arxiv.org/abs/2605.02647v1](http://arxiv.org/abs/2605.02647v1)  
   作者: Rodríguez Béjar et al.  
   **一句话说明**：利用进化算法在多轮对话中生成上下文诱导攻击，系统性地绕过 LLM 安全对齐，揭示了当前对齐方法的薄弱环节。

3. **Mitigating Misalignment Contagion by Steering with Implicit Traits**  
   [http://arxiv.org/abs/2605.02751v1](http://arxiv.org/abs/2605.02751v1)  
   作者: Chang et al.  
   **一句话说明**：首次定义多智能体场景中的“对齐传染”问题，并提出通过隐式特质向量引导模型行为的防御方法。

4. **Bolek: A Multimodal Language Model for Molecular Reasoning**  
   [http://arxiv.org/abs/2605.02745v1](http://arxiv.org/abs/2605.02745v1)  
   作者: Grabowski et al.  
   **一句话说明**：构建了融合分子结构图与文本描述的分子推理模型，输出可审计的解释，弥补传统预测器黑箱短板。

5. **Trustworthy AI Suffers from Invariance Conflicts and Causality is The Solution**  
   [http://arxiv.org/abs/2605.02640v1](http://arxiv.org/abs/2605.02640v1)  
   作者: Binkyte et al.  
   **一句话说明**：论证公平性、鲁棒性、隐私等可信目标之间存在不变性冲突，提出以因果理论统一解决。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

6. **AcademiClaw: When Students Set Challenges for AI Agents**  
   [http://arxiv.org/abs/2605.02661v1](http://arxiv.org/abs/2605.02661v1)  
   作者: Yu et al.  
   **一句话说明**：发布包含 80 个真实研究生作业的学术级多智能体基准，填补了现有智能体评测缺少高阶推理任务的空白。

7. **U-Define: Designing User Workflows for Hard and Soft Constraints in LLM-Based Planning**  
   [http://arxiv.org/abs/2605.02765v1](http://arxiv.org/abs/2605.02765v1)  
   作者: Lee et al.  
   **一句话说明**：研究用户如何在 LLM 规划中表达硬约束与软约束，设计交互式工作流以增强端用户对规划结果的控制力。

8. **ORPilot: A Production-Oriented Agentic LLM-for-OR Tool for Optimization Modeling**  
   [http://arxiv.org/abs/2605.02728v1](http://arxiv.org/abs/2605.02728v1)  
   作者: Xie  
   **一句话说明**：开源生产级智能体系统，能将模糊的业务问题自动转化为可求解的优化模型，弥补学术工具与实际需求之间的鸿沟。

9. **Reinforcement Learning for LLM-based Multi-Agent Systems through Orchestration Traces**  
   [http://arxiv.org/abs/2605.02801v1](http://arxiv.org/abs/2605.02801v1)  
   作者: Zhang  
   **一句话说明**：利用编排痕迹对多智能体协作流程进行强化学习优化，不仅优化单个智能体动作，还优化任务分配与通信模式。

### 🔧 方法与框架（新技术、基准测试、效率优化）

10. **Compress Then Adapt? No, Do It Together via Task-aware Union of Subspaces**  
    [http://arxiv.org/abs/2605.02829v1](http://arxiv.org/abs/2605.02829v1)  
    作者: Ge et al.  
    **一句话说明**：挑战先压缩后微调的范式，提出任务感知子空间联合优化方法，在压缩与适应之间取得更好的 Pareto 前沿。

11. **Deciphering Shortcut Learning from an Evolutionary Game Theory Perspective**  
    [http://arxiv.org/abs/2605.02658v1](http://arxiv.org/abs/2605.02658v1)  
    作者: Li et al.  
    **一句话说明**：利用进化博弈论分析深度神经网络训练过程中捷径学习的形成机制，为缓解非本质特征依赖提供理论基础。

12. **AI-Generated Smells: An Analysis of Code and Architecture in LLM and Agent-Driven Development**  
    [http://arxiv.org/abs/2605.02741v1](http://arxiv.org/abs/2605.02741v1)  
    作者: Zhu et al.  
    **一句话说明**：系统性审计 AI 生成代码中的技术债务，揭示 LLM 在追求功能正确性时容易引入架构异味和代码坏味。

13. **FlexSQL: Flexible Exploration and Execution Make Better Text-to-SQL Agents**  
    [http://arxiv.org/abs/2605.02815v1](http://arxiv.org/abs/2605.02815v1)  
    作者: Pham et al.  
    **一句话说明**：提出基于探索-执行循环的 Text-to-SQL 智能体，通过多次数据库交互解决复杂 schema 下的歧义查询。

### 📊 应用（垂直领域、多模态、代码生成）

14. **Foundation Models to Unlock Real-World Evidence from Nationwide Medical Claims**  
    [http://arxiv.org/abs/2605.02740v1](http://arxiv.org/abs/2605.02740v1)  
    作者: Ma et al.  
    **一句话说明**：利用基础模型处理全美医疗理赔数据，提取真实世界证据，支持监管评估与医疗决策。

15. **PubMed-Ophtha: An open resource for training ophthalmology vision-language models on scientific literature**  
    [http://arxiv.org/abs/2605.02720v1](http://arxiv.org/abs/2605.02720v1)  
    作者: Hallitschke et al.  
    **一句话说明**：构建包含 10 万+眼底图像-文本的公开数据集，填补眼科领域大规模多模态训练资源的空白。

16. **Standing on the Shoulders of Giants: Stabilized Knowledge Distillation for Cross-Language Code Clone Detection**  
    [http://arxiv.org/abs/2605.02860v1](http://arxiv.org/abs/2605.02860v1)  
    作者: Khajezade et al.  
    **一句话说明**：提出稳定的知识蒸馏方法，将大型语言模型的跨语言代码克隆检测能力压缩至轻量级模型，实现工业级部署。

17. **When Audio-Language Models Fail to Leverage Multimodal Context for Dysarthric Speech Recognition**  
    [http://arxiv.org/abs/2605.02782v1](http://arxiv.org/abs/2605.02782v1)  
    作者: Moure et al.  
    **一句话说明**：揭示当前音频-语言模型虽能输入临床文本上下文，但在构音障碍语音识别中无法有效利用该信息，指出了多模态融合的瓶颈。

---

## 研究趋势信号

从今日投稿中可以观察到几个新兴方向：**进化红队测试**（ContextualJailbreak）将自动对抗攻击从单轮扩展到多轮上下文诱导，成为对齐研究的新前沿；**因果视角**（Trustworthy AI、Deciphering Shortcut Learning）被用于统一解释与解决 AI 系统中的矛盾目标；**学术级智能体基准**（AcademiClaw）的出现标志着智能体评测从简单工具调用向复杂长程推理迈进；此外，**代码技术债务审计**（AI-Generated Smells）开始关注 AI 生成软件的长期维护性，而非仅功能正确性。

---

## 值得精读

1. **SpecKV** — 首次将推测解码中的投机长度选择从固定超参变为自适应机制，实验显示在保证生成质量的同时可显著减少冗余计算，对 LLM 推理部署有直接实用价值。

2. **ContextualJailbreak** — 提出通过进化算法在多轮对话中自动生成上下文诱导攻击，成功绕过包括 GPT-4 类模型在内的商业系统，为安全对齐研究提供了急需的强对抗基准。

3. **Trustworthy AI Suffers from Invariance Conflicts and Causality is The Solution** — 从理论上指出公平性、鲁棒性、隐私等目标之间的根本矛盾，并论证因果推理是化解冲突的统一框架，对可信 AI 领域具有重要启示。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*