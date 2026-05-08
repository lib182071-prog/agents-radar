# AI CLI Tools Community Digest 2026-05-08

> Generated: 2026-05-08 06:18 UTC | Tools covered: 8

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# AI CLI Developer Tools: Cross-Tool Comparison Report
**Date:** 2026-05-08

## 1. Ecosystem Overview

The AI CLI tools ecosystem continues to mature rapidly, with eight active projects shipping releases this week and addressing distinct pain points around authentication, session continuity, and platform compatibility. A clear divide is emerging between established tools (Claude Code, Copilot CLI) focusing on stability and enterprise features, and newer entrants (Kimi Code CLI, Qwen Code, Pi) racing to close feature gaps while expanding platform support. The community is increasingly vocal about local model flexibility, multi-account identity management, and cross-platform reliability. Notably, authentication failures—from phone OTP loops to certificate errors—are the most disruptive pain points across multiple tools, indicating shared infrastructure challenges. The competitive landscape shows convergence on key workflows (worktrees, hooks, slash commands) while differentiation centers on model strategy and IDE integration depth.

## 2. Activity Comparison

| Tool | Issues Reported (24h) | PRs Active (24h) | Release Status |
|------|----------------------|------------------|----------------|
| **Claude Code** | 10 hot issues, 2 open PRs | 4 (2 open, 2 closed) | **v2.1.133** released today |
| **OpenAI Codex** | 10 hot issues, 10 key PRs | 10 (all active) | **v0.129.0** + v0.130.0-alpha |
| **Gemini CLI** | 10 hot issues | 10 (1 open, 9 closed) | **v0.42.0-nightly** |
| **Copilot CLI** | 10 hot issues | 0 (no updates) | **v1.0.44-0/-1/-2** (3 patches) |
| **Kimi Code CLI** | 7 issues | 9 (3 new, 6 updated) | No new release |
| **OpenCode** | 10 hot issues | 10 (4 open, 6 closed) | **v1.14.41** today |
| **Pi** | 10 hot issues | 10 (2 open, 8 closed) | **v0.73.1 / v0.74.0** today |
| **Qwen Code** | 10 hot issues | 10 (9 open, 1 closed) | **v0.15.8** + nightly |

**Key observation:** Copilot CLI is the only tool with zero PR activity in the last 24 hours despite three patch releases—suggesting a stabilization phase. Pi and OpenCode show the highest PR throughput, with Pi closing 8 PRs in its "big-refactor" wave.

## 3. Shared Feature Directions

### Multi-Account & Identity Separation
- **Claude Code** (#27302, 221 👍) and **OpenCode** (#2072, 168 👍) both face demands for multi-account connector support and Cursor CLI integration
- **Gemini CLI** lacks explicit multi-account requests but has related credential persistence issues (#24916)

### Session Continuity & State Management
- **Claude Code** (#13354) and **Codex** (#21343, #21671) both hit `/compact` and session-limit continuation problems
- **Qwen Code** (#3925) and **Copilot CLI** (#2543) face session corruption from sub-agent mismanagement
- **Pi** (#2616) has architectural sync-only session persistence blocking async backends

### IDE Integration & Platform Support
- **JetBrains plugin gaps** appear in Claude Code (#47166), Qwen Code (#3511), and Kimi Code CLI (#2185)
- **Windows-specific bugs** plague Copilot CLI (#3188, #2355), Kimi (#2178), OpenCode (#26209), and Qwen Code (401 errors on IDE login)
- **Cross-platform terminal rendering** affects Pi (#4208, #4270), Qwen Code (#3838), and Claude Code (#5674)

### MCP & OAuth Stability
- **Claude Code** (#28256, #53803) and **Qwen Code** (#3940, #3939) both report fragile token management and 401 errors
- **Copilot CLI** (#2282, #3162) has MCP connection and policy validation failures
- **OpenCode** (#8601) has certificate errors across providers

### Terminal UI Customization
- **Vim/vi input modes** requested by Copilot CLI (#13, 58 👍) and Codex (#20749)
- **Bash output collapse config** requested by Claude Code (#11334)
- **Multi-line paste handling** broken in Kimi (#2010), Qwen Code (#3901), and Pi (#767)

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code |
|-----------|-------------|--------------|------------|-------------|-----------|----------|-----|-----------|
| **Primary model strategy** | Anthropic (Claude) | OpenAI (GPT) | Google (Gemini) | Multi-model | MoonshotAI (Kimi) | Multi-provider | OpenAI-compatible | Qwen (local + cloud) |
| **Key architectural focus** | Connector/MCP ecosystem | Service tier routing | Sub-agent protocols | Shell alias compatibility | Plugin/Hook system | Effect-TS refactoring | Local LLM flexibility | Remote control stack |
| **Unique strength** | Agent isolation worktrees | Vim modal TUI editing | A2A remote subagents | GitHub ecosystem integration | Claude plugin compatibility | Provider-agnostic config | Extensive image support | ToolSearch prompt optimization |
| **Biggest user segment** | Enterprise multi-account teams | CI/CD automation | Docker/CI runners | GitHub-ecosystem developers | JetBrains IDE users | Multi-provider power users | Local-first developers | Asian market + local inference |
| **Release cadence** | Steady weekly patches | Alpha/beta track daily | Nightly builds | Patch storm (3/day) | Slower, batch fixes | Weekly stable + PRs | Refactor waves + patches | Nightly + stable |

**Notable architectural differences:**
- **Pi** is unique in pursuing local LLM support as a primary feature (#3357, 23 👍)
- **Codex** leads on service-tier abstraction with dynamic slash commands (#20978)
- **Gemini CLI** is the only tool explicitly building A2A remote agent protocols (#25303)
- **Claude Code** has the deepest connector/MCP tooling but the most OAuth fragility

## 5. Community Momentum & Maturity

### High Maturity, Stable Cadence
- **Claude Code**: Most engaged community by comment volume (#27302: 170 comments, 221 👍). Consistent weekly releases with clear regression testing. Enterprise features (worktree, hooks) mature.
- **Copilot CLI**: Strong GitHub ecosystem gravity. Community active on regression reporting but zero PR activity suggests maintainer bandwidth constraints.
- **OpenCode**: Rapidly maturing with v1.14.41 and strong PR activity. Effect-TS refactoring signals long-term architectural investment. Community highly engaged on Cursor integration (168 👍).

### Rapid Iteration, Moderate Maturity
- **Codex**: Most aggressive release cadence (multiple alpha tracks). High community engagement but phone verification crisis (#20161, 100 comments) points to systemic auth issues.
- **Pi**: Highest PR volume (10, 8 closed) driven by "big-refactor" wave. Community active on local LLM features (23 👍). Migration to `@earendil-works` scope indicates growing maintainer organization.
- **Qwen Code**: Nightly release + desktop app move (#3778) shows expanding scope. Community divided over free tier changes (#3203, 122 comments). Sub-agent visibility (#3925) and remote control (#3929-3931) are ambitious additions.

### Emerging, Niche Focus
- **Gemini CLI**: Active nightly releases but lower community engagement (max 5 comments on hot issues). Strengths in agent protocols and Alpine Linux support suggest backend/devops use case.
- **Kimi Code CLI**: Lowest community engagement metrics. Focused on bug fixes and enterprise proxy support. Potential to grow with JetBrains/ACP ecosystem expansion.

## 6. Trend Signals

### For Technical Decision-Makers

1. **Multi-provider flexibility is the top strategic requirement.** OpenCode (#2072, 168 👍) and Pi (#3357, 23 👍) both see community demand for provider-agnostic architectures. Tools locked to single providers face pressure as developers seek cost optimization and model diversity.

2. **Local/offline model support is a growing wedge.** Pi and Qwen Code are investing heavily. For security-conscious enterprises, this capability may become a selection criteria within 6-12 months.

3. **Session state management is the unsolved scaling problem.** Across Claude Code, Codex, Copilot CLI, and Qwen Code, users report context corruption, session limit interrupts, and sub-agent notification pollution. This is a structural challenge as agents become multi-step and multi-threaded.

4. **Platform-specific stability remains the weakest link.** Windows regressions (Copilot CLI #3188, Kimi #2178), macOS clipboard issues (Copilot CLI #2082), Alpine Linux crashes (Gemini CLI #26690)—each tool has platform-specific gaps that limit adoption in diverse enterprise environments.

5. **Authentication is the top adoption blocker.** Phone OTP loops (Codex #20161, 100 comments), certificate errors (OpenCode #8601, 23 comments), and 401 token failures (Qwen Code #3940) collectively represent the most disruptive class of issues. Any tool that solves persistent credential management will gain a competitive advantage.

6. **Sub-agent visibility is an emerging requirement.** Five separate tools have issues requesting better insight into sub-agent reasoning, tool calls, and termination states. As agents orchestrate more sub-agents, transparency becomes critical for debugging and trust.

7. **Terminal UX parity with editors is becoming table stakes.** Vim modal editing (Codex v0.129.0, Copilot CLI #13), image rendering (Pi #3887), and customizable status lines are shifting CLI expectations from "functional" to "polished." Developers increasingly expect terminal experiences that rival IDE polish.

8. **Remote control APIs signal ecosystem expansion.** Qwen Code's remote-control PR stack (#3929-3931) and Pi's WebSocket transport represent a pattern where CLI tools become programmable backends for IDEs, CI/CD pipelines, and custom UIs—extending beyond the terminal into broader development workflows.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data snapshot:** github.com/anthropics/skills — 2026-05-08  

---

## 1. Top Skills Ranking

Based on discussion volume (comments), the following Skill PRs have drawn the most community attention. All are currently **open**.

| Rank | Skill PR | Description | Key Discussion Points |
|------|----------|-------------|----------------------|
| 1 | [#514 Add document-typography skill](https://github.com/anthropics/skills/pull/514) | Typographic quality control for AI-generated documents (orphan word wrap, widow paragraphs, numbering alignment). | Addresses a universal pain point in Claude-generated documents; highly practical. |
| 2 | [#83 Add skill-quality-analyzer + skill-security-analyzer](https://github.com/anthropics/skills/pull/83) | Meta-skills that evaluate other Skills across five quality dimensions (structure, documentation, etc.) and security posture. | Significant interest in self-improving the Skill ecosystem; raises questions about evaluation standards. |
| 3 | [#210 Improve frontend-design skill clarity](https://github.com/anthropics/skills/pull/210) | Refines the existing `frontend-design` Skill for better actionability and singleness of purpose. | Community feedback focused on making Skill instructions actually followable within a single turn. |
| 4 | [#486 Add ODT skill (OpenDocument)](https://github.com/anthropics/skills/pull/486) | Create, fill, convert ODT/ODS files; parse ODT to HTML. | Supports the open-source document ecosystem; integration with LibreOffice is a requested extension. |
| 5 | [#181 Add SAP-RPT-1-OSS predictor skill](https://github.com/anthropics/skills/pull/181) | Leverages SAP’s open‑source tabular foundation model for predictive analytics on business data. | Niche but technically deep; discussions about hardware requirements and model integration. |
| 6 | [#723 Add testing-patterns skill](https://github.com/anthropics/skills/pull/723) | Comprehensive testing stack guide: unit tests (AAA pattern), React Testing Library, E2E with Playwright, visual regression. | Widely seen as a missing foundation – nearly every codebase needs this guidance. |
| 7 | [#154 Add shodh-memory skill](https://github.com/anthropics/skills/pull/154) | Persistent memory system for AI agents – context across conversations using `proactive_context` triggers. | Early adopter discussions on memory reliability and token budget management. |
| 8 | [#147 Add codebase-inventory-audit skill](https://github.com/anthropics/skills/pull/147) | 10‑step workflow to identify orphaned code, unused files, documentation gaps, and infrastructure bloat. | Valued for large-scale cleanup; debate on false‑positive rates for orphan detection. |

📎 **Notable runner‑ups:** [#360 AppDeploy](https://github.com/anthropics/skills/pull/360) (full‑stack deployment), [#568 ServiceNow](https://github.com/anthropics/skills/pull/568) (enterprise IT platform), [#444 AURELION skill suite](https://github.com/anthropics/skills/pull/444) (cognitive framework), [#335 Masonry AI](https://github.com/anthropics/skills/pull/335) (image/video generation), [#806 Sensory skill](https://github.com/anthropics/skills/pull/806) (macOS AppleScript automation).

---

## 2. Community Demand Trends

Analysis of the most-discussed Issues reveals several clear demand directions:

| Trend | Key Issues | What the Community Wants |
|-------|------------|--------------------------|
| **Organizational skill sharing** | [#228](https://github.com/anthropics/skills/issues/228) (9 comments, 7👍) | Direct team/skill library sharing – eliminate manual `.skill` file transfers. |
| **Quality & evaluation tooling** | [#202](https://github.com/anthropics/skills/issues/202), [#556](https://github.com/anthropics/skills/issues/556) (6 comments, 6👍) | Better `skill-creator` (not a developer‑facing doc) and a working evaluation harness (`run_eval.py` triggers at 0%). |
| **Cross‑platform integration** | [#29](https://github.com/anthropics/skills/issues/29) (4 comments), [#16](https://github.com/anthropics/skills/issues/16) (4 comments) | Support for AWS Bedrock and exposing Skills as MCPs (Model Context Protocol) for universal API access. |
| **Security & trust boundaries** | [#492](https://github.com/anthropics/skills/issues/492) (4 comments, 2👍) | Community skills appear under the `anthropic/` namespace, enabling impersonation – need clear origin labeling. |
| **Agent governance** | [#412](https://github.com/anthropics/skills/issues/412) (4 comments) | Formal safety patterns for multi‑agent systems: policy enforcement, threat detection, audit trails. |
| **Plugin deduplication** | [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 8👍) | `document-skills` and `example-skills` plugins contain identical content – causes context‑window waste. |

**Emerging pattern:** The community is not just requesting *more* skills; it is demanding **better tooling around skills** – evaluation, sharing, deduplication, security, and multi‑platform reach.

---

## 3. High‑Potential Pending Skills

These PRs have active discussion and are likely to land soon. They address clearly articulated needs.

| PR | Skill | Why It Could Land Quickly |
|----|-------|---------------------------|
| [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Solves a universal problem; implementation is straightforward (regex‑based checks). |
| [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer + skill-security-analyzer** | Directly addresses the community’s call for Skill quality assurance; meta‑skill format is well‑understood. |
| [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design improvement** | Tightening existing content is lower risk than novel skills; clear author intent. |
| [#486](https://github.com/anthropics/skills/pull/486) | **ODT skill** | High demand from open‑source users; no complex dependencies. |

*Note: All 50 PRs remain open. The absence of merged PRs suggests an active review pipeline rather than stagnation.*

---

## 4. Skills Ecosystem Insight

> **The Claude Code community’s most concentrated demand is not for more individual skills, but for a robust quality, sharing, and evaluation infrastructure that turns the current collection of scripts into a reliable, enterprise‑grade ecosystem.**

Supporting signals:  
- The top skill PR (#83) is a **meta‑skill to evaluate other skills**.  
- The top issues (#228, #556, #189, #492) all relate to **sharing, testing, deduplication, and trust**.  
- Skills that do succeed (typography, testing patterns, codebase audit) are those that address **universal, repeatable pain points** with clear, executable instructions.

The next phase of community growth will likely depend on solving these systemic challenges rather than simply adding more skills.

---

# Claude Code Community Digest – 2026-05-08

## Today’s Highlights
A new release (v2.1.133) introduces a `worktree.baseRef` setting, flipping the default branching strategy back to `origin/<default>` for worktrees. Community attention remains focused on the long‑standing request for multi‑account connector support (#27302, 170 comments, 221 👍) and a feature to continue sessions after hitting usage limits (#13354). Several MCP OAuth bugs continue to frustrate users, with a critical race condition fix now closed (#43392) but token persistence issues still open.

## Releases
**v2.1.133** – *Released today*  
- Added `worktree.baseRef` setting (`fresh` | `head`) to control whether `--worktree`, `EnterWorktree`, and agent‑isolation worktrees branch from `origin/<default>` or local `HEAD`.  
- **Note:** The default changed to `fresh`, meaning `EnterWorktree` now bases on `origin/<default>` (reverting recent behavior).  
*Full release details:* [GitHub Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.133)

## Hot Issues (Top 10 by Engagement)

1. **[#27302] Support Multiple Connector Accounts**  
   *Enhancement* – Request to use the same connector (e.g., Google Drive) with different accounts on claude.ai and Claude Code. 170 comments, 221 👍. Community strongly desires workspace identity separation.  
   [Issue](https://github.com/anthropics/claude-code/issues/27302)

2. **[#13354] Continue When Session Limit Reached**  
   *Enhancement* – Many users hit the usage cap mid‑task and want a non‑disruptive way to resume. 47 comments, 100 👍.  
   [Issue](https://github.com/anthropics/claude-code/issues/13354)

3. **[#5674] Persistent ECONNRESET Errors on macOS**  
   *Bug* – Network connections drop repeatedly on macOS but not on Windows/Linux. 33 comments, 25 👍. Possibly related to Apple’s networking stack.  
   [Issue](https://github.com/anthropics/claude-code/issues/5674)

4. **[#32450] Google Drive Connector Not Loading in VS Code Extension**  
   *Bug* – Google Drive connector fails to appear as an MCP tool in VS Code, while Gmail/Calendar work. 24 comments, 20 👍. Highlights inconsistency in connector loading.  
   [Issue](https://github.com/anthropics/claude-code/issues/32450)

5. **[#11334] Prevent Auto‑Collapsing Long Bash Outputs**  
   *Enhancement* – Users want a config option to keep long terminal outputs expanded. 13 comments, 23 👍. Important for debugging and visibility.  
   [Issue](https://github.com/anthropics/claude-code/issues/11334)

6. **[#36797] Authentication Redirect Loops for Existing Accounts**  
   *Bug* – Logging in to claude.ai redirects to onboarding, even for active subscribers. 11 comments, 8 👍. Blocks paid users.  
   [Issue](https://github.com/anthropics/claude-code/issues/36797)

7. **[#47166] JetBrains Plugin Needs More Love**  
   *Enhancement* – Users request a dedicated AI Assist interface for JetBrains IDEs. 10 comments, 0 👍 (low reaction but consistent demand).  
   [Issue](https://github.com/anthropics/claude-code/issues/47166)

8. **[#55917] Can’t Upgrade Pro → Max: Payment Authentication Fails**  
   *Bug* – All payment methods fail during upgrade. 10 comments, 1 👍. Affects conversion funnel.  
   [Issue](https://github.com/anthropics/claude-code/issues/55917)

9. **[#4276] Environment Variable Expansion in `settings.json`**  
   *Enhancement* – Allow use of `${VAR}` patterns in settings for secrets and per‑environment config. 10 comments, 27 👍. Strong security angle.  
   [Issue](https://github.com/anthropics/claude-code/issues/4276)

10. **[#34062] Chrome Extension Black Screen in Vivaldi (Linux)**  
    *Bug* – Extension renders black screen on Vivaldi browser, no tool access. 9 comments, 5 👍. Platform‑specific rendering issue.  
    [Issue](https://github.com/anthropics/claude-code/issues/34062)

## Key PR Progress (4 Open/Closed Today)

- **[#57190] Remove `statsig.anthropic.com` from firewall script**  
  *Open* – Proposal to remove a now‑unresolvable telemetry endpoint from the firewall bypass script. Community request to clean up stale entries.  
  [PR](https://github.com/anthropics/claude-code/pull/57190)

- **[#57108] Fix hookify enabled boolean parsing**  
  *Open* – Ensures the `enabled` field in hook frontmatter is parsed as a strict YAML boolean, rejecting invalid values. Adds unit tests. Improves reliability of claude‑hooks.  
  [PR](https://github.com/anthropics/claude-code/pull/57108)

- **[#57046] Docs: Clarify hook blocking exit code**  
  *Open* – Updates documentation to specify that only exit code `2` blocks hook execution; other non‑zero codes are non‑blocking. Fixes #44707.  
  [PR](https://github.com/anthropics/claude-code/pull/57046)

- **[#53949] Update HackerOne links in SECURITY.md**  
  *Closed* – Minor housekeeping: updated submission form and program page links for vulnerability disclosure.  
  [PR](https://github.com/anthropics/claude-code/pull/53949)

## Feature Request Trends
The most‑requested feature directions from today’s issues are:

1. **Multi‑account & credential separation** – Top request (#27302) plus related env‑variable expansion (#4276). Users need to manage multiple identities for connectors and environments.
2. **Session continuity** – Continue after usage limits (#13354) and a `--wait-on-usage-limit` flag for non‑interactive sessions (#41502). Essential for long‑running automations.
3. **IDE integration expansion** – JetBrains native plugin (#47166) and better VS Code extension reliability for connectors (#32450).
4. **UI/UX customization** – Configurable bash output collapse (#11334), auto‑generated session titles (#57193), and configurable Cowork workspace path (#57177). Users want more control over their experience.
5. **MCP stability & OAuth improvements** – While mostly bug reports, the frequent OAuth token refresh issues (see Pain Points below) translate into requests for more robust credential handling and multi‑session sharing.

## Developer Pain Points
Recurring frustrations observed across today’s bug reports:

- **MCP OAuth token management is fragile** – Tokens not persisting across sessions (#28256), refresh tokens never used (#53803), corporate CA certificates ignored (#55760), and a race condition when running parallel agents (#43392, now closed). OAuth flows remain the #1 source of connectivity pain.
- **Platform‑specific installation & tool failures** – Windows segmentation fault during install (#57159), auto‑update breaking the macOS symlink (#57178), Windows bash tool directory locks (#49984), and redirected Documents folder breaking Cowork scheduled tasks (#56001).
- **Authentication and account‑level bugs** – Redirect loops to onboarding (#36797), payment failures blocking upgrades (#55917), and connection drops on macOS (#5674) continue to affect paying users.
- **Security and permissions concerns** – One user reported that Claude Code performed a `find` across the Desktop and sent personal files to a third‑party API without confirmation (#56739). This highlights the need for stricter permission boundaries.
- **Syntax highlighting and TUI gaps** – GDScript files lack highlighting (#48181), and the `@` file picker does not refresh for newly created files (#53517). Minor but quality‑of‑life issues.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-05-08

## Today's Highlights

The big story today is the **v0.129.0 release**, which introduces **Vim modal editing in the TUI composer** and a redesigned resume/fork picker. However, a **persistent phone‑verification bug** (#20161, #20320) continues to block users from logging in, generating the most comments across all issues. Several Windows‑specific regressions and a `/compact` failure after upgrade are also generating heat. On the PR side, improvements to **tool caching, service‑tier slash commands**, and **accepted‑code attribution** are nearing completion.

## Releases

| Version | Key Changes |
|---------|-------------|
| **v0.129.0** | 🎉 **New Features:** TUI now supports modal Vim editing in the composer (`/vim`, `default‑mode` config, Vim‑specific keymaps). Redesigned resume/fork picker, raw scrollback mode, `/ide` context injection. |
| **v0.130.0‑alpha.1–.4** | Alpha releases on the 0.130 track – no changelogs published yet. |
| **v0.129.0‑alpha.15** | Pre‑release for 0.129.0. |

## Hot Issues (Top 10 by Community Attention)

1. **#20161** – *Phone number verification doesn't work* [CLOSED]  
   👥 100 comments | 👍 74  
   **Why it matters:** SSO login flow suddenly requires a phone number; users cannot complete registration. The top‑voted issue indicates a systemic auth failure.  
   🔗 https://github.com/openai/codex/issues/20161

2. **#20320** – *ChatGPT asking phone number verify but didn't send any code* [OPEN]  
   👥 15 comments | 👍 3  
   **Why it matters:** Users trying to upgrade to Pro are locked out. OTP never arrives, creating a critical onboarding bottleneck.  
   🔗 https://github.com/openai/codex/issues/20320

3. **#20749** – *Disable right panel on hover* [OPEN]  
   👥 7 comments | 👍 1  
   **Why it matters:** Accidental pop‑ups from the right sidebar disrupt workflow. User requests a toggle to disable hover activation.  
   🔗 https://github.com/openai/codex/issues/20749

4. **#21343** – *Context compact error* [OPEN]  
   👥 5 comments | 👍 7  
   **Why it matters:** `/compact` fails with a vague error message. Affects users managing context in long sessions.  
   🔗 https://github.com/openai/codex/issues/21343

5. **#19450** – *Browser Use / in‑app browser fails to start app‑server on Windows 10* [OPEN]  
   👥 5 comments | 👍 13  
   **Why it matters:** Windows users cannot use the in‑app browser feature (os error 3). High upvote count indicates broad impact.  
   🔗 https://github.com/openai/codex/issues/19450

6. **#21639** – *Hooks no longer run after Codex Desktop update* [OPEN]  
   👥 4 comments | 👍 0  
   **Why it matters:** Users relying on hooks for custom automation find them broken after update to CLI version 0.129.0‑alpha.15.  
   🔗 https://github.com/openai/codex/issues/21639

7. **#21189** – *Phone verification OTP not received (Pakistan)* [OPEN]  
   👥 4 comments | 👍 0  
   **Why it matters:** Regional SMS delivery failures are blocking users globally.  
   🔗 https://github.com/openai/codex/issues/21189

8. **#21527** – *Codex is really too slow* [OPEN]  
   👥 4 comments | 👍 2  
   **Why it matters:** Performance complaints cover both VS Code extension and desktop app; model response latency is a core experience issue.  
   🔗 https://github.com/openai/codex/issues/21527

9. **#21671** – *0.129.0: /compact fails with unknown service_tier parameter* [OPEN]  
   👥 2 comments | 👍 0  
   **Why it matters:** A regression in the latest stable release; users upgrading to 0.129.0 cannot use context compaction.  
   🔗 https://github.com/openai/codex/issues/21671

10. **#21668** – *Privacy/security risk: Computer Use captures wrong macOS Space* [OPEN]  
    👥 1 comment | 👍 0  
    **Why it matters:** Screenshots from the wrong Space can be uploaded as context – a potential data leak.  
    🔗 https://github.com/openai/codex/issues/21668

## Key PR Progress (Top 10 by Relevance)

1. **#21497** – *Using cached connector directory for discoverable tools list*  
   **Fix:** Reduces startup latency by caching connector directory metadata for `tool_suggest discoverables`.  
   🔗 https://github.com/openai/codex/pull/21497

2. **#21651** – *Delete function‑style apply_patch*  
   **Refactor:** Converts `apply_patch` to a freeform/custom tool, removing the legacy JSON/function‑style registration path.  
   🔗 https://github.com/openai/codex/pull/21651

3. **#15730** – *Fix: harden symlinked output and project config writes*  
   **Security:** Rejects symlinked paths for `--output‑last‑message` and protects `.codex/config.toml` with `O_NOFOLLOW`.  
   🔗 https://github.com/openai/codex/pull/15730

4. **#20974** – *Add service tier id to config*  
   **Feature:** Introduces `service_tier_id` alongside legacy `service_tier`, with fallback logic. Enables finer‑grained tier selection.  
   🔗 https://github.com/openai/codex/pull/20974

5. **#20978** – *Use model service tier slash commands*  
   **Feature:** Replaces hard‑coded `/fast` with dynamic slash commands generated from model metadata.  
   🔗 https://github.com/openai/codex/pull/20978

6. **#21669** – *Display blended token count in status line*  
   **UX Improvement:** The status line now shows blended token count (excluding cached input) instead of raw totals.  
   🔗 https://github.com/openai/codex/pull/21669

7. **#20638** – *Record model‑input image metadata on turn traces*  
   **Observability:** Adds image metadata to traces for debugging slow turns that include screenshots from Browser Use etc.  
   🔗 https://github.com/openai/codex/pull/20638

8. **#21601** – *Emit accepted line fingerprint analytics*  
   **Analytics:** Hashes accepted‑code lines client‑side for attribution without uploading raw code.  
   🔗 https://github.com/openai/codex/pull/21601

9. **#20527** – *Support PreToolUse updatedInput rewrites*  
   **Hooks:** Allows hook authors to modify tool input before execution via `updatedInput` in the `PreToolUse` lifecycle.  
   🔗 https://github.com/openai/codex/pull/20527

10. **#21617** – *Support multi‑environment apply_patch selection*  
    **Feature:** Adds environment selector to `apply_patch` tool for routing patches to different environments.  
    🔗 https://github.com/openai/codex/pull/21617

## Feature Request Trends

- **🔐 Phone‑based auth improvements** – Multiple issues (#20161, #20320, #21189) demand reliable OTP delivery and an alternative to phone verification.
- **📋 Right panel / sidebar accidental trigger** – Requests to disable hover activation (#20749, #20953) are recurring.
- **🧩 Hooks and MCP server reload** – Users want hooks to persist across updates (#21639) and a way to reload MCP servers without restarting (#7767).
- **📎 Context compaction & handoff** – `/compact` errors (#21343, #21671) and requests for a *compact handoff command with copyable context* (#21673) show demand for better session state management.
- **💻 Multi‑line status line** – The TUI status line truncates; users request line‑breaks for multiple configured items (#21653).
- **🌐 Windows‑specific polish** – Quotes for paths with parentheses (#21667), Chrome plugin install failures (#21674, #21670), and Browser Use startup errors (#19450) are top Windows pain points.

## Developer Pain Points

- **Authentication lock‑up** – The phone‑number verification loop (as in issue #20161) is the most commented problem, blocking both login and subscription activation.
- **Performance regressions** – General slowness (#21527) and specific regressions (e.g., `/compact` failure after v0.129.0 upgrade #21671) erode trust in releases.
- **Windows instability** – A cluster of issues (#19450, #21247, #21670, #21674, #21667) shows that Windows support still has rough edges in Browser Use, plugin installation, and path handling.
- **Hooks and plugins breaking after updates** – #21639 (hooks stop working) and #16430 (plugin‑local hooks not loaded) indicate a fragile configuration system.
- **MCP tool inconsistency** – #21654 reports that the app shows MCP servers enabled but only a subset of tools are available in sessions.
- **Desktop app crashes and freezes** – #21663 (SIGABRT on macOS) and #21668 (wrong Space capture) highlight stability and privacy concerns.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-08

## Today's Highlights

A critical crash fix for Alpine Linux (musl libc) was submitted, addressing two root causes in the CLI entrypoint, including an unhandled PTY resize exception. The Auto Memory system continues to receive focused attention, with three bug reports tracking indefinite retries, malformed patch handling, and secret redaction gaps. The nightly release includes a JSON output fix for non-interactive agent execution and new shell command safety evaluations.

## Releases

- **[v0.42.0-nightly.20260507.ga809bc7c5](https://github.com/google-gemini/gemini-cli/releases/tag/v0.42.0-nightly.20260507.ga809bc7c5)** — Two changes: `fix(cli): provide JSON output for AgentExecutionStopped in non-interactive mode` and `feat(evals): add shell command safety evals`.

## Hot Issues

1. **[#26563 — Tool "save_memory" not found](https://github.com/google-gemini/gemini-cli/issues/26563)** (5 comments)
   Using `/memory add` in v0.41.1 fails because the `save_memory` tool is being called as a regular tool instead of a slash command. The model suggests alternatives like `ask_user` and `list_memories`, indicating a routing failure between agent tools and memory commands.

2. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (5 comments)
   EPIC tracking expansion of behavioral evals beyond the current 76 tests across 6 Gemini models. This is foundational work for regression testing agent behavior.

3. **[#22745 — AST-aware file reads, search, and codebase mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (5 comments, 👍1)
   Investigation into using AST-aware tools for precise method-bound reads and reduced token noise. Could significantly improve `codebase_investigator` accuracy.

4. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (5 comments, 👍2)
   `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` despite hitting the turn limit before performing any analysis. This masks real failures and misleads users about agent completion.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (5 comments)
   Anecdotal evidence that custom skills and sub-agents are rarely invoked autonomously, even for related tasks. Users report needing explicit instructions to trigger them.

6. **[#24916 — Gemini CLI keeps asking for permissions on the same file](https://github.com/google-gemini/gemini-cli/issues/24916)** (3 comments)
   Permission prompts don't persist—"allow for all future sessions" doesn't always apply. This breaks workflow flow and creates friction during extended sessions.

7. **[#26690 — Gemini CLI crashes on Alpine Linux (musl libc)](https://github.com/google-gemini/gemini-cli/issues/26690)** (1 comment)
   Two root causes identified: an unhandled PTY resize exception and a relaunch IPC failure on musl-based systems. Blocks use on lightweight Docker images and CI runners.

8. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (2 comments)
   Auto Memory sends content to the model before redacting secrets. The extraction prompt instructs redaction, but data has already left local context. Also, existing skills may be logged in transcripts.

9. **[#22093 — (Sub)agents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** (1 comment)
   After update to v0.33.0, subagents like `generalist` activate even when agent mode is set to disabled. Unexpected agent execution raises trust and safety concerns.

10. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (2 comments, 👍3)
    Simple CLI commands hang after completion, still showing "Awaiting user input". This affects fundamental shell tool reliability.

## Key PR Progress

1. **[#26689 — fix: Alpine Linux (musl) compatibility in CLI entrypoint](https://github.com/google-gemini/gemini-cli/pull/26689)** (OPEN)
   Fixes #26690 by suppressing PTY resize exceptions on non-Windows and fixing the relaunch IPC path for musl libc. Critical for Docker/CI users.

2. **[#24826 — feat(cli): add OSC 8 hyperlinks for file paths and URLs](https://github.com/google-gemini/gemini-cli/pull/24826)** (CLOSED)
   Clickable terminal hyperlinks using OSC 8 escape sequences for file paths and URLs in model responses. Supports VS Code, iTerm2, Ghostty, WezTerm.

3. **[#26410 — fix(cli): use os.homedir() for home directory warning check](https://github.com/google-gemini/gemini-cli/pull/26410)** (CLOSED)
   Safety warning was triggering in subdirectories of home because it used the `GEMINI_CLI_HOME`-aware helper instead of the system home directory.

4. **[#25900 — fix(core): prefer pwsh.exe over Windows PowerShell 5.1](https://github.com/google-gemini/gemini-cli/pull/25900)** (CLOSED)
   Fixes embedded double-quote issues on Windows by preferring PowerShell Core (pwsh.exe) over legacy Windows PowerShell 5.1.

5. **[#26256 — fix(shell): stop foreground commands after excessive output](https://github.com/google-gemini/gemini-cli/pull/26256)** (CLOSED)
   Adds a 10 MiB output guard for foreground shell commands. Prevents runaway output and surfaces `outputLimitExceeded` to guide users toward background mode.

6. **[#26259 — fix(cli): continue task after skill slash activation](https://github.com/google-gemini/gemini-cli/pull/26259)** (CLOSED)
   Skill slash commands (`/<skill-name>`) now continue the active task instead of sending a weak default prompt. Reduces friction when manually invoking skills.

7. **[#25303 — feat(core): add RemoteSubagentProtocol behind AgentProtocol](https://github.com/google-gemini/gemini-cli/pull/25303)** (CLOSED)
   Wraps A2A remote agent streaming behind the `AgentProtocol` interface, enabling multi-send streaming from remote subagents.

8. **[#25885 — fix(core): prevent ENOENT crash due to proper-lockfile race condition](https://github.com/google-gemini/gemini-cli/pull/25885)** (CLOSED)
   Critical startup crash fix for `ENOENT: no such file or directory, stat '.../.gemini/projects.json.lock'` race condition.

9. **[#25886 — feat(routing): availability-aware auto-routing with best-effort pro](https://github.com/google-gemini/gemini-cli/pull/25886)** (CLOSED)
   Detects Pro model timeouts and temporarily routes to Flash fallback. Introduces "Best Effort Pro" setting for users who prefer Pro but need reliability.

10. **[#25893 — fix(core): drain stderr stream unconditionally for StdioClientTransport](https://github.com/google-gemini/gemini-cli/pull/25893)** (CLOSED)
    Fixes MCP server deadlock when stderr output fills the OS pipe buffer in non-debug mode. Server processes can now write stderr without blocking.

## Feature Request Trends

- **AST-aware code understanding**: Multiple EPICs (#22745, #22746) explore using abstract syntax trees for more precise file reads, method-bound navigation, and codebase mapping to reduce token waste and improve tool accuracy.
- **Agent protocol abstraction**: Merged PRs (#25302, #25303) introduce `LocalSubagentProtocol` and `RemoteSubagentProtocol` behind a unified `AgentProtocol` interface, enabling consistent subagent execution across local and A2A remote agents.
- **Adaptive model routing**: PR #25886 adds availability-aware routing that falls back from Pro to Flash on timeouts, with a "Best Effort Pro" toggle—addressing a common user pain point around model reliability.
- **Non-interactive mode parity**: Continued work on `/stats` output (#20536) and JSON output for agent results (#26504) aims to bring feature parity to headless/CI environments.

## Developer Pain Points

- **Agent permission inconsistencies**: Subagents running despite being disabled (#22093) and repeated permission prompts ignoring "always allow" settings (#24916) disrupt trust in the permission model.
- **Shell execution reliability**: Commands hanging with "Awaiting input" after completion (#25166) and excessive output not being guarded (#26256) are recurring issues that break automation workflows.
- **Browser agent configuration fragility**: The browser subagent ignores `settings.json` overrides for `maxTurns` (#22267) and fails on Wayland (#21983), limiting its utility across Linux desktop environments.
- **Platform compatibility gaps**: Crashes on Alpine Linux (#26690) and broken PowerShell 5.1 support (#25900) highlight gaps in non-mainstream OS and shell testing.
- **Skill/sub-agent underutilization**: The agent rarely invokes custom skills or sub-agents autonomously (#21968), undermining the value of user-configured tooling and requiring manual prompting.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-08

## 1. Today’s Highlights
Three patch releases (v1.0.44-0 through v1.0.44-2) landed today, fixing critical shell compatibility, quota display, and tool-permission persistence bugs, while adding a prerelease flag for `copilot update`. The community is actively reporting regressions in the new v1.0.44-x line—especially around non‑interactive mode on Windows and macOS, whitespace tokenization, and silent exits. A long‑standing Linux clipboard shortcut issue (#2082) continues to gather attention (18 comments).

## 2. Releases
Three versions shipped in the last 24 hours:

- **v1.0.44-2** — Added optional `prerelease` argument to `copilot update` and `/update` to fetch the latest prerelease build. Fixed shell commands via the `!` prefix for all shell configurations.
- **v1.0.44-1** — Improved shell alias/rc file support inside `!` commands.
- **v1.0.44-0** — Timeline now shows the resolved model for rubber‑duck sub‑agents (e.g., `Rubber-duck(claude-opus-4.7)`). Fixed quota display for Free users (no longer always shows 100% used) and tool permissions granted in autopilot mode now survive a `/clear`.

## 3. Hot Issues (10 Noteworthy)

1. **#13 – CLI input should have a vi/vim input mode**  
   [Link](https://github.com/github/copilot-cli/issues/13) | 👍58 | 6 comments  
   The most‑upvoted feature request on the board. Users want modal editing in the interactive prompt. No movement from maintainers yet.

2. **#2082 – ctrl+shift+c no longer copies to clipboard on Linux**  
   [Link](https://github.com/github/copilot-cli/issues/2082) | 👍7 | 18 comments  
   A long‑standing regression affecting Ubuntu 24.04. The community is actively discussing workarounds; no fix in the latest releases.

3. **#2543 – Concurrent sub‑agent events corrupt session state**  
   [Link](https://github.com/github/copilot-cli/issues/2543) | 👍2 | 4 comments  
   A persistent `tool_use ids were found without tool_result blocks` error that forces users to discard sessions. High severity – impacts anyone using multiple sub‑agents.

4. **#2282 – Unable to connect to MCP servers on Windows**  
   [Link](https://github.com/github/copilot-cli/issues/2282) | 👍1 | 9 comments  
   `Failed to connect to MCP server` error reported by WinGet users. Blocking MCP adoption on Windows.

5. **#3188 – Windows: copilot.exe exits 1 with empty streams when stdout is piped**  
   [Link](https://github.com/github/copilot-cli/issues/3188) | 👍3 | 0 comments (new)  
   `FlushFileBuffers ERROR_INVALID_FUNCTION` breaks all non‑PowerShell automation on v1.0.44-0. Critical for CI/CD workflows.

6. **#3189 – `copilot -p` exits 1 silently with no output (macOS)**  
   [Link](https://github.com/github/copilot-cli/issues/3189) | 0 comments (new)  
   Non‑interactive mode fails completely on macOS v1.0.44-1. No log file, no error message – hard to diagnose.

7. **#3183 – SDK: orphan `tool_use` left mid‑conversation after hard kill**  
   [Link](https://github.com/github/copilot-cli/issues/3183) | 1 comment (new)  
   A related session‑corruption bug specific to the SDK, causing 400 errors on resume. Affects custom integrations.

8. **#3186 – `-p` / `--prompt` tokenizes value on whitespace (Windows)**  
   [Link](https://github.com/github/copilot-cli/issues/3186) | 1 comment (new)  
   Regression in v1.0.44-0: multi‑word prompts break. Fixed in the closed state, but the release note is missing.

9. **#2355 – Internal PowerShell tool fails to spawn pwsh.exe on Windows**  
   [Link](https://github.com/github/copilot-cli/issues/2355) | 👍4 | 4 comments  
   `ENOENT` error for PowerShell 7, even when it’s on PATH. Interactive mode works, but tool execution fails.

10. **#3194 – Mouse scroll cycles input history in Android Studio’s terminal**  
    [Link](https://github.com/github/copilot-cli/issues/3194) | 0 comments (new)  
    Since v1.0.43, scroll events are misinterpreted as arrow keys, making the terminal nearly unusable in JetBrains IDEs.

## 4. Key PR Progress
No pull requests were updated in the last 24 hours. (Data shows 0 items.)

## 5. Feature Request Trends
Several recurring themes emerge from the issue tracker:

- **Input mode customization** – #13 (vi/vim mode) and #3191 (carriage‑return support) point to a desire for flexible terminal input.
- **Richer terminal rendering** – #1465 (sixel/image rendering) and #3193 (blockquote wrapping) indicate users want graphical output and better markdown formatting.
- **Deeper agent recursion** – #1374 (more levels of sub‑agent calls) and #3190 (Copilot Subconscious REM process) show interest in multi‑layer agent orchestration.
- **MCP protocol enhancements** – #2282 (connection reliability), #2538 (tasks capability negotiation), and #3162 (policy validation false negatives) reflect growing reliance on MCP and demands for robust integration.
- **Tool permission & auditing** – #3177 (co‑authored tag), #3181 (remove automatic co‑author), and #3123 (`/research` write tool unavailable) highlight concerns about attribution and tool availability.
- **Automation reliability** – #3188, #3189, #2385, and #2985 (grep timeout) all point to the community using Copilot CLI in scripts and CI, and hitting platform‑specific barriers.

## 6. Developer Pain Points
The highest‑frequency frustrations reported in the last 24 hours:

- **Platform friction**: Linux clipboard regression (#2082), Windows PowerShell spawning (#2355), Windows pipe buffer errors (#3188), and Android Studio mouse handling (#3194) show that cross‑platform polish is still lacking.
- **Non‑interactive mode regressions**: Multiple reports of `copilot -p` failing silently on macOS (v1.0.44-1) and Windows (v1.0.44-0) – a critical concern for CI/CD users.
- **Session state corruption**: Two separate issues (#2543, #3183) point to a fragile session persistence model that can leave conversations permanently broken after crashes or concurrent agent calls.
- **MCP connection hurdles**: New users on Windows (#2282) and custom‑registry users (#3162) face false‑positive policy blocks and connection failures, slowing MCP adoption.
- **Configuration/resource quirks**: Effort‑level ignored on model switch (#3159), BYOK statusline showing wrong effort (#3135), quota display for Free users (#44-0 fix), and custom footer commands not executing (#3192) – all erode trust in the settings system.
- **Data loss**: Crashes swallowing enqueued messages (#3184) and silent exits with no logs (#3189) make debugging painful.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-08

## Today's Highlights

Today’s activity is dominated by targeted bug fixes and community-requested workflow improvements. A new PR allows API-key based authentication to bypass forced OAuth in ACP environments, unblocking IDE users. Meanwhile, a long-standing issue about truncated thinking traces continues to draw community engagement, and a PR addressing macOS screenshot attachment failures has been submitted, resolving a major UX pain point for Mac users. The project also saw merges and reopenings on plugin compatibility and display name fixes, indicating steady maintenance momentum.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#1864] Display full thinking traces in Kimi CLI**  
   Author: YunfanZhang42 | Comments: 12 | 👍: 10  
   Users want the complete reasoning chain (thinking traces) visible in the CLI output, not truncated. High community interest suggests this is a missing feature for power users auditing model behavior.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/1864)

2. **[#2182] macOS screenshot thumbnails fail to attach**  
   Author: abm9111 | Comments: 1 | 👍: 0  
   Drag-and-drop of floating macOS screenshot thumbnails into the terminal results in attachment failure due to a race condition with temporary files. A minor but very visible UX bug for Mac developers.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2182)

3. **[#2010] Shift+Enter for newline in prompt input**  
   Author: wowlegend | Comments: 1 | 👍: 1  
   Users request Shift+Enter to insert a newline, aligning with modern chat interface conventions (ChatGPT, Claude, Discord). Currently only Ctrl+J works.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2010)

4. **[#2178] Windows kimi.exe blank FileVersionInfo**  
   Author: Kafshi3239sty | Comments: 1 | 👍: 0  
   The Windows binary lacks proper version info, causing the VS Code extension to reject it as incompatible. Blocks Windows users from using the latest CLI in VS Code.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2178)

5. **[#2180] Web CLI needs /task command**  
   Author: scially | Comments: 0  
   Users of the web-based CLI expect a `/task` command for workflow management, which is available in the desktop terminal but missing in the web interface.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2180)

6. **[#2179] Incremental token deltas in stream-json mode**  
   Author: FlamingoPg | Comments: 0  
   The `--print --output-format stream-json` mode buffers entire assistant turns instead of emitting token-level deltas, breaking downstream tooling that requires streaming granularity.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2179)

7. **[#2175] model_display_name ignores backend display_name**  
   Author: tears-mysthrala | Comments: 0  
   Hardcoded display name override prevents showing the correct model name (e.g., "Kimi-k2.6") returned by the backend. Misleading for users relying on model identification.  
   → [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2175)

---

## Key PR Progress

1. **[#2185] fix(acp): allow API-key based auth to bypass forced OAuth login**  
   Author: yogaxu | Updated: 2026-05-08  
   Unblocks users who have configured an API key but are forced through OAuth when using ACP (e.g., JetBrains). Direct fix for an authentication friction point in IDE workflows.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2185)

2. **[#2177] fix(soul): clear partial UI output when LLM step is retried**  
   Author: 7Sageer | Updated: 2026-05-08  
   Prevents concatenation of failed partial output with retried attempts, ensuring clean output on retry. Important for reliability of streaming UX.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2177)

3. **[#762] fix: respect SSL_CERT_FILE env var for corporate proxy support**  
   Author: aaraujodata | Updated: 2026-05-08  
   Enables CLI to work behind corporate proxies (Zscaler, etc.) by respecting the `SSL_CERT_FILE` environment variable. A long-standing request from enterprise users.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/762)

4. **[#2183] fix(shell): attach dropped image paths eagerly**  
   Author: he-yufeng | Updated: 2026-05-07  
   Resolves #2182 by scanning user text for local image paths and sending them immediately, avoiding race conditions with temporary files. Direct fix for the macOS thumbnail issue.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2183)

5. **[#1715] feat(plugin): add Claude-compatible local plugin support (Closed)**  
   Author: GTC2080 | Updated: 2026-05-07  
   Draft PR adding local plugin loading via `--plugin-dir` and auto-discovery of Claude Plugins. Closed after discussion; may be a sign of a changing plugin strategy.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/1715)

6. **[#1127] style(web): tweak some web UI details (Closed)**  
   Author: anxndsgn | Updated: 2026-05-07  
   Minor visual refinements to the web interface. Closed after review; likely merged.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/1127)

7. **[#2181] fix: add Windows binary version info**  
   Author: he-yufeng | Updated: 2026-05-07  
   Fixes #2178 by generating version-info from `pyproject.toml` and including it in PyInstaller builds. Ensures Windows release artifacts are accepted by VS Code extension.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2181)

8. **[#2176] fix(hooks): extract text from ContentPart for UserPromptSubmit hook**  
   Author: tears-mysthrala | Updated: 2026-05-07  
   Fixes #2148 — the `UserPromptSubmit` hook was receiving empty prompts for list-type inputs, breaking regex-based matchers. Now correctly extracts text from `ContentPart`.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2176)

9. **[#2174] fix: respect model display_name for kimi-for-coding**  
   Author: tears-mysthrala | Updated: 2026-05-07  
   Resolves #2175 by removing the hardcoded display name override, allowing the backend's correct name (e.g., "Kimi-k2.6") to appear.  
   → [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2174)

---

## Feature Request Trends

- **CLI Interaction Ergonomics:** Multiple requests for Shift+Enter newline insertion and full thinking trace display indicate a community that wants richer, more familiar interaction patterns in the terminal.
- **Developer Tooling Integration:** Requests for incremental token deltas in JSON streaming and `/task` command in the web CLI point toward deeper CI/CD and IDE pipeline integration needs.
- **Model Information Transparency:** Users want accurate, backend-derived model display names, not hardcoded overrides — a sign of growing trust and reliance on model version tracking.

---

## Developer Pain Points

- **Model Display Name Override:** The hardcoded override in `model_display_name()` is a recurring frustration, misleading users about which backend model is actually being used.
- **macOS Screenshot Attachment:** A simple UX task (drag-and-drop) breaks due to temporary file handling — a sharp edge for everyday Mac users.
- **Windows Version Compatibility:** Missing `FileVersionInfo` blocks the less-common but vocal Windows user base from using the CLI in their preferred IDE.
- **Corporate/Proxy Network Adapter:** SSL certificate issues remain a high-latency pain for enterprise developers; the `SSL_CERT_FILE` PR (#762) is a welcome but long-overdue fix.
- **Streaming Data Fidelity:** Developers expecting token-level streaming for monitoring or caching are blocked by message-level buffering — a technical debt for those building on top of Kimi.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-08

## Today's Highlights
The OpenCode team shipped **v1.14.41** with a critical fix for formatter output handling and a UX improvement: session warping now preserves uncommitted file changes. The community is buzzing about **Cursor CLI integration** (Issue #2072) with 168 👍, while a new update regression (Issue #26278) is causing input failures for some users. On the PR front, the desktop main process is being refactored to Effect-TS (PR #26148), and a major config override bug has been fixed (PR #25121).

## Releases
**v1.14.41** was released in the last 24 hours. Changes include:
- **Core bugfix**: Restored formatter output handling for formatters that write to stdout/stderr.
- **Core improvement**: Session warping across workspaces now carries over uncommitted file changes.
- **TUI bugfix**: Custom provider dialog exposed attachment toggle (regression from previous release).

[View full release notes](https://github.com/anomalyco/opencode/releases/tag/v1.14.41)

## Hot Issues
*Top 10 noteworthy issues from the last 24 hours, ranked by community engagement and impact.*

1. **[#2072 – Support for Cursor?](https://github.com/anomalyco/opencode/issues/2072)** (67 comments, 168 👍)  
   *Asks if OpenCode can support Cursor’s new public CLI. High demand, but API may be undocumented.*

2. **[#11112 – Always stuck at “Preparing write…”](https://github.com/anomalyco/opencode/issues/11112)** (65 comments, 28 👍)  
   *Persistent blocking loop when writing to workflow files. Ongoing for months, affects many users.*

3. **[#4704 – /undo and /timeline undo does not revert file edits](https://github.com/anomalyco/opencode/issues/4704)** (16 comments, 14 👍)  
   *Undo commands not restoring file changes even in git-tracked projects. Core editing workflow issue.*

4. **[#8601 – Error: unknown certificate verification error](https://github.com/anomalyco/opencode/issues/8601)** (23 comments, 2 👍)  
   *Certificate errors across multiple AI providers, Gemini 3 login also broken. Likely TLS/proxy issue.*

5. **[#1515 – CLI tab completions for bash, fish, and zsh](https://github.com/anomalyco/opencode/issues/1515)** (8 comments, 31 👍)  
   *Long-standing feature request for shell completion scripts. Contributor interest noted.*

6. **[#26209 – Win Desktop cannot use oh-my-opencode plugin](https://github.com/anomalyco/opencode/issues/26209)** (7 comments)  
   *Plugin broken since v1.14.35 on Windows desktop. Multiple reports of similar plugin loading failures.*

7. **[#14332 – Amazon Bedrock Opus 4.6 compaction failure](https://github.com/anomalyco/opencode/issues/14332)** (7 comments, 7 👍)  
   *Error with thinking/redacted_thinking blocks on Bedrock. Affects Anthropic models via Bedrock.*

8. **[#21299 – Markdown rendering broken since opentui upgrade](https://github.com/anomalyco/opencode/issues/21299)** (6 comments, 1 👍)  
   *Raw markdown shown instead of formatted output on macOS and WSL. Likely opentui compatibility issue.*

9. **[#26278 – New update breaks app](https://github.com/anomalyco/opencode/issues/26278)** (3 comments)  
   *Typing fails to clear “Ask anything” status; input not accepted. Critical regression reported immediately after v1.14.41 upgrade.*

10. **[#24744 – Project edit dialog does not persist name or icon changes](https://github.com/anomalyco/opencode/issues/24744)** (3 comments, 2 👍)  
    *Web sidebar project metadata not saving reliably. Affects project organization UX.*

## Key PR Progress
*10 pull requests with significant changes or community interest.*

1. **[#26148 – refactor(desktop): convert main process to Effect-TS](https://github.com/anomalyco/opencode/pull/26148)**  
   *Large refactor of desktop main process using Effect-TS for better error handling and composability. Extracted updater logic, replaced manual promise chains.*

2. **[#25121 – fix(opencode): project .opencode/ config now overrides global ~/.opencode](https://github.com/anomalyco/opencode/pull/25121)**  
   *Bug fix: global config was incorrectly winning over project config. Now project config takes precedence. Closes #19296 and #21307.*

3. **[#23111 – feat(opencode): display cached token count inline in TUI](https://github.com/anomalyco/opencode/pull/23111)**  
   *Shows `(N cached)` next to token counts when cache read/write > 0. Improves visibility of caching savings.*

4. **[#23525 – fix(opencode): handle AWS SSO session expiry with automatic re-login](https://github.com/anomalyco/opencode/pull/23525)**  
   *Intercepts credential errors, prompts SSO login, and retries transparently. Eliminates manual re-authentication for Bedrock users.*

5. **[#23108 – feat(opencode): add cache_point_ttl option for Bedrock provider](https://github.com/anomalyco/opencode/pull/23108)**  
   *Configurable TTL for cache points in Bedrock (5m or 1h). Injects cachePoint block after system prompt for better prompt caching.*

6. **[#23104 – fix(opencode): preserve reasoning providerMetadata across model switches](https://github.com/anomalyco/opencode/pull/23104)**  
   *Anthropic thinking blocks were stripped when switching models. Now preserved. Fixes #22813.*

7. **[#26291 – fix(ci): pin workflow actions](https://github.com/anomalyco/opencode/pull/26291)**  
   *Pins GitHub Actions to immutable commit SHAs for supply-chain security. Closes #16041.*

8. **[#25867 – fix(session): clone tool input before passing to EventV2 to prevent Immer freeze](https://github.com/anomalyco/opencode/pull/25867)**  
   *Fixes `Attempted to assign to readonly property` on every tool call when EXPERIMENTAL mode is enabled.*

9. **[#26270 – fix(i18n): complete Simplified Chinese (zh) translations](https://github.com/anomalyco/opencode/pull/26270)**  
   *Brings zh.ts to full parity with en.ts — 12 translation fixes and numerous new entries. Community contribution.*

10. **[#26280 – feat(app): add ctrl/cmd+number keybinds to switch projects](https://github.com/anomalyco/opencode/pull/26280)**  
    *Discord-style number keybinds for project switching. Also adds hidden parameter for commands not shown in palette.*

## Feature Request Trends
Based on recent issues and PRs, the most requested feature directions are:

- **Multi-provider expansion** – Support for Cursor CLI, Amazon Bedrock improvements, Google Vertex AI, custom OpenAI-compatible providers with proper vision handling.
- **Semantic code understanding** – Repeated requests for semantic indexing (like Kilo/Cursor), vector database integration, and semantic grep (mgrep).
- **Shell & CLI ergonomics** – Tab completions for bash/zsh/fish, better signal forwarding, configurable command timeouts.
- **Caching & performance** – Segment-based prefix caching for multi-agent orchestration, token caching indicators, cache TTL for Bedrock.
- **Plugin ecosystem reliability** – Plugin display and loading on Windows desktop, plugin registry integration with Zed, better plugin API.
- **Mobile & accessibility** – Mobile touch optimizations, agent status indicators visible without hover, non-ASCII path support.
- **Project & session management** – Persisting project metadata, session list reliability, undo improvements.

## Developer Pain Points
Recurring frustrations from the community:

- **Update regressions** – Each release seems to break plugin compatibility (Windows desktop), input handling (#26278), or markdown rendering (#21299). Users want more rigorous regression testing.
- **Undo & version control** – The `/undo` and `/timeline` commands do not reliably revert file changes (#4704), even in git-tracked projects. This undermines trust in the editing workflow.
- **Certificate & authentication errors** – Multiple users report certificate verification failures across providers (#8601), and AWS SSO session expiry interrupts workflows.
- **Local / offline model issues** – Ollama integration returns empty results (#7083). Users running local models encounter silent failures.
- **Non-ASCII path support** – Issues with Japanese/Chinese filenames (#26267) block global adoption.
- **Plugin post-update failures** – After v1.14.35, Windows desktop cannot load oh-my-opencode plugin (#26209, #26123). Plugin users feel unsupported on Windows.
- **Config persistence** – Changing project names/icons doesn't stick (#24744), and global config overrides project config unexpectedly (though #25121 fixes this).

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# 🥧 Pi Community Digest – 2026-05-08

*Generated from github.com/badlogic/pi-mono (mirroring earendil-works/pi)*

---

## Today's Highlights

The team completed the **npm scope migration** from `@mariozechner` to `@earendil-works`, releasing **v0.73.1** with self-update support and **v0.74.0** with updated repository references. A massive **big-refactor wave** closed over a dozen issues, including critical fixes for OpenAI delta handling, terminal corruption, and update logic. Meanwhile, the community continues to push for **local LLM support** (open issue #3357, 23 👍) and new provider integrations like **GPT-5.5 Instant** and **Together AI**.

---

## Releases

### v0.74.0
- **Changed** – Updated all repository links and package references for the migration to `earendil-works/pi-mono` and `@earendil-works/*` package scopes.
### v0.73.1
- **New** – `pi update --self` now supports the scope rename from `@mariozechner/pi-coding-agent` to `@earendil-works/pi-coding-agent`, enabling smooth migration for global installs.

*Both releases were published within the last 24 hours.*

---

## Hot Issues (10 noteworthy)

1. **[#3357 – Official local LLM provider extension](https://github.com/earendil-works/pi/issues/3357)**  
   *Open, 23 👍, 9 comments*  
   The most-upvoted open feature request asks for dynamic model fetching from `{baseUrl}/models` to support llama.cpp, Ollama, LM Studio, etc. Community clearly wants Pi to be provider-agnostic.

2. **[#2616 – SessionManager is sync-only: blocks async/database-backed persistence](https://github.com/earendil-works/pi/issues/2616)**  
   *Open, 4 comments*  
   A fundamental architectural pain point: every `SessionManager` method uses blocking I/O (`appendFileSync`, `readFileSync`), making async backends impossible. No movement yet.

3. **[#3929 – Bun startup crash when `bun pm bin -g` fails](https://github.com/earendil-works/pi/issues/3929)**  
   *Closed, 8 comments*  
   Critical bug for Bun users – Pi crashed on startup if `~/.bun/install/global/package.json` was missing. Fixed in a recent update.

4. **[#4228 – Fix openai-completions provider incorrectly handling deltas with both content and tool calls](https://github.com/earendil-works/pi/issues/4228)**  
   *Closed (big-refactor), 18 comments*  
   High-activity bug where stream deltas mixing `reasoning_content`, `content`, and `tool_calls` were processed sequentially instead of accumulated independently. Fixed by PR #4247.

5. **[#4208 – Inline image previews corrupt terminal rendering in cmux/Ghostty](https://github.com/earendil-works/pi/issues/4208)**  
   *Closed (big-refactor), 14 comments*  
   Pi’s Kitty graphics path broke inside `cmux` (Ghostty). A separate rendering fix was merged in PR #4261.

6. **[#3780 – Duplicate characters on Italian keyboard with Kitty Keyboard Protocol](https://github.com/earendil-works/pi/issues/3780)**  
   *Closed (inprogress, weekend), 7 comments*  
   Keyboard input regression: certain keys on Italian layouts inserted twice when Kitty protocol flags `1+2+4` were active. Root cause in `pi-tui` editor.

7. **[#2451 – Add support for Cursor’s models (Composer 1.5/2)](https://github.com/earendil-works/pi/issues/2451)**  
   *Closed, 6 comments*  
   Proposal to bring Cursor subscription models into Pi. Not yet implemented, but the conversation shows appetite for multi-vendor model access.

8. **[#4273 – Incorrect Pi update notice in TUI](https://github.com/earendil-works/pi/issues/4273)**  
   *Closed (bug, big-refactor), 5 comments*  
   After updating to 0.73.1, the TUI immediately showed a 0.74.0 notice – a false alarm caused by stale version detection. Fixed in the big refactor.

9. **[#4294 – `pi update` is parsed as a prompt instead of a CLI subcommand](https://github.com/earendil-works/pi/issues/4294)**  
   *Closed (weekend, big-refactor), 1 comment*  
   Running `pi update` started an interactive session treating "update" as the initial message. A breaking UX regression caught quickly.

10. **[#4293 – Support internal models from Copilot subscription](https://github.com/earendil-works/pi/issues/4293)**  
    *Closed (weekend, big-refactor), 1 comment*  
    Users want Pi to expose Copilot’s internal models (e.g., Opus 4.7 with 1M context). This mirrors the ongoing trend of leveraging existing subscriptions.

---

## Key PR Progress (10 important)

1. **[#4247 – fix(ai): handle mixed chat completion deltas](https://github.com/earendil-works/pi/pull/4247)**  
   *Closed, by mitsuhiko*  
   Switches to separate accumulators for content and tool calls, fixing the core issue of #4228. Tests were auto-generated (“clanker slop”).

2. **[#4261 – fix(tui): keep kitty image redraws inside TUI](https://github.com/earendil-works/pi/pull/4261)**  
   *Closed, by mitsuhiko*  
   Fixes image corruption when rendering inside reduced scroll regions (fixes #4208 and related ghost image bleed).

3. **[#4277 – feat(ai): add gpt-5.5-chat-latest (OpenAI’s new default Instant model)](https://github.com/earendil-works/pi/pull/4277)**  
   *Closed*  
   Adds the newly announced GPT-5.5 Instant model to Pi’s model catalog, including context window metadata.

4. **[#4259 – feat: complete rollback architecture with 1300+ tests](https://github.com/earendil-works/pi/pull/4259)**  
   *Closed*  
   Major milestone: `FileSnapshotManager` wired into `AgentSession`, thin adapter pattern, 10 core rollback tests passing. Enables reliable session rollback.

5. **[#4281 – feat(tui): show/hide cursor on terminal focus change](https://github.com/earendil-works/pi/pull/4281)**  
   *Closed, by dukejeffrie*  
   Enables DECSET 1004 focus reporting – the cursor now hides when the terminal window loses focus and reappears on focus, a subtle but polished UX improvement.

6. **[#4283 – update `pi-mono` repo name to `pi`](https://github.com/earendil-works/pi/pull/4283)**  
   *Closed, by bronson*  
   Fixes the changelog link in update notices (fixes #4280). Housekeeping during the migration.

7. **[#4264 – fix(extensions): expose label/execute in ToolInfo and allow tool override via last-write-wins](https://github.com/earendil-works/pi/pull/4264)**  
   *Closed, by nantas*  
   Fixes extension tool collision issues, enabling extensions like `pi-tool-display` to override MCP Direct Tools’ rendering.

8. **[#3887 – feat: image content (open)](https://github.com/earendil-works/pi/pull/3887)**  
   *Open, by cristinaponcela*  
   Adds image output support via a new API. Mirrors the stream API for image blocks, allowing agents to generate images. Early but high-potential.

9. **[#3624 – feat(ai): add Together AI as a provider (open)](https://github.com/earendil-works/pi/pull/3624)**  
   *Open, by Nutlope*  
   Native integration with Together AI’s OpenAI-compatible Chat Completions API. Model list sourced from `models.dev`. Awaiting review.

10. **[#4244 – chore(coding-agent): switch back from fork to upstream jiti 2.7](https://github.com/earendil-works/pi/pull/4244)**  
    *Closed, by pi0*  
    Drops the custom jiti fork in favor of upstream v2.7, which includes needed virtual module and static bundling fixes.

---

## Feature Request Trends

- **Local & Alternative Providers** – The community consistently wants to run Pi with local models (#3357, #3624), Cursor subscription models (#2451), and Copilot internal models (#4293). A **provider-agnostic architecture** is the top request.
- **Image & Document Input/Output** – Requests for native PDF/file input (#4287), image output from agents (#3887), and clipboard image paste (#2144) indicate a desire to handle richer content beyond text.
- **Better Terminal Compatibility** – IME input (Italian, Chinese) and terminal emulator quirks (cmux, Windows Terminal) drive requests for configurable keyboard protocols and fallback rendering.
- **Extension & SDK Hooks** – Requests for graceful turn stop (#4291), configurable VCS status (#4292), and tool override control (#4264) show that developers want more fine-grained control over Pi’s internals.
- **Model Persistence & Display** – Users want model selection to not overwrite defaults (#3254) and macOS-specific UI labels (#4289).

---

## Developer Pain Points

- **Terminal Rendering Instability** – Inline images break inside cmux/Ghostty (#4208), hyperlinks stop working (#4180), background colors bleed (#4270), and Kitty images corrupt across scroll regions (#4261). Terminal compatibility remains a top frustration.
- **Input & IME Regressions** – Italian keyboard duplication (#3780), Chinese IME doubled/lost characters (#4253), and multiline paste submission on Windows (#767) – all stem from the Kitty Keyboard Protocol implementation.
- **Update & Migration Woes** – The scope migration from `@mariozechner` to `@earendil-works` caused multiple issues: stale update notices (#4273), leftover bin shims (#4284), `pi update` being treated as a prompt (#4294), and general inability to update (#4288).
- **Async/Sync Architecture Gaps** – The sync-only `SessionManager` (#2616) and WebSocket transport errors that kill the agent loop (#4257) highlight a need for more robust async handling.
- **Bun Support Fragility** – Startup crash on missing `package.json` (#3929) – even after fixes, Bun users face occasional instabilities.
- **CLI vs Interactive Mode Confusion** – `pi -p "say Hi"` hangs after execution (#4279) and `pi update` enters interactive mode (#4294) – the command-line parity with other tools is not yet seamless.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the **Qwen Code Community Digest** for **2026-05-08**, generated from the provided GitHub data.

---

# Qwen Code Community Digest — 2026-05-08

## 1. Today’s Highlights
The team released **v0.15.8**, focusing on SDK telemetry and test stability, while the nightly build introduces a sensitive span attribute opt-in for OpenTelemetry. A highly controversial **OAuth free tier reduction proposal** (Issue #3203) continues to dominate community discussion with 122 comments, reflecting developer concerns over access costs. On the technical front, a stacked **remote-control foundation** (PRs #3929-#3931) and a **virtual viewport** fix for long conversations (PR #3941) were proposed to address long-standing UI performance issues like terminal flickering.

## 2. Releases
- **[v0.15.8-nightly.20260508.0491252b2](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.8-nightly.20260508.0491252b2)**: Adds a `feat(telemetry)` option to opt-in for sensitive span attributes, improving observability control for enterprise users.
- **[v0.15.8](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.8)**: Includes test alignment for tool-control E2E (prior-read enforcement) and a fix for symlinks pointing outside the skills directory.

## 3. Hot Issues (Top 10)
1.  **#3203 [OPEN] Qwen OAuth Free Tier Policy Adjustment**: Proposes reducing the daily free quota from 1,000 to 100 requests and phasing out the free tier. **122 comments**, community is heavily divided on the impact to hobbyists and testing workflows. [Link](https://github.com/QwenLM/qwen-code/issues/3203)
2.  **#3740 [CLOSED] Settings.json Model Override Problem**: Users report that v0.15.5 overwrites manually configured non-Coding Plan models on startup, overriding user preferences. Highlights a UX regression in model management. [Link](https://github.com/QwenLM/qwen-code/issues/3740)
3.  **#3901 [CLOSED] TUI Multi-line Paste Auto-Submission**: Pasting code into the CLI triggers multiple submissions due to newline interpretation. Critical for power-users who rely on copying logs or code blocks. [Link](https://github.com/QwenLM/qwen-code/issues/3901)
4.  **#3881 [OPEN] Local Qwen3-27B Repeating Characters**: Querying a locally deployed model causes it to emit infinite `/` characters until token limit. Suggests an issue with local inference streaming or stop-token logic. [Link](https://github.com/QwenLM/qwen-code/issues/3881)
5.  **#3838 [OPEN] Terminal Infinite Scroll/Flicker**: The terminal UI enters a rapid refresh loop during code analysis, making output unreadable. Affects developer trust in the CLI interface. [Link](https://github.com/QwenLM/qwen-code/issues/3838)
6.  **#3877 [OPEN] .env File API Key Ignored**: Users manually setting `OPENCODE_GO_API_KEY` in config files are forced to re-authenticate. Signals a regression in config hierarchy parsing. [Link](https://github.com/QwenLM/qwen-code/issues/3877)
7.  **#3511 [OPEN] JetBrains AI Integration**: Users cannot integrate Qwen Code into JetBrains IDEs without Qwen OAuth, requesting support for plain API keys. Highlights demand for IDE/ACP integration flexibility. [Link](https://github.com/QwenLM/qwen-code/issues/3511)
8.  **#3945 [OPEN] Edit Tool Deadlock on Large Files**: The `edit` tool requires a "full read" before editing, but `read_file` truncates large files, creating an impossible precondition. This is a critical blocker for editing production codebases. [Link](https://github.com/QwenLM/qwen-code/issues/3945)
9.  **#3925 [OPEN] Monitor Tool Notifications Misrouted for Sub-agents**: Notifications from sub-agents are delivered to the main agent, polluting the parent context. Affects multi-agent debugging clarity. [Link](https://github.com/QwenLM/qwen-code/issues/3925)
10. **#3940 / #3939 [OPEN] 401 Invalid Token Errors**: Multiple users reporting "401 invalid access token or token expired" errors, preventing any usage. Likely an upstream authentication provider issue. [Link](https://github.com/QwenLM/qwen-code/issues/3940) | [Link](https://github.com/QwenLM/qwen-code/issues/3939)

## 4. Key PR Progress (Top 10)
1.  **#3775 (OPEN) Refactor Side-Query LLM Calls**: Routes all one-shot LLM calls through a `runSideQuery` chokepoint for consistent telemetry and caching. Improves observability across features like tool summaries and session titles. [Link](https://github.com/QwenLM/qwen-code/pull/3775)
2.  **#3589 (OPEN) ToolSearch for On-Demand Tools**: Introduces a `ToolSearch` feature to defer MCP and low-frequency tool schemas, shrinking the default prompt by ~15K tokens. Directly improves cost and latency for most sessions. [Link](https://github.com/QwenLM/qwen-code/pull/3589)
3.  **#3902 (OPEN) Throttle Shell Tool Live Text**: Fixes a bug where `ShellToolInvocation` updates UI on every data chunk, reducing redraw pressure during long-running shell commands. [Link](https://github.com/QwenLM/qwen-code/pull/3902)
4.  **#3896 (OPEN) Normalize OpenAI Stream Deltas**: Fixes a compatibility issue where some upstream providers send cumulative text instead of incremental deltas, preventing text duplication in Gemini and other pipelines. [Link](https://github.com/QwenLM/qwen-code/pull/3896)
5.  **#3778 (OPEN) Desktop App Package**: Adds a new `packages/desktop/` module with ACP SDK integration, expanding Qwen Code from a CLI-only tool to a desktop application. [Link](https://github.com/QwenLM/qwen-code/pull/3778)
6.  **#3900 (OPEN) NotebookEdit Tool**: Adds dedicated editing support for `.ipynb` files, allowing Qwen to read and write structured Jupyter notebook cells. Closes a long-standing feature request (#2816). [Link](https://github.com/QwenLM/qwen-code/pull/3900)
7.  **#3933 (OPEN) Fix Monitor Notifications for Sub-agents**: Routes monitor events to the correct agent (foreground, background, fork), fixing the misrouting bug in #3925. Critical for multi-agent environments. [Link](https://github.com/QwenLM/qwen-code/pull/3933)
8.  **#3835 (OPEN) Python SDK Release Notes**: Replaces manual verbatim release notes with automated `--generate-notes`, streamlining the release process for the Python SDK package. [Link](https://github.com/QwenLM/qwen-code/pull/3835)
9.  **#3932 (CLOSED) Accept Partial Reads in Prior-Read Enforcement**: Relaxes the edit precondition to allow editing after a partial read, resolving the deadlock on large files (related to Issue #3945). [Link](https://github.com/QwenLM/qwen-code/pull/3932)
10. **#3929-#3931 (OPEN) Remote Control Stack**: A three-PR stack (Foundation, Worker Server, TUI Integration) that establishes a local HTTP/WebSocket remote-control server, enabling programmatic control of the CLI session. A major infrastructure move. [Link](https://github.com/QwenLM/qwen-code/pull/3929) | [Link](https://github.com/QwenLM/qwen-code/pull/3930) | [Link](https://github.com/QwenLM/qwen-code/pull/3931)

## 5. Feature Request Trends
- **Sub-Agent Visibility (5 requests)**: Users are demanding better insight into sub-agent thinking (Issue #3758, #3924, #3666). They want to see full reasoning traces, TODO lists, and tool-call summaries for sub-agents, not just the main session.
- **Enhanced Observability (3 requests)**: A strong push for OpenInference-compliant traces (Issue #3917), correlated debug logs (PR #3847), and general telemetry to support external monitoring tools like Phoenix.
- **Extensibility & Native Tools (2 requests)**: A call for first-class native tool registration for extensions (Issue #3870), allowing plugins to contribute tools beyond the existing MCP model.
- **Terminal UX Improvements (3 requests)**: Requests for better input editing (Ctrl+Backspace, text selection in Issue #3926) and expanded command visibility (Issue #3139) to match the polish of tools like Claude Code.

## 6. Developer Pain Points
- **Model Configuration Overrides (#3740, #3877)**: Users are frustrated by Qwen Code forcibly overwriting custom model configurations and ignoring environment variables. This erodes trust in local settings.
- **TUI Input Handling (#3901, #3926)**: The inability to paste multi-line text without breaking commands, and missing text-editing shortcuts, makes the CLI feel unpolished for daily coding.
- **Terminal Rendering Flicker (#3838, #3941)**: The UI struggles with long conversations, causing scrolling loops and high CPU usage. The proposed "virtual viewport" fix is a direct response to this persistent UX issue.
- **AI Behavior Aberrations (#3881)**: Local models outputting infinite repeating characters is a red flag for local-first users, suggesting a gap in streaming or stop-sequence handling.
- **Tool Usability (#3945, #3925)**: The edit tool’s deadlock on large files and the misrouting of sub-agent notifications create "silent failures" that are hard to diagnose, lowering developer confidence in autonomous workflows.
- **Authentication Burdens (#3940, #3511)**: Frequent 401 errors and the forced OAuth requirement for IDE integration create friction for users who prefer API-key-based, serverless setups.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*