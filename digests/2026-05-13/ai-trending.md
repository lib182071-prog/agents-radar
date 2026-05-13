# AI 开源趋势日报 2026-05-13

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-05-13 10:00 UTC

---

# AI 开源趋势日报（2026-05-13）

## 今日速览

今日 GitHub 热搜榜与主题搜索呈现三大看点：**AI Agent 记忆层**成为爆发新热点——`agentmemory` 单日暴增 1048 星，定义持久化记忆标准；**智能体框架与应用**持续井喷，Hermes Agent、CherryStudio、OpenHands 等头部项目持续吸星，同时 `AI-Trader` 等垂直 Agent 应用崭露头角；**LLM 训练与推理**生态稳步扩张，`vllm`、`ollama`、`picollm` 等推理引擎持续迭代，`minimind` 低资源训练教程获得大量关注。此外，**浏览器操控**（browser-use）与 **RAG 引擎**（RAGFlow）仍是社区基建重点，向量数据库赛道竞争激烈。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 171,307 | 本地 LLM 推理引擎，现已支持 Kimi-K2.5、GLM-5、MiniMax 等最新模型，一键运行。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 79,860 | 高吞吐、低显存占用的 LLM 推理服务引擎，成为生产环境首选。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | 7,256 | Rust 生态的 LLM 应用开发框架，模块化设计，适合高性能场景。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 312 | 端侧 LLM 推理库，基于 X-Bit 量化技术，可在设备端运行。 |
| [mattpocock/skills](https://github.com/mattpocock/skills) | 0 (+3867 today) | 从 `.claude` 目录提取的工程师技能集，一键导入 Claude Code 等 Agent 工具。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,274 | 里程碑级通用 Agent 平台，持续引领自主任务执行范式。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 141,206 | 生产级 Agentic Workflow 开发平台，支持可视化编排与多模型接入。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 147,781 | 与用户共同成长的 Agent，支持长期记忆与工具调用，社区活跃。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 73,347 | AI 驱动软件开发助手，能自动完成编码、测试、部署全流程。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 74,673 | 多 Agent 金融交易框架，LLM 组合决策实现量化策略。 |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) | 42,335 | 超轻量个人 AI Agent，适合部署在资源受限环境。 |
| [ruvnet/ruflo](https://github.com/ruvnet/ruflo) | 49,972 | Claude Agent 编排平台，支持多智能体 swarm、RAG 集成与自学习。 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 45,558 | AI 生产力工作室，集成自助Agent、300+ 助手，统一访问前沿 LLM。 |
| [HKUDS/AI-Trader](https://github.com/HKUDS/AI-Trader) | 0 (+229 today) | 100% 全自动 Agent 原生交易系统，今日热榜新星。 |
| [TinyHumansAI/openhuman](https://github.com/tinyhumansai/openhuman) | 0 (+1014 today) | 个人 AI 超级智能，强调隐私、简洁与强大，Rust 实现。 |
| [rohitg00/agentmemory](https://github.com/rohitg00/agentmemory) | 0 (+1048 today) | 基于真实基准的 AI 编码代理持久记忆层，#1 记忆方案。 |
| [yikart/AiToEarn](https://github.com/yikart/AiToEarn) | 0 (+1282 today) | “用 AI 赚钱” 应用，今日热榜增量最高项目之一。 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 67,496 | 金融数据平台，支持 AI Agent 集成分析。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 160,563 | 业界标准模型定义框架，支持文本、视觉、多模态。 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 94,135 (+772 today) | 手把手从零实现 ChatGPT 风格 LLM 的教程，今日仍火爆。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 49,664 | 2 小时从零训练 64M 参数小模型，低资源入门最佳实践。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 225 | 可靠、简洁的预训练库，支持基础模型与世界模型训练。 |
| [RainBowLuoCS/OpenOmni](https://github.com/RainBowLuoCS/OpenOmni) | 139 (NIPS 2025) | 开源全模态大语言模型，支持实时情感语音合成与多模态对齐。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 80,406 | 领先的开源 RAG 引擎，融合 Agent 能力构建 LLM 上下文层。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 55,565 | 通用 AI Agent 记忆层，实现跨会话持久化上下文。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,271 | 高性能云原生向量数据库，广泛用于大规模 RAG 场景。 |
| [lancedb/lancedb](https://github.com/lancedb/lancedb) | 10,287 | 嵌入式向量检索库，开发者友好，支持多模态搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 31,278 | 高可扩展向量搜索引擎，提供云服务（@cloud.qdrant.io）。 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 17,203 | 6 行代码为 AI Agent 添加记忆控制面板，轻量易用。 |
| [yichuan-w/LEANN](https://github.com/yichuan-w/LEANN) | 10,993 | 节省 97% 存储的高效私有 RAG 系统，适合个人设备。 |

---

## 趋势信号分析

1. **Agent 记忆层成为新基建**：`agentmemory` 单日获 1048 星，直接定义“基于真实基准的持久记忆”，与 `mem0`、`cognee`、`claude-mem` 等项目共同推动 **Agent 记忆标准化**。这标志着社区从关注 Agent 能力转向关注 Agent 长期效用，记忆层可能成为未来每个 Agent 的标配。

2. **轻量与高性能并行爆发**：`openhuman`（Rust，1014 星/日）、`picollm`（端侧量化）、`nanobot`（超轻量）等强调资源效率的项目同时登榜，说明开发者既需要本地可运行的 AI，也追求极致的性能（Rig 框架用 Rust 打造 LLM 应用）。**Rust 在 AI 基础设施中的渗透加速**。

3. **金融垂直场景 Agent 崛起**：`AI-Trader`（229 星/日）与 `TradingAgents`（74.6k 星）均聚焦量化交易，结合 LLM 实现多 Agent 协作决策。这与近期大模型在金融领域微调、工具调用能力提升（如 OpenAI 函数调用）密切相关，**Agent 商业化闭环正在金融等数据密集型行业率先落地**。

4. **RAG 生态趋向“零启动”与“私有化”**：`LEANN` 主打 97% 存储节省与完全私有，`lancedb` 强调嵌入式部署，`PageIndex` 提出“无向量”推理 RAG。**RAG 正从依赖外挂向量库转向轻量、离线的全流程方案**，满足企业和个人数据隐私需求。

---

## 社区关注热点

- **`agentmemory`（记忆层王者）**：单日 1048 星，基于真实基准的持久记忆方案，适合所有需要长上下文 Agent 的开发者。  
- **`openhuman`（Rust 个人 AI）**：强调隐私与强大，Rust 实现，代表未来 AI 客户端的性能与安全方向。  
- **`minimind`（2 小时训练 LLM）**：适合个人开发者快速入门模型训练，低资源门槛破圈力强。  
- **`browser-use`（浏览器操控 Agent）**：93k 星，让 AI 直接操作网页，自动化任务场景极其广泛。  
- **`RAGFlow`（RAG 引擎新标杆）**：80k 星且持续增长，结合 Agent 能力，成为企业构建知识问答系统的首选开源方案。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*