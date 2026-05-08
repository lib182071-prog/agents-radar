# ArXiv AI 研究日报 2026-05-08

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-05-08 06:18 UTC

---

# ArXiv AI 研究日报 (2026-05-08)

## 今日速览

今日投稿围绕**MoE架构革新**（全局专家池与模块性预训练）、**智能体自我进化**（递归子任务委派与技能复用）、**推理强化学习的尺度理论**（人工逻辑环境ScaleLogic揭示RL提升推理的边界）以及**科学发现加速**（AI协同数学家、CFD智能体）展开。此外，Transformer注意力沉没的结构起源、优化器一致性对遗忘的影响、以及基于验证器的数学难题自动生成也提供了重要理论突破。整体趋势是：架构层面追求更深层次的模块化与动态路由，训练层面强调优化器匹配与分布鲁棒性，应用层面则向长周期科学研究闭环迈进。

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

- **UniPool: A Globally Shared Expert Pool for Mixture-of-Experts**  
  [http://arxiv.org/abs/2605.06665v1](http://arxiv.org/abs/2605.06665v1)  
  *Minbin Huang et al.*  
  突破传统每层独立专家的限制，提出全局共享专家池，解耦深度增长与参数线性增长，有望大幅降低MoE参数量并提升专家利用率。

- **EMO: Pretraining Mixture of Experts for Emergent Modularity**  
  [http://arxiv.org/abs/2605.06663v1](http://arxiv.org/abs/2605.06663v1)  
  *Ryan Wang et al.*  
  预训练阶段引入特殊正则，使MoE天然分化出面向代码、数学、知识等不同能力的模块，为按需激活子模型提供新思路。

- **Optimizer-Model Consistency: Full Finetuning with the Same Optimizer as Pretraining Forgets Less**  
  [http://arxiv.org/abs/2605.06654v1](http://arxiv.org/abs/2605.06654v1)  
  *Yuxing Liu et al.*  
  发现全量微调时使用与预训练相同的优化器能显著缓解灾难性遗忘，为实际微调策略提供简单有效的指导原则。

- **The Structural Origin of Attention Sink: Variance Discrepancy, Super Neurons, and Dimension Disparity**  
  [http://arxiv.org/abs/2605.06611v1](http://arxiv.org/abs/2605.06611v1)  
  *Siquan Li et al.*  
  从数学上揭示注意力沉没现象源于初始位置与后续位置方差差异及维度不对等，为改进长上下文Transformer提供理论依据。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

- **Recursive Agent Optimization**  
  [http://arxiv.org/abs/2605.06639v1](http://arxiv.org/abs/2605.06639v1)  
  *Apurva Gandhi et al.*  
  训练能递归委派子任务的智能体，实现推理时计算扩展，使单个智能体可通过分治解决远超自身能力范围的复杂问题。

- **Can RL Teach Long-Horizon Reasoning to LLMs? Expressiveness Is Key**  
  [http://arxiv.org/abs/2605.06638v1](http://arxiv.org/abs/2605.06638v1)  
  *Tianle Wang et al.*  
  提出ScaleLogic人工逻辑框架，系统研究任务难度与RL训练尺度的关系，指出表达力不足是RL提升长程推理的关键瓶颈。

- **AI Co-Mathematician: Accelerating Mathematicians with Agentic AI**  
  [http://arxiv.org/abs/2605.06651v1](http://arxiv.org/abs/2605.06651v1)  
  *Daniel Zheng et al.*  
  构建交互式智能工作台，支持数学家进行文献检索、猜想生成、证明尝试等开放式研究，展示AI深度参与数学发现的完整闭环。

- **StraTA: Incentivizing Agentic Reinforcement Learning with Strategic Trajectory Abstraction**  
  [http://arxiv.org/abs/2605.06642v1](http://arxiv.org/abs/2605.06642v1)  
  *Xiangyuan Xue et al.*  
  通过策略性轨迹抽象（将长轨迹压缩为高层策略）增强长期信用分配，显著改善LLM作为交互式智能体的探索效率。

### 🔧 方法与框架（新技术、基准测试、效率优化）

- **Verifier-Backed Hard Problem Generation for Mathematical Reasoning**  
  [http://arxiv.org/abs/2605.06660v1](http://arxiv.org/abs/2605.06660v1)  
  *Yuhang Lai et al.*  
  利用验证器自动生成高质量、难度可控的新数学问题，解决LLM训练中困难问题不足的痛点，推动自主科学推理研究。

- **Transformers Efficiently Perform In-Context Logistic Regression via Normalized Gradient Descent**  
  [http://arxiv.org/abs/2605.06609v1](http://arxiv.org/abs/2605.06609v1)  
  *Chenyang Zhang et al.*  
  理论证明单层Transformer可通过实现归一化梯度下降来执行上下文逻辑回归，为理解ICL的算法本质提供严谨分析。

- **Improved techniques for fine-tuning flow models via adjoint matching: a deterministic control pipeline**  
  [http://arxiv.org/abs/2605.06583v1](http://arxiv.org/abs/2605.06583v1)  
  *Zhengyi Guo et al.*  
  将流式模型偏好对齐视为最优控制问题，提出伴随匹配框架，在速度场上直接回归价值梯度，实现稳定高效的人类偏好微调。

### 📊 应用（垂直领域、多模态、代码生成）

- **Cited but Not Verified: Parsing and Evaluating Source Attribution in LLM Deep Research Agents**  
  [http://arxiv.org/abs/2605.06635v1](http://arxiv.org/abs/2605.06635v1)  
  *Hailey Onweller et al.*  
  系统评估LLM深度研究智能体生成的引用准确性，发现大量“引用但不可验证”的情况，为构建可信的自动化研究报告提供评测基准。

- **AI CFD Scientist: Toward Open-Ended Computational Fluid Dynamics Discovery with Physics-Aware AI Agents**  
  [http://arxiv.org/abs/2605.06607v1](http://arxiv.org/abs/2605.06607v1)  
  *Nithin Somasekharan et al.*  
  将AI智能体闭环扩展至高保真物理仿真领域，通过物理约束与验证器实现CFD仿真全流程的自动化发现，有望加速空气动力学等工程学科的研究。

- **DINORANKCLIP: DINOv3 Distillation and Injection for Vision-Language Pretraining with High-Order Ranking Consistency**  
  [http://arxiv.org/abs/2605.06592v1](http://arxiv.org/abs/2605.06592v1)  
  *Shuyang Jiang et al.*  
  通过蒸馏DINOv3的细粒度视觉特征并注入CLIP，同时引入高阶排序一致性损失，显著提升图文对比学习对细粒度语义的建模能力。

## 研究趋势信号

- **Mixture-of-Experts 架构的范式跃迁**：从“每层独立专家”到“全局共享专家池”（UniPool）以及“模块性预训练”（EMO）使得MoE不再仅是稀疏激活的压缩手段，而是向着真正的功能模块化迈进。
- **递归与自我进化的智能体**：本日多篇工作（RAO、StraTA、SkillOS）聚焦智能体如何通过委派子任务、轨迹抽象、技能复用实现“自我升级”，标志智能体研究开始从“一次性任务求解”转向“持续学习”范式。
- **注意力机制的深层机理揭示**：Attention Sink的结构解释、ICL的梯度下降等价定理等，表明社区正从现象描述转向理论归因，为设计更高效或更可解释的Transformer提供基础。
- **科学发现AI的闭环实践**：AI数学家、AI CFD科学家、自动化材料数据集（GlazyBench）等突出强化了“AI辅助开放研究”的趋势，验证器与物理仿真器的结合成为关键环节。

## 值得精读

1. **Recursive Agent Optimization**（RAO）  
   - 提出递归智能体范型，允许智能体在推理时动态扩展能力，通过子任务委派实现超越自身参数规模的问题求解。这种“推理时计算扩展”思路极具前瞻性，可能成为未来Agent系统的基础架构。

2. **UniPool: A Globally Shared Expert Pool for Mixture-of-Experts**  
   - 打破MoE“一层一专家池”的铁律，证明全局共享池可在保持容量的同时大幅减少参数，并提升负载均衡与专家专业化。对现有大模型稀疏化方法有颠覆性启发。

3. **AI Co-Mathematician**  
   - 首个展示AI智能体在数学家开放式工作流中端到端协同的系统，覆盖从文献检索、猜想生成到证明辅助的全链条。其交互式设计模式对所有科学AI应用都有示范意义。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*