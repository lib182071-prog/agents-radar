# OpenClaw Ecosystem Digest 2026-05-16

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-16 07:32 UTC

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

# OpenClaw Project Digest — 2026-05-16

## Today's Overview

OpenClaw shows **extremely high activity** today with 500 issues and 500 PRs updated in the last 24 hours, indicating a major development push or hot-fix cycle. The project released **two beta versions** today (v2026.5.16-beta.1 and v2026.5.14-beta.2), with changes focused on maintainer tooling, CLI localization, and SDK enhancements. However, the **high open-PR count (463 of 500)** and dense issue tracker suggest the project may be in a **stabilization bottleneck** — many features are implemented but not yet merged, while regressions and bugs continue to surface from recent runtime changes. The QA lab infrastructure (issues #80171, #80319, #80936) indicates an ongoing **Codex-vs-Pi runtime parity** effort driving much of the current work.

---

## Releases

### v2026.5.16-beta.1 (released today)
**Changes:**
- **Maintainer tooling:** Crabbox skill defaults now routed through repo-brokered AWS config; Blacksmith Testbox is an explicit opt-in instead of default.
- **CLI/onboarding:** Setup wizard and bundled channel setup flows now localize for English, Simplified Chinese, and [third language not fully specified in changelog].

**No breaking changes or migration notes documented.**

### v2026.5.14-beta.2 (released today)
**Changes:**
- **Channels/SDK:** Added normalized command turn facts to channel turn construction; exposed command-turn helpers for plugin inbound contexts.
- **Agents/config:** Support for per-agent bootstrap profile overrides for `contextInjection`, `bootstrapMaxChars`, and `bootstrapTotalMaxChars` (inheriting behavior noted but incomplete changelog).

**No breaking changes or migration notes documented.**

---

## Project Progress

**37 PRs merged/closed in the last 24 hours.** Notable merged PRs today:

- **#82395 [MERGED]** — `fix(gateway): isolate gmail watcher restart and abort handling` — Resolves a significant gateway hot-reload issue where Gmail sidecars could run with stale state and abort commands could be misclassified as clean exits.
- **#82301 [CLOSED]** — Stock-to-externalized plugin migration unblocked — Fixes the `doctor:release-configured-plugin-installs` early-return bug that blocked the intended migration cure.
- **#82495 [MERGED]** — `fix(doctor): scope state dir scan to current home` — Security fix: `openclaw doctor` no longer enumerates sibling account home directories, preventing disclosure of other users' OpenClaw state paths.
- **#82347 [CLOSED]** — Telegram infinite retry loop on expired callback_query approval — Fixes a channel-blocking infinite retry bug.
- **#82475 [CLOSED]** — MiMo tool call 400 regression — Fixes `reasoning_content` stripping conflict with MiMo provider requirements.

**Features advanced but not yet merged:**
- **#82349** (PR) — Skill author-defined setup hook plugin — Implements `setup.script` hook in SKILL.md frontmatter as a bundled plugin.
- **#81864** (PR) — Plain-language plugin approvals — Replaces raw debug output in approval prompts with human-readable copy.
- **#82496** (PR) — Codex native tool policy enforcement — Injects policy guard into Codex app-server native shell/file operations.

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#80319** — *QA tool-defaults suite conflates Codex-native tools with OpenClaw dynamic tool parity*  
   14 comments | [![:1:](https://github.githubassets.com/favicons/favicon.svg) 1](https://github.com/openclaw/openclaw/issues/80319)  
   **Analysis:** Core QA infrastructure debate — the harness incorrectly flags tool dropouts that are actually architectural differences between Codex-native and OpenClaw dynamic tool surfaces. The community is pushing for better mock-provider isolation.

2. **#80171** — *Codex-vs-Pi runtime parity QA harness (RFC + tracking)*  
   13 comments | [![:1:](https://github.githubassets.com/favicons/favicon.svg) 1](https://github.com/openclaw/openclaw/issues/80171)  
   **Analysis:** The umbrella issue for the ongoing Codex migration. The community is deeply engaged in validating that the new Codex runtime doesn't regress on Pi-built tool surfaces, doctor migrations, and plugin flows. High maintainer attention.

3. **#79902** — *[Feature]: Add companion-friendly SQLite transcript/session seams*  
   13 comments | [![:2:](https://github.githubassets.com/favicons/favicon.svg) 2](https://github.com/openclaw/openclaw/issues/79902)  
   **Analysis:** Strong demand (2 upvotes) from advanced consumers who need canonical runtime state access without scraping opaque blobs. The follow-up to #78595.

4. **#78308** — *Channel-mediated approval for MCP tool calls (consent envelope)*  
   10 comments | [![:1:](https://github.githubassets.com/favicons/favicon.svg) 1](https://github.com/openclaw/openclaw/issues/78308)  
   **Analysis:** Security-focused feature request — MCP servers need the same approval pipeline as shell-exec calls. Indicates growing MCP adoption and user concern about unguarded state mutations.

5. **#82150** — *DeepSeek V4 via OpenRouter returns 500 error on turns following tool calls*  
   6 comments | [![:3:](https://github.githubassets.com/favicons/favicon.svg) 3](https://github.com/openclaw/openclaw/issues/82150)  
   **Analysis:** High-reaction bug — the `reasoning_content` field injection into assistant messages with `tool_calls` is breaking DeepSeek V4. The 3 upvotes suggest significant user impact.

### Most Active PRs (by comment count)

- **#82349** — Skill setup hook plugin (5 comments)
- **#82395** — Gateway: isolate gmail watcher restart (merged today)
- **#76091** — Discord reply typing lifecycle fix (long-running, still open)

---

## Bugs & Stability

### Critical / High Severity

1. **#50642** — *macOS node auto-trusts first TLS certificate and accepts rogue gateway control*  
   **CVSS 9.0 / 9.5 (Critical)** — Still open. A massive security vulnerability where macOS Node.js auto-trusts the first TLS certificate, enabling rogue gateway control. **No fix PR identified.** This is a **long-unresolved critical security bug** dating to March 2026.

2. **#82462** — *model-fetch streaming response processing starves the event loop*  
   **Just opened today.** SocketError / 30s+ freeze when processing large contexts. The event loop is blocked for 25-30 seconds, causing `liveness` failures. **No fix PR yet.**

3. **#82453** — *Excessive RequestEventLog polling (~1000/sec) causing Nack events*  
   **Just opened today.** OpenClaw gateway sends ~1000 log polling commands per second to Exo, causing system instability. **No fix PR yet.**

4. **#80040** — *Cascading failure: invalidated OAuth produces empty placeholder reply; duplicate tool execution; cold-cache bootstrap loses recent context*  
   **Still open.** Three compounded failure modes in 2026.5.7. **No fix PR yet.**

### Regressions (Beta Release Blockers)

5. **#82343** — *Codex app-server backend timeout — model completes but response never delivered*  
   **Open.** `embedded_run` response delivery deadlock in codex-app-server path. The model generates output but it never reaches Discord/Telegram channels. **No fix PR yet.**

6. **#81214** — *OpenClaw 2026.5.7 subagent regression with Ollama runtimes*  
   **Open.** Major regression affecting native/local subagent execution. **No fix PR yet.**

7. **#81955** — *Injections do not work on 2026.5.12 update — Ollama agents lose persona*  
   **Closed (regression identified).** Agent loses identity despite correct `/context list` output. Fix likely included in today's beta.

### Fixed Today

- **#82150** (DeepSeek V4 500 error) — Closed
- **#82069** (OpenAI-codex OAuth refresh 401) — Closed (post-#80738 fix)
- **#82347** (Telegram infinite retry loop) — Closed
- **#82475** (MiMo tool call 400) — Closed

---

## Feature Requests & Roadmap Signals

### Strong Community Demand (2+ upvotes)

- **#79902** — *SQLite transcript/session seams* (2 upvotes) — Likely to land in next minor release given the database-first runtime work (#78595).
- **#80213** — *Skill author-defined setup hook* (4 upvotes) — Already has a companion PR (#82349) in review. **Strong candidate for next release.**
- **#80520** — *Telegram messages silently dropped* (3 upvotes) — High-impact reliability request.
- **#79625** — *Decouple sidecar startup from ACPX* (2 upvotes, flagged beta release blocker) — High priority.

### Emerging User-Requested Features

- **#82011** — *Input text typo/grammar detection* (1 upvote, Chinese-language feature request) — "非好常好" → "非常好" detection. Addresses context-waste from agent misunderstandings.
- **#71142** — *Configurable upload size limit for Control UI* — Hardcoded 5MB limit blocks legitimate use cases.
- **#38622** — *Workspace file injector does not follow symlinks* — Long-standing limitation for multi-workspace setups.

### What to Expect in Next Release

Based on active PRs and roadmap signals:
- **Codex runtime parity** (PR #80323, issues #80171/#80319) — Beta.5 confidence proof is green; likely to ship when live token-efficiency gates pass.
- **Skill setup hooks** (PR #82349) — Bundled plugin implementation likely to merge this week.
- **Plain-language plugin approvals** (PR #81864) — UX improvement with sufficient proof.
- **MCP tool approval pipeline** (issue #78308) — May be deferred to v2026.5.x due to scope.

---

## User Feedback Summary

### Pain Points (Real User Impact)

- **Message loss / delivery failures:** Multiple reports of silent message drops on Telegram (#80520, #71178) and Discord (#81262). Users report "no sendMessage logged" despite gateway processing.
- **Reboot / restart amnesia:** TUI requires scope re-approval after reboot despite valid tokens (#80730). Claude CLI sessions lose context on rotation (#80905).
- **Performance degradation:** `sessions.list` takes 10-16s under load (#75839); `model-resolution` takes 7-8s per run (#78851); excessive polling causes Nack events (#82453).
- **Regressions from rapid releases:** Multiple users on 2026.5.12 report persona loss (#81955), DeepSeek 500 errors (#82150), and plugin migration blockers (#82301).

### Satisfaction Signals

- **QA infrastructure appreciation:** The detailed confidence proofs (#80936, #80411) and parity harness (#80171) suggest maintainers are investing heavily in quality — several community members have engaged constructively.
- **MCP approval pipeline request (#78308)** has clear community consensus — users want unified security controls across all tool types.
- **Companion-friendly SQLite seams (#79902)** indicates advanced users are building on OpenClaw and need programmatic access.

### Dissatisfaction Signals

- **"Beta release blocker" tags** on #79625, #81955 (now closed) indicate users feel recent betas introduced regressions that shouldn't have shipped.
- **Silent failures** (Telegram drops, Media directive swallowing) erode trust — PR #69310 (surface dropped media) has been open since April 20.

---

## Backlog Watch

### Issues Needing Maintainer Attention

1. **#50642** — *macOS node auto-trusts first TLS certificate (CVSS 9.0)*  
   **Created: 2026-03-19** — Critical security vulnerability. 7 comments, **no maintainer response since March 23**. This is the highest-severity open issue in the tracker and appears abandoned.

2. **#38622** — *Workspace file injector does not follow symlinks*  
   **Created: 2026-03-07** — 4 comments, no resolution. Blocks multi-workspace setups that rely on shared IDENTITY.md/SOUL.md via symlinks.

3. **#1210** — *Images from Discord stored as base64 in session transcripts*  
   **Created: 2026-01-19** — 7 comments. Causes context overflow after ~7 images. Currently closed but may need re-evaluation — no comprehensive solution merged.

4. **#68751** — *session-memory: raw prior-session turns replay as current input on /reset*  
   **Created: 2026-04-19** — 4 comments. Autonomous re-execution of prior user commands. Still open, no PR.

5. **#71412** — *stopChannel abort-timeout leaves zombie task in store*  
   **Created: 2026-04-25** — 6 comments. Prevents health-monitor restart. No PR.

### Long-Open PRs Stalled

- **#69310** (Fix: surface dropped media instead of swallowing) — Open since April 20, 3 comments, labeled `needs-real-behavior-proof`.
- **#49044** (Per-account SOUL files) — Open since March 17, stalled.
- **#47090** (Session archiving) — Open since March 15, `dirty-candidate` status.
- **#46753** (Cap global cache maps to prevent memory leaks) — Open since March 15, `size: XL` — addresses a real long-running daemon concern.

---

*Generated from openclaw/openclaw GitHub activity data as of 2026-05-16T23:59:59Z.*

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**2026-05-16 | Analyst Assessment**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing an **acceleration phase**, driven by two dominant tensions: the migration from proprietary runtime architectures (Pi → Codex) and the growing demand for provider diversity to reduce Anthropic/OpenAI lock-in. Projects are converging on a shared set of infrastructure concerns—secure tool execution, multi-channel messaging gateways, and persistent memory systems—while diverging starkly in architectural philosophy (monolithic vs. microservice, Python vs. Rust vs. TypeScript). The ecosystem shows signs of maturation, with several projects reaching v0.8+ stability and formalizing release processes, but proliferation of nearly identical forks (Claw variants) risks fragmentation and user confusion. A critical security vulnerability (OpenClaw #50642, CVSS 9.0) remains unfixed across all projects that inherit its macOS TLS auto-trust behavior, underscoring the risk of shared codebases without coordinated security patching.

---

## 2. Activity Comparison (24h Window: 2026-05-15 → 2026-05-16)

| Project | Issues Updated | PRs Updated | Merged/Closed PRs | New Release | Health Score | Primary Activity Driver |
|---------|---------------|-------------|-------------------|-------------|--------------|------------------------|
| **OpenClaw** | 500 | 500 | 37 | v2026.5.16-beta.1 | 🟡 Stabilization bottleneck (463 open PRs) | Codex-vs-Pi runtime parity |
| **NanoBot** | 57 | 23 | 17 | None | 🟢 Strong | Documentation & code annotation sprint |
| **Hermes Agent** | 50 | 50 | 13 | None | 🟢 Strong | Bug fixes & feature PRs |
| **NanoClaw** | 50 | 50 | 39 | v2.0.63 | 🟢 Very strong | First official GitHub Release + bug fixes |
| **ZeroClaw** | 21 | 50 | 5 | None (v0.8.0 pending) | 🟡 Rapid development | Multi-agent runtime PR #6398 |
| **PicoClaw** | 9 | 20 | 7 | v0.2.8-nightly | 🟢 Moderate | Audio input, MCP fixes |
| **CoPaw (QwenPaw)** | 17 | 34 | 19 | None (v1.1.7 stable) | 🟢 Strong | Security hardening, provider flexibility |
| **IronClaw** | 21 | 50 | 28 | None | 🟢 Intense sprint | Reborn architecture cutover |
| **LobsterAI** | ~5 | 21 | 9 | None | 🟢 Moderate | Bug fixes + stale PR cleanup |
| **Moltis** | 8 (all closed) | 8 | 7 | None | 🟢 Strong | Remote access, agent builder skill |
| **NullClaw** | 2 | 0 | 0 | None | 🔴 Quiet | Bug report + feature request |
| **TinyClaw** | 0 | 0 | 0 | None | ⚫ Inactive | No activity |
| **ZeptoClaw** | 0 | 0 | 0 | None | ⚫ Inactive | No activity |

**Health Score Legend:** 🟢 Strong (responsive maintainers, low open-PR/issue ratio) | 🟡 Moderate (high churn, notable blockers) | 🔴 Concerning (low engagement, critical bug unresolved) | ⚫ Inactive

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Reference implementation status**: OpenClaw is the upstream for 6+ Claw forks (NanoClaw, PicoClaw, NullClaw, TinyClaw, ZeptoClaw, CoPaw). Its architectural decisions propagate downstream.
- **Largest community**: 500 issues/PRs in 24h dwarfs all peers. High signal-to-noise ratio in issue discussions indicates deep technical engagement.
- **QA infrastructure maturity**: Detailed confidence proofs (#80936, #80411) and parity harness documentation (#80171) are unmatched. Other projects rely on ad-hoc testing.
- **SDK & plugin ecosystem**: Skill author-defined setup hooks (#82349) and plain-language approvals (#81864) demonstrate investment in extensibility.

**Technical Approach Differences:**
- **Runtime abstraction layer**: OpenClaw explicitly supports Codex and Pi runtimes with parity guarantees—a complexity none of the other projects addresses directly. This creates both technical debt and competitive advantage.
- **Plugin architecture**: OpenClaw's plugin system (bundled, channel-mediated, with approval pipelines) is more sophisticated than NanoBot's skill system or Hermes Agent's extensions.
- **Modular gateway**: Dedicated channel abstraction (Gmail watcher restart isolation, Telegram retry fixes) shows production-oriented design. Most peers have monolithic gateway implementations.

**Community Size Comparison:**
- OpenClaw has the highest raw engagement (500 issues, 500 PRs) but also the highest open-PR stagnation (463 of 500, 92.6%). Only 37 PRs merged in 24h—a 7.4% merge rate. By contrast, NanoClaw merged 39 of 50 PRs (78%) and Moltis merged 7 of 8 (87.5%). This suggests OpenClaw's review pipeline is a bottleneck relative to its contributor base.

**Risk**: The unfixed critical TLS vulnerability (#50642, CVSS 9.0) with no maintainer response since March 23 poses a systemic risk to all Claw forks that inherit OpenClaw's macOS gateway code.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects Involved | Specific Requirements |
|------------|------------------|----------------------|
| **Codex Runtime Parity** | OpenClaw (#80171, #80319), NanoBot (#3793) | Prompt cache key stability, tool surface equivalence, streaming reasoning preservation |
| **MCP Tool Approval Security** | OpenClaw (#78308), ZeroClaw (#6699), CoPaw (MCP collision fix #4428) | Consent envelope, channel-mediated approval, filter group no-op fixes |
| **Session/Memory Persistence** | OpenClaw (#79902 SQLite seams), Hermes Agent (#346 structured memory), ZeroClaw (#6693 dream mode), CoPaw (#4162 zombie sessions) | Companion-friendly runtime state access, entity linking, soft-delete, memory consolidation |
| **Provider Diversity** | NanoClaw (#80 multi-provider), CoPaw (#4387 custom Anthropic base URL), LobsterAI (#1988 model routing regression), Hermes Agent (#26105 DeepSeek billing) | OpenRouter, Gemini, LiteLLM, custom endpoints, fallback on quota errors |
| **Multi-Channel Gateway** | OpenClaw (Gmail, Discord, Telegram), Hermes Agent (Telegram SIGSEGV, WhatsApp timeout), PicoClaw (Matrix identity), LobsterAI (pairing codes), NanoClaw (Slack threads) | Channel-specific bug fixes, identity injection, OAuth refresh, rate limiting |
| **Audio/Vision Support** | PicoClaw (#2626 audio input), CoPaw (image recognition skill), OpenClaw (Discord image storage) | Multimodal LLM integration, voice transcription, inline media payloads |
| **Regressive Update Safety** | OpenClaw (#82343, #81955), Hermes Agent (#26804 .env stripping, #26737 cron deletion), LobsterAI (#1988 model routing) | Configuration preservation during updates, rollback safety, migration testing |

**Observation**: No single project excels across all focus areas. OpenClaw leads on runtime parity and security architecture but lags on update safety. NanoClaw excels at operational reliability but lacks sophisticated memory features. ZeroClaw pushes multi-agent orchestration but has severe SOP subsystem bugs.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | NanoBot | Hermes Agent | NanoClaw | ZeroClaw | CoPaw |
|-----------|----------|---------|--------------|----------|----------|-------|
| **Primary User** | Advanced power users, developers building on top | Developers who want low-commitment quick start | Power users needing platform stability | Users fleeing Anthropic lock-in | Multi-agent orchestration teams | Chinese-speaking users, Alibaba ecosystem |
| **Architecture** | Monolithic (Python) with plugin system | Lightweight modular (Python) | Monolithic (Node.js) | Microservice? (Docker-centric) | Rust native + WASM sandbox | Desktop app + plugins (TypeScript) |
| **Runtime** | Codex + Pi (dual) | OpenAI-compatible | OpenAI + Anthropic + OpenRouter | Anthropic-focused, moving to OpenRouter | Custom Rust agent runtime | Qwen + Anthropic |
| **Memory** | SQLite sessions (#79902 RFC) | Basic session store | Structured memory (#346 closed) | Context compaction skill | Dream mode (#6693, open) | Session-based (zombie bug #4162) |
| **Deployment** | Self-hosted, complex | pip install, simple | Homebrew + manual | Docker required | Rust binary + Nix | Desktop app + Docker |
| **Maturity** | v2026.5.x (beta churn) | 0.1.5.post3 (early) | Unversioned (rapid) | v2.0.63 (mature release) | v0.7.x (pre-0.8) | v1.1.7 (stable) |
| **Security** | Mixed: robust plugin approval but unfixed TLS CVE | Good: media attachment fix (#3842) | Critical: .env stripping, cron deletion | Good: OAuth health monitor (#2505) | Mixed: path policy fixes but SOP audit silent | Good: backup HMAC, but plaintext config leak |

**Key Insight**: The ecosystem is bifurcating between **"Claw-compatible" forks** (PicoClaw, NullClaw, TinyClaw, ZeptoClaw) that inherit OpenClaw's architecture but often lag on fixes, and **"independent agents"** (NanoBot, Hermes Agent) that build from scratch and ship faster but lack ecosystem leverage. NanoClaw and CoPaw occupy a middle ground—derived but with significant diverging investments.

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration (high PR throughput, responsive maintainers)**
- **NanoClaw**: 39 PRs merged in 24h, 78% merge rate, first official GitHub Release. Strongest ratio of merged-to-open work.
- **ZeroClaw**: 50 PRs updated, but only 10% merged. High community contribution volume but review pipeline is the bottleneck.
- **IronClaw**: 28 merges in 24h with explicit Reborn architecture milestones. Structured roadmap but downstream publishing blocked.

**Tier 2 — Strong but Strategic (focused work, lower volume)**
- **OpenClaw**: Massive raw volume but stabilization bottleneck. Merge rate is lowest among active projects.
- **Hermes Agent**: Responsive bug fixing (13 merges) but Telegram instability erodes trust. Two P1 bugs opened and fixed same day.
- **Moltis**: 7/8 PRs merged (=87.5%), all bugs fixed within 24h. Smallest project but highest quality signal.

**Tier 3 — Stabilizing / Catch-up**
- **PicoClaw**: Nightly builds, steady fixes, but LM Studio integration (#28, open since Feb) and exec guard bug (#1042) unresolved for months.
- **CoPaw (QwenPaw)**: Healthy activity but core reliability bugs (write_file infinite loop, zombie sessions) are not yet fixed. Features outpacing stability.

**Tier 4 — Quiet / Inactive**
- **NullClaw**: Two new issues, zero PRs. Low community engagement. May be a single-maintainer project.
- **TinyClaw & ZeptoClaw**: No activity. Risk of abandonment.

**Maturity Assessment**: The ecosystem has an **upstream bottleneck** problem. OpenClaw, as the reference implementation, processes contributions slowly (7.4% merge rate). Downstream projects that maintain closer sync (NanoClaw) ship faster but diverge, while those that stay passive (NullClaw, TinyClaw) risk accumulating unpatched vulnerabilities from upstream.

---

## 7. Trend Signals (for AI Agent Developers)

1. **Provider diversity is the #1 community demand**. Users across OpenClaw, NanoClaw, CoPaw, and Hermes Agent are fleeing Anthropic/OpenAI due to account bans, cost, and quotas. LiteLLM, OpenRouter, and self-hosted endpoints are becoming table stakes. **Takeaway:** Build agents with pluggable backend layers from day one.

2. **Memory is the next frontier after conversation**. Three projects (OpenClaw #79902, Hermes Agent #346, ZeroClaw #6693) are independently building structured memory systems—SQLite seams, entity graphs, and "dream mode" consolidation. The industry is moving beyond chat logs to persistent, queryable agent memory. **Takeaway:** Invest in RAG and memory APIs now; they will differentiate agents in 6–12 months.

3. **Tool call security is a first-class concern**. MCP approval pipelines, consent envelopes, and path policy enforcement appear across OpenClaw, ZeroClaw, CoPaw, and PicoClaw. Uncontrolled tool calls are the most dangerous attack vector. **Takeaway:** Implement layered security (allowlist + regex guards + approval prompts + audit logging) from the start.

4. **Multi-channel gateways cause disproportionate bugs**. Telegram drops, Matrix identity injection, WhatsApp timeouts, and OAuth token refresh failures account for the majority of user-reported pain. This area is undervalued—every project underestimates channel-specific complexity. **Takeaway:** If your agent supports more than one platform, budget 40% of QA effort for channel-specific edge cases.

5. **Update safety is a trust crisis**. Hermes Agent users lost crons and .env files. LobsterAI forced a model routing change. OpenClaw betas introduce regressions. The rapid release cadence is alienating users who need stability. **Takeaway:** Implement configuration snapshots, rollback procedures, and canary testing before anyone else in the ecosystem does—it's a competitive advantage.

6. **The Claw ecosystem needs governance**. Six "Claw" projects exist with shared architecture but no coordinated security patching, no shared CVE process, and diverging features. A single unfixed TLS vulnerability (OpenClaw #50642) silently affects all forks. **Takeaway:** Consider adopting OpenSSF Scorecard or creating an ecosystem-wide security working group. The fragmentation without coordination creates systemic risk.

7. **Low-resource deployment is growing**. Requests for Podman support (NanoClaw), Raspberry Pi compatibility (Hermes Agent), and Termux on Android (PicoClaw) show agents are being deployed beyond cloud servers. **Takeaway:** Design for memory-constrained environments. Expose configurable timeouts and lightweight alternatives to Docker.

---

*Report generated from community digest summaries dated 2026-05-16. Data reflects 24-hour update windows for each project's GitHub activity. Health scores are analyst assessments based on merge rates, issue closure patterns, and bug severity.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-16

---

## Today’s Overview

NanoBot experienced an extraordinary surge in activity over the past 24 hours, driven primarily by a coordinated, large-scale documentation and code annotation initiative. Out of 57 updated issues, 54 were closed, and of 23 updated pull requests, 17 were merged or closed. This indicates a focused effort to improve project documentation, developer onboarding, and codebase clarity rather than routine development churn. One new open bug (#3790) regarding WebUI rendering remains active. No new releases were published today. Overall, project health appears strong with high maintainer responsiveness and active community participation.

## Releases

No new releases were published in the last 24 hours. The latest available version remains `0.1.5.post3.2026.05.13`.

## Project Progress

A significant number of pull requests were merged today, reflecting progress across multiple areas:

- **Codex Cache Stability** — PR #3793 (merged) stabilizes the Codex Responses API `prompt_cache_key` across conversation turns, fixing a long-standing issue where the cache key changed every turn.
- **Brave Search Rate Limiting** — PR #3840 (merged) adds automatic retry with backoff when Brave search returns HTTP 429, improving reliability for serial tool calls.
- **Gateway Lifecycle Notifications** — PR #3373 and PR #3792 (both merged) add `on_start` / `on_stop` notification hooks for gateway lifecycle, fulfilling feature request #3279.
- **Long-Task Infrastructure** — PR #3460 and PR #3788 (both merged) introduced a LongTaskTool and `/goal` command for multi-step agent tasks, including session metadata persistence and WebUI integration.
- **MiMo Thinking Control** — PR #3734 and PR #3844 (both merged) wire MiMo thinking control for both direct and gateway providers, and improve runtime context placement for cache stability.
- **Security Fix** — PR #3842 (merged) confines local media attachments in the `message` tool when workspace restriction is enabled.
- **Developer Experience** — PR #3850 (merged) fixes a misleading `ruff format` instruction in contributing docs that caused large unrelated diffs.
- **New Provider** — PR #3750 (merged) adds first-class support for Atomic Chat as a local OpenAI-compatible LLM provider.
- **Documentation & Code Annotation** — A large batch of issues (#3815–#3839, #3822–#3831) were closed, corresponding to merged PRs that created Chinese-language documentation (quick-start, deployment, development, extension guides, security, performance, gotchas) and added Chinese annotations across core modules (Agent, tools, providers, bus, WebUI, etc.). Mermaid architecture, flowchart, sequence, and data-structure diagrams were also added.

## Community Hot Topics

- **#3790 [OPEN] — WebUI rendering bug** (11 comments)  
  URL: [Issue #3790](https://github.com/HKUDS/nanobot/issues/3790)  
  This is the only open issue with significant discussion. The user reports that after updating to the latest source, WebUI session content displays incorrectly (text is jumbled) until the page is refreshed. The high comment count suggests other users may be experiencing similar behavior. No fix PR has been linked yet.

- **#3854 [OPEN] — Peer roster via bootstrap endpoint**  
  URL: [PR #3854](https://github.com/HKUDS/nanobot/pull/3854)  
  This new PR proposes an optional peer-discovery injection point in the WebUI bootstrap endpoint, enabling multi-instance orchestration scenarios. It signals growing interest in multi-agent, multi-container deployments.

- **#3852 [OPEN] — Signal channel support**  
  URL: [PR #3852](https://github.com/HKUDS/nanobot/pull/3852)  
  A substantial PR adding Signal messenger integration via signal-cli daemon, including DMs, group chats, attachments, and typing indicators. This reflects strong community desire for diverse communication channel support.

## Bugs & Stability

| Severity | Issue | Description | Linked Fix PR |
|----------|-------|-------------|---------------|
| High | [#3790](https://github.com/HKUDS/nanobot/issues/3790) [OPEN] | WebUI session content display corruption after update; requires page refresh to restore. | None yet |
| Medium | [#3853](https://github.com/HKUDS/nanobot/pull/3853) [OPEN] | `ExecTool` deny pattern incorrectly blocks `format` in URL query parameters (e.g., `&format=json`), breaking legitimate curl commands. | PR #3853 (open) |
| Low | [#3849](https://github.com/HKUDS/nanobot/issues/3849) [CLOSED] | `ruff format` instruction in developer docs produced ~80-file unrelated diff on fresh clone. | PR #3850 (merged) |
| Low | [#3842](https://github.com/HKUDS/nanobot/pull/3842) [MERGED] | Security: `message` tool allowed LLM-controlled local file attachment paths in restricted deployments. | PR #3842 (merged) |

The most pressing bug is the WebUI rendering issue (#3790), which directly impacts user experience for all users of the latest codebase. No maintainer has responded publicly yet, but the high activity level suggests attention is likely.

## Feature Requests & Roadmap Signals

Several user-requested features were fulfilled today:

- **Gateway lifecycle notifications** (#3279) — now merged in PR #3373.
- **Secret reference support** (#2172) — remains a good-first-issue but no new PR linked.
- **Signal channel** — PR #3852 adds this highly requested integration.
- **Peer discovery / multi-instance** — PR #3854 proposes bootstrap-level peer roster support.

Predictions for next release:
- **Signal Channel** — PR #3852 is feature-complete and likely to be merged soon.
- **Multi-instance peer discovery** — PR #3854 may land if maintainers accept the approach.
- **Long-task and planning tools** — PR #3460, #3788, and #3791 (open) together form a coherent suite for task decomposition and sustained goal tracking; once #3791 is reviewed, the full feature set could ship together.

## User Feedback Summary

Real user pain points visible in today's data:

- **WebUI stability**: The rendering bug (#3790) is the most vocal complaint, indicating the new build introduced a regression that affects daily use.
- **Tool restrictions too aggressive**: PR #3853 highlights that security-focused deny patterns in `ExecTool` are breaking legitimate commands (e.g., weather API queries with `&format=json`).
- **Developer onboarding friction**: Issue #3849 (now fixed) showed that new contributors hit a confusing wall when running `ruff format` on a fresh clone.
- **Desire for more channels**: PR #3852 (Signal) and the high activity around channel features indicate users want more messaging integrations beyond Telegram/Discord.
- **Security consciousness**: Issue #2172 (secret references) and the media attachment fix (#3842) show users are actively thinking about secure deployments.

User satisfaction is reflected in the rapid closure of documentation and feature PRs, suggesting responsive maintainers. However, the open WebUI bug may erode trust if not addressed quickly.

## Backlog Watch

While today's activity resolved many items, a few long-standing items bear watching:

- **#2172 — Secret reference support** ([Issue](https://github.com/HKUDS/nanobot/issues/2172)):  
  Created 2026-03-17, labeled `good first issue`, with 5 comments. No PR has been submitted despite being open for two months. As a security-related feature, this may benefit from maintainer attention or a nudge.

- **#3790 — WebUI rendering bug** ([Issue](https://github.com/HKUDS/nanobot/issues/3790)):  
  The most recent high-comment open issue. No maintainer response or linked fix PR yet. Given its impact on the UI, this should be a top priority.

No other issues older than 30 days with significant comment counts appear in today's data. The high closure rate suggests the project maintains a healthy triage cadence.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-05-16

## Today’s Overview

The project shows **very high activity** with 50 issues and 50 pull requests updated in the last 24 hours. 19 issues were closed and 13 PRs were merged/closed, indicating a rapid pace of both bug fixing and feature landing. Several critical bugs were reported today (P1 – .env stripping, P1 – cron deletion) and corresponding fix PRs were opened within hours, demonstrating responsive maintenance. Community engagement remains strong, with users filing feature requests and reporting real-world stability problems across multiple platforms (Telegram, WhatsApp, Feishu, Raspberry Pi). No new releases were cut today.

## Releases

No new releases today.

## Project Progress

13 PRs were merged or closed in the last 24 hours. Although the snapshot lists only one closed PR in the top 20 ([#26667](https://github.com/NousResearch/hermes-agent/pull/26667) – expose provider models in `/v1/models`), the overall total of 13 merged/closed PRs indicates active development. Key areas of progress visible from open PRs that are likely to merge soon:

- **Auxiliary fallback fix** ([#26809](https://github.com/NousResearch/hermes-agent/pull/26809)) – detects quota keywords in 429 responses to trigger fallback providers.
- **`.env` stripping fix** ([#26807](https://github.com/NousResearch/hermes-agent/pull/26807)) – preserves user-added environment variables during `hermes update`.
- **MiMo thinking blocks** ([#26802](https://github.com/NousResearch/hermes-agent/pull/26802)) – preserves reasoning content on Anthropic replay for Xiaomi models.
- **Kanban context pollution** ([#26730](https://github.com/NousResearch/hermes-agent/issues/26730)) – bug reported and fix being addressed in context handling PRs.
- **Feishu card rendering** ([#26797](https://github.com/NousResearch/hermes-agent/pull/26797)) – uses interactive card schema 2.0 for full markdown support.
- **Plugin context preservation** ([#26798](https://github.com/NousResearch/hermes-agent/pull/26798)) – preserves `pre_llm_call` context through compression paths.
- **Holographic memory entity linking** ([#26794](https://github.com/NousResearch/hermes-agent/pull/26794)) – links known product entities during memory extraction.
- **Windows bootstrap** ([#26620](https://github.com/NousResearch/hermes-agent/pull/26620)) – brings `install.ps1 -Ensure`/`-PostInstall` parity with Linux/macOS.
- **Dashboard Clean Dark theme** ([#26801](https://github.com/NousResearch/hermes-agent/pull/26801)) – new built-in theme for the web UI.

## Community Hot Topics

The most active discussions (by comment count and reactions) reveal both excitement and frustration:

- **Structured Memory System** ([#346](https://github.com/NousResearch/hermes-agent/issues/346) – 8 comments, 2 👍) – Closed today. This major feature request for typed nodes, graph edges, and hybrid search was likely implemented or otherwise resolved. Represents strong community desire for richer memory beyond flat files.
- **Homebrew install missing skills** ([#24360](https://github.com/NousResearch/hermes-agent/issues/24360) – 6 comments) – User reports that Homebrew-packaged Hermes ships with an empty `skills/` folder. Suggests the Homebrew formula may be outdated.
- **Gateway RBAC** ([#527](https://github.com/NousResearch/hermes-agent/issues/527) – 6 comments) – Proposal for role-based access control (Owner/Admin/User/Guest) on messenger platforms. Indicates growing production use where multi-user permission is needed.
- **Telegram suddenly stops working** ([#26580](https://github.com/NousResearch/hermes-agent/issues/26580) – 5 comments) – A highly frustrated user reports daily failures, Telegram requiring re‑authorisation, and even attempted self-destruction. No dev response visible, increasing tension.
- **WhatsApp npm install timeout** ([#14980](https://github.com/NousResearch/hermes-agent/issues/14980) – 5 comments, 3 👍) – Hardcoded 60‑second timeout fails on slow NAS/container systems. A test PR ([#26795](https://github.com/NousResearch/hermes-agent/pull/26795)) adds coverage for the new 300s default, indicating a fix is in progress.
- **Extension system / Tool interception** ([#359](https://github.com/NousResearch/hermes-agent/issues/359) – 6 comments, 3 👍) – Inspired by Pi coding agent, this feature request for richer lifecycle events and tool interception was closed today, likely merged or superseded.
- **Multi‑model routing** ([#157](https://github.com/NousResearch/hermes-agent/issues/157) – 2 comments, 10 👍) – High user demand for configurable model routing by capability categories. Closed today – may be part of the upcoming release.

## Bugs & Stability

Several high-severity bugs were reported today. Most have immediate fix PRs.

| Severity | Bug | Status / PR |
|----------|-----|-------------|
| **P1** | `.env` file silently stripped during `hermes update` ([#26804](https://github.com/NousResearch/hermes-agent/issues/26804)) | Fix PR [#26807](https://github.com/NousResearch/hermes-agent/pull/26807) opened same day |
| **P1** | Update deleted all crons ([#26737](https://github.com/NousResearch/hermes-agent/issues/26737)) | No PR yet – maintainer attention needed |
| **P2** | Auxiliary `call_llm` fallback not triggered on quota 429 ([#26803](https://github.com/NousResearch/hermes-agent/issues/26803)) | Fix PR [#26809](https://github.com/NousResearch/hermes-agent/pull/26809) |
| **P2** | `delegate_task` ignores parent runtime `base_url`/`api_key` ([#26722](https://github.com/NousResearch/hermes-agent/issues/26722)) | No PR yet |
| **P2** | Kanban workers fail due to context pollution from parent session ([#26730](https://github.com/NousResearch/hermes-agent/issues/26730)) | No PR yet, but related compression fix [#26798](https://github.com/NousResearch/hermes-agent/pull/26798) may help |
| **P2** | Telegram gateway SIGSEGV on Raspberry Pi aarch64 ([#25666](https://github.com/NousResearch/hermes-agent/issues/25666)) | No PR yet; reported 2 days ago |
| **P2** | Long‑running gateway tasks drop off without durable stall detection ([#26410](https://github.com/NousResearch/hermes-agent/issues/26410)) | No PR yet |
| **P2** | Dashboard OOM on low‑memory VPS due to full rebuild on every startup ([#14898](https://github.com/NousResearch/hermes-agent/issues/14898)) | Closed – fix merged? |
| **P2** | Unreliable Telegram gateway (daily token refresh, self-deletion attempts) ([#26580](https://github.com/NousResearch/hermes-agent/issues/26580)) | No dev response; user extremely dissatisfied |
| **P3** | MiMo thinking blocks stripped causing HTTP 400 ([#26774](https://github.com/NousResearch/hermes-agent/issues/26774)) | Fix PR [#26802](https://github.com/NousResearch/hermes-agent/pull/26802) |
| **P3** | Unexpected charges while using DeepSeek V4 Flash (model mismatch) ([#26105](https://github.com/NousResearch/hermes-agent/issues/26105)) | No PR yet |

**Stability trend:** The number of platform-specific crashes (Telegram, WhatsApp, Feishu) and regressions caused by updates (cron deletion, .env stripping) is concerning. The community appears to be using Hermes in diverse, often low‑resource environments (Raspberry Pi, NAS, VPS with ≤1GB RAM), exposing timeout and memory issues.

## Feature Requests & Roadmap Signals

- **Native Nia retrieval toolset** ([PR #26805](https://github.com/NousResearch/hermes-agent/pull/26805)) – Adds a new toolset for repository retrieval, web search, and source management. Likely to be in next release.
- **Suppress skills injection for scripted use** ([#26806](https://github.com/NousResearch/hermes-agent/issues/26806)) – Users running high‑frequency scripts want to avoid the ~14k token `available_skills` block when no tool use is needed. A pragmatic optimisation.
- **Clean Dark dashboard theme** ([PR #26801](https://github.com/NousResearch/hermes-agent/pull/26801)) – Minimal, image‑free alternative for users who dislike the default background.
- **Plugin startup advisory API** ([PR #26792](https://github.com/NousResearch/hermes-agent/pull/26792)) – Lets plugins register one-line startup notices; improves visibility of plugin health.
- **Gateway RBAC** ([#527](https://github.com/NousResearch/hermes-agent/issues/527)) – Role‑based access for messenger platforms; signals enterprise/team use.
- **Configurable platform notes** ([#2020](https://github.com/NousResearch/hermes-agent/issues/2020)) – Users want to customise the hardcoded "Platform notes" that describe what each gateway can/can’t do.
- **Email account variable** ([#25849](https://github.com/NousResearch/hermes-agent/issues/25849)) – `EMAIL_ACCOUNT` needed when the email address differs from the account name.
- **Structured Memory System** ([#346](https://github.com/NousResearch/hermes-agent/issues/346)) – Closed today; likely to land in the next major version, given the high community interest.

**Prediction:** The next release will likely include the Nia toolset, dashboard Clean Dark theme, plugin startup advisories, and fixes for the top P1 bugs. Multi‑model routing and RBAC may follow soon.

## User Feedback Summary

**Positive signals:**
- Users are actively proposing high-quality features (memory system, extensions, RPC mode, evolutionary self‑improvement).
- The community contributes PRs for both features and bug fixes – today saw contributions from at least 12 different authors.
- The Homebrew and Windows packaging gaps are being addressed (PRs [#24360](https://github.com/NousResearch/hermes-agent/issues/24360) and [#26620](https://github.com/NousResearch/hermes-agent/pull/26620) show progress).

**Pain points and dissatisfaction:**
- **Telegram reliability** is the most vocal pain point: user “fwends” reports “Hermes has made my life worse not better”, with daily token resets and even self‑deletion attempts ([#26580](https://github.com/NousResearch/hermes-agent/issues/26580)). Another user lost all crons after an update ([#26737](https://github.com/NousResearch/hermes-agent/issues/26737)).
- **Update regressions** – two separate users report `hermes update` destroying configuration (`.env` stripped, crons deleted). This erodes trust in the update process.
- **Resource constraints** – users on low‑memory VPS, Raspberry Pi, and Docker on Unraid hit OOM crashes and npm install timeouts. The hardcoded 60s timeout for WhatsApp bridge is a recurring complaint.
- **Unexpected billing** – one user ([#26105](https://github.com/NousResearch/hermes-agent/issues/26105)) discovered Hermes silently switched from DeepSeek V4 Flash to the more expensive Pro model, draining the API balance.
- **Configuration inflexibility** – the inability to set per‑tool model routing or separate account names for email remains a friction point.

Overall, while the project is innovating rapidly, the pace may be causing regression pain for some users, especially around gateway stability and update safety.

## Backlog Watch

The following items have been open for some time without a clear resolution or maintainer response:

- **Homebrew‑installed Hermes missing skills** ([#24360](https://github.com/NousResearch/hermes-agent/issues/24360)) – Opened May 12, 6 comments, no maintainer acknowledgment. The Homebrew formula may need updating.
- **WhatsApp bridge npm install timeout** ([#14980](https://github.com/NousResearch/hermes-agent/issues/14980)) – Opened April 24, 3 👍, 5 comments. A test PR exists ([#26795](https://github.com/NousResearch/hermes-agent/pull/26795)) but the actual fix branch is unclear.
- **`hermes upgrade` silently fails optional extras** ([#10651](https://github.com/NousResearch/hermes-agent/issues/10651)) – Opened April 16, 2 👍, 1 comment. No PR yet; the fix in [#10733](https://github.com/NousResearch/hermes-agent/pull/10733) adds warnings but is still open.
- **Make platform notes configurable** ([#2020](https://github.com/NousResearch/hermes-agent/issues/2020)) – Opened March 19, 3 comments. No activity from maintainers.
- **`delegate_task` ignores parent runtime config** ([#26722](https://github.com/NousResearch/hermes-agent/issues/26722)) – Filed today but important for multi‑agent setups; no fix PR yet.
- **Telegram SIGSEGV on Pi** ([#25666](https://github.com/NousResearch/hermes-agent/issues/25666)) – Opened May 14, 2 comments. Affects multiple profiles, no maintainer reply yet.

These items may require maintainer prioritisation to avoid community frustration and to ensure the project’s stability reputation improves.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-16

## Today's Overview
Development activity remains high with 20 pull requests updated in the last 24 hours (13 open, 7 merged/closed) and 9 new or active issues. A nightly build v0.2.8-nightly.20260516 was released, reflecting ongoing work on the next stable release. The community is engaged, but several long-standing bugs and feature requests are still pending maintainer action. Notable progress was made in audio input support, MCP integration, streaming reasoning fixes, and documentation alignment. However, a few regressions and configuration gaps were also reported.

## Releases
- **Nightly Build (`v0.2.8-nightly.20260516.0df050ff`)**  
  Automated unstable build from the `main` branch.  
  **Changelog**: [compare/v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
  *No migration notes or breaking changes documented.*

## Project Progress (Merged/Closed PRs Today)
Seven pull requests were merged or closed in the last 24 hours:

| PR | Description |
|----|-------------|
| [#2626](https://github.com/sipeed/picoclaw/pull/2626) | **feat(agent):** Add native audio input support for multimodal LLMs (e.g., Gemini 1.5) — audio MIME detection, data URL encoding in `Message.Audio` field. |
| [#2270](https://github.com/sipeed/picoclaw/pull/2270) | **fix(config):** Prevent panic in `collectSensitive` when iterating over non-addressable `SecureString` map values. |
| [#2766](https://github.com/sipeed/picoclaw/pull/2766) | **docs:** Sync all 26 documentation files to the V3 config format (`api_key` → `api_keys`, `channels` → `channel_list`, version bump). |
| [#2811](https://github.com/sipeed/picoclaw/pull/2811) | **fix(mcp):** Support streamable HTTP alias, request-response mode, and introduce a generic Docker-backed integration testing framework. |
| [#2741](https://github.com/sipeed/picoclaw/pull/2741) | **fix(openai_compat):** Parse `reasoning_content` in streaming responses and preserve reasoning fields. |
| [#2862](https://github.com/sipeed/picoclaw/pull/2862) | **fix(openai_compat):** Align MiMo multi-turn thinking-mode replay with DeepSeek’s canonical reasoning rules. |
| [#2874](https://github.com/sipeed/picoclaw/pull/2874) | **fix(pico):** Preserve image media across pico attachments and client, including inline payload parsing from `media` and `attachments`. |

**Key advancements:** Audio input infrastructure, streaming reasoning robustness, MCP transport flexibility, and configuration safety.

## Community Hot Topics

| Issue / PR | Comments | Reactions | Summary |
|------------|----------|-----------|---------|
| [#28 – LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28) | 19 | 👍 2 | Long-standing feature request (since Feb) for simplified LM Studio integration. User requests “easy way to connect.” |
| [#1042 – Exec tool guardCommand path issue](https://github.com/sipeed/picoclaw/issues/1042) | 11 | 👍 2 | `restrict_to_workspace` blocks legitimate commands like `curl` by misinterpreting relative paths (e.g., `../../../../Beijing?T`). |
| [#2785 – ToolFeedbackAnimator Feishu notification](https://github.com/sipeed/picoclaw/issues/2785) | 2 | – | When `separate_messages=false`, only first tool call message appears in notification center. |

**Analysis:** The #28 LM Studio request reflects a desire for easier local model setups, especially for Android users. Issue #1042 continues to frustrate users because a security guard is too aggressive, affecting many everyday commands. Both have been open for months.

## Bugs & Stability

### High Severity (Functional Regression / Data Loss)
- **[#2878 – load_image not configurable in config.json](https://github.com/sipeed/picoclaw/issues/2878)**  
  Created 2026-05-15. Tool registration in `agent_init.go` checks `IsToolEnabled("load_image")` but no dedicated branch exists, so it’s always enabled. **Fix PR #2879 already submitted.**

- **[#2817 – Voice transcription not passed to LLM](https://github.com/sipeed/picoclaw/issues/2817)**  
  Groq Whisper completes but LLM receives `[voice]` instead of transcribed text. No fix PR yet.

- **[#2816 – Matrix sender identity not injected](https://github.com/sipeed/picoclaw/issues/2816)**  
  Agent receives no sender info on Matrix channel (unlike Telegram `chat_id`). No fix PR.

- **[#2815 – `allow_from` filter broken on Matrix](https://github.com/sipeed/picoclaw/issues/2815)**  
  Any non-empty value blocks all messages; only `[]` works. **Fix PR #2827 open** (skips canonical ID parsing for `@`-prefixed entries).

### Medium Severity
- **[#2744 – Android v0.2.8 cannot access data from tabs](https://github.com/sipeed/picoclaw/issues/2744)**  
  Since May 1, no response. Likely a UI/permission issue on Termux.

- **[#2820 – Destructive `/clear` deletes Seahorse history](https://github.com/sipeed/picoclaw/issues/2820)**  
  Feature request for non-destructive session reset. No fix PR.

## Feature Requests & Roadmap Signals

| Request | Likelihood for Next Release |
|---------|---------------------------|
| **LM Studio Easy Connect** (#28) | Low – no maintainer activity, but high community interest. |
| **Non-destructive session reset** (#2820) | Medium – requested with clear use case and upvoted. |
| **Tirith pre-exec scanning** (PR #2877) | High – actively under review; could land in v0.2.9. |
| **Exec tool guard improvements** (#1042) | High – fix PR #2814 is open (allows relative script paths). |
| **Matrix identity injection** (#2816) | High – needed for parity with Telegram; no fix yet. |
| **MCP test connection API** (PR #2833) | High – part 3 of 3, depends on two other PRs; likely included. |

## User Feedback Summary

**Pain Points:**
- LM Studio connectivity is a major barrier for local model users on Android.
- The `exec` tool’s safety guard blocks harmless commands (curl, scripts) – reported multiple times.
- Voice transcription fails silently after successful recognition (#2817).
- Matrix channel lacks basic sender identity and allow-list filtering (#2815, #2816).
- Android v0.2.8 has a data tab access issue (#2744).
- Configuration regression: `load_image` cannot be disabled (#2878).

**Satisfaction Indicators:**
- Active contributor engagement with 13 open PRs and 7 merged in 24h.
- Windows security enhancement PR (#2836) and Docker improvements (#2239) show cross-platform interest.

## Backlog Watch
These items have been open for an extended period without maintainer resolution:

| Issue / PR | Opened | Comments | Stale | Needs Attention |
|------------|--------|----------|-------|-----------------|
| [#28 – LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28) | 2026-02-11 | 19 | Yes | Maintainer decision: implement or close with guidance. |
| [#1042 – Exec guard command path](https://github.com/sipeed/picoclaw/issues/1042) | 2026-03-04 | 11 | Yes | Fix PR #2814 open; needs review. |
| [#2744 – Android tab access](https://github.com/sipeed/picoclaw/issues/2744) | 2026-05-01 | 2 | Yes | No response from maintainers; likely platform-specific. |
| [#2785 – Feishu notification issue](https://github.com/sipeed/picoclaw/issues/2785) | 2026-05-06 | 2 | Yes | Requires channel logic investigation. |
| [#2662 – PR: Unify vendors table](https://github.com/sipeed/picoclaw/pull/2662) | 2026-04-24 | – | Yes | Documentation improvement; pending review. |
| [#2239 – PR: Docker compose privileged](https://github.com/sipeed/picoclaw/pull/2239) | 2026-04-01 | – | Yes | Simple change; needs maintainer approval. |

*All dates reflect creation dates; “stale” indicated in GitHub data.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest – 2026-05-16

## 1. Today's Overview
NanoClaw saw exceptionally high activity in the past 24 hours, with 50 issues and 50 pull requests updated. Of those, **44 issues were closed** and **39 PRs were merged/closed**, indicating strong maintenance momentum. A **new release (v2.0.63)** was published—the first properly cut GitHub Release for the project. Open/active work includes **6 issues** and **11 open PRs**, many of which are fixes for stability, security, and multi‑provider support. Overall, the project is in a healthy, fast‑paced development cycle.

## 2. Releases
- **v2.0.63** – First properly published release. Starting with this version, every `package.json` version bump that lands on `main` will eventually get a GitHub Release (cut manually by a maintainer). This resolves previous tag‑only releases and improves traceability. No breaking changes or migration notes are declared; it is a process‑level improvement.

## 3. Project Progress (Merged/Closed PRs Today)
Among the 39 merged/closed PRs, several notable advances landed:
- **Documentation & tooling:** #2502 (CHANGELOG entry and RELEASING.md), #2493 (per‑install slug for service names), #2489 (align Gmail/Calendar skill docs with v2 architecture).
- **Reliability fixes:** #954 (OpenRouter non‑Anthropic model routing fix), #956 (fast LLM credential sanity checks in setup), #967 (improve reliability for stuck sessions and runner turns—stop stream after first result, fix IPC polling), #2469 (better WhatsApp failure recovery messages).
- **Skills:** #514 (image recognition skill for WhatsApp), #519 (context compaction skill via Claude Agent SDK), #522 (Slack replies in threads instead of flattening to channel).

The volume of merged work shows the team is actively closing out bugs and shipping feature skills.

## 4. Community Hot Topics

| Item | Type | Comments | Reactions | Link |
|------|------|----------|-----------|------|
| #80 – Support runtimes/providers other than Claude/Anthropic | Enhancement | 32 | 60 👍 | [Issue #80](https://github.com/nanocoai/nanoclaw/issues/80) |
| #384 – Skill marketplace/registry | Enhancement | 9 | 16 👍 | [Issue #384](https://github.com/nanocoai/nanoclaw/issues/384) |
| #957 – Support Podman as Docker alternative | Enhancement | 8 | 6 👍 | [Issue #957](https://github.com/nanocoai/nanoclaw/issues/957) |
| #730 – OAuth token expires overnight (401 errors) | Bug | 6 | 0 | [Issue #730](https://github.com/nanocoai/nanoclaw/issues/730) |
| #29 – Add Signal messaging channel | Enhancement | 4 | 4 👍 | [Issue #29](https://github.com/nanocoai/nanoclaw/issues/29) |

**Underlying needs:**  
- #80 reflects growing unease with vendor lock‑in to Anthropic, especially after account suspensions reported for OpenClaw usage. Users want to swap providers (OpenRouter, Gemini, Codex) easily.  
- #384 shows demand for a curated, auditable skill ecosystem—NanoClaw’s core design of a small, user‑controlled attack surface is valued, and a registry could make skills more discoverable.  
- #957 indicates a portion of the userbase runs on systems where Docker is not feasible (e.g. rootless setups) and desires Podman support.  
- #730 is a critical operational pain point (service fails each morning) that two open PRs (#2505, #2508) are actively addressing.

## 5. Bugs & Stability

### Critical
- **#595 – OOM crash after ~40h due to ghost socket accumulation** on reconnect. Fixed by PR #967 (closed today) which improves runner reliability and ends streams after first result. Likely resolved.

### High
- **#730 – OAuth token expires overnight** (401 errors for systemd/launchd services). No fix in the closed list yet, but open PRs #2505 and #2508 propose a health monitor with auto‑refresh and sweeping token checks every 5 minutes.
- **#233 – IPC messages dropped when piped to active container after query result.** Closed today; fix included in #967.
- **#356 – ExitPlanMode tool fails** and leaves agent stuck. Closed today (likely fixed in the same reliability changes).
- **#341 – add-discord skill uses outdated Apple Container code** breaking Docker users. Closed today.
- **#635 – WhatsApp auth files created with 644 permissions** instead of 600, exposing credentials to other users. Closed today (permissions fix landed).

### Medium
- #413 (systemd fallback misdetection), #414 (stale docker group not remediated), #553 (container fails after WhatsApp recovery), #611 (agent‑runner source copy never updated), #184 (voice notes/documents not handled), #186 (no rate limiting). All closed today.

**Stability outlook:** The flurry of bug fixes—especially the OOM and IPC drop issues—should noticeably improve long‑running reliability. The OAuth token problem is being actively worked on with dedicated health‑monitor PRs.

## 6. Feature Requests & Roadmap Signals

| Request | Issue/PR | Likely inclusion |
|---------|----------|------------------|
| Multi‑provider support (OpenRouter, Gemini, etc.) | #80 (closed), #2490 (open PR for LiteLLM) | **High** – PR #2490 directly adds a LiteLLM operational skill |
| Skill marketplace/registry | #384 (closed) | Medium – design already accepted, implementation pending |
| Podman support | #957 (closed) | Medium – documentation PR likely, container runner change may follow |
| Groq Whisper as cloud backend | #2396 (open) | Low – opt‑in, but follows sovereignty model |
| Agent network / cross‑agent communication | #2497 (open PR) | Experimental – feature skill for advanced users |
| Health monitor with token status | #2505, #2508 (open PRs) | **Very high** – already being developed and tested |
| Early compact nudge skill | #2500 (open PR) | Medium – quality‑of‑life improvement |
| Message steering / quote‑reply | #617, #618 (closed) | Likely in next minor release |

The roadmap is clearly steering toward **provider diversity** (LiteLLM, OpenRouter fixes) and **operational resilience** (health monitor, token refresh). A **skill registry** remains a high‑interest but not yet implemented feature.

## 7. User Feedback Summary

**Positive signals:**
- Users appreciate NanoClaw’s **small, auditable core** (#384 praise).
- The project is considered “amazing” and “well designed” (#664, #957).
- Many contributors are actively submitting PRs—a sign of a healthy community.

**Pain points:**
- **Anthropic lock‑in / account bans** (#80) – users feel forced to find alternatives.
- **Installation difficulty** (#439) – install via Claude is novel but not for everyone; a simpler shell script is requested.
- **OAuth token refresh** (#730) – the most impactful operational problem, causing daily service disruption.
- **Docker dependency** (#957) – users on rootless systems or with security constraints would like Podman.
- **WhatsApp auth file permissions** (#635) – a security concern on multi‑user machines.

## 8. Backlog Watch

| Item | Last Update | Age (days) | Status |
|------|-------------|------------|--------|
| #2396 – Add Groq Whisper cloud backend | 2026-05-15 | 6 | Open, 1 comment – no maintainer response yet. Low complexity, but not prioritized. |
| #2501 – Channel auto‑binding on multi‑agent installs | 2026-05-15 (closed) | 1 | Filed by mistake, closed as noise. No action needed. |
| #2509 – Docs changelog alignment | 2026-05-16 | 0 | Open, minor. |
| #2500 – Early compact nudge skill | 2026-05-15 | 1 | Open PR, awaiting review. |

No critical, long‑unanswered issues remain in the top 30. The project team is highly responsive—most issues are addressed within hours or days. The only item that may need attention is #2396, but it is a feature request with low priority and no blockers.

---

**Project health summary:** NanoClaw is in a strong development phase with high community engagement, rapid bug fixing, and clear roadmap direction toward provider flexibility and operational stability. The first official release marks a maturation milestone.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-16

## 1. Today’s Overview
NullClaw experienced very low activity over the past 24 hours. Two new issues were opened, both with no comments or reactions, and no pull requests or releases were recorded. The project remains in a stable state with no signs of rapid development or urgent regressions. Community engagement is minimal, and maintainer attention is likely focused on the two newly reported items. Overall, the project is in a quiet phase, with no major changes to report.

## 2. Releases
No new releases were published today. The latest release remains unchanged.

---

## 3. Project Progress
No pull requests were updated, merged, or closed in the last 24 hours. No feature advances or fixes were committed.

---

## 4. Community Hot Topics
The two open issues received zero comments or reactions, indicating no active discussion. Both are in early stages:
- **Issue #916** – “Telegram: include reply_to_message text in inbound context” (created 2026-05-15, updated 2026-05-15) – proposes enhancing Telegram integration.
- **Issue #915** – “\[bug\] Problem with scheduler unauthorized” (created 2026-05-15, updated 2026-05-15) – reports a scheduler failure.

Because neither has attracted community discussion, there are no “hot topics” today. The underlying need from #916 is to improve context handling in group chats; #915 points to a potential authentication/permission issue with the scheduler.

---

## 5. Bugs & Stability
One bug was reported:
- **Issue #915** – Scheduler unauthorized – **Medium severity** (tool calling works but scheduler fails entirely). No associated fix PR exists yet. The issue mentions the scheduler does not function in both Telegram and CLI contexts, which could block automated workflows for users. No crashes or regressions were reported.

---

## 6. Feature Requests & Roadmap Signals
One feature request was opened:
- **Issue #916** – Request to include `reply_to_message` text in inbound Telegram context. This would improve conversational awareness when a user replies to an earlier message, especially in group chats. Given the low development velocity, this is unlikely to appear in the next version unless prioritized by maintainers.

No other feature signals were observed.

---

## 7. User Feedback Summary
Both open issues reflect real user pain points:
- **#915**: A user running NullClaw on Ubuntu with an external Ollama host reports that the scheduler is completely non-functional despite LLM and tool calling working. This suggests a configuration or permission issue that could frustrate users relying on scheduled tasks.
- **#916**: A user identifies missing Telegram API data that limits natural conversation flow. No satisfaction/dissatisfaction expressed beyond the initial reports.

Overall, feedback is sparse but points to integration gaps and stability concerns.

---

## 8. Backlog Watch
No long-unanswered issues or PRs are flagged in today’s data. The two new issues have been open less than 24 hours. No dormant items require immediate maintainer attention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest – 2026-05-16

**Generated from GitHub data (nearai/ironclaw):**  
- Issues updated in last 24h: 21 (all open)  
- PRs updated in last 24h: 50 (22 open, 28 merged/closed)  
- New releases: 0  

---

## 1. Today’s Overview

The IronClaw project is in an intense development sprint, with 50 PRs updated and 21 active issues in the last 24 hours. Activity is overwhelmingly focused on the **Reborn** architecture track—the planned replacement of the agent runtime and production workflow. The project merged 28 PRs today, including several large “workstream” (WS) branches that prove production-ready cutovers, ingress contracts, and cancellation safety. No new releases were published. The nightly E2E test remains broken (issue #3447), and a newly reported macOS prebuilt binary bug (#3701) may affect downstream users. Overall, the project is healthy but under heavy churn, with many open blockers that need maintainer triage.

---

## 2. Releases

No new versions were published today. The latest tagged release remains **ironclaw-v0.27.0** (Apr 29, 2026), but only **v0.24.0** is available on crates.io (see #3259). Downstream consumers are pinned to an older version due to wasmtime security CVEs.

---

## 3. Project Progress

Today saw 28 merged/closed PRs, with the following key advances:

- **Reborn product-live cutover proven (WS-17):** PR #3653 ([link](https://github.com/nearai/ironclaw/pull/3653)) merged, proving that the product inbound path can select a planned runtime and persist replies to thread history. This is the cornerstone for future Reborn routing.  
- **Live planned runtime composition wired (WS-16):** PR #3652 ([link](https://github.com/nearai/ironclaw/pull/3652)) merged, composing the planned driver, registry, resolver, coordinator, and host adapters into a production builder.  
- **Planned driver default path (WS-14):** PR #3651 ([link](https://github.com/nearai/ironclaw/pull/3651)) merged, adding registry/profile helpers for Reborn’s default path.  
- **Integration of six host-port branches (WS-14 parent):** PR #3650 ([link](https://github.com/nearai/ironclaw/pull/3650)) merged, combining capability, checkpoint, input, progress, cancellation, and identity-context support.  
- **Cancellation safety fixes:** PRs #3684, #3685, #3686 ([links](https://github.com/nearai/ironclaw/pull/3684), [#3685](https://github.com/nearai/ironclaw/pull/3685), [#3686](https://github.com/nearai/ironclaw/pull/3686)) merged, fixing cancellation from turn state and ack-aware boundary handling.  
- **Host-owned ingress contracts:** PR #3683 ([link](https://github.com/nearai/ironclaw/pull/3683)) added validated route descriptors and policy vocabulary for Reborn product/API surfaces.  
- **Composition root & binary:** PR #3695 ([link](https://github.com/nearai/ironclaw/pull/3695)) promoted `ironclaw_reborn_composition` to the official Reborn composition root and shipped a live binary.  
- **ProductAdapter manifest simplification:** PR #3688 ([link](https://github.com/nearai/ironclaw/pull/3688)) replaced the old separate TOML format with a projection from Extension Manifest v2.  
- **Universal file system dispatch:** PR #3679 ([link](https://github.com/nearai/ironclaw/pull/3679)) applied the `RootFilesystem` fabric across consumer crates (+15k LOC).  
- **Feature additions:**  
  - `DISABLE_TOOLS_LIST` flag (PR #3548, [link](https://github.com/nearai/ironclaw/pull/3548)) allows disabling specific tools at startup.  
  - Temperature plumbed through Responses API (PR #3641, [link](https://github.com/nearai/ironclaw/pull/3641)).  
  - `IRONCLAW_DISABLE_CODEACT` flag (PR #3665, [link](https://github.com/nearai/ironclaw/pull/3665)) disables engine v2 CodeAct.  
  - Thread/response ids exposed to tools (PR #3669, [link](https://github.com/nearai/ironclaw/pull/3669)).  
  - Markdown fix for Slack channel (PR #3532, [link](https://github.com/nearai/ironclaw/pull/3532)).  

---

## 4. Community Hot Topics

The most active discussions center on the Reborn cutover and production readiness.

- **#3616 – “Reborn: wire production app/gateway/channel ingress to product live workflow”** ([Issue](https://github.com/nearai/ironclaw/issues/3616)) — 4 comments. This is the master tracker for shifting from test-only to production ingress. It reflects the core tension between proving the loop and making it durable.  
- **#3259 – “Publish 0.25.0–0.27.0 to crates.io — downstream pinned to 0.24.0 by wasmtime 28.x CVEs”** ([Issue](https://github.com/nearai/ironclaw/issues/3259)) — 4 comments. High urgency: downstream consumers cannot use newer features.  
- **#3692 – “Reborn: add policy-gated personal identity and heartbeat prompt context”** ([Issue](https://github.com/nearai/ironclaw/issues/3692)) — 3 comments. Defers two identity/context surfaces that need additional prompt-context shape.  
- **#3698 – “Reborn: build test/dry-run product-live runtime harness”** ([Issue](https://github.com/nearai/ironclaw/issues/3698)) — 2 comments. First shippable slice toward #3616.  
- **#3620 / #3622** ([#3620](https://github.com/nearai/ironclaw/issues/3620), [#3622](https://github.com/nearai/ironclaw/issues/3622)) — each with 2 comments, discussing tool call integration into ParentLoopOutput and verification of tool-result completions.  

The underlying need is clear: the community (especially core contributors) is eager to see the Reborn architecture reach a production state, but many integration details remain unresolved.

---

## 5. Bugs & Stability

Two new or recurring bugs reported today:

- **#3701 – “v0.28.2 macOS prebuilt: gateway never binds despite config & doctor reporting it enabled”** ([Issue](https://github.com/nearai/ironclaw/issues/3701)) — *Severity: Medium (affects macOS users)*. No fix PR yet. Likely a build/portability issue.  
- **#3447 – “Nightly E2E failed”** ([Issue](https://github.com/nearai/ironclaw/issues/3447)) — *Severity: High (CI blocked)*. Open since May 10, updated today with another failure. No fix PR attached. The project’s automated test pipeline is unreliable.  

Two production-readiness issues remain open but are not new:  
- **#3026** ([Issue](https://github.com/nearai/ironclaw/issues/3026)) – config-driven composition root (blocker).  
- **#3602** ([Issue](https://github.com/nearai/ironclaw/issues/3602)) – production readiness gate not invoked at startup (risk high).  

No crash or regression reports beyond these.

---

## 6. Feature Requests & Roadmap Signals

Several user-facing features are being actively implemented or requested:

- **`DISABLE_TOOLS_LIST` flag** (#3548) – Allows administrators to disable specific tools at startup, improving security. Likely to be included in the next release.  
- **Per-channel MCP and built-in tool filtering** (#1378, [PR](https://github.com/nearai/ironclaw/pull/1378)) – Large PR still open; would enable Slack vs Telegram vs web tool scoping.  
- **External tools in Responses API** (#3122) – Support for caller-provided tools via `/v1/responses`. Already sees implementation activity.  
- **Temperature plumbed through Responses API** (#3641) – Already merged; will be in next release.  
- **Secrets & WASM sandbox documentation** (#3676) – New deep-dive docs for evaluators.  
- **Reborn WebUI Beta** – A set of four issues (#3611, #3625, #3626, #3627) targeting minimal native WebChat v2 routes, idempotency, turn scoping, and facade methods. These are P0 for the Reborn WebUI module and are likely to land soon.  

**Prediction for next release (v0.28.0+):** Expect inclusion of `DISABLE_TOOLS_LIST`, temperature support, Reborn composition root binary, and the first WebUI route set. The crates.io publish gap (#3259) must be resolved first.

---

## 7. User Feedback Summary

Direct user feedback is sparse, but the following pain points emerge from issue descriptions and PR comments:

- **Downstream consumers are stuck on v0.24.0** due to missing crates.io updates (#3259). This is the most concrete user-facing problem: users cannot use new features or security fixes.  
- **macOS users cannot start the gateway** with the official prebuilt binary (#3701).  
- **Production deployments lack validation** of Reborn readiness (#3602); no startup gate ensures the system is properly configured.  
- **Nightly E2E failures** (#3447) suggest the CI is flaky, which erodes confidence in test results.  

No positive user feedback or testimonials are present in the dataset.

---

## 8. Backlog Watch

Several important issues remain unanswered for an extended period:

| Issue | Created | Days Open | Priority | Notes |
|-------|---------|-----------|----------|-------|
| [#3447 – Nightly E2E failed](https://github.com/nearai/ironclaw/issues/3447) | May 10 | 6 | High | CI broken; no maintainer response. |
| [#3259 – Publish 0.25.0–0.27.0 to crates.io](https://github.com/nearai/ironclaw/issues/3259) | May 5 | 11 | High | Downstream blocked; no official response. |
| [#3026 – config-driven production composition root](https://github.com/nearai/ironclaw/issues/3026) | Apr 28 | 18 | High (P0 labeled) | Reborn blocker; no update in last 4 days. |
| [#3602 – Wire production readiness gate](https://github.com/nearai/ironclaw/issues/3602) | May 14 | 2 | High (risk: high) | New but urgent; no assignee. |
| [#3611 – WebUI Beta routes](https://github.com/nearai/ironclaw/issues/3611) | May 14 | 2 | P0 | Active but needs assignment. |
| [#1378 – Per-channel tool filtering](https://github.com/nearai/ironclaw/pull/1378) | Mar 18 | 59 | Medium | PR has not been updated in 1 day; awaiting maintainer review. |

The crates.io publishing bottleneck (#3259) and the nightly E2E failure (#3447) are the most critical items for community trust and usability. The Reborn composition root (#3026) is a declared blocker for the full Reborn cutover and should be prioritized.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **2026-05-16**, generated from the provided GitHub activity data.

---

## LobsterAI Project Digest: 2026-05-16

### 1. Today's Overview

Project activity remains **high**, with a significant surge in Pull Request (PR) updates (21 total), including 9 merges/closures. While there were no new releases, the project is in an active bug-fixing and feature-integration phase. A key user-reported issue (#1988) regarding model invocation after a recent update highlights a potential regression affecting core usability. The maintainer team appears highly responsive, merging several stale PRs and addressing long-standing bugs in areas like security, skills management, and session handling.

### 2. Releases

**None.** No new releases were recorded for this date.

### 3. Project Progress

Today saw the closure of 9 PRs, indicating significant progress across multiple domains:

- **Artifacts & UI:**
    - **Multi-tab preview (#1989):** Implemented a multi-tab preview mode for the right panel, allowing users to view multiple files (e.g., PPT, Word) simultaneously. Tab positioning was moved to the top bar.
    - **PPT preview optimization (#1990):** Added a left thumbnail bar for widescreen PPT previews, fixed a bug where adjusting panel width accidentally closed the preview, and improved tab transitions.
- **IM & Security:**
    - **Pairing code input (#1987):** Added a pairing code input field for Telegram, Discord, QQ, and POPO to facilitate approval requests, standardizing the experience with DingTalk/Feishu.
    - **Channel attribution (#1991):** Introduced a `keyfrom` channel attribution system for packaging and request context, improving user tracking and analytics.
    - **Security fix (#1992):** Fixed a bug where a default model option incorrectly persisted in the model list.
- **General Fixes:**
    - **Scheduled task filtering (#1191):** Fixed a critical bug where POPO and WeCom channels were not visible in the scheduled task notification picker, and corrected an erroneous "Not Supported" label for WeChat.
    - **Session sync bug (#1986):** Resolved a serious issue in `managed session` sync where characters (e.g., in file paths like `file:///` or extensions like `.pptx`) were being incorrectly truncated.
    - **Legacy cleanup (#1967):** Removed outdated URLs and documentation.

### 4. Community Hot Topics

The most active conversation revolves around a critical regression:

- **#1988 [OPEN] - Model Invocation Issue (Top Issue):** Users report that after a recent LobsterAI update, the `qwen3.6-plus` model **forcibly redirects** to NetEase's own endpoint, showing an "insufficient quota" error, especially when using the "Coding Plan." Users have attempted manual config changes but the system overrides them.
    - **Analysis:** This is a high-impact issue. It suggests an unintended hardcoding or default routing logic for specific models, likely breaking the workflow of many external API users (e.g., Alibaba Bailian).
    - **Link:** [Issue #1988](https://github.com/netease-youdao/LobsterAI/issues/1988)

Several older, "stale" PRs received attention today, indicating maintainer activity on long-standing problems:
- **#789 [OPEN] - Session Export Feature:** A long-awaited feature request for exporting Cowork sessions as Markdown/PDF.
- **#801 [OPEN] & #793 [OPEN] - Skills Toggle Bug:** The well-known bug where disabling a skill in settings does not prevent it from being invoked.
- **#798 [OPEN] - Alibaba Bailian 401 Auth:** A persistent authentication compatibility issue with DashScope/Volcengine Anthropic endpoints.

### 5. Bugs & Stability

**High Severity:**
- **Model Invocation Regression (#1988):** Users are forcibly routed to NetEase servers and blocked by quota errors. This is a **Critical** regression affecting core AI interaction, with no existing fix PR.
- **Session Sync Character Loss (#1986):** A **High** severity bug where characters in file paths/URLs were systematically removed during session sync. This was fixed today via PR #1986.

**Medium Severity (Fixed Today):**
- **Disabled Skills Remain Active (#801, #793):** A P0 bug where disabled skills could still be invoked. Fixed by ensuring the gateway service is restarted on config change.
- **Delete Session Resource Leak (#805):** Deleting a running session did not `abort` the background process, leading to wasted tokens. Fixed by adding a stop call before deletion.

**Medium Severity (Open/Stale):**
- **Alibaba Bailian 401 (#798):** A recurring compatibility issue for users of specific API providers.
- **Continue Session UI Bug (#799):** Re-sending a message in an ongoing conversation did not show the "stop" button, preventing user cancellation.

### 6. Feature Requests & Roadmap Signals

- **Session Export (#789):** The user demand for exporting conversations (Markdown/PDF) is strong and has been waiting since late March. It is a likely candidate for an upcoming minor release.
- **Multi-Tab Preview (#1989):** Just implemented, this feature addresses a common UX pain point for users working with multiple generated artifacts (documents, presentations, code).
- **Channel Attribution (#1991):** Indicates a focus on better user analytics and distribution channel tracking, suggesting enterprise/operational usage is being prioritized.
- **Model Compatibility:** The #1988 regression underscores a user desire for **flexible and transparent model routing**, not just a fixed set of default providers. Future releases may need to improve the model provider fallback logic.

### 7. User Feedback Summary

- **Pain Point (Bug Regression):** The primary dissatisfaction stems from the **model invocation issue (#1988)**. Users feel a lack of control, as their manual configuration is overridden. The phrase "无法使用coding plan" (cannot use the coding plan) indicates this breaks a key usage scenario.
- **Pain Point (IM Integration):** Users using Telegram, Discord, QQ, and POPO faced a broken onboarding flow due to the missing pairing code input (#1987), which was resolved today.
- **Satisfaction (UI/UX):** The improved multi-tab preview and PPT viewing experience (#1989, #1990) likely addresses user requests for a more desktop-native file management experience.

### 8. Backlog Watch

Several critical PRs and issues remain open and stale for over a month, requiring immediate maintainer attention:

- **#789 [OPEN] - Session Export Feature (Created: 2026-03-25):** A high-value feature request that has been stuck for over 7 weeks. It is a common expectation for productivity tools.
- **#790 [OPEN] - Security: Hardcoded Export Password (Created: 2026-03-25):** A security PR to remove a hardcoded password. Despite the high security implications, it remains unmerged.
- **#794 [OPEN] - Security: URL Scheme Allowlist (Created: 2026-03-25):** Another long-standing security hardening for `shell.openExternal()`, making the app more resistant to dangerous links.
- **#798 [OPEN] - Alibaba Bailian 401 Auth (Created: 2026-03-25):** A persistent regression for a major API provider (Alibaba) that users rely on.
- **#1967 [CLOSED] - Legacy URL/Code Cleanup:** Closed today, but its description notes it was "Wrongly pushed by ClaudeCode," which may warrant a quick review for unintended changes.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-05-16

## 1. Today’s Overview
Over the past 24 hours Moltis saw **high development velocity**: 8 pull requests were updated (7 merged/closed), and 4 issues were closed. All closed issues were accompanied by fix or implementation PRs, indicating a responsive maintainer team. The project is actively shipping new features—remote‑access gateways, an agent‑system builder skill, OAuth support for MCP, and improved TLS certificate generation—while addressing three reported bugs. Documentation migration to an Astro‑based site is also now complete. Overall, project health appears strong with a steady flow of contributions.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
All merged/closed PRs advanced either feature work or stability fixes:

- **Feature – Remote Access**  
  [#1002 (open)](https://github.com/moltis-org/moltis/pull/1002) – Adds NetBird private mesh support and Cloudflare Tunnel integration (config, CLI, REST routes). Still open for review.  
  [#1000 (merged)](https://github.com/moltis-org/moltis/pull/1000) – Enables `tls.public_ip` so auto‑generated TLS certificates include a public IP as a Subject Alternative Name.

- **Feature – Agent Systems**  
  [#1003 (merged)](https://github.com/moltis-org/moltis/pull/1003) – Bundles a `build-agent-systems` skill for designing multi‑user, multi‑channel distributed agent systems, including templates and progressive‑disclosure references.

- **Feature – MCP OAuth**  
  [#1001 (merged)](https://github.com/moltis-org/moltis/pull/1001) – Adds optional `client_secret` support for MCP OAuth override config, with updated validation and docs.

- **Bug Fixes**  
  [#998 (merged)](https://github.com/moltis-org/moltis/pull/998) – Fixes chat horizontal overflow (closes #994).  
  [#997 (merged)](https://github.com/moltis-org/moltis/pull/997) – Makes optional Proxmox CA certificate failures non‑fatal (closes #993).  
  [#1000 (merged)](https://github.com/moltis-org/moltis/pull/1000) – Also addresses the TLS localhost‑only issue (closes #996).

- **Infrastructure & Maintenance**  
  [#987 (merged)](https://github.com/moltis-org/moltis/pull/987) – Replaces the old mdBook documentation deployment with an Astro site featuring sidebar navigation, light/dark themes, and responsive design.  
  [#999 (merged)](https://github.com/moltis-org/moltis/pull/999) – Dependency bump for `astro` (5.18.1 → 6.3.3) in the docs directory.

## 4. Community Hot Topics
No issues or PRs accumulated more than one comment in the last 24 hours. The most notable piece of active community interest is:

- **[#995 – Feature: Integration of `portal-tunnel` as a trustless relay channel](https://github.com/moltis-org/moltis/issues/995)** – This enhancement request was **closed** with no public PR yet. It signals user interest in trustless relaying, likely related to remote access or peer‑to‑peer connectivity. The project’s concurrent work on NetBird/Cloudflare (PR #1002) may partly address this need.

## 5. Bugs & Stability
All three reported bugs were fixed within 24 hours, demonstrating strong turnaround:

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| [#996](https://github.com/moltis-org/moltis/issues/996) | **High** – Generated TLS certificates limited to `localhost` contradicting documentation. Could block production use on public IPs. | [#1000](https://github.com/moltis-org/moltis/pull/1000) |
| [#994](https://github.com/moltis-org/moltis/issues/994) | **Medium** – Chat UI regressed to horizontal scroll on long prompt text. Degraded UX. | [#998](https://github.com/moltis-org/moltis/pull/998) |
| [#993](https://github.com/moltis-org/moltis/issues/993) | **Medium** – Proxmox LXC helper failed when CA certificate was missing, blocking installation. | [#997](https://github.com/moltis-org/moltis/pull/997) |

No new crashes or regressions were reported today.

## 6. Feature Requests & Roadmap Signals
Two user‑requested features were recently closed without implementation:

- **[#995 (portal‑tunnel integration)](https://github.com/moltis-org/moltis/issues/995)** – Closed. Likely superseded or deferred in favour of NetBird/Cloudflare support (PR #1002). Given the overlap, the remote‑access feature being reviewed now may satisfy the underlying need for trustless relay channels.

Actively developed features that suggest next‑version content:
- **NetBird & Cloudflare Tunnel** (PR #1002) – Could form the foundation of the next minor release’s remote‑access capabilities.
- **Agent system builder skill** (PR #1003) – Adds authoring templates and documentation, likely part of the upcoming feature set.
- **Public IP TLS** (PR #1000) and **MCP OAuth client secrets** (PR #1001) – Both are backwards‑compatible enhancements with clear use cases for production deployments.

## 7. User Feedback Summary
Direct user feedback is limited to the three bug reports. However, the quick resolution of all three (within 24 hours) reflects a responsive development process that values stability. The closed feature request #995 suggests users are exploring trustless relay channels, which aligns with the project’s increasing focus on remote‑access features. No expressions of dissatisfaction were recorded.

## 8. Backlog Watch
No old, unanswered, or stalled issues or PRs were observed in the last 24 hours. The only currently open PR is:

- **[#1002 (NetBird and Cloudflare Tunnel support)](https://github.com/moltis-org/moltis/pull/1002)** – Opened 2026-05-15, still open for review. This is a large integration (config, CLI, REST, runtime controllers) that will benefit from timely maintainer attention and community testing.

No long‑unanswered issues are present in the dataset.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-05-16

## 1. Today's Overview

CoPaw (QwenPaw) shows **high development activity** with 34 PRs updated in the last 24 hours and 19 of them merged/closed. On the issue side, 17 items were updated, mostly open bugs and feature requests. No new release cuts this cycle (current stable: v1.1.7). The community is actively contributing: first-time contributors are addressing core bugs (e.g., zombie session, MCP tool name collisions), while the maintainer team is shipping security hardening and provider configurability. The project appears healthy but faces a growing backlog of usability and stability concerns that need prioritisation.

## 2. Releases

No new releases in the last 24 hours. Latest available version remains **v1.1.7** (desktop app).

## 3. Project Progress

**19 PRs were merged/closed** today (16 May). Notable advances:

- **Security hardening**: Two backup-related PRs merged — `Fix(backup): backup import restore trust controls` (#4409) and `Fix(backup): backup restore trust follow-up` (#4429) by jinglinpeng, adding HMAC signing and authentication to backup endpoints.
- **Provider flexibility**: `feat(providers): allow custom base URL for Anthropic provider` (#4387) by ekzhu unblocks self-hosted Anthropic-compatible endpoints.
- **Custom HTTP headers & Anthropic auth**: `feat(models): add custom headers editor and Anthropic auth token support` (#4413) by rayrayraykk — addresses community demand for provider header configuration.
- **Cron & session management**: `fix(cron): implement soft delete to prevent zombie session resurrection` (#4223) targets the long-standing zombie session issue (#4162) but remains open; separate PR `feat(cron): add timeout when creating cron job` (#4425) and `fix(WeCom): suppress duplicate "Thinking…" placeholder` (#4427) also closed.
- **Frontend polish**: `feat(console): implement localStorage for pinned state in chat session drawer` (#4416) by zhijianma.
- **Matrix channel enhancement**: `feat(console): enhance Matrix E2EE verify step` (#4120) by Morxi (merged).
- **Plugin fixes**: `fix(plugin): resolve CloudPaw plugin issues and enhance Alibaba Cloud Skills remote hosting integration` (#4423) by xuanrui-L.

**Still open but actively reviewed** are PRs adding new built-in skills (#4282, #4407), shell env injection (#4331), and token usage tracking (#4433).

## 4. Community Hot Topics

| Issue/PR | Comments | Topic | Link |
|----------|----------|-------|------|
| #4051 | 7 (closed) | DeepSeek `think` content parsing failure | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4051) |
| #4299 | 7 (open) | `write_file()` infinite loop error when output is long | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4299) |
| #4421 | 4 (closed) | Security: channel config written in plaintext to agent-readable directory | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4421) |
| #4162 | 3 (open) | Zombie session: cron tasks reuse deleted session context | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4162) |
| #3109 | 3 (closed) | DingTalk group chat cannot read quoted messages | [Issue](https://github.com/agentscope-ai/QwenPaw/issues/3109) |

**Underlying needs**: Users are hitting core agent reliability issues — LLM response parsing (DeepSeek thinking tags), skill tool parameter errors (`write_file` missing content), and session/cron lifecycle bugs. The **zombie session** problem (#4162) has spawned at least two PRs (#4223, #4434) indicating high community demand for a clean fix. The security report (#4421) was quickly closed, suggesting maintainer responsiveness.

## 5. Bugs & Stability

**High severity** (active, affecting production use):
1. **`write_file()` infinite loop** (#4299) — triggers `missing positional argument: 'content'` when output is long; affects any skill that writes files. **No known fix PR in queue** — should be prioritised.
2. **Zombie session resurrection** (#4162) — cron tasks keep old session context even after session deletion and restart. PR #4223 implements soft delete, PR #4434 adds "clear before run" toggles. Both are open and need review.
3. **macOS 15 icon size anomaly** (#4412) — dock and launchpad icons appear distorted. Low impact but visible in desktop app.

**Medium severity** (closed or mitigated):
4. **Plaintext channel config leak** (#4421) — limited exposure window, quickly reported and closed.
5. **DeepSeek think tag parsing** (#4051) — closed, likely with a fix or workaround.

**Under review PRs targeting bugs**:
- `fix(shell): inject request context into subprocess env` (#4331) — fixes missing attribution in shell executions.
- `fix(security): guard shell file access bypasses` (#4361) — prevents file guard bypass via shell commands.
- `fix(cron): isolate non-shared runs` (#4303) — additional zombie session fix.

Overall, **the project has 12 open bugs** in the 24h window. The `write_file()` and zombie session issues are the most impactful.

## 6. Feature Requests & Roadmap Signals

**Top user-requested features** (by recency and community engagement):
- **One-click OpenCode/OpenAI compatible config** (#4441) — "one-click configure opencode go" suggests demand for simplified model setup.
- **External memory integration via plugin** (#4439) — ask for integrating Hindsight or similar memory systems.
- **Delete single/partial chat turns** (#4437) — precise message removal without clearing full session.
- **Conversation turn count display** (#4435) — help users manage context length/API costs.
- **Split conversation to new session** (#4436) — extract part of history to avoid long context.
- **Parallel processing for DingTalk group chats** (#4431) — different users should not block each other.

**Likely to appear in next version**:
- Custom HTTP headers and Anthropic auth (just merged in #4413) → v1.1.8.
- MCP tool name collision fix (#4428) — critical for multi-MCP setups.
- Cron "clear before run" toggle (#4432, #4434) — directly addresses zombie session workaround.
- Built-in plugins listing (#4406) — parity with skills UX.

The roadmap signals strong community interest in **session lifecycle management** (split, delete, clear, display context length) and **memory integration**, indicating a shift toward more deterministic agent orchestration.

## 7. User Feedback Summary

**Satisfaction**:
- Security vulnerability #4421 was acknowledged and fixed rapidly — users appreciate responsiveness.
- DeepSeek think tag parsing (#4051) seems resolved; no follow-up complaints.
- First-time contributors are warmly welcomed (PRs #4407, #4428, #4120 marked as `first-time-contributor`).

**Dissatisfaction / friction points**:
- **`write_file()` crashes** (#4299) frustrates users who rely on file output for long documents — still unaddressed.
- **Session/cron confusion** (#4162) — users expect deleting a session to fully reset bound cron tasks; current behaviour feels like a bug.
- **Upgrade fear** (#4430) — user asks whether v1.1.6 → 1.1.7 upgrade preserves settings; existing documentation advises uninstall/reinstall, which causes concern about data loss.
- **Serial processing in DingTalk** (#4431) — one long task blocks all other users, impacting team collaboration.

**Common patterns**: Most user reports stem from **edge cases in LLM output handling** (think tags, long file writes), **session identity persistence** (zombie sessions), and **channel-specific quirks** (DingTalk quoting, Matrix E2EE).

## 8. Backlog Watch

**Issues needing maintainer attention** (open, dated ≥ 7 days):
- **#4299** (bug: `write_file()` infinite loop) — opened 2026-05-14, 7 comments, no PR assigned. High impact; should be prioritised.
- **#4162** (zombie session) — opened 2026-05-09, multiple PRs exist but none merged yet. Needs review and decision.
- **#4195** (not shown in 24h window, but likely older) — would need full scan. From visible data, #3796 (custom headers, closed now) and #3109 (closed) had longer tail but are resolved.

**Open PRs that are long-lived**:
- **#4223** (zombie session fix) — opened 2026-05-11, still open after 5 days. This is the primary fix candidate.
- **#4282** (`/make-skill` command) — opened 2026-05-13, significant feature but under review.

**Recommendation**: The maintainer team should prioritise reviewing and merging the zombie session PRs (#4223, #4303, #4434) and addressing the `write_file()` bug (#4299) to improve core reliability before building more features. The growing number of session management feature requests (#4435, #4436, #4437, #4441) signals a strong community need that could be addressed with a cohesive session management enhancement in the next minor release.

---

*Generated from GitHub data snapshot 2026-05-16 (24h update window including 2026-05-15 to 2026-05-16).*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-16

## 1. Today's Overview

ZeroClaw saw **high activity** over the past 24 hours, with 21 issues updated (14 open, 7 closed) and 50 pull requests updated (45 open, 5 merged/closed). No new releases were published. The project is in a **rapid development and stabilization phase**: a major v0.8.0 multi-agent runtime PR (#6398) continues to accumulate incremental reviews, while several critical bugs (Anthropic tool naming, Docker bind mount shadowing, MCP filter bugs) were reported and are being actively addressed. Community contributions remain strong, with multiple documentation improvements, a new “dream mode” memory consolidation feature, and fixes for Slack token handling and Nextcloud Talk integration.

## 2. Releases

No new releases were published in the last 24 hours. The next expected milestone is **v0.8.0** (see PR #6398), which introduces a multi-agent runtime and Schema V3. Users should watch for release notes once that PR is finalized.

## 3. Project Progress

Five PRs were merged or closed today (out of 50 total PRs updated). Key closures include:

- **#6396** (closed) – *feat(ci): force check pr title* – Enforces the project’s PR title convention (`type(scope): description`) via a new GitHub Action workflow.
- **#6287** (closed) – *fix(config/channels/slack): make bot_token optional and load from env at startup* – Resolves long-standing issue #6237 where Slack bot tokens were required in the config file instead of environment variables.
- **#6236** (closed) – *fix(security): allow safe device redirect targets in path policy* – Fixes the `forbidden_path_argument` scanner to permit legitimate shell redirects like `> /dev/null`.
- **#6525** (closed) – *fix(matrix): avoid threading root timeline messages* – Prevents Matrix root messages from automatically opening threads, keeping the experience consistent.

Additionally, several open PRs received significant updates including:
- **#6398** – v0.8.0 multi-agent runtime (still open, incremental review underway)
- **#6693** – New “dream mode” memory consolidation subsystem (opened today)
- **#6675** – Strict tool parsing mode for providers (opened 2026-05-15)
- **#6553** – Restore broken SSE /logs stream for observability (updated today)

## 4. Community Hot Topics

The most active discussions in the last 24 hours center on security, CI enforcement, and feature requests with high community engagement:

| Issue / PR | Comments | Summary |
|------------|----------|---------|
| [#5833 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/5833) | 4 | *feat(tools): session ownership model for destructive operations* – Long-running enhancement to scope session keys per agent, now closed. High interest from the community. |
| [#6394 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/6394) | 3 | *GitHub action that checks for PR’s title* – Led to merged PR #6396. Community desire for automated governance. |
| [#5518 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/5518) | 3 | *forbidden_path_argument blocks safe redirect targets* – Critical bug affecting shell tool usage, now resolved with PR #6236. |
| [#6679 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/6679) | 2 | *require fresh PR checks before merging stale branches* – CI reliability concern raised by a frequent contributor. |
| [#5533 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/5533) | 2 | *allowed_Path doesn't respect contains logic* – Configuration parsing bug fixed earlier, but still resonating with users. |

**Underlying need**: The community is pushing for **stronger security and CI discipline** – automated title checks, session ownership, and path policy correctness are repeatedly raised. Contributors expect predictable, auditable behavior from ZeroClaw’s tooling and runtime.

## 5. Bugs & Stability

Several bugs were reported or updated today, with severity ranging from S0 (security/data loss) to S2 (degraded behavior). No S0 issues were opened today, but high-severity open bugs remain:

| Issue | Severity | Component | Status | Fix PR? |
|-------|----------|-----------|--------|---------|
| [#6678](https://github.com/zeroclaw-labs/zeroclaw/issues/6678) – Skill tool names violate Anthropic API regex | S1 – workflow blocked | runtime/skills | OPEN | No PR yet |
| [#6681](https://github.com/zeroclaw-labs/zeroclaw/issues/6681) – `zeroclaw skills install clawhub:*` panics | S1 – workflow blocked | runtime/daemon | OPEN | No PR yet |
| [#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) – `tool_filter_groups` no-op for real MCP tools | S2 – degraded behavior | agent/config | OPEN | No PR yet |
| [#6698](https://github.com/zeroclaw-labs/zeroclaw/issues/6698) – Fluent locale files lag English sources | S2 – degraded behavior | runtime/daemon | OPEN | No PR yet |
| [#6697](https://github.com/zeroclaw-labs/zeroclaw/issues/6697) – `cargo mdbook sync` produces unstable gettext diffs | S2 – degraded behavior | docs | OPEN | #6696 (fixes docs policy) |
| [#6694](https://github.com/zeroclaw-labs/zeroclaw/issues/6694) – `cargo mdbook sync` creates churn for tiny edits | S2 – degraded behavior | docs | OPEN | See #6696 |
| [#6691](https://github.com/zeroclaw-labs/zeroclaw/issues/6691) – Stale RUST_LOG target filters in docs | S2 – degraded behavior | docs | OPEN | #6692 (fix PR open) |
| [#6689](https://github.com/zeroclaw-labs/zeroclaw/issues/6689) – Production SOP audit silently no-op | S0 – data loss? | runtime/sop | OPEN | No PR yet |
| [#6687](https://github.com/zeroclaw-labs/zeroclaw/issues/6687) – Two independent SopEngine instances | S1 – workflow blocked | runtime/sop | OPEN | No PR yet |
| [#6686](https://github.com/zeroclaw-labs/zeroclaw/issues/6686) – SOP cron triggers have no production caller | S2 – degraded behavior | runtime/sop | OPEN | No PR yet |
| [#6685](https://github.com/zeroclaw-labs/zeroclaw/issues/6685) – SOP HTTP fan-in not wired | S2 – degraded behavior | runtime/sop | OPEN | No PR yet |
| [#6683](https://github.com/zeroclaw-labs/zeroclaw/issues/6683) – `skill_manage` patch ignores cooldown | S2 – degraded behavior | runtime/skills | OPEN | No PR yet |

**Notable**: The SOP (Standard Operating Procedures) subsystem has multiple bugs (4 open issues from @JordanTheJet) indicating that this new feature is not yet production-ready. The Anthropic API naming bug (#6678) and the installation panic (#6681) block basic skill workflows. Urgent attention needed.

## 6. Feature Requests & Roadmap Signals

New feature requests opened today:

- **[#6695](https://github.com/zeroclaw-labs/zeroclaw/issues/6695)** – *Add skills management to the gateway web UI* – Community member @NiuBlibing requests a dashboard UI for listing, enabling/disabling, and editing skills. Likely to be prioritized given skills are a first-class concept.
- **[#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)** – *Track: zeroclaw skills support and UX (v0.7.6)* – Already accepted tracker for a past release theme, still active.
- **[#6693](https://github.com/zeroclaw-labs/zeroclaw/pull/6693)** – *feat(memory): add dream mode for periodic memory consolidation* – Opened today as a large PR by @JordanTheJet. Introduces a 5-phase “dream mode” subsystem. Signals a move toward long-term memory and context optimization.
- **[#6318](https://github.com/zeroclaw-labs/zeroclaw/pull/6318)** – *feat(hooks): add on_before_compaction hook* – Pre-compression notification for agents, still awaiting author action.

**Prediction for next release (v0.8.0)**: The massive PR #6398 will likely land first, bringing multi-agent orchestration and Schema V3. Feature requests like skills UI (#6695) and dream mode (#6693) may follow as v0.8.1 or v0.9.0 targets.

## 7. User Feedback Summary

Real user pain points surfaced in today’s issues:

- **Skill installation broken** – `zeroclaw skills install` panics on `clawhub:*` sources (#6681). A show-stopper for anyone trying out community skills.
- **Anthropic API incompatibility** – Skill tool names with dots (`format!("{}.{}", ...)`) violate Anthropic’s name regex, blocking all requests (#6678). Users cannot use custom shell/script tools with Anthropic providers.
- **Docker bind mount shadows web UI** – Pre-built dashboard is hidden when using persistent volumes (#6400, closed). Users relying on Docker need a workaround.
- **Slack token configuration friction** – Resolved by PR #6287, but the original issue (#6237) shows strong dissatisfaction with forced config-file storage over environment variables.
- **Path policy surprises** – Both `allowed_path` contains logic (#5533) and `forbidden_path_argument` blocking `/dev/null` (#5518) have been fixed, but the experience highlighted that path policy is unintuitive for new users.

Overall sentiment: **Active and engaged community** but some **critical regressions in skill/tool functionality** are causing frustration. The rapid pace of fixes (e.g., Slack token, path policy) indicates maintainers are responsive.

## 8. Backlog Watch

The following issues and PRs are **stale or awaiting maintainer action**:

| Item | Created | Last Update | Status | Notes |
|------|---------|-------------|--------|-------|
| [#6318](https://github.com/zeroclaw-labs/zeroclaw/pull/6318) – `feat(hooks): add on_before_compaction hook` | 2026-05-03 | 2026-05-16 | **Needs author action** | Risk: high, needs maintainer sign-off. |
| [#5987](https://github.com/zeroclaw-labs/zeroclaw/pull/5987) – `feat: nix package` | 2026-04-22 | 2026-05-16 | **Needs author action** | Large Nix build refactor, risk: high. |
| [#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253) – *Track: zeroclaw skills support and UX* | 2026-05-01 | 2026-05-16 | Accepted, no PR yet | Community tracker; no implementation assigned. |
| [#6685](https://github.com/zeroclaw-labs/zeroclaw/issues/6685) – *SOP HTTP fan-in not wired* | 2026-05-15 | 2026-05-15 | Open, no comments | SOP subsystem lack may need design review. |
| [#6689](https://github.com/zeroclaw-labs/zeroclaw/issues/6689) – *SOP audit silently no-op* | 2026-05-15 | 2026-05-15 | Open, no comments | Data loss risk – critical for production SOP users. |

**Call to action**: Maintainers should prioritize review of the two stalled PRs (#6318, #5987) and assign a response to the SOP audit bug (#6689), which is flagged as a potential data loss issue.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*