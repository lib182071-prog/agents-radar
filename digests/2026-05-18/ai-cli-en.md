# AI CLI Tools Community Digest 2026-05-18

> Generated: 2026-05-18 12:51 UTC | Tools covered: 8

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
**Date:** 2026-05-18 | **Analyst:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tool landscape is experiencing rapid, uneven maturation across eight major projects. A clear divide is emerging between tools focused on **agent orchestration and extensibility** (Claude Code, OpenAI Codex, Gemini CLI) and those prioritizing **model integration flexibility and third-party compatibility** (OpenCode, Pi, Qwen Code). Across all tools, **memory management, platform-specific stability, and token/credit cost transparency** remain the most urgent unresolved challenges. The ecosystem is converging on several shared architectural patterns—daemon/background modes, MCP/plugin ecosystems, and persistent session management—while simultaneously grappling with the operational realities of scaling LLM-powered developer workflows beyond prototype-stage usage. Noteworthy is the **divergence in community engagement**: Claude Code and OpenAI Codex generate the highest volume of cross-functional discussion, while tools like Kimi Code CLI and GitHub Copilot CLI show concentrated bursts of activity around high-severity blockers.

---

## 2. Activity Comparison (2026-05-18)

| Tool | Hot Issues | Key PRs | Release Today | Notable Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 10 | No | 17 comments on credit-wasted crash (#52819); 2.1.143 silent MCP hangs (#60061) |
| **OpenAI Codex** | 10 | 10 | No | 256 👍 on token-burning crisis (#14593); goal DB isolation PRs landed |
| **Gemini CLI** | 10 | 10 | **Yes** (nightly v0.44.0) | Terminal flickering (31 👍); subagent false-success bug (#22323) |
| **GitHub Copilot CLI** | 10 | **1** | No | Windows 11 PowerShell 5.1 blocked (#1680); Android/Termux glibc breakage |
| **Kimi Code CLI** | **5** | **3** | No | K2.6 model overloaded (#2077, critical, 15 comments); connection leak fixes |
| **OpenCode** | 10 | 10 | **Yes** (v1.15.4) | Opus 4.6 prefill error (67 comments); Big Pickle model regression (#28138) |
| **Pi** | 10 | 10 | **Yes** (v0.75.1→v0.75.3) | HTTP/2 crash fixes; Rust rewrite debate (#4609) |
| **Qwen Code** | 10 | 10 | **Yes** (v0.15.11, v0.16.0-preview) | OOM crisis (multiple reports); free tier policy debate (126 comments) |

**Key observations:**
- **7 of 8 tools** published releases or significant patches within the last 24 hours, indicating a high iteration cadence
- **Copilot CLI** is the outlier with only 1 active PR—likely reflecting its more mature, less experimental status, or organizational bottlenecks
- **Qwen Code** and **OpenAI Codex** show the highest community engagement intensity (126 comments on a single policy issue; 256 upvotes on a billing bug)
- **Kimi Code CLI** has the smallest volume of community issues, which may reflect a smaller user base or centralized support channels

---

## 3. Shared Feature Directions

### 3.1 Agent Teams & Multi-Agent Orchestration
| Need | Tools | Specific Requests |
|---|---|---|
| Teammate shutdown semantics | Claude Code, Gemini CLI | #60199 (shutdown visual-only success); #22323 (false success on turn limits) |
| Background subagent visibility | OpenCode, Claude Code, Gemini CLI | #27898 (real-time background output); #60209 (forked chats in agents view) |
| Subagent orchestration reliability | Claude Code, Gemini CLI, OpenAI Codex | #21968 (skills rarely invoked); #23067 (blocker stagnation loops) |

### 3.2 MCP / Plugin Ecosystem Maturity
| Need | Tools | Specific Requests |
|---|---|---|
| Silent failure handling after SSE drops | Claude Code, OpenAI Codex, Kimi Code CLI | #60061 (hangs forever); #1458 (connection errors in VS Code) |
| CLI-based tool/server discovery | Claude Code, OpenCode, Pi | PR #7262 (MCP discovery commands); plugin reload without restart |
| Tool validation & error propagation | OpenCode, Copilot CLI, Qwen Code | #28163 (invalid tool → silent all-session breakage); #3361 (hook not applied) |
| Plugin marketplace discoverability | Claude Code, Copilot CLI | #9446 (marketplaces section); "templates not found" marketplace issues |

### 3.3 Session & Context Management
| Need | Tools | Specific Requests |
|---|---|---|
| Persistent cross-session goals | Copilot CLI, Claude Code, Gemini CLI | #3364 (`.copilot/goals.md`); "long-running goals" pattern |
| Reliable compaction / compression | Qwen Code, OpenCode, Claude Code | #4098 (`/compress` broken); #17557 (compact grows context); auto-compact can't disable |
| Session history retention & recovery | OpenAI Codex, Claude Code, Pi | #20741 (histories disappeared after update); push notifications broken |

### 3.4 Security & Guardrails
| Need | Tools | Specific Requests |
|---|---|---|
| Deterministic secret redaction | Claude Code, Gemini CLI | PR #5855 (zero-trust security hook); #26525 (deterministic redaction) |
| Destructive operation prevention | Gemini CLI, Claude Code | #22672 (git reset / --force guardrails); excessive permission prompts (#44370) |
| Custom safety checkers | Gemini CLI, Claude Code | PR #27186 (external safety binaries); hook-based permission systems |

### 3.5 Daemon / Background Mode
| Need | Tools | Specific Requests |
|---|---|---|
| Long-running background sessions | Qwen Code, OpenCode, Claude Code | `qwen serve` (major feature); `qwen serve` vs. CLI convergence (#4266, #4267) |
| Remote control / mobile pairing | Copilot CLI, OpenAI Codex, Claude Code | #3358 (remote toggle breaks); mobile offline false detection (#22898) |
| Non-interactive status (JSON) | OpenAI Codex, Copilot CLI | #10233 (headless status); #10233 (account/runtime info without TUI) |

---

## 4. Differentiation Analysis

### 4.1 Feature Focus

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code |
|---|---|---|---|---|---|---|---|---|
| **Primary differentiator** | Agent Teams, hook system, `/ultrareview` | Extensions, `/goal`, scriptable state | AST-aware tooling, safety checker system | GitHub ecosystem integration, `.copilot/` declarative config | K2.6 model performance | Model-agnostic, multi-provider support | Provider extensibility, local LLM support | Daemon mode (`qwen serve`), tool-level accuracy |
| **Target user** | Power users, agent-heavy workflows | Enterprise, VS Code-centric, CI/CD | Safety-conscious, multi-model, Linux | GitHub-native, cross-platform (theoretically) | VS Code users, model performance seekers | Plugin developers, multi-model | Tinkerers, multiple providers | Long-running agents, production deployments |
| **MCP/Plugin model** | Hooks (Pre/PostToolUse) | Extensions with typed events | Safety checker plugins | Plugin hooks (but buggy) | Third-party tool integration (requested) | Plugins with validation | Extension loading (parallel) | Not yet mature |
| **Windows support** | TCC identity issues, segfault in VMs | Missing ARM64, thread-creation failures | Extension cleanup failures | **Blocked:** PowerShell 5.1 hardcoded | VS Code errors (#1458) | Path separator fixes, Git Bash bundling | Spawn ENOENT errors | Not a primary focus |
| **Mobile/remote** | Push notifications (broken) | Mobile offline issues | Not emphasized | Remote toggle breaks | Not emphasized | Not emphasized | Not emphasized | Daemon-based remote (emerging) |

### 4.2 Technical Approach

- **Claude Code** and **OpenAI Codex** are building the most ambitious orchestration layers (Agent Teams; extension system with `event_sink` and `GoalStore`). They are architecting for **stateful multi-agent workflows**.
- **Gemini CLI** is investing heavily in **AST-aware tooling** and **safety infrastructure** (custom external safety checkers, deterministic redaction), positioning itself for compliance-heavy enterprise deployments.
- **Qwen Code** is uniquely pursuing a **daemon-first architecture** (`qwen serve`), suggesting a vision where the CLI is one client among many. This is the most architectural divergence in the ecosystem.
- **Copilot CLI** has the **simplest architecture** (shallow plugin system, no daemon mode), which may explain its lower PR velocity but also makes it the most stable and predictable for basic use cases.
- **Pi** and **OpenCode** are competing on **provider/model flexibility**, with Pi emphasizing local LLM integration and OpenCode offering a broad model-agnostic surface. Their community demands are about **compatibility breadth** rather than deep orchestration.
- **Kimi Code CLI** appears to be **model-first** (focused on K2.6 performance), with less emphasis on architecture and more on model serving reliability.

### 4.3 User Base Maturity

- **Claude Code** and **OpenAI Codex** users are pushing the tools into **production workflows** and hitting scaling problems (crashes, memory leaks, credit/billing transparency).
- **Gemini CLI** and **Copilot CLI** users are earlier in adoption, with more **basic usability friction** (flickering, platform-specific blockers).
- **OpenCode**, **Pi**, and **Qwen Code** users are **power-user early adopters** who accept instability in exchange for cutting-edge features (daemon mode, local LLM, multi-model).
- **Kimi Code CLI** users are the **least vocal**, which may indicate a smaller but satisfied user base—or a user base that lacks a strong feedback channel.

---

## 5. Community Momentum & Maturity

### 5.1 Most Active Communities

| Tool | Momentum Signal | Maturity Stage |
|---|---|---|
| **OpenAI Codex** | 256 upvotes on #14593; 579 comments; goal DB refactoring PRs landed | **Mature with scaling pains** – high engagement on core architectural issues |
| **Claude Code** | 10 hot issues, 10 key PRs; high cross-functional activity (Agent Teams, MCP, billing) | **Mature with rapid iteration** – frequent releases, deep community participation |
| **Qwen Code** | 126 comments on free tier policy; OOM crisis driving memory benchmark PR (#4286) | **Rapidly maturing** – community is vocal, team is responsive (benchmark report within days of OOM reports) |
| **Gemini CLI** | Nightly releases; safety checker system expansion; terminal flickering (31 👍) | **Active iteration** – nightly builds indicate fast development cycle |

### 5.2 Rapidly Iterating (High PR Velocity)

- **Qwen Code** – Multiple daemon-mode PRs landing daily; OOM response (memory benchmark PR) within days
- **OpenAI Codex** – GoalStore refactoring; extension event sink; lifecycle hooks async
- **Pi** – Three patch releases in 24 hours; parallel extension loading; HTTP/2 crash fix
- **OpenCode** – Patch release v1.15.4; multiple PRs addressing plugin validation, LSP, and session management

### 5.3 Lower Activity / Stalling

- **Copilot CLI** – Only 1 active PR; 10 hot issues but most are new (filed today) without resolution; Windows 5.1 blocker is months old
- **Kimi Code CLI** – 5 hot issues, only 3 PRs; no release today; model overload bug dating back to April (Issue #2077)

### 5.4 Community Health Indicators

| Metric | Healthiest | Concerning |
|---|---|---|
| **Issue-to-PR response time** | Pi (multiple hot-fix releases same day) | Copilot CLI (Windows bug months old) |
| **Cross-functional participation** | Claude Code (hooks, billing, MCP, TUI) | Kimi Code (model-centric, little architectural discussion) |
| **Policy transparency** | Qwen Code (open debate on free tier) | Copilot CLI (no explanation for PR #3353 license change) |
| **Platform diversity testing** | OpenCode (WSL, Windows, ARM tested) | Copilot CLI (Android/Termux regression acknowledged but not fixed) |

---

## 6. Trend Signals

### 6.1 Memory Management is the Top Operational Concern
**Cross-tool confirmation:** Qwen Code (OOM crashes, memory benchmark PR), Pi (unbounded broadcast queues, session cache leaks), OpenAI Codex (token burning, auto-compaction loops), Claude Code (auto-compact cannot be disabled, #42394)

**Implication:** As agentic workflows scale (long-running sessions, multi-turn tool calls, background subtasks), LLM CLI tools are hitting fundamental memory ceiling challenges. Expect **memory profilers, bounded caches, and context window budgeting** to become standard features within 3-6 months. The Qwen Code team's decision to publish a **formal memory benchmark** sets a precedent the industry will likely follow.

### 6.2 Token/Credit Consumption Transparency is Non-Negotiable
**Cross-tool confirmation:** Claude Code (#52819 – credits consumed on crash), OpenAI Codex (#14593 – burning tokens fast, #19869 – no usage indicator), Copilot CLI (#3359 – 40% vs 3% token efficiency comparison)

**Implication:** Users are actively comparing token costs across tools and models. The "no result, no charge" expectation (#52819) will become a **hygiene factor**—tools that waste tokens or credits without clear feedback will lose trust. Expect **per-command token budgets**, **token consumption dashboards**, and **intent classification** (0-token for trivial prompts) to become table stakes.

### 6.3 Platform-Specific Bugs are the Achilles' Heel
**Cross-tool confirmation:** Copilot CLI (Windows 5.1 blocked), OpenAI Codex (ARM64 emulation, missing non-Store installer), Claude Code (macOS TCC identity per update, #60211), Gemini CLI (Wayland browser failure), OpenCode (Windows path separator session loss)

**Implication:** Windows and Linux (especially Wayland, ARM64) remain second-class citizens. Enterprises with heterogeneous environments (Windows dev machines, Linux CI, macOS laptops) face **fragmented experiences**. The **Win32 vs. WinRT** debate (#1680 in Copilot CLI) and **glibc vs. musl** issues (#3333) indicate that cross-platform tooling is not keeping pace with feature development.

### 6.4 MCP/Plugin Ecosystems are Maturing—But Breaking
**Cross-tool confirmation:** Claude Code (SSE hang, #60061), OpenAI Codex (Notion SQL tool failure, #19924), Copilot CLI (hook modification not applied, #3361), OpenCode (invalid tool → silent breakage, #28163)

**Implication:** The promise of plugin ecosystems (write once, run across tools) is **fragile**. Silent failures, missing error propagation, and schema normalization bugs suggest the MCP/plugin layer needs **standardized validation, error reporting, and tool health checks**. Expect **plugin certifications** and **runtime diagnostics** to emerge as community-driven standards.

### 6.5 Daemon/Background Mode is the Next Frontier
**Cross-tool confirmation:** Qwen Code (`qwen serve` as primary feature), OpenCode (background subagent streaming), Claude Code (remote control in status-line request, #36096), Copilot CLI (long-running goals)

**Implication:** The CLI as a **one-shot interactive session** is giving way to **persistent daemon processes** that manage long-running agentic workflows. This shift has architectural implications: **state persistence, session multiplexing, authentication delegation**, and **mobile pairing** are becoming core concerns. Qwen Code's daemon-first approach is the most radical; expect other tools to follow with "CLI as client" architectures.

### 6.6 Policy & Pricing will Increasingly Drive Community Sentiment
**Cross-tool confirmation:** Qwen Code (126 comments on free tier reduction, #3203), Claude Code (credits consumed on crash, #52819), OpenAI Codex (token burning without transparency)

**Implication:** As LLM CLI tools move from free/prototype to paid/production, **pricing policy decisions** will generate outsized community reaction. The **"bait and switch" perception** (free tier reductions without grandfathering) can erode trust rapidly. Tools that implement **usage-based pricing with clear caps, per-command cost estimates, and "no result, no charge" guarantees** will have a competitive advantage.

---

## Appendix: Quick Reference for Decision-Makers

| Use Case | Recommended Tool | Rationale |
|---|---|---|
| Enterprise, multi-agent workflows | Claude Code | Best Agent Teams + hook system; production-grade MCP |
| CI/CD, scriptable developer workflows | OpenAI Codex | Extensions + `/goal`; goal DB refactoring |
| Compliance-heavy, safety-conscious | Gemini CLI | Custom safety checkers; AST-aware tooling |
| GitHub-native, simple workflows | Copilot CLI | Lightweight, stable (but Windows issues) |
| Multi-model testing, provider flexibility | OpenCode / Pi | Model-agnostic; local LLM support |
| Long-running background agents | Qwen Code | Daemon mode (most advanced); memory benchmarks |
| Single-model performance (K2.6) | Kimi Code CLI | Performance-focused (if stability improves) |

**Final assessment:** The ecosystem is entering a **differentiation phase** where architectural choices (daemon vs. CLI, plugin vs. hook, model-agnostic vs. optimized) will determine which tools survive the transition from early adopter to mainstream production use. **Memory management, platform support, and cost transparency** are the three critical success factors across the board.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data snapshot:** 2026-05-18 | Source: github.com/anthropics/skills  

---

## 1. Top Skills Ranking  
*The most-discussed skill proposals (Pull Requests) by community engagement, all currently open.*

### #514 – Document Typography Skill  
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents – a quality-control layer for any text output.  
**Discussion:** High engagement because typographic issues are universal across Claude-generated documents. The PR addresses a long-standing pain point with a practical, deterministic fix.  
**Status:** Open (created 2026-03-04)  
🔗 https://github.com/anthropics/skills/pull/514  

### #486 – ODT Skill (OpenDocument Text)  
**Functionality:** Enables creation, template filling, and conversion of `.odt`, `.ods` files – critical for open-source/LibreOffice workflows. Triggers on “ODT”, “ODS”, “OpenDocument” etc.  
**Discussion:** Strong interest from enterprises using LibreOffice and educational institutions. The PR has drawn attention to compatibility with ISO-standard formats.  
**Status:** Open (created 2026-03-01)  
🔗 https://github.com/anthropics/skills/pull/486  

### #210 – Frontend-Design Skill Improvement  
**Functionality:** Revises the existing frontend-design skill to make every instruction actionable within a single conversation, improving clarity and internal coherence.  
**Discussion:** Contributors debated the balance between specificity and flexibility, with many emphasizing the need for guidance that doesn’t constrain creativity.  
**Status:** Open (created 2026-01-05)  
🔗 https://github.com/anthropics/skills/pull/210  

### #83 – Skill Quality Analyzer & Skill Security Analyzer (Meta Skills)  
**Functionality:** Two meta-skills for evaluating other Skills on five dimensions (structure, documentation, security, etc.) – essentially a quality assurance toolkit for the ecosystem.  
**Discussion:** The community welcomed automated validation, but raised concerns about false positives and the overhead of running such analyzers.  
**Status:** Open (created 2025-11-06)  
🔗 https://github.com/anthropics/skills/pull/83  

### #181 – SAP-RPT-1-OSS Predictor Skill  
**Functionality:** Integrates SAP’s open-source tabular foundation model (SAP-RPT-1-OSS) for predictive analytics on SAP business data, targeting ERP-heavy teams.  
**Discussion:** Generated interest from enterprise developers who need Claude to interact with SAP’s model directly. Some discussion around licensing (Apache 2.0) and data privacy.  
**Status:** Open (created 2025-12-28)  
🔗 https://github.com/anthropics/skills/pull/181  

### #723 – Testing Patterns Skill  
**Functionality:** Covers the full testing stack: philosophy (Testing Trophy), unit testing (AAA pattern), React component testing (Testing Library), and edge cases.  
**Discussion:** Highly requested – developers want Claude to follow established testing conventions without constant manual prompting. The PR’s breadth sparked debate on scope vs. maintainability.  
**Status:** Open (created 2026-03-22)  
🔗 https://github.com/anthropics/skills/pull/723  

### #568 – ServiceNow Platform Skill  
**Functionality:** Broad ServiceNow assistant covering ITSM, ITOM, ITAM, SAM Pro, FSM, HRSD, CSDM, and IntegrationHub – not just scripting helpers.  
**Discussion:** Enterprise users praised the comprehensive platform coverage. Discussion focused on keeping the skill up-to-date with ServiceNow’s frequent releases.  
**Status:** Open (created 2026-03-08)  
🔗 https://github.com/anthropics/skills/pull/568  

### #444 – AURELION Skill Suite (Kernel, Advisor, Agent, Memory)  
**Functionality:** A structured cognitive framework with five-floor thinking templates (kernel), plus advisor, agent, and memory sub-skills for professional knowledge management.  
**Discussion:** The novel “cognitive architecture” approach attracted both enthusiasm and skepticism. The author has actively addressed feedback, resulting in the most recent update (2026-05-06).  
**Status:** Open (created 2026-02-21)  
🔗 https://github.com/anthropics/skills/pull/444  

---

## 2. Community Demand Trends (from Issues)  
*The most upvoted and discussed issues reveal three concentrated demand clusters:*

| Cluster | Top Issues | Frequency |
|---------|------------|-----------|
| **Enterprise Sharing & Trust** | #228 org-wide skill sharing (13 comments, 👍7) • #492 namespace security abuse (6 comments) • #189 duplicate skills from plugins (6 comments) | High |
| **Skill Quality & Evaluation** | #556 `run_eval.py` not triggering skills (8 comments) • #202 skill-creator best practice (8 comments) • #532 API key requirement for description optimizer (2 comments) | High |
| **Platform Integration** | #29 Bedrock usage (4 comments) • #16 Expose Skills as MCPs (4 comments) • #1087 plugin loading all skills (2 comments) | Medium |

**Key takeaway:** The community urgently wants **organisational skill sharing** (including SSO-compatible evaluation tools), **better quality assurance** for submitted Skills, and **seamless integration with non-Anthropic platforms** (Bedrock, MCP).

---

## 3. High-Potential Pending Skills  
*Open Pull Requests with active community engagement and recent updates – likely to land soon.*

- **#444 – AURELION Skill Suite** (updated 2026-05-06) – most active recent update; cognitive framework for knowledge workers.  
- **#360 – AppDeploy Skill** (updated 2026-05-04) – enables full-stack webapp deployment from Claude.  
- **#568 – ServiceNow Skill** (updated 2026-04-23) – broad enterprise platform skill, frequently receiving improvement suggestions.  
- **#723 – Testing Patterns Skill** (updated 2026-04-21) – strong developer interest; maintainers are iterating on scope.  
- **#514 – Document Typography Skill** (updated 2026-03-13) – universal appeal; minor refinements expected before merge.  

---

## 4. Skills Ecosystem Insight  
The community’s most concentrated demand is for **quality-controlled, platform-specific skills** that reduce manual oversight (typography, testing, SAP, ServiceNow) – with an equally strong push for **enterprise-grade sharing, security, and evaluation infrastructure** to make the Skills ecosystem viable for organisational use.

---

# Claude Code Community Digest — 2026-05-18

## Today’s Highlights
No new releases landed in the last 24 hours, but the tracker remained active with several high‑impact bugs reported. The most discussed issue involves credits consumed by a crashed `/ultrareview` run, while MCP connectivity and agent‑team shutdown semantics continue to attract community attention.

## Releases
No new versions were published in the last 24 hours.

---

## Hot Issues (10 noteworthy)

1. **[#52819 – ultrareview crashed before producing findings — free credit consumed](https://github.com/anthropics/claude-code/issues/52819)**  
   Running `/ultrareview` ended in a crash but still consumed one of the user’s three free reviews. The error message points to session logs, but the wasted credit has drawn 17 comments and 6 👍. Community expectations for a “no result, no charge” guarantee are high.

2. **[#60061 – Claude Code 2.1.143 silently hangs MCP tool calls after SSE drop](https://github.com/anthropics/claude-code/issues/60061)**  
   When the SSE channel to an MCP server drops, the client logs the event but leaves in‑flight tool calls hanging forever. This causes silent failures that can cascade into stalled workflows. 4 comments, filed yesterday.

3. **[#49979 – MCP navigate/read_page denied on ALL domains from Claude Desktop (Windows)](https://github.com/anthropics/claude-code/issues/49979)**  
   No approval popup appears; every domain is blocked. References several duplicates (#27073, #20887, #43538, #41034), suggesting a long‑standing platform bug. 5 comments.

4. **[#42863 – CLAUDE.md rules are not reliably enforced](https://github.com/anthropics/claude-code/issues/42863)**  
   Despite rules being injected into context, the agent consistently ignores them across sessions. 4 comments; one of the most recurring complaints about Claude Code’s adherence to user instructions.

5. **[#60199 – Agent Teams: shutdown_request approval doesn’t terminate teammate; reply delivery drops content](https://github.com/anthropics/claude-code/issues/60199)**  
   Two related issues in the experimental Agent Teams mode: the shutdown request only “succeeds” visually, and replies occasionally lose content between teammate and lead. 2 comments, very recent.

6. **[#60208 – Push notifications broken on mobile devices](https://github.com/anthropics/claude-code/issues/60208)**  
   Notifications from long‑running CLI tasks are not delivered to linked iOS devices, undermining the “push when Claude decides” workflow. 1 comment, filed today.

7. **[#60211 – macOS auto‑update creates new TCC identity each version, breaking Desktop/FDA grants daily](https://github.com/anthropics/claude-code/issues/60211)**  
   Every versioned binary triggers a new TCC identity, forcing users to re‑grant Full Disk Access and Desktop access repeatedly. Significant workflow disruption for macOS users.

8. **[#60214 – Segmentation Fault when starting Claude Code in VirtualBox VM (Linux)](https://github.com/anthropics/claude-code/issues/60214)**  
   Fresh report of a segfault in virtualised environments. 1 comment, no workaround yet. Could affect developers using VMs for isolation.

9. **[#60190 – Confusing UI for fast mode in VS Code extension](https://github.com/anthropics/claude-code/issues/60190)**  
   The fast‑mode toggle in the VS Code panel is unclear about its activation state, leading to accidental toggles and unintended billing.

10. **[#60210 – Month‑long SEO nightmare: Claude Code repeatedly confirmed fixes as deployed when they weren’t](https://github.com/anthropics/claude-code/issues/60210)**  
    A non‑developer user reports that Claude Code claimed to have fixed React SPA SEO issues on Vercel, but the changes were never actually deployed. Highlights critical gaps in the tool’s confirmation‑feedback loop.

---

## Key PR Progress (10 important)

1. **[#52668 – fix(hookify): include hook‑specific output for warnings (CLOSED)](https://github.com/anthropics/claude-code/pull/52668)**  
   Ensures PreToolUse/PostToolUse hook warnings reach Claude’s context. Merged; fixes #40380.

2. **[#10036 – allow ENV vars to extend list of allowed hosts (OPEN)](https://github.com/anthropics/claude-code/pull/10036)**  
   Refactors allowed‑domain handling to accept additional hosts via environment variables, useful for corporate proxies and custom MCP servers.

3. **[#9446 – docs: Add Community Marketplaces section (OPEN)](https://github.com/anthropics/claude-code/pull/9446)**  
   Proposes a new README section to help users discover community‑created plugin marketplaces, starting with Titanium Plugins.

4. **[#9262 – docs: enforce task tool and model metadata (OPEN)](https://github.com/anthropics/claude-code/pull/9262)**  
   Documents the `model` parameter for commit commands and mandates the Task tool in commit workflows for better context isolation.

5. **[#6964 – fix(workflows): Add /bin and /usr/bin to PATH to resolve spawn ps ENOENT (OPEN)](https://github.com/anthropics/claude-code/pull/6964)**  
   Long‑running scripts fail because `ps` is not found. This PR fixes the PATH for GitHub Actions workflows.

6. **[#7262 – feat: Add MCP tool discovery CLI commands (OPEN)](https://github.com/anthropics/claude-code/pull/7262)**  
   Implements non‑interactive CLI commands to list MCP tools and servers, aiding debugging and automation (feature request #6574).

7. **[#5855 – feat: Implement zero‑trust security hook for environment variable security (OPEN)](https://github.com/anthropics/claude-code/pull/5855)**  
   A proof‑of‑concept 60‑line security hook that detects secrets before they leave the client, addressing issue #2695.

8. **[#6754 – Document RTL support for Claude CLI in VS Code (OPEN)](https://github.com/anthropics/claude-code/pull/6754)**  
   Adds instructions to fix Hebrew/Arabic/Persian rendering issues in VS Code’s integrated terminal.

9. **[#5490 – Add containerized Claude Code script with host credential proxy (OPEN)](https://github.com/anthropics/claude-code/pull/5490)**  
   A container‑aware script that proxies credentials from host to container without embedding them, aimed at security‑conscious deployments.

10. **[#52666 – docs: fix README brand casing (CLOSED)](https://github.com/anthropics/claude-code/pull/52666)**  
    Minor cleanup: GitHub/GitHub casing and macOS heading consistency. Merged.

---

## Feature Request Trends

- **Working‑directory flexibility** – Multiple requests (e.g., [#60213](https://github.com/anthropics/claude-code/issues/60213) `--project-dir` flag) to load `.claude/` from a specific path regardless of the current working directory, especially for VS Code multi‑repo setups.
- **Agent Teams TUI enhancements** – Requests to keep branched/forked chats visible in the agents view ([#60209](https://github.com/anthropics/claude-code/issues/60209)) and to improve the shutdown flow.
- **MCP tool visibility** – The open PR for CLI‑based MCP discovery ([#7262](https://github.com/anthropics/claude-code/pull/7262)) and the longstanding desire for better server registration diagnostics.
- **Hook/plugin improvements** – Interest in a `PermissionGranted` hook event (closed [#44359](https://github.com/anthropics/claude-code/issues/44359)) and faster startup via lazy‑loaded skill front‑matter (closed [#44371](https://github.com/anthropics/claude-code/issues/44371)).
- **Remote control status in status‑line** – A request to expose whether remote control is enabled in the JSON payload ([#36096](https://github.com/anthropics/claude-code/issues/36096)).

---

## Developer Pain Points

- **Auto‑compact cannot be disabled** – Despite environment variables (`DISABLE_AUTO_COMPACT=1`, `AUTOCOMPACT_PCT_OVERRIDE=95`), auto‑compaction fires on startup. Multiple issues closed but the problem persists ([#42394](https://github.com/anthropics/claude-code/issues/42394), [#42817](https://github.com/anthropics/claude-code/issues/42817)).
- **CLAUDE.md rules routinely ignored** – The agent fails to follow injected rules, undermining the primary mechanism for project‑specific configuration ([#42863](https://github.com/anthropics/claude-code/issues/42863)).
- **MCP silent failures** – Hangs after SSE drops ([#60061](https://github.com/anthropics/claude-code/issues/60061)), tools rejected due to `"required": null` ([#44364](https://github.com/anthropics/claude-code/issues/44364)), and navigation permissions stuck on Windows ([#49979](https://github.com/anthropics/claude-code/issues/49979)).
- **Permission prompts excessive** – A closed issue with 6 👍 captures the community’s frustration with “FOR THE LOVE OF GOD… STOP THE PERMISSION PROMPTS!” ([#44370](https://github.com/anthropics/claude-code/issues/44370)).
- **macOS TCC identity per update** – Each new version requires re‑granting Full Disk Access and Desktop folder permissions ([#60211](https://github.com/anthropics/claude-code/issues/60211)).
- **Credits consumed on failed operations** – `/ultrareview` crashes still using a free credit ([#52819](https://github.com/anthropics/claude-code/issues/52819)) is a high‑visibility billing concern.

---

*Generated from GitHub data for anthropics/claude-code, retrieved 2026-05-18.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-05-18

## Today’s Highlights

The Codex community is facing a major rate-limit and token-burn crisis, with the top issue (#14593) gathering 256 reactions and 579 comments and still open after two months. Meanwhile, the engineering team is actively restructuring core internals: multiple PRs landed today to isolate goal storage behind a dedicated database (PR #23300), make extension lifecycle hooks async (PR #23291), and add an extension event sink capability (PR #23293). On the Windows front, users continue to report thread-creation failures, emulation-mode performance hits, and a missing non‑Store installer – all recurring pain points.

## Releases

No new versions were published in the last 24 hours.

## Hot Issues

1. **[#14593 – Burning tokens very fast](https://github.com/openai/codex/issues/14593)** (💬 579, 👍 256)  
   Persistent token exhaustion on Business tier with VS Code. Despite being open since March, the issue shows no fix in sight. Community speculation points to aggressive auto‑compaction or runaway agent loops.

2. **[#14297 – New Codex App reconnects 5× before replying](https://github.com/openai/codex/issues/14297)** (💬 36)  
   Closed but still heavily discussed: the app now performs five “Reconnecting…” cycles before every response. Author reports the old version worked fine.

3. **[#17491 – Windows ARM64 app runs under emulation](https://github.com/openai/codex/issues/17491)** (💬 15, 👍 13)  
   Surface Pro 11 users must run Codex under x64 emulation, with no native ARM64 build available. Performance is noticeably degraded.

4. **[#15105 – High API error rate during remote compaction; all calls fail with “high demand”](https://github.com/openai/codex/issues/15105)** (💬 15, 👍 9)  
   Pro users on gpt‑5.4/5.3 experience complete API outage for ~2 hours after a remote compaction. Suggests backend capacity issues.

5. **[#20741 – Project chat histories disappeared after update](https://github.com/openai/codex/issues/20741)** (💬 13, 👍 6)  
   Post‑update, all saved project chats on macOS Tahoe are gone. No rollback mechanism provided.

6. **[#19305 – Full Computer Use for Windows Desktop](https://github.com/openai/codex/issues/19305)** (💬 13, 👍 27)  
   Feature request: native Windows desktop Computer Use (not just Browser Use). Strong community demand.

7. **[#22802 – Mobile remote setup fails](https://github.com/openai/codex/issues/22802)** – “Secure setup failed” when pairing iOS ChatGPT with a Mac. Affects mobile‑to‑desktop remote workflow.

8. **[#23067 – `/goal` should treat repeated blockers as completion](https://github.com/openai/codex/issues/23067)** – Agent enters infinite loop re‑stating the same blocker. Request for `/goal` to detect stagnation and either pause or complete.

9. **[#22898 – Mobile shows desktop as offline; Reconnect does nothing](https://github.com/openai/codex/issues/22898)** (👍 20) – Despite desktop running, iOS app sees machine as offline. Silent reconnect failure worsens debugging.

10. **[#10233 – Non‑interactive status (JSON/headless)](https://github.com/openai/codex/issues/10233)** (👍 13) – Request for a CLI flag to get account/runtime info without entering TUI. Important for CI and scripting use.

## Key PR Progress

1. **[#23300 – feat: dedicated goal DB](https://github.com/openai/codex/pull/23300)** – Moves goal persistence into its own SQLite database, decoupling from shared state. Foundation for future per‑goal isolation and extension‑owned storage.

2. **[#23295 – chore: isolate thread goal storage behind GoalStore](https://github.com/openai/codex/pull/23295)** – Refactors goal read/write/cleanup behind a `GoalStore` trait, preparing for the dedicated DB PR above.

3. **[#23293 – feat: add extension event sink capability](https://github.com/openai/codex/pull/23293)** – Gives extensions a typed way to emit protocol events (progress, status) back to the host, reducing ad‑hoc persistence.

4. **[#23291 – Make extension lifecycle hooks async](https://github.com/openai/codex/pull/23291)** – Lifecycle callbacks are now async, enabling extensions to seed state without blocking the host.

5. **[#23288 – chore: goal ext skeleton](https://github.com/openai/codex/pull/23288)** – Skeleton of `/goal` moving into an extension, paving the way for custom goal strategies.

6. **[#23094 – goal: pause continuation loops on usage limits and blockers](https://github.com/openai/codex/pull/23094)** – Addresses #23067 and similar: `/goal` now pauses when hitting usage caps or repeated blockers instead of burning tokens.

7. **[#22870 – Add `body_after_prefix` auto‑compact token limit scope](https://github.com/openai/codex/pull/22870)** – Enables a separate token budget for “growth since compaction,” preventing preserved context from forcing immediate repeated compactions.

8. **[#22166 – Preserve MCP JSON schema structure in codex-rs](https://github.com/openai/codex/pull/22166)** – MCP tool schemas are now preserved as raw JSON Schema, while local tools continue using typed builders. Reduces schema normalization bugs.

9. **[#23299 – Add `/reload-plugins` command to TUI](https://github.com/openai/codex/pull/23299)** – Reloads plugin‑backed runtime state without a model turn. Useful during development of MCP tools and custom plugins.

10. **[#23275 – Bound state log payloads](https://github.com/openai/codex/pull/23275)** – Caps each log entry field at 16 KiB before writing to SQLite, preventing runaway memory from verbose MCP stderr or large span fields.

## Feature Request Trends

- **Windows native support** continues to dominate:  
  - Full Computer Use for Windows Desktop (#19305)  
  - Non‑Microsoft Store installer for enterprise (#21538)  
  - Side‑by‑side terminal layout in the app (#15836)  
  - CLI plugin management (list/install/upgrade) without TUI (#17431)  

- **Remote / mobile connectivity** improvements are urgently needed:  
  - Reliable mobile‑to‑desktop pairing and reconnection (#22802, #22898, #23078)  
  - Clear error messages for remote setup failures  

- **Agent / goal behavior** enhancements:  
  - Allow `/goal` to detect repeated blockers and pause (#23067, being addressed by #23094)  
  - Clear context between tasks while preserving session ID (#23218)  
  - Per‑command sandbox exclusion rules without approval (#20917)  

- **CLI ergonomics**:  
  - TUI Vim mode default to Insert mode (#21850)  
  - Non‑interactive `/status` in JSON (#10233)  
  - Interactive editing of sandbox permission prefixes (#23227)  

## Developer Pain Points

- **Rate‑limit opacity**: Users have no visible remaining usage indicator in the app (#19869). Combined with the “burning tokens” bug (#14593), many feel they can’t control costs.  

- **Windows‑specific instability**:  
  - Automations create threads but never start agents (#19011)  
  - Every new thread shows “Reconnecting…” with prewarm timeout (#21880)  
  - Infinite configure‑sandbox loop (#23137)  
  - Main‑process crash when sessions exceed V8 string length (#22004)  

- **MCP / plugin ecosystem friction**:  
  - Notion connector exposes a SQL tool that fails at runtime (#19924)  
  - Plugin marketplace layout clipped on Intel Mac (#21865)  
  - No way to reload plugins without restarting the session (addressed by #23299)  

- **Remote execution errors**:  
  - High‑error on remote compaction causes total outage (#15105)  
  - “Failed to read thread goal” in TUI (#20841)  
  - Sandbox permission approvals not surfaced through app‑server (#21982)  

- **Session / history loss**:  
  - Chat histories disappear after updates (#20741)  
  - No rollback or recovery mechanism for lost state  

These pain points highlight an urgent need for better Windows testing, rate‑limit transparency, and a more reliable remote‑connectivity stack.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-05-18

## Today's Highlights
The team published a nightly release (v0.44.0-nightly.20260517) with critical security dependency updates and a fix for web fetch aborts. Community attention is focused on persistent terminal flickering (31 👍) and a recurring subagent bug where MAX_TURNS interruptions are reported as success. Several PRs landed to address environment variable leakage into subprocesses and improve IDE integration.

## Releases
- **[v0.44.0-nightly.20260517.g77e65c0db](https://github.com/google-gemini/gemini-cli/releases/tag/v0.44.0-nightly.20260517.g77e65c0db)** – Security: updated dependencies to fix critical and high vulnerabilities. Fixes: web fetch abort on Ctrl+C; added aliases and thinking support to core.

## Hot Issues

1. **[#14708 – CLI interface flickering (P1, 11 comments, 31 👍)](https://github.com/google-gemini/gemini-cli/issues/14708)** – Terminal screen redraws every second while idle or during execution, making output unreadable. Community strongly affected; a high-priority fix is awaited.

2. **[#22323 – Subagent recovery after MAX_TURNS reported as GOAL success (P1, 6 comments, 2 👍)](https://github.com/google-gemini/gemini-cli/issues/22323)** – `codebase_investigator` subagent claims success despite hitting the turn limit without doing analysis. Misleading termination reason undermines trust in agent reporting.

3. **[#21968 – Gemini does not use skills and sub-agents enough (P2, 6 comments)](https://github.com/google-gemini/gemini-cli/issues/21968)** – Model rarely invokes custom skills or sub-agents unless explicitly instructed, even for very relevant tasks. Reduces automation potential.

4. **[#25166 – Shell command execution stuck at "Waiting input" after completion (P1, 3 comments, 3 👍)](https://github.com/google-gemini/gemini-cli/issues/25166)** – After simple CLI commands, Gemini hangs with the shell still shown as active. Blocks workflow for many users.

5. **[#22745 – Assess AST-aware file reads, search, and mapping (P2, 7 comments)](https://github.com/google-gemini/gemini-cli/issues/22745)** – Epic investigating whether AST-aware tools can reduce turns and token noise. High potential for smarter code understanding.

6. **[#24353 – Robust component-level evaluations (P1, 6 comments)](https://github.com/google-gemini/gemini-cli/issues/24353)** – Follow-up to build 76 behavioral eval tests; aims to reliably measure subagent and agent quality. Critical for quality assurance.

7. **[#22267 – Browser Agent ignores settings.json overrides (P2, 3 comments)](https://github.com/google-gemini/gemini-cli/issues/22267)** – Configuration like `maxTurns` is read correctly but not applied by the browser subagent. Causes unexpected behavior in automated browsing.

8. **[#23571 – Model frequently creates tmp scripts in random directories (P2, 3 comments)](https://github.com/google-gemini/gemini-cli/issues/23571)** – When restricted to shell execution, the model scatters temporary edit scripts, creating workspace clutter and complicating clean commits.

9. **[#21983 – Browser subagent fails in Wayland (P1, 4 comments, 1 👍)](https://github.com/google-gemini/gemini-cli/issues/21983)** – Termination reason GOAL reached prematurely on Wayland sessions. Linux users face a broken subagent experience.

10. **[#22672 – Agent should stop/discourage destructive behavior (P2, 2 comments, 1 👍)](https://github.com/google-gemini/gemini-cli/issues/22672)** – Model occasionally uses `git reset` or `--force` flags when safer alternatives exist. Community wants guardrails for dangerous operations.

## Key PR Progress

1. **[PR #27203 – Fix project .env vars leaking into subprocess environments (P1, open)](https://github.com/google-gemini/gemini-cli/pull/27203)** – Prevents `DB_DATABASE` and similar overrides from polluting spawned processes. Closes #25798.

2. **[PR #27204 – Correct Thai and Lao SARA AM display width (P2, open)](https://github.com/google-gemini/gemini-cli/pull/27204)** – Adds terminal-aware wrapper for `string-width` to keep Ink aligned on tmux and wcwidth-based terminals.

3. **[PR #27200 – Retry transient directory cleanup failures on Windows (P1/P2, open)](https://github.com/google-gemini/gemini-cli/pull/27200)** – Retries cleanup during extension updates to handle Windows file-lock timing issues.

4. **[PR #26428 – Add IDE paste bindings to terminal setup (P1/P2, open)](https://github.com/google-gemini/gemini-cli/pull/26428)** – Extends `/terminal-setup` with `ctrl+v`, `cmd+v`, `alt+v` sequences for VS Code-style terminals. Fixes #22185.

5. **[PR #27198 – Avoid blocking IDE detection in bare terminals (P1, open)](https://github.com/google-gemini/gemini-cli/pull/27198)** – Prevents "Initializing..." hang by making IDE detection fail fast and adding timeout to Unix process lookups.

6. **[PR #27186 – Add support for custom external safety checkers (open)](https://github.com/google-gemini/gemini-cli/pull/27186)** – Implements Phase 5 of the safety checker system, allowing organizations to plug in their own security/compliance binaries.

7. **[PR #27068 – Add validation tests for esbuild and eslint config (P2, open)](https://github.com/google-gemini/gemini-cli/pull/27068)** – Adds unit tests covering native-module externalization, WASM plugin resolution, and ESLint rules – addressing issue #16114.

8. **[PR #26404 – Stop buffering events when telemetry is disabled (P1, closed)](https://github.com/google-gemini/gemini-cli/pull/26404)** – Unbounded `telemetryBuffer` growth on API/MCP errors is fixed, preventing memory leaks in disabled-telemetry environments.

9. **[PR #26769 – Add system PATH fallback for ripgrep discovery (P2, open)](https://github.com/google-gemini/gemini-cli/pull/26769)** – Re-introduces fallback to system `rg` to resolve performance degradation reported in #26409 after bundling for SEA.

10. **[PR #27096 – Prevent text duplication in AfterAgent hook prompt_response (P2, open)](https://github.com/google-gemini/gemini-cli/pull/27096)** – Fixes duplicated text and extra spaces in hook payloads, ensuring extensions receive clean model output.

## Feature Request Trends
- **AST-aware tooling** – Multiple issues (#22745, #22746, #22747) push for AST-based file reads, search, and codebase mapping to reduce turns and token cost.
- **Autonomous skill and memory management** – Requests for the agent to periodically reflect on its trajectory and recommend new skills (#21421) or update memory (#26516) without manual intervention.
- **Better subagent orchestration** – Users want subagents to be backgroundable (#22741) and to be used more proactively (#21968, #22602). Also needed: reliable subagent evals (#22601).
- **Browser agent resilience** – Demands for automatic session takeover, lock recovery, and settings.json respect (#22232, #22267).
- **Safety and guardrails** – Features to prevent destructive operations (#22672), add custom safety checkers (#27186), and enforce deterministic redaction of secrets (#26525).

## Developer Pain Points
- **Terminal flickering & performance** – #14708 (flickering every second) and #21924 (flicker on resize) remain top complaints; work is ongoing to migrate to RenderStatic.
- **Subagent misbehaviour** – False success after turn limits (#22323), not using configured skills (#21968), and ignoring settings (#22267) erode developer confidence.
- **Shell execution issues** – Commands stuck after completion (#25166) and model scattering tmp scripts (#23571) disrupt workflows.
- **Environment leaks** – Project `.env` variables leaking into subprocesses (#25798, addressed by #27203) cause configuration conflicts in Laravel, Docker, etc.
- **Cross-platform consistency** – Wayland browser failure (#21983), Windows extension cleanup failures (#27200), and Thai/Lao display misalignment (#27204) reveal gaps in platform testing.
- **IDE integration fragility** – Non-blocking IDE detection hanging in bare terminals (#21477), paste binding inconsistencies (#22185), and race conditions in initialization (#26407) add friction.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-18

## Today's Highlights
No new releases were published in the last 24 hours. The community is active around regressions and platform-specific blockers: a long-standing Windows PowerShell 5.1 incompatibility (#1680) prevents the CLI from running at all on many Windows 11 machines, and Android/Termux support broke in v1.0.48 (#3333) due to a dependency on glibc. A single pull request (#3353) proposes removing the Copilot subscription requirement entirely, signalling a potential shift in licensing.

## Releases
None in the last 24 hours.

## Hot Issues

1. **[#1680 – pwsh.exe hardcoded – CLI completely unusable on Windows 11 with PowerShell 5.1](https://github.com/github/copilot-cli/issues/1680)**  
   *Labels: area:platform-windows, area:tools*  
   ⚠ **Why it matters:** This is a months-old regression (originally reported in #411) that still blocks the CLI on Windows systems that ship only with `powershell.exe`. The author shows that the exe is hardcoded in 6 places and the error now prevents **any** shell command from running.  
   **Community reaction:** 10 upvotes, multiple users confirming the bug persists after the “not_planned” closure of the original issue.

2. **[#3333 – Android/Termux support broken in v1.0.48+ (runtime.node requires glibc)](https://github.com/github/copilot-cli/issues/3333)**  
   *Labels: area:platform-linux, area:installation*  
   ⚠ **Why it matters:** v1.0.48 introduced a native Rust addon linked against glibc, which is incompatible with Android’s Bionic libc. This broke Copilot CLI for all Termux users.  
   **Community reaction:** 1 upvote, 3 comments from affected users.

3. **[#3364 – Feature: long-running goals via .copilot/goals.md](https://github.com/github/copilot-cli/issues/3364)**  
   *Labels: triage*  
   **Why it matters:** Proposes declarative cross-session goal tracking (per-repo and global), complementing existing session persistence features. Could fundamentally improve how developers manage multi-step workflows.  
   **Community reaction:** New issue, 1 comment (likely author clarifying scope).

4. **[#3359 – Qwen3.6-plus consumes 40% of tokens vs 3% in Claude Code](https://github.com/github/copilot-cli/issues/3359)**  
   *Labels: area:models*  
   **Why it matters:** Token efficiency is critical for cost-conscious users. The discrepancy suggests Copilot CLI may have a suboptimal token budget or prompt structure for certain models.  
   **Community reaction:** 1 comment, likely from author.

5. **[#3365 – Session Auto-Rename does not work anymore](https://github.com/github/copilot-cli/issues/3365)**  
   *Labels: triage*  
   **Why it matters:** A regression that breaks the AI-generated session title feature, now showing the last prompt instead.  
   **Community reaction:** New issue, 0 comments.

6. **[#3363 – Response interrupted due to server error – cannot work](https://github.com/github/copilot-cli/issues/3363)**  
   *Labels: area:models*  
   **Why it matters:** Repeated server errors lock users out of the session entirely, making the tool unusable.  
   **Community reaction:** New issue, 0 comments.

7. **[#3362 – Changing workdir doesn’t emit event anymore](https://github.com/github/copilot-cli/issues/3362)**  
   *Labels: area:sessions*  
   **Why it matters:** Workdir changes are no longer recorded in events.jsonl or workspace.yaml, breaking logging and potentially session replay.  
   **Community reaction:** New issue, 0 comments.

8. **[#3361 – Extension onPostToolUse modifiedResult not applied to model context](https://github.com/github/copilot-cli/issues/3361)**  
   *Labels: area:plugins*  
   **Why it matters:** Plugin developers rely on this hook to modify tool results; the bug means the model sees unmodified output, defeating the purpose of the extension.  
   **Community reaction:** 1 upvote, 0 comments.

9. **[#3358 – /remote toggle stops working in long-running sessions](https://github.com/github/copilot-cli/issues/3358)**  
   *Labels: area:sessions, area:networking*  
   **Why it matters:** Remote mode (for GitHub mobile integration) becomes irrecoverably stuck after prolonged use. Users must restart the session.  
   **Community reaction:** New issue, 0 comments.

10. **[#3357 – Feature request: Gemma4-like token reduction](https://github.com/github/copilot-cli/issues/3357)**  
    *Labels: area:models*  
    **Why it matters:** User requests 0-token intent classification to avoid wasting tokens on trivial prompts – a pattern seen in Gemini/Claude. Could reduce cost significantly.  
    **Community reaction:** New issue, 0 comments.

## Key PR Progress
Only one pull request was updated in the last 24 hours:

- **[#3353 – Copilot subscription no longer required](https://github.com/github/copilot-cli/pull/3353)**  
  **Author:** andresdelfino | Created: 2026-05-16 | Updated: 2026-05-18  
  **Summary:** (No description provided beyond title.)  
  **Significance:** If merged, this would be a major shift – making Copilot CLI available without a Copilot subscription. The community is watching closely, but no comments or reviews are visible yet.

## Feature Request Trends
From the issues filed in the last 24h, the following feature directions stand out:

- **Persistent, cross-session goals** – A declarative `.copilot/goals.md` file (per-repo and global) to maintain long-running objectives (#3364).
- **Token efficiency improvements** – Inspired by Google’s Gemma 4, users want 0-token intent classification to avoid wasting tokens on simple prompts (#3357).
- **Model-specific optimizations** – Users are directly comparing token consumption across models (e.g., Qwen vs Claude vs DeepSeek) and asking for per-model budgets (#3359, #3357).
- **Plugin ecosystem maturity** – Demand for robust hook execution (e.g., `onPostToolUse` context propagation) is a sign that developers want to build complex extensions (#3361).

## Developer Pain Points
Recurring frustrations from the last 24h:

- **Windows PowerShell 5.1 is a first-class blocker** – Hardcoded `pwsh.exe` path prevents the CLI from working on the default Windows 11 setup for many enterprise users (#1680).
- **Native addon breakage** – The Rust addon in v1.0.48 broke both Android/Termux (#3333) and may affect other non-glibc platforms.
- **Session reliability degrades over time** – Remote toggle (#3358) and server error loops (#3363) force session restarts, hurting long-running workflows.
- **Regressions in user-facing UX** – Session auto-rename (#3365) and workdir event logging (#3362) broke silently.
- **Plugin development friction** – Extension hooks not applying modifications to model context (#3361) undermines the plugin system value.
- **Plugin marketplace discovery issues** – Browsing the `awesome-copilot` marketplace fails with “templates not found” (#3360).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Okay, here is the Kimi Code CLI community digest for 2026-05-18, based on the provided GitHub data.

---

## Kimi Code CLI Community Digest – 2026-05-18

### Today's Highlights
Today's activity is dominated by performance and reliability concerns. The critical `K2.6 model overloaded` bug (Issue #2077) continues to receive significant community attention, signaling a major service stability problem. On a positive note, two important pull requests from contributor `ekhodzitsky` aim to fix long-standing memory and connection leak issues. A new feature request to whitelist the **Cline** VS Code extension (Issue #2322) highlights a growing desire for third-party tool integration.

### Releases
**No new releases in the last 24 hours.** The latest release remains stable.

### Hot Issues
*   **#2077**: **[bug] [Critical] K2.6 model overloaded – unusable under normal load** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2077)]: This critical issue, with 15 comments and persisted since April 26, describes the flagship K2.6 model as constantly retrying and unusable under normal load. The prolonged discussion indicates a deeply rooted infrastructure or model-serving problem that remains unresolved. This is the community's top concern.
*   **#2314**: **Prompts take way too long to complete in general** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2314)]: User reports extreme latency (up to 5 minutes) for simple database operations, citing the model "overthinking everything." This points to a potential regression in model efficiency or prompt processing, possibly related to the issues in #2077.
*   **#1458**: **[bug] VS Code report "error":{"code":-32003,"message":"Connection error."...** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/1458)]: A persistent, older bug causing connection errors specifically within VS Code. Its continued lifespan suggests a tricky integration issue between the CLI and the VS Code extension.
*   **#2322**: **[enhancement] [Feature Request] Add Cline to the Kimi Code whitelist** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2322)]: Users want to use Kimi Code's model with the popular Cline VS Code extension but receive a `403 access_terminated_error`. This request signals demand for broader ecosystem compatibility and API accessibility.
*   **#2321**: **Feature Request: Configurable git status/branch polling intervals for monorepo users** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2321)]: A common pain point for developers in large monorepos where frequent git status polling can introduce latency. Requesting configuration via env vars or `config.toml`.
*   **#2320**: **[bug] An error seems caused by the ✨ emoji.** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2320)]: A peculiar bug report where a sparkle emoji can cause a crash. While seemingly minor, it highlights a potential unicode parsing or rendering edge case in the terminal UI.
*   **#2319**: **[enhancement] macos zsh request to discard cyan highlighting** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2319)]: A request for more customizable syntax highlighting schemes. The user found the default cyan highlights on dark themes unreadable and had to modify source code to change them.
*   **#2318**: **[bug] request reached organization TPD rate limit, current: 1505241** [[Link](https://github.com/MoonshotAI/kimi-cli/issues/2318)]: A user reports a TPD (Tasks Per Day) rate limit error with an extremely high number (1.5 million), claiming it is an incorrect calculation. This raises questions about rate limiting logic and user communication.

### Key PR Progress
*   **#2231**: **[fix(aiohttp): reuse TCPConnector to prevent connection leaks]** [[Link](https://github.com/MoonshotAI/kimi-cli/pull/2231)]: A critical fix by `ekhodzitsky` to reuse `TCPConnector` objects. This prevents file-descriptor pressure and reduces HTTP handshake overhead, directly addressing performance degradation under heavy load.
*   **#2236**: **[fix(utils): bound broadcast queues and cap web store cache to prevent memory leaks]** [[Link](https://github.com/MoonshotAI/kimi-cli/pull/2236)]: Another essential fix from `ekhodzitsky` tackling two potential OOM (Out of Memory) causes: unbounded `asyncio.Queue` for broadcast subscribers and an ever-growing in-memory session cache.
*   **#1127**: **[style(web): tweak some web ui details]** [[Link](https://github.com/MoonshotAI/kimi-cli/pull/1127)]: An older, closed PR that made minor visual adjustments to the web UI. Its recent update activity suggests it may be considered for merging or its changes being revisited.

### Feature Request Trends
*   **Third-Party IDE/Tool Integration**: There is a strong desire to use Kimi Code's backend models (specifically `kimi-for-coding`) within other popular development tools like the **Cline** VS Code extension (Issue #2322).
*   **Deep Configuration & Customization**: Users are requesting more granular control over the CLI's behavior, such as configurable Git polling intervals for monorepos (Issue #2321) and customizable terminal UI themes/syntax highlighting (Issue #2319).

### Developer Pain Points
*   **Model Performance & Stability**: The dominant frustration is the unreliability and slowness of the K2.6 model under normal conditions (Issue #2077, #2314). This is the single biggest blocker for user productivity and trust.
*   **Connectivity & Integration Errors**: Recurring issues with VS Code integration (Issue #1458), API rate limits (Issue #2318), and access errors with third-party tools (Issue #2322) create a fragmented and frustrating developer experience.
*   **Lack of Usability Polish**: Minor but frequent complaints, such as unchangeable, hard-to-read syntax highlighting (Issue #2319) and unexpected crashes from emoji characters (Issue #2320), degrade the overall polish and feel of the tool.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-18

## Today's Highlights
A patch release v1.15.4 landed today fixing scoped bus events and LSP refresh issues. The community is seeing a surge in reports around the “Big Pickle” model regression introduced in the upgrade, with at least three new issues filed today alone. Meanwhile, a critical bug in plugin tool validation is now being addressed via a PR after multiple silent session failures.

## Releases
**v1.15.4** – [Release notes](https://github.com/anomalyco/opencode/releases/tag/v1.15.4)  
Core bugfixes: fixed project-scoped bus events so file watcher and update notifications reach the correct instance; fixed custom LSP servers not sending refresh events after initialization; background subagent task instructions are now hidden unless experimental mode is enabled.

## Hot Issues
1. **[#13768](https://github.com/anomalyco/opencode/issues/13768) – Opus 4.6 assistant message prefill error** (67 comments, 28👍)  
   Frequent `"This model does not support assistant message prefill"` errors when using Opus 4.6. High community impact; still open.

2. **[#28138](https://github.com/anomalyco/opencode/issues/28138) – Big Pickle model broken after upgrade** (14 comments, 1👍)  
   `Model big-pickle not supported for format anthropic` error on v1.15.4. Duplicate reports in #28133 and #28146 suggest a widespread regression.

3. **[#27602](https://github.com/anomalyco/opencode/issues/27602) – Kimi for Coding HTTP 429 errors** (11 comments, 4👍)  
   Built-in provider returns `engine overloaded` due to non-whitelisted User-Agent header. Closed but awaiting fix merge.

4. **[#26667](https://github.com/anomalyco/opencode/issues/26667) – AbortError crashes sidecar** (8 comments)  
   Unhandled `AbortError` from LLM streaming causes the entire sidecar process to crash. Needs graceful error handling.

5. **[#24771](https://github.com/anomalyco/opencode/issues/24771) – Severe performance issues** (5 comments)  
   Sporadic slowdowns in v1.14.20; response times vary wildly. Team reports similar experiences.

6. **[#27902](https://github.com/anomalyco/opencode/issues/27902) – Kimi User-Agent header fix (PR attached)** (5 comments, 9👍)  
   Community proposed fix to add a proper User-Agent to avoid 429s. Active discussion.

7. **[#17557](https://github.com/anomalyco/opencode/issues/17557) – `/compact` command increases context instead of compressing** (4 comments)  
   Users report token count grows after running `/compact`, indicating the command does nothing or fails silently.

8. **[#7624](https://github.com/anomalyco/opencode/issues/7624) – Base path / prefix routing support** (7 comments, 29👍)  
   Feature request to run OpenCode under a URL prefix for platform integration. Highest 👍 count in the top 30.

9. **[#7226](https://github.com/anomalyco/opencode/issues/7226) – `/resume` and `/pause` commands** (4 comments, 18👍)  
   Users want explicit session control to easily reattach context without retyping.

10. **[#28163](https://github.com/anomalyco/opencode/issues/28163) – Plugin with invalid tool definition silently breaks all sessions** (2 comments)  
    Plugin registering tools with raw `parameters` instead of the SDK helper causes silent failures. PR #28161 now addresses this.

## Key PR Progress
1. **[#27961](https://github.com/anomalyco/opencode/pull/27961) – Reduce TUI fenced code streaming flicker**  
   Stops re-rendering the fenced block on every chunk, improving visual stability.

2. **[#27940](https://github.com/anomalyco/opencode/pull/27940) – Refresh mutable plugin specs during install**  
   Prevents stale package cache from blocking plugin updates.

3. **[#27694](https://github.com/anomalyco/opencode/pull/27694) – Resolve LSP dependencies from workspace root**  
   Allows OpenCode to correctly find language tools when launched from a monorepo root.

4. **[#28161](https://github.com/anomalyco/opencode/pull/28161) – Prevent crash when plugin tool has invalid/missing args**  
   Direct fix for #27630 and #28163 – adds guard against undefined `tool.args`.

5. **[#28067](https://github.com/anomalyco/opencode/pull/28067) – Reconcile compaction summary with preserved tail**  
   Fixes stale next-steps summaries after session compaction.

6. **[#23356](https://github.com/anomalyco/opencode/pull/23356) – Prevent auto-updating session timestamps on metadata changes**  
   Stops unwanted timestamp bumps when only metadata (e.g., title) is changed.

7. **[#28165](https://github.com/anomalyco/opencode/pull/28165) – Fix Windows path separator for session list**  
   Solves session loss when opening projects via CLI on Windows.

8. **[#28147](https://github.com/anomalyco/opencode/pull/28147) – Wrap MCP commands with wsl.exe in WSL mode**  
   Enables MCP local commands to work when the desktop app runs in WSL.

9. **[#28143](https://github.com/anomalyco/opencode/pull/28143) – Add GLM-5 reasoning support on AWS Bedrock**  
   Adds `reasoning_config` variants for GLM models via `additionalModelRequestFields`.

10. **[#27981](https://github.com/anomalyco/opencode/pull/27981) – Directory-based skill name prefixing**  
    Opens namespace support for skills using `:`-separated prefixes derived from directory structure.

## Feature Request Trends
- **URL routing & platform embedding** – Issue #7624 (29👍) highlights demand for deploying OpenCode behind a base path for platform integration.
- **Session control commands** – Issues #7226 (18👍) for `/resume`/`/pause` and #17557 for `/compact` fixes show users want finer-grained context management.
- **Background subagent streaming** – Issue #27898 asks for real-time output from background subagents, indicating a need for better multi-agent observability.
- **Plugin tool validation** – The #28163 bug and its PR #28161 signal a community push for stricter plugin API enforcement.
- **i18n expansion** – PR #28061 adds Ukrainian locale, joining ongoing localization efforts.

## Developer Pain Points
- **Big Pickle model regression** – Multiple issues (#28138, #28133, #28146) report the same `not supported for format anthropic` error after upgrading to v1.15.4.
- **Kimi provider reliability** – Persistent 429 throttling (Issue #27602) due to missing User-Agent header frustrates users; a fix is in review.
- **Silent plugin failures** – Invalid tool definitions (Issue #28163) break all sessions without UI feedback, wasting developer time on debugging.
- **Session switching lag** – Issue #27910 documents a ~170ms blank flash and Suspense splash screen when switching sessions, harming UX.
- **Model reasoning effort not prompted** – Issue #27893 reports that after switching models via `/models`, the reasoning effort selection no longer appears.
- **Account deletion dead end** – Issue #18016 (2👍) points to an inability to delete Zen accounts, with billing concerns unaddressed.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-05-18

## Today’s Highlights
The project shipped three patch releases within 24 hours (v0.75.1 → v0.75.3), primarily fixing critical HTTP/2 transport crashes and Bun-compiled binary startup failures. Community attention remains focused on Windows compatibility, provider authentication regressions under Node 26, and the ongoing debate around a Rust rewrite of Pi.

## Releases

- **v0.75.3** – Hot-fix for undici HTTP/2 destroyed-session races that crashed the Node CLI; preserves the previous HTTP/1.1-only fetch dispatcher behavior.  
  [Release notes](https://github.com/earendil-works/pi/issues/4681)

- **v0.75.2** – Fixed Bun-compiled release binaries failing to start when Bun’s built-in undici shim lacks the `install` export.  
  [PR #4661](https://github.com/earendil-works/pi-mono/pull/4661)

- **v0.75.1** – Config selectors now scale visible row count to terminal height; fixed Anthropic-compatible API‑key requests ignoring unrelated `ANTHROPIC_AUTH_TOKEN` environment.  
  [PR #4243](https://github.com/earendil-works/pi-mono/pull/4243)

- **v0.75.0** – **Breaking:** minimum Node.js version raised to 22.19.0. Fixed compaction summary calls to use custom agent stream functions, preserving proxy-backed LLM routing.  
  [Issue #4484](https://github.com/earendil-works/pi/issues/4484)

## Hot Issues (10 of 30)

1. **#3357 – Official local LLM provider extension** (OPEN, 18 comments)  
   Request to fetch model list dynamically from `{baseUrl}/models`, making it trivial to hook Pi into llama.cpp, Ollama, LM Studio, etc. Highly upvoted (👍24).  
   [Link](https://github.com/earendil-works/pi/issues/3357)

2. **#4647 – `pi update` fails for valid global pnpm install** (CLOSED, 11 comments)  
   Package manager ownership check compares incorrect resolved paths after symlink expansion.  
   [Link](https://github.com/earendil-works/pi/issues/4647)

3. **#4505 – 400 error with MiMo models: reasoning_content not preserved in multi-turn tool use** (CLOSED, 11 comments)  
   Cold-start tool calls fail on second turn because the provider does not send required `reasoning_content`.  
   [Link](https://github.com/earendil-works/pi/issues/4505)

4. **#4609 – Rewrite pi in Rust** (CLOSED, 10 comments)  
   Polarising meta-discussion by @badlogic. Closed quickly but many devs chimed in.  
   [Link](https://github.com/earendil-works/pi/issues/4609)

5. **#4659 – Pi freezes using Zen opencode models, shows no error** (CLOSED, 8 comments)  
   Complete unresponsiveness with OpenCode Zen free models; only Ctrl+C works.  
   [Link](https://github.com/earendil-works/pi/issues/4659)

6. **#4157 – Error/warning running `pi update` on Windows** (CLOSED, 8 comments)  
   `NODE_TLS_REJECT_UNAUTHORIZED` warning and path issues on Windows.  
   [Link](https://github.com/earendil-works/pi/issues/4157)

7. **#4680 – Add static headers to opencode/opencode-go model metadata** (CLOSED, 7 comments)  
   Missing `OPENCODE_STATIC_HEADERS` constant – without it, model definitions lack required HTTP headers.  
   [Link](https://github.com/earendil-works/pi/issues/4680)

8. **#4653 – Copilot subscription fails with JSON parse error** (CLOSED, 6 comments)  
   `Unexpected token '…' is not valid JSON` after upgrading to 0.75.0 – affects both login and token refresh.  
   [Link](https://github.com/earendil-works/pi/issues/4653)

9. **#4682 – Pi crashes on uncaught ERR_HTTP2_INVALID_SESSION from undici** (CLOSED, 5 comments)  
   Long-running Objective Loop sessions trigger uncaught HTTP/2 transport crash. Fixed in v0.75.3.  
   [Link](https://github.com/earendil-works/pi/issues/4682)

10. **#4650 – gptpro sub OAuth receives invalid JSON error** (CLOSED, 5 comments)  
    `/login` with OpenAI provider returns `Unexpected token` on macOS.  
    [Link](https://github.com/earendil-works/pi/issues/4650)

## Key PR Progress (10 of 20)

1. **#4651 – Fetch portable git bash on Windows** (OPEN, draft)  
   Experiment to auto-download git bash (~350 MB) into `~/.pi` – a potential solution for Windows spawn issues, but still under evaluation.  
   [Link](https://github.com/earendil-works/pi/pull/4651)

2. **#4684 – Refresh agent interface after run settles** (CLOSED)  
   Fixes a stale streaming state in the web UI when `Agent.finishRun()` completes.  
   [Link](https://github.com/earendil-works/pi/pull/4684)

3. **#4603 – Update OpenAI Codex model list** (CLOSED)  
   Removes deprecated models and adds new ones with correct pricing data from models.dev. Resolves #4601.  
   [Link](https://github.com/earendil-works/pi/pull/4603)

4. **#4661 – Guard undici install under Bun** (CLOSED)  
   Prevents the v0.75.1 startup crash on Bun by conditionally importing `install` from undici.  
   [Link](https://github.com/earendil-works/pi/pull/4661)

5. **#4664 – Scroll shared tool entries to rendered tool calls** (OPEN)  
   Improves `/share` HTML sidebar navigation for tool result entries.  
   [Link](https://github.com/earendil-works/pi/pull/4664)

6. **#4606 – Null check before `.startsWith()` on result.error** (CLOSED)  
   Defensive fix preventing `Cannot read properties of undefined` when API providers return malformed errors.  
   [Link](https://github.com/earendil-works/pi/pull/4606)

7. **#4672 – Claude-hooks-compat exit code 3 + comprehensive guard E2E tests** (CLOSED)  
   Correctly handles exit code 3 (ask confirmation) and adds 17 E2E tests for security guards.  
   [Link](https://github.com/earendil-works/pi/pull/4672)

8. **#4668 – Feature/simple parallel package loading** (CLOSED)  
   Reduces startup time by loading Pi extensions in parallel – a noticeable improvement for heavy extension users.  
   [Link](https://github.com/earendil-works/pi/pull/4668)

9. **#4600 – Route compaction through streamFn** (CLOSED)  
   Fixes compaction summary calls bypassing custom agent streams, which broke proxy‑backed LLM routing. Closes #4484.  
   [Link](https://github.com/earendil-works/pi/pull/4600)

10. **#4112 – Switch Xiaomi default to API billing, add per-region token plan providers** (CLOSED)  
    Splits Xiaomi MiMo provider so the default targets the API billing endpoint; token plan users pick a regional endpoint explicitly.  
    [Link](https://github.com/earendil-works/pi/pull/4112)

## Feature Request Trends

- **Local LLM integration** (#3357) remains the most‑requested feature: fetching model lists dynamically from `{baseUrl}/models` would allow seamless hooking into llama.cpp, Ollama, and LM Studio.
- **Provider extensibility** – Multiple PRs add new providers (e.g., routing.run #4636) or split existing ones (Xiaomi #4112). The community wants a streamlined way to add custom OpenAI‑compatible providers.
- **Better Windows support** – While often expressed as bug reports, the underlying demand is for first‑class Windows handling: Git Bash bundling (#4651), fixed npm spawning, and proper shell quoting.
- **Parallel operations** – Slower startup due to extension loading (#4668) has prompted work on concurrent package loading; expect more optimisation PRs.

## Developer Pain Points

- **Windows spawn ENOENT errors** dominated the issue tracker: npm commands fail because the resolved path doesn’t match the expected location (issues #4677, #4665, #4670, #4623). The root cause is a recent commit (`6b872be2`) that changed npm detection.
- **Bun vs. undici compatibility** – v0.75.1 broke Bun‑compiled releases because `undici.install` is missing from Bun’s built‑in shim. Multiple users reported startup failures and workarounds.
- **HTTP/2 session crashes** – Long‑running Objective Loop sessions with undici’s H2 client caused uncaught `ERR_HTTP2_INVALID_SESSION`, crashing the whole Pi session. v0.75.3 rolled back to HTTP/1.1 as a mitigation.
- **Auth regressions on Node 26** – Several providers (Copilot, OpenAI, Codex) failed with “Unexpected token … is not valid JSON”, often caused by gzip decompression issues or missing interceptors (#4653, #4650, #4654, #4652).
- **MiMo / DeepSeek protocol quirks** – Missing `reasoning_content` on assistant messages in multi‑turn tool calls leads to 400 errors that are non‑obvious and provider‑specific (#4505).
- **External editor stdin leakage** – Opening an editor (e.g., nvim) via Ctrl+G randomly sends keys to Pi instead of the editor, particularly in pre‑compiled releases (#4365, #4612).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Based on the GitHub data for QwenLM/qwen-code, here is the community digest for 2026-05-18.

---

### Qwen Code Community Digest - 2026-05-18

#### 1. Today's Highlights

The Qwen Code ecosystem is rapidly maturing its **daemon mode (`qwen serve`)** with a flurry of PRs adding workspace file editing, MCP guardrails, and device-flow authentication, signaling a strong push toward the v0.16 production-ready milestone. However, the project is simultaneously facing a significant **stability crisis**, with a high volume of user-reported "heap out of memory" (OOM) crashes dominating recent discussions. A particularly hot topic is a controversial proposal to drastically reduce the free tier for the Qwen OAuth service, which has sparked a record 126 comments from the community.

#### 2. Releases

Two new releases were published in the last 24 hours, both containing the same set of key fixes and a new feature:
- **v0.15.11-nightly.20260518** and **v0.16.0-preview.0**
  - **feat(cli):** Markdown links in the terminal now wrap in OSC 8 escape sequences, ensuring URLs remain clickable after output.
  - **fix(core):** Normalized cumulative OpenAI stream deltas to suffixes, fixing a potential issue with streamed responses.
  - **fix(cli):** Implemented auto-restore functionality for the CLI session.

#### 3. Hot Issues

1.  **[#3203] Qwen OAuth Free Tier Policy Adjustment**
    *Comment count: 126* | **Status: OPEN**
    A high-impact proposal to reduce the free daily quota from 1,000 to 100 requests and eventually phase out the free tier entirely. The extreme level of engagement (126 comments) indicates this is a highly sensitive topic that is driving significant community debate.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/3203)

2.  **[#3803] Daemon mode (qwen serve): proposal & open decisions ([wenshao])**
    *Comment count: 15* | **Status: OPEN**
    A foundational design proposal for the daemon mode, organized as a multi-chapter design series. This is the central reference for the current wave of `qwen serve` development.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/3803)

3.  **[#4175] proposal(serve): Mode B feature-priority roadmap toward v0.16 production-ready ([doudouOUC])**
    *Comment count: 13* | **Status: OPEN**
    Lays out the remaining work (Wave 4 features) required to make `qwen serve` production-ready, including HTTP/SSE routes, auth, and session multiplexing. This is the tactical roadmap driving today's PRs.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4175)

4.  **[#4149] FATAL ERROR: Ineffective mark-compacts near heap limit... JavaScript heap out of memory ([Aleks-0])**
    *Comment count: 10* | **Status: OPEN**
    A critical bug report showing the Node.js process crashing with an OOM error during mark-compact GC. This is representative of a major, recurring pain point for the user base.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4149)

5.  **[#4167] cli crashed ([ProphetOB])**
    *Comment count: 6* | **Status: OPEN**
    Another report of a CLI crash, with the log showing a similar OOM-related GC failure. This reinforces the urgency of the memory leak/management problem.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4167)

6.  **[#4275] Problem with gpt-oss-120b model, that qwen can handle ([v0ff4k])**
    *Comment count: 5* | **Status: CLOSED**
    Reports an endless loop with a specific model (`gpt-oss-120b`). While closed, it highlights ongoing compatibility challenges with non-Qwen models.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4275)

7.  **[#4223] mimo-v2.5-pro API Error: 400 Param Incorrect ([Gove2004])**
    *Comment count: 4* | **Status: OPEN**
    A model-specific integration issue where tool calls fail after the first successful use. The user suspects a `reasoning_content` field problem, similar to issues with other models like DeepseekV4Pro.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4223)

8.  **[#4278] 任务中断了，自己不继续执行** (Task interrupted, not continuing automatically) ([htstcsn])
    *Comment count: 3* | **Status: OPEN**
    A critical user experience issue where a long-running task stops without completing. This is likely related to the OOM and context management problems reported elsewhere.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4278)

9.  **[#4094] Trim outdated background task results and improve new-task discoverability... ([huww98])**
    *Comment count: 3* | **Status: CLOSED**
    A welcomed proposal to improve the task management UI by cleaning up stale results and making new tasks more visible. Its closure suggests the requested enhancement was implemented or declined.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4094)

10. **[#4098] "Long conversation? /compress summarizes history to free context" is not working ([undici77])**
    *Comment count: 3* | **Status: OPEN**
    A feature-critical bug report indicating that the `/compress` command, which is meant to manage long conversation context, is non-functional. This directly impacts users with lengthy workflows.
    [Link to Issue](https://github.com/QwenLM/qwen-code/issues/4098)

#### 4. Key PR Progress

1.  **[#4282] feat(serve): approval / tools / init / MCP-restart mutation routes ([doudouOUC])**
    **Status: OPEN**
    Part of the v0.16 roadmap, this PR adds critical mutation control routes (approval mode, tools, init, MCP restart) to the daemon, enabling remote control of a session's runtime behavior.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4282)

2.  **[#4280] feat(serve): add workspace file write/edit routes ([doudouOUC])**
    **Status: OPEN**
    Another Wave 4 PR that allows remote clients to safely mutate files in the daemon's workspace, including bounded reads, hash-bearing writes, and content-concurrency checks.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4280)

3.  **[#4255] feat(serve): auth device-flow route ([doudouOUC])**
    **Status: OPEN**
    Implements OAuth 2.0 Device Authorization Grant for the daemon, allowing remote SDK clients to trigger a web-based login without exposing API keys to the client machine.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4255)

4.  **[#4286] docs: add runtime memory benchmark report and investigation plan ([yiliang114])**
    **Status: OPEN**
    A direct response to the OOM crisis. This PR provides a formal benchmark report and a plan for investigating runtime memory usage in headless tasks, a clear sign the team is prioritizing this issue.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4286)

5.  **[#4277] feat(cli): per-turn /diff with interactive dialog ([BZ-D])**
    **Status: OPEN**
    A powerful UX improvement that overhauls the `/diff` command, allowing users to view changes from each individual conversation turn instead of just the aggregate working tree diff.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4277)

6.  **[#4266] feat(tui): add experimental daemon stream path ([chiga0])**
    **Status: OPEN**
    An experimental feature to connect the standard TUI to a `qwen serve` daemon session, showing the long-term convergence of the CLI and daemon architectures.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4266)

7.  **[#4267] feat(ide): add experimental daemon webview path ([chiga0])**
    **Status: OPEN**
    The companion PR to #4266 for the VS Code extension, adding an experimental daemon-backed connection for the IDE.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4267)

8.  **[#4238] Pin fetch to bundled undici for undici higher versions compatibility ([ideal])**
    **Status: OPEN**
    A compatibility fix addressing a `Connection error` on Node.js 26 (which bundles undici v8). It pins the fetch implementation to the project's bundled undici v6 to prevent handler mismatches.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4238)

9.  **[#4146] feat(cli): virtual viewport for long conversations on ink 7 ([chiga0])**
    **Status: OPEN**
    An architectural improvement to handle very long conversations in the TUI without performance degradation, essential for users who run extensive agentic sessions.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4146)

10. **[#4242] fix(cli): map rewind turns after compression ([Jerry2003826])**
    **Status: OPEN**
    Fixes a bug where the `rewind` feature didn't work correctly after the `/compress` command was used, ensuring users can reliably navigate their conversation history.
    [Link to PR](https://github.com/QwenLM/qwen-code/pull/4242)

#### 5. Feature Request Trends

- **Daemon Mode Maturation (`qwen serve`):** The strongest trend is the push to make `qwen serve` a production-grade service. Feature requests and PRs are filling in missing pieces like authentication flows (device-auth), file I/O routes, and runtime mutation controls.
- **Context & Session Management:** Users are consistently requesting better tools for managing long-running sessions. This includes requests for non-AI compression (`/compress-fast`), fixes for the existing `/compress` command, and improvements to session persistence and rewind capabilities.
- **Performance Metrics & Transparency:** There is a growing demand for exposing runtime performance metrics, specifically tokens per second (TPS) and time to first token (TTFT). This indicates a developer base that wants to diagnose and optimize model response times.

#### 6. Developer Pain Points

- **Memory Leaks & Crashes (OOM):** This is the single biggest pain point. Multiple reports (Issues #4149, #4167, #4276, #2868, #4254) describe a process that consumes ever-increasing memory until it crashes with a "heap out of memory" error. This is a critical stability issue that undermines trust for long-running tasks.
- **Model Switching & API Incompatibility:** Users integrating with a wide variety of third-party models (e.g., `gpt-oss-120b`, `mimo-v2.5-pro`, `deepseek-v4-pro`) are encountering frequent API errors and compatibility issues, often related to how the tool handles specific response fields like `reasoning_content`.
- **Node.js Version Compatibility:** A specific, critical bug (Issue #4274) has emerged where the tool fails entirely on Node.js 26 with a connection error. This highlights the fragility of relying on specific internal APIs that change with new Node.js versions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*