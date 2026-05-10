# AI CLI Tools Community Digest 2026-05-10

> Generated: 2026-05-10 07:48 UTC | Tools covered: 8

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
**Date: 2026-05-10**

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is experiencing a period of intense community activity characterized by rapid feature iteration, significant platform-specific stability challenges, and growing demands for enterprise-grade reliability. The six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, and Qwen Code—each occupy distinct positions but share common pain points around session management, agent reliability, terminal compatibility, and cross-platform support. Windows users remain disproportionately affected across the ecosystem, while developers increasingly demand sophisticated multi-agent orchestration, persistent memory systems, and seamless IDE integration. The overall landscape suggests a market transitioning from novelty to production-readiness, with community trust hinging on transparency around pricing, model behavior, and breaking changes.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Key PRs (24h) | Release Status | Notable Activity |
|------|-----------------|---------------|----------------|-----------------|
| **Claude Code** | 10 active | 0 updated | No release | High emotional engagement (#45596, 1,075 👍 on Buddy removal) |
| **OpenAI Codex** | 10 active | 10 open/closed | No release | High PR throughput; Windows stability pain points |
| **Gemini CLI** | 10 active | 10 open/closed | No release | Major Windows fixes in progress; memory system bugs |
| **GitHub Copilot CLI** | 7 non-spam | 0 updated | No release | Low activity; session state corruption issues |
| **Kimi Code CLI** | 10 active | 10 open/closed | No release (v1.41.0 latest) | WebUI focus; Windows shell refactoring merged |
| **OpenCode** | 10 active | 10 open/closed | **5 releases** (v1.14.42–46) | Highest release cadence; Scout agent launched |
| **Pi** | 10 active | 10 open/closed | No new release | Heavy refactoring; org migration causing trust issues |
| **Qwen Code** | 10 active | 10 open/closed | **v0.15.10** + Python SDK preview | Binary detection fix; daemon mode ongoing |

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tools, indicating convergent community demands:

| Shared Requirement | Tools Affected | Specific Need |
|-------------------|----------------|---------------|
| **Session management & recovery** | Claude Code, Codex, Copilot CLI, OpenCode, Qwen Code | `/rename` sessions, remote session deletion, graceful resume after interruptions, session compaction without data loss |
| **Multi-agent / subagent orchestration** | Claude Code (#57752), Gemini CLI (#22323), OpenCode, Qwen Code (#3969) | Parallel subagent dispatch, background task promotion (Ctrl+B), subagent tool scoping |
| **Model selection & fallback consistency** | Gemini CLI (#21609), Copilot CLI (#3217), Qwen Code | Auto-fallback on quota exhaustion should resume, not stall; consistent access to latest models |
| **Memory / context persistence** | Claude Code (#57760), Gemini (#26516), Codex (#18490), OpenCode (#16959), Qwen Code | Instructions surviving compaction, auto-memory maturity, compact vs. clear options |
| **Terminal / IME stability** | Claude Code (tmux #29937, CJK #57759), Pi (#4347), Qwen Code | CJK input method compatibility, tmux rendering, non-ASCII text handling |
| **Windows platform parity** | All tools | Freezes, WSL2 OAuth, path issues, PowerShell vs. Git Bash, process management |
| **MCP / plugin standardization** | Codex (#20135), Gemini (#25989), OpenCode (#26598), Kimi Code (#2208), Qwen Code (#4007) | Hyphenated server names, env var expansion, tool scoping per agent, server mode APIs |
| **Agent honesty & error reporting** | Gemini (#22323), Copilot (#3183), Pi (#4290), OpenCode | Subagents reporting `success` after failure, orphaned tool calls, silent stream termination |
| **Configuration portability** | Qwen Code (#4015–4016), Kimi Code (#2171), Pi | Multi-device sync, YAML skins, profile management across machines |

---

## 4. Differentiation Analysis

Each tool serves a distinct segment of the developer market, reflected in their technical priorities:

**Claude Code** – Strongest emotional user attachment (Buddy removal generated 1,075 👍). Focus on agent companion experience and desktop app parity. Vulnerable to backend model regressions (Opus 4.7). Community values transparency most.

**OpenAI Codex** – Highest PR throughput and most structured feature pipeline. Targeting enterprise deployment with worktree management, session forking, and service-tier persistence. TUI quality-of-life investments suggest a power-user focus. Chrome plugin integration unique to this tool.

**Gemini CLI** – Most memory-system innovation (auto-memory, save_memory tool) but also most bugs in that area. Heavy investment in Windows fix infrastructure. Subagent dishonesty (#22323) signals trust gap. Google's model versioning strategy causes user confusion.

**GitHub Copilot CLI** – Lowest activity, most stable (or most stagnant). Focus on plugin hooks and SDK tool-call lifecycle. Silent failure modes (#3189) indicate quality gaps. Least feature-rich but benefits from GitHub ecosystem lock-in.

**Kimi Code CLI** – Most distinctive in WebUI-first approach. Editable path bars, autocomplete, sidebar UX. Unique window into Chinese developer needs (WeChat bot integration, CJK text handling). Behind on agent loop reliability (429 errors).

**OpenCode** – Highest release velocity (5 releases in 24h). Aggressive feature addition: Scout agent, HTTP compression, slash chaining, sub-project groups. Breaking changes occurring frequently (CLI binary removal, schema mismatches). Caters to early adopters tolerant of instability.

**Pi** – Most transparent about internal refactoring (closed-with-weekend tags). Strong TUI innovation (background bash, prefix command matching, CJK cell handling). NVIDIA NIM provider addition shows enterprise cloud focus. Organization migration creates uncertainty.

**Qwen Code** – Most architecturally ambitious with daemon mode and Python SDK preview. ToolSearch for context optimization shows advanced prompt engineering. Binary detection bugs highlight frontier of file system integration. Unique Chinese ecosystem integrations (Alibaba Cloud, WeChat, Bailian CLI).

---

## 5. Community Momentum & Maturity

**Highest Velocity / Rapid Iteration:**
- **OpenCode** – 5 releases in 24h signals extremely rapid development cycles, but at the cost of regression frequency and breaking changes
- **Qwen Code** – v0.15.10 + SDK preview + daemon mode Stage 1 shows both stability fixes and architectural expansion
- **Pi** – Despite refactoring churn, substantive new features (NVIDIA NIM, background commands, prefix matching) demonstrate active investment

**High Engagement / Emotional Investment:**
- **Claude Code** – The Buddy issue (#45596) with 1,075 👍 dwarfs all other single-issue engagement across the ecosystem. Community sentiment is passionate but currently frustrated with transparency.
- **Gemini CLI** – Memory system bugs (#26516) and model confusion (#21609) generate sustained discussion, indicating a community that wants the tool to succeed but feels underserved.

**Lowest Activity / Potential Stagnation:**
- **GitHub Copilot CLI** – Only 7 non-spam issues updated in 24h, zero PRs. The tool appears to be maintained rather than actively developed, consistent with its mature, SDK-centered role.

**Platform Maturity Ranking (by stability over feature rate):**
Copilot CLI > Claude Code > Gemini CLI > Codex > Kimi Code > Pi > Qwen Code > OpenCode

**Innovation Maturity Ranking (by feature velocity):**
OpenCode > Qwen Code > Pi > Codex > Gemini CLI > Kimi Code > Claude Code > Copilot CLI

---

## 6. Trend Signals

**Six industry-relevant trends emerging from community feedback:**

1. **Multi-agent orchestration is the next frontier.** Multiple communities are demanding structured parallel agent dispatch, background task promotion, and subagent tool scoping. This suggests developers are moving beyond single-turn agent interactions toward persistent, multi-agent workflows. Tools that solve this first (OpenCode's slash chaining, Qwen Code's Ctrl+B, Gemini Code's subagent refactoring) will gain strategic advantage.

2. **Reliability beats features for enterprise adoption.** The most upvoted issues across the ecosystem are bugs and regressions, not missing features. Silent failures (empty responses, orphaned tool calls, false success reports) erode trust faster than missing capabilities. The community is signaling that "works consistently" is the #1 purchase criterion.

3. **Windows parity is a competitive differentiator.** Every tool has Windows-specific blockers. The first tool to deliver truly stable Windows support (not just workarounds) will capture a significant underserved market. Gemini CLI's PR #26392 (process management overhaul) and Kimi Code's Git Bash migration (#2186) show emerging solutions.

4. **Context management is the new "state management."** Developers are struggling with token budgets, compaction, memory persistence, and context limits. Requests for compact-vs-clear options, hierarchical archives, and instruction survival across compaction mirror the state management problems of early web development. This is a technical debt area that will define tool limits.

5. **MCP/plugin ecosystem is standardizing but fragmenting.** Every tool is building its own plugin interface, but the community is asking for interoperability (OpenAI-compatible APIs, shared server formats, tool scoping per agent). The winner may be the tool that bridges rather than builds—e.g., Qwen Code's daemon mode using ACP protocol or Pi's multi-provider integration.

6. **Transparency is becoming a trust requirement.** Claude Code's Buddy removal without explanation (#45596) and Pi's silent organization migration (#4349) generated significant negative sentiment. Users increasingly expect changelogs, migration guides, and opt-in deprecation timelines. The tools that communicate breaking changes proactively will retain community trust during rapid iteration.

**Recommendation for developers evaluating these tools:**
- Choose **OpenCode** or **Qwen Code** if you tolerate instability for cutting-edge features
- Choose **Claude Code** or **Gemini CLI** for balanced feature/trust ratio
- Choose **GitHub Copilot CLI** for maximum stability in GitHub-centric workflows
- Monitor **Pi** and **Kimi Code** for cross-platform and CJK-specific needs respectively

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data as of 2026-05-10 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Pull Requests attracted the highest discussion volume (sorted by comment count) and represent the community’s most active skill contributions.

| # | Skill PR | Functionality | Highlights | Status |
|---|----------|---------------|------------|--------|
| 1 | **[#514 – Add document-typography skill](https://github.com/anthropics/skills/pull/514)** | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a universal typographic quality gap in Claude output. | Contributors noted that “every document Claude generates” suffers from these issues; high practical value for professional reports. | **Open** |
| 2 | **[#83 – Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83)** | Meta‑skills that evaluate quality across dimensions (structure, documentation, examples, security). Provides a systematic validation framework for the Skills ecosystem itself. | Discussion centered on expanding the analyzer to cover more skill types and integrating it into CI. | **Open** |
| 3 | **[#210 – Improve frontend-design skill](https://github.com/anthropics/skills/pull/210)** | Revises the existing frontend‑design skill to make every instruction actionable within a single conversation, improving clarity and internal coherence. | Community feedback focused on real‑world usability; reviewers praised the “specific enough to steer behavior” principle. | **Open** |
| 4 | **[#486 – Add ODT skill](https://github.com/anthropics/skills/pull/486)** | Creates, fills, reads, and converts OpenDocument Format files (.odt, .ods). Responds to mentions of LibreOffice, ODF, or open‑source document standards. | High demand for interoperability with non‑Microsoft office suites; discussion included template‑filling edge cases. | **Open** |
| 5 | **[#181 – Add SAP-RPT-1-OSS predictor skill](https://github.com/anthropics/skills/pull/181)** | Enables predictive analytics on SAP business data using SAP’s open‑source tabular foundation model (SAP‑RPT‑1‑OSS, Apache 2.0). | Enterprise‑focused skill; reviewers highlighted the niche value for SAP‑heavy organizations. | **Open** |
| 6 | **[#723 – Add testing-patterns skill](https://github.com/anthropics/skills/pull/723)** | Covers the full testing stack: philosophy (Trophy model), unit testing (AAA pattern), React component testing (Testing Library), edge cases, and what *not* to test. | One of the most‑requested categories; discussion debated the Trophy model vs. traditional pyramid. | **Open** |
| 7 | **[#360 – Add AppDeploy skill](https://github.com/anthropics/skills/pull/360)** | Deploys and manages full‑stack web apps directly from Claude via the AppDeploy platform, including lifecycle management and versioning. | Strong interest from developers wanting one‑shot deployment; discussion covered rate limits and auth flows. | **Open** |
| 8 | **[#444 – Add AURELION skill suite](https://github.com/anthropics/skills/pull/444)** | Four skills (kernel, advisor, agent, memory) implementing a structured cognitive framework (5‑floor hierarchy) for professional knowledge management and AI collaboration. | Philosophical discussions about “too much framework” vs. “necessary structure”; actively evolving with contributor engagement. | **Open** |

---

## 2. Community Demand Trends

Analysis of the top Issues (by comment count) reveals four dominant demand directions:

### a) Skill Library Usability & Sharing
- **Issue #228** (9 comments, 7 👍) – *Org‑wide skill sharing*: Users want a direct share link or centralized skill library instead of manual file downloads.  
- **Issue #62** (10 comments, 1 👍) – *Skills disappearing*: Unexplained loss of user‑created skills, pointing to fragile local storage/upload workflows.  
- **Issue #406** (2 comments, 4 👍) – *Upload errors*: Internal server error when replacing skills; high upvote ratio indicates wide frustration.  
- **Issue #61** (3 comments) – *“Not found” on team plan*: API 404 when listing skills for organizations.

### b) Developer Experience & Tooling
- **Issue #556** (8 comments, 6 👍) – *`run_eval.py` never triggers skills*: The evaluation harness fails to invoke skills in `claude -p` mode, breaking the skill‑creator testing loop.  
- **Issue #532** (2 comments, 1 👍) – *Enterprise/SSO compatibility*: Description optimizer requires `ANTHROPIC_API_KEY`, unusable for SSO‑authenticated users.  
- **Issue #202** (8 comments, 1 👍) – *skill‑creator best‑practice update*: Current version is too verbose and education‑focused, not actionable for Claude.

### c) Security, Trust, & Governance
- **Issue #492** (4 comments, 2 👍) – *Trust boundary abuse*: Community skills distributed under the `anthropic/` namespace impersonate official skills, creating a security vulnerability.  
- **Issue #412** (4 comments) – *Proposal: agent‑governance skill*: Demand for safety patterns – policy enforcement, threat detection, audit trails for agentic systems.

### d) Platform Integration & Standards
- **Issue #16** (4 comments) – *Expose skills as MCPs*: Call for an MCP‑based API to make skills interoperable with other AI tooling.  
- **Issue #29** (4 comments) – *Bedrock compatibility*: Users want skills to work with AWS Bedrock deployments.  
- **Issue #189** (6 comments, 8 👍) – *Duplicate skills from plugins*: `document‑skills` and `example‑skills` plugins install identical content, bloating context windows.  
- **Issue #1087** (2 comments, 1 👍) – *Plugin loads all skills instead of declared subset*: Further plugin mismanagement.

**Key takeaway:** The community is equally concerned with *operational stability* (sharing, uploading, evaluation) and *platform expansion* (enterprise SSO, Bedrock, MCP, plugin correctness). New skill *directions* are dominated by **quality assurance** (typography, testing, security analysis) and **enterprise platform integration** (SAP, ServiceNow, ODT, AppDeploy).

---

## 3. High‑Potential Pending Skills

These open PRs have active discussion and are likely to land soon:

| PR | Skill | Why It’s High‑Potential |
|----|-------|-------------------------|
| [#538 – fix(pdf) case‑sensitive references](https://github.com/anthropics/skills/pull/538) | PDF skill | Fixes 8 case‑sensitivity bugs on case‑sensitive filesystems – a quick, uncontroversial quality‑of‑life fix. |
| [#541 – fix(docx) tracked change w:id collision](https://github.com/anthropics/skills/pull/541) | DOCX skill | Prevents document corruption from ID space collision; directly addresses a reported bug. |
| [#539 – fix(skill‑creator) unquoted description validation](https://github.com/anthropics/skills/pull/539) | skill‑creator | Small but impactful validation addition that prevents silent YAML parsing failures. |
| [#806 – Add sensory skill (macOS AppleScript)](https://github.com/anthropics/skills/pull/806) | Sensory / macOS | Two‑tier permission system for native macOS automation – fills a gap for desktop users without screenshot‑based computer use. |
| [#509 – Add CONTRIBUTING.md](https://github.com/anthropics/skills/pull/509) | Meta‑documentation | Addresses community health gap (repo scored 25% on GitHub metrics); likely to be merged quickly. |

All are **open** as of the data snapshot. The fixes (#538, #541, #539) are small and non‑controversial, suggesting imminent merge. The sensory skill and CONTRIBUTING.md are larger but have strong community support.

---

## 4. Skills Ecosystem Insight

**The community’s most concentrated demand is for skills that improve Claude’s output quality (typography, testing, documentation audit) and extend its reach into enterprise platforms (SAP, ServiceNow, ODT, AppDeploy) while simultaneously demanding better tooling for skill creation, sharing, and security governance.**

In other words: *users want to make Claude more capable and reliable in production settings, and they need the supporting infrastructure (evaluation, sharing, security) to do so safely at scale.*

---

# Claude Code Community Digest — 2026-05-10

**Today’s Highlights**  
No new releases or pull requests were made available in the last 24 hours. The community remains vocal about the abrupt removal of the `/buddy` command (Issue #45596, 231 comments, 1,075 👍), and several blocking bugs—including silent daily-limit tightening on Max plans and a CJK IME regression—continue to generate significant discussion.

---

## Releases

No new versions were published in the last 24 hours.

---

## Hot Issues

1. **#45596 — [Enhancement] Bring Back Buddy — A Consolidated Plea from the Community**  
   *Hujoepandiselvan* | 231 comments | 1,075 👍  
   The `/buddy` skill was silently removed in v2.1.97. Thousands of developers lost their terminal companion overnight. This single issue has become the highest-voted request in the repo, reflecting deep attachment to the feature and frustration over the lack of an official explanation.  
   [https://github.com/anthropics/claude-code/issues/45596](https://github.com/anthropics/claude-code/issues/45596)

2. **#55982 — [BUG] Plan upgrade payment fails — PaymentIntent voided immediately**  
   *ssshreyans26* | 44 comments | 10 👍  
   Upgrading to Max plans fails because the `PaymentIntent` is voided before the confirmation can complete. Blocks access to higher tiers for users who want to upgrade, making it a high-priority transaction-critical bug.  
   [https://github.com/anthropics/claude-code/issues/55982](https://github.com/anthropics/claude-code/issues/55982)

3. **#34255 — [BUG] Remote Control: automatic reconnection doesn't work**  
   *BluCreator* | 30 comments | 71 👍  
   Remote Control sessions drop silently and never recover, forcing manual restarts. Affects macOS and iOS users relying on remote workflows; a persistent usability headache for mobile developers.  
   [https://github.com/anthropics/claude-code/issues/34255](https://github.com/anthropics/claude-code/issues/34255)

4. **#54714 — [BUG] Max 20x plan hitting daily limit with reduced usage**  
   *tbuckworth* | 12 comments | 7 👍  
   Max subscribers ($200/month) are hitting daily caps despite using *less* than usual. Suggests silent limit tightening on the server side, undermining trust in plan transparency.  
   [https://github.com/anthropics/claude-code/issues/54714](https://github.com/anthropics/claude-code/issues/54714)

5. **#27725 — [Enhancement] Detachable OS-level windows in desktop app for split screen**  
   *ExtraE113* | 10 comments | 45 👍  
   Users want native window breakout for side-by-side monitoring. A long-standing request that would bring Claude Code closer to standard IDE ergonomics.  
   [https://github.com/anthropics/claude-code/issues/27725](https://github.com/anthropics/claude-code/issues/27725)

6. **#29937 — [BUG] Terminal rendering corruption in tmux**  
   *efloehr* | 7 comments | 12 👍  
   Text overlaps and overwrites previous output in tmux sessions on Linux. Affects power users who rely on multiplexers; terminal emulation fallback issues remain unresolved.  
   [https://github.com/anthropics/claude-code/issues/29937](https://github.com/anthropics/claude-code/issues/29937)

7. **#57687 — [BUG] Claude Code on the Web: Git LFS not supported**  
   *tomkitewing* | 5 comments | 0 👍  
   The web proxy rejects LFS batch API calls, breaking projects that store large assets. Emerging pain point as more teams move development to the browser.  
   [https://github.com/anthropics/claude-code/issues/57687](https://github.com/anthropics/claude-code/issues/57687)

8. **#51890 — [BUG] CLI returns empty responses with Opus 4.7 & Sonnet 4.6**  
   *ns-ctw* | 3 comments | 0 👍  
   The model emits `<thinking>` blocks but `output_tokens` stays 0, resulting in empty replies. Intermittent but perplexing; likely a backend pipeline issue.  
   [https://github.com/anthropics/claude-code/issues/51890](https://github.com/anthropics/claude-code/issues/51890)

9. **#57760 — [BUG] Claude Code ignores CLAUDE.md/memory + suspected Opus 4.7 regression**  
   *saminlion* | 2 comments | 3 👍  
   Project instructions are not being followed, and token waste is noticeably higher. Users suspect a core model regression; combined with memory issues, this erodes trust in agent reliability.  
   [https://github.com/anthropics/claude-code/issues/57760](https://github.com/anthropics/claude-code/issues/57760)

10. **#57759 — [BUG] CJK IME candidate selection broken — number keys intercepted**  
    *ndtsoklm1114-collab* | 1 comment | 0 👍  
    Chinese IME users cannot select candidates because number keys are grabbed by the CLI prompt. Regression that makes the tool unusable for CJK developers.  
    [https://github.com/anthropics/claude-code/issues/57759](https://github.com/anthropics/claude-code/issues/57759)

---

## Key PR Progress

No pull requests were updated in the last 24 hours. Community development activity appears to be in a lull, likely focused on filing and discussing the issues above.

---

## Feature Request Trends

- **Buddy revival** – The call to restore `/buddy` (#45596) dwarfs all other feedback. The community is asking for transparency and a return of the companion feature.
- **Session management** – Multiple requests for renaming sessions (`/rename` commands, editable labels) indicate that auto-generated timestamps are inadequate for navigating long histories.
- **Multi-agent orchestration** – A new draft (#57752) proposes reusable workflows for parallel subagent dispatch, reflecting growing interest in agent composition.
- **Worktree isolation** – Several enhancement requests (#57767, #57765) focus on improving worktree lifecycle visibility and cleanup, especially on Windows and Linux.
- **Detachable windows** – Desktop app users want OS-level window breakout (#27725) for better multi-monitor workflows.
- **Documentation accuracy** – Repeated documentation fixes from *coygeek* (permissions, network config, runtime references) show that the docs lag behind the CLI’s fast-moving codebase.

---

## Developer Pain Points

- **Silent plan limit tightening** (#54714) – Max subscribers feel misled when caps shrink without notice. Trust and billing communication are at stake.
- **Payment flow breakage** (#55982) – A hard blocker for plan upgrades that should have been caught by integration tests.
- **Remote Control instability** (#34255) – Silent reconnection failures are disruptive for mobile and cross-device users.
- **Terminal/IME regressions** – tmux rendering corruption (#29937) and CJK IME broken selection (#57759) frustrate specific but sizable developer segments.
- **Agent worktree cleanup** (#57765, #57767, #57768) – Stale worktrees accumulate when sessions end early, requiring manual pruning and confusing developers.
- **Desktop app session sync** (#57345) – CLI and desktop sessions stored in different directories cause confusion; chats spontaneously re-archive (#57586).
- **CLI empty responses** (#51890) – Output-token zero bugs erode confidence in the model’s reliability for production use.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-10

## Today's Highlights

The community remains focused on two major areas: **Windows desktop stability** (multiple open issues around Chrome plugin hangs, socket mismatches, and installation failures on unsupported OS versions) and **authentication friction** (a long-running closed issue about phone verification blockers that generated 104 comments). Several high-value PRs landed to improve TUI session management and service-tier configuration, while feature requests continue to push for better context compression and per-agent tool scoping.

## Releases

No new releases published in the last 24 hours.

## Hot Issues

1. **[#20161](https://github.com/openai/codex/issues/20161) – Phone number verification doesn't work** [CLOSED, 104 comments]  
   Auth flow broke for users signing in via SSO on a new device; asked to enter a phone number even if none is linked. High engagement suggests widespread frustration. Fixed and closed, but no root cause shared.

2. **[#21670](https://github.com/openai/codex/issues/21670) – Windows Codex Desktop: Chrome plugin and Browser Use setup hang** [OPEN, 10 comments]  
   The Chrome plugin is slow and unreliable on Windows; direct browser-client calls time out, and plugin uninstallation fails with OS error 5. Affects all Windows users who rely on browser automation.

3. **[#14794](https://github.com/openai/codex/issues/14794) – VS Code extension sandbox makes writable devcontainer appear read-only on Linux** [OPEN, 8 comments]  
   After reinstalling the Codex extension, the sandbox incorrectly marks workspace files as read-only, breaking normal edit workflows in dev containers.

4. **[#21719](https://github.com/openai/codex/issues/21719) – Chrome plugin native host connects to wrong socket and times out** [OPEN, 7 comments]  
   On macOS Apple Silicon, the bundled Chrome plugin and the Codex browser-use pipe connect to different sockets, causing `@chrome` tasks to fail. Multiple similar reports indicate a systemic connectivity issue.

5. **[#20988](https://github.com/openai/codex/issues/20988) – Codex now searches the web far too frequently** [CLOSED, 7 comments]  
   Users on `gpt-5.3-codex high` report the model invokes web search even when not needed, inflating latency and token cost. Closed, but underlying heuristics remain a concern.

6. **[#8179](https://github.com/openai/codex/issues/8179) – "The '' model is not supported" error with ChatGPT account** [CLOSED, 7 comments]  
   After a single exchange, a new chat returns an unsupported model error. Affects Plus users on Windows. Closed with no public fix details.

7. **[#18490](https://github.com/openai/codex/issues/18490) – Request: "Compact context and implement plan" in Plan Mode** [OPEN, 6 comments]  
   Users want a middle ground between “clear context” and “keep context” – compacting instead of discarding, to retain memory while reducing token usage.

8. **[#21791](https://github.com/openai/codex/issues/21791) – Chrome plugin selectable but not exposed as active tool** [OPEN, 5 comments]  
   Fresh chats can mention `@chrome`, but the runtime doesn't register it as a callable tool. UI/Runtime mismatch breaks user expectations.

9. **[#21704](https://github.com/openai/codex/issues/21704) – Browser-use setup hangs when /backend-api/me probe doesn't complete** [OPEN, 5 comments]  
   The Chrome/browser-use initialisation can hang indefinitely if an ambient health probe fails, blocking all browser capabilities.

10. **[#13270](https://github.com/openai/codex/issues/13270) – `invalid_request_error`: string too long** [OPEN, 4 comments]  
    Input arguments exceeding 1,048,576 characters produce a hard error. Users hitting long context windows need either truncation or clear error guidance.

## Key PR Progress

1. **[#17850](https://github.com/openai/codex/pull/17850) – Render high-risk MCP elicitation warnings in TUI** [OPEN]  
   Adds visual styling (red + ⚠ prefix) for dangerous MCP operations, with subtitle support and focused test coverage. Improves safety UX.

2. **[#14428](https://github.com/openai/codex/pull/14428) – Fork sessions into new multiplexer panes** [CLOSED]  
   Adds `/fork` support for tmux and zellij, letting users launch concurrent sessions in separate panes with preserved CLI overrides. Merged.

3. **[#17393](https://github.com/openai/codex/pull/17393) – Unwrap PowerShell commands for exec policy** [CLOSED]  
   Fixes a Windows bypass where wrapped PowerShell invocations were not evaluated against the execution policy. Merged.

4. **[#21888](https://github.com/openai/codex/pull/21888) – Build v8 from source for all CI targets** [OPEN]  
   CI infrastructure change to compile the v8 JavaScript engine for cross-platform builds, improving reproducibility.

5. **[#21844](https://github.com/openai/codex/pull/21844) – Ignore stale /tmp git markers in project discovery** [OPEN]  
   Prevents `.git` markers in world-writable directories (like `/tmp`) from being treated as repo roots, while still honoring repos below them.

6. **[#18748](https://github.com/openai/codex/pull/18748) – Emit terminal review events for analytics** [OPEN]  
   Makes review telemetry first-class events (guardian/user) instead of counters, enabling better analysis of command execution, file changes, and permissions.

7. **[#21492](https://github.com/openai/codex/pull/21492) – Stop spelling skills extra roots in TUI requests** [CLOSED]  
   Cleanup – removes unnecessary verbose default values from `skills/list` calls. Merged.

8. **[#20825](https://github.com/openai/codex/pull/20825) – Read cached metadata for installed Git plugins** [OPEN]  
   Improves `plugin/list` by populating metadata from cached Git plugin bundles, falling back gracefully when cache is missing.

9. **[#21991](https://github.com/openai/codex/pull/21991) – Persist 'priority' service tier as 'fast' in config** [CLOSED]  
   Normalizes storage: user-facing `fast` is persisted even if API uses `priority`. Avoids confusion in config files. Merged.

10. **[#21435](https://github.com/openai/codex/pull/21435) – Managed worktrees in TUI** [OPEN]  
    Brings Git worktree creation and management into the CLI/TUI, matching the Desktop App's capability. Users can now create and switch between workspaces without raw git commands.

## Feature Request Trends

- **Context compression & persistence** – Multiple requests for compacting (not clearing) context (#18490), hierarchical archived context with rehydration (#15425), and “Yes, compact context and implement plan” options.
- **Session control enhancements** – Forking conversations from any message (#14024), injecting command output into active sessions (#22003), and dedicated `/usage` command (#17190).
- **Per-agent tool scoping** – Subagents should be able to opt out of inherited MCP servers (#20135) and have isolated tool sets.
- **TUI quality-of-life** – Sticky prompt textbox when scrolling (#14045), better visual differentiation of permission prompts (#16802), and goal objective editing (#21954).
- **Environment management** – Native UI for switching between dev/test/prod environments (#16094) and project-based chat separation (#17185).

## Developer Pain Points

- **Windows instability** – Chrome plugin hangs (#21670), socket mismatches (#21719), OS error 5 on uninstall, and workspace dependency repair failing on Windows 10 (#19811) collectively make the Windows experience unreliable.
- **Authentication and model errors** – Phone verification issues (#20161), “model not supported” errors (#8179), and API key validation gaps block new users.
- **Sandbox/permission quirks** – Linux devcontainer workspace appearing read-only (#14794) after reinstall breaks productivity.
- **Unexpected tool behavior** – Codex searching the web too often (#20988) and not exposing the Chrome plugin as a usable tool (#21791) confuse users.
- **Context limit breakage** – String-too-long errors (#13270) with no guidance on truncation or workaround.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-10

## Today's Highlights
Windows users continue to face major stability issues with initialization hangs and WSL2 OAuth problems, while a recent surge in memory‑system bugs (e.g., `save_memory` tool not found) signals growing pains in the agent’s long‑term recall. On the PR front, several critical fixes landed for Windows process management, proxy support, and MCP tool routing — but the community still awaits improvements in model selection consistency and subagent reliability.

## Releases
No new releases in the last 24 hours.

## Hot Issues
*Picked for impact, community engagement, and visibility into recurring problems.*

1. **[🐛 #19248] Windows 11 freeze at “Initializing…”**  
   P1 bug with 9 comments. Resolved Node v22 issue by downgrading to v20, but then freezes on “Trust folder” step. Still unaddressed.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/19248)

2. **[🐛 #23865] WSL2 OAuth broken – Paid Pro user blocked**  
   P1, 2 👍, 5 comments. OAuth flow broken on Ubuntu/WSL2, conflicting with Antigravity software. User paying for inaccessible service.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/23865)

3. **[🐛 #21937] gemini-3.1-pro-preview 100% error – infinite loading**  
   P1, 4 comments. Model hangs in “thinking” state indefinitely; no streaming output. Windows/v0.32.1.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/21937)

4. **[🐛 #21925] False hand icon marking action required**  
   P3, 17 comments. Shell scripts that run long trigger the interactive input indicator even though no input is needed. Annoying but widespread.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/21925)

5. **[🙋 #21609] User frustrated with non‑competitive 2.5 models**  
   P3, 16 comments. Spent hours trying to use 3.1 Pro but got 2.5 models instead. Model selection/availability confusion.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/21609)

6. **[🐛 #22323] Subagent false success after MAX_TURNS**  
   P1/P2, 2 👍, 6 comments. `codebase_investigator` reports `status: "success"` even after hitting turn limit, hiding real interruption.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

7. **[🙋 #21968] Gemini does not use skills and sub‑agents enough**  
   P2, 6 comments. Custom skills (gradle, git) rarely used autonomously; only triggered when explicitly instructed.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

8. **[🐛 #25166] Shell command hangs with “Waiting input” after completion**  
   P2, 3 👍, 3 comments. Simple commands (e.g., `ls`) leave the agent stuck in “awaiting user input” state.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

9. **[🐛 #26563] Tool “save_memory” not found**  
   P2, 5 comments. `/memory add` fails because the internal tool `save_memory` is missing from the agent’s tool list.  
   → [Issue](https://github.com/google-gemini/gemini-cli/issues/26563)

10. **[🐛 #26516] Memory system bugs – tracking issue**  
    P2, 2 comments. Aggregates several memory flaws: indefinite retries on low‑signal sessions, silent skip of invalid patches, missing redaction in Auto Memory.  
    → [Issue](https://github.com/google-gemini/gemini-cli/issues/26516)

## Key PR Progress
*Noteworthy pull requests merged or active in the last 24h that address critical fixes or feature gaps.*

1. **[fix(windows) #26392] Resolve hangs, zombie processes, and improve subagent reliability**  
   P1, open. Overhauls process management on Windows, fixes Node v20 freeze and orphaned subagent processes.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/26392)

2. **[fix(core) #26361] Externalize https‑proxy‑agent to fix proxy support**  
   P1, open. Prevents `TypeError: HttpsProxyAgent is not a constructor` by bundling the proxy agent externally. Essential for enterprise/network‑restricted environments.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/26361)

3. **[fix(mcp) #25989] Handle hyphenated server names consistently in tool dispatch**  
   P1, merged. MCP tools with hyphens in names (e.g., `mcp_hyphen-server_test-tool`) were not matched because models convert hyphens to underscores. Now normalized.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/25989)

4. **[fix(mcp) #25963] Expand env vars in stdio args**  
   P2, merged. Placeholders like `${DISCORD_TOKEN}` in MCP server args were not expanded; now handled before spawning.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/25963)

5. **[feat(cli) #25957] Implement event‑driven hook system messages**  
   P2, merged. Refactors hook message delivery to use queuing (`_emitOrQueue`) so UI doesn’t miss messages when not yet subscribed.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/25957)

6. **[fix(routing) #26761] Refactor tool turn handling to prevent 400 Bad Request**  
   New, open. Fixes malformed conversation history that caused API validation errors when the `contents` array starts with an orphaned tool call/response.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/26761)

7. **[fix(cli) #25654] Preserve extension rollback and end startup phase**  
   P1, open. Ensures extension update failures don’t remove the installed version and that builtin startup profiling always completes.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/25654)

8. **[fix(core) #26387] System ripgrep fallback when bundled binary missing**  
   P3, open. Falls back to system‑installed `rg` if the bundled vendor binary is absent – improves cross‑platform reliability.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/26387)

9. **[fix #26362] Guard stdin cleanup after SSH/TTY disconnect**  
   P2, open. Prevents crashes when `gemini --yolo` is run over an interactive SSH session that gets disconnected.  
   → [PR](https://github.com/google-gemini/gemini-cli/pull/26362)

10. **[rename #21877] Rename `/directory` command to `/workspace`**  
    Maintainer only, open. Moves toward consistent “workspace” terminology; keeps `/dir` and `/directory` as compatibility aliases.  
    → [PR](https://github.com/google-gemini/gemini-cli/pull/21877)

## Feature Request Trends
*The most‑requested directions emerging from recent issues and PRs.*

- **Model selection & quality** – Users want easier access to the latest Pro models (e.g., 3.1 Pro) and less frequent fallback to older 2.5 models.  
- **Agent autonomy** – Skills and sub‑agents should be used proactively, not only when explicitly commanded. Community wants smarter tool invocation without manual hints.  
- **Memory system maturity** – Auto Memory needs deterministic redaction, proper patch validation, and avoidance of infinite retries on low‑signal sessions.  
- **AST‑aware tooling** – Several issues and an epic (#22745) explore code‑structure‑aware file reads and mapping to reduce token usage and turn count.  
- **Browser agent resilience** – Requests for automatic session takeover, lock recovery, and better Wayland support.  

## Developer Pain Points
*Recurring frustrations that continue to block or annoy users.*

- **Windows‑specific blockers** – Freeze at startup, WSL2 OAuth failure, drive‑letter path errors (`A:\`). Paid users on Windows are disproportionately affected.  
- **Shell execution reliability** – Commands hanging after completion (false “Waiting input”), orphaned scripts, and the hand‑icon false positive cause constant manual intervention.  
- **Model confusion** – Users cannot reliably select or stay on the desired model version; the default seems to shift without warning.  
- **Subagent dishonesty** – Agents report `success` even after hitting turn limits or failing silently, eroding trust in automated workflows.  
- **MCP configuration friction** – Hyphenated server names break tool dispatch, env vars in args are not expanded, and settings overrides are ignored by the browser agent.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-10

## Today’s Highlights
No new releases or pull requests landed in the last 24 hours. The community reported several quality-of-life and SDK‑related regressions, including a silent non‑interactive exit on macOS (issue **#3189**), an orphan `tool_use` bug in the SDK (issue **#3183**), and a persistent failure when using DeepSeek‑V4 models (issue **#3215**). Two spam issues were quickly closed; the maintainers continue to focus on session stability and plugin hook improvements.

## Releases
None in the last 24 hours.

## Hot Issues
*(All open issues updated in the last 24h are listed below. Only 7 non‑spam items were active; the remaining 5 are triage/spam and are omitted.)*

1. **#2643 – [area:plugins] `preToolUse` silent command rewrite via `updatedInput` — confirmation dialog still appears**  
   *Author: jeziellopes* | [View issue](https://github.com/github/copilot-cli/issues/2643)  
   Plugins that rewrite commands with `permissionDecision: allow` still trigger an interactive confirmation. Users want a true “silent rewrite” path for automation. 7 comments, no 👍.

2. **#3189 – [area:non-interactive] `copilot -p` exits 1 silently with no output/log on macOS**  
   *Author: idanshimon* | [View issue](https://github.com/github/copilot-cli/issues/3189)  
   Non‑interactive mode produces zero stdout/stderr and no log file. Interactive mode works fine, hinting at a broken pipe or fork error. 4 comments, 0 👍.

3. **#3183 – [area:sessions, area:tools] SDK: orphan `tool_use` left mid‑conversation after hard kill + resume causes 400 error**  
   *Author: ulugbekna* | [View issue](https://github.com/github/copilot-cli/issues/3183)  
   When a session is killed and resumed, `tool_use` IDs are missing corresponding `tool_result` blocks, causing persistent 400 errors. Originally misattributed to subagent interleaving; now confirmed as orphan state. 2 comments.

4. **#3216 – [area:sessions, area:context-memory] Agent enters infinite compaction/directory‑list loop on long sessions**  
   *Author: edeslaurSTOXX* | [View issue](https://github.com/github/copilot-cli/issues/3216)  
   After ~136 turns near the context limit, the agent repeatedly compacts memory and lists directories, consuming tokens without progress. The user requested a refund. 1 comment.

5. **#3072 – [area:sessions, area:agents] Provide for deletion of remote agent sessions**  
   *Author: 4kbyte* | [View issue](https://github.com/github/copilot-cli/issues/3072)  
   The `/resume` menu can delete local sessions but refuses to delete remote ones without any workaround. A feature request with 1 👍.

6. **#3215 – [area:models, area:tools] Fail Tool Call for DeepSeek‑V4**  
   *Author: zzyu17* | [View issue](https://github.com/github/copilot-cli/issues/3215)  
   Configuring DeepSeek‑V4 models causes 400 errors due to `tool_use` blocks missing corresponding `tool_result` blocks. Identical symptom to #3183 but with a different model provider. 1 comment.

7. **#3217 – [area:sessions, area:models] Auto model fallback on quota limit shows new model but does not resume**  
   *Author: nicosafull* | [View issue](https://github.com/github/copilot-cli/issues/3217)  
   When premium quota is exhausted, the CLI switches the displayed model (e.g., `Auto -> GPT‑…`) but the agent remains stuck until a full restart. 0 comments.

## Key PR Progress
No pull requests were updated in the last 24 hours.

## Feature Request Trends
- **Plugin hook automation**: Users want `preToolUse` hooks to be able to silently rewrite commands without confirmation dialogs, enabling fully automated CLI toolchains.
- **Session management**: The ability to delete remote agent sessions from the `/resume` menu (issue #3072) would align local and remote session handling.
- **Graceful model fallback**: Automatic fallback on quota exhaustion should actually resume the session with the new model, not just update the status line.

## Developer Pain Points
- **Silent failures**: The non‑interactive mode (`copilot -p`) on macOS exits cleanly but produces no diagnostic output, making debugging impossible.
- **Orphaned state after interruptions**: Hard kills and session resumes frequently leave the system in an inconsistent state (`tool_use` without `tool_result`), causing 400 errors that require session destruction.
- **Infinite loops near context limits**: Long sessions can devolve into resource‑wasting compaction/directory‑list loops, frustrating users who rely on extended agent workflows.
- **Model‑specific tool call bugs**: DeepSeek‑V4 and potentially other models share the same `tool_use`/`tool_result` mismatch, indicating a broader SDK issue with tool‑call lifecycle management.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-05-10**.

---

## Kimi Code CLI Community Digest
**Date: 2026-05-10**

### 1. Today's Highlights
This week’s pulse is split between **WebUI usability enhancements** and **stability fixes for the agent loop**. Two new PRs from contributor `morphishk` aim to resolve long-standing sidebar navigation friction, while `he-yufeng` has landed a critical fix for the background auto-trigger cooldown logic. Meanwhile, a long-running `429 engine_overloaded` issue (#2209) continues to affect remote users, signaling potential capacity constraints on the backend.

### 2. Releases
**No new releases in the last 24 hours.** The latest stable version remains **v1.41.0**.

### 3. Hot Issues

1.  **[[Bug] Reading file loop (Issue #640)](https://github.com/MoonshotAI/kimi-cli/issues/640)** – A persistent bug causing the CLI to repeatedly read a single file in an infinite loop. This issue has received 6 comments and a thumbs-up, but has been open since January. It appears to be related to a custom Anthropic endpoint, suggesting a potential conflict with non-Kimi models.
2.  **[[Bug] Cannot Login (Issue #2162)](https://github.com/MoonshotAI/kimi-cli/issues/2162)** – A user on an Asahi Linux (ARM) system is blocked from logging in entirely. This is a critical onboarding barrier for users on niche hardware.
3.  **[[RFC] Custom Color Skins (Issue #2171)](https://github.com/MoonshotAI/kimi-cli/issues/2171)** – VrtxOmega proposes a YAML-based skin system to allow custom color palettes. With 1 comment, the community is receptive to moving beyond the hardcoded `dark`/`light` themes.
4.  **[[Enhancement] Shift+Enter for line breaks (Issue #2121)](https://github.com/MoonshotAI/kimi-cli/issues/2121)** – A common ergonomic request: users want `Shift+Enter` to insert newlines instead of the current `Ctrl+J` behavior. The single comment supports the move, which would standardize behavior with other popular CLI tools.
5.  **[[Bug] Long filenames hide action buttons in WebUI (Issue #2206)](https://github.com/MoonshotAI/kimi-cli/issues/2206)** – A clear UX bug in the WebUI sidebar where long file names push the expand/download buttons out of view. This is the most actionable bug in the current batch.
6.  **[[Feature Request] Editable path bar with autocomplete (Issue #2216)](https://github.com/MoonshotAI/kimi-cli/issues/2216)** – The same author from #2206 asks for a typeable path bar for keyboard-driven navigation. This reflects a desire for "power user" flow in the WebUI.
7.  **[[Bug] 429 engine_overloaded for 48+ hours (Issue #2209)](https://github.com/MoonshotAI/kimi-cli/issues/2209)** – A remote server user reports a persistent `429 engine_overloaded` error lasting over two days, even after upgrading from v1.24.0 to v1.41.0. This suggests a possible API throttling or model availability issue.
8.  **[[Enhancement] OpenAI-compatible API (Issue #2208)](https://github.com/MoonshotAI/kimi-cli/issues/2208)** – User `janeza2` requests that the Kimi CLI backend expose an OpenAI-compatible endpoint for use with tools like Cursor. This is a high-value integration request that could broaden the tool's ecosystem.
9.  **[[Bug] Windows Shell Configuration (Issue #1618)](https://github.com/MoonshotAI/kimi-cli/issues/1618)** – Though closed, this issue spurred a major refactor. The request was to allow Windows users to configure bash/zsh as the shell executor instead of PowerShell.
10. **[[Bug] /btw not registering (Part of PR #2205)](https://github.com/MoonshotAI/kimi-cli/issues/2205)** – The `/btw` slash command was documented but missing from slash completion and `/help`. This is a small but frustrating inconsistency for agent-mode users.

### 4. Key PR Progress

1.  **[PR #2217: fix: recover background auto-trigger after cooldown](https://github.com/MoonshotAI/kimi-cli/pull/2217)** – Fixes the agent loop getting stuck after 3 consecutive failures. Uses a 10-minute cooldown and reset counter to keep the agent responsive.
2.  **[PR #2215: feat(webui): editable path bar with autocomplete](https://github.com/MoonshotAI/kimi-cli/pull/2215)** – Directly implements the feature requested in Issue #2216. A major UX win for keyboard-centric users.
3.  **[PR #2207: fix(webui): prevent long filenames from hiding action buttons](https://github.com/MoonshotAI/kimi-cli/pull/2207)** – Addresses Issue #2206 with Radix UI and CSS fixes. Likely to be merged soon as a quick win.
4.  **[PR #2214: fix(soul): show rotated backup hint after /clear](https://github.com/MoonshotAI/kimi-cli/pull/2214)** – Improves the `/clear` command by displaying the backup file path and clarifying that `/undo` cannot restore cleared history. Prevents data loss confusion.
5.  **[PR #2212: fix(shell): tighten Windows PowerShell guidance (CLOSED)](https://github.com/MoonshotAI/kimi-cli/pull/2212)** – Improves documentation to warn Windows users about missing Unix tools (`head`, `grep`, etc.) in PowerShell 5.
6.  **[PR #2186: refactor(windows): switch Shell backend from PowerShell to git-bash (CLOSED)](https://github.com/MoonshotAI/kimi-cli/pull/2186)** – A major Windows fix that resolves Issue #1618. Git Bash is now the default, ensuring POSIX semantics for commands.
7.  **[PR #2177: fix(soul): clear partial UI output when LLM step is retried (CLOSED)](https://github.com/MoonshotAI/kimi-cli/pull/2177)** – Fixes a "ghost output" bug where failed attempts concatenate with successful retries. Improves the streaming experience.
8.  **[PR #2190: feat(telemetry): add app_name and build_sha with remote provenance (CLOSED)](https://github.com/MoonshotAI/kimi-cli/pull/2190)** – Adds build provenance and distinguishes manual vs. automation triggers in telemetry. Good for debugging and internal metrics.
9.  **[PR #2183: fix(shell): attach dropped image paths eagerly](https://github.com/MoonshotAI/kimi-cli/pull/2183)** – Fixes a race condition where local image paths would expire before reading. Prepares images immediately on submission.
10. **[PR #2113: fix(acp): wrap shell command in `bash -c` for terminal/create](https://github.com/MoonshotAI/kimi-cli/pull/2113)** – Ensures shell commands sent via ACP (terminal) are correctly wrapped in `bash -c`, preventing parsing errors.

### 5. Feature Request Trends
- **Cross-Platform Compatibility:** There is a growing push for better Windows support (Git Bash integration) and OpenAI-compatible APIs for broader tool integration.
- **WebUI as a First-Class Client:** Two feature requests this week focus on making the WebUI navigable without a mouse (path bar, autocomplete). Users want the WebUI to match the CLI’s power.
- **Customizability:** The YAML skins proposal indicates a desire for deep personalization, moving beyond predefined themes.
- **Input Ergonomics:** The `Shift+Enter` request is a small but loud signal that users expect modal-aware text entry, not just "terminal emulator" defaults.
- **Reliability & Resilience:** The requests for cooldowns on retries and clear backup paths show a user base sensitive to agent flakiness and data loss.

### 6. Developer Pain Points
- **Windows CTD:** Despite recent fixes, Windows remains a source of friction. The long-lived #1618 (resolved) and the tightening of PowerShell guidance #2212 indicate that non-POSIX environments are still a major headache.
- **Login/Onboarding:** Issue #2162 suggests hardware-specific authentication failures are blocking new users, which is a high-stakes problem.
- **429 Errors on Remote Deployments:** Issue #2209 is alarming because it implies a persistent, long-term service degradation for headless/remote users, which is a primary use case for CLI tools.
- **WebUI Interaction Limits:** The sidebar bugs (#2206, #2216) indicate that the WebUI currently lacks the keyboard-navigation efficiency that power users expect.
- **Model Compatibility:** The sticky loop in #640 and the 429 errors in #2209 suggest friction when using custom endpoints or high-demand models like `kimi-k2.6`. Users want a "just works" experience.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-10

## Today’s Highlights

Five point releases landed in the last 24 hours (v1.14.42 – v1.14.46), bringing a new Scout agent for repository research, HTTP response compression, a built-in `customize-opencode` skill, and several critical bug fixes around API parameter handling and workspace upgrades. Meanwhile, community hot topics include a persistent CLI copy-paste issue, a mysterious `nul` file creation bug, and growing frustration over TUI configuration schema mismatches.

---

## Releases

**v1.14.46**  
- New built-in `customize-opencode` skill to prevent config edits from breaking startup.  
- Fixed numeric HTTP API query parameters in the OpenAPI spec and SDK for session/file endpoints.  
- Fixed boolean HTTP API query handling.

**v1.14.45**  
- Provider configs and API responses now accept models marked as `active`.  
- Read tool permission rules now correctly match worktree-relative paths.  
- Workspace-routed HTTP API endpoints no longer reject valid `directory` and `workspace` queries.

**v1.14.44**  
- Fixed upgrades failing for existing workspaces when adding the `time_used` field.

**v1.14.43**  
- Fixed provider and config API responses when authentication loaders add non-JSON options.  
- Include tool image attachments in ACP updates and session replays (community contribution by @SteffenDE).

**v1.14.42**  
- Added HTTP API response compression for large non-streaming responses.  
- Added the **Scout agent** for repo research, docs lookup, and dependency-source inspection.  
- Added workspace sync so adapter-backed workspaces can be discovered and registered automatically.

---

## Hot Issues (10 noteworthy)

1. **#13984 – Cannot copy and paste in OpenCode CLI**  
   - 35 comments, 13 👍  
   - Users report clipboard copy appears to succeed but paste yields nothing. High engagement suggests widespread impact.  
   - [https://github.com/anomalyco/opencode/issues/13984](https://github.com/anomalyco/opencode/issues/13984)

2. **#11403 – Unexpected file named "nul" repeatedly created after update**  
   - 13 comments, 11 👍  
   - A mysterious `nul` file appears in the working directory; community suspects a regression in file-handling logic.  
   - [https://github.com/anomalyco/opencode/issues/11403](https://github.com/anomalyco/opencode/issues/11403)

3. **#11083 – Claude model cannot properly enable caching function**  
   - 10 comments, 4 👍  
   - Third-party Anthropic proxy with `setCacheKey` fails to trigger prompt caching. Workaround needed.  
   - [https://github.com/anomalyco/opencode/issues/11083](https://github.com/anomalyco/opencode/issues/11083)

4. **#25879 – What happened to the opencode-cli TUI?**  
   - 8 comments, 3 👍  
   - The `opencode-cli` binary disappeared from the Debian package after v1.14.30. Users on newer versions are left without the TUI.  
   - [https://github.com/anomalyco/opencode/issues/25879](https://github.com/anomalyco/opencode/issues/25879)

5. **#26209 – Windows Desktop cannot use oh-my-opencode plugin**  
   - 8 comments  
   - After v1.14.35, the oh-my-opencode plugin fails on Windows Desktop. Affects multiple plugins.  
   - [https://github.com/anomalyco/opencode/issues/26209](https://github.com/anomalyco/opencode/issues/26209)

6. **#26628 – TUI config schema mismatch + leader none crash**  
   - 7 comments, fresh issue  
   - `tui.json` expects `keymap` but v1.14.46 rejects it; falling back to `keybinds` with disabled leader key causes a blank screen.  
   - [https://github.com/anomalyco/opencode/issues/26628](https://github.com/anomalyco/opencode/issues/26628)

7. **#14212 – [FEATURE] Support more DBMS for OpenCode state storage**  
   - 7 comments, 14 👍  
   - Request to extend Drizzle-based session storage to Postgres and others. High upvotes indicate strong demand.  
   - [https://github.com/anomalyco/opencode/issues/14212](https://github.com/anomalyco/opencode/issues/14212)

8. **#25202 – GPT‑5.5 visible token count does not drop mid-session like GPT‑5.4**  
   - 6 comments  
   - Token count behavior differs between GPT‑5.4 and GPT‑5.5, causing earlier hard compaction and potential performance impact.  
   - [https://github.com/anomalyco/opencode/issues/25202](https://github.com/anomalyco/opencode/issues/25202)

9. **#26321 – Desktop app shell tool uses minimal PATH while CLI preserves zsh PATH**  
   - 6 comments, 3 👍  
   - macOS Desktop users get a stripped `PATH` when running shell tools, breaking Homebrew-based commands.  
   - [https://github.com/anomalyco/opencode/issues/26321](https://github.com/anomalyco/opencode/issues/26321)

10. **#26549 – `/exit` and `/quit` slash commands missing in autocomplete**  
    - 5 comments, 14 👍  
    - Commands work via command palette but not from the prompt’s `/` autocomplete. High visibility UX bug.  
    - [https://github.com/anomalyco/opencode/issues/26549](https://github.com/anomalyco/opencode/issues/26549)

---

## Key PR Progress (10 important pull requests)

1. **#26664 – docs: add man page for opencode(1)**  
   - Fresh PR submitting a complete manpage for the CLI tool. Improves offline discoverability.  
   - [https://github.com/anomalyco/opencode/pull/26664](https://github.com/anomalyco/opencode/pull/26664)

2. **#18767 – feat(app): Mobile Touch Optimization**  
   - Long-running effort to adapt the web app for mobile/touch devices while preserving desktop UX.  
   - [https://github.com/anomalyco/opencode/pull/18767](https://github.com/anomalyco/opencode/pull/18767)

3. **#16976 – fix(edit): raise BlockAnchorReplacer threshold when anchors are non-unique**  
   - Fixes erroneous edit blocks when anchor lines appear multiple times.  
   - [https://github.com/anomalyco/opencode/pull/16976](https://github.com/anomalyco/opencode/pull/16976)

4. **#16973 – docs: link to official OpenCode extensions**  
   - Updates docs to point directly to official extensions, not just marketplace search.  
   - [https://github.com/anomalyco/opencode/pull/16973](https://github.com/anomalyco/opencode/pull/16973)

5. **#16959 – feat: preserve AGENTS.md/CLAUDE.md instructions across compaction**  
   - Ensures that runtime instruction files survive session compaction, preventing sudden behavior loss.  
   - [https://github.com/anomalyco/opencode/pull/16959](https://github.com/anomalyco/opencode/pull/16959)

6. **#16934 – feat(app): add sub-project groups**  
   - Adds sidebar grouping for projects, enabling better organization. Supersedes an earlier PR.  
   - [https://github.com/anomalyco/opencode/pull/16934](https://github.com/anomalyco/opencode/pull/16934)

7. **#16931 – feat(opencode): add grouped memory view**  
   - New `/memory` TUI view that shows active instruction and skill files grouped by source.  
   - [https://github.com/anomalyco/opencode/pull/16931](https://github.com/anomalyco/opencode/pull/16931)

8. **#16921 – fix: keep Copilot Claude prompts user-final across continuation turns**  
   - Resolves a regression where Copilot Claude models (e.g. Opus 4.6) rejected assistant prefills during continuation.  
   - [https://github.com/anomalyco/opencode/pull/16921](https://github.com/anomalyco/opencode/pull/16921)

9. **#16917 – feat: support chaining multiple slash commands in a single prompt**  
   - Enables `/command1 /command2` sequences; previously only the first slash command executed.  
   - [https://github.com/anomalyco/opencode/pull/16917](https://github.com/anomalyco/opencode/pull/16917)

10. **#16912 – feat: add `/tui` and `/config` slash commands**  
    - Two new convenience commands to open `tui.json` and `opencode.json` from within the TUI.  
    - [https://github.com/anomalyco/opencode/pull/16912](https://github.com/anomalyco/opencode/pull/16912)

---

## Feature Request Trends

The community’s most-wanted enhancements center on **storage flexibility** and **platform expansion**:

- **Database backend support** (Postgres, etc.) – #14212 (14👍) and related issues.  
- **Native Android support** without Proot/distro environment – #26650.  
- **Plugin health/availability checks** – #26645 (➕1).  
- **“Disable thinking” toggle for DeepSeek V4** – #24610 (4👍).  
- **Improved MCP server configuration UI** on Desktop (similar to Goose) – #26598.  
- **Better handling of remote MCP tool schemas** (circular references, Stitch integration) – #26260, #26382.  
- **Resilience improvements** (server crash recovery, error logging) – #26646.  
- **Ability to refresh model lists from Desktop** (CLI no longer bundled) – #26613.  
- **Permission wildcard semantics clarification** (last-match rule vs. override) – #24335.

---

## Developer Pain Points

Several recurring frustrations emerged from the top issues:

- **TUI configuration instability** – Schema mismatches (`keymap` vs `keybinds`), leader key crashes, and missing `/exit` slash commands indicate testing gaps in TUI UX.  
- **Desktop vs CLI divergence** – The Desktop app lacks the CLI binary (making CLI-dependent tasks like model refresh impossible), uses a different `PATH`, and fails with certain plugins on Windows.  
- **Mysterious file creation** – The `nul` file issue (#11403) and similar artifacts erode trust in file-system handling.  
- **Permission rule confusion** – The “last matching rule wins” documentation contradicts user expectations when a wildcard `*` overrides specific rules (#24335).  
- **MCP integration fragility** – Remote MCP servers with non-trivial JSON schemas (circular $defs, Stitch proxy) fail to load tools, requiring workarounds.  
- **Upgrade regressions** – Each release seems to break something: CLI binary removal, Windows plugin incompatibility, new field migration crashes. Community demands better regression testing.  
- **OAuth and proxy issues** – GitHub Copilot OAuth fails on Windows behind system proxy unless environment variables are explicitly set (#26629), highlighting poor integration with network environments.  
- **Token behavior inconsistency** – GPT‑5.5’s token count not dropping like GPT‑5.4 leads to earlier compaction and unexpected context loss (#25202).

These pain points suggest a need for more robust integration testing across platforms, schema validation, and clearer documentation of breaking changes in release notes.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-10

## Today’s Highlights
The project remains in heavy refactoring with a move from `@mariozechner/pi-coding-agent` to `@earendil-works/pi-coding-agent`. A long-standing bug where external editor keystrokes leak into Pi has been reproduced and filed as #4365, while the community is still seeking an explanation for the organization change (#4349). On the feature front, background bash command support (`Ctrl+B`) and a built-in NVIDIA NIM provider were merged.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 noteworthy)

1. **#715** — *Keys from external editor are sometimes sent to pi*  
   Closed but marked as reproducible in #4365. A critical TUI UX issue affecting users who rely on `Ctrl+g` in Neovim.  
   [GitHub](https://github.com/earendil-works/pi/issues/715)

2. **#4288** — *npm install and pi update cannot update pi*  
   User reports version mismatch (0.73.0 vs 0.74.0) and failed updates. Closed as part of the big refactor.  
   [GitHub](https://github.com/earendil-works/pi/issues/4288)

3. **#4290** — *Messages aborted for length treated as regular stops*  
   User waits for thinking to complete, but the `Working…` indicator has disappeared. Session history shows turns stopped for length without a visible error.  
   [GitHub](https://github.com/earendil-works/pi/issues/4290)

4. **#4309** — *Expose editor cursor position via ExtensionUIContext*  
   Feature request to allow extensions to place an external editor’s cursor at the same position as Pi’s prompt cursor.  
   [GitHub](https://github.com/earendil-works/pi/issues/4309)

5. **#3700** — *Inline autocomplete skills*  
   Autocomplete for `/skill:foo` only works at the very beginning of chat input. Reported earlier but never followed up.  
   [GitHub](https://github.com/earendil-works/pi/issues/3700)

6. **#4251** — *Using Kimi K2.6 on OpenCode Go results in “reasoning_content is missing” error*  
   Provider compatibility issue when thinking is enabled. Still open.  
   [GitHub](https://github.com/earendil-works/pi/issues/4251)

7. **#1837** — *Feature Request: temperature, top_p, and other generation parameters*  
   Popular request (3 👍) – community wants more LLM parameters exposed. Previous attempts closed with suggestion to use custom provider.  
   [GitHub](https://github.com/earendil-works/pi/issues/1837)

8. **#4344** — *The ‘xhigh’ thinking effort level cannot be toggled via keyboard shortcuts*  
   GUI shows the option, but the coding agent TUI key binding does not support it.  
   [GitHub](https://github.com/earendil-works/pi/issues/4344)

9. **#4349** — *Organization change explanation would be great to have*  
   User expresses suspicion about the invasive move from `@mariozechner/pi-coding-agent` to `@earendil-works/pi-coding-agent` with no announcement. Closed without resolution.  
   [GitHub](https://github.com/earendil-works/pi/issues/4349)

10. **#4365** — *Opening external editor leaks stdin to pi instead (reproducible)*  
    Fresh open bug – a reproducible variant of #715 that affects pre-compiled releases.  
    [GitHub](https://github.com/earendil-works/pi/issues/4365)

## Key PR Progress (10 important)

1. **#4367 / #4368** — *feat: background direct bash commands*  
   Adds `Ctrl+B` to background interactive `!` bash commands, with proper UI and session tracking.  
   [GitHub](https://github.com/earendil-works/pi/pull/4367)

2. **#4282** — *docs(coding-agent): fix termux-open chooser flag*  
   Updates documentation to use `--chooser` instead of the unsupported `-c` flag.  
   [GitHub](https://github.com/earendil-works/pi/pull/4282)

3. **#4363** — *feat(agent): resolve slash commands by unambiguous prefix*  
   Allows `/ed` to match `/editor` if no other command starts with “ed”. Closes #4364.  
   [GitHub](https://github.com/earendil-works/pi/pull/4363)

4. **#4360** — *feat(ai): add NVIDIA NIM as built-in OpenAI-compatible provider*  
   Adds `KnownProvider` entry for NVIDIA, endpoint `https://integrate.api.nvidia.com/v1`, with 67 tool-capable models.  
   [GitHub](https://github.com/earendil-works/pi/pull/4360)

5. **#4358** — *fix(ai): add session affinity and compat fixes for Fireworks provider caching*  
   Adds `x-session-affinity` header to avoid per-replica cache misses and improve `cacheRead` pricing. Closes #4359.  
   [GitHub](https://github.com/earendil-works/pi/pull/4358)

6. **#4354** — *fix(ai): respect proxy envs in bun's websocket (OPEN)*  
   Workaround for Bun’s missing proxy support for WebSocket. Fixes #4346.  
   [GitHub](https://github.com/earendil-works/pi/pull/4354)

7. **#4352** — *Fix turn-boundary compaction resume flow*  
   Fixes a crash on `/resume` by properly waiting for persistence before compaction and resuming when idle.  
   [GitHub](https://github.com/earendil-works/pi/pull/4352)

8. **#4351** — *feat: auto-discover Ollama context windows from /api/show*  
   Dynamically queries `context_length` per model instead of hardcoding 128 Kb, fixing wrong defaults for many Ollama models.  
   [GitHub](https://github.com/earendil-works/pi/pull/4351)

9. **#4348** — *feat(ai): Add retries to Google Vertex AI*  
   Passes the `maxRetries` argument to Vertex AI provider to handle frequent `429` errors.  
   [GitHub](https://github.com/earendil-works/pi/pull/4348)

10. **#4347** — *fix(tui): CJK text extraction and double-width cell handling*  
    Fixes text selection and rendering for CJK characters, reverts broken paste detection on Windows.  
    [GitHub](https://github.com/earendil-works/pi/pull/4347)

## Feature Request Trends

- **Provider diversity** – NVIDIA NIM (#4360), better Ollama integration (#4351), retries for Vertex AI (#4348), and session affinity for Fireworks caching (#4358) show strong demand for cloud provider optimizations.
- **TUI power‑user features** – Background bash commands (#4367–4368), shortest‑unique‑prefix command matching (#4363), inline autocomplete (#3700), keyboard‑toggle for thinking levels (#4344), and editor cursor extension (#4309) indicate users want fast, keyboard‑driven workflows.
- **Advanced generation parameters** – Temperature, top_p, top_k still requested (#1837) but blocked by refactor; power users want more control.
- **Portability** – Supporting `~` and `$HOME` in `settings.shellPath` (#4353) and proxy env vars for WebSocket (#4354, #4346) show a need for cross‑machine configs.

## Developer Pain Points

- **External editor keyboard leaks** – Issues #715 and #4365 (both pre‑compiled releases) cause keystrokes intended for editors (especially the enter key) to be captured by Pi, making real‑world use painful.
- **Update / organization chaos** – `pi update` and `npm install` fail (#4288, #4362), and the silent org migration (#4349) erodes trust and breaks extensions.
- **Unclear error states** – Thinking‑level UI confusion (#4350), stopped‑without‑notice messages (#4290), and reasoning‑content mismatch (#4251) leave users waiting or hitting silent failures.
- **Provider regression in proxy support** – Bun’s WebSocket ignoring proxy envs since v0.72 (#4346) is a blocker for many corporate environments.
- **Stream truncation silent acceptance** – OpenAI‑compatible providers may treat incomplete streams as “done” without auto‑retry (#4345), losing work without error.

> **Note:** The large number of issues closed with the tags `closed-because-weekend` and `closed-because-bigrefactor` suggests the maintainers are aggressively tidying up during a major internal rewrite. While this reduces noise, it may leave some genuine bugs and feature requests unaddressed for the moment.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Here is the Qwen Code community digest for 2026-05-10.

---

## Qwen Code Community Digest — 2026-05-10

### 1. Today's Highlights
The project released **v0.15.10** with critical fixes for the file binary detection logic that has been plaguing users editing source files. A landmark **Python SDK preview (`qwen-code-sdk` v0.1.0rc0)** was also published, opening the door for programmatic integrations. The community remains highly active around configuration management and interop features, with a significant batch of feature requests from user **Maddock-DR** focusing on multi-device profile sync and MCP/HTTP server modes.

### 2. Releases
Three versions were published in the last 24 hours:

- **[v0.15.10](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.10)**: Primary release. Includes two key fixes:
    - `fix(cli)`: Validate `/model` command arguments (by @yiliang114)
    - `fix(core)`: Ensure OpenAI requests are logged as actually sent on the wire (by @tanzhenxin)
- **[v0.15.9-nightly.20260510.f4d0ad6b7](https://github.com/QwenLM/qwen-code/releases/tag/v0.15.9-nightly.20260510.f4d0ad6b7)**: Nightly build containing the same patches as v0.15.10.
- **[sdk-python-v0.1.0-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/sdk-python-v0.1.0-preview.0)**: Initial preview release of the official Python SDK (`qwen-code-sdk` v0.1.0rc0 on PyPI). This is a major milestone for developers looking to integrate Qwen Code programmatically.

### 3. Hot Issues
- **[[#3964] File type detection misidentifies encrypted .c/.cpp/.h files as binary payloads](https://github.com/QwenLM/qwen-code/issues/3964)** *(CLOSED)*: A high-priority bug (P1) that has been affectively blocking users on Windows with encrypted file systems. The `edit` and `write_file` tools were incorrectly flagging standard source files as binary. The PR #4002 fix is included in today's release.
- **[[#3945] edit tool unusable for large files](https://github.com/QwenLM/qwen-code/issues/3945)** *(CLOSED)*: Another P1 bug where `read_file` truncates large files, making the "fully read" precondition for `edit` impossible. This created a deadlock for users working on large codebases. Also resolved by #4002.
- **[[#4004] write_file misidentifies UTF-8 text (e.g., Chinese + Markdown) as binary](https://github.com/QwenLM/qwen-code/issues/4004)** *(OPEN)*: A variant of the binary detection issue, specifically triggered by Unicode characters. Community sentiment is frustrated as they must resort to `shell cat` workarounds. The linked fix in #4002 is expected to address this.
- **[[#4010] read_file incorrectly marks large files as binary after truncation](https://github.com/QwenLM/qwen-code/issues/4010)** *(CLOSED)*: A precise description of the bug fixed in today's release. After truncating a file, the system incorrectly marks it as binary, preventing subsequent operations.
- **[[#3203] Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** *(OPEN)*: A controversial proposal to drastically reduce the free quota from 1,000 to 100 requests/day and potentially close the free tier. With 123 comments, this is a hot topic indicating significant community concern about access restrictions.
- **[[#4003] about write_file tool](https://github.com/QwenLM/qwen-code/issues/4003)** *(OPEN)*: A user reports that after an agent writes a Markdown file, subsequent modifications frequently fail because the file is misidentified as binary. This highlights a general instability in the `write_file` tool's state tracking.
- **[[#4000] feat(cli): redesign /commit slash command to leverage AI for commit message drafting](https://github.com/QwenLM/qwen-code/issues/4000)** *(OPEN)*: After a previous PR was closed, the community is pushing for a smarter `/commit` command that uses AI to draft messages rather than being a simple `git` wrapper.
- **[[#3803] Daemon mode (qwen serve): proposal & open decisions](https://github.com/QwenLM/qwen-code/issues/3803)** *(OPEN)*: A comprehensive 24-chapter design proposal for a daemon mode. This is a major architectural evolution for Qwen Code, enabling server-like operation. The PR #3889 is the first stage of this effort.
- **[[#3993] Weixin channel bot sends gray placeholder images](https://github.com/QwenLM/qwen-code/issues/3993)** *(OPEN)*: A specific integration bug where the WeChat channel bot fails to display images correctly, showing only a gray placeholder instead of the intended picture.
- **[[#3888] Model stream ended without a finish reason](https://github.com/QwenLM/qwen-code/issues/3888)** *(OPEN)*: A recurring API error where the model stream ends unexpectedly. This suggests either an unstable connection to the inference endpoint or a timeout on the server side, causing user frustration.

### 4. Key PR Progress
- **[[#4002] fix(core): unify Edit/WriteFile prior-read with Claude Code](https://github.com/QwenLM/qwen-code/pull/4002)** *(CLOSED, MERGED)*: The critical patch for the binary detection and file truncation bugs (#3964, #3945). Aligns Qwen Code's prior-read logic with Claude Code's approach, resolving the read-before-edit deadlock.
- **[[#3889] feat(cli,sdk): qwen serve daemon (Stage 1)](https://github.com/QwenLM/qwen-code/pull/3889)** *(OPEN)*: First stage of the `qwen serve` daemon, implementing an HTTP + SSE server that bridges the ACP protocol. This is a foundational piece for running Qwen Code as a service.
- **[[#3589] feat(tools): add ToolSearch for on-demand loading of deferred tool schemas](https://github.com/QwenLM/qwen-code/pull/3589)** *(CLOSED, MERGED)*: Shrinks the default tool list by hiding MCP and low-frequency tools behind a search tool, saving ~15K tokens in context. A significant optimization for prompt budgets.
- **[[#3598] feat(cli): add --json-schema for structured output in headless mode](https://github.com/QwenLM/qwen-code/pull/3598)** *(OPEN)*: Allows users to enforce structured JSON output in headless mode by supplying a JSON Schema. A powerful feature for automated workflows and tool calling.
- **[[#3733] feat(cli): support batch deletion of sessions in /delete](https://github.com/QwenLM/qwen-code/pull/3733)** *(OPEN)*: Introduces multi-select for the `/delete` slash command, improving session management UX. Uses space to check items and enter to confirm.
- **[[#3969] feat(cli): Ctrl+B promote keybind](https://github.com/QwenLM/qwen-code/pull/3969)** *(OPEN)*: The final piece of the foreground-to-background task promotion feature, allowing sub-agents to be moved to the background via a Ctrl+B keybind.
- **[[#3871] feat(cli): core built-in i18n coverage](https://github.com/QwenLM/qwen-code/pull/3871)** *(OPEN)*: Expands internationalization support, localizing built-in slash commands and UI labels. This is a major step for non-English developer communities.
- **[[#3776] feat(installer): add standalone archive installation](https://github.com/QwenLM/qwen-code/pull/3776)** *(OPEN)*: Introduces code-server-style standalone archives for installation, with a fallback to npm. Improves offline deployment scenarios.
- **[[#3491] feat: add /diff command and git diff statistics utility](https://github.com/QwenLM/qwen-code/pull/3491)** *(CLOSED, MERGED)*: Implements a `/diff` command and a core utility to parse structured git diff statistics (`numstat`, `shortstat`). Directly addresses the feature request in #2997.
- **[[#3849] feat(models): add cross-authType model resolution to ModelRegistry](https://github.com/QwenLM/qwen-code/pull/3849)** *(OPEN)*: Moves complex model resolution logic from the Gemini client into the core data layer, making it available for all providers. A clean architecture improvement.

### 5. Feature Request Trends
A clear trend has emerged from user **Maddock-DR** with a suite of interconnected feature requests:
- **Multi-Device/Profile Sync**: A unified system for syncing profiles (SOUL.md, skills, memory) across devices, with Git integration ([#4015](https://github.com/QwenLM/qwen-code/issues/4015)) and encrypted storage ([#4016](https://github.com/QwenLM/qwen-code/issues/4016)).
- **Interoperability / Server Modes**: Strong demand for exposing Qwen Code’s tools via standard protocols: **MCP Server** ([#4007](https://github.com/QwenLM/qwen-code/issues/4007)) for integration with other AI tools, and **HTTP API Server** ([#4008](https://github.com/QwenLM/qwen-code/issues/4008)) for simpler REST-based control.
- **Extensibility & Packaging**: Proposals for a standard skill packaging format (`.skill.tar.gz`) for distribution ([#4014](https://github.com/QwenLM/qwen-code/issues/4014)) and integration of Alibaba Cloud Bailian CLI for multimodal capabilities like image/video generation ([#4009](https://github.com/QwenLM/qwen-code/issues/4009)).
- **Developer Experience**: Improvements like a **JSON Schema-driven config validation** ([#4005](https://github.com/QwenLM/qwen-code/issues/4005)) and a **smarter `/commit` command** that uses AI ([#4000](https://github.com/QwenLM/qwen-code/issues/4000)).
- **Agent Configuration**: A formal **Anti-Sycophancy Protocol** to define core personality and bias correction rules ([#4011](https://github.com/QwenLM/qwen-code/issues/4011)).

Overall, the community is pushing Qwen Code from a standalone tool toward a **platform-agnostic, pluggable agent backend** with robust configuration and distribution systems.

### 6. Developer Pain Points
- **File Write & Edit Instability**: The most critical pain point of the week. The `write_file` and `edit` tools frequently and unpredictably misidentify valid UTF-8 text files (especially those with Chinese characters or Markdown) as binary. This forces agents into workarounds (`cat`, `sed`) or completely rewriting files, breaking the promise of stable file operations. See issues #4003, #4004, #4010.
- **Large File Handling**: The `edit` tool requires a file to be read in full first, but `read_file` truncates large files, creating a deadlock. While fixed in today's release, this highlights a long-standing fragility in the file operation pipeline.
- **Configuration & Profile Management**: There is no built-in way to manage or sync configuration across machines. Users must manually copy the `~/.qwen/` directory, risking loss of context, memory, and skills. The suite of feature requests from Maddock-DR highlights this as a major unmet need.
- **Connection & API Errors**: Recurrent errors like "fetch failed," "Model stream ended without a finish reason," and misleading ENOENT errors (due to tilde expansion in `cwd`) indicate that error handling and connection resilience for various backends (OpenRouter, Alibaba Cloud) needs improvement. See issues #3914, #3888, #3998.
- **Binary Detection False Positives**: The heuristic for detecting binary files is too aggressive, flagging common office documents, modern C++ files, and localized text files as binary. This creates a poor user experience and requires constant manual intervention.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*