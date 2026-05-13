# AI CLI Tools Community Digest 2026-05-13

> Generated: 2026-05-13 10:00 UTC | Tools covered: 8

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date:** 2026-05-13

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing rapid maturation, with six major tools (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, and Qwen Code) all shipping frequent releases and engaging active communities. However, the day's data reveals a landscape plagued by regressions and reliability issues—every tool except Pi and OpenCode released a patch or minor version today, often to fix bugs introduced in the previous release (e.g., GitHub Copilot CLI v1.0.46 broke MCP native bindings; Claude Code v2.1.140 fixed `/goal` hangs; Gemini CLI v0.43.0-preview.0 targets surgical edit accuracy). Common pain points across tools include MCP plugin fragility, configuration corruption under stress, catastrophic slowness on small tasks, and credit/usage waste on failures. The community is vocal about session lifecycle management (fork, pause, resume across worktrees) and guardrail consistency (plan‑mode trust, runaway protection). At the same time, ambitious architectural shifts—daemon/service modes, AST‑aware file reads, vendorized dependency management—signal a move toward more robust, production‑grade tooling.

## 2. Activity Comparison

| Tool                     | Issues Updated (notable) | PRs Updated (notable) | Release Today? |
|--------------------------|--------------------------|------------------------|----------------|
| **Claude Code**          | 10 hot / 25+ duplicates  | 10 key                 | ✅ v2.1.140   |
| **OpenAI Codex**         | 10 hot                   | 10 key                 | ❌            |
| **Gemini CLI**           | 10 hot                   | 10 key                 | ✅ v0.43.0-preview.0 |
| **GitHub Copilot CLI**   | 10 hot                   | 2                      | ✅ v1.0.47-0  |
| **Kimi Code CLI**        | 10 hot                   | 10 key                 | ✅ v1.43.0    |
| **OpenCode**             | 50 updated               | 50 updated             | ❌            |
| **Pi (pi-mono)**         | 10 hot                   | 10 key                 | ❌            |
| **Qwen Code**            | 10 hot                   | 10 key                 | ✅ v0.15.11   |

**Observation:** OpenCode dominates raw issue/PR activity (50 each), indicating a very high community engagement velocity despite no release today. Claude Code, Gemini CLI, and Kimi Code show strong release cadence. GitHub Copilot CLI’s PR activity is unusually low (2), likely due to team focus on the v1.0.46 regression firefight.

## 3. Shared Feature Directions

The following requirements appear across multiple tool communities, indicating industry‑wide unmet needs:

| Requirement | Tools Affected | Specific Evidence |
|-------------|----------------|-------------------|
| **Session fork/pause/resume** | Claude Code (#58646), Copilot CLI (#2058, #3265), Kimi Code (#2252), Qwen Code (#4088) | Git‑aware history, `/fork`, `/pause`, `/goal` commands for branching workflows. |
| **MCP/Plugin reliability** | Claude Code (#57642, #57644), Copilot CLI (#3281, #3257), Kimi Code (#2251), OpenCode (#7006) | Transient disconnect kills tools permanently; `/reload-plugins` doesn’t respawn; stale TCP connections; hooks not firing. |
| **Atomic writes / config integrity** | Claude Code (#57639), Qwen Code (#4095), Pi (#4432 supply chain) | Disk‑full corruption leaves config files empty; need transactional file writes. |
| **Performance/latency (small tasks)** | Gemini CLI (#22141, 161👍), Codex (#21527), Kimi Code (#2077) | 10–60+ minute waits for simple edits or questions; model overload errors. |
| **Guardrail & runaway protection** | Claude Code (#57675 plan‑mode drift), Qwen Code (#4105 headless), Copilot CLI (#3279 “lies”) | Mode violations, no turn limits, agents making unenforced promises. |
| **Provider/failover flexibility** | Gemini (#26845, flash-lite fallback), Kimi (#1925 model switch), OpenCode (#13768 prefill error) | Automatic fallback to cheaper/free models when quota exhausted; model downgrading. |
| **Credit/usage transparency** | Claude Code (#57655 ultrareview credits wasted), Codex (#18101 context usage), Qwen (#4109 footer) | Rate‑limit errors still consume credits; no real‑time usage dashboard. |
| **Integration with IDEs & remote** | Claude Code (#57617 CLI↔IDE), OpenCode (#7790 SSH), Codex (#19681 cross‑device) | Workspace‑scoped connections, remote server mode, iOS control. |

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code |
|-----------|-------------|--------------|------------|-------------|-----------|----------|----|-----------|
| **Core Strength** | Agent orchestration & MCP ecosystem | VS Code + desktop integration | Fast response (claimed; currently failing) | GitHub workflow integration | K2.6 model + UI polish | Plugin extensibility & remote SSH | Lightweight, open‑source | Enterprise daemon & security |
| **Target User** | Multi‑agent power users | Pro/enterprise IDE users | TUI‑first developers | GitHub‑centric teams | Moonshot AI subscribers | Customizable plugin developers | Self‑hosting minimalists | Chinese & global enterprise |
| **Release Maturity** | High (2.1.x, daily patches) | Medium (0.129.x, regressions) | Low (0.43.0 preview, unstable) | High (1.0.x, stable base) | Medium (1.43.0, UI polish) | High (1.14.x, desktop app) | Low (0.74, active refactor) | Low (0.15.x, rapid iteration) |
| **Key Differentiator** | Agent sub‑types & review guidelines | Desktop app, Copilot integration | Thinking levels, memory system | Cloud agent, `gh` CLI native | Chinese market, K2.6 model | Hooks/plugin architecture | Vendorized deps, minimal supply chain | Daemon mode, git worktree support |
| **Observability** | Beta tracing (#4097) | Pulse metadata (#20081) | Telemetry buffer bug (#26404) | None visible | Telemetry schema (#2249) | Effect‑typed errors (#27301) | Arena ranking (#3546) | OpenTelemetry (#3731) |

**Key insight:** Claude Code and OpenCode lead in extensibility (plugins, hooks, agents). Gemini CLI and Codex are struggling with basic reliability. Qwen Code is investing in daemon/service‑oriented architecture, a differentiator from the TUI‑first tools. Pi is the only tool aggressively vendorizing dependencies to reduce supply chain risk.

## 5. Community Momentum & Maturity

| Tool | Community Activity | Velocity | Pain Tolerance |
|------|-------------------|----------|----------------|
| **OpenCode** | Very high (50+ issues/PRs/day) | High (frequent commits, many contributors) | Low – users report specific blocking bugs (Opus 4.6, sound effects) |
| **Claude Code** | High (25+ duplicates/day, strong PR pipeline) | High (daily releases, active maintainers) | Moderate – users accept regressions but demand fixes quickly |
| **Gemini CLI** | Very high (210 comments on #22141) | High (preview releases every few days) | Low – top frustration with slowness is dominant signal |
| **Codex** | Moderate (10 hot issues, but many closed) | Medium (no release today) | Low – quality regression eroding trust |
| **Kimi Code** | Moderate (10 hot issues, 10 PRs) | High (daily releases) | Moderate – K2.6 reliability issues, but feature requests still growing |
| **Qwen Code** | Growing (10 hot issues, 10 PRs) | High (nightly + preview releases) | Low – version 0.15.x users expect instability |
| **Pi** | Small but engaged (10 issues, 10 PRs) | Medium (refactoring phase) | High – community contributes fixes, tolerant of breakage |
| **Copilot CLI** | Low (2 PRs, 10 issues) | Low (patch release) | Moderate – regression fatigue from v1.0.46 |

**Maturity Assessment:**
- **Mature & stable:** Claude Code, Copilot CLI (despite regression)
- **Rapid growth with instability:** Gemini CLI, Qwen Code, Kimi Code
- **Established but struggling:** OpenAI Codex (quality regressions)
- **Niche & community‑driven:** Pi, OpenCode

## 6. Trend Signals

1. **From TUI to Daemon/Service Mode:** Qwen Code’s `qwen serve` (#3803) and OpenCode’s SSH remote (#7790) indicate a shift from purely TUI tools toward background services that can run persistently, survive sleep, and integrate with IDEs/RPC. This is a direct response to “session dead after sleep” and “can’t connect across workspaces” complaints across all tools.

2. **Supply Chain Security Awareness:** Pi removing 17 lockfile entries (#4467) and hard‑pinning deps (#4452), plus the Mistral 2.2.4 compromise (#4432), show that AI CLI tools are being treated as critical development infrastructure. Expect more vendorization, SBOMs, and automated vulnerability scanning in upcoming releases.

3. **Context‑Aware Compaction & File Handling:** Gemini CLI’s AST‑aware reads (#22745), Claude Code’s git‑aware history (#58646), and Qwen Code’s inline media stripping (#4101) all tackle the same core problem: current file I/O and context management are too blunt. The trend is toward intelligent, selective context preservation instead of full rewrites.

4. **Guardrail Fatigue & Runaway Agents:** Multiple issues across tools (Gemini #22323 false goal success, Claude #57675 plan‑mode drift, Copilot #3279 “lies”, Qwen #4093 command substitution bypass) reveal that users cannot trust agent self‑regulation. Expect push toward **configurable, enforced execution budgets** (turn limits, timeouts, tool‑use caps) and **explicit audit trails** rather than implicit agent promises.

5. **Model Agnosticism & Fallback Chains:** With Gemini and Kimi both fielding parallel PRs to add cheaper fallback models (#26845, #1925), and OpenCode users blocked on Opus 4.6 (#13768), the ecosystem is demanding automatic provider failover. The era of single‑model CLI tools is ending; future tools must handle multiple providers, automatic fallbacks, and transparent cost/quality tradeoffs.

6. **Real‑Time Usage Transparency:** Claude Code’s usage dashboard PR (#9918), Kimi Code’s telemetry schema (#2245), and multiple requests for visible token counts (Codex #18101, Qwen #4109) show that developers want **metered awareness before committing to a long session**. Expect usage metrics to become a standard UI element in all major CLI tools within the next quarter.

---

*Report generated from community digest data for 2026-05-13. All issue/PR links reference the respective GitHub repositories.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

**Data snapshot:** `github.com/anthropics/skills` (2026-05-13)

---

## 1. Top Skills Ranking (Most Discussed Pull Requests)

The following PRs command the highest level of community discussion, based on comment volume and sustained engagement.

### #514 – Add document-typography skill
**Status:** Open | **Author:** PGTBoos | **[GitHub](https://github.com/anthropics/skills/pull/514)**

A skill that catches orphan word wraps, widow paragraphs, and numbering misalignment in AI-generated documents. The author notes these typographic issues affect *every* document Claude produces. Discussion centers on whether the skill should be a standalone file or folded into existing document skills. High interest because it addresses a universal pain point for prose-heavy outputs.

### #538 – fix(pdf): correct case-sensitive file references in SKILL.md
**Status:** Open | **Author:** Lubrsy706 | **[GitHub](https://github.com/anthropics/skills/pull/538)**

Fixes eight case-sensitivity mismatches (e.g. `REFERENCE.md` → `reference.md`) that break on Linux/macOS file systems. While small in scope, the PR generated discussion because it uncovered a broader pattern of inconsistent casing across the repo and sparked debate about CI enforcement.

### #210 – Improve frontend-design skill clarity and actionability
**Status:** Open | **Author:** justinwetch | **[GitHub](https://github.com/anthropics/skills/pull/210)**

Revises the frontend-design skill to make every instruction executable within a single Claude conversation. The discussion highlighted the tension between descriptive (educational) and prescriptive (actionable) skill writing, a recurring theme in the community.

### #83 – Add skill-quality-analyzer and skill-security-analyzer to marketplace
**Status:** Open | **Author:** eovidiu | **[GitHub](https://github.com/anthropics/skills/pull/83)**

Two meta-skills for evaluating existing Skills across five dimensions (structure, documentation, security, etc.). This PR sparked the longest thread; contributors debated whether quality evaluation should be a community standard, how to weight dimensions, and whether security analysis belongs in the same skill.

### #486 – Add ODT skill (OpenDocument text creation and template filling)
**Status:** Open | **Author:** GitHubNewbie0 | **[GitHub](https://github.com/anthropics/skills/pull/486)**

Enables Claude to create, fill, read, and convert `.odt`/`.ods` files - essential for LibreOffice users. Discussion raised concerns about maintaining template fidelity and whether ODT support duplicates functionality already in the DOCX skill.

### #723 – feat: add testing-patterns skill
**Status:** Open | **Author:** 4444J99 | **[GitHub](https://github.com/anthropics/skills/pull/723)**

Comprehensive skill covering testing philosophy, unit testing, React component testing, and mocking. Conversation gravitated toward the "Testing Trophy" model vs. the more traditional pyramid, and whether the skill should enforce one approach or remain framework-agnostic.

### #509 – docs: add CONTRIBUTING.md
**Status:** Open | **Author:** narenkatakam | **[GitHub](https://github.com/anthropics/skills/pull/509)**

Addresses the repo's community health gap (25% on GitHub's metrics). The discussion strongly supported better onboarding; several commenters suggested this should be a high-priority merge before any new skill submissions.

---

## 2. Community Demand Trends (From Issues)

The most-voted and most-commented Issues reveal four clear demand clusters:

| Trend | Example Issues | Votes |
|-------|----------------|-------|
| **Organizational sharing & SSO** | #228 (org-wide skill sharing, 12 comments, +7 votes), #532 (skill-creator requires API key, blocks SSO users) | Highest |
| **Security & trust boundaries** | #492 (namespace abuse under anthropic/, 6 comments), #412 (agent governance proposal, 4 comments) | High |
| **Tooling & evaluation reliability** | #556 (run_eval.py never triggers skills, 8 comments, +6 votes), #202 (skill-creator outdated, 8 comments) | High |
| **Duplicate loading & plugin hygiene** | #189 (document-skills and example-skills install identical content, 6 comments, +8 votes), #1087 (plugin loads all 17 skills instead of declared 4) | Moderate |

**Secondary demands** include MCP integration (#16), AWS Bedrock compatibility (#29), and general bug reports around skill persistence (#62, #61).

The community is *not* asking for more niche domain skills (e.g., finance, healthcare) but rather for **infrastructure and governance**: better sharing mechanisms, trust verification, evaluation tooling, and plugin correctness.

---

## 3. High-Potential Pending Skills (Active PRs Not Yet Merged)

These PRs have sustained discussion and are likely to land soon:

- **#806 feat: add sensory skill — native macOS automation via AppleScript** – Uses `osascript` for window management, app scripting, and file automation without screenshot-based computer use. A two-tier permission system addresses security concerns. **[GitHub](https://github.com/anthropics/skills/pull/806)**

- **#360 Added AppDeploy skill for deploying full-stack webapps** – Teaches Claude to deploy and manage web apps using the AppDeploy platform. Updated as recently as 2026-05-04, suggesting active maintenance. **[GitHub](https://github.com/anthropics/skills/pull/360)**

- **#568 feat: add ServiceNow platform skill** – Covers ITSM, ITOM, ITAM, HRSD, CSDM, IntegrationHub, and more. Broad scope, but the author has addressed early review comments and the skill fills a clear enterprise gap. **[GitHub](https://github.com/anthropics/skills/pull/568)**

- **#147 Add codebase-inventory-audit skill** – A 10-step workflow for orphaned code detection, documentation gaps, and infrastructure bloat. Discussion focused on whether the output should be a standard `CODEBASE-STATUS.md` convention. **[GitHub](https://github.com/anthropics/skills/pull/147)**

- **#154 Add shodh-memory skill** – Persistent memory system for cross-session context. The "proactive_context" approach generated debate about context window management and privacy. **[GitHub](https://github.com/anthropics/skills/pull/154)**

- **#335 Add masonry-generate-image-and-videos skill** – Image/video generation via Masonry CLI (Imagen 3.0, Veo 3.1). Updated mid-March; pending because of dependency on external API availability. **[GitHub](https://github.com/anthropics/skills/pull/335)**

- **#444 feat: add AURELION skill suite (kernel, advisor, agent, memory)** – A four-skill set for structured thinking templates and knowledge management. Discussion focused on whether the suite should be split or kept together. **[GitHub](https://github.com/anthropics/skills/pull/444)**

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is no longer for more domain-specific skills, but for infrastructure that makes skills trustworthy, sharable, evaluable, and consistently deployable—meta-tooling and governance are the new frontier.**

---

# Claude Code Community Digest — 2026-05-13

## Today's Highlights

A minor release v2.1.140 shipped with improved subagent type matching and a critical fix for `/goal` hanging under restricted hook configurations. The issue tracker saw a surge of duplicate reports (25+ closed as duplicates today) around MCP plugin orphan markers, session corruption on disk-full errors, and ultrareview credit consumption on zero-output failures — suggesting these are hot topics the team is already triaging. A notable PR (#58646) proposes git-aware session history, which would fix the long-standing fragmentation across worktrees.

## Releases

**v2.1.140** (shipped today)
- **Agent tool `subagent_type` matching** now accepts case- and separator-insensitive values (e.g., `"Code Reviewer"` resolves to `code-reviewer`) — reduces friction when referencing agents by display names.
- **Agent color palette updated** — cosmetic improvement for multi-agent sessions.
- **Fixed:** `/goal` silently hanging when `disableAllHooks` or `allowManagedHooksOnly` is set; now surfaces an error. Important for users with strict hook policies.

## Hot Issues (10 Noteworthy)

1. **#58333** [OPEN] — **False-positive PATH warning on `claude update`** — `~/.local/bin` is correctly in PATH but warning persists. Affects macOS users. 3 comments, still open → [Link](https://github.com/anthropics/claude-code/issues/58333)

2. **#57603** [CLOSED] — **Resume idle agents from /agents picker** — Agents vanish from picker after final report; context is preserved but unreachable. Duplicate, but high community demand for session visibility. → [Link](https://github.com/anthropics/claude-code/issues/57603)

3. **#57617** [CLOSED] — **CLI-to-IDE connection limited to CWD** — Can't connect Claude Code CLI to IDEs running from different workspace directories. Duplicate, but a key workflow blocker for multi-project developers. → [Link](https://github.com/anthropics/claude-code/issues/57617)

4. **#57639** [CLOSED] — **`.claude.json` corruption on disk-full errors** — Large builds exhaust disk space, leaving config files empty. Community comment: "happened often enough that i wanted to complain." Duplicate, but highlights need for atomic writes. → [Link](https://github.com/anthropics/claude-code/issues/57639)

5. **#57642** [CLOSED] — **`.orphaned_at` marker permanently disables MCP servers** — Transient transport disconnect leaves MCP tools dead until full restart. `/reload-plugins` reports success but doesn't respawn child processes. Duplicate, but a major MCP reliability pain point. → [Link](https://github.com/anthropics/claude-code/issues/57642)

6. **#57651** [CLOSED] — **`/security-review` and `/build-review` fail on `--separate-git-dir` layouts** — Git preflight check assumes colocated `.git`. Affects bare-repo workflows and shell-wrapper patterns. Duplicate. → [Link](https://github.com/anthropics/claude-code/issues/57651)

7. **#57668** [CLOSED] — **Empty text block with `cache_control` causes unrecoverable session crash** — Harness emits malformed content blocks; Anthropic API rejects them permanently. Exact reproducibility cited. Duplicate. → [Link](https://github.com/anthropics/claude-code/issues/57668)

8. **#57675** [CLOSED] — **Plan-mode checkbox stays checked after approval but no longer gates prompts** — Visual state drift: first prompt is plan-gated, subsequent prompts execute freely despite checkmark. UX bug that undermines plan-mode trust. → [Link](https://github.com/anthropics/claude-code/issues/57675)

9. **#57681** [CLOSED] — **TeamDelete cannot clean up "in-process" agents after shutdown** — Agents acknowledge shutdown but `TeamDelete` refuses cleanup while they're still in `members[]`. Duplicate, with 1 👍 indicating community interest in team management. → [Link](https://github.com/anthropics/claude-code/issues/57681)

10. **#57655** [CLOSED] — **Ultrareview credit consumed with zero output** — Rate-limit (429) error still deduplicates review quota. Duplicate alongside #57619; users losing credits on infrastructure failures. → [Link](https://github.com/anthropics/claude-code/issues/57655)

## Key PR Progress (10 Important)

1. **#58646** [OPEN] — **Git-aware session history** — Keys history by repo root, not CWD. Fixes orphaned sessions across worktrees and enables `/resume` across branches. Community-requested for months. → [Link](https://github.com/anthropics/claude-code/pull/58646)

2. **#58644** [OPEN] — **Chained Bash hook example** — Conservative `PreToolUse` hook that blocks compound shell commands outside quoted strings. Helps plugin developers avoid unsafe auto-approval for `&&` / `||` chains. → [Link](https://github.com/anthropics/claude-code/pull/58644)

3. **#58641** [OPEN] — **Auth environment troubleshooting docs** — Adds README guidance for "organization disabled" errors when `ANTHROPIC_API_KEY` overrides subscription login. Includes safe shell checks. → [Link](https://github.com/anthropics/claude-code/pull/58641)

4. **#58639** [OPEN] — **AGENTS.md support in review guidelines** — Code-review workflows now gather AGENTS.md alongside CLAUDE.md. Defines coexistence: apply both, prefer CLAUDE.md on conflict. → [Link](https://github.com/anthropics/claude-code/pull/58639)

5. **#9916** [CLOSED] — **Fix directory operation crashes ("No assistant message found")** — Robust error handling for directory listings affecting AWS Bedrock and Haiku users. Stale PR (Oct 2025) but updated today. → [Link](https://github.com/anthropics/claude-code/pull/9916)

6. **#9917** [CLOSED] — **Fix session resume failures** — OAuth token refresh during restoration, missing sessionId handling, corrupt file recovery. Complementary to #9916. → [Link](https://github.com/anthropics/claude-code/pull/9917)

7. **#9918** [CLOSED] — **Usage limit transparency dashboard** — Real-time daily/weekly/monthly usage display. Response to the unannounced 2000→1000 limit cut in Sept 2025. → [Link](https://github.com/anthropics/claude-code/pull/9918)

8. **#9919** [CLOSED] — **Context-aware content filter** — Stops blocking legitimate DevOps work (SMTP config, Gmail passwords, automation tasks). Uses task-type recognition to reduce false positives. → [Link](https://github.com/anthropics/claude-code/pull/9919)

9. **#44055** [CLOSED] — **Fix agent YAML frontmatter in pr-review-toolkit** — Six agent files had invalid frontmatter (`mapping values are not allowed in this context`) due to unquoted colons in descriptions. Simple but critical for agent loading. → [Link](https://github.com/anthropics/claude-code/pull/44055)

10. **#11713** [OPEN] — **Developer-utilities plugin** — 5 commands for session management and project scaffolding. Original `/list-sessions`/`/label-session` components removed because they were superseded by core features. Community plugin with long tail. → [Link](https://github.com/anthropics/claude-code/pull/11713)

## Feature Request Trends

- **Session & Agent Lifecycle Management:** Multiple requests for resuming idle agents from the picker (#57603), showing per-message timestamps (#57671), and unifying session history across git worktrees (#58646). Users want session visibility without leaving the TUI.
- **IDE/Workspace Integration:** Strong demand for connecting CLI to IDEs outside the CWD (#57617), a "Select All Open Tabs" button in VS Code (#57610), and rendering session history in IDE context.
- **MCP Reliability & Observability:** Orphan markers (#57642), non-respawning child processes (#57644), and startup hook errors (#57665) all point to a fragile MCP plugin lifecycle. Users want `/reload-plugins` to actually reload.
- **Safety & Configuration Integrity:** Atomic writes for `.claude.json` (#57639), safe handling of disk-full errors, and warning-free PATH detection (#58333). Configuration corruption is a recurring theme.
- **Gatekeeping & Mode Consistency:** Plan-mode checkbox drift (#57675) and content-filter false positives (#9919, #57621) erode trust in Claude's mode enforcement and safety systems.

## Developer Pain Points

1. **MCP Plugin Lifecycle Fragility** — The `.orphaned_at` marker pattern (#57642) and `/reload-plugins` not respawning processes (#57644) are the most duplicated complaints today. A transient network blip permanently kills MCP tools until full restart.
2. **Configuration Corruption Under Stress** — `.claude.json` left empty on disk-full (#57639) is a "happened often enough" gripe. Combined with non-recursive `mkdir` crashes on plugin data dirs (#57665), these are high-frustration, low-signal bugs.
3. **Credit Consumption Without Output** — Ultrareview credits burned on 429 rate-limit failures (#57655, #57619) when zero findings were generated. Users paying for infrastructure errors.
4. **Session Fragmentation Across Worktrees** — History isolation per CWD path means orphaned sessions, broken `/resume`, and no cross-branch visibility (#58646). Long-standing pain for git worktree users.
5. **Plan-Mode Trust Erosion** — Checkbox UI persisting after plan approval causes silent mode violations (#57675). Developers can't rely on the visual indicator to know whether guardrails are active.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-05-13

## Today's Highlights
Performance and reliability issues continue to dominate the Codex community conversation. A regression in `/compact` for CLI 0.129.0 was identified and closed, while reports of high GPU usage during “thinking” animations and overall slowness persist. On the development side, several PRs lay groundwork for a unified tool execution system and better hook lifecycle support.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[Phone number verification broken](https://github.com/openai/codex/issues/20161)**  
   *Closed* – 117 comments, 86 👍  
   Users unable to add a phone or use SSO without being forced into phone verification. Closed after extensive discussion; likely a server-side fix.

2. **[5 reconnects before response in new Codex app](https://github.com/openai/codex/issues/14297)**  
   *Closed* – 33 comments  
   A persistent UI bug where the app displays “Reconnecting…” five times before answering. Impacts Free-tier users on ARM Macs.

3. **[Error after MacBook sleep](https://github.com/openai/codex/issues/3355)**  
   *Open* – 32 comments, 15 👍  
   Long-running task fails when lid is closed; `codex-cli` cannot recover the connection. Affects many CLI/remote workflows.

4. **[High GPU usage from “thinking” animation](https://github.com/openai/codex/issues/16857)**  
   *Open* – 25 comments, 29 👍  
   A tiny idle animation causes unnecessary GPU load. Users on Darwin arm64 report heat and battery drain.

5. **[/compact fails in Codex CLI 0.129.0](https://github.com/openai/codex/issues/21671)**  
   *Closed* – 15 comments, 5 👍  
   A regression introduced in the latest CLI release – the compact command sends an unknown `service_tier` parameter. Workaround: stay on 0.128.0.

6. **[Codex is really too slow](https://github.com/openai/codex/issues/21527)**  
   *Open* – 13 comments, 7 👍  
   Broad complaint about response latency in both VS Code plugin and Desktop app despite a Pro subscription.

7. **[Desktop silently hides old project conversations](https://github.com/openai/codex/issues/21128)**  
   *Open* – 9 comments, 5 👍  
   Once a conversation falls outside the recent-50 list, it becomes inaccessible through the UI. Critical for project-based working memory.

8. **[[GPT‑5.5 / Codex quality degraded in the last 2 days](https://github.com/openai/codex/issues/21942)**  
   *Closed* – 6 comments, 3 👍  
   A paying user reports noticeable drop in model reliability, threatening renewal. Highlights the impact of backend changes on developer trust.

9. **[Extensive UI flickering while working](https://github.com/openai/codex/issues/11901)**  
   *Open* – 5 comments, 10 👍  
   UI flickers continuously during code generation, making the app uncomfortable to use. Affects Plus users on Darwin.

10. **[“Model at capacity” error every day for Pro users](https://github.com/openai/codex/issues/22456)**  
    *Open* – 1 comment, 2 👍 (new today)  
    Pro users ($200/mo) hitting model capacity errors on GPT‑5.5/5.4, rendering the desktop app unusable during peak times.

## Key PR Progress

1. **[Refactor extension tools onto shared ToolExecutor](https://github.com/openai/codex/pull/22369)**  
   *Open* – Unifies extension tool authoring with core and MCP tools, reducing drift between public and internal APIs.

2. **[Add strict config parsing](https://github.com/openai/codex/pull/20559)**  
   *Open* – Opt-in strict mode catches silent typos in `config.toml` while preserving backward compatibility.

3. **[Fix unknown tool schemas (MCP)](https://github.com/openai/codex/pull/22380)**  
   *Open* – Treats schemas without a `type` as open objects instead of strings, improving flexibility for MCP tool providers.

4. **[Add managed hook suppression](https://github.com/openai/codex/pull/21577)**  
   *Closed* – Lets admins suppress noisy lifecycle notifications from managed hooks without allowing user config to hide local hooks.

5. **[Add `--dangerously-bypass-hook-trust` CLI flag](https://github.com/openai/codex/pull/21768)**  
   *Closed* – Escape hatch for headless/non‑interactive use cases where hook trust prompts block automation.

6. **[Support compact `SessionStart` hooks](https://github.com/openai/codex/pull/21272)**  
   *Open* – Ensures hooks that inject durable context (e.g., via `SessionStart`) re‑run after compaction rewrites history.

7. **[Add installed-plugin mention API](https://github.com/openai/codex/pull/22448)**  
   *Open* – New `/plugin/installed` endpoint for `@`-mention autocompletion, returning only user‑installed plugins.

8. **[Fix TUI wrapping panic for borrowed slices](https://github.com/openai/codex/pull/21235)**  
   *Open* – Prevents a panic when `textwrap` returns a slice that doesn’t point into the original text. Fixes a reported crash.

9. **[Support `updatedToolOutput` for `PostToolUse`](https://github.com/openai/codex/pull/20703)**  
   *Open* – Allows hook authors to redact or normalise tool outputs before returning them to the model.

10. **[Expose used plugin IDs in turn metadata](https://github.com/openai/codex/pull/20081)**  
    *Closed* – Adds `plugin_ids_used` to `x-codex-turn-metadata` so downstream services (e.g., Pulse) can make request-time decisions.

## Feature Request Trends
- **Per‑project configuration** – Users want `.codex/config.toml` to support MCP servers per project ([#13056](https://github.com/openai/codex/issues/13056)) and isolated chat contexts per workspace ([#17185](https://github.com/openai/codex/issues/17185)).
- **Better context‑window management** – Requests for a separate model for compaction ([#13739](https://github.com/openai/codex/issues/13739)) and persistent display of context usage ([#18101](https://github.com/openai/codex/issues/18101)).
- **UI/UX conveniences** – File browser in the Windows app ([#13646](https://github.com/openai/codex/issues/13646)), search within chat ([#8591](https://github.com/openai/codex/issues/8591)), opening chat in a separate window ([#16615](https://github.com/openai/codex/issues/16615)).
- **Cross‑device continuity** – iOS app to control a Mac‑side Codex instance ([#19681](https://github.com/openai/codex/issues/19681)).
- **Authentication improvements** – Device‑code sign‑in without WhatsApp ([#21533](https://github.com/openai/codex/issues/21533)) and support for Iranian phone numbers ([#21918](https://github.com/openai/codex/issues/21918)).

## Developer Pain Points
- **Performance** – High GPU usage from animations, general slowness, UI flickering, and choppiness with large messages are the most common complaints across all platforms.
- **Connection & reliability** – Frequent reconnects before responses, session breaks after sleep, voice transcription blocked by Cloudflare, and compaction stream disconnects.
- **Regression after updates** – The `/compact` failure in 0.129.0 and the recent quality regression in GPT‑5.5 erode trust in point‑release updates.
- **Platform restrictions** – ARM64 Windows incompatibility, GPU access blocked in WSL2 sandbox, and missing Linux sandbox device nodes.
- **Model availability** – Pro users hitting “model at capacity” errors, suggesting capacity planning hasn’t kept pace with demand.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-13

## Today's Highlights

Today's release of **v0.43.0-preview.0** introduces a surgical edit tool that steers the model toward more precise code modifications, a promising response to the community's long-standing complaints about agent slowness and bloated edits. Meanwhile, the most active issue (#22141) continues to dominate discussion with 210 comments, as users report wait times of over an hour for trivial file edits. Two parallel PRs from different contributors propose adding `gemini-2.5-flash-lite` to the default fallback chain, indicating free-tier quota exhaustion is a growing pain point.

---

## Releases

- **[v0.43.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.43.0-preview.0)**: New `feat(core): steer model to use edit tool for surgical edits` — aims to reduce unnecessary file rewrites by guiding the model toward targeted, single-block replacements. Includes a documentation fix clarifying that Auto Memory proposes, not automatically applies, memory updates.

- **[v0.42.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.42.0)**: Fixes automatic updates from switching to less stable channels. A stability-focused release.

- **[v0.42.0-nightly.20260512](https://github.com/google-gemini/gemini-cli/releases/tag/v0.42.0-nightly.20260512.gc987b9939)**: Fixes snapshotter model configuration, allows extension installation from SSH repos, and prevents duplicate session entries.

---

## Hot Issues

1. **[#22141: Gemini CLI becomes extremely slow (1+ hours) for small code-edit tasks](https://github.com/google-gemini/gemini-cli/issues/22141)**  
   *210 comments, 161 👍*  
   The most-upvoted open issue. Users report waiting 13–14 minutes for simple "why did this test fail" questions and hours for 1–3 file edits. Community suspects agent loop overhead and model response delays. Still open after two months—this is the community's top frustration.

2. **[#22920: AgentLoopContext incompatible with Config type](https://github.com/google-gemini/gemini-cli/issues/22920)**  
   *15 comments*  
   Type-level bug causing runtime failures when `deleteSession` is called. Highlights ongoing TypeScript strictness issues in the agent codebase.

3. **[#26919: Simple commands take a long time](https://github.com/google-gemini/gemini-cli/issues/26919)**  
   *12 comments, filed yesterday*  
   User reports 7-minute wait times for commit-and-push operations with Auto (Gemini 3) models. Context usage at 38% seems to amplify latency—directly related to #22141.

4. **[#24353: Robust component level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *10 comments*  
   Tracking for expanding behavioral eval tests beyond the current 76. Critical for catching regressions as the agent system grows.

5. **[#21740: Investigate impact of tracker on multiagent workflows](https://github.com/google-gemini/gemini-cli/issues/21740)**  
   *8 comments*  
   Internal investigation into whether the context tracker creates bottlenecks in multi-agent sessions.

6. **[#22745: Assess AST-aware file reads, search, and mapping (EPIC)](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *7 comments, 1 👍*  
   Proposes replacing naive file reads with AST-aware tools to reduce token usage and misaligned reads. Considered a high-impact potential performance fix.

7. **[#22323: Subagent recovery after MAX_TURNS reports false GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *6 comments, 2 👍*  
   `codebase_investigator` subagent reports `status: "success"` even when it hits max turn limit before analyzing anything. Misleading termination reasons hide real failures.

8. **[#21968: Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *6 comments*  
   Users report custom skills (e.g., gradle, git) are ignored unless explicitly instructed. The agent's tool selection logic appears too narrow.

9. **[#26563: Tool "save_memory" not found](https://github.com/google-gemini/gemini-cli/issues/26563)**  
   *5 comments*  
   Running `/memory add` fails because the tool name doesn't match the registered tool. A UX regression in the memory system.

10. **[#26972: Daily quota cap at 200 despite AI Pro subscription](https://github.com/google-gemini/gemini-cli/issues/26972)**  
    *3 comments, filed today*  
    Free-tier users hitting quota exhaustion unexpectedly; user expected much higher limits with Google AI Pro subscription.

---

## Key PR Progress

1. **[#26976: fix(core): stop replace from editing the wrong similar block](https://github.com/google-gemini/gemini-cli/pull/26976)**  
   Prevents the `replace` tool from applying edits to incorrect similar blocks when approximate matching produces multiple candidates. Directly addresses edit accuracy complaints.

2. **[#26973: feat(cli): add animated progress bar to /compress command](https://github.com/google-gemini/gemini-cli/pull/26973)**  
   User-facing improvement for the `/compress` workflow—fills asymptotically toward 90%, then snaps to completion. No new dependencies.

3. **[#26169: fix: remove unsafe exec() in app.ts](https://github.com/google-gemini/gemini-cli/pull/26169)**  
   Critical security fix: replaces `exec()` with safe alternatives in the A2A server package. Flagged by automated scanner as CRITICAL severity.

4. **[#26404: fix(telemetry): stop buffering events when telemetry is disabled](https://github.com/google-gemini/gemini-cli/pull/26404)**  
   Fixes unbounded memory growth when telemetry is off—every `log*` call was pushing closures into a never-drained buffer. Privacy and stability fix.

5. **[#26912: fix(core): detect zsh from $SHELL to prevent shopt errors](https://github.com/google-gemini/gemini-cli/pull/26912)**  
   Stops hardcoding `bash` as the shell type; reads `$SHELL` env var. Zsh users will no longer see `shopt` errors on invocation.

6. **[#26951: feat(bot): implement issue-fixer skill and mandate selection](https://github.com/google-gemini/gemini-cli/pull/26951)**  
   Adds an `issue-fixer` skill for the Gemini CLI bot, plus interactive mandate selection via workflow dispatch. Improves bot autonomy.

7. **[#26965: fix(bot): transition metrics to stable 7-day windows](https://github.com/google-gemini/gemini-cli/pull/26965) (CLOSED)**  
   Stabilizes bot metrics by switching from `last: 1` to rolling 7-day windows. Merged.

8. **[#26960: fix: resolve monorepo type errors and stabilize build](https://github.com/google-gemini/gemini-cli/pull/26960)**  
   Fixes build failures across packages by removing deprecated `baseUrl` and converting absolute imports to relative paths.

9. **[#26312: fix(core): refresh MCP OAuth token usage after re-auth](https://github.com/google-gemini/gemini-cli/pull/26312)**  
   Stops transport auth from using stale tokens after refresh. Previously required CLI restart to pick up new credentials.

10. **[#26845 / #26914: Two parallel PRs adding gemini-2.5-flash-lite to fallback chain](https://github.com/google-gemini/gemini-cli/pull/26845)**  
    Both from different contributors, same fix: add flash-lite (1000 RPD free tier) to the model fallback chain so users don't hit QUOTA_EXHAUSTED after 350 Pro/Flash requests. Duplicate effort indicates strong community demand.

---

## Feature Request Trends

- **AST-aware code understanding**: Multiple EPICs (#22745, #22746) propose replacing raw file reads with AST-aware tools for more precise method-bound extraction and codebase mapping. Expected to reduce tokens and turnaround time.

- **Enhanced model fallback chains**: The community strongly wants automatic fallback to cheaper/free-tier models (flash-lite) when quota is exhausted—evidenced by two near-identical PRs filed within 24 hours.

- **Deterministic memory system behavior**: Users want Auto Memory to properly quarantine invalid patches, stop retrying low-signal sessions, and redact secrets before sending transcripts to the model (#26523, #26522, #26525).

- **Component-level evaluation frameworks**: The team is expanding behavioral eval tests (#24353) to ensure agent sub-components (browser agent, codebase investigator) are tested systematically before releases.

---

## Developer Pain Points

- **Catastrophic slowness on small tasks**: The #1 complaint. Even simple file edits or questions trigger 10–60+ minute waits. Multiple users report the CLI "hangs" or becomes unresponsive after completing the actual work (#22141, #26919, #26970, #26915).

- **Subagent reliability and transparency issues**: Subagents report false `GOAL` success after hitting turn limits (#22323), ignore `settings.json` overrides (#22267), and run without permission after updates (#22093).

- **Memory system bugs**: The `/memory` command is broken ("save_memory" tool not found), Auto Memory retries low-signal sessions indefinitely, and invalid patches are silently skipped (#26563, #26522, #26523).

- **Token waste and runaway scripts**: Models create temporary edit scripts in random directories (#23571), and the browser agent fails on Wayland (#21983). Users report tokens consumed "insanely" even during hangs (#26970).

- **Configuration and permission friction**: Shell execution hangs with "Waiting input" after completion (#25166), `settings.json` overrides are ignored by subagents (#22267), and the automatic model selection causes indefinite "Thinking..." hangs (#26915).

---

*Data sourced from [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli). Generated 2026-05-13.*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-13

## Today's Highlights
A patch release (v1.0.47-0) landed today with improved `/diff` navigation and better `--resume` support for cloud agent sessions, alongside a fix for PowerShell detection. However, **v1.0.46 introduced a critical native-binding regression** affecting MCP servers, session persistence, and Linux systems — driving several high-priority bug reports. The community is also actively requesting richer session management features like `/fork` and `/pause`.

## Releases
**v1.0.47-0** (latest, 2026-05-13)
- **Added:** `j/k` keybindings for up/down navigation in `/diff` view.
- **Improved:** `--resume` now handles Copilot cloud agent sessions where the agent hasn't pushed any branch changes yet.

**v1.0.46** (2026-05-12)
- Warns users when the CLI version is deprecated (premium model access may be lost).
- Fixes PowerShell startup when `pwsh` is installed as a .NET global tool shim.
- Long lines in diff view now wrap at terminal width instead of being truncated.
- Adds support for read-only `gh` CLI commands (list, view).

## Hot Issues (Top 10)

1. **#2058 — [area:sessions] Add /fork command** *(Comments: 9, 👍: 7)*  
   Users want a `/fork` to branch a conversation for side-questions without derailing the main agent objective. High community demand for non-destructive context switching.  
   [Link](https://github.com/github/copilot-cli/issues/2058)

2. **#1433 — [area:context-memory] COPILOT_CUSTOM_INSTRUCTIONS_DIRS broken on Linux with NFS** *(Comments: 7, 👍: 6)*  
   Persistent frustration: custom AGENTS.md files on NFS mounts are ignored despite correct env var configuration. Affects Linux users working on shared filesystems.  
   [Link](https://github.com/github/copilot-cli/issues/1433)

3. **#3281 — [area:mcp] v1.0.46 MCP server startup fails with “Cannot find native binding”** *(Comments: 3, 👍: 0)*  
   Critical regression: after upgrading to v1.0.46, users see `Failed to start MCP Servers` due to a missing npm optional dependency. Several users confirming the same error.  
   [Link](https://github.com/github/copilot-cli/issues/3281)

4. **#3259 — [area:platform-windows] PowerShell detection broken in v1.0.45 (fixed in 1.0.46)** *(Comments: 3, 👍: 1)*  
   Closed as fixed, but highlights the fragility of shell detection — particularly for `dotnet tools`-installed `pwsh`.  
   [Link](https://github.com/github/copilot-cli/issues/3259)

5. **#2818 — [area:authentication] Session token expires mid-task** *(Comments: 3, 👍: 5)*  
   Long-running autopilot sessions fail abruptly with “Session token expired. Please resend your message.” Users want automatic token refresh for multi-hour workflows.  
   [Link](https://github.com/github/copilot-cli/issues/2818)

6. **#3041 — [area:authentication] Copilot Cloud Agent gets intermittent access denied errors** *(Comments: 1, 👍: 1)*  
   Cloud agent mode fails on `git push` and GitHub API calls despite correct tokens — unclear whether OAuth scopes or token rotation is the root cause. Blocks automated issue processing.  
   [Link](https://github.com/github/copilot-cli/issues/3041)

7. **#3257 — [area:networking] HTTP MCP servers fail with `TypeError: fetch failed` after idle period** *(Comments: 1, 👍: 0)*  
   TCP connection pooling causes stale connections to be reused after NAT/firewall idle timeouts. No automatic reconnection logic.  
   [Link](https://github.com/github/copilot-cli/issues/3257)

8. **#3283 — [area:platform-linux] GLIBC_2.33 required but not available on older Linux (Ubuntu)** *(Comments: 0, 👍: 0)*  
   v1.0.46’s native `runtime.linux-x64-gnu.node` binary requires newer glibc symbols, breaking on Ubuntu systems with GLIBC < 2.33.  
   [Link](https://github.com/github/copilot-cli/issues/3283)

9. **#3279 — [area:agents] “Copilot Lies” — agent makes verbal commitments without enforcing actions** *(Comments: 0, 👍: 0)*  
   Agent says “from now on I’ll only X” but doesn’t write rules or call tools to persist the promise. Misleading for users who expect stateful behavior.  
   [Link](https://github.com/github/copilot-cli/issues/3279)

10. **#3265 — [area:agents] Add a /pause or /stop command to gently interrupt an agent** *(Comments: 0, 👍: 0)*  
    Users want a non-destructive interrupt to pause an agent mid-reasoning (e.g., “stop after this thought”), rather than canceling and losing progress.  
    [Link](https://github.com/github/copilot-cli/issues/3265)

## Key PR Progress

Only **2 pull requests** were updated in the last 24 hours:

1. **#772 — Add installation script** *(Closed)*  
   Adds a `curl | bash` installation path for easier onboarding. Addresses issue #771 (no install script).  
   [Link](https://github.com/github/copilot-cli/pull/772)

2. **#2587 — Add automated issue classification with GitHub Agentic Workflows** *(Closed)*  
   Introduces an AI-powered workflow that auto-tags new issues with `area:` and `triage` labels using `gh-aw`. Aims to reduce manual triage overhead for maintainers.  
   [Link](https://github.com/github/copilot-cli/pull/2587)

*Note: Activity appears light on the PR side today, likely due to the team responding to the v1.0.46 regressions.*

## Feature Request Trends

The most-requested feature directions from recent issues include:

- **Session forking and pausing** – multiple users want `/fork` to branch conversations and `/pause` to non-destructively interrupt agents (e.g., #2058, #3265).
- **Persistent behavioral rules** – users want agents to write and follow explicit rules, not just “promise” behavior (#3279).
- **Multiple BYOK model support** – current single-model env var is limiting; users want in-session model switching (#3282).
- **Shell command discoverability** – the `!` prefix for shell commands is hard to discover; users want a `/shell` or `/exec` slash command (#3261).
- **Timing and progress indicators** – users want per-response elapsed time and better progress feedback during long autopilot runs (#3278).

## Developer Pain Points

**1. v1.0.46 native-binding regression**  
The most acute pain today. Upgrading to v1.0.46 breaks MCP servers, session persistence, and even basic startup on Linux systems with older glibc (Ubuntu, Rocky Linux). The root cause is an npm optional dependency issue that forces users to reinstall or downgrade.  
*Related issues: #3281, #3287, #3280, #3283, #3276*

**2. Session token expiration during long tasks**  
Users running autopilot for hours hit “Session token expired” errors with no automatic refresh (#2818). Combined with the cloud agent’s intermittent access-denied errors (#3041), this makes unattended workflows unreliable.

**3. Context corruption from side-questions**  
When an agent is pursuing a multi-step objective and the user asks a quick question, the agent derails its entire context. The lack of `/fork` forces users to restart sessions from scratch (#2058).

**4. MCP connection fragility**  
HTTP MCP servers fail after idle periods due to stale TCP connections (#3257), and the authentication flow for MCP servers provides misleading “Authorization successful” messages even when the flow actually failed (#3269).

**5. Silent model substitution**  
Background agents sometimes silently swap the requested model without warning (#3266). Users only discover the substitution by inspecting metadata, undermining trust in agent behavior.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-13

## Today’s Highlights
**Release 1.43.0** shipped with improved UI spacing, link highlighting, and a polished telemetry schema. A critical report of the K2.6 model being overloaded under normal load (Issue #2077) continues to draw attention, while the community rallied around a long-requested **Shift+Enter** newline shortcut — now implemented in PR #2255. Several memory-leak and connection-pool fixes landed to improve stability.

## Releases
**[v1.43.0](https://github.com/MoonshotAI/kimi-cli/releases/tag/v1.43.0)**
- `feat(ui)`: shell spacing, link highlighting, notification duration improvements
- `feat(telemetry)`: event schema with outcome enum, lifecycle tracking, error enrichment

## Hot Issues (10 selected)

1. **[#2077 – K2.6 model overloaded – unusable under normal load](https://github.com/MoonshotAI/kimi-cli/issues/2077)** (Critical, updated today)  
   Users on Allegretto membership report the K2.6 model constantly returns retry errors. 6 comments, high frustration.

2. **[#778 – API Error: 400 "Invalid request Error"](https://github.com/MoonshotAI/kimi-cli/issues/778)** (Open, updated today, 16 comments)  
   Persistent invalid-request error on Windows with `claude-sonnet-4-5-20250929`. Long-standing issue with no fix yet.

3. **[#1925 – Kimi K2.5 vs K2.6 – request to allow model switching](https://github.com/MoonshotAI/kimi-cli/issues/1925)** (Open, 10 comments)  
   Community feedback that K2.6 "drowns out creativity" and increases hallucinations. Wants system prompt from K2.5 back.

4. **[#2251 – MCP stdio server stderr leaks break TUI rendering after upgrading to 1.43.0](https://github.com/MoonshotAI/kimi-cli/issues/2251)** (New bug, 0 comments)  
   macOS users see TUI glitches after the 1.43.0 update, caused by stderr pollution from MCP servers.

5. **[#2258 – Bundled CLI unavailable. Please install manually](https://github.com/MoonshotAI/kimi-cli/issues/2258)** (New bug, Windows 10)  
   After upgrading to 1.43.0, CLI cannot find bundled binary. Affects Windows users.

6. **[#1947 – kimi code support OAI-compatible copilot](https://github.com/MoonshotAI/kimi-cli/issues/1947)** (Open, 4 comments)  
   Users want to use Kimi Code through VS Code Copilot’s OAI-compatible endpoint. Request keeps resurfacing.

7. **[#1585 – Feature Request: customizable keybinding for inserting newlines (Shift+Enter)](https://github.com/MoonshotAI/kimi-cli/issues/1585)** (Open, 3 comments, 2 👍)  
   Long-standing ask from March. The proposed `Ctrl+J` is deemed unintuitive. Now partially addressed by PR #2255.

8. **[#2247 – Theme Mode Diff Render Error](https://github.com/MoonshotAI/kimi-cli/issues/2247)** (New bug, K2.6)  
   Diff display broken in certain theme modes after 1.43.0. No workaround yet.

9. **[#2256 – Official Co-authored-by trailer with branded GitHub avatar](https://github.com/MoonshotAI/kimi-cli/issues/2256)** (New feature request)  
   Suggests automatic `Co-authored-by` git trailer for AI-assisted commits, backed by a verified GitHub account.

10. **[#2252 – Add /goal command and allow coding plan import into Codex](https://github.com/MoonshotAI/kimi-cli/issues/2252)** (New enhancement)  
    References Claude Code’s `/goal` feature; wants Kimi Code to support similar project-level goal commands and interoperability with Codex.

## Key PR Progress (10 selected)

1. **[#2246 – `--prompt-interactive` option](https://github.com/MoonshotAI/kimi-cli/pull/2246)** (Open)  
   Adds `-P` flag to pass an initial prompt while keeping interactive session alive. Resolves #2240.

2. **[#2236 – Fix broadcast queues and web store cache memory leaks](https://github.com/MoonshotAI/kimi-cli/pull/2236)** (Open)  
   Bounds `BroadcastQueue` and caps `_sessions_cache` to prevent OOM under heavy use.

3. **[#2255 – Support Shift+Enter for inserting newlines](https://github.com/MoonshotAI/kimi-cli/pull/2255)** (Open)  
   Adds the most-demanded shortcut, closing #2254 and related requests. Community has been asking since March.

4. **[#2231 – Reuse TCPConnector to prevent connection leaks](https://github.com/MoonshotAI/kimi-cli/pull/2231)** (Open)  
   Introduces `_ConnectionPool` to reuse HTTP connections across tool calls, reducing file-descriptor churn.

5. **[#2249 – Unified approval modes with toolbar badges and temporary toasts](https://github.com/MoonshotAI/kimi-cli/pull/2249)** (Open)  
   Consolidates four auto-approval methods (`--yolo`, `--afk`, `/yolo`, `/afk`) into a single UI with badges and toasts.

6. **[#2245 – Improve provider error UX across 429 surfaces](https://github.com/MoonshotAI/kimi-cli/pull/2245)** (Open)  
   Centralizes rate-limit error formatting; distinguishes transient 429 from quota exhaustion with friendly messages.

7. **[#2242 – Tool call deduplication for same-step and cross-step repeats](https://github.com/MoonshotAI/kimi-cli/pull/2242)** (Merged)  
   Prevents redundant tool executions when the model issues identical calls, boosting efficiency.

8. **[#2244 – Bump to 1.43.0](https://github.com/MoonshotAI/kimi-cli/pull/2244)** (Merged)  
   Release automation: version bump and changelog move.

9. **[#2248 – Implement `/loop` recurring prompt scheduler](https://github.com/MoonshotAI/kimi-cli/pull/2248)** (Merged)  
   New slash command for scheduling prompts using cron expressions, with jitter and config models.

10. **[#2187 – Bump pillow to 12.2.0 for CVE-2026-25990](https://github.com/MoonshotAI/kimi-cli/pull/2187)** (Merged)  
    Fixes out-of-bounds write vulnerability in PSD image loading. Closes #2153.

## Feature Request Trends
- **OpenAI-compatible API**: Multiple issues (#1947, #2208) ask for Kimi Code to act as a drop-in replacement for OpenAI endpoints in tools like VS Code Copilot and Cursor.
- **Model flexibility**: Strong demand to switch between K2.5 and K2.6 (#1925), preserve older system prompts, and avoid regressions in creativity.
- **Improved keybindings**: Shift+Enter for newlines (#1585, #2254) is the most 👍-ed request, finally addressed.
- **Project-level commands**: `/goal` and integration with Codex (#2252) show desire for structured planning workflows.
- **Git integration**: Co-authored-by trailers (#2256) and better commit attribution.

## Developer Pain Points
- **K2.6 reliability**: Frequent overload errors (HTTP 429/503) make the flagship model unusable for some subscribers (#2077).
- **API error ambiguity**: Broad "Invalid request Error" (#778) with no actionable details, still unresolved after months.
- **Upgrade regressions**: Each release introduces new TUI bugs — MCP stderr leaks (#2251), missing CLI binary on Windows (#2258), diff rendering issues (#2247).
- **Memory leaks**: Unbounded queues and caches (#2236) cause OOM under sustained use.
- **Dependency security**: Old `pillow` version with CVE (#2153) blocked installations in secure environments.
- **Customization gaps**: No support for custom keybindings beyond basic shortcuts (#1585).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-13

## Today’s Highlights
No new releases landed in the past 24 hours, but the community remains highly active with 50 issues and 50 PRs updated. The most critical open thread (#13768) now has 65 comments as users struggle with Opus 4.6 prefill errors, while a flurry of bug reports related to the v1.14.48 desktop build — including connection drops and image recognition regressions — suggests a spotty rollout. On the PR side, contributors are pushing a systematic overhaul of error handling across the provider, session, and worktree layers, moving from generic middleware to typed Effect errors.

## Releases
None in the last 24 hours.

## Hot Issues

1. **[Issue #13768: “This model does not support assistant message prefill” with Opus 4.6](https://github.com/anomalyco/opencode/issues/13768)**  
   *65 comments, 27 👍*  
   A persistent blocker for Copilot users – sessions abort mid-conversation. Community is frustrated because the error forces them to restart sessions and avoid the model altogether.

2. **[Issue #6209: Cannot scroll on opencode when using iTerm2](https://github.com/anomalyco/opencode/issues/6209)**  
   *21 comments, 18 👍*  
   TUI scrolling breaks in iTerm2 – the input box scrolls but not the output. High impact for macOS developers who rely on terminal mode.

3. **[Issue #11532: AGENTS.md not loaded after /new](https://github.com/anomalyco/opencode/issues/11532)**  
   *18 comments, 14 👍*  
   Starting a fresh session with `/new` does not reload the project’s `AGENTS.md`. Users must manually ask the model to re-read it, breaking workflow automation.

4. **[Issue #22528: How to turn off sound effects and animations in 1.4.4](https://github.com/anomalyco/opencode/issues/22528)**  
   *14 comments, 42 👍*  
   A new splash animation and sound shipped without documentation or toggle – community backlash is strong, with 42 upvotes demanding a disable option.

5. **[Issue #7790: Feature request – SSH-based remote server connections to OpenCode Desktop](https://github.com/anomalyco/opencode/issues/7790)**  
   *12 comments, 53 👍*  
   The highest-upvoted feature request. Users want to connect the desktop app to a remote `opencode` server over SSH, enabling a cloud‑like experience.

6. **[Issue #7006: `permission.ask` plugin hook is defined but not triggered](https://github.com/anomalyco/opencode/issues/7006)**  
   *9 comments, 12 👍*  
   The plugin hook for auto‑approving permissions exists in documentation but never fires. Plugin authors are blocked from building custom approval flows.

7. **[Issue #26230: Double compaction for Copilot Opus 4.7](https://github.com/anomalyco/opencode/issues/26230)**  
   *9 comments, 1 👍*  
   Recent updates cause token usage to double every time compaction runs when using Opus 4.7, wasting money and context.

8. **[Issue #12553: Windows installer should detect CPU capabilities (AVX2)](https://github.com/anomalyco/opencode/issues/12553)**  
   *6 comments, 1 👍*  
   The Windows x64 binary requires AVX2 but crashes silently on older CPUs (Ivy Bridge, Sandy Bridge). No baseline fallback exists.

9. **[Issue #19267: Agent stuck in infinite loop with Minimax-2.7](https://github.com/anomalyco/opencode/issues/19267)**  
   *5 comments, 0 👍*  
   Sessions with Minimax models get infinitely compacted, making the agent unusable. Also affects Minimax-2.5 across all modes.

10. **[Issue #17769: Session state stale after device sleep/resume – heartbeat mismatch](https://github.com/anomalyco/opencode/issues/17769)**  
    *3 comments, 5 👍*  
    After laptop lid close or phone lock, the web UI shows stuck sessions and “Unable to retrieve session”. SSE disconnect due to heartbeat timing.

## Key PR Progress

1. **[PR #27301: fix(provider): type auth errors](https://github.com/anomalyco/opencode/pull/27301)**  
   Converts OAuth and validation failures from generic middleware to tagged Effect errors, improving debuggability.

2. **[PR #7156: feat: add agent default variant handling in TUI and desktop](https://github.com/anomalyco/opencode/pull/7156)**  
   Closes #22065 – respects an agent’s configured model variant instead of falling back to the default.

3. **[PR #19543: feat(tui): add /clear command to clear session messages](https://github.com/anomalyco/opencode/pull/19543)**  
   Adds a TUI `/clear` that removes all messages without changing the session – requested by many workflow-heavy users.

4. **[PR #27055: chore: add low TPS model alerts](https://github.com/anomalyco/opencode/pull/27055)**  
   Implements alerts when a model’s throughput drops below a threshold, helping users avoid slow providers.

5. **[PR #27298: fix(router): stabilise hash for no-repo sessions](https://github.com/anomalyco/opencode/pull/27298)**  
   Fixes a bug where sessions without a repo URL got a random UUID per call, causing PVC/Pod references to fail.

6. **[PR #27296: fix(worktree): type expected errors](https://github.com/anomalyco/opencode/pull/27296)**  
   Moves worktree error handling to tagged Effect errors, preserving legacy response shape for backward compatibility.

7. **[PR #18767: feat(app): Mobile Touch Optimization](https://github.com/anomalyco/opencode/pull/18767)**  
   Large PR optimising the app for mobile/touch devices while keeping the desktop experience intact.

8. **[PR #27249: docs(ecosystem): add theSaver plugin to ecosystem page](https://github.com/anomalyco/opencode/pull/27249)**  
   Adds a cost‑aware delegation enforcer plugin to the official ecosystem directory.

9. **[PR #27291: fix(session): make message reads effectful](https://github.com/anomalyco/opencode/pull/27291)**  
   Makes `MessageV2.page/get` the canonical Effect APIs and removes transitional wrappers, improving type safety.

10. **[PR #26178: fix(session): exclude orphaned interrupted tools from run-loop continuation](https://github.com/anomalyco/opencode/pull/26178)**  
    Prevents infinite loops by marking orphaned `tool_use` calls as `error` with `interrupted: true` after a stream retry.

## Feature Request Trends

The community’s top direction is **remote connectivity**: the SSH server feature (#7790) leads with 53 👍, and related requests for better network resilience (e.g., enterprise proxy support) appear in comments.  

**Context management** is the second theme: users want `AGENTS.md` to persist across `/new` (#11532) and to support a global `~/.claude/CLAUDE.md` (#259).  

**Performance and stability** requests centre on compaction behaviour (avoiding double compaction, safer abort handling) and baseline CPU detection for Windows.  

**UX customisation** – especially disabling sound effects/animations (#22528) – has strong community backup, indicating the new splash screen was poorly received.

## Developer Pain Points

- **Copilot model incompatibility**: The “assistant message prefill” error (#13768) blocks Opus 4.6 entirely, forcing users to downgrade or switch providers.
- **Windows fragility**: Binary crashes on CPUs without AVX2 (#12553) and CRLF/symlink false modifications (#27276) make Windows adoption unreliable.
- **CJK input bugs**: `@` file mentions fail after Chinese characters (#27293) and autocomplete does not support Chinese (#27290), hurting non‑Latin users.
- **Unreliable plugin hooks**: The `permission.ask` hook (#7006) is documented but broken – plugin authors cannot trust the extension system.
- **Connection drops**: Frequent disconnect after sleep (#17769) and the v1.14.48 local server disconnection (#27018, #26839) frustrate desktop users.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-13

## Today's Highlights
A major dependency cleanup sweep landed today, removing 17 lockfile entries by vendorizing small utilities. The project remains in an active refactoring phase, with many issues auto-closed under the `closed-because-refactor` label, signaling a broader codebase cleanup. A security alert was raised regarding a compromised Mistral npm package (2.2.4), though the project remains on the unaffected 2.2.1 version.

## Releases
No new releases in the last 24 hours. The latest published version remains Pi 0.74.

## Hot Issues

1. **[#3299 — Add "max" thinking level for Opus 4.7 parity](https://github.com/earendil-works/pi/issues/3299)** [CLOSED]
   Proposes extending pi's thinking ladder to `off / minimal / low / medium / high / xhigh / max` to match Opus 4.7's five-rung API. Community interest is moderate (9 comments). This follows the pattern of #143 which added `xhigh` for Codex max.

2. **[#4251 — Kimi k2.6 on OpenCode fails with "reasoning_content is missing"](https://github.com/earendil-works/pi/issues/4251)** [OPEN]
   A provider compatibility bug where Kimi k2.6 returns a 400 error when thinking is enabled but the reasoning_content field is absent. 7 comments, still unresolved. Important for users relying on this provider.

3. **[#4210 — Bedrock converse-stream: empty end_turn treated as successful stop](https://github.com/earendil-works/pi/issues/4210)** [CLOSED]
   Bedrock occasionally returns null object responses instead of throwing, causing agents to silently stop. User built a local extension to remediate. 7 comments, auto-closed due to bigrefactor.

4. **[#4290 — Messages aborted for length treated as regular stops](https://github.com/earendil-works/pi/issues/4290)** [OPEN]
   Thinking turns silently stop when hitting length limits, with only a "Thinking..." indicator misleading users. 5 comments, still open. A UX hazard that wastes developer time.

5. **[#4430 — Errors (write, edit, read) during long sessions (>70k context)](https://github.com/earendil-works/pi/issues/4430)** [CLOSED]
   User reports consistent failures with sessions exceeding 70-90k context across multiple model quantizations and servers. 5 comments. Suggests a fundamental scalability issue.

6. **[#4319 — Use explicit fences for AGENTS.md in system prompt](https://github.com/earendil-works/pi/issues/4319)** [OPEN]
   Proposes wrapping project context files in explicit code fences (`~~~`) to prevent LLM confusion. 4 comments. A clean, low-cost fix for prompt engineering hygiene.

7. **[#4413 — getTextOutput crashes when tool result has no content array](https://github.com/earendil-works/pi/issues/4413)** [CLOSED]
   `TypeError: Cannot read properties of undefined (reading 'filter')` crashes the TUI when built-in tools return error results without a content field. 4 comments. A crash-on-error scenario that degrades UX.

8. **[#4222 — Maximum call stack size exceeded in Markdown renderer](https://github.com/earendil-works/pi/issues/4222)** [CLOSED]
   Large markdown content causes `RangeError` due to the spread operator limitation (65,536 elements) in JS engines. 3 comments. Now fixed by PR #4463.

9. **[#4432 — Mistral package 2.2.4 compromised](https://github.com/earendil-works/pi/issues/4432)** [CLOSED]
   Security alert — Mistral npm package 2.2.4 was compromised. The project pinned at 2.2.1 is unaffected. 3 comments, 1 👍.

10. **[#4342 — ANTHROPIC_AUTH_TOKEN causes 401 for non-Anthropic providers](https://github.com/earendil-works/pi/issues/4342)** [OPEN]
    The Anthropic SDK auto-reads `ANTHROPIC_AUTH_TOKEN` and sends it alongside `x-api-key`, causing 401 errors for providers like Xiaomi MiMo. 3 comments. An env var collision that blocks multi-provider setups.

## Key PR Progress

1. **[#4467 — chore(deps): Kill small dependencies](https://github.com/earendil-works/pi/pull/4467)** [CLOSED] — by mitsuhiko
   Removes 4 direct deps (`extract-zip`, `file-type`, `strip-ansi`, `uuid`) and 17 lockfile entries by vendorizing small utilities. Direct impact on install size and supply chain risk.

2. **[#4461 — fix(tui): place image correctly when viewport height < image height](https://github.com/earendil-works/pi/pull/4461)** [OPEN] — by haoqixu
   Fixes image rendering offset by removing error-prone cursor-up/down sequences. The kitty image `C=1` flag already disables cursor moving, making the dance unnecessary.

3. **[#4463 — Fix(tui): Make markdown.ts more robust to larger markdown files](https://github.com/earendil-works/pi/pull/4463)** [CLOSED] — by herrnel
   Fixes #4222 by replacing spread operator usage with `Array.from()` or loops to avoid the 65,536-argument limit in V8/JSC.

4. **[#4458 — Add Windows ARM64 Binary Output](https://github.com/earendil-works/pi/pull/4458)** [OPEN] — by brianmichel
   Adds native Windows ARM64 binary builds. Requires Bun 1.3.10+. Important for Surface Pro X and other ARM Windows users.

5. **[#4452 — chore(coding-agent): add publish shrinkwrap](https://github.com/earendil-works/pi/pull/4452)** [OPEN] — by mitsuhiko
   Hard-pins all dependencies in the published npm package. Mitigates supply chain attacks like the Mistral 2.2.4 incident.

6. **[#4379 — fix(tui): render checkboxes in to-do list items](https://github.com/earendil-works/pi/pull/4379)** [CLOSED] — by Perlence
   Markdown to-do lists now render with visible checkboxes instead of blank space. A small but visible UX fix.

7. **[#4383 — fix(coding-agent) docs: update tool configuration API](https://github.com/earendil-works/pi/pull/4383)** [CLOSED] — by maximilianzuern
   Updates SDK documentation from deprecated `readTool`/`bashTool` factories to modern `createAgentSession({ tools })` API.

8. **[#4391 — fix(coding-agent): dispose SDK example sessions](https://github.com/earendil-works/pi/pull/4391)** [CLOSED] — by yzhg1983
   Ensures SDK examples clean up sessions when using `websocket-cached` transport, preventing zombie Node processes.

9. **[#4426 — fix(coding-agent): restore terminal on uncaught exception](https://github.com/earendil-works/pi/pull/4426)** [CLOSED] — by ofa1
   Adds an uncaught exception handler that calls `ui.stop()` to restore raw-mode stdin and cursor. Prevents broken terminals after crashes.

10. **[#4446 — fix(openai-codex): repair raw control chars in SSE/WebSocket frames](https://github.com/earendil-works/pi/pull/4446)** [CLOSED] — by raedkhasawneh
    Replaces bare `JSON.parse` with a tolerant parser that handles U+0000–U+001F control characters in agent tool output. Prevents parse failures on real-world traffic.

## Feature Request Trends

- **Extended thinking ladder**: Strong demand for additional thinking levels (`max`) to match competing APIs (Opus 4.7, Codex). Multiple issues reference ladder parity.
- **Better provider compatibility**: Requests for AirLLM support, Xiaomi MiMo fixes, Harmony response format handling, and more robust env var handling for multi-provider setups.
- **GUI client**: A formal request for a graphical interface alongside the existing TUI, citing user preference for non-terminal workflows.
- **Extension API improvements**: Requests for typed cross-extension service calls (beyond event bus), model filtering APIs, and provider registration queries.
- **Offline/first-class local model support**: Cannot-start-without-internet bug and AirLLM request both point to demand for disconnected workflows.

## Developer Pain Points

- **Long session instability**: Sessions exceeding 70-90k context consistently trigger write/edit/read errors, regardless of model or server.
- **Silent failures**: "length aborted" messages treated as normal stops, empty `end_turn` from Bedrock, and missing `reasoning_content` errors all cause silent agent halts.
- **Dependency and supply chain friction**: Mistral 2.2.4 compromise, broken `pi install github:REPO@COMMIT` with tags, and zero-byte dot-files appearing after updates.
- **Environment variable collisions**: `ANTHROPIC_AUTH_TOKEN` conflicting with non-Anthropic providers; `ANTHROPIC_BASE_URL` not respected for the Anthropic provider.
- **TUI rendering fragility**: Stack overflow with large markdown, image rendering offset, checkbox disappearance, and terminal corruption on uncaught exceptions.
- **Provider-specific edge cases**: Harmony `<|channel|>` tokens corrupting tool call names, Codex raw control chars breaking JSON parsing, and macOS clipboard dependency not bundled in bun-compiled binaries.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-05-13

## Today's Highlights
A busy day for Qwen Code with the **v0.15.11 release** bringing a significant performance optimization for session-list metadata reads. The community is actively discussing **daemon mode** (stage 1 already merged), **runaway protection for headless mode**, and several **security fixes** including a ReDoS vulnerability patch. New feature requests around **git worktree support**, **atomic file writes**, and **project-local context files** signal growing enterprise use cases.

## Releases
**Latest: v0.15.11** (also v0.15.11-preview.2, v0.15.10-preview.1, nightly)
- **perf(core):** Bound session-list metadata reads to head/tail 64KB; pool buffer; lazy message count – reduces memory footprint and I/O for long-running code sessions.
- **test:** Stabilized main end-to-end tests.
- [View release notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.11)

## Hot Issues (Top 10 Noteworthy)

1. **#3803 – Daemon mode (qwen serve) proposal** – A comprehensive 14-chapter design series for running Qwen Code as a background service. Stage 1 already merged; PR #4113 advances to “1 daemon = 1 workspace”. High community interest (👍1, 4 comments).  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/3803)

2. **#3730 – Auto stop task after update** – Users report that Qwen Code spontaneously stops tasks without ESC key press, causing data loss. 7 comments, needs more information. Critical for reliability.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/3730)

3. **#4035 – DashScope-intl fetch failure** – `fetch` fails on international DashScope endpoint due to incompatible undici dispatcher. Affects international users. 4 comments, 👍1.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4035)

4. **#4089 – Context window bug** – Setting model context size in `settings.json` to 262K tokens is ignored; `/context detail` shows 1M. Core configuration issue. 3 comments.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4089)

5. **#4111 – SessionStart hook output not injected** – `additionalContext` and `systemMessage` from SessionStart hook are lost due to missing `getAdditionalContext()` call. Internal Alibaba team report; affects hook-driven workflows. 2 comments.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4111)

6. **#4098 – `/compress` not working** – Context compression command shows a tip but does nothing when invoked. Session management pain point. 2 comments.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4098)

7. **#4033 – High power usage while idle** – Tool agent uses excessive CPU waiting for external processes (downloads, compilations). Feature request for idle throttling. 2 comments.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4033)

8. **#4093 – Command substitution denial inconsistency** – Security check for shell injection is applied inconsistently, with some compound commands bypassing the filter. Opaque to users. 1 comment.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4093)

9. **#4095 – Atomic file write & transaction rollback** – `fs.writeFile` leaves corrupted files on crash; codebase already has TODO comments. Request for transactional writes. 1 comment.  
   [Issue link](https://github.com/QwenLM/qwen-code/issues/4095)

10. **#4103 – Headless mode lacks runaway protection** – `--prompt` and `--yolo` modes have no configurable execution budgets (turn limits, timeouts). 0 comments but directly addressed by PR #4105.  
    [Issue link](https://github.com/QwenLM/qwen-code/issues/4103)

## Key PR Progress (Top 10 Important)

1. **#4112 – Fix ReDoS in DashScope URL check** – Replaces regex with `URL.hostname` to fix a CodeQL‑flagged polynomial Redos vulnerability. Critical security fix.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4112)

2. **#4113 – Daemon: 1 workspace per daemon** – Stage 2 of the daemon design (#3803). Changes multi‑workspace routing to single‑workspace isolation for simpler lifecycle.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4113)

3. **#4105 – Headless runaway-protection guardrails** – Adds `--max-turns`, `--max-time`, `--max-steps` and approval budget to headless mode. Closes #4103.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4105)

4. **#4073 – Generic git worktree support** – Two new tools (`enter_worktree`, `exit_worktree`) plus agent isolation parameter. Enables safe parallel coding sessions.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4073)

5. **#4088 – Session-scoped `/goal` command** – Pins a condition (e.g., “test passes”) and uses LLM judge to auto‑continue turns until met. Powerful for iterative coding.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4088)

6. **#4101 – Strip inline media in compaction summaries** – Prevents images/PDFs from bloating context during `/compress`, improving quality and saving tokens.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4101)

7. **#4064 – File restoration in `/rewind`** – Adds file‑copy backup (inspired by Claude Code) so `/rewind` can optionally roll back assistant‑modified files. Closes #3697.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4064)

8. **#3994 – Progressive MCP availability** – Speeds up first prompt by making MCP discovery non‑blocking. Measurable TTI improvement for users with multiple MCP servers.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/3994)

9. **#4109 – Fix context‑usage footer for Anthropic** – Accounts for prompt cache tokens and uses `promptTokenCount` instead of `totalTokenCount`. Improves accuracy for Claude‑compatible providers.  
   [PR link](https://github.com/QwenLM/qwen-code/pull/4109)

10. **#4097 – Hierarchical session tracing** – Implements proper `interaction → llm_request/tool → tool.execution` spans with AsyncLocalStorage, aligning with Claude Code’s beta tracing.  
    [PR link](https://github.com/QwenLM/qwen-code/pull/4097)

## Feature Request Trends
- **Daemon / Service Mode** – Multiple PRs and issues around `qwen serve`, single‑workspace daemon, and background session management.
- **Security & Guardrails** – Demand for config‑based runaway protection, consistent command‑substitution denial, and OAuth removal (e.g., #4108 dropping OpenRouter OAuth).
- **Session & File Management** – Batch session deletion (#3706), `/rewind` file rollback, atomic file writes (#4095), and `QWEN.local.md` for per‑user context (#4091).
- **User Experience** – TAB completion for `/model` (#4029), status‑line presets (#4087), OSC‑8 hyperlinks for clickable URLs (#3954), and quiet‑restore (#4079).
- **Observability & Telemetry** – Production‑ready OpenTelemetry (#3731), hierarchical tracing (#4097), and improved context‑usage metrics (#4109).

## Developer Pain Points
- **Stability regressions** – Auto‑stop task (#3730) and session‑compression not working (#4098) erode trust in updates.
- **Configuration friction** – Context window override ignored (#4089), DashScope international endpoint broken (#4035), and custom API key setup is confusing (#3582).
- **High resource usage** – Excessive CPU while waiting for external processes (#4033) is a common complaint.
- **Inconsistent security** – Command‑substitution denial bypass (#4093) and lack of headless run limits (#4103) worry CI/CD users.
- **Missing power features** – No native atomic file writes (#4095), hooks not injecting context (#4111), and `/model` lacks TAB completion (#4029).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*