# OpenClaw Ecosystem Digest 2026-05-04

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-04 08:44 UTC

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

# OpenClaw Project Digest — 2026-05-04

## 1. Today's Overview

The project is in an intense burst of activity: **500 issues** and **500 PRs** were updated in the last 24 hours. Of those issues, 278 are open/active and 222 have been closed, while PRs show 409 open and 91 merged/closed. Three new releases (including stable `v2026.5.3`) shipped, centered on a bundled file-transfer plugin. The community is actively reporting regressions in performance and stability, but a high volume of fix PRs indicates maintainers are responding quickly. Overall project health is high, with both feature work and bugfixing proceeding in parallel.

## 2. Releases

Three releases were published today:

- **v2026.5.3** (stable)
- **v2026.5.3-beta.3**
- **v2026.5.3-beta.2**

All share the same major highlight:

- **Plugins/file-transfer**: A new bundled plugin providing `file_fetch`, `dir_list`, `dir_fetch`, and `file_write` agent tools for binary file operations between paired gateway nodes. It includes a default-deny per-node path policy under `plugins.entries.file-transfer.config.nodes` with operator approval and symlink protection.

*No breaking changes or migration notes were provided.* The plugin is opt-in via configuration.

## 3. Project Progress

In the last 24 hours, **91 PRs were merged or closed**. Notable advances from the top 30 PRs by comment count include:

- **Trajectory runtime fix** – PR [#77154](https://openclaw/openclaw/pull/77154) bounds runtime trajectory payload shaping and stops live capture once a write budget is reached.
- **Durable message lifecycle delivery** – PR [#77205](https://openclaw/openclaw/pull/77205) adds opt-in durable final reply delivery for Telegram (injection) and WhatsApp (text-only fallback), plus hardened plugin module loading.
- **APNs HTTP/2 proxy** – PR [#74905](https://openclaw/openclaw/pull/74905) routes direct APNs sessions through the active managed proxy with allowlisting and credential redaction.
- **Sessions list cache** – PR [#77187](https://openclaw/openclaw/pull/77187) fixes CPU‑burning `sessions.list` resolver by caching gateway session row builders (production profile showed 88.9s total for 1217 sessions).
- **Bounded filesystem operations** – PR [#73442](https://openclaw/openclaw/pull/73442) extends `fs-safe` with bounded stat, readdir, and rename helpers.
- **Scoped mention pattern policy** – PR [#70864](https://openclaw/openclaw/pull/70864) adds a global/agent/provider mention‑pattern gating system across 15+ channels.
- **Memory supplement preservation** – PRs [#77200](https://openclaw/openclaw/pull/77200) and [#77098](https://openclaw/openclaw/pull/77098) fix loss of `MemoryCorpusSupplement` during lazy plugin re-registration.
- **TUI abort gap** – PR [#77199](https://openclaw/openclaw/pull/77199) fixes Esc key during pre-event waiting gap not aborting the run.
- **Task registry quarantine** – PR [#77196](https://openclaw/openclaw/pull/77196) adds fallback for corrupt SQLite task store, preserving files in a `quarantine/` directory.
- **Azure Speech provider** – PR [#73456](https://openclaw/openclaw/pull/73456) adds Azure Speech as a realtime transcription provider for `voice-call`.
- **Cron agentId filtering** – PR [#77188](https://openclaw/openclaw/pull/77188) allows agents to filter cron jobs by agentId, reducing noise in multi‑agent setups.

## 4. Community Hot Topics

The most active discussions and highest‑reaction issues indicate strong community focus on **installation trouble, performance regressions, and missing UX features**.

| Issue | Title | Comments | Reactions | Summary of underlying need |
|-------|-------|----------|-----------|---------------------------|
| [#14593](https://openclaw/openclaw/issues/14593) | Skill install fails in Docker: `brew not installed` on Linux container | 29 | 17👍 | Docker image lacks brew; skill installation for Linux users is broken. Need a package manager fallback. |
| [#25592](https://openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | 24 | 0 | Internal processing text (errors, acknowledgments) appears as visible messages – UX regression. Need output filtering. |
| [#32473](https://openclaw/openclaw/issues/32473) | Control UI requires device identity (use HTTPS or localhost secure context) | 15 | 4👍 | VPS/Docker users unable to use control UI without HTTPS – need secure context workaround or documentation. |
| [#22676](https://openclaw/openclaw/issues/22676) | Signal daemon stop() race condition on SIGUSR1 restart | 15 | 0 | Orphaned processes and send failures during config restart – need proper process lifecycle management. |
| [#73501](https://openclaw/openclaw/issues/73501) | BLOCKER: 4.22 to 4.26 significantly slower | 14 | 5👍 | **Critical performance regression** – reactions/sends slowed drastically. |
| [#72808](https://openclaw/openclaw/issues/72808) | Silently lost connection to Slack | 13 | 2👍 | Slack disconnect without notification – need reconnection alerts or heartbeat health checks. |
| [#29387](https://openclaw/openclaw/issues/29387) | Bootstrap files in agentDir silently ignored | 13 | 4👍 | Per‑agent SOUL.md etc. not loaded – need consistent file injection from agentDir. |
| [#8081](https://openclaw/openclaw/issues/8081) | Feature Request: Multi‑user permission management with RBAC | 11 | 28👍 | **Highest‑voted feature** – families/teams need role‑based access control to protect API keys and configs. |
| [#73532](https://openclaw/openclaw/issues/73532) | Plugin loader hot loop: prepareBundledPluginRuntimeDistMirror + JSON5 parsing | 13 | 1👍 | Event loop starvation causing Telegram long‑poll timeouts – severe stability issue. |
| [#22358](https://openclaw/openclaw/issues/22358) | Post‑subagent completion extension hook | 11 | 0 | Need hook for automated trajectory generation after subagent finishes. |

## 5. Bugs & Stability

Several severe regressions and critical bugs were reported today. **Ranked by severity:**

| Severity | Issue | Title | Status | Notes |
|----------|-------|-------|--------|-------|
| 🔴 Blocker | [#73501](https://openclaw/openclaw/issues/73501) | OpenClaw 4.22 to 4.26 significantly slower | CLOSED | Performance regression in reactions/replies. Fix likely included in recent releases. |
| 🔴 Blocker | [#74328](https://openclaw/openclaw/issues/74328) | Gateway main thread CPU‑bound at ~100% (`fs.stat` storm) | CLOSED | Regression in v2026.4.26, fixed? (closed status). |
| 🔴 Critical | [#75330](https://openclaw/openclaw/issues/75330) | Gateway event loop blocked during agent prep (max delay 32s) | CLOSED | Massive blocking – API requests hang. Closed, likely patched. |
| 🔴 Critical | [#73428](https://openclaw/openclaw/issues/73428) | Severe chat latency (30–90s) on Docker VPS | CLOSED | Direct OpenAI <1s, OpenClaw adds huge overhead. Closed. |
| 🟠 High | [#73532](https://openclaw/openclaw/issues/73532) | Plugin loader hot loop saturates gateway | CLOSED | `prepareBundledPluginRuntimeDistMirror` + JSON5 parsing peg CPU. Closed. |
| 🟠 High | [#74953](https://openclaw/openclaw/issues/74953) | Both web and CLI super laggy since 4.23 | CLOSED | Increasing lag over versions – multiple user reports. Closed. |
| 🟠 High | [#76804](https://openclaw/openclaw/issues/76804) | WebChat assistant text not persisted to session transcript (5.2 regression) | CLOSED | Data loss for tool‑using turns. Closed with fix PR? |
| 🟠 High | [#75824](https://openclaw/openclaw/issues/75824) | Web UI chat bubbles then disappears; direct API works | CLOSED | No assistant response in Web UI. Closed. |
| 🟡 Medium | [#74497](https://openclaw/openclaw/issues/74497) | Telegram group chats not discovered/ingested | CLOSED | DMs work, groups don't – likely configuration issue. |
| 🟡 Medium | [#32296](https://openclaw/openclaw/issues/32296) | Agent replies to previous message (session context confusion) | OPEN | Still open – conversation misalignment persists. |
| 🟡 Medium | [#31583](https://openclaw/openclaw/issues/31583) | `exec` tool does not inherit `skills.entries.*.env` environment variables | OPEN | Regression – secrets can't be injected to subprocesses. |
| 🟡 Medium | [#38439](https://openclaw/openclaw/issues/38439) | Webchat avatar endpoint returns 404 | OPEN | Avatar broken in control UI. No fix PR visible. |
| 🟡 Medium | [#38327](https://openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" with google-vertex/gemini | OPEN | Regression in 2026.3.2. |

*Many critical bugs were closed, indicating successful patches in the latest releases.*

## 6. Feature Requests & Roadmap Signals

High‑demand features likely to influence upcoming versions:

- **Multi‑user permission management with RBAC** – [#8081](https://openclaw/openclaw/issues/8081) (28👍) – Most requested feature. Expect a security profile PR soon.
- **Direct Exec Mode for Cron Jobs** – [#18160](https://openclaw/openclaw/issues/18160) (9👍) – Avoid LLM interpretation for simple cron tasks; would reduce API costs and latency.
- **Hourly spending ceiling** – [#38248](https://openclaw/openclaw/issues/38248) (0👍 but closed) – Already implemented? (closed status).
- **Recursive `memory_search` subdirectory support** – [#34400](https://openclaw/openclaw/issues/34400) – Organize daily memory files into folders.
- **Write tool append mode** – [#40001](https://openclaw/openclaw/issues/40001) – Prevent data loss when multiple cron sessions write to same file.
- **Theme Customization System** – [#28300](https://openclaw/openclaw/issues/28300) (5👍) – Preset themes + custom studio for control UI.
- **Post‑subagent completion extension hook** – [#22358](https://openclaw/openclaw/issues/22358) – Enables structured trajectory generation.
- **Multi‑Agent Collaboration Enhancement (RFC)** – [#35203](https://openclaw/openclaw/issues/35203) – Capability profiling, shared blackboard, layered memory, token cost governance.

**Predictions for next release**: Permission management (following the new file‑transfer plugin's security model), cron direct mode, and memory recursion are likely near‑term additions based on reaction counts and existing PRs.

## 7. User Feedback Summary

- **Pain points**:
  - Docker users report `brew` dependency breaking skill installation (Issue [#14593](https://openclaw/openclaw/issues/14593)).
  - Performance on low‑resource VPS (2 vCPU/4GB) is 30–90s per turn (Issue [#73428](https://openclaw/openclaw/issues/73428)), despite fast model API – indicates OpenClaw overhead.
  - Silent Slack connection loss (Issue [#72808](https://openclaw/openclaw/issues/72808)) erodes trust.
  - Tool‑call internal text leaking to channels (Issue [#25592](https://openclaw/openclaw/issues/25592)) is a significant UX issue.
  - Per‑agent configuration (agentDir) is broken (Issue [#29387](https://openclaw/openclaw/issues/29387)).
  - Regression in avatar display (Issue [#38439](https://openclaw/openclaw/issues/38439)).
  - CLI/TUI experience: lag, abort confusion (Issues [#38501](https://openclaw/openclaw/issues/38501), [#74953](https://openclaw/openclaw/issues/74953)).

- **Satisfaction signals**:
  - New file‑transfer plugin directly addresses the requested `file_push`/`file_pull` feature from Issue [#41716](https://openclaw/openclaw/issues/41716) (closed, now released).
  - Many critical performance bugs were closed quickly, showing responsive maintenance.
  - High PR volume (91 merged/closed) indicates active development and release cadence.

## 8. Backlog Watch

Long‑unanswered issues requiring maintainer attention:

| Issue | Date Created | Last Updated | Comments | Notes |
|-------|-------------|--------------|----------|-------|
| [#14593](https://openclaw/openclaw/issues/14593) – Docker brew not installed | 2026-02-12 | 2026-05-04 | 29 | Top‑by‑comments; 17👍 – no maintainer response visible. |
| [#25592](https://openclaw/openclaw/issues/25592) – Text leaks to channels | 2026-02-24 | 2026-05-04 | 24 | UX breaking – no fix PR. |
| [#22676](https://openclaw/openclaw/issues/22676) – Signal daemon race | 2026-02-21 | 2026-05-04 | 15 | Orphaned processes – no resolution. |
| [#29387](https://openclaw/openclaw/issues/29387) – agentDir bootstrap ignored | 2026-02-28 | 2026-05-04 | 13 | Per‑agent configuration broken – no assignee. |
| [#22358](https://openclaw/openclaw/issues/22358) – Post‑subagent hook | 2026-02-21 | 2026-05-04 | 11 | Feature request with no milestone. |
| [#32296](https://openclaw/openclaw/issues/32296) – Session context confusion | 2026-03-02 | 2026-05-04 | 11 | Conversation misalignment – still open. |
| [#31583](https://openclaw/openclaw/issues/31583) – `exec` tool env inheritance | 2026-03-02 | 2026-05-04 | 11 | Regression – no PR linked. |
| [#38439](https://openclaw/openclaw/issues/38439) – Avatar 404 | 2026-03-07 | 2026-05-04 | 9 | UI regression – no fix. |
| [#38327](https://openclaw/openclaw/issues/38327) – Gemini "Cannot convert undefined or null" | 2026-03-06 | 2026-05-04 | 7 | Regression – still open. |
| [#40001](https://openclaw/openclaw/issues/40001) – Write tool append mode | 2026-03-08 | 2026-05-04 | 8 | Data loss risk – no PR. |

*The most urgent backlog item is the Docker brew issue (#14593), affecting many users and generating high frustration.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing intense, convergent development across multiple independent projects, all racing to deliver production-grade agent infrastructure. Activity levels are exceptionally high, with several projects processing 50-500 issues and PRs daily, while maintainers respond to user-reported regressions within hours. The ecosystem is fragmenting around three core architectural decisions: plugin vs. monolithic design, memory persistence strategies, and provider abstraction layers. Key cross-cutting concerns—performance overhead, security hardening, multi-user RBAC, and local LLM compatibility—are emerging as shared priorities that will define competitive differentiation in the coming quarters. The community is mature and vocal, with detailed bug reports and proactive feature proposals driving rapid iteration cycles.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release Today | Health Score |
|---------|---------------------|-------------------|-------------------|--------------|
| **OpenClaw** | 500 | 500 | ✅ v2026.5.3 (stable) | Excellent |
| **Hermes Agent** | 50 | 50 | ❌ | Very High |
| **NanoClaw** | 10 | 50 | ❌ | High |
| **ZeroClaw** | 50 | 50 | ❌ | High |
| **CoPaw** | 27 | 16 | ❌ | High |
| **IronClaw** | 20 | 18 | ❌ | Mixed/Good |
| **NanoBot** | 9 | 22 | ❌ | Good |
| **PicoClaw** | 4 | 29 | ❌ | Good |
| **NullClaw** | 2 | 2 | ❌ | Stable |
| **Moltis** | 1 | 2 | ❌ | Stable/Low Activity |
| **LobsterAI** | 1 | 1 | ❌ | Low Activity |
| **ZeptoClaw** | 0 | 1 (updated) | ❌ | Minimal |
| **TinyClaw** | 0 | 0 | ❌ | Inactive |

*Health Score reflects issue closure rate, bug severity, release cadence, and community engagement. See source digests for methodology.*

## 3. OpenClaw's Position

**Advantages vs. peers:**
OpenClaw is the undisputed scale leader, processing 10x more daily activity (500 issues/PRs) than the next most active projects. It is the only project to ship a stable release today (v2026.5.3), demonstrating mature release engineering. The new bundled file-transfer plugin with default-deny policy and symlink protection sets a security standard others are now emulating. Its 91 merged/closed PRs in a single day—including trajectory runtime fixes, APNs proxy support, and scoped mention patterns—confirm an exceptionally productive core team.

**Technical approach differences:**
OpenClaw employs a modular plugin architecture with opt-in security policies, contrasting with monolithic or bundle-all approaches seen in NanoBot and Moltis. Its gateway-node pairing model for file operations is unique and addresses a common security concern. The plugin loader hot loop bug (#73532) that saturated gateways indicates some architectural complexity, but fixes are deployed rapidly.

**Community size comparison:**
OpenClaw’s community is an order of magnitude larger than any peer: 500 issues and 500 PRs daily vs. 50 each for Hermes and ZeroClaw. The 28 👍 for its RBAC feature request (#8081) is the highest-voted feature across all projects. However, this scale also yields proportionally more bug reports—notably the Docker `brew` issue (#14593) with 29 comments and 17 👍, which remains a significant user frustration despite the project's overall health.

## 4. Shared Technical Focus Areas

Multiple projects are converging on the same infrastructure challenges:

| Focus Area | Affected Projects | Specific Needs |
|------------|------------------|----------------|
| **Memory Persistence & Context Reliability** | OpenClaw, Hermes, NanoClaw, IronClaw, CoPaw | MemoryCorpusSupplement preservation, session context confusion, viking_remember empty sessions, memory_search crashes |
| **Performance Overhead Reduction** | OpenClaw, ZeroClaw, CoPaw | 30-90s per-turn latency on VPS, CPU-bound fs.stat storms, input field lag, stream sanitization |
| **Security Hardening & RBAC** | OpenClaw, NanoBot, Hermes, CoPaw, ZeroClaw | Multi-user permission management, file write protection, SSRF guards, env_read allowlists, credential rotation |
| **MCP/Tool Ecosystem** | CoPaw, Hermes, PicoClaw | MCP retry on startup, per-request dynamic headers, import validation, degraded connection handling |
| **Provider Model Compatibility** | OpenClaw, ZeroClaw, PicoClaw, IronClaw | DeepSeek reasoning_content drops, Gemini tool_call ordering, empty tool_calls arrays, thought_signature handling |
| **Terminal/CLI UX** | OpenClaw, NanoBot, Hermes, IronClaw | TUI abort gaps, garbled ANSI output, terminal corruption after /quit, multi-line paste drops |
| **Docker/Container Deployment** | OpenClaw, CoPaw, IronClaw, ZeroClaw | ARM64 GLIBC incompatibility, brew dependency, port conflicts, HEARTBEAT.md deadlock |

## 5. Differentiation Analysis

**Feature Focus:**

| Project | Primary Differentiator | Target User |
|---------|----------------------|-------------|
| **OpenClaw** | Scale & ecosystem breadth; stable release cadence | Production deployments, power users |
| **Hermes Agent** | Rapid bugfix throughput; strong CLI/TUI focus | Developers, terminal-centric users |
| **NanoBot** | Stability & security hardening; small surface area | Conservative adopters, enterprise-adjacent |
| **ZeroClaw** | Desktop/macOS parity + schema migration leadership | Desktop users, Apple ecosystem |
| **CoPaw** | MCP ecosystem depth; Chinese community focus | MCP integrators, Asia-Pacific |
| **PicoClaw** | Lightweight, low-resource optimization | Embedded, edge devices |
| **IronClaw** | Reborn architecture overhaul (event-sourced) | Long-term scalability, high-throughput |
| **NullClaw** | Sandbox-first design (Landlock) | Security-conscious minimalists |
| **Moltis** | Local TTS integration; reasoning replay fidelity | Voice interaction enthusiasts |
| **LobsterAI** | Agent interoperability (Hermes/OpenClaw connector) | Multi-agent orchestration |

**Architecture Comparison:**
- *Plugin vs. Monolithic:* OpenClaw (plugin) vs. NanoBot (bundled) vs. Moltis (minimal). ZeroClaw is hybrid with WASM plugin support.
- *Memory Models:* OpenClaw uses MemoryCorpusSupplement; Hermes uses viking_remember; CoPaw uses Lore Context; IronClaw is building event-sourced persistence.
- *Provider Abstraction:* All projects aim for abstraction, but OpenClaw provides the most provider integrations (Azure Speech, APNs). ZeroClaw and ZeroClaw focus on strict provider validation.

## 6. Community Momentum & Maturity

**Tier 1 (Rapid Iteration, 50+ daily updates):** OpenClaw, Hermes, NanoClaw, ZeroClaw, CoPaw
- These projects are releasing multiple fixes per day, with low median bug resolution time.
- OpenClaw and ZeroClaw are preparing major releases (v2026.5.3, v0.8.0 schema migration).
- Hermes is in a stabilization push after v0.12.0, merging 46 PRs today.

**Tier 2 (Active, 10-40 daily updates):** NanoBot, PicoClaw, IronClaw
- NanoBot and PicoClaw are fixing regressions from recent releases.
- IronClaw is architecturally busy (Reborn overhaul) but user-facing progress is slower.

**Tier 3 (Low Activity, 1-5 daily updates):** NullClaw, Moltis, LobsterAI
- These projects are stable but not attracting new contributors or feature work.
- Moltis and NullClaw have responsive maintainers; LobsterAI appears to be in maintenance mode.

**Tier 4 (Stable/Sleeping):** ZeptoClaw, TinyClaw
- ZeptoClaw has one active PR; TinyClaw is completely inactive.

## 7. Trend Signals

**Extracted from community feedback across all projects:**

1. **Memory is the top frustration.** Every major project has unresolved memory persistence or recall bugs. Users report losing context, empty sessions, and `viking_remember` failures. This is the #1 blocker for building reliable long-running agents.

2. **Performance overhead is a systemic problem.** Multiple projects (OpenClaw, ZeroClaw, CoPaw) report 5-90x latency inflation over direct API calls. The community is demanding profiled benchmarks as a release requirement.

3. **Multi-user RBAC is the most requested missing feature.** OpenClaw’s #8081 (28👍), CoPaw’s agent isolation requests, and NanoClaw’s permission work all point to a clear market need for family/team deployments.

4. **Local LLM compatibility is breaking regularly.** ARM64 Docker images, macOS Rosetta subprocesses, Ollama credential gaps, and provider-specific validation errors (DeepSeek, Gemini) are recurring themes. Users want "it just works" for self-hosted models.

5. **MCP is becoming the universal tool protocol.** CoPaw, Hermes, and PicoClaw all invested heavily in MCP integration this week. Users expect MCP tools to work reliably with retry, timeout configuration, and degraded error handling.

6. **Security hardening is reactive, not proactive.** File write overwrites, SSRF, environment variable exposure, and credential pool rotation issues were all reported in the last 24 hours. The community is demanding default-deny policies and sandboxing.

7. **Desktop distribution is nascent.** ZeroClaw’s macOS notarization and auto-update pipeline represents the most advanced desktop effort. No project has a mature cross-platform desktop offering yet.

**Value for AI agent developers:** The ecosystem is converging on a standard stack: MCP tools + memory persistence + RBAC + performance benchmarking. Developers building on top of these projects should prioritize memory reliability and provider abstraction, as these are the most volatile and rapidly improving layers. The window for differentiation through performance optimization and security hardening is open but closing quickly.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Based on the provided GitHub data for NanoBot (github.com/HKUDS/nanobot), here is a project digest for 2026-05-04.

---

### NanoBot Project Digest – 2026-05-04

#### 1. Today's Overview
The NanoBot project is in a period of high activity, with a clear focus on stability, security hardening, and community bug-fixing. Over the last 24 hours, 22 pull requests and 9 issues have been updated, indicating robust development momentum. The number of closed PRs (10) and issues (4) demonstrates strong progress in resolving user-reported problems and integrating fixes. While no new releases were published today, the project's maintainers and community contributors are actively addressing a wide range of concerns, from core security vulnerabilities to user experience regressions like garbled CLI output and silent errors.

#### 2. Releases
**None.** No new releases were published in the last 24 hours. The latest version remains `v0.1.5.post3`. Development activity is concentrated on fixes and features that will likely be bundled in a future release.

#### 3. Project Progress
Ten pull requests were merged or closed today, marking significant progress in fixing bugs and enhancing functionality.

- **Critical Fixes:**
  - **DeepSeek V4 Reasoning:** PR [#3616](https://github.com/HKUDS/nanobot/pull/3616) was merged to fix the persistent `reasoning_content` error (closing issues [#3554](https://github.com/HKUDS/nanobot/issues/3554) and [#3584](https://github.com/HKUDS/nanobot/issues/3584)). The solution replaces a destructive history trim with a non-destructive backfill.
  - **WhatsApp Voice Messages:** PR [#3607](https://github.com/HKUDS/nanobot/pull/3607) was merged to fix a critical missing feature where WhatsApp voice messages were not downloaded, rendering them unusable.
  - **CLI Garbled Output:** PR [#3609](https://github.com/HKUDS/nanobot/pull/3609) was closed, fixing a bug that caused API retry messages to be mixed with normal output in the CLI, resulting in ANSI code garbage.
  - **Safety Guard False Positives:** PR [#3613](https://github.com/HKUDS/nanobot/pull/3613) was merged to fix false positives in the workspace safety guard, specifically exempting `/dev/*` paths from blocking.
  - **Provider Logout Command:** PR [#3612](https://github.com/HKUDS/nanobot/pull/3612) was merged, addressing the long-standing feature request to add a `nanobot provider logout` command (also closing similar PR [#2727](https://github.com/HKUDS/nanobot/pull/2727)).
  - **Cron Job Data Integrity:** PR [#3606](https://github.com/HKUDS/nanobot/pull/3606) was merged to fix a bug where corrupt `jobs.json` files were silently overwritten, causing scheduled tasks to disappear.
- **Other Improvements:**
  - PR [#3583](https://github.com/HKUDS/nanobot/pull/3583) was merged, improving the beta WebUI by fixing turn completion signaling and chat isolation issues.
  - PR [#3614](https://github.com/HKUDS/nanobot/pull/3614) was merged, replacing a fatal workspace guard with a softer, retryable error policy.
  - PR [#1154](https://github.com/HKUDS/nanobot/pull/1154) was closed, implementing a new "Mezon" channel integration.
  - PR [#3600](https://github.com/HKUDS/nanobot/issues/3600) was closed after the fix was implemented.

#### 4. Community Hot Topics
The most active discussions and contributions focus on user experience and regional limitations.

- **Regional Model Access Blocking (Issue [#3618](https://github.com/HKUDS/nanobot/issues/3618)):** This is a critical, high-impact bug reported as a "严重BUG [Critical Bug]" where a user was blocked from using their Plus plan due to a `403: This model is not available in your region` error. The user was forced to restore a backup from 10 days prior. This issue highlights a significant pain point for users in specific geographies.
- **Concurrent Subagent Limit (Issue [#3611](https://github.com/HKUDS/nanobot/issues/3611) and PR [#3615](https://github.com/HKUDS/nanobot/pull/3615)):** An active feature request and corresponding PR address a common problem for users with local LLM servers (Ollama, mlx_lm). The lack of a concurrency limit for subagents causes Out-of-Memory (OOM) crashes on consumer hardware. The PR proposes a `maxConcurrentSubagents` setting, showing a responsive community.
- **Provider Logout Command (PR [#3612](https://github.com/HKUDS/nanobot/pull/3612) and Issue [#2665](https://github.com/HKUDS/nanobot/issues/2665)):** A feature request from March regarding re-authenticating an OpenAI Codex provider was finally addressed. This was a significant quality-of-life need that had been pending for over a month.

#### 5. Bugs & Stability
Several bugs were reported today, with the most severe having immediate fixes merged.

- **Critical: Regional Availability (Issue [#3618](https://github.com/HKUDS/nanobot/issues/3618)):** A user is entirely unable to use their preferred model due to a regional 403 error. **Severity: Critical (Service Blocking).** No specific fix PR exists, but it is a top-priority investigation.
- **High: Silent Turn Drop on Safety Guard (Issue [#3605](https://github.com/HKUDS/nanobot/issues/3605)):** When the `exec` tool is blocked by the safety guard, the error message does not reach the user (e.g., Telegram gets nothing), leaving them confused. **Severity: High (Data Loss/User Confusion).** This was addressed in PR [#3614](https://github.com/HKUDS/nanobot/pull/3614), which replaced the abort with a softer policy.
- **Medium: CLI Output Garbling (Issue [#3600](https://github.com/HKUDS/nanobot/issues/3600)):** API retry messages create ANSI garble in CLI output, causing a poor user experience, especially over SSH. **Severity: Medium (Usability).** Fix PR [#3609](https://github.com/HKUDS/nanobot/pull/3609) was already merged.
- **Medium: WhatsApp Voice Not Working (Issue [#3604](https://github.com/HKUDS/nanobot/issues/3604)):** Voice messages on WhatsApp are completely non-functional. **Severity: Medium (Feature Broken).** Fix PR [#3607](https://github.com/HKUDS/nanobot/pull/3607) was merged.
- **Medium: Safety Guard False Positives (Issue [#3599](https://github.com/HKUDS/nanobot/issues/3599)):** The safety guard blocks harmless commands like `rm` on files within the workspace due to false positives. **Severity: Medium (Usability).** Fix PR [#3613](https://github.com/HKUDS/nanobot/pull/3613) was merged.

#### 6. Feature Requests & Roadmap Signals
User requests signal a need for more mature security and deployment features.

- **Concurrent Subagent Limiting:** The request for a `maxConcurrentSubagents` setting (Issue [#3611](https://github.com/HKUDS/nanobot/pull/3615)) is a clear signal from users deploying NanoBot on local hardware. This is likely to be included in the next version, as a fix PR is already open.
- **Provider Logout:** The addition of a `provider logout` command (Issue [#2665](https://github.com/HKUDS/nanobot/issues/2665)) indicates that managing dynamic provider accounts is a core user workflow. This has now been implemented.
- **Xiaomi MiMo Support:** A user (Issue [#3617](https://github.com/HKUDS/nanobot/issues/3617)) is requesting documentation for using a "Xiaomi MiMo token plan," indicating users are exploring non-standard LLM providers.
- **Documentation for "Sen" Agent:** A new PR [#3608](https://github.com/HKUDS/nanobot/pull/3608) adds documentation for a new agent called "Sen," suggesting expansion of the agent ecosystem.

#### 7. User Feedback Summary
User satisfaction is mixed due to recent regressions, but the community is resilient and active.

- **Pain Points:**
    - **Model Access:** Users on Plus plans are being blocked by regional restrictions (Issue [#3618](https://github.com/HKUDS/nanobot/issues/3618)), causing significant frustration.
    - **Update Regressions:** Upgrading to `v0.1.5.post3` introduced new issues like safety guard false positives (Issue [#3599](https://github.com/HKUDS/nanobot/issues/3599)), suggesting a need for more rigorous regression testing.
    - **UI/UX Gaps:** Missing features such as voice message support (Issue [#3604](https://github.com/HKUDS/nanobot/issues/3604)) and silent errors on blocked commands (Issue [#3605](https://github.com/HKUDS/nanobot/issues/3605)) degrade the user experience.
- **Positive Signals:**
    - The user who restored from backup (Issue [#3618](https://github.com/HKUDS/nanobot/issues/3618)) reported that after reinstalling, NanoBot was alive and working, showing the system is generally recoverable.
    - There is strong community participation, with contributors creating PRs to fix their own reported bugs (e.g., [#3612](https://github.com/HKUDS/nanobot/pull/3612) by chengyongru).
    - Users are actively trying to extend NanoBot to new providers (Xiaomi MiMo, Sen agent), indicating high engagement.

#### 8. Backlog Watch
Several important PRs and issues appear to be languishing and may need maintainer attention.

- **Security PRs (PRs [#3492](https://github.com/HKUDS/nanobot/pull/3492), [#3255](https://github.com/HKUDS/nanobot/pull/3255), [#3252](https://github.com/HKUDS/nanobot/pull/3252), [#3235](https://github.com/HKUDS/nanobot/pull/3235)):** All authored by `mohamed-elkholy95`, these PRs address critical security concerns (SSRF, CSRF, filesystem-level history protection). They have been open since **April 17** but have seen no comments in 10-14 days. These are high-priority items that should be reviewed.
- **Heartbeat Reasoning (PR [#1443](https://github.com/HKUDS/nanobot/pull/1443)):** This feature to decouple heartbeat reasoning from notifications has been open since **March 2**, making it over two months old. It may be a large or complex change, or it has simply slipped through the cracks.
- **Telegram Group Features (PR [#2867](https://github.com/HKUDS/nanobot/pull/2867)):** This PR adds a Telegram group allowlist and is open since **April 6**. It could be a valuable feature for community managers.
- **SDK Result Population (PR [#3254](https://github.com/HKUDS/nanobot/pull/3254)):** This PR fixes a SDK consumer experience issue (`RunResult.tools_used` and `RunResult.messages` being empty) and has been open since **April 17**.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-04

## 1. Today's Overview
The Hermes Agent project is experiencing **very high activity**, with **50 issues updated** (38 open, 12 closed) and **50 PRs updated** (46 merged/closed, 4 open) in the last 24 hours. A significant number of PRs were **fast‑tracked by the core team** (many merged by @teknium1 as “salvages” of deferred PRs onto current `main`), indicating an active cleanup and stabilization push. No new releases were cut today, but the volume of merged fixes and feature work suggests a near‑term release is likely. The community is engaged on both functional improvements (CLI auto‑queue, MCP retry) and cultural/naming proposals.

---

## 2. Releases
**No new releases today.** The latest available version remains v0.12.0 (2026.4.30) as referenced in issue #19194.

---

## 3. Project Progress (Merged & Closed PRs)
46 PRs were merged or closed today, covering **bug fixes, security hardening, documentation updates, and minor feature enhancements**. Key highlights:

- **Browsing & Tooling:**  
  - `fix: _chromium_installed() honors AGENT_BROWSER_EXECUTABLE_PATH and system Chrome` ([#19298](https://github.com/NousResearch/hermes-agent/pull/19298), merged via [#19595](https://github.com/NousResearch/hermes-agent/pull/19595)) – unblocks browser tools for users with system Chrome or custom env vars.  
  - `fix(feishu): enable MEDIA attachment delivery in send_message tool` ([#19306](https://github.com/NousResearch/hermes-agent/pull/19306), merged via [#19596](https://github.com/NousResearch/hermes-agent/pull/19596)).

- **API Server & Config:**  
  - `fix: inherit reasoning config in API server runs` ([#19220](https://github.com/NousResearch/hermes-agent/pull/19220), merged via [#19599](https://github.com/NousResearch/hermes-agent/pull/19599)) – API server now respects `reasoning_effort` settings.  
  - `fix(setup): back up config.yaml before setup modifies it` ([#19383](https://github.com/NousResearch/hermes-agent/pull/19383), merged via [#19598](https://github.com/NousResearch/hermes-agent/pull/19598)).

- **Security:**  
  - `fix(security): bind Meet node server to localhost and restrict token file to owner read` ([#19382](https://github.com/NousResearch/hermes-agent/pull/19382), merged via [#19597](https://github.com/NousResearch/hermes-agent/pull/19597)) – closes a network‑exploitable RPC vector.

- **CLI / TUI Stability:**  
  - `fix(tui): restore terminal modes on all exit paths` ([#19210](https://github.com/NousResearch/hermes-agent/pull/19210), merged via [#19589](https://github.com/NousResearch/hermes-agent/pull/19589)) – fixes broken state in Fish shell after `/quit` (resolves #19194).  
  - `fix(tests): tolerate ps ancestor‑walk in find_gateway_pids fallback test` ([#19590](https://github.com/NousResearch/hermes-agent/pull/19590)).

- **Lifecycle & Monitoring:**  
  - `fix(agent): surface preflight compression status` ([#19247](https://github.com/NousResearch/hermes-agent/pull/19247), merged via [#19592](https://github.com/NousResearch/hermes-agent/pull/19592)) – gateway/WebUI now see compression progress.

- **Docs:**  
  - `docs: clarify session_search auxiliary model docs` ([#19296](https://github.com/NousResearch/hermes-agent/pull/19296), merged via [#19593](https://github.com/NousResearch/hermes-agent/pull/19593)).

- **Web UI:**  
  - `fix(web): add missing icons for config page category sidebar` ([#19219](https://github.com/NousResearch/hermes-agent/pull/19219), merged via [#19591](https://github.com/NousResearch/hermes-agent/pull/19591)).

---

## 4. Community Hot Topics
The most discussed issues and PRs (by comment count) reveal a mix of **quality‑of‑life features, platform integration glitches, and one cultural/renaming proposal**.

| Issue/PR | Title | Comments | Tag |
|----------|-------|----------|-----|
| [#18313](https://github.com/NousResearch/hermes-agent/issues/18313) | [Feature]: Proposal: Rename the project to "河马" (Hippo) | 8 | 🔥 Top discussion |
| [#13072](https://github.com/NousResearch/hermes-agent/issues/13072) | CLI Auto‑Queue Mode with Smart Interrupt and Crash Recovery | 5 | Feature request (Draft) |
| [#17998](https://github.com/NousResearch/hermes-agent/issues/17998) | viking_remember creates empty sessions — data never persisted | 4 | P2 bug |
| [#18836](https://github.com/NousResearch/hermes-agent/issues/18836) | Weixin Gateway timeout context manager bug | 4 | P2 bug |
| [#19294](https://github.com/NousResearch/hermes-agent/issues/19294) | _chromium_installed() ignores env var and system Chrome | 3 | P2 bug (now fixed) |
| [#19344](https://github.com/NousResearch/hermes-agent/issues/19344) | Planning Consultant — model‑initiated frontier‑model review via /consult | 3 | Feature request |
| [#19566](https://github.com/NousResearch/hermes-agent/issues/19566) | OpenAI‑Codex credential pool drops newly added credential after rotation | 3 | P2 bug |
| [#19559](https://github.com/NousResearch/hermes-agent/issues/19559) | MCP client doesn't retry connecting to HTTP servers after startup | 3 | Feature request |

**Analysis:**  
- The **renaming proposal** (#18313) is the most commented, reflecting a desire for better branding in China (away from the “Hermès” luxury connotation). It echoes a previous “Lobster” trend and suggests the community cares about cultural resonance.  
- **CLI auto‑queue** (#13072) and **MCP retry** (#19559) point to a need for more resilient and user‑friendly CLI/interaction patterns.  
- **Memory persistence** (#17998) and **credential pool** (#19566) are core reliability issues that could erode trust if left unfixed.

---

## 5. Bugs & Stability
**High‑severity bugs (P1) reported today:**

| Issue | Title | Status | Fix PR exists? |
|-------|-------|--------|----------------|
| [#17666](https://github.com/NousResearch/hermes-agent/issues/17666) | CLI: long pasted multi‑line messages silently dropped | **Closed** | Yes (presumed fixed, not explicitly linked) |
| [#19434](https://github.com/NousResearch/hermes-agent/issues/19434) | session_search recall failures: 4 bugs + 2 design gaps (P1) | **Open** | No |
| [#19471](https://github.com/NousResearch/hermes-agent/issues/19471) | `--profile` gateway crash loop after SIGTERM → event loop lost (P1) | **Open** | No |
| [#19566](https://github.com/NousResearch/hermes-agent/issues/19566) | Credential pool drops newly added credential (P2) | **Open** | No |
| [#19477](https://github.com/NousResearch/hermes-agent/issues/19477) | Todo tool state lost on gateway restart (P2) | **Open** | No |
| [#19040](https://github.com/NousResearch/hermes-agent/issues/19040) | Can't invoke personal skills after move (P2) | **Open** | No |
| [#19294](https://github.com/NousResearch/hermes-agent/issues/19294) | Chromium detection ignores env var (P2) | **Closed** | Fixed via #19298 |

**Additional stability notes:**  
- Several P2 bugs related to **memory/session search** (#17998, #14420) remain open, indicating a weak spot.  
- The **Kanban profile‑scoped DB** issue (#18959) was closed as duplicate, but the root cause (profile isolation) may still affect cron workers.  
- The **TUI terminal state corruption** (#19194) was fixed today (#19589).

---

## 6. Feature Requests & Roadmap Signals
Notable feature proposals that may shape the next release:

- **Rename to “河马” (Hippo)** (#18313) – if accepted, would require extensive rebranding across docs, code, and packages. Likely controversial but may proceed as an alias.  
- **CLI Auto‑Queue Mode** (#13072) – smart interrupt and crash recovery would improve the interactive experience. The deep draft suggests serious intent; possible inclusion in v0.13.  
- **Planning Consultant** (#19344) – a `/consult` command to escalate complex tasks to a frontier model. Fits the trend of hierarchical agent orchestration.  
- **MCP Client Retry on Startup** (#19559) – a common pain point for local MCP servers (TouchDesigner, etc.). Relatively small change, high impact.  
- **Suppress Lifecycle Status Messages on Gateways** (#19572) – reduces noise from fallback transitions, likely welcomed by Telegram/Slack users.  
- **Kanban Tool Auto‑Subscribe** (#19479) – when an agent creates a kanban task, automatically subscribe the originating chat to notifications. Nice QoL.

**Prediction:** The next minor release (v0.13) will likely include the **MCP retry**, **lifecycle suppression**, and **kanban auto‑subscribe** as low‑risk enhancements, plus the set of 46 merged fixes from today.

---

## 7. User Feedback Summary
Real user pain points extracted from today’s issue updates:

| Pain Point | Evidence | Sentiment |
|------------|----------|-----------|
| **Memory / context not persistent** | #17998 (viking_remember empty sessions), #14420 (agent can't recall earlier conversation) | Frustration – “data never persisted” |
| **WeChat integration broken** | #18836 (timeout context manager), users in China rely on WeChat | Moderate frustration; no fix PR yet |
| **CLI pastes lost** | #17666 – long multi‑line messages silently dropped | Fixed, but previously disruptive |
| **Credential management fragile** | #19566 – dropping new credentials in a pool | Concern about reliability in multi‑process setups |
| **Skills migration broken** | #19040 – personal skills relocated incorrectly, can't use `/command` | Confusion/annoyance – user asks “how to undo?” |
| **Terminal state corruption** | #19194 – Fish shell broken after `/quit` | Fixed today – satisfaction that issue was addressed |
| **Browser tools gated unnecessarily** | #19294 – system Chrome not detected | Fixed – positive response |

Overall, users are **actively engaged** but encountering real stability problems, especially around **memory persistence** and **platform gateways**. The quick turnaround on many fixes (e.g., chromium detection, terminal modes) is a positive sign for project health.

---

## 8. Backlog Watch
Long‑standing open issues that have not seen direct maintainer action:

| Issue | Title | Age | Priority | Notes |
|-------|-------|-----|----------|-------|
| [#4876](https://github.com/NousResearch/hermes-agent/issues/4876) | Upgrade bundled Node.js from 20 to 22 | Created 2026‑04‑03 | P3 | Node 20 LTS ends April 2026 – security risk |
| [#13126](https://github.com/NousResearch/hermes-agent/issues/13126) | Slack — TTS voice reply never sent after voice input | Created 2026‑04‑20 | P2 | No comment from maintainers; likely low usage |
| [#14420](https://github.com/NousResearch/hermes-agent/issues/14420) | Agent cannot read previous context (Ollama provider) | Created 2026‑04‑23 | P2 | User reports empty context – may be provider‑specific |
| [#13072](https://github.com/NousResearch/hermes-agent/issues/13072) | CLI Auto‑Queue Mode | Created 2026‑04‑20 | P3 | Draft phase, no maintainer response |
| [#17666](https://github.com/NousResearch/hermes-agent/issues/17666) | Long pasted multi‑line messages dropped | Created 2026‑04‑30 | P1 (closed) | Marked closed but no explicit fix PR linked; verify |
| [#13408](https://github.com/NousResearch/hermes-agent/issues/13408) | `bundle_content_hash` crashes with bytes values | Created 2026‑04‑21 | P2 | Closed as fixed – but re‑check if fix is in release |

**Action items for maintainers:**  
- Prioritise **Node.js upgrade** (#4876) before the April 2026 EOL.  
- Investigate **session_search** deep audit (#19434) – a critical memory recall component.  
- Triage **credential pool** (#19566) and **todo tool persistence** (#19477) – both affect everyday reliability.  
- Provide update on **memory context** (#14420) especially for Ollama users (a popular self‑hosted option).

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest – 2026-05-04

## Today's Overview

The project shows high activity with **4 issues updated** and **29 pull requests touched** in the last 24 hours. Of those PRs, **8 were merged or closed**, signaling steady progress toward the next release. The community is actively contributing features (image generation, multi-subagent parallelism, Gemini web search) while also fixing stability issues like build-from-source failures and provider compatibility bugs. Two open bugs remain, and one feature request (Ollama cloud credentials) has gathered significant discussion.

## Releases

No new releases today; the latest version remains unchanged.

## Project Progress

**Merged/Closed PRs today (8 total, 4 visible in top-20):**

- [#2764](https://github.com/sipeed/picoclaw/pull/2764) – **fix(agent):** Use runtime event kind for LLM retry (bug fix, merged).
- [#2754](https://github.com/sipeed/picoclaw/pull/2754) – **Feature:** Multi-subagent parallel calls (new capability, merged).
- [#2677](https://github.com/sipeed/picoclaw/pull/2677) – **Feat:** Unified runtime event infrastructure (merged, large architectural change).
- [#2682](https://github.com/sipeed/picoclaw/pull/2682) – **docs:** Fix `agents.defaults.model` config format in documentation (merged).

These changes advance agent event observability, introduce parallel subagent delegation, and fix documentation for V2→V3 migration.

## Community Hot Topics

- [#2225](https://github.com/sipeed/picoclaw/issues/2225) (10 comments) – **Open** request for Ollama cloud credentials. The user wants to use PicoClaw with Ollama Cloud but finds no credential configuration option. This is the most-discussed issue today, reflecting a growing need for cloud-hosted model backends.

- [#2753](https://github.com/sipeed/picoclaw/issues/2753) (1 comment) – **Open** bug report: building from source fails because `picoclaw-launcher` is missing. User followed README steps but the binary is absent.

## Bugs & Stability

| Severity | Issue / PR | Status | Description |
|----------|------------|--------|-------------|
| **High** | [#2753](https://github.com/sipeed/picoclaw/issues/2753) | Open | Build from source produces no `launcher` binary. Blocks fresh developers from running PicoClaw. No fix PR yet. |
| Medium | [#2718](https://github.com/sipeed/picoclaw/pull/2718) (closed) | Closed | DeepSeek (and strict providers) rejecting `image_url` in history when non-multimodal models receive images; fix merged. |
| Medium | [#2668](https://github.com/sipeed/picoclaw/issues/2668) (closed) | Closed | Gemini API 400 errors on MCP tools with complex JSON schemas (`$ref`, `anyOf`); fix released. |
| Low | [#2740](https://github.com/sipeed/picoclaw/pull/2740) | Open | DeepSeek streaming drops `reasoning_content`; fix awaiting review. |
| Low | [#2750](https://github.com/sipeed/picoclaw/pull/2750) | Open | Exec guard incorrectly treats relative paths as root-absolute; open fix. |
| Low | [#2725](https://github.com/sipeed/picoclaw/pull/2725) | Open | MCP initialization failure kills agent loop; non-fatal fix proposed. |

## Feature Requests & Roadmap Signals

- **Ollama cloud credentials** ([#2225](https://github.com/sipeed/picoclaw/issues/2225)) – High interest (10 comments). Likely to be addressed in the next minor release given community demand.
- **Image generation tool** ([#2760](https://github.com/sipeed/picoclaw/pull/2760)) – Open PR adding `image_generate` with OpenAI/Codex OAuth backend.
- **Stop command** ([#2762](https://github.com/sipeed/picoclaw/pull/2762)) – Open PR implementing `/stop` builtin to abort active agent tasks.
- **Subagent improvements** – Multiple PRs ([#2754](https://github.com/sipeed/picoclaw/pull/2754) merged, [#2761](https://github.com/sipeed/picoclaw/pull/2761) open) add parallel subagent calls and explicit agent_id selection.
- **Gemini web search provider** ([#2763](https://github.com/sipeed/picoclaw/pull/2763)) – Open PR bringing Google Search grounding to the `web_search` tool.
- **Multimodal/reasoning support** ([#2755](https://github.com/sipeed/picoclaw/pull/2755)) – Open PR adds streaming reasoning content and video media support for OpenAI-compatible providers (driven by Xiaomi Mimo).
- **V3 config documentation sync** ([#2766](https://github.com/sipeed/picoclaw/pull/2766)) – Large doc overhaul (26 files) aligning guides with the new V3 config schema.

These features point to a near-term release focused on **multimodal capabilities**, **agent control**, and **better provider integration**.

## User Feedback Summary

- **Build friction**: User [guettli](https://github.com/sipeed/picoclaw/issues/2753) reports the README “install from source” instructions are broken – the launcher binary is not produced. This indicates a need to update build scripts or documentation.
- **Ollama Cloud missing credentials**: [Suisei110](https://github.com/sipeed/picoclaw/issues/2225) wants to use Ollama Cloud but finds no credential option. Suggests a gap in provider configuration for cloud-hosted Ollama.
- **Provider compatibility pain**: Users reported 400 errors from Gemini (complex tool schemas) and DeepSeek (image in history). Both were fixed, but the feedback shows that strict provider validation is a recurring source of frustration.
- **Telegram media handling**: PRs [#2758](https://github.com/sipeed/picoclaw/pull/2758) and [#2756](https://github.com/sipeed/picoclaw/pull/2756) address specific Telegram user pain points – album grouping and topic context loss.

Overall, users appreciate the rapid fixes but need smoother onboarding and broader cloud provider support.

## Backlog Watch

- [#2225](https://github.com/sipeed/picoclaw/issues/2225) – **Open since 2026-03-31** (over a month). Feature request for Ollama cloud credentials with 10 comments and no maintainer response. This may become a blocker for users migrating to cloud-hosted models.
- [#2696](https://github.com/sipeed/picoclaw/pull/2696) – **Open since 2026-04-28** (6 days). Enhances MCP with per-request dynamic headers from channel context. Awaiting review.
- [#2725](https://github.com/sipeed/picoclaw/pull/2725) – **Open since 2026-04-30** (4 days). Critical fix for MCP initialization failure causing zombie gateways. Needs maintainer attention to merge.
- [#2740](https://github.com/sipeed/picoclaw/pull/2740) – **Open since 2026-05-01** (3 days). DeepSeek streaming fix; low severity but blocks thinking-mode usage.

No issues older than a month remain unaddressed except #2225, which is the longest-standing open request.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-04

## Today’s Overview

NanoClaw experienced a **high-activity day** on 3–4 May 2026, with 50 pull requests updated (34 merged/closed) and 10 issues resolved or updated in the last 24 hours. Development velocity is strong: the team merged multiple feature PRs—including headless sign-in support, migration UI fixes, and new MCP tools—while also closing eight bug reports. Two open issues remain, and no new releases were cut, suggesting the next stable version may be rounding on RC. Overall project health is vibrant, with community contributions flowing in alongside core team commits.

## Releases

No new releases in the last 24 hours.

## Project Progress

**34 pull requests were merged or closed** today, indicating a productive burst of work. Notable merged/closed PRs include:

- **#2222** – `fix: update /update-nanoclaw skill for v2 architecture` (gabi-simons) — adds dependency install, container typecheck, and channel/provider update awareness.
- **#2212** – `feat(setup): headless-aware Claude sign-in pre-message` (alipgoldberg) — shows accurate guidance for headless devices (Raspberry Pi, CI).
- **#2235** – `fix: migration UX improvements + legacy OneCLI container cleanup` (Koshkoshinsk) — bundling TTY guard, OneCLI health endpoint fix, and old service file retirement.
- **#2240** – `feat(mcp): add baget_read_document tool` (SamBagetAI) — resolves hallucinated `baget_send_document_file` calls.
- **#2239** – `feat(telegram): include company name in pairing welcome message` (SamBagetAI) — differentiates multiple Baget companies in Telegram.
- **#2229** – `Recognize ANTHROPIC_AUTH_TOKEN in setup verification` (SebTardif) — closes bug #853.
- **#2097** – `feat(skill): add Lore Context semantic memory skill` (zhushuanbao-dot) — enables cross-session memory via Lore Context integration.
- **#2228** – `feat(baget): partial team support` (SamBagetAI) — strips off‑team roles and falls back to CoS persona.
- **#2216** – `fix: migration script UX improvements` (Koshkoshinsk) — superseded by #2235 but contributed to final result.

Open PRs (16) include several security hardenings (#2004, #2000, #1999) and feature additions (#2237 interval scheduling, #2233 per‑group model overrides, #2238 MacPorts support) that are still under review.

## Community Hot Topics

- **Issue #853** – `Support ANTHROPIC_AUTH_TOKEN in setup verification` (3 comments, now closed). Community member `scguoi` reported the gap; fix PR #2229 by `SebTardif` was merged quickly, showing responsive triage.
- **Issue #2234** – `Can this work with llama.cpp?` (open, 0 comments). This is a fresh bug report from `Kwisss` describing a timeout error when connecting to llama.cpp. Though no comments yet, it may become a hot topic as external LLM integration is of high interest.
- **Issue #2227** – `Bug: engage_mode='always' not handled in evaluateEngage()` (open, 0 comments). This is a silent behavioral bug that could affect many users relying on `always` engagement.

Despite low comment counts, the high volume of merged PRs suggests the community is actively contributing code rather than lengthy discussion.

## Bugs & Stability

| Severity | Issue | Summary | Status | Fix PR |
|----------|-------|---------|--------|--------|
| **Critical** | #2221 | `gh CLI missing from agent container PATH (regression)` – prevents issue/PR operations | **Closed** | Not explicitly linked, but #2222 addresses container build updates |
| **High** | #2227 | `engage_mode='always' silently drops group messages` – messages lost with no log error | **Open** | — |
| **High** | #2234 | `Can this work with llama.cpp?` – connection fails with “didn't reply in time” | **Open** | — |
| **Medium** | #2223 | Agent conflates Telegram handle (`MythicalClaw`) with identity | **Closed** | — |
| **Medium** | #2220 | Agent posts to deregistered `'Old.wtf'` chat | **Closed** | — |
| **Low** | #2214 | iMessage local‑mode adapter never delivers inbound messages | **Closed** | — |
| **Low** | #853 | `ANTHROPIC_AUTH_TOKEN` not recognized | **Closed** | #2229 merged |

The most impactful regression (#2221 – `gh` missing) was resolved quickly. The open engage_mode bug (#2227) and the llama.cpp integration issue (#2234) need maintainer attention.

## Feature Requests & Roadmap Signals

- **Interval-based scheduling** (#2237) – `@every:<ms>` recurrence format has been proposed and has an open PR. Likely to land in the next minor release.
- **Per‑group model + effort overrides** (#2233) – Adds flexibility for multi‑agent setups. Strong signal for advanced configuration.
- **MacPorts support** (#2238) – Community request for macOS package manager diversity. Low‑risk and expected to merge.
- **Lore Context semantic memory** (#2097) – Already merged; marks a move toward richer memory beyond flat files.
- **Security hardening** (PRs #2004, #2000, #1999) – These have been open for ~10 days and represent a concerted security review. Likely to be merged soon after final review.
- **Headless/silent setup improvements** (#2212, #2206) – Already merged, but indicate ongoing UX polish.

Predictions for next release: scheduling intervals, per‑group model overrides, MacPorts support, and the security trio are all strong candidates.

## User Feedback Summary

- **Pain points**: Users report confusion around credential setup (#853), missing `gh` CLI after an update (#2221), messages going to deleted chats (#2220), and silent message drops when using `engage_mode='always'` (#2227). The llama.cpp integration failure (#2234) shows a desire to self‑host AI backends.
- **Use cases**: Multi‑company Baget deployments (#2239), headless/remote installations (#2212), and semantic memory for long‑running agents (#2097) are clearly important.
- **Satisfaction**: The fast closure of 8 issues within a day indicates responsive maintainership. However, the engage_mode bug and the llama.cpp issue are unresolved and may cause frustration for affected users.

## Backlog Watch

- **Security PRs #2004, #2000, #1999** (all by `Hinotoi‑agent`, opened April 25, updated May 3) – These address trust‑boundary hardening (canonical channels remote, webhook body caps, symlink rejection). They have no comments or reviews for 10 days, which is unusually quiet for security patches. Maintainer review is advised.
- **Open issue #2227** (engage_mode bug, opened May 3) – No PR yet despite being a high‑severity behavioral bug.
- **Open issue #2234** (llama.cpp integration) – Fresh, but could benefit from a maintainer response to confirm repro and suggest workarounds.
- **Open PR #2238** (MacPorts support) – Minimal controversy, could be merged quickly with a single reviewer.

No issues are older than two weeks, but the security PR queue is the biggest risk for stagnation.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-04

## Today's Overview
NullClaw saw moderate activity in the last 24 hours, with two issues and two pull requests updated. One PR (#884) was merged, bringing critical test coverage for high-risk runtime contracts and fixing several production bugs. Another PR (#883) remains open, addressing a pre-spawn executable resolution bug. No new releases were published. Overall, the project is stable with focused work on sandbox reliability, test infrastructure, and documentation of runtime contracts.

## Releases
*No new releases have been published.* The latest release remains unchanged.

## Project Progress
- **PR #884 [merged/closed]** — *Fix/add crit tests* by DonPrus. Added critical Zig coverage for NullClaw’s high-risk runtime contracts (ownership, lifecycle, security, routing, parser, and registry). The merge also fixed several production issues that were exposed by the new tests. This represents a concrete step toward improving runtime safety and regressions.
- **PR #883 [open]** — *probe: resolve executable before spawning child process* by mark-os. Adds a pre‑spawn check to `runQuietCommand` to verify the target executable exists on PATH before forking. This avoids a Zig stdlib bug where failed `execve` calls can leave zombie processes.

## Community Hot Topics
- **Issue #871 [OPEN] — Critical: web_search is impractical on low-resource devices without direct DuckDuckGo support**  
  *5 comments, updated today*  
  User `uMendex` reports that the current `web_search` feature is unusable on weak/low‑resource devices because the only practical options (Brave Search API with an external key, or other heavy dependencies) do not suit the intended lightweight use case. The request is for direct DuckDuckGo integration without external API keys. This is the most commented issue and reflects a clear community pain point for the target deployment environment.  
  [GitHub](https://github.com/nullclaw/nullclaw/issues/871)

- **Issue #882 [OPEN] — sandbox: default to Landlock on Linux, stop probing external tools at startup**  
  *2 comments, updated today*  
  Author `mark-os` proposes changing the `sandbox.backend: "auto"` default to use Landlock on Linux, thereby eliminating the costly and error‑prone startup probes for Firejail, Bubblewrap, and Docker. The proposal reduces startup latency and avoids spawning child processes that can cause issues (see #871 related).  
  [GitHub](https://github.com/nullclaw/nullclaw/issues/882)

## Bugs & Stability

| Severity | Bug | Fix / Workaround |
|----------|-----|------------------|
| **Critical** | **Issue #871** — `web_search` is impractical on low‑resource devices without direct DuckDuckGo support. Users relying on weak hardware have no viable search option. | No PR open yet; discussion ongoing. |
| **Medium** | **Issue #882** — Sandbox auto‑detection spawns child processes at startup, causing unpredictable failures and resource waste. | PR #883 (#probe PR) addresses part of the process‑spawn problem but does not fully resolve the sandbox probing issue. Workaround: manually set `sandbox.backend` to a specific tool. |
| **Low** | **PR #883** — A Zig stdlib bug can leave zombie processes when `execve` fails, due to missing executable resolution check before spawn. | The PR itself is the fix (still open). Once merged, it prevents the zombie process scenario. |

## Feature Requests & Roadmap Signals
- **Direct DuckDuckGo web search (Issue #871)** — Strong community demand for a built‑in, API‑key‑free search backend tailored to low‑resource devices. This could become a priority for the next minor release if the maintainers agree.
- **Default Landlock sandbox on Linux (Issue #882)** — A formal proposal to simplify sandbox configuration and remove startup probes. Likely to be accepted as a configuration default change, reducing maintenance burden and startup time.
- **Pre‑spawn executable resolution (PR #883)** — Although a bug fix, it indicates a broader interest in making NullClaw’s child‑process handling more robust, which could lead to further improvements in the `probe` module.

## User Feedback Summary
- **Pain points:** Users on low‑end hardware (e.g., Raspberry Pi, cheap VPS) find the `web_search` function unusable without a dedicated API key. The sandbox auto‑detection is also slow and brittle. Both issues were raised by active contributors.
- **Use cases:** The primary use case is running NullClaw on weak, cheap devices where external API dependencies and heavy tooling are undesirable.
- **Satisfaction:** The merging of PR #884 (critical tests and bug fixes) suggests that maintainers are responsive to quality and stability concerns, which is positively received.

## Backlog Watch
- **Issue #871** (opened 2026-04-25) — **Critical bug** regarding web search. Despite being open for over a week, it was updated today with new comments. No maintainer response or linked fix has appeared yet. This issue may require maintainer prioritisation to prevent user frustration.
- No other long‑unanswered or stale items were observed in the last 24‑hour snapshot.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-04

## 1. Today's Overview

Project activity remains intense, with 20 issues and 18 pull requests updated in the last 24 hours. The dominant theme is the **Reborn architecture overhaul** — 14 of the 20 updated issues are Reborn-related trackers defining contracts for turn coordination, persistence, cancellation, and runtime services. Three PRs were merged/closed today, including a critical Gemini tool-calling fix and two CI/e2e stabilization patches. No new releases were cut. The community is most engaged in the Configuration-as-Code epic (#3036) and terminal stability bugs (#3228). Overall project health is mixed: architectural progress is rapid, but several high-severity bugs (critical LLM config corruption, terminal corruption) remain unresolved.

## 2. Releases

No new releases in this period.

## 3. Project Progress

Three pull requests were merged/closed today:

- **#3226** (fix, merged) — [Fix Gemini thought_signature in OpenAI-compatible tool loops](https://github.com/nearai/ironclaw/pull/3226). This patch adds optional `thought_signature` to shared ToolCall types, threads it through LLM call sites, and adds integration regression coverage. It directly resolves bug #3225.

- **#3234** (closed) — [Replace deleted preflight test with tool_activate surface](https://github.com/nearai/ironclaw/pull/3234). An e2e test was removed in a previous engine-v2 change; this PR updates the CI workflow to use an equivalent test, unblocking the Live Canary auth lanes.

- **#3170** (closed) — [Add host runtime vertical gates](https://github.com/nearai/ironclaw/pull/3170). Part of the Reborn integration effort, this adds caller-level gate coverage for durable replay, mount attenuation, and resource limits.

Notable open PRs advancing core architecture:
- **#3230** — [Land Reborn substrate into main behind default-off gates](https://github.com/nearai/ironclaw/pull/3230). A massive (XL) PR merging the Reborn substrate from `reborn-integration` into `main` to reduce branch drift. This is the first major integration step.
- **#3099** — [Add Reborn transport adapter contract](https://github.com/nearai/ironclaw/pull/3099) (XL, core contributor).
- **#3212** — [Add Reborn event projection service](https://github.com/nearai/ironclaw/pull/3212) (XL).
- **#3171** — [Add Reborn event store backends](https://github.com/nearai/ironclaw/pull/3171) (XL).

## 4. Community Hot Topics

The most active issues by comments and reactions:

- **[#3036 — Configuration-as-Code for IronClaw Reborn: tenant blueprints and use-case harnesses](https://github.com/nearai/ironclaw/issues/3036)** (3 comments, 1 👍). This epic proposes declarative configuration for two operator classes currently forced to hand-edit multiple files. The high engagement suggests strong user demand for schema-driven, auditable setup.

- **[#3016 — Reborn cutover blocker: add reference AgentLoopHost facade](https://github.com/nearai/ironclaw/issues/3016)** (3 comments, 0 👍). A critical architectural tracker with many dependent issues.

- **[#3225 — Gemini API-key backend fails tool-calling with missing thought_signature](https://github.com/nearai/ironclaw/issues/3225)** (1 comment). Quickly resolved by merged PR #3226.

- **[#3228 — Terminal corruption after /quit in SSH/noVNC/screen/tmux](https://github.com/nearai/ironclaw/issues/3228)** (1 comment, high severity). Affects headless/remote users — a pain point for containerized deployments.

The underlying needs are clear: users want a **declarative, consistent configuration system** (#3036) and **reliable terminal behavior** in remote/headless environments (#3228, #3227).

## 5. Bugs & Stability

Bugs reported or updated today, ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **Critical** | [#3229](https://github.com/nearai/ironclaw/issues/3229) | LLM provider fallback persists to DB on startup, permanently destroying user's model/provider config. Component: `src/config/mod.rs` — `resolve_llm_with_secre...`. | None yet |
| **High** | [#3228](https://github.com/nearai/ironclaw/issues/3228) | Terminal corruption after `/quit` in multiplexed/remote sessions — mouse tracking only partially disabled. Affects SSH, noVNC, screen, tmux. | None yet |
| **Medium** | [#3227](https://github.com/nearai/ironclaw/issues/3227) | TUI text copy fails silently in headless/X11-less environments (arboard needs X11/Wayland). | None yet |
| **Medium** | [#3201](https://github.com/nearai/ironclaw/issues/3201) | Tool use for Deepseek is not working (`deepseek-v4-flash`). | None yet |
| **Resolved** | [#3225](https://github.com/nearai/ironclaw/issues/3225) | Gemini API-key backend fails tool-calling with missing `thought_signature`. | [Merged #3226](https://github.com/nearai/ironclaw/pull/3226) |

The critical bug #3229 is particularly concerning because it can permanently corrupt a user's LLM configuration after a simple restart. No fix PR exists yet.

## 6. Feature Requests & Roadmap Signals

The most prominent feature request is **Configuration-as-Code** (#3036), an epic for tenant blueprints and use-case harnesses. This is likely a candidate for the next major release, as it directly addresses a common operator pain point.

Several Reborn architecture issues define contracts that are **blocking the cutover** from the current agent loop to the new architecture:
- TurnCoordinator (#3013, #3198, #3016)
- TurnRunner (#3199)
- Turn persistence (#3202)
- Cancellation semantics (#3238)
- LoopExit contract (#3232)
- Follow-up architecture deepening (#3231)

These are all high-priority internal items, but will eventually translate into user-facing improvements in stability, scalability, and observability.

The **Slack Socket Mode** PR (#1549, open since March 21) and **NEAR intents trial** PR (#3218) indicate community desire for connectivity without public URLs and for crypto integration.

## 7. User Feedback Summary

Real pain points expressed through issues:

- **Terminal corruption** (#3228): Users running IronClaw in LXC containers or via SSH/tmux experience broken terminal state after quitting. This is a significant quality-of-life issue for headless/remote operators.
- **LLM config corruption** (#3229): A single restart can wipe out carefully configured provider settings — critical for production users.
- **Headless clipboard failure** (#3227): TUI copy fails silently, breaking workflow for users without X11/Wayland.
- **Deepseek tool use broken** (#3201): A specific provider integration issue affecting users who rely on Deepseek.

Satisfaction signals are harder to find, but the rapid pace of Reborn development and the quick fix for Gemini thought_signature (#3226) show responsive maintainers.

## 8. Backlog Watch

Items that have remained open or unanswered for an extended period:

- **[#1549 — Slack Socket Mode for NAT-friendly connectivity](https://github.com/nearai/ironclaw/pull/1549)** (open since 2026-03-21, 44 days). A large PR from a new contributor with no comments from maintainers. Risk of bitrot.

- **[#2593 — chore(deps): bump the actions group](https://github.com/nearai/ironclaw/pull/2593)** (open since 2026-04-17, 17 days). A dependency bump PR from Dependabot that has not been merged or commented on.

- **[#2973 — chore(deps): bump the everything-else group](https://github.com/nearai/ironclaw/pull/2973)** (open since 2026-04-26, 8 days). Similar situation.

- **[#2971, #2972 — tokio-ecosystem and wasm group dependency bumps](https://github.com/nearai/ironclaw/pull/2971)** (open since 2026-04-26). These dependency updates could introduce breaking changes if not reviewed.

- **[#3099 — Add Reborn transport adapter contract](https://github.com/nearai/ironclaw/pull/3099)** (open since 2026-04-29, 5 days). Core contributor PR, but no review activity yet despite being a large architectural change.

No long-unanswered issues were identified beyond the above PRs; most issues have maintainer activity within the last 24h.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-05-04

**Project:** [LobsterAI](https://github.com/netease-youdao/LobsterAI)  
**Date:** 2026-05-04

---

## 1. Today's Overview

Project activity remains minimal. In the last 24 hours, one new feature request was opened (Issue #1880) and one stale optimization pull request (PR #811) received a routine update but remains unmerged. No new releases, no closed issues, and no merged PRs were recorded. The overall pulse suggests a maintenance phase with low community engagement, though the single new issue signals that users are still looking for expanded capabilities like third‑party agent integration.

---

## 2. Releases

No new releases were published today.

---

## 3. Project Progress

**Merged/Closed PRs today:** None.

**Active PR:**  
- [#811 – `perf(cowork): 使用索引表优化流式消息更新查找性能从 O(n) 到 O(1)`](https://github.com/netease-youdao/LobsterAI/pull/811)  
  **Status:** Open (created 2026‑03‑25, updated 2026‑05‑04). Marked as stale.  
  **Summary:** This performance optimization introduces an index map to reduce the time complexity of streamed message updates from O(n) to O(1). Despite being open for over a month, the PR has received no reviewer feedback and has not been merged. No other PRs advanced today.

---

## 4. Community Hot Topics

Only one issue was updated in the last 24 hours:  

- [#1880 – [OPEN] 希望增加Hermes Agent功能](https://github.com/netease-youdao/LobsterAI/issues/1880)  
  **Author:** ecolife007 · Created: 2026‑05‑03 · Comments: 0 · 👍: 0  
  **Summary:** Requests the addition of Hermes Agent and OpenClaw integration, similar to Open WebUI’s “Connect an Agent” feature. The user references [Open WebUI docs](https://docs.openwebui.com/getting-started/quick-start/connect-an-agent/) as a design pattern.  
  **Analysis:** The absence of community reactions suggests this is an early, individual request. However, the reference to a well‑known project (Open WebUI) indicates a desire for agent interoperability – a recurring theme in the AI‑assistant ecosystem. The maintainers may want to evaluate whether this aligns with LobsterAI’s roadmap.

No PR had comments today.

---

## 5. Bugs & Stability

No new bugs, crashes, or regressions were reported in the last 24 hours.

---

## 6. Feature Requests & Roadmap Signals

The only feature request is **Issue #1880** (Hermes Agent integration). While it currently has no upvotes, the underlying idea – enabling users to connect third‑party agents (Hermes Agent, OpenClaw) to LobsterAI – resonates with the growing trend of composable AI workflows. If the project’s roadmap includes multi‑agent support or external tool integration, this request could become a candidate for the next minor release. Otherwise, it may remain as a “nice‑to‑have” backlog item.

No other roadmap signals emerged today.

---

## 7. User Feedback Summary

- **Pain points:** No direct feedback was provided beyond the feature request. However, the request itself implies that users find the current agent ecosystem limited and would prefer a more open, connectable architecture similar to Open WebUI.
- **Use cases:** The user envisions a scenario where LobsterAI can delegate tasks to specialized agents (e.g., Hermes Agent for reasoning, OpenClaw for code execution) via a simple UI.
- **Satisfaction/Dissatisfaction:** No explicit sentiment data is available. The low volume of activity may indicate either general satisfaction or project neglect – further data would be needed to differentiate.

---

## 8. Backlog Watch

- **PR #811 – `perf(cowork)` (stale, open since 2026‑03‑25)**  
  This PR introduces a meaningful performance improvement but has been stuck without review for over a month. If left untouched, the code could diverge from the main branch, increasing merge effort. **Recommended action:** A maintainer should review and either merge, request changes, or close with explanation.

- **Issue #1880 – Hermes Agent request (open, no response)**  
  While not urgent, this is the only issue currently open. A quick acknowledgement or question from maintainers would improve community perception and encourage further engagement.

Maintainer attention is especially warranted for PR #811, as it directly improves code quality and has been waiting the longest.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-05-04

## 1. Today's Overview

Project activity is light but focused. One open issue was updated in the last 24 hours, highlighting an intermittent bug where tool calls with malformed or empty arguments can collapse into missing required fields, causing pre‑dispatch validation failures. Two pull requests remain open—one improves TTS provider documentation (Piper and Coqui) and another fixes reasoning content replay for DeepSeek models. No releases or merged PRs occurred today, indicating a maintenance and bug‑fix phase rather than feature expansion. Overall project health is stable, with maintainers actively addressing reported issues and regression gaps.

## 2. Releases

No new releases are available. The latest release remains unchanged. Skipping further detail.

## 3. Project Progress

No pull requests were merged or closed today. However, two open PRs represent ongoing contributions:

- **#962 – Update local TTS provider docs**  
  Revises Piper and Coqui documentation: updates Piper to link to the maintained OHF‑Voice repository and current voices page; updates Coqui to reference the maintained `idiap/coqui-ai-TTS` fork, the `coqui-tts` package, and the current container image. Also adds the Piper `.onnx.json` config download to match current usage.  
  [View PR #962](https://github.com/moltis-org/moltis/pull/962)

- **#961 – fix(providers): replay DeepSeek reasoning content**  
  Fixes issue #959 by preserving provider reasoning on typed assistant messages when converting persisted chat history, and replaying tool reasoning as `reasoning_content` for DeepSeek/OpenAI‑compatible follow‑up requests. Includes regression coverage for DeepSeek V4 thinking‑mode scenarios.  
  [View PR #961](https://github.com/moltis-org/moltis/pull/961)

Both PRs address community‑raised concerns (documentation accuracy and reasoning replay) and are close to review.

## 4. Community Hot Topics

Activity is very low; the only open issue and both open PRs each have zero comments and zero reactions. No discussion or debate emerged in the last 24 hours. The absence of engagement suggests either a small user base or that reported topics are well‑understood and do not require community back‑and‑forth.

- **Issue #963** – *Tool calls with malformed or empty arguments collapse to missing required fields*  
  This is the sole active issue and likely the most impactful for users relying on tool‑using agents. It describes intermittent `exec` failures with `missing=command` after the model has previously succeeded, caused by schema validation occurring before `ExecTool.execute()` or `BeforeToolCall` hooks run.  
  [View Issue #963](https://github.com/moltis-org/moltis/issues/963)

## 5. Bugs & Stability

One high‑severity bug was reported and remains open without a known fix PR:

- **#963 (Open, High Severity)**  
  **Symptoms:** Intermittent `exec` tool calls fail with `missing=command` even when the model has previously activated the tool successfully. The error occurs during pre‑dispatch schema validation, bypassing normal execution hooks.  
  **Impact:** Breaks core tool‑calling reliability, especially in multi‑step agent workflows.  
  **Status:** No fix PR yet; maintainers have not commented.

Additionally, PR #961 fixes a related regression (#959) about DeepSeek reasoning content not being replayed correctly across chat history conversions. That fix is under review and will likely land soon, improving stability for DeepSeek/OpenAI‑compatible providers.

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today. The two PRs are incremental improvements—TTS documentation alignment and reasoning replay correction—rather than new features. Based on the recent pattern, the next version is likely to focus on:

- **Reliability improvements** for tool‑calling validation (driven by issue #963)  
- **Provider parity** for reasoning content across all OpenAI‑compatible backends  
- **Documentation refresh** for local TTS integrations (Piper/Coqui)  

A roadmap signal is the inclusion of regression tests in PR #961, indicating a push toward more robust testing before new releases.

## 7. User Feedback Summary

User feedback is limited but revealing:

- **Pain point (Issue #963):** A user reports that tool calls fail intermittently due to validation happening too early, causing confusion because the model appears to use the tool correctly but the runner rejects it. This undermines trust in agent‑assisted workflows.
- **Improvement request (PR #962):** A contributor updated TTS documentation to reflect actively maintained forks and packages, addressing a gap where users were being directed to stale resources.
- **Bug report (PR #961 fix for #959):** DeepSeek users lost reasoning content after chat history conversion; the contributor provided a targeted fix with tests.

Overall satisfaction is likely moderate—the project addresses reported issues quickly, though the validation bug remains open.

## 8. Backlog Watch

No long‑unanswered or high‑priority issues or PRs requiring maintainer attention were identified in the 24‑hour window. The open issue #963 is recent (created yesterday) and has not yet been triaged. There are no stale PRs or ignored community requests visible in this snapshot. The project appears to keep a clean backlog.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the CoPaw project digest for **2026-05-04**.

---

## CoPaw Project Digest — 2026-05-04

### 1. Today's Overview

Project activity remains **high**, with 27 issues and 16 pull requests updated in the last 24 hours. The team continues to prioritize stability and hardening, merging 12 PRs today, many from the core contributor `futuremeng` focusing on MCP runtime improvements, stream sanitization, and context overflow recovery. A notable wave of user-reported bugs emerged around memory management, configuration persistence, and local model compatibility, balanced by several high-quality first-time-contributor PRs addressing file security and media handling. The community is actively discussing agent isolation, Hermes-inspired architecture upgrades, and interactive UI enhancements.

### 2. Releases

**None.** No new versions or releases were published today.

### 3. Project Progress

Twelve PRs were merged or closed today, reflecting a strong push on runtime stability and developer experience:

- **MCP Ecosystem Hardening:** Multiple PRs by `futuremeng` improved MCP import validation, template generation, runtime status diagnostics ([#1978](agentscope-ai/QwenPaw PR #1978)), degraded connection errors to tool-level failures ([#2052](agentscope-ai/QwenPaw PR #2052)), and added graceful MCP teardown on shutdown ([#1977](agentscope-ai/QwenPaw PR #1977)). A new MCP source browsing and import flow was also merged ([#1883](agentscope-ai/QwenPaw PR #1883)).
- **Agent & Stream Stability:** Context overflow recovery was enhanced with automatic compaction retry ([#2783](agentscope-ai/QwenPaw PR #2783), [#2240](agentscope-ai/QwenPaw PR #2240)). A streaming fix sanitizes leaked reasoning/thinking prefixes from visible text ([#2784](agentscope-ai/QwenPaw PR #2784)).
- **Desktop & Connectivity:** A fix cleans up stale packaged backend processes on startup to prevent port conflicts ([#1479](agentscope-ai/QwenPaw PR #1479)). Ollama connectivity now defaults to `127.0.0.1` with better error surfacing ([#1480](agentscope-ai/QwenPaw PR #1480)).
- **First-Time Contributor (FTC) PRs:**
    - [#4026](agentscope-ai/QwenPaw PR #4026) introduces `WriteFileOverwriteGuardian` to prevent `write_file` from silently overwriting non-empty files.
    - [#4021](agentscope-ai/QwenPaw PR #4021) fixes `file://` URL audio block processing in the message pipeline.
    - [#3928](agentscope-ai/QwenPaw PR #3928) adds a safe default timeout for `delegate_external_agent` tool.

### 4. Community Hot Topics

| Issue/PR | Title | Activity | Underlying Need |
|---|---|---|---|
| [#3936](https://agentscope-ai/QwenPaw Issue #3936) (CLOSED) | [Question]: 智能体之间是否可以完全隔离... | 8 comments | **Agent isolation & workspace security.** Users want granular per-agent file sandboxing (white/blacklist) to prevent cross-contamination. |
| [#1516](https://agentscope-ai/QwenPaw Issue #1516) (OPEN) | [Bug]: AudioContent not supported in Telegram | 5 comments | **Cross-platform media support.** Voice messages in Telegram need proper conversion for LLM processing. |
| [#4024](https://agentscope-ai/QwenPaw Issue #4024) (OPEN) | [Feature]: 有计划借鉴下Hermes的机制升级qwenpaw么 | 3 comments | **Architecture curiosity.** Users are watching competitive projects (Hermes) and questioning CoPaw’s evolution strategy. |
| [#3977](https://agentscope-ai/QwenPaw Issue #3977) (OPEN) | [Bug]: 对话上下文没有记忆管理... | 4 comments | **Memory search reliability.** `memory_search` crashing due to `list` vs `dict` type mismatch is a critical UX blocker. |

**Analysis:** The strongest signal is the demand for **better agent isolation and memory safety**. Users want predictable, auditable system behavior—especially as workflows grow more complex. The Hermes comparison query signals a need for clearer roadmap communication.

### 5. Bugs & Stability

**High Severity:**
- **[#4025](https://agentscope-ai/QwenPaw Issue #4025) (OPEN):** **ARM64 Docker image incompatibility.** Local LLM fails on ARM64 due to Debian 12’s older GLIBC (2.36) vs. llama.cpp’s requirement for GLIBC 2.38+. **Fix not yet proposed.**
- **[#4015](https://agentscope-ai/QwenPaw Issue #4015) (OPEN):** **Mac M5 Pro local model failure.** Bundled Python spawns subprocesses under Rosetta (i386), breaking native ARM tools. **Fix not yet proposed.**
- **[#4017](https://agentscope-ai/QwenPaw Issue #4017) (OPEN):** **Network reconnection deadlock.** Enabling `HEARTBEAT.md` prevents agent channels from reconnecting after network interruptions. **Fix not yet proposed.**

**Medium Severity:**
- **[#4023](https://agentscope-ai/QwenPaw Issue #4023) (OPEN):** **Severe input field lag.** User reports extreme input box stuttering on the console frontend, degrading core editing experience.
- **[#3969](https://agentscope-ai/QwenPaw Issue #3969) (OPEN):** **`FunctionCallOutput` validation error.** `call_id` being `None` triggers `ValidationError` and corrupts `loop_config.json`. **Fix not yet proposed.**
- **[#3019](https://agentscope-ai/QwenPaw Issue #3019) (OPEN):** **Skill uninstall corrupts skill.json.** Removing a Chinese-named skill breaks encoding, preventing default agent startup. **Open since April 7.**
- **[#3984](https://agentscope-ai/QwenPaw Issue #3984) (OPEN):** **Context compaction orphans assistant messages.** After compaction, frontend may show an assistant response without a preceding user message. **Fix not yet proposed.**

**Lower Severity / Fixed:**
- **[#3991](https://agentscope-ai/QwenPaw Issue #3991) (CLOSED):** Ollama channel dropping conversation history—was correctly closed.
- **[#3992](https://agentscope-ai/QwenPaw Issue #3992) (CLOSED):** Agent stops responding after several conversation rounds—resolved.

### 6. Feature Requests & Roadmap Signals

| Issue | Request | Likelihood for Next Version |
|---|---|---|
| [#4002](https://agentscope-ai/QwenPaw Issue #4002) | Visual shared canvas (drag/annotate) for human-AI interaction | Low (very large UI feature) |
| [#4001](https://agentscope-ai/QwenPaw Issue #4001) | Manual single-message deletion in chat history | Medium (high demand, relatively standalone) |
| [#4019](https://agentscope-ai/QwenPaw Issue #4019) | Mid-task guidance mode (like Codex’s steering during execution) | Low-Medium (user already has a prototype) |
| [#4020](https://agentscope-ai/QwenPaw Issue #4020) | Force `MEMORY/AGENTS/SOUL` files read-only at tool layer | **High** (PR [#4026](https://agentscope-ai/QwenPaw PR #4026) already implements a related guard) |
| [#3995](https://agentscope-ai/QwenPaw Issue #3995) | Enhanced memory lifecycle management (auto-archive, conflict detection) | Medium (aligns with ongoing memory quality focus) |
| [#4022](https://agentscope-ai/QwenPaw Issue #4022) | Save workspace config files to sub-folder | Medium (simple structural improvement) |

**Prediction:** The next release will likely include **file write protection** (PR #4026 is under review) and possibly **configurable MCP client timeout** (issue #3997 is trending). The user request for a **codex-like guidance mode** may not be native but a prototype already exists.

### 7. User Feedback Summary

**Pain Points:**
1. **Configuration fragility:** Multiple users report settings being reset after update (e.g., embedding config [#4018](https://agentscope-ai/QwenPaw Issue #4018), `loop_config.json` corruption [#3969](https://agentscope-ai/QwenPaw Issue #3969)).
2. **Memory loss:** Ollama users lose conversation history ([#3991](https://agentscope-ai/QwenPaw Issue #3991)—fixed); `memory_search` errors interrupt workflows ([#3977](https://agentscope-ai/QwenPaw Issue #3977)).
3. **File write risks:** Users frustrated that AI agents can inadvertently overwrite memory/config files, causing data loss ([#4020](https://agentscope-ai/QwenPaw Issue #4020)).
4. **Local model friction:** Apple Silicon (especially M5 Pro) and Docker ARM64 users face subprocess/path irregularities ([#4003](https://agentscope-ai/QwenPaw Issue #4003), [#4015](https://agentscope-ai/QwenPaw Issue #4015), [#4025](https://agentscope-ai/QwenPaw Issue #4025)).
5. **UI micro-friction:** Missing single-message delete, no system tray icon, and severe input lag ([#4023](https://agentscope-ai/QwenPaw Issue #4023)) frustrate daily users.

**Satisfaction Signals:**
- Users appreciate the MCP ecosystem progress and are actively testing Jin10 MCP integrations ([#3961](https://agentscope-ai/QwenPaw Issue #3961)).
- Community members are proactively building extensions (e.g., Guide Mode prototype in [#4019](https://agentscope-ai/QwenPaw Issue #4019)).

### 8. Backlog Watch

| Issue/PR | Age | Summary | Reason for Concern |
|---|---|---|---|
| [#2430](https://agentscope-ai/QwenPaw Issue #2430) | 5 weeks | **System tray icon + minimize to tray** | No maintainer response since creation; moderate upvotes. |
| [#3019](https://agentscope-ai/QwenPaw Issue #3019) | 4 weeks | **Skill uninstall corrupts skill.json** | Reproducible bug blocking default agent startup; no fix proposed. |
| [#3984](https://agentscope-ai/QwenPaw Issue #3984) | 4 days | **Context compaction orphans assistant messages** | Directly affects chat history rendering; root cause identified but no fix PR yet. |
| [#3997](https://agentscope-ai/QwenPaw Issue #3997) | 2 days | **MCP client timeout not configurable** | Simple config model gap; feature request with clear workaround. |

**Urgent Attention Needed:** The **ARM64 Docker incompatibility** ([#4025](https://agentscope-ai/QwenPaw Issue #4025)) blocks an entire user segment from using local LLMs. This is a deployment-breaking issue that should be prioritized alongside the **network reconnection deadlock** ([#4017](https://agentscope-ai/QwenPaw Issue #4017)).

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-04

## 1. Today’s Overview
Project activity was minimal over the last 24 hours, with no new issues, releases, or merged pull requests. A single open PR (#571) was updated, proposing an enhancement to the `longterm_memory` tool’s description by adding concrete trigger phrases. Overall, the project appears to be in a quiet phase with no closed work or reported problems.

## 2. Releases
No new releases were published. There are no versions to report for this period.

## 3. Project Progress
No pull requests were merged or closed today. The only active PR (#571) remains open and has not yet been integrated. No features, fixes, or changes were finalized.

## 4. Community Hot Topics
- **PR #571** – *feat(tools): trigger-phrase nudges in longterm_memory description*  
  [View on GitHub](https://github.com/qhkm/zeptoclaw/pull/571)  
  This is the only item updated in the last 24 hours. It aims to rewrite the `longterm_memory` tool’s description to enumerate explicit “Use when” / “Do NOT use when” triggers, following patterns from Hermes Agent’s `memory_tool.py`. It also adds a doc-test to guard the trigger block. Despite being the sole topic of discussion, it has attracted no comments or reactions yet, suggesting low community engagement at this time.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project has no open stability issues to note.

## 6. Feature Requests & Roadmap Signals
The only feature signal is **PR #571**, which introduces structured trigger-phrase nudges for the `longterm_memory` tool. This is a quality-of-life and documentation improvement that aligns with best practices seen in other agent toolkits. Given its straightforward nature and lack of opposition, it is likely to be merged in the next minor version update.

## 7. User Feedback Summary
There is no user feedback captured in this period — no issues, comments, or reactions were posted. User sentiment cannot be assessed from the available data.

## 8. Backlog Watch
No long-unanswered or stale issues or PRs exist. The only open PR (#571) was created and updated on 2026-05-03, so it does not yet require maintainer attention for neglect. The project maintainer queue is clear.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-04

## Today's Overview
ZeroClaw saw high activity with **50 issues** and **50 PRs** updated in the last 24 hours. **19 PRs were merged or closed**, while **31 remain open**. No new releases were cut today. The project is heavily focused on **v0.8.0 schema migrations** (schema v3, `SwarmConfig`, agent filesystem reorganisation) and **desktop/Tauri parity** for macOS (signed builds, notarization, accessibility permissions). Several high-severity bugs affecting provider integrations (DeepSeek, Gemini, WhatsApp) have been reported and are actively being triaged, with a security‑related plugin PR (#6274) merged.

## Releases
**None** — no new tags or release artifacts were published within the reporting window.

## Project Progress (Merged/Closed PRs)
The 19 merged/closed PRs include several notable improvements:

- [#6352](https://github.com/zeroclaw-labs/zeroclaw/pull/6352) – **add support rocket chat** (channel addition, closed without merge? actually closed)
- [#6299](https://github.com/zeroclaw-labs/zeroclaw/pull/6299) – **fix(installer): install prebuilt dashboard assets** – ensures web UI works after binary installs.
- [#6274](https://github.com/zeroclaw-labs/zeroclaw/pull/6274) – **feat(skills): consolidate first‑party skills into repo, default to compact mode** – moves skills from an external repository into a top‑level `skills/` directory, simplifying distribution.

Other merged PRs (not shown in top 20) likely include follow‑up fixes for streaming, memory, and gateway improvements.

## Community Hot Topics
The most active discussions (by comment count) reveal key pain points and development blockers:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#6233](https://github.com/zeroclaw-labs/zeroclaw/issues/6233) | 8 | `chat_messages_to_native()` drops `reasoning_content` for plain‑text assistant messages after streaming fix – affects DeepSeek V4 multi‑turn conversations. |
| [#5947](https://github.com/zeroclaw-labs/zeroclaw/issues/5947) | 6 | **Schema v3** – batch breaking field migrations; a merge blocker for v0.8.0. |
| [#5878](https://github.com/zeroclaw-labs/zeroclaw/issues/5878) | 4 | **v0.7.5 release automation** milestone tracking. |
| [#6298](https://github.com/zeroclaw-labs/zeroclaw/issues/6298) | 3 | Empty `tool_calls` array sent to provider API causing 400 errors on strict validators (DeepSeek, NVIDIA NIM). |
| [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | 2 | Gemini 400 – `assistant` tool_call emitted as first non‑system turn (violates Gemini history order). |

**Underlying needs**: Contributors are experiencing integration friction with advanced provider features (reasoning content, strict tool validation, conversation history ordering). The high comments on #5947 and #5878 indicate strong community interest in both the v0.8.0 migration and a reliable release pipeline.

## Bugs & Stability
Several high‑severity bugs were reported today, each with the potential to break core functionality:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| 🔴 **High** | [#6298](https://github.com/zeroclaw-labs/zeroclaw/issues/6298) | Empty `tool_calls` array sent to providers (DeepSeek, NVIDIA NIM) when `use_native_tools` enabled – causes 400 errors. | Not yet |
| 🔴 **High** | [#6302](https://github.com/zeroclaw-labs/zeroclaw/issues/6302) | Gemini model rejects requests where first turn is `assistant` with `tool_calls` (violates Gemini API contract). | Not yet |
| 🔴 **High** | [#6351](https://github.com/zeroclaw-labs/zeroclaw/issues/6351) | WhatsApp Web – self‑chat‑mode triggers on all `fromMe` messages, causing agent to reply to the operator’s own contacts. | Not yet |
| 🔴 **High** | [#6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350) | WhatsApp Web – `allowed-numbers` bypassed for LID‑based contacts; messages silently dropped. | Not yet |
| 🟡 **Medium** | [#6348](https://github.com/zeroclaw-labs/zeroclaw/issues/6348) | Dashboard Agent chat renders every `tool_call` as a standalone chat bubble, including errored calls. | Not yet |
| 🟡 **Medium** | [#6349](https://github.com/zeroclaw-labs/zeroclaw/issues/6349) | Desktop menu‑bar chat inherits same tool_call rendering defect as dashboard. | Not yet |
| 🟢 **Low** | [#6347](https://github.com/zeroclaw-labs/zeroclaw/issues/6347) | Telegram channel tests fail under default features. | Not yet |

No fix PRs are currently linked for these bugs, but the team has accepted several (`status:accepted`) for the WhatsApp and dashboard issues.

## Feature Requests & Roadmap Signals
The following **enhancements** were filed today, most of which are likely candidates for the upcoming v0.7.7 or v0.8.0 releases:

- [#6345](https://github.com/zeroclaw-labs/zeroclaw/issues/6345) – **Per‑channel reply‑min‑interval‑secs** (throttle outbound agent replies) – accepted for v0.7.7.
- [#6346](https://github.com/zeroclaw-labs/zeroclaw/issues/6346) – **Node CLI + dashboard health & management** (multi‑machine node foundation).
- [#6344](https://github.com/zeroclaw-labs/zeroclaw/issues/6344) – **Dashboard editor for workspace persona files** (`SOUL.md`, `IDENTITY.md`, etc.) – accepted.
- [#6343](https://github.com/zeroclaw-labs/zeroclaw/issues/6343) – **v0.7.7 track: Desktop app (Tauri) parity** – a large tracked issue covering menu bar, macOS accessibility, signed `.dmg`, auto‑updates, and universal binary.
- [#6342](https://github.com/zeroclaw-labs/zeroclaw/issues/6342) – **`install.sh --desktop` flag** for macOS menu‑bar app installation.
- [#6341](https://github.com/zeroclaw-labs/zeroclaw/issues/6341) – **Signed .dmg release asset** for macOS (blocked by #6338).
- [#6339](https://github.com/zeroclaw-labs/zeroclaw/issues/6339) – **Universal binary (arm64 + x86_64)** for macOS desktop app.
- [#6338](https://github.com/zeroclaw-labs/zeroclaw/issues/6338) – **macOS notarization + code‑signing pipeline** – blocks all distribution.
- [#6337](https://github.com/zeroclaw-labs/zeroclaw/issues/6337) – **Reduced‑motion and Increase‑Contrast** accessibility support.
- [#6336](https://github.com/zeroclaw-labs/zeroclaw/issues/6336) – **VoiceOver / NSAccessibility audit** of menu‑bar chat panel.
- [#6335](https://github.com/zeroclaw-labs/zeroclaw/issues/6335) – **macOS Microphone permission flow** for voice input.
- [#6334](https://github.com/zeroclaw-labs/zeroclaw/issues/6334) – **macOS Screen Recording permission flow** for screenshot‑to‑chat.
- [#6333](https://github.com/zeroclaw-labs/zeroclaw/issues/6333) – **macOS Accessibility (AX) permission flow**.
- [#6332](https://github.com/zeroclaw-labs/zeroclaw/issues/6332) – **Auto‑update channel** for desktop app (blocked by #6338).
- [#6273](https://github.com/zeroclaw-labs/zeroclaw/issues/6273) – **ModelProviderConfig typed‑family split and path field types** (part of schema v3).
- [#6272](https://github.com/zeroclaw-labs/zeroclaw/issues/6272) – **Agent filesystem layout** (`agents/<alias>/` directory + `AGENTS.md` migration).
- [#6271](https://github.com/zeroclaw-labs/zeroclaw/issues/6271) – **V3 SwarmConfig schema + runtime implementation**.
- [#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) – **zc_env_read allowlist** – restrict WASM plugin access to environment variables.
- [#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) – **SSRF protection for zc_http_request** host function.

**Prediction**: The majority of the macOS desktop features (#6332–#6343) will land in **v0.7.7**, while the schema v3 migration (#6271–#6273, #5947) is targeted for **v0.8.0**.

## User Feedback Summary
- **Pain Points**:
  - DeepSeek V4 multi‑turn conversations break after streaming fix (#6233).
  - WhatsApp Web issues: self‑chat mode sends unwanted replies to operator’s contacts (#6351) and `allowed-numbers` bypass for LID contacts (#6350) cause silent message drops.
  - Gemini tool‑call order validation errors (#6302) block multi‑turn tool use.
  - Empty `tool_calls` array rejection (#6298) affects all strict providers.
  - Dashboard and desktop chat UIs show tool calls as inline chat bubbles (#6348, #6349), cluttering the conversation.
- **Satisfaction Signals**: No explicit praise or thanks reported today, but the high number of merged PRs (19) indicates active maintenance and community contributions being accepted.

## Backlog Watch
Issues and PRs that have been awaiting action for an extended period:

- [#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) – `zc_env_read` allowlist (opened Apr 19, status `in‑progress` and `no‑stale`). No PR linked; needs maintainer review.
- [#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) – SSRF protection for `zc_http_request` (opened Apr 19, status `in‑progress` and `no‑stale`). No PR linked.
- [#5372](https://github.com/zeroclaw-labs/zeroclaw/pull/5372) – `fix(gateway): truncate oversized memory api payloads` (opened Apr 6, still open with `needs‑author‑action`). Waiting on author response.
- [#5161](https://github.com/zeroclaw-labs/zeroclaw/pull/5161) – `fix(gateway): keep websocket steering additive...` (opened Apr 1, still open with `needs‑author‑action`). Critical WebSocket stability improvement stuck in review.
- [#5770](https://github.com/zeroclaw-labs/zeroclaw/pull/5770) – `fix: use SqliteSessionBackend for session tools` (opened Apr 15, `needs‑author‑action`). Addresses session persistence mismatch.

**Maintainer attention recommended** for #5919 and #5918 (security hardening for WASM plugins) and #5372 (memory payload handling) which affect dashboard usability.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*