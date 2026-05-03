# OpenClaw Ecosystem Digest 2026-05-03

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-03 03:50 UTC

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

# OpenClaw Project Digest — 2026-05-03

## Today's Overview
Project activity remains extremely high with **500 issues updated** in the last 24 hours (452 open/active, 48 closed) and **500 pull requests updated** (437 open, 63 merged/closed). Three releases were published today — stable `v2026.5.2` and two betas (`v2026.5.2-beta.3`, `v2026.5.2-beta.2`) — all centred on **npm-first cutover for external plugins**, gateway hot‑path optimisations, and diagnostics improvements. Despite this, the community signals significant stability concerns: a cluster of gateway runtime degradation reports, memory leak risks, and several regressions introduced in recent versions are generating high‑comment issues. The project is clearly shipping fast but is struggling to contain the blast radius of frequent releases, especially for core channels (Telegram, Slack, Discord) and long‑running sessions.

## Releases
Three new versions landed today:

- **v2026.5.2** (stable)  
  [openclaw/openclaw/releases/tag/v2026.5.2](https://github.com/openclaw/openclaw/releases/tag/v2026.5.2)  
  *Highlights:*  
  - External plugin installation now covers diagnostics, onboarding, doctor repair, stale‑configured installs, missing package payloads, and beta‑channel fallback.  
  - Gateway and agent hot paths are leaner (no further detail in provided data).  
  - Artifact metadata handling is expanded for the npm‑first cutover.  
  *No breaking changes or migration notes were explicitly documented in the available data.* However, a critical regression has already been reported (see **Bugs & Stability** – Brave plugin install fails on 5.2).

- **v2026.5.2-beta.3** and **v2026.5.2-beta.2**  
  [openclaw/openclaw/releases/tag/v2026.5.2-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.5.2-beta.3)  
  Both betas contain identical highlights to the stable release (plugin installation, diagnostics, gateway startup improvements). The beta channel is presumably a staging ground for the same set of changes.

## Project Progress (Merged/Closed PRs Today)
63 pull requests were merged or closed today. Among the top 30 by comment count, several important fixes landed:

- **#73554** – `fix(cli): reject missing plugin ids before config writes` — prevents persistent junk config from typo commands.  
- **#75893** – `fix(telegram): chunk markdown‑mode outbound text > 4096 chars` — resolves a regression that broke long Telegram messages in markdown mode.  
- **#76188** – `Performance: chain of issues causing excessive CPU/event‑loop saturation on low‑power hosts` — closed with multiple performance fixes (likely merged).  
- **#75819** – `fix(cli): block gateway‑owned package updates` — stops `openclaw update` from running inside the active gateway process tree.  
- **#76174** – `[Bug]: 2026.4.29 — all openai/* embedded runs hang...` — closed (fix presumably merged; direct curl works, so the bug was in the gateway’s HTTP client or timeout logic).  
- **#76203** – `Performance regression: eager media/web provider discovery...` — closed (fix for pre‑streaming delays).  
- **#76203** – was closed; improves startup time before first streaming token.

Key open PRs that continue to gather attention:  
- **#76420** – `Preserve delivered assistant replies in session repair` (size S, automerge candidate)  
- **#76418** – `fix(web‑search): late‑bind bundled‑owner‑lookup config in sub‑agent sessions`  
- **#76427** – `Keep empty agent replies silent`  
- **#76423** – `fix(agents): block message sends through exec` — fixes a duplicate WhatsApp delivery bug.

The maintainer team appears focused on **session correctness, plugin integrity, and performance regressions**.

## Community Hot Topics
Issues with the highest engagement today reveal widespread frustration with reliability and regression velocity:

- **#73323** – *Gateway runtime degradation: pricing fetch 60s timeouts, Telegram polling stalls, slow RPC* (15 comments, 1 👍)  
  [openclaw/openclaw/issues/73323](https://github.com/openclaw/openclaw/issues/73323)  
  A critical, multi‑subsystem slowdown reproducible across three consecutive releases (4.23/4.25/4.26) on Windows 11 + Node 24. The issue suggests a deep architectural problem in the gateway’s networking/timer management.

- **#48183** – *Feishu monitor state cleanup incomplete – potential memory leak in httpServers Map* (16 comments)  
  [openclaw/openclaw/issues/48183](https://github.com/openclaw/openclaw/issues/48183)  
  A long‑standing (since March) memory leak that remains open. The Map entries are deleted before the HTTP server fully closes, creating a risk of unbounded growth.

- **#47940** – *Heartbeat alternates between sent and ok‑token every cycle — effective interval is 2x* (13 comments)  
  [openclaw/openclaw/issues/47940](https://github.com/openclaw/openclaw/issues/47940)  
  A confusing UX bug: heartbeat fires correctly every 30m but alternates between a real send and a silent `ok‑token`, effectively doubling the configured interval.

- **#72808** – *Silently lost connection to Slack* (11 comments, 2 👍)  
  [openclaw/openclaw/issues/72808](https://github.com/openclaw/openclaw/issues/72808)  
  The agent stopped responding on Slack without any error, forcing manual recovery. Represents a reliability gap for a core channel.

- **#65302** – *Your Updates Are Killing Your Product – A Phenomenon‑Level Project in Self‑Destruct Mode* (9 comments, 6 👍)  
  [openclaw/openclaw/issues/65302](https://github.com/openclaw/openclaw/issues/65302)  
  An impassioned open letter (in English and Chinese) from a Chinese user operator named “Scarlet”. It argues that frequent updates are breaking the product for real users and that the project is losing trust. The high reaction count (6 👍) suggests broad community agreement.

**Underlying needs**: Users are crying out for **stability over feature velocity**. The same few regressions (heartbeat timing, session routing, silent channel drops) reappear across releases. The community wants a “freeze” period to fix the foundation before adding plugin‑first cutover features.

## Bugs & Stability

| Severity | Issue | Description | Status | Fix PR? |
|----------|-------|-------------|--------|---------|
| Critical | [#73323](https://github.com/openclaw/openclaw/issues/73323) | Gateway runtime degradation (60s timeouts, Telegram stalls, RPC slowdowns) across multiple versions | Open | Not yet |
| High | [#48183](https://github.com/openclaw/openclaw/issues/48183) | Feishu memory leak (httpServers Map not cleaned) | Open since March | Not yet |
| High | [#76373](https://github.com/openclaw/openclaw/issues/76373) | Brave plugin install fails on v2026.5.2 – missing `openclaw.extensions`, no beta fallback | Open (5 comments, filed today) | Not yet |
| High | [#76174](https://github.com/openclaw/openclaw/issues/76174) | All `openai/*` embedded runs hang until timeout (2026.4.29) | Closed (fix merged) | [PR #76203](https://github.com/openclaw/openclaw/pull/76203) |
| High | [#74620](https://github.com/openclaw/openclaw/issues/74620) | (implied by PR #76420) Session repair trimming trailing assistant replies | Addressed in PR #76420 | Open PR #76420 |
| Medium | [#72808](https://github.com/openclaw/openclaw/issues/72808) | Silent Slack connection loss | Open | Not yet |
| Medium | [#76188](https://github.com/openclaw/openclaw/issues/76188) | Excessive CPU/event‑loop saturation on low‑power hosts | Closed | Multiple PRs |
| Medium | [#47940](https://github.com/openclaw/openclaw/issues/47940) | Heartbeat effective interval double | Open | Not yet |
| Medium | [#74907](https://github.com/openclaw/openclaw/issues/74907) | Multi‑tool turn replay produces orphan `tool_use` blocks after session compaction (v2026.4.x regression) | Open | Not yet |

**Key observation**: The **Brave plugin installation regression** on the just‑released v2026.5.2 is especially concerning — it suggests the npm‑first cutover may not have been fully validated with all external plugins. The gateway degradation (#73323) has been open for 5 days with 15 comments, no fix PR, and affects three consecutive releases.

## Feature Requests & Roadmap Signals

Active feature requests that appear closest to the project’s current trajectory:

- **#63990** – *Multi‑index embedding memory with model‑aware failover* (5 comments)  
  [openclaw/openclaw/issues/63990](https://github.com/openclaw/openclaw/issues/63990)  
  Request for proper multi‑embedding‑model support in memory. With the plugin‑first architecture maturing, memory resilience is a natural next focus.

- **#66399** – *Process supervisor: graceful signal escalation and drain timeout for exec tool* (5 comments)  
  [openclaw/openclaw/issues/66399](https://github.com/openclaw/openclaw/issues/66399)  
  Proposes escalating from SIGTERM to SIGKILL with a drain timeout, avoiding immediate SIGKILL on exec timeout. This signals growing demand for production‑grade subprocess management.

- **#42840** – *Add MathJax/LaTeX support to Control UI* (6 comments, 4 👍)  
  [openclaw/openclaw/issues/42840](https://github.com/openclaw/openclaw/issues/42840)  
  High user desire for better display of mathematical content in the web UI. Likely to be picked up if the UI team gains capacity.

- **#40786** – *Add .gitignore‑like exclude patterns to backup CLI* (6 comments)  
  [openclaw/openclaw/issues/40786](https://github.com/openclaw/openclaw/issues/40786)  
  Operational quality‑of‑life feature. With growing enterprise adoption, backup flexibility is becoming important.

- **#72629** – *Token‑cost scaling in conversational multi‑agent coordination* (4 comments)  
  [openclaw/openclaw/issues/72629](https://github.com/openclaw/openclaw/issues/72629)  
  A design discussion on quadratic token growth in multi‑agent conversations. The project is likely to invest in smarter context management here.

**Prediction**: The next version will likely include fixes for the **multi‑tool compaction orphan blocks** (#74907) and the **gateway degradation** (#73323), as well as incremental improvements to the plugin installation flow. The multi‑agent token cost scaling (#72629) may see a design RFC.

## User Feedback Summary
- **Frustration with regression velocity**: Multiple users express that “updates are killing the product” (#65302). The same categories of bugs (heartbeat, session routing, channel disconnects) reappear monthly.
- **Pain with channel reliability**: Slack (#72808), Telegram (#41165, #43549, #70628), and Discord (#75346) all have open issues about connections being silently lost or messages not reaching the agent.
- **Performance on low‑power hardware**: #76188 and #73323 highlight that OpenClaw is becoming unusable on Raspberry Pi / NUC / homelab machines due to event‑loop saturation and timeout storms.
- **Occasional positive signals**: The fact that 63 PRs were merged today and three releases shipped shows a highly responsive core team, but users see this as “too much too fast” without adequate testing.

## Backlog Watch
Several important but unattended issues have been open for more than a month:

- **#14785** – *Reduce tool schema token overhead (~3,500 tok/session)*  
  [openclaw/openclaw/issues/14785](https://github.com/openclaw/openclaw/issues/14785)  
  Opened Feb 12, 6 comments, no assignee. A persistent token tax that affects every session. Simple optimisation could reduce costs by thousands of tokens.

- **#13751** – *Feishu plugin: remove dependency on contact:contact.base:readonly for sender name resolution*  
  [openclaw/openclaw/issues/13751](https://github.com/openclaw/openclaw/issues/13751)  
  Opened Feb 11, 6 comments. The Feishu plugin requires a high‑risk org‑wide permission just to resolve a user’s name. A scoped permission alternative has been discussed but not implemented.

- **#38501** – *TUI Ctrl+C can imply cancellation while active run continues*  
  [openclaw/openclaw/issues/38501](https://github.com/openclaw/openclaw/issues/38501)  
  Opened Mar 7, 5 comments. A UX bug that causes confusion — Ctrl+C in the TUI shows “canceled” but the run still completes.

- **#40895** – *Discord Thread Mention Handling Bug*  
  [openclaw/openclaw/issues/40895](https://github.com/openclaw/openclaw/issues/40895)  
  Opened Mar 9, 4 comments. Threads remain “active” after initial mention, causing responses to all subsequent messages regardless of `requireMention`. PR #63230 (open) attempts to add a per‑channel override but does not fix the core logic.

**Call to maintainers**: The tool schema token overhead (#14785) and Feishu permission issue (#13751) are both low‑effort, high‑impact improvements that have been waiting for months. Their continued neglect signals a focus on fire‑fighting rather than proactive quality improvement.

---

*Digest generated from GitHub data retrieved 2026-05-03. All links are to the OpenClaw repository.*

---

## Cross-Ecosystem Comparison

# Cross-Project AI Agent Ecosystem Report — 2026-05-03

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is experiencing an intense period of rapid iteration, with flagship projects shipping multiple releases per week but struggling to maintain stability. The landscape is bifurcated: established projects like OpenClaw and ZeroClaw push architectural overhauls (npm-first plugin cutover, v3 configuration schemas) while smaller projects like NanoBot and NanoClaw demonstrate higher reliability through more measured release cycles. A clear tension has emerged between feature velocity and production stability, with several projects receiving direct community pushback about regression frequency. The ecosystem appears to be at an inflection point where the next 3-6 months will determine which projects transition from experimental to production-grade.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases (24h) | Overall Health |
|---------|---------------------|-------------------|----------------|----------------|
| **OpenClaw** | 500 (452 open) | 500 (437 open) | 3 (1 stable, 2 beta) | **Concerning** — High instability, community frustration, gateway degradation |
| **ZeroClaw** | 50 | 33 | 0 | **Stable but turbulent** — Major v0.8.0 refactor in flight, active bug triage |
| **Hermes Agent** | 50 (44 open) | 50 (46 open) | 0 | **Moderate** — Healthy fix velocity, growing feature discussions |
| **IronClaw** | 20 | 43 | 0 | **High activity** — Reborn architecture overhaul, strong maintainer response |
| **NanoBot** | 3 new | 19 (8 merged) | 0 | **Healthy** — Measured releases, good fix-to-feature ratio |
| **NanoClaw** | 13 | 18 (7 merged) | 0 | **Strong** — Fast bug resolution, active community contributions |
| **NullClaw** | 5 | 16 (15 merged) | 0 | **High throughput** — 15 PRs merged, strong engineering discipline |
| **CoPaw** | 13 | 14 (4 merged) | 0 | **Moderate** — Active contributors but critical MCP hang unsolved |
| **Moltis** | 4 | 3 (1 merged) | 0 | **Steady** — Low volume but responsive, multi-backend sandbox in progress |
| **PicoClaw** | 7 | 8 (2 merged) | 1 nightly | **Moderate** — Nightly builds show rapid iteration but stale PR backlog |
| **LobsterAI** | 0 | 4 (0 merged) | 0 | **Stagnant** — 39-day stale PRs, no new issues or releases |
| **TinyClaw** | 0 | 0 | 0 | **Inactive** — No activity |
| **ZeptoClaw** | 0 | 0 | 0 | **Inactive** — No activity |

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale leader:** With 500 daily issues/PRs, OpenClaw dwarfs every other project in community engagement and commits. It is the de facto reference implementation.
- **Ecosystem founder:** Multiple derived projects (PicoClaw, NanoClaw, CoPaw) explicitly build on OpenClaw's plugin architecture and diagnostic tooling.
- **Channel breadth:** Mature Telegram, Slack, Discord, Feishu support — wider than any single peer.

**Technical approach differences:**
- OpenClaw pursues an **npm-first plugin cutover** for external extensions, while Hermes and NullClaw prefer WASM-based sandboxing. ZeroClaw is also moving toward WASM.
- OpenClaw uses a **heavy gateway architecture** with hot-path optimization; NullClaw (Zig) and ZeroClaw (Rust) aim for minimal binary footprints.
- OpenClaw's release cadence (3 versions/day) is the fastest but also the most destabilizing — no other project ships multiple daily releases.

**Community size comparison:**
- OpenClaw's issue tracker volume (500/day) is 10x the next most active project (ZeroClaw, 50/day).
- However, community sentiment in OpenClaw is notably negative (#65302 "Updates Are Killing Your Product"), while smaller projects receive more positive feedback for reliability.
- OpenClaw's high volume may create **visibility bias** — problems are more visible because more people use it, but the absolute regression rate appears genuinely elevated.

---

## 4. Shared Technical Focus Areas

Requirements emerging independently across multiple projects (evidence of genuine industry need):

| Focus Area | Projects Affected | Specific Needs |
|------------|------------------|----------------|
| **Reasoning model support** | OpenClaw, NullClaw, ZeroClaw, Hermes, Moltis, CoPaw | `reasoning_content` preservation in streaming, DeepSeek compatibility, thinking model context compression |
| **Multi-agent orchestration** | OpenClaw, Hermes, ZeroClaw, IronClaw | A2A protocol, agent-to-agent skill delegation, session routing, sub-agent spawning |
| **Sandboxing & security** | NullClaw, ZeroClaw, Moltis, CoPaw, PicoClaw | Landlock default, risk classification tiers, allowlist/dry-run exec, shell vs WASM isolation |
| **Channel reliability** | OpenClaw, NanoBot, Hermes, ZeroClaw, PicoClaw | Silent disconnects (Slack, Telegram, Discord), mention-only bugs, heartbeat doubling, polling stalls |
| **Memory & context management** | OpenClaw, NanoBot, Hermes, ZeroClaw, CoPaw | Token optimization, history truncation, reasoning content in compression, multi-embedding failover |
| **Cross-platform init support** | NanoClaw, NullClaw, PicoClaw, ZeroClaw | OpenRC compatibility, Docker-free deployment, ARM64 builds, RTC-less hardware |
| **Plugin/extensibility** | OpenClaw, LobsterAI, ZeroClaw, CoPaw | Plugin path persistence, WASM discovery vs install mismatch, npm-first vs local-first |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NullClaw | ZeroClaw | NanoBot | Hermes | IronClaw |
|-----------|----------|----------|----------|---------|--------|----------|
| **Language** | TypeScript/Node | Zig | Rust | TypeScript | TypeScript | Rust |
| **Architecture** | Heavy gateway + plugin host | Minimal binary, no Docker | Microkernel + WASM skills | Lightweight, CLI-first | Plugin host + gateway | Reborn (event-sourced) |
| **Target user** | Power users, homelab | Embedded, low-resource | Developer, self-hosters | Casual, task-focused | Advanced multi-agent | DeFi/trading agents |
| **Release philosophy** | Ship fast, fix later | Conservative, test-heavy | Milestone-based (v0.7.x → v0.8.0) | Measured, patch-focuse | Feature + stability | Architectural refactor |
| **Primary differentiator** | Ecosystem scale | Minimalism (Zig) | WASM skill sandbox | Edge simplicity | A2A/Curator | Trading + NEAR intents |
| **Weakness** | Regression velocity | Fewer channels, docs gap | Heavy refactor in flight | Limited channel breadth | DeepSeek provider bugs | Reborn incomplete |

**Key insight:** No single project excels across all dimensions. OpenClaw leads in ecosystem size but lags in stability. NullClaw wins on resource efficiency but lacks channel depth. ZeroClaw has the most ambitious architectural vision but is mid-transition. This creates space for multiple projects to coexist and compete.

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid iteration, high volatility:**
- **OpenClaw** — Shipping 3 releases/day, but community confidence is eroding. The "updates are killing the product" sentiment is real. Risk: burn-out or fork.
- **ZeroClaw** — High PR/issue velocity with a major v0.8.0 refactor in progress. Healthy contributor ecosystem but heavy breaking changes incoming.

**Tier 2 — High throughput, stabilizing:**
- **NullClaw** — 15 PRs merged in 24h on Zig codebase. Strong engineering discipline. REST Admin API and A2A multi-modal now landed. Maturing rapidly.
- **IronClaw** — Reborn architecture is well-defined. Good maintainer responsiveness. Trading-specific features differentiate it from general-purpose agents.
- **NanoClaw** — Excellent bug fix velocity (readonly DB crash fixed in hours). Growing contributor base. OpenRC support gap emerging.

**Tier 3 — Healthy growth, measured releases:**
- **NanoBot** — 8 PRs merged, good feature-to-bug ratio. WhatsApp media and env-var config are meaningful additions. Community is supportive.
- **Hermes** — Curator feature merged, 6 bugs closed. Active roadmap discussions (A2A, cron memory). Stable but not flashy.
- **CoPaw** — First-time contributors active, but the MCP hang bug (#3640) is a growing black mark on reliability.
- **Moltis** — Low volume but strategic (multi-backend sandbox, i18n). Small community but engaged.

**Tier 4 — Stagnant or inactive:**
- **LobsterAI** — 39-day stale PRs, no new issues, no releases. Plugin path bug (#1879) remains unmerged. Risk of contributor abandonment.
- **TinyClaw, ZeptoClaw** — Zero activity. Effectively dormant.

---

## 7. Trend Signals

**1. Stability crisis in flagship projects** — OpenClaw's community directly demanding a "freeze period" (#65302) mirrors broader industry patterns. The most common bug class across all projects is **regression from rapid releases** (heartbeat timing, session routing, channel disconnects). Value for developers: **prioritize regression testing over new features if deploying agents in production.**

**2. Reasoning model support is the gating factor** — Every project that supports DeepSeek/Gemini/Ollama thinking models has an open bug about `reasoning_content` being dropped or mishandled. This is the single largest cross-project pain point. Value for developers: **vet your agent framework's thinking model support before adopting it for reasoning-heavy workloads.**

**3. Agent-to-agent protocols are becoming strategic** — A2A support is explicitly requested by Hermes and NullClaw communities. OpenClaw and ZeroClaw are building multi-agent session routing. IronClaw's Reborn architecture enables turn coordination. Value for developers: **choose a framework with documented A2A or MCP interoperability — standalone agents will be increasingly isolated.**

**4. Sandbox simplicity is a competitive differentiator** — NullClaw (#882) and ZeroClaw (#5722) are both moving toward Landlock-only sandboxing, eliminating Docker/Firejail dependencies. Users deploying on cheap hardware or OpenRC systems cannot run Docker. Value for developers: **if targeting edge/IoT/ARM deployments, prioritize projects with lightweight sandbox options.**

**5. Configuration management is a growing friction point** — LobsterAI's plugin path deletion, ZeroClaw's Slack token file-vs-env-var confusion, and Hermes's config loss after updates all point to a shared pain: **config systems are not keeping pace with feature growth.** Value for developers: **look for projects with environment-variable-first or structured config schemas (v3 in ZeroClaw, env-var in NanoBot).**

**6. "Self-improving agents" are early-stage but demanded** — Dream Mode (ZeroClaw), Curator (Hermes), and skill consolidation (ZeroClaw) all aim at autonomous improvement. This is the next frontier after basic task execution. Value for developers: **watch ZeroClaw v0.8.0 and Hermes Curator as trendsetters; expect this to become table stakes within 6 months.**

**Bottom line for technical decision-makers:** The ecosystem is still maturing. For production deployments, NanoBot or NullClaw offer the best stability-to-feature ratio today. For ecosystem access and plugin breadth, OpenClaw remains the default despite instability. For multi-agent or trading-specific use cases, Hermes and IronClaw respectively offer unique value. No single project is "ready for enterprise" without substantial evaluation and testing.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-03

## 1. Today's Overview
Project activity remains high, with **19 pull requests updated** in the last 24 hours (8 merged/closed, 11 open) and **3 new issues filed**. No new releases were published. Development momentum continues across multiple fronts — the merged PRs include long-awaited features (WhatsApp media support, environment-variable-based config, Feishu thread isolation) as well as important fixes (exec command guard priority, memory error handling). The open PR queue suggests active work on Discord interactive components, audio transcription unification, and CLI UX improvements. The three open issues are focused on regressions and reliability concerns, indicating that while feature velocity is strong, stability is a growing user focus.

## 2. Releases
None.

## 3. Project Progress (Merged/Closed PRs Today)
Eight pull requests were merged or closed:

- **[#2010 – feat(whatsapp): add media send/receive support](https://github.com/HKUDS/nanobot/pull/2010)** — Closed after a long development cycle (opened March 14). Adds image, audio, video, and document support for WhatsApp channels.
- **[#2218 – feat(security): support `{env:VAR}` syntax for environment variable references](https://github.com/HKUDS/nanobot/pull/2218)** — Allows sensitive config values like API keys to be read from environment variables instead of plain text config files.
- **[#3456 – feat(skills): add create-instance built-in skill + webui remote backend](https://github.com/HKUDS/nanobot/pull/3456)** — Lets a running agent spawn new bot instances via a helper script, and supports GitHub Pages deployment with secret-based auth.
- **[#3419 – fix(provider): preserve reasoning_content when merging consecutive assistant messages](https://github.com/HKUDS/nanobot/pull/3419)** — Fixes a DeepSeek thinking-mode 400 error by retaining `reasoning_content` during message merges.
- **[#3414 – fix(agent): cap recent history section in system prompt](https://github.com/HKUDS/nanobot/pull/3414)** — Truncates the “Recent History” section to 32K characters to prevent system prompt bloat.
- **[#3176 – feat(feishu): thread-scoped sessions, reply_in_thread, non-blocking reaction](https://github.com/HKUDS/nanobot/pull/3176)** — Introduces proper session isolation per Feishu thread and adds interactive reply/reaction support.
- **[#3247 – fix(memory): fall back to raw_archive on LLM error response](https://github.com/HKUDS/nanobot/pull/3247)** — Prevents data loss when `/new` is executed and the LLM returns an error during background archiving.
- **[#3594 – [bug] fix: allow_patterns take priority over deny_patterns in ExecTool](https://github.com/HKUDS/nanobot/pull/3594)** — Reverses the guard logic so user-defined allow patterns can override built-in deny patterns, fixing a usability issue where safe commands were blocked.

## 4. Community Hot Topics
While no issues or PRs have accumulated many comments or reactions in this snapshot, several items indicate areas of high user interest:

- **Issue #3599 – [bug] “Command blocked by safety guard” after upgrade to v0.1.5.post3** – A regression report that is likely generating frustration, as the bot suddenly refuses to execute commands that previously worked. The user notes that a retry succeeds, implying a timing or path-resolution bug. _(0 comments, 0 reactions)_
- **Issue #3595 – [enhancement] Remove the 600 second cap on configuring `exec` timeout** – A clear use-case complaint: long-running tasks (downloads, scripts) are cut off. The request has been addressed by open PR #3596, showing maintainer responsiveness. _(0 comments, 0 reactions)_
- **PR #3583 – [WIP] Improve beta WebUI turn completion and chat isolation** – This work-in-progress PR touches streaming UX and message isolation, a common pain point in multi-chat setups. It has been open since May 1 and is still under review.

Underlying needs: users want **reliability without surprise restrictions** (safety guard regression), **configurability for long-running workloads** (exec timeout), and **polished chat interfaces** (WebUI). The community is actively shaping the agent’s operational flexibility.

## 5. Bugs & Stability
Three bug reports were filed today; fix PRs exist for two of them.

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| [#3599](https://github.com/HKUDS/nanobot/issues/3599) | **High** | Safety guard blocks valid commands after upgrade to v0.1.5.post3. User can retry to succeed, suggesting a transient path check failure. | None yet. |
| [#3597](https://github.com/HKUDS/nanobot/issues/3597) | **Medium** | Agent confused about workspace root; fails to find a file it was told to create. Causes workflow disruption for daily tasks. | None yet. |
| [#3595](https://github.com/HKUDS/nanobot/issues/3595) | **Medium** (enhancement) | Hard timeout cap of 600s on `exec` tool cuts off long-running tasks. | [PR #3596](https://github.com/HKUDS/nanobot/pull/3596) – adds activity-aware timeout controls. |

Additionally, PR [#3587](https://github.com/HKUDS/nanobot/pull/3587) (open) fixes a bug where explicit `reasoningEffort: null` was not properly disabling reasoning; PR [#3588](https://github.com/HKUDS/nanobot/pull/3588) fixes a transcription upload issue for self-hosted Whisper backends.

**Assessment**: The safety-guard regression (#3599) is the most urgent bug, as it directly impacts user trust after a version upgrade. No fix PR is open yet.

## 6. Feature Requests & Roadmap Signals
The most prominent user-requested feature is **removing the hard 600-second timeout** on the `exec` tool ([#3595](https://github.com/HKUDS/nanobot/issues/3595)). The associated PR [#3596](https://github.com/HKUDS/nanobot/pull/3596) introduces _activity-aware timeout controls_, separating hard config-level limits from operation-level timeouts. This is likely to land in the next patch release.

Other signals in the open PR queue that may shape the next minor version:

- **Discord interactive components** ([#3589](https://github.com/HKUDS/nanobot/pull/3589)) – buttons, select menus, modals.
- **CLI UX improvements** ([#3592](https://github.com/HKUDS/nanobot/pull/3592) – Ctrl+C clear line; [#3593](https://github.com/HKUDS/nanobot/pull/3593) – help text for subcommands).
- **Audio unification** ([#3513](https://github.com/HKUDS/nanobot/pull/3513), [#3588](https://github.com/HKUDS/nanobot/pull/3588)) – a unified transcription provider layer plus local Whisper support.
- **Dream / heartbeat controls** ([#3590](https://github.com/HKUDS/nanobot/pull/3590), [#3591](https://github.com/HKUDS/nanobot/pull/3591)) – manual triggers and scope restrictions for automatic consolidation to prevent skill drift.
- **WebUI streaming polish** ([#3583](https://github.com/HKUDS/nanobot/pull/3583)) – better turn completion signals and chat isolation.

These indicate a roadmap focused on **channel richness (Discord, audio), user control (timeout, dream scope, heartbeat), and polished terminal/Web interfaces**.

## 7. User Feedback Summary
Real user pain points captured this period:

- **“Stability regression after update”** – Issue #3599: the safety guard blocks legitimate workspace commands after upgrading to v0.1.5.post3. The user’s workaround (retry) suggests a logic bug rather than a security hardening.
- **“Agent forgets workspace”** – Issue #3597: the agent is confused about which directory is its workspace root, failing to complete a simple write task. User explicitly states the task was “supposed to be saved inside its workspace”, indicating path resolution issues for long-running conversations.
- **“Long-running tasks get killed”** – Issue #3595: the 600-second cap is arbitrary and cuts off downloads or scripts. The user requests configurable limits.

Overall satisfaction seems mixed: users are actively testing NanoBot for real work (drafting articles, running scripts) but encountering hard limits and regressions that make reliability “not yet sufficient.” The swift PR for the timeout cap is a positive signal.

## 8. Backlog Watch
No extremely long-stale issues or PRs are visible in this snapshot. The oldest open item among those updated recently is:

- **[PR #3513 – feat(audio): unify transcription providers and add local Whisper support](https://github.com/HKUDS/nanobot/pull/3513)** – Opened April 28, last updated May 2. This is a substantial feature with two related PRs ([#3588](https://github.com/HKUDS/nanobot/pull/3588) fix), but it has not yet received maintainer approval or merging. Given its impact on audio workflows, it could become a growing pain point if left unmerged for weeks.

Other open PRs are recent (within 3 days) and likely under active review. The project appears to have good maintainer engagement.

---

*Data snapshot: 2026-05-03, based on GitHub activity at HKUDS/nanobot.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-03

## 1. Today’s Overview
The project remains extremely active, with **50 issues and 50 pull requests updated in the last 24 hours** (44 open issues, 46 open PRs). No new releases were cut today, but the community and maintainers are heavily engaged in both feature discussion and bug triage. Notable themes include inter-agent protocol support (A2A), multi-agent orchestration improvements, and a cluster of high-severity fixes for gateway latency, Discord typing loops, and provider credential handling. Six issues and four PRs were closed or merged today, indicating steady progress on stabilising the codebase.

---

## 2. Releases
None today.

---

## 3. Project Progress
**Merged/closed PRs (4 total):**
- [#2524 fix(gateway): isolate Telegram polling from streaming edits to prevent httpx.ReadError](https://github.com/NousResearch/hermes-agent/pull/2524) — closes a P1 streaming crash in the Telegram adapter.
- [#2531 fix: /stop bypasses all replay paths to prevent message replay](https://github.com/NousResearch/hermes-agent/pull/2531) — resolves a P1 bug where `/stop` would be replayed as a user message.
- [#2536 fix(discord): stop persistent typing loop after response completes](https://github.com/NousResearch/hermes-agent/pull/2536) — fixes a P2 Discord issue where the typing indicator never turns off.

**Closed issues (6 total):**
- [#16077 RFC: Curator — background skill maintenance (merged via #16049)](https://github.com/NousResearch/hermes-agent/issues/16077) — new Curator feature reviewed and closed.
- [#19045 Gateway adds ~5s of fixed latency per message (P2, fixed)](https://github.com/NousResearch/hermes-agent/issues/19045) — latency hotfix closed.
- [#2836 Channel name resolution fails with emoji prefixes (P2, fixed)](https://github.com/NousResearch/hermes-agent/issues/2836)
- [#2833 Docker container fails with duplicate mount point (P2, fixed)](https://github.com/NousResearch/hermes-agent/issues/2833)
- [#16677 DeepSeek V4 Pro via OpenRouter causes gateway crash loop (P1, fixed)](https://github.com/NousResearch/hermes-agent/issues/16677)
- [#14829 FTS5 unicode61 tokenizer silently drops CJK characters (P2, fixed)](https://github.com/NousResearch/hermes-agent/issues/14829)

These fixes directly improve stability for Telegram, Discord, Docker, Chinese-language users, and multi-provider setups.

---

## 4. Community Hot Topics
The most engaging discussions this period:

- **[#514 Feature: A2A (Agent-to-Agent) Protocol Support](https://github.com/NousResearch/hermes-agent/issues/514)** — 11 comments, 3 👍. The community strongly backs inter-agent communication via Google’s open A2A standard. This is a high-visibility feature request that complements MCP and would enable Hermes agents to discover and collaborate with agents from other platforms.

- **[#16077 RFC: Curator — background skill maintenance](https://github.com/NousResearch/hermes-agent/issues/16077)** — 5 comments, 3 👍. Closed today after the associated PR was merged. The Curator automatically reviews and maintains agent-created skills, marking a significant improvement in self-improving agent capabilities.

- **[#2704 feat: cron job results written back to conversational memory](https://github.com/NousResearch/hermes-agent/issues/2704)** — 4 comments, 2 👍. Users want scheduled tasks to be queryable in later conversations, highlighting the need for tighter memory integration with cron.

- **[#17199 DeepSeek provider model normalization breaks custom endpoints](https://github.com/NousResearch/hermes-agent/issues/17199)** — 3 comments, reported today. Users configuring custom OpenAI-compatible endpoints (e.g., Volcengine ARK) face two blocking bugs in the `deepseek` provider. No fix PR visible yet.

- **[#19045 Gateway ~5s latency tax](https://github.com/NousResearch/hermes-agent/issues/19045)** — 3 comments, closed quickly. Shows community responsiveness to performance regressions.

Underlying needs: users want **interoperability**, **self-maintenance** of agent skills, **scheduled task memory**, and **reliable multi-provider support**.

---

## 5. Bugs & Stability
**High-severity bugs reported or updated today (P1/P2):**

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#16677](https://github.com/NousResearch/hermes-agent/issues/16677) DeepSeek V4 Pro via OpenRouter crash loop | P1 | Gateway enters crash loop, Telegram bot fails | ✅ Closed |
| [#19045](https://github.com/NousResearch/hermes-agent/issues/19045) 5s latency tax in non-streaming mode | P2 | Every message pays unnecessary delay | ✅ Closed |
| [#19046](https://github.com/NousResearch/hermes-agent/issues/19046) Excessive branding detected by Anthropic API | P2 (unconfirmed) | Agent branding may trigger API warnings | ❌ Open |
| [#19043](https://github.com/NousResearch/hermes-agent/issues/19043) `pyproject.toml` exclude-newer blocks dependency resolution | P2 | `uv pip install` fails for packages without recent releases | ❌ Open |
| [#19036](https://github.com/NousResearch/hermes-agent/issues/19036) Kanban DB profile-aware breaks multi-agent worker flows | P2 | Each profile gets its own isolated database, hindering orchestrator/worker pattern | ❌ Open |
| [#19035](https://github.com/NousResearch/hermes-agent/issues/19035) Feishu code blocks cannot be expanded (only ~2 lines visible) | P2 | Rendering bug specific to Feishu platform | ❌ Open |
| [#19003](https://github.com/NousResearch/hermes-agent/issues/19003) Context compressor ignores reasoning field with Ollama thinking models | P2 | Empty summaries when using DeepSeek-R1, QwQ, etc. | ❌ Open |
| [#17199](https://github.com/NousResearch/hermes-agent/issues/17199) DeepSeek provider bugs: model normalization + base_url override | P2 | Custom endpoints non-functional | ❌ Open |

**Medium-severity issues updated:**
- [#2747 swallowed exception hides local model auto-detection failures](https://github.com/NousResearch/hermes-agent/issues/2747) (P3)
- [#2743 command injection risk via shell=True](https://github.com/NousResearch/hermes-agent/issues/2743) (P2 security)
- [#2744 asyncio.gather discards results on failure](https://github.com/NousResearch/hermes-agent/issues/2744) (P2)
- [#2745 unchecked str.split() index access](https://github.com/NousResearch/hermes-agent/issues/2745) (P3)
- [#18875 Hindsight memory provider crashes gateway when client not installed](https://github.com/NousResearch/hermes-agent/issues/18875) (P3)

---

## 6. Feature Requests & Roadmap Signals
Top user-requested features observed this period:

- **A2A Protocol Support** ([#514](https://github.com/NousResearch/hermes-agent/issues/514)) — strong community traction (11 comments, 3👍). Likely to be considered for next release given its strategic fit with MCP.
- **Cron results written to conversational memory** ([#2704](https://github.com/NousResearch/hermes-agent/issues/2704)) — high usability demand.
- **Compose context files instead of first-match-wins** ([#2835](https://github.com/NousResearch/hermes-agent/issues/2835)) — would allow merging multiple project context files.
- **Delegate task ACP transport override** ([#2653](https://github.com/NousResearch/hermes-agent/issues/2653)) — enables spawning ACP child agents from non-ACP parents.
- **Current-session context buffer** ([#2667](https://github.com/NousResearch/hermes-agent/issues/2667)) — searchable archive of compressed messages during long sessions.
- **Richer local memory with structured retrieval** ([#2184](https://github.com/NousResearch/hermes-agent/issues/2184)) — semantic search beyond flat files.
- **Native payment execution via x402/agentpay-mcp** ([#2919](https://github.com/NousResearch/hermes-agent/issues/2919)) — new commercial use case.
- **Day-of-week session reset schedule** ([#16796](https://github.com/NousResearch/hermes-agent/issues/16796)) — simple config enhancement.

Predictions: A2A support, cron memory write-back, and context composition are the most likely to land in the next minor or major release, given existing PR activity around them.

---

## 7. User Feedback Summary
**Pain points reported in the last 24 hours:**

- “Custom config.yaml values lost after update” ([#2293](https://github.com/NousResearch/hermes-agent/issues/2293)) — a recurring frustration during upgrades.
- “CLI terminal interface hard to read in light background” ([#19039](https://github.com/NousResearch/hermes-agent/issues/19039)) — TUI theme regression.
- “Feishu code blocks cannot be expanded” ([#19035](https://github.com/NousResearch/hermes-agent/issues/19035)) — platform-specific rendering issue.
- “Dependency resolution blocked by exclude-newer setting” ([#19043](https://github.com/NousResearch/hermes-agent/issues/19043)) — breaks `pip install` for stable packages.
- “Excessive branding triggers Anthropic API warnings” ([#19046](https://github.com/NousResearch/hermes-agent/issues/19046)) — potential compatibility issue with Anthropic.

**Positive signals:**
- Rapid closure of the gateway latency bug ([#19045](https://github.com/NousResearch/hermes-agent/issues/19045)) within the same day shows responsive maintainers.
- The Curator feature ([#16077](https://github.com/NousResearch/hermes-agent/issues/16077)) has been merged, indicating ongoing investment in self-improvement capabilities.
- Multiple quality-of-life PRs are open (e.g., Codex quota indicator [#19063](https://github.com/NousResearch/hermes-agent/pull/19063), DuckDuckGo search [#2485](https://github.com/NousResearch/hermes-agent/pull/2485)) — community-driven enhancements are active.

---

## 8. Backlog Watch
Issues and PRs that have been open for an extended period or lack maintainer response:

- **[#514 A2A Protocol Support](https://github.com/NousResearch/hermes-agent/issues/514)** — Open since 2026-03-06, 11 comments, no official maintainer reply. Growing community interest.
- **[#2293 Custom config values lost after update](https://github.com/NousResearch/hermes-agent/issues/2293)** — Open since 2026-03-21, 1 comment. A recurring pain point with no resolution.
- **[#2184 Richer local memory](https://github.com/NousResearch/hermes-agent/issues/2184)** — Open since 2026-03-20, 1 comment. Despite 2👍, no follow-up from maintainers.
- **[#2743 Command injection risk via shell=True](https://github.com/NousResearch/hermes-agent/issues/2743)** — Open since 2026-03-24, security-related, 2 comments. Needs prioritisation.
- **[#19003 Context compressor ignores reasoning field with Ollama thinking models](https://github.com/NousResearch/hermes-agent/issues/19003)** — Open since 2026-05-02, P2, affects a growing number of users deploying local thinking models.

These items would benefit from a maintainer triage response or escalation to the next release milestone.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-03

## 1. Today’s Overview

Project activity remains moderate, with **7 open issues** and **8 pull requests** updated in the last 24 hours. A new **nightly build (v0.2.8-nightly.20260503)** was released, continuing the project’s rapid iteration cycle. Community engagement is focused on two enhancement requests (native email channel and OAuth 2.1 for MCP servers) and a high-priority PID-check crash bug. Two PRs were merged today — a documentation fix for OpenRouter reasoning suppression and a WeChat QR code update. Several stale PRs and bugs continue to linger, indicating a need for maintainer prioritization.

## 2. Releases

- **v0.2.8-nightly.20260503.a94ba821 (Nightly)** — Automated nightly build, may be unstable.  
  **Full Changelog**: [v0.2.8…main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
  No breaking changes or migration notes are provided; the changelog reflects all commits since the last stable tag.

## 3. Project Progress

Merged/closed PRs in the last 24 hours:

- **[[CLOSED] chore: update WeChat group QR code](https://github.com/sipeed/picoclaw/pull/2747)** (#2747) — Replaced the WeChat community QR image (valid through May 9). A minor maintenance task.
- **[[CLOSED] fix(openrouter): document reasoning suppression preset](https://github.com/sipeed/picoclaw/pull/2746)** (#2746) — Adds a preset and documentation to suppress reasoning output from OpenRouter reasoning models (e.g., `nvidia/nemotron-3-super-120b-a12b`). Directly addresses the leak reported in #2745.

No other PRs were merged today. The remaining 6 open PRs represent feature advances and bug fixes that are still in review.

## 4. Community Hot Topics

Most active issues and PRs (by comments/reactions):

- **[[Feature] Add email as native channel](https://github.com/sipeed/picoclaw/issues/2421)** (#2421, 4 comments) — Long-running request for email as a native communication channel. Originated in April, still open with moderate discussion. Underlying need: users in corporate/scientific environments where chat platforms are restricted.
- **[[Feature] Support OAuth 2.1 + PKCE for MCP servers, addable from dashboard](https://github.com/sipeed/picoclaw/issues/2546)** (#2546, 3 comments) — Proposed solution for non-technical users to add OAuth-protected MCP servers by URL. Same UX as Claude.ai’s “Add connector.” Reflects growing demand for enterprise-grade MCP integrations.
- **[[BUG] Singleton PID check doesn't verify process identity — stale PID causes crash loop](https://github.com/sipeed/picoclaw/issues/2720)** (#2720, 1 comment) — High-priority bug causing gateway crash on startup when PID file contains a reused PID (e.g., `systemd-resolved`). The fix is being tracked as a critical stability issue.
- **[[BUG] Gemini API returns HTTP 400 for MCP tools with complex JSON schemas](https://github.com/sipeed/picoclaw/issues/2668)** (#2668, 1 comment, 1 👍) — Affects users integrating Notion or other tools with `$ref`, `anyOf` schemas. Stale label applied; maintainers have not yet responded.

## 5. Bugs & Stability

Bugs reported or updated today, ranked by severity:

1. **HIGH — [Singleton PID check crash loop](https://github.com/sipeed/picoclaw/issues/2720)** (#2720) – Stale PID causes gateway to fail repeatedly. Originally reported Apr 30, updated May 2. No fix PR yet. Critical for deployments on shared hosts.
2. **MEDIUM — [Bash evaluates relative path as absolute path](https://github.com/sipeed/picoclaw/issues/2749)** (#2749) – New bug (May 2) where a command like `archive/SKILL.md` is misinterpreted as root-absolute, breaking workspace checks. **Fix PR exists**: [#2750 `fix(tools): exec guard must not treat relative paths as root-absolute`](https://github.com/sipeed/picoclaw/pull/2750) by same author.
3. **MEDIUM — [OpenRouter reasoning model leaks thinking into assistant content](https://github.com/sipeed/picoclaw/issues/2745)** (#2745) – New bug (May 2). Reasoning preamble appears in final assistant message. **Addressed by documented PR**: [#2746](https://github.com/sipeed/picoclaw/pull/2746) (merged today), which adds suppression preset.
4. **LOW (stale) — [Wrong model IDs in Anthropic dropdown (Android)](https://github.com/sipeed/picoclaw/issues/2665)** (#2665) – Invalid model IDs (dots vs dashes) cause selection failures. Reported Apr 24, stale label.
5. **LOW (stale) — [Gemini 400 on complex JSON schemas](https://github.com/sipeed/picoclaw/issues/2668)** (#2668) – Stale for 8 days without maintainer reply.

Additional active bugs with ongoing fix PRs:
- [DeepSeek reasoning_content dropped in streaming](https://github.com/sipeed/picoclaw/pull/2740) – PR #2740 (open, updated today).
- [Codex streaming + Telegram duplicate retries](https://github.com/sipeed/picoclaw/pull/2462) – PR #2462 (stale, but updated today).
- [Google Antigravity OAuth scope loss on refresh](https://github.com/sipeed/picoclaw/pull/2163) – PR #2163 (stale, over a month old).

## 6. Feature Requests & Roadmap Signals

Top feature requests that may land in the next stable version:

- **Native email channel** ([#2421](https://github.com/sipeed/picoclaw/issues/2421)) – Strong use case from corporate/scientific users. No PR yet, but active discussion.
- **OAuth 2.1 + PKCE for MCP servers** ([#2546](https://github.com/sipeed/picoclaw/issues/2546)) – Mimics Claude.ai’s UX. Would enable non-technical deployments. No associated PR but well-articulated.
- **xAI provider support** ([PR #2260](https://github.com/sipeed/picoclaw/pull/2260)) – Open PR adding xAI compatibility (stale since Apr 2). Could be revived soon given growing interest in alternative providers.

Other roadmap signals: The nightly build cadence suggests the team is preparing for a v0.3.0 release, likely incorporating multiple provider fixes (DeepSeek, OpenRouter, Gemini) and the PID crash fix.

## 7. User Feedback Summary

Real pain points and use cases expressed in recent issues:

- **Email as a primary channel**: Users in corporate, scientific, or conservative environments cannot use chat platforms and rely solely on email. This is a persistent accessibility gap.
- **Simplified MCP server onboarding**: Non-technical users want a “paste URL to add” workflow, similar to Claude.ai. Current shell/Node.js requirements are a barrier.
- **Gemini MCP tool integration broken**: Complex JSON schemas (common in Notion, Airtable tools) cause HTTP 400 errors when using Gemini models. Users who switch between providers are affected.
- **Anthropic model ID mismatch**: Android users cannot select any Anthropic model due to incorrect dropdown values (dots vs dashes). A trivial but frustrating UI bug.
- **Path handling confusion**: Relative paths in Bash tool commands are misinterpreted, breaking workflows that use project-relative file references.
- **Reasoning model leak**: OpenRouter reasoning models (e.g., Nemotron) spill internal reasoning into final responses, damaging user trust and readability. The merged documentation fix is a partial solution, but a deeper fix may be needed.

Overall satisfaction is not directly measured, but the volume of bugs indicates the nightly build is indeed unstable. The community is actively reporting issues, which is a positive health sign.

## 8. Backlog Watch

Issues and PRs that are stale (no maintainer response for >7 days) or have been open for extended periods:

| Item | Type | Age | Status | Notes |
|------|------|-----|--------|-------|
| [#2668 Gemini 400 on complex schemas](https://github.com/sipeed/picoclaw/issues/2668) | Bug | 8 days (stale) | No comment from maintainers | 1 👍, likely affects multiple users |
| [#2665 Wrong Anthropic model IDs](https://github.com/sipeed/picoclaw/issues/2665) | Bug | 9 days (stale) | No comment from maintainers | Android-specific, trivial fix |
| [#2462 Codex streaming + Telegram retries](https://github.com/sipeed/picoclaw/pull/2462) | PR | ~24 days (stale) | No updates since Apr 9 | Fix for two bugs, rebase/merge needed |
| [#2260 xAI provider](https://github.com/sipeed/picoclaw/pull/2260) | PR | ~31 days (stale) | No updates since Apr 2 | Feature PR, may conflict with recent provider changes |
| [#2163 Google Antigravity OAuth scope](https://github.com/sipeed/picoclaw/pull/2163) | PR | ~35 days (stale) | No updates since Mar 29 | Important fix for Cloud Code Assist users |
| [#2630 Web UI datetime](https://github.com/sipeed/picoclaw/pull/2630) | PR | ~10 days (stale) | No updates since Apr 23 | UI improvement, low risk |

These items urgently need maintainer attention to prevent feature lag and user frustration.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-03

## 1. Today's Overview

NanoClaw shows strong, sustained development velocity with **13 issues and 18 pull requests** updated in the last 24 hours. Activity is dominated by bug fixes and community-contributed features, including critical stability patches for the host-sweep loop and the poll-loop, as well as new channel integrations (DeltaChat, Signal reactions, voice transcription V2). Two high-severity bugs (readonly database crash, OneCLI identifier rejection) have already been closed via PRs merged today. Several OpenRC compatibility issues surfaced from a real user deployment, indicating growing adoption beyond systemd environments. The project remains highly responsive: many bug reports received fixes within hours.

## 2. Releases

*No new releases were published in the last 24 hours.*

## 3. Project Progress

**Merged/Closed PRs (7) — major advances:**

- **DeltaChat channel adapter** ([PR #2192](https://github.com/qwibitai/nanoclaw/pull/2192)) — adds a new messaging channel, expanding platform support.
- **OneCLI agent identifier sanitization** ([PR #2179](https://github.com/qwibitai/nanoclaw/pull/2179), closes [#2046](https://github.com/qwibitai/nanoclaw/issues/2046)) — underscores in agent group IDs are now replaced with hyphens to comply with OneCLI requirements; prevents container spawn failures.
- **Host-sweep readonly database fix** ([PR #2183](https://github.com/qwibitai/nanoclaw/pull/2183), closes [#2188](https://github.com/qwibitai/nanoclaw/issues/2188) / [#2196](https://github.com/qwibitai/nanoclaw/issues/2196)) — `deleteOrphanProcessingClaims` now reopens the outbound DB as writable, eliminating the `attempt to write a readonly database` crash on every tick.
- **Poll-loop slash command fix** ([PR #2181](https://github.com/qwibitai/nanoclaw/pull/2181)) — slash commands (e.g., `/clear`) no longer silently fail on warm containers; the poller properly acks and processes them.
- **Atom feed parsing fix** ([PR #2190](https://github.com/qwibitai/nanoclaw/pull/2190)) — `fast-xml-parser` object-formatted `<link>` elements are now handled, preventing `TypeError` crashes in YouTube/Atom feed polls.
- **Andy ops fixes bundle** ([PR #2178](https://github.com/qwibitai/nanoclaw/pull/2178)) — resolves 10 operational issues including Maps 403, Twitter token gaps, container timeouts, and LinkedIn posting limits.
- **V1→V2 migration flow** ([PR #1931](https://github.com/qwibitai/nanoclaw/pull/1931), merged) — experimental automated migration for v1 installs; now part of the setup script.

**Notable open PRs advancing features:**
- Signal reaction support inbound+outbound ([#2203](https://github.com/qwibitai/nanoclaw/pull/2203))
- Voice transcription V2 container-side ([#2003](https://github.com/qwibitai/nanoclaw/pull/2003), follow-up [#2202](https://github.com/qwibitai/nanoclaw/pull/2202) for Signal)
- OpenCode provider + custom model support ([#2201](https://github.com/qwibitai/nanoclaw/pull/2201))

## 4. Community Hot Topics

**Most active issues/PRs (by comments):**
- [#1017](https://github.com/qwibitai/nanoclaw/issues/1017) (open, 2 comments) — request to add percentage to token badge; low priority but long-standing enhancement.
- [#2188](https://github.com/qwibitai/nanoclaw/issues/2188) (closed, 1 comment) — readonly database crash; quickly fixed after report.
- [#2046](https://github.com/qwibitai/nanoclaw/issues/2046) (closed, 1 comment) — OneCLI identifier rejection; fix merged same day.

**Underlying needs:** The community is actively using NanoClaw in production-like scenarios. The readonly database bug (reported by two users independently) highlights the need for robust orphan-claim cleanup in high-turnover environments. The OpenRC installation failures ([#2199](https://github.com/qwibitai/nanoclaw/issues/2199), [#2200](https://github.com/qwibitai/nanoclaw/issues/2200)) and Telegram pairing hang indicate demand for broader init system support.

**Long-running but still active PRs:**
- Matrix E2EE channel + per-group config ([#1624](https://github.com/qwibitai/nanoclaw/pull/1624), last updated today) — major feature awaiting maintainer review.
- Home Assistant MCP integration ([#1327](https://github.com/qwibitai/nanoclaw/pull/1327), updated today) — community-contributed skill.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#2188]/[#2196](https://github.com/qwibitai/nanoclaw/issues/2196) | `host-sweep` crashes every tick due to readonly DB write attempt; stalls session processing | **Closed** via PR #2183 |
| **High** | [#2194](https://github.com/qwibitai/nanoclaw/issues/2194) | WhatsApp LID→phone JID mapping lost on restart → routing failures for all senders | No fix PR yet |
| **High** | [#2200](https://github.com/qwibitai/nanoclaw/issues/2200) | Telegram pairing hangs on OpenRC systems (service never started) | No fix PR yet |
| **Medium** | [#2193](https://github.com/qwibitai/nanoclaw/issues/2193) | `init-first-agent` stores platform_id with channel prefix, causing silent routing failures for WhatsApp | No fix PR yet |
| **Medium** | [#2186](https://github.com/qwibitai/nanoclaw/issues/2186) | CLI channel always produces `cli:local` platform ID → router lookup fails | Fix PR [#2187](https://github.com/qwibitai/nanoclaw/pull/2187) open |
| **Medium** | [#2185](https://github.com/qwibitai/nanoclaw/issues/2185) | Composed CLAUDE.md never imports `CLAUDE.local.md`; per-group memory never loaded | No fix PR yet |
| **Low** | [#2191](https://github.com/qwibitai/nanoclaw/issues/2191) | `migrate-v2.sh` misleading "registered_groups missing" error when `sqlite3` CLI absent | No fix PR yet |
| **Low** | [#2195](https://github.com/qwibitai/nanoclaw/issues/2195) | `add-gmail-tool` assumes single account; no documented workaround for multi-account | No fix PR yet |

**Token efficiency** ([#2189](https://github.com/qwibitai/nanoclaw/issues/2189)) — user reports significant token bloat reducing performance and increasing cost; contributor offers to submit PRs. Not a crash but high impact on user experience.

## 6. Feature Requests & Roadmap Signals

**High-likelihood for next release:**
- **Signal reactions** (PR #2203) — bidirectional reaction support, closely mirrors existing chat-sdk-bridge pattern; likely to merge soon.
- **Voice transcription V2** (PR #2003 + #2202) — container-side transcription with sovereignty model; already reviewed, follow-up for Signal adapter open.
- **OpenCode provider** (PR #2201) — adds a new LLM provider; simple config change, low risk.

**User-requested features that may appear in next minor version:**
- Badge percentage display ([#1017](https://github.com/qwibitai/nanoclaw/issues/1017)) — easy UI enhancement, contributor PR already submitted (#2198).
- Token/perf optimization ([#2189](https://github.com/qwibitai/nanoclaw/issues/2189)) — community member willing to contribute; likely to be accepted if PR aligns with project direction.

**Longer-term signals:**
- Multi-account Gmail support ([#2195](https://github.com/qwibitai/nanoclaw/issues/2195)) — no immediate solution due to OneCLI limitation; may require adapter-level changes.
- OpenRC/init system support — recurring theme from today’s reports; could lead to maintainer documentation or auto-detection improvements.
- Per-group model/effort config (PR #1624) — already implemented in the Matrix PR; may be generalized.

## 7. User Feedback Summary

**Pain points voiced today:**
- Token inefficiency reduces non-coding agent performance and increases costs ([#2189](https://github.com/qwibitai/nanoclaw/issues/2189)).
- Installation failures on OpenRC systems (Docker start, Telegram pairing) block non-systemd users ([#2199](https://github.com/qwibitai/nanoclaw/issues/2199), [#2200](https://github.com/qwibitai/nanoclaw/issues/2200)).
- WhatsApp LID mapping loss after restart breaks routing for all messages ([#2194](https://github.com/qwibitai/nanoclaw/issues/2194)).
- "No reply" from CLI channel due to platform ID namespace bug ([#2186](https://github.com/qwibitai/nanoclaw/issues/2186)).
- Multi-account Gmail users have no documented setup path ([#2195](https://github.com/qwibitai/nanoclaw/issues/2195)).

**Satisfaction signals:**
- Users are actively contributing fixes (e.g., mnolet on token efficiency, cfis on host-sweep, alex-shepel on CLI).
- The project’s fast response (readonly DB bug fixed within hours) builds trust.
- "Really enjoying playing with it" — direct positive quote in [#2189](https://github.com/qwibitai/nanoclaw/issues/2189).

## 8. Backlog Watch

| Item | Activity | Needs Maintainer Attention |
|------|----------|----------------------------|
| [#1624](https://github.com/qwibitai/nanoclaw/pull/1624) — Matrix E2EE + per-group config (PR) | Open since Apr 4, last updated May 2 | **Yes** — large feature, no maintainer review in a month; community eager. |
| [#1327](https://github.com/qwibitai/nanoclaw/pull/1327) — Home Assistant MCP skill (PR) | Open since Mar 22, updated May 2 | **Yes** — similar situation; could benefit from review. |
| [#1017](https://github.com/qwibitai/nanoclaw/issues/1017) — badge percentage (issue) | Open since Mar 13, low priority | **Low** — enhancement, but corresponding PR #2198 now open. |
| [#2189](https://github.com/qwibitai/nanoclaw/issues/2189) — token optimization (issue) | Opened May 2, no maintainer reply | **Watch** — user offered PRs; maintainer acknowledgement would encourage contribution. |
| [#2194](https://github.com/qwibitai/nanoclaw/issues/2194) — WhatsApp LID mapping (issue) | Opened May 2, no comments | **High risk** — affects all WhatsApp message routing on every restart; no fix yet. |
| [#2200](https://github.com/qwibitai/nanoclaw/issues/2200) — Telegram OpenRC (issue) | Opened today, no response | **New** — blocking for OpenRC users; need diagnosis or workaround. |

**Recommendation:** Prioritize review of Matrix and Home Assistant PRs to unblock community innovation. The WhatsApp LID mapping bug should be escalated given its severity for real-world usage.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-03

## 1. Today’s Overview
The project saw **heavy engineering activity** in the last 24 hours: 15 pull requests were merged or closed and 1 remains open, while 5 open issues were updated — including one freshly filed today. No new release was cut. The bulk of changes target compatibility fixes (Zig 0.16 regressions), security hardening (sandbox defaults, anti-spoofing, risk classification), and REST Admin API completion. A new sandbox issue (#882) proposes replacing the `auto` backend probing with a Landlock default on Linux, indicating a shift toward simpler, lower-dependency deployment. Overall, the project is stable but actively patching production regressions from the Zig 0.16 migration and refining its security model.

## 2. Releases
*No new releases this period.* The latest release remains dated prior to this digest cycle.

## 3. Project Progress (Merged/Closed PRs)
The following **15 PRs** were closed or merged in the last 24 hours, representing significant forward motion:

- **#880** (merged) – `feat(security): wrap web_fetch and web_search output with anti-spoofing boundaries` – Adds random boundary IDs and homoglyph folding to prevent prompt injection.  
- **#856** (merged) – `fix(service): harden SysVinit script for RTC-less hardware` – Improves service boot ordering for NTP and hardware without real-time clock.  
- **#878** (open) – `fix(compat): use nanosleep on POSIX in thread.sleep to actually suspend OS thread` – Still open; addresses gateway accept-loop CPU spin.  
- **#876** (merged) – `fix(compat): replace readSliceShort with readVec in Stream.read` – Unblocks HTTP/1.1 keep-alive clients (e.g., curl).  
- **#873** (merged) – `fix: Zig 0.16 Mattermost empty-body POST and gateway accept-loop CPU spin` – High-severity regression fix for Mattermost-connected agents.  
- **#872** (merged) – Duplicate/alternative of #873.  
- **#780, #771, #770** (merged) – Three-part **REST Admin API** series: config mutation, channel status, runtime status, model listing, cron jobs, MCP servers, sessions, memory.  
- **#877** (merged) – `fix(channels/mattermost): finalize allocating writer body before curlPost` – Fixes empty-body POST after Zig 0.16.  
- **#761** (merged) – `fix(cli): filter streamed tool-call markup` – Prevents raw `<tool_call>` from leaking to terminal.  
- **#685** (merged) – `fix(error_classify): handle msg field and image+not-supported pattern` – Better error handling for non-OpenAI providers.  
- **#875** (merged) – `security: add 3-tier risk classification and exec-prefix stripping` – Introduces medium-risk tier (curl, wget, etc.) and fixes allowlist bypass. Closes #167.  
- **#687** (merged) – `feat(gateway): make HTTP body size limit and request timeout configurable`.  
- **#686** (merged) – `feat(a2a): multi-modal support` – Agent card capability, inline data forwarding, vision probe.  
- **#863** (merged) – `feat(capabilities): add colored table format for channels with TTY detection`.

## 4. Community Hot Topics

| Issue/PR | Comments | 👍 | Summary |
|----------|----------|----|---------|
| [#882 – sandbox: default to Landlock on Linux](https://github.com/nullclaw/nullclaw/issues/882) | 1 | 0 | Fresh issue proposing removal of Firejail/Bubblewrap probing at startup. Highlights recurring breakage (#…). |
| [#871 – web_search impractical on low-resource devices](https://github.com/nullclaw/nullclaw/issues/871) | 2 | 0 | User reports Brave API key requirement and lack of direct DuckDuckGo support hampers use on cheap hardware. |
| [#865 – CLI shows ctrl characters for arrow keys](https://github.com/nullclaw/nullclaw/issues/865) | 1 | 0 | Terminal input broken; up/down/left/right produce garbage. |
| [#866 – curl post fails even if curl on allowlist](https://github.com/nullclaw/nullclaw/issues/866) | 1 | 1 | Allowlist bypass? User experiences blocked POST despite configuration. |
| *PR* [#880 – anti-spoofing boundaries](https://github.com/nullclaw/nullclaw/pull/880) | 0 | 0 | Security enhancement inspired by OpenClaw (external content wrapping). |

**Underlying needs**: The community is pushing for **lower resource requirements** (no Docker, no API key dependencies, simpler sandboxing) and **robust terminal UX** (keyboard input, CLI readability). Security concerns around prompt injection and command allowlisting remain top of mind.

## 5. Bugs & Stability

| Severity | Issue | Status | Fix PR Exists? |
|----------|-------|--------|----------------|
| **High** | [#882 – Sandbox probing failures on startup](https://github.com/nullclaw/nullclaw/issues/882) | Open (new) | Proposal only; no PR yet. |
| **High** | [#871 – web_search unusable on low-resource devices](https://github.com/nullclaw/nullclaw/issues/871) | Open | No PR; feature request. |
| **Medium** | [#865 – CLI arrow key handling broken](https://github.com/nullclaw/nullclaw/issues/865) | Open | No PR yet. |
| **Medium** | [#866 – curl POST blocked despite allowlist](https://github.com/nullclaw/nullclaw/issues/866) | Open | No PR yet; potential regression from recent risk classification changes. |
| **Critical (fixed)** | Gateway 100% CPU & Mattermost empty body (#873/#877) | Closed | Fixed via #873, #877. |

**Note**: The high-severity Mattermost regression (Zig 0.16) was resolved in today’s merges. No crashes reported in last 24h.

## 6. Feature Requests & Roadmap Signals

- **Default to Landlock on Linux** (#882): A strong signal that the team wants to eliminate external tool dependencies (Firejail, Bubblewrap, Docker) and simplify sandboxing. Likely to land in next minor release.
- **Direct DuckDuckGo / no-API-key web search** (#871): Addresses core use case on cheap devices. Could become a configurable backend option in v0.10 or later.
- **REST Admin API** (PRs #770, #771, #780): Now merged; will appear in next release. Allows lightweight clients (menubar, iOS, CLI dashboards) to inspect and control the agent.
- **Multi-modal A2A** (#686): Merged; prepares NullClaw for image payloads over the Agent-to-Agent protocol.

## 7. User Feedback Summary

- **Pain Points**: 
  - Zig 0.16 migration introduced two critical regressions (Mattermost messaging, CPU spin), now fixed.
  - CLI missing basic readline/termios support (#865) frustrates daily interactions.
  - Curl allowlist still not working (#866) undermines users’ trust in the sandbox.
  - Web search requires external API key on low-resource devices (#871), limiting adoption on Raspberry Pi / older hardware.

- **Satisfaction**: 
  - Positive reception for the REST Admin API (no new dependencies, small binary increase).
  - Security improvements (anti-spoofing boundaries, risk tiers) are praised as proactive.
  - The colored capabilities table (#863) was well-received.

- **Use Cases Observed**:
  - Lightweight automation on cheap VPS/devices (use of `curl`, `wget`).
  - Mattermost-integrated agents in production.
  - CLI-based interaction for headless environments.

## 8. Backlog Watch

| Item | Age | Status | Why It Matters |
|------|-----|--------|----------------|
| [#820 – How to install Zig on Debian?](https://github.com/nullclaw/nullclaw/issues/820) | 19 days | Open | Documentation gap; may block new users. No maintainer response yet. |
| [#866 – curl POST blocked despite allowlist](https://github.com/nullclaw/nullclaw/issues/866) | 10 days | Open | Has 1 👍; may be a regression after PR #875 (risk classification). Needs investigation. |
| [#865 – CLI ctrl characters](https://github.com/nullclaw/nullclaw/issues/865) | 10 days | Open | Terminal usability issue; no activity for 10 days. |
| [#871 – web_search impractical](https://github.com/nullclaw/nullclaw/issues/871) | 8 days | Open | User feature request with 2 comments; no maintainer label. |

**Recommendation**: Maintainers should triage #882 quickly (it already references previous breaking issues). The documentation issue #820 and the allowlist regression #866 deserve prompt attention as they affect onboarding and security trust.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-03

## 1. Today’s Overview

IronClaw is in a high‑activity phase, with 20 issues and 43 pull requests updated in the last 24 hours. The majority of open work is concentrated on the **Reborn** architecture overhaul – a host‑layer restructuring that touches turn coordination, runtime obligations, and conversation binding. Bug‑fix velocity is also strong: 5 issues were closed and 6 PRs merged/closed today, including a re‑fix for a critical `thoughtSignature` regression in Gemini 3.x SSE handling. The project is shipping no new releases today, but a swarm of infrastructure, CLI, and Docker‑related PRs indicates the team is actively hardening the codebase alongside the Reborn transition.

## 2. Releases

No new releases were published today. The latest available version remains `ironclaw-v0.27.0-8-g749fe9da` (referenced in Issue #3214).

## 3. Project Progress

**Merged/Closed PRs (6 items noted):**

- **#3105** (closed) – Staging fix for Telegram channel activation on headless servers; adds WASM channel fallback.
- **#3214** (closed) – Bug fix: `thoughtSignature` dropped in Cloud Code SSE handler (Gemini 3.x). See *Bugs & Stability*.
- **#3144, #3147, #3145** (all closed) – Three Reborn enhancement items: wired `EnforceResourceCeiling` into runtime/sandbox; wired built‑in obligation audit records to production event sinks; defined background process obligation reconciliation lifecycle.

**Key features advanced:**

- **Reborn architecture** – A series of “definition” issues (#3193, #3195, #3198, #3199, #3202, #3204) for conversation binding, crate boundaries, public APIs, turn runner execution, persistence schemas, and transcript storage were all created and updated. This signals that the Reborn design is being fleshed out rapidly.
- **CLI enhancements**: New `ironclaw backup --quick` (#3178), `ironclaw import backup` (#3186), and `ironclaw insights` (#3177) PRs are open for review.
- **NEAR Intents trading foundation**: Three large PRs (#3218, #3207, #3211) introduce an intents‑trading agent skill, paid research layer, and trial mode.
- **Docker**: PR #3208 adds `linux/arm64` build support (closes #3168).
- **UI & Admin**: PR #3209 debounces duplicate user creation; PR #3210 fixes misleading "Configure" button for optional‑auth tools.
- **LLM fixes**: PR #3215 re‑fixes Gemini `thoughtSignature`; PR #3213 allows workspace identity override; PR #3206 coerces numeric‑string guardrails for tools.

## 4. Community Hot Topics

The most actively discussed items (by comment count within the last 24 hours):

- **Issue #3016** (3 comments) — *Reborn cutover blocker: add reference AgentLoopHost facade*. This is a key architectural dependency for the Reborn project. Contributors are discussing how the facade interacts with the TurnCoordinator and run‑class profiles.
- **Issue #90** (2 comments) — *Audio pipeline (speech‑to‑text, text‑to‑speech)*. A long‑standing feature that has resurfaced as voice notes become a priority for WhatsApp integration.
- **Issue #3214** (1 comment) — The `thoughtSignature` bug (now closed) attracted rapid attention from the fix author and maintainers.
- **Issue #3013** (1 comment) — *Reborn cutover blocker: add kernel TurnCoordinator*. Another Reborn core component being debated.
- **Issue #2344** (1 comment) — *Web UI console errors on page load*. A QA‑flagged issue that remains open, likely because the Reborn frontend refactors are in flight.

**Underlying needs**: The community is clearly invested in the Reborn architectural shift, both for performance (execution model) and correctness (turn admission, persistence). The audio pipeline (#90) responds to a clear user demand for voice‑based interaction on messaging channels.

## 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR? | Status |
|----------|-------|---------|---------|--------|
| **Critical** | [#3214](https://github.com/nearai/ironclaw/issues/3214) | `thoughtSignature` dropped in Cloud Code SSE handler – causes HTTP 400 `INVALID_ARGUMENT` on Gemini 3.x tool calls. Regression from earlier fixes. | [#3215](https://github.com/nearai/ironclaw/pull/3215) (open) | Closed |
| **High** | [#3201](https://github.com/nearai/ironclaw/issues/3201) | Tool use for DeepSeek (deepseek-v4-flash) not working – error on asking current news. No fix PR yet. | None | Open |
| **Medium** | [#2344](https://github.com/nearai/ironclaw/issues/2344) | Web UI console errors on page load (TypeError, ReferenceError, CSP violations) on staging. | Not directly addressed; may be fixed by frontend refactors. | Open |
| **Low** | [#2818](https://github.com/nearai/ironclaw/issues/2818) | Installer fails on `x86_64-unknown-linux-gnu` for v0.26.0. | Closed (likely fixed by subsequent release changes). | Closed |

- **Closed today**: #3214 (re‑fix via #3215), #2818 (likely resolved), #3144/#3147/#3145 (Reborn enhancements).
- **Regression risk**: #3214 was a regression from earlier fixes (#1565, #1752). The fix author (abbyshekit) identified that the upstream SSE handler was never fully patched.

## 6. Feature Requests & Roadmap Signals

**User‑requested features visible today:**

- **Audio pipeline** (#90) – Speech‑to‑text, text‑to‑speech for voice notes. Priority P1‑P2; could land soon given WhatsApp channel momentum.
- **ARM64 Docker support** (#3168) – Now addressed by PR #3208 (open). Expected in next release.
- **Magic‑link onboarding for pilot users** (PR #3187) – Invitation system for managed deployments.
- **NEAR Intents trading agent** (PRs #3207, #3211, #3218) – A sophisticated trading skill with backtesting, paid research, and trial mode.

**Roadmap signals**: The **Reborn** architecture is the dominant theme. The flurry of definition issues (#3193–3204) strongly suggests the next version (likely v0.28.0) will ship a refactored turn coordination layer. The addition of `EventProjectionService` (PR #3212) hints at a move toward event‑sourced persistence, which could unify Reborn and legacy stores.

## 7. User Feedback Summary

**Pain points**:
- Gemini 3.x tool calls fail silently for some users (#3214) – fixed today.
- DeepSeek tool use broken (#3201) – no fix yet.
- Users on ARM64 cannot run official Docker images (#3168) – fix in review.
- Duplicate user creation in admin UI (#3083) – fix in review (#3209).
- Misleading “Configure” button on portfolio extension (#3081) – fix in review (#3210).

**Use cases**:
- Portable backups and migration (`ironclaw backup --quick` and `import backup`) – addresses a clear pain point for self‑hosters.
- CLI `insights` command for usage analytics without log scraping – valued by operators.
- WASM channel fallback for headless servers (PR #3105) – solves a deployment friction point.

**Satisfaction factors**: The rapid turnaround on the `thoughtSignature` bug (issue opened and closed within ~24 hours) demonstrates strong maintainer responsiveness. The community also benefits from the many PRs contributed by newcomer `abbyshekit`, who is driving both fixes and new features.

## 8. Backlog Watch

| Item | Age (since creation) | Notes |
|------|---------------------|-------|
| [#90 – Audio pipeline](https://github.com/nearai/ironclaw/issues/90) | ~79 days (2026‑02‑14) | Long‑standing feature; P1 but no visible PR. May be blocked by Reborn refactors. |
| [#2344 – Web UI console errors](https://github.com/nearai/ironclaw/issues/2344) | ~22 days (2026‑04‑11) | QA‑flagged; no maintainer response in last 24h. Likely tied to frontend reworks. |
| [#2700 – Descriptive chat titles](https://github.com/nearai/ironclaw/pull/2700) | ~12 days (2026‑04‑20) | Large PR replacing hex hashes in sidebar. Open with no recent activity; may need re‑review after Reborn changes. |
| [#3016 – AgentLoopHost facade](https://github.com/nearai/ironclaw/issues/3016) | ~5 days | Key Reborn blocker; discussed but no PR yet. |

**Maintainer attention needed**: The audio pipeline (#90) is a notable gap – despite being labelled P1, it has not moved in months. The Web UI console errors (#2344) remain a user‑visible defect that could erode confidence in staging. The descriptive chat titles PR (#2700) is a large community contribution that appears stalled.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI Project Digest — 2026-05-03

### Today’s Overview

The project saw no new issues or releases in the last 24 hours, but four pull requests received updates, indicating continued development and review activity. None of these PRs were merged or closed today, suggesting either ongoing refinement or pending maintainer decisions. The most notable new contribution is PR #1879, which addresses a configuration syncing bug that silently discards manually-added plugin load paths. Three other PRs (#813, #1181, #1191) are marked as stale but received maintenance attention (updated today). Overall, the project is in a steady state with active open PRs but no immediate releases or regression reports.

### Releases

No new releases were published. The latest release remains unknown (data shows “None”).

### Project Progress

No pull requests were merged or closed in the last 24 hours. The four open PRs that were updated are the only signs of progress:

- **#1879** (fix: preserve manually-added plugin load paths on config sync) – a new, unmerged fix.
- **#813** (feat: add MiMo V2 Pro and MiMo V2 Omni models for Xiaomi channel) – a feature PR from March 25 that is now stale.
- **#1181** (fix: hide OpenClaw main agent sessions from session list) – a fix for user confusion, stale since April 1.
- **#1191** (fix: resolve notification channel filtering defects for scheduled tasks) – a multi-bug fix, stale since April 1.

The absence of merges suggests the team may be reviewing these changes more thoroughly or waiting for additional feedback.

### Community Hot Topics

No issues or PRs received comments or reactions in the recorded data (all “comments: undefined”, 👍: 0). However, the four updated PRs are the main focus:

| PR | Title | Created | Updated | Key Topic |
|----|-------|---------|---------|-----------|
| [#1879](https://github.com/netease-youdao/LobsterAI/pull/1879) | fix: preserve manually-added plugin load paths on config sync | 2026-05-02 | 2026-05-02 | Plugin path persistence |
| [#813](https://github.com/netease-youdao/LobsterAI/pull/813) | feat(config): 小米渠道新增 MiMo V2 Pro 和 MiMo V2 Omni 模型 | 2026-03-25 | 2026-05-02 | Xiaomi model support |
| [#1181](https://github.com/netease-youdao/LobsterAI/pull/1181) | fix(cowork): hide OpenClaw main agent sessions from session list | 2026-04-01 | 2026-05-02 | UI/UX confusion |
| [#1191](https://github.com/netease-youdao/LobsterAI/pull/1191) | fix(定时任务): 修复通知渠道过滤缺陷，升级渠道选择器显示体验 | 2026-04-01 | 2026-05-02 | Notification channel usability |

**Underlying needs**: Users want configuration to survive automated syncs (#1879), expect new AI model availability from Xiaomi (#813), demand cleaner UI without internal sessions (#1181), and require working notification channel selection with human-readable names (#1191). All reflect real friction points in daily use.

### Bugs & Stability

No new bugs, crashes, or regressions were reported in the last 24 hours. The open PRs target existing bugs:

- **High severity** (data loss): PR #1879 fixes a bug where manually-added plugin paths are silently discarded when LobsterAI writes its config file. This could break community-installed plugins like `memory-lancedb-pro`. A fix exists but is not yet merged.
- **Medium severity** (UI confusion): PR #1181 prevents internal OpenClaw sessions from appearing in the user-facing cowork session list. While not a crash, it degrades user experience.
- **Medium severity** (functionality gap): PR #1191 addresses three bugs: missing POPO/WeChat channels in scheduled task notification selectors, incorrect “not supported” label for WeChat, and raw channel codes shown instead of human-readable names. Fix is proposed.

No fix PRs exist for any new bugs beyond these.

### Feature Requests & Roadmap Signals

The only feature-level request visible is PR #813, which adds two new Xiaomi models (`mimo-v2-pro`, `mimo-v2-omni`) to the provider configuration. This aligns with keeping the AI provider catalog up-to-date with platform releases. Given that this PR has been open since March 25 and remains unmerged, it may be waiting for testing or broader model support. It is a strong candidate for inclusion in the next minor release.

No other feature requests were recorded in the last 24 hours.

### User Feedback Summary

While no direct user comments were captured, the PR summaries reveal clear pain points:

- **Plugin path loss** (#1879): Users who manually install community plugins find their modifications overwritten after config sync. This indicates dissatisfaction with configuration management.
- **UI clutter** (#1181): The appearance of internal heartbeat/cron sessions in the cowork session list causes user confusion. The hardcoded `[OpenClaw]` title is not intuitive.
- **Notification channel issues** (#1191): Users cannot select POPO or WeChat for scheduled task notifications, and channel labels show raw codes like `moltbot-popo`. This creates a poor user experience for a high-value feature (timed notifications).
- **Model support gaps** (#813): Users of Xiaomi model APIs cannot use the latest V2 Pro and Omni models through the LobsterAI interface, potentially forcing them to switch tools.

All point to real use cases (plugin extensibility, multi-agent workflows, automated notifications, diverse AI providers) where LobsterAI currently falls short.

### Backlog Watch

Three pull requests have been open for over a month without merging and are marked as stale. They require maintainer attention:

| PR | Title | Created | Last Updated | Days Open | Risk if Ignored |
|----|-------|---------|--------------|-----------|-----------------|
| [#813](https://github.com/netease-youdao/LobsterAI/pull/813) | feat: add MiMo V2 Pro and MiMo V2 Omni models | 2026-03-25 | 2026-05-02 | 39 | Users may switch to other tools for Xiaomi models |
| [#1181](https://github.com/netease-youdao/LobsterAI/pull/1181) | fix: hide OpenClaw main agent sessions | 2026-04-01 | 2026-05-02 | 32 | Persistent user confusion / poor UX |
| [#1191](https://github.com/netease-youdao/LobsterAI/pull/1191) | fix: notification channel filtering/display | 2026-04-01 | 2026-05-02 | 32 | Scheduled task notifications remain broken for some channels |

These three PRs together address both functional bugs and user experience improvements. Their age suggests they may need rebase or re-review. The most critical is #813 (feature addition for a major AI platform) and #1879 (data loss prevention) which is newer but equally urgent.

No long-unanswered issues were recorded (0 issues total in the data).

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest — 2026-05-03

### 1. Today's Overview

Moltis is in a steady development phase with moderate activity over the last 24 hours: 4 issues were updated (all open), and 3 pull requests saw updates—including one merged PR. No new releases were cut. The community is actively filing bugs and feature requests, while core contributors continue to push infrastructure improvements like multi-backend sandbox support and Matrix OIDC debugging. The project appears responsive but faces a notable DeepSeek integration bug that may require immediate attention.

### 2. Releases

No new releases in the last 24 hours.

### 3. Project Progress

One pull request was merged today:

- **[#339 – feat(i18n): add zh-TW Traditional Chinese locale support](https://github.com/moltis-org/moltis/pull/339)** (merged)  
  Adds full Traditional Chinese (Taiwan) UI translations to both macOS and web apps, including locale detection and language selection. This advances the project's internationalisation coverage.

Two open PRs continue to receive updates:

- **[#942 – feat(sandbox): remote & multi-backend sandbox support](https://github.com/moltis-org/moltis/pull/942)** (open, last updated today)  
  Enables sandboxed command execution on cloud deployments where Docker-in-Docker is unavailable, with providers for Docker, Firecracker, Vercel, and Daytona.

- **[#957 – fix(matrix): add debug logging for OIDC registration](https://github.com/moltis-org/moltis/pull/957)** (open, last updated today)  
  Adds diagnostic logging for Matrix OIDC flows and deduplicates redirect URI normalisation, helping operators troubleshoot `invalid_redirect_uri` errors.

No other closed/merged PRs were reported.

### 4. Community Hot Topics

All Issues and PRs updated today have zero or one comment, so activity is low. The most notable items by subject matter:

- **[Issue #959 – DeepSeek reasoning_content bug](https://github.com/moltis-org/moltis/issues/959)** (1 comment)  
  Reports that the `thinking mode` for DeepSeek requires passing back `reasoning_content` to the API, and currently fails. This is likely a high-impact bug for users of DeepSeek's reasoning models.

- **[Issue #960 – SwarmScore portable trust rating for AI agents](https://github.com/moltis-org/moltis/issues/960)** (0 comments)  
  An external proposal to integrate a portable reputation system for AI agents based on verified execution history. No maintainer response yet. This could signal community interest in agent trust and safety.

- **[Issue #958 – Outdated docs for local TTS (Coqui) provider setup](https://github.com/moltis-org/moltis/issues/958)** (0 comments)  
  Documentation links to archived/unmaintained repositories. A straightforward documentation fix.

- **[Issue #956 – Image generation via OpenAI Codex OAuth](https://github.com/moltis-org/moltis/issues/956)** (0 comments)  
  Requests adding `gpt-image-2` support through OpenAI Codex OAuth. Indicates demand for multimodal content generation.

**Underlying needs:** Users are hitting real integration bugs (DeepSeek reasoning), seeking improved documentation accuracy (TTS), and asking for new capabilities (image gen, agent reputation). The low comment count may reflect the project's relatively small but active user base.

### 5. Bugs & Stability

| Issue | Severity | Summary | Fix PR? |
|-------|----------|---------|---------|
| [#959 – DeepSeek reasoning_content must be passed back](https://github.com/moltis-org/moltis/issues/959) | **High** | Chat sessions using DeepSeek's thinking mode fail because the API requires sending back the `reasoning_content` field. No workaround mentioned. | No open fix PR yet |
| [#958 – Outdated TTS docs](https://github.com/moltis-org/moltis/issues/958) | Low | Documentation links to abandoned repos, but no functional impact. | None needed (docs fix) |

**Severity ranking:** The DeepSeek bug is the most critical as it breaks a core feature (reasoning model support) for users of that provider. No fix PR exists yet, so maintainers should prioritise investigation.

### 6. Feature Requests & Roadmap Signals

Several user-submitted features emerged today:

- **[#956 – Image generation (gpt-image-2) via OpenAI Codex OAuth](https://github.com/moltis-org/moltis/issues/956)**  
  Likely to be well-received as AI image generation becomes standard. Could be bundled with existing OpenAI integration.

- **[#960 – SwarmScore portable reputation for agents](https://github.com/moltis-org/moltis/issues/960)**  
  More ambitious; would require a new trust system. Unlikely to land in the next minor release unless maintainers show interest.

- **[#942 – Remote & multi-backend sandbox support](https://github.com/moltis-org/moltis/pull/942)** (in-progress PR)  
  This is a major infrastructure enhancement poised for merge. It addresses a real pain point for cloud deployments and is likely to appear in the next version.

- **[#957 – Matrix OIDC debug logging](https://github.com/moltis-org/moltis/pull/957)** (in-progress)  
  This is a reliability fix, not a feature, but it shows focus on Matrix interoperability.

**Prediction for next version:** Image generation support and the sandbox multi-backend PR are the most likely additions. The SwarmScore proposal is further out.

### 7. User Feedback Summary

- **Pain point:** DeepSeek reasoning mode is unusable – user reported the error and likely expects a swift fix.
- **Dissatisfaction:** Outdated documentation for local TTS (Coqui) – a user noted it points to archived repos. This is a minor but consistent frustration.
- **Use case demand:** Image generation via OpenAI Codex, and a portable trust/rating system for AI agents, indicating users want both utility and safety features.
- **Overall sentiment:** The community is actively reporting issues and proposing enhancements, which suggests engagement. No strong negative tone, but the lack of responses on some issues may leave submitters waiting.

### 8. Backlog Watch

No issues or PRs in the backlog that have been unanswered for an extended period. All new items were created yesterday (2026-05-02). The oldest open PR is:

- **[#942 – feat(sandbox): remote & multi-backend sandbox](https://github.com/moltis-org/moltis/pull/942)** (opened 2026-04-30, last updated today)  
  This is a substantial feature PR that has been open for 3 days. It has been actively updated, so it is not stale, but it would benefit from a maintainer review and potential merge.

**No long-unanswered important issues identified.** The project's issue tracker appears well-maintained with recent activity.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-03

## Today's Overview
Activity remains high with **13 issues** and **14 pull requests** updated in the last 24 hours. The project shows a healthy mix of bug reports, feature requests, and community contributions, including several first-time contributors. One critical bug (MCP client hang) is actively discussed but not yet resolved. No new releases were published today. Community attention is concentrated on **model fallback mechanisms** and **conversation memory reliability** – recurring themes in recent weeks.

## Releases
**No new releases today.** The last recorded version remains v1.1.5.post1 (Apple Silicon) and v1.1.2 (general). A version bump PR (#4012) was closed today, indicating an imminent v1.1.6b1 release, but no artifacts are published yet.

## Project Progress
Four PRs were merged/closed today:

- **#1642** (closed) – `feat(error code): add error code`. Adds standardized error codes across the codebase, improving debuggability.
- **#1055** (closed) – `feat: add MiniMax as a built-in provider`. New OpenAI-compatible provider for MiniMax models (M2.5 series), including unit tests.
- **#559** (closed) – `fix: remove failed user messages from memory to prevent session poisoning`. Prevents `save_session_state()` from persisting user messages that triggered exceptions (e.g., malformed image URIs).
- **#4012** (closed) – `chore(version): bumping version to 1.1.6b1`. Chore PR, likely preparing the next beta release.

All others remain open, with several under review (#3994, #4009, #4005, #4007, #3831, #3525).

## Community Hot Topics
| Issue/PR | Comments | Topic |
|----------|----------|-------|
| [#3640 – MCP client TaskGroup hang](https://github.com/agentscope-ai/QwenPaw/issues/3640) | 6 | Agent freezes without error, critical stability issue |
| [#1327 – Model fallback chain](https://github.com/agentscope-ai/QwenPaw/issues/1327) | 5 | Automatic fallback for rate limit handling |
| [#4010 – Interrupt/stop on Feishu/WeChat](https://github.com/agentscope-ai/QwenPaw/issues/4010) | 2 | Closed, user request granted – ability to abort agent execution from chat channels |
| [#4006 – Reasoning content not filtered](https://github.com/agentscope-ai/QwenPaw/issues/4006) | 2 | Bug: MiniMax provider leaks reasoning tokens into output |

The **MCP client deadlock (#3640)** remains the most commented and highest-impact open issue. Users report that agents become unresponsive (no response, no error) when MCP tasks time out inside a `TaskGroup`. The workaround is a full restart, but no fix PR has emerged yet. The **model fallback chain (#1327)** continues to attract support for a multi-tier fallback strategy (e.g., GPT-4 → GPT-3.5 → local model).

## Bugs & Stability
**Critical severity:**
- **[#3640 – MCP client TaskGroup hang](https://github.com/agentscope-ai/QwenPaw/issues/3640)** – Agent becomes unresponsive when MCP tasks encounter errors. No existing fix; the issue is under investigation.

**Medium severity:**
- **[#4006 – Reasoning content not filtered in OpenAI-compatible provider](https://github.com/agentscope-ai/QwenPaw/issues/4006)** – MiniMax API returns reasoning tokens that CoPaw does not strip, causing output pollution. Confirmed by maintainers.
- **[#3991 – Ollama channel loses conversation history](https://github.com/agentscope-ai/QwenPaw/issues/3991)** – Context memory is not carried across turns for local models via Ollama, while online APIs work fine. Affects QwenPaw v1.5.1.
- **[#4004 – Auto-derive max_input_length from model context window](https://github.com/agentscope-ai/QwenPaw/issues/4004)** – Static `max_input_length` causes incorrect compression behavior when switching models. User Mzaxd contributes a detailed analysis and proposes auto-derivation.

**Low severity:**
- [#4005 – WSL2 NAT network timeout](https://github.com/agentscope-ai/QwenPaw/issues/3041) – Docs issue; fix PR under review.

**Fix PRs in progress:**
- [#4007](https://github.com/agentscope-ai/QwenPaw/pull/4007) addresses #3182 (vector index not built) and #3828 (embedding config not synced), plus adds a MemoryHook for long-term memory.
- [#4005](https://github.com/agentscope-ai/QwenPaw/pull/4005) fixes documentation for WSL2 NAT timeout (#3041).

## Feature Requests & Roadmap Signals
Highly requested features with clear community demand:

1. **Model fallback/retry chain** – Multiple requests (#1327, #4011, #3789) ask for an optional backup model when the primary fails. This is the most-requested enhancement across recent weeks.
2. **Interrupt/stop capability in chat channels** – Closed issue #4010 was implemented; users can now abort agent runs from Feishu/WeChat. This signals a growing focus on user control.
3. **Conversation message management** – #4001 (delete single messages) and #4002 (shared visual workspace with annotation) reflect a desire for richer chat UX.
4. **Agent evaluation / full history export** – #4008 asks for a built-in evaluation dashboard to benchmark agents, needed for production adoption.
5. **Voice input in web console** – #4000 mentions missing microphone feature in the web UI, a gap for accessibility.
6. **Ollama context handling** – Several issues (#3991, #4003) point to problems with local model memory and ARM64 compatibility (Apple Silicon subprocess architecture).

**Prediction for next release (v1.1.6b1):** Likely includes the MiniMax provider (#1055), error code system (#1642), memory poisoning fix (#559), and possibly the Volcengine provider (#3994, under review). Model fallback may not land yet but is a strong candidate for v1.2.0.

## User Feedback Summary
Users broadly appreciate CoPaw’s capability but show **clear frustration with reliability**:

- **“Agent freezes without error”** (#3640) – a showstopper for production deployments.
- **“Ollama memory lost”** (#3991) – local model users feel second-class compared to cloud API users.
- **“No evaluation tools”** (#4008) – enterprises require benchmarking before committing.
- **“WeChat and web not synced”** (#4000) – cross-channel consistency is expected but missing.
- **“Cannot delete single messages”** (#4001) – power users want granular control over conversation history.

Positive signals: The community is actively contributing (7 first-time contributor PRs today, including pt-BR l10n, skill testing CLI, and memory enhancements). Users are also providing detailed reproduction steps and self-diagnosis (e.g., #3640's AI-generated root cause analysis).

## Backlog Watch
Issues and PRs that have been open for an extended period without maintainer response or visible progress:

- **[#1327 – Model fallback chain](https://github.com/agentscope-ai/QwenPaw/issues/1327)** – Created 2026-03-12, last updated today by users, but no maintainer comment since initial creation. High demand.
- **[#3640 – MCP client hang](https://github.com/agentscope-ai/QwenPaw/issues/3640)** – Created 2026-04-21, 6 comments, still open with no linked PR or assignee. Critical for stability.
- **[#3789 – Model fallback (duplicate of #1327)](https://github.com/agentscope-ai/QwenPaw/issues/3789)** – Created 2026-04-24, only 1 comment, no maintainer reply.
- **[#3525 – Discord thread for cron jobs](https://github.com/agentscope-ai/QwenPaw/pull/3525)** – Open PR since 2026-04-17, under review but no progress in two weeks.
- **[#3831 – Vector model connection test](https://github.com/agentscope-ai/QwenPaw/pull/3831)** – Open PR since 2026-04-25, under review, no recent activity.

These items would benefit from a maintainer check-in to avoid community frustration.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-03

## 1. Today’s Overview

ZeroClaw is experiencing a highly active development phase. In the last 24 hours, 50 issues and 33 pull requests were updated, reflecting sustained community engagement and rapid triage. Two PRs were merged/closed, and six issues were closed. While no new releases were published today, the project shows strong momentum around the upcoming v0.7.5 and v0.8.0 milestones, with significant work underway on the v3 configuration schema, skill consolidation, and critical bug fixes for reasoning model support.

## 2. Releases

- There are **no new releases** in the last 24 hours. The latest tracked milestone is **v0.7.5** (tracking issue [#5878](https://github.com/zeroclaw-labs/zeroclaw/issues/5878)), which focuses on release pipeline automation. The v0.8.0 integration branch is being prepared via PR [#6266](https://github.com/zeroclaw-labs/zeroclaw/pull/6266).

## 3. Project Progress

**Merged/Closed PRs today (2):**

- **[PR #6087](https://github.com/zeroclaw-labs/zeroclaw/pull/6087)** (closed): Added environment variable overrides for Slack, Discord, and Telegram channel tokens, with `ZEROCLAW_`-prefixed variants taking precedence. Fixes long-standing configuration burden.
- **[PR #5206](https://github.com/zeroclaw-labs/zeroclaw/pull/5206)** (closed): Restored CI by removing stale firmware dependency, upgrading `rumqttc`, and suppressing a false-positive security advisory. Unblocks all PR builds.

**Also closed (1 issue):**
- **[Issue #6259](https://github.com/zeroclaw-labs/zeroclaw/issues/6259)** (bug): Gemini 3 thinking model broken by `tool_call extra_content` drop; fixed via PR #6284 (still open).

## 4. Community Hot Topics

The most active discussions attract between 4 and 9 comments. Key themes:

- **Cron tool unawareness** — [Issue #5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862) (“zeroclaw does not know it can add cron”): 9 comments, 0 reactions. Users expect the agent to autonomously use the `zeroclaw cron` command when asked to schedule recurring tasks. The underlying need is for agent meta-knowledge of its own CLI tools.
- **Dream Mode** — [Issue #5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) (feature request, 9 comments): Periodic memory consolidation and reflective learning. Demonstrates strong interest in long-term adaptive behavior, though no implementation is yet scheduled.
- **Reasoning content loss** — [Issue #6233](https://github.com/zeroclaw-labs/zeroclaw/issues/6233) (bug, 6 comments): DeepSeek V4 multi-turn conversations fail because `reasoning_content` is dropped from plain-text assistant messages. Fix PR [#6284](https://github.com/zeroclaw-labs/zeroclaw/pull/6284) is already open.
- **Shell sandbox blocking Python** — [Issue #5722](https://github.com/zeroclaw-labs/zeroclaw/issues/5722) (bug, 6 comments): Default sandbox prevents realistic Python skills, affecting the InvestorClaw project. Suggests need for configurable sandbox profiles.
- **Reply intent gating** — [Issue #5674](https://github.com/zeroclaw-labs/zeroclaw/issues/5674) (feature, 4 comments, 3 👍): Users want the “should I reply” classifier to be configurable, especially in 1:1 chats. High community alignment indicates this will likely land in v0.7.6.

## 5. Bugs & Stability

**High-severity bugs reported or updated today:**

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| [#6298](https://github.com/zeroclaw-labs/zeroclaw/issues/6298) | S2 (degraded) | Empty `tool_calls` array sent to strict validators (DeepSeek, NVIDIA NIM) -> 400 error | No |
| [#6295](https://github.com/zeroclaw-labs/zeroclaw/issues/6295) | S1 (workflow blocked) | Windows full build fails in `zeroclaw-hardware` crate (#6280) – S3, but blocks all Windows development | No |
| [#6269](https://github.com/zeroclaw-labs/zeroclaw/issues/6269) | S2 (degraded) | Context compressor drops `reasoning_content` – affects thinking models | [PR #6285](https://github.com/zeroclaw-labs/zeroclaw/pull/6285) |
| [#6243](https://github.com/zeroclaw-labs/zeroclaw/issues/6243) | S1 (blocked) | Streaming error (`HTTP error: error decoding response body`) from custom provider hangs ZeroClaw | No |
| [#6237](https://github.com/zeroclaw-labs/zeroclaw/issues/6237) | S1 (blocked) | Slack `bot_token` must be in config file, not env var – crashes if missing | [PR #6287](https://github.com/zeroclaw-labs/zeroclaw/pull/6287) |
| [#6229](https://github.com/zeroclaw-labs/zeroclaw/issues/6229) | S2 (degraded) | Telegram `mention_only=true` fails for photo/media messages | [PR #6286](https://github.com/zeroclaw-labs/zeroclaw/pull/6286) |
| [#6254](https://github.com/zeroclaw-labs/zeroclaw/issues/6254) | S2 (degraded) | WASM plugin install path vs runtime scan path mismatch – plugins invisible | No |
| [#6227](https://github.com/zeroclaw-labs/zeroclaw/issues/6227) | S2 (degraded) | `zeroclaw status` hardcodes service name, misreports named instances | [PR #6288](https://github.com/zeroclaw-labs/zeroclaw/pull/6288) |

**Overall stability assessment:** The project is actively addressing a cluster of reasoning-content and provider-compatibility regressions. Multiple open fix PRs indicate rapid resolution. However, new streaming-decode and empty tool_calls errors suggest ongoing edge cases with strict provider APIs.

## 6. Feature Requests & Roadmap Signals

**Most notable requests (ranked by community engagement):**
1. [Dream Mode](https://github.com/zeroclaw-labs/zeroclaw/issues/5849) – memory consolidation & reflective learning (9 comments)
2. [Configurable reply intent](https://github.com/zeroclaw-labs/zeroclaw/issues/5674) (4 comments, 3 👍)
3. [Air-gapped execution mode](https://github.com/zeroclaw-labs/zeroclaw/issues/6293) (1 comment; new today) – unix socket isolation for offline agent + online companion daemon
4. [Hybrid skills + WASM tools](https://github.com/zeroclaw-labs/zeroclaw/issues/6140) (1 comment) – next evolution after markdown-only skills
5. [LM Studio configurable URL](https://github.com/zeroclaw-labs/zeroclaw/issues/6260) (2 comments)
6. [Cost per provider](https://github.com/zeroclaw-labs/zeroclaw/issues/6251) (1 comment) – model cost tied to provider definition

**Roadmap signals:**
- The **v0.7.5 release** ([#5878](https://github.com/zeroclaw-labs/zeroclaw/issues/5878)) is in milestone tracking – focus on release automation.
- **v0.7.6** ([#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)) is themed around “skills support and UX” – CLI improvements, skill authoring, sandbox, test harness.
- The **v0.8.0 integration branch** is being built via PR [#6266](https://github.com/zeroclaw-labs/zeroclaw/pull/6266), introducing v3 schema migration, channel aliasing, model-provider aliasing, and profile lifting. This is a massive breaking-change batch that must land together.
- **v3 config shapes** are landing in parallel – nested provider configs ([#6270](https://github.com/zeroclaw-labs/zeroclaw/issues/6270)), SwarmConfig redesign ([#6271](https://github.com/zeroclaw-labs/zeroclaw/issues/6271)), agent filesystem layout ([#6272](https://github.com/zeroclaw-labs/zeroclaw/issues/6272)), and per-provider typed structs ([#6273](https://github.com/zeroclaw-labs/zeroclaw/issues/6273)).

**Prediction for next version (v0.7.6):** Skills consolidation ([PR #6274](https://github.com/zeroclaw-labs/zeroclaw/pull/6274)), first-party skills moved in-repo, compact mode. Configurable reply intent likely. Possibly the Tavily search provider implementation and LM Studio URL configuration.

## 7. User Feedback Summary

**Pain points voiced:**
- **Cron tool discoverability** – users expect the agent to understand its own capabilities (e.g., `zeroclaw cron`) without manual coaching.
- **Sandbox rigidity** – default shell sandbox prevents realistic Python workflows from skills like InvestorClaw.
- **Token management friction** – Slack and Telegram bot tokens forced into config file despite documentation suggesting env vars; multiple duplicates of the same issue.
- **Memory and reasoning content** – users of DeepSeek and other thinking models experience broken multi-turn conversations after context compression.
- **Plugin path mismatch** – WASM plugins installed to one directory but runtime scans another; immediate confusion.
- **Named-instance support** – `status` and `service status` misreport state for non-default daemons.
- **Windows build** – full build fails; community contributions blocked.

**Satisfaction signals:**
- Active community contribution: new PRs addressing multiple pain points (Slack env, Telegram mention_only, service naming, reasoning content) demonstrate responsive maintainers.
- Feature requests like Dream Mode and skill registries attract thoughtful discussion.

## 8. Backlog Watch

Long-standing issues requiring maintainer attention:

- **[Issue #5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862)** “zeroclaw does not know it can add cron” – opened Apr 18, 9 comments, no fix PR. Direct user experience blocker for cron usage.
- **[Issue #5722](https://github.com/zeroclaw-labs/zeroclaw/issues/5722)** “Default shell sandbox blocks Python skills” – opened Apr 14, 6 comments, marked in-progress but no associated PR.
- **[Issue #5674](https://github.com/zeroclaw-labs/zeroclaw/issues/5674)** “Make classify_channel_reply_intent configurable” – opened Apr 12, 4 comments, 3 👍. High community interest, no assigned PR.
- **[Issue #5628](https://github.com/zeroclaw-labs/zeroclaw/issues/5628)** “Daemon auto-start port conflict” – opened Apr 11, 3 comments, in-progress but no PR.
- **[Issue #5617](https://github.com/zeroclaw-labs/zeroclaw/issues/5617)** “Reduce core tools to 10-12” – opened Apr 11, 2 comments, in-progress. Part of microkernel architecture but stalled.
- **[PR #6143](https://github.com/zeroclaw-labs/zeroclaw/pull/6143)** “Universal skill registry support” – opened Apr 26, untouched for 7 days, no reviewer feedback. Large change (L-sized).
- **[PR #6101](https://github.com/zeroclaw-labs/zeroclaw/pull/6101)** “WebUI hot-switch model” – opened Apr 25, marked `needs-author-action`. Awaiting author revision.

**Notable:** The v0.8.0 integration branch PR [#6266](https://github.com/zeroclaw-labs/zeroclaw/pull/6266) is explicitly marked “DO NOT MERGE YET” and requires coordinated merging. Maintainers should monitor that all dependent PRs land together to avoid master breakage.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*