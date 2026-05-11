# OpenClaw Ecosystem Digest 2026-05-11

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-11 11:46 UTC

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

**OpenClaw Project Digest — 2026-05-11**

---

## 1. Today's Overview

The project remains highly active with **500 issues** and **500 pull requests** updated in the last 24 hours. Of those, **69 PRs were merged or closed** today, and **393 issues remain open** (active). Three new beta releases (`v2026.5.10-beta.1/2/3`) were published, focusing heavily on QA automation infrastructure, particularly Telegram-based evidence capture for PRs. The community is reporting numerous regressions and behavior bugs, with the most active thread (Issue #52875) collecting 20 comments about agent session discovery failures after a recent upgrade. A notable security concern (CVSS 9.0 – #50642) regarding TLS auto-trust on macOS remains open and critical. Overall, the project's velocity is high but stability appears strained, with many open bugs tied to session handling, tool routing, and channel integrations.

---

## 2. Releases

Three beta versions were released today (all dated 2026-05-10):

- **`v2026.5.10-beta.3`** — Build tooling improvements: stricter Vitest lint rules (focused, disabled, conditional tests), pinned `oxfmt` defaults for stable formatting, and stricter TypeScript compiler checks enabled.
- **`v2026.5.10-beta.2`** — QA/Mantis module additions: Telegram live PR evidence automation (Convex-leased credentials, Crabbox transcript capture, motion GIF previews, inline PR comments). Also added a Telegram desktop scenario builder that leases Crabbox and configures native Telegram Desktop.
- **`v2026.5.10-beta.1`** — Same QA/Mantis changes as above, without the extra build tweaks.

**No breaking changes** or migration notes were documented. These releases appear targeted at improving testing infrastructure rather than end-user features.

---

## 3. Project Progress

Today's merged/closed PRs (from the top 30 by comment count):

- **#80615** (`fix(sessions): stream JSONL transcript scans instead of buffering whole files`) — Closed. Addresses memory scaling issues for large sessions.
- **#79826** (`fix(doctor): warn when per-agent model omits fallbacks key`) — Closed. Improves configuration diagnostics.
- **#80493** (`Use native Codex side threads and OpenAI auth fallback`) — Closed. A large refactor (size: XL) to handle side-question routing properly when using Codex OAuth profiles.

Additionally, among the **69 merged/closed PRs** (not all shown), these three represent notable improvements to session persistence, configuration validation, and Codex integration. No new major features were merged; most fixes target reliability and diagnostics.

---

## 4. Community Hot Topics

The most active discussions (by comment count and reactions):

| Issue/PR | Comments | Reactions (👍) | Topic |
|----------|----------|----------------|-------|
| [#52875 – bug/regression](https://openclaw/openclaw/issues/52875) | 20 | 0 | `session_send` fails with "no session found" after upgrade (2026-03-22 regression). Agent cannot contact other agents. |
| [#50090 – Feature request](https://openclaw/openclaw/issues/50090) | 14 | 1 | Community Skill Development & ClawHub ecosystem – wide gap between promise and practice. |
| [#53628 – bug/behavior](https://openclaw/openclaw/issues/53628) | 12 | 0 | `$XDG_CONFIG_HOME` not expanded when installing a skill. |
| [#76877 – closed bug/regression](https://openclaw/openclaw/issues/76877) | 11 | 4 (👍) | Agents stop responding mid‑work in v2026.5.2; regression since 2026.04.23. |
| [#51429 – bug/behavior](https://openclaw/openclaw/issues/51429) | 11 | 0 | Hardcoded developer workspace path (`/Users/wangtao`) merged into production – serious code review failure. |
| [#54253 – bug/behavior](https://openclaw/openclaw/issues/54253) | 10 | 3 (👍) | LLM request fails on RISC‑V64 systems – “run Error : LLM Request Failed”. |

**Underlying needs:** The community is experiencing **reliability regressions** after recent upgrades, particularly around session management, agent‑to‑agent communication, and tool execution (mid‑turn stalls). The hardcoded path incident (#51429) highlights quality‑control gaps. Meanwhile, the ClawHub ecosystem (#50090) remains a top desire but is not yet delivering a smooth experience.

---

## 5. Bugs & Stability

New or updated bugs (from today’s data) ranked by severity:

**Critical**
- [#50642 – macOS node auto‑trusts first TLS certificate](https://openclaw/openclaw/issues/50642) – CVSS 9.0 (Critical). Node.js on macOS automatically trusts the first presented TLS certificate, allowing a rogue gateway to control OpenClaw. No fix PR yet.
- [#50630 – Tailscale serve + auth.mode=none exposes gateway to full Tailnet](https://openclaw/openclaw/issues/50630) – CVSS 9.3 (Critical). No authentication enforcement when using Tailscale. Still open.

**High**
- [#76877 – Agents stop responding mid‑work (regression)](https://openclaw/openclaw/issues/76877) – Reported on v2026.5.2, closed today but presumably unresolved if marked as closed? (Note: the issue is closed, but the problem may have a fix merged? Not clear from data.)
- [#79596 – Gateway "ready" fires before acpx plugin finishes registering](https://openclaw/openclaw/issues/79596) – Beta release blocker.

**Medium**
- [#52875 – session_send gives no session found](https://openclaw/openclaw/issues/52875) – Regression since 2026-03-22. Most commented issue.
- [#51429 – Hardcoded path `/Users/wangtao` in code](https://openclaw/openclaw/issues/51429) – Poor code review; still open.
- [#52305 – Async task completion reports lost due to untargeted wake events](https://openclaw/openclaw/issues/52305)
- [#53486 – Feishu card JSON sent as plain text (regression)](https://openclaw/openclaw/issues/53486)
- [#53540 – Embedded runner timeout with large tool call parameters](https://openclaw/openclaw/issues/53540)
- [#52130 – Telegram restart storm due to type mismatch](https://openclaw/openclaw/issues/52130)

**Low**
- [#51871 – Cron jobs not displayed in dashboard on Raspberry Pi](https://openclaw/openclaw/issues/51871)
- [#53399 – Browser control server hangs](https://openclaw/openclaw/issues/53399)
- [#52421 – HTTP 400: duplicated tool_use_id](https://openclaw/openclaw/issues/52421)
- [#51593 – HTTP 400: "tool call id duplicated" in WhatsApp groups](https://openclaw/openclaw/issues/51593)

**Fix PRs in flight:** PR #80615 (streaming transcript scans) addresses memory issues linked to session corruption; PR #79826 improves fallback diagnostics; PR #56420 (still open) prevents permission spoofing across sessions.

---

## 6. Feature Requests & Roadmap Signals

Top user‑requested features from today's active threads:

- **Community Skill Development & ClawHub** (#50090) – Still the highest‑voted feature. Ambition to let anyone publish skills via `SKILL.md`, but implementation gaps (driftnet, metadata handling) remain.
- **Force reply to originating channel** (#54531) – Users want responses to be sent back to Telegram/Discord/WhatsApp even when the agent talks in other contexts.
- **Persistent task‑status surface for long‑running turns** (#52640) – Seeing typing indicators isn’t enough; users want a definitive status panel.
- **Context Provenance metadata** (#54373) – Ability to distinguish injected context (SOUL.md, memory) from fresh data in the prompt.
- **Unbypassable outbound policy enforcement** (#56349) – A single pre‑send validation boundary across all delivery paths.

**Predictions for next version:** Given the QA‑focused betas and the high volume of session‑related bugs, the next stable release will likely include:
- Improved session persistence and recovery (PR #79910, #80615)
- Robust Telegram/WhatsApp reply routing (PR #54531 related)
- Config validation enhancements (PR #79826)
- Possibly the first step toward ClawHub 2.0 if community pressure continues.

---

## 7. User Feedback Summary

**Pain points (most frequently reported):**
- **Regressions after minor upgrades** – Several users note that v2026.03.22 and v2026.5.2 broke previously working workflows (session discovery, agent responsiveness). Frustration level is high (#52875, #76877, #51871).
- **Hardcoded paths** – The incident with `wangtao`’s work path in production code (#51429) has significantly eroded user trust in code review quality.
- **Complex configuration drift** – Issues like `$XDG_CONFIG_HOME` not expanded (#53628) and doctor warnings that cannot be auto‑fixed (#50561) create friction for new users.
- **Server/process hangs** – Reports of unbounded memory growth (#55334), frozen event loops (#56733), and retry storms (#56096) indicate reliability bottlenecks.

**Satisfaction signals:**
- Users on RISC‑V (#54253) and with esoteric setups express enthusiasm for the platform but hit roadblocks.
- The Feishu community is engaged (multiple Feishu bugs reported), showing growing international adoption.
- Several PR authors (e.g., from ClawOps, community contributors) are actively building on OpenClaw, indicating a healthy extension ecosystem despite ClawHub struggles.

---

## 8. Backlog Watch

Issues and PRs that are high‑impact but have been open for months without maintainer response or progress:

- **[#44431 – Browser tool: 7 improvements from real-world automation field test](https://openclaw/openclaw/issues/44431)**  
  Opened 2026-03-12, 5 comments, no assigned milestone. Contains concrete, actionable improvements (CSS selector support, session reuse, etc.) – yet stalled for 2 months.

- **[#48003 – Steer mode does not inject messages mid‑turn for main sessions](https://openclaw/openclaw/issues/48003)**  
  Opened 2026-03-16, 7 comments. Reported as a regression from a March 3 commit. Still open with no fix PR.

- **[#50642 – macOS node auto‑trusts first TLS certificate](https://openclaw/openclaw/issues/50642)**  
  Critical security bug (CVSS 9.0) reported 2026-03-19. No maintainer comment or fix. This is a major liability.

- **[#50630 – Tailscale serve + auth.mode=none exposes gateway to full Tailnet](https://openclaw/openclaw/issues/50630)**  
  Same author, same severity, also untouched since March 19.

- **[#56420 – fix: bind Claude permission replies to session](https://openclaw/openclaw/pull/56420)**  
  Open since 2026-03-28, security‑related PR. Not merged; comment count undefined (likely 0). Needs review.

- **[#50090 – Community Skill Development & ClawHub](https://openclaw/openclaw/issues/50090)**  
  Not a bug but a feature with high community interest. No assigned milestone, no roadmap response from maintainers.

**Recommendation:** Maintainers should prioritize triage on the two CVSS 9+ security issues, the hardcoded path incident (which signals process‑level problems), and the stalled browser tool improvements to regain community confidence.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem
**Analysis Date:** 2026-05-11

---

## 1. Ecosystem Overview

The personal AI agent open-source landscape is experiencing explosive growth, with over a dozen actively maintained projects competing to define the standard architecture for autonomous, multi-platform agents. The ecosystem is bifurcating into two tracks: **heavyweight reference implementations** (OpenClaw, IronClaw) that prioritize extensibility and community plugin ecosystems, and **lightweight, opinionated alternatives** (NanoBot, NanoClaw, Hermes Agent) that focus on immediate usability and specific provider integrations. A critical pattern emerging across all projects is the tension between rapid feature iteration and stability—most projects are shipping daily betas while accumulating regressions in session management, provider authentication, and message delivery. The landscape strongly favors projects that can balance architectural ambition with reliable core loop execution, as user trust erodes quickly when upgrades break existing workflows.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Score |
|---------|----------------------|-------------------|---------------|--------------|
| **OpenClaw** | 500 | 500 | ✅ 3 betas (v2026.5.10-beta.1/2/3) | High velocity, **strained** (393 open issues, CVSS 9.0 security bug unsolved) |
| **IronClaw** | 25 | 46 | ❌ | **High** — 19 PRs merged, focused Reborn rewrite progressing, but ENGINE_V2 bugs emerging |
| **CoPaw** | 31 | 31 | ❌ | **High** — 15 PRs merged, 12 issues closed, strong community contributions |
| **ZeroClaw** | 11 | 38 | ❌ | **High** — 9 PRs merged, trending toward v0.8.0 release |
| **Hermes Agent** | 50 | 50 | ❌ | **Medium-High** — 6 PRs merged, but 44 open PRs and critical OAuth bug unresolved (17 days) |
| **NanoBot** | 12 | 17 | ❌ | **Medium** — 6 PRs merged, but 2 high-severity bugs with no fix PRs |
| **PicoClaw** | 6 | 21 | ✅ Nightly (v0.2.8-nightly) | **Medium** — 6 PRs merged, steady progress on streaming/MCP UI |
| **NanoClaw** | 18 | 23 | ❌ | **Medium-High** — 11 PRs merged, focused on container/poll-loop stability |
| **NullClaw** | 2 | 7 | ❌ | **Medium** — 2 PRs merged, rapid fix for siliconflow regression, but low community engagement |
| **LobsterAI** | 1 | 29 | ❌ | **Medium** — 29 PRs merged (bulk bug fixes), but core NO_REPLY bug (#1849) still open |
| **ZeptoClaw** | 0 | 1 | ❌ | **Low activity** — Single internal refactor PR, no community interaction |
| **Moltis** | 1 | 1 | ❌ | **Stable, quiet** — One dependency fix merged |
| **TinyClaw** | 0 | 0 | ❌ | **Inactive** (no changes in 24h) |

**Notes on Health Scoring:** Based on ratio of closed to open issues, security bug response time, community engagement, and stability indicators. "Strained" denotes high activity with accumulating unresolved critical issues.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Largest community by orders of magnitude** (500+ daily active issues/PRs vs. ~30–50 for most peers). This creates unmatched plugin ecosystem potential ("ClawHub" aspiration) and faster bug discovery.
- **First-mover status** as the core reference implementation—most derivatives (NanoClaw, PicoClaw, ZeptoClaw) explicitly fork or extend OpenClaw conventions. This establishes OpenClaw as the de facto standard for session management, tool routing, and gateway architecture.
- **Aggressive QA automation investment** (Telegram-based evidence capture for PRs, Convex-leased credentials) indicates a maturing testing culture that peers lack.
- **Three beta releases in one day** demonstrates release velocity unmatched by any other project.

**Key Technical Differences:**
- OpenClaw is the only project shipping **three simultaneous beta versions** with build-toolchain hardening (Vitest lint rules, TypeScript strict checks). This signals a focus on developer experience and code quality at scale.
- The **CVSS 9.0 TLS auto-trust vulnerability** (#50642) is unique to OpenClaw—no other project has reported a similar macOS-specific security risk. This may reflect OpenClaw's more complex certificate handling.
- OpenClaw's **session transcript streaming** (PR #80615) is a distinctive architectural choice to address memory scaling—alternatives like NanoBot use summary-based approaches (PR #3711).

**Community Size Comparison:**
| Metric | OpenClaw | Next Largest (IronClaw) |
|--------|----------|------------------------|
| Daily active issues | 500 | 25 |
| Daily active PRs | 500 | 46 |
| Open issues | 393 | N/A (not reported) |
| Community contributors per day | High (69 PRs merged) | Moderate (19 merged) |
| Security issues (CVSS 9+) | 2 open, no fix | 0 reported |

**Weakness:** OpenClaw's scale creates a **quality-control bottleneck**—the hardcoded path incident (#51429, `/Users/wangtao` in production code) and the ~393 open issues suggest the review process cannot keep pace with contribution volume. By comparison, smaller projects like NanoClaw can merge 11 PRs in a day with apparently better outcomes.

---

## 4. Shared Technical Focus Areas

These requirements are emerging independently across multiple projects, indicating industry-wide priorities:

### Session & Memory Management
| Requirement | Projects Affected | Specific Needs |
|-------------|------------------|----------------|
| **Reliable session persistence** | OpenClaw (#52875), NanoClaw (#2393), LobsterAI (#1849), CoPaw (#3843) | Agent-to-agent discovery, message delivery guarantees, recovery after upgrades |
| **Memory governance** | NanoBot (#3744 session-level USER.md/MEMORY.md), CoPaw (#4208 mem0 support), PicoClaw (#2847 agent self-evolution), IronClaw (storage substrate PR #3421) | Per-user memory isolation, automatic summarization, context size management |
| **Streaming stability** | ZeroClaw (#6034 user message loss), PicoClaw (#2674 Codex OAuth empty responses), LobsterAI (#1908 text merge bug) | Consistent token streaming across providers, no dropped characters/images |

### Provider & Authentication
| Requirement | Projects Affected | Specific Needs |
|-------------|------------------|----------------|
| **OAuth credential compatibility** | OpenClaw (#15080 Claude Max 400 error), Hermes Agent (#14637 OpenRouter 401), PicoClaw (#2674 Codex OAuth), NanoClaw (#2401 MITM errors) | Working integration with Anthropic, OpenAI, OpenRouter paid subscriptions from `~/.claude/credentials.json` |
| **Custom / local provider support** | NanoClaw (#1984 local OpenAI-compat endpoints), ZeroClaw (#6034 Qwen provider), Hermes Agent (#23158 NVIDIA URL not recognized) | Routing to non-blessed provider endpoints documented in SKILL.md |
| **Fallback / failover** | CoPaw (#4011, #4181), Hermes Agent (#19691 docs stale) | Automatic model fallback on timeout/rate limit, documented fallback configuration |

### Messaging Platform Parity
| Requirement | Projects Affected | Specific Needs |
|-------------|------------------|----------------|
| **Telegram reliability** | OpenClaw (#52130 restart storm), PicoClaw (#2849 guest mode), ZeroClaw (#6565 inline keyboard cleanup), Hermes Agent (#5394 thread-bound runtimes) | Connection resilience, thread/session binding, tool-approval UX |
| **Feishu/Lark integration** | OpenClaw (#53486 card JSON regression), Hermes Agent (#23732 wrong chat routing, #23488 CardKit), CoPaw (multiple Feishu fixes) | Card formatting, reply routing, multi-instance support |
| **Slack thread history** | IronClaw (#2066 thread fetch), OpenClaw (Slack bridging) | Bot context in threads without prior participation |
| **WeChat / WeCom support** | Hermes Agent (WeCom), NanoBot (#3737 WeChat file name), CoPaw (WeCom fixes) | File handling, message format compatibility |

### Infrastructure & Build Reliability
| Requirement | Projects Affected | Specific Needs |
|-------------|------------------|----------------|
| **CI stability** | ZeroClaw (#6530 matrix-sdk recursion), NanoClaw (#2402 CI silent no-op), IronClaw (#3447 nightly E2E failure) | Predictable builds across platforms, automated smoke tests after dependency bumps |
| **Container build integrity** | Moltis (#988 discrawl path), NanoClaw (#2380 sandbox crash, #2381 update breaks containers), ZeroClaw (container docs PR #6570) | Reliable container images, smooth update paths |
| **Cross-platform testing** | Hermes Agent (#11645 pytest EMFILE on macOS), ZeroClaw (#6562 NixOS module) | Test matrix coverage for macOS ARM64, Linux, Windows, NixOS |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | CoPaw | NanoBot | Hermes Agent | ZeroClaw |
|-----------|----------|----------|-------|---------|--------------|----------|
| **Core philosophy** | Reference/ecosystem hub | Production-quality rewrite | Enterprise IM integration | Beginner-friendly, stable provider expansion | Multi-platform gateway | Consolidation for v0.8 release |
| **Target user** | Power users, plugin devs | Self-hosters, deployers | Chinese enterprise teams | Individual developers | Power users with paid subscriptions | Self-hosters, Linux/NixOS users |
| **Architecture** | Monolithic with plugin system | Modular Rust rewrite (Reborn) | AgentScope framework | Node.js with provider abstraction | Gateway-centric | Tool wrapper/debt reduction |
| **Release cadence** | Daily betas | Reborn in development | Frequent patches | No releases this week | No releases this week | Prepping v0.8 integration |
| **Community contribution model** | Open, high volume, quality issues | Contributor-driven (Slack, mobile) | First-time contributor friendly | PRs reviewed quickly | High open PR backlog | Needs maintainer review |
| **Security posture** | 2 open CVSS 9+ bugs | None reported | MD5→SHA-256 migration in progress | No critical reported | 17-day unresolved OAuth bug | No critical reported |
| **Distinctive features** | ClawHub ecosystem (WIP), Telegram QA automation | Reborn binary, Slack thread history, i18n (CN/EN) | Multi-IM (POPO, Feishu), memory dreaming | DuckDuckGo search, context compression | Claude Max OAuth, remote management API | Matrix-sdk bump, native Responses API |
| **Geographic focus** | Global | Global (US/Europe) | China-dominant (WeChat, DingTalk, Feishu) | China (DeepSeek, VolcEngine, LongCat) | Global | Global with NixOS community |

**Key Insight:** The ecosystem is **not converging**—projects are diverging on architecture (Rust rewrite vs. Node.js monolith vs. Python framework), target markets (China IM vs. global Slack/Telegram), and stability philosophy (daily shipping vs. cautious consolidation). This fragmentation suggests the "standard platform" has not yet been established.

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity, Potentially Unstable
| Project | Signal | Risk |
|---------|--------|------|
| **OpenClaw** | 500 daily issues/PRs, 3 betas/day | Quality control overwhelmed (393 open issues, production hardcoded path) |
| **IronClaw** | 19 merged PRs/day, Reborn rewrite progressing | ENGINE_V2 bugs (image rendering, repeated tool calls) showing new engine churn |
| **CoPaw** | 15 merged PRs, 12 closed issues, strong first-time contributor pipeline | Session history bug was critical; auto-memory feature still maturing |

### Tier 2: Steady, Growing, More Stable
| Project | Signal | Maturity Indicator |
|---------|--------|-------------------|
| **ZeroClaw** | 9 merged PRs, trending toward v0.8 release, tool wrapper migration completed | Consolidation phase before major release; lower open issue count |
| **NanoBot** | 6 merged PRs, provider expansion (LongCat, NVIDIA, MiMo disable) | Growing provider diversity; 2 high-severity bugs without fixes indicate needed attention |
| **PicoClaw** | 6 merged PRs, new releases (nightly), Slack webhook, MCP UI | Steady feature addition with nightly builds; cloud credentials gap blocks some users |
| **NanoClaw** | 11 merged PRs, container stability focus, CLI hardening | Rapid iteration on infrastructure; container crashes and mont issues for new users |

### Tier 3: Low Activity or Stabilizing
| Project | Signal | Reason |
|---------|--------|--------|
| **Hermes Agent** | 44 open PRs, 6 merged, critical OAuth bug open 17 days | Maintainer bandwidth constrained despite high contribution volume |
| **NullClaw** | 2 merged PRs, low community engagement | Small team, focused on incremental improvements (Discord, cron) |
| **LobsterAI** | 29 merged PRs (bulk fix day), then quiet | Appears to be clearing a bug backlog; core NO_REPLY bug remains |
| **ZeptoClaw** | 1 open PR (internal refactor), no issues | Long-running pipeline refactor; no community signals |
| **Moltis** | 1 dependency fix merged, no other activity | Stable but essentially dormant |
| **TinyClaw** | No activity | Effectively inactive |

### Community Effort Distribution
```
OpenClaw   ████████████████████████████████████ 500/500 issues/PRs
IronClaw   ████ 46/25
CoPaw      ███ 31/31
ZeroClaw   ███ 38/11
Hermes     ███ 50/50
NanoBot    █ 17/12
PicoClaw   █ 21/6
NanoClaw   █ 23/18
Others     ▏ 1–7 each
```

OpenClaw commands ~80% of the ecosystem's visible activity, but this does not correlate linearly with output quality or user satisfaction.

---

## 7. Trend Signals

### Emerging Industry Trends

**1. Upgrade Regression is the #1 User Frustration**
Across projects, users consistently report that **minor version upgrades break previously working workflows**:
- OpenClaw: "session_send fails after upgrade" (#52875, regression since March 22), "agents stop responding mid-work" (#76877, regression since April 23)
- NullClaw: `HostResolutionFailed` after upgrading to 2026.5.x (#902)
- CoPaw: Cron jobs interrupted after unknown upgrade (#2429)
- ZeroClaw: Bulk revert lost 153 commits (#6074)

**Implication for developers:** A must-have capability for any production deployment is **gradual rollout** (canary testing, rollback support) and **configuration snapshots** tied to versions. The ecosystem currently lacks this—projects ship daily betas without migration tests.

**2. Multi-Provider Flexibility is Non-Negotiable**
Users demand the ability to switch providers **per-session or per-query**, not just at startup:
- NanoBot: `/model` slash command requested (#3742) due to network instability in China
- Hermes Agent: `max_tokens` configurable per profile (#22879)
- ZeroClaw: ComfyUI as media provider (#6563), SearXNG as search fallback (#5316)
- CoPaw: Model failover (#4011, #4181) top-voted feature

**Trend:** The "one model" era is ending. Agents must be **provider-agnostic** with dynamic routing, automatic fallback, and per-request model selection. This is especially critical for enterprise and China-market deployments.

**3. Observability is the New Frontier**
Multiple projects are independently developing token usage tracking, cost dashboards, and performance statistics:
- NanoBot: `/insights` command (PR #3735) for cumulative token/cost tracking
- NullClaw: Performance statistics report requested (#909)
- CoPaw: AI diagnostics for email failures (#1916)
- OpenClaw: Session transcript streaming (#80615) enables analytics

**Implication:** As AI agents become cost-bearing (pay-per-token), **spending visibility** becomes a prerequisite for adoption. Expect agent-specific logging and monitoring tools to emerge as a category.

**4. Memory is Becoming a First-Class Feature**
Every major project is adding or refactoring memory systems:
- CoPaw: Auto-memory management (#4204), mem0 integration request (#4208)
- NanoBot: Session-level memory (#3744), archived summaries in system prompt (#3711)
- PicoClaw: Agent self-evolution (#2847) clustering successful task patterns
- IronClaw: Shared storage substrate (#3421), blob/record store traits
- Hermes Agent: Session recall tools (#23689), compression fallback (#16670)

**Trend:** Long-term memory is shifting from "nice to have" to **core architectural component**. The winning projects will offer pluggable memory backends (vector DB, append-only files, cloud storage) with automatic summarization and retrieval.

**5. Mobile and IM Integration is Driving Adoption**
The most active feature PRs and community contributions revolve around messaging platform parity:
- Telegram: Thread-bound runtimes (Hermes #5394), guest/business modes (PicoClaw #2849/#2845), inline keyboard cleanup (ZeroClaw #6565)
- Feishu/Lark: CardKit support (Hermes #23488), wrong chat routing fix (Hermes #23732)
- Slack: Thread history fetch (IronClaw #2066), pairing via chat (IronClaw #3396)
- Mobile UI: Hamburger drawer (IronClaw #2935), mobile layout refinements (IronClaw #3461)

**Implication:** The "personal AI assistant" is primarily accessed via **messaging apps**, not web UIs or CLI. Projects that optimize for chat platform UX (inline keyboards, thread management, media handling) will win end-user adoption.

**6. Security Debt Accumulates Faster Than Fixes**
Critical security issues remain open for weeks:
- OpenClaw: TLS auto-trust (CVSS 9.0, open since March 19, #50642), Tailscale auth bypass (CVSS 9.3, same date, #50630)
- CoPaw: MD5→SHA-256 migration PR open since May 10 (#4180)
- Hermes Agent: OpenRouter auth fixed, but Anthropic OAuth (#15080) open 17 days
- ZeroClaw: Lost commits audit (#6074) unresolved

**Risk:** The ecosystem's rapid shipping cadence is **outpacing security review**. For developers evaluating these projects, a security audit should be a prerequisite for production deployment. OpenClaw's scale makes it the highest-risk target.

**7. China Market is an Independent Innovation Hub**
Projects like **CoPaw** (Netease Youdao), **NanoBot** (HKU DS), and **LobsterAI** are innovating independently from Western projects:
- CoPaw's IM-first architecture (DingTalk, Feishu, POPO, WeCom) with features like memory dreaming and automatic extraction
- NanoBot's China-specific providers (LongCat by Meituan, VolcEngine, DeepSeek v4)
- LobsterAI's POPO multi-instance and scheduled task history filtering

**Implication:** The China sub-ecosystem has **different user needs** (WeChat/WeCom integration, network resilience, Chinese language AI models) and is developing solutions that may later influence global projects. Cross-pollination between China and Western projects is minimal currently, suggesting **market-specific fragmentation** will persist.

### Value for AI Agent Developers

1. **Expect instability**: If deploying any of these projects, freeze dependency versions and budget time for upgrade validation. The "daily beta" model is not production-ready without your own testing layer.

2. **Prioritize session reliability**: The most painful bugs across all projects involve lost messages, broken agent-to-agent communication, and session corruption. Invest in monitoring session health.

3. **Plan for multi-model**: Build your agent to support runtime model/provider switching from day one. The days of single-model agents are ending.

4. **Track costs aggressively**: Implement your own token counters and spending dashboards—the project-level solutions are immature.

5. **Choose based on IM ecosystem**: If your users are on Telegram, OpenClaw/NullClaw/PicoClaw. WeChat/Feishu? CoPaw/LobsterAI. Slack/Discord? IronClaw/Hermes. The project's IM support will define your user experience more than any other feature.

6. **Security hygiene is on you**: Do not assume timely security patches—particularly from the highest-velocity projects. Plan to review and patch critical CVEs yourself.

---

*Analysis generated 2026-05-11 from community digest summaries of 13 open-source AI agent projects. Data reflects single-day snapshot; trends may not predict long-term trajectories.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-11

## 1. Today's Overview

May 11 saw elevated activity with **12 issues** and **17 pull requests** updated in the last 24 hours. Eight issues remain open, while four were closed. PR activity was similarly split: 11 open and 6 merged/closed. No new releases were published. The project is processing a steady stream of bug reports and feature contributions, with community attention focused on system-hanging web searches, provider compatibility, and session-level memory. The presence of multiple high-severity bugs (DuckDuckGo hang, context compression crash) suggests stability remains the top concern, although several fixes landed today.

## 2. Releases

No new releases today.

## 3. Project Progress

**6 PRs were merged or closed** today, advancing both fixes and features:

- **WebUI non-secure context fix** – `crypto.randomUUID` shim for LAN access ([PR #3733](https://github.com/HKUDS/nanobot/pull/3733))
- **MiMo reasoning disable** – Wired `thinking_type` to allow disabling reasoning when `reasoning_effort: "none"` ([PR #3734](https://github.com/HKUDS/nanobot/pull/3734), fixes [#3585](https://github.com/HKUDS/nanobot/issues/3585))
- **New provider: LongCat (美团)** – Added OpenAI-compatible provider with models Flash-Chat, Flash-Thinking ([PR #3736](https://github.com/HKUDS/nanobot/pull/3736))
- **New provider: NVIDIA NIM** – Support for NIM’s API endpoint ([PR #3707](https://github.com/HKUDS/nanobot/pull/3707))
- **Configurable CLI bot name and icon** – Added `bot_name` and `bot_icon` under `agents.defaults` in config ([PR #3730](https://github.com/HKUDS/nanobot/pull/3730), fixes [#3650](https://github.com/HKUDS/nanobot/issues/3650))
- **Archived summary moved to system prompt** – Improves KV cache stability by keeping summaries in the system prefix ([PR #3711](https://github.com/HKUDS/nanobot/pull/3711))

These merged PRs indicate progress on provider expansion, UI polish, and memory/cache optimisation.

## 4. Community Hot Topics

| Item | Type | Comments | Reactions | Summary |
|------|------|----------|-----------|---------|
| [#2828 DuckDuckGo web search hangs entire system](https://github.com/HKUDS/nanobot/issues/2828) | Issue (CLOSED) | 5 | 👍 1 | Web search via DuckDuckGo causes entire system to hang—cannot Ctrl+C, cannot force stop from Proxmox. |
| [#3650 Configure bot name and icon](https://github.com/HKUDS/nanobot/issues/3650) | Issue (CLOSED) | 3 | 0 | User wanted `botName` and `botIcon` in config.json; resolved via merged PR #3730 today. |
| [#2829 Ollama tool calling broken](https://github.com/HKUDS/nanobot/issues/2829) | Issue (OPEN) | 2 | 0 | Models like `gemma4:e4b` cannot use tools—makes up answers instead. Open since Apr 5. |
| [#3469 deepseek-v4 API error: `reasoning_content` must be passed back](https://github.com/HKUDS/nanobot/issues/3469) | Issue (CLOSED) | 2 | 0 | Error during multi-turn thinking with DeepSeek-v4; resolved. |

The strongest community reaction centered on the DuckDuckGo hang bug—though closed, it received the most comments and reaction, indicating a desire for a clear solution. The bot name/icon feature was quickly implemented after its request, showing good maintainer responsiveness.

## 5. Bugs & Stability

**Critical/High severity:**
- **DuckDuckGo web search hangs entire system** ([#2828](https://github.com/HKUDS/nanobot/issues/2828)) – Marked CLOSED but without a visible fix PR; users may still be affected if root cause unresolved.
- **Context compression bug causes system crash** ([#3726](https://github.com/HKUDS/nanobot/issues/3726)) – Token consolidation fails with `no safe boundaries` debug messages; agent loop crashes. No fix PR yet.
- **Ollama tool calling broken** ([#2829](https://github.com/HKUDS/nanobot/issues/2829)) – Long-standing bug (since Apr 5) with no PR attached; models fail to use tools.

**Medium severity:**
- **MCP service not started → nanobot agent crash** ([#3739](https://github.com/HKUDS/nanobot/issues/3739)) – When MCP is unreachable, startup fails with error. Coincides with a related PR ([#3740](https://github.com/HKUDS/nanobot/pull/3740)) that probes HTTP port before connecting.
- **WeChat Work file name not recognized** ([#3737](https://github.com/HKUDS/nanobot/issues/3737)) – Filename extraction broken due to SDK download header handling.
- **deepseek-v4 reasoning error** ([#3469](https://github.com/HKUDS/nanobot/issues/3469)) – Already closed.
- **`reasoning_effort: null` not disabling thinking** ([#3585](https://github.com/HKUDS/nanobot/issues/3585)) – Fixed via PR #3734 today.
- **VolcEngine `max_tokens` / `max_completion_tokens` conflict** – Opened as PR #3738 (fix not yet merged).

**Fix PRs in progress:**
- [#3740 (MCP port probe)](https://github.com/HKUDS/nanobot/pull/3740)
- [#3738 (VolcEngine provider fix)](https://github.com/HKUDS/nanobot/pull/3738)
- [#3693 (centralize LLM concurrency gate)](https://github.com/HKUDS/nanobot/pull/3693) – prevents background tasks from overloading local LLMs.

Overall, stability remains a key area; two high-severity issues have no direct fix PR yet.

## 6. Feature Requests & Roadmap Signals

Today’s issues and PRs point to several desired directions:

- **Session-level memory** – Request [#3744](https://github.com/HKUDS/nanobot/issues/3744) asks for separate `USER.md`/`MEMORY.md` per IM user. No PR yet, but memory governance is already under exploration via MGP sidecar ([PR #3408](https://github.com/HKUDS/nanobot/pull/3408)).
- **Slash command to switch model/provider** ([#3742](https://github.com/HKUDS/nanobot/issues/3742)) – Motivated by network instability in China; `/model` would allow dynamic fallback.
- **Provider-hosted web search** ([#3741](https://github.com/HKUDS/nanobot/issues/3741) & [PR #3743](https://github.com/HKUDS/nanobot/pull/3743)) – Opt-in support for native search tools from providers like Azure OpenAI. This aligns with partner requests.
- **Historical token usage tracking** ([#3731](https://github.com/HKUDS/nanobot/issues/3731) & [PR #3735](https://github.com/HKUDS/nanobot/pull/3735)) – `/insights` command to track cumulative usage and cost across sessions. Likely to be reviewed and merged soon given PR is already open.
- **Agent self-correction** – Hooks for loop detection and reflect-retry ([PR #3728](https://github.com/HKUDS/nanobot/pull/3728)) could stabilise iterative workflows.
- **Local voice transcription** ([PR #3723](https://github.com/HKUDS/nanobot/pull/3723)) – Using faster-whisper for offline audio processing; privacy-focused feature for self-hosters.
- **Plugin tool architecture** ([PR #3729](https://github.com/HKUDS/nanobot/pull/3729)) – Refactors tool registration to a self-describing pattern, reducing boilerplate. Likely to reduce maintenance burden.

Of these, `/insights` and provider-hosted web search appear most ready for the next release, while session-level memory and plugin architecture are more foundational.

## 7. User Feedback Summary

Users expressed both satisfaction and frustration:

- **Positive:** Custom bot name/icon feature was requested and implemented within days ([#3650](https://github.com/HKUDS/nanobot/issues/3650)), and the MiMo reasoning toggle fix (#3585) was quickly addressed.
- **Frustration:** The **DuckDuckGo hang** (#2828) and **context compression crash** (#3726) directly block usage. Users cannot gracefully terminate the process or restart without force.
- **Missing tooling:** Chinese users report issues with WeChat Work file handling and MCP startup errors.
- **Cost visibility:** Developers running pay-per-token models want in-app spending insights rather than provider dashboards.
- **Flexibility:** The need to switch providers on-the-fly (/model command) is driven by real regional network instability.

Overall, users value configurability and provider diversity but are impeded by stability regressions in core loops and web search.

## 8. Backlog Watch

The following items require maintainer attention due to age or impact:

- **[#2829 Ollama tool calling broken](https://github.com/HKUDS/nanobot/issues/2829)** – Open since Apr 5, no fix PR. Blocks users of local Ollama models from using tools.
- **[#2828 DuckDuckGo web search hangs system](https://github.com/HKUDS/nanobot/issues/2828)** – Closed but unclear resolution; if not fixed, the community may reopen.
- **[PR #3408 MGP sidecar](https://github.com/HKUDS/nanobot/pull/3408)** – Open since Apr 23, no recent comments. Large feature that may need further design review.
- **[PR #3693 Concurrency gate](https://github.com/HKUDS/nanobot/pull/3693)** – Open since May 8, addresses a frequent crash pattern for local LLM users. May benefit from wider testing.
- **[PR #3728 Agent self-correction hooks](https://github.com/HKUDS/nanobot/pull/3728)** – Open since May 10; valuable for reducing wasted iterations, needs review.
- **[#3737 WeChat Work file name bug](https://github.com/HKUDS/nanobot/issues/3737)** – New but affects Chinese community users; no PR yet.

Maintainers should prioritise patching the high-severity hangs/crashes and reviewing the Ollama tool bug that has lingered for over a month.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-05-11

## 1. Today’s Overview

The Hermes Agent project saw very high activity in the last 24 hours, with **50 issues** and **50 pull requests** updated – of which 37 issues remain open and 44 PRs are open, indicating a vibrant and fast-moving open-source ecosystem. No new release was published today, but the sheer volume of contributions (13 issues closed, 6 PRs merged/closed) suggests steady progress toward the next version. The community is particularly vocal about authentication failures, output truncation, and messaging platform integrations, while maintainers are actively merging fixes for documentation gaps and test regressions.

---

## 2. Releases

*No new releases were published today.*

---

## 3. Project Progress

Today **6 pull requests were merged or closed**, and **13 issues were resolved**. Notable closures include:

- **Bug fixes** – OpenRouter Authentication HTTP 401 (#14637) was closed, indicating a fix for a critical provider authentication path.
- **Documentation improvements** – Several doc-related issues were closed: Node.js version mismatch in CONTRIBUTING (#11684), broken Docker link (#14532), broken Nix anchor (#14595), and missing Flash Attention / SAELens reference docs (#14563, #14562).
- **Test fixes** – A test assertion regression for `fetch_api_models` (#15243) and a Matrix upload test failure (#11679) were resolved.

The 44 open PRs span feature work (Feishu CardKit support, remote management API, LLM runtime overrides, session recall tools) and bug fixes (packaging, terminal hang, image fallback, compressor orphan turns). The high open-PR count reflects rapid concurrent development.

---

## 4. Community Hot Topics

| Issue/PR | Comments | 👍 | Topic |
|----------|----------|----|-------|
| [#7237 [CLOSED]](https://github.com/NousResearch/hermes-agent/issues/7237) | 22 | 4 | **Response truncated due to output length limit** – a long-standing frustration where long-form agent replies are cut off mid-stream. Closed today, suggesting a fix landed. |
| [#15080 [OPEN]](https://github.com/NousResearch/hermes-agent/issues/15080) | 7 | 0 | **Claude Max subscription OAuth token rejected** – despite valid credentials from `~/.claude/.credentials.json`, every Hermes request to Anthropic returns HTTP 400. Users cannot use paid subscriptions. |
| [#14637 [CLOSED]](https://github.com/NousResearch/hermes-agent/issues/14637) | 7 | 1 | **OpenRouter HTTP 401 auth error** – resolved today; users had working API keys but Hermes failed to authenticate. |
| [#21867 [OPEN]](https://github.com/NousResearch/hermes-agent/issues/21867) | 5 | 0 | **Cron tool doesn’t work** – scheduled jobs advance `next_run_at` but never actually execute. Blocks automation use cases. |
| [#5394 [OPEN]](https://github.com/NousResearch/hermes-agent/issues/5394) | 2 | 4 | **Thread-bound agent runtimes for Telegram** – popular feature request to bind Telegram topics to persistent external agent surfaces (like Codex/Claude/Gemini). |

**Underlying needs:**  
- Users want reliable, uninterrupted long-form responses from the agent (#7237).  
- Provider authentication flows (Anthropic, OpenRouter) must work seamlessly with existing credential files (#15080, #14637).  
- Automation (cron) is a core use case that is currently broken (#21867).  
- Multi-platform gateway users (Telegram, Feishu, LINE) are driving integration and configuration improvements.

---

## 5. Bugs & Stability

**High severity (P1):**  
- [#15080](https://github.com/NousResearch/hermes-agent/issues/15080) – **Anthropic OAuth 400 on Claude Max subscription** – blocks all users with paid Anthropic accounts. No fix PR visible yet.

**Medium severity (P2):**  
- [#21867](https://github.com/NousResearch/hermes-agent/issues/21867) – **Cron tool non-functional** – jobs never run. No associated fix PR.  
- [#23694](https://github.com/NousResearch/hermes-agent/issues/23694) – **Windows CLI hang on destructive slash commands** (`/new`, `/clear`) – confirmation prompt freezes terminal (Windows beta).  
- [#23732](https://github.com/NousResearch/hermes-agent/issues/23732) – **Feishu messages sent to wrong chat** – reply routing broken when using home channel.  
- [#23613](https://github.com/NousResearch/hermes-agent/issues/23613) – **Atomic file writes leave new files at `0o600`** – permission leak for shared environments.  
- [#23728](https://github.com/NousResearch/hermes-agent/issues/23728) – **LINE adapter crash** (`AttributeError: 'LineAdapter' object has no attribute 'create_source'`) – newly merged adapter is non-functional.  
- [#23158](https://github.com/NousResearch/hermes-agent/issues/23158) – **NVIDIA base URL not recognized** – cannot add NVIDIA as provider via CLI.

**Low severity (P3):**  
- [#23620](https://github.com/NousResearch/hermes-agent/issues/23620) – **Kanban dashboard `COLUMN_LABEL` undefined** in aria-label.  
- [#23724](https://github.com/NousResearch/hermes-agent/issues/23724) – **Hindsight plugin resends full transcript** on every retain, duplicating content.  
- [#23741](https://github.com/NousResearch/hermes-agent/issues/23741) – **`/sessions` slash command registered but no dispatcher** – triggers “Unknown command”. A fix PR [#23745](https://github.com/NousResearch/hermes-agent/pull/23745) is already open.

**Known recurring issues:**  
- Nix build failures due to stale `npmDepsHash` (#15244, recurrence of #12965) – closed today.  
- `pytest -n auto` EMFILE on macOS (#11645) – still open.

---

## 6. Feature Requests & Roadmap Signals

**Top user-requested features (high engagement):**  
- [#5394](https://github.com/NousResearch/hermes-agent/issues/5394) – **Thread-bound agent runtimes for Telegram** (4 👍). Likely to be considered for a future gateway overhaul.  
- [#12688](https://github.com/NousResearch/hermes-agent/issues/12688) – **Configurable command prefix** for Matrix/Mattermost (where `/` is reserved). A small but impactful quality-of-life change.  
- [#22879](https://github.com/NousResearch/hermes-agent/issues/22879) – **`max_tokens` configurable per profile** – currently hardcoded to model maximum, causing OpenRouter HTTP 402. Highly requested for power users.

**Features appearing in today’s PRs (likely for next release):**  
- **Feishu CardKit support** ([#23488](https://github.com/NousResearch/hermes-agent/pull/23488)) – richer message formatting for Feishu/Lark.  
- **Remote management API endpoints** ([#23742](https://github.com/NousResearch/hermes-agent/pull/23742)) – enables external dashboard/desktop clients.  
- **Pre-LLM-call runtime overrides** ([#23744](https://github.com/NousResearch/hermes-agent/pull/23744)) – plugin hook for dynamic LLM configuration.  
- **Session recall tools** ([#23689](https://github.com/NousResearch/hermes-agent/pull/23689)) – read-only forensic recall over `state.db`.  
- **Clarify tool bridging to messaging platforms** ([#23740](https://github.com/NousResearch/hermes-agent/pull/23740)) – makes the clarify tool work on Telegram/Discord/Slack.  
- **Feishu threaded replies** ([#22539](https://github.com/NousResearch/hermes-agent/pull/22539)) – default to threads in group chats.  

**Roadmap signal:** The project is heavily investing in messaging platform parity (Feishu, LINE, WeCom) and external API management, while also improving plugin extensibility.

---

## 7. User Feedback Summary

**Pain points (explicit user reports):**

- **Authentication friction** – Users with valid Claude Max OAuth tokens (#15080) or OpenRouter API keys (#14637, now fixed) cannot use their paid subscriptions. This causes frustration and support churn.  
- **Output truncation** (#7237, now closed) – Long agent responses are cut off, breaking the conversation flow.  
- **Cron unreliability** (#21867) – Scheduled tasks are a core automation need; the current broken state limits use cases.  
- **Windows support** (#23694) – Terminal hangs on `/new`/`/clear` make the Windows CLI beta nearly unusable for session management.  
- **Packaging gaps** – Homebrew formula (#19690) is stale (points to 0.6.0 with placeholder SHA256); pip wheel missing bundled skills (#23738, now fixed in PR). Early adopters face installation friction.  
- **Documentation inconsistencies** – Missing reference docs (#14563, #14562), stale config paths (#19691), and Node.js version mismatch (#11684) create onboarding barriers.

**Satisfaction signals:**  
- Rapid issue closure (13 issues closed today) indicates responsive maintainers.  
- High PR volume (44 open) suggests strong community contributor momentum.  
- Popular feature requests (e.g., Telegram thread binding, #5394) have been open for over a month and still attract new votes, showing sustained interest.

---

## 8. Backlog Watch

Issues that remain open for more than a week and appear to need maintainer attention:

| Issue | Age | Priority | Status |
|-------|-----|----------|--------|
| [#15080](https://github.com/NousResearch/hermes-agent/issues/15080) – Anthropic OAuth 400 | Created 2026-04-24 (17 days) | P1 | No fix PR; blocks paid Anthropic users. |
| [#21867](https://github.com/NousResearch/hermes-agent/issues/21867) – Cron not working | Created 2026-05-08 (3 days) | P2 | No fix PR; core automation feature broken. |
| [#16670](https://github.com/NousResearch/hermes-agent/issues/16670) – Compression fallback loses context | Created 2026-04-27 (14 days) | P2 | No fix PR; affects long sessions. |
| [#5394](https://github.com/NousResearch/hermes-agent/issues/5394) – Telegram thread-bound runtimes | Created 2026-04-06 (35 days) | P3 | Popular feature; no assignee. |
| [#11645](https://github.com/NousResearch/hermes-agent/issues/11645) – pytest EMFILE on macOS | Created 2026-04-17 (24 days) | P3 | Affects contributor workflows. |
| [#19690](https://github.com/NousResearch/hermes-agent/issues/19690) – Stale Homebrew formula | Created 2026-05-04 (7 days) | P3 | No fix PR; blocks Homebrew installs. |
| [#19691](https://github.com/NousResearch/hermes-agent/issues/19691) – Fallback provider docs stale | Created 2026-05-04 (7 days) | P3 | No fix PR; confusing for users. |

**Critical watch item:** #15080 (Anthropic OAuth) is P1, unresolved, and affects a significant portion of users (Claude Max subscribers). The project should prioritize either a fix or a workaround guide.

---

*Digest generated from GitHub data refreshed 2026-05-11. All linked issues/PRs are from the [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) repository.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-11

## 1. Today's Overview

Activity remains high with **6 issues updated** (5 open, 1 closed) and **21 pull requests touched** (15 open, 6 merged/closed) in the last 24 hours. A new **nightly build (v0.2.8-nightly)** was released, incorporating recent `main` branch changes. The project is seeing steady progress on core infrastructure (streaming, model management, MCP UI) alongside several bug fixes. Community engagement is active, particularly around cloud provider credentials and OAuth streaming issues.

## 2. Releases

- **`nightly`** — v0.2.8-nightly.20260511.6e6293e5 (automated build, may be unstable)  
  [GitHub Release](https://github.com/sipeed/picoclaw/releases/tag/v0.2.8-nightly.20260511.6e6293e5)  
  Full changelog: [v0.2.8…main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
  No breaking changes or migration notes are documented for this nightly.

## 3. Project Progress

Six PRs were merged or closed today, advancing several features and fixes:

- **#2831** (closed) — Foundation for improved model configuration: CRUD model endpoints, provider metadata, and UI form components (part 1 of 3 from #2752).  
- **#2719** (closed) — New `slack_webhook` output-only channel with Block Kit formatting and multi-target support.  
- **#2847** (closed) — Agent self-evolution foundation: a safe loop that records successful task outcomes, clusters patterns, and generates candidate skill drafts.  
- **#2783** (closed) — Fixes media store alignment after gateway reload, preventing stale references.  
- **#2645** (closed) — Real-time token streaming via `StreamingProvider` for the AWS Bedrock provider using ConverseStream API.  
- **#2770** (closed) — Dedicated MCP section in the web config UI, enabling enable/discovery settings and server management without raw config editing.

Additionally, issue **#2780** (voice recognition broken after config reload) was closed today, likely resolved by the media store fix or a parallel change.

## 4. Community Hot Topics

- **Issue #2225** — [Ollama cloud credentials](https://github.com/sipeed/picoclaw/issues/2225) (11 comments, open since March)  
  Users request credential support for Ollama Cloud. No maintainer acknowledgment yet. This reflects a growing demand for managed cloud provider integration.

- **Issue #2674** — [Codex OAuth empty response](https://github.com/sipeed/picoclaw/issues/2674) (3 👍, 3 comments)  
  Assistant responses come back empty when using the ChatGPT Codex OAuth backend. The fallback “empty response” error is triggered even when streaming items are received. Underlying need: stable streaming support for OpenAI OAuth providers.

- **Issue #2720** — [Singleton PID check bug](https://github.com/sipeed/picoclaw/issues/2720) (stale, 2 comments)  
  Gateway fails to start when a stale PID file points to an unrelated process. The singleton check does not verify process identity.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **High** | [#2674](https://github.com/sipeed/picoclaw/issues/2674) (open) | Codex OAuth: empty assistant response when streaming items arrive via `response.output_item.done` | No fix PR yet; PR #2462 (also stale) may address this |
| **Medium** | [#2749](https://github.com/sipeed/picoclaw/issues/2749) (open) | Bash tool evaluates relative paths as absolute, breaking workspace restrictions | PR #2826 (open) and PR #2750 (open) both address this |
| **Medium** | [#2720](https://github.com/sipeed/picoclaw/issues/2720) (open) | Stale PID causes crash loop on gateway start | No fix PR yet |
| **Low** | [#2780](https://github.com/sipeed/picoclaw/issues/2780) (closed) | Voice recognition broke after reloading config (resolved) | Closed, probably fixed by #2783 or related changes |

## 6. Feature Requests & Roadmap Signals

- **Diff preview for `edit_file` tool** ([#2848](https://github.com/sipeed/picoclaw/issues/2848)) — Opened today, requests a unified diff preview similar to Claude Code CLI. Likely to be prioritized given tool usability improvements.
- **Ollama cloud credentials** ([#2225](https://github.com/sipeed/picoclaw/issues/2225)) — High community interest, may land in next minor release if maintainer picks it up.
- **Telegram guest mode** ([#2849](https://github.com/sipeed/picoclaw/pull/2849)) and **Telegram business mode** ([#2845](https://github.com/sipeed/picoclaw/pull/2845)) are open PRs, signaling expanded channel support.
- **Agent self-evolution** ([#2847](https://github.com/sipeed/picoclaw/pull/2847)) was merged today, so its config UI and documentation ([#2852](https://github.com/sipeed/picoclaw/pull/2852)) are likely next for the web interface.
- **Per-message timestamps** ([#2788](https://github.com/sipeed/picoclaw/pull/2788)) is still open, improving session history accuracy.

## 7. User Feedback Summary

- **Pain points**  
  - Cloud provider credentials (Ollama) missing → blocks cloud-only users.  
  - Codex OAuth streaming breaks entirely → makes ChatGPT backend unusable for many.  
  - Relative path resolution in the `bash` tool forces users to workaround workspace restrictions.  
  - Config reload breaks voice recognition (now fixed).  

- **Satisfaction indicators**  
  - Positive engagement: PRs for Slack webhook, MCP UI, and Bedrock streaming were merged, addressing real integration needs.  
  - The community is contributing proactively (e.g., Yocto layer documentation PR #2851, feishu fix #2846).

## 8. Backlog Watch

The following issues and PRs have been **stale for over a week** and may need maintainer attention:

| Item | Age | Why important |
|------|-----|---------------|
| [#2225](https://github.com/sipeed/picoclaw/issues/2225) (issue) | 41 days | Ollama cloud credentials – high community demand |
| [#2720](https://github.com/sipeed/picoclaw/issues/2720) (issue) | 11 days | Singleton PID crash – blocks startup on some systems |
| [#2749](https://github.com/sipeed/picoclaw/issues/2749) (issue) | 9 days | Bash relative path bug – affects tool safety |
| [#2462](https://github.com/sipeed/picoclaw/pull/2462) (PR) | 32 days | Codex streaming + Telegram duplicate retries (stale, but may fix #2674) |
| [#2696](https://github.com/sipeed/picoclaw/pull/2696) (PR) | 13 days | Per-request dynamic MCP headers from channel context |
| [#2750](https://github.com/sipeed/picoclaw/pull/2750) (PR) | 9 days | Alternative fix for relative path bug |
| [#2788](https://github.com/sipeed/picoclaw/pull/2788) (PR) | 5 days | Per-message timestamps for session API |

*All data sourced from the PicoClaw GitHub repository ([sipeed/picoclaw](https://github.com/sipeed/picoclaw)) as of 2026-05-11.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-11

## Today’s Overview

NanoClaw saw a surge of activity on May 10–11, with **18 issues updated** (16 open, 2 closed) and **23 PRs updated** (12 open, 11 merged/closed). The project had no new releases. The day was dominated by **stability fixes** for the poll-loop and container infrastructure, **CLI hardening** (scope enforcement, missing commands), and **CI/onboarding improvements** following the repository rename from `qwibitai/nanoclaw` to `nanocoai/nanoclaw`. A significant portion of the open PRs target message delivery reliability after compaction. Overall project health is **highly active but with notable bugs** around agent message wrapping, container image staleness, and new-user setup friction.

## Releases

*No new releases were published in the last 24 hours.*

## Project Progress

**Merged/Closed PRs (11 items):** All originated from maintainers and regular contributors.

- **Container stability:**
  - [PR #2410](https://github.com/nanocoai/nanoclaw/pull/2410) — Graceful handling of missing `on_wake` column in container’s read-only `inbound.db` (prevented restart loop).
  - [PR #2399](https://github.com/nanocoai/nanoclaw/pull/2399) — Made the `claude` binary resolvable from `agent-runner`; fixes first-message failure with the default Claude provider.
  - [PR #2330](https://github.com/nanocoai/nanoclaw/pull/2330) — Made axios-based MCP servers work through OneCLI’s CONNECT-only proxy.
  - [PR #2384](https://github.com/nanocoai/nanoclaw/pull/2384) — Teach the agent to use OneCLI gateway credentials after MCP server install (stops fabricating manual OAuth instructions).

- **CLI & security:**
  - [PR #2392](https://github.com/nanocoai/nanoclaw/pull/2392) — Fail-closed scope enforcement on `sessions-get` and `ResourceDef` – two hardening fixes from security review.
  - [PR #2356](https://github.com/nanocoai/nanoclaw/pull/2356) — `update-nanoclaw` now installs `~/.local/bin/ncl` symlink on upgrade (fixes missing CLI after update).

- **CI & repository migration:**
  - [PR #2408](https://github.com/nanocoai/nanoclaw/pull/2408) — Renamed remaining `qwibitai/nanoclaw` references to `nanocoai/nanoclaw`.
  - [PR #2402](https://github.com/nanocoai/nanoclaw/pull/2402) — Fixed CI workflows that silently no-op after repo rename.
  - [PR #2400](https://github.com/nanocoai/nanoclaw/pull/2400) — Updated `CONTRIBUTING.md` repo references.

- **Docs:**
  - [PR #2407](https://github.com/nanocoai/nanoclaw/pull/2407) — Added documentation for workspace `/zenodotus` skill to gate upstream PRs in the Kromatic-Innovation fork.

**Open PRs (12 items)** cover improvements to poll‑loop message handling (nudging, compaction reminders, per‑message reasoning effort), a major voice transcription rewrite ([#2003](https://github.com/nanocoai/nanoclaw/pull/2003)), and an X‑integration skill with 25 tools ([#2409](https://github.com/nanocoai/nanoclaw/pull/2409)).

## Community Hot Topics

- **#1984 – Provider support for custom/local OpenAI-compat endpoints ([link](https://github.com/nanocoai/nanoclaw/issues/1984))**  
  *4 comments, last updated 2026-05-11.*  
  A long-standing feature request (since April 24) asking NanoClaw to route to non‑blessed endpoints documented in `SKILL.md`. The issue notes that both Codex and OpenCode paths have hooks but neither actually works in practice. Maintainers appear to have acknowledged the gap; the issue remains open and is the most commented‑on item in the last 24 hours.

- **#2404 – Double delivery when agent uses send_message MCP tool and `<message>` blocks ([link](https://github.com/nanocoai/nanoclaw/issues/2404))**  
  *1 comment, opened yesterday.*  
  A clear bug report with root cause (separate subprocess for MCP server). The community reported it quickly; a fix may land soon given the poll-loop focus in open PRs.

- **#2379 – Recurring container image staleness ([link](https://github.com/nanocoai/nanoclaw/issues/2379))**  
  *2 comments, closed.*  
  This was a reopened pattern but has since been closed (likely with a documented workaround or fix via one of the container PRs). It highlights ongoing infra pain.

## Bugs & Stability

| Severity | Issue | Description | Fix PR(s) |
|----------|-------|-------------|-----------|
| **Critical** | [#2380](https://github.com/nanocoai/nanoclaw/issues/2380) – Sandbox container crashes: `/app/src not mounted` | Fresh install on Ubuntu 24.04; container exits immediately with module-not-found error. | No fix PR yet. |
| **High** | [#2381](https://github.com/nanocoai/nanoclaw/issues/2381) – `/update-nanoclaw` silently breaks containers | After an update that changes `package.json` or `bun.lock`, live-mounted source diverges from baked deps; all container spawns crash. | No fix PR yet (related to container image rebuild strategy). |
| **High** | [#2404](https://github.com/nanocoai/nanoclaw/issues/2404) – Double delivery with MCP + message blocks | Agent sends a message twice when both output paths are used simultaneously. | Possibly addressed by poll-loop compaction PRs (e.g., [#2405](https://github.com/nanocoai/nanoclaw/pull/2405)). |
| **High** | [#2393](https://github.com/nanocoai/nanoclaw/issues/2393) – Poll-loop silently drops agent responses when `</message>` tag omitted | Entire response lost, logged as scratchpad. Critical for reliability. | [#2414](https://github.com/nanocoai/nanoclaw/pull/2414) (nudge agent when output lacks wrapping) is open. |
| **Medium** | [#2401](https://github.com/nanocoai/nanoclaw/issues/2401) – `pnpm run chat` times out with MITM error to Anthropic | Windows+WSL2 environment; Claude Code not reachable. | No fix PR; likely environment-specific. |
| **Low** | [#2390](https://github.com/nanocoai/nanoclaw/issues/2390) – `groups create` silently ignores `--id` flag | Passed ID overridden by auto-UUID without warning. | No fix PR yet (trivial UX bug). |
| **Low** | [#2389](https://github.com/nanocoai/nanoclaw/issues/2389) – Wirings created via CLI don’t auto-create destinations | Agent messages silently swallowed because destination row missing. | No fix PR. |

Several of the critical/high bugs have **open fix PRs** targeting poll-loop and compaction behavior, indicating active work.

## Feature Requests & Roadmap Signals

- **Container/stability features:**  
  - [#2396](https://github.com/nanocoai/nanoclaw/issues/2396) – Add Groq Whisper as an opt-in cloud backend alongside `whisper.cpp` (builds on sovereignty model from [#2003](https://github.com/nanocoai/nanoclaw/pull/2003)).  
  - [#2398](https://github.com/nanocoai/nanoclaw/issues/2398) – Configurable recurring task catch-up policy (currently implicit).  
  - [#2395](https://github.com/nanocoai/nanoclaw/issues/2395) – CLI commands for mounts (`add-mount` / `remove-mount`) after DB migration.  
  - [#2388](https://github.com/nanocoai/nanoclaw/issues/2388) – CLI `ncl mounts init` to bootstrap `mount-allowlist.json`.  
  - [#2385](https://github.com/nanocoai/nanoclaw/issues/2385) – Rootless setup script (strong community demand from a new user).

- **CLI usability enhancements:**  
  - [#2397](https://github.com/nanocoai/nanoclaw/issues/2397) – Top-level `ncl` CLI for scheduled tasks (list, run-now, pause, cancel).  
  - [#2387](https://github.com/nanocoai/nanoclaw/issues/2387) – Support `--agent-group-id` in `wirings update`.  
  - [#2386](https://github.com/nanocoai/nanoclaw/issues/2386) – Ensure `groups create` generates OneCLI-compatible identifiers.

*Prediction:* The next minor version (v2.0.55+) will likely include:
- Poll‑loop message‑wrapping fixes (PRs #2414, #2413, #2405)
- Voice transcription V2 (PR #2003) – long open but actively updated
- CLI mount‑allowlist bootstrap (#2388) and `ncl groups` improvement (#2386, #2390, #2389) – several are low-hanging UX fixes from the same submitter.

## User Feedback Summary

- **Pain points (explicit user frustration):**  
  - “Setup required me to spin up a VM” [#2385](https://github.com/nanocoai/nanoclaw/issues/2385) – strong user desire for rootless installation.  
  - “Agent response silently dropped” ([#2393](https://github.com/nanocoai/nanoclaw/issues/2393)) – trust‑breaking for users relying on message delivery.  
  - “Fresh install → container crashes” ([#2380](https://github.com/nanocoai/nanoclaw/issues/2380)) – immediate onboarding failure.

- **Use cases:**  
  - Multi‑agent council synthesis (motivates per‑message reasoning effort in [#2406](https://github.com/nanocoai/nanoclaw/pull/2406)).  
  - Twitter/X integration with 25 tools ([#2409](https://github.com/nanocoai/nanoclaw/pull/2409)) – indicates growing demand for social media automation.

- **Satisfaction indicators:**  
  - High number of PRs from contributors (glifocat, alexli-77, gavrielc, matt1995ai) – active, healthy community.  
  - Prompt security review and hardening (PR #2392) suggests maintainers take safety seriously.

## Backlog Watch

- **[#1984 – Custom OpenAI-compat endpoints](https://github.com/nanocoai/nanoclaw/issues/1984)** (open since April 24, 4 comments) – no clear maintainer response; a promised “Option C” that doesn’t work. This blocks users with local models or non‑standard providers. Should be prioritised for next release.

- **[#2003 – Voice transcription V2](https://github.com/nanocoai/nanoclaw/pull/2003)** (open since April 25) – a large PR from a regular contributor. It was re‑submitted after maintainer feedback; still not merged after 16 days. Voice is a high‑demand feature; its staleness may discourage the contributor.

- **[#2385 – Rootless setup](https://github.com/nanocoai/nanoclaw/issues/2385)** (posted yesterday, no maintainer reply) – a direct plea from a new user. If it receives no engagement, it could create a negative first impression.

- **[#2395 – Add/remove mount commands](https://github.com/nanocoai/nanoclaw/issues/2395)** – a UX gap after a recent migration. Unaddressed, it leaves administrative tasks half‑baked.

**Maintainer attention needed** on #1984 (promised feature not working) and #2385 (new‑user onboarding friction) to keep community trust high.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest – 2026-05-11

**Data source:** GitHub (`github.com/nullclaw/nullclaw`)  
**Analysis period:** 2026-05-10 – 2026-05-11

---

## 1. Today's Overview

Project activity is **high**, with 7 pull requests updated in the last 24 hours (2 merged/closed, 5 open) and 2 issues updated. The 24-hour cadence indicates a focused push on stability and infrastructure, especially around Discord connectivity, security hardening, and the cron subagent feature. A critical regression in the `siliconflow` provider (`HostResolutionFailed` in 2026.5.x) was reported and closed the same day it was updated, suggesting a rapid fix cycle. The open issue requesting agent performance statistics signals growing user interest in observability and operational analytics.

No new releases were published today; the latest stable is still 2026.4.9 (per the bug report context).

---

## 2. Releases

None.

---

## 3. Project Progress – Merged/Closed PRs

Two pull requests were merged/closed in the last 24 hours:

- **PR #906** (closed) – *fix(tools): defer shell sandbox auto-detection*  
  Defers shell sandbox probing until the tool is actually used, avoiding unnecessary subprocess spawning during gateway/channel startup. Adds regression coverage for lazy initialization.  
  [PR #906](https://github.com/nullclaw/nullclaw/pull/906)

- **PR #905** (closed) – *fix(discord): avoid Android gateway startup stalls*  
  Retries websocket connections across all DNS results (instead of only the first), keeps gateway A2A runtime lazy in daemon mode so provider/MCP initialization does not block Discord startup. Includes regression tests for the Android DNS retry path.  
  [PR #905](https://github.com/nullclaw/nullclaw/pull/905)

These PRs improve **startup reliability** (especially on Android) and **resource efficiency** by deferring expensive initialization steps.

---

## 4. Community Hot Topics

Only one issue attracted discussion comments in the last 24 hours:

- **Issue #902** [CLOSED] – *[Bug] 2026.5.x: HostResolutionFailed when using siliconflow provider*  
  **Comments: 2** | Author: agiminds  
  This is a regression report – the same configuration works in 2026.4.9 but fails after upgrade to 2026.5.x. The user links the failure to HTTP/DNS client refactoring. The issue was closed on 2026-05-11, implying a fix was applied (likely via PR #908 or another linked PR). The underlying need is **backward compatibility and smooth upgrades** – users expect point releases to not break existing provider integrations.  
  [Issue #902](https://github.com/nullclaw/nullclaw/issues/902)

No other issues or PRs currently have reactions or comments beyond the author. The community engagement is low in terms of discussion volume, but the speed of response to the regression suggests active maintainer attention.

---

## 5. Bugs & Stability

| Severity | Bug | Status | Notes |
|----------|-----|--------|-------|
| **Critical** | `HostResolutionFailed` with `siliconflow` provider after upgrading to 2026.5.x | **Closed** – Issue #902 | Regression in HTTP/DNS client. Fixed quickly; likely patched via PR #908. |
| **High** | Zig stdlib bug causing failed `execve` to leave process state inconsistent | **Fix in PR #883** (open) | Adds pre-spawn executable resolution to `runQuietCommand`. Prevents hanging or zombie child processes. |
| **Medium** | Discord heartbeat starvation due to mutex held during blocking `readVec` | **Fix in PR #910** (open) | Removes `io_mu` from `WsClient` to avoid deadlocks on macOS/ARM64. |
| **Medium** | Discord gateway startup stalls on Android due to single-DNS-address connection attempt | **Fixed** – PR #905 merged | Retries all resolved addresses; improves mobile reliability. |
| **Low** | Stale resume URL on Discord gateway connection reset | **Fix in PR #910** (open) | Clears stale resume URL to avoid reconnection loops. |

The most pressing stability concern (siliconflow regression) has been resolved. The remaining open PRs (#910, #883) address systematic issues in Discord gateway and child process spawning that affect reliability on diverse platforms.

---

## 6. Feature Requests & Roadmap Signals

The following user-submitted request and open feature PRs indicate likely directions for the next release:

- **Issue #909** – *Performance stat. report and analysis* (open, 0 comments)  
  Requests a report covering token input/output, tool invocation success/failure counts, and security warnings. This aligns with the ongoing cron subagent PR (#783) which already adds JSON output for job histories. The maintainers may combine these into a general observability dashboard.  
  [Issue #909](https://github.com/nullclaw/nullclaw/issues/909)

- **PR #907** (open) – *Security harden webhooks, HTTP secrets, and cron shell jobs*  
  Removes credential-bearing curl calls, rejects insecure headers/query params, and requires explicit inbound trust for Telegram/Discord/LINE integrations. This indicates a **security-first release** is being prepared – possibly the next minor version.

- **PR #783** (open, since April 7) – *feat(cron): cron subagent*  
  A large feature adding DB-backed cron scheduling, JSON CLI output, per-job timezones, and security hardening. Has been open for over a month; combined with PR #907, cron shell jobs will get security restrictions. Likely to be merged in the next 1–2 weeks.

- **PR #908** (open) – *Project hktn* (WB × OpenSource Hackathon)  
  Adds a handler for `HostResolutionFailed` in HTTP utility, reasoning stream, cost tracking, and enhanced DDG search. Likely to be merged after review; parts may supersede the fix for #902.

**Prediction:** The next release (2026.5.x or 2026.6.x) will include the cron subagent, security hardening, Discord gateway reliability improvements, and the performance stats feature (as a lightweight JSON output from the cron system).

---

## 7. User Feedback Summary

- **Pain point:** Upgrade regression – a user was blocked from using the `siliconflow` provider after upgrading to 2026.5.x. This indicates that the provider's HTTP client refactoring was not sufficiently tested against all providers. The issue was addressed within 2 days (created May 9, closed May 11).
- **Desired feature:** A user (jacktang) explicitly wants operational metrics (tokens, tool invocations, security warnings). This mirrors broader industry demand for AI agent observability.
- **Satisfaction:** No explicit satisfaction reports. The rapid fix of the regression may have mitigated user frustration, but the lack of a public release means the fix is only available via HEAD builds.

---

## 8. Backlog Watch

The following open items are at risk of becoming stale and may need maintainer attention:

- **PR #783** – *feat(cron): cron subagent* (open since 2026-04-07, last updated 2026-05-11)  
  A large, complex feature with no recent comments from maintainers. It has been open for over a month. If not actively worked on, it risks merge conflicts and community frustration. The maintainer should either assign reviewers or provide an ETA.

- **Issue #909** – *Performance stat. report* (created 2026-05-11, no maintainer response)  
  While new, it has zero comments. Acknowledging the request and indicating if it's planned would improve community trust.

- **PR #883** – *probe: resolve executable before spawning child process* (open since 2026-05-03)  
  Addresses a known Zig stdlib bug. Low comment activity but critical for stability on systems where `execve` can fail. Could be merged after basic review.

No issues or PRs have been unanswered for more than a month except PR #783. All other open PRs are less than two weeks old, which is typical for an active project.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

**Date:** 2026-05-11  
**Project:** IronClaw (github.com/nearai/ironclaw)  
**Generated by:** AI Analyst  

---

## 1. Today's Overview
The project is in a **high-activity phase**, with **46 pull requests** and **25 issues** updated in the last 24 hours. The overwhelming focus remains on the **Reborn architecture rewrite**, which is progressing methodically through contract definitions, adapter implementations, and production-seam replacements. Today saw 19 PRs merged/closed and 14 issues closed, mostly in the Reborn domain. However, stability signals are mixed: several **ENGINE_V2 bugs** reported today (image rendering, repeated tool calls, inconsistent failure display) and a **nightly E2E failure** indicate that core functionality and CI are still under churn. Community contributions continue on **Slack integration**, **mobile UI**, and **internationalization**.

---

## 2. Releases
**No new releases** have been published. The latest available release remains the previous version (none listed). The Reborn binary (`ironclaw-reborn`) is still in development and not yet shipped as a release artifact.

---

## 3. Project Progress
**19 PRs were merged or closed** in the last 24 hours. Key milestones advanced:

- **TurnRunner Worker Composition** – PR [#3446](https://github.com/nearai/ironclaw/pull/3446) closed, adding a concrete `TurnRunnerWorker` that claims runs, manages leases, resolves drivers, and applies `LoopExit` through the transition port.
- **Shared Storage Substrate** – PR [#3421](https://github.com/nearai/ironclaw/pull/3421) closed, introducing `ironclaw_storage` as a common persistence layer for Reborn adapters (Redacted errors, migration descriptors, `BlobStore`, `RecordStore` traits).
- **LoopExitApplier** – PR [#3460](https://github.com/nearai/ironclaw/pull/3460) merged (open), adding a trusted `LoopExitApplier` with validation derived from evidence ports.
- **Mobile Layout & Navigation** – PR [#2935](https://github.com/nearai/ironclaw/pull/2935) closed, replacing the cramped mobile layout with a hamburger drawer (≤768px).
- **Internationalization (i18n)** – PR [#929](https://github.com/nearai/ironclaw/pull/929) merged after a long wait (opened 2026-03-11), adding Chinese and English translations with language switching.

**Closed issues** that defined core Reborn contracts include:
- [#3193](https://github.com/nearai/ironclaw/issues/3193) – Conversation binding and session thread contracts.
- [#3204](https://github.com/nearai/ironclaw/issues/3204) – Transcript and thread storage boundary.
- [#3107](https://github.com/nearai/ironclaw/issues/3107) – AgentLoopDriver and run-class profile contract.
- [#3090](https://github.com/nearai/ironclaw/issues/3090) – ToolSurfaceService and CapabilityCatalog.
- [#3264](https://github.com/nearai/ironclaw/issues/3264) – Multi-tenant turn admission policy.
- [#3232](https://github.com/nearai/ironclaw/issues/3232) – LoopExit contract.
- [#3407](https://github.com/nearai/ironclaw/issues/3407) – Text-only AgentLoopDriverHost factory.
- [#3409](https://github.com/nearai/ironclaw/issues/3409) – Host-owned loop prompt bundle port.
- [#3419](https://github.com/nearai/ironclaw/issues/3419) – Shared storage substrate and secret-store boundary.
- [#3435](https://github.com/nearai/ironclaw/issues/3435) – Production TurnRunWakeNotifier scheduler.
- [#3452](https://github.com/nearai/ironclaw/issues/3452) – Replaced stringly-typed identity/reason fields with typed enums.
- [#3406](https://github.com/nearai/ironclaw/issues/3406) – Loop checkpoint state staging store.
- [#3402](https://github.com/nearai/ironclaw/issues/3402) – Loop driver registry and readiness validation.

---

## 4. Community Hot Topics
Most active discussions (by comment count) centered on **architectural issues**, all closed today:

- **#3193 – Define conversation binding and session thread contracts** – 6 comments. The core interface for session ingress was settled.  
- **#3204 – Define transcript and thread storage boundary** – 5 comments. Finalised storage boundaries for thread persistence.  
- **#3107 – Define AgentLoopDriver and run-class profile contract** – 4 comments. This was a large contract that affected multiple downstream issues.  
- **#3090 – Add ToolSurfaceService and CapabilityCatalog** – 4 comments. The visibility-only capability surface was agreed upon.  
- **#3069 – Ship Reborn as a separate `ironclaw-reborn` binary** – 3 comments (still open). This remains a live roadmap discussion about the executable boundary and CLI design.

**Community-contributed PRs** also attracted attention:
- **#2066 – Slack thread history fetch** (opened 2026-04-06) – a long-running PR now receiving fresh reviews.
- **#2457 – OIDC audience claim fix** – addresses load balancer compatibility, important for deployments.
- **#3396 – Slack pairing via chat** – new feature allowing users to bind Slack accounts using an LLM-called tool.

**Underlying needs:** Users and deployers want smoother Slack integration (thread history, pairing), reliable OIDC setup, and a polished mobile experience. The Reborn contract discussions reflect internal engineering alignment rather than user demand.

---

## 5. Bugs & Stability
**Three new ENGINE_V2 bugs** were reported today, all by `hanakannzashi` – representing a pattern of regressions in the new engine path:

- **[#3463 – Engine V2 generated images do not render correctly in Gateway UI](https://github.com/nearai/ironclaw/issues/3463)** – high severity. Images generated via tools fail to appear as image cards; assistant responds with text “image generated successfully.” A related fix PR [#3065](https://github.com/nearai/ironclaw/pull/3065) is already open (size: XL, WIP) but has not yet been merged.
- **[#3465 – ENGINE_V2 repeatedly calls `tool_info` during tool-use flows](https://github.com/nearai/ironclaw/issues/3465)** – high severity. The agent gets stuck in a loop calling `tool_info(schema)` and sometimes also help tools, degrading UX and increasing costs.
- **[#3464 – Failed tool calls render inconsistently in Gateway UI](https://github.com/nearai/ironclaw/issues/3464)** – medium severity. UI shows malformed or inconsistent failure states; previously persisted failures render differently from new ones.

**Nightly E2E failure** – [#3447](https://github.com/nearai/ironclaw/issues/3447) – the `v2-engine` job failed. This is a CI reliability issue; the commit (`6e6eca7`) is recent and may be related to the above bugs.

**Older bug still open:**  
- **[#2752 – `onboard` command throws DB error on provider step](https://github.com/nearai/ironclaw/issues/2752)** (opened 2026-04-20, uncommented since). This blocks new local setups with PostgreSQL. No fix PR has been linked yet.

---

## 6. Feature Requests & Roadmap Signals
**User-requested features** with ongoing activity:

- **Voice recording in web gateway** – [#1343](https://github.com/nearai/ironclaw/issues/1343) (open since March, 0 comments). Backend already supports audio attachments; only the UI microphone button is missing. **Prediction:** Likely to be implemented in the next minor release given the low effort vs. high impact.
- **Attachment button polish** – [#1342](https://github.com/nearai/ironclaw/issues/1342) – Replace paperclip emoji with styled `+` button. Closely related to the ongoing attachment UI work in PR [#3331](https://github.com/nearai/ironclaw/pull/3331). Expected to land soon.
- **Slack thread history** – PR [#2066](https://github.com/nearai/ironclaw/pull/2066) adds bot thread context even without prior participation – near completion.
- **Slack pairing via chat** – PR [#3396](https://github.com/nearai/ironclaw/pull/3396) introduces a `pairing_approve` tool – new feature, likely in next release.
- **Mobile layout redesign** – PR [#3461](https://github.com/nearai/ironclaw/pull/3461) (just opened) refines the mobile experience. If merged quickly, will appear in the next binary release.

**Roadmap signals from the Reborn track:**  
- The imminent closure of issues like [#3069](https://github.com/nearai/ironclaw/issues/3069) (ship Reborn binary) and [#3459](https://github.com/nearai/ironclaw/issues/3459) (user-selectable model routes) suggests the **next major release will likely include `ironclaw-reborn`** as a co-shipped binary, along with configurable model routing and the production substrate.

---

## 7. User Feedback Summary
Real user pain points and satisfaction indicators from the data:

- **ENGINE_V2 instability** – Users of the v2 engine are experiencing at least three distinct bugs (image rendering, tool call loops, inconsistent failure UI). This is likely frustrating users who have opted into the new engine, and the number of bug reports suggests early adopters are actively testing but encountering reliability issues.
- **Deployment friction** – The OIDC fix (PR [#2457](https://github.com/nearai/ironclaw/pull/2457)) and the `onboard` DB error (issue [#2752](https://github.com/nearai/ironclaw/issues/2752)) indicate that setting up the project in production (traefik, OIDC proxies, PostgreSQL) is still bumpy.
- **Slack integration demand** – The community contributions for thread history and pairing (by `synner88` and `PierreLeGuen`) show real use cases around team collaboration. The positive reaction (no negative comments) suggests these features are welcome.
- **Mobile-first expectations** – The attention to mobile layout (two PRs from `italic-jinxin`) reflects user feedback that the web UI is hard to use on phones. The replacement of the narrow rail with a hamburger drawer appears to be a direct response.
- **Internationalization** – The i18n PR [#929](https://github.com/nearai/ironclaw/pull/929) (Chinese and English) addresses multilingual users. The fact that it took over two months to review and merge may indicate maintainer bandwidth constraints, but the feature itself was well-received.

---

## 8. Backlog Watch
Several important issues and PRs risk falling behind:

- **Issue [#2752](https://github.com/nearai/ironclaw/issues/2752) – `onboard` DB error** – Open for 3+ weeks with no recent activity. Blocks new local PostgreSQL setups. Labels: `bug_bash_P1`, `scope: db`, `scope: secrets`. Needs maintainer triage.
- **Issue [#1343](https://github.com/nearai/ironclaw/issues/1343) – Voice recording** – Low-effort UI addition that has been sitting for two months with no comments. Likely a quick win for user satisfaction.
- **Issue [#1342](https://github.com/nearai/ironclaw/issues/1342) – Attachment button polish** – Similar to above, trivial UI change that has lingered since March. The ongoing PR [#3331](https://github.com/nearai/ironclaw/pull/3331) may address this indirectly, but it is not explicitly linked.
- **PR [#2066](https://github.com/nearai/ironclaw/pull/2066) – Slack thread history** – Opened 2026-04-06, still open with no recent review. The feature is substantial (size: L) and would be a significant community contribution; maintainer review is needed.
- **PR [#2892](https://github.com/nearai/ironclaw/pull/2892) – Whitespace trimming for LLM base_url** – A small fix that has been open since April 23; its absence may cause recurring CI failures.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-11

## Today's Overview

The project saw moderate activity with **29 pull requests merged/closed** in the last 24 hours and only **1 open issue** updated. No new releases were published. The majority of work was concentrated on bug fixes and feature integration, particularly around artifact previews, memory management, IM (POPO) multi-instance support, and workspace isolation. The single open issue (#1849) reports a critical user-facing problem where the agent outputs noise or stops mid-sentence, indicating a remaining stability concern despite several related fixes being merged today.

## Releases

No new releases were tagged today.

## Project Progress

The following key changes were merged or closed today (all 29 PRs were closed/merged, with the top 20 listed in the data):

- **Artifact preview fixes (#1945):** Fixes for `.mermaid/.mmd` browser opening, PPTX sandbox missing `allow-scripts`, passive event listener errors, and file search empty-state text. Adds zoom controls for Mermaid preview and hides binary file edit button.
- **Code block background on horizontal scroll (#1944):** Ensures background color covers fully when code blocks scroll horizontally, and fixes blockquote overflow.
- **Memory settings tab refactor (#1943):** Redesigns the memory settings page into three tabs (Memory entries / Embedding search / Dreaming content). Adds read-only display of Dreaming data sourced from the OpenClaw backend.
- **Message metadata hover fix (#1942):** Prevents timestamp/copy/edit buttons from staying visible after click; unifies hover backgrounds; fixes blurry settings icon.
- **NO_REPLY sync fix (#1940):** Addresses an issue where the "NO_REPLY" status was not synchronised correctly (likely related to #1849).
- **POPO multi-instance support (#1883, #1887, #1901):** Upgrades the POPO plugin to support multiple bot instances, adds configuration UI, and cleans up lint warnings.
- **Workspace decoupling from working directory (#1890, #1894):** Moves the main agent workspace (MEMORY.md, SOUL.md, etc.) to a fixed `workspace-main/` directory, preventing data loss when changing the working directory. Fixes a migration ordering bug that could skip copying the `memory/` folder.
- **Streaming text merge fix (#1908):** Removes an overlap detection function that wrongly dropped repeated characters (e.g., `.pptx` became `.ptx`).
- **Pagination for session list and message history (#1907):** Cherry-picks and resolves conflicts from #924, adding pagination to reduce memory/rendering load for long conversations.
- **Windows file preview duplicate cards (#1909):** Fixes duplicate preview cards and path errors caused by drive letter inconsistencies between `file:///D:/path` and `D:\path`.
- **AI diagnostics for email connectivity (#1916):** Adds an “AI Diagnostics” button on email skill failures that pre-fills the cowork view with structured error context for LLM-assisted troubleshooting.
- **Scheduled task run history filtering (#1913):** Adds time range and status filters to task run history views, plus a new DateInput component.
- **Other fixes:** Cross-platform test assertions (#1914), POPO i18n key fix (#1901), release branch merge (#1902), and removal of dead engine-branching code (#1884).

## Community Hot Topics

- **#1849 [OPEN] — “追问时会出现无限NO_REPLY或者输出几个文字就直接不输出了”**  
  [Issue #1849](https://github.com/netease-youdao/LobsterAI/issues/1849)  
  User reports that follow-up questions result in infinite “NO_REPLY” responses or truncated output. The issue is still open with 1 comment. Analysis points to early task completion while the model continues generating, leaving the page unresponsive. This is the only open issue and the most active community discussion point today. No PR directly links to it, but #1940 (“fix: 修复消息尾部NO_REPLY同步问题”) may be a related partial fix.

No other issues or PRs received notable reactions or comments today (all comment counts are undefined).

## Bugs & Stability

| Severity | Bug | Status | Fix PR(s) |
|----------|-----|--------|-----------|
| **High** | Agent outputs infinite “NO_REPLY” or cuts off mid-sentence (#1849) | Still open | Possibly addressed by #1940 (NO_REPLY sync fix) but not confirmed |
| **Medium** | Artifact preview: .mermaid/.mmd browser open broken, PPTX sandbox blocking scripts, scroll zoom errors (#1945) | Fixed | #1945 |
| **Medium** | Streaming text merges incorrectly dropping repeated characters like `.pptx` → `.ptx` (#1908) | Fixed | #1908 |
| **Medium** | Windows file preview duplicates and `D:\D:\path` errors (#1909) | Fixed | #1909 |
| **Low** | Code block background not extending on horizontal scroll (#1944) | Fixed | #1944 |
| **Low** | Message metadata row staying visible after mouse leaves (#1942) | Fixed | #1942 |

The most critical unresolved bug remains #1849, which likely caused user frustration and may require deeper investigation beyond the sync fix in #1940.

## Feature Requests & Roadmap Signals

- **Memory management overhaul** – The refactor in #1943 introduces a tab-based memory settings page and backend-driven Dreaming content display. This suggests a roadmap push toward richer memory visualization and management, likely to appear in the next release.
- **IM multi-instance support** – POPO multi-instance (#1883) follows earlier multi-instance patterns for WeChat and other platforms, indicating a continued effort to support enterprise-grade IM bot deployments.
- **Workspace isolation** – Decoupling the main agent workspace from the configurable working directory (#1890) improves data safety and aligns with best practices for state management. This change will be part of the upcoming release.
- **Task management improvements** – Pagination and filtering for scheduled task history (#1913) and AI diagnostics for email failures (#1916) show ongoing investment in task reliability and usability.
- **No new feature requests** were filed today; the only open issue is a bug report.

## User Feedback Summary

The single open issue (#1849) expresses visible frustration: users report that the assistant becomes unresponsive after follow-up questions, either looping indefinitely or stopping output prematurely. This is a core user pain point that directly impacts trust and usability. Other merged fixes (preview bugs, code block rendering, file path issues on Windows) indicate that users have encountered frequent UI and integration glitches, particularly in artifact-heavy workflows and on Windows. The wide range of fixes today suggests the team is actively addressing these reports, although the NO_REPLY problem remains open.

## Backlog Watch

No long-unanswered issues or PRs were identified. The only open issue (#1849) was updated today, so it is receiving attention. All PRs from the data set are either closed or merged, leaving a clean backlog. Maintainer response times appear to be healthy.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-11

## Today’s Overview
Project activity was minimal today, with only one issue closed and one pull request merged. The lone event revolved around a dependency‑related bug in the sandbox container build, which was promptly fixed. No new releases were published, and no other issues or PRs were updated in the last 24 hours. Overall, the project appears stable but quiet, with no ongoing open work to report.

## Releases
No new releases were published in the last 24 hours.

## Project Progress
- **PR #989** ([merged](https://github.com/moltis-org/moltis/pull/989)): *fix(sandbox): update discrawl module path*  
  This PR fixes a break in the sandbox container build caused by a change in the upstream `discrawl` repository. The Go module path was updated from `github.com/steipete/discrawl` to `github.com/openclaw/discrawl`, and the bundled discrawl skill metadata was adjusted accordingly. A Dockerfile regression test was added to prevent future stale‑path issues.

## Community Hot Topics
The only activity today was the closed issue and its corresponding fix PR. Neither item received comments or reactions, so there were no community discussions to highlight. The underlying need was a straightforward dependency update to unblock sandbox container builds.

- **Issue #988** ([closed](https://github.com/moltis-org/moltis/issues/988)): *[Bug]: discrawl repo URL changes break sandbox container build*  
- **PR #989** ([merged](https://github.com/moltis-org/moltis/pull/989)): *fix(sandbox): update discrawl module path*

## Bugs & Stability
One bug was reported and fixed today. Severity is **medium** — it blocked sandbox container builds but had a clear cause and a straightforward fix.

| Bug | Severity | Fix PR |
|-----|----------|--------|
| [Sandbox build broken due to discrawl repo URL change](https://github.com/moltis-org/moltis/issues/988) | Medium | [PR #989](https://github.com/moltis-org/moltis/pull/989) – merged |

No other stability issues, crashes, or regressions were reported.

## Feature Requests & Roadmap Signals
No feature requests were filed or discussed today. Based on the activity, the immediate roadmap focus is on maintaining build integrity rather than introducing new capabilities. No predictions can be made for the next version from today’s data alone.

## User Feedback Summary
User feedback today was absent. The only issue was a technical bug raised by a contributor, not an end‑user pain point. No satisfaction or dissatisfaction signals were shared.

## Backlog Watch
No long‑unanswered issues or PRs require maintainer attention. All items updated in the last 24 hours have been resolved.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-05-11

## Today’s Overview
Activity remains high, with **31 issues** and **31 pull requests** updated in the past 24 hours.  
12 issues were closed, 15 PRs were merged or closed, and 16 PRs remain open (several under review).  
New features such as **multiple file attachments**, **browser batch actions**, and **auto-memory management** were merged, while critical bugs including **session history loss** and **DashScope configuration not being read** received fixes.  
The community continues to contribute actively, with multiple first-time contributors submitting patches for channels (DingTalk, Feishu), security improvements, and Tauri desktop support.  
No new releases were published today.

## Releases
*None.* (No new releases in the last 24 hours.)

## Project Progress (Merged/Closed PRs Today)
Several notable PRs were merged or closed, advancing both features and stability:

- **Multiple file attachments in chat** – PR [#4206][PR4206] (closed) adds the ability to select multiple files using Ctrl/Shift.
- **Async execution for `delegate_external_agent`** – PR [#4197][PR4197] (closed) improves long-running external ACP workflows.
- **Browser batch actions** – PR [#4139][PR4139] (closed) adds `_action_batch` to the browser_use tool, enabling sequential sub-actions (navigate, click, type, etc.).
- **Reference image support for gpt-image2** – PR [#4194][PR4194] (closed) allows 1–16 reference images for generation/editing.
- **DingTalk quoted message handling** – PR [#4209][PR4209] (closed) processes replied-to messages, aligning with Feishu and WeCom.
- **Session history disappearing fix** – PR [#4203][PR4203] (closed) resolves the bug where history and messages were routed to wrong sessions (fixes [#3843][I3843]).
- **Provider metadata fix for DashScope** – PR [#4186][PR4186] (closed) exposes regional Base URL options in the Console UI.
- **Auto-memory management** – PR [#4204][PR4204] (closed) implements automatic memory retrieval, summarization during compaction, and periodic extraction.
- **Avatar upload for agents** – PR [#1791][PR1791] (closed) adds avatar upload/preview/delete in the Console.

## Community Hot Topics
The most discussed issues (by comment count) reveal key user concerns:

- **Cron job interruption** – [#2429][I2429] (10 comments): Users report agents interrupting scheduled tasks with “I noticed that you have interrupted me.” The root cause appears to be cron interaction with active agent state.
- **Session history disappearing** – [#3843][I3843] (9 comments, now fixed by PR [#4203][PR4203]): A critical UX bug where all chat history vanishes but the session title remains.
- **Volcano Engine model configuration** – [#4165][I4165] (8 comments): After configuring API keys, all models fail connectivity tests.
- **HEARTBEAT.md network reconnection bug** – [#4017][I4017] (7 comments): Enabling heartbeat prevents automatic reconnection after network outages.
- **Windows console flash** – [#4123][I4123] (6 comments): Every `execute_shell_command` call flashes a console window.

## Bugs & Stability
New bugs reported today, ranked by severity:

| Severity | Issue | Description | Fix PR exists? |
|----------|-------|-------------|----------------|
| **Critical** | [#4185][I4185] | Chat cannot be opened if persisted session contains malformed empty `tool_use` entry – history file intact but UI blocked. | No |
| **High** | [#4205][I4205] | Offline desktop cannot use voice transcription (whisper+ffmpeg installed) – requires internet. | No |
| **High** | [#4159][I4159] | DashScope provider config exists but is not read at runtime – `api_key` empty, causing 401 errors. | PR [#4186][PR4186] fixes the UI side, but runtime config reading may still need attention. |
| **Medium** | [#4170][I4170] | Agent action logs only shown after completion – no streaming updates, making long tasks opaque. | No |
| **Medium** | [#4187][I4187] | Dark mode: plan text contrast too low, almost invisible. | No |
| **Medium** | [#4191][I4191] | MCP tools fail when schema contains `$defs` or `$ref` (schema is stripped). | No |
| **Medium** | [#4104][I4104] | Chinese filenames with mixed characters get an extra space (e.g. “2026年报告.word” becomes “2026 年报告.word”). | No |
| **Low** | [#4183][I4183] | Custom model API appends provider_id prefix (e.g. `cpa/gpt-5.5`) causing request errors. | No |
| **Low** | [#4199][I4199] | Volcano Engine `thinking` parameter ignored – cannot disable deep thinking. | No |

## Feature Requests & Roadmap Signals
Community requests that entered today and may land in the next version:

- **Model failover / fallback** – [#4011][I4011] (3 comments) and [#4181][I4181] (2 comments) both request automatic fallback when the primary model fails (timeout, rate limit). Given multiple related open issues, this is a high-priority roadmap candidate.
- **mem0 memory integration** – [#4208][I4208] asks whether mem0 is supported and how to implement it. No documentation exists yet.
- **Multi-agent collaboration skill alignment** – [#4211][I4211] proposes aligning the built-in skill with the newer inter-agent tools (`list_agents`, `chat_with_agent`, etc.) instead of shell commands.
- **File page showing workspaces** – [#4195][I4195] requests the Console file browser to display files created in `/app/working/workspaces`.
- **Desktop default agent setting** – [#4182][I4182] (bug report, but also feature request) – setting `active_agent` in `config.json` is ignored on desktop startup. A fix PR [#4201][PR4201] is open (under review).

## User Feedback Summary
User sentiment this week is mixed: many bug reports indicate friction with configuration, network resilience, and UI polish, but the rapid rate of fixes and community contributions shows strong engagement.

- **Pain points**:
  - Session history loss remains the most disruptive issue (now fixed).
  - Configuration errors (DashScope, Volcano Engine, custom models) waste user time.
  - Offline capability gaps (voice transcription, model fallback) limit production use.
  - Lack of streaming agent action logs reduces trust during long tasks.
- **Positive signals**:
  - New features like multiple attachments, batch browser actions, and avatar uploads are well received.
  - First-time contributors are submitting high-quality PRs (Tauri desktop, Feishu voice bubbles, memory plug-ins).
  - The memory distillation plugin PR [#4171][PR4171] demonstrates advanced community interest in long-term memory.

## Backlog Watch
Issues and PRs that have been open for extended periods and would benefit from maintainer attention:

- **Tauri 2.x Desktop Support** – PR [#3813][PR3813] (open since April 24, 2026, first-time contributor, under review). Moving from Electrobun to Tauri is a significant infrastructure change and has stalled.
- **Pluggable Memory Manager (ADBPG)** – PR [#2308][PR2308] (open since March 26, 2026, first-time contributor). Adds persistent long-term memory via AnalyticDB for PostgreSQL – last updated today but still not merged.
- **Cron job concurrency fixes** – PR [#4084][PR4084] (open since May 7, 2026, under review). Addresses state leaks in CronManager; vital for reliability of scheduled tasks.
- **MD5 → SHA-256 security upgrade** – PR [#4180][PR4180] (open since May 10, 2026, first-time contributor). Replaces MD5 in iMessage, WeCom, DingTalk, and file utilities – low risk and should be prioritized.
- **Matrix E2EE enhancement** – PR [#4120][PR4120] (open since May 8, 2026, first-time contributor). Extends Matrix configuration UI and sign-in flows.

[I2429]: https://github.com/agentscope-ai/CoPaw/issues/2429
[I3843]: https://github.com/agentscope-ai/CoPaw/issues/3843
[I4165]: https://github.com/agentscope-ai/CoPaw/issues/4165
[I4017]: https://github.com/agentscope-ai/CoPaw/issues/4017
[I4123]: https://github.com/agentscope-ai/CoPaw/issues/4123
[I4185]: https://github.com/agentscope-ai/CoPaw/issues/4185
[I4205]: https://github.com/agentscope-ai/CoPaw/issues/4205
[I4159]: https://github.com/agentscope-ai/CoPaw/issues/4159
[I4170]: https://github.com/agentscope-ai/CoPaw/issues/4170
[I4187]: https://github.com/agentscope-ai/CoPaw/issues/4187
[I4191]: https://github.com/agentscope-ai/CoPaw/issues/4191
[I4104]: https://github.com/agentscope-ai/CoPaw/issues/4104
[I4183]: https://github.com/agentscope-ai/CoPaw/issues/4183
[I4199]: https://github.com/agentscope-ai/CoPaw/issues/4199
[I4011]: https://github.com/agentscope-ai/CoPaw/issues/4011
[I4181]: https://github.com/agentscope-ai/CoPaw/issues/4181
[I4208]: https://github.com/agentscope-ai/CoPaw/issues/4208
[I4211]: https://github.com/agentscope-ai/CoPaw/issues/4211
[I4195]: https://github.com/agentscope-ai/CoPaw/issues/4195
[I4182]: https://github.com/agentscope-ai/CoPaw/issues/4182
[PR4206]: https://github.com/agentscope-ai/CoPaw/pull/4206
[PR4197]: https://github.com/agentscope-ai/CoPaw/pull/4197
[PR4139]: https://github.com/agentscope-ai/CoPaw/pull/4139
[PR4194]: https://github.com/agentscope-ai/CoPaw/pull/4194
[PR4209]: https://github.com/agentscope-ai/CoPaw/pull/4209
[PR4203]: https://github.com/agentscope-ai/CoPaw/pull/4203
[PR4186]: https://github.com/agentscope-ai/CoPaw/pull/4186
[PR4204]: https://github.com/agentscope-ai/CoPaw/pull/4204
[PR1791]: https://github.com/agentscope-ai/CoPaw/pull/1791
[PR4201]: https://github.com/agentscope-ai/CoPaw/pull/4201
[PR4171]: https://github.com/agentscope-ai/CoPaw/pull/4171
[PR3813]: https://github.com/agentscope-ai/CoPaw/pull/3813
[PR2308]: https://github.com/agentscope-ai/CoPaw/pull/2308
[PR4084]: https://github.com/agentscope-ai/CoPaw/pull/4084
[PR4180]: https://github.com/agentscope-ai/CoPaw/pull/4180
[PR4120]: https://github.com/agentscope-ai/CoPaw/pull/4120

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-11

## 1. Today's Overview
Development activity was low over the past 24 hours, with **no new issues** opened or closed and **no releases published**. The only pull request updated, [#583](https://github.com/qhkm/zeptoclaw/pull/583), remains open and represents the second phase of a larger middleware pipeline refactor (tracking #399). The single PR signals continued internal progress, but the absence of issue activity or merged patches suggests a quiet day focused on long-running refactoring work. Overall project health appears stable, with the core team advancing a structural change rather than addressing community feedback or bugs.

## 2. Releases
No new releases were published today. The latest release remains unchanged from prior dates.

## 3. Project Progress
No pull requests were merged or closed today. The only active contribution is:

* **PR #583** (open) – `refactor(agent): wire Pipeline into process_message + CoreLoop (phase 2 of #399)`  
  *Adds the Phase 2 wiring scaffolding for the agent middleware pipeline, including `build_subsystems()`, `build_pipeline_context()`, and `build_pipeline()` in `AgentLoop`. Also introduces `src/agent/core_loop.rs` with a `LegacyTerminal` stub that short-circuits with a structured error until fully implemented.*  
  [View PR](https://github.com/qhkm/zeptoclaw/pull/583)

## 4. Community Hot Topics
No issues or PRs attracted comments or reactions today. The only item with any recent activity is:

* **PR #583** (open, 0 comments, 0 👍) – While lacking discussion, this PR is the focal point of current development. It directly addresses the middleware pipeline wiring originally planned in #399, indicating that the team is methodically decomposing a larger architectural change. The lack of community input may simply reflect the early, internal stage of the refactor.  
  [PR #583](https://github.com/qhkm/zeptoclaw/pull/583)

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project shows no stability concerns as of this digest.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, **PR #583** is a direct follow-up to **issue #399** (likely a meta-issue for the pipeline architecture). This suggests that the next release may include the fully wired middleware pipeline, enabling modular agent processing. No other roadmap signals are visible in the data.

## 7. User Feedback Summary
No user feedback, pain points, or use-case discussions were recorded in the past 24 hours. Community interaction remains minimal on this particular day.

## 8. Backlog Watch
No issues or PRs in the backlog have gone unanswered for an extended period. The only open PR (#583) is recent (created 2026-05-11) and actively maintained by the author (`qhkm`). No stale items require maintainer attention at this time.

---

*Report generated from ZeptoClaw GitHub data snapshot for 2026-05-11.*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest – 2026-05-11

## 1. Today’s Overview

Project activity remains high with **38 pull requests updated** in the last 24 hours (29 open, 9 merged/closed) and **11 issues updated** (8 open, 3 closed). No new release was tagged. The largest ongoing effort is the **`integration/v0.8.0` PR** ([#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)), an XL-sized branch that bundles schema v3 migration, workspace restructuring, and dozens of feature/bugfix commits. Meanwhile, a flurry of smaller fixes and enhancements landed today—most notably the **matrix-sdk 0.16→0.17 dependency bump** ([#6566](https://github.com/zeroclaw-labs/zeroclaw/pull/6566)) and the closure of several long-standing tool wrapper migration PRs. The project is clearly in a consolidation phase ahead of a v0.8.0 release, with maintainers actively resolving build regressions and addressing community feedback.

---

## 2. Releases

**No new releases** in the last 24 hours. The last tagged version remains **v0.7.5** (per the Homebrew merge issue [#6547](https://github.com/zeroclaw-labs/zeroclaw/issues/6547), which confirmed the missing v0.7.5 release on Homebrew has now been fixed externally). The next release is expected to be **v0.8.0** based on the integration branch activity.

---

## 3. Project Progress

**Merged / closed PRs today (9 total):**

| PR | Description | Status |
|----|-------------|--------|
| [#6566](https://github.com/zeroclaw-labs/zeroclaw/pull/6566) | **fix(channels,deps): bump matrix-sdk 0.16 → 0.17** – resolves recursion limit overflow ([#6530](https://github.com/zeroclaw-labs/zeroclaw/issues/6530) closed) | ✅ Merged |
| [#6117](https://github.com/zeroclaw-labs/zeroclaw/pull/6117) | **feat(codex): support native Responses tool calls** – adds OpenAI Responses API support to the `openai-codex` provider | ✅ Closed |
| [#4954](https://github.com/zeroclaw-labs/zeroclaw/pull/4954) | **refactor(tools): delegate rate-limiting to RateLimitedTool** in network/skill tools | ✅ Closed |
| [#4953](https://github.com/zeroclaw-labs/zeroclaw/pull/4953) | **refactor(tools): delegate rate-limiting to RateLimitedTool** in ClaudeCodeRunnerTool | ✅ Closed |
| [#4952](https://github.com/zeroclaw-labs/zeroclaw/pull/4952) | **refactor(tools): delegate rate-limiting to RateLimitedTool** in AI CLI tools (Gemini, Claude, Codex, OpenCode) | ✅ Closed |
| [#4949](https://github.com/zeroclaw-labs/zeroclaw/pull/4949) | **refactor(tools): apply RateLimitedTool** to CronAdd/CronRemove/CronUpdate tools | ✅ Closed |
| (3 additional closed PRs not shown in top-20 list ) | – | ✅ Closed |

**Key advances:**
- The **matrix-sdk bump** (#6566) unblocks Matrix channel builds that had been failing with a recursion limit overflow since v0.7.5. A dedicated smoke check feature ([#6576](https://github.com/zeroclaw-labs/zeroclaw/issues/6576)) is now planned for the v0.7.6 release gate.
- The **tool wrapper migration** (PRs #4949–#4954) finally lands after weeks of review, consolidating rate-limiting logic into a shared `RateLimitedTool` wrapper. This reduces code duplication across 7+ tools.
- **Closed issues** for today include: build failure with matrix-sdk v0.16.0 ([#6530](https://github.com/zeroclaw-labs/zeroclaw/issues/6530)), Homebrew merge fail ([#6547](https://github.com/zeroclaw-labs/zeroclaw/issues/6547)), and a runtime cron job failure ([#5991](https://github.com/zeroclaw-labs/zeroclaw/issues/5991)).

---

## 4. Community Hot Topics

| Issue | Title | Comments | Link |
|-------|-------|----------|------|
| #6530 | [Bug]: Build failure with matrix-sdk v0.16.0 | 5 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6530) |
| #6547 | [Feature]: homebrew merge fail | 3 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6547) |
| #5991 | [Bug]: failed cron job | 3 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5991) |
| #6034 | [Bug]: 单轮对话以及多轮对话会出现丢失 user message的现象 | 3 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) |
| #6074 | audit: track 153 commits lost in bulk revert c3ff635 for recovery | 2 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) |
| #5316 | [Feature]: Propose SearXNG search support and improve Web Search robustness | 2 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) |

### Analysis:
- The **matrix-sdk build failure** (#6530) attracted the most discussion (5 comments) but has now been resolved by the PR merged today (#6566).
- The **Homebrew merge gap** (#6547) was a release-process issue – the v0.7.5 tarball was not published to Homebrew’s core tap. The community member luckbyte raised the PR upstream, and the issue was closed after confirmation.
- The **cron job failure** (#5991) with severity S0 (data loss) is now closed, indicating a fix was deployed.
- The **user message loss bug** (#6034) – reported in Chinese, affecting a custom provider (Qwen3.5-35B) – remains open as a **high-risk, priority P1** bug. The user experiences missing user messages in both single and multi-turn dialogues. No fix PR has been linked yet.
- The **lost commits audit** (#6074) is a long-running internal concern about a bulk revert that removed 153 commits. It remains in-progress with no resolution.

No issue or PR has any 👍 reactions recorded (all zero), so community sentiment is inferred from comment activity.

---

## 5. Bugs & Stability

### Bugs reported/updated today (2026-05-11)

| ID | Title | Severity | Status | Fix PR? |
|----|-------|----------|--------|---------|
| [#6034](https://github.com/zeroclaw-labs/zeroclaw/issues/6034) | User message loss with custom provider (Qwen) | **High** – S1 (workflow blocked) | Open, accepted | No |
| [#6561](https://github.com/zeroclaw-labs/zeroclaw/issues/6561) | Gateway non-loopback host recovery hint advertises admin URL that guard rejects | **Low** – S3? | Open | No direct PR, but related to #6192 |
| [#6530](https://github.com/zeroclaw-labs/zeroclaw/issues/6530) | Build failure with matrix-sdk v0.16.0 recursion limit | **Medium** – S2 | Closed | [#6566](https://github.com/zeroclaw-labs/zeroclaw/pull/6566) |
| [#5991](https://github.com/zeroclaw-labs/zeroclaw/issues/5991) | Cron job failure (data loss risk) | **High** – S0 | Closed | (fixed in earlier update) |

### Bug-fix PRs opened today

- [#6572](https://github.com/zeroclaw-labs/zeroclaw/pull/6572) – **fix(channels): close Discord media send/receive gaps** (size L, risk medium). Addresses inbound attachment deduplication and missing media types.
- [#6575](https://github.com/zeroclaw-labs/zeroclaw/pull/6575) – **fix(gemini): propagate token usage to cost tracker** (size S, risk medium). Recovers usage reporting from a previous superseded PR.
- [#6573](https://github.com/zeroclaw-labs/zeroclaw/pull/6573) – **fix(providers/glm): mark GLM provider as vision-capable** (size XS, risk low). Resolves a misconfiguration where GLM models (e.g., glm-4.5v) were rejected as vision providers.

### Notable regression:
No immediate regressions reported, but the **Discord media gaps** (#6572) and **Gemini costing fixes** (#6575) address latent issues that may have affected users running those integrations.

---

## 6. Feature Requests & Roadmap Signals

### Features opened today (2026-05-11)

| ID | Title | Risk | Link |
|----|-------|------|------|
| [#6574](https://github.com/zeroclaw-labs/zeroclaw/issues/6574) | Configurable behaviour for image-bearing messages when no vision path is available | Low | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6574) |
| [#6576](https://github.com/zeroclaw-labs/zeroclaw/issues/6576) | Add v0.7.6 Matrix live homeserver smoke check after matrix-sdk 0.17 bump | Low | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6576) |
| [#6565](https://github.com/zeroclaw-labs/zeroclaw/issues/6565) | Clear inline-keyboard + reflect outcome on Telegram tool-approval messages after click | Medium | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6565) |
| [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) | ComfyCloud/ComfyUI as shared media provider (remote workflows; image + path to gen_video) | High | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) |
| [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) | Audit: track 153 commits lost in bulk revert c3ff635 for recovery | High | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) |

### Older but active feature requests:

- [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) – **SearXNG search support + DuckDuckGo CAPTCHA detection** (open since Apr 5, needs maintainer review)
- [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) – **ComfyUI as media generation provider** (opened yesterday, high risk, may land in v0.8.0 if accepted)

### Roadmap predictions:
- **v0.8.0** integration PR ([#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)) is the single largest branch, containing schema v3 migration (breaking config changes), workspace splits, and many tool/channel/ci improvements. Likely release candidate within 1–2 weeks.
- **Matrix smoke check** (#6576) is explicitly tagged as a `release-gate` for v0.7.6, suggesting a minor release (v0.7.6) may precede v0.8.0 to ship the matrix-sdk fix and tests.
- **Telegram inline keyboard cleanup** (#6565) and **image handling config** (#6574) are smaller UX improvements that could also slip into a v0.7.x patch.

---

## 7. User Feedback Summary

**Pain points observed:**
- **Provider compatibility issues**: The #6034 bug (user message loss with custom Qwen provider) indicates that the provider abstraction may not handle all OpenAI-compatible APIs correctly. The user’s custom endpoint returns a 400 error with missing parameters.
- **Vision capabilities lacking**: Two users raised concerns about image handling. #6574 (new) wants configurable behavior when no vision path is available, and #6573 fixes one such case (GLM not recognized as vision-capable). This suggests the vision routing logic is a common friction point.
- **Web search reliability**: #5316 (still open) highlights DuckDuckGo CAPTCHA blocking and lack of an alternative search engine. The user requests SearXNG as a privacy-focused fallback.
- **Telegram UX**: #6565 reports that tool-approval inline keyboards remain clickable after use, causing confusion in chat history.
- **Homebrew availability**: #6547 was a release distribution issue; now resolved, but the user had to fix it themselves. This points to a need for better release automation.

**Satisfaction signals:**
- Quick turnaround on the matrix-sdk build failure (#6530) – reported May 8, fix merged May 11.
- The tool wrapper migration PRs (7 PRs closed today) reduce technical debt and are a net positive for maintainability.
- NixOS module (#6562) and container docs (#6570) contributions from the community show healthy ecosystem involvement.

---

## 8. Backlog Watch

### Issues needing maintainer review (labeled `needs-maintainer-review`):

| ID | Title | Last Update | Link |
|----|-------|-------------|------|
| [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) | Propose SearXNG search support and improve Web Search robustness | 2026-05-11 (updated) | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) |
| [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) | ComfyCloud/ComfyUI as shared media provider | 2026-05-11 | [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) |

Both are feature requests with significant design impact. No maintainer has triaged or commented on them recently.

### PRs needing author action (`needs-author-action`):

| ID | Title | Last Update | Link |
|----|-------|-------------|------|
| [#6555](https://github.com/zeroclaw-labs/zeroclaw/pull/6555) | Image gen runpod – augmentation of image generation with RunPod ComfyUI | 2026-05-11 | [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/6555) |
| [#4944](https://github.com/zeroclaw-labs/zeroclaw/pull/4944) | Bundle of wrapper migration for file, pdf/image, cron, AI CLI, runner, network, skill tools | 2026-05-11 | [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/4944) |

Both require author follow-up (e.g., addressing review feedback, merging conflicts). #4944 is a large bundle that overlaps with the newly merged wrapper PRs; it may need rebasing.

### Long-standing open items:

- [#5120](https://github.com/zeroclaw-labs/zeroclaw/pull/5120) – **fix(memory): reject clear on append-only markdown backend** – opened Mar 29, 2026, risk medium. No recent activity from author or maintainers.
- [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) – **audit lost commits** – opened Apr 24, marked high risk and in-progress, but no merged resolution.

These items represent potential technical debt or unresolved regressions that could affect stability. The lost-commits audit (#6074) is particularly concerning for long-term code history integrity.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*