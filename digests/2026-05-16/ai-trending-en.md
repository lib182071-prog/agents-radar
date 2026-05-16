# AI Open Source Trends 2026-05-16

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-05-16 07:32 UTC

---

# AI Open Source Trends Report — 2026-05-16

## 1. Today's Highlights

The AI open-source landscape is being reshaped by an explosion of **“agent skills”** — reusable, plug‑in capabilities for AI agents. Anthropic’s official `skills` repo and Matt Pocock’s engineer‑focused `skills` both surged today, alongside a wave of modular skill frameworks (e.g., `scientific-agent-skills`, `qiaomu-anything-to-notebooklm`). Simultaneously, the **MCP (Model Context Protocol) ecosystem** matures: `n8n-mcp` lets agents build n8n workflows on the fly, and `claude-mem` (from topic search) persists agent context across sessions. On the infrastructure side, `supertonic` brings lightning‑fast on‑device multilingual TTS, while `RuView` innovates by turning commodity WiFi into spatial intelligence — no cameras needed. The trend is clear: agents are shifting from monolithic systems to composable, skill‑based architectures.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
| Project | Stars | What it is & why it matters today |
|--------|-------|-----------------------------------|
| [supertone-inc/supertonic](https://github.com/supertone-inc/supertonic) | 0 (719 today) | Lightning‑fast, on‑device multilingual TTS running natively via ONNX — enables low‑latency voice for edge agents. |
| [NVIDIA-AI-Blueprints/video-search-and-summarization](https://github.com/NVIDIA-AI-Blueprints/video-search-and-summarization) | 0 (308 today) | GPU‑accelerated reference architecture for video understanding and vision agents. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 80,159 | High‑throughput LLM inference engine, the de‑facto standard for serving open models. |
| [ollama/ollama](https://github.com/ollama/ollama) | 171,483 | Simplified local model runner supporting Kimi‑K2.5, GLM‑5, DeepSeek, and more — essential for edge AI. |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 120,401 | Web scraping and cleaning API tailored for AI agents to fetch live data. |

### 🤖 AI Agents / Workflows
| Project | Stars | What it is & why it matters today |
|--------|-------|-----------------------------------|
| [anthropics/skills](https://github.com/anthropics/skills) | 0 (689 today) | Official Anthropic repository for Agent Skills — signals enterprise‑grade, shareable agent capabilities. |
| [mattpocock/skills](https://github.com/mattpocock/skills) | 0 (3,132 today) | Developer‑focused skills straight from the author’s `.claude` directory; practical, real‑world agent patterns. |
| [obra/superpowers](https://github.com/obra/superpowers) | 0 (1,648 today) | Agentic skills framework + software development methodology — aims to standardize agentic development. |
| [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | 0 (646 today) | Ready‑to‑use skills for research, engineering, finance, and writing — domain‑specific agent capabilities. |
| [czlonkowski/n8n-mcp](https://github.com/czlonkowski/n8n-mcp) | 0 (68 today) | MCP server that lets Claude and other agents build n8n workflows — bridges agent orchestration with low‑code automation. |
| [joeseesun/qiaomu-anything-to-notebooklm](https://github.com/joeseesun/qiaomu-anything-to-notebooklm) | 0 (438 today) | Claude Skill that converts web articles, YouTube, PDFs, etc., into podcasts, mind maps, and quizzes. |
| [ruvnet/ruflo](https://github.com/ruvnet/ruflo) | 51,655 | Leading agent orchestration platform for Claude — multi‑agent swarms, RAG integration, self‑learning. |

### 📦 AI Applications
| Project | Stars | What it is & why it matters today |
|--------|-------|-----------------------------------|
| [tinyhumansai/openhuman](https://github.com/tinyhumansai/openhuman) | 0 (1,271 today) | “Personal AI super intelligence” — private, simple, and powerful personal agent for daily tasks. |
| [ruvnet/RuView](https://github.com/ruvnet/RuView) | 0 (1,859 today) | Turns commodity WiFi signals into real‑time spatial intelligence and vital sign monitoring — privacy‑preserving sensing. |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 75,945 | Multi‑agent LLM financial trading framework — AI‑driven market analysis and execution. |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,342 | Vision for accessible autonomous agents — still a benchmark for agent‑driven problem solving. |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 94,111 | Makes websites accessible for AI agents — automates web tasks programmatically. |

### 🧠 LLMs / Training
| Project | Stars | What it is & why it matters today |
|--------|-------|-----------------------------------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 94,885 | Step‑by‑step implementation of a ChatGPT‑like LLM in PyTorch — the ultimate learning resource. |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,179 | Course on building a tiny vLLM for Apple Silicon — hands‑on LLM inference serving. |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 231 | Reliable, minimal library for pretraining foundation and world models — emerging research code. |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 6,996 | Comprehensive LLM evaluation platform supporting 100+ datasets and many models. |

### 🔍 RAG / Knowledge
| Project | Stars | What it is & why it matters today |
|--------|-------|-----------------------------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 80,599 | Leading open‑source RAG engine fused with agent capabilities — enterprise‑grade context layer. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 55,824 | Universal memory layer for AI agents — persistence across sessions, critical for long‑running agents. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 76,054 | Captures and compresses agent session context, injecting relevant memory into future sessions — works with multiple agents. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 31,346 | High‑performance vector database for semantic search at scale. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,317 | Cloud‑native vector database, the backbone for many RAG pipelines. |

## 3. Trend Signal Analysis

The most explosive community attention today is concentrated on **agent skills as a new atomic unit of AI development**. Three of the top‑starred trending repos (`mattpocock/skills` +3,132, `obra/superpowers` +1,648, `anthropics/skills` +689) are pure skill collections or skill‑frameworks. This signals a paradigm shift: instead of building monolithic agents, developers now compose, discover, and version skills like they do npm packages. The simultaneous rise of **MCP bridges** (`n8n-mcp`, `claude-mem`) suggests the ecosystem is standardising interfaces for agent capabilities.

A second vector is **on‑device and privacy‑first AI**. `supertonic` (719 today) brings high‑quality TTS without cloud dependencies, while `openhuman` (1,271 today) posits a private personal AI. `RuView` (1,859 today) pushes this further by using WiFi signals — no cameras or microphones needed. This aligns with growing concerns about data sovereignty and the “edge AI” narrative.

Notably, **vertical AI agents** gain traction: `scientific-agent-skills` and `qiaomu-anything-to-notebooklm` target research and content creation. The appearance of `n8n-mcp` suggests that **low‑code automation platforms (n8n) are being consumed by AI agents**, blurring lines between no‑code and agentic workflows.

The wave is likely triggered by Anthropic’s continued investment in Claude Code and the recent launch of their Agent SDK (implied by the `anthropics/skills` repo). We are witnessing early‑stage convergence: skill‑based agents + MCP + vector memory + on‑device inference = a new, more modular AI stack.

## 4. Community Hot Spots

- **Anthropic’s `skills` repository** — official signals from Anthropic on how to structure agent capabilities; a must‑watch for anyone building Claude‑powered tools.
- **`n8n-mcp`** — bridges agent orchestration (Claude Code, Cursor) with the popular n8n automation platform; enables agents to create complex workflows on demand.
- **`supertonic`** — on‑device TTS with ONNX runtime; lowers the barrier for voice‑enabled agents without cloud costs or latency.
- **`RuView`** — WiFi‑based sensing for spatial intelligence; opens novel non‑camera AI applications in smart buildings, healthcare, and security.
- **`claude-mem`** and **`mem0`** — persistent memory across sessions is a critical unsolved problem; these projects are setting early standards for agent context management.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*