# AI CLI Tools Community Digest 2026-05-04

> Generated: 2026-05-04 08:44 UTC | Tools covered: 8

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

# AI CLI Developer Tools — Cross-Tool Comparison Report
**Date:** 2026-05-04

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem continues to mature rapidly, with six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, Qwen Code, and Pi—now sharing a common architectural pattern: agentic loops with tool-calling, subagent orchestration, and hooks/plugin systems. All tools face similar growing pains around session persistence, MCP reliability, cross-platform parity, and silent failure modes. The community dialogue reveals that no tool has yet solved the fundamental tension between agent autonomy and user control, with permission management, undo capabilities, and configurable escalation policies emerging as universal pain points. Most tellingly, the dominant feature requests across tools converge on **session resilience**, **multi-agent orchestration**, and **custom model provider support**, suggesting the next competitive frontier lies in reliability and flexibility rather than raw model capability.

---

## 2. Activity Comparison

| Tool | GitHub Stars | Open Issues | Hot Issues (24h) | PRs Active (24h) | Release Status (24h) |
|---|---|---|---|---|---|
| **Claude Code** | ~45k+ | 50 | 10 (high engagement, 156 comments on #27302) | 6 | No new release |
| **OpenAI Codex** | ~35k+ | — | 10 (#20161: 48 comments) | 10 | No new release |
| **Gemini CLI** | ~20k+ | — | 10 (#22141: 181 comments) | 10 | No new release |
| **GitHub Copilot CLI** | ~25k+ | — | 10 (#1799: 9 comments) | 0 | No new release |
| **Kimi Code CLI** | ~10k+ | — | 10, but lower engagement (max 2 👍) | 1 | No new release |
| **OpenCode** | ~15k+ | — | 10 | 10 | No new release |
| **Pi** | ~5k+ | 30 (open) | 10 | 9 | No new release |
| **Qwen Code** | ~15k+ | — | 10 | 10 | **v0.15.6-nightly** released |

**Key observations:**
- **Qwen Code** was the only tool shipping a nightly release today (v0.15.6-nightly with `FileReadCache` and proxy fix).
- **Claude Code** shows the highest community engagement intensity: issue #27302 (multi-connector accounts) has 156 comments and 214 👍 — the single most-voted feature request across all ecosystems.
- **Gemini CLI** has the most urgent community pain: issue #22141 (1+ hour hangs on small tasks) has 181 comments and 147 👍, indicating a systemic agent-loop bottleneck.
- **OpenAI Codex** and **Gemini CLI** show strong internal development velocity with 10 PRs each updated today.
- **Copilot CLI** is an outlier with 0 PR activity and a relatively small but vocal community facing v1.0.40 regressions.

---

## 3. Shared Feature Directions

| Requirement | Tools | Specific Needs |
|---|---|---|
| **Multi-account/multi-connector support** | Claude Code (#27302), Pi (#4143 regional providers) | Users want to attach multiple workspaces, orgs, or regional accounts without re-authentication. |
| **Session persistence & recovery** | Claude Code (PR #55864), OpenAI Codex (#18993), Qwen Code (#3822), Kimi Code (#1493) | Losing session context on crash/close is a top frustration; all tools need graceful resume, crash recovery, and undo capabilities. |
| **MCP reliability & authentication flexibility** | Copilot CLI (#3083, #3100), OpenCode (#25670), Qwen Code (#3817, #3799) | Broken MCP auto-load, OAuth vs. header conflict, duplicate processes, and transport reconnection are shared pain points. |
| **Subagent reliability & error reporting** | Claude Code (#55928, #22323), Gemini CLI (#22323), OpenCode (#25681) | Subagents silently fail, lie about completion, or hit turn limits without honest reporting. |
| **Configurable default values & session configuration** | Kimi Code (#20301, #2155), Gemini CLI (#22267), Claude Code (#55594) | Users want configurable prompts, keybindings, symbols, and per-project settings instead of hardcoded defaults. |
| **Undo/rollback & safety nets** | OpenAI Codex (#9203, 182 👍), Claude Code (#22672 destructive guardrails), Gemini CLI (#22672) | `undo` is the single most upvoted feature across ecosystems; users fear accidental destructive operations. |
| **Cross-platform parity** | Claude Code (Windows: #45297, #54865), Copilot CLI (PowerShell footgun #3098), Gemini CLI (Windows: #26174, #25900) | Windows/SSH users face disproportionately more bugs; macOS/Linux generally smoother. |
| **Custom model & BYO provider support** | Copilot CLI (#2995, #3099), Gemini CLI (#25684), Pi (#3357 local LLMs), OpenAI Codex (#20301) | Users want to bring their own model endpoints, fallback chains, and private deployments. |

---

## 4. Differentiation Analysis

| Tool | Core Focus | Target User | Technical Distinctives |
|---|---|---|---|
| **Claude Code** | Deep agentic workflows, hooks ecosystem, multi-session orchestration | Professional developers, enterprise teams | Hooks system (PreToolUse/PostToolUse), plugin architecture, `Background Agent` pattern, connector-based identity. Most sophisticated tool governance surface. |
| **OpenAI Codex** | Multi-agent control, observability, session management | Professional developers, VS Code ecosystem | Fork debugging (PR #20914), watchdog agents, TUI subagent views, custom role prompts (`AGENTS.*.md`). Strongest emphasis on debugging multi-agent sessions. |
| **Gemini CLI** | Codebase understanding, memory routing, performance at scale | Google Cloud ecosystem, Python/Go developers | AST-aware codebase mapping (#22745), global vs. project memory routing (#22819), quota failover (Flash-to-Flash-Lite). Most advanced code understanding pipeline. |
| **GitHub Copilot CLI** | Lightweight agent, ACP protocol, VS Code integration | GitHub ecosystem, individual developers | ACP agent protocol, `.mcp.json` config, alt-screen TUI, plan/autopilot modes. Friction-free "ask" interface. |
| **Kimi Code CLI** | Simple UX, thinking model visibility, Web UI | East Asian market, cloud/SaaS users | Ctrl+T thinking toggle (PR #2158), `yolo`/`afk` modes, Web UI status indicators. Emphasis on visual polish and usability. |
| **OpenCode** | Model-agnostic TUI, MCP resilience, plugin system | Power users, multi-provider users | ACP client capabilities (#5182), auto-reconnect MCP (#25670), mobile touch optimization (PR #18767). Most model-agnostic and platform-flexible. |
| **Pi** | Local-first LLM integration, SDK, extensibility | Hobbyists, local AI enthusiasts, Rust/Node developers | Official local LLM extensions (Ollama, llama.cpp, LM Studio, vLLM) via PR #4154, `pi serve` daemon mode. Strongest focus on offline/ private deployments. |
| **Qwen Code** | Cost optimization, stability, Alibaba Cloud ecosystem | Asian enterprise market, cloud-native developers | `FileReadCache` to reduce token waste, `qwen serve` daemon mode, proxy/protocol normalization. Most focused on production reliability and cost control. |

**Key differentiation insight:** Claude Code and OpenAI Codex are racing toward **enterprise agent orchestration** (hooks, subagents, permissions). Gemini CLI is investing in **code understanding intelligence** (AST mapping, memory routing). Pi and OpenCode prioritize **flexibility and local deployment**. Copilot CLI and Kimi Code target **low-friction UX** for busy individual developers. Qwen Code focuses on **cost efficiency and cloud-native stability**.

---

## 5. Community Momentum & Maturity

| Tool | Community Activity (24h) | Maturity Indicators | Risk Signals |
|---|---|---|---|
| **Claude Code** | ⭐⭐⭐⭐⭐ Highest engagement per issue (156 comments on top issue) | Mature hooks system, plugin ecosystem, 50 open issues managed | Cross-platform gaps (Windows/UNC, path encoding) persist; regression sensitivity high (#54847, #55889) |
| **OpenAI Codex** | ⭐⭐⭐⭐⭐ Strong PR velocity (10 PRs merged/updated) | Multi-agent panel, watchdog, fork debugging — sophisticated architecture | Auth fragility (#20161 SSO block), plugin reliability (#18258 Computer Use), broken `/undo` (#9203) |
| **Gemini CLI** | ⭐⭐⭐⭐ High urgency (181 comments on top issue) | AST-aware codebase mapping, memory routing, eval suite (#24353) | Critical performance hang (#22141) dominates; SSH/Windows unreliable |
| **GitHub Copilot CLI** | ⭐⭐ Low activity, 0 PRs | ACP protocol, `.mcp.json` config | v1.0.40 regressions (#3083, #3101); security concerns (#1607 ACP permissions); controversial alt-screen |
| **Kimi Code CLI** | ⭐ Low engagement (max 2 👍 per issue) | Clean UI, thinking model visibility | Very small community; UX complaints about basic interactions (newlines, emojis) |
| **OpenCode** | ⭐⭐⭐ Steady activity, 10 PRs | Model-agnostic, ACP client, mobile touch | Subagent recursion (#25681), TUI copy regression (#17796), long-standing shell/PATH issues |
| **Pi** | ⭐⭐⭐ Active (9 PRs), local LLM milestone (PR #4154) | Local-first SDK, Xiaomi/MiMo integration, profile-isolated state | Hung processes (#4141, #4144), macOS crashes (#4142), small user base |
| **Qwen Code** | ⭐⭐⭐ Nightly release today, 10 PRs | `FileReadCache`, daemon mode architecture, retry classification | Session bloat (#3822), MCP race condition (#3817), free-tier controversy (#3203) |

**Maturity ordering (rough):** Claude Code ≈ OpenAI Codex > Gemini CLI > Copilot CLI > Qwen Code > OpenCode > Pi > Kimi Code

**Momentum leaders:** Claude Code (highest engagement), OpenAI Codex (highest PR velocity), Gemini CLI (urgent need driving attention), Qwen Code (shipping nightly releases).

---

## 6. Trend Signals

### 1. MCP is the Universal Integration Layer, but Failing
Every tool adopted MCP, but every tool also reports MCP reliability issues — broken auto-loading (Copilot CLI #3083), transport disconnects (OpenCode #25670), duplicate processes (Qwen Code #3817), auth conflicts (Copilot CLI #3100). **The industry needs MCP specification hardening around reconnection, auth fallback, and lifecycle management.** Tools that ship robust MCP resilience first will win enterprise trust.

### 2. Session Persistence is the Unmet Basic Need
Loss of context — on crash, window close, or usage limit — is the #1 shared frustration across Claude Code, OpenAI Codex, Qwen Code, and Kimi Code. The community is building client-side workarounds (Claude Code PR #55864 session-persist plugin), but **first-class crash recovery and undo are table stakes for production adoption.** This is not a nice-to-have; it's the gating factor moving from "experimental" to "daily driver."

### 3. Local/Private LLM Integration Reaches Critical Mass
Pi's official local-LLM provider extensions (Ollama, llama.cpp, LM Studio, vLLM) closed the most-requested feature (#3357), and Copilot CLI community demands BYO model support (#2995). **Organizations increasingly demand data sovereignty.** Tools that offer seamless local/cloud fallback chains (like Gemini CLI's Flash-to-Flash-Lite quota failover) will gain competitive advantage in regulated industries.

### 4. The Hooks/Plugin Ecosystem is Becoming a Differentiator
Claude Code's hooks system (PreToolUse, PostToolUse, UserPromptSubmit) is the most sophisticated, but regressions (#55889 dropped context channels) show growing pains. OpenAI Codex adds custom role prompts and watchdog agents. **The ability for enterprises to inject governance, compliance, and custom tool logic will determine CLI tool adoption in large organizations.** This is where agentic AI meets corporate policy.

### 5. Cross-Platform Parity is a Persistent Weakness
Windows users face 2–3× more bugs than macOS/Linux across every tool: UNC path failures (Claude Code #45297), PowerShell quote parsing (Gemini CLI #26174), `$home` variable footgun (Copilot CLI #3098), SSH text scrambling (Gemini CLI #24202). **No tool has mastered Windows support.** This is a significant opportunity for a tool that prioritizes Windows/SSH reliability — especially given the large enterprise Windows developer base.

### 6. Silent Failures Erode Trust Faster than Visible Bugs
The most community-damaging bug class across all tools is **operations that fail without feedback**: tool dispatch stalls (Claude Code #54847), background agents "complete" with empty deliverables (Claude Code #55928, Gemini CLI #22323), subagents lying about success (Gemini CLI #22323). **Silent failures destroy developer confidence more than visible crashes.** The next generation of CLI tools must invest in observability: progress indicators, honest error reporting, and subagent output streaming.

### 7. Authentication & Billing Fragility is a Universal Pain
SSO phone-verification blocks (OpenAI Codex #20161), expired-token hangs (Pi #4141), free-tier reductions (Qwen Code #3203), per-tool-call premium billing (Copilot CLI #1770) — all tools face identity and cost management friction. **Developers want predictable authentication and transparent billing.** Tools that offer usage hooks (Claude Code #55945) and rate-limit resilience (Qwen Code PR #3790) are responding, but the industry lacks a standard approach.

### 8. Desktop/CLI Feature Parity is Incomplete
Claude Code users report hooks working in CLI but ignored in desktop app (#55951). OpenAI Codex VS Code extension loses conversation history (#18993). **Multi-surface consistency is a growing expectation.** As tools expand from CLI to desktop IDE extensions to Web UI, maintaining feature parity across surfaces becomes a significant engineering challenge.

### Recommended Actions for Tool Maintainers:
1. **Ship session persistence and undo immediately** — it's the #1 unmet need across all communities.
2. **Fix MCP reliability before adding more features** — the protocol is the integration backbone and it's failing.
3. **Invest in Windows support** — no tool has solved this, creating a clear differentiation opportunity.
4. **Eliminate silent failures** — every "silent hang" or "false success" should be treated as severity-critical.
5. **Build authentication/billing transparency** — users need to understand what they're paying for and why auth fails.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (Data as of 2026-05-04)

## 1. Top Skills Ranking (by Community Attention)

Based on the most active Pull Requests in the `anthropics/skills` repository, the following Skills have drawn the strongest community interest. (Comment counts were unavailable in the dataset; ranking is inferred from topic relevance and discussion breadth.)

| # | Skill PR | Description | Key Discussion Points | Status |
|---|----------|-------------|----------------------|--------|
| 1 | **document-typography** [#514](https://github.com/anthropics/skills/pull/514) | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Aims to fix systemic typography issues across all Claude output. | High relevance to every Claude user; focus on real-world document quality rather than theoretical features. | **Open** |
| 2 | **skill-quality-analyzer + skill-security-analyzer** [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills for evaluating other skills across 5 dimensions (structure, documentation, examples, etc.) and for security analysis of skill behavior. | Community interest in self-regulation and quality assurance; discussion around making these part of the official CI pipeline. | **Open** |
| 3 | **frontend-design** (improvement) [#210](https://github.com/anthropics/skills/pull/210) | Revises the existing frontend-design skill to be more actionable and instruction-following, ensuring every directive is executable within a single conversation. | Clarity vs. token efficiency debate; many users want Claude to produce production-ready UI code consistently. | **Open** |
| 4 | **ODT (OpenDocument Text)** [#486](https://github.com/anthropics/skills/pull/486) | Creates, fills, reads, and converts `.odt`/`.ods` files, including template filling and ODT→HTML conversion. Triggers on any mention of LibreOffice or OpenDocument. | Strong demand for open-source document formats; complements existing DOCX/PDF skills. | **Open** |
| 5 | **testing-patterns** [#723](https://github.com/anthropics/skills/pull/723) | Comprehensive testing skill covering Trophy model, unit testing (AAA pattern), React Testing Library, and what _not_ to test. | Developers want Claude to write reliable tests; discussion focused on framework-agnostic patterns vs. framework-specific guidance. | **Open** |
| 6 | **shodh-memory** [#154](https://github.com/anthropics/skills/pull/154) | Persistent memory system for AI agents that maintains context across conversations using `proactive_context` calls. | Demand for long-term agent memory; questions about privacy, storage limits, and integration with Claude Code’s existing context. | **Open** |
| 7 | **ServiceNow Platform** [#568](https://github.com/anthropics/skills/pull/568) | Broad platform assistant covering ITSM, ITOM, ITAM, SecOps, SPM, CSDM, and IntegrationHub – not just scripting. | Enterprise users want Claude to navigate complex ServiceNow ecosystems; discussion about maintainability of such a wide skill. | **Open** |
| 8 | **sensory (macOS automation via AppleScript)** [#806](https://github.com/anthropics/skills/pull/806) | Uses `osascript` for native macOS automation with a two-tier permission system (Tier 1: direct app scripting, Tier 2: Accessibility). | Alternative to screenshot-based computer use; community excited about performance gains and reliability. | **Open** |

---

## 2. Community Demand Trends (from Issues)

Analysis of the most commented Issues reveals the following concentrated demand directions:

- **Agent Safety & Governance** – Issue [#412](https://github.com/anthropics/skills/issues/412) proposes an `agent-governance` skill with policy enforcement, threat detection, and audit trails. Reflects growing concern around multi-step agent reliability.
- **Enterprise Skill Sharing** – Issue [#228](https://github.com/anthropics/skills/issues/228) calls for org-wide skill libraries with direct sharing links, bypassing manual file transfer. Not a skill itself, but a feature request that would dramatically change how skills are deployed in teams.
- **MCP Integration** – Issue [#16](https://github.com/anthropics/skills/issues/16) asks for skills to be exposed as MCP tools (e.g., `generateAlgorithmArt({ prompt, options })`). Suggests the community wants skills to become composable, API-like building blocks.
- **Skill-Creator Improvements** – Issues [#202](https://github.com/anthropics/skills/issues/202) and [#532](https://github.com/anthropics/skills/issues/532) highlight the need for a more operational, token-efficient skill-creator that works with enterprise SSO (no `ANTHROPIC_API_KEY` dependency).
- **Bedrock Compatibility** – Issue [#29](https://github.com/anthropics/skills/issues/29) remains open, indicating demand for skills to work with AWS Bedrock deployments.
- **Security & Namespace Trust** – Issue [#492](https://github.com/anthropics/skills/issues/492) raises alarm about community skills impersonating official Anthropic skills under the `anthropic/` namespace. This could influence future repository governance.

---

## 3. High-Potential Pending Skills (Likely to Merge Soon)

These open PRs have active community engagement and appear close to landing:

- **document-typography** [#514](https://github.com/anthropics/skills/pull/514) – Addresses a universal pain point; authors have responded to feedback on edge cases. Likely to merge after minor refinements.
- **testing-patterns** [#723](https://github.com/anthropics/skills/pull/723) – Well-structured and fills a clear gap in the skills collection. Awaiting final review.
- **ODT skill** [#486](https://github.com/anthropics/skills/pull/486) – Completes the document format suite; only minor formatting issues remain per PR comments.
- **shodh-memory** [#154](https://github.com/anthropics/skills/pull/154) – Innovative, but faces questions about privacy and API usage pattern. Active discussion suggests it will evolve and merge.
- **CONTRIBUTING.md** [#509](https://github.com/anthropics/skills/pull/509) – While not a skill, this meta-PR is a community health priority (resolves Issue [#452](https://github.com/anthropics/skills/issues/452)) and is likely to be merged soon after minor wording adjustments.

---

## 4. Skills Ecosystem Insight

> The community’s most concentrated demand is for **production-quality documentation and testing skills** that address real-world output issues (typography, file format fidelity, test reliability), alongside a growing appetite for **enterprise integration** (ServiceNow, macOS automation, memory persistence) and **agent governance**, signaling that Claude Code is moving from experimental tool to production deployment hub.

---

# Claude Code Community Digest — 2026-05-04

## Today's Highlights

No new releases shipped in the last 24 hours, but the community remains highly active with 50 open issues and 6 pull requests. The most notable development is the exceptionally high engagement on a multi-connector account feature request (#27302, 156 comments, 214 👍), while several regressions in tool dispatch and macOS desktop stability continue to surface as recurring pain points across versions 2.1.121–2.1.123.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 picks)

**1. Support multiple Connector accounts** [#27302](https://github.com/anthropics/claude-code/issues/27302)  
*Enhancement | 156 comments, 214 👍*  
The single most-requested feature in the repository. Users want the ability to connect multiple accounts for the same connector type (e.g., multiple Slack or GitHub orgs) within Claude Code and claude.ai. With broad community support and sustained discussion since February, this is clearly a top priority request for the product team.

**2. Tool dispatch stalls silently** [#54847](https://github.com/anthropics/claude-code/issues/54847)  
*Bug (regression) | 8 comments*  
A critical regression in versions 2.1.121–2.1.123: local tool calls (Write, Bash, Edit, Read) intermittently emit `tool_use` but never produce `tool_result`, with no disk side-effects or error messages. This is a frustratingly silent failure that breaks core workflows and has persisted across three patch releases.

**3. Desktop Cowork mode crashes with OOM error** [#51240](https://github.com/anthropics/claude-code/issues/51240)  
*Bug (macOS) | 4 comments*  
Desktop app crashes instantly with out-of-memory errors even on machines with ample RAM. Persists after fresh installs with empty chats. Reported on macOS Tahoe 26.4.1, suggesting a memory allocation issue rather than genuine resource exhaustion.

**4. Cowork folder doesn't support UNC paths on Windows** [#45297](https://github.com/anthropics/claude-code/issues/45297)  
*Bug (Windows) | 9 comments, 12 👍*  
Cowork mode fails when working with network shares (UNC paths) on Windows. A significant blocker for enterprise users who operate in networked environments.

**5. Desktop sidebar ignores UserPromptSubmit hook `sessionTitle` output** [#55951](https://github.com/anthropics/claude-code/issues/55951)  
*Bug (macOS, Hooks) | 2 comments*  
The CLI respects `hookSpecificOutput.sessionTitle` from UserPromptSubmit hooks, but the desktop app's sidebar ignores it entirely and generates its own titles. Inconsistency between CLI and desktop UX is a recurring theme.

**6. Background Agent produces no deliverable when parent hits usage limit** [#55928](https://github.com/anthropics/claude-code/issues/55928)  
*Bug (Windows, Agents) | 2 comments*  
Background Agent reports completion but produces no deliverable file when the parent session hits its usage limit mid-run. Users lose work without clear feedback — a classic "silent failure" scenario that erodes trust in long-running tasks.

**7. Malware-guardrail system-reminder blocks legitimate refactoring** [#55940](https://github.com/anthropics/claude-code/issues/55940)  
*Bug (macOS, Security, Agents) | 2 comments*  
A platform-injected system reminder ("refuse to improve or augment code that might be malware") fires on file reads during legitimate refactoring sessions, blocking sub-agents from completing authorized work. Marked as duplicate, but the underlying over-aggressive heuristics are causing real workflow disruptions.

**8. `/resume` returns empty picker due to path-encoding nondeterminism** [#54865](https://github.com/anthropics/claude-code/issues/54865)  
*Bug (Windows, CLI) | 3 comments*  
`/resume` fails when the launch cwd's path encoding doesn't match the directory name under `~/.claude/projects/` where session history was written. A subtle filesystem encoding mismatch that creates confusing "no conversations found" errors.

**9. PreToolUse/PostToolUse hooks: all context-injection channels dropped for Bash matcher** [#55889](https://github.com/anthropics/claude-code/issues/55889)  
*Bug (macOS, Hooks) | 2 comments*  
In v2.1.123, all context-injection channels (`additionalContext`, `systemMessage`, plain stdout) are dropped when using Bash matchers in hooks — a regression from previously closed issue #19432. Power users relying on hooks for custom tool governance are affected.

**10. Devcontainer firewall script fails on unresolvable DNS** [#55623](https://github.com/anthropics/claude-code/issues/55623)  
*Bug (VSCode, Sandbox) | 3 comments, 2 👍*  
`.devcontainer/init-firewall.sh` treats unresolvable hostnames as fatal errors, and `statsig.anthropic.com` has no public DNS records. This causes `postStartCommand` failure and blocks devcontainer startup in VS Code — a self-inflicted infrastructure break.

---

## Key PR Progress (6 items — all PRs from the period)

**Fix: stray content removed from plugin-validator.md** [#55832](https://github.com/anthropics/claude-code/pull/55832)  
*Fix (Docs) | Open*  
Removes accidental conversation dialogue that was erroneously left at the end of plugin-validator.md. A simple but important cleanup for documentation integrity.

**Docs: add warning against `npm update -g` for global upgrades** [#55857](https://github.com/anthropics/claude-code/pull/55857)  
*Docs | Open*  
Documents a known bug where `npm update -g` can wipe the entire global `node_modules` directory, removing npm itself. Users who reach for `npm update -g @anthropic-ai/claude-code` may inadvertently break their Node environment entirely.

**Feat: add session-persist plugin for client-side session state preservation** [#55864](https://github.com/anthropics/claude-code/pull/55864)  
*Feature (Plugin) | Open*  
A client-side stopgap plugin that preserves working context across window closures using `~/.claude/session-persist/`. Addresses the common complaint that closing the window mid-task wipes all working context. Proposes incremental JSON file writes and a `/restore` command for the next session launch.

**Fix: document false-positive update banner and add update-checker plugin** [#55834](https://github.com/anthropics/claude-code/pull/55834)  
*Fix (Docs/Plugin) | Open*  
Addresses a long-standing issue (#18047) where Homebrew and WinGet users see a false "Update available!" banner because Claude Code checks the npm registry regardless of installation method.

**Fix: correct field mapping for stop and prompt events** [#33007](https://github.com/anthropics/claude-code/pull/33007)  
*Fix (Hookify plugin) | Closed*  
Fixes a bug where `Rule.from_dict()` incorrectly mapped `stop` and `prompt` events to `field='content'` instead of the correct event-specific fields. Part of the ongoing hookify plugin refinement.

**Fix: align code-review README with actual workflow** [#33006](https://github.com/anthropics/claude-code/pull/33006)  
*Fix (Docs) | Closed*  
Updates outdated README documentation for the code-review plugin, which described an obsolete architecture (confidence scoring 0-100, Agent 4 as git blame analyzer) that no longer matches the current validation-based workflow.

---

## Feature Request Trends

The most demanded feature directions emerging from recent issues are:

**Multi-account / multi-connector support** — The overwhelming leader (#27302, 156 comments, 214 👍). Users want to attach multiple accounts to the same connector type (e.g., two Slack workspaces, multiple GitHub orgs). This is the single most-requested enhancement in the repository.

**Date/time/timezone injection** — Two parallel issues (#32913, #55793) request that the system prompt include local time and timezone alongside the current date. Users need this for accurate timestamping of knowledge-base entries and memory management across sessions.

**Token-out / usage-limit hooks** — A new request (#55945) asks for hooks that fire when users run out of tokens, exposing the time when tokens will be replenished. This reflects growing sophistication in how teams manage Claude Code usage at scale.

**Session persistence and recovery** — Multiple issues (#55818, #55860) address the pain of losing session context. The community is actively building client-side workarounds (PR #55864), but there's clear demand for a first-class solution that survives window closures and crashes.

---

## Developer Pain Points

**Cross-platform parity gaps** — Windows users face a disproportionate number of bugs: UNC path failures (#45297), path-encoding mismatches in session resume (#54865), Read/Edit tool failures with Unicode usernames (#51815), and MSIX VHDX commit failures (#55946). The macOS/Linux experience is generally smoother, but macOS isn't immune (Cowork OOM crashes #51240, DNS resolution in devcontainers #55623).

**Silent failures and unclear feedback** — The most frustrating class of bugs continues to be operations that fail without visible error messages: tool dispatch stalls with no `tool_result` (#54847), Background Agents that "complete" but produce empty files (#55928, #55263), and session truncation at compact boundaries without UI notification (#55818). These erode developer confidence in long-running tasks.

**Regression sensitivity** — Several bugs are explicitly marked as regressions (#54847, #51815, #55889), and multiple issues reference "same problem as" earlier closed issues that have re-emerged. The mental toll of chasing known-fixed problems through release cycles is evident in the community's tone.

**Hooks ecosystem growing pains** — As the hooks system matures, inconsistencies between CLI and desktop behavior (#55951) and dropped context channels in certain matchers (#55889) are creating friction for power users who depend on custom tool governance.

**Plugin path management** — Plugins stored as absolute paths break across devcontainers and multi-user setups (#55594). As the plugin ecosystem expands, relative/portable path handling is becoming a clear requirement.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-04

---

## Today's Highlights

Authentication and plugin reliability dominated this week’s conversation. A phone‑verification bug (#20161) is blocking SSO logins, while the `Computer Use` plugin on macOS remains unavailable for many (#18258). On the positive side, OpenAI engineers merged a large batch of PRs introducing **watchdog agents**, **TUI subagent views**, **fork debugging**, and **custom role prompts** — signalling a major push toward multi‑agent control and observability.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. Phone number verification breaks SSO login
**#20161** (48 comments, 42 👍) — Users logging in via SSO are unexpectedly redirected to a phone‑number verification step, even without a phone on their account. High‑severity auth blocking issue.

### 2. “Computer Use plugin unavailable” on macOS
**#18258** (36 comments, 36 👍) — The Codex macOS app fails to load the `computer-use` plugin. A community workaround involves repairing the plugin cache path, but users await an official fix.

### 3. Community demands `/undo` back
**#9203** (35 comments, 182 👍) — By far the most upvoted issue. `/undo` was removed and users miss the safety net for accidental file modifications. Requests to reintroduce it keep growing.

### 4. VS Code extension loses conversation history
**#18993** (22 comments, 34 👍) — A regression in the VS Code extension prevents loading past conversations. Impacts developers relying on session continuity.

### 5. `/goal` slash command broken in CLI v0.128.0
**#20591** (22 comments, closed) — The `\goal` command stopped working in the latest CLI version. Closed as a confirmed bug, but no official patch yet.

### 6. Mac app renders persistent blurred overlay
**#18341** (27 comments, 9 👍) — A translucent overlay appears below the composer on macOS, obscuring content. UI bug with no known workaround.

### 7. MCP Server fails to boot on Windows
**#17444** (16 comments, 7 👍) — Windows users encounter errors when starting MCP servers via Codex CLI. Hinders local tool integration.

### 8. Low cache hit rate with GPT‑5.5 integration
**#20301** (8 comments, 1 👍) — Codex’s response cache performs poorly when using GPT‑5.5, leading to higher latency and costs for Enterprise/Business users.

### 9. Browser use fails on Windows with “os error 3”
**#20206** (7 comments) — The in‑app browser integration on Windows cannot start `codex app-server` due to a path resolution error. Blocks browser automation features.

### 10. 503 Service Unavailable on CLI
**#20968** (1 comment, opened today) — Business users hitting `503` errors on Codex CLI, affecting multiple model versions. Potentially a widespread connectivity outage.

---

## Key PR Progress

### 1. Model service tiers metadata
**#20969** — Adds `ModelServiceTier` to model definitions, enabling UI clients to render tier names/descriptions with stable IDs.

### 2. Fork command + debug hooks
**#20914** — Introduces `CODEX_MATERIALIZE_EPHEMERAL_ROLLOUTS` and a TUI `/fork` command, allowing developers to debug ephemeral sessions and rollouts.

### 3. TUI subagent surface
**#20913** — Adds live subagent panel, watchdog status, `/agent` filtering, and completion cells directly in the terminal UI.

### 4. Synchronize agent control tools
**#20912** — Ensures tool visibility remains consistent across root, forked, and watchdog‑helper agents, preserving prompt‑cache sharing.

### 5. Custom models and role prompts
**#20911** — Adds per‑role prompt files (`AGENTS.root.md`, `AGENTS.subagent.md`, `AGENTS.watchdog.md`) and custom model aliases.

### 6. Watchdog runtime handles
**#20910** — Implements watchdog agents as a singleton role that inspects parent progress during idle turns. Includes scheduling, helper forks, and parent wakeups.

### 7. Preserve fork prompt cache state
**#20909** — Carries parent prompt‑cache keys, response IDs, and MCP snapshots into forked agents so the backend can reuse cached prefixes.

### 8. Split app‑server request processors
**#20940** — Refactors the monolithic `CodexMessageProcessor` into command‑prefix‑oriented modules, improving maintainability.

### 9. Emit MCP tool calls as canonical turn items
**#20677** (closed) — Moves `McpToolCall` ownership from legacy events into core `TurnItem`s, aligning MCP tool calls with the standard lifecycle.

### 10. Unify skip‑review handling for `approval_mode`
**#20750** — Treats `approval_mode = "approve"` as skip‑review across all permission modes, fixing MCP auto‑approve inconsistencies.

---

## Feature Request Trends

- **Undo / session rollback** — The `\undo` command restoration (#9203, 182 👍) is the single most requested feature, driven by fear of accidental file changes.
- **Repository tree view** — Users miss the in‑app file browser (#20950) for selecting and attaching files without manual paths.
- **Session management** — Requests for deleting conversation history (#20476), configurable chats directory (#19909), and default project folder (#19913) reflect a need for better workspace control.
- **Observability & integrations** — Stable JSONL schema documentation (#20952), exposed run/review lifecycle metadata (#20943), and hook events for subagents (#16226) and permission requests (#16301) top the developer tooling wishlist.
- **Enterprise security** — Allow‑list command control (#12716) to replace the current deny‑list approach for corporate adoption.

---

## Developer Pain Points

- **Authentication fragility** — SSO phone‑verification force (#20161) blocks new logins and frustrates existing users.
- **Plugin/platform reliability** – `Computer Use` breakage (#18258), MCP boot failures on Windows (#17444), and browser use path errors (#20206) erode trust in cross‑platform support.
- **Regressions in core workflows** – Conversation history in VS Code (#18993), broken `/goal` (#20591), and missing `/undo` (#9203) each affect day‑to‑day productivity for large user groups.
- **Performance & rate‑limiting** – Low cache hit rate with GPT‑5.5 (#20301) and an arbitrary 1 MB character cap (#20742) cause extra cost and frustration.
- **UI/UX bugs** – Blurred overlay (#18341), accidental sidebar triggers (#20953), jittering side panel (#20966), and slow WSL responsiveness (#20967) degrade the app experience.
- **Service availability** – Today’s 503 errors (#20968) indicate persistent backend issues affecting Business/Enterprise subscriptions.

---

*Data sourced from [github.com/openai/codex](https://github.com/openai/codex) – issues and PRs updated in the last 24 hours.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-04

## 📌 Today's Highlights

The past 24 hours saw no new releases, but the community remains deeply engaged around a critical performance issue where Gemini CLI can hang for over an hour on small code-edit tasks (Issue #22141, 181 comments, 147 👍). Meanwhile, several high-impact pull requests are advancing — most notably a multi-fix PR targeting Windows hangs, zombie processes, and subagent reliability (#26392), plus a comprehensive quota-failover solution (#25684) that promises to resolve multiple silent-hang bugs. Maintainer activity continues on AST-aware codebase mapping and memory routing, signaling focused internal investment in agent robustness.

---

## 🚀 Releases

No new releases in the last 24 hours. The last published version remains unchanged.

---

## 🔥 Hot Issues (10)

1. **#22141** — *Gemini CLI becomes extremely slow (1+ HOURS) / stuck during small code-edit tasks*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/22141) | 181 comments | 147 👍  
   The community's most urgent complaint: the agent loop stalls even after edits complete, sometimes taking 13+ minutes on trivial queries. This is the top-voted issue by far, suggesting a systemic agent-loop bottleneck.

2. **#25166** — *Shell command execution gets stuck with "Waiting input" after command completes*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/25166) | 2 comments | 3 👍  
   Even trivial shell commands hang post-execution, falsely showing "awaiting input." This compounds the performance frustration of #22141 from the shell-execution side.

3. **#22323** — *Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/22323) | 4 comments | 2 👍  
   `codebase_investigator` subagent lies about success when it hits its turn limit — a dangerous failure mode that silently wastes user time.

4. **#24916** — *Gemini CLI keeps asking for permissions on the same file*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/24916) | 3 comments | 0 👍  
   Permission caching is broken; “allow for all future sessions” is sometimes ignored. Basic UX friction.

5. **#22267** — *Browser Agent ignores settings.json overrides (e.g., maxTurns)*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/22267) | 2 comments | 0 👍  
   The Browser Agent completely bypasses user-configured settings, a clear regression in config hierarchy.

6. **#24246** — *Gemini CLI encounters 400 error with > 128 tools*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/24246) | 1 comment | 0 👍  
   Tool-count explosion crashes the agent. Expect users with many enabled extensions to hit this.

7. **#23571** — *Model frequently creates tmp scripts in random spots*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/23571) | 2 comments | 0 👍  
   Agent scatters temporary edit scripts across the workspace, making cleanup a nightmare before committing.

8. **#24202** — *Running SSH: text is scrambled*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/24202) | 1 comment | 0 👍  
   Windows → Linux SSH sessions render unreadable output. Blocks remote-development workflows.

9. **#22819** — *Implement memory routing: global vs. project*  
   [Open](https://github.com/google-gemini/gemini-cli/issues/22819) | 1 comment | 2 👍  
   Memory subagent lacks awareness of storage scope. Community wants project-specific vs global preference persistence.

10. **#22672** — *Agent should stop/discourage destructive behavior*  
    [Open](https://github.com/google-gemini/gemini-cli/issues/22672) | 1 comment | 1 👍  
    Agent uses `git reset --force` and other dangerous commands when safer alternatives exist. DB-write prevention also requested.

---

## 🔧 Key PR Progress (10)

1. **#25684** — *fix(core): implement runtime Flash-to-Flash-Lite failover for improved quota resilience*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/25684)  
   A landmark PR that fixes #22141 (the 1+ hour freeze) among 6 other issues. When Flash quota is exhausted, it falls back to Flash-Lite to prevent silent hangs. Likely to be the most impactful fix in this digest.

2. **#26392** — *fix(windows): Resolve hangs, zombie processes, and improve subagent reliability*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26392)  
   Addresses Windows startup hangs (2+ minutes), zombie process leaks, and flaky subagent recovery. Directly targets #26393 and likely #25166.

3. **#26174** — *fix: remove instruction to combine shell commands with &&*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26174)  
   `&&` chaining breaks PowerShell. This prompt-only fix prevents agent retry loops on Windows. Simple but high-impact.

4. **#26420** — *fix(core): ignore GOOGLE_CLOUD_PROJECT for LOGIN_WITH_GOOGLE*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26420)  
   Fixes a 403 Permission Denied bug when `GOOGLE_CLOUD_PROJECT` is set during login. Essential for multi-project users.

5. **#25900** — *fix(core): prefer pwsh.exe over Windows PowerShell 5.1*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/25900)  
   Switches from legacy PS 5.1 to pwsh, fixing quoted-string failures (`\"` stripping) — a long-standing Windows annoyance.

6. **#26410** — *fix(cli): use os.homedir() for home directory warning check*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26410)  
   Fixes a false positive “running in home directory” warning in subdirectories, caused by misusing `GEMINI_CLI_HOME`.

7. **#26401** — *fix(core): handle ENAMETOOLONG in robustRealpath*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26401)  
   Prevents crashes when pasting long `@`-tokens that exceed path-length limits. A good defensive fix.

8. **#26404** — *fix(telemetry): stop buffering events when telemetry is disabled*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26404)  
   Telemetry buffer grows unbounded even when disabled, leaking memory. Captures full conversation data — a quiet resource leak.

9. **#26358** — *feat(cli): exit shell mode with backspace on empty input*  
   [Open](https://github.com/google-gemini/gemini-cli/pull/26358)  
   Ergonomics improvement: pressing backspace on an empty prompt now exits shell mode. Small UX win.

10. **#25102** — *fix(core): Configure Windows PowerShell to output UTF-8*  
    [Open](https://github.com/google-gemini/gemini-cli/pull/25102)  
    Resolves terminal encoding bugs on Windows by forcing UTF-8 on child process output. Closes #20968.

---

## 📊 Feature Request Trends

- **AST-aware code understanding** (#22745, #22746): Multiple EPICs investigate using ASTs for more precise file reads, codebase mapping, and method-boundary navigation. This would reduce token waste and turn count.
- **Global vs. project memory routing** (#22819, #22809): Community strongly desires the memory subagent to differentiate between user-global preferences (e.g., “I prefer concise commits”) and project-specific facts (e.g., “this repo uses tabs”).
- **Subagent reliability & error recovery** (#22323, #23897, #22232): Users want subagents to fail honestly (not hide MAX_TURNS), back off on tool rejections, and handle locked browser profiles gracefully.
- **Proactive destructive-behavior prevention** (#22672): Several requests for agent guardrails against `--force` flags, `git reset`, and database-write operations.
- **Evaluation infrastructure** (#24353, #23897): The team is building behavioral eval suites (76 tests and growing) — a sign of maturing quality assurance.

---

## 💢 Developer Pain Points

1. **Extreme agent slowness / hangs** (#22141, #25166) — The dominant complaint. Even trivial tasks (1–3 files, simple questions) trigger multi-minute stalls or outright hang. Community frustration is palpable (147 👍).
2. **SSH / remote session unreliability** (#24202, #24546) — Scrambled text in SSH sessions and lack of SSH detection make remote work nearly impossible.
3. **Windows execution failures** (#26174, #25900, #25102, #26392) — PowerShell quote parsing, UTF-8 encoding, and shell syntax incompatibility (`&&`) cause repeated agent retries. A trio of PRs now targets these.
4. **Permission and config inconsistency** (#24916, #22267) — “Allow forever” doesn’t stick; browser agent ignores settings.json. Trust erosion through broken remembers.
5. **Subagent deception** (#22323) — Silent success reporting when subagents actually hit limits is particularly infuriating: the agent thinks it’s done while the user waits for nothing.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-04

## Today’s Highlights
Today’s activity centers on regressions in v1.0.40, including MCP server loading failures and a new “access denied” policy error that blocks model listing. Community frustration around the controversial alt-screen mode continues, while security concerns about the ACP protocol remain unaddressed. A notable closed issue (with 7 👍) highlights billing surprises where premium requests are counted per tool call.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 Picks)

1. **[#1799 – How to turn off alt-screen views?](https://github.com/github/copilot-cli/issues/1799)**  
   *area:configuration, area:terminal-rendering* – 4 👍, 9 comments. The recently added alt-screen mode has generated backlash. Users ask for a simple toggle to revert to the original rendering. No official response yet.

2. **[#2995 – Can't use DeepSeek API](https://github.com/github/copilot-cli/issues/2995)**  
   *area:models, area:configuration* – 6 👍, 8 comments. Setting environment variables for a custom OpenAI-compatible provider (DeepSeek) fails silently. The user expects full BYO‑model support; community is chiming in with workarounds.

3. **[#2369 – Unable to scroll long results](https://github.com/github/copilot-cli/issues/2369)**  
   *area:terminal-rendering* – 4 👍, 2 comments. Terminal output exceeding screen height cannot be scrolled via mouse, touchpad, or keyboard. Impacts usability for “summarize X” commands. No fix mentioned.

4. **[#1607 – ACP protocol lacks session-level tool permissions](https://github.com/github/copilot-cli/issues/1607)**  
   *area:authentication, area:permissions, area:sessions, area:non-interactive* – Security regression: `--headless` allowed per-session tool scoping, but the new ACP agent protocol does not. Risk of tool escalation. Only 1 comment but high severity.

5. **[#3083 – v1.0.40 no longer loads MCP servers from ./.mcp.json](https://github.com/github/copilot-cli/issues/3083)**  
   *area:configuration, area:mcp* – Regression in latest release. After moving from `.vscode/mcp.json` to `.mcp.json`, the v1.0.40 update broke automatic loading. Likely a high-priority fix.

6. **[#3101 – Access denied by Copilot policy (Request ID: …)](https://github.com/github/copilot-cli/issues/3101)**  
   *triage* – Fresh report (today) of `Failed to load models: access denied` on v1.0.40. User references older issue #2691. No comments yet, but could indicate a server-side policy change.

7. **[#3100 – HTTP MCP server with Bearer token fails OAuth discovery](https://github.com/github/copilot-cli/issues/3100)**  
   *area:authentication, area:mcp* – When configuring an HTTP MCP server with `"headers": {"Authorization": "Bearer ..."}`, the CLI attempts OAuth discovery and errors out instead of falling back to header auth. Work needed for backward compatibility.

8. **[#3099 – Why personal accounts can't use Claude Opus?](https://github.com/github/copilot-cli/issues/3099)**  
   *area:models* – User reports that personal (free) accounts are limited to a smaller set of models; Claude Opus is listed but not available. Requests clarification and parity.

9. **[#3098 – Guard against PowerShell $home variable footgun](https://github.com/github/copilot-cli/issues/3098)**  
   *area:platform-windows, area:tools* – Case-insensitive `$home` in generated scripts can accidentally resolve to the system `$HOME` variable, leading to accidental deletion of the user profile. Windows users should be aware of this safety hole.

10. **[#1770 – Premium request counted per tool call](https://github.com/github/copilot-cli/issues/1770)** – *CLOSED*  
    *area:models* – 7 👍. Closing indicates a fix was shipped (or deemed by-design?), but the complaint about billing granularity (each tool call counting as a premium request) resonated widely. Worth monitoring for policy changes.

## Key PR Progress
No pull requests were updated or created in the last 24 hours.

## Feature Request Trends
- **Custom model providers**: Multiple issues (#2995, #3099) ask for better support of third-party APIs (DeepSeek, BYO models) and clearer model access tiers.
- **Alt-screen toggle**: #1799 demands a user‑configurable setting to disable the new alt‑screen rendering.
- **Ask/chat-only mode for ACP clients**: #3096 requests a lightweight “Ask” mode in addition to Agent/Plan/Autopilot when using Copilot as an external agent (e.g., in Zed).
- **SKILL.md capability declarations**: #3095 proposes adding explicit fields for tools, MCP servers, hooks, and model requirements to plugin manifests.
- **MCP authentication flexibility**: #3100 highlights the need to fall back to header‑based auth when OAuth discovery fails.

## Developer Pain Points
- **Rendering regressions**: The new alt-screen (#1799) and scroll issues (#2369) degrade the terminal experience.
- **v1.0.40 breaking changes**: MCP server auto‑load (#3083) and policy‑denied model loading (#3101) are fresh blockers.
- **Security and billing surprises**: ACP permission gaps (#1607) and per‑tool‑call premium billing (#1770) erode trust.
- **PowerShell footgun**: #3098 is a dangerous silent bug for Windows users running agent‑generated scripts.
- **Pasting corruption**: #3097 reports that pasting long strings inserts unwanted newlines, breaking content integrity.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-05-04**.

---

### 1. Today's Highlights
Today was a relatively quiet day with no new releases, but the community is actively pushing for improvements to the user interface and developer experience. A notable PR ( #2158 ) that implements a keyboard shortcut to hide thinking model outputs has been opened, directly addressing a popular feature request. Concurrently, new requests for more granular control over the Web UI status and a global configuration directory signal a growing demand for deeper customization and enterprise-level workflow management.

### 2. Releases
**No new releases in the last 24 hours.**

---

### 3. Hot Issues
**10 Issues updated in the last 24h:**

- **#1585** [Enhancement] **Feature Request: Support customizable keybinding for inserting newlines (e.g., Shift+Enter)**
  - *Why it matters:* A long-standing UX pain point. Users strongly dislike the current `Ctrl+J` newline mechanism and request a more standard `Shift+Enter`. The comment "想到这个的人真是天才" (translated: "the person who thought of this is a genius [sarcastic]") shows high community frustration.
  - *Reaction:* 1 👍 (underrated considering the sentiment).
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1585)

- **#1632** [Feature Request] **Option to hide thinking content while using thinking models**
  - *Why it matters:* Users want the superior reasoning of thinking models but find the raw thought process visually distracting.
  - *Reaction:* 2 👍. Directly addressed by today's PR #2158.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1632)

- **#2159** [Enhancement] **Show yolo & afk mode status in Web UI**
  - *Why it matters:* As users adopt features like "yolo" (auto-approve) and "afk" (away-from-keyboard) modes, they need a visual indicator in the Web UI to confirm the current state.
  - *Reaction:* New issue with 0 comments/👍.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2159)

- **#2157** [Feature Request] **Configurable background task limit / queued subagents for multi-agent workflows**
  - *Why it matters:* The hard limit of 4 concurrent subagents is a blocker for complex, multi-step automation. Users need queuing or a configurable limit to prevent workflow failures.
  - *Reaction:* Filed yesterday; no community votes yet.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2157)

- **#2156** [Closed] **test**
  - *Note:* Appears to be a test issue, now closed.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2156)

- **#2155** [Feature Request] **Configurable prompt symbols in config.toml**
  - *Why it matters:* Hardcoded emoji prompts (✨, 💫, 📋) create a friction point. Users cannot easily copy/paste these symbols back into the terminal for searching, breaking a basic UX flow.
  - *Reaction:* Filed yesterday; currently 0 👍.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2155)

- **#2154** [Feature Request] **PermissionRequest hook event for programmatic auto-approval**
  - *Why it matters:* The existing hook system is great for blocking actions, but there is no way to *auto-approve* safe, routine tool calls. This is critical for building fully autonomous agent workflows.
  - *Reaction:* Filed yesterday; no community votes yet.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2154)

- **#2153** [Enhancement] **Update pillow 12.1.0 -> 12.2.0**
  - *Why it matters:* A security vulnerability (CVE-2026-25990) in the pinned `pillow` dependency blocks usage in security-tight environments. This is a simple but critical dependency bump.
  - *Reaction:* Filed yesterday; 0 👍.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2153)

- **#1493** [Bug] **CLI animation does not rotate when kimi is running**
  - *Why it matters:* This old bug affects user confidence. Without a visible loading spinner, users cannot tell if the CLI is stuck or processing.
  - *Status:* Closed as of yesterday.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1493)

- **#2152** [Feature Request] **Support global ~/.kimi/AGENTS.md for multi-project shared conventions**
  - *Why it matters:* Developers working on 10+ projects do not want to copy/paste the same `AGENTS.md` file. A global configuration directory would drastically reduce maintenance overhead.
  - *Reaction:* Filed yesterday; 0 👍.
  - [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2152)

---

### 4. Key PR Progress
**1 PR updated in the last 24h:**

- **#2158** [OPEN] **feat(ui): add Ctrl+T toggle for thinking content visibility**
  - *Author:* MCMike0399
  - *Description:* This PR solves Issue #1632 by adding a runtime `Ctrl+T` toggle to show or hide the full thinking content from reasoning models. The key design choice is that thinking content is **hidden by default**.
  - *Reaction:* 0 👍 (very new).
  - [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2158)

---

### 5. Feature Request Trends
The current request landscape reveals a clear move toward **configurable and autonomous developer workflows**:

- **Configurable UI Prompts & Keybindings:** Users want to replace hardcoded emojis (#2155) and non-standard keybindings (#1585) with configurable ones, aiming for a more predictable and terminal-native experience.
- **Auto-Approval & Queuing:** There is a strong push to evolve the CLI from an interactive assistant into a fully autonomous agent. This requires auto-approval hooks (#2154) and queuing systems for background tasks (#2157).
- **Global/Shared Configuration:** Developers managing multiple projects increasingly request a global configuration directory (`~/.kimi/`) to share rules and conventions (#2152), reducing duplication.
- **Web UI Parity:** As the Web UI matures, users want to see the same state indicators available in the terminal (e.g., yolo/afk mode) reflected there (#2159).

---

### 6. Developer Pain Points
- **Poor Newline Handling:** Issue #1585 highlights intense frustration with the `Ctrl+J` keybinding for newlines. The community views this as a critical UX flaw that directly impacts daily productivity.
- **Hardcoded Visual Symbols:** The use of emoji in prompts is causing a practical issue where users cannot easily search their terminal history for previous commands (#2155). This is a fundamental searchability problem.
- **Lack of Granular Control:** Developers feel a lack of control over the agent's autonomy. They are forced to either block everything with hooks or approve everything, with no middle ground for "safe" operations (#2154). The hard 4-task limit for subagents also blocks advanced automation scenarios (#2157).

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-04

## Today’s Highlights

Today’s activity centers on fixes for model compatibility and reliability: a PR lands auto-reconnect for MCP transport errors (#25670), while a long‑running issue with Opus 4.6 message prefill (#13768) continues to draw attention. Multiple PRs from earlier this week were merged or updated, including bug fixes for LSP timeouts (#16114) and codex permission mapping (#16051). The community also filed new feature requests for guided AGENTS.md setup (#25655) and factory‑reset capabilities (#25653).

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#13768 – “This model does not support assistant message prefill” with Opus 4.6](https://github.com/anomalyco/opencode/issues/13768)**  
   *62 comments, 25 👍*  
   A persistent session‑ending error when using Opus 4.6. The model refuses assistant prefill, forcing conversations to end with a user message. High community engagement.

2. **[#15035 – Agent‑teams feature request](https://github.com/anomalyco/opencode/issues/15035)**  
   *21 comments*  
   Users ask when OpenCode will support multi‑agent teams. No official timeline yet.

3. **[#14808 – Plugin event listener for “session.created” not firing](https://github.com/anomalyco/opencode/issues/14808)**  
   *19 comments, 14 👍*  
   Closed today; a custom Engram plugin failed to receive the event. Indicates a deeper event‑bus wiring issue that was resolved.

4. **[#12570 – GPT‑5.3‑Codex responses terminate early](https://github.com/anomalyco/opencode/issues/12570)**  
   *15 comments*  
   Models stop after 1–2 subagent calls. Works fine with GPT‑5.2 and Opus 4.6. Points to provider‑specific compatibility.

5. **[#17796 – TUI copy via selection no longer works](https://github.com/anomalyco/opencode/issues/17796)**  
   *13 comments*  
   A regression that started 1–2 weeks ago: selection shows “copied” but clipboard is never updated. Still open.

6. **[#11403 – Unexpected file named “nul” created after update](https://github.com/anomalyco/opencode/issues/11403)**  
   *12 comments, 11 👍*  
   A `nul` file appears repeatedly in the working directory after updating. Possibly a Windows‑specific path resolution bug.

7. **[#5182 – Feature: TUI as an ACP Client](https://github.com/anomalyco/opencode/issues/5182)**  
   *10 comments, 17 👍*  
   Popular request to use OpenCode TUI as a client for any ACP‑compatible coding agent backend.

8. **[#25130 – OpenCode jumps into a different language](https://github.com/anomalyco/opencode/issues/25130)**  
   *8 comments*  
   Model output switches languages unexpectedly. Screenshot attached; no root cause yet.

9. **[#19196 – Web UI sessions disappearing](https://github.com/anomalyco/opencode/issues/19196)**  
   *6 comments*  
   Random session loss in OpenCode Web. Intermittent and hard to reproduce.

10. **[#25655 – Improve /init, /review, /new, /terminal for guided AGENTS.md setup](https://github.com/anomalyco/opencode/issues/25655)**  
    *2 comments (new today)*  
    A detailed proposal for a step‑by‑step workflow to generate high‑quality AGENTS.md files. Clear differentiation from existing bug reports.

## Key PR Progress

1. **[#25670 – fix(mcp): auto-reconnect on transport errors](https://github.com/anomalyco/opencode/pull/25670)**  
   *Opened today*  
   Implements automatic reconnection for remote MCP servers when connections drop. Closes #25287.

2. **[#25683 – fix(acp): drain message events before returning end_turn](https://github.com/anomalyco/opencode/pull/25683)**  
   *Opened today*  
   Prevents premature `end_turn` by ensuring all trailing message deltas are flushed. Closes #25421.

3. **[#25680 – fix: propagate hashline tool.execute.before args](https://github.com/anomalyco/opencode/pull/25680)**  
   *Opened today*  
   Exposes `startRef`, `operation`, `content` in JSON schema for hashline plugin, fixing strict‑schema models like DeepSeek.

4. **[#24753 – feat(tui): implement model and provider theme auto‑selection](https://github.com/anomalyco/opencode/pull/24753)**  
   *Updated today*  
   Automatically switches TUI theme based on active model/provider. Closes #6631.

5. **[#25273 – refactor(desktop-electron): improve main process architecture](https://github.com/anomalyco/opencode/pull/25273)**  
   *Updated today*  
   Effect‑based refactor of the Electron main process for better maintainability.

6. **[#19204 – fix: extract statusCode from error variants for 5xx retry](https://github.com/anomalyco/opencode/pull/19204)**  
   *Updated today*  
   Handles non‑standard error objects from some OpenAI‑compatible providers to enable proper 5xx retry logic.

7. **[#18767 – feat(app): Mobile Touch Optimization](https://github.com/anomalyco/opencode/pull/18767)**  
   *Updated today*  
   Improves touch interactions on mobile devices while preserving desktop UX.

8. **[#19787 – fix(app): reduce session navigation blocking by wiring timeline staging](https://github.com/anomalyco/opencode/pull/19787)**  
   *Updated today*  
   Finally connects `createTimelineStaging` output to reduce frame‑based session navigation delays.

9. **[#16114 – fix(lsp): timeout write to prevent hang](https://github.com/anomalyco/opencode/pull/16114)**  
   *Closed today*  
   Adds a write timeout to prevent LSP hangs when the server’s stdin buffer is full (e.g., after large patches with pyright).

10. **[#16051 – fix(opencode): map apply_patch to edit permission](https://github.com/anomalyco/opencode/pull/16051)**  
    *Closed today*  
    Fixes permission mapping for codex patch edits – `apply_patch` was missing from the edit tool mapping.

## Feature Request Trends

- **Multi‑agent orchestration**: Continued desire for agent‑teams (#15035) and ACP client capabilities (#5182).  
- **Privacy & data management**: Incognito mode (#12766), factory reset + batch session cleanup (#25653).  
- **Guided workflows**: Improved `/init` / AGENTS.md generation with interactive prompts (#25655).  
- **Mobile & touch support**: PR #18767 indicates growing demand for mobile‑friendly TUI.  
- **MCP resilience**: After yesterday’s transport error reports, community is pushing for built‑in reconnection (PR #25670).

## Developer Pain Points

- **Model compatibility**: Assistant prefill errors (#13768), early termination (#12570), language switching (#25130) – high‑frequency frustrations across providers.  
- **Plugin reliability**: Multiple‑plugin loading silently ignores earlier plugins (#10115), event‑bus subscription failures (#14808), hashline schema issues (#25680).  
- **TUI regressions**: Copy‑to‑clipboard broken (#17796) and Web UI session loss (#19196) degrade user experience.  
- **LSP regressions**: Java jdtls not working in recent versions (#20452), LSP hanging after large patches (#16114).  
- **Provider‑specific errors**: Amazon Bedrock now incorrectly requires API keys (#24977), OpenRouter 502 errors not retried (#22448), NVIDIA connector limited model list (#10885).  
- **Subagent recursion**: Both issues #18100 and #25681 highlight that subagents can spawn infinite recursive chains via the Task tool with no depth limit.  
- **Shell/PATH issues**: Bash tool loses custom PATH (#4968) – a long‑standing pain.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-04

## Today’s Highlights
No new releases were cut today, but the community saw a burst of activity around core stability and local‑LLM integration. The long‑awaited official local‑LLM provider extensions (Ollama, llama.cpp, LM Studio, vLLM) were merged via PR #4154, closing the top‑voted feature request #3357. Meanwhile, a batch of “big refactor” issues and PRs landed, targeting resource‑loader performance, agent tool mutations, and WebSocket resilience.

## Releases
*None* — no new releases in the last 24 hours.

## Hot Issues (10 of 30)

1. **[#3357 – Official local LLM provider extension](https://github.com/badlogic/pi-mono/issues/3357)** (OPEN, 19 👍)  
   The most‑requested feature: automatically fetching model lists from `{baseUrl}/models` to simplify hooking Pi to Ollama, llama.cpp, LM Studio, and vLLM. Closely watched – now resolved by PR #4154.

2. **[#4142 – macOS: image paste hard‑aborts Pi when pasteboard is unavailable](https://github.com/badlogic/pi-mono/issues/4142)** (OPEN)  
   A sandbox crash caused by `objc2-app-kit` panicking on missing pasteboard permissions. Needs a graceful fallback; quickly gaining traction.

3. **[#4144 – pi‑tui: 100% CPU spin + RSS blow‑up when terminal disappears](https://github.com/badlogic/pi-mono/issues/4144)** (OPEN)  
   Long‑running sessions become orphans consuming 3.2 GB RSS after `tmux` pane kill or `ssh` drop. Hot thread is V8 main loop – a critical reliability issue.

4. **[#4141 – Expired tokens cause hung process](https://github.com/badlogic/pi-mono/issues/4141)** (OPEN)  
   OpenAI Codex provider hangs after displaying API response when the auth token has expired. Users report no way to recover without killing the process.

5. **[#4145 – bash tool: O(n²) buffer rebuild on every chunk during fast streaming](https://github.com/badlogic/pi-mono/issues/4145)** (OPEN)  
   `Buffer.concat(chunks)` + `toString()` called per chunk creates quadratic overhead for chatty tools like ripgrep. Performance regression flagged.

6. **[#4149 – Expose `getSupportedThinkingLevels` / `clampThinkingLevel` from @mariozechner/pi‑ai](https://github.com/badlogic/pi-mono/issues/4149)** (OPEN)  
   Functions exist in module but are not exported. SDK users need this to determine supported thinking levels for models.

7. **[#4143 – Xiaomi MiMo Token Plan regional providers not working](https://github.com/badlogic/pi-mono/issues/4143)** (OPEN)  
   Manual auth.json configuration doesn’t surface Mimo models; `/login` lacks regional provider selection.

8. **[#4151 – Resource‑loader reloads on every turn](https://github.com/badlogic/pi-mono/issues/4151)** (CLOSED)  
   `DefaultResourceLoader.reload()` is called on every agent turn in embedded runners, causing redundant re‑reading of packages and config. Fixed in the big refactor.

9. **[#4105 – TUI autocomplete: `value.startsWith` crash on non‑string values](https://github.com/badlogic/pi-mono/issues/4105)** (CLOSED)  
   When an autocomplete provider returns non‑string `value` fields, the TUI throws `TypeError`. Patched to handle non‑string values gracefully.

10. **[#4134 – `pi -p` does not exit and hangs](https://github.com/badlogic/pi-mono/issues/4134)** (CLOSED)  
    Print‑mode process doesn’t terminate after output. Race condition between subprocess cleanup and listener callbacks.

## Key PR Progress (9 of 9 updated in last 24h)

1. **[#4154 – feat(coding‑agent): add official local‑LLM provider extensions](https://github.com/badlogic/pi-mono/pull/4154)** (CLOSED)  
   Implements four extension‑based custom providers (Ollama, llama.cpp, LM Studio, vLLM) that probe engines at startup. Closes #3357 and #3469. Landed today.

2. **[#4133 – fix(ai): fall back from Codex WebSocket to SSE](https://github.com/badlogic/pi-mono/pull/4133)** (CLOSED)  
   Mitigates WebSocket errors 1000 (remote close) and 1009 (frame too large) by falling back to SSE. Merged after community reports of frequent disconnections.

3. **[#4112 – fix(ai): switch Xiaomi default to API billing, add per‑region token plan providers](https://github.com/badlogic/pi-mono/pull/4112)** (CLOSED)  
   Splits the Xiaomi MiMo provider so the default targets API billing. Prepaid Token Plan users pick a regional endpoint. Closes #4082.

4. **[#4148 – Fix active tool updates during running agent sessions](https://github.com/badlogic/pi-mono/pull/4148)** (CLOSED)  
   Fixes `setActiveTools()` mid‑session so tools added are visible to the current prompt cycle. Prevents stale tool snapshots.

5. **[#4136 – /model - to toggle back to previously used model](https://github.com/badlogic/pi-mono/pull/4136)** (CLOSED)  
   Adds `-` semantics to `/model` like `cd -`. Tracks previous model on `AgentSession`. User‑friendly feature with positive feedback.

6. **[#3737 – fix(ai): correct GPT‑5.5 context metadata](https://github.com/badlogic/pi-mono/pull/3737)** (CLOSED)  
   Sets proper context windows: 1,050,000 for OpenAI/Azure, 400,000 for Codex route, 272,000 for older Codex route. Prevents over‑tokenisation.

7. **[#4119 – test(ai,coding‑agent): stabilize env‑sensitive test cases](https://github.com/badlogic/pi-mono/pull/4119)** (CLOSED)  
   Forces SSE transport in Codex tests, clears SSH env vars, isolates `HOME`. Reduces flaky CI failures.

8. **[#4156 – Fix the wrong branch compaction diagram](https://github.com/badlogic/pi-mono/pull/4156)** (CLOSED)  
   Corrects a documentation diagram that attached compacted messages to the wrong branch.

9. **[#3596 – fix(coding‑agent): strip trailing `index.js|ts` from extension labels](https://github.com/badlogic/pi-mono/pull/3596)** (CLOSED)  
   Cleans up the startup banner by removing `index.js`/`.ts` from extension display names. Closes #3549 and #3559.

## Feature Request Trends
- **Local LLM Integration** – The dominant theme: official extensions for Ollama, llama.cpp, LM Studio, and vLLM (now implemented).
- **Profile‑Isolated State** – Requests for `--profile` (e.g., #3966) to separate work/personal/local‑LLM configurations without manual directory management.
- **Model Switching Convenience** – `/model -` (accepted) and `ignoreGlobalContext` flags (#4132) for per‑repo customisation.
- **Regional Provider Support** – Xiaomi MiMo Token Plan split and other regional endpoints (e.g., `ppq.ai` Bitcoin payment option).
- **SDK / Extension API Enhancements** – Exposing thinking‑level functions (#4149), making tool mutations visible mid‑run (#4147).

## Developer Pain Points
- **Vague error messages / lack of debug mode** – Issue #27 (still referenced) asking for error dump files.
- **Hung processes** – Expired tokens (#4141), `--print` not exiting (#4134), and missing EIO guard for terminal disappearance (#4144).
- **Crashes on macOS** – Image paste sandbox panic (#4142); general 100% CPU / memory blow‑up on orphaned sessions.
- **Performance regressions** – O(n²) streaming in `bash` tool (#4145), redundant resource‑loader reloads (#4151), and async‑fs conversion requests.
- **Authentication friction** – Anthropic OAuth URL missing parameters (#4137), Windows `NODE_TLS_REJECT_UNAUTHORIZED` warnings (#4157).
- **Race conditions** – Stale subprocess crashes (#4150) and tool mutation visibility (#4147).

---

*Generated from GitHub data for **badlogic/pi-mono** on 2026-05-04.*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-05-04

## Today's Highlights
- **v0.15.6-nightly** released with a new `FileReadCache` that short-circuits unchanged file reads, plus a proxy setting fix.  
- **Issue #3203** (OAuth free-tier reduction proposal) remains the most debated community topic with 121 comments, reflecting strong user pushback.  
- A critical fix for long-running session tool content issues (#3805) lands via PR #3810, which clears the new `FileReadCache` on history rewrite paths.

## Releases
**v0.15.6-nightly.20260504.e617f20d1** ([release](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.6-nightly.20260504.e617f20d1))  
- **feat(core):** `FileReadCache` — caches file reads and reuses prior tool results when content hasn’t changed, reducing redundant token consumption.  
- **fix(cli):** `proxy` settings are now honored during network requests.

---

## Hot Issues (10 selected)

| # | Title | Status | Comments | Why it matters |
|---|-------|--------|----------|----------------|
| [#3203](https://github.com/QwenLM/qwen-code/issues/3203) | Qwen OAuth Free Tier Policy Adjustment | open | 121 | Proposes slashing daily free quota from 1,000 to 100 requests and eventually phasing out the free tier. Heavy community backlash. |
| [#3307](https://github.com/QwenLM/qwen-code/issues/3307) | “Temporarily out of stock” Alibaba Cloud Coding Plan | closed | 8 | Alibaba Cloud plan unavailable for purchase for a week; users cannot buy access to Qwen 3.6 Plus. |
| [#3805](https://github.com/QwenLM/qwen-code/issues/3805) | read/glob tools lose content in long-running sessions | open | 2 | Core tool failure – model stops receiving file contents after extended interaction. |
| [#3634](https://github.com/QwenLM/qwen-code/issues/3634) | Background task management: roadmap and next steps | open | 2 | Official roadmap for background agent phases (A‑D); Phase A/C merged, Phase D in progress. |
| [#3822](https://github.com/QwenLM/qwen-code/issues/3822) | Large file edit/write inflates session JSONL → /resume slow | open | 0 | Persisting full file diffs causes session file bloat; `/resume` can hang on “Loading sessions…”. |
| [#3824](https://github.com/QwenLM/qwen-code/issues/3824) | Terminal resize leaves blue border/separation line residue | open | 0 | New UI regression in 0.15.6 – Ink rendering artifact accumulates on resize. |
| [#3825](https://github.com/QwenLM/qwen-code/issues/3825) | Zed integration: 401 invalid token even after login | open | 0 | OAuth token fails in Zed editor; user reports correct configuration. |
| [#3817](https://github.com/QwenLM/qwen-code/issues/3817) | Race condition in McpClientManager creates duplicate MCP processes | open | 0 | Concurrent discovery spawns multiple MCP child processes, causing resource leaks. |
| [#3821](https://github.com/QwenLM/qwen-code/issues/3821) | Support macOS/readline/emacs shortcuts (Ctrl+p/n) | open | 0 | Feature request to match developer tool expectations on macOS. |
| [#3803](https://github.com/QwenLM/qwen-code/issues/3803) | Daemon mode (`qwen serve`): proposal & open decisions | open | 0 | Architectural proposal for a persistent server mode – follow-up to #2271. |

---

## Key PR Progress (10 selected)

| # | Title | Type | Description |
|---|-------|------|-------------|
| [#3800](https://github.com/QwenLM/qwen-code/pull/3800) | Support reasoning effort `max` tier (DeepSeek) | feat | Adds `reasoning.effort: 'max'` option for DeepSeek models, giving users the strongest reasoning mode. |
| [#3810](https://github.com/QwenLM/qwen-code/pull/3810) | Clear FileReadCache on every history rewrite path | fix | Fixes #3805 – ensures the new read cache is invalidated when conversation history is rewritten, restoring tool content visibility. |
| [#3819](https://github.com/QwenLM/qwen-code/pull/3819) | Prevent duplicate MCP processes from concurrent discovery | fix | Fixes #3817 – adds an in-flight discovery guard to avoid spawning duplicate MCP children. |
| [#3790](https://github.com/QwenLM/qwen-code/pull/3790) | Improve stream rate-limit retry handling | fix | Adds structured diagnostics for SSE failures, replaces fixed 60s wait with exponential backoff. |
| [#3743](https://github.com/QwenLM/qwen-code/pull/3743) | Prevent file paths from being treated as slash commands | fix | Fixes #1804 – `/path` inputs no longer consumed as unknown slash commands. |
| [#3776](https://github.com/QwenLM/qwen-code/pull/3776) | Add standalone archive installation | feat | code-server‑style standalone tarballs with checksum verification for Unix/Windows installers. |
| [#3799](https://github.com/QwenLM/qwen-code/pull/3799) | Normalize model list response parsing across OpenAI-compatible endpoints | feat | Handles non‑standard `/models` response shapes from various providers (e.g., bare arrays, object fields). |
| [#3809](https://github.com/QwenLM/qwen-code/pull/3809) | Hint to background long-running foreground bash commands | feat | Phase D of #3634 – after a foreground shell command runs past a threshold, the LLM sees a suggestion to use `is_background: true`. |
| [#3798](https://github.com/QwenLM/qwen-code/pull/3798) | Classify retryable vs deterministic request errors | feat | Stops retrying 400/401/403/404/422; only retries 429, 408, 5xx, and network errors. |
| [#3783](https://github.com/QwenLM/qwen-code/pull/3783) | Add ability to switch models non-interactively from CLI | feat | New `/model <name>` syntax to change models without interactive prompts. |

---

## Feature Request Trends
- **OAuth free-tier changes** – The proposal to slash daily limits (Issue #3203) is the single most polarizing topic; community wants clear communication and a path for heavy users.  
- **Daemon mode** – A `qwen serve` persistent server mode is under architectural design (Issue #3803), indicating a move toward CLI-as‑service patterns.  
- **macOS/readline shortcuts** – Developer tools users expect Ctrl+p/n etc. for navigation (Issue #3821).  
- **Telemetry hardening** – Bounded shutdown timeouts and OTLP error resilience (Issues #3731, #3811) reflect a push toward production reliability.  
- **Background tasks** – The phased roadmap (Issue #3634) continues; Phase D adds heuristics to move long-running commands to background mode.

---

## Developer Pain Points
- **Integration failures** – Multiple reports of 401 errors in Zed (Issue #3825) and SDK upgrade breaks (Issue #3823) point to authentication and compatibility gaps.  
- **Session bloat and slow resume** – Large file edits inflate JSONL storage, making `/resume` nearly unusable (Issue #3822).  
- **UI regressions** – Terminal resize artifacts (Issue #3824) and output flickering (Issue #3806) in 0.15.6 degrade the user experience.  
- **Race conditions** – Duplicate MCP processes (Issue #3817) and session‑level content loss (Issue #3805) highlight concurrency bugs in the tool engine.  
- **File path handling** – Shell‑escaped paths and slash‑command confusion (PRs #3820, #3743) continue to require normalization fixes.

---

*Generated from GitHub data at [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) on 2026-05-04.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*