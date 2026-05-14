# AI CLI Tools Community Digest 2026-05-14

> Generated: 2026-05-14 09:39 UTC | Tools covered: 8

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
**Date:** 2026-05-14 | **Author:** Senior Technical Analyst, AI Developer Tools Ecosystem

---

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing rapidly, with seven major tools (Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code) each serving distinct developer segments while converging on shared infrastructure concerns. The ecosystem is experiencing a classic tension between feature velocity and platform stability: model-level regressions (particularly Kimi's K2.6 downgrade complaints) and streaming fragility (Claude Code's `assertNever`, Copilot CLI's HTTP/2 session errors) are generating the most community heat. A clear pattern emerges of tools evolving from single-agent assistants into multi-agent orchestration platforms with plugin ecosystems, MCP integrations, and daemon/server modes. The competitive differentiation is narrowing on basic features (command suggestions, file operations, git integration) while widening on extensibility architecture, remote orchestration capabilities, and enterprise readiness (auth, permissions, telemetry). Platform compatibility—particularly Windows ARM64 and legacy Linux GLIBC versions—remains an underinvested area causing disproportionate user frustration.

---

## 2. Activity Comparison

| Tool | Hot Issues (Notable) | Key PRs (Reported) | Releases Today | Release Velocity Signal |
|---|---|---|---|---|
| **Claude Code** | 10 | 10 | ✅ v2.1.141 | Steady minor releases, hook features |
| **OpenAI Codex** | 10 | 10 | ❌ None | Major permission migration PoC active |
| **Gemini CLI** | 10 | 10 | ❌ None | Heavy PR activity, security fixes |
| **GitHub Copilot CLI** | 10 | 0 | ✅ v1.0.48-0, -1 | Hotfix cycle for ARM64 regression |
| **Kimi Code CLI** | 10 | 10 | ✅ v1.44.0 | Minor release, but model controversy dominates |
| **OpenCode** | 10 | 10 | ✅ v1.14.49, v1.14.50 | Double patch day; GLIBC regression fixed |
| **Pi** | 10 | 10 | ❌ None | Major refactor sweep (mass closure) |
| **Qwen Code** | 10 | 10 | ❌ None | Nightly pipeline failed; active PRs |

**Key observations:**
- **Zero PR activity** on Copilot CLI is an outlier—suggests tightly controlled release process or hidden development
- **OpenCode** shipped two releases in 24 hours (1.14.49 feature + 1.14.50 bugfix), demonstrating aggressive iteration
- **Pi** closed dozens of issues under `closed-because-refactor` label—signaling consolidation before a major release
- **All tools** have active OOM/streaming/stability bugs competing with new features

---

## 3. Shared Feature Directions

### Requirements appearing across multiple tool communities:

**A. Remote Session Orchestration (4 tools)**
- **Claude Code** (#29006): Control sessions from Desktop app
- **Kimi Code** (#2269): Handoff sessions between devices
- **OpenCode** (#13388): ACP over WebSocket for remote access
- **Pi** (implicit): `runWhenIdle()` for scheduling after agent settles

*Common need*: Developers want headless, long-running sessions they can interact with from multiple clients—essentially "AI agent as a service."

**B. Plugin/MCP Ecosystem Stability (5 tools)**
- **Claude Code** (#58897): Stream parsing crashes on unknown event types
- **Copilot CLI** (#2630): Custom agent MCP servers not connecting in sub-agent mode
- **Kimi Code** (#2263): MCP stderr leaking into interactive terminal
- **OpenCode** (multiple SSE parse failures)
- **Pi** (#4466): Custom autocomplete providers

*Common need*: The plugin/MCP extension model is fragile—connection handling, error isolation, and backward compatibility are universally broken.

**C. Secrets Protection & Security Scanning (3 tools)**
- **Claude Code** (#44868): Model reads and echoes `.env` files
- **Kimi Code** (#2273): Auto-updater lacks SHA256 integrity check
- **Pi** (#4494): Adding provider attribution headers for telemetry governance

*Common need*: Users are increasingly concerned about AI agents accessing sensitive files and about update channel security.

**D. Configurable Context / Memory Budgets (4 tools)**
- **Claude Code** (#56691): Preflight request-size warnings before 32MB limit
- **Gemini CLI** (#21968): Model doesn't use skills enough
- **Copilot CLI** (#3314): Context window dropped from 304k to 128k in one release
- **Qwen Code** (#4141): Context compression not working

*Common need*: Token management is opaque and fragile—users want visibility, control, and reliable compression.

**E. RTL & Unicode Handling (2 tools)**
- **Claude Code** (#16814): Arabic/Hebrew rendered left-to-right
- **Copilot CLI** (v1.0.48-1 fixed CJK/emoji rendering gaps)

*Common need*: Internationalization and non-Latin script support are afterthoughts, causing accessibility excludes.

**F. Platform-Specific Blocker Bugs (4 tools)**
- **Copilot CLI** (#3306): Windows ARM64 completely broken
- **Qwen Code** (#4140): Node.js 26 compatibility regression
- **OpenCode** (#27419): GLIBC_2.29 dependency broke older Linux
- **Pi** (#4323): Wezterm Kitty keyboard breaks Esc key

*Common need*: Fast-moving toolchains (Node.js, Electron, Tauri) create constant platform churn that breaks production setups.

**G. Agent Looping / False Success Signals (3 tools)**
- **Gemini CLI** (#22323): Subagent reports "success" after MAX_TURNS
- **Kimi Code** (#1927): Subagent infinite loops reading same file
- **Pi** (#4338): Agent says "working" but loops forever

*Common need*: Agent orchestration lacks proper termination detection—failures are masked as successes.

**H. Session Management & Archiving (3 tools)**
- **OpenCode** (#6680): View archived sessions on desktop
- **Claude Code** (#57602): Windows auto-archives on focus loss
- **Qwen Code**: Session persistence and restoration

---

## 4. Differentiation Analysis

| Dimension | Market Leader | Runner-up | Also-rans & Lagging |
|---|---|---|---|
| **Release Velocity** | OpenCode (2 releases/day) | Claude Code (minor releases) | Gemini CLI, Pi (refactor phase) |
| **Community Engagement** | Claude Code (239 👍 on #18170) | Kimi Code (high frustration volume) | Copilot CLI (0 PRs today) |
| **Platform Support** | OpenCode, Pi (broadest OS support) | Copilot CLI (Windows ARM64 broken) | Qwen Code (Node 26 broken) |
| **Plugin/Extension Maturity** | Claude Code (hooks, plugins) | OpenAI Codex (MCP OAuth, kernel PoC) | Pi (refactoring extension API) |
| **Enterprise Readiness** | OpenAI Codex (permissions migration) | Claude Code (agent governance) | Kimi Code (no auth/telemetry) |
| **Local LLM Support** | Pi (keyless providers PR #4498) | Qwen Code (ModelScope integration) | All others (cloud-first) |
| **Security Posture** | Gemini CLI (removed `exec()` vulnerability) | Pi (retry watchdog) | Kimi Code (no update integrity) |
| **Model Quality Perception** | Claude Code (stable, minor issues) | Copilot CLI (reliable for GitHub integration) | Kimi Code (severe K2.6 backlash) |

### Key strategic differentiators:

- **Claude Code** dominates on *community trust*—its most-upvoted issue (#18170, 239 👍) is a copy-paste bug, not a model reliability complaint. The `/teach` command (PR #58744) and `agents.txt` spec (PR #58801) show long-term thinking about agent governance.

- **OpenAI Codex** is betting on *architectural separation*—the `codex-kernel` PoC (#20229) extracts core orchestration from host-specific logic, and the permissions migration (PRs #22610-#22612) moves toward fine-grained, runtime-evaluated permission models. This positions Codex for enterprise compliance.

- **Gemini CLI** focuses on *subagent orchestration* with tool repair (#26158) and snapshot recovery (#26939), but suffers from false success signals (#22323) that erode trust. The `issue-fixer` skill (#26951) shows aspiration toward automated maintenance.

- **GitHub Copilot CLI** is most *tightly integrated with GitHub ecosystem* but least open. Zero community PRs today and heavy reliance on hotfixes for platform regressions suggests a corporate-controlled development process.

- **Kimi Code CLI** is in a *crisis of confidence*—the K2.6 model backlash (#1925, 2,268) and persistent 429 errors (#2209) overshadow the v1.44.0 release and MCP fixes. The `/goal` command (#2276) and kill-ring clipboard config (#2260) show product thinking, but infrastructure stability is the primary concern.

- **OpenCode** is the *aggressively open innovator*—two patch releases in one day, DigitalOcean support, MiniMax integration, and mobile touch optimization (#18767). The GLIBC regression shows velocity outweighing QA, but the community appreciates fast iteration.

- **Pi** is undergoing a *foundational refactor*—mass issue closure, proxy agent dependency reduction (#4470), and retry watchdog (#4475) suggest a focus on core reliability before feature expansion. Keyless local LLM support (#4498) is a strategic bet on on-premise AI.

- **Qwen Code** is building for *Chinese ecosystem integration*—ModelScope (#4150), Bailian CLI (#4009), and zh-TW translations (#4129) show a focused regional strategy. The daemon mode (#3803) and tracing infrastructure (#4097, #4126) point toward enterprise deployment.

---

## 5. Community Momentum & Maturity

| Metric | High Momentum | Moderate | Low / Stalled |
|---|---|---|---|
| **Issue Engagement** | Claude Code (239👍 record) | Kimi Code (vocal but frustrated) | Copilot CLI (low community PRs) |
| **PR Velocity** | OpenCode (double releases) | Pi (refactor sweep) | Gemini CLI (steady but not rapid) |
| **Feature Development** | OpenAI Codex (permissions PoC) | Claude Code (agent governance) | Kimi Code (fixing model issues) |
| **Platform Stabilization** | Pi (retry watchdog, OOM fixes) | Qwen Code (daemon refactor) | Copilot CLI (hotfix cycle) |

### Maturity assessment:

- **Claude Code**: Most mature—highest issue engagement, stable release cadence, active plugin ecosystem. The copy-paste bug (#18170) being the most-voted issue indicates core functionality is solid; remaining issues are polish. **Risk**: Complacency on platform bugs (Windows, RTL).

- **OpenAI Codex**: Maturing rapidly—permissions PoC shows enterprise focus, MCP OAuth signals third-party integration maturity. The `codex-kernel` architecture could become a differentiator. **Risk**: Community frustration with authentication (phone verification) and connectivity (WebSocket drops) may erode trust.

- **Gemini CLI**: Mature subagent architecture but *reliability issues* (false success signals, shell hangs) undermine confidence. The eval test expansion (#24353) shows commitment to quality. **Risk**: Model reluctance to use skills (#21968) means orchestration meta-prompts need improvement.

- **GitHub Copilot CLI**: Most *corporate-controlled*—low community PRs, heavy reliance on hotfixes. MCP connection failures (#2630) and context window regressions (#3314) are blockers for agency workflows. **Risk**: Platform exclusivity (GitHub ecosystem) limits cross-platform adoption.

- **Kimi Code CLI**: *High emotional engagement but negative sentiment*—model degradation and 429 errors dominate. The community is demanding revert to K2.5. **Risk**: If model quality issues persist, users will migrate to alternatives.

- **OpenCode**: *Highest raw velocity*—two releases/day, wide provider support, community contributions. The GLIBC regression shows speed over stability. **Risk**: Platform compatibility debt (GLIBC, Windows gaps) may slow future adoption.

- **Pi**: *Healthy foundational phase*—refactoring for long-term maintainability, keyless local LLM support. The mass issue closure is concerning for contributors. **Risk**: Need to prove post-refactor velocity.

- **Qwen Code**: *Building for Chinese enterprise*—ModelScope and Bailian integrations show strategic positioning. OOM errors (#4149) are critical blockers. **Risk**: Memory instability undermines trust in daemon mode.

---

## 6. Trend Signals for Developers

### 🚩 Red Flags (Watch Closely)

1. **Model quality regressions will drive churn**—Kimi Code's K2.6 backlash is a cautionary tale: a single model update can tank community sentiment. Developers should evaluate tools with model-agnostic architectures (OpenCode, Pi) or clear rollback mechanisms.

2. **Platform compatibility debt is accumulating**—Windows ARM64 (Copilot), GLIBC (OpenCode), Node 26 (Qwen Code), and Wayland (Gemini) are breaking on each release. Developers on non-macOS platforms should expect friction.

3. **MCP/plugin fragility is universal**—EVERY tool has at least one MCP connection or stream parsing issue. Agent workflows depending on custom MCP servers will be unreliable across all tools.

4. **False success signals mask agent failures**—Gemini CLI's subagent success reporting and Kimi's infinite loops are not unique. Trusting agent completion status without manual verification is dangerous.

### ✅ Green Flags (Recommended)

1. **Retry watchdogs and heartbeat mechanisms**—Pi (#4475) and Claude Code (hooks) are building recovery logic. This pattern will become standard for agent reliability.

2. **Architectural separation (kernel pattern)**—OpenAI Codex's `codex-kernel` PoC (#20229) and Pi's refactoring point toward cleaner separation of orchestration logic from host-specific code. Tools adopting this pattern will be more maintainable.

3. **Agent governance specifications**—Claude Code's `agents.txt` spec (#58801) and Qwen Code's daemon mode (#3803) indicate a shift from "what can the agent do?" to "what SHOULD the agent do?" Expect governance frameworks to emerge.

4. **Keyless local LLM support**—Pi's PR #4498 and Qwen Code's ModelScope integration show demand for on-premise AI. As data privacy regulations tighten, local LLM support will become table stakes.

5. **Remote session orchestration**—Multiple tools adding WebSocket/remote control features (Claude Code #29006, Kimi Code #2269, OpenCode #13388). The "agent as a service" pattern is emerging.

### 📊 Industry Implications

- **The "model lock-in" era is ending**—Users are demanding model choice (Claude Code, OpenCode, Pi offer multiple providers). Tools that lock users into a single model family will struggle.

- **CLI is becoming the thin client**—The trend toward daemon modes and remote orchestration suggests the CLI will become a local UI for a remote agent service. This enables headless CI/CD integration.

- **Security is the next battleground**—Secrets leakage (#44868 at Claude Code), update integrity (#2273 at Kimi Code), and permission models (Codex's migration) will differentiate tools for enterprise adoption.

- **Platform parity is still unsolved**—Windows and Linux remain second-class citizens in a macOS-dominant ecosystem. Tools that invest in cross-platform quality (Pi, OpenCode) will capture underserved user segments.

---

**Bottom Line for Technical Decision-Makers:**

- **For stability & community**: Claude Code remains the safest bet, but monitor the copy-paste workflow blocker.
- **For enterprise/compliance**: OpenAI Codex's permissions PoC and kernel architecture show promise, but connectivity issues need resolution.
- **For local/on-premise workflows**: Pi's keyless local LLM support is the most advanced; Qwen Code's ModelScope integration serves the Asian market.
- **For maximum flexibility**: OpenCode's multi-provider support and rapid iteration win, but expect platform quirks.
- **For GitHub-centric teams**: Copilot CLI is convenient but risky—MCP instability and platform regressions suggest waiting for maturation.
- **For agent orchestration**: Gemini CLI's subagent architecture is sophisticated, but false success signals need fixing.
- **Avoid if**: You need reliable Windows ARM64 support (Copilot broken), stable context compression (Qwen Code broken), or consistent model quality (Kimi Code in turmoil).

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report (2026-05-14)

## 1. Top Skills Ranking

The following pull requests represent the most actively discussed Skill submissions in the `anthropics/skills` repository, ranked by community comment volume. All are currently **open**.

| # | Skill | Functionality | Discussion Highlights |
|---|-------|---------------|----------------------|
| **#514** | **document-typography** | Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Addresses a pervasive quality issue across all Claude-generated content. | Strong consensus that typographic problems are universal. Reviewer suggestions for configurable thresholds. |
| **#210** | **frontend-design (improvement)** | Revises the existing frontend-design skill to be more actionable, ensuring every instruction is conversation-executable and steering Claude’s behavior precisely. | Debate over balancing brevity with completeness; alignment with Claude’s inherent UI/UX awareness. |
| **#83** | **skill-quality-analyzer + skill-security-analyzer** | Meta-skills that evaluate other Skills across five dimensions (structure, documentation, security) and identify trust-boundary risks. | Community interest in self-auditing the Skills ecosystem; concerns about false positives in security scanning. |
| **#486** | **ODT (OpenDocument Text)** | Enables creation, template filling, and conversion of .odt/.ods files (LibreOffice/ISO standard), plus ODT-to-HTML parsing. | Demand for open-format office support; discussion on handling complex tables and embedded images. |
| **#723** | **testing-patterns** | Covers testing philosophy (Testing Trophy), unit/React component/integration/e2e patterns, CI integration, and flaky test management. | Broad approval for a comprehensive testing reference; queries about mocking strategy coverage. |
| **#181** | **SAP-RPT-1-OSS predictor** | Wraps SAP’s open-source tabular foundation model for predictive analytics on SAP business data (Apache 2.0). | Niche but enthusiastic reception from enterprise users; performance comparisons with GPT-based forecasting. |
| **#360** | **AppDeploy** | Enables full-stack web app deployment directly from Claude using AppDeploy.ai, including lifecycle management (status checks, scaling, rollbacks). | Strong demand for "one-click deploy" from Claude; security concerns about credential handling. |
| **#444** | **AURELION skill suite (kernel, advisor, agent, memory)** | A structured cognitive and memory framework: 5-floor reasoning kernel, domain advisor, autonomous agent orchestration, persistent memory. | Mixed reactions – some find it overly complex; others see it as a reference architecture for agentic systems. |

**GitHub links:** [#514](https://github.com/anthropics/skills/pull/514), [#210](https://github.com/anthropics/skills/pull/210), [#83](https://github.com/anthropics/skills/pull/83), [#486](https://github.com/anthropics/skills/pull/486), [#723](https://github.com/anthropics/skills/pull/723), [#181](https://github.com/anthropics/skills/pull/181), [#360](https://github.com/anthropics/skills/pull/360), [#444](https://github.com/anthropics/skills/pull/444)

---

## 2. Community Demand Trends

The top-voted Issues reveal clear unmet needs:

- **Organizational skill sharing** – Issue [#228](https://github.com/anthropics/skills/issues/228) (13 comments, 7 👍) calls for a shared skill library or direct sharing links within Claude.ai teams, citing friction in the current manual upload workflow.
- **Agent safety and governance** – Issue [#412](https://github.com/anthropics/skills/issues/412) (4 comments) proposes a dedicated *agent-governance* skill for policy enforcement, threat detection, and audit trails – currently absent from the collection.
- **Cross-platform integration** – Issues about running Skills via AWS Bedrock ([#29](https://github.com/anthropics/skills/issues/29)) and exposing Skills as MCP endpoints ([#16](https://github.com/anthropics/skills/issues/16)) indicate strong demand to decouple Skills from the Claude Code client.
- **Evaluation and testing tooling** – Issue [#556](https://github.com/anthropics/skills/issues/556) (8 comments, 6 👍) reports `run_eval.py` failing to trigger Skills in 100% of test queries, highlighting the need for reliable Skill evaluation infrastructure.
- **Security and trust boundaries** – Issue [#492](https://github.com/anthropics/skills/issues/492) (6 comments) warns that community skills under the `anthropic/` namespace create impersonation risks; users want clear provenance labels.
- **Skill-creator modernization** – Issue [#202](https://github.com/anthropics/skills/issues/202) (8 comments) demands a rewrite of the skill-creator meta-skill to be operational rather than educational.

**Anticipated new Skill directions:** enterprise governance policies, cross-client protocol bridges (MCP/Bedrock), automated validation suites, and trust-scoring mechanisms.

---

## 3. High-Potential Pending Skills

Several open PRs with recent activity are likely to land soon:

| PR | Skill | Last Updated | Why It’s Close |
|----|-------|--------------|----------------|
| [#360](https://github.com/anthropics/skills/pull/360) | **AppDeploy** | 2026-05-04 | Final review cycle; deployment workflow considered mature by community. |
| [#444](https://github.com/anthropics/skills/pull/444) | **AURELION suite** | 2026-05-06 | Author resolved most review feedback; only minor formatting issues remain. |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | 2026-04-21 | Positive consensus; maintainer requested one more example section. |
| [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | 2026-03-13 | Awaiting final maintainer sign-off; technical implementation already validated. |
| [#806](https://github.com/anthropics/skills/pull/806) | **sensory (macOS automation)** | 2026-04-02 | Tiered permission model approved; minor AppleScript edge cases being documented. |
| [#568](https://github.com/anthropics/skills/pull/568) | **ServiceNow platform** | 2026-04-23 | Large but well-structured; maintainer requested splitting into sub-skills. |

These Skills address the most common user requests and have absorbed substantive review, making them strong candidates for immediate merging.

---

## 4. Skills Ecosystem Insight

The community’s most concentrated demand is for **integration and reliability skills** – tools that bridge Claude Code into existing enterprise workflows (SAP, ServiceNow, deployment, macOS automation), while simultaneously raising the quality floor for all generated output (typography, testing, codebase audits).

---

# Claude Code Community Digest – 2026-05-14

## Today’s Highlights
A minor release (v2.1.141) lands with hook enhancements for desktop notifications and a new HTTPS cloning preference for plugin sources. The community is buzzing about a long‑standing copy/paste indentation bug now at 239 👍 and 111 comments, while a fresh VSCode extension crash (`"Unhandled case: [object Object]"`) signals a possible regression in streaming‑event handling. Multiple users continue to report subscription‑upgrade payment failures, suggesting a systemic billing issue.

## Releases
**v2.1.141** – Two changes:
- Added `terminalSequence` field to hook JSON output, enabling hooks to emit desktop notifications, window titles, and bells without a controlling terminal.
- Added `CLAUDE_CODE_PLUGIN_PREFER_HTTPS` environment variable to clone GitHub plugin sources over HTTPS instead of SSH, useful for environments without SSH key setup.

[View release →](https://github.com/anthropics/claude-code/releases/tag/v2.1.141)

## Hot Issues (10 noteworthy)

1. **Copy/paste indentation pollution** (#18170) – When copying text from the terminal, leading tabs/spaces and trailing spaces are included. 239 👍 and 111 comments – the most up‑voted issue. A clear workflow blocker for anyone pasting code or prose from Claude Code. [Issue](https://github.com/anthropics/claude-code/issues/18170)

2. **Opus 4.7 via Bedrock: VSCode stream ends with 0 events** (#52151) – After several turns, stream emits zero events; fallback shows `"Unhandled case: [object Object]"`. Only happens in VSCode GUI, CLI works fine. 26 comments, 21 👍. Suggests a VSCode‑specific stream parsing issue. [Issue](https://github.com/anthropics/claude-code/issues/52151)

3. **Feature Request: Remote Control for Desktop sessions** (#29006) – 83 👍, 20 comments. Users want to control Claude Code sessions from the Claude Desktop app, enabling remote orchestration. High demand. [Issue](https://github.com/anthropics/claude-code/issues/29006)

4. **RTL (Right‑to‑Left) support** (#16814) – Arabic, Hebrew, and other RTL languages are rendered left‑to‑right. 46 👍, 20 comments. Accessibility blocker for a significant user base. [Issue](https://github.com/anthropics/claude-code/issues/16814)

5. **Image paste in SSH sessions** (#5277) – Pasting images into Claude Code CLI via SSH doesn’t work (no terminal graphics protocol support). 29 👍. Workaround mentioned: use terminal multiplexers with kitten protocol. [Issue](https://github.com/anthropics/claude-code/issues/5277)

6. **Ultrareview crash consumes free credit** (#52819) – Running `/ultrareview` crashes before producing findings, but still deducts one of three free reviews. 14 comments, 6 👍. Billing/refund concern. [Issue](https://github.com/anthropics/claude-code/issues/52819)

7. **Max 5x → Max 20x upgrade fails ("Unable to update subscription")** (#55266, also #56281, #57122) – Multiple reports of payment failures when upgrading plans, with no resolution from support. 14+ comments each. Indicates a recurring billing system bug. [Issue](https://github.com/anthropics/claude-code/issues/55266)

8. **Active session auto‑archives on focus loss (Windows)** (#57602) – Desktop app auto‑archives the current session within seconds of alt‑tabbing. 8 comments. Annoying data loss for multitaskers. [Issue](https://github.com/anthropics/claude-code/issues/57602)

9. **VSCode extension `"Unhandled case: [object Object]"`** (#58897, also #58994) – TypeScript `assertNever` throws on unknown streaming event types, causing a visible error banner. 5 comments, 4 👍. Points to a forward‑compatibility gap in the event parser. [Issue](https://github.com/anthropics/claude-code/issues/58897)

10. **Claude Code exposes secrets from .env files** (#44868) – Despite `CLAUDE.md` prohibitions, the model reads and echoes secret‑bearing files. 4 comments, 2 👍. A safety and compliance risk. [Issue](https://github.com/anthropics/claude-code/issues/44868)

## Key PR Progress (10 important)

1. **Update Node.js from 20 to 24 in devcontainer** (#16228) – Bumps the DevContainer Node.js version to a supported LTS. Low risk, improves developer environment. [PR](https://github.com/anthropics/claude-code/pull/16228)

2. **Fix: use `git diff --stat` in commit commands** (#58842) – Replaces full `git diff HEAD` with `--stat` to avoid loading massive diffs into context on every `/commit`. Reduces token bloat. [PR](https://github.com/anthropics/claude-code/pull/58842)

3. **Add `agents.txt` v1.0 spec** (#58801) – Introduces a root `agents.txt` file declaring what AI agents may do on the repo. Built entirely with Claude Code. Novel governance mechanism. [PR](https://github.com/anthropics/claude-code/pull/58801)

4. **Docs: Windows Developer Mode note for symlink support** (#56334) – Documents that Windows requires Developer Mode for symlinks, otherwise background agent outputs may show “0 tokens” silently. Addresses #55263. [PR](https://github.com/anthropics/claude-code/pull/56334)

5. **Docs: Troubleshooting section for upstream API errors** (#58789) – Adds a README section guiding users on how to triage API errors before filing GitHub issues. [PR](https://github.com/anthropics/claude-code/pull/58789)

6. **Add `/teach` command** (#58744) – A new slash command that lets users incrementally teach Claude Code about project conventions, patterns, etc., by exploring the codebase and updating `CLAUDE.md`. Community‑contributed enhancement. [PR](https://github.com/anthropics/claude-code/pull/58744)

7. **Docs: clarify instruction precedence** (#58657) – Documents the hierarchy of instruction files (user instructions → project instructions → repo‑level). Addresses #58564. [PR](https://github.com/anthropics/claude-code/pull/58657)

8. **Docs: clarify plugin `bin` executables** (#58656) – Explains how plugins can expose `bin/` executables as bare Bash commands, including packaging requirements. Addresses #42873. [PR](https://github.com/anthropics/claude-code/pull/58656)

9. **Fix: avoid positional substitution in `clean_gone`** (#58655) – Replaces `awk '{print $1}'` with `sed` field extraction to prevent Claude Code’s command parser from stripping `$1`, which broke branch/worktree parsing in `/clean_gone`. Fixes #52226. [PR](https://github.com/anthropics/claude-code/pull/58655)

10. **Feature: git‑aware history plugin** (#58646) – Fixes session fragmentation across git worktrees by using a cross‑worktree session history key. Prevents orphaned sessions when worktrees are deleted. [PR](https://github.com/anthropics/claude-code/pull/58646)

## Feature Request Trends

- **Remote control / orchestration** – Multiple requests for controlling Claude Code sessions from external apps (Desktop, browser, API). (#29006, #41565)
- **Better copy/paste handling** – Remove leading whitespace and hard line breaks from copied terminal output. (#18170, #48037)
- **RTL language support** – Proper rendering for Arabic, Hebrew, etc. (#16814)
- **Image paste in SSH/remote terminals** – Support terminal graphics protocols for pasting images over SSH. (#5277)
- **Auth preservation in `--bare` mode** – Keep OAuth/keychain auth while skipping context collection. (#38022)
- **Preflight request‑size warnings** – Show byte usage for uploaded images before hitting the 32MB limit. (#56691)
- **Secrets protection** – Prevent Claude from reading and echoing `.env`/credential files. (#44868)
- **Configurable network allowlist** – For remote triggers, restrict which hosts can initiate sessions. (#41565)

## Developer Pain Points

- **Copy/paste text corruption** – The most up‑voted issue by far: users cannot cleanly copy code or paragraphs from the terminal. Affects daily workflow.
- **Subscription upgrade failures** – Multiple reports (3+ distinct issues) of payment failures when upgrading plans, with inconsistent support responses. Frustrating for paying users.
- **Permission path bugs** – Auto‑generated `Read` and `Edit` permissions add double‑slash paths (`//Users/...`) in settings files, causing matchers to fail silently. (#44106, #52835)
- **VSCode stream parsing fragility** – The `assertNever` crash on unknown event types makes the extension brittle to API changes. (#58897, #58994)
- **Stream stalls after updates** – Regressions in v2.1.141 causing streams to hang (`sdk_stream_ended_no_result`). (#58989, #58976)
- **Secrets leakage** – Despite instructions, Claude will read and output sensitive files, which is a security risk for projects with `.env` files. (#44868)
- **Session auto‑archive on focus loss** – Desktop app on Windows aggressively archives sessions, interrupting multitasking. (#57602)
- **Ultrareview crediting bugs** – Crashes that still consume free credits, causing billing distrust. (#52819)
- **Hard line breaks in clipboard** – Terminal‑width line breaks are included in clipboard, breaking paragraph structure when pasting elsewhere. (#48037)

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-14

## Today's Highlights

The community remains vocal about authentication hassles (Issue #20161 on phone verification reached 123 comments) and persistent connectivity drops in the desktop app. On the engineering side, OpenAI engineers landed a major permissions migration prototype (`codex-kernel` PoC, #20229) and opened a multi-PR stack to canonicalize workspace roots and MITM hook policies. The new plugin marketplace CLI commands (#21396) and MCP OAuth client ID support (#22575) signal growing investment in extensibility and third-party integration.

## Releases

No new releases in the last 24 hours.

## Hot Issues (10 noteworthy)

1. **[#20161 – Phone number verification doesn't work](https://github.com/openai/codex/issues/20161)** (closed, 123 comments, 88 👍)  
   Users report being forced to enter a phone number after SSO login, even if none was added. High engagement suggests widespread frustration.

2. **[#20552 – View > Toggle File Tree does not reliably reveal the file tree](https://github.com/openai/codex/issues/20552)** (open, 33 comments, 12 👍)  
   macOS desktop app bug where the file tree toggle is intermittently ignored. Affects basic navigation.

3. **[#18960 – Frequent reconnect loop: websocket closed before response.completed](https://github.com/openai/codex/issues/18960)** (open, 24 comments, 19 👍)  
   Streaming failures hit Pro users on macOS. The recurring disconnect pattern indicates a server‑side stability issue.

4. **[#21527 – codex is really too slow](https://github.com/openai/codex/issues/21527)** (open, 17 comments, 7 👍)  
   Performance complaint about both the VS Code extension and the desktop app on Windows. Model response latency cited as the main pain point.

5. **[#22135 – “codex-aarch64-apple-darwin” contains malware (false positive)](https://github.com/openai/codex/issues/22135)** (open, 6 comments, 19 👍)  
   macOS Gatekeeper flags the Codex binary as malware. High reaction count (19 👍) underscores the severity for Mac users.

6. **[#19679 – Make skills metadata context budget configurable](https://github.com/openai/codex/issues/19679)** (open, 9 comments, 13 👍)  
   Enhancement request to avoid the hardcoded 2% skills budget truncation. Power users with many skills are affected.

7. **[#20873 – Chat flagged for possible cybersecurity risk](https://github.com/openai/codex/issues/20873)** (closed, 7 comments, 2 👍)  
   False positive safety checks interrupt legitimate work. Similar reports in #21544 indicate the safety‑check logic needs tuning.

8. **[#22352 – The Codex app on Windows is absolutely garbage](https://github.com/openai/codex/issues/22352)** (open, 5 comments)  
   Harsh title aside, the app freezes (“Not Responding”) on Win11. Combined with #21527, Windows stability is a recurring theme.

9. **[#9471 – Codex arbitrarily renames conversation titles](https://github.com/openai/codex/issues/9471)** (closed, 10 comments, 6 👍)  
   Auto‑renaming makes it hard to track multiple conversations. Closed but still relevant to users managing many threads.

10. **[#22599 – Esc dismisses /side instead of submitting queued steering](https://github.com/openai/codex/issues/22599)** (open, 2 comments)  
    New today: pressing Escape during a `/side` command loses side‑chat context. A quality‑of‑life regression for TUI users.

## Key PR Progress (10 important)

1. **[#22560 – feat: make ToolExecutor an async trait](https://github.com/openai/codex/pull/22560)** (closed)  
   Unifies extension‑tool and host‑tool execution paths by turning `ToolExecutor` into an async trait. Simplifies routing and registration.

2. **[#22575 – Support explicit MCP OAuth client IDs](https://github.com/openai/codex/pull/22575)** (open)  
   Adds `oauth.client_id` to MCP server config, enabling PKCE flows with providers that require a pre‑registered client ID.

3. **[#22610 – permissions: support workspace roots in profiles](https://github.com/openai/codex/pull/22610)** (open)  
   First half of the alternative permissions migration – models workspace roots inside permission profiles, decoupling write permissions from root access.

4. **[#22611 – app-server: use permission ids and runtime workspace roots](https://github.com/openai/codex/pull/22611)** (open)  
   App‑server counterpart to #22610, wiring named permission IDs and runtime workspace roots into session state.

5. **[#22612 – tui/exec: show effective workspace roots in summaries](https://github.com/openai/codex/pull/22612)** (open)  
   Builds on #22611 to improve `/status` and exec startup summaries so they accurately reflect the runtime workspace roots.

6. **[#20659 – Wire MITM hooks into runtime enforcement](https://github.com/openai/codex/pull/20659)** (open)  
   Second of three PRs to add MITM (man‑in‑the‑middle) hook support. This one enforces the hook model during proxy request handling.

7. **[#21396 – [codex] add plugin marketplace CLI commands](https://github.com/openai/codex/pull/21396)** (open)  
   Introduces `apt-get`‑style plugin install from configured marketplaces, treating local cache as a download cache only.

8. **[#20277 – tighten exec safety parsing and sandbox path review](https://github.com/openai/codex/pull/20277)** (closed)  
   Decodes backslash escapes before safety matching and requires approval for sandbox overrides inside explicit paths. Hardens command safety.

9. **[#20338 – tui: stop referencing SandboxMode](https://github.com/openai/codex/pull/20338)** (closed)  
   Removes TUI’s direct dependency on the legacy `SandboxMode` type, pushing the lossy conversion into the remote thread lifecycle layer.

10. **[#20229 – PoC: codex-kernel](https://github.com/openai/codex/pull/20229)** (closed)  
    Proof‑of‑concept extracting prompt construction, sampling, and tool loop into a separate `codex-kernel` crate – a step toward clearer separation of core orchestration from host‑specific logic.

## Feature Request Trends

- **Configurable context budgets** – Users want to adjust the skills metadata slice (currently hardcoded 2%) to prevent truncation warnings (#19679) and a dedicated `.codex/skills` discovery directory alongside `.agents/skills` (#22590).
- **Plugin & MCP ecosystem improvements** – Requests for plugin marketplace CLI (#21396), explicit MCP OAuth client IDs (#22575), and a DingTalk MCP server that should not require OAuth (#21532) show a growing appetite for managed extensibility.
- **Permissions granularity** – The multi‑PR stack (##22610, #22611, #22612) aims to separate workspace‑root permissions from the broader write model. Community feedback (e.g., #18240) asks for named MITM profiles.
- **TUI quality of life** – Esc key should not discard `/side` context (#22599), `/goal` validation must apply to pasted text (#22616), and file paths should be clickable (#22585).

## Developer Pain Points

- **Connectivity & stability** – Frequent WebSocket reconnects (#18960) and stream‑disconnection errors during context compaction (#22107, #22449) plague both macOS and Windows users.
- **Authentication friction** – Phone verification after SSO (#20161) and false‑positive safety flags (#20873, #21544) interrupt workflows without clear workarounds.
- **Performance on Windows** – The desktop app freezes (#22352, #21527), dictation silently fails (#21129), and the Chrome plugin times out (#21878). Windows remains the most problematic platform.
- **TUI quirks** – Backspace deleting multiple characters (#17793), terminal cursor override in Neovim (#21666), and non‑clickable file paths (#22585) erode terminal‑first productivity.
- **False-positive malware warnings** – macOS Gatekeeper falsely flags the Codex binary (#22135), undermining trust on installation.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest – 2026-05-14

## Today's Highlights

No new releases landed in the last 24 hours, but the project saw a flurry of closed PRs addressing Windows shell compatibility, tool recovery, and security vulnerabilities. The community is actively discussing subagent reliability issues, particularly around false success reports after `MAX_TURNS` and the model’s reluctance to use custom skills. A new issue (#27029) has been raised to protect the repository from low-quality AI-generated PRs, signaling growing community concern about code quality gatekeeping.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   Epic tracking the expansion of behavioral eval tests (76 tests across 6 Gemini models). Community has high interest in evaluation reliability (10 comments, p1/p2). This underpins quality assurance for all agent features.

2. **[#22323 – Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   Critical bug: the `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit the maximum turn limit before doing any analysis. 2 👍 and 6 comments, p1/p2. This misreporting hides real failures and confuses debugging.

3. **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   Users report that the model rarely invokes custom skills or sub-agents unless explicitly prompted, even for related tasks. 6 comments, p2. Signals a need for better agent orchestration or prompt engineering.

4. **[#25166 – Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   Repeated hanging behavior after simple commands finish. 3 👍 and 3 comments, p2. High frustration due to workflow disruption.

5. **[#26563 – Tool "save_memory" not found](https://github.com/google-gemini/gemini-cli/issues/26563)**  
   Attempting `/memory add` fails with "Tool 'save_memory' not found." 5 comments, p2. Indicates a regression in the memory system tool registration.

6. **[#21983 – browser subagent fails in wayland](https://github.com/google-gemini/gemini-cli/issues/21983)**  
   Browser agent terminates with `GOAL` but fails in Wayland environments. 4 comments, p1/p2, 1 👍. Affects Linux users with modern display servers.

7. **[#22267 – Browser Agent ignores settings.json overrides (e.g., maxTurns)](https://github.com/google-gemini/gemini-cli/issues/22267)**  
   Configuration overrides from `settings.json` are not applied to browser subagents. 3 comments, p2. Undermines user customization.

8. **[#24246 – Gemini CLI encounters 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   When more than 128 tools are available, the CLI receives 400 errors from the Gemini API. 2 comments, p2. Scalability issue for power users with many custom tools.

9. **[#22186 – get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)**  
   Crash when `get-shit-done` output hook prints user summary near completion. 2 comments, p1. Affects reliability of one of the most popular workflows.

10. **[#27029 – Protect gemini-cli from AI slop PRs](https://github.com/google-gemini/gemini-cli/issues/27029)**  
    New issue proposing a GitHub Action to automatically close low-quality AI-generated PRs. 1 comment, 1 👍. Reflects community desire for stricter PR review gates.

---

## Key PR Progress

1. **[#27028 – perf(sessions): sub-second /chat loading for large session histories](https://github.com/google-gemini/gemini-cli/pull/27028)**  
   Reduces `/chat` command load time from 25+ seconds to 634ms on a 59-session, 2.3GB benchmark. Open, area/core. Major UX improvement for users with heavy history.

2. **[#27032 – fix(cli): support Volta auto updates](https://github.com/google-gemini/gemini-cli/pull/27032)**  
   Detects Volta-managed installations and uses Volta’s install command to avoid auto-update loops. Open, p2. Fixes a long-standing pain point for Node version manager users.

3. **[#26939 – fix(context): Fix snapshot recovery across sessions](https://github.com/google-gemini/gemini-cli/pull/26939)**  
   Fixes #26927: context snapshot recovery now works correctly after session boundaries. Open, p2/p3, area/core/agent/platform. Crucial for multi-session workflows.

4. **[#26951 – feat(bot): implement issue-fixer skill and mandate selection](https://github.com/google-gemini/gemini-cli/pull/26951)**  
   Adds an `issue-fixer` skill for the Gemini CLI Bot and allows manual mandate selection (`auto`, `issue-fixer`, `metrics`, `interactive`). Open. Enhances automated issue triage.

5. **[#27025 – fix(core): handle Windows paths under WSL](https://github.com/google-gemini/gemini-cli/pull/27025)**  
   Translates Windows drive-letter paths to WSL mount paths, preserving existing behavior for native environments. Open, p1. Resolves a major cross-platform workflow blocker.

6. **[#27026 – feat(cli): add full-access approval controls](https://github.com/google-gemini/gemini-cli/pull/27026)**  
   Introduces `--full-access` as the privileged approval flag (deprecating `--yolo`). Open, p3. Improves clarity and safety for high-risk operations.

7. **[#25900 – fix(core): prefer pwsh.exe over Windows PowerShell 5.1](https://github.com/google-gemini/gemini-cli/pull/25900)**  
   Merged/closed. Fixes shell command failures with embedded double quotes by using PowerShell Core (`pwsh.exe`) instead of the older Windows PowerShell 5.1. Critical for Windows users.

8. **[#26169 – fix: remove unsafe exec() in app.ts](https://github.com/google-gemini/gemini-cli/pull/26169)**  
   Closed. Removes a CRITICAL severity `exec()` vulnerability in the A2A server. Security fix discovered by automated scanner.

9. **[#26174 – fix: remove instruction to combine shell commands with &&](https://github.com/google-gemini/gemini-cli/pull/26174)**  
   Closed. Removes the system prompt instruction to combine shell commands with `&&`, which broke PowerShell on Windows. Improves cross-platform reliability.

10. **[#26158 – feat(core): implement tool repair](https://github.com/google-gemini/gemini-cli/pull/26158)**  
    Closed. Adds automatic recovery when tool calls fail, retrying with repaired parameters. Addresses #26156. Enhances agent robustness.

---

## Feature Request Trends

- **AST-aware code understanding** – Multiple issues (#22745, #22746) request AST-aware file reads, search, and codebase mapping to reduce token noise and improve subagent efficiency.
- **Better memory system hygiene** – Several issues (#26525, #26523, #26522, #26516) focus on improving Auto Memory: deterministic redaction, handling invalid patches, avoiding infinite retries on low-signal sessions.
- **Browser agent resilience** – Users want automatic session takeover, lock recovery (#22232), and `settings.json` respect (#22267) for browser subagents.
- **Agent orchestration improvements** – Requests for smarter tool limiting (#24246), better subagent usage (#21968), and prevention of destructive actions (#22672).
- **Quality gates for contributions** – A new trend (#27029) calls for automated PR quality checks to filter out AI-generated slop.

---

## Developer Pain Points

- **False success signals** – Subagents incorrectly report GOAL success after hitting turn limits (#22323), wasting debugging time.
- **Shell hangs and Windows incompatibilities** – Shell commands hanging (#25166), alias lack of support (#21461), and PowerShell quote issues (addressed by #25900) are recurring frustrations.
- **Browser agent fragility** – Failures on Wayland (#21983), ignored configuration (#22267), and locked profile issues (#22232) plague Linux and persistent-session users.
- **Unwanted subagent activation** – Since v0.33.0, subagents run without permission (#22093) even when disabled in configuration.
- **Workspace and cleanup overhead** – The model frequently creates temporary scripts in random directories (#23571), and there is no way to remove invalid workspace directories (closed PR #26179).
- **Security and policy concerns** – Lack of deterministic redaction in Auto Memory (#26525) and missing warnings for dangerous policies (#21596) worry users about accidental data leaks.
- **Terminal rendering issues** – Flicker on resize (#21924) and corruption after external editors (#24935) hamper the CLI experience.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-14

## Today's Highlights

A quick hotfix release (v1.0.48-1) landed today to resolve a **critical Windows ARM64 regression** introduced in v1.0.48-0, which left the CLI completely unusable on that platform. Alongside that fix, improvements to CJK/emoji rendering and accurate token-limit display in `/context` shipped. Meanwhile, the community is heavily reporting **MCP server connection failures** in sub-agent and non-interactive modes, and a **transient HTTP/2 session error** that breaks long-running reasoning sessions.

---

## Releases

Three versions were published in the last 24 hours:

**v1.0.48-1** (latest)
- **Fixed:** CJK characters and emoji now render without blank gaps between lines.
- **Fixed:** `/context` now shows correct token limits per model (was incorrectly always showing 128k).

**v1.0.48-0**
- **Improved:** `/ask` dialog no longer prompts for follow-up replies it cannot receive.
- **Improved:** Skill content sent to the model no longer includes YAML frontmatter metadata.
- **Fixed:** Auto-disable the built-in `github-mcp-server` in Azure DevOps-only workspaces when running in prompt/headless mode.

**v1.0.47** (2026-05-13)
- `/fork` accepts an optional name; forked sessions display their origin in the sessions dialog.
- Copilot Max subscribers see the correct models for their subscription tier.
- `j/k` keys now supported for up/down navigation in `/diff` view.
- `--resume` support for Copilot cloud agent sessions.

> **Notable:** v1.0.48-0 shipped with missing `runtime.node` for `win32-arm64`, causing immediate crash on Windows ARM64. v1.0.48-1 fixed this issue.

---

## Hot Issues

| # | Title | Comments | Why It Matters |
|---|-------|----------|----------------|
| [#2630](https://github.com/github/copilot-cli/issues/2630) | Custom agent `mcp-servers` not connected in CLI sub-agent or `--prompt` contexts | 9 | A **blocker for agent workflows**: agents defined with `mcp-servers` in YAML frontmatter lose MCP tool access when invoked as sub-agents or via `--prompt`. Community is frustrated — the agent only receives basic tools. |
| [#1433](https://github.com/github/copilot-cli/issues/1433) | `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` not working | 8 (👍 6) | A **long-standing configuration bug** (since February): pointing `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` at an NFS directory doesn't load custom AGENTS.md. The 6 upvotes show this is a common pain point for teams using shared instruction files. |
| [#3304](https://github.com/github/copilot-cli/issues/3304) | `ERR_HTTP2_INVALID_SESSION` — repeated transient retries | 6 | **Frequent mid-session crashes** on long reasoning responses. Users report being unable to complete interactions after this error. A networking reliability issue that impacts daily workflows. |
| [#3281](https://github.com/github/copilot-cli/issues/3281) | v1.0.46 fails to start MCP servers: "Cannot find native binding" | 6 | A **post-upgrade breakage** where the CLI banner appears then immediately errors out on MCP startup. Users hit an npm optional-dependency bug. Triggered the quick hotfix cycle. |
| [#3287](https://github.com/github/copilot-cli/issues/3287) | v1.0.46 blocker: "Failed to persist session events" | 6 (👍 2) | Another **v1.0.46 blocker** — any typed message causes a native binding error when persisting session events. Closed after v1.0.48-0 shipped. Highlights the fragility of native addon builds across platform upgrades. |
| [#3260](https://github.com/github/copilot-cli/issues/3260) | Copy/Paste broken in tmux → Windows Server 2025 | 4 | A **niche but painful UX regression** in v1.0.47: copy/paste fails when accessing Copilot CLI on a remote Windows machine from inside a `tmux` session on macOS/Linux. Points to terminal input-handling issues. |
| [#3013](https://github.com/github/copilot-cli/issues/3013) | Hooks don't fire for background (task) agents | 2 | A **security concern**: hooks intended to block dangerous commands are bypassed when sub-agents call the command. Community notes this is effectively a jailbreak vector. |
| [#3083](https://github.com/github/copilot-cli/issues/3083) | v1.0.40 no longer loads MCP servers from `.mcp.json` on startup | 2 | A **regression in MCP auto-loading** after moving from `.vscode/mcp.json` to `.mcp.json`. Users who migrated are now missing MCP tools at startup. |
| [#3314](https://github.com/github/copilot-cli/issues/3314) | Significant reduction in context window (304k → 128k) in v1.0.47 | 1 | A **new regression** reported today: context window dropped dramatically after upgrading from 1.0.46 to 1.0.47. This would severely limit the amount of code/context an agent can handle. |
| [#3052](https://github.com/github/copilot-cli/issues/3052) | `--add-github-mcp-tool` leaves endpoint readonly | 1 (👍 1) | **Workflow blocker**: adding a non-readonly tool (e.g., `create_pull_request`) still forces the MCP server to use a read-only endpoint, making the tool unusable. |

---

## Key PR Progress

This section is **empty** — no pull requests were updated in the last 24 hours across the `github/copilot-cli` repository. This is unusual and may indicate that the core team has been focused on shipping the v1.0.48 hotfix cycle rather than merging community contributions.

> **Why this matters:** With multiple high-impact bugs (Windows ARM64 breakage, MCP connection failures, HTTP/2 session errors) and zero PR activity, the community may be relying on issue reports and hotfix releases rather than collaborative code contributions. This could indicate a tightly controlled release process or that development is happening in private forks.

---

## Feature Request Trends

1. **Non-interactive / web-based UI** ([#3301](https://github.com/github/copilot-cli/issues/3301))
   Demand for a `copilot web` command similar to OpenCode's web interface — a local HTTP server with a browser-based UI for the AI coding agent.

2. **Tool-callable `cwd`** ([#3035](https://github.com/github/copilot-cli/issues/3035))
   Users want skills/agents to be able to invoke `/cwd <path>` programmatically, enabling dynamic workspace switching without restarting the CLI.

3. **Org-wide usage monitoring** ([#3305](https://github.com/github/copilot-cli/issues/3305))
   Enterprise users are asking for telemetry and dashboards to track which skills are used, by whom, and with what reliability.

4. **Per-prompt statistics** ([#3312](https://github.com/github/copilot-cli/issues/3312))
   A request for resource-usage data per prompt (token counts, model costs) to help developers optimize their AI usage.

5. **Reject/override agent choices** ([#3303](https://github.com/github/copilot-cli/issues/3303))
   When plan-mode presents options, users want the ability to reject all suggestions and input a custom alternative.

6. **Blocking prompt visibility** ([#2650](https://github.com/github/copilot-cli/issues/2650))
   A notification mechanism when the CLI is waiting for user input — especially for long-running or multi-step tasks.

7. **Windows symlink support in plugin install** ([#2286](https://github.com/github/copilot-cli/issues/2286))
   Resolving git symlink text stubs on Windows when installing plugins from the marketplace.

---

## Developer Pain Points

1. **Native binding failures on Windows ARM64** — The v1.0.48-0 release broke the CLI entirely on ARM64, and the root cause (missing `runtime.node` in prebuilds) was compounded by npm optional-dependency bugs. Three separate issues [#3306](https://github.com/github/copilot-cli/issues/3306), [#3307](https://github.com/github/copilot-cli/issues/3307), [#3309](https://github.com/github/copilot-cli/issues/3309) report the same crash.

2. **MCP server configuration friction** — Custom MCP servers fail silently in sub-agent mode ([#2630](https://github.com/github/copilot-cli/issues/2630)), `.mcp.json` is ignored in non-interactive mode ([#3313](https://github.com/github/copilot-cli/issues/3313)), and migration from `.vscode/mcp.json` broke auto-loading ([#3083](https://github.com/github/copilot-cli/issues/3083)). Three distinct MCP bugs surfaced in the same week.

3. **Transient networking errors kill sessions** — `ERR_HTTP2_INVALID_SESSION` ([#3304](https://github.com/github/copilot-cli/issues/3304)) causes repeated retries and session destruction on long reasoning responses, making the CLI unreliable for heavy tasks.

4. **Configuration weirdness** — `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` fails on NFS ([#1433](https://github.com/github/copilot-cli/issues/1433)), and "No copilot instructions found" warnings are misleading when user-level instructions exist ([#1570](https://github.com/github/copilot-cli/issues/1570)).

5. **Context window regressions** — A single-point update (v1.0.46 → v1.0.47) dropped available context from 304k to 128k ([#3314](https://github.com/github/copilot-cli/issues/3314)), directly limiting AI agent capability.

6. **Cross-platform rendering and input bugs** — Copy/paste broken in tmux→Windows setups ([#3260](https://github.com/github/copilot-cli/issues/3260)), and CJK/emoji rendering gaps (fixed in v1.0.48-1 but symptomatic of deeper terminal TUI issues).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the Kimi Code CLI community digest for 2026-05-14, structured for a technical developer audience.

---

### Kimi Code CLI Community Digest: 2026-05-14

Today's community pulse is dominated by significant frustration with the K2.6 model and widespread "engine overloaded" (429) errors. While the team shipped a minor patch release (v1.44.0), the conversation is heavily focused on model degradation and critical infrastructure instability. Prolific community member **ktwu01** submitted four key documentation and security issues, adding a quality-of-life and safety dimension to the day’s discussions.

### Releases

**Version 1.44.0** was released.
- **Changelog:** This is a minor release primarily focused on internal telemetry improvements, specifically refactoring the "by the way" side-question flow to be tracked as a structured `tool_call` event for better observability.
- **Link:** [https://github.com/MoonshotAI/kimi-cli/releases/tag/1.44.0](https://github.com/MoonshotAI/kimi-cli/releases/tag/1.44.0)

### Hot Issues

1.  **Model Degradation and Performance (#1925, #2268, #2077)**
    - **Tags:** `enhancement`, `bug`, `Critical`
    - **Summary:** A trifecta of complaints. Users are begging for the option to revert to the K2.5 model, claiming K2.6's thinking mode "drowns out creativity" and increases hallucinations (#1925). Another user reports "insane degradation" in task quality since the model change (#2268). Simultaneously, K2.6 is under severe server load, making the service "unusable" under normal conditions (#2077).
    - **Why it matters:** This is the single biggest concern for the community today. The core value proposition—high-quality AI-assisted coding—is being undermined by what many perceive as a bad model release. Community reaction is overwhelmingly negative, with users actively seeking workarounds (like reverting models) or expressing outright frustration.
    - **Links:** [#1925](https://github.com/MoonshotAI/kimi-cli/issues/1925), [#2268](https://github.com/MoonshotAI/kimi-cli/issues/2268), [#2077](https://github.com/MoonshotAI/kimi-cli/issues/2077)

2.  **Subagent Wireless Loop (#1927)**
    - **Tags:** `bug`
    - **Summary:** A critical bug where the `subagent` enters an infinite loop, repeatedly reading the same file hundreds of times. This completely halts any multi-agent workflow.
    - **Why it matters:** This severely impacts the reliability of the subagent system, a key feature for complex tasks. The community reaction (0 likes) suggests it might be affecting a specific use case, but the severity is high for those encountering it.
    - **Link:** [#1927](https://github.com/MoonshotAI/kimi-cli/issues/1927)

3.  **Endless "Engine Overloaded" (429) Errors (#2209)**
    - **Tags:** `bug`
    - **Summary:** A user on a remote server reports a persistent "429 engine_overloaded" error that has lasted over 48 hours, even after upgrading from v1.24.0 to v1.41.0. The issue persists across models (K2.6, K2.5, kimi-for-coding).
    - **Why it matters:** This suggests the overload problem is not just peak-time congestion but a systemic infrastructure or rate-limiting issue. The user has prepared diagnostic files, indicating a high level of engagement and frustration. The 2 👍 reactions show it's not an isolated incident.
    - **Link:** [#2209](https://github.com/MoonshotAI/kimi-cli/issues/2209)

4.  **Remote Session Handoff (#2269)**
    - **Tags:** `Feature Request`
    - **Summary:** A feature request to start a CLI session on one device and seamlessly continue or control it from another (e.g., laptop to mobile).
    - **Why it matters:** This addresses a real workflow need for developers working across multiple environments. While new, it taps into a growing demand for more flexible, cloud-connected development tools.
    - **Link:** [#2269](https://github.com/MoonshotAI/kimi-cli/issues/2269)

5.  **MCP stderr Leak (#2263)**
    - **Tags:** `bug`
    - **Summary:** A regression where stderr output from MCP servers leaks directly into the interactive terminal, disrupting the user interface despite CLI redirects.
    - **Why it matters:** This is a significant usability bug for anyone using MCP servers, making the TUI unstable and messy. The community's response is clear, as a PR (#2275, #2259) was immediately opened to fix this.
    - **Link:** [#2263](https://github.com/MoonshotAI/kimi-cli/issues/2263)

6.  **Windows `hFileVersionInfo` Blank (#2178)**
    - **Tags:** `bug`
    - **Summary:** The Windows binary (`kimi.exe`) has a blank `FileVersionInfo`, causing VS Code's extension to reject it as incompatible.
    - **Why it matters:** This is a critical platform-specific bug that completely blocks Windows users with the VS Code extension from using the latest CLI.
    - **Link:** [#2178](https://github.com/MoonshotAI/kimi-cli/issues/2178)

7.  **Unlimited Background Task Limit (#2157)**
    - **Tags:** `Feature Request`
    - **Summary:** A request for a configurable background task limit or a queueing system. The current hard limit of 4 concurrent tasks causes the 5th to fail with an error.
    - **Why it matters:** This is a major blocker for users trying to scale their agentic workflows, preventing them from using the tool's parallel capabilities effectively.
    - **Link:** [#2157](https://github.com/MoonshotAI/kimi-cli/issues/2157)

8.  **Background Task Timeout (#2232)**
    - **Tags:** `enhancement`
    - **Summary:** Background tasks are killed upon a single timeout, even if the task is nearly complete. Users want to be able to adjust the timeout value.
    - **Why it matters:** The current behavior is wasteful and frustrating. A hard kill on timeout forces users to restart long-running tasks from scratch, negating the benefits of the background agent feature.
    - **Link:** [#2232](https://github.com/MoonshotAI/kimi-cli/issues/2232)

9.  **Security: No Integrity Check for Updates (#2273)**
    - **Tags:** `Security`
    - **Summary:** The auto-updater downloads and executes a binary from a CDN without verifying a SHA256 checksum or a digital signature, and uses an unfiltered `tarfile.extractall`.
    - **Why it matters:** This is a high-severity security vulnerability. A compromised CDN or a man-in-the-middle attack could lead to arbitrary code execution without detection. The community's reaction (via the issue author) is immediate concern.
    - **Link:** [#2273](https://github.com/MoonshotAI/kimi-cli/issues/2273)

10. **Web UI: Duplicate Image Sending (#2279)**
    - **Tags:** `bug`
    - **Summary:** In Web mode, when a session is restored, previously uploaded images are re-sent to the LLM, wasting tokens and potentially confusing the model.
    - **Why it matters:** This is a clear bug that wastes user credits and degrades the session experience.
    - **Link:** [#2279](https://github.com/MoonshotAI/kimi-cli/issues/2279)

### Key PR Progress

1.  **Fix: MCP stderr Leak (#2275, #2259)**
    - **Status:** `CLOSED` (#2275) / `OPEN` (#2259)
    - **Summary:** Two PRs address the critical MCP stderr leak. #2275 redirects MCP stderr to log files and displays errors via the `/mcp` command. #2259 routes it to `~/.kimi/logs/mcp/`. Both include tests for the fix.
    - **Why it matters:** These are hotfix PRs, directly responding to the urgent community bug report (#2263). The fast turnaround is commendable.
    - **Links:** [#2275](https://github.com/MoonshotAI/kimi-cli/pull/2275), [#2259](https://github.com/MoonshotAI/kimi-cli/pull/2259)

2.  **New Feature: `/goal` Slash Command (#2276)**
    - **Status:** `OPEN`
    - **Summary:** Introduces a `/goal` command for stateful goal management, including persistence (objective, status, token budget), subcommands (`/goal create`, `/goal status`), and budget tracking.
    - **Why it matters:** This adds a high-demand workflow feature inspired by Codex, allowing users to define and track long-running objectives directly within the CLI. It's a significant UX enhancement.
    - **Link:** [#2276](https://github.com/MoonshotAI/kimi-cli/pull/2276)

3.  **Fix: Memory Leaks (Broadcast Queues & Web Store) (#2236)**
    - **Status:** `OPEN`
    - **Summary:** Fixes memory leaks by bounding broadcast queues (awaiting slow consumers) and capping the web store session cache to prevent OOMs for users with thousands of sessions.
    - **Why it matters:** This is a critical fix for stability, especially for long-running sessions or users with many projects. It addresses the root cause of potential Out-of-Memory crashes.
    - **Link:** [#2236](https://github.com/MoonshotAI/kimi-cli/pull/2236)

4.  **Fix: Connection Leaks (aiohttp TCPConnector) (#2231)**
    - **Status:** `OPEN`
    - **Summary:** Reuses a single `TCPConnector` for all HTTP requests instead of creating a new one each time, preventing file descriptor pressure and reducing latency.
    - **Why it matters:** This is a key performance improvement that reduces overhead for all tool calls, fetches, and auth flows. It's a low-level, architectural fix.
    - **Link:** [#2231](https://github.com/MoonshotAI/kimi-cli/pull/2231)

5.  **New Feature: `--prompt-interactive` Flag (#2246)**
    - **Status:** `OPEN`
    - **Summary:** Adds a `-P`/`--prompt-interactive` flag for the shell UI. The current `--prompt` flag runs a single command and exits; this new flag allows passing an initial prompt and then staying in the interactive session.
    - **Why it matters:** This addresses a common workflow gap, allowing users to start a directed session without losing the ability to ask follow-up questions.
    - **Link:** [#2246](https://github.com/MoonshotAI/kimi-cli/pull/2246)

6.  **Fix: Tool Message Content Type (#1771)**
    - **Status:** `OPEN`
    - **Summary:** Fixes a bug where the CLI sends a list of `ContentPart` objects as the content for a `role: "tool"` message, violating the OpenAI API spec which requires a string. This caused a 400 error.
    - **Why it matters:** This is a core protocol compliance fix. It's been open for over a month, suggesting a potentially complex root cause, but it's crucial for interoperability.
    - **Link:** [#1771](https://github.com/MoonshotAI/kimi-cli/pull/1771)

7.  **Fix: UserPromptSubmit Hook with ContentPart (#2176)**
    - **Status:** `OPEN`
    - **Summary:** Fixes a bug where the `UserPromptSubmit` hook received an empty prompt when the user input was a list of `ContentPart` objects instead of a plain string.
    - **Why it matters:** This fixes a broken core hook, which could break extensions or other hooks that depend on the prompt text.
    - **Link:** [#2176](https://github.com/MoonshotAI/kimi-cli/pull/2176)

8.  **Test: Flaky Background Agent Tests (#2008)**
    - **Status:** `OPEN`
    - **Summary:** Fixes flaky tests in `test_agent_tool.py` by using `wait_for_status` instead of tight polling loops that timeout on slow CI runners.
    - **Why it matters:** This improves the reliability of the CI pipeline, reducing false negatives and developer friction when contributing.
    - **Link:** [#2008](https://github.com/MoonshotAI/kimi-cli/pull/2008)

9.  **New Feature: Slash Command Aliases (#2261)**
    - **Status:** `OPEN`
    - **Summary:** Introduces a system for slash command aliases, allowing users to invoke commands via short names, with UI feedback and canonical telemetry tracking.
    - **Why it matters:** This is a quality-of-life improvement that streamlines the command line workflow, making it faster for experienced users.
    - **Link:** [#2261](https://github.com/MoonshotAI/kimi-cli/pull/2261)

10. **New Feature: `kill_ring_system_clipboard` Config (#2260)**
    - **Status:** `OPEN`
    - **Summary:** Adds a config option to disable the integration between the Emacs-style kill ring and the system clipboard (defaulting to `true`).
    - **Why it matters:** This addresses a common user preference and potentially a source of confusion for developers who don't want their shell commands polluting the system clipboard.
    - **Link:** [#2260](https://github.com/MoonshotAI/kimi-cli/pull/2260)

### Feature Request Trends

- **Model Selection & Control:** A resounding demand for the ability to choose between models (K2.5 vs K2.6) and a revert of the recent model change due to degraded performance (#1925).
- **Remote & Multi-Device Workflow:** A clear interest in starting sessions on one machine and continuing on another, including remote control capabilities (#2269).
- **Scalable Agent Orchestration:** Users want to control the concurrency and timeout behavior of background/subagent tasks to scale their workflows (#2157, #2232).
- **Internationalization (i18n):** A formal request for multi-language support, starting with Simplified Chinese, to lower the barrier for non-English speakers (#2270).
- **Better MCP Ecosystem:** Issues and PRs around MCP stderr leakage and configuration suggest a need for better isolation and error handling for MCP servers (#2275, #2259, #2263).
- **Developer Experience & Onboarding:** Users are asking for clearer documentation on rate limits, prerequisites for development, and more straightforward installation instructions (#2278, #2274, #2271).
- **Security & Integrity:** A strong signal from the community about the need for integrity checks in the update process (#2273).

### Developer Pain Points

- **Model Performance Regression:** The most significant pain point. Upgrading to the K2.6 model is widely perceived as a downgrade, causing confusion, hallucinations, and general unreliability for coding tasks.
- **Service Unavailability (429):** The "engine overloaded" error is persistent and widespread, effectively blocking a large number of users from using the service for extended periods. This is a critical infrastructure issue.
- **Subagent Reliability:** The subagent system is suffering from show-stopping bugs like infinite loops (#1927) that make it unusable for some workflows.
- **Platform-Specific Bugs:** Windows users face a critical blocker with the VS Code extension, indicating a need for platform parity and rigorous QA.
- **Usability Regressions:** The MCP stderr leak is a prime example of a new bug that severely degrades the user experience.
- **Hard Limits & Waste:** The hard limit on background tasks and the forced timeout kill policy are causing frustration and wasted compute cycles for users trying to push the tool to its limits.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-05-14

## Today’s Highlights
Two patch releases (v1.14.49 and v1.14.50) landed today. v1.14.49 introduced a new model/provider API and DigitalOcean support but broke the TUI on older Linux systems due to an accidental GLIBC_2.29 dependency; v1.14.50 shipped hours later with critical bugfixes for HTTP event streams and busy‑session handling. Meanwhile, the community is rallying around long‑standing feature requests (archived sessions, ACP over WebSocket) and reporting SSE parsing issues across multiple models.

## Releases
- **v1.14.50** — Bugfix release: kept HTTP event streams alive after initial connect, returned proper busy errors when a session is already running prompt/shell work, and allowed invalid `small_model` config values to fall back cleanly.
- **v1.14.49** — Feature release: added v2 model/provider listing API, DigitalOcean OAuth + Inference Router (thanks @Spherrrical), automatic `opencode.jsonc` creation, and enabled `customize-opencode` by default. **Notable regression**: introduced a hard dependency on GLIBC_2.29+, causing TUI startup failures on Ubuntu 18.04 and other older systems.

## Hot Issues
1. [#6680 – View archived sessions on desktop](https://github.com/anomalyco/opencode/issues/6680)  
   *33 comments, 7 👍* – Long‑running request for a menu item to browse archived sessions. One of the most upvoted open features.

2. [#21643 – Socket connection closed unexpectedly](https://github.com/anomalyco/opencode/issues/21643)  
   *13 comments* – Users on various backends see `fetch()` failures with a cryptic socket error. No clear root cause yet.

3. [#13388 – ACP over WebSocket for remote access](https://github.com/anomalyco/opencode/issues/13388)  
   *7 comments, 1 👍* – Expose the Agent Client Protocol over WebSocket to allow clients on other hosts to use OpenCode seamlessly.

4. [#27419 – v1.14.49 hard dependency on GLIBC_2.29+](https://github.com/anomalyco/opencode/issues/27419)  
   *6 comments* – Reported immediately after v1.14.49 release; workaround is downgrade to v1.14.48. A PR to fix is already open.

5. [#7370 – ACP sets rawInput back to empty](https://github.com/anomalyco/opencode/issues/7370)  
   *6 comments, 6 👍* – Critical for ACP users: tool calls lose the original `rawInput` field, breaking downstream validation.

6. [#19005 – Make local file paths clickable in terminal](https://github.com/anomalyco/opencode/issues/19005)  
   *5 comments, 1 👍* – Simple UX improvement: clickable paths would save manual copy‑paste in the TUI.

7. [#23442 – SSE JSON parse failure with GLM‑5.1 (Z.AI)](https://github.com/anomalyco/opencode/issues/23442)  
   *5 comments* – Malformed SSE from the model’s response kills the stream; not a pure OpenCode bug but affects many users of that provider.

8. [#27418 – opencode-linux-1.14.49 can’t start (SIGPWR)](https://github.com/anomalyco/opencode/issues/27418)  
   *4 comments, 1 👍* – Another startup failure on Linux, seemingly different from the GLIBC issue (receives SIGPWR). Downgrade works.

9. [#23153 – Pay‑Go with crypto](https://github.com/anomalyco/opencode/issues/23153)  
   *4 comments, 7 👍* – High demand for cryptocurrency payment options for OpenCode Go usage.

10. [#27081 – Leader key stops working in v1.14.42](https://github.com/anomalyco/opencode/issues/27081)  
    *4 comments, 1 👍* – TUI keybinding regression after the simplified flat‑keybind refactor. Still open, affecting power users.

## Key PR Progress
1. [#27491 – Upgrade OpenTUI to 0.2.10](https://github.com/anomalyco/opencode/pull/27491) – Fixes the GLIBC_2.29 issue (#27419). Merged quickly after the regression was confirmed.

2. [#27494 – Refactor LSP initialize errors to tagged types](https://github.com/anomalyco/opencode/pull/27494) – Converts legacy error handling to `Schema.TaggedErrorClass`, improving diagnostics for LSP timeouts.

3. [#27484 – Refactor provider init errors](https://github.com/anomalyco/opencode/pull/27484) – Similar refactor for provider initialization errors, keeping CLI formatting compatible.

4. [#18767 – Mobile Touch Optimization](https://github.com/anomalyco/opencode/pull/18767) – Still open; adds touch‑friendly gestures and responsive layout for the desktop app on tablets/phones.

5. [#27011 – MiniMax OAuth device code flow plugin](https://github.com/anomalyco/opencode/pull/27011) – New provider integration supporting both global and China‑domestic MiniMax endpoints.

6. [#16513 – Add Go usage endpoint](https://github.com/anomalyco/opencode/pull/16513) – New `/zen/go/v1/usage` API for OpenCode Go users, enabling external billing dashboards.

7. [#25066 – Auto‑enable interleaved reasoning for Kimi K2.6](https://github.com/anomalyco/opencode/pull/25066) – Fixes slow responses with Kimi models by forcing interleaved reasoning mode. Closes several related issues.

8. [#27460 – MiniMax Token Plan OAuth provider](https://github.com/anomalyco/opencode/pull/27460) – Companion PR to #27011, adding OAuth + API key support for MiniMax’s “token plan” tier.

9. [#27469 – Remap base64 workspace store names during Tauri→Electron migration](https://github.com/anomalyco/opencode/pull/27469) – Fixes silent loss of historical session data when upgrading from the old Tauri desktop app to the Electron version.

10. [#26861 – Fix old messages disappearing during long sessions](https://github.com/anomalyco/opencode/pull/26861) – Adds lazy‑scroll loading and virtualisation to prevent message loss, a long‑standing TUI bug (#7380).

## Feature Request Trends
- **Session & conversation management** – Multiple requests for viewing archived sessions (#6680), making file paths clickable (#19005), and a built‑in Git UI (#26558).
- **Payment expansions** – Crypto payment support (#23153) and a “Pro” tier with shareable monthly quotas (#24879) reflect frustration with current Go/Zen pricing.
- **Remote access & ACP** – ACP over WebSocket (#13388) and the ability to use OpenCode from another host are increasingly requested.
- **Agent/sub‑agent stability** – Features around parallel multi‑task execution and sub‑agent interaction are surfacing, likely driven by the “oh-my-openagent” plugin.

## Developer Pain Points
- **GLIBC & platform compatibility** – v1.14.49’s accidental GLIBC_2.29 dependency broke the TUI on older Linux distros, forcing urgent rollbacks. A recurring concern for users on LTS systems.
- **SSE stream parsing fragility** – Multiple reports (#23442, #27365, #25247) of JSON parse errors and lost stream boundaries; the parser appears sensitive to malformed model responses.
- **LSP timeout too short** – Java/Gradle projects with JDTLS need >100s to initialise, but OpenCode’s default is ~15s (#23982). Hardcoded plugin skip logic (#16225) also blocks legitimate external plugins.
- **Windows toolchain gaps** – `.docx` reading, PowerShell Chinese encoding, and Word COM automation all fail or are unsupported (#27476).
- **TUI regressions** – Leader key broken (#27081), messages disappearing (#7380, now fixed via PR), and sub‑agent freezes (#27479) harm daily workflows.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest – 2026-05-14

## Today's Highlights
A major refactor sweep is underway, with dozens of issues closed under the `closed-because-refactor` label, signalling a consolidation phase before a significant release. The community is actively pushing for better local LLM support (a keyless provider pattern is already in review) and terminal compatibility fixes, while a new retry watchdog hook aims to resolve persistent agent-stalling problems.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **[#3357 – Official local LLM provider extension](https://github.com/earendil-works/pi/issues/3357)**  
   Highest-upvoted open issue (23 👍) requesting dynamic model list fetching from `{baseUrl}/models`. The top comment thread discusses hooking into llama.cpp, Ollama, and LM Studio. Community strongly favours a first-class local provider.

2. **[#27 – Implement Retries (pkg:ai)](https://github.com/earendil-works/pi/issues/27)**  
   Closed but historically critical; the discussion highlights vague error messages and the need for proper retry logic, now addressed by the retry watchdog PRs.

3. **[#2023 – pi.runWhenIdle() for scheduling after agent settles](https://github.com/earendil-works/pi/issues/2023)**  
   Still open, 10 comments. Demonstrates a real workflow gap: tools that queue `/reload-runtime` via `sendUserMessage` need guarantees on agent idle state. A well-received feature with multiple +1 reactions.

4. **[#4323 – Wezterm Kitty keyboard breaks Esc key](https://github.com/earendil-works/pi/issues/4323)**  
   Reported in v0.64, confirmed on latest wezterm. The `enable_kitty_keyboard` option causes raw escape sequences to be printed instead of recognized. A PR (#4482) is already merged to fix this.

5. **[#4338 – Agent says "working" but loops forever](https://github.com/earendil-works/pi/issues/4338)**  
   A recurring pain point: the agent gets stuck in silent loops requiring a restart. The retry watchdog PR (#4475) directly addresses this by recovering idle provider errors.

6. **[#4477 – Fake context window usage size](https://github.com/earendil-works/pi/issues/4477)**  
   Shows 44.2% context usage in Pi versus 155k tokens reported by the llama server, with a puzzling "Buffer: 262.1k (202%)". Community suspects a mismatch between token counting and compression logic.

7. **[#4207 – Typed cross-extension service calls (Extension API)](https://github.com/earendil-works/pi/issues/4207)**  
   4 comments, closed as part of the refactor. Proposes a lightweight service registry to replace ad-hoc RPC over the untyped event bus. The strawman API garnered positive feedback.

8. **[#4466 – @ file autocomplete ignores .gitignore'd files](https://github.com/earendil-works/pi/issues/4466)**  
   Discussion about whether to expose custom autocomplete providers or respect `.gitignore`. 3 comments, 1 👍. A nuanced UX trade-off for OSS contributors.

9. **[#3954 – New default verbosity for codex breaks workflows](https://github.com/earendil-works/pi/issues/3954)**  
   Closed as a behaviour change alert. Community reports that increased verbosity from codex integration breaks scripts expecting silence. Suggests a need for configurable verbosity levels.

10. **[#4439 – Harmony response format corrupts tool calls](https://github.com/earendil-works/pi/issues/4439)**  
    Models using Harmony produce malformed tool names (e.g., `read<|channel|>commentary`). The parser lacks special handling for Harmony's `<|channel|>` tokens. 3 comments, reported as a blocker for specific providers.

## Key PR Progress
1. **[#4516 – fix(coding-agent): blocked edit tool calls render with error styling](https://github.com/earendil-works/pi/pull/4516)**  
   Fixes a TUI visual bug where blocked edit tool calls displayed green (success) instead of red (failure). Small UX win for developer feedback.

2. **[#4498 – feat(agent): keyless providers](https://github.com/earendil-works/pi/pull/4498)**  
   Introduces a `keyless` boolean attribute for provider definitions, allowing local providers (Ollama, LM Studio) to register without an API key. Consolidates shared header resolution into `resolveAllHeaders`.

3. **[#4496 – fix(compaction): auto-compaction for local models with no usage data](https://github.com/earendil-works/pi/pull/4496)**  
   Solves the problem that local models report zero token usage, causing `shouldCompact` to always return false. Also fixes two additional bugs in the compaction logic.

4. **[#4486 – fix(ai): OpenAI Codex SSE - prefer retry-after headers](https://github.com/earendil-works/pi/pull/4486)**  
   Honors `retry-after-ms` and `retry-after` headers returned by OpenAI Codex, improving retry behavior over a fixed default fallback.

5. **[#4494 – Track direct NVIDIA NIM request origin](https://github.com/earendil-works/pi/pull/4494)**  
   Adds provider attribution headers for NVIDIA NIM requests, reusing the same telemetry-gated path as OpenRouter. Helps NVIDIA identify Pi-originated requests.

6. **[#4470 – refactor(ai): replace proxy agent dependencies](https://github.com/earendil-works/pi/pull/4470)**  
   Vendors HTTP(S) proxy resolution, removing 8+ transitive dependencies including `@tootallnate/quickjs-emscripten`. SOCKS/PAC proxy no longer supported, but the reduction in bundle size is significant.

7. **[#4482 – Address kitty protocol edge-case in wezterm](https://github.com/earendil-works/pi/pull/4482)**  
   Fixes the `\x1b\x1b` legacy meta-key detection that broke `enable_kitty_keyboard`. The patch checks the next character to avoid splitting escape sequences.

8. **[#4475 / #4472 – Add retry watchdog hook for terminal provider errors](https://github.com/earendil-works/pi/pull/4475)**  
   A heartbeat mechanism that recovers idle retryable provider/API errors if the normal retry path is missed. Exposes a `retry_watchdog` extension hook for observability.

9. **[#4463 – fix(tui): Make markdown.ts more robust to large files](https://github.com/earendil-works/pi/pull/4463)**  
   Replaces `...Array` spread operator with a `for` loop to avoid the 65k argument limit on V8/JSC. Fixes #4222 (crash on large markdown files).

10. **[#4452 – chore(coding-agent): add publish shrinkwrap](https://github.com/earendil-works/pi/pull/4452)**  
    Hard-pins all transitive dependencies for the CLI package to ensure reproducible builds across environments.

## Feature Request Trends
- **First-class local LLM support**: Issue #3357 (23 👍) and the merged PR #4498 (keyless providers) show clear demand for seamless integration with local runtimes (Ollama, LM Studio, llama.cpp).  
- **Extension API enrichment**: Requests for typed cross-extension service calls (#4207), subagent detection (#4469), and custom autocomplete providers (#4466) indicate the community wants richer plugin capabilities beyond the event bus.  
- **Auto-compaction customisation**: Issues #4481 (threshold ignoring during multi-turn) and the negative context display (#4477) point to a need for more transparent and configurable memory management.  
- **Keyboard/customisation improvements**: #4508 (model-cycle keybinding override ignored) and #4517 (case-insensitive tool names) reflect demand for finer-grained user control over shortcuts and parsing.

## Developer Pain Points
- **Terminal compatibility is the #1 recurring frustration**: Wezterm Kitty keyboard (#4323), Windows Terminal backspace (#2733), Termux SSH+tmux jumping (#4506) – each highlights the challenge of maintaining robust TTY handling across radically different environments.  
- **Provider-specific quirks break tool calls**: MiMo models requiring `reasoning_content` (#4507, #4505) and Harmony corrupting tool names (#4439) force developers to write provider-aware workarounds.  
- **Context management is still confusing**: The fake usage display (#4477) and silent agent looping (#4338) erode trust in the agent’s progress reporting. Auto-compaction failing on local models (#4496) only worsens the experience.  
- **Dependency chain fragility**: `pnpm` 11 breaking package re-install (#4501), proxy-from-env missing in binary builds (#4513), and the Mistral AI SDK unpinned (#4483) show that dependency hygiene remains a support tax.  
- **The "closed-because-refactor" firehose**: While necessary, the mass closure of issues during the refactor may leave some contributors feeling their reports were dismissed without public resolution. The community would benefit from a post-refactor audit of reopened or re-triaged items.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

Based on the provided GitHub data for the QwenLM/qwen-code repository, here is the technical digest for 2026-05-14.

---

### Qwen Code Community Digest: 2026-05-14

**1. Today's Highlights**

Memory issues are the dominant concern, with multiple reports ([#4149](https://github.com/QwenLM/qwen-code/issues/4149), [#4134](https://github.com/QwenLM/qwen-code/issues/4134)) of JavaScript heap out-of-memory errors and a bug report about context compression not working ([#4141](https://github.com/QwenLM/qwen-code/issues/4141)). On the development front, the community is actively building critical infrastructure, including a finalized `/language` hot-reload fix ([#4143](https://github.com/QwenLM/qwen-code/pull/4143)) and a major architectural rework of the `qwen serve` daemon ([#4113](https://github.com/QwenLM/qwen-code/pull/4113)). A significant integration PR for ModelScope as a new built-in provider has also been opened ([#4150](https://github.com/QwenLM/qwen-code/pull/4150)).

**2. Releases**

No new releases were published in the last 24 hours. A nightly build pipeline failed for `v0.15.10-nightly.20260514.d343e2c15` ([#4128](https://github.com/QwenLM/qwen-code/issues/4128)).

**3. Hot Issues**

- **[#3803](https://github.com/QwenLM/qwen-code/issues/3803) - Daemon mode (qwen serve): proposal & open decisions:** A comprehensive 14-chapter design series for the `qwen serve` daemon. This is a major community effort shaping the tool's architecture, with Stage 1 already merged. (👍: 1)
- **[#4149](https://github.com/QwenLM/qwen-code/issues/4149) - FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed:** A critical memory bug causing crashes. Likely the same root cause as [#4134](https://github.com/QwenLM/qwen-code/issues/4134), this is a high-priority issue for users with long-running sessions.
- **[#4141](https://github.com/QwenLM/qwen-code/issues/4141) - не работает сжатие контекста (Context compression not working):** A bug report (in Russian) indicating that the context compression feature is spinning indefinitely without actually reducing context, a serious problem for long conversations.
- **[#4091](https://github.com/QwenLM/qwen-code/issues/4091) - Feature Request: Add project-level local context file (QWEN.local.md):** A popular request (👍: 2) for a `.gitignore`-able local context file (e.g., `.qwen/QWEN.local.md`), providing a way to add personal prompts and secrets without polluting the project's shared `QWEN.md`.
- **[#4142](https://github.com/QwenLM/qwen-code/issues/4142) - /language output 切换后必须重启才能生效:** A bug report detailing that changing the output language doesn't apply to the running session. This has been quickly addressed by PR [#4143](https://github.com/QwenLM/qwen-code/pull/4143).
- **[#3730](https://github.com/QwenLM/qwen-code/issues/3730) - [CLOSED] After the update, the Qwen code automatically instructs the user to stop the task:** A closed bug where the tool autonomously stopped long-running tasks. The fix for this was likely in a preceding release. (👍: 0)
- **[#4009](https://github.com/QwenLM/qwen-code/issues/4009) - FEAT(PLUGINS): ADD BAILIAN CLI AS PREINSTALLED MULTIMODAL CAPABILITY PLUGIN:** A proposal to pre-install the Alibaba Cloud Bailian CLI, providing out-of-the-box access to multimodal models for image/video generation and understanding.
- **[#4135](https://github.com/QwenLM/qwen-code/issues/4135) - Tool name migrations not applied at dispatch:** A bug where tool calls using legacy names (`task` for `agent`) fail, as the migration logic is not in the dispatch path. This breaks backward compatibility for cached or remote sessions.
- **[#4111](https://github.com/QwenLM/qwen-code/issues/4111) - SessionStart hook's output cannot be injected into context:** A critical bug from the Alibaba internal team where the `SessionStart` hook's `additionalContext` and `systemMessage` outputs are ignored, preventing dynamic session initialization. This is fixed by PR [#4115](https://github.com/QwenLM/qwen-code/pull/4115).
- **[#4140](https://github.com/QwenLM/qwen-code/issues/4140) - node 26.0.0 - API Error: Connection error:** A compatibility regression with Node.js 26, causing fetch failures. This highlights the need for adapters like the one in PR [#4104](https://github.com/QwenLM/qwen-code/pull/4104).

**4. Key PR Progress**

- **[#4113](https://github.com/QwenLM/qwen-code/pull/4113) - refactor(serve): 1 daemon = 1 workspace (#3803 §02):** A major architectural revision of the `qwen serve` daemon, moving from a multi-workspace to a single-workspace model for simplification and reliability.
- **[#4115](https://github.com/QwenLM/qwen-code/pull/4115) - fix(hooks): inject SessionStart additionalContext into chat context:** Directly addresses bug [#4111](https://github.com/QwenLM/qwen-code/issues/4111) by moving the `SessionStart` hook's `getAdditionalContext()` call to ensure its outputs are properly injected. A critical fix for enterprise users.
- **[#4104](https://github.com/QwenLM/qwen-code/pull/4104) - fix(core): skip incompatible OpenAI dispatcher on Node 26:** Fixes the Node 26 connection regression ( [#4035](https://github.com/QwenLM/qwen-code/issues/4035)) by conditionally applying the custom dispatcher. A crucial compatibility patch following [#4140](https://github.com/QwenLM/qwen-code/issues/4140).
- **[#4143](https://github.com/QwenLM/qwen-code/pull/4143) - fix(cli): apply /language output to running session without restart:** A hotfix for bug [#4142](https://github.com/QwenLM/qwen-code/issues/4142), this is an important UX improvement that eliminates the need to restart the session to apply language changes.
- **[#4129](https://github.com/QwenLM/qwen-code/pull/4129) - fix(i18n): Correct zh-TW translations:** A detailed community contribution fixing 131 lines of Traditional Chinese translations to adhere to local conventions.
- **[#4096](https://github.com/QwenLM/qwen-code/pull/4096) - feat(core,cli): add generic atomicWriteFile:** A foundational infrastructure change adding an `atomicWriteFile` utility to prevent data corruption during tool operations, with a multi-faceted approach for reliability.
- **[#4064](https://github.com/QwenLM/qwen-code/pull/4064) - feat(rewind): add file restoration support to /rewind command:** A significant enhancement to the `/rewind` command that now restores file contents from a backup, allowing users to fully undo an assistant's file modifications.
- **[#4073](https://github.com/QwenLM/qwen-code/pull/4073) - feat(tools): add generic worktree support:** Adds first-class git worktree support with new tools (`enter_worktree`, `exit_worktree`), enabling parallel, isolated agent workspaces.
- **[#4150](https://github.com/QwenLM/qwen-code/pull/4150) - feat(cli): add ModelScope as a built-in third-party API provider:** Integrates ModelScope as a first-class provider, expanding the tool's reach within the ModelScope ecosystem.
- **[#3828](https://github.com/QwenLM/qwen-code/pull/3828) - feat(installer): add standalone hosted install and uninstall flow:** Provides an alternative, non-npm installation path for the application, which simplifies deployment and update management.

**5. Feature Request Trends**

- **Daemonization & Server Mode:** A strong push to make Qwen Code a stable, long-running service (`qwen serve`), with ongoing architectural discussions ([#3803](https://github.com/QwenLM/qwen-code/issues/3803)) and PRs for a debug UI ([#4132](https://github.com/QwenLM/qwen-code/pull/4132)).
- **Enhanced Observability & Telemetry:** Multiple PRs are building out a hierarchical tracing system ([#4097](https://github.com/QwenLM/qwen-code/pull/4097), [#4126](https://github.com/QwenLM/qwen-code/pull/4126)) and hardening the OpenTelemetry setup ([#3731](https://github.com/QwenLM/qwen-code/issues/3731)), making the tool more suitable for production environments.
- **Multimodal & Extension Integration:** A clear desire for extending capabilities beyond code, with proposals to integrate the Bailian CLI ([#4009](https://github.com/QwenLM/qwen-code/issues/4009)) and ModelScope ([#4150](https://github.com/QwenLM/qwen-code/pull/4150)) as built-in multimodal providers.
- **Session Management & UX Improvements:** Requests for features like a per-project local context file ([#4091](https://github.com/QwenLM/qwen-code/issues/4091)), persistent history collapse ([#4085](https://github.com/QwenLM/qwen-code/pull/4085)), and hot-reloading settings ([#4143](https://github.com/QwenLM/qwen-code/pull/4143)) show a focus on improving the developer's day-to-day workflow.

**6. Developer Pain Points**

- **Memory Instability (OOM):** The most critical pain point, with multiple reports of out-of-memory crashes ([#4149](https://github.com/QwenLM/qwen-code/issues/4149), [#4134](https://github.com/QwenLM/qwen-code/issues/4134)). This is compounded by reports that the context compression feature is not working ([#4141](https://github.com/QwenLM/qwen-code/issues/4141)), which is designed to mitigate this issue.
- **Node.js Version Compatibility:** The community is feeling friction from the rapid Node.js release cycle, with version 26 causing immediate breakage ([#4140](https://github.com/QwenLM/qwen-code/issues/4140)).
- **Session Hooks & Extensibility:** Enterprise users are reporting that the `SessionStart` hook is broken ([#4111](https://github.com/QwenLM/qwen-code/issues/4111)), highlighting the fragility of this core extensibility mechanism.
- **Tool Name Migration Issues:** Backward compatibility is a concern, as tools with renamed actions fail silently when old names are invoked ([#4135](https://github.com/QwenLM/qwen-code/issues/4135)).
- **Configuration Not Reflected in Current Session:** The need to restart the CLI for changes like output language to take effect ([#4142](https://github.com/QwenLM/qwen-code/issues/4142)) is a recurring source of friction.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*