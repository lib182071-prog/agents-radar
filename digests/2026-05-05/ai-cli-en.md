# AI CLI Tools Community Digest 2026-05-05

> Generated: 2026-05-05 07:32 UTC | Tools covered: 8

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
**Date**: May 5, 2026

---

## 1. Ecosystem Overview

The AI CLI tools landscape continues to mature rapidly, with eight major tools showing distinct maturation patterns. **Claude Code, OpenAI Codex, OpenCode, and Qwen Code** lead in community engagement and iteration velocity, while **Pi** and **Gemini CLI** focus on architecture refactoring and local-first approaches. **GitHub Copilot CLI** remains stable but sees growing frustration around silent resource consumption, and **Kimi Code CLI** shows minimal activity, indicating a smaller or less vocal user base. Across all tools, three dominant themes emerge: **token efficiency and cost transparency**, **local/self-hosted LLM integration**, and **agent reliability improvements**—each reflecting users’ desire for predictable, controllable, and cost-effective AI-assisted development.

---

## 2. Activity Comparison

| Tool | Hot Issues (Tracked) | PRs Updated (24h) | Release Status | Notable Release |
|------|---------------------|-------------------|----------------|-----------------|
| **Claude Code** | 10 of ~50 tracked | 3 OPEN | ✅ v2.1.128 | Random session colors, `.zip` plugin support |
| **OpenAI Codex** | 10 of ~30 trending | 10 OPEN | ✅ 3 alpha releases (rust-v0.129.0-a.4–.6) | Service tier refactoring, `--attachment` flag |
| **Gemini CLI** | 10 noteworthy | 10 OPEN / CLOSED | ✅ v0.42.0-nightly | ACP client refactor, doc workflow updates |
| **GitHub Copilot CLI** | 10 | 0 | ✅ v1.0.41-0 | `--attachment` flag, file-edit reliability |
| **Kimi Code CLI** | 4 | 0 | ❌ No new release | – |
| **OpenCode** | 10 | 10 (5 MERGED) | ✅ v1.14.37, 35, 34 | Child task cancellation, session warping |
| **Pi** | 10 | 10 (8 CLOSED) | ✅ v0.73.0 | Xiaomi billing, local-LLM provider extensions (#4154) |
| **Qwen Code** | 10 | 10 | ✅ v0.15.6-nightly | FileReadCache, proxy fix, WebSearch tool PR |

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities:

### 🔍 Token Efficiency & Cost Transparency
- **Claude Code**: Excessive token burn during failures (#56075, #56206) – users paying for useless output.
- **OpenAI Codex**: RTK filtering of shell output (#19001) for 60–90% token reduction.
- **GitHub Copilot CLI**: HTTP/2 GOAWAY race wastes premium requests (#2421); infinite request loops (#2591).
- **Qwen Code**: Session file bloat causing slow `/resume` (#3822); auto-memory latency (#3814 fix).
- **Common pattern**: Users demand **visible usage indicators** (GitHub Copilot #2052: “context used” bar) and **rollback/no-cost failure recovery**.

### 💾 Persistent Settings & Cross-Session Memory
- **Claude Code**: `/effort` leaks across sessions (#53416); persistent settings request (#41548).
- **Kimi Code CLI**: Community plugin `kimi-mneme` for cross-session context retention.
- **OpenCode**: Session lifecycle management (archive, batch delete, factory reset).
- **Pi**: Per-model configuration (thinking levels, provider tuning).
- **Common driver**: Users want to **preserve context and preferences** across restarts without manual re-entry.

### 🔌 Plugin/MCP Ecosystem Maturation
- **Claude Code**: `.zip` plugin support, `/mcp` tool counts, server discovery.
- **GitHub Copilot CLI**: Per-repo MCP config (#2528); `.vscode/mcp.json` removed (#3019 regression).
- **Gemini CLI**: Auto-discover `.mcp.json` from project root (#26490).
- **OpenCode**: OMO plugin compatibility breaks (#25799); `AGENTS.md` loading (#12096 merged).
- **Common theme**: Users want **repository-scoped, shareable** MCP configurations and **plugin isolation** to avoid breaking on updates.

### 🔑 Multi-Account & Authentication Flexibility
- **Claude Code**: Multi-account profile management (#27359).
- **OpenCode**: Multi-account OAuth with auto-relogin (#11830).
- **GitHub Copilot CLI**: Scoped permission requests per repo (#953); enterprise model access control (#3101).
- **Common driver**: Growing **enterprise adoption** requires per-project accounts, credential rotation, and granular authorization.

### 🤖 Agent Reliability & Recovery
- **Gemini CLI**: Subagent false success on MAX_TURNS (#22323); crash on `get-shit-done` (#22186).
- **Claude Code**: Infinite thinking loops; skills ignored (#56228).
- **GitHub Copilot CLI**: Retry loops during peak hours (#3117); silent premium waste.
- **OpenCode**: Retry state lock prevents context cleanup (#25803).
- **Common need**: Users want **predictable, interruptible agents** with fallback mechanisms and **transparent progress monitoring**.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code CLI | OpenCode | Pi | Qwen Code |
|-----------|-------------|--------------|------------|-------------------|---------------|----------|----|-----------|
| **Primary Focus** | Agent skills & MCP ecosystem | Model selection & sandbox security | Enterprise policies & multi-agent | GitHub integration & plugin systems | Minimal (community-driven) | Multi-platform UI & plugin extensibility | Local LLM + multi-provider billing | Background tasks & auto-memory |
| **Target Users** | Heavy users, plugin enthusiasts | Power users, multi-model devs | Enterprise teams, security-conscious | GitHub ecosystem developers | Niche / early adopters | Desktop & web hybrid users | OSS contributors, self-hosters | Chinese market, Qwen ecosystem |
| **Technical Approach** | React-based TUI, server-side agent loop | Rust CLI, desktop app, API-first | ACP client refactor, AST-aware agents | Node.js CLI, GitHub auth, MCP | Basic Node.js | TypeScript/React, plugin system (OMO) | TypeScript/Node, extensions, JSON-driven | Python/Node, auto-memory, nightly releases |
| **Key Differentiator** | Deep MCP integration, `/color`, `/effort` | `/undo` (community demand), GPT-5.5 context | `allowEnv`, browser agent, eval framework | Premium requests, copilot feedback cmd | Persistent memory plugin (community) | Session warping, mobile touch, OMO plugins | Local LLM provider extensions, Xiaomi billing | WebSearch tool, auto-memory “dreaming” |
| **Release Cadence** | Frequent patches (v2.1.x) | Multiple alphas per week | Nightly builds | Stable with minor patches | Very slow | Multiple patch releases per day | Weekly+ | Nightly builds |
| **Pain Point Profile** | Token consumption, regression churn | Auth loops, sandbox friction | Crashes & hangs, permission prompts | Silent premium waste, model instability | Crashes on Win/WSL, login fail | Windows regressions, plugin breakage | Silent failures, OAuth fragility | UI rendering issues, session bloat |

---

## 5. Community Momentum & Maturity

### 🟢 High Momentum (rapid iteration, strong engagement)
- **OpenCode**: 3 patch releases in 24h, 10 active PRs (5 merged), 47-comment issue on Kimi tool-calling. High plugin ecosystem activity.
- **Qwen Code**: Nightly builds, 10 PRs (including major features like WebSearch and auto-memory fixes), responsive to community bug reports.
- **Claude Code**: Despite token-consumption frustration, community is highly vocal (38 comments on #23377, 31👍). Release cadence steady.
- **OpenAI Codex**: 10 PRs in 24h, 121 comments on 1M context issue (#19464). Strong demand for `/undo` (193👍) shows passionate user base.

### 🟡 Moderate Momentum (stable but slower)
- **Gemini CLI**: Nightly releases but fewer community comments per issue. Focus on internal refactors (ACP client) and enterprise features.
- **Pi**: 10 PRs (8 closed), but many bugs closed due to “bigrefactor” – indicates internal churn. Local LLM PR (#4154) is a major win.
- **GitHub Copilot CLI**: Only 0 PRs in 24h. Issues show frustration but no rapid fixes. MCP and plugin complaints suggest ecosystem gaps.

### 🟢 Low Activity / Niche
- **Kimi Code CLI**: Only 4 issues, 0 PRs, no release. Community is tiny or inactive. Plugin showcase (#2161) is the only bright spot.

### Maturity Indicators
- **Most mature**: Claude Code (largest issue tracker, structured releases), OpenAI Codex (extensive PR pipeline, sandbox architecture).
- **Fastest iteration**: OpenCode (multi-patch days, responsive to regressions like #25799).
- **Best community responsiveness**: Qwen Code (same-day PRs for filed bugs like #3839→#3840).

---

## 6. Trend Signals

### ⚡ 1. Token Cost Becomes a First-Class Product Concern
Every major tool faces backlash over invisible token consumption. **Expect built-in usage dashboards, per-request cost breakdowns, and configurable caps** to become table stakes. Tools that fail to provide transparency (like GitHub Copilot’s GOAWAY waste) will lose trust.

### 🔧 2. Local & Self-Hosted LLM Integration Accelerates
Pi’s local-LLM PR (#4154) and OpenCode’s OS model tool-calling issues (#234) signal growing demand for **privacy and cost control** via local inference. Qwen Code’s WebSearch tool with 7-layer injection defense shows how tools differentiate by proximity to their model ecosystem.

### 🌐 3. MCP Standardization Pressure Grows
All major tools now support MCP, but fragmentation exists: per-repo vs. global config, `.mcp.json` vs. `.vscode/mcp.json`. The community clearly wants **repository-scoped, version-controlled MCP files** (Gemini CLI #26490, GitHub Copilot #2528). Expect a de facto standard to emerge.

### 🧠 4. Agent Memory Moves from Nice-to-Have to Necessity
Cross-session memory (Kimi’s plugin, Claude’s persistent settings, OpenCode’s session lifecycle) is no longer optional. **Agent “blank slate” resets are unacceptable** for daily use. Tools that natively offer compressed, task-specific memory will win.

### 🏢 5. Enterprise Readiness Becomes a Battleground
Multi-account support, scoped permissions, audit trails, and compliance (e.g., AI contribution attribution) are appearing across Claude Code, Gemini CLI, and OpenCode. **The enterprise developer is the key growth segment**, and CLI tools must integrate with existing identity and security stack.

### 🐛 6. Cross-Platform Pain Is Persistent and Unresolved
Windows-specific regressions (Claude Code segfault #51464, OpenCode startup freeze #24418, Pi TLS warnings #4157) show that **cross-platform stability is still a major gap**. Wayland, non-AVX CPUs, and ARM Linux issues compound. Expect tools to invest in CI matrix testing or risk losing platform share.

### 📊 7. Community-Driven Undo/Rollback Becomes a Litmus Test
OpenAI Codex’s #9203 (193👍 for `/undo`) and Copilot CLI’s file-edit reliability fixes indicate users want **reversible agent actions**. Tools that lack recovery mechanisms will face higher churn when agents make costly mistakes.

---

**Bottom line for decision-makers**: If you prioritize ecosystem breadth and MCP plugin support, **Claude Code** and **OpenCode** lead. For enterprise security and policy control, **Gemini CLI** is strongest. Self-hosters should watch **Pi** and **OpenCode** for local LLM support. If token cost is your chief concern, no tool has solved it yet—but **OpenAI Codex**’s RTK filtering proposal and **Qwen Code**’s caching optimizations point in the right direction.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
*Data as of 2026-05-05 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking (by Discussion Activity)  

Below are the most-discussed Pull Requests (sorted by comment count), each representing a Skill proposal or improvement actively debated by the community.

| # | Skill PR | Description | Key Discussion Points | Status |
|---|----------|-------------|-----------------------|--------|
| 1 | [#514 – Add document-typography skill](https://github.com/anthropics/skills/pull/514) | Prevents orphan words, widow paragraphs, and numbering misalignment in AI-generated documents. | Community recognized this as a universal pain point. Discussion centered on scope — should it be a standalone skill or part of a larger document quality suite? High enthusiasm for immediate value. | Open |
| 2 | [#210 – Improve frontend-design skill clarity](https://github.com/anthropics/skills/pull/210) | Revises the existing frontend-design skill for better actionability and coherence within a single conversation. | Focused on making instructions more executable. Debate about whether changes break backward compatibility for existing users. | Open |
| 3 | [#83 – Add skill-quality-analyzer & skill-security-analyzer](https://github.com/anthropics/skills/pull/83) | Meta-skills that evaluate other skills across structure, documentation, and security dimensions. | Mixed reactions: some praised systematic QA, others worried about over-engineering. Security analyzer raised concerns about false positives. | Open |
| 4 | [#486 – Add ODT skill](https://github.com/anthropics/skills/pull/486) | OpenDocument creation, template filling, and ODT→HTML conversion. | Compatibility with LibreOffice workflows was heavily discussed. Requests for ODS (spreadsheet) support as well. | Open |
| 5 | [#538 – Fix case-sensitive file references in PDF skill](https://github.com/anthropics/skills/pull/538) | Fixes 8 case-mismatch issues in `skills/pdf/SKILL.md` that break on case-sensitive filesystems. | Though small, it sparked broader conversation about cross-platform testing and Linux adoption of Claude Code. | Open |
| 6 | [#539 – Fix skill-creator: warn on unquoted YAML special characters](https://github.com/anthropics/skills/pull/539) | Prevents silent YAML parsing failures in description fields containing colons. | Technical but critical for new contributors. Discussion led to a proposal for a full YAML linter for Skills. | Open |
| 7 | [#541 – Fix docx: prevent tracked change w:id collision](https://github.com/anthropics/skills/pull/541) | Fixes document corruption when tracked changes conflict with existing bookmarks in OOXML. | Deep OOXML internals debate. Appreciated by advanced DOCX users; considered a model example of edge-case handling. | Open |
| 8 | [#509 – docs: add CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509) | Community health gap fix; adds contribution guidelines to address low GitHub community score. | Unanimously positive. Discussion focused on how to make the file beginner-friendly while setting quality bars. | Open |

---

## 2. Community Demand Trends (from Issues)  

Analysis of the most-commented Issues reveals clear directional signals for what the community wants next.

| Trend | Evidence (Issue #) | Key Demand |
|-------|--------------------|------------|
| **Skill persistence & reliability** | [#62 (10 comments)](https://github.com/anthropics/skills/issues/62) – "All my skills have disappeared"<br>[#406 (2 comments)](https://github.com/anthropics/skills/issues/406) – "Unable to upload or replace skills"<br>[#403 (2 comments)](https://github.com/anthropics/skills/issues/403) – "Unable to delete skill versions" | Users are frustrated by skills vanishing, upload failures, and API errors. Demand for robust storage and lifecycle management. |
| **Org-wide skill sharing** | [#228 (9 comments)](https://github.com/anthropics/skills/issues/228) – "Enable org-wide skill sharing" | Enterprise users want direct sharing links or a skill library instead of manual .skill file distribution. |
| **Skill-creator best practices** | [#202 (8 comments)](https://github.com/anthropics/skills/issues/202) – "skill-creator should be updated to best practice" | The official skill-creator is too verbose and human-focused. Community wants a lean, Claude-actionable version. |
| **Evaluation & testing infrastructure** | [#556 (6 comments)](https://github.com/anthropics/skills/issues/556) – "run_eval.py never triggers skills/commands" | The evaluation script for testing Skill triggers is broken (0% trigger rate). Demand for a reliable way to test if skills are being invoked. |
| **Duplicate & namespace trust issues** | [#189 (5 comments)](https://github.com/anthropics/skills/issues/189) – "document-skills and example-skills install identical content"<br>[#492 (4 comments)](https://github.com/anthropics/skills/issues/492) – "Community skills under anthropic/ namespace enable trust abuse" | Community wants curated, unique skill sets and clearer branding to avoid trust confusion. |

**Secondary signals** (3–4 comments):  
- [#412](https://github.com/anthropics/skills/issues/412) – Agent governance / safety patterns.  
- [#532](https://github.com/anthropics/skills/issues/532) – skill-creator requires ANTHROPIC_API_KEY, blocking enterprise/SSO users.  
- [#184](https://github.com/anthropics/skills/issues/184) – agentskills.io site broken (too many redirects).  

---

## 3. High-Potential Pending Skills  

The following PRs are not yet merged but are actively discussed and close to landing. They represent skills likely to ship in the near term.

| PR | Skill | Why It Matters | Status |
|----|-------|----------------|--------|
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** – Full testing stack (unit, React, integration, E2E) | Comprehensive, aligns with modern test trophy model. High community need. | Open |
| [#568](https://github.com/anthropics/skills/pull/568) | **servicenow** – Broad ServiceNow platform skill (ITSM, SecOps, ITAM, etc.) | Addresses large enterprise demand. Covers 10+ modules. | Open |
| [#806](https://github.com/anthropics/skills/pull/806) | **sensory** – macOS automation via AppleScript | First native macOS automation skill. Tiered permission system well-received. | Open |
| [#360](https://github.com/anthropics/skills/pull/360) | **appdeploy** – Deploy full-stack web apps from Claude | End-to-end deployment is a top request. Uses AppDeploy service. | Open |
| [#147](https://github.com/anthropics/skills/pull/147) | **codebase-inventory-audit** – Orphaned code, docs gaps, infrastructure bloat | Systematic codebase health check – 10-step workflow. | Open |
| [#335](https://github.com/anthropics/skills/pull/335) | **masonry** – AI image & video generation (Imagen, Veo) | Media generation is a rapidly growing use case. | Open |
| [#299](https://github.com/anthropics/skills/pull/299) | **Google Workspace suite** – Email triage, draft, calendar, etc. (via GOG CLI) | Personal assistant use case; 6 sub-skills. High utility. | Open |
| [#664](https://github.com/anthropics/skills/pull/664) | **claude-obsidian-reporter** – Auto daily Git reports in Obsidian | Developer productivity + Obsidian ecosystem integration. | Open |

---

## 4. Skills Ecosystem Insight  

**The community's most concentrated demand is for skills that make Claude a reliable, shareable, and auditable enterprise tool** — with top priorities being skill lifecycle stability (no disappearing data, no broken evaluation), production-grade testing/document quality, and seamless sharing across teams. The surge in infrastructure skills (ServiceNow, AppDeploy, macOS automation) signals a shift from experimental coding companions toward trusted enterprise automation platforms.

---

# Claude Code Community Digest — 2026-05-05

## Today's Highlights

A quiet release day with **v2.1.128** shipping a handful of quality-of-life improvements, including random session colors and `.zip` plugin support. The community is voicing growing frustration over **excessive token consumption** (#56206, #56075) and **billing/usage-limit issues** (#29223), while the long-running #23377 (prompt length overflow) continues to dominate discussion with 38 comments. Three new PRs are open, including a sensible client-side session persistence stopgap (#55864).

---

## Releases

**v2.1.128** — released within the last 24h

Changes:
- Bare `/color` (no args) picks a random session color
- `/mcp` now displays tool counts for connected servers and flags servers that connected with zero tools
- `--plugin-dir` now accepts `.zip` plugin archives in addition to directories
- `--channels` flag now works with console API output

---

## Hot Issues (10 selected from 50)

1. **#23377 — [BUG] GitHub Issue Prompt Too Long**  
   [Link](https://github.com/anthropics/claude-code/issues/23377)  
   *Comments: 38 | 👍: 31*  
   The most-discussed issue today. Users report that Claude Code's prompt becomes excessively long when processing GitHub issues, likely overflowing context windows. Despite being filed three months ago, it remains open — suggesting a non-trivial root cause. High engagement indicates this affects many workflows.

2. **#29223 — [BUG] Plan upgraded but limit is not reset in sessions**  
   [Link](https://github.com/anthropics/claude-code/issues/29223)  
   *Comments: 17 | 👍: 24*  
   A long-standing billing bug: upgrading a plan does not refresh usage limits in the current session. Users must restart to see the new limit. High upvote count suggests this is a frequent pain point for paying customers.

3. **#29247 — [BUG] Cowork: VirtioFS mount fails for macOS username "shared"**  
   [Link](https://github.com/anthropics/claude-code/issues/29247)  
   *Comments: 9*  
   Path collision with `/Users/Shared/` breaks Cowork workspace mounting. Niche but reproducible — a classic edge case that's been open since February.

4. **#37065 — [BUG] SIGILL crash on Intel Westmere — native binary requires AVX2**  
   [Link](https://github.com/anthropics/claude-code/issues/37065)  
   *Comments: 7*  
   Older Intel CPUs (Xeon X5675) crash with an illegal instruction signal because the binary was compiled with AVX2. Marked as duplicate, but the fact it's still open suggests the build pipeline hasn't been fixed.

5. **#53416 — [BUG] /effort setting is global across sessions instead of per-session**  
   [Link](https://github.com/anthropics/claude-code/issues/53416)  
   *Comments: 6 | 👍: 4*  
   Changing effort level in one session immediately propagates to all other open sessions. A scoping issue that undermines concurrent multi-project workflows.

6. **#55404 — [BUG] Cowork desktop app — bash workspace fails to start repeatedly**  
   [Link](https://github.com/anthropics/claude-code/issues/55404)  
   *Comments: 5 | 👍: 1*  
   Persistent workspace startup failure on Windows for Cowork desktop. Filed 4 days ago and already accumulating traction.

7. **#56075 — [BUG] Single README.md edit burns entire 5-hour Max 5x window in 9m 39s**  
   [Link](https://github.com/anthropics/claude-code/issues/56075)  
   *Comments: 5 | 👍: 2*  
   A shocking usage report: a trivial edit consumed an entire 5-hour session window in under 10 minutes. Likely an infinite thinking loop or runaway context. On Opus 4.7 1M, resumed session, JetBrains, Windows.

8. **#51464 — [BUG] Segmentation fault at address**  
   [Link](https://github.com/anthropics/claude-code/issues/51464)  
   *Comments: 4*  
   Windows segfault with a reproduction case available. Marked as regression. No resolution after two weeks.

9. **#37277 — [BUG] ccd-cli v2.1.78 crashes with `invalid opcode` on non-AVX CPUs**  
   [Link](https://github.com/anthropics/claude-code/issues/37277)  
   *Comments: 4*  
   A regression of a previously fixed issue (#19907). Non-AVX CPUs (common in cloud VMs and older hardware) get `invalid opcode` crashes. Duplicate of #37065 but independently filed on Linux.

10. **#56228 — [BUG] Claude Code ignores review skill during execution**  
    [Link](https://github.com/anthropics/claude-code/issues/56228)  
    *Comments: 2*  
    A visibly frustrated user reports that a previously working review skill is now ignored by the model. The emotional tone suggests this is not an isolated incident — skills ignoring configurations is a recurring theme.

---

## Key PR Progress

Only **3 PRs** were updated in the last 24 hours. All remain open:

1. **#56179 — Remove 'statsig.anthropic.com' from firewall script**  
   [Link](https://github.com/anthropics/claude-code/pull/56179)  
   Author: nafu  
   A maintenance PR. The domain `statsig.anthropic.com` now returns NXDOMAIN, so the firewall allowance is dead code. Cleanup.

2. **#56176 — Claude/book outline bootstrap toolkit**  
   [Link](https://github.com/anthropics/claude-code/pull/56176)  
   Author: LOUSTA79  
   Title appears incomplete or garbled. No description. Likely a test or accidental submission — low signal.

3. **#55864 — feat: add session-persist plugin for client-side session state preservation**  
   [Link](https://github.com/anthropics/claude-code/pull/55864)  
   Author: SanskaarUndale21  
   A client-side stopgap for issue #55860: preserves working context across window closures by saving session state locally. A pragmatic solution while the server-side fix (agent loop independent of window) is built. Worth watching.

---

## Feature Request Trends

The following directions recur across multiple issues and enhancement requests:

- **Multi-account profile management** (#27359, 31 👍): Users want named profiles to switch between personal/work Anthropic accounts without re-authenticating.
- **Persistent user settings** (#41548, 9 👍; #53416): Settings like "always show thinking trace" and effort level should persist across sessions, not reset on restart.
- **Visibility into background tasks and wakeups** (#47518): Users want to see scheduled monitoring tasks and pending wakeups in the TUI.
- **Chat platform-specific message formatting** (#56230): Request for auto-formatting output for Teams/Slack/Discord paste targets.
- **Auto-run missed scheduled tasks on startup** (#54555): Routine tasks skipped while the app was closed should execute on next launch.
- **Subcommand whitelisting** (#56233): Granular permission control for bash commands, not just blanket allow/deny.
- **Thinking trace always on** (#41548): Persistent toggle (not per-session) for showing reasoning traces.

---

## Developer Pain Points

The community's most acute frustrations cluster around **cost and consumption**:

- **Excessive token burn during failures** (#56075, #56206, #56139, #56231): Users report entire session limits consumed by infinite thinking loops, timed-out requests that still deduct tokens, and rate-limit errors that burn quota. The lack of partial refunds or rollbacks amplifies the pain.
- **Billing/plan inconsistencies** (#29223): Upgrading plans doesn't reset session limits, forcing app restarts.
- **Platform-specific breakage**: Windows symlinks creating duplicate projects (#56173), macOS username collisions (#29247), and non-AVX CPU crashes (#37065, #37277) show fragmentation across platforms.
- **Regression churn**: Issues like #37277 and #51464 are labeled as regressions of previously fixed bugs, eroding confidence in the release process.
- **Cross-session state leakage** (#53416): `/effort` setting bleeds across sessions, breaking isolation.
- **Skills and configurations silently ignored** (#56228, #56224): The model does not reliably honor user-defined skills, settings, or token environment variables, leading to wasted effort and context.

A recurring theme: **users feel they are paying for tokens that produce no useful output**, whether from loops, crashes, or ignored configurations. The community response is increasingly vocal about this.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-05

## Today’s Highlights
Three new Rust CLI alpha releases landed (v0.129.0-alpha.4 through .6), while the community continues to rally around long-standing requests like returning the `/undo` command and expanding the GPT-5.5 context window to 1M tokens. A series of internal PRs refactoring service tiers and tool definitions signals upcoming improvements to model selection and MCP compatibility.

## Releases
- **`rust-v0.129.0-alpha.4`**, **`alpha.5`**, and **`alpha.6`** — No changelog details were provided beyond the version bump. These likely contain incremental fixes and experimental features for the Rust-based CLI.

## Hot Issues (10 of 30 trending)

1. **[#19464 – Support 1M token context for GPT-5.5 in Codex](https://github.com/openai/codex/issues/19464)** (121 comments, 154 👍)  
   Users are pushing for the GPT-5.5 context window to match the API’s 1M tokens, not the current 400K documented limit. High engagement suggests this is a top priority for power users.

2. **[#20161 – Phone number verification doesn’t work](https://github.com/openai/codex/issues/20161)** (65 comments, 56 👍)  
   SSO login triggers a phone verification loop on a second device. The issue has been open over a week without a fix, causing frustration for multi-device workflows.

3. **[#9203 – Please make `/undo` back](https://github.com/openai/codex/issues/9203)** (37 comments, 193 👍)  
   The most-liked request on the board. Users miss the ability to revert unintended file changes or deletions, especially when git isn’t tracking all files.

4. **[#2137 – Pasting multi-line text only keeps first line on Windows](https://github.com/openai/codex/issues/2137)** (33 comments, 41 👍)  
   Closed but still updated. A long-standing Windows terminal bug that auto-submits after the first line, breaking multi-line paste. Still affects users.

5. **[#16857 – High GPU usage while “thinking” due to tiny animation](https://github.com/openai/codex/issues/16857)** (20 comments, 24 👍)  
   A seemingly minor animation causes significant GPU drain on macOS during model inference. Users report battery drain and fan noise.

6. **[#9926 – Interactive `ask_user_question` tool (tabbed questionnaire UI)](https://github.com/openai/codex/issues/9926)** (14 comments, 21 👍)  
   A structured Q&A tool to replace free-form back-and-forth. Community sees this as a way to reduce ambiguity and speed up agent interactions.

7. **[#18693 – Desktop performance collapses with very large local conversation histories](https://github.com/openai/codex/issues/18693)** (13 comments, 4 👍)  
   Typing, scrolling, and thread-list navigation become unusable when a few conversations grow very large. The issue links to several related performance regressions.

8. **[#15057 – Linux sandbox fails with AppArmor userns restrictions](https://github.com/openai/codex/issues/15057)** (12 comments, 4 👍)  
   `bwrap` loopback fails on Ubuntu when unprivileged user namespace restrictions are enabled. Closed but the workaround is unclear for many.

9. **[#19196 – ‘Full Access’ permissions still sandboxed](https://github.com/openai/codex/issues/19196)** (11 comments, 21 👍)  
   Setting sandbox to “Full Access” still blocks network calls. Users expect a true no-sandbox mode for debugging and development.

10. **[#16688 – TUI freeze during agent fan-out](https://github.com/openai/codex/issues/16688)** (11 comments, 1 👍)  
    The terminal UI becomes unresponsive when spawning multiple subagents. Impacts productivity on complex tasks.

## Key PR Progress (10 of 20 trending)

1. **[#21043 – Document Windows metadata request boundary](https://github.com/openai/codex/pull/21043)**  
   Adds documentation for the setup request boundary objects, aiding future reviewers of the Windows adapter layer.

2. **[#20969 → #20974 → #20971 → #20978 – Service tier ID migration series](https://github.com/openai/codex/pull/20969)**  
   A four-PR stack adding model service tier metadata, moving from closed enums to string IDs, and introducing dynamic slash commands like `/fast`. This will make tier selection more flexible and visible.

3. **[#18424 – Enable await-holding Clippy lints](https://github.com/openai/codex/pull/18424)**  
   The final step in a lint-enforcement chain to prevent holding locks across `.await`. Improves code safety across the Rust codebase.

4. **[#18809 – Cross-compile hacks for bwrap](https://github.com/openai/codex/pull/18809)**  
   Fixes `bazel` build for Linux musl targets from macOS. Essential for CI reproducibility.

5. **[#17273 – Use scoped remote control server tokens](https://github.com/openai/codex/pull/17273)**  
   App-server now consumes short-lived, scoped tokens for remote control, improving security during enrollment.

6. **[#18001 – Tighten shell wrapper detection](https://github.com/openai/codex/pull/18001)**  
   Stops over-matching unknown shell paths in approval prompts, reducing false positives for custom launchers.

7. **[#18736 – Add context length regression review](https://github.com/openai/codex/pull/18736)**  
   Introduces a PR health check that measures prompt size for common `codex exec` scenarios, aiming to catch accidental context growth early.

8. **[#18376 – Clarify Windows image paste shortcut](https://github.com/openai/codex/pull/18376)**  
   Updates TUI guidance: Windows users are now told to use Ctrl+Shift+V (or similar) since Ctrl+V is often intercepted by terminals.

9. **[#18399 – Add app-server ThreadStore adapter](https://github.com/openai/codex/pull/18399)**  
   Moves thread metadata writes behind a `ThreadStore` abstraction, enabling cleaner separation between CLI and app-server storage.

10. **[#20658 – Enforce add-dir for macOS sandbox](https://github.com/openai/codex/pull/20658)**  
    Fixes a migration path where `--add-dir` was ignored in workspace-write sandbox mode, breaking exec workflows on macOS.

## Feature Request Trends
- **Larger context windows** – #19464 (1M tokens for GPT-5.5) is the most active request; users expect parity with the API.
- **Undo / recovery** – #9203 (bring back `/undo`) and related requests show strong desire for rollback capabilities.
- **Structured user interaction** – #9926 (tabbed Q&A tool) and #8673 (Shift+Enter newline) reflect demand for more keyboard-friendly and guided input.
- **Token efficiency** – #19001 (RTK filtering of shell output) proposes 60–90% token reduction; this aligns with rising context costs.
- **Plugin & marketplace scoping** – #18115 asks for repository-scoped plugins and local marketplaces, a sign of growing enterprise adoption.

## Developer Pain Points
- **Authentication hiccups** – #20161 (phone verification loop) and #18653 (CLI misidentifying Plus as Free) erode trust in the login flow.
- **Sandbox friction** – #15057 (AppArmor), #19196 (Full Access still sandboxed), and #19349 (Full Access broken) indicate the sandbox is not yet reliable for all setups.
- **Performance regressions** – #16857 (GPU animation drain), #18693 (desktop slowdown with large histories), and #16688 (TUI freeze) are top-of-mind for daily drivers.
- **Windows-specific issues** – #2137 (multi-line paste), #10347 (UNC path handling), and #21147 (WSL mode spawns PowerShell) show ongoing platform gaps.
- **UI/UX regressions** – #20607 (Shift+Enter broken on macOS 0.128.0) and #21154 (thread titles storing full messages) degrade the experience for returning users.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-05

## 1. Today’s Highlights

Today’s nightly release (`v0.42.0-nightly.20260504`) brings a significant refactor of the ACP client and documentation workflow updates. On the bug front, a newly filed crash on large pastes (#26491) and a persistent shell‑command hang (#25166) are drawing attention. The community is actively discussing agent evaluation robustness (#24353) and AST‑aware file mapping (#22745), while new PRs propose multi‑agent orchestration (#26345) and auto‑discovery of MCP configuration files (#26490).

## 2. Releases

**v0.42.0-nightly.20260504.g37edd1d4d**  
[Release link](https://github.com/google-gemini/gemini-cli/releases/tag/v0.42.0-nightly.20260504.g37edd1d4d)  
* Changes:  
  - Update documentation workflows with workspace trust by @g-samroberts  
  - Refactor `acpClient` into specialized files by @sripasg  
  - Test fixes  

---

## 3. Hot Issues (10 noteworthy)

1. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   `priority/p1, area/agent` – Epic to extend behavioral eval framework (76 tests today). Community wants more granular coverage; 5 comments, 0 👍.

2. **[#22745 – AST‑aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   `area/agent` – Investigates using AST to read methods precisely and reduce token noise. 5 comments, 1 👍. High strategic value.

3. **[#22323 – Subagent recovery after MAX_TURNS reports success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   `priority/p1, area/agent` – `codebase_investigator` falsely reports `GOAL` success when hitting turn limits. 4 comments, 2 👍.

4. **[#24916 – Re‑peated permission prompts on the same file](https://github.com/google-gemini/gemini-cli/issues/24916)**  
   `area/security` – Users report “allow for all future sessions” ignored. 3 comments, 0 👍. Irritating UX.

5. **[#25166 – Shell command stuck on “Waiting input” after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   `area/core` – Simple commands hang; 2 comments, 3 👍. Reproducible and high impact.

6. **[#26491 – CLI crash / infinite loop on large text paste (>2,000 chars)](https://github.com/google-gemini/gemini-cli/issues/26491)**  
   `status/need-triage` – New regression in input buffer handling. 1 comment, 0 👍. Urgent.

7. **[#22267 – Browser Agent ignores settings.json overrides (e.g., maxTurns)](https://github.com/google-gemini/gemini-cli/issues/22267)**  
   `priority/p2, area/agent` – AgentRegistry fails to merge project settings. 2 comments, 0 👍.

8. **[#23571 – Model creates tmp scripts in random places](https://github.com/google-gemini/gemini-cli/issues/23571)**  
   `priority/p2, area/agent` – Workspace cleanup overhead. 2 comments, 0 👍.

9. **[#24246 – 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   `area/agent` – Excessive tool count triggers API error. 1 comment, 0 👍. Suggests tool‑scoping improvements.

10. **[#22186 – get‑shit‑done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)**  
    `priority/p1, area/agent` – Crash when printing user summary. 1 comment, 0 👍.

---

## 4. Key PR Progress (10 important)

1. **[#24782 – allowEnv policy option for shell commands](https://github.com/google-gemini/gemini-cli/pull/24782)**  
   `area/enterprise` (CLOSED) – Adds `allowEnv` rule to let the AI run prefixed env commands without confirmation. Merged.

2. **[#26490 – Auto‑discover .mcp.json from project root](https://github.com/google-gemini/gemini-cli/pull/26490)**  
   `status/need-issue` (OPEN) – Solves MCP config duplication; aligns with Claude Code convention.

3. **[#26489 – Skip O(N) token calculation when tracer disabled](https://github.com/google-gemini/gemini-cli/pull/26489)**  
   `status/need-issue` (OPEN) – Performance fix for `render.ts` – eagerly evaluated call eliminated.

4. **[#26345 – Secure non‑interactive multi‑agent orchestration](https://github.com/google-gemini/gemini-cli/pull/26345)**  
   `status/need-issue` (OPEN) – Conservative sequential execution for non‑interactive CLI, preserving policies.

5. **[#25900 – Prefer pwsh.exe over Windows PowerShell 5.1](https://github.com/google-gemini/gemini-cli/pull/25900)**  
   `priority/p2, status/pr-nudge-sent` (OPEN) – Fixes embedded‑quote stripping on Windows; closes several related issues.

6. **[#26487 – Speed up --resume / /resume session listing](https://github.com/google-gemini/gemini-cli/pull/26487)**  
   (OPEN) – Stops JSON‑parsing every chat file for metadata; reduces 10–15s hang on Windows.

7. **[#24736 – Union‑find context compaction for AgentHistoryProvider](https://github.com/google-gemini/gemini-cli/pull/24736)**  
   `area/agent, help wanted` (OPEN) – Alternative compression strategy: hot buffer + cold forest for semantic similarity clustering.

8. **[#26432 – Improve error messages for authentication failures](https://github.com/google-gemini/gemini-cli/pull/26432)**  
   `priority/p2` (OPEN) – Replaces vague exceptions with actionable messages for missing API key, 400, 401 errors.

9. **[#26479 – Fix A2A server tool approval race condition](https://github.com/google-gemini/gemini-cli/pull/26479)**  
   `status/need-issue` (CLOSED) – Prevents premature `input-required` state while tools are still validating.

10. **[#26480 – Steer model to surgical edits, prevent accidental deletions](https://github.com/google-gemini/gemini-cli/pull/26480)**  
    `area/agent` (OPEN) – Updates tool descriptions for `write_file`/`replace` to encourage targeted edits.

---

## 5. Feature Request Trends

The most‑requested capabilities, distilled from recent issues, fall into three clusters:

- **Agent intelligence & reliability** – Better memory routing (global vs. project, #22819), AST‑aware code understanding (#22745), subagent recovery after turn limits (#22323), and automatic session takeover for browser agent (#22232).
- **Enterprise & security** – Environment variable policies (`allowEnv`, #24782), secure multi‑agent orchestration (#26345), and improved authentication error reporting (#26432).
- **Developer experience** – Auto‑discovery of MCP JSON (#26490), faster session listing (#26487), and non‑duplicating permission prompts (#24916).

---

## 6. Developer Pain Points

Recurring frustrations reported by the community:

- **Permission handling** – Repeated prompts on the same file (#24916); `allow for all future sessions` failing.
- **Shell execution issues** – Commands stuck after completion (#25166); model creating random tmp scripts (#23571).
- **Crashes & hangs** – Large paste causes infinite loop (#26491); `get‑shit‑done` output hook crashes (#22186); CLI hang on Windows `A:\` path (#25216).
- **Inconsistent configuration** – Browser agent ignoring `settings.json` (#22267); settings overrides not merged.
- **Performance regressions** – Token breakdown calculation running even when tracer disabled (#26489); `--resume` taking 10+ seconds (#26487).
- **Accessibility & display** – Scrambled text over SSH (#24202); broken table rendering during streaming (#25218); scrollbar jumps in long chats (#24470).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-05

## Today’s Highlights
A minor release (v1.0.41-0) landed today, adding an `--attachment` flag for non-interactive prompts and improving file-edit reliability. The bug tracker remains active, with several high-severity issues around model availability (Claude Opus 4.5, GPT‑5.5 BYOK) and a persistent HTTP/2 GOAWAY race condition that silently wastes premium requests. Meanwhile, two new feature requests propose a `gh copilot feedback` command and a timer for agent thinking time.

## Releases
**v1.0.41-0**  
- **Added**: `--attachment` flag in non-interactive (`-p`/`--prompt`) mode to attach files (images or native documents) to the initial prompt.  
- **Improved**: Reliability of file edits by better recovering from fuzzy or misaligned edit blocks.  
- **Fixed**: `@-mention` completion works for `./` paths.

## Hot Issues (10 noteworthy items)

1. **[#2591](https://github.com/github/copilot-cli/issues/2591) — [CLOSED] Infinite premium requests per tool invocation**  
   Single request consumed 80–100 premium requests because each agent reply triggered a new API call. **Community reaction**: 31 comments, 13 👍. *Closed after extensive discussion*.

2. **[#2421](https://github.com/github/copilot-cli/issues/2421) — [OPEN] HTTP/2 GOAWAY race condition causes cascading retry failures**  
   Undici HTTP/2 pool misbehaves when server sends GOAWAY mid-flight, leading to silent premium request waste. Consolidates five earlier issues. **16 👍, 7 comments** – a top pain point for heavy CLI users.

3. **[#953](https://github.com/github/copilot-cli/issues/953) — [OPEN] Excessive permission requests on authentication**  
   Users want scoped permissions (read/write per repo) instead of blanket access. **7 comments, 3 👍** – long-running request for enterprise/security teams.

4. **[#2643](https://github.com/github/copilot-cli/issues/2643) — [OPEN] Plugin `preToolUse` silent rewrite still shows confirmation dialog**  
   Even with `permissionDecision: allow`, rewritten commands prompt the user. **6 comments** – blocks fully automated plugin workflows.

5. **[#1665](https://github.com/github/copilot-cli/issues/1665) — [OPEN] Support project/repo-scoped plugins**  
   Plugins are currently global per user; teams want per-repo configuration files. **5 comments, 11 👍** – strong community demand.

6. **[#2795](https://github.com/github/copilot-cli/issues/2795) — [OPEN] `--agent` + `--plugin-dir` + `-p` fails to find agent**  
   The CLI scans wrong directories when all three flags are used. **4 comments, 12 👍** – high impact for agent-heavy setups.

7. **[#3019](https://github.com/github/copilot-cli/issues/3019) — [OPEN] Breaking: `.vscode/mcp.json` support removed**  
   Users now must maintain separate MCP configs for CLI and VS Code. **3 comments, 2 👍** – a regression for multi-editor environments.

8. **[#2528](https://github.com/github/copilot-cli/issues/2528) — [OPEN] Add per-repository MCP server configuration**  
   Request for `.github/mcp.json` similar to custom instructions. **3 comments, 5 👍** – aligns with plugin scoping requests.

9. **[#2052](https://github.com/github/copilot-cli/issues/2052) — [OPEN] Persistent token/context usage indicator**  
   Users want an always‑visible “45% context used” bar in the TUI. **2 comments, 11 👍** – strong desire for resource transparency.

10. **[#3101](https://github.com/github/copilot-cli/issues/3101) — [OPEN] Enterprise: model access denied by Copilot policy**  
   Error persists even in v1.0.40. **1 comment, 2 👍** – enterprise accounts affected by policy misconfiguration.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
The most demanded feature directions across recent issues are:

- **Project‑scoped configuration**: Per‑repository MCP servers (`.github/mcp.json`) and project‑level plugin directories (e.g., `.github/copilot-plugins/`).  
- **Visibility improvements**: A persistent token/context usage indicator, a timer for agent thinking time, and a `gh copilot feedback` command to file issues from the terminal.  
- **Model control**: Allow sub‑agents to use the model specified in their `.agent.md` frontmatter (opt‑out for cost‑multiplier guard); better BYOK model catalog coverage.  
- **Plugin ecosystem**: Silent command rewriting, headless plugin loading, and the ability to list available agents in stdout for automation.

## Developer Pain Points
Recurring frustrations voiced in the community:

- **Model instability**: “Model keeps switching to auto,” “Opus 4.5 suddenly unsupported,” and “BYOK GPT‑5.5 missing from limits catalog” – poor model persistence and onboarding.  
- **Silent premium consumption**: The GOAWAY race condition (#2421) and the infinite‑request loop (#2591) waste $ without user awareness.  
- **Permission model granularity**: Harmless commands like `2>/dev/null` still prompt (#2693), and authentication asks for universal write access (#953).  
- **TUI usability**: Terminal output overwrites scrollback (#3110), macOS backspace breaks attached image tokens (#3105), and long conversations get caught in reprocessing loops (#3114).  
- **MCP & plugin friction**: No per‑repo MCP config, `.vscode/mcp.json` support removed, and plugins fail in non‑interactive (`-p`) mode.  
- **Transient API errors during peak hours** (#3117) – several reports of “retrying” loops, especially in evening time zones.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-05-05

## 1. Today's Highlights
A community plugin introducing persistent cross-session memory (`kimi-mneme`) was showcased, indicating growing interest in context retention. On the stability front, three crash-related bugs (Windows, WSL) and one login failure on Linux were reported within the last 24 hours, all concerning version 1.41.0. No new releases or pull requests were published today.

## 2. Releases
No new releases in the last 24 hours. The current stable version remains `1.41.0`.

## 3. Hot Issues
*Only 4 issues were updated in the reporting window. They are listed below with commentary on their relevance.*

- **[#2160 – [bug] Inexplicable crash during operation](https://github.com/MoonshotAI/kimi-cli/issues/2160)**  
  *Author: elcky | Comments: 3 | 👍: 0*  
  **Why it matters:** Users on Windows 10 x64 running Kimi 2.6 experience random crashes and disappearances. With 3 comments, this is the most discussed crash issue. The lack of upvotes may indicate it’s an intermittent problem affecting a small subset.

- **[#2162 – [bug] Cannot Login](https://github.com/MoonshotAI/kimi-cli/issues/2162)**  
  *Author: gg582 | Comments: 1 | 👍: 0*  
  **Why it matters:** Login failure on Linux (aarch64, kernel 6.18.15) blocks all functionality. This is a critical entry-point bug, especially for users on non‑x86 architectures.

- **[#2161 – Plugin Showcase: kimi-mneme — Persistent Memory for Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli/issues/2161)**  
  *Author: barrelc | Comments: 1 | 👍: 0*  
  **Why it matters:** A community plugin that solves the “blank slate” problem by compressing and restoring context across sessions. This demonstrates the ecosystem’s desire for long‑term memory, a feature not yet natively supported.

- **[#2163 – [bug] Random KIMI CLI crash on WSL](https://github.com/MoonshotAI/kimi-cli/issues/2163)**  
  *Author: spektant-png | Comments: 0 | 👍: 0*  
  **Why it matters:** Similar crash pattern as #2160 but on Windows 11 with WSL (Ubuntu). It shows the instability is not platform‑specific, affecting both native Windows and WSL users.

## 4. Key PR Progress
No pull requests were updated in the last 24 hours.

## 5. Feature Request Trends
The only feature‑related contribution this week is the **persistent memory** plugin (#2161). This aligns with a recurring community wish: **context retention across sessions** (the “blank slate” problem). Users want the CLI to remember conversation history, project state, and preferences without manual re‑entry.

## 6. Developer Pain Points
- **Unexplained crashes across platforms** – Two separate crash reports (#2160, #2163) on Windows and WSL with identical symptoms (random termination, disappearance). All affect version 1.41.0 with the Kimi 2.6 model.
- **Login blocking on uncommon architectures** – Issue #2162 shows that login fails entirely on Linux aarch64, preventing any usage. No workaround is mentioned yet.
- **No upvotes or strong community engagement** – Only 4 comments total across all issues, suggesting either low user activity or that these bugs are hard to reproduce. The team may need more detailed logs to diagnose crashes.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-05

## Today's Highlights

Three patch releases rolled out in the last 24 hours, led by **v1.14.37** which fixes child task cancellation and brings cleaner v2 session rendering plus workspace warping. The community is buzzing about a **Kimi k2.5 tool‑calling regression** (#20650) with 47 comments, and a **Windows startup freeze** (#24418) affecting 1.14.25+ users. On the PR side, a long‑awaited **`.opencode/AGENTS.md` loading** feature (#12096) was merged, and a new **Open WebUI provider** (#18306) is under review.

## Releases

- **[v1.14.37](https://github.com/anomalyco/opencode/releases/tag/v1.14.37)** — Canceling a task now also cancels child subtask sessions. Improved v2 session rendering: cleaner tool states, better compaction summaries, more accurate timing. Added ability to warp a session into another workspace or back to local project.
- **[v1.14.35](https://github.com/anomalyco/opencode/releases/tag/v1.14.35)** — Bugfix: preserve diff patch boundaries so session diffs keep rendering correctly when file contents include `diff --git` text.
- **[v1.14.34](https://github.com/anomalyco/opencode/releases/tag/v1.14.34)** — Added PTY connection tickets for more reliable authenticated terminal websockets. Added v2 session failure events for client detection. Improved shell command handling for Bash, PowerShell, cmd.

## Hot Issues

1. **#20650 — Kimi k2.5 tool‑calling broken**  
   [Issue](https://github.com/anomalyco/opencode/issues/20650) (47 comments, 4 👍)  
   Model produces malformed JSON for tool calls (e.g., unterminated strings) and tries unavailable tools. High‑impact for Kimi users; still open.

2. **#6680 — [FEATURE] View archived sessions on desktop**  
   [Issue](https://github.com/anomalyco/opencode/issues/6680) (30 comments, 6 👍)  
   Request for a menu item to list/show archived sessions. Long‑standing (since Jan), low effort, high value.

3. **#24418 — Windows CLI stuck on “Loading plugins…” (50% of startups)**  
   [Issue](https://github.com/anomalyco/opencode/issues/24418) (23 comments)  
   Regression after v1.14.25. Can’t Ctrl+C; must kill terminal. Affects users with no plugins installed.

4. **#11830 — Multi‑account OAuth support with auto‑relogin**  
   [Issue](https://github.com/anomalyco/opencode/issues/11830) (20 comments, 16 👍)  
   Users need multiple accounts per provider to handle rate limits. Includes credential rotation and browser‑based session management.

5. **#10490 — Config option to disable copy‑on‑select**  
   [Issue](https://github.com/anomalyco/opencode/issues/10490) (13 comments, 23 👍)  
   Copy‑on‑select is forced on; users want a toggle in `opencode.json`. Very popular.

6. **#23315 — No release files for v1.4.12 (Homebrew 404)**  
   [Issue](https://github.com/anomalyco/opencode/issues/23315) (12 comments, 10 👍)  
   Missing release assets caused installation failures. Now closed, but highlighted a process gap.

7. **#19081 — Reasoning content stripped from assistant messages on replay**  
   [Issue](https://github.com/anomalyco/opencode/issues/19081) (8 comments, 15 👍)  
   Thinking tokens are lost in subsequent turns, breaking KV cache for local inference. Affects users running models like DeepSeek.

8. **#234 — Tool calling issues with open‑source models**  
   [Issue](https://github.com/anomalyco/opencode/issues/234) (7 comments, 24 👍)  
   Long‑running issue: OS models (e.g., Llama, Qwen) have inconsistent tool‑calling formats vs. frontier models. High popularity.

9. **#25799 — v1.14.35 breaks OMO plugin loading**  
   [Issue](https://github.com/anomalyco/opencode/issues/25799) (7 comments, 2 👍)  
   After updating, OMO (oh‑my‑opencode) fails to load; only Build and Plan tabs remain. Closed as regression.

10. **#25832 — Opencode cannot read images anymore**  
    [Issue](https://github.com/anomalyco/opencode/issues/25832) (4 comments)  
    Image analysis (PNG/JPG) stopped working around May 5, returns `Bad Request`. Regression likely after recent provider changes.

## Key PR Progress

1. **[#12096](https://github.com/anomalyco/opencode/pull/12096) — Load `.opencode/AGENTS.md` instructions** (merged)  
   Adds project‑level agent rules from `.opencode/AGENTS.md`, alongside existing `AGENTS.md`/`CLAUDE.md`. Closes #11454.

2. **[#18306](https://github.com/anomalyco/opencode/pull/18306) — Open WebUI provider** (open)  
   New provider integration for self‑hosted Open WebUI instance. Builds on earlier work; still in review.

3. **[#18767](https://github.com/anomalyco/opencode/pull/18767) — Mobile touch optimization** (open)  
   Improves touch interactions for the app without breaking desktop. Addresses tap targets, scrolling, zoom.

4. **[#7239](https://github.com/anomalyco/opencode/pull/7239) — Write truncated tool outputs to files** (merged)  
   When large tool output is truncated, saves full content to a local file and references it. Closes #7168, #4560.

5. **[#25833](https://github.com/anomalyco/opencode/pull/25833) — Respect safe area in web shell** (open)  
   Fixes Safari safe‑area insets for iOS/iPadOS by using `viewport-fit=cover` and `env()` padding.

6. **[#25680](https://github.com/anomalyco/opencode/pull/25680) — Propagate hashline tool args to schema** (merged)  
   Fixes hashline plugin: edit tool call args (`startRef`, `operation`, `content`) now exposed in JSON Schema, required by strict‑schema models like DeepSeek.

7. **[#16279](https://github.com/anomalyco/opencode/pull/16279) — Update locale cookie on language change** (merged)  
   Fixes language persistence when switching back to English after using a localized language in web client.

8. **[#16273](https://github.com/anomalyco/opencode/pull/16273) — Pass `roots:true` in TUI session list bootstrap** (merged)  
   Prevents child sessions from diluting the root session list; improves session tree rendering.

9. **[#16251](https://github.com/anomalyco/opencode/pull/16251) — Improve desktop project switching performance** (merged)  
   Reduces synchronous work on switching projects; avoids redundant processing.

10. **[#16248](https://github.com/anomalyco/opencode/pull/16248) — Generate MCP OAuth state on‑the‑fly** (merged)  
    Fixes remote MCP server OAuth flows by generating state at connection time instead of using a stale value.

## Feature Request Trends

- **Account & Auth Flexibility** — Multi‑account OAuth (#11830) and automatic credential rotation dominate requests. Users want to seamlessly switch accounts when rate limits hit.
- **Session Lifecycle Management** — Requests for archived session viewing (#6680), factory reset/incognito mode (#25653), and batch delete of sessions (#25653) show a need for better data control.
- **UI Customisation** — Copy‑on‑select disable toggle (#10490) and preset instructions in chat UI (#25616) reflect desire for user‑configurable terminal behavior.
- **Localisation & Compliance** — Incomplete Chinese translations (#25604) and requests for AI‑driven GitHub template compliance (#25785) point to growing global and enterprise usage.
- **Agent & Rules Configuration** — Improved `/init` and guided `AGENTS.md` setup (#25655) and loading from `.opencode/AGENTS.md` (now merged via #12096) are highly requested.

## Developer Pain Points

- **Windows‑specific regressions** — CLI stuck on “Loading plugins” (#24418), missing entry point for older Windows (#9875), and desktop not showing models/conversations (#23011) indicate chronic Windows stability issues.
- **Plugin compatibility breaks** — OMO failing to load after update (#25799) and custom agents not appearing in desktop GUI (#25824) frustrate plugin‑heavy workflows.
- **Model/Provider integration bugs** — Image analysis broken (#25832), reasoning content stripped on replay (#19081), model not recognised for subagents (#25802), and `/models` showing presets instead of local models (#25351) hurt multi‑model setups.
- **UI/UX regressions** — Removal of refresh/delete buttons (#25827), copy‑on‑select causing selection to stop working (#14420), and VSCode clipboard permission denied (#25809) degrade day‑to‑day usability.
- **Retry state lock** — Inability to stop retry state to clean up context after quota recovery (#25803) leaves users without control over failed sessions.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-05

## Today’s Highlights
Version **v0.73.0** shipped with Xiaomi MiMo API billing and new regional token-plan providers. The community is most animated by the long‑running push for official local LLM providers (#3357 with 22 👍), while a flurry of bug reports (many tagged `closed-because-bigrefactor`) signal a major internal refactor is underway. A high‑impact PR (#4154) delivering four ready‑to‑use local‑LLM extensions landed, directly addressing the top feature request.

## Releases
**v0.73.0** — one change:
- **Xiaomi MiMo API billing** – the `xiaomi` provider now uses API billing; separate `xiaomi-token-plan-{cn,ams,sgp}` providers have been added. See [docs/providers.md#api-keys](docs/providers.md#api-keys) and [README.md#providers--models](README.md#providers--models).

## Hot Issues (10 noteworthy)

1. **[#3357 – Official local LLM provider extension](badlogic/pi-mono Issue #3357)** (OPEN, 8 comments, 👍22)  
   *Why it matters:* The #1 community ask—dynamic model fetching from local servers (llama.cpp, Ollama, LM Studio). High upvote count shows strong demand for self‑hosted workflow.

2. **[#3208 – Custom Thinking Levels per Model](badlogic/pi-mono Issue #3208)** (CLOSED, 14 comments, 👍13)  
   *Why it matters:* Proposal to let models define their own thinking levels in `models.json`. Active discussion and author offered to implement; signals desire for per‑model granularity.

3. **[#3567 – Official llama.cpp provider](badlogic/pi-mono Issue #3567)** (CLOSED, 4 comments)  
   *Why it matters:* Complements #3357; directly asks for llama‑server integration with sensible defaults. Now superseded by the PR #4154.

4. **[#4157 – `pi-update` warning on Windows](badlogic/pi-mono Issue #4157)** (OPEN, 4 comments)  
   *Why it matters:* TLS certificate bypass warnings on Windows. Affects all Windows users; no workaround mentioned yet.

5. **[#4173 – `/login` for Anthropic OAuth gives invalid URL](badlogic/pi-mono Issue #4173)** (CLOSED, 3 comments)  
   *Why it matters:* Blocks connecting to Claude Code Pro subscriptions. Reproducible and labelled as a bug; closed due to the bigrefactor.

6. **[#4163 – `pi -p` silently no-ops when prompt starts with `---`](badlogic/pi-mono Issue #4163)** (CLOSED, 3 comments)  
   *Why it matters:* Critical for script automation—no error, no output. Breaks pipelines and makes debugging opaque.

7. **[#4158 – TUI markdown nested‑list double indent](badlogic/pi-mono Issue #4158)** (OPEN, 3 comments)  
   *Why it matters:* Visual regression on both shipped themes. Indent drifts deeper per nesting level; affects readability of structured chat output.

8. **[#4160 – Extensions incompatible with Bun](badlogic/pi-mono Issue #4160)** (CLOSED, 2 comments)  
   *Why it matters:* Extensions hard‑require `npm`, failing with Bun. Limits use of alternative runtimes. Workaround suggested in thread.

9. **[#4180 – Links not clickable after recent update](badlogic/pi-mono Issue #4180)** (CLOSED, 2 comments)  
   *Why it matters:* Regression likely from alternate terminal mode. Breaks a core UX expectation—clickable URLs.

10. **[#4142 – macOS paste crash in sandbox environments](badlogic/pi-mono Issue #4142)** (OPEN, 2 comments)  
    *Why it matters:* Hard abort when pasteboard access is denied. Affects users in seatbelt sandboxes or limited permissions.

## Key PR Progress (10 important)

1. **[#4154 – Official local‑LLM provider extensions](badlogic/pi-mono PR #4154)** (CLOSED)  
   Delivers four async‑factory custom providers for llama.cpp, Ollama, LM Studio, and a generic OAI‑compatible server. Closes #3357 and #3469. The most anticipated contribution this week.

2. **[#4162 – Allow comments & trailing commas in `models.json`](badlogic/pi-mono PR #4162)** (CLOSED)  
   Small but ergonomic: adds `stripJsonComments` so users can annotate model config without breaking JSON parsing.

3. **[#4178 – Moonshot K2.6 reasoning_content placeholder fix](badlogic/pi-mono PR #4178)** (CLOSED)  
   Provider‑specific fix: ensures non‑empty `reasoning_content` on assistant messages to avoid 400 errors for Moonshot K2.6 when thinking is enabled.

4. **[#3887 – Image content support](badlogic/pi-mono PR #3887)** (OPEN)  
   New API for image blocks and image models (Google/OpenRouter). Includes TUI demo; significant feature expansion.

5. **[#4170 – Preserve OpenRouter reasoning with Responses API](badlogic/pi-mono PR #4170)** (CLOSED)  
   Fixes out‑of‑order stream events for OpenRouter on the `openai‑responses` endpoint, correcting reasoning token handling.

6. **[#4165 – Stream bash output incrementally](badlogic/pi-mono PR #4165)** (CLOSED)  
   Performance fix: replaces full‑buffer rebuild with incremental streaming for bash tool output, preventing TUI lag on chatty commands.

7. **[#4183 – OAuth localhost callback branding](badlogic/pi-mono PR #4183)** (CLOSED)  
   Allows consumers of Pi‑ai to brand the callback HTML page with their own logo/title instead of hard‑coded Pi branding. Useful for embedded CLIs.

8. **[#4126 – Retry on transient 404/408](badlogic/pi-mono PR #4126)** (CLOSED)  
   Extends retry logic (previously only 429, 5xx) to cover 404 and 408 status codes. Concrete trigger observed with Cerebras edge returns.

9. **[#3737 – Correct GPT-5.5 context metadata](badlogic/pi-mono PR #3737)** (CLOSED)  
   Sets accurate context window sizes for GPT‑5.5 across OpenAI, Azure, and Codex routes. Prevents erroneous context‑limit errors.

10. **[#4181 – Add `.claude/` to `.gitignore`](badlogic/pi-mono PR #4181)** (CLOSED)  
    Simple ergonomic PR for developers using Claude Code on the project. Merged quickly.

## Feature Request Trends

- **Local LLM dominance** – The most vocal demand is for first‑class support of local inference engines (llama.cpp, Ollama, LM Studio). #3357 and #3567 are the canonical asks; PR #4154 now delivers a concrete implementation.
- **Per‑model configuration** – Custom thinking levels (#3208) and provider‑specific settings (e.g., reasoning_content placeholder, context windows) reflect a desire for fine‑grained model control.
- **Cross‑platform compatibility** – Requests for Bun support (#4160), better Windows handling (#4157), and Wayland clipboard (#4177) show the user base extends beyond the primary platform.
- **UI/UX polish** – Multiple issues about markdown rendering, link clickability, and color scheme contrast (#4158, #4180, #4185) indicate a need for more robust terminal UI.

## Developer Pain Points

- **Unexpected silent failures** – `pi -p` with `---` (#4163) and expired tokens causing hangs (#4141) break automation and trust.
- **Platform gaps** – Windows TLS warnings, Wayland clipboard false positives, macOS paste crashes, and Bun incompatibility create friction for a diverse user base.
- **Performance regressions** – Bash tool streaming O(n²) (#4145), resource‑loader reload spam (#4151), and terminal‑disappearance CPU spin (#4144) degrade long‑running sessions.
- **OAuth fragility** – Anthropic `/login` URL missing parameters (#4173) and Codex usage limit not parsed (#4172) hinder paid subscription usage.
- **UI breakage** – Markdown indent drift, non‑clickable links, and model selector display bugs (#4164) reduce the polish expected from a modern TUI.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-05-05 Qwen Code 社区文摘。

---

## Qwen Code 社区文摘 | 2026-05-05

### 1. 今日亮点

本周Qwen Code社区异常活跃，发布了最新的`v0.15.6-nightly`版本，引入了文件读取缓存和代理设置修复。在功能方面，社区热烈讨论并迅速推进了WebSearch工具的集成，同时多项核心优化（如内存召回延迟、终端渲染问题、会话膨胀）正在通过PR得到解决。开发者对终端稳定性、配置兼容性和大文件处理的痛点反馈集中，但核心团队响应迅速。

### 2. 版本发布

**最新发布: [v0.15.6-nightly.20260505.2e69d641d](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.6-nightly.20260505.2e69d641d)**
- **主要变更：**
    - **性能优化：** `feat(core): add FileReadCache and short-circuit unchanged Reads` 新增了文件读取缓存机制，避免在文件未变更时重复读取，提升工具调用效率。
    - **Bug修复：** `fix(cli): honor proxy setting` 修复了CLI模式下未能正确遵循系统代理设置的问题。

### 3. 热门问题 (Hot Issues)

1.  **#3838 [终端界面无限滚动/刷新循环] (https://github.com/QwenLM/qwen-code/issues/3838)**
    - **重要性：** 致命性UI问题。当模型进行大量代码输出时，终端界面进入疯狂刷新循环，完全无法阅读。这严重影响了核心编码场景的用户体验。
    - **社区反应：** 刚被报告，暂无明显讨论，但影响面可能很大。

2.  **#3822 [大文件编辑后会话JSONL膨胀，导致/恢复极慢] (https://github.com/QwenLM/qwen-code/issues/3822)**
    - **重要性：** 核心性能问题。使用`edit`/`write`处理大文件会导致会话文件大小膨胀，进而使得`/resume`功能加载缓慢甚至卡死。
    - **社区反应：** 开发者 `RunMintOn` 提供了详细的根因分析（`resultDisplay`未做大小限制），这是一个高质量的bug报告，很可能被开发团队优先处理。

3.  **#3669 [使用自定义模型时思考字段出现错误] (https://github.com/QwenLM/qwen-code/issues/3669)**
    - **重要性：** 兼容性问题。使用MiniMax等第三方提供商的模型时，模型输出的`<think>`标签无法被正确解析和渲染，破坏了“思考链路”的视觉体验。
    - **社区反应：** 已关闭，表明该问题已通过相关PR修复。

4.  **#3843 [启动时覆盖settings.json配置文件] (https://github.com/QwenLM/qwen-code/issues/3843)**
    - **重要性：** 严重的配置管理问题。每次启动都会无条件覆盖用户的`settings.json`文件，这可能导致用户自定义配置丢失。
    - **社区反应：** 刚报告，暂无回复。这是个非常危险的bug，预计会得到紧急处理。

5.  **#3839 [编辑/写入文件功能静默覆盖外部修改] (https://github.com/QwenLM/qwen-code/issues/3839)**
    - **重要性：** 数据安全与并发控制问题。如果模型读取后，文件被外部修改，`Edit`和`WriteFile`不会报错，而是直接覆盖。这可能导致用户数据丢失。
    - **社区反应：** 开发者 `ihubanov` 已提出具体修复方案，并在同一天提交了PR #3840，响应迅速。

6.  **#3825 [在Zed中集成时出现401错误] (https://github.com/QwenLM/qwen-code/issues/3825)**
    - **重要性：** 核心IDE集成问题。用户在Zed中配置好登录后仍反复出现401 token过期错误，这直接导致A C P模式无法使用，影响了平台扩展性。
    - **社区反应：** 已关闭，推测与代理或认证流程有关，但日志显示已修复或正在排查。

7.  **#3824 [终端Resize时底部输入框蓝色边框/分隔线残留并累积] (https://github.com/QwenLM/qwen-code/issues/3824)**
    - **重要性：** 终端渲染Bug。窗口resize后，输入框区域的蓝色边框不能正确擦除并不断累积，导致显示混乱。
    - **社区反应：** 开发者 `RunMintOn` 提供了详细的复现截图和现象描述，疑似与Ink UI库的版本有关。

8.  **#3829 [Wayland上无法粘贴图片] (https://github.com/QwenLM/qwen-code/issues/3829)**
    - **重要性：** Linux Wayland兼容性问题。核心功能“粘贴图片”在最新版本的Wayland环境下失效，影响用户体验。
    - **社区反应：** 刚报告，暂无解决方案。与历史问题#2885关联，表明该问题可能长期存在。

9.  **#3823 [@qwen-code/sdk 升级后CLI进程报错退出] (https://github.com/QwenLM/qwen-code/issues/3823)**
    - **重要性：** SDK稳定性问题。升级SDK版本后，原本正常的任务会随机触发 “CLI process exited with code 1” 错误，对下游开发者和集成方影响很大。
    - **社区反应：** 刚报告，开发团队需要排查是SDK内部原因还是集成方的使用问题。

10. **#3387 [OpenAI兼容的MiniMax接口泄露`<think>`内容] (https://github.com/QwenLM/qwen-code/issues/3387)**
    - **重要性：** 核心兼容性Bug。使用OpenAI兼容端点时，MiniMax的思考内容直接以纯文本形式暴露给用户，而非渲染在思考UI中。这与#3669和#3228是同一类问题的不同表现。
    - **社区反应：** 已关闭，表明相关修复已合并。

### 4. 关键PR进展 (Key PR Progress)

1.  **#3844 [feat(tools): 添加WebSearch工具] (https://github.com/QwenLM/qwen-code/pull/3844)**
    - **核心内容：** 核心开发者 `wenshao` 提交的，为DashScope兼容提供商实现了一个具备7层提示注入防御的显式`web_search`工具。这是对社区长期需求（#3841）的关键响应，填补了Qwen Code在搜索功能上的空白。

2.  **#3701 [feat(cli): 改进export格式补全导航] (https://github.com/QwenLM/qwen-code/pull/3701)**
    - **核心内容：** 改进了交互式`/export`命令的格式补全导航体验，使开发者更容易导出不同格式的会话记录。

3.  **#3840 [feat(core): 拒绝在文件变更后执行编辑/写入] (https://github.com/QwenLM/qwen-code/pull/3840)**
    - **核心内容：** 直接解决了#3839问题。在写入文件前，检查文件自上次读取后是否被修改，如果已变，则拒绝写入并通知用户，有效防止数据被静默覆盖。

4.  **#3814 [fix(core): 防止自动记忆回忆阻塞主请求] (https://github.com/QwenLM/qwen-code/pull/3814)**
    - **核心内容：** 修复了每次对话轮次都因自动记忆查询（含5秒超时）而延迟约5秒的性能问题，这对于提升长对话的流畅度至关重要。

5.  **#3836 [feat(core,cli): 展示并取消自动记忆“做梦”任务] (https://github.com/QwenLM/qwen-code/pull/3836)**
    - **核心内容：** 将后台自动记忆整合任务纳入统一的“后台任务”UI，并使其可取消。这增强了用户对系统后台行为的可见性和控制力。

6.  **#3818 [fix(core): 合并MCP服务器重复发现] (https://github.com/QwenLM/qwen-code/pull/3818)**
    - **核心内容：** 修复了MCP服务器重新连接时可能发起多个重复发现请求，导致MCP进程启动失败的问题。这是对服务器稳定性的重要提升。

7.  **#3677 [fix(openai): 解析MiniMax思考标签] (https://github.com/QwenLM/qwen-code/pull/3677)**
    - **核心内容：** 为MiniMax OpenAI兼容端点添加了思考标签解析支持，将`<think>`和`<thinking>`内容正确渲染为思考部分，修复了#3387、#3228和#3669等问题。

8.  **#3774 [feat(core): 强制编辑/写入前先读取文件] (https://github.com/QwenLM/qwen-code/pull/3774)**
    - **核心内容：** 实现了更严格的文件操作安全策略：模型必须在其会话中实际读取过某个文件，才能对其进行编辑或写入操作，防止模型在未确认文件内容的情况下进行修改。

9.  **#3832 [fix(sdk-python): 标准化标签前缀] (https://github.com/QwenLM/qwen-code/pull/3832)**
    - **核心内容：** 修复了Python SDK的版本标签前缀不一致问题，使其与TypeScript SDK保持一致，避免在CI/CD流程中产生混淆。

10. **#3819 [fix(core): 防止并发发现导致的重复MCP进程] (https://github.com/QwenLM/qwen-code/pull/3819)**
    - **核心内容：** 在MCP客户端管理中增加了并发防护，防止对同一个服务器的并发发现操作生成重复的子进程，从而避免了资源泄漏和通信混乱。

### 5. 功能请求趋势

- **背景任务管理：** 围绕**背景任务管理**（Issue #3634）的持续演进是当前最大的趋势。从合并Phase A/B，到设计Phase D（如通过`Ctrl+B`将前台进程发送到后台，PR #3842），社区和核心团队正在系统地构建一个完整的后台异步执行生态系统。
- **Web搜索集成：** **WebSearch工具**（#3841, PR #3844）是一个强烈的需求。社区普遍认为这是一个关键缺失，而开发团队在短短一天内就从设计讨论（#3841）推进到了实现阶段（#3844），反应非常迅速。
- **Git集成与合规：** **AI贡献归因**（PR #3115）持续吸引关注，表明企业和开源项目对追踪AI生成代码的需求日益增长。此外，`--json-schema`（PR #3598）支持结构化输出，也体现了对CI/CD和自动化流程的更高级功能需求。

### 6. 开发者痛点

- **终端/UI渲染问题：** 这是当前最突出的痛点。多个问题（#3213, #3838, #3824）都指向一个共同的根源：终端窗口大小调整（resize）会导致严重的UI错乱、闪烁和刷新循环，严重影响开发者在长对话和代码编辑场景下的体验。
- **会话与文件管理性能：** 在处理大文件或长时间运行的会话后，性能瓶颈显著。具体表现为**会话文件膨胀**导致`/resume`极慢（#3822），以及**自动内存查询**导致的无辜延迟（#3759在PR #3814中修复）。这反映了现有数据结构在处理大规模持续交互时的不足。
- **配置与兼容性问题：**
    - **配置文件被覆盖** (#3843) 是一个非常危险的痛点，给用户带来的信任打击极大。
    - **第三方模型兼容性**，特别是MiniMax等模型的`<think>`标签解析问题，给选择非Qwen模型的开发者造成了困扰，好在相关Bug（#3387, #3669）已在v0.15.6中通过PR #3677修复。
    - **IDE集成失败**，如Zed中的401错误（#3825）和Wayland下无法粘贴图片（#3829），凸显了在不同环境和平台下保持功能一致的挑战。

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*