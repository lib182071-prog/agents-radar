# OpenClaw Ecosystem Digest 2026-05-12

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-12 09:49 UTC

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

# OpenClaw Project Digest — 2026-05-12

## 1. Today’s Overview

OpenClaw remains in an extremely high-activity phase with 500 issues and 500 PRs updated in the last 24 hours. Two new beta releases (v2026.5.10-beta.4 and v2026.5.10-beta.5) landed, carrying a CI improvement and a Fly runtime environment detection fix. The community is heavily engaged, but a significant portion of the day’s issue traffic is concentrated on QA harness corrections (see the dozen issues from @100yenadmin that were closed as harness/mock artifacts—not real user-facing regressions). However, several long-standing regression bugs (Coding Agent never completes, Windows chat UI broken, Mattermost slash commands returning 503) remain **open** and continue to draw high comment counts, signalling unresolved user pain.

## 2. Releases

**Two versions released today:**

- **[openclaw v2026.5.10-beta.5](https://github.com/openclaw/openclaw/releases/tag/v2026.5.10-beta.5)**  
- **[openclaw v2026.5.10-beta.4](https://github.com/openclaw/openclaw/releases/tag/v2026.5.10-beta.4)**  

Both share the same change entries (likely a data artifact; beta.4 may be a partial retag):

| Change | Details |
|--------|---------|
| CI | Adds a non‑blocking `plugin-inspector-advisory` artifact to Plugin Prerelease pipelines. Release runs now capture bundled plugin compatibility triage without altering the blocking gate. |
| Runtime/Fly | Detects Fly Machines as container environments from their runtime env vars, so the gateway binds correctly. |

**Breaking changes:** None noted.  
**Migration notes:** No special steps required. The Fly change is automatic for deployments on that platform.

## 3. Project Progress

In the last 24 hours, **41 PRs were merged or closed** (out of 500 updated). Notable closed PRs include:

- **[#80904](https://github.com/openclaw/openclaw/pull/80904) – memory‑wiki: require write scope for Obsidian search** (closed today) – Tightens gateway method scopes for security.
- **[#80890](https://github.com/openclaw/openclaw/pull/80890) – fix(matrix): default markdown tables to bullets** (closed today) – Improves Matrix channel output readability.
- **[#79529](https://github.com/openclaw/openclaw/pull/79529) – Add paperclip property to AgentParamsSchema** (closed today) – Fixes schema validation for Paperclip adapter.
- **[#79482](https://github.com/openclaw/openclaw/pull/79482) – feat(nvidia): fetch featured model catalog** (merged) – Replaces static model list with live catalog from build.nvidia.com.
- **[#78806](https://github.com/openclaw/openclaw/pull/78806) – fix(doctor): emit only one Gateway runtime panel per condition** (merged) – Resolves duplicate panel output in `doctor` command.
- **[#50221](https://github.com/openclaw/openclaw/pull/50221) – fix(admscp): cleanup adm scope handling** (merged) – Improves internal scope consistency.

Additionally, many **open PRs** with promising labels (e.g., CORS support, security redaction, i18n, subagent delivery hardening) remain active and may land in the next release.

## 4. Community Hot Topics

The most discussed issues (by comment count) reflect acute pain around regressions and unexpected behavior:

| Issue | Comments | Topic | Link |
|-------|----------|-------|------|
| #62505 | 13 | **Regression:** Coding Agent never completes (worked in 2026.4.2) | [Issue](https://github.com/openclaw/openclaw/issues/62505) |
| #58450 | 13 | Agent promises follow‑up but never starts any action | [Issue](https://github.com/openclaw/openclaw/issues/58450) |
| #67035 | 13 | Windows chat UI regression – input swallowed, replies invisible | [Issue](https://github.com/openclaw/openclaw/issues/67035) |
| #80319 | 12 | QA tool‑defaults suite conflates Codex‑native tools with OpenClaw tools | [Issue](https://github.com/openclaw/openclaw/issues/80319) |
| #79531 | 11 (closed) | Telegram forum topics intermittently stop responding | [Issue](https://github.com/openclaw/openclaw/issues/79531) |
| #68113 | 10 | Mattermost slash commands return 503 “not yet initialized” | [Issue](https://github.com/openclaw/openclaw/issues/68113) |
| #67793 | 9 | queue.mode “collect” not batching messages | [Issue](https://github.com/openclaw/openclaw/issues/67793) |

**Underlying needs:** The top issues share a theme – **reliability regressions** in core agent execution, UI rendering, and channel integration. Users are frustrated that previously working workflows (Coding Agent, Windows WebChat, Mattermost commands) broke in recent releases. The QA harness issues (#80319 and friends) generated intense discussion but were ultimately closed as test‑infrastructure bugs, not product faults.

No PRs had comment counts listed (likely zero or unrecorded). The most active PR by label is **[#79645](https://github.com/openclaw/openclaw/pull/79645)** – a security‑fix PR for inline redaction in `appendSessionTranscriptMessage`, flagged for human review.

## 5. Bugs & Stability

**High severity (open, regressions, high impact):**

| Issue | Description | Severity | Status |
|-------|-------------|----------|--------|
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent never completes – **regression from 2026.4.2** | 🔴 Critical | Open, 13 comments, no fix PR linked |
| [#67035](https://github.com/openclaw/openclaw/issues/67035) | Windows chat UI: input swallowed, streamed replies invisible, typing indicator blanks | 🔴 Critical | Open, 13 comments |
| [#68113](https://github.com/openclaw/openclaw/issues/68113) | Mattermost slash commands return 503 “not yet initialized” – regression in v2026.4.15 | 🟠 High | Open, 10 comments |
| [#58450](https://github.com/openclaw/openclaw/issues/58450) | Agent promises follow‑up but never starts any action | 🟠 High | Open, 13 comments |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | Subagent completion delivery lost on timeout/drain/orphan prune | 🟠 High | Open |
| [#67419](https://github.com/openclaw/openclaw/issues/67419) | Session context bloat – bootstrap re‑injected every turn, wasting 20‑30% tokens | 🟡 Medium | Open |
| [#67793](https://github.com/openclaw/openclaw/issues/67793) | queue.mode “collect” not batching messages despite debounce | 🟡 Medium | Open |
| [#65374](https://github.com/openclaw/openclaw/issues/65374) | Dreaming system contaminates agent identity in multi‑agent setups | 🟡 Medium | Open |
| [#67366](https://github.com/openclaw/openclaw/issues/67366) | `openclaw onboard` crashes with TypeError when replacing Telegram token | 🟡 Medium | Open |
| [#65624](https://github.com/openclaw/openclaw/issues/65624) | Mattermost slash commands use cleartext callback URLs exposing reusable tokens (CVSS 8.6) | 🟠 High (Security) | Open |

**Low severity but noteworthy:**  
- [#66614](https://github.com/openclaw/openclaw/issues/66614) – Block streaming splits markdown tables across messages (annoyance).  
- [#67088](https://github.com/openclaw/openclaw/issues/67088) – Dashboard falsely reports “No GUI detected” on macOS with SSH env vars.

**Fix PRs exist for some issues:**  
- [#80904](https://github.com/openclaw/openclaw/pull/80904) closes #80904 (memory‑wiki scope) – minor.  
- No fix PRs are directly linked to the top regressions (#62505, #67035, #68113) in today’s data.

## 6. Feature Requests & Roadmap Signals

Several enhancement issues attracted high community engagement (👍 counts) and are likely candidates for upcoming releases:

| Issue | Request | 👍 | Predict Next Release |
|-------|---------|----|---------------------|
| [#66944](https://github.com/openclaw/openclaw/issues/66944) | Plugin UI Extension System – plugins add native tabs to Control UI | 3 | Possibly mid‑term; UI plugin architecture is a large change |
| [#66252](https://github.com/openclaw/openclaw/issues/66252) | Per‑Agent TTS/STT configuration overrides for multi‑language | 1 | Likely soon – relatively contained config change |
| [#64463](https://github.com/openclaw/openclaw/issues/64463) | `session.maxDurationMinutes` and `maxTokensPerSession` | 0 | High demand for cost control; could appear in next minor |
| [#67000](https://github.com/openclaw/openclaw/issues/67000) | Warm‑up / session reuse for embedded agents (active‑memory) | 1 | Performance improvement – plausible for next beta |
| [#8295](https://github.com/openclaw/openclaw/issues/8295) | Allow `allowBots` support for Telegram groups | 4 | Parity with Discord/Slack – simple config addition |
| [#44431](https://github.com/openclaw/openclaw/issues/44431) | 7 browser tool improvements (CSS selector support, etc.) | 0 | Lower priority – field report, but no PR yet |

**In‑progress feature PRs:**  
- **[#68647](https://github.com/openclaw/openclaw/pull/68647)** – CORS support for Gateway HTTP endpoint (size XL, open).  
- **[#80774](https://github.com/openclaw/openclaw/pull/80774)** – Manifest plugin auth requirements (adds `authRequirements` metadata).  
- **[#80661](https://github.com/openclaw/openclaw/pull/80661)** – Make run loop retry limits configurable in `openclaw.json`.  
- **[#79482](https://github.com/openclaw/openclaw/pull/79482)** – NVIDIA live model catalog (already merged).  

**Prediction:** The next beta (v2026.5.x) will likely include configurable retries (#80661), CORS (#68647 if merged), and perhaps per‑model allowlist improvements. Session duration caps (#64463) may appear as a config parameter.

## 7. User Feedback Summary

**Real pain points expressed (direct quotes):**

- *“Coding Agent never completes anything”* – [#62505](https://github.com/openclaw/openclaw/issues/62505) – severe regression affecting daily work.
- *“Input text swallowed, streamed replies invisible until refresh”* – [#67035](https://github.com/openclaw/openclaw/issues/67035) – Windows chat UI regression makes the dashboard unusable.
- *“All commands return 503 ‘not yet initialized’”* – [#68113](https://github.com/openclaw/openclaw/issues/68113) – Mattermost integration broken.
- *“越更新越更的像屎一样”* (roughly: “The more updates, the more it becomes like shit”) – [#67626](https://github.com/openclaw/openclaw/issues/67626) – frustration with breaking config changes.
- *“Agents have no visibility into their context window usage, causing unexpected compaction”* – [#2597](https://github.com/openclaw/openclaw/issues/2597) – long‑standing request.
- *“The agent continues to work fine in DM but forum topics stop responding”* – [#79531](https://github.com/openclaw/openclaw/issues/79531) – Telegram channel‑specific reliability.

**Use cases that are not working:**  
- Coding agents that previously ran autonomously now stall.  
- Multi‑agent setups with dream memory contamination (#65374).  
- Geographically distributed users (Mattermost, Nextcloud Talk) losing replies after recent releases.  
- Users on macOS with WSL2 reporting Gemini model hangs (#78502, closed but indicative).

**Satisfaction indicators:** Few positive feedback items in today’s data; the high number of regression reports suggests user trust is shaken. The rapid release of beta.4 and beta.5 shows the team is responsive, but the QA harness corrections (dozens closed) indicate the test suite itself needed shoring up.

## 8. Backlog Watch

The following issues have been open for **extended periods** (weeks to months) with high engagement but no linked fix PRs or official maintainer response visible:

| Issue | Age (created) | Comments | Summary |
|-------|---------------|----------|---------|
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | 2026-04-07 (35 days) | 13 | Coding Agent never completes – regression |
| [#58450](https://github.com/openclaw/openclaw/issues/58450) | 2026-03-31 (42 days) | 13 | Agent promises follow‑up but never starts action |
| [#67035](https://github.com/openclaw/openclaw/issues/67035) | 2026-04-15 (27 days) | 13 | Windows chat UI regression |
| [#68113](https://github.com/openclaw/openclaw/issues/68113) | 2026-04-17 (25 days) | 10 | Mattermost slash commands 503 |
| [#67777](https://github.com/openclaw/openclaw/issues/67777) | 2026-04-16 (26 days) | 7 | Subagent completion delivery lost |
| [#67419](https://github.com/openclaw/openclaw/issues/67419) | 2026-04-15 (27 days) | 7 | Session context bloat (20‑30% wasted tokens) |
| [#2597](https://github.com/openclaw/openclaw/issues/2597) | 2026-01-27 (105 days) | 8 | Context usage percentage in Runtime line – feature request |

**Old PRs needing maintainer attention** (open since 2026-04-18, no activity for ~24 days):

- [#68558](https://github.com/openclaw/openclaw/pull/68558) – fix(auto-reply): stop misleading compact labels  
- [#68537](https://github.com/openclaw/openclaw/pull/68537) – fix(telegram): allow ACP bindings for direct chats  
- [#68647](https://github.com/openclaw/openclaw/pull/68647) – feat: CORS for Gateway HTTP (size XL)  
- [#68433](https://github.com/openclaw/openclaw/pull/68433) – Prewarm mirrored outbound sessions  
- [#68462](https://github.com/openclaw/openclaw/pull/68462) – fix(config): refuse to restore from polluted backup  
- [#68464](https://github.com/openclaw/openclaw/pull/68464) – Harden subagent completion delivery (size L)

These PRs have been reviewed or labelled but not merged; they may need rebasing or re‑review. The CORS PR (#68647) is a widely requested feature and its prolonged open state may be blocking downstream use cases.

---

*Generated from GitHub data for 2026-05-12. All links are to the openclaw/openclaw repository.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem
**Date: 2026-05-12**

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing a period of **intense maturation**, characterized by rapid feature iteration alongside significant reliability challenges. Multiple projects are converging on similar architectural patterns—agent loop orchestration, memory management, multi-channel delivery, and tool plugin systems—while differentiating on deployment model (container-native vs. lightweight), target user (individual developers vs. enterprise teams), and UI paradigm (CLI/TUI vs. rich web dashboard). A clear "platform vs. specialized agent" dichotomy is emerging, where projects like OpenClaw and IronClaw serve as core infrastructure, while NanoBot, PicoClaw, and others focus on specific use cases. The ecosystem is healthy but fragmented, with no single project achieving dominance across all dimensions, and **reliability regressions** remain the single largest source of user dissatisfaction across nearly every project.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | Open Issues | PRs Updated (24h) | PRs Merged/Closed | New Release? | Health Score¹ |
|---------|---------------------|-------------|-------------------|-------------------|-------------|---------------|
| **OpenClaw** | 500 | ~500 (high churn) | 500 | 41 | ✅ (2 betas) | ⚠️ Strained |
| **NanoBot** | 8 | 5 | 18 | 7 | ❌ | ✅ Healthy |
| **Hermes Agent** | 50 | 44 | 50 | 2 | ❌ | 🔴 Critical |
| **PicoClaw** | 11 | 4 | 17 | 6 | ✅ (nightly) | ⚠️ Mixed |
| **NanoClaw** | 5 | 5 | 18 | 9 | ❌ | ✅ Productive |
| **NullClaw** | 1 | 0 | 0 | 0 | ❌ | ✅ Stable |
| **IronClaw** | 43 | 20 | 50 | 14 | ✅ (v0.28.1) | ✅ Healthy |
| **LobsterAI** | 0² | 0 | 18 | 18 | ❌ | ✅ High velocity |
| **TinyClaw** | 0 | 0 | 0 | 0 | ❌ | 💤 Dormant |
| **Moltis** | 4 | 1 | 2 | 2 | ❌ | ✅ Stable |
| **CoPaw** | 46 | 22 | 38 | 27 | ❌ | ✅ High activity |
| **ZeptoClaw** | 1 | 0 | 0 | 0 | ❌ | 💤 Maintenance |
| **ZeroClaw** | 19 | 7 | 47 | 23 | ❌ | ✅ High velocity |

¹ *Health Score: ✅ Healthy = active, responsive, low regression rate; ⚠️ Mixed = high activity but significant regressions; 🔴 Critical = multiple P1 bugs with no fix; 💤 Dormant/Maintenance = minimal or zero activity.*
² *LobsterAI had 0 new issues but 18 PRs—indicating a development push without new bug reports.*

**Key observations:**
- **OpenClaw** dominates in raw volume but suffers from a high noise floor (dozens of QA harness artifacts cluttering issue tracker)
- **Hermes Agent** shows critical strain: multiple P1 bugs (Telegram down, compression hang, macOS gateway failure) with no fix PRs
- **ZeroClaw** and **CoPaw** show strong bug-fix velocity, closing 60%+ of updated items within 24 hours
- **NullClaw** and **Moltis** demonstrate best-in-class responsiveness—single bugs closed same day
- **TinyClaw** and **ZeptoClaw** appear in maintenance/sleep mode with zero development activity

---

## 3. OpenClaw's Position

### Advantages vs. Peers

| Dimension | OpenClaw | Best Peer | Gap Analysis |
|-----------|----------|-----------|--------------|
| **Release cadence** | 2 beta releases in 24h | Next: IronClaw (v0.28.1) | Unmatched velocity, but beta quality is erratic |
| **Feature surface** | 500+ open PRs covering every domain | CoPaw: 38 PRs | Vastly larger scope, but harder to stabilize |
| **Community size** | 500 issues/PRs/day | Hermes: 100/day | ~5x larger than next biggest; clear reference project status |
| **Integration support** | 12+ channel adapters | ZeroClaw: comparable | Broadest channel coverage, but many (Telegram, Mattermost) have regressions |
| **QA infrastructure** | Dedicated harness (flawed) | NanoBot: no harness | Has testing infrastructure, but harness bugs generate noise |

### Technical Approach Differences

- **Plugin architecture**: OpenClaw uses a formal plugin-inspector pipeline for compatibility triage—unique among peers
- **Runtime detection**: Fly.io container detection (added today) shows cloud-native focus vs. self-hosted peers
- **Agent loop**: Centralized `CodexAgent` with rich scheduling, but the "never completes" regression (#62505) suggests recent refactors broke core loop logic—a failure mode not present in simpler projects like NanoBot or NullClaw

### Vulnerability: Reliability Trust

OpenClaw is **the most feature-rich but also the most regression-prone** project. The top 10 bugs by comment count (Coding Agent never completes, Windows chat UI broken, Mattermost 503) all share an origin: **regressions from recent releases**. Users explicitly express frustration ("the more updates, the more it becomes like shit"). This contrasts with NullClaw where a single bug was fixed in < 24h, or Moltis where 3/4 bugs were closed same day.

**Net assessment**: OpenClaw is the de facto ecosystem reference implementation by volume and breadth, but it is **losing user trust** due to reliability regressions. Competitors (particularly ZeroClaw, NanoBot, and IronClaw) may capture dissatisfied users seeking stability.

---

## 4. Shared Technical Focus Areas

The following requirements emerged **across multiple projects** (≥3), indicating ecosystem-wide priorities:

| Requirement | Projects Expressing Need | Count | Specifics |
|------------|-------------------------|-------|-----------|
| **Memory / context management** | OpenClaw (#67419), NanoBot (#3744), Hermes (#509), PicoClaw (auto-memory), CoPaw (#4220), NanoClaw (#2419) | 6 | Session context bloat (20-30% wasted tokens), memory isolation per-user/per-group, cross-session recall, vector index sync |
| **Channel reliability & message delivery** | OpenClaw (#67035, #68113), Hermes (#24140), PicoClaw (#2720), NanoClaw (#2423), IronClaw (#2903), CoPaw (#4170) | 6 | Silent message drops, Telegram/Matrix/WeChat failures, 503 errors, rate-limit swallowing, timeout handling |
| **Fallback / failover models** | NanoBot (#3742), Hermes (#24279), NanoClaw (#2417), NullClaw (#902), ZeroClaw (#6589) | 5 | Runtime model switching, configurable retry limits, vision fallback bypass, provider-specific reasoning field incompatibilities |
| **Security & credential handling** | OpenClaw (#65624, #79645), IronClaw (#3490), Hermes (#7674), NanoClaw (container mount persistence), CoPaw (#4244) | 5 | Cleartext tokens in URLs, admin settings not propagating, shell evasion bypass, stale PIDs, model-name mutation causing auth errors |
| **Multi-agent / squad orchestration** | OpenClaw (#67777), NanoBot (#3621), Hermes (#24284), PicoClaw (#2830), CoPaw (#4211) | 5 | Subagent delivery on timeout, multi-agent squad deployments, cron self-scheduling, async result routing, delegation protocols |
| **UI/UX discoverability** | IronClaw (#3500), Hermes (#24186/24188), CoPaw (#4213), PicoClaw (#2796) | 4 | Local web UI hidden, Kanban dashboard broken, large conversation freezing, history truncation |
| **Tool plugin extensibility** | OpenClaw (#80904), NanoBot (#3729), Hermes (#24283), PicoClaw (#2855) | 4 | Plugin security scopes, self-describing tool patterns, plugin UI extensions, media attachments in tool outputs |
| **Session context compression** | OpenClaw (#67419), Hermes (#19539, #24098), NanoClaw (compaction) | 3 | Token-wasting context bloat, compression waiting causing hangs, predictable threshold-based compression |

**Most urgent cross-project gap:** **Memory and context management** is the #1 shared pain point, with six projects actively working on solutions ranging from vector-index integration (CoPaw, NanoClaw) to per-session memory files (NanoBot) to cognitive memory operations (Hermes). The lack of a standard solution is fragmenting the ecosystem.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | NanoBot | Hermes | CoPaw | ZeroClaw |
|-----------|----------|----------|---------|--------|-------|----------|
| **Primary user** | Power users / self-hosters | Enterprise teams | Individual devs | AI researchers | Chinese developers | Linux sysadmins |
| **Deployment model** | Cloud-native (Fly.io) + self-host | Docker + self-host | CLI/TUI + LAN web | Docker + macOS | Desktop + server | NixOS + systemd |
| **UI paradigm** | Web dashboard heavy | Web + CLI | CLI/TUI first | Web dashboard | Desktop client | No GUI |
| **Agent loop complexity** | High (scheduling, loops) | Extreme (Reborn architecture) | Low (simple loop) | Medium (Kanban workers) | High (ACP delegation) | Medium (RouterProvider) |
| **Memory approach** | Session context + wiki | Reborn memory substrate | USER.md / MEMORY.md | Cognitive memory ops | Auto-memory + vector DB | Schema v3 migration |
| **Channel differentiation** | 12+ adapters | Slack, WeChat, Gmail | Feishu, WeCom, WebSocket | Telegram, Feishu, Kanban | Feishu, Telegram | Discord, Matrix |
| **Security posture** | Plugin scopes (basic) | Trust-boundary hardening (active) | Minimal (local-first) | Emerging (vision auth) | Shell evasion checks | Cleartext tokens (weak) |
| **Community contributions** | High (external PRs) | Moderate | High (external PRs) | Moderate | Very high (Chinese devs) | Moderate |
| **Risk profile** | Regression-prone | Architecture churn | Stable but narrow | Critical outages | Feature-rich but fragmented | Rapid bug fixes |

**Key differentiators:**
- **IronClaw** is the most architecturally ambitious, with a complete "Reborn" rewrite of the agent loop—highest risk/reward
- **NanoBot** is the most accessible for individual developers, with a lightweight CLI/TUI and rapid feature turnaround
- **CoPaw** dominates the Chinese-language ecosystem with ACP (Alibaba Agent Communication Protocol) and Feishu integration
- **ZeroClaw** focuses on operational reliability for Linux/NixOS deployments, with the best bug-fix closure rate among active projects
- **Hermes** targets researchers but is currently hampered by critical outages—highest immediate user impact

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (40+ PRs/day, high churn)
- **OpenClaw** – Unmatched velocity but noise and regressions erode trust
- **IronClaw** – Reborn rewrite consuming most capacity; shipping features but creating architectural debt
- **CoPaw** – Extremely responsive (27 PRs merged in 24h); Chinese ecosystem leader
- **ZeroClaw** – Rapid bug fixes (23 PRs merged); preparing v0.8.0 major release

### Tier 2: Productive Development (10-20 PRs/day)
- **NanoBot** – Healthy cadence with quality features (multi-tenant WebUI, tool plugin refactor); good community responsiveness
- **NanoClaw** – Moderate but focused activity; container runtime and memory integration work
- **LobsterAI** – Burst activity (18 PRs merged); voice input, UI overhaul, telemetry removal—polishing for next release

### Tier 3: Stable / Maintenance (<10 items/day)
- **NullClaw** – Minimal activity but fast incident response; project appears stable
- **Moltis** – Small-scale but effective; Proxmox installer fixes suggest focused user base
- **PicoClaw** – Mixed signals: nightly builds and community PRs, but high-severity PID bug (#2720) unresolved for 12 days

### Tier 4: Dormant / Sleep
- **TinyClaw** – No activity in 24h; may be abandonware
- **ZeptoClaw** – Single security audit issue closed; otherwise zero activity

**Maturity assessment:** The ecosystem is **bifurcating** between projects that are shipping quickly but accumulating technical debt (Tier 1) and those that are stable but slowing down (Tier 3). Tier 2 projects (NanoBot, LobsterAI) represent the healthiest balance of velocity vs. quality. The dormant projects (TinyClaw, ZeptoClaw) likely indicate developer attrition—users depending on these should evaluate migration paths.

---

## 7. Trend Signals

### Signal 1: Reliability Regressions Are the #1 Ecosystem Risk
Across **7 of 13** active projects, users report regressions from recent releases as their primary pain point.  
- 0 users say "I want more features"  
- Dozens say "X that worked last month is now broken"  
*Implication:* The ecosystem is prioritizing speed over stability. For decision-makers, this means **pinning versions** and **extensive integration testing** before upgrades are mandatory. Projects with strong bug-fix records (NullClaw, Moltis, NanoBot) should be favored for production deployments.

### Signal 2: Memory & Context Management Is the Next Battleground
Six projects are independently building memory solutions (vector DB, MEMORY.md, cognitive ops, memory sidecars). This fragmentation creates **portability risk**—agents built for one project's memory model cannot migrate.  
*Implication:* An ecosystem-wide memory standard (or at least a compatible API) is needed to prevent lock-in. OpenClaw, as the reference project, should lead this effort.

### Signal 3: Multi-Modal (Voice, Vision, Media) Is Now Table Stakes
Projects shipping voice input (LobsterAI #1947), vision capability (ZeroClaw #6573, Hermes #21037), and media attachments (PicoClaw #2855, NanoClaw #2426) are gaining community traction. Chinese projects (CoPaw, PicoClaw) are particularly aggressive on Feishu/WeChat media support.  
*Implication:* Projects that cannot handle voice, images, and file attachments will be seen as legacy. This is especially true for enterprise-facing deployments.

### Signal 4: Infrastructure Reliability (Docker, Proxmox, NixOS, Systemd) Is Becoming Critical
Multiple projects saw Docker container mount bugs (NanoClaw #2424), Proxmox LXC failures (Moltis #991, #993), NixOS configuration mismatches (Hermes #21341), and macOS gateway failures (Hermes #23387). Users are deploying these agents on real infrastructure, not just desktops.  
*Implication:* The "works on my machine" era is over. Projects need robust CI/CD for diverse deployment targets, or they will lose enterprise adopters.

### Signal 5: Security Concerns Are Emerging but Underserved
Cleartext tokens (OpenClaw #65624, CVSS 8.6), admin tool isolation bypasses (IronClaw #3490), and shell command injection vectors (CoPaw #4244) point to **immature security posture** across the ecosystem. Only IronClaw has active trust-boundary hardening work (#3492/#3494).  
*Implication:* For enterprise or production use, additional security auditing and sandboxing are required before deployment. This is a significant barrier to institutional adoption.

### Signal 6: Chinese Ecosystem Is Parallel and Surging
CoPaw and PicoClaw (from Chinese developers) show activity levels comparable to global projects, with unique integrations (Feishu, WeChat, Alibaba Cloud APIs, DashScope models). Feature requests from Chinese users (model switching for mainland network instability, per-group memory) differ from Western priorities.  
*Implication:* The AI agent ecosystem is becoming **bilingual and biregional**. Western projects that ignore Asian-market needs (especially WeChat/WeCom integration and Chinese LLM provider support) will cede this fast-growing user base.

---

## Executive Summary

| Project | Recommendation for Developers | Recommendation for Enterprise | Risk Level |
|---------|------------------------------|------------------------------|------------|
| **OpenClaw** | Best for experimentation; pin to v2026.4.2 for stability | Wait for regression fixes; use with extensive testing | 🟡 High |
| **IronClaw** | Promising architecture; watch Reborn stabilization | Evaluate after v0.29 release; strong security work | 🟡 Medium |
| **NanoBot** | Best for individual devs; good community, stable | Too lightweight for enterprise | 🟢 Low |
| **Hermes Agent** | Avoid until critical P1 bugs are fixed | Not recommended—Telegram/macOS outages | 🔴 High |
| **CoPaw** | Best for Chinese-language deployments | Evaluate ACP/compliance for Alibaba infrastructure | 🟢 Low (within CN) |
| **ZeroClaw** | Best for Linux/NixOS production | Strong operational reliability; monitor v0.8.0 | 🟢 Low |
| **NullClaw** | Stable; minimal maintenance | Suitable for simple deployments | 🟢 Very Low |
| **Moltis** | Proxmox-focused users | Niche—containerized deployments only | 🟢 Low |
| **LobsterAI** | Desktop users wanting polished UI | Not server-grade | 🟢 Low |

**Bottom line:** The ecosystem is vibrant but fragmented. For production reliability, **NanoBot** (individual devs) and **ZeroClaw** (Linux-based deployments) are the safest choices. For maximum feature surface, **OpenClaw** remains the reference but requires significant operational vigilance. The next 90 days will determine whether the ecosystem converges on shared standards (memory, security, multi-modal) or continues to fragment.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-12

## 1. Today’s Overview

Activity remained high with **8 issues** and **18 PRs** updated in the last 24 hours. Three bugs were closed and five remain open, while the PR pipeline saw **7 merges/closures** against **11 still under review**. No new release was cut, indicating the team is consolidating a series of feature and refactoring PRs before tagging a version. Community engagement is lively, centering on session memory isolation, conversation interruption handling, and dynamic model switching.

## 2. Releases

No new releases occurred in this period.

## 3. Project Progress (Merged/Closed PRs Today)

Seven PRs were merged or closed, advancing both functionality and stability:

- **Feishu topic isolation switch** ([PR #3747](https://github.com/HKUDS/nanobot/pull/3747)) – adds a configurable `topic_isolation` boolean to Feishu channels, allowing users to disable per-topic session isolation (requested in issue #3692).
- **VolcEngine provider compatibility fix** ([PR #3738](https://github.com/HKUDS/nanobot/pull/3738)) – sets `supports_max_completion_tokens` to `False` for VolcEngine, preventing a 400 error when both `max_tokens` and `max_completion_tokens` are sent.
- **Tool plugin architecture** ([PR #3729](https://github.com/HKUDS/nanobot/pull/3729)) – refactors the tool system from a hardcoded registration method to a self-describing plugin pattern, reducing boilerplate and enabling easier third‑party tool authoring.
- **WeCom filename preservation** ([PR #3751](https://github.com/HKUDS/nanobot/pull/3751)) – fixes issue #3737 by forwarding `None` instead of `"unknown"` for missing file names, so the SDK‑returned real filename is used.
- **Multi‑tenant WebUI** ([PR #3749](https://github.com/HKUDS/nanobot/pull/3749)) – converts the WebUI from single‑user to multi‑user, with per‑user state isolation under `~/.nanobot/users/<ulid>/` and email/password authentication. Chat channels (Telegram, Slack, etc.) remain admin‑scoped in v1.
- **WebSocket media passthrough** ([PR #3673](https://github.com/HKUDS/nanobot/pull/3673)) – restores support for image attachments sent via the `media` field in WebSocket message envelopes.
- **WebUI `crypto.randomUUID` shim** ([PR #3733](https://github.com/HKUDS/nanobot/pull/3733)) – adds a fallback for `crypto.randomUUID` so that the WebUI works over plain‑HTTP LAN connections.

## 4. Community Hot Topics

The most discussed issues and PRs reveal three core user needs:

- **Session‑level memory for multi‑IM users** – Issue [#3744](https://github.com/HKUDS/nanobot/issues/3744) (3 comments) asks how `USER.md` and `MEMORY.md` behave when multiple IM users share a single agent. The user seeks explicit session‑scoped memory rather than global files. This is the most active open issue.
- **Interrupted conversation context loss** – Issue [#3689](https://github.com/HKUDS/nanobot/issues/3689) (2 comments) reports that interrupting an agent mid‑task causes it to lose the previous chat history, including what steps were already executed. The author suggests the agent should remember the conversation state even after interruption.
- **Feishu topic isolation toggle** – Issue [#3692](https://github.com/HKUDS/nanobot/issues/3692) (1 comment, 1 👍) was directly addressed by merged PR #3747, satisfying the user request for a configurable switch.

A secondary signal is the `/model` slash‑command request (issue [#3742](https://github.com/HKUDS/nanobot/issues/3742)), which emerged from network instability with GPT‑5.5 in mainland China – the user wants to switch provider/models at runtime without restarting.

## 5. Bugs & Stability

Four bugs were active today, with two being high‑severity:

| Bug | Severity | Fix PR / Status |
|-----|----------|-----------------|
| **Model ignores external file content** ([#3754](https://github.com/HKUDS/nanobot/issues/3754)) – DeepSeek V4 Flash skips `read_file` tool calls for small/common‑knowledge files (e.g., element period table) and invents content. | **High** – undermines tool‑augmented generation reliability. | No fix PR yet; issue links to #3753. |
| **DeepSeek reasoning_content error** ([#3753](https://github.com/HKUDS/nanobot/issues/3753)) – post3 automatically injects `reasoning_content` into API calls, causing a 400 error on models that don’t support thinking mode. | **Medium** – blocking for DeepSeek V4 Flash users, but a workaround (switch to non‑thinking model) exists. | Issue closed as completed (likely a quick patch or documentation fix). |
| **WebUI markdown chunk preload** ([#3746](https://github.com/HKUDS/nanobot/issues/3746)) – a >1 MB code‑highlighting chunk is eagerly loaded even in sessions without code blocks, wasting bandwidth. | **Low/Medium** – performance regression for production WebUI. | No fix PR yet. |
| **WeCom file‑name recognition** ([#3737](https://github.com/HKUDS/nanobot/issues/3737), closed) – missing filename defaulted to `"unknown"`. | **Medium** – caused `[file: unknown]` to be forwarded to LLM. | Fixed by PR #3751 (merged today). |

A related fix PR for **voice transcription file‑path leakage** ([#3752](https://github.com/HKUDS/nanobot/pull/3752)) remains open: `.ogg` paths from WhatsApp transcription are appended as `[file: ...]` tags, confusing the LLM.

## 6. Feature Requests & Roadmap Signals

The following user‑requested features are likely candidates for upcoming releases:

- **Per‑user/group session memory** – Issue #3744 (session‑level `MEMORY.md`) aligns with the broader cross‑session memory work in PR [#3408](https://github.com/HKUDS/nanobot/pull/3408) (MGP sidecar, still open) and with the ongoing discussion on conversation interruption handling.
- **Dynamic model/provider switching** – Issue [#3742](/model slash command) is echoed in open PRs for **model presets with runtime switching** (PR [#3714](https://github.com/HKUDS/nanobot/pull/3714)) and **model failover chains** (PR [#3756](https://github.com/HKUDS/nanobot/pull/3756)). These two PRs together would enable `/model` command without additional work.
- **Tool progress streaming** – PR [#3745](https://github.com/HKUDS/nanobot/pull/3745) adds SSE event `nanobot.tool.progress` to the chat completions API, enabling real‑time tool execution status in WebUI and custom clients. The underlying issue [#3698](https://github.com/HKUDS/nanobot/issues/3698) is referenced.
- **Agent self‑correction** – PR [#3728](https://github.com/HKUDS/nanobot/pull/3728) introduces `LoopDetectHook` and `ReflectRetryHook` to automatically break out of tool‑call loops and avoid blind retries. This directly addresses issue #3689 (interrupted conversations).
- **Reasoning content display** – PR [#3655](https://github.com/HKUDS/nanobot/pull/3655) adds a `show_reasoning` config option for the CLI/TUI, allowing users to see model thinking in real time.
- **Multi‑agent squad deployments** – PR [#3621](https://github.com/HKUDS/nanobot/pull/3621) proposes a production‑ready multi‑agent orchestration for Hugging Face Spaces, enabling multiple specialized agents to run in a single container.

Given the merge velocity, the next minor release is likely to include model presets/failover, the tool plugin refactor, multi‑tenant WebUI, and the Feishu topic isolation switch.

## 7. User Feedback Summary

**Pain points** (most frequently voiced):

- **Memory & context sharing** – Users of multi‑IM setups (e.g., several WeChat users pointed at the same agent) are confused by global `USER.md`/`MEMORY.md` files. They expect session‑scoped memory.
- **Conversation interruption fragility** – Interrupting a stuck agent loses the entire conversation thread, forcing users to re‑explain context. This is a major quality‑of‑life gap.
- **Model instability in restrictive regions** – Chinese users experience timeouts/errors with certain providers and request `/model` commands to hot‑swap.
- **File‑reading reliability** – The agent sometimes ignores explicit `read_file` instructions for well‑known knowledge (e.g., periodic table), undermining user trust in tool execution.

**Satisfaction signals**:

- The team’s rapid turnaround on the WeCom filename bug (#3737 → fixed same day) and the Feishu topic isolation feature (#3692 → PR merged in 3 days) demonstrates responsiveness.
- Community contributions are growing – Atomic Chat provider (PR [#3750](https://github.com/HKUDS/nanobot/pull/3750)), multi‑tenant WebUI (PR #3749), and refactoring tool plugin system (PR #3729) are all from external developers.

## 8. Backlog Watch

| Item | Type | Age & Status | Maintainer Attention Needed? |
|------|------|--------------|-------------------------------|
| [MGP memory sidecar](https://github.com/HKUDS/nanobot/pull/3408) | PR | Opened **Apr 23** (19 days ago), still open. Adds governed cross‑session memory. Last updated May 11. | Low – actively evolving; may be waiting on upstream MGP changes. |
| [Multi‑agent squad deployment](https://github.com/HKUDS/nanobot/pull/3621) | PR | Opened May 4 (8 days ago), still open. Complex deployment scheme. | Medium – no recent activity; may need rebase or review from core team. |
| [Reasoning display in CLI](https://github.com/HKUDS/nanobot/pull/3655) | PR | Opened May 6 (6 days ago), still open. Relatively small change. | Low – conflcit with other TUI changes; can be reviewed after #3728 lands. |
| [Loop detection & reflect retry](https://github.com/HKUDS/nanobot/pull/3728) | PR | Opened May 10 (2 days ago), still open. Focused on self‑correction. | Low – recent, likely under review. |
| [SSE tool progress events](https://github.com/HKUDS/nanobot/pull/3745) | PR | Opened May 11 (1 day ago). | Low – fresh, no review yet. |
| [Model presets + runtime switching](https://github.com/HKUDS/nanobot/pull/3714) | PR | Opened May 9 (3 days ago), still open. Foundational for /model command. | Medium – large change touching config schema; needs careful review. |

No old, completely ignored issues were identified among the tracked items. The oldest open PR (#3408) is active and supported by ongoing commits. The team appears to have good coverage of incoming work.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-12

## Today’s Overview

The project is experiencing an exceptional spike in activity, with **50 issues and 50 pull requests updated in the last 24 hours** — a volume suggesting either a major release cycle, widespread instability, or both. The open/active issue count stands at 44, while 6 issues and 2 PRs have been closed/merged. No new releases were published today. The community is reporting several **critical outages** (Telegram bot completely down, Kanban dashboard broken, context‑window enforcement blocking models) and a number of **persistent infrastructure bugs** (compression hanging, macOS gateway failure, Feishu formatting issues). Maintainer response appears fragmented, as several P1 bugs lack corresponding fix PRs. The overall project health is **strained but responsive**, with feature development continuing in parallel.

## Releases

No new releases today.

## Project Progress

Two pull requests were merged or closed in the last 24 hours (from the top‑20 list, only one such PR is visible; the second is not shown in the provided data).

**Closed #13140** — *feat: add Traditional Chinese (zh‑TW) support on dashboard*  
Adds a full `tw.ts` locale for the Web UI dashboard, covering terminology such as “儲存” for Save and “重新整理” for Refresh.  
🔗 [NousResearch/hermes-agent PR #13140](https://github.com/NousResearch/hermes-agent/pull/13140)

Three issues were also closed:
- **#24263** – [CLOSED] Duplicate feature request for per‑sub‑agent provider/model selection.  
- **#24007** – [CLOSED] Habit reminder workflow decay (closed as feature, not bug).  
- **#24101** – [CLOSED] Documentation fix for malformed Markdown table in Voice & TTS page.

These closures represent **incremental documentation and duplicate‑handling work** rather than substantial bug fixes or feature completions.

## Community Hot Topics

Issues and PRs attracting the most discussion and reactions reveal deep concerns around **stability, usability, and memory capabilities**.

### Most Commented Issues

1. **#24140** (7 comments, P1)  
   *“All models rejected with context window below minimum 64,000 tokens — Telegram completely down”*  
   A configuration/enforcement bug is blocking all model calls on Telegram, effectively taking the primary user interface offline.  
   🔗 [NousResearch/hermes-agent Issue #24140](https://github.com/NousResearch/hermes-agent/issues/24140)

2. **#509** (6 comments, 2 👍)  
   *“Feature: Cognitive Memory Operations — LLM‑Driven Encoding, Consolidation, Adaptive Recall & Extraction”*  
   A highly anticipated feature request proposing autonomous memory management inspired by CrewAI. The 2 thumbs‑up indicate strong community support.  
   🔗 [NousResearch/hermes-agent Issue #509](https://github.com/NousResearch/hermes-agent/issues/509)

3. **#21341** (4 comments, P2)  
   *“[Bug]: nixosModule documents option installs files to wrong paths”*  
   Nix users report that personality/memory files are stored in `workingDirectory` instead of `$HERMES_HOME`, breaking Her‑mes configuration.  
   🔗 [NousResearch/hermes-agent Issue #21341](https://github.com/NousResearch/hermes-agent/issues/21341)

4. **#24072** (4 comments, P2)  
   *“Bug Report: model.context_length persists across /model provider switches”*  
   A subtle configuration bug that does not re‑resolve `_config_context_length` after runtime provider changes, causing silent misbehaviour.  
   🔗 [NousResearch/hermes-agent Issue #24072](https://github.com/NousResearch/hermes-agent/issues/24072)

### Most Reacted Issues

- **#509** (2 👍) — Cognitive memory feature.  
- **#21037** (1 👍, P1) — Vision auto‑detect hang requiring LLM call.  
- **#11701** (1 👍, P3) — Persistent usage/cost footer on gateway messages.

## Bugs & Stability

The project is dealing with **multiple P1‑severity bugs** that directly impact user experience.

### Critical (P1) — Active today

| Issue | Description | Impact | Fix PR exists? |
|-------|-------------|--------|----------------|
| #24140 | Context‑window minimum 64k rejects all models; Telegram bot down | Complete Telegram outage | **No** |
| #24098 | Compression failure hangs main response loop for up to 88 minutes | Silent user blocking | PR #19551 (auxiliary timeouts) partially addresses |
| #23387 | `hermes gateway start` fails on macOS 26.4.1 with launchctl error 125 | macOS users cannot start gateway | **No** |
| #21037 | Hermes hangs after “Vision auto‑detect” with no LLM call | Agent unusable with vision | **No** |
| #24268 | `kimi‑k2.6` context length incorrectly reported as 32K (actual 256K) | Model blocked from use | **No** |

### High (P2) — Active today

- **#24072** – `context_length` persists across provider switches (patch provided in issue).  
- **#21341** – NixOS module file path mismatch.  
- **#23938** / **#21866** – Feishu adapter strips Markdown formatting or renders tables as raw text.  
- **#17244** – MCP server `amap` fails due to unsupported SSE discovery mechanism.  
- **#24280** – `session_search` loads entire conversation before truncation, causing slow recall.  
- **#24218** – DeepSeek v4‑pro sessions show unknown cost in `hermes insights`.  
- **#7674** (old, P2) – Non‑retryable 401 error due to model‑name mutation (`.` → `-`).

### Medium (P3) — Includes regressions

- **#24186** / **#24188** – Kanban dashboard broken (401 Unauthorized + rendering error `COLUMN_LABEL not defined`) after recent update.  
- **#24278** – CLI TUI symbols render as question marks.  
- **#19539** – Compression feasibility check ignores custom provider `context_length` overrides.

## Feature Requests & Roadmap Signals

The community is actively shaping the future of Hermes Agent with a wide range of enhancement proposals. Several are likely candidates for the next minor release based on community interest and existing PRs.

### High‑Interest Features (Likely next‑version candidates)

- **Cognitive Memory Operations** (#509) — LLM‑driven memory encoding, consolidation, and adaptive recall. A companion PR #24283 (MemPalace native plugin) directly implements this vision.  
- **Absolute token threshold for compression** — PR #24279 adds `compression.threshold_tokens` config option, enabling predictable compression unrelated to context percentage.  
- **Gateway auto‑resume hook** — PR #23619 scans sessions on restart and automatically resumes interrupted conversations.  
- **Microsoft Agent 365 governance skill** (#20133) — Proposal for `hermes‑a365` optional skill.  
- **Persistent usage/cost footer** (#11701) — Request to show token usage on every gateway message, with 1 👍.

### Other Notable Requests

- **Per‑model compression thresholds** (#18733)  
- **Skills versioning** (#20352) — Hand‑edited markdown skills need diff/rollback support.  
- **Cron job self‑scheduling** (#24284) — Allow a cron‑triggered workflow to reschedule itself.  
- **Per‑task model override for Kanban workers** (#24206)  
- **Telegram Markdown fix** (#24171) — Replace regex conversion with `telegramify‑markdown`.  
- **WeChat media burst batching** (PR #24274) — Prevent session lockup on rapid file uploads.

## User Feedback Summary

### Expressed Pain Points

- **“Telegram completely down”** — #24140 is the most urgent: users cannot access the bot at all.  
- **“Kanban board inaccessible after update”** — #24186 and #24188 indicate a regression in the dashboard plugin.  
- **“Feishu tables strip all Markdown”** — #23938 affects enterprise users relying on formatted messages.  
- **“MacOS gateway does not start”** — #23387 blocks native launch on modern macOS.  
- **“Vision hangs without any LLM call attempt”** — #21037 suggests a regression in the vision pipeline.  
- **“Unknown costs for DeepSeek models”** — #24218 and #24141 show billing/insights gaps.

### Satisfaction Signals

- Users are contributing patches (e.g., #24072 includes a patch file; PRs #24279, #24283, #24286 are new contributions).  
- The cognitive memory feature (#509) continues to receive positive reactions (2 👍) and has spawned a concrete PR (#24283).  
- Chinese locale support (PR #13140) was merged, showing the community’s global reach.

## Backlog Watch

Several important issues and PRs have remained open for an extended period without maintainer response:

| Item | Age | Last Update | Maintainer Attention |
|------|-----|-------------|----------------------|
| #509 – Cognitive memory feature | Since 2026‑03‑06 (2+ months) | Updated today (comments) | No assignee or milestone visible |
| #7674 – 401 error due to model‑name mutation | Since 2026‑04‑11 (1 month) | Updated today | No PR linked |
| #10663 – MCP connection error | Since 2026‑04‑16 (26 days) | Updated today | Still open |
| #11701 – Persistent usage footer | Since 2026‑04‑17 (25 days) | Updated today | No PR |
| #17244 – MCP amap SSE discovery | Since 2026‑04‑29 (13 days) | Updated today | No fix PR |
| #18733 – Per‑model compression thresholds | Since 2026‑05‑02 (10 days) | Updated today | No PR |
| #19539 – Compression ignores custom provider context_length | Since 2026‑05‑04 (8 days) | Updated today | No PR |
| #20133 – Microsoft Agent 365 skill proposal | Since 2026‑05‑05 (7 days) | Updated today | Awaiting triage |
| #20352 – Skills versioning | Since 2026‑05‑05 (7 days) | Updated today | No PR |

The **longest‑standing issue** (#509) is also the most upvoted community request. Its continued open status suggests either high implementation complexity or a resource bottleneck. Similarly, the MCP‑related bugs (#17244, #10663) have remained unresolved for weeks despite being clearly reported.

**Maintainers should prioritise:**  
1. Restore Telegram functionality (#24140) — most urgent.  
2. Patch the compression hang (#24098) — already partially covered by PR #19551.  
3. Resolve the macOS gateway launch failure (#23387).  
4. Triage and assign milestones to long‑standing feature requests (#509, #18733).  
5. Address Kanban dashboard regression (#24186/#24188).

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-12

## 1. Today's Overview

PicoClaw saw **high activity** over the past 24 hours, with **11 issues updated** (7 closed, 4 still open) and **17 pull requests updated** (6 merged/closed, 11 open). A new **nightly build** (v0.2.8-nightly) was published, though it is marked as potentially unstable. The project continues to receive substantial community contributions, particularly around tooling, channel support, and bug fixes. A notable number of older issues and PRs remain *stale*, indicating a need for maintainer review to keep momentum.

## 2. Releases

- **Nightly Build v0.2.8-nightly.20260512.777269b4**  
  Automated build from `main`. No detailed changelog beyond the compare link to v0.2.8.  
  **⚠️ Use with caution** — may contain unstable changes.  
  **No migration notes** provided.

## 3. Project Progress (Merged/Closed PRs)

Six PRs were merged or closed in the last day:

- **#2852** — *docs: add evolution config controls* (closed)  
  Documents the `evolution` config block for agent self‑evolution, with Web UI configuration support.

- **#2854** — *docs: add LicheeRV‑Claw AliExpress news* (closed)  
  Community documentation update.

- **#2758** — *fix(telegram): media group album handling* (merged)  
  Buffers album updates, preserves captions, and orders media correctly.

- **#2645** — *feat(bedrock): implement StreamingProvider for real‑time token streaming* (merged)  
  Adds `ChatStream` support to the Bedrock (AWS) provider using ConverseStream API.

- **#2581** — *Recover Codex output from streamed message events* (merged)  
  Fixes empty‑payload issue when streaming responses from ChatGPT Codex.

- **#2565** — *fix(config): preserve explicit mention_only=false in GroupTriggerConfig* (merged)  
  Corrects Go’s `omitempty` behavior that silently ignored `mention_only: false`.

## 4. Community Hot Topics

The most active discussions (by comments/reactions) centered on:

- **Issue #2046** (closed, 6 comments) — *[BUG] PicoClaw does not call tool with LongCat API*  
  Underlying need: Provider‑specific tool invocation failures; resolved but highlights need for better provider documentation.

- **Issue #2232** (closed, 5 comments) — *[Feature] Serp API is missing in web search api*  
  Underlying need: Free search API alternatives as Brave becomes paid; community wants SerpAPI integration (250 free queries/month).

- **Issue #2720** (open, high priority, 3 comments) — *[BUG] Singleton PID check doesn’t verify process identity — stale PID causes crash loop*  
  **Critical**: A stale PID (e.g., from `systemd‑resolved`) prevents gateway startup. No fix PR yet.  
  [View Issue #2720](https://github.com/sipeed/picoclaw/issues/2720)

- **Issue #2796** (open, 2 comments) — *[BUG]历史记录中，一次对话有多次用户消息，只能查看到最后一条用户消息*  
  History only shows the last user message in a multi‑message conversation – affects user experience.

- **PR #2830** (open) — *fix(spawn): add explicit async delivery policy with configurable spawn routing*  
  Addresses a real runtime problem where subagent results re‑trigger parent turns unnecessarily. Closes #2829.  
  [View PR #2830](https://github.com/sipeed/picoclaw/pull/2830)

## 5. Bugs & Stability

| Bug | Severity | Status | Fix PR Exists? |
|-----|----------|--------|----------------|
| **#2720** – Singleton PID check doesn’t verify process identity (stale PID crash loop) | **High** – prevents gateway start | Open | No |
| **#2796** – History only shows last user message in multi‑message conversations | **Medium** – data loss in UI | Open | No |
| **#2684** – Skill address parsing error ([BUG] with no title) | **Low** – user‑reported but unclear | Closed | N/A |
| **#2690** – Gateway started with no channels on v0.2.7 | **High** – affected Docker users | Closed | Fixed by config changes |

**Newly identified bugs today**: None directly opened, but #2796 was already open and saw activity.

**PRs addressing stability**:  
- #2768 (open) – *fix(agent): retry transient LLM HTTP errors*  
- #2740 (open) – *fix(deepseek): capture reasoning_content from streaming* (thinking mode)  
- #2647 (open) – *fix: enable web_search tool config YAML support and enable DuckDuckGo by default*

## 6. Feature Requests & Roadmap Signals

Several feature requests point toward upcoming enhancements:

- **#2855** – *[Feature] Extend message tool to support media attachments and channel‑aware rich outbound delivery*  
  PR #2856 is already open implementing this for Telegram. Likely to appear in v0.2.9.

- **#2829** – *[Proposal] explicit async result delivery policy for async tool results*  
  Already addressed by PR #2830 (open). Strong candidate for next release.

- **#2763** – *feat(providers): add gemini web search provider*  
  Adds `web_search` tool support via Gemini grounding. Open PR.

- **#2761** – *feat(subagent): support agent_id on sync subagent*  
  Enables explicit lane selection for synchronous subagent calls.

- **#2232** (closed) – *Serp API integration* – may be revisited if community demand continues.

**Prediction for next minor release (v0.2.9)**: Media attachments in `message` tool, async delivery policy for spawn, Gemini web search provider, and improvements to subagent routing.

## 7. User Feedback Summary

Real pain points expressed by users:

- **“PicoClaw does not call tool with LongCat API”** – Provider‑specific tool invocation gaps frustrate users.
- **“Service does not start in the Android app”** – Build and packaging issues on mobile (fixed in nightly?).
- **“Singleton PID check doesn’t verify process identity”** – Stale PID crashes on restart – **critical** for server deployments.
- **“History only shows last user message”** – Conversation continuity broken in Web UI.
- **“Search API 额度耗尽时缺少自动 Fallback 机制”** – No automatic fallback when search API rate limit is hit; community proposed Brave → Tavily → Perplexity → DuckDuckGo chain.
- **Lack of Raspberry Pi support** – User requested official instructions for Pi Zero 2W (closed as an enhancement, but no binary release yet).

Overall, satisfaction is tempered by stability issues and missing features, but community engagement remains strong with detailed bug reports and proposed solutions.

## 8. Backlog Watch

Issues and PRs that have gone **stale** (no maintainer response in >1 week) and require attention:

| Item | Type | Last Activity | Impact |
|------|------|---------------|--------|
| **#2720** – Singleton PID check | Bug (high) | Updated 2026‑05‑12 (comments from Apr 30) | **Critical** – no progress, no fix PR |
| **#2796** – History message bug | Bug (medium) | Updated 2026‑05‑11 (no maintainer response) | User experience regression |
| **PR #2647** – web_search YAML/DuckDuckGo default | Fix | Last commit Apr 24, awaiting review | Blocks default search provider |
| **PR #2768** – Retry LLM HTTP errors | Fix | Opened May 4, stale 8 days | Stability improvement for provider failures |
| **PR #2761** – agent_id on sync subagent | Feature | Opened May 4, stale | New capability |
| **PR #2740** – DeepSeek streaming reasoning | Fix | Opened May 1, stale | Thinking‑mode parity |

**Maintainer action needed**: Review #2720 (critical), provide feedback on #2796, and respond to open PRs to unblock community contributions.

---
*Generated from GitHub data (github.com/sipeed/picoclaw) – 2026-05-12 12:00 UTC*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-12

## Today's Overview

NanoClaw saw moderate activity today with **5 open issues** and **18 pull requests updated** in the last 24 hours, of which **9 were merged or closed**. No new releases were cut. The merged PRs primarily addressed container output parsing, CLI version bumps, compaction improvements, and channel isolation—indicating ongoing stabilisation of the agent runtime and CLI tooling. Open work continues on Fedora Podman support, Google‑Auth skills, Hindsight long‑term memory integration, and fallback model plumbing. One notable bug surfaced around container mount persistence after daemon restarts.

## Releases

**None** — no new releases were published today.

## Project Progress

**9 PRs were merged or closed today** (all classified as closed; most appear merged). Key highlights:

- **Container & runtime fixes**  
  [`#1912`](https://github.com/nanocoai/nanoclaw/pull/1912) – Fix fallback output parser in `runContainerAgent` to surface clear errors on empty container stdout.  
  [`#2414`](https://github.com/nanocoai/nanoclaw/pull/2414) – Poll‑loop now nudges the agent when output lacks `<message>` wrapping (prevents silent drops).  
  [`#2413`](https://github.com/nanocoai/nanoclaw/pull/2413) – Compaction summary now places the destination‑reminder at the end for better compliance.  
  [`#2412`](https://github.com/nanocoai/nanoclaw/pull/2412) – Reverts problematic compaction reminder injection from PR #2327 that caused agent to send unintended messages.

- **CLI & configuration**  
  [`#2425`](https://github.com/nanocoai/nanoclaw/pull/2425) – Bumped pinned container CLI versions (`@anthropic-ai/claude-code` 2.1.119 → 2.1.139, `agent-browser` pinned to 0.27.0, etc.).  
  [`#1785`](https://github.com/nanocoai/nanoclaw/pull/1785) – Isolated channel connect failures so one broken channel (e.g., expired Gmail OAuth) does not crash the entire service.

- **Skills & integrations**  
  [`#1662`](https://github.com/nanocoai/nanoclaw/pull/1662) – Merged: Sentry IPC integration skill.  
  [`#2419`](https://github.com/nanocoai/nanoclaw/pull/2419) – Merged: `/add-hindsight` skill for per‑group long‑term memory via Hindsight MCP wrapper.  
  [`#63`](https://github.com/nanocoai/nanoclaw/pull/63) – Closed: WhatsApp auth retry logic (originally from Feb 2026).

## Community Hot Topics

No issues or PRs had non‑zero comment or reaction counts in today’s data, but several items drew clear community interest by volume of parallel work:

- **Google‑Auth foundation skill** [`#2422`](https://github.com/nanocoai/nanoclaw/pull/2422) (open) – Adds diagnostic MCP tools and OneCLI‑based OAuth prerequisites. Underlying need: ability to authenticate Google services from within agent groups.
- **Hindsight memory integration** [`#2420`](https://github.com/nanocoai/nanoclaw/pull/2420) (open) – Bundled MCP wrapper for Vectorize‑io’s Hindsight engine. Signals demand for persistent, per‑group long‑term memory.
- **Fallback model support** [`#2417`](https://github.com/nanocoai/nanoclaw/issues/2417) (open) + [`#2418`](https://github.com/nanocoai/nanoclaw/pull/2418) (open) – User‑requested ability to continue a session on a secondary model when the primary hits usage limits. The PR includes both config plumbing and detection logic. This is a high‑value feature for reliability.

## Bugs & Stability

**Critical (2 issues, no fix PRs yet):**
- [`#2424`](https://github.com/nanocoai/nanoclaw/issues/2424) – Container survives daemon restart with partial mount config (missing `/workspace/agent` bind after folder rename). The agent group comes back but loses the group‑level bind—no error surfaced. Potential data loss/corruption risk.
- [`#2423`](https://github.com/nanocoai/nanoclaw/issues/2423) – Outbound delivery failures (Telegram 4xx/5xx, rate limits) are silently swallowed after 3 retries; the agent never knows a message was dropped. This breaks user expectation of reliable message delivery.

**High (1 issue, fix PR exists):**
- [`#2415`](https://github.com/nanocoai/nanoclaw/issues/2415) – `ncl groups create` skips inserting the `container_configs` row, causing first spawn to fail with "Container config not found".  
  **Fix PR:** [`#2416`](https://github.com/nanocoai/nanoclaw/pull/2416) (open) – provisions companion rows on `ncl groups create` and `ncl wirings create`.

**Medium (1 issue, no fix yet):**
- [`#2426`](https://github.com/nanocoai/nanoclaw/issues/2426) – LLM cannot see images in Discord; only receives `[image: file.png]` placeholder text. Reported reproducible. Impacts Discord image‑based workflows.

## Feature Requests & Roadmap Signals

| Request | Type | Likelihood for next release |
|---------|------|-----------------------------|
| **`fallbackModel` for `agent-runner`** (Issue #2417, PR #2418) | Core runtime resilience | Very high – PR already implements plumbing + detection |
| **Fedora Podman support** (PR #2421) | Platform expansion | High – only need review and testing |
| **Google‑Auth skill** (PR #2422) | Integration skill | High – foundation for many Google‑based tools |
| **Hindsight long‑term memory** (PR #2420) | Memory skill | Medium – wrapped MCP, but depends on Hindsight deployment |
| **Unknown slash commands treated as normal chat** (PR #2346) | User experience | Medium – long‑standing issue with silent drops |
| **Rename `@Andy` triggers with non‑default ASSISTANT_NAME** (PR #1913, #1917) | Configuration | Low/Stale – open since April |

The most strong roadmap signal is the fallback model work, which directly addresses a common failure mode. The Fedora support PR suggests growing demand for non‑macOS/Linux deployments.

## User Feedback Summary

- **Reliability pain points**  
  Users report that container mounts can become incomplete after host folder renames without any error (`#2424`), and that outbound message failures are invisible to the agent (`#2423`). Both degrade trust in autonomous workflows.

- **Feature gaps**  
  The inability to see images in Discord (`#2426`) frustrates visual‑task users. The lack of fallback model support (`#2417`) causes mid‑session failures on expensive models.

- **CLI usability**  
  The `ncl groups create` bug (`#2415`) breaks first‑time setup for new agents – a poor onboarding experience flagged by user `glifocat`.

- **Positive signals**  
  Multiple closed PRs today focused on compaction and polling fixes, indicating maintainers are responsive to reported issues around message routing and agent output handling.

## Backlog Watch

Several PRs have been open for **weeks without maintainer activity** and may need attention:

- [`#1913`](https://github.com/nanocoai/nanoclaw/pull/1913) (Apr 22) – Rename `@Andy` triggers when assistant name changes.  
- [`#1916`](https://github.com/nanocoai/nanoclaw/pull/1916) (Apr 22) – Guard numeric config env vars against NaN/non‑positive values.  
- [`#1917`](https://github.com/nanocoai/nanoclaw/pull/1917) (Apr 22) – Rename `@Andy` trigger in runtime group registration.  
- [`#2346`](https://github.com/nanocoai/nanoclaw/pull/2346) (May 8) – Treat unknown slash commands as normal chat.

These address **configuration correctness** and **user‑experience improvements** that have been hanging for 3‑4 weeks. Merging or updating their status would reduce community uncertainty.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-12

## Today's Overview

The project saw moderate activity over the past 24 hours. One high‑severity regression bug (HostResolutionFailed with the `siliconflow` provider) was reported and quickly closed, indicating responsive maintainer attention. Three pull requests remain open, focusing on gateway stability, a new synchronous webhook endpoint, and privacy‑preserving audit enhancements. No new releases were published today. Overall, the project is advancing toward improved infrastructure reliability and feature expansion while maintaining a fast bug‑fix turnaround.

## Releases

*No new releases in the last 24 hours.*

## Project Progress

- **Issue #902** ([bug] HostResolutionFailed with siliconflow provider) was **closed** on 2026-05-11. The regression, introduced in the 2026.5.x HTTP/DNS client refactoring, has been resolved – a clear win for stability.
- No pull requests were merged or closed today. However, three open PRs are actively progressing:
  - **PR #912** – new synchronous webhook endpoint for paired‑token workers.
  - **PR #910** – Discord/WebSocket gateway stability fixes (watchdog, backoff, interrupt‑safe stop, TLS leak fix).
  - **PR #911** – privacy‑preserving LLM triage for workspace audits.

## Community Hot Topics

- **Issue #902** (2 comments, closed) – The most active item, raised by user `agiminds`. The problem (siliconflow provider broken after upgrade) sparked discussion about the regression and its fix.  
  [Issue #902](https://github.com/nullclaw/nullclaw/issues/902)
- **PR #910** – While it has zero comments, its broad soak‑test across four architectures (macOS ARM, Linux aarch64, riscv64, Android) signals strong community interest in gateway stability.  
  [PR #910](https://github.com/nullclaw/nullclaw/pull/910)

## Bugs & Stability

The only bug reported today was **Issue #902** (closed).  
- **Severity:** High – the regression broke the `siliconflow` provider completely for any user on 2026.5.x.  
- **Status:** Fixed. The issue is closed, and the fix likely rolled into upcoming commits.  
- Additional stability improvements are under active development in **PR #910**, which targets gateway robustness (watchdog, backoff, interrupt handling, TLS leak). No other crash or regression reports surfaced in the last 24 hours.

## Feature Requests & Roadmap Signals

Two significant feature PRs are open:

- **PR #912** (`feat(gateway): synchronous /webhook for paired-token workers`) – Addresses a documented high‑priority gap in the integration analysis. This endpoint will enable direct, token‑authenticated webhook responses from workers, likely targeted for the next minor release.
- **PR #911** (`feat(audit): privacy-preserving secret triage`) – Adds optional LLM classification to workspace audits while keeping raw secrets out of LLM calls. This reflects a growing user interest in both automated security analysis and privacy.

Neither PR has been merged yet, so both are candidates for inclusion in the upcoming 2026.5.x patch or 2026.6.x.

## User Feedback Summary

- **Pain point:** The upgrade from 2026.4.9 to 2026.5.x broke the `siliconflow` provider for user `agiminds`. The fast fix reduces dissatisfaction, but indicates that the HTTP/DNS rewrite lacked sufficient backwards‑compatibility testing.
- **Use case:** Multi‑architecture deployment is clearly important – PR #910 was tested on macOS ARM, Linux aarch64, riscv64, and even Android. Users value cross‑platform reliability.
- **Satisfaction:** No negative sentiment beyond the single bug report. The presence of well‑documented PRs (PR #912 references `docs/integration-analysis.md`) suggests the team is addressing roadmap commitments transparently.

## Backlog Watch

No critical long‑standing items were updated in the last 24 hours. The three open PRs are recent and under active review. No unanswered issues older than 24h were surfaced in the provided data. Maintainers should continue to monitor PR #910 (largest change set) for any integration friction.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-12

## 1. Today's Overview

The IronClaw project is in a period of **intense, focused activity**, driven primarily by the “Reborn” architecture overhaul. In the last 24 hours, 43 issues were updated (20 open, 23 closed) and 50 pull requests were touched (36 open, 14 merged/closed). One new minor release (`ironclaw-v0.28.1`) landed yesterday, adding two new communication-channel features. The vast majority of recent work—both merged and in-flight—converges on the Reborn persistence, loop execution, and trust-boundary hardening layers, indicating the team is pushing hard toward a stable Reborn integration branch. Community engagement remains high, with several user-reported bugs receiving prompt attention.

## 2. Releases

### ironclaw‑v0.28.1 — 2026‑05‑11

**Changes:**
- *(channels)* Added `pairing_approve` tool for Slack binding via chat ([PR #3396](https://github.com/nearai/ironclaw/pull/3396)).
- *(channels)* Added WeChat registry artifact metadata ([PR #3386](https://github.com/nearai/ironclaw/pull/3386)).
- *(common)* Described paths and platform–specific behaviour (release notes truncated; further details may be in commit messages).

**Breaking changes:** None announced.  
**Migration notes:** No migration steps required; users upgrading from v0.28.0 can apply the new release directly. The WeChat metadata addition is additive and does not affect existing configuration.

## 3. Project Progress

**Merged/closed PRs today (14 items):** The Reborn initiative continues to absorb the bulk of commits. Notable closures include:

- [#3309 – Make Skills E2E lifecycle deterministic](https://github.com/nearai/ironclaw/pull/3309): Replaced live ClawHub-dependent UI tests with deterministic Playwright API mocks, improving CI reliability.
- [#3303 – Refactor(reborn-memory): e2e coverage](https://github.com/nearai/ironclaw/pull/3303): Added 1,690 LOC of E2E tests for the Reborn memory substrate (libSQL-only) without any production code change.
- Several Reborn “bookkeeping” issues closed that define contracts for turn admission, loop checkpoints, and run‑wake notification (e.g., [#3264](https://github.com/nearai/ironclaw/issues/3264), [#3451](https://github.com/nearai/ironclaw/issues/3451), [#3435](https://github.com/nearai/ironclaw/issues/3435)).

**Features advanced today:**
- **Reborn runtime adapters:** FirstParty and System runtime adapter paths ([#3466](https://github.com/nearai/ironclaw/issues/3466), [#3478](https://github.com/nearai/ironclaw/issues/3478)) were closed, enabling execution of host-owned capabilities through the kernel-mediated flow.
- **Loop model milestones:** PR [#3487](https://github.com/nearai/ironclaw/pull/3487) added durable event projection for model/reply milestones, essential for observability.
- **Text-only AgentLoopDriverHost factory** ([#3407](https://github.com/nearai/ironclaw/issues/3407)) closed, completing the first concrete per-run host object for text-only loop profiles.
- **Docker image publishing** ([#748](https://github.com/nearai/ironclaw/issues/748)) saw renewed activity after weeks of quietness, though the issue remains open.

## 4. Community Hot Topics

### Most commented issues (last 24h update)

| Issue | Comments | Link |
|-------|----------|------|
| #3193 – Define conversation binding and session thread contracts (closed) | 6 | [↗](https://github.com/nearai/ironclaw/issues/3193) |
| #3204 – Define transcript and thread storage boundary (closed) | 5 | [↗](https://github.com/nearai/ironclaw/issues/3204) |
| #3069 – Ship Reborn as a separate `ironclaw-reborn` binary (closed) | 4 | [↗](https://github.com/nearai/ironclaw/issues/3069) |
| #3107 – Define AgentLoopDriver and run-class profile contract (closed) | 4 | [↗](https://github.com/nearai/ironclaw/issues/3107) |
| #748 – Publish ironclaw-worker Docker image (open, 6 👍) | 1 | [↗](https://github.com/nearai/ironclaw/issues/748) |

### Analysis

The highest-activity discussions center on **architectural contracts for Reborn**—conversation binding, thread storage, binary separation, and loop driver definitions. These are all closed now, signalling that the design phase is largely complete and the team is executing on implementation.  
Issue #748 (Docker image publishing) has been a long-standing community pain point with six 👍 reactions; the recent update suggests maintainers are finally addressing it, though no PR has been merged yet.

## 5. Bugs & Stability

### High severity

- **[#3500 – Local web UI undiscoverable through onboarding](https://github.com/nearai/ironclaw/issues/3500)**  
  *Reported 2026‑05‑11* – Fresh local installs drop users into the TUI without any hint that `http://localhost:3000` is available or how to enable it.  
  **Fix PR exists:** [#3510](https://github.com/nearai/ironclaw/pull/3510) (open, size: XL, risk: high).  

- **[#3490 – Admin tools settings not propagated to users](https://github.com/nearai/ironclaw/issues/3490)**  
  *Reported 2026‑05‑11* – In multi-tenant setups, disabling the “shell” tool for an admin does not cascade to user agents, creating a security bypass.  
  **No fix PR yet.**

### Medium severity

- **[#3128 – Connecting to Gmail gives 502 error](https://github.com/nearai/ironclaw/issues/3128)**  
  *Reported 2026‑04‑30* – Authentication flow fails at callback link with 502; installing via settings works. Issue is one week old with no maintainer response.  

- **[#2903 – Telegram long response fails silently](https://github.com/nearai/ironclaw/issues/2903)**  
  *Reported 2026‑04‑23, closed 2026‑05‑11* – Very long responses from Telegram are dropped without notification. The issue has been closed, but no public fix PR was linked; likely resolved internally.

- **[#3317 – Telegram setup did not work with local IronClaw](https://github.com/nearai/ironclaw/issues/3317)**  
  *Reported 2026‑05‑06, closed 2026‑05‑11* – Setup flow failed with unclear error screens. Closed, presumably fixed.

### Long-standing

- **[#748 – Docker sandbox image not published](https://github.com/nearai/ironclaw/issues/748)**  
  *Opened 2026‑03‑09* – `ironclaw-worker:latest` is absent from any public Docker registry, breaking sandbox features for most users. Activity resumed today (2026‑05‑11) but no resolution yet.

## 6. Feature Requests & Roadmap Signals

**Recently requested features:**

- **[#3515 – WeChat channel documentation](https://github.com/nearai/ironclaw/issues/3515)** (opened today) – Now that WeChat is working in v0.28.1, a docs page for the channel is needed. This is a small, high-priority task that will likely land in the next patch release.

- **[#1494 – Add email/password signup option](https://github.com/nearai/ironclaw/issues/1494)** (closed today) – This feature request was marked as closed; the team may have decided to postpone or implement it in a different manner.

- **[#2394 – WeCom (Enterprise WeChat) channel](https://github.com/nearai/ironclaw/pull/2394)** (open PR) – A standalone WASM-based WeCom channel is under active development. Given the recent Slack and WeChat additions, this is likely to be included in v0.29.

**Roadmap signals:**
- The Reborn initiative is nearing completion of its core contracts; issues closed today include the first-party and system runtime adapters, loop checkpoint staging, and run-wake notification. Expect a Reborn integration branch to be merged into `main` within the next 1–2 sprints.
- Trust-boundary hardening ([#3492](https://github.com/nearai/ironclaw/issues/3492)) was opened and a corresponding PR ([#3494](https://github.com/nearai/ironclaw/pull/3494)) started today – security hardening is a clear priority for the upcoming releases.

## 7. User Feedback Summary

**Pain points expressed:**
- **Telegram silent failures** (#2903) – users receiving no feedback when responses exceed length limits. Closed without visible fix, which may frustrate affected users.
- **Gmail 502 during OAuth** (#3128) – authentication flow breaks at the callback URL; workaround exists (install via settings) but not documented.
- **Admin tool restrictions ignored** (#3490) – a security-related misconfiguration that undermines multi-tenant tenancy.
- **Local web UI invisible** (#3500) – newcomers have no discoverable way to access the web interface after local installation.

**Use cases highlighted:**
- Multi-tenant administration – needs proper tool isolation.
- Docker sandbox onboarding – still broken for new contributors.
- Social-channel integration (WeChat, Telegram, Gmail) – high demand but stability issues persist.

**Satisfaction indicators:**
- The pace of bug fixes (23 issues closed in 24h) suggests maintainers are responsive.
- Community members are actively filing clear, reproducible bug reports, indicating continued engagement.

## 8. Backlog Watch

| Issue | Age | Status | Why it matters |
|-------|-----|--------|----------------|
| [#748 – Publish ironclaw-worker Docker image](https://github.com/nearai/ironclaw/issues/748) | 64 days | Open, 6 👍, no maintainer assignment | Blocks Docker sandbox for most users; new contributors cannot test sandbox-dependent features. Activity today (2026-05-11) gives hope for a fix soon. |
| [#3128 – Gmail 502 error](https://github.com/nearai/ironclaw/issues/3128) | 12 days | Open, no maintainer comment | Authentication flow is a critical onboarding path; the lack of response could mean temporary deprioritisation. |
| [#3490 – Admin tools not propagated](https://github.com/nearai/ironclaw/issues/3490) | 1 day | Open, no fix PR yet | Security misconfiguration; should be escalated given its severity. |
| (No other old, high-comment issues remain open; the team has been vigilantly closing stale items.) | | | |

**Overall assessment:** The project is healthy and shipping quickly, though several user-facing bugs need priority triage. The Reborn architectural shift is absorbing most developer capacity, but it promises to improve extensibility and security in the medium term.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Okay, here is the project digest for LobsterAI, based on the provided GitHub data for 2026-05-12.

---

## LobsterAI Project Digest | 2026-05-12

### 1. Today's Overview

LobsterAI shows extremely high development activity today, with a massive wave of 18 pull requests (PRs) being merged or closed. This indicates a focused push to finalize features and polish the codebase. The core team, led by contributor `fisherdaddy`, drove a significant cleanup and enhancement sprint, concentrating on UI/UX improvements for the chat interface and agent management, as well as critical infrastructure changes like telemetry removal. A notable new feature for voice input was also introduced and merged, demonstrating rapid iteration. While no new releases were cut, the project is in a state of intensive refinement.

### 2. Releases

None.

### 3. Project Progress

Today’s activity is defined by a large batch of merged PRs, signaling the completion of a significant development cycle.

- **UI/UX Overhaul**: A major focus was on polishing the user interface. PRs were merged optimizing the main UI (#1937), agent layout (#1924), agent UI (#1911), input UI (#1946), and model selection UI (#1954). This suggests a concerted effort to refine the user experience for the upcoming release.
- **Core Feature: Voice Input**: The team merged a major feature adding a voice input button for chat (PR #1947). This utilizes OS-native speech-to-text (Win+H on Windows, Fn+Fn on macOS) rather than a web-based API, ensuring privacy and reliability. A follow-up fix (PR #1952, still open) adds error handling for when users deny microphone permissions on macOS.
- **Infrastructure Cleanup**: A critical PR (#1950) was merged to clean up telemetry code. The update check system was permanently disabled and centralized endpoints were removed, significantly enhancing user privacy by cutting the last remaining telemetry link.
- **Bug Fixes & Stability**: Several bugs were addressed, including a fix for incorrect timestamps in chat history (#1936), a batch delete task glitch (#1939), and a persistent model selection issue after restart (#1905).
- **Artifact & Code Block Enhancements**: The preview module received multiple fixes and enhancements (#1945), including support for Mermaid diagrams (.mermaid/.mmd) and resolving issues with PPTX previews and pinch-to-zoom. The code block toolbar was also refined for better rendering clarity (#1951).

### 4. Community Hot Topics

Today's activity was dominated by internal development, but one PR stands out as a high-interest, user-facing feature.

- **[[OPEN] #1952](netease-youdao/LobsterAI PR #1952): fix(voice): macOS 语音输入权限拒绝后显示 toast 提示** (Fix(voice): Show toast prompt when macOS voice input permission is denied)
    - **Author**: btc69m979y-dotcom | **Last Updated**: 2026-05-12
    - **Analysis**: This PR directly addresses a user pain point identified from the new voice input feature (PR #1947). The initial implementation could fail silently on macOS if the user denied accessibility permissions. This hotfix ensures clear feedback is provided, guiding users to enable the necessary system setting. It reflects a user-centered approach to feature rollout, anticipating and resolving common friction points.

### 5. Bugs & Stability

No new issues were filed today, but several bugs were proactively fixed by the development team through PRs.

- **High Severity: macOS Voice Input Permission Denial (PR #1952)**: A fix is in progress for the new voice feature where denying permissions on macOS results in a non-responsive button. The fix will show a clear instruction toast. This is high severity as it causes a feature to fail silently on a major platform.
- **Medium Severity: UI/UX Rendering & Display Issues**: Multiple fixes addressed display glitches, such as incorrect timestamps in IM chat history (#1936). A fix for convoluted code block rendering (#1951) and a scroll gutter instability in the cowork chat (#1949) were also merged, pointing to ongoing polish of the rendering layer.
- **Low Severity: Batch Delete Task Functionality (PR #1939)**: A specific issue where the batch delete function for tasks was not working was identified and resolved.

### 6. Feature Requests & Roadmap Signals

The merged PRs provide a clear signal for the features planned for the next version.

- **Intelligent Input (Likely for Next Version)**: The **voice input feature** (PR #1947) is a strong signal. It suggests a roadmap towards more natural, multi-modal interaction with AI agents, moving beyond just text.
- **Agent Management Improvements**: The feature for **independent working directories for each Agent** (PR #1904) is a significant architectural enhancement that was recently merged. This signals a roadmap direction towards giving users more granular control and isolation over their agents' contexts and data.
- **Enhanced Preview Capabilities**: The comprehensive fixes and enhancements to the **artifact preview module** (PR #1945), including support for Mermaid diagrams and better file search, indicate a focus on making the built-in preview a more powerful and versatile tool, especially for developers.

### 7. User Feedback Summary

No direct user feedback is available in today's data.

### 8. Backlog Watch

- **[[OPEN] #1277](netease-youdao/LobsterAI PR #1277): chore(deps-dev): bump the electron group across 1 directory with 2 updates**
    - **Author**: dependabot[bot] | **Last Updated**: 2026-05-11 (Age: ~40 days)
    - **Analysis**: This dependabot PR, which updates `electron` and `electron-builder`, has been open for over a month. While not a functional issue, failing to keep up with major dependency updates (e.g., Electron 40.x to 42.x) can lead to security vulnerabilities and introduces extra work when catching up. This PR may require maintainer review to ensure it doesn't break compatibility, especially given the significant number of UI changes being made in other PRs.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-12

## Today’s Overview
Over the past 24 hours, the Moltis project saw moderate activity with four issues and two pull requests updated. Three issues were closed, while one remains open, and both PRs were merged. No new releases were published. The team focused on fixing sandbox and Proxmox installation failures, suggesting ongoing stability improvements. Overall, the project is in a healthy maintenance rhythm, with quick turnaround on reported bugs.

## Releases
No releases were published today. The last version remains unchanged since the previous digest.

## Project Progress
Two pull requests were merged today, both addressing recent regressions:

- **[PR #992](https://github.com/moltis-org/moltis/pull/992)** — *fix(install): avoid Proxmox Docker prompt failure*  
  Resolves an issue where the Docker sandbox prompt would fail during LXC installation due to non-interactive `lxc-attach`. The fix preserves interactive behavior when a TTY is available and defaults to the `MOLTIS_INSTALL_DOCKER` environment variable or `no` otherwise. Also keeps root and website installer copies synchronized.

- **[PR #989](https://github.com/moltis-org/moltis/pull/989)** — *fix(sandbox): update discrawl module path*  
  Corrects the Go module path for discrawl from the stale `github.com/steipete/discrawl` to the new `github.com/openclaw/discrawl`. Updates bundled skill metadata and adds a Dockerfile regression test to prevent reintroducing the old path.

Both PRs directly address bugs reported earlier today (Issues #988 and #991/993), showing a responsive development cycle.

## Community Hot Topics
No issues or PRs generated significant reaction counts (all have zero 👍). However, the following items attracted comments or remain open:

- **[Issue #990](https://github.com/moltis-org/moltis/issues/990)** — *[Bug]: User defined agent modes doesn't work* (Closed, 1 comment)  
  The sole comment likely contains additional context. The issue was closed quickly, indicating either a simple fix or a known configuration workaround was shared.

- **[Issue #993](https://github.com/moltis-org/moltis/issues/993)** — *[Bug]: Proxmox script - LXC Creation fails on 91* (Open, 0 comments)  
  This is currently the only open bug. It mirrors Issue #991 (closed after PR #992) but at a different line number, suggesting a related regression that may need a separate fix.

The underlying need appears to be **reliable Proxmox LXC provisioning**, which is a critical path for users deploying Moltis in containerised environments.

## Bugs & Stability
Four bugs were reported today, all classified as *bug*. They are ranked by severity based on impact and fix status:

| Severity | Issue | Description | Fix Available? |
|----------|-------|-------------|----------------|
| **High** | [#991](https://github.com/moltis-org/moltis/issues/991) | Proxmox LXC creation fails on Line 29 | ✅ Fixed via PR #992 |
| **Medium** | [#993](https://github.com/moltis-org/moltis/issues/993) | Proxmox LXC creation fails on Line 91 | ❌ Open / no fix yet |
| **Medium** | [#988](https://github.com/moltis-org/moltis/issues/988) | discrawl repo URL change breaks sandbox container build | ✅ Fixed via PR #989 |
| **Low** | [#990](https://github.com/moltis-org/moltis/issues/990) | User-defined agent modes don’t work | ✅ Closed (presumably fixed or resolved without code change) |

The Proxmox line‑91 failure (Issue #993) remains the most pressing unresolved stability issue. It was reported by the same user as #991 (Thndr), suggesting a systematic problem with the installation script.

## Feature Requests & Roadmap Signals
No explicit feature requests were observed in today’s data. All activity centred on bug fixes. However, the repeated attention on **Proxmox LXC support** and **sandbox construction** may indicate that users are increasingly deploying Moltis in virtualised or containerised environments. Future versions may include more robust LXC setup scripts or interactive installation fallbacks.

## User Feedback Summary
User pain points emerge clearly from the bug reports:

- **Proxmox installation fragility** (Issues #991 and #993): The LXC creation script fails at two distinct lines, likely due to missing dependencies or environment assumptions. The user Thndr filed both, indicating frustration with repeat failures.
- **Sandbox build breaks on external dependency changes** (Issue #988): The discrawl module path changed upstream, breaking container builds. This highlights a lack of dependency pinning or automatable update checks.
- **User-defined agent modes not working** (Issue #990): The reporter bsarkisov followed the preflight checklist and had expected configuration issues that were quickly resolved.

Satisfaction is implied by the rapid closure of three of the four issues, but the open ticket (#993) may cause continued dissatisfaction for Proxmox users.

## Backlog Watch
The only open issue from the last 24 hours is:

- **[Issue #993](https://github.com/moltis-org/moltis/issues/993)** — *Proxmox script - LXC Creation fails on Line 91*  
  Created 2026-05-11, no comments, no assignee. This is a regression directly related to the recently merged PR #992 (which fixed line 29). A follow‑up PR or patch is needed to address line 91. Maintainers should investigate whether the fix for line 29 introduced this new failure.

No other long‑unanswered issues were observed in the limited dataset. The project’s backlog appears well‑managed today.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-05-12

## Today's Overview
The CoPaw project saw intense activity on 2026-05-12, with **46 issues** and **38 pull requests** updated in the last 24 hours. Of those issues, 24 were closed and 22 remain open, while 27 PRs were merged or closed and 11 are still open. No new releases were published today. The high churn (nearly 70% of updated items closed) indicates a responsive maintainer team and active community debugging. Key areas of attention include memory index synchronisation, shell command handling, multi-agent delegation, and MCP (Model Context Protocol) error handling. The project continues to evolve rapidly, with several feature PRs merging today (e.g., user message newlines, chat floating UI, Feishu QR authentication).

## Releases
*No new releases in the last 24 hours.*  
The latest release remains v1.1.5.post2 (reported in issues), with v1.1.6 already referenced in some open bugs (e.g., #4220). Users upgrading from v1.1.5 to post2 have reported regressions in the OpenCode provider (#4133) and DashScope configuration (#4159), which remain unresolved.

## Project Progress
**Merged/closed PRs today** (27 items) include several notable advances:

- **Browser idle watchdog fix** ([PR #2843](https://github.com/agentscope-ai/QwenPaw/pull/2843)) – Resolved a bug where the browser process would not exit after idle timeout.
- **CoPaw → QwenPaw renaming** ([PR #3204](https://github.com/agentscope-ai/QwenPaw/pull/3204)) – Utility namespace migration completed.
- **Browser start strategy & private mode** ([PR #3164](https://github.com/agentscope-ai/QwenPaw/pull/3164)) – Improved Playwright startup flow to reduce automation detection.
- **ACP-based external agent delegation** ([PR #3340](https://github.com/agentscope-ai/QwenPaw/pull/3340) & [#4197](https://github.com/agentscope-ai/QwenPaw/pull/4197)) – Added async execution for `delegate_external_agent`, enabling long-running external tasks.
- **ACP SDK upgrade & runner UI** ([PR #3589](https://github.com/agentscope-ai/QwenPaw/pull/3589)) – Adopted official ACP Python SDK and added a dedicated ACP runner configuration page in the Console.
- **ACP agent rename/delete** ([PR #3859](https://github.com/agentscope-ai/QwenPaw/pull/3859)) – Frontend support for managing custom ACP agents.
- **ACP documentation polish** ([PR #3741](https://github.com/agentscope-ai/QwenPaw/pull/3741)) – Improved docs and added link in ACP config page.
- **Chat floating module** ([PR #4240](https://github.com/agentscope-ai/QwenPaw/pull/4240)) – Chat panel can now be pinned in the menu.
- **User message newline support** ([PR #4231](https://github.com/agentscope-ai/QwenPaw/pull/4231)) – Closes issues #4216 and #2712, allowing line breaks in user input.
- **MCP monkey-patch fix** ([PR #4245](https://github.com/agentscope-ai/QwenPaw/pull/4245)) – Addresses MCP error handling (related to open bug #4227).
- **Feishu QR bot creation** ([PR #4236](https://github.com/agentscope-ai/QwenPaw/pull/4236)) – Added OAuth Device Flow for easier bot setup.
- **Plugin install/uninstall from Console** ([PR #4214](https://github.com/agentscope-ai/QwenPaw/pull/4214)) – Users can now manage plugins via the web UI.
- **ADBPG long-term memory manager** ([PR #2308](https://github.com/agentscope-ai/QwenPaw/pull/2308)) – Pluggable memory backend with AnalyticDB PostgreSQL support (closed after review).

A significant feature PR ([#4210](https://github.com/agentscope-ai/QwenPaw/pull/4210)) is still open, adding a new **Inbox system** and optimized cron job scheduling – a major roadmap item.

## Community Hot Topics
The most-discussed issues (by comment count) reveal core pain points:

1. **Interrupted agent message** ([#2429](https://github.com/agentscope-ai/QwenPaw/issues/2429)) – 11 comments, closed. User encountered "I noticed that you have interrupted me" during cron job testing. Root cause identified (agent state handling) and resolved.
2. **OpenCode provider broken after upgrade** ([#4133](https://github.com/agentscope-ai/QwenPaw/issues/4133)) – 10 comments, closed. Regression in v1.1.5.post2, reported to work in v1.1.5. Likely a config migration issue.
3. **DashScope provider not reading config** ([#4159](https://github.com/agentscope-ai/QwenPaw/issues/4159)) – 6 comments, **open**. A high-severity regression where `dashscope.json` is ignored, resulting in empty `api_key`. Multiple users affected.
4. **Page load slowness** ([#3499](https://github.com/agentscope-ai/QwenPaw/issues/3499)) – 6 comments, closed. Intermittent `curl` latency; likely backend/network issue.
5. **Network fluctuation causing agent failures** ([#2435](https://github.com/agentscope-ai/QwenPaw/issues/2435)) – 6 comments, closed. Serious environment-specific issue with shell command timeouts and GitHub API failures.
6. **Auto-memory writes file but doesn't sync vector index** ([#4220](https://github.com/agentscope-ai/QwenPaw/issues/4220)) – 4 comments, **open**. New session `memory_search` returns empty after auto-memory summary. A fix PR ([#4224](https://github.com/agentscope-ai/QwenPaw/pull/4224)) has been submitted.
7. **FunctionCallOutput validation error** ([#3969](https://github.com/agentscope-ai/QwenPaw/issues/3969)) – 4 comments, closed. `call_id` being `None` caused crashes; `loop_config.json` corruption also noted.
8. **Chat cannot open due to malformed tool_use** ([#4185](https://github.com/agentscope-ai/QwenPaw/issues/4185)) – 4 comments, closed. Persisted session file with bad `tool_use` entry blocks UI opening.
9. **Approval timeout without user prompt** ([#2193](https://github.com/agentscope-ai/QwenPaw/issues/2193)) – 4 comments, closed. Tool approval hung for 2928 seconds because user was never prompted.
10. **Multiple file attachments** ([#4192](https://github.com/agentscope-ai/QwenPaw/issues/4192)) – 4 comments, closed. Feature request for Ctrl/Shift select; acknowledged.

Underlying needs: **Configuration reliability** after upgrades (#4133, #4159), **memory persistence** (#4220), **approval UX** (#2193, #4238), and **stability of shell execution** (#2435, #3183).

## Bugs & Stability
**Bugs reported today (2026-05-12):**

| # | Title | Severity | Status | Fix PR? |
|---|-------|----------|--------|---------|
| [#4244](https://github.com/agentscope-ai/QwenPaw/issues/4244) | `shell_evasion_checks.newlines=True` silently blocks multiline commands | **High** – agent thought chain chaos | Open | No |
| [#4227](https://github.com/agentscope-ai/QwenPaw/issues/4227) | MCP `stream_http` blocks until timeout on 401 response (other errors too) | **High** – blocks MCP workflow | Open | PR #4245 (merged today, may address) |
| [#4238](https://github.com/agentscope-ai/QwenPaw/issues/4238) | Approval process loops infinitely | **Medium** – user cannot proceed | Open | No |
| [#4213](https://github.com/agentscope-ai/QwenPaw/issues/4213) | Web page delivers entire large conversation at once, causing freeze | **Medium** – UI performance | Open | No |
| [#4243](https://github.com/agentscope-ai/QwenPaw/issues/4243) | Browser cannot download files | **Medium** – file export broken | Open | No |
| [#3816](https://github.com/agentscope-ai/QwenPaw/issues/3816) | macOS Desktop: `file://` links not clickable | **Medium** – local file access | Open | No |
| [#4239](https://github.com/agentscope-ai/QwenPaw/issues/4239) | Packaged desktop client does not open external links in browser | **Low** – documentation links | Open | No |
| [#4170](https://github.com/agentscope-ai/QwenPaw/issues/4170) | Agent actions displayed only after all actions finish (delayed UI) | **Medium** – user cannot monitor progress | Open | No |

**Regressions:**  
- **DashScope provider ignored** (#4159) – open, no fix PR yet.  
- **OpenCode provider broken** (#4133) – closed but root cause may not be patched in release.  

**Fixed today:**  
- `auto_memory_interval` index sync (#4220 → PR #4224 merged).  
- MCP monkey patch (#4245) aims to fix #4227 but requires verification.  
- Browser idle watchdog (#2843) closed.  
- A few closed bugs (#4185, #3969, #2193) were resolved in earlier PRs.

## Feature Requests & Roadmap Signals
**New feature requests today (highest activity):**

- **Multiple file attachments** ([#4192](https://github.com/agentscope-ai/QwenPaw/issues/4192)) – closed as enhancement; likely to appear in next release.
- **Adaptive shell execution mode** ([#4045](https://github.com/agentscope-ai/QwenPaw/issues/4045)) – closed; suggests `execute_shell_command` should choose sync/async based on command type.
- **Align multi_agent_collaboration skill with built-in tools** ([#4211](https://github.com/agentscope-ai/QwenPaw/issues/4211)) – open; requests updating the skill to use `list_agents`, `chat_with_agent`, etc. instead of `qwenpaw agents chat`.
- **Feishu large file sending** ([#4228](https://github.com/agentscope-ai/QwenPaw/issues/4228)) – closed; file size limit for Feishu channel.
- **Inbox & cron optimization** ([PR #4210](https://github.com/agentscope-ai/QwenPaw/pull/4210)) – open but substantial; adds one-time and recurring scheduled jobs with inbox delivery.
- **New plugins: Qwen-Image, Wan 2.7** ([PR #4248](https://github.com/agentscope-ai/QwenPaw/pull/4248)) – open; adds DashScope-based image generation and video generation tools.
- **Matrix E2EE enhancements** ([PR #4120](https://github.com/agentscope-ai/QwenPaw/pull/4120)) – open; improves Matrix channel configuration and end-to-end encryption verification.
- **System tray for Windows** ([PR #4041](https://github.com/agentscope-ai/QwenPaw/pull/4041)) – open; allows background operation and auto-start.
- **Tauri 2.x desktop app** ([PR #3813](https://github.com/agentscope-ai/QwenPaw/pull/3813)) – open; wraps Console frontend with Tauri for a native desktop experience.

**Prediction for next version (likely v1.1.7 or v1.2.0):**  
The Inbox + cron overhaul (#4210) is a strong candidate. The memory index fix (#4224) and MCP error handling (#4245) should land. Plugin management from Console (#4214) and new image/video plugins (#4248) may also ship. The multi-agent skill alignment (#4211) could be fast-tracked.

## User Feedback Summary
**Pain points expressed:**

- **Upgrade breakage:** Users upgrading from v1.1.5 to v1.1.5.post2 lost OpenCode and DashScope provider functionality. (Issues #4133, #4159)
- **Memory not syncing:** Auto-memory wrote files but new sessions couldn’t search them – breaks continuity. (#4220)
- **Approval UX:** “Approval timeout with no prompt” (#2193) and infinite approval loops (#4238) frustrate users who cannot unblock workflows.
- **Shell environment:** Users on Ubuntu/Debian complain `/bin/sh` is used instead of the user’s shell, causing `bash`-specific commands to fail. (#3767, #3183)
- **Large conversation handling:** Web UI becomes unresponsive while fetching huge chat histories. (#4213)
- **File operations:** Inability to download files from browser (#4243) and open local file links on macOS (#3816). Also, Feishu can’t send files >30 MB (#4228).
- **Configuration reliability:** Even when `dashscope.json` is correct, the app reports missing API keys. (#4159)

**Satisfaction signals:**
- The community actively contributes fixes (first-time contributors: #4224, #4120, #4041, #3813).
- Feature requests like multiple attachments (#4192) and newline support (#2712) were quickly implemented and merged.
- The ACP external delegation feature is maturing with SDK adoption and UI configuration.

## Backlog Watch
**Open issues that need maintainer attention (by age and impact):**

| Issue | Title | Age | Priority Reason |
|-------|-------|-----|----------------|
| [#4159](https://github.com/agentscope-ai/QwenPaw/issues/4159) | DashScope provider config not read | 3 days | High – blocks many Chinese users |
| [#4220](https://github.com/agentscope-ai/QwenPaw/issues/4220) | Auto-memory index not synced | 1 day | High – fix PR #4224 merged, but issue not yet closed; needs verification. |
| [#4244](https://github.com/agentscope-ai/QwenPaw/issues/4244) | Newlines silently blocked by `shell_evasion_checks` | Today | High – agent logic broken |
| [#4227](https://github.com/agentscope-ai/QwenPaw/issues/4227) | MCP 401 causes full timeout | Today | High – blocks MCP integration |
| [#4170](https://github.com/agentscope-ai/QwenPaw/issues/4170) | Action display delayed until completion | 2 days | Medium – user experience |
| [#4213](https://github.com/agentscope-ai/QwenPaw/issues/4213) | Web page streaming/pagination needed | 1 day | Medium – performance |
| [#3816](https://github.com/agentscope-ai/QwenPaw/issues/3816) | macOS Desktop `file://` links not opening | 18 days | Medium – workflow blocker for desktop users |
| [#4239](https://github.com/agentscope-ai/QwenPaw/issues/4239) | Packaged desktop external links not opening | Today | Low – but may affect new desktop adopters |

**Open PRs that could benefit from review:**
- [#4210](https://github.com/agentscope-ai/QwenPaw/pull/4210) (cron & inbox) – large feature, needs thorough review.
- [#3813](https://github.com/agentscope-ai/QwenPaw/pull/3813) (Tauri desktop) – long-standing since April 24, may require rebase.
- [#4041](https://github.com/agentscope-ai/QwenPaw/pull/4041) (system tray) – Windows-only for now, could be extended.
- [#4120](https://github.com/agentscope-ai/QwenPaw/pull/4120) (Matrix E2EE) – first-time contributor, complex encryption logic.

The project is in a healthy state with high community engagement, but two critical regressions (#4159, #4244) and the MCP blocking bug (#4227) need urgent attention.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-12

## 1. Today's Overview

Project activity in the last 24 hours was very low, with a single closed issue and no pull requests or new releases. The only item of note—Issue #584, a security audit workflow—was completed and closed, suggesting focused maintenance rather than feature development. No open issues or PRs are currently being updated, indicating a quiet period for the repository. The absence of new releases and merged PRs points to a pause in active development, though the team may be preparing future work. Overall project health appears stable but idle, with no signs of community distress.

## 2. Releases

*No new releases were published in the last 24 hours.*

## 3. Project Progress

- **Closed/Merged PRs:** 0  
- **Issues resolved:** 1  
  - [#584 chore(security): single-repository deep ai-vulns audit](https://github.com/qhkm/zeptoclaw/issues/584) — *Closed*  
    A complete single-repository vulnerability workflow was run using the role-orchestrator skill. The audit produced `.codex-audit-work` artifacts and shared memory, tracking accepted findings, negative boundaries, and blockers. No other features or fixes were advanced today.

## 4. Community Hot Topics

The only active discussion was around the now-closed security audit:

- **Most active issue:** [#584 chore(security): single-repository deep ai-vulns audit](https://github.com/qhkm/zeptoclaw/issues/584) — 2 comments, 0 reactions  
  *Author: liey1*  
  *Underlying need:* The community (or maintainer) demonstrated a desire for rigorous, evidence-gated vulnerability scanning integrated into the repository workflow. The closure implies the task was completed to satisfaction, but no further discussion or follow-up issues were opened.

No other issues or PRs received comments or reactions in the last 24 hours.

## 5. Bugs & Stability

No new bugs, crashes, or regressions were reported today. The security audit (#584) may have surfaced vulnerabilities, but any findings were marked as accepted or blocked within the audit artifacts and do not appear as open issues. The project currently has no open bug reports.

## 6. Feature Requests & Roadmap Signals

No feature requests were submitted today. The closed security audit suggests the team is prioritizing security tooling and audit automation; future releases may include deeper integration of the role-orchestrator skill for vulnerability workflows. However, without active feature discussions, no concrete roadmap signals can be inferred.

## 7. User Feedback Summary

No user feedback, questions, or pain points were expressed in the last 24 hours. The repository appears to have no open user-reported issues or complaints. This could indicate satisfaction or a lack of active engagement.

## 8. Backlog Watch

No long-unanswered important issues or PRs are currently awaiting maintainer attention. The only issue updated today was promptly closed. The backlog is clean, with no stale items visible from the provided data.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

### ZeroClaw Project Digest — 2026-05-12

## 1. Today’s Overview
ZeroClaw shows **high development activity** with 19 issues and 47 pull requests updated in the last 24 hours. 12 issues were closed and 23 PRs were merged or closed, indicating a strong focus on bug fixing and release preparation. No new public releases were tagged. The project maintains a steady cadence despite lingering high-severity issues and a large integration PR (v0.8.0) remaining in draft status.

## 2. Releases
None. The last tagged version remains 0.7.x; the `integration/v0.8.0` branch is still open.

## 3. Project Progress — Merged/Closed PRs Today
Several important fixes landed today, many directly resolving recently reported bugs:

- **Discord media pipeline** — [#6572](https://github.com/zeroclaw-labs/zeroclaw/pull/6572) closes multiple gaps: inbound attachments now populate `ChannelMessage`, outbound image markers are properly resolved, and video/audio document types are supported.
- **TTS with `stream_mode=partial`** — [#6588](https://github.com/zeroclaw-labs/zeroclaw/pull/6588) fixes silent TTS disabling in Telegram channel.
- **GLM vision capability** — [#6573](https://github.com/zeroclaw-labs/zeroclaw/pull/6573) marks `glm-4.5v` models as vision-capable.
- **`cron_add` error messages** — [#6586](https://github.com/zeroclaw-labs/zeroclaw/pull/6586) provides clear guidance when `schedule` is passed as a plain string.
- **DuckDuckGo search blocks** — [#6582](https://github.com/zeroclaw-labs/zeroclaw/pull/6582) detects 403/redirects and reports actionable errors.
- **Image marker normalization** — [#6183](https://github.com/zeroclaw-labs/zeroclaw/pull/6183) ensures local image paths from skills are rewritten to `[IMAGE:...]` before history replay.
- **Documentation** — [#6554](https://github.com/zeroclaw-labs/zeroclaw/pull/6554) refines the PR review guide; [#6556](https://github.com/zeroclaw-labs/zeroclaw/pull/6556) (issue) closed after the Discord fix.

Other merged PRs include fixes for CI labeler, test failures, and Rust analyzer errors.

## 4. Community Hot Topics
- **Wecom (WxWork) channel support** — [#3090](https://github.com/zeroclaw-labs/zeroclaw/issues/3090) remains the longest-standing feature request (open since March) with 4 comments. Users actively discuss implementation details and reference the openclaw extension.
- **User message loss in Chinese model setups** — [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) (S1, open) has 4 comments and reports a critical blocking bug in single and multi-turn conversations when using Custom/Ollama providers. No fix PR yet.
- **Audit of 153 lost commits** — [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) (open) tracks a bulk revert that removed bug fixes and features. The community is seeking a recovery plan; 2 comments.
- **Large integration PR v0.8.0** — [#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398) is a massive draft PR (28+ components affected) gathering Schema v3 migration, channel improvements, and provider updates. Feedback is invited.

## 5. Bugs & Stability
| Severity | Issue | Status | Summary | Fix PR? |
|----------|-------|--------|---------|---------|
| S1 (workflow blocked) | [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) | Open | User message loss in multi-turn conversations with Custom/Ollama providers | None yet |
| S2 (degraded) | [#6589](https://github.com/zeroclaw-labs/zeroclaw/issues/6589) | Open | Vision fallback bypassed in mixed-provider setups (RouterProvider inconsistency) | None yet |
| S2 | [#6584](https://github.com/zeroclaw-labs/zeroclaw/issues/6584) | Open | OpenAI-compatible providers ignore `reasoning` field, only read `reasoning_content` | [#6587](https://github.com/zeroclaw-labs/zeroclaw/pull/6587) (open) |
| S2 | [#6556](https://github.com/zeroclaw-labs/zeroclaw/issues/6556) | Closed | Discord media send/receive broken (fixed by #6572) | ✅ |
| S2 | [#6415](https://github.com/zeroclaw-labs/zeroclaw/issues/6415) | Closed | TTS disabled when `stream_mode=partial` (fixed by #6588) | ✅ |
| S2 | [#6422](https://github.com/zeroclaw-labs/zeroclaw/issues/6422) | Closed | `cron_add` unhelpful error on plain‑string `schedule` (fixed by #6586) | ✅ |
| S2 | [#6530](https://github.com/zeroclaw-labs/zeroclaw/issues/6530) | Closed | Matrix build failure with `matrix-sdk v0.16.0` (recursion limit) | ✅ |

Overall, 7 S2/S3 bugs were closed today. The most critical open bug remains #6034 (user message loss).

## 6. Feature Requests & Roadmap Signals
- **Wecom (WxWork) channel** ([#3090](https://github.com/zeroclaw-labs/zeroclaw/issues/3090)) — accepted, P2, likely target for v0.8.x.
- **SearXNG search support** ([#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316)) — help-wanted, P2, not yet assigned. Would improve privacy and reliability over DuckDuckGo.
- **Matrix live home-server smoke check** ([#6576](https://github.com/zeroclaw-labs/zeroclaw/issues/6576)) — release-gate for v0.7.6 after matrix-sdk bump.
- **Observability tracing** ([#5986](https://github.com/zeroclaw-labs/zeroclaw/pull/5986)) — open PR adding SSE broadcast for agent turn lifecycle.
- **Claude Code vision support** ([#6549](https://github.com/zeroclaw-labs/zeroclaw/pull/6549)) — open PR to enable image input.
- **NixOS module** ([#6562](https://github.com/zeroclaw-labs/zeroclaw/pull/6562)) — open PR adding systemd multi-instance support.

The large `integration/v0.8.0` PR (#6398) bundles Schema v3 migration, channel fixes for Discord/Matrix, and many provider updates, suggesting a major release is in preparation.

## 7. User Feedback Summary
- **Pain points being actively addressed**: Discord media handling, TTS in streaming mode, confusing cron error messages, and DuckDuckGo blocking — all got fixes this week.
- **Remaining pain points**: Chinese users report message loss in high‑latency setups (#6034) — no fix yet. Documentation errors (outdated Docker install guides) were reported and quickly corrected (#6393 closed).
- **Feature demand**: Wecom (WeChat Work) channel support is the most‑requested integration (#3090), with users pointing to existing openclaw extensions as reference.
- **Satisfaction indicators**: Users filing bugs receive timely responses; 12 of 19 updated issues were closed within 1–3 days of reporting. The project maintainers are responsive.

## 8. Backlog Watch
Items that have been open for a significant time without maintainer action or clear resolution:

| Issue/PR | Age | Status | Notes |
|----------|-----|--------|-------|
| [#3090](https://github.com/zeroclaw-labs/zeroclaw/issues/3090) – Wecom channel | 2 months | Open, accepted, P2 | No assignee; community reference but no PR. |
| [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) – SearXNG search | 1 month | Open, help-wanted, needs‑maintainer‑review | No maintainer response since April. |
| [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) – Audit lost commits | 18 days | Open, in‑progress | One contributor drafted a recovery plan; no PR yet. |
| [#5986](https://github.com/zeroclaw-labs/zeroclaw/pull/5986) – Observability tracing | 20 days | Open, needs‑author‑action | Lacks requested changes since April 25. |
| [#4944](https://github.com/zeroclaw-labs/zeroclaw/pull/4944) – Tool wrapper migration | 45 days | Open, needs‑author‑action | Stalled since March. |
| [#5120](https://github.com/zeroclaw-labs/zeroclaw/pull/5120) – Memory clear rejection | 44 days | Open, no label | Small fix, no review activity. |
| [#6584](https://github.com/zeroclaw-labs/zeroclaw/issues/6584) – Reasoning field not read | 1 day | New | A fix PR (#6587) already exists; needs review. |
| [#6589](https://github.com/zeroclaw-labs/zeroclaw/issues/6589) – Vision fallback bypass | 1 day | New | No response yet; likely requires architectural discussion. |

**Project health assessment**: Very active with rapid bug fixes. The main risk is the number of open, unassigned feature requests (especially Wecom and SearXNG) that may delay user adoption. The v0.8.0 integration branch is a positive signal for a structured release, but its size and draft status warrant monitoring.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*