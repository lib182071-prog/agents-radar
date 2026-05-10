# OpenClaw Ecosystem Digest 2026-05-10

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-10 07:48 UTC

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

# OpenClaw Project Digest — 2026-05-10

## Today’s Overview

Project OpenClaw shows extremely high activity with 500 issues and 500 pull requests updated in the last 24 hours, reflecting a vibrant community with both heavy bug triage and active feature development. A new beta release (`v2026.5.9-beta.1`) was published, adding chat command overrides and refreshing dependency pins. The open/active issue count sits at 299, with 201 closed, while PRs have 319 open and 181 merged/closed — indicating a strong merge cadence. Despite the volume, several regressions and high-priority bugs remain under discussion, particularly around container deployment, credential handling, and channel-specific breakages.

## Releases

### v2026.5.9‑beta.1
- **New chat commands**: `/think default` and `/fast default` allow users to clear session-level overrides and revert to configured/provider defaults ([#79385]).
- **Dependency refresh**: Workspace lockfile updated, including `@openai/codex` 0.130.0, `acpx` 0.7.0, and AWS SDK 3.1044.0.
- No explicitly documented breaking changes or migration notes in the release summary.

## Project Progress

In the last 24 hours, **181 pull requests** were merged or closed, and **201 issues** were resolved. Notable merged/closed PRs include:
- **#74932** *(auto-reply fallback clearing)* – Fixes stale heartbeat auto fallback overrides persisting across model defaults changes.
- **#80149** *(node wake nudge budgets)* – Exposes nudge budget state and adds infinite‑nudge mode via `OPENCLAW_NODE_WAKE_NUDGE_BUDGET=0`.
- **#79691** *(diagnostics‑otel content capture)* – Populates `inputMessages`/`outputMessages` on model‑call events for OTEL export.

Key fix PRs that remain open but indicate progress (many have `proof: supplied` or are tagged `size: XS`/`S`):
- **#79924** – Honors `suppressDefaultToolProgressMessages` regardless of verbose level.
- **#79961** – Prevents duplicate reasoning fields on OpenRouter DeepSeek models.
- **#79987** – Plugin install wizard skips reinstall when already installed version satisfies the request.
- **#80043** – Dispatches WhatsApp media messages individually to avoid image loss.

## Community Hot Topics

The most active issues (by comment count) reveal the community’s top concerns:

- **[#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** (104 comments, 74 👍) – Long‑standing request for desktop app builds beyond macOS/iOS/Android. **Need**: cross‑platform parity, especially for Linux power‑users.
- **[#14593 – Docker: `brew not installed`](https://github.com/openclaw/openclaw/issues/14593)** (29 comments, 17 👍) – Skill installation failing in official Docker image due to missing Homebrew. **Need**: consistent container onboarding without external package managers.
- **[#25592 – Text between tool calls leaks to channels](https://github.com/openclaw/openclaw/issues/25592)** (26 comments) – Internal agent narrative/error text being sent to Slack/iMessage. **Need**: strict separation of internal processing from user‑visible output.
- **[#9443 – Prebuilt Android APK](https://github.com/openclaw/openclaw/issues/9443)** (24 comments) – Request for official GitHub release builds for the Android companion app. **Need**: easier distribution for mobile users.
- **[#22676 – Signal daemon race condition](https://github.com/openclaw/openclaw/issues/22676)** (16 comments) – SIGUSR1 restart leads to orphaned processes and port conflicts. **Need**: clean process lifecycle management.
- **[#22438 – Tiered bootstrap file loading](https://github.com/openclaw/openclaw/issues/22438)** (16 comments) – Proposal to limit LLM token waste by tiered session‑scope context loading. **Need**: better context budget control for large workspaces.

PR activity is also high, though top PRs have no comment counts listed. The most technically involved ones (e.g., **#80167** post‑first‑message list stalls, **#80163** durable auto‑reply fix) show active maintainer participation.

## Bugs & Stability

Several regressions and crashes were reported in the last 24 hours. Ranked by severity:

| Issue | Severity | Description | Fix PR exists? |
|-------|----------|-------------|----------------|
| **#71127** – Stuck processing sessions never aborted | 🔴 High | Diagnostic subsystem detects stuck sessions but has no recovery action; gateway requires external restart. | Not yet (still open) |
| **#22676** – Signal daemon race condition on restart | 🔴 High | Orphaned processes and port lock failures under SIGUSR1. | Not yet (open) |
| **#77551** – Bedrock `ExpiredTokenException` after credential refresh (regression) | 🟠 Medium | Credential rotation no longer picked up without manual gateway restart. | Not yet (closed issue, regression reported) |
| **#31583** – `exec` tool does not inherit skill‑level env vars (regression) | 🟠 Medium | Environment variables from `skills.entries.*.env` missing in spawned subprocesses. | Not yet (open) |
| **#41494** – Gemini reasoning still leaks into chat (regression) | 🟠 Medium | Internal chain‑of‑thought shown to users on Telegram. | Not yet (closed issue, but root cause re‑opened) |
| **#79492** – Claude Opus 4‑7 returns empty response in agent runtime | 🟠 Medium | `infer model run` works but agent runtime fails silently. | Not yet (closed, likely fixed in release) |
| **#78232** – WeChat plugin 2.4.1 incompatible with 2026.5.4 | 🟡 Low | `channelRuntime` API changes break inbound message processing. | Not yet (closed issue, regression) |
| **#79408** – Telegram forum‑topic replies vanish when thread ID invalid | 🟡 Low | Replies disappear if Telegram rejects the topic. | Not yet (open) |
| **#67792** – OpenRouter model menu missing provider prefix | 🟢 Low | Display bug in Telegram model selection. | Not yet (closed) |

**Positive note**: The project has a healthy number of small fix PRs (XS/S) targeting these bug categories, and the release included no known critical regressions.

## Feature Requests & Roadmap Signals

The top feature requests, together with their traction, indicate the community’s priorities:

- **Cross‑platform desktop apps** (#75, Linux/Windows) – By far the most reacted issue (74 👍). Unlikely to ship in next beta (massive scope), but momentum suggests maintainers are aware.
- **Masked secrets** (#10659, 12 comments, 4 👍) – Prevents agents from reading raw API keys. Low complexity, high security value → **likely to appear in next minor release**.
- **Pre‑response enforcement hooks** (#13583, 10 comments, 2 👍) – Hard gates to require tool calls before final answer. Important for finance/security workflows → **could be considered for v2026.6**.
- **Direct Exec Mode for cron jobs** (#18160, 10 comments, 9 👍) – Avoid LLM overhead for simple commands. High urgency for automation users → **strong candidate**.
- **Slack Block Kit support** (#12602, 13 comments) – Richer agent messages. Moderate complexity; some work already done in plugins.
- **Session snapshots** (#13700, 6 comments) – Checkpoint/restore for long sessions. Not yet implemented but requested for development workflows.
- **Tiered bootstrap loading** (#22438, 16 comments) – Reduce token waste. Addresses a core cost concern → **medium likelihood** given current PR activity around context management.
- **Skill permission manifest** (#12219, 5 comments) – Security standard for skill installation. Could be accelerated by recent plugin‑security discussions.

The v2026.5.9‑beta.1 release focused on minor quality‑of‑life improvements rather than major features, suggesting the team is stabilizing for a larger release.

## User Feedback Summary

Prevalent pain points from recent issue comments and reactions:

1. **Container deployment friction**: Docker users cannot install brew‑based skills (#14593). Pushes users toward manual setup or alternative images.
2. **Channel‑specific UX failures**: Text between tool calls leaks (#25592), Gemini reasoning shown (#41494), Telegram forum‑topic replies lost (#79408). These degrade the user experience significantly and erode trust.
3. **Environment and credential handling**: Exec tool ignores skill env vars (#31583), AWS credential refresh broken (#77551), API keys exposed to agents (#10659). Users express frustration with “it worked before” regressions.
4. **Missing platform support**: Repeated calls for Linux desktop apps (#75), prebuilt Android APK (#9443), and Telegram Business Bot support (#20786). Users feel the macOS/iOS focus leaves out large segments.
5. **Memory setup omission**: Onboarding does not configure embeddings (#16670) – a key feature left undiscovered by new users.
6. **Session management gaps**: Stuck sessions (#71127), context token waste (#22438), and lack of session snapshots (#13700) indicate that large, long‑running agent workflows are still painful.

Satisfaction signals: The project has a high volume of new issues and PRs, the release cadence is steady, and many configuration/UX complaints have quick‑fix PRs already posted. This suggests a responsive maintainer team despite the bug load.

## Backlog Watch

Several important issues are open for months with high community engagement:

- **[#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)** – Created 2026‑01‑01, 104 comments, 74 👍. No maintainer response visible. **Needs: a public roadmap statement or milestone assignment**.
- **[#14593 – Docker `brew not installed`](https://github.com/openclaw/openclaw/issues/14593)** – Created 2026‑02‑12, 29 comments, 17 👍. Docker onboarding is a barrier for new adopters. **Needs: fix or decision to strip brew dependency**.
- **[#25592 – Text between tool calls leaks](https://github.com/openclaw/openclaw/issues/25592)** – Created 2026‑02‑24, 26 comments. Critical UX bug. **Needs: a confirmed fix PR** – no open fix yet despite high attention.
- **[#22676 – Signal daemon race condition](https://github.com/openclaw/openclaw/issues/22676)** – 16 comments, no maintainer activity after initial report. **Needs: triage and reproduction guidance**.
- **[#65824 – Feature request bundle](https://github.com/openclaw/openclaw/issues/65824)** – Closed as meta, but 15 comments indicate unresolved gaps. The closing note is not visible here – **worth auditing whether the 11 items were independently addressed**.

Maintainer attention is most urgently needed on **#14593** (Docker), **#25592** (text leaks), and **#22676** (Signal daemon), as they affect core usability and system stability.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-05-10 | **Analyst:** Senior AI Agent Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is experiencing a **rapid maturation phase**, characterized by high-velocity development across at least 12 actively maintained projects. The ecosystem is converging on a shared core architecture—multi-provider LLM backends, channel-based messaging adapters, tool-calling loops, and memory systems—while differentiating on orchestration models (single-agent vs. multi-agent), deployment targets (desktop, container, embedded), and security governance approaches. Community activity remains intense, with projects like OpenClaw processing 500+ issues and PRs daily, signaling both strong adoption and the growing complexity of production-grade agent systems. The emergence of **multi-agent runtimes** (ZeroClaw v0.8.0, OpenClaw's steering-chain, Hermes Agent's DAG orchestration) represents the next architectural frontier, moving beyond single-agent chat interfaces toward coordinated agent swarms. However, the ecosystem still grapples with cross-cutting challenges—credential management, container deployment friction, reasoning leak prevention, and platform-specific UX bugs—that remain unsolved across multiple projects.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status (24h) | Health Score | Activity Level |
|---------|----------------------|-------------------|---------------------|--------------|----------------|
| **OpenClaw** | 500 (299 open) | 500 (319 open) | ✅ v2026.5.9-beta.1 | High | **Extreme** |
| **ZeroClaw** | 22 (15 open) | 26 (14 open) | 🔜 v0.8.0 integration | High | **Very High** |
| **Hermes Agent** | 50 (39 open) | 50 (45 open) | No new release | Medium-High | **Very High** |
| **IronClaw** | 19 (18 open) | 33 (20 open) | No new release | High | **Very High** |
| **LobsterAI** | 0 new | 26 updated | ✅ v2026.5.9 | High | **High** |
| **CoPaw (QwenPaw)** | 29 (16 open) | 18 (10 open) | ✅ v1.1.6 + v1.1.6-beta.2 | High | **High** |
| **NanoClaw** | 3 open | 18 (7 open) | No new release | Medium-High | **High** |
| **PicoClaw** | 11 (8 open) | 23 (13 open) | ✅ nightly v0.2.8 | Medium | **High** |
| **NanoBot** | 5 (2 open) | 10 (5 open) | No new release | Medium | **Moderate** |
| **NullClaw** | 1 open | 3 (1 open) | No new release | Medium | **Moderate** |
| **Moltis** | 0 | 2 (1 open) | No new release | Medium | **Low** |
| **ZeptoClaw** | 0 | 1 open | No new release | Stable | **Minimal** |
| **TinyClaw** | 0 | 0 | No new release | Stable | **Inactive** |

**Key observations:**
- OpenClaw's extreme volume (1,000 combined issues/PRs) reflects its role as the ecosystem's core reference implementation, though maintainer bandwidth may be strained.
- ZeroClaw and IronClaw show the highest build-up to major architectural releases (multi-agent runtime and Reborn architecture respectively).
- LobsterAI and CoPaw demonstrate the most balanced release cadence with stable patch cycles.
- ZeptoClaw and TinyClaw show near-dormant development, potentially indicating maintenance-only mode.

---

## 3. OpenClaw's Position

### Advantages Over Peers
| Dimension | OpenClaw | Peer Average |
|-----------|----------|--------------|
| **Community Size** | ~4,000+ stargazers (est.) | ~1,500 stargazers (est.) |
| **Release Cadence** | Daily beta/nightly builds | Weekly to monthly |
| **Plugin Ecosystem** | Extensive MCP + channel plugins | Growing, but fragmented |
| **Multi-Platform Support** | macOS, iOS, Android, Docker | Varies by project |
| **Bug Fix Velocity** | 201 issues closed in 24h | 5-20 per day |
| **Provider Coverage** | 15+ LLM providers | 5-10 providers |

### Technical Approach Differences
- **Architecture:** OpenClaw uses a centralized gateway pattern with channel adapters, while ZeroClaw and IronClaw are pioneering modular multi-agent runtimes. OpenClaw's "steering-chain" is an overlay, not a native multi-agent substrate.
- **Memory System:** OpenClaw relies on a tiered bootstrap loading model (PR #22438), whereas NanoClaw and CoPaw are moving toward semantic memory graphs (e.g., `/add-mnemon` in NanoClaw #2318).
- **Security Model:** OpenClaw exposes secrets to agents by default (Issue #10659), while NullClaw and some ZeroClaw features are introducing whitelist/approval gating earlier in the design.
- **Deployment Focus:** OpenClaw prioritizes desktop/mobile experience; PicoClaw and NanoClaw target containerized/embedded deployments more aggressively.

### Community Size Comparison
OpenClaw's issue and PR volume exceeds the combined activity of the next 5 most active projects (ZeroClaw, Hermes, IronClaw, LobsterAI, CoPaw). This dominance is a double-edged sword: it indicates the largest user base and contributor pool, but also the highest bug surface and support burden. The top-voted issue (#75, Linux/Windows desktop apps) with 74 👍 and 104 comments demonstrates a clear community demand that OpenClaw has not yet addressed.

### Vulnerability
OpenClaw's regression rate is concerning: 9 reported regressions in the last 24 hours alone, including critical issues like credential refresh failures (#77551) and session stall recovery (#71127). The project's high merge velocity may be trading stability for throughput. Peers like IronClaw (with its Reborn architecture's durable resource governor) and ZeroClaw (with its SOP engine reload fix) are investing more heavily in state persistence and crash recovery.

---

## 4. Shared Technical Focus Areas

The following requirements have emerged independently across multiple projects, indicating ecosystem-level priorities:

| Focus Area | Affected Projects | Specific Needs |
|------------|------------------|----------------|
| **Container Deployment Friction** | OpenClaw (#14593), Hermes Agent | Brew-based skill installation fails in Docker; missing Homebrew in official images. Need consistent container onboarding. |
| **Reasoning/Thought Leakage** | OpenClaw (#41494), PicoClaw (#2745, Gemini & OpenRouter), Hermes Agent (#22949, Kimi K2.6) | Models' internal chain-of-thought or reasoning preamble appears in user-facing channels. **Critical UX bug.** |
| **Credential & Secret Management** | OpenClaw (#10659, #77551), Hermes Agent (Gemini tier detection #21399), NanoClaw (#1669, credential proxy ban risk), LobsterAI (#1606, hardcoded keys), ZeroClaw (#5833, session ownership) | Agents can read raw API keys; credential refresh broken; no masking; token leak risks. Strong demand for vault-backed secrets. |
| **Multi-Agent Orchestration** | ZeroClaw (v0.8.0), OpenClaw (steering-chain), Hermes Agent (DAG #12436), PicoClaw (#2158), NanoClaw (#2369) | Need for agent-to-agent delegation, workspace isolation, capability catalogs, and permission gating. |
| **Platform Support Gaps** | OpenClaw (#75, Linux/Windows apps), PicoClaw (#2421, email channel), Hermes Agent (#23052, Discord per-guild config) | Users want cross-platform desktop apps, email as a native channel, and channel-specific configuration. |
| **Tool & Scaffolding Reliability** | OpenClaw (#31583, exec tool env inheritance), PicoClaw (tool registry cloning #2793), Hermes Agent (#22696, tool_use parser), NanoClaw (#2369, delegation compliance) | Tools fail to inherit environment variables; tool registries don't clone correctly; parser fails on edge cases; delegation breaks at scale. |

These six areas represent the ecosystem's **shared pain points**. A coordinated effort (e.g., a shared library for container base images, or a standardized secret injection protocol) could accelerate all projects.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | Hermes Agent | NanoBot | PicoClaw | LobsterAI | CoPaw |
|-----------|----------|----------|--------------|---------|----------|-----------|-------|
| **Core Philosophy** | General-purpose agent platform | Autonomous agent runtime | Skill-learning agent | Research/experimental agent | Lightweight embedded agent | Enterprise multi-agent | Qwen-focued Chinese ecosystem agent |
| **Target User** | Enthusiasts, power users, devs | Enterprise, advanced devs | Devs, researchers | Researchers, hobbyists | Embedded/small-scale users | Enterprise teams | Chinese-speaking users, Qwen users |
| **Architecture** | Centralized gateway + channel adapters | Modular, multi-agent runtime w/ SOP engine | Agent with auto-skill creation | Functional state machine (refactored) | Lightweight with steering-chain | Multi-agent with artifact system, per-agent workdir | Monolithic with plugin system |
| **Key Differentiator** | Largest plugin ecosystem, most providers | Multi-agent runtime, durable governance (Reborn) | Automatic skill generation and learning | State machine refactor, Claude Code subscription | Small footprint, Telegram business, MCP config UI | Paginated loading, artifact system, multi-agent | Qwen/deepseek optimization, Windows/Chinese tools |
| **Security Maturity** | Early (exposed secrets, no masking) | Moderate (SOP engine, approval back-channel) | Moderate (skill evolution gate #21315, approval checks) | Early (no notable security features) | Early (PowerShell injection fix #2836) | Moderate (env variable secrets) | Early |
| **Deployment Model** | Desktop/mobile + Docker | CLI + daemon + web dashboard | CLI + TUI + Telegram/Discord | CLI + headless | Docker + embedded | Desktop app (packaged) | Desktop (Tauri 2.x PR), plugin-based |
| **Release Maturity** | Stable beta with daily regressions | Approaching v0.8.0 major release | Active PR-heavy, no recent full release | Moderate, steady bug fixes | Nightly builds | Stable patch releases | Stable patch releases |
| **Community Language** | English (global) | English (global) | English (global) | Chinese + English | Chinese + English | Chinese (primary) | Chinese (primary) |

### Strategic Implications
- **ZeroClaw** is best positioned to win the **enterprise multi-agent** segment if its v0.8.0 lands cleanly.
- **Hermes Agent** has the most innovative **skill-learning loop**, but its high regression rate and platform-specific bugs may erode trust.
- **LobsterAI** and **CoPaw** dominate the **Chinese-language market** and are investing heavily in multi-agent and artifact systems.
- **OpenClaw** remains the **broadest platform** but risks being outflanked on multi-agent and security if ZeroClaw and IronClaw execute.
- **PicoClaw** and **NanoClaw** are carving out **container-native/embedded niches** that OpenClaw does not serve well.

---

## 6. Community Momentum & Maturity

### Activity Tiers

| Tier | Projects | Characteristics |
|------|----------|-----------------|
| **Tier 1: Extreme Velocity** | OpenClaw | 500+ daily updates, daily releases, high regression rate, largest community |
| **Tier 2: Very High Velocity** | ZeroClaw, Hermes Agent, IronClaw | 20-50 daily updates, major architectural releases underway (v0.8.0, Reborn), strong maintainer responsiveness |
| **Tier 3: High Velocity** | LobsterAI, CoPaw, NanoClaw, PicoClaw | 10-30 daily updates, stable release cadence, active bug fixing, growing contributor bases |
| **Tier 4: Moderate Velocity** | NanoBot, NullClaw | 3-10 daily updates, focused improvements, smaller communities |
| **Tier 5: Low/Inactive** | Moltis, ZeptoClaw, TinyClaw | Minimal or no daily activity, maintenance-only mode |

### Maturity Assessment

| Project | Maturity Score | Reasoning |
|---------|---------------|-----------|
| **OpenClaw** | **7/10** | Large community, many releases, but high regression rate and unresolved long-standing issues (#75, #14593) |
| **ZeroClaw** | **6/10** | Rapidly maturing; v0.8.0 is a major step; high-severity bugs (Discord media, context compression) need resolution |
| **Hermes Agent** | **6/10** | Innovative auto-skill learning but 45 open PRs and P1 unbound-local-error suggest maintenance backlog |
| **IronClaw** | **8/10** | Reborn architecture shows rigorous design; strong CI; few user-facing regressions; lowest bug rate among high-activity projects |
| **LobsterAI** | **8/10** | Stable releases, timely bug fixes, clear versioning, enterprise-focused features |
| **CoPaw** | **7/10** | Good release cadence, responsive to Chinese users, but multi-agent and memory still early |
| **NanoBot** | **5/10** | Interesting refactoring but low community engagement; single core maintainer visible |
| **PicoClaw** | **5/10** | High development activity but nightly builds and reasoning leaks suggest instability |
| **NanoClaw** | **6/10** | Strong infrastructure features (DB config, per-group overrides) but credential risk (#1669) unaddressed |
| **NullClaw** | **4/10** | Small community; regression in 2026.5.x line breaks provider connectivity |
| **Moltis, ZeptoClaw, TinyClaw** | **3/10** | Minimal recent activity; not recommended for active deployment |

### Iteration vs. Stabilization
- **Rapidly Iterating:** OpenClaw, ZeroClaw, Hermes Agent, IronClaw — pushing new architectures and features aggressively.
- **Stabilizing:** LobsterAI, CoPaw — focusing on patch releases and UX polish after feature launches.
- **Consolidating:** NanoClaw, PicoClaw, NanoBot — balancing new features (Whisper, marketplace) with bug fixes.

---

## 7. Trend Signals

The following industry trends are extractable from cross-project community feedback and development priorities:

### 1. The Multi-Agent Shift
Every major project is investing in multi-agent orchestration. ZeroClaw's v0.8.0, OpenClaw's steering-chain, Hermes Agent's DAG (#12436), and NanoClaw's delegation compliance (#2369) all point to a market demand for **coordinated multi-agent workflows** beyond simple chat responses. **Signal strength:** Very High. **Verdict:** Multi-agent is the next major ecosystem inflection.

### 2. Demand for Persistent, Governed Memory
NanoClaw's `/add-mnemon` skill (#2318), CoPaw's pluggable memory manager (#2307), and Hermes Agent's agentmemory integration (#6715) indicate strong demand for **survivable, queryable knowledge graphs** that persist across sessions and survive context compaction. Users want agents that remember indefinitely. **Signal strength:** High. **Verdict:** Memory is becoming a core feature, not an add-on.

### 3. Credential Security Is a Growing Concern
Across OpenClaw (#10659), NanoClaw (#1669), LobsterAI (#1606), and ZeroClaw (#5833), users are raising alarm about **API key exposure, OAuth proxy risks, and credential refresh failures**. The lack of a standardized, ecosystem-wide secrets management approach is becoming a blocker for enterprise adoption. **Signal strength:** High. **Verdict:** Expect a security standardization effort in H2 2026.

### 4. Platform Inclusivity Pressure
The most-upvoted ecosystem issue is OpenClaw's lack of Linux/Windows desktop apps (#75, 74 👍). PicoClaw's email channel request (#2421) and Hermes Agent's Discord per-guild config (#23052) show that users want **first-class support for non-chat platforms** (email, desktop OS, enterprise messaging). **Signal strength:** Medium-High. **Verdict:** Platforms that expand beyond Telegram/Discord/macOS will capture underserved segments.

### 5. Reasoning Model Integration Problems
Multiple projects report **leaking internal reasoning** (OpenClaw #41494, PicoClaw #2745, Hermes Agent #22949) and **provider compatibility breaks** with reasoning-enabled models (ZeroClaw #3436, DeepSeek 400 error). As reasoning models (Claude Opus, Gemini 2.5 Pro, DeepSeek R1) become the default, the ecosystem must adapt. **Signal strength:** High. **Verdict:** This is a critical bug category that will affect all projects if not addressed.

### 6. Deployability Drives Adoption
The most successful projects (OpenClaw, CoPaw, LobsterAI) all offer **packaged desktop apps or nightly builds**. Conversely, projects with CLI-only or compile-from-source requirements (NullClaw, ZeptoClaw) show minimal community engagement. **Signal strength:** Confirmed. **Verdict:** Easy installation and updates are table stakes for ecosystem growth.

### 7. Tool Call Scaffolding Maturation
Issues like NanoClaw's delegation compliance breakage (#2369), OpenClaw's exec tool env inheritance (#31583), and PicoClaw's tool registry cloning (#2793) indicate that **tool-calling infrastructure is still brittle** when scaled to 30+ tools or multi-agent contexts. **Signal strength:** Medium. **Verdict:** Investment in robust tool scaffolding will pay dividends as agents grow more capable.

---

## Dashboard Summary for Decision-Makers

| Recommendation | Rationale |
|---------------|-----------|
| **Build on ZeroClaw or IronClaw for enterprise multi-agent** | Most mature architectural approach, durable state management, strong maintainer responsiveness |
| **Use OpenClaw for maximum provider coverage and plugin ecosystem** | Largest community, but prepare for regressions and container deployment workarounds |
| **Evaluate LobsterAI or CoPaw for Chinese-language deployments** | Best local model support, stable patches, active Chinese-speaking maintainers |
| **Avoid NullClaw, ZeptoClaw, TinyClaw for production** | Low activity, unresolved regressions, minimal community support |
| **Watch Hermes Agent for skill-learning innovation** | Most differentiated feature (auto-skill generation), but bug backlog may slow progress |
| **Contribute to credential security standardization** | The highest-impact contribution an individual could make to the ecosystem today |
| **Invest in multi-agent governance tools** | Every major project needs approval workflows, capability catalogs, and audit trails — an open opportunity |

---

*Report generated from GitHub digest data for period 2026-05-09 to 2026-05-10. All metrics are 24-hour snapshots unless otherwise noted.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-10

## 1. Today’s Overview
The NanoBot project saw moderate activity with **5 issues** (2 open, 3 closed) and **10 pull requests** (5 open, 5 merged/closed) updated in the last 24 hours. No new releases were tagged. The community contributed a significant refactor of the agent loop into a functional state machine, several bug fixes (including a dead-code elimination and a CLI retry spinner corruption), and a new feature enabling local Whisper transcription. Two open bugs—cron streaming missing `stream_id` and feishu topic isolation toggle—remain under active discussion. Overall project health is solid, with steady contributions from both maintainers and external developers.

## 2. Releases
*No new releases were published on this date.*

## 3. Project Progress (Merged/Closed PRs Today)
Five pull requests were merged or closed:

- **[#3715 – `refactor(loop): convert _process_message to functional state machine`](https://github.com/HKUDS/nanobot/pull/3715)**  
  Refactored the 300-line `_process_message` into an explicit state machine (`RESTORE → COMPACT → COMMAND → BUILD → RUN → SAVE → RESPOND`) with a `TurnState` enum. Improves readability and maintainability.

- **[#3719 – `fix(utils): remove unreachable dead code in find_legal_message_start`](https://github.com/HKUDS/nanobot/pull/3719)**  
  Fixed a logic error where an invalid list slice made a for loop unreachable (fixes issue #3716).

- **[#3705 – `fix(cli): handle retry-wait messages in interactive mode`](https://github.com/HKUDS/nanobot/pull/3705)**  
  Resolved terminal corruption caused by spinner interleaving with retry/progress messages during transient LLM errors.

- **[#1333 – `feat: add Claude Code subscription provider (OAuth)`](https://github.com/HKUDS/nanobot/pull/1333)**  
  Added an OAuth-based subscription provider for Claude Code, expanding the set of supported LLM backends.

- **[#3722 – `feat: added instant_memory bypass tool`](https://github.com/HKUDS/nanobot/pull/3722)**  
  Introduced a new tool that allows agents to bypass the long-term memory summarisation process when immediate response is needed.

## 4. Community Hot Topics

| Issue/PR | Comments | 👍 | Summary |
|----------|----------|----|---------|
| [#3724 – Enhancement: dynamic cognitive posture](https://github.com/HKUDS/nanobot/issues/3724) | 3 | 0 | A grateful user proposes making the agent’s system prompt, toolset, and knowledge base adaptive per-task instead of static, to avoid “repeater” behavior. |
| [#2709 – Error: streaming required for long operations](https://github.com/HKUDS/nanobot/issues/2709) | 2 | 0 | User hit a timeout error when using LLM calls exceeding 10 minutes; discussed a streaming-workaround. |
| [#3692 – Enhancement: feishu group topic isolation toggle](https://github.com/HKUDS/nanobot/issues/3692) | 1 | 1 | Requests an on/off switch for the new topic isolation in Feishu groups, as automatic isolation breaks multi-file workflows. |

**Underlying needs:** Users are pushing for greater agent flexibility (adaptive cognition), better control over group chat isolation, and robust handling of long-running LLM calls. The active discussion on #3692 (with a thumbs-up) suggests strong interest in a configuration toggle.

## 5. Bugs & Stability

| Bug | Severity | Status | Fix PR |
|-----|----------|--------|--------|
| [#3716 – Unreachable dead code in `find_legal_message_start`](https://github.com/HKUDS/nanobot/issues/3716) | Low (logic error, no runtime impact) | **Closed** | [#3719](https://github.com/HKUDS/nanobot/pull/3719) (merged) |
| [#3718 – Cron stream reminders missing `stream_id`](https://github.com/HKUDS/nanobot/issues/3718) | **High** (WS clients cannot associate streaming fragments) | **Open** | [#3720](https://github.com/HKUDS/nanobot/pull/3720) (open) |
| [#2709 – Long LLM calls fail without streaming](https://github.com/HKUDS/nanobot/issues/2709) | Medium (timeout for some long-running tasks) | Closed (likely resolved by other streaming improvements) | — |
| CLI spinner corruption in retry (PR #3705) | Medium (visual glitch) | Fixed | [#3705](https://github.com/HKUDS/nanobot/pull/3705) (merged) |

**Top priority:** The cron streaming bug (#3718) directly affects users relying on scheduled reminders via WebSocket. A fix is already in progress (#3720) and should be merged soon.

## 6. Feature Requests & Roadmap Signals

- **Dynamic agent cognition (#3724)** — The suggestion to make system prompts, tool sets, and knowledge bases adapt per task is a conceptual leap toward more autonomous agents. While no implementation is yet proposed, it aligns with ongoing re-architecture (e.g., #3715 state machine) and could influence a future plugin-based personality system.
- **Feishu topic isolation toggle (#3692)** — A small configuration knob that is likely to land in the next minor release given the clear user need and existing implementation.
- **Local Whisper transcription (#3723)** — A newly opened PR adds support for `faster-whisper` for on‑device voice transcription. If merged, this will be valuable for privacy‑conscious and offline users.
- **HookCenter typed-event hook system (#3564)** — This large PR (still open since April 30) proposes a robust plugin architecture for hooks. It is a significant infrastructure change and may require more review before inclusion.

*Prediction:* The next version (v0.1.6?) will likely include local Whisper, the feishu toggle, and the cron streaming fix. The HookCenter system may be deferred to v0.2.0.

## 7. User Feedback Summary

- **Positive appreciation:** User `wenge6090-cell` explicitly thanked the project and shared a companion project (Taiji), indicating a strong developer community around NanoBot.
- **Pain points:**
  - Streaming deficiencies: cron reminders not sending `stream_id` (#3718), and long LLM calls hitting streaming limits (#2709).
  - Feishu topic isolation is too aggressive; users want to opt out when processing multiple files (#3692).
  - Static agent behavior leads to perceived repetition (#3724).
- **Satisfaction drivers:** Active bug fixing (dead code, CLI spinner), refactoring for maintainability, and new features like local transcription and memory bypass tools show responsiveness to community needs.

## 8. Backlog Watch

| Item | Age | Importance | Notes |
|------|-----|------------|-------|
| [#3564 – HookCenter typed-event hook system](https://github.com/HKUDS/nanobot/pull/3564) | 10 days (open) | **High** — Core infrastructure | Large PR with plugin support. Needs maintainer review and possibly discussion on backwards compatibility. |
| [#3558 – Dynamic feishu reactEmoji via allowlist](https://github.com/HKUDS/nanobot/pull/3558) | 10 days (open) | Medium | Complementary to #3692; could be merged together. |
| [#3711 – Move archived summary into system prompt for KV cache stability](https://github.com/HKUDS/nanobot/pull/3711) | 1 day (open) | Medium — Performance | Fixes KV cache waste. Relatively small change, likely to be merged soon. |

All three open PRs affect core behaviour (hooks, caching, channel config). Maintainers should prioritise #3564 to unblock plugin development, while #3711 offers a quick performance win.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-10

## 1. Today's Overview

Hermes Agent is seeing an **extremely active** day with **50 issues and 50 pull requests** updated in the last 24 hours. While no new release was cut, the community and core contributors are engaged in heavy bug triage, with **11 issues closed** and **5 PRs merged/closed**. The majority of activity centers on platform-specific bugs (Telegram, Feishu, Discord), skill auto-creation quality, and infrastructure stability (Kanban, database locking, CI). A growing number of feature-oriented PRs — including DAG orchestration, unified skill triggers, and API server extensions — signal that the project is expanding its architectural capabilities alongside fixing regressions. The maintainers appear responsive, but several P1/P2 bugs remain open and may need faster resolution.

## 2. Releases

No new releases were published in the last 24 hours. The latest tagged version remains unknown from this data set.

## 3. Project Progress

### Merged / Closed PRs (5 total, top 2 shown)

- **#23057** refactor(agent): remove `skip_soul` context loading path → *Merged*  
  Cleans up dual SOUL.md injection routes, keeping identity loading exclusive to `load_soul_md()`. Tests and docs updated.

- **#22898** docs(skills): clarify Kanban fan-out decomposition → *Merged*  
  Improves skill documentation by teaching the `kanban-orchestrator` to split multi-lane requests into independent cards.

### Notable Closed Issues (bugs fixed)

- **#21503** – Kanban migration crashed on duplicate column; migration made idempotent  
- **#21374** – Race condition on gateway startup (duplicate column error) – fixed  
- **#21378** – `sqlite3.OperationalError: database is locked` on first Kanban tick – fixed  
- **#6051** – Skill auto-creation learned from transient failures (“learned helplessness”) – fixed  
- **#12812** – One-off troubleshooting actions saved as reusable skills – fixed  
- **#12081** – Fire-and-forget memory injection caused turn-lag – fixed (sync injection added)

These fixes address several stability and intelligence-quality concerns that had been accumulating over the past weeks.

## 4. Community Hot Topics

### Most Discussed / Reacted

| Issue | Title | Comments | 👍 | Status |
|-------|-------|----------|----|--------|
| [#5290](https://github.com/NousResearch/hermes-agent/issues/5290) | UnboundLocalError in gateway/run.py – missing `nonlocal message` | 4 | 3 | **P1 Open** |
| [#7022](https://github.com/NousResearch/hermes-agent/issues/7022) | Feishu Bug: Markdown source code displayed instead of rendered card | 4 | 0 | **P2 Open** |
| [#4538](https://github.com/NousResearch/hermes-agent/issues/4538) | Skill auto-named incorrectly – “company-research-summary” for crypto query | 3 | 0 | Closed |
| [#23052](https://github.com/NousResearch/hermes-agent/issues/23052) | Discord adapter: per-guild/per-server configuration | 2 | 0 | **Open** (new today) |
| [#6715](https://github.com/NousResearch/hermes-agent/issues/6715) | Integration: agentmemory as a memory provider plugin | 2 | 1 | **Open** |

**Analysis:**  
The P1 `UnboundLocalError` in the Telegram gateway is generating the most community concern (3 👍). It is a straightforward coding bug that prevents message delivery — likely to be prioritized next. The Feishu markdown rendering issue (#7022) reflects frustration from users on that platform. Meanwhile, the Discord per-guild config request (#23052) and agentmemory integration (#6715) show users are demanding more flexible, multi-environment configuration and advanced memory capabilities.

## 5. Bugs & Stability

**P1 (Critical)**
- **#5290** – `UnboundLocalError` in `gateway/run.py` – Telegram messages fail entirely.  
  *Fix PRs?* None yet open; needs a `nonlocal message` declaration.

**P2 (High Impact)**
- **#23024** – Ollama Cloud returns HTTP 400 “roles must alternate” when tools are used. Blocks all tool-using sessions.  
- **#22949** – Kimi K2.6 with `thinking: true` returns `content: null`; reasoning not displayed in Telegram.  
- **#22899** – Telegram message queuing delays agent response by 30–60 minutes → agent works on stale state.  
- **#22934** – Feishu adapter ignores `quote` field, breaking reply context.  
- **#22724** – MCP connectivity check resolves config key as DNS hostname instead of using configured URL.  
- **#22696** – `tool_use` parser fails when closing tag appears inside JSON strings.  
- **#22976** – TUI terminal resize accumulates blank separator lines.  
- **#22990** – `/model` picker uses hardcoded Copilot list, ignoring live catalog (newer/gated models invisible).  
- **#23065** – TTS overlapping audio when `auto_tts` enabled – no serial queue.  
- **#23052** (feature request but also config bug) – Discord `require_mention` is global only; per-guild needed.  
- **#21399** – Gemini setup reports API keys as paid without reliable tier signal.

**P3 (Minor)**
- **#22970** – RuntimeWarning on `/new`, `/clear`, `/undo`, `/reload-mcp` (coroutine never awaited) – cosmetic but annoying.
- **#22999** – Classic CLI resize clears startup banner/tool summary.
- **#22961** – Dashboard shows `vision_analyze` tool result as user message.
- **#22885** – Hindsight plugin warns wrong port (8080/8081) while service runs on 8888.

**Fix PRs in flight:**  
- #23070 (Signal group messages)  
- #23067 (oneshot stdout empty; cron WhatsApp delivery)  
- #23061 / #23063 (Telegram unsupported document types)  
- #23062 (skip_soul removal – already merged)  
- #22984 (CI acceptance lanes – open)

Several P2 bugs already have PRs submitted, indicating responsive maintainers.

## 6. Feature Requests & Roadmap Signals

### Notable Feature Issues (new or trending)

| Issue | Title | Priority | Likelihood for Next Release |
|-------|-------|----------|-----------------------------|
| [#23052](https://github.com/NousResearch/hermes-agent/issues/23052) | Discord per-guild configuration | P3 | High – simple config extension |
| [#21315](https://github.com/NousResearch/hermes-agent/issues/21315) | `skills.evolution_mode` – confirmation gate for skill auto-evolution | P3 | High – addresses shared/production deployments |
| [#6715](https://github.com/NousResearch/hermes-agent/issues/6715) | agentmemory integration as memory provider plugin | P3 | Medium – requires plugin architecture changes |
| [#12081](https://github.com/NousResearch/hermes-agent/issues/12081) | Synchronous memory context injection (now closed/merged) | – | Already shipped |
| [#17583](https://github.com/NousResearch/hermes-agent/issues/17583) | User-locked vs self-improving skill tiers + feedback-driven updates | P3 | Medium – complements #21315 |

### Featured PRs (likely to land soon)

- **#18255** – Cron token leak mitigation (max tokens cap, background review skip) – P2  
- **#12436** – DAG TaskGraph + delegate bridge + A2A bus (orchestration package) – major architecture addition  
- **#16530** – Unified skill trigger framework with Discord components – adds event-driven skill invocation  
- **#18510** – Telegram forum topics routed to Hermes profiles – per-topic persona support  
- **#23068** – Expose provider models in `/v1/models` and stream reasoning content – better frontend compatibility  
- **#23069** – Integrate CloakBrowser as stealth browser backend – adds 1,300 LOC of browser automation

**Predictions:**  
The next minor release will likely include the cron token fixes (#18255), Discord per-guild support (#23052-style), and possibly the skill evolution gate (#21315). The orchestration DAG (#12436) is a larger feature that may take another cycle.

## 7. User Feedback Summary

Common sentiments from issue comments:

- **Positive:** Users appreciate the automatic skill generation and learning system (“genuinely one of Hermes’s biggest strengths” – #6051).  
- **Pain points:**
  - *Platform inconsistency*: Feishu markdown not rendering, Telegram messages delayed, Discord mention rules global – users expect unified cross-platform behavior.
  - *Quality of auto-skills*: Multiple reports (#4538, #6051, #12812) that transient failures and one-off actions get persisted as skills, causing hallucinations and “learned helplessness”.
  - *Memory lag*: Asynchronous memory injection caused response delays (#12081) – now fixed.
  - *Configuration friction*: Copilot model list hardcoded, Gemini tier detection unreliable, NixOS file paths misconfigured.
  - *CLI/TUI ergonomics*: Resize issues, startup banner lost, Dashboard role mislabeling.
- **Use cases revealed:**  
  Users are running Hermes in production/shared environments (#21315), multi-agent setups, Telegram forum bots (#18510), and with small local models (2B–14B) on limited hardware (#22930).

Overall, community satisfaction seems high regarding core capabilities, but rigorous QA on edge cases and platform-specific polishing is needed.

## 8. Backlog Watch

### Issues needing maintainer attention (low comments but high impact / long open)

| Issue | Title | Open Since | Priority | Notes |
|-------|-------|------------|----------|-------|
| [#5290](https://github.com/NousResearch/hermes-agent/issues/5290) | UnboundLocalError in gateway/run.py | 2026-04-05 | **P1** | 4 comments, 3 👍 – no fix PR yet; blocks Telegram gateway |
| [#7022](https://github.com/NousResearch/hermes-agent/issues/7022) | Feishu markdown rendering | 2026-04-10 | **P2** | 4 comments – Feishu users affected for a month |
| [#22724](https://github.com/NousResearch/hermes-agent/issues/22724) | MCP connectivity resolves config key as DNS | 2026-05-09 | **P2** | 1 comment – MCP breakage |
| [#22696](https://github.com/NousResearch/hermes-agent/issues/22696) | `tool_use` parser fails on closing tag in JSON | 2026-05-09 | **P2** | 1 comment – affects Claude model tool calls |
| [#22899](https://github.com/NousResearch/hermes-agent/issues/22899) | Telegram message queuing delays | 2026-05-10 | **P2** | 1 comment – severe usability issue |
| [#21399](https://github.com/NousResearch/hermes-agent/issues/21399) | Gemini tier detection unreliable | 2026-05-07 | **P2** | 1 comment – misleads users about billing |
| [#22930](https://github.com/NousResearch/hermes-agent/issues/22930) | Running small offline models with insufficient compute (context window too small) | 2026-05-10 | **P3** | 1 comment – not a code bug but design feedback |

The **P1 UnboundLocalError** (#5290) is the most urgent backlog item. Several P2 bugs from May 9–10 also lack any maintainer response. The `Feishu markdown` issue (#7022) has been open for a full month — Feishu is an important platform for the Chinese user base, and a fix would reduce friction significantly.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-10

## 1. Today's Overview
The project shows strong, sustained activity with **11 issues** and **23 pull requests** updated in the last 24 hours. A new **nightly build (v0.2.8-nightly)** was published, reflecting ongoing development. The community is actively contributing to both feature work (steering-chain coordination, Telegram business mode, MCP configuration UI) and critical bug fixes (reasoning leaks, OAuth token refresh, PowerShell injection). Maintainers are responsive, merging 10 PRs today and closing 3 issues. Overall project health is good, with a clear focus on multi-agent orchestration, provider compatibility, and UX polish.

## 2. Releases
- **nightly (v0.2.8-nightly.20260510.6e6293e5)**: Automated build that may be unstable. Full changelog available at [v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main). No breaking changes or migration notes reported.

## 3. Project Progress
Today **10 PRs were merged/closed**. Notable advances:

- **Steering-chain final reply synthesis** ([#2842](https://github.com/sipeed/picoclaw/pull/2842)): Introduces an optional mode that builds terminal replies from a log of user-facing outcomes, addressing a major UX gap.
- **Multi-agent discovery prompt** ([#2158](https://github.com/sipeed/picoclaw/pull/2158) merged): Injects a lightweight agent registry into system prompts for Layer 1 multi-agent awareness.
- **Tool registry cloning fix** ([#2793](https://github.com/sipeed/picoclaw/pull/2793)): Corrects deferred tool discovery inside cloned registries used in subagent turns.
- **Spawn tool routing** ([#2790](https://github.com/sipeed/picoclaw/pull/2790)): Passes `agent_id` through to sub-turn execution, enabling targeted agent spawning.
- **xAI provider support** ([#2260](https://github.com/sipeed/picoclaw/pull/2260)): Adds xAI compatibility through the existing OpenAI-compatible path.
- **Google Antigravity OAuth scope fix** ([#2163](https://github.com/sipeed/picoclaw/pull/2163)): Preserves required OAuth scopes during token refresh to prevent PERMISSION_DENIED errors.
- **Web UI datetime display** ([#2630](https://github.com/sipeed/picoclaw/pull/2630)): Assistant replies now show full `YYYY-MM-DD HH:mm` timestamps.

Additionally, issues **#2665** (wrong Anthropic model IDs) and **#1347** (GitHub device authentication) were closed.

## 4. Community Hot Topics
- **[Feature] Email as native channel** ([#2421](https://github.com/sipeed/picoclaw/issues/2421), 5 comments, 1 👍): Users want email support for corporate/scientific environments where chat platforms are restricted. This is the most commented issue.
- **[Feature] OAuth 2.1 + PKCE for MCP servers** ([#2546](https://github.com/sipeed/picoclaw/issues/2546), 4 comments): Non-technical users need a dashboard-based “Add connector” UX for OAuth-protected MCP servers, similar to Claude.ai. Underlying need: lowering the barrier for enterprise MCP adoption.
- **[Bug] Codex OAuth empty assistant response** ([#2674](https://github.com/sipeed/picoclaw/issues/2674), 2 comments, 3 👍): High user interest (3 upvotes) in a streaming issue where ChatGPT backend returns empty responses. The root cause appears to be a misfire in the `response.output_item.done` event handling.
- **Steering-chain final reply UX** (multiple interlinked issues/PRs: [#2839](https://github.com/sipeed/picoclaw/issues/2839), [#2841](https://github.com/sipeed/picoclaw/issues/2841), [#2843](https://github.com/sipeed/picoclaw/issues/2843), [#2840](https://github.com/sipeed/picoclaw/pull/2840), [#2842](https://github.com/sipeed/picoclaw/pull/2842), [#2844](https://github.com/sipeed/picoclaw/pull/2844)): A cluster of 6 items around improving how PicoClaw renders final replies after multi-turn steering. Users report that the last reply often over-focuses on the recent follow-up and edits placeholder messages instead of sending new ones. This is a hot area of development.

## 5. Bugs & Stability
| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **High** | **OpenRouter reasoning model leaks thinking into assistant content** ([#2745](https://github.com/sipeed/picoclaw/issues/2745)) – Model's reasoning preamble appears in final output. | Open, stale | None yet |
| **High** | **Codex OAuth returns empty assistant response** ([#2674](https://github.com/sipeed/picoclaw/issues/2674)) – ChatGPT backend streaming mishandles `response.output_item.done`. | Open | None yet |
| **Medium** | **Steering-chain final reply edits placeholder messages instead of sending new ones** ([#2839](https://github.com/sipeed/picoclaw/issues/2839)) | Open | [#2840](https://github.com/sipeed/picoclaw/pull/2840) fix exists |
| **Medium** | **PowerShell encoding bypass via IEX injection** ([#2836](https://github.com/sipeed/picoclaw/pull/2836)) – Security fix in PR. | PR open | The PR itself is the fix |
| **Low** | **Hidden tools promoted in wrong registry** (already fixed in [#2793](https://github.com/sipeed/picoclaw/pull/2793)) | Merged | – |

The reasoning leak and empty Codex response are the most impactful open bugs. Both lack a fix PR.

## 6. Feature Requests & Roadmap Signals
- **Email channel** ([#2421](https://github.com/sipeed/picoclaw/issues/2421)): Strong candidate for next minor release if development resources permit.
- **OAuth MCP dashboard** ([#2546](https://github.com/sipeed/picoclaw/issues/2546)): High demand from enterprise users; may appear after the ongoing MCP config UI work ([#2770](https://github.com/sipeed/picoclaw/pull/2770)).
- **Steering-chain final reply synthesis** ([#2841](https://github.com/sipeed/picoclaw/issues/2841), [#2843](https://github.com/sipeed/picoclaw/issues/2843)): Already in active development – likely to land in the next nightly or v0.2.9.
- **Tool policy filters in AGENT.md frontmatter** ([#2837](https://github.com/sipeed/picoclaw/issues/2837)): A key enabler for multi-agent governance, with a matching PR ([#2838](https://github.com/sipeed/picoclaw/pull/2838)) open. Expect it in the next release.
- **Update from source tutorial** ([#2834](https://github.com/sipeed/picoclaw/issues/2834)): User requests clearer upgrade docs – may be resolved by a documentation update.
- **Session per-message timestamps** ([#2788](https://github.com/sipeed/picoclaw/pull/2788)): PR open, likely to be merged soon for frontend accuracy.
- **Telegram business mode** ([#2845](https://github.com/sipeed/picoclaw/pull/2845)): New PR adding support for Telegram Business accounts.

## 7. User Feedback Summary
Users express both satisfaction with PicoClaw’s flexibility and pain points in specific areas:
- **Pain points**: OAuth flow for MCP servers is too technical; reasoning models leak internal thoughts; steering-heavy turns produce confusing final messages; no easy upgrade path for self-hosters.
- **Use cases**: Corporate communication via email, secure headless GitHub Copilot integration, multi-agent workflows with clear ownership boundaries, Telegram business messaging.
- **Satisfaction**: Positive engagement on feature proposals (email, OAuth MCP) and willingness to contribute fixes (e.g., #2836 security fix).

## 8. Backlog Watch
These items need maintainer attention due to age, importance, or lack of response:
- **[Feature] Email as native channel** ([#2421](https://github.com/sipeed/picoclaw/issues/2421)) – 33 days old, top comment count, no maintainer decision.
- **[Feature] OAuth 2.1 + PKCE for MCP servers** ([#2546](https://github.com/sipeed/picoclaw/issues/2546)) – 24 days old, stale label, unresolved despite being a frequent user ask.
- **[Bug] OpenRouter reasoning leak** ([#2745](https://github.com/sipeed/picoclaw/issues/2745)) – 8 days old, stale label, high severity but no fix PR yet.
- **[Bug] Codex OAuth empty response** ([#2674](https://github.com/sipeed/picoclaw/issues/2674)) – 14 days old, 3 upvotes, still open without a reproducer or fix.
- **[PR] Fix gateway media store alignment after reload** ([#2783](https://github.com/sipeed/picoclaw/pull/2783)) – 4 days old, no comments from maintainers, may be waiting for review.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-10

## 1. Today’s Overview

Project activity is high, with 18 pull requests updated in the last 24 hours and 11 merged/closed. Three open issues were updated, all remaining active. Development centres on container configuration management, skill ecosystem expansion, and compliance fixes. The merged PRs signal a release cycle in steady state, while open issues highlight ongoing edge cases in agent delegation and credential handling. No new releases were cut today, but the volume of merged features suggests an imminent version bump.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Project Progress

Eleven pull requests were merged or closed today, covering substantial infrastructure changes, new skills, and targeted fixes.

**Infrastructure & Configuration**
- [#2280 – fix(claude-provider): use `[1m]` model tag for reliable 1M context](https://github.com/nanocoai/nanoclaw/pull/2280) — Plumbs model-field through container config to signal extended context without betas.
- [#2233 – feat(container-config): add per-group model + effort overrides](https://github.com/nanocoai/nanoclaw/pull/2233) — Adds per-group runtime overrides for model and effort, enabling fine-grained agent tuning.
- [#2351 – feat(db): move container config from filesystem to DB](https://github.com/nanocoai/nanoclaw/pull/2351) — Source of truth for runtime config moves to a central database table; files become materialised views. No container-side changes required.
- [#2364 – chore(container): bump claude-code 2.1.116 → 2.1.128](https://github.com/nanocoai/nanoclaw/pull/2364) — 12 patch versions, including `${CLAUDE_EFFORT}`, plugin `channels` field, and settled `arguments` frontmatter.

**New Skills**
- [#2318 – feat(skills): add `/add‑mnemon` — persistent semantic memory](https://github.com/nanocoai/nanoclaw/pull/2318) — Installs a queryable knowledge graph that survives container restarts and context compaction.
- [#2319 – feat(add‑aws): AWS CLI access in agent containers](https://github.com/nanocoai/nanoclaw/pull/2319) — Wires `awscli`, CA bundle, and vault-stored credentials into agent containers.

**Accuracy & Stability Fixes**
- [#2372 / #2371 – fix: COO brief accuracy — skeleton templates, NPS source, ALICE windows, timestamps](https://github.com/nanocoai/nanoclaw/pull/2372) — Locks output to fill-in skeletons, corrects NPS source filter, and fixes temporal windows flagged by Austin GM.
- [#2352 – fix(container-runner): raise `install_packages` build timeout to 15 min](https://github.com/nanocoai/nanoclaw/pull/2352) — Resolves `ETIMEDOUT` on slow networks during self-mod package installation.

**Documentation**
- [#2373 – docs: add changelog entry for 2.0.54](https://github.com/nanocoai/nanoclaw/pull/2373)
- [#2320 – docs(skills): update SKILL.md for six skills](https://github.com/nanocoai/nanoclaw/pull/2320) — Troubleshooting, credential migration, and setup instructions refreshed.

---

## 4. Community Hot Topics

Most discussion remains on open issues and PRs with no merged resolution yet.

- **[#2369 – Destinations-addendum compliance degrades past N tools](https://github.com/nanocoai/nanoclaw/issues/2369)** (1 comment)  
  *Pain point:* When groups exceed 30+ MCP tools, agents begin *narrating* delegation instead of emitting the correct `<message to=>` tag. This breaks multi-destination workflows and suggests a threshold bug in prompt construction or tool routing.

- **[#1669 – Does Credential Proxy implementation risk Anthropic account bans?](https://github.com/nanocoai/nanoclaw/issues/1669)** (1 comment, open since April 6)  
  *Concern:* Users ask whether the current OAuth reverse‑proxy implementation violates Anthropic’s prohibition and could trigger anti‑fraud checks. No maintainer response yet.

- **[#2370 – WhatsApp attachments not mounted into agent containers](https://github.com/nanocoai/nanoclaw/issues/2370)** (0 comments)  
  *Bug:* Inbound attachments are saved to the host’s `data/attachments/` directory but the mount is missing, causing agent-runner failures when referencing `/workspace/<localPath>`.

**Open PRs with ongoing development:**
- [#2368 – feat(self‑mod): agent‑initiated plugin install/uninstall + denial cache](https://github.com/nanocoai/nanoclaw/pull/2368)
- [#2367 – feat(skills): seven operator skills for plugin/marketplace management](https://github.com/nanocoai/nanoclaw/pull/2367)
- [#2365 – feat(plugins): wire `extraKnownMarketplaces` + `enabledPlugins` via container.json](https://github.com/nanocoai/nanoclaw/pull/2365)
- [#2363 – fix(credential‑proxy): proactively refresh expiring Anthropic OAuth tokens (v2 port)](https://github.com/nanocoai/nanoclaw/pull/2363)
- [#2366 – feat(skills): add `SKILL_DATA_DIR` per‑group persistent state mount](https://github.com/nanocoai/nanoclaw/pull/2366)
- [#2362 – feat/add watchdog](https://github.com/nanocoai/nanoclaw/pull/2362)
- [#2361 – tighten codex provider contracts](https://github.com/nanocoai/nanoclaw/pull/2361)

These PRs indicate strong community and contributor interest in plugin ecosystems, credential renewal, and persistent skill state.

---

## 5. Bugs & Stability

**Severity: Medium**

- **[#2369 – Compliance degrades past ~N tools](https://github.com/nanocoai/nanoclaw/issues/2369)**  
  *Impact:* Agents in multi‑destination groups with many MCP tools fail to emit proper delegation tags, instead narrating actions. No fix PR exists yet; root cause likely in prompt construction or tool aggregation.  
  *Severity:* Moderate — breaks expected multi‑agent orchestration.

- **[#2370 – WhatsApp attachments not mounted into containers](https://github.com/nanocoai/nanoclaw/issues/2370)**  
  *Impact:* Attachments stored on host are inaccessible to agent containers, causing runtime errors for WhatsApp‑sourced media.  
  *Severity:* Moderate — new feature gap; no fix PR yet.

- **[#1669 – Credential proxy ban risk](https://github.com/nanocoai/nanoclaw/issues/1669)** (not a crash but a stability/governance concern)  
  *Impact:* Potential account suspension if Anthropic enforces OAuth reverse‑proxy restrictions. No resolution or official response.  
  *Severity:* Low/Medium — depends on enforcement.

**Fixed today:**
- COO brief accuracy (PRs #2372, #2371) – resolved invented sections and wrong data source.
- Build timeout (PR #2352) – prevents `ETIMEDOUT` during self‑mod package installation.

---

## 6. Feature Requests & Roadmap Signals

The data shows strong momentum toward three themes:

1. **Plugin & Marketplace Ecosystem** – PRs #2365, #2367, #2368, and #2366 introduce operator skills for plugin install/uninstall, `extraKnownMarketplaces`, and persistent skill data directories. These align with Claude Code’s plugin taxonomy and suggest a future where NanoClaw agents can independently discover, install, and manage plugins under admin approval.

2. **Persistent Agent Memory** – PR #2318 (`/add‑mnemon`) already merged, bringing semantic memory with entity tags and importance scores. The open `SKILL_DATA_DIR` PR (#2366) complements this by providing a dedicated host‑persistent path for any skill’s state.

3. **Credential Safety & Governance** – PR #2363 (proactive OAuth token refresh) and the ongoing concern in #1669 indicate users and maintainers are investing in secure credential proxy practices.

**Predictions for next version (likely 2.0.55 or 2.1.x):**
- Integration of the plugin marketplace PRs (#2365, #2367, #2368) as they are closely related.
- Credential proxy token refresh (#2363) to mitigate ban risk.
- Codex provider contract tightening (#2361) for better multi‑provider support.

---

## 7. User Feedback Summary

Recent feedback clusters around three pain points:

- **Delegation compliance breaks at scale** – Issue #2369 describes a real scenario where agent groups with numerous MCP tools fail to produce the correct delegation format. This undermines confidence in multi‑agent orchestration for power users.

- **Concerns about Anthropic account security** – Issue #1669 shows users are cautious about violating Anthropic’s terms. The silence from maintainers may be causing hesitation to use the credential proxy feature.

- **Missing attachment mounts for WhatsApp** – Issue #2370 reports a clear usability gap for WhatsApp‑based workflows. Quick triage is needed to avoid frustration for channel integrators.

- **COO Brief accuracy** – The fix in PR #2372 was prompted by real user (Austin GM) feedback. The underlying need for deterministic, template‑driven reports is now addressed.

Overall, users are actively deploying NanoClaw for production workflows (multi‑destination, WhatsApp, retail analytics) and demanding reliability and compliance.

---

## 8. Backlog Watch

- **[Issue #1669 – Credential proxy ban risk](https://github.com/nanocoai/nanoclaw/issues/1669)**  
  *Created:* 2026-04-06 | *Last updated:* 2026-05-09 | *Comments:* 1  
  *Status:* No maintainer response in over a month. Given the sensitivity of account bans, this deserves an official statement or a link to an existing security audit/guidance. A fix PR (#2363) exists but only targets token refresh, not the policy question.

- **[Issue #2370 – WhatsApp attachments missing mount](https://github.com/nanocoai/nanoclaw/issues/2370)**  
  *Created:* 2026-05-09 | *Comments:* 0  
  *Status:* New, but no triage or acknowledgment. Should be assigned and marked `bug` promptly to signal visibility.

No other issues appear to have been long‑ignored; the community engagement is healthy.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

## NullClaw Project Digest — 2026-05-10

### 1. Today's Overview

NullClaw saw moderate activity over the past 24 hours, with one open issue, three pull requests updated (two closed/merged, one still open), and no new releases. A **regression bug** in the 2026.5.x line was reported, breaking connectivity when using the `siliconflow` provider—an issue that had worked in the previous stable release (2026.4.9). On the positive side, a useful **security feature** (HTTP domain whitelisting) was merged, and a **hackathon submission** from the **WB × OpenSource Hackathon** proposing a Data Governance Layer remains under review. Overall, the project is actively maintained, though the regression signals a need for careful patch testing.

### 2. Releases

No new releases were published today. The latest stable version remains **2026.4.9**. Users upgrading to the 2026.5.x branch should be aware of the regression described below (Issue #902).

### 3. Project Progress

Two pull requests were closed/merged today, advancing both infrastructure and user-facing features:

- **PR #903** (closed) — **feat: add config to whitelist insecure http endpoints**  
  Introduces `http_request.allowed_insecure_domains` configuration, enabling agents to connect to whitelisted HTTP endpoints (e.g., other containers in a Docker Compose stack). This improves flexibility for local/development setups while maintaining security defaults.  
  [GitHub Link](https://github.com/nullclaw/nullclaw/pull/903)

- **PR #796** (closed) — **ci: add Nix flake build workflow**  
  Adds a CI job that builds and smoke-tests the NullClaw Nix flake on every push and PR, using `cachix/install-nix-action` and `nix-community/cache-nix-action`. This strengthens cross-platform build reliability.  
  [GitHub Link](https://github.com/nullclaw/nullclaw/pull/796)

### 4. Community Hot Topics

Activity in issues and PRs was low in terms of comments and reactions. The most notable items are:

- **Issue #902** — **[Bug] HostResolutionFailed when using siliconflow provider**  
  Reported by `agiminds`, this is the only open issue updated today. It describes a regression in 2026.5.x that breaks provider connectivity. The author explicitly states that the exact same configuration works in 2026.4.9, pointing to HTTP/DNS client refactoring as the likely cause. No comments or reactions yet, but the bug directly affects users who rely on the `siliconflow` provider.  
  [GitHub Link](https://github.com/nullclaw/nullclaw/issues/902)

- **PR #885** (open) — **[hackathon] feat(memory): Add NullClaw Data Governance Layer**  
  Submitted by the “Безопасность бэкофиса (DS)” team as part of the **WB × OpenSource Hackathon**, this PR introduces a comprehensive data governance layer. Though not yet merged, it signals growing community interest in memory management, privacy, and compliance features.  
  [GitHub Link](https://github.com/nullclaw/nullclaw/pull/885)

### 5. Bugs & Stability

**Severity: High** — One regression reported:

- **Issue #902**: `HostResolutionFailed` error when using the `siliconflow` provider in the 2026.5.x branch. The error occurs immediately and appears to be a direct consequence of HTTP/DNS client refactoring in the new release line. No fix PR exists yet. Users are advised to either stay on 2026.4.9 or wait for a patch.  
  [GitHub Link](https://github.com/nullclaw/nullclaw/issues/902)

No other bugs or crashes were reported in the last 24 hours.

### 6. Feature Requests & Roadmap Signals

- **HTTP Insecure Domain Whitelist** (PR #903, already merged): This feature is now available for developers who need to connect agents to internal HTTP endpoints, such as in Docker Compose stacks. It directly addresses a common pain point in local/testing environments.
- **Data Governance Layer** (PR #885, open): The hackathon submission proposes features like memory policy controls, audit trails, and privacy-preserving data handling. If accepted, it could become a cornerstone of NullClaw’s enterprise offering. Given the hackathon context, a decision from maintainers is expected soon.
- No explicit feature requests were filed as issues in the last 24 hours.

### 7. User Feedback Summary

The single user report (Issue #902) reflects clear **dissatisfaction** with a regression: “Exact same config, token, network works perfectly in 2026.4.9.” This demonstrates that users expect backward compatibility and rely on the `siliconflow` provider for production workloads. The lack of workaround or immediate fix is a pain point. On a positive note, the merged whitelist feature (PR #903) directly addresses a previously missing capability, likely improving satisfaction for users deploying NullClaw in containerized environments.

### 8. Backlog Watch

No long-unanswered issues or PRs were identified in the provided data. The oldest open PR is #885 (created May 4, 2026), which is actively being reviewed as part of the hackathon. The only open issue (#902) was created yesterday, so it has not yet had time to wait for attention. Maintainers should monitor #902 closely and prioritize a hotfix for the regression, as it affects a commonly used provider.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-10

## 1. Today's Overview

IronClaw saw very high activity over the past 24 hours, with 33 pull requests updated (13 merged/closed) and 19 issues updated (18 open). The project remains heavily focused on the **Reborn architecture landing** (epic #2987), which accounted for the majority of new issues and PRs. A nightly end-to-end test failure (#3447) was reported but appears unrelated to the Reborn push. No new releases were published. Overall project health is strong but under strain from the large-scale Reborn integration; the team is delivering at a rapid pace.

## 2. Releases

No new releases were published in the last 24 hours. No new tags or binaries were detected. (Omitted as requested.)

## 3. Project Progress

**13 pull requests were merged or closed** in the last 24 hours. The following were among the most significant (top 20 by comment count):

- **[#3437] Avoid REPL auth retry race in E2E** — Fixed a flaky end-to-end test that was causing sporadic failures in the CI pipeline.
- **[#3427] feat(reborn): add durable resource governor** — Added `PersistentResourceGovernor` with JSON-file, libSQL, and PostgreSQL stores, improving resource accounting for production Reborn runs.
- **[#3426] Implement Reborn visible capability catalog** — Implements `ToolSurfaceService`/`CapabilityCatalog` for host-runtime visibility filtering by trust, grants, and approval policies.
- **[#3414] feat(reborn): add durable encrypted secret store** — libSQL/Postgres `SecretsStore` that persists encrypted secrets with per-row salts and atomic `consume_if_matches` for OAuth token exchange.
- **[#3411] feat(reborn): add loop prompt bundle port** — Added `LoopPromptPort` DTOs and a text-only `HostManagedLoopPromptPort` to materialize host-owned prompts without exposing raw provider internals.
- **[#3398] Compose Reborn text-only loop host ports** — Stacked on #3397 to compose thread-backed context, model, transcript, and empty capability ports with integration coverage.
- **[#3445] fix(reborn): close secret store review gaps** — Preserved durable secret metadata and ensured pre-sentinel store readiness decryption.
- **[#3440] fix(resources): close durable governor review gaps** — Rebuilt host-runtime process lifecycle store linkage and sanitized `ResourceError::Storage` display.

Additionally, several older PRs (e.g., #1378 per-channel tool filtering) received updates but remain open.

## 4. Community Hot Topics

The most active discussions were squarely around the Reborn architecture:

- **[#2987] [EPIC] Track Reborn architecture landing strategy and grouped PR plan** (44 comments, 0 👍) — The definitive tracker for the Reborn landing. Updated on May 9 with the latest shape of the grouped implementation PRs. This issue is the central coordination point for all Reborn work.
- **[#84] feat: Agent system advanced features** (4 comments, no reactions recently) — A long-standing feature parity request for multi-agent routing, global sessions, and thinking modes. Low recent activity but represents a key community need.
- **[#2949] ERROR: there isn't a download for your platform x86_64-unknown-linux-gnu** (4 comments) — A user-facing install issue on Linux. The release page shows the build exists, but the installer script fails to match the platform. Some confusion around naming conventions.
- **[#3107] [Reborn] Define AgentLoopDriver and run-class profile contract** (3 comments) — Another Reborn tracker for the driver contract, closely linked to the epic.

Underlying need: The community is closely watching the Reborn architecture landing because it will unlock production-grade turn orchestration, secret management, and multi-tenant isolation. The high comment count on #2987 reflects the team’s transparent planning process.

## 5. Bugs & Stability

**Bugs reported in the last 24 hours**, ranked by severity:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **High** | [#3425] Bug: Intermittent i18n regression in Production causes translation keys to render in the UI (raw keys like `auth.title`) | Production agents intermittently show i18n keys instead of localized strings. Affects UI tabs and auth screens. | No fix PR linked yet. |
| **High** | [#3447] Nightly E2E failed | CI failure in the `Full E2E / E2E (v2-engine)` job. Commit `6e6eca77` is the head. No additional details provided. | Not yet; likely being investigated. |
| **Medium** | [#3436] DeepSeek API returns 400: reasoning_content must be passed back in thinking mode | When using DeepSeek with thinking/reasoning mode, the provider returns a 400 error. User @Serhioromano reported with a 👍. | No fix PR yet. |
| **Low** | [#3447] also reports `web-regressions` job failure (previous nightly run #3323 was closed but may be recurring) | Previous nightly failure closed without public root cause. | #3323 was closed, but underlying issue may persist. |

Notable fix: **#3437** (REPL auth retry race) was merged and should improve CI stability for auth-related tests.

## 6. Feature Requests & Roadmap Signals

- **[#84] Agent system advanced features** (multi-agent, streaming, thinking modes, elevated mode) — This is a direct user request from February. While not in immediate focus due to Reborn, the thinking mode issue (#3436) may accelerate a DeepSeek-specific fix. The feature likely lands in the **next minor release** after Reborn stabilizes.
- **[#3436] DeepSeek thinking mode support** — The bug report also serves as a feature request: users want proper thinking/reasoning round-trip with DeepSeek. A fix is likely in the near-term backlog.
- **Reborn architecture** (multiple issues: #3429, #3431, #3432, #3433, #3434, #3435, etc.) — While internal, these are direct signals that **production readiness validations, memory prompt services, skill context service, and budget/credential tests** are being completed. Expect a Reborn “beta” or “stable” release once the EPIC (#2987) is closed.
- **[#3419] Define shared Reborn storage substrate and secret-store boundary** — Suggests consolidation of domain-local SQL adapters into a unified storage layer. This will reduce maintenance overhead and improve cross-domain query capabilities.

## 7. User Feedback Summary

- **Installation friction**: User @gittyhubert (#2949) attempted to install on `x86_64-unknown-linux-gnu` but the installer script did not recognise the platform despite the release archive existing. This is a **moderate pain point** for new users on Linux.
- **Internationalization regression**: @sunglow666 (#3425) reported raw i18n keys showing in production UI — a clear regression affecting user trust. No immediate workaround.
- **DeepSeek integration breakage**: @Serhioromano (#3436) encountered a 400 error when using thinking mode. This affects users relying on DeepSeek for reasoning tasks.
- **General sentiment**: The high pace of Reborn development suggests the team is responsive to architectural needs, but end-user issues (install, i18n, third-party provider compatibility) may be temporarily deprioritized. The broader community seems engaged in watching Reborn progress.

## 8. Backlog Watch

- **[#84] Agent system advanced features** — Opened on **2026-02-14**, last updated 2026-05-09. Three months stale with only 4 comments. This is a significant feature request that has not seen dedicated implementation yet. Likely blocked by Reborn completion.
- **[#2949] Install platform detection issue** — Opened **2026-04-24**, last updated 2026-05-09. User has been waiting over two weeks. A quick triage could improve first-time user experience.
- **[#1378] per-channel MCP and built-in tool filtering** — PR opened **2026-03-18**, last updated today (2026-05-10). An experienced contributor’s large PR covering multi-channel tool scoping. It has received no comments and remains unmerged. This PR may need maintainer attention to review the configuration scheme and resolve conflicts.
- **[#3352] feat(reborn): add product adapter host auth and egress primitives** — Opened 2026-05-07, still open though the broader ProductAdapter stack is moving fast. Needs review to unblock downstream PRs.

**Maintainer attention recommended**: #1378 (stale large PR), #2949 (user-impacting install bug), and #84 (long-standing feature request) could benefit from a maintainer comment or roadmap assignment.

---

*Digest generated for 2026-05-10 from nearai/ironclaw GitHub data.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Based on the provided GitHub data for LobsterAI (github.com/netease-youdao/LobsterAI), here is the project digest for 2026-05-10.

---

# LobsterAI Project Digest - 2026-05-10

## 1. Today's Overview

Today marks a period of **high maintenance activity** for LobsterAI, with 26 pull requests updated and a new patch release. While no new issues were opened, the team is focused on **closing out a backlog of stability and bug-fix PRs**, many of which are marked as `stale`. The single issue closed today (`#820`) resolves a significant packaging bug related to MCP functionality, indicating a strong focus on hardening the project for production use. The release of v2026.5.9 introduces notable new features, including independent agent working directories and an artifact system, alongside performance improvements like paginated session loading.

## 2. Releases

- **New Version: [LobsterAI 2026.5.9](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.5.9)**
  - **Date:** 2026-05-09

**Key Changes:**
- **Feature:** Each Agent now supports an independent working directory (`#1904`). This is a significant enhancement for users running multi-agent setups, allowing for better isolation of files, workspaces, and session data per agent.
- **Feature:** Introduction of an "artifact" system (`#1906`). This likely relates to the ability for agents to generate and manage files, code, or other digital artifacts as part of their output.
- **Feature:** Added paginated loading for session list and message history (`#924`). This improves performance and user experience for users with long conversation histories.

**Migration Notes:** No breaking changes or specific migration steps were mentioned in the release notes. Users can update directly from the previous beta version.

## 3. Project Progress

Today, **7 PRs were merged or closed (total 26 updated)**. The primary focus was on fixing regressions, improving data consistency, and closing out stale, but important, bug fixes that have been open for weeks.

**Key Fixes & Features Advanced Today:**
- **Data Integrity & Migration:**
    - `#1595`: Fixed a critical bug in SQLite where a failed legacy memory migration was incorrectly marked as complete, preventing future retries.
- **Configuration & Security:**
    - `#1606`: Addressed a security concern by replacing a hardcoded NetEase Bee secret key in the `openclaw.json` config with an environment variable placeholder.
- **API & Streaming Stability:**
    - `#1607`: Added SSE (Server-Sent Events) line buffering for Anthropic and Gemini API requests, preventing content loss or stream interruption when JSON data is split across network packets.
- **User Interface & Experience:**
    - `#857` (Closed): Implemented HTTP streaming support for MCP, a feature requested by the community.
    - `#1600`: Fixed a form navigation bug in the scheduled task page that falsely warned users about unsaved changes after a successful save.

## 4. Community Hot Topics

Today's activity shows a project team deeply engaged in resolving long-standing issues. There are no new issues with high comment counts, but the activity on the closed issue is notable:

- **Most Active Issue:** **[#820 [CLOSED] dev阶段MCP可用；打包后，MCP不可用](https://github.com/netease-youdao/LobsterAI/issues/820)**
    - **Summary:** A user reported that MCP (Model Context Protocol) configurations that worked during development failed to show any tools after the application was packaged. The user did significant testing, including cloning the repo to confirm the feature worked in dev.
    - **Analysis:** This was a high-priority issue affecting the packaging/delivery pipeline. The fact that it was closed today suggests the fix was likely included in the v2026.5.9 release or is related to a recently merged PR. The underlying need is for the development experience to perfectly mirror the production experience.

## 5. Bugs & Stability

The vast majority of today's PRs are dedicated to fixing bugs and stability issues. Here are the most critical ones, ranked by severity:

- **High Severity:**
    - **[#1602](https://github.com/netease-youdao/LobsterAI/pull/1602) (OPEN): Concurrent Race in `addMessage` Sequence Number.** Under heavy load, this bug could cause duplicate message sequence numbers, leading to potential data corruption and session ordering issues. A fix PR exists.
    - **[#1601](https://github.com/netease-youdao/LobsterAI/pull/1601) (OPEN): Gateway Reconnect Clears Session Stop State.** A critical logic bug where a WebSocket reconnection would clear the "stopped" state for all sessions, causing user-stopped sessions to be unintentionally revived by incoming messages.
    - **[#1593](https://github.com/netease-youdao/LobsterAI/pull/1593) (OPEN): OpenClaw Gateway Crash on Startup.** A configuration bug caused the OpenClaw gateway to crash loop on startup due to an unrecognized config key (`skipMissedJobs`).

- **Medium Severity:**
    - **[#1603](https://github.com/netease-youdao/LobsterAI/pull/1603) (OPEN): Duplicate Error Messages & Swallowed Exceptions.** Duplicate error messages in the UI and critical errors being silently swallowed in the backend.
    - **[#1594](https://github.com/netease-youdao/LobsterAI/pull/1594) (OPEN): Session Search Broken.** The search function was limited to the current agent and only searched titles, not message content, making it nearly useless for finding specific information.
    - **[#1598](https://github.com/netease-youdao/LobsterAI/pull/1598) (OPEN): `executionMode` Hardcoded.** The configuration system ignored the user's chosen execution mode (local/auto/sandbox), always defaulting to 'local'.

## 6. Feature Requests & Roadmap Signals

While no new feature requests were opened today, several signals point toward the next version's priorities based on open PRs:

- **Collaboration & UX Improvement:**
    - **[#1590](https://github.com/netease-youdao/LobsterAI/pull/1590) (OPEN): Message Queue During AI Reply.** This feature would allow users to type and queue up messages while the AI is still generating a response, a major UX improvement for power users. This is a strong candidate for the next release.
    - **[#1584](https://github.com/netease-youdao/LobsterAI/pull/1584) (OPEN): Short UUID for Agent IDs.** This prevents data leakage between deleted and new agents. This is a backend stability and data privacy improvement that is likely to be merged soon.

- **Ecosystem & Integration:**
    - **[#857](https://github.com/netease-youdao/LobsterAI/pull/857) (CLOSED): MCP HTTP Streaming Support.** A user-requested feature that was just closed today, indicating it is now available.

## 7. User Feedback Summary

- **Primary Pain Points:**
    - **Configuration & Deployment:** The single biggest pain point is the inconsistency between development and production/packaged environments (Issue #820). Users are frustrated that features work during development but fail after packaging.
    - **Data Loss & Stability:** There is an underlying anxiety about data integrity, evidenced by the high number of fixes for SQLite migrations, session state, and message ordering. Users are experiencing "orphan" data and unexpected session behavior.
    - **Usability:** The fact that the search function was broken (PR #1594) for an extended period is a significant UX pain point for users trying to retrieve information from their history.

- **Positive Signals:**
    - **Responsive Maintainers:** The closure of Issue #820 and the rapid development of the MCP streaming support (PR #857) show that the team is responsive to community feedback and critical bugs.

## 8. Backlog Watch

Several high-priority PRs remain open and appear to be stagnating. These have been marked as `stale` for over a month and require immediate maintainer attention.

- **Highest Priority:**
    - **[#1601](https://github.com/netease-youdao/LobsterAI/pull/1601): Gateway Reconnect Clears Session Stop State.** This is a critical stability bug that could lead to unwanted AI responses in the middle of the night for users. It has been open since April 9th.
    - **[#1593](https://github.com/netease-youdao/LobsterAI/pull/1593): OpenClaw Gateway Crash on Startup.** This bug prevents the entire gateway from functioning for some users. It has been open since April 9th.
    - **[#1594](https://github.com/netease-youdao/LobsterAI/pull/1594): Session Search Broken.** This is a core usability bug that has been open since April 9th.

- **Notable Stale Items:**
    - **[#1584](https://github.com/netease-youdao/LobsterAI/pull/1584): Agent ID Generation.** This fix prevents a serious data leakage issue. Despite being a critical non-functional requirement, it has been open since April 9th.
    - **[#1585](https://github.com/netease-youdao/LobsterAI/pull/1585): Enter Key Closes Settings.** A frustrating UX bug that has been open for over a month.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-10

## 1. Today's Overview
Moltis saw moderate development activity over the past 24 hours, with two pull requests updated but no new releases or open issues. A significant UI enhancement for the web chat interface (PR #985) was merged, redesigning the composer with a centered rounded layout and improved footer controls. Another PR (#987) remains open, proposing a migration from mdBook to an Astro-based documentation site. The project appears to be focusing on polish and documentation infrastructure, with no active bugs or feature requests reported.

## 2. Releases
No new releases were published in the last 24 hours. The latest release remains unchanged. No migration notes or breaking changes to report.

## 3. Project Progress
- **PR #985 (closed/merged)** — *Refresh web chat composer*  
  Author: penso  
  Summary: Redesigned the chat input as a centered rounded composer with footer controls for model selection, reasoning, attachments, voice, and send. Moved token/context status into the footer with wrapping instead of truncation. Added an explicit attachment picker and handled empty queued messages.  
  → This PR advances the user interface by modernizing the chat input area and improving usability.  
  [View PR #985](https://github.com/moltis-org/moltis/pull/985)

- **PR #987 (open)** — *Replace docs deployment with Astro site*  
  Author: penso  
  Summary: Proposes replacing the existing mdBook deployment with an Astro-generated docs site, retaining existing Markdown sources and `.html` URLs. Includes a custom shell with sidebar navigation, page TOC, copy buttons, title search, responsive hamburger menu, and light/dark/auto theme controls.  
  → This is an infrastructure improvement to enhance documentation readability and maintainability.  
  [View PR #987](https://github.com/moltis-org/moltis/pull/987)

## 4. Community Hot Topics
Both PRs have **0 comments and 0 reactions**, indicating low community engagement in the past 24 hours. No issues were updated. The underlying need in PR #985 is a more intuitive and modern chat input experience, while PR #987 addresses the desire for a better document browsing experience. Both are maintainer-driven, not user-requested.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. No associated fix PRs. Project stability appears healthy.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were made in the last 24 hours. Based on the two active PRs, the team is prioritizing:
- UI polish (chat composer redesign) — likely to be part of the next release.
- Documentation infrastructure overhaul (Astro migration) — may land in a subsequent release.

No user-requested features were observed; the roadmap seems internally driven at this time.

## 7. User Feedback Summary
No user feedback (comments, reactions, or issue descriptions) was recorded in the last 24 hours. It is not possible to assess user satisfaction or pain points from the available data.

## 8. Backlog Watch
No important issues or PRs have been left unanswered for an extended period. Both open/updated PRs are recent (created 2026-05-08, updated 2026-05-09). No long-standing blockers are apparent.

---

*This digest is generated from GitHub data available for the period 2026-05-09 to 2026-05-10.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-10

## 1. Today's Overview

CoPaw (QwenPaw) maintained high activity over the past 24 hours with 29 issues updated (16 open/active, 13 closed) and 18 pull requests (10 open, 8 merged/closed). Two new releases were published: v1.1.6 and v1.1.6-beta.2, reflecting ongoing stability improvements and feature additions. The community remains engaged, contributing both bug reports and code fixes — notably a critical memory leak fix in MCP subprocess management and a Windows diagnostics enhancement. Overall project health is strong, with maintainers actively merging fixes and tracking feature requests.

## 2. Releases

**v1.1.6** — [Release Notes](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.6)
- Added `qwenpaw doctor` with Windows-specific environment checks (long path support, PowerShell language mode, working directory length).
- Introduced Agent Status API.
- No breaking changes or migration notes.

**v1.1.6-beta.2** — [Release Notes](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.6-beta.2)
- Fix: renamed `channel` variable to `channel_name` in command dispatch (runner).
- Perf: skip chat history lookup for non-arrow keys in console.
- No breaking changes.

## 3. Project Progress

Eight PRs were merged or closed today, advancing both stability and features:

- **MCP lifecycle fix** ([#4152](https://github.com/agentscope-ai/QwenPaw/pull/4152)) — Fixed orphaned MCP subprocess accumulation (`~18 GB RAM leak over 1.5 days`). The root cause (early return on `close()` when `is_connected=False`) is resolved.
- **Agent config persistence** ([#4157](https://github.com/agentscope-ai/QwenPaw/pull/4157)) — Preserves complete agent configuration on save, preventing nested config loss when multiple agents are configured.
- **Console QrcodeAuth refactor** ([#4153](https://github.com/agentscope-ai/QwenPaw/pull/4153)) — Extracted reusable component and fixed polling leak on drawer close.
- **Feishu channel user display name** ([#4055](https://github.com/agentscope-ai/QwenPaw/pull/4055)) — Propagates sender nickname instead of raw `open_id` to agent context.
- **OpenWond Draw Tool plugin** ([#4172](https://github.com/agentscope-ai/QwenPaw/pull/4172)) — Adds image generation via GPT Image 2 and Nano Banana fallback.
- **Release infrastructure** — Version bump ([#4161](https://github.com/agentscope-ai/QwenPaw/pull/4161)), release notes update ([#4163](https://github.com/agentscope-ai/QwenPaw/pull/4163)), and New Contributors section ([#4168](https://github.com/agentscope-ai/QwenPaw/pull/4168)).

## 4. Community Hot Topics

Most active discussions (highest comment count):

| Issue | Topic | Comments |
|-------|-------|----------|
| [#578](https://github.com/agentscope-ai/QwenPaw/issues/578) | Meta: OpenClaw-inspired features for compounding agent value | 8 |
| [#4165](https://github.com/agentscope-ai/QwenPaw/issues/4165) | Volcano Engine model configuration not working | 8 |
| [#4145](https://github.com/agentscope-ai/QwenPaw/issues/4145) (CLOSED) | Multi-agent config not persisting | 8 |
| [#3843](https://github.com/agentscope-ai/QwenPaw/issues/3843) | Session history disappears / new messages routed elsewhere | 7 |
| [#4164](https://github.com/agentscope-ai/QwenPaw/issues/4164) (CLOSED) | Request for Chinese prompt support | 7 |

Underlying needs:
- **Provider configuration usability** — Users struggle with non-OpenAI providers (Volcano Engine, LM Studio, DashScope). The Volcano Engine issue has a fix PR ([#4169](https://github.com/agentscope-ai/QwenPaw/pull/4169)) open.
- **Memory and session consistency** — Session disappearance and config loss are top pain points; both have received recent fixes.
- **Localization** — Chinese prompt support (for models like DeepSeek, GLM) is requested, reflecting the project’s strong Chinese-speaking user base.

## 5. Bugs & Stability

**Critical / High Severity:**
- **Orphaned MCP processes memory leak** ([#4105](https://github.com/agentscope-ai/QwenPaw/issues/4105)) — ~18 GB RAM leaked over 1.5 days. **Fixed** in [#4152](https://github.com/agentscope-ai/QwenPaw/pull/4152) (merged).
- **Volcano Engine provider broken** ([#4165](https://github.com/agentscope-ai/QwenPaw/issues/4165)) — All models fail connection due to incorrect model name mapping. **Fix available** ([#4169](https://github.com/agentscope-ai/QwenPaw/pull/4169)) awaiting merge.
- **DashScope provider API key not read** ([#4159](https://github.com/agentscope-ai/QwenPaw/issues/4159)) — Returns 401 despite correct config. No fix PR yet.
- **Agent actions only displayed after completion** ([#4170](https://github.com/agentscope-ai/QwenPaw/issues/4170)) — Blocks user from monitoring long-running actions. No fix yet.

**Medium / Active Discussion:**
- **MCP streamable_http auto-reconnect failure** ([#4100](https://github.com/agentscope-ai/QwenPaw/issues/4100)) — Connection lost after timeout, state inconsistent. Closed but likely related to lifecycle fix.
- **LM Studio integration returns Internal Server Error** ([#4147](https://github.com/agentscope-ai/QwenPaw/issues/4147)) — May be configuration mapping issue. Closed without fix.
- **Failed model calls persist user messages** ([#4149](https://github.com/agentscope-ai/QwenPaw/issues/4149)) — Replays failed message on next turn. Fixed in next commit.
- **Scheduled task ignores deleted session** ([#4162](https://github.com/agentscope-ai/QwenPaw/issues/4162)) — Old session context persists after deletion. No fix yet.

**Low / Cosmetic:**
- **Windows console window flash on `execute_shell_command`** ([#4123](https://github.com/agentscope-ai/QwenPaw/issues/4123)) — Annoying but functional. PR [#4173](https://github.com/agentscope-ai/QwenPaw/pull/4173) proposed fix for Unix.

## 6. Feature Requests & Roadmap Signals

**High-community-interest requests likely for next version:**
- **Multi-agent routing from single channel** ([#4160](https://github.com/agentscope-ai/QwenPaw/issues/4160)) — Enables dispatching messages to different agents via one endpoint. Currently no PR.
- **Pluggable memory manager with ADBPG** ([#2307](https://github.com/agentscope-ai/QwenPaw/issues/2307)) — Long-standing request; PR [#2308](https://github.com/agentscope-ai/QwenPaw/pull/2308) has been open since March.
- **Tauri 2.x desktop app** ([#3813](https://github.com/agentscope-ai/QwenPaw/pull/3813)) — PR under review; could replace Electron-based desktop.
- **Dream Log Output for memory consolidation** ([#3663](https://github.com/agentscope-ai/QwenPaw/issues/3663)) — Already closed; likely implemented in recent builds.

**Other notable requests:**
- Inject current timestamp in `pre_reply` hook ([#4166](https://github.com/agentscope-ai/QwenPaw/issues/4166)) — **Closed** (likely implemented).
- gpt-image2 reference image support ([#4167](https://github.com/agentscope-ai/QwenPaw/issues/4167))
- Font size adjustment and file path clickability ([#4154](https://github.com/agentscope-ai/QwenPaw/issues/4154))
- Client startup performance improvement ([#4158](https://github.com/agentscope-ai/QwenPaw/issues/4158)) — User suggests rebuilding with native packaging.

The next minor release (v1.1.7) is likely to include the Volcano Engine fix, MCP improvements, and possibly the multi-agent routing feature given its traction.

## 7. User Feedback Summary

**Pain Points:**
- Provider configuration remains confusing — multiple reports of misconfigured API keys, model names, and provider-specific quirks (Volcano Engine, LM Studio, DashScope).
- Session data loss or misrouting ([#3843](https://github.com/agentscope-ai/QwenPaw/issues/3843)) causes frustration during long conversations.
- Desktop startup is slow (~30 seconds) ([#4158](https://github.com/agentscope-ai/QwenPaw/issues/4158)) — user requests native packaging over Python bundling.
- Language switching UI not fully internationalized ([#4156](https://github.com/agentscope-ai/QwenPaw/issues/4156)).
- browser_use tool cannot reuse existing Chrome sessions ([#4155](https://github.com/agentscope-ai/QwenPaw/issues/4155)), requiring repeated logins.

**Satisfactions:**
- Many bugs are addressed quickly (e.g., config loss fix merged same day as report).
- Community-requested features (Draw tool plugin, time injection) are being implemented and merged.
- First-time contributors are active and welcomed (multiple PRs from new contributors merged today).

**Use Cases:**
- Chinese-speaking users heavily rely on DeepSeek, GLM, and Qwen models — hence the demand for Chinese prompts and local model support.
- Enterprise/team deployment: user reports syncing skills between test and production environments ([#4079](https://github.com/agentscope-ai/QwenPaw/issues/4079)) and running scheduled tasks with session isolation.

## 8. Backlog Watch

Issues and PRs requiring maintainer attention:

| Item | Created | Status | Age | Notes |
|------|---------|--------|-----|-------|
| [#2307](https://github.com/agentscope-ai/QwenPaw/issues/2307) / [#2308](https://github.com/agentscope-ai/QwenPaw/pull/2308) — ADBPG memory manager | 2026-03-26 | Open / Open PR | 45 days | No recent activity; needs review. |
| [#3525](https://github.com/agentscope-ai/QwenPaw/pull/3525) — Discord thread creation before agent dispatch | 2026-04-17 | Open PR (Under Review) | 23 days | Rebased onto main on 2026-05-09; needs final review. |
| [#3840](https://github.com/agentscope-ai/QwenPaw/issues/3840) — Xioayi (华为小艺) channel fails to send replies | 2026-04-26 | Open | 14 days | WebSocket protocol issue; no fix PR yet. |
| [#578](https://github.com/agentscope-ai/QwenPaw/issues/578) — Meta: OpenClaw-inspired features | 2026-03-04 | Open | 67 days | Long-running meta-issue; likely needs roadmap planning. |
| [#3813](https://github.com/agentscope-ai/QwenPaw/pull/3813) — Tauri 2.x desktop app | 2026-04-24 | Open PR (Under Review) | 16 days | Large PR; may need architectural discussion. |

These items represent either high-value features with no progress or long-standing bugs affecting specific channels. Their resolution would significantly improve project maturity.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-10

## 1. Today's Overview
Activity on the ZeptoClaw repository remained minimal over the past 24 hours. No new issues were reported, and no pull requests were merged or closed. The only update was a single open PR that saw its last edit on 2026-05-09, indicating a quiet period with no active bug reports or community discussion. The project appears stable but with limited recent development momentum.

## 2. Releases
No new releases were published. The latest available version is unchanged.

## 3. Project Progress
No pull requests were merged or closed today. All recent development efforts are concentrated in the sole open PR.

**Open PR ([#571](https://github.com/qhkm/zeptoclaw/pull/571)) — `feat(tools): trigger-phrase nudges in longterm_memory description`**
- **Author:** qhkm · **Created:** 2026-05-03 · **Last updated:** 2026-05-09
- This PR rewrites the `longterm_memory` tool’s description to enumerate explicit “Use when” and “Do NOT use when” trigger phrases, mirroring the pattern in Hermes Agent’s `memory_tool.py`. It also introduces a doc-test (`test_tool_description_has_trigger_phrases`) to ensure the trigger block is not accidentally removed in future edits.
- Status: Open, no reviews or comments yet.

## 4. Community Hot Topics
With zero issues and only one open PR, there are no topics drawing significant community attention. PR #571 is the only active discussion point (currently without comments or reactions), suggesting that the change is still awaiting review or wider input. No underlying user needs are apparent from the data.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported today. The project’s stability appears unaffected.

## 6. Feature Requests & Roadmap Signals
The only feature signal is PR #571, which aims to improve developer experience by making the `longterm_memory` tool description clearer with guardrails for appropriate usage. Such enhancements align with a broader trend in AI agent projects toward more explicit tool documentation and test coverage. If merged, this feature is likely to be included in the next release of ZeptoClaw.

## 7. User Feedback Summary
No user feedback (comments, reactions, or user-submitted issues) was recorded in the past 24 hours. The absence of complaints or suggestions may indicate general satisfaction or, alternatively, low community engagement during this period.

## 8. Backlog Watch
There are no long-unanswered issues or stale PRs requiring maintainer attention. The only open PR (#571) has been awaiting review since its creation on May 3; while not yet stale, it may benefit from maintainer review to keep development momentum.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-05-10

## Today’s Overview
ZeroClaw is in a high-activity phase, with **22 issues** and **26 pull requests** updated in the last 24 hours (15 open issues, 14 open PRs). The team closed 7 issues and merged/closed 12 PRs today, focusing on the upcoming **v0.8.0 release** (active `integration/v0.8.0` branch) which lands the long-awaited multi-agent runtime and a breaking change to environment-variable configuration. At the same time, several **high-severity bugs** surfaced – Discord media handling, system‑message ordering, and approval bypass – all of which already have fix PRs in review or merged. No new releases were published. Overall project health is **intense but responsive**, with core maintainers actively triaging and patching.

## Releases
*None.* No new versions were tagged in the last 24 hours. The most recent stable release remains **v0.7.5**.

## Project Progress – Merged/Closed PRs Today (selected)
- **Multi-agent runtime v0.8.0** – [#6545](https://github.com/zeroclaw-labs/zeroclaw/pull/6545) (feat, merged) lands the full multi-agent runtime: isolated workspaces, per‑alias identity, declared peers, and inheritable sub‑agents. Base branch is `integration/v0.8.0`.
- **Config env-var grammar (breaking)** – [#6523](https://github.com/zeroclaw-labs/zeroclaw/pull/6523) (feat, merged) restores a V3‑compatible environment variable schema for credentials and runtime knobs, dropping legacy overrides.
- **Config path respect** – [#6533](https://github.com/zeroclaw-labs/zeroclaw/pull/6533) (fix, merged) makes default paths respect `ZEROCLAW_CONFIG_DIR`, fixing multi‑instance deployments.
- **Build reliability** – [#6540](https://github.com/zeroclaw-labs/zeroclaw/pull/6540) (fix, merged) routes web‑dashboard builds through `cargo` to keep API client fresh.
- **Shell approval fix** – [#6539](https://github.com/zeroclaw-labs/zeroclaw/pull/6539) (fix, merged) ensures `shell` commands in direct sessions go through the approval back‑channel.
- **Channel session key scoping** – [#6541](https://github.com/zeroclaw-labs/zeroclaw/pull/6541) (fix, merged) enables `sessions_current` tools in channel contexts (Telegram, Discord, etc.).
- **Tool protocol suppression** – [#6546](https://github.com/zeroclaw-labs/zeroclaw/pull/6546) (fix, merged) suppresses empty‑tools prompt scaffolding for small models.
- **SOP engine reload** – [#6534](https://github.com/zeroclaw-labs/zeroclaw/pull/6534) (fix, merged) calls `reload()` after `SopEngine` construction – previously no SOPs were ever loaded.
- **Omitting native tool catalog** – [#6544](https://github.com/zeroclaw-labs/zeroclaw/pull/6544) (fix, merged) recovers prompt cleanup from a reverted commit.

## Community Hot Topics
_Issues and PRs with the most discussion in the last 24 hours._

1. **[#6378 – Discord Bot respond only in specific Discord channels](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) (5 comments)**  
   User requests an `allowed_channels` config field to restrict bot replies to whitelisted channels, mirroring the Matrix `allowed_rooms` pattern. The need reflects growing Discord deployments where operators want fine‑grained access control. **Accepted** with `p2` priority.

2. **[#6207 – Web dashboard / WebSocket gateway path bypasses ApprovalManager](https://github.com/zeroclaw-labs/zeroclaw/issues/6207) (4 comments, closed today)**  
   A high‑severity security bug where supervised tool approvals never surfaced in the daemon web UI. **Resolved** by #6539 (merged today). Community involvement helped identify the gap.

3. **[#6530 – Build failure with matrix-sdk v0.16.0](https://github.com/zeroclaw-labs/zeroclaw/issues/6530) (4 comments)**  
   Users report a recursion-limit overflow when building with `channel-matrix` feature on v0.7.5. The issue is open and assigned `p3`, but the Matrix channel is a valued integration.

4. **[#6272 – Multi-agent runtime: per-alias workspaces, permissions, and shared resources](https://github.com/zeroclaw-labs/zeroclaw/issues/6272) (2 comments, updated today)**  
   This V3 design proposal is the foundation for today’s merged #6545. The discussion confirms strong community interest in isolated agent environments.

5. **[#6558 – providers erro](https://github.com/zeroclaw-labs/zeroclaw/issues/6558) (2 comments)**  
   A user reports a **405 Method Not Allowed** error when using a custom OpenAI‑compatible endpoint (DashScope/Qwen). The provider adapter appears to send an incorrect HTTP method.

## Bugs & Stability
### High‑Severity (S1 / P1) Bugs
- **[#6207 (CLOSED) – Approval bypass via web dashboard](https://github.com/zeroclaw-labs/zeroclaw/issues/6207)** – Fixed in #6539 today. No longer a risk.
- **[#6361 – context_compression drops tool calls for OpenAI-compatible providers](https://github.com/zeroclaw-labs/zeroclaw/issues/6361)** – Still open. Causes tool loops and invalid `system` role errors with MiniMax. Requires maintainer review.
- **[#6551 – Non-leading system messages sent to OpenAI-compatible providers](https://github.com/zeroclaw-labs/zeroclaw/issues/6551)** – Open. Some endpoints reject non‑initial `system` messages. **Fix PR #6552 is open** (merges system messages to the first position).
- **[#6556 – Discord channel media send/receive broken](https://github.com/zeroclaw-labs/zeroclaw/issues/6556)** – Open. Four failures: empty attachments, non‑image types dropped, outbound markers leak. No fix PR yet, but flagged as `p1`.

### Medium‑Severity (S2 / P2)
- **[#6419 – WorkspaceManager fails to load profiles at startup on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/6419)** – Open. `load_profiles()` not invoked; affects v0.7.4.
- **[#6309 – model_routing_config stomps schema_version=2 settings](https://github.com/zeroclaw-labs/zeroclaw/issues/6309)** – Open. Agent‑run actions remove provider sections. P1 but accepted.
- **[#6548 – Channel runtime command replies bypass Fluent localization](https://github.com/zeroclaw-labs/zeroclaw/issues/6548)** – Open. Hard‑coded English strings even with `zh‑CN` locale. **Fix PR #6550 is open**.

### Low‑Severity (S3 / P3)
- **[#6530 – matrix-sdk build recursion overflow](https://github.com/zeroclaw-labs/zeroclaw/issues/6530)** – Open.
- **[#6558 – Provider error (405) with custom DashScope endpoint](https://github.com/zeroclaw-labs/zeroclaw/issues/6558)** – Open.
- **[#6547 (CLOSED) – Homebrew merge fail (no v0.7.5 in homebrew-core)](https://github.com/zeroclaw-labs/zeroclaw/issues/6547)** – Closed, but indicates a release‑process gap.

## Feature Requests & Roadmap Signals
| Issue / PR | Summary | Likely Version |
|---|---|---|
| [#6378](https://github.com/zeroclaw-labs/zeroclaw/issues/6378) | Discord `allowed_channels` config | v0.8.0 / later |
| [#6543](https://github.com/zeroclaw-labs/zeroclaw/issues/6543) | ACP session restore (`session/load`) | v0.8.0 candidate |
| [#6557](https://github.com/zeroclaw-labs/zeroclaw/issues/6557) | Reconcile runtime model switching with provider structure | v0.8.0 hardening |
| [#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253) | Skills support & UX (v0.7.6 theme) | v0.7.6 (underway) |
| [#6549](https://github.com/zeroclaw-labs/zeroclaw/pull/6549) | Claude Code vision input support | Branch: `master` |
| [#6555](https://github.com/zeroclaw-labs/zeroclaw/pull/6555) | RunPod ComfyUI image generation | Branch: `master` |

The **v0.8.0** line is already set: multi‑agent runtime, new env‑var grammar, and provider/config reconciliation. Meanwhile v0.7.6 seems focused on **skills** (CLI, loader, audit) as tracked in #6253. Community requests for Discord channel control, ACP session restore, and model‑switching UX will likely land in one of these two releases.

## User Feedback Summary
- **Pain Points from Bug Reports**  
  - **Discord media is completely broken** (#6556) – images never reach agent, outbound markers leak.  
  - **Tool loops with MiniMax** (#6361) – context compression drops tool calls, making multi‑turn conversations unusable.  
  - **Provider configuration gets erased** by agent actions (#6309) – frustrating for users who have fine‑tuned `schema_version=2` setups.  
  - **Windows users** still hit profile‑loading issues (#6419) even after repeated fixes.  
  - **Matrix users** cannot build the latest release (#6530) due to dependency changes.

- **Satisfaction Signals**  
  - Approval bypass (#6207) was **fixed the same day** the PR was merged – shows responsive triage.  
  - Multi‑agent runtime (#6272 / #6545) is eagerly awaited; the design discussion and merge reflect strong community engagement.  
  - The **skills documentation** (#5863, closed today) and user‑facing skills guide (#6542, merged) directly address a previously unmet need.

- **Feature Desires**  
  - Administrators want **channel‑specific Discord permissions** (#6378).  
  - Developers request **ACP session restoration** (#6543) for long‑running agent sessions.  
  - A user asked for **vision support in Claude Code** (#6549, already in PR).  
  - Homebrew users expected automatic v0.7.5 availability (#6547) – the failure indicates a release‑automation gap.

## Backlog Watch
Issues and PRs that are important, open for several days, or have received no maintainer attention:

- **[#5833 – Session ownership model for destructive operations](https://github.com/zeroclaw-labs/zeroclaw/issues/5833)**  
  Blocked, needs maintainer review. Session keys are not scoped per‑agent, allowing cross‑agent resets/deletes. A fundamental security concern.

- **[#6009 – Enrich OTel tool spans with gen_ai.tool.* attrs](https://github.com/zeroclaw-labs/zeroclaw/pull/6009)**  
  Open since April 22. Adds observability metadata. No recent activity; may conflict with v0.8.0 refactors.

- **[#6192 – Fix gateway paircode retrieval to running instance](https://github.com/zeroclaw-labs/zeroclaw/pull/6192)**  
  Open since April 28. Improves `zeroclaw gateway get-paircode` with `--port`/`--host`. Awaiting review.

- **[#6361 – context_compression drops tool calls for OpenAI‑compatible providers](https://github.com/zeroclaw-labs/zeroclaw/issues/6361)**  
  Needs maintainer review; blocked users on MiniMax. Labelled `needs-maintainer-review`.

- **[#6309 – model_routing_config stomps schema_version=2 settings](https://github.com/zeroclaw-labs/zeroclaw/issues/6309)**  
  Accepted but not assigned. Only 1 comment; high impact for users with multiple providers.

- **[#6398 – Integration/v0.8.0 (DO NOT MERGE)](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)**  
  Still open as the integration branch; intentionally blank but acts as the target for all v0.8.0 PRs.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*