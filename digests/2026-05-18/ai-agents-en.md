# OpenClaw Ecosystem Digest 2026-05-18

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-18 12:51 UTC

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

# OpenClaw Project Digest — 2026-05-18

## 1. Today's Overview
OpenClaw maintained a high-velocity pulse over the past 24 hours, with **500 issues** and **500 pull requests** updated. Community engagement remains intense — the top issue alone (#75) has 104 comments and 75 👍 reactions. Three new beta releases (v2026.5.16-beta.5 through .7) landed, focusing on dependency upgrades, Mac UI redesign, and a Docker build arg. Activity is evenly split between bug fixes (especially around message delivery, session state, and security) and feature requests spanning desktop platform support, secrets management, and multi-agent orchestration. The project shows strong health but faces growing pressure to address long-standing cross-platform gaps and stability regressions.

## 2. Releases
Three releases shipped today, all on the `2026.5.16-beta` train:

- **v2026.5.16-beta.7**: Updated `@openclaw/proxyline` to 0.3.3; bumped Pi packages to 0.75.1 and minimum Node.js to 22.19; added `OPENCLAW_IMAGE_APT_PACKAGES` Docker/Podman build arg for runtime-neutral apt package injection.
- **v2026.5.16-beta.6**: Redesigned Mac app Settings pages with consistent card layouts, cached navigation, and cleaner permissions/voice/skills/cron/exec/debug panes. Renamed repo-local Codex closeout review skill to `autoreview`.
- **v2026.5.16-beta.5**: Same changes as beta.6 (likely a duplicate entry in the release feed; no additional delta).

**Migration notes**: No breaking changes announced. Users on older Node.js (<22.19) should upgrade their runtime.

## 3. Project Progress
Today **143 PRs were merged or closed**. Notable merged/closed PRs:

- **#83571** `fix(messages): keep Codex source replies tool-gated` (closed) — preserves harness direct/source replies on message-tool delivery by default; adds opt-out with `messages.visibleReplies: "automatic"`.
- **#83587** `fix(cron): use resolveApiKeyForProvider for preflight probe auth` (closed) — cron preflight checks now send `Authorization` header, fixing spurious 401s with proxy backends like LiteLLM.
- **#83550** (open, AI-assisted) `fix(agents): skip model fallback for embedded session takeover and session write-lock errors` — reduces retry storms on `EmbeddedAttemptSessionTakeoverError` or `SessionWriteLockError`.
- **#83476** (open) `fix(codex): complete dynamic tool diagnostics` — fixes a bookkeeping gap where dynamic tool call responses weren’t emitting terminal diagnostics.

Key features advancing: native Slack plan/task-card rendering (PR #82258), Mattermost model dialog picker (#83573), subagent tool forwarding (#78441), and WhatsApp upload-file optimization (#81883).

## 4. Community Hot Topics
- **Issue #75** – “Linux/Windows Clawdbot Apps” (104 comments, 75 👍)  
  *Longest-running open issue (since Jan 1, 2026). Users urgently want desktop apps for Linux and Windows, mirroring macOS feature set.*  
  [openclaw/openclaw #75](https://github.com/openclaw/openclaw/issues/75)

- **Issue #25592** – “Text between tool calls leaks to messaging channels” (26 comments)  
  *P1 security/UX bug: internal processing output (error handling, narration) is routed to Slack/iMessage as visible messages. Highly disruptive.*  
  [openclaw/openclaw #25592](https://github.com/openclaw/openclaw/issues/25592)

- **Issue #9443** – “Request: Prebuilt Android APK releases” (24 comments)  
  *Submitted by an AI assistant on behalf of a user. Community wants compiled Android APKs in GitHub releases.*  
  [openclaw/openclaw #9443](https://github.com/openclaw/openclaw/issues/9443)

- **Issue #22676** – “Signal daemon stop() race condition on SIGUSR1 restart — orphaned processes and send failures” (17 comments)  
  *P1 bug causing process leaks and send failures during gateway restarts. Root cause: SIGTERM sent without waiting for process exit.*  
  [openclaw/openclaw #22676](https://github.com/openclaw/openclaw/issues/22676)

- **ISSUE #22438** – “feat: Tiered bootstrap file loading for progressive context control” (16 comments)  
  *Popular request to reduce token waste by loading workspace files only when needed.*  
  [openclaw/openclaw #22438](https://github.com/openclaw/openclaw/issues/22438)

## 5. Bugs & Stability
**Critical (P1, active)**:
- `#25592` – Text between tool calls leaks to messaging channels (impact: security, message loss). Fix PR #83571 addresses part of the harness path.
- `#22676` – Signal daemon restart race (orphaned processes, send failures). No fix PR yet.
- `#32296` – Agent replies to previous message due to session context confusion (12 comments). No fix PR yet.
- `#29387` – Bootstrap files in agentDir silently ignored (13 comments, 4👍). No fix PR.
- `#32473` – Control UI requires HTTPS/localhost (regression, impacts Docker users). No fix PR.
- `#31583` – `exec` tool doesn’t inherit `skills.entries.*.env` variables (regression). No fix PR.
- `#38327` – Google Vertex/Gemini 3.1 “Cannot convert undefined or null to object” in 2026.3.2 (7 comments). No fix PR.

**Recently closed**:
- Issue #71127 (*Stuck processing sessions never aborted*) was closed — likely fixed earlier.

**Stability risks**: Several P1 bugs with no linked fix PRs suggest the maintainer team is bottlenecked. The heartbeat drift fix (PR #39182) introduced a new regression (#40611) that blocks Telegram during active conversations.

## 6. Feature Requests & Roadmap Signals
Top community-wanted features:

| Feature | Issue | Votes | Likely Next Version |
|---------|-------|-------|---------------------|
| **Linux/Windows apps** | #75 | 75 👍 | Not imminent (no active PR) |
| **Masked secrets** (agents use keys without seeing them) | #10659 | 4 👍 | Possible (many security-related PRs open) |
| **Exec-approvals denylist** | #6615 | 7 👍 | High interest, could land next |
| **Direct exec mode for cron jobs** (skip LLM for simple commands) | #18160 | 9 👍 | Strong use case, but no PR yet |
| **Tiered bootstrap file loading** (#22438) | – | 0 votes but 16 comments | Good candidate for token optimization |
| **Prebuilt Android APK** | #9443 | 1 👍 | Low priority (no maintainer action) |
| **Multi-agent collaboration enhancements** (capability profiling, blackboard, token governance) | #35203 | 0 votes, 7 comments | Long-term roadmap |
| **Session snapshots** (save/load checkpoints) | #13700 | 0 votes, 6 comments | Medium-term |

**Predictions for next release**:  
- Improved secrets handling (masked secrets or env inheritance fix #31583)  
- Exec-approvals denylist or capability-based permissions (#12678)  
- Tiered bootstrap loading as part of token optimisation (#14785 mentions 3500 tok/session overhead)  

## 7. User Feedback Summary
**Pain points**:
- **Cross-platform desktop gaps**: “We have apps for macOS, iOS, and Android… Linux and Windows are missing.” (#75)  
- **Android deployment friction**: “Currently, the repository includes Android source code … but no precompiled APK.” (#9443)  
- **Telegram silent drops**: Messages processed but never sent back; no `sendMessage` logged. (#80520, fresh)  
- **Configuration surprises**: Bootstrap files in agentDir silently ignored (#29387); exec tool ignores skill-level env vars (#31583)  
- **Poor recovery**: Stuck sessions require external restart (#71127, now fixed? closed but root cause may resurface).  
- **Secrets leakage**: API keys visible to agents — “This is a significant UX problem” (#25592) and “secrets stored in .env are fully accessible” (#10659).  

**Satisfaction signals**: Users praise the “intentionally powerful” tool system (#12678) and the “most important feature” of memory persistence (#16670). The high volume of feature requests indicates active, invested user base.

## 8. Backlog Watch
Issues and PRs that have been open for long periods or need maintainer review:

| ID | Title | Created | Status | Notes |
|----|-------|---------|--------|-------|
| #75 | Linux/Windows Clawdbot Apps | 2026-01-01 | Open, needs maintainer review | 104 comments, 75👍; no PR in sight |
| #9443 | Prebuilt Android APK | 2026-02-05 | Open, needs security review | No maintainer activity since creation |
| #29387 | Bootstrap files in agentDir ignored | 2026-02-28 | Open, needs security review | 13 comments, 4👍; no fix PR |
| #25592 | Text between tool calls leaks | 2026-02-24 | Open, needs security review | P1, closed PR #83571 partially addresses |
| #22676 | Signal daemon race condition | 2026-02-21 | Open, linked PR open | No fix merged despite 17 comments |
| #32296 | Agent replies to previous message | 2026-03-02 | Open, needs live repro | 12 comments; high severity |
| #32473 | Control UI HTTPS requirement (Docker) | 2026-03-03 | Open, needs security review | 15 comments; regression |
| PR #77017 | feat(ui): add generated image actions | 2026-05-04 | Open, waiting on author | Large XL PR, needs maintainer final look |
| PR #42223 | Fix sidebar tree collapse | 2026-03-10 | Open, ready for maintainer look | XS fix, 0 comments; stuck for 2+ months |

*Maintainer bottleneck evident: many P1/P2 issues have been waiting for product decisions or security reviews since February. The project would benefit from triage prioritisation or additional maintainer bandwidth.*

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent / Personal Assistant Open-Source Ecosystem
**Date:** 2026-05-18 | **Analyst:** Senior Ecosystem Analyst

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape remains **highly active and fragmented**, with at least 10 projects showing meaningful development activity in a single 24-hour window. The ecosystem is converging around **multi-agent orchestration**, **provider flexibility**, and **cross-platform deployment**, while struggling with **stability regressions** and **maintainer bottlenecks** that slow down critical bug fixes. Community demand is strongest for **reliable core functionality** (chat, memory, tool execution) over new features, though adoption of advanced capabilities like streaming, image generation, and persistent memory is accelerating. The landscape appears to be in a **pre-consolidation phase**, where projects are differentiating on architecture (Python vs. Rust vs. Go), target user (developer vs. consumer), and deployment model (desktop app vs. Docker container vs. cloud).

---

## 2. Activity Comparison (24-hour window: 2026-05-17 to 2026-05-18)

| Project | Issues Updated | PRs Updated | Releases Today | Health Score | Notes |
|---------|---------------|-------------|----------------|--------------|-------|
| **OpenClaw** | 500 | 500 | 3 beta releases | ⚠️ Moderate | High volume but many P1 bugs unfixed; maintainer bottleneck evident |
| **Hermes Agent** | 50 | 50 | 0 | ⚠️ Moderate | v0.14.0 regressions active; strong fix velocity but new bugs appearing |
| **ZeroClaw** | 15 | 50 | 0 | ⚠️ Moderate | High PR volume; multi-agent runtime PR (#6398) blocking progress |
| **IronClaw** | 16 | 42 | 0 | ⚠️ Moderate | Reborn beta transition; crate publication blocked (0.24.0 pinned) |
| **CoPaw** | 26 | 28 | 0 | ⚠️ Moderate | High bug report activity; strong triage rate (10/26 closed) |
| **NanoBot** | 8 | 26 | 0 | ✅ Good | 11/26 PRs merged; quick turnaround on enhancement requests |
| **NanoClaw** | 8 | 29 | 0 | ✅ Good | 5 PRs merged; active community contributions |
| **PicoClaw** | 13 | 21 | 1 nightly | ✅ Good | 8 PRs merged; rapid iteration with nightly releases |
| **LobsterAI** | 0 | 17 | 0 | ✅ Good | 12/17 PRs merged; release branch consolidated |
| **Moltis** | 6 | 8 | 1 patch | ✅ High | 6/8 PRs merged; all bugs fixed same day |
| **TinyClaw** | 0 | 0 | 0 | 💤 Inactive | No activity in 24h |
| **ZeptoClaw** | 0 | 0 | 0 | 💤 Inactive | No activity in 24h |
| **NullClaw** | 2 | 0 | 0 | ⚠️ Low | Quiet phase; only 2 issues updated |
| **OpenClaw (control)** | 500 | 500 | 3 | ⚠️ Moderate | *Included as baseline* |

**Health Score Definitions:**
- **High:** All or most bugs fixed same-day; active maintainer response; low regression rate
- **Good:** Activity balanced between fixes and features; no critical unaddressed blockers
- **Moderate:** High activity but with notable open bugs, regressions, or maintainer delays
- **Low:** Low activity; unresolved bugs; risk of stagnation

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Largest community by volume** – 500+ issues/PRs/day vs. 15–50 for peers; serves as the de facto reference implementation
- **Ecosystem integration** – Proxyline, Pi packages, Docker/Podman build args indicate mature DevOps thinking
- **Most comprehensive feature surface** – Cron, secrets management, multi-agent, WhatsApp, Slack, Mattermost, Codex integration

**Technical Approach Differences:**
- **Node.js runtime** – Unusual for agent frameworks (Python dominates: NanoBot, Moltis, CoPaw; Rust: IronClaw; Go: NanoClaw)
- **Heavy reliance on tool-gated message delivery** – Unique "visibleReplies" system (PR #83571) for controlling what channels see
- **Progressive context loading** (Issue #22438) – Token-waste reduction strategy not yet seen in competitors

**Community Size Comparison:**
- Comment volume on single issue (#75): 104 comments – higher than any other project's top issue
- Reaction count (#75): 75 👍 – surpasses ZeroClaw's most-voted issue (#6059: 4 👍)
- Bug report depth: Users filing detailed reproduction steps with session logs, indicating sophisticated user base

**Weaknesses:**
- **Maintainer bottleneck** – 7+ P1 bugs with no linked fix PRs; backlog items aging since January
- **Cross-platform gaps** – Linux/Windows desktop apps missing (Issue #75, 104 comments); Android only source-code (no APK)
- **Stability regressions** – Recent fixes (heartbeat drift) introduced new bugs (Telegram blocked, #40611)
- **Secrets management gap** – Agents can read API keys from `.env` (#10659); peers like NanoBot are adding restricted mode (PR #3898)

---

## 4. Shared Technical Focus Areas

The following requirements are emerging **across multiple projects**, indicating ecosystem-wide priorities:

| Focus Area | Projects Affected | Specific Needs |
|------------|-------------------|----------------|
| **Multi-agent orchestration** | OpenClaw, ZeroClaw, Hermes, CoPaw, IronClaw | Capability profiling, blackboard communication, token governance, sub-agent tool forwarding |
| **Provider compatibility** | All projects | DeepSeek V4 thinking mode (ZeroClaw #6059, CoPaw #4051), Gemini/Kimi-code streaming issues, local model endpoints (PicoClaw #28) |
| **Memory persistence** | NanoBot, PicoClaw, Moltis, OpenClaw | Mnemon integration (#3888), Seahorse memory system (#1919), nested subfolders (#1010), session snapshots (#13700) |
| **Cross-platform deployment** | OpenClaw, PicoClaw, NullClaw, CoPaw | Linux/Windows desktop apps, Android APK, RISC-V support, Docker improvements |
| **Tool execution security** | NanoBot, OpenClaw, PicoClaw, Moltis | Restricted mode, denylist for dangerous commands, per-agent tool policies, heredoc false-positive fixes |
| **Context/token optimization** | OpenClaw, Hermes, Moltis, LobsterAI | Tiered bootstrap loading, sliding windows, session compression, per-model context sliders |
| **Secrets & auth management** | OpenClaw, CoPaw, NullClaw, ZeroClaw | Masked secrets, OAuth credential sync, plugin RCE prevention, scheduler auth for external hosts |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes | PicoClaw | NanoClaw | IronClaw | Moltis | CoPaw | ZeroClaw |
|-----------|----------|---------|--------|----------|----------|----------|--------|-------|----------|
| **Primary Language** | Node.js | Python | Python | Go | Go | Rust | Python | Python | Python |
| **Target User** | Developers, power users | Developers | DevOps, power users | Mobile/edge users | Enterprise SaaS | System integrators | Plugin devs | Consumer | Developers |
| **Deployment Model** | Desktop + Docker | CLI + Docker | CLI + Docker | Docker + nightly | Docker + SaaS | Docker + crates | Library | Desktop + Docker | CLI + Docker |
| **Key Differentiator** | Broadest feature set | Fast onboarding | Kanban orchestration | Mobile/local LLM | WhatsApp/Signal focus | TEE security | Plugin ecosystem | Visual richness | Multi-agent V3 |
| **Stability Signal** | Mixed – high bug count | Good – quick fixes | Moderate – regressions | Good – nightly cycle | Good – active merges | Moderate – crate block | High – all fixed same-day | Mixed – critical bugs | Moderate – large PR stalled |
| **Community Maturity** | Most mature | Growing rapidly | Established | Growing | Niche | Niche | Niche | Growing | Rapidly growing |

**Key Findings:**
- **OpenClaw** is the **broadest but most stretched** – no single area where it dominates peers technically
- **Moltis** has the **best stability record** – all 5 bugs reported today were fixed same-day
- **NanoBot** shows **best balance of new features + stability** – 11 PRs merged, only 2 critical bugs open
- **ZeroClaw** is the **most ambitious** architecturally (multi-agent Schema V3) but carries highest risk (153 commits lost in revert)
- **IronClaw** is the **most differentiated** technically (Rust, TEE, WASM runtime) but crate publication blockage stifles adoption

---

## 6. Community Momentum & Maturity

**Activity Tiers (by 24h issue+PR volume):**

| Tier | Projects | Characteristics |
|------|----------|-----------------|
| **High Velocity** (51+ updates) | OpenClaw (1000), Hermes (100), ZeroClaw (65) | Massive activity; both features and bugs; risk of maintainer burnout |
| **Medium Velocity** (10–50 updates) | IronClaw (58), CoPaw (54), NanoBot (34), NanoClaw (37), PicoClaw (34), LobsterAI (17) | Healthy balance; reviewing at sustainable pace |
| **Low Velocity** (1–9 updates) | Moltis (14), NullClaw (2) | Stable or quiet period; may indicate maturity or neglect |
| **Inactive** (0 updates) | TinyClaw, ZeptoClaw | No recent development; risk of abandonment |

**Stabilizing Projects:**
- **Moltis** – High stability, low bug count, patches shipped regularly → likely entering maintenance mode
- **NullClaw** – Only 2 updates; may be stable or unmaintained (scheduler bug #915 unresolved)

**Rapidly Iterating Projects:**
- **ZeroClaw** – v0.8.0 multi-agent runtime in review; high PR volume suggests major release imminent
- **IronClaw** – Reborn WebUI beta transitioning; crate publication is critical blocker
- **PicoClaw** – Nightly releases + 8 PRs merged/day indicate fast iteration cycle

---

## 7. Trend Signals

### Industry Trends Extracted from Community Feedback

**1. The "Provider Matrix" Problem is Unsolved**
Every project struggles with provider-specific API quirks: DeepSeek thinking mode, Gemini streaming, Kimi-code reasoning_content, Xiaomi Mimo format mismatch. This is the **#1 cause of user frustration** across the ecosystem. *Signal: A universal provider abstraction layer (like LiteLLM) is becoming a prerequisite, not a differentiator.*

**2. Multi-Agent is the Next Frontier, but Immature**
Three projects (OpenClaw, ZeroClaw, Hermes) are actively building multi-agent runtimes. Yet most implementations are **pre-beta** – token governance, capability profiling, and blackboard communication are mentioned but not shipped. *Signal: Early adopters will tolerate instability for multi-agent features, but production readiness is 6–12 months away.*

**3. Memory Persistence is Table Stakes**
Users across NanoBot (#3888), PicoClaw (#1919), OpenClaw (#16670), and Moltis (#1010) explicitly demand persistent, configurable memory. The "context loss across sessions" pain point is universal. *Signal: Projects without memory systems (NullClaw, TinyClaw) risk obsolescence.*

**4. Cross-Platform Gaps Create Market Opportunity**
OpenClaw's Linux/Windows desktop gap (#75 – highest-voted issue in ecosystem) and Android APK demand (#9443) show **massive unmet demand** for desktop and mobile client apps. PicoClaw's mobile focus and nightly releases position it well. *Signal: A project that ships polished Linux/Windows/Android clients could capture significant share.*

**5. Security is Becoming a Differentiator**
NanoBot's restricted mode (#3898), OpenClaw's masked secrets (#10659), and CoPaw's RCE vulnerability (#4470) highlight growing security awareness. Users are moving beyond "does it work?" to "can it be safely used?" *Signal: Security features (tool denylists, credential isolation, plugin sandboxing) will become selection criteria.*

**6. Developer Experience > Feature Count**
Projects with fast bug fix turnaround (Moltis: same-day fixes; NanoBot: 11/26 PRs merged) earn user trust despite smaller feature sets. Projects with high bug counts and slow fixes (OpenClaw: 7 P1s unfixed) see frustrated users despite broadest features. *Signal: The ecosystem is maturing – reliability now trumps novelty for most users.*

### Value for AI Agent Developers

- **If building a production system today:** Moltis or NanoBot offer the best stability-to-feature ratio
- **If exploring multi-agent architectures:** ZeroClaw's v0.8.0 (if it ships) and OpenClaw's sub-agent forwarding are reference implementations
- **If targeting mobile/edge:** PicoClaw's Go stack and nightly releases are worth evaluating
- **If security is paramount:** IronClaw's TEE support and NanoBot's restricted mode are leading, though both are early
- **If contributing to the ecosystem:** The provider compatibility layer and cross-platform client gaps present the highest-impact contribution opportunities

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-18

## Today’s Overview

Project activity remains high, with 8 issues updated and 26 PRs updated in the last 24 hours. The community is actively contributing both bug fixes and new features, resulting in 11 merged/closed PRs. No new releases were published, but the codebase is evolving rapidly, with major refactors (e.g., `AgentRunner.run()` decomposition) and new provider support (Gemini, MiniMax, Manifest). While most bugs are being addressed promptly, a few critical WebUI and WeChat login issues remain open, signalling ongoing stability work.

## Releases

None.

## Project Progress

**Merged/closed PRs today (11 total)** — key highlights:

- **Image Generation Providers**: Two new providers shipped: [MiniMax](https://github.com/HKUDS/nanobot/pull/3879) (`image-01` model) and [Gemini](https://github.com/HKUDS/nanobot/pull/3886) (Imagen 4 & Gemini Flash). Both enable text-to-image and reference image support.
- **CLI Improvements**: [Model Preset wizard](https://github.com/HKUDS/nanobot/pull/3890) added to `nanobot onboard`; [model configuration commands](https://github.com/HKUDS/nanobot/pull/3883) (though later closed as invalid, indicating scope refinement).
- **WebUI Fixes**: [Markdown rendering](https://github.com/HKUDS/nanobot/pull/3889) now preserves single newlines (important for `/help` output); [Docker deployment docs](https://github.com/HKUDS/nanobot/pull/3875) updated to fix WebUI and `bwrap` sandbox issues (resolves #3873).
- **WeChat Protocol**: [Upgrade to `openclaw-weixin` v2.x](https://github.com/HKUDS/nanobot/issues/3882) closed as an issue (likely merged via separate PR not listed).
- **Memory/ECM**: [#3888](https://github.com/HKUDS/nanobot/issues/3888) introduced **Mnemon** integration for persistent agent memory (closed as enhancement).

## Community Hot Topics

- [#3790 – WebUI Sessions Display Corruption](https://github.com/HKUDS/nanobot/issues/3790) (14 comments, open)  
  Users report that after updating to the latest v0.1.5.post3.2026.05.13, printed session content becomes garbled until manual refresh. This is the most commented issue, indicating a high-impact UI regression.
- [#3863 – WeChat Cannot Login](https://github.com/HKUDS/nanobot/issues/3863) (5 comments, open)  
  WeChat scan shows “your WeChat version is too low”, even after upgrading to latest. Points to an underlying protocol mismatch.
- [#3888 – Persistent Memory with Mnemon](https://github.com/HKUDS/nanobot/issues/3888) (1 comment, closed)  
  Community-driven integration that solves a long-standing pain point: context loss across sessions. The quick close suggests it was well-received and merged.

**Underlying needs**: Users are demanding stable core features (WebUI, WeChat, Docker) while eagerly adopting new capabilities like persistent memory and image generation.

## Bugs & Stability

| Bug | Severity | Status | Fix PR? |
|-----|----------|--------|---------|
| [#3790](https://github.com/HKUDS/nanobot/issues/3790) WebUI display corruption | **High** – renders UI unusable | Open | No linked PR; workaround is page refresh |
| [#3863](https://github.com/HKUDS/nanobot/issues/3863) WeChat login failure | **High** – channel unusable | Open | No linked PR; likely related to [#3882](https://github.com/HKUDS/nanobot/issues/3882) (upgrade to openclaw v2.x, closed) |
| [#3884](https://github.com/HKUDS/nanobot/issues/3884) WebUI conversation closes after first response | **Medium** – session broken | Open | No linked PR |
| [#3873](https://github.com/HKUDS/nanobot/issues/3873) Docker deployment docs inconsistencies | **Medium** – blocked deployment | Closed | Fixed by [#3875](https://github.com/HKUDS/nanobot/pull/3875) |

**Additional**: [#3882](https://github.com/HKUDS/nanobot/issues/3882) (WeChat protocol upgrade) closed, likely addressing #3863 partially. No critical security bugs reported.

## Feature Requests & Roadmap Signals

**User-requested enhancements (open):**
- [#3885](https://github.com/HKUDS/nanobot/issues/3885) – Global switch to disable Dream system jobs (memory tasks). High demand for configurability.
- [#3887](https://github.com/HKUDS/nanobot/issues/3887) – User authorization mechanism for dangerous commands (`exec` tool). Addresses safety usability gap.

**Trending PRs (open) that hint at next version features:**
- **Restricted Mode** ([#3898](https://github.com/HKUDS/nanobot/pull/3898)) – Adds tool isolation based on user privilege (sender_id/is_privileged). Could land next.
- **Skill Load Tool** ([#3847](https://github.com/HKUDS/nanobot/pull/3847)) – Persists skill content across multi-turn conversations, solving a critical bug.
- **Signal Channel** ([#3852](https://github.com/HKUDS/nanobot/pull/3852)) – New chat platform integration (signal-cli).
- **Provider Registry for Image Generation** ([#3893](https://github.com/HKUDS/nanobot/pull/3893)) – Refactor to reduce boilerplate when adding new providers.

**Predictions**: The next release (v0.2.x) will likely include restricted mode, the skill-load tool, and at least one of the image generation providers already merged.

## User Feedback Summary

- **Pain points**: WebUI display corruption and WeChat login failures are the most acute; both degrade core experiences. Docker deployment docs inconsistencies also frustrated users (now fixed).
- **Unmet needs**: Users want granular control over system jobs (Dream) and safe override of dangerous command guards. The warm reception of Mnemon (persistent memory) shows strong desire for long-term context.
- **Satisfaction indicators**: Quick closure of enhancement requests (e.g., #3888, #3882) and merged PRs for new providers suggest active maintainer responsiveness. However, open high-severity bugs without linked fixes may erode confidence.

## Backlog Watch

Unanswered or long-open items needing maintainer attention:

- [#2060](https://github.com/HKUDS/nanobot/pull/2060) (PR, opened March 15) – `shell tool` allowing configurable paths when `restrict_to_workspace=True`. Still open after 2+ months; may have been superseded by restricted mode PR #3898.
- [#2867](https://github.com/HKUDS/nanobot/pull/2867) (PR, opened April 6) – Telegram group allowlist, fallback agents, and thought-tag fixes. Open with no recent activity.
- [#3568](https://github.com/HKUDS/nanobot/pull/3568) (PR, opened April 30) – Manifest LLM router support. Needs review.
- [#3762](https://github.com/HKUDS/nanobot/pull/3762) (PR, opened May 12) – Codex provider retry blank failures. No recent comments.
- [#3790](https://github.com/HKUDS/nanobot/issues/3790) (issue, opened May 14) – WebUI corruption, highest-comment issue, no fix yet.

**Recommendation**: Prioritise #3790 and #3863 – both break fundamental user-facing features. Review #2060 and #2867 for possible closure or progress.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-18

## 1. Today’s Overview
Hermes Agent saw very high activity, with 50 issues and 50 pull requests updated in the past 24 hours. The community is actively reporting bugs and proposing features, while maintainers merged 11 PRs and closed 5 issues. Key areas of focus include gateway stability (Telegram, Discord), Kanban worker orchestration, provider-specific issues (Gemini, OpenAI Codex, MiniMax/DeepSeek), and the TUI/Dashboard UX. The project remains in a healthy, fast-moving state, though several critical bugs (P1) demand immediate attention.

---

## 2. Releases
*No new releases today.* The latest tagged version remains `v0.14.0 (2026-05-16)`.

---

## 3. Project Progress
**Merged/closed PRs today (11 total; notable examples from data):**

- **#27981** – *docs: add Korean writing editor skill* (closed)  
- **#27971** – *fix(tui): keep /goal verdict out of compact status row* (closed) – Prevents long judge verdicts from cluttering the status bar.  
- **#27969** – *feat(discord): allow opt-in auto-threading for free-response channels* (closed) – Solves a long-standing tension between free‑response and threading.  
- **#27956** – *feat: add parallel agent pair workflow skill* (closed) – New orchestration pattern for heavy tasks using Claude Code and Codex.

**Other merged/closed PRs (not in top‑20 but mentioned in issues):**  
- Fixes for Kanban scroll (#27982), Honcho peer‑card read/write (#27979), and Telegram audio handling (#24883) are still **open** but actively iterated.

**Closed issues today (5):**  
- **#27339** – *Prompt Cache invalidation due to dynamic tool shuffling* (P2, bug fixed).  
- **#27826** – *Bootstrap consolidation: pip/uvx browser setup broken + Windows dep_ensure missing* (P2).  
- **#25836** – *Telegram typing indicator drops mid‑response* (P2).  
- **#26388** – *Codex usage_limit_reached 429 retries exhausted pool credential once before rotating* (P2).  

These closures reflect steady progress on both user‑reported regressions and infrastructure bugs.

---

## 4. Community Hot Topics
**Most active issues (by comment count):**

- **[#15895] (14 comments)** – `[type/bug, comp/cli, provider/gemini, P3]` – *google-gemini-cli causing 429 but gquota ok*  
  → User sees HTTP 429 despite quota appearing healthy; root cause unclear. High engagement suggests many users face similar Gemini‑CLI auth issues.  
  [NousResearch/hermes-agent Issue #15895](https://github.com/NousResearch/hermes-agent/issues/15895)

- **[#27339] (6 comments, closed today)** – Prompt cache invalidation with dynamic tool shuffling – Already fixed; but the discussion highlighted broader concerns about KV‑cache stability with streaming backends.

- **[#20500] (5 comments)** – *Dashboard Chat tab fails with EACCES in Docker* – Permission issue in official Docker image; maintainers have acknowledged.  
  [NousResearch/hermes-agent Issue #20500](https://github.com/NousResearch/hermes-agent/issues/20500)

- **[#12058] (5 comments)** – *OpenAI Codex OAuth works in CLI, but Telegram gateway replies “No Codex credentials stored”* – Gateway‑specific auth desync affects Telegram users.  
  [NousResearch/hermes-agent Issue #12058](https://github.com/NousResearch/hermes-agent/issues/12058)

- **[#26241] (4 comments)** – *Mirror web/browser plugin migration for FAL image generation backend* – Architecture improvement to move FAL into its own plugin; aligns with recent refactoring trend.  
  [NousResearch/hermes-agent Issue #26241](https://github.com/NousResearch/hermes-agent/issues/26241)

**Most reacted issues:** #15895 (👍 3) leads; other issues have 0–1 reactions, indicating focused technical discussion rather than widespread outcry.

---

## 5. Bugs & Stability
**Critical (P1) bugs reported or updated today:**

- **#27370** – *NameError: ‘_pool_may_recover_from_rate_limit’ not defined in conversation_loop.py*  
  v0.14.0 regression; rate‑limit fallback calls undefined function. **No fix PR yet.**  
  [NousResearch/hermes-agent Issue #27370](https://github.com/NousResearch/hermes-agent/issues/27370)

- **#27881** – *Discord Gateway: Premature conversation turn termination during autonomous workflows*  
  Agent stops mid‑task in Discord, delivering partial responses. **No fix PR.**  
  [NousResearch/hermes-agent Issue #27881](https://github.com/NousResearch/hermes-agent/issues/27881)

- **#27856** – *Gateway restart can lose long‑running sessions during shutdown drain*  
  Sessions may be lost if process is killed while waiting for agents to drain. **No fix PR.**  
  [NousResearch/hermes-agent Issue #27856](https://github.com/NousResearch/hermes-agent/issues/27856)

- **#27938** – *hermes_cli.proxy missing from wheel – ModuleNotFoundError on `hermes proxy`*  
  v0.14.0 wheel missing the proxy subpackage. **No fix PR yet.**  
  [NousResearch/hermes-agent Issue #27938](https://github.com/NousResearch/hermes-agent/issues/27938)

**High‑severity (P2) bugs reported today:**

- **#27970** – *Telegram auto voice replies fall back to MP3 attachments / silent final notifications* – Voice reply quality regression.  
- **#27834** – *MiniMax/DeepSeek V4 XML tool calls rendered as text instead of executed* – Affects Web UI and gateway.
- **#27942** – *Telegram group edit streaming leaves final replies visibly unfinished* – Saved session shows complete answer, but Telegram message truncates.
- **#27924** – *Clean‑exit protocol violation blocks downstream pipeline tasks when workers complete silently* – Kanban pipeline deadlock.

**Stability notes:** Several long‑standing issues (#5326 – Gateway crash with `UnboundLocalError`, #25666 – Telegram SIGSEGV on Raspberry Pi) remain open but were not updated today. The high number of P1/P2 bugs filed today suggests the v0.14.0 release introduced regressions, especially around gateway edge cases and build packaging.

---

## 6. Feature Requests & Roadmap Signals
**Notable feature issues/PRs submitted or updated today:**

- **#27977** – *feat(auxiliary): add enabled toggle for individual auxiliary tasks* – Lets users disable failing auxiliary tasks (e.g., compression) via config; addresses a common annoyance.  
- **#26897** – *feat: support per‑task Kanban model overrides* – Allows overriding the worker model per Kanban task via CLI `--model`.  
- **#27954** – *feat(memory): add governance executor* – Adds `hermes memory governance` for cleanup orchestration and health smoke tests.  
- **#27978** – *feat(simplex): groups, native attachments, text batching, auto‑accept* – Major extension of the SimpleX Chat plugin.  
- **#27976** – *chore(agent): raise default iteration budget to 150* – Proposes increasing default tool‑call limit from 90 to 150; likely bundled into next patch.

**Feature requests from community:**  
- **#27953** – *Add delete session button in Web Dashboard* (P3, likely next UI iteration).  
- **#17790** – *Make Discord voice inactivity timeout configurable* (open since Apr 30).  
- **#27855** – *Optimize full‑history reprocessing per turn* (sliding window / incremental context).  

**Prediction for next version (v0.14.1 or v0.15.0):**  
- Per‑task Kanban model overrides (#26897) and the `auxiliary.enabled` toggle (#27977) are low‑risk, high‑value features that may ship soon.  
- Memory governance and the iteration budget change require more testing and could appear in a minor release.

---

## 7. User Feedback Summary
**Real pain points reported today:**

- **Rate limiting confusion:** User `herbalizer404` – *“Despite I have last Hermes update and gemini ai pro with full quotas … I encounter 429”* – suggests quota tracking discrepancies.  
- **Docker permission issues:** `jbellsolutions` – Dashboard chat tab fails with `EACCES` because `ui-tui` is root‑owned.  
- **Telegram quality regressions:** `andrepia` – *“auto voice replies can fail … fall back to MP3 attachment … final voice reply can arrive silently instead of spoken.”*  
- **Kanban worker deadlocks:** `AI-OWEN` – *“clean‑exit protocol violation blocks downstream pipeline tasks when workers complete silently.”*  
- **Incomplete replies:** `barronlroth` – *“Telegram group edit streaming can leave final replies visibly unfinished even though the model/session transcript contains the complete final answer.”*  
- **Missing wheel components:** `alphanury` – `hermes proxy` fails with `ModuleNotFoundError` because the subpackage is not in the wheel; affects all pip/uvx installs.

**Satisfaction signals:** Active contribution of new skills (Korean writing editor, changelog-gen, prompt-crafter) and plugin improvements (SimpleX, TrustedRouter.com provider) indicate the ecosystem is thriving.

---

## 8. Backlog Watch
**Issues that have been open longer than two weeks without a maintainer resolution (P1/P2):**

- **#5326** (P1, opened Apr 5) – *Gateway crash with UnboundLocalError on message after smart model routing change*  
  Still open; users report it affects Discord and Telegram. No linked PR.  
  [NousResearch/hermes-agent Issue #5326](https://github.com/NousResearch/hermes-agent/issues/5326)

- **#12058** (P2, opened Apr 18) – *OpenAI Codex OAuth works in CLI, but Telegram gateway replies “No Codex credentials stored”*  
  No maintainer comment since Apr 24. Affects Telegram users relying on Codex.  
  [NousResearch/hermes-agent Issue #12058](https://github.com/NousResearch/hermes-agent/issues/12058)

- **#15895** (P3, opened Apr 26) – *google-gemini-cli 429 despite quota OK* – High community engagement (14 comments) but still triaged as P3. May need reprioritization.

- **#20500** (P2, opened May 6) – *Docker Dashboard EACCES* – Acknowledged but no fix merged.  
- **#25666** (P2, opened May 14) – *Telegram SIGSEGV on Raspberry Pi aarch64* – No fix yet; impacts multiple Pi users.

**PRs needing attention:**  
- #24090 (PR for Kanban policy audit, open since May 12) – No recent maintainer review.  
- #24217 (PR for spaced MEDIA paths, open since May 12) – Addresses a long‑standing file‑path bug.

*Note: The high number of issues created today suggests that maintainer response time will be critical in the next 48 hours to prevent backlog bloat.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# Project Digest: PicoClaw (sipeed/picoclaw)
**Date:** 2026-05-18  
**Data Window:** Issues and PRs updated in the last 24 hours

---

## 📈 Today's Overview

PicoClaw shows **high development velocity** today with 13 issues updated (5 still open), 21 PRs updated (12 open), and a new nightly release. The community remains very active—several enhancement discussions have attracted double-digit comments, signaling growing adoption and diverse use cases. The project is clearly in a phase of rapid iteration, with multiple large feature PRs (streaming, provider additions, channel refactoring) converging simultaneously. While the nightly build is marked as potentially unstable, the overall signal is healthy: bugs are being closed quickly, and feature requests are being addressed.

---

## 📦 Releases

### **v0.2.8-nightly.20260518.0df050ff** (Nightly Build)

This is an automated nightly build targeting **v0.2.8** (based on main branch as of today).  
- **Nature:** Unstable, use for testing only.  
- **Full Changelog:** [v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
- No breaking changes or migration notes were provided.

---

## 🚀 Project Progress (Merged/Closed PRs Today)

**8 PRs were merged/closed in the last 24 hours**, reflecting active bugfixing and feature delivery:

| PR | Domain | Description |
|----|--------|-------------|
| [#2885](https://github.com/sipeed/picoclaw/pull/2885) | Provider | **Added SiliconFlow as a first-class provider** (OpenAI-compatible) – closes #2884 |
| [#2886](https://github.com/sipeed/picoclaw/pull/2886) | Web UI | **Chat detail visibility selector** – four-state toggle for reasoning/tool calls |
| [#2882](https://github.com/sipeed/picoclaw/pull/2882) | Web UI | **Code block copy & collapse controls** + JSON highlighting for tool arguments |
| [#2836](https://github.com/sipeed/picoclaw/pull/2836) | Security | **PowerShell encoding bypass prevention** via iex injection |
| [#2879](https://github.com/sipeed/picoclaw/pull/2879) | Config | **Fixed `load_image` tool configurability** in `config.json` (#2878) |
| [#2833](https://github.com/sipeed/picoclaw/pull/2833) | API/Web | **Real connectivity test** for model configurations (part of UI workflow #2752) |
| [#2752](https://github.com/sipeed/picoclaw/pull/2752) | Config/UI | **Model configuration workflow overhaul** – upstream model fetching, provider-aware validation, connectivity test |
| [#2889](https://github.com/sipeed/picoclaw/pull/2889) | Docs | **Updated WeChat QR code** |

---

## 🔥 Community Hot Topics

### Most Active Issues (by comments/reactions)

1. **[#28 – Feat Request: LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28)**  
   **19 comments, 2 👍** — Created Feb 2026, still open.  
   User requests a simple way to connect to LM Studio, especially on Android. The high engagement signals a strong demand for local model providers on mobile.

2. **[#1042 – [BUG] exec工具guardCommand方法问题](https://github.com/sipeed/picoclaw/issues/1042)**  
   **12 comments, 2 👍** — Created Mar 2026, still open.  
   A safety guard false-positive that blocks valid `curl` commands (e.g., weather queries) due to overly strict relative-path regex. Affects many tool users.

3. **[#1919 – [Feature] Seahorse Memory System](https://github.com/sipeed/picoclaw/issues/1919)**  
   **11 comments, 0 👍** — Closed today after discussion.  
   Biologically-inspired memory system proposal. Closed likely because implementation PRs have started (see [#2759](https://github.com/sipeed/picoclaw/pull/2759)).

4. **[#2225 – [Feature] Ollama Cloud Credentials](https://github.com/sipeed/picoclaw/issues/2225)**  
   **12 comments** — Closed today.  
   User needed credential support for Ollama Cloud. Resolution indicates provider flexibility is being improved.

### Underlying Needs
- **Mobile/local LLM access** (#28)  
- **Better tool path safety** (#1042)  
- **Memory persistence** (Seahorse #1919)  
- **Cloud provider credential management** (#2225)

---

## 🐞 Bugs & Stability

### Bugs Reported Today (last 24h)

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) | **Critical** | `.deb` on **RISC-V** architecture fails with OpenAI model. User reports `gpt-5.4-2026-03-05` non-functional on Debian GNU/Linux RISC-V. | ❌ None yet |
| [#2839](https://github.com/sipeed/picoclaw/issues/2839) | **Medium** | Steering chain final replies edit placeholder messages instead of sending new messages on channels that use tool-feedback editing. | ❌ Open |
| [#2878](https://github.com/sipeed/picoclaw/issues/2878) | **Medium** | `load_image` tool not configurable in `config.json` — fixed by [#2879](https://github.com/sipeed/picoclaw/pull/2879) (merged) | ✅ Merged |

### Recently Fixed Bugs
- [#2749](https://github.com/sipeed/picoclaw/issues/2749) – Bash evaluating relative paths as absolute (closed)  
- [#2745](https://github.com/sipeed/picoclaw/issues/2745) – OpenRouter reasoning leak (closed)  
- [#1297](https://github.com/sipeed/picoclaw/issues/1297) – Light model routing mismatch (closed)

**Verdict:** The RISC-V issue is the most critical open bug; all other recent bugs have been addressed quickly.

---

## 💡 Feature Requests & Roadmap Signals

### Requests with Active PRs (likely in next version)

- **Streaming support** — [#2892](https://github.com/sipeed/picoclaw/pull/2892) (open) adds configuration-driven provider streaming with dual opt-in model/channel.  
- **Per-request MCP headers** — [#2696](https://github.com/sipeed/picoclaw/pull/2696) (open) allows channels to forward dynamic headers to MCP servers.  
- **Chat stream over WebSocket** — [#2853](https://github.com/sipeed/picoclaw/pull/2853) (open) adds `ChatStream` support to the pico channel.  
- **Factory reset** — [#2891](https://github.com/sipeed/picoclaw/pull/2891) (open) provides recovery path for broken configs.  
- **Agent tool policy filters** — [#2838](https://github.com/sipeed/picoclaw/pull/2838) (stale, open) adds `allow/deny` glob patterns in `AGENT.md` frontmatter.

### Other Notable Requests
- [#2837](https://github.com/sipeed/picoclaw/issues/2837) – Tool policies in `AGENT.md` frontmatter (open, related to #2838).  
- [#28](https://github.com/sipeed/picoclaw/issues/28) – LM Studio easy connect (still open, no PR yet).  
- [#2546](https://github.com/sipeed/picoclaw/issues/2546) – OAuth 2.1 + PKCE for MCP servers (closed, but indicates future dashboard integration interest).

**Prediction:** The next release (v0.2.8 or v0.3.0) will likely include **streaming**, **SiliconFlow provider**, **MCP per-request headers**, and **factory reset**.

---

## 🗣️ User Feedback Summary

- **Pain Points:**  
  - RISC-V platform not working with OpenAI models (#2887) – likely architectural issue.  
  - LM Studio connectivity remains difficult for non-technical users (#28).  
  - Tool safety guard blocks legitimate commands (#1042).  
  - Reasoning models leak thinking into responses (#2745, fixed).  
  - Config file `load_image` not toggleable (#2878, fixed).

- **Use Cases:**  
  - Cloud LLM access (Ollama cloud, SiliconFlow) – users want first-class provider support.  
  - Multi-agent setups with per-agent tool restrictions (#2837).  
  - Mobile/Android deployment (#28).  
  - MCP server integration with OAuth (#2546).

- **Satisfaction Signals:**  
  Quick turnaround on bugs (e.g., #2878 fixed same day, #2225, #2745 closed).  
  Community contributions are being merged regularly (8 PRs today).  
  Users are actively discussing advanced features (Seahorse memory system).

---

## ⏰ Backlog Watch

| Item | Days Since Last Update | Status | Concern |
|------|-----------------------|--------|---------|
| [#28](https://github.com/sipeed/picoclaw/issues/28) – LM Studio Easy Connect | ~96 days (created Feb 11) | Open, 19 comments | High demand, no assignee, no PR. Community may benefit from a maintainer response or acceptance of contributions. |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) – exec guardCommand false positives | ~75 days (created Mar 4) | Open, 12 comments | Long-standing bug affecting many users; no fix PR yet. |
| [#2837](https://github.com/sipeed/picoclaw/issues/2837) – Frontmatter tool policies | 9 days (May 9) | Open, related PR #2838 stale | Should be reviewed as part of multi-agent improvements. |
| [#2839](https://github.com/sipeed/picoclaw/issues/2839) – Steering chain reply editing | 9 days (May 9) | Open | Medium severity, no fix yet. |

**Maintainer Attention Needed:** Especially [#28](https://github.com/sipeed/picoclaw/issues/28) and [#1042](https://github.com/sipeed/picoclaw/issues/1042) have been open for months with high community engagement. A maintainer response or assignment would be valuable.

---

*Generated from public GitHub data for `sipeed/picoclaw`. All links point to the original issues/PRs.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-18

*Generated from GitHub activity data (issues, PRs, releases) for nanocoai/nanoclaw*

---

## 1. Today's Overview

The NanoClaw project is experiencing **high activity** with 8 issues and 29 pull requests updated in the last 24 hours. Several important bugs were reported and are being actively addressed—many have fix PRs already in review. The community is engaged around **WhatsApp integration**, **Signal media handling**, **group management**, and **provider flexibility**. No new releases were cut today, but multiple fixes are queued for the next patch. Project health is strong, with maintainers and contributors collaborating across a wide range of areas from CLI fixes to new features like video generation and CalDAV tooling.

---

## 2. Releases

**No new releases today.**

The last release (v2.0.64) is being documented by a pending PR (#2536). Users should expect a new patch release soon incorporating the fixes merged today, notably the session container status reconciliation (#2533) and the pre-commit hooks CI (#1874, #2537).

---

## 3. Project Progress

**Merged/closed PRs today (5 items):**

- **#867** — Fix: allow scheduled-task agents to `send_message` to their task output JID (swarm/coordinator routing). Merged after a long review period.
- **#2375** — Fix: exclude per-thread sessions from agent-shared lookup. Prevents Signal DMs from being incorrectly routed into active GitHub PR sessions. **Merged.**
- **#1874** — Chore: add pre-commit hooks (prettier, eslint, typecheck, vitest). This is the first step of a planned CI improvement; a newer PR (#2537) refines it. **Merged.**
- **#2376** — Docs: warn against using `agent-shared` with per-thread channels (e.g., GitHub). **Merged.**
- **#2533** — Issue closed: stale `sessions.container_status` after deploy/service restarts. Root cause identified; fix likely in a subsequent PR.

**Closed issue (1 item):**  
- **#2533** (mentioned above) – reconciliation of stale session container status. The problem was observed on `shapiroserver2` and has been fixed.

**What advanced:**  
The project consolidated several session routing and container lifecycle fixes, added developer tooling (pre-commit hooks), and improved documentation for channel isolation.

---

## 4. Community Hot Topics

### Most Active Issue  
**#1984** — *Provider support for custom/local OpenAI-compat endpoints (Codex + OpenCode)*  
- **6 comments**, 0 reactions  
- Created 2026-04-24, still open  
- **URL:** [#1984](https://github.com/nanocoai/nanoclaw/issues/1984)  

The community is asking for a reliable way to use self-hosted or custom endpoints with NanoClaw's provider integrations. Despite the skill documentation mentioning "experimental" support for BYO endpoints, practical routing doesn't work. This is a significant barrier for users who want to use local models or proxy endpoints. The long comment thread suggests this is a **high-priority feature request** that may influence provider architecture in the next milestone.

### Other Active Discussions  
- **#2525** (Bug: `ncl groups delete` fails with FOREIGN KEY constraint) – received 1 comment and a quick fix PR (#2526).  
- **#2386** (UUID generation violates OneCLI identifier rules) – ongoing since May 10, 1 comment.  
- **#2415** (`ncl groups create` skips `container_configs` row) – open since May 11, 1 comment.  

---

## 5. Bugs & Stability

### High Severity  
- **#2525** — `ncl groups delete` fails with `FOREIGN KEY constraint failed` on any non-trivial group.  
  🔧 Fix PR **#2526** exists (cascading delete). **Critical** for any group management workflow.  
- **#2535** — WhatsApp group messages appear as "Waiting for this message" (LID encryption desync).  
  ⚠️ No fix PR yet. Blocks WhatsApp group functionality.  

### Medium Severity  
- **#2528** — Signal channel: image/PDF attachments unreachable from agent container. Media staged to host directory but not mounted into container's workspace.  
  🔧 No dedicated fix PR yet; likely depends on shared session inbox routing.  
- **#2522** — `transformOutboundText` skipped on `ask_question` and `card` paths → approval cards fail to deliver on Telegram.  
  🔧 No fix PR yet. Affects structured message delivery.  
- **#2415** — `ncl groups create` skips `container_configs` insertion, leading to "Container config not found" on first spawn.  
  🔧 No fix PR yet; requires extension of the CLI group creation logic.  

### Low Severity (new today)  
- **#2386** — UUIDs generated by `ncl groups create` violate OneCLI identifier rules (dashes, uppercase). Workaround exists but UX impact is low.  

### Fixed/Closed Today  
- **#2533** (stale container_status) – closed after investigation.  

---

## 6. Feature Requests & Roadmap Signals

### Strong Community Demand  
- **Custom/local API endpoints** (#1984) – likely to be addressed in a provider abstraction overhaul.  
- **Per-agent provider & model configuration** (PR #1968) – a large chain of commits aiming for first-class, chat-driveable provider selection per session. This is a major roadmap item.  

### New Skills & Integrations  
- **Veo 3.1 video generation** (PR #2532) – Edna agent can now generate, extend, and stitch videos via Google's Gemini API. A clear sign of expanding Edna's creative capabilities.  
- **CalDAV tool** (PR #2530) – adds calendar access for agents.  
- **Whisper voice transcription** (PR #2317) – free, local voice transcription skill (openai-whisper / whisper.cpp).  
- **GitHub polling mode** (PR #2301) – no-port-required GitHub integration for NAT/firewall environments.  

### Predictions for Next Version  
The next release (v2.0.65) is likely to include:  
- The `ncl groups delete` fix (#2526)  
- The session routing fix (#2375, already merged)  
- The stale container_status fix (closed #2533)  
- Possibly the Codex auth bind-mount fix (#2534)  
- Changelog entry for v2.0.64 (PR #2536)  
- The `agent-groups` cascading delete and `container_configs` fix might slip to a subsequent patch unless merged soon.  

---

## 7. User Feedback Summary

**Pain points (explicit in issues):**  
1. **WhatsApp group incompatibility** – Messages from group members are encrypted in a way that NanoClaw cannot decode; bot sees "Waiting for this message". High frustration for WhatsApp-first users.  
2. **Signal media inaccessibility** – Images/PDFs are stored on host but not mounted into agent containers, making them unusable. Blocks common use cases like "look at this image".  
3. **Group management CLI broken** – Deleting a group fails with foreign key error; creating a group leaves out `container_configs` → first spawn fails. Basic administration is unreliable.  
4. **Telegram approval cards broken** – Markdown sanitization not applied to card/ask_question paths, causing cards to fail silently.  
5. **Session routing confusion** – Agents with both shared and per-thread channels can misroute messages to the wrong session (PR #2375 fixes this, now merged).  

**Satisfaction signals:**  
- Quick turnaround on reported bugs: e.g., #2525 got a fix PR the same day.  
- Active PR review and merging on long-standing PRs (#867, #1874).  
- Community contributors (glifocat, IamAdamJowett, cfis, nightlaro) are actively pushing features and fixes – a sign of a healthy ecosystem.  
- Pre-commit hooks added to improve code quality and contributor experience (welcomed by developers).  

---

## 8. Backlog Watch

Issues and PRs that are **long-unanswered or appear stuck** and need maintainer attention:

| Item | Created | Last Activity | Status | Notes |
|------|---------|---------------|--------|-------|
| **#2386** – `ncl groups create` UUID violates OneCLI rules | 2026-05-10 | 2026-05-17 | Open, 1 comment | No PR yet. Simple fix (change ID generation) but no owner. |
| **#2415** – `ncl groups create` skips `container_configs` row | 2026-05-11 | 2026-05-17 | Open, 1 comment | Blocks group creation. No PR yet. |
| **#1968** – Per-agent provider/model config (PR) | 2026-04-24 | 2026-05-18 | Open | Large PR with 5 commits; awaits review/maintainer merge. High feature impact. |
| **#2082** – V2 docs: clarify upstream developer references (PR) | 2026-04-28 | 2026-05-18 | Open | Docs-only; waiting for approval. |
| **#2089** – Telegram `setReaction` for status-tracker compatibility (PR) | 2026-04-29 | 2026-05-18 | Open | Feature for Telegram reaction support; no review comments. |
| **#2184** – Fix poll-loop: retry immediately on stale session instead of delivering error (PR) | 2026-05-02 | 2026-05-18 | Open | Fix for UX improvement; may conflict with other poll-loop changes. |

**Recommendation:** Maintainers should prioritize #2386 and #2415 as they are simple fixes blocking basic CLI functionality. The large PR #1968 (per-agent provider config) is a roadmap item and should receive reviewer bandwidth soon.

---

*Digest end. Data as of 2026-05-18, 24h window.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

**NullClaw Project Digest – 2026-05-18**

---

### 1. Today’s Overview
NullClaw is in a quiet phase with no new releases or merged pull requests in the last 24 hours. Two open issues were updated, reflecting a mix of a reported scheduler bug and a user-proposed feature to control memory recall. Community activity is low, with only one comment across all issues. The project appears stable but may benefit from maintainer attention to the open bug (scheduler unauthorized) that has been lingering since May 15.

---

### 2. Releases
No new releases were published in the last 24 hours. There are no recent versions to report.

---

### 3. Project Progress
No pull requests were created, merged, or closed in the last 24 hours. No feature advancements or fixes were integrated.

---

### 4. Community Hot Topics
- **[#915 – Bug: Problem with scheduler unauthorized](https://github.com/nullclaw/nullclaw/issues/915)**  
  *Author: scabros | Created: 2026-05-15 | Updated: 2026-05-17 | Comments: 1 | 👍: 0*  
  This is the most active issue, with one comment. The user reports that the scheduler component fails (unauthorized) when running NullClaw on Ubuntu with an external Ollama host (Qwen3.6:27b on RTX 3090). Tool calling works in general, but scheduler operations (both in Telegram and chat) are broken.  
  **Underlying need**: A reliable scheduling system that works with external LLM backends; likely an authentication/authorization mismatch between the scheduler service and the LLM host.

- **[#919 – Feature: Allow disabling automatic memory recall (FTS5) per-message](https://github.com/nullclaw/nullclaw/issues/919)**  
  *Author: weissfl | Created: 2026-05-18 | Updated: 2026-05-18 | Comments: 0 | 👍: 0*  
  A fresh request from a user who wants control over the built-in FTS5 + BM25 recall that runs on every incoming message. Hardcoded parameters (recall limit 5, max context 4 KB, etc.) cannot be disabled, leading to unwanted overhead.  
  **Underlying need**: Performance tuning and flexibility – users need to disable or customize memory recall for specific conversations or contexts where it is unnecessary or degrades response quality.

---

### 5. Bugs & Stability
**One active bug**:
- **[#915 – Scheduler unauthorized](https://github.com/nullclaw/nullclaw/issues/915)**  
  *Severity: Medium* – Affects a core feature (scheduling) for users with external LLM hosts, but tool calling otherwise works. No fix PR exists yet. The issue has been open for 3 days with one comment. No workaround has been shared.  
  *No other crashes or regressions reported in the last 24 hours.*

---

### 6. Feature Requests & Roadmap Signals
- **Disable memory recall per-message** ([#919](https://github.com/nullclaw/nullclaw/issues/919))  
  This is the only feature request today. It suggests a configurable toggle or per-message API parameter to skip FTS5/BM25 recall. Given that the parameters are currently hardcoded, this feature would likely involve exposing them in configuration or adding a `no_recall` flag.  
  **Prediction**: Could appear in the next minor release if maintainers prioritize performance flexibility. The request is straightforward and aligns with existing modularity patterns.

---

### 7. User Feedback Summary
- **Pain Point – Scheduler authentication**: User scabros reports that the scheduler fails with an “unauthorized” error when using an external Ollama host. This indicates a gap in the scheduler’s credential handling or host validation logic. The user is dissatisfied enough to open a bug but has not received a response.
- **Pain Point – Inflexible memory recall**: User weissfl wants to disable memory recall on a per-message basis to reduce overhead or improve response relevance. This suggests that the current automatic recall can be inappropriate for certain use cases (e.g., short queries, sensitive contexts).
- Overall sentiment is neutral-to-slightly concerned, with no new positive feedback.

---

### 8. Backlog Watch
No long-unanswered issues or PRs are identified from the current data. The only open issue older than 24 hours is [#915](https://github.com/nullclaw/nullclaw/issues/915) (3 days old), which has received one comment but no maintainer response. It should be watched as it may require triage soon. The project maintainers should review this bug to prevent it from stalling.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-18

## 1. Today's Overview
The IronClaw project shows **high activity** with 16 issues and 42 pull requests updated in the last 24 hours. The majority of work remains concentrated on the **Reborn** architecture (WebUI product workflow, provider tool-call integration, personal context gating) and on **bug fixes** for the v0.28.2 release. 5 PRs were merged or closed today, and 2 issues were resolved. Daily merge velocity remains moderate, but the open PR count (34) signals sustained development effort. The project is currently in a **beta transition** phase, with Reborn features landing alongside urgent stability patches.

## 2. Releases
No new releases were published today. The most recent tag remains `ironclaw-v0.28.2` (approximately May 15–16). Downstream consumers on crates.io are still pinned to `0.24.0` due to wasmtime CVE concerns (see Issue #3259).

## 3. Project Progress
Five pull requests were **merged or closed** today:

- **[#3744](https://github.com/nearai/ironclaw/pull/3744)** — `refactor(registry): address product adapter review follow-ups` — Documentation, cleanup of unused error variants, and validation clarifications.
- **[#3735](https://github.com/nearai/ironclaw/pull/3735)** — `feat(product_workflow): expose get_run_state on RebornServicesApi facade` — Fourth M2 facade method added, enabling WebUI route handlers to read run state without direct dependencies.
- **[#3681](https://github.com/nearai/ironclaw/pull/3681)** — `feat:[extensions] Add first-party HTTP egress tool` — Built-in `builtin.http` capability for Reborn first-party tools, delegating outbound calls to the existing host `RuntimeHttpEgress`.
- **[#2506](https://github.com/nearai/ironclaw/pull/2506)** — `feat(orchestrator): ORCHESTRATOR_HOST env var for worker callback address` — Long-standing fix for Linux Docker deployments; replaces hardcoded `host.docker.internal`.
- **[#2418](https://github.com/nearai/ironclaw/pull/2418)** — `feat: slim mode runtime, Dockerfiles, and /health route` — Reduces per-instance resource footprint for high-density multi-tenant deployments.

All five represent incremental improvements to Reborn, the orchestrator, and developer infrastructure.

## 4. Community Hot Topics
Two issues attracted the most discussion (both with 5 comments):

- **[#3692](https://github.com/nearai/ironclaw/issues/3692)** — *Reborn: add policy-gated personal identity and heartbeat prompt context* — The community is debating how to safely inject user‑specific context (e.g., `USER.md`) without violating the stable identity-file scope. Underlying need: ensure Reborn can personalise responses while maintaining security boundaries.
- **[#3259](https://github.com/nearai/ironclaw/issues/3259)** — *Publish 0.25.0–0.27.0 to crates.io — downstream pinned to 0.24.0 by wasmtime 28.x CVEs* — Discusses the blocking effect of wasmtime security advisories on crate publication. Downstream consumers cannot upgrade beyond 0.24.0, which is now two months behind HEAD.

Additionally, **[#3622](https://github.com/nearai/ironclaw/issues/3622)** and **[#3620](https://github.com/nearai/ironclaw/issues/3620)** (both Reborn tool-completion evidence and provider tool-call conversion) each have 3 comments, indicating ongoing refinement of the Reborn loop protocol.

## 5. Bugs & Stability
Several bugs were reported today, all related to v0.28.2 regressions or UI state inconsistencies:

| Severity | Issue | Summary | Fix PR exists? |
|----------|-------|---------|----------------|
| **High** | [#3734](https://github.com/nearai/ironclaw/issues/3734) | Provider config UI missing API Key and “Fetch available models” controls in non‑TEE agents (v0.28.2 regression). | Yes – [#3742](https://github.com/nearai/ironclaw/pull/3742) restores the missing fields. |
| **High** | [#3729](https://github.com/nearai/ironclaw/issues/3729) | Failed `tool_install(gmail)` calls show as successful after page refresh (state inconsistency). | No fix PR identified yet. |
| **Medium** | [#3733](https://github.com/nearai/ironclaw/issues/3733) | Invalid Gmail OAuth token shows success/activated toast, then immediately re‑prompts for OAuth. | No fix PR identified. |
| **Medium** | [#3743](https://github.com/nearai/ironclaw/issues/3743) | Telegram pairing approval shows duplicate success toasts. | No fix PR identified. |
| **Low** | [#3447](https://github.com/nearai/ironclaw/issues/3447) | Nightly E2E scheduled run continues to fail (open since May 10, last failure May 18). | No PR linked. |

The team is actively addressing the provider config regression (PR #3742). The page‑refresh state bug (#3729) and invalid token feedback (#3733) represent user‑facing quality issues that may require deeper investigation into frontend state management or backend response caching.

## 6. Feature Requests & Roadmap Signals
Today’s issues and PRs are dominated by **Reborn WebUI Beta** (M2/M3 modules). Key roadmap signals:

- **Personal context gating** (PR [#3721](https://github.com/nearai/ironclaw/pull/3721)) — Adds `ResolvedRunProfile.personal_context_policy` to allow or exclude personal prompts (`USER.md`, `assistant-directives.md`) based on run profile.
- **WebUI facade contract tests** (PR [#3741](https://github.com/nearai/ironclaw/pull/3741)) — Fake thread/timeline ports for isolated facade testing.
- **Boot‑config and provider catalog** (PR [#3704](https://github.com/nearai/ironclaw/pull/3704)) — Standalone config file split for `ironclaw-reborn` binary.
- **Before‑inbound policy seam** (PR [#3632](https://github.com/nearai/ironclaw/pull/3632)) — Allows WebUI/WebChat v2 messages to be checked, rewritten, or rejected before staging.

Predictions for the next patch/minor release (v0.28.3 or v0.29.0):
- Restoration of missing provider config controls (#3734, #3742).
- Gating of personal context for Reborn (#3721).
- Basic WebUI facade methods (#3735, #3741).
- The `builtin.http` egress tool (#3681) will likely ship as a first‑party capability.

## 7. User Feedback Summary
User reports from the past 24 hours highlight **frustration with UI state inconsistency** and **regressions** introduced in v0.28.2:

- “After refreshing the page, denied tool calls are displayed as successful” (#3729) – undermines trust in the UI.
- “Settings > Inference provider config no longer shows API Key or Fetch available models controls” (#3734) – blocks configuration of NEAR AI provider.
- “Invalid Gmail token shows success toast” (#3733) – misleading feedback, followed by repeated auth prompts.
- “Telegram pairing approval shows duplicate success toasts” (#3743) – minor annoyance.

These reports indicate that the v0.28.2 release, while shipping Reborn features, introduced frontend regressions. Users are actively testing the new UI and reporting issues, which suggests ongoing adoption of the latest version.

## 8. Backlog Watch
Several important items remain unresolved for extended periods:

- **[#3259](https://github.com/nearai/ironclaw/issues/3259)** — Crate publication gap (open since May 5, active today). Downstream consumers cannot upgrade beyond 0.24.0. **This is a critical blocker for ecosystem adoption**; no maintainer comment yet on resolution timeline.
- **[#3447](https://github.com/nearai/ironclaw/issues/3447)** — Nightly E2E failure (open since May 10, 0 comments). No fix PR or discussion. May indicate an unstable test or environment issue.
- **[#2066](https://github.com/nearai/ironclaw/pull/2066)** — Slack thread history fetch when bot is @mentioned (open since April 6). This feature PR has been untouched for over a month; a decision to merge, revise, or close is pending.
- **[#2457](https://github.com/nearai/ironclaw/pull/2457)** — OIDC audience claim optional for proxying load balancers (open since April 14). A small but important fix for deployments behind OIDC proxies; no recent activity.

These items should be prioritised for maintainer attention to prevent stagnation and retain contributor trust.

---

*Digest generated from GitHub data for 2026-05-18. All links point to the `nearai/ironclaw` repository.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-18

**Note:** All data is sourced from the LobsterAI GitHub repository (netease-youdao/LobsterAI). Metrics reflect activity in the last 24 hours unless stated otherwise.

---

## Today's Overview

The project saw a **high level of development activity** today with **17 PRs updated**, of which **12 were merged or closed** — a strong release-oriented push. The release branch `release/2026.5.18` (#2010) was created and closed, consolidating several features, refactors, and bug fixes. No new issues were filed or updated in the last 24h, indicating a focused effort on merging existing work rather than triaging new problems. The release concludes a cycle that includes a notable new **per-model context window slider** and multiple UI/UX improvements.

---

## Releases

**No new releases were published today.** The consolidated release branch `release/2026.5.18` (#2010) was closed but not tagged as a formal release. It is likely that an official release (e.g., v2026.5.18) will follow soon based on this branch’s content.

---

## Project Progress

### Merged/Closed PRs Today (12)

All 12 merged PRs represent significant progress across core areas:

- **Feature – Per-model context window slider** (#2001)  
  Adds a nonlinear slider in model settings with a new 2M token upper bound, configurable per model. Required changes in shared types, renderer UI, and OpenClaw service.

- **Bug fixes**
  - **Markdown local resource path** (#2002) — Fixes relative image paths in markdown preview by resolving them via `localfile://`.
  - **Non-ASCII MCP server names** (#2006) — Uses deterministic MD5-based key generation to handle CJK and other non-ASCII names for OpenClaw compatibility.
  - **UI regression in new-task page** (#2007) — Restores theme-aware background color after an accidental change to `bg-surface`.
  - **Dreaming toggle** (#2005) — Replaces a text button with a standard sliding toggle switch, aligning it with the Embedding switch in the memory page.

- **Refactors**
  - **Model settings extraction** (#2004) — Extracts the model tab UI from `Settings.tsx` (5162 → 3502 lines) into a dedicated `ModelSettingsSection.tsx` component.
  - **MIMO model compatibility** (#2000) — Fixes Anthropic format compatibility for the MIMO model.

- **Housekeeping**
  - **Plugin upgrade** (#2003) — `moltbot-popo` plugin 2.1.1 → 2.1.8.
  - **Cron UI update** (#2009) and **icon update** (#2008) — Minor chore changes.

### Open (5) PRs Updated Today

All are **stale PRs** (created March 2026) that received updates today (likely due to merge conflict resolution or being included in the release branch):

- #748 – Refactor IM platform config handlers  
- #749 – Memoize Cowork streaming components  
- #752 – `/compact` command & auto-compression (feat)  
- #755 – Export chat logs as Markdown/JSON  
- #760 – Remove duplicate session status update  
- #811 – Use index table for O(1) message lookup  

These remain unmerged, indicating they may need further review or conflict resolution before inclusion.

---

## Community Hot Topics

**No issues were updated today**, so no issue-based discussions to highlight. Among the open PRs, the most notable from community or activity perspective:

- **#752 (Feat/compact)** — Implements `/compact` command and automatic compression for Cowork sessions. This is a long-standing feature request (since March 24) that touches all major LLM providers. The number of changes (multi-file, dual API format) suggests high effort and interest.
- **#755 (Export chat logs)** — Export to Markdown/JSON. A user-facing feature that could have high demand for data portability.

These PRs have been open for nearly two months and have not received maintainer comments (based on metadata). The underlying need is clear: **better session management and data portability** for power users.

---

## Bugs & Stability

### Fixed Today (4 bugs, all resolved via merged PRs)

| Rank | Bug | PR | Severity |
|------|-----|----|----------|
| High | **Non-ASCII MCP server names break OpenClaw** (#2006) | Fixed by hashing names | Medium-high (breaks CJK users) |
| Medium | **Markdown preview: relative images not shown** (#2002) | Fixed path resolution | Medium (affects local markdown viewing) |
| Low | **New-task page background wrong color** (#2007) | Reverted single class | Low (visual cosmetic) |
| Low | **Dreaming toggle inconsistent with other UI** (#2005) | Replaced toggle component | Low (UI consistency) |

### Regressions / Known Issues

- **#2004 (refactor)** introduces a minor modal overlay scope change: the modal for editing models now has a different `z-index` context, which could cause display issues in edge cases. Noted as a known issue in the PR.

No new bugs were reported today (0 new issues).

---

## Feature Requests & Roadmap Signals

- **Per-model context window** (#2001) is a clear step toward fine-grained model control — requested frequently in agent-based workflows where different models need different token budgets.
- **Dreaming toggle standardization** (#2005) and **cron UI update** (#2009) suggest ongoing polish of the “Dreaming” (possibly a persistent memory/background agent) feature.
- The merging of the release branch indicates that **Cowork session streaming performance** (PR #749, #811) and **IM platform refactoring** (#748) are not yet prioritized for this release, but remain on the radar.

Based on the stale open PRs, the next version might include:
- Session compression / auto-compact (#752) — a frequently requested feature for long-running Cowork sessions.
- Export functionality (#755) — likely to improve user data control.
- Message lookup optimization (#811) — important for large session performance.

---

## User Feedback Summary

While no direct user comments are available from the data, the PR descriptions reveal common pain points addressed today:

- **CJK users** faced MCP server name corruption (Chinese characters replaced with hyphens) — now fixed with hashing.
- **Markdown authors** could not preview local images attached to notes — now resolved.
- **New users** likely confused by inconsistent toggle components (dreaming vs embedding) — standardized.
- **Power users** managing many models (diverse context windows) now have per-model slider granularity.

Overall, the development team is responsive to user-facing UI consistency and cross-locale issues, while pushing forward larger features (context windows, compression) in the background.

---

## Backlog Watch

The following **stale open PRs** have not been merged for ~55 days and may need maintainer attention:

| PR | Description | Last Updated | Risk |
|----|-------------|--------------|------|
| #748 | Refactor IM platform handlers | 2026-05-18 (today) | Low – clean code, no functional change |
| #749 | Memoize Cowork components | 2026-05-18 | Medium – performance gain but risky if re-render logic changes |
| #752 | Feat/compact for Cowork | 2026-05-18 | High – large feature, potential merge conflicts |
| #755 | Export chat logs | 2026-05-18 | Medium – user-facing, might need UX review |
| #760 | Remove duplicate session status update | 2026-05-18 | Low – trivial fix |
| #811 | O(1) message lookup index | 2026-05-18 | Medium – performance critical but may conflict with other message handling refactors |

**Recommendation:** Given the release branch merge, it is advisable to resolve conflicts on these PRs and prioritize merging those with clear value (especially #752 and #811) in the next development cycle.

---

*End of digest. Generated from GitHub data on 2026-05-18.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis Project Digest – 2026-05-18

### 1. Today's Overview
The project saw a surge of focused activity: 6 issues were updated (5 closed, 1 open) and 8 pull requests were touched (6 merged/closed, 2 open). A new patch release was cut. All closed bugs from the last 24 hours were fixed within the same day, indicating a healthy turnaround. The two open PRs and one open feature request signal continued momentum on memory management and agent routing.

### 2. Releases
- **20260517.03** (2026-05-17)  
  No changelog or migration notes were provided. Given the volume of bug fixes merged on 2026-05-18, this release likely pre-dates the day's patches and does not contain them. Users should expect a follow-up release incorporating today’s fixes.

### 3. Project Progress
Six pull requests were merged/closed today, each addressing a specific bug:

- **#1019** – fix(tools): ignore heredoc bodies in dangerous command scan (fixes #1014)  
- **#1018** – fix(agents): honor BeforeLLMCall hook modifications (fixes #1013)  
- **#1017** – fix(agents): dispatch before agent start hooks (fixes #1012)  
- **#1016** – fix(providers): parse thought reasoning tags (`<thought>`) for Gemma (fixes #1007)  
- **#1015** – fix(config): preserve explicit defaults on startup (fixes #1006)  
- **#1008** – Add NetBird and Cloudflare Tunnel to onboarding (feature enhancement, no bug linked)

Additionally, two PRs remain open and under review:

- **#1010** – feat(memory): allow nested subfolders and collection-aware writes  
- **#1009** – fix(qmd): kill child process when `run_with_timeout` expires

### 4. Community Hot Topics
No issues or PRs received comments or reactions today. All bug reports were filed and fixed without further discussion, suggesting clear reproduction and straightforward patches. The only open feature request (#1011, see Section 6) also has zero comments, but its detailed proposal hints at a common pain point for users of smaller LLMs.

- [Issue #1011](https://github.com/moltis-org/moltis/issues/1011) – open feature request, 0 comments, 0 reactions.

### 5. Bugs & Stability
All five bugs reported in the last 24 hours were closed with corresponding fix PRs. Severity ranking:

| Priority | Issue | Description | Status |
|----------|-------|-------------|--------|
| **Critical** | [#1012](https://github.com/moltis-org/moltis/issues/1012) | `BeforeAgentStart` hook never fires – dispatch lost in April refactor | **Fixed** (PR #1017) |
| **Critical** | [#1013](https://github.com/moltis-org/moltis/issues/1013) | `BeforeLLMCall` hook `ModifyPayload` silently discarded | **Fixed** (PR #1018) |
| **High** | [#1007](https://github.com/moltis-org/moltis/issues/1007) | Gemma-4-31b reasoning tags (`<thought>`) treated as plain text | **Fixed** (PR #1016) |
| **Medium** | [#1014](https://github.com/moltis-org/moltis/issues/1014) | Dangerous pattern regex false-positive on heredoc body content | **Fixed** (PR #1019) |
| **Low** | [#1006](https://github.com/moltis-org/moltis/issues/1006) | VoiceCoquiTtsConfig defaults stripped during auto-compact | **Fixed** (PR #1015) |

No regressions or crashes remain open.

### 6. Feature Requests & Roadmap Signals
One new feature request was filed today:

- **[#1011](https://github.com/moltis-org/moltis/issues/1011)** – *Per-turn `tool_choice` + `active_tools` filtering for drift-resistant agent routing*  
  The request stems from the difficulty small/cheap LLMs (e.g., Claude Haiku 4-5) have in reliably selecting from many tools. The proposal would allow per-turn narrowing of available tools and explicit `tool_choice`, improving routing accuracy.

Coupled with the two open PRs ([#1010](https://github.com/moltis-org/moltis/pull/1010) on nested memory folders and [#1009](https://github.com/moltis-org/moltis/pull/1009) on QMD child process cleanup), the next minor release will likely include:

- Extended memory collection support (subfolders)
- Better timeout handling in QMD runner
- Possibly the per-turn tool control, if the community discussion gains traction.

### 7. User Feedback Summary
Real user-reported pain points from today’s issues all centered on **hook reliability and configuration surprises**:

- Two hook bugs (`BeforeAgentStart`, `BeforeLLMCall`) directly broke custom agent workflows – high dissatisfaction, but swiftly fixed.
- False-positive dangerous pattern detection (`rm -r`) in heredocs caused needless alarms for users writing shell scripts.
- Gemma reasoning tags bleeding into visible output was a real user-facing quality issue for TTS and chat.
- Config auto-compacting silently dropping explicit defaults (Coqui TTS port) created configuration fragility.

All reports are now resolved, which should restore user trust.

### 8. Backlog Watch
No open issues or PRs appear to have been waiting for maintainer attention for an extended period. The following open items are worth monitoring for next steps:

- **[#1010](https://github.com/moltis-org/moltis/pull/1010)** (open 1 day) – needs review and merge to support nested memory collections.  
- **[#1009](https://github.com/moltis-org/moltis/pull/1009)** (open 1 day) – a process‑leak fix that could improve stability under heavy `memory_save` usage.  
- **[#1011](https://github.com/moltis-org/moltis/issues/1011)** (open 1 day) – feature request that could shape the next roadmap.

No stale issues were identified.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-18

A daily analysis of the CoPaw (agentscope-ai/CoPaw) open-source project, based on GitHub activity from the past 24 hours.

## 1. Today's Overview

The CoPaw project is in a state of **high activity**, driven by a surge of community bug reports, developer pull requests, and ongoing issue triage. A total of **26 issues** were updated in the last 24 hours, with **10 closed** and **16 remaining open**, indicating a healthy triage pace. The **28 updated pull requests** (with **6 merged/closed**) reflect a focus on stability fixes, with key merges addressing critical user-facing bugs like chat unresponsiveness and rate-limiting errors. While no new releases were cut today, the community is rallying behind stabilizing the v1.1.7 series, with maintainers actively reviewing contributions for security and core functionality.

## 2. Releases

**None.** No new releases were published during this period.

## 3. Project Progress (Merged/Closed PRs)

Today’s activity saw **6 pull requests merged or closed**, focusing on bug fixes across backend, provider, and UI layers.

- **`#4487` - Fix: replace global LLM rate limiter with per-model instances** (rayrayraykk). This is a significant fix addressing the "three dots spinning / chat unresponsive" bug (Issues #4469, #4453) by moving from a process-wide rate limiter singleton to per-model instances. This resolves a major pain point for users with multiple models.
- **`#4476` - Fix: add per-model token usage aggregation** (zhijianma). Fixes the `get_token_usage` tool, which was reported broken in Issue #4473. This restores accurate token tracking for users.
- **`#4488` - Fix: upgrade chat library to v1.1.63 to fix SSE connection leak** (zhijianma). Fixes a connection leak that occurred during page navigation in the Console UI, resolving intermittent message failures and browser connection limits.
- **`#4489` - Fix: increase min `max_tokens` to 20** (qbc2016). Addresses an API error for restrictive models (e.g., `qwen3.5-omni-plus`) that require a higher minimum `max_tokens`, preventing “InternalError.Algo.InvalidParameter” errors.
- **`#4484` - Fix: OpenAIProvider connection test fails to read `extra_headers`** (Andrai985). Merged, a closed issue with PR `#4492` to fix API connectivity validation issues for third-party providers.
- **`#4479` - New octoken provider added** (xusuohan). A new model provider was added, though the description notes a potential over-reach ("删除其他供应商") and has been closed. This may represent a misstep that was quickly reverted.
- **`#4429` - Fix: backup restore trust hardening** (jinglinpeng). A follow-up fix addressing security and compatibility concerns with the backup restore feature (under review).

## 4. Community Hot Topics

The most active discussions today highlight a strong community focus on **reliability and compatibility**.

- **`#4469` • [Bug]: Chat window unresponsive, model options not working** (linllyw). *16 comments.* This is the most impactful bug report of the day, mirroring the concerns in `#4453` (9 comments). Users report a complete inability to use the chat interface after updating to v1.1.7, with symptoms of spinning dots and no response. The root cause was identified and fixed in PR `#4487` (global rate limiter). **Link:** [Issue #4469](https://github.com/agentscope-ai/CoPaw/issues/4469)
- **`#4051` • [Question]: DeepSeek model thinking tags parsed incorrectly** (wxfvf). *8 comments.* Users report that DeepSeek's `think` content is not parsed correctly, leading to empty replies. This is a long-standing issue (May 6) that is gaining attention, pointing to a gap in handling reasoning-focused models. **Link:** [Issue #4051](https://github.com/agentscope-ai/CoPaw/issues/4051)
- **`#4477` • [Bug]: WeChat iLink scheduled task push failure** (zhanggegehao). *7 comments.* A detailed report describes how the WeChat iLink channel fails to push scheduled tasks when the `context_token` expires (ret=-2), with no retry logic. Also highlights a lack of logging for file/image send failures. **Link:** [Issue #4477](https://github.com/agentscope-ai/CoPaw/issues/4477)
- **`#4474` • [Question]: Does it support ChatGPT-5.5?** (jiang-zhong-xi). *6 comments.* A user is asking about compatibility with a new model. This reflects the community's desire for bleeding-edge model support.
- **`#4367` • [Bug]: Assistant stuck showing only "Thinking" after tool result** (SophiaNamesLiu). *3 comments.* A tricky session-state bug where the UI shows a "thinking" step but no text answer.

## 5. Bugs & Stability

The project’s bug status is **critical**, with multiple high-impact stability issues reported. The good news is that core fixes are already being merged.

- **Severity: Critical**
    - **`#4469` & `#4453` — Chat window unresponsive (Global Rate Limiter bug).** Users on v1.1.7 cannot send messages. **Status: FIXED** by PR `#4487` (merged today). This is the most important fix of the day.
- **Severity: High**
    - **`#4477` — WeChat iLink timed task failure.** Scheduled messages fail to deliver due to a `context_token` expiry with no retry. **Status: OPEN.** A related fix (PR `#4490`) is proposed.
    - **`#4448` — Context compaction failing.** Long conversations break due to a header format error during context compression. **Status: OPEN.** A duplicate (`#4447`) was closed. This is a core stability issue.
    - **`#4485` — Plugin Tool Injection Failure.** Plugin tools are discovered and listed but their Python functions are never linked into the Agent's function-calling toolkit. **Status: OPEN.** This prevents users from using any installed plugin tools.
- **Severity: Medium**
    - **`#4470` — Plugin interface unauthorized RCE vulnerability.** A user has identified a potential security flaw. **Status: OPEN.** Requires immediate maintainer review.
    - **`#4494` — Console stream stalling mid-generation.** The UI stops streaming and shows a misleading "you interrupted me" message. **Status: OPEN.**
- **Severity: Low**
    - **`#4481` — Windows GBK encoding issues (system-level).** A request to replace existing scattered patches with a systemic fix. **Status: OPEN.**

## 6. Feature Requests & Roadmap Signals

User requests are leaning towards **improved model support, packaging, and platform integration**.

- **Model Compatibility:** `#4474` requests support for "chatgpt-5.5", indicating the community is actively pushing the boundaries of new models. This suggests a roadmap item to support a broader set of LLM providers.
- **Developer Experience/CLI:** `#4472` proposes switching from `click` to `typer` for colored and modern CLI behavior. This is a strong signal that the command-line interface is a priority for users.
- **Packaging:** `#4486` requests a `Flathub` / `flatpak` installer for Linux. While the current installer is functional, the popularity of Flathub among Linux users signals demand for a decentralized, sandboxed app manager.
- **Agent Architecture:** `#4491` raises a deep question about configuration inheritance for sub-agents (MCP/ACP config). This suggests the community is exploring multi-agent topologies and needs clear design decisions.
- **New Skills:** A new "World Cup 2026 match companion skill" (`#4407`) and a "QwenPaw pet plugin" (`#4418`) are in the pipeline, showing momentum in expanding plugin ecosystems.

**Prediction:** The next minor release (v1.1.8) will likely include the rate limiter fix, token usage fix, and chat library upgrade. More ambitious features like Flathub support or the World Cup skill may land in a v1.2.0.

## 7. User Feedback Summary

Overall sentiment is **mixed**. While the community is enthusiastic enough to file detailed bug reports and feature requests, there is notable frustration regarding stability.

- **Pain Points:**
    - **"chat not responding":** This is the loudest complaint. User from `#4469`: "发送消息后一直是三个点在跳动状态" (Message is sent, but only three dots are jumping). Another user from `#4475` says: "这阿里技术也不行啊" (Alibaba's tech is not good either), albeit mistakenly attributing the bug to Alibaba.
    - **"Plugin tools don't work":** User from `#4485` reports a complete failure to execute function calls via plugins, a significant workflow blocker.
    - **"Model Parsing Errors":** User from `#4051` and others report that advanced models (like DeepSeek's thinking models) produce garbled or empty responses, damaging user trust for complex use cases.
- **Satisfaction Signals:**
    - **Proactive Reporting:** Users are providing stack traces, session logs, and screen recordings. The detailed bug report for the WeChat channel (`#4477`) shows a mature user base.
    - **Feature Excitement:** The creation of new PRs like the pet plugin and World Cup skill suggests a healthy, engaged developer community excited to build on the platform.

## 8. Backlog Watch

Several important issues remain unanswered or unaddressed, posing a risk to project health.

- **`#3854` • [Bug]: chromadb Rust binding segfault (SIGSEGV) kills process** (zealonexp). **(Opened: April 27).** A severe, stability-critical bug on Linux that requires a safer default or graceful fallback. **No maintainer response since May 17.** This directly impacts agent memory reliability. **Link:** [Issue #3854](https://github.com/agentscope-ai/CoPaw/issues/3854)
- **`#2908` • [Bug]: Application icon fails to load in local network deployment (CDN dependency)** (myhylijp). **(Opened: April 3).** A long-standing issue where the UI relies on an external CDN for icons, breaking on private networks. **Marked closed but no visible fix.** This impacts enterprise adopters. **Link:** [Issue #2908](https://github.com/agentscope-ai/CoPaw/issues/2908)
- **`#4470` • [Bug]: Plugin interface unauthorized RCE vulnerability** (iQingshan). **(Opened: May 17).** **No security label or maintainer assignment.** Given the potential severity, this needs immediate attention to prevent security incidents.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-18

## 1. Today’s Overview

Project activity remains high: **15 issues** and **50 PRs** were updated in the last 24 hours. Of those, **5 issues** were closed and **7 PRs** were merged or closed. No new releases were cut. The open issue count (10 active) and PR backlog (43 open) reflect a busy development phase, with several high-priority bugs (DeepSeek V4 compatibility, Kimi-code streaming, reasoning_content forwarding) still in progress. The largest single effort is the **v0.8.0 multi-agent runtime PR** (#6398), which remains open and seeking approval after nearly two weeks.

---

## 2. Releases

**None.** The `Latest Releases` section is empty. There are no new versions to report.

---

## 3. Project Progress

**Merged/Closed PRs today** (7 total; known examples from the top 20):

- **[#6732] fix(skills): use __ separator in tool names for OpenAI-compat function calling** — Resolves a tool-name validation failure on OpenAI/OpenRouter/Gemini caused by dots in skill tool names.
- **[#6755] docs+test: refresh stale MiniMax endpoint and model** — Updates the provider catalog and integration tests to point at the current MiniMax API (moved from `api.minimax.chat` to current endpoint) and a non‑deprecated model.

**Closed Issues today** (5 total):

- [[#1924] FreeBSD platform support](zeroclaw-labs/zeroclaw Issue #1924) — Closed after prebuilt binaries for FreeBSD were added.
- [[#5994] Build official website + end-to-end docs](zeroclaw-labs/zeroclaw Issue #5994) — The documentation site is now live.
- [[#6431] SQLite memory schema init can fail during concurrent startup](zeroclaw-labs/zeroclaw Issue #6431)
- [[#6548] Channel runtime command replies bypass Fluent localization](zeroclaw-labs/zeroclaw Issue #6548)
- [[#6705] Cron job execution fails on Windows — hardcoded `sh`](zeroclaw-labs/zeroclaw Issue #6705)

---

## 4. Community Hot Topics

Most active issues (by comments and reactions):

- [#6059 – Incompatible with DeepSeek-V4 API format](zeroclaw-labs/zeroclaw Issue #6059)  
  **9 comments** · 4 👍 · High risk · P1  
  *Underlying need*: Users running DeepSeek-V4-Pro and V4-Flash hit a “thinking mode” API format mismatch. This blocks a major provider.

- [#5600 – Use kimi-code provider in streaming chat call tools, API error](zeroclaw-labs/zeroclaw Issue #5600)  
  **9 comments** · 1 👍 · P1 · Open since Apr 10  
  *Underlying need*: Streaming tool calls with Kimi-code provider fail with a `reasoning_content` missing error, making a popular provider unusable.

- [#6672 – reasoning_content not passed back in agentic tool-call loops with Xiaomi thinking mode](zeroclaw-labs/zeroclaw Issue #6672)  
  **3 comments** · P1 · In progress  
  *Underlying need*: Agent loops lose the reasoning trail when using Xiaomi’s Mimo models, causing data loss (S0 severity).

- [#6074 – Audit: track 153 commits lost in bulk revert](zeroclaw-labs/zeroclaw Issue #6074)  
  **2 comments** · High risk · P2  
  *Underlying need*: Development history recovery — a bulk revert wiped out features and fixes; community wants a recovery plan.

**Most discussed PRs** (multiple updates today):

- **[#6398 v0.8.0: Multi-Agent Runtime and Schema V3](zeroclaw-labs/zeroclaw PR #6398)** — A massive cross‑cutting PR (touches nearly every component) that is still awaiting approval. It defines the beta release baseline.
- **[#6741 / #6740 Cron timezone fixes](zeroclaw-labs/zeroclaw PR #6741, #6740)** — Two related PRs addressing timezone handling in the cron API and scheduler.
- **[#6675 Fix(runtime): add strict tool parsing mode](zeroclaw-labs/zeroclaw PR #6675)** — Adds a configurable strict mode to avoid text fallback parsing, important for provider compatibility.

---

## 5. Bugs & Stability

**Bugs reported today (2026-05-18):**

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| [#6756] | Medium (functionality blocked) | `zeroclaw models list` fails for custom providers because `doctor path` never reads stored `api_key` from config | No |
| [#6754] | Low (enhancement) | ACP bridge auto-pairing depends on one‑time‑use code, fragile for operators | No |
| [#6751] | High (CI silent failure) | PR title workflow (`Validate PR title`) has never run since merge (startup_failure) | No |
| [#6747] | High (CI dead) | `amannn/action-semantic-pull-request` fails because it’s not in the allowed actions list | No |

**Other active high‑severity bugs:**

- [#6059 DeepSeek-V4 API incompatibility](zeroclaw-labs/zeroclaw Issue #6059) — P1, in progress
- [#5600 Kimi-code streaming error](zeroclaw-labs/zeroclaw Issue #5600) — P1, open since Apr 10
- [#6672 reasoning_content not forwarded for Xiaomi](zeroclaw-labs/zeroclaw Issue #6672) — S0 data loss, P1, in progress

**Notable fix PRs in flight:**

- [#6753 fix(providers/deepseek): honor configured base_url override](zeroclaw-labs/zeroclaw PR #6753) — Addresses a hardcoded URL bug.
- [#6732 Skills tool name separator fix](zeroclaw-labs/zeroclaw PR #6732) — Already merged; closes a blocker for OpenAI‑compatible providers.

---

## 6. Feature Requests & Roadmap Signals

**New feature requests this period:**

- [#6742 Add streaming payload tracing tests for `--log-llm`](zeroclaw-labs/zeroclaw Issue #6742) — Testing infrastructure for LLM payload tracing.
- [#6754 ACP bridge auto-pairing improvement](zeroclaw-labs/zeroclaw Issue #6754) — Remove dependency on one‑time‑use codes.
- [#1924 FreeBSD platform support](zeroclaw-labs/zeroclaw Issue #1924) — Now closed; binaries added.

**Roadmap indicators:**

- **[#6253 v0.7.6 tracker: Improve `zeroclaw skills` support and UX](zeroclaw-labs/zeroclaw Issue #6253)** — Coordinating tracker for the next minor release. Community input welcome.
- **[#6398 v0.8.0: Multi-Agent Runtime and Schema V3](zeroclaw-labs/zeroclaw PR #6398)** — The next major release, still in review. It touches nearly every crate and is described as the beta baseline.
- **[#6074 Commit recovery audit](zeroclaw-labs/zeroclaw Issue #6074)** — A planned recovery effort for lost commits; not tied to a specific version but signals process improvement.

*Prediction*: The next release will likely be **v0.7.6** focused on skills UX, followed by **v0.8.0** (multi‑agent runtime, schema V3). Several bugs (DeepSeek, Kimi-code, reasoning_content) are blockers that should be resolved before either release.

---

## 7. User Feedback Summary

**Pain points expressed by users:**

- **Provider incompatibility**: DeepSeek-V4, Kimi-code, and Xiaomi Mimo models fail with thinking‑mode or API format mismatches. Users report S1/S0 workflow blocks.
- **Windows support gaps**: Cron jobs are entirely broken on Windows without Git Bash (#6705, now closed). Snapshot TTL too short on Windows (#6750, fix in progress).
- **FreeBSD lack of binaries** (now resolved with #1924).
- **Documentation fragmentation** (#5994, now resolved with a dedicated website).
- **Localization bypass** (#6548, fixed) — hard‑coded English strings in channel replies.

**Satisfaction signals**: Several closed issues show users’ reported problems being acknowledged and resolved quickly (FreeBSD, website docs, SQLite concurrency, Windows cron). The active in‑progress status on high‑severity bugs (#6059, #6672) indicates maintainers are prioritizing them.

**Use cases** observed: Server/operator workflows (ACP bridge, cron), multi‑channel deployment (Matrix, Slack, WhatsApp, WeChat), custom provider integration, and skill authoring.

---

## 8. Backlog Watch

Issues and PRs that have been open for an extended period or lack maintainer response:

- [[#5600] Use kimi-code provider in streaming chat call tools, API error](zeroclaw-labs/zeroclaw Issue #5600)  
  **Open since Apr 10** · P1 · No fix PR yet. Mainstream provider broken for streaming tool calls.

- [[#6074] Audit: track 153 commits lost in bulk revert](zeroclaw-labs/zeroclaw Issue #6074)  
  **Open since Apr 24** · High risk · Development history recovery still unaddressed.

- [[#6059] Incompatible with DeepSeek-V4 API format](zeroclaw-labs/zeroclaw Issue #6059)  
  **Open since Apr 24** · P1 · Marked in progress but no fix PR linked.

- [[#6307? Not listed, but note #6398 PR is large and pending]  
  **PR #6398** (v0.8.0) has been open since May 5 and is seeking approval. Blocking progress on numerous other features.

- [[#5838] Webhook retry with exponential backoff](zeroclaw-labs/zeroclaw PR #5838)  
  **Open since Apr 17** · No maintainer comments visible. A well‑scoped improvement that could benefit many users.

Maintainers should prioritise unblocking the DeepSeek and Kimi-code issues, as they affect popular providers, and provide a timeline for v0.8.0 review to reduce the PR backlog.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*