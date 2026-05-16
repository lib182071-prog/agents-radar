# AI CLI Tools Community Digest 2026-05-16

> Generated: 2026-05-16 07:32 UTC | Tools covered: 8

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
**Date:** 2026-05-16 | **Tools Analyzed:** Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing a maturation phase characterized by escalating community engagement, systematic reliability challenges, and convergent feature demands. While each tool targets overlapping developer workflows (code generation, agentic task execution, sandboxed operations), their architectural choices and community dynamics reveal distinct strategic positions. Claude Code and OpenCode lead in community scale and feature breadth, while Qwen Code and Gemini CLI demonstrate aggressive feature velocity through architectural innovation (daemon mode, AST-aware tools). A shared industry challenge has emerged around **streaming reliability, context window management, and cross-platform terminal compatibility**—pain points that transcend individual tools. The ecosystem is also witnessing a shift from "demo-grade" agent loops to production-grade orchestration, with MCP (Model Context Protocol) convergence, sandbox hardening, and reasoning model support becoming universal priorities.

---

## 2. Activity Comparison (2026-05-16)

| Tool | Hot Issues (24h) | Key PRs (24h) | Release Status | Community Engagement Signal |
|------|------------------|---------------|----------------|----------------------------|
| **Claude Code** | 10 (85👍 top) | 2 | ✅ v2.1.143 shipped | Strongest upvote density; 228👍 on mobile switching |
| **OpenAI Codex** | 10 (15 comments top) | 10 | ✅ 2 alpha releases | High comment volume; Windows session loss dominant |
| **Gemini CLI** | 10 (7👍 top) | 10 | ❌ No release | Moderate engagement; agent hang (#21409) persistent |
| **GitHub Copilot CLI** | 10 (11👍 top) | 0 | ✅ 2 releases | Lower issue volume; authentication + MCP tooling focus |
| **Kimi Code CLI** | 7 (14 comments top) | 4 | ❌ No release | **Lowest activity**; K2.6 model overload critical |
| **OpenCode** | 10 (77 comments top) | 10 | ✅ v1.15.1 shipped | High community engagement; memory megathread driving |
| **Pi** | 10 (18 comments top) | 10 | ❌ No release | Strong PR activity; reasoning_content bugs widespread |
| **Qwen Code** | 10 (125 comments top) | 10 | ✅ 3 releases | **Highest comment count**; OAuth policy backlash (#3203) |

**Key observations:**
- **OpenCode and Qwen Code tie for most PR activity**, reflecting sustained engineering investment.
- **Kimi Code CLI is the weakest performer**—lowest issue count, fewest PRs, and a critical model-overload bug unresolved for 3 weeks.
- **Qwen Code's 125-comment issue (#3203)** signals community volatility around pricing/policy changes.
- **Claude Code's 228👍 feature request** demonstrates unmatched user demand for multi-account support.

---

## 3. Shared Feature Directions

| Shared Requirement | Tools Affected | Specific Needs |
|-------------------|----------------|----------------|
| **MCP ecosystem standardization** | Claude Code, Copilot CLI, OpenCode, Pi, Qwen Code | Config schema alignment (env/`environment` field), auto-reconnect, streamable-HTTP, discoverable registries |
| **Session recovery & persistence** | Claude Code, Codex, Gemini CLI, Copilot CLI, Kimi, OpenCode, Qwen Code | Crash-safe session restore, SSE stall handling, session JSONL reliability, worktree session persistence |
| **Windows platform parity** | Claude Code, Codex, Copilot CLI, Gemini CLI, Kimi, Qwen Code | Path case sensitivity, npm `.cmd` shims, auth DNS resolution, PowerShell quoting, keybinding conflicts |
| **Terminal/rendering quality** | Claude Code, Codex, Gemini CLI, Copilot CLI, OpenCode, Pi, Qwen Code | Raw mouse sequence pollution, resize flicker, scroll lock, Dvorak keybinds, Shift+Enter compatibility |
| **Memory/context management** | Claude Code, OpenCode, Pi, Qwen Code | V8 OOM in long sessions, auto-compaction reliability, progressive-disclosure skills, heap diagnostics |
| **Reasoning model support** | Pi, Claude Code, Qwen Code | `reasoning_content` preservation in tool calls, adaptive thinking budgets, "None" reasoning effort option |
| **Agent observability** | Codex, Gemini CLI, OpenCode, Copilot CLI | Sticky agent headers, subagent progress visibility, per-call token usage, turn-level duration tracking |
| **Sandbox/worktree isolation** | Claude Code, Codex, Gemini CLI, OpenCode | Git write permissions, worktree isolation gaps, hook validation, background task lifecycle |

**Notable convergent urgency:** **Session recovery and SSE streaming reliability** appear across 6 of 8 tools, making it the highest-priority cross-cutting concern. **Windows compatibility** is the second most common pain point, with every tool except Pi reporting at least one Windows-specific regression.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code |
|-----------|-------------|--------------|------------|-------------|-----------|----------|-----|-----------|
| **Primary UX** | Plugin-heavy, TUI-first | Permission-profile, Guardian sandbox | Multi-agent orchestration | Prompt-mode, MCP extensions | Shell-UI with hooks | TUI + agent marketplace | Minimalist, terminal-compatible | Daemon mode, worktree |
| **Target User** | Full-stack developers, plugin authors | Enterprise, security-conscious teams | Google ecosystem users, sub-agent workflows | Git/CLI veterans, MCP enthusiasts | East Asian market, cost-sensitive | Agent marketplace adopters, tinkerers | Provider-agnostic power users | Heavy automation, IDE-integration |
| **Architecture** | Node.js, VSCode extension | Rust-based (alpha) | Rust-native | Go-based | Python + asyncio | TypeScript/Node.js | Node.js, provider-agnostic | Node.js, daemon-adapter pattern |
| **Key Strength** | Feature breadth, community scale | Security model (Guardian, approval routing) | Sub-agent orchestration, OAuth | GitHub ecosystem integration | K2.6 model access, low cost | Agent marketplace, memory diagnostics | Provider diversity, theme system | Daemon mode, architecture docs |
| **Key Weakness** | Streaming instability, plugin fragility | Windows update regressions, quota opacity | Agent hangs, sub-agent recovery | Auth failures on Windows, silent exits | Model overload, lowest community health | Terminal pollution, version instability | `reasoning_content` bugs, terminal edge cases | OOM in long sessions, OAuth policy risk |
| **Community Health** | ✅ Strong, organized | ✅ Moderate, growing | ✅ Moderate, stable | ⚠️ Low issue velocity | ❌ Stagnant | ✅ High energy, PR-driven | ✅ Contributor-rich | ✅ Fast-paced, policy-vocal |
| **Release Cadence** | Frequent (weekly) | Frequent (daily alpha) | Moderate | Moderate | Slow | Moderate | Slow | High (3x daily in burst) |

**Strategic positioning insights:**
- **OpenAI Codex** is doubling down on **enterprise security** (approval routing, Guardian sandbox) while sacrificing UX polish on desktop.
- **Claude Code** is **broadest but buggiest**—its plugin ecosystem and feature surface attract the largest community, but SSE stalls and session JSONL regressions erode trust.
- **Qwen Code** is the most **architecturally ambitious**, building daemon mode and worktree features that could leapfrog competitors in CI/CD and IDE integration.
- **Pi** occupies a **provider-agnostic niche**, but `reasoning_content` bugs with Kimi, Anthropic, and MiMo reveal thin provider abstraction.
- **Kimi Code CLI** is **losing ground**—critical model overload unresolved, minimal PR activity, and no releases in 24h suggest resource constraints or strategic pivot.

---

## 5. Community Momentum & Maturity

### High-Maturity Tools (Stable, large user base, systematic bug tracking)
- **Claude Code**: Largest issue tracker breadth, explicit priority tags, active maintainer responses. However, "assertNever" crashes and skills progressive-disclosure issues have been open for months, indicating **maturity with maintenance debt**.
- **OpenCode**: Memory megathread (#20695, 77 comments, 54👍) shows mature triage process. Agent marketplace proposal (#7467) indicates community self-organizing around extensions.
- **Gemini CLI**: P1/P2 priority system, behavioral eval pipeline (#24353), and retesting workflow for bugs (#21409) reflect disciplined engineering culture.

### High-Velocity Tools (Rapid iteration, but regressions common)
- **Qwen Code**: 3 releases in 24h with daemon mode PRs landing concurrently. OOM diagnostics (#4180) and `tool_use` invariant (#4176) show responsiveness. Risk: OAuth policy controversy (#3203) could fragment community.
- **OpenCode**: v1.15.1 released but immediately reported with `InstanceRef not provided` crash. The version jump confusion (#23419) signals communication gaps around release strategy.

### Struggling Tools (Low engagement, unresolved critical bugs)
- **Kimi Code CLI**: K2.6 model overload (#2077) unresolved for 3 weeks with no release. Hook subsystem has 3 related bugs (#2303, #2304, #2307) but only 1 contributor fixing them. **Community confidence is at risk.**
- **Copilot CLI**: Only 2 releases (minor), **zero PRs updated** in 24h. Authentication failure (#716) open long-term. MCP partial loading (#2634) unresolved. The tool appears **maintenance-mode** compared to peers.

### Community Engagement Leaders (by emotional investment)
- **Qwen Code** (#3203, 125 comments on OAuth policy): Users are **politically engaged**, not just bug-reporting.
- **OpenCode** (#20695, 77 comments on memory): Users are **collaborating on diagnostics**, not just asking for fixes.
- **Claude Code** (#36151, 228👍 on multi-account): Users are **voting with massive signal** for a clear, unmet need.

---

## 6. Trend Signals

### 1. MCP Convergence is Accelerating
**Signal:** Copilot CLI adds `/mcp search` (experimental), OpenCode aligns `env` field alias, Pi adds LiteLLM provider, Qwen Code adds daemon adapter plans for MCP consumption.
**Implication:** MCP is becoming the *lingua franca* for tool extensibility. Tools that resist standardization (e.g., Kimi's isolated hook system) risk plugin ecosystem isolation.

### 2. Reasoning Model Support is a Double-Edged Sword
**Signal:** Pi has 4 open bugs (#4251, #4514, #4526, #4505) all related to `reasoning_content` propagation. Claude Code adds adaptive thinking. Qwen Code normalizes cumulative stream deltas.
**Implication:** Reasoning models introduce new failure modes (thinking content leaking, missing fields, 400 errors) that tool developers underestimated. **Provider abstraction layers need hardening** before these become standard.

### 3. Windows Parity Remains an Industry-wide Gap
**Signal:** Every major tool except Pi has open Windows bugs—auth failures, path sensitivity, PowerShell quoting, npm shims, keybinding conflicts. Claude Code's #59362 (drive letter case) is a 2026-level bug that persists.
**Implication:** AI CLI tools are **still built by macOS/Linux-first teams**. Windows users are second-class citizens despite growing adoption among enterprise developers.

### 4. "Observability" is Becoming a First-Class Feature
**Signal:** Codex adds `started_at_ms` to events, OpenCode has memory megathread + diagnostics, Qwen Code ships `/doctor memory`, Gemini CLI adds behavioral eval pipelines, Copilot CLI exposes spend controls.
**Implication:** Developers are demanding **introspection into agent behavior and resource consumption**. Tools that lack diagnostic commands (`/doctor`, usage snapshots, token traces) will lose power users.

### 5. Agent Orchestration is Shifting from "Demo" to "Production"
**Signal:** Gemini CLI's subagent hangs (#21409), Claude Code's Cowork model routing bug (#47488), OpenCode's subagent permission inheritance (#27654), and Qwen's daemon mode all indicate **production-grade multi-agent workflows are immature**.
**Implication:** The "10-agent overnight run" dream is still broken. Reliability, observability, and authorization for multi-agent setups are the next frontier—and currently no tool has solved it.

### 6. Pricing & Access Policies Trigger Stronger Community Reactions
**Signal:** Qwen Code's #3203 (free tier reduction) generated 125 comments in hours. Claude Code's multi-account request (#36151) is the top-voted feature. Users are increasingly **vocal about cost and access**, not just features.
**Implication:** Developers are sensitive to vendor lock-in and pricing changes. Tools that offer **provider-agnostic options** (Pi, OpenCode with LiteLLM) may win over price-sensitive segments.

### 7. Terminal UI is Under Renewed Pressure
**Signal:** OpenCode (#26198, raw mouse sequences), Pi (#3113, Konsole Shift+Enter), Qwen (#4171, Windows Tab conflict), Claude Code (#59163, TUI corruption), Gemini (#24935, external editor corruption).
**Implication:** As tools add more interactive features (sessions, streams, MCP), terminal compatibility becomes a **regression sink**. Headless/daemon modes (Qwen, Codex) may be the escape valve for power users who want stability over interactivity.

---

## Recommendations for Developers Evaluating AI CLI Tools

| If you prioritize... | Choose | Reason |
|---------------------|--------|--------|
| **Feature breadth + community** | Claude Code | Largest plugin ecosystem and community, but expect streaming bugs |
| **Enterprise security** | OpenAI Codex | Guardian sandbox, approval routing, Rust-based reliability |
| **Multi-agent workflows** | Gemini CLI | Native sub-agent orchestration, though hang bugs persist |
| **MCP ecosystem** | Copilot CLI or OpenCode | Deepest MCP integration and discoverability |
| **Provider flexibility** | Pi | LiteLLM, FirePass, adaptive thinking support; watch for `reasoning_content` bugs |
| **Automation/daemon mode** | Qwen Code | Most ambitious architecture for CI/CD and IDE integration |
| **Minimum friction** | Claude Code or Copilot CLI | Most mature onboarding and documentation |
| **Budget/regional access** | Kimi Code CLI (risky) or Pi + LiteLLM | Low-cost model access, but Kimi community is stagnant |

**Bottom line:** No single tool dominates across all dimensions. The ecosystem is converging on MCP, observability, and reasoning-model support, but **Windows parity and multi-agent reliability remain industry-wide weaknesses**. For production use, prioritize tools with active maintenance (OpenCode, Qwen, Claude Code) and explicit migration paths for sessions and tool configurations.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-05-16 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following PRs have attracted the most community discussion and represent the most-watched skill developments:

### #1: Document Typography Skill (#514)
- **Functionality**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents — solving systemic typographic quality issues
- **Discussion Highlights**: Broad community recognition that typographic problems affect virtually all Claude-generated documents; high practical value for professional output
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/514)

### #2: PDF Case-Sensitivity Fix (#538)
- **Functionality**: Corrects 8 file reference mismatches in `skills/pdf/SKILL.md` (`REFERENCE.md` → `reference.md`, `FORMS.md` → `forms.md`)
- **Discussion Highlights**: While a bugfix rather than a new skill, this PR signals the community's keen attention to cross-platform compatibility (case-sensitive filesystems)
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/538)

### #3: ODT / OpenDocument Skill (#486)
- **Functionality**: Create, fill, read, and convert OpenDocument Format files (.odt, .ods) — LibreOffice/ISO-standard document handling
- **Discussion Highlights**: Addresses the demand for open-source document formats beyond Microsoft Office, with template filling and ODT-to-HTML parsing
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/486)

### #4: Frontend-Design Skill Clarity (#210)
- **Functionality**: Revises the frontend-design skill for actionable, conversation-followable instructions with specific behavioral guidance
- **Discussion Highlights**: Deep discussion around what makes a skill *actually usable* by Claude — moving from educational tone to operational precision
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/210)

### #5: Skill Quality & Security Analyzers (#83)
- **Functionality**: Two meta-skills — `skill-quality-analyzer` (evaluates across Structure, Documentation, Examples, Resources, Clarity, UX, Robustness, Coverage) and `skill-security-analyzer` (security posture assessment)
- **Discussion Highlights**: Pioneering "skills about skills" — meta-quality tooling that could become standard for the ecosystem
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/83)

### #6: DOCX Tracked Change Fix (#541)
- **Functionality**: Prevents document corruption when `w:id` values collide between tracked changes and existing bookmarks in OOXML
- **Discussion Highlights**: Demonstrates deep OOXML technical knowledge; important for enterprise document workflows
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/541)

### #7: Skill-Creator YAML Validation (#539)
- **Functionality**: Adds pre-parse validation to detect unquoted `description` fields containing `:` — preventing silent YAML parsing failures
- **Discussion Highlights**: Addresses a common pain point for skill authors; part of the broader push for tooling robustness
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/539)

### #8: Testing Patterns Skill (#723)
- **Functionality**: Comprehensive testing stack coverage — Testing Trophy model, AAA pattern, React component testing, E2E, visual testing
- **Discussion Highlights**: Strong interest in testing standardization; the Testing Trophy model (over Test Pyramid) signals modern testing philosophy alignment
- **Status**: OPEN | [View PR](https://github.com/anthropics/skills/pull/723)

---

## 2. Community Demand Trends

From Issues activity, the community's most-anticipated skill directions cluster around five themes:

**🔐 Enterprise & Org-Wide Collaboration** — *Highest urgency*
- **Issue #228** (13 comments, 7 👍): "Enable org-wide skill sharing in Claude.ai" — users want shared skill libraries and direct sharing links instead of manual `.skill` file distribution via Slack
- Root demand: Enterprise teams need centralized skill management, not file-based sharing

**🧪 Evaluation & Testing Infrastructure**
- **Issue #556** (8 comments, 6 👍): `run_eval.py` fails to trigger skills via `claude -p` (0% trigger rate) — the community is actively trying to build skill evaluation pipelines and hitting fundamental tooling gaps
- **Issue #202** (8 comments): `skill-creator` needs rewriting for operational rather than educational tone

**🛡️ Trust & Security Boundaries**
- **Issue #492** (6 comments, 2 👍): Community skills distributed under `anthropic/` namespace create trust boundary vulnerabilities — users may grant elevated permissions thinking skills are official
- **Issue #412** (4 comments): Proposal for an `agent-governance` skill covering safety patterns, policy enforcement, and audit trails

**📦 Plugin & Distribution Concerns**
- **Issue #189** (6 comments, 8 👍): `document-skills` and `example-skills` plugins install identical content, causing duplicate skills in context window
- **Issue #1087** (2 comments): Plugin loads all skills from repo instead of only declared ones in `marketplace.json`

**🔄 MCP & Cross-Platform Integration**
- **Issue #16** (4 comments): Request to expose Skills as MCPs for standardized API signaling
- **Issue #1102** (2 comments): MCP returns excess data — context congestion from unoptimized data transmission

---

## 3. High-Potential Pending Skills

These active-comment PRs are not yet merged but show strong community interest and may land soon:

| Skill | PR | Status | Last Updated | Why It Matters |
|-------|-----|--------|--------------|----------------|
| SAP-RPT-1-OSS Predictor | [#181](https://github.com/anthropics/skills/pull/181) | OPEN | 2026-03-16 | Enterprise ML on SAP data using open-source tabular foundation model |
| ServiceNow Platform | [#568](https://github.com/anthropics/skills/pull/568) | OPEN | 2026-04-23 | Broad ITSM/ITOM/SecOps coverage — enterprise IT giant |
| AppDeploy (Web App Deployment) | [#360](https://github.com/anthropics/skills/pull/360) | OPEN | 2026-05-04 | Full-stack deployment from Claude — bridges gap between code generation and hosting |
| AURELION Skill Suite | [#444](https://github.com/anthropics/skills/pull/444) | OPEN | 2026-05-06 | Structured cognitive framework + persistent memory — 4 skills in one PR |
| Masonry AI (Image/Video) | [#335](https://github.com/anthropics/skills/pull/335) | OPEN | 2026-03-14 | AI image/video generation via Imagen 3.0 and Veo 3.1 |
| Shodh-Memory (Persistent Context) | [#154](https://github.com/anthropics/skills/pull/154) | OPEN | 2026-03-03 | Cross-conversation memory for AI agents |
| Sensory (macOS Automation) | [#806](https://github.com/anthropics/skills/pull/806) | OPEN | 2026-04-02 | Native AppleScript automation — alternative to screenshot-based computer use |
| Codebase Inventory Audit | [#147](https://github.com/anthropics/skills/pull/147) | OPEN | 2026-02-04 | 10-step orphan code/documentation bloat detection |
| FAF-Context (Project Understanding) | [#281](https://github.com/anthropics/skills/pull/281) | OPEN | 2026-03-18 | AI-instant project context via `.faf` files — sits between `package.json` and `README` |
| Contributing Guide | [#509](https://github.com/anthropics/skills/pull/509) | OPEN | 2026-03-19 | Community health gap — repo currently scores 25% on GitHub health metrics |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for enterprise-grade document processing (ODT/PDF/DOCX typography), evaluative quality tooling (testing patterns, skill analyzers), and organizational sharing infrastructure — reflecting a shift from individual skill experimentation toward production-ready, team-scale Claude Code deployment.**

---

# Claude Code Community Digest — 2026-05-16

## Today's Highlights
Anthropic shipped **v2.1.143** with plugin dependency enforcement, a significant quality-of-life improvement that prevents accidental plugin disabling and handles transitive dependency chains automatically. Meanwhile, the community is rallying around a high-severity `[BUG] Unhandled Case [object Object]` (#59033) with 85 upvotes, exposing an `assertNever`-style crash path in the VSCode extension's streaming event handler. The long-standing skills progressive-disclosure issue (#14882) continues to attract attention, with 14 upvotes and growing frustration over token waste at startup.

## Releases
**v2.1.143** — Plugin dependency management overhauled: `claude plugin disable` now refuses when another enabled plugin depends on the target, providing a copy-pasteable disable-chain hint; `claude plugin enable` force-enables transitive dependencies. A "projected context cost" indicator (per-turn and per-session) was also added to help developers understand token consumption before execution. Full release notes available at: https://github.com/anthropics/claude-code/releases

## Hot Issues

1. **#59033 — [BUG] Unhandled Case [object Object]** (67 comments, 85 👍)
   Closed as duplicate. The root cause is a TypeScript `assertNever` exhaustive-check in the VSCode extension that throws when the server emits an unknown streaming-event type. Users hit this frequently during rapid deploys. Related issue #58897 provides deeper analysis. https://github.com/anthropics/claude-code/issues/59033

2. **#36151 — [FEATURE] Multi-account switching in Claude Mobile app** (59 comments, 228 👍)
   The most upvoted open issue. Developers managing multiple Anthropic accounts (personal/work) want a non-shared-email switching mechanism. Growing demand suggests this is a top priority feature for mobile users. https://github.com/anthropics/claude-code/issues/36151

3. **#14882 — Skills consume full token count at startup instead of progressive disclosure** (17 comments, 14 👍)
   Despite documentation promising progressive disclosure, skills files are fully loaded at session start, wasting context window. The community wants metadata-only (name+description) loading with deferred content. No resolution timeline from Anthropic. https://github.com/anthropics/claude-code/issues/14882

4. **#30435 — [FEATURE] Allow suppressing bash safety heuristic prompts via settings** (17 comments, 39 👍)
   Claude's aggressive `Bash` tool safety checks interrupt workflows. The feature request asks for a `permissions` setting to suppress repetitive "safety heuristic" confirmations without fully switching to auto-approve. https://github.com/anthropics/claude-code/issues/30435

5. **#58897 — VSCode extension: Unhandled case from assertNever on unknown streaming-event types** (16 comments, 12 👍)
   Technical deep-dive into the `webview/index.js` error. The `QB1` helper throws `Error("Unhandled case: ${J}")` when server-side event types aren't recognized by the client-side switch. Community fix discussion centers on adding a graceful fallback for unknown event types. https://github.com/anthropics/claude-code/issues/58897

6. **#29315 — [FEATURE] Support `url` field in `launch.json` for preview feature** (13 comments, 38 👍)
   Developers running dev servers on non-standard ports cannot use Claude's preview feature because it lacks a configurable URL. The feature would allow pointing the preview browser at any running server. https://github.com/anthropics/claude-code/issues/29315

7. **#50780 — [BUG] Desktop app cannot rewind the first message** (8 comments, 6 👍)
   A basic UX gap: users cannot edit the very first message in a conversation thread using the desktop app's rewind feature, breaking the ability to correct initial prompts. https://github.com/anthropics/claude-code/issues/50780

8. **#54434 — [Bug] SSE stream stalls in long-running sessions without message_stop event** (7 comments)
   Critical for power users. Server-sent events stop mid-response, leaving the session hung. Affects automated workflows and long coding sessions. https://github.com/anthropics/claude-code/issues/54434

9. **#47488 — [BUG] Cowork: Agent tool `model` parameter silently ignored — all sub-agents routed to Haiku** (6 comments)
   A serious regression where selecting a specific model for sub-agents is ignored; all Cowork sub-agents end up on the cheapest (Haiku) tier regardless of user preference. https://github.com/anthropics/claude-code/issues/47488

10. **#58463 — [Regression bug] AskUserQuestion tool_use event not written to session.jsonl until user responds** (4 comments, 4 👍)
    Breaks session replay and debugging. Previously, the `AskUserQuestion` event was logged immediately; now it's deferred until the user responds, making transcript analysis unreliable. Verified working in v2.1.119. https://github.com/anthropics/claude-code/issues/58463

## Key PR Progress

Only **2 pull requests** were updated in the last 24 hours:

1. **#59508 — fix(examples/hooks): bash_command_validator regex false negatives** (OPEN)
   Fixes two regex bugs: the `grep` exemption incorrectly exempted `grep` when leading a pipeline, and the `find` regex missed `find` with `-name` flags. Important for teams relying on the hook example for security guardrails. https://github.com/anthropics/claude-code/pull/59508

2. **#59495 — docs: fix GitHub capitalization in README** (CLOSED)
   Trivial but necessary: corrected "Github" to "GitHub" in the project's README per brand guidelines. Demonstrates ongoing attention to documentation polish. https://github.com/anthropics/claude-code/pull/59495

## Feature Request Trends

The most commonly requested feature directions across all open issues:

- **Multi-account & workspace management** (#36151, 228 👍): Seamless switching between personal and enterprise accounts, especially on mobile and desktop.
- **Bash safety prompt suppression** (#30435, 39 👍): Developers want granular control over repetitive safety heuristics without full auto-approve mode.
- **Preview/launch URL configuration** (#29315, 38 👍): Allow arbitrary server URLs for the preview feature, enabling dev servers on custom ports.
- **Local-only session bridging** (#59565): Expose the remote-control endpoint locally, eliminating cloud hops for machine-local automation.
- **MCP streamable-HTTP auto-reconnect** (#59442): When MCP server sessions expire, the client should automatically re-establish connections rather than failing all tool calls.
- **Multi-agent coordination improvements** (#54393): A comprehensive post-mortem cataloging 12 coordination bugs in autonomous overnight runs — the community is actively demanding better agent orchestration.

## Developer Pain Points

Several recurring frustration themes emerged from the issue tracker:

- **Streaming instability** (#54434, #57492, #46745): SSE streams stalling mid-response without `message_stop` events is the most frequently reported networking problem, affecting long-running sessions across all platforms.
- **Windows-specific regressions** (#59362, #54130, #58463): Case-sensitive path tracking (drive letter `C:` vs `c:`), zombie subprocesses corrupting session files, and logging regression in session JSONL files disproportionately impact Windows users.
- **TUI/corruption bugs** (#59163, #59546, #59633): Character encoding corruption after long sessions in VSCode integrated terminals and unresponsive transcript views are causing friction for heavy terminal users.
- **Sandbox/worktree isolation gaps** (#59628, #59455): Worktree sessions can edit parent checkout files with no guardrails, defeating the purpose of workspace isolation.
- **Background task lifecycle** (#55893): Polling loops in background bash tasks get stuck across sessions, and `TaskStop` cannot reference prior-session task IDs — a blocking issue for automation workflows.
- **Agent thinking loss** (#59627, #47488): Agent-cowork model routing to wrong tiers and thinking output lost when hitting limits suggest the agent subsystem still has reliability gaps.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-05-16

## Today's Highlights
Two Rust alpha releases (0.131.0-alpha.21 and .22) rolled out in the last 24 hours, while a wave of Windows desktop app bugs dominated the issue tracker. Community frustration is high around session recovery failures after app updates, and a major refactor to centralize approval routing landed in PRs alongside new spending-control visibility.

## Releases
- [**rust-v0.131.0-alpha.22**](https://github.com/openai/codex/releases/tag/rust-v0.131.0-alpha.22)  
- [**rust-v0.131.0-alpha.21**](https://github.com/openai/codex/releases/tag/rust-v0.131.0-alpha.21)

Both are incremental pre-release builds; no detailed changelog was published. They likely include the latest round of permission-profile and sandbox improvements from the day’s merged PRs.

## Hot Issues (top 10 by comment count)

1. **[#22956 – Long conversations cannot be opened after Windows app update](https://github.com/openai/codex/issues/22956)**  
   *15 comments, 7 👍*  
   Urgent bug: sessions become unloadable post‑update (v26.513.31313). API-key subscribers affected. Community reaction is strong—multiple reports of lost work.

2. **[#4607 – Needs a sticky header describing what the agent is working on](https://github.com/openai/codex/issues/4607)**  
   *5 comments, 8 👍 (CLOSED)*  
   Terminal‑tabs user loses track of which agent is active. Request for a persistent summary header. Highly upvoted, signals a common multi‑session pain point.

3. **[#19869 – Show remaining usage limit in Codex app chat](https://github.com/openai/codex/issues/19869)**  
   *4 comments (OPEN)*  
   Users want a visible quota indicator like the old UI had. Without it, hitting limits during work is disruptive.

4. **[#17997 – Support external approval reviewers via `approvals_reviewer = "command"`](https://github.com/openai/codex/issues/17997)**  
   *4 comments (CLOSED)*  
   Extends approval routing to allow local policy scripts (e.g., `gitleaks`) to gate execution. Shows demand for custom security hooks.

5. **[#22971 – Windows chat history bug after updating](https://github.com/openai/codex/issues/22971)**  
   *3 comments, 3 👍 (OPEN)*  
   Second Windows bug: all local session histories fail to resume after desktop update (v26.513.3673). Complements #22956.

6. **[#14693 – Configurable no‑interrupt mode for CLI/TUI](https://github.com/openai/codex/issues/14693)**  
   *3 comments, 1 👍 (CLOSED)*  
   Accidental keystrokes can steer an active run. Users want a lock‑in mode to prevent interruption during long operations.

7. **[#17539 – Include per‑API‑call token usage in `turn.completed` JSONL events](https://github.com/openai/codex/issues/17539)**  
   *3 comments (CLOSED)*  
   `codex exec --json` only reports cumulative totals, making it impossible to track context‑window headroom per call. Important for heavy CLI users.

8. **[#14463 – Plan mode review / edit feature](https://github.com/openai/codex/issues/14463)**  
   *3 comments, 2 👍 (CLOSED)*  
   Users want to fix plan typos directly instead of re‑prompting. Suggests UI improvements for the “Plan mode” workflow.

9. **[#17660 – Make host‑faithful local execution a first‑class workflow](https://github.com/openai/codex/issues/17660)**  
   *3 comments (CLOSED)*  
   Combining `danger‑full‑access` + `on‑request` approval already works, but users want an official, documented workflow to avoid accidental global writes.

10. **[#20563 – Heavy I/O activity from idle `codex` processes](https://github.com/openai/codex/issues/20563)**  
    *2 comments (OPEN)*  
    Idle CLI process (0.128.0) causes high disk I/O on Linux aarch64. Performance concern for background sessions.

## Key PR Progress (10 important PRs)

1. **[#22448 – Add installed‑plugin mention API](https://github.com/openai/codex/pull/22448)**  
   *Open* – Enables `@`‑based plugin discovery by only loading installed plugins, not the full catalog. Reduces latency for mention completions.

2. **[#22972 – Expose spend controls in usage status](https://github.com/openai/codex/pull/22972)**  
   *Open* – Extends the usage snapshot with spend‑control detail so the TUI can display active limits and reset countdowns. Directly addresses requests like #19869.

3. **[#22780 – Remove personality feature switch](https://github.com/openai/codex/pull/22780)**  
   *Open* – Personality is now always‑on; users can opt out via `personality = none`. Simplifies config and eliminates disabled‑personality edge cases.

4. **[#22967 – Fix Windows doctor npm root probe](https://github.com/openai/codex/pull/22967)**  
   *Open* – Fixes `codex doctor` on Windows where `npm.cmd` is the shim (fixes #22964). Critical for npm‑based installs on Windows.

5. **[#20737 – Centralize approval routing](https://github.com/openai/codex/pull/20737)**  
   *CLOSED* – A major refactor introducing a canonical `ApprovalRequest` / `ApprovalOutcome` model. Unifies approval logic across user, guardian, and future external reviewers (supports #17997).

6. **[#17036 – Allow limited git writes in workspace sandbox](https://github.com/openai/codex/pull/17036)**  
   *CLOSED* – Adds `allow_limited_git_writes` config for workspace‑write sandboxes. Lets Git commands update repo metadata without exposing hooks.

7. **[#17286 – Prefix Compaction](https://github.com/openai/codex/pull/17286)**  
   *CLOSED* – Background pre‑warm of prefix compaction; foreground auto‑compaction as fallback. Reduces context window bloat and improves session responsiveness.

8. **[#20653 – Report running command durations](https://github.com/openai/codex/pull/20653)**  
   *CLOSED* – Adds `started_at_ms` to `ExecCommandBeginEvent` and derives elapsed durations in `ThreadHistoryBuilder`. Enables better progress tracking in the TUI.

9. **[#19467 – Route MCP elicitations through Guardian review](https://github.com/openai/codex/pull/19467)**  
   *CLOSED* – Ensures approval‑shaped MCP requests (e.g. Browser Use) go through Guardian/auto‑review before becoming user prompts. Strengthens sandbox security.

10. **[#19176 – Add conditional network proxy prompt guidance](https://github.com/openai/codex/pull/19176)**  
    *CLOSED* – Provides the model with context about active network proxies to avoid misrouting or misinterpreting policy denials. Improves reliability behind enterprise proxies.

## Feature Request Trends

- **Sticky agent context in terminal** – Users running multiple tabs want a persistent header showing which agent is active and what it’s working on (see #4607, #14693).  
- **Visible usage/quota indicators** – Demand for real‑time spend‑control UI in both the app and CLI, including reset countdowns (#19869, #17457).  
- **Customizable approval pipelines** – Extensions to support external review commands, local policy scripts, and host‑faithful workflows (#17997, #17660).  
- **Editability of AI‑generated plans** – Users want to correct typos or adjust plans inline without re‑prompting (#14463).  
- **Session & history scoping** – Requests to scope prompt recall to the current thread (#16227) and to auto‑copy resume commands on exit (#17771).

## Developer Pain Points

- **Windows app update breaks sessions** – Two critical bugs (#22956, #22971) report that after updating the desktop app, all existing conversations become unopenable or lose history. This is the loudest issue today.  
- **No clear usage limits feedback** – Users run into rate limits without warning because the remaining quota indicator was removed from the chat UI (#19869).  
- **Accidental interruption in CLI** – Typing during an active run can steer the agent in unexpected ways; lack of a “no‑interrupt” mode causes frustration (#14693).  
- **Per‑call token visibility missing** – `codex exec --json` only shows cumulative token usage, making it hard to monitor context‑window utilization per API call (#17539).  
- **High idle I/O** – Idle `codex` processes consume disk I/O on Linux, affecting performance in CI/long‑running sessions (#20563).  

*Generated from GitHub data for `openai/codex` as of 2026-05-16.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-16

## Today's Highlights

No new releases were cut in the past 24 hours, but the community is actively tracking a set of long-running issues and PRs. The main agent hang bug (#21409) continues to draw attention with seven reactions, and several PRs landed to improve OAuth handling, fallback model selection, and terminal compatibility. The “AST-aware file reads” EPIC (#22745) saw fresh comments, indicating sustained interest in smarter code understanding.

## Releases

No releases in the last 24h.

## Hot Issues (Top 10)

1. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *Priority P1 – 7 comments, 7 👍*  
   The generalist agent hangs indefinitely when deferring to sub-agents. Users report that instructing the model not to use sub-agents works around the issue. The bug is marked for retesting.

2. **[#22323 — Subagent recovery after MAX_TURNS misreported as success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *Priority P1 – 6 comments, 2 👍*  
   The `codebase_investigator` subagent returns `status: "success"` even though it hit the turn limit before performing any analysis. This hides real interruptions and misleads the orchestrator.

3. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *Priority P2 – 6 comments*  
   Anecdotal reports that the agent rarely invokes custom skills or sub-agents autonomously, even when the skill description clearly matches the task.

4. **[#25166 — Shell command execution gets stuck on “Waiting input”](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *Priority P1 – 3 comments, 3 👍*  
   After a simple CLI command finishes, the shell state remains active with `Awaiting user input`. This happens for commands that do not prompt for input. High community frustration.

5. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   *Priority P1 – 4 comments, 1 👍*  
   The browser agent terminates early or crashes under Wayland display servers. The termination reason is often reported as “GOAL” despite no real work being done.

6. **[#22745 — Assess the impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *Priority P2 – 7 comments*  
   An EPIC tracking whether AST-aware tools can reduce token noise and improve codebase understanding. Suggests using tools like `tilth` or `glyph` for method-bound reads and smarter searches.

7. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *Priority P1 – 6 comments*  
   Follow-up on behavioral evals: the team has created 76 tests across 6 models, but needs a more reliable component-level evaluation pipeline.

8. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *Priority P2 – 2 comments*  
   Current memory extraction sends transcripts to the model before secrets are redacted. This issue calls for pre-context redaction and fewer logs from Auto Memory.

9. **[#26523 — Surface or quarantine invalid Auto Memory inbox patches](https://github.com/google-gemini/gemini-cli/issues/26523)**  
   *Priority P2 – 2 comments*  
   Invalid memory patches (malformed, no hunks, escaped paths) are silently skipped, but the background extractor still reads every `.patch` file, wasting cycles. Users want invalid patches to be surfaced or quarantined.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
    *Priority P2 – 2 comments, 1 👍*  
    The model occasionally uses `git reset --force` or other destructive commands when safer alternatives exist. Community suggests adding a safety layer for risky operations.

## Key PR Progress (Top 10)

1. **[#27139 — fix(core): validate MCP OAuth resources from metadata URL](https://github.com/google-gemini/gemini-cli/pull/27139)**  
   Fixes #20017 by deriving the expected protected resource from the metadata URL returned by the OAuth endpoint, improving RFC 9728 compliance.

2. **[#26932 — fix(cli): handle refreshAuth rejection in non-interactive prompt path](https://github.com/google-gemini/gemini-cli/pull/26932)**  
   Prevents unhandled promise rejection crashes during OAuth token refresh in non-interactive mode. Wraps the second `refreshAuth` call in a try-catch.

3. **[#26914 — fix(core): include gemini-2.5-flash-lite in default fallback chain](https://github.com/google-gemini/gemini-cli/pull/26914)**  
   Adds `gemini-2.5-flash-lite` as a fallback when Pro/Flash quotas are exhausted. Free-tier users no longer have to manually specify the model.

4. **[#27137 — fix(cli): make --skip-trust actually load workspace settings](https://github.com/google-gemini/gemini-cli/pull/27137)**  
   The `--skip-trust` flag was documented to trust the workspace but did not load `.gemini/settings.json`. This PR fixes the behavior, so hooks and extensions are properly honored.

5. **[#25900 — fix(core): prefer pwsh.exe over Windows PowerShell 5.1](https://github.com/google-gemini/gemini-cli/pull/25900)**  
   Resolves issues with double quotes being stripped by Windows PowerShell 5.1. Now prefers PowerShell Core (`pwsh.exe`) when available.

6. **[#26358 — feat(cli): exit shell mode with backspace on empty input](https://github.com/google-gemini/gemini-cli/pull/26358)**  
   Adds a backspace-to-exit shortcut in shell mode, matching the intuitive “erase the `!`” behavior. Already closed (merged).

7. **[#26317 — fix: bypass powershell command substitution check for setup-github](https://github.com/google-gemini/gemini-cli/pull/26317)**  
   Removes the subshell wrapper `(...)` from generated `setup-github` commands to avoid false-positive command substitution detection in PowerShell.

8. **[#26345 — feat: add secure non-interactive multi-agent orchestration](https://github.com/google-gemini/gemini-cli/pull/26345)**  
   Proposes a conservative sequential multi-agent execution path for non-interactive use, preserving all existing security controls (policy engine, sandbox, auth).

9. **[#26710 — fix(tests): update model name in plan mode test to auto-gemini-3](https://github.com/google-gemini/gemini-cli/pull/26710)**  
   Fixes a failing integration test after `gemini-2.5-flash` was removed from the API v1beta. Updates test to use the new auto-alias.

10. **[#26692 — feat(cli): support GEMINI_CLI_ENABLE_AUTO_UPDATE env var](https://github.com/google-gemini/gemini-cli/pull/26692)**  
    Adds an environment variable to control auto-update, useful for ephemeral environments or CI without needing a `.gemini/settings.json` file.

## Feature Request Trends

- **AST-aware code understanding** – Multiple issues (#22745, #22746, #22747) explore using AST tools for file reads, search, and codebase mapping to reduce token waste and improve accuracy.
- **Better sub-agent orchestration** – Users want sub-agents to be backgroundable (Ctrl+B, #22741), automatically invoked when relevant (#21968), and used for build/lint tasks (#22602). A dedicated subagent eval strategy is also requested (#22601).
- **Self-awareness & proactive skills** – The agent should know its own CLI flags, hotkeys, and capabilities (#21432). It should also periodically reflect on the session and suggest creating or updating skills (#21421).
- **Discouraging destructive actions** – A safety net to prevent `git reset --force`, dangerous DB commands, or other destructive operations when safe alternatives exist (#22672).

## Developer Pain Points

- **Agent hangs & stuck states** – Generalist agent hangs (#21409), shell commands stuck after completion (#25166), and subagent recovery misreporting (#22323) are the top recurring issues.
- **Sub-agent reliability** – Browser agent fails on Wayland (#21983), subagents run without permission (#22093), and config overrides are ignored (#22267).
- **Memory system bugs** – Auto Memory retries low-signal sessions indefinitely (#26522), invalid patches are silently skipped (#26523), and sensitive data leaks via transcripts (#26525).
- **Terminal/rendering issues** – Corruption after exiting external editors (#24935), flicker on resize (#21924), and forced full-screen refresh problems indicate ongoing TUI pain.
- **Inconsistent environment support** – Alpine Linux shell compatibility (#26689, #26770), Windows PowerShell quoting bugs (#25900), and Wayland display issues (#21983) highlight gaps in cross-platform robustness.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-16

## Today’s Highlights
Two incremental releases shipped today, the most notable being **v1.0.49-0** which introduces experimental MCP search and tool discovery, plus a new “None” reasoning effort option. Community activity focused on authentication hurdles on Windows, the silent exit bug in non‑interactive mode, and the ongoing debate around automatic co‑author tags on commits. Several fresh issues surfaced around MCP tooling, terminal UI regressions, and content‑filtering false positives.

## Releases
- **v1.0.49-1** — *Improved*: prompt mode (`-p`) now automatically loads workspace MCP sources when the current folder is already trusted.
- **v1.0.49-0** — *Added*:
  - Experimental `/mcp search` command to discover and install MCP servers from a registry.
  - Experimental tool search with deferred loading for MCP and external tools.
  - “None” reasoning effort option to disable model reasoning entirely.
  - New `COPILOT_PLUGIN_DIR_ONLY` environment variable.

No new pull requests were updated in the last 24 hours.

## Hot Issues
1. **[#3181 – Remove automatic co‑author to Copilot CLI commits or provide opt‑out](https://github.com/github/copilot-cli/issues/3181)** (CLOSED)  
   Users strongly opposed personifying AI by adding `Co-authored-by: Copilot` to every commit. The issue was closed, but the topic remains divisive.

2. **[#3189 – Non‑interactive mode exits silently with code 1 on macOS](https://github.com/github/copilot-cli/issues/3189)** (CLOSED)  
   `copilot -p` produced zero output, no logs, and exit code 1. Interactive mode worked fine. Closure suggests a fix is already in an upcoming release.

3. **[#716 – Windows auth fails with `getaddrinfo ENOTFOUND`](https://github.com/github/copilot-cli/issues/716)** (OPEN, 👍 5)  
   Long‑standing authentication crash on Windows when resolving `next-waitlist.azurewebsites.net`. Affects many users and has no workaround mentioned.

4. **[#1082 – CLI hangs on sudo commands without password prompt](https://github.com/github/copilot-cli/issues/1082)** (OPEN, 👍 11)  
   Running commands that require `sudo` (e.g. package installs) causes infinite hang. Requests for elevating privileges are never surfaced to the user.

5. **[#2634 – MCP tools loaded partially / incorrectly](https://github.com/github/copilot-cli/issues/2634)** (OPEN)  
   Stdio MCP servers expose tools with different schemas than defined – tools appear incorrect to the agent, leading to incorrect usage.

6. **[#3340 – Input box too tall in latest update](https://github.com/github/copilot-cli/issues/3340)** (OPEN)  
   After an update the input prompt occupies significantly more vertical space, reducing useful terminal area. Community reports it as a regression.

7. **[#3135 – BYOK statusline shows “medium” effort despite `--effort high`](https://github.com/github/copilot-cli/issues/3135)** (OPEN)  
   Custom provider (BYOK) users see `model.display_name` incorrectly appended with `(medium)` even when `reasoning_effort: "high"` is sent. Works in older versions.

8. **[#3318 – Copilot suddenly refusing valid requests](https://github.com/github/copilot-cli/issues/3318)** (OPEN, 👍 2)  
   Clean contexts with standard prompts (bug fixes, tests, directory queries) are being rejected. Pattern suggests content‑filtering false positives.

9. **[#3262 – Crash on update triggers VS JIT Debugger](https://github.com/github/copilot-cli/issues/3262)** (CLOSED)  
   After running `/update`, `copilot.exe` crashed with an unhandled exception in `koffi.node`, opening Visual Studio JIT debugger. Windows‑specific.

10. **[#3331 – Feature request: auto‑update plugins on CLI startup](https://github.com/github/copilot-cli/issues/3331)** (OPEN, 👍 2)  
    Currently plugins must be updated manually. Users want a marketplace flag to keep installed plugins automatically synced to latest.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
- **MCP ecosystem expansion** – Experimental `/mcp search` and deferred tool loading signal a push toward a discoverable plugin registry. Users want auto‑update of plugins and machine‑level slash commands.
- **Co‑author control** – Despite #3181 being closed, calls for an opt‑out toggle remain. A related issue (#3177) asks for *adding* co‑author tags for AI‑generated commits – highlighting a split in community preferences.
- **Terminal UX polish** – Requests include distinguishing agent states in the title bar (#3327), respecting `\r` for progress bars (#3191), and fixing markdown link rendering in tables (#3204).
- **Reasoning effort granularity** – The new “None” effort option is welcomed, but BYOK users still see incorrect statusline labels and need reliable reasoning‑effort mapping for custom/unknown models.

## Developer Pain Points
- **Authentication failures on Windows** (#716) remain a persistent blocker with no clear resolution timeline.
- **Silent exits and hangs** (#3189, #1082) erode trust – users get no error message, no log, and no password prompt.
- **Content‑filtering false positives** (#3318, #3348) block valid technical queries without explanation, a growing frustration.
- **MCP tool loading inconsistencies** (#2634, #2135) cause silent misbehavior – the agent sees different schemas than defined, leading to wrong tool calls.
- **UI regressions** (#3340) after each release degrade the terminal experience, forcing users into workarounds.

---

*Digest generated from [github/github-copilot-cli](https://github.com/github/copilot-cli) activity on 2026-05-16.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区文摘 — 2026-05-16

## Today's Highlights

昨日社区焦点集中在两件事：一是 **K2.6 模型在正常负载下持续重试、几乎不可用**（Issue #2077），该问题已持续三周，用户强烈不满；二是 **Hook 子系统迎来三连 PR（#2305、#2307、#2308）**，来自同一贡献者 AkaCoder404 正集中修复 `UserPromptSubmit` 空载荷问题、并增强 `Stop` 钩子 payload。此外，社区对 `/goal` 命令与 Codex 集成的呼声仍在发酵（#2252）。

## Releases

过去 24 小时内无新版本发布。当前最新版本为 **v1.44.0**（如 Issue #2310 所报告）。

## Hot Issues

以下列出全部 7 个过去 24h 内有更新的 Issue。由于总量不足 10 个，此处全部收录。

1. **#2077 [Critical] K2.6 模型过载 — 正常负载下不可用**  
   报告称 K2.6 模型（Allegretto 订阅）持续重试，几乎无法完成对话。已保持 open 近三周，有 14 条评论，但尚未被解决。用户仅获得 1 个 👍，反映出短期内影响范围可能尚未爆发，但严重性极高。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2077)

2. **#2252 [Enhancement] 希望增加 `/goal` 命令并允许 coding plan 导入到 Codex 中使用**  
   社区强烈要求引入类似 Claude Code 138 版本的 `/goal` 命令，并将 Kimi Code CLI 的 coding plan 功能导出至 Codex 主流平台。9 条讨论，1 个 👍，属于近期最受关注的功能请求。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2252)

3. **#2304 [Bug] UserPromptSubmit Hook stdout 被静默丢弃，无法注入提示词增强**  
   `UserPromptSubmit` hook 的标准输出 stdout 内容被完全忽略，导致用户自定义插件无法生效。1 条评论，尚未解决。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2304)

4. **#2310 [Bug] Shell 工具超时但未终止子进程**  
   运行在 WSL2 Linux 上的 v1.44.0，Shell 工具达到超时后，子进程依然挂起，产生孤立进程。0 条评论，刚提交。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2310)

5. **#2307 [Enhancement] Hook Stop 事件应包含 LLM 响应和停止原因**  
   希望 `Stop` hook 的 payload 从当前仅包含 session_id 等基本信息，扩展包含完整的 LLM 响应文本和停止原因（如 `stop`、`length`）。0 条评论，但已出现配套 PR（#2308）。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2307)

6. **#2306 [Bug] APC 协议回放 — 会话历史不显示**  
   用户在 `kimi acp`（Zed 集成）和 `kimi web` 两种模式下均遇到会话历史丢失问题：重启后标签存在但内容为空，切换会话后内容也空。0 条评论，但报告格式非常详细。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2306)

7. **#2303 [Bug] UserPromptSubmit hook 在 Shell UI 输入时收到空提示**  
   当用户通过 Shell UI（非直接输入）提交 prompt 时，`UserPromptSubmit` hook 接收到空字符串 payload。0 条评论，与 #2304 属同一子系统的不同 bug。  
   [链接](https://github.com/MoonshotAI/kimi-cli/issues/2303)

## Key PR Progress

共 4 个过去 24h 内更新的 PR。同样全部收录。

1. **#2236 fix(utils): 限制广播队列大小与 Web Store 缓存防止内存泄漏**  
   解决 `BroadcastQueue` 中慢速消费者导致队列无限增长（OOM）以及 Web Store 会话缓存全量加载的问题。已获得 maintainer 关注，更新于 5 月 16 日。  
   [链接](https://github.com/MoonshotAI/kimi-cli/pull/2236)

2. **#2231 fix(aiohttp): 复用 TCPConnector 防止连接泄漏**  
   每次调用 `new_client_session()` 都会新建 `TCPConnector`，导致 HTTP 连接无法复用、文件描述符压力增大。此 PR 改为全局复用，降低延迟与资源消耗。同样于 5 月 16 日更新。  
   [链接](https://github.com/MoonshotAI/kimi-cli/pull/2231)

3. **#2305 fix(hook): 修复 UserPromptSubmit payload 捕获输入文本而非空字符串**  
   对应 Issue #2303，使 hook 能够正确获取用户输入内容。作者 AkaCoder404，创建于 5 月 15 日。  
   [链接](https://github.com/MoonshotAI/kimi-cli/pull/2305)

4. **#2308 feat(hook): 在 Stop hook payload 中包含 response 和 stop_reason**  
   对应 Issue #2307，扩展 Stop hook 数据使其可用于日志、统计等高级场景。作者同为 AkaCoder404。  
   [链接](https://github.com/MoonshotAI/kimi-cli/pull/2308)

## Feature Request Trends

从所有 Issue 中提炼出以下关键方向：

- **Coding Plan 与外部平台互通**：用户强烈期望 `/goal` 命令（灵感来自 Claude Code 138）以及将 Kimi Code CLI 的 coding plan 导入 Codex（#2252）。这表明社区不再满足于闭门造车，而是希望 Kimi 的规划能力能融入更主流的编辑器生态。
- **Hook 系统能力增强**：连续多个 Issue 和 PR 聚焦于 Hook 的 payload 完整性（#2304、#2303、#2307），用户需要 `Stop` 事件中的响应内容和停止原因，以及 `UserPromptSubmit` 能真正携带用户输入。这是一个对插件/自动化生态的基础需求。
- **会话持久化与回放**：Issue #2306 提出 APC 协议下会话历史不保存的问题，说明用户在日常迭代中依赖可靠的会话恢复能力。

## Developer Pain Points

过去 24h 暴露的痛点集中在以下两方面：

1. **模型稳定性与性能**：K2.6 模型在正常负载下频繁重试（#2077），严重影响日常使用。虽然该 Issue 已存在数周，但依然未关闭，开发者可能需要警惕模型服务的容量问题。
2. **Hook 子系统一致性**：`UserPromptSubmit` 在不同的输入路径下（Shell UI vs 直接输入）表现不一致（#2303），且 stdout 输出被静默丢弃（#2304）。这种碎片化的行为让依赖 Hook 的开发者非常头疼，幸而已有社区贡献者快速提交修复 PR。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-16

## Today's Highlights

OpenCode **v1.15.1** is out with a handful of targeted bugfixes, but the release is clouded by a new crash (`InstanceRef not provided`) affecting `opencode run --agent`. Meanwhile, the community is rallying around the **Memory Megathread** (#20695) to collect heap snapshots, and a flurry of terminal‑state issues (raw mouse sequences, scroll fights, Dvorak keybinds) is testing the TUI’s resilience. A steady stream of PRs this week hints at stronger provider normalization (NVIDIA NIM, LAN discovery) and a more robust MCP ecosystem.

---

## Releases

### [v1.15.1](https://github.com/anomalyco/opencode/releases) (published today)
- **Improvements:** Clarified recovery path when the npm package is installed without its native binary.
- **Bugfixes:**
  - Duplicate consecutive entries in prompt history are now suppressed.
  - Full config validation errors are shown during TUI startup instead of a generic failure.
  - Fixed npm installs so the native binary is correctly resolved.
- **⚠️ Notable:** Several reports (e.g., #27829, #27833) indicate that `opencode run --agent` crashes with `InstanceRef not provided` in this release – pinning to 1.15.0 is a workaround.

---

## Hot Issues (10 noteworthy)

1. **[#20695 – Memory Megathread](https://github.com/anomalco/opencode/issues/20695)** (OPEN, 77 comments)
   Central tracker for scattered memory reports. Maintainers request heap snapshots, not LLM suggestions. High community traction (54 👍).

2. **[#2224 – Airgapped installation support](https://github.com/anomalco/opencode/issues/2224)** (CLOSED, 24 comments)
   User running OpenCode in Kubernetes without internet access hit a curl‑install failure. 43 👍 indicates strong demand for offline deployment.

3. **[#7467 – GitHub‑based Agent Marketplace](https://github.com/anomalco/opencode/issues/7467)** (OPEN, 15 comments)
   Proposal to share/ discover agents via GitHub without manual file copying. Still open with ongoing discussion.

4. **[#26198 – Terminal flooded with raw mouse escape sequences](https://github.com/anomalco/opencode/issues/26198)** (OPEN, 15 comments, 2 👍)
   Mouse tracking not disabled before returning to shell prompt, causing terminal “stuck” in raw mode. Frustrating for CLI users.

5. **[#23419 – Version jump confusion (1.4.x → 1.14.x)](https://github.com/anomalco/opencode/issues/23419)** (OPEN, 14 comments, 19 👍)
   Users question aggressive update cadence and apparent version skip. Signals a trust/communication gap with the dev cycle.

6. **[#27096 – Dvorak keybinds broken](https://github.com/anomalco/opencode/issues/27096)** (CLOSED, 11 comments)
   Switching keyboard layout exposes scancode vs. keycode mismatch. Emacs‑like binds (ctrl+k, ctrl+y) behave differently. Important for non‑QWERTY users.

7. **[#15728 – Read tool cannot pass image data to vision models](https://github.com/anomalco/opencode/issues/15728)** (OPEN, 9 comments, 6 👍)
   Key limitation for multi‑modal workflows (e.g., Qwen3.5‑plus). Forcing workaround via separate image tools.

8. **[#7659 – Don’t automatically scroll chat window](https://github.com/anomalco/opencode/issues/7659)** (OPEN, 8 comments, 12 👍)
   Repeated frustration: users cannot read previous output while streaming continues. Related to #27792 (closed but same sentiment).

9. **[#25582 – Fork to new session from message timeline](https://github.com/anomalco/opencode/issues/25582)** (OPEN, 7 comments)
   Desktop app feature request to fork a session at any user message – aligns with existing web/CLI behaviour.

10. **[#27758 – Model refused to make a Compaction](https://github.com/anomalco/opencode/issues/27758)** (OPEN, 5 comments)
    “Big Pickle” model returned garbage and a thumbs‑up emoji instead of a summary during auto‑compaction. Highlights brittle agent self‑summarization.

---

## Key PR Progress (10 important)

1. **[#27836 – docs: add LiteLLM plugin to ecosystem](https://github.com/anomalco/opencode/pull/27836)** (OPEN)
   New community plugin `@finger_xie/opencode-plugin-litellm` with `/connect` support and automatic model discovery. Expands provider choice.

2. **[#26167 – fix(session): retry empty stream truncations with attempt cap](https://github.com/anomalco/opencode/pull/26167)** (OPEN)
   Fixes silent failures when upstream provider ends stream without `stop_reason`. Retries with a limit to avoid infinite loops. Closes #26170.

3. **[#27830 – fix(nim): NVIDIA NIM provider hardening](https://github.com/anomalco/opencode/pull/27830)** (OPEN)
   Normalizes OpenAI‑incompatible responses from NVIDIA NIM (e.g., missing fields, non‑standard stop reasons). Closes 6 related issues.

4. **[#27554 – feat: local LAN provider discovery + auto‑discover models](https://github.com/anomalco/opencode/pull/27554)** (OPEN)
   Adds mDNS/broadcast‑based discovery for OpenAI‑compatible local servers. Reduces manual config for self‑hosted models.

5. **[#27820 – serve: add socket listener mode](https://github.com/anomalco/opencode/pull/27820)** (OPEN)
   Enables Unix sockets and Windows named pipes for `opencode serve`. Important for systemd‑managed deployments.

6. **[#27825 – fix(sync): publish events on injected project bus](https://github.com/anomalco/opencode/pull/27825)** (CLOSED)
   Ensures `message.part.updated` events reach `/event` subscribers after DB transaction. Fixes sync‑backed event propagation.

7. **[#27824 – fix: /event bug](https://github.com/anomalco/opencode/pull/27824)** (CLOSED)
   Quick fix for an unstated `/event` endpoint issue. No details but merged fast – likely a regression.

8. **[#26821 – [beta] core: reduce prompts for shell, todowrite, and task tools](https://github.com/anomalco/opencode/pull/26821)** (CLOSED)
   Trimmed lengthy system prompts now that models are smarter. Expect lower token counts and faster responses.

9. **[#26311 – fix(lsp): use which() for node/npm in ESLint LSP](https://github.com/anomalco/opencode/pull/26311)** (CLOSED)
   Replaces hardcoded binary paths with dynamic lookup, fixing environments where `node` is not in the default PATH.

10. **[#26333 – fix(mcp): accept 'env' field as alias for 'environment'](https://github.com/anomalco/opencode/pull/26333)** (CLOSED)
    Aligns MCP config schema with Claude Desktop / Cursor convention. Lowers friction for tool portability.

---

## Feature Request Trends

Distilling the most‑requested directions from recent issues:

- **Agent sharing & discoverability** (#7467) – A GitHub‑based marketplace for agents is the top community ask.
- **Session forking & navigation** (#25582, #27787) – Users want to fork from any message and navigate long sessions with keyboard‑focused modes.
- **Subagent observability** (#27828) – Parent agents need real‑time visibility into background subagent progress.
- **MCP ecosystem alignment** (#27809, #26333) – The community is pushing for compatibility with the broader MCP standard (env field alias, Claude‑style config sections).
- **Plugin API expansion** (#26097, #21096) – TUI plugin hooks for session projection and signed receipts for tool calls.
- **Airgapped / offline support** (#2224) – Strong demand for running OpenCode without internet access.
- **Auto‑relink stale sessions** (#27822) – Clean handling when project directories are renamed.

---

## Developer Pain Points

Recurring frustrations surfaced in today’s data:

- **Terminal state pollution** – Raw mouse escape sequences (#26198) and auto‑scroll (#7659, #27792) disrupt reading and shell usage.
- **Version instability** – Aggressive release cadence (#23419) and regressions like `InstanceRef not provided` in v1.15.1 (#27829, #27833) erode trust.
- **Keyboard layout edge cases** – Dvorak keybind confusion (#27096) and missing `/exit` autocomplete (#26625) harm accessibility.
- **Provider‑specific crashes** – NVIDIA NIM (#27830), Kimi (#25489), and local MCP disconnects (#27414) point to fragile provider logic.
- **Agent self‑summarization failures** – Model refusal during compaction (#27758) and infinite loops after tool calls (#26220) waste time and tokens.
- **Permission inheritance bugs** – Subagent `edit:deny` overrides (#27654) and `pkill` hangs (#25672) complicate multi‑agent workflows.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-05-16

## Today's Highlights
The Pi community continues to grapple with **reasoning `content` injection bugs** across multiple providers (Kimi K2.6, MiMo, Xiaomi), triggering 400 errors when thinking mode is enabled on models that don’t properly preserve `reasoning_content`. Several PRs landed to harden **auto-compaction logic** and fix **terminal rendering issues**, while new provider integrations (LiteLLM, FirePass) expand Pi’s reach. No new releases were published in the last 24 hours.

## Releases
No new releases in the past 24 hours.

---

## Hot Issues
*(10 selected for significance, community engagement, and impact)*

1. **#4251** – [Using kimi k2.6 on OpenCode go results in "reasoning_content is missing in assistant tool call message" error](https://github.com/earendil-works/pi/issues/4251)  
   **Status:** Open (bug, inprogress)  
   **Comments:** 18 | 👍 7  
   A core bug when using Kimi K2.6 with thinking enabled: the API expects `reasoning_content` but the provider omits it after a tool call, causing a 400. Highlights growing pains with reasoning-capable models and tool use.

2. **#3357** – [Official local LLM provider extension](https://github.com/earendil-works/pi/issues/3357)  
   **Status:** Open  
   **Comments:** 13 | 👍 23  
   A long-running feature request to dynamically fetch model lists from `{baseUrl}/models` (for llama.cpp, Ollama, LM Studio). High community demand for a first-class local‑LLM integration.

3. **#4514** – [Kimi K2.6 error 400: Extra inputs are not permitted, field: 'messages[8].reasoning'](https://github.com/earendil-works/pi/issues/4514)  
   **Status:** Closed (bug, refactor)  
   **Comments:** 8 | 👍 7  
   Similar to #4251 – the `reasoning` field leaked into subsequent messages after thinking was used, rejected by the provider. Closed as part of a larger refactor.

4. **#3113** – [Pi doesn't recognize Shift + Enter under Konsole](https://github.com/earendil-works/pi/issues/3113)  
   **Status:** Closed  
   **Comments:** 5  
   Konsole’s magic sequence `\x1bOM` for Shift+Enter is misinterpreted as Enter, breaking multi-line input. A recurring terminal-compatibility pain point.

5. **#3931** – [pi is missing all the latest openrouter models](https://github.com/earendil-works/pi/issues/3931)  
   **Status:** Closed  
   **Comments:** 4  
   Models like `gpt-5.5` aren't listed in Pi’s known models, forcing custom IDs. Points to an out-of-sync model registry that frustrates users of rapidly updated providers.

6. **#4556** – [Crash of pi with very narrow terminal](https://github.com/earendil-works/pi/issues/4556)  
   **Status:** Closed (bug, weekend, refactor)  
   **Comments:** 4  
   A crash when terminal width is < 40 columns – rendered line exceeds terminal width. Highlights lack of graceful degradation for unusual display sizes.

7. **#4315** – [package-lock.json missing resolved/integrity entries since v0.74.0](https://github.com/earendil-works/pi/issues/4315)  
   **Status:** Open (bug, inprogress)  
   **Comments:** 4 | 👍 6  
   Missing `resolved`/`integrity` fields in `package-lock.json` break Nix and offline `npm ci` builds. A build reliability issue with high impact for reproducible environments.

8. **#3974** – [Double keypress in Alacritty (single backspace registers twice)](https://github.com/earendil-works/pi/issues/3974)  
   **Status:** Closed  
   **Comments:** 4  
   Backspace triggers twice in Alacritty on X11. Another terminal-specific input handling bug, suggesting Pi’s TUI needs better cross-terminal input normalization.

9. **#4538** – [Add `/exit` Alias for `/quit`](https://github.com/earendil-works/pi/issues/4538)  
   **Status:** Closed (weekend, refactor)  
   **Comments:** 4  
   Simple but popular quality-of-life request: `/exit` as an alias for `/quit`. Merged quickly – reflects users’ muscle memory from other CLI tools.

10. **#4522** – [Anthropic streaming response body not decompressed on Node.js v26](https://github.com/earendil-works/pi/issues/4522)  
    **Status:** Open  
    **Comments:** 4  
    Anthropic streaming responses arrive gzip-compressed but are not decompressed on Node v26 due to an empty `Headers` object from the SDK. Affects users on the latest Node LTS.

---

## Key PR Progress
*(10 selected for feature impact, fixes, and community value)*

1. **#4574** – [docs(coding-agent): document overflow normalization for custom providers](https://github.com/earendil-works/pi/pull/4574)  
   Adds documentation explaining how auto‑compaction is triggered when providers report context‑window limits. Helps custom provider authors avoid silent failures.

2. **#4567** – [docs(coding-agent): fix invalid notify type in extensions example](https://github.com/earendil-works/pi/pull/4567)  
   Fixes a sample using `"success"` in `ctx.ui.notify()`, which only accepts `"info" | "warning" | "error"`. Prevents confusion for extension developers.

3. **#4566** – [Force TUI redraw on terminal resize](https://github.com/earendil-works/pi/pull/4566)  
   Addresses broken TUI rendering after window resize (see issue #4568). Forces a full redraw on resize, preserving Termux soft-keyboard behavior.

4. **#4558** – [fix(ai): openai-completions - throw error on missing finish-reason](https://github.com/earendil-works/pi/pull/4558)  
   Tracks `finish_reason` and throws before emitting `done` if missing, improving error handling for non‑standard providers. A step toward provider compatibility.

5. **#4564** – [feat: add lockDefaults option](https://github.com/earendil-works/pi/pull/4564)  
   Implements a `lockDefaults` setting to prevent model/provider/thinking changes from persisting across sessions. Requested in #4565.

6. **#4562** – [Feat/add litellm provider](https://github.com/earendil-works/pi/pull/4562)  
   Adds LiteLLM as a built‑in provider, leveraging the existing `openai-completions` wire format for 100+ backends. Lowers friction for teams using a LiteLLM proxy.

7. **#4560** – [feat(ai): add firepass provider support](https://github.com/earendil-works/pi/pull/4560)  
   Adds Fireworks FirePass (subscription) as a provider, enabling access to Skimi K2.6 models. Demonstrates community drive to support new inference services.

8. **#4555** – [feat(ai): add "adaptive" thinking level for Claude 4.6+/4.7/Sonnet 4.6](https://github.com/earendil-works/pi/pull/4555)  
   Exposes Anthropic's new `thinking: { type: "adaptive" }` mode, letting Claude self‑regulate thinking budget. A forward‑looking feature for next‑gen reasoning models.

9. **#4552** – [Copilot/fix auto compact functionality](https://github.com/earendil-works/pi/pull/4552)  
   Introduces `shouldStopAfterTurn` hook to trigger automatic context compaction when the window limit is reached. Directly addresses long‑running agent crashes.

10. **#4547** – [UI enhancements: Tokyo Night theme, Unicode progress bars, modern styling](https://github.com/earendil-works/pi/pull/4547)  
    Adds a Tokyo Night theme, auto‑discovers themes from directory, Unicode block bars for context usage, and a graceful compaction spinner. Aesthetic and functional polish.

---

## Feature Request Trends
- **Local & Custom Provider Support** – Issue #3357 (dynamic model listing for local LLMs) remains the top‑voted feature. PRs for LiteLLM and FirePass show the community wants easy access to diverse backends.
- **Configuration Flexibility** – Requests for model aliases (#4569), `lockDefaults` (#4565), command‑based `apiKey` (#4557), and `/exit` alias (#4538) indicate a desire for more user‑controllable defaults and session behavior.
- **Thinking / Reasoning Control** – Adaptive thinking for Claude (#4555) and general desire to control `reasoning_content` preservation (see also pain points) are driving new PRs.
- **Tooling Improvements** – Case‑insensitive tool call names (#4517), SPD spec additions (#4572), and frontmatter parsing robustness (#4532) reflect maturing extension ecosystem.

---

## Developer Pain Points
- **reasoning_content Propagation Bugs** – Multiple issues (#4251, #4514, #4526, #4505) report 400 errors when thinking mode is enabled: `reasoning_content` is either missing in tool calls, injected as extra field, or not preserved across turns. This is the most frequent source of runtime errors for users of reasoning models.
- **Terminal Compatibility Roulette** – Shift+Enter fails in Konsole (#3113), double backspace in Alacritty (#3974), missing Shift+Enter on macOS (#4520), crashes on narrow terminals (#4556), and broken rendering after resize (#4568). Each terminal seems to expose a unique TUI edge case.
- **Package & Build Reliability** – Missing `resolved`/`integrity` entries in `package-lock.json` (#4315) breaks Nix builds, while repeated `pnpm install -g` on startup (#4501) frustrates users of pnpm 11.
- **Context Compaction / Orphan toolResult** – Issue #4570 reports an unrecoverable state after two compactions cause a `toolResult` to outlive its `toolCall`. This regression disrupts long agent sessions.
- **Installation Permission Errors** – Issue #4525 shows `npm install -g` fails on fresh systems without write access to global Node modules – a barrier for new users.
- **Node Version Compatibility** – Anthropic streaming fails on Node v26 (#4522) due to SDK changes, highlighting the challenge of keeping up with Node releases.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-05-16

## Today's Highlights

Today’s digest is dominated by terminal UX polish (clickable markdown links, auto-restore on crash), **daemon mode** architecture design (three draft adapter plans landed), and the start of a systematic memory diagnostics effort (`/doctor memory`). On the bug front, a weak-network wedge affecting DeepSeek-V4-Pro users was closed, while a wave of OOM reports from long sessions triggered multiple new memory-triage issues. Community discussion on **OAuth free tier reduction** (#3203) continues to simmer with 125 comments, reflecting strong user sentiment.

## Releases

Three releases shipped today, all sharing the same changelog:

- **v0.15.11-nightly.20260516.435f711e3**
- **v0.15.12-preview.2**
- **v0.15.12-preview.1**

**What’s Changed (common to all):**
- `feat(cli)`: wrap markdown links in OSC 8 escape sequences so wrapped URLs remain clickable in terminals that support the standard (`@BZ-D` in [#4037](https://github.com/QwenLM/qwen-code/pull/4037)).
- `fix(core)`: normalize cumulative OpenAI stream deltas to suffixes, fixing a malformed-stream edge case (`@chiga0` in [#3896](https://github.com/QwenLM/qwen-code/pull/3896)).
- `fix(cli)`: auto-restore of the previous session on crash or unexpected exit.

## Hot Issues

1. **[#3203](https://github.com/QwenLM/qwen-code/issues/3203) – Qwen OAuth Free Tier Policy Adjustment**  
   ☑ *Needs-triage, Feature-request* | 125 comments  
   **Why it matters:** Proposes drastic reduction from 1,000 to 100 free requests/day, and phase-out in 60 days. The comment count indicates strong community backlash. No contributor reaction yet; maintainers likely watching closely.

2. **[#3803](https://github.com/QwenLM/qwen-code/issues/3803) – Daemon Mode Proposal (`qwen serve` design series)**  
   ☑ *Needs-triage, Feature-request* | 12 comments · 1 👍  
   **Why it matters:** A comprehensive 6-chapter design for a headless daemon. This is the architectural spine of Mode A/B separation. Community engagement is measured but includes authoring from core contributor `@wenshao`.

3. **[#4156](https://github.com/QwenLM/qwen-code/issues/4156) – `qwen --serve` (Mode A): TUI + in-process HTTP daemon**  
   ☑ *Feature-request, CLI* | 6 comments  
   **Why it matters:** Direct follow-up to #3803, proposing a 3-phase plan to let a local user’s TUI also run a daemon. Addresses a real workflow gap – today you can’t run both simultaneously.

4. **[#3914](https://github.com/QwenLM/qwen-code/issues/3914) – API Connected, No Errors but Fail to Fetch**  
   ☑ *Bug, Authentication* | 5 comments · 1 👍  
   **Why it matters:** A persistent connection error on OpenRouter with no clear error path. Users are stuck with a silent failure. The 1 👍 suggests it affects multiple people.

5. **[#4167](https://github.com/QwenLM/qwen-code/issues/4167) – CLI Crashed (OOM)**  
   ☑ *Bug, Memory* | 5 comments  
   **Why it matters:** Full V8 OOM with mark-compact logs showing heap pressure near 2 GB. Likely long session + large context. This is part of a broader OOM trend (see #4185). High urgency for heavy users.

6. **[#4177](https://github.com/QwenLM/qwen-code/issues/4177) – SSE Stream Idle Watchdog**  
   ☑ *Feature-request, Core* | 0 comments  
   **Why it matters:** Proposes aborting hung SSE streams after idle timeout – weak‑network hang half of the failure mode fixed in #4176. Important for reliability on mobile/train connections.

7. **[#4178](https://github.com/QwenLM/qwen-code/issues/4178) – Close `tool_use↔tool_result` Invariant at Failure Point**  
   ☑ *Enhancement, Core* | 2 comments  
   **Why it matters:** Defense-in-depth for the tool‑use contract after #4176. Prevents future regressions.

8. **[#4185](https://github.com/QwenLM/qwen-code/issues/4185) – OOM in Long Sessions: V8 Heap Pressure**  
   ☑ *Bug, Performance* | 1 comment  
   **Why it matters:** Explicitly calls out the root cause – huge context retention from large tool outputs and diffs. This is the core memory issue driving #4182, #4183, #4184.

9. **[#4171](https://github.com/QwenLM/qwen-code/issues/4171) – Tab Key Conflict on Windows**  
   ☑ *Bug, Keybindings* | 1 comment  
   **Why it matters:** Tab triggers both auto-complete and permission mode simultaneously. UX-critical for Windows users; suggests need for custom keybindings.

10. **[#4194](https://github.com/QwenLM/qwen-code/issues/4194) – [API Error: Connection error. (fetch failed)]**  
    ☑ *Bug, Authentication* | 1 comment  
    **Why it matters:** Another fetch-failed report (same as #3914), reinforcing that OpenRouter/3rd-party endpoint failures are a recurring pain point.

## Key PR Progress

1. **[#4197](https://github.com/QwenLM/qwen-code/pull/4197) – docs(channel): draft daemon adapter plan**  
   **What:** Adapter plan for consuming `qwen serve` from channel/web backends via `DaemonSessionClient`.  
   **Why important:** Extends daemon reach to non-CLI consumers (chat bots, web UIs). Architecture-first approach.

2. **[#4198](https://github.com/QwenLM/qwen-code/pull/4198) – docs(ide): draft daemon adapter plan**  
   **What:** Adapter plan for VS Code extension host to connect to `qwen serve`.  
   **Why important:** First-party IDE integration path; explicit boundary that webview code must not talk directly to daemon.

3. **[#4196](https://github.com/QwenLM/qwen-code/pull/4196) – docs(tui): draft daemon adapter plan**  
   **What:** Flag-gated `DaemonSessionClient` transport for TUI.  
   **Why important:** TUI is the first Mode B dogfood client; default-off migration ensures safety.

4. **[#4195](https://github.com/QwenLM/qwen-code/pull/4195) – feat(sdk): add DaemonSessionClient skeleton**  
   **What:** Experimental SDK wrapper binding a daemon session to `DaemonClient`, including `Last-Event-ID` replay.  
   **Why important:** Concrete code for the adapter plans above – the building block for all Mode B clients.

5. **[#4180](https://github.com/QwenLM/qwen-code/pull/4180) – feat(cli): add baseline /doctor memory diagnostics**  
   **What:** First `/doctor memory` slice: paste-safe V8 heap stats, handle counts, process metadata.  
   **Why important:** Kicks off the memory diagnostics programme (#3000). Essential for debugging OOMs.

6. **[#4193](https://github.com/QwenLM/qwen-code/pull/4193) – Allow custom output directory for /export**  
   **What:** `/export` now accepts optional output directory; creates directory if not exists.  
   **Why important:** Addresses long-standing clutter complaint when exporting multiple sessions.

7. **[#4191](https://github.com/QwenLM/qwen-code/pull/4191) – feat(serve): add capability registry protocol versions**  
   **What:** `qwen serve` now advertises serve protocol version and has a feature registry for future daemon extensions.  
   **Why important:** Enables stable negotiation between daemon and future clients.

8. **[#4174](https://github.com/QwenLM/qwen-code/pull/4174) – feat(worktree): Phase C — session persistence, hooksPath, Footer + WorktreeExitDialog**  
   **What:** Adds worktree session persistence to `.qwen/file-history/`, hooks path configuration, and UI for worktree exit.  
   **Why important:** Completes major chunk of the worktree feature (Phase A+B in #4073).

9. **[#4064](https://github.com/QwenLM/qwen-code/pull/4064) – feat(rewind): add file restoration support to /rewind**  
   **What:** File-copy backup system (ported from claude-code’s `fileHistory`) so `/rewind` can roll back file changes.  
   **Why important:** Solves #3697 – previously `/rewind` only truncated conversation, leaving modified files on disk.

10. **[#4176](https://github.com/QwenLM/qwen-code/pull/4176) – fix(core,cli): close tool_use↔tool_result invariant across all failure paths**  
    **What:** Fixes unrecoverable wedge on weak-network connections with DeepSeek-V4-Pro (and Anthropic-compatible backends). Persists partial assistant turn so `tool_result` lands correctly.  
    **Why important:** A critical reliability fix; reproduces under three additional failure modes, all closed.

## Feature Request Trends

1. **Daemon Mode & Client Adapters** – The largest feature vector this week. Three adapter plan PRs (channel, IDE, TUI) and the `DaemonSessionClient` skeleton indicate a coordinated push toward making `qwen serve` a first-class production service with multiple consumption modes.

2. **Memory Diagnostics & OOM Mitigation** – A burst of ~6 issues/PRs (#3000, #4179, #4181–4185, #4188) all targeting memory pressure. Requests span from baseline `/doctor memory` to heap snapshot tools to bounded cache eviction. The volume signals that long-session users are hitting limits hard.

3. **Export/File Management** – [#4192](https://github.com/QwenLM/qwen-code/issues/4192) (custom export directory) and [#4173](https://github.com/QwenLM/qwen-code/issues/4173) (stale file-history cleanup) show users want more control over output artifacts and less disk clutter.

4. **Authentication & Endpoint Flexibility** – [#4138](https://github.com/QwenLM/qwen-code/issues/4138) (DashScope-compatible custom endpoints) and multiple fetch-failed reports (#3914, #4194) point to a need for first-class support for non-OpenAI gateways.

5. **Platform-Specific UX** – [#4171](https://github.com/QwenLM/qwen-code/issues/4171) (Windows Tab conflict) and older Git Bash issues (#2774) highlight that Windows and alternative shells remain underserved.

## Developer Pain Points

- **API Connection Failures on Third-Party Endpoints** – Repeated reports of `[API Error: Connection error. (cause: fetch failed)]` with no clear resolution path. Users on OpenRouter and custom gateways are most affected. (#3914, #4194)
- **OOM in Long Sessions** – V8 heap exhaustion is the most common hard crash this cycle. Contributors are reacting with diagnostics, but the root cause (large tool output retention) is not yet mitigated. (#4167, #4185)
- **Weak-Network Reliability** – DeepSeek-V4-Pro users on mobile/train connections experienced unrecoverable wedges. The fix (#4176) addresses one half; an SSE idle watchdog (#4177) is proposed for the other.
- **Windows Keybinding Conflicts** – Tab key collision between auto-complete and permission mode is a daily frustration for Windows developers. No fix merged yet. (#4171)
- **MCP Tools Silently Unavailable in Headless Mode** – A regression after progressive-MCP rollout left `--prompt` mode without access to MCP tools, with no error message. (#4163, closed)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*