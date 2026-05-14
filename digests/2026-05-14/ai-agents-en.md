# OpenClaw Ecosystem Digest 2026-05-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-14 09:39 UTC

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

# OpenClaw Project Digest — 2026-05-14

## Today's Overview
OpenClaw saw very high activity today: **500 issues** and **500 pull requests** were updated in the last 24 hours, with **220 issues closed** and **59 PRs merged/closed**. Two beta releases were shipped (`v2026.5.12-beta.5` and `beta.6`) with targeted fixes for iMessage media, gateway protocol compliance, and session creation. Despite the fast pace, critical regressions remain unresolved—particularly around the Windows chat UI and MCP tool injection—and the community is actively discussing the long‑term runtime migration to Codex.

## Releases
Two beta versions were published today:

- **v2026.5.12-beta.6** ([release](https://github.com/openclaw/openclaw/releases/tag/v2026.5.12-beta.6))
  - **Fix (iMessage):** Stop sending visible `<media:image>` placeholder text for media‑only native image sends while preserving the internal echo key that prevents self‑echo duplicate replies. (#81209, thanks @homer‑byte)
  - **Fix (Agents/sessions):** Create configured agent main sessions before the first session request, preventing race conditions in session initialization.

- **v2026.5.12-beta.5** ([release](https://github.com/openclaw/openclaw/releases/tag/v2026.5.12-beta.5))
  - **Fix (gateway):** Pass Talk session scope to the AI resolver. (#81379, thanks @pgondhi987)
  - **Fix (gateway protocol):** Require v4 clients to stream explicit `deltaText`/`replace` frames so SDK clients can consume assistant updates without local diffing. (#80725, thanks @samzong)
  - **Fix (GitHub Copilot):** (description truncated in source data)

No breaking changes or migration notes were mentioned; these are cumulative fixes on the beta channel.

## Project Progress
Today’s **59 merged/closed PRs** include several notable improvements:

- **Brave search fallback** — `fix(web): keep legacy Brave search fallback provider-owned` ([#81744](https://github.com/openclaw/openclaw/pull/81744)) ensures doctor migration remains the canonical repair path.
- **Gateway test coverage** — `test(gateway): cover TUI paired token recovery` ([#80742](https://github.com/openclaw/openclaw/pull/80742)) adds integration tests for re‑issuing operator tokens without creating spurious scope‑upgrade requests.
- **i18n tooling** — `[Feat] Add Control UI i18n baseline report` ([#81320](https://github.com/openclaw/openclaw/pull/81320)) gives contributors a concise command to read translation baselines and prioritize work.
- **Session‑isolated app‑server clients** (new open PR) — `[codex] support session-isolated app-server clients` ([#81777](https://github.com/openclaw/openclaw/pull/81777)) is a large PR that adds `appServer.clientIsolation=session` for Codex, isolating run attempts, queued follow‑ups, and compaction per session.

Additionally, infrastructure work continues: memoization of skill snapshots ([#81451](https://github.com/openclaw/openclaw/pull/81451)), CJK‑aware tokenization for memory deduplication ([#80620](https://github.com/openclaw/openclaw/pull/80620)), and a `before_model_call` preflight hook ([#77256](https://github.com/openclaw/openclaw/pull/77256)) were all advanced today.

## Community Hot Topics
The most active issues (by comment count) reveal several pain points:

1. **[#67035](https://github.com/openclaw/openclaw/issues/67035)** — *Windows chat UI regression* (13 comments) — input text swallowed, streamed replies invisible until refresh, typing indicator flashes then blanks. Users report this makes the web dashboard unusable on Windows.
2. **[#80171](https://github.com/openclaw/openclaw/issues/80171)** — *Codex‑vs‑Pi runtime parity QA harness* (12 comments, 1 👍) — An RFC and tracking issue for ensuring feature parity as OpenClaw moves to Codex as the default runtime. The community is eager for structured testing.
3. **[#68449](https://github.com/openclaw/openclaw/issues/68449)** — *Dreaming plugin stopword list too narrow* (11 comments, 2 👍) — Tokenization artifacts surface as top themes; no filter for cron‑triggered sessions.
4. **[#51857](https://github.com/openclaw/openclaw/issues/51857)** — *Blind Spot Problem* (8 comments) — Media and vision failures where the agent reports success but silently operates on incorrect input (e.g., wrong image model or file).
5. **[#46080](https://github.com/openclaw/openclaw/issues/46080)** — *Anthropic tool_result succeeds but assistant content empty* (7 comments, 3 👍) — Final assistant turn persisted with `content: []` and `stopReason: “stop”`, showing “No reply from agent” to the user.

Underlying needs: users are frustrated by silent failures (false‑positive tool execution, missing UI feedback) and demand better diagnostics, configurable limits, and reliability for multi‑channel deployments.

## Bugs & Stability
Reported bugs ranked by severity:

### 🔴 Critical
- **OOM crash** (`#51264` — *loadCombinedSessionStoreForGateway loads all agent session stores simultaneously*) — Crashes the gateway when hook dispatch triggers eager loading of all agent sessions. No fix PR yet.
- **TUI Fatal Deadlock** (`#75844` — *regression in 2026.4.29*) — The terminal UI deadlocks, blocking all interaction. No fix PR identified.

### 🟠 High
- **Windows chat UI regression** (`#67035` — 13 comments) — No fix PR, remains open.
- **MCP server tools missing from agent request body** (`#76063` — still present despite claimed fix in v2026.4.27). Dangerous silent confabulation.
- **Discord gateway READY event never fires** (`#79794` — regression in 2026.5.7) — Bot online but guild messages not received. No fix PR.
- **Matrix channel missing `matrix-js-sdk`** (`#77896`) — Crash‑loop after npm update. No fix PR.
- **Slack channel final replies silently dropped** (`#77320` — 3 👍) — Agent emits `[thinking,text]` only, no tool result, with `visibleReplies="message_tool"`.
- **WhatsApp group auto‑reply silently suppressed** (`#80669` — 2 👍) — Agent generates reply but it’s never delivered.
- **Gateway duplicate stdio MCP children** (`#75621` — 2 👍) — Memory/CPU leak, double processes for same config.
- **Session lane queue has no task‑level timeout** (`#48488`) — Hung promises permanently block lanes. No fix PR.
- **Scope upgrade pending approval blocks all browser CLI commands** (`#81555`) — No approval UI visible. No fix PR.
- **Native hook relay remains stuck after restart** (`#73723`) — Codex native tool execution blocked. No fix PR.

### 🟡 Medium
- **Markdown tables split across streamed messages** (`#66614`), **overflow recovery duplicates user messages** (`#66443`), **aborted agent run emits garbage content** (`#48241`), **WebChat fails to render some messages** (`#77136` — 2 👍), **Matrix thread session key case‑normalization** (`#75670`), **buildExecEventPrompt race** (`#75322`).

Several high‑priority bugs have **no linked fix PR** today, indicating they may be under investigation or blocked.

## Feature Requests & Roadmap Signals
Active feature requests that are likely to shape the next releases:

- **[#66944](https://github.com/openclaw/openclaw/issues/66944)** — *Plugin UI Extension System* (7 comments, 3 👍) — Allow plugins to contribute native Lit‑based pages to the Control UI. High demand, design already proposed.
- **[#67000](https://github.com/openclaw/openclaw/issues/67000)** — *Warm‑up / session reuse for embedded agents* — Cold start on every invocation is a major bottleneck; a warm‑up cache could cut latency by 80% for active‑memory workflows.
- **[#77202](https://github.com/openclaw/openclaw/issues/77202)** — *Signal channel: live tool‑call progress* — An edit‑free send‑and‑delete pattern to close the silence gap on Signal.
- **[#76952](https://github.com/openclaw/openclaw/issues/76952)** — *Realtime Talk docs and mobile/phone bridge* — Users love low‑latency voice but need documentation and practical mobile usage.

Predictions for the next minor release:
- Plugin UI extensions (already gaining traction in PR discussions)
- Codex runtime parity harness (tracking issue #80171 is active)
- Performance improvements (skill cache, metadata memoization, CJK tokenization)
- Session‑isolated app‑server clients (large PR #81777) could land if reviewed quickly.

## User Feedback Summary
**Positive signals:** The Realtime Talk feature is described as “genuinely useful and low‑latency” (#76952). The community appreciates the rapid pace of beta fixes for iMessage and gateway protocol.

**Pain points (multiple reports):**
- **Windows experience is broken** — #67035, #72922 (Windows Server sluggish), #75844 (TUI deadlock on WSL2). Windows users feel abandoned.
- **Silent failures are the #1 complaint** — #46080, #76063, #77320, #80669 all describe cases where the agent *appears* to succeed but delivers nothing or wrong content. Trust in the system is eroding.
- **Channel reliability** — Discord, WhatsApp, Telegram, Matrix each have regressions that block basic usage. Users running multi‑channel setups face constant workarounds.
- **Slow bootstrap** — #77532 (3–5 minutes per turn on clean install) is a barrier for new users.
- **OAuth token refresh** — #77467 (MiniMax Portal) forces manual re‑auth every two hours.

## Backlog Watch
Issues and PRs that remain open for extended periods without maintainer resolution:

- **[#46080](https://github.com/openclaw/openclaw/issues/46080)** (March 14) — Anthropic tool_result empty reply. 3 👍, 7 comments, no progress in 2 months.
- **[#48488](https://github.com/openclaw/openclaw/issues/48488)** (March 16) — Lane queue no timeout. 5 comments, no progress.
- **[#51857](https://github.com/openclaw/openclaw/issues/51857)** (March 21) — Blind Spot / vision failures. 8 comments, no linked PR.
- **[#66399](https://github.com/openclaw/openclaw/issues/66399)** (April 14) — Process supervisor: graceful signal escalation. 5 comments, no fix.
- **[#66561](https://github.com/openclaw/openclaw/issues/66561)** (April 14) — Codex SSE stream abort → timeout. 5 comments, no fix.
- **[#67035](https://github.com/openclaw/openclaw/issues/67035)** (April 15) — Windows chat UI regression. **13 comments** — highest engagement of any open issue, yet no maintainer response or fix PR.
- **[#75621](https://github.com/openclaw/openclaw/issues/75621)** (May 1) — Duplicate MCP children leak. 2 👍, 5 comments, no fix.
- **[#79794](https://github.com/openclaw/openclaw/issues/79794)** (May 9) — Discord READY event not firing. 6 comments, 1 👍, no fix.

These issues represent clear gaps in reliability and UX that, if left unaddressed, risk eroding user trust in the project’s stability. The high‑activity levels today show the team is moving fast, but the backlog of critical bugs requires prioritization.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent Open-Source Ecosystem

## 1. Ecosystem Overview

The personal AI assistant open-source landscape on 2026-05-14 shows an ecosystem in rapid flux, with **OpenClaw as the dominant reference implementation** commanding overwhelming activity (500 issues/500 PRs daily), while a long tail of specialized projects pursue differentiated niches. The ecosystem is experiencing a **split between production-reliability pressures** (silent failures, channel regressions, credential management) and **architectural modernization** (runtime unification, multi-agent support, skill ecosystems). Community feedback converges on three pain points: silent failures eroding trust, Windows/desktop neglect, and configuration fragility across upgrades. The projects collectively signal an industry moving from proof-of-concept to mission-critical deployment, with corresponding demands for security, observability, and deterministic behavior.

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed (24h) | Release Today | Health Score | Dominant Activity Type |
|---------|-------------|-----------|---------------------|---------------|--------------|----------------------|
| **OpenClaw** | 500 updated (220 closed) | 500 updated | 59 | ✅ v2 betas | ⚠️ Strong but strained | Bug fixes + runtime migration |
| **ZeroClaw** | 41 (16 closed) | 50 (16 merged) | 16 | ❌ | ✅ High momentum | Multi-agent + skills ecosystem |
| **Hermes Agent** | 50 | 50 | 3 | ❌ | ⚠️ High activity, unresolved critical bugs | Platform adapter fixes |
| **CoPaw** | 50 (10 closed) | 50 (12 merged) | 12 | ✅ v1.1.7 + beta | ✅ Stable, responsive | Plugin/system fixes |
| **NanoBot** | 14 (10 closed) | 19 (4 merged) | 4 | ❌ | ✅ Growing steadily | Model routing + failover |
| **PicoClaw** | 8 | 42 (27 merged) | 27 | ✅ Nightly | ⚠️ Fast but unstable | Provider support + streaming |
| **NanoClaw** | 9 (1 closed) | 18 (15 merged) | 15 | ❌ | ✅ Focused feature push | Skill localization |
| **IronClaw** | 22 | 50 | 12 | ❌ | ⚠️ High-velocity re-architecture | Reborn migration + docs |
| **LobsterAI** | 1 | 26 (26 merged) | 26 | ❌ | ✅ Backlog cleanup completed | Bug fixes + security scan |
| **Moltis** | 1 | 0 | 0 | ❌ | ❌ Stalled | (none) |
| **NullClaw** | 1 | 0 | 0 | ❌ | ❌ Low activity | (single feature request) |
| **ZeptoClaw** | 2 (2 closed) | 0 | 0 | ❌ | ✅ Stable, dormant | Documentation |
| **TinyClaw** | 0 | 0 | 0 | ❌ | ❌ Inactive | No activity |

**Health scoring methodology**: weighted combination of issue/PR volume, closure rate, backlog severity, and community engagement. Projects with critical unfixed bugs affecting core functionality are downgraded (OpenClaw, Hermes, PicoClaw).

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Ecosystem primacy**: 10x the daily activity of the next busiest project. 500 issues + 500 PRs dwarfs ZeroClaw (41/50) and Hermes (50/50).
- **Cross-channel coverage**: iMessage, Discord, Slack, Matrix, WhatsApp, Signal – most comprehensive channel matrix in the ecosystem.
- **Reference implementation status**: The `OpenClaw` name serves as the de facto standard; other projects (PicoClaw, NanoClaw, NullClaw, ZeroClaw) explicitly fork or draw inspiration from its architecture.
- **Release cadence**: Two beta releases in 24 hours demonstrates rapid iteration capability.

**Technical approach differences:**
- **Runtime migration**: OpenClaw is uniquely executing a **Codex-to-Pi runtime transition** (tracking issue #80171), a foundational re-architecture that no peer has attempted at this scale. This creates both opportunity (unified runtime) and risk (regressions, compatibility breaks).
- **Session isolation model**: PR #81777 introduces `session-isolated app-server clients` – a pattern ZeroClaw is only now exploring for v0.8.0.
- **Gateway protocol**: OpenClaw enforces structured streaming (`deltaText`/`replace` frames for gateway v4), a standardization effort absent in peers who rely on ad-hoc diffing.

**Community size comparison:**
- **Issue engagement**: OpenClaw's #67035 (Windows chat UI) has 13 comments with zero maintainer response – the same issue has higher engagement than any single issue in NanoBot, PicoClaw, or NanoClaw.
- **PR authorship**: OpenClaw has 59 merged/closed PRs vs ZeroClaw's 16 and CoPaw's 12, indicating a larger contributor base.
- **Risk**: The backlog of critical bugs (OOM #51264, TUI deadlock #75844) with no fix PRs, plus the 2-month-old #46080 (empty Anthropic replies), suggests velocity may be outpacing quality assurance.

## 4. Shared Technical Focus Areas

Requirements emerging independently across multiple projects:

| Need | Projects Affected | Specific Pain Points |
|------|------------------|---------------------|
| **Silent failure detection** | OpenClaw (#46080, #76063), Hermes (#15886), PicoClaw (auth 401), CoPaw (#4300) | False-positive tool execution, empty replies, dropped messages without error |
| **Windows/desktop parity** | OpenClaw (#67035, #72922), Hermes (#25551, #25514), NanoBot (#3780), LobsterAI (#1973) | Broken chat UI, console crashes, sandbox limitations, garbled localization |
| **Streaming reliability** | Hermes (#15886), PicoClaw (#1950, #2404), OpenClaw (gateway protocol), CoPaw (#4318) | Stalled mid-tool-call, diffing failures, incomplete delivery |
| **Channel-specific regressions** | OpenClaw (Discord, WhatsApp, Slack), Hermes (Matrix, QQBot, Slack), PicoClaw (Telegram), NanoBot (Feishu), ZeroClaw (Matrix, Nextcloud Talk) | Each project has 1-2 channels actively broken at any time |
| **Model/provider compatibility** | NanoBot (DeepSeek V4), PicoClaw (DeepSeek reasoning), CoPaw (Volcano Engine, MiMo), ZeroClaw (Anthropic Opus, GLM-5.1), Hermes (Cloudflare WAF) | Reasoning content dropped, 400 errors on thinking mode, temperature serialization |
| **Security/access control** | NanoBot (#3780), ZeroClaw (#6613), LobsterAI (#842), Hermes (#22620), PicoClaw (#2688) | File access granularity, sandbox escapes, credential isolation, script auditing |
| **Observability/tracing** | ZeroClaw (#6641, #6642), NanoClaw (#2456 LangFuse), LobsterAI (#842 security scan) | Turn-level tracing, LLM call spans, security audit trails |
| **Context management** | Hermes (#22620 skill bloat), LobsterAI (#866 lost-in-middle), CoPaw (#3944 auto-memory), ZeroClaw (#6269 reasoning dropped) | Token waste on irrelevant skills, memory clutter from system sessions |

**Critical pattern**: **Silent failures** are the most cross-cutting concern – they appear in OpenClaw, Hermes, PicoClaw, and CoPaw simultaneously, indicating a systemic trust issue with agent reliability.

## 5. Differentiation Analysis

| Project | Primary Differentiator | Target User | Unique Architectural Choice |
|---------|----------------------|-------------|----------------------------|
| **OpenClaw** | Ecosystem authority + broadest channel support | Power users, multi-channel deployers | Codex→Pi runtime migration; gateway protocol standardization |
| **ZeroClaw** | Multi-agent runtime + skills ecosystem | Teams building agent swarms | v0.8.0 dedicated to agent-orchestrated workflows; skills marketplace ambition |
| **Hermes Agent** | Platform adapter breadth (QQBot, Matrix, Feishu, Discord, Slack) | Multi-platform operators | Strongest China-region provider support; long-term assistant memory features |
| **NanoBot** | Model failover + routing maturity | Production reliability engineers | `fallback_models` and hook-based routing; lightweight core |
| **PicoClaw** | Low-power device optimization | Raspberry Pi / edge deployers | Automated nightly builds; minimal resource footprint; WhatsApp on-arm |
| **NanoClaw** | Enterprise skill localization | Marketing/operations teams | Skills as first-class primitives (LinkedIn, Reddit, Serper); LangFuse observability |
| **CoPaw** | Browser automation + desktop app | End-users wanting rich UI | Tauri desktop app; batch browser actions; Telegram streaming |
| **IronClaw** | Reborn architecture migration | Architectural decision-makers | WASM component runtime; product adapter registry; sealed handoff stores |
| **LobsterAI** | Plugin system + security scanning | Security-conscious enterprises | UserData plugin isolation; offline whisper; security environment scanning |
| **NullClaw** | Minimalist / specialist | (Inactive – single JIRA tool request) | No identifiable architectural distinction |
| **Moltis** | Decentralized relay infrastructure | Privacy-focused users | Trustless relay channel proposal (portal-tunnel) |
| **ZeptoClaw** | Security advisory documentation | Compliance teams | CVE/GHSA tracking focus; otherwise dormant |
| **TinyClaw** | (Inactive) | (None) | No activity |

**Key insight**: The ecosystem is **not competing on core LLM agent capabilities** – all projects support similar Chat SDK, MCP tools, and provider integrations. Differentiation happens through **deployment environment** (edge, desktop, enterprise), **architectural philosophy** (monolith vs. composable runtime), and **channel coverage breadth**.

## 6. Community Momentum & Maturity

**Tier 1 – Rapidly iterating (very high activity, architectural changes in flight)**
- **OpenClaw**: 500+ daily issues/PRs, but critical bug backlog risks quality collapse. Moving fastest but also most fragile.
- **ZeroClaw**: Strong momentum with v0.7.6 skills push and v0.8.0 multi-agent. 16 PRs merged/day, responsive maintainers.
- **CoPaw**: 12 PRs merged/day, two releases in 24h. Most balanced velocity-to-quality ratio among top projects.
- **Hermes Agent**: High raw numbers but only 3 PRs merged – heavy discussion volume with less throughput.

**Tier 2 – Stabilizing (high activity, fewer architectural risks)**
- **NanoBot**: 4 PRs merged, all valuable (failover, routing, crash fix). Growing contributor base, clean backlog.
- **PicoClaw**: 27 PRs merged but nightly build dependency. Unstable auth blocks all users – fixing this is prerequisite to maturity.
- **NanoClaw**: 15 PRs merged, focused skill localization. Low bug count, clean trajectory.
- **LobsterAI**: 26 PRs merged in backlog cleanup. Now manageable; active bug remains on virtual scrolling.

**Tier 3 – High risk / transitional** 
- **IronClaw**: Massive architectural re-architecture (Reborn) creates high activity but daily regressions (TEE failure, Telegram setup). Pain before payoff.
- **PicoClaw**: Auth failure (#2769) is a showstopper for all users. Until fixed, nightly builds are untrustworthy.

**Tier 4 – Low activity / stalled**
- **NullClaw**: Single issue in 24h. No PRs. Potentially abandoned.
- **Moltis**: Single issue in 24h. No PRs. Development appears paused.
- **ZeptoClaw**: Documentation-only. Functionally dormant.
- **TinyClaw**: Zero activity. Effectively archived.

**Maturity assessment**: The ecosystem has **no project that is both high-velocity and low-regression** – OpenClaw and Hermes ship features but accumulate bugs; NanoBot and CoPaw are stable but slower. ZeroClaw shows the best balance of velocity and reliability.

## 7. Trend Signals

**Industry trends extracted from community feedback:**

1. **The trust crisis in agent output**: Silent failures (empty replies, false-positive tool execution, dropped messages) are the #1 cross-project complaint. This reflects an industry maturing from "can it do it" to "can I trust it did it correctly." Expect **deterministic execution tracking** and **confirmation loops** to become table stakes.

2. **Channel reliability as a competitive moat**: Multi-channel deployment is the dominant use case, yet every project has 1-2 broken channels at any time. The winner will invest in **channel-specific integration testing** and **automatic failover across channels**.

3. **Enterprise adoption drives security demands**: File access controls, credential isolation, script auditing, and OTel observability requests all came from users using agents in shared/regulated environments. **Sandboxing and audit trails** will differentiate production-ready projects from hobbyist tools.

4. **Windows neglect is a market opportunity**: OpenClaw (#67035, 13 comments), Hermes (#25551, install failure), LobsterAI (#1973, Chinese encoding) – Windows users are vocal and underserved. A project that delivers a **first-class Windows desktop experience** could capture significant mindshare.

5. **The runtime unification wave**: OpenClaw (Codex→Pi), IronClaw (Reborn), ZeroClaw (v0.8.0 multi-agent) – three major projects are simultaneously rewriting their core runtimes. This suggests the community recognizes the **limitations of monolithic SDK APIs** and is converging on **pluggable, composable runtime architectures** as the next generation.

6. **Model-specific reasoning handling is a growing pain point**: DeepSeek V4's `reasoning_content`, Anthropic Opus temperature constraints, GLM-5.1 thought merging – each new model release breaks existing abstraction layers. The industry needs **model-agnostic reasoning/content separators** – expect this to become a focus for OpenClaw's gateway protocol and ZeroClaw's provider abstraction.

7. **Skill/memory optimization for cost control**: Hermes (#22620 skill bloat), CoPaw (#3944 auto-memory filter), ZeroClaw (#6269 reasoning drop from compression) – users are hitting token limits and API costs. **Intelligent skill routing, lazy loading, and hierarchical memory** will differentiate mature projects.

**Value for AI agent developers**: The data suggests developers should (a) prioritize **failure detectability** over feature velocity, (b) choose projects with **dedicated channel testing** over those with broad but broken coverage, and (c) prepare for **runtime architecture migrations** as the industry standardizes on composable, pluggable designs.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-14

## 1. Today’s Overview
NanoBot saw high activity over the last 24 hours, with 14 issues updated (10 closed) and 19 PRs updated (4 merged/closed). The project continues to mature, focusing on production‑readiness: model failover and routing features have been merged, along with critical bug fixes for MCP connection crashes and Feishu channel errors. Several new CLI diagnostics and session management PRs are under review, indicating a push toward better developer experience. Community engagement remains strong, with users actively reporting bugs and requesting security enhancements for shared deployments.

## 2. Releases
No new releases were published today.

## 3. Project Progress
Four pull requests were merged or closed today, advancing key features and stability:

- **Model Routing via Hooks** ([PR #3121](https://github.com/HKUDS/nanobot/pull/3121)) — Merged. Adds a `model` field to `AgentHookContext`, enabling users to implement custom model routing logic without modifying core code. Addresses issue [#3070](https://github.com/HKUDS/nanobot/issues/3070).
- **Model Failover with `fallback_models`** ([PR #3756](https://github.com/HKUDS/nanobot/pull/3756)) — Merged. Adds `fallback_models` to `ModelPresetConfig`, allowing automatic fallback to alternate models/providers when the primary fails. Resolves issue [#3376](https://github.com/HKUDS/nanobot/issues/3376).
- **MCP Connection Crash Fix** ([PR #3740](https://github.com/HKUDS/nanobot/pull/3740)) — Merged. Adds a lightweight TCP probe before connecting to HTTP/SSE MCP servers, preventing event‑loop crashes when the service is unreachable.
- **Combined CLI/Slash Command PR** ([PR #3773](https://github.com/HKUDS/nanobot/pull/3773)) — Closed (superseded). Its features (`doctor`, session management, `/export`) are now split into individual open PRs (#3776, #3777, #3778).

## 4. Community Hot Topics
The most active discussions highlight reliability and security concerns:

- **#2880 – “无论发什么消息都回复报错”** ([Issue](https://github.com/HKUDS/nanobot/issues/2880))  
  17 comments. A persistent bug where the agent always replies with an error, regardless of input. User reports reinstallation doesn’t help; the issue is marked `stale` but remains open. Underlying need: a root‑cause fix for a critical user‑facing failure.
- **#3376 – “支持模型异常自动切换”** ([Issue](https://github.com/HKUDS/nanobot/issues/3376))  
  13 comments. Now resolved by PR #3756, this was the top‑voted feature request. Users managing multiple providers wanted automatic failover on timeouts, 429s, and 5xx errors.
- **#3780 – “支持更安全的文件访问控制与脚本审查”** ([Issue](https://github.com/HKUDS/nanobot/issues/3780))  
  3 comments. A company using NanoBot on Windows without sandbox asks for granular read permissions and script auditing. Reflects growing enterprise interest in secure shared deployments.
- **#3070 – “模型路由”** ([Issue](https://github.com/HKUDS/nanobot/issues/3070))  
  3 comments. Now implemented via PR #3121. Users wanted cost‑effective model selection based on task complexity.

## 5. Bugs & Stability
Several bugs were reported or escalated today, ordered by severity:

| Issue | Description | Severity | Fix Status |
|-------|-------------|----------|------------|
| [#3772](https://github.com/HKUDS/nanobot/issues/3772) | Feishu group bot crashes when other bots are @mentioned (`processor not found`) | **High** – blocks Feishu usage with multi‑bot groups | Fix in PR [#3775](https://github.com/HKUDS/nanobot/pull/3775) (no‑op handlers registered) |
| [#3760](https://github.com/HKUDS/nanobot/issues/3760) | DeepSeek V4 Flash returns 400 error due to `reasoning_content` in thinking mode | **High** – breaks a popular model combination | No open fix yet; workaround may require mode configuration |
| [#3754](https://github.com/HKUDS/nanobot/issues/3754) | DeepSeek V4 Flash ignores `read_file` tool and fabricates content for small files | **Medium** – affects data‑analysis workflows | No fix PR; may be model‑specific |
| [#3739](https://github.com/HKUDS/nanobot/issues/3739) | Agent startup crash when MCP service is not running | **Medium** – affects users who enable MCP without running services | Fixed in PR [#3740](https://github.com/HKUDS/nanobot/pull/3740) (merged) |
| [#2880](https://github.com/HKUDS/nanobot/issues/2880) | Agent always replies with error (stale, open since April 7) | **High** – impacts core functionality | No resolution yet |

Additional stability improvements: PR [#3762](https://github.com/HKUDS/nanobot/pull/3762) (retry blank Codex failures) and PR [#3235](https://github.com/HKUDS/nanobot/pull/3235) (fail‑closed on DNS failure in URL validation) remain open.

## 6. Feature Requests & Roadmap Signals
Today’s activity points to several likely roadmap items:

- **CLI Diagnostic Tool** – `nanobot doctor` ([PR #3776](https://github.com/HKUDS/nanobot/pull/3776)) and `nanobot sessions` management ([PR #3777](https://github.com/HKUDS/nanobot/pull/3777)) are in review. These will greatly improve debugging for operators.
- **DM Sender Approval** – Issue [#3768](https://github.com/HKUDS/nanobot/issues/3768) proposes a pairing/allowlist system for private messages. PR [#3774](https://github.com/HKUDS/nanobot/pull/3774) (chat‑native pairing) directly addresses this, indicating strong maintainer interest.
- **Security Access Controls** – Issue [#3780](https://github.com/HKUDS/nanobot/issues/3780) requests file access granularity and script auditing on Windows. Given the enterprise use case, this may land in an upcoming minor release.
- **Long‑Task Tool** – PR [#3460](https://github.com/HKUDS/nanobot/pull/3460) (multi‑step agent tasks) has been open since April 26. Its size and complexity may delay merging, but it signals interest in handling long‑running workflows.

## 7. User Feedback Summary
Real‑world user experiences from today’s data:

- **Positive**: Community contributions are strong — multiple first‑time PR authors submitted well‑structured features (doctor, session export, Telegram access controls). The merged model failover and routing features directly address top‑voted requests, demonstrating responsive maintainership.
- **Pain Points**:
  - Windows users face sandbox limitations and file access issues when sharing NanoBot across a team.
  - DeepSeek V4 Flash users report both compatibility bugs (thinking mode) and unreliable file reading — a known model‐specific pain that may require workarounds.
  - Feishu channel integration is brittle when other bots are present, blocking adoption in multi‑bot chat environments.
  - The stale bug #2880 (always‑error replies) remains unresolved for over a month, eroding trust for affected users.

## 8. Backlog Watch
The following important items lack maintainer resolution or remain open for extended periods:

- **Issue [#2880](https://github.com/HKUDS/nanobot/issues/2880)** – Error‑on‑every‑message bug (since April 7, 17 comments, marked `stale`). Needs maintainer diagnosis and fix.
- **Issue [#1998](https://github.com/HKUDS/nanobot/issues/1998)** – Coder‑model compatibility with GLM‑5, Qwen‑3.5 (since March 14, still open). Relevant as more code‑oriented models gain popularity.
- **Issue [#3768](https://github.com/HKUDS/nanobot/issues/3768)** – DM sender pairing (enhancement, no official response yet). PR #3774 exists but depends on other patches.
- **PR [#3235](https://github.com/HKUDS/nanobot/pull/3235)** – DNS fail‑closed security patch (since April 17). Important for SSRF protection but not yet merged.
- **PR [#3460](https://github.com/HKUDS/nanobot/pull/3460)** – Long‑task tool (since April 26). Large feature that may need more review time.

*All links are to the [HKUDS/nanobot repository](https://github.com/HKUDS/nanobot).*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent Project Digest – 2026-05-14

### 1. Today’s Overview
The project saw high activity with **50 issues and 50 PRs updated** in the last 24h, indicating a flurry of community engagement and contributor fixes. **3 PRs were merged/closed** (none in the top-20 list besides one). No new releases were published. The majority of discussion revolves around **stability improvements for credential management, streaming reliability, platform adapters (Discord, Slack, QQBot, Matrix), and Windows‑specific bugs**. Several **P1 severity bugs** were reported today, and multiple PRs address critical gaps in context compression, heartbeat handling, and voice/UI ergonomics.

### 2. Releases
**None** – No releases were published in the last reporting period.

### 3. Project Progress (Merged/Closed PRs)
Only **one merged/closed PR** appears among the top-20 PRs by comment count:

- **[PR #25500]** – `fix(cli): gracefully handle Windows console failures in _cprint (kanban fix)`  
  Resolves a crash on Windows when `prompt_toolkit` fails in background subprocesses (e.g., Kanban board).  
  URL: https://github.com/NousResearch/hermes-agent/pull/25500

The other two merged/closed PRs (from the 3 total) are not in the shown subset, but this fix alone demonstrates progress on Windows compatibility.

### 4. Community Hot Topics
The most discussed issues and PRs this period (highest comment count / reactions):

| Item | Title | Comments | 👍 | URL |
|------|-------|----------|----|-----|
| Issue #19566 | [Bug]: OpenAI-Codex credential pool can drop newly added credential after stale auth.json rewrite during rotation | 5 | 1 | https://github.com/NousResearch/hermes-agent/issues/19566 |
| Issue #9721  | [Bug]: Cannot set custom HTTP headers for custom providers — Cloudflare 403 | 5 | 0 | https://github.com/NousResearch/hermes-agent/issues/9721 |
| Issue #15886 | [Bug]: 长文档写入频繁触发 'Stream stalled mid tool-call' 错误 | 4 | 0 | https://github.com/NousResearch/hermes-agent/issues/15886 |
| Issue #22620 | [Feature]: Skill list bloat causes massive context window inflation — need vector-based skill routing or lazy loading | 3 | 0 | https://github.com/NousResearch/hermes-agent/issues/22620 |

**Underlying needs**:  
- **Credential rotation (#19566)** – Users running multiple Hermes processes need safe, race‑free credential management.  
- **Provider configurability (#9721)** – Self‑hosted or proxied OpenAI‑compatible endpoints require the ability to set arbitrary HTTP headers (e.g., User‑Agent).  
- **Streaming stability (#15886)** – Long file writes through the `write_file` tool hit timeout/stall errors, hurting reliability for large document editing.  
- **Context window optimisation (#22620)** – As skill sets grow, the agent wastes tokens on irrelevant skills; users want intelligent routing or lazy loading.

### 5. Bugs & Stability
All bug reports from the top‑30 issues, ranked by severity (P1 → P2 → P3). Fixed PRs are noted where relevant.

#### P1 Critical
- **[#25495]** – Matrix / synapse broken in official Docker image; last working commit sha‑1e01b25e. Logs stuck at “fixing ownership :1000”. No fix PR visible.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25495
- **[#25538]** – `context.max_history_depth` not enforced; history grows unbounded, causing token bloat and cost increases. PR #25588 may partially address related compression issues.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25538

#### P2 High
- **[#25551]** – Windows install fails on new Windows installations (script download/corruption issues).  
  URL: https://github.com/NousResearch/hermes-agent/issues/25551
- **[#25517]** – Kanban stale_lock reclaim when single MCP tool call exceeds 15‑minute TTL; no heartbeat possible during blocking call.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25517
- **[#25505]** – QQBot adapter silently dies after exhausting reconnect attempts; permanent offline until manual restart.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25505
- **[#25349]** – Discord streaming can duplicate final responses across chunked delivery (30‑second gap).  
  URL: https://github.com/NousResearch/hermes-agent/issues/25349
- **[#25476]** – Slack Socket Mode WebSocket silently drops without auto‑reconnect; no log at default WARNING level.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25476
- **[#25514]** – Windows terminal foreground commands return empty output due to `select.select()` failure on pipe fds.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25514
- **[#25568]** – Shift+Enter triggers send instead of newline in terminal UIs. PR #25586 (Cmd+Enter fix) may be related.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25568
- **[#9721]** – Custom provider HTTP headers not configurable, causing Cloudflare 403 blocks. (Open since April 14.)  
  URL: https://github.com/NousResearch/hermes-agent/issues/9721
- **[#19566]** – Credential pool drop during rotation (see Hot Topics).  
- **[#15886]** – Stream stalled mid tool‑call on long writes.

#### P3 Lower
- **[#25535]** – Kanban goals stuck in “Blocked” state; no automatic recovery.  
  URL: https://github.com/NousResearch/hermes-agent/issues/25535
- **[#25542]** – China‑region OAuth provider code exists but not exposed (feature request, not a bug).  
- **[#25544]** – Cross‑platform session sharing (WeChat vs Feishu) not supported.
- **[#25526]** – Memory bridge missing old_text metadata for external providers.
- **[#25527]** – Built‑in `memory` tool does not use external MemoryProvider as primary store.
- Plus several other P3 items (backup, voice, dashboard prefix).

**Notable fix PRs** (not yet merged):  
- PR #25591 – Aligns Kanban failure diagnostics with actual circuit‑breaker threshold (addresses #25517 partially).  
- PR #25588 – Prevents context compression from discarding turns on summary failure (may help #25538).  
- PR #25586 – Makes Cmd+Enter submit on macOS (related to #25568).  
- PR #25411 – Queues rapid text messages and fixes paste collapses (#4469, #17666).

### 6. Feature Requests & Roadmap Signals
The following feature requests represent the community’s most wanted capabilities and likely candidates for the next release:

| Issue | Title | Priority | URL |
|-------|-------|----------|-----|
| #22620 | Skill list bloat → vector‑based routing / lazy loading | P3 | https://github.com/NousResearch/hermes-agent/issues/22620 |
| #25542 | Add China‑region (minimax‑cn) OAuth provider | P3 | https://github.com/NousResearch/hermes-agent/issues/25542 |
| #25544 | Cross‑platform session sharing (WeChat ↔ Feishu) | P3 | https://github.com/NousResearch/hermes-agent/issues/25544 |
| #25526 | Memory bridge mirror with old_text metadata | P3 | https://github.com/NousResearch/hermes-agent/issues/25526 |
| #25527 | First‑class external MemoryProvider for built‑in memory tool | P3 | https://github.com/NousResearch/hermes-agent/issues/25527 |
| #25460 / #25600 / #25599 / #25598 / #25596 / #25595 | Series of backup/restore, memory consent/decay, and personal signal classifier features (by leo21052545) | P3 | Various (see top‑30 list) |

**Roadmap signals**:  
- The flood of **personal assistant features** (backup, memory classification, consent tracking) suggests a move toward **autonomous long‑term assistant usage** (L Butler use case).  
- **Skill routing** (#22620) and **cross‑platform session continuity** (#25544) indicate demand for scaling Hermes from single‑user to multi‑platform, high‑context scenarios.  
- Improvement to **voice mode** (PR #25582 – default voice mode via env var) shows increasing interest in voice‑first deployments.

### 7. User Feedback Summary
- **Pain points**:  
  - Credential drops during rotation (#19566) frustrate multi‑instance users.  
  - Startup/install failures on Windows (#25551) and loss of language/console support (#25568, #25514) degrade the Windows experience.  
  - Platform adapter instability (Matrix, QQBot, Slack, Discord) forces manual restarts.  
  - Context window inflation (#22620) increases API costs linearly.  
  - Inability to customise provider headers (#9721) blocks integration with common WAF/proxy setups.  

- **Satisfaction**:  
  - The community actively submits both bug reports and feature PRs, indicating high engagement.  
  - Quick handling of some P1 issues (e.g., PR #25500 for Windows console, PR #25588 for context compression) shows maintainers are responsive.  

- **Use cases**:  
  - Multi‑process credential rotation for OpenAI‑Codex.  
  - Self‑hosted proxies/gateways (Cloudflare).  
  - Long document editing (write_file >5KB).  
  - Voice‑first and multi‑platform deployments (Telegram, Feishu, Slack, Discord).  

### 8. Backlog Watch
Issues and PRs that have been open for an extended period without maintainer response or merge, and which are important to project health:

- **[Issue #9721]** – **Cannot set custom HTTP headers** (Open since April 14, P2). 5 comments but still no maintainer assignment or PR. Blocks many self‑hosted users.  
  URL: https://github.com/NousResearch/hermes-agent/issues/9721

- **[Issue #15886]** – **Stream stalled mid tool‑call** (Open since April 26, P2). 4 comments, several users affected. No PR linked.  
  URL: https://github.com/NousResearch/hermes-agent/issues/15886

- **[PR #18331]** – **fix(teams): route plain‑text replies via per‑conversation serviceUrl** (Open since May 1, no comments). Still awaiting review; may fix Microsoft Teams integration.  
  URL: https://github.com/NousResearch/hermes-agent/pull/18331

- **[PR #25202]** – **feat(feishu): CardKit v2 streaming cards** (Open since May 13, P2). Large enhancement for Feishu users, not yet merged.  
  URL: https://github.com/NousResearch/hermes-agent/pull/25202

These items represent **known community needs that have not received explicit maintainer attention** in the past few weeks.

---  

**Summary**: Hermes Agent is actively maintained with high community throughput, but several P1/P2 bugs (especially on Windows and platform adapters) and older feature requests require prioritisation. The influx of personal‑assistant features signals a strategic shift toward long‑lived, memory‑rich agent deployments.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-14

## 1. Today's Overview

The project saw **exceptionally high activity** in the past 24 hours, with 42 pull requests and 8 issues updated. Among the 27 merged/closed PRs, key bug fixes and feature additions landed, including a new Gemini web search provider, CLI gateway commands, and archival‑preserving session logic. A nightly build (`v0.2.8‑nightly.20260514.eb065307`) was released, incorporating the latest commits from `main`. Four issues remain open, with the most critical being a **cross‑provider authentication failure** (401) that currently affects stable and nightly builds. Overall, development velocity is very strong, but the project’s reliance on nightly builds for recent fixes means users may need to tolerate some instability.

## 2. Releases

| Version | Type | Changelog |
|---------|------|-----------|
| `v0.2.8-nightly.20260514.eb065307` | Nightly | Automated build comparing against `v0.2.8` ([Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)) |

**⚠️ Notes:** This is an automated nightly and may be unstable. No breaking changes or migration instructions were provided. Developers deploying to production should pin to a stable tag.

## 3. Project Progress

27 pull requests were merged or closed in the last 24 hours. Notable completed items:

- **New Provider** – [PR #2763](https://github.com/sipeed/picoclaw/pull/2763) (closed/merged): Added a Gemini Google Search provider for the `web_search` tool, using `generateContent` with grounding.
- **CLI Commands** – [PR #2383](https://github.com/sipeed/picoclaw/pull/2383) (closed/merged): Added `picoclaw gateway status` and `picoclaw gateway stop` commands.
- **Session / History** – [PR #2311](https://github.com/sipeed/picoclaw/pull/2311) (closed/merged): Preserved archived chat history after summarization truncation; web session endpoints now read the full JSONL archive.
- **Agent Loop Fixes** – [PR #2309](https://github.com/sipeed/picoclaw/pull/2309) (closed/merged): Normalized tool‑call history for strict providers, removing duplicate/stray tool messages.
- **Thinking Level** – [PR #2306](https://github.com/sipeed/picoclaw/pull/2306) (closed/merged): Correctly resolves `thinking_level` through model‑ref lookup (fixes #2286).
- **Telegram Fix** – [PR #2199](https://github.com/sipeed/picoclaw/pull/2199) (closed/merged): Keeps reply context without breaking `/` and `!` commands.
- **Multi‑user Group Chats** – [PR #2715](https://github.com/sipeed/picoclaw/pull/2715) (closed/merged): Attributes history messages per sender in group‑capable channels (Discord, Telegram, Slack).

These merged PRs represent substantial progress in provider support, CLI tooling, history management, and platform‑specific channel handling.

## 4. Community Hot Topics

The following issues and PRs attracted the most discussion and reactions:

- **[Issue #1950](https://github.com/sipeed/picoclaw/issues/1950) – Streaming Output for Web Chat** (8 comments, 0 👍)  
  *Enhancement request for real‑time streaming in the web UI. Labeled low‑priority but on the current roadmap.*
- **[Issue #2404](https://github.com/sipeed/picoclaw/issues/2404) – Configurable Streaming HTTP Requests** (6 comments, 1 👍)  
  *User wants a `"streaming": true` config flag, similar to the OpenAI Python client. Proposed solution straightforward.*
- **[Issue #2625](https://github.com/sipeed/picoclaw/issues/2625) – WhatsApp Support in Default Builds** (4 comments, 1 👍)  
  *Raspberry Pi Zero 2 user cannot easily update because the arm64 build lacks WhatsApp support; requests compilation flags.*
- **[Issue #2706](https://github.com/sipeed/picoclaw/issues/2706) – DeepSeek v4 Thinking Model** (3 comments, 1 👍, closed)  
  *Bug report (and fix) for `reasoning_content` not being preserved in streaming responses, causing 400 errors.*
- **[PR #2587](https://github.com/sipeed/picoclaw/pull/2587) – Full Streaming + Scroll UX for Web Chat** (open, 0 comments shown)  
  *Implements end‑to‑end streaming in the agent loop and rebuilds frontend rendering – directly addresses #1950 and #2404.*

**Underlying need:** The community is clearly pushing for **streaming capabilities** across channels (web, HTTP config, and provider inference). The DeepSeek discussion also highlights a desire for full provider compatibility without manual workarounds.

## 5. Bugs & Stability

| Bug | Severity | Status | Fix PR | Notes |
|-----|----------|--------|--------|-------|
| [Authentication failure across providers (401)](https://github.com/sipeed/picoclaw/issues/2769) | **Critical** – blocks all API calls | Open, updated May 13 | None seen | Affects stable and nightly builds; keys verified valid outside PicoClaw. |
| [Sandbox bypass via `find /` and `ls /`](https://github.com/sipeed/picoclaw/issues/2688) – related PR [PR #2693](https://github.com/sipeed/picoclaw/pull/2693) | **High** – security escape | Open PR | #2693 (blocks specific paths) | Fix pending review. |
| [MCP initialization failure causes zombie agent](https://github.com/sipeed/picoclaw/pull/2725) | **Medium** – agent stuck | Open PR | #2725 (makes init failure non‑fatal) | Under review. |
| [Transient LLM HTTP errors not retried](https://github.com/sipeed/picoclaw/pull/2768) | **Medium** – spurious failures | Open PR | #2768 (reuses error classifier) | Fix ready. |
| DeepSeek v4 reasoning content (Issue #2706) | **High** – 400 errors | **Closed** – fixed via [PR #2741](https://github.com/sipeed/picoclaw/pull/2741) | Merged? (still open) | PR #2741 parses `reasoning_content` in streaming. |
| DingTalk SDK panic (Issue #2704) | **Medium** – gateway crash | **Closed** – likely fixed by SDK patch | Not specified | 6 crashes logged; root cause is concurrency bug in upstream SDK. |

**Overall stability:** While many bugs are being closed quickly, the **authentication regression (#2769)** is a showstopper for all users. No fix PR has appeared yet, so users should expect continued issues until a patch lands.

## 6. Feature Requests & Roadmap Signals

- **Streaming (Web & Config):** Issues #1950 and #2404 are both tagged *on the current roadmap*. The large open PR [#2587](https://github.com/sipeed/picoclaw/pull/2587) (backed by contributor SiYue‑ZO) delivers web streaming and scroll UX; PR #2741 also improves streaming parsing. **Likely included in the next version.**
- **WhatsApp Builds:** Issue #2625 requests that the default arm64 build includes WhatsApp support. Low priority, but the maintainer may add compilation flags soon.
- **New Tools:** Several feature PRs were submitted (still open):
  - **Image generation** ([PR #2760](https://github.com/sipeed/picoclaw/pull/2760)) – disabled by default, provider‑agnostic.
  - **update_plan tool** ([PR #2765](https://github.com/sipeed/picoclaw/pull/2765)) – for multi‑step progress tracking.
  - **get_current_time tool** ([PR #2691](https://github.com/sipeed/picoclaw/pull/2691)) – timezone‑aware.
- **OpenCode Support:** Issue #2671 was closed (stale) without clear resolution; unlikely to land soon.
- **Config V3 Documentation:** [PR #2766](https://github.com/sipeed/picoclaw/pull/2766) syncs all docs to the V3 config format (array `api_keys`, `channel_list`, etc.). This indicates the V3 schema is stabilizing and will be the default in the next stable release.

**Prediction:** The next stable release (v0.2.9) will almost certainly include **streaming** (web + config), **Gemini web search**, **V3 config docs**, and several tool additions (image_generate, update_plan). Bug fixes for authentication and MCP initialization may also ship, if resolved in time.

## 7. User Feedback Summary

- **Pain Points:**
  - Authentication is currently broken across multiple providers (#2769), despite valid keys.
  - Raspberry Pi Zero 2 users cannot get WhatsApp support without compiling from source (#2625).
  - Android app has a “model not configured” bug (closed #2368, but fix may not be in stable yet).
  - DeepSeek v4 thinking mode required manual extra_body to disable – now fixed via PR #2741.
- **Use Cases:**
  - Developers using PicoClaw as a self‑hosted AI assistant on low‑power devices (RPi).
  - Teams leveraging group‑chat channels (Discord/Telegram/Slack) with multi‑user awareness (#2715).
  - Users wanting real‑time streaming responses for interactive web chat.
- **Satisfaction Indicators:**
  - High PR contribution volume (42 in 24h) suggests a motivated contributor community.
  - Many bug reports are being closed quickly (4 issues closed today).
  - However, the authentication bug, if unfixed, will erode trust in the nightly builds. Users are actively reporting issues and expect a timely fix.

## 8. Backlog Watch

The following important, long‑standing items may need maintainer attention:

| Item | Type | Age (since opened) | Last Update | Notes |
|------|------|--------------------|-------------|-------|
| [#1950](https://github.com/sipeed/picoclaw/issues/1950) – Streaming output for web chat | Enhancement | 2026‑03‑24 (51 days) | 2026‑05‑13 | Open, low priority but on roadmap. PR #2587 addresses it and needs review. |
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) – Streaming HTTP config flag | Enhancement | 2026‑04‑07 (37 days) | 2026‑05‑13 | 6 comments, 1 👍. No PR yet. |
| [#2625](https://github.com/sipeed/picoclaw/issues/2625) – WhatsApp compiled builds | Enhancement | 2026‑04‑22 (22 days) | 2026‑05‑13 | 4 comments, 1 👍. Needs compiler flag configuration. |
| [#2551](https://github.com/sipeed/picoclaw/pull/2551) – Channel identification refactor | PR | 2026‑04‑16 (28 days) | 2026‑05‑14 | Stale, large refactoring that would allow multiple instances of the same provider. Needs maintainer review. |
| [#2587](https://github.com/sipeed/picoclaw/pull/2587) – Web chat streaming + scroll UX | PR | 2026‑04‑19 (25 days) | 2026‑05‑14 | High impact; waiting for review. |
| [#2769](https://github.com/sipeed/picoclaw/issues/2769) – Authentication failure (401) | Bug | 2026‑05‑04 (10 days) | 2026‑05‑13 | **Critical** – no fix yet. Urgent maintainer attention required. |

**Recommendation:** The authentication bug (#2769) should be the top priority, as it breaks all provider communication. After that, merging the streaming PR (#2587) and the channel refactor (#2551) would unblock the next stable release.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-14

## 1. Today’s Overview
NanoClaw saw **very high activity** over the past 24 hours: 9 issues were updated (8 open, 1 closed) and 18 pull requests were updated, with **15 merged/closed PRs** and 3 remaining open. The surge in merged PRs points to a focused feature push—especially around new skills, observability, and platform fixes. Two critical bugs (duplicate container spawn, missing destination wiring) were reported, alongside five medium‑priority bugs and the closure of a Slack setup gap. Community engagement remains strong, with several enhancement discussions continuing.

## 2. Releases
No new releases were published today.

## 3. Project Progress
**15 pull requests were merged or closed** today, advancing the following areas:

| PR | Description | Status |
|----|-------------|--------|
| [#2455](https://github.com/nanocoai/nanoclaw/pull/2455) | **feat(audit-website):** Composite local audit stack (Lighthouse + axe + linkinator) | Merged |
| [#2454](https://github.com/nanocoai/nanoclaw/pull/2454) | **docs(onecli):** Add vault secrets reference | Merged |
| [#2453](https://github.com/nanocoai/nanoclaw/pull/2453) | **feat(copy-grader):** Localize copy-grader skill from upstream | Merged |
| [#2452](https://github.com/nanocoai/nanoclaw/pull/2452) | **feat(container):** Add Lighthouse CLI for site audits | Merged |
| [#2451](https://github.com/nanocoai/nanoclaw/pull/2451) | **feat(audit-website):** Localize audit-website skill from upstream | Merged |
| [#2450](https://github.com/nanocoai/nanoclaw/pull/2450) | **feat(linkedin-ads):** Add LinkedIn Ads playbook skills for Ads group | Merged |
| [#2449](https://github.com/nanocoai/nanoclaw/pull/2449) | **feat(linkedin-community):** Add agent‑browser‑based LinkedIn community manager skill | Merged |
| [#2448](https://github.com/nanocoai/nanoclaw/pull/2448) | **feat(social-listening):** Add composite social‑listening skill | Merged |
| [#2447](https://github.com/nanocoai/nanoclaw/pull/2447) | **feat(reddit):** Add read‑only Reddit MCP and /reddit‑research skill | Merged |
| [#2445](https://github.com/nanocoai/nanoclaw/pull/2445) | **feat(serper):** Add Serper MCP env passthrough and /serper‑search skill | Merged |
| [#2446](https://github.com/nanocoai/nanoclaw/pull/2446) | **feat(firecrawl):** Add Firecrawl MCP and /firecrawl skill | Merged |
| [#2460](https://github.com/nanocoai/nanoclaw/pull/2460) | **setup:** Add `files:read` and `files:write` to Slack scope checklist | Merged |
| [#2458](https://github.com/nanocoai/nanoclaw/pull/2458) | **feat(channels):** Voice transcription hook in Chat SDK bridge | Merged |
| [#974](https://github.com/nanocoai/nanoclaw/pull/974) | **feat:** Add image vision and voice transcription for Discord (was blocked, now merged) | Merged |
| [#2456](https://github.com/nanocoai/nanoclaw/pull/2456) | **feat(langfuse):** Add LangFuse observability to Claude provider | Merged |

**Highlights:** Five new skills (LinkedIn Ads, LinkedIn Community, Social‑Listening, Reddit Research, Serper Search, Firecrawl) were integrated as local skills, reducing dependency on external skill catalogs. Voice transcription for Discord (and any Chat SDK bridge) is now opt‑in via whisper.cpp. LangFuse observability brings per‑session tracing to the Claude provider. The Slack setup documentation was corrected to include missing file‑access scopes.

## 4. Community Hot Topics
The most active discussions are around **credential management** and **infrastructure reliability**:

- **[Issue #869](https://github.com/nanocoai/nanoclaw/issues/869)** (Enhancement, High priority) – *Per‑group credential management and interactive reauth via channels*  
  Opened 2026‑03‑09, 3 comments, 0 👍. The community is pushing for multi‑tenant credential isolation—currently all groups share one set of Claude credentials. The underlying need is security and quota separation, especially as organizations adopt NanoClaw for multiple teams.

- **[Issue #2466](https://github.com/nanocoai/nanoclaw/issues/2466)** (Bug, Low priority) – *Duplicate container spawn race on wakeContainer when script and host sweep run concurrently*  
  Opened today, 1 comment. While labelled “low”, it exposes a real race condition that can result in duplicate processing of the same brief.

- **[Issue #2457](https://github.com/nanocoai/nanoclaw/issues/2457)** (Closed) – *Slack setup walkthrough is missing files:read scope*  
  Closed today after the fix PR [#2460](https://github.com/nanocoai/nanoclaw/pull/2460) was merged. This was a high‑impact documentation bug—users following the official flow would silently break file‑attachment workflows.

## 5. Bugs & Stability
Three new bugs and two existing priority bugs were reported today, plus one fix merged.

| Issue | Priority | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#2465](https://github.com/nanocoai/nanoclaw/issues/2465) | **High** | `ncl destinations add` through approval flow doesn’t populate receiver’s `inbound.db`; wiring breaks | No fix yet |
| [#2466](https://github.com/nanocoai/nanoclaw/issues/2466) | Low (hardening) | Duplicate container spawn race between script `wakeContainer` and host sweep | No fix yet |
| [#2464](https://github.com/nanocoai/nanoclaw/issues/2464) | Medium | CLI silently overrides explicitly passed `--agent-group-id` under group scope | No fix yet |
| [#2462](https://github.com/nanocoai/nanoclaw/issues/2462) | Medium | `setup/install-node.sh` fails on non‑Debian Linux (Fedora/RHEL) | No fix yet |
| [#2461](https://github.com/nanocoai/nanoclaw/issues/2461) | Medium | Teams setup hardcodes `supportsFiles: false`, blocking file attachments | No fix yet |
| [#2457](https://github.com/nanocoai/nanoclaw/issues/2457) | (Closed) | Slack setup missing `files:read` scope | Fixed in [#2460](https://github.com/nanocoai/nanoclaw/pull/2460) |

**Critical note:** Issue #2465 (High priority) has no associated fix PR yet—it breaks destination wiring for approved receivers, meaning new destinations are invisible until the session‑local database is manually updated.

## 6. Feature Requests & Roadmap Signals
The most significant open enhancement is **[#869](https://github.com/nanocoai/nanoclaw/issues/869)** (per‑group credential management), which is likely to land in the next minor release given its “High” priority and sustained community discussion.  

The rush of merged skill‑localisation PRs signals a roadmap shift toward **self‑contained, fork‑friendly skills**—reducing reliance on upstream catalogs that can be removed or blocked. We also see a pattern of **multi‑channel media support**: voice transcription (merged), files:read for Slack (fixed), and the pending Teams files fix indicate that media handling across channels is a top‑priority roadmap item.

## 7. User Feedback Summary
**Pain points reported today:**
- **Slack / Teams file handling** – Users lost inbound file attachments because official setup docs omitted required scopes (Slack: `files:read`, Teams: `supportsFiles:true`). The Slack fix is merged; Teams remains open.
- **Cross‑platform setup** – Users on Fedora/RHEL cannot run `setup/install-node.sh` (Issue [#2462](https://github.com/nanocoai/nanoclaw/issues/2462)).
- **CLI silent overrides** – Operators may believe they are setting a different agent group but the CLI silently ignores their explicit flag (Issue [#2464](https://github.com/nanocoai/nanoclaw/issues/2464)).
- **Missing destination wiring** – Approved destinations are invisible to receivers (Issue [#2465](https://github.com/nanocoai/nanoclaw/issues/2465)), blocking collaborative workflows.

**Positive signals:**
- Users are actively creating skill integrations (LinkedIn, Reddit, Serper, Firecrawl) and contributing documentation.
- The LangFuse observability PR [#2456](https://github.com/nanocoai/nanoclaw/pull/2456) was well‑received and merged quickly.
- The voice transcription feature (PRs [#2458](https://github.com/nanocoai/nanoclaw/pull/2458) and [#974](https://github.com/nanocoai/nanoclaw/pull/974)) fills a long‑requested gap for Discord audio support.

## 8. Backlog Watch
Two open issues need maintainer attention:

1. **[Issue #869](https://github.com/nanocoai/nanoclaw/issues/869)** (Enhancement, High) – Opened 2026‑03‑09 (over two months ago). Per‑group credentials remain unimplemented despite being labelled high priority and receiving community comments. This is the oldest open enhancement.

2. **[Issue #1787](https://github.com/nanocoai/nanoclaw/issues/1787)** (Bug, macOS) – Opened 2026‑04‑15 (one month ago). `setup` fails with merge conflicts on macOS when selecting Apple Container runtime. No fix PR yet; 2 comments.

3. **[PR #2187](https://github.com/nanocoai/nanoclaw/pull/2187)** (Fix) – Opened 2026‑05‑02, still open with no merge decision. Addresses CLI platform ID namespacing (fixes #2186). Stale for 12 days.

**Project health:** High velocity but accumulating technical debt. The 15 merged PRs show strong forward momentum, while the 3 long‑standing open items (especially #869) risk becoming blockers for multi‑tenant deployments.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-14

## 1. Today's Overview
The NullClaw project experienced minimal activity in the last 24 hours. A single new issue was filed, and no pull requests or releases were recorded. The project remains in a low-velocity state, with no closed items or merged changes to report. The sole open issue suggests ongoing community interest in expanding platform integrations, particularly with JIRA.

## 2. Releases
No new releases were published today. The latest available release remains unchanged (none listed). No migration notes or breaking changes are applicable.

## 3. Project Progress
No pull requests were merged or closed today. No features advanced or fixes were resolved in the last 24 hours.

## 4. Community Hot Topics
The only active item today is an enhancement request:

- **[#914 [OPEN] [enhancement] Create JIRA access tool](https://github.com/nullclaw/nullclaw/issues/914)**  
  *Author: sayjeyhi | Created: 2026-05-13 | Updated: 2026-05-13 | Comments: 0 | 👍: 0*  
  **Analysis:** This issue proposes a new tool to integrate NullClaw with JIRA for authentication and standard project management operations (read issues, create tickets, update statuses, add comments, retrieve sprints). Despite zero comments or reactions, the request addresses a common enterprise need—connecting AI agents with existing project tracking systems. It signals user demand for more workflow-oriented integrations.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported today. The project appears stable in the absence of new defect reports.

## 6. Feature Requests & Roadmap Signals
The only feature request is **#914** (JIRA access tool). Given its specificity and practical use case (automating project management tasks), it could be considered for inclusion in the next release if the maintainer prioritizes enterprise integrations. No other roadmap signals were observed.

## 7. User Feedback Summary
With only one user (sayjeyhi) submitting a request and no comments or reactions available, direct feedback is minimal. The request itself reflects a user pain point: the lack of native JIRA connectivity. The user likely wants to automate ticket handling and sprint tracking without leaving the NullClaw ecosystem. No satisfaction/dissatisfaction indicators exist beyond the filing of the issue.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified. The single open issue is only one day old and has not yet received maintainer attention. No items require immediate intervention.

---  
*Data sourced from NullClaw GitHub repository (github.com/nullclaw/nullclaw) as of 2026-05-14.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-05-14

## 1. Today's Overview

The IronClaw project remains highly active, with **22 issues updated and 50 pull requests touched in the last 24 hours**. The Reborn architecture migration dominates development: a wave of infrastructure PRs (WASM component runtime, product adapter registry, sealed handoff stores) were opened, several closed (documentation, Extension Manifest v2 types), and a new channel‑porting tracker was published. Meanwhile, production stability is under scrutiny: a **critical TEE regression** (`still‑frog` instance) and a **nightly E2E failure** were reported today. Two previously reported bugs (agent file‑saving, Telegram setup) have been closed, but the Web UI refresh bug (#2285) remains open pending QA re‑verification. Overall, the project is in a **high‑velocity phase** – significant architectural rework is landing alongside urgent bug fixes, which demands careful coordination.

## 2. Releases

**None** – no new versions were released in the last 24 hours.

## 3. Project Progress

**12 pull requests were merged or closed** today. Notable advances include:

- **Documentation & governance**  
  - [`PR #3595`](https://github.com/nearai/ironclaw/pull/3595) – Updated `crates/README.md` to list all 45 crates (9 missing entries added) for the reborn‑integration branch.  
  - [`PR #3593`](https://github.com/nearai/ironclaw/pull/3593) – Added a Reborn Crate Map to the main README, grouping crates into six themes.  
  - [`PR #3585`](https://github.com/nearai/ironclaw/pull/3585) – Published a tool porting guide for Reborn (v1 → capability path).  

- **Core infrastructure**  
  - [`PR #3591`](https://github.com/nearai/ironclaw/pull/3591) – Added Extension Manifest v2 types and parser (slice 2a), paving the way for a new extension system.  
  - [`Issue #3459`](https://github.com/nearai/ironclaw/issues/3459) – *Closed* – Added user‑selectable model routes and provider pools as part of Reborn model selection.  
  - [`Issue #2905`](https://github.com/nearai/ironclaw/issues/2905) – *Closed* – Fixed agent file‑saving to `/home/agent` (inaccessible in hosted) – now saved to a proper location.

- **Design system adoption**  
  - [`PR #2689`](https://github.com/nearai/ironclaw/pull/2689) – *Merged* – Phase A design‑system tokens (Defuse OmniSwap palette) landed, a first step in UI modernization.

## 4. Community Hot Topics

| Item | Type | Comments | What’s happening |
|------|------|----------|------------------|
| [#2285 – Web UI refresh restores wrong thread](https://github.com/nearai/ironclaw/issues/2285) | Issue | 8 | Long‑standing bug (fixed by #2330 but pending QA re‑verification). Active discussion about the refresh behaviour and how it interacts with non‑assistant threads. The fix has been in staging since mid‑April, but the issue remains open. |
| [#3533 – Telegram v0.28.1 not auto‑setup from UI](https://github.com/nearai/ironclaw/issues/3533) | Issue | 2 | QA reports that Telegram setup directions are outdated and the automatic setup flow is broken. Users are asked to follow manual steps that no longer work. This is a high‑priority (P1) bug affecting a primary channel. |
| [#3447 – Nightly E2E failed](https://github.com/nearai/ironclaw/issues/3447) | Issue | 0 | Automated CI failure report. The Full E2E suite failed on `features` job. No comments yet – likely an infrastructure flake or a regression introduced by recent merges. |
| [#3600 – TEE routine regression on still‑frog](https://github.com/nearai/ironclaw/issues/3600) | Issue | 0 | Fresh critical report: after an upgrade, cron heartbeat routines are failing. High severity – production instance. |

**Underlying needs**: The community (QA team) is repeatedly surfacing regressions and documentation‑to‑implementation mismatches. The Reborn transition appears to be introducing subtle behavioural changes that break existing production workflows.

## 5. Bugs & Stability

Bugs reported or updated today, ranked by severity:

1. **Critical** – [`#3600`](https://github.com/nearai/ironclaw/issues/3600) – **TEE routine regression on `still‑frog`**  
   *Deployed production instance*: after upgrade, cron heartbeat routines stop working. No fix PR yet.  
2. **High (P1)** – [`#3533`](https://github.com/nearai/ironclaw/issues/3533) – **Telegram auto‑setup broken in v0.28.1**  
   *Reported 2 days ago, still open.* Fix direction unclear – likely requires documentation update or code change.  
3. **Medium** – [`#2285`](https://github.com/nearai/ironclaw/issues/2285) – **Web UI refresh restores assistant thread instead of active non‑assistant thread**  
   *Fix exists in staging since April 12, but not yet promoted* – pending QA re‑verification.  
4. **Medium** – [`#3447`](https://github.com/nearai/ironclaw/issues/3447) – **Nightly E2E failure**  
   *Infrastructure flake or regression* – no root cause identified. No fix PR.  
5. **Closed (resolved)** – [`#2905`](https://github.com/nearai/ironclaw/issues/2905) – Agent saving files in unreachable `/home/agent` folder – closed by PR.

## 6. Feature Requests & Roadmap Signals

The most active feature‑related items all point toward the **Reborn architecture**:

- **Porting v1 channels to Reborn** – A “porting tracker” ([#3577](https://github.com/nearai/ironclaw/issues/3577)) classifies all v1 channels (Web, Telegram, Slack, WeChat) and spawns individual porting issues (e.g., [#3580](https://github.com/nearai/ironclaw/issues/3580), [#3581](https://github.com/nearai/ironclaw/issues/3581), [#3579](https://github.com/nearai/ironclaw/issues/3579), [#3582](https://github.com/nearai/ironclaw/issues/3582)). This is a clear next‑release priority.  
- **Loop hooks framework** – Two issues ([#3523](https://github.com/nearai/ironclaw/issues/3523), [#3524](https://github.com/nearai/ironclaw/issues/3524)) define a first‑class hook system for Reborn loops, including inline hooks and a roadmap. Likely to appear in the next 2–3 releases.  
- **Model memory as extension** ([#3537](https://github.com/nearai/ironclaw/issues/3537)) – Proposes making memory a pluggable Extension rather than part of the kernel.  
- **Self‑authored hooks** ([#3567](https://github.com/nearai/ironclaw/issues/3567)) – A novel security pattern allowing agents to create restrictions with monotonic constraints and unforgeable‑channel ratification.  

**Prediction**: The next minor release (likely 0.29) will include **first channel ports** (Web/Telegram) and the **Extension Manifest v2** types that landed today. The loop hooks framework may arrive in 0.30.

## 7. User Feedback Summary

Real pain points from QA and user reports:

- **Telegram onboarding broken** – Users on v0.28.1 are unable to complete Telegram pairing because the UI directions are outdated. This blocks new Telegram users.  
- **Web UI refresh confuses conversation state** – Reloading the page can restore a different thread, causing lost context. Workaround exists (avoid refresh), but not acceptable for production.  
- **Agent file storage not portable** – Previously agents saved to `/home/agent` which is inaccessible in hosted setups. This was fixed (closed as #2905), but earlier reports indicate confusion.  
- **Production TEE routines fail after upgrade** – The `still‑frog` instance’s cron heartbeats are broken, which directly affects users relying on scheduled agent tasks.  

Satisfaction: positive reactions to the ongoing documentation improvements (crate maps, tool porting guide) and the design‑system tokens PR (#2689) – these indicate that the team is listening to developer experience needs.

## 8. Backlog Watch

Items that have been open for several days without maintainer response or resolution:

- [#2285](https://github.com/nearai/ironclaw/issues/2285) – **Web UI refresh bug** – Open since **2026-04-10** (34 days). Fix exists in staging but not promoted. Requires final QA verification and deployment.  
- [#3447](https://github.com/nearai/ironclaw/issues/3447) – **Nightly E2E failure** – Open since **2026-05-10** (4 days). No investigation or fix PR yet. Could indicate a flaky test or a genuine regression.  
- [#3534](https://github.com/nearai/ironclaw/issues/3534) – **Tool to download logs for debugging** – Feature request (open since 2026-05-12). No assignee or comments from maintainers yet.  
- [#3004](https://github.com/nearai/ironclaw/pull/3004) – **Dedicated image tool configuration** – PR open since **2026-04-28**, still awaiting review despite multiple updates. May be stalled due to reborn priorities.  
- [#3006](https://github.com/nearai/ironclaw/pull/3006) – **MCP retry startup after auth failures** – Open since April 28, also awaiting review.

**Recommendation**: The project would benefit from a quick triage of the nightly CI failure and the Telegram setup bug, as both directly affect user trust and production stability. The long‑standing #2285 should be resolved by promoting the existing fix.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Based on the data provided for the LobsterAI project on 2026-05-14, here is your structured project digest.

---

### LobsterAI Project Digest | 2026-05-14

#### 1. Today's Overview

Development activity on LobsterAI was exceptionally high today, driven by a massive batch merge of 26 closed Pull Requests. This marks a significant cleanup of the backlog, with several long-standing feature branches and bug fixes finally integrating into the main codebase. The focus was heavily weighted towards fixing UI bugs (including a critical virtual scrolling issue), improving plugin management and runtime stability, and pushing new features for the cowork session exporting and security scanning. While no new releases were cut, the project's health appears robust, with a strong signal that maintainers are actively resolving technical debt and user-facing issues. The single open bug (a scrolling anomaly with Mermaid diagrams) is a notable stability concern that remains active.

#### 2. Releases

**None.** No new releases were published in the last 24 hours.

---

#### 3. Project Progress

Today saw the closure of **26 Pull Requests**, indicating a major push to merge completed work. Key areas of progress include:

- **Plugin Management Revamp:**
    - [#1979] A significant fix moves user-installed plugins from the app's installation directory (`resources/...`) to the `userData` directory. This prevents plugin loss during application upgrades.
    - [#842] A long-running feature for **Security Environment Scanning** was merged, introducing a security scan engine for Skill data leaks and system permission management.
- **Architecture & Stability:**
    - [#1977] **Artifact Preview Overhaul**: Replaced the inline HTML preview for file artifacts with a local HTTP server (`127.0.0.1`), improving security with session/token authentication and path traversal protection.
    - [#841] **Runtime Polling**: Replaced interval-based cron polling with a non-overlapping self-rescheduling cycle to prevent runtime crashes from overlapping poll operations.
    - [#866] **Context Management**: Implemented a new context management system to mitigate "Lost in the Middle" issues in long cowork sessions, potentially a major quality-of-life improvement for users.
- **Bug Fixing Blitz:**
    - [#1974] Fixed an issue where the working directory for IM channels was incorrect.
    - [#1973] Fixed garbled text in the "Open with" dropdown for apps on Chinese Windows (encoding issue).
    - [#852] Fixed a critical crash where destroying a window could cause the main process to crash due to asynchronous IPC calls.
    - [#860] Added missing error handling for `JSON.parse` in SSE streams to prevent entire processing chains from failing on malformed data.
    - [#864] Fixed a UI issue where switching models caused a "gateway starting" overlay to block user input.
    - [#868] Added transaction protection for memory deletion operations to prevent database inconsistencies.
- **UI/UX Improvements:**
    - [#1976, #1975] A set of chores to fix various UI bugs.
    - [#862] Added a custom theme option allowing users to select an accent color.
    - [#853] Added Markdown, JSON, and JSONL export formats for cowork sessions.

---

#### 4. Community Hot Topics

The single active Issue is the focal point of user frustration, while the merged PR on scrolling cycles points to a major ongoing effort.

- **[Issue #1971: 【Bug】会话页面向上滚动异常，无法滚动或滚动异常](https://github.com/netease-youdao/LobsterAI/issues/1971)**
    - **Status:** Open, 0 comments.
    - **Analysis:** This is the most critical community feedback point. The user reports a complete breakdown of the virtual scrolling mechanism when a session contains a long element (e.g., a Mermaid diagram). The reported root cause—re-rendering loops triggered by height changes—is a classic virtual-scroll pitfall. The lack of comments suggests this might be a recent or isolated report, but the severity is high as it blocks basic usage.

- **[PR #841: fix(polling): prevent overlapping runtime poll cycles](https://github.com/netease-youdao/LobsterAI/pull/841)**
    - **Status:** Merged (from March 25).
    - **Analysis:** While closed today, this is a significant community-facing fix. Overlapping poll cycles are a classic cause of high CPU usage, application lag, and potential freezes. The fact that a test was included ("prove slow poll cycles do not overlap") indicates this was a tenacious bug that the community may have complained about.

---

#### 5. Bugs & Stability

**Critical Severity:**
- **Virtual Scrolling Anomaly (Issue #1971):** Sessions with large elements (like Mermaid) become un-scrollable. This is a functional blocker for users working with complex diagrams. **Status:** No fix PR currently linked.

**High Severity:**
- **Main Process Crash on Window Close (PR #852):** Asynchronous IPC calls after a window is destroyed could crash the entire app. **Status:** Fixed by PR #852.
- **Encoding Garbled Text (PR #1973):** The "Open with" dropdown shows garbled text on Chinese Windows, hindering file operations for a major user segment. **Status:** Fixed by PR #1973.
- **Model Switch UI Block (PR #864):** Switching models caused a 3-5 second blocking overlay, preventing message sending. **Status:** Fixed by PR #864.

**Medium Severity:**
- **Plugin Loss on Upgrade (PR #1979):** User-installed plugins were deleted during app updates. **Status:** Fixed by PR #1979.
- **Database Corruption Risk (PR #863):** SQLite writes were non-atomic, risking corruption on crash. **Status:** Fixed by PR #863.
- **SSE Stream Breaking (PR #860):** Malformed JSON could break the entire stream. **Status:** Fixed by PR #860.

---

#### 6. Feature Requests & Roadmap Signals

The following new features, now merged, signal the direction for the next release:

- **`feat(security): security environment scanning (PR #842)`** — This is a major addition. It suggests the roadmap is prioritizing user safety and system control, possibly to address enterprise adoption.
- **`feat(cowork): context management (PR #866)`** — This is a significant intellectual effort to solve a known LLM weakness (Lost in the Middle). It strongly indicates a focus on improving the quality of long, multi-step AI interactions.
- **`feat(artifacts): local HTTP server for preview (PR #1977)`** — Moving from inline to HTTP for artifact preview is a strong architectural signal, likely enabling more secure and complex file interactions (e.g., executing client-side scripts) while blocking path traversal attacks.
- **`feat(cowork): session export formats (PR #853)`** — Adding Markdown, JSON, and JSONL export is a direct response to the need for data portability and secondary processing of AI session history.

**Prediction:** The next release will likely be centered around a **"Stability & Security"** theme, packaging these long-running feature branches (security scanning, context management) with the critical bug fixes (window crashes, plugin persistence).

---

#### 7. User Feedback Summary

Based on the bug reports and fixes, clear user pain points have been identified:

- **Breakage with Visual Content:** Users creating diagrams (Mermaid) or embedding rich artifacts are experiencing severe scroll failures. **Dissatisfaction is high** as it blocks a core workflow.
- **Data Loss Fears:** The risk of losing custom plugins after an update (PR #1979) or database corruption from non-atomic writes (PR #863) are strong sources of user anxiety regarding data safety.
- **Cross-Platform Friction:** The garbled text on Chinese Windows (PR #1973) shows a specific, unmet localization need, leading to a poor UX for non-English users.
- **Stability on Long Sessions:** Users with longer, complex sessions are likely hitting "Lost in the Middle" issues (PR #866) and window crashes (PR #852), leading to frustration with the AI's memory and app reliability.
- **Desire for Customization:** The addition of custom accent colors (PR #862) and session exports (PR #853) shows a clear, data-backed demand for personalization and data control.

---

#### 8. Backlog Watch

The following items, while now merged/closed today, were open for **over 50 days** (since March 25), indicating they were lingering in the backlog:

- **[PR #841](https://github.com/netease-youdao/LobsterAI/pull/841) (fix(polling))**, **[PR #842](https://github.com/netease-youdao/LobsterAI/pull/842) (feat(security))**, **[PR #847](https://github.com/netease-youdao/LobsterAI/pull/847) (fix(markdown))**, **[PR #848](https://github.com/netease-youdao/LobsterAI/pull/848) (fix(cowork))**, **[PR #852](https://github.com/netease-youdao/LobsterAI/pull/852) (fix(main))**, **[PR #853](https://github.com/netease-youdao/LobsterAI/pull/853) (feat(cowork))**, **[PR #860](https://github.com/netease-youdao/LobsterAI/pull/860) (bugfix(JSON))**, **[PR #862](https://github.com/netease-youdao/LobsterAI/pull/862) (feat(theme))**, **[PR #863](https://github.com/netease-youdao/LobsterAI/pull/863) (fix(sqlite))**, **[PR #864](https://github.com/netease-youdao/LobsterAI/pull/864) (fix(openclaw))**, **[PR #866](https://github.com/netease-youdao/LobsterAI/pull/866) (feat(cowork))**, **[PR #868](https://github.com/netease-youdao/LobsterAI/pull/868) (fix(sqlite))**, **[PR #869](https://github.com/netease-youdao/LobsterAI/pull/869) (fix(security))**

This was a massive backlog cleanup. The long gestation of these PRs suggests they are complex changes requiring careful review or were blocked by higher priorities. Their successful merge today dramatically reduces the project's technical debt. **No new "long-unanswered" issues or PRs are currently visible in the data**; the only active Issue ( #1971 ) is recent. Maintainers should ensure the scrolling bug (#1971) is prioritized to prevent it from becoming the next stale backlog item.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-14

## 1. Today's Overview
Activity on the Moltis repository was very low over the past 24 hours. Only a single new enhancement issue was opened (and remains open), with no pull requests, merged changes, or new releases. This suggests the project is either in a quiet period or that maintainers are focusing on ongoing work without observable GitHub activity. The single issue signals continued community interest in expanding relay infrastructure, but overall project momentum appears stalled for the day.

## 2. Releases
No new releases were published today. The latest available release remains unchanged from prior periods.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. No features or bug fixes were advanced today.

## 4. Community Hot Topics
- **Issue #995 – Feature: Integration of `portal-tunnel` as a trustless relay channel**  
  *Opened by gg582, updated today. No comments or reactions.*  
  *Link: [Issue #995](https://github.com/moltis-org/moltis/issues/995)*  
  The sole active discussion item proposes adding support for `portal-tunnel` as a trustless relay channel. Although it has received no engagement yet, the underlying need appears to be for a censorship‑resistant, decentralized relay mechanism—likely to improve network resilience or reduce dependency on centralized relay servers.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project has no open or unaddressed stability issues from today.

## 6. Feature Requests & Roadmap Signals
The only feature request is **Issue #995** for `portal-tunnel` integration. Given that the author verified no existing enhancement covers this, it may align with future plans to expand trustless communication paths. If the team is already considering alternative relay backends, this request could influence the next minor or major release. No other roadmap signals were present today.

## 7. User Feedback Summary
No user feedback (reactions, comments, or detailed pain points) was recorded today. The single issue submission indicates a user’s desire for trustless relay support but provides no further information on satisfaction or dissatisfaction with the current product.

## 8. Backlog Watch
No long‑standing open issues or PRs requiring maintainer attention were identified in today’s data. All recent issues are either brand‑new or have been closed previously. The project backlog appears clean with no items left unanswered beyond a reasonable timeframe.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here's the CoPaw project digest for 2026-05-14.

---

# CoPaw Project Digest — 2026-05-14

## 1. Today's Overview
CoPaw (GitHub: [agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)) experienced high activity over the past 24 hours, with **50 issues updated** (40 open, 10 closed) and **50 pull requests updated** (38 open, 12 merged/closed). Two releases were published: **v1.1.7** (stable) and **v1.1.7-beta.2** (pre‑release). Community engagement remained strong, with several bug reports and feature requests attracting multiple comments. The merge queue included fixes for shell environment inheritance, browser lifecycle management, and plan‑mode gating, alongside a version bump toward v1.1.8.

## 2. Releases

### v1.1.7
- **Released:** 2026-05-14
- **Key additions:**
  - **Browser Use – Batch Actions:** Execute multiple browser steps (navigate, click, type, screenshot, etc.) in a single tool call ([#4139](https://github.com/agentscope-ai/QwenPaw/pull/4139))
  - **Browser Use – File Download:** Download files by clicking page elements
- **Breaking changes:** None noted.
- **Migration notes:** No migration steps required.

### v1.1.7-beta.2
- **Released:** 2026-05-14
- **Key changes:**
  - `feat(plugins)`: Enable registration of FastAPI `APIRouter` instances through plugins ([#4255](https://github.com/agentscope-ai/QwenPaw/pull/4255))
  - `feat`: Add timeout for keyring operations ([#4263](https://github.com/agentscope-ai/QwenPaw/pull/4263))
  - `fix(console)`: Correct TokenUsage display ([#zha](https://github.com/agentscope-ai/QwenPaw/pull/4264)) – *link truncated in data*
- **Breaking changes:** None expected for beta users.

## 3. Project Progress
The following pull requests were **merged or closed** today (12 total), moving key fixes and features forward:

- **#4325** – `fix(shell): honor envs path for commands` – Resolves `execute_shell_command` not inheriting custom `PATH` from `envs.json` ([#4325](https://github.com/agentscope-ai/QwenPaw/pull/4325))
- **#4306** – `fix(tool): browser implement activity tracking, crash monitoring, and lifecycle management` – Adds activity touch, crash listener, and health check for browser tools ([#4306](https://github.com/agentscope-ai/QwenPaw/pull/4306))
- **#4198** – `feat(plan mode): Strengthen plan reaffirm from the user message` – Prevents non‑plan tool execution before user confirmation ([#4198](https://github.com/agentscope-ai/QwenPaw/pull/4198))
- **#4346** – `chore(version): bumping version to 1.1.8b1` – Prepares alpha branch for v1.1.8 ([#4346](https://github.com/agentscope-ai/QwenPaw/pull/4346))
- **#4329** – `test(console): complete frontend unit test milestone` – Adds ~100 test cases for constants, contexts, layouts, api‑types, and components ([#4329](https://github.com/agentscope-ai/QwenPaw/pull/4329))

Additional open PRs under review (not merged) include Tauri 2.x desktop app support ([#3813](https://github.com/agentscope-ai/QwenPaw/pull/3813)), OAuth provider extension ([#4352](https://github.com/agentscope-ai/QwenPaw/pull/4352)), and AgentScope tracing initialization ([#4351](https://github.com/agentscope-ai/QwenPaw/pull/4351)).

## 4. Community Hot Topics
The most active discussions (by comment count) reveal both urgent bugs and long‑standing UX wishes:

- **#4165** (closed, 9 comments) – *Volcano Engine model configuration broken in v1.1.6* – Users report all model connection tests fail despite correct API key ([#4165](https://github.com/agentscope-ai/QwenPaw/issues/4165))
- **#3957** (open, 7 comments) – *Agent workspace switches incorrectly when receiving messages via channel* – Critical identity confusion bug when main agent receives messages from other agents ([#3957](https://github.com/agentscope-ai/QwenPaw/issues/3957))
- **#4323** (closed, 5 comments) – *execute_shell_command doesn't inherit custom PATH from envs.json* – Fix merged in #4325 ([#4323](https://github.com/agentscope-ai/QwenPaw/issues/4323))
- **#4314** (open, 5 comments) – *MiMo thinking mode + tool calls return 400 after multi‑turn* – Affects all models with reasoning enabled when tool calls exist in history ([#4314](https://github.com/agentscope-ai/QwenPaw/issues/4314))
- **#4300** (open, 5 comments) – *Agent response duplication* – Exact same content returned twice, including reasoning steps ([#4300](https://github.com/agentscope-ai/QwenPaw/issues/4300))
- **#4227** (open, 5 comments) – *MCP stream_http mode hangs on 401 non‑404 errors* – Causes blocks until timeout when server returns 401 ([#4227](https://github.com/agentscope-ai/QwenPaw/issues/4227))
- **#3944** (open, 4 comments, 1 👍) – *Auto‑Memory should exclude Heartbeat & Cron sessions* – Users want to prevent system‑generated dialogues from being consolidated as experiences ([#3944](https://github.com/agentscope-ai/QwenPaw/issues/3944))

Underlying needs: configuration reliability (cloud vendor model configs), agent identity isolation in multi‑agent setups, tool environment consistency (PATH), improved error handling for model API restrictions, and better memory management for automated prompts.

## 5. Bugs & Stability
**High severity (likely affecting many users):**
- **#4300** – *Agent response duplication.* The agent returns every message twice, doubling reasoning steps. No fix PR yet, but #4301 (repair malformed tool raw input) may be related ([#4300](https://github.com/agentscope-ai/QwenPaw/issues/4300)).
- **#4314** – *400 error with MiMo thinking mode + tool calls.* Blocks multi‑turn chat completely when thinking mode is enabled ([#4314](https://github.com/agentscope-ai/QwenPaw/issues/4314)).
- **#4227** – *MCP stream_http hangs on 401.* Any non‑200 error (except 404) can cause indefinite timeouts ([#4227](https://github.com/agentscope-ai/QwenPaw/issues/4227)).

**Medium severity:**
- **#4323** – *execute_shell_command PATH ignored.* Already fixed in #4325 (merged) ([#4323](https://github.com/agentscope-ai/QwenPaw/issues/4323)).
- **#4354** – *Large Excel file forces agent interruption.* Reading a big XLSX causes the agent to be forcibly stopped ([#4354](https://github.com/agentscope-ai/QwenPaw/issues/4354)).
- **#4299** – *write_file() infinite loop / missing arguments.* Long outputs trigger repeated “missing required positional argument” errors ([#4299](https://github.com/agentscope-ai/QwenPaw/issues/4299)).
- **#4205** – *Desktop version v1.1.15 offline whisper fails.* Offline speech‑to‑text forces internet connectivity despite local Whisper and ffmpeg ([#4205](https://github.com/agentscope-ai/QwenPaw/issues/4205)).

**Low severity / regressions:**
- **#4018** – *embedding_model_config reset after update.* Vector search breaks after `qwenpaw update` ([#4018](https://github.com/agentscope-ai/QwenPaw/issues/4018)).
- **#4151** – *Orphan chat entries after restart.* UI shows chats that cannot be opened because session state files are missing ([#4151](https://github.com/agentscope-ai/QwenPaw/issues/4151)).

## 6. Feature Requests & Roadmap Signals
The following enhancements saw active discussion today. Based on recent commits and merged PRs, several are likely to appear in v1.1.8:

| Request | Issue/PR | Likely in v1.1.8? | Rationale |
|---------|----------|-------------------|-----------|
| **Auto‑Memory exclude heartbeat/cron** | [#3944](https://github.com/agentscope-ai/QwenPaw/issues/3944) | ✅ | Fix PR #4348 open and under review |
| **AgentScope tracing support** | [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) | ✅ | PR #4351 adds env‑based init |
| **Session lifecycle hooks** | [#4249](https://github.com/agentscope-ai/QwenPaw/issues/4249) | 🟡 | No PR yet, but requested by multiple users |
| **Real‑time context token display** | [#4284](https://github.com/agentscope-ai/QwenPaw/issues/4284) | 🟡 | Strong UX request, backend already tracks tokens |
| **Backup rotation (retention policy)** | [#3864](https://github.com/agentscope-ai/QwenPaw/issues/3864) | ✅ | PR #4355 adds opt‑in `keep_last` |
| **Tauri 2.x desktop app** | [#3813](https://github.com/agentscope-ai/QwenPaw/pull/3813) | 🟡 | Large undertaking, still under review |
| **Indonesian language support** | [#4287](https://github.com/agentscope-ai/QwenPaw/pull/4287) | ✅ | PR open, likely to merge soon |
| **Telegram streaming output** | [#4318](https://github.com/agentscope-ai/QwenPaw/pull/4318) | ✅ | PR under review, adds `editMessageText` streaming |
| **OAuth provider extension** | [#4352](https://github.com/agentscope-ai/QwenPaw/pull/4352) | 🟡 | First‑time contributor, may need iteration |

Other notable requests: chat list pagination ([#3570](https://github.com/agentscope-ai/QwenPaw/issues/3570)), Markdown rendering for user messages ([#2975](https://github.com/agentscope-ai/QwenPaw/issues/2975)), code block folding ([#3572](https://github.com/agentscope-ai/QwenPaw/issues/3572)), and per‑message context injection into shell subprocess ([#3825](https://github.com/agentscope-ai/QwenPaw/issues/3825)).

## 7. User Feedback Summary
Real user pain points expressed in the last 24 hours:

- **Configuration fragility:** Several users report that upgrades silently reset key settings (Volcano Engine models, embedding config, desktop offline mode). The update process does not preserve customisations, causing repeated manual re‑configuration.
- **Agent identity confusion:** The workspace‑switching bug ([#3957]) breaks multi‑agent setups on channels – a core use case for team automation.
- **Environment inconsistency:** The shell tool does not respect user‑added PATH entries ([#4323]), forcing users to hardcode paths or manually install tools in the venv. This was seen as a major friction for developers using QwenPaw as a dev assistant.
- **Memory and performance:** Users complain about 1GB+ Chrome memory usage for long chats ([#3923]) and that auto‑memory clutters with heartbeat/cron sessions ([#3944]).
- **Positive signals:** The community actively contributes features (Indonesian language, OAuth extension, Telegram streaming). The rapid fixes for shell PATH and browser lifecycle indicate responsive maintainers.

## 8. Backlog Watch
The following open issues and PRs have been unanswered or unassigned for an extended period, despite being important:

- **#1853** (created Mar 19) – *Configurable base path for reverse proxy.* Affects deployments behind URL prefixes. 2 comments, 1 👍. No maintainer response yet ([#1853](https://github.com/agentscope-ai/QwenPaw/issues/1853)).
- **#2975** (created Apr 6) – *Markdown rendering for user messages.* Pure UX improvement with 3 comments. Unassigned ([#2975](https://github.com/agentscope-ai/QwenPaw/issues/2975)).
- **#3809** (created Apr 24) – *Node symlink missing from shell env; manual creation lost after update.* 2 comments. Affects agent scripts depending on `node` ([#3809](https://github.com/agentscope-ai/QwenPaw/issues/3809)).
- **#3825** (created Apr 25) – *Inject per‑message context into shell subprocess environment.* 2 comments. Important for skill scripts that need session metadata ([#3825](https://github.com/agentscope-ai/QwenPaw/issues/3825)).
- **#3923** (created Apr 28) – *1GB+ Chrome memory due to no pagination/virtual scrolling.* 2 comments. Prioritisation unclear despite high impact ([#3923](https://github.com/agentscope-ai/QwenPaw/issues/3923)).
- **#4151** (created May 9) – *Orphan chat entries after restart.* 2 comments. Could lead to data loss perception ([#4151](https://github.com/agentscope-ai/QwenPaw/issues/4151)).

These items would benefit from maintainer triage or a comment to confirm they are on the roadmap.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-14

## 1. Today's Overview
The ZeptoClaw project saw minimal activity in the last 24 hours, with no new releases or pull requests. Two documentation-focused issues were closed, both related to handling CVE/GHSA advisory records under the `llm-enhance/official-cve` repository. No open issues or active PRs remain, indicating a quiet period for the project. Overall project health appears stable, though with no visible feature development or bug fixes today.

## 2. Releases
*No new releases were published today. The latest release remains unchanged.*

## 3. Project Progress
**Pull Requests:** No pull requests were created, merged, or closed in the last 24 hours.

**Issues Closed (2):** Both closed issues are documentation tasks:
- [#590 – docs(cve): extract advisory patch files](https://github.com/qhkm/zeptoclaw/issues/590) – Track extraction of local git patches for published ZeptoClaw CVE/GHSA advisories.
- [#589 – docs(cve): collect published ZeptoClaw advisories](https://github.com/qhkm/zeptoclaw/issues/589) – Track collection of published GitHub Security Advisories and CVE-backed records.

These represent internal process improvements rather than user-facing features.

## 4. Community Hot Topics
No issues or PRs have drawn significant community engagement today. The two closed issues each received one comment but no reactions. They reflect ongoing effort to formalize security advisory tracking, which may align with broader industry interest in CVE management.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project remains stable with no open stability-related issues.

## 6. Feature Requests & Roadmap Signals
No new feature requests were submitted today. Based on recent closed issues, the project’s near-term focus appears to be on improving security advisory documentation rather than adding new capabilities.

## 7. User Feedback Summary
No user feedback (pain points, use cases, or satisfaction reports) was recorded today. The lack of active discussion may indicate the project is either meeting current user needs or experiencing low engagement.

## 8. Backlog Watch
No long-standing issues or PRs requiring maintainer attention are present. The current backlog is clear.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-14

## 1. Today's Overview

ZeroClaw saw very high activity over the past 24 hours, with **41 issues** (25 open, 16 closed) and **50 pull requests** (34 open, 16 merged/closed). No new releases were published, but the project continues to deliver incremental fixes and features through PR merges. Significant effort focused on the upcoming **v0.8.0 multi-agent runtime** (PR #6398) and the **skills ecosystem** (tracker #6253). Community involvement is strong, with multiple bug reports and enhancements arriving daily, and several maintainers actively reviewing and merging contributions.

## 2. Releases

No new releases were published today. The latest tagged version remains **v0.7.5**, with v0.7.6 and v0.8.0 in active development. The v0.7.6 release theme is centered on improving `zeroclaw skills` support and UX (see tracker #6253). No migration notes are applicable at this time.

## 3. Project Progress

Today’s closed/merged PRs advanced stability, testing, and provider compatibility:

- **[#6598](https://github.com/zeroclaw-labs/zeroclaw/pull/6598)** (merged) – Defensively omit `temperature` for Anthropic Opus 4.7, matching the Bedrock-side fix (#6144). Prevents serialization errors when the model does not support temperature.
- **[#6652](https://github.com/zeroclaw-labs/zeroclaw/pull/6652)** (merged) – Added unit tests for `is_user_allowed` and `is_channel_watched` in the Discord history module, increasing test coverage.
- **[#6650](https://github.com/zeroclaw-labs/zeroclaw/pull/6650)** (merged) – **Feat/web dashboard m3** – a large PR touching many providers and channels, advancing the web dashboard milestone.
- **[#5086](https://github.com/zeroclaw-labs/zeroclaw/pull/5086)** (closed, needs-author-action) – Fix `zeroclaw update` to detect host architecture at runtime, resolving wrong binary selection on aarch64/QEMU.

Several critical bugs were also closed (see §5).

## 4. Community Hot Topics

The most discussed issues this period:

| Issue | Comments | Summary |
|-------|----------|---------|
| [#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269) (open) | 4 | Context compressor drops `reasoning_content` from assistant messages – high‑severity for DeepSeek users |
| [#6547](https://github.com/zeroclaw-labs/zeroclaw/issues/6547) (closed) | 4 | Homebrew merge failure – version 0.7.5 missing from homebrew-core |

**Underlying needs**: Users relying on provider-specific structured thinking (like `reasoning_content`) expect compression to preserve all message fields. The Homebrew packaging lag signals a need for better release pipeline synchronisation with package managers. Both issues were acknowledged and acted upon quickly.

The most active open PR is **[#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)** (v0.8.0 multi-agent runtime) – a massive change that has been under incremental review since May 5. It remains the project’s largest single contribution and draws frequent feedback.

## 5. Bugs & Stability

New bugs reported today (2026-05-14) ranked by severity:

**S1 – Workflow blocked**

- **[#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647)** – Cron job output not routed to configured channels (only web dashboard). No fix PR yet.
- **[#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646)** – `web_search_tool` and `web_fetch` not firing via Telegram in v0.7.5 (LM Studio provider). No fix PR yet.

**S2 – Degraded behavior**

- **[#6651](https://github.com/zeroclaw-labs/zeroclaw/issues/6651)** – Matrix channel memory leak (~1 MB Pss per `/admin/reload`) due to upstream `Arc` cycle. No fix PR yet.
- **[#6648](https://github.com/zeroclaw-labs/zeroclaw/issues/6648)** – Cron `session_target=main` still runs in an isolated cron session, ignoring the primary session. No fix PR yet.
- **[#6643](https://github.com/zeroclaw-labs/zeroclaw/issues/6643)** – Thoughts merge into final message when using GLM-5.1 (regression of #5285). No fix PR yet.
- **[#6634](https://github.com/zeroclaw-labs/zeroclaw/issues/6634)** – Cron-scheduled webhook callbacks drop `thread_id`, causing lost context for receiving services. A fix PR **[#6635](https://github.com/zeroclaw-labs/zeroclaw/pull/6635)** (carry `thread_id` through cron announce) is open.
- **[#6654](https://github.com/zeroclaw-labs/zeroclaw/issues/6654)** – Cron read-only operations use the schema-init SQLite path (minor S3). A fix PR **[#6655](https://github.com/zeroclaw-labs/zeroclaw/pull/6655)** is open to split read-only access.

Several previously reported high-severity bugs were closed today, including:

- [#6514](https://github.com/zeroclaw-labs/zeroclaw/issues/6514) – Gateway WebSocket turn spinning after client disconnect (S1). Closed, presumably fixed.
- [#6589](https://github.com/zeroclaw-labs/zeroclaw/issues/6589) – `RouterProvider::supports_vision()` bypasses `multimodal.vision_provider` fallback (S2). Closed.
- [#6609](https://github.com/zeroclaw-labs/zeroclaw/issues/6609) – Matrix outbound attachments omit size metadata (S2). Closed.

## 6. Feature Requests & Roadmap Signals

Notable new feature requests opened today:

- **[#6653](https://github.com/zeroclaw-labs/zeroclaw/issues/6653)** – Host-architecture policy for emulated installs (detect physical arch at runtime for `zeroclaw update`). Likely to be picked up after #5086 is finalised.
- **[#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642)** – Capture full prompt/completion on `llm.call` spans via `gen_ai.input.messages` / `gen_ai.output.messages` (observability enhancement). The author offers to upstream an implementation from a downstream fork.
- **[#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641)** – Turn-level OTel trace correlation, nesting `llm.call`, `tool.call`, `memory.*` spans under a single turn trace. Follow-up to #6009 and #6190.

Ongoing roadmap signals:

- **Skills ecosystem** remains the primary focus for v0.7.6 ([#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)), with many related issues today: [#6645](https://github.com/zeroclaw-labs/zeroclaw/issues/6645) (SkillImprover missing `manifest.toml` support) and [#6644](https://github.com/zeroclaw-labs/zeroclaw/issues/6644) (skill review fork summary parser misses tool receipts).
- **Multi‑agent support** (v0.8.0, PR #6398) continues to gather steam. A new feature request [#6604](https://github.com/zeroclaw-labs/zeroclaw/issues/6604) (closed as duplicate) aligned with OpenClaw’s model.
- **Security hardening** is visible in [#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613) (stronger pairing codes) and the ongoing work on supervised-mode tool approval in PR [#6603](https://github.com/zeroclaw-labs/zeroclaw/pull/6603).

## 7. User Feedback Summary

**Pain points** (from issues and comments):

- Users with slow/remote LLMs (LocalAI, LM Studio) report timeouts in Nextcloud Talk and Telegram channels that are not configurable (see #6156 closed, #6646 open).
- The context compressor silently losing `reasoning_content` (#6269) frustrates DeepSeek users who rely on structured reasoning for tool selection.
- Matrix users experience memory leaks on reload (#6651) and missing attachment metadata (#6609 closed), degrading long-running deployments.
- Cron output isolation and channel routing gaps (#6647, #6648, #6634) surprise users expecting cron jobs to behave like interactive sessions.

**Satisfaction signals**:

- Multiple issues were closed quickly (e.g., #6514 WebSocket hang, #6589 vision fallback, #6609 Matrix metadata), showing responsive maintainers.
- The community is contributing feature PRs (e.g., Claude Code vision support [#6549](https://github.com/zeroclaw-labs/zeroclaw/pull/6549), web dashboard M3 [#6650]) indicating positive engagement and trust in the project’s direction.

## 8. Backlog Watch

Items that may need maintainer attention:

- **PRs with `needs-author-action`** (awaiting contributor response):
  - [#5120](https://github.com/zeroclaw-labs/zeroclaw/pull/5120) – fix(memory): reject clear on append-only markdown backend (stale since March 29)
  - [#6228](https://github.com/zeroclaw-labs/zeroclaw/pull/6228) – fix: sanitize session keys at channel orchestrator layer (stale since April 29)
  - [#5652](https://github.com/zeroclaw-labs/zeroclaw/pull/5652) – feat(provider): native extended thinking for Anthropic and Bedrock (stale since April 11, with recent update on May 14)
- **Issue with `needs-maintainer-review`**:
  - [#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613) – Stronger pairing codes (opened May 13, no maintainer response yet)
- **Large open PR with no recent update**:
  - [#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398) – v0.8.0 multi-agent runtime (active, but incremental review is proceeding; community feedback welcome)

**No issues older than 30 days** are currently unanswered in the top 30, but the three stale PRs above could benefit from maintainer ping or takeover. The `v0.8.0` PR is the biggest decision pending and will likely shape the next several releases.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*