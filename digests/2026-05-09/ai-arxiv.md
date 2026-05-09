# ArXiv AI 研究日报 2026-05-09

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-05-09 07:22 UTC

---

# ArXiv AI 研究日报 (2026-05-09)

## 今日速览

今日投稿围绕**大语言模型架构创新、推理能力强化、智能体自主演进**三条主线展开。MoE 领域出现打破逐层专家隔离的全局共享池设计（UniPool）以及旨在实现模块化的预训练新范式（EMO）；推理训练方面，正向策略优化与递归智能体成为新热点，前者（Beyond Negative Rollouts）利用隐含负梯度提升 RLVR 效果，后者（Recursive Agent Optimization）让智能体能自我递归分解任务；此外，AI 辅助科学研究（AI Co-Mathematician、AI CFD Scientist）和**安全评估**（无基准安全比较、记忆过时检测）也涌现出值得关注的工作。

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

- **[UniPool: A Globally Shared Expert Pool for Mixture-of-Experts](http://arxiv.org/abs/2605.06665v1)**  
  Minbin Huang, Han Shi, Chuanyang Zheng et al.  
  打破传统 MoE 各层独立专家池的约束，引入全局共享专家池，显著减少参数冗余并提升容量效率。

- **[EMO: Pretraining Mixture of Experts for Emergent Modularity](http://arxiv.org/abs/2605.06663v1)**  
  Ryan Wang, Akshita Bhagia, Sewon Min  
  研究发现标准 MoE 预训练后并未自然产生模块化，提出 EMO 训练方法，使模型可按需激活子集并保持性能。

- **[Optimizer-Model Consistency: Full Finetuning with the Same Optimizer as Pretraining Forgets Less](http://arxiv.org/abs/2605.06654v1)**  
  Yuxing Liu, Jianyu Wang, Tong Zhang  
  实证表明：全量微调时使用与预训练相同的优化器能大幅降低灾难性遗忘，简单实用的训练建议。

- **[The Structural Origin of Attention Sink: Variance Discrepancy, Super Neurons, and Dimension Disparity](http://arxiv.org/abs/2605.06611v1)**  
  Siquan Li, Kaiqi Jiang, Jiacheng Sun et al.  
  从方差差异、超级神经元和维度不均衡的角度给出 attention sink 的机制解释，为架构改进提供理论基础。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

- **[AI Co-Mathematician: Accelerating Mathematicians with Agentic AI](http://arxiv.org/abs/2605.06651v1)**  
  Daniel Zheng, Ingrid von Glehn, Yori Zwols et al.  
  为数学家打造交互式 AI 工作台，支持构思、文献检索、定理探索等全流程，代表 AI for Science 的前沿方向。

- **[Recursive Agent Optimization](http://arxiv.org/abs/2605.06639v1)**  
  Apurva Gandhi, Satyaki Chakraborty, Xiangjun Wang et al.  
  提出递归智能体：智能体可自我生成子任务并递归调用新实例，实现推断时间计算扩展，在复杂规划任务上表现出色。

- **[Beyond Negative Rollouts: Positive-Only Policy Optimization with Implicit Negative Gradients](http://arxiv.org/abs/2605.06650v1)**  
  Mingwei Xu, Hao Fang  
  针对可验证奖励的 RL 训练，提出仅使用正样本来更新策略，通过隐含负梯度避免奖励饱和，提升推理模型训练稳定性。

- **[STALE: Can LLM Agents Know When Their Memories Are No Longer Valid?](http://arxiv.org/abs/2605.06527v1)**  
  Hanxiang Chao, Yihan Bai, Rui Sheng et al.  
  构建基准评估 LLM agent 的“记忆过时”检测能力，发现现有 agent 在长程记忆更新上严重不足，是持续学习的关键挑战。

### 🔧 方法与框架（新技术、基准测试、效率优化）

- **[Verifier-Backed Hard Problem Generation for Mathematical Reasoning](http://arxiv.org/abs/2605.06660v1)**  
  Yuhang Lai, Jiazhan Feng, Yee Whye Teh et al.  
  利用验证器自动生成困难的高质量数学问题，用于增强 LLM 推理训练，有望解决训练数据稀缺问题。

- **[Are We Making Progress in Multimodal Domain Generalization? A Comprehensive Benchmark Study](http://arxiv.org/abs/2605.06643v1)**  
  Hao Dong, Hongzhao Li, Shupan Li et al.  
  对多模态领域泛化领域进行系统性基准研究，指出许多报告的性能提升可能是评估不一致导致的伪像，呼吁标准化评测。

- **[Efficient Pre-Training with Token Superposition](http://arxiv.org/abs/2605.06546v1)**  
  Bowen Peng, Théo Gigant, Jeffrey Quesnelle  
  提出 Token 叠加训练方法（TST），作为简单即插即用模块，可显著提升预训练吞吐量且不影响下游性能。

- **[PACZero: PAC-Private Fine-Tuning of Language Models via Sign Quantization](http://arxiv.org/abs/2605.06505v1)**  
  Murat Bilgehan Ertan, Xiaochen Zhu, Phuong Ha Nguyen et al.  
  提出 PAC（可能近似正确）隐私微调机制，通过符号量化实现零阶梯度估算，在隐私保证下提供实用效用。

### 📊 应用（垂直领域、多模态、代码生成）

- **[ActCam: Zero-Shot Joint Camera and 3D Motion Control for Video Generation](http://arxiv.org/abs/2605.06667v1)**  
  Omar El Khalifi, Thomas Rossi, Oscar Fossey et al.  
  零样本方法同时控制视频生成中的角色运动和相机轨迹，为影视创作提供细粒度控制能力。

- **[Patch2Vuln: Agentic Reconstruction of Vulnerabilities from Linux Distribution Binary Patches](http://arxiv.org/abs/2605.06601v1)**  
  Isaac David, Arthur Gervais  
  利用语言模型 agent 从二进制补丁中重建漏洞代码，提升安全分析自动化水平，实用价值高。

- **[NeuroAgent: LLM Agents for Multimodal Neuroimaging Analysis and Research](http://arxiv.org/abs/2605.06584v1)**  
  Lujia Zhong, Yihao Xia, Jianwei Zhang et al.  
  开发专用于多模态神经影像分析的全流程 agent，涵盖预处理、统计分析、疾病分类，降低神经科学研究门槛。

## 研究趋势信号

从今日投稿中可以观察到几个新兴方向：一是 **MoE 架构的模块化探索**，不再满足于稀疏激活效率，而是追求真正的功能解耦；二是 **智能体的递归与自我进化**（RAO、SkillOS）成为 agent 研究的新前沿，强调通过自我递归和技能积累实现持续学习；三是 **数学与科学场景的 AI Agent 闭环**（AI Co-Mathematician、AI CFD Scientist、Verifier-Backed Problem Generation）表明 AI 正从“生成答案”迈向“自主科研”；四是 **安全评估的细粒度化**（无基准比较、记忆过时检测、创意多样性崩溃）反映社区对部署风险的关注已从单一指标转向多维度鲁棒性。

## 值得精读

1. **UniPool (2605.06665)**  
   打破 MoE 逐层专家隔离的固有假设，设计全局共享池，可能改变未来大规模 MoE 模型的参数分配范式，理论分析与实验扎实。

2. **AI Co-Mathematician (2605.06651)**  
   完整呈现 AI agent 如何从工具变成科学家的“合作者”，其开放研究循环的设计思路对 AI for Science 领域具有标杆意义。

3. **The Structural Origin of Attention Sink (2605.06611)**  
   对 attention sink 现象给出了首个系统的机制解释，有助于指导新的注意力机制设计和长上下文模型改进，理论价值高。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*