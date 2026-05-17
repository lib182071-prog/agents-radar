# AI CLI Tools Community Digest 2026-05-17

> Generated: 2026-05-17 08:34 UTC | Tools covered: 8

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
**Date**: 2026-05-17  
**Scope**: Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with all eight tools actively addressing platform stability, model compatibility, and developer workflow integration. Today’s digest reveals a shared focus on session reliability, memory management, and extensibility (skills/hooks/MCP), while differentiation emerges in target use cases—from code-centric agents (Claude Code, Codex) to universal assistants (Gemini, Pi). OpenCode and Pi shipped new releases today, signaling sustained iteration cycles. Communities remain vocal about persistent pain points (copy/paste corruption, OOM crashes, reasoning content fragmentation), indicating that polish—not just features—is a decisive factor for user adoption.

---

## 2. Activity Comparison

| Tool                   | Hot Issues Listed | Key PRs Tracked | Release Published |
|------------------------|-------------------|-----------------|-------------------|
| Claude Code            | 10                | 1               | No                |
| OpenAI Codex           | 10                | 10              | No                |
| Gemini CLI             | 10                | 10              | No                |
| GitHub Copilot CLI     | 10                | 2               | No                |
| Kimi Code CLI          | 9                 | 3               | No                |
| **OpenCode**           | 10                | 10              | **Yes (v1.15.3, v1.15.2)** |
| **Pi**                 | 10                | 10              | **Yes (v0.74.1)** |
| Qwen Code              | 10                | 10              | No                |

*Note: Counts represent items featured in today’s community digest, not total project activity; OpenCode and Pi show highest release velocity.*

---

## 3. Shared Feature Directions

Several requirements appear across multiple tool communities, revealing cross-cutting developer needs:

| Requirement | Affected Tools | Specific Need |
|-------------|----------------|---------------|
| **Shareable agent instructions** | Claude Code, Kimi Code, OpenCode | Global fallback `AGENTS.md` or `.agents/` directory for reusable configurations |
| **Session continuity across devices** | Claude Code, Kimi Code, OpenCode | Import/export context, resume sessions on different machines |
| **Deterministic billing/rate‑limit transparency** | Claude Code, OpenAI Codex, Kimi Code | Clear cache token accounting, weekly quota reset visibility |
| **Reasoning/thinking block handling** | Gemini CLI, Pi, Qwen Code | Robust treatment of `reasoning_content` in tool-call chains across providers |
| **MCP/hook reliability** | Claude Code, Gemini CLI, GitHub Copilot CLI | Non‑bypassed permissions, read-only trust in Plan Mode, external hook loading |
| **Memory management for long sessions** | Qwen Code, Pi, OpenCode | Heap-pressure compaction, OOM prevention, memory diagnostics |
| **Enhanced TUI & accessibility** | Claude Code, OpenCode, Pi, Gemini CLI | RTL text support, screen reader mode, streaming scroll lock |
| **Skill/agent self‑improvement** | Gemini CLI, OpenAI Codex, OpenCode | Periodic reflection, skill recommendation, skill_search tools |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach |
|------|---------------|-------------|-------------------|
| **Claude Code** | Agent instructions, plugin hooks, conversation sharing | Power developers working in large codebases | Heavily community‑driven feature requests; slow PR velocity but high-quality governance |
| **OpenAI Codex** | Multi‑agent workflows, PDF/document ingest, rate‑limit control | Enterprise teams needing structured output and extensibility | Fast PR pipeline (10 tracked today); skill_search tool merged; next‑turn state API stack in progress |
| **Gemini CLI** | Subagent reliability, AST‑aware tooling, memory system | Developers wanting agent self‑awareness and safe autonomy | P1‑focused bug fixes with PR merging; Windows shell fallback and exponential token leak fix |
| **GitHub Copilot CLI** | Scheduling commands, unified config, BYOK support | Copilot subscribers needing workflow automation | Slower PR activity (2 tracked); emphasis on parity with Claude Code (`/every`, `/config`) |
| **Kimi Code CLI** | Cross‑platform compatibility, session handoff | Multi‑device developers, Windows/PowerShell users | Small community but rapid bug closure (2 Windows issues closed today); global AGENTS.md request |
| **OpenCode** | Skill system, TUI customization, LLM provider flexibility | Developers who want deep Vim‑like control and skill scripting | Most active release cycle (2 releases today); strong community feature voting; decoupled architecture |
| **Pi** | Provider-agnostic reasoning, dynamic model discovery | Power users mixing proprietary & open models | v0.74.1 adds image generation; many closed issues hint at internal rewrite; heavy focus on `reasoning_content` |
| **Qwen Code** | Memory/performance at scale, daemon mode (Mode B) | Users running long‑sessions, headless/CI automation | Heap‑pressure compaction merged; 7 PRs target v0.16 daemon production readiness; roadmap /goal hardening |

---

## 5. Community Momentum & Maturity

- **High‑velocity clusters**: **OpenCode** and **Pi** published releases today and track 10+ PRs each, indicating rapid iteration. **OpenAI Codex** and **Gemini CLI** also show strong PR throughput (10 each), though without releases today.
- **Mature, vocal communities**: **Claude Code** has the highest upvotes on open issues (240 👍 on copy/paste bug) but low PR activity—community patience may be wearing thin for long‑standing requests (AGENTS.md outstanding since Aug 2025). **Qwen Code** and **Gemini CLI** have significant issue depth, with P1 memory bugs and subagent failures dominating.
- **Emerging tools**: **Kimi Code CLI** and **GitHub Copilot CLI** have smaller communities (fewer comments/upvotes per issue) but are addressing critical gaps (Windows support, scheduling). Their feature requests show they are benchmarking against dominant players.
- **Release cadence**: Only OpenCode and Pi shipped today; others had no releases. This may reflect different development cycles or prioritization of internal stability over public releases.

---

## 6. Trend Signals

From cross‑tool community feedback, we identify the following industry trends:

1. **Agent instructions as a first‑class artifact.** Multiple communities (Claude, Kimi, OpenCode) demand portable, version‑controlled agent configurations (AGENTS.md, .agents/). This mirrors the `.cursorrules` pattern and signals a shift toward treating agent behavior as code.

2. **Billing transparency is a trust issue.** Claude Code’s cache billing bug (#59872) and Codex’s deterministic reset request (#9508) highlight that opaque or buggy usage metering erodes developer confidence—especially for paid tiers.

3. **Reasoning‑aware tool chains.** The explosion of `reasoning_content` issues across Gemini, Pi, and Qwen Code (400 errors on multi‑turn tool calls) suggests that 2025–2026 reasoning models are exposing brittle assumptions in CLI frameworks. Robust handling of mixed text+reasoning+tool‑call sequences is becoming a table‑stakes requirement.

4. **Memory and OOM as a scalability blocker.** Qwen Code leads with heap‑pressure compaction (#4186), but Pi and OpenCode also address session‑metadata streaming and queue‑bounding. Long‑running agents are pushing Node.js/V8 to its limits—memory‑aware designs are essential for production readiness.

5. **Accessibility and global language support.** RTL text (Claude Code), screen reader mode (Pi), and non‑UTF‑8 file handling (Kimi) indicate growing awareness that AI CLI tools must work for diverse user bases and environments.

6. **Daemon / remote session architectures.** Qwen Code’s Mode B, Gemini’s remote control, and Copilot CLI’s background agents all point toward a future where CLI tools run as persistent services, enabling headless automation, mobile connectivity, and cross‑device handoff.

7. **Provider diversity demands runtime adaptation.** Pi’s dynamic model discovery, OpenCode’s fallback model chain, and Qwen’s tool name migrations underscore that users expect CLIs to adapt to any API provider—not just the parent company’s models.

---

*Report generated from community digest data for 2026-05-17. Interpretation reflects cross‑tool analysis, not individual tool roadmaps.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-05-17 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills have garnered the most community discussion and attention. All are currently **open** PRs.

### #1: Document Typography Skill (#514)
- **Functionality**: Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents—a quality-control layer for Claude's output.
- **Discussion Highlights**: Addresses a universal pain point: "These issues affect every document Claude generates." Community resonance is strong given the ubiquity of document output.
- **Status**: Open | [PR #514](https://github.com/anthropics/skills/pull/514)

### #2: OpenDocument (ODT) Skill (#486)
- **Functionality**: Create, fill, read, and convert `.odt` and `.ods` files. Supports template filling and ODT-to-HTML conversion, targeting LibreOffice/ISO standard formats.
- **Discussion Highlights**: Fills a major gap in document format support. Unclear whether this overlaps with or complements the existing `pdf` and `docx` skills.
- **Status**: Open | [PR #486](https://github.com/anthropics/skills/pull/486)

### #3: Frontend Design Skill Improvement (#210)
- **Functionality**: Revises the existing frontend-design skill for clarity and actionability, ensuring every instruction is executable within a single conversation.
- **Discussion Highlights**: Focus on *skill quality* itself—making guidance specific enough to steer behavior without ambiguity. Reflects growing maturity in skill authoring.
- **Status**: Open | [PR #210](https://github.com/anthropics/skills/pull/210)

### #4: Skill Quality & Security Analyzers (#83)
- **Functionality**: Two meta-skills—`skill-quality-analyzer` evaluates Skills across Structure, Documentation, Examples, Resources, and Portability (5 axes); `skill-security-analyzer` audits security posture.
- **Discussion Highlights**: Meta-skills signal demand for governance and quality assurance across the Skill ecosystem. The first "meta-skill" proposals in the repo.
- **Status**: Open | [PR #83](https://github.com/anthropics/skills/pull/83)

### #5: Testing Patterns Skill (#723)
- **Functionality**: Comprehensive testing coverage: philosophy (Testing Trophy model), unit testing (AAA pattern), React component testing (Testing Library), and guidance on what *not* to test.
- **Discussion Highlights**: Practical and opinionated—community interest in standardized testing best practices for AI-generated code.
- **Status**: Open | [PR #723](https://github.com/anthropics/skills/pull/723)

### #6: ServiceNow Platform Skill (#568)
- **Functionality**: Broad ServiceNow assistant covering ITSM, ITOM, ITAM/SAM, FSM, HRSD, CSM, SPM, Vulnerability Response, Security Incident Response, and IntegrationHub.
- **Discussion Highlights**: Ambition is notable—aims to be a platform assistant, not a narrow scripting helper. Enterprise demand for AI-assisted ServiceNow workflows.
- **Status**: Open | [PR #568](https://github.com/anthropics/skills/pull/568)

### #7: AURELION Skill Suite (#444)
- **Functionality**: Four skills—`aurelion-kernel` (5-floor cognitive framework), `aurelion-advisor` (knowledge graph), `aurelion-agent` (persistent context), `aurelion-memory` (memory management).
- **Discussion Highlights**: The most complex submission to date. Community interest centers on structured cognitive frameworks for professional knowledge management.
- **Status**: Open | [PR #444](https://github.com/anthropics/skills/pull/444)

### #8: AppDeploy Skill (#360)
- **Functionality**: Deploy full-stack web apps from Claude to public URLs via AppDeploy, including lifecycle management (status checks, versioning).
- **Discussion Highlights**: Bridges AI coding and deployment—a natural progression from "write code" to "ship it." Active discussion on security boundaries.
- **Status**: Open | [PR #360](https://github.com/anthropics/skills/pull/360)

---

## 2. Community Demand Trends

From the Issues with highest engagement, five clear demand clusters emerge:

**🏢 Enterprise & Org Features**
- **Org-wide skill sharing** ([Issue #228](https://github.com/anthropics/skills/issues/228), 13 comments, 👍7): Users want direct sharing within organizations without manual file transfer. The most-upvoted Issue reflects unmet enterprise distribution needs.
- **Bedrock compatibility** ([Issue #29](https://github.com/anthropics/skills/issues/29), 4 comments): Skills currently don't work with AWS Bedrock—a blocker for enterprise cloud deployments.

**🔒 Security & Governance**
- **Trust boundary abuse** ([Issue #492](https://github.com/anthropics/skills/issues/492), 6 comments): Community skills distributed under the `anthropic/` namespace risk impersonating official Anthropic skills. Users demand namespace separation.
- **Agent governance** ([Issue #412](https://github.com/anthropics/skills/issues/412), 4 comments): Proposed skill for safety patterns—policy enforcement, threat detection, trust scoring, audit trails.

**🛠 Developer Experience & Tooling**
- **Skill-creator modernization** ([Issue #202](https://github.com/anthropics/skills/issues/202), 8 comments): Current skill-creator is "verbose, educational tone" not operational. Users want actionable instructions, not documentation.
- **SSO/enterprise auth** ([Issue #532](https://github.com/anthropics/skills/issues/532), 2 comments): `run_eval.py` depends on `ANTHROPIC_API_KEY`—incompatible with enterprise SSO.

**⚡ Reliability & Consistency**
- **Duplicate skills loading** ([Issue #189](https://github.com/anthropics/skills/issues/189), 6 comments, 👍8): `document-skills` and `example-skills` plugins install identical content, wasting context window.
- **Plugin boundary violations** ([Issue #1087](https://github.com/anthropics/skills/issues/1087), 2 comments): Plugins load *all* skills instead of declared subset.

**🔌 Integration Standards**
- **MCP exposure** ([Issue #16](https://github.com/anthropics/skills/issues/16), 4 comments): Skills should be callable via MCP protocol—treating each Skill as an API endpoint.

**Key takeaway**: The community is outgrowing the individual-"my skill disappeared" phase (Issue #62) and demanding **enterprise-grade distribution, security, and reliability**—signaling the ecosystem's maturation from hobbyist to professional use.

---

## 3. High-Potential Pending Skills

These open PRs show sustained discussion activity and are strong candidates for near-term merge:

| Skill | PR | Last Updated | Est. Priority |
|-------|-----|-------------|----------------|
| **Document Typography** | [#514](https://github.com/anthropics/skills/pull/514) | 2026-03-13 | **High** - Solves universal document quality problem |
| **AURELION Suite** | [#444](https://github.com/anthropics/skills/pull/444) | 2026-05-06 | **High** - Most comprehensive framework, actively maintained |
| **AppDeploy** | [#360](https://github.com/anthropics/skills/pull/360) | 2026-05-04 | **High** - Bridges coding→deployment gap |
| **ServiceNow** | [#568](https://github.com/anthropics/skills/pull/568) | 2026-04-23 | **Medium-High** - Enterprise demand, broad scope |
| **Testing Patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 2026-04-21 | **Medium-High** - Practical, fills testing gap |
| **PDF Fix (case sensitivity)** | [#538](https://github.com/anthropics/skills/pull/538) | 2026-04-29 | **Medium** - Bugfix, likely fast-tracked |
| **SAP-RPT-1-OSS** | [#181](https://github.com/anthropics/skills/pull/181) | 2026-03-16 | **Medium** - Niche but strong enterprise signal |
| **Shodh-Memory** | [#154](https://github.com/anthropics/skills/pull/154) | 2026-03-03 | **Medium** - Persistent context across conversations |

**Note**: The AURELION, AppDeploy, and ServiceNow PRs have the most recent update dates with substantial comment threads, suggesting active author engagement and maintainer review. The Document Typography and Testing Patterns skills have the widest potential user base.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for Skills that transform Claude from a single-session code generator into a production-grade document processor and enterprise workflow orchestrator**, evidenced by the dominance of document-quality tools (typography, ODT, DOCX), enterprise platform integrations (ServiceNow, SAP, AppDeploy), and cross-session persistence (Shodh-Memory, AURELION)—all layered with growing demands for security, governance, and org-wide distribution infrastructure.

---

# Claude Code Community Digest — 2026-05-17

## Today's Highlights
The community remains focused on two long-standing pain points: **copy/paste formatting corruption** (Issue #18170) and the **missing AGENTS.md and `.agents/skills/` support** (Issue #31005). A worrying new billing bug surfaced today (#59872) where `cache_read` tokens on Opus 4.6 are counted at full rate despite cache hits, potentially burning through weekly quotas. No releases landed in the last 24 hours.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#18170 – Copy/paste from terminal includes unwanted indentation and trailing spaces](https://github.com/anthropics/claude-code/issues/18170)**  
   *116 comments · 240 👍*  
   **Why it matters:** The most-upvoted open issue. Users copying code or text from the terminal get leading tabs/spaces and trailing whitespace, breaking every paste. Affects daily workflow for almost everyone.

2. **[#31005 – Support for AGENTS.md and .agents/skills/](https://github.com/anthropics/claude-code/issues/31005)**  
   *11 comments · 164 👍*  
   **Why it matters:** A feature request that has been repeatedly raised since August 2025 with zero official response. Users want shareable, versionable agent instructions (analogous to `.cursorrules` or `.clinerules`). Frustration is high.

3. **[#13843 – Share conversation context from Claude.ai to Claude Code](https://github.com/anthropics/claude-code/issues/13843)**  
   *14 comments · 68 👍*  
   **Why it matters:** Users plan on Claude.ai and then want to continue in the CLI without losing context. This is a key integration gap.

4. **[#32982 – Remote Control sessions die after ~20 min idle](https://github.com/anthropics/claude-code/issues/32982)**  
   *9 comments · 52 👍*  
   **Why it matters:** All Remote Control sessions silently disconnect after 5–30 minutes of inactivity, ignoring keepalives. Critical for anyone using persistent agents or background work.

5. **[#38005 – RTL Support for Hebrew & Arabic](https://github.com/anthropics/claude-code/issues/38005)**  
   *13 comments · 32 👍*  
   **Why it matters:** Missing bidirectional text rendering blocks adoption in large language markets. Labeled `area:a11y`.

6. **[#36649 – Context window defaulting back to 200k](https://github.com/anthropics/claude-code/issues/36649)**  
   *17 comments · 10 👍*  
   **Why it matters:** A regression causing the context window to fall back to the 200K default instead of using the user's configured larger window. Breaks long-session workflows.

7. **[#39027 – Background task notifications trigger autonomous API calls with bypassPermissions](https://github.com/anthropics/claude-code/issues/39027)**  
   *9 comments · 7 👍*  
   **Why it matters:** A security/privacy bug where completed background tasks generate synthetic user messages that trigger autonomous tool calls, bypassing permission checks. Model responds as if it were the user.

8. **[#16288 – Plugin hooks not loaded from external hooks.json file](https://github.com/anthropics/claude-code/issues/16288)**  
   *14 comments · 14 👍*  
   **Why it matters:** Plugin hooks defined in an external `hooks.json` are silently ignored. Breaks the plugin extensibility model.

9. **[#59872 – Opus 4.6 cache_read tokens counted at full rate despite cache hits](https://github.com/anthropics/claude-code/issues/59872)**  
   *6 comments · new today*  
   **Why it matters:** On Max 20x plan, `cache_read_input_tokens` appear to be billed at full rate, consuming disproportionate weekly quota. If confirmed, this is a costly billing bug.

10. **[#58909 – Hook event `permission_prompt` stops firing during active thinking](https://github.com/anthropics/claude-code/issues/58909)**  
    *4 comments · 6 👍*  
    **Why it matters:** A regression in 2.1.141 that breaks downstream hooks subscribed to permission prompts when the model is in a thinking phase. TUI renders correctly but hooks are silent.

## Key PR Progress
Only one pull request was updated in the last 24 hours: **[#58673](https://github.com/anthropics/claude-code/pull/58673)** with a trivial title `s`. No significant PR activity to report.

## Feature Request Trends
The most-requested feature directions, distilled from open issues:

- **Agent Instruction Files (AGENTS.md, `.agents/skills/`)** – A persistent top ask since August 2025. Users want portable, shareable agent configs akin to `.cursorrules`.
- **Conversation Sharing** – Import/export context between Claude.ai and Claude Code.
- **RTL/Bidirectional Text Support** – Accessibility for Hebrew, Arabic, and similar scripts.
- **Enhanced Permissions & Allow Rules** – Persistent allow rules, especially for paths under `~/.claude/`, need runtime matching fixes.
- **Plugin/Hook Reliability** – External hook loading, hook events during thinking, and stable MCP transport.
- **Context Window Management** – Reliable larger context windows, plus transparency on cache billing.

## Developer Pain Points
Recurring themes from the highest-traffic issues:

- **Copy/paste formatting corruption** (#18170) remains the top pain point after months.
- **Session reliability** – Remote Control disconnects, auto-archiving, stale task lists, and background sessions not resumable.
- **Billing confusion** – Cache token counting at full rate (#59872) and unexpected “extra usage” requirements (#58730).
- **Authentication loop** (#36797) still unresolved for some users with active subscriptions.
- **MCP transport fragility** – Stdio connections dropped during response generation (#47378), OAuth failures for Meta Ads MCP (#59924).
- **Regression sensitivity** – Recent releases (2.1.141) introduced hook regressions (#58909) and terminal corruption (#59539).
- **Sub-agent hallucinations** – Background sub-agents returning context-decoupled completions (#59903) is a worrying quality issue.
- **Platform-specific bugs** – Windows suffers from `/desktop` failures (#59824), LSP spawn errors (#59925), and UI unresponsiveness (#59899).

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-17

---

## 1. Today’s Highlights

The community remains active on stability and cross-platform polish, with a long‑running remote compact task bug (#14860) still gathering attention and a popular PDF‑support feature request (#1797) reaching 137 👍. On the PR side, a multi‑PR stack to revamp next‑turn state for remote clients is making headway, and a new skill_search tool (#23118) was merged. No new releases were published in the last 24 hours.

---

## 2. Releases

No new versions of Codex CLI, Codex Desktop, or the VS Code extension were released in the past 24 hours.

---

## 3. Hot Issues (10 noteworthy)

1. **[#14860 – Error running remote compact task](https://github.com/openai/codex/issues/14860)**  
   *Bug, context* – 71 comments, 56 👍. Users on Codex CLI 0.114.0 and GPT‑5.4 report a failure when running `compact` on remote sessions. The issue remains open for two months with no fix yet; it’s a top community concern.

2. **[#9508 – Make Weekly Limit Reset Deterministic](https://github.com/openai/codex/issues/9508)**  
   *Enhancement, rate‑limits* – 24 comments, 20 👍. Pro users want a predictable reset window for the weekly usage cap instead of the current ambiguous schedule.

3. **[#1797 – PDF support](https://github.com/openai/codex/issues/1797)**  
   *Enhancement, agent* – 17 comments, 137 👍. Highly voted request to let Codex read text, tables, and charts from PDF files – a clear signal of demand for richer document ingestion.

4. **[#11744 – `npm install -g @openai/codex@latest` broken on Windows](https://github.com/openai/codex/issues/11744)**  
   *Bug, CLI* – 14 comments, 18 👍. A packaging change broke the global npm install on Windows 11, affecting new users on that platform.

5. **[#20741 – Project chat histories disappeared after update](https://github.com/openai/codex/issues/20741)**  
   *Bug, app, session* – 11 comments, 5 👍. A recent Codex Desktop update (26.429.30905) caused all project chat histories to vanish on macOS, causing significant disruption.

6. **[#21700 – Computer Use Chrome extension unavailable in Chrome Web Store](https://github.com/openai/codex/issues/21700)**  
   *Bug, windows‑os, app, computer‑use* – 9 comments, 16 👍. The official Chrome extension required for Computer Use integration errors in the store, with no offline installer available.

7. **[#18456 – reqwest HTTP clients missing User‑Agent → Cloudflare 403 from HKG edge](https://github.com/openai/codex/issues/18456)**  
   *Bug, windows‑os, app* – 9 comments. Rust‑based HTTP requests are blocked by Cloudflare on some regions (e.g., Hong Kong) because the `reqwest` default User‑Agent is flagged as bot traffic.

8. **[#21704 – Chrome/browser‑use `setupAtlasRuntime` hang when `/backend‑api/me` probe doesn’t complete](https://github.com/openai/codex/issues/21704)**  
   *Bug, app, connectivity, browser* – 8 comments. Desktop app hangs during browser‑use setup if the ambient authentication probe fails, leaving the UI frozen.

9. **[#17991 – Windows Summary tab shows false GitHub CLI / PR errors for WSL repos](https://github.com/openai/codex/issues/17991)**  
   *Bug, windows‑os, app* – 7 comments. The Summary tab on Windows reports spurious status errors for repos hosted under WSL, plus logs `ENOENT` on `.git` paths.

10. **[#20601 – TUI freezes during idle long wait while session continues](https://github.com/openai/codex/issues/20601)**  
    *Bug, TUI* – 5 comments (closed). The terminal UI becomes unresponsive during long waits (e.g., tool execution), even though the underlying session finishes normally.

---

## 4. Key PR Progress (10 important)

1. **[#23128 – Fix TUI stream cleanup after turn errors](https://github.com/openai/codex/pull/23128)**  
   *etraut‑openai* – Prevents the TUI from leaving partial streaming output visible after a network disconnect, avoiding stale diff/SVG content.

2. **[#23127 – Hide ChatGPT usage link for non‑OpenAI status](https://github.com/openai/codex/pull/23127)**  
   *etraut‑openai* – Removes the irrelevant ChatGPT usage‑page link from `/status` when using custom providers (e.g., Bedrock), reducing confusion.

3. **[#22929 – Harden CLI rate limit window labels](https://github.com/openai/codex/pull/22929)**  
   *ase‑openai* – Makes the CLI display whatever rate‑limit period the server returns, rather than assuming fixed 5‑hour/week windows – important for custom deployments.

4. **[#23123 – Support `--output‑schema` for `exec resume`](https://github.com/openai/codex/pull/23123)**  
   *etraut‑openai* – Adds structured output support to resumed sessions, fixing #22998. Multi‑turn automation can now keep schema‑validated JSON output.

5. **[#23121 – TUI: keep cleared Fast tier from reappearing after side‑thread resume](https://github.com/openai/codex/pull/23121)**  
   *etraut‑openai* – Fixes a UI bug where disabling Fast mode in the TUI would visually revert when resuming from a side thread.

6. **[#23118 – feat(tools): `skill_search` tool](https://github.com/openai/codex/pull/23118)**  
   *dylan‑hurd‑oai* – New tool that lets the model search for skills at runtime instead of embedding all descriptions in the developer message, improving scalability.

7. **[#22999 – fix(permissions): truncate rules as tokens](https://github.com/openai/codex/pull/22999)**  
   *dylan‑hurd‑oai* – Changes permission rule truncation from bytes to tokens (closed). Prevents partial‑character cutoffs in rule text.

8. **[#22509 – Add app‑server next‑turn state API (6 of 7)](https://github.com/openai/codex/pull/22509)**  
   *etraut‑openai* – Part of a 7‑PR stack to allow remote clients to update thread next‑turn defaults (model, plan mode, etc.) without starting a turn, plus broadcast notifications.

9. **[#23094 – goal: pause continuation loops on usage limits and blockers](https://github.com/openai/codex/pull/23094)**  
   *etraut‑openai* – `/goal` will now pause when hitting rate limits or repeated resource blockers, avoiding wasteful token burning – addresses #22833, #22245, #23067.

10. **[#23093 – sdk/python: add first‑class login support](https://github.com/openai/codex/pull/23093)**  
    *aibrahim‑oai* – (closed) Exposes account login, logout, and status inspection directly in the Python SDK, removing the need for external auth handling.

---

## 5. Feature Request Trends

- **PDF & document support** (#1797) is the most upvoted request, indicating a strong need for agents that can parse structured PDFs (text, tables, charts).
- **Deterministic rate‑limit resets** (#9508) – users want clarity on when their weekly quota refreshes, rather than the current opaque schedule.
- **Project‑isolated chat contexts** (#17185) – developers with multiple active projects need separate conversation histories to avoid context contamination.
- **Multi‑agent TUI view** (#22321) – power users managing several parallel agents want a unified dashboard to monitor and control them.
- **Chronicle control** (#23124) – Plus users request a UI toggle to disable background memory summarization that consumes their quota.

---

## 6. Developer Pain Points

- **Cloudflare blocks on Linux/WSL2** – Several reports (#17860, #18456, #21346) highlight that `rustls` TLS fingerprinting or missing User‑Agent headers cause 403 challenges, making Codex unusable on some networks.
- **Remote / mobile connectivity** – Multiple issues (#22733, #22802, #22831, #23078) describe “Waiting for desktop…”, “Secure setup failed”, or network‑lost errors when connecting from iOS/Android or SSH hosts.
- **Session and chat history loss** – #20741 and #23077 show that updates can wipe project histories and that parallel use of CLI and VS Code extension leads to session conflicts.
- **TUI instability** – Freezes (#20601), stale Fast mode display (#23121), and incomplete stream cleanup (#23128) degrade the terminal experience.
- **Rate‑limit confusion** – Plus users report that background features like Chronicle (#23124) or `/goal` loops (#23094) can silently burn their limited quota without visible feedback.
- **Platform‑specific bugs** – Windows users face broken npm installs (#11744), false git status errors for WSL (#17991), and missing Chrome extensions (#21700). macOS users complain about GPU/CPU drain from the pet overlay (#20680) and long‑session high‑CPU usage (#23026).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-05-17

## Today’s Highlights
No new releases landed in the past 24 hours, but the community and maintainers stayed busy across multiple fronts. A cluster of high‑priority bug reports around subagent recovery (false success after max turns) and shell command hangs continue to draw attention. On the PR side, several important cross‑platform fixes are moving forward, including Windows shell fallback, SEA build forking, and a critical fix for exponential token leaks in the state snapshot processor.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 selected)
1. **[#22323 – Subagent recovery after MAX_TURNS reports GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   **Priority P1, Bug** – A subagent (e.g., `codebase_investigator`) returns `status: "success"` even after hitting the turn limit and doing no real work. This masks actual failures and wastes user trust. Community reactions (👍2) suggest this is a frustrating pattern.

2. **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   **Priority P2, Bug** – Users report that custom skills and sub‑agents are almost never invoked autonomously, even when the task is directly related. Purely anecdotal but aligns with other “agent self‑awareness” requests.

3. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   **Priority P1, Feature** – Follow‑up on behavioral evals (76 tests already). The team wants systematic component‑level testing across six Gemini models. High impact for quality assurance.

4. **[#27149 – Google OAuth login mapping may fail for personal accounts](https://github.com/google-gemini/gemini-cli/issues/27149)**  
   **Security** – Users hitting 403 errors due to blocked API access. The issue suggests OAuth entitlement path might not be reliably mapped. Fresh report (yesterday) with 5 comments already – urgent.

5. **[#25166 – Shell command execution gets stuck with “Waiting input” after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   **Priority P1, Bug** – Repeated reports of simple CLI commands hanging after finishing. High community agreement (👍3). A major workflow blocker.

6. **[#23571 – Model frequently creates tmp scripts in random spots](https://github.com/google-gemini/gemini-cli/issues/23571)**  
   **Priority P2, Bug** – When shell execution is restricted, the model scatters edit scripts across directories, creating cleanup overhead. Impacts commit hygiene.

7. **[#22267 – Browser Agent ignores settings.json overrides (e.g., maxTurns)](https://github.com/google-gemini/gemini-cli/issues/22267)**  
   **Priority P2, Bug** – Configuration overrides read correctly by `AgentRegistry` are ignored by the browser agent. Undermines customisation.

8. **[#26525 – Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   **Priority P2, Security** – Auto Memory sends transcripts to model context before redaction, and may log sensitive data. A privacy/security concern.

9. **[#22672 – Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
   **Priority P2, Customer Issue** – The model sometimes uses `git reset --force` or other destructive commands when safer alternatives exist. Community (👍1) wants better guardrails.

10. **[#21421 – Gemini CLI should periodically reflect and recommend skill creation](https://github.com/google-gemini/gemini-cli/issues/21421)**  
    **Priority P2/P3, Feature** – Idea to have the agent monitor its own performance and suggest new skills or memory updates. Linked to #20062. Proactive self‑improvement.

## Key PR Progress (10 selected)
1. **[PR #27170 – Prevent dropping valid model turns with empty text parts](https://github.com/google-gemini/gemini-cli/pull/27170)**  
   **Priority P1, Area/agent** – Fixes 400 error (“function call turn comes immediately after a user turn”) by not filtering out turns that contain a `functionCall` plus an empty text part. Just opened today.

2. **[PR #27157 – Non‑interactive env and PTY skip for Full Access shell exec](https://github.com/google-gemini/gemini-cli/pull/27157)**  
   **Priority P1, Area/agent** – Injects non‑interactive environment variables so `npm`, `apt`, etc. auto‑confirm, preventing hangs in `--full-access` mode.

3. **[PR #27158 – Cycle Shift+Tab through Full Access and add “⏵⏵ auto mode” label](https://github.com/google-gemini/gemini-cli/pull/27158)**  
   **Priority P2/P3, UX** – Adds Full Access to the in‑session mode cycle and shows a visible indicator. Closes a UX gap.

4. **[PR #27156 – Opt‑in trust for MCP readOnlyHint in Plan Mode](https://github.com/google-gemini/gemini-cli/pull/27156)**  
   **Area/agent** – New setting `general.plan.trustReadOnlyHint` (default false) allows MCP read‑only tools to run silently in Plan Mode instead of prompting every time.

5. **[PR #27115 – Restore extension after failed update](https://github.com/google-gemini/gemini-cli/pull/27115)**  
   **Priority P1, Area/extensions** – Backs up extensions before update and restores on failure, preventing broken state. Fixes #21671.

6. **[PR #26734 – Fix audio/wav API errors and context overestimation](https://github.com/google-gemini/gemini-cli/pull/26734)**  
   **Priority P2, Area/agent** – Corrects unsupported audio nesting inside `function_response.parts` and fixes context size overestimation. Important for multimodal workflows.

7. **[PR #26758 – Prevent exponential token leak in StateSnapshotAsyncProcessor](https://github.com/google-gemini/gemini-cli/pull/26758)**  
   **Priority P1, Area/agent** – Critical bug fix: episodic context graph was causing exponential token growth due to failure to filter already‑summarised nodes. Reduces model costs.

8. **[PR #26752 – Add Windows shell fallback support](https://github.com/google-gemini/gemini-cli/pull/26752)**  
   **Core** – When `powershell.exe` or `cmd.exe` are unavailable (Git Bash, MSYS, enterprise restrictions), falls back to other shells. Improves Windows parity.

9. **[PR #27028 – Sub‑second /chat loading for large session histories](https://github.com/google-gemini/gemini-cli/pull/27028)**  
   **Area/core, Performance** – Reduces `/chat` load time from 25+ seconds to ~634ms for 59 sessions / 2.3GB JSONL. Three bottlenecks eliminated.

10. **[PR #27161 – Prevent ghost text wrapping stall](https://github.com/google-gemini/gemini-cli/pull/27161)**  
    **Fix** – Addresses infinite loop when ghost completion text contains a code point wider than the input width. Closes #19985.

## Feature Request Trends
- **AST‑aware tooling** – Several issues (#22745, #22746, #22747) explore using AST grep/parsing for precise file reads, search, and codebase mapping to reduce noise and token waste.
- **Agent self‑awareness & skill recommendation** – Users want the CLI to understand its own capabilities, hotkeys, and CLI flags (#21432), and to periodically suggest new skills or memory updates (#21421).
- **Backgroundable subagents** – Request to send local agents to background with Ctrl+B (#22741) to parallelise non‑blocking tasks like linting.
- **Better MCP integration** – Opt‑in trust for read‑only tools in Plan Mode (#27156) and more control over MCP tool execution.
- **Robust evaluation infrastructure** – Stabilise internal evals (#23166, #24353), make steering tests always pass (#23313).

## Developer Pain Points
- **Subagent reliability** – False success reporting after max turns (#22323), agents ignoring config overrides (#22267), and subagents running without permission after updates (#22093).
- **Shell command hangs** – Commands “stuck waiting input” after completion (#25166), interactive prompts blocking automation (#27157).
- **Memory system issues** – Auto Memory retrying low‑signal sessions indefinitely (#26522), invalid patches silently skipped (#26523), secret redaction happening after context exposure (#26525).
- **Destructive command risk** – Model using `--force` or `git reset` when safer alternatives exist (#22672), scattered tmp scripts (#23571).
- **Cross‑platform gaps** – Windows hangs and zombie processes (#26392), missing shell fallback (#26752), Wayland browser agent failures (#21983).
- **High memory / token waste** – Context overestimation with audio (#26734), exponential token leak in snapshot processor (#26758), large `/chat` load times (#27028).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest – 2026-05-17

## Today’s Highlights
No new release dropped in the last 24 hours, but the community surfaced several critical bugs and feature requests. A v1.0.48 regression broke Android/Termux support, the long-standing sudo hang issue remains unresolved, and users are pushing for scheduling commands (`/every`, `/after`) and a unified `/config` slash command. Windows startup failures and background agent freezes also caught attention.

## Releases
No releases published in the last 24 hours.

---

## Hot Issues (10 of 15 updated in last 24h)

1. **[#1082 – Copilot CLI hangs on sudo commands](https://github.com/github/copilot-cli/issues/1082)**  
   *Opened Jan 2026, updated May 16*  
   Critical usability bug: `sudo` prompts are never forwarded, causing indefinite hangs. 11 👍, 3 comments, no fix yet. Affects any task requiring elevated permissions.

2. **[#3333 – Android/Termux broken in v1.0.48 (glibc dependency)](https://github.com/github/copilot-cli/issues/3333)**  
   *Opened May 15, updated May 17*  
   A native Rust addon now requires glibc, rendering Copilot CLI unusable on Termux (Bionic libc). High priority for mobile developers.

3. **[#3356 – Request: `/every` and `/after` slash commands for scheduled prompts](https://github.com/github/copilot-cli/issues/3356)**  
   *Opened May 17*  
   Seeks Claude Code `/loop` parity: schedule one-shot or recurring prompts within a session. No comments yet, but a clear gap in workflow automation.

4. **[#3355 – Configurable context window for Claude Opus 4.6](https://github.com/github/copilot-cli/issues/3355)**  
   *Opened May 17*  
   Copilot caps Opus 4.6 at 200K tokens, despite model supporting 1M. Causes premature compaction in deep sessions. High interest for power users.

5. **[#3354 – CTRL+T does nothing with BYOK models](https://github.com/github/copilot-cli/issues/3354)**  
   *Opened May 17*  
   Bring-Your-Own-Key users cannot view model thinking/reasoning. No output or state change, breaking a key debugging feature.

6. **[#3352 – Feature request: `/config` slash command](https://github.com/github/copilot-cli/issues/3352)**  
   *Opened May 16*  
   Users want a single interactive editor for all writable settings, replacing scattered `/model`, `/theme`, `/experimental`, etc. Parity with Claude Code’s `/config`.

7. **[#3351 – Windows startup failure after `/update`](https://github.com/github/copilot-cli/issues/3351)**  
   *Opened May 16*  
   After applying an update, the `copilot` command silently exits with code 0. No error output. Affects Windows users.

8. **[#3350 – Background sub-agents never complete](https://github.com/github/copilot-cli/issues/3350)**  
   *Opened May 16*  
   `task` with `mode: "background"` and general‑purpose agents hang indefinitely. No timeout or completion notification.

9. **[#2181 – `COPILOT_CUSTOM_INSTRUCTIONS_DIR` regression](https://github.com/github/copilot-cli/issues/2181)**  
   *Opened Mar 20, updated May 17*  
   In v1.0.9, custom instructions from multiple directories are not loaded (worked in v1.0.8). Regression still open after 2 months.

10. **[#3345 – Hooks not loaded in non‑interactive mode](https://github.com/github/copilot-cli/issues/3345)**  
    *Opened May 16, closed May 17*  
    `.github/hooks/*.json` work interactively but are ignored in `copilot -p "..."` mode. Closed as confirmed bug, pending fix.

---

## Key PR Progress (2 updated in last 24h)

- **[#3353 – Copilot subscription no longer required (OPEN)](https://github.com/github/copilot-cli/pull/3353)**  
  *Opened May 16*  
  Proposes removing the Copilot subscription check entirely. No comments yet; could signal a shift in access model. Community watching closely.

- **[#140 – Add GitHub Actions for issue management (CLOSED)](https://github.com/github/copilot-cli/pull/140)**  
  *Created Sep 2025, merged/closed May 16*  
  Introduces automated triage, labeling, and stale‑issue handling. Internal maintenance improvement, not user‑facing.

---

## Feature Request Trends
From recent issues and discussions, the most requested feature directions are:

- **Workflow scheduling**: `/every` and `/after` commands for recurring or delayed prompts (Claude Code parity).
- **Unified configuration editor**: A single `/config` slash command to manage all settings.
- **Model‑level context control**: Allow users to raise the token cap for models that support larger contexts (e.g., Claude Opus 4.6).
- **MCP connection thresholds**: Configurable slow‑connection warning timeouts for authentication‑heavy servers.
- **Session management improvements**: Restore alphanumeric session IDs and make session resumption more predictable.

---

## Developer Pain Points
Recurring frustrations drawn from high‑frequency or high‑reaction issues:

- **Sudo hangs** (#1082) – No password prompt blocks package installations and system‑level tasks.
- **Termux breakage** (#3333) – Native addon glibc dependency locks out Android developers.
- **Custom instructions regression** (#2181) – `COPILOT_CUSTOM_INSTRUCTIONS_DIR` still broken for multiple directories.
- **Non‑interactive hook gap** (#3345) – Hooks silently ignored in `copilot -p` mode.
- **Context window hard cap** (#3355) – Premature compaction forces users to restart sessions unnecessarily.
- **BYOK thinking pane** (#3354) – CTRL+T useless for BYOK model users.
- **Windows update failure** (#3351) – Silent crash after `/update` with no diagnostic output.
- **Background agents stuck** (#3350) – Background tasks never finish, blocking automated pipelines.

These pain points highlight a need for better platform compatibility, more user‑friendly configuration, and transparent error handling.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-17

## Today's Highlights
The community saw no new releases, but two long-standing Windows compatibility bugs were closed after fixes (PowerShell syntax and Unix pipeline generation). Meanwhile, actionable feature requests around shared configurations and multi-device session handoff continue to gain traction, and a new wave of bugs affecting the Web UI and VS Code integration surfaced.

---

## Releases
No new releases in the last 24 hours. The latest stable remains **v1.44.0** (referenced in recent issues).

---

## Hot Issues (9 items)

### #2152 – [Feature Request] Support global `~/.kimi/AGENTS.md` for multi-project shared conventions
**Why it matters:** Developers managing 10+ projects currently have to copy the same rules into each project’s `AGENTS.md`. A global fallback would eliminate this friction.  
**Community reaction:** 3 upvotes, 4 comments; consensus that this is a common pain point.  
[GitHub Issue #2152](https://github.com/MoonshotAI/kimi-cli/issues/2152)

### #2314 – Prompts take way too long to complete in general
**Why it matters:** Simple tasks like pushing data to NeonDB take ~5 minutes, with the agent “overthinking.” Performance regressions directly impact developer productivity.  
**Community reaction:** 2 comments, no upvotes yet; user expects faster execution for deterministic operations.  
[GitHub Issue #2314](https://github.com/MoonshotAI/kimi-cli/issues/2314)

### #2269 – [Feature Request] Remote Control / Multi-Device Session Handoff
**Why it matters:** Users want to start a CLI session on one device and continue on another (laptop, web, mobile). This is a major workflow enabler for hybrid setups.  
**Community reaction:** 2 comments; the request is still open with no official response.  
[GitHub Issue #2269](https://github.com/MoonshotAI/kimi-cli/issues/2269)

### #2194 – [CLOSED] [bug] Agent generates PowerShell 7.x syntax incompatible with default PowerShell 5.x
**Why it matters:** Windows users stuck on PowerShell 5.x cannot run generated commands. The fix has been merged (see PR #1360).  
**Community reaction:** 1 comment; closed today.  
[GitHub Issue #2194](https://github.com/MoonshotAI/kimi-cli/issues/2194)

### #2192 – [CLOSED] [bug] Agent repeatedly generates Unix pipeline commands (head/tail) incompatible with PowerShell
**Why it matters:** Similar Windows compatibility issue causing silent failures. Also closed today.  
**Community reaction:** 1 comment; resolved.  
[GitHub Issue #2192](https://github.com/MoonshotAI/kimi-cli/issues/2192)

### #2312 – [bug] Web UI: Clicking on archived sessions does not open them
**Why it matters:** Critical UX bug on macOS; archived sessions become inaccessible via the Web UI.  
**Community reaction:** 1 comment; no workaround mentioned yet.  
[GitHub Issue #2312](https://github.com/MoonshotAI/kimi-cli/issues/2312)

### #2315 – VS Code Integrated Terminal: Ctrl+V paste image does nothing (Windows)
**Why it matters:** Image-based inputs (e.g., screenshots, diagrams) are completely broken in VS Code on Windows.  
**Community reaction:** 0 comments; newly filed today.  
[GitHub Issue #2315](https://github.com/MoonshotAI/kimi-cli/issues/2315)

### #2313 – [bug] `'utf-8' codec can't decode byte 0x97 in position 462: invalid start byte`
**Why it matters:** A non-UTF-8 file in the project directory crashes the CLI. This breaks users on Windows with certain file encodings.  
**Community reaction:** 0 comments; reported on v1.44.0.  
[GitHub Issue #2313](https://github.com/MoonshotAI/kimi-cli/issues/2313)

### #2311 – [bug] First question claims 19516 TPM, which seems weird
**Why it matters:** Token-per-minute counter shows an implausibly high number on first request, confusing users about actual usage.  
**Community reaction:** 0 comments; user suspects a bug in the TPM reporting logic.  
[GitHub Issue #2311](https://github.com/MoonshotAI/kimi-cli/issues/2311)

---

## Key PR Progress (3 items)

### #1360 – [CLOSED] fix: replace `platform.version()` with system+release for HTTP headers
**What it does:** Fixes `httpx.LocalProtocolError` on Linux where kernel version strings starting with `#` violate HTTP header specs.  
**Impact:** Enables proper HTTP communication on Ubuntu and other distributions. Merged and closed today.  
[GitHub PR #1360](https://github.com/MoonshotAI/kimi-cli/pull/1360)

### #2236 – [OPEN] fix(utils): bound broadcast queues and cap web store cache to prevent memory leaks
**What it does:** Prevents OOM when a slow consumer causes unbounded `asyncio.Queue` growth, and caps the Web store session cache to avoid holding thousands of sessions in memory.  
**Impact:** Critical for users with long-running sessions or many projects. Still under review.  
[GitHub PR #2236](https://github.com/MoonshotAI/kimi-cli/pull/2236)

### #2249 – [OPEN] feat(shell): unified approval modes with toolbar badges and temporary toasts
**What it does:** Consolidates four different auto-approval mechanisms (`--yolo`, `--afk`, `/yolo`, `/afk`, session button) into a single consistent UI with visual badges and toasts.  
**Impact:** Reduces confusion and improves discoverability of approval modes. Still open.  
[GitHub PR #2249](https://github.com/MoonshotAI/kimi-cli/pull/2249)

---

## Feature Request Trends

Based on recent issues, three feature directions are gaining momentum:

1. **Global configuration & conventions**  
   Users want a `~/.kimi/AGENTS.md` that applies across all projects, reducing duplication. (#2152)

2. **Cross-device session continuity**  
   The ability to start a CLI session on one device and resume on another (laptop, web, mobile) is a recurring desire. (#2269)

3. **Smarter auto-approval controls**  
   The PR #2249 hints at community demand for a unified, visually clearer approval system beyond the current four overlapping modes.

Smaller requests include improved token usage transparency (#2311) and support for non-UTF-8 file handling.

---

## Developer Pain Points

- **Slow task execution** – The CLI “overthinks” simple database pushes, causing multi-minute delays. (#2314)
- **Windows incompatibility** – Agent-generated PowerShell and Unix commands break on default Windows 5.x; fixes are now in, but the pain is ongoing for users on older configurations. (#2194, #2192)
- **Image paste broken in VS Code** – A critical workflow block for Windows developers using screenshots. (#2315)
- **Encoding errors with non-UTF-8 files** – The CLI crashes instead of gracefully handling binary or non-UTF-8 files. (#2313)
- **Web UI regression** – Archived sessions cannot be accessed via the Web UI. (#2312)
- **TPM reporting bug** – Misleading token-per-minute counter on first query. (#2311)

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 OpenCode 社区技术日报。

---

## OpenCode 社区技术日报 (2026-05-17)

### 1. 今日亮点
今日发布了两个维护版本 v1.15.2 和 v1.15.3，主要修复了异步命令丢失上下文和大型文件读取时的性能问题。社区中关于“技能（Skills）”系统的讨论热度不减，同时多个与模型兼容性相关的 Bug 正在通过新的 PR 积极解决，尤其是针对 Qwen3 和 DeepSeek 等模型的集成问题。

### 2. 版本发布
今日发布了 **v1.15.3** 和 **v1.15.2** 两个版本。

- **v1.15.3** ([查看](https://github.com/anomalyco/opencode/releases/tag/v1.15.3)): 核心修复了读取大型文件可能造成资源浪费的问题。TUI 修复了异步命令丢失活动实例上下文的关键 Bug，该问题可能导致 Agent 生成和 GitHub 驱动的运行中断。
- **v1.15.2** ([查看](https://github.com/anomalyco/opencode/releases/tag/v1.15.2)): 核心优化了关于 Shell、任务和待办事项流程的提示，减少不必要的交互；修复了注入实例中同步事件未到达项目级订阅者的问题。TUI 优化了置顶会话的排序逻辑。

### 3. 热门议题 (Top 10)

1.  **[[OPEN] Auto-compaction infinite loop]](https://github.com/anomalyco/opencode/issues/15533)**：当助手自然结束其轮次时，自动压缩会触发无限循环并注入假消息。社区讨论热烈（23条评论），这是个严重的会话管理 Bug。
2.  **[[OPEN] [FEATURE]: Add /skills command]](https://github.com/anomalyco/opencode/issues/7846)**：社区强烈要求（72 👍）新增 `/skills` 命令来列出和快速调用技能。表明用户对技能系统有很高的快速访问需求。
3.  **[[CLOSED] Press ESC again to interrupt does not work]](https://github.com/anomalyco/opencode/issues/888)**：旧版中按 ESC 无法中断 LLM 的 Bug 被再次提及（22条评论），虽然已关闭，但说明该基础交互的稳定性对用户至关重要。
4.  **[[OPEN] Progress halts with Qwen 3.6]](https://github.com/anomalyco/opencode/issues/24316)**：Qwen 3.6 模型在控制台中输出裸工具调用时导致进度挂起。这是一个与特定模型集成相关的阻塞性问题。
5.  **[[OPEN] Error: 402 Insufficient Balance]](https://github.com/anomalyco/opencode/issues/27593)**：用户在明明有使用配额时，却收到特定模型（ds4-flash）的“余额不足”错误，引发了社区的广泛关注和讨论（15条评论，12 👍）。
6.  **[[OPEN] ACP, Zed: does not support native changes review]](https://github.com/anomalyco/opencode/issues/4240)**：用户期望 OpenCode 像其他 Agent 一样在 Zed 编辑器中支持原生变更审查，这是一个重要的 IDE 集成缺口（18 👍）。
7.  **[[OPEN] Setting to prevent TUI scrolling when new messages are streamed-in]](https://github.com/anomalyco/opencode/issues/7648)**：希望在流式输出时固定 TUI 界面，防止自动滚动，这是一个影响阅读体验的高频需求（11 👍）。
8.  **[[OPEN] Winget installation option for windows]](https://github.com/anomalyco/opencode/issues/5121)**：请求官方支持 Winget 安装方式，用户自行发现的包版本与 Release 版本不一致，暴露了分发方式的管理问题（21 👍）。
9.  **[[OPEN] LSP detection in monorepo not working]](https://github.com/anomalyco/opencode/issues/7690)**：在 Monorepo 根目录启动 OpenCode 时，无法正确检测子项目的 LSP（如 ESLint）。这是影响大型项目开发者的关键问题（22 👍）。
10. **[[OPEN] [MaxDepth] placeholders leak into tool schemas]](https://github.com/anomalyco/opencode/issues/27946)**：`[MaxDepth]` 占位符泄漏到工具定义中，违反 JSON Schema 规范，导致 API 400 错误。这是一个严重的代码生成 Bug。

### 4. 关键 PR 进展 (Top 10)

1.  **[[OPEN] feat(session): add configurable fallback model chain]](https://github.com/anomalyco/opencode/pull/27939)**：允许配置降级模型链，当主模型失败时自动切换，极大地增强了会话的健壮性。
2.  **[[OPEN] fix: keep paste badges readable]](https://github.com/anomalyco/opencode/pull/27991)**：修复了当主题背景透明时，粘贴、图片、PDF 徽章文本难以辨认的问题，改进了 TUI 的可读性。
3.  **[[OPEN] fix: merge adjacent reasoning cycles]](https://github.com/anomalyco/opencode/pull/27990)**：修复了 Provider 在流式输出时，将连续的推理过程分割成多个独立块的问题，使其合并显示为一个连贯的推理过程。
4.  **[[OPEN] fix(opencode): consume Model.prefill + runtime-probe llama.cpp templates]](https://github.com/anomalyco/opencode/pull/27916)**：旨在修复末尾为 `role:"assistant"` 的请求导致本地兼容服务器返回 400 错误的问题，对支持本地模型推理至关重要。
5.  **[[OPEN] fix(opencode): filter empty assistant content for @ai-sdk/openai-compatible]](https://github.com/anomalyco/opencode/pull/27914)**: 与#27916 协作，通过过滤空内容的助手消息，解决与思维链模板的兼容性问题。
6.  **[[CLOSED] fix: generate fallback tool call IDs for providers missing id field]](https://github.com/anomalyco/opencode/pull/12585)**：合并的 PR，为 NVIDIA NIM、AWS Bedrock 等缺失流式响应 ID 的 Provider 自动生成回退 ID，提升了跨 Provider 的兼容性。
7.  **[[OPEN] fix(llm): strip dangling XML tool call closing tags from text content]](https://github.com/anomalyco/opencode/pull/27984)**：专门修复 Qwen3 模型通过 vLLM/llama.cpp 使用时，偶尔在文本内容中附加多余 XML tool call 结束标签，导致工具执行失败的问题。
8.  **[[OPEN] fix: make postinstall fallback executable]](https://github.com/anomalyco/opencode/pull/27982)**：修复因缺失 shebang 导致在忽略生命周期脚本的包管理器（如 Bun）上安装失败的问题，保证了安装体验。
9.  **[[OPEN] feat: namespace nested skill names]](https://github.com/anomalyco/opencode/pull/27985)**：支持从目录路径派生命名空间技能名称（如 `team-a:deploy`），解决了技能名冲突问题，是技能系统的重要增强。
10. **[[OPEN] feat(opencode): add per-agent thinking toggle]](https://github.com/anomalyco/opencode/pull/27856)**：支持在 Agent 配置中为每个 Agent 独立开启或关闭模型的思维链功能，提供了更精细的控制粒度。

### 5. 特性请求趋势

1.  **技能系统增强**: 社区强烈希望改进“技能（Skills）”系统。核心需求包括：1) 新增 `/skills` 命令进行快速列表和调用；2) 支持技能的热加载，无需重启；3) 提供更好的命名空间或分组支持，以管理大量技能。
2.  **更高的配置灵活性与扩展性**: 用户希望 OpenCode 能更深入地融入自身的工作流。具体表现为：1) 支持更多数据库系统（如 PostgreSQL）作为会话存储；2) 增加国际化（i18n）支持；3) 提供会话历史搜索工具，实现“即时记忆”功能。
3.  **增强 TUI 可用性**: 持续的 TUI 优化需求包括：1) 设置选项以阻止流式输出时 TUI 自动滚动；2) 支持 `/copy` 命令仅复制最新的 Agent 回复，而非整个会话。

### 6. 开发者痛点

1.  **模型兼容性之痛**: 多起问题报告了与特定模型集成时的问题，例如 Qwen3 导致的进程挂起和错误的工具调用格式，以及 DeepSeek V4 Flash 模型上下文窗口缩水。这表明适配主流模型仍是一个持续的挑战。
2.  **安装与运行环境问题**: 用户在 Windows 上报告了可执行文件损坏的问题，在 Linux 上（`/tmp` 目录 `noexec`）存在静默挂起的问题，以及在 Bun 等非 npm 包管理器上因缺少 `postinstall` 脚本而安装失败。这些环境适配问题对用户上手体验影响巨大。
3.  **会话状态与性能异常**: 持续的“无限压缩循环”和“30GB 内存消耗”问题，以及“InstanceRef not provided”导致的 TUI 挂起，暴露出会话管理模块在处理极端或异常状态时存在严重的健壮性问题。
4.  **Provider API 错误**: 用户在使用 mimo-v2.5 和 ds4-flash 等模型时，即使有有效订阅也遇到 HTTP 402 “余额不足”错误，导致无法使用。这种 Provider 端 API 的错误映射和反馈机制给用户造成了混淆和使用障碍。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-17

## Today’s Highlights
Version **v0.74.1** ships with built-in image generation support and a new Together AI provider, but the community’s attention is on a cascade of provider‑compatibility bugs – particularly around `reasoning_content` in tool calls. A high‑profile issue reveals that Kimi K2.6 and MiMo models break on multi‑turn tool use, while several closed issues (often tagged `closed-because-refactor`) hint at a major internal rewrite in progress. On the PR side, a fix for the streaming decompression bug on Node.js v26 and a proposal to address `--resume` out‑of‑memory crashes were merged.

## Releases
- **[v0.74.1](https://github.com/earendil-works/pi/releases/tag/v0.74.1)**:  
  - Image generation APIs and built‑in OpenRouter image support (inherited from `@earendil-works/pi-ai`).  
  - Together AI as a first‑class provider, with API‑key auth via the `/login` flow.

## Hot Issues (10 selected)

1. **#4251** – `reasoning_content is missing` error when using Kimi K2.6 via OpenCode Go provider.  
   *Community reaction:* 21 comments, 14 👍. The error appears after the first agent message, blocking any chain with reasoning.  
   [GitHub](https://github.com/earendil-works/pi/issues/4251)

2. **#4609** – “Rewrite pi in Rust” (closed).  
   Author `badlogic` opened and closed the same day. While light on discussion (7 comments), the mere existence of this issue signals a potential future direction.  
   [GitHub](https://github.com/earendil-works/pi/issues/4609)

3. **#4587** – Pi attempts global npm installs on Linux instead of within the `~/.pi` folder, causing EACCES errors.  
   *7 comments, open, in progress.* A frequent pain point for Linux users.  
   [GitHub](https://github.com/earendil-works/pi/issues/4587)

4. **#4532** – `parseFrontmatter` rejects valid Claude Code agent files with long unquoted descriptions.  
   *7 comments, closed.* Highlighted a compatibility gap between Pi and a widely used agent format.  
   [GitHub](https://github.com/earendil-works/pi/issues/4532)

5. **#4323** – WezTerm with `enable_kitty_keyboard` breaks the Esc key in Pi (outputs raw escape codes).  
   *7 comments, closed.* Affects a popular terminal, impacting many developers.  
   [GitHub](https://github.com/earendil-works/pi/issues/4323)

6. **#4505** – MiMo models fail with 400 error on second turn because `reasoning_content` is not preserved.  
   *7 comments, 4 👍, open.* Mirrors the Kimi issue – reasoning in tool use is a systemic problem.  
   [GitHub](https://github.com/earendil-works/pi/issues/4505)

7. **#4315** – `package-lock.json` missing resolved/integrity entries since v0.74.0, breaking offline builds (e.g., Nix).  
   *5 comments, 6 👍, closed.* A critical regression for reproducible environments.  
   [GitHub](https://github.com/earendil-works/pi/issues/4315)

8. **#4599** – GitHub Copilot provider cannot discover models not in the build‑time registry.  
   *3 comments, closed.* Users want dynamic model discovery; the static list is insufficient for enterprise variants.  
   [GitHub](https://github.com/earendil-works/pi/issues/4599)

9. **#4605** – RPC mode crashes with `Cannot read properties of undefined (reading 'startsWith')` on OpenRouter API errors.  
   *2 comments, closed quickly.* A raw undefined error that breaks Telegram/web integrations.  
   [GitHub](https://github.com/earendil-works/pi/issues/4605)

10. **#4484** – Compaction bypasses custom `streamFn`, so proxy users get direct calls during context window compression.  
    *2 comments, open.* Undermines the entire proxy configuration for advanced setups.  
    [GitHub](https://github.com/earendil-works/pi/issues/4484)

## Key PR Progress (10 selected)

1. **[#4600](https://github.com/earendil-works/pi/pull/4600)** – Fix: route compaction through `streamFn`. Closes #4484 (proxy bypass). Still open.

2. **[#4606](https://github.com/earendil-works/pi/pull/4606)** – Add null check for `result.error` in `_getRequiredRequestAuth`; fixes RPC mode crash (#4605). Merged.

3. **[#4541](https://github.com/earendil-works/pi/pull/4541)** – Use XML boundaries in system prompt to avoid ambiguity with user `##` headers. Open.

4. **[#4603](https://github.com/earendil-works/pi/pull/4603)** – Update OpenAI Codex model list to match current availability; fixes #4601. Open.

5. **[#4482](https://github.com/earendil-works/pi/pull/4482)** – Address edge‑case with Kitty protocol in WezTerm (double‑escape parsing). Merged.

6. **[#4574](https://github.com/earendil-works/pi/pull/4574)** – Document overflow normalization for custom providers (auto‑compaction guidance). Merged.

7. **[#4558](https://github.com/earendil-works/pi/pull/4558)** – Throw error on missing `finish_reason` in OpenAI completions. Merged.

8. **[#4560](https://github.com/earendil-works/pi/pull/4560)** – Add Fireworks FirePass (subscription) provider for skimi K2p6. Merged.

9. **[#4592](https://github.com/earendil-works/pi/pull/4592)** – Add `--screen-reader` flat mode for accessibility. Merged.

10. **[#4589](https://github.com/earendil-works/pi/pull/4589)** – Fix `--resume` OOM by streaming session metadata line‑by‑line and capping concurrency at 20. Merged.

## Feature Request Trends

- **Dynamic provider model discovery** – Instead of hardcoded model lists, users want providers (GitHub Copilot, Codex, etc.) to query available models at runtime.  
- **Better reasoning / thinking block handling** – Several requests ask for robust handling of `reasoning_content` across providers, especially in tool call sequences.  
- **Customizable system prompt boundaries** – The XML boundary PR (#4541) reflects a desire to prevent agent confusion when user context files contain markdown headers.  
- **Screen reader / accessibility** – Merged #4592 shows demand for non‑visual interaction modes.  
- **Suppress skill warnings** – #4534 asks for an option to silence `[Skill conflicts]` warnings.  
- **Windows‑first improvements** – Requests include forward‑slash reminders in bash tool defaults and fixes for global npm install paths.

## Developer Pain Points

- **Reasoning content fragmentation** – At least three providers (Kimi, MiMo, Anthropic-clone) fail when `reasoning_content` is missing or malformed in tool‑call loops, causing 400 errors and session aborts.  
- **npm/pnpm installation path inconsistencies** – On Linux, Pi tries global install paths (`/usr/lib/node_modules`) instead of the `~/.pi` sandbox, leading to permission errors. On Windows, the fresh install often fails silently.  
- **Memory / performance regressions** – `--resume` with hundreds of session files caused OOM (fix merged), and `package-lock.json` missing integrity entries broke offline builds.  
- **Terminal compatibility** – WezTerm’s Kitty keyboard flag still causes Esc‑key issues; Ghostty’s portrait screenshots overwhelm the transcript.  
- **Proxy & streamFn bypass** – Compaction and certain internal calls ignore user‑supplied `streamFn`, breaking proxy setups.  
- **Repeated global `pnpm install`** – With pnpm 11, Pi re‑installs the same packages on every startup (unresolved).  
- **Race conditions on startup** – Theme not initialized before markdown rendering, clipboard sandbox on macOS aborting interactive mode early.

---

*Digest generated from `github.com/badlogic/pi-mono` (community data under `earendil-works/pi`).*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-05-17

## Today's Highlights
The community remains focused on **memory management and long-session stability**, with multiple OOM-related issues and a new heap-pressure auto-compaction PR merged (#4186). Meanwhile, the **qwen serve daemon (Mode B)** ecosystem continues to expand rapidly, with four new PRs adding session-scoped permissions, daemon-stamped client identity, typed event schemas, and bridge adapters for TUI and IDE. A nightly release failed today (#4221), but the development pace toward v0.16 production readiness remains high.

## Releases
No new releases in the last 24 hours. The latest stable version remains **v0.15.10**.

## Hot Issues (10 selected)

1. **#4149** – *FATAL ERROR: Ineffective mark-compacts near heap limit — JavaScript heap out of memory*  
   [link](https://github.com/QwenLM/qwen-code/issues/4149)  
   A classic OOM crash in long sessions with 8 comments. The GC trace shows memory approaching 4 GB limit. This is the most commented issue today, reflecting a persistent pain point.

2. **#4116** – *problem critical error*  
   [link](https://github.com/QwenLM/qwen-code/issues/4116)  
   General critical error report with 6 comments. Likely related to session management or memory, but the author provided little detail.

3. **#4076** – *工具调用似乎都没有返回实际内容 (Tool calls return no actual content)*  
   [link](https://github.com/QwenLM/qwen-code/issues/4076)  
   A user reports that tool calls (likely via GLM-5.1 on siliconflow) return empty results. 5 comments, suggests interoperability issues with third-party API providers.

4. **#4175** – *proposal(serve): Mode B feature-priority roadmap toward v0.16 production-ready*  
   [link](https://github.com/QwenLM/qwen-code/issues/4175)  
   A detailed roadmap proposal for the daemon mode, covering remaining work beyond Stage 1. Important for developers tracking Mode B progress.

5. **#728** – *FATAL ERROR: Reached heap limit Allocation failed* (P1, open since Sep 2025)  
   [link](https://github.com/QwenLM/qwen-code/issues/728)  
   An ancient OOM issue still seeing comments today (3). Highlights how long memory issues have plagued the project.

6. **#4223** – *mimo-v2.5-pro API Error: 400 Param Incorrect*  
   [link](https://github.com/QwenLM/qwen-code/issues/4223)  
   A model‑switching bug where reasoning_content fields cause 400 errors on second tool call. Similar to DeepSeek V4 issues, indicating fragile API compatibility.

7. **#4185** – *OOM in long sessions: V8 heap pressure can exceed limit before token-based compaction runs*  
   [link](https://github.com/QwenLM/qwen-code/issues/4185)  
   A detailed analysis of the root cause – token‑based compaction triggers too late. This issue directly informed the fix in PR #4186.

8. **#4218** – *[Bug Report] MCP Server "filesystem" shows connected but tools not available*  
   [link](https://github.com/QwenLM/qwen-code/issues/4218)  
   Windows‑specific MCP bug: UI shows connected, but model doesn’t receive tool definitions. 2 comments, impacts Windows users heavily.

9. **#4219** – *@image attachments fail in env-var-only mode — modalities never auto-detected*  
   [link](https://github.com/QwenLM/qwen-code/issues/4219)  
   When using only env vars (no settings.json), image attachments are silently replaced with a placeholder. Important for headless/CI setups.

10. **#4228** – *Roadmap: harden /goal into a reliable long-horizon workflow primitive*  
    [link](https://github.com/QwenLM/qwen-code/issues/4228)  
    A new feature request to make `/goal` more robust, building on previous discussions. Shows growing interest in goal‑driven automation.

## Key PR Progress (10 selected)

1. **#4186** *(CLOSED)* – *fix(core): add heap-pressure auto-compaction safety net*  
   [link](https://github.com/QwenLM/qwen-code/pull/4186)  
   Merged today. Adds a 70% heap‑used threshold that triggers auto‑compaction even if token count is low. Critical for long‑session stability.

2. **#4232** *(OPEN)* – *feat(serve): add session-scoped permission route*  
   [link](https://github.com/QwenLM/qwen-code/pull/4232)  
   Adds a new `POST /session/:id/permission/:requestId` endpoint for daemon mode, plus legacy fallback. A key piece of Mode B.

3. **#4231** *(CLOSED)* – *feat(serve): add daemon-stamped client identity*  
   [link](https://github.com/QwenLM/qwen-code/pull/4231)  
   Introduces `X-Qwen-Client-Id` to track daemon client sessions. Merged today.

4. **#4226** *(OPEN)* – *feat(protocol): typed daemon event schema v1 (#4175 Wave 1 PR 4)*  
   [link](https://github.com/QwenLM/qwen-code/pull/4226)  
   Adds a discriminated union `TypedDaemonEvent` and a pure reducer skeleton. Zero runtime cost, improves SDK type safety.

5. **#4230** *(OPEN)* – *feat(core): fail impossible goals*  
   [link](https://github.com/QwenLM/qwen-code/pull/4230)  
   Adds an impossible‑judge outcome for `/goal`, terminating endless loops. Improves user experience for long‑running goals.

6. **#4233** *(OPEN)* – *fix(cli): restore ACP prompt counter on resume*  
   [link](https://github.com/QwenLM/qwen-code/pull/4233)  
   Fixes a bug where ACP session resume left the turn counter at zero, causing duplicate prompt IDs.

7. **#4224** *(CLOSED)* – *fix(cli): include skill base dir in slash commands*  
   [link](https://github.com/QwenLM/qwen-code/pull/4224)  
   Ensures skills that reference relative files (e.g., `qc-helper`) work correctly. Merged today.

8. **#4213** *(OPEN)* – *fix(core): apply tool name migrations at dispatch*  
   [link](https://github.com/QwenLM/qwen-code/pull/4213)  
   Canonicalizes legacy tool names (`task` → `agent`, `replace` → `edit`) before dispatch. Prevents tool‑call failures after name changes.

9. **#4203** *(OPEN)* – *feat(channel): add daemon bridge spike*  
   [link](https://github.com/QwenLM/qwen-code/pull/4203)  
   Adds a `DaemonChannelBridge` for server‑side channel bots to consume daemon SSE events. Part of the broader Mode B integration.

10. **#4127** *(OPEN)* – *fix(core): memory-based chat compression to prevent heap OOM*  
    [link](https://github.com/QwenLM/qwen-code/pull/4127)  
    Replaces entry‑count caps with memory‑based compaction. Long‑running sessions (80+ min) are the target. Complements #4186.

## Feature Request Trends
- **Memory diagnostics and self‑healing**: Several requests for `/doctor memory` (#4179), heap‑pressure auto‑compaction (#4186, #4185), and structured diagnostics JSON (#3785) reflect a strong desire for proactive memory management.
- **Daemon mode (Mode B) production readiness**: The flurry of PRs (permission routes, client identity, typed events, bridges) indicates the community is pushing `qwen serve` toward v0.16.
- **Session lifecycle improvements**: Forking sessions (#4158), custom export directories (#4192), and ACP SDK upgrades for `resumeSession`/`forkSession` (#4227) show a need for better session management.
- **Goal‑driven workflows**: The roadmap for `/goal` (#4228, #4230) is gaining traction as users want reliable long‑horizon automation.
- **Tool call and MCP robustness**: Multiple issues (#4076, #4223, #4218) point to fragile tool‑call, model‑switching, and MCP server integration, driving requests for better error handling and API compatibility.

## Developer Pain Points
1. **Heap OOM crashes in long sessions** – The most frequent and critical issue. Multiple reports (#4149, #728, #4185, #2945, #2868) and a dedicated performance label. The root cause (token‑based compaction lag) was only partially addressed by #4186; a permanent fix may require deeper architectural changes.
2. **Tool call and MCP failures** – Silent failures, 400 errors on reasoning content, and MCP tools not reaching the model are common. Especially painful for third‑party API providers and Windows users.
3. **Keyboard shortcut limitations** – Lack of Emacs/readline shortcuts on macOS (#3821) frustrates developers accustomed to conventional CLI tools.
4. **Missing recovery mechanisms** – Users report that `/rename --auto` fails when models return plain JSON (#4057), and image attachments break in env‑var‑only mode (#4219). These edge cases reduce the tool’s reliability in automated workflows.
5. **Nightly release failures** – The failed release (#4221) is a minor but visible hiccup that can delay access to nightly fixes.

*For the full list of issues and PRs, visit [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code).*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*