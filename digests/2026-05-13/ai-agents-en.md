# OpenClaw Ecosystem Digest 2026-05-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-05-13 10:00 UTC

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

# OpenClaw Project Digest — 2026-05-13

## 1. Today's Overview
Project activity remains extremely high, with **500 issues and 500 pull requests updated** in the last 24 hours. The maintainers pushed **four beta releases** (v2026.5.12‑beta.1–4) focused on fixing regressions in the Codex runtime, auth‑profile‑backed media tools, WhatsApp install compatibility, and memory‑wiki permission scopes. Despite rapid iteration, the community is experiencing a spike in regression reports—particularly around gateway performance, agent response drops, and UI rendering on Windows. A total of **285 issues were closed** and **45 PRs were merged/closed**, indicating active triage and patch work. However, the large number of open issues (215 open/active) and open PRs (455) suggests the project is stretched by the volume of incoming reports.

## 2. Releases
**Four beta releases** were published today: v2026.5.12‑beta.1 through beta.4. All are iterative fixes on the 2026.5 branch.

- **v2026.5.12‑beta.4**:  
  – Codex runtime: allows the official installed `@openclaw/codex` package to use its private task‑runtime SDK helper, fixing `MODULE_NOT_FOUND` errors during migrated OpenAI/Codex beta runs.  
  – Codex migration: makes Enter activate the highlighted checkbox row before continuing, so “skip for now” actions are no longer missed.

- **v2026.5.12‑beta.3** (and beta.2, which had identical patch notes):  
  – Codex harness: keeps auth‑profile‑backed media tools (`image_generate`, etc.) available when OpenAI auth lives in the agent’s auth‑profile store instead of environment variables.  
  – WhatsApp/install: allows Baileys’ pinned libsignal git subdependency under pnpm 11, unblocking source installs.

- **v2026.5.12‑beta.1**:  
  – `fix(memory‑wiki)`: require admin scope for ingest and write scope for Obsidian search (thanks @pgondhi987).  
  – Build: skip copied metadata for bundled plugins that are excluded from build entries, preventing update/status confusion.

These releases are all beta‑quality; no breaking changes or migration steps were documented.

## 3. Project Progress
The following notable pull requests were **closed/merged** today (some may have been merged earlier but recorded as updated today):

- **#81361** – [fix(plugins): raise default install scan file limit to 25k](https://github.com/openclaw/openclaw/pull/81361): resolves a Codex plugin install failure (fans out to ~18k files) that blocked `openclaw onboard`.
- **#81291** – [feat(webchat): add streaming autoscroll toggle](https://github.com/openclaw/openclaw/pull/81291): fixes #81287 by adding a persisted toggle for automatic scrolling during streaming.
- **#81363** – [Revert “Check ClawHub trust before plugin installs”](https://github.com/openclaw/openclaw/pull/81363): the original PR #81307 was reverted because an automation bot went “rogue”; the feature may be reconsidered.
- **#53030** – [i18n(ja‑JP): expand glossary and add multi‑lang glossary check](https://github.com/openclaw/openclaw/pull/53030): Japanese glossary grew from 13→75 entries; automated checks were added for consistency.
- Numerous bug fix issues were also closed (see section 5).

Key **open** PRs that moved forward today include:
- **#81333** – [feat(i18n): translate Nodes page UI strings to Simplified Chinese](https://github.com/openclaw/openclaw/pull/81333) (XL size, proof supplied).
- **#70864** – [feat: add scoped mention pattern policy](https://github.com/openclaw/openclaw/pull/70864) (XL, proof supplied).
- **#76601** – [fix(config): serialize concurrent config mutations](https://github.com/openclaw/openclaw/pull/76601) (XL, proof supplied).
- **#78583** – [Add World ID AgentKit HITL approvals](https://github.com/openclaw/openclaw/pull/78583) (XL, proof supplied).

Overall, the project is shipping fixes rapidly but many fresh features remain in review.

## 4. Community Hot Topics
The most discussed issues and PRs (by comment count and reactions) highlight deep user frustrations:

1. **#65867** – [Bug: Gemini `<final>` tags leak into delivered messages](https://github.com/openclaw/openclaw/issues/65867) (18 comments, 0 👍)  
   *Regression*: reappearance of old bug #48587. Users see unformatted `<final>` tags in web UI output. No fix PR yet.

2. **#73323** – [Gateway runtime degradation: pricing fetch 60s timeouts, Telegram polling stalls, slow RPC](https://github.com/openclaw/openclaw/issues/73323) (17 comments, 1 👍)  
   *Chronic*: reproduced across multiple versions (4.23–4.26) on Windows 11 + Node 24. Users report multi‑subsystem network/timer degradation.

3. **#76877** – [2026.5.2 Agents stop responding mid work](https://github.com/openclaw/openclaw/issues/76877) (14 comments, 4 👍)  
   *High reaction*: after tool use, agents go silent until manually prompted for progress. Several users could not run any version newer than 2026.04‑23.

4. **#67035** – [Windows chat UI regression: input swallowed, streamed replies invisible](https://github.com/openclaw/openclaw/issues/67035) (13 comments, 0 👍)  
   *Sustained*: opened 2026‑04‑15, still unfixed. Typed input often does not appear; replies require a page refresh.

5. **#79902** – [Feature: Add companion-friendly SQLite transcript/session seams](https://github.com/openclaw/openclaw/issues/79902) (13 comments, 2 👍)  
   *Feature request*: users want a way to build on canonical runtime state without scraping opaque blobs.

These issues collectively signal that **release quality and regression testing** are top community concerns. The feature request for SQLite transcript seams (#79902) also indicates a desire for more transparent session data.

## 5. Bugs & Stability
| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#73323 – Gateway runtime degradation](https://github.com/openclaw/openclaw/issues/73323) | Multi‑subsystem timeouts on Windows, not yet fixed. | None open |
| **High** | [#76877 – Agents stop responding mid work](https://github.com/openclaw/openclaw/issues/76877) | Work‑stopper for v2026.5.2; users stuck. | Closed but regression persists in later versions? Needs revalidation. |
| **High** | [#67035 – Windows chat UI regression](https://github.com/openclaw/openclaw/issues/67035) | Input/reply rendering broken since 2026.4.14. | None open |
| **Medium** | [#81295 – Gateway deferred loading silently skips non‑bundled plugins](https://github.com/openclaw/openclaw/issues/81295) | Regression that blocks npm/workspace plugins. | Closed – fix merged in 24h. |
| **Medium** | [#80356 – EXTERNAL_UNTRUSTED_CONTENT wrappers leak into Discord](https://github.com/openclaw/openclaw/issues/80356) | Envelope markers visible in agent input and rendered messages. | Closed – fix likely in progress. |
| **Medium** | [#80669 – WhatsApp group auto‑reply silently suppressed](https://github.com/openclaw/openclaw/issues/80669) | Typing indicator sent but reply not delivered. | None open |
| **Low** | [#79856 – `config set` silently discards values matching schema defaults](https://github.com/openclaw/openclaw/issues/79856) | Data loss without error. | Closed – fix merged. |

Several regressions have been closed with fixes today – notably #81295 (deferred loading), #80356 (Discord envelope leak), and #79856 (config data loss). However, the most severe long‑standing bugs (#73323, #67035) remain open and continue to affect many users.

## 6. Feature Requests & Roadmap Signals
The following feature requests and in‑progress PRs give strong signals for the next stable release:

- **Plugin UI Extension System** (#66944) – Allows plugins to contribute native tabs to Control UI. 3 👍, active discussion.
- **Per‑Agent TTS/STT Configuration** (#66252) – Multi‑language/voice per agent.
- **SQLite transcript/seam access** (#79902) – Advanced session introspection.
- **Graceful signal escalation for exec tool** (#66399) – Process supervisor improvements.
- **Task‑level timeout for lane queue** (#48488) – Prevents permanent session stalls.

On the PR side, the following are ready for review and likely candidates for the next minor release:
- **#81333** – i18n for Nodes page (Simplified Chinese)
- **#70864** – Scoped mention pattern policy (gateway & channels)
- **#78583** – World ID / AgentKit human‑in‑the‑loop approval
- **#80240** – AlpaCore bridge and ACA deploy flow
- **#81351/81356/81353/81354** – Telegram and plugin‑SDK enhancements (localized commands, web_app, tool exposure, type exports)

The project appears to be moving toward **better plugin extensibility, i18n, and new channel integrations**.

## 7. User Feedback Summary
**Common pain points expressed today:**
- “After upgrading, I get `<final>` tags in replies” (#65867) – frustration with recurring bugs.
- “Multiple versions (4.23–4.26) are unusably slow on Windows 11” (#73323) – stability concerns.
- “I could not run anything newer than 2026.04‑23” (#76877) – users are stuck on old versions.
- “Config changes silently discarded” (#79856) – trust erosion in configuration management.
- “Messages vanish in WhatsApp groups” (#80669) – delivery reliability.

**Positive feedback signals:**
- Quick closure of #81295 (deferred loading) and #80356 (Discord leak) shows responsive maintainers.
- Contributors are actively submitting PRs for i18n and new features, indicating a healthy contributor community.
- Users requesting SQLite seams (#79902) and plugin UI (#66944) are planning advanced use cases.

Overall, the sentiment is **mixed**: the project is innovating rapidly, but regressions are shaking user confidence, particularly on Windows and during long sessions.

## 8. Backlog Watch
The following important issues and PRs have been open for an extended period without resolution:

1. **#65867** – Gemini final tags (opened 2026‑04‑13, 18 comments) – no fix PR; beta release blocker not set.
2. **#73323** – Gateway runtime degradation (opened 2026‑04‑28, 17 comments) – no fix; high severity for Windows users.
3. **#67035** – Windows chat UI regression (opened 2026‑04‑15, 13 comments) – no fix; long‑standing.
4. **#67423** – Auth router ignores provider `apiKey` field (opened 2026‑04‑15, 5 comments) – forces wrong API key for split providers.
5. **#48488** – Lane queue lacks task‑level timeout (opened 2026‑03‑16) – can permanently block session lanes.
6. **#75219** – PR: opt‑in transient retries for provider execution (opened 2026‑04‑30, tagged `needs‑real‑behavior‑proof`) – stalled while maintainers request evidence.
7. **#77023** – PR: steer mid‑turn prompts by default (opened 2026‑05‑04, XL) – also waiting for proof.

These items represent **outstanding risks** to project stability and user experience. Maintainer focus on these high‑impact tickets would likely improve community sentiment.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent Open Source Ecosystem
**Analysis Date: 2026-05-13**

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is experiencing **unprecedented velocity**, with the core reference project (OpenClaw) processing over 500 issues daily, while downstream forks and derivatives mature their own specializations. The landscape is bifurcating into two camps: **comprehensive reference implementations** (OpenClaw, IronClaw) that prioritize feature breadth and architectural experimentation, and **lightweight or domain-adapted forks** (NanoBot, PicoClaw, NanoClaw, CoPaw) that optimize for specific user bases—Chinese language providers, embedded hardware, enterprise WeChat, or simplified deployment. A recurring tension across all projects is the struggle to maintain stability while shipping rapidly, with regression density becoming a primary community pain point. Notably, the ecosystem is converging on several shared challenges—session memory continuity, provider API compatibility, and multi-platform channel reliability—while diverging in architectural philosophy (Rust-native vs. TypeScript, monolithic vs. modular plugin architectures).

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score | Notes |
|---------|---------------------|-------------------|----------------|--------------|-------|
| **OpenClaw** | 500 (285 closed) | 500 (45 merged) | 4 beta releases today | 🟡 High activity, high regression risk | Largest absolute volume; regression density a concern |
| **NanoBot** | 15 (12 closed) | 23 (12 merged) | No new release | 🟢 Healthy sprint | Strong maintenance cadence, clearing backlog |
| **Hermes Agent** | 50 (4 closed) | 50 (6 merged) | No new release | 🟡 Very active, many open bugs | High issue-to-fix ratio; maintainers responsive |
| **PicoClaw** | 18 (7 closed) | 15 (2 merged) | Nightly build (unstable) | 🟡 Moderate, focused | Security bugs have fix PRs; streaming gap persists |
| **NanoClaw** | 2 (1 security) | 21 (8 merged) | No new release | 🟢 Productive | Lean team, high PR throughput, focused scope |
| **NullClaw** | 1 (new issue) | 1 (existing PR) | No new release | 🔴 Low activity | Single feature PR aging; minimal maintainer engagement |
| **IronClaw** | 21 (multiple closed) | 50 (11 merged) | No new release | 🟢 High velocity, architecture-focused | Reborn architecture advancing; downstream crate release blocked |
| **LobsterAI** | 1 open issue | 30 (28 merged) | v2026.5.12 (released yesterday) | 🟢 Very healthy | Aggressive backlog clearance; strong feature cadence |
| **TinyClaw** | 0 | 0 | No activity | 🔴 Dormant | No updates in 24h |
| **Moltis** | 1 (bug report) | 0 | No release | 🔴 Low activity | Single UI regression; no maintainer response |
| **CoPaw** | 24 (12 closed) | 35 (22 merged) | v1.1.7-beta.1 today | 🟢 Very healthy | Balanced issue/PR closure; security + MCP focus |
| **ZeptoClaw** | 2 closed (security) | 3 (1 merged) | No new release | 🟡 Maintenance phase | Dependency bumps + security audit closure only |
| **ZeroClaw** | 5 (all open) | 46 (13 merged) | No new release | 🟢 High velocity, pre-release | Targeting v0.8.0; rapid bug-fix PRs |

**Interpretation:** The ecosystem spans a wide activity spectrum. The top four projects (OpenClaw, IronClaw, CoPaw, ZeroClaw) operate at industrial scale. A second tier (LobsterAI, NanoClaw, Hermes Agent, NanoBot, PicoClaw) shows sustained but manageable throughput. Three projects (NullClaw, TinyClaw, Moltis) are essentially dormant or single-contributor efforts.

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Community scale:** 500 daily issues/PRs dwarfs all peers (next largest: IronClaw at 50). This creates a self-sustaining ecosystem of contributors, reviewers, and testers.
- **Release velocity:** Four beta releases in a single day demonstrates CI/CD maturity and a low-friction release pipeline unmatched by peers.
- **Plugin ecosystem:** The ClawHub trust system (despite recent revert) and plugin extension system (PR #66944) signal a platform play that forks cannot replicate.
- **Reference status:** As the upstream for NanoClaw, PicoClaw, and ZeroClaw, architectural decisions propagate downstream—creating influence beyond direct user count.

**Technical Approach Differences:**
- **Language stack:** TypeScript/Node.js reference vs. IronClaw's Rust-native and ZeptoClaw's mixed stack. This lowers the barrier for web developers but introduces runtime performance gaps.
- **Monolithic vs. modular:** OpenClaw ships as a full-featured platform; competitors like NanoClaw emphasize lightweight setups with optional dependencies (OneCLI debate in #2437).
- **Migration tolerance:** OpenClaw explicitly maintains Codex migration paths (beta.4); most forks lack backward-compatibility guarantees.

**Community Size Comparison:**
- OpenClaw's community engagement (reactions, multi-comment threads) is 5–10× any peer. The 18-comment thread on Gemini `<final>` tags (#65867) alone exceeds the total daily comments of NullClaw or Moltis.

**Risk:** OpenClaw's rapid iteration carries a quality tax. The 215 open issues and 455 open PRs suggest maintainers are stretched thin. Long-standing bugs (#73323, #67035) erode Windows user trust—a vulnerability that lighter-weight forks could exploit.

---

## 4. Shared Technical Focus Areas

The following requirements emerge independently across **multiple projects**, indicating ecosystem-wide consensus on user needs:

| Focus Area | Projects Affected | Specific Needs |
|------------|------------------|----------------|
| **Memory & Session Continuity** | OpenClaw #76877, NanoBot #3689/#3726, Hermes Agent #24699, PicoClaw #2859, CoPaw #4232, ZeroClaw #6608 | Agents losing context mid-work/after interrupt; session corruption during compaction; silent failure on tool-use boundary |
| **Provider API Compatibility** | OpenClaw #65867, NanoBot #3760, Hermes Agent #24833, PicoClaw #2859, IronClaw #3128, CoPaw #4159 | DeepSeek reasoning fields, Gemini final tags, Anthropic base_url quirks, Xiaomi MIMO failures—each new provider breaks existing assumptions |
| **Streaming & Real-time UX** | OpenClaw #81291, NanoBot #3655 (TUI/WebUI), PicoClaw #1950/#2404, Moltis #994 (scrolling regression) | Users expect streaming output to be reliable, scroll-locked, and stateful; regressions in WebUI are a top complaint |
| **Channel Reliability** | OpenClaw #80669, Hermes Agent #22487/#24922, CoPaw #2642/#4056, ZeroClaw #6609 | WhatsApp silent drops, DingTalk crashes, Matrix metadata gaps, Telegram setup failures—multi-platform delivery is still fragile |
| **Security Hardening** | PicoClaw #2688 (sandbox bypass), ZeroClaw #6613 (pairing code), LobsterAI #877 (URL whitelist), CoPaw #4267 (macOS sandbox-exec) | Path enumeration, authentication strength, and Electron IPC exposure are being addressed in parallel, suggesting common attack surface patterns |
| **Configuration & Onboarding Friction** | ZeroClaw #6120 (Codex/API key confusion), CoPaw #4159 (DashScope not read), NanoClaw #2433 (loopback exposure) | New users struggle with provider setup; misconfigured credentials or ports cause silent failures |

**Implication for developers:** Investing in session persistence patterns, provider API abstraction layers, and channel delivery retry logic would benefit the entire ecosystem. The convergence on these pain points represents a **market signal** for tooling and middleware opportunities.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | CoPaw | NanoBot | ZeroClaw | LobsterAI |
|-----------|----------|----------|-------|---------|----------|-----------|
| **Primary Language** | TypeScript/Node.js | Rust | TypeScript | TypeScript/Node.js | TypeScript | TypeScript (Electron) |
| **Target User** | Developers, advanced users | Rust ecosystem, security-conscious | Chinese enterprise teams | Lightweight home users | Developers, pre-release testers | Desktop UI users |
| **Key Architect. Choice** | Monolithic reference | Reborn architecture (composition hooks, outbound policy) | Multi-agent team rooms | OneCLI dependency, channel-first | Schema v3 migration, ACP session persistence | Electron desktop, Cowork collaboration |
| **Feature Strength** | Breadth, plugin system | Compile-time safety, performance | Enterprise IM (Feishu/DingTalk), MCP OAuth | Low-resource, quick setup | Provider compatibility, file management | Plugin management, voice input |
| **Community Structure** | Centralized maintainers, large contributor base | Core team + community PRs | Hybrid (Alibaba ecosystem) | Small, active core | Small core + active contributors | NetEase Youdao-backed |
| **Release Maturity** | Beta (daily releases) | Pre-release (nightly E2E failing) | Stable beta (v1.1.7) | v0.1.5.post3 (early) | Pre-v0.8.0 | Recent stable (v2026.5.12) |

**Key Insight:** The ecosystem is not in direct competition—projects serve distinct niches. OpenClaw is the **platform**; IronClaw targets **infrastructure-first** deployments; CoPaw owns **Chinese enterprise**; LobsterAI owns **desktop UX**; NanoBot and PicoClaw serve **lightweight/embedded** use cases.

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration with Quality Concerns:**
- **OpenClaw** — Highest feature velocity, but regression density is alarming. Users pinning to old versions (#76877) is a red flag. The 215 open issues and 455 open PRs suggest maintainers may be approaching cognitive overload.
- **IronClaw** — Reborn architecture advances weekly, but the nightly E2E pipeline failure (#3447) and blocked crate releases (#3259) slow downstream adoption.
- **ZeroClaw** — Accelerating toward v0.8.0 with strong bug-fix PR turnaround. Draft mega-PR (#6398) needs attention to avoid integration hell.

**Tier 2 — Healthy, Sustainable Cadence:**
- **CoPaw** — Balanced issue/PR closure, new beta release today, active security hardening. The most stable of the high-activity projects.
- **LobsterAI** — Cleared 14 stale PRs today. Strong feature cadence (voice, plugins, favorites). The only project with a proper "cowork" collaboration feature.
- **NanoClaw** — Small team, high PR throughput (8 merged today). Focused scope (Slack, Webhook, Google skills) prevents feature bloat.

**Tier 3 — Maintenance or Dormant:**
- **NanoBot** — Clearing backlog but no new release. One critical bug (#3760) unresolved.
- **PicoClaw** — Nightly builds available but unstable. Two security bugs have fix PRs, but streaming and cron features stalled for weeks.
- **Hermes Agent** — High issue count (46 open) with low merge rate (6/50). Maintainers responsive to critical bugs but not keeping up with volume.
- **ZeptoClaw** — Pure maintenance (dependency bumps, security audits). No feature development visible.
- **NullClaw, TinyClaw, Moltis** — Effectively stalled. Single PR aging for weeks/months; user question (#913) unanswered.

---

## 7. Trend Signals

### From Community Feedback, Extracted Industry Trends

**1. Users Demand "Reliable Autonomy" Over Feature Breadth**
Across the ecosystem, the most upvoted issues are not about new features but about **agents staying alive mid-work** (OpenClaw #76877, NanoBot #3689), **not losing context** (Hermes Agent #24699), and **not silently failing** (CoPaw #4232). This signals that the market has moved past "can it do X?" to "can I trust it to finish Y without intervention?".

**2. Provider API Fragmentation is the #1 Integration Cost**
DeepSeek reasoning fields, Gemini final tags, Anthropic base_url quirks—each project is independently solving the same provider API edge cases. This is a **strong signal for a standardized provider abstraction layer** or middleware SDK that could serve the whole ecosystem.

**3. Streaming is Table Stakes, Not a Differentiator**
Users expect streaming to work out of the box—reliable, scroll-locked, with reasoning display. Projects that treat streaming as a feature request (PicoClaw #1950, 50 days open) are falling behind. The market has normalized streaming as a baseline expectation.

**4. Multi-Platform Delivery is the Hardest Unsolved Problem**
WhatsApp drops, DingTalk crashes, Matrix metadata gaps, WeChat message loss—every project with channel support has a telemetry gap. This suggests the underlying protocol adaptation layer (Webhook, WebSocket, IM bridges) is inherently fragile and needs more investment.

**5. Security is Becoming a Differentiator**
PicoClaw's sandbox bypass fix, CoPaw's macOS `sandbox-exec`, LobsterAI's URL whitelist, ZeroClaw's pairing code strength—projects that ship security hardening alongside features are building trust. Users are noticing (ZeroClaw #6613 got immediate attention).

**6. Chinese Provider Ecosystem is Driving Parallel Innovation**
CoPaw (Alibaba ecosystem), PicoClaw (Xiaomi MIMO, GLM), and NanoBot (Qiniu AI, DashScope) are optimizing for Chinese LLM providers while the western-focused projects (OpenClaw, Hermes Agent) struggle with OpenAI/Anthropic edge cases. This bifurcation will likely persist as regulatory environments diverge.

**Value for AI Agent Developers:**
- **Invest in session persistence** — Transient session state is the top cause of user frustration. SQLite-backed transcripts (requested in OpenClaw #79902) would benefit all projects.
- **Abstract provider APIs aggressively** — The ecosystem is collectively spending too much time on provider-specific reasoning fields and error handling.
- **Prioritize channel reliability over new integrations** — A single well-tested Telegram path is worth more than five flaky channel adapters.
- **Build for headless/offline scenarios** — Multiple issues (Hermes Agent #22930, NanoBot #67, OpenClaw #67035 Windows regression) show users want to run agents on servers, thin clients, and low-resource hardware—not just developer workstations.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-05-13

## 1. Today's Overview
Today NanoBot shows very high activity: 15 issues and 23 pull requests were updated within the last 24 hours. Of the 15 issues, 12 are now closed and 3 remain open. Among the 23 PRs, 12 were merged or closed and 11 are still open. No new releases were published. The project appears in a maintenance and enhancement sprint, with a strong focus on fixing bugs (e.g., session compaction, DeepSeek reasoning, WebUI performance), adding new features (model failover, long-task tool, reasoning display), and cleaning up dead code. Community engagement is healthy, with several long-standing issues finally being resolved.

## 2. Releases
No new releases were detected in the last 24 hours. The latest published version remains **v0.1.5.post3**, as referenced in recent issue #3760.

## 3. Project Progress
Several notable PRs were merged or closed today, indicating significant feature advancement and refactoring:

- **Context preservation & session management:** PR #3765 (open) proposes a fix for `AutoCompact` to preserve session messages, while PR #3655 (merged) adds optional live display of model reasoning/thinking content in the TUI and WebUI.
- **Model failover:** PR #3756 (open) introduces `fallback_models` for chaining providers when the primary fails, a highly requested reliability improvement.
- **Long-task tool:** PR #3460 (open) adds a `LongTaskTool` meta-agent loop for breaking complex multi-step tasks into sequential subagent steps.
- **Dead code removal:** PR #3755 (merged) removed 103 lines of verified dead code across the CLI and agent modules, improving maintainability.
- **Provider & channel enhancements:** PR #3643 (open) adds support for Qiniu AI (七牛云) provider; PR #3761 (open) adds typing indicators and emoji reactions to the WhatsApp channel; PR #3752 (open) fixes media_paths cleanup after voice transcription.
- **Testing improvements:** PR #3766 (merged) adds 121 new tests and splits a 3313-line test file into focused modules, greatly expanding coverage.
- **Bedrock compatibility:** PR #3758 (merged) fixes a bug where Bedrock Converse rejected requests with historical tool blocks but no current `toolConfig`.
- **UX fixes:** PR #3759 (merged) makes WebUI default to a new chat on load and preserves scroll position when leaving settings.

Merged/closed PRs (12 total) also include several minor fixes such as Windows UNC path handling (#3764), Codex blank failure retries (#3762), and removal of the `ask_user` tool (#3757).

## 4. Community Hot Topics
- **Issue #235** – *"I've completed processing but have no response to give."*  
  (15 comments, 9 👍) – [Link](https://github.com/HKUDS/nanobot/issues/235)  
  A long-running mystery where the Telegram bot with `deepseek/deepseek-chat` silently stops responding after some time. No errors in gateway logs. Closed today, but the underlying cause may be related to session memory corruption or model output suppression.

- **Issue #3689** – *Interrupted session loses previous chat history (Chinese)*  
  (5 comments, 0 👍) – [Link](https://github.com/HKUDS/nanobot/issues/3689)  
  User reports that interrupting the agent during a loop causes it to forget the conversation and context. A clear pain point for users relying on multi-turn tasks. The community is discussing deeper memory continuity during interrupts.

- **Issue #67** – *Add explicit `provider` field for custom endpoint routing*  
  (3 comments, 7 👍) – [Link](https://github.com/HKUDS/nanobot/issues/67)  
  Closed today after a long wait. The feature would allow custom model names to bypass automatic routing (e.g., for local OpenAI-compatible servers). The high number of 👍 shows strong demand for more flexible provider configuration.

- **PR #3460** – *LongTaskTool for multi-step agent tasks*  
  (open, likely high interest) – [Link](https://github.com/HKUDS/nanobot/pull/3460)  
  This PR addresses the core need for executing long-running tasks without losing intermediate state. It is actively discussed and may become a cornerstone for agent reliability.

## 5. Bugs & Stability
Three open bugs were reported or updated today, plus one critical closed bug:

- **Critical: Issue #3760** – *deepseek-v4-flash + post3: reasoning_content triggered 400 error*  
  [Link](https://github.com/HKUDS/nanobot/issues/3760)  
  First-turn failure with DeepSeek v4 models due to the `reasoning_content` field being incorrectly passed. No fix PR exists yet. Severity: high, as it blocks usage of popular DeepSeek models.

- **High: Issue #3726** – *Context compression bug causing system crash*  
  [Link](https://github.com/HKUDS/nanobot/issues/3726)  
  Closed today. The auto-compact mechanism was destructively replacing session messages, leading to runtime errors. PR #3765 (open) proposes a fix by preserving messages with a cursor.

- **Medium: Issue #3746** – *WebUI preloads >1 MB code-highlighting chunk*  
  [Link](https://github.com/HKUDS/nanobot/issues/3746)  
  Performance issue where the Markdown renderer eagerly loads a large asset even when not needed. No fix PR yet, but it is labeled as both bug and enhancement.

- **Low: Issue #1640** – *Session stuck after manual memory deletion (GLM-4.7)*  
  [Link](https://github.com/HKUDS/nanobot/issues/1640)  
  Closed today. A persistent conversation context could not be reset. Likely resolved by related memory consolidation fixes.

## 6. Feature Requests & Roadmap Signals
Several enhancement issues and PRs indicate where the project is heading:

- **Model failover (PR #3756)** – Already proposed and under review. Likely to land soon, improving reliability for users in regions with unstable API access (e.g., China Mainland).

- **`/model` slash command (Issue #3742)** – Request to dynamically switch provider/model. If adopted, it would be a quick win for power users.

- **Streaming output (Issue #1860, closed)** – Already closed, but the feature is partially implemented via PR #3655 (reasoning display). Full streaming for all outputs may come in a future release.

- **WebSocket channel (Issue #1685)** – Closed, but user expressed need for agent-only usage without chat platforms. The PR from the forker may still be incoming.

- **Multi-agent setup clarity (Issue #1642)** – Closed, but the official recommendation (separate workspaces) remains unchanged. Could be revisited if demand grows.

- **More web search tools (Issue #941)** – Closed, but user wanted free options beyond Brave. No code change yet; may resurface.

Prediction for next release: model failover (PR #3756), long-task tool (PR #3460), reasoning display (PR #3655), and the session compaction fix (PR #3765) are strong candidates.

## 7. User Feedback Summary
- **Pain point #1: Session memory fragility.** Multiple issues (#3689, #1640, #235, #3726) describe agents losing context or getting stuck. Users expect robust memory across interrupts, idle periods, and manual resets.
- **Pain point #2: Provider/model compatibility.** DeepSeek's `reasoning_content` field (Issue #3760) and Bedrock tool config (PR #3758) show that edge cases in provider APIs are a recurring source of frustration.
- **Pain point #3: Need for fallback reliability.** Issue #3742 and PR #3756 reflect real-world instability when using Chinese AI services. Users want the bot to automatically switch to a backup provider when the primary fails.
- **Satisfaction:** Users praise NanoBot’s extensibility (channel support, MCP) but are vocal about missing production-grade resilience features. The swift merging of many long-standing issues (e.g., #1871 exec truncation, #67 routing) signals that maintainers are responsive.

## 8. Backlog Watch
- **Issue #3760** (open, 1 day old) – *DeepSeek v4 reasoning_content 400 error* – No fix PR yet. Given the popularity of DeepSeek models, this should be prioritized.
- **Issue #3746** (open, 2 days old) – *WebUI large preload* – Minor but affects first-load performance. No assignee.
- **Issue #3689** (open, 5 days old) – *Session interrupt loses history* – Enhancements toward memory continuity are being discussed; PR #3765 partially addresses it, but not fully merged.
- **PR #3460** (open since Apr 26) – *LongTaskTool* – A large, important feature; needs review and testing.
- **PR #3693** (open since May 8) – *Centralize LLM concurrency gate* – Addresses background task behavior; may be waiting for more test coverage.

No issue or PR has remained unanswered for more than a few days; the maintainers are highly active.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest – 2026-05-13

## 1. Today's Overview

Hermes Agent is experiencing a **very high level of activity**: 50 issues and 50 pull requests were updated in the last 24 hours. Of those, 4 issues were closed and 6 PRs were merged/closed, while 46 issues and 44 PRs remain open. No new releases were published today. The community is actively reporting bugs, contributing fixes, and proposing features—indicating a healthy, engaged development ecosystem. The project’s maintainers appear responsive, with multiple fix PRs already opened for bugs reported today.

## 2. Releases

**None.** No new versions were released in the last 24 hours. The latest release remains the previous tag (not specified in data).

## 3. Project Progress

The following PRs were **merged or closed** today (6 total). Key contributions include:

- **[PR #24310](https://github.com/NousResearch/hermes-agent/pull/24310)** (closed, type/perf) – Improved session-search performance by loading only windowed FTS5 match context instead of full conversations.
- Other closed/merged PRs (not shown in top 20) include minor fixes for gateway, CLI, and documentation. Additionally, 4 issues were closed:
  - **[#7237](https://github.com/NousResearch/hermes-agent/issues/7237)** – Response truncation bug (fix released earlier, now closed).
  - **[#8173](https://github.com/NousResearch/hermes-agent/issues/8173)** – Feishu/Lark gateway crash due to missing import.
  - **[#24837](https://github.com/NousResearch/hermes-agent/issues/24837)** – Shift+Enter regression on CLI (duplicate of #22908, closed as duplicate).

**Notable open PRs that advanced** (new today) include:
- **[#24936](https://github.com/NousResearch/hermes-agent/pull/24936)** – New CLI subcommand `hermes gateway send-message` to send text through connected platforms.
- **[#24938](https://github.com/NousResearch/hermes-agent/pull/24938)** – Adds update channels (`main` vs `release`) for more stable upgrades.
- **[#24925](https://github.com/NousResearch/hermes-agent/pull/24925)** – Performance improvement for `session_search` using FTS5 match IDs.
- **[#24811](https://github.com/NousResearch/hermes-agent/pull/24811)** – Adds `kanban_suspend`/`kanban_resume` primitives for long-running task management.
- **[#24423](https://github.com/NousResearch/hermes-agent/pull/24423)** – Multi-user identity via `X-Hermes-User-*` headers for the API server.
- **[#24916](https://github.com/NousResearch/hermes-agent/pull/24916)** – Buffered tool-progress for platforms without `edit_message` support (e.g., WeChat).

## 4. Community Hot Topics

The most discussed issues (by comment count) highlight central user concerns:

| Issue | Comments | Description |
|-------|----------|-------------|
| [#7237](https://github.com/NousResearch/hermes-agent/issues/7237) [CLOSED] | 25 | Response truncated due to output length limit – a common pain point for long-form generation. |
| [#22714](https://github.com/NousResearch/hermes-agent/issues/22714) [P1] | 8 | Matrix gateway lacks in-band channel for per-message LLM orchestration, blocking downstream dispatchers. |
| [#20249](https://github.com/NousResearch/hermes-agent/issues/20249) [P3] | 8 | Request for per-turn model escalation ("expert-on-demand") to switch between cheap/fast and powerful models within a session. |
| [#8173](https://github.com/NousResearch/hermes-agent/issues/8173) [CLOSED] | 5 | Feishu gateway crash due to missing `RedactingFormatter` import (fix merged). |
| [#24699](https://github.com/NousResearch/hermes-agent/issues/24699) [P3] | 4 | Abnormal Kanban task processing – context loss after suspension, spurious execution. |

**Underlying needs**: Users want better control over model selection (mid-session escalation), longer output handling, and more reliable multi-platform gateway support.

## 5. Bugs & Stability

Many bugs were reported today, with several **P2** and **P1** severity issues. PRs fixing most of them are already open.

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| [#24933](https://github.com/NousResearch/hermes-agent/issues/24933) | P2 | Codex/Responses API commentary-phase planning text leaks as visible Telegram messages. | None yet |
| [#24922](https://github.com/NousResearch/hermes-agent/issues/24922) | P2 | Email adapter fails to send audio attachments (`.mp3`, `.wav`, etc.) – `send_voice()` missing. | [#24931](https://github.com/NousResearch/hermes-agent/pull/24931), [#24932](https://github.com/NousResearch/hermes-agent/pull/24932) |
| [#24842](https://github.com/NousResearch/hermes-agent/issues/24842) | P2 | `vision_analyze` and `browser_vision` hardcoded to Gemma, ignoring `auxiliary.vision` config. | None yet |
| [#24833](https://github.com/NousResearch/hermes-agent/issues/24833) | P2 | Anthropic provider 404s when `base_url` includes `/v1` (SDK appends another). | None yet |
| [#24523](https://github.com/NousResearch/hermes-agent/issues/24523) | P2 | `custom:llmgateway` tool calls fail when streamed. | None yet |
| [#24029](https://github.com/NousResearch/hermes-agent/issues/24029) | P2 | Auxiliary tasks silently fall back to paid OpenRouter models, bypassing user's free-only configuration. | None yet |
| [#24882](https://github.com/NousResearch/hermes-agent/issues/24882) | P2 | `terminal.cwd` not correctly injected into system prompt causing wrong directory usage. | None yet |
| [#24827](https://github.com/NousResearch/hermes-agent/issues/24827) | P3 | Web UI build fails on Windows because of Unix `rm` command. | None yet |
| [#24906](https://github.com/NousResearch/hermes-agent/issues/24906) | P2 | Feishu MEDIA protocol support issue – image sending fails through some code paths. | None yet |
| [#24910](https://github.com/NousResearch/hermes-agent/issues/24910) | P2 | Dashboard Chat shows `[session ended]` in PTY/headless environments – TUI entry.js exits early. | None yet |
| [#22908](https://github.com/NousResearch/hermes-agent/issues/22908) | P2 | Shift+Enter no longer inserts newline in classic CLI (regression from thin PTY fix). | Duplicate of [#24837](https://github.com/NousResearch/hermes-agent/issues/24837) (closed) |
| [#24920](https://github.com/NousResearch/hermes-agent/issues/24592) (via PR) | P1 | ACP/LLM responses stripped of whitespace (e.g., "Hey there!" → "Heythere!"). | [#24920](https://github.com/NousResearch/hermes-agent/pull/24920) |
| [#24930](https://github.com/NousResearch/hermes-agent/pull/24930) | P2 | Browser sandbox bypass fails because `AGENT_BROWSER_CHROME_FLAGS` is ignored in agent-browser 0.26+. | Fix PR already open |

**Summary**: Today saw a cluster of regressions (Shift+Enter, gateway crashes) and platform-specific bugs (Email audio, Feishu MEDIA, Windows build). The maintainers have been quick to open fix PRs for many of these, indicating healthy triage.

## 6. Feature Requests & Roadmap Signals

Several feature-oriented issues were opened today, pointing toward upcoming enhancements:

| Issue | Severity | Feature | Likelihood for Next Release |
|-------|----------|---------|-----------------------------|
| [#24913](https://github.com/NousResearch/hermes-agent/issues/24913) | P3 | One gateway serving multiple agents, switchable via `/profile <name>` or `@<name>` | Medium – requested often, complex |
| [#24917](https://github.com/NousResearch/hermes-agent/issues/24917) | P3 | Support user-provided extra CA bundles for HTTPS proxies | High – simple config change, low risk |
| [#24935](https://github.com/NousResearch/hermes-agent/issues/24935) | P3 | Per-profile isolation for hindsight memory provider | Medium – improves multi-tenant use |
| [#24937](https://github.com/NousResearch/hermes-agent/issues/24937) | – | Enable DashScope explicit context caching for alibaba provider to cut costs (90% savings) | High – already has PR? (no PR yet) |
| [#24862](https://github.com/NousResearch/hermes-agent/issues/24862) | P3 | Persistent TODO side panel in TUI | Low – nice-to-have UI enhancement |
| [#20249](https://github.com/NousResearch/hermes-agent/issues/20249) | P3 | Per-turn model escalation (expert-on-demand) | High – 8 comments, strong interest |
| [#24423](https://github.com/NousResearch/hermes-agent/pull/24423) | P3 | Multi-user identity headers for API server | Already in PR – likely to merge soon |

**Prediction**: The next minor release will likely include support for extra CA bundles (#24917), the new `hermes gateway send-message` command (#24936), update channels (#24938), and DashScope caching (#24937). The model escalation feature (#20249) may land in a subsequent release due to its architectural impact.

## 7. User Feedback Summary

Common pain points expressed in today's issues:

- **Output length limits** – Users generating long responses (e.g., code, analysis) hit truncation errors (#7237).
- **Multi-platform reliability** – DingTalk file sending (#22487), Feishu media (#24906), Email audio (#24922), and Matrix orchestration (#22714) all have gaps.
- **CLI/UI regressions** – Shift+Enter behavior broke for macOS users (#22908, #24837, #24890), and the TUI shows empty session in headless environments (#24910).
- **Model control gaps** – Hardcoded vision models (#24842), auxiliary tasks ignoring free-only config (#24029), and inability to switch models mid-session (#20249) show users want finer-grained control.
- **Offline/limited GPU setups** – Users struggle to run smaller models (2B–14B) offline when computing power is insufficient (#22930).
- **Configuration friction** – Custom CA bundles (#24917), Homebrew missing skills (#24360), and provider base URL confusion (#24833) highlight documentation/tooling needs.

Satisfaction signals: High engagement (many PRs opened by community members), quick maintainer response to critical bugs (e.g., #24920 fixed within hours), and active feature development on performance and usability.

## 8. Backlog Watch

The following issues are **open, important, and lack a fix PR or maintainer response in recent days**:

| Issue | Severity | Created | Last Updated | Remarks |
|-------|----------|---------|--------------|---------|
| [#11411](https://github.com/NousResearch/hermes-agent/issues/11411) | – | Apr 17 | May 13 | Custom GPT-5.4 gateway sessions hit Responses API 400 error. Still reproducible after update. No fix PR. |
| [#22487](https://github.com/NousResearch/hermes-agent/issues/22487) | P2 | May 9 | May 13 | DingTalk cannot send images/files. Logs show attempts but nothing arrives. No fix PR. |
| [#22930](https://github.com/NousResearch/hermes-agent/issues/22930) | P3 | May 10 | May 13 | Offline mode for small models – insufficient guidance. No maintainer response. |
| [#24029](https://github.com/NousResearch/hermes-agent/issues/24029) | P2 | May 11 | May 13 | Auxiliary tasks bypassing free-only OpenRouter config, causing unexpected billing. No fix PR. |
| [#24523](https://github.com/NousResearch/hermes-agent/issues/24523) | P2 | May 12 | May 13 | `custom:llmgateway` streaming failures. No fix PR. |
| [#24833](https://github.com/NousResearch/hermes-agent/issues/24833) | P2 | May 13 | May 13 | Anthropic provider 404 due to double `/v1`. No fix PR yet. |
| [#24884](https://github.com/NousResearch/hermes-agent/issues/24884) | P3 | May 13 | May 13 | Xiaomi MiMo thinking mode broken via Anthropic endpoint. No maintainer response. |

These issues may require maintainer triage to either accept contributions or provide workarounds. Notably, #11411 (custom GPT-5.4) and #22487 (DingTalk) have been open for weeks without resolution.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-05-13

## 1. Today's Overview

PicoClaw remains in an active development and community feedback cycle. In the last 24 hours, 18 issues were updated (11 still open) and 15 pull requests saw activity (11 open), indicating sustained contributor interest. A new **nightly build** (v0.2.8-nightly.20260513) was published, though marked as potentially unstable. Several high-priority bugs—including a PID-file collision crash and a workspace sandbox bypass—received actionable fix PRs, while user-facing improvements like unified diff preview for `edit_file` were merged. Overall project health appears robust, with maintainers handling both critical defects and long-standing feature requests.

## 2. Releases

**New release:** `v0.2.8-nightly.20260513.223ebdf0` (Nightly Build)  
- **Changelog:** [Compare v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
- **Notes:** Automated build, may be unstable. No breaking changes or migration notes provided.  
- **Verdict:** Not recommended for production use; intended for early testing of pre-release features.

## 3. Project Progress (Merged/Closed PRs Today)

Two pull requests were closed/merged today:

- **[#2857](https://github.com/sipeed/picoclaw/pull/2857) — feat(tools): show unified diff for `edit_file` edits**  
  Merged. Changes the `edit_file` tool to return a `DiffResult` with a unified diff instead of a generic `SilentResult`, giving users and the LLM immediate visibility into file changes.

- **[#2860](https://github.com/sipeed/picoclaw/pull/2860) — docs: update WeChat QR code**  
  Merged. A documentation update refreshing the WeChat channel QR code.

Other closed PRs (from previous days):  
- [#2505](https://github.com/sipeed/picoclaw/pull/2505) (CLI workspace embedding fix)  
- [#2490](https://github.com/sipeed/picoclaw/pull/2490) (onboarding advisory fix)

## 4. Community Hot Topics

Most active issues and PRs (by comments or reactions):

| Issue/PR | Title | Comments | Reactions | Key Notes |
|----------|-------|----------|-----------|-----------|
| [#2859](https://github.com/sipeed/picoclaw/issues/2859) | [BUG] Xiaomi MIMO multi-turn conversation failure | 0 | 1 👍 | Newly opened; downstream LLM error after 2–3 rounds |
| [#2513](https://github.com/sipeed/picoclaw/issues/2513) | [BUG] gateway start abnormal (closed) | 9 | 0 | Closed; resolved after debugging |
| [#1950](https://github.com/sipeed/picoclaw/issues/1950) | [Feature] Streaming output for Web Chat | 8 | 0 | Long-running request (since March), still open |
| [#1757](https://github.com/sipeed/picoclaw/issues/1757) | [BUG] Cron + channel error when asking agent to repeat tasks | 8 | 0 | Affects Telegram channel; stale but unresolved |
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) | [Feature] Add streaming config for HTTP requests | 6 | 1 👍 | Key for advanced LLM backends |
| [#2444](https://github.com/sipeed/picoclaw/issues/2444) | [Feature] MCP secrets in `.security.yml` (closed) | 5 | 2 👍 | Popular request, now closed as resolved |

**Underlying needs:** Users consistently demand better streaming support (both HTTP and Web Chat), improved security for path enumeration, and stable multi-turn conversation with newer Chinese providers (Xiaomi MIMO). The high engagement on MCP secrets (#2444) indicates strong interest in secure credential management.

## 5. Bugs & Stability

**High severity** (all with open fix PRs):

- **[#2720](https://github.com/sipeed/picoclaw/issues/2720) — Singleton PID check doesn’t verify process identity**  
  Gateway fails if stale PID is reused by an unrelated process. **Fix PR:** [#2813](https://github.com/sipeed/picoclaw/pull/2813) (updated today) — adds verification that the PID belongs to a `picoclaw gateway` instance.

- **[#2688](https://github.com/sipeed/picoclaw/issues/2688) — Security: `find /` can enumerate paths outside workspace sandbox**  
  Workspace sandbox bypass. **Fix PR:** [#2693](https://github.com/sipeed/picoclaw/pull/2693) — blocks `find /` and `ls /` commands.

**Medium severity:**

- **[#2859](https://github.com/sipeed/picoclaw/issues/2859) — Xiaomi MIMO integration: multi-turn conversation fails with 400 error**  
  New bug; no fix PR yet. Likely provider-specific parameter handling issue.

- **[#2742](https://github.com/sipeed/picoclaw/issues/2742) — gateway starts with no channels in v0.2.8**  
  Reported on Telegram channel; appears configuration-dependent.

**Lower severity / closed:**

- [#2513](https://github.com/sipeed/picoclaw/issues/2513) — Gateway start abnormal (closed)  
- [#2694](https://github.com/sipeed/picoclaw/issues/2694) — x509 certificate verification failure in ADB shell (closed)  
- [#2848](https://github.com/sipeed/picoclaw/issues/2848) — Missing diff preview for `edit_file` (closed; fixed by PR #2857)

## 6. Feature Requests & Roadmap Signals

| Request | Issue/PR | Status | Likelihood for next version |
|---------|----------|--------|-----------------------------|
| Streaming config for HTTP requests | [#2404](https://github.com/sipeed/picoclaw/issues/2404) | Open, stale | Medium – aligns with existing streaming work |
| WhatsApp support in default builds | [#2625](https://github.com/sipeed/picoclaw/issues/2625) | Open, stale | Low – depends on build flag adoption |
| Mission Control integration | [#2698](https://github.com/sipeed/picoclaw/issues/2698) | Closed | Not accepted |
| Context/memory management (inspired by magic-context plugin) | [#2774](https://github.com/sipeed/picoclaw/issues/2774) | Open | Low – vague requirements |
| Config reliability and migration UX | [#2771](https://github.com/sipeed/picoclaw/issues/2771) | Open | Medium – practical improvements |
| Gemini web search provider | [#2763](https://github.com/sipeed/picoclaw/pull/2763) | Open PR | High – under review |
| Streaming reasoning_content + video media (OpenAI-compat) | [#2755](https://github.com/sipeed/picoclaw/pull/2755) | Open PR | High – adds multimodal support |
| Intel OpenVINO Model Server support | [#2703](https://github.com/sipeed/picoclaw/pull/2703) | Open PR | Medium – niche hardware |
| Session management commands (`/status`, `/compact`, `/new`) | [#2491](https://github.com/sipeed/picoclaw/pull/2491) | Open, stale | Medium – valuable power-user feature |
| Skill catalog token optimization | [#2781](https://github.com/sipeed/picoclaw/pull/2781) | Open PR | High – improves efficiency on all providers |

**Prediction for v0.2.9:** The most likely merges are the Gemini search provider (#2763), streaming reasoning/video support (#2755), and the skill catalog optimization (#2781). The PID fix (#2813) and sandbox bypass (#2693) are critical and should also land.

## 7. User Feedback Summary

- **Pain points:**
  - Sandbox security gaps (path enumeration via `find /`).
  - Gateway process identity not validated, leading to crash loops after unclean shutdowns.
  - Multi-turn conversations failing with Chinese providers (Xiaomi MIMO).
  - Web Chat lacks streaming output (top requested feature).
  - Build from source does not produce the `picoclaw-launcher` binary (reported by several users, e.g., [#2753](https://github.com/sipeed/picoclaw/issues/2753)).

- **Positive signals:**
  - Successful hardware validation on NXP i.MX93 EVK ([#2646](https://github.com/sipeed/picoclaw/issues/2646), closed).
  - Users actively contributing fixes (e.g., sandbox bypass, PID verification, config YAML support).
  - High 👍 count on the MCP secrets feature (#2444) indicates strong alignment with user needs.

- **Satisfaction:** Generally moderate; users appreciate rapid bug fixes but are frustrated by long-standing feature gaps (streaming, sandbox) and build issues.

## 8. Backlog Watch

Issues and PRs that have been open for >30 days without maintainer response or progress:

| Item | Issue/PR | Last Update | Days Open | Concern |
|------|----------|-------------|-----------|---------|
| [#1757](https://github.com/sipeed/picoclaw/issues/1757) — Cron + channel error | Issue | 2026-05-12 | 56 | No maintainer comment since creation; affects cron jobs |
| [#1950](https://github.com/sipeed/picoclaw/issues/1950) — Streaming Web Chat | Issue | 2026-05-12 | 50 | High community interest, no roadmap commitment |
| [#2404](https://github.com/sipeed/picoclaw/issues/2404) — Streaming HTTP config | Issue | 2026-05-12 | 36 | Directly needed by many users |
| [#2491](https://github.com/sipeed/picoclaw/pull/2491) — Session management commands | PR | 2026-05-12 | 31 | Needs review; good UX feature |
| [#2647](https://github.com/sipeed/picoclaw/pull/2647) — YAML web_search + DuckDuckGo default | PR | 2026-05-12 | 19 (but stale) | Awaiting merge conflict resolution |
| [#2703](https://github.com/sipeed/picoclaw/pull/2703) — OpenVINO support | PR | 2026-05-12 | 15 (but stale) | Needs maintainer feedback |

**Action needed:** Maintainers should triage the backlog—particularly #1757 (cron/channel bug) and #1950 (streaming)—to avoid contributor burnout and user frustration.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-05-13

## 1. Today's Overview
NanoClaw saw moderately high activity with **21 PRs updated** in the last 24 hours, of which **8 were merged/closed** and **13 remain open**. Two issues were active, one of which (a high-priority security hardening for OneCLI) has an associated fix PR. The project is advancing on multiple fronts: **Slack channel support** (bidirectional AI-to-AI), a new **webhook channel type**, Google Workspace skill expansion, and various bug fixes. The community is also questioning the lightweight ethos of the project in light of the OneCLI dependency, prompting a separate discussion issue.

## 2. Releases
**No new releases.** The latest release remains unchanged.

## 3. Project Progress – Merged/Closed PRs Today
Eight PRs were merged or closed (with several appearing to have been merged based on their status and summary):

- **#2443** – `feat(slack): auto-prepend peer mention on AI-to-AI outbound messages` – adds transport-layer guard for Slack peer mentions, configurable via `SLACK_PEER_MENTIONS` env var.  
- **#2442** – `fix(core-instructions): require message wrapping for single-destination agents` – corrects stale instruction that caused responses to be silently dropped to scratchpad.  
- **#567** – `docs: clarify that any Docker-compatible runtime works` – updates README and docs to list Colima / OrbStack as alternatives to Docker Desktop.  
- **#2441** – `feat(channels): Slack channel with AI-to-AI bidirectional support` – cherry-picks Slack adapter with patches for peer-bot messaging.  
- **#2438** – `fix(chat-sdk-bridge): fetch attachment URL when adapter lacks fetchData` – fixes silent failure for channels that don’t provide binary attachment fetching.  
- **#1631** – `skill/sentry: add Sentry IPC integration` – new feature skill for error reporting.  
- **#2439** – `feat(webhook): webhook channel type – push-based inbound from Supabase, GitHub Actions, and other producers` – adds authenticated POST endpoint per messaging group.  
- **#2422** – `feat(skills): add /add-google-auth foundation skill + diagnostic MCP tools` – ships shared Google OAuth prerequisites and diagnostic tools.

**Summary of progress:** Slack integration is maturing, webhook channel is live, Google tool suite is expanding, and several fixes addressing silent failures and documentation gaps have been merged.

## 4. Community Hot Topics
The most active discussions center around the project’s dependency on OneCLI:

- **[Issue #2437](https://github.com/nanocoai/nanoclaw/issues/2437) – “Any appetite for removing/improving the OneCLI dependency?”**  
  The author argues that NanoClaw’s lightweight claim is undermined by a heavy dependency on OneCLI. No comments yet, but the topic touches a core architectural philosophy.

- **[Issue #2433 / PR #2434](https://github.com/nanocoai/nanoclaw/issues/2433) – “restrict OneCLI admin API and Postgres to loopback after install”**  
  Marked **Priority: High** with an existing fix PR. The bug exposes admin and database ports on the `docker0` bridge, a security concern. The PR (#2434) is open and authored by the same reporter (glifocat). This has drawn attention due to its security implications.

Other active PRs with ongoing discussion (though comment counts are not shown) include the **scheduled tasks fix** (#2411) and the **model-config community skill** (#1545).

## 5. Bugs & Stability
Reported bugs ranked by severity:

| Severity | Issue/PR | Description | Fix Status |
|----------|----------|-------------|------------|
| **High** | #2433 / #2434 | OneCLI install binds admin API (`:10254`) and Postgres (`:5432`) to `docker0` bridge, exposing them on the network. | Open PR #2434 |
| **Medium** | #2411 | Recurring scheduled tasks silently no‑op – row fires, agent ends cleanly, but no output and user never receives expected message. | Open PR #2411 |
| **Medium** | #2442 (merged) | Stale instruction caused agents to write messages to scratchpad instead of delivering them. | Fixed (merged today) |
| **Medium** | #2438 (merged) | Chat SDK bridge crashes when adapter lacks `fetchData` for attachments; now falls back to URL. | Fixed (merged today) |
| **Low** | #2435 | Webhook server hardcoded to port 3000 causing `EADDRINUSE` crashes. | Open PR #2435 |
| **Low** | #2429 | WhatsApp inbound media not routed to session inbox (host path exposure). | Open PR #2429 |
| **Low** | #2276 | Older PR proposing similar URL fallback fix; overlaps with #2438 (now merged). | Open, possibly superseded |

A long-standing timestamp normalization bug (#1845) remains open since April.

## 6. Feature Requests & Roadmap Signals
- **OneCLI dependency reconsideration** – Issue #2437 signals that some users want a lighter, self-contained setup. This could lead to a future architecture change or extraction of OneCLI into an optional component.
- **Slack channel maturity** – Multiple PRs (#2441, #2443) merged today indicate Slack is being actively developed for both human‑bot and AI‑to‑AI communication. Likely to be included in next release.
- **Webhook channel** – PR #2439 adds a push-based inbound channel, enabling integrations with GitHub Actions, Supabase, etc. This broadens the platform’s reach beyond Chat SDK adapters.
- **Google Workspace skill suite** – With Gmail, Calendar, and now Google Drive (#2430) skills, a complete Google tool integration is emerging. A community skill for Google Auth foundation (#2422) is already merged.
- **Per‑invocation model config** – PR #1545 proposes an `/add-model-config` skill to allow overriding model, effort, and thinking parameters at invocation time. This would address a common use case for advanced users.
- **Conditional thread policy for Slack** – PR #2431 introduces optional `shouldUseThreadsFor` on adapters, letting Slack disable threading in DMs while preserving it in channels.

**Likely next‑version features:** Slack AI‑to‑AI support, webhook channel, and the OneCLI loopback security fix.

## 7. User Feedback Summary
- **Philosophical dissatisfaction** – Issue #2437 questions the “lightweight” branding given the OneCLI dependency. The user appreciates the `pnpm run dev` simplicity but finds the gateway dependency “detracts significantly from this.”
- **Silent failures causing confusion** – Multiple bugs (scheduled tasks #2411, core instructions #2442, attachment bridging #2438) point to a pattern where agents silently drop messages or skip actions. Users notice only when expected output never arrives.
- **Security conscious** – The loopback binding issue (#2433) was reported with a clear reproduction scenario, showing that users are running on bare‑metal Linux and monitoring port exposure.
- **Positive contributor momentum** – High volume of quality PRs from community members (glifocat, flusterff, jesolsen, TriKro, etc.) suggests a healthy, engaged contributor base.

## 8. Backlog Watch
The following issues/PRs have been open for extended periods and need maintainer attention:

- **#567** – `docs: clarify that any Docker-compatible runtime works` – **Open since Feb 27, status “Blocked”**. Updated today but still unmerged. Likely needs final review or a decision on scope.
- **#1845** – `fix(db): normalize auto-generated timestamps to ISO 8601` – **Open since Apr 18**. Affects query compatibility with channel adapters. No activity for over a month.
- **#1545** – `feat: add /add-model-config skill` – **Open since Mar 30**. A community‑written operational skill. No maintainer review. Awaiting decision on inclusion.
- **#2276** – `fix(channels): URL fallback in bridge when adapter omits fetchData` – **Open since May 5**. Possibly superseded by now‑merged #2438. Should be closed.

**Action items:** Evaluate #567 for merge; provide feedback on #1845 and #1545; close #2276 as duplicate.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-05-13

## 1. Today's Overview
Activity on the NullClaw project is light today. One new issue was opened (#913) inquiring about A2A protocol performance, indicating user interest in benchmarking. The only pull request update came from an existing feature branch (#783, introducing a cron subagent engine), which received its latest activity after a month of relative quiet. No new releases or merged PRs are recorded, suggesting the project is in a steady-state phase with one large feature still under review. Overall, the repository shows low churn but a clear signal that users are beginning to test and compare core subsystems.

## 2. Releases
No new releases were published in the last 24 hours. The latest release remains unchanged.

## 3. Project Progress
No pull requests were merged or closed today. The single open PR (#783) was last updated on 2026-05-13 but remains unmerged. No code changes or fixes were committed to the main branch in the reporting period.

## 4. Community Hot Topics
Only two items saw activity today:

- **[Issue #913 – a2a performance?](https://github.com/nullclaw/nullclaw/issues/913)**  
  *Author: jacktang* | Created: 2026-05-12 | Updated: 2026-05-12 | Comments: 0 | 👍: 0  
  The user asks for benchmark data on the A2A protocol implementation, noting that raw NullClaw messaging/response appears faster. While lacking comments or reactions, this is the only issue opened today and touches on a core architectural question. Underlying need: users require transparent performance metrics to decide when to use A2A vs. raw messaging, and may be experiencing unexpected latency.

- **[PR #783 – feat(cron): cron subagent, run history, JSON output, security hardening](https://github.com/nullclaw/nullclaw/pull/783)**  
  *Author: yanggf8* | Updated: 2026-05-13 | Comments: undefined | 👍: 0  
  This large feature PR (opened 2026-04-07) adds a DB-backed job scheduler, JSON CLI output, and per-job timezone support. Its recent update after a long pause suggests the author is still active, but the lack of reviewer comments or reactions may indicate maintainer bandwidth is a limiting factor.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. **Issue #913** is a performance question, not a bug report. The project appears stable in the near term.

## 6. Feature Requests & Roadmap Signals
- **Performance benchmarking for A2A** – Issue #913 implicitly requests official benchmarks or documentation comparing A2A vs. raw messaging. If the maintainers address this, it could lead to optimizations in the A2A protocol path.
- **Cron subagent feature** – PR #783 is a substantial addition (scheduler, job history, JSON output, security hardening). If merged, it would become part of the next release, likely v0.x or a minor version bump.
- No other feature requests appeared today. The roadmap signal points to continued investment in scheduling/automation capabilities.

## 7. User Feedback Summary
The single user interaction (issue #913) reflects a real pain point: the A2A protocol’s performance is perceived as slower than raw messaging. The user is actively comparing the two and seeks data to justify their choice. No positive or negative feedback on other features was recorded. The feedback is constructive but carries implicit dissatisfaction with A2A’s current speed.

## 8. Backlog Watch
- **PR #783 – Cron subagent feature** (opened 2026-04-07, last updated 2026-05-13)  
  This PR has been open for over a month without review. The large diff and new feature scope require maintainer attention to assess, test, and merge. Its continued aging could lead to merge conflicts or morale drain on the contributor.
- **Issue #913** is still very fresh (1 day old) and does not yet qualify as backlog, but if left unanswered for a week it could indicate poor responsiveness to user queries.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-05-13

## 1. Today's Overview
The IronClaw project is in a high‑activity phase: 50 pull requests and 21 issues were updated in the last 24 hours, with 11 PRs merged or closed. Development is heavily concentrated on the **Reborn** architecture—new composition infrastructure, loop hooks, outbound policy, and API crate. At the same time, multiple user‑facing bugs (Gmail authentication, Telegram setup, UI timestamps) are being addressed. A **nightly E2E pipeline failure** (#3447) remained unresolved as of today, signalling a stability risk. Downstream consumers remain blocked from receiving crate updates beyond `0.24.0` due to the unpinned release gap (#3259).

---

## 2. Releases
No new releases were published today.

---

## 3. Project Progress
**Merged/closed PRs (total 11)** – exact PR numbers are not enumerated in the data, but issue closures strongly indicate progress has landed for:

- **[#2229]** – Google Sheets OAuth blocked (closed after 11 comments)  
- **[#3128]** – Gmail 502 on authentication callback (closed)  
- **[#3523]** – Reborn: first‑class loop hook framework (merged/closed)  
- **[#3034]** – V2 engine HTTP tool disabled by default (closed)  
- **[#3530]** – Test agent hosting issue (closed)

These closures show the team is actively fixing critical authentication and engine‑level bugs. The **Reborn hooks framework** (#3523) is a major architectural addition that landed today, promising better extensibility without weakening existing boundaries.

**Ongoing feature work** visible in open PRs includes:
- **Reborn composition root readiness** (#3566, XL) – adds facade‑only crate with profiles and readiness API
- **Deterministic instruction bundle builder** (#3536, XL) – core for Reborn agent loop
- **Non‑image attachment UX** (#3531, XL) – closes a long‑standing web UI gap (reference #1341)
- **WeCom channel** (#2394, XL) – new WASM channel for Enterprise WeChat (still open since April)
- **Credential signers (HMAC / EIP‑712 / NEP‑413 / Solana)** (#3256, XL) – blocked by security review (#3564)
- **Image tool configuration** (#3004, XL) – dedicated image generation/editing endpoints

---

## 4. Community Hot Topics

### Most‑commented issues
- **[#2229] Google Sheets OAuth blocked** – 11 comments, now closed. Users hit `invalid_request` during the authorize flow; the fix was likely coordinated with the Gmail 502 fix.
- **[#3259] Publish 0.25.0–0.27.0 to crates.io** – 3 comments, still open. Downstream projects are pinned to `0.24.0` due to `wasmtime` CVE fixes in later versions. This is a blocking issue for the Rust ecosystem.
- **[#3128] Connecting to Gmail gives 502** – 2 comments, now closed. The authentication callback returned 502 in chat, but installing via settings worked – a routing or environment‑specific bug.

### Most active PR discussions (based on review activity)
- **[#3256] Credential signers** – still under security review, with a dedicated issue (#3564) arguing the approach is architecturally unsound.
- **[#3531] Non‑image attachment UX** – received extensive review and iteration, touching both frontend and backend.
- **[#3559] Restore chat‑driven tool_install / fix Telegram setup** – directly addresses user frustration from [#3533](#3533).

**Underlying needs**: Users overwhelmingly struggle with **authentication flows** (Gmail, Google Sheets, Telegram) and **onboarding**. The community is also vocal about the **missing crate releases** that block consumption of improvements and security fixes.

---

## 5. Bugs & Stability

### New bugs reported today (2026-05-13)
| Issue | Severity | Summary | Fix PR exists? |
|-------|----------|---------|----------------|
| [#3533] | **P1** | Telegram in v0.28.1 does not automatically setup from UI | Yes – [#3559] (open, in review) |
| [#3535] | **P1** | UI timestamps are incorrect for conversations | No |
| [#3564] | **Security** | Wallet signing requires unforgeable user‑auth channel – host‑resident keys problematic | No (blocks #3256) |
| [#3447] | **Stability** | Nightly E2E scheduled run failed | No (workflow failure, not a code bug) |
| [#3319] | **P1** | Gmail authentication fails (400) when started from Telegram | No (related to #3320) |
| [#3320] | **P1** | IronClaw in Telegram cannot continue after Gmail auth failure (even after `/clear`) | No (related to #3319) |
| [#2905] | **P1** | Agent saves files to inaccessible `/home/agent` in hosted setup | No (open since Apr 23) |
| [#2991] | **P2** | V2 approval flow broken: unclear prompts, sequential execution | No |
| [#2752] | **P1** | `onboard` command throws DB error on provider step | No |
| [#2283] | **P2/P3** | Web UI still cannot send files to bot | No (open since Apr 10) |

**Stability note**: The nightly E2E failure (#3447) is a recurring concern with no fix yet. A PR (#3565) extends the workflow timeout, but the root cause is still unknown.

---

## 6. Feature Requests & Roadmap Signals

**User‑requested / enhancement issues** (all created or updated today):
- **[#3537]** – **Reborn: model memory as userland extension** – memory should be a pluggable extension, not kernel layer. Likely to land in next Reborn release.
- **[#3524]** – **Reborn: first‑class loop hooks roadmap** – complementary to the now‑merged #3523. Defines inline hooks, outbound policies, and security gates.
- **[#3564]** – **Wallet signing channel** – argues for a mediated auth channel instead of host‑resident keys. Could reshape credential signing implementation.
- **[#3534]** – **Tool to download logs for debugging** – simple but high‑impact request for operational users.
- **[#3259]** – **Publish missing crate versions** – not a feature, but a frequent request from the Rust community.

**Prediction for next version (likely 0.28.x or 0.29.0)**:
- Reborn loop hooks (already merged) and instruction bundle builder.
- Authenticated credential signing (will depend on resolution of #3564).
- Improved Telegram onboarding (via #3559).
- Non‑image file attachments in web UI (#3531).

---

## 7. User Feedback Summary

**Frustrations (pain points)**:
- **Authentication failures** – Gmail and Google Sheets OAuth consistently break when initiated from Telegram chat; users are left with a dead conversation.
- **Telegram setup not automatic** – users expect a seamless flow; current UI asks to complete steps that used to be automatic.
- **No file uploads in Web UI** – a known limitation since April 10 (#2283) with no timeline.
- **Incorrect timestamps** – minor but erodes trust in conversation history.
- **Broken approval flow in V2 engine** – unclear prompts and routing force sequential execution.
- **Onboarding command fails with DB error** – blocks local development.

**Satisfaction signals**:
- Several bugs from the April bug bash (Google Sheets OAuth, Gmail 502, V2 HTTP tool) have been closed, showing the team is responsive.
- The **Reborn architecture** is rapidly maturing, with concrete PRs landing for hooks, composition, and outbound policy – a positive sign for long‑term stability.

**Unmet need**: The community still lacks a stable release channel for Rust consumers, and many basic UX flows (file upload, new user onboarding) remain incomplete despite being reported months ago.

---

## 8. Backlog Watch

Issues that have been **open for weeks or longer** with no clear resolution or maintainer response:

| Issue | Created | Days Open | Summary | Status |
|-------|---------|-----------|---------|--------|
| [#2283] | 2026-04-10 | 33 | Web UI cannot send files to bot | No assignee; labelled P2/P3 |
| [#2905] | 2026-04-23 | 20 | Agent saves files to inaccessible `/home/agent` | Labelled P1 but no fix PR |
| [#2991] | 2026-04-27 | 16 | V2 approval flow broken (P2) | Open |
| [#2752] | 2026-04-20 | 23 | `onboard` command DB error (P1) | Open |
| [#3259] | 2026-05-05 | 8 | Crate versions not published downstream | No maintainer comment since creation |
| [#3447] | 2026-05-10 | 3 | Nightly E2E failing | No fix PR; timeout extension only |

**High‑priority attention needed**:
- **#3259** (crates.io release) – directly blocks the open‑source ecosystem from using recent IronClaw improvements.
- **#3447** (E2E stability) – a broken pipeline reduces confidence in all future merges.
- **#3564** (wallet signing security) – will likely block PR #3256 and requires architectural decision from maintainers.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-05-13

## Today’s Overview
The project saw very high activity with **30 pull requests updated** (28 merged/closed, 2 open) and **1 open issue** touching a critical response-hang bug. A new release (v2026.5.12) was shipped yesterday, introducing a memory settings tab refactor, Dreaming content display, and UI polish. The large number of merged PRs – including many long‑standing fixes from March – signals both a strong development cadence and a concerted effort to clear technical debt. Overall project health is robust, though one ongoing user‑facing bug requires resolution.

## Releases
- **LobsterAI 2026.5.12** (released 2026-05-12)  
  Highlights:  
  - Refactored memory settings tab and added Dreaming content display ([PR #1943](https://github.com/netease-youdao/LobsterAI/pull/1943))  
  - Multiple UI updates ([PR #1946](https://github.com/netease-youdao/LobsterAI/pull/1946), and [other](https://github.com/netease-youdao/LobsterAI/pull/))  

No breaking changes or migration notes were announced in the release notes.

## Project Progress
Today **28 PRs were merged/closed**, reflecting both new features and a sweep of older fixes. Key merged contributions include:

### Features
- **Plugin management system** – install (npm/clawhub/git/local), uninstall, enable/disable with advanced config UI ([PR #1963](https://github.com/netease-youdao/LobsterAI/pull/1963))
- **POPO channel session titles** – smart parsing of `direct/group/channel` to display human‑readable names ([PR #1966](https://github.com/netease-youdao/LobsterAI/pull/1966))
- **Dev mode session ID display** – for debugging purposes ([PR #1964](https://github.com/netease-youdao/LobsterAI/pull/1964))
- **UI polish** – artifact icon clarity on low‑res displays, skill list tooltip removal ([PR #1965](https://github.com/netease-youdao/LobsterAI/pull/1965))
- **Legacy URL and docs removal** – cleanup of outdated references ([PR #1967](https://github.com/netease-youdao/LobsterAI/pull/1967))
- **Favorites and navigation** – full‑stack favorites (single/batch), scroll‑to‑bottom, session index jump ([PR #903](https://github.com/netease-youdao/LobsterAI/pull/903))
- **Clone remote‑managed session as local task** ([PR #905](https://github.com/netease-youdao/LobsterAI/pull/905))
- **Standalone speech input** – microphone recording, GLM/Qwen ASR adapters, waveform feedback ([PR #901](https://github.com/netease-youdao/LobsterAI/pull/901))
- **Message sharing** – check‑select, preview, one‑click copy, branded export ([PR #880](https://github.com/netease-youdao/LobsterAI/pull/880))

### Fixes (stale PRs merged today)
- Concurrent token refresh race condition causing zero‑point display ([PR #874](https://github.com/netease-youdao/LobsterAI/pull/874))
- SQLite foreign key enforcement for cascade deletion of messages ([PR #881](https://github.com/netease-youdao/LobsterAI/pull/881))
- Duplicate error messages on `continueSession` failure ([PR #878](https://github.com/netease-youdao/LobsterAI/pull/878))
- Security hardening: URL scheme whitelist for `shell.openExternal` ([PR #877](https://github.com/netease-youdao/LobsterAI/pull/877), [PR #889](https://github.com/netease-youdao/LobsterAI/pull/889))
- IPC channel allowlist in preload bridge ([PR #890](https://github.com/netease-youdao/LobsterAI/pull/890))
- Null‑safe store.getItem to preserve falsy values ([PR #891](https://github.com/netease-youdao/LobsterAI/pull/891))
- Redux immutability violation in `modelSlice` ([PR #892](https://github.com/netease-youdao/LobsterAI/pull/892))
- SQLite disk write exception handling with retry mechanism ([PR #907](https://github.com/netease-youdao/LobsterAI/pull/907))

## Community Hot Topics
The only **open issue** updated today is the primary community concern:

- **[#1849] (open)** – “追问时会出现无限NO_REPLY或者输出几个文字就直接不输出了”  
  *Summary*: User reports that task completion fires prematurely while the model is still generating, leading to a blank page.  
  *Engagement*: 2 comments, updated 2026-05-13.  
  [View issue](https://github.com/netease-youdao/LobsterAI/issues/1849)

Although no PRs attracted high comment counts, the plugin management PR [#1963](https://github.com/netease-youdao/LobsterAI/pull/1963) is a large feature that likely drew community interest. The high volume of merged stale PRs also indicates maintainers are responsive to community‑submitted fixes.

## Bugs & Stability

| Severity | Bug | Status | Notes |
|----------|-----|--------|-------|
| **High** | **Task completed prematurely** – model still outputs but page shows no response (Issue [#1849](https://github.com/netease-youdao/LobsterAI/issues/1849)) | Open, no fix PR yet | Root cause identified as early `complete` event; likely requires coordination between streaming and UI state. |
| Medium | Duplicate error messages on `continueSession` failure ([PR #878](https://github.com/netease-youdao/LobsterAI/pull/878)) | Fixed & merged today | UX improvement – no more double error toasts. |
| Medium | SQLite data loss risk on write failure ([PR #907](https://github.com/netease-youdao/LobsterAI/pull/907)) | Fixed & merged today | Adds exception handling and atomic write. |
| Low | Login token refresh race causing zero points ([PR #874](https://github.com/netease-youdao/LobsterAI/pull/874)) | Fixed & merged today | Critical for billing UI consistency. |
| Low | Multiple security vulnerabilities (URL scheme, IPC, XSS) ([PR #877](https://github.com/netease-youdao/LobsterAI/pull/877), [#889](https://github.com/netease-youdao/LobsterAI/pull/889), [#890](https://github.com/netease-youdao/LobsterAI/pull/890)) | All fixed today | Electron app hardening. |

## Feature Requests & Roadmap Signals
While no explicit feature request issues were updated today, the merged PRs provide strong signals for the next release:

- **Plugin ecosystem maturity** – the new plugin management system ([PR #1963](https://github.com/netease-youdao/LobsterAI/pull/1963)) sets the stage for third‑party extensibility. Likely to be followed by plugin store or documentation.
- **Security monitoring** – the open PR [#1962](https://github.com/netease-youdao/LobsterAI/pull/1962) introduces a hot‑toggle for `nsp-clawguard` security monitoring in Settings, suggesting a proactive security stance.
- **Collaboration enhancements** – favorites, clone‑as‑local-task, and improved POPO titles show continued investment in the “Cowork” (collaborative work) area.
- **Voice input** – the standalone speech flow ([PR #901](https://github.com/netease-youdao/LobsterAI/pull/901)) points toward multimodal interaction.

These features are strong candidates for inclusion in the next minor release.

## User Feedback Summary
- **Pain points**: Issue [#1849](https://github.com/netease-youdao/LobsterAI/issues/1849) is the loudest – users are unable to receive complete responses when asking follow‑ups, causing frustration and work disruption. The fix for duplicate error messages (PR #878) addressed a similar user‑experience annoyance.
- **Use cases**: The range of merged PRs (favorites, remote‑session cloning, speech input, plugin management) shows users are actively using LobsterAI for both personal assistant tasks (speech, memory) and team collaboration (Cowork, IM channels). The high number of stale fixes merged today suggests a positive reception to community contributions.
- **Satisfaction**: The quick turnaround on many March‑era fixes indicates maintainers value stability and security, which should boost user trust.

## Backlog Watch
No significant long‑unanswered issues or PRs remain – the 14 stale PRs from March–April were all merged today. The team appears to be actively clearing the backlog. The next items to watch are:

- **Issue #1849** – the only open issue with recent updates; no fix PR yet, so it may become the next priority.
- **PR #1962** (open) – the nsp-clawguard hot-toggle is still pending merge/feedback.

No other items require maintainer intervention at this time.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

**Moltis Project Digest — 2026-05-13**

---

### 1. Today's Overview
Project activity over the past 24 hours was minimal. Only one new issue was updated (a bug report), while no pull requests were opened or merged, and no new releases were published. This low activity suggests the project may be in a quiet period or maintainers are focusing on other tasks. The single open bug indicates ongoing stability work, but overall project momentum appears subdued.

---

### 2. Releases
No new releases were created in the last 24 hours. The project currently has no tagged releases to report.

---

### 3. Project Progress
No pull requests were merged or closed today. No features or fixes advanced through the PR pipeline in this period.

---

### 4. Community Hot Topics
The only issue active in the last 24 hours is a bug report with zero comments or reactions:

- **[Bug #994 – chat has horizontal scrolling again](https://github.com/moltis-org/moltis/issues/994)**  
  Reported by **vvuk** on 2026-05-13. The user indicates they are on the latest version and have searched for duplicates. This issue has no discussion yet, so community engagement is absent. The underlying need is for a consistent, non-scrolling chat UI that respects viewport width.

Given the lack of comments, there are no current community hot topics.

---

### 5. Bugs & Stability
One bug was reported today. Severity is assessed as **medium** (UI regression that degrades user experience but does not block core functionality).

- **[Bug #994 – chat has horizontal scrolling again](https://github.com/moltis-org/moltis/issues/994)**  
  **Severity:** Medium  
  **Fix PRs:** None yet.  
  The issue appears to be a regression of a previously fixed layout problem. No linked PRs or maintainer responses exist as of this digest.

No crashes or critical regressions were reported.

---

### 6. Feature Requests & Roadmap Signals
No feature requests were submitted or discussed in the last 24 hours. Based on available data, there are no clear signals for upcoming features. The next version may focus on UI stability if the reported scrolling bug is prioritized.

---

### 7. User Feedback Summary
The only user feedback is from the bug report #994, which expresses dissatisfaction with a recurring layout issue. The reporter explicitly indicates they are using the latest version, implying an expectation that the bug should have been fixed. This points to potential frustration with regression quality. No positive feedback or use-case descriptions were recorded today.

---

### 8. Backlog Watch
No long-unanswered issues or PRs were updated or referenced in the last 24 hours. The project backlog appears to be clear of aging items, though the single open issue (#994) has been open for only one day and does not yet warrant maintainer attention flags. Maintainers should monitor it for further user reports.

---

**Project Health Summary:** Low activity; one UI regression bug reported; no community discussion or code changes. Maintainers may need to address the scrolling regression and re-engage the community.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-05-13

## 1. Today's Overview
CoPaw (GitHub: `agentscope-ai/CoPaw`) sees heavy, well-balanced activity today: **24 issues updated** (12 open, 12 closed) and **35 PRs updated** (13 open, 22 merged/closed). A new beta release (v1.1.7-beta.1) shipped, primarily fixing provider and console display issues. Community engagement remains high, with several critical bugs reported and promptly addressed—particularly memory exhaustion and configuration-related crashes. The project is healthy, with clear progress in multi-agent collaboration, MCP OAuth support, and desktop client improvements.

## 2. Releases
**v1.1.7-beta.1** ([Release](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.7-beta.1))
- **Fixes**:
  - VOLCENGINE Provider model handling (@Nioolek)
  - Console text contrast in Plan panel (@xieyxclack)
- **Chore**: Version bump to 1.1.7b1.
- **Breaking Changes**: None noted.
- **Migration Notes**: No specific migration steps required; update via `pip install qwenpaw==1.1.7b1` or pull latest Docker image.

## 3. Project Progress
**22 PRs merged/closed** today, advancing several key areas:

- **Console & UI**:
  - [#4270](https://github.com/agentscope-ai/QwenPaw/pull/4270) – Fix external links not opening in packaged desktop client (replaces `window.open` with `openExternalLink`).
  - [#4268](https://github.com/agentscope-ai/QwenPaw/pull/4268) – Fix data misalignment in TokenUsage trend chart across year boundaries.
  - [#4266](https://github.com/agentscope-ai/QwenPaw/pull/4266) – PluginManager refactoring and code optimization.
  - [#4110](https://github.com/agentscope-ai/QwenPaw/pull/4110) – Chat performance optimization (polling stabilization, lazy rendering).
  - [#4091](https://github.com/agentscope-ai/QwenPaw/pull/4091) – Batch enable/disable for skills in the console.
  - [#4094](https://github.com/agentscope-ai/QwenPaw/pull/4094) – TokenUsage style/code refactoring and time picker fix.

- **MCP & Integrations**:
  - [#4256](https://github.com/agentscope-ai/QwenPaw/pull/4256) – Add OAuth 2.1 PKCE support for remote MCP servers (fixes silent 401 loops).
  - [#4263](https://github.com/agentscope-ai/QwenPaw/pull/4263) – Add timeout for keyring operations to avoid hangs on Linux servers with X11 forwarding.

- **Providers**: Multiple fixes merged including VOLCENGINE model fixes and DashScope config read issues.

- **Security**: [#4267](https://github.com/agentscope-ai/QwenPaw/pull/4267) – macOS file path whitelist with `sandbox-exec` protection for shell commands.

## 4. Community Hot Topics
The most active issues and PRs (by comments/reactions) reveal three key community preoccupations:

1. **Configuration & Provider Glitches** – [#4159](https://github.com/agentscope-ai/QwenPaw/issues/4159) (8 comments) and [#4183](https://github.com/agentscope-ai/QwenPaw/issues/4183) (4 comments) highlight users struggling with provider configs (DashScope not read, custom model prefix pollution). Underlying need: better validation and error messages for provider setup.

2. **Memory & Resource Issues** – [#3932](https://github.com/agentscope-ai/QwenPaw/issues/3932) (6 comments) and [#4265](https://github.com/agentscope-ai/QwenPaw/issues/4265) (4 comments) describe severe memory exhaustion from file reading and log scanning. The `read_file_safe` bug now has a fix PR ([#4272](https://github.com/agentscope-ai/QwenPaw/pull/4272)).

3. **Channel Reliability** – [#2642](https://github.com/agentscope-ai/QwenPaw/issues/2642) (15 comments) reports crashes after PPT generation via DingTalk/etc.; [#4056](https://github.com/agentscope-ai/QwenPaw/issues/4056) (4 comments) describes WeChat message loss. Community wants robust channel lifecycle and error recovery.

## 5. Bugs & Stability
| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **Critical** | [#4265](https://github.com/agentscope-ai/QwenPaw/issues/4265) | Memory exhaustion when reading conversation logs; system freezes, SSH unreachable. | Open; no PR yet. |
| **Critical** | [#4232](https://github.com/agentscope-ai/QwenPaw/issues/4232) | SafeJSONSession drops concurrent writes for same chat; two runs clobber session state. | Open; no PR yet. |
| **High** | [#4260](https://github.com/agentscope-ai/QwenPaw/issues/4260) | File messages sent by AI show blank title and tiny preview in Console. | Open; reproducible. |
| **High** | [#4227](https://github.com/agentscope-ai/QwenPaw/issues/4227) | MCP `stream_http` blocks on 401/other errors until timeout (besides 404). | Open; discussion ongoing. |
| **High** | [#3932](https://github.com/agentscope-ai/QwenPaw/issues/3932) | `read_file_safe` allocates up to 1GB causing MemoryError on low-memory systems. | **Fix PR** [#4272](https://github.com/agentscope-ai/QwenPaw/pull/4272) submitted. |
| **Medium** | [#4257](https://github.com/agentscope-ai/QwenPaw/issues/4257) | Browser management has premature idle timeouts, no crash self-healing, zombie processes. | Open; fix PR [#4254](https://github.com/agentscope-ai/QwenPaw/pull/4254) under review. |

## 6. Feature Requests & Roadmap Signals
- **Pre-made Agent Templates** ([#4259](https://github.com/agentscope-ai/QwenPaw/issues/4259)) – Strong signal to lower entry barriers for non-technical users.
- **Rollback & Collaboration Diary** ([#4258](https://github.com/agentscope-ai/QwenPaw/issues/4258)) – Ability to revert messages and clear memory/actions simultaneously.
- **In-Chat Command Observability** ([#4237](https://github.com/agentscope-ai/QwenPaw/issues/4237)) – See, kill, or extend timeout on running shell commands.
- **Web Chat Pagination** ([#4213](https://github.com/agentscope-ai/QwenPaw/issues/4213)) – Split large conversation history to avoid page freeze.
- **Voice Input for Web Console** ([#4000](https://github.com/agentscope-ai/QwenPaw/issues/4000)) – Community expectation mismatch; likely to be added in next minor release.

These requests align with ongoing PRs: [#4210](https://github.com/agentscope-ai/QwenPaw/pull/4210) (inbox & cron enhancements) and [#4237](https://github.com/agentscope-ai/QwenPaw/issues/4237) (observability). Expect at least template presets and inbox in v1.2.0.

## 7. User Feedback Summary
- **Pain Points**:
  - Configuration fragility (provider model names, DashScope key not picked up).
  - Memory and resource management (30%+ of open issues relate to memory/stability).
  - Channel inconsistencies (WeChat message loss, DingTalk crashes, Matrix ack loops).
  - Multi-agent collaboration complexity (ack mirror loops in Team Rooms – [#4251](https://github.com/agentscope-ai/QwenPaw/issues/4251)).
- **Satisfaction Indicators**: The community actively submits detailed bug reports with logs and expects quick fixes—a sign of high engagement. PRs from first-time contributors indicate healthy onboarding.
- **Use Cases**: Primarily enterprise automation (PPT generation, document reading, shell command execution) and multi-agent team coordination.

## 8. Backlog Watch
| Issue | Created | Last Update | Comments | Status |
|-------|---------|-------------|----------|--------|
| [#3528](https://github.com/agentscope-ai/QwenPaw/issues/3528) – Markdown table auto-wraps with `<br>` | 2026-04-17 | 2026-05-13 | 2 | Open; low maintainer attention. |
| [#2433](https://github.com/agentscope-ai/QwenPaw/issues/2433) – `RemoteProtocolError` on large output | 2026-03-28 | 2026-05-13 | 3 | Closed as invalid but may need re-evaluation. |
| [#2642](https://github.com/agentscope-ai/QwenPaw/issues/2642) – Channel crash after PPT generation | 2026-03-31 | 2026-05-13 | 15 | Closed; root cause not addressed in release notes. |
| [#3690](https://github.com/agentscope-ai/QwenPaw/issues/3690) – DingTalk mention not parsed | 2026-04-22 | 2026-05-13 | 3 | Closed as question; actual fix unclear. |

These issues have either gone stale or were closed without satisfactory resolution. Maintainers should verify if underlying problems persist in current version.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-05-13

## Today's Overview
Project activity remains low, with no new releases or feature work. Two security tracking issues were closed after completing deep AI‑vulnerability audits on the web/control‑plane surfaces and Docker/runtime configurations. Three dependency pull requests (PRs) were updated by dependabot, of which one was merged and two remain open. The overall pulse suggests a maintenance‑focused phase with incremental dependency housekeeping and security verification wrap‑up.

## Releases
No new releases were published today.

## Project Progress
- **Merged/Closed PR:** [#574](https://github.com/qhkm/zeptoclaw/pull/574) – Automated dependency bump for `taiki-e/install-action` from v2.75.17 to v2.75.22 (merged/closed). This keeps CI toolchain provisioning up‑to‑date.
- No feature PRs or human-authored changes were merged.

## Community Hot Topics
Both active issues today are closed and involve security verification passes:
- **[#588](https://github.com/qhkm/zeptoclaw/issues/588)** – “chore(security): continue deep ai‑vulns verification for web/control‑plane surfaces” (1 comment). Focuses on persistent audit artifacts and the strongest candidate vulnerability (unauthenticated HTTP MCP → shell exec). Closed as completed.
- **[#587](https://github.com/qhkm/zeptoclaw/issues/587)** – “chore(security): deep ai‑vulns audit of web/control‑plane surfaces” (1 comment). Similar scope, closed after findings acceptance.

These issues reflect the team’s ongoing commitment to surface‑level security hardening. While engagement is low, the closure indicates that identified risks have been evaluated and accepted or mitigated.

## Bugs & Stability
No bugs, crashes, or regressions were reported today.

## Feature Requests & Roadmap Signals
No feature requests were submitted today. Based on the security audit closure, the next minor version may include tightened MCP endpoint access controls and Docker runtime hardening, but no explicit roadmap signals are present.

## User Feedback Summary
No direct user feedback (comments, reactions, or support requests) appeared in the last 24 hours. The project is currently in a quiet maintenance window with no reported pain points.

## Backlog Watch
No stale or long‑unanswered issues or PRs require maintainer attention. The two open PRs ([#586](https://github.com/qhkm/zeptoclaw/pull/586) and [#585](https://github.com/qhkm/zeptoclaw/pull/585)) are dependency bumps awaiting merge and carry no age concern.

---

*Generated from GitHub data (qhkm/zeptoclaw) for 2026-05-13.*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-05-13

## 1. Today's Overview
Project activity remains very high, with **46 pull requests updated** in the last 24 hours (13 merged/closed, 33 still open) and **5 new issues** (all open). No new releases were published. The development focus is on **provider compatibility fixes** (OpenAI reasoning fields, Gemini CLI flag changes), **matrix channel metadata improvements**, and **infrastructure work** (file rotation, ACP session persistence, gateway SSE broadcasting). The volume of PRs suggests the team is accelerating toward the planned `integration/v0.8.0` release. A significant bug (S1 – workflow blocked) was reported around the onboarding tool selecting the wrong API key type for Codex subscriptions.

## 2. Releases
**No new releases** this period. The latest tagged release remains earlier versions; the `integration/v0.8.0` branch continues to accumulate changes.

## 3. Project Progress
**Merged/closed PRs today (13 total):**

| PR | Summary |
|----|---------|
| [#6608](https://github.com/zeroclaw-labs/zeroclaw/pull/6608) | **`fix(agent): preserve reasoning_content across turns for DeepSeek reasoning models`** – Resolves 400 errors when reasoning content from assistant messages was not forwarded correctly across DeepSeek thinking-mode conversations. Closed. |
| [#2025](https://github.com/zeroclaw-labs/zeroclaw/pull/2025) | **`feat(cron): add lark and feishu delivery targets`** – Extends cron scheduler to support Lark and Feishu as valid delivery channels, including auto-injected context. Closed. |
| [#5938](https://github.com/zeroclaw-labs/zeroclaw/pull/5938) | **`feat(file-management): add independent file rotation and cleanup module`** – Introduces a new workspace crate for file rotation, replacing the single-file append behavior of `RuntimeTraceLogger`. Closed. |
| [#5963](https://github.com/zeroclaw-labs/zeroclaw/pull/5963) | **`feat(file-management): add independent file rotation and cleanup module with size+date policy`** – A refined version of #5938, adding size‑ and date‑based cleanup policies. Closed. |
| Other 9 PRs | Closed without explicit details in the data; likely minor fixes or dependency bumps. |

**Notable open PRs advancing features:**
- [#6602](https://github.com/zeroclaw-labs/zeroclaw/pull/6602) – **ACP session persistence** (SQLite-backed) for editor sessions, targeting `integration/v0.8.0`.
- [#6603](https://github.com/zeroclaw-labs/zeroclaw/pull/6603) – **Supervised-mode tool approval UI** (web frontend) – closes [#6522](https://github.com/zeroclaw-labs/zeroclaw/issues/6522).
- [#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398) – **Integration/v0.8.0 mega‑PR** (draft) uniting schema v3 migration, new providers, and channel updates.

## 4. Community Hot Topics
Issues and PRs with the most engagement (by comment count; PRs had undefined/zero comments in the provided data):

| Item | Comments | Topic |
|------|----------|-------|
| [#6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120) | 2 | **[Bug] Onboarding: choosing OpenAI Codex prompts for OpenAI API key instead** – User reports that the new onboarding tool incorrectly prompts for an OpenAI API key even when the user selects a Codex subscription. This S1 bug blocks the entire workflow for Codex users. |
| [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) | 1 | **[Feature] Comfy Cloud / ComfyUI as shared media provider** – A proposal to integrate ComfyUI backends (including official Comfy Cloud) as first‑class media generation providers, laying groundwork for a future `gen_video` tool. This issue is labelled `needs-maintainer-review`. |

**Underlying need:** Users want flexible provider selection for both conversation and media generation, and the onboarding flow must correctly distinguish between API key types (OpenAI vs. Codex).

## 5. Bugs & Stability
**Bugs reported today (5 issues total, 3 are bugs/regressions):**

| Issue | Severity | Summary | Fix PR exists? |
|-------|----------|---------|----------------|
| [#6120](https://github.com/zeroclaw-labs/zeroclaw/issues/6120) | **S1 – workflow blocked** | Onboarding tool for OpenAI Codex asks for OpenAI API key instead. | Not yet. |
| [#6609](https://github.com/zeroclaw-labs/zeroclaw/issues/6609) | **S2 – degraded behavior** | Matrix outbound attachments (files, images, audio, video) omit `content.info.size` metadata, causing Matrix clients to show size as unknown. | **Yes** – [#6610](https://github.com/zeroclaw-labs/zeroclaw/pull/6610) is open, fixing exactly this. |
| [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) | Enhancement, not a bug | – | – |

**Other bug-fix PRs merged/opened today:**
- [#6608](https://github.com/zeroclaw-labs/zeroclaw/pull/6608) – Fixed DeepSeek reasoning content persistence (merged).
- [#6605](https://github.com/zeroclaw-labs/zeroclaw/pull/6605) – `fix(runtime): load workspace profiles before tool registration` – closes [#6419](https://github.com/zeroclaw-labs/zeroclaw/issues/6419) (open).
- [#6606](https://github.com/zeroclaw-labs/zeroclaw/pull/6606) – `fix(providers): preserve compatible reasoning field` – closes [#6584](https://github.com/zeroclaw-labs/zeroclaw/issues/6584) (open).
- [#6607](https://github.com/zeroclaw-labs/zeroclaw/pull/6607) – `fix(providers): respect explicit provider kind` – closes [#6255](https://github.com/zeroclaw-labs/zeroclaw/issues/6255) (open).
- [#6612](https://github.com/zeroclaw-labs/zeroclaw/pull/6612) – `fix(gateway): cancel turn on WS disconnect to stop forward_fut spin` – closes [#6514](https://github.com/zeroclaw-labs/zeroclaw/issues/6514) (open).
- [#6610](https://github.com/zeroclaw-labs/zeroclaw/pull/6610) – `fix(matrix): include attachment media metadata` – fixes [#6609](https://github.com/zeroclaw-labs/zeroclaw/issues/6609) (open).

Overall stability appears good; bugs are being addressed promptly with matching fix PRs.

## 6. Feature Requests & Roadmap Signals
**New feature requests filed today:**

| Issue | Feature | Priority/Labels | Likely for next version? |
|-------|---------|----------------|--------------------------|
| [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) | **Comfy Cloud / ComfyUI as media generation provider** | P2, needs-maintainer-review | Possibly v0.8.0 – related PRs exist for image gen on RunPod (#6555). |
| [#6604](https://github.com/zeroclaw-labs/zeroclaw/issues/6604) | **Multi‑Agent Support: role-based collaboration, per‑agent tools/skills** | Enhancement (no priority) | Unlikely in immediate next release – large architectural change. |
| [#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613) | **Stronger pairing code (default 32 chars alphanumeric)** | Enhancement | Likely in next minor release – simple config change. |

**PRs indicating roadmap direction:**
- [#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398) – Integration/v0.8.0 gathers schema v3 migration, new providers, channel support, and observability improvements.
- [#6602](https://github.com/zeroclaw-labs/zeroclaw/pull/6602) – ACP session persistence for editor workflows.
- [#6555](https://github.com/zeroclaw-labs/zeroclaw/pull/6555) – Image generation via RunPod ComfyUI.
- [#5838](https://github.com/zeroclaw-labs/zeroclaw/pull/5838) – Webhook retry with exponential backoff (enhancement).
- [#6068](https://github.com/zeroclaw-labs/zeroclaw/pull/6068) – Configurable reply-intent precheck model + timeout.

## 7. User Feedback Summary
**Pain points expressed today:**

- **Onboarding for Codex users is broken** – The tool prompts for an API key type mismatch, blocking the entire workflow (Issue #6120). This is a direct usability regression for anyone connecting a Codex subscription.
- **Weak default pairing code** – Six numeric digits are considered insecure by users; a suggestion to default to 32 alphanumeric characters (Issue #6613) indicates security consciousness.
- **Matrix media metadata missing** – Attachment sizes are not visible in Matrix clients, degrading the user experience for file sharing (Issue #6609). The fix is already in review.
- **Demand for ComfyUI integration** – Users want to leverage remote ComfyUI workflows (including official Comfy Cloud) for media generation, not just for LinkedIn images (Issue #6563).
- **Multi-agent collaboration** – A feature request for role‑based multi‑agent collaboration aligned with OpenClaw’s model (Issue #6604) reflects growing interest in complex team‑style AI workflows.

**Satisfaction signals:** The high volume of PRs and quick bug-fix turnaround (e.g., reasoning field fixes merged same day as issues) suggests an active, responsive development team.

## 8. Backlog Watch
**Issues/PRs needing maintainer attention (older or with special labels):**

| Item | Date Created | Label | Why it matters |
|------|-------------|-------|----------------|
| [#6563](https://github.com/zeroclaw-labs/zeroclaw/issues/6563) | 2026-05-10 | `needs-maintainer-review` | ComfyUI feature request with 1 comment – no maintainer response yet. Unaddressed for 3 days. |
| [#6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398) | 2026-05-05 | Draft, still open | The massive `integration/v0.8.0` PR – 11 days without merge or substantial review comments. |
| [#5838](https://github.com/zeroclaw-labs/zeroclaw/pull/5838) | 2026-04-17 | `needs-author-action` | Webhook retry PR – author has not responded to requested changes for 26 days. |
| [#6068](https://github.com/zeroclaw-labs/zeroclaw/pull/6068) | 2026-04-24 | `needs-author-action` | Configurable precheck PR – author dormant for 19 days. |
| [#6555](https://github.com/zeroclaw-labs/zeroclaw/pull/6555) | 2026-05-09 | `needs-author-action` | RunPod image gen PR – author requested changes, no activity for 4 days. |
| [#6527](https://github.com/zeroclaw-labs/zeroclaw/pull/6527) | 2026-05-08 | `size: M, risk: high, gateway, observability, runtime` | Fix for SSE event broadcasting – open for 5 days without merge, despite being a critical bug. |

**Observation:** Several enhancement PRs are stalled awaiting author action. The `needs-maintainer-review` label on #6563 indicates the maintainers have not yet triaged the ComfyUI feature request, which could become a popular addition. The draft v0.8.0 integration PR (#6398) is large and may benefit from incremental review.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*