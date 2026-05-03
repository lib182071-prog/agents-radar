# AI CLI Tools Community Digest 2026-05-03

> Generated: 2026-05-03 03:50 UTC | Tools covered: 8

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
**Date:** 2026-05-03 | **Analyst:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tool landscape in early May 2026 is characterized by **intense reliability and cost-transparency pressure** across all major players. Community trust has been shaken by billing bugs, opaque session-window depletion, and context-compaction failures that undermine the core value proposition of “infinite” agentic sessions. At the same time, a clear **feature convergence** is emerging: every tool is racing to support multiple providers, MCP (Model Context Protocol) ecosystems, and plugin-based extensibility. The week’s digest reveals a market shifting from early-adopter enthusiasm to enterprise-grade demands: predictable costs, robust sandboxing, Windows parity, and auditable agent behavior. Smaller tools (Kimi Code, OpenCode, Pi, Qwen Code) are aggressively closing feature gaps with incumbents, while incumbents (Claude Code, Codex, Copilot CLI, Gemini CLI) are grappling with scaling pains from rapid adoption.

---

## 2. Activity Comparison

| Tool | Issues Updated (Last 24h) | PRs Updated (Last 24h) | Release Status | Notable Activity |
|------|---------------------------|------------------------|----------------|------------------|
| Claude Code | ~10 hot issues | 7 PRs (2 open, 5 closed) | No new release (latest v2.1.126) | Billing bugs dominate; one critical bug closed fast |
| OpenAI Codex | 10 hot issues | 10 PRs (mix open/closed) | No new release | Heavy feature requests (1M context, LSP) |
| Gemini CLI | 10 hot issues | 10 PRs (6 open, 4 merged) | No new release | Windows reliability PR major news |
| GitHub Copilot CLI | 10 hot issues | 0 PRs in 24h | No new release | Session management bugs flood |
| Kimi Code CLI | 9 issues | 3 PRs (1 open, 2 closed) | No new release (v1.41.0) | Windows crash, skill recursion PR |
| OpenCode | 10 hot issues | 10 PRs (mix open/closed) | **2 releases** (v1.14.32, v1.14.33) | High patch velocity, Effect refactoring |
| Pi | 10 hot issues | 10 important PRs | **1 release** (v0.72.1) | Provider additions, keyboard fixes |
| Qwen Code | 10 hot issues | 10 key PRs | **1 nightly release** (v0.15.6-nightly) | DeepSeek V4 fixes, retry logic |

**Key observations:**
- OpenCode shipped two releases in 24 hours – the fastest iteration cadence.
- GitHub Copilot CLI had zero PR activity, signaling a possible development lull or bottleneck.
- Pi had the highest raw count of issues (nearly 40) and PRs (23) updated, indicating strong community engagement.
- Claude Code and Codex are the most-watched repositories, with highest upvotes and comments per issue.

---

## 3. Shared Feature Directions

Across the eight tools, the following requirements appear in **two or more communities**:

### 3.1 Multi-Provider / Model Switching
- **Gemini CLI**: Vertex AI region override, model switching in-session
- **Codex**: `/fast` tiers, structured service tiers via model metadata
- **Pi**: NVIDIA NIM, Xiaomi MiMo, Together AI provider additions
- **Qwen Code**: DeepSeek V4 support, `/model` switch command
- **Kimi Code**: Growing demand for multi-model quota display

### 3.2 MCP (Model Context Protocol) Ecosystem
- **Claude Code**: MCP transport bugs, scrollable `/mcp` list
- **Copilot CLI**: `.mcp.json` not loading regression, server management UX
- **Kimi Code**: Lazy-load MCP tool schemas
- **OpenCode**: Cursor CLI integration interest (related to tool interoperability)
- **Gemini CLI**: ACP mode (Agent Communication Protocol) disconnect fixes

### 3.3 Context Window / Compaction Reliability
- **Claude Code**: Context leaks from advisor calls, session window squeeze
- **Codex**: Compaction failures, usage limit depletion
- **Copilot CLI**: Deadlocks related to hooks (indirectly context-related)
- **OpenCode**: Compaction not running on time
- **Pi**: Compaction deletes everything (critical bug)
- **Qwen Code**: Subagent context auto-compact fix

### 3.4 Session Branching / Forking / History Management
- **Copilot CLI**: #1313 (session branching) – most requested feature
- **OpenCode**: Session persistence, fork/resume UX
- **Codex**: Session picker redesign (PR #20065)
- **Claude Code**: Session history fragility (VS Code restart, IPC crashes)
- **Kimi Code**: Approval persistence across session resumes

### 3.5 Keyboard / Locale / Terminal Compatibility
- **Pi:** Italian, Ukrainian, Bépo keyboard regressions
- **Codex:** Russian keyboard breaks dictation paste
- **Copilot CLI:** Hardcoded `pwsh.exe` on Windows
- **Claude Code:** Windows subprocess isolation docs
- **Kimi Code:** Windows `NoneType` crash on path completion
- **Gemini CLI:** Windows startup hangs, zombie processes

### 3.6 Plugin / Extension / Hook Systems
- **Claude Code:** Skill aliases, multi-account MCP
- **Copilot CLI:** Plugin marketplace improvements
- **Kimi Code:** Hook system (permission-based), `UserPromptSubmit` bug
- **OpenCode:** Plugin hooks for model routing
- **Pi:** Filesystem override hook, TypeBox migration
- **Qwen Code:** Background task management, monitors

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Differentiator |
|------|---------------|-------------|-------------------------|
| **Claude Code** | Cost transparency, agent isolation, MCP ecosystem | Power users, enterprise teams | Anthropic's prompt engineering; subagent sandboxing (PID isolation); `--dangerously-skip-permissions` |
| **OpenAI Codex** | IDE parity, large context, service tiers | Professional developers, heavy GPT-5.5 users | GPT-5.5 with 1M context ambition; LSP auto-install; `/side` conversations; Plan mode |
| **Gemini CLI** | Agent evaluation, AST-aware tooling, memory routing | Google Cloud / Vertex AI users | Gemini 3 models; ACP for IDE integration; task-based evaluations; versioned pre-write backups |
| **Copilot CLI** | Remote sessions, session branching, reasoning effort | GitHub ecosystem, enterprise orgs | Tight Copilot integration; `/remote` for org repos; reasoning effort per model |
| **Kimi Code** | Extensibility, skill discovery, Codex compatibility | Developers migrating from Claude Code | Recursive skill loading; pseudo-cwd in shell; approval persistence |
| **OpenCode** | Fast iteration, Effect-native architecture, custom providers | Early adopters, plugin developers | Effect v4 refactoring; `packages/llm` foundation; 2 releases/day cadence |
| **Pi** | Provider diversity, keyboard layout support | International users, open-source enthusiasts | 50+ free NVIDIA NIM endpoints; Kitty Keyboard Protocol; Light/dark theme |
| **Qwen Code** | SDK standardization, retry robustness, ACP mode | Chinese-speaking developers, multi-provider users | FileReadCache; background tasks; nightly releases |

**Key differentiators:**
- **Claude Code** leads on agent isolation and cost transparency (despite billing bugs).
- **Codex** is the most ambitious on context window size and IDE integration.
- **Gemini CLI** has the strongest focus on safety (destructive behavior detection, versioned backups).
- **Copilot CLI** is the only tool explicitly targeting **org repositories** for remote sessions.
- **Kimi Code** and **OpenCode** are the most active in closing feature parity gaps with incumbents.
- **Pi** and **Qwen** focus on **provider diversity** and **non-English user experience**.

---

## 5. Community Momentum & Maturity

| Tool | Community Size (Reactions per Issue) | Iteration Speed (PRs/day) | Maturity Level | Risk Observed |
|------|---------------------------------------|---------------------------|----------------|---------------|
| Claude Code | High (194 👍 on top issue) | Moderate (7 PRs/24h) | **Mature** – stable release, but billing trust issue | High – billing bugs erode trust |
| OpenAI Codex | Very High (294 👍 on LSP issue) | High (10 PRs/24h) | **Maturing** – core stable, feature velocity high | Medium – context compaction flaky |
| Gemini CLI | Medium (3 👍 typical) | High (10 PRs/24h) | **Maturing** – evaluation framework expanding | Medium – Windows reliability poor |
| GitHub Copilot CLI | Medium (12 👍 typical) | Low (0 PRs/24h) | **Stable but stagnant** – regression risk | High – session deadlocks, unresolved old bugs |
| Kimi Code CLI | Low (few 👍) | Low (3 PRs/24h) | **Early stage** – version 1.41.0, catching up | Medium – Windows crash critical |
| OpenCode | Medium (161 👍 on top issue) | Very High (10 PRs/24h, 2 releases) | **Rapid iteration** – v1.14.x, heavy refactoring | Low – fast fixes, but architectural changes risky |
| Pi | Medium (8 comments typical) | Very High (23 PRs/24h) | **Rapid iteration** – v0.72.x, strong OSS community | Medium – keyboard regressions, compaction bug |
| Qwen Code | Low (few 👍) | High (10 PRs/24h, nightly releases) | **Rapid iteration** – v0.15.x, focused on reliability | Low – DeepSeek compatibility, but responsive fixes |

**Insights:**
- **OpenCode** and **Pi** have the highest degree of community-driven development (many outside contributors).
- **Copilot CLI** shows signs of stagnation (zero PRs) despite many open bugs – a risk for GitHub’s enterprise foothold.
- **Claude Code** remains the most **community-trusted** in terms of features, but the billing fiasco is a trust-breaking event.
- **Gemini CLI** is investing heavily in **agent evaluation** (76 tests, expansion epic) – a sign of enterprise maturity.
- **Qwen Code** targets a different demographic (Chinese-speaking, multi-provider) and is growing rapidly with nightly releases.

---

## 6. Trend Signals

### 6.1 Cost Transparency Becomes Table Stakes
The Claude Code HERMES.md billing bug and Codex/Gemini quota depletion issues signal a **critical industry pain point**: users demand per-request cost breakdowns, predictable session windows, and no silent overages. Expect all major tools to ship usage dashboards and cost warnings within the next quarter.

### 6.2 MCP / ACP Standardization Pressure
MCP bugs appear across Claude Code, Copilot CLI, and Kimi Code – the protocol is still fragile. Meanwhile, Gemini CLI's ACP (Agent Communication Protocol) and OpenCode’s Effect-native architecture suggest a **divergence between Anthropic's MCP and Google/OpenAI's proprietary protocols**. Community demand for multi-protocol support is inevitable.

### 6.3 Windows Parity Is a Dealbreaker
Reports of Windows crashes, sandbox failures, `pwsh.exe` hardcoding, and terminal compatibility issues are legion across all tools. With developer adoption broadening beyond macOS/Linux, Windows support is no longer optional – it’s a competitive differentiator. Tools that ignore Windows (Copilot CLI’s lingering `pwsh.exe` bug) will lose enterprise deals.

### 6.4 Agent Safety & Auditability
False-positive subagent results (Gemini), dangerous git commands (Gemini), context leaks (Claude Code), and ignored deny permissions (OpenCode) highlight a **growing trust gap in autonomous agent behavior**. Versioned pre-write backups, rollback capabilities, and explicit destructive-action prompts are becoming expected features, not nice-to-haves.

### 6.5 Keyboard / Locale Accessibility Gaps
Pi’s cluster of keyboard layout bugs and Codex’s Russian keyboard issue signal that **AI CLI tools are still predominantly designed for US English users**. As tools globalize, input normalization (e.g., abstracting Ctrl+<letter> mappings) will be a recurring engineering challenge.

### 6.6 IDE Integration Wars
Codex’s LSP auto-install (#8745, 294 👍) and `/ide` command, Copilot CLI’s remote sessions, and Gemini CLI’s ACP mode (JetBrains, Zed) indicate a **race to embed AI CLI capabilities into IDEs**. The winner will offer seamless back-and-forth between terminal and editor without context loss. OpenCode’s Cursor CLI support request (#2072) further confirms this trend.

### 6.7 SDK / Release Pipeline Standardization
Qwen Code’s push for unified release notes and network timeouts in its Python/TypeScript SDKs mirrors a broader industry need: **AI CLI tools are becoming platforms with SDKs**. The community is demanding professional-grade DevOps – automated changelogs, versioned APIs, and reliable CI/CD.

### 6.8 Smaller Players Outpacing Incumbents on Velocity
OpenCode (2 releases/day) and Pi (23 PRs/day) are iterating far faster than Claude Code (0 releases) and Copilot CLI (0 PRs). This suggests that **nimble, open-source-backed tools can close feature gaps quickly**, while incumbents risk stagnation if they don’t maintain velocity. The “fast follower” strategy is paying off for Kimi Code and Qwen Code, which are explicitly targeting Codex and Claude Code compatibility.

---

**Final Recommendation:** For technical decision-makers evaluating AI CLI tools for their team, the landscape is highly fragmented but converging on reliability, cost transparency, and cross-platform support. **Prioritize tools with active Windows fixes, explicit cost monitoring, and MCP/ACP support.** OpenCode and Qwen Code offer the fastest iteration, while Claude Code and Codex provide the most mature feature sets – albeit with emerging trust risks.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-05-03 | Source: github.com/anthropics/skills*

> **Note:** Comment counts for PRs were reported as `undefined` in the source data. Rankings below are based on observable engagement indicators including update recency, discussion depth inferred from PR descriptions and review activity, and cross-referencing with related Issues.

---

## 1. Top Skills Ranking

### #1: Document Typography Quality Control (#514)
- **Functionality:** Prevents orphan word wrap, widow paragraphs (section headers stranded at page bottoms), and numbering misalignment in AI-generated documents — issues that affect nearly every document Claude produces.
- **Discussion Highlights:** Addresses a universal pain point for users who generate reports or long-form content. The skill resonates because typographic quality is rarely requested explicitly but consistently degrades output professionalism.
- **Status:** OPEN (Created 2026-03-04, Updated 2026-03-13)
- **Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

### #2: Skill Quality Analyzer & Skill Security Analyzer (#83)
- **Functionality:** Meta-skills that evaluate other Skills across five dimensions (structure, documentation, examples, resources, security posture). A quality assurance framework for the ecosystem itself.
- **Discussion Highlights:** Represents a maturing ecosystem — the community is now building tools to standardize and police skill quality. This indicates the repository has passed critical mass.
- **Status:** OPEN (Created 2025-11-06, Updated 2026-01-07)
- **Link:** [PR #83](https://github.com/anthropics/skills/pull/83)

### #3: Frontend Design Skill Clarity Overhaul (#210)
- **Functionality:** Complete revision of the frontend-design skill to ensure every instruction is concrete, actionable within a single conversation, and specific enough to steer Claude's behavior reliably.
- **Discussion Highlights:** Reflects a broader community concern that some Skills are written for humans (educational tone) rather than for Claude (imperative execution instructions). The verbosity-vs-actionability tension is a recurring theme.
- **Status:** OPEN (Created 2026-01-05, Updated 2026-03-07)
- **Link:** [PR #210](https://github.com/anthropics/skills/pull/210)

### #4: Testing Patterns Skill (#723)
- **Functionality:** Comprehensive testing coverage spanning Testing Trophy philosophy, unit testing (AAA pattern), React component testing with Testing Library, integration testing (Playwright/Cypress), and accessibility testing.
- **Discussion Highlights:** Addresses a major gap — testing guidance was previously absent from the official Skills collection. The PR's scope (full-stack testing) and its thoroughness have generated sustained attention.
- **Status:** OPEN (Created 2026-03-22, Updated 2026-04-21)
- **Link:** [PR #723](https://github.com/anthropics/skills/pull/723)

### #5: Sensory Skill — Native macOS Automation (#806)
- **Functionality:** Teaches Claude to use `osascript` (AppleScript) for native macOS automation as an alternative to screenshot-based computer use. Two-tier permission system: Tier 1 works out of the box, Tier 2 requires Accessibility permissions.
- **Discussion Highlights:** Innovative approach to a longstanding pain point — screenshot-based computer use is slow and brittle. AppleScript automation offers a more reliable, accessible path. The permission tiering design is a thoughtful safety addition.
- **Status:** OPEN (Created 2026-03-29, Updated 2026-04-02)
- **Link:** [PR #806](https://github.com/anthropics/skills/pull/806)

### #6: Shodh-Memory — Persistent Context for AI Agents (#154)
- **Functionality:** Persistent memory system that maintains context across conversations. Teaches Claude when to surface relevant memories, how to structure rich context entries, and how to use proactive context retrieval on every user message.
- **Discussion Highlights:** Addresses one of the most fundamental limitations of conversational AI — context windows. The skill effectively gives Claude a long-term memory layer, which has high potential for complex multi-session workflows.
- **Status:** OPEN (Created 2025-12-19, Updated 2026-03-03)
- **Link:** [PR #154](https://github.com/anthropics/skills/pull/154)

### #7: ServiceNow Platform Skill (#568)
- **Functionality:** Broad ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD/CSM, SPM/PPM, Vulnerability Response, Security Incident Response, CSDM, and IntegrationHub.
- **Discussion Highlights:** Enterprise-focused skill with unusually broad platform coverage. Extended discussion around scope boundaries — some community members questioned whether a single skill should cover this much surface area versus being split into specialized sub-skills.
- **Status:** OPEN (Created 2026-03-08, Updated 2026-04-23)
- **Link:** [PR #568](https://github.com/anthropics/skills/pull/568)

### #8: HADS — Human-AI Document Standard (#616)
- **Functionality:** Lightweight Markdown convention for writing technical documentation that serves both human and AI readers without maintaining separate files. Addresses the reality that AI models increasingly read documentation before humans do.
- **Discussion Highlights:** Thought-provoking discussion about documentation standards for the AI era. The concept of "AI-first" documentation signals a paradigm shift in how technical content is authored.
- **Status:** OPEN (Created 2026-03-12, Updated 2026-03-31)
- **Link:** [PR #616](https://github.com/anthropics/skills/pull/616)

---

## 2. Community Demand Trends

### 🔴 Most Anticipated New Skill Directions

**1. Organizational Skill Sharing & Management**
- Issue [#228](https://github.com/anthropics/skills/issues/228) (9 comments, 👍7) — "Enable org-wide skill sharing in Claude.ai" is the most-upvoted open feature request. Users are forced to download `.skill` files and share via Slack/Teams. A shared skill library or direct sharing link is the #1 requested platform capability.

**2. Skill Quality & Best-Practice Tooling**
- Issue [#202](https://github.com/anthropics/skills/issues/202) (8 comments) — "skill-creator should be updated to best practice" argues the existing skill-creator reads like developer documentation rather than operational instructions. The community wants meta-skills that teach *how to write good Skills*.
- Issue [#532](https://github.com/anthropics/skills/issues/532) (2 comments) — skill-creator's description optimizer requires `ANTHROPIC_API_KEY`, making it unusable for enterprise/SSO users.

**3. Platform & Ecosystem Expansion**
- Issue [#16](https://github.com/anthropics/skills/issues/16) (4 comments) — "Expose Skills as MCPs" proposes using the Model Context Protocol as a standard interface for Skills, enabling programmatic access to Skill capabilities.
- Issue [#29](https://github.com/anthropics/skills/issues/29) (4 comments) — "Usage with Bedrock" asks for AWS Bedrock compatibility, indicating enterprise demand for Claude Code Skills outside Anthropic's direct hosting.

**4. Security & Trust Boundaries**
- Issue [#492](https://github.com/anthropics/skills/issues/492) (4 comments, 👍2) — "Security: Community skills distributed under anthropic/ namespace enable trust boundary abuse" raises legitimate concerns about namespace confusion where community skills appear official.
- Issue [#412](https://github.com/anthropics/skills/issues/412) (4 comments) — Proposal for an agent-governance skill covering safety patterns, policy enforcement, and audit trails.

**5. Reliability & Bug Fixing Urgency**
- Issue [#62](https://github.com/anthropics/skills/issues/62) (10 comments) — "All my skills have disappeared" — 12 complex skills vanished. Highest comment count of any issue.
- Issue [#556](https://github.com/anthropics/skills/issues/556) (6 comments, 👍6) — `run_eval.py` has 0% skill trigger rate across all queries. The evaluation tooling is fundamentally broken.

**6. Duplicate Content & Install Bloat**
- Issue [#189](https://github.com/anthropics/skills/issues/189) (5 comments, 👍7) — "document-skills and example-skills plugins install identical content, causing duplicate skills." Users are experiencing context window waste from redundant skill installations.

---

## 3. High-Potential Pending Skills

These active PRs show sustained discussion and recent updates — likely to merge soon:

| PR | Skill | Last Updated | Why It Might Land Soon |
|----|-------|-------------|------------------------|
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 2026-04-21 | Addresses a clear ecosystem gap (no testing skill existed); extensive and well-structured |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | 2026-03-13 | Universal pain point; low complexity to merge; solves an issue every user experiences |
| [#806](https://github.com/anthropics/skills/pull/806) | sensory (macOS automation) | 2026-04-02 | Innovative approach with clear safety design; addresses screenshot-CUA performance complaints |
| [#568](https://github.com/anthropics/skills/pull/568) | ServiceNow | 2026-04-23 | Enterprise demand is high; broad scope but well-organized; sustained updates suggest active maintenance |
| [#616](https://github.com/anthropics/skills/pull/616) | HADS (document standard) | 2026-03-31 | Novel concept with growing interest; low implementation complexity |
| [#486](https://github.com/anthropics/skills/pull/486) | ODT (OpenDocument) | 2026-04-14 | Fills a format gap (LibreOffice/OpenOffice); clear triggers and comprehensive template handling |
| [#210](https://github.com/anthropics/skills/pull/210) | frontend-design revision | 2026-03-07 | Improves an existing skill rather than adding new surface area — lower friction to merge |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for skills that improve Claude's output quality (typography, testing, documentation standards) and enable enterprise-scale usage (organizational sharing, platform integrations, security governance), with a growing parallel demand for meta-tooling that standardizes how skills themselves are built, evaluated, and distributed.**

---

# Claude Code Community Digest — 2026-05-03

## Today's Highlights

A major billing bug (Issue #53262) exploded this week, where the string `HERMES.md` in commit messages silently routed requests to extra usage billing — draining $200+ from a Max plan user. Meanwhile, users report a sudden 5–10× faster session window burn starting April 29 (Issue #55053), sparking widespread concern. No new releases landed in the last 24 hours, but the queue of open cost-related bugs is now the community's top pain point.

## Releases

No new releases in the last 24 hours. The latest stable version remains **2.1.126** (based on issue references).

## Hot Issues (10 Noteworthy)

1. **[#53262 — HERMES.md in git commit messages causes extra usage billing](https://github.com/anthropics/claude-code/issues/53262)**  
   *CLOSED* | 91 comments, 194 👍  
   A shocking bug: if your repo's commit history contains the string `HERMES.md` (case-sensitive), Claude Code routes all API requests to "extra usage" billing instead of the Max plan's included quota. One user silently burned $200. Closed rapidly by Anthropic, but the root cause (fragile string matching in billing routing) remains a trust concern.

2. **[#55053 — Sudden 5-hour session window squeeze starting Apr 29](https://github.com/anthropics/claude-code/issues/55053)**  
   *OPEN* | 29 comments, 11 👍  
   Since April 29 evening, the 5-hour session window depletes 5–10× faster for the same work. Light editing (scp, Read, small Edit) burns 20–25% of the window in under an hour. Likely tied to Sonnet sub-agent cost increases or a backend change. No official response yet.

3. **[#36024 — Support multiple Gmail accounts in MCP integration](https://github.com/anthropics/claude-code/issues/36024)**  
   *OPEN* | 16 comments, 42 👍  
   Top feature request: Gmail MCP only supports one connected account. Many users need personal + work simultaneously. Highly upvoted, no movement yet.

4. **[#14362 — Sonnet model consuming both "All models" AND "Somente Sonnet" limits](https://github.com/anthropics/claude-code/issues/14362)**  
   *OPEN* | 14 comments, 15 👍  
   Long-standing billing double-counting bug on Windows. Still unaddressed after 5 months.

5. **[#52908 — "You've hit your org's monthly usage limit" erroneously](https://github.com/anthropics/claude-code/issues/52908)**  
   *OPEN* | 13 comments, 6 👍  
   False positive usage limit errors for org users. Frustrating for teams relying on Claude Code in CI.

6. **[#37765 — --dangerously-skip-permissions doesn't bypass .claude/ directory write prompts](https://github.com/anthropics/claude-code/issues/37765)**  
   *CLOSED* | 13 comments, 12 👍  
   Flag that claims to skip permissions still blocks `.claude/` setting writes. Closed — likely will be fixed in next release.

7. **[#30958 — v2.1.69: thinking summaries empty in transcript and TUI](https://github.com/anthropics/claude-code/issues/30958)**  
   *OPEN* | 11 comments, 10 👍  
   Undocumented behavior change: thinking summaries are missing from transcripts. Users rely on these for debugging and traceability.

8. **[#46465 — Harness system-reminder phrasing indistinguishable from prompt injection](https://github.com/anthropics/claude-code/issues/46465)**  
   *OPEN* | 5 comments  
   Claude Code's internal `<system-reminder>` includes "NEVER mention this reminder to the user" — the classic sign of a prompt injection attack. Security/transparency concern.

9. **[#55488 — Spawned subagent identifies as "team-lead" and exposes parent conversation](https://github.com/anthropics/claude-code/issues/55488)**  
   *OPEN* | 4 comments  
   Privacy/security bug: a spawned subagent, when DM'd directly, claims to be the team lead and reveals the parent's full conversation history. Serious for enterprise use.

10. **[#55702 — Advisor call re-injects full executor transcript, doubling context window usage](https://github.com/anthropics/claude-code/issues/55702)**  
    *CLOSED* | 1 comment  
    Fresh today: `/advisor` sends the whole transcript again, instantly jumping from ~485k to 971k tokens on a 1M context model. Root cause of many "context limit" crashes. Closed quickly — fix expected soon.

## Key PR Progress (All 7 PRs in last 24h)

1. **[#55484 — Dashboard improvements](https://github.com/anthropics/claude-code/pull/55484)**  
   *CLOSED* | Created May 2 | Merged quickly. Likely fixes for billing dashboard accuracy.

2. **[#41447 — Open source Claude Code ✨](https://github.com/anthropics/claude-code/pull/41447)**  
   *OPEN* | Has been open since March 31. Claims to close several high-profile feature requests (#59, #456, #2846, #22002, #41434). Still pending review — a potential game-changer if merged.

3. **[#20448 — Add web4-governance plugin](https://github.com/anthropics/claude-code/pull/20448)**  
   *OPEN* | Since Jan 23. Adds AI governance with trust tensors and audit trails. Low activity, but conceptually interesting for regulated environments.

4. **[#36594 — Add remote-control plugin](https://github.com/anthropics/claude-code/pull/36594)**  
   *CLOSED* | Added `/remote-control` command for guided session setup, diagnostics, connection guidance. Useful for mobile/browser use.

5. **[#36592 — Add comprehensive skill library across three new plugins](https://github.com/anthropics/claude-code/pull/36592)**  
   *CLOSED* | Three plugins with 20+ skills covering API development, document processing, and examples. Good for onboarding.

6. **[#36562 — Add CLAUDE_CODE_GIT_BASH_PATH env var for Windows](https://github.com/anthropics/claude-code/pull/36562)**  
   *CLOSED* | Windows usability improvement — allows overriding Git Bash path for non-standard installations.

7. **[#46025 — Docs: Linux subprocess isolation and CLAUDE_CODE_SCRIPT_CAPS](https://github.com/anthropics/claude-code/pull/46025)**  
   *CLOSED* | Documents PID namespace isolation and new env vars for subprocess hardening. Important for enterprise deployments.

## Feature Request Trends

- **Multi-account MCP support** (Gmail, Google Workspace) — #36024 leads with 42 👍. Users want to connect personal + work accounts simultaneously.
- **Skill aliases** — #54487 proposes `aliases` in SKILL.md frontmatter so that verbose skill names (e.g., `/skaile-dev-git`) can have shortcuts.
- **Open source** — #41447 PR (still open) would make Claude Code source-available, addressing a long-standing community desire for transparency and custom builds.
- **Remote control/browser-based Claude Code** — #53437 reports bugs with the new "try it out" web version, but the feature itself is highly desired.
- **Improved agent isolation** — Multiple issues (#55708, #55709) ask for stronger subagent sandboxing (git worktree isolation, correct docstrings).

## Developer Pain Points

- **Billing and cost bugs dominate.** Three separate billing issues in the top 10 (HERMES.md, session window squeeze, org limits). Community trust is shaken — users feel they can't predict costs.
- **Session window behavior is opaque.** The 5–10× faster depletion without any changelog entry (#55053) is driving frustration. Users want per-request cost breakdowns.
- **Context window leaks from advisors and subagents.** #53065, #55702 show that advisor and subagent calls re-inject full transcripts, doubling token usage and triggering premature compaction.
- **Prompt injection phrasings in system reminders** (#46465) create a transparency problem — users can't distinguish safe system messages from malicious injections.
- **Session history fragility.** Issues #54186 (VS Code restart loses history), #53281 (IPC crash on desktop), #55704 (Samba network drives lose history) show that local persistent storage is unreliable across platforms.
- **MCP transport bugs.** #55495 (HTTP transport ignores path component), #55705 (`/mcp` list not scrollable), #54513 (duplicate MCP processes) hurt the growing MCP ecosystem.
- **Permission model bypasses.** Even with `--dangerously-skip-permissions`, some writes to `.claude/` still blocked (#37765); older bypass via command chaining (#13371) still a concern.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-03

## Today’s Highlights
The community continues to push for a larger context window, with the **1M-token GPT-5.5** request hitting 141 reactions and 112 comments. Meanwhile, **LSP auto‑detect + auto‑install** for Codex CLI (#8745) remains the most upvoted open enhancement (294 👍), reflecting strong demand for IDE‑grade intelligence. Windows stability is a recurring pain point—several reports detail **Browser Use failures** on Windows due to an app‑server path error, while a new PR introduces **structured service tiers** to replace hardcoded `/fast` commands.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 Picks)

1. **[#19464 – Support 1M token context for GPT-5.5 in Codex](https://github.com/openai/codex/issues/19464)**  
   *112 comments, 141 👍* – The most active feature request. Users want parity with the API’s 1M context limit; the current 400K in Codex feels restrictive for large‑project analysis.

2. **[#8745 – LSP integration (auto-detect + auto-install) for Codex CLI](https://github.com/openai/codex/issues/8745)**  
   *46 comments, 294 👍* – Top‑voted enhancement. Proposed built‑in Language Server Protocol support to bring richer diagnostics and symbol navigation to the CLI.

3. **[#19585 – Pro weekly usage limit depletes unusually fast on GPT-5.5](https://github.com/openai/codex/issues/19585)**  
   *25 comments* – Pro users report faster‑than‑expected quota consumption, compounded by unstable context compaction. Impacts heavy users of Codex with GPT-5.5.

4. **[#8259 – Format Markdown tables to be human‑readable in TUI](https://github.com/openai/codex/issues/8259)**  
   *25 comments, 98 👍* – Generated tables have misaligned whitespace, making them hard to read in terminal. A new PR (#20252) now addresses this directly.

5. **[#10090 – `elevated_windows_sandbox` causes all agent commands to fail](https://github.com/openai/codex/issues/10090)**  
   *16 comments* – On Windows, the sandbox fails with `CreateProcessAsUserW failed: 5`, producing no output. Blocks all agent usage for affected users.

6. **[#17827 – Customizable status line (like Claude Code)](https://github.com/openai/codex/issues/17827)**  
   *12 comments, 17 👍* – Request for a user‑configurable bottom bar showing token usage, model, rate limits, etc. Mirrors a popular Claude Code feature.

7. **[#17508 – Compaction/Autocompaction fails](https://github.com/openai/codex/issues/17508)**  
   *10 comments* – Context compaction sometimes silently fails, leading to bloated sessions. Impact on users who rely on long‑running threads.

8. **[#20048 – Windows Desktop Browser Use fails to start app-server](https://github.com/openai/codex/issues/20048)**  
   *9 comments* – One of several Windows‑specific Browser Use issues (see also #19365, #19450, #20206, #20661). The bundled Node app‑server fails to launch with “os error 3”.

9. **[#20552 – View > Toggle File Tree is unreliable on macOS](https://github.com/openai/codex/issues/20552)**  
   *8 comments* – The menu command doesn’t always reveal the file tree in the desktop app, an annoyance for users who rely on sidebar navigation.

10. **[#20161 – Codex asks for a phone number on SSO login](https://github.com/openai/codex/issues/20161)**  
    *35 comments, 31 👍* – When logging in via SSO on a new device, Codex demands a phone number. Users who never added one are locked out.

## Key PR Progress (10 Picks)

1. **[#20838 – Pause goals while in Plan mode](https://github.com/openai/codex/pull/20838)**  
   Prevents `/goal` from appearing active when Plan mode blocks autonomous continuation. Fixes the awkward UX where `/goal resume` could fail.

2. **[#20824 – Drive TUI service‑tier commands from model metadata](https://github.com/openai/codex/pull/20824)**  
   Builds slash commands (e.g., `/fast`) dynamically from the active model’s `serviceTiers` metadata, replacing hardcoded variants.

3. **[#20822 – Use structured service tiers across core and app‑server](https://github.com/openai/codex/pull/20822)**  
   Adds `ModelServiceTier` metadata with structured `{ id, name, description }`. Improves configurability and deprecates old `additionalSpeedTiers` fields.

4. **[#20252 – Render responsive Markdown tables in TUI](https://github.com/openai/codex/pull/20252)**  
   Directly addresses the community’s top table readability issue (#8259). Preserves raw Markdown source to re‑render on terminal resize.

5. **[#20819 – Add raw scrollback mode to TUI](https://github.com/openai/codex/pull/20819)**  
   Introduces a plain‑text output mode for easier copy‑pasting of partial responses, solving a long‑standing granular copy complaint.

6. **[#20065 – Redesign session picker (resume/fork)](https://github.com/openai/codex/pull/20065)**  
   Replaces the fixed table with compact, responsive cards. Adds full‑text search across thread names, IDs, branches, and working directories.

7. **[#20815 – Speed up `/side` parent restore replay](https://github.com/openai/codex/pull/20815)**  
   Optimizes thread‑snapshot replay when returning from a side conversation, drastically reducing time for long threads.

8. **[#20744 – Fix flaky `request_permissions` test on macOS](https://github.com/openai/codex/pull/20744)**  
   Stabilises a core test that was failing non‑deterministically due to ambient config inheritance.

9. **[#20825 – Read cached metadata for installed Git plugins](https://github.com/openai/codex/pull/20825)**  
   Populates `plugin/list` with metadata from cached Git‑sourced marketplace plugins, preserving category precedence.

10. **[#20619 – Request desktop attestation before protected requests](https://github.com/openai/codex/pull/20619)**  
    Adds a v2 `attestation/generate` server request. Ensures fresh attestation is supplied for compaction and realtime setup promises.

## Feature Request Trends

- **Context expansion** – #19464 (1M‑token GPT-5.5) is the top‑voted enhancement; users want API parity.
- **IDE integration** – LSP auto‑detect/auto‑install (#8745), `/ide` command to attach to active IDE (#13834), and workspace/editor context.
- **TUI polish** – Customizable status line (#17827), responsive Markdown tables (#8259), raw scrollback mode, session picker redesign.
- **Service tier flexibility** – Structured model metadata for tier selection (#20822, #20824) and in‑session `/profile` commands (#20635).
- **Image generation parameters** – Request to expose size, quality, format in `image_gen` tool (#20839).
- **Plugin ecosystem** – Richer marketplace metadata and Git plugin caching (#20825).

## Developer Pain Points

- **Windows sandbox and Browser Use failures** – Multiple reports (#10090, #20048, #19365, #20206, #20661) of `app-server` failing with “os error 3” on Windows, blocking agent execution.
- **Authentication friction** – Phone number requirement on SSO (#20161), refresh token exhaustion (#17340), inability to switch accounts (#18638).
- **Performance regressions** – Slow thread switching on macOS (#20802), high CPU from MCP server renderer (#20435), app freezes on Windows (#20214).
- **Context compaction instability** – Failures (#17508) and unexplained usage limit depletion (#19585) reduce trust in long sessions.
- **Locale‑sensitive bugs** – Russian keyboard breaks dictation paste (#19710); Markdown tables are unreadable for all.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-05-03

## Today’s Highlights
A major Windows reliability PR (#26392) lands to address startup hangs, zombie processes, and subagent execution loops – a direct response to community frustration (#26393). The team continues to push toward agent robustness, with a critical bug (#22323) where subagents report “success” after hitting their turn limit still under active discussion. On the feature front, AST-aware file reading and memory routing between global and project scopes (#22745, #22819) are moving from investigation to implementation.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#22323 – Subagent recovery after MAX_TURNS reports success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   `codebase_investigator` subagent claims `status: "success"` even when it exhausted all turns before doing any work. A P1 priority with 2👍 – the community is concerned about false negatives in agent reports.

2. **[#24916 – Gemini CLI keeps asking for permissions on the same file](https://github.com/google-gemini/gemini-cli/issues/24916)**  
   Permission prompts persist across sessions despite “allow for all future”. A security/UX issue that breaks workflow.

3. **[#25166 – Shell command execution gets stuck with “Waiting input” after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   High community reaction (3👍). Simple CLI commands hang, showing “Awaiting user input” after the process has finished.

4. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   Epic (P1/area-agent) to expand the behavioral evaluation framework beyond the existing 76 tests. Signals a systematic push for quality assurance.

5. **[#22745 – Assess the impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   Epic exploring AST-aware tools for precise method bounds, reduced turn count, and lower token noise. 1👍, with follow-up issues already tracking implementation (e.g., #22746).

6. **[#26393 – Multiple reliability issues on Windows and subagent execution loops](https://github.com/google-gemini/gemini-cli/issues/26393)**  
   Filed today, detailing Windows startup hang (minutes-long WMI scanning), zombie processes, and subagent loops. The community is seeking urgent Windows support.

7. **[#24246 – 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   Encountering a 400 error when more than 128 tools are enabled. Suggests the agent lacks tool-scoping logic – a scalability concern for large projects.

8. **[#22819 – Implement memory routing: global vs. project](https://github.com/google-gemini/gemini-cli/issues/22819)**  
   Proposes storing preferences in `~/.gemini/` and codebase-specific context in `.gemini/`. 2👍 – the community wants smarter, context-aware memory.

9. **[#22672 – Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
   Reports of the model issuing `git reset --force` or similar dangerous commands when safer alternatives exist. Safety-critical with 1👍.

10. **[#22186 – get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)**  
    P1 bug: the output summary hook crashes the CLI just before completion. Repeated occurrence, impacts productivity.

## Key PR Progress
1. **[#26392 – fix(windows): Resolve hangs, zombie processes, and improve subagent reliability](https://github.com/google-gemini/gemini-cli/pull/26392)**  
   Open. Directly addresses #26393. Replaces WMI scanning with a faster process enumeration and fixes subagent loop termination.

2. **[#25633 – fix(core): record response's modelVersion in session transcript](https://github.com/google-gemini/gemini-cli/pull/25633)**  
   Merged (closed). Fixes #25632: now logs the actual model served (important for A/B routing and per-model telemetry).

3. **[#26361 – fix(core): externalize https-proxy-agent to fix proxy support](https://github.com/google-gemini/gemini-cli/pull/26361)**  
   Open. Resolves `TypeError: HttpsProxyAgent is not a constructor` by bundling the proxy agent correctly. Essential for enterprise users.

4. **[#25684 – fix(config): use flash-lite for utility model configs to preserve quota](https://github.com/google-gemini/gemini-cli/pull/25684)**  
   Open. Switches internal utility tools from `gemini-3-flash-preview` to `3.1-flash-lite` to avoid quota exhaustion. Fixes multiple related issues (e.g., #23397, #25736).

5. **[#25362 – feat(vertex): add vertexLocation config setting for Vertex AI region override](https://github.com/google-gemini/gemini-cli/pull/25362)**  
   Open (help wanted). Allows users to override the default `us-central1` region – critical for preview models that are only available in `global`.

6. **[#26387 – fix(core): implement system ripgrep fallback when bundled binary is missing](https://github.com/google-gemini/gemini-cli/pull/26387)**  
   Open. After removing architecture-specific binaries to reduce npm tarball size, this adds a graceful fallback to system `rg`.

7. **[#25947 – feat(tools): versioned pre-write backups with agent-driven restore](https://github.com/google-gemini/gemini-cli/pull/25947)**  
   Open. Introduces a session-scoped transactional layer for file writes, enabling rollback from destructive modification loops.

8. **[#26383 – fix(web-fetch): enforce rate limiting in fallback fetch execution and add tests](https://github.com/google-gemini/gemini-cli/pull/26383)**  
   Merged. Closes a gap where fallback fetch paths could bypass rate limits – important for preventing abuse.

9. **[#26374 – perf: optimize performance and memory for large chat sessions](https://github.com/google-gemini/gemini-cli/pull/26374)**  
   Merged. Uses `React.memo` and prop-based updates to handle 1,000+ message conversations without lag.

10. **[#26332 – fix(acp): resolve agent mode disconnect and improve mode awareness](https://github.com/google-gemini/gemini-cli/pull/26332)**  
    Merged. Fixes the disconnect between the ACP client (JetBrains, Zed) and the agent when switching between Plan, YOLO, Auto-Edit modes.

## Feature Request Trends
- **AST-Aware Tooling**: Multiple issues (#22745, #22746, #22747) propose leveraging syntax trees for more precise code reading and mapping, reducing token waste and improving file navigation.
- **Memory Routing**: Strong demand for separating user preferences (global) from project-specific context (#22819), with guidance on when to write proactively (#22809).
- **Agent Safety & Recovery**: Users want the agent to avoid destructive git operations (#22672) and to recover gracefully from subagent turn limits instead of reporting false success (#22323).
- **Browser Agent Configuration**: The `browser_agent` should respect `settings.json` overrides (#22267) and support automatic session takeover (#22232).
- **Tool Scalability**: With growing toolsets, the agent needs to intelligently limit enabled tools to avoid 400 errors (#24246).
- **UI/UX Polish**: Requests for favorite model cycling (#25072), keyboard shortcuts for @-mentions (#25060), improved table rendering (#25218), and better dependency tree indentation (#22816).

## Developer Pain Points
- **Windows Instability**: Top complaint – startup hangs, zombie processes, and SSH scrambling make the CLI nearly unusable on Windows (#26393, #24202, #25216).
- **Shell Command Hanging**: Commands that finish remain in “Awaiting input” state (#25166, 3👍), blocking further interaction.
- **Permission Loop**: The “allow for all future” setting doesn’t persist, repeatedly asking for consent on the same file (#24916).
- **Quota Exhaustion**: Using premium models for internal tooling quickly depletes quota, making the CLI inaccessible (#25684, #24937).
- **Subagent False Positives**: Subagents reporting success when they hit turn limits erodes trust in automated analysis (#22323).
- **Destructive Edits**: The agent occasionally overwrites files or runs dangerous git commands without proper safeguards (#22672, #23571).
- **Proxy & Network Issues**: Corporate environments hit `HttpsProxyAgent` constructor errors (#26361) or region-locked model 404s (#25362).
- **Scrolling & Rendering Glitches**: Long chats cause screen flashes and scrollbar jumps (#24470), and incremental table re-renders break screen readers (#25218).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date: 2026-05-03**

## 1. Today's Highlights
A wave of new issues flooded the repository over the last 24 hours, dominated by session-management bugs (phantom locks, deadlocks, misleading timestamps) and a critical v1.0.40 regression that **no longer loads MCP servers from `.mcp.json`**. Meanwhile, long-standing feature requests around session branching (`/fork`, `/branch`) and reasoning effort control continue to gather strong community support. No new releases were published.

## 2. Releases
*No new versions were released in the past 24 hours.*

## 3. Hot Issues
1. **[#2751 – `Remote session disabled: could not resolve repository` when using `/remote` on an org repo](github/copilot-cli Issue #2751)**  
   *12 👍 · 6 comments*  
   Enterprise users cannot use remote sessions on organization repositories. Blocking for team workflows.  

2. **[#2739 – `xhigh reasoning was removed for gpt-5.4 and gpt-5.3-codex!`](github/copilot-cli Issue #2739)**  
   *12 👍 · 5 comments*  
   Users report the CLI silently dropped high reasoning effort for certain models. Highly upvoted; community expects a fix.  

3. **[#1590 – `Execution failed: Error: Failed to get response from the AI model; retried 5 times`](github/copilot-cli Issue #1590)**  
   *12 👍 · 11 comments* *(Closed)*  
   A persistent server-error retry loop that disrupted long-running tasks. Closed but indicates backend reliability concerns.  

4. **[#1680 – `pwsh.exe hardcoded in 6 places – CLI completely unusable on Windows 11 with only PowerShell 5.1`](github/copilot-cli Issue #1680)**  
   *9 👍 · 7 comments*  
   A reopened issue from 2025. The CLI hard-codes `pwsh.exe`, breaking on Windows machines with only `powershell.exe`. Blocks all shell commands.  

5. **[#1313 – `Session Branching`](github/copilot-cli Issue #1313)**  
   *9 👍 · 6 comments*  
   The most-requested feature: allow users to branch the current session preserving history. Often requested alongside `/fork`.  

6. **[#3080 – `Cannot select reasoning_effort=high; model claude-opus-4.7-high rejects requests with 400 error`](github/copilot-cli Issue #3080)**  
   *1 👍 · 1 comment*  
   The CLI sends `reasoning_effort: "medium"` to a model that only accepts `high`, making the model unusable. No UI to change effort.  

7. **[#3082 – `Copilot locks files`](github/copilot-cli Issue #3082)**  
   *0 👍 · 1 comment*  
   Files remain locked after a prompt, causing "Access denied" errors on subsequent operations. Forces users to restart sessions.  

8. **[#3083 – `v1.0.40 no longer loads mcp servers from ./.mcp.json on start up`](github/copilot-cli Issue #3083)**  
   *0 👍 · 0 comments*  
   A regressive bug: after migrating from `.vscode/mcp.json` to `.mcp.json`, v1.0.40 ignores the file entirely. Breaks all MCP integrations.  

9. **[#3084 – `postToolUse hook deadlocks after write-permission request, process spins at 99% CPU`](github/copilot-cli Issue #3084)**  
   *0 👍 · 0 comments*  
   A critical crash: after a permission request, the process deadlocks, spins CPU, and ignores SIGTERM. Can run for days undetected.  

10. **[#3086 – `'Go back' from 'session in use' warning leaves a phantom lock on the abandoned session's folder`](github/copilot-cli Issue #3086)**  
    *0 👍 · 0 comments*  
    A session management bug: choosing "Go back" leaves a stale `.lock` file, potentially blocking future usage of that session.

## 4. Key PR Progress
*No pull requests were merged or updated in the last 24 hours.*

## 5. Feature Request Trends
The most requested feature directions from recent issues are:

- **Session branching / forking** (`#1313`, `#2058`, `#3091`): Users want to explore side questions without derailing the main objective, and navigate a tree of branched sessions with keybindings.
- **Reasoning effort control** (`#3074`, `#3080`, `#2739`): A dedicated `/effort` command and support for all reasoning levels across models is highly demanded.
- **MCP server management** (`#2956`, `#3090`, `#3073`): Better UX for enabling/disabling MCP servers, plus support for resource subscriptions and notifications.
- **Plugin marketplace improvements** (`#3088`): The `copilot plugin marketplace list` CLI command should respect repository-level settings.

## 6. Developer Pain Points
- **Windows compatibility** (#1680): Hardcoded `pwsh.exe` path still breaks the CLI for users stuck on PowerShell 5.1 – a recurring frustration since 2025.
- **Reasoning effort mismatches** (#2739, #3080): Models silently reject requests or lose capabilities due to hardcoded effort levels; users cannot override.
- **Session locking and deadlocks** (#3082, #3084, #3086, #3085): Multiple bugs around file locks, phantom locks, misleading timestamps, and process deadlocks degrade reliability.
- **MCP configuration regressions** (#3083): Version bumps unexpectedly break working MCP setups, forcing users to downgrade or debug.
- **Platform authentication** (#3081): NixOS keychain support is broken, blocking `copilot login` on that platform.
- **Model resetting to “auto”** (#3079): Users complain the CLI keeps switching the model back to auto without explanation.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-03

## Today’s Highlights
A critical Windows crash (#2151) in v1.41.0 was reported today, affecting path completion and image attachment transmission. On the feature side, a pull request (#2146) addressing the long-standing recursive skill discovery issue (#1894) was opened, aiming to match Codex’s behaviour. Several enhancement requests for hooks, status bars, and MCP tool lazy-loading also surfaced, indicating growing demand for extensibility and performance tuning.

## Releases
No new releases in the last 24 hours. The latest version remains **v1.41.0**.

## Hot Issues
*All 9 issues updated in the last 24 hours are listed below (10 requested, but only 9 available).*

1. **#2151** — `[Bug] v1.41.0 Windows terminal: NoneType crash on path completion + image attachment transmission broken`  
   ⚠️ **Critical**: Crashes on Windows 10 when tab-completing paths; also breaks sending images with copied file paths. No workaround yet.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2151)

2. **#2091** — `Session becomes extremely slow in v1.37.0 after extensive MATLAB work`  
   🐛 Performance regression: a specific session takes seconds per token after heavy MATLAB usage, but other sessions remain fast. Likely a memory leak or context bloat.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2091)

3. **#2150** — `API usage display is confusing: two independent quota systems, inverted semantics, and poor discoverability`  
   📊 UX pain: `/usage` shows two different quota sets without explanation; semantics of “free” vs. “subscription” are inverted for multi‑model users.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2150)

4. **#2149** — `[Feature] Claude Code-style configurable statusline with usage/cost metadata`  
   🚀 Request for a configurable status bar that reports model, cost, and token usage after each interaction, similar to Claude Code’s `statusline`.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2149)

5. **#2148** — `[bug] UserPromptSubmit hook receives empty prompt when user_input is list[ContentPart]`  
   🐛 Plugin hook bug: when a user sends a message with multiple content parts (e.g., text + image), the hook receives an empty string. Blocks multi‑modal plugins.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2148)

6. **#2147** — `[Feature] Lazy-load MCP tool schemas into context — only inject when tools are needed`  
   🎯 Performance improvement: injecting all MCP tool schemas upfront wastes context window. Suggests dynamic loading based on user intent.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2147)

7. **#2145** — `[enhancement] Hooks`  
   🔌 Wishes to add permission‑based hooks for agent tools, e.g., restricting write/edit permissions to specific agents on specific directory trees.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2145)

8. **#2040** — `[enhancement] Send VS Code notification (showInformationMessage) when approval is required in VS Code Extension`  
   💡 UX enhancement: if VS Code is minimized, approval dialogs are missed. Request to fire a system notification via the VS Code API.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/2040)

9. **#1894** — `Kimi CLI cannot recursively load nested skill directories (…), Codex is compatible but Kimi is not`  
   🔄 Compatibility gap: `.agents/skills/{name}/skills/xxx` works in Codex but not in Kimi CLI. Blocks migration from Claude Code. PR #2146 now addresses this.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/issues/1894)

## Key PR Progress
*Only 3 PRs received updates in the last 24 hours. All are covered below.*

1. **#2146** (OPEN) — `feat(#1894): recursively discover skills in nested subdirectories`  
   🧠 Resolves the skill loading gap with Codex by adding `_discover_subdir_skills()`. Currently under review.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/2146)

2. **#768** (CLOSED, updated yesterday) — `feat(shell): add pseudo-cwd for shell mode`  
   🏷️ Merged earlier but updated with documentation/last review. Adds a tracked current directory in shell mode, making `cd` consistent while agent workdir stays unchanged.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/768)

3. **#767** (CLOSED, updated yesterday) — `feat(approval): persist approve_for_session per session`  
   💾 Persists `auto_approve_actions` across session resumes via a state file, preventing re‑approval after reconnection.  
   [GitHub](https://github.com/MoonshotAI/kimi-cli/pull/767)

## Feature Request Trends
The community is converging on four major themes:

- **Codex‑compatibility**: Recursive skill loading (#1894) and hooks for permission control (#2145) are directly driven by migration from Claude Code.
- **Extensibility & hooks**: Multiple requests for plugin/hook systems – `UserPromptSubmit` bug (#2148) and permission‑based hooks (#2145) show demand for custom tooling.
- **Performance optimisation**: Lazy‑loading MCP schemas (#2147) and fixing session slowdowns (#2091) point to scaling pains as projects grow.
- **Better UX / observability**: Configurable status bars (#2149), clearer API quota display (#2150), and VS Code notifications for approvals (#2040) all aim to reduce friction in daily workflows.

## Developer Pain Points
- **Windows stability**: The `NoneType` crash (#2151) and the long‑standing `UserPromptSubmit` empty‑prompt bug (#2148) indicate that Windows and multi‑modal inputs require more attention.
- **Performance cliffs**: The MATLAB‑induced slowdown (#2091) suggests session state (context accumulation, file watchers) leaks or grows unchecked in certain environments.
- **Confusing quota semantics**: Two independent quota systems with inverted meanings (#2150) confuse new and migrating users; documentation improvements are urgently needed.
- **Plugin integration gaps**: Hooks receive malformed data (#2148) and MCP tool schemas waste context (#2147), making advanced automation brittle.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-03

## Today's Highlights

Two patch releases landed, fixing shell mode editing and custom agent plugin loading. Community momentum remains strong around **Cursor CLI support** (Issue #2072, 161 👍, 66 comments), while a fresh critical bug (#25526) reports local server connectivity loss overnight. The refactoring wave toward Effect-native handlers continues with multiple PRs from @kitlangton.

## Releases

Two versions shipped in the last 24 hours:

- **v1.14.33** — Fixed custom agents in plugins not loading. Thanks to community contributors @jerome-benoit (Nix cleanup), @OpeOginni (CLI docs), and @HyeokjaeLee (instance fix).  
  [Release notes](https://github.com/anomalyco/opencode/releases/tag/v1.14.33)

- **v1.14.32** — Shell mode prompt re-enabled editing (backspace, cursor movement). Fixed HTTP API workspace adapters losing instance context, which could break create/sync/routing flows. Also fixed experimental workspace creation requests omitting required fields.  
  [Release notes](https://github.com/anomalyco/opencode/releases/tag/v1.14.32)

## Hot Issues

1. **#2072 – Support for Cursor?** (OPEN, 161 👍, 66 comments)  
   The most-upvoted open request. Cursor released a public CLI; community wants OpenCode to integrate it. API not documented, but interest is huge.  
   [Issue #2072](https://github.com/anomalyco/opencode/issues/2072)

2. **#1298 – AI_TypeValidationError with custom provider** (CLOSED, 18 comments)  
   Common pain point: custom providers (e.g., Qwen3-coder) fail type validation on usage metadata. Suggests stricter schema handling needed.  
   [Issue #1298](https://github.com/anomalyco/opencode/issues/1298)

3. **#6286 – Compaction not running on time** (CLOSED, 15 comments)  
   Context balloons before compaction triggers, especially with Opus 4.5. Users reporting work loss.  
   [Issue #6286](https://github.com/anomalyco/opencode/issues/6286)

4. **#4422 – Primary agent responds in subagent view** (CLOSED, 14 comments)  
   UI bug: clicking a delegated subagent still routes input to the primary agent. Moderately complex to fix due to view state.  
   [Issue #4422](https://github.com/anomalyco/opencode/issues/4422)

5. **#10238 – Safer default for build agent: prompt on destructive bash** (CLOSED, 9 comments)  
   Feature request to require user confirmation before running dangerous commands (rm -rf, etc.). Some users prefer opt-in safety.  
   [Issue #10238](https://github.com/anomalyco/opencode/issues/10238)

6. **#12834 – Random TUI freeze (process continues in background)** (CLOSED, 7 comments)  
   Intermittent freeze lasting minutes to hours. No pattern; suspected rendering race.  
   [Issue #12834](https://github.com/anomalyco/opencode/issues/12834)

7. **#18793 – Add `chat.model` plugin hook for pre-call model routing** (OPEN, 6 comments)  
   Needed to dynamically swap provider/model before an LLM call – currently impossible with plugin hooks.  
   [Issue #18793](https://github.com/anomalyco/opencode/issues/18793)

8. **#24559 – Context window % always 0% with 9Router** (OPEN, 5 comments)  
   Bug report: using the 9Router provider disables context percentage display. Annoying for monitoring token usage.  
   [Issue #24559](https://github.com/anomalyco/opencode/issues/24559)

9. **#25526 – Can't connect to local server (sudden regression)** (OPEN, 4 comments)  
   Fresh issue: worked on May 2, broken May 3 – stuck on “unable to connect to local server”. Possibly related to auth or network change.  
   [Issue #25526](https://github.com/anomalyco/opencode/issues/25526)

10. **#25515 – OpenCode ignoring deny permissions?** (OPEN, 3 comments)  
    Security concern: a planning agent executed file writes despite “deny” permissions. Needs immediate investigation.  
    [Issue #25515](https://github.com/anomalyco/opencode/issues/25515)

## Key PR Progress

1. **#25537 – Flatten CLI/providers to Effect-native** (OPEN, @kitlangton)  
   Stage 4 of refactoring: providers handlers now run entirely as Effect v4. Removes `Effect.promise` wraps and `runPromise` bridges.  
   [PR #25537](https://github.com/anomalyco/opencode/pull/25537)

2. **#25538 – Sort docs sidebar entries by visual width** (OPEN, @PanAchy)  
   Closes #25536: reorders top-level docs sidebar for consistent readability.  
   [PR #25538](https://github.com/anomalyco/opencode/pull/25538)

3. **#25534 – Fix `retryCount` in `json_schema` structured output** (OPEN, @21pounder)  
   `retryCount` was defined in schema but never read; this PR wires it up so retries work as documented.  
   [PR #25534](https://github.com/anomalyco/opencode/pull/25534)

4. **#25529 – Fix auth login regression (stderr ignored)** (CLOSED, @rekram1-node)  
   Restores inherited stderr for remote auth helpers (e.g., cloudflared), fixing invisible login URLs.  
   [PR #25529](https://github.com/anomalyco/opencode/pull/25529)

5. **#24712 – Add native LLM core foundation** (OPEN, @kitlangton)  
   New `packages/llm` with Effect-based typed request/event/tool streaming, behind experimental flag. A major architecture step.  
   [PR #24712](https://github.com/anomalyco/opencode/pull/24712)

6. **#25389 – Fix file watch in dev mode** (OPEN, @Eric-Guo)  
   Legacy instance paths skipped `InstanceBootstrap`, causing file watcher to never start. Now fixed.  
   [PR #25389](https://github.com/anomalyco/opencode/pull/25389)

7. **#25528 – Encode v2 session responses** (CLOSED, @thdxr)  
   Returns session data as proper class instances so HttpApi encoding works, and omits undefined optional fields.  
   [PR #25528](https://github.com/anomalyco/opencode/pull/25528)

8. **#25513 – Support subpath serving** (OPEN, @ramonpaolo)  
   Adds `basePath` support for running OpenCode server/UI from a subpath (e.g., reverse proxy). Closes #13847.  
   [PR #25513](https://github.com/anomalyco/opencode/pull/25513)

9. **#25523 – CLI/stats fully Effect-native** (CLOSED, @kitlangton)  
   First Stage 4 demo: stats handler now yields services once and uses `Effect.forEach` instead of `runPromise`.  
   [PR #25523](https://github.com/anomalyco/opencode/pull/25523)

10. **#25500 – Exclude .map files from CLI binary build** (CLOSED, @PanAchy)  
    Removes ~30 MB of source maps from the binary, reducing download size.  
    [PR #25500](https://github.com/anomalyco/opencode/pull/25500)

## Feature Request Trends

The community is pushing for **broader provider integration** (Cursor CLI, PPQ.ai, Auggie) and **plugin hooks for model routing** (Issue #18793). Users want **safer defaults** for the build agent – prompting before destructive commands – and **easier import of settings/agents/MCP servers** from other tools like Claude Code (Issue #6207). Mobile and touch optimization (PR #18767) also received attention. Finally, several requests ask for **better CLI documentation** and **GUI partition tool recommendations** to avoid complex terminal work.

## Developer Pain Points

Recurring frustrations include **type validation errors** when integrating custom providers (Issue #1298), **compaction failures** leading to ballooning context windows (Issue #6286), and **random TUI freezes** with background continuation (Issue #12834). **Session persistence loss** (Issue #12310) and **deny permissions being ignored** (Issue #25515) are serious reliability/security concerns. Windows users face display issues in IntelliJ terminal (Issue #10629), and desktop users report **unresponsive text input** when pasting large content (Issues #15917, #15918). The sudden local-server connectivity regression (Issue #25526) is a top-priority blocker for many.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-03

## Today’s Highlights

A quiet patch release (`v0.72.1`) landed, but the community remained active with nearly **40 issues** and **23 PRs** updated in the last 24h. Keyboard‑layout regressions (Italian, Ukrainian, Bépo) and provider‑specific bugs (OpenAI Codex, Xiaomi MiMo, DeepSeek) dominated discussions. Several pull requests advanced provider support (Xiaomi MiMo, NVIDIA NIM, Together AI) and fixed critical tool‑calling reliability.

---

## Releases

- **[v0.72.1](https://github.com/badlogic/pi-mono/releases)** — A point release; no changelog details provided. Likely contains small fixes for the issues reported in the previous days.

---

## Hot Issues (10 Noteworthy)

1. **[#4026 – OpenAI Codex verbosity regression](https://github.com/badlogic/pi-mono/issues/4026)** (8 comments)  
   *Bug*: Switching `text.verbosity` from `"medium"` to `"low"` (default) causes Codex models to emit commentary instead of tool calls, breaking automation. Community concern about deployment workflows.

2. **[#4046 – Compaction deletes everything](https://github.com/badlogic/pi-mono/issues/4046)** (7 comments)  
   *Critical bug*: The compaction feature wipes all data. No root cause identified yet; marked `closed-because-weekend` but remains unresolved.

3. **[#3780 – Duplicate characters on Italian keyboard (Kitty protocol)](https://github.com/badlogic/pi-mono/issues/3780)** (5 comments)  
   *Keyboard regression*: Kitty Keyboard Protocol flag `4` causes duplicate input on Italian layouts. Affects many non‑US users.

4. **[#4082 – Xiaomi MiMo Token Plan URL for China](https://github.com/badlogic/pi-mono/issues/4082)** (6 comments)  
   *Provider bug*: The Chinese‑specific endpoint (`token-plan-cn.xiaomimimo.com`) is not recognised, returning 401. Immediate blocker for users in China.

5. **[#4104 – Filesystem operations need foundational override](https://github.com/badlogic/pi-mono/issues/4104)** (3 comments, 👍 3)  
   *Feature request*: Extensions need a lower‑level hook to replace filesystem ops (e.g., for remote sandboxes). High community upvote.

6. **[#4109 – Support Ukrainian Cyrillic layout for Ctrl combinations](https://github.com/badlogic/pi-mono/issues/4109)** (3 comments)  
   *Keyboard bug*: Ctrl+<letter> shortcuts don’t work on Cyrillic layouts. Similar to #3780 – a recurring theme.

7. **[#4047 – DeepSeek models cause 400 error with `reasoning_content`](https://github.com/badlogic/pi-mono/issues/4047)** (3 comments)  
   *Provider error*: DeepSeek V4 flash via OpenRouter fails due to unsupported `reasoning_content` field. Users forced to downgrade models.

8. **[#4105 – Autocomplete crash on non‑string values](https://github.com/badlogic/pi-mono/issues/4105)** (3 comments)  
   *TUI crash*: Autocomplete provider returns object values; `value.startsWith` throws `TypeError`. Hard crash that blocks completion.

9. **[#4114 – `resolveToCwd` crashes when `cwd` is undefined](https://github.com/badlogic/pi-mono/issues/4114)** (2 comments)  
   *Core crash*: Tool path resolution fails for extensions that don’t pass `cwd`. Affects third‑party integrations.

10. **[#1291 – Npm extensions with `@latest` slow startup](https://github.com/badlogic/pi-mono/issues/1291)** (2 comments)  
    *Performance*: Using `@latest` for npm extensions causes Pi to fetch packages on every start, delaying launch. Long‑standing issue.

---

## Key PR Progress (10 Important PRs)

1. **[#4117 – `stopAfterTurn` handoff control](https://github.com/badlogic/pi-mono/pull/4117)** (closed)  
   *New API*: Adds `agent.stopAfterTurn()` and `session.stopAfterTurn()` to allow graceful turn termination without hard `abort()`. Addresses long‑standing request.

2. **[#4116 – NVIDIA NIM provider](https://github.com/badlogic/pi-mono/pull/4116)** (closed)  
   *New provider*: Adds NVIDIA NIM as a built‑in OpenAI‑compatible provider with 50+ free model endpoints. Lowers barrier for new users.

3. **[#4005 & #4112 – Xiaomi MiMo provider (API & Token Plan)](https://github.com/badlogic/pi-mono/pull/4005)** (closed + open)  
   *Provider support*: Splits Xiaomi MiMo into two variants – API billing (default) and regional Token Plan endpoints. Fixes #4082.

4. **[#3624 – Together AI provider](https://github.com/badlogic/pi-mono/pull/3624)** (open)  
   *New provider*: Adds native Together AI support with model sourcing from `models.dev`. Awaiting merge.

5. **[#3474 – TypeBox v1 migration with extension compat](https://github.com/badlogic/pi-mono/pull/3474)** (closed)  
   *Infrastructure*: Migrates from AJV to TypeBox 1.x for schema validation, keeping legacy extension imports working. Important for future stability.

6. **[#3247 – TypeBox fallback for Cloudflare](https://github.com/badlogic/pi-mono/pull/3247)** (closed)  
   *Edge compatibility*: Adds TypeBox fallback for Cloudflare Workers environment. Enables Pi on serverless edges.

7. **[#3229 – Harden Anthropic tool‑call streaming](https://github.com/badlogic/pi-mono/pull/3229)** (closed)  
   *Reliability*: Switches to raw event‑based streaming with fallback to non‑streaming on failure. Reduces mid‑turn crashes.

8. **[#4094 – OpenAI image generation in interactive TUI](https://github.com/badlogic/pi-mono/pull/4094)** (closed)  
   *New feature*: Wires `image_generation` tool for OpenAI Responses API, allowing interactive TUI image gen. Mimics Codex behavior.

9. **[#3615 – Add GPT‑5.5 models](https://github.com/badlogic/pi-mono/pull/3615)** (closed)  
   *Model support*: Adds GPT‑5.5 across OpenAI, Azure, and Codex providers with appropriate context windows.

10. **[#4119 – Stabilise env‑sensitive test cases](https://github.com/badlogic/pi-mono/pull/4119)** (open)  
    *Quality*: Forces SSE transport in Codex tests, clears SSH/MOSH env vars, isolates HOME. Reduces flaky CI failures.

---

## Feature Request Trends

- **Non‑Latin keyboard support** – Multiple issues (Ukrainian, Italian, Bépo, Hangul) request proper handling of Ctrl+letter shortcuts and accented characters. A single input‑normaliser hook or per‑layout key‑mapping is the most wanted enhancement.
- **Provider expansion** – Requests for NVIDIA NIM, Together AI, Xiaomi MiMo, and Nebius Token Factory reflect a strong desire for diverse, low‑cost or free model backends. Users want one‑click login for each.
- **Sandbox / remote filesystem integration** – #4104 and #4100 ask for a foundational hook to replace file‑system operations, enabling extensions to connect to remote sandboxes (Daytona, etc.) without breaking core tools.
- **Graceful turn control** – #4118 and #4117 propose `stopAfterTurn` to avoid hard `abort()`. This is essential for agent loops that need clean boundaries (e.g., tool‑calling sequences).
- **System theme auto‑detection** – #1436 (light/dark mode switching) remains open, with moderate interest. Users expect Pi to follow the OS theme without manual intervention.

---

## Developer Pain Points

- **Keyboard layout regressions** – Italian, Ukrainian, Bépo, and Hangul users report duplicate characters, broken AltGr, and non‑functional Ctrl shortcuts. The recurring pattern suggests the Kitty Keyboard Protocol changes need broader locale testing.
- **Provider‑specific errors** – OpenAI Codex verbosity change (#4026), DeepSeek `reasoning_content` (#4047), and Xiaomi MiMo Chinese endpoint (#4082) each cause immediate workflow breaks. Users feel provider updates are not well‑communicated.
- **Installation & update headaches** – #4086 (cannot install) and #4102 (`pi update` breaks mise versioning) show that the update mechanism can corrupt versioned installations, forcing manual recovery.
- **Performance degradation** – #1291 (`@latest` extensions slow startup) remains unresolved, hurting developer experience in daily use.
- **Autocomplete crashes** – #4105 (non‑string values) and #4103 (WebSocket prevents `--print` exit) are hard crashes that interrupt work. Likely low test coverage in edge cases.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Based on the provided GitHub data for `QwenLM/qwen-code`, here is the **Qwen Code Community Digest** for 2026-05-03.

---

## Qwen Code Community Digest
**Date:** 2026-05-03
**Analyst:** AI Developer Tools Specialist

### 1. Today's Highlights

The project is witnessing a surge in **reliability and infrastructure improvements**. Key efforts include reworking the retry/error classification logic for API calls (PR #3798) and standardizing the release pipeline across Python and TypeScript SDKs (Issues #3793-#3796). Additionally, the **Background Task Management** feature is nearing completion with Phase B closure (PR #3801 and Issue #3634), while the community is actively filing and fixing bugs related to third-party provider integrations, particularly for DeepSeek and MiniMax.

### 2. Releases

A new nightly release was published:
- **v0.15.6-nightly.20260503.5037fa762**: This release includes a core performance optimization—a new `FileReadCache` that short-circuits unchanged read operations—and a CLI fix that ensures proxy settings are properly honored.

### 3. Hot Issues

1.  **[(#3634) Background task management: roadmap and next steps](https://github.com/QwenLM/qwen-code/issues/3634)**
    - *Significance:* A high-level roadmap for a critical feature (background tasks), with Phases A and B already merged. This issue serves as the single source of truth for developers working on this area. Community reaction is positive, with author coordination evident.

2.  **[(#3004) API Exponential Backoff & Fallback Retry / API 指数退避与降级重试](https://github.com/QwenLM/qwen-code/issues/3004)**
    - *Significance:* A highly requested P1 reliability feature. The current retry mechanism is too simple. The community strongly desires automatic exponential backoff, model downgrade on specific errors (529), and token refresh logic to make the tool more robust.

3.  **[(#3748) Non-interactive (-p) mode prints API errors three times and double-wraps the message](https://github.com/QwenLM/qwen-code/issues/3748)**
    - *Significance:* A clear bug affecting scripting and CI/CD use cases. The duplicate and malformed error output makes automation difficult. This was quickly addressed by PR #3749, showing a responsive development cycle.

4.  **[(#3772) deepseek v4 pro出现api error 400](https://github.com/QwenLM/qwen-code/issues/3772)**
    - *Significance:* Highlights integration pain with third-party models. The error `reasoning_content in the thinking mode must be passed back` suggests a serious compatibility issue with DeepSeek's thinking mode that requires a specific protocol handling, causing community frustration.

5.  **[(#3786) An error occurred when calling the DeepSeek v4 Pro model](https://github.com/QwenLM/qwen-code/issues/3786)**
    - *Significance:* This mirrors the previous issue, but filed by the lead maintainer `wenshao`, confirming the priority of fixing DeepSeek V4 integration. The request for "Better support for Deepseek v4 Pro" is clear.

6.  **[(#3789) 读取不了文件系统中目录下的文件 (Cannot read files in the filesystem directory)](https://github.com/QwenLM/qwen-code/issues/3789)**
    - *Significance:* A potential critical bug affecting users with specific remote desktop setups (Sunflower). It suggests a file system permission or path resolution edge case that requires triage and could impact user trust in basic functionality.

7.  **[(#3796) feat(sdk-python): replace verbatim release notes inheritance with git-log-based notes](https://github.com/QwenLM/qwen-code/issues/3796)**
    - *Significance:* Indicates a major maintenance improvement for the Python SDK. The current release note generation is a "linear chain that grows with every release," which is fragile and messy. The community is pushing for automated, clean changelogs.

8.  **[(#3795) refactor: extract shared release helper utilities](https://github.com/QwenLM/qwen-code/issues/3795)**
    - *Significance:* A clear code quality and maintainability issue. The same function exists in three files. This "copy-paste" pattern is a bug magnet and a sign of technical debt that the community (via `doudouOUC`) is proactively addressing.

9.  **[(#3794) feat(sdk-python): add network timeouts to release version helper](https://github.com/QwenLM/qwen-code/issues/3794)**
    - *Significance:* A DevOps-focused issue warning that the build pipeline can hang indefinitely due to missing network timeouts. This is a critical fix for the reliability of the CI/CD system.

10. **[(#3787) Using ACP mode, the language used in the thinking process is inconsistent with the user's target language](https://github.com/QwenLM/qwen-code/issues/3787)**
    - *Significance:* A user experience (UX) bug where the thinking process defaults to English despite the user's session language. This is a quality-of-life issue for non-English speakers and reflects a need for more contextual awareness in the agent's reasoning.

### 4. Key PR Progress

1.  **[(#3801) feat(cli): include monitors in /tasks + add interactive-mode hint](https://github.com/QwenLM/qwen-code/pull/3801)**
    - *Significance:* Closes Phase B of the background task roadmap. It fixes a critical bug where monitors were not visible in the `/tasks` command and adds UX hints, completing a major feature milestone.

2.  **[(#3774) feat(core): enforce prior read before Edit / WriteFile mutates a file](https://github.com/QwenLM/qwen-code/pull/3774)**
    - *Significance:* A safety feature that leverages the new `FileReadCache`. It enforces that the model must have read a file's current state before attempting to edit it, preventing dangerous overwrites or conflicts.

3.  **[(#3798) feat(core): classify retryable transport/provider failures vs deterministic request errors](https://github.com/QwenLM/qwen-code/pull/3798)**
    - *Significance:* Implements a core reliability feature. It adds a `classifyError()` function to intelligently differentiate between transient errors (429, 5xx) and user errors (400, 401), preventing infinite retries on deterministic failures.

4.  **[(#3800) feat(core): support reasoning effort 'max' tier (DeepSeek extension)](https://github.com/QwenLM/qwen-code/pull/3800)**
    - *Significance:* Directly addresses the DeepSeek compatibility issues raised in Issues #3772 and #3786 by supporting the new `max` reasoning effort tier, ensuring the tool stays compatible with the latest vendor APIs.

5.  **[(#3783) feat(cli): Add ability to switch models non-interactively from the cli](https://github.com/QwenLM/qwen-code/pull/3783)**
    - *Significance:* A community-requested feature for scripting and automation. It introduces a new `/model` syntax, allowing users to change the backend model without entering an interactive menu.

6.  **[(#3797) feat(cli): add /model list subcommand for dynamic model discovery](https://github.com/QwenLM/qwen-code/pull/3797)**
    - *Significance:* Complements PR #3783. It allows users to dynamically list available models from the provider's API endpoint, improving discoverability and UX.

7.  **[(#3735) fix(core): auto-compact subagent context to prevent overflow](https://github.com/QwenLM/qwen-code/pull/3735)**
    - *Significance:* Fixes a common crash (`max_length`) with sub-agents on smaller context windows. This is a crucial stability fix for users running complex, multi-turn agentic workflows.

8.  **[(#3707) fix(core): per-agent ContentGenerator view via AsyncLocalStorage](https://github.com/QwenLM/qwen-code/pull/3707)**
    - *Significance:* Ensures sub-agents using a different model correctly use their own configuration. This is essential for the correct operation of multi-model strategies and agent hierarchies.

9.  **[(#3733) feat(cli): support batch deletion of sessions in /delete](https://github.com/QwenLM/qwen-code/pull/3733)**
    - *Significance:* A UX polish for session management. It introduces multi-select checkboxes for batch deletion, making it easier to manage a large number of sessions.

10. **[(#3790) fix(core): improve stream rate-limit retry diagnostics](https://github.com/QwenLM/qwen-code/pull/3790)**
    - *Significance:* Improves debugging for API rate limits. It adds structured diagnostics and changes the retry from a fixed wait to an adaptive delay based on the `Retry-After` header.

### 5. Feature Request Trends

- **Automatic Error Recovery & Robustness:** The community strongly desires smarter retry logic (exponential backoff, model fallback), as seen in Issue #3004 and PR #3798. This is the top infrastructure demand.
- **Build & SDK Standardization:** There is a clear push from the community (via `doudouOUC` and others) to improve and standardize the release pipeline for the Python and TypeScript SDKs, focusing on timeouts, clean changelogs, and reducing code duplication (Issues #3793, #3794, #3795, #3796).
- **Enhanced Third-Party Provider Support:** Users are actively running against various backends (DeepSeek, MiniMax, ollama) and are encountering edge cases. The trend is towards more flexible and compliant OpenAI protocol handling.
- **Batch & Non-Interactive Operations:** Users want to manage their environment (sessions, models) via scriptable commands, as shown by the PRs for batch session deletion and model switching from the CLI (PRs #3733, #3783, #3797).

### 6. Developer Pain Points

- **DeepSeek V4 Integration:** This is the most prominent pain point. The "thinking mode" protocol mismatch causes outright errors, directly blocking users of this popular model. Urgent fixes are in progress (PR #3800) but the issue highlights the fragility of integrating with fast-moving third-party APIs.
- **SDK Release Pipeline Fragility:** The verbatim copy of release notes and missing network timeouts in the CI/CD pipeline (Issues #3794, #3796) point to a fragile build system that could lead to broken releases or developer downtime.
- **Unpredictable File Access:** The issue where files cannot be read in certain remote desktop environments (Issue #3789) is a critical bug that undermines the core "code agent" functionality, suggesting an insufficiently tested file system abstraction layer.
- **Silent Data Loss / Corruption:** The bug where `SessionService` could miscount messages due to corrupt session data (PR #3692) is a significant pain point for reliability, as it could lead to user confusion and data being effectively "lost" from session management views.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*