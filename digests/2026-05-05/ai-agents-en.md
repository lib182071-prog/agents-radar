# OpenClaw Ecosystem Digest 2026-05-05

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-05 07:32 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-05-05

## 1. Today's Overview

The OpenClaw project saw exceptionally high activity over the past 24 hours, with **500 issues and 500 pull requests updated** — roughly 39% of issues closed (305) and 26% of PRs merged/closed (131). **Four new releases** were published (three rolling betas for v2026.5.4 and one hotfix for v2026.5.3), focusing on Google Meet/Twilio voice bridge improvements, a bundled file-transfer plugin, and a security scanner fix. The maintainer team is actively closing regressions from the v2026.4.x series — at least 20 bugs were closed today — while also pushing forward major features like durable message lifecycle delivery and gateway proxy bypass controls. Community engagement remains high, with several long‑running discussions around bootstrap file loading, Docker installation friction, and text‑leak UX concerns.

## 2. Releases

Four new versions shipped today:

- **[v2026.5.4-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.5.4-beta.3)** – OpenClaw 2026.5.4-beta.3 Highlights: Google Meet/Voice Call – Twilio dial‑in joins now speak through the realtime Gemini voice bridge with paced audio streaming, backpressure‑aware buffering, barge‑in queue clearing, and no TwiML fallback during realtime speech.
- **[v2026.5.4-beta.2](https://github.com/openclaw/openclaw/releases/tag/v2026.5.4-beta.2)** – Same highlight as beta.3 (likely a copy‑and‑paste in the release notes). No additional changes documented.
- **[v2026.5.4-beta.1](https://github.com/openclaw/openclaw/releases/tag/v2026.5.4-beta.1)** – Introduces a bundled **file-transfer plugin** with `file_fetch`, `dir_list`, `dir_fetch`, and `file_write` agent tools for binary file operations on paired nodes. Default‑deny per‑node path policy under `plugins.entries.file-transfer.config.nodes` with operator approval.
- **[v2026.5.3-1](https://github.com/openclaw/openclaw/releases/tag/v2026.5.3-1)** – Core npm hotfix: stops the install scanner from blocking official bundled plugin packages when `process.env` access and normal API sends appear only in distant parts of the same compiled bundle. Published as `openclaw@2026.5.3-1` on the `beta` npm tag.

No breaking changes or migration notes are documented for these releases. However, the Feishu channel crash reported in [#77116](https://github.com/openclaw/openclaw/issues/77116) may be related to config schema changes introduced in v2026.5.2; users on earlier versions should test before upgrading.

## 3. Project Progress

**131 PRs merged/closed** today. Notable merged/closed PRs include:

- **[#77728](https://github.com/openclaw/openclaw/pull/77728)** – Changelog fix: move #77046 and #77280 entries from released `2026.5.3` to `Unreleased`.
- **[#77652](https://github.com/openclaw/openclaw/pull/77652)** & **[#77617](https://github.com/openclaw/openclaw/pull/77617)** – Expose Ollama thinking profile before plugin activation (fixes `/think max` for reasoning models like `deepseek-v4-pro:cloud`).
- **[#76747](https://github.com/openclaw/openclaw/pull/76747)** – QA Lab: add Mantis Discord status‑reaction scenario.
- **[#77304](https://github.com/openclaw/openclaw/pull/77304)** – Codex: display human‑readable duration (e.g., “5h”, “1w”) instead of “Primary/Secondary” in rate‑limit display.
- **[#77018](https://github.com/openclaw/openclaw/pull/77018)** – Gateway proxy bypass: add `proxy.loopbackMode` with three states (`gateway-only`, `proxy`, `block`).
- **[#76643](https://github.com/openclaw/openclaw/pull/76643)** – Docker security hardening: add `cap_drop` and `no-new-privileges` to gateway container.
- **[#77205](https://github.com/openclaw/openclaw/pull/77205)** – Durable message lifecycle delivery: spec and route opt‑in durable final reply delivery through a message send‑context bridge.

Several regression bugs from v2026.4.x were closed today (see §5), indicating focused triage on performance and reliability issues.

## 4. Community Hot Topics

The most active issues (by comment count and reactions) reveal several persistent pain points and user needs:

- **[#14593](https://github.com/openclaw/openclaw/issues/14593)** – *Skill install fails in Docker: `brew not installed` on Linux container* (29 comments, 17 👍). Users trying to run `openclaw onboard` inside the official Docker container hit an immediate failure when selecting `brew`‑based skills. The Docker image lacks `brew` but the skill scanner assumes it is present. This blocks onboarding for many Linux‑Power users.

- **[#25592](https://github.com/openclaw/openclaw/issues/25592)** – *Text between tool calls leaks to messaging channels* (24 comments). Agent’s internal processing output (error messages, acknowledgments) is sent to Slack, iMessage, etc., breaking UX. Users want a clean separation between internal agent steps and visible responses.

- **[#77598](https://github.com/openclaw/openclaw/issues/77598)** – *Track live dev agent behavior and trajectory* (18 comments). A running observational issue monitoring Pash’s development agent over 24 hours. Represents the project’s interest in real‑world agent observability and self‑improvement.

- **[#22438](https://github.com/openclaw/openclaw/issues/22438)** – *Tiered bootstrap file loading* (16 comments). Users want granular control over which bootstrap files are loaded in which sessions (sub‑agents, cron, etc.) to save LLM context tokens.

- **[#32473](https://github.com/openclaw/openclaw/issues/32473)** – *Control UI requires HTTPS/localhost secure context* (15 comments, 4 👍). A regression that breaks the web UI on VPS/Docker setups without HTTPS.

- **[#22676](https://github.com/openclaw/openclaw/issues/22676)** – *Signal daemon stop() race condition on SIGUSR1 restart* (15 comments). Gateway restarts can orphan Signal‑CLI processes, leading to port/file lock conflicts.

Underlying need: **reliability and UX polish** for Docker deployments, multi‑channel communication, and agent output transparency.

## 5. Bugs & Stability

The project closed at least 20 bugs today, many of them severe performance regressions introduced in v2026.4.x:

- **[#75999](https://github.com/openclaw/openclaw/issues/75999)** – *4.29 dispatch prep stages take ~73s synchronous CPU work* (closed). This blocked agent responses for 2–5 minutes.
- **[#75882](https://github.com/openclaw/openclaw/issues/75882)** – *Gateway event‑loop stalls cause cross‑channel latency* (closed).
- **[#75137](https://github.com/openclaw/openclaw/issues/75137)** – *TUI process CPU 89–99% at idle* (closed).
- **[#75703](https://github.com/openclaw/openclaw/issues/75703)** – *Gateway WS handler CPU‑spin on Raspberry Pi 5 / ARM64* (closed).
- **[#76174](https://github.com/openclaw/openclaw/issues/76174)** – *2026.4.29 – all openai/* embedded runs hang until timeout* (closed).
- **[#76057](https://github.com/openclaw/openclaw/issues/76057)** – *Gateway CPU 60–80% on ARM64 Linux, event loop blocked 37s* (closed).
- **[#75944](https://github.com/openclaw/openclaw/issues/75944)** – *Gateway timeout/reconnect loop after upgrade* (closed).
- **[#45438](https://github.com/openclaw/openclaw/issues/45438)** – *structuredClone native memory leak (~1GB/min)* (closed).
- **[#63125](https://github.com/openclaw/openclaw/issues/63125)** – *Multiple regressions in 2026.4.8* (closed today, previously reported).

**New bugs reported today (still open):**

| Issue | Severity | Description |
|-------|----------|-------------|
| [#77116](https://github.com/openclaw/openclaw/issues/77116) | **Critical** – Feishu channel crashes/restart loop after upgrade to v2026.5.2. appId/appSecret field incompatibility. | |
| [#77374](https://github.com/openclaw/openclaw/issues/77374) | **High** – Assistant messages disappear from Control UI after each new user message. Webchat channel. | |
| [#77598](https://github.com/openclaw/openclaw/issues/77598) | Medium – Observational issue, not a bug. | |

Existing high‑impact bugs that remain open: Docker `brew` install failure ([#14593](https://github.com/openclaw/openclaw/issues/14593)), Signal daemon race condition ([#22676](https://github.com/openclaw/openclaw/issues/22676)), agent replies to wrong message ([#32296](https://github.com/openclaw/openclaw/issues/32296)), and control UI HTTPS requirement ([#32473](https://github.com/openclaw/openclaw/issues/32473)).

## 6. Feature Requests & Roadmap Signals

Several user‑requested features with traction:

- **Tiered bootstrap file loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438)) – likely to be prioritized given high comment count and token‑saving benefit.
- **Post‑subagent completion hook** ([#22358](https://github.com/openclaw/openclaw/issues/22358)) – for automated trajectory generation.
- **Recursive memory_search** ([#34400](https://github.com/openclaw/openclaw/issues/34400)) – supports growing daily‑note directories.
- **`announceTarget` for sub‑agent completion** ([#27445](https://github.com/openclaw/openclaw/issues/27445)) – allows parent agent orchestration.
- **Fallback approval mode + model attribution** ([#33975](https://github.com/openclaw/openclaw/issues/33975)) – transparency for users when models fail over.
- **Security Profile v1.1** ([#8719](https://github.com/openclaw/openclaw/issues/8719)) – data‑centric security defaults.

PRs merged/under review that signal near‑term roadmap:

- **Durable message lifecycle delivery** ([#77205](https://github.com/openclaw/openclaw/pull/77205)) – large refactor likely targeting v2026.5.5.
- **Gateway proxy bypass control** ([#77018](https://github.com/openclaw/openclaw/pull/77018)) – adds three modes for loopback traffic.
- **Container security hardening** ([#76643](https://github.com/openclaw/openclaw/pull/76643)) – likely to become default.
- **Configurable typing indicator TTL** ([#72009](https://github.com/openclaw/openclaw/pull/72009)) – simple quality‑of‑life improvement.

Predictions for next minor release (v2026.5.5): the durable message lifecycle spec, gateway proxy controls, and thinking‑profile fixes for Ollama will likely land. The Feishu crash (critical) may prompt a hotfix before then.

## 7. User Feedback Summary

**Pain points expressed today:**

- Docker users still blocked by missing `brew` for skill installation ([#14593](https://github.com/openclaw/openclaw/issues/14593)).
- Agent internal text leaking to channels ruins conversational flow ([#25592](https://github.com/openclaw/openclaw/issues/25592)).
- Bootstrap files in `agentDir` silently ignored ([#29387](https://github.com/openclaw/openclaw/issues/29387)).
- `exec` tool not inheriting skill environment variables ([#31583](https://github.com/openclaw/openclaw/issues/31583)).
- Feishu upgrade breakage ([#77116](https://github.com/openclaw/openclaw/issues/77116)) undermines confidence in smooth upgrades.
- Assistant messages disappearing in Web UI ([#77374](https://github.com/openclaw/openclaw/issues/77374)) with high severity.

**Positive signals:**

- Rapid closure of severe regression bugs (CPU starvation, memory leaks, timeouts) shows strong maintenance velocity.
- Many users contributing detailed root‑cause analyses (heap sampling, timing diagrams), indicating an engaged technical community.

**Overall satisfaction/dissatisfaction:** Users appreciate the fast release cycle but are frustrated by regressions that require downgrading. Docker and Windows users remain the most affected by platform‑specific bugs.

## 8. Backlog Watch

Long‑standing issues that still lack maintainer action:

| Issue | Age (days) | Comments | Why it matters |
|-------|------------|----------|----------------|
| [#14593](https://github.com/openclaw/openclaw/issues/14593) – Docker brew install | 82 | 29 | Blocks Docker onboarding for many users |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) – Signal daemon race | 73 | 15 | Affects Signal channel reliability |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) – Text leaks to channels | 70 | 24 | Critical UX issue, no fix PR yet |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) – Tiered bootstrap | 73 | 16 | High‑value feature, no PR |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) – Control UI HTTPS required | 63 | 15 | Regression affecting VPS/Docker users |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) – AgentDir bootstrap ignored | 66 | 13 | Breaks per‑agent configuration |
| [#32296](https://github.com/openclaw/openclaw/issues/32296) – Agent replies to wrong message | 64 | 11 | Conversation misalignment bug |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) – exec missing env | 64 | 11 | Blocks skill secret injection |

**PRs needing attention:** The large refactoring PRs [#43469](https://github.com/openclaw/openclaw/pull/43469) (Markdown injection scanning, 55 days open) and [#52747](https://github.com/openclaw/openclaw/pull/52747) (ACP task timeout, 43 days) have no recent activity and may conflict with newer changes. The maintainer team should review these before they grow stale.

---

## Cross-Ecosystem Comparison

Based on the provided community digests for 2026-05-05, here is a cross-project comparison report for the open-source personal AI assistant and agent ecosystem.

---

## Cross-Project Comparison Report: Personal AI Agent Ecosystem
**Date:** 2026-05-05
**Analyst:** Senior Analyst, AI Agent & Personal AI Assistant Ecosystem

### 1. Ecosystem Overview

The open-source personal AI agent landscape is experiencing a phase of rapid, high-velocity iteration, with the largest projects (OpenClaw, Hermes Agent, ZeroClaw) processing hundreds of issues and pull requests daily. The dominant themes across the ecosystem are a push toward production-grade reliability (solving Docker deployment friction, memory leaks, and crash-causing race conditions) and a strong user demand for transparent, observable agent behavior (e.g., thinking/reasoning visibility, progress feedback). While projects share core goals—multi-channel communication, LLM provider abstraction, and tool-use safety—they are diverging in architectural philosophy, with some (IronClaw) pursuing a full micro-service "Reborn" rewrite and others focusing on pragmatic plugin and skill ecosystems. A key tension remains between rapid feature development and the stability regressions this velocity introduces, a frustration frequently voiced by the community.

### 2. Activity Comparison

| Project | Issues (Open/Closed) | PRs (Open/Closed) | Release Status | Health Score | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 495 / 305 | 369 / 131 | **New release (4)** | **Healthy** | Highest absolute activity. Rapid bug closure offsets critical Feishu crash. |
| **Hermes Agent** | 43 / 7 | 43 / 7 | No new release | **Active but fragile** | High severity, P0 CLI crash (#19903) and gateway session leaks (#20098) are red flags. |
| **NanoBot** | 6 / 0 | 10 / 8 | No new release | **Stable** | Low issue count, steady PR flow. A mature, well-maintained project. |
| **PicoClaw** | 14 / 15 | 19 / 40 | **New build (nightly)** | **Healthy** | Very high PR throughput (59). Critical authentication bug (#2769) is a concern. |
| **NanoClaw** | 4 / 1 | 17 / 18 | No new release | **Stable** | Strong contributor velocity. Security PR backlog (10+ days) needs attention. |
| **NullClaw** | 1 / 0 | 3 / 2 | **New release (patch)** | **Steady** | Low activity niche project. Focused on skill ecosystem alignment. |
| **IronClaw** | 1 / 0 | 16 / 12 | No new release | **Active (architectural)** | Heavy internal refactoring ("Reborn"). Low user-facing activity; high internal churn. |
| **LobsterAI** | 0 / 1 | 0 / 2 | No new release | **Stable** | Low activity. Critical crash fix (PR #808) has been open for over a month. |
| **TinyClaw** | - | - | - | **Dormant** | No activity in the last 24 hours. |
| **Moltis** | 1 / 0 | 0 / 1 | No new release | **Low activity** | Single, high-severity Docker sandbox collision bug with no fix yet. |
| **CoPaw** | 11 / 2 | 8 / 4 | No new release | **Stable** | Consolidation phase. Critical streaming model bug (#4034) needs attention. |
| **ZeptoClaw** | 0 / 0 | 11 / 0 | No new release | **Maintenance** | All activity is automated dependency bumps. No community engagement. |
| **ZeroClaw** | 37 / 13 | 29 / 21 | No new release | **Active (milestone-driven)** | Strong forward momentum. S0 data-spillage bug (#5415) is a major risk. |

### 3. OpenClaw's Position

**Advantages:**
- **Dominant Community:** With ~500 issues and PRs updated in 24 hours, OpenClaw has the largest and most active community in the ecosystem. This velocity allows rapid bug squashing (20 bugs closed today) and feature integration.
- **Breadth of Features:** OpenClaw is the only project to ship a bundled file-transfer plugin, durable message lifecycle delivery, and advanced voice bridge features (Google Meet, Twilio with barge-in and backpressure) in a single day.
- **Release Cadence:** Four releases in one day, including hotfixes, demonstrates a mature CI/CD pipeline and a proactive response to regressions.

**Technical Approach Differences:**
- OpenClaw uses a **centralized gateway architecture** with proxy bypass controls, while projects like IronClaw are refactoring toward a micro-service "substrate" model. This makes OpenClaw more monolithic but also simpler to deploy.
- OpenClaw's plugin system is deeply integrated, allowing for rapid community contributions, whereas ZeroClaw is considering removing dedicated tool code in favor of a similar skill-based system.

**Community Size Comparison:**
- OpenClaw's community is an order of magnitude larger than any other project in this cohort. The next most active projects (Hermes, ZeroClaw) each touched ~50 items, compared to OpenClaw's ~1,000. This gives OpenClaw a significant advantage in bug discovery and feature contribution.

### 4. Shared Technical Focus Areas

The following needs are emerging across multiple projects, indicating ecosystem-wide pain points and opportunities:

- **Docker & Deployment Friction (5 projects):**
  - **OpenClaw:** `brew` not installed in Docker container (#14593).
  - **PicoClaw:** Gateway starts with no channels in Docker (#2690, #2742).
  - **ZeroClaw:** Dashboard unavailable in Docker (#5959, now fixed).
  - **CoPaw:** Missing dependencies in Docker image (#1508, now fixed).
  - **Hermes:** Gateway drain hangs on WSL+Feishu (#19937).

- **Voice & Audio Integration (3 projects):**
  - **OpenClaw:** Google Meet/Twilio voice bridge with Gemini.
  - **ZeroClaw:** Matrix voice transcription fails (#6153).
  - **PicoClaw:** TTS/ASR support is a top community request (#1648).

- **MCP (Model Context Protocol) Tool Reliability (4 projects):**
  - **NanoClaw:** `send_card` MCP tool silent on Chat SDK (#2263).
  - **CoPaw:** MCP timeout hard-coded to 30s (#4033).
  - **Hermes:** `add_mcp_server` registrations silently dropped (#2241).
  - **ZeroClaw:** Nextcloud Talk MCP requests canceled (#6156).

- **Provider Interoperability (4 projects):**
  - **NanoClaw:** Cannot connect to local `llama.cpp` (#2234).
  - **PicoClaw:** Authentication header missing for OpenAI-compatible endpoints (#2578).
  - **ZeroClaw:** `default_model` not found on remote Ollama (#6123).
  - **Hermes:** CLI crashes due to unsupported keybinding, breaking all users (#19903).

- **Agent Observability (4 projects):**
  - **NullClaw:** Option to show reasoning/thinking during long tasks (#886).
  - **OpenClaw:** Text between tool calls leaks to messaging channels (#25592).
  - **PicoClaw:** Progress feedback during tool execution (#571).
  - **Hermes:** TUI transcript scroll blank after row cache drift (#19944).

### 5. Differentiation Analysis

| Feature/Aspect | OpenClaw | Hermes (NousResearch) | ZeroClaw | PicoClaw | NanoBot |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Core Focus** | Centralized multi-channel gateway + agent | CLI/TUI agent with delegation & skills | Fleet/daemon management & dashboard | Embedded/mobile agent (SiPEED) | SDK ecosystem & multi-provider support |
| **Target User** | Power users, enterprises, self-hosters | Developers, terminal power users | System admins, fleet operators | Hobbyists, mobile users, edge devices | Developers building custom agents |
| **Architecture** | Monolithic gateway with plugins | Process-per-user CLI with sub-agents | Daemon nodes with a central dashboard | Single-binary (Go) for portability | Lightweight SDK with modular providers |
| **Key Differentiator** | File-transfer plugin, durable message lifecycle | Anthropic WIF support, Kanban orchestration | Air-gapped execution RFC, context-spillage fix | OpenRouter model rotation, context compression | Safety guards, session-level focus tool |
| **Deployment Model** | Docker/Podman, npm install | pip/brew, CLI | Docker/separate containers | Android APK, Raspberry Pi, Go binary | PyPI, pip install |

### 6. Community Momentum & Maturity

**Tier 1: High Velocity / Rapid Iteration**
- **OpenClaw, ZeroClaw, Hermes Agent:** These projects are processing 50+ items daily. They exhibit a "release early, release often" culture, which generates community excitement but also introduces regressions that frustrate users. They are the ecosystem's innovation drivers.

**Tier 2: Steady Growth / Consolidation**
- **PicoClaw, NanoBot, CoPaw, NanoClaw:** These projects show healthy, sustainable activity. They release less frequently but are building robust features (context compression, skill managers, session focus). PicoClaw's very high PR count (59) is notable.

**Tier 3: Niche but Active**
- **IronClaw, NullClaw:** IronClaw is focused on a major architectural overhaul ("Reborn"), with low user-facing features. NullClaw is a smaller project aligning with the Agent Skills ecosystem. Both are stable but not rapidly expanding.

**Tier 4: Dormant or Maintenance-Only**
- **LobsterAI, Moltis, ZeptoClaw, TinyClaw:** These projects show minimal to no community activity. LobsterAI has a critical crash fix stalled for a month. ZeptoClaw is only receiving Dependabot PRs. They are at risk of falling behind as the ecosystem matures.

**Maturity Assessment:**
- **Most Mature:** **NanoBot** (low bug count, steady fixes) and **PicoClaw** (high PR throughput, strong community features).
- **Most at Risk:** **Hermes** (high severity, unaddressed P0 bugs), **LobsterAI** (stale critical fix), and **Moltis** (single high-severity bug with no solution).

### 7. Trend Signals for AI Agent Developers

The following trends are consistent across the feedback of thousands of users and hundreds of issues. They represent key areas for investment and product focus:

1.  **Voice & Audio is the Next UX Frontier:** The intense focus on voice bridges (OpenClaw, PicoClaw) and transcription (ZeroClaw) signals that users are moving beyond text-only chat. Agents must handle multi-modal input and paced, interruptible speech output.

2.  **“Observability or Bust”:** The demand for progress indicators, reasoning/thinking visibility, and "health" dashboards (ZeroClaw, NullClaw, PicoClaw) shows that users will not tolerate a black-box agent. Developers must prioritize streaming, phased, and cancellable agent actions.

3.  **Self-Hosted LLM Integration is a Hard Requirement:** The repeated failures to connect to `llama.cpp`, Ollama, and custom OpenAI endpoints (NanoClaw, ZeroClaw, PicoClaw) are a significant barrier. For agents to truly become personal, they must work seamlessly with local, private models.

4.  **Sandbox Security is Non-Negotiable:** From `find /` path traversal in PicoClaw (#2688) to Docker name collisions in Moltis (#964) to context spillage in ZeroClaw (#5415), security is the #1 risk for production deployment. Developers must build air-gapped execution and strict data isolation from day one.

5.  **"Skill" Ecosystem Convergence:** The trend is away from monolithic, built-in tools toward dynamically loadable, user-contributed "skills" or "plugins." OpenClaw, Hermes, CoPaw, ZeroClaw, and NullClaw are all converging on this model. A universal skill standard is likely to emerge.

6.  **Multi-Tenancy and Team Features are Emerging:** Requests for Discord channel scoping (ZeroClaw), multi-agent squads (NanoBot), and delegation sub-agent routing (Hermes) indicate that personal agents are being adapted for team and enterprise use. Single-user architecture will be a limitation.

7.  **Token & Context Optimization is a Core Concern:** Features like tiered bootstrap loading (OpenClaw), structured context compression (PicoClaw), and configurable memory consolidation (NanoBot) show that managing LLM context windows is a critical, unsolved user pain point. Any improvement in this area provides a significant competitive advantage.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-05

## 1. Today's Overview

Activity remains high with 6 issues and 18 PRs updated in the last 24 hours. The project closed 8 PRs, indicating steady progress on both bug fixes and feature development. Community engagement is strong, especially around the long-standing model failover enhancement (#3376) and a new session-level focus tool (#3292). Two Telegram-related bugs (#3626, #3625) were reported today, with immediate fix PRs submitted (#3627, #3629). No new releases were published.

## 2. Releases

No new releases today. (Latest release information not available.)

## 3. Project Progress (Merged/Closed PRs Today)

Eight PRs were merged or closed, advancing several areas:

- **SDK / Core**  
  - [#3254](https://github.com/HKUDS/nanobot/pull/3254) – Fixed `RunResult.tools_used` and `RunResult.messages` being hard-coded to `[]`.  
  - [#3613](https://github.com/HKUDS/nanobot/pull/3613) – Prevented safety guard false positives (e.g., `/dev/*` paths) and streamed message drops.

- **Telegram / Channels**  
  - [#3480](https://github.com/HKUDS/nanobot/pull/3480) – Restored intermediate progress deltas for OpenAI Codex provider in channels.  
  - [#3548](https://github.com/HKUDS/nanobot/pull/3548) – Reverted a prior Feishu streaming card fix due to side effects.

- **Memory**  
  - [#3281](https://github.com/HKUDS/nanobot/pull/3281) – Made memory consolidation ratio configurable (range 0.1–0.95).

- **LLM Fallback**  
  - [#1163](https://github.com/HKUDS/nanobot/pull/1163) – Implemented fallback chain on retriable errors (Timeout/503/502/429). (Closed after updates.)

- **Web Search**  
  - [#3091](https://github.com/HKUDS/nanobot/pull/3091) – Added support for custom `base_url` in Tavily provider.

- **Workspace / Custom Providers**  
  - [#3080](https://github.com/HKUDS/nanobot/pull/3080) – Introduced custom provider support and workspace command loading.

## 4. Community Hot Topics

- **Issue #3376** – *Support model provider/model failover on errors*  
  (13 comments, 👍1)  
  [Link](https://github.com/HKUDS/nanobot/issues/3376)  
  User requests automatic switching to alternative providers/models when hitting timeouts, 429s, or 5xx errors. This complements the recently merged fallback chain PR (#1163) but asks for a higher-level orchestration layer.

- **Issue #3292** – *Session-level focus tool for persistent task awareness*  
  (7 comments, 👍0)  
  [Link](https://github.com/HKUDS/nanobot/issues/3292)  
  Proposes an improved “task board” mechanism to maintain attention on a primary goal across interruptions. The `my` tool’s current scratchpad is deemed insufficient.

- **Issue #2804** – *DuckDuckGo web search hangs indefinitely* (CLOSED)  
  [Link](https://github.com/HKUDS/nanobot/issues/2804)  
  A long-standing blocking bug was finally closed, indicating a fix has been merged or mitigated.

## 5. Bugs & Stability

Three new bugs reported today, ranked by severity:

1. **High: Telegram long polling silently hangs**  
   - [#3626](https://github.com/HKUDS/nanobot/issues/3626) – Network outages cause the bot to stop receiving updates while staying alive and able to send messages. No error logged.  
   - **Fix PR**: [#3627](https://github.com/HKUDS/nanobot/pull/3627) adds a watchdog to detect and recover from silent hangs.

2. **Medium: Dream advances cursor on error, dropping memory entries**  
   - [#3630](https://github.com/HKUDS/nanobot/issues/3630) – `agent/memory.py` writes cursor even when Phase 1 fails, silently discarding valid memory entries. No Telegram surface for diagnostics.

3. **Low: WhatsApp sends each token as separate message**  
   - [#3625](https://github.com/HKUDS/nanobot/issues/3625) – When using OpenAI Codex with `supports_progress_deltas=True`, WhatsApp floods the chat with per-token messages.

Additionally, PR [#3629](https://github.com/HKUDS/nanobot/pull/3629) fixes unauthorized user handling in Telegram (silent ignore instead of replying to `/start`/`/help`).

## 6. Feature Requests & Roadmap Signals

Active feature PRs hinting at upcoming capabilities:

- **Multi-agent squad deployment** – [#3621](https://github.com/HKUDS/nanobot/pull/3621) targets Hugging Face Spaces with a gatekeeper middleware for OAuth and port forwarding.
- **Message preprocessing hook** – [#3628](https://github.com/HKUDS/nanobot/pull/3628) adds `before_process` callback for media preprocessing.
- **Hallucinated tool-call guard** – [#3624](https://github.com/HKUDS/nanobot/pull/3624) detects when the model claims an action without actually calling a tool.
- **Configurable tool hint truncation** – [#3623](https://github.com/HKUDS/nanobot/pull/3623) makes `toolHintMaxLength` user-adjustable.
- **Persistent focus key** – [#3622](https://github.com/HKUDS/nanobot/pull/3622) reuses the existing `my` tool’s scratchpad to automatically inject a focus key from session metadata, directly addressing issue #3292.

Longer-term roadmap signals: the SDK capture hook PR [#3620](https://github.com/HKUDS/nanobot/pull/3620) (open) aims to wire `tools_used` and `messages` properly, and issue #3376 (failover chain) is likely to be addressed in the next minor version given the community pressure.

## 7. User Feedback Summary

- **Pain points**  
  - Silent service degradation (Telegram polling, DuckDuckGo search) frustrates users who notice only after tasks fail.  
  - Memory fragmentation during Dream loops reduces reliability.  
  - WhatsApp channel unusable with streaming providers due to token-level messaging.

- **Use cases**  
  - Multi‑provider redundancy is critical for production deployments (e.g., multiple API keys for resilience).  
  - Session-level focus is essential for complex, interrupt-driven workflows.

- **Satisfaction**  
  - The rapid fix PRs (#3627, #3629) and closure of long‑standing bugs (#2804) show responsiveness.  
  - Configurable memory consolidation (#3281) was positively received as it gives users control over fidelity vs. compression.

## 8. Backlog Watch

- **Issue #3292** – Session-level focus tool (created Apr 19, 7 comments) has a corresponding PR [#3622](https://github.com/HKUDS/nanobot/pull/3622) but the design discussion is still open. Requires maintainer decision on scope.
- **Issue #3376** – Model failover (created Apr 22, 13 comments) is the most active open feature request. The recent merge of basic fallback (#1163) may be seen as an interim solution; users want a fully integrated failover orchestration layer.
- **PR #2438** – ImageContent handling in MCP responses (open since Mar 24) has no recent activity. Needs reviewer attention to avoid falling behind.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-05

## Today’s Overview
Hermes Agent experienced a highly active day with **50 Issues and 50 PRs updated in the last 24 hours**. Of those, 43 Issues and 43 PRs remain open, while 7 of each were closed or merged. No new releases were cut. The activity mix skews heavily toward bug fixes and stability improvements — several P0/P1 crashes have been identified and are already being addressed by corresponding fix PRs. The community continues to drive feature requests, especially around multi-tenancy, mobile integration, and authentication. Overall project health is good but warrants close monitoring of the growing open-issue count.

## Releases
No new releases today.

## Project Progress
Seven PRs were merged or closed today (based on the top 20 PRs listed). These include:
- **#20087** – fix(model_tools): log plugin hook exceptions instead of silently swallowing
- **#20088** – fix(tools): use `tempfile.gettempdir()` instead of hardcoded `/tmp`
- **#20089** – fix(security): quote background process command with `shlex.quote()`
- **#20090** – fix(model_tools): narrow exception handler to `ImportError`/`AttributeError`

Additionally, several high-priority bugs were closed:
- **#487** – Feature: Cryptographic Audit Trail (closed after implementation)
- **#19567** – TUI delegation subagent routing to wrong provider (fixed)
- **#19861** – `claw migrate` produces wrong `api_mode` for byoky-anthropic (fixed)
- **#17558** – Persistent shell cwd deleted causing ENOENT (closed)
- **#15989** – TUI fails when cwd contains a Python package named `utils/` (closed)

These closures reflect continued progress on CLI/TUI stability, configuration correctness, and terminal safety.

## Community Hot Topics
The most active discussions (by comment count) reveal key community concerns:

- **#19903** (7 comments, 4 👍) – *CLI crash on startup: Invalid key `c-S-c`*  
  A P0 regression affecting all users. The root cause is a hardcoded `Ctrl+Shift+C` binding that `prompt_toolkit` does not support. Users are blocked immediately on launch.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19903)

- **#14420** (6 comments) – *Agent unable to give accurate answer based on previous context*  
  A Chinese-speaking user reports that the agent fails to remember named entities (e.g., “小明”) across turns, pointing to a memory/context pipeline issue.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/14420)

- **#19567** (5 comments, now closed) – *TUI delegation subagent incorrectly routed to copilot-acp*  
  A configuration bug that prevented correct provider fallback in TUI mode. The fix has been merged.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19567)

- **#19861** (4 comments, now closed) – *`claw migrate` produces wrong api_mode for byoky-anthropic*  
  Fresh users hit a 404 on migrate because the generated config used the wrong API path. Already fixed.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19861)

- **#20074** (3 comments) – *Kanban CLI invoked from agent session ignores active-board pin*  
  A race condition between in-process `kanban_*` tools and shelled-out `harness kanban` commands, causing task invisibility.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/20074)

The underlying theme: users are encountering configuration mismatches, environment-dependent crashes, and race conditions in multi-tool workflows, which highlights the need for more robust integration testing and documentation of edge cases.

## Bugs & Stability
Below are the most severe bugs reported today, ranked by priority. Fix PRs are noted where available.

| Priority | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **P0** | #19903 | CLI crash on startup: invalid key `c-S-c` | No PR yet |
| **P1** | #20098 | Gateway session store leaks orphaned JSON files, desyncs session index | No |
| **P1** | #19981 | OpenAI headers from PR #12664 silently dropped due to wrong SDK attribute | No |
| **P1** | #20001 | TUI compression creates ghost sessions with incomplete metadata | No |
| **P2** | #19567 (closed) | TUI delegation subagent wrong provider | Already fixed |
| **P2** | #19937 | Gateway drain hangs on wedged adapter websockets (WSL+Feishu/Weixin) | #19946 (open) |
| **P2** | #19944 | TUI transcript scroll blank after virtual row height cache drift | No |
| **P2** | #20035 | Feishu DM pairing mode drops messages under high frequency | No |
| **P2** | #20064 | Terminal safety filter false-positives on background keywords inside quoted strings | #20099 (open) |
| **P2** | #20084 | TUI Markdown rendering strips asterisks in code blocks | #20091 (open) |
| **P2** | #18872 | `skill_view`/`skills_list` name mismatch breaks tool-calling loop | No |
| **P3** | #20002 | MacOS Voice crash (sigfault) with sounddevice library | No |
| **P3** | #19992 | `url_safety.py` incorrectly blocks RFC 2544 (198.18.0.0/15) used by Clash TUN | No |
| **P3** | #18875/18876 | Hindsight memory provider crashes gateway if client not installed | No duplicate |

The high number of P1 bugs — especially gateway session leaks and silent header dropping — suggests the gateway and agent core need more thorough regression testing. The community has also flagged several platform-specific issues (WSL, MacOS, Feishu) that may require platform maintainers.

## Feature Requests & Roadmap Signals
Several feature requests emerged today with strong community traction:

- **#19986** – *Make non-core bundled skills optional, keep default install minimal*  
  Users want a lighter default installation, reducing maintenance burden for skills they never use.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19986)

- **#20078** – *Support Anthropic Workload Identity Federation (WIF)*  
  A keyless authentication method replacing static API keys. A corresponding PR **#20073** has already been opened.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/20078)

- **#11712** – *Expose a local WebSocket interface for third-party clients (e.g. CoClaw mobile app)*  
  This would allow native mobile apps to connect to Hermes. Opened 2026-04-17, still awaiting maintainer engagement.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/11712)

- **#19922** – *Expand `display.runtime_footer` to include all variables from `/usage`*  
  Multi-agent operators need real-time cost/token monitoring without manual `/usage` commands.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19922)

- **#19198** – *Refactor web tools into capability-based provider architecture*  
  Would allow combining different backends (e.g., SearXNG for search + Firecrawl for extract). No PR yet.
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19198)

Additionally, PR **#19989** (Feishu multitenancy bundled plugin) and **#20096** (channel-based profile routing for Discord) indicate strong enterprise demand for multi-tenant, multi-persona deployments.

**Prediction for next release:** The WIF authentication support (#20078 + #20073) and the non-core skills optional feature (#19986) are likely candidates. The gateway session leak fix (#20098) and the CLI crash fix (#19903) are urgent enough to warrant hotfixes.

## User Feedback Summary
Real user pain points captured today:

- **Chinese users** (#14420) report that the agent cannot remember named context (e.g., “我叫小明”) despite short message histories, suggesting either a memory provider bug or conversation summarisation issue.
- **MacOS users** (#20002) experience signal faults when using voice-to-voice interactions with tool calls, making long sessions unstable.
- **WSL users** (#19937) face gateway shutdown hangs due to wedged Feishu/Weixin websockets, requiring manual `systemctl` intervention.
- **New users** (#19861) are blocked immediately after `claw migrate` because the generated config points to a nonexistent API endpoint.
- **Kanban orchestrator users** (#20074) lose tasks when mixing in-process tools and CLI commands in the same turn, breaking automation workflows.
- **Community request for minimal install** (#19986) indicates that the default installation footprint is too large for many users, especially those only using a few skills.

User satisfaction is mixed: while bug fixes are being delivered quickly (many closed today), the volume of new issues suggests that regressions are introduced at a pace that frustrates early adopters. On the positive side, feature requests like WIF and channel-based routing show that power users see Hermes as a platform worth investing in.

## Backlog Watch
Several important issues have remained open for days or weeks without maintainer attention:

- **#11712** (2026-04-17) – *WebSocket interface for third-party clients*  
  Only 1 comment. A foundational feature for mobile integration, yet no maintainer response.  
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/11712)

- **#19198** (2026-05-03) – *Capability-based provider architecture for web tools*  
  Zero comments from maintainers. A significant refactor that could streamline web tool configuration.  
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19198)

- **#19533** (2026-05-04) – *Require dashboard auth for Kanban plugin API*  
  Security vulnerability: Kanban plugin routes bypass session middleware, allowing unauthenticated mutations. Only 2 comments, no PR.  
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/19533)

- **#18875** (2026-05-02) – *Hindsight memory provider crashes gateway without error*  
  A duplicate exists (#18876). Causes infinite Docker restart loops. No fix PR yet.  
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/18875)

- **#20060** (2026-05-05) – *API Server lacks session key interface for long-term memory scoping*  
  A user integrating Hermes with a third-party Web UI reports that the API Server does not expose the `session_key` concept used by CLI/gateway. This limits external integrations.  
  [Issue Link](https://github.com/NousResearch/hermes-agent/issues/20060)

These items, especially #11712 and #19533, represent missing capabilities and potential security holes that could hinder adoption. Maintainers should prioritize triaging them in the coming days.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-05

## Today's Overview
PicoClaw saw extremely high activity in the past 24 hours, with **29 issues updated** (14 open/active, 15 closed) and **59 pull requests** updated (19 open, 40 merged/closed). One automated **nightly build** was released. The project is moving quickly — nearly 70% of PR updates were merged or closed, and several long-standing bugs and enhancements landed. The community continues to push for voice support, easier local model integration, and better configuration UX. However, a critical authentication bug affecting multiple providers surfaced today, while some open issues remain stale despite high interest.

## Releases
- **Nightly Build** `v0.2.8-nightly.20260505.57459574` — automated build based on the latest `main` branch. May be unstable. No explicit breaking changes or migration notes provided. Full changelog: [compare v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)

## Project Progress (Merged/Closed PRs Today)
40 PRs were merged or closed today. Key highlights:

- **Tool feedback UX** — `feat(agent): add pretty_print and disable_escape_html options for tool feedback` ([#2670](https://github.com/sipeed/picoclaw/pull/2670)) merged, fixing Unicode escape issues in tool previews.
- **FreeRide tool** — Automated OpenRouter model rotation and fallback management ([#2603](https://github.com/sipeed/picoclaw/pull/2603)) merged.
- **Structured context compression** — A 6-phase algorithm for iterative summaries with token-budget protection ([#2333](https://github.com/sipeed/picoclaw/pull/2333)) merged.
- **SkillManager** — CRUD operations for dynamic skill creation, with duplicate detection ([#2332](https://github.com/sipeed/picoclaw/pull/2332)) merged.
- **Thinking level fix** — Agent now correctly resolves `thinking_level` from model references ([#2336](https://github.com/sipeed/picoclaw/pull/2336)) merged.
- **Dependency updates** — AWS Bedrock Runtime SDK bump ([#2731](https://github.com/sipeed/picoclaw/pull/2731)) and general `go mod tidy` with minor fixes ([#2331](https://github.com/sipeed/picoclaw/pull/2331)) closed.

Additionally, several open PRs added new capabilities (see Section 4 and 6).

## Community Hot Topics
The following issues and PRs attracted the most discussion and reactions:

- **TTS/ASR Support** ([#1648](https://github.com/sipeed/picoclaw/issues/1648)) — 24 comments, closed. Feature request with an existing PR (#1642) but not yet integrated into the gateway. Community strongly desires voice interaction.
- **LM Studio Easy Connect** ([#28](https://github.com/sipeed/picoclaw/issues/28)) — 17 comments, 2 👍, open since Feb. Users want a simple way to connect to LM Studio’s local inference server, especially on Android.
- **openai_compat Authentication Header Missing** ([#2578](https://github.com/sipeed/picoclaw/issues/2578)) — 13 comments, closed. A v0.2.6 bug where the API key was silently dropped, breaking all HTTP-based providers.
- **Self-Upgrade Support** ([#618](https://github.com/sipeed/picoclaw/issues/618)) — 11 comments, 2 👍. Users want automatic updates via package managers (deb, winget, opkg).
- **Progress Feedback During Tool Execution** ([#571](https://github.com/sipeed/picoclaw/issues/571)) — 8 comments. Agents execute tools silently; users request visible progress indicators (e.g., in Telegram).

**Analysis:** The underlying needs are (1) better integration with local/third-party LLM providers, (2) more transparent agent behaviour, and (3) easier deployment and lifecycle management.

## Bugs & Stability
Several bugs were reported or updated today, ranked by severity:

- **HIGH — Authentication fails with valid API keys (401 across providers)** ([#2769](https://github.com/sipeed/picoclaw/issues/2769)). Affects Groq, OpenRouter, Nvidia on both stable and nightly builds. Possibly a regression. No fix PR yet.
- **HIGH — Security: `find /` can enumerate paths outside workspace sandbox** ([#2688](https://github.com/sipeed/picoclaw/issues/2688)). Stale since 2026-04-27. The sandbox blocks direct `cat`/`ls` but `find` bypasses. Critical for agent safety.
- **MEDIUM — Gateway starts with no channels in v0.2.7 and v0.2.8** ([#2690](https://github.com/sipeed/picoclaw/issues/2690), [#2742](https://github.com/sipeed/picoclaw/issues/2742)). Affects Telegram, QQ on Docker. Users must downgrade or patch config.
- **MEDIUM — Codex OAuth returns empty assistant response** ([#2674](https://github.com/sipeed/picoclaw/issues/2674)). ChatGPT backend streaming issue. Related PR: [#2679](https://github.com/sipeed/picoclaw/pull/2679) (open) and [#2581](https://github.com/sipeed/picoclaw/pull/2581) (open) aim to recover output from stream events.
- **LOW — Android app service not starting** ([#2590](https://github.com/sipeed/picoclaw/issues/2590)). Stale, no recent activity.
- **LOW — Skill address parsing error** ([#2684](https://github.com/sipeed/picoclaw/issues/2684)). Third-party skill URLs fail.

## Feature Requests & Roadmap Signals
Notable user-requested features from recent issues and PRs:

- **MCP Configuration in Web UI** ([#2770](https://github.com/sipeed/picoclaw/pull/2770)) – New PR adding MCP management to the config interface.
- **Intel OpenVINO Model Server support** ([#2703](https://github.com/sipeed/picoclaw/pull/2703)) – Local LLM inference on Intel hardware.
- **Telegram forum topic preservation for tool messages** ([#2772](https://github.com/sipeed/picoclaw/pull/2772)) – Fixes thread routing in group chats.
- **Gemini Web Search provider** ([#2763](https://github.com/sipeed/picoclaw/pull/2763)) – New web search backend.
- **Config reliability & migration UX** ([#2771](https://github.com/sipeed/picoclaw/issues/2771)) – Outdated example config, missing migration command, manual remote backup needed.
- **Raspberry Pi / Pi Zero 2W support** ([#2675](https://github.com/sipeed/picoclaw/issues/2675)).
- **Serp API web search** ([#2232](https://github.com/sipeed/picoclaw/issues/2232)) – Free alternative to Brave Search.

**Likely next-version items:** The MCP config UI (#2770) is a small, focused enhancement; the Gemini search provider (#2763) is already implemented; and the config reliability improvements (#2771) address a common pain point. These may land in the next stable release.

## User Feedback Summary
Real pain points from the community:

- **Authentication breakage** – Users reporting valid keys returning 401 across providers (#2769) is frustrating and blocks usage.
- **Empty responses from ChatGPT Codex** – Power users relying on ChatGPT Plus subscription are seeing silent failures.
- **Gateway channel loss** – Docker users on v0.2.7/v0.2.8 find their bots unresponsive after upgrade.
- **Tool feedback unreadable** – HTML escaping of `&&`, `>` etc. in tool previews makes shell commands gibberish (fixed in #2670, now merged).
- **Model fallbacks don’t work** (#2334) – Already closed with a fix in #2336.
- **Positive sentiment** – Many users are contributing features (context compression, skill manager, FreeRide tool), indicating strong engagement and satisfaction with the project’s direction.

## Backlog Watch
Important items needing maintainer attention:

- **LM Studio Easy Connect** ([#28](https://github.com/sipeed/picoclaw/issues/28)) – Open since Feb, 17 comments, 2 👍. No PR yet. Popular request, especially for Android.
- **Cron/Channel bug** ([#1757](https://github.com/sipeed/picoclaw/issues/1757)) – Scheduled tasks fail with channel errors. Stale since March.
- **LongCat API tool not called** ([#2046](https://github.com/sipeed/picoclaw/issues/2046)) – Agent skips tool calls with this provider. Stale.
- **Serp API integration** ([#2232](https://github.com/sipeed/picoclaw/issues/2232)) – Open since March, 4 comments. Simple addition, low hanging fruit.
- **Search API fallback chain** ([#2582](https://github.com/sipeed/picoclaw/issues/2582)) – When rate-limited, no automatic fallback. Stale.
- **Security: sandbox bypass via `find`** ([#2688](https://github.com/sipeed/picoclaw/issues/2688)) – High severity, but no activity since creation.
- **Android service crash** ([#2590](https://github.com/sipeed/picoclaw/issues/2590)) – Prevents APK use entirely.
- **Session management commands PR** ([#2491](https://github.com/sipeed/picoclaw/pull/2491)) – Adds `/status`, `/compact`, `/new`. Open since April with no review.

These items, if addressed, could significantly improve PicoClaw’s stability, security, and user experience.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest — 2026-05-05

### 1. Today's Overview

NanoClaw shows **very high activity** with 35 pull requests touched in the past 24 hours (17 still open, 18 merged or closed) and 5 issues updated (4 open, 1 closed). No new releases are available, but the surge in merged PRs (18) indicates active bug‑fixing and feature landing, especially around channel adapters, container hardening, and setup improvements. The open issue count remains modest, suggesting the maintainers are keeping pace with community contributions. Key themes are **Discord card handling**, **WhatsApp LID migration**, **security hardening**, and **MCP tool reliability**.

### 2. Releases

*None. No new versions were published in this window.*

---

### 3. Project Progress — Merged / Closed PRs Today

18 PRs were merged or closed in the last 24 hours. Notable items:

- **#2256** (closed) – A guidelines‑compliant skill contribution (details not disclosed in summary).  
- **#2268** (merged) – **Setup simplification:** Removes the disk‑space pre‑flight check (underreports on separate `/home`/`/var` mounts); keeps the RAM check unchanged. Updates warning copy and PostHog events.  
- **#2092** (merged) – **Split commit skill rewrite** – a complete rework of the Split commit utility skill.  
- **#2215** (merged) – **Wire Discord channels and fix webhook delivery** – a core fix for Discord channel integration.  
- **#2055** (merged) – **Fix PATH injection in setup:** Ensures `~/.local/bin` is in `PATH` so `register-claude-to...` is reachable after installation.  
- **#2258** (closed – duplicate) – Duplicate of the ffmpeg MCP tool PR (#2261), closed in favour of the open version.  
- **#2241** (closed issue) – Addressed a bug where `add_mcp_server` registrations were silently dropped due to SDK `allowedTools` filtering; now resolved.

---

### 4. Community Hot Topics

Most active issues and PRs (by number of updates, as comment counts were not populated):

- **Issue #2234 — [OPEN] Can this work with llama.cpp?**  
  [qwibitai/nanoclaw Issue #2234](qwibitai/nanoclaw Issue #2234)  
  User reports that NanoClaw fails to connect to `llama-server` with “Your assistant didn't reply in time,” though `llama.cpp` itself responds. The community need is **provider interoperability** — users want to run NanoClaw with local/self‑hosted LLM backends.

- **Issue #2264 — [OPEN] Bug: New installs ship Discord card duplication**  
  [qwibitai/nanoclaw Issue #2264](qwibitai/nanoclaw Issue #2264)  
  All channel‑install skills pin `@chat-adapter/*@4.26.0`, which unconditionally sets `payload.content` when posting cards, causing duplication on Discord. The companion fix PR #2266 bumps the adapter to `4.27.0`, which is already open and under review.

- **PR #1999 — [OPEN] [security] fix(container): reject symlinked host‑managed directories**  
  [qwibitai/nanoclaw PR #1999](qwibitai/nanoclaw PR #1999)  
  A long‑standing security PR (created 2026-04-25) that hardens the container filesystem boundary. It has not yet been merged, signalling a careful review process for security changes.

- **PR #2000 — [OPEN] [security] fix(webhook): cap request bodies before adapter dispatch**  
  [qwibitai/nanoclaw PR #2000](qwibitai/nanoclaw PR #2000)  
  Another security PR preventing memory exhaustion via oversized webhook payloads. Still open after 10 days, indicating a backlog of security‑related contributions awaiting maintainer attention.

---

### 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| **High** | #2257 — Corrupt `container.json` silently wiped on next container spawn | Per‑group container configuration (mounts, MCP servers, packages) is lost when `container.json` is corrupt. Silent data loss. | Not yet |
| **Medium** | #2264 — Discord card duplication on fresh installs | `@chat-adapter/discord@4.26.0` duplicates payload content. | Yes, PR #2266 bumps to 4.27.0 |
| **Medium** | #2263 — `send_card` MCP tool silent no‑op on every Chat SDK channel | Chat SDK bridge has no branch to handle card‑type messages. | Yes, PR #2265 adds support |
| **Low** | #2234 — Cannot connect to `llama.cpp` | Timeout on “reply in time” despite server logs showing response. Workaround unknown. | Not yet |

Two high‑priority security PRs (#1999, #2000) remain open for 10+ days; they address container filesystem boundary hardening and webhook body‑size limits — both important for production deployments.

---

### 6. Feature Requests & Roadmap Signals

- **Local LLM support (llama.cpp)** — Issue #2234 expresses strong demand for running NanoClaw with open‑source local models. This is a recurring theme across AI agent projects. A fix could unlock a broader user base.
- **Media transformation MCP tool** — PR #2261 (still open) proposes an ffmpeg/ffprobe MCP server skill. If merged, it would let agents transcode, thumbnail, and analyse media files directly — a useful skill for media‑oriented workflows.
- **Better Telegram setup UX** — PR #2249 improves the “Open Telegram” card with a mobile fallback. This suggests attention to headless/remote‑VM deployments, which may become a target use case.

**Predictions for next release:** The Discord card duplication fix (PR #2266), the Chat SDK card support (PR #2265), and the setup simplification (PR #2268) are all review‑ready and likely to be included in the next version.

---

### 7. User Feedback Summary

- **Pain point (llama.cpp):** Users are frustrated that NanoClaw does not work with local LLM backends despite them working with other tools like Claude Code. The error message “didn't reply in time” is unhelpful.
- **Pain point (setup):** The disk‑space pre‑flight check produced false warnings on common partition layouts, leading to unnecessary confusion. This is now removed (PR #2268).
- **Pain point (WhatsApp):** Multiple issues and PRs (#2259, #2260) address WhatsApp LID resolution failures and split sessions after the v2 rewrite. The upgrade of Baileys from v6 to v7 is a major fix.
- **Satisfaction indicator:** High PR volume (35 in 24h) and quick turnaround for several bugs (Discord card duplication, Chat SDK bridge) suggest that the community finds the project responsive and worth contributing to.

---

### 8. Backlog Watch

| Item | Type | Age (as of 2026-05-05) | Why It Matters |
|------|------|------------------------|----------------|
| **PR #1999** (security) | Container symlink rejection | 10 days | Blocks a potential host‑escape vector; needs maintainer decision |
| **PR #2000** (security) | Webhook body cap | 10 days | Prevents resource exhaustion on public webhooks; no maintainer review yet |
| **PR #2004** (security) | Trust only canonical channels remote | 10 days | Hardens channel installer trust boundary; also unreviewed |
| **Issue #2257** (high severity) | Corrupt container.json data loss | 1 day | Reported yesterday; no fix PR yet — urgent for users relying on container config |
| **Issue #2234** (llama.cpp) | Interoperability request | 2 days | Stalled; no apparent progress, may need systematic debugging |

These items indicate a **security review backlog** and a **high‑severity bug** (#2257) that has not yet attracted a fix. The maintainers may want to prioritise the three security PRs that share a common author (Hinotoi‑agent) and are now 10 days old.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-05

## 1. Today's Overview
The project saw moderate activity with 5 PRs updated in the last 24 hours, 1 new issue opened, and a new patch release **v2026.5.4** cut. The release includes support for Agent Skills RFC 0.2.0 and hardened web skill fetch logic, signalling ongoing alignment with the Agent Skills ecosystem. Two PRs were merged: a version bump for the release and a migration of CI workflows to `nullbuilder`. A hackathon contribution proposing a Data Governance Layer was opened, indicating growing community interest in data privacy and compliance. The single new issue highlights a user pain point around long‑running task visibility, which may influence upcoming UI/UX improvements.

## 2. Releases
**v2026.5.4** (released 2026-05-04/05) – [Release page](https://github.com/nullclaw/nullclaw/releases/tag/v2026.5.4)  
*What’s changed* (from changelog and merged PRs):
- v2026.4.17 changes by @DonPrus (PR [#830](https://github.com/nullclaw/nullclaw/pull/830))
- **Agent Skills RFC 0.2.0 support** and hardening of the web skill fetch (PR [#831](https://github.com/nullclaw/nullclaw/pull/831) by @manelsen)
- Additional `feat: add to …` (truncated in data – likely further additions)

No breaking changes or migration notes were mentioned. This is a mostly incremental patch with targeted improvements for skill interoperability and stability.

## 3. Project Progress (Merged/Closed PRs Today)
- **[Merged/Closed] PR #889** – *Move GitHub workflows to nullbuilder* (by @DonPrus)  
  Infrastructure change relocating CI/CD scripts to a dedicated repository.
- **[Closed] PR #888** – *v2026.5.4* (by @DonPrus) – Version bump for the new release.

**Open PRs that advanced discussion:**
- **#878** – Fix `thread.sleep` on POSIX using `nanosleep` (ongoing, no merge yet)
- **#887** – Fix build with Zig v0.16 for Windows/Linux
- **#885** – Hackathon: Data Governance Layer (draft)

## 4. Community Hot Topics
- **Issue #886** – [ENHANCEMENT] *option to show reasoning/thinking* (opened by @darklight9811)  
  [Link](https://github.com/nullclaw/nullclaw/issues/886) | 💬 0 comments | 👍 0  
  The user reports that long tasks (e.g., reading emails via Outlook MCP) show no output for 30+ minutes, making it impossible to know if the agent is stuck or working. The underlying need is for real‑time progress or “thought streaming” – a recurring ask in AI assistants.

No other issue or PR attracted comments or reactions in this 24‑hour window. The hackathon PR (#885) may generate discussion once maintainers review the draft.

## 5. Bugs & Stability
**No new bugs were filed today.**  
Two stability‑related PRs are under review:
- **PR #878** – POSIX `thread.sleep` now uses `nanosleep` to actually suspend the OS thread instead of a cooperative yield. This addresses a latent scheduling issue in managed environments.  
  [Link](https://github.com/nullclaw/nullclaw/pull/878)
- **PR #887** – Fixes build failures with Zig v0.16 on Windows and Linux, ensuring compatibility with the latest compiler.  
  [Link](https://github.com/nullclaw/nullclaw/pull/887)

Both are moderate severity – the first could affect performance and predictability of sleep intervals; the second blocks new users on Zig v0.16.

## 6. Feature Requests & Roadmap Signals
The most notable request is **Issue #886** (reasoning/thinking visibility). Given the strong UX impact and the fact that the project already supports Agent Skills RFC 0.2.0, a “show thoughts” mode could be a logical next feature. Expect it to be considered for v2026.5.x or v2026.6.

The **Data Governance Layer** proposal (PR #885) from a hackathon team adds access control and audit logging for personal data. While still a draft, its inclusion signals community desire for privacy‑first agent design. If accepted, it would likely appear in a future minor release after review and integration with existing skill pipelines.

## 7. User Feedback Summary
- **Pain point** (Issue #886): “No way to know what the agent is doing during long tasks – stuck or working?”  
  User @darklight9811 specifically mentions Outlook MCP email reading taking 30 minutes without terminal feedback. This reflects dissatisfaction with the current black‑box execution model, especially for I/O‑heavy or agentic loops.

No other user feedback was captured in this window. Overall sentiment seems neutral with a clear pain point around observability.

## 8. Backlog Watch
No issues or PRs are critically stale. However, these items merit maintainer attention:
- **PR #878** (nanosleep fix) – open since April 30, last updated May 5. Requires review and testing before merge.
- **PR #887** (Zig v0.16 build fix) – open since May 4, no comments from maintainers. Could block new contributors using the latest Zig.
- **PR #885** (Data Governance Layer) – draft submitted for hackathon; lacks maintainer feedback.

No long‑unanswered issues were identified in the 24‑hour data window.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-05

## Today's Overview
Activity remains high, with 28 pull requests updated in the last 24 hours, of which 12 were closed or merged. The majority of merged work advances the **Reborn** substrate — a major architectural overhaul — while a single open issue (#3090) reflects continued refinement of the capability/tool surface layer. Dependabot continues to keep dependencies current across three separate update PRs. The project shows strong forward momentum with no regressions or critical bugs reported today.

## Releases
No new releases were published.

## Project Progress (Merged/Closed PRs Today)
- **#3230** — ***feat:(reborn) land Reborn substrate into main behind default‑off gates*** (core contributor)  
  Landed the Reborn substrate from a long‑lived branch, enabling CI validation while keeping Reborn opt‑in.
- **#3245** — ***fix(routines): normalize notification summaries with truncation and metadata*** (core contributor)  
  Clean recreation of #1470: capitalizes status labels, truncates summaries to 500 chars, adds `job_id` to metadata. The original diverged branch (#1470) was also closed.
- **#3244** — ***Demo/abound fix missions 4*** (core contributor)  
  Makes missions configurable for admin users and sends notifications to the same thread.
- **#3181–#3185** — ***Reborn memory stack (PRs 2–6 of #3118)*** (core contributor)  
  A 6‑PR stack collapsed into the still‑open #3180. Today PRs 2–6 were merged into that branch, adding native schema, libSQL/Postgres repository implementations, and vertical integration tests for the Reborn memory substrate.

Additionally, three Dependabot PRs (#2971, #2972, #2973) were updated (rebasing) but remain open.

## Community Hot Topics
- **#3090** (*open*) — **[Reborn] Add ToolSurfaceService and CapabilityCatalog**  
  The only issue updated today, with 3 comments. Proposes a host‑owned service that computes the model‑visible tool surface without granting authority. Underlying need: decouple tool visibility from execution authorization in the Reborn architecture.
- **#1764** (*open*) — **Abound demo — Responses API, credential injection, skills, guardrails**  
  A long‑running feature PR (open since March 30) with wide scope; last updated today. Reflects ongoing integration work with the Abound platform, a key use‑case demo.
- **#3246** (*open*) — **fix(installer): add Linux/macOS platform support and fix release tag URL**  
  A new contributor PR adding platform support. Shows community engagement and infrastructure enhancements.

## Bugs & Stability
No new bugs, crashes, or regressions were reported. The only stability‑related work closed today was the notification summary fix (#3245), which addresses a user‑visible formatting issue. The open PR **#2341** (*fix(tools): bound file history memory…*) remains under review, targeting memory‑related stability improvements.

## Feature Requests & Roadmap Signals
The overwhelming signal is the **Reborn architectural refactor**:
- **#3099** (open) — Reborn transport adapter contract  
- **#3171** (open) — Reborn event store backends (JSONL, PostgreSQL, libSQL)  
- **#3212** (open) — Reborn event projection service  
- **#3243** (open) — Runtime policy vocabulary (first of an 8‑PR stack for #3045)  
- **#3180** (open) — Collapsed Reborn memory substrate (native‑isolated guardrails, module split)

These PRs collectively implement a micro‑services‑style runtime with durable event logs, separate projection services, policy vocabularies, and memory backends. Expect the next release to ship Reborn behind feature gates, likely starting with tool‑surface and event‑store components.

## User Feedback Summary
No explicit user feedback was captured in today’s data. The only user‑facing change (notification formatting in #3245) was driven by prior feedback. The installer fix (#3246) addresses a community pain point around platform support and release tagging. Overall, the project appears to be in a phase of heavy internal restructuring rather than surfacing new user requests.

## Backlog Watch
- **#1764** (*open since 2026-03-30*) — Abound demo PR remains large and high‑risk; continued activity suggests it is actively maintained but not yet ready to merge.
- **#2341** (*open since 2026-04-11*) — File history memory fix awaits review; while not critical, it addresses a potential resource exhaustion issue.
- **#3090** (*the only open issue*) is only a week old — no long‑unanswered items require immediate maintainer attention.

No dormant issues or PRs with unanswered maintainer responses were identified.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-05-05

## 1. Today's Overview
Activity was moderate with **2 pull requests merged** and **1 issue closed** in the last 24 hours. No new releases were published. The project continues to mature with incremental improvements to skill management and documentation, while a long-standing crash fix remains open and stale. Community interaction was limited, with most attention on a recently closed regional authentication issue. Overall project health appears stable, though some important maintenance tasks (dependabot update, critical stability fix) are awaiting review.

## 2. Releases
No new releases.

## 3. Project Progress
Two pull requests were merged today:

- **PR #1882** `[area: docs, area: skills] feat(skill): upgrade youdaonote skill to 1.0.8`  
  Merged by liuzhq1986. Upgrades the built-in YoudaoNote skill to version 1.0.8, likely bringing new features or compatibility improvements.  
  [GitHub Link](https://github.com/netease-youdao/LobsterAI/pull/1882)

- **PR #1881** `[area: renderer, area: docs, area: main, area: skills] fix(skills): improve Windows skill delete reliability and import feedback`  
  Merged by liuzhq1986. Adds a best-effort attribute normalization step (`attrib -r -s -h`) on Windows after skill installation to reduce later delete failures. Also strengthens permission diagnostics (EPERM/EACCES/EBUSY) with localized success messages for the skill import flow.  
  [GitHub Link](https://github.com/netease-youdao/LobsterAI/pull/1881)

Both PRs contribute to the stability and user experience of the skill system, especially on Windows.

## 4. Community Hot Topics
The only project item with more than zero comments is:

- **Issue #1877** `[CLOSED] openAI 认证不成功,本地的codex是可以正常使用的`  
  **Author:** AK-blank | **Created:** 2026-04-29 | **Updated:** 2026-05-04 | **Comments:** 2  
  User reports an OpenAI sign-in failure with HTTP 403 and message "Country, region, or territory not supported." The issue was closed, suggesting either a resolution or a decision to mark as unsupported. The underlying need is for regional compatibility or clearer error messaging.  
  [GitHub Link](https://github.com/netease-youdao/LobsterAI/issues/1877)

No other issues or PRs received reactions or high comment counts in the observation period.

## 5. Bugs & Stability
No new bugs were reported today. The most significant stability concern remains:

- **PR #808** `[OPEN][stale] fix(api): prevent main process crash when renderer is destroyed during streaming`  
  **Author:** BucleLiu | **Created:** 2026-03-25 | **Updated:** 2026-05-05 | **Status:** Open, stale  
  This fix addresses a high-severity crash: if the user closes the window while an AI streaming response is in progress, the Electron main process crashes and all unsaved session data is lost. Despite being open for over a month, the PR has not been merged. Risk remains for users who frequently interrupt long responses.  
  [GitHub Link](https://github.com/netease-youdao/LobsterAI/pull/808)

No fix PRs were opened for new crash issues today.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests appeared in today’s activity. However, the merged PR #1882 (youdaonote skill upgrade) and PR #1881 (Windows skill reliability) indicate a continued focus on:

- **Skill ecosystem maturity** – improving installation, deletion, and feedback.
- **Platform-specific robustness** – Windows-specific workarounds for file permission issues.

The ongoing dependabot update (PR #1277) hints at a planned upgrade to Electron 41.5.0 (from 40.2.1), which could bring security patches and new API capabilities. This is likely to be included in the next release after review.

## 7. User Feedback Summary
- **Regional limitation frustration** (Issue #1877): A user cannot authenticate with OpenAI due to a geographic restriction, while their local Codex client works. This points to a need for better proxy/region handling or clearer error guidance.
- **Data loss risk** (PR #808): Users losing session content when closing windows during streaming is a clear pain point, though no new reports were filed today.
- **Windows skill management** (PR #1881): The merged fix addresses previous failures to delete skills on Windows, which likely caused user confusion or leftover files.

Overall, user satisfaction appears mixed – core functionality works, but edge cases (regional blocks, crashes under specific conditions) cause dissatisfaction.

## 8. Backlog Watch
Two long-stale items require maintainer attention:

- **PR #808** – *fix(api): prevent main process crash when renderer is destroyed during streaming*  
  Open since 2026-03-25, labeled stale. A critical crash fix that has been waiting for review for over a month. High priority.  
  [GitHub Link](https://github.com/netease-youdao/LobsterAI/pull/808)

- **PR #1277** – *chore(deps-dev): bump the electron group across 1 directory with 2 updates*  
  Open since 2026-04-02, updated 2026-05-04. Dependabot PR updating Electron from 40.2.1 to 41.5.0 and electron-builder. A routine dependency bump that should be merged after CI passes to avoid accumulating technical debt.  
  [GitHub Link](https://github.com/netease-youdao/LobsterAI/pull/1277)

No unresolved issues older than a month without response were identified.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-05

## 1. Today’s Overview
Moltis saw low activity over the past 24 hours, with only one open issue and one closed pull request. No new releases were published. The single new issue reports a critical bug where parallel tool execution causes Docker name sandbox collisions, pointing to a race condition in the sandbox lifecycle management. The lone PR, while merged, is a debugging enhancement for CI flakiness rather than a feature or direct fix. Overall, project maintainers appear focused on stabilising CI and addressing a high-severity sandboxing defect.

## 2. Releases
No new releases were recorded for the period. Users are advised to continue using the latest available release until further notice.

## 3. Project Progress
One pull request was merged/closed:

- **[#965 – debug(e2e): add RPC logging + gateway.log capture for CI diagnosis](https://github.com/moltis-org/moltis/pull/965)**  
  *Author: penso*  
  This PR adds verbose WebSocket RPC logging (method, timing, success/failure), connection closure warnings, and captures gateway stderr to a log artifact in CI. It also records timing warnings for lock acquisitions and RPC dispatches exceeding 50 ms. The change is diagnostic-only; it does not fix the underlying CI timeout issue but aims to help root-cause it.

While not a direct feature advancement, improved observability in CI is a necessary step toward resolving flaky tests and may accelerate future bug fixes.

## 4. Community Hot Topics
The only active discussion revolves around:

- **[#964 – [Bug]: Parallel tool execution results in docker name sandbox collisions](https://github.com/moltis-org/moltis/issues/964)**  
  *Author: faevourite*  
  This bug report describes a race condition where concurrent tool calls generate identical Docker sandbox names, leading to container name conflicts and execution failures. The issue has zero comments so far, but its potential impact on users running multi-agent or parallel-workspace workloads is high. The underlying need is for thread-safe or unique naming of ephemeral sandboxes, likely requiring either a UUID-based naming scheme or a centralised name allocation lock.

No other issues or PRs received significant community engagement within the window.

## 5. Bugs & Stability
One new bug was reported:

- **Issue #964 – Docker name sandbox collisions (Severity: High)**  
  *Impact:* Parallel tool execution fails intermittently due to duplicate container names. This can break workflows that rely on concurrent sandboxed tool calls (e.g., code execution, shell commands).  
  *Status:* Open, no fix PR linked yet.  
  *Risk level:* High – may block users leveraging multi-turn or multi-agent execution.  
  *Mitigation:* As a temporary workaround, users could serialise tool calls or use separate agent instances. A proper fix would likely involve adding a unique suffix (e.g., timestamp + random) to Docker container names.

No regressions, crashes, or other stability issues were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed or discussed in the last 24 hours. However, the Docker collision bug (issue #964) implicitly signals a need for **concurrency-safe sandbox orchestration**, which may drive architectural changes in the sandbox manager. Additionally, the CI diagnostic PR (#965) hints that **reliable end-to-end testing** is a current priority for the maintainers.

Predictions for next minor release:
- A hotfix for Docker name collisions (likely a UUID-based naming scheme).
- Further CI reliability improvements (timeout handling, logging).

## 7. User Feedback Summary
The only direct user feedback comes from issue #964, where the reporter followed the preflight checklist and used the latest version. They experienced a clear, reproducible pain point (parallel execution failure) indicating that production-scale or concurrent usage is being tested. No expressions of overall satisfaction or dissatisfaction were recorded.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified in the data provided. The single open issue (#964) was created on 2026-05-04 and is already receiving tracker attention (though no response yet). Maintainers should prioritise this bug given its high severity and potential to affect advanced workflows.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-05-05

## 1. Today's Overview

CoPaw saw moderate activity over the past 24 hours, with **13 issues** and **12 PRs** updated. Four PRs were merged/closed and two issues were resolved, indicating steady progress toward stability and feature delivery. The community is actively contributing first-time-contributor PRs (5 of the 12 open PRs), while user-reported bugs around streaming models, MCP timeouts, and session interruption remain the top stability concerns. No new release was published today; the project appears to be in a consolidation phase after the recent v1.1.x series.

## 2. Releases

**None** – no new releases were tagged in the last 24 hours.

## 3. Project Progress

Four pull requests were closed/merged today:

- **#3829** *(merged)* – **feat(chat): generate session titles asynchronously via LLM**  
  Replaces the awkward “first 10 characters” placeholder with a real model-generated title in the console session drawer. The PR also adds a fallback mechanism to keep the UI responsive.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/3829)

- **#1508** *(merged)* – **fix(provider): add full dependencies to Docker image**  
  Ensures the Docker image installs all required extras (including 7 previously undeclared third-party packages).  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/1508)

- **#763** *(merged)* – **fix(imessage): surface channel errors to Console UI and CLI**  
  Prevents silent crashes on iMessage channel and adds a `last_error` attribute for all channels, with visual error indicators in the console.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/763)

- **#756** *(merged)* – **fix(providers): use max_completion_tokens for OpenAI connection test**  
  Fixes connection test failures for GPT‑5 and o‑series models by adopting the correct parameter.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/756)

Two issues were also closed:

- **#2553** – Feature request to optimise model list ordering and session title generation (addressed by PR #3829).  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/2553)

- **#1798** – Enhancement request for Discord multi-channel parallel task processing.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/1798)

## 4. Community Hot Topics

The most active discussions (by comment count) reflect a mix of stability concerns and feature requests:

- **#4023** (3 comments) – *Input box severe lag* – user reports high input latency; no root cause identified yet.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/4023)

- **#3988** (3 comments) – *conda‑pack conflict with pip install on Windows* – a packaging bug that blocks Windows distribution.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/3988)

- **#4017** (2 comments) – *HEARTBEAT.md prevents automatic reconnection after network interruption* – a regression in v1.1.5.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/4017)

- **#4027** (2 comments) – *Session interruption intermittently fails; Python interpreter misses project venv* – user includes a fix PR (#4028).  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/4027)

The underlying need across these topics is **reliability under real-world conditions** – network drops, packaging tooling, and session control all point to production-readiness gaps.

## 5. Bugs & Stability

Several bugs were reported or updated today, ranked by potential impact:

| Severity | ID | Title | Summary | Fix PR? |
|----------|----|-------|---------|---------|
| **Critical** | #4034 | Streaming models cause ReAct loop to repeat tool calls | MiMo‑V2.5 / DeepSeek‑V4‑Pro trigger duplicate tool calls and duplicated output text. Not engine/channel layer; likely streaming parsing bug. | None yet |
| **High** | #4033 | MCP tool timeout hard‑coded to 30 s | `execution_timeout` ignored; always uses `HttpStatefulClient.timeout`. | None yet |
| **High** | #4027 | Session interrupt unreliable; Python interpreter not using project venv | Two bugs. A fix PR (#4028) has been submitted. | #4028 (open) |
| **Medium** | #4017 | HEARTBEAT.md prevents reconnection after network restore | Regression in v1.1.5. | None |
| **Medium** | #3988 | conda‑pack conflicts with pip install on Windows | Blocks Windows packaging. | None |
| **Low** | #4023 | Input box extreme lag | Performance issue, unclear root cause. | None |

Additionally, #4026 (PR) adds a safety guard to prevent `write_file` from silently overwriting non‑empty files – addressing a security‑adjacent bug. #4038 (PR) fixes an unauthenticated HTTP gateway by refusing non‑loopback bind unless auth is enabled (closes #4037).

## 6. Feature Requests & Roadmap Signals

Several feature requests were opened today, indicating user demand for deeper integration and flexibility:

- **#4037** – *Tool‑enabled HTTP gateway should require auth by default* – Now addressed by PR #4038 (open).  
- **#4036** – *Too many steps to add a new model* – Users want a streamlined wizard.  
- **#4031** – *Multi‑agent context loss and polling blockage* – Sub‑agents not sharing sessions cause lost context and forced manual polling.  
- **#4030** – *Add Vertex AI Gemini provider* – Enterprise users need Google Cloud IAM and regional routing.  
- **#4029** – *One‑shot cron jobs via `--at`* – Datetime‑based scheduling for reminders.

**Likely candidates for next release:**  
- #4038 (HTTP auth hardening) is already a PR and likely to be merged soon.  
- The `--at` cron feature (#4029) is a small, well‑defined extension.  
- The model adding UX (#4036) may be addressed in a future UX sprint.

## 7. User Feedback Summary

Real user pain points surfaced today:

- **Steep learning curve for model setup** – “Too many clicks back and forth” (#4036).  
- **Unreliable session control** – “Interrupt generation may not work” (#4027).  
- **Network resilience gaps** – HEARTBEAT.md causes permanent disconnection on network restore (#4017).  
- **Context loss in multi‑agent flows** – agent collaboration without shared session context (#4031).  
- **MCP tool timeouts** – hard‑coded 30‑s limit forces unnatural workarounds (#4033).  
- **Input performance** – Severe lag on some systems (#4023).  

Satisfaction drivers: contributions from first‑time contributors (5 open PRs) and the quick acceptance of async session titles (PR #3829) show that the community values responsive UX improvements.

## 8. Backlog Watch

The following issues and PRs have remained open for an extended period or require maintainer attention:

- **#3117** (PR, opened Apr 8, updated May 5) – *Semantic skill routing* – a relatively large feature that adds embedding‑based skill selection. Still under review; may need design alignment.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/3117)

- **#3729** (PR, opened Apr 23, updated May 4) – *Fix Windows taskbar icon using Win32 API* – a WIP, likely needs testing on multiple Windows versions.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/pull/3729)

- **#3988** (Issue, opened Apr 30) – *conda‑pack conflict on Windows* – no fix PR yet; affects Windows packaging pipeline.  
  [GitHub](https://github.com/agentscope-ai/QwenPaw/issues/3988)

- **#4033** (Issue, opened May 4) – *MCP timeout hard‑coded* – a simple parameter binding issue that could be fixed quickly; no assignee yet.

- **#1798** (Closed today) – *Discord multi‑channel parallel tasks* – closed without a visible merging of code. May still need a concrete implementation.

**Maintainer attention is most needed on the critical streaming model bug (#4034) and the MCP timeout issue (#4033), as both directly impact core agent functionality for popular models.**

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-05

## 1. Today's Overview
ZeptoClaw saw no issue activity and no merged pull requests in the last 24 hours, indicating a quiet day for the project. Eleven pull requests were opened—all automated dependency bumps by Dependabot—covering Rust (rustyline, rustls, libc, axum, tokio), JavaScript (globals, astro, @astrojs/starlight), and GitHub Actions. No human-committed changes or bug reports were introduced, suggesting the project is in a steady maintenance phase. Overall project health appears stable, though attention is needed to review and merge the pending dependency updates.

## 2. Releases
*No new releases were published today.*

## 3. Project Progress
- **Merged/Closed PRs**: 0  
  No feature work, bug fixes, or documentation improvements landed today.  
- **Open PRs (all by Dependabot)**:  
  - [PR #582](https://github.com/qhkm/zeptoclaw/pull/582) — chore(deps-dev): bump globals 17.3.0 → 17.5.0 in `/panel`  
  - [PR #581](https://github.com/qhkm/zeptoclaw/pull/581) — chore(deps): bump rustyline 17.0.2 → 18.0.0  
  - [PR #580](https://github.com/qhkm/zeptoclaw/pull/580) — chore(deps): bump @astrojs/starlight 0.38.3 → 0.38.4 in landing docs  
  - [PR #579](https://github.com/qhkm/zeptoclaw/pull/579) — chore(deps): bump rustls 0.23.37 → 0.23.39  
  - [PR #578](https://github.com/qhkm/zeptoclaw/pull/578) — chore(deps): bump astro 6.1.6 → 6.1.9 in landing docs  
  - [PR #577](https://github.com/qhkm/zeptoclaw/pull/577) — chore(deps): bump libc 0.2.185 → 0.2.186  
  - [PR #576](https://github.com/qhkm/zeptoclaw/pull/576) — chore(deps): bump astro 6.1.6 → 6.1.9 in `/landing/r8r/docs`  
  - [PR #575](https://github.com/qhkm/zeptoclaw/pull/575) — chore(deps): bump axum 0.8.8 → 0.8.9  
  - [PR #574](https://github.com/qhkm/zeptoclaw/pull/574) — chore(deps): bump taiki-e/install-action 2.75.17 → 2.75.22  
  - [PR #573](https://github.com/qhkm/zeptoclaw/pull/573) — chore(deps): bump tokio 1.51.1 → 1.52.1  
  - [PR #572](https://github.com/qhkm/zeptoclaw/pull/572) — chore(deps): bump @astrojs/starlight 0.38.3 → 0.38.4 in `/landing/r8r/docs`

## 4. Community Hot Topics
No issues or pull requests generated comments or reactions today. The project’s community engagement was effectively zero, likely because all recent activity is automated dependency updates. This may signal a need for maintainers to proactively solicit feedback or highlight roadmap items to re‑energize discussion.

## 5. Bugs & Stability
No bug reports, crashes, or regressions were filed in the last 24 hours. The absence of such reports suggests the current version(s) are stable, though the lack of testing or CI changes in today’s PRs could mask latent issues.

## 6. Feature Requests & Roadmap Signals
No feature requests were submitted today. The only signals come from the dependency update patterns: Rust dependency upgrades (rustyline 18.0.0, tokio 1.52.1) and Astro ecosystem bumps (astro 6.1.9, starlight 0.38.4) indicate the project is keeping up with ecosystem evolution, but no new feature directions are visible.

## 7. User Feedback Summary
No user feedback was captured in issues or PR comments today. The project’s user base appears inactive in public channels.

## 8. Backlog Watch
No issues or PRs are tagged as needing maintainer attention in the sense of long‑unanswered questions. However, the 11 open Dependabot PRs have not been reviewed or merged; they require maintainer action to keep dependencies current and avoid security or compatibility drift. Priority should be given to the Rust core dependencies (`rustyline`, `tokio`, `rustls`, `axum`) as they directly affect the agent’s runtime.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-05

## 1. Today’s Overview

The ZeroClaw project remains highly active, with **50 issues** and **50 pull requests** updated in the last 24 hours. Of these, **13 issues were closed** and **21 PRs were merged or closed**, indicating strong forward momentum. No new releases were published today, but the repository is approaching several milestone closures (v0.7.5 and v0.7.6) and shows a healthy balance of bug fixes, feature work, and community-driven enhancements. Developer velocity is high, though several critical bugs (S0/S1) remain open and require maintainer attention.

## 2. Releases

**No new releases today.** The latest tagged version remains v0.6.9. Milestone tracking for v0.7.5 ([#5878](https://github.com/zeroclaw-labs/zeroclaw/issues/5878)) continues, with the release pipeline moving toward full automation.

## 3. Project Progress

Several important bug fixes and features were merged or closed today:

- **Dashboard & web UI** – Bug #5959 (web dashboard unavailable in Docker) closed; fix via proper `web/dist` copy. PR #6179 merged, introducing per-property CRUD endpoints for web onboarding parity. PR #6392 (nodes dashboard) opened.
- **Jira integration** – Issue #5613 closed: auth failure for Jira Server (PAT) resolved (email field corrupting bearer string).
- **Nextcloud Talk** – Issue #5837 (cancellation support for ACP sessions) closed. PR #6048 continues work on draft-update streaming.
- **Anthropic provider** – PR #6314 merged: `base_url` config now respected for default Anthropic provider.
- **Docker build** – Issue #6304 closed: missing `tools/fill-translations` in COPY fixed.
- **Encryption / config** – Issue #6205 (silent `enc2` decryption failure) closed with diagnostics.
- **Onboarding** – Issues #6206 (custom OpenAI endpoint mislabel) and #6364 (duplicate) closed.
- **Documentation** – PR #6232 (philosophy.md links) merged; PR #6382 (reconcile channel docs against schema) opened.
- **CI** – PR #6396 opened to enforce PR title format.
- **Skills** – Issue #6210 (SkillForge auto-integrator emitting non-schema fields) being tracked; fix in progress.

## 4. Community Hot Topics

The most discussed issues and PRs reflect both critical blockers and desired improvements:

| Item | Comments | Description | Link |
|------|----------|-------------|------|
| #6123 | 16 | Fresh install `default_model` issue on LXC / Ollama remote – workflow blocked. | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6123) |
| #5878 | 6 | v0.7.5 release milestone tracking – high interest in automation and scope. | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5878) |
| #6153 | 6 | Matrix voice transcription fails with "Unsupported audio format '.'" on Element. | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6153) |
| #5415 | 5 | **S0 severity**: context spillage from chat to scheduled tasks – data leak / security risk. | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5415) |
| #6378 | 3 | Request for `allowed_channels` in Discord config (like Matrix). | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) |
| #6394 | 3 | Feature request for automatic PR title format check (now implemented in #6396). | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6394) |
| #6391 | 2 | Real heartbeat tracking for daemon nodes (Online/Stale/Offline). | [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6391) |

The underlying needs are clear: smoother onboarding, better cross-platform channel support (Matrix, Nextcloud, Discord), and stronger security guarantees (context isolation, air-gapped execution).

## 5. Bugs & Stability

**High-severity bugs reported or still active today (ranked by priority):**

- **[S0 – data loss / security]** #5415 – Context spillage from chat to scheduled execution. **No fix PR yet.** Status: blocked, waiting for reproduction steps.
- **[S1 – workflow blocked]** #6123 – `default_model` not found on fresh install (Ollama on separate LXC). No fix PR observed.
- **[S1 – workflow blocked]** #6180 – Cannot use llama-server services (`All providers/models failed`). Needs repro steps.
- **[S1 – workflow blocked]** #6206 *(closed today)* – Onboarding fails with “Unknown property” for custom OpenAI-compatible endpoint.
- **[S1 – workflow blocked]** #6304 *(closed today)* – Docker build failure due to missing workspace member.
- **[S2 – degraded]** #6153 – Matrix voice transcription fails (audio format '.'). Needs repro.
- **[S2 – degraded]** #6173 – `model_switch` tool does not persist across turns; gateway ignores it. Accepted, in progress.
- **[S2 – degraded]** #6360 – Prompt caching broken on Telegram (forces re-processing).
- **[S2 – degraded]** #6156 – Nextcloud Talk model request canceled after ~5 seconds.
- **[S2 – degraded]** #6157 – Nextcloud Talk wrong bot message API used.

Several of these have fix PRs in flight (e.g., #6156, #6157, #6360 are open bugs without linked PRs yet). The closure of #5959 and #6304 improves overall stability.

## 6. Feature Requests & Roadmap Signals

The following enhancement requests indicate strong community interest in:

- **Discord channel scoping** – #6378: `allowed_channels` config (consistent with Matrix). Likely candidate for next minor release.
- **PR title enforcement** – #6394 (now implemented in #6396): CI improvement.
- **Daemon heartbeat tracking** – #6391: real health signals for fleet dashboard.
- **Air-gapped execution** – #6293 (RFC): split process with unix socket for offline LLM + internet proxy. This architectural change could be high impact but requires maintainer review.
- **Lighter ZeroClaw** – #6165: remove dedicated integrations (e.g., Jira, GitHub) in favor of skill-based tools.
- **HMAC tool receipts** – #6182: re-enable cryptographic receipts (wiring stripped before merge). Docs already describe as shipped.
- **Config dynamic map support** – #6053: `zeroclaw config set` for dynamic keys like `providers.models.<name>`. Accepted, no-stale.
- **Skills UX and support** – #6253: v0.7.6 tracker for skill authoring, CLI, sandbox, etc. Accepted, in progress.

Based on issue labels (`status:accepted`, `status:in-progress`), v0.7.6 will focus on skills, while v0.7.5 is already scoped. Features like #6378 and #6394 are low-risk and may land before the next release.

## 7. User Feedback Summary

User pain points highlight the following real-world scenarios:

- **Fresh install friction** – Multiple users (rgnyldz, tigran123) reported onboarding failures when using custom OpenAI-compatible endpoints or remote Ollama instances. The experience for first-time users is fragile.
- **Security concerns** – Context spillage (#5415) is a serious data exposure issue; user cites Discord chat context influencing scheduled tasks. No repro yet, but high attention.
- **Channel-specific problems** – Matrix voice transcription is broken with default clients (Element). Nextcloud Talk has both timeout and API issues. Telegram prompt caching fails, causing unnecessary latency.
- **Plugin / provider interoperability** – llama-server (#6180) and Groq (PR #5932) have compatibility problems. Users want per-model native tool support for Groq.
- **Administration** – Dashboards lacking real node health (#6391), version display (PR #6367), and tool approval flow (#6387) are gaps in production use.

On the positive side, the quick closures of #5959 (Docker dashboard) and #6304 (Docker build) were well received (👍 on #5959). The community appreciates rapid bug fixes.

## 8. Backlog Watch

Several important items require maintainer attention or have gone stale:

| Item | Type | Status | Reason |
|------|------|--------|--------|
| [#5415](https://github.com/zeroclaw-labs/zeroclaw/issues/5415) | Bug (S0) | Blocked, no-stale | Context spillage – awaiting repro steps from reporter. |
| [#6180](https://github.com/zeroclaw-labs/zeroclaw/issues/6180) | Bug (S1) | Needs repro | Cannot use llama-server – no reproduction steps provided. |
| [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293) | Enhancement (RFC) | Needs maintainer review | Air-gapped execution mode – architectural impact high. |
| [#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) | Enhancement | Needs maintainer review | Remove dedicated tool code in favor of skills – significant refactor. |
| [#6192](https://github.com/zeroclaw-labs/zeroclaw/pull/6192) | PR | Needs author action | Gateway paircode retrieval – awaiting author updates. |
| [#6048](https://github.com/zeroclaw-labs/zeroclaw/pull/6048) | PR | Needs author action | Nextcloud Talk draft-update streaming – follow-up action requested. |

The project maintainers have been responsive overall, but the backlog of items needing reviewer input (especially RFCs and large refactors) could slow roadmap progress if not addressed soon.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*