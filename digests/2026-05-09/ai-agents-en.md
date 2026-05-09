# OpenClaw Ecosystem Digest 2026-05-09

> Issues: 464 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-09 07:22 UTC

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

# OpenClaw Project Digest — 2026-05-09

## Today’s Overview
OpenClaw remains in a period of extremely high activity, with **464 issues** and **500 pull requests** updated in the last 24 hours. Of these, **191 issues were closed** and **142 PRs were merged/closed**, indicating an aggressive pace of bug fixing and feature integration. No new releases were published today, but the community is actively testing the latest `2026.5.x` versions, reporting regressions as well as providing patches. The project’s health is strong, with rapid triage and many contributors stepping in to address stability concerns, especially around channel integrations (WeChat, Discord, Telegram, Feishu) and model provider compatibility.

## Releases
No new releases were made today. The most recent stable version remains `2026.5.7` (as implied by recent issue references). Users are advised to monitor the [releases page](https://github.com/openclaw/openclaw/releases) for upcoming changes.

## Project Progress
Today’s merged/closed PRs (142 total) include several important fixes and features:

- **CLI & tool confusion** – PR [#77221](https://github.com/openclaw/openclaw/pull/77221) (closed) improves error messages when users invoke agent tool names at the CLI, preventing misleading `plugins.allow` suggestions. Replaced by [#79693](https://github.com/openclaw/openclaw/pull/79693) (closed) with refined wording.
- **ACP thread binding** – PR [#50955](https://github.com/openclaw/openclaw/pull/50955) (closed) unifies thread-bound session creation and delivery routing for the Agent Communication Protocol, fixing inconsistencies between `sessions_spawn` and `/acp spawn`.
- **Gateway watch mode** – PR [#70805](https://github.com/openclaw/openclaw/pull/70805) (open) fixes a race condition where `pnpm gateway:watch` could start with missing plugin artifacts, causing Telegram startup failures.
- **Cron recovery** – PR [#75036](https://github.com/openclaw/openclaw/pull/75036) (open) adds durable cron recovery for tasks lost due to false-positive “backing session missing” errors.
- **Embedding query prefix** – PR [#79702](https://github.com/openclaw/openclaw/pull/79702) (open) adds instruction-aware prefixing for OpenAI-compatible embedding providers (Qwen3, Nomic, mxbai), improving retrieval quality.
- **Security: redaction centralization** – PR [#79645](https://github.com/openclaw/openclaw/pull/79645) (open) moves credential redaction into `appendSessionTranscriptMessage` to prevent leaks.
- **Runtime state refactor** – PR [#78595](https://github.com/openclaw/openclaw/pull/78595) (open) is a massive, ongoing effort to move OpenClaw’s state from scattered JSON/JSONL files to a unified SQLite model (refs [#78096](https://github.com/openclaw/openclaw/issues/78096)).
- **Channel ingress refactor** – PR [#79092](https://github.com/openclaw/openclaw/pull/79092) (open) centralizes message channel authorization behind an experimental SDK API, with 22 channel labels affected.
- **Many smaller fixes** for Telegram outbound delivery timing, diagnostics OTEL event population, stream read error classification, and cron job malformed row handling.

## Community Hot Topics
The most active discussions (by comment count and reactions) reveal these core concerns:

- **Docker skill install failure** – Issue [#14593](https://github.com/openclaw/openclaw/issues/14593) (29 comments, 17 👍) – `brew not installed` error when using brew-based skills inside the official Docker container. Users need a pre-installed `brew` or fallback mechanism.
- **Sudden filesystem tool loss** – Issue [#34810](https://github.com/openclaw/openclaw/issues/34810) (29 comments, 9 👍, **closed**) – Agent lost ability to create files/run commands around 4 AM ET, later resolved. Root cause still under discussion but fix appears to have been rolled out.
- **Text between tool calls leaks to channel** – Issue [#25592](https://github.com/openclaw/openclaw/issues/25592) (26 comments, 0 👍) – Internal processing narration leaks to Slack/iMessage, a major UX problem. Community is asking for a routing fix.
- **Doctor migration breaks Codex OAuth** – Issue [#78407](https://github.com/openclaw/openclaw/issues/78407) (19 comments, 3 👍, **closed**) – `openclaw doctor --fix` rewrites `openai-codex/*` model refs to `openai/*`, locking out ChatGPT OAuth users. A serious regression in `2026.5.4→2026.5.5` update.
- **Memory flush reliability** – Issue [#12590](https://github.com/openclaw/openclaw/issues/12590) (19 comments, 0 👍, **closed**) – `memoryFlush` fires only on every other compaction cycle due to dedup logic bug.
- **Tiered bootstrap loading** – Issue [#22438](https://github.com/openclaw/openclaw/issues/22438) (16 comments) – Feature request to reduce token waste by loading bootstrap files only when needed, especially for sub-agents and cron.

## Bugs & Stability
Bugs reported today are ranked by severity:

### Critical / Beta Release Blockers
- **Gateway “ready” fires before acpx plugin finishes** – [#79596](https://github.com/openclaw/openclaw/issues/79596) (5 comments, 1 👍) – Marked **Beta release blocker**. Plugin registers 58s after ready signal, causing clients to connect prematurely.
- **Codex embedded agent path still throws “Failed to extract accountId”** – [#79662](https://github.com/openclaw/openclaw/issues/79662) (4 comments, 1 👍, **closed**) – Fix in `2026.5.7` only covered OAuth refresh path; embedded agent path remains broken. A follow-up is needed.

### High Severity (Regressions in latest versions)
- **Cloudflare AI Gateway broken in 2026.5.6** – [#78962](https://github.com/openclaw/openclaw/issues/78962) (4 comments, 2 👍, **closed**) – Full chat failure after upgrade. Likely a provider compatibility issue.
- **Google Gemini models hang/timeout on main sessions** – [#78502](https://github.com/openclaw/openclaw/issues/78502) (6 comments, 2 👍, **closed**) – Affects `2026.5.5`; works fine via direct API. Regression from `2026.5.3-1`.
- **Gateway event-loop starvation due to stuck tool call** – [#78402](https://github.com/openclaw/openclaw/issues/78402) (11 comments, 2 👍, **closed**) – Websocket disconnects (1000/1005/1006) after upgrading to `2026.5.5`. Fixed in later patch.
- **WeChat plugin fails to start (runtime undefined)** – [#77779](https://github.com/openclaw/openclaw/issues/77779) (7 comments, 1 👍, **closed**) – Regression in `2026.5.4` for `@tencent-weixin/openclaw-weixin`.
- **Discord Unknown Channel error on message send** – [#78572](https://github.com/openclaw/openclaw/issues/78572) (6 comments, 2 👍, **closed**) – Regression in `2026.5.4` for Discord outbound.
- **Feishu group chat replies=0 despite dispatch success** – [#77869](https://github.com/openclaw/openclaw/issues/77869) (8 comments, 2 👍) – Still open; bot shows typing indicator but no response sent.
- **Command replies silently dropped in group chats** – [#77260](https://github.com/openclaw/openclaw/issues/77260) (7 comments, 3 👍, **closed**) – When `visibleReplies: “message_tool”`, slash commands are lost.

### Moderate Severity
- **Session context confusion (replies to wrong message)** – [#32296](https://github.com/openclaw/openclaw/issues/32296) (12 comments, 1 👍) – Ongoing issue, not yet closed.
- **Signal daemon race condition on restart** – [#22676](https://github.com/openclaw/openclaw/issues/22676) (16 comments) – Orphaned processes due to missing wait on SIGTERM.
- **Stuck sessions never aborted** – [#71127](https://github.com/openclaw/openclaw/issues/71127) (8 comments) – Diagnostic detects stuck sessions but no recovery action is taken; requires external restart.

### Fix PRs in Progress
- [#79692](https://github.com/openclaw/openclaw/pull/79692) – Classifies `stream_read_error` as transient, enabling model fallback.
- [#79687](https://github.com/openclaw/openclaw/pull/79687) – Emits reasoning stream events to gateway clients without channel callback (thinking not surfaced live).
- [#79695](https://github.com/openclaw/openclaw/pull/79695) – Tracks active reply runs in diagnostics to avoid deadlock.
- [#79704](https://github.com/openclaw/openclaw/pull/79704) – Annotates message‑tool‑only replies in Codex tool spec to fix silent drops.

## Feature Requests & Roadmap Signals
Several feature requests have gathered community support and are likely to be included in the next minor release:

- **Tiered bootstrap file loading** ([#22438](https://github.com/openclaw/openclaw/issues/22438)) – High interest (16 comments). Token savings are significant; an implementation appears in earlier PR discussion.
- **Post-subagent completion extension hook** ([#22358](https://github.com/openclaw/openclaw/issues/22358)) – Would enable structured trajectory logging. Useful for debugging and compliance.
- **Direct Exec Mode for cron jobs** ([#18160](https://github.com/openclaw/openclaw/issues/18160)) – 9 👍, avoids LLM overhead for simple commands. A practical performance improvement.
- **Telegram Business Bot support** ([#20786](https://github.com/openclaw/openclaw/issues/20786)) – 3 👍, requested for enterprise use cases.
- **Allow bots in Telegram groups** ([#8295](https://github.com/openclaw/openclaw/issues/8295)) – 4 👍, parity with Discord/Slack.
- **Native web_search passthrough for ZAI and Google** ([#17925](https://github.com/openclaw/openclaw/issues/17925)) – 5 👍, building on existing Grok support.
- **Message delete action for WhatsApp** ([#14344](https://github.com/openclaw/openclaw/issues/14344)) – 1 👍, needed for agent error correction.
- **Reaction-triggered agent turns** ([#17840](https://github.com/openclaw/openclaw/issues/17840)) – Interactive polling/labeling use cases.

**Likely to land next** (based on PR activity): the runtime SQLite refactor ([#78595](https://github.com/openclaw/openclaw/pull/78595)) and channel ingress centralization ([#79092](https://github.com/openclaw/openclaw/pull/79092)) are massive PRs that will underpin many future improvements.

## User Feedback Summary
Real user pain points expressed in today’s issues include:

- 🐛 **Docker environment missing brew** – Users cannot install skills in containers without manual workarounds. A clear demand for consistent Linux container support.
- 🔁 **Frequent regressions after minor version bumps** – Many users report features breaking on `2026.5.4`, `2026.5.5`, `2026.5.6`. Examples: WeChat plugin crash, Cloudflare Gateway broken, Gemini models timing out, Feishu silent replies. Satisfaction is low for those who upgraded rapidly.
- 💬 **Leaked internal text to messaging channels** – A major UX annoyance; users expect clean separation between internal processing and user-facing messages.
- 📝 **Onboarding lacks memory setup** – Users discover embedding provider configuration only after setup, causing frustration.
- 📱 **Voice messages not working on Matrix** – Agent receives audio but doesn’t process it.
- 📄 **Missing plain text copy option** – Minor but frequently requested.
- 🔐 **OAuth issues with Codex/OpenAI** – Repeated token extraction failures and model reference rewrites cause lockouts.

Overall, power users appreciate the rapid iteration but are frustrated by the frequency of breaking changes. The community is highly engaged, reporting bugs quickly and even submitting PRs for fixes.

## Backlog Watch
The following issues and PRs have remained open for an extended period and warrant maintainer attention:

| Item | Age | Comments | Status |
|------|-----|----------|--------|
| [#14593](https://github.com/openclaw/openclaw/issues/14593) Docker skill install: `brew not installed` | ~3 months | 29 comments, 17 👍 | Open, no fix in sight |
| [#25592](https://github.com/openclaw/openclaw/issues/25592) Text leaks between tool calls | ~2.5 months | 26 comments | Open, no assignee |
| [#22438](https://github.com/openclaw/openclaw/issues/22438) Tiered bootstrap file loading | ~2.5 months | 16 comments | Open, feature request |
| [#22676](https://github.com/openclaw/openclaw/issues/22676) Signal daemon restart race | ~2.5 months | 16 comments | Open, needs design |
| [#16670](https://github.com/openclaw/openclaw/issues/16670) Onboarding missing memory setup | ~3 months | 8 comments, 1 👍 | Open, UX improvement |
| [#20786](https://github.com/openclaw/openclaw/issues/20786) Telegram Business Bot | ~2.5 months | 7 comments, 3 👍 | Open, feature request |
| [#70805](https://github.com/openclaw/openclaw/pull/70805) Gateway watch mode fix | ~2 weeks | 0 comments | Open, awaiting review |
| [#78595](https://github.com/openclaw/openclaw/pull/78595) SQLite runtime refactor | 3 days | 0 comments (massive PR) | Open, needs careful review |

The Docker brew issue and text leakage problem are among the most upvoted and oldest open issues, yet no fix has been committed. These should be prioritized to improve user trust and reduce regressions.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent Open-Source Ecosystem
**Date:** 2026-05-09

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape remains intensely competitive, with a clear bifurcation between foundational reference implementations (OpenClaw) and specialized forks targeting specific deployment environments (mobile, enterprise, embedded). The ecosystem is experiencing a **stability crisis**: multiple projects report regressions after minor version bumps, and cross-project patterns show that provider compatibility (OpenAI Codex OAuth, DeepSeek, Gemini) and channel integration reliability (WeChat, Feishu, Telegram) are the dominant pain points. A converging theme is the demand for **Web UI management interfaces**, with NanoBot, CoPaw, and LobsterAI all actively shipping browser-based dashboards. The overall health is strong but strained — high contributor throughput is offset by growing backlog of long-standing bugs in every major project.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 464 | 500 | None | **High** — rapid triage, aggressive merge pace, but regressions accumulating |
| **Hermes Agent** | 50 | 50 | None | **High** — heavy security hardening, but P1 bugs open >1 month |
| **ZeroClaw** | 50 | 50 | None | **High** — high velocity, but build failures blocking adoption |
| **NanoBot** | 18 | 143 | None | **High** — strong contributor diversity, Web UI momentum |
| **CoPaw** | 36 | 42 | v1.1.6-beta.1 | **High** — fast release cycle, regression pain in .post2 |
| **PicoClaw** | 21 | 23 | Nightly v0.2.8 | **Moderate** — steady, exec tool bug blocking workflows |
| **IronClaw** | 12 | 45 | None (v0.28.0 yesterday) | **High** — Reborn engine progress, production bug today |
| **NanoClaw** | 5 | 17 | None | **Moderate** — critical data-loss bug (setup script) |
| **LobsterAI** | 2 | 18 | None | **Moderate** — focused maintenance, UI polish |
| **NullClaw** | 2 | 1 | Nightly prerelease | **Low** — two bugs, minimal engagement |
| **Moltis** | 0 | 5 | None (yesterday) | **Low** — stable, but no community activity |
| **ZeptoClaw** | 0 | 1 | None | **Low** — near-dormant |
| **TinyClaw** | 0 | 0 | None | **Inactive** |

**Note:** Health Score combines issue resolution rate, PR merge velocity, release cadence, and severity of open bugs. OpenClaw and Hermes have the highest raw activity but also the most critical open defects.

---

## 3. OpenClaw's Position

**Advantages vs Peers:**
- **Scale dominance:** OpenClaw's 464 issues and 500 PRs in 24 hours eclipses all others by a factor of 3–10x. It is the de facto reference implementation, with the largest contributor base.
- **Triage speed:** 191 issues closed and 142 PRs merged/closed in a single day — unmatched responsiveness.
- **Channel breadth:** Native support for WeChat, Discord, Telegram, Feishu, and more. Competitors (e.g., ZeroClaw, PicoClaw) have fewer channels or weaker implementations.
- **Runtime refactoring leadership:** The SQLite state migration (PR #78595) positions OpenClaw for long-term architectural stability that smaller projects cannot resource.

**Technical Approach Differences:**
- **Monolithic core with plugin architecture** — unlike NanoBot's modular agent loop or IronClaw's Rust+WebAssembly stack, OpenClaw uses a TypeScript monorepo with plugin-based channel integrations.
- **Heavy emphasis on ACP (Agent Communication Protocol)** — OpenClaw is driving protocol standardization that Hermes, Moltis, and others are adopting.
- **Gateway-centric deployment** — OpenClaw's `gateway` process is a distinct architectural layer, while PicoClaw and NanoClaw embed similar functionality more tightly.

**Community Size Comparison:**
- OpenClaw's community dwarfs peers: 464 issues/day vs. Hermes (50), ZeroClaw (50), NanoBot (18). Its PR volume (500) is 10x IronClaw (45) and 3.5x NanoBot (143).
- However, this scale carries risk: **regression density is higher**. Four `2026.5.x` releases in May alone caused breakage for WeChat, Discord, Feishu, Cloudflare, and Gemini users. Smaller projects like Moltis (no regressions reported) trade velocity for stability.

---

## 4. Shared Technical Focus Areas

The following requirements appear across ≥3 projects, indicating ecosystem-wide priorities:

| Focus Area | Affected Projects | Specific Needs |
|---|---|---|
| **Docker/Container Environment Gaps** | OpenClaw, NanoClaw, CoPaw, ZeroClaw | Missing `brew` in containers (OpenClaw #14593), setup script data loss (NanoClaw #2360), secrets restore failures (CoPaw #3827), Windows build failures (ZeroClaw #6280) |
| **Channel Message Routing & Leaks** | OpenClaw, Hermes, CoPaw, ZeroClaw | Internal processing text leaks to Slack/iMessage (OpenClaw #25592), WhatsApp wrong-target routing (Hermes #18646, PicoClaw #2540), Feishu silent replies (OpenClaw #77869), cron wrong-channel dispatch (CoPaw) |
| **Provider Compatibility Regressions** | OpenClaw, Hermes, PicoClaw, CoPaw, ZeroClaw | OpenAI Codex OAuth breakage (OpenClaw #78407, PicoClaw #2674), Gemini 429/timeout (Hermes #15895, OpenClaw #78502), DeepSeek/NVIDIA empty tool_calls (ZeroClaw #6298), OpenCode regression (CoPaw #4133) |
| **Context & Session Management** | OpenClaw, NanoBot, Hermes, CoPaw, ZeroClaw | Memory flush reliability (OpenClaw #12590), session search hangs (Hermes #7725), context overflow hallucination (ZeroClaw #6517), multi-turn UI lag (CoPaw #3350) |
| **Web UI / Management Interface** | NanoBot, CoPaw, LobsterAI, Moltis | Built-in Web UI demand (NanoBot #2949, #1922), skeleton loading states (LobsterAI #1920), chat composer redesign (Moltis #985) |
| **Multi-Agent / Subagent Workflows** | OpenClaw, NanoBot, Hermes, PicoClaw, ZeroClaw | Subagent profiles (NanoBot #1012), async result delivery (PicoClaw #2829), multi-agent runtime (ZeroClaw #6272), post-subagent hooks (OpenClaw #22358) |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | PicoClaw | IronClaw | ZeroClaw |
|---|---|---|---|---|---|---|
| **Primary Language** | TypeScript | Rust (core) | Python | Rust | Rust+WebAssembly | Rust |
| **Target User** | Full-stack dev, community host | CLI-first agent user | Power user, security-conscious | Mobile/Android, embedded | Enterprise, multi-tenant | Rust ecosystem dev, Matrix user |
| **Deployment Model** | Gateway+plugins | Standalone binary + WebSocket | Daemon + channels | Android Termux + CLI | Container/Kubernetes | CLI + desktop (planned) |
| **Unique Strength** | Channel breadth (WeChat, Feishu) | Web UI momentum, contributor diversity | Security hardening, Chinese localization | Android native, LM Studio focus | Reborn engine, scalable sessions | Rust performance, Matrix native |
| **Unique Weakness** | Regression frequency | Session persistence issues | P1 bugs open >1 month | exec tool false positive blocking workflows | Production routing bug | Windows build failures |
| **Architecture Philosophy** | Monorepo, protocol-driven | Modular agent loop | Hardened provider stack | Mobile-first simplification | Next-gen engine rewrite | Rust ecosystem compatibility |
| **Community Maturity** | Most mature, largest | Growing, ~19 active contributors | Mature, security-focused | Niche (mobile/embedded) | Professional, NEAR AI-backed | Early, high contributors |

**Key Architectural Splits:**
- **State Management:** OpenClaw is migrating from JSON/JSONL to SQLite (PR #78595). IronClaw uses PostgreSQL/libSQL. ZeroClaw uses sled/embedded databases. Hermes uses filesystem-based session files.
- **Provider Abstraction:** OpenClaw has the deepest provider matrix. Hermes has the most robust security (SSRF protection, credential encryption, webhook validation). ZeroClaw has the most granular provider configuration (per-channel, per-alias).
- **Channel Approach:** OpenClaw centralizes via ingress refactor (PR #79092). Hermes uses per-channel plugins. NanoBot uses a WebSocket channel + adapter pattern.

---

## 6. Community Momentum & Maturity

**Tier 1 — Hyper-Active (rapid iteration, risk of regression):**
- **OpenClaw** — Unmatched volume, but regression density is a concern. 4 releases in May caused multiple breakages. The community accepts this trade-off for rapid feature velocity.
- **Hermes Agent** — Security and gateway hardening dominate. Contributor diversity is lower (mostly core team), but PR quality is high.
- **ZeroClaw** — Extremely active (50 PRs/day), but 50 open issues in one day signals a backlog problem. Build failures on Windows and matrix-sdk are blocking new users.

**Tier 2 — High Velocity (stable core, feature expansion):**
- **NanoBot** — 143 PRs/day with 19 unique authors shows healthy contributor growth. Web UI is the dominant theme. Session persistence is the weakest link.
- **CoPaw** — 32 PRs merged/day with v1.1.6-beta.1 release. Strong localization (Portuguese) and MCP integration. Provider regressions in .post2 need attention.
- **PicoClaw** — Steady, mobile-focused. The `exec` tool false positive bug (#1042) is a critical quality gate for Linux/Android users.

**Tier 3 — Stabilizing / Maintenance:**
- **IronClaw** — Heavy Reborn engine development with 45 PRs/day. Two production bugs (E2E failure, mission routing) and long-standing PRs (52-day-old per-channel tool filtering) suggest maintainer bandwidth is stretched.
- **NanoClaw** — Critical data-loss bug (#2360) overshadows otherwise solid progress. The admin CLI (`ncl`) is a positive differentiation.

**Tier 4 — Low Activity / Niche:**
- **LobsterAI** — Healthy merge rate (16/18 PRs) but minimal community engagement. Focused on UI polish.
- **NullClaw** — Minimal activity, two significant bugs (supervised mode broken, config inconsistency). Risk of stagnation.
- **Moltis** — Low churn but incremental progress (persistent sessions PR). No community engagement signals.
- **ZeptoClaw** — Near-dormant. Single PR (tool descriptions) with no reviews.
- **TinyClaw** — Inactive.

---

## 7. Trend Signals

The following industry trends are validated by cross-project community feedback and should inform AI agent developer strategy:

1. **Observability is an afterthought — and becoming a bottleneck.** Langfuse traces missing LLM I/O (Hermes #22342), OTEL events incomplete (OpenClaw), and SSE event drops (ZeroClaw #6526) indicate that debugging agent behavior is harder than it should be. Developers building on these frameworks should budget for custom observability instrumentation.

2. **Security hardening is moving from optional to table-stakes.** Hermes is shipping SSRF protection, webhook client_state requirements, and credential encryption. OpenClaw is centralizing redaction. ZeroClaw is adding trust-CA support. The ecosystem is reacting to real-world attack surface from multi-channel, multi-provider deployments.

3. **Provider diversity is a UX problem, not just a config problem.** The number of provider-specific bugs (Gemini 429, DeepSeek tool_calls, Codex OAuth, Ollama unrecognized, LM Studio Internal Server Error) across every major project suggests that abstracting providers behind a unified API is far from solved. Developers should expect to write provider-specific workarounds.

4. **The "Web UI gap" is closing.** NanoBot, CoPaw, LobsterAI, and Moltis are all shipping browser-based management interfaces. The CLI-only era is ending. Projects without a Web UI (ZeroClaw, NullClaw) risk losing mainstream adoption.

5. **Context management is the next frontier.** Memory flush bugs, session search hangs, context overflow hallucination, and UI lag at 200+ turns are reported across OpenClaw, Hermes, CoPaw, and ZeroClaw. The SQLite state refactor in OpenClaw and IronClaw's Reborn engine are bets on structured storage. Developers should prioritize session persistence design early — it is the top scalability pain point.

6. **Mobile deployment is underserved but growing.** PicoClaw is the only project with an Android build. Hermes and CoPaw have Docker support but no mobile clients. The LM Studio Easy Connect request (#28, PicoClaw) signals demand for local LLM integration on phones — a gap no mainstream project currently fills.

7. **Multi-agent orchestration is converging on ACP.** OpenClaw's agent communication protocol is being mirrored in Hermes (session lifecycle fixes), Moltis (persistent sessions), and ZeroClaw (session restore). The industry is standardizing around spawn/subagent patterns — but async result handling (PicoClaw #2829) and post-subagent hooks (OpenClaw #22358) are still immature.

---

**Bottom Line for Decision-Makers:**

- **Choose OpenClaw** if you need maximum channel breadth, community support, and are willing to navigate frequent regressions.
- **Choose Hermes or NanoBot** for security-hardened, Python/Rust-native deployments with strong local-First workflows.
- **Choose PicoClaw** for Android/mobile agent use cases.
- **Choose IronClaw or ZeroClaw** for Rust-ecosystem integration, multi-tenant, or Kubernetes deployments — but expect missing features and build friction.
- **Monitor NullClaw, Moltis, and ZeptoClaw** for specific protocol innovations but don't build on them as primary platforms today.
- **Avoid TinyClaw entirely** — no activity signals abandonment.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-09

## 1. Today's Overview
NanoBot maintained a high level of activity with **18 issues updated** (7 open, 11 closed) and **143 PRs updated** (110 open, 33 merged/closed) in the past 24 hours. Community interest continues to center around **Web UI integration** and **quality-of-life improvements** such as a `nanobot update` command and configurable bot names. No new releases were published today, but the pull request pipeline shows steady progress on stability fixes (session persistence, tool-loop guards) and new provider support (NVIDIA NIM). The project remains healthy with strong contributor engagement.

## 2. Releases
*No new releases in the past 24 hours.*  
No version bumps, changelogs, or migration notes to report.

## 3. Project Progress
**33 PRs were merged or closed today**, indicating rapid iteration. Standout merged/closed PRs include:

- **#3705** – Fix CLI spinner corruption on retry messages (`eugenechae`)  
- **#3673** – Fix WebSocket channel silently dropping media attachments (`ivelin`)  
- **#3685 / #3710** – Fix and revert cycle for `_last_summary` persistence across restarts (`chengyongru` / `Re-bin`)  
- **#3680** – Handle corrupted session files where `last_consolidated` exceeds message count (`Lumjiel`)  
- **#3697** – Sanitize surrogate code points from Windows emoji input (`chengyongru`)  
- **#3709** – WebUI: add BYOK web search settings (`Re-bin`)  
- **#3534** – Add CLAUDE.md and `.agent/` guides for AI contributors (`chengyongru`)  
- **#3671** – Fix nightly regression where runtime context leaked into prompt cache (`T3chC0wb0y`)  
- **#3030** – Web App and Mobile APIs channel (`mterhar`)  
- **#1707, #2050, #1650, #2972, #1047** – Multiple Web UI channel contributions (various authors)

**Key advances:**
- Core agent loop refactoring underway (PR #3708 introduces `AgentLoop.from_config()`)
- NVIDIA NIM provider support added (PR #3707)
- Mock CRM MCP server for testing (PR #3706)

## 4. Community Hot Topics
Most active discussions (by comments and reactions):

| Issue | Title | Comments | 👍 | Status |
|-------|-------|----------|---|--------|
| [#2949](https://github.com/HKUDS/nanobot/issues/2949) | Should nanobot have its own WebUI? | 10 | 13 | Closed |
| [#1922](https://github.com/HKUDS/nanobot/issues/1922) | I've created [nanobot-webui], a self-hosted web management panel | 9 | 10 | Closed |
| [#510](https://github.com/HKUDS/nanobot/issues/510) | Gateway not binding to 18790 | 5 | 0 | Closed |
| [#2389](https://github.com/HKUDS/nanobot/issues/2389) | OpenWebUI as an official channel? | 4 | 0 | Closed |
| [#3421](https://github.com/HKUDS/nanobot/issues/3421) | RFC: Should we add a `nanobot update` command? | 4 | 1 | Closed |
| [#3650](https://github.com/HKUDS/nanobot/issues/3650) | Configure bot name and icon | 3 | 0 | Open |

**Analysis:** The overwhelming community theme is **Web UI demand**. Multiple feature requests and community-built panels (nanobot-webui, OpenWebUI integration) show users want a browser-based management interface. The maintainers appear to be converging on an official solution, as evidenced by several Web UI PRs merged today. The `nanobot update` command also garnered interest, reflecting desire for simpler maintenance.

## 5. Bugs & Stability
**Severity: High**  
- **[[#3699]](https://github.com/HKUDS/nanobot/issues/3699) – Repeated identical local tool calls causing infinite loops** (closed, fix not yet merged)  
  *User reports missing guard for local tool call duplicates. PR #3700 proposes turn-level escalation.*  
- **[[#3674]](https://github.com/HKUDS/nanobot/issues/3674) – WebSocket channel silently drops media attachments** (closed, fixed in PR #3673)  
  *Critical for file-sharing workflows; fix merged today.*  
- **[[#3689]](https://github.com/HKUDS/nanobot/issues/3689) – Session history lost after interrupting a loop (Chinese user report)** (open)  
  *User expects conversation memory to persist across interrupts; no fix PR yet.*  
- **[[#3637]](https://github.com/HKUDS/nanobot/issues/3637) – Transcription provider config not transparent (Groq)** (open)  
  *Misleading configuration leads to invalid setups; requires documentation improvement.*  
- **[[#3694]](https://github.com/HKUDS/nanobot/issues/3694) – Feishu group topic: files sent to wrong channel** (closed)  
  *Multi-file handling bug in Feishu channel.*  
- **[[#3652]](https://github.com/HKUDS/nanobot/issues/3652) – Request to disable Dream feature** (closed, resolved)  
  *User required an `enabled` flag; likely merged via PR.*

**Regression watch:** PR #3671 fixed a nightly regression where runtime context leaked into persistent prompt cache. No other regressions reported.

## 6. Feature Requests & Roadmap Signals
**High-likelihood for next release:**
- **Built-in Web UI** (#2949, #1922, #3059, multiple PRs) – Maintainers are actively merging Web UI channels; official support likely in next version.
- **`nanobot update` command** (#3421) – Rustic CLI improvement, already discussed and closed; might be implemented soon.
- **Configurable bot name/icon** (#3650) – Open enhancement with 3 comments; low-hanging UX fruit.
- **Subagent profiles with configurable tools** (#1012) – Long-standing request (since Feb); no resolution yet but PR #3708 refactoring might lay groundwork.
- **Feishu topic isolation toggle** (#3692) – User-driven feature for group chat management; open, likely to be addressed.

**Lower probability / longer-term:**
- OpenWebUI as official channel (#2389) – Closed without action; maintainers seem to prefer in-house Web UI.
- Interrupt-session memory persistence (#3689) – Complex; may require design RFC.

## 7. User Feedback Summary
**Pain points:**
- “I can’t easily disable Dream” (#3652) – simple config missing.
- “WebSocket media silently dropped” (#3674) – broken file upload in custom clients.
- “Transcription setup is confusing” (#3637) – poor documentation.
- “Session history lost after interrupt” (#3689) – frustrating for iterative tasks.
- “Feishu file routing is wrong” (#3694) – channel-specific bug.

**Positive signals:**
- High 👍 on Web UI discussions (13 on #2949) indicates strong demand and appreciation.
- User-created nanobot-webui (#1922) shows community investment.
- Multiple contributors submitting PRs (19 unique authors in top 20 PRs alone) reflects a healthy ecosystem.

**Use cases:**
- Personal assistant via telegram/feishu/wechat
- Multi-agent research and coding tasks
- Self-hosted AI chat with custom configuration

## 8. Backlog Watch
**Issues needing maintainer attention (older, no recent responses):**

- **[[#1012]](https://github.com/HKUDS/nanobot/issues/1012) – Add subagent profiles with configurable tools** (created 2026-02-22, updated today but only by user comment)  
  *No maintainer comment. Core feature request for advanced multi-agent setups.*  
- **[[#1412]](https://github.com/HKUDS/nanobot/issues/1412) – Processing from another bot (HomeAssistant)** (created 2026-03-02, last comment user)  
  *Allowing bot-to-bot communication; no maintainer acknowledgement.*  
- **[[#3637]](https://github.com/HKUDS/nanobot/issues/3637) – Transcription provider transparency** (open 2026-05-06, no fix yet)  
  *Documentation bug affecting new users; should be addressed soon.*  
- **[[#3698]](https://github.com/HKUDS/nanobot/issues/3698) – Inject tool events into API server SSE stream** (open 2026-05-08)  
  *Feature request with explicit code suggestion; no response from maintainers yet.*  
- **[[#3692]](https://github.com/HKUDS/nanobot/issues/3692) – Feishu topic isolation toggle** (open 2026-05-08)  
  *Request from Chinese user community; may need localization consideration.*

**PRs with high impact awaiting review:**
- **#3708** – `AgentLoop.from_config()` – core refactoring (1/4 of model preset feature) – very fresh, needs review.
- **#3712** – Corrupted session file fix (alternative to #3680) – merged already? (appears open, but similar to fixed #3680).

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-09

## 1. Today's Overview

Hermes Agent saw extremely high activity on 2026-05-09, with **50 issues** and **50 pull requests** updated in the last 24 hours. No new releases were published. The community is heavily engaged: 47 PRs remain open, while 3 were merged/closed. The issue tracker reflects a balanced mix of **critical bugs** (several P1/P2), **user experience regressions**, and **ambitious feature proposals**. Many of the open PRs address security hardening, gateway reliability, and observability fixes. The project appears to be in an active maintenance and feature‑development cycle, though some long‑standing blocking bugs remain unaddressed.

## 2. Releases

**None** – no new versions were published in the last 24 hours.

## 3. Project Progress

Only one merged/closed PR appeared in the top 20:

- **[#22348]** — *Fix ACP shutdown and resumed‑session lifecycle* (closed, P2)  
  Flushes ACP session memory providers on shutdown and preserves resumed session IDs for the client.  
  **Merge status**: closed (likely merged).

All other PRs are open and represent active work in progress:

- **Gateway & Platform hardening**:  
  - [#21682] fix(gateway): harden Windows PID liveness probes  
  - [#22340] security: harden Yuanbao URL downloads (SSRF)  
  - [#22353] security: require Graph webhook `client_state`  
  - [#22354] fix(gateway): scope quiet‑mode tool schema cache by sender identity  
  - [#22355] fix(skills): hide restricted skills from unauthorized gateway senders  
  - [#22356] fix(cron): do not treat delivery origin as live gateway sender identity  
  - [#22347] fix(feishu): keep CardKit progress in one finalized card  
  - [#22316] fix(feishu): render markdown tables as interactive cards  

- **Provider & CLI fixes**:  
  - [#22358] fix(azure‑foundry): honor explicit `api_mode`  
  - [#22366] fix(cli): surface clear error on Python <3.11  

- **Testing & Refactoring**:  
  - [#22311], [#22312], [#22314] – new unit tests for `get_config_path`, `get_skills_dir`, `get_env_path` (P3)  
  - [#22359] chore(gitignore): ignore CocoIndex code cache  

- **Feature additions**:  
  - [#22341] feat(skills): add session‑level automatic skill preloading  
  - [#22364] feat(api_server): emit `hermes.reasoning.delta` SSE event in streaming  
  - [#22363] feat: surface command context in approval prompts  
  - [#21997] feat(chinese): full Chinese localization (CLI/banner/feishu/setup)  

- **Observability**:  
  - [#22345] fix langfuse observability – LLM input/output and tool outputs (open, P3)

## 4. Community Hot Topics

The most actively discussed issues (by comment count) highlight two main themes: **provider reliability** and **terminal flexibility**.

| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#15895] [Bug] google‑gemini‑cli causing 429 but gquota ok | 8 | 👍 1 | User reports 429 errors despite showing full quotas via `/gquotas`. Suggests OAuth token or header issue. |
| [#1855] [Feature] Multi‑backend terminal — local + N named remotes with persistent shell | 5 | 👍 4 | Long‑standing request to support multiple terminal backends (local, SSH, Docker, etc.) simultaneously. High community interest. |
| [#19566] [Bug] OpenAI‑Codex credential pool can drop newly added credential | 4 | — | Credential lost after credential rotation rewrites `auth.json`. Multi‑process race condition. |
| [#20465] [Bug] Interactive CLI session does not auto‑fallback on Codex 429, but cron jobs do | 4 | 👍 1 | Behavioral inconsistency between interactive and cron sessions. Users expect uniform fallback handling. |
| [#7266] [Bug] DashScope endpoint model validation warning (Chinese user) | 4 | — | Annoying but non‑blocking warning on every model switch for Alibaba Cloud DashScope. |
| [#22328] [Bug] `vision_analyze` cannot read any local files (browser screenshots, cached images) | 2 | — | Tool completely broken for local images; reproduces with multiple file paths. |

The most reacted‑upon issue is **#1855** (4 👍), indicating strong user demand for multi‑backend terminal support. **#15895** (8 comments) shows significant troubleshooting around Gemini OAuth.

## 5. Bugs & Stability

**P1 (Critical)** – Two priority‑1 issues were updated today:

- **[#20465]** ([link](https://github.com/NousResearch/hermes-agent/issues/20465)) — Interactive CLI does not auto‑fallback on Codex 429 (`usage_limit_reached`), while cron jobs with the same chain do. Fix PR: none yet.  
- **[#7725]** ([link](https://github.com/NousResearch/hermes-agent/issues/7725)) — `session_search` can hang for 5+ minutes after upgrade, bypassing timeout/cancellation. No fix PR. Created April 11 – now a month old.

**P2 (High)** – Several new and recurring bugs:

| Issue | Description | Fix PR Exists? |
|-------|-------------|----------------|
| [#19566] | OpenAI‑Codex credential pool drops newly added credential during rotation | No |
| [#18646] | `send_message` ignores WhatsApp group target, routes to home channel | No |
| [#6388] | Telegram MarkdownV2 escaping breaks bullet list display (`-` → `\-`) | No |
| [#19337] | MiniMax OAuth stale `verification_uri` linking to deleted page | No |
| [#20675] | `hermes debug` should check credential_pool OAuth tokens, not just env vars | No |
| [#22313] | DeepSeek Anthropic‑compatible API: HTTP 400 – thinking blocks stripped from history | No |
| [#21352] | Ollama provider not recognized by `auxiliary_client.py` – silently falls back to OpenRouter | No |
| [#21527] | Telegram media path escaping broken – regex patterns passed as file paths | No |
| [#22328] | `vision_analyze` cannot read any local files (vision tool completely broken) | Yes? – [#22345] partially fixes observability but not the core vision bug. |
| [#22342] | Langfuse traces missing LLM input/output and tool output | Yes – [#22345] (open, P3) |
| [#19814] | `custom-tools` plugin causes `KeyError: slice(None, 500, None)` in `_detect_tool_failure` | No |
| [#18060] | 23 production files hardcode `Path.home()/.hermes` instead of `get_hermes_home()` – breaks Docker | No |
| [#20539] | `docker_run_as_host_user` overrides `HOME` via `/etc/passwd` | No |
| [#21341] | NixOS module documents option installs files to wrong paths | No |
| [#19776] | Discord gateway connect timeout too short when slash command sync >30s | No |

Several security fixes are in PRs today: [#22340] (Yuanbao SSRF), [#22353] (Graph webhook client_state), [#22354]/[#22355]/[#22356] (gateway access control). These are mature and ready for review.

## 6. Feature Requests & Roadmap Signals

The following feature requests were updated or created today:

| Issue | Description | Likelihood for Next Version |
|-------|-------------|-----------------------------|
| [#1855] | Multi‑backend terminal (local + N named remotes) | **High** – 4 👍, 5 comments, fundamental for power users |
| [#22352] | Discord channel management tools (create/edit/delete) | **Medium** – new, aligns with existing Discord integration |
| [#22365] | Customize Discord reaction emoji (thinking/done/error) | **Low** – cosmetic, but easy to implement |
| [#13466] | Per‑conversation background sessions for long tasks (Feishu/Telegram) | **Medium** – addresses common UX pain |
| [#18430] | Auto‑rename Discord threads from generated session titles | **Medium** – uses existing title generator |
| [#21997] | Full Chinese localization (CLI, banner, Feishu, setup wizard) | **High** – PR already open with code changes |
| [#22341] | Automatic skill preloading at session start | **High** – PR open, reduces user friction |
| [#22364] | SSE `reasoning.delta` event in `/v1/chat/completions` | **High** – needed for ACP/streaming compatibility |
| [#22363] | Surface command context in approval prompts | **High** – improves safety UX, PR open |

**Predicted next‑version inclusions**: Multi‑back end terminal (part of v0.9?), Chinese localization (already PR), skill preloading (PR ready), reasoning delta SSE (PR ready), command context approval (PR ready), Discord thread auto‑rename.

## 7. User Feedback Summary

**Pain Points (high satisfaction when fixed)**:

- **Gemini OAuth 429 despite quotas** – User *herbalizer404* spent days troubleshooting. Shows poor error messaging or token handling ([#15895]).
- **Vision tool completely broken** – *wangqin102* reports that `vision_analyze` cannot read any local file, including Telegram cache and browser screenshots. Essentially a regression that blocks image analysis workflows ([#22328]).
- **Interactive vs cron fallback inconsistency** – *ddoKx* finds that cron jobs handle Codex 429 correctly but interactive sessions don’t. This erodes trust in the agent’s reliability ([#20465]).
- **Session search hangs** – *qaqcvc* describes waiting 5+ minutes after upgrade; pressing Ctrl+C does not cancel. Critical for daily use ([#7725]).
- **Telegram bullet list rendering** – *ShuaiHui* reports cosmetic but annoying issue where `-` items display as `\-` [[#6388]].

**Satisfaction signals**:

- Active community contributions: many first‑time PR authors (e.g., *wesleysimplicio*, *oferlaor*, *Hinotoi-agent*) submitting fixes and tests.
- High engagement on the multi‑backend terminal feature (4 👍) and on security hardening PRs – suggests a mature and active user base that cares about reliability and security.
- Chinese users actively filing and discussing issues (e.g., [#7266], [#22328], [#22316]), indicating strong international adoption.

**Dissatisfaction**:

- Several P1/P2 bugs have been open for weeks without fix PRs (e.g., [#7725] since April 11, [#20465] since May 5). Users may feel these are being deprioritized.
- The `vision_analyze` blocker (#22328) directly impacts agents that rely on vision input – a core capability.

## 8. Backlog Watch

The following issues and PRs require maintainer attention due to age, importance, or lack of response:

| Issue/PR | Created | Status | Why Watch |
|----------|---------|--------|-----------|
| [#1855] [Feat] Multi‑backend terminal | 2026‑03‑18 | Open, P3, 4 👍 | Oldest active feature request with wide support; no maintainer comment. |
| [#7725] [Bug] `session_search` hangs 5+ minutes | 2026‑04‑11 | Open, P1 | Critical P1 bug with no fix PR after one month. |
| [#10648] [Bug] GitHub Copilot ACP mode fails (deprecated CLI + token limit) | 2026‑04‑16 | Open, P1? (no label) | Blocking users of GitHub Copilot as provider. No assignee. |
| [#6768] [Bug] Banner title ignores skin `agent_name` (regression) | 2026‑04‑09 | Open, P3 | Simple UI bug, easy fix – suggests backlog neglect. |
| [#6388] [Bug] Telegram bullet list rendering | 2026‑04‑09 | Open, P2 | Month‑old medium‑severity platform bug. |
| [#21352] [Bug] Ollama provider not recognized by auxiliary clients | 2026‑05‑07 | Open, P2 | Local‑only Ollama users affected by silent fallback. |
| [#21527] [Bug] Telegram media path escaping broken | 2026‑05‑07 | Open, P1 | Blocks sending media via Telegram. |
| [#22328] [Bug] `vision_analyze` cannot read local files | 2026‑05‑09 (today) | Open, P2 | New but immediately blocking for vision users. |

**Notable**: No maintainer has responded to the P1 issues #7725 or #20465 in this digest period. The community is actively submitting fixes for security and gateway issues, but the backlog of core reliability bugs remains a risk.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-09

## 1. Today's Overview

The project shows high activity with **21 issues** and **23 pull requests** updated in the past 24 hours. Of these, **8 issues remain open/active** and **13 have been closed**, indicating steady triage. Pull requests see **5 merged/closed** and **18 still open**, reflecting ongoing development. A new automated **nightly build v0.2.8-nightly.20260509.8508f806** was published, though marked as potentially unstable. Overall, the project is in a healthy state with active community participation and consistent code contributions across providers, channels, and tooling.

## 2. Releases

- **nightly**: Automated nightly build `v0.2.8-nightly.20260509.8508f806`  
  Full changelog: [compare v0.2.8…main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
  *Note*: This is an automated build and may be unstable. No breaking changes or migration notes are specified in the release announcement.

## 3. Project Progress

**Merged/Closed PRs this cycle (5 total):**
- **#2655** (closed) – Restore verified unified kernel baseline, fixing runtime invariants and tool execution metadata routing.  
- **#2522** (closed) – Add streaming usage support to OpenAI-compatible provider, gating `stream_options.include_usage` for native OpenAI endpoints.  
- **#2128** (closed) – Ensure tool parameters have valid JSON Schema `properties` field, fixing strict API compatibility (e.g., LM Studio).  

**Key open PRs advanced today:**
- **#2826** – Fix relative path resolution in `exec` tool safety guard (addresses issue #2749).  
- **#2830** – Add async result delivery policy for spawned subagents (closes #2829).  
- **#2828** – Transcribe queued voice follow-ups and preserve normal voice-note behavior.  
- **#2823** – Dismiss tool feedback when outbound is skipped.  
- **#2822** – Dismiss child tool feedback after sync subturn completion.  
- **#2752** – Improve model configuration workflows in web UI and backend API.  
- **#2763** – Add Gemini Google Search provider for the `web_search` tool.  
- **#2770** – Add MCP section to configuration web UI.  

These contributions advance **tool safety**, **agent spawning**, **provider support** (Gemini, Bedrock streaming, OpenAI-compat), **MCP client functionality**, and **UI/UX improvements**.

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Summary |
|----------|----------|-----------|---------|
| [#28 – LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28) | 18 | 👍2 | User requests simplified LM Studio integration for Android. Active discussion. |
| [#1042 – exec tool guardCommand false positive](https://github.com/sipeed/picoclaw/issues/1042) | 10 | 👍2 | Critical bug: `restrict_to_workspace` blocks legitimate commands (e.g., `curl`). Fix PR #2826 now open. |
| [#2376 – Option to disable Enter key from sending messages](https://github.com/sipeed/picoclaw/issues/2376) | 5 | 👍1 | Android feature request for separate send button vs newline. Closed. |
| [#2782 – MCP client Streamable HTTP transport](https://github.com/sipeed/picoclaw/issues/2782) | 1 | 0 | Urgent request: current SSE-only client cannot connect to modern MCP servers. Only 1 day old but high impact. |

The **LM Studio request** (#28) reveals strong user demand for easy local LLM integration, while **exec tool guardCommand** (#1042) highlights a safety feature causing real workflow disruptions. **MCP Streamable HTTP** (#2782) signals growing ecosystem pressure for modern MCP protocol support.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix PR |
|----------|-------|-------------|--------|
| **High** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `exec` tool `guardCommand` falsely blocks valid commands (e.g., `curl`) due to naive path matching. | [#2826](https://github.com/sipeed/picoclaw/pull/2826) (open) |
| **Medium** | [#2674](https://github.com/sipeed/picoclaw/issues/2674) | Codex OAuth provider returns empty assistant responses when ChatGPT backend streams via `response.output_item.done`. | Unassigned |
| **Medium** | [#2744](https://github.com/sipeed/picoclaw/issues/2744) | Android v0.2.8 – cannot access any data from tabs. | Unassigned |
| **Low** | [#2785](https://github.com/sipeed/picoclaw/issues/2785) | Feishu channel only shows first tool call message in notification center when `separate_messages: false`. | Unassigned |
| **Low** | [#2829](https://github.com/sipeed/picoclaw/issues/2829) | Proposal: async result delivery policy – spawned subagent results re-injected into parent causing duplicate turns. | [#2830](https://github.com/sipeed/picoclaw/pull/2830) (open) |

**Previously closed fixes today:**  
- [#2738](https://github.com/sipeed/picoclaw/issues/2738) – Image recognition broken in v0.2.8 (closed).  
- [#2602](https://github.com/sipeed/picoclaw/issues/2602) – OAuth authentication errors (closed).  
- [#2540](https://github.com/sipeed/picoclaw/issues/2540) – WhatsApp `allow_from` drops LID-migrated accounts (closed).  
- [#2541](https://github.com/sipeed/picoclaw/issues/2541) – WhatsApp `group_trigger.mention_only` non-functional (closed).  

The **exec tool false positive** remains the most impactful open bug; **Codex OAuth** and **Android tabs** lack confirmed fixes. Several WhatsApp bugs have been resolved, improving stability for that channel.

## 6. Feature Requests & Roadmap Signals

| Request | Domain | Predicted Next-Version Inclusion |
|---------|--------|----------------------------------|
| [#2782](https://github.com/sipeed/picoclaw/issues/2782) – MCP Streamable HTTP transport | Provider | **High** – essential for MCP ecosystem compatibility; growing demand. |
| [#2763](https://github.com/sipeed/picoclaw/pull/2763) – Gemini web search provider | Provider | **High** – PR already open and reviewed; may land in next minor release. |
| [#2626](https://github.com/sipeed/picoclaw/pull/2626) – Native audio input for multimodal LLMs | Agent | **Medium** – PR active since April; could appear in v0.2.9. |
| [#2158](https://github.com/sipeed/picoclaw/pull/2158) – Multi-agent discovery prompt | Agent | **Medium** – foundational feature; needs more review. |
| [#28](https://github.com/sipeed/picoclaw/issues/28) – LM Studio Easy Connect | Provider | **Low-Medium** – popular but no concrete implementation started. |
| [#2649](https://github.com/sipeed/picoclaw/issues/2649) – Serial port (UART) tool | Tool | **Low** – niche use case; no PR yet. |
| [#2515](https://github.com/sipeed/picoclaw/issues/2515) – Robust memory system (mem0, Supermemory, HydraDB) | Agent | **Low** – broad scope; likely far from release. |

The **MCP transport** and **Gemini search** features are closest to inclusion. Multi-agent discovery and audio input are further along than LM Studio or memory system integrations.

## 7. User Feedback Summary

**Pain points expressed:**
- **Exec tool safety guard** (#1042) breaks legitimate commands, forcing users to disable `restrict_to_workspace` or face hundreds of false error logs.  
- **LM Studio integration** (#28) is desired by Android users but outside their technical capability.  
- **WhatsApp LID migration** caused silent message drops (#2540) – now fixed.  
- **OAuth errors** (#2602) – resolved.  
- **Android v0.2.8** (#2744) – data tabs inaccessible, unclear root cause.  

**Use cases highlighted:**
- **Android Termux** users rely on PicoClaw on phones and Raspberry Pi.  
- **Embedded developers** want serial/UART tool ( #2649 ).  
- **Multi-agent workflows** (spawn/subagent) need better async result handling ( #2829 ).  
- **Chinese users** request Feishu channel optimizations ( #2580 ).  

**Satisfaction indicators:**  
Closed bug reports (WhatsApp, OAuth, image recognition) demonstrate responsive maintainers. Presence of multiple open feature PRs suggests active development aligns with community needs.

## 8. Backlog Watch

| Item | Created | Last Update | Comments | Issue |
|------|---------|-------------|----------|-------|
| **#28** – LM Studio Easy Connect | 2026-02-11 | 2026-05-08 | 18 comments, still open | [Link](https://github.com/sipeed/picoclaw/issues/28) |
| **#1042** – exec tool false positive | 2026-03-04 | 2026-05-08 | 10 comments, fix PR #2826 open | [Link](https://github.com/sipeed/picoclaw/issues/1042) |
| **#2515** – Robust memory system | 2026-04-14 | 2026-05-08 | 3 comments, no maintainer response | [Link](https://github.com/sipeed/picoclaw/issues/2515) |
| **#2158** – Multi-agent discovery prompt PR | 2026-03-29 | 2026-05-09 | No maintainer review yet | [Link](https://github.com/sipeed/picoclaw/pull/2158) |
| **#2645** – Bedrock streaming provider PR | 2026-04-23 | 2026-05-08 | Stale with no recent review | [Link](https://github.com/sipeed/picoclaw/pull/2645) |

**Notable:**  
- **#28** and **#1042** are high-visibility community issues requiring maintainer attention (decision or progress).  
- **#2158** (PR) has been open over a month without maintainer review – risk of stagnation.  
- **#2515** (memory system) lacks any maintainer acknowledgment, despite being a significant feature request.  

Active triage is recommended for these items to maintain community trust and momentum.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-09

## Today’s Overview

NanoClaw had a high‑activity day with 17 pull requests touched and 5 issues updated in the last 24 hours. Five PRs were merged or closed, including critical graceful‑shutdown fixes and a new admin CLI. One stability bug (readonly‑database crash) was resolved. No new releases were published; the project appears focused on hardening production paths and expanding container‑runtime capabilities. Community feedback highlights data‑loss concerns in the setup script and missing CLI‑symlink on upgrade, both of which have incoming fixes.

## Releases

No new releases today. The latest tagged version remains **2.0.45** (introduced `/update-nanoclaw` and the CLI socket). A minor or patch release incorporating the shutdown fixes, the `ncl` CLI, and the intake overhaul is likely in the next few days.

## Project Progress

Five pull requests were merged or closed today, advancing both stability and features:

- **Shutdown reliability** – [#2359](https://github.com/qwibitai/nanoclaw/issues/2359) (merged): Drained in‑flight `dispatchResponse` on SIGTERM, preventing dropped replies on restart or container upgrade.  
  [#2358](https://github.com/qwibitai/nanoclaw/issues/2358) (merged): Drained `routeInbound` before exit, fixing a race that caused lost agent replies during `launchd` restarts and deploys.

- **Intake system redesign** – [#2357](https://github.com/qwibitai/nanoclaw/issues/2357) (merged): Replaced the `INTAKE_ENABLED_PLATFORM_IDS` env‑var allowlist with a per‑channel `auto_url_intake` column in `messaging_groups` and a `/intake` slash command, aligning with the project’s documented design trajectory.

- **Admin CLI** – [#2350](https://github.com/qwibitai/nanoclaw/issues/2350) (merged): Added the `ncl` admin CLI, enabling querying and modification of the central DB (agent groups, messaging groups, sessions, approvals, etc.) via Unix socket and container‑side transport.

- **Documentation fix** – [#2300](https://github.com/qwibitai/nanoclaw/issues/2300) (merged): Corrected Slack member‑ID card directions (button location and icon glyph), reducing setup confusion.

Additionally, issue [#2196](https://github.com/qwibitai/nanoclaw/issues/2196) was closed after a fix for the `resetStuckProcessingRows` crash caused by opening an outbound database in read‑only mode.

## Community Hot Topics

- **[#2360 – Setup script silently deletes existing group configs](https://github.com/qwibitai/nanoclaw/issues/2360)**  
  _Opened today, no comments yet._ A user reports that re‑running `bash nanoclaw.sh` deletes all `groups/*/CLAUDE.md` files without warning, backup, or log. This is a **critical data‑loss issue** and has already drawn attention from contributors. A fix is expected to add a backup step and a confirmation prompt.

- **[#2194 – WhatsApp LID→JID mapping not persisted](https://github.com/qwibitai/nanoclaw/issues/2194)**  
  _Open for 7 days, 1 comment._ In‑memory cache of WhatsApp phone‑JID mappings is lost on restart, causing routing failures for LID‑based senders. Underlying need: persistent mapping store for relaying to phone numbers. No fix PR yet; a database‑backed cache would resolve the issue.

- **[#2355 – `ncl` not added to PATH on upgrade past 2.0.45](https://github.com/qwibitai/nanoclaw/issues/2355)**  
  _Open 1 day._ Users who reach the new version via `/update-nanoclaw` lack the `~/.local/bin/ncl` symlink. Fix PR [#2356](https://github.com/qwibitai/nanoclaw/issues/2356) is open and ready for review.

## Bugs & Stability

Bugs reported today, ranked by severity:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#2360](https://github.com/qwibitai/nanoclaw/issues/2360) | Setup script silently deletes `groups/*/CLAUDE.md` on re‑run – **data loss** | No PR yet, high urgency |
| **High** | [#2194](https://github.com/qwibitai/nanoclaw/issues/2194) | WhatsApp LID→JID mapping lost on restart → routing failures | No fix PR |
| **Medium** | [#2355](https://github.com/qwibitai/nanoclaw/issues/2355) | `ncl` CLI missing from PATH after upgrade | PR [#2356](https://github.com/qwibitai/nanoclaw/issues/2356) open |
| **Medium** | [#2358](https://github.com/qwibitai/nanoclaw/issues/2358) (trace) | SIGTERM mid‑turn dropped agent replies – fixed by merged PR | Fixed in today's merge |
| **Low** | [#2196](https://github.com/qwibitai/nanoclaw/issues/2196) | `deleteOrphanProcessingClaims` crash on readonly DB – fixed | Closed today |

Additional bug‑fix PRs opened today:
- [#2346](https://github.com/qwibitai/nanoclaw/issues/2346) – Unknown slash commands misclassified as `passthrough`, causing silent drops (open)
- [#2352](https://github.com/qwibitai/nanoclaw/issues/2352) – Raises `install_packages` build timeout from 5 to 15 minutes to prevent ETIMEDOUT (open)
- [#2353](https://github.com/qwibitai/nanoclaw/issues/2353) – `chown` new session dirs when host runs as root to avoid container spawn loop on network filesystems (open)
- [#2349](https://github.com/qwibitai/nanoclaw/issues/2349) – Tolerate missing `path` field in mount‑security allowlist entries (open)
- [#2330](https://github.com/qwibitai/nanoclaw/issues/2330) – axios MCP servers failing through OneCLI proxy due to HTTP/1.0 vs CONNECT (open)

## Feature Requests & Roadmap Signals

- **Kubernetes container runtime** – [#2354](https://github.com/qwibitai/nanoclaw/issues/2354) (opened yesterday, feature request) would allow spawning per‑session agent containers as Kubernetes pods instead of local Docker. This aligns with the project’s move toward container abstraction and likely targets a 2.1 feature release.

- **Container config moved to DB** – [#2351](https://github.com/qwibitai/nanoclaw/issues/2351) (open PR, 1 day old) moves the source of truth for container runtime configuration from `container.json` files to a new `container_configs` table. This is a natural companion to the recent admin CLI and would simplify multi‑host deployments.

- **Slash command improvements** – [#2346](https://github.com/qwibitai/nanoclaw/issues/2346) (open PR) treats unknown slash commands as normal chat instead of passing them through to the Agent SDK, preventing silent message drops. Likely to land in next patch.

- **Further shutdown hardening** – The two shutdown fixes merged today (#2358, #2359) are part of an ongoing effort to make NanoClaw production‑ready for auto‑restarting environments; additional patterns may be identified.

## User Feedback Summary

- **Pain point: Data loss in setup script** – [#2360] reports that re‑running the setup script destroys custom agent configurations with no warning. This is the most severe usability complaint today.
- **Pain point: WhatsApp routing breaks on restart** – [#2194] shows that multi‑platform messaging users lose WhatsApp call routing when the daemon restarts.
- **Pain point: Missing CLI tool after upgrade** – [#2355] reflects frustration that `ncl` is not on PATH for existing users, undermining the promise of a simplified admin experience.
- **Pain point: Build timeout on slow networks** – The `install_packages` flow (#2352) can cause a stuck container build; a user likely experienced a disrupted session.
- **Minor friction: Slack setup instructions** – [#2300] (merged) fixed confusing documentation; users previously wasted time on wrong icon/position.
- **Use case: Kubernetes deployment** – [#2354] request indicates enterprise users want to run NanoClaw agents on a cluster, suggesting production adoption beyond single‑host Docker.

## Backlog Watch

Several PRs have been open for **17+ days** without maintainer review or merge:

- [#1917](https://github.com/qwibitai/nanoclaw/issues/1917) – Rename `@Andy` trigger references in runtime group registration (open since 2026-04-22)
- [#1916](https://github.com/qwibitai/nanoclaw/issues/1916) – Guard numeric config env vars against NaN and non‑positive values (open since 2026-04-22)
- [#1913](https://github.com/qwibitai/nanoclaw/issues/1913) – Rename `@Andy` triggers when assistant name changes (open since 2026-04-22)
- [#1912](https://github.com/qwibitai/nanoclaw/issues/1912) – Handle empty container stdout with clear error in fallback parser (open since 2026-04-22)

These are small, well‑scoped fixes that should be low risk. Their age suggests either maintainer bandwidth is stretched or they need rebasing. They should be prioritised for the next maintenance merge.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest — 2026-05-09

### 1. Today's Overview
NullClaw saw a moderate activity day with two open bugs filed and one PR merged. A new nightly prerelease was published automatically, continuing the project's CI modernization. The community contributed a draft hackathon feature for a Data Governance Layer, while two configuration and security-related issues highlight stability gaps. Overall health is stable but with active quality-of-life regressions needing fixes.

### 2. Releases
A new **nightly prerelease** was published:  
- **Version:** `nightly-20260509-5d533da`  
- **Commit:** `5d533da90dd0986edf190247c27655f969bdcb7d`  
- **Workflow:** [Run #25590590011](https://github.com/nullclaw/nullclaw/actions/runs/25590590011)  

No breaking changes or migration notes are provided; this is a rolling nightly build. The release is automated via the merged CI pipeline (PR #899).

### 3. Project Progress
- **PR #899** ([closed/merged](https://github.com/nullclaw/nullclaw/pull/899)): *ci: publish nightly prerelease* – Enables scheduled nightly publishing using the reusable `nullbuilder` workflow. Merged today.

No other PRs were closed. The open hackathon PR #885 was updated but is not yet merged.

### 4. Community Hot Topics
Both open issues currently have no comments or reactions, but they represent the most active discussions by virtue of being filed today:

- **Issue #901** [bug]: [`channel list` always shows "not configured" for telegram despite correct config.json](https://github.com/nullclaw/nullclaw/issues/901)  
  *Underlying need:* Configuration consistency – when `nullclaw config` shows correct settings, `channel list` should reflect that. Frustrating user workflow for Telegram users.

- **Issue #900** [bug]: [`approval_request` defined in spec but never emitted — supervised mode fails risky commands instead of prompting](https://github.com/nullclaw/nullclaw/issues/900)  
  *Underlying need:* Supervised mode is broken; the architecture exists but the signal is not actually sent. Need an immediate fix to restore the intended approval prompt UX.

### 5. Bugs & Stability
Two bugs reported today, both open with no fix PRs yet:

| Issue | Severity | Description |
|-------|----------|-------------|
| [#900](https://github.com/nullclaw/nullclaw/issues/900) | **High** | `approval_request` not emitted – supervised mode silently fails instead of prompting. Affects security policy gating for risky tool execution. |
| [#901](https://github.com/nullclaw/nullclaw/issues/901) | **Medium** | `channel list` reports "not configured" for Telegram even when config.json is correct. Affects user experience but not core functionality. |

No crashes or regressions beyond these two reported.

### 6. Feature Requests & Roadmap Signals
- **PR #885** (draft, [hackathon](https://github.com/nullclaw/nullclaw/pull/885)): *feat(memory): Add NullClaw Data Governance Layer* – Submitted by team “Безопасность бэкофиса (DS)” during WB × OpenSource Hackathon. This adds a data governance overlay to the memory subsystem. If reviewed positively, could be included in a future minor release.

- The nightly release pipeline (PR #899) improves release automation, aligning with the project's goal of consistent pre-release delivery.

Predictions: Next version (v2026.5?) may address the two high-impact bugs and possibly integrate the Data Governance Layer if the hackathon team further refines it.

### 7. User Feedback Summary
- **Pain point:** Config correctness vs channel list discrepancy (Issue #901) – users expect that if `config` shows a channel as configured, `channel list` should reflect that. Confusing and time-wasting.  
- **Pain point:** Supervised mode does not prompt for risky commands (Issue #900) – users relying on approval-based security are left with hard failures instead of interactive approval. Dissatisfaction with broken spec compliance.  
- **Use case:** Telegram channel integration appears to be a primary use case. The hackathon Data Governance Layer indicates interest in enterprise/regulatory compliance features.

Overall satisfaction is tempered by the two fresh bugs, but the hackathon engagement shows community investment.

### 8. Backlog Watch
- **PR #885** (draft, [open since 2026-05-04](https://github.com/nullclaw/nullclaw/pull/885)) – last updated today but still awaiting maintainer review/reaction. This is a substantial proposal from a hackathon team; a maintainer response would help guide its integration or request adjustments.

No other issues or PRs have remained unanswered for an extended period; both bug reports are less than 24 hours old.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-09

## 1. Today's Overview
The IronClaw project continues at high intensity, with **45 pull requests updated** in the last 24 hours (27 open, 18 merged/closed) and **12 active issues** receiving updates. No new releases were cut today. Activity is dominated by **Reborn** (the next-generation engine and session architecture) – nearly two‑thirds of issues and PRs target that epic. A significant number of PRs involve hardening and infrastructure: durable secrets stores, credential encryption, driver registry, and checkpoint state staging. The CI/CD pipeline shows one nightly E2E failure and a production bug (mission results posted to wrong conversation) reported today, both under active investigation. Overall, the project is in a heavy development and integration phase with parallel streams for Reborn cutover, platform stability, and user‑facing features.

## 2. Releases
**None.** No new versions were published today. The last release was `ironclaw v0.28.0` (cut yesterday, PR #3388). That release included `ironclaw_common` v0.4.2 (API‑compatible changes) and `ironclaw` v0.28.0.

---

## 3. Project Progress (Merged/Closed PRs today)
18 PRs were merged or closed in the last 24 hours. Key completions:

- **Reborn credential and secret infrastructure**  
  - [#3408](https://github.com/nearai/ironclaw/pull/3408) *(closed)* – Encrypt durable Reborn credential payloads with `SecretsCrypto`.  
  - [#3401](https://github.com/nearai/ironclaw/pull/3401) *(closed)* – Add durable credential stores (account/session persistence for libSQL and Postgres).  
  - [#3413](https://github.com/nearai/ironclaw/pull/3413) *(closed)* – Add `CheckpointStateStore` contract and in‑memory implementation for Reborn loop checkpoint payload staging.  
  - [#3405](https://github.com/nearai/ironclaw/pull/3405) *(closed)* – Add loop driver registry and readiness validation in `ironclaw_reborn`.  
  - [#3403](https://github.com/nearai/ironclaw/pull/3403) *(closed)* – Add Reborn production loop model gateway (`ThreadBackedLoopModelGateway`).  
  - [#3397](https://github.com/nearai/ironclaw/pull/3397) *(closed)* – Emit Reborn loop support model and transcript milestones.

- **Bug fixes and stability**  
  - [#3366](https://github.com/nearai/ironclaw/pull/3366) *(closed)* – Fix missions: auto‑resume paused missions after OAuth/approval gate resolution (half‑2 of #3133, DB migration).  
  - [#3412](https://github.com/nearai/ironclaw/pull/3412) *(open)* – Harden durable credential stores (atomic consumption, parameterized lookups). *Note: status open, but updated today – progress on hardening.*  
  - [#3390](https://github.com/nearai/ironclaw/pull/3390) *(open)* – Isolate cross‑tenant SSE/WS status events and thread access (multi‑tenant leak fix).

- **Other**  
  - [#3309](https://github.com/nearai/ironclaw/pull/3309) *(open)* – Make Skills E2E lifecycle deterministic (Playwright API mocks).  
  - [#3303](https://github.com/nearai/ironclaw/pull/3303) *(open)* – Add Reborn memory substrate E2E coverage.

---

## 4. Community Hot Topics
The most active discussions are concentrated on **Reborn integration test suites and architecture definitions**:

- **[Issue #3067](https://github.com/nearai/ironclaw/issues/3067)** – *Reborn: Add vertical‑slice integration test suite*  
  **32 comments** – Highest engagement. Discusses caller‑level integration tests for the Reborn stack. The underlying need is proving the substrate works through public entrypoints rather than unit/contract tests alone.  
- **[Issue #3016](https://github.com/nearai/ironclaw/issues/3016)** – *Reborn cutover blocker: add reference AgentLoopHost facade*  
  **11 comments** – A critical path item. Community members are validating the facade contract against existing v2 engine calls.  
- **[Issue #3193](https://github.com/nearai/ironclaw/issues/3193)** – *Define conversation binding and session thread contracts*  
  **5 comments** – Implemented semantic slice on `origin/reborn-integration`. Still open for final contract sign‑off.  
- **[Issue #3107](https://github.com/nearai/ironclaw/issues/3107)** – *Define AgentLoopDriver and run‑class profile contract*  
  **3 comments** – Parent of many subsidiary issues (driver registry, host factory, checkpointing).

No PRs show comment counts in the data, but PR activity is high, especially from core contributors `serrrfirat` and `ilblackdragon`.

---

## 5. Bugs & Stability
Two bugs reported today, with the fix for one already in progress.

| Issue | Severity | Summary | Fix PR Status |
|-------|----------|---------|---------------|
| [#3323](https://github.com/nearai/ironclaw/issues/3323) | **High** | Nightly E2E scheduled run failed. Workflow run: [link](https://github.com/nearai/ironclaw/actions/runs/25591324197). Job: "Full E2E / E2E (web‑regressions)" failed.  | No fix PR yet – likely auto‑generated alert, investigation pending. |
| [#3415](https://github.com/nearai/ironclaw/issues/3415) | **High (production)** | Mission results posted to wrong conversation in production for user `tall‑elk‑vuvim` (v0.27.0). Results from a daily NYC weather mission appear in a different conversation than where the mission was created. | No fix PR yet – reported by `sunglow666` today. |

**Stability note:** The nightly E2E failure may be related to web regression tests – see PR [#3309](https://github.com/nearai/ironclaw/pull/3309) which makes Skills E2E deterministic (merged today) – that might address similar flakiness.

---

## 6. Feature Requests & Roadmap Signals
User‑visible feature requests are few today, but several internal feature issues signal the upcoming **Reborn cutover**:

- **Reborn v2 engine driver model adapter** – Issues [#3410](https://github.com/nearai/ironclaw/issues/3410), [#3409](https://github.com/nearai/ironclaw/issues/3409), [#3407](https://github.com/nearai/ironclaw/issues/3407), [#3406](https://github.com/nearai/ironclaw/issues/3406), [#3404](https://github.com/nearai/ironclaw/issues/3404), [#3402](https://github.com/nearai/ironclaw/issues/3402) – All filed by `serrrfirat` today. They represent the **completion of the Reborn loop driver stack**: host‑owned prompt bundle port, text‑only factory, checkpoint state staging, concrete TurnRunner worker composition, and driver registry. This signals that the next IronClaw release (v0.29.0+) will likely include the first Reborn‑capable runtime.
- **Multi‑tenant SSE/WS isolation** – PR [#3390](https://github.com/nearai/ironclaw/pull/3390) addresses a security leak; this may land soon as a hotfix.
- **WeCom (Enterprise WeChat) channel** – PR [#2394](https://github.com/nearai/ironclaw/pull/2394) (open since April 13) adds a WASM‑based WeCom channel, requested by the enterprise community.

No direct user‑submitted feature requests appeared in today's data; most new issues are technical debt or internal architecture.

---

## 7. User Feedback Summary
Today's user feedback is limited to one production bug:

- **Mission conversation routing** – User `sunglow666` reports that mission results are being posted to the wrong conversation (Issue [#3415](https://github.com/nearai/ironclaw/issues/3415)). This is a **concrete pain point** for anyone using recurring missions (e.g., daily weather updates). The user expects results in the conversation where the mission was created. No workaround is mentioned.

Otherwise, no new feature satisfaction/dissatisfaction comments surfaced. Previous discussions around Reborn (e.g., Issue #3067) are developer‑focused.

---

## 8. Backlog Watch
Two items warrant attention due to age, risk, or lack of maintainer response:

1. **[Issue #3067](https://github.com/nearai/ironclaw/issues/3067)** – *Reborn: Add vertical‑slice integration test suite* (created Apr 29, 10 days ago) – high risk, critical for Reborn cutover. Despite 32 comments, still no fix PR; ongoing discussion about design.  
2. **[PR #1378](https://github.com/nearai/ironclaw/pull/1378)** – *feat(routing): per‑channel MCP and built‑in tool filtering* (created Mar 18, 52 days ago) – large PR (XL), risk medium, by experienced contributor `nick‑stebbings`. No updates in the last 24h; last activity May 9 (possibly stale). Needs maintainer review or guidance.  
3. **[PR #2394](https://github.com/nearai/ironclaw/pull/2394)** – *feat: wecom channel* (created Apr 13, 26 days ago) – large, risk high, very active in discussion but not merged. Important for enterprise users. Maintainers may need to prioritize or provide feedback.

No other issues appear to have been ignored for extended periods given the high overall activity.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-09

## 1. Today's Overview

The project saw a burst of activity with **18 pull requests updated in the last 24 hours**, of which **16 were merged or closed** — indicating a focused release cycle. No new releases were cut, but the high merge rate suggests preparations for a near-term build. Two new UI polish issues were opened, both receiving quick feedback. Overall, the project is in **active maintenance mode**, with engineering effort concentrated on bug fixes, UI consistency, and cherry-picking features into a `release/2026.05.08` branch.

---

## 2. Releases

*No new releases were published in the last 24 hours.*

---

## 3. Project Progress

**16 PRs were merged or closed** in the past day, covering multiple areas:

| Area | Changes |
|------|---------|
| **Cowork (Agent Collaboration)** | Fixed cache read display when value is zero ([#1927]), fixed stop-session not halting crawler tasks ([#1923], cherry-picked from [#1756]), fixed `NO_REPLY` prefix appearing in conversations ([#1918]) |
| **Renderer / UI** | Updated file list icon style ([#1931]), modified preview file list display ([#1926]), fixed duplicate/validity issues in preview files ([#1925]), optimized sidebar UI ([#1928]) and agents layout ([#1924]), overrode local agent avatar ([#1929]) |
| **Code Block** | Cherry-picked full rewrite using CodeMirror 6 from [#1306] into release branch ([#1922]) — adds syntax highlighting, search, line numbers, fullscreen modal |
| **Form UX** | Added required field red-star indicators (cherry-pick from [#1511] into release branch, [#1919]) |
| **Bookmark** | Merged bookmark feature for Cowork messages ([#1664]) — star messages, view in sidebar, jump to original context |
| **Dependency** | Upgraded `penclaw-weixin` to v2.4.3 ([#1930]) |

**Open PRs (2 remaining):**
- [#1769] — Skeleton loading screen for Cowork initialization (addresses issue #1920)
- [#1770] — Enhanced empty states for Skills Manager and TaskRunHistory (addresses issue #1921)

---

## 4. Community Hot Topics

Both open issues in the last 24 hours are UI polish requests with identical author (`xiaoye5200`). Although they have few comments or reactions (0–1), they have corresponding open PRs, indicating the team is already acting on them.

- **[#1920] Blank loading state during Cowork initialization**  
  *User reports static `Loading...` text instead of a skeleton shimmer, creating a jarring experience.*  
  → Related PR [#1769] (open, 18 days old) proposes animated skeleton placeholders.

- **[#1921] Empty states lacking icons and subtitles**  
  *SkillsManager and TaskRunHistory empty placeholders feel unfinished compared to richer empties elsewhere.*  
  → Related PR [#1770] (open, 18 days old) adds PuzzleIcon and subtitles.

**Why these matter:** Both signal a user desire for **visual polish and consistency** — a recurring theme as the project matures from functional to polished.

---

## 5. Bugs & Stability

| Severity | Bug / Issue | Status |
|----------|-------------|--------|
| **High** | Cowork stop session does not halt crawler tasks — users click "Stop" but crawlers keep running until cooldown. | Fixed in [#1756] and cherry-picked into release via [#1923]. |
| **Medium** | `NO_REPLY` text appears as visible content in conversations. | Fixed in [#1918]. |
| **Medium** | Cowork initialization displays plain "Loading..." text with no feedback — a UX regression. | Issue [#1920]; fix PR [#1769] open. |
| **Low** | Preview files show duplicates or invalid entries. | Fixed in [#1925]. |
| **Low** | Cache read display shows `0` value unnecessarily. | Fixed in [#1927]. |

No crashes or regressions were reported today.

---

## 6. Feature Requests & Roadmap Signals

The two new issues (#1920, #1921) are **explicit user requests for UI enhancements**. Based on the presence of open PRs, these are likely slated for the next release.

**Other signals from recent merges:**
- **CodeMirror 6 for code blocks** – now in release branch; offers advanced code interaction (search, fold, fullscreen). Likely will ship in next version.
- **Bookmarking for messages** – a new user-requested feature that adds a sidebar, star icons, and context jumping – merged into main.
- **Required field indicators** – part of a continued UX improvement sweep.

**Prediction:** The next release (`2026.05.09` or `2026.05.10`) will likely include skeleton loading screens, enriched empty states, CodeMirror 6, and bookmark features.

---

## 7. User Feedback Summary

While raw user comments are limited, the following **pain points** are directly voiced in issues:

- **“Blank / jarring user experience”** (#1920) – Loading state is a primary interaction point; poor feedback frustrates users.
- **“Feel unfinished”** (#1921) – Inconsistency in empty states undermines perceived quality.
- **Crawler not stopping** (#1756) – Critical workflow interruption; users expect immediate stop on click.

No obvious satisfaction signals were logged, but the fast PR turnaround on these issues suggests the team is responsive to feedback.

---

## 8. Backlog Watch

Two PRs have been open for **18 days** without being merged, despite addressing recently raised issues:

- **[#1769] – Skeleton loading screen** (open since 2026-04-20, last updated 2026-05-08)  
  *Direct fix for issue #1920. Awaiting maintainer review/merge.*
- **[#1770] – Enhanced empty states** (open since 2026-04-20, last updated 2026-05-08)  
  *Direct fix for issue #1921. Awaiting maintainer review/merge.*

Both are authored by the same user (`xiaoye5200`) who also filed the issues. The delay may be due to prioritization of the release branch, but they are strong candidates for inclusion in the upcoming release.

Additionally, no open issues are older than 1 day except these two PRs. The backlog is relatively clean.

---

*Data source: GitHub – [netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI)*

[#1927]: https://github.com/netease-youdao/LobsterAI/pull/1927
[#1923]: https://github.com/netease-youdao/LobsterAI/pull/1923
[#1756]: https://github.com/netease-youdao/LobsterAI/pull/1756
[#1918]: https://github.com/netease-youdao/LobsterAI/pull/1918
[#1931]: https://github.com/netease-youdao/LobsterAI/pull/1931
[#1926]: https://github.com/netease-youdao/LobsterAI/pull/1926
[#1925]: https://github.com/netease-youdao/LobsterAI/pull/1925
[#1928]: https://github.com/netease-youdao/LobsterAI/pull/1928
[#1924]: https://github.com/netease-youdao/LobsterAI/pull/1924
[#1929]: https://github.com/netease-youdao/LobsterAI/pull/1929
[#1922]: https://github.com/netease-youdao/LobsterAI/pull/1922
[#1306]: https://github.com/netease-youdao/LobsterAI/pull/1306
[#1919]: https://github.com/netease-youdao/LobsterAI/pull/1919
[#1511]: https://github.com/netease-youdao/LobsterAI/pull/1511
[#1664]: https://github.com/netease-youdao/LobsterAI/pull/1664
[#1930]: https://github.com/netease-youdao/LobsterAI/pull/1930
[#1769]: https://github.com/netease-youdao/LobsterAI/pull/1769
[#1770]: https://github.com/netease-youdao/LobsterAI/pull/1770
[#1920]: https://github.com/netease-youdao/LobsterAI/issues/1920
[#1921]: https://github.com/netease-youdao/LobsterAI/issues/1921

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest — 2026-05-09

### 1. Today's Overview

Project activity is low today with **no open or closed issues** updated in the last 24 hours. Pull request activity is moderate: **5 PRs** were updated, of which **2 were merged/closed** (a locale update and a voice settings improvement), and **3 remain open**, including a large ongoing effort to add persistent agent sessions. A new release (`20260508.01`) was published yesterday, indicating steady incremental delivery. Overall, the project is moving forward but lacks the high-velocity churn of community engagement on issues.

### 2. Releases

- **Latest Release:** `20260508.01` (published 2026-05-08)
  - No release notes or changelog are provided in the data, so the exact contents are unknown. However, given that two PRs (#986 and #984) were closed on May 8–9, it is likely this release includes improved Traditional Chinese locale support and OpenAI voice model guidance.
  - **No migration notes or breaking changes** indicated. Users can safely upgrade via standard channels.

### 3. Project Progress

Two pull requests were merged/closed in the last 24 hours:

- **#986 – Update and improve zh-TW Traditional Chinese locale**  
  Standardised UI translations across modules, with consistent terminology for “AI 助理” and “Moltis”. [PR #986](https://github.com/moltis-org/moltis/pull/986) *(closed)*

- **#984 – feat(voice): surface OpenAI realtime model guidance**  
  Added STT model selection for Whisper (`gpt-4o-transcribe`, `gpt-4o-mini-transcribe`) and surfaced Realtime voice model IDs in voice settings to prevent misconfiguration. Included Playwright coverage. [PR #984](https://github.com/moltis-org/moltis/pull/984) *(closed)*

These advances improve internationalisation and voice configuration safety.

### 4. Community Hot Topics

No issues or PRs attracted significant comments or reactions; all entries have `0` 👍. The most active PRs (by recency of updates) are:

- **#566 – feat(external-agents): add persistent agent sessions**  
  A long-running open PR that adds persistence for external agent sessions (ACP, Codex CLI, Claude Code). Last updated May 8 after a month of inactivity. [PR #566](https://github.com/moltis-org/moltis/pull/566) *(open)*  
  *Underlying need:* Users want conversational continuity when switching between external agents.

- **#985 – Refresh web chat composer**  
  Redesigns the chat input area with a centered rounded composer, footer controls, attachment picker, and improved token/context display. This aligns with UX modernisation. [PR #985](https://github.com/moltis-org/moltis/pull/985) *(open)*

- **#987 – Replace docs deployment with Astro site**  
  Moves documentation from mdBook to Astro, preserving existing Markdown sources, adding sidebar navigation, search, copy buttons, and theme support. [PR #987](https://github.com/moltis-org/moltis/pull/987) *(open)*

### 5. Bugs & Stability

**No bugs, crashes, or regressions were reported today.** The project appears stable in the last 24-hour window, with no open issues and no defect-related PRs.

### 6. Feature Requests & Roadmap Signals

No new feature requests (issues) were filed. The following ongoing or recently merged features signal likely roadmap inclusions:

- **Persistent agent sessions** (#566) – A major feature that would allow users to keep context across external agent conversations. Given it has been open for over a month and was recently updated, it may be close to review/merge and likely appears in the next release.
- **Chat composer redesign** (#985) – A UX improvement that is still open; depending on review speed, it could land in the next minor version.
- **Astro-based docs site** (#987) – A substantial infrastructure change; if merged, it would improve documentation accessibility and maintainability.

No other feature signals (e.g., from user requests) were present.

### 7. User Feedback Summary

No direct user feedback (issues, comments) was recorded today. The only traces of user needs come from PR descriptions:

- Localisation improvements (#986) reflect a desire for clearer, more consistent Traditional Chinese translations.
- Voice guidance (#984) indicates users were confused about which model IDs to use for clip transcription vs. Realtime sessions – the fix addresses this usability gap.

Without issue or comment data, broader sentiment cannot be assessed.

### 8. Backlog Watch

The only PR that may be considered stale is:

- **#566 – feat(external-agents): add persistent agent sessions**  
  Created April 6, 2026, and last updated May 8, 2026. Despite the recent update, it has seen no reviewer activity for over a month. This is a non-trivial feature affecting external agent integration and may need maintainer attention to avoid stalling. [PR #566](https://github.com/moltis-org/moltis/pull/566)

No other long-unanswered issues or PRs were identified (no open issues exist).

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-09

## Today’s Overview
CoPaw remains highly active with 36 issues and 42 pull requests updated in the last 24 hours. The project closed or merged 16 issues and 32 PRs, indicating strong development throughput. A new beta release (v1.1.6-beta.1) was published, primarily containing a critical SSE crash fix and improved integration test coverage. Community engagement is robust, though several regression bugs reported by users following the v1.1.5.post2 update signal ongoing stability challenges. The overall project health is strong but warrants close attention to configuration persistence and provider compatibility regressions.

## Releases
- **v1.1.6-beta.1** — published [2026-05-09]
  - **Changes:**
    - Version bumped to 1.1.6b1 ([#4082](https://github.com/agentscope-ai/QwenPaw/pull/4082))
    - Added integration smoke tests for app startup and settings/envs ([#4081](https://github.com/agentscope-ai/QwenPaw/pull/4081))
    - Fixed an SSE crash in the console ([#4082](https://github.com/agentscope-ai/QwenPaw/pull/4082))
  - **Breaking changes:** None reported.
  - **Migration notes:** Standard version upgrade; no special migration steps required.

## Project Progress
Today’s merged/closed PRs (32 total) advanced several feature areas, including:

- **MCP integration:** `feat(mcp): support listing tools for mcp` ([#3149](https://github.com/agentscope-ai/QwenPaw/pull/3149)) — enables enumeration of tools exposed by MCP servers.
- **WeCom channel interactivity:** `feat(WeCom): tool-guard interactive approval card` ([#4112](https://github.com/agentscope-ai/QwenPaw/pull/4112)) — adds Approve/Deny buttons for risky tool calls inside Enterprise WeChat.
- **Markdown table rendering:** `fix(channels): keep markdown tables renderable across split_text chunks` ([#4119](https://github.com/agentscope-ai/QwenPaw/pull/4119)) — prevents broken table display on WeChat.
- **Agent config reading:** `fix(agent): replace hardcoded agent name with config-driven value` ([#4140](https://github.com/agentscope-ai/QwenPaw/pull/4140)) — resolves the “Friday” hardcoding issue.
- **Tool schema sanitization:** `fix(tool_schema): add sanitize tool function schemas` ([#4126](https://github.com/agentscope-ai/QwenPaw/pull/4126)) — improves compatibility with stricter providers like DeepSeek.
- **Console performance:** `perf(console): skip chat history lookup for non-arrow keys` ([#4130](https://github.com/agentscope-ai/QwenPaw/pull/4130)) — reduces keydown overhead.
- **Docker/WSL proxy handling:** `fix(cli): bypass proxies for loopback API checks (#3664)` ([#4092](https://github.com/agentscope-ai/QwenPaw/pull/4092)) — resolves Windows proxy-related 502 errors.
- **Localization:** `feat(settings): add pt-BR language support` ([#4143](https://github.com/agentscope-ai/QwenPaw/pull/4143)).

## Community Hot Topics

1. **[Question] Multi-turn chat UI performance (#3350)** — 11 comments  
   User reports severe scroll lag after 200+ conversation turns during project-level code iteration. **Underlying need:** Virtual scrolling or automated context management for long-running agent sessions.  
   [Issue #3350](https://github.com/agentscope-ai/QwenPaw/issues/3350)

2. **[Question] v1.1.5.post2 breaks OpenCode provider (#4133)** — 10 comments  
   Regression after upgrade: `MODEL_EXECUTION_FAILED` error for OpenCode models. v1.1.5 worked fine. Strong community engagement seeking workarounds.  
   [Issue #4133](https://github.com/agentscope-ai/QwenPaw/issues/4133)

3. **[Bug] Multi-agent config does not persist (#4145)** — 7 comments (opened today)  
   Configured agents revert to previous settings, disrupting multi-agent workflows.  
   [Issue #4145](https://github.com/agentscope-ai/QwenPaw/issues/4145)

4. **[Feature] Project-group chat with multi-role rooms (#4131)** — 2 comments, 1 👍  
   User proposes dedicated project-level group chats with role assignment, shared memory, and @-mention routing. Signals demand for structured collaboration features.  
   [Issue #4131](https://github.com/agentscope-ai/QwenPaw/issues/4131)

5. **[Feature] Add conversation deletion (#4113)** — 2 comments, 1 👍  
   Users want to remove low-quality Q&A turns from context to avoid confusion.  
   [Issue #4113](https://github.com/agentscope-ai/QwenPaw/issues/4113)

## Bugs & Stability

### Critical / High Severity
- **[v1.1.5.post2 regression] OpenCode provider fails (#4133)** — `MODEL_EXECUTION_FAILED` on model calls. No fix PR identified yet.  
  [Issue #4133](https://github.com/agentscope-ai/QwenPaw/issues/4133)

- **[New] Multi-agent config not persistent (#4145)** — Agent configuration reverts after saving. Opened today; no fix PR yet.  
  [Issue #4145](https://github.com/agentscope-ai/QwenPaw/issues/4145)

- **[Bug] Failed model calls persist user messages, replayed next turn (#4149)** — Opened today; root cause in session memory handling.  
  [Issue #4149](https://github.com/agentscope-ai/QwenPaw/issues/4149)

- **[Bug] Plan mode executes tools before user confirmation (#4150)** — `create_plan` tool runs immediately without awaiting user approval. Opened today.  
  [Issue #4150](https://github.com/agentscope-ai/QwenPaw/issues/4150)

- **[Bug] Orphan chat entries on restart (#4151)** — Session file not persisted before restart leads to empty conversations. Opened today.  
  [Issue #4151](https://github.com/agentscope-ai/QwenPaw/issues/4151)

- **[Bug] LM Studio integration returns Internal Server Error (#4147)** — Configuration fails; model ID parsing issue suspected. Opened today.  
  [Issue #4147](https://github.com/agentscope-ai/QwenPaw/issues/4147)

### Medium Severity
- **[Bug] Windows: console window flashes on every shell command (#4123)** — User experience degradation.  
  [Issue #4123](https://github.com/agentscope-ai/QwenPaw/issues/4123)

- **[Bug] Ollama connection error message too generic (#4135)** — Docker deployments affected; no clear root cause.  
  [Issue #4135](https://github.com/agentscope-ai/QwenPaw/issues/4135)

- **[Bug] Screenshots fill context; no OCR tool (#4102)** — Visual context not properly gated, causing token waste.  
  [Issue #4102](https://github.com/agentscope-ai/QwenPaw/issues/4102)

### Fixed Today
- **Mermaid graph blank rendering** — `feat(console): support mermaid graph` ([PR #4146](https://github.com/agentscope-ai/QwenPaw/pull/4146)) fixes issue #4137.
- **Agent name hardcoded as “Friday”** — `fix(agent): replace hardcoded agent name with config-driven value` ([PR #4140](https://github.com/agentscope-ai/QwenPaw/pull/4140)) fixes issue #4099.
- **Secrets restore failure on Docker** — `fix(backup): restore secrets on Docker volume mount points` ([PR #3916](https://github.com/agentscope-ai/QwenPaw/pull/3916)) fixes issue #3827.
- **Tool schema incompatibility with DeepSeek** — `fix(tool_schema): add sanitize tool function schemas` ([PR #4126](https://github.com/agentscope-ai/QwenPaw/pull/4126)) resolves issue #4115.
- **MiMo-V2.5 / DeepSeek-V4-Pro duplicate responses** — One discussion mentions it may be related to tool schema; partially addressed by #4126.

## Feature Requests & Roadmap Signals
Likely candidates for the next minor release based on today's PRs and community demand:

1. **Batch browser_use actions** — `feat(tool): browser_use add batch action support` ([PR #4139](https://github.com/agentscope-ai/QwenPaw/pull/4139), open) — enables multiple sequential sub-actions from a single tool call.
2. **Project-level group chats with multi-role rooms** ([#4131](https://github.com/agentscope-ai/QwenPaw/issues/4131)) — Strong community signal; would require significant feature work.
3. **Conversation deletion** ([#4113](https://github.com/agentscope-ai/QwenPaw/issues/4113)) — High user demand for context hygiene; relatively simple to implement.
4. **Timed session clearing** ([#3111](https://github.com/agentscope-ai/QwenPaw/issues/3111)) — Already discussion Open; could arrive as cron-related enhancement.
5. **OAuth login for OpenAI / Codex providers** ([#4124](https://github.com/agentscope-ai/QwenPaw/issues/4124)) — New feature request; low implementation complexity.
6. **System tray startup (Windows)** — `feat(cli-desktop): system tray startup item` ([PR #4041](https://github.com/agentscope-ai/QwenPaw/pull/4041), open) — Indicates growing desktop-first UX focus.

## User Feedback Summary
- **Positive signals:** Community appreciates fast iteration (32 merged PRs/day), and the new MCP listing feature and WeCom interactive approvals are well received. The Portuguese localization and Mermaid graph support are direct responses to user requests.
- **Pain points (recurring):**
  - **Upgrade regressions:** Several users reported that v1.1.5.post2 broke previously working provider configurations (OpenCode, LM Studio, Ollama).
  - **Context management:** Long-running sessions (200+ turns) cause UI lag; users want virtual scrolling or context summarization. Screenshots and video bloat are also criticized.
  - **Configuration persistence:** Multi-agent setups lose custom settings; agent name hardcoding annoys users who rename “Friday.”
  - **Channel routing:** Cron jobs sometimes dispatch to the wrong channel (console instead of WeChat), causing missed notifications.
- **Satisfaction drivers:** The project’s responsiveness to bugs and feature requests (e.g., Mermaid fix shipped same day) maintains high community trust despite occasional regressions.

## Backlog Watch
- **Issue #2165** — [Bug]: Unknown agent error on model switch. **Created 2026-03-24, last updated 2026-05-08.** No maintainer response in over a month.  
  [Issue #2165](https://github.com/agentscope-ai/QwenPaw/issues/2165)

- **PR #3117** — `Feat/semantic skill routing` — **Created 2026-04-08, open and under review.** Adds embedding-based skill filtering to reduce context token usage. Awaiting further discussion or review from maintainers.  
  [PR #3117](https://github.com/agentscope-ai/QwenPaw/pull/3117)

- **PR #4041** — `feat(cli-desktop): system tray startup item` — **Created 2026-05-05, open and under review.** Win32-only system tray support; needs maintainer feedback on cross-platform strategy.  
  [PR #4041](https://github.com/agentscope-ai/QwenPaw/pull/4041)

- **Issue #3111** — `[Feature]: Timed session clearing` — **Created 2026-04-08.** Open enhancement with moderate community interest; no active PR.  
  [Issue #3111](https://github.com/agentscope-ai/QwenPaw/issues/3111)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-09

## Today's Overview
ZeptoClaw saw no new issues or releases in the past 24 hours, and only one pull request (#571) was updated yesterday. The project appears to be in a low-activity phase, with maintainer focus on refining existing features rather than introducing new ones. The single open PR indicates steady but slow progress on tool description improvements. No community engagement (comments, reactions) was recorded on any open items.

## Releases
No new releases.

## Project Progress
No pull requests were merged or closed today. The only active PR (#571) is still open and under review:

- **#571 [OPEN]** `feat(tools): trigger-phrase nudges in longterm_memory description`  
  *Author: qhkm* · Updated: 2026-05-08  
  Rewrites the `longterm_memory` tool’s `description()` to explicitly list “Use when” / “Do NOT use when” triggers, following the pattern from Hermes Agent’s `memory_tool.py`. Also adds a doc-test (`test_tool_description_has_trigger_phrases`) to guard against future removal of these trigger blocks.  
  This enhancement aims to improve tool selection reliability for agents using long-term memory.

*GitHub*: [qhkm/zeptoclaw PR #571](https://github.com/qhkm/zeptoclaw/pull/571)

## Community Hot Topics
No issues or PRs accumulated meaningful discussion or reactions in the last 24 hours. The only open PR (#571) has zero comments and zero 👍 reactions, reflecting low community engagement at this time.

## Bugs & Stability
No new bugs, crashes, or regressions were reported today. No open issues tagged as bugs exist in the data. The project remains stable with no urgent stability concerns.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. The ongoing work in PR #571 signals a roadmap focus on improving tool description clarity and guardrails for agent decision-making. This pattern (mirroring Hermes Agent) may be extended to other tool descriptions in future releases.

## User Feedback Summary
No user feedback (comments, reactions, or issue reports) was provided in the past 24 hours. The absence of pain points or satisfaction signals suggests either a stable user base or low active usage at this time.

## Backlog Watch
No long-unanswered issues or PRs requiring maintainer attention. The only open PR (#571) has been actively updated by the author and is not considered stale. The project backlog is effectively clean.

---

*Data snapshot for 2026-05-09, generated from qhkm/zeptoclaw GitHub activity.*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-09

## 1. Today's Overview
The project saw extremely high traffic over the past 24 hours: **50 issues updated** (all still open) and **50 pull requests updated** (32 open, 18 merged/closed). No new releases were published. Activity is concentrated on bug fixes and community-requested enhancements, with a notable cluster of build and provider compatibility issues. The wave of merged PRs indicates active development velocity, but the sheer volume of open issues (50 in one day) suggests a maintenance backlog is building.

## 2. Releases
**No releases this period.** The last tagged release remains 0.7.5. Several PRs are targeting an upcoming `v0.8.0` integration branch (e.g., #6545 for multi-agent runtime).

## 3. Project Progress
**18 PRs were merged or closed** today. Highlights of merged/closed work:

- **#6191** (closed, fix) – Reply-intent classifier guard against meta-instruction echo – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6191)
- **#6178** (closed, enhancement) – Ollama `num_ctx`/`num_predict`/temperature tuning – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6178)
- **#6536** (closed, bugfix) – Gateway returns onboarding error via WS chat instead of crashing – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6536)
- **#6048** (closed, enhancement) – Nextcloud Talk draft-update streaming (follow-up to #5718) – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6048)

Other notable open PRs that advanced today (not yet merged):

- **#6544** (fix) – Omit native tool prompt catalog when provider-native tools are active – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6544)
- **#6545** (feat) – Multi-agent runtime additive landing (70% of #6272) on `integration/v0.8.0` – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6545)
- **#6542** (docs) – User-facing skills guide – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6542)
- **#6527** (fix) – Broadcast observer events to SSE endpoint – [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6527)

## 4. Community Hot Topics
The three issues attracting the most discussion (3 comments each) are:

- **#6530** [Bug] Build failure with matrix-sdk v0.16.0 – recursion limit overflow with `channel-matrix` feature. User reports blocking build for 0.7.5. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6530)
- **#6378** [Feature] Discord bot respond only in specific channels – mirrors `allowed_rooms` from Matrix. Strong demand for parity. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6378)
- **#6298** [Bug] Empty `tool_calls` array sent to strict validators (DeepSeek, NVIDIA NIM) – causes 400 errors. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6298)

Underlying need: **Provider compatibility and configuration flexibility** are top community priorities. The Matrix SDK build breakage and the missing Discord channel restriction both show friction when deploying ZeroClaw in production environments with strict backend requirements.

## 5. Bugs & Stability
Several new or newly active bugs were reported, ranked by severity:

### Critical / High Priority (P1)
- **#6298** (p1) – Empty `tool_calls` array sent to strict providers → 400 errors. No fix PR yet. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6298)
- **#6309** (p1) – `model_routing_config` "upsert_agent" stomps on `schema_version = 2` settings. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6309)
- **#6254** (p1) – WASM plugin install path vs runtime scan path diverge → plugins invisible. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6254)
- **#6526** (p2, but with fix PR) – SSE drops tool-call events; `BroadcastObserver` bypassed. **Fix PR #6527** exists. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6526) | [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6527)
- **#6517** (p2) – Context overflow causes hallucination / topic drift. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6517)

### Medium / Notable
- **#6520** (p2) – Gemini CLI provider crashes due to outdated `--print` vs `--prompt` argument syntax. **Fix PR #6519** open. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6520) | [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6519)
- **#6528** (p2) – Trust system CA for provider requests (self-signed certs). Needs maintainer review. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6528)
- **#6433** (p2) – Heartbeat not working with Matrix channel. **Fix PR #6509** open. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6433) | [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6509)
- **#6524** (p2) – Matrix root timeline messages create separate threaded sessions when `reply_in_thread=true`. **Fix PR #6525** open. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6524) | [PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6525)
- **#6280** (p2) – Windows full build fails in `zeroclaw-hardware` crate. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6280)
- **#6419** (p2) – `WorkspaceManager` fails to load profiles at startup on Windows. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6419)
- **#6422** (p2) – `cron_add` schedule error message unhelpful for plain string input. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6422)
- **#6530** (p3) – Build failure with matrix-sdk v0.16.0 recursion limit. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6530)

Several of these bugs already have open fix PRs, indicating responsive maintainers. The Windows build and provider compatibility bugs remain the most disruptive.

## 6. Feature Requests & Roadmap Signals
New feature requests and their likely inclusion in upcoming releases:

### Likely for v0.8.0 (integration branch active)
- **#6272** – Multi-agent runtime with per-alias workspaces and permissions – **PR #6545** lands the additive 70%. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6272)
- **#6271** – V3 `SwarmConfig` schema + runtime – major config redesign. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6271)
- **#6273** – Typed-family split for model/TTS providers; dead field deletion. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6273)
- **#6270** – Configurable macro for v3 nested config shapes. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6270)

### High demand / next-wave features
- **#6378** – Discord `allowed_channels` (parity with Matrix) – likely to be addressed after multi-agent lands. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6378)
- **#6522** – Web chat tool approval UI for supervised mode – backend already supports, frontend missing. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6522)
- **#6345** – Per-channel `reply-min-interval-secs` (throttle agent replies) – for WhatsApp/paired identity channels. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6345)
- **#6518** – First-class support for custom OpenAI-compatible providers (Kimi K2.5) – currently requires workarounds. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6518)
- **#6543** – ACP session restore – protocol feature. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6543)
- **#6510** – Cron `delivery.mode = "announce"` option to send only final message. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6510)
- **#6260** – Configurable LM Studio server URL across all surfaces. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6260)
- **#6255** – Named provider entries ignored; `kind` field broken. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6255)

### Desktop & UX polish
- **#6339** – Universal binary for macOS (arm64+x86_64). [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6339)
- **#6327** – Desktop menu-bar chat with channels overview. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6327)
- **#6329** – Tray menu items (quit, restart gateway, copy token, logs). [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6329)

The multi-agent runtime and provider config overhaul dominate the near-term roadmap, while Discord and desktop parity features are poised for next.

## 7. User Feedback Summary
User sentiment reflects both enthusiasm and frustration:

- **Pain points (dissatisfaction):**
  - Build failures (Matrix SDK, Windows) prevent adoption. Multiple issues (#6530, #6280) with no immediate fix.
  - Provider compatibility gaps: DeepSeek/NVIDIA reject empty tool calls (#6298), Gemini CLI crash (#6520), custom providers hard to add (#6518, #6255). Users need workarounds.
  - Missing parity features: Discord `allowed_channels` (#6378) and cron announce mode (#6510) are requested repeatedly.
  - Context management: Hallucination/drift (#6517) and no per-channel throttle (#6345) degrade long-running conversations.
  - Plugin discovery broken (#6254) – install path versus scan path mismatch.

- **Satisfaction signals:**
  - Rapid PR merge activity shows maintainers are responsive. Multiple bug fix PRs landed today.
  - Users contributing fixes themselves (e.g., #6519 for Gemini, #6525 for Matrix threading, #6509 for heartbeat). Community involvement is strong.
  - Documentation improvements (#6542) and provider tuning (#6178) address common concerns.

Overall, users are engaged but are experiencing friction from a rapidly evolving codebase and incomplete migration to v0.8.0 config schemas.

## 8. Backlog Watch
Issues and PRs that require maintainer attention or have been open without resolution:

- **#6074** (2026-04-24) – Audit lost 153 commits from bulk revert – long-standing meta-issue for recovery. Needs triage. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)
- **#6528** (2026-05-08) – Trust system CA for providers – tagged `needs-maintainer-review`. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6528)
- **#6518** (2026-05-07) – First-class custom provider support – same tag. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6518)
- **#6345** (2026-05-03) – Per-channel reply-min-interval – also `needs-maintainer-review`. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6345)
- **#6279** (2026-05-02) – Improve release tag triage selection – needs maintainer feedback on priorities. [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6279)
- **#6517** (2026-05-07) – Context overflow hallucination – tagged `needs-author-action` (author may need to provide more info). [Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6517)

The bulk revert audit (#6074) is particularly important but appears stalled. The maintainer-review items are small but block community contributions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*