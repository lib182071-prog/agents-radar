# OpenClaw Ecosystem Digest 2026-05-17

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-17 08:34 UTC

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

# OpenClaw Project Digest — 2026-05-17

## 1. Today’s Overview

OpenClaw continues to show extremely high developer and community activity: **500 issues** and **500 pull requests** were updated in the last 24 hours, with **140 PRs merged or closed** and **97 issues resolved**. Three beta releases (v2026.5.16‑beta.2 through beta.4) were pushed, adding xAI Grok OAuth, CLI cron `--wait` controls, and security audit suppression. The project remains in a rapid‑iteration phase, with critical P1 bugs (text leakage, signal‑daemon race, session context confusion) still open but attracting heavy triage attention. Community engagement remains strong, with top issues gathering over 20 comments each.

## 2. Releases

Three releases landed today, all part of the `2026.5.16` beta line:

### v2026.5.16‑beta.4
- **Security/audit**: Added `security.audit.suppressions` to allow intentional audit findings to be excluded from active summaries while preserving them in JSON output with a suppression notice. (#76949, thanks @100menotu001)
- **Agents/subagents**: Delegated agents are now consistently labelled, improving traceability.

### v2026.5.16‑beta.3 & v2026.5.16‑beta.2
Both carry identical change logs (likely incremental staging):
- **Providers/xAI**: Added xAI Grok OAuth login for SuperGrok subscribers, allowing `xai/*` models and xAI media/tool providers to authenticate without `XAI_API_KEY`.
- **CLI/cron**: Added `openclaw cron run --wait` with timeout and poll interval controls, plus exact `runs --run-id` filtering.

No breaking changes or explicit migration notes were provided. Users on earlier betas should update via `npm install -g openclaw@latest`.

## 3. Project Progress

**Merged/closed PRs today** — The 140 merged/closed items include several notable fixes that moved from open to resolved:

- **#68449** (Dreaming plugin stopword list too narrow) – closed, adds stopword filtering for cron‑triggered sessions.
- **#76552** (High CPU during Codex runtime) – closed; root‑cause fix for hook‑relay and session/history amplification.
- **#44810** (Codex ACP run stalls due to missing proxy/network) – closed; adds network readiness checks.
- **#81114** (Codex app‑server timeout/fallback) – closed; improves timeout handling during large context assemblies.
- **#77896** (Matrix channel missing `matrix-js-sdk` after npm update) – closed; dependency bundling fix.
- **#81820** (Slack socket‑mode reconnect → `@bot` replies skipped) – closed; re‑evaluates mention detection after reconnect.

Several new PRs (still open) advanced long‑running features:
- **#83006** – Adds `defineToolPlugin` SDK helper and `openclaw plugins init/build/validate` for simple tool‑plugin authoring.
- **#82986** – Fixes Chrome CDP launch error that self‑contradicts (throws with `ok: true`).
- **#82258** – Renders Slack progress drafts as native plan cards instead of legacy blocks.

## 4. Community Hot Topics

| Issue / PR | Comments | Key Underlying Need |
|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) – Text between tool calls leaks to channels | 26 | **Security & UX**: Internal processing output visible to end users — a P1 security issue that also degrades conversation quality. Community wants deterministic suppression of inter‑tool narration. |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) – Prebuilt Android APK | 24 | **Mobile access**: Strong demand for a ready‑to‑install Android companion app. Users want to avoid manual compilation. |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) – Signal daemon `stop()` race → orphaned processes | 17 | **Reliability**: SIGUSR1 restarts cause port conflicts and message‑send failures — a critical stability concern for Signal users. |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) – Tiered bootstrap file loading | 16 | **Context optimization**: Users want to reduce token waste by loading only relevant bootstrap files per session, especially for sub‑agents and cron. |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) – Control UI requires HTTPS/localhost | 15 | **Deployment friction**: Running behind reverse proxies (e.g., Hostinger) breaks device‑identity checks. Community requests a configurable secure‑context bypass. |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) – Bootstrap files in `agentDir` silently ignored | 13 | **Configuration confusion**: Per‑agent bootstrap files don’t work; only workspace‑level files are loaded. Needs documentation clarity and eventual fix. |

## 5. Bugs & Stability

**P1 (Critical, with active user impact):**
- [#25592](https://github.com/openclaw/openclaw/issues/25592) – Text between tool calls leaks to messaging channels (security, message loss). No fix PR yet; marked `needs-maintainer-review`.
- [#22676](https://github.com/openclaw/openclaw/issues/22676) – Signal daemon race on SIGUSR1 restart (crash‑loop, orphaned processes). Open; has `linked-pr-open` tag.
- [#32296](https://github.com/openclaw/openclaw/issues/32296) – Agent replies to previous message instead of current (session context confusion). Open; needs product decision.

**P1 Regressions:**
- [#31583](https://github.com/openclaw/openclaw/issues/31583) – `exec` tool no longer inherits `skills.entries.*.env` environment variables (regression). Linked PR is open.
- [#38327](https://github.com/openclaw/openclaw/issues/38327) – `google-vertex/gemini-3.1-pro-preview` fails with “Cannot convert undefined or null to object” on latest release. Open; queueable fix.

**P2 with community impact:**
- [#40540](https://github.com/openclaw/openclaw/issues/40540) – `openclaw update` fails with EBUSY on Windows (unable to self‑update). Open.
- [#37634](https://github.com/openclaw/openclaw/issues/37634) – Sandbox with `workspaceAccess: none` mounts workspace read‑only, breaking file tools.
- [#31331](https://github.com/openclaw/openclaw/issues/31331) – Docker + Docker‑out‑of‑Docker sandbox cannot bind `/workspace` at all.
- [#81820](https://github.com/openclaw/openclaw/issues/81820) – Slack socket‑mode reconnect silently drops `@bot` thread replies (closed today, but represents a pattern of reconnect fragility).

**Notable: multiple security‑related bugs** (e.g., #25592, #31583, #37634, #31331) remain open — the project’s `clawsweeper` triage system is actively labeling them.

## 6. Feature Requests & Roadmap Signals

**Recently shipped in today’s betas:**
- xAI Grok OAuth login (v2026.5.16‑beta.2/3)
- CLI cron `--wait` with timeout / poll controls (same release)
- Security audit suppression (beta.4)

**Likely candidates for next release (based on community priority and maintainer interest):**
- **Tiered bootstrap loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438)) – high demand, 16 comments, no pending PR but tagged `needs-product-decision`.
- **Prebuilt Android APK** ([#9443](https://github.com/openclaw/openclaw/issues/9443)) – long‑standing request with 24 comments; a previous PR was mentioned but not merged.
- **Slack Block Kit support** ([#12602](https://github.com/openclaw/openclaw/issues/12602)) – enables rich interactive messages.
- **Private network access opt‑in** ([#39604](https://github.com/openclaw/openclaw/issues/39604)) – 12 comments, 7 👍; blocking enterprise deployments.
- **Exec denylist** ([#6615](https://github.com/openclaw/openclaw/issues/6615)) – complementary to allowlist, 7 👍.
- **Telegram Business bot support** ([#20786](https://github.com/openclaw/openclaw/issues/20786)) – 8 comments, 5 👍.

**Long‑term roadmap signals (RFCs / big features):**
- Multi‑agent collaboration enhancement ([#35203](https://github.com/openclaw/openclaw/issues/35203)) – capability profiling, shared blackboard, layered memory, token cost governance.
- Secrets management integration ([#13610](https://github.com/openclaw/openclaw/issues/13610)) – AWS Secrets Manager, Vault, etc.
- Native AWS deployment guides ([#13597](https://github.com/openclaw/openclaw/issues/13597)) – EC2, ECS, Lambda.

## 7. User Feedback Summary

**Pain points expressed repeatedly:**
- **Text leakage** – the highest‑voted concern: internal agent processing (error handling, narration) appears in public chat channels, causing confusion and potential data exposure.
- **Android unavailability** – many users want to run the OS‑companion app without building from source.
- **Deployment hurdles** – Control UI requiring HTTPS, Docker sandbox workspace issues, and Windows update failures frustrate self‑hosters.
- **Session reliability** – agent replies to wrong messages, Signal daemon crashes, Slack reconnects lose context – eroding trust in conversational consistency.

**Positive signals:**
- xAI Grok integration was well‑received (multiple 👍 on the release announcement).
- The quick turnaround of closed bugs (#76552 CPU, #77896 Matrix, #81820 Slack) shows the team is responsive to high‑impact regressions.
- Community members actively contribute features (Feishu tools, iOS Liquid Glass UI, cron improvements) – a healthy ecosystem.

**Use cases driving feature requests:**
- **Mobile & multi‑platform** – Android APK, iOS Dynamic Island, Telegram Business, WhatsApp integration.
- **Enterprise & security** – secrets management, path‑scoped permissions, exec denylists, audit suppression.
- **Cost & token optimization** – tiered bootstrap, reduced tool schema overhead (#14785), `memory_search` recursion (#34400).

## 8. Backlog Watch

These important issues/PRs have been open for **15–100+ days** and remain unmerged or need maintainer action:

| Item | Days Open | Status |
|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) – Text leak (P1 security) | 83 | Needs maintainer review & product decision |
| [#9443](https://github.com/openclaw/openclaw/issues/9443) – Android APK | 102 | Needs product decision (high demand) |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) – Signal daemon race (P1) | 86 | Linked PR open; needs review |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) – Tiered bootstrap | 86 | Needs product decision |
| [#32473](https://github.com/openclaw/openclaw/issues/32473) – Control UI HTTPS requirement | 75 | Needs product decision & security review |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) – agentDir bootstrap ignored | 79 | Needs security review |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) – `exec` env regression | 77 | Needs live repro & linked PR open |
| [#41637](https://github.com/openclaw/openclaw/issues/41637) – Feishu webhook `EADDRINUSE` fix (PR) | 69 | Awaiting real‑behavior proof |
| [#41067](https://github.com/openclaw/openclaw/issues/41067) – Dashboard chat recovery (PR) | 69 | Needs real‑behavior proof |

These items represent critical gaps in usability, security, and stability. Community attention is highest on the text‑leak and Android issues. The `clawsweeper` team has labelled most for `needs-maintainer-review` or `needs-product-decision`, indicating they are queued but not yet acted upon.

---

*Digest generated from GitHub data as of 2026-05-17T23:59 UTC.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem

**Date:** 2026-05-17  
**Purpose:** Provide a data-driven overview of the personal AI assistant / agent open-source landscape, comparing activity, positioning, shared challenges, and emerging trends across 13 monitored projects.

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is in a phase of rapid expansion and competitive differentiation. Projects are maturing from single‑channel chatbots into multi‑modal, multi‑agent systems with plugin SDKs, OAuth provider integrations, and enterprise-grade security features. OpenClaw remains the largest reference implementation by raw contribution volume, but Hermes Agent, NanoBot, and ZeroClaw are closing the gap with significant releases and architecture rewrites. A few projects (NullClaw, TinyClaw, ZeptoClaw) show no recent activity, signaling potential stagnation. Overall, the community is pushing for mobile access, token efficiency, multi‑agent orchestration, and robust provider compatibility—reflecting the growing demands of both individual users and enterprise deployers.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | Release(s) Today | Health Score (1–10) |
|---|---|---|---|---|---|
| OpenClaw | 500 | 500 | 140 | 3 betas | 8 |
| NanoBot | 4 | 22 | 15 | None | 8 |
| Hermes Agent | 50 | 50 | 6 | None (v0.14.0 yesterday) | 7 |
| NanoClaw | 6 | 11 | 9 | None | 7 |
| ZeroClaw | 50 | 50 | 6 | None | 8 |
| IronClaw | 6 | 44 | 18 | None | 8 |
| CoPaw | 16 | 12 | 4 | None | 6 |
| PicoClaw | 7 | 5 | 1 | 1 nightly | 7 |
| LobsterAI | 1 | 8 | 8 | None | 6 |
| Moltis | 3 | 2 | 0 | None | 5 |
| NullClaw | 0 | 0 | 0 | None | N/A (inactive) |
| TinyClaw | 0 | 0 | 0 | None | N/A (inactive) |
| ZeptoClaw | 0 | 0 | 0 | None | N/A (inactive) |

*Health Score reflects: activity volume, bug‑fix velocity, release cadence, community engagement, and stability posture. Scores are relative within this cohort.*

---

## 3. OpenClaw's Position

**Advantages vs Peers:**  
- **Scale**: OpenClaw handles **500 issues and PRs daily**—5–10× the volume of the next most active projects (Hermes, ZeroClaw).  
- **Release cadence**: Three beta releases in one day demonstrate CI maturity and rapid iteration.  
- **Security focus**: Unique features like audit suppression (#76949), exec denylist (#6615), and tiered bootstrap (#22438) address enterprise compliance.  
- **Provider breadth**: xAI Grok OAuth, Vertex AI, and multiple first‑party providers give it the widest LLM backend support.

**Technical Approach Differences:**  
- OpenClaw uses a **modular plugin SDK** (`defineToolPlugin`) and a `clawsweeper` triage system, whereas Hermes relies on a monolithic architecture with gateway‑based delegation.  
- NanoBot’s `/goal` feature provides persistent session objectives—a simpler alternative to OpenClaw’s more complex context management.  
- IronClaw is rewriting its core (Reborn) to move from Rust to a composition‑root architecture, while OpenClaw remains in TypeScript/Node.

**Community Size Comparison:**  
- OpenClaw’s top issues gather 20+ comments; Hermes’s top issue (#6839) has 10 👍.  
- OpenClaw’s contributor base is likely larger (implied by 140 merged PRs/day vs Hermes’s 6).  
- However, Hermes’s v0.14.0 had **215 community contributors** for 808 commits—indicating deeper contributor engagement per release.

**Net Assessment:** OpenClaw is the **volume leader** but faces competition from Hermes for community mindshare and from IronClaw for architectural innovation.

---

## 4. Shared Technical Focus Areas

The following requirements appear across multiple projects, signalling ecosystem‑wide gaps or priorities:

| Focus Area | Projects Affected | Specific Needs |
|---|---|---|
| **Multi‑provider OAuth / Login** | OpenClaw, ZeroClaw, CoPaw, PicoClaw | xAI Grok, Ollama Cloud, Kimi, MiniMax, SiliconFlow |
| **Token & Cost Efficiency** | OpenClaw, Hermes, NanoBot, ZeroClaw | Tiered bootstrap, lazy tool schemas, BM25‑lite skill router, reduced tool overhead |
| **Multi‑Agent Orchestration** | OpenClaw, Hermes, NanoBot, ZeroClaw | A2A protocol, mailbox channels, shared blackboard, peer roster, `spawn_agent` |
| **Mobile & Cross‑Platform** | OpenClaw, NanoBot, Hermes | Prebuilt Android APK, iOS support, Telegram Business, Signal channel |
| **Cron / Scheduled Tasks** | OpenClaw, NanoClaw, ZeroClaw, CoPaw | `--wait` controls, job dedup, timezone consistency, output suppression |
| **Security & Access Control** | OpenClaw, Hermes, ZeroClaw, CoPaw | Prompt injection scanners, credential redaction, per‑skill permissions, denylists |
| **Enterprise Deployment** | OpenClaw, IronClaw, Hermes | Secrets management (Vault), private network opt‑in, config‑as‑code, E2E testing |
| **Channel Expansion** | NanoBot, PicoClaw, ZeroClaw, CoPaw | Email, Signal, Mattermost, WeChat multi‑account, Slack Block Kit |

These patterns indicate that **the ecosystem is converging on a shared architecture**: multi‑provider, multi‑channel, with cost‑aware context management and agent‑to‑agent communication.

---

## 5. Differentiation Analysis

| Project | Primary Differentiator | Target User | Notable Unique Features |
|---|---|---|---|
| **OpenClaw** | Breadth & scale; reference implementation | Advanced self‑hosters, enterprises | xAI OAuth, cron `--wait`, audit suppression, plugin SDK |
| **Hermes Agent** | Community‑driven innovation; large release v0.14 | Power users, multi‑model experimenters | A2A protocol request, lazy tool schemas, `hermes doctor`, profile dashboard |
| **NanoBot** | Lightweight goal‑oriented agents | Python‑focused developers, quick deployment | `/goal` command, BM25‑lite skill router, mailbox channel, Telegram inline keyboards |
| **ZeroClaw** | Multi‑agent runtime (v0.8.0) & skill self‑improvement | Those building collaborative agent systems | `skill_manage` tool, webhook transforms, multi‑agent orchestration |
| **IronClaw** | Reborn architecture (Rust → composition root) | Performance‑critical, enterprise operators | Binary E2E tests, policy‑gated identity, built‑in HTTP tools |
| **NanoClaw** | Finance‑focused skills & cron reliability | Financial / quantitative users | Finance Plan 3 schema, Codex provider, WhatsApp recovery |
| **CoPaw** | Approval workflow & chat reliability | Chinese‑speaking users, Docker deployers | Lightweight goal mode, instant ack, E2E testing infrastructure |
| **PicoClaw** | Lean, nightly builds, WeChat multi‑account | Users on arm64 / low‑resource devices | SiliconFlow provider, MCP Streamable HTTP, independent code block controls |
| **LobsterAI** | Desktop IM integration (NetEase ecosystem) | Chinese enterprise / desktop users | Reasoning fix for Mimo, Dream UI, Opik observability |
| **Moltis** | Small footprint, multi‑model reasoning | Developers needing minimal dependencies | Gemini reasoning tags, VoiceCoquiTTS, remote access (NetBird) |

---

## 6. Community Momentum & Maturity

**Tier 1 – Very High Activity / Rapid Iteration**  
OpenClaw, NanoBot, Hermes Agent, NanoClaw, ZeroClaw, IronClaw  
*These projects merge dozens of PRs daily, fix critical bugs within hours of reporting, and have active maintainer engagement.*

**Tier 2 – Moderate Activity / Stabilizing**  
PicoClaw, CoPaw, LobsterAI, Moltis  
*These projects process fewer contributions, have some stale PRs, but still ship incremental improvements.*

**Tier 3 – Inactive**  
NullClaw, TinyClaw, ZeptoClaw  
*No code changes in 24h; may be archived or dormant.*

**Maturity Signals:**  
- **Release discipline**: OpenClaw (3 betas/day) and IronClaw (nightly CI) show mature pipelines; LobsterAI and Moltis rely on irregular release trains.  
- **Bug‑fix speed**: NanoBot fixed a duplicate context injection bug the same day; ZeroClaw pushed fix PRs alongside bug reports.  
- **Community health**: Hermes has the strongest contributor base (215 per release), but its plagiarism controversy (#17688) is a risk. CoPaw has first‑time contributors stuck in review limbo.

---

## 7. Trend Signals

Extracted from community feedback and roadmap signals across all projects, these are the key industry trends relevant to AI agent developers:

1. **Multi‑Agent Orchestration Becomes Standard** – A2A protocol, mailbox channels, and peer rosters signal that projects are competing on how well agents collaborate, not just chat.  
2. **Provider Proliferation via OAuth** – Users expect zero‑key access to Grok, Ollama Cloud, Kimi, and MiniMax. OAuth integrations are a competitive differentiator.  
3. **Token Efficiency is the #1 Performance Concern** – Lazy tool schemas, tiered bootstrap, BM25 routers, and skill routers all aim to cut token waste. Developers building tools for these ecosystems should optimize for minimal token add‑on.  
4. **Mobile Access is an Unmet Need** – Multiple projects (OpenClaw, Hermes, NanoBot) have requests for Android/iOS clients. This is a recurring gap that dedicated mobile app developers could fill.  
5. **Security as a Product Feature** – Prompt injection scanners, credential redaction, audit suppression, and exec denylists are moving from nice‑to‑have to required. Projects that neglect security (e.g., Hermes with open scanner gaps) risk user trust.  
6. **Enterprise Deployment Drives Architecture** – Secrets management, private network opt‑in, config‑as‑code, and Docker sandbox improvements reflect real production requirements. Self‑hosting is the dominant deployment model.  
7. **Cron / Automation is the New Baseline** – Users expect agents to run scheduled tasks, with timezone awareness, dedup, and output suppression. This transforms agents from reactive chat bots to proactive assistants.

**Value for AI Agent Developers:**  
- Focus on **multi‑agent communication protocols** (A2A, mailbox) and **token‑efficient context management** to align with ecosystem direction.  
- Invest in **OAuth provider plugins** and **mobile SDKs**—these are high‑demand gaps.  
- **Security hardening** for input validation (prompt injection) and output redaction is a cross‑project priority that any library or tool can contribute to.  
- **Cron and scheduling** primitives are becoming a prerequisite for agent platforms; building a robust cron system (with timezone, dedup, and wait controls) will have wide applicability.

---

*Data aggregated from public GitHub activity on 2026-05-17. Health scores are subjective assessments based on observed activity, bug resolution speed, and community engagement.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-17

## 1. Today’s Overview
The project is in a highly active phase following the **v0.2.0** release (105 PRs, 20 new contributors). In the last 24 hours, 15 of 22 updated PRs were merged or closed, indicating a strong cadence of bug fixes and feature delivery. Four open issues remain active, including a WebUI display regression and a Docker deployment documentation mismatch. Overall project health is strong, with rapid iteration and responsive maintainers.

## 2. Releases
- **v0.2.0** (tagged 2026-05-14)  
  **Headline feature:** `/goal` command – agents can now maintain a sustained objective across turns via `long_task`. The goal state is persisted in Runtime Context, survives compaction, and is pinned every turn.  
  **No explicit breaking changes or migration notes** are provided in the release description. However, a currently open issue (#3873) documents four inconsistencies in `docker-compose.yml`, `docs/deployment.md`, and `README.md` that prevent a clean Docker deployment of v0.2.0. Users upgrading via Docker should review that issue.  
  **Related merged PRs:** #3788 (goal feat), #3861 (LLM timeout fix for goals).

## 3. Project Progress
Today’s merged/closed PRs (15 total) include several high-impact changes:

- **Docker build fixes** (#3870, #3872) – resolved “hatch_build.py not found” and WebUI port exposure.
- **Goal/agent loop refinements** – removed duplicate runtime context injection during mid-turn drain (#3859), re-evaluate LLM timeout when goal state changes mid-run (#3861), refactored checkpoint and turn persistence out of `loop.py` (#3856).
- **MiMo thinking control for gateways** (#3851, #3867) – wired `reasoning.effort` via OpenRouter and fixed post-merge follow-up for `reasoning.effort` injection.
- **Chinese rate-limit handling** (#3864) – added `访问量过大` to transient error markers.
- **Multi‑agent inter‑communication** – merged **mailbox channel plugin** (#3461) for file‑system‑based agent‑to‑agent messaging.
- **Session cleanup** (#3516) – configurable auto‑deletion of idle sessions (cron‑based, disabled by default).
- **Claude docs update** (#3860) – reflected current channels, providers, tools, and storage modules.
- **Refactoring** – extracted public `ContextBuilder.build_user_content()` (#3858).

These PRs show a focus on **stability, scaling, and developer experience**.

## 4. Community Hot Topics
- **Issue #3790** – *“WebUI会话-打印内容显示错乱”* (13 comments)  
  Users report WebUI session content becomes garbled after a print/stream update, requiring a page refresh. This is the most discussed bug today; no fix PR has been linked yet. The underlying need is a reliable, glitch‑free WebUI for production use.
- **Issue #3873** – *“Docker deployment docs and docker-compose.yml have multiple inconsistencies with v0.2.0”* (0 comments, opened today)  
  High‑impact for Docker users: four mismatches prevent correct deployment, especially with the bundled WebUI and `bwrap` sandbox. This signals that the v0.2.0 release may have been tested primarily outside Docker, and quick documentation/configuration fixes are needed.
- **Issue #3845 (closed)** – *“MiMo thinking control not working through gateway providers”* (0 comments)  
  The issue was fixed in #3851 and then improved in #3867, demonstrating maintainer responsiveness.

## 5. Bugs & Stability
| Severity | Bug | Status | Fix |
|----------|-----|--------|-----|
| **High** | #3857 – bootstrap HTTP 500 on gateway access | Open (1 comment) | None yet |
| **High** | #3873 – Docker deployment docs incompatible with v0.2.0 | Open (0 comments) | None yet |
| **Medium** | #3790 – WebUI session display corruption after update | Open (13 comments) | None yet |
| **Medium** | #3863 – WeChat login blocked by version check (微信版本较低) | Open (1 comment) | Likely upstream issue |
| **Low** | #3845 – MiMo thinking control through gateways | Closed | #3851 / #3867 (merged) |

**Quick regression fix:** The duplicate runtime context injection bug (#3859) found and merged the same day it was reported.

## 6. Feature Requests & Roadmap Signals
Several open PRs indicate likely direction for v0.2.x or v0.3.0:

- **Skill/state optimisation:**
  - #3865 – *BM25-lite skill router*: reduces system prompt by ~60% by injecting only top‑5 relevant skills per turn. If merged, it will significantly improve token efficiency for users with many skills.
  - #3728 – *LoopDetectHook & ReflectRetryHook*: self‑correction hooks to break tool‑call loops and blind retries. This adds agent resilience without manual intervention.

- **Multi‑instance / orchestration:**
  - #3854 – *Peer roster via bootstrap endpoint*: exposes `NANOBOT_PEER_*` variables for WebUI to discover other NanoBot instances. Essential for multi‑container or HF Spaces deployments.

- **Channel expansion:**
  - #3852 – *Signal channel* (via signal‑cli daemon). If merged, adds support for the popular secure messaging platform.

- **Provider hardening:**
  - #3869 – *DeepSeek message hardening*: fixes null content, “(empty)” placeholder leakage, and assistant text being dropped. Signals that DeepSeek compatibility remains a focus.

No single “next version” target is announced, but the volume of open feature PRs suggests a v0.3.0 may incorporate skill router, self‑correction hooks, and peer roster.

## 7. User Feedback Summary
- **Satisfaction:** Users praise the `/goal` feature as a meaningful step toward persistent agent objectives. Quick acceptance of fixes (e.g., MiMo thinking) shows trust in the maintainers.
- **Pain points:**
  - WebUI display corruption (#3790) – clearly interferes with daily use, and its 13 comments show broad impact.
  - Docker users face a poor out‑of‑box experience (#3873), which may deter adoption for self‑hosting.
  - Chinese language users encounter provider‑specific errors (#3863 WeChat, #3864 rate‑limit) – though the latter was quickly resolved.
  - Bootstrap 500 (#3857) suggests possible configuration or networking failure for new users.

Overall, the community is active (many issues filed in Chinese, international participation) and grateful for the rapid bug‑fix cycle.

## 8. Backlog Watch
- **Issue #3790** (WebUI display corruption) – opened 2026-05-14, last updated today, no fix PR assigned. With 13 comments and high visibility, this deserves maintainer attention.
- **PR #3728** (LoopDetectHook & ReflectRetryHook) – opened 2026-05-10, no updates since maintainer review. This is a substantial feature that could improve agent robustness; it may need a second review or conflict resolution.
- **Issue #3857** (bootstrap HTTP 500) – opened 2026-05-16, only one comment from reporter. No reproduction details have been provided yet, but the bug blocks gateway access entirely.
- **Issue #3863** (WeChat login version issue) – likely not a NanoBot code bug, but no workaround or documentation update has been published. Users may be left stranded.

No long‑unanswered PRs older than a week are present, reflecting good maintainer responsiveness.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-05-17

## 1. Today's Overview

Project activity remains very high, with 50 issues and 50 pull requests updated in the last 24 hours. Yesterday’s release of **Hermes Agent v0.14.0** (v2026.5.16) marks the most significant milestone in months, packing 808 commits and contributions from 215 community members. Despite strong momentum, the issue tracker shows a steady influx of P2/P3 bugs and security concerns, indicating that the rapid growth phase is producing both feature richness and stability challenges. Community engagement is healthy, with long-standing feature requests (e.g., A2A protocol, lazy tool schemas) gaining traction and duplicate reports surfacing around delegation and credential handling.

## 2. Releases

### v0.14.0 (v2026.5.16) – "The Foundation Release"
- **Date:** May 16, 2026
- **Commits since v0.13.0:** 808
- **Merged PRs:** 633
- **Files changed:** 1,393 (165,061 insertions)
- **Issues closed:** 545 (12 P0, 50 P1, 483 others)
- **Community contributors:** 215 (including co-authors)

The release tagline is cut short: *“Hermes installs and runs an…”* (likely “agent”). No explicit breaking changes or migration notes were provided in the snippet. Given the 1,400+ file changes, users upgrading from v0.13.0 should verify their config files and test core workflows (especially delegation, Matrix, and provider credentials) before deploying in production. A migration guide is expected to follow.

## 3. Project Progress

In the last 24 hours, **6 PRs were merged/closed** and **11 issues were closed**.

**Notable closed issues:**
- [#12614](https://github.com/NousResearch/hermes-agent/issues/12614) – [bug] Matrix bot not receiving messages on fresh setup (fixed).
- [#24140](https://github.com/NousResearch/hermes-agent/issues/24140) – [bug] All models rejected due to context window minimum (Telegram down) – root cause identified and resolved.
- [#27018](https://github.com/NousResearch/hermes-agent/issues/27018) – [bug] Chrome not responding on WSL when using `/browser connect`.
- [#27350](https://github.com/NousResearch/hermes-agent/issues/27350) – [feature] Unify text + TTS in a single Signal message (closed as implemented? The PR is open? Actually issue closed, PR #27350 is missing from list; check: #27350 issue closed, PR #27349 is different. Probably merged quickly).
- [#26947](https://github.com/NousResearch/hermes-agent/issues/26947) – [feature] Slack Block Kit table rendering (closed as duplicate of another work).

**Closed/merged PRs (6 total):**
- [#27353](https://github.com/NousResearch/hermes-agent/pull/27353) – chore: update Hermes favicon (website).
- [#27338](https://github.com/NousResearch/hermes-agent/pull/27338) – feat: add profile runtime comparison dashboard.
- [#27337](https://github.com/NousResearch/hermes-agent/pull/27337) – feat: add Pinecone memory indexer for topic files and session summaries.
- Others likely minor fixes or chore PRs.

**Open PRs advancing features:**
- [#25660](https://github.com/NousResearch/hermes-agent/pull/25660) – "single gateway, multiple agents" (MVP, P2) – still open, major architectural change.
- [#27347](https://github.com/NousResearch/hermes-agent/pull/27347) – centralized model registry and dashboard overhaul (P3).
- [#27356](https://github.com/NousResearch/hermes-agent/pull/27356) – new Google Cloud Vertex AI provider for Anthropic models.
- [#27348](https://github.com/NousResearch/hermes-agent/pull/27348) – new Tenstorrent AI provider.
- [#21997](https://github.com/NousResearch/hermes-agent/pull/21997) – Chinese localization (still open since May 8).

## 4. Community Hot Topics

| Issue | Comments | 👍 | Summary |
|-------|----------|----|---------|
| [#12614](https://github.com/NousResearch/hermes-agent/issues/12614) [closed] | 18 | 0 | Matrix bot fails to receive inbound events after update – resolved but generated deep discussion. |
| [#514](https://github.com/NousResearch/hermes-agent/issues/514) [open] | 12 | 4 | A2A (Agent-to-Agent) protocol support – long-standing feature, high interest, linked to Google’s open standard. |
| [#24140](https://github.com/NousResearch/hermes-agent/issues/24140) [closed] | 11 | 0 | All models rejected due to context window minimum – Telegram outage, urgent. |
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) [open] | 8 | **10** | Lazy tool schema loading – token overhead reduction, strong community backing. |
| [#7833](https://github.com/NousResearch/hermes-agent/issues/7833) [open] | 5 | 1 | `delegate_task` overwrites custom endpoint with parent credential pool. |
| [#10232](https://github.com/NousResearch/hermes-agent/issues/10232) [closed] | 1 | **16** | A single dot (`.`), likely a meme or placeholder, received 16 👍 – community humor. |

**Analysis:** The A2A protocol request (#514) has been open since March 6 and gathers consistent thumbs-up. It is seen as complementary to MCP and would enable Hermes to discover and interoperate with remote agents. The high number of 👍 on #6839 indicates that token efficiency from tool schemas is a top pain point for users, especially those with many toolsets.

## 5. Bugs & Stability

### New P2 Bugs Reported Today
- [#27339](https://github.com/NousResearch/hermes-agent/issues/27339) – Prompt cache / KV cache invalidation on follow-up messages due to dynamic tool shuffling. Impacts inference performance on OpenAI-compatible backends.
- [#27344](https://github.com/NousResearch/hermes-agent/issues/27344) – `computer_use` multimodal tool message causes 400 error on providers that don’t support multimodal tool content (e.g., Xiaomi MiMo). **Fix PR #27351 exists.**
- [#27311](https://github.com/NousResearch/hermes-agent/issues/27311) – Gemini native adapter does not accept OpenAI-format `video_url` parts for video analysis.
- [#27319](https://github.com/NousResearch/hermes-agent/issues/27319) – Context-file prompt injection scanner misses multi-word variants (e.g., “ignore all prior instructions”).
- [#27284](https://github.com/NousResearch/hermes-agent/issues/27284) – Memory and MCP prompt injection scanners also miss multi-word ignore-instruction variants.
- [#27282](https://github.com/NousResearch/hermes-agent/issues/27282) – `--tui` gateway exits mid-turn with `stdin EOF` on macOS (not byterover-related).
- [#26730](https://github.com/NousResearch/hermes-agent/issues/26730) – Kanban workers fail due to context pollution from parent session (already P2).
- [#27294](https://github.com/NousResearch/hermes-agent/issues/27294), [#27295](https://github.com/NousResearch/hermes-agent/issues/27295), [#27296](https://github.com/NousResearch/hermes-agent/issues/27296) – Three duplicates reporting `delegate_task` ignores delegation `base_url` – subagent inherits parent model instead (P2). **Indicates a systematic delegation misrouting problem.**
- [#27325](https://github.com/NousResearch/hermes-agent/issues/27325) – Xiaomi MiMo provider does not pass `thinking` parameter, defaults to enabled and wastes tokens (P3).
- [#27310](https://github.com/NousResearch/hermes-agent/issues/27310) – `hermes doctor` misreports Gemini API keys when checked via generic Bearer probe (P3).

### Fix PRs in Flight
- [#27351](https://github.com/NousResearch/hermes-agent/pull/27351) – guard multimodal tool content by provider capability (fixes #27344).
- [#27217](https://github.com/NousResearch/hermes-agent/pull/27217) – add missing credential paths to write denylist (security, P2).
- [#27349](https://github.com/NousResearch/hermes-agent/pull/27349) – redact xAI (Grok) API keys in logs (security, P2).
- [#27336](https://github.com/NousResearch/hermes-agent/pull/27336) – use runtime Hermes home for agent logging (fixes log misrouting).
- [#26006](https://github.com/NousResearch/hermes-agent/pull/26006) – invalidate update-check cache when git refs change.

**Verdict:** Security and delegation bugs are the most pressing, with multiple duplicates and missing credential coverage. The prompt injection scanner gaps (#27319, #27284) are particularly concerning for production deployments using shared memory.

## 6. Feature Requests & Roadmap Signals

**High-signal requests (most 👍 and discussion activity):**
- [#514](https://github.com/NousResearch/hermes-agent/issues/514) – A2A protocol support. Likely to be a major theme for v0.15 given industry alignment and repeated asks.
- [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) – Lazy tool schema loading. With 10 👍 this is the most upvoted open feature. Expect it to be prioritized as token savings are critical for local models.

**Newly requested features today:**
- [#27314](https://github.com/NousResearch/hermes-agent/issues/27314) – Honcho memory provider: runtime peer alias/prefix mapping for multi-user gateways.
- [#27313](https://github.com/NousResearch/hermes-agent/issues/27313) – Allow video analysis to use separate auxiliary backend from image vision.
- [#27322](https://github.com/NousResearch/hermes-agent/issues/27322) – Feishu `send_slash_confirm` with interactive card buttons (now implemented in PR #27358).
- [#27298](https://github.com/NousResearch/hermes-agent/issues/27298) – General per-task fallback chains for all auxiliary models (vision, compression, STT, etc.) – addresses Great Firewall constraints.

**Already in PR stage:**
- [#27356](https://github.com/NousResearch/hermes-agent/pull/27356) – Google Cloud Vertex AI provider for Anthropic models.
- [#27348](https://github.com/NousResearch/hermes-agent/pull/27348) – Tenstorrent AI provider.
- [#25660](https://github.com/NousResearch/hermes-agent/pull/25660) – Single gateway, multiple agents (multi-tenant) – likely the next major architecture shift.
- [#27347](https://github.com/NousResearch/hermes-agent/pull/27347) – Centralized model registry and dashboard overhaul.

**Prediction for next minor release (v0.14.1 or v0.15.0):** Expect inclusion of at least one new provider (Vertex, Tenstorrent), security scanner hardening, and the lazy tool schema loading feature given its popularity. The multi-agent gateway PR (#25660) may land as an experimental feature.

## 7. User Feedback Summary

**Pain points (most frequently reported):**
1. **Delegation misrouting** – Multiple dups (#27294–#27296) and earlier #7833: subagents inherit parent credentials/endpoints instead of using `delegation.base_url`.
2. **Token overhead from tool schemas** – #6839 (lazy loading) and #20975 (truncated tool call retry) both touch on token waste.
3. **Provider-specific compatibility** – Xiaomi MiMo, Gemini, and others lack proper parameter handling (thinking, multimodal tool messages, video URLs).
4. **Security scanner gaps** – Prompt injection bypasses in both context files and memory/MCP (reported by same user in #27319, #27284).
5. **Platform breakage** – Matrix sync stall (#12614, now fixed), Telegram downtime (#24140, now fixed), WSL browser issues (#27018), TUI crash on macOS (#27282), Unicode rendering in cron (#26128).

**Satisfaction signals:**
- The v0.14.0 release with 215 contributors is celebrated.
- Community humor (#10232 with 16 👍) suggests a lighthearted core user base.
- Feature PRs are actively reviewed and many land within weeks.

**Criticism / controversy:**
- Two issues ([#17688](https://github.com/NousResearch/hermes-agent/issues/17688), [#27266](https://github.com/NousResearch/hermes-agent/issues/27266)) accuse Hermes of plagiarizing the Evolver architecture from the Chinese team EvoMap. The claims focus on the self-evolution loop and memory system timeline. No maintainer response visible yet. This could affect community trust if not addressed.

## 8. Backlog Watch

Several important issues and PRs have been open for weeks without resolution or clear maintainer attention:

| Issue/PR | Created | Last Update | Comments/👍 | Why it matters |
|----------|---------|-------------|-------------|----------------|
| [#514](https://github.com/NousResearch/hermes-agent/issues/514) – A2A protocol | 2026-03-06 | 2026-05-17 | 12 comments, 4 👍 | Core interoperability feature; community expects roadmap. |
| [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) – Lazy tool schema | 2026-04-09 | 2026-05-17 | 8 comments, **10 👍** | Top-voted feature; token savings critical for local models. |
| [#4402](https://github.com/NousResearch/hermes-agent/issues/4402) – `gateway stop` kills all profiles | 2026-04-01 | 2026-05-17 | 4 comments, 1 👍 | Dangerous multi-profile UX bug. |
| [#7833](https://github.com/NousResearch/hermes-agent/issues/7833) – Delegate endpoint overwrite | 2026-04-11 | 2026-05-17 | 5 comments, 1 👍 | Related to today’s duplicates (#27294+), systemic delegation flaw. |
| [#25660](https://github.com/NousResearch/hermes-agent/pull/25660) – Single gateway, multiple agents | 2026-05-14 | 2026-05-17 | No maintainer activity | Huge PR touching 12+ components; needs careful review. |
| [#17688](https://github.com/NousResearch/hermes-agent/issues/17688) – Plagiarism allegation | 2026-04-30 | 2026-05-17 | 3 comments | Maintainer response absent; could escalate. |

**Recommendation:** Maintainers should prioritize a response to the plagiarism claims, address the delegation duplicates with a unified fix, and provide a timeline for the A2A and lazy schema features to keep community momentum high.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

**PicoClaw Project Digest – 2026-05-17**

---

### 1. Today's Overview  
The project remains in a high‑activity phase with **7 issues** and **5 PRs** updated in the last 24 hours. One new nightly release (`v0.2.8-nightly.20260517`) was published, continuing the rapid development cadence. A fresh feature request for **SiliconFlow provider support** (#2884) was opened and almost instantly paired with a corresponding PR (#2885) by the same author, signalling strong contributor momentum. The community is actively discussing integration enhancements (LM Studio, email channel) while the core team appears focused on channel multi‑account support and Web UI improvements. One bug (#2742) regarding gateway startup with no channels in v0.2.8 requires attention, but overall project health is robust.

---

### 2. Releases  
- **nightly (v0.2.8-nightly.20260517)** – Automated build from `main`.  
  - Full changelog: [compare/v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
  - ⚠️ **Warning**: Unstable – use in testing only.  
  - No breaking changes or migration notes were included in the release announcement.

---

### 3. Project Progress  
- **Merged/Closed PRs (today):**  
  - **#2881** – [feat: WeChat multi‑account configuration support](https://github.com/sipeed/picoclaw/pull/2881) (closed/merged). Adds backend CRUD, frontend management UI, and multi‑account state handling.  
  - **#2782** – [Feature: MCP client should support Streamable HTTP transport](https://github.com/sipeed/picoclaw/issues/2782) (closed). Although this was an issue, it was closed – likely resolved by a prior PR.

- **Open PRs (notably):**  
  - **#2885** – [feat(provider): add SiliconFlow provider support](https://github.com/sipeed/picoclaw/pull/2885) (opened today). Implements first‑class provider integration.  
  - **#2882** – [feat(chat): add independent code block copy and collapse controls](https://github.com/sipeed/picoclaw/pull/2882) – Web UI polish.  
  - **#2883** – [feat: WeChat multi‑account configuration](https://github.com/sipeed/picoclaw/pull/2883) – duplicate/revision of #2881? (still open).  
  - **#2835** – [fix(agent): always publish final reply after interim message](https://github.com/sipeed/picoclaw/pull/2835) – addresses a core interaction bug where final responses were suppressed after a `message` tool call.

---

### 4. Community Hot Topics  
- **#28** – [Feat Request: LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28) (19 comments, 2 👍) – *Stale*. The community wants a simplified setup for LM Studio, but no maintainer has stepped in. Suggests a desire for better local LLM integration.  
- **#1042** – [[BUG] exec工具的guardCommand方法问题](https://github.com/sipeed/picoclaw/issues/1042) (12 comments, 2 👍) – *Stale*. The `exec` tool’s safety guard incorrectly blocks `curl` calls to external URLs (e.g., weather queries). Active discussion on improving path detection.  
- **#2421** – [Feature: Add email as native channel](https://github.com/sipeed/picoclaw/issues/2421) (6 comments, 1 👍) – *Stale*. Users in corporate/legacy environments want email support. No implementation yet.  
- **#2884** – [Feature: Add siliconflow provider support](https://github.com/sipeed/picoclaw/issues/2884) (0 comments, opened today) – Immediately has a PR (#2885), indicating strong contributor alignment.

Underlying need: Users are pushing for broader connectivity – both local (LM Studio) and new cloud providers (SiliconFlow), plus unconventional channels (email). The community is also actively filing reports about tool safety false positives.

---

### 5. Bugs & Stability  
- **#2742** (Severity: **Medium**) – [[BUG] gateway starts with no channels in v0.2.8](https://github.com/sipeed/picoclaw/issues/2742). User reports that with `Telegram` enabled in config, the gateway starts without any channels. Likely a regression in stable 0.2.8. No fix PR yet.  
- **#1042** (Severity: **Medium**) – `guardCommand` false positive blocks legitimate commands (e.g., `curl wttr.in`). Discussed for months without a merged fix. PR could appear soon.  
- **#2835** (PR, open) – [Fix agent final reply suppression](https://github.com/sipeed/picoclaw/pull/2835). Addresses a bug where using the `message` tool in the same turn prevents the agent’s final text from being sent. Important for conversational UX.

No critical crashes or regressions have been reported in the last 24 hours.

---

### 6. Feature Requests & Roadmap Signals  
- **SiliconFlow provider** (#2884 / PR #2885) – Already in PR; likely to land in next nightly.  
- **Email as native channel** (#2421) – High demand from enterprise users, but no PR. Could appear in a future minor release.  
- **MCP Streamable HTTP** (closed #2782) – Now supported, enabling connections to modern MCP servers.  
- **WeChat multi‑account** (PR #2881 merged, #2883 still open) – Multiple accounts for the same channel is now a reality. Expect this in the next stable release.  
- **Update-from-source tutorial** (#2834) – A user requests documentation for upgrading; no solution yet.

**Prediction:** The next minor release (v0.2.9?) will include SiliconFlow provider, WeChat multi‑account, MCP Streamable HTTP, and the code block UI improvements.

---

### 7. User Feedback Summary  
- **Pain Points:**  
  - “I can only use openai compatible mode to connect siliconflow, which is inconvenient.” (#2884)  
  - “It would be nice to have an easy way to connect to LM Studio.” (#28)  
  - “After upgrading to v0.2.8, gateway starts with no channels.” (#2742)  
  - “I need a tutorial how to upgrade to new version.” (#2834)  

- **Satisfaction Signals:**  
  - Quick turnaround on SiliconFlow request (issue → PR same day).  
  - Merged WeChat multi‑account shows responsiveness to feature requests.  
  - Community contributors actively fixing bugs (e.g., #2835).  

- **Overall sentiment:** Users are engaged and grateful for the rapid evolution, but some friction remains around tooling (exec safety) and documentation/upgrade paths.

---

### 8. Backlog Watch  
- **#28** – *LM Studio Easy Connect* (stale since Feb 2026). No maintainer response; 19 comments show high community effort. Should be triaged.  
- **#1042** – *exec guardCommand bug* (stale since Mar 2026). The workaround is known, but no fix merged. Could block users relying on external APIs.  
- **#2834** – *Update from source* (opened 2026-05-09, no replies). Simple documentation gap – low effort to resolve but important for user onboarding.  
- **#2421** – *Email as native channel* (stale since Apr 2026). While not urgent, it is a recurring request; maintainers should at least add a “help wanted” or “future” label.

*All links: [PicoClaw GitHub](https://github.com/sipeed/picoclaw)*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-05-17

## 1. Today’s Overview

NanoClaw saw very high activity over the last 24 hours, with 6 issues updated (5 open, 1 closed) and 11 pull requests updated (9 merged/closed, 2 open). The project is clearly in a sprint mode: core infrastructure fixes, finance feature work, and new provider support are landing alongside a steady stream of community-reported bugs. No new release was cut today, but the volume of merged PRs suggests a release may be imminent once remaining blockers are resolved. Stability and reliability remain the community’s biggest concerns, with several reports of silent message drops, database corruption, and setup failures.

## 2. Releases

No new releases today. The latest release remains v2.0.63 (based on PR #2509 changelog alignment). No breaking changes or migration notes to report.

## 3. Project Progress (Merged/Closed PRs Today)

Nine PRs were merged or closed in the last 24 hours, spanning feature work, bug fixes, and documentation:

- **Finance Plan 3 – Schema & Bootstrap (PR #2486)** – First of three PRs for a finance skill reform. Adds schema definitions and bootstrap templates. No source code changes.  
- **Finance Plan 3 – Levis Behavior (PR #2487)** – Second PR of the finance plan, adds skill template for Levis agent behavior. Depends on #2486.  
- **Cron Output Fix (PR #2481)** – Two independent bugs that caused scheduled cron firings to be acked but never delivered. Fixes prevent silent suppression of cron output across all agents.  
- **CLI Mode for Interactive Quota (PR #2470)** – Adds `runCliQuery()` path to agent-runner, allowing use of `claude --print --resume` instead of Agent SDK for groups with `useCliMode: true`. Includes 40 unit tests.  
- **WhatsApp Recovery Guidance (PR #2469)** – Corrects operator instructions for decrypt-failure and 401 logout; replaces incorrect `launchctl kickstart` with session cleanup steps.  
- **Telegram Inline Keyboard Buttons (PR #2515)** – Adds `InlineButton` and `SendMessageOptions` types, updates `send_message` MCP tool with optional buttons parameter, passes through IPC to Telegram channel.  
- **Platform m1 (PR #2519)** – Closed as `[follows-guidelines]`, likely a template or skill addition for M1 Mac platform support.  
- **Feat/restart no nanoclaw (PR #2476)** – Another guidelines-compliant PR, likely adding a restart skill or container restart logic.  
- **Changelog Alignment (PR #2509)** – Documentation fix to align v2.0.63 rollup line with `RELEASING.md` voice.

## 4. Community Hot Topics

The most discussed issues today are:

- **#2512 – OneCLI-Postgres intercommunication failure** (closed, 1 comment) – A Docker bridge network issue where containers cannot resolve hostnames. The user’s comment likely contains a workaround or the devs closed it with a fix.  
- **#2506 – `send_message` dedup silently drops responses** (open, 1 comment) – Agent responses vanish when two turns complete within 60 seconds or when a follow-up arrives during streaming. Community is likely frustrated by silent data loss.  
- **#2517 – MGA references archived agent_groups** (open, 0 comments) – Discovered during cross-check audit. Points to a data integrity issue: MGA rows point to archived groups without automatic unarchive, requiring garbage collection.  
- **#2518 – Codex provider feature PR** (open) – This new provider would add a Codex (OpenAI?) alternative alongside Claude. The PR is generating interest as it enables multi-LLM support, a frequently requested capability.

Underlying need: the community wants reliability (especially around message delivery) and multi-provider flexibility.

## 5. Bugs & Stability

**High severity:**
- **Silent message drop (Issue #2506)** – Agent responses silently disappear under timing conditions. No fix PR yet; could cause significant user trust issues.  
- **Setup stuck on needrestart whiptail (Issue #2514)** – Ubuntu setup blocks indefinitely on a dialog prompt. Blocks new users from completing installation.  
- **Colima CA cert bind-mount silently empty (Issue #2513)** – On macOS with Colima, all HTTPS fails because the CA certificate mount becomes an empty directory. Blocks all agents using HTTPS APIs.  
- **Stale outbound.db journal after SIGKILL (Issue #2516)** – Container kills leave partial database journal files, preventing host delivery poll from reading `outbound.db`. No fix PR yet, but a design proposal in the issue.

**Medium severity:**
- **OneCLI-Postgres intercommunication (Issue #2512, closed)** – Appears fixed; likely a documentation or config change.

**Fix PRs in flight:**
- **PR #2510** (open) – Fixes CLI receiver `inbound.db` hydration when adding approval-path destinations.  
- **PR #2481** (merged) – Fixed cron output suppression.  
- **PR #2469** (merged) – Fixed WhatsApp recovery guidance (operator UX fix, not a code bug).

## 6. Feature Requests & Roadmap Signals

The following features landed or are in review, indicating near-term roadmap priorities:

- **Multi-provider support** – PR #2518 (open) adds a Codex provider alongside Claude, suggesting a strategic move to support multiple LLM backends.  
- **CLI mode alternative (merged #2470)** – Allows using the `claude` CLI directly instead of the Agent SDK, enabling interactive quota usage. This expands deployment flexibility.  
- **Finance Plan 3 (merged #2486, #2487)** – A three-PR finance skill reform; the third PR (behaviors) is still pending. Likely targeted for next release.  
- **Telegram inline keyboards (merged #2515)** – Enhances Telegram channel interaction, allowing rich button-based UIs.  
- **Platform M1 support (closed #2519)** – Suggests efforts to improve compatibility on Apple Silicon.

Predictions for next release: Codex provider, the remaining Finance Plan 3 PR, fixes for #2506 and #2516, and possibly Colima certificate handling improvements.

## 7. User Feedback Summary

Real user pain points expressed this week:

- **“On a default install on an Ubuntu machine intercommunication between onecli and postgres fails”** – Docker networking confusion, resolved but highlights documentation gaps.  
- **“Agent responses are silently dropped and the client times out”** – Two users (mshirel and maybe others in #2506) report message loss; trust in the system is undermined.  
- **“Setup runs far too long… waiting for dialog confirmation”** – User b1rdex shows a screenshot of `needrestart` blocking setup. Setup UX needs non-interactive handling.  
- **“On macOS with Colima as the Docker runtime, agent containers can’t reach api.anthropic.com”** – Certificate mount issue. User p2c2e points to a common macOS setup pitfall.  
- **“MGA references archived agent_groups”** – Discovered during audit, indicates data integrity problem in production databases. User kenansun-dev-bot flagged a cross-check finding.

Satisfaction signals: The high number of merged PRs (especially quick fixes like #2469) shows the team is responsive. The community’s willingness to report detailed issues (with screenshots and root-cause analysis) indicates an engaged user base.

## 8. Backlog Watch

No issues have gone unanswered for more than a few days – all items are recent. However, two items need maintainer attention:

- **Issue #2506 (silent message drop)** – Open since 2026-05-16 with only 1 comment. This is a high-impact bug; a maintainer should assign or comment on a fix timeline.  
- **PR #2510 (CLI fix for inbound.db)** – Open since 2026-05-16. This is a bug fix PR that appears to lack reviewer attention.  
- **Issue #2517 (MGA archive references)** – Important data integrity concern; needs discussion on whether to implement the suggested unarchive-on-reference + GC.

No long-unanswered issues from previous weeks were found in this data window.

*All links are relative to `github.com/nanocoai/nanoclaw`.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-05-17

## 1. Today's Overview

The project saw **high activity** with **44 pull requests updated** (18 merged/closed, 26 open) and **6 issues updated** (5 open, 1 closed) in the last 24 hours. Development momentum remains centered on the **Reborn architecture rewrite**, with major PRs advancing composition root consolidation (#3695), boot-config file loading (#3704), WebUI thread scoping (#3725), and a sweeping FS‑dispatch fabric merge (#3679). Security‑related dependency bumps (#3719) and a nightly E2E pipeline failure (#3447) also drew attention. No new releases were cut today.

## 2. Releases

**None.** No new versions were published in the last 24 hours.

## 3. Project Progress

**Merged / closed PRs today (selected from the top‑20 list and issue data):**

- **#3724** – *feat(reborn): webui turn scope* – Closed. Binds WebUI caller + thread_id through `SessionThreadService` and prevents implicit thread creation.  
- **#3723** – *[codex] replace agent-loop planning docs* – Closed. Removes old planning documents and adds concise `CLAUDE.md` guidance across Reborn surfaces.  
- **#3719** – *chore(deps): bump deps to address security advisories* – Closed. Patches `rustls-webpki` (CRL panic), `h2` (HTTP/2 stack overflow), and `hyper` (HTTP/2 resource exhaustion).  
- **#3417** – *chore(deps): bump fast-uri (docs/architecture-video)* – Closed. Security release for fast-uri.

**Other notable open PRs with substantial progress:**

- **#3695** (XL, open) – Considers `ironclaw_reborn_composition` the Reborn composition root, ships a live binary, narrows public surface.  
- **#3704** (XL, open) – Landed boot‑config TOML + provider catalog for the standalone Reborn binary.  
- **#3679** (XL, open, DB MIGRATION) – Applies a universal `RootFilesystem` dispatch fabric across consumer crates (+15k LOC).  
- **#3681** (L, open) – Adds a first‑party HTTP egress tool (`builtin.http`).  
- **#3683** (XL, open) – Adds host‑owned HTTP ingress contracts for Reborn in `ironclaw_host_api`.  
- **#3720** (XL, open) – Verifies durable tool‑result reference transcripts across all storage backends.  
- **#3722** (XL, open) – Preserves provider tool‑call metadata throughout the Reborn loop.  
- **#3721** (M, open) – Gates personal‑context identity files (`USER.md`, `context/assistant-directives.md`) by run profile.  
- **#3717** (S, open) – Wires the planned Reborn run‑profile resolver into production composition.  
- **#3632** (XL, open) – Adds a `BeforeInboundPolicy` seam for WebUI message validation/rewriting.

## 4. Community Hot Topics

**Most active Issues (by comments):**

- **#3692** – *[OPEN] Reborn: add policy‑gated personal identity and heartbeat prompt context* (4 comments, 👍0)  
  [Issue #3692](https://github.com/nearai/ironclaw/issues/3692)  
  Discussion around scoping stable identity‑file context and two deferred context surfaces (policy‑gated personal identity, heartbeat). Signals need for fine‑grained prompt context control in the Reborn loop.

- **#3036** – *[OPEN] [EPIC] Configuration‑as‑Code for IronClaw Reborn: tenant blueprints and use‑case harnesses* (4 comments, 👍1)  
  [Issue #3036](https://github.com/nearai/ironclaw/issues/3036)  
  A long‑standing epic requesting declarative configuration (schema‑driven `.env`, workspace docs, settings, extensions) for tenant operators. High impact for operational tooling.

**Most active Pull Requests (by size/scope, though comment counts are undefined):**

- **#3695** – *arch(reborn): consolidate composition root, narrow public surface, ship live binary* – Core contributor, XL size, low risk. Central to Reborn architecture.  
- **#3679** – *feat(reborn): apply universal FS dispatch across consumer crates* – XL, DB migration, heavily stacked commits.  
- **#3724** – *feat(reborn): webui turn scope* – Despite being closed, had broad scope tags (agent, channel, tool, db, ci, etc.), indicating cross‑cutting impact.

**Underlying needs:** Operators and core developers are pushing for architectural clarity (composition root), operator‑friendly boot‑config files, robust WebUI threading, and security hygiene (dependency bumps).

## 5. Bugs & Stability

**High severity:**

- **#3447** – *[OPEN] Nightly E2E failed* – Updated today. Nightly E2E pipeline failure on commit `b921b42` (v2‑engine job). No fix PR referenced yet.  
  [Issue #3447](https://github.com/nearai/ironclaw/issues/3447)

**Medium severity:**

- **#3719** – *Closed PR* – Fixed three security advisories: `rustls-webpki` panic, `h2` stack overflow, `hyper` resource exhaustion. Promptly merged.  
  [PR #3719](https://github.com/nearai/ironclaw/pull/3719)

- **#3707** – *[OPEN] chore(deps): bump jsonwebtoken 9.3.1 → 10.3.0* – Significant jump with breaking changes; still open.  
  [PR #3707](https://github.com/nearai/ironclaw/pull/3707)

- **#3361 / #3360 / #3247** – Group dependency bumps (tokio‑ecosystem, wasm, everything‑else) – open for 10–12 days. Merging is likely blocked by validation or breaking changes.

**Stability concerns:** The nightly E2E failure (#3447) is the most pressing issue – no root cause or fix PR has appeared yet. Security fixes were expedited (#3719), which is positive.

## 6. Feature Requests & Roadmap Signals

**User‑facing requests (from issues):**

- **#3036** – *Configuration‑as‑Code (EPIC)* – Declarative tenant blueprints and use‑case harnesses. Still open; likely a long‑term roadmap item.  
- **#3692** – *Policy‑gated personal identity and heartbeat context* – Would allow operators to control what personal context (e.g., `USER.md`) the agent sees per run profile. Likely next milestone.  
- **#3702** – *[OPEN] Reborn: revise and implement binary‑E2E test framework plan* – New issue (May 16) calling for a standalone binary E2E test strategy. Expected to land soon as part of Reborn maturity.  
- **#3534** – *[CLOSED] Create a tool that downloads logs for debugging* – Now implemented (closed May 16). Indicates operator demand for debugging tools.

**Roadmap predictions (next release likely includes):**

- Reborn composition root (#3695) + boot‑config file (#3704) + live binary  
- WebUI threading and ingress contracts (#3725, #3683)  
- Before‑inbound policy seam (#3632) for message validation  
- Run‑profile resolvers and personal‑context gating (#3717, #3721)  
- Security patches and dependency updates (#3719, but still open PRs for others)

## 7. User Feedback Summary

- **CI reliability pain point:** Nightly E2E failure (#3447) directly affects developers and operators relying on continuous integration. No fix yet.  
- **Operator configuration friction:** #3036 (Config‑as‑Code) and #3692 (policy‑gated personal context) reflect frustration with manual `.env`/settings/extension management.  
- **Security concerns:** Proactive bumps (#3719) show responsiveness; but lingering open dependency PRs (jsonwebtoken, tokio, wasm) may worry users expecting regular updates.  
- **Positive signal:** #3534 closed – log download tool was requested and delivered, satisfying user debugging needs.

Overall sentiment appears neutral‑to‑positive for architecture progress but with notable CI and security‑update latency.

## 8. Backlog Watch

Issues / PRs that have remained open for multiple days without maintainer resolution:

- **#3036** – *[EPIC] Configuration‑as‑Code* – Created Apr 28, last updated May 16. No maintainer response or milestone tagged. High community demand (👍1).  
- **#3447** – *Nightly E2E failed* – Created May 10, updated May 17. No comments or fix PR. Pipeline reliability is at risk.  
- **#3361** – *deps: bump everything‑else group (43 updates)* – Created May 7, open for 10 days. Likely blocked by breaking changes.  
- **#3360** – *deps: bump tokio‑ecosystem group (6 updates)* – Same timeframe.  
- **#3247** – *deps: bump wasm group (4 updates)* – Same timeframe.  

These dependabot PRs need either merging with necessary code adaptations or explicit closure with reasoning. The E2E failure (#3447) deserves immediate investigate‑and‑fix, especially given its nightly cadence.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-05-17

## 1. Today's Overview

Project activity was moderate today, driven by the merger of a release integration branch (release/2026.5.15) into main. A total of 8 pull requests were closed or merged, while 8 remain open. Only one new issue was reported, concerning an AI engine connection loss on the desktop app. Several stale PRs continue to await review, many of which have been open for over seven weeks. No new releases were published today, but the release train merge signals that a new version (2026.5.16) is now part of the main branch.

## 2. Releases

No new releases were created today. The latest version remains as previously recorded.

## 3. Project Progress

Today’s merged/closed PRs indicate a focus on releasing accumulated fixes and optimizations:

- **Release train merge** – PR [#1998](https://github.com/netease-youdao/LobsterAI/pull/1998) (labeled areas: renderer, build, docs, main, openclaw, cowork, im, artifacts) merged the release/2026.5.15 branch into main, bundling product fixes, build attribution work, artifacts UX improvements, IM onboarding, and Cowork/OpenClaw changes.
- **Reasoning content fixes** – PR [#1994](https://github.com/netease-youdao/LobsterAI/pull/1994) fixed reasoning content display for the Mimo model in multi-turn sessions, and PR [#1999](https://github.com/netease-youdao/LobsterAI/pull/1999) provided a similar fix labeled as docs.
- **Default model updates** – PR [#1997](https://github.com/netease-youdao/LobsterAI/pull/1997) updated default models for various AI providers.
- **Dream UI optimizations** – PRs [#1995](https://github.com/netease-youdao/LobsterAI/pull/1995) and [#1996](https://github.com/netease-youdao/LobsterAI/pull/1996) optimized the Dream UI (renderer, cowork, main, openclaw areas).
- **Performance and infrastructure** – Two older PRs were also closed today: PR [#871](https://github.com/netease-youdao/LobsterAI/pull/871) added Skill execution statistics display, and PR [#812](https://github.com/netease-youdao/LobsterAI/pull/812) debounced SQLite save operations and cached configuration reads to reduce main-thread blocking.

No breaking changes were documented in these merges.

## 4. Community Hot Topics

Community discussion remains low. The only issue generated today:

- **Issue #1993** – ["AI engine connection lost issue"](https://github.com/netease-youdao/LobsterAI/issues/1993) (1 comment, 0 reactions). The reporter states that the desktop application consistently loses AI engine connection, while the IM Bot works reliably. This suggests a desktop-specific networking or initialization problem. No PRs have been linked yet.

Open PRs with the longest history remain without new comments or reactions:

- PR [#762](https://github.com/netease-youdao/LobsterAI/pull/762) (auto-detect API format)
- PR [#768](https://github.com/netease-youdao/LobsterAI/pull/768) (Opik observability integration)
- PR [#770](https://github.com/netease-youdao/LobsterAI/pull/770) (React.memo for MarkdownContent)
- PR [#771](https://github.com/netease-youdao/LobsterAI/pull/771) (image thumbnail preview)
- PR [#783](https://github.com/netease-youdao/LobsterAI/pull/783) (bottom input area spacing fix)
- PR [#787](https://github.com/netease-youdao/LobsterAI/pull/787) (theme service destroy method)
- PR [#788](https://github.com/netease-youdao/LobsterAI/pull/788) (deduplicate scheduled tasks)

None have received comments or reactions since creation, indicating low community engagement on these proposals.

## 5. Bugs & Stability

One new bug was reported today:

- **AI engine connection loss (desktop app)** – Issue [#1993](https://github.com/netease-youdao/LobsterAI/issues/1993). **Severity: High** – prevents desktop app from functioning properly. The reporter notes that the IM Bot works fine, isolating the problem to the desktop client. No fix PR has been opened yet.

Two bug-fix PRs were merged today as part of the release train:

- PR [#1994](https://github.com/netease-youdao/LobsterAI/pull/1994) – fix for reasoning content in Mimo model (multi-turn).
- PR [#1999](https://github.com/netease-youdao/LobsterAI/pull/1999) – additional fix for reasoning_content return.

No regressions or crash reports were noted.

## 6. Feature Requests & Roadmap Signals

Several feature-rich PRs remain open and may be candidates for the next version:

- **Auto-detect API format** – PR [#762](https://github.com/netease-youdao/LobsterAI/pull/762) simplifies configuration for DeepSeek, Zhipu, MiniMax, and custom models by automatically detecting whether the provider uses Anthropic- or OpenAI-compatible protocols.
- **Observability integration** – PR [#768](https://github.com/netease-youdao/LobsterAI/pull/768) adds an Opik tab in settings via OpenClaw plugin, with extensibility planned for LangFuse/LangSmith.
- **Performance improvements** – PR [#770](https://github.com/netease-youdao/LobsterAI/pull/770) (React.memo for MarkdownContent) and PR [#812](https://github.com/netease-youdao/LobsterAI/pull/812) (debounced SQLite saves, already merged) indicate ongoing optimization efforts.
- **UI enhancements** – PR [#771](https://github.com/netease-youdao/LobsterAI/pull/771) (image thumbnails in cowork attachments) and PR [#783](https://github.com/netease-youdao/LobsterAI/pull/783) (bottom spacing fix) improve the attachment and input experience.
- **Theme service cleanup** – PR [#787](https://github.com/netease-youdao/LobsterAI/pull/787) adds a destroy method to prevent memory leaks.
- **Task deduplication** – PR [#788](https://github.com/netease-youdao/LobsterAI/pull/788) prevents duplicate scheduled tasks after restart.

Given the release train just merged, the next minor release may include these pending features, especially the auto-detect API format and observability integration, which have broad user benefit.

## 7. User Feedback Summary

The sole user report (Issue #1993) describes a **critical frustration**: the desktop application fails to maintain an AI engine connection, while the same functionality works via the IM Bot. This points to a potential difference in network handling, service disposal, or authentication between the two interfaces. The user’s tone suggests dissatisfaction, as they are unable to use the desktop app reliably.

No other explicit user satisfaction or dissatisfaction signals were recorded today. The many stale PRs, however, may indicate that contributors are awaiting merge decisions, which can indirectly reflect on community momentum.

## 8. Backlog Watch

Several important PRs remain open with no updates for over seven weeks. Maintainers should prioritize review and merge decisions:

| PR | Title | Last Updated | Days Open |
|----|-------|--------------|-----------|
| [#762](https://github.com/netease-youdao/LobsterAI/pull/762) | feat(settings): auto-detect API format | 2026-05-17 (same day) | 54 |
| [#768](https://github.com/netease-youdao/LobsterAI/pull/768) | feat(observability): Opik integration | 2026-05-17 | 54 |
| [#770](https://github.com/netease-youdao/LobsterAI/pull/770) | perf(renderer): React.memo for MarkdownContent | 2026-05-17 | 54 |
| [#771](https://github.com/netease-youdao/LobsterAI/pull/771) | feat(cowork): image thumbnail preview | 2026-05-17 | 54 |
| [#783](https://github.com/netease-youdao/LobsterAI/pull/783) | fix(cowork): bottom input spacing | 2026-05-17 | 53 |
| [#787](https://github.com/netease-youdao/LobsterAI/pull/787) | Implement destroy method for theme service | 2026-05-17 | 53 |
| [#788](https://github.com/netease-youdao/LobsterAI/pull/788) | fix(scheduled-task): deduplicate tasks | 2026-05-17 | 53 |
| [#1766](https://github.com/netease-youdao/LobsterAI/pull/1766) | chore(deps-dev): bump vite to 8.0.13 | 2026-05-16 | 27 |

These PRs cover performance, usability, and infrastructure improvements. The vite dependency bump (#1766) may become a maintenance requirement as older versions lose support.

**Project health summary**: The project shows active release management and ongoing development, but the high number of stale PRs and the single unresolved desktop connectivity bug suggest that maintainer bandwidth may need to increase to sustain community momentum.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-17

## 1. Today's Overview
Activity has been moderate, with three open issues and two open pull requests updated in the last 24 hours, but no new releases or merged contributions. The project is actively addressing bugs related to Gemini reasoning tags and TTS configuration handling, while also expanding remote access capabilities and OpenAI Codex integration via outstanding PRs. No code has been merged today, indicating a focus on review and refinement. Overall project health appears stable, though the lack of closed issues or merged PRs suggests a slower processing cadence.

## 2. Releases
No new releases were published in the last 24 hours. The latest releases remain unchanged.

## 3. Project Progress
No pull requests were merged or closed today. All two open PRs remain under review:
- **PR #1002** (feat: remote-access – NetBird & Cloudflare Tunnel support) – last updated 2026-05-16
- **PR #1005** (feat: reasoning effort for OpenAI Codex) – last updated 2026-05-16

No feature advancements or fixes have been merged.

## 4. Community Hot Topics
All open issues and PRs currently have zero comments and zero reactions, so no single topic has drawn exceptional community engagement. The items generating discussion (though none yet) are:
- **Issue #1007** – Bug: Gemini 4‑31B reasoning tags treated as plain text  
  ([link](https://github.com/moltis-org/moltis/issues/1007))
- **Issue #1006** – Bug: VoiceCoquiTtsConfig defaults stripped during auto-compact  
  ([link](https://github.com/moltis-org/moltis/issues/1006))
- **Issue #1004** – Feature: Non‑blocking `spawn_agent`  
  ([link](https://github.com/moltis-org/moltis/issues/1004))
- **PR #1002** – Remote access (NetBird & Cloudflare Tunnel)  
  ([link](https://github.com/moltis-org/moltis/pull/1002))
- **PR #1005** – Reasoning effort for Codex  
  ([link](https://github.com/moltis-org/moltis/pull/1005))

Underlying needs include better multimodal model support (reasoning tags), configuration robustness, and non‑blocking agent operations.

## 5. Bugs & Stability
Two bugs were reported today, both classified as open and unaddressed:

- **High severity** – **Issue #1007**: Gemini 4‑31B `<thought>` reasoning tags are interpreted as plain text rather than reasoning blocks. This can break expected agent behavior when using reasoning models. No fix PR exists yet.  
  ([link](https://github.com/moltis-org/moltis/issues/1007))

- **Medium severity** – **Issue #1006**: `VoiceCoquiTtsConfig` defaults are lost during auto‑compaction, causing the TTS configuration to appear missing. This is a data‑integrity issue affecting voice synthesis. No fix PR exists yet.  
  ([link](https://github.com/moltis-org/moltis/issues/1006))

No regression reports or crash reports were filed.

## 6. Feature Requests & Roadmap Signals
One feature request was opened today and one from yesterday:

- **Issue #1004** (May 16) – Non‑blocking `spawn_agent`: allows parent sessions to remain responsive during long sub‑agent runs. This is a user experience improvement likely to be addressed if aligned with the project’s concurrency goals.  
  ([link](https://github.com/moltis-org/moltis/issues/1004))

- **PR #1005** – Adds `reasoning_effort` support to OpenAI Codex, including serialization of GPT‑5 Codex effort in Responses API. This is likely to be included in the next minor release as it enhances Codex model compatibility.

- **PR #1002** – Adds NetBird private mesh and Cloudflare Tunnel support, expanding remote access features. This is a substantial feature that may appear in a future version.

Predictions: Next release will likely include reasoning effort support (PR #1005) and possibly remote‑access enhancements (PR #1002) if review completes quickly. The non‑blocking spawn agent may be scheduled for after these PRs.

## 7. User Feedback Summary
While no explicit satisfaction/dissatisfaction comments exist, the bug reports and feature request reveal real user pain points:
- **Multimodal reasoning handling**: Users leveraging Gemma 4‑31B expect reasoning tags to be parsed correctly; current behavior degrades model output.
- **Configuration reliability**: TTS config disappearing is a data loss issue that undermines trust in the system.
- **Concurrency limitations**: Blocking during sub‑agent execution is a usability friction for complex workflows.

These indicate that users are actively deploying Moltis with advanced models and voice synthesis, and expect robust defaults and non‑blocking operations.

## 8. Backlog Watch
No long‑unanswered issues or PRs were identified in the last 24 hours. All open items are recent (May 15–17) and have not yet received maintainer responses. Maintainer attention is needed on:
- **Issue #1007** (reasoning tags bug) – high impact, should be triaged quickly.
- **Issue #1006** (TTS config bug) – medium impact, requires investigation.

Both PRs (#1002, #1005) are also awaiting review to unblock feature progress.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-17

## 1. Today's Overview

The CoPaw project shows moderate activity with **16 issues** and **12 pull requests** updated in the last 24 hours. **13 open issues** and **8 open PRs** indicate a healthy but slightly backlogged state. Three issues were closed, and four PRs were merged or closed. Notably, there are **no new releases** today, and the project is currently processing a wave of E2E testing infrastructure work alongside several user-reported bugs. The community is actively discussing configuration enhancements and critical stability issues (chat freezing, context compaction failures), while maintainers are merging legacy refactoring and fixes.

---

## 2. Releases

**None.** No new versions were published today.

---

## 3. Project Progress

**4 PRs were merged or closed today** (all closed, not all necessarily merged – verify with repo details). The following represent tangible progress:

- **[PR #3605 – refactor(wechat): centralize legacy weixin → wechat data migrations on workspace startup](https://github.com/agentscope-ai/CoPaw/pull/3605)** — Cleaned up inconsistent identifier rename migrations.
- **[PR #1669 – fix(Workspace): handle path separators correctly in workspace path…](https://github.com/agentscope-ai/CoPaw/pull/1669)** — Resolved a long-standing bug causing workspace path to show "loading…" indefinitely, especially on Windows.
- **[PR #1661 – fix(workspace): fix memory files not being fetched by agent ID](https://github.com/agentscope-ai/CoPaw/pull/1661)** — Fixed daily memory retrieval scoping per agent/bot folder.
- **[PR #3246 – feat(qq): add configurable instant acknowledgment message](https://github.com/agentscope-ai/CoPaw/pull/3246)** — First-time contributor PR to improve QQ channel responsiveness by sending an instant ack while the agent processes.

Additionally, **ongoing open PRs** that advanced today include:
- **PR #4041** (system tray for Windows) – under review since May 5.
- **PR #4444** (Grok provider integration via xAI OAuth) – new feature.
- **PR #4443** (lightweight goal mode `/goal`) – new session-scoped objectives system.

---

## 4. Community Hot Topics

The most active discussions (by comment count and reactions) center on configuration flexibility and critical user-facing bugs:

- **[Issue #4455 – feat(skills): support multiple external skill paths via config](https://github.com/agentscope-ai/CoPaw/issues/4455)**  
  *5 comments* — Proposal to allow users to add custom skill directories in `config.json` alongside the default `skill_pool`. The core team is discussing implementation details and backward compatibility.

- **[Issue #4453 – [Question] 聊天窗口聊天无回应 (Chat window not responding)](https://github.com/agentscope-ai/CoPaw/issues/4453)**  
  *3 comments, 1 👍* — User reports chat freeze after sending messages; switching models and restarting Docker did not help. Error indicates an event loop stopped unexpectedly. This is a **high-severity usability blocker** for Chinese users.

- **[Issue #4450 – Simplify approval commands: short aliases + session/always scopes](https://github.com/agentscope-ai/CoPaw/issues/4450)**  
  *1 comment* — Feature request to document and extend `/approve`/`/deny` commands with scoping (once/session/always). The author notes the short commands already exist in v1.1.7 but are undocumented.

- **[Issue #4448 – [Bug]: Context compaction often fails with "invalid format"](https://github.com/agentscope-ai/CoPaw/issues/4448)**  
  *2 comments* — Reported twice (duplicate #4447). Affects long conversations; no fix PR yet.

The **E2E testing milestone** (hanson‑hex) generated 6 issues today (#4457–#4462) but these are low-discussion planning items.

---

## 5. Bugs & Stability

| Severity | Bug | Issue | Status | Fix PR exists? |
|----------|-----|-------|--------|----------------|
| **Critical** | Chat window freezes after sending messages (event loop error) | [#4453](https://github.com/agentscope-ai/CoPaw/issues/4453) | Open, active | No |
| **High** | `/mission` command causes console freeze (process alive but UI unresponsive) | [#4454](https://github.com/agentscope-ai/CoPaw/issues/4454) | Open, active | No |
| **High** | Rate-limit 429 triggers `zero_downtime_reload` → wipes pending messages permanently, leaving agent "frozen" | [#4449](https://github.com/agentscope-ai/CoPaw/issues/4449) | Open, active | No |
| **Medium** | Context compaction fails frequently with "missing ## header" during long conversations | [#4448](https://github.com/agentscope-ai/CoPaw/issues/4448) | Open, duplicate (#4447) | No |
| **Medium** | Importing `runner.*` eagerly pulls full stack, causing import failures in test environments | [#4445](https://github.com/agentscope-ai/CoPaw/issues/4445) | Open | Yes – [PR #4446](https://github.com/agentscope-ai/CoPaw/pull/4446) (under review) |

**Note:** Three of the top four bugs involve complete UI or messaging freezes, signaling a need for urgent stability investigation.

---

## 6. Feature Requests & Roadmap Signals

- **[External skill paths (#4455)](https://github.com/agentscope-ai/CoPaw/issues/4455)** — High demand for flexible skill sourcing; likely to land in v1.1.8.
- **[Interactive approval buttons for Telegram/QQ (#4451)](https://github.com/agentscope-ai/CoPaw/issues/4451)** — User experience improvement for channel interactions; complements WebUI's existing approval UI.
- **[Lightweight goal mode (#4443)](https://github.com/agentscope-ai/CoPaw/pull/4443)** — Already in PR; adds `/goal` commands for persistent session objectives. Likely to be merged soon.
- **[Grok provider integration (#4444)](https://github.com/agentscope-ai/CoPaw/pull/4444)** — Adds support for xAI's Grok models with OAuth. If merged, expands model options significantly.
- **[E2E testing infrastructure (#4457–#4462)](https://github.com/agentscope-ai/CoPaw/issues/4457)** — Foundation for automated UI smoke tests; indicates maintainers are investing in quality assurance for the frontend.

---

## 7. User Feedback Summary

**Pain points:**
- **Freezes & unresponsiveness** – Multiple users report complete freeze after `/mission` command, or after sending messages in chat (#4453, #4454). Workarounds (reset session, clear directories) are ineffective.
- **Unexpected data loss** – Rate-limit handling (`429`) silently destroys pending messages (#4449), leaving users waiting indefinitely.
- **Context compaction reliability** – Long conversations are disrupted by persistent compaction errors (#4448).
- **Undocumented features** – The `/approve`/`/deny` short commands exist in v1.1.7 but are not mentioned in help text, confusing users (#4450).

**Satisfaction signals:**
- The E2E testing effort (hanson‑hex) shows maintainer commitment to quality.
- Contributor activity remains steady (4 first-time-contributor PRs open or recently merged).

---

## 8. Backlog Watch

The following open issues/PRs have been awaiting attention for a prolonged period:

- **[PR #2771 – fix(install): restrict mlx-lm to Apple Silicon macOS](https://github.com/agentscope-ai/CoPaw/pull/2771)**  
  *Open since April 1, updated May 17* — Simple fix still under review; likely blocked by CI or release scheduling.

- **[PR #4041 – feat(cli-desktop): system tray startup item (win32 only)](https://github.com/agentscope-ai/CoPaw/pull/4041)**  
  *Open since May 5, first-time contributor* — Appears functionally complete but has not moved beyond "Under Review" in 12 days.

- **[Issue #4452 – [TEST] 工具调用测试 – 不应合并 (test issue, do not merge)](https://github.com/agentscope-ai/CoPaw/issues/4452)**  
  *Closed* — This was a test issue, not actionable.

- **Older open PRs** (e.g., #4084, #4173, #4303) have been updated recently but are still pending review/merge. The high volume of E2E work may be diverting reviewer capacity.

---

*Generated from GitHub data for 2026-05-17. All links use `https://github.com/agentscope-ai/CoPaw` as base.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw Project Digest — 2026-05-17

### 1. Today's Overview
ZeroClaw recorded a very active 24‑hour period with **50 issues** and **50 pull requests** updated, reflecting a healthy development cadence. Of those, 5 issues and 6 PRs were closed or merged, though **no formal release** was cut. The project is processing a high volume of community feedback and bug reports, with maintainers actively triaging and merging fixes. Several high‑priority bugs (e.g., streaming errors, context compressor drop) have received associated fix PRs, indicating responsive maintenance. The v0.8.0 multi‑agent runtime PR remains open and is a major focus for the upcoming beta release.

### 2. Releases
No new releases were published today. The last tagged version remains `zeroclaw 0.7.4` (referenced in issue #6659).

### 3. Project Progress
Only one PR was closed/merged today, but it is a substantial dashboard improvement:

- **PR #6728** (CLOSED) — *feat(web-dashboard): M5.0 — Overview page + shared SectionNav*  
  Adds an `/overview` page with read‑only summary cards for memory, crons, integrations, and skills, pulling from existing API endpoints. Also introduces a shared `SectionNav` component.  
  [zeroclaw-labs/zeroclaw Pull Request #6728](https://github.com/zeroclaw-labs/zeroclaw/pull/6728)

No other PR closures were recorded in the provided dataset. The six closed or merged PRs in the last 24h (per the overview) likely include other minor fixes not listed in the top‑20 view.

### 4. Community Hot Topics
The following issues and PRs generated the most discussion and reactions:

- **Issue #6123** (CLOSED) — *[Bug]: default_model issue on fresh install*  
  18 comments. A fresh install fails because `default_model` is not set during onboarding, blocking the agent workflow.  
  [zeroclaw-labs/zeroclaw Issue #6123](https://github.com/zeroclaw-labs/zeroclaw/issues/6123)

- **Issue #5600** (OPEN) — *[Bug]: Use kimi-code provider in streaming chat call tools, provider API reports an error*  
  8 comments, 1 👍. Streaming calls to kimi‑code fail with a 400 error related to `reasoning_content`. Still needs reproduction.  
  [zeroclaw-labs/zeroclaw Issue #5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)

- **Issue #2467** (OPEN) — *[Feature]: Webhook transforms*  
  5 comments. Request for custom webhook paths and payload inspection — still blocked.  
  [zeroclaw-labs/zeroclaw Issue #2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467)

- **Issue #5601** (OPEN) — *[Feature]: Add subscription-native OAuth support for Ollama Cloud, z.ai, Kimi, MiniMax*  
  5 comments, 1 👍. A well‑structured proposal to extend OAuth login support beyond the three already implemented providers.  
  [zeroclaw-labs/zeroclaw Issue #5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)

- **Issue #6269** (OPEN) — *Context compressor drops reasoning_content from compressed assistant messages*  
  4 comments. Systematic loss of reasoning content during proactive compression impacts providers that require it.  
  [zeroclaw-labs/zeroclaw Issue #6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269)

**Underlying needs:** Users are experiencing real friction during onboarding (missing defaults), provider incompatibilities, and missing features for advanced use cases (webhooks, OAuth). The community is highly engaged in shaping the roadmap.

### 5. Bugs & Stability
Several new bugs were filed today, along with existing ones that were updated. They are ranked by severity:

| Issue | Severity | Summary | Fix PR exists? |
|-------|----------|---------|----------------|
| #6399 (CLOSED) | S1 – workflow blocked | Custom remote provider sends local image file paths instead of data URLs, breaking multimodal requests on arm64 | Yes, closed as accepted (but fix not listed) |
| #5600 (OPEN) | S1 – workflow blocked | kimi‑code streaming tool calls fail with 400 error (needs reproduction) | No |
| #6269 (OPEN) | S2 – degraded behavior | Context compressor drops `reasoning_content` from assistant messages | No |
| #6739 (OPEN) | S2 – degraded behavior | Cron timezone contract inconsistent across tools, CLI, API | Yes: #6740, #6741 |
| #6734 (OPEN) | S2 – degraded behavior | Qwen 3.6 tool‑call envelopes leak into Matrix replies | Yes: #6736 |
| #6733 (OPEN) | S2 – degraded behavior | Matrix streaming draft state keyed only by room, causing overlap | Yes: #6735 |
| #6721 (OPEN) | S2 – degraded behavior | `tool_search` not in default auto‑approve → webhook hangs 120s then auto‑denies | No |
| #6724 (OPEN) | S2 – degraded behavior | Channels supervisor crashloops when all channels have `enabled=false` | No |
| #6723 (OPEN) | S2 – degraded behavior | Native OpenAI provider hardcodes 120s timeout, ignores `timeout_secs` config | No |

**Note:** Fix PRs for the most recent bugs were opened quickly by the core team (drbparadise, nick‑pape, etc.), indicating strong bug‑fix velocity.

### 6. Feature Requests & Roadmap Signals
Today saw several enhancement requests and notable feature PRs. The most significant roadmap signals are:

- **Multi‑Agent Runtime (v0.8.0)** — PR #6398 (OPEN, XL size) is the largest ongoing effort, covering schema V3, multi‑agent orchestration, and many channel/tool/provider updates.  
  [zeroclaw-labs/zeroclaw Pull Request #6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)

- **Skills improvements** — Issue #6253 (tracker for v0.7.6 skills UX) and PR #6667 (*background review fork + skill_manage tool*) show strong focus on skill authoring and self‑improvement features.  
  [zeroclaw-labs/zeroclaw Issue #6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)  
  [zeroclaw-labs/zeroclaw Pull Request #6667](https://github.com/zeroclaw-labs/zeroclaw/pull/6667)

- **OAuth & Provider Expansion** — Issue #5601 (OAuth for Ollama Cloud, Zhipu, Kimi, MiniMax) and PR #6268 (Manifest LLM router integration) align with ZeroClaw’s goal of supporting more subscription‑based providers.  
  [zeroclaw-labs/zeroclaw Pull Request #6268](https://github.com/zeroclaw-labs/zeroclaw/pull/6268)

- **Documentation** — Issue #5994 (official documentation website) and PR #6639 (Homebrew config fix) indicate the community wants better onboarding.  
  [zeroclaw-labs/zeroclaw Issue #5994](https://github.com/zeroclaw-labs/zeroclaw/issues/5994)

- **Cron/Channel enhancements** — Issues #5604 (Mattermost private messages), #5573 (SMTP email channel), and PRs #6666 (separate IMAP/SMTP credentials), #6730 (cron suppression), #6731 (Slack unfurl config) show demand for richer channel integrations.

**Prediction:** The next minor release (likely v0.7.6) will focus on skills UX (tracked in #6253). The v0.8.0 beta will follow with multi‑agent runtime, likely incorporating many of the open feature requests as they mature.

### 7. User Feedback Summary
Real user pain points emerged from the data:

- **Onboarding friction** — Fresh installations lack a working `default_model`, blocking first use (#6123). Users also struggle with distributed configuration docs (#5994).
- **Provider issues** — Streaming errors with kimi‑code (#5600), missing OAuth support (#5601), and multimodal image path handling (#6399) frustrate users who rely on diverse backends.
- **Channel limitations** — Mattermost users cannot send private messages to bots (#5604); email as a channel is missing (#5573); Matrix streaming state is broken (#6733), and Slack unfurl control is absent (#6731).
- **Missing tool/security features** — Users want PDF ingestion (#5745), per‑skill security permissions (#5775), and agent capability flags (#6729). The lack of an LSP integration (#5907) limits coding‑agent use cases.
- **Positive signals** — The community is proactively filing well‑structured feature requests and bug reports. Maintainers respond quickly with fix PRs (e.g., #6735, #6736, #6740, #6741). The `v0.8.0` PR (#6398) has explicit “SEEKING APPROVAL” with encouragement for screenshots and feedback, showing open development.

### 8. Backlog Watch
Several important issues remain open, marked as blocked or needing maintainer review, many for weeks:

| Issue | Created | Status | Summary |
|-------|---------|--------|---------|
| #2467 | 2026-03-02 | blocked | Webhook transforms for custom payloads |
| #5601 | 2026-04-10 | blocked | OAuth support for four providers |
| #5607 | 2026-04-10 | blocked, needs‑maintainer‑review | Pre‑hook skip gates for cron/SOP |
| #5745 | 2026-04-15 | blocked, needs‑maintainer‑review | PDF support in tools |
| #5775 | 2026-04-15 | blocked, needs‑maintainer‑review | Per‑skill security permissions |
| #5842 | 2026-04-17 | blocked, needs‑maintainer‑review | `extra_args` validation for Codex CLI security |
| #5843 | 2026-04-17 | blocked, needs‑maintainer‑review | Model‑wise reasoning configuration |
| #5882 | 2026-04-18 | blocked, needs‑maintainer‑review | Ratatui‑based agent mode REPL |
| #5907 | 2026-04-19 | blocked, needs‑maintainer‑review | LSP support |
| #5908 | 2026-04-19 | blocked, needs‑maintainer‑review | CI/CD container builds for Debian image |

These issues represent significant community investment and, if left unaddressed, risk discouraging contributors. Maintainer prioritization of the v0.8.0 milestone may explain the delays, but a roadmap communication would help manage expectations.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*