# OpenClaw Ecosystem Digest 2026-05-08

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-08 06:18 UTC

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

# OpenClaw Project Digest — 2026-05-08

## 1. Today's Overview

The OpenClaw project is experiencing a period of **very high activity**, with 500 issues and 500 PRs updated in the last 24 hours, 168 PRs merged/closed, and one new release (v2026.5.7). The community is actively testing the latest release candidates, with a significant cluster of regression reports targeting gateway stability, Discord connectivity, and the recent codex-harness migration. Maintainers are responding quickly — numerous fix PRs were opened today targeting event-loop starvation, session recovery, and CLI output for automation. The project remains in a **responsive firefighting mode** following the v2026.5.x releases, balancing user-reported regressions against feature development.

## 2. Releases

**New release: [v2026.5.7](https://github.com/openclaw/openclaw/releases/tag/v2026.5.7)** — openclaw 2026.5.7

**Fixes included:**
- **ClawHub CLI dependency install retry:** transient failures during plugin publishing now retry automatically, reducing publish pipeline flakiness.
- **Preview-flake resilience:** plugins that pass all preview cells except one flaky cell remain publishable, preventing blocked releases.
- **Package version verification:** Every expected ClawHub package version is verified after publish, enabling faster recovery for maintenance releases and reducing the likelihood of silent half-published states.

**No breaking changes or explicit migration notes** accompany this release. It is a stability patch focused on the plugin publishing and CI/CD pipeline.

## 3. Project Progress

Today's merged/closed PRs (168 total) include several notable fixes:

- **[#79278](https://github.com/openclaw/openclaw/pull/79278)** — `perf(status): eliminate duplicate bundled-plugin manifest scans in status --json` — merged, addressing a performance regression that caused `openclaw status --json --all` to scan all 97 bundled plugin manifests twice.
- **[#78679](https://github.com/openclaw/openclaw/pull/78679)** — `fix: recognize PI native API provider streams in embedded session stream resolution` — closes [#78661](https://github.com/openclaw/openclaw/issues/78661), fixing zero-token-usage reporting in embedded sessions using PI-native streams.
- **[#78780](https://github.com/openclaw/openclaw/pull/78780)** — `Harden browser download output writes` — merged, routing downloads through `writeExternalFileWithinRoot` for safer private staging and finalization.
- **[#54606](https://github.com/openclaw/openclaw/pull/54606)** — `Followup runner: thread followups using current message` — merges fix for [#54456](https://github.com/openclaw/openclaw/issues/54456), ensuring followup carries originating message ID.
- **[#48971](https://github.com/openclaw/openclaw/pull/48971)** — `fix(media): harden MIME type sanitization` — merged, rejecting trailing junk in MIME types instead of silently truncating.

Open PRs advancing today include gateway restart throttling ([#79181](https://github.com/openclaw/openclaw/pull/79181)), session store recovery from corrupted writes ([#77915](https://github.com/openclaw/openclaw/pull/77915)), and global loop breaker for agent sessions ([#79267](https://github.com/openclaw/openclaw/pull/79267)).

## 4. Community Hot Topics

The following issues and PRs generated the most discussion in the last 24 hours:

### Top Issues by Comment Activity

- **[#77668](https://github.com/openclaw/openclaw/issues/77668)** — **Discord gateway hang at 'awaiting gateway readiness'** (21 comments, 2 👍). A regression from v2026.5.3-1 on macOS. Community analysis isolated the failure to the Carbon Client lifecycle. Six duplicates closed. This is a high-priority blocker for Discord users.

- **[#12590](https://github.com/openclaw/openclaw/issues/12590)** — **`memoryFlush` fires only every other cycle** (19 comments). Open since February. Users have traced the root cause to a dedup logic bug in `shouldRunMemoryFlush`. A longstanding issue that may require architectural attention.

- **[#78407](https://github.com/openclaw/openclaw/issues/78407)** — **`openclaw doctor --fix` rewrites `openai-codex/*` to `openai/*`** (16 comments, 3 👍). The auto-migration during update caused ChatGPT-OAuth users to lose access. This is highly disruptive — locking out users who rely on Codex subscriptions.

- **[#65824](https://github.com/openclaw/openclaw/issues/65824)** — **Meta feature request bundle: 11 platform gaps** (15 comments, 1 👍). A consolidated list from an intensive daily user, audited against v2026.4.15. Demonstrates real-world usage friction across multiple dimensions.

### Top PRs

- **[#77153](https://github.com/openclaw/openclaw/pull/77153)** — `Highlight exec command risks in Web approvals` — labeled `clawsweeper:automerge`, building on shell command explainer work. Broadens safety UI for exec approvals.
- **[#79238](https://github.com/openclaw/openclaw/pull/79238)** — `Keep OpenAI Codex migrations on automatic runtime routing` — large (XL) PR addressing the very regression reported in [#78407](https://github.com/openclaw/openclaw/issues/78407). Expected to merge quickly.
- **[#77948](https://github.com/openclaw/openclaw/pull/77948)** — `fix: reuse plugin metadata snapshot for provider runtime loads` — improves warm provider path performance.

**Underlying needs:** Users are frustrated by regressions introduced by automated migrations and by long-standing bugs in core subsystems (memory, Discord gateway). The community is actively debugging and providing reproduction steps, signaling a mature user base invested in stability.

## 5. Bugs & Stability

**Critical regressions (fix PRs exist or are imminent):**

| Issue | Severity | Summary | Fix Status |
|-------|----------|---------|------------|
| [#78601](https://github.com/openclaw/openclaw/issues/78601) | **Critical** | Gateway liveness watchdog restarts gateway every few minutes on v2026.5.6; event-loop freezes of 23s+ | Closed — likely included in v2026.5.7 |
| [#77668](https://github.com/openclaw/openclaw/issues/77668) | **High** | Discord gateway hangs on macOS at "awaiting gateway readiness" | Six duplicates closed; root cause isolated to Carbon Client lifecycle |
| [#78407](https://github.com/openclaw/openclaw/issues/78407) | **High** | `doctor --fix` rewrites Codex model refs, locks out OAuth users | Fix in [#79238](https://github.com/openclaw/openclaw/pull/79238) |
| [#78502](https://github.com/openclaw/openclaw/issues/78502) | **High** | Google Gemini models 3.1 Pro & 2.5 Pro hang/timeout on main sessions | Reproduced on two versions; no fix PR yet |
| [#76315](https://github.com/openclaw/openclaw/issues/76315) | **High** | Gateway unstable under subagent load on Linux — WhatsApp 408 disconnects | Open, 6 comments |
| [#78846](https://github.com/openclaw/openclaw/issues/78846) | **Medium** | `[object Object]` in messages with Mistral thinking models | Closed; specific to Mistral provider |

**Other notable bugs:**
- **[#77374](https://github.com/openclaw/openclaw/issues/77374)** — Assistant messages disappear from Control UI after each new user message. Severity: High.
- **[#76562](https://github.com/openclaw/openclaw/issues/76562)** — High CPU + extreme RPC latency after upgrade from 2026.4.24 to 2026.4.29/2026.5.2. 4 👍.
- **[#71412](https://github.com/openclaw/openclaw/issues/71412)** — `stopChannel` abort-timeout leaves zombie task, blocking health-monitor restart.
- **[#50590](https://github.com/openclaw/openclaw/issues/50590)** — Sandbox mode resolves skills to global path instead of sandbox-local copy (closed).

**Observability:** The cluster of gateway stability bugs (event-loop starvation, watchdog restarts, zombie tasks) suggests a systemic issue with the gateway's task scheduling under load, particularly during subagent runs and tool calls. The v2026.5.7 release appears targeted at some of these, but [#78502](https://github.com/openclaw/openclaw/issues/78502) and [#76315](https://github.com/openclaw/openclaw/issues/76315) remain open.

## 6. Feature Requests & Roadmap Signals

**Most-upvoted active feature requests:**

- **[#10659](https://github.com/openclaw/openclaw/issues/10659)** — **Masked Secrets** (4 👍, 12 comments). Prevent agents from accessing raw API keys. Long-standing security request.
- **[#75739](https://github.com/openclaw/openclaw/issues/75739)** — **Codex harness migration bugs** (3 👍, 6 comments). Two related runtime-routing bugs from the canonical codex-harness migration.
- **[#13597](https://github.com/openclaw/openclaw/issues/13597)** — **Comprehensive AWS deployment guide** (3 👍). EC2, ECS, Lambda documentation requested.
- **[#13751](https://github.com/openclaw/openclaw/issues/13751)** — **Feishu plugin: remove overbroad contact permission** (2 👍). Privacy-focused improvement.
- **[#13583](https://github.com/openclaw/openclaw/issues/13583)** — **Pre-response enforcement hooks** (2 👍, 10 comments). Hard gates for mandatory tool-call policy rules.
- **[#78308](https://github.com/openclaw/openclaw/issues/78308)** — **Channel-mediated approval for MCP tool calls** (1 👍, 10 comments). Consent envelope pattern.

**Likely candidates for next release:**
- The **codex-harness migration fix** ([#79238](https://github.com/openclaw/openclaw/pull/79238)) is almost certain to ship in the next patch given community impact.
- **Plugin metadata snapshot reuse** ([#77948](https://github.com/openclaw/openclaw/pull/77948)) reduces warm path latency and is low-risk.
- **Session store recovery** ([#77915](https://github.com/openclaw/openclaw/pull/77915)) addresses crash/OOM data loss, likely to be merged.
- **Gateway restart throttling** ([#79181](https://github.com/openclaw/openclaw/pull/79181)) prevents infinite restart loops on Ubuntu.

Notably, the **masked secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)) and **MCP tool approval** ([#78308](https://github.com/openclaw/openclaw/issues/78308)) features have consistent community engagement and were raised by different authors independently, suggesting a broader demand for security hardening.

## 7. User Feedback Summary

**Pain points expressed today:**

1. **Regression fatigue** — Multiple users report "worked before, now fails" patterns, especially around the v2026.4.24 → v2026.5.x upgrade path. Users express frustration that previously fixed bugs (e.g., `thought_signature` error) regress in subsequent releases.
2. **Silent failures** — Issues like assistant messages disappearing from UI ([#77374](https://github.com/openclaw/openclaw/issues/77374)), missing replies in transcripts ([#76990](https://github.com/openclaw/openclaw/issues/76990)), and false `health --json` status ([#59287](https://github.com/openclaw/openclaw/issues/59287)) erode user trust.
3. **Migration anxiety** — The `doctor --fix` rewrite bug ([#78407](https://github.com/openclaw/openclaw/issues/78407)) is a concrete example of automated migration causing harm. Users want opt-in or preview before automated config changes.
4. **Channel parity gaps** — Telegram reaction handling ([#64752](https://github.com/openclaw/openclaw/issues/64752)), Slack Block Kit ([#12602](https://github.com/openclaw/openclaw/issues/12602)), and iMessage typing indicators ([#10737](https://github.com/openclaw/openclaw/issues/10737)) are recurring themes.

**Positive signals:** The community is actively debugging and providing reproduction steps (e.g., raw-ws test isolation in [#77668](https://github.com/openclaw/openclaw/issues/77668)). The presence of detailed bug reports with root cause analysis indicates a technically skilled user base willing to invest in the project's health.

## 8. Backlog Watch

**Long-unanswered issues requiring maintainer attention:**

| Issue | Age | Comments | Summary |
|-------|-----|----------|---------|
| [#12590](https://github.com/openclaw/openclaw/issues/12590) | **90 days** (Feb 9) | 19 | `memoryFlush` fires every other cycle — dedup logic bug |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | **91 days** (Feb 6) | 12 | Masked secrets for agent API key protection (4 👍) |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) | **87 days** (Feb 10) | 8 | Backup/restore utility for config, cron, sessions |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | **88 days** (Feb 9) | 13 | Slack Block Kit support for agent messages |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | **87 days** (Feb 10) | 10 | Pre-response enforcement hooks (hard gates) |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) | **89 days** (Feb 8) | 6 | Webhook hook sessions don't reuse sessions for multi-turn |

**PRs needing maintainer review:**
- **[#69310](https://github.com/openclaw/openclaw/pull/69310)** — `fix: surface dropped media to users instead of silently swallowing` — open since April 20, labeled `needs-real-behavior-proof`. Addresses user-facing silent failure.
- **[#74974](https://github.com/openclaw/openclaw/pull/74974)** — `fix(gateway): tolerate Paperclip metadata on agent invocation payloads` — open since April 30, large PR blocking Paperclip integration.
- **[#69312](https://github.com/openclaw/openclaw/pull/69312)** — `fix: prevent MEDIA: false-positive extraction from indented code blocks` — open since April 20, affects code blocks in agent output.

**Notable orphaned issue:**
- **[#48874](https://github.com/openclaw/openclaw/issues/48874)** — RFC: Multi-Session Architecture (Shared LLM + Isolated Sessions). Last updated May 7 but no maintainer response visible. This architectural proposal has 6 comments and could inform future roadmap directions if acknowledged.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report — 2026-05-08

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is in a **hypergrowth phase**, with seven actively developed projects collectively processing **800+ issues and 750+ PRs** daily. The ecosystem is fragmenting around three architectural philosophies: monolithic reference implementations (OpenClaw), modular plugin-based agents (Hermes, IronClaw), and lightweight embedded assistants (NanoBot, PicoClaw). A significant **platform compatibility gap** persists—projects struggle with macOS-specific bugs (Hermes, OpenClaw), Docker deployment friction (ZeroClaw, Moltis), and Windows encoding issues (CoPaw). Community sentiment reveals **regression fatigue** as the dominant pain point, with users reporting "worked before, now broken" patterns across multiple projects following rapid release cycles. The ecosystem remains overwhelmingly **developer-driven**, with power users contributing reproduction steps and root-cause analysis rather than passive consumption.

## 2. Activity Comparison

| Project | Issues Updated (Open/Closed) | PRs Updated (Open/Merged) | Release Today | Health Score |
|---------|-----------------------------|---------------------------|---------------|--------------|
| **OpenClaw** | 500 (high) | 500 (168 merged) | ✅ v2026.5.7 | **Responsive firefighting** — high velocity, critical regressions being patched within hours |
| **Hermes Agent** | 50 (36 open) | 50 (10 merged) | ✅ v0.13.0 landed yesterday | **Strong** — major release shipped, 295 contributors, but P1 bugs lingering 11–16 days |
| **NanoBot** | 9 (3 open) | 20 (7 merged) | ❌ | **Healthy** — balanced bug fixes and features, maintainer bandwidth evident |
| **PicoClaw** | 33 (11 open) | 48 (28 merged) | ✅ Nightly build | **High velocity** — 28 PRs merged/day, rapid bug closure |
| **NanoClaw** | 9 (4 open) | 35 (22 merged) | ❌ | **Fast iteration** — 22 PRs merged, A2A routing stabilization push |
| **NullClaw** | 5 (3 open) | 8 (5 merged) | ❌ | **Moderate** — steady progress, ACP adapter merged, documentation gaps remain |
| **IronClaw** | 21 (14 open) | 50 (32 merged) | ✅ v0.28.0 | **Transformative** — Reborn refactor on main, but nightly E2E broken |
| **LobsterAI** | 2 (2 open) | 50 (43 merged) | ✅ v2026.5.7 | **Merge surge** — 43 PRs merged, login blocker remains critical |
| **CoPaw** | 36 (21 open) | 29 (20 merged) | ❌ | **Active** — strong UX focus, memory leak and performance regression pressing |
| **Moltis** | 4 (0 open) | 9 (9 merged) | ✅ 2 releases today | **Lean & responsive** — all bugs fixed within 24 hours of reporting |
| **TinyClaw** | — | — | ❌ | **Inactive** — no activity in 24h |
| **ZeptoClaw** | — | — | ❌ | **Inactive** — no activity in 24h |
| **ZeroClaw** | 50 (high) | 50 (2 merged) | ✅ v0.7.5 | **Release-rich, bug-heavy** — major UX features shipped, 6+ S1 blockers open |

## 3. OpenClaw's Position

**Advantages over peers:**
- **Largest community by orders of magnitude** — 500 daily issues/PRs vs. 20–50 for peers. This translates to faster bug identification and broader plugin ecosystem.
- **Mature CI/CD pipeline** — v2026.5.7 shipped within hours of regression reports (gateway watchdog, event-loop starvation). No other project demonstrates this release cadence.
- **Deepest plugin infrastructure** — 97 bundled plugins, ClawHub publishing with retry logic and version verification. Rival projects (CoPaw, NanoBot) are still debating which MCPs to ship built-in.
- **Codex-harness migration** — While controversial (causing [#78407](https://github.com/openclaw/openclaw/issues/78407)), this architectural shift positions OpenClaw for multi-provider routing. Rivals like NanoBot and PicoClaw are still on single-provider or early multi-provider stacks.

**Technical approach differences:**
- **Monolithic core + plugin architecture** — OpenClaw maintains a single reference binary with plugin extensions. In contrast, IronClaw is pursuing a WASM-based modular runtime (Reborn), and Moltis uses Ed25519 node identity for decentralized agent-to-agent communication.
- **Gateway stability is the Achilles' heel** — The cluster of event-loop starvation, watchdog restarts, and zombie tasks ([#78601](https://github.com/openclaw/openclaw/issues/78601), [#77668](https://github.com/openclaw/openclaw/issues/77668), [#71412](https://github.com/openclaw/openclaw/issues/71412)) is systemic. NanoBot and CoPaw face similar WebSocket/gateway issues at smaller scale, suggesting this is an unsolved industry problem.
- **Migration automation is aggressive** — The `doctor --fix` rewrite bug ([#78407](https://github.com/openclaw/openclaw/issues/78407)) is unique to OpenClaw's scale but reflects a broader industry tension between convenience and user control.

**Community size comparison:**
- OpenClaw's daily activity (500 issues/PRs) exceeds the combined total of all other projects tracked (~280). Hermes Agent (295 contributors since last release) is the nearest rival in contributor base, but at 50 daily issues/PRs, it operates at 10% of OpenClaw's throughput.

## 4. Shared Technical Focus Areas

Requirements emerging across multiple projects, ranked by cross-project frequency:

| Focus Area | Affected Projects | Specific Needs |
|------------|------------------|----------------|
| **Gateway/WebSocket stability** | OpenClaw, NanoBot, Hermes, CoPaw, ZeroClaw | macOS-specific hangs (OpenClaw #77668, Hermes #21613), silent disconnects (Hermes #21633, ZeroClaw #6246), event-loop starvation under load (OpenClaw #78601, CoPaw #4105) |
| **Session state management** | Hermes, NanoBot, OpenClaw, CoPaw, ZeroClaw | Session loss on interrupt (NanoBot #3689), history loss after agent switch (CoPaw #3919), memory persistence bugs (OpenClaw #12590), zombie tasks blocking restart (OpenClaw #71412) |
| **Provider routing & fallback** | OpenClaw, Hermes, ZeroClaw, CoPaw | Codex→OpenAI migration breakage (OpenClaw #78407), local provider fallback to OpenRouter (Hermes #16623), fallback credential inheritance failure (ZeroClaw #6418), DeepSeek integration fragility (NanoBot #3665, CoPaw #4051) |
| **Tool/approval UI safety** | OpenClaw, Hermes, ZeroClaw, CoPaw | MCP approval no-ops (Hermes #21563), CLI prompt freezing (Hermes #13951), backend-only approval lacking web UI (ZeroClaw #6522), shell tool dispatch blocked at full autonomy (ZeroClaw #6434) |
| **Channel reliability & parity** | OpenClaw, CoPaw, ZeroClaw, Hermes | WeChat message loss (CoPaw #4056, OpenClaw #76315), WhatsApp protocol breaks (ZeroClaw #6246), Telegram reaction gaps (OpenClaw #64752), missing typing indicators across channels |
| **Docker/container deployment** | ZeroClaw, Moltis, Hermes, CoPaw | Dashboard shadowed by bind mount (ZeroClaw #6400), browser sandbox failure in Docker (Moltis #977), Node version conflicts (Hermes #21656), data migration failures (CoPaw #4101) |

**Underlying pattern**: The ecosystem is converging on a **multi-provider, multi-channel, multi-session** architecture, but every project independently rediscovers the same set of failure modes. A shared reference implementation for gateway state machines and session stores could save significant duplicated debugging effort.

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | IronClaw | Moltis | NanoBot | NullClaw | ZeroClaw |
|-----------|----------|--------------|----------|--------|---------|----------|----------|
| **Primary Use Case** | Universal assistant (desktop, channels, API) | Developer agent (CLI, ACP, multi-agent) | Enterprise sandboxed agent (WASM, Reborn) | Voice/telephony agent | Lightweight multi-channel agent | Minimalist Zig-native agent | Desktop-first consumer agent |
| **Target User** | Power users, plugin developers | AI engineers, DevOps | Enterprise dev teams | Telephony/voice developers | Everyday chat users | Systems programmers | Non-technical users |
| **Language** | Rust (core) + Python (plugins) | Python | Rust (WASM runtime) | Rust | Python (backend) + JS (frontend) | Zig | Rust + Tauri (desktop) |
| **Key Architectural Choice** | Monolithic + plugin registry | Brain control plane + subagents | WASM tool runtime (Reborn) | Ed25519 node identity (TOFU) | Auth CLI + provider abstraction | Native ACP stdio adapter | JSON-schema onboarding + per-property CRUD |
| **Channel Breadth** | 25+ (Discord, Slack, WeChat, etc.) | 15+ (Telegram, Discord, QQ) | 10+ (Slack, Telegram, WeChat) | 8+ (Telephony, WhatsApp, voice) | 10+ (Telegram, Discord) | 5+ (Telegram, Lark) | 10+ (WhatsApp, Telegram, desktop) |
| **Risk Tolerance** | High (rapid releases, aggressive migrations) | Medium (major releases every 2-3 weeks) | High (full Reborn refactor on main) | Low (bugs fixed within 24h) | Medium (balanced feature/bug cycle) | Low (conservative, docs-focused) | High (v0.7.5 shipped with E2E broken) |
| **Operational Maturity** | Advanced: CI/CD, publishing pipeline, deprecation warnings | Advanced: 588 PRs in one release, detailed severity tracking | Rebuilding: Reborn introduces new operational model | Early: No release notes, low community engagement | Growing: Auth CLI reduces setup friction | Early: README accuracy gaps, no release pipeline | Improving: Schema-driven config, but Docker/secret mgmt raw |

**Key insight**: The market is splitting into **three tiers** — developer assistants (Hermes, NullClaw), enterprise sandboxed agents (IronClaw), and general-purpose assistants (OpenClaw, CoPaw, ZeroClaw). Projects in the latter tier are converging on a **minimum viable channel set** (WeChat, WhatsApp, Telegram, Discord) but diverge sharply on UX philosophy (ZeroClaw: desktop-first onboarding vs. OpenClaw: CLI/API-first).

## 6. Community Momentum & Maturity

### Tier 1: Hypergrowth (>100 daily updates)
- **OpenClaw** — Dominates by raw volume. In responsive firefighting mode; regressions fixed within hours. **Risk**: Regression fatigue may erode trust. **Velocity**: Very high.
- **CoPaw** — 36 issues + 29 PRs daily, strong UX feature pipeline. **Risk**: Memory leak (#4105) and UI lag (#4108) are growing concerns. **Velocity**: High.

### Tier 2: High Growth (20–50 daily updates)
- **Hermes Agent** — Shipped v0.13.0 with 588 PRs. Well-organized maintenance (P0/P1/P2 severity). **Risk**: 11–16 day lag on P1 bugs (#13951, #16623) suggests maintainers stretched thin. **Maturity**: High.
- **IronClaw** — Reborn refactor is a massive architectural bet. 32 PRs merged today, but nightly E2E fails. **Risk**: Integration debt may compound. **Maturity**: Medium (transitioning).
- **ZeroClaw** — Shipped v0.7.5 with significant UX improvements but 6+ S1 blockers open. **Risk**: Feature velocity outpacing stability. **Maturity**: Medium.
- **LobsterAI** — 43 PRs merged in a surge, login bug (#1903) blocks paying users. **Risk**: Auth failure undermines monetization. **Velocity**: Very high (today only).

### Tier 3: Steady State (5–20 daily updates)
- **NanoBot** — Balanced 20 PRs, 9 issues. Healthy maintainer bandwidth. **Maturity**: High for project size.
- **PicoClaw** — 48 PRs updated, nightly builds. **Maturity**: Medium (stable release cadence, but LLM retry bug #629 unresolved for 75 days).
- **NanoClaw** — Rapid PR merges (22 today), low community discussion. **Maturity**: Early (A2A routing still stabilizing).

### Tier 4: Low Activity (0–5 daily updates)
- **NullClaw** — 8 PRs, 5 issues. Steady but low-volume. **Maturity**: Early (ACP adapter is a notable architectural win).
- **Moltis** — 9 PRs merged, all bugs fixed within 24 hours. **Maturity**: High responsiveness but low community engagement.
- **TinyClaw, ZeptoClaw** — Dormant.

## 7. Trend Signals

### 1. Multi-Agent Orchestration Is the Next Battleground
Hermes (subagent delegation, closed Brain feature), NanoClaw (A2A routing), and Moltis (Ed25519 node identity) are all investing in agent-to-agent communication. OpenClaw has no visible multi-agent architecture, a potential competitive gap. **Takeaway**: Support for recursive, delegated, or swarm-based agent topologies will differentiate projects in 2026–2027.

### 2. Security Hardening Is Lagging Behind Feature Velocity
Masked secrets (OpenClaw #10659, 91 days open), MCP approval no-ops (Hermes #21563), and backend-only tool approval (ZeroClaw #6522) are all unresolved. Users are requesting **pre-response enforcement hooks** (OpenClaw #13583) and **consent envelope patterns** (OpenClaw #78308). **Takeaway**: Security features are not keeping pace with agent autonomy; expect regulatory and enterprise pressure to force prioritization.

### 3. Local-First vs. Cloud-Native Is a Core Tension
Users with local OpenAI-compatible setups (LM Studio, Ollama) report provider routing failures across Hermes (#16623), NanoBot (#3665), and ZeroClaw (#6399). At the same time, cloud integration (Gmail, OAuth, Codex) introduces fragility from automated migrations (OpenClaw #78407). **Takeaway**: A robust "local detection → local provider → cloud fallback" chain is table stakes. Projects that solve this cleanly will win on-premise and enterprise adoption.

### 4. Platform-Specific Debugging Is an Unsolved Tax
macOS (OpenClaw #77668, Hermes #21613, #21623), Windows (CoPaw #1909, ZeroClaw #6410, CoPaw #4103), and Docker (ZeroClaw #6400, Moltis #977, Hermes #21656) each introduce unique failure modes. No project has a cross-platform CI/CD that catches these. **Takeaway**: Investment in platform-specific CI (macOS runners, Windows test suites, Docker Compose E2E) is a high-ROI differentiator.

### 5. The "Dream" / Adaptive Agent Tradeoff Is Emerging
NanoBot's "Dream" feature—an adaptive agent that learns from user interactions—is polarizing. Users explicitly request disable toggles (#3652). OpenClaw's "memoryFlush" bug (#12590) and CoPaw's OpenClaw-inspired compounding value proposal (#578) suggest the industry is debating **how much agency** an assistant should have. **Takeaway**: Configurable agent personality (adaptive vs. deterministic) will become a standard UX requirement, not an edge case.

### 6. Desktop Parity Is the New Baseline
ZeroClaw (#6329, #6339, #6465), CoPaw (#2235), and OpenClaw (Control UI) are all investing in desktop clients with native tray icons, offline capability, and system-level integration. The CLI-only era is ending; users expect a **persistent, always-on desktop companion**. **Takeaway**: Projects without a desktop story (NullClaw, NanoBot minimally) will be relegated to server-side or embedded use cases.

### 7. Regression Fatigue Is a Retention Risk
OpenClaw (#78407 "Codex migration broke OAuth"), Hermes (#16623 "local provider reverts to OpenRouter"), and CoPaw (#4108 "new version UI lag") all exhibit `worked before` → `now broken` patterns. Users express distrust: "previously fixed bugs regress." **Takeaway**: Feature gates, opt-in migrations, and canary releases are no longer nice-to-haves—they are essential for user trust. The project that prioritizes **stability SLAs** will capture the most conservative enterprise segment.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-08

## Today's Overview

Project activity remains very high. In the last 24 hours, 20 pull requests were updated (13 open, 7 merged/closed) and 9 issues saw updates (3 currently open, 6 recently closed). No new releases were published. The community is actively contributing across channels, memory systems, and configuration improvements, while several websocket and DeepSeek integration bugs are being resolved. A clear balance between bug fixes and feature development suggests healthy maintainer bandwidth.

## Releases

No new releases.

## Project Progress

Seven pull requests were merged or closed in the past 24 hours:

- **#3691** and **#3690** — Two identical fixes (cherry-pick to main) resolving onboard wizard input-handling bugs where empty strings and falsy values were incorrectly rejected. This improves the first-run configuration experience.
- **#3221** — Adds a `nanobot auth` CLI command with OAuth Device Flow support and automatic default provider/model configuration, enabling a streamlined "nanobot agent" startup after authentication. Token storage is added to `~/.nanobot/auth.json`.
- **#3608** — Documentation and example configuration for "Sen," a local agent setup. No runtime code changes.
- **#3660** — Fixes Dream's cursor state tracking so restores correctly roll back memory alongside the cursor. Includes a regression test.
- **#3677** — Removes HTTP compression (gzip) from the API layer's SSE streaming endpoints, fixing a bug where streaming appeared batched instead of real-time incremental.
- **#1835** — Enables sending arbitrary additional arguments to backend LLMs (e.g., `"stream": false` for Ollama), increasing flexibility for downstream providers.

Five other PRs saw updates today but remain open, notably work on WeChat message reliability (#3684), memory consolidation fixes (#3687), and a unified summary buffer for archiving (#3686).

## Community Hot Topics

Most commented issues:

- **Issue #3682** (3 comments) — Websocket handshake failure ("opening handshake failed") on NanoBot gateway. The user reports errors originating from `websockets/http11.py`. This is the most active open stability issue.
- **Issue #3650** (2 comments) — Feature request to configure bot name and icon in agent mode. Users want to see "mybot is thinking..." with a custom logo rather than the default cat image. Proposal: a `config.json` setting for `botName`.
- **Issue #3652** (2 comments) — Request to completely disable the Dream feature via an `enabled` flag in Dream config. User reports wanting full control over agent behavior without Dream interfering.

The underlying needs center on **configuration flexibility** (branding, feature toggles) and **reliability** (websocket errors affect multiple users).

## Bugs & Stability

Reported bugs ranked by severity:

1. **Critical — #3682 (CLOSED): Websocket handshake crash.** Gateway fails with "opening handshake failed" traceback. User `NewAlice` encountered it on Linux server with Windows/Mac clients. Likely affects cross-platform deployments. Resolved by user or maintainer.
2. **High — #3665 (CLOSED): DeepSeek-V4 Flash reasoning_content error.** After a few queries, the API rejects requests: "The reasoning_content in the thinking mode must be passed back to the API." This is a provider-specific integration bug affecting users of DeepSeek's thinking mode. Closed without clear root cause published.
3. **Medium — #3681 (CLOSED): LLM timeout after 300 seconds.** User reports frequent "Error calling LLM: timed out after 300s" errors. May be network-related or provider-side, but user suspects NanoBot. Version 0.1.5.post3 on Windows.
4. **Medium — #3689 (OPEN): Session history lost on interrupt.** When user interrupts a reasoning loop, NanoBot forgets the previous conversation context. Bug report suggests context summarization is not persisting the interrupted state. No fix PR yet.
5. **Low — #3604 (CLOSED): WhatsApp voice message not downloaded.** Audio attachment processing fails; user cannot transcribe via OpenAI/Groq. Fixed in other recent PRs? Not explicitly.

## Feature Requests & Roadmap Signals

- **#3650 — Bot name and icon configuration.** Strong demand for white-labeling in agent mode. Likely candidates for next minor release given PR activity around config systems.
- **#3652 — Disable Dream.** A simple `enabled` flag toggle. Low implementation complexity, high desirability for users who want a non-adaptive agent.
- **#3358 (OPEN PR) — Model presets.** A sophisticated feature enabling named bundles of model parameters for quick switching. Still open after 17 days; may land in v0.2.
- **#3513 (OPEN PR) — Unified transcription providers + local Whisper.** Addresses unreliable voice transcription. Nearing completion with community testing.
- **#3486 (OPEN PR) — SimpleX channel integration.** New messaging channel for privacy-focused users. Significant scope but actively maintained.
- **#3655 (OPEN PR) — CLI reasoning content display.** Shows model thinking during streaming via `show_reasoning` config option. TUI duplication fix included.

Predictions for next version: Expect model presets, Dream disable toggle, and CLI reasoning display to be merged. Keep an eye on SimpleX channel and unified transcription for v0.2.

## User Feedback Summary

**Positive signals:** Community is actively contributing code and documentation (20 PRs). The auth command (#3221) and model presets (#3358) address long-standing setup friction. Users appreciate the project's breadth of channel support.

**Pain points:** Repeated websocket issues across platforms (#3682, #3683), DeepSeek integration fragility (#3665), and session context loss (#3689) are the clearest dissatisfaction areas. WhatsApp voice failure (#3604) and LLM timeouts (#3681) indicate reliability gaps in production deployments. The "Dream" feature, while innovative, frustrates some users who prefer predictable agent behavior (#3652). Users also want more branding control (#3650).

**Underlying needs:** Cross-platform reliability, provider-specific bug handling for popular models, and user-configurable agent personality/settings.

## Backlog Watch

Items needing maintainer attention:

- **PR #1219 (OPEN since Feb 26)** — Adds stock market analysis, code performance analysis, and test case generation skills. Extensive documentation included. No activity for ~2 months despite being large and well-structured. May conflict with newer agent architecture.
- **PR #1443 (OPEN since Mar 2)** — Decouples heartbeat reasoning from notification with `sendReasoning` config. Long-standing enhancement that could improve silent agent behavior. Stalled.
- **Issue #3652 (OPEN, 2 days old)** — Dream disable request. Simple, popular, but has no dedicated PR yet.
- **Issue #3689 (OPEN, created today)** — Session history loss on interrupt. No fix PR exists; the reporter seems frustrated. This is a high-impact UX bug for production users.

**Maintainer attention summary:** Two long-dormant PRs (1219, 1443) may need triage to accept, reject, or request rebasing. The Dream disable request (#3652) and session loss bug (#3689) are low-complexity issues that could yield quick wins for community satisfaction.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-08

## 1. Today’s Overview

Hermes Agent remains highly active with 50 issues and 50 pull requests updated in the last 24 hours. Of those, 36 issues are open/active and 14 were closed; 40 PRs are open and 10 were merged or closed. A major new release, **v0.13.0 (v2026.5.7) “The Tenacity Release”**, landed yesterday, bringing 588 merged PRs and 282 closed issues since v0.12.0. The project shows strong community engagement (295 contributors since last release) and a steady pipeline of bug fixes, features, and infrastructure improvements. Today’s activity spans critical P1/P2 bug reports, feature requests, and several open PRs addressing long-standing stability issues.

## 2. Releases

**New release: [v0.13.0 (v2026.5.7) – The Tenacity Release](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.5.7)**  
*Released May 7, 2026*

**Changes since v0.12.0:**  
- 864 commits · 588 merged PRs · 829 files changed · 128,366 insertions  
- 282 issues closed (13 P0, 36 P1)  
- 295 community contributors (including co-authors)  

**Notable changes (from release notes, not fully listed in data):**  
- Emphasis on agent resilience and task completion (“finishes what i[t] starts”)  
- Likely includes many of the features and fixes seen in the backlog (e.g., Brain control plane, friction analyzer, autonomy tracker)  

**Breaking changes:** The release notes are truncated in the data; no explicit migration notes are visible. Given the large number of changes, users upgrading from v0.12.0 should consult the [full release notes](https://github.com/NousResearch/hermes-agent/releases/tag/v2026.5.7) for potential schema or config migrations.

## 3. Project Progress

In the last 24 hours, **10 PRs were merged or closed**. The available top-20 PR list shows only one closed PR (#21700, a trivial placeholder). However, the high merged/closed count suggests several important fixes landed, including:

- Likely fixes for issues addressed by open PRs that may have been merged today (not shown in the truncated list).  
- The release v0.13.0 itself was likely completed earlier this week, but today’s merged PRs may include post-release hotfixes.  

Notable **open PRs that indicate progress toward future merges**:

- [#21704](https://github.com/NousResearch/hermes-agent/pull/21704) – Adds zh-CN documentation translations across skills, plugins, and MLOps  
- [#21703](https://github.com/NousResearch/hermes-agent/pull/21703) – Fixes stale Ollama credentials after provider switch  
- [#21702](https://github.com/NousResearch/hermes-agent/pull/21702) – Adds dashboard `/api/local-token` and `/health` endpoints  
- [#21701](https://github.com/NousResearch/hermes-agent/pull/21701) – Adds Hermes User-Agent attribution for GMI requests  
- [#21696](https://github.com/NousResearch/hermes-agent/pull/21696) – Fixes `mcp_` prefix drop in tool call repair  
- [#21695](https://github.com/NousResearch/hermes-agent/pull/21695) – Wires API-key model-provider plugins into runtime  
- [#21694](https://github.com/NousResearch/hermes-agent/pull/21694) – Adds Google Places API (New) integration  
- [#21683](https://github.com/NousResearch/hermes-agent/pull/21683) – Guards BlueBubbles sends with contact book validation  

These PRs span documentation, provider stability, dashboard improvements, tool integrations, and security.

## 4. Community Hot Topics

The most active issues and pull requests (by comment count) reveal key areas of user interest and frustration:

| Item | Type | Comments | Reactions | Key Topic |
|------|------|----------|-----------|-----------|
| [#20842](https://github.com/NousResearch/hermes-agent/issues/20842) | Bug (closed) | 6 | 0 👍 | Kanban migration SQLite schema error after auto-update |
| [#13951](https://github.com/NousResearch/hermes-agent/issues/13951) | Bug (open, P1) | 3 | 2 👍 | CLI approval prompt frozen due to background output flooding |
| [#21686](https://github.com/NousResearch/hermes-agent/issues/21686) | Feature (open) | 2 | 0 👍 | Walk CLAUDE.md / AGENTS.md to git root for project-local skills |
| [#21563](https://github.com/NousResearch/hermes-agent/issues/21563) | Bug (open) | 2 | 0 👍 | MCP approval tools are no-ops (no IPC channel) |
| [#21558](https://github.com/NousResearch/hermes-agent/issues/21558) | Bug (closed) | 2 | 0 👍 | Same root cause as #21563 – approvals subsystem broken |
| [#21658](https://github.com/NousResearch/hermes-agent/issues/21658) | Bug (open, P1) | 2 | 0 👍 | Subagent tool delegation inconsistent despite correct `toolsets` |
| [#21656](https://github.com/NousResearch/hermes-agent/issues/21656) | Bug (open, P2) | 2 | 0 👍 | Docker/install.sh Node version mismatch breaks web build |

**Analysis:** The most discussed issue (#20842, Kanban migration failure) was already closed, likely fixed. The P1 CLI unresponsiveness (#13951) continues to draw user votes and comments. The MCP approvals gap (#21563/#21558) was partially addressed but remains a pain point. The subagent tool delegation bug (#21658) is a new P1 reported today, indicating a regression or uncovered edge case.

## 5. Bugs & Stability

**Critical / P1 bugs reported or updated today (2026-05-08):**

| Issue | Title | Status | Impact |
|-------|-------|--------|--------|
| [#13951](https://github.com/NousResearch/hermes-agent/issues/13951) | CLI approval prompt unresponsive (background output flooding) | Open | Blocks dangerous command approvals; terminal freezes |
| [#21658](https://github.com/NousResearch/hermes-agent/issues/21658) | Subagent tool delegation inconsistent – file/terminal tools missing | Open | Breaks multi-agent workflows when delegating with specific toolsets |
| [#13971](https://github.com/NousResearch/hermes-agent/issues/13971) | `_is_ollama_glm_backend()` false positive causes spurious truncation | Open | Local API proxies incorrectly trigger truncation continuation, wasting tokens |
| [#16623](https://github.com/NousResearch/hermes-agent/issues/16623) | Explicit local OpenAI-compatible config still resolves to OpenRouter | Open | Provider routing broken for local LM Studio setups |

**P2 bugs:**

| Issue | Title | Status | Notes |
|-------|-------|--------|-------|
| [#21656](https://github.com/NousResearch/hermes-agent/issues/21656) | Docker/install.sh Node version conflict (20 vs 22) | Open | Blocks web asset builds on Debian 13.4 |
| [#21566](https://github.com/NousResearch/hermes-agent/issues/21566) | Auxiliary LLM calls use short 30s timeout – causes retry storms on slow local inference | Open | Affects session_search, skills_hub; no local-endpoint detection |
| [#21666](https://github.com/NousResearch/hermes-agent/issues/21666) | `hermes acp` triggers OpenAI safety refusal on greeting with OpenRouter mini-class models | Open | System-prompt mismatch between `acp` and `chat`/`-z` |
| [#21633](https://github.com/NousResearch/hermes-agent/issues/21633) | QQ Bot WebSocket silently dies – no reconnection after heartbeat timeout | Open | Bot goes offline without logs |
| [#21623](https://github.com/NousResearch/hermes-agent/issues/21623) | `@` autocomplete freezes in tmux on macOS | Open | CPU spike, terminal freeze |
| [#21613](https://github.com/NousResearch/hermes-agent/issues/21613) | macOS Telegram gateway lock start_time=null – PID reuse false positives | Open | Prevents gateway startup after crash |
| [#21596](https://github.com/NousResearch/hermes-agent/issues/21596) | Stale platform-lock detection broken on macOS – PID reuse causes permanent startup failure | Open | Same root cause as #21613 |

**Fixes in progress (open PRs addressing bugs above or related):**

- [#21703](https://github.com/NousResearch/hermes-agent/pull/21703) – Fixes stale Ollama credentials after provider switch (related to #16623 provider routing)  
- [#21696](https://github.com/NousResearch/hermes-agent/pull/21696) – Fixes `mcp_` prefix drop in tool call repair (addresses MCP tool naming errors)  
- [#14407](https://github.com/NousResearch/hermes-agent/pull/14407) – Validates tool calls before persisting (prevents session poisoning, related to #20001)  
- [#11927](https://github.com/NousResearch/hermes-agent/pull/11927) – Invalidates LRU cache on skill file deletion (phantom skill entries)  

**Overall stability assessment:** Today saw multiple new P2 bugs related to platform-specific lock files (macOS), WebSocket reliability, and API compatibility. The MCP approvals subsystem (P2) remains broken in practice despite a closed issue (#21558) – the real fix may still be pending. The provider routing bug (#16623) and CLI unresponsiveness (#13951) are long-standing P1s that need attention.

## 6. Feature Requests & Roadmap Signals

**Notable feature requests opened or updated today:**

| Issue | Title | Type | Likelihood for v0.14.0 |
|-------|-------|------|------------------------|
| [#21686](https://github.com/NousResearch/hermes-agent/issues/21686) | Walk CLAUDE.md / AGENTS.md to git root + auto-discover project-local skills | Feature (P3) | High – aligns with agent context awareness improvements |
| [#21637](https://github.com/NousResearch/hermes-agent/issues/21637) | Per-channel personality and model routing (extend channel_prompts) | Feature (P3) | Medium – requested by power users of gateway |
| [#21642](https://github.com/NousResearch/hermes-agent/issues/21642) | Dashboard: profile-scoped config not visible in web UI | Feature (P3) | Medium-high – improves multi-profile management |
| [#21625](https://github.com/NousResearch/hermes-agent/issues/21625) | Add skill execution log (how to check if skill has been executed) | Feature (P3) | Medium – developer experience |
| [#19164](https://github.com/NousResearch/hermes-agent/issues/19164) | Recursive Multi-Agent Systems | Feature (P3) | Low – requires architectural changes, but linked to RecursiveMAS research |
| [#17067](https://github.com/NousResearch/hermes-agent/issues/17067) | Fallback models for auxiliary/web_extract | Feature (P3) | Medium – reliability improvement for slow models |

**Roadmap signals from PRs:**  
- [#21699](https://github.com/NousResearch/hermes-agent/pull/21699) – Control-plane canary cockpit for WebUI (HERA-198) – suggests upcoming operational tooling for “Brain”  
- [#20515](https://github.com/NousResearch/hermes-agent/pull/20515) – Tailscale Serve identity auth for dashboard – security enhancement  
- [#21694](https://github.com/NousResearch/hermes-agent/pull/21694) – Google Places API (New) integration – new tool expansion  

The “Brain” control plane issues (#12350-12345) are all **closed**, indicating that the feature has been implemented and rolled out in recent releases (likely part of v0.13.0). This suggests the roadmap is shifting toward peripheral improvements (auth, dashboard, more tools, localization).

## 7. User Feedback Summary

**Pain points expressed today:**

- **CLI instability:** The approval prompt freeze (#13951) and `@` autocomplete freeze (#21623) frustrate terminal users, especially on macOS/tmux.  
- **Inconsistent tool delegation:** Subagents not receiving files/terminal tools despite correct parameters (#21658) undermines the multi-agent value proposition.  
- **MCP approvals broken:** Users trying to use MCP bridges for permissions management find the tools non-functional (#21563, #21558).  
- **Provider routing confusion:** Users with local OpenAI-compatible setups (LM Studio) report that Hermes reverts to OpenRouter (#16623), causing unexpected costs or failures.  
- **Docker build friction:** The Node version mismatch (#21656) breaks containerized deployments.  
- **Platform-specific issues:** macOS users face PID reuse bugs for Telegram and generic locks (#21613, #21596), making gateway unreliable.  

**Satisfaction signals:**  
- 295 community contributors since the last release indicates strong engagement and willingness to contribute fixes.  
- The release of v0.13.0 with 588 merged PRs shows the team is shipping rapidly.  
- Users are opening thoughtful feature requests (e.g., #21686 on AGENTS.md discovery, #21637 on per-channel routing) that suggest active real-world usage.

## 8. Backlog Watch

The following issues and PRs have been open for an extended period (≥2 weeks) and may require maintainer attention:

| Item | Author | Opened | Last Updated | Reason for Watch |
|------|--------|--------|--------------|------------------|
| [#13951](https://github.com/NousResearch/hermes-agent/issues/13951) (bug, P1) | W-W-Go | 2026-04-22 | 2026-05-08 | CLI freezing; high user reaction (2 👍); no fix PR yet |
| [#13971](https://github.com/NousResearch/hermes-agent/issues/13971) (bug, P1) | xzmzm | 2026-04-22 | 2026-05-08 | Spurious truncation for local proxies; affects many Ollama/OAI users |
| [#16623](https://github.com/NousResearch/hermes-agent/issues/16623) (bug, P1) | syukouyuu | 2026-04-27 | 2026-05-08 | Local provider routing always falls back to OpenRouter – fundamental reliability issue |
| [#17067](https://github.com/NousResearch/hermes-agent/issues/17067) (feature, P3) | mr-gila | 2026-04-28 | 2026-05-08 | Fallback models for auxiliary tasks – multiple comments, no movement |
| [#18793](https://github.com/NousResearch/hermes-agent/issues/18793) (bug, P3) | y0shua1ee | 2026-05-02 | 2026-05-08 | Hardcoded model name in image_gen plugin – breaks third-party backends |
| [#19164](https://github.com/NousResearch/hermes-agent/issues/19164) (feature, P3) | yepyhun | 2026-05-03 | 2026-05-08 | Recursive multi-agent – interesting but needs design discussion |
| PR [#11927](https://github.com/NousResearch/hermes-agent/pull/11927) (fix, P2) | Bartok9 | 2026-04-18 | 2026-05-08 | Phantom skill entries – rebased but not merged |
| PR [#11877](https://github.com/NousResearch/hermes-agent/pull/11877) (feature, P3) | Bartok9 | 2026-04-18 | 2026-05-08 | Friction analyzer – large feature, may need review |
| PR [#11879](https://github.com/NousResearch/hermes-agent/pull/11879) (feature, P3) | Bartok9 | 2026-04-18 | 2026-05-08 | Autonomy tracker – similar status |
| PR [#11925](https://github.com/NousResearch/hermes-agent/pull/11925) (fix, P2) | Bartok9 | 2026-04-18 | 2026-05-08 | Falsey tool results in ACP – core correctness issue |
| PR [#11926](https://github.com/NousResearch/hermes-agent/pull/11926) (fix, P2) | Bartok9 | 2026-04-18 | 2026-05-08 | OPENAI_BASE_URL vs config.yaml conflict |

**Notable:** Several P1 bugs (#13951, #13971, #16623) have been open for 11–16 days with no assigned fix PR. The author Bartok9 has submitted multiple high-quality PRs (some open for 20 days) that address important stability issues but remain unmerged. These long-open items could indicate maintainer bandwidth constraints or prioritization of the v0.13.0 release. After the release, these should be re-evaluated for merging.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-08

## 1. Today's Overview
PicoClaw continues to see **high development velocity**, with 33 issues and 48 PRs updated in the last 24 hours. Of those, 22 issues were closed and 28 PRs were merged/closed, reflecting strong ongoing maintenance and feature delivery. A new **nightly build** (v0.2.8-nightly.20260508) was published, though it is marked as potentially unstable. The project is actively addressing bugs across providers, channels, and tools, while also pushing forward major enhancements like multi-agent discovery, Telegram media album handling, and model configuration workflow improvements.

## 2. Releases
A single new release was published today:
- **nightly** – *Nightly Build*  
  `v0.2.8-nightly.20260508.2834db13`  
  This is an automated build from the `main` branch and may be unstable.  
  **No breaking changes or migration notes** are indicated in the release notes.  
  Full changelog: [compare/v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)

## 3. Project Progress
In the last 24 hours, **28 PRs were merged or closed**, including several key dependency updates and one major refactor:

- **LINE Bot SDK v8 migration** – PR [#2413](https://github.com/sipeed/picoclaw/pull/2413) replaced hand-rolled HTTP/HMAC/JSON code with the official `line-bot-sdk-go`, reducing maintenance burden.
- **Dependency bumps** – Multiple automated PRs updated frontend dependencies: `i18next` (v26.0.8 → v26.0.10), `react-i18next` (v17.0.4 → v17.0.6), `globals` (v17.5.0 → v17.6.0), `@tabler/icons-react` (v3.41.1 → v3.43.0), `shadcn` (v4.3.0 → v4.7.0), and `fyne.io/systray` (v1.12.0 → v1.12.1).
- **Ongoing open PRs** advancing feature work: multi-agent discovery prompt ([#2158](https://github.com/sipeed/picoclaw/pull/2158)), Slack webhook output channel ([#2719](https://github.com/sipeed/picoclaw/pull/2719)), and several fixes by contributor `bogdanovich` around tool feedback throttling, async context preservation, and spawn tool routing.

## 4. Community Hot Topics
The most active issues by comment count reveal deep user interest in reliability and extensibility:

- **#629** ([BUG] Didn't retry if meet LLM call failed) – 13 comments  
  Long-standing (since Feb 2026) complaint that PicoClaw hangs without retry when an LLM provider returns HTTP 500. Users need robust automatic retry logic.

- **#2408** ([Feature] LLM Account Stacking – Automatic API key rotation) – 11 comments  
  Users want to provide multiple API keys for the same provider and have PicoClaw rotate on rate limits/quotas. This “cartridge-belt” feature is a top-requested enhancement.

- **#2171** ([Refactor] Move to OpenAI Responses API) – 10 comments  
  Community discussion on migrating from Chat Completions to the newer Responses API for better compatibility and future-proofing.

- **#1042** ([BUG] exec tool guardCommand method issues) – 9 comments  
  A popular issue (2 👍) highlighting that the `exec` tool’s path guard incorrectly blocks commands like `curl -s "wttr.in/Beijing?T"` by treating domain names as relative path escapes.

These threads signal that users are actively invested in PicoClaw’s tooling and provider reliability, and the maintainer team is engaging (many closed with merged fixes).

## 5. Bugs & Stability
New bugs reported today (created 2026-05-07 or 2026-05-08) include:

- **#2817** (Voice transcription not passed to LLM) – **High severity**. Despite successful transcription, the LLM receives `[voice]` placeholder instead of the transcribed text. No fix PR yet.
- **#2721** (Session history race with `tool_use_id` 400 from Anthropic) – **High severity**. A reopened race condition that persists in v0.2.5. The original issue #704 was closed without a visible fix. A dedicated fix is urgently needed.
- **#2702** (Multi-user group channels lack sender attribution in default session) – **Medium severity**. All users in a group channel share a single conversation, causing confusion. No fix PR yet.

Additionally, several older bugs were closed today, including:
- **#2468** (Scheduled task execution restricted to internal channels) – closed.
- **#2478** (Skill override when using `/use <skill>` multiple times) – likely fixed.
- **#2482** (Open weights models with OpenAI backend fail on tool calls) – closed.

## 6. Feature Requests & Roadmap Signals
User-requested features visible in today’s top issues:

- **LLM Account Stacking** (#2408) – automatic API key rotation. High demand; likely to land in next minor release.
- **Migration to OpenAI Responses API** (#2171) – partly implemented (checklist shows some endpoints done). Could appear in v0.3.0.
- **General Attachment Support** (#348) – roadmap item for processing files/images across channels. Still open with high priority tag.
- **Non-destructive session reset** (#2820) – new request to clear session without deleting Seahorse history. Quick to implement.
- **Multiple Feishu applications** (#2493) – already closed but signals continued channel flexibility.

Based on current PR momentum, the next version (v0.2.9 or v0.3.0) is likely to include multi-agent discovery ([#2158](https://github.com/sipeed/picoclaw/pull/2158)), improved model configuration UI ([#2752](https://github.com/sipeed/picoclaw/pull/2752)), and consolidated tool feedback throttling ([#2789](https://github.com/sipeed/picoclaw/pull/2789)).

## 7. User Feedback Summary
Real pain points expressed by users:

- **Reliability**: “Task hangs without retry” (#629) and “voice transcription not passed” (#2817) erode trust in long-running or voice-based tasks.
- **Tooling sensitivity**: The `exec` tool’s path guard is too aggressive (#1042), blocking legitimate commands. Users desire smarter heuristics.
- **Multi-channel confusion**: Consecutive messages are only processed for the last one (#2447, #2464) and tokens are undocumented (#2439). Power users require predictable behavior.
- **Configuration friction**: Custom authentication headers (#2169) and secret storage for MCP servers (#2444) are missing, forcing workarounds.

Despite these, the project’s responsiveness (22 bugs closed today) and active community engagement (high comment counts) indicate high satisfaction with the overall direction and maintainer support.

## 8. Backlog Watch
Several important issues and PRs have been open for extended periods without a maintainer response or fix:

- **#629** (LLM retry on failure) – Open since 2026-02-22, 13 comments, no fix PR. One of the most upvoted bugs.
- **#2171** (OpenAI Responses API migration) – Open since 2026-03-30, 10 comments, partially implemented but not fully resolved.
- **#348** (General Attachment Support) – Roadmap item open since 2026-02-17, high priority, but no visible progress.
- **#2158** (Multi-agent discovery prompt) – PR open since 2026-03-29, important for modular agents, still awaiting review.

These items represent the most significant gaps in user experience and project roadmap. Addressing them in the upcoming weeks would greatly enhance PicoClaw’s competitiveness among open-source AI assistants.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-08

## 1. Today's Overview

The project saw very high development activity over the past 24 hours, with **35 pull requests** (22 merged/closed) and **9 issues** updated (5 closed). The burst of merged PRs indicates a focused push to stabilise the agent‑to‑agent routing layer and container environment, while new issues highlight ongoing security hardening and feature expansion. Community discussion remains light (low comment counts), but the volume of code changes suggests a healthy, fast‑moving maintenance and feature cycle.

## 2. Releases

**None** — no new releases were tagged today. The project continues to ship changes through direct merges to `main`.

## 3. Project Progress

**22 pull requests were merged or closed today**, covering several key areas:

- **Routing & A2A fixes** – [#2002](https://github.com/qwibitai/nanoclaw/pull/2002) (closed) fixed origin‑session threading for agent‑to‑agent replies; [#2277](https://github.com/qwibitai/nanoclaw/pull/2277) (closed) refreshed routing context on follow‑up messages; [#2267](https://github.com/qwibitai/nanoclaw/pull/2267) (closed) routed A2A replies back to the originating session.
- **Container & build tools** – [#2336](https://github.com/qwibitai/nanoclaw/pull/2336) (closed) repaired the `claude` binary for pnpm v11; [#2335](https://github.com/qwibitai/nanoclaw/pull/2335) (closed) pinned pnpm to 10.33.0 in containers.
- **New skills** – [#2321](https://github.com/qwibitai/nanoclaw/pull/2321) (closed) added a `onecli-gateway` container skill; [#2319](https://github.com/qwibitai/nanoclaw/pull/2319) (closed) introduced `/add-aws` for AWS CLI access; [#2318](https://github.com/qwibitai/nanoclaw/pull/2318) (closed) added `/add-mnemon` persistent semantic memory.
- **Setup & UX improvements** – [#2324](https://github.com/qwibitai/nanoclaw/pull/2324) (closed) added a “Skip — I’ll connect later” option to Claude auth picker; [#2316](https://github.com/qwibitai/nanoclaw/pull/2316) (closed) gave a back‑to‑channels exit from the “Other…” channel prompt.
- **Documentation** – [#2320](https://github.com/qwibitai/nanoclaw/pull/2320) (closed) updated SKILL.md files for six skills.
- **Compaction reminder** – [#2327](https://github.com/qwibitai/nanoclaw/pull/2327) (closed) injected destination reminders after SDK auto‑compaction, addressing issue [#2325](https://github.com/qwibitai/nanoclaw/issues/2325) (closed).

## 4. Community Hot Topics

Discussion activity remains low across both issues and PRs. The only issue with any traction is:

- **[#869](https://github.com/qwibitai/nanoclaw/issues/869) (open, enhancement, high priority)** — *Per‑group credential management and interactive reauth via channels* — created 2026‑03‑09, 3 comments, no reactions. This long‑standing request for multi‑tenant API credential isolation is the most discussed open issue. The underlying need is for teams or tenants to use separate Claude accounts per group, which is currently impossible.

No pull request attracted more than a few comments. The project’s communication appears to happen primarily through code review rather than public discussion.

## 5. Bugs & Stability

Several bugs were reported and many were fixed within the same 24‑hour window. Severity ranking:

**Critical**  
- **[#2332](https://github.com/qwibitai/nanoclaw/issues/2332) (open, bug)** – `findSessionByAgentGroup` may route A2A replies to the wrong session in multi‑channel groups. Detailed audit confirms message misrouting and dropped messages.  
- **[#2331](https://github.com/qwibitai/nanoclaw/issues/2331) (open, high priority, a2a)** – Same root cause: recency‑based session selection breaks when multiple active sessions exist. No fix PR linked yet, but related closed PRs [#2002](https://github.com/qwibitai/nanoclaw/pull/2002) and [#2267](https://github.com/qwibitai/nanoclaw/pull/2267) address similar issues.

**High**  
- **[#2330](https://github.com/qwibitai/nanoclaw/pull/2330) (open, fix)** – Axios‑based MCP servers silently fail behind OneCLI’s CONNECT‑only proxy. Fix PR exists and is open.  
- **[#2343](https://github.com/qwibitai/nanoclaw/issues/2343) (closed)** – `credentials.json` unreadable for 45 minutes; `sendSystemAlert` did not fire as configured. Closed with fix presumably already merged.  
- **[#2342](https://github.com/qwibitai/nanoclaw/issues/2342) (closed)** – Connectivity watchdog dead since May 1 due to Docker restart failure. Closed.

**Medium**  
- **[#2338](https://github.com/qwibitai/nanoclaw/pull/2338) (open, fix)** – Telegram URL mangling when odd counts of `*` or `_` are present; fix escapes instead of stripping.  
- **[#2339](https://github.com/qwibitai/nanoclaw/pull/2339) (open, fix)** – Test objects missing `in_reply_to` field after TypeScript interface change.  
- **[#2344](https://github.com/qwibitai/nanoclaw/pull/2344) (open, fix)** – `tsc` build broken by five type errors in tests; fix adds missing fields.

**Low**  
- **[#2347](https://github.com/qwibitai/nanoclaw/pull/2347) (open, fix)** – Thread context lost when batch begins with a system message; fix preserves routing fields.  
- **[#2346](https://github.com/qwibitai/nanoclaw/pull/2346) (open, fix)** – Unknown slash commands were incorrectly treated as passthrough, causing responses to be dropped.

## 6. Feature Requests & Roadmap Signals

Features requested or implemented today point toward **multi‑tenant credential management**, **file attachments**, and **expanded skill ecosystem**.

- **[#869](https://github.com/qwibitai/nanoclaw/issues/869) (open, high priority)** – Per‑group credentials. Likely to be a high‑impact feature in the next release, given the long wait and high priority tag.
- **[#2334](https://github.com/qwibitai/nanoclaw/issues/2334) (open)** – File attachment support in the web UI. A common user request that would significantly boost the web client’s utility.
- **[#2337](https://github.com/qwibitai/nanoclaw/pull/2337) (open)** – Surface Claude Code skill catalog to non‑Claude providers, enabling provider‑agnostic skill reuse. Signals roadmap expansion beyond Anthropic-only environments.
- **[#2345](https://github.com/qwibitai/nanoclaw/pull/2345) (open)** – Auto‑import per‑group `CLAUDE.role.md` files, furthering per‑group customisation.
- Skills added today (OneCLI gateway, AWS, mnemon) show the project is actively building an pluggable container skill marketplace.

**Prediction for next version**: Per‑group credentials (#869) and file attachment support (#2334) are the most requested and untouched features; they are strong candidates for inclusion in the next tagged release.

## 7. User Feedback Summary

User‑facing pain points implicitly visible through issues and PRs:

- **Frustration with A2A misrouting** — Two separate bug reports (#2332, #2331) describe conversations going to the wrong session. This is a critical reliability issue for users operating multi‑channel agents.
- **Setup friction** — The addition of a “Skip — I’ll connect later” button (#2324) and a back‑to‑channels exit (#2316) indicates users were getting stuck in modal flows with no escape other than Ctrl‑C.
- **Silent failures** — The `credentials.json` outage (#2343) and the dead watchdog (#2342) show operational blind spots; users may have experienced unresponsive agents without alerts.
- **Positive response** — Rapid closure of many bugs (5 issues closed, 22 PRs merged) suggests the maintainers are responsive and users’ fixes are being shipped quickly.

## 8. Backlog Watch

The following open issues and PRs deserve maintainer attention due to age, priority, or lack of activity:

- **[#869](https://github.com/qwibitai/nanoclaw/issues/869)** — *Per‑group credential management*. Open since 2026‑03‑09 (2 months), high priority, only 3 comments. No assigned developer or linked PR. This is the most visible gap in the project’s roadmap.
- **[#2332](https://github.com/qwibitai/nanoclaw/issues/2332) / [#2331](https://github.com/qwibitai/nanoclaw/issues/2331)** — A2A session routing bugs. Filed just today, but no fix PR yet. Should be prioritised given the “critical” nature and unresolved duplicates.
- **[#2330](https://github.com/qwibitai/nanoclaw/pull/2330)** — Axios proxy fix. Open for ~1 day, awaiting review. Could block users relying on axios‑based MCP servers.

No PRs or issues appear to be truly abandoned or unanswered for >30 days besides #869.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-08

## Today’s Overview
Development activity is **high**, with 8 pull requests touched in the last 24 hours (5 merged/closed) and 5 issues updated (2 closed, 3 open). The team is actively shipping features and fixes: a native Agent Client Protocol (ACP) stdio adapter was merged, CI nightly builds were hardened, and documentation for Zig setup was added. Two new feature requests for the Lark integration suggest growing community interest in real‑time chat bots. No release was cut today, but the CI pipeline is being prepared for nightly prereleases.

---

## Releases
**None** — no new versions were published today.

---

## Project Progress (Merged/Closed PRs)
Five pull requests were merged or closed in the last 24 hours:

- **[#898: ci: force scheduled nightly builds](https://github.com/nullclaw/nullclaw/pull/898)** (closed) – Ensures nightly CI runs are never deduplicated by `head_sha`, preventing silent skips.
- **[#897: chore(docs): Add docs for quick zig setup](https://github.com/nullclaw/nullclaw/pull/897)** (closed) – Resolves #820 by documenting how to install Zig on Debian without Docker.
- **[#896: Add native ACP stdio adapter](https://github.com/nullclaw/nullclaw/pull/896)** (closed) – Implements the Agent Client Protocol (JSON‑RPC over stdio) directly inside the `nullclaw` binary, enabling native agent interoperability.
- **[#893: feat(toolkit): integrate zig-qm-toolkit](https://github.com/nullclaw/nullclaw/pull/893)** (closed) – Adopts the chezmoi‑managed toolkit (hooks, agents, skills, 4‑tier verification) without modifying existing documentation.
- **[#790: fix(providers): Responses API tool schema and null error handling](https://github.com/nullclaw/nullclaw/pull/790)** (closed) – Fixes two bugs in the OpenAI‑compatible Responses API: tool schema format and null error handling.

---

## Community Hot Topics
The most active discussion remains **Issue #167** (“[CLOSED] why cannot use the shell command ‘curl and wget’”, [link](https://github.com/nullclaw/nullclaw/issues/167)) – 10 comments, 1 👍. Users are questioning why common shell tools are hard‑coded and whether there is a configuration to enable them. The underlying need is for **flexible command sandboxing** and better documentation of the allowed tool set.

**Issue #820** (“[CLOSED] How to install Zig on Debian?”, [link](https://github.com/nullclaw/nullclaw/issues/820)) – 5 comments, resolved via PR #897. This reflects the community’s desire for **simpler setup steps**, especially on less common platforms.

**Issue #473** (“[OPEN] README changes”, [link](https://github.com/nullclaw/nullclaw/issues/473)) – 2 comments, 1 👍. Questions the accuracy of the benchmark table in the README; the maintainers have not yet replied. This indicates a need for **ongoing documentation freshness**.

---

## Bugs & Stability
No new crash or regression bugs were reported today, but two stability‑related fixes were merged:

- **PR #790** – Fixes tool schema format errors and null pointer handling in the OpenAI Responses API provider.  
  *Severity: Medium* – The bug could cause incomplete or failed tool calls.
- **PR #887** ([OPEN](https://github.com/nullclaw/nullclaw/pull/887)) – Aims to fix build errors with Zig v0.16 on Windows and Linux.  
  *Severity: Medium* – Blocks contributors using the latest Zig compiler.

No other open stability issues were identified.

---

## Feature Requests & Roadmap Signals
Two new feature requests were opened today, both targeting the **Lark** channel integration:

- **[#895: feat(lark): add config option to disable typing placeholder / retract behavior](https://github.com/nullclaw/nullclaw/issues/895)** – Users want to suppress the “…” indicator sent while the LLM is generating.
- **[#894: feat(lark): add config option to respond to all group messages (not just @mentions)](https://github.com/nullclaw/nullclaw/issues/894)** – A request for the bot to actively participate in group chats without requiring explicit mention.

Both issues have no maintainer response yet; they are likely candidates for the next minor release.

Additionally, **PR #899** ([OPEN](https://github.com/nullclaw/nullclaw/pull/899)) adds nightly prerelease publishing, signaling a shift toward **continuous delivery** of rolling builds. The **hackathon PR #885** ([OPEN](https://github.com/nullclaw/nullclaw/pull/885)) introduces a “Data Governance Layer” – a major feature that could land in a future version if accepted.

---

## User Feedback Summary
- **Pain points**: Confusion over which shell commands are allowed (#167), lack of straightforward Zig installation steps (#820), and stale benchmark numbers in the README (#473).
- **Use cases**: Developers integrating NullClaw in group chats (Lark) and those seeking native agent interoperability (ACP adapter). The merged ACP adapter (#896) directly addresses a long‑standing request for protocol‑standard agent connectivity.
- **Satisfaction**: The team’s responsiveness (closing #820 quickly, merging #790) suggests good maintenance health, but the lack of reply on #473 may frustrate documentation‑focused contributors.

---

## Backlog Watch
The following items require maintainer attention:

- **[Issue #473](https://github.com/nullclaw/nullclaw/issues/473)** (OPEN since 2026-03-13) – README benchmark table accuracy. Last updated May 7, but no official response. Stale for nearly two months.
- **[PR #885](https://github.com/nullclaw/nullclaw/pull/885)** (OPEN since 2026-05-04) – Hackathon data governance layer. Needs review or feedback from core maintainers.
- **[PR #887](https://github.com/nullclaw/nullclaw/pull/887)** (OPEN since 2026-05-04) – Build fix for Zig v0.16. Untriaged; contributors cannot build on latest Zig without it.
- **[#895](https://github.com/nullclaw/nullclaw/issues/895) and [#894](https://github.com/nullclaw/nullclaw/issues/894)** (both opened today) – No initial response yet. Acknowledgment would be helpful to signal activity.

*None of these are critical blockers, but they represent gaps in triage responsiveness.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-08

## Today’s Overview
Project activity remains high, driven by the ongoing **Reborn** architecture refactor. In the last 24 hours, **21 issues** were updated (14 open, 7 closed) and **50 PRs** were updated (18 open, 32 merged/closed). A new release **ironclaw-v0.28.0** landed, delivering the first major Reborn integration substrate on `main`. The release and the flood of Reborn‑related PRs signal that the project is moving aggressively from prototype to production wiring, while several bug‑bash P1 issues and a nightly E2E failure indicate continued stabilization work is needed.

## Releases
**ironclaw-v0.28.0** (2026-05-07) — [Release](https://github.com/nearai/ironclaw/releases/tag/ironclaw-v0.28.0)  
- **Reborn integration substrate** now on `main`, introducing host foundation crates, capability host, runtime dispatcher, process lifecycle, filesystem, secrets, network, and extension manifest registry boundaries.  
- Added WIT‑compatible WASM tool runtime.  
- No explicit breaking changes or migration notes were published; downstream consumers on crates.io are still pinned to 0.24.0 (see #3259), but the tagged release includes all changes up to 0.28.0.

## Project Progress (Merged/Closed PRs Today)
32 PRs were merged or closed today. Key highlights include:

- **Reborn durable stores** – Several PRs added production‑grade database stores:  
  - #3379 — `SessionThreadService` (libSQL/PostgreSQL) for canonical threads and transcripts  
  - #3378 — wired durable `RunStateApprovalStore` backends  
  - #3368 — `CapabilityLeaseStore` implementations  
  - #3349 — run‑state database stores  
  - #3351 — `ironclaw_product_adapters` core contract (PR 1/7 of ProductAdapter stack)  
  - #3382 — hardened `AgentLoopHostFacade` with bounded refs  

- **Worker runtime in Docker image** – #3275 now builds the worker runtime into the official Docker image, enabling sandbox workers without separate pulls.  

- **Telegram/approval UX fixes** – #3365 fixed an inline‑await approval gate deadlock; #3364 addressed the “Restarting IronClaw” hang (#3082) and improved approval clarity.  

- **WeChat channel** – #3386 added WASM artifact metadata so WeChat installations use pre‑built bundles in production.  

- **Testing scaffolds** – #2806 stubs for engine v2 acceptance and regression suites.

## Community Hot Topics
Most active issues and PRs by comment count (all are core team driven, no external contributors with high comments):

- **[#3067] Reborn vertical‑slice integration tests** (28 comments) — open, high risk, tracking caller‑level tests to prove the Reborn substrate works through public entrypoints.  
- **[#3022] Event substrate integration tests** (9 comments) — open blocker for Reborn cutover; cross‑service test suites for V1 event producers.  
- **[#3016] Reference AgentLoopHost facade** (7 comments) — open, part of the Reborn cutover blocker chain.  
- **[#3093] EventProjectionService** (4 comments) — closed, implemented.  
- **[#3333] Production wiring and missing crates** (1 comment) — open audit of fake/no‑op seams in `origin/reborn‑integration`.  

The underlying theme is **completing the Reborn refactor**; these issues track the remaining integration and test gaps before cutover.

## Bugs & Stability

### Critical / High Severity
- **Nightly E2E failure** ([#3323](https://github.com/nearai/ironclaw/issues/3323)) — scheduled run failed with `Full E2E / E2E (v2‑engine)` job broken. No fix PR yet; root cause unknown.  
- **Telegram setup not working** ([#3317](https://github.com/nearai/ironclaw/issues/3317), P1) — Bug Bash priority 1. A fix PR [#3381](https://github.com/nearai/ironclaw/pull/3381) (open) addresses the root cause (cross‑channel OAuth leaks).  
- **Pinned crates.io version** ([#3259](https://github.com/nearai/ironclaw/issues/3259)) — downstream consumers stuck at 0.24.0 due to wasmtime CVEs. No PR yet.

### Moderate Severity
- **Conversation titles default to first user message** ([#3385](https://github.com/nearai/ironclaw/issues/3385)) — no automatic summarization, leading to poor UX. No fix PR yet.  
- **Multi‑workspace Slack support** ([#3334](https://github.com/nearai/ironclaw/issues/3334)) — feature request but also a potential gap in existing Slack integration.

### Fixed / Closed Today
- [#3225](https://github.com/nearai/ironclaw/issues/3225) — Gemini API‑key tool‑calling failure (closed).  
- [#3229](https://github.com/nearai/ironclaw/issues/3229) — LLM provider fallback persisting to DB (closed).  
- [#3082](https://github.com/nearai/ironclaw/issues/3082) — App hang on restart after enabling auto‑approvals (fixed via [#3364](https://github.com/nearai/ironclaw/pull/3364)).  
- [#3201](https://github.com/nearai/ironclaw/issues/3201) — Deepseek tool use not working (closed).  
- [#3274](https://github.com/nearai/ironclaw/issues/3274) — Data missing after 0.26→0.27 upgrade (closed).

## Feature Requests & Roadmap Signals
- **Multi‑workspace support** ([#3334](https://github.com/nearai/ironclaw/issues/3334)) — one IronClaw instance across multiple Slack workspaces, opened by a community member. Likely a longer‑term feature.  
- **Automatic conversation titles** ([#3385](https://github.com/nearai/ironclaw/issues/3385)) — users want title generation from summary, not verbatim first message.  
- **Reborn migration tasks** — Issues [#3290](https://github.com/nearai/ironclaw/issues/3290) (missions/jobs), [#3289](https://github.com/nearai/ironclaw/issues/3289) (secrets/OAuth), [#3288](https://github.com/nearai/ironclaw/issues/3288) (extensions/skills/MCP), [#3287](https://github.com/nearai/ironclaw/issues/3287) (memory/workspace) are part of a planned product‑surface migration for 0.29.0 or later.  

**Prediction for next release (0.29.0):** Likely includes more Reborn crate integrations (product adapters, durable stores), fixes for Telegram OAuth, and possibly the conversation title improvement if picked up.

## User Feedback Summary
Real pain points expressed through Bug Bash issues and feature requests:

- **Telegram setup friction** (#3317) — cross‑channel auth (Telegram → Gmail) fails silently, leaving users stuck.  
- **Upgrade data loss** (#3274) — after an in‑place upgrade data appeared missing until manual refresh, causing confusion.  
- **LLM provider configuration fragility** (#3229, #3225) — users faced permanent provider config corruption and Gemini tool‑call failures.  
- **Missing convenience** (#3385) — conversation titles are not human‑friendly, requiring manual renaming.  
- **Long‑standing crates.io publish gap** (#3259) — downstream Rust developers cannot use any version beyond 0.24.0 despite multiple tagged releases.

Overall satisfaction appears lower for setup/upgrade stability, but the Reborn refactor promises a more reliable architecture.

## Backlog Watch
Issues and PRs that require maintainer attention:

- **[#3067] Reborn integration tests** — 28 comments, open for 9 days; critical for cutover but still no active PR.  
- **[#3022] Event substrate tests** — blocker for cutover; no PR in 10 days.  
- **[#3259] crates.io publish** — open since May 5; blocks all downstream Rust users.  
- **[#2979] Kubernetes sandbox runtime** — PR open since Apr 27 (size XL); has no recent activity.  
- **[#3333] Production wiring audit** — opened today, but already flagged multiple fake/no‑op seams that need real implementations.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-08

## Today's Overview
The project experienced a surge of activity on May 8, 2026, with **50 pull requests updated** in the last 24 hours—43 of which were merged or closed. This marks one of the most intense merge days in recent history, reflecting a concerted push toward the `release/2026.05.08` branch. One new release (2026.5.7) was published yesterday. Two open issues remain, one of which (member login failures) blocks paid users from accessing premium models. Overall project health is strong: the team is actively fixing bugs, enhancing UI/UX, and delivering features at a high velocity.

## Releases
- **LobsterAI 2026.5.7** (2026-05-07)  
  [GitHub Release](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.5.7)  
  **Changes:**  
  - fix(skills): improve Windows skill delete reliability and import feedback (#1881)  
  - feat(skill): upgrade youdaonote skill to 1.0.8 (#1882)  
  - refactor (general)  
  **Breaking changes:** None reported.  
  **Migration notes:** No action required; update normally.

## Project Progress
The majority of today’s merged PRs were cherry-picks or feature branches targeting the `release/2026.05.08` branch. Key advancements include:

### 🆕 New Features
- **AI Diagnostics for Email Failures** (#1916, #1527) – One‑click AI diagnosis when IMAP/SMTP connectivity tests fail, pre‑filling error context into the cowork view.  
- **Token Usage Display** (#1912) – Shows input/output tokens, cache reads, context window percentage, model name, and agent info below each assistant message.  
- **Onboarding Tour** (#1577) – 6‑step driver.js‑based tour for new users (side navigation, first conversation, model configuration).  
- **Scheduled Task History Pagination & Filtering** (#1913, #1564) – Time range, status filters, and pagination for task run history.  
- **Per‑Agent Working Directory** (#1904) – Each agent can now have an independent workspace.  
- **Artifact Feature** (#1906) – New artifact subsystem merged (details pending).  
- **Home Screen Animations** (#1915, #1554) – Staggered entrance animations, gradient meshes, and theme‑aware styling improvements.  

### 🔧 Major Fixes
- **Streaming Text Merge Bug** (#1908) – Removed erroneous overlap detection that dropped characters (e.g., `.pptx` → `.ptx`).  
- **Windows File Preview Duplicate Cards** (#1909) – Fixed path dedup and ENOENT errors on `D:\` paths.  
- **Startup Reliability** (#1910) – Reduced false initialization failures; added in‑app relaunch button on error screen.  
- **Model Selection Persistence** (#1905) – Fixed issue where the default model was not remembered after restart.  
- **Markdown Table Persistence** (#1900) – Harden assistant segment persistence to avoid truncated tables under concurrent sessions.  

### ♻️ Refactoring & Cleanup
- **ESLint Zero‑Error Pass** (#1498) – Fixed all 165 remaining ESLint errors (161 files auto‑sorted, 1 manual fix).  
- **Cross‑Platform Test Fix** (#1914) – Used `path.resolve()` in test assertions to stop Windows CI failures.  
- **Cowork Session Pagination** (#1907, #924) – Paginated session list and message history to reduce memory/rendering overhead.  
- **Agent UI Optimization** (#1911) – Minor UI tweaks to the agent management interface.

## Community Hot Topics
| Issue/PR | Type | Comments | Summary | Link |
|----------|------|----------|---------|------|
| **#1878** | Issue (open) | 2 | IM robot WeChat interface: after scanning QR code, user cannot enter the 6‑digit verification number; client lacks input field. | [Issue #1878](https://github.com/netease-youdao/LobsterAI/issues/1878) |
| **#1903** | Issue (open) | 1 | Frequent membership login failures; user cannot access paid NetEase models. Screenshot shows error screen. | [Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903) |

**Analysis:** Both issues reflect pain points around authentication/authorization. #1903 is especially critical as it blocks paying customers from using the core value proposition (premium models). #1878 indicates a missing UI affordance for the WeChat bot configuration flow—users are stuck after scanning.

## Bugs & Stability
Ranked by severity:

1. **🔴 CRITICAL: Member login failures (#1903)** – Users cannot log in at all, preventing access to paid NetEase models. No fix PR yet. Root cause unknown.  
2. **🟡 HIGH: Missing verification code input for WeChat bot (#1878)** – Blocks setup of IM robot with WeChat interface. No fix PR yet.  
3. **🟡 HIGH: Streaming text corruption (#1908)** – Characters dropped in edge cases (e.g., `.pptx` rendered as `.ptx`). **Fixed** in PR #1908.  
4. **🟢 LOW: Windows file preview duplicate cards & paths (#1909)** – ENOENT errors on Windows only. **Fixed** in PR #1909.  
5. **🟢 LOW: False startup failures (#1910)** – Timeout thresholds increased and relaunch button added. **Fixed** in PR #1910.  
6. **🟢 LOW: Markdown table degradation (#1900)** – Intermittent truncation under concurrent sessions. **Fixed** in PR #1900.  
7. **🟢 LOW: Model selection not persisted (#1905)** – Annoyance after restart. **Fixed** in PR #1905.

## Feature Requests & Roadmap Signals
- **Better login mechanism** – Issue #1903 implicitly requests a more robust authentication flow. Likely to be addressed in an upcoming hotfix.  
- **WeChat bot verification UI** – Issue #1878 requests a text input pop‑up for the 6‑digit code. Easy to implement once prioritized.  
- **AI‑assisted diagnostics** – The “AI Diagnostics” button for email failures (#1527/#1916) signals a pattern that could extend to other error scenarios (e.g., general config issues, network errors).  
- **Per‑agent working directories** (#1904) suggests growing interest in agent isolation and task‑specific environments.  
- **Artifact subsystem** (#1906) – While details are sparse, this could be a major feature for collaborative document or code generation. Expect more documentation in the next release.  
- **Onboarding tour** (#1577) and **home screen animations** (#1554) indicate a polish phase aimed at improving first‑time user experience and visual appeal.

## User Feedback Summary
- **Frustration:** Login failures (#1903) are generating direct dissatisfaction, as users cannot use paid services. One comment from the author: “会员登录不进去，无法使用网易付费的模型” (cannot log in, cannot use NetEase paid models).  
- **Usability gap:** The WeChat scanner flow (#1878) lacks a verification code input, leaving users stuck mid‑configuration (“咱们客户端未给出输入界面，导致无法成功配置”).  
- **Positive signal:** No new complaints about email diagnostics or text corruption after today’s fixes. The high PR merge velocity suggests the team is listening and shipping quickly.

## Backlog Watch
No critical long‑standing issues or PRs were identified. The two open issues (#1878 and #1903) are recent (created within the last 8–9 days) and are actively discussed. However, maintainers should prioritize a fix for #1903 (login failures) as it directly impacts revenue and trust. All other open PRs (7 total, not listed in detail) appear to be minor or awaiting review; none show signs of abandonment.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-08

## 1. Today's Overview

Moltis has seen a burst of activity in the past 24 hours, with 4 closed issues, 9 merged/closed pull requests, and 2 new releases. The project is moving quickly across multiple fronts: voice and speech-to-text improvements, a new telephony integration, image generation support, sandbox reliability fixes, and a foundational node identity protocol. The sole open PR (still in review) expands voice model guidance for OpenAI Realtime. Overall project health is strong – high throughput, responsive maintainers, and several critical bugs fixed within a day of reporting.

## 2. Releases

Two releases landed today, labelled **20260507.05** and **20260507.04**. No release notes or changelogs were provided, but based on the merged PRs, these likely include the fixes for browser sandbox Docker failures, tool-call argument diagnostics, the new whisper-local STT provider, image generation via Codex OAuth, and the Ed25519 node identity system. No breaking changes or migration notes have been announced; upgrades should be safe.

## 3. Project Progress (Merged/Closed PRs)

Nine PRs were closed or merged in the last 24 hours, spanning features, fixes, and documentation:

| PR | Description | Status |
|----|-------------|--------|
| [#981](https://github.com/moltis-org/moltis/issues/981) | **feat(voice):** add whisper-local STT provider, show all voice providers by default | Merged |
| [#983](https://github.com/moltis-org/moltis/issues/983) | **fix(agents):** preserve tool argument diagnostics (fixes #963) | Merged |
| [#982](https://github.com/moltis-org/moltis/issues/982) | **feat:** Add Codex OAuth image generation via `gpt-image-2` | Merged |
| [#920](https://github.com/moltis-org/moltis/issues/920) | **feat(telephony):** add phone call support via Twilio (call state machine, PCM→mu-law, channel plugin) | Merged |
| [#980](https://github.com/moltis-org/moltis/issues/980) | **fix(browser):** resolve sandbox profile host mounts (fixes #977) | Merged |
| [#979](https://github.com/moltis-org/moltis/issues/979) | **feat(nodes):** Ed25519 challenge-response node identity (TOFU) | Merged |
| [#978](https://github.com/moltis-org/moltis/issues/978) | **chore(deps):** bump wasmtime to 36.0.8 | Merged |
| [#976](https://github.com/moltis-org/moltis/issues/976) | **docs:** add Agent Identity + Onboarding Protocols integration guide | Merged |
| [#942](https://github.com/moltis-org/moltis/issues/942) | **feat(sandbox):** remote & multi-backend sandbox support (Vercel, Daytona, Firecracker) | Merged |

The open PR [#984](https://github.com/moltis-org/moltis/issues/984) (feat(voice): surface OpenAI realtime model guidance) is still under review.

## 4. Community Hot Topics

None of the issues or pull requests received comments or reactions, suggesting either low community chatter or that the project’s issues are mainly filed by the development team themselves for tracking. Nevertheless, the following items indicate active pain points:

- **Issue [#963](https://github.com/moltis-org/moltis/issues/963)** (Tool calls with malformed/empty arguments): Fixed by PR #983 – user-reported intermittent failures in exec tool.
- **Issue [#956](https://github.com/moltis-org/moltis/issues/956)** (Image generation support): Feature request from bashrusakh – implemented in PR #982.
- **Issue [#973](https://github.com/moltis-org/moltis/issues/973)** (Onboarding & Identity protocols): Proposal by vystartasv – implemented in PR #979 and documented in PR #976.
- **Issue [#977](https://github.com/moltis-org/moltis/issues/977)** (Browser sandbox fails in Docker): User TLA020 reported a blocker – fixed by PR #980.

The community need is clear: users want Moltis to work reliably in containerized and cloud environments, support voice/image generation, and enable multi-agent interoperability.

## 5. Bugs & Stability

Two bugs were reported and both were fixed within 24 hours.

| Severity | Issue | Description | Fix PR |
|----------|-------|-------------|--------|
| **High** | [#977](https://github.com/moltis-org/moltis/issues/977) | Browser sandbox completely fails when Moltis runs inside Docker (LXC/Proxmox) due to unresolved host mounts. | [#980](https://github.com/moltis-org/moltis/issues/980) |
| **Medium** | [#963](https://github.com/moltis-org/moltis/issues/963) | Intermittent exec tool failures – malformed or empty arguments collapse to `missing=command` before validation hooks run. | [#983](https://github.com/moltis-org/moltis/issues/983) |

No regressions were introduced. The nightly releases appear stable.

## 6. Feature Requests & Roadmap Signals

Two user-requested features were shipped today:

- **Image generation** (issue #956) via Codex OAuth and `gpt-image-2` – likely to be included in the next stable release.
- **Agent Identity & Onboarding Protocols** (issue #973) – Ed25519 TOFU trust model is now in place, along with integration documentation.

Other roadmap signals from merged PRs:

- **Telephony** (PR #920) – Twilio integration is now available, a major new channel.
- **Whisper-local STT** (PR #981) – enables privacy-preserving speech-to-text via local servers.
- **Remote/cloud sandbox backends** (PR #942) – Vercel, Daytona, Firecracker support expands deployments.

The open PR [#984](https://github.com/moltis-org/moltis/issues/984) hints at deeper OpenAI Realtime voice model configuration options.

**Prediction:** The next version (likely `20260508.x` or `v0.13`) will include all of the above: voice improvements, image generation, telephony, sandbox multi-backend, and node identity.

## 7. User Feedback Summary

User-submitted issues reveal three real pain points:

1. **Docker environment failures** – TLA020 reported that browser sandbox breaks entirely in Docker (Proxmox/LXC). The fix was fast, reflecting responsive support.
2. **Intermittent tool-call corruption** – Cstewart-HC experienced unpredictable exec failures. The root cause (argument serialization collapse) was identified and patched.
3. **Missing features** – bashrusakh wanted image generation; vystartasv wanted identity protocols. Both were quickly implemented, indicating the maintainers are highly receptive to community-driven enhancements.

Overall satisfaction appears high – all reported issues were closed, and features requested were delivered within days.

## 8. Backlog Watch

There are no stale or long-unanswered issues or pull requests in the current dataset. All tracked items are recent and have been addressed or are actively in review (PR #984). The project maintains a clean backlog with rapid turn-around. Maintainers should continue this cadence to keep the community engaged.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-05-08

## 1. Today's Overview
CoPaw saw high activity in the last 24 hours, with **36 issues** updated (21 open, 15 closed) and **29 pull requests** updated (9 open, 20 merged/closed). Despite no new releases, the team has been actively closing bugs and merging features, especially around UX improvements, channel reliability (WeChat, Feishu), and developer tooling (CLI diagnostics, backup commands). Community engagement remains strong, with several long-standing discussions still unresolved and new performance regression reports emerging on the latest version. Overall project health is good, but resource leaks and UI lag on high-usage scenarios are pressing concerns.

**No new releases** since the data snapshot.

---

## 2. Releases
No new releases available in the last 24 hours.

---

## 3. Project Progress
The following PRs were merged/closed today (May 8), representing tangible progress:

- **#4106** – *fix(WeChat): flush WeChat merge buffer immediately for cron sends* (merged) – Fixes cron-triggered messages being stuck when `message_merge_delay_ms=0`.
- **#4098** – *feat(feishu): surface sender nickname to agent env context* (merged) – Feishu channel now passes display name to agents.
- **#4091** – *feat(console): Add "Enable" and "Disable" buttons to the batch operation of skills* (merged) – Delivers on feature request #3503.
- **#4093** – *fix(pack): restore conda packaging tools before conda-pack* (merged) – Fixes Windows packaging conflict with `conda-pack` (related to #3988).
- **#4094** – *refactor(console): TokenUsage* (merged) – UI and code refactoring for token usage page.
- **#4089** – *fix(chat): remove redundant URL prefix stripping in file preview paths* (merged) – Addresses file link expiration issue (#4047).
- **#3999** – *feat(skills): add cli skill test command* (merged) – New `qwenpaw skills test` CLI command for validating skills.
- **#4055** – *feat(channel): propagate user display name to agent env context* (merged) – Similar to #4098, enhances channel metadata passing.
- **#3911** – *plugin: add gpt image 2 tool plugin* (merged) – New plugin.
- **#3605** – *refactor(wechat): centralize legacy weixin → wechat data migrations* (merged) – Cleans up workspace startup migrations.
- **#2205** – *fix: fallback to model-level connection check for minimax-cn* (merged) – Fixes connection testing for Minimax China provider.

Additionally, **open PRs** still in review/under development include:
- **#4107** – new agent status endpoint with task tracking.
- **#3819** – browsable remote model listing and batch insertion (replaces Auto Discover).
- **#4046** – rule-level auto deny for Tool Guard.
- **#4095** – CLI backup commands.
- **#3238** – experimental PlanNotebook support for task planning.

---

## 4. Community Hot Topics
The most active issues (by comment count) reflect both strategic discussions and recurrent problems:

| Issue | Title | Comments | Status |
|-------|-------|----------|--------|
| [#280](https://github.com/agentscope-ai/QwenPaw/issues/280) | Discussion: Which Skills and MCPs Can Be Built-in? | **27** | Open |
| [#3919](https://github.com/agentscope-ai/QwenPaw/issues/3919) | [Bug]: 切换Agent后返回原agent，发现任务中断且session丢失 | **9** | Closed |
| [#578](https://github.com/agentscope-ai/QwenPaw/issues/578) | [Meta]: OpenClaw-Inspired Features for Compounding Agent Value | **7** | Open |
| [#3350](https://github.com/agentscope-ai/QwenPaw/issues/3350) | [Question]: 页面进行超多轮对话后页面滚动变得特别卡 | **7** | Closed |
| [#1403](https://github.com/agentscope-ai/QwenPaw/issues/1403) | [Bug]: 飞书消息处理没有去重机制 | **6** | Closed |

- **#280** continues to gather feedback on which skills and MCP servers should ship as built-in – a major UX and ecosystem decision that remains unresolved.
- **#578** proposes a set of “compounding value” features inspired by OpenClaw, including long-term memory and progressive personalization – the community is weighing in on these holistic improvements.
- **#3350** (scrolling lag after 200+ turns) and **#3919** (session loss on agent switch) highlight critical UX regressions that were recently closed, though some underlying issues may persist.

On the PR side, **#4107** (agent status endpoint) and **#3819** (remote model browser) are the most notable open contributions.

---

## 5. Bugs & Stability
Several bugs were reported or updated in the last 24 hours, ordered by severity:

**High severity:**
- **#4105** — *Orphaned MCP processes accumulate under `qwenpaw app` daemon (~18 GB RAM leaked over 1.5 days)*. This is a critical memory leak from MCP child processes not being cleaned up after session end. No fix PR yet.
- **#4102** — *Screenshots kept in context, continuously compressed, consuming tokens without benefit*. User reports that visual context is bloated and cannot be disabled. Frustration with unclear control.
- **#4108** — *New version webui extremely laggy during response generation; CPU spikes, UI freezes*. Multiple confirmations on v1.5.1.post2, Windows 11.
- **#4056** — *WeChat Channel Message Loss Under Normal Network Conditions*. Agent stops responding intermittently on WeChat, though other functions remain alive.
- **#4101** (closed) — *Upgrade to 1.1.5.post2 loses agent session and config again*. Regression on Docker deployments.

**Medium severity:**
- **#4104** — *File names with mixed Chinese/English get an extra space (e.g., "2026 年报告.word")*. Purely cosmetic but affects file handling.
- **#4099** — *Agent name "Friday" hardcoded in session init instead of reading from agent.json*. Prevents custom naming.
- **#4036** — *Adding a model requires too many steps and clicks*. UX complaint about excessive navigation (5+ steps). This is partly addressed by PR #3819.
- **#4051** — *DeepSeek model think content parsing issue* – model sometimes only returns thinking tags, no reply.

**Low severity:**
- **#4103** — *Windows shell selection not configurable* (always uses PowerShell 5, causing encoding issues).
- **#4000** — *WeChat conversation not synced with browser + missing voice input on web*.

*Note:* Several closed bugs today (e.g., #3919, #3988, #4047) have associated fix PRs that were merged.

---

## 6. Feature Requests & Roadmap Signals
Active feature requests that are likely candidates for the next release:

- **#280** — *Built-in Skills/MCPs list*: The team has been discussing which MCPs to ship pre-installed. Community suggestions include web scraping, file operations, and calendar integration. A decision is expected soon.
- **#578** — *OpenClaw-Inspired Compounding Value*: Covers long-term memory, adaptive preferences, and progressive personalization. This meta-issue is gaining traction and may drive several sprint items.
- **#4030** — *Vertex AI Gemini provider*: Enterprise users need GCP billing and IAM. PR #3819 (remote model browser) partially addresses discovery, but provider support is separate.
- **#2235** — *Web console upgrade mechanism*: Users want remote upgrading without CLI. No PR yet, but frequently +1’ed.
- **#4087** — *Enhance File module to view non-.md files*: Currently only markdown files are previewable. Simple fix that would improve daily workflow.
- **#4078** — *Interactive Skill Selector dropdown (instead of plain text list)*: Pressing `/` currently dumps all skill names as text; a proper dropdown would reduce copy-paste friction.

The merged PR **#4091** (batch enable/disable skills) directly fulfills request **#3503**, indicating the team is responsive to community-driven UI improvements.

---

## 7. User Feedback Summary
Recent user sentiment reflects both enthusiasm and frustration:

- **Performance regressions** are the top pain point. Multiple reports (e.g., #4108, #3350) describe severe UI slowdown after prolonged use, especially with long conversations (>200 turns) or on Windows. Users feel the experience is “getting worse” with each version.
- **Session and state management** issues cause distrust. Loss of chat context after switching agents (#3919, #4101) disrupts workflows, especially for those running multi-agent project iterations.
- **WeChat / Feishu channel reliability** remains a concern: message loss (#4056), duplicate processing (#1403), and nickname not propagated (#4098 fixed, but #4055 also addressed it). Users expect seamless sync.
- **Onboarding friction** is evident from issues like #4036 (model addition complexity) and #4000 (lack of voice input, unclear sync). New users find setup daunting.
- **Positive signals**: The community actively contributes features (CLI skill test, batch skill management, diagnostic tools). Long-standing issues like file token expiration (#4047) are being addressed. There is strong interest in built-in MCPs and long-term intelligent features.

---

## 8. Backlog Watch
The following items are important but have not received maintainer attention recently or remain unresolved for a long time:

| Item | Title | Age | Status |
|------|-------|-----|--------|
| [#280](https://github.com/agentscope-ai/QwenPaw/issues/280) | Discussion: Which Skills and MCPs Can Be Built-in? | ~2 months (Mar 2) | Open, no decision |
| [#578](https://github.com/agentscope-ai/QwenPaw/issues/578) | OpenClaw-Inspired Features for Compounding Agent Value | ~2 months (Mar 4) | Open, no triage |
| [#2235](https://github.com/agentscope-ai/QwenPaw/issues/2235) | Web console upgrade capability | ~1.5 months (Mar 25) | Open, no PR |
| [#3238](https://github.com/agentscope-ai/QwenPaw/pull/3238) | PlanNotebook support (experimental) | ~1 month (Apr 10) | Open PR, no recent reviews |
| [#3819](https://github.com/agentscope-ai/QwenPaw/pull/3819) | Browsable remote model listing & batch insertion | ~2 weeks (Apr 25) | Open PR, no merge |
| [#3916](https://github.com/agentscope-ai/QwenPaw/pull/3916) | fix(backup): restore secrets on Docker volume mount points | ~10 days (Apr 28) | Open, needs review |

- **#280** is critical for ecosystem direction – deciding built-in capabilities will shape onboarding and compete with other agent platforms.
- **#578** is a meta-issue that spans multiple sprints but needs explicit roadmap commitment.
- **PR #3238** (PlanNotebook) is a significant architectural addition that has stalled in review.
- **PR #3819** (model browser) directly addresses UX complaints (#4036) and should be prioritized for merge.

*Note:* No pull requests or issues have been completely abandoned, but several key ones have been waiting for maintainer feedback for weeks.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-08

## 1. Today’s Overview
ZeroClaw saw extremely high activity over the past 24 hours, with **50 issues and 50 PRs updated**. The project shipped **v0.7.5**, a substantial release introducing a schema-driven in-browser onboarding flow, per-property gateway CRUD, and a three-surface personality editor. Despite the positive release momentum, the community is grappling with several **high-severity bugs**—most notably a WhatsApp Web protocol regression, broken shell tool dispatch at full autonomy, and a Docker bind‑mount conflict that shadows the web dashboard. The maintainer team has merged two PRs and closed two issues, but many critical items remain in the **“needs-maintainer-review”** queue.

## 2. Releases
**v0.7.5** ([changelog](https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.7.5))  
- **New features**: In-browser onboarding (`/onboard`) driven by a JSON schema; per‑property gateway CRUD surface backed by an OpenAPI 3.1 spec and a typed CLI; a three‑surface personality editor (CLI / TUI / web UI).  
- **Breaking changes**: None documented.  
- **Migration notes**: No explicit migration steps are listed; the release is a drop‑in replacement for v0.7.4. Administrators should verify that any custom `config.toml` entries remain compatible with the new schema‑driven validation.

## 3. Project Progress
Two PRs were merged/closed in the last 24 hours (not visible in the top‑20 list, but the aggregate data reports 2 closed/merged PRs).  
- **Issue #6418** ([closed](https://github.com/zeroclaw-labs/zeroclaw/issues/6418)) — “Fallback Providers Fail to Inherit Credentials from `config.toml`” (severity S0) was resolved, likely by a corresponding merge.  
- **Issue #6320** ([closed](https://github.com/zeroclaw-labs/zeroclaw/issues/6320)) — “Desktop menu‑bar chat — first‑run onboarding parity” was closed; the desktop app now offers an onboarding flow without requiring a terminal.

Among ongoing PRs, the most immediately actionable is **#6502** ([PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6502)), which fixes the v0.7.5 release workflow (a missing `gen-api` step was blocking the web build). This PR is tagged **release-gate** and appears to have been needed to ship v0.7.5.

## 4. Community Hot Topics
The most commented‑on issues reveal deep infrastructure concerns:

- **#5937** ([8 comments](https://github.com/zeroclaw-labs/zeroclaw/issues/5937)) — “refactor: Unify providers architecture and reqwest client management” (enhancement, risk:high, blocked). Contributors want a unified provider API to eliminate duplicated configuration and inconsistent HTTP client usage. This is a long‑running architectural wish that has been open since April 20.

- **#6246** ([6 comments](https://github.com/zeroclaw-labs/zeroclaw/issues/6246)) — “WhatsApp Web channel: pair succeeds but messages don't flow after April 2026 server‑side protocol bump” (bug, S1). A server‑side WhatsApp Web protocol change around April 24 has silently broken message delivery. Users are blocked and tag this as a top‑priority channel regression.

- **#6399** ([3 comments](https://github.com/zeroclaw-labs/zeroclaw/issues/6399)) — “Custom remote provider sends local image file paths instead of data URLs, breaking multimodal requests” (bug, S1). Operators using remote vLLM/llama.cpp servers cannot use multimodal features because absolute local paths are sent instead of data URIs.

- **#6474** ([3 comments](https://github.com/zeroclaw-labs/zeroclaw/issues/6474)) — “process 1 user request, invoking the LLM twice repeatedly” (bug, S1). Reports of duplicate LLM calls on a single user request, wasting tokens and slowing response times.

## 5. Bugs & Stability
Several S1 (workflow‑blocked) bugs were reported or updated:

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| [#6246](https://github.com/zeroclaw-labs/zeroclaw/issues/6246) | S1 | WhatsApp Web silent message drop after server‑side protocol bump | Not yet |
| [#6399](https://github.com/zeroclaw-labs/zeroclaw/issues/6399) | S1 | Custom remote provider sends local file paths instead of data URLs | Not yet |
| [#6434](https://github.com/zeroclaw-labs/zeroclaw/issues/6434) | S1 | Shell tool calls refused at `[autonomy] level = "full"` — `tool_dispatch` never reaches runtime | Not yet (needs‑maintainer‑review) |
| [#6410](https://github.com/zeroclaw-labs/zeroclaw/issues/6410) | S1 | `google_workspace` tool fails on Windows (`.cmd` extension) and mangles JSON via shell fallback | Not yet |
| [#6377](https://github.com/zeroclaw-labs/zeroclaw/issues/6377) | S1 | Llama.cpp default provider throws 500 on tool usage; should use `"responses"` endpoint | Not yet |
| [#6472](https://github.com/zeroclaw-labs/zeroclaw/issues/6472) | S2 (reported as high risk) | Gateway panics when using Postgres (“Cannot start a runtime from within a runtime”) | Not yet |
| [#6400](https://github.com/zeroclaw-labs/zeroclaw/issues/6400) | S2 | Docker bind mount at `/zeroclaw-data` shadows pre‑built web dashboard | Not yet |
| [#6431](https://github.com/zeroclaw-labs/zeroclaw/issues/6431) | S2 | SQLite memory schema init can fail during concurrent startup | ✅ PR [#6432](https://github.com/zeroclaw-labs/zeroclaw/pull/6432) (open) |

## 6. Feature Requests & Roadmap Signals
The top‑voted enhancements include both desktop parity and provider flexibility:

- **Desktop parity features** (likely for v0.7.6):  
  - [#6465](https://github.com/zeroclaw-labs/zeroclaw/issues/6465) — Bundle `chat‑ui` as static assets in the Tauri binary so the desktop app boots without a remote gateway.  
  - [#6329](https://github.com/zeroclaw-labs/zeroclaw/issues/6329) — Menu‑bar tray items (quit, restart gateway, copy pairing token, show logs).  
  - [#6339](https://github.com/zeroclaw-labs/zeroclaw/issues/6339) — Universal macOS binary (`lipo`‑merged arm64 + x86_64).  
  - [#6327](https://github.com/zeroclaw-labs/zeroclaw/issues/6327) — Desktop channels overview (mirror web parity).

- **Provider and configuration improvements**:  
  - [#6375](https://github.com/zeroclaw-labs/zeroclaw/issues/6375) — V3 environment‑variable override mechanism for credentials and runtime knobs (replaces removed V1/V2 path).  
  - [#6371](https://github.com/zeroclaw-labs/zeroclaw/issues/6371) — WhatsApp Web `allowed_groups` allowlist.  
  - [#6518](https://github.com/zeroclaw-labs/zeroclaw/issues/6518) — First‑class support for custom OpenAI‑compatible providers (e.g. Kimi K2.5).  
  - [#6522](https://github.com/zeroclaw-labs/zeroclaw/issues/6522) — Web chat tool approval UI for supervised‑mode tool execution (currently backend‑only).

- **Runtime enhancements**:  
  - [#6510](https://github.com/zeroclaw-labs/zeroclaw/issues/6510) — Cron `delivery.mode = "announce"` option to send only the final assistant message.  
  - [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) — Unifying providers architecture (tagged as blocked, but consistently receives votes).

Given the high volume of bug reports, v0.7.6 may prioritise **stability fixes** over new features, with desktop parity (especially the Tauri bundling) and env‑var overrides being the most likely additions.

## 7. User Feedback Summary
**Pain points** (direct from bug reports and feature requests):

- “WhatsApp Web silently stops working after a server‑side update; pairing succeeds but no messages flow.” (alexandme, #6246)  
- “The Docker image’s web dashboard is hidden behind the bind‑mount folder; I have to work around every time.” (rikwade, #6400)  
- “Shell tool calls are refused even when autonomy is set to `full`; the agent can no longer run basic commands.” (sam74S, #6434)  
- “Fallback providers don’t inherit credentials from `config.toml`, which is a security risk and forces a single‑provider setup.” (kmukul123, #6418 — closed, so partially addressed)  
- “I expected `web_search` to work out of the box, but only `web_fetch` works; the search tool returns nothing.” (RampantB, #6373)  
- “The onboarding flow doesn’t let me set a custom model ID for Qwen without dropping to a terminal.” (Vangalle, addressed in PR #5322)

**Satisfaction signals**:

- Users welcomed v0.7.5’s in‑browser onboarding (“finally no CLI required for first run”).  
- The closed #6320 (“Desktop first‑run onboarding parity”) indicates the team listens to desktop users.

## 8. Backlog Watch
Several important issues and PRs lack maintainer response or have remained open for weeks:

- **#5937** ([issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5937)) — “refactor: Unify providers architecture” (open since Apr 20, **blocked** tag, 8 comments, no maintainer assignment).  
- **#6246** ([issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6246)) — WhatsApp Web regression (open since Apr 30, **priority:p1**, no maintainer review).  
- **#6360** ([issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6360)) — “Prompt caching does not work with Telegram” (since May 4, **needs‑maintainer‑review**).  
- **#6373** ([issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6373)) — “`web_search` doesn’t work, `web_fetch` does” (since May 4, accepted but no PR).  
- **#6399** ([issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6399)) — “Custom remote provider sends file paths instead of data URLs” (since May 5, accepted, no PR).  
- **#6400** ([issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6400)) — “Docker bind mount shadows dashboard” (since May 5, accepted, no PR).  
- **#5661** ([PR](https://github.com/zeroclaw-labs/zeroclaw/pull/5661)) — “feat(cron): wire CLI delivery flags” (open since Apr 12, size XL, **risk:high**).  
- **#5254** ([PR](https://github.com/zeroclaw-labs/zeroclaw/pull/5254)) — “fix(provider): sanitize llama.cpp gemma4 tool schemas” (open since Apr 3, **risk:medium**).  
- **#5077** ([PR](https://github.com/zeroclaw-labs/zeroclaw/pull/5077)) — “docs(auth): clarify codex setup” (open since Mar 29, **risk:low**, but stalled).

These items represent **growing technical debt** and risk alienating early adopters if left unaddressed in the next cycle.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*