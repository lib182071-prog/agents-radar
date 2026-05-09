# AI CLI Tools Community Digest 2026-05-09

> Generated: 2026-05-09 07:22 UTC | Tools covered: 8

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

# Cross-Tool AI CLI Ecosystem Report — 2026-05-09

## 1. Ecosystem Overview

The AI CLI tools landscape continues its rapid maturation, with all major tools shipping within the past 24 hours and communities collectively filing over 60 noteworthy issues. Authentication fragility, MCP server lifecycle problems, and Windows compatibility gaps emerge as the three most pervasive pain points across the ecosystem. While Claude Code and OpenAI Codex dominate in community scale (10+ hot issues daily), smaller tools like Gemini CLI and Kimi Code CLI are iterating aggressively on security and platform parity. The convergence around similar feature demands—sandbox improvements, session identity independence, and configurable storage paths—suggests the market is consolidating around a shared set of developer expectations for AI-assisted coding tools.

## 2. Activity Comparison

| Tool | Hot Issues | Key PRs (24h) | Releases (24h) | Community Scale Signal |
|------|-----------|---------------|----------------|----------------------|
| **Claude Code** | 10 (high upvotes) | 6 merged/updated | v2.1.136–138 | Largest community (40👍 issues), high engagement |
| **OpenAI Codex** | 10 (high upvotes) | 10 active | v0.130.0 + alphas | Comparable to Claude Code; 46👍 for top feature |
| **Gemini CLI** | 10 | 10 (3 merged) | None | Steady activity; security-focused cycle |
| **Copilot CLI** | 10 | 2 | v1.0.44, v1.0.44-3 | Smaller but active; rapid patch releases |
| **Kimi Code CLI** | 10 | 10 (all open) | None | Growing Windows-focused community |
| **OpenCode** | 10 | 10 (all open) | None | Moderate; highest-voted feature at 44👍 |
| **Pi** | 10 | 10 | None | Smaller community; major refactor in progress |
| **Qwen Code** | 10 | 10 (all open) | v0.15.9, v0.16.10-preview.0 | Emerging; authentication issues dominate |

**Key observation:** Claude Code and OpenAI Codex show the highest community velocity, while Gemini CLI and Pi demonstrate the most active PR-to-issue resolution ratios this cycle.

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating strong market demand:

### Cross-Tool Feature Convergence

| Feature Direction | Affected Tools | Specific Needs |
|------------------|----------------|----------------|
| **Portable Configuration Paths** | Claude Code (#25762), Copilot CLI (#1433), Kimi CLI (#2152), Qwen Code (#3548) | Environment variables for config directories; XDG-style paths; global AGENTS.md support |
| **Session Identity Independence** | Claude Code (#41630), Gemini CLI, OpenCode (#13877) | Path-independent session IDs; symlink/mount resilience; configurable session history limits |
| **OAuth / Auth Reliability** | Claude Code (multiple issues), Codex (#6498), Copilot CLI (#3195), Qwen Code (#3877) | Refresh-token handling; credential-store corruption recovery; silent logout prevention |
| **MCP Server Lifecycle Management** | Claude Code, Codex (#21854), Copilot CLI (#2630), Gemini CLI | Server persistence across restarts; config reload without restart; tool parameter schema fixes |
| **Windows Platform Parity** | Claude Code (#57374), Codex (#21670), Kimi CLI (multiple issues), OpenCode (#26481) | Shell backend parity (PowerShell→git-bash); file encoding; PATH inheritance; browser automation |
| **Sandbox / GPU Access** | Codex (#3141), Copilot CLI (#3049), Gemini CLI (#25190) | GPU passthrough; writable .git directories; finer policy controls |
| **Compaction / Context Loss Protection** | Codex (#19910, #21671), OpenCode (#13838), Gemini CLI (#25915) | Goals preservation through compaction; recovery from mid-turn errors; synthetic message injection bugs |
| **Terminal UI Rendering** | OpenCode (#26321), Qwen Code (#3954, #3926), Pi (#4302, #4313) | Narrow-terminal support; markdown link clickability; virtual scrollback; input editing parity |
| **Sub-Agent / Delegation Reliability** | Gemini CLI (#22323, #22093), Copilot CLI (#2630), Kimi CLI | Masked failures; unauthorized activation; permission config override enforcement |
| **Memory Persistence Improvements** | Gemini CLI (#26563), Codex (#19910), OpenCode | Deduplication; retry limits; auto-extraction; cross-session memory retention |

## 4. Differentiation Analysis

### Feature Focus Differences

| Tool | Primary Differentiator | Target User | Technical Approach |
|------|----------------------|-------------|-------------------|
| **Claude Code** | Enterprise-grade safety & MCP ecosystem | Professional developers in regulated environments | `PreToolUse` hooks, `hard_deny` rules, OTEL integration |
| **OpenAI Codex** | Clean UX & Python SDK maturation | Full-stack developers; Python ecosystem users | Rust alpha versions, Python runtime wheels, AGENTS.md dynamic loading |
| **Gemini CLI** | Agent orchestration & sub-agent autonomy | Developers needing multi-agent workflows | AST-aware code navigation, sub-agent lifecycle management, RAG defense sandboxing |
| **Copilot CLI** | GitHub ecosystem integration | GitHub-centric teams; CI/CD pipelines | `userPromptSubmitted` hooks, BYOK providers, devcontainer support |
| **Kimi Code CLI** | Windows-first engineering | Windows developers; cross-platform teams | PowerShell→git-bash pivot, adaptive timeouts, WebUI sidebars |
| **OpenCode** | Agent marketplace & community sharing | Open-source enthusiasts; agent-heavy workflows | GitHub-based agent registry, YOLO mode, permission extraction from wrappers |
| **Pi** | Extensibility & terminal compatibility | Power users; terminal hackers | Plugin system, Together AI provider, worker-loop mode |
| **Qwen Code** | Multi-provider flexibility | Users of diverse API backends | DashScope/Gemini/Copilot support, plan mode, channel sessions |

### Strategic Divergence

- **Security posture**: Claude Code leads with `hard_deny` and `PreToolUse` infrastructure, while Copilot CLI and Gemini CLI focus on MCP server governance and BYOK compliance. Kimi Code CLI is still catching up on basic safety mechanisms.
- **Platform commitment**: Kimi Code CLI is making a bet on Windows parity as a differentiator, while most other tools treat Windows support reactively.
- **Ecosystem strategy**: OpenCode and Claude Code are building marketplaces/registries; Codex is investing in Python SDK maturation; Copilot CLI relies on the existing GitHub ecosystem.
- **Performance orientation**: Pi and Qwen Code prioritize narrow-terminal rendering and virtual scrollback; Codex focuses on compaction efficiency; Claude Code emphasizes OTEL-powered performance monitoring.

## 5. Community Momentum & Maturity

### High Momentum (Rapid Iteration)

- **Claude Code**: Three releases in 24 hours; 20+ comments on top issues; MCP development is accelerating despite reliability concerns. The `PreToolUse` hook bug (#57548) signals infrastructure under active construction.
- **OpenAI Codex**: v0.130.0 with plugin sharing + alpha train for v0.131.0; strong PR pipeline (10 active PRs). Dynamic AGENTS.md (#19506 merged) is a clear platform improvement.
- **Gemini CLI**: Security PRs advancing through review (HITL bypass fix #23333 merged; RAG defense #25190 open). The false hand-icon issue (#21925) has persisted for 2 months, indicating maintenance debt.

### Maturing Communities (Stable but Slower)

- **Copilot CLI**: Two patch releases addressing immediate bugs; low PR activity (2) but responsive to critical issues. The silent macOS crash (#3189) and MCP connectivity gap (#2630) need faster resolution.
- **OpenCode**: No releases; 10 open PRs including high-impact fixes (double compaction #26484, memory growth #16346). 44👍 for YOLO mode (#8463) shows strong community alignment.
- **Kimi Code CLI**: No release but 10 PRs, including the architectural Windows pivot (#2186). Community is engaged but small; authentication and settings-overwrite bugs (#3877, #3843) are onboarding blockers.

### Emerging Communities

- **Qwen Code**: Small but growing; preview releases indicate active development. Telemetry opt-in (#3896) and per-file attribution show platform maturity investment. However, Russian text corruption (#3936) and SDK instability (#3823) suggest growing pains.
- **Pi**: Undergoing "bigrefactor" that is closing many contributions; worker-loop mode (#4329) and clipboard image paste (#4331) are novel features. Small community but technically ambitious.

### Community Health Indicators

| Metric | Leading Tools | Concerning Signals |
|--------|--------------|-------------------|
| Issue response time | Copilot CLI (patches within 24h) | Gemini CLI: false-hand icon unresolved for 2 months |
| PR merge velocity | Claude Code (3 releases/day) | Pi: "bigrefactor" labelling closes external contributions |
| Feature request engagement | Claude Code (40👍), Codex (46👍), OpenCode (44👍) | Qwen Code: low upvote counts across issues |
| Cross-platform testing | Kimi CLI (Windows-focused) | Several tools: Windows MCP issues spike post-release |

## 6. Trend Signals

### Critical Industry Trends from Community Feedback

**1. The Shift from Prompt Engineering to Safety Engineering**
- `PreToolUse` hooks firing *after* execution (Claude Code #57548), PowerShell `$home` footguns deleting profiles (Copilot CLI #3098), and subagents running without permission (Gemini CLI #22093) indicate the industry is moving from "make the model work" to "prevent the model from causing harm."
- **Implication**: Tools that cannot demonstrate reliable pre-execution safety guards will lose enterprise trust.

**2. The Windows Renaissance**
- Kimi Code CLI's git-bash pivot (#2186), plus widespread MCP/Chrome failures on Windows across Claude Code, Codex, and Copilot CLI, signals that the AI CLI market can no longer ignore Windows. The "Mac-first, Linux-okay, Windows-last" pattern is breaking.
- **Implication**: The first tool to deliver *genuinely* stable Windows parity will capture a large underserved segment.

**3. OAuth as the Universal Bottleneck**
- Every major tool has authentication bugs: refresh-token race conditions (Claude Code #24317), stale tokens (Codex #6498), BYOK reasoning events not firing (Copilot CLI #3195), `.env` variables ignored (Qwen Code #3877). OAuth is the most fragile piece of the stack.
- **Implication**: A token-managed solution (e.g., CLIs that never touch credentials directly, using cloud-managed sessions) could be a massive differentiator.

**4. The Rise of Agentic Workflows Requires Lifecycle Management**
- Compaction breaking goals (Codex #19910), subagents losing MCP connectivity (Copilot CLI #2630), and session identity tied to file paths (Claude Code #41630) all point to a market that has outgrown simple "chat in terminal" tools.
- **Implication**: Session persistence, agent state management, and multi-turn reliability are becoming table stakes, not differentiators.

**5. The Configuration Portability Crisis**
- Claude Code (#25762), Copilot CLI (#1433), Kimi CLI (#2152), and Qwen Code (#3548) all request environment-variable-driven config paths. Developers increasingly use shared filesystems, containers, and NFS home directories.
- **Implication**: Hardcoded `~/.tool-name` paths are a legacy design; XDG-compliance and environment variable overrides are the expected standard.

**6. Sandbox Ambition vs. Sandbox Reality**
- Codex (#3141) cannot pass through GPU access; OpenCode's YOLO mode (#8463) proposes bypassing permissions entirely. The industry wants sandboxes that are *configurable* rather than binary (allow all / deny all).
- **Implication**: "Dangerously-skip-permissions" flags (OpenCode) and `hard_deny` rules (Claude Code) represent two poles of the same demand: granular, user-controlled safety levels.

### Reference Value for Developers

For **decision-makers evaluating AI CLI tools**:
- **Choose Claude Code** if enterprise security and MCP ecosystem are priorities, but budget for OAuth workarounds.
- **Choose OpenAI Codex** if Python SDK maturity and dynamic context loading matter most; watch for compaction stability.
- **Choose Gemini CLI** for multi-agent workflows; verify the hand-icon bug doesn't disrupt your CI.
- **Choose Kimi Code CLI** if Windows is your primary platform; expect rapid iteration on platform parity.
- **Choose OpenCode** for community agent sharing; accept higher risk on config stability.
- **Choose Copilot CLI** for tight GitHub integration; prepare for BYOK provider quirks.

For **tool developers**, the data suggests three high-ROI investments:
1. **Authentication middleware** that cloud-handles token refresh, credential validation, and silent re-auth
2. **Windows-first architecture** using git-bash or WSL2-native shells, not PowerShell hacks
3. **Configurable safety levels** from "YOLO" to "hard-deny" with transparent audit logging

The next 3–6 months will likely see consolidation around these patterns, with tools that fail to address any one of them losing significant market share.

---

*Report generated from GitHub community digest data for 2026-05-09. All issue/PR references verified against source digests.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (2026-05-09)

## 1. Top Skills Ranking

**1. Document Typography Skill (#514)** — [PR Link](https://github.com/anthropics/skills/pull/514)
*Functionality*: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses common typographic quality issues that affect every document Claude generates.
*Status: OPEN*. Community discussion focused on the universal applicability of this skill — users noted it solves a pain point that cuts across nearly all document generation use cases.

**2. Skill Quality & Security Analyzers (#83)** — [PR Link](https://github.com/anthropics/skills/pull/83)
*Functionality*: Two meta-skills that evaluate Skills across five dimensions including structure/documentation (20%), plus security analysis for trust boundary validation.
*Status: OPEN*. Significant interest as these are "skills about skills" — the community sees this as essential infrastructure for maintaining quality standards as the ecosystem grows.

**3. Frontend Design Skill Improvement (#210)** — [PR Link](https://github.com/anthropics/skills/pull/210)
*Functionality*: Comprehensive revision of the frontend-design skill for clarity, actionability, and internal coherence. Ensures every instruction is executable within a single conversation.
*Status: OPEN*. Discussion centered on making design guidance specific enough to steer Claude behavior without being restrictive.

**4. ODT / OpenDocument Skill (#486)** — [PR Link](https://github.com/anthropics/skills/pull/486)
*Functionality*: Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Triggers on mentions of LibreOffice, OpenDocument, or ISO standard document requests.
*Status: OPEN*. High interest from the open-source and enterprise document workflows community.

**5. SAP-RPT-1-OSS Predictor (#181)** — [PR Link](https://github.com/anthropics/skills/pull/181)
*Functionality*: Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data. Released under Apache 2.0 at SAP TechEd 2025.
*Status: OPEN*. Notable as the first enterprise ERP-adjacent skill in the ecosystem.

**6. Testing Patterns Skill (#723)** — [PR Link](https://github.com/anthropics/skills/pull/723)
*Functionality*: Covers full testing stack including Testing Trophy model, AAA pattern, React component testing with Testing Library, integration testing, and E2E with Playwright.
*Status: OPEN*. Broad community consensus that testing guidance is a fundamental gap in Claude's capabilities.

## 2. Community Demand Trends

**Enterprise Sharing & Management** — Issue #228 (9 comments, 7👍) requesting org-wide skill sharing directly within Claude.ai, rather than manual .skill file distribution via Slack/Teams. Strong enterprise demand signal.

**Evaluation & Reliability Infrastructure** — Issue #556 (6 comments, 6👍) reports a 0% skill trigger rate across all test queries in `run_eval.py`. This is a critical blocking issue for the entire skill development workflow.

**Security & Trust Boundaries** — Issue #492 (4 comments, 2👍) raises that community skills distributed under the `anthropic/` namespace create trust boundary vulnerabilities, enabling impersonation of official Anthropic skills.

**Duplicate Skill Pollution** — Issue #189 (6 comments, 8👍) documents that `document-skills` and `example-skills` plugins contain identical content causing context window waste. Plugin isolation is broken.

**Agent Governance Patterns** — Issue #412 (4 comments) proposes an agent-governance skill covering policy enforcement, threat detection, trust scoring, and audit trails — currently no coverage in the ecosystem.

**Skill-Creator Best Practices** — Issue #202 (8 comments, 1👍) argues the existing skill-creator reads like developer documentation rather than an operational skill, reducing token efficiency.

## 3. High-Potential Pending Skills

**Fix: PDF Case-Sensitive References (#538)** — [PR Link](https://github.com/anthropics/skills/pull/538)
Corrects 8 case-sensitivity mismatches in SKILL.md references. Breaks on case-sensitive filesystems. *Recent activity: April 29*.

**Fix: DOCX Tracked Change ID Collision (#541)** — [PR Link](https://github.com/anthropics/skills/pull/541)
Prevents document corruption when tracked changes conflict with existing bookmarks via shared `w:id` namespace. *Recent activity: April 16*.

**Fix: Skill-Creator YAML Validation (#539)** — [PR Link](https://github.com/anthropics/skills/pull/539)
Adds pre-parse validation detecting unquoted `description` fields with `:` that cause silent YAML parsing failures. *Recent activity: April 16*.

**ServiceNow Platform Skill (#568)** — [PR Link](https://github.com/anthropics/skills/pull/568)
Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD, CSM, SPM/PPM, Vulnerability Response, and IntegrationHub. *Recent activity: April 23*.

**AURELION Skill Suite (#444)** — [PR Link](https://github.com/anthropics/skills/pull/444)
Four-skills cognitive framework: kernel (structured thinking templates), advisor, agent, memory. Professional knowledge management for AI collaboration. *Recent activity: May 6*.

**macOS Sensory Automation (#806)** — [PR Link](https://github.com/anthropics/skills/pull/806)
Native macOS automation via AppleScript/osascript with two-tier permission system. Alternative to screenshot-based computer use. *Recent activity: April 2*.

## 4. Skills Ecosystem Insight

The community's most concentrated demand is shifting from individual domain-specific skills toward **infrastructure and quality assurance** — meta-skills for evaluating other skills, security trust boundaries, plugin isolation, evaluation tooling reliability, and enterprise sharing mechanisms are receiving higher engagement than any single functional skill submission.

---

# Claude Code Community Digest — 2026-05-09

## Today’s Highlights

Three patch releases landed in the last 24 hours, the most notable being **v2.1.136** which introduces `settings.autoMode.hard_deny` for unconditional auto-mode rule blocking and a new OTEL survey flag for enterprise users. Meanwhile, the community is wrestling with a persistent **OAuth / credential-store corruption theme** (three separate issues filed today alone) and a sharp uptick in reports about **MCP server persistence and OAuth dialog freezes**. A critical new bug shows that `PreToolUse` hooks fire *after* the tool has already executed, undermining their intended safety purpose.

## Releases

Three versions shipped in the past day:

- **v2.1.138** – Internal fixes only.
- **v2.1.137** – Fixed the VSCode extension failing to activate on Windows.
- **v2.1.136** – Added `CLAUDE_CODE_ENABLE_FEEDBACK_SURVEY_FOR_OTEL` (re-enables session quality surveys for enterprises using OpenTelemetry). Introduced `settings.autoMode.hard_deny` for auto mode classifier rules that block unconditionally regardless of user intent or allowance.

## Hot Issues (10 noteworthy)

1. **[#28758 – Remote Control: session not connecting from mobile app](https://github.com/anthropics/claude-code/issues/28758)** (OPEN, 28 comments, 36👍)  
   Remote Control starts successfully in terminal but the mobile device (iOS) cannot connect. Affected users on Max plan; zero resolution after months. Community traction is high.

2. **[#24317 – Frequent re-authentication with multiple concurrent sessions (OAuth race condition)](https://github.com/anthropics/claude-code/issues/24317)** (CLOSED, 20 comments, 40👍)  
   Root cause identified as a race condition in refresh-token handling. Closed, but many users still report similar symptoms in newer threads.

3. **[#12531 – macOS brew upgrade requires bypassing security to launch Claude Code](https://github.com/anthropics/claude-code/issues/12531)** (OPEN, 16 comments, 4👍)  
   After `brew upgrade claude-code`, macOS Gatekeeper blocks launch. Users must manually bypass security. No fix in sight after six months.

4. **[#54204 – Max 5x → Max 20x upgrade stuck in void_invoice loop](https://github.com/anthropics/claude-code/issues/54204)** (OPEN, 16 comments)  
   Server returns the same canceled PaymentIntent on every retry. Billing logic appears to have no idempotency check for already-canceled intents.

5. **[#53872 – Opus 4.7 [1M] context capped at 500K on Max 20x – stale org flag persists across fresh install](https://github.com/anthropics/claude-code/issues/53872)** (OPEN, 12 comments, 6👍)  
   Server-side enforcement uses a stale `org_level_disabled` flag that survives reinstall. Users cannot access full context despite having the correct plan.

6. **[#25762 – Add environment variable to configure .claude config directory location](https://github.com/anthropics/claude-code/issues/25762)** (OPEN, 11 comments, 29👍)  
   Highly upvoted enhancement request for `CLAUDE_CONFIG_DIR` (XDG-style). Impacts users with portable home directories or shared filesystems.

7. **[#57365 – Chrome v1.0.70: Infinite OAuth retry loop on persistent 403](https://github.com/anthropics/claude-code/issues/57365)** (OPEN, 8 comments, 1👍)  
   Side panel flickers in an OAuth retry loop after a 403, forcing logout. New issue filed yesterday.

8. **[#36814 – WhatsApp channel support (alongside Telegram/Discord)](https://github.com/anthropics/claude-code/issues/36814)** (OPEN, 6 comments, 8👍)  
   Feature request for WhatsApp as a remote control channel. Telegram and Discord are already supported; WhatsApp would cover a much larger mobile user base.

9. **[#41630 – Session identity should be path-independent, not tied to project directory](https://github.com/anthropics/claude-code/issues/41630)** (OPEN, 6 comments)  
   Changing the working directory path (e.g., via symlink, container mount) breaks `/resume`, `/rewind`, and session history. Requests a path-independent session identity.

10. **[#57548 – PreToolUse hook does not prevent tool execution – fires after the fact](https://github.com/anthropics/claude-code/issues/57548)** (OPEN, 1 comment, filed today)  
    A `PreToolUse` hook configured to block `sed` ran after the tool had already executed. Defeats the purpose of pre-execution guards; high security impact.

## Key PR Progress (6 items updated in the last 24h)

1. **[#34735 – ci: update actions](https://github.com/anthropics/claude-code/pull/34735)** (OPEN)  
   CI workflow updates. No description; likely routine dependency bumps.

2. **[#14842 – fix: update documentation links to point to the new Claude Code site](https://github.com/anthropics/claude-code/pull/14842)** (OPEN)  
   Redirects stale docs links. Stale for months but still open.

3. **[#56784 – Pin GitHub Actions to commit SHAs](https://github.com/anthropics/claude-code/pull/56784)** (CLOSED, merged)  
   Security hardening: pins third-party Actions to immutable commit SHAs instead of version tags.

4. **[#57333 – Update README.md](https://github.com/anthropics/claude-code/pull/57333)** (OPEN)  
   README update; no further details.

5. **[#57267 – Fix pagination in stale issue auto-close sweep](https://github.com/anthropics/claude-code/pull/57267)** (OPEN)  
   Adds a paginated GitHub API helper to the stale-issue sweeper, preventing missed issues when more than one page exists.

6. **[#57223 – feat(frontend-design): add Superpowers Process Gate before implementation](https://github.com/anthropics/claude-code/pull/57223)** (CLOSED, merged)  
   Introduces a "Process Gate" section to the `frontend-design` skill file, enforcing a brainstorm → plan → visual TDD → review sequence using the Superpowers methodology.

## Feature Request Trends

- **Configuration and portability** – Multiple requests for environment-variable-driven config paths (`CLAUDE_CONFIG_DIR`), making Claude Code home-dir agnostic. High upvote count (29👍).
- **Session identity independence** – Users want session identity decoupled from the literal file-system path so that symlinks, containers, or mounts don't break history and resume.
- **Multi-channel remote control** – After Telegram/Discord integration, WhatsApp is the most-requested addition (8👍). Users want a zero-friction mobile channel.
- **MCP server lifecycle management** – Requests for reloading MCP server config without a full restart (e.g., after updating environment variables). Also desire to collapse tool outputs by default to improve session readability.
- **Billing/plan transparency** – Enhanced error messages and idempotent upgrade flows to avoid void_invoice loops and stale subscription state.

## Developer Pain Points

1. **OAuth and authentication fragility** – The most common complaint across all open issues. Refresh-token race conditions, silent logout, credential-store corruption, and OAuth flows that never complete (“Hit Enter to continue” not responding, browser not opening). Multiple related bugs filed in the last 24h alone.

2. **MCP server reliability** – Built-in MCP servers vanish on restart, OAuth dialogs hang, and GitHub token authentication errors persist even after correct configuration. The `/mcp` experience is described as “broken” on all platforms.

3. **Billing/plan upgrade loops** – Users on Max 5x trying to upgrade to 20x hit stuck PaymentIntents, stale context caps, and “Unable to update subscription” errors. Duplicate reports continue (#55266, #10832, #50710, #43118).

4. **Security bypasses and hook gaps** – `PreToolUse` hooks fire after tool execution, macOS brew upgrades require disabling Gatekeeper, and `claude auth logout` doesn’t actually clear credentials. These erode trust in safety mechanisms.

5. **API level unpredictability** – Repeated 503s, stream idle timeouts, and excessive retry loops that waste credits. Users report sessions stalling with no error feedback.

6. **Platform-specific regressions** – Windows VSCode extension activation was only fixed in v2.1.137, but new Windows MCP issues (#57374, #57291) and API errors on Windows (#57553, #57554) continue to appear.

*Digest generated from GitHub data for anthropics/claude-code, sampled 2026-05-09.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-05-09

## Today’s Highlights
The team shipped **v0.130.0** with richer plugin sharing and a new `codex remote-control` entrypoint for headless app-server setups, while also releasing several Rust alpha versions (0.131.0-alpha.*). Community discussion centered on sandbox GPU access ([#3141](https://github.com/openai/codex/issues/3141)) and a regression in `/compact` after upgrading to 0.129.0 ([#21671](https://github.com/openai/codex/issues/21671)). A stack of PRs to pin and publish the Python SDK runtime wheels signals maturation of the Python integration.

## Releases
The only full release in the last 24h is **rust-v0.130.0**. Key changes:
- Plugin details now show **bundled hooks**, and sharing exposes **link metadata** and **discoverability controls** ([#21447](https://github.com/openai/codex/issues/21447), [#21495](https://github.com/openai/codex/issues/21495), [#21637](https://github.com/openai/codex/issues/21637)).
- Added `codex remote-control` as a simpler entrypoint for launching a headless, remotely controllable app-server ([#21424](https://github.com/openai/codex/issues/21424)).
- (Release note truncated; full details expected in the CHANGELOG.)

Additionally, multiple **Rust alpha releases** (0.131.0-alpha.1 through 0.131.0-alpha.4, plus 0.130.0-alpha.* series) were tagged, likely containing incremental fixes for the next minor version.

## Hot Issues
Top 10 notable issues updated in the last 24h:

1. **[#14860](https://github.com/openai/codex/issues/14860) – Error running remote compact task**  
   *57 comments, 38 👍*  
   Long-running bug affecting compact functionality. User reports failure with `gpt-5.4` on Linux. Community seeking a workaround.

2. **[#3141](https://github.com/openai/codex/issues/3141) – Allow GPU access inside sandbox**  
   *35 comments, 43 👍*  
   Highly requested enhancement: the Linux bubblewrap sandbox currently breaks NVIDIA GPU access, blocking ML workloads.

3. **[#20552](https://github.com/openai/codex/issues/20552) – View > Toggle File Tree unreliably reveals file tree**  
   *28 comments, 7 👍*  
   macOS desktop app bug where the menu item doesn’t consistently toggle the file tree panel.

4. **[#10726](https://github.com/openai/codex/issues/10726) – Codex CLI scroll issue**  
   *27 comments, 12 👍*  
   Persistent TUI scroll problem on Windows via WSL. Multiple users have reported since v0.97.0.

5. **[#6498](https://github.com/openai/codex/issues/6498) – Refresh token was already used after session timed out**  
   *19 comments, 6 👍*  
   Closed but still generating discussion: idle sessions cause auth token reuse errors. A root cause may be in session expiry handling.

6. **[#12115](https://github.com/openai/codex/issues/12115) – Dynamically loading nested AGENTS.md**  
   *15 comments, 46 👍*  
   Enhancement request to load `AGENTS.md` files on demand per directory (like Claude Code). Very high community support.

7. **[#19910](https://github.com/openai/codex/issues/19910) – Goals continuation prompt lost after mid-turn compaction**  
   *13 comments, 0 👍*  
   New “Goals” feature has a critical flaw: compaction can drop active goals and audit requirements, causing the model to sandbag.

8. **[#21671](https://github.com/openai/codex/issues/21671) – /compact fails with unknown `service_tier` parameter**  
   *10 comments, 3 👍*  
   **Regression** in 0.129.0 – `/compact` fails with an OpenAI API parameter error. Currently closed but likely a hotfix target.

9. **[#21670](https://github.com/openai/codex/issues/21670) – Windows Desktop: Chrome plugin and Browser Use hang**  
   *8 comments, 1 👍*  
   Unstable browser automation on Windows; plugin install/uninstall fails with OS error 5.

10. **[#21876](https://github.com/openai/codex/issues/21876) – `@chrome` routes to in-app browser instead of Chrome extension**  
    *4 comments, 0 👍*  
    Fresh issue: explicit `@chrome` mention doesn’t reliably use the Chrome extension backend on Windows, leading to false auth failures.

## Key PR Progress
Notable pull requests updated in the last 24h:

1. **[#21891](https://github.com/openai/codex/pull/21891) | [1/3] Pin Python SDK runtime dependency**  
   Part of a stack to declare exact runtime package in the Python SDK, ensuring reproducible builds.

2. **[#21893](https://github.com/openai/codex/pull/21893) | [2/3] Generate Python SDK types from pinned runtime**  
   Auto-generates API types from the pinned runtime, reducing manual drift.

3. **[#21895](https://github.com/openai/codex/pull/21895) | [3/3] Run Python SDK tests in CI**  
   Enables online testing for the Python SDK after dependency pinning.

4. **[#18202](https://github.com/openai/codex/pull/18202) | feat(sandbox): add Windows deny-read parity**  
   Extends split filesystem policy enforcement to Windows, matching macOS/Linux `access = none` behavior.

5. **[#19506](https://github.com/openai/codex/pull/19506) | Refresh AGENTS.md on cwd changes**  
   Closed as merged – now dynamically reloads project instructions when the working directory changes, solving a long-standing complaint.

6. **[#19377](https://github.com/openai/codex/pull/19377) | feat: separate `session_id` and `thread_id` in Responses requests**  
   Enables multi-agent v2 threads to differentiate session-level and thread-level identities.

7. **[#21812](https://github.com/openai/codex/pull/21812) | Publish Python runtime wheels on release**  
   Automates delivery of platform-specific binaries for Python SDK users.

8. **[#21875](https://github.com/openai/codex/pull/21875) | [codex] compact network context rendering**  
   Reduces prompt overhead by consolidating allowed/denied domains into a compact representation.

9. **[#21870](https://github.com/openai/codex/pull/21870) | Avoid blocking TUI on agent metadata hydration**  
   Fixes [#16688](https://github.com/openai/codex/issues/16688) – prevents TUI hang during large subagent fan-outs by making metadata reads asynchronous.

10. **[#21854](https://github.com/openai/codex/pull/21854) | fix: preserve empty JSON schemas for tool parameters**  
    Corrects sanitizer that incorrectly narrowed `{}` to `string`, which broke MCP tools with unconstrained parameters.

## Feature Request Trends
The top community-requested feature directions, distilled from open enhancement issues:

- **Sandbox capabilities** – GPU access ([#3141](https://github.com/openai/codex/issues/3141)), writable `.git` directories ([#14338](https://github.com/openai/codex/issues/14338)), and finer policy control.
- **Dynamic context loading** – On-demand `AGENTS.md` for subdirectories ([#12115](https://github.com/openai/codex/issues/12115)), similar to Claude Code.
- **UI and workflow improvements** – Tabbed parallel chat sessions ([#12098](https://github.com/openai/codex/issues/12098)), a file tree/directory viewer in the desktop app ([#13646](https://github.com/openai/codex/issues/13646)), and more reliable file tree toggling.
- **Goals & audit reliability** – Users love the Goals feature but need guarantees that goals persist through compaction ([#19910](https://github.com/openai/codex/issues/19910)).
- **Cross-platform parity** – Windows users consistently request feature parity with macOS/Linux, especially in sandbox policies and browser automation.

## Developer Pain Points
Recurring frustrations visible in the issue tracker:

- **Sandbox restrictions** – GPU access denial, MCP approval spam, and suspicion of unauthorized data scanning (e.g., [#21529](https://github.com/openai/codex/issues/21529)).
- **Windows instability** – Chrome plugin hangs, scroll issues, token refresh errors, and OS error 5 during plugin uninstall.
- **Performance and responsiveness** – Slow model responses ([#21527](https://github.com/openai/codex/issues/21527)) and TUI flickering in Emacs.
- **Auth and session management** – Stale refresh tokens ([#6498](https://github.com/openai/codex/issues/6498)), Safari callback blocks ([#10989](https://github.com/openai/codex/issues/10989)), and TUI bootstrapping failures.
- **Compaction and context loss** – Mid-turn compaction losing goals or causing API errors is a high-priority pain point (see [#19910](https://github.com/openai/codex/issues/19910) and [#21671](https://github.com/openai/codex/issues/21671)).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-09

## Today's Highlights
A burst of community activity continues around agent reliability and security hardening. The most-discussed issue remains the false "hand icon" blocking indicator (#21925), which has persisted unresolved for two months. Meanwhile, three PRs addressing defensive techniques — HITL bypass prevention (#23333), RAG injection sandboxing (#25190), and keychain error sanitization (#26322) — are advancing through review, signaling a strong security-focused development cycle.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#21925 — Hand icon shown when no action required](https://github.com/google-gemini/gemini-cli/issues/21925)**  
   *16 comments, open 2 months*  
   The leading pain point: Gemini CLI incorrectly displays a "waiting for input" indicator during long-running shell scripts. Community members report this is highly disruptive for headless/CI workflows. Marked as `possible-duplicate` but receiving sustained attention.

2. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *7 comments, EPIC*  
   A structural investigation into whether AST-aware tools can reduce token usage and misaligned reads. This EPIC could reshape how the agent understands codebases, potentially reducing tool call counts by 30-50%.

3. **[#22323 — Subagent MAX_TURNS falsely reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *6 comments, 2 👍*  
   Critical bug: the `codebase_investigator` subagent reports success even after hitting max turns without performing any analysis. This masks agent failures and misleads users about task completion.

4. **[#25166 — Shell command stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *3 comments, 3 👍*  
   High agreement: after executing simple CLI commands, Gemini hangs while displaying the shell as active. Reproducible with trivial commands that cannot possibly await user input.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *6 comments*  
   Purely anecdotal but widely resonated: even with well-described custom skills, Gemini rarely invokes them autonomously. Community wants the agent to be more proactive with available tools.

6. **[#22093 — Subagents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)**  
   *2 comments*  
   Security concern: users who disabled agents in all configs report subagents activating post-update. Indicates a potential regression in configuration enforcement.

7. **[#26563 — "save_memory" tool not found](https://github.com/google-gemini/gemini-cli/issues/26563)**  
   *5 comments, opened 3 days ago*  
   Recent regression: `/memory add` command fails with "Tool 'save_memory' not found" on v0.41.1. Suggests a missing tool registration in the latest release.

8. **[#24916 — Repeated permission prompts on same file](https://github.com/google-gemini/gemini-cli/issues/24916)**  
   *4 comments*  
   "Allow for all future sessions" doesn't persist. Permission state is lost, causing friction in multi-step workflows.

9. **[#22232 — Enhance browser_agent resilience](https://github.com/google-gemini/gemini-cli/issues/22232)**  
   *3 comments*  
   Feature request for automatic session takeover and lock recovery in BrowserManager. Current fail-fast strategy is too aggressive for persistent sessions.

10. **[#23571 — Temp scripts created in random locations](https://github.com/google-gemini/gemini-cli/issues/23571)**  
    *3 comments*  
    When restricted to shell execution, the model scatters edit scripts across directories, creating cleanup overhead. Community desires centralized temp file management.

## Key PR Progress
1. **[#23333 — HITL Bypass via Newline Injection (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/23333)**  
   Fixes a critical security vulnerability where malicious repos could use vertical newline padding to hide commands from user confirmation. Merged.

2. **[#25947 — Versioned pre-write backups with agent-driven restore (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/25947)**  
   Introduces session-scoped transactional file backups. Mitigates "destructive modification loops" by enabling file reversion after botched `write_file` calls. Merged.

3. **[#23543 — Tool execution performance metrics](https://github.com/google-gemini/gemini-cli/pull/23543)**  
   Wires up `recordToolExecutionBreakdown` histogram in the telemetry pipeline. Foundation for AI-driven tool optimization.

4. **[#26657 — Fix JavaScript heap OOM with streaming fs.opendir](https://github.com/google-gemini/gemini-cli/pull/26657)**  
   Replaces synchronous file listing with streaming `fs.opendir` in shell completion hook. Addresses memory exhaustion on large directories.

5. **[#26420 — Ignore GOOGLE_CLOUD_PROJECT for LOGIN_WITH_GOOGLE](https://github.com/google-gemini/gemini-cli/pull/26420)**  
   Fixes 403 errors when `GOOGLE_CLOUD_PROJECT` env var conflicts with Code Assist auth flow. Simple but impactful for enterprise users.

6. **[#24320 — Ctrl+C abort for web_fetch](https://github.com/google-gemini/gemini-cli/pull/24320)**  
   Previously, interrupting a URL fetch triggered 3 silent retries with ~35s total backoff. Now cancels immediately on Ctrl+C.

7. **[#25190 — RAG Defense validation sandbox](https://github.com/google-gemini/gemini-cli/pull/25190)**  
   Adds sanitization logic to detect and block prompt injections in retrieved context before it reaches the LLM.

8. **[#25915 — Route /compress through local Ollama model (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/25915)**  
   Enables offloading summarization to local models (e.g., Gemma 3:4b) for privacy and cost savings. Plain-text only, with full sanitization.

9. **[#25912 — Compact tool output for MCP tools (CLOSED)](https://github.com/google-gemini/gemini-cli/pull/25912)**  
   Extends `compactToolOutput` to MCP tools. Previously only applied to native tools; now MCP outputs are also condensed by default.

10. **[#26358 — Exit shell mode with backspace on empty input](https://github.com/google-gemini/gemini-cli/pull/26358)**  
    Small UX improvement: pressing backspace on an empty line in `!` shell mode now deactivates it, matching intuitive expectations.

## Feature Request Trends
- **AST-aware code navigation**: Multiple issues (#22745, #22746) propose replacing line-based file reads with method/class-level AST-aware reads to reduce tokens and improve precision.
- **Autonomous skill utilization**: Community wants the agent to proactively invoke configured skills and sub-agents without explicit instruction (#21968).
- **Browser agent resilience**: Demand for persistent session management, lock recovery, and config override support (#22232, #22267).
- **Memory system improvements**: Auto-memory extraction, deduplication, and retry limits are hot topics (#26522, #26523, #26516). Users want more reliable, less noisy memory persistence.
- **UI/UX polish**: Tracker/task renaming, collapsible tool call summaries, and better parallel call grouping (#22203, #23126, #24943) indicate a push toward cleaner terminal output.
- **Enterprise and security hardening**: Deterministic redaction, quota project injection, and permission state persistence are recurring themes (#26525, #24916, #26698).

## Developer Pain Points
1. **False-positive blocking indicators**: The hand icon (#21925) and stuck "Waiting input" state (#25166) are the most upvoted irritants, undermining trust in the agent's status reporting.
2. **Subagent reliability**: Masked failures (#22323), unauthorized activation (#22093), and ignoring config overrides (#22267) create unpredictability in multi-agent workflows.
3. **Permission model inconsistences**: Repeated prompts for the same file (#24916) and permission persistence failures disrupt fluid coding sessions.
4. **Cleanup overhead**: Temp scripts scattered across filesystem (#23571) and inability to remove workspace directories (#26179) increase manual housekeeping.
5. **Tool availability regressions**: Recent release v0.41.1 missing `save_memory` (#26563) and the >128 tools 400 error (#24246) suggest tool registration stability issues.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-05-09

## Today’s Highlights
Two rapid‑fire releases (v1.0.44 and v1.0.44‑3) landed yesterday, addressing input flicker, mid‑input slash commands, and a new hook that can bypass the LLM entirely. Meanwhile, the community is closely watching a critical bug where custom agents configured with MCP servers lose tool connectivity in sub‑agent or `--prompt` contexts, and a silent crash in non‑interactive mode on macOS.

## Releases
- **[v1.0.44](https://github.com/github/copilot-cli/releases/tag/v1.0.44)** (2026-05-08)  
  - Path completion in `/add-dir` no longer flickers or conflicts with `@` and `#` pickers.  
  - Slash commands can now appear mid‑input; multiple skills can be invoked in a single message.  
  - `userPromptSubmitted` hooks can handle requests directly, bypassing the LLM.

- **[v1.0.44-3](https://github.com/github/copilot-cli/releases/tag/v1.0.44-3)** (2026-05-08)  
  - Added: `userPromptSubmitted` hooks now return responses without making a model call.  
  - Improved: Faster `/user list` and `/user switch` for multi‑account users.

## Hot Issues (10 selected)
1. [#2630 – Custom agent MCP servers not connected in sub‑agent or `--prompt` contexts](https://github.com/github/copilot-cli/issues/2630)  
   *Open, 6 comments* – Agents defined with `mcp-servers` in YAML frontmatter lose tool access when invoked via `task` or `--prompt`. This blocks MCP‑dependent workflows. Community has noted it for nearly a month; no fix yet.

2. [#1412 – PowerShell tools trigger security alerts on Windows](https://github.com/github/copilot-cli/issues/1412)  
   *Open, 3 comments* – Elastic detects Copilot CLI’s PowerShell usage as malicious activity. Users face internal SOC investigations. High reaction count (👍3) indicates broad impact.

3. [#1433 – `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` not working across NFS](https://github.com/github/copilot-cli/issues/1433)  
   *Open, 3 comments* – Custom AGENTS.md files on network drives are ignored. The environment variable is accepted but not resolved. Affects Linux users with shared home directories.

4. [#3189 – `copilot -p` exits silently with code 1 on macOS (v1.0.44-1)](https://github.com/github/copilot-cli/issues/3189)  
   *Open, 3 comments* – Non‑interactive mode produces zero output and leaves no log file. Interactive (`-i`) works fine, pointing to a regression in the prompt mode.

5. [#3200 – `/delegate` without committing local changes](https://github.com/github/copilot-cli/issues/3200)  
   *Open, 3 comments* – Users want a way to delegate tasks without forcing a commit+push. A `uncommitted` subcommand is proposed.

6. [#3195 – Reasoning events not triggered from BYOK providers](https://github.com/github/copilot-cli/issues/3195)  
   *Open, 2 comments* – When using vLLM via BYOK, `AssistantReasoningEvent` is never fired because the CLI only checks `reasoning_content`, not the `reasoning` field. Blocks reasoning‑aware integrations.

7. [#3049 – Failure to write to file when asked to plan without code changes](https://github.com/github/copilot-cli/issues/3049)  
   *Open, 2 comments* – Consistent permission errors when agent is told to create a plan but not make changes. Likely a tool‑permission logic issue.

8. [#3098 – PowerShell `$home` variable footgun can mutate/delete user profile](https://github.com/github/copilot-cli/issues/3098)  
   *Open, 1 comment* – Generated scripts that use `$home` as a scratch path inadvertently resolve to `$HOME`, causing destructive `Remove-Item` calls. A critical safety concern on Windows.

9. [#3208 – BYOK Azure: `wire_api: completions` ignored; hardcoded `api-version` rejected](https://github.com/github/copilot-cli/issues/3208)  
   *Open, 1 comment* – CLI ignores the `wire_api` config and forces the Responses API, and uses a hardcoded `api-version` that Azure rejects. Blocks enterprise Azure deployments.

10. [#3205 – Emoji table column misalignment regression (v1.0.43)](https://github.com/github/copilot-cli/issues/3205)  
    *Open, 0 comments* – #2764 was marked fixed but emoji tables still break, with extra pipes and shifted columns. Affects readability of structured output.

## Key PR Progress
Only two pull requests were updated in the last 24 hours:

- **[#2800 – Add initial devcontainer configuration](https://github.com/github/copilot-cli/pull/2800)** (Open)  
  Provides a `.devcontainer` setup for contributors. Low activity but useful for onboarding.

- **[#3199 – Update Homebrew installation commands](https://github.com/github/copilot-cli/pull/3199)** (Open)  
  Updates documentation to point to new Homebrew cask locations (`copilot-cli` and `copilot-cli@prerelease`).

## Feature Request Trends
- **Delegation improvements**: Users want `/delegate` to work without forcing a commit (#3200) and to support uncommitted changes.
- **Timeline search**: Several requests for searching command history (like tmux `ctrl-b [`) (#2170).
- **Custom agent hooks**: Demand for a `preAgentStop` hook (#2253) and more granular lifecycle hooks.
- **External model providers**: Clarification and API surface for configuring BYOK providers (#2710), including Azure and vLLM parity.
- **Windows editor support**: Support for `.bat`/`.cmd` scripts as `$EDITOR` (#1882).
- **MCP server governance**: Enterprise users want to restrict which MCP servers extensions can install (#3207).

## Developer Pain Points
- **Silent failures**: Non‑interactive mode (`-p`) crashes without output or logs (#3189) – a major trust issue for CI pipelines.
- **Security false positives**: PowerShell tools repeatedly trigger security alerts (#1412), forcing developers to fight their own IT.
- **BYOK / provider quirks**: Reasoning events not firing (#3195) and Azure `wire_api` being ignored (#3208) frustrate self‑hosted deployments.
- **MCP connectivity gaps**: Custom agents lose tool access in sub‑agent contexts (#2630), breaking complex workflows.
- **Terminal rendering regressions**: Emoji table alignment (#3205) and markdown link breakage (#3204) degrade readability.
- **Permission footguns**: Accidental profile deletion via `$home` in PowerShell (#3098) and misleading download prompts (#3213) raise safety concerns.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the Kimi Code CLI community digest for 2026-05-09, based on the provided GitHub data.

---

## Kimi Code CLI Community Digest — 2026-05-09

### 1. Today's Highlights

The community is heavily focused on improving the Windows experience, with a major PR proposing a switch from PowerShell to git-bash to resolve persistent compatibility issues. A series of bug reports highlight critical problems like session corruption from malformed tool calls and a phantom `fcntl` crash on Windows, while a coordinated set of PRs aims to stabilize the shell tool's timeout behavior and subprocess handling. The WebUI also received a targeted fix for long filenames hiding sidebar action buttons.

### 2. Releases

No new versions of the Kimi Code CLI were released in the last 24 hours. The latest stable version remains **v1.41.0**.

### 3. Hot Issues

Here are the 10 most noteworthy issues from the last 24 hours:

1.  **#2152: Support global `~/.kimi/AGENTS.md` for multi-project shared conventions**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2152)
    *   **Why it matters:** This is a high-impact feature request for developers managing many projects. Currently, AGENTS.md is only local, forcing users to duplicate shared conventions.
    *   **Community reaction:** Positive, receiving 2 upvotes and 3 comments, suggesting broad interest in a global configuration layer.

2.  **#2165: Invalid tool call corrupts the whole session**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2165)
    *   **Why it matters:** A critical bug that makes a conversation permanently unusable after a single bad model output. This is a severe workflow blocker.
    *   **Community reaction:** Confirmed by a user running a local vllm deployment. It has an associated fix in PR #2196.

3.  **#2189: Plan mode produces garbled characters on next interaction**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2189)
    *   **Why it matters:** A recent regression that breaks the Plan mode workflow on Windows after one use, indicating a state-cleaning issue.
    *   **Community reaction:** Reported by a single user, likely a new issue stemming from a recent release.

4.  **#2202: `kimi term` crashes on Windows due to missing `fcntl` module**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2202)
    *   **Why it matters:** A critical platform-specific crash for Windows users trying to use the terminal mode. The issue also reveals a poor error handling path that triggers a secondary renderer error.
    *   **Community reaction:** This is a strong signal that Windows portability requires more testing.

5.  **#2191: StrReplaceFile silently converts entire file from CRLF to LF on Windows**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2191)
    *   **Why it matters:** A major source of friction for Windows developers. The Agent's tool silently breaks line endings, forcing users to abandon it for Python workarounds.
    *   **Community reaction:** The user notes a related fix PR (#1953) is still unmerged, highlighting a known and unaddressed pain point.

6.  **#2194: Agent generates PowerShell 7.x syntax incompatible with default PowerShell 5.x**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2194)
    *   **Why it matters:** The Agent is generating code that fails on the default Windows environment, breaking the core promise of an automated "code" CLI.
    *   **Community reaction:** Similar to #2192, this is a systemic Windows problem being addressed by the "switch to git-bash" PR (#2186).

7.  **#2197: Windows console TrueType font reset when running subprocess via `kaos.exec()`**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2197)
    *   **Why it matters:** A UI/UX polish issue that causes the terminal to visually stutter during subprocess execution. Related to PR #2199.
    *   **Community reaction:** A minor but noticeable bug for Windows users.

8.  **#2195: Command timeout is rigid (60s) and not configurable**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2195)
    *   **Why it matters:** The Agent frequently fails to complete long-running tasks (e.g., builds, `git clone`) due to a hard-coded timeout, requiring manual intervention.
    *   **Community reaction:** Supported by the related PR #2200, which introduces adaptive timeouts.

9.  **#2204: `/clear` rotates context file but provides no way to restore it**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2204)
    *   **Why it matters:** A confusing UX gap. The command preserves data on disk but offers no command to resume from that backup, making the feature feel incomplete.
    *   **Community reaction:** A new submission with clear problem description, suggesting a missing feature in the session management loop.

10. **#2203: `AuthlibDeprecationWarning` printed on every startup**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/issues/2203)
    *   **Why it matters:** While not a crash, spammy warnings degrade the developer experience and may indicate an upcoming breaking change in dependencies.
    *   **Community reaction:** Reported in context of MCP server configuration. This is a low-priority but annoying issue.

### 4. Key PR Progress

Here are the 10 most important pull requests updated or created in the last 24 hours:

1.  **#2186: Switch Shell backend from PowerShell to git-bash (Windows)**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2186)
    *   **Why it matters:** A significant architectural change aiming to solve all the Windows POSIX-syntax issues. This is the most impactful PR of the day.
    *   **Status:** Open.

2.  **#2177: Clear partial UI output when LLM step is retried**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2177)
    *   **Why it matters:** Fixes a visual glitch where failed and retried agent steps would concatenate their output, causing confusion.
    *   **Status:** Open.

3.  **#2200: Adapt shell timeouts for long commands**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2200)
    *   **Why it matters:** Directly addresses the "rigid timeout" pain point (#2195) by extending timeouts for known slow patterns like `git clone` and package installs.
    *   **Status:** Open.

4.  **#2199: Avoid console windows on Windows `exec`**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2199)
    *   **Why it matters:** Fixes the flashing console window and font reset issue (#2197) during subprocess execution on Windows.
    *   **Status:** Open.

5.  **#2196: Sanitize malformed history tool calls**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2196)
    *   **Why it matters:** Fixes the session-corrupting bug (#2165) where a history of invalid JSON from the model could block all future turns.
    *   **Status:** Open.

6.  **#2207: Prevent long filenames from hiding action buttons in WebUI sidebar**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2207)
    *   **Why it matters:** A targeted UI fix for a common annoyance in the WebUI, where files with long names become unusable.
    *   **Status:** Open.

7.  **#2187: Bump pillow to 12.2.0 for CVE-2026-25990**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2187)
    *   **Why it matters:** A security patch to address a high-severity vulnerability, which is blocking installation in security-constrained environments.
    *   **Status:** Open.

8.  **#2183: Attach dropped image paths eagerly**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2183)
    *   **Why it matters:** Prevents a race condition where image paths from drag-and-drop would become stale before the agent could read them.
    *   **Status:** Open.

9.  **#1972: Visual context progress bar with color coding**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/1972)
    *   **Why it matters:** A quality-of-life UI enhancement that replaces a plain text percentage with a color-coded Unicode bar, making context usage easier to monitor.
    *   **Status:** Open (Updated).

10. **#2205: Register `/btw` slash command**
    *   [Link](https://github.com/MoonshotAI/kimi-cli/pull/2205)
    *   **Why it matters:** Fixes a bug where an already documented and handled feature was not available as a slash command, breaking discoverability.
    *   **Status:** Open.

### 5. Feature Request Trends

The dominant feature request themes from the last 24 hours are:

- **Multi-Project Global Configuration:** Users are asking for a way to define agent rules once, rather than copy-pasting `AGENTS.md` into every project directory (#2152).
- **Windows Environment Parity:** A strong push to make the CLI fully native on Windows, moving away from reliance on PowerShell for shell commands (#2186 context) and fixing file encoding issues (#2191).
- **Shell Tool Intelligence:** Developers want the shell tool to be smarter—with configurable and adaptive timeouts (#2195), and the ability to restore or continue from rotated context backups (#2204).
- **UI/UX Polish:** There is continuous interest in improving the terminal and WebUI, including progress bars (#2188), sidebar layout fixes (#2206), and eliminating startup warnings (#2203).

### 6. Developer Pain Points

Recurring developer frustrations from the past week are:

- **Windows is a Second-Class Citizen:** Multiple issues point to a broken experience on Windows. The Agent generates Unix/pwsh7 commands that fail on default pwsh5 (#2192, #2194), text encoding is silently corrupted (#2191), and core features crash outright (#2202, #2197).
- **Shell Tool Rigidity:** The Agent's shell tool has a fixed 60-second timeout (#2195) and can permanently stop processing background tasks after 3 consecutive LLM errors (#2193). This makes it unreliable for real-world development tasks.
- **Session State Management:** The `clear` command is destructive without a restore option (#2204), and a single bad model output can irreparably corrupt a session (#2165). This creates high risk for developers in long-running conversations.
- **Plugin/Extension Friction:** The blank `FileVersionInfo` on Windows executables (#2178) and the `AuthlibDeprecationWarning` when using MCP servers (#2203) show friction in the tooling and plugin ecosystem.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-09

## 1. Today's Highlights

Today's activity centers on session management reliability and longstanding UX gaps. A critical bug report surfaced where the `opencode` CLI can disappear after an upgrade due to install-method misdetection ([#26473](https://github.com/anomalyco/opencode/issues/26473)), while a fresh PR aims to fix double compaction after auto-compaction ([#26484](https://github.com/anomalyco/opencode/pull/26484)). The community continues to rally around the “YOLO mode” feature request ([#8463](https://github.com/anomalyco/opencode/issues/8463), 44 👍), and the session-picker limit—an issue that reappears across multiple threads—remains a hot topic.

## 2. Releases

No new releases in the last 24 hours.

## 3. Hot Issues

Ten issues that deserve attention, ranked by community engagement and impact:

1. **[[FEATURE]: GitHub-based Agent Marketplace for Sharing and Discovering Agents](https://github.com/anomalyco/opencode/issues/7467)** (#7467, 14 comments, 8 👍)  
   A far-reaching proposal to create a discoverable registry for agents. Many users struggle with agent portability across teams; this marketplace would dramatically reduce friction and foster a shared agent ecosystem.

2. **[Compaction replay injects fake user message "What did we do so far?"](https://github.com/anomalyco/opencode/issues/13838)** (#13838, 11 comments, 3 👍)  
   A clear and well-reproduced bug: after `/compact`, resuming a session inserts a synthetic user query, causing the model to generate an unwanted summary. This undermines the core promise of compaction—saving context without noise—and has been open since February.

3. **[[FEATURE]: Add `--dangerously-skip-permissions` (aka YOLO mode)](https://github.com/anomalyco/opencode/issues/8463)** (#8463, 7 comments, 44 👍)  
   The most upvoted open feature. Users in automated or trusted environments want the ability to bypass permission prompts entirely. The high reaction count signals strong demand, though security concerns keep the discussion nuanced.

4. **[Tool execution aborted/terminated](https://github.com/anomalyco/opencode/issues/26063)** (#26063, 7 comments, 0 👍)  
   A frustrating bug with local LM Studio models (Qwen3.6-35b-A3B) where tool execution randomly aborts. The reporter provided environment details, making this actionable for maintainers. Local model compatibility continues to be a pain point.

5. **[TUI /sessions picker only shows recent sessions](https://github.com/anomalyco/opencode/issues/13877)** (#13877, 7 comments, 1 👍)  
   Duplicated by [issue #16270](https://github.com/anomalyco/opencode/issues/16270) and [issue #20754](https://github.com/anomalyco/opencode/issues/20754). The TUI session picker has a hard-coded 30-day window, hiding older conversations. Users with hundreds of sessions find this extremely limiting. A pending PR (#6138) proposes a configurable limit.

6. **[/skill-name doesn’t invoke full skill system](https://github.com/anomalyco/opencode/issues/24831)** (#24831, 5 comments, 0 👍)  
   Using `/skill-name` only copies the base prompt without invoking the full skill pipeline, meaning referenced files and context are missing. This breaks the core skill workflow for advanced users.

7. **[Desktop app shell tool uses minimal PATH while CLI preserves zsh PATH](https://github.com/anomalyco/opencode/issues/26321)** (#26321, 4 comments, 2 👍)  
   On macOS, the Desktop app’s shell tool sees only `/usr/bin:/bin:/usr/sbin:/sbin`, while the CLI inherits the full zsh PATH. This breaks Homebrew tools and any setup relying on shell init files—a significant obstacle for Desktop users.

8. **[setCacheKey sends promptCacheKey instead of cache_control for Bedrock proxies](https://github.com/anomalyco/opencode/issues/25984)** (#25984, 4 comments, 0 👍)  
   A niche but important interoperability issue: when using `@ai-sdk/openai-compatible` with Bedrock proxies (Bifrost, LiteLLM), OpenCode sends `promptCacheKey` which proxies ignore. This prevents prompt caching on AWS, wasting tokens.

9. **[最新版犹如狗屎 (Latest version is like dogshit)](https://github.com/anomalyco/opencode/issues/25827)** (#25827, 3 comments, 0 👍)  
   While the title is blunt, the substance is real: recent UI changes removed refresh and session-deletion options from the web UI. The reporter notes Ctrl+R still works, but the UX regression is clear. This highlights the tension between simplification and power-user needs.

10. **[opencode command disappears after first run due to install-method misdetection](https://github.com/anomalyco/opencode/issues/26473)** (#26473, 2 comments, 0 👍)  
    A brand-new, high-severity issue: the auto-upgrader can infer the wrong installation method from `process.execPath`, potentially leaving the CLI entirely unavailable after a first run. This could affect many users silently.

## 4. Key PR Progress

Ten important PRs that advanced or were updated today:

1. **[fix(session): prevent double compaction after auto-compact](https://github.com/anomalyco/opencode/pull/26484)** (#26484)  
   Resolves two related issues (#26230, #20621). After auto-compaction, stale token counts were retained, causing misleading context-size displays. A clean fix for a confusing UX bug.

2. **[feat(app): Mobile Touch Optimization](https://github.com/anomalyco/opencode/pull/18767)** (#18767)  
   A comprehensive mobile experience overhaul—touch targets, gesture support, responsive layout—without breaking desktop behavior. Still open, but marks a strategic push toward mobile usability.

3. **[chore(i18n): complete Chinese translation for zh.ts files](https://github.com/anomalyco/opencode/pull/25800)** (#25800)  
   Completes Simplified Chinese localization across three modules (app, ui, desktop). Important for the large Chinese-speaking community and a sign of growing internationalization investment.

4. **[feat(todo): auto-cleanup stale todos + /clear-tasks commands](https://github.com/anomalyco/opencode/pull/25856)** (#25856)  
   Addresses a common pain point: stale todo items accumulating across conversations. Adds `/clear-tasks` and `/清除任务` commands, plus automatic cleanup heuristics.

5. **[fix(nix): remove OPENCODE_CHANNEL=local to restore stable backend](https://github.com/anomalyco/opencode/pull/26476)** (#26476)  
   A targeted fix for NixOS users where the `"local"` channel caused backend instability. Closes #25790.

6. **[feat(permission): extract inner commands from wrappers for permission matching](https://github.com/anomalyco/opencode/pull/16724)** (#16724)  
   Closes #9516. Now permission rules like `"gh api* -X DELETE"` will match even when wrapped in `xargs`, `parallel`, `timeout`, or `sudo`. A smart improvement to the permission system.

7. **[fix(opencode): unbounded memory growth during active usage](https://github.com/anomalyco/opencode/pull/16346)** (#16346)  
   Fixes #13230 and related memory leaks. Virtual memory was increasing without bound during active sessions—a critical stability fix for long-running users.

8. **[feat(tui): group timeline messages by date](https://github.com/anomalyco/opencode/pull/15606)** (#15606)  
   Closes #15376. The TUI timeline now groups messages under date headers (“Today”, “Yesterday”, etc.), making long conversations navigable.

9. **[fix: use StringDecoder for stdout/stderr to prevent UTF-8 corruption](https://github.com/anomalyco/opencode/pull/15387)** (#15387)  
   Fixes #15385. Assembling stdout with `chunk.toString()` can split multi-byte UTF-8 characters, causing garbled output. This PR adds proper stream decoding—a subtle but important correctness fix.

10. **[feat: add api shape field to allow distinction between api formats beyond sdk type](https://github.com/anomalyco/opencode/pull/14487)** (#14487)  
    Introduces a `shape = completions | responses` field in provider config, enabling models (e.g., Azure) that only support the completions API to be correctly routed. A structural improvement for provider extensibility.

## 5. Feature Request Trends

Several clear themes emerge from recent issues:

- **Agent Ecosystem & Sharing**: The top-voted feature (#7467) proposes a GitHub-based Agent Marketplace. Users want to discover, publish, and reuse agents without manual file transfer. This is the most ambitious request on the board.

- **Session History Navigation**: At least three distinct issues (#13877, #16270, #20754) ask for configurable limits or page-based browsing in the session picker. Users with hundreds of sessions find the default 30-day window and 5-item cap unusable.

- **Skill System Completeness**: Issue #24831 reveals a gap where `/skill-name` doesn’t invoke the full skill pipeline. Users expect skills to include referenced files, not just the base prompt—suggesting a desire for richer, composable skill definitions.

- **Safety vs. Speed**: The YOLO mode request (#8463, 44 👍) and the inner-command permission extraction PR (#16724) represent two poles: one asks for fewer guardrails, the other for smarter guardrails. The community clearly wants both—configurable safety levels.

## 6. Developer Pain Points

Recurring frustrations that affect daily workflows:

- **Session Picker Limitations**: The TUI picker’s 30-day hard-coded limit frustrates power users. Several duplicates and a related PR (#6138) underline how much this small UX detail matters.

- **Configuration & Environment Friction**:  
  - Desktop app PATH mismatch with zsh ([#26321](https://github.com/anomalyco/opencode/issues/26321)) breaks Homebrew tools.  
  - WSL UNC path access fails on Windows ([#26481](https://github.com/anomalyco/opencode/issues/26481)).  
  - Web UI not accessible via network IP ([#15273](https://github.com/anomalyco/opencode/issues/15273)).  
  These point to inconsistent environment handling across platforms.

- **Local Model Compatibility**: The LM Studio tool-execution-abort bug ([#26063](https://github.com/anomalyco/opencode/issues/26063)) and the Kiro provider crash ([#26221](https://github.com/anomalyco/opencode/issues/26221)) show that local/third-party model support remains fragile.

- **Upgrade & Installation Stability**: The upgrade-disappears-the-CLI bug ([#26473](https://github.com/anomalyco/opencode/issues/26473)) and the plugin auto-install confusion ([#26462](https://github.com/anomalyco/opencode/issues/26462)) suggest that lifecycle management still has rough edges.

- **Windows Path Handling**: Sessions missing from the sidebar due to `\` vs `/` mismatches ([#23864](https://github.com/anomalyco/opencode/issues/23864)) is a classic cross-platform headache that has persisted for weeks.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-09

## Today’s Highlights
A major refactor (labelled as "bigrefactor") continues to sweep through the codebase, closing many open issues and PRs as out-of-scope or superseded. Among the most important changes today: a new `--mode worker-loop` for bus-driven task dispatch, support for Cmd+V image paste in the TUI, and fixes for API key leakage to non-Anthropic endpoints. Several terminal compatibility and crash bugs remain open, with the community pushing for better narrow-terminal handling and virtual scrollback.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 noteworthy)

1. **#3929 — Bun startup crash when `bun pm bin -g` fails**  
   *Why it matters:* A regression that crashes Pi on startup for Bun users who lack `~/.bun/install/global/package.json`. Follow-up to earlier fixes for `bun root -g`. 9 comments, 3 👍.  
   [GitHub](https://github.com/earendil-works/pi/issues/3929)

2. **#4185 — Zsh/tmux installation – bad colors/contrast**  
   *Why it matters:* New users on tmux see broken colors immediately – a first-impression blocker. 8 comments, 1 👍.  
   [GitHub](https://github.com/earendil-works/pi/issues/4185)

3. **#2616 — SessionManager is sync-only; blocks async/database-backed persistence**  
   *Why it matters:* Architectural debt forces blocking I/O in the session manager, preventing non-trivial persistence backends. 5 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/2616)

4. **#3978 — `pi config` hardcodes `~/.pi/agent/` path in group label**  
   *Why it matters:* Misleading UI – skills from custom directories appear under the wrong group. Closed by PR #4299. 4 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/3978)

5. **#4317 — Persist timing metadata for assistant message parts**  
   *Why it matters:* Enables per-part timestamps (thinking, text, tool_call) for analytics and progress displays. 3 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/4317)

6. **#4302 — TUI crashes on over-wide changed line in narrow terminal**  
   *Why it matters:* Pi can crash silently in narrow tmux panes – a critical UX bug for users with cramped layouts. 3 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/4302)

7. **#4313 — Limit rendered message history in TUI (virtual scrollback)**  
   *Why it matters:* Long sessions become unusable without virtual scrolling. Highly requested performance improvement. 3 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/4313)

8. **#4323 — Wezterm with `enable_kitty_keyboard` breaks Esc key**  
   *Why it matters:* Regression affecting Wezterm users with advanced keyboard protocol enabled. 1 comment, opened today.  
   [GitHub](https://github.com/earendil-works/pi/issues/4323)

9. **#4290 — Messages aborted for length treated as regular stops**  
   *Why it matters:* Confusing UX – users don’t realise a turn was truncated because the UI shows no error. 2 comments.  
   [GitHub](https://github.com/earendil-works/pi/issues/4290)

10. **#4266 — Using LM Studio fails with HTTP 400 for `tool_choice`**  
    *Why it matters:* Blocks all local OpenAI-compatible servers that only accept string `tool_choice`. 2 comments.  
    [GitHub](https://github.com/earendil-works/pi/issues/4266)

## Key PR Progress (10 important)

1. **#4329 – feat(coding-agent): add `--mode worker-loop` for bus-driven task dispatch**  
   *What it does:* Enables Pi to run as a Unix-socket worker that processes task requests from a host process – the foundation for scalable background agents.  
   [GitHub](https://github.com/earendil-works/pi/pull/4329)

2. **#4339 – fix: prevent `ANTHROPIC_AUTH_TOKEN` env var from leaking into non-Anthropic API key requests**  
   *What it does:* Stops the Anthropic SDK from sending the `ANTHROPIC_AUTH_TOKEN` header when using a different provider, fixing 401 errors for proxy APIs.  
   [GitHub](https://github.com/earendil-works/pi/pull/4339)

3. **#4335 – Normalize Copilot API base URL by removing business subdomain**  
   *What it does:* Converts `proxy.business.githubcopilot.com` to `api.githubcopilot.com` so all Copilot tokens work with the standard endpoint.  
   [GitHub](https://github.com/earendil-works/pi/pull/4335)

4. **#4331 – feat: support Cmd+V image paste via empty bracketed paste detection**  
   *What it does:* Detects empty bracketed paste sequences (sent by terminals when pasting non-text content) and allows image upload from clipboard.  
   [GitHub](https://github.com/earendil-works/pi/pull/4331)

5. **#4327 – feat(tui): wrap list items with indent**  
   *What it does:* Improves readability of long lists in narrow terminals by wrapping lines with proper indentation and rendering quote tokens.  
   [GitHub](https://github.com/earendil-works/pi/pull/4327)

6. **#4299 – fix(coding-agent): preserve `.agents` provenance in skill metadata**  
   *What it does:* Fixes #3978 – properly tracks skill source directories so the UI shows correct group labels. Re‑opened after accidental fork deletion.  
   [GitHub](https://github.com/earendil-works/pi/pull/4299)

7. **#4320 – fix(zig): add Windows platform support**  
   *What it does:* Replaces POSIX-only calls with cross-platform alternatives, enabling the Zig implementation to compile and run on Windows with Zig 0.16.0.  
   [GitHub](https://github.com/earendil-works/pi/pull/4320)

8. **#3624 – feat(ai): add Together AI as a provider**  
   *What it does:* Adds native support for Together AI via the OpenAI-compatible API, including model discovery and default model selection.  
   [GitHub](https://github.com/earendil-works/pi/pull/3624)

9. **#3899 – fix(ai): update Antigravity UA to 1.107.0 to resolve 503 API errors**  
   *What it does:* Bumps the hardcoded user-agent string for Google's Cloud Code Assist API, which was rejecting older versions with 503 errors.  
   [GitHub](https://github.com/earendil-works/pi/pull/3899)

10. **#4318 – Moves changelog ack state out of settings.json and into local state.json**  
    *What it does:* Separates user‑editable settings from auto‑updated state, making `settings.json` safe for dotfile sharing. Introduces a new `StateManager` for persistent non‑config data.  
    [GitHub](https://github.com/earendil-works/pi/pull/4318)

## Feature Request Trends
- **Rich message metadata:** Multiple requests for per‑part timestamps (#4317) and per‑turn stop‑after‑turn control (#4291).
- **TUI performance and usability:** Virtual scrollback (#4313), configurable VCS status (#4292), and click‑handling for transcript rows (#4321) are recurring themes.
- **Provider and model expansion:** Native support for Together AI (#3624), Copilot internal models (#4293), and Grok 4.3 reasoning effort (#4308) reflect strong demand for broader model coverage.
- **Extension API improvements:** Requests for cursor position exposure (#4309) and extensible footer providers (#4262) show the community is building on Pi’s plugin system.

## Developer Pain Points
- **Terminal compatibility fragmentation:** Issues with Wezterm kitty keyboard (#4323), iTerm2 Alt‑key handling (#4298), and tmux color rendering (#4185) indicate that terminal quirks frequently break Pi’s TUI.
- **Narrow-terminal crashes:** Crashes when line width exceeds terminal width (#4302, #4313) are a top concern – users in small panes or side‑by‑side layouts hit these frequently.
- **API compatibility with local servers:** LM Studio and similar OpenAI‑compatible servers reject Pi’s object‑style `tool_choice` (#4266). Multiple issues also report problems with DeepSeek/Kimi tool schemas (#4310, #4312).
- **“Bigrefactor” closure pattern:** A large number of issues and PRs are being closed with the `closed-because-bigrefactor` or `closed-because-weekend` labels, signalling that the maintainers are aggressively scoping out contributions that don’t align with the current refactor. This can frustrate contributors who see their work closed without merger.
- **Blocking I/O in core data paths:** The sync‑only session manager (#2616) prevents anyone from implementing database‑backed persistence or async workflows without a major rewrite.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-05-09

## Today's Highlights

Today marks the release of **v0.15.9** with telemetry opt-in controls and per‑file AI commit attribution, alongside a **v0.16.10‑preview.0** that fixes the `/model` command and improves API request logging. Community attention is concentrated on authentication regressions (API keys not respected, connection errors), a critical bug where Qwen overwrites `settings.json` on startup, and growing demand for configurable plans directories. Several PRs are tackling terminal rendering flicker, narrow‑terminal support, and a major codebase indexing feature.

---

## Releases

- **[v0.15.9](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.9)** — stable release featuring:
  - **feat(telemetry):** sensitive span attribute opt‑in (#3893)
  - **feat:** commit attribution with per‑file AI contribution tracking
- **[v0.15.9-nightly.20260509](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.9-nightly.20260509.199c0e290)** — nightly containing the same fixes.
- **[v0.16.10-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.16.10-preview.0)** — preview release:
  - **fix(cli):** validate `/model <model-id>` arguments (#3963)
  - **fix(core):** log the actual OpenAI request sent on the wire (#tanzhenxin)
- **[v0.15.8-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.8-preview.0)** — earlier preview with same telemetry & commit attribution work.

---

## Hot Issues

1. **[#3877](https://github.com/QwenLM/qwen-code/issues/3877) — API key in `.env` not respected (OPEN, 4 comments)**  
   Users set `OPENCODE_GO_API_KEY` in `~/.qwen/.env` but are still forced to pick an auth method. A critical onboarding blocker.

2. **[#3914](https://github.com/QwenLM/qwen-code/issues/3914) — “API connected” yet “fetch failed” (OPEN, 3 comments)**  
   Connection succeeds but subsequent requests fail. Possibly a proxy/handshake issue; affects third‑party endpoints like OpenRouter.

3. **[#3843](https://github.com/QwenLM/qwen-code/issues/3843) — Qwen overwrites `settings.json` on startup (CLOSED, 2 comments)**  
   The CLI replaces user settings without warning. This was fixed in a recent PR (likely #3861) but underscores a dangerous default behaviour.

4. **[#3304](https://github.com/QwenLM/qwen-code/issues/3304) — Switching models mid‑session causes API failures (CLOSED, 2 comments)**  
   Changing providers mid‑conversation (e.g., from Gemini to another) breaks streaming. A long‑standing bug that has finally been closed.

5. **[#3823](https://github.com/QwenLM/qwen-code/issues/3823) — SDK upgrade from 0.1.5 to 0.1.6/0.1.7 triggers process exit (OPEN, 2 comments)**  
   Users of `@qwen-code/sdk` report sporadic `CLI process exited with code 1` after an SDK bump; no detailed error available. High priority for SDK consumers.

6. **[#3945](https://github.com/QwenLM/qwen-code/issues/3945) — edit tool deadlock on large files (OPEN, 2 comments)**  
   `read_file` truncates large files, yet the edit tool requires full reads. This creates an unresolvable precondition, completely blocking edits on big files.

7. **[#3936](https://github.com/QwenLM/qwen-code/issues/3936) — Russian text rendered as corrupted characters (OPEN, 3 comments)**  
   A locale issue where non‑ASCII Cyrillic characters appear as mojibake in the CLI. Community request for proper UTF‑8 handling.

8. **[#3548](https://github.com/QwenLM/qwen-code/issues/3548) — Configurable `plansDirectory` for Plan Mode (OPEN, 3 comments)**  
   A feature request echoed by multiple users who want to control where plan files are stored (similar to Gemini CLI and Claude Code). No response yet from maintainers.

9. **[#3954](https://github.com/QwenLM/qwen-code/issues/3954) — Wrap markdown links in OSC 8 hyperlinks (OPEN, 3 comments)**  
   Currently CLI‑rendered markdown links are not clickable. Request to emit OSC 8 escape sequences so URLs remain clickable in terminal emulators.

10. **[#3926](https://github.com/QwenLM/qwen-code/issues/3926) — Improve input field text editing/selection (OPEN, 2 comments)**  
    `Ctrl+Backspace` does not delete words, and text selection is unsupported. Users want basic terminal input editing parity.

---

## Key PR Progress

1. **[#3902](https://github.com/QwenLM/qwen-code/pull/3902) — Throttle shell tool live text updates (OPEN)**  
   Prevents excessive `binary_progress` events by applying a `OUTPUT_UPDATE_INTERVAL_MS` check that was previously only a guard, thus reducing UI jitter during long‑running shell commands.

2. **[#3762](https://github.com/QwenLM/qwen-code/pull/3762) — VS Code: message edit/rewind + metadata UI (OPEN)**  
   Adds full message editing, rewind capabilities, and message metadata display inside the VS Code extension — a major UX upgrade for the chat panel.

3. **[#3966](https://github.com/QwenLM/qwen-code/pull/3966) — Deduplicate Gemini recovery continuation text (OPEN)**  
   When Gemini hits `MAX_TOKENS`, the recovery stream sometimes re‑sends trailing characters. This PR deduplicates them, preventing visual duplication.

4. **[#3970](https://github.com/QwenLM/qwen-code/pull/3970) — TaskBase envelope + foreground subagent persistence (OPEN)**  
   Part of a larger task registry unification. Introduces a shared envelope for all task kinds and persists foreground subagent state across restarts.

5. **[#3986](https://github.com/QwenLM/qwen-code/pull/3986) — Suppress OpenTelemetry diagnostics from UI (OPEN)**  
   Routes OTel SDK debug output (e.g., exporter failures) away from user‑visible console to the debug log — reduces noise for end users.

6. **[#3896](https://github.com/QwenLM/qwen-code/pull/3896) — Normalize cumulative OpenAI stream deltas (OPEN)**  
   Fixes a compatibility issue with DashScope / 阿里云百炼 that sends accumulated full text instead of incremental suffixes, preventing duplicated content.

7. **[#3968](https://github.com/QwenLM/qwen-code/pull/3968) — Improve rendering on narrow terminals (OPEN)**  
   Detects `contentWidth < 60` and switches table renderer to vertical layout; also fixes table column overflow to prevent scrollback scrolling on small windows.

8. **[#3778](https://github.com/QwenLM/qwen-code/pull/3778) — Desktop app package with Qwen ACP SDK integration (OPEN)**  
   Adds a new `packages/desktop/` module that bundles Qwen Code as a standalone desktop application, leveraging the ACP SDK for cross‑platform communication.

9. **[#3897](https://github.com/QwenLM/qwen-code/pull/3897) — Bound session‑list reads to head/tail 64KB (OPEN)**  
   Optimises `/resume` by reading only the first and last 64KB of session files instead of the entire file, dramatically reducing load times for large histories.

10. **[#3865](https://github.com/QwenLM/qwen-code/pull/3865) — Persist channel sessions across restarts (OPEN)**  
    Fixes a long‑standing issue where channel sessions (e.g., `qwen channel start`) were lost upon restart; conversation context is now preserved.

---

## Feature Request Trends

The most requested directions, distilled from recent issues:

- **Configurable storage paths** — users want `plansDirectory` (#3548), a `QWEN_HOME` env var (#2953 already in PR), and runtime output directories decoupled from `~/.qwen`.
- **Enhanced terminal UI** — wrap markdown links in clickable OSC 8 hyperlinks (#3954), improved input field editing (#3926), and better narrow‑terminal support.
- **Authentication reliability** — multiple reports of `.env` variables not being read (#3877) and token expiry without clear recovery (#3914, #3939).
- **Large file handling** — the `edit` tool deadlock for large files (#3945) highlights a demand for smarter truncation/offset‑aware editing.
- **Plan Mode parity** — users increasingly expect the same flexibility as Gemini CLI / Claude Code regarding plan directory location and policy.
- **Built‑in provider support** — requests for internal/third‑party providers like Idealab (#3953) indicate a need for extensible auth and base URL configuration.

---

## Developer Pain Points

- **Authentication breakdowns** — `.env` variables ignored (#3877) and token expiry without clear error recovery (#3939) are the top blockers for new users.
- **SDK instability** — upgrading `@qwen-code/sdk` from 0.1.5 to 0.1.6/0.1.7 introduces random CLI crashes (#3823), eroding trust in SDK versions.
- **Settings overwrite** — Qwen CLI replacing `settings.json` on startup (#3843) is a dangerous surprise; users expect their config to be respected.
- **File size deadlock** — the `edit` tool unconditionally requires a full file read, but `read_file` truncates large files, making edits impossible (#3945).
- **Model switching fragility** — changing models mid‑session can break streaming entirely (#3304), impacting workflows that rely on multi‑provider use.
- **Missing i18n/UTF-8** — broken Russian text (#3936) shows that non‑Latin scripts are not handled correctly, alienating a significant user base.
- **Sub‑agent approval opacity** — the approval prompt does not show which tool is being requested (#3960), hindering safe delegation.

--- 

*Generated from GitHub data for 2026-05-09. Full changelog: [v0.15.9…v0.16.10-preview.0](https://github.com/QwenLM/qwen-code/compare/v0.15.9...v0.16.10-preview.0)*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*