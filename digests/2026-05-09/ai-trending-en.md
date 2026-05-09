# AI Open Source Trends 2026-05-09

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-05-09 07:22 UTC

---

# AI Open Source Trends Report
**Date:** 2026-05-09  
**Source:** GitHub Trending (12 repos) + AI Topic Search (80 repos, deduplicated)

---

## 1. Today's Highlights

The open-source AI ecosystem is seeing explosive growth in **agent infrastructure and tooling**, with multiple projects surpassing 3,000 stars in a single day. **Anthropic’s financial-services** repository and **DeepSeek-TUI (Rust)** led the trending chart, signaling strong developer interest in domain-specific agent skills and terminal-based coding assistants. Meanwhile, the **agent harness** concept continues to mature — projects like `addyosmani/agent-skills` and `awslabs/aidlc-workflows` are standardizing production-grade engineering skills and adaptive workflows for AI coding agents. The **RAG/vector-db** space remains highly active, with `LEANN` and `memvid` pushing memory-layer innovations, while `lobehub` introduces a multi-agent “work unit” paradigm that redefines how teams collaborate with AI teammates.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference, CLI Tools)

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐171,031 — Local LLM runtime now supporting Kimi-K2.5, GLM-5, and more, making on-device inference accessible.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐79,454 — High-throughput LLM serving engine; continues to be the backbone for production deployments.
- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐136,194 — The agent engineering platform (Python + TypeScript) powering hundreds of downstream projects.
- **[trycua/cua](https://github.com/trycua/cua)** ⭐15,764 — Open-source infrastructure for computer-use agents: sandboxes, SDKs, and benchmarks for desktop-control AI.
- **[jackwener/OpenCLI](https://github.com/jackwener/OpenCLI)** ⭐19,402 — Universal CLI Hub for AI agents, enabling any website, Electron app, or binary to become an AI-callable tool.
- **[decolua/9router](https://github.com/decolua/9router)** ⭐0 (+1,052 today) — Free AI coding router connecting Claude Code, Cursor, etc. to 40+ providers with auto-fallback and token savings.

### 🤖 AI Agents / Workflows

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐139,781 — A growing agent framework that adapts to users over time, emphasized by its “grows with you” philosophy.
- **[Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps)** ⭐109,348 — 100+ runnable AI Agent & RAG apps; a practical reference for building and shipping agents.
- **[HKUDS/nanobot](https://github.com/HKUDS/nanobot)** ⭐42,048 — Ultra-lightweight personal AI agent designed for edge devices and minimal resource consumption.
- **[lobehub/lobehub](https://github.com/lobehub/lobehub)** ⭐0 (+125 today) — Multi-agent collaborative harness that treats agent teams as the primary unit of work interaction.
- **[awslabs/aidlc-workflows](https://github.com/awslabs/aidlc-workflows)** ⭐0 (+58 today) — AI-Driven Life Cycle adaptive workflow steering rules for coding agents, bringing enterprise-grade orchestration.
- **[activepieces/activepieces](https://github.com/activepieces/activepieces)** ⭐22,115 — AI Agents & MCP-driven workflow automation, now supporting ~400 MCP servers.

### 📦 AI Applications (Specific Use Cases)

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐45,283 — AI productivity studio with smart chat, autonomous agents, and 300+ pre-built assistants.
- **[HKUDS/AI-Trader](https://github.com/HKUDS/AI-Trader)** ⭐0 (+202 today) — 100% automated agent-native trading system, showing AI’s push into financial markets.
- **[CloakHQ/CloakBrowser](https://github.com/CloakHQ/CloakBrowser)** ⭐0 (+526 today) — Stealth Chromium that passes 30/30 bot detection tests; essential for testing and deploying web agents.
- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐43,662 — AI-powered job search system with 14 skill modes and PDF generation, demonstrating vertical agent applications.
- **[OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB)** ⭐67,249 — Financial data platform designed for analysts and AI agents, bridging quantitative research with agent workflows.

### 🧠 LLMs / Training

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐92,211 — Step-by-step PyTorch implementation of a ChatGPT-like LLM; the go-to educational resource for model building.
- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** ⭐71,069 — Unified fine-tuning framework for 100+ LLMs & VLMs (ACL 2024), accelerating model customization.
- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐49,330 — Train a 64M-parameter LLM from scratch in 2 hours; lowers the barrier for LLM research.
- **[z-lab/dflash](https://github.com/z-lab/dflash)** ⭐0 (+379 today) — Block Diffusion for Flash Speculative Decoding, a novel inference optimization technique gaining traction.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐222 — Minimal and scalable pretraining library for foundation and world models.

### 🔍 RAG / Knowledge

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐140,663 — Production-ready agentic workflow platform with strong RAG integration; a top choice for building retrieval-augmented systems.
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐80,036 — Leading open-source RAG engine that combines retrieval, agents, and a context layer for LLMs.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐55,181 — Universal memory layer for AI agents; complements RAG with long-term contextual memory.
- **[LearningCircuit/local-deep-research](https://github.com/LearningCircuit/local-deep-research)** ⭐0 (+559 today) — Achieves ~95% on SimpleQA with local models (e.g., Qwen3.6-27B on a 3090); supports 10+ search engines and private documents, with full encryption.
- **[yichuan-w/LEANN](https://github.com/yichuan-w/LEANN)** ⭐10,975 (topic:vector-db) — [MLsys2026] RAG on Everything with 97% storage savings while maintaining fast, accurate, and private on-device retrieval.
- **[zilliztech/claude-context](https://github.com/zilliztech/claude-context)** ⭐10,896 — Code search MCP for Claude Code, turning entire codebase into agent context.

---

## 3. Trend Signal Analysis

**Explosive growth of agent harnesses and coding assistants:** The top trending repos today — `DeepSeek-TUI`, `financial-services`, and `agent-skills` — all revolve around giving AI coding agents more structured skills and domain-specific capabilities. The community is moving beyond simple chat completion toward agents that can navigate real development environments, manage multi-step workflows, and integrate with existing toolchains. The fact that `9router` (a multi-provider routing proxy) amassed 1,052 stars signals that developers are looking for cost-efficient, fallback-enabled ways to power these agents across multiple LLM providers.

**New tech stacks: Block Diffusion and speculative decoding** — `z-lab/dflash` introduces block diffusion for flash speculative decoding, a novel inference-time technique that promises faster generation without sacrificing quality. This is part of a broader trend toward optimizing inference latency, especially as agentic systems require many sequential LLM calls.

**Memory and context layers are becoming first-class infrastructure** — Projects like `mem0`, `memvid`, and `local-deep-research` (with its “all local & encrypted” pitch) show that developers want agents to have persistent, secure, and efficient memory. The convergence of RAG, vector databases, and agent memory is creating a new “memory plane” category that bridges retrieval and long-term agent state.

**Connection to recent LLM releases** — The inclusion of Kimi-K2.5, GLM-5, and MiniMax in `ollama`’s supported models reflects the fast-paced model release cycle. The strong interest in `DeepSeek-TUI` (3,731 stars) indicates that DeepSeek’s open-weight models are driving developer adoption in the agent space. Additionally, the surge in `financial-services` (3,660 stars) from Anthropic suggests that domain-specific agent skills — especially in regulated industries like finance — are a new frontier for the ecosystem.

---

## 4. Community Hot Spots

- **🪄 Agent Harnesses & Skills Standardization** — `addyosmani/agent-skills` and `awslabs/aidlc-workflows` are defining what “production-grade” means for AI agents. Developers looking to move from toy demos to reliable, composable agents should watch these repos closely.

- **🧠 Terminal-Native Coding Agents** — `Hmbown/DeepSeek-TUI` (Rust) and `DeepSeek` integration tooling are proving that the terminal remains a powerful interface for AI coding agents, especially for power users who prefer speed and low overhead.

- **🌐 Multi-Provider Routing & Fallback** — `decolua/9router` represents a growing demand for resilient, cost-efficient agent backends. With “unlimited FREE AI coding” as its headline, it taps into the developer pain of API limits and provider outages.

- **🔒 Privacy-First RAG & Local Reasoning** — `LearningCircuit/local-deep-research` and `LEANN` highlight a strong shift toward on-device, encrypted retrieval that rivals cloud-based performance. This is crucial for enterprise and sensitive-data use cases.

- **🏗️ Computer-Use Agents Infrastructure** — `trycua/cua` (15,764 stars) and `CloakBrowser` signal that the community is building the foundational layers (sandboxes, benchmarks, stealth browsers) needed for agents that can control entire desktops — not just web browsers.

---

*End of Report*

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*