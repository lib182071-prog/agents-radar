# AI CLI Tools Community Digest 2026-05-07

> Generated: 2026-05-07 09:44 UTC | Tools covered: 8

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

# Cross-Tool AI CLI Ecosystem Comparison Report
**Date:** 2026-05-07

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with **seven major tools** now representing distinct philosophical approaches to agentic development. This week's activity reveals a **convergence around MCP (Model Context Protocol)** as the dominant integration standard, while each tool differentiates on execution model—from Claude Code's structured agent workflows to Pi's extensible plugin architecture. **Cross-platform reliability** (Windows, Linux, macOS) and **authentication stability** remain universal pain points, with billing friction and token consumption transparency emerging as top community concerns. The ecosystem is seeing increased **enterprise adoption pressure**, evidenced by demand for Azure DevOps integration, policy compliance, and SSO support across multiple tools. Notably, the rapid release cadence (4+ releases across tools today) signals that vendors are prioritizing iteration velocity over stability—a trade-off visible in the high number of regression bugs reported.

---

## 2. Activity Comparison (2026-05-07)

| Tool | Hot Issues (24h) | Key PRs (24h) | Release Status | Notable Metric |
|------|-----------------|---------------|----------------|----------------|
| **Claude Code** | 10 active | 5 open | ✅ v2.1.132 shipped | 347 👍 on XDG issue (#1455) |
| **OpenAI Codex** | 10 noteworthy | 10 important | ✅ Rust SDK alpha 12-15 | 140 👍 on Linux desktop (#11023) |
| **Gemini CLI** | 10 hot | 10 key | ✅ v0.42.0-preview.2, v0.41.2 | Critical SSRF fix merged (#26615) |
| **Copilot CLI** | 10 noteworthy | 1 (spam) | ✅ v1.0.43, v1.0.43-0, v1.0.42 | RCE security fix in v1.0.43 |
| **Kimi Code** | 8 active | 3 open | ❌ No new release | YAML skins PR (#2170) gaining traction |
| **OpenCode** | 10 hot | 10 key | ✅ v1.14.40 shipped | 85 👍 for `/btw` command (#16992) |
| **Pi** | 10 noteworthy | 10 merges/open | ❌ Big refactor ongoing | 1300+ test rollback architecture (#4259) |
| **Qwen Code** | 10 noteworthy | 10 important | ✅ v0.15.7 shipped | Agent Team experimental PR (#2886) |

---

## 3. Shared Feature Directions

The following requirements appear across **multiple tool communities**, indicating industry-wide demand:

### a) MCP Resilience & Management
- **Graceful MCP failure handling** — Kimi Code (#769), Copilot CLI (#2282), Qwen Code (#3895)
- **Batch MCP reconnect** — Claude Code (#56937), Copilot CLI (/mcp show improvements)
- **MCP server lifecycle** — OpenAI Codex (first-class runtime servers, PR #21356), Pi (parameter type coercion #4226)

### b) Permission & Safety UX
- **Permission fatigue** — Gemini CLI (#24916), Copilot CLI (#2693, #3165), Claude Code (#42797)
- **Enterprise policy enforcement** — Copilot CLI (#3101, #3162), OpenAI Codex (managed app approval PR #21061)
- **False positive safety filters** — OpenAI Codex (#17615, closed)

### c) Cross-Platform Stability
- **Windows-specific issues** — Claude Code (MSIX failures #49917), Copilot CLI (MCP connectivity #2282), OpenCode (Bun crash #8785, child process hang PR #26147)
- **macOS Gatekeeper friction** — Claude Code (#12531), OpenCode (NAPI crash #24148)
- **Linux (Wayland) incompatibility** — Gemini CLI (#21983), Qwen Code (paste broken #3829)

### d) Session & State Management
- **Session branching/forking** — Gemini CLI (/fork PR #26618), OpenCode (session compression #24709)
- **Session pause/resume** — Copilot CLI (#1928), OpenCode (--continue #25989)
- **Session recovery from errors** — Pi (#3108, #4141), Claude Code (#45937 offline state)

### e) Token & Cost Transparency
- **Token waste from polling** — OpenAI Codex (#13733), Copilot CLI (#2591 infinite premium requests)
- **Configurable context budget** — OpenAI Codex (#19679 skills metadata), Kimi Code (#2168 system prompt)
- **Thought processes counted as tokens** — Gemini CLI (#26631), Pi (#4249 GPT-5.5 blocks)

### f) Theming & UI Customization
- **Light/dark theme toggle** — Qwen Code (#3678 export HTML), Kimi Code (#2171 YAML skins)
- **Terminal rendering fixes** — Pi (#4208 cmux images, #4253 IME), Copilot CLI (#3170 Chinese input)
- **Status line customization** — Claude Code (alt-screen control), Copilot CLI (username toggle)

### g) Provider Integration
- **Azure DevOps support** — OpenAI Codex (#10665), Claude Code (Git provider parity)
- **Custom provider support** — Copilot CLI (ACP mode #3048), OpenCode (#20287 Azure provider)
- **SSO/Enterprise auth** — Claude Code (billing loops), OpenAI Codex (#20161 phone verification)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code |
|-----------|-------------|--------------|------------|-------------|-----------|----------|----|-----------|
| **Primary focus** | Structured agent workflows | IDE-adjacent TUI | Research/OEM platform | GitHub-native enterprise | MCP-first minimalist | AI-first DX | Plugin ecosystem | Open-source local-first |
| **Execution model** | Sub-agent delegation | Goal-based sessions | Component evals | Auto-mode routing | Single-agent MCP | Agent marketplace | Extension host | Agent Team (experimental) |
| **Target user** | Power developers | Full-stack devs | Enterprise teams | GitHub orgs | CLI minimalists | Ecosystem builders | Hackers/Extenders | Open-source community |
| **Differentiator** | XDG compliance (#1 issue) | Rust SDK depth | AST-aware tools | Server-side routing | YAML theming | Bun-based speed | 1300+ test rollback | Local model focus |
| **Weakness** | Billing loops (#54204) | Phone auth (#20161) | Sub-agent false success (#22323) | Transient API errors (#2101) | PyYAML crash (#2166) | Bun crashes (#8785) | Terminal fragility (#4208) | Config overwrite (#3843) |
| **Release cadence** | Weekly patches | Daily alphas | Daily nightlies | Multiple patches/week | Slower (no release today) | Weekly patches | Refactor pause | Weekly patches |
| **Enterprise readiness** | Medium (billing issues) | Medium (auth problems) | High (evaluation framework) | High (GitHub ecosystem) | Low (no SSO) | Medium (desktop app) | Low (experimental) | Medium (daemon mode) |

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid Iteration, Active Community)
- **Claude Code** — Largest community engagement (347 👍 on single issue). High bug density but rapid patch cycle. The XDG compliance demand (#1455) is the ecosystem's most-upvoted issue—a signal of user maturity demanding platform standards.
- **OpenCode** — Second most active community (85 👍 on `/btw`). Strong feature request velocity with responsive PR merging. Bun crash (#8785) is the critical blocker affecting trust.
- **Qwen Code** — Aggressive feature development (Agent Team, daemon mode, light theme). Good PR density but suffers from config-busting bugs (#3843) that erode user confidence.

### Stable but Growing
- **OpenAI Codex** — Active alpha releases (4 in one day) indicate internal iteration, but community feels the gap in Linux desktop support (#11023). Phone verification bugs (#20161) are a recurring trust issue.
- **Gemini CLI** — Strong security consciousness (SSRF fix) and evaluation framework (#24353). Sub-agent reliability (#22323) and token transparency (#26631) are top pain points. Lower community engagement (fewer 👍) but more enterprise-grade feature planning.

### Enterprise-Heavy with Friction
- **Copilot CLI** — Highest security maturity (RCE fix in v1.0.43) but plagued by API reliability (#2101) and premium request confusion (#2591). Enterprise policy blocks (#3101) indicate real deployment friction. Low PR velocity (1 today) suggests maintenance mode or internal development.

### Niche / Early Stage
- **Kimi Code** — Smallest community but innovative (YAML skins, OAuth compliance). MCP resilience (#769) is the defining feature request. Python 3.14 crash (#2166) limits adoption among bleeding-edge users.
- **Pi** — Undergoing major refactor (1300+ tests, rollback architecture). High technical ambition but terminal fragility (#4208) and session unrecoverability (#3108) create trust issues. Plugin ecosystem is unique but complex.

---

## 6. Trend Signals

### For Developers & Decision-Makers

**1. Security Hardening is Non-Negotiable**
- Copilot CLI patched an RCE vulnerability (v1.0.43)
- Gemini CLI fixed SSRF via open redirect (#26615)
- Expect more security-focused audits as these tools gain CI/CD access

**2. Token Waste is the #1 Cost Concern**
- OpenAI Codex background polling (#13733) and Copilot CLI's infinite premium requests (#2591) both highlight that **users are paying for invisible inefficiency**
- Trend: Demand for token budgeting, cost transparency, and configurable polling intervals

**3. Cross-Platform is Still a Differentiator**
- Windows remains the weakest link (MSIX failures, Bun crashes, child process hangs)
- Tools that invest in Windows/Linux parity will win enterprise adoption
- Wayland support is emerging as a Linux-specific litmus test

**4. MCP is Winning the Integration War**
- Every major tool now supports MCP, but **management UX** (reconnect, disable, status) is universally poor
- First-class MCP runtime support (Codex PR #21356) and batch reconnect (Claude Code #56937) signal the next wave

**5. Config Over Convention**
- Claude Code's XDG compliance demand (#1455) and Qwen Code's `settings.json` overwrite bug (#3843) both reflect users demanding **standardized, predictable configuration**
- Customizable everything—context files, themes, budgets, directories—is the clear trend

**6. Agent Reliability is the Trust Barrier**
- Sub-agent false success (Gemini #22323), session unrecoverability (Pi #3108), and stuck processes (Copilot #2101) all erode trust
- Tools that invest in **observability** (e.g., Qwen Code's live agent tree PR #3904) and **recovery** (OpenCode's session compression) will win loyalty

**7. Dual Distribution (CLI + Desktop + IDE)**
- Claude Code and OpenCode both ship desktop apps; Qwen Code adds VS Code plugin; Copilot CLI relies on GitHub ecosystem
- Users expect **seamless switching** between terminal, desktop, and IDE—a gap no tool fully closes yet

**8. Community-Driven Feature Prioritization**
- Most-upvoted issues (XDG compliance, Linux desktop, `/btw` command) are not technical breakthroughs but **quality-of-life improvements**
- The tools that listen to community voting will retain users; those that don't (e.g., Kimi Code removing system prompt #2168 without communication) will face backlash

---

**Bottom Line for Decision-Makers:**

- **Choose Claude Code** for maximum community support and rapid iteration—but budget for billing friction.
- **Choose Copilot CLI** for enterprise/GitHub-native workflows—but prepare for API reliability issues.
- **Choose OpenCode** for the best ecosystem potential and feature velocity—but accept Bun-related instability.
- **Choose Qwen Code** for open-source flexibility and local model support—but expect configuration headaches.
- **Choose Gemini CLI** for evaluation-driven development and security consciousness—but wait for sub-agent reliability improvements.
- **Monitor Pi** for plugin architecture inspiration, but avoid until refactor stabilizes.
- **Evaluate Kimi Code** for MCP-first minimalist workflows, but confirm Python 3.14 compatibility.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot: 2026-05-07 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The most-discussed Pull Requests (by engagement) reveal where community energy is concentrated:

### #1 – Document Typography Skill
**PR #514** — *Add document-typography skill*  
**Status:** Open (since 2026-03-04)  
**Function:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents—issues that affect nearly every long-form document Claude produces.  
**Why it's notable:** Addresses a universal pain point. The community recognizes that typographic quality is a silent differentiator for professional document output.  
🔗 https://github.com/anthropics/skills/pull/514

### #2 – Meta-Skills: Quality & Security Analyzers
**PR #83** — *Add skill-quality-analyzer and skill-security-analyzer to marketplace*  
**Status:** Open (since 2025-11-06)  
**Function:** Two meta-skills that evaluate other Skills across structure, documentation, and security dimensions. The quality analyzer scores on five axes; the security analyzer audits for risk patterns.  
**Why it's notable:** This is the community's strongest signal for "Skills about Skills"—tooling to improve the ecosystem itself.  
🔗 https://github.com/anthropics/skills/pull/83

### #3 – Frontend Design Skill Overhaul
**PR #210** — *Improve frontend-design skill clarity and actionability*  
**Status:** Open (since 2026-01-05)  
**Function:** Revises the existing frontend-design skill to ensure every instruction is concretely actionable within a single conversation, with specific behavioral guidance.  
**Why it's notable:** Reflects demand for *actionable* Skills rather than reference documentation. The discussion centers on token efficiency and Claude-executable instructions.  
🔗 https://github.com/anthropics/skills/pull/210

### #4 – SAP Predictive Analytics Skill
**PR #181** — *Add SAP-RPT-1-OSS predictor skill*  
**Status:** Open (since 2025-12-28)  
**Function:** Wraps SAP's open-source tabular foundation model for predictive analytics on enterprise business data. Enables Claude to run forecasts directly.  
**Why it's notable:** Enterprise AI use case with a concrete model integration. Signals demand for Skills that bridge Claude to specialized ML models.  
🔗 https://github.com/anthropics/skills/pull/181

### #5 – AppDeploy Full-Stack Deployment Skill
**PR #360** — *Added AppDeploy skill for deploying full-stack web apps*  
**Status:** Open (since 2026-02-09, updated 2026-05-04)  
**Function:** Enables Claude to deploy, manage, and version full-stack web applications to public URLs via the AppDeploy platform.  
**Why it's notable:** One of the most actively maintained PRs. Deployment is a high-value capability—turns Claude into an end-to-end app builder.  
🔗 https://github.com/anthropics/skills/pull/360

### #6 – AURELION Cognitive Framework Suite
**PR #444** — *Add AURELION skill suite (kernel, advisor, agent, memory)*  
**Status:** Open (since 2026-02-21, updated 2026-05-06)  
**Function:** Four Skills providing structured thinking templates (5-floor cognitive framework), memory management, and agent orchestration for professional knowledge work.  
**Why it's notable:** Most expansive single submission. The memory component (`proactive_context`) directly addresses a known LLM limitation. High community curiosity.  
🔗 https://github.com/anthropics/skills/pull/444

### #7 – ServiceNow Platform Skill
**PR #568** — *Add ServiceNow platform skill*  
**Status:** Open (since 2026-03-08)  
**Function:** Broad ServiceNow assistant covering ITSM, ITOM, SecOps, ITAM/SAM, FSM, HRSD, CSDM, and IntegrationHub.  
**Why it's notable:** Enterprise platform integration at scale. Demonstrates demand for Skills that replace domain-specific documentation lookups.  
🔗 https://github.com/anthropics/skills/pull/568

---

## 2. Community Demand Trends

Analysis of the top Issues (by comment count) reveals four clear demand vectors:

### 🏢 Enterprise Sharing & Administration
- **Issue #228** (9 comments, 7 👍) — *Enable org-wide skill sharing*: Users want direct sharing links or team skill libraries, not manual file Slack-forwarding.  
- **Issue #61** (3 comments) — *"Not found" error on Team plans*: Infrastructure reliability concerns for organizational users.  

### 🛡️ Security & Trust Boundaries
- **Issue #492** (4 comments) — *Trust boundary abuse via anthropic/ namespace*: Community Skills distributed under `anthropic/` impersonate official offerings. This is the highest-severity community concern.  
- **Issue #412** (4 comments) — *Agent governance skill proposal*: Explicit demand for safety patterns—policy enforcement, threat detection, audit trails.  

### 🔧 Tooling Quality & Developer Experience
- **Issue #202** (8 comments) — *Skill-creator needs best-practice rewrite*: The official skill-creator reads like documentation, not an operational Skill.  
- **Issue #556** (6 comments) — *Run_eval.py 0% trigger rate*: The evaluation pipeline is fundamentally broken. This blocks Skill quality improvement workflows.  
- **Issue #189** (6 comments) — *Duplicate skills from overlapping plugins*: Plugin architecture confusion wastes context window.  

### 🔄 Integration & Platform Expansion
- **Issue #16** (4 comments) — *Expose Skills as MCPs*: Desire for Skills to become interoperable via the Model Context Protocol.  
- **Issue #29** (4 comments) — *Usage with AWS Bedrock*: Demand for cloud-agnostic Skill deployment.  

---

## 3. High-Potential Pending Skills

These open PRs show strong community traction and may land soon:

### Document Typography (PR #514)
🔗 https://github.com/anthropics/skills/pull/514  
Recently updated (March 13). Solves a universal document quality problem. Low implementation risk—purely textual analysis rules.

### Meta-Skills Suite (PR #83)
🔗 https://github.com/anthropics/skills/pull/83  
Quality and security analyzers for the ecosystem. The longest-running high-engagement PR. Addresses the "who audits the auditors" problem for Skills.

### ODT Skill (PR #486)
🔗 https://github.com/anthropics/skills/pull/486  
OpenDocument Format creation, template filling, and HTML conversion. Fill an obvious format gap alongside the existing DOCX/PDF skills. Updated April 14.

### AppDeploy Skill (PR #360)
🔗 https://github.com/anthropics/skills/pull/360  
Most recently maintained (May 4). Full-stack deployment is a clear demo-worthy capability. Likely to merge as the infrastructure matures.

### AURELION Suite (PR #444)
🔗 https://github.com/anthropics/skills/pull/444  
Updated May 6—most active PR. The memory component is a genuinely novel contribution to Claude's persistent context problem. Could become a reference Skill architecture.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for *ecosystem quality tooling* (meta-skills for Skill auditing, security analyzers, and developer experience fixes) paired with *enterprise integration Skills* (ServiceNow, SAP, deployment pipelines), revealing a shift from "cool Skills" to "production-grade Skills that organizations can trust and share."**

---

# Claude Code Community Digest — 2026-05-07

## Today's Highlights
A fresh release (v2.1.132) adds environment variables for session identification and alternate-screen control. The long-standing XDG compliance issue (#1455) continues to draw massive community support (347 👍), while a new LSP workspaceSymbol bug (#30948) is gaining traction. Installation and billing friction remain top pain points, with multiple Windows MSIX failures and subscription loops reported this week.

## Releases
**v2.1.132** — [Release Link](https://github.com/anthropics/claude-code/releases/tag/v2.1.132)  
- Added `CLAUDE_CODE_SESSION_ID` environment variable to the Bash tool subprocess, matching the `session_id` passed to hooks.  
- Added `CLAUDE_CODE_DISABLE_ALTERNATE_SCREEN=1` env var to opt out of the fullscreen alternate-screen renderer, keeping the conversation in the terminal buffer.

## Hot Issues
1. [#11447 — [BUG] Claude can't edit files that use tabs for indentation](https://github.com/anthropics/claude-code/issues/11447)  
   *56 comments, 51 👍* — A long-standing bug: Claude Code fails to apply edits to files indented with tabs. High engagement suggests many users hit this daily.

2. [#1455 — Claude Code does not respect the XDG Base Directory specification](https://github.com/anthropics/claude-code/issues/1455)  
   *55 comments, 347 👍* — The most-upvoted open issue. Users demand proper separation of config, cache, and runtime data per freedesktop standards. Feature request #2350 tracks the same root cause.

3. [#45937 — Dispatch main conversation permanently offline despite working Cowork tasks](https://github.com/anthropics/claude-code/issues/45937)  
   *26 comments, 12 👍* — Desktop “offline” state breaks the main thread but not Cowork tasks, confusing multi-device workflows.

4. [#17149 — [BUG] LSP workspaceSymbol operation sends empty query parameter](https://github.com/anthropics/claude-code/issues/17149)  
   *25 comments, 17 👍* — LSP tool silently fails during symbol search; user reports confirm the tool schema lacks a query field.

5. [#30948 — LSP tool: workspaceSymbol needs a query parameter](https://github.com/anthropics/claude-code/issues/30948)  
   *20 comments, 61 👍* — Complementary to #17149 with a clear schema fix request. High 👍 count indicates broad impact across language servers.

6. [#2350 — Follow XDG Base Directory specification properly](https://github.com/anthropics/claude-code/issues/2350)  
   *19 comments, 84 👍* — Duplicate of #1455 but focused specifically on moving cache/runtime out of `$XDG_CONFIG_HOME`. Unified demand for platform compliance.

7. [#14360 — [BUG] Failed to install Anthropic marketplace · Will retry on next startup](https://github.com/anthropics/claude-code/issues/14360)  
   *18 comments, 11 👍* — Marketplace installation flakiness on Linux; users stuck in a retry loop with no clear resolution path.

8. [#12531 — macOS brew upgrade requires bypassing security to launch Claude Code](https://github.com/anthropics/claude-code/issues/12531)  
   *15 comments, 4 👍* — After `brew upgrade claude-code`, macOS Gatekeeper blocks launch, requiring manual bypass via System Settings.

9. [#56924 — [DOCS] 5 hour limit removed, but weekly limit remains?](https://github.com/anthropics/claude-code/issues/56924)  
   *15 comments, 0 👍* — Fresh today: users question the “doubled capacity” announcement. Removing the 5-hour cap but keeping the weekly cap may not increase usable time. Documentation clarity needed.

10. [#54204 — Max 5x → Max 20x upgrade stuck in void_invoice loop](https://github.com/anthropics/claude-code/issues/54204)  
    *13 comments, 0 👍* — Billing upgrade fails with the same canceled PaymentIntent on every retry. Duplicates #10832, #50710, #43118 — a recurring infrastructure issue.

## Key PR Progress
1. [#56334 — docs: Add Windows Developer Mode note for symlink support](https://github.com/anthropics/claude-code/pull/56334)  
   *Open* — Adds documentation for Windows users about enabling Developer Mode to prevent silent “0 tokens” failures from background agents.

2. [#49596 — refactor: extract shared GitHub API client into github-api.ts with tests](https://github.com/anthropics/claude-code/pull/49596)  
   *Open* — Clean separation of GitHub client logic, adds unit tests. Improves maintainability for MCP/API integrations.

3. [#56784 — Pin GitHub Actions to commit SHAs](https://github.com/anthropics/claude-code/pull/56784)  
   *Open* — Security hardening: pins all third-party CI actions to immutable commit hashes instead of version tags.

4. [#56621 — Fix duplicate rules on init firewall](https://github.com/anthropics/claude-code/pull/56621)  
   *Open* — Prevents `init-firewall.sh` from failing when duplicate iptables rules already exist. Small but practical fix for Linux deployers.

5. [#20824 — Add CLAUDE.md: Comprehensive AI assistant guidelines for repository](https://github.com/anthropics/claude-code/pull/20824)  
   *Closed* — Adds a structured guideline document for AI assistants contributing to the repo. Merged; sets a precedent for other projects.

*Note: Only 5 PRs were updated in the past 24 hours; all are listed above.*

## Feature Request Trends
- **XDG Base Directory compliance** (#1455, #2350) — Overwhelming community consensus to stop dumping cache and state into config directories. The highest-upvoted request cluster.
- **Native Bitbucket integration** (#38179) — Users want Git provider parity beyond GitHub and GitLab.
- **Inference mode switching UI** (#56606) — A native toggle between first-party and third-party/gateway inference in Claude Desktop.
- **Batch MCP server reconnect** (#56937) — `/mcp reconnect-all` command to restart all stdio MCP servers after network drops, especially important for setups with 10+ servers.
- **Cross-platform installation reliability** — Implicit request from repeated Windows MSIX and macOS Gatekeeper issues.

## Developer Pain Points
- **LSP workspaceSymbol broken by missing query parameter** — Issues #17149 and #30948 show the tool schema is incomplete; users on clangd, TypeScript, and other LSPs cannot search symbols.
- **Windows MSIX installer wedged state** (#49917, #56949) — HRESULT 0x80073CF6 appears repeatedly after failed installations, requiring manual cleanup. No official remediation documented.
- **Billing upgrade loops** (#54204, #55266) — Stuck payment intent retries when upgrading from Max 5x to Max 20x; users cannot complete purchase.
- **macOS security bypass after upgrade** (#12531) — Each brew update triggers Gatekeeper, forcing devs to manually approve the binary.
- **Desktop dispatch offline inconsistency** (#45937) — Main thread appears offline while Cowork tasks work; mobile clients show stale state.
- **Auto-mode ignoring permissions setting** (#42797) — When `permissions.ask` is configured, auto-mode bypasses the prompt, potentially executing unsafe operations.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest – 2026-05-07

## Today’s Highlights
Multiple Rust SDK alpha releases (0.129.0-alpha.12–15) hit the repository, signaling active internal iteration. The community continues to push for a native Linux desktop app and better Azure DevOps integration, while a critical authentication bug and token-wasting polling behavior dominate discussion. On the engineering side, the team is converging on operation-backed diff tracking, first-class MCP runtime servers, and config validation improvements.

## Releases
- **rust-v0.129.0-alpha.12, .13, .14, .15** – Four consecutive alpha releases for the Rust SDK. No changelog details are available; the rapid cadence suggests ongoing internal testing or CI adjustments.
  - [rust-v0.129.0-alpha.12](https://github.com/openai/codex/releases/tag/rust-v0.129.0-alpha.12)
  - [rust-v0.129.0-alpha.13](https://github.com/openai/codex/releases/tag/rust-v0.129.0-alpha.13)
  - [rust-v0.129.0-alpha.14](https://github.com/openai/codex/releases/tag/rust-v0.129.0-alpha.14)
  - [rust-v0.129.0-alpha.15](https://github.com/openai/codex/releases/tag/rust-v0.129.0-alpha.15)

## Hot Issues (10 Noteworthy)
1. **Phone verification failure (Closed)** – [#20161](https://github.com/openai/codex/issues/20161)  
   Users switching devices or using SSO are forced to verify a phone number even when none was added. 98 comments and 72 👍 indicate a widespread authentication blocker. Closed today without visible resolution notes.

2. **Linux desktop app (Open)** – [#11023](https://github.com/openai/codex/issues/11023)  
   With 140 👍 and 47 comments, this is the most upvoted open feature request. Users report macOS power issues and want a native Linux app for stability on desktop Linux.

3. **“I’m sorry, but I cannot assist” false positive (Closed)** – [#17615](https://github.com/openai/codex/issues/17615)  
   Safety-check rejects legitimate requests on Azure with GPT-5.2 high. 31 comments, closed today. Underlying safety filter tuning remains a pain point for enterprise users.

4. **High GPU usage from “thinking” animation (Open)** – [#16857](https://github.com/openai/codex/issues/16857)  
   A tiny animation during model processing causes excessive GPU load, especially on macOS. 21 comments; users call for a toggle or resource-efficient alternative.

5. **Background process polling wastes tokens (Open)** – [#13733](https://github.com/openai/codex/issues/13733)  
   Each poll of a running command (e.g., `cargo build`) sends the full conversation history, burning credits. 16 comments, 16 👍. A design-level issue affecting heavy terminal users.

6. **Native Azure DevOps integration (Open)** – [#10665](https://github.com/openai/codex/issues/10665)  
   46 👍 and 13 comments request first-class support for Azure Repos, mirroring GitHub integration. Enterprise teams feel left out.

7. **Skills metadata context budget hardcoded at 2% (Open)** – [#19679](https://github.com/openai/codex/issues/19679)  
   Users with many skills hit truncation warnings. 11 👍 – a configurable budget would prevent silent loss of skill descriptions.

8. **Branch detail panel blocks scrollbar (Open)** – [#20569](https://github.com/openai/codex/issues/20569)  
   On Windows and macOS, the right panel overlaps the chat scrollbar, making it impossible to grab the thumb. 15 👍 – a UI regression affecting daily workflow.

9. **Chats directory not configurable (Open)** – [#19909](https://github.com/openai/codex/issues/19909)  
   Codex stores chat history in `~/Documents/Codex`, which often syncs to iCloud, causing corruption. 5 comments – users request a setting to change the path.

10. **`/goal` rejects long pasted input (Closed)** – [#21477](https://github.com/openai/codex/issues/21477)  
    CLI 0.128.0 fails to normalize long objectives before rejecting. Closed quickly but highlights input handling issues in the TUI.

## Key PR Progress (10 Important)
1. **Show goal-started threads in resume lists** – [#21489](https://github.com/openai/codex/pull/21489)  
   Ensures `/goal` threads appear in resume listings even before a normal user message. Improves session continuity.

2. **Fix: preserve exact turn diffs after partial apply_patch failures** – [#21518](https://github.com/openai/codex/pull/21518)  
   Follow-up to operation-backed diffs; handles cases where file operations partially succeed, preventing data loss.

3. **Make turn diff tracking operation-backed** – [#21180](https://github.com/openai/codex/pull/21180)  
   Replaces filesystem-based diff tracking with an operation accumulator, improving accuracy for move-overwrite scenarios. Merged.

4. **Move tool specs onto handlers** – [#21461](https://github.com/openai/codex/pull/21461)  
   Consolidates tool definition with handler registration, eliminating indirection and simplifying registry construction.

5. **Feat: make built-in MCPs first-class runtime servers** – [#21356](https://github.com/openai/codex/pull/21356)  
   Elevates built-in MCPs above user-configured servers, decoupling them from stdio config. Experimental but promises better lifecycle management.

6. **Warn on invalid config enum values** – [#21111](https://github.com/openai/codex/pull/21111)  
   Instead of failing on a bad `config.toml` value, Codex will now warn and continue with remaining valid settings. User-friendly resilience.

7. **Add stdio exec-server client transport** – [#20664](https://github.com/openai/codex/pull/20664)  
   Enables connecting to exec-server instances via command-line stdio rather than pre-existing WebSocket URLs, useful for custom environment setups.

8. **Expose plugin share metadata in shareContext** – [#21495](https://github.com/openai/codex/pull/21495)  
   Extends `PluginSummary.shareContext` with `shareUrl` and `shareTargets`, enabling richer sharing workflows from plugins.

9. **Feat: support managed app tool approval requirements** – [#21061](https://github.com/openai/codex/pull/21061)  
   Allows administrators to enforce per-tool approval rules for connector apps via `requirements.toml` or cloud policies.

10. **Drop duplicate contiguous user messages during compaction** – [#19082](https://github.com/openai/codex/pull/19082)  
    Merged – removes redundant user messages in session compaction, reducing token usage and improving conversation quality.

## Feature Request Trends
- **Linux Desktop App** – [#11023](https://github.com/openai/codex/issues/11023) remains the top-voted feature.
- **Azure DevOps Integration** – [#10665](https://github.com/openai/codex/issues/10665) shows strong enterprise demand.
- **Configurable Skills & Storage** – Requests to make skills metadata budget ([#19679](https://github.com/openai/codex/issues/19679)) and chat directory ([#19909](https://github.com/openai/codex/issues/19909)) user-configurable.
- **UI/UX Customization** – Disable right‑panel hover ([#20749](https://github.com/openai/codex/issues/20749)), show remaining usage in chat ([#19869](https://github.com/openai/codex/issues/19869)).
- **IDE Integration** – VS Code extension support for opening Codex sessions as editor tabs ([#20951](https://github.com/openai/codex/issues/20951)).
- **CLI Image Support** – Paste images directly into CLI sessions ([#19143](https://github.com/openai/codex/issues/19143)).
- **MCP Management** – Interactive enable/disable and status indicators in `/mcp` ([#21384](https://github.com/openai/codex/issues/21384), [#20995](https://github.com/openai/codex/issues/20995)).

## Developer Pain Points
- **Authentication instability** – Phone verification loops and OAuth revocations ([#20161](https://github.com/openai/codex/issues/20161), [#20320](https://github.com/openai/codex/issues/20320), [#19801](https://github.com/openai/codex/issues/19801)) block access without clear recovery.
- **Token waste** – Background polling ([#13733](https://github.com/openai/codex/issues/13733)) and duplicate messages burning credits.
- **Desktop performance** – High GPU from animations ([#16857](https://github.com/openai/codex/issues/16857)) and slowdown with large histories ([#18693](https://github.com/openai/codex/issues/18693)).
- **Sandbox & compatibility** – Bubblewrap failure on older Linux ([#21516](https://github.com/openai/codex/issues/21516)), WebSocket fallback timeouts ([#15014](https://github.com/openai/codex/issues/15014)).
- **Safety false positives** – Overly strict filtering on legitimate requests ([#17615](https://github.com/openai/codex/issues/17615)).
- **UI regressions** – Scrollbar blocked by panels ([#20569](https://github.com/openai/codex/issues/20569), [#21488](https://github.com/openai/codex/issues/21488)), file tree toggle unreliable ([#20552](https://github.com/openai/codex/issues/20552)).
- **`/goal` command quirks** – Rejects long pastes and ignores plan mode ([#21477](https://github.com/openai/codex/issues/21477), [#21512](https://github.com/openai/codex/issues/21512)).
- **MCP configuration friction** – No built-in way to disable servers without editing config files ([#21384](https://github.com/openai/codex/issues/21384)).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-05-07

## Today's Highlights
Three patch releases landed today, fixing a tool approval race condition in the A2A server and a dialog clipping issue. The community is actively discussing sub‑agent recovery after turn limits (issue #22323) and the introduction of AST‑aware file reading for smarter codebase mapping (issue #22745). A security‑critical PR addresses a potential SSRF via open redirect in the web‑fetch tool.

## Releases
- **v0.42.0-preview.2** – Cherry‑pick fix into preview branch.  
  [Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.42.0-preview.1...v0.42.0-preview.2)
- **v0.42.0-nightly.20260506.g80d269054** – Fixes: tool approval race condition in A2A server (`#26479`); settings dialog border clipping using maxHeight (`#26485`).  
  [Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.42.0-nightly.20260505...v0.42.0-nightly.20260506.g80d269054)
- **v0.41.2** – Patch backported from `#26568`.  
  [Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.41.1...v0.41.2)

## Hot Issues (10 noteworthy)
1. **#24353 – Robust component level evaluations**  
   Follow‑up to #15300; tracks 76 behavioral eval tests across 6 supported models. Community eager for standardised evaluation framework.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/24353) (5 comments)

2. **#22745 – Assess AST‑aware file reads, search, and mapping**  
   Epic investigating whether AST‑aware tools reduce token noise and improve navigation. Highly upvoted (+1).  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22745) (5 comments)

3. **#22323 – Subagent recovery after MAX_TURNS reports GOAL success**  
   Critical bug: `codebase_investigator` falsely reports success after hitting turn limit. Users frustrated by hidden interruptions.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/22323) (5 comments, 👍 2)

4. **#21968 – Gemini does not use skills and sub‑agents enough**  
   Anecdotal but widespread: the model rarely invokes custom skills unless explicitly told.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21968) (5 comments)

5. **#26563 – Tool "save_memory" not found**  
   `/memory add` command fails with tool not found error. Blocks memory functionality for users on v0.41.1.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26563) (3 comments)

6. **#24916 – Keeps asking for permissions on the same file**  
   Repeated permission prompts despite “allow for all future sessions”. Tops usability frustrations.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/24916) (3 comments)

7. **#21983 – Browser subagent fails in Wayland**  
   Wayland users cannot use browser agent; fails with cryptic “GOAL” termination.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/21983) (3 comments, 👍 1)

8. **#25166 – Shell command execution gets stuck “Waiting input”**  
   After a simple command completes, agent hangs indefinitely. High impact (👍 3).  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/25166) (2 comments)

9. **#26631 – Thought processes counted as tokens**  
   Users report internal thought processes being billed as output tokens, causing unexpected costs.  
   [Issue](https://github.com/google-gemini/gemini-cli/issues/26631) (2 comments)

10. **#26516 – Memory system bugs and quality improvements** (tracking issue)  
    Aggregates several memory‑related bugs: low‑signal retry loops, invalid patch handling, deterministic redaction.  
    [Issue](https://github.com/google-gemini/gemini-cli/issues/26516) (1 comment)

## Key PR Progress (10 important)
1. **#26361 – fix(core): externalize https‑proxy‑agent to fix proxy support** (P1)  
   Fixes `HttpsProxyAgent is not a constructor` when behind a proxy.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26361)

2. **#26630 – fix(browser): reset actionCounter between sequential browser_agent invocations**  
   Prevents hitting `maxActionsPerTask` immediately on reused `BrowserManager`.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26630)

3. **#26625 – feat: interactive hunk review for file edits**  
   Gives users granular control to accept/reject individual changed hunks.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26625)

4. **#26618 – feat(cli): add /fork session branching command**  
   Implements `/fork` to snapshot a session, avoiding last‑write‑wins corruption when resuming.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26618)

5. **#26594 – fix(context): implement loose boundary policy for gc backstop**  
   Breaks a rare feedback loop in context manager and adds token calculation logging.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26594)

6. **#26498 – feat(cli): show acknowledgment when user steering hint is processed**  
   Provides visible feedback when a mid‑turn steering hint is registered (addresses #26485).  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26498)

7. **#26615 – fix(core): prevent SSRF via open redirect in web‑fetch tool**  
   Security fix: disables automatic redirect following to block internal network scanning.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26615)

8. **#26609 – fix(ux): transcribed text not showing after releasing space (Whisper models)**  
   Increases draining grace period so speech‑to‑text transcription appears reliably.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26609)

9. **#26189 – fix(cli): prevent Windows bash backspace from triggering delete‑word**  
   Patches input handling for Git Bash/MSYS2 where backspace sends `ESC + DEL`.  
   [PR](https://github.com/google-gemini/gemini-cli/pull/26189)

10. **#26241 – fix(cli): resolve tmux scroll issue using ink's useStdout**  
    Fixes scroll buffer using only top 20% of screen under tmux.  
    [PR](https://github.com/google-gemini/gemini-cli/pull/26241)

## Feature Request Trends
- **Memory system improvements** – Multiple issues (#26516, #26525, #26523, #26522) focus on auto‑memory: better redaction, invalid patch quarantine, stopping retry loops on low‑signal sessions.
- **AST‑aware tools** – Epic #22745 explores parsing code to improve file reads and codebase mapping.
- **Sub‑agent reliability** – Request for session takeover, lock recovery (#22232), and preventing destructive behavior (#22672).
- **Permission UX** – Requests for once‑only permission prompts (#24916) and clearer parallel tool call layouts (#24943).
- **Streaming & UI polish** – Incremental table rendering (#25218), thought‑process hiding from token count (#26631), and screen corruption after external editors (#24935).

## Developer Pain Points
- **Sub‑agent false success** – #22323 shows agents marking MAX_TURNS as “GOAL” instead of reporting failure.
- **Shell hangs** – #25166 reports commands that complete but leave the agent stuck on “Awaiting input”.
- **Tool not found** – #26563: `/memory add` fails with missing tool, breaking core memory feature.
- **Permission fatigue** – #24916: persistent prompts even after “allow forever”.
- **Wayland incompatibility** – #21983: browser agent crashes under Wayland.
- **Agent ignores skills** – #21968: models rarely use custom skills or sub‑agents autonomously.
- **Stack overflows** – #22505 (now closed) fixed a recursion bug in scroll handling; similar edge cases still reported.
- **Windows input quirks** – #26189 addresses backspace conflicts, and #24202 reports scrambled text over SSH on Windows.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-05-07

## Today's Highlights

Three patch releases landed in the last 24 hours, most notably **v1.0.43** which introduces a critical fix for a remote code execution (RCE) vulnerability and adds server-side model routing for Auto mode. The community remains vocal about two pain points: infinite premium request consumption per session (Issue #2591, 32 comments) and transient API errors leading to rate limits (Issue #2101, 24 comments). Several new MCP-related issues also surfaced, including false-positive policy blocks for registry-listed servers.

---

## Releases

**v1.0.43** ([release notes](https://github.com/github/copilot-cli/releases/tag/v1.0.43))  
- Username toggle in `/statusline` picker to display active account  
- Auto mode now uses server-side model routing for real-time model selection  
- Resume prompt shows correct session name with multiple active sessions  
- **Critical security fix**: Protects against RCE from malicious input  
- `/mcp show` now suggests directly runnable commands when server names contain whitespace  
- MCP server failure warnings include stderr output  

**v1.0.43-0** ([release notes](https://github.com/github/copilot-cli/releases/tag/v1.0.43-0))  
- Download progress displayed during `update` command  
- Fixed: MCP server child processes (npx/uvx) are now fully terminated when a session ends  

**v1.0.42** ([release notes](https://github.com/github/copilot-cli/releases/tag/v1.0.42))  
- Improved MCP server failure warnings with actionable `/mcp show` commands  
- Added `-C <directory>` flag to change working directory before starting  

---

## Hot Issues (10 noteworthy)

1. **[#2591] Single session request → infinite premium requests consumed**  
   *Area: models* – A single user request spawns dozens of tool invocations, each consuming a premium request (80–100 per reply). High community engagement (32 comments, 13 👍).  
   [Issue #2591](https://github.com/github/copilot-cli/issues/2591)

2. **[#2101] “Request failed due to a transient API error. Retrying…”**  
   *Area: models* – Persistent transient errors eventually hit rate limits. Affects many users (24 comments, 16 👍).  
   [Issue #2101](https://github.com/github/copilot-cli/issues/2101)

3. **[#1928] Allow to pause Copilot work**  
   *Area: sessions* – Users want the ability to pause a session, give additional instructions, and resume without losing context. 8 comments.  
   [Issue #1928](https://github.com/github/copilot-cli/issues/1928)

4. **[#2282] Not able to connect to MCP servers on Windows**  
   *Area: mcp* – `Failed to connect to MCP server` errors even after running `/mcp show`. Likely path/installation issue. 8 comments.  
   [Issue #2282](https://github.com/github/copilot-cli/issues/2282)

5. **[#3101] Enterprise: access denied by Copilot policy**  
   *Area: enterprise, models* – Loading models fails with policy denial despite correct configuration. 5 comments, 3 👍.  
   [Issue #3101](https://github.com/github/copilot-cli/issues/3101)

6. **[#3162] 1.0.42 falsely reports registry-listed custom MCP servers as blocked by policy**  
   *Area: mcp* – Regression where a custom server already in the MCP registry is incorrectly flagged as blocked. 3 comments.  
   [Issue #3162](https://github.com/github/copilot-cli/issues/3162)

7. **[#3135] BYOK statusline shows “medium” effort despite `--effort high`**  
   *Area: models, configuration* – The statusline displays `gpt-5.5 (medium)` even when the actual request uses `reasoning_effort: "high"`. 2 comments.  
   [Issue #3135](https://github.com/github/copilot-cli/issues/3135)

8. **[#2729] `/delegate` command doesn’t use specified source branch**  
   *Area: agents* – Delegated tasks ignore user-specified branch names or source branches. 2 comments, 2 👍.  
   [Issue #2729](https://github.com/github/copilot-cli/issues/2729)

9. **[#3048] Support custom providers via ACP mode**  
   *Area: non-interactive, models* – ACP mode ignores `COPILOT_PROVIDER_*` environment variables. 2 comments, 1 👍.  
   [Issue #3048](https://github.com/github/copilot-cli/issues/3048)

10. **[#3170] Chinese input cursor position is wrong**  
    *Area: input-keyboard, terminal-rendering* – Cursor misalignment when typing Chinese characters breaks the input experience. 1 comment.  
    [Issue #3170](https://github.com/github/copilot-cli/issues/3170)

---

## Key PR Progress

Only **one pull request** was updated in the last 24 hours:  

- **[#3163]** – Titled “ViewSonic monitor”, appears to be unrelated/spam (references an action runner and unrelated issue numbers). No relevant code changes.  
  [PR #3163](https://github.com/github/copilot-cli/pull/3163)

No meaningful PRs were merged or updated this period. The community’s focus remains on bug reports and feature requests.

---

## Feature Request Trends

Based on the most-upvoted and active issues, the clearest feature directions are:

- **Session pause/resume** – Ability to halt a session mid-execution, inject new instructions, and continue without losing context (Issue #1928).  
- **Vi/Vim input mode** – Long-standing request (57 👍) for modal editing in the interactive CLI (Issue #13).  
- **Configurable system prompt** – Users want to slim down the fixed token overhead (~20,500 tokens) of the default system prompt (Issue #2627, 4 👍).  
- **Image deletion from context** – Once an image is used, it remains in the context window; users request a way to remove it to preserve token budget (Issue #3168).  
- **Custom providers in ACP mode** – Support `COPILOT_PROVIDER_*` environment variables for non-interactive sessions (Issue #3048).  
- **User account switching** – A `--user` argument to select between work and personal accounts without re-authentication (Issue #3169).  

---

## Developer Pain Points

Several recurring frustrations stand out from the latest issues:

1. **Infinite premium request consumption** – Single user requests triggering 80–100 API calls undermines trust and cost predictability (#2591).  
2. **Transient API errors & rate limits** – Users hit rate limits even during normal usage because of retry loops (#2101).  
3. **MCP server connectivity** – Windows users struggle with initial MCP connection, and registry validation false positives block legitimate servers (#2282, #3162).  
4. **Enterprise policy blocks** – Access denied errors for model loading persist across versions (#3101).  
5. **Permission fatigue** – Harmless commands like `2>/dev/null` still require approval (#2693), and compound shell commands always prompt even when individual commands are whitelisted (#3165).  
6. **Context size loss after `/compact`** – Token count drops dramatically, ignoring user-configured `COPILOT_PROVIDER_MAX_PROMPT_TOKENS` (#3174).  
7. **Windows terminal quirks** – `cmd.exe` windows flash on MCP server start (#3171), clipboard ownership messages break layout (#3172), and Chinese input cursor misalignment (#3170).  

These pain points highlight the community’s desire for more stable API handling, refined permission systems, and better platform compatibility.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-07

**Data Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## 1. Today's Highlights

Today’s community activity centers on **MCP reliability improvements** and **user interface customization**. A new PR (#2170) introduces YAML-based color skins, addressing a long-standing desire for personalized themes. Meanwhile, two critical MCP bugs—connection handling and OAuth compliance—continue to generate discussion, alongside a crash caused by Python 3.14 alpha incompatibility with PyYAML.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

*All 8 issues updated in the last 24h are listed below, as they represent the most active community topics.*

| Issue | Title | Why it matters | Community reaction |
|-------|-------|----------------|-------------------|
| [#769](https://github.com/MoonshotAI/kimi-cli/issues/769) | [enhancement] MCP should not exit automatically when connection fails | Prevents single MCP failure from blocking entire CLI session, aligns with Codex/Claude Code behavior. | 6 👍, 3 comments; long-running discussion (since Jan 2026) indicates strong demand. |
| [#2173](https://github.com/MoonshotAI/kimi-cli/issues/2173) | [enhancement] Add crow-cli support to kimi coding plan | User reports inability to use custom API keys with paid plan; requests support for third-party agent `crow-cli`. | 0 👍, 0 comments; new issue, may gain traction if more users face similar restrictions. |
| [#2172](https://github.com/MoonshotAI/kimi-cli/issues/2172) | MCP OAuth fails when server returns `client_secret_basic` | OAuth flow broken for servers using `client_secret_basic` method; blocks integration with many standard OAuth MCP servers. | 0 👍, 0 comments; specific bug that could affect enterprise users. |
| [#2171](https://github.com/MoonshotAI/kimi-cli/issues/2171) | RFC: user-customizable color skins via YAML | Proposes `~/.kimi/skins/` directory for user-defined color palettes, enabling terminal branding and accessibility. | 0 👍, 0 comments; feature request that already has a companion PR (#2170). |
| [#2169](https://github.com/MoonshotAI/kimi-cli/issues/2169) | Feature request: non-interactive `kimi usage` for programmatic quota checks | Users need scriptable quota inspection for CI/dashboard usage; current `/usage` only works inside REPL. | 0 👍, 0 comments; clear use case for automation. |
| [#2168](https://github.com/MoonshotAI/kimi-cli/issues/2168) | [bug] Bring the system prompt back PLEASE!!! | Reports that system prompt is completely removed in v1.41.0, affecting model behavior. | 1 👍, 0 comments; emotional tone suggests user frustration. |
| [#2167](https://github.com/MoonshotAI/kimi-cli/issues/2167) | [enhancement] Web UI: blink/tab title notification when approval needed | Users multitasking miss tool approval prompts; requests browser tab notification. | 0 👍, 0 comments; usability improvement for web mode. |
| [#2166](https://github.com/MoonshotAI/kimi-cli/issues/2166) | kimi-cli crashes with SIGSEGV on Python 3.14.0a6 due to PyYAML C extension ABI | Segmentation fault on Python 3.14+ blocks `kimi term`/Toad users on that platform. | 0 👍, 0 comments; compatibility issue with bleeding-edge Python. |

---

## 4. Key PR Progress

*All 3 PRs updated in the last 24h are included.*

| PR | Title | What it does | Status |
|----|-------|-------------|--------|
| [#2138](https://github.com/MoonshotAI/kimi-cli/pull/2138) | fix(shell): respect default shell in shell mode | Passes `$SHELL` environment variable to subprocess, preferring user’s default shell over bash. Includes regression tests. | Open (updated May 7) |
| [#2139](https://github.com/MoonshotAI/kimi-cli/pull/2139) | fix(mcp): preserve structured content and sanitize refs | Ensures MCP tool results retain machine-readable JSON content; removes problematic `$ref` sibling metadata before sending to model. With tests. | Open (updated May 7) |
| [#2170](https://github.com/MoonshotAI/kimi-cli/pull/2170) | feat: add user-customizable color skins via YAML | Implements `/skin` slash command and YAML loader (`~/.kimi/skins/`). Closes #2171. Hermes-compatible fallback. | Open (created May 6) |

---

## 5. Feature Request Trends

The most requested feature directions, distilled from **all issues**:

- **MCP resilience and compliance** — Do not crash on MCP connection failure (#769); support OAuth `client_secret_basic` (#2172); preserve structured MCP output (PR #2139).
- **Customization and theming** — User-defined color skins via YAML (#2171, PR #2170); non-interactive quota command (#2169); Web UI tab notifications (#2167).
- **Third-party integration** — Allow custom API keys with paid plans for tools like `crow-cli` (#2173); better support for default shell environments (PR #2138).
- **System prompt transparency** — Users demand the system prompt be restored after it was removed in v1.41.0 (#2168).

---

## 6. Developer Pain Points

Recurring frustrations and high-frequency requests:

- **Single point of failure in MCP** — A single misconfigured MCP server blocks all CLI usage (#769). Workarounds are non-existent, and the behavior differs from competitors like Codex/Claude Code.
- **Fragile Python version compatibility** — The CLI crashes on Python 3.14 alpha due to PyYAML C extension ABI (#2166). Developers using rolling-release distros or actively testing new Python versions are affected.
- **Loss of system prompt control** — Users feel the removal of the system prompt in v1.41.0 reduces model quality and removes a trusted parameter (#2168). No official response or rollback option.
- **No scriptable quota monitoring** — Teams that automate CI pipelines or resource dashboards cannot programmatically check remaining usage; the `/usage` command is REPL-only (#2169).
- **OAuth interoperability gaps** — MCP servers using standard OAuth flows (`client_secret_basic`) fail to authenticate (#2172), limiting integration with enterprise identity providers.

---

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-07

## Today's Highlights

A new patch release v1.14.40 ships with core improvements including remote `.well-known/opencode` configs and reasoning block fixes. Meanwhile, the community is buzzing over a persistent Bun crash on Windows (36 comments) and a critical `edit` tool regression that breaks file modifications. High demand for a `/btw` command (85 👍) continues to grow, and a wave of Windows-specific process-handling PRs signals improving platform stability.

## Releases

**[v1.14.40](https://github.com/anomalyco/opencode/releases/tag/v1.14.40)** — Core improvements: support `.well-known/opencode` configs pointing to remote files. Bugfixes: preserve assistant text when replaying signed reasoning blocks (@edevil), consistent not-found errors for missing sessions, and CORS headers applied before authentication to ensure proper browser behavior.

## Hot Issues

1. **[#8785 — Bun has crashed](https://github.com/anomalyco/opencode/issues/8785)** (36 comments, 7 👍)  
   Critical crash on Windows x64 with Bun v1.3.5. Users report it happening without clear reproduction steps; team is investigating.

2. **[#24529 — edit tool crashes on existing file modification](https://github.com/anomalyco/opencode/issues/24529)** (22 comments)  
   `undefined is not an object (evaluating 'output.args.filePath')` when `oldString` is non-empty. Breaks the most common edit workflow.

3. **[#7030 — Ollama / qwen2.5-coder: tool calls shown as executed but no files written](https://github.com/anomalyco/opencode/issues/7030)** (22 comments, 18 👍)  
   Affects `write` and `edit` tools when using local Ollama models. No file changes happen despite successful-looking JSON output. Long-standing issue with high upvotes.

4. **[#16992 — Feature Request: add `/btw` command](https://github.com/anomalyco/opencode/issues/16992)** (15 comments, 85 👍)  
   Inspired by Claude Code's `/btw`, users want a quick way to insert non-contextual reminders. Highest upvoted feature request this month.

5. **[#7467 — GitHub-based Agent Marketplace](https://github.com/anomalyco/opencode/issues/7467)** (11 comments, 8 👍)  
   Proposal for sharing agents via GitHub repos, eliminating manual file copying. Strong community desire for discoverability.

6. **[#20287 — @ai-sdk/azure provider broken since v1.3.4](https://github.com/anomalyco/opencode/issues/20287)** (11 comments)  
   Azure OpenAI compatible provider fails with `/chat/completions`. Workaround needed for enterprise users.

7. **[#24148 — Bun panic on macOS: napi_create_error](https://github.com/anomalyco/opencode/issues/24148)** (9 comments, 2 👍)  
   macOS crash with embedded Bun runtime. Traces back to NAPI error creation; affects stability on Apple Silicon.

8. **[#25873 — Bash tool readonly property error in v1.14.34+](https://github.com/anomalyco/opencode/issues/25873)** (5 comments, 1 👍)  
   `Attempted to assign to readonly property` when executing shell commands. Confirmed regression due to minification changes.

9. **[#26123 — oh-my-openagent missing in desktop v1.14.40](https://github.com/anomalyco/opencode/issues/26123)** (4 comments)  
   Regression: the agent display panel no longer appears after upgrade. Windows desktop users affected.

10. **[#26103 — deepseek-v4-flash missing image modality](https://github.com/anomalyco/opencode/issues/26103)** (3 comments, closed)  
    Multimodal model definition missing `image` in input modalities, causing error when sending images. Fixed by quick model update.

## Key PR Progress

1. **[#11303 — ACP client expose input/output properly](https://github.com/anomalyco/opencode/pull/11303)** (open)  
   Fixes Zed integration (#10998) by sending `tool_call` with `kind: "execute"` correctly, making run commands visible in Zed.

2. **[#26147 — Add exit event fallback for child process close hang on Windows](https://github.com/anomalyco/opencode/pull/26147)** (open)  
   Solves the long-standing Windows hang when child processes spawn grandchildren (e.g., Gradle daemons). Uses `exit` event as fallback.

3. **[#26152 — Detect MIME type for `--file` flag instead of hardcoding text/plain](https://github.com/anomalyco/opencode/pull/26152)** (open)  
   Closes three issues (#16723, #24698, #25353) by dynamically detecting MIME type for file attachments.

4. **[#26150 — Handle cancel in upgrade process and customize spinner](https://github.com/anomalyco/opencode/pull/26150)** (open)  
   Fixes #26154: `Ctrl+C` during upgrade now cleanly aborts; spinner UX improved.

5. **[#12822 — Proxy directly to process.env instead of snapshotting](https://github.com/anomalyco/opencode/pull/12822)** (open)  
   Prevents stale environment variables by injecting a dynamic proxy into `Env` service, resolving runtime config mismatches.

6. **[#26148 — Refactor desktop main process to Effect-TS](https://github.com/anomalyco/opencode/pull/26148)** (open)  
   Modernizes desktop app architecture: auto-updater extracted, initialisation uses `Effect.gen`/`Fiber`, promise chains replaced. Improves error handling.

7. **[#26134 — Redirect Bun's tempdir when /tmp is mounted noexec](https://github.com/anomalyco/opencode/pull/26134)** (open)  
   Fixes silent hang on hardened Linux systems by detecting noexec and using an alternative temp directory.

8. **[#26140 — Build desktop package with Electron for Nix](https://github.com/anomalyco/opencode/pull/26140)** (open)  
   Updates Nix derivation to package the Electron app (Tauri tree removed), using shared `node_modules` and Nix-provided Electron.

9. **[#11629 — Container init script](https://github.com/anomalyco/opencode/pull/11629)** (closed)  
   Introduces custom entry scripts for development containers, deprecating multiple Docker images. Community-requested feature for reproducible environments.

10. **[#21801 — Forward subagent session events to ACP client](https://github.com/anomalyco/opencode/pull/21801)** (open)  
    Fixes bug where ACP clients missed subagent session events (new/load/close), breaking IDEs that depend on session lifecycle tracking.

## Feature Request Trends

The most demanded feature directions from recent issues include:

- **Quick context injection** – `/btw` command (85 👍) leads all requests, indicating users want lightweight, non-conversational notes.
- **Agent ecosystem** – A GitHub-based marketplace (#7467) and support for sharing agent configurations keep gaining traction.
- **Model & provider parity** – Requests for new model support (Gemini 3.1 Pro, deepseek multimodal, Opus 4.6) and fixing custom provider quirks are recurring.
- **Session management UX** – Features like `--continue` fail gracefully (#25989), session listing improvements (#25978, #15023), and session compression recovery (#24709) reflect pain points around state handling.
- **Cross-platform hardening** – Interest in daemon/heartbeat/memory features (#11570) signals a desire for more robust persistent environments.

## Developer Pain Points

- **Tool execution failures** – `edit`, `write`, and `bash` tools breaking on specific providers (Ollama, custom OpenAI) or after minification (readonly property) is the #1 frustration.
- **Platform crashes** – Bun panics on both Windows and macOS, desktop regressions (oh-my-openagent missing), and session deserialisation errors top the crash reports.
- **Provider compatibility bugs** – Azure, Bedrock, and custom OpenAI-compatible endpoints frequently regress on new releases, especially around reasoning blocks and multimodal inputs.
- **Sandboxing & permissions** – Clipboard failing in tmux, Bün tempdir issues on noexec systems, and child process hangs on Windows highlight environment-specific configuration headaches.
- **Localization & documentation** – Wrong Japanese translation (#26133) and outdated README claiming Tauri instead of Electron (#26143) show quality-of-life gaps that frustrate users.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-07

This week’s activity is dominated by the ongoing **big refactor** (label `closed-because-bigrefactor`), which has swept up dozens of closed issues and PRs. Despite that churn, several high-impact fixes landed, including critical delta handling for OpenAI completions, parallel extension loading for startup speed, and a comprehensive rollback architecture. Community discussions continue to focus on terminal rendering quirks (inline images, IME input) and provider-specific edge cases.

---

## Hot Issues (10 most noteworthy)

1. **[#4228](https://github.com/badlogic/pi-mono/issues/4228) — Fix openai-completions provider delta handling**  
   *Closed* · 17 comments · 0 👍  
   **Why it matters:** Deltas containing both `content` and `tool_calls` were accumulated incorrectly, breaking multi-turn agent workflows. The community quickly converged on a fix (see PR #4247). High engagement indicates this was a widespread blocker for OpenAI users.

2. **[#4208](https://github.com/badlogic/pi-mono/issues/4208) — Inline image previews corrupt terminal in cmux/Ghostty**  
   *Open* · 14 comments · 0 👍  
   **Why it matters:** The TUI’s Kitty graphics path fails inside `cmux`, a popular multiplexer. Users report that reverting to iTerm2 works fine, making this a platform-specific regression. No fix yet, and it’s blocking cmux users from using Pi’s image features.

3. **[#3108](https://github.com/badlogic/pi-mono/issues/3108) — Session becomes unrecoverable when model returns tool call with empty name**  
   *Closed* · 8 comments · 0 👍  
   **Why it matters:** A malformed tool call permanently corrupts session history, causing all subsequent API requests to fail with 400. This bug has been open for weeks; its closure (likely via refactor) is a relief for users who encounter flaky models.

4. **[#2717](https://github.com/badlogic/pi-mono/issues/2717) — Make context-file discovery configurable**  
   *Closed* · 7 comments · 4 👍  
   **Why it matters:** Hardcoded search paths (`AGENTS.md`, `CLAUDE.md`) forced many users to rely on workarounds. The 4 upvotes signal strong demand for customization—scope, accepted filenames, exclusions. Likely addressed in the refactor.

5. **[#4185](https://github.com/badlogic/pi-mono/issues/4185) — Zsh/tmux installation: bad colors/contrast**  
   *Open* · 5 comments · 1 👍  
   **Why it matters:** New npm users immediately notice poor color rendering in `tmux`. The issue includes screenshots showing washed-out interface; community suspects missing terminal capability detection. Still unresolved.

6. **[#4210](https://github.com/badlogic/pi-mono/issues/4210) — Bedrock converse-stream: empty end_turn treated as success**  
   *Closed* · 4 comments · 0 👍  
   **Why it matters:** Bedrock occasionally returns null responses instead of errors, causing the agent to trail off silently. A local extension workaround exists, but the community wants a core fix.

7. **[#4141](https://github.com/badlogic/pi-mono/issues/4141) — Expired tokens cause hung process**  
   *Closed* · 4 comments · 0 👍  
   **Why it matters:** When an `openai-codex` auth token expires mid-session, the process hangs without error. A clear UX regression that erodes trust; likely fixed in refactor.

8. **[#2909](https://github.com/badlogic/pi-mono/issues/2909) — Find and Grep tools referenced in prompt but not enabled**  
   *Closed* · 4 comments · 1 👍  
   **Why it matters:** Default system prompt mentions `find`/`grep` tools, but they’re only available via `--tools` flag. The community wants a permanent enable mechanism; this inconsistency confuses new users.

9. **[#3254](https://github.com/badlogic/pi-mono/issues/3254) — Add setting to prevent model switch from overwriting default**  
   *Closed* · 4 comments · 1 👍  
   **Why it matters:** Every `/model` command or Ctrl+P cycle overwrites the default model in `settings.json`. The requested `persistModelSelection` setting (default false) would give users control over this behavior.

10. **[#4253](https://github.com/badlogic/pi-mono/issues/4253) — Chinese IME input causes doubled/lost characters with Kitty keyboard protocol**  
    *Open* · 1 comment · 0 👍  
    **Why it matters:** Non-English users are directly affected; the bug corrupts input in VS Code terminal when Kitty protocol is enabled. A companion PR (#4252) has already been submitted (see below).

---

## Key PR Progress (10 important merges/open changes)

1. **[#4247](https://github.com/badlogic/pi-mono/pull/4247) — fix(ai): handle mixed chat completion deltas**  
   *Closed* by mitsuhiko  
   Separates accumulators for `reasoning_content`, `content`, and `tool_calls`. Fixes #4228. Tests are described as "clanker slop" — the fix is clean, the test code less so.

2. **[#4261](https://github.com/badlogic/pi-mono/pull/4261) — fix(tui): keep kitty image redraws inside TUI**  
   *Open* by mitsuhiko  
   Prevents Kitty graphics from bleeding outside the TUI scroll region. Includes a repro extension demonstrating corruption; the fix ensures images are cleared on line redraws.

3. **[#4259](https://github.com/badlogic/pi-mono/pull/4259) — feat: complete rollback architecture with 1300+ tests**  
   *Closed* by dyyz1993  
   A massive PR wiring `FileSnapshotManager` into `AgentSession` and thinning the file-snapshot extension. All 10 core test cases pass. This is a foundational feature for safe undo.

4. **[#4244](https://github.com/badlogic/pi-mono/pull/4244) — chore(coding-agent): switch back from fork to upstream jiti 2.7**  
   *Closed* by pi0  
   Moves from a custom jiti fork back to upstream, incorporating virtual modules and static bundling fixes. Reduces maintenance burden and gets the community on the latest jiti.

5. **[#4256](https://github.com/badlogic/pi-mono/pull/4256) — fix(openai-responses): multi-turn reasoning fails under store:false on Azure**  
   *Closed* by 0xnavarro  
   Azure OpenAI Responses returns a 400 on turn 2 when `store: false` is set. The fix conditionally enables `store` when the previous response ID is used — a critical patch for Azure customers.

6. **[#4242](https://github.com/badlogic/pi-mono/pull/4242) — perf(coding-agent): parallel extension loading via Promise.all**  
   *Closed* by samjonester  
   Swaps sequential `for...await` to `Promise.all` for extension imports. Directly addresses startup latency — especially impactful for users with 50+ extensions.

7. **[#4255](https://github.com/badlogic/pi-mono/pull/4255) — perf(coding-agent): shared jiti instance with moduleCache**  
   *Closed* by samjonester  
   Follow-up to #4242: hoists jiti to a lazy singleton and enables `moduleCache`. Together with #4242, extension loading time drops from ~1100ms to a fraction.

8. **[#4252](https://github.com/badlogic/pi-mono/pull/4252) — fix(tui): Chinese IME input dedup and Windows UTF-8 codepage**  
   *Closed* by catlain  
   Three fixes: deduplicate CSI-u sequences for IME, handle ambiguous-width characters in Kitty protocol, and add Windows UTF-8 codepage detection. Addresses #4253 and improves CJK support.

9. **[#4243](https://github.com/badlogic/pi-mono/pull/4243) — config selector: scale maxVisible to terminal height**  
   *Closed* by samjonester  
   Previously hardcoded `maxVisible = 15`; now dynamically computed from terminal height. With 50+ extensions, users no longer need to scroll 15 items at a time — usability win.

10. **[#4231](https://github.com/badlogic/pi-mono/pull/4231) — feat: mouse reporting + rendered-lines API for selection extensions**  
    *Closed* by mrmartineau  
    Adds `setMouseReporting()` and `getRenderedLines()` primitives, enabling extensions to implement copy-on-select, hover, and click actions. SGR 1006 mouse sequences flow through existing TUI input — extensibility improvement.

---

## Feature Request Trends

- **Configurable context-file discovery** (scope, filenames, exclusions) — #2717, #3360  
- **Persistent model selection** — prevent `/model` from overwriting `settings.json` (#3254)  
- **Native image generation** in interactive mode, mirroring Codex TUI (#4095)  
- **LSP and formatters by default** — automatic formatting on read/edit/write without extra setup (#4235)  
- **Python SDK for `pi-agent-core` and `pi-ai`** — enabling Python apps to reuse Pi libraries (#4174)  
- **Always show model provider in footer** — even with a single provider, to help project-specific configs (#4233)

---

## Developer Pain Points

- **Session-unrecoverable errors** — empty tool call names (#3108), expired tokens (#4141), transient WebSocket failures (#4257) all leave sessions permanently stuck or hung.  
- **Terminal rendering fragility** — inline images in `cmux` (#4208), Chinese IME doubling (#4253), scrollback destruction during streaming (#4260) degrade the interactive experience, especially in non-iTerm2 terminals.  
- **Provider-specific quirks** — Bedrock returns nulls instead of errors (#4210), Azure Responses fails with `store: false` (#4256), OpenAI GPT-5.5 blocks `off` thinking levels (#4249). Users need more robust fallbacks.  
- **Extension loading performance** — despite #4242/#4255 improvements, startup time with many extensions remains a pain point (original 1100ms for 64 extensions).  
- **MCP tool parameter type coercion** — all parameters sent as strings breaks boolean/number inputs (#4226).  
- **Model switching side effects** — `/model`, Ctrl+P cycling overwrite persistent defaults unless manually restored (#3254).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest – 2026-05-07

## Today's Highlights
The team shipped **v0.15.7** featuring a new `FileReadCache` for short‑circulating unchanged reads and a CLI proxy fix. A wave of performance and stability PRs landed — throttling shell tool live updates, normalising streaming deltas, and speeding up session‑list loading. On the feature side, an Agent Team experimental PR, a daemon server stage 1, and a light‑theme toggle for `/export` HTML all reached review.

## Releases
- **v0.15.7** ([release](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.7))  
  *What’s Changed*  
  - `feat(core)`: add `FileReadCache` and short‑circuit unchanged Reads ([#3717](https://github.com/QwenLM/qwen-code/pull/3717) by @wenshao)  
  - `fix(cli)`: honor proxy setting ([#37](https://github.com/QwenLM/qwen-code/pull/37) by @cyphercodes)  

- Also published as `v0.15.7-preview.2`, `v0.15.7-preview.1`, and `v0.15.6-nightly.20260507.15342b893` (identical changelog).

## Hot Issues (10 noteworthy)
1. **#3881** – [BUG] Local Qwen3.6‑27b model returns “/” repeatedly until token limit  
   *Author*: chn126943 | *Comments*: 4 | *Link*: [Issue #3881](https://github.com/QwenLM/qwen-code/issues/3881)  
   *Why matters*: Affects first‑turn behaviour with many local deployments; high frustration.

2. **#3878** – [BUG] `settings.json` context window value ignored  
   *Author*: fantasyz | *Comments*: 4 | *Link*: [Issue #3878](https://github.com/QwenLM/qwen-code/issues/3878)  
   *Why matters*: Misconfiguration leads to truncated conversations; common with custom model setups.

3. **#3678** – [Feature] Add light theme & toggle to `/export` HTML page  
   *Author*: justmcl | *👍*: 3 | *Link*: [Issue #3678](https://github.com/QwenLM/qwen-code/issues/3678)  
   *Why matters*: Users report eye strain from the only‑dark exported reports.

4. **#3634** – [Feature] Background task management roadmap & next steps  
   *Author*: wenshao | *Comments*: 2 | *Link*: [Issue #3634](https://github.com/QwenLM/qwen-code/issues/3634)  
   *Why matters*: Foundation for background agent resume, already partially merged.

5. **#3004** – [P1] API exponential backoff & fallback retry  
   *Author*: pomelo‑nwu | *Link*: [Issue #3004](https://github.com/QwenLM/qwen-code/issues/3004)  
   *Why matters*: Lack of backoff causes disruption on provider rate‑limits; acknowledged as P1.

6. **#3822** – [BUG] Session JSONL bloat after large file edits, `/resume` becomes extremely slow  
   *Author*: RunMintOn | *Closed* | *Link*: [Issue #3822](https://github.com/QwenLM/qwen-code/issues/3822)  
   *Why matters*: Root cause identified – `toolCallResult` storing full file diff without size limit.

7. **#3843** – [BUG] Qwen overrides `settings.json` on startup  
   *Author*: master‑vsv | *Link*: [Issue #3843](https://github.com/QwenLM/qwen-code/issues/3843)  
   *Why matters*: Destructive overwrite of user config; blocks customisation.

8. **#3823** – [BUG] `@qwen-code/sdk` 0.1.6/0.1.7 causes CLI process exit code 1  
   *Author*: flyshadowhan | *Link*: [Issue #3823](https://github.com/QwenLM/qwen-code/issues/3823)  
   *Why matters*: SDK upgrade regression; affects integrations.

9. **#3895** – [BUG] MCP health pill not refreshed after disabling MCP server via `/mcp`  
   *Author*: BZ‑D | *Link*: [Issue #3895](https://github.com/QwenLM/qwen-code/issues/3895)  
   *Why matters*: UI inconsistency confuses users about actual MCP status.

10. **#3906** – [Feature] PR Review Assistant: Risk Level & Cross‑PR Conflict Analysis via CodeGraph  
    *Author*: BingqingLyu | *Link*: [Issue #3906](https://github.com/QwenLM/qwen-code/issues/3906)  
    *Why matters*: Proposes AI‑assisted code review for large projects; aligns with OSS maintainer needs.

## Key PR Progress (10 important pull requests)
1. **#3902** – `fix(core): throttle shell tool live text updates` ([PR #3902](https://github.com/QwenLM/qwen-code/pull/3902))  
   *Author*: chiga0 | Prevents over‑rendering of streaming shell output; reduces CPU load.

2. **#3896** – `fix(core): normalise cumulative OpenAI stream deltas to suffixes` ([PR #3896](https://github.com/QwenLM/qwen-code/pull/3896))  
   *Author*: chiga0 | Fixes repeated text accumulation from certain DashScope upstreams.

3. **#3908** – `feat(web-templates): add light theme and toggle to /export HTML` ([PR #3908](https://github.com/QwenLM/qwen-code/pull/3908))  
   *Author*: dreamWB | Implements the requested light‑theme switch for exported reports.

4. **#3905** – `fix(cli): unfreeze Ctrl+O compact‑mode toggle on long conversations` ([PR #3905](https://github.com/QwenLM/qwen-code/pull/3905))  
   *Author*: chiga0 | Closes [#3899](https://github.com/QwenLM/qwen-code/issues/3899); fixes UI freeze.

5. **#3897** – `perf(core): bound session‑list metadata reads to head/tail 64KB` ([PR #3897](https://github.com/QwenLM/qwen-code/pull/3897))  
   *Author*: qqqys | Drastically improves `/resume` speed for large session files.

6. **#3894** – `feat(core): foreground → background promote integration` ([PR #3894](https://github.com/QwenLM/qwen-code/pull/3894))  
   *Author*: wenshao | Stage 2 of phase D(b) – Ctrl+B to send foreground shell to background.

7. **#2886** – `feat: add Agent Team experimental feature for parallel sub‑agent coordination` ([PR #2886](https://github.com/QwenLM/qwen-code/pull/2886))  
   *Author*: tanzhenxin | Major new architecture for parallel sub‑agents; gated by experimental flag.

8. **#3889** – `feat(cli,sdk): qwen serve daemon (Stage 1)` ([PR #3889](https://github.com/QwenLM/qwen-code/pull/3889))  
   *Author*: wenshao | HTTP daemon bridging ACP; closes part of [#3803](https://github.com/QwenLM/qwen-code/issues/3803).

9. **#3864** – `feat(cli): refactor auth around provider registry` ([PR #3864](https://github.com/QwenLM/qwen-code/pull/3864))  
   *Author*: pomelo‑nwu | Cleaner multi‑provider auth setup; supports custom providers.

10. **#3904** – `feat(cli): inline compact tree for live agents` ([PR #3904](https://github.com/QwenLM/qwen-code/pull/3904))  
    *Author*: tanzhenxin | Shows running sub‑agents as a compact tree in the live area.

## Feature Request Trends
- **Theme customisation** – Multiple requests for light‑mode / theme toggle in CLI banner and export HTML.
- **Background & sub‑agent visibility** – Users want more detailed live views of agent team progress and the ability to promote foreground shells to the background.
- **API reliability** – Exponential backoff, model fallback on 529, and token refresh are highly demanded.
- **MCP & ACP improvements** – Better integration with MCP servers (e.g., `/` slash commands in ACP mode, health pill refresh).
- **Daemon mode** – A persistent `qwen serve` process for CI/CD and IDE integration (formal proposal in [#3803](https://github.com/QwenLM/qwen-code/issues/3803)).
- **PR review assistant** – Automated risk‑level classification and dependency conflict detection using CodeGraph.
- **Session management** – Faster resume, memory optimisation for large files, and inline file autocomplete.

## Developer Pain Points
- **Startup config overwrite** – `settings.json` is silently replaced every launch ([#3843](https://github.com/QwenLM/qwen-code/issues/3843)).
- **Context window ignored** – Custom `contextWindowSize` setting not honoured for local models ([#3878](https://github.com/QwenLM/qwen-code/issues/3878)).
- **CLI freeze on long sessions** – Ctrl+O and paste of multi‑line content cause UI hangs ([#3899](https://github.com/QwenLM/qwen-code/issues/3899), [#3901](https://github.com/QwenLM/qwen-code/issues/3901)).
- **MCP health indicator stale** – After disabling a server, the footer pill does not update ([#3895](https://github.com/QwenLM/qwen-code/issues/3895)).
- **SDK regression** – Upgrading `@qwen-code/sdk` from 0.1.5 to 0.1.6 introduces random CLI exits ([#3823](https://github.com/QwenLM/qwen-code/issues/3823)).
- **Wayland paste broken** – Image pasting fails on Wayland despite having `wl-clipboard` installed ([#3829](https://github.com/QwenLM/qwen-code/issues/3829)).
- **ACP multilingual inconsistency** – Thinking process always uses English even when user requests another language ([#3787](https://github.com/QwenLM/qwen-code/issues/3787)).
- **Separate CLI/VS Code updates** – Users must update both independently, leading to version mismatch ([#3891](https://github.com/QwenLM/qwen-code/issues/3891)).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*