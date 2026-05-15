# OpenClaw Ecosystem Digest 2026-05-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-15 10:00 UTC

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

# OpenClaw Project Digest — 2026-05-15

## Today’s Overview

OpenClaw is in an exceptionally high-activity period. In the last 24 hours, **500 issues and 500 pull requests** were updated, far exceeding typical volumes for a single day. With **48 issues closed and 34 PRs merged/closed**, the maintainers are processing a significant backlog, but the sheer volume of open items (452 open issues, 466 open PRs) suggests the project may be straining under rapid growth. Three new releases landed today, including a beta that externalizes several provider dependencies to reduce core install size. While momentum is strong, the density of regressions reported against the latest stable release (v2026.5.12) — particularly around WebSocket connectivity and the new Codex runtime — indicates that quality assurance is not keeping pace with feature velocity.

---

## Releases

Three releases were published today:

### v2026.5.14-beta.1
- **Dependencies**: Route root ambient Node proxy agents through `@openclaw/proxyline`, dropping root-level `proxy-agent`, `https-proxy-agent`, and `minimatch` dependencies. Low risk of breakage for most users.
- **Control UI/i18n**: Added a `pnpm ui:i18n:report` baseline command to identify hardcoded copy and locale fallback metadata. Internal tooling change — no user-facing impact.

### v2026.5.12
- **Highlights**: WhatsApp, Slack, Amazon Bedrock, Anthropic Vertex, and related provider/plugin dependency cones have been moved out of the core runtime. Installs now only pull what you actually use. Telegram received resilience improvements including isolated polling and durable local spooling.
- **Breaking change potential**: Users who explicitly import from core provider paths may need to adjust. No migration script provided.
- **⚠️ Note**: This release has triggered multiple regression reports (see Bugs & Stability).

### v2026.5.12-beta.8
- **Amazon Bedrock & Plugins**: Externalized Bedrock, Bedrock Mantle, Slack, OpenShell sandbox, and Anthropic Vertex provider packages so core installs no longer pull their transitive dependencies (e.g., AWS SDK). Completes the dependency-slimming work that landed in v2026.5.12.

---

## Project Progress

Today 34 PRs were merged or closed. Key advances:

- **Security hardening**: PR [#80751](https://github.com/openclaw/openclaw/pull/80751) scopes custom provider baseUrl SSRF trust by origin, closing a significant security gap where compromised models could probe internal networks. This is ready for maintainer review.
- **Codex runtime stability**: PR [#82101](https://github.com/openclaw/openclaw/pull/82101) strips response-only reasoning fields from OpenAI Completions requests to fix OpenRouter 500 errors on multi-turn conversations. Also in review.
- **Method descriptor registry**: PR [#82063](https://github.com/openclaw/openclaw/pull/82063) adds a gateway method descriptor registry with handler/scope metadata. This architectural change paves the way for more granular access control and observability.
- **Plugin approvals UX**: PR [#81864](https://github.com/openclaw/openclaw/pull/81864) replaces debug-style approval prompts with plain-language copy — a direct response to user confusion about raw `title`/`command` text being shown in chat.
- **Dependency cleanup**: The three releases today consolidate months of work extracting provider packages from core. This should meaningfully reduce install size and `node_modules` bloat for users who only use a subset of providers.

---

## Community Hot Topics

### Most Active Issues

**1. Codex-vs-Pi runtime parity QA harness** — [#80171](https://github.com/openclaw/openclaw/issues/80171) (13 comments, 1 👍)
This RFC tracks the ongoing migration to Codex as the default runtime. The discussion reveals deep architectural complexity: tool surface parity, doctor migrations, and plugin versioning all diverge between Pi and Codex. The community is pushing for a formal QA harness before full cutover.

**2. XDG_CONFIG_HOME not processed during skill install** — [#53628](https://github.com/openclaw/openclaw/issues/53628) (12 comments)
A long-running bug affecting Docker users who set `XDG_CONFIG_HOME` in `.env` files. This has been open since March 24 with no fix merged — a growing pain point for containerized deployments.

**3. Long-Term Memory & Knowledge Management** — [#50096](https://github.com/openclaw/openclaw/issues/50096) (12 comments, closed)
A visionary thread arguing that OpenClaw's "Driftnet" memory system is failing the promise of agentic continuity. The issue was closed without a resolution, which may disappoint community members who see memory as the critical differentiator.

**4. gh-issues skill: untrusted issue body injection** — [#45740](https://github.com/openclaw/openclaw/issues/45740) (12 comments)
A security-conscious user identified that raw GitHub issue bodies are injected directly into sub-agent prompts without sanitization. This has been open for two months — concerning for anyone using OpenClaw in collaborative or CI environments.

**5. Hardcoded working path** — [#51429](https://github.com/openclaw/openclaw/issues/51429) (11 comments)
A user found that `openclaw` creates a `/Users/wangtao` directory on their system. The thread has a mix of frustration (Chinese and English) about a developer's personal path being merged. This is an embarrassing incident for a mature project.

### Most Active Pull Requests

- **Scoped mention pattern policy** — [#70864](https://github.com/openclaw/openclaw/pull/70864) (still open, extensive labels). This massive PR (touches 15+ channels) adds configurable mention-pattern gating. It's been open since April 24 — the breadth of changes is clearly slowing review.
- **Message-tool-only final improvements** — [#80949](https://github.com/openclaw/openclaw/pull/80949) (open, 1 day). Addresses a recurring pain point: when the model generates a normal final in `message_tool_only` mode, the reply is silently suppressed. This adds diagnostic warnings and prompt guidance.

### Broader Signals
The volume of messages about **reply delivery failures** across Telegram, Discord, and WhatsApp (issues #54531, #51628, #75327) indicates that channel reliability is a top community concern. Users expect messages to *arrive*, not just be generated.

---

## Bugs & Stability

Several significant regressions were reported today against **v2026.5.12**:

### Critical/High Severity

1. **MacOS 26.5 WebSocket connection failure** — [#82037](https://github.com/openclaw/openclaw/issues/82037) (6 comments, 1 👍)
   - **Symptom**: Web and Mac App fail to connect to gateway after upgrade from v2026.5.7 to v2026.5.12, with "wrong protocol" errors.
   - **Environment**: MacOS 26.5, Node 26.0.0, Ollama 0.23.4.
   - **Status**: No fix PR linked. **This is a blocker for Mac users.**

2. **Codex harness OAuth token_expired** — [#81941](https://github.com/openclaw/openclaw/issues/81941) (6 comments, 3 👍, closed)
   - **Symptom**: Every agent turn via Codex harness fails with `token_expired` for freshly logged-in profiles.
   - **Status**: Closed, presumably with a fix in the pipeline. The speed of resolution (filed yesterday, closed today) is encouraging.

3. **SSRF trust vulnerability** — [#80751](https://github.com/openclaw/openclaw/pull/80751) (PR)
   - **Symptom**: Custom providers can be tricked into probing internal networks. The existing SSRF guard blocks private IPs, but the scope is too broad — trusted origins are not distinguished.
   - **Status**: Fix PR is ready for maintainer review. Given the security implications, this should be prioritized.

4. **Tailscale + auth.mode=none exposes gateway to full Tailnet** — [#50630](https://github.com/openclaw/openclaw/issues/50630) (5 comments)
   - **CVSS 9.3 (Critical)**: When using Tailscale serve with `auth.mode=none`, the gateway is exposed without authentication to the entire Tailnet.
   - **Status**: Open since March 19. No fix merged. This is a serious security gap for users who rely on Tailscale for network isolation.

### Moderate Severity

5. **sessions.json unbounded growth → OOM** — [#55334](https://github.com/openclaw/openclaw/issues/55334) (8 comments)
   - **Symptom**: Gateway memory grows 50-100 MB/min until OOM. Root cause is `skillsSnapshot` duplicated per session with no pruning.
   - **Status**: Open since March 26. This affects anyone running long-lived gateways.

6. **Embedded-run zombie agents** — [#48573](https://github.com/openclaw/openclaw/issues/48573) (10 comments)
   - **Symptom**: Subagents leave stale state in session store after parent termination.
   - **Status**: Open since March 17. This undermines the reliability of agent orchestration.

### Regressions (v2026.5.12 specific)
- **Anthropic tool_result → empty assistant content** — [#46080](https://github.com/openclaw/openclaw/issues/46080) (9 comments, closed) — fixed, but indicates fragility in the Anthropic provider path.
- **OpenRouter 500 on multi-turn conversations** — being addressed by PR [#82101](https://github.com/openclaw/openclaw/pull/82101) (filed today).

---

## Feature Requests & Roadmap Signals

### Likely to Land in Next Version

- **YAML config file support** — [#45758](https://github.com/openclaw/openclaw/issues/45758) (6 comments, 2 👍). Low implementation cost, high developer experience win. The PR ecosystem has several "extract schema to dedicated file" patterns that suggest maintainers are receptive to config refactoring.
- **Persistent task-status surface for long-running turns** — [#52640](https://github.com/openclaw/openclaw/issues/52640) (6 comments, 1 👍). Users want a visible "processing" indicator for channel turns that take >30 seconds. The `message_tool_only` improvements in PR #80949 may be a stepping stone.
- **TTS ElevenLabs provider fix** — [#52186](https://github.com/openclaw/openclaw/issues/52186) (5 comments, 1 👍). A regression where ElevenLabs successfully generates audio but OpenClaw plays OpenAI's voice instead. Likely a routing bug that should be straightforward to fix.

### Speculative / Longer-Term

- **Gateway lifecycle warnings to dedicated channel** — [#45565](https://github.com/openclaw/openclaw/issues/45565) (6 comments). Users want system health warnings routed to a separate Discord channel, not the active conversation. This would require significant rework of the event routing system.
- **ACP session binding for WhatsApp** — PR [#56866](https://github.com/openclaw/openclaw/pull/56866) (still open after 47 days). Enables Agent Communication Protocol sessions in WhatsApp, bringing agent routing parity with other channels. Slow review suggests architectural complexity.
- **Memory provenance metadata** — [#54373](https://github.com/openclaw/openclaw/issues/54373) (5 comments). The agent cannot distinguish between injected context and fresh content. This is an advanced feature that would improve reasoning quality but requires deep prompt assembly changes.

---

## User Feedback Summary

### Pain Points (Repeated Themes)

1. **Reply delivery failures** — Users across Telegram, Discord, and WhatsApp report that the model generates a response, but the message never reaches the originating channel. This is the #1 reliability complaint.

2. **Memory/resource leaks** — `sessions.json` unbounded growth, zombie subagent sessions, and Control UI becoming stuck after extended use are eroding trust in long-running deployments.

3. **Config drift and hardcoded paths** — The `/Users/wangtao` incident (#51429) and `XDG_CONFIG_HOME` not being interpreted (#53628) suggest that config handling still has rough edges in multi-platform scenarios.

4. **Codex migration anxiety** — The QA harness RFC (#80171) and token_expired regression (#81941) indicate that the community is watching the Pi-to-Codex transition closely. Users value stability over new features during a runtime migration.

### What’s Working Well

- **Dependency externalization** is widely appreciated. Users running minimal setups (e.g., Telegram + Ollama) see noticeably faster installs and smaller disk footprints.
- **Telegram resilience improvements** in v2026.5.12 (isolated polling, local spooling) address a long-standing pain point. No new Telegram-specific reliability bugs were filed today.
- **Plugin approval UX** (PR #81864) directly responds to user complaints about raw debug text in approvals. The community is quick to praise when the team listens.

### Sentiment Snapshot

The overall tone is **constructive but strained**. Users are reporting bugs in good faith, but the volume of regressions against stable releases suggests that testing coverage is insufficient. The security issues (#50630, #80751) have been open for weeks without resolution, which may erode confidence among enterprise or security-conscious users.

---

## Backlog Watch

### Issues Needing Maintainer Attention

1. **[Security] Tailscale + auth.mode=none exposes gateway** — [#50630](https://github.com/openclaw/openclaw/issues/50630)
   - Open since March 19. CVSS 9.3. No fix merged. This is the most urgent item in the backlog.

2. **[Memory] sessions.json unbounded growth** — [#55334](https://github.com/openclaw/openclaw/issues/55334)
   - Open since March 26. Affects all long-running gateways. A fix would likely involve adding a pruning interval and excluding `skillsSnapshot` from ephemeral sessions.

3. **[Quality] Codex-vs-Pi runtime parity QA harness** — [#80171](https://github.com/openclaw/openclaw/issues/80171)
   - Open since May 10. The community is effectively asking for a formal test suite before the Codex cutover. This should be treated as a dependency for the next stable release.

### PRs Stuck in Review

- **WhatsApp ACP session binding** — [#56866](https://github.com/openclaw/openclaw/pull/56866) (47 days open)
- **Media caching during context pruning** — [#56858](https://github.com/openclaw/openclaw/pull/56858) (47 days open)
- **Scoped mention pattern policy** — [#70864](https://github.com/openclaw/openclaw/pull/70864) (21 days open, touches 15+ channels)

These three PRs represent significant feature work that has been ready for review for weeks. Their stalled state may be blocking downstream development in the WhatsApp and Signal channels.

### Notable

- **Long-Term Memory issue** — [#50096](https://github.com/openclaw/openclaw/issues/50096) was closed today without a resolution. Given the comment count (12) and the strategic importance of memory to the project's vision, the community may expect a follow-up RFC or at least a "won't fix" rationale.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem
**Date:** 2026-05-15 | **Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape is experiencing an **unprecedented surge in development velocity**, with seven out of twelve tracked projects showing high or very high activity today. The ecosystem is converging around **multi-channel messaging, provider-agnostic runtimes, and memory/persistence as core differentiators**, while diverging on architectural philosophy—monolithic reference implementations (OpenClaw) versus lightweight modular agents (NanoBot, TinyClaw). Security hardening is emerging as a top cross-cutting concern, with CVSS 9.3+ vulnerabilities reported across OpenClaw, ZeroClaw, and CoPaw. The market is fragmenting between **general-purpose personal assistants** (OpenClaw, Hermes Agent, IronClaw) and **task-specific or domain-optimized agents** (NanoBot, PicoClaw, LobsterAI), with the "Codex runtime migration" theme affecting three major projects simultaneously.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Releases Today | Activity Level | Health Score | Key Signal |
|---------|:-------------:|:-----------:|:--------------:|:-------------:|:------------:|------------|
| **OpenClaw** | 500 | 500 | 3 (1 beta, 1 stable, 1 beta) | Very High | ⚠️ Strained | Regression density outpacing fix velocity |
| **NanoBot** | 60 | 23 | 0 | High | ✅ Healthy | Fast bug turnaround, major doc campaign |
| **Hermes Agent** | 50 | 50 | 0 | Very High | ✅ Healthy | Security P1 fixed same day |
| **IronClaw** | 50 | 50 | 1 (v0.28.2) | Very High | ⚠️ Rebuilding | Reborn architecture consuming all dev cycles |
| **CoPaw** | 40 | 50 | 0 | Very High | ✅ Healthy | 33 PRs merged, security hardening active |
| **ZeroClaw** | 31 | 50 | 0 | Very High | ⚠️ Unstable | 3 S1 bugs unblocked; cron reliability critical |
| **PicoClaw** | 10 | 30 | 1 (nightly) | High | ✅ Iterating | DeepSeek/MiMo fixes landed |
| **LobsterAI** | 1 | 37 | 1 (v2026.5.14) | High | ✅ Consolidating | 33 PRs batch-closed from backlog |
| **NanoClaw** | 1 | 25 | 0 | High | ✅ Iterating | Docker issue critical, but active PR pipeline |
| **Moltis** | 1 | 0 | 0 | Low | 🟢 Dormant | Single TLS bug, no maintainer response |
| **TinyClaw** | 0 | 0 | 0 | None | 🟢 Idle | No activity |
| **NullClaw** | 0 | 0 | 0 | None | 🟢 Idle | No activity |
| **ZeptoClaw** | 0 | 0 | 0 | None | 🟢 Idle | No activity |

**Health Score Methodology:** ✅ Healthy = Fast fix turnaround, active maintainer response, balanced issue/PR velocity. ⚠️ Strained/Unstable = Regression density, critical bugs unaddressed, or architectural churn. 🟢 Dormant/Idle = No activity or single unaddressed issue.

---

## 3. OpenClaw's Position

**Advantages Over Peers:**
- **Scale & community:** 500 issues/PRs updated daily—2–10× any other project. Largest contributor base and user community in the ecosystem.
- **Maturity:** Stable release v2026.5.12 with three years of iterative development. Only project shipping multiple releases in a single day.
- **Provider breadth:** Native support for 15+ providers (WhatsApp, Slack, Telegram, Anthropic, Bedrock, Vertex, etc.) with externalized dependency model—most comprehensive in ecosystem.
- **Codex runtime investment:** First-mover on next-gen runtime, though migration is causing regression pain.

**Technical Approach Differences:**
- **Monolithic core, plugin-extensible:** Unlike NanoBot's single-binary approach or IronClaw's Rust-native modularity, OpenClaw uses a Node.js core with npm-provider isolation. This enables rapid provider addition but creates dependency bloat (partially addressed by today's externalization).
- **"Driftnet" memory system:** Unique approach to agentic persistence, but community feedback (#50096) suggests it's failing to deliver on the promise of true agentic continuity.
- **SSRF trust scoping (#80751):** OpenClaw's security model for custom providers is more nuanced than peers—it distinguishes trusted origins rather than blanket-blocking.

**Community Size Comparison:**
- OpenClaw's daily volume (500 issues, 500 PRs) dwarfs the next most active projects (IronClaw/Hermes at 50/50 each).
- However, **issue closure rate (48/500 ≈ 10%)** is the lowest in the ecosystem—NanoBot closed 51/60 (85%), Hermes closed 34/50 (68%).
- This suggests **OpenClaw is struggling with review bandwidth** despite having the largest community.

---

## 4. Shared Technical Focus Areas

The following requirements emerged across **three or more projects** in today's data:

| Requirement | Projects Affected | Specific Pain Points |
|-------------|------------------|---------------------|
| **Cron/scheduling reliability** | OpenClaw, NanoClaw, ZeroClaw, CoPaw | Output not delivered (#6647 ZeroClaw), session isolation broken (#6648), cron context lost (#6105) |
| **Provider security hardening** | OpenClaw, CoPaw, ZeroClaw, LobsterAI | SSRF trust scoping, plaintext channel credentials, path traversal, token refresh races |
| **Model reasoning content handling** | OpenClaw, PicoClaw, IronClaw, CoPaw, ZeroClaw | DeepSeek V4 `reasoning_content`, MiMo thinking mode causing 400 errors across multiple APIs |
| **Multi-channel message delivery** | OpenClaw, ZeroClaw, NanoBot, CoPaw | Telegram/Discord reply failures, audio content unsupported, Matrix memory leaks |
| **Configuration UX** | OpenClaw, NanoBot, IronClaw, NanoClaw | JSON vs TOML debate, hardcoded paths (#51429), XDG compatibility, vault secrets management |
| **Session/state management** | OpenClaw, NanoBot, PicoClaw, CoPaw | Zombie subagents, `sessions.json` unbounded growth, interrupted retry loses context |
| **Runtime migration (Pi→Codex)** | OpenClaw, IronClaw (Reborn), NanoClaw (Codex parity) | QA harness needed, feature parity gaps, regressions in stable releases |

**Emerging requirement across 2+ projects (watch list):**
- Agent internet access control (NanoClaw #2477, IronClaw trust policy)
- YAML/TOML configuration (NanoBot #3402, OpenClaw #45758)
- Observability/OTel traces (ZeroClaw #6641, Hermes dashboard improvements)
- Per-channel model override (LobsterAI #838, CoPaw #3173)

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | IronClaw | CoPaw | PicoClaw |
|-----------|----------|---------|-------------|----------|-------|----------|
| **Primary Language** | TypeScript/Node.js | Python | C++/CLI | Rust | Python/FastAPI | Go |
| **Target User** | Plugin developers, power users | Individual assistant users | CLI-first developers | Enterprise infra teams | Multi-platform ops | Edge/embedded AI |
| **Release Cadence** | Multiple/week | ~Weekly | Irregular | Patch-driven | Bi-weekly | Nightly builds |
| **Unique Feature** | Largest provider ecosystem | Easiest setup (single binary) | Agent delegation & MCP | Reborn event-driven arch | Visual plan mode | Self-contained binary |
| **Security Posture** | Reactively patching | Proactive (Chinese doc team) | Fastest P1 response | Rebuild-then-secure | Slow on long-standing issues | Tirith scanner (new) |
| **Memory Architecture** | Driftnet (failing) | Simple session store | Delegation-based | Event-ledger (Reborn) | Workspace files | None (stateless) |
| **Best For** | Extensibility, multi-provider | Quick personal deployment | Terminal power users | Production infra at scale | Chinese IM ecosystem | Minimal resource VMs |

**Key Insight:** No project dominates all dimensions. OpenClaw leads on ecosystem size but lags on stability. NanoBot leads on ease-of-use but has limited provider breadth. IronClaw leads on architectural elegance (Reborn) but is inaccessible during rebuild. Hermes Agent leads on security response time.

---

## 6. Community Momentum & Maturity

**Tier 1: High Velocity, High Risk (Rapidly Iterating)**
- **OpenClaw** — Growing too fast for QA capacity. 452 open issues, 466 open PRs. The regression density against stable releases is the highest in the ecosystem. If the team can stabilize Codex migration, it remains the reference implementation.
- **IronClaw** — "Reborn" architecture is absorbing all development energy. 48 open issues, 22 PRs merged today. Positive momentum but high disruption risk until cutover completes.
- **ZeroClaw** — Very high activity with worrying bug severity. 3 S1 (workflow-blocked) bugs unaddressed. Cron fragility is the top weakness.

**Tier 2: Healthy Velocity, Consolidating**
- **NanoBot** — Most balanced ratio of issue closure (85% in 24h). Chinese documentation campaign shows community growth focus. Stable iteration pattern.
- **Hermes Agent** — Fast P1/P2 fix turnaround (security fixes same day). Healthy 34/50 PR close rate. Mature security posture.
- **CoPaw** — Strong backend test coverage investment. 33 PRs merged. DingTalk channel improvements suggest Chinese-ecosystem focus succeeding.
- **LobsterAI** — Backlog clearing day (33 PRs). Single regression (#1988) needs hotfix. Transitioning from feature-adding to stability phase.

**Tier 3: Low Activity / Dormant**
- **Moltis** — Single bug with no response. Project may be abandoned or internal-only.
- **TinyClaw, NullClaw, ZeptoClaw** — Zero activity. Likely niche or paused projects. No threat to major players.

**Maturity Assessment:** The ecosystem has **two reference-quality projects** (OpenClaw, NanoBot), **three stable platforms** (Hermes, CoPaw, LobsterAI), **two in architectural transition** (IronClaw, ZeroClaw), and **two emerging** (PicoClaw, NanoClaw). The remaining four are effectively inactive.

---

## 7. Trend Signals for AI Agent Developers

**1. Security is No Longer Optional** — Three projects (OpenClaw, ZeroClaw, CoPaw) addressed CVSS 9+ vulnerabilities in a single day. Developers integrating these tools must audit SSRF guards, channel credential storage, and authorization models. The Tailscale + `auth.mode=none` issue (#50630) suggests many users are misconfiguring for convenience.

**2. Cron/Scheduling is the Critical Gap** — Across ZeroClaw, NanoClaw, and CoPaw, cron output delivery, session isolation, and agent context are all broken. For developers building autonomous agents, **reliable scheduled execution is the #1 production blocker**—not intelligence quality.

**3. Multi-Provider Support is Table Stakes** — Every active project supports multiple LLM providers. The differentiator is now **how gracefully failures are handled**: OpenClaw's OpenRouter 500s, CoPaw's Anthropic file-type incompatibility, ZeroClaw's Xiaomi reasoning content loss. Developers should prioritize **circuit breakers and retry logic** over additional provider count.

**4. Memory & Continuity Remain Unsolved** — OpenClaw closed its Long-Term Memory issue (#50096) without resolution. NanoBot sessions lose context on interrupt. The Driftnet approach is failing. **No project has a working long-term memory architecture**—this is the ecosystem's biggest open problem.

**5. Codex / Runtime Migration Creates Fragmentation** — Three projects (OpenClaw, IronClaw, NanoClaw) are migrating runtimes simultaneously. Developers should **freeze runtime dependencies** until at least one project completes migration successfully. The QA harness RFC (#80171) may set the standard.

**6. Chinese Ecosystem is Growing Independently** — LobsterAI, CoPaw, and NanoBot all have strong Chinese-language communities. CoPaw's DingTalk improvements and LobsterAI's NetEase provider integration suggest a **parallel ecosystem developing around Chinese IM platforms** (DingTalk, Feishu, QQ, WeChat). Western developers may miss features if ignoring this trend.

**7. Observability is Becoming Standard** — ZeroClaw's OpenTelemetry/Prometheus integration, IronClaw's event ledger, and Hermes' dashboard improvements signal that **agent observability is moving from luxury to requirement**. Expect OTel-based monitoring to become a selection criterion in 6–12 months.

---

**Summary for Decision-Makers:**
- **Build on OpenClaw** if you need maximum provider breadth and community support—but budget for stability overhead.
- **Build on NanoBot or Hermes** if stability and fast security fixes are priorities.
- **Avoid IronClaw** until Reborn cutover completes (est. Q3 2026).
- **Watch ZeroClaw**—highest innovation velocity but lowest reliability score.
- **The ecosystem is maturing rapidly, but no single project has solved the memory, scheduling, and security triangle simultaneously.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-15

**Generated from GitHub data: 60 issues and 23 PRs updated in the last 24 hours**

---

## 1. Today's Overview

Activity surged today with **51 closed issues and 13 merged/closed PRs**, indicating a highly productive day. A major documentation and commenting campaign (over 20 issues) was completed by contributor `xianqiangfu`, adding Chinese annotations, architecture diagrams, and guide translations. Concurrently, the development team landed several security fixes, channel integrations improvements, and infrastructure patches. No new releases were cut, but the sheer volume of merged code suggests a release may be imminent. Overall project health appears strong: bug reports are being addressed rapidly, and new features for goal-state streaming, task planning, and provider expansion are moving through the review pipeline.

---

## 2. Releases

No new releases today. The latest published version remains `0.1.5.post3.2026.05.13`.

---

## 3. Project Progress

13 PRs were merged or closed today. Key advancements include:

- **Security hardening**  
  - [`#3842`](https://github.com/HKUDS/nanobot/pull/3842) – Confine local media attachments when workspace restriction is enabled.  
  - [`#3789`](https://github.com/HKUDS/nanobot/pull/3789) – Sanitize Feishu/Lark downloaded media filenames to prevent path traversal.

- **Channel & provider fixes**  
  - [`#3775`](https://github.com/HKUDS/nanobot/pull/3775) – Register no‑op handlers for Feishu bot member events, silencing “processor not found” errors.  
  - [`#3786`](https://github.com/HKUDS/nanobot/pull/3786) – Wire Telegram `transcription_provider` / `transcription_api_key` / `transcription_language` config fields so voice messages are transcribed.  
  - [`#3752`](https://github.com/HKUDS/nanobot/pull/3752) – Clear `media_paths` after successful WhatsApp voice transcription to avoid phantom file tags.  
  - [`#3764`](https://github.com/HKUDS/nanobot/pull/3764) – Support UNC paths (`\\server\share`) in shell tool’s Windows path extraction.

- **Provider compatibility**  
  - [`#3734`](https://github.com/HKUDS/nanobot/pull/3734) – Wire Xiaomi MiMo `thinking_type` so setting `reasoning_effort: "none"` correctly disables reasoning.

- **Infrastructure & config**  
  - [`#3783`](https://github.com/HKUDS/nanobot/pull/3783) – Add `ssl_verify` config option for corporate proxy SSL MITM scenarios.  
  - [`#2848`](https://github.com/HKUDS/nanobot/pull/2848) – Fix config compatibility for plugin channels by using consistent attribute access.  
  - [`#3841`](https://github.com/HKUDS/nanobot/pull/3841) – Remove redundant `GlobTool` (its functionality is already covered by GrepTool’s `glob` parameter).  
  - [`#3779`](https://github.com/HKUDS/nanobot/pull/3779) – Persist shortcut commands (e.g., `/help`) so WebUI history hydration works correctly.  
  - [`#3774`](https://github.com/HKUDS/nanobot/pull/3774) – Chat‑native DM sender approval flow for private‑assistant deployments.

---

## 4. Community Hot Topics

Issues and PRs attracting the most comments or reactions reveal three underlying user pain points:

- **Configuration complexity**  
  [Issue #3402](https://github.com/HKUDS/nanobot/issues/3402) (9 comments, closed) – User proposes replacing JSON with TOML for configuration. While closed without visible PR, the lively discussion signals broad desire for more human‑friendly config format.

- **Session continuity**  
  [Issue #3689](https://github.com/HKUDS/nanobot/issues/3689) (5 comments, closed) – User reports that interrupting a bot mid‑task causes it to lose context of the previous session. Although marked closed, the need for reliable, non‑volatile session memory remains a top user concern.

- **Channel integration quirks**  
  [Issue #3772](https://github.com/HKUDS/nanobot/issues/3772) (2 comments, closed) – Bot errors when another bot @‑mentions it in Feishu. Rapidly fixed by ([#3775](https://github.com/HKUDS/nanobot/pull/3775)).  
  [Issue #3787](https://github.com/HKUDS/nanobot/issues/3787) (2 comments, open) – Request for bot reply‑mention feature, indicating users want richer interaction patterns.

Other active items:  
[Issue #3790](https://github.com/HKUDS/nanobot/issues/3790) (2 comments, open) – WebUI display corruption after updating to latest source, forcing manual refresh.  
[PR #3788](https://github.com/HKUDS/nanobot/pull/3788) – Large feature PR (goal_state streaming, long_task, WebUI composer) awaiting merge; likely to shape the next minor release.

---

## 5. Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **High** | WebUI session printing shows garbled content; requires page refresh to restore ([#3790](https://github.com/HKUDS/nanobot/issues/3790)) | Open | None yet |
| **Medium** | Session interruption causes loss of previous turn context ([#3689](https://github.com/HKUDS/nanobot/issues/3689)) | Closed | Possibly addressed by ongoing session‑persistence work (PR [#3779](https://github.com/HKUDS/nanobot/pull/3779) fixed shortcut persistence, but broader context loss may still be open) |
| **Medium** | Brave search rate‑limits not handled gracefully; bot returns HTTP 429 errors ([#2560](https://github.com/HKUDS/nanobot/issues/2560), referenced in [#3840](https://github.com/HKUDS/nanobot/pull/3840)) | Fix open | [#3840](https://github.com/HKUDS/nanobot/pull/3840) adds serialized requests and Retry‑After handling |
| **Low** | Feishu errors when other bot @‑mentions; “processor not found” ([#3772](https://github.com/HKUDS/nanobot/issues/3772)) | Fixed | [#3775](https://github.com/HKUDS/nanobot/pull/3775) |
| **Low** | Shell tool fails on Windows UNC paths ([#3764](https://github.com/HKUDS/nanobot/pull/3764)) | Fixed | [#3764](https://github.com/HKUDS/nanobot/pull/3764) |
| **Low** | Telegram voice messages not transcribed despite config ([#3786](https://github.com/HKUDS/nanobot/pull/3786)) | Fixed | [#3786](https://github.com/HKUDS/nanobot/pull/3786) |

The WebUI display bug (#3790) is the most critical unresolved issue, as it directly degrades user experience for all WebUI users.

---

## 6. Feature Requests & Roadmap Signals

**User‑requested features with strong engagement:**

- **TOML configuration** – [Issue #3402](https://github.com/HKUDS/nanobot/issues/3402) (closed, but discussion alive). The project maintainers may consider offering a TOML option if user demand persists.
- **Bot reply‑mention** – [Issue #3787](https://github.com/HKUDS/nanobot/issues/3787) (open). Users want the bot to be able to @‑mention users in replies.

**In‑development features (open PRs likely to land soon):**

- **Goal‑state streaming & long‑task WebUI** – [PR #3788](https://github.com/HKUDS/nanobot/pull/3788) introduces chat‑scoped sustained goal state, end‑to‑end from session metadata to WebUI.
- **Plan tool for task decomposition** – [PR #3791](https://github.com/HKUDS/nanobot/pull/3791) adds a `plan` tool enabling the agent to break down complex multi‑step tasks, persist plans across turns, and survive context compaction.
- **Provider expansion** – [PR #3785](https://github.com/HKUDS/nanobot/pull/3785) adds support for OpenCode Go gateway, aggregating GLM, Kimi, DeepSeek, MiMo, Qwen, MiniMax.
- **Gateway lifecycle hooks** – [PR #3792](https://github.com/HKUDS/nanobot/pull/3792) adds start/stop notification hooks for channels like Feishu.

**Prediction:** The next version (likely `0.1.6`) will include the plan tool, goal‑state streaming, the OpenCode Go provider, and several security/UX fixes. TOML config support may appear as a community contribution rather than a core change.

---

## 7. User Feedback Summary

Based on closed issues and the discussion patterns:

| Pain Point | Frequency | Sentiment |
|------------|-----------|-----------|
| Session context lost on interrupt | High | Negative – “I told it to restart and it forgot the conversation” |
| WebUI misbehaving after update | One report | Frustrated – “content displayed in disorder, must refresh” |
| Channel integration edge‑cases (Feishu, Telegram, WhatsApp) | Several | Mixed – quick fixes appreciated, but users expect zero‑config |
| Configuration format | Moderate | Neutral – some power‑users prefer TOML; JSON is tolerated |
| Security / corporate firewall issues | Moderate | Positive – fixes landed same day (SSL verify, media confinement) |

**Satisfaction indicator:** Many bug reports were closed within hours of being opened, and roll‑up fixes often merged the same day. This responsiveness should increase community trust.

---

## 8. Backlog Watch

No truly long‑stale items appear in the top 30 issues (all from April–May 2026). However, a few open PRs require attention before they go stale:

- [PR #3460](https://github.com/HKUDS/nanobot/pull/3460) – LongTaskTool (multi‑step agent tasks). Open since April 26. It is a large feature and may need rebasing after the merged pairing and plan‑tool changes.
- [PR #3785](https://github.com/HKUDS/nanobot/pull/3785) – OpenCode Go gateway. Open since May 14; no reviewer comments yet.
- [PR #3793](https://github.com/HKUDS/nanobot/pull/3793) – Stabilize Codex prompt cache key. Open since May 15; addresses a long‑standing performance issue (#2440).

**Recommendation:** Reviewers should prioritise #3785 (provider expansion) and #3793 (cache stability) to keep the pipeline moving. The WebUI bug #3790 also needs a fix PR created promptly.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-15

## 1. Today’s Overview
The project experienced **very high activity** over the last 24 hours, with **50 issues updated** (34 closed, 16 still open) and **50 pull requests updated** (23 merged/closed, 27 open). No new releases were published. The development focus was squarely on **stability fixes**: PRs landed for a critical security fix (P1), vision model handling, cron reliability, terminal workdir expansion, and launchd restart logic. The community is actively engaged on **Feishu platform improvements** and **custom provider compatibility**, with several open feature requests and bug reports receiving multiple comments. The high close rate and rapid PR turnaround indicate a healthy, responsive development cycle.

## 2. Releases
*No new releases were published in the last 24 hours.*

## 3. Project Progress
The following **23 pull requests were merged/closed** since yesterday. Highlights by area:

### Security & Stability
- **PR #26003** (P1, security) – Guards `os.chmod(path.parent, 0o700)` against system directories like `/`, preventing root inode permission escalation.  
- **PR #26001** (P2, vision) – Caps image pixel dimensions at 8000 px to avoid Anthropic 400 errors that could permanently brick a session.  
- **PR #26002** (P2, vision) – Adds server error (5xx) detection to auxiliary vision fallback, enabling retry when Gemini returns 503.  
- **PR #26164** (P2, terminal) – Expands `~` and `$VAR` in `workdir` before resolving cwd.  
- **PR #26125** (P2, cron/MCP) – Lazy reconnect on dead MCP sessions for cron jobs.  
- **PR #26253** (P2, CLI/gateway) – Gives `launchd_restart` a cleanup tail past the drain budget to prevent premature SIGKILL.  
- **PR #26266** (P3, cron) – Stops escaping non-ASCII characters in cron JSON storage and tool output.  
- **PR #25948** (P3, CLI) – Strips OSC-8 hyperlinks from welcome banner on `/clear` / `/reset` / `/new`.

### Configuration & Provider
- **PR #25949** (P2, agent/config) – Adds `configurable default_headers` for API requests (e.g., custom User-Agent).  
- **PR #25316** (P2, OpenRouter) – Preserves `:free` suffix in auxiliary fallback models.  
- **PR #17652** (P2, ACP) – Replays session history on `session/load` or `session/resume`.

### Documentation & Housekeeping
- Several issues labelled “Withdrawn: private tracking moved” were closed (no action required).

## 4. Community Hot Topics
The most discussed items in the last 24 hours:

| Issue / PR | Comments | Topic |
|------------|----------|-------|
| [#7237 – Response truncated due to output length limit](https://github.com/NousResearch/hermes-agent/issues/7237) | 28 (closed) | Long-form output truncation bug |
| [#16084 – Feishu platform: use CardKit streaming card](https://github.com/NousResearch/hermes-agent/issues/16084) | 6 (open) | Feishu streaming output |
| [#25594 – Vision-capable model detection missing for custom providers](https://github.com/NousResearch/hermes-agent/issues/25594) | 5 (open) | Custom provider vision support |
| [#26174 – Hermes content cannot render on Feishu](https://github.com/NousResearch/hermes-agent/issues/26174) | 3 (closed) | Feishu markdown rendering |

**Underlying needs:**
- **Feishu users** are actively requesting native card-based streaming (instead of plain message editing) – see also #26236 (open). The community wants a polished, non-“edited” badge experience.
- **Custom provider users** need robust vision model detection to avoid HTTP 400 errors. This is a top pain point for users behind proxies or using non-registry models.
- **Long output handling** (#7237) has been resolved (closed), but its high engagement signals that users expect Hermes to handle large responses gracefully.

## 5. Bugs & Stability
Bugs reported or active today, ranked by severity:

### P1 (Critical)
- **`os.chmod` on system directories** – Fixed by PR #26003 (merged). Risk of breaking DNS, networking, Docker. **Resolved.**

### P2 (High)
- **Vision model detection missing for custom providers** – [#25594 (open)](https://github.com/NousResearch/hermes-agent/issues/25594). No fix PR yet; related fix [#23750 (open)](https://github.com/NousResearch/hermes-agent/pull/23750) addresses a similar issue on the provider profile path.
- **delegate_task returns HTTP 404 with DeepSeek provider** – [#26210 (open)](https://github.com/NousResearch/hermes-agent/issues/26210). No fix PR seen; may be a provider-specific API compatibility issue.
- **Dashboard resume in chat shows “session ended” on explicit network binds** – [#26264 (open)](https://github.com/NousResearch/hermes-agent/issues/26264). A fix PR [#26265 (open)](https://github.com/NousResearch/hermes-agent/pull/26265) is already proposed.
- **Hermes gateway restart on macOS leaves gateway in stopped state** – [#26198 (open)](https://github.com/NousResearch/hermes-agent/issues/26198). Not yet fixed; related PR #26253 improves launchd handling for clean shutdown, but this issue may require more work.

### P3 (Medium/Low)
- **Native user timezone configuration** – [#26255 (open)](https://github.com/NousResearch/hermes-agent/issues/26255) – Feature request, but also impacts cron scheduling.
- **Platform-aware output formatting** – [#26239 (open)](https://github.com/NousResearch/hermes-agent/issues/26239) – Affects Markdown rendering on Feishu/Discord.
- **Mouse-aware TUI / clickable output** – [#26202 (open)](https://github.com/NousResearch/hermes-agent/issues/26202) – Nice-to-have improvements.

**Overall stability:** The project is actively fixing regressions. Several P2 bugs now have paired fix PRs, indicating a fast response time.

## 6. Feature Requests & Roadmap Signals
Open feature requests from the community that point toward upcoming enhancements:

- **Feishu CardKit streaming** – [#16084](https://github.com/NousResearch/hermes-agent/issues/16084), [#26236](https://github.com/NousResearch/hermes-agent/issues/26236). Multiple users requesting native card rendering for Feishu. Likely candidate for next minor release.
- **User timezone configuration** – [#26255](https://github.com/NousResearch/hermes-agent/issues/26255). Strong concern from users running containers in UTC. Ties into cron scheduling.
- **Platform-aware output formatting** – [#26239](https://github.com/NousResearch/hermes-agent/issues/26239). Would improve cross-platform UX significantly.
- **Session platform filter for WebUI dashboard** – PR [#20242](https://github.com/NousResearch/hermes-agent/pull/20242) is open and addresses user complaints about cron sessions flooding the dashboard.
- **Mouse-aware input and smart arrow keys** – [#26202](https://github.com/NousResearch/hermes-agent/issues/26202). Inspired by Claude Code, this would modernise the TUI experience.

**Predictions:** The next version (likely v0.x) will include at least one Feishu streaming improvement, the timezone configuration, and the session platform filter. The MCP reconnect fix and vision dimension cap are already merged and will be part of the next release.

## 7. User Feedback Summary
Real user pain points and satisfaction signals evidenced by today’s data:

### Pain Points (Explicit in Issues)
- **Output truncation** (#7237) – “frequently throws error … truncates output mid-stream” – critical for chat users. Now closed.
- **Feishu markdown not rendering** (#26174, #26239) – Screenshot shows garbled output; user compares unfavourably with OpenClaw.
- **Custom provider vision failures** (#25594) – Non-vision models receive image_url parts; HTTP 400 error. User expectations for “just works” not met.
- **MacOS gateway restart failure** (#26198) – Service left stopped; degrades user experience on Mac.
- **DeepSeek delegation failure** (#26210) – “always returns HTTP 404” – blocks use of a popular provider for delegation.

### Satisfaction & Positive Signals
- **Fast fix turnaround** – Issues like #26174 (Feishu rendering) were closed within 24 hours of being opened. PR #26266 (non-ASCII in cron) also turned around quickly.
- **Feature PRs from community** – Contributions like #20242 (session filter), #16652 (account limits), and #26263 (Ctrl+J) show an active, engaged contributor base.

### Use Cases Highlighted
- Gateway/multi-platform usage (Telegram, Discord, Slack, Feishu) is clearly a primary deployment mode.
- Custom providers (OpenRouter, DeepSeek, self-hosted) are widely used – support must be robust.
- Long-running tasks via delegation and cron are common; users need non-blocking async patterns.

## 8. Backlog Watch
Issues and PRs that have been open for a while and may need maintainer attention:

- **Feishu streaming card feature** – Issue [#16084](https://github.com/NousResearch/hermes-agent/issues/16084) opened 2026-04-26 (20 days ago). Still open, 6 comments. Though related PRs are not yet merged, this is the most-upvoted open feature request. Should be prioritised given multiple duplicate requests.
- **Session platform filter PR** – [#20242](https://github.com/NousResearch/hermes-agent/pull/20242) opened 2026-05-05 (10 days ago). No merge yet; addresses a clear UX problem. Consider reviewing and merging.
- **Account limits in status bar** – [#16652](https://github.com/NousResearch/hermes-agent/pull/16652) opened 2026-04-27 (18 days ago). Open, no recent activity. Could be stale but adds value.
- **Self-hosted CI workflow** – [#25924](https://github.com/NousResearch/hermes-agent/pull/25924) opened 2026-05-14 (1 day ago), but no discussion yet. Important for fork contributors.

No truly ancient open issues were present in the top 30, which is a positive sign of project health.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Based on your request, here is a structured project digest for PicoClaw, generated from the provided GitHub data.

---

## PicoClaw Project Digest – 2026-05-15

### 1. Today's Overview

PicoClaw exhibits extremely high activity on this date, with 30 pull requests and 10 issues updated in the last 24 hours. The project released a new nightly build (v0.2.8-nightly.20260515), signaling continuous rapid iteration. Key areas of focus include stabilizing the OpenAI-compatible provider layer, fixing reasoning content handling for DeepSeek and MiMo models, and enhancing the web chat streaming experience. A major security feature, the optional Tirith pre-exec command scanner, has been revived, indicating a strong commitment to production-grade security.

### 2. Releases

- **New Release:** **Nightly Build v0.2.8-nightly.20260515.794eb04f** is available.
- **Details:** This is an automated nightly build that may be unstable. It includes all changes on the `main` branch since the last stable release (v0.2.8).
- **Changelog:** The full changelog compares the current `main` branch against the last tag `v0.2.8` ([compare link](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)).
- **Migration/Notes:** Users are advised to use this build with caution. It is best suited for testing upcoming features and fixes but is not recommended for production environments.

### 3. Project Progress

A significant volume of code has been merged today, primarily focused on bug fixes, dependency updates, and feature implementation.

- **Provider and Model Compatibility Fixes:** Critical fixes were merged for the OpenAI-compatible provider. PR [#2862](https://github.com/sipeed/picoclaw/pull/2862) aligns MiMo model reasoning replay with the DeepSeek fix, and PR [#2741](https://github.com/sipeed/picoclaw/pull/2741) hardens streaming response parsing to preserve `reasoning_content` for all compatible providers.
- **Core Functionality & UX:**
    - PR [#2874](https://github.com/sipeed/picoclaw/pull/2874) fixes a bug where images sent via the Pico client were not being properly forwarded.
    - PR [#2587](https://github.com/sipeed/picoclaw/pull/2587) was merged, adding end-to-end streaming support for the new Pico web chat experience with improved scroll behavior.
- **Security & Infrastructure:**
    - A new feature, PR [#2877](https://github.com/sipeed/picoclaw/pull/2877) (replacing older PR [#1932](https://github.com/sipeed/picoclaw/pull/1932)), was opened to add an optional **Tirith** pre-exec command scanner for enhanced security.
    - MCP support was expanded in PR [#2811](https://github.com/sipeed/picoclaw/pull/2811) with support for streamable HTTP, request-response mode, and a new Docker-backed integration test framework.
- **Dependency Updates:** Numerous automated dependency bumps were merged, including updates for Tailwind CSS, various Go libraries, Slack SDK, Vite, and Jotai, keeping the project current and secure.

### 4. Community Hot Topics

The community is actively contributing and reporting issues, with a strong focus on model compatibility and complex use cases.

- **Most Active Issue:** [#2706](https://github.com/sipeed/picoclaw/issues/2706) - **Deepseek v4 thinking model problem.** This issue received the most reactions (👍 1) and generated a detailed technical discussion about how to handle DeepSeek V4's `reasoning_content` field. The issue was closed today, indicating a fix has been applied, likely via PR [#2862](https://github.com/sipeed/picoclaw/pull/2862).
- **Long-standing Bug Fix:** [#629](https://github.com/sipeed/picoclaw/issues/629) - **Didn't retry if meeting LLM call failed.** With 14 comments, this is the most discussed issue. It highlights a major stability pain point where HTTP 500 errors from providers like OpenRouter would cause tasks to hang indefinitely. The community is actively waiting for an automatic retry mechanism.
- **Feature Discussion:** [#2775](https://github.com/sipeed/picoclaw/issues/2775) - **Child Agents inheriting root Agent's AGENT.md.** This issue reflects a complex multi-agent use case where spawned agents (Planner, Builder, etc.) lose their distinct identity. This speaks to a growing need for more sophisticated multi-agent architecture management.

### 5. Bugs & Stability

Here are the bugs reported today, ranked by severity:

- **High: Session History Race (Reopened)** - Issue [#2721](https://github.com/sipeed/picoclaw/issues/2721) reports that a critical race condition causing a `400` error from the Anthropic API (`tool_use_id`) is still present in v0.2.5. This is a **regression of a previously closed issue** (#704) and is a high-priority stability risk. No fix PR has been linked yet.
- **High: MiMo Model Multi-turn Failure** - Issue [#2859](https://github.com/sipeed/picoclaw/issues/2859) describes a `400` error ("Param Incorrect...") occurring after 2-3 conversation turns with the Xiaomi MiMo model. This was closed alongside PR [#2862](https://github.com/sipeed/picoclaw/pull/2862), suggesting the root cause (mishandled reasoning content) has been addressed.
- **Medium: PDF Processing Failure in Telegram** - Issue [#2798](https://github.com/sipeed/picoclaw/issues/2798) reports that attaching a PDF in Telegram breaks the session, while the same PDF works in a similar bot (OpenClaw). This indicates a specific issue within PicoClaw's PDF handling or Telegram channel integration.
- **Low: Conversation History Display** - Issue [#2795](https://github.com/sipeed/picoclaw/issues/2795) reports a UI bug where viewing past conversations only shows the last user message, potentially confusing users.
- **Low: Missing Timestamps in Session API** - Issue [#2787](https://github.com/sipeed/picoclaw/issues/2787) describes a data integrity issue where the Session API doesn't return per-message timestamps, forcing the frontend to use incorrect timestamps.

### 6. Feature Requests & Roadmap Signals

User requests today signal a demand for better multi-agent management, improved data fidelity, and more robust provider support.

- **Strong Signal (Likely in v0.2.9):** The fix for **DeepSeek V4 and MiMo reasoning content** (Issue [#2706](https://github.com/sipeed/picoclaw/issues/2706), PR [#2862](https://github.com/sipeed/picoclaw/pull/2862)) is already merged, making support for these thinking models a core part of the upcoming release.
- **Strong Signal (Likely in v0.3.0):** The merged PR [#2587](https://github.com/sipeed/picoclaw/pull/2587) for **web chat streaming** and the new PR [#2877](https://github.com/sipeed/picoclaw/pull/2877) for **Tirith security scanning** are significant features. The streaming UX is a major step for the web interface, and the security scanning addresses a fundamental safety concern, suggesting a push toward a more polished, enterprise-ready v0.3.0.
- **Moderate Signal:** Issues like [#2775](https://github.com/sipeed/picoclaw/issues/2775) (agent identity inheritance) and [#2702](https://github.com/sipeed/picoclaw/issues/2702) (multi-user attribution) point to a need for more sophisticated **multi-agent and multi-user features**. These are likely to be roadmapped for a future release.
- **Documentation:** PR [#2766](https://github.com/sipeed/picoclaw/pull/2766) is a large documentation update to synchronize with the new V3 config format, showing a focus on improving developer experience.
- **Testing Infrastructure:** PR [#2811](https://github.com/sipeed/picoclaw/pull/2811) introduces a general Docker-backed integration test framework, a strong signal for improved code quality and stability.

### 7. User Feedback Summary

Real user feedback can be extracted from the issues:

- **Pain Point: Provider Instability & Retry Handling:** The high engagement on Issue [#629](https://github.com/sipeed/picoclaw/issues/629) ("Didn't retry if meet LLM call failed") shows deep user dissatisfaction with the system's fragility when upstream providers are unstable. Users need robust retry logic to avoid task hang-ups.
- **Pain Point: Advanced Model Compatibility:** Users are actively trying cutting-edge models like **Deepseek V4** (Issue [#2706](https://github.com/sipeed/picoclaw/issues/2706)) and **Xiaomi MiMo** (Issue [#2859](https://github.com/sipeed/picoclaw/issues/2859)) and hitting failures. This shows a desire for PicoClaw to be the first or best interface for new models, and frustration when it fails.
- **Use Case & Satisfaction:** The PR for **Tirith security scanning** (PR [#2877](https://github.com/sipeed/picoclaw/pull/2877)) is a clear response to a user need for sandboxing and preventing malicious code execution, a sign that the community values safety.
- **Use Case: Complex Multi-User/Multi-Agent Workflows:** Issues like [#2702](https://github.com/sipeed/picoclaw/issues/2702) (multi-user chat) and [#2775](https://github.com/sipeed/picoclaw/issues/2775) (child agent identity) show users are pushing PicoClaw into more complex, collaborative, and structured scenarios, moving beyond simple single-user chat.
- **Satisfaction Indicator:** Issues are being **closed** (4/10) and PRs are being **merged** at a high rate, indicating a responsive maintainer team and a healthy project lifecycle.

### 8. Backlog Watch

The following items appear to be important but are either stale or lack recent maintainer attention.

- **Issue [#629](https://github.com/sipeed/picoclaw/issues/629) - LLM call retry failure (Stale, High Impact):** With 14 comments and no PR linked, this long-standing bug (from 2026-02-22) is a significant source of user frustration. It needs a maintainer to propose a design and implement a fix.
- **Issue [#2702](https://github.com/sipeed/picoclaw/issues/2702) - Multi-user group channel history (Stale, Moderate Impact):** This is a well-defined feature request/bug describing a real-world problem for team usage. It lacks traction and could block adoption in group settings.
- **Issue [#2775](https://github.com/sipeed/picoclaw/issues/2775) - Child Agent role confusion (Stale, Moderate Impact):** This is a critical feature for anyone trying to build complex multi-agent systems. It has low engagement but represents a gap in core architecture.
- **Issue [#2798](https://github.com/sipeed/picoclaw/issues/2798) - PDF Stream Data error (Stale, Medium Impact):** A specific "showstopper" bug for Telegram users who need to share documents. No fix is in progress.
- **Issues [#2795](https://github.com/sipeed/picoclaw/issues/2795) and [#2787](https://github.com/sipeed/picoclaw/issues/2787) - UI/Data fidelity bugs (Stale, Low Impact):** While low severity, these bugs degrade the user experience. They have no discussion or a PR linked, indicating they may be considered low priority.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-15

## 1. Today’s Overview

NanoClaw saw **very high** activity in the last 24 hours: 25 pull requests were updated, of which **13 were merged or closed**, and **12 remain open**. A single new issue was opened, but no new releases were cut. The project continues to mature rapidly, with substantial contributions across bug fixes, new skills (LinkedIn, Reddit, social listening, website auditing), infrastructure hardening (security for approval responses, network access hooks for agents), and parity improvements for the Codex provider. Developer velocity remains strong, though the density of open PRs suggests the maintainers may need to increase review bandwidth.

## 2. Releases

**No new releases** were published today.

---

## 3. Project Progress — Merged/Closed PRs Today

The following 10 significant PRs (out of 13 total merged/closed) represent the day’s completed work:

- **#2450** – [feat(linkedin-ads): add LinkedIn Ads playbook skills for Ads group](https://github.com/nanocoai/nanoclaw/pull/2450)  
  New operational skills for LinkedIn Ads management.

- **#2473** – [fix(destinations): remove misleading scratchpad clause from internal-tag description](https://github.com/nanocoai/nanoclaw/pull/2473)  
  Corrects a prompt contradiction that confused agents about `<internal>` tag usage.

- **#2454** – [docs(onecli): add vault secrets reference](https://github.com/nanocoai/nanoclaw/pull/2454)  
  Single-source-of-truth table for the OneCLI vault, linked from `CLAUDE.md`.

- **#2453** – [feat(copy-grader): localize copy-grader skill from upstream](https://github.com/nanocoai/nanoclaw/pull/2453)  
  Localizes the Ogilvy-inspired marketing-copy grader to survive upstream removal.

- **#2448** – [feat(social-listening): add composite social-listening skill](https://github.com/nanocoai/nanoclaw/pull/2448)  
  Parallel dispatch across Serper, Reddit MCP, Brave Search, RSS, and WebSearch with deduplication.

- **#2449** – [feat(linkedin-community): add agent-browser-based LinkedIn community manager skill](https://github.com/nanocoai/nanoclaw/pull/2449)  
  Agent-browser-driven organic LinkedIn operations (post, reply, engage, triage).

- **#2452** – [feat(container): add lighthouse CLI for site audits](https://github.com/nanocoai/nanoclaw/pull/2452)  
  Pins Lighthouse 13.3.0 in the container, reusing existing Chromium.

- **#2451** – [feat(audit-website): localize audit-website skill from upstream](https://github.com/nanocoai/nanoclaw/pull/2451)  
  Clones the squirrelscan-based audit skill verbatim into local skill catalog.

- **#2455** – [feat(audit-website): composite local audit stack (Lighthouse + axe + linkinator)](https://github.com/nanocoai/nanoclaw/pull/2455)  
  Replaces external squirrelscan with a self-hosted Node tool stack to bypass Cloudflare AI protections.

- **#2447** – [feat(reddit): add read-only Reddit MCP and /reddit-research skill](https://github.com/nanocoai/nanoclaw/pull/2447)  
  New read-only Reddit access via `reddit-mcp-buddy` and four research playbooks.

---

## 4. Community Hot Topics

The only issue updated today is **#2480** (0 comments, 0 reactions), but several open PRs attracted attention:

- **#2481** – [fix(cron): stop self-suppressing cron output across all agents](https://github.com/nanocoai/nanoclaw/pull/2481)  
  Two independent bugs caused cron firings to be acked but never delivered. This fix addresses a common “crons not running” symptom that frustrated operators.

- **#2478** – [security: fix(approvals): require admin for approval responses](https://github.com/nanocoai/nanoclaw/pull/2478)  
  Hardens approval flow so that non-admin users cannot resolve approvals even if they possess a valid `questionId`. A critical security improvement.

- **#2475** – [feat(codex): surface skills + persona to codex agents (parity with Claude)](https://github.com/nanocoai/nanoclaw/pull/2475)  
  Enables Codex agents to see the same persona and skill catalog as Claude Code agents, reducing content rewrite when switching providers.

- **#2477** – [feat(network): hooks to allow skills to regulate agents' internet access](https://github.com/nanocoai/nanoclaw/pull/2477)  
  A new feature skill that gives agents fine-grained control over their own network access, addressing compliance and security use cases.

The underlying need across these PRs is **production reliability** (cron delivery, security), **provider parity** (Codex vs. Claude), and **agent autonomy** (network self-regulation).

---

## 5. Bugs & Stability

| Severity | Bug / Issue | Status | Notes |
|----------|-------------|--------|-------|
| **Critical** | **#2480** – Docker Desktop on Linux: container crashes on fresh install (exit code 1) due to three stacked bugs | Open, 0 comments | Syptom: “Claude Code native binary not found at /pnpm/claude”. No fix PR yet; likely requires installation script refinements or documentation fix. |
| **High** | **#2481** – Cron output self-suppression (“lobby silence” + internal silent tag) | Fix PR open | Agents woke up and processed tasks but output was dropped or self-silenced. The fix is under review. |
| **High** | **#2478** – Approval response bypass (non-admin can resolve approvals) | Fix PR open | Security vulnerability; requires admin role check. |
| **Medium** | **#2469** – WhatsApp decrypt failures and 401 logout: recovery guidance is wrong | Fix PR open | Current instructions tell operators to `launchctl kickstart` which doesn't repair session corruption. Updated guidance. |
| **Medium** | **#2473** – Misleading scratchpad clause in `<internal>` tag description (merged today) | Fixed | Contradicted system prompt; now corrected. |

**Overall assessment**: The project is experiencing real stability pains around Docker setup and cron reliability, but both have active fix attempts. The approval security issue is a serious but contained vulnerability.

---

## 6. Feature Requests & Roadmap Signals

Several open PRs indicate user-driven or community-driven feature additions that are likely to land in the next minor release:

- **Provider-agnostic setup**: [#2474](https://github.com/nanocoai/nanoclaw/pull/2474) introduces a CLI picker to choose Claude Code or Codex during setup, with future support for Aider, Gemini-CLI, etc.
- **Slack session improvements**: [#2472](https://github.com/nanocoai/nanoclaw/pull/2472) and [#2471](https://github.com/nanocoai/nanoclaw/pull/2471) fix per-thread session collapsing in Slack DMs and add an adapter hook for platform-specific threadId rewriting.
- **Agent internet access control**: [#2477](https://github.com/nanocoai/nanoclaw/pull/2477) adds hooks for skills to regulate network access, a strong signal for enterprise/compliance needs.
- **Codex parity**: [#2475](https://github.com/nanocoai/nanoclaw/pull/2475) is a clear roadmap item to make Codex a first-class provider equal to Claude Code.

**Prediction**: The next release (likely v2.x) will include the setup CLI picker, Slack thread fixes, and the Codex parity changes, given the high volume of PRs targeting these areas.

---

## 7. User Feedback Summary

While explicit user comments are scarce (the only issue #2480 has no discussion yet), the PRs and their descriptions reveal real-world pain points:

| Pain Point | Evidence | User Sentiment |
|------------|----------|----------------|
| Docker on Linux fails out of the box | Issue #2480 (fresh install crash) | Frustration – immediate exit code 1 |
| Scheduled tasks appear to not run | PR #2481 (cron output swallowed) | Confusion – operators thought crons were failing |
| WhatsApp recovery instructions wrong | PR #2469 (invalid guidance) | Impediment – operators couldn't restore connectivity |
| Security concern with approval bypass | PR #2478 (non-admin can resolve) | Urgent – trust model broken |
| Blocked by Cloudflare when using external audit tools | PR #2455 (replace squirrelscan with self-hosted stack) | Workaround – switch to local tooling |
| Need Codex as viable provider | PR #2475 (skill/persona parity) | Active demand – want choice of AI backend |

Overall, users seem satisfied with the project's rapid iteration but are experiencing friction in initial setup and production reliability. The community is actively contributing fixes, which is a healthy sign.

---

## 8. Backlog Watch

No stale or long-unanswered issues were identified in the last 24 hours. The only open issue (#2480) was created today. No PRs have been left without updates for more than a day. The project’s maintainers and community are keeping the backlog current. However, with **12 open PRs** awaiting review, there is a risk that review latency could become a bottleneck if maintainer bandwidth doesn’t scale.

---

*Generated from GitHub data snapshot dated 2026-05-15.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-15

## Today's Overview
IronClaw remains in a period of exceptionally high activity, driven by the **Reborn architecture** re‑architecture effort. In the last 24 hours, 50 issues and 50 pull requests were updated, and a new patch release `v0.28.2` was published. 48 issues are currently open, and 22 PRs were merged or closed today, reflecting steady progress across storage refactoring, trust policies, and the WebUI beta. The community continues to organise Reborn work through large coordination epics, while several user-facing bugs have been reported that may affect stability.

## Releases
**ironclaw-v0.28.2** (2026-05-14)

### Fixed
- Restored chat‑driven `tool_install` functionality that regressed in the May 8–13 window ([#3559](https://github.com/nearai/ironclaw/pull/3559)).
- Addressed a double‑invocation of tool install and an auto‑approve footgun in the extensions subsystem.

### Changed
- LLM provider‑specific authentication, model fetching, and embeddings configuration are now hidden behind facades ([#3416](https://github.com/nearai/ironclaw/pull/3416) – URL truncated in source). This reduces coupling for future provider additions.

**Migration notes:** No breaking changes are mentioned; the patch should be a drop‑in upgrade. Downstream consumers still pinned to `0.24.0` (see issue #3259) will need to wait for a crates.io publish to benefit.

## Project Progress
22 PRs were merged/closed today. Notable changes:

- **Canary reliability** – `fix(canary): accurate test counts, chat-install probe, strict xfails` ([#3682](https://github.com/nearai/ironclaw/pull/3682)) patches the CI pipeline to catch regressions like the tool_install bug that slipped past for five days.
- **Universal filesystem dispatch** – A large refactoring closed multiple stacked PRs that migrate consumer crates to the unified `RootFilesystem` surface:
  - `feat(reborn): apply universal FS dispatch across consumer crates` ([#3679](https://github.com/nearai/ironclaw/pull/3679)) – +15k LOC across 61 files.
  - Dissolved the `ironclaw_storage` crate and replaced `BlobStorage` with the new surface ([#3678](https://github.com/nearai/ironclaw/pull/3678)).
  - `feat(authorization): route FilesystemCapabilityLeaseStore through unified put/get` ([#3671](https://github.com/nearai/ironclaw/pull/3671)), `feat(run-state): unified put/get for filesystem stores` ([#3672](https://github.com/nearai/ironclaw/pull/3672)), and `feat(outbound): FilesystemOutboundStateStore on the unified surface` ([#3670](https://github.com/nearai/ironclaw/pull/3670)).
- **Reborn trust policy** – `fix(trust): make default host policy explicitly fail closed` ([#3638](https://github.com/nearai/ironclaw/pull/3638)) removes ambiguity in `HostTrustPolicy`.
- **WebUI beta** – `feat(webui): add RebornServices facade` ([#3664](https://github.com/nearai/ironclaw/pull/3664)) exposes stable DTOs and contract tests.
- **HTTP egress tool** – `feat(reborn): add first-party HTTP egress tool` ([#3681](https://github.com/nearai/ironclaw/pull/3681)) introduces a built‑in `builtin.http` capability.
- **Telegram v2 inbound tracer** – `feat(reborn): Telegram v2 inbound tracer (webhook → ledger + binding, no reply)` ([#3590](https://github.com/nearai/ironclaw/pull/3590)) lands the first Reborn ProductAdapter for a real channel.

Several issues were also closed, including the browser chat route migration ([#3282](https://github.com/nearai/ironclaw/issues/3282)) and the WebUI inbound DTO contract definition ([#3624](https://github.com/nearai/ironclaw/issues/3624)).

## Community Hot Topics
The most active discussions continue to revolve around the Reborn architecture:

- **EPIC: Track Reborn architecture landing strategy and grouped PR plan** ([#2987](https://github.com/nearai/ironclaw/issues/2987)) – 44 comments. This is the master coordination issue for the entire Reborn cutover. It defines landing phases, PR grouping, and the checklist for the eventual `reborn-integration → staging` merge.
- **Reborn cutover blocker: add event substrate integration tests** ([#3022](https://github.com/nearai/ironclaw/issues/3022)) – 9 comments. Defines the cross‑service test suite needed before user‑visible Reborn activation.
- **Publish 0.25.0–0.27.0 to crates.io** ([#3259](https://github.com/nearai/ironclaw/issues/3259)) – 4 comments. Downstream consumers are stuck on `0.24.0` due to wasmtime CVEs; the community is pushing for newer releases on crates.io.
- **Configuration‑as‑Code for Reborn** ([#3036](https://github.com/nearai/ironclaw/issues/3036)) – 3 comments, 1 👍. Operators want declarative tenant blueprints instead of hand‑editing `.env` and JSON config files.

Underlying need: The community is actively preparing for the “Reborn” architecture to go live, and both developers and operators are calling for better testing, packaging, and declarative configuration before cutover.

## Bugs & Stability
Several bugs were reported today, ranked by severity:

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| High | [#3673](https://github.com/nearai/ironclaw/issues/3673) | `openai_compatible` provider drops `reasoning_content` on outgoing requests, breaking DeepSeek v4‑pro multi‑turn tool calls. | No fix PR yet. |
| Medium | [#3675](https://github.com/nearai/ironclaw/issues/3675) | TUI cannot render Markdown tables; table syntax appears as plain text. | No fix PR yet. |
| Low | [#3447](https://github.com/nearai/ironclaw/issues/3447) | Nightly E2E scheduled run failed (commit `faf2ed4465`). Failure in Full E2E / E2E (features). | Likely being addressed by the canary fixes in #3682, but not closed. |

An older but still open bug: **Telegram not working for NEAR Foundation instance** ([#2902](https://github.com/nearai/ironclaw/issues/2902)) – only 1 comment, no resolution since April 23. The Telegram v2 inbound tracer PR (#3590) may eventually supersede this.

The release v0.28.2 fixes the critical chat‑driven `tool_install` regression that had been slipping through canary tests.

## Feature Requests & Roadmap Signals
The roadmap is overwhelmingly driven by the Reborn initiative. The following requests are likely to land in the next release (0.28.3 or 0.29.0):

- **Reborn WebUI Beta** – Multiple P0 issues (e.g. [#3611](https://github.com/nearai/ironclaw/issues/3611)) define minimal native WebChat v2 routes, inbound DTO contracts, and a `BeforeInboundPolicy` seam ([#3623](https://github.com/nearai/ironclaw/issues/3623)). The facade (#3664) is already merged.
- **First‑class loop hooks framework** – [#3524](https://github.com/nearai/ironclaw/issues/3524) and [#3523](https://github.com/nearai/ironclaw/issues/3523) define inline hooks and a production gate‑ref factory. The foundation PR ([#3573](https://github.com/nearai/ironclaw/pull/3573)) is still open but has successor drafts.
- **Channel porting to Reborn** – Issues track ports for Telegram ([#3581](https://github.com/nearai/ironclaw/issues/3581)), Slack ([#3579](https://github.com/nearai/ironclaw/issues/3579)), WeChat ([#3582](https://github.com/nearai/ironclaw/issues/3582)), and the Web Gateway ([#3580](https://github.com/nearai/ironclaw/issues/3580)). Telegram v2 is the first to land (PR #3590).
- **Host‑owned ingress contracts** – [#3678](https://github.com/nearai/ironclaw/issues/3578) and PR [#3683](https://github.com/nearai/ironclaw/pull/3683) add explicit route descriptors for Reborn HTTP surfaces.

The Configuration‑as‑Code epic ([#3036](https://github.com/nearai/ironclaw/issues/3036)) is a user‑requested feature that may gain traction once Reborn stabilises.

## User Feedback Summary
Real user pain points expressed through issues:

- **crates.io lag** (#3259): Downstream Rust consumers cannot update beyond `0.24.0` because newer tags are not published. This blocks users who depend on the `ironclaw` crate for library integration.
- **DeepSeek tool‑call breakage** (#3673): A specific LLM provider (DeepSeek v4‑pro) fails in multi‑turn scenarios due to dropped `reasoning_content`. This affects users who customise the OpenAI‑compatible backend.
- **TUI rendering defect** (#3675): The terminal UI displays raw Markdown tables, making tool output unreadable. Usability regression for CLI users.
- **Telegram outage** (#2902): The NEAR Foundation deployment cannot use Telegram. No resolution in 22 days, though the Reborn port may be the long‑term fix.

Satisfaction signals are limited; the community appears focused on engineering work rather than expressing satisfaction. The release note for v0.28.2 and the canary fixes (#3682) indicate that the team is responsive to regressions.

## Backlog Watch
Issues and PRs that have been open for an extended period with no recent maintainer action:

- **Telegram not working for NEAR Foundation** ([#2902](https://github.com/nearai/ironclaw/issues/2902)) – open since April 23, only 1 comment. The Telegram v2 port may address it, but no direct fix has been communicated.
- **Publish 0.25.0–0.27.0 to crates.io** ([#3259](https://github.com/nearai/ironclaw/issues/3259)) – open since May 5, 4 comments, no response from maintainers. The release v0.28.2 exists on GitHub but still absent from crates.io.
- **Nightly E2E failure** ([#3447](https://github.com/nearai/ironclaw/issues/3447)) – reported May 10, with multiple failures (re‑opened after each nightly?). Though the canary PR (#3682) aims to improve detection, the specific failure root cause has not been publicly addressed.

These items represent risks for community trust and operational stability. A maintainer acknowledgment or timeline would be beneficial.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-15

## 1. Today's Overview
LobsterAI saw an extremely high-activity day, with **37 PRs updated** in the last 24 hours—**33** of which were merged or closed. This surge reflects a significant batch processing of accumulated backlog items, including many stale PRs from late March and April being finalized. A single new release, **v2026.5.14**, shipped yesterday with collaborative coding and plugin management enhancements. The issue tracker remains light, with only **1 open/active issue** filed today regarding a model-calling regression. Overall, the project is in a **rapid consolidation phase**, clearing technical debt and landing long-pending features.

## 2. Releases
**New Release: [LobsterAI 2026.5.14](https://github.com/netease-youdao/LobsterAI/releases/tag/v2026.5.14)**  
**What's Changed:**
- **feat(cowork):** Improved OpenClaw context compaction handling (PR #1969 – @liuzhq1986)
- **feat(plugins):** Added plugin management with advanced configuration (PR #1963 – @btc69m979y-dotcom)
- Additional fixes by @liuzhq1986 (details in full changelog)

**🐛 Breaking/Migration Notes:**  
The changelog is truncated in the provided data, but the one critical regression reported today (Issue #1988) is directly linked to this release — users of Alibaba Bailian's `qwen3.6-plus` model report that the update forces the use of NetEase's built-in model, causing authentication failures. **If you use third-party model providers, hold this update or patch the model routing config manually** until a hotfix is confirmed.

## 3. Project Progress
Of the 37 PRs updated, **33 were merged/closed**. Key themes:

### Feature Landings & Advanced Features
- **[PR #1963](https://github.com/netease-youdao/LobsterAI/pull/1963)** (merged/closed) – Plugin management with advanced config (shipped in v2026.5.14)
- **[PR #1943](https://github.com/netease-youdao/LobsterAI/pull/1943)** (merged/closed) – Memory settings tab refactor + Dreaming content display (Tab-based UI for memory items, embedding search, and Dreaming diary)
- **[PR #1185](https://github.com/netease-youdao/LobsterAI/pull/1185)** (merged/closed) – "Open skill folder" button for user-installed skills
- **[PR #835](https://github.com/netease-youdao/LobsterAI/pull/835)** (merged/closed) – JSON paste mode for batch MCP server creation (supports Claude Desktop config formats)

### Security & Stability Fixes
- **[PR #828](https://github.com/netease-youdao/LobsterAI/pull/828)** (merged/closed) – Prevent path traversal in `localfile://` protocol handler (critical vulnerability fix)
- **[PR #826](https://github.com/netease-youdao/LobsterAI/pull/826)** (merged/closed) – URL protocol validation for `shell.openExternal`
- **[PR #822](https://github.com/netease-youdao/LobsterAI/pull/822)** (merged/closed) – Unify token refresh locking to eliminate race conditions
- **[PR #1190](https://github.com/netease-youdao/LobsterAI/pull/1190)** (merged/closed) – Force-close app before Windows uninstall (prevents ghost processes)
- **[PR #1962](https://github.com/netease-youdao/LobsterAI/pull/1962)** (merged/closed) – `nsp-clawguard` security monitoring plugin hot-toggle in Settings
- **[PR #830](https://github.com/netease-youdao/LobsterAI/pull/830)** (merged/closed) – SQLite performance optimization (WAL mode, larger cache, temp-store tuning)

### Performance & UX
- **[PR #1186](https://github.com/netease-youdao/LobsterAI/pull/1186)** (merged/closed) – Optimized streaming response rendering (eliminated full-list re-render on every 90ms tick)
- **[PR #806](https://github.com/netease-youdao/LobsterAI/pull/806)** (open, stale) – SQL index for session & message query performance (still open, newly updated)
- **[PR #1944](https://github.com/netease-youdao/LobsterAI/pull/1944)** (merged/closed) – Fix code block background not extending on horizontal scroll

### IM & Platform Integration
- **[PR #1987](https://github.com/netease-youdao/LobsterAI/pull/1987)** (merged/closed) – Added pairing code input boxes for Telegram/Discord/QQ/POPO (fixed missing approval UI)
- **[PR #838](https://github.com/netease-youdao/LobsterAI/pull/838)** (merged/closed) – Per-channel model override for IM bot sessions
- **[PR #1986](https://github.com/netease-youdao/LobsterAI/pull/1986)** (merged/closed) – Fix managed session sync losing duplicate characters (e.g., `file:///` → `file://`)

### Skill & Install Duplication
- **[PR #827](https://github.com/netease-youdao/LobsterAI/pull/827)** (merged/closed) – Prevent duplicate skill installation
- **[PR #836](https://github.com/netease-youdao/LobsterAI/pull/836)** (merged/closed) – Handle duplicate local skill imports with content fingerprinting

## 4. Community Hot Topics
### Most Active Issue
- **[Issue #1988](https://github.com/netease-youdao/LobsterAI/issues/1988)** – "模型调用问题：lobsterai版本更新后，阿里百炼coding plan无法正常调用qwen3.6-plus"  
  *(Model call issue: after update, Alibaba Bailian coding plan cannot call qwen3.6-plus properly)*  
  **Author:** nee207 | **Comments:** 1 | **Updated:** 2026-05-15  
  **Analysis:** The user reports that **only the qwen3.6-plus model** is being forcibly routed to NetEase's built-in provider (causing quota errors), while other models work fine. Configuration file changes are also overridden by the system. This suggests a **model-mapping or provider-routing regression** introduced in v2026.5.14, possibly related to the context compaction changes (PR #1969) or plugin management. The underlying need is clear: users want **model selection freedom** without provider lock-in.

### Most Active PR (by comment count)
The data does not provide comment counts for individual PRs, but the **most structurally active** is **[PR #1985](https://github.com/netease-youdao/LobsterAI/pull/1985)** (still open) — it adds "Thinking Level" control (Off/Minimal/Low/Medium/High/Adaptive) to chat sessions, a new feature that is generating interest among the developer community.

## 5. Bugs & Stability
### 🔴 Critical (P0)
- **[Issue #1988](https://github.com/netease-youdao/LobsterAI/issues/1988)** – Model routing regression after v2026.5.14. Qwen3.6-plus forcibly redirects to NetEase provider. No known fix PR yet. **Impact:** Blocks users of Alibaba Bailian for that specific model. Workaround: downgrade or configure manually.

### 🟡 Medium (Fixed Today)
- **[PR #1986](https://github.com/netease-youdao/LobsterAI/pull/1986)** – Managed session sync losing duplicate characters (`file:///` → `file://`, `.pptx` → `.ptx`). **Fixed in today's batch.**
- **[PR #1967](https://github.com/netease-youdao/LobsterAI/pull/1967)** – Legacy URLs and docs removed (accidentally pushed by ClaudeCode — cleanup merged).

### 🟢 Low (Already Merged)
- **Path traversal** (PR #828) – Critical vulnerability **already patched and merged**.
- **Windows uninstall ghost process** (PR #1190) – Fixed.
- **Security protocol validation** (PR #826) – Fixed.

## 6. Feature Requests & Roadmap Signals
### Top Signals from Today's Activity
1. **Thinking Level Control (PR #1985):** A new dropdown for controlling AI "thinking depth" per session. This is still **open** and represents a significant UX evolution — likely targeting a future release (possibly v2026.6.x). Community demand for fine-grained model reasoning control is strong.
2. **Plugin Management (PR #1963):** Shipped in v2026.5.14. This formalizes the plugin ecosystem, suggesting LobsterAI is moving toward **extensibility** as a core differentiator.
3. **Per-Channel Model Override (PR #838):** Merged today. Enables IM bot operators to pin different models per channel (DingTalk, Feishu, Telegram, etc.) — a **high-demand capability** for multi-channel ops teams.
4. **Batch MCP Server Creation (PR #835):** JSON paste mode merged. Users can now bulk-import MCP servers from Claude Desktop configs — signals **interoperability** with the broader AI tool ecosystem.
5. **Memory & Dreaming Refactor (PR #1943):** Tab-based memory settings with dreaming content display — suggests **memory management** is maturing beyond basic storage.

**Prediction:** The next minor release (2026.5.x) will likely include:
- Hotfix for Issue #1988 (model routing regression)
- Thinking Level control (if PR #1985 is finalized)
- Further plugin API enhancements

## 7. User Feedback Summary
### Real Pain Points Expressed
- **"Forced model provider routing"** (Issue #1988): "更新后，qwen3.6-plus模型会强制调用网易自带的并提示没有额度" — A user on Alibaba Bailian cannot use their preferred model because the system overrides their config. This indicates frustration with **perceived lock-in** to NetEase's ecosystem.
- **Workflow transparency:** The user explicitly attempted to modify the config file but "系统会强制改成错误的" (system forces it back to wrong values), suggesting a **lack of user control** in the model selection UI.

### Satisfaction Signals
- The massive **batch closure of 33 PRs** (including many from March/April) suggests maintainers are responsive to long-standing issues. Users waiting for IM pairing code input (PR #1987), skill deduplication (PR #827, #836), and performance optimizations (PR #806, #830) are now served.
- **Security-conscious users** will appreciate the three security fixes merged today (path traversal, URL protocol validation, token refresh race condition).

## 8. Backlog Watch
### ⏳ Open Items Needing Maintainer Attention
| Item | Created | Status | Summary | Why It Matters |
|------|---------|--------|---------|----------------|
| **[PR #806](https://github.com/netease-youdao/LobsterAI/pull/806)** | 2026-03-25 | Open (stale) | SQL index for session & message query performance | **User impact:** "会话列表加载缓慢（置顶排序全表扫描）" — slow session list loading. This has been open for 51 days; despite being updated today, it's still not merged. The SQLite optimization (PR #830) was merged instead, but this PR adds specific indices. |
| **[PR #807](https://github.com/netease-youdao/LobsterAI/pull/807)** | 2026-03-25 | Open (stale) | `executionMode` config not working (always defaults to local) | **User impact:** "设置中选择 auto 或 sandbox 模式后，实际仍按 local 模式运行" — users cannot switch execution modes. This is a **functional usability bug** that has lingered for 51 days. |
| **[PR #1985](https://github.com/netease-youdao/LobsterAI/pull/1985)** | 2026-05-15 | Open (active) | Thinking Level control for chat sessions | New feature, expected to be prioritized for next release. |

**⚠️ Watch List:** The two stale PRs (#806, #807) were updated today but remain unmerged — they may be candidates for **maintainer decision** (merge, close, or assign to a new owner). Both address real user pain points reported since March.

---

*Digest generated: 2026-05-15 | Source: github.com/netease-youdao/LobsterAI*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-15

## Today's Overview
Activity on the Moltis repository was minimal over the past 24 hours. A single bug issue was opened and remains active, with no pull requests or new releases recorded. The project appears to be in a low‑activity phase, with the development team likely focusing on ongoing work outside the public repository. The absence of merged PRs or closed issues suggests no immediate fixes or features landed today.

## Releases
No new releases were published in the last 24 hours.

## Project Progress
**Merged/Closed PRs (last 24h):** None.  
No pull requests were updated, merged, or closed today. No features or fixes were advanced.

## Community Hot Topics
Only one issue was active in the reporting period:

- **[Bug] Generated TLS certificates only work for localhost, contrary to the docs** [#996](https://github.com/moltis-org/moltis/issues/996)  
  *Author:* IlyaBizyaev — *Created:* 2026-05-14 — *Comments:* 0 — *👍:* 0  
  *Summary:* The reporter states that TLS certificates generated by Moltis are only valid for `localhost`, while the documentation claims they should work for all standard use cases. No community reactions or comments have been posted yet, but the topic may gain attention once users encounter the same limitation. The underlying need is for correct, documented certificate behavior in production‑like environments.

## Bugs & Stability
**Severity: Medium**  
One new bug was reported today:

- **#996 — TLS certificates scoped to localhost only**  
  The issue contradicts the documentation, which promises broader support. While not a crash or security vulnerability, it undermines trust in the tool’s configuration and could block users who rely on custom hostnames or IPs. No fix PR or maintainer response exists yet.

## Feature Requests & Roadmap Signals
No explicit feature requests were raised in the last 24 hours. The only signal from #996 is a request for the documented certificate behavior to be implemented. If fixed, this would improve the self‑signed certificate generation module. Likely not in the next minor version unless a quick patch is prepared.

## User Feedback Summary
The sole user interaction today is a bug report (IlyaBizyaev). The pain point is clear: a mismatch between documentation and actual behavior regarding TLS certificates. The user appears dissatisfied that the tool does not work as advertised, but no broader sentiment data (e.g., praise or multiple complaints) is available. This single report highlights a potential gap in testing or validation of generated certificates.

## Backlog Watch
No long‑unanswered issues or PRs were present in today’s data. The only open item, #996, was created less than 24 hours ago, so no maintainer attention is overdue. However, given the lack of any response, team members should acknowledge the report soon to prevent user frustration.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-15

## 1. Today's Overview

The CoPaw project is in an **extremely active** state with 40 issues updated and 50 pull requests updated in the last 24 hours. Of the PRs, **33 were merged or closed**, indicating a strong cadence of incoming fixes and features. The project maintains **29 open/active issues**, many of which are structured test-coverage milestones and critical bug reports. No new releases were published today; the latest tag remains v1.1.7b1. Activity is concentrated on backend unit test completion (a multi-phase milestone), channel integration fixes (DingTalk, WeChat, Matrix), security hardening, and browser automation stability.

## 2. Releases

**None.** The latest release is v1.1.7b1 (presumed prior to 2026-05-15). No new version or changelog was published in the last 24 hours.

## 3. Project Progress

The **33 merged/closed PRs** cover a broad range of improvements:

- **Security hardening**: PR [#4409](https://github.com/agentscope-ai/QwenPaw/pull/4409) adds HMAC signing and validation for backup archives, blocks unauthenticated remote access, and introduces trust controls for backup import/restore. PR [#4422](https://github.com/agentscope-ai/QwenPaw/pull/4422) adds a spam gate that auto-closes issues/PRs when open count exceeds 10, helping contain AI-generated noise.
- **Plan mode**: PR [#4198](https://github.com/agentscope-ai/QwenPaw/pull/4198) strengthens plan reaffirmation by fixing a gate bypass where non-plan tools could execute before user confirmation. PR [#3787](https://github.com/agentscope-ai/QwenPaw/pull/3787) resets `ssePlanRef` on panel reopen to preserve latest plan state.
- **DingTalk channel**: PR [#4420](https://github.com/agentscope-ai/QwenPaw/pull/4420) refactors the DingTalk channel to remove legacy synchronous reply paths and unify message processing, adding streaming card support.
- **Skill scanner**: PRs [#1580](https://github.com/agentscope-ai/QwenPaw/pull/1580) and [#1581](https://github.com/agentscope-ai/QwenPaw/pull/1581) add YARA and consistency analyzers to the skill scanner, improving security analysis for user-contributed skills.
- **Dependencies**: PR [#4419](https://github.com/agentscope-ai/QwenPaw/pull/4419) upgrades `agentscope` to 1.0.20 and removes the now-unnecessary MCP JSON schema monkey-patch.
- **Documentation**: PR [#4424](https://github.com/agentscope-ai/QwenPaw/pull/4424) updates the project roadmap for May development.
- **CI fixes**: PR [#4426](https://github.com/agentscope-ai/QwenPaw/pull/4426) is a CI test update.

Additionally, several open PRs are under review, including custom base URL for Anthropic ([#4387](https://github.com/agentscope-ai/QwenPaw/pull/4387)), custom headers editor and Anthropic auth token support ([#4413](https://github.com/agentscope-ai/QwenPaw/pull/4413)), and per-model `max_tokens` configuration ([#4417](https://github.com/agentscope-ai/QwenPaw/pull/4417)).

## 4. Community Hot Topics

The most active issues by comment count (7+ comments) reflect both critical bugs and planned improvements:

- **[#4342 (11 comments)](https://github.com/agentscope-ai/QwenPaw/issues/4342)** — Test coverage for `local_models/`, `providers/`, `tunnel/`, `utils/` (Phase 5). Strong community interest in completing the backend unit test milestone.
- **[#3957 (8 comments)](https://github.com/agentscope-ai/QwenPaw/issues/3957)** — Closed bug: agent workspace switches incorrectly when receiving messages via channel. Users experienced identity confusion; root cause was addressed and issue closed.
- **[#4299 (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/4299)** — `write_file()` infinite loop error when output is long. Recurring complaint affecting multi-turn file writing.
- **[#1516 (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/1516)** — AudioContent not supported in Telegram channel. Long-standing request (since March 15) still open.
- **[#4314 (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/4314)** — Closed bug: MiMo thinking mode + tool calls return 400 due to missing `reasoning_content`. Critical for users of Xiaomi's MiMo model.
- **[#2953 (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/2953)** — Closed bug: wrong info printed after `copaw app` start. Cosmetic but reported from first release.

Other notable: [#4421 (4 comments)](https://github.com/agentscope-ai/QwenPaw/issues/4421) — Channel configuration written in plaintext to agent-readable directory (security vulnerability, closed today), [#4360 (5 comments)](https://github.com/agentscope-ai/QwenPaw/issues/4360) — Browser CDP mode fails on Ubuntu 26.04, [#4018 (5 comments)](https://github.com/agentscope-ai/QwenPaw/issues/4018) — embedding config reset on update.

**Underlying needs**: Users want robust multi-channel messaging with proper context isolation, stable file generation, and secure configuration handling.

## 5. Bugs & Stability

**Severity: High**

- **Plaintext channel credentials** ([#4421](https://github.com/agentscope-ai/QwenPaw/issues/4421)) — Channel configuration (including sensitive tokens) is written to the agent-readable workspace directory. Issue closed today; a fix PR [#4409](https://github.com/agentscope-ai/QwenPaw/pull/4409) addresses backup security but not necessarily the plaintext storage itself. No explicit fix PR linked to #4421; may be under review.
- **`write_file()` infinite loop** ([#4299](https://github.com/agentscope-ai/QwenPaw/issues/4299)) — When output is long, the function errors with missing positional argument, causing agent to loop. No fix PR yet; remains open.
- **MiMo thinking mode 400 error** ([#4314](https://github.com/agentscope-ai/QwenPaw/issues/4314)) — Multi-turn chat with tool calls fails when MiMo thinking mode is enabled. Closed; likely fixed by a recent PR.
- **Browser CDP timeout on Ubuntu 26.04** ([#4360](https://github.com/agentscope-ai/QwenPaw/issues/4360)) — Zero success rate connecting to Chrome CDP. No fix PR yet; remains open.
- **Browser CDP timeout causing agent freeze** ([#4309](https://github.com/agentscope-ai/QwenPaw/issues/4309)) — Listed, closed; a fix may exist.

**Severity: Medium**

- **AudioContent unsupported in Telegram** ([#1516](https://github.com/agentscope-ai/QwenPaw/issues/1516)) — Voice messages cannot be processed. Open since March 15.
- **Anthropic API fails with `file` content type** ([#2751](https://github.com/agentscope-ai/QwenPaw/issues/2751)) — `send_file_to_user` results in a 400 error. Open since April 1.
- **Model detection misclassifies vision models** ([#3259](https://github.com/agentscope-ai/QwenPaw/issues/3259)) — Zhipu GLM-4.6V-Flash treated as text-only. Open since April 11.
- **chromadb Rust binding segfault** ([#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854)) — Process crash on Ubuntu 25.10. Open since April 27.

**Severity: Low**

- Wrong startup info ([#2953](https://github.com/agentscope-ai/QwenPaw/issues/2953)), workspace switch confusion ([#3957]), both closed.

## 6. Feature Requests & Roadmap Signals

The following user-requested features or enhancements are under active discussion or development:

- **Built-in plugin discoverability** ([#4406](https://github.com/agentscope-ai/QwenPaw/issues/4406)) — Users want to list and install first-party plugins (cloudpaw, qwen-image, etc.) with the same ease as built-in skills. Likely to appear in next minor release given existing plugin infrastructure.
- **Cleaner workspace default files** ([#4408](https://github.com/agentscope-ai/QwenPaw/issues/4408)) — Suggestion to organize defaults under `.qwenpaw` directory for tidiness. Low effort, high polish.
- **DingTalk quoted message reading** ([#3109](https://github.com/agentscope-ai/QwenPaw/issues/3109)) — Support for reading referenced messages in DingTalk group chats.
- **Tracing / observability** ([#4114](https://github.com/agentscope-ai/QwenPaw/issues/4114)) — User asks about link tracing; no official plan yet.
- **Per-model `max_tokens` and `max_input_length`** ([#4417 PR](https://github.com/agentscope-ai/QwenPaw/pull/4417)) — Under review; expected to land soon.
- **Custom base URL for Anthropic** ([#4387 PR](https://github.com/agentscope-ai/QwenPaw/pull/4387)) — Under review; enables use of Anthropic-compatible proxies.
- **GitHub Copilot provider** ([#3846 PR](https://github.com/agentscope-ai/QwenPaw/pull/3846)) — First-time contributor PR, under review.
- **MCP client TTY detection fix** ([#4410](https://github.com/agentscope-ai/QwenPaw/issues/4410)) — Closed; fix likely in place for `yuque-mcp` compatibility.

**Prediction for next version (v1.2.0)**: Per-model token limits, custom Anthropic base URL, plugin discovery UI, and improved channel security will likely ship.

## 7. User Feedback Summary

Real user pain points reported in the last 24 hours:

- **Severe**: Channel config stored plaintext ([#4421]) — security concern for self-hosters.
- **Critical**: `write_file()` loops on long output ([#4299]), MiMo thinking model 400 errors ([#4314] — fixed), browser CDP completely broken on latest Ubuntu ([#4360]).
- **Integration frustrations**: Telegram voice messages unusable ([#1516]), WeChat messages routed to wrong tab ([#3173]), QQ message duplication and session corruption ([#3178]).
- **Upgrade regressions**: Embedding model config reset after `qwenpaw update` ([#4018]).
- **UX annoyances**: Interrupted retry hides user message bubble ([#3114]), “Thinking” placeholder duplication on rapid messages ([#4427] — PR submitted).
- **Positive signals**: Community actively filing detailed bug reports with logs, environment specs, and reproduction steps. Multiple first-time contributors submitting PRs for new providers and features.

## 8. Backlog Watch

Several long-unanswered issues and PRs require maintainer attention:

- **[#1853](https://github.com/agentscope-ai/QwenPaw/issues/1853) — Configurable base path** (since March 19, 3 comments, 1 👍). Prevent deployment behind reverse proxies.
- **[#1516](https://github.com/agentscope-ai/QwenPaw/issues/1516) — AudioContent not supported in Telegram** (since March 15, 7 comments). Persistent feature gap.
- **[#2751](https://github.com/agentscope-ai/QwenPaw/issues/2751) — Anthropic API `file` content type not supported** (since April 1, 4 comments). Blocks Anthropic users.
- **[#1499](https://github.com/agentscope-ai/QwenPaw/issues/1499) — QQ integration error: "No active model configured"** (since March 14, 4 comments). Basic connectivity issue.
- **[#3178](https://github.com/agentscope-ai/QwenPaw/issues/3178) — Session list corruption from malformed `chats.json`** (since April 10, 2 comments). No backup/validation mechanism.
- **[#3173](https://github.com/agentscope-ai/QwenPaw/issues/3173) — WeChat routing + non-vision model image handling** (since April 9, 2 comments). Two bugs in one report.
- **[#3114](https://github.com/agentscope-ai/QwenPaw/issues/3114) — Interrupted retry loses original user message bubble** (since April 8, 2 comments).
- **[#3259](https://github.com/agentscope-ai/QwenPaw/issues/3259) — Zhipu vision model misclassification** (since April 11, 2 comments).
- **[#3846 PR](https://github.com/agentscope-ai/QwenPaw/pull/3846) — GitHub Copilot provider** (since April 26, under review). Needs reviewer bandwidth.
- **[#4120 PR](https://github.com/agentscope-ai/QwenPaw/pull/4120) — Matrix E2EE verify step** (since May 8, under review). Community contribution with complex security implications.

Maintainers should prioritize the security hardening backlog (#1853, #4421) and the long-standing channel feature gaps (#1516, #2751) to improve user experience and deployment flexibility.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-15

## 1. Today's Overview

ZeroClaw saw very high activity in the last 24 hours, with **31 issues** and **50 pull requests** updated. Of the issues, 23 remain open/active and 8 were closed. PRs show a balanced merge/close rate (15 merged/closed vs 35 still open). The project is clearly in a busy development phase, with significant focus on cron scheduling reliability, Telegram channel integration, skill auditing, observability (OpenTelemetry/Prometheus), and security hardening. No new releases were published today, but numerous fixes and features are converging across the runtime, gateway, and CLI.

---

## 2. Releases

*No new releases today.*

---

## 3. Project Progress — Merged/Closed PRs

The following PRs were merged or closed in the last 24 hours, reflecting tangible progress:

- **[fix(cron): keep read-only access off schema init path]** ([#6655](https://github.com/zeroclaw-labs/zeroclaw/pull/6655)) — Prevents cold daemon startup from creating the cron DB for read-only queries.
- **[perf(cron): persist run results in one transaction]** ([#6656](https://github.com/zeroclaw-labs/zeroclaw/pull/6656)) — Batches cron run persistence into a single SQLite transaction for better performance.
- **[fix(skills): restrict audit to structural checks, delegate command safety]** ([#5952](https://github.com/zeroclaw-labs/zeroclaw/pull/5952)) — Removes duplicate command-content scanning from skill audit, delegating to runtime policy.
- **[fix(skills): don’t scan markdown content for high-risk command patterns]** ([#6071](https://github.com/zeroclaw-labs/zeroclaw/pull/6071)) — Reduces false positives in skill audit.
- **[fix(matrix): avoid threading root timeline messages]** ([#6525](https://github.com/zeroclaw-labs/zeroclaw/pull/6525)) — Prevents Matrix root messages from auto‑creating threads.
- **[fix(matrix): include attachment media metadata]** ([#6610](https://github.com/zeroclaw-labs/zeroclaw/pull/6610)) — Adds proper `AttachmentInfo` for file/image/audio outbound.
- **[fix: keep system messages at the start of chat history]** ([#6552](https://github.com/zeroclaw-labs/zeroclaw/pull/6552)) — Normalises chat history to merge all system messages, fixes tricky conversational UX.
- **[fix(cron): cron-scheduled webhook callbacks drop thread_id]** ([#6634](https://github.com/zeroclaw-labs/zeroclaw/issues/6634) → closed) — Underlying bug resolved by the read-only schema fix.
- **[ci: Advisory scan failed — 2026-05-14]** ([#6657](https://github.com/zeroclaw-labs/zeroclaw/issues/6657)) — Closed after dependency upgrade for `lettre` TLS vulnerability.

Additionally, feature-tracking issues such as **web chat tool approval UI** ([#6522](https://github.com/zeroclaw-labs/zeroclaw/issues/6522)) and **bash completion infinite recursion** ([#6402](https://github.com/zeroclaw-labs/zeroclaw/issues/6402)) were closed, indicating completed work.

---

## 4. Community Hot Topics

The most active discussions (by comment count) reveal core user concerns:

| Issue | Comments | Topic |
|-------|----------|-------|
| [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) | 4 | **Cron job output not routed to configured channels** (bug, S1 — workflow blocked) |
| [#5833](https://github.com/zeroclaw-labs/zeroclaw/issues/5833) | 3 | **Session ownership model for destructive operations** (enhancement, security) |
| [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) | 3 | **SearXNG search support and web search robustness** (enhancement) |
| [#6659](https://github.com/zeroclaw-labs/zeroclaw/issues/6659) | 3 | **No API for pushing notifications into gateway session** (bug/enhancement) |
| [#5956](https://github.com/zeroclaw-labs/zeroclaw/issues/5956) | 2 | **Document skill audit scope decision** (doc closed) |
| [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) | 2 | **Track 153 commits lost in bulk revert** (recovery effort) |
| [#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105) | 2 | **Agent lacks context of cron job it runs** (bug, S2) |

**Underlying needs:**  
- Cron reliability remains the top pain point — output delivery, session isolation, and job context are all broken.  
- Security and session scoping (destructive tools) are gaining traction, signalling enterprise/team use cases.  
- Search tooling limitations (DuckDuckGo CAPTCHA, no privacy alternatives) impede autonomous agents.  
- Gateway notification API is requested by downstream projects (e.g., `klodi-plugin`) for multi-instance architectures.

---

## 5. Bugs & Stability

Several serious bugs were reported or addressed today. Severity estimated from labels and descriptions:

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) | S1 – workflow blocked | Cron output not delivered to configured channels | Not yet |
| [#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646) | S1 – workflow blocked | `web_search_tool` / `web_fetch` not firing via Telegram (v0.7.5) | Not yet |
| [#6659](https://github.com/zeroclaw-labs/zeroclaw/issues/6659) | S1 – workflow blocked | No API for push notifications into gateway | Not yet |
| [#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672) | S0 – data loss | `reasoning_content` not passed in tool-call loops (Xiaomi models) | Not yet |
| [#6678](https://github.com/zeroclaw-labs/zeroclaw/issues/6678) | S1 – blocked | Skill tools rejected by Anthropic API due to illegal tool names | Not yet |
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | S2 – degraded | `allowed_private_hosts` ineffective for DNS resolving to private IPs | Not yet |
| [#6648](https://github.com/zeroclaw-labs/zeroclaw/issues/6648) | S2 – degraded | `cron session_target=main` still runs in isolated session | Not yet |
| [#6651](https://github.com/zeroclaw-labs/zeroclaw/issues/6651) | S2 – degraded | Matrix channel memory leak (~1 MB Pss per reload) | Blocked on upstream |
| [#6645](https://github.com/zeroclaw-labs/zeroclaw/issues/6645) | S3 – minor | Skill tools only handle `SKILL.toml`, not `manifest.toml` | Not yet |
| [#6654](https://github.com/zeroclaw-labs/zeroclaw/issues/6654) | S3 – minor | Cron read-only queries still hit schema init path | Fixed by [#6655](https://github.com/zeroclaw-labs/zeroclaw/pull/6655) |

**Note:** Several cron-related issues are being addressed in parallel PRs (e.g., #6655, #6656), but output routing (#6647) and session context (#6105) remain unresolved.

---

## 6. Feature Requests & Roadmap Signals

Today’s enhancements suggest the following themes for upcoming releases (likely v0.7.6 / v0.7.7):

- **Skills UX & localization** — [#6670](https://github.com/zeroclaw-labs/zeroclaw/issues/6670) (Fluent localisation), [#6674](https://github.com/zeroclaw-labs/zeroclaw/pull/6674) (PR), [#6676](https://github.com/zeroclaw-labs/zeroclaw/pull/6676) (skill suggestions). Strong momentum behind `zeroclaw skills` polish.
- **Observability refinement** — [#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) (turn-level OTel traces), [#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642) (capture prompt/completion), [#6669](https://github.com/zeroclaw-labs/zeroclaw/issues/6669) (audit metric sinks). A community contributor (alexandme) is driving this.
- **Telegram partial streaming** — [#6663](https://github.com/zeroclaw-labs/zeroclaw/issues/6663) (show tool-call progress). Democratises UX for long-running tool chains.
- **Web search improvements** — [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) (SearXNG support, DuckDuckGo CAPTCHA handling). High community demand.
- **Session & security** — [#5833](https://github.com/zeroclaw-labs/zeroclaw/issues/5833) (session ownership for destructive tools) is still blocked but essential for multi-agent deployments.
- **Gateway steering** — [#6661](https://github.com/zeroclaw-labs/zeroclaw/issues/6661) (preserve streamed output during steering) addresses a core UX regression.
- **Installation** — [#6658](https://github.com/zeroclaw-labs/zeroclaw/issues/6658) (musl aarch64 support in install script), [#6653](https://github.com/zeroclaw-labs/zeroclaw/issues/6653) (host-architecture policy for emulated installs).

**Prediction:** The v0.7.6 release (tracked in [#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)) will likely include skills localization, improved skill audit, and the observability bridges. Cron fixes and Telegram improvements may be fast‑tracked.

---

## 7. User Feedback Summary

Real user pain points captured today:

- **Cron unpredictability** – Users report cron jobs not routing to channels (#6647), agents lacking cron context (#6105), and session_target ignoring `main` (#6648). This is the most frequent complaint.
- **Telegram integration fragility** – `web_search_tool` and `web_fetch` fail to fire on Telegram (#6646) and `mention_only` does not suppress media responses (#6229 closed but fix uncertain).
- **Model compatibility** – Anthropic API rejects custom skill tools due to name format (#6678). Xiaomi thinking models lose `reasoning_content` (#6672). Both block workflow.
- **Memory leaks** – Matrix channel leaks memory on reload (#6651), annoying for long-lived daemons.
- **Skill authoring friction** – Skill tools only read `SKILL.toml`, not the more common `manifest.toml` (#6645). Skill review fork output is incomplete (#6644).
- **CLI regressions** – Bash completion infinite recursion (#6402) was fixed, but `zeroclaw onboard --interactive` regressed (#6673 fixed via PR).

Satisfaction signals: Positive reception of extended thinking provider PR (#5652), file rotation crate (#6611), and the doc fix for Arduino Uno Q setup (#6172).

---

## 8. Backlog Watch

Issues/PRs that have been open for a significant time or are blocked awaiting maintainer review:

| Item | Created | Status | Reason for Watch |
|------|---------|--------|------------------|
| [#5833](https://github.com/zeroclaw-labs/zeroclaw/issues/5833) — Session ownership model | 2026-04-17 | **blocked, needs-maintainer-review** | Essential for multi-tenant security; no assignee. |
| [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) — SearXNG support | 2026-04-05 | **needs-maintainer-review** | High community value, waiting for design go-ahead. |
| [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) — `web_fetch` private IP block is useless | 2026-03-29 | **no-stale** | Long-standing security hole, no fix PR. |
| [#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641) — Turn-level OTel traces | 2026-05-13 | **blocked** | Awaiting upstream contribution from alexandme. |
| [#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642) — Capture prompt/completion in OTel | 2026-05-13 | **blocked** | Similar dependency on alexandme. |
| [#6651](https://github.com/zeroclaw-labs/zeroclaw/issues/6651) — Matrix memory leak | 2026-05-14 | **blocked** | Root cause is upstream `matrix-rust-sdk` bug. |
| [#5652](https://github.com/zeroclaw-labs/zeroclaw/pull/5652) — Extended thinking providers (large PR) | 2026-04-11 | **open** | Significant feature, no maintainer feedback since creation. |
| [#6288](https://github.com/zeroclaw-labs/zeroclaw/pull/6288) — Systemd unit name for named instances | 2026-05-02 | **open** | Small fix, waiting for review. |
| [#6086](https://github.com/zeroclaw-labs/zeroclaw/pull/6086) — Config alias `allowed_path` | 2026-04-24 | **open** | Trivial UX improvement, untouched. |

**Actionable signal:** The maintainer team should prioritise unblocking #5833 and #5316 to address security and search reliability. The #5122 security issue is over 45 days old without a PR — this is a critical blind spot.

---

*Digest generated from public GitHub data of zeroclaw-labs/zeroclaw on 2026-05-15. All links point to the official repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*