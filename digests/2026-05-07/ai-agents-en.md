# OpenClaw Ecosystem Digest 2026-05-07

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-07 09:44 UTC

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

## OpenClaw Project Digest — 2026-05-07

### 1. Today's Overview

Project activity remains extremely high, with **500 issues** and **500 pull requests** updated in the last 24 hours. 315 issues were closed (63%), and 151 PRs were merged or closed, indicating rapid resolution of reported problems alongside a large influx of new work. The team shipped **v2026.5.6** as a hotfix to revert a potentially breaking OAuth route change from the previous release. Several critical regressions are under active investigation, particularly around the WeChat plugin, Gateway WebSocket stability, and Telegram forum delivery. The community is highly engaged, with strong demand for cross-platform desktop apps and improvements to tool security and cost controls.

---

### 2. Releases

**v2026.5.6** (released 2026-05-06) is a patch release focused on a single fix:

- **Fix (Doctor/OpenAI Codex):** Reverts the `doctor --fix` repair from v2026.5.5 that rewrote valid `openai-codex/*` ChatGPT/Codex OAuth routes to `openai/*`. That change could break OAuth-only GPT-5.5 setups or inadvertently migrate users onto the OpenAI API-key route. Users who already applied v2026.5.5 and experienced route issues should re-run `doctor --fix` (or manually restore their config) after upgrading.

**No breaking changes or migration notes** beyond the reverted behavior. Users on v2026.5.5 are strongly advised to update.

[Release link](https://github.com/openclaw/openclaw/releases/tag/v2026.5.6)

---

### 3. Project Progress

Today’s merged/closed PRs (151 total in the last 24h) include several notable improvements:

- **feat(realtime‑voice): optional sendVideoFrame** ([PR #78810](https://github.com/openclaw/openclaw/pull/78810)) – Adds an additive vision-input seam to the realtime voice bridge, enabling screen/camera frame input behind a stable type. All new fields are optional; existing providers and channels compile unchanged.

- **Feat/channels list show all and drop auth** ([PR #78456](https://github.com/openclaw/openclaw/pull/78456)) – Overhauls `openclaw channels list` to separate chat channels from model-provider auth profiles and usage/quota snapshots. Hidden channels are now shown with a status indicator, and auth data is removed from the default output.

- **Fix Tavily tool SecretRef runtime config** ([PR #78610](https://github.com/openclaw/openclaw/pull/78610)) – Registers Tavily’s tools as runtime-context factories rather than one-time objects, fixing credential resolution from active runtime config snapshots.

- **fix(agents): zero usage cost for openai‑codex OAuth sessions** ([PR #78814](https://github.com/openclaw/openclaw/pull/78814) – open, but close is expected soon) – Prevents `calculateCost` from being called unconditionally for OAuth/subscription-only `openai-codex` models, which previously showed wrong nonzero cost rates.

Other areas of advancement: improved subagent tool allowlist forwarding, ACP bridge lifecycle handlers, macOS LaunchAgent recovery, and deeper performance profiling for session list caching.

---

### 4. Community Hot Topics

| Issue | Comments | Reactions | Summary |
|-------|----------|-----------|---------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 104 | 74 👍 | **Linux/Windows Clawdbot Apps** – Long-standing request for desktop apps beyond macOS/iOS/Android. High engagement indicates strong user base waiting for cross-platform support. |
| [#41494](https://github.com/openclaw/openclaw/issues/41494) | 11 | 0 | **Gemini reasoning leak** – Internal chain-of-thought visible to users in Telegram. Closed as fixed, but its re-emergence suggests incomplete test coverage for reasoning suppression. |
| [#78232](https://github.com/openclaw/openclaw/issues/78232) | 11 | 1 👍 | **WeChat plugin incompatibility** – After upgrade, `channelRuntime` API changes break inbound message processing. Multiple users affected, highlighting a fragile plugin API boundary. |
| [#78402](https://github.com/openclaw/openclaw/issues/78402) | 10 | 2 👍 | **Gateway connection loop** – Event-loop starvation from stuck tool call causes repeated WebSocket disconnects (codes 1000/1005/1006). First observed after v2026.5.5; likely critical for deployment stability. |
| [#78308](https://github.com/openclaw/openclaw/issues/78308) | 9 | 1 👍 | **Channel‑mediated MCP tool approval** – Users want MCP servers to opt into the existing `/approve <id>` pipeline for state-mutating calls. Suggests growing MCP ecosystem needs better consent controls. |

The community is clearly demanding more robust **cross-platform support**, **plugin API stability**, and **cost/security transparency**. The WeChat plugin breakage is a top pain point due to its popularity, while the Gateway disconnection issue directly impacts uptime for all users.

---

### 5. Bugs & Stability

**Severity: Critical**

- **Gateway repeatedly closes connections (1000/1005/1006) due to event‑loop starvation** ([#78402](https://github.com/openclaw/openclaw/issues/78402)) – After upgrade to v2026.5.5, a stuck tool call triggers WebSocket closure, making the UI and CLI unreachable. No dedicated fix PR yet, but likely related to concurrent processing in PRs like [#78875](https://github.com/openclaw/openclaw/pull/78875) (catalog normalization) or [#77859](https://github.com/openclaw/openclaw/pull/77859) (runtime snapshot clobbering).

**Severity: High**

- **WeChat plugin failures after upgrade** – Multiple interlinked issues: `channelRuntime` API changes break inbound processing ([#78232](https://github.com/openclaw/openclaw/issues/78232)); `fetch failed` in `getUpdates` ([#77837](https://github.com/openclaw/openclaw/issues/77837)); runtime initialization timeout due to module scope isolation ([#78376](https://github.com/openclaw/openclaw/issues/78376)); login TypeError ([#78434](https://github.com/openclaw/openclaw/issues/78434)). These are regression chains from v2026.5.4 API changes. No single fix PR; the team appears to be addressing them piecemeal (e.g., [#78456](https://github.com/openclaw/openclaw/pull/78456) for channels list improvement, but not directly fixing the plugin contract).

- **Telegram Forum Topic Delivery Silently Fails** ([#77248](https://github.com/openclaw/openclaw/issues/77248)) – Responses are generated but never sent via `sendMessage` API. Classic regression with no clear root cause in the data.

- **Compaction triggers every ~5 minutes instead of ~30 minutes** ([#78604](https://github.com/openclaw/openclaw/issues/78604)) – Introduced in v2026.5.5/5.6, still unfixed. Wastes CPU and context window. Related PRs like [#78877](https://github.com/openclaw/openclaw/pull/78877) aim to fix preflight pressure estimation.

**Severity: Medium**

- **Feishu topic session key mismatch** ([#78262](https://github.com/openclaw/openclaw/issues/78262)) – First message uses `messageId`, subsequent use `thread_id`, causing session splitting. Fix PR [#78872](https://github.com/openclaw/openclaw/pull/78872) addresses both native `topic_group` and normal groups.

- **Bedrock ExpiredTokenException after credential file refresh** ([#77551](https://github.com/openclaw/openclaw/issues/77551)) – AWS credentials rotation no longer picked up without gateway restart.

- **WebChat assistant responses not persisted to transcript** ([#76804](https://github.com/openclaw/openclaw/issues/76804)) – 5.2 regression where tool-using turns lose output.

- **tool‑loop detection disabled by default** ([#77474](https://github.com/openclaw/openclaw/issues/77474)) – Default `false` leaves agent looping unattended. Feature exists but not enabled.

---

### 6. Feature Requests & Roadmap Signals

**High community demand (likely next version):**

- **Linux/Windows Clawdbot Apps** ([#75](https://github.com/openclaw/openclaw/issues/75)) – The most‑requested feature (74 👍). Given the maturity of the macOS/iOS/Android apps, porting to Linux/Windows would unlock a huge user base. Likely a mid‑2026 roadmap item, but no maintainer response yet.

- **Channel‑mediated approval for MCP tool calls** ([#78308](https://github.com/openclaw/openclaw/issues/78308)) – Proposal to reuse the `/approve <id>` pipeline for MCP servers. Low implementation cost, high alignment with existing security architecture.

- **Per‑hour spending ceiling to prevent runaway failover costs** ([#38248](https://github.com/openclaw/openclaw/issues/38248) – closed) – Though closed, the underlying problem remains active. The team may integrate cost capping via dynamic provider quotas.

- **Tool allowlist forwarding for subagents** – Already merged as part of PR [#78441](https://github.com/openclaw/openclaw/pull/78441) (adds `toolsAllow` to `sessions_spawn`). Expect it in next stable release.

**Lower priority or speculative:**

- **Rust rewrite for safe/unsafe mode** ([#6731](https://github.com/openclaw/openclaw/issues/6731)) – Radical proposal with only 0 👍. Unlikely to be pursued.

- **WhatsApp sticker send support** ([#7476](https://github.com/openclaw/openclaw/issues/7476)) – Niche feature, but repeated requests suggest plugin maintainers could pick it up.

- **Denylist support for exec‑approvals** ([#6615](https://github.com/openclaw/openclaw/issues/6615)) – Complement to existing allowlist. 7 👍, moderate interest.

- **Security Profile v1.1 (data‑centric, secure‑by‑default)** ([#8719](https://github.com/openclaw/openclaw/issues/8719)) – Comprehensive proposal; 3 👍. Could become a milestone if adoption grows.

**PRs signaling imminent features:**

- **Realtime voice video frames** (PR [#78810](https://github.com/openclaw/openclaw/pull/78810) – merged) – Already landable.
- **Caching provider tool schema normalization** (PR [#78664](https://github.com/openclaw/openclaw/pull/78664) – open) – Performance improvement for embedded agent turns.
- **Defer Codex dynamic tools behind search** (PR [#78854](https://github.com/openclaw/openclaw/pull/78854) – open) – Speeds up Codex mode startup.

---

### 7. User Feedback Summary

**Positive signals:**

- Users are actively requesting **more capability and security features** rather than abandoning the project – a sign of high engagement.
- The team’s rapid hotfix (v2026.5.6) for an OAuth regression was well‑timed, though some users may have already migrated to API keys prematurely.

**Pain points:**

- **WeChat plugin ecosystem fragility** dominates the complaints. Multiple users report clean upgrades failing with cryptic `TypeError: fetch failed` and `runtime initialization timeout`. The pattern suggests the **plugin API contract is insufficiently versioned** or tested across minor releases.
- **Gateway instability** (WebSocket disconnects, high CPU, compaction storms) is eroding trust in the 2026.5.x series. Users report requiring daily restarts.
- **Cost surprises** from failover chains (e.g., using expensive fallback models) are a recurring frustration – users want **predictable budgets** before actual bills arrive.
- **Telegram group owners** are frustrated by silent message drops and missing bot‑to‑bot communication (`allowBots` not supported in Telegram, see [#8295](https://github.com/openclaw/openclaw/issues/8295)).

**Satisfaction:**

- The **Control UI** and **TUI** continue to receive praise for feature depth.
- The **MCP integration** and **plugin ecosystem** are generating enthusiasm, even though stability issues sometimes overshadow them.

---

### 8. Backlog Watch

**Issues needing maintainer response / prioritization:**

| Issue | Created | Updated | Comments | Why It Matters |
|-------|---------|---------|----------|----------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | 2026-05-06 | 104 | Most‑commented issue ever. No maintainer acknowledgment of Linux/Windows plans. |
| [#2597](https://github.com/openclaw/openclaw/issues/2597) | 2026-01-27 | 2026-05-07 | 8 | Context usage percentage in Runtime line – old, unsolved, and directly related to compaction bugs. |
| [#68449](https://github.com/openclaw/openclaw/issues/68449) | 2026-04-18 | 2026-05-07 | 8 | Dreaming plugin stopword list too narrow – affects users relying on automated dreaming pipelines. |
| [#76562](https://github.com/openclaw/openclaw/issues/76562) | 2026-05-03 | 2026-05-07 | 6 | High CPU after upgrade – still no accepted diagnosis. |
| [#75739](https://github.com/openclaw/openclaw/issues/75739) | 2026-05-01 | 2026-05-07 | 5 | Codex harness migration bugs – two runtime‑routing bugs that block production Codex setups. |
| [#78604](https://github.com/openclaw/openclaw/issues/78604) | 2026-05-06 | 2026-05-07 | 5 | Compaction frequency storm – directly impacts performance, fix PRs exist but not merged. |

**PRs stuck in review/triage:**

- [#74508](https://github.com/openclaw/openclaw/pull/74508) (XL, 46 labels) – Large batch fix for Telegram reasoning overflow, per‑token throttler, QQBot SSRF guard. Open since 2026-04-29; likely needs splitting.
- [#71817](https://github.com/openclaw/openclaw/pull/71817) (XL, 46 labels) – Similar monolithic PR for Telegram/Feishu reasoning config. The developer’s approach of stacking many fixes in one PR is causing review delays.

**Maintainer attention needed:**

- **Feishu session splitting** ([#78262](https://github.com/openclaw/openclaw/issues/78262)) has a fix PR [#78872](https://github.com/openclaw/openclaw/pull/78872) that should be fast‑tracked.
- **Compaction preflight estimation** ([#78877](https://github.com/openclaw/openclaw/pull/78877)) directly fixes the compaction storm – priority review.
- The **WeChat plugin stability issues** need a coordinated backport or API versioning plan; piecemeal fixes are not scaling.

---

*Digest generated from GitHub data retrieved 2026-05-07 23:59 UTC. All links point to `github.com/openclaw/openclaw`.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — 2026-05-07

## 1. Ecosystem Overview

The personal AI assistant / agent open-source ecosystem is experiencing a period of intense development, with seven of thirteen tracked projects showing high daily activity (50+ issues or PRs). The landscape is fragmented by design philosophy: some projects pursue broad, all-in-one reference implementations (OpenClaw, CoPaw), while others target specific niches such as low-resource devices (NullClaw), multi-agent orchestration (PicoClaw, Hermes Agent), or enterprise-grade architecture (IronClaw). Recurring cross-project pain points include WebSocket instability, plugin API brittleness, and insufficient cost security controls. Despite these challenges, community engagement remains strong, with users actively submitting feature proposals—particularly for cross-platform desktop apps, memory persistence, and agent identity protocols.

## 2. Activity Comparison

| Project | Issues Updated (last 24h) | PRs Updated (last 24h) | Release in 24h | Health Score |
|---------|---------------------------|------------------------|----------------|--------------|
| OpenClaw | 500 | 500 | v2026.5.6 (hotfix) | 🔴 Critical regressions (WebSocket, WeChat, compaction) |
| NanoBot | 14 | 43 | None | 🟡 High severity CPU leak, WebSocket drops |
| Hermes Agent | 50 | 50 | None | 🟡 Multiple P2 bugs, MemOS memory leak |
| PicoClaw | 22 | 54 | Nightly build | 🟡 Critical history truncation, auth failures |
| NanoClaw | 3 | 25 | None | 🟢 Moderate bugs; stable overall |
| NullClaw | 1 | 2 | None | 🟠 Critical web_search impracticability |
| IronClaw | 34 | 50 | None | 🟠 Critical provider fallback destroys config |
| LobsterAI | 1 issue (critical) | 40 (29 merged) | None | 🟡 Critical login failure, but rapid fixes |
| TinyClaw | 0 | 0 | None | ⚪ Inactive |
| Moltis | 6 | 14 (12 merged) | None | 🟢 Good stability; one Docker sandbox bug |
| CoPaw | 50 | 45 | v1.1.5.post2 | 🟢 Healthy; WeChat message loss critical |
| ZeptoClaw | 0 | 0 | None | ⚪ Inactive |
| ZeroClaw | 50 | 50 | Attempted (blocked) | 🟠 CI blocker, critical Docker image missing |

**Health interpretation:** 🟢 stable, 🟡 concerning, 🟠 degraded, 🔴 crisis, ⚪ dormant.

## 3. OpenClaw’s Position

**Advantages:**
- **Largest community scale:** 500 issues/PRs daily—10× higher than the next busiest projects (Hermes, ZeroClaw at 50 each). This reflects the widest user base and plugin ecosystem.
- **Mature release cadence:** Hotfixes (v2026.5.6) are shipped within 24 hours of regression detection; the `doctor --fix` tool shows operational maturity.
- **Broadest feature surface:** Real-time voice with video frames, Telegram forums, WeChat, Feishu, WebSocket gateway—no other project matches channel breadth.

**Technical approach differences:**
- **OpenClaw** uses a monolithic _core reference_ model with extensive plugin API support. Others are more modular: **IronClaw** is rebuilding with a microservice “Reborn” architecture; **ZeroClaw** pursues “everything is a plugin”; **NanoBot** focuses on lightweight edge deployment.
- **Community size comparison:** OpenClaw’s top issue (#75, Linux/Windows apps) has 104 comments and 74 👍—far exceeding any single issue in other projects (Hermes #6323 has 25 👍). This signals a much larger active user base.

**Vulnerabilities:**
- **Stability erosion:** Gateway WebSocket loops (#78402), compaction storms (#78604), and WeChat plugin breakage (#78232) threaten the trust built by the hotfix speed.
- **Plugin API fragility:** The WeChat regression chain (5+ interlinked issues) shows the plugin contract lacks versioning or testing coverage—a risk that smaller projects can avoid by having fewer plugins.

## 4. Shared Technical Focus Areas

The following requirements emerge across multiple projects, indicating industry-wide needs:

| Focus Area | Projects Affected | Specific Needs |
|------------|-------------------|----------------|
| **WebSocket / Gateway stability** | OpenClaw, NanoBot, Hermes, IronClaw | Event-loop starvation, cascading disconnections, 1000/1005/1006 errors |
| **Plugin API versioning & compatibility** | OpenClaw, CoPaw, ZeroClaw | WeChat breakage, missing channel contracts, fragile `channelRuntime` |
| **Cost & security controls** | OpenClaw, NanoBot, Hermes, PicoClaw, CoPaw | Per-hour ceilings (#38248), tool approval pipeline (MCP), secret redaction (#21044), failover cost surprises |
| **Multi-agent delegation** | OpenClaw, Hermes, PicoClaw, IronClaw, Moltis | Subagent tool allowlist, `sessions_spawn`, delegate tool (#2531), agent identity/onboarding protocols |
| **Memory persistence & context management** | Hermes, PicoClaw, CoPaw, NullClaw | Holographic memory, MemOS process leaks, compaction frequency, context window overflow |
| **Cross-platform desktop apps** | OpenClaw, Hermes, ZeroClaw | Linux/Windows apps (#75), native Windows support (#2512), portability (#6501) |
| **Reasoning/thinking content handling** | OpenClaw, NanoBot, Hermes, IronClaw, CoPaw, LobsterAI | Gemini reasoning leak (#41494), DeepSeek `reasoning_content` (#3665), MiniMax token leak |
| **Provider authentication & configuration friction** | OpenClaw, NanoBot, PicoClaw, IronClaw, LobsterAI, ZeroClaw | Multiple credentials error, fallback destroys config, login failures, Bearer-token mismatches |

## 5. Differentiation Analysis

| Project | Core Focus | Target Users | Architectural Distinction |
|---------|------------|--------------|---------------------------|
| **OpenClaw** | Reference implementation, broadest channel/plugin support | General users, plugin developers, self-hosters | Monolithic core with plugin API; `doctor --fix` tooling |
| **NanoBot** | Lightweight, edge device agent (CPU/memory constrained) | Low-resource environments, hobbyists | MCP integration, streamable HTTP, focus on token conservation |
| **Hermes Agent** | Memory systems (holographic, MemOS), Discord-first, multi-agent | Power users, Discord communities, memory-centric workflows | Rich memory providers, `/fork` commands, ACP client |
| **PicoClaw** | Multi-agent delegation (delegate tool), low-code skills | Users wanting agent orchestrators, RPA-like workflows | `delegate` tool for subagent spawning, exec sandbox |
| **NanoClaw** | Setup UX, skill ecosystem, CI/CD for skills | Developers, tinkerers | Emphasis on setup flow escape routes, skill deprecation, GitHub integration |
| **NullClaw** | Ultra-low-resource devices (weak CPUs, cheap hardware) | Embedded systems, IoT | Minimal dependencies; web_search blocked by Brave API key requirement |
| **IronClaw** | Enterprise-grade Reborn architecture (microservices), Slack relay | Enterprise, multi-tenant deployments | Crate-based microservices, E2E test pipelines, cloud-native |
| **LobsterAI** | Chinese market, coding plan support, ChatGPT OAuth | Chinese-speaking users, developers using NetEase ecosystem | YoudaoNote integration, DeepSeek/Qwen provider fixes |
| **Moltis** | Cross-agent trust (Ed25519 TOFU), telephony, sandbox diversity | Advanced users, multiple-agent networks | Multi-backend sandbox (Firecracker, Daytona), auto-unseal vault |
| **CoPaw** | Web console GUI, long-conversation management, Chinese channels | Desktop users, WeChat power users | React-window virtualization, PlanNotebook support, CLI backup |
| **ZeroClaw** | Channel explosion (Twilio, Mastodon, Zulip, etc.), desktop capabilities | Power users wanting every communication platform | “Everything is a plugin” philosophy, typed-family provider split |

## 6. Community Momentum & Maturity

**Tier 1 – High volume, stable release cycles (mature)**
- **OpenClaw** – Largest community, frequent hotfixes, but accumulating regressions.
- **CoPaw** – Steady release (v1.1.5.post2), healthy repository, strong Chinese community.

**Tier 2 – Rapid iteration, critical bugs under active development**
- **Hermes Agent** – High feature velocity (11 PRs merged today); memory and WebSocket issues degrading reliability.
- **PicoClaw** – Landmark multi-agent delegation merged; but history truncation and auth bugs are urgent.
- **ZeroClaw** – CI blocker for v0.7.5, but community channel contributions are exploding; architectural work progressing.
- **LobsterAI** – Exceptional fix throughput (29 merges in 24h); critical login bug is a priority blip.
- **IronClaw** – Deep into Reborn architecture migration; nightly E2E infrastructure improving; provider config bug is severe.

**Tier 3 – Moderate activity, niche stability**
- **NanoBot** – High-quality merges (Ruff, streaming fixes) but critical CPU leak and WebSocket issues unresolved.
- **Moltis** – Good stability, most bugs resolved same-day; telephony and identity features in progress.
- **NanoClaw** – Steady improvement (6 merges), but small community; skill deprecation and setup UX focus.
- **NullClaw** – Very low activity; single critical bug defines the project’s viability for its niche.

**Tier 4 – Inactive**
- **TinyClaw**, **ZeptoClaw** – No activity in 24h; likely stalled or unmaintained.

## 7. Trend Signals

**Emerging industry trends from community feedback (value for AI agent developers):**

1. **Multi-agent trust & identity protocols are becoming essential.** Moltis (PR #979, Issue #973) and NanoBot (Issue #3639) both propose Ed25519-based onboarding. This foreshadows a standard similar to OIDC for agents—developers should plan for identity verification in their agent architectures.

2. **Cost governance is a top user pain point.** Across OpenClaw (#38248), Hermes (credential exhaustion fix), and CoPaw (no cost ceiling), users demand predictable budgets before bills arrive. Tool-level cost capping and per-provider quotas will be table stakes for production deployments.

3. **WebSocket reliability is the Achilles’ heel of real-time agents.** Four major projects (OpenClaw, NanoBot, Hermes, PicoClaw) report event-loop starvation, handshake failures, or connection loops. Developers must prioritize async task isolation and heartbeat resilience.

4. **Plugin API versioning is overdue.** The WeChat regression chain (OpenClaw, CoPaw, PicoClaw all hit) shows that binary compatibility across minor releases is broken. Adopting semantic versioning for plugin interfaces or gRPC-style contracts would prevent serial regressions.

5. **Memory consolidation is moving from “nice-to-have” to “must-have.”** Hermes (mempalace proposal), PicoClaw (context preservation fixes), and CoPaw (long-conversation handling) all point to production users needing persistent, deduplicated memory that survives restarts and compaction.

6. **Desktop apps for Linux/Windows are the most demanded cross-project feature.** OpenClaw (#75, 104 comments), Hermes (#2512), and ZeroClaw (#6501) all lack maintainer commitment. Any project that solves this first will capture a significant underserved user base.

7. **Reasoning/thinking content handling is a new compliance and UX requirement.** As models (DeepSeek, MiniMax, Gemini) increasingly expose chain-of-thought, agents must sanitize, filter, or expose it appropriately. This is still ad-hoc across projects.

8. **Open-source provider lock-in is real: Brave Search API dependency in NullClaw and costly fallback in OpenClaw show that default configurations can create hidden costs. Developers should design for provider-agnostic fallback with cost telemetry.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-07

## Today's Overview

The NanoBot project experienced high activity over the past 24 hours, with **14 issues updated** (5 open, 9 closed) and **43 pull requests updated** (24 open, 19 merged/closed). No new releases were published. The community submitted a substantial cross-agent identity proposal, multiple bug reports around WebSocket and streaming behavior, and several enhancement PRs targeting configuration, security, and channel support. The maintainer team merged 19 PRs, reflecting a healthy pace of code quality improvements, bug fixes, and feature polishing.

---

## Releases

*None in the last 24 hours.*

---

## Project Progress

The following **merged/closed PRs** advanced the project today:

- **#3672** – CI/CD: Enabled full Ruff F-rule checks and fixed related errors (improves code quality across the codebase).  
- **#3678** – Logging: Replaced remaining bare `logger.error` in `except` blocks with `logger.exception` to preserve stack traces.  
- **#3623** – Config: Added `toolHintMaxLength` to control truncation of tool command hints in channel messages.  
- **#3676 / #3675** – API: Removed HTTP compression from SSE streaming to restore real-time incremental delivery (two similar PRs, both merged).  
- **#3669** – Nightly: Fixed runtime context prompt scaffolding leaking into persisted chat history (upstream fix for nightly branch).  

These merges indicate ongoing focus on **developer tooling (Ruff, logging)**, **user-facing configuration**, and **streaming reliability**. The nightly regression fix for context scaffolding is particularly important for chat history integrity.

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#3639** – *Proposal: Identity + Onboarding protocols for cross-agent trust* (3 comments)  
   - Author proposes Ed25519-based identity and onboarding protocols for NanoBot agents on edge devices. This signals growing interest in **agent-to-agent trust and interoperability** as NanoBot scales.
   - https://github.com/HKUDS/nanobot/issues/3639

2. **#3682** – *WebSocket handshake failure bug* (2 comments)  
   - Reported error in `websockets/http11.py` with `opening handshake failed`. Multiple users likely affected.  
   - https://github.com/HKUDS/nanobot/issues/3682

3. **#3665** – *DeepSeek-V4-Flash reasoning_content error* (2 comments)  
   - Recurring error after a few queries, requiring “reasoning_content” to be passed back. Indicates API compatibility issue.  
   - https://github.com/HKUDS/nanobot/issues/3665

4. **#2132** – *Runtime context metadata merged into user messages* (2 comments)  
   - Long-standing issue on `main` branch, now resurrected as a nightly regression (#3670).  
   - https://github.com/HKUDS/nanobot/issues/2132

### Most Active PRs (by comment count, all shown as “undefined” but top entries have activity)

- **#1219** – Stock market analysis enhancement (large PR with docs/tests; open since Feb 26) – needs maintainer review.  
- **#3622** – Persist focus key to session metadata for auto-injection (proposed solution for #3292).  
- **#3655** – Display model reasoning content during streaming (adds `show_reasoning` config).  
- **#3671** – Nightly fix for runtime context ephemeral (alternative approach to #3669).

---

## Bugs & Stability

### High Severity

| Bug | Description | Fix PR? |
|-----|-------------|---------|
| **#3638** | **100% CPU leak via MCP `streamable_http_client` cancel-scope mismatch** – orphaned asyncio tasks, critical for embedded deployments. | No linked fix yet (labeled `good first issue`). |
| **#3674** | **WebSocket channel silently drops media** from inbound messages – `_dispatch_envelope` ignores `media` field. | **#3673** (open, same author) |
| **#3670** | **Runtime context prompt scaffolding leaks** into persisted/replayed chat history on `nightly` (regression). | **#3671** (open) and **#3669** (merged) |
| **#3665** | **DeepSeek-V4-Flash `reasoning_content` error** – breaks thinking mode after a few queries. | No PR yet. |
| **#3681** | **LLM timeout after 300s** – frequent timeouts reported on Windows with v0.1.5post3. | No PR. |
| **#3682 / #3683** | **WebSocket handshake failures** across platforms (Linux server / Windows / Mac browsers). | #3684 (open, fixes WeChat, not WebSocket) |

### Medium Severity

- **#3657** – Dream restore doesn’t roll back `.dream_cursor`, causing memory gaps.  
- **#3625** – WhatsApp channel sends each token as separate message with OpenAI Codex (supports_progress_deltas).  
- **#3604** – WhatsApp voice messages not downloaded.  

### Low Severity / Minor

- **#2132** – Runtime context metadata merge (known, now partially addressed by #3669).

**Overall stability assessment:** The project is experiencing several **critical regressions** around WebSocket handling, streaming, and MCP resource cleanup. The CPU leak (issue #3638) and the nightly context leak (#3670) are particularly concerning for production use. Fix PRs exist for some issues but remain open.

---

## Feature Requests & Roadmap Signals

Based on community submissions and open PRs, the following features are gaining traction and are likely candidates for the next minor release (v0.1.6):

| Feature | Issue/PR | Priority Signal |
|---------|----------|----------------|
| **Configurable bot name & icon** (vs. default “nanobot is thinking…”) | #3650 | Low effort, clear UX win |
| **Disable Dream functionality** via `enabled` flag | #3652 | High user demand (1 comment, no pushback) |
| **Show model reasoning/thinking content** in CLI/TUI | #3655 (PR) | Already implemented, awaiting merge |
| **Custom bwrap bind mounts** for sandbox (`sandboxBindsRo/Rw`) | #3642 (PR) | Power-user request for tool exec |
| **Bearer-token authentication** for API server | #3649 (PR) | Security fix, likely to be fast-tracked |
| **Agent identity & onboarding protocols** | #3639 | Proposal only; signals future architecture work |
| **Add ROKID SSE channel** (smart glasses support) | #3679 (PR) | New hardware channel, innovative |

Other notable PRs that may land soon:

- **#3685** – Persist `_last_summary` across restarts (conversation memory improvement).  
- **#3684** – Fix silent message drops in WeChat channel (bug fix with enhancement).  
- **#3622** – Focus key persistence (from #3292).  
- **#1219** – Stock market analysis skills (large PR, needs careful review).  
- **#1939** – Skip heartbeat before LLM call (token savings, open since March).

---

## User Feedback Summary

Real pain points expressed by community members:

- **WebSocket instability** – Multiple users across Linux/Windows/Mac report handshake failures and media drops (#3682, #3683, #3674). Chinese-language users are affected.
- **LLM timeout frustration** – “最近经常报这个错误” (frequent timeout errors) – user expects reliability (#3681).
- **Dream feature incomplete** – Restore does not reset cursor (#3657); some users want to disable it entirely (#3652).
- **DeepSeek integration broken** – Thinking mode fails after a few queries (#3665).
- **WhatsApp channel limitations** – Voice not working (#3604), token-level spam (#3625).
- **Customization desire** – Users want to configure bot name, icon, and disable built-in features (#3650, #3652).
- **Positive engagement** – Active community submitting high-quality proposals (#3639) and numerous fix PRs. Maintainer responsiveness visible through rapid merging of CI and logging improvements.

---

## Backlog Watch

The following issues and PRs have been open for an extended period or require maintainer attention:

| Item | Days Open | Notes |
|------|-----------|-------|
| **PR #1219** – Stock market analysis + 3 new skills | 70 days | Large PR (600+ lines) with docs; needs review |
| **PR #1939** – Skip heartbeat before LLM call | 56 days | Important for token conservation and ToS compliance |
| **PR #3622** – Persist focus key | 3 days | Tagged for issue #3292, awaiting merge conflicts? |
| **Issue #2132** – Runtime context merged into user messages | 51 days | Closed but original problem may persist on `main` |
| **Issue #3652** – Disable Dream | 1 day | Low-effort request, could be implemented quickly |
| **Issue #3639** – Identity + Onboarding protocol | 1 day | Needs architectural discussion; could shape v0.2.0 |

**Recommendation:** Prioritize review of PR #1939 (heartbeat skip) and issue #3638 (CPU leak) given their direct impact on cost and stability. The identity proposal (#3639) is a forward-looking design that deserves a formal discussion thread or RFC.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-07

## 1️⃣ Today's Overview

Activity remains very high, with 50 issues and 50 PRs updated in the last 24 hours. The community is actively filing bugs and feature requests, while maintainers are merging fixes across credential handling, gateway stability, and subagent delegation. No new release was published today, but the volume of merged PRs (11) suggests a patch release may be imminent. Notable ongoing challenges include Windows compatibility, memory consolidation, and cross-platform WebSocket reliability.

## 2️⃣ Releases

**None** published in the last 24 hours.

## 3️⃣ Project Progress

Eleven pull requests were merged or closed today. Key advances and fixes include:

- **Discord `/skill` 8000‑byte limit overflow & auxiliary client crash resilience** ([PR #10078](https://github.com/NousResearch/hermes-agent/pull/10078)) — fixes two critical gateway stability issues that caused slash‑command sync failure and gateway crashes after restart loops.
- **Subagent delegation hardening** ([PR #20993](https://github.com/NousResearch/hermes-agent/pull/20993) → merged) — adds `delegation.max_tokens` config and documentation to prevent truncated tool‑call output from cascading errors.
- **Truncated tool‑call retry guidance** ([PR #21093](https://github.com/NousResearch/hermes-agent/pull/21093)) — improves retry logic by injecting a narrow user hint on second attempt.
- **Z.AI endpoint recovery and `/costs` command improvements** ([PR #21124](https://github.com/NousResearch/hermes-agent/pull/21124)) — handles credential exhaustion and makes `/costs` the canonical usage command.
- **iLink WeChat rate‑limit fix** ([Issue #21011](https://github.com/NousResearch/hermes-agent/issues/21011) → closed) — added retry/backoff for WeChat send message rate limiting.
- **WSL2 web_extract private‑network false positive** ([Issue #20795](https://github.com/NousResearch/hermes-agent/issues/20795) → closed) — corrected URL safety detection when run under WSL2.

## 4️⃣ Community Hot Topics

The most active discussions (by comments and reactions) reveal strong interest in memory systems, multi‑agent orchestration, and native platform support.

| Issue/PR | Comments | 👍 | Summary |
|----------|----------|----|---------|
| [#6323](https://github.com/NousResearch/hermes-agent/issues/6323) *mempalace external memory* | 17 | 25 | Proposal to add a structured persistent memory module (`mempalace`) for long‑horizon tasks and cross‑session continuity. High community enthusiasm. |
| [#2512](https://github.com/NousResearch/hermes-agent/issues/2512) *Native Windows Support* | 7 | 6 | Long‑standing request (since March) for full Windows support without WSL dependency. Large scope feature. |
| [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) *Generalized ACP client for multi‑agent CLI orchestration* | 5 | 8 | Extend the existing Copilot‑specific ACP client to orchestrate any ACP‑compatible coding agent (Claude Code, etc.). |

**Underlying need:** Users are demanding more flexible memory persistence, genuine first‑class Windows support, and the ability to orchestrate multiple agents through Hermes. These three topics together indicate a shift toward production‑grade agent management.

## 5️⃣ Bugs & Stability

Today’s bug reports cover several regressions and stability issues. No new P1/bugs were filed, but a notable security‑focused fix PR was opened (P1 severity below). Summary table:

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|---------------|
| [#21044](https://github.com/NousResearch/hermes-agent/pull/21044) | **P1** | Redact secrets from assistant output (streamed deltas, reasoning callbacks, stored content) – security fix (PR, open) | Yes (identical PR) |
| [#18529](https://github.com/NousResearch/hermes-agent/issues/18529) | P2 | Session title leaks thinking tokens when using reasoning models (e.g. MiniMax‑M2.7) | No |
| [#18870](https://github.com/NousResearch/hermes-agent/issues/18870) | P2 | `/fork` only copies ~15 messages instead of full history | No |
| [#20143](https://github.com/NousResearch/hermes-agent/issues/20143) | P2 | WhatsApp self‑chat mode silently drops user’s own group messages | No |
| [#21058](https://github.com/NousResearch/hermes-agent/issues/21058) | P2 | `hermes doctor` Gemini healthcheck false positive (401 due to Bearer‑token mismatch) | No |
| [#21050](https://github.com/NousResearch/hermes-agent/issues/21050) | P2 | Auxiliary context‑length tracking fragmented across compression/web_extract paths | No |
| [#21026](https://github.com/NousResearch/hermes-agent/issues/21026) | P2 | Multi‑platform WebSockets share single event loop → cascading disconnections | No |
| [#20927](https://github.com/NousResearch/hermes-agent/issues/20927) | P2 | Windows file‑write path handling errors + tool call mechanism failure | Yes ([PR #21027](https://github.com/NousResearch/hermes-agent/pull/21027)) |
| [#20939](https://github.com/NousResearch/hermes-agent/issues/20939) | P3 | MemOS memory provider spawns new `bridge.cts` process on every turn (massive memory leak) | No |
| [#21102](https://github.com/NousResearch/hermes-agent/issues/21102) | P3 | Holographic memory `fact_store search` returns 0 results when query contains FTS5 operator characters (e.g. hyphens) | No |
| [#21032](https://github.com/NousResearch/hermes-agent/issues/21032) | P2 | Clarify tool broken in Telegram gateway mode — missing callback wiring | No |
| [#19195](https://github.com/NousResearch/hermes-agent/issues/19195) | P2 | Discord‑cached PNG‑as‑.webp causes HTTP 400 from Anthropic (wrong `media_type`) | No |
| [#19559](https://github.com/NousResearch/hermes-agent/issues/19559) | P3 | MCP client never retries connecting to HTTP servers after startup window | No |
| [#21074](https://github.com/NousResearch/hermes-agent/issues/21074) | P3 | Native Windows Terminal support (redundant with #2512) | No |

**Critical stability issues:** The WebSocket cascading disconnection bug (multi‑platform) and the MemOS process leak could cause severe resource exhaustion and unreliability in multi‑platform deployments. The GitHub‑related `media_type` mismatch persists despite previous fixes.

## 6️⃣ Feature Requests & Roadmap Signals

| Issue | Votes | Type | Likelihood for next version |
|-------|-------|------|----------------------------|
| [#6323](https://github.com/NousResearch/hermes-agent/issues/6323) *mempalace external memory* | 25 👍 | Feature | **High** — strong community signal, aligns with existing memory providers |
| [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) *Generalized ACP client* | 8 👍 | Feature | **Medium** — builds on existing Copilot ACP client, valuable for multi‑agent workflows |
| [#10771](https://github.com/NousResearch/hermes-agent/issues/10771) *Auto Dream memory consolidation* | 1 👍 | Feature | **Medium** — periodic dedup/optimization of memory files; complements mempalace |
| [#21074](https://github.com/NousResearch/hermes-agent/issues/21074) *Native Windows Terminal support* | 0 👍 (new) | Feature | **Low** — duplicates #2512, which has no sign of progress |
| [#20743](https://github.com/NousResearch/hermes-agent/pull/20743) *Pocket TTS provider* | 0 👍 (PR) | Feature | **Medium** — adds multilingual local TTS (Kyutai Labs); open for some time |

**Prediction:** The `mempalace` external memory feature will likely be prioritized due to its high engagement and strategic fit with the existing holographic memory and MemOS providers. The generalized ACP client could appear as a follow‑up to the Copilot‑specific client.

## 7️⃣ User Feedback Summary

Real pain points expressed today:

- **Windows users** continue to face broken file‑write paths, false private‑network detection in WSL2, and lack of native CLI/terminal support ([#20927](https://github.com/NousResearch/hermes-agent/issues/20927), [#21074](https://github.com/NousResearch/hermes-agent/issues/21074), [#21058](https://github.com/NousResearch/hermes-agent/issues/21058)).
- **Telegram users** report broken `clarify` tool and poor markdown table rendering on mobile ([#14160](https://github.com/NousResearch/hermes-agent/issues/14160), [#21032](https://github.com/NousResearch/hermes-agent/issues/21032) — both still open).
- **Memory users** experience silent failures: holographic memory returns zero results for queries with hyphens, and MemOS spawns a new Node.js process every turn, consuming 250MB+ per turn ([#21102](https://github.com/NousResearch/hermes-agent/issues/21102), [#20939](https://github.com/NousResearch/hermes-agent/issues/20939)).
- **Discord & Anthropic** users hit a regression where every image attachment is rejected with HTTP 400 after v0.12.0 ([#21049](https://github.com/NousResearch/hermes-agent/issues/21049)).
- **Satisfaction points:** The delegation subagent hardening and Z.AI endpoint recovery fixes address complaints about truncation and credential exhaustion. The Kanban dashboard improvements are well‑received but a new cron tab rendering bug was reported ([#21038](https://github.com/NousResearch/hermes-agent/issues/21038)).

## 8️⃣ Backlog Watch

These high‑signal issues/PRs have been open for an extended period without maintainer response or action:

| Issue | Age | Needed attention |
|-------|-----|------------------|
| [#2512](https://github.com/NousResearch/hermes-agent/issues/2512) *Native Windows Support* | Since 2026‑03‑22 (46 days) | Large‑scope feature request with 6 👍; no maintainer comment. |
| [#6323](https://github.com/NousResearch/hermes-agent/issues/6323) *mempalace external memory* | Since 2026‑04‑08 (29 days) | High community excitement (25 👍, 17 comments) but no official response or status. |
| [#5257](https://github.com/NousResearch/hermes-agent/issues/5257) *Generalized ACP client* | Since 2026‑04‑05 (32 days) | Clear proposal with 8 👍; no maintainer acknowledgment. |
| [#10771](https://github.com/NousResearch/hermes-agent/issues/10771) *Auto Dream memory consolidation* | Since 2026‑04‑16 (21 days) | Memory optimization request; no maintainer reply. |
| [#17962](https://github.com/NousResearch/hermes-agent/pull/17962) *reverse‑shell and two‑stage download‑execute detection* | Since 2026‑04‑30 (7 days) | Security PR adding three dangerous patterns to approval list; no review or merge comment. |

**Observations:** The community is investing significant effort in memory‑related features and Windows support, but maintainers have not yet acknowledged these proposals. The security PR #17962 adds important coverage but has not been reviewed. A maintainer response on at least #6323 and #2512 would help direct development effort.

---

*Generated from GitHub data as of 2026-05-07. Total issues updated in last 24h: 50 (42 open). Total PRs updated: 50 (39 open).*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Based on the GitHub data from PicoClaw (github.com/sipeed/picoclaw) for the last 24 hours, here is the project digest for 2026-05-07.

---

### PicoClaw Project Digest
**Date:** 2026-05-07
**Data Snapshot:** 24-hour activity

### 1. Today's Overview

PicoClaw is experiencing a period of high-intensity development and community engagement, with 22 issues updated and 54 pull requests updated in the last 24 hours. The core team appears focused on stabilizing the agent runtime, particularly around context management and multi-agent coordination, while the community is actively reporting bugs related to session history and provider authentication. A new nightly build (`v0.2.8-nightly.20260507`) was released, though it is marked as potentially unstable. The volume of activity signals a project in rapid iteration, with key discussions centered on improving reliability and user experience for complex, multi-turn workflows.

### 2. Releases

A new release is available:

- **[nightly: Nightly Build](https://github.com/sipeed/picoclaw/releases/tag/v0.2.8-nightly.20260507.788cda5c)**: An automated build tagged `v0.2.8-nightly.20260507.788cda5c`. It is explicitly noted as unstable and intended for testing.
    - **Full Changelog:** [Compare v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)

**Analysis:** No stable release was cut today. The single nightly release indicates active work on the `main` branch, but no features or fixes have been deemed stable enough for a version bump. Users encountering issues on the stable `v0.2.8` should refer to the changelog for potential fixes in this build.

### 3. Project Progress

In the last 24 hours, **11 PRs were merged or closed**, indicating significant progress on several fronts:

- **Agent Delegation (High Impact):** The **[delegate tool](https://github.com/sipeed/picoclaw/pull/2531)** (PR #2531) was merged. This is a landmark feature allowing agents to hand off tasks to other named agents synchronously, enabling sophisticated multi-agent workflows and task specialization.
- **Provider & Tooling Improvements:**
    - **[Web Search Provider Fallback](https://github.com/sipeed/picoclaw/pull/2629)** (PR #2629) was merged, centralizing search provider logic and allowing native-search-capable models to use their built-in search path.
    - **[OpenAI-Compatible Embeddings](https://github.com/sipeed/picoclaw/pull/2624)** (PR #2624) support was added, expanding compatibility with vLLM-style endpoints.
- **CI/CD Enhancements:**
    - A workflow improvement was merged to **[allow releasing from an existing tag](https://github.com/sipeed/picoclaw/pull/2610)** (PR #2610), giving maintainers more flexibility in the release process.

### 4. Community Hot Topics

The following issues are generating the most discussion and engagement:

- **[#293: Feature: Autonomous Browser Operations](https://github.com/sipeed/picoclaw/issue/293)** (8 👍, 7 comments): A high-priority roadmap feature that continues to draw significant interest. The community is keen on expanding PicoClaw's reach to the web, with discussions weighing native browser control versus MCP-based approaches. This is a clear signal for a major upcoming capability.
- **[#1042: [BUG] exec工具的guardCommand方法问题](https://github.com/sipeed/picoclaw/issue/1042)** (8 comments): A long-standing bug where the `exec` tool’s path guard incorrectly blocks legitimate commands like `curl wttr.in`. The discussion highlights a user pain point with an overly restrictive safety system. This has 2 👍 reactions, suggesting moderate frustration.
- **[#2548: [Error] Multiple authentication credentials received.](https://github.com/sipeed/picoclaw/issue/2548)** (6 comments): A recently closed issue that was actively discussed. It reflects common user confusion with the provider configuration model, specifically when using Gemini.

**Analysis:** The community is currently most vocal about two things: the desire for web automation and the friction caused by overly aggressive safety defaults or complex configuration.

### 5. Bugs & Stability

Several new bugs were reported today, with a notable theme around **session history and context loss**:

- **Critical:**
    - **[#2796](https://github.com/sipeed/picoclaw/issue/2796) & [#2795](https://github.com/sipeed/picoclaw/issue/2795)**: Two separate users reported that **conversation history is truncated to only show the last user message**. This is a critical data integrity and user experience bug. **Fix PR exists?** Potentially related PRs [#2794](https://github.com/sipeed/picoclaw/pull/2794) (context preservation) and [#2788](https://github.com/sipeed/picoclaw/pull/2788) (timestamps) are open but do not directly address this.
- **High:**
    - **[#2769: PicoClaw authentication fails with valid API keys (401 across providers)](https://github.com/sipeed/picoclaw/issue/2769)**: A severe bug where valid API keys for Groq, OpenRouter, and Nvidia all return 401 errors. This is likely a show-stopper for affected users. **No fix PR is currently linked.**
    - **[#2794: fix(agents): preserve origin context for async follow-ups](https://github.com/sipeed/picoclaw/pull/2794)**: This PR addresses an issue where async tool callbacks lose their original routing context, leading to messages being sent to the wrong channel. While a fix, it confirms a real, high-severity bug.
- **Medium:**
    - **[#2704: DingTalk SDK 的 panic 导致 getway 异常停止](https://github.com/sipeed/picoclaw/issue/2704)**: A panic in the DingTalk channel SDK causes the gateway to crash due to a race condition. This is a stability issue for DingTalk users.
    - **[#2787: Session messages lack individual timestamps](https://github.com/sipeed/picoclaw/issue/2787)**: A data model issue where all messages in a session show the same time. A **fix PR [exists](https://github.com/sipeed/picoclaw/pull/2788)** (#2788).

### 6. Feature Requests & Roadmap Signals

Several feature requests are trending, pointing towards the project's future direction:

- **[Multi-Agent Role Inheritance (#2775)](https://github.com/sipeed/picoclaw/issue/2775)**: Users want spawned sub-agents (e.g., Planner, Builder) to inherit their own specific roles, not the root agent's. The recently merged **delegate tool (#2531)** directly enables this use case, suggesting it will be a major focus for upcoming versions.
- **[Streamable HTTP for MCP Clients (#2782)](https://github.com/sipeed/picoclaw/issue/2782)**: A request to support the new MCP transport standard, indicating the project must adapt to external protocol evolution. This is likely to be addressed soon as it's a blocker for connecting to modern MCP servers.
- **[Model Provider Additions (#2671, #2706)](https://github.com/sipeed/picoclaw/issue/2671)**: Requests for `opencode` and fixes for `Deepseek v4` thinking model show a strong user desire to use a diverse and cutting-edge set of LLMs.
- **[Skill Configuration via .env (#2623)](https://github.com/sipeed/picoclaw/issue/2623)**: A request to pass environment variables to custom skills via `.env`, which would greatly improve the developer experience for building custom skills.

### 7. User Feedback Summary

User feedback from the last 24 hours reveals several clear pain points:

- **Pain: Loss of Conversation History (High Frequency):** Multiple users (#2796, #2795, #2310) are frustrated by the system only retaining the last 1-2 messages in a session. This destroys continuity and makes backtracking impossible. This appears to be a **consolidated and critical issue**.
- **Pain: Complex Configuration & Provider Issues:** Users are struggling with the configuration model. The authentication failure bug (#2769) and the "Multiple credentials" error (#2548) point to a configuration system that is not intuitive for all users.
- **Pain: Unexpected Behavior with Safety Systems:** The `exec` tool guard issue (#1042) demonstrates a legitimate user workflow being blocked by a buggy safety feature, leading to frustration.
- **Satisfaction (Potential):** The rapid closing of bugs like the i18n issue (#2367) and the merging of the `delegate` tool (#2531) suggests that the team is responsive to well-defined bugs and is making good on roadmap promises, which likely keeps core contributors engaged.

### 8. Backlog Watch

The following items, while possibly stale, represent unresolved, high-importance tasks or long-standing issues that require maintainer attention:

- **[#293: Feature: Autonomous Browser Operations](https://github.com/sipeed/picoclaw/issue/293)**: This high-priority roadmap item has 8 upvotes and no PR linked. Its progress is a key indicator of the project's future scope.
- **[#2158: feat(agent): Multi-agent discovery prompt](https://github.com/sipeed/picoclaw/pull/2158)**: This PR is over a month old and has no maintainer feedback. It proposes a method for agents to discover each other, which is a foundational capability for the multi-agent ecosystem. Its staleness is a concern.
- **[#2368: [BUG] Android app. Model is not configured for local models](https://github.com/sipeed/picoclaw/issue/2368)**: This bug, reported over a month ago, prevents local model usage on Android. Given the growth of edge AI, this could be a strategic blocker that needs prioritization.
- **[#2671 & #2706](https://github.com/sipeed/picoclaw/issue/2671)**: These requests for `opencode` and `Deepseek v4` support are two weeks old with no maintainer comment. As these are prominent providers, silence may signal a bottleneck in provider integration logic.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest — 2026-05-07

### 1. Today's Overview
The project saw **high activity** with 25 pull requests (19 open, 6 closed) and 3 issues (2 open, 1 closed) updated in the last 24 hours. No new releases were published, but the development pace indicates sustained community engagement around infrastructure migration, setup flow improvements, and new skill features. Two design-level issues surfaced around file management and skill deprecation, while six PRs were merged—covering observability, prompt corrections, and a critical SQLite dependency change.

### 2. Releases
None.

---

### 3. Project Progress (Merged/Closed PRs Today)
Six pull requests were closed/merged, advancing several areas:

- **Observability & Delivery Receipts** — [#2244](https://github.com/qwibitai/nanoclaw/pull/2244) (feat): Added Sentry integration, structured delivery-failure logging for Telegram, pairing deeplinks, and outbound media support.
- **Prompt Flow Fixes** — [#2308](https://github.com/qwibitai/nanoclaw/pull/2308) (fix): Tightened approval-card wording, removed a ghost tool reference (`baget_park_task` → `list_recent_batches`), and shrunk verbose error notes.
- **WhatsApp Self-Chat Filter** — [#2302](https://github.com/qwibitai/nanoclaw/pull/2302) (fix): Stopped dropping user-typed self-chat messages by using the existing sent-message cache instead of a blanket `fromMe` filter.
- **Slack Setup Card Tidy** — [#2297](https://github.com/qwibitai/nanoclaw/pull/2297) (fix): Moved the “Get started” link to the top and formatted OAuth scopes for readability.
- **Escape Routes in Setup** — [#2313](https://github.com/qwibitai/nanoclaw/pull/2313) (setup): Added back-to-channels exit at every step gate of the Teams setup, preventing operators from being trapped in multi-step flows.
- **SQLite CLI Dependency Fix** — [#2309](https://github.com/qwibitai/nanoclaw/pull/2309) (fix): Replaced external `sqlite3` CLI calls with an in-tree `better-sqlite3` wrapper, resolving the misleading error reported in issue [#2191](https://github.com/qwibitai/nanoclaw/issues/2191) (closed).

---

### 4. Community Hot Topics
The most active discussion items (by comment/reaction count, though data shows low totals) point to infrastructure and design tension:

- **Issue #2312** — [groups/global/CLAUDE.md unconditionally deleted on startup](https://github.com/qwibitai/nanoclaw/issues/2312): A contributor reports that a committed file produces a permanent dirty working tree on every restart. The one comment likely includes debate on whether to remove the file from the repo entirely.
- **Issue #2311** — [Deprecate `/claw` skill: incompatible with v2](https://github.com/qwibitai/nanoclaw/issues/2311): The `/claw` skill’s architecture (DB schema, transport, container model) assumes v1 and is fundamentally incompatible with v2. The community is pushing for a clean removal rather than patching.
- **PR #2301** (open, feat) — [Polling mode for GitHub integration](https://github.com/qwibitai/nanoclaw/pull/2301): This PR adds a no-port-required polling mode, secure OneCLI secret merge, and webhook security warnings. Its breadth suggests strong interest in non-webhook setups.

The underlying needs are **clean migration paths** (v1→v2), **reduced maintenance burden** (remove broken code), and **accessibility for operators behind NAT/firewall**.

---

### 5. Bugs & Stability
**High Severity**

- **Issue #2312** — *Permanent dirty working tree*: `groups/global/CLAUDE.md` is deleted on startup, breaking git-based deployments. No fix PR yet. If users pull the repo and restart, they get a perpetually dirty tree.
- **Issue #2311** — *Skill incompatibility*: `/claw` is broken under v2, but this is a deprecation request rather than a crash.

**Medium/Low Severity**

- **Issue #2191** — *Misleading error in migrate-v2.sh* (closed): SQLite3 CLI binary missing produced a confusing “registered_groups missing” message. Fixed by [#2309](https://github.com/qwibitai/nanoclaw/pull/2309) which replaced the CLI dependency entirely.
- **PR #2302** (merged) — *WhatsApp self-chat echo filter*: User-typed messages to self were being dropped. Now fixed.
- **PR #2310** (open, fix) — *Fallback on `invalid_blocks`*: Chat-SDK bridge currently crashes on invalid block payloads; this PR adds a raw-text fallback.
- **PR #2291** (open, fix) — *Container CA trust*: OneCLI gateway CA is not trusted inside agent containers, causing TLS failures. The fix mounts the CA, but is still open and awaiting review.

---

### 6. Feature Requests & Roadmap Signals
Several open PRs indicate user-requested capabilities with high likelihood of inclusion in the next release:

- **Semantic Memory Skill** — [#2318](https://github.com/qwibitai/nanoclaw/pull/2318): `/add-mnemon` – persistent knowledge graph for agents surviving restarts and context compaction.
- **Local Voice Transcription** — [#2317](https://github.com/qwibitai/nanoclaw/pull/2317): `/add-voice-transcription-free-whisper` with support for `openai-whisper` and `whisper.cpp`.
- **GitHub Polling Mode** — [#2301](https://github.com/qwibitai/nanoclaw/pull/2301): No-port-required integration via REST API polling every 30s, plus webhook security warnings.
- **Tool-Call Previews** — [#2211](https://github.com/qwibitai/nanoclaw/pull/2211): Live tool-visibility skill showing tool calls to users before execution.
- **yt-dlp MCP Server** — [#2306](https://github.com/qwibitai/nanoclaw/pull/2306): In-tree MCP server and installer for YouTube downloading capabilities.

Setup UX improvements dominate contributor interest: [#2315](https://github.com/qwibitai/nanoclaw/pull/2315) (remove E.164 jargon), [#2316](https://github.com/qwibitai/nanoclaw/pull/2316) (back affordance in “Other…” channel), [#2314](https://github.com/qwibitai/nanoclaw/pull/2314) (fix Photon URL), [#2305](https://github.com/qwibitai/nanoclaw/pull/2305) (Slack post-install gate), [#2304](https://github.com/qwibitai/nanoclaw/pull/2304) (plain-language Slack step 1).

---

### 7. User Feedback Summary
- **Pain Points**:
  - Dirty working tree after fresh clone (Issue #2312) – blocks git-based deployment workflows.
  - `/claw` skill dead in v2 (Issue #2311) – confusion for users still relying on it.
  - migrate-v2.sh error message misled operators (Issue #2191, now fixed) – caused wasted debugging time.
  - Setup flows lack escape routes (PRs #2313, #2316) – users stuck in multi-step wizards with Ctrl-C as only exit.
  - Slack post-install wall (PR #2305, #2304) – non-technical users faced jargon (“expose”, “webhook server”) without warning.
- **Positive Signals**: The community is actively contributing both feature skills and UX refinements, indicating satisfaction with the project’s roadmap and maintainer responsiveness.

---

### 8. Backlog Watch
Several important open items require maintainer attention:

- **[#2187](https://github.com/qwibitai/nanoclaw/pull/2187)** – *Fix platform-id namespacing for CLI* (open since May 2): Carve-out to prevent CLI bare platform IDs from being namespaced. Needs review; affects channel identity consistency.
- **[#2211](https://github.com/qwibitai/nanoclaw/pull/2211)** – *Tool-visibility skill* (open since May 3): A feature skill adding live tool-call previews, waiting for maintainer feedback.
- **[#2291](https://github.com/qwibitai/nanoclaw/pull/2291)** – *Container CA trust fix* (open since May 5): Critical for agents behind OneCLI gateway but still unreviewed. Could cause TLS errors for containerized agents.
- **[#2307](https://github.com/qwibitai/nanoclaw/pull/2307)** – *Switch to Debian trixie, upgrade deps, smaller image* (open since May 6): An infrastructure improvement that depends on upstream compatibility testing.
- **Issue #2312** – *CLAUDE.md deletion* (open, severe): No fix PR yet; maintainers should decide whether to remove the file from the repo or change the startup logic.

These items represent either regressions, missing reviews, or long-standing feature requests. Prioritising the bug fixes (#2312, #2291) and the platform-id fix (#2187) would improve project stability and contributor trust.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest — 2026-05-07

### 1. Today's Overview
Activity on the NullClaw repository was moderate today, with one open issue and two pull requests updated in the last 24 hours. A critical bug report regarding `web_search` impracticality on low-resource devices remains open and continues to gather community discussion. One pull request was merged, fixing tool schema and error handling in the OpenAI-compatible Responses API, while a large feature PR for a cron subagent is still under review. No new releases were published.

### 2. Releases
None.

### 3. Project Progress
- **PR #790 (merged/closed)** – `fix(providers): Responses API tool schema and null error handling`  
  Merged today. This fix corrects two bugs in the OpenAI-compatible Responses API code path: (1) the tool schema format previously used nested Chat Completions format, which was incompatible with the Responses API; (2) null error handling was improved.  
  [GitHub: PR #790](https://github.com/nullclaw/nullclaw/pull/790)

- **PR #783 (open, updated)** – `feat(cron): cron subagent, run history, JSON output, security hardening`  
  This feature PR continues to receive updates. It introduces a DB-backed cron scheduler with support for skill/agent/shell job types, timezone offsets, delivery routing, operator alerts, and JSON CLI output.  
  [GitHub: PR #783](https://github.com/nullclaw/nullclaw/pull/783)

### 4. Community Hot Topics
- **Issue #871 (open)** – `[bug] Critical: web_search is impractical on low-resource devices without direct DuckDuckGo support`  
  With 7 comments, this is the most actively discussed issue today. The reporter describes that the current `web_search` tool essentially requires a Brave Search API key, which is not feasible for NullClaw's target use case on weak, cheap devices. The community is discussing alternatives, including direct DuckDuckGo integration.  
  [GitHub: Issue #871](https://github.com/nullclaw/nullclaw/issues/871)

### 5. Bugs & Stability
- **Critical**: Issue #871 (described above) is the only new bug report today. It highlights a fundamental usability blocker for the intended low-resource deployment scenario. No fix PR has been linked yet.  
- **Fixed**: PR #790 addressed a related tool schema bug in the Responses API, which likely affected stability for users of that provider.

### 6. Feature Requests & Roadmap Signals
- Issue #871 implicitly requests direct DuckDuckGo support for `web_search`, or at least a lightweight alternative that does not require an API key. This could be a high-priority roadmap item given the “critical” severity.
- PR #783 (cron subagent) is a large feature under review and is likely to land in the next minor or major release, bringing scheduled task execution and operator alerts.
- Users may also expect a quick patch to address the web_search limitation, possibly via a DuckDuckGo provider or a fallback mechanism.

### 7. User Feedback Summary
The primary pain point voiced in community discussion (Issue #871) is the impracticality of using `web_search` on low-resource devices without a free, API-key‑free search backend. The reporter and commenters are dissatisfied with the current reliance on Brave Search API and express a strong preference for direct DuckDuckGo integration. This reflects a broader user need for minimal external dependencies to keep NullClaw viable on cheap hardware. No positive feedback was recorded today.

### 8. Backlog Watch
- **PR #783** (created April 7, last updated May 7) – The cron subagent feature has been open for a month without being merged. While it received updates today, maintainers may need to review and decide on blockers to avoid feature stagnation.  
  [GitHub: PR #783](https://github.com/nullclaw/nullclaw/pull/783)
- **Issue #871** (created April 25, no fix PR yet) – This critical bug has been open for nearly two weeks. Community engagement is high, but no maintainer response or fix PR has been attached. It warrants immediate attention to restore basic search functionality for low-resource users.  
  [GitHub: Issue #871](https://github.com/nullclaw/nullclaw/issues/871)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-07

## 1. Today’s Overview

IronClaw remains in a high‑activity development phase driven by the **Reborn architecture migration**. Over the past 24 hours, 34 issues were updated (24 open, 10 closed) and 50 pull requests saw activity (23 open, 27 merged/closed). The majority of activity continues to focus on defining and implementing Reborn service contracts, with multiple large contract‑slice PRs landing (e.g., conversation binding, session thread transcripts, credential sessions). A notable volume of bug fixes and operational improvements (CI timeout adjustments, nightly failure attribution) also landed. No new releases were cut today.

## 2. Releases

*No new releases in the last 24 hours.*

## 3. Project Progress

**Merged/closed PRs today (highlights):**

- [#3315](https://github.com/nearai/ironclaw/pull/3315) – **feat(reborn): add session thread transcript contract** – Defines `ironclaw_threads` crate with `SessionThreadService` DTOs, message kind/status enums, and in‑memory implementation.
- [#3332](https://github.com/nearai/ironclaw/pull/3332) – **test(e2e): address PR 3251 Gemini smoke feedback** – Fixes subprocess lifecycle in Reborn gateway smoke tests.
- [#3329](https://github.com/nearai/ironclaw/pull/3329) – **ci: extend nightly e2e timeout** – Increased job timeout from 30 to 90 minutes to prevent cancellation of v2‑engine shards.
- [#3318](https://github.com/nearai/ironclaw/pull/3318) – **ci: attribute nightly failures to PRs merged since last green** – Adds `@mention` of responsible authors in nightly alert issues.
- [#3313](https://github.com/nearai/ironclaw/pull/3313) – **fix(turns): make run wake notifications best effort** – Isolates notifier errors from durable submit/resume path; adds regression tests.
- [#3308](https://github.com/nearai/ironclaw/pull/3308) – **docs(reborn): add crate agent maps** – Introduces `AGENTS.md` files for all current Reborn crates.
- [#3306](https://github.com/nearai/ironclaw/pull/3306) – **feat: e2e effective runtime policy** – Adds 1,354 LOC of test coverage for runtime‑policy substrate (additive only).
- [#3212](https://github.com/nearai/ironclaw/pull/3212) – **Add Reborn event projection service** – Defines `ironclaw_event_projections` with `EventProjectionService`, replay‑derived contracts, and cursor/rebase metadata.

**Closed design issues:** Several Reborn planning issues closed, including #3093 (EventProjectionService), #3089 (SessionThreadService), #3198 (TurnCoordinator API shape), #3199 (TurnRunner execution model), #3195 (crate boundary), #3162 (durable event/audit store), and #3019 (PromptWriteSafetyPolicy hook). This indicates the design phase for core Reborn components is nearly complete.

## 4. Community Hot Topics

The most active discussions remain centered on the **Reborn cutover**:

- [#3013](https://github.com/nearai/ironclaw/issues/3013) (7 comments) – **Reborn cutover blocker: add kernel TurnCoordinator** – Debate on host‑layer turn admission and one‑active‑run enforcement.
- [#3031](https://github.com/nearai/ironclaw/issues/3031) (6 comments) – **[EPIC] Reborn product surface migration** – Tracks the full migration of user/operator behaviour onto Reborn services; remains the central roadmap epic.
- [#3198](https://github.com/nearai/ironclaw/issues/3198) (5 comments, closed) – **Define TurnCoordinator public API shape** – Finalised the adapter‑safe interface, serving as a blueprint for upcoming implementation.
- [#3093](https://github.com/nearai/ironclaw/issues/3093) (4 comments, closed) – **Add EventProjectionService** – Closed after PR #3212 landed, but the validation of durable‑event fanout continues.
- [#3204](https://github.com/nearai/ironclaw/issues/3204) (4 comments, open) – **Define transcript and thread storage boundary** – Remains a key open discussion on canonical storage contracts.

**Underlying need:** The community (core team and contributors) is deeply invested in getting the Reborn architecture ready for production cutover. The high comment counts reflect careful design review and the need to avoid regressions for existing users.

## 5. Bugs & Stability

**Critical bugs reported today (with impact):**

- [#3323](https://github.com/nearai/ironclaw/issues/3323) – **Nightly E2E failed** – Workflow cancelled due to 30‑minute job timeout. **Fix PR:** [#3329](https://github.com/nearai/ironclaw/pull/3329) (merged, increased timeout to 90 mins).
- [#3320](https://github.com/nearai/ironclaw/issues/3320) – **Telegram conversation stuck after Gmail auth failure** – User cannot recover even after `/clear`. No fix PR yet.
- [#3319](https://github.com/nearai/ironclaw/issues/3319) – **Gmail Authentication fails (400) when started from Telegram** – Blocks Telegram usage for Gmail‑based workflows. No fix PR yet.
- [#3229](https://github.com/nearai/ironclaw/issues/3229) – **LLM provider fallback persists to DB on startup, permanently destroying user's model/provider config** – Critical/severe: fresh v0.27.0 install causes permanent config loss. No fix PR yet.

**Moderate bugs:**

- [#3317](https://github.com/nearai/ironclaw/issues/3317) – **Telegram setup did not work with local IronClaw** – Setup flow fails; user provided screenshots. No fix PR.
- [#3132](https://github.com/nearai/ironclaw/issues/3132) – **Mission creation fails: cooldown_secs must be integer** – Root cause: LLMs send numeric strings as strings. **Fix PR:** [#3206](https://github.com/nearai/ironclaw/pull/3206) (open, awaiting review).

**Stability improvements:** The nightly E2E timeout fix (#3329) and the nightly failure attribution (#3318) are operational improvements to catch and diagnose regressions faster.

## 6. Feature Requests & Roadmap Signals

- [#3334](https://github.com/nearai/ironclaw/issues/3334) – **Multi‑workspace support: one IronClaw instance across multiple Slack workspaces** – A new feature request from contributor PierreLeGuen, building on the channel‑relay bridge. This is a clear next‑step after the multi‑tenant Slack relay (PR #3253) and will likely appear in the next minor version.
- [#3327](https://github.com/nearai/ironclaw/issues/3327) – **feat(llm): surface and persist LLM reasoning content** – User‑visible: show model “thinking” in UI and store reasoning details for replay. PR #3326 already implements the round‑trip for DeepSeek, Gemini, and OpenRouter. This is a high‑visibility feature likely targeting the next release.
- [#3300](https://github.com/nearai/ironclaw/issues/3300) – **Multi‑tenant Slack relay: follow‑up items** – Security (OAuth state parameter), UX (connection confirmation), and edge cases. Indicates the Slack relay is nearing production quality.

**Roadmap alignment:** The Reborn epic (#3031) remains the primary roadmap driver. The features above (multi‑workspace, reasoning display) are additive and do not conflict with the migration.

## 7. User Feedback Summary

**Pain points expressed:**

- **LLM provider fallback destroys config** (#3229) – A v0.27.0 fresh install permanently overwrites user’s model/provider settings on restart. User considers it “Critical” and has filed a detailed report with reproduction steps.
- **Gmail auth failure from Telegram** (#3319) and **conversation stuck** (#3320) – A user reports that after a Gmail auth 400 error, the entire Telegram conversation becomes unrecoverable. This is a blocking issue for Telegram users who rely on Gmail tools.
- **Telegram setup difficulties** (#3317) – Another user could not get the Telegram channel to work with their local instance, with unclear error messages.

**Positive signals:**

- The multi‑workspace Slack request (#3334) shows real‑world demand for scaling IronClaw across multiple Slack tenants.
- The reasoning display feature (#3327) is driven by user need to see LLM “thinking” in the UI, indicating that users are using sophisticated models (DeepSeek, Gemini) and want transparency.

## 8. Backlog Watch

Issues and PRs that have gone without maintainer response or remain open for extended periods:

- [#3229](https://github.com/nearai/ironclaw/issues/3229) – **LLM provider fallback persists to DB** (opened May 3, no fix PR, no maintainer comment). **Severity: Critical** – needs urgent triage.
- [#3206](https://github.com/nearai/ironclaw/pull/3206) – **fix(bridge): coerce numeric‑string guardrails** (opened May 2, still open) – Fix for #3132, awaiting review.
- [#3215](https://github.com/nearai/ironclaw/pull/3215) – **fix(gemini‑oauth): preserve thoughtSignature** (opened May 2, still open) – Fix for #3214, awaiting review.
- [#1378](https://github.com/nearai/ironclaw/pull/1378) – **feat(routing): per‑channel MCP and built‑in tool filtering** (opened March 18, still open) – Large feature that adds channel‑aware tool scoping; has not seen recent activity.
- [#1666](https://github.com/nearai/ironclaw/pull/1666) – **feat: wechat channel** (opened March 26, still open) – WASM channel for WeChat DM; requires maintainer review.

**Recommendation:** The team should prioritise addressing #3229 (data‑loss bug) and the two pending fix PRs #3206 and #3215, as they block users on Telegram and Gemini workflows. The long‑idle feature PRs (#1378, #1666) may need a decision to merge, iterate, or close.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest – 2026-05-07

**Project Health:** Very high activity with 40 pull requests updated in the last 24 hours (29 merged/closed, 11 open). A single critical user issue (#1903) warrants immediate attention. No new releases today.

---

## 1. Today's Overview
Development velocity is exceptionally strong. The team merged 29 PRs covering bug fixes, new features (ChatGPT OAuth, multiple coding plan integrations), and infrastructure improvements. The only open issue (#1903) reports a persistent login failure for paying members, which could severely impact user retention. The open PRs include a fix for default model persistence after restart (#1905) and a feature to give each Agent an independent working directory (#1904). Overall, the project is in an active refinement and release preparation phase.

## 2. Releases
None today.

## 3. Project Progress (Merged/Closed PRs Today)
29 PRs were merged/closed, spanning multiple areas:

**New Features**
- [PR #1830](https://github.com/netease-youdao/LobsterAI/pull/1830) – Added ChatGPT OAuth login support.
- [PR #1862](https://github.com/netease-youdao/LobsterAI/pull/1862) – Xiaomi Mimo model coding plan support.
- [PR #1859](https://github.com/netease-youdao/LobsterAI/pull/1859) – Baidu Qianfan coding plan support.
- [PR #1852](https://github.com/netease-youdao/LobsterAI/pull/1852) – Optimized Agent-related copywriting and UX.
- [PR #1882](https://github.com/netease-youdao/LobsterAI/pull/1882) – Upgraded YoudaoNote skill to v1.0.8.

**Critical Fixes**
- [PR #1900](https://github.com/netease-youdao/LobsterAI/pull/1900) – Hardened assistant segment persistence to prevent markdown table corruption in concurrent sessions.
- [PR #1891](https://github.com/netease-youdao/LobsterAI/pull/1891) – Fixed Windows EPERM when deleting skill directories.
- [PR #1888](https://github.com/netease-youdao/LobsterAI/pull/1888) – Fixed ClawHub install failures in packaged environments (ENOENT on `/.clawhub`).
- [PR #1818](https://github.com/netease-youdao/LobsterAI/pull/1818) – Fixed OpenAI models being inaccessible when a proxy is enabled.
- [PR #1819](https://github.com/netease-youdao/LobsterAI/pull/1819) – Fixed DeepSeek v4 requiring `reasoning_content` when tool calls are present.
- [PR #1847](https://github.com/netease-youdao/LobsterAI/pull/1847) – Fixed custom model suppliers using DeepSeek V4.
- [PR #1872](https://github.com/netease-youdao/LobsterAI/pull/1872) – Fixed gateway restart caused by plan model list updates.
- [PR #1870](https://github.com/netease-youdao/LobsterAI/pull/1870) – Fixed Qwen 3.6 Plus triggering gateway restart after answering.
- [PR #1871](https://github.com/netease-youdao/LobsterAI/pull/1871) – Fixed IM messages intermittently appearing first in task records.
- [PR #1886](https://github.com/netease-youdao/LobsterAI/pull/1886) – Fixed `/models` command display incompleteness after ChatGPT OAuth introduction.
- [PR #1889](https://github.com/netease-youdao/LobsterAI/pull/1889) – Added OpenClaw runtime patch for Qwen vision catalog fallback.

## 4. Community Hot Topics
**Issue #1903 – Member login failure**  
[Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903) (opened today, 0 comments) reports that paying users cannot log in and therefore cannot use paid models. The user attached a screenshot of the error. This is a high-severity blocker with zero community discussion yet — likely due to its recent creation. Underlying need: reliable authentication for subscription members.

No other issues or PRs had notable discussion. All PRs in the list show `Comments: undefined` (likely zero).

## 5. Bugs & Stability
**Critical (immediate user impact)**  
- **Login failure (#1903)** – Blocks all paid usage. No fix PR linked yet. Needs urgent triage.

**High (fixed today)**  
- Gateway restart triggered by model list changes (#1872, #1870).  
- Qwen 3.6 Plus answer-induced reboot (#1870).  
- Markdown table corruption in concurrent sessions (#1900).  
- IM message display order glitch (#1871).  
- /models command truncated after OAuth (#1886).  

**Medium (fixed today)**  
- Windows permission errors on skill directory deletion (#1891).  
- ClawHub ENOENT on `/.clawhub` in packaged builds (#1888).  
- DeepSeek v4 reasoning_content requirement conflict (#1819).  

The high volume of merged fixes suggests robust quality assurance.

## 6. Feature Requests & Roadmap Signals
- **ChatGPT OAuth login** (merged today) signals a push toward third-party identity integration.
- **Coding plan support** for Xiaomi Mimo and Baidu Qianfan indicates multi-model pipeline expansion.
- **Agent-independent working directory** ([PR #1904](https://github.com/netease-youdao/LobsterAI/pull/1904), open) is a major user-requested enhancement for workspace isolation.
- **Default model persistence fix** ([PR #1905](https://github.com/netease-youdao/LobsterAI/pull/1905), open) addresses a long-standing UX pain point.

Likely next release will bundle these open PRs along with the login fix.

## 7. User Feedback Summary
- **Pain point:** Member login is broken (#1903), preventing paid model access. User explicitly requests “improved login method”.
- **Satisfaction indicators:** 29 merged PRs show rapid response to community-reported bugs (Windows EPERM, proxy blocking, gateway crashes).
- **Usage context:** The user of #1903 is a paid subscriber trying to use NetEase’s own models, suggesting enterprise or heavy personal use.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified in today’s data. All items are recent. However, **Issue #1903** should be monitored closely — if it remains unassigned for more than 24 hours, it could escalate user frustration.

**PRs to watch:**  
- [#1905](https://github.com/netease-youdao/LobsterAI/pull/1905) (open, fix for default model) – critical for UX consistency.  
- [#1904](https://github.com/netease-youdao/LobsterAI/pull/1904) (open, per-agent working directory) – significant feature that may require more review.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest — 2026-05-07

**Data Window:** Issues and PRs updated in the last 24 hours.

---

### 1. Today’s Overview

The Moltis project saw high activity over the past day, with 6 issues and 14 PRs updated. Twelve of those PRs were merged or closed, indicating a strong pace of feature completion and bugfixing. The two remaining open PRs address long-awaited features—Ed25519 node identity (TOFU) and Twilio telephony integration—while two open issues highlight a critical Docker sandbox bug and a formal interoperability proposal. Overall, the project is in a healthy, fast-moving state with a clear focus on sandbox reliability, identity protocols, and documentation quality.

---

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Project Progress (Merged/Closed PRs)

Twelve pull requests were merged or closed, spanning several areas:

**Sandbox & Deployment**
- **#942** (`feat(sandbox): remote & multi-backend sandbox support`) – Adds support for Vercel, Daytona, and Firecracker backends, enabling sandboxed execution on cloud deployments where Docker-in-Docker is unavailable.
- **#971** (`fix(sandbox): serialize container startup`) – Fixes race conditions that caused Docker/Podman sandbox collisions during parallel tool execution (fixes #964).

**Provider Fixes**
- **#961** (`fix(providers): replay DeepSeek reasoning content`) – Preserves and replays `reasoning_content` for DeepSeek/OpenAI-compatible models, preventing errors in thinking mode (fixes #959).
- **#358** (`fix(providers): route Copilot enterprise tokens via proxy endpoint`) – Resolves HTTP 421 errors for enterprise GitHub Copilot accounts.
- **#957** (`fix(matrix): add debug logging for OIDC registration`) – Adds logging to diagnose `invalid_redirect_uri` failures and deduplicates redirect normalization.

**Authentication & Security**
- **#974** (`Auto-unseal vault from recovery key at startup`) – Allows unattended vault unsealing via environment variable or file at startup.
- **#970** (`fix(auth): respect X-Forwarded-Proto for cookie Secure attribute`) – Fixes login failures when Moltis runs behind a non-TLS proxy (fixes #968).

**Documentation**
- **#976** (`docs: add Agent Identity + Onboarding Protocols integration guide`) – Documents the proposed cross-server trust protocols using Ed25519 keypairs.
- **#962** (`Update local TTS provider docs`) – Updates Piper and Coqui TTS references to maintained forks and current download links (fixes #958).

**Dependency Updates**
- **#978** – wasmtime 36.0.7 → 36.0.8
- **#975** – openssl 0.10.78 → 0.10.79
- **#967** – gix 0.78.0 → 0.83.0

---

### 4. Community Hot Topics

- **[Issue #959 – DeepSeek thinking mode error](https://github.com/moltis-org/moltis/issues/959)**  
  *1 comment, 1 👍*  
  Closed and resolved via PR #961. Users reported that DeepSeek models require `reasoning_content` to be sent back in follow-up requests; the fix ensures this data is preserved and replayed.

- **[Issue #973 – Proposal: Onboarding + Identity protocols](https://github.com/moltis-org/moltis/issues/973)**  
  *0 comments, 0 reactions*  
  A thoughtful proposal for standardizing how Moltis agents discover, verify, and exchange capabilities with each other. Although new, it aligns closely with the PR #979 that implements Ed25519 node identity.

- **[Issue #977 – Browser sandbox fails in Docker](https://github.com/moltis-org/moltis/issues/977)**  
  *0 comments*  
  Currently the only open bug report. The user runs Moltis in a LXC container on Proxmox and encounters a persistent failure creating the browser sandbox directory. No maintainer response yet.

- **[PR #979 – Ed25519 challenge-response node identity (TOFU)](https://github.com/moltis-org/moltis/pull/979)**  
  Open, created today. Likely to be a hot topic given the community interest in interoperability expressed in #973.

---

### 5. Bugs & Stability

| Severity | Issue        | Description                                                                 | Fix Status                     |
|----------|--------------|-----------------------------------------------------------------------------|--------------------------------|
| **High** | [#977 (open)](https://github.com/moltis-org/moltis/issues/977) | Browser sandbox fails when Moltis runs inside a Docker container (Proxmox). | Unresolved; no fix PR yet.     |
| **Medium** | ~~#964~~  | Parallel tool execution causes Docker name sandbox collisions.               | Fixed by PR #971.              |
| **Medium** | ~~#959~~  | DeepSeek “reasoning_content must be passed back” error.                      | Fixed by PR #961.              |
| **Low**   | ~~#968~~  | Login failure when behind non-TLS proxy (cookie `Secure` attribute).         | Fixed by PR #970.              |
| **Low**   | ~~#958~~  | Documentation links to unmaintained TTS repos (Piper / Coqui).               | Fixed by PR #962.              |

Overall stability is good; the only critical remaining bug is #977 affecting Docker users, particularly those with LXC containers. The sandbox race condition and login issue were both resolved within a day of reporting.

---

### 6. Feature Requests & Roadmap Signals

- **Cross-agent interoperability** – Issue #973 proposes standard protocols for agent–agent discovery, identity verification, and capability exchange. This is reinforced by PR #979 which implements Ed25519 node identity with a TOFU model. Both are strong signals that the next release will include a foundation for multi-agent trust.

- **Telephony** – PR #920 (`feat(telephony): add phone call support via Twilio`) remains open and under active development. It introduces a pluggable provider architecture and a call state machine, likely to land soon.

- **Remote sandbox backends** – PR #942 (merged) paves the way for cloud deployments without Docker-in-Docker. Expect continued adoption on DigitalOcean, Fly.io, and Render.

- **Vault auto-unseal** – PR #974 (merged) allows unattended startup with recovery keys, a quality-of-life improvement for operators.

Given these signals, the next minor release will probably focus on **node identity and agent interoperability**, with telephony following shortly after.

---

### 7. User Feedback Summary

**Pain points reported:**
- Docker sandbox failures when Moltis runs inside a container (Proxmox) – user TLA020.
- DeepSeek models erroring out on reasoning content when using chat history – user krokozha.
- Login failure when accessing Moltis via plain HTTP behind a proxy – user BrandonStudio.
- Parallel tool calls causing sandbox name collisions – user faevourite.
- Outdated documentation for Piper and Coqui TTS providers – user Thndr.

**Satisfaction indicators:**
- All reported issues (except #977) were resolved within 24 hours of being filed.
- The community proposal for identity protocols (#973) received immediate follow-up in the form of PR #979, showing responsive maintainers.

**Use cases revealed:**
- Running Moltis on a LAN behind a non-TLS proxy (common for home lab setups).
- Deploying Moltis inside LXC containers on Proxmox.
- Using remote cloud platforms (DigitalOcean, Fly.io) where Docker-in-Docker is unavailable.
- Interconnecting multiple Moltis agents in a multi-user or multi-server environment.

---

### 8. Backlog Watch

- **[Issue #977 – Browser sandbox fails in Docker](https://github.com/moltis-org/moltis/issues/977)**  
  Open since 2026-05-06 with no comments from maintainers. This is the only unresolved bug affecting a non-trivial deployment scenario (Docker/LXC). Likely requires investigation into directory permissions or mount propagation.

- **[PR #920 – Telephony support via Twilio](https://github.com/moltis-org/moltis/pull/920)**  
  Open since 2026-04-29 (9 days). It is a large feature with multiple files; no recent review activity despite being updated today with the latest merge from main. May need additional review cycles.

- **[Issue #973 – Onboarding + Identity protocols proposal](https://github.com/moltis-org/moltis/issues/973)**  
  While PR #979 partially addresses it, the issue itself has received no comments. Maintainers should confirm alignment with the broader roadmap.

No other items appear to be languishing unaddressed.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-07

## Today’s Overview

Activity remains high, with **50 Issues** and **45 PRs** updated in the last 24 hours. **24 Issues were closed** and **26 PRs were merged or closed**, indicating steady progress on both bug fixing and feature development. The project released **v1.1.5.post2**, which brings asynchronous session title generation and documentation updates. Community engagement is lively, with long-standing discussions about built-in skills/MCPs (#280) continuing to attract comments. Several stability issues around streaming models and channel reliability have been resolved, but new bugs—particularly WeChat channel message loss (#4056) and deep‑seek reasoning parsing (#4051)—require attention. The overall health of the project appears **healthy**, with a healthy balance of new features, refactoring, and user‑reported bug fixes.

## Releases

**v1.1.5.post2** (released 2026-05-07)
- **Changes:**
  - Documentation updated to v1.1.5.
  - Async generation of session titles via LLM.
  - Fix for `message_processing` return value.
- **Breaking changes:** None reported.
- **Migration notes:** No special steps required.

## Project Progress

Over the last 24 hours, **26 PRs were merged or closed**. Key advancements include:

- **CLI backup commands** (PR [#4095](https://github.com/agentscope-ai/QwenPaw/pull/4095)) – new `qwenpaw backup` subcommands for managing backups without the console UI.
- **Console refactoring and UI improvements:**
  - Token usage page style/refactor (PR [#4094](https://github.com/agentscope-ai/QwenPaw/pull/4094)).
  - Language switching logic optimized and icon updated (PR [#4085](https://github.com/agentscope-ai/QwenPaw/pull/4085)).
  - Chat session list virtualized with `react-window` to improve scroll performance (PR [#3912](https://github.com/agentscope-ai/QwenPaw/pull/3912)).
  - Fixed duplicate rendering in console (PR [#4052](https://github.com/agentscope-ai/QwenPaw/pull/4052)).
  - Session list style fixes and Chinese input issues resolved (PRs [#3943](https://github.com/agentscope-ai/QwenPaw/pull/3943), [#3934](https://github.com/agentscope-ai/QwenPaw/pull/3934)).
- **WeChat legacy migration** – centralized data migration for the “weixin → wechat” rename (PR [#3605](https://github.com/agentscope-ai/QwenPaw/pull/3605)).
- **File preview fix** – removed redundant URL prefix stripping (PR [#4089](https://github.com/agentscope-ai/QwenPaw/pull/4089)), related to Issue [#4047](https://github.com/agentscope-ai/QwenPaw/issues/4047) (file link expiry).
- **Default agent name** – now respects user‑defined custom names (PR [#4073](https://github.com/agentscope-ai/QwenPaw/pull/4073), fixes [#3465](https://github.com/agentscope-ai/QwenPaw/issues/3465)).
- **Approval level proxy fix** – backend now supports partial updates for agent config (PR [#3896](https://github.com/agentscope-ai/QwenPaw/pull/3896)).

## Community Hot Topics

1. **[Discussion: Which Skills and MCPs Can Be Built‑in? (#280)](https://github.com/agentscope-ai/QwenPaw/issues/280)** – *27 comments, open since March 2.*  
   Users debate which skills/MCPs should ship by default to improve out‑of‑box experience. This is the most commented issue and signals demand for a curated built‑in set.

2. **[Long conversation can’t reply (#4059)](https://github.com/agentscope-ai/QwenPaw/issues/4059)** – *8 comments, closed.*  
   After many turns, AI stops responding completely; `/compact` did not help. The bug was closed, implying a fix was applied, but the underlying context‑window problem remains a common complaint.

3. **[Volcengine coding plan support (#3753)](https://github.com/agentscope-ai/QwenPaw/issues/3753)** – *8 comments, closed.*  
   User requested default support for Volcengine’s “coding plan” model. Closed, suggesting the feature was either added or deemed out of scope.

4. **[Page scrolling lag after 200+ turns (#3350)](https://github.com/agentscope-ai/QwenPaw/issues/3350)** – *7 comments, closed.*  
   The need for front‑end virtualisation was confirmed; PR [#3912](https://github.com/agentscope-ai/QwenPaw/pull/3912) directly addresses this. Users still ask for methodological guidance on long‑running coding sessions.

**Underlying needs:**  
- Better handling of extremely long conversations (context management, UI performance).  
- Improved out‑of‑box experience with pre‑installed skills.  
- First‑party support for popular Chinese cloud providers (Volcengine).

## Bugs & Stability

| Issue | Description | Severity | Status | Fix PR |
|-------|-------------|----------|--------|--------|
| [#4056](https://github.com/agentscope-ai/QwenPaw/issues/4056) | WeChat channel messages lost under normal network | **High** – complete loss of agent response for WeChat users | Open | None yet |
| [#4051](https://github.com/agentscope-ai/QwenPaw/issues/4051) | DeepSeek v4 Flash think content not parsed correctly | **Medium** – agent may not respond when think tags are malformed | Open | None yet |
| [#3988](https://github.com/agentscope-ai/QwenPaw/issues/3988) | Conda‑pack conflicts with `pip install qwenpaw[full]` on Windows | **Medium** – breaks Windows desktop packaging | Open | PR [#4093](https://github.com/agentscope-ai/QwenPaw/pull/4093) (*fix pending merge*) |
| [#4006](https://github.com/agentscope-ai/QwenPaw/issues/4006) | Reasoning content not filtered in OpenAI‑compatible provider (MiniMax) | **Medium** – leaks reasoning tokens to front-end | Open | None yet |
| [#4000](https://github.com/agentscope-ai/QwenPaw/issues/4000) | WeChat chat not synced with browser; missing voice input on web | **Low** – confusion but not data loss | Open | None yet |
| [#3997](https://github.com/agentscope-ai/QwenPaw/issues/3997) | MCP client timeout hard‑coded to 30s, no config option | **Medium** – blocks long‑running MCP tools | Open | None yet |

**Closed bugs today** include:
- Long conversation cannot reply ([#4059](https://github.com/agentscope-ai/QwenPaw/issues/4059))
- File link expiry ([#4047](https://github.com/agentscope-ai/QwenPaw/issues/4047)) – fixed by PR [#4089](https://github.com/agentscope-ai/QwenPaw/pull/4089)
- Streaming models cause ReAct loop ([#4034](https://github.com/agentscope-ai/QwenPaw/issues/4034))
- Console GUI performance after many sessions ([#3830](https://github.com/agentscope-ai/QwenPaw/issues/3830))

## Feature Requests & Roadmap Signals

**Open feature requests with community support:**
- **[Adding a model requires too many steps (#4036)](https://github.com/agentscope-ai/QwenPaw/issues/4036)** – 5 comments, labelled `good first issue`. Users want a streamlined model setup.
- **[Auto backup scheduling (#4086)](https://github.com/agentscope-ai/QwenPaw/issues/4086)** – 3 comments, request for cron‑like automatic backups.
- **[Enhance File module to support non‑markdown files (#4087)](https://github.com/agentscope-ai/QwenPaw/issues/4087)** – 2 comments, wants wider file preview.
- **[Web console upgrade capability (#2235)](https://github.com/agentscope-ai/QwenPaw/issues/2235)** – 2 comments, desire to update CoPaw remotely via web UI.
- **[WeChat–browser sync and web voice input (#4000)](https://github.com/agentscope-ai/QwenPaw/issues/4000)** – multi‑part request.
- **[MCP client timeout configurable (#3997)](https://github.com/agentscope-ai/QwenPaw/issues/3997)** – 2 comments.
- **[Built‑in skills/MCPs (#280)](https://github.com/agentscope-ai/QwenPaw/issues/280)** – still under discussion.

**Recently closed, likely candidates for next release:**
- **PlanNotebook support** – experimental PR [#3238](https://github.com/agentscope-ai/QwenPaw/pull/3238) is open and under review.
- **Skill batch enable/disable** – PR [#4091](https://github.com/agentscope-ai/QwenPaw/pull/4091) adds multi‑select status toggle.
- **CLI skill test** – PR [#3999](https://github.com/agentscope-ai/QwenPaw/pull/3999) (first‑timer, under review) adds `qwenpaw skills test`.
- **Workspace/storage separation** – Issue [#3967](https://github.com/agentscope-ai/QwenPaw/issues/3967) (closed) suggests splitting core config from user files; user demand is high.
- **Custom workspace path** – Issue [#4067](https://github.com/agentscope-ai/QwenPaw/issues/4067) (closed feature request) may already be in development.

## User Feedback Summary

- **Pain points:**
  - Long conversations eventually become unusable – agent stops responding, context window issues.
  - File attachment links expire after one day, making older chat content inaccessible.
  - Adding a new model provider requires many clicks and back‑and‑forth navigation.
  - Workspace directory mixes core agent files with user documents, leading to accidental deletions.
  - WeChat channel users experience message loss and need better sync with browser interface.
  - Missing web voice input and MCP timeout configuration.

- **Satisfaction signals:**
  - Recent UI performance improvements (virtualised session list, reduced re‑renders) address the “after 200 turns” lag.
  - New backup CLI and skill batch management are welcomed.
  - PlanNotebook experimental feature shows progress on complex task decomposition.
  - Users are actively requesting evaluation/benchmarking capabilities for production deployment (Issue [#4008](https://github.com/agentscope-ai/QwenPaw/issues/4008)).

- **Overall sentiment:** Mixed – appreciation for frequent updates and community responsiveness, but frustration with production‑readiness gaps (context handling, channel reliability, configuration UX).

## Backlog Watch

| Item | Age | Comments | Maintainer Attention |
|------|-----|----------|----------------------|
| [#280](https://github.com/agentscope-ai/QwenPaw/issues/280) – Built‑in skills/MCPs | 2+ months | 27 | **High** – needs roadmap decision |
| [#4036](https://github.com/agentscope-ai/QwenPaw/issues/4036) – Simplify model setup | 3 days | 5 | Medium – good first issue |
| [#4056](https://github.com/agentscope-ai/QwenPaw/issues/4056) – WeChat message loss | 1 day | 4 | **High** – critical for channel users |
| [#4051](https://github.com/agentscope-ai/QwenPaw/issues/4051) – DeepSeek think parsing | 1 day | 4 | Medium |
| [#3988](https://github.com/agentscope-ai/QwenPaw/issues/3988) – Conda‑pack conflict | 7 days | 3 | Medium – fix PR almost ready |
| [#4000](https://github.com/agentscope-ai/QwenPaw/issues/4000) – WeChat sync & voice | 5 days | 2 | Low – enhancement |
| [#3997](https://github.com/agentscope-ai/QwenPaw/issues/3997) – MCP timeout config | 5 days | 2 | Medium |
| [#2235](https://github.com/agentscope-ai/QwenPaw/issues/2235) – Web console upgrade | 1.5 months | 2 | Low – long‑term feature |
| [#4087](https://github.com/agentscope-ai/QwenPaw/issues/4087) – Enhance File module | 0 days | 2 | Low – nice‑to‑have |

The maintainers should prioritise the **WeChat message loss** bug and the **long conversation handling** topic, as these directly impact daily users. The built‑in skills discussion (#280) would benefit from a formal roadmap announcement to guide community expectations.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-07

## 1. Today’s Overview
The ZeroClaw project shows **high activity** with 50 issues and 50 pull requests updated in the last 24 hours. A significant release‑engineering push is underway: the v0.7.5 milestone is being finalized after a CI defect held the first attempt, and multiple foundational PRs (typed‑family provider split, gateway boot fix) were merged. The community is also contributing a wave of new channel integrations (Twilio SMS, Mastodon, Zulip, Rocket.Chat, and several SMS siblings) and desktop‑capability features, signalling a clear roadmap focus on **communication breadth** and **local agent control**. While no new releases were cut today, the project is clearly approaching a v0.7.5 tag.

## 2. Releases
**None.** The v0.7.5 release was attempted but blocked by a CI bug (missing `api-generated` module); a re‑attempt is queued (PR #6508).

## 3. Project Progress
Six pull requests were closed/merged today, moving key features and fixes forward:

- **feat(config,providers): typed‑family split for model + TTS providers** (#6403, closed) – Restructured provider configuration to a single canonical shape per family, laying groundwork for v0.8.0.
- **fix(gateway,channels): boot without configured model so /onboard stays reachable** (#6493, closed) – Gateway no longer panics on startup when no model is configured; logs a warning and serves an onboarding endpoint.
- **fix(install): picker prompts go to stderr** (#6496, closed) – The interactive feature picker in `install.sh` now correctly displays prompts instead of swallowing them.
- **fix(web): agent tool button height** (#6369, closed) – CSS fix to make agent tool buttons fill available space.
- **fix(docs): generate lang switcher before mdbook sync** (#6486, closed) – Corrected documentation build order.
- **chore: bump version to v0.7.5** (#6492, closed) – Version bump across all hardcoded references.

Additionally, a fix for the cron jobs table UX (#6505) was opened and is under review.

## 4. Community Hot Topics
The most active discussions are concentrated around long‑term design and release coordination:

- **[RFC] Multi‑agent UX flow — design** (#5890, 8 comments) – An accepted RFC proposing a full UX flow for multi‑agent scenarios. The discussion period concluded; a team vote approved the design. This is a **high‑impact, high‑priority** architectural decision.
- **[Feature] A better LOGO of ZeroClaw** (#4710, 10 comments, 2 👍) – A low‑priority enhancement request for a new logo. The thread shows community interest in visual identity, but it remains open without maintainer action.
- **Release v0.7.5 milestone tracking** (#5878, 8 comments) – The canonical scope‑definition issue for the v0.7.5 release. Contributors are actively coordinating the pipeline fixes and final checks.
- **New channel feature requests** by contributor `theonlyhennygod` – Multiple issues (Zulip #6437, Rocket.Chat #6435, Twilio SMS #6427, Mastodon #6423, etc.) each have 1–2 comments, indicating rapid proposal and initial review. The sheer volume (5+ new channels in one day) highlights strong community demand for diverse communication backends.

## 5. Bugs & Stability
Several bugs were reported today, with varying severity:

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| #6500 – “not found docker image zeroclawlabs/tool‑runner” | **S0 – data loss / security risk** | The Docker sandbox documentation references a non‑existent image. No container can start. | None yet |
| #6472 – “gateway can not use postgres” | **S2 – degraded behavior** | Runtime panic (`Cannot start a runtime from within a runtime`) when Postgres memory backend is configured. | None yet |
| #6474 – “invoking the LLM twice repeatedly” | Risk: medium | A user’s request triggers two identical LLM calls in the omlx provider. | None yet |
| #6504 – “Confusing cron jobs table UX” | **S2 – degraded behavior** | Missing column borders and misaligned headers make the cron table unusable. | #6505 (open) |
| #6413 – “WhatsApp Web reacts to own‑account outbound messages” | **S1 – workflow blocked** (closed) | The fix was merged prior to today; issue closed. | #6413 (closed) |
| #6418 – “Fallback Providers Fail to Inherit Credentials” | **S1 – workflow blocked** (closed) | Marked as duplicate; presumably fixed elsewhere. | – |

The docker‑image issue (#6500) is the most critical open bug, as it completely blocks sandboxed execution for Docker users.

## 6. Feature Requests & Roadmap Signals
The project is experiencing an **explosion of new channel integration requests**, all filed on 2026‑05‑06/07 by contributor `theonlyhennygod`. These include:

- **SMS siblings:** Twilio (#6429, merged), Vonage (#6494, open), Plivo (#6453), Sinch (#6452), Telnyx (#6451)
- **Chat platforms:** Zulip (#6437), Rocket.Chat (#6435), Mastodon (#6423), Lemmy (#6441), Twitch (#6443)
- **Desktop capabilities:** Persistent WebSocket connection (#6498), macOS UI control handlers (#6499), cross‑platform port (#6501)
- **Architecture:** “Everything is a plugin” long‑term vision (#6489)

The v0.7.5 release is imminent (waiting on CI fix #6502). The v0.8.0 integration branch (#6398) is already open, suggesting the typed‑family provider split (#6403) will land in the next minor version. The desktop features appear to target a post‑v0.7.7 release, with macOS‑only onboarding merged today (#6506) and early capability handlers (#6507) stacked on top.

**Likely next‑release items:** v0.7.5 will include the CI pipeline fix, the typed‑family provider groundwork, and the gateway boot fix. The new channels and desktop capabilities are more likely to ship in v0.8.0 or later.

## 7. User Feedback Summary
Although direct user satisfaction data is limited, the bug reports reveal several pain points:

- **Configuration friction:** Users struggle with provider fallback credential inheritance (#6418), missing sandbox Docker images (#6500), and Slack token handling (#6237, fixed in #6287). The latter’s fix (making `bot_token` optional) directly addresses a common misconfiguration.
- **Runtime instability:** The Postgres memory backend panic (#6472) and duplicate LLM calls (#6474) degrade the reliability of self‑hosted deployments. Both were reported within the last two days, indicating possible regression or insufficient testing of recent changes.
- **UX dissatisfaction:** The cron job table has lost its styling (#6504), making it confusing to use. The web UI’s version number is missing from the sidebar (#6367, open PR). These are low‑severity but visible to everyday operators.
- **Positive signals:** The rapid community contribution of multiple new channels (authored by a single user) suggests that the plugin/channel architecture is well‑received and invites external contributions.

## 8. Backlog Watch
Several important issues and PRs have remained open for weeks without maintainer decision:

- **PR #5797 – “add tls_ca_cert_path support for custom inference providers”** (from April 16, status `needs-author-action`) – This PR adds TLS certificate support for private/corporate inference endpoints. It is risk‑high and critical for enterprise adoption, but the author has not responded to review requests.
- **Issue #4710 – “A better LOGO of ZeroClaw”** (from March 25, 10 comments) – Despite community interest, no maintainer has closed or implemented this low‑priority enhancement. It may be waiting for a branding initiative.
- **PR #6287 – “fix(config/channels/slack): make bot_token optional”** (from May 2, still open) – Although the fix addresses a known bug (#6237), it has not been merged. It is a small, low‑risk change.
- **Issue #6273 – “Typed‑family split for model and TTS providers”** (from May 2) – The implementation PR (#6403) was merged today, so this tracking issue should be closed.
- **PR #6367 – “feat(gateway): expose version in /api/status”** (from May 4, open) – A straightforward, non‑controversial UI improvement that could have been merged quickly; still awaiting review.

The project maintains a healthy velocity, but the backlog of low‑risk, user‑visible fixes (Slack config, version display) suggests review bandwidth is focused on higher‑risk architectural changes.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*