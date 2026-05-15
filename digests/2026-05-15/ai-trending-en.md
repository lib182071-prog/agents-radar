# AI Open Source Trends 2026-05-15

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-05-15 10:00 UTC

---

# AI Open Source Trends Report — 2026-05-15

## 1. Today's Highlights

The open-source AI ecosystem is experiencing a surge in **agent-centric tooling**, with three major themes dominating today's trending lists: **(1) persistent memory for coding agents** (agentmemory, claude-mem, mem0), **(2) reusable agent skill frameworks** (superpowers, scientific-agent-skills, mattpocock/skills), and **(3) agent harnesses that wrap Claude/Cursor/Gemini** (everything-claude-code, learn-claude-code). The sharpest signal is the explosive growth of **agentmemory** (+1,879 stars today), which directly addresses the "ephemeral session" problem limiting coding agents. Meanwhile, **OpenHuman** (+3,329 stars) suggests strong appetite for private, locally-run personal AI, and **RuView** demonstrates an entirely new AI sensing modality — turning commodity WiFi into a spatial intelligence sensor. The financial AI space is also heating up with **Kronos**, a foundation model for financial markets, and **TradingAgents** (75.6k stars), signaling a push toward domain-specific LLM applications.

---

## 2. Top Projects by Category

### 🤖 AI Agents / Workflows

| Project | Stars | Today's Stars | Why It Matters Today |
|---------|-------|---------------|---------------------|
| [agentmemory](https://github.com/rohitg00/agentmemory) | 0 | +1,879 | #1 persistent memory for coding agents based on real benchmarks — solves the session-loss problem that plagues current agent workflows |
| [superpowers](https://github.com/obra/superpowers) | 0 | +1,780 | An agentic skills framework + software dev methodology — codifies how agents should learn and reuse capabilities |
| [scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | 0 | +654 | Ready-to-use agent skills for research, finance, engineering — a playbook for vertical agent specialization |
| [mattpocock/skills](https://github.com/mattpocock/skills) | 0 | +2,987 | Skills from `.claude` directory for "Real Engineers" — shows the skill-sharing ecosystem is becoming mainstream |
| [everything-claude-code](https://github.com/affaan-m/everything-claude-code) | 182,645 | — | The agent harness performance optimization system — skills, instincts, memory, security integrated |
| [roboflow/supervision](https://github.com/roboflow/supervision) | 0 | +83 | Reusable computer vision tools for agents — bridges CV pipelines into agent workflows |

### 📦 AI Applications

| Project | Stars | Today's Stars | Why It Matters Today |
|---------|-------|---------------|---------------------|
| [RuView](https://github.com/ruvnet/RuView) | 0 | +1,715 | Turns commodity WiFi into spatial intelligence and vital sign monitoring — zero-video sensing breakthrough |
| [openhuman](https://github.com/tinyhumansai/openhuman) | 0 | +3,329 | Personal AI super intelligence that's private and simple — massive traction suggests "AI for individuals" is booming |
| [supertonic](https://github.com/supertone-inc/supertonic) | 0 | +1,128 | Lightning-fast, on-device multilingual TTS via ONNX — browser/Swift-native speech synthesis |
| [NVIDIA-AI-Blueprints/video-search-and-summarization](https://github.com/NVIDIA-AI-Blueprints/video-search-and-summarization) | 0 | +62 | GPU-accelerated vision agents for video analytics — reference architecture for multimodal pipelines |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 45,706 | — | AI productivity studio with smart chat, agents, and 300+ assistants — all-in-one front-end for frontier LLMs |

### 🔧 AI Infrastructure

| Project | Stars | Today's Stars | Why It Matters Today |
|---------|-------|---------------|---------------------|
| [gstack](https://github.com/garrytan/gstack) | 0 | +915 | Garry Tan's exact Claude Code setup with 23 opinionated tools — a "CEO-in-a-box" agent infrastructure template |
| [spec-kit](https://github.com/github/spec-kit) | 0 | +1,232 | GitHub's toolkit for Spec-Driven Development — formalizing how AI agents consume specifications |
| [garrytan/gstack](https://github.com/garrytan/gstack) | 0 | +915 | 23 tools serving as CEO, Designer, Eng Manager — multi-role agent orchestration |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 80,074 | — | High-throughput LLM inference engine — the standard for serving open models |
| [ollama/ollama](https://github.com/ollama/ollama) | 171,435 | — | Run frontier models locally — now supports Kimi-K2.5, GLM-5, DeepSeek, Qwen |

### 🧠 LLMs / Training

| Project | Stars | Today's Stars | Why It Matters Today |
|---------|-------|---------------|---------------------|
| [Kronos](https://github.com/shiyu-coder/Kronos) | 0 | +363 | Foundation model for the language of financial markets — domain-specific LLM pretraining |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 151,190 | — | The agent that grows with you — open model for adaptive agent intelligence |
| [stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 229 | — | Minimal library for pretraining foundation and world models — lowers barrier for training from scratch |
| [OpenOmni](https://github.com/RainBowLuoCS/OpenOmni) | 140 | — | NIPS 2025: open-source omnimodal LLMs with emotional speech synthesis — multimodal alignment |

### 🔍 RAG / Knowledge

| Project | Stars | Today's Stars | Why It Matters Today |
|---------|-------|---------------|---------------------|
| [claude-mem](https://github.com/thedotmack/claude-mem) | 75,864 | — | Persistent context across agent sessions — compresses session data and injects relevant context |
| [mem0](https://github.com/mem0ai/mem0) | 55,775 | — | Universal memory layer for AI agents — plug-and-play persistent Recall |
| [ragflow](https://github.com/infiniflow/ragflow) | 80,562 | — | Leading open-source RAG engine with agent capabilities — fuses RAG + agents |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,306 | — | High-performance vector database for scalable ANN search — bedrock of production RAG |
| [LEANN](https://github.com/yichuan-w/LEANN) | 11,000 | — | MLsys 2026: 97% storage savings for private on-device RAG — efficiency breakthrough |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | 52,826 | — | Build AI agents visually — low-code RAG + workflow for non-engineers |

---

## 3. Trend Signal Analysis

**Explosive attention on agent memory and skills.** The single strongest signal today is the race to solve **persistent memory for coding agents**. `agentmemory` (+1,879 today), `claude-mem` (75.6k total), and `mem0` (55.8k) are all competing on the same problem: agents forget everything between sessions. This is the bottleneck preventing agents from becoming truly autonomous developers. The rise of `superpowers` and `scientific-agent-skills` suggests the industry is moving beyond "how to make agents work" to "how to make agents learn and reuse skills."

**A new sensing modality: WiFi as AI sensor.** `RuView` (+1,715 today) is the first trending project to turn commodity WiFi into a spatial intelligence sensor — no cameras, no microphones. This opens an entirely new category of privacy-preserving ambient AI for healthcare (vital signs), smart buildings (occupancy), and security. It's early but the star velocity suggests strong developer curiosity.

**Domain-specific foundation models are gaining momentum.** `Kronos` (+363 today) and `TradingAgents` (75.6k total) both target finance — a domain with structured data, clear reward functions, and high willingness to pay. The connection to recent LLM releases: as general-purpose models commoditize, differentiation shifts to vertical fine-tuning and domain-specific architectures.

**The "Claude Code ecosystem" is crystallizing.** `gstack` (+915), `everything-claude-code` (182.6k), `learn-claude-code` (60.6k), and `openclaude` (26.8k) all orbit Claude Code as the reference agent harness. This indicates Anthropic's Claude is becoming the default runtime for AI coding agents, much like VS Code for human developers.

**Privacy-first on-device AI is accelerating.** `OpenHuman` (+3,329) and `supertonic` (+1,128) both emphasize local execution. Combined with `ollama` (171k) and `picollm` (on-device LLM inference), the trend toward sovereign AI — models that run entirely on user hardware — is no longer niche.

---

## 4. Community Hot Spots

- **🥇 Persistent memory for coding agents:** Watch `agentmemory`, `claude-mem`, and `mem0`. The agent-session-memory problem is the most active open challenge in agent tooling today — whichever solution achieves "just works" persistence will become the default.

- **🥈 Agent skill marketplaces:** `superpowers` and `scientific-agent-skills` point toward a future where agents download specialized skills on demand. The `.claude` directory convention in `mattpocock/skills` and `gstack` is becoming a de facto standard.

- **🥉 WiFi-based sensing AI:** `RuView` is the first project in an entirely new category. If the 1.7k stars in one day translate to sustained development, this could parallel the early days of computer vision on mobile cameras.

- **🏅 Financial domain LLMs:** `Kronos` + `TradingAgents` + `OpenBB` (67.6k) form a growing stack for agent-driven financial analysis. The combination of structured market data and LLM reasoning is a high-value vertical.

- **🏅 On-device multilingual TTS:** `supertonic` (Swift + ONNX) is noteworthy for its platform-native approach — running TTS directly on iOS/macOS without cloud dependencies. This could power a new generation of voice-first local AI assistants.

---

*Report generated from GitHub trending and topic search data for 2026-05-15.*

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*