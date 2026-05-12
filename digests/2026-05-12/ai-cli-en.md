# AI CLI Tools Community Digest 2026-05-12

> Generated: 2026-05-12 09:49 UTC | Tools covered: 8

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

# Cross-Tool Comparison Report: AI CLI Developer Tools — 2026-05-12

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem continues to mature rapidly, with eight actively maintained tools now vying for developer mindshare. Today's data shows a landscape characterized by rapid iteration cycles—OpenAI Codex shipped four alpha releases in 24 hours—alongside persistent platform-specific pain points, particularly on Windows and macOS. A dominant cross-cutting theme is the **Model Context Protocol (MCP) ecosystem**, with all major tools investing heavily in plugin architectures, subagent protocols, and tool discovery. However, significant differentiation is emerging around pricing localization (Claude Code's India pricing thread at 364 upvotes), session management strategies (fork, rewind, agent views), and enterprise security controls (managed hooks, permission inheritance). The community is collectively grappling with agent autonomy failures, billing friction, and cross-platform parity as the primary barriers to mainstream adoption.

## 2. Activity Comparison

| Tool | Hot Issues | PR Activity (24h) | Release Status |
|---|---|---|---|
| **Claude Code** (v2.1.139) | 10 notable (50 updated) | 1 PR | ✅ New release (Agent View, `/goal`) |
| **OpenAI Codex** (rust-v0.131.0-alpha.6–9) | 10 notable | 10 PRs merged/open | ✅ 4 alpha releases |
| **Gemini CLI** (v0.42.0-nightly) | 10 notable | 10 PRs (P1 fixes) | ✅ Nightly release |
| **GitHub Copilot CLI** (v1.0.45) | 10 notable | 0 PRs | ✅ New release (`/autopilot`) |
| **Kimi Code CLI** | 10 notable | 10 PRs (memory/conn leaks) | ⏸️ No release today |
| **OpenCode** | 10 notable | 10 PRs (CJK TUI fixes) | ⏸️ No release today |
| **Pi** (pi-mono) | 10 notable (big refactor) | 7 PRs | ⏸️ No release today |
| **Qwen Code** (v0.15.11-preview.0/1) | 10 notable | 10 PRs (daemon, rewind) | ✅ 2 preview releases |

**Key observations:** OpenAI Codex leads raw PR volume and release cadence. Claude Code dominates community engagement (single issue at 364 upvotes). GitHub Copilot CLI had zero PR activity—atypically quiet. Pi and OpenCode are in active refactor phases. Qwen Code is the fastest-growing in feature PRs per release.

## 3. Shared Feature Directions

| Requirement | Tools Affected | Specific Needs |
|---|---|---|
| **Session lifecycle management** | **Copilot CLI, Codex, Claude Code, Qwen Code** | Fork/rewind/delete sessions; `/goal` persistent completion conditions; session ID surfacing |
| **MCP tool limit increases** | **Gemini CLI, Codex** | 100–128 tool ceiling too low for multi-server setups; requests for 500+ |
| **Model capacity/reliability** | **Copilot CLI, Codex, OpenCode** | "At capacity" errors despite Pro subscriptions; model-specific API failures (Sonnet 4.5, Opus 4.6/4.7) |
| **OAuth token refresh** | **Codex, Kimi Code, Pi** | Refresh tokens stored but never used; silent MCP failures after expiry |
| **Custom agent/subagent definition** | **Copilot CLI, Gemini CLI, OpenCode** | User-defined agents via Task tool; subagent type validation against hallucinations |
| **Pricing localization** | **Claude Code** (most vocal), **Codex** | INR-denominated plans; regional billing remains unsupported |
| **Windows/Linux parity** | **All tools** | CRLF enforcement (Copilot CLI), WSL scroll issues (Codex), Wayland browser crashes (Gemini CLI), TUI hangs on symlinks (OpenCode) |
| **Context window introspection** | **OpenCode, Qwen Code** | Compression loss detection, duplicate summary prevention, compaction visibility |

**Dominant pattern:** MCP ecosystem integration and session management are the two most universally demanded capabilities, spanning established tools (Claude Code, Codex) and newer entrants (Kimi Code, Qwen Code).

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | Qwen Code |
|---|---|---|---|---|---|---|
| **Primary focus** | Enterprise UX, agent orchestration | Multi-agent collaboration, Rust toolchain | Google ecosystem, subagent protocols | GitHub integration, autopilot mode | Infrastructure hardening, vLLM compat | Daemon architecture, model parity |
| **Target user** | Professional developers, enterprise teams | Power users, multi-model workflows | Google Cloud / Android devs | GitHub-native developers | Python-heavy workflows | Qwen model ecosystem |
| **Technical approach** | Plugin marketplace, managed hooks | Agent protocol interface (A2A), code-mode | Union-find context compaction, session protocols | Custom agent YAML, perms profiles | Python-based, FastMCP OAuth | Git worktree isolation, virtual viewport |
| **Key differentiator** | Agent View dashboard, `/goal` persistence | 4 alpha releases/day, Rust variant | Google OAuth + Vertex AI, A2A protocol | GitHub Copilot subscription bundling | Security-first (CVE fixes, connection pooling) | Daemon mode, rewind-with-files |
| **Current weakness** | Auto-updater TCC dialogs, macOS churn | Model capacity errors at highest tier | Quota confusion, subagent goal masking | Broken `/fork` feature, model 400 errors | Empty tools array bug, Windows 400 error | Ink 7 regression, infinite scroll loop |

**Strategic insight:** Claude Code and Codex are racing toward enterprise-grade agent orchestration, while Gemini CLI and Qwen Code are investing in architectural foundations (subagent protocols vs. daemon mode). Copilot CLI lags in PR velocity but benefits from GitHub's distribution. Kimi Code and Pi are infrastructure specialists—focused on reliability and provider compatibility rather than feature velocity.

## 5. Community Momentum & Maturity

| Tool | Community Maturity | Iteration Speed | Pain Point Severity |
|---|---|---|---|
| **Claude Code** | **Highest** — 364 upvotes on single issue, 50 issues/day | Moderate (1 major release, 1 PR) | High — billing bugs, macOS UX erosion |
| **OpenAI Codex** | **High** — active PRs, frequent alphas | **Fastest** (4 alphas in 24h) | High — capacity for Pro users, zombie processes |
| **Gemini CLI** | **Moderate-High** — structured issue triage, P1/P2 hierarchy | Moderate (1 nightly, 10 PRs) | Medium — quota confusion, shell hangs |
| **GitHub Copilot CLI** | **Moderate** — vocal but low PR output | Low (0 PRs today) | Medium-High — broken features, 400 errors |
| **Kimi Code CLI** | **Emerging** — small but engaged | Moderate (10 PRs, 0 releases) | Medium — memory leaks, vLLM compat |
| **OpenCode** | **Growing** — CJK community active | Moderate (10 PRs, 0 releases) | Medium — Bun crashes on Windows, provider issues |
| **Pi** | **Niche** — refactor-driven churn | Low (7 PRs, refactor focus) | High — SSE parsing, platform gaps |
| **Qwen Code** | **Rapidly Growing** — daily previews | **Fast** (2 previews, 10 PRs) | Medium-High — regressions (Ink 7, scroll loop) |

**Momentum leaders:** Claude Code for community engagement and enterprise credibility; OpenAI Codex for raw development velocity; Qwen Code for fastest improvement-to-regression ratio (aggressively fixing issues within same release cycle).

## 6. Trend Signals

1. **MCP is becoming universal infrastructure.** Every tool either supports MCP natively (Gemini CLI, Codex), has plugins for it (Claude Code, Copilot CLI), or is actively adding it (OpenCode, Pi). The community expects MCP as a baseline, not a differentiator.

2. **Agent autonomy is the trust bottleneck.** The most painful category of bugs across all tools involves agents that:
   - Act without permission (Gemini CLI, Copilot CLI)
   - Mask failures as success (Gemini CLI subagent goal)
   - Hallucinate tool types (OpenCode Task tool)
   - Run destructive commands (Gemini CLI `git reset --force`)

3. **Pricing localization is a geographic expansion gate.** Claude Code's India pricing thread at 364 upvotes is the single highest-voted issue across *all* tools. This signals that US/EU-centric pricing is blocking adoption in the fastest-growing developer markets (India, SE Asia).

4. **Terminal UX is the new UI battleground.** CJK text handling (OpenCode, Pi), scroll stability (Qwen Code, Codex Windows TUI), and keybinding conventions (Ctrl+Backspace, Shift+Enter vs. Ctrl+J) are becoming competitive differentiators as tools reach parity on raw coding ability.

5. **Session management is replacing conversation history.** The move from linear chat logs to forkable, archivable, resumable sessions (Claude Code Agent View, Codex thread deletion, Qwen Code worktree isolation) signals a paradigm shift toward treating AI sessions as first-class development artifacts.

6. **Security hardening is accelerating.** Managed hooks bypassed via proxy (Claude Code), compromised dependency packages (Pi/Mistral), and OAuth token refresh failures (Codex, Kimi Code) indicate the ecosystem is entering an enterprise security maturation phase. Expect more investment in permission inheritance models and supply-chain verification.

7. **Cross-platform parity remains unsolved.** macOS TCC dialogs (Claude Code), Windows Bun crashes (OpenCode, Pi), Wayland browser failures (Gemini CLI), and WSL terminal regressions (Codex) collectively account for ~30% of all high-severity issues. No tool has achieved platform parity.

**Recommendation for developers:** If you prioritize **ecosystem maturity and enterprise readiness**, Claude Code leads. For **fastest iteration and bleeding-edge features**, monitor OpenAI Codex alpha releases. For **strong provider flexibility** (especially Qwen/Google models), Qwen Code or Gemini CLI are gaining ground. For **GitHub-native workflows**, Copilot CLI is adequate but watch for feature parity gaps. The MCP plugin ecosystem is the single best bet for long-term tool portability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report  
**Data as of 2026-05-12 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking  
*Ranked by total discussion attention (comments, engagement) among open Pull Requests.*

| # | PR | Skill / Change | Functionality | Status |
|---|----|----------------|---------------|--------|
| 1 | [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Prevents orphan words, widow paragraphs, and numbering misalignment in AI‑generated documents — a pervasive quality issue. | Open |
| 2 | [#83](https://github.com/anthropics/skills/pull/83) | **skill-quality-analyzer & skill-security-analyzer** | Meta‑skills that evaluate Claude Skills across structure, documentation, and security dimensions. | Open |
| 3 | [#210](https://github.com/anthropics/skills/pull/210) | **frontend-design improvement** | Revises the existing skill for clearer, more actionable instructions that Claude can follow in a single conversation. | Open |
| 4 | [#486](https://github.com/anthropics/skills/pull/486) | **ODT skill** | Create, fill, read, and convert OpenDocument Format files (.odt, .ods) – includes template filling and ODT‑to‑HTML conversion. | Open |
| 5 | [#538](https://github.com/anthropics/skills/pull/538) | **PDF fix (case‑sensitive refs)** | Resolves 8 case‑sensitivity mismatches in `skills/pdf/SKILL.md` that break on case‑sensitive file systems. | Open |
| 6 | [#541](https://github.com/anthropics/skills/pull/541) | **DOCX tracked‑change fix** | Prevents document corruption when adding tracked changes to DOCX files that contain existing bookmarks (shared `w:id` space). | Open |
| 7 | [#539](https://github.com/anthropics/skills/pull/539) | **skill‑creator YAML validation** | Adds pre‑parse detection of unquoted `description` fields containing `:` to avoid silent YAML parsing failures. | Open |
| 8 | [#181](https://github.com/anthropics/skills/pull/181) | **SAP‑RPT‑1‑OSS predictor** | Integrates SAP’s open‑source tabular foundation model for predictive analytics on SAP business data. | Open |

**Discussion highlights:** The document‑focused PRs (#514, #538, #541) reflect strong community interest in **output quality and reliability**. The meta‑skills (#83) and validation improvements (#539) indicate a growing need for **tooling that keeps the Skills ecosystem itself healthy**.

---

## 2. Community Demand Trends  
*Extracted from the most‑commented Issues (sorted by engagement).*

| Issue | Topic | Comments | Key Demand |
|-------|-------|----------|------------|
| [#62](https://github.com/anthropics/skills/issues/62) | Skills disappearing after file rename | 10 | **Reliability and user‑friendly skill management** – users need safe ways to update/organise skill files without losing them. |
| [#228](https://github.com/anthropics/skills/issues/228) | Org‑wide skill sharing | 9 | **Enterprise sharing** – a direct link or shared library to avoid manual `.skill` file distribution. |
| [#556](https://github.com/anthropics/skills/issues/556) | `run_eval.py` never triggers skills | 8 | **Evaluation infrastructure** – the official eval harness is broken (`claude -p` ignores commands), blocking skill development/testing. |
| [#492](https://github.com/anthropics/skills/issues/492) | Security: community skills under `anthropic/` namespace | 6 | **Trust boundary & namespace governance** – community skills impersonating official ones create a phishing‑like risk. |
| [#189](https://github.com/anthropics/skills/issues/189) | Duplicate skills from `document‑skills` and `example‑skills` | 6 | **Plugin content de‑duplication** – two plugins install identical skills, wasting context window space. |
| [#412](https://github.com/anthropics/skills/issues/412) | Skill proposal: agent‑governance | 4 | **Safety patterns for agent systems** – policy enforcement, threat detection, audit trails. |
| [#1087](https://github.com/anthropics/skills/issues/1087) | Plugin loads all repo skills, not declared subset | 2 | **Selective skill loading** – plugins should honour `marketplace.json` declarations to prevent bloat. |
| [#532](https://github.com/anthropics/skills/issues/532) | skill‑creator requires `ANTHROPIC_API_KEY` | 2 | **Enterprise/SSO compatibility** – the description optimizer is unusable for users without a raw API key. |

**Dominant themes:**
- **Enterprise readiness** (sharing, SSO, security)
- **Reliability & quality** (run_eval broken, duplicate loading, disappearing skills)
- **Governance & safety** (namespace trust, agent governance)
- **Infrastructure tooling** (better evaluation, selective plugin loading)

---

## 3. High‑Potential Pending Skills  
*Active‑comment PRs that are not yet merged – these are likely to land soon and address clear community needs.*

| PR | Skill | Why It Matters |
|----|-------|----------------|
| [#514](https://github.com/anthropics/skills/pull/514) | **document-typography** | Addresses a universal pain point: AI‑generated documents with orphan text and widow paragraphs. Easy to adopt, high visibility. |
| [#723](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Covers the full testing stack (unit, React, integration, E2E) – fills a gap for developers using Claude for code. |
| [#360](https://github.com/anthropics/skills/pull/360) | **AppDeploy** | Enables full‑stack web app deployment directly from Claude – a clear productivity win for prototyping and DevOps. |
| [#568](https://github.com/anthropics/skills/pull/568) | **ServiceNow platform** | Broad enterprise platform coverage (ITSM, ITOM, SecOps, CSDM, etc.) – directly responds to demand for enterprise integration. |
| [#806](https://github.com/anthropics/skills/pull/806) | **sensory (macOS automation via AppleScript)** | Offers native macOS automation as an alternative to screenshot‑based computer use – performance and reliability improvement. |
| [#444](https://github.com/anthropics/skills/pull/444) | **AURELION skill suite** | Structured cognitive framework + persistent memory – appeals to power‑users building long‑running agent workflows. |

All of these are **open** with ongoing discussion and updates. Their broad utility suggests they have a high probability of merging in the near term.

---

## 4. Skills Ecosystem Insight  

**The community’s most concentrated demand is for skills that improve AI output quality (typography, document formatting), enable enterprise integration (ServiceNow, SAP, AppDeploy, org‑wide sharing), and provide meta‑level tooling to validate, secure, and evaluate the skills themselves.**  

*This signals a maturation of the ecosystem: from “what can Claude do?” to “how can we make Claude’s output reliable, enterprise‑safe, and easy to share?”*

---

# Claude Code Community Digest — 2026-05-12

## Today’s Highlights

Anthropic shipped **v2.1.139** introducing the long-awaited **Agent View** (Research Preview) — a unified session dashboard accessible via `claude agents` — alongside the new **`/goal`** command for persistent completion conditions. The community is buzzing about **India-specific pricing** (the most-upvoted issue ever at 364 👍 with 157 comments) and a **critical payment-intent bug** (#55982) blocking plan upgrades. Several macOS auto-updater and TCC permission issues continue to erode user trust in the native CLI installer.

---

## Releases

**v2.1.139** — [Release Notes](https://github.com/anthropics/claude-code/releases/tag/v2.1.139)

- **Agent View (Research Preview):** A single-pane dashboard listing every Claude Code session — running, blocked, or finished. Launch with `claude agents`. Documentation at https://code.claude.com/docs/en/agent-view
- **`/goal` command:** Set a completion condition; Claude continues working across interruptions until the condition is met. The changelog entry truncates there, suggesting additional fixes were included but not yet documented.

---

## Hot Issues (10 Noteworthy)

1.  **[#17432 — India-Specific Pricing Plans](https://github.com/anthropics/claude-code/issues/17432)** (157 comments, 364 👍)
    *The most-voted issue in the tracker.* Users request INR-denominated plans comparable to OpenAI and Google. The 4-month-old thread remains active, with Anthropic yet to comment. This signals a major geographic expansion pain point.

2.  **[#55982 — PaymentIntent Voids Immediately](https://github.com/anthropics/claude-code/issues/55982)** (54 comments, 13 👍)
    Plan upgrade payments fail because the `PaymentIntent` is `void_invoice` before confirmation completes. Multiple users report being stuck on lower tiers. A high-severity billing blocker.

3.  **[#26408 — Model Selection Bug](https://github.com/anthropics/claude-code/issues/26408)** (28 comments, 10 👍)
    Issues with `claude-sonnet-4-6` model selection. The 3-month-old bug persists across versions, suggesting a deeper routing or capability-mapping problem.

4.  **[#47482 — YAML Frontmatter Not Injected](https://github.com/anthropics/claude-code/issues/47482)** (20 comments, 1 👍)
    Output styles with YAML frontmatter are parsed and displayed in the status line but **not** injected into the system prompt — contradicting official docs. A configuration trust-breaker.

5.  **[#19031 — Corrupted Image Breaks Entire Session](https://github.com/anthropics/claude-code/issues/19031)** (18 comments, 28 👍)
    A single corrupted image file in context causes persistent API 400 errors for all subsequent messages. No recovery mechanism exists; the session is unrecoverable.

6.  **[#28792 — Remote Control Not Working on Pro](https://github.com/anthropics/claude-code/issues/28792)** (17 comments, 11 👍)
    `claude remote-control` fails with "not enabled" despite an active Pro subscription. Multiple platforms affected.

7.  **[#38008 — Desktop App Shows Wrong Plugins](https://github.com/anthropics/claude-code/issues/38008)** (9 comments, 3 👍)
    The Claude Code plugin marketplace in the Desktop app now displays **Co-Work plugins** instead of CLI plugins. A regression in the app’s UI layer.

8.  **[#51123 — Managed Hooks Bypassed via Proxy](https://github.com/anthropics/claude-code/issues/51123)** (3 comments, 0 👍)
    A **security concern**: the `allowManagedHooksOnly` restriction is bypassed when `ANTHROPIC_BASE_URL` points to a local proxy. Enterprises relying on managed settings are exposed.

9.  **[#48311 — Auto-Updater Spams TCC Dialogs](https://github.com/anthropics/claude-code/issues/48311)** (3 comments, 2 👍)
    Old binaries accumulate in `~/.local/share/claude/versions/`; each new binary triggers fresh macOS permission dialogs. A persistent UX nuisance for Mac users.

10. **[#58298 — Surface Short Session IDs](https://github.com/anthropics/claude-code/issues/58298)** (2 comments, 0 👍)
    *Filed today.* Shell commands (`claude attach`, `claude logs`, etc.) require a short ID, but the ID is not surfaced in `claude agents list` or the Agent View UI. A clear documentation/UX gap for the new feature.

---

## Key PR Progress

Only **one pull request** was updated in the last 24 hours:

**[#58126 — Add `neonpanel` plugin v1.0.0](https://github.com/anthropics/claude-code/pull/58126)**
- **Author:** msoroch
- **Status:** Open
- **Summary:** A new plugin for Amazon-seller operations featuring eight domain agents (replenishment, accounting, supply chain, marketing, forecasting, FP&A, market intel, customer success) grounded in live NeonPanel commerce data via MCP. Demonstrates the growing plugin ecosystem for domain-specific AI workforces.

*Note: PR activity is unusually light today. This may reflect a lull after the v2.1.139 release or that the maintainer team is focused on triaging the 50 open issues updated in the past 24 hours.*

---

## Feature Request Trends

**1. Conversation / Session Navigation** (4+ issues)
Multiple requests for keyboard shortcuts to jump between Q&A blocks (#16784, #54797, #49702) and for a permanently visible prompt bar (#50378). The Agent View partially addresses this, but users want *within-session* navigation, not just session listing.

**2. Pricing Localization** (2+ issues, 500+ combined reactions)
The India pricing thread (#17432) is the top-voted issue ever. Payment failures (#55982, #56281) compound the frustration. The community is signaling that global, flexible billing is a prerequisite for adoption outside the US/EU.

**3. Agent View Enhancements**
Hard-disabled on third-party backends (Bedrock/Vertex/Foundry) per [#58284](https://github.com/anthropics/claude-code/issues/58284). Users also want session IDs surfaced in the CLI list ([#58298](https://github.com/anthropics/claude-code/issues/58298)). The feature is nascent but already drawing configuration/access friction.

**4. Desktop & IDE Integration**
- VS Code extension: disable arrow-key history recall ([#51202](https://github.com/anthropics/claude-code/issues/51202)), system notifications on completion ([#56305](https://github.com/anthropics/claude-code/issues/56305))
- macOS native notifications misattributed to "Script Editor" ([#41511](https://github.com/anthropics/claude-code/issues/41511))

**5. Plugin Ecosystem**
Only one new plugin PR today, but the marketplace confusion bug (#38008) suggests growth is coming. Users want clear separation between Co-Work and CLI plugin catalogs.

---

## Developer Pain Points

**🔴 Payment & Billing (High Severity)**
- PaymentIntent `void_invoice` failure (#55982) — 54 comments, no fix yet
- Can't upgrade Max plans (#56281)
- No INR or region-specific pricing (#17432) — 364 👍

**🔴 macOS Auto-Updater (High Frequency)**
- Old binaries accumulate in `~/.local/share/claude/versions/` without cleanup (#48311)
- Each binary triggers a fresh macOS TCC permission dialog (#58279)
- Desktop app bundled binary exits with code 1 on first message (#58288)

**🟡 Configuration & Security**
- YAML frontmatter in output styles silently ignored (#47482)
- Managed hooks bypassed via `ANTHROPIC_BASE_URL` proxy (#51123)
- Corrupted images crash entire sessions with no recovery (#19031)
- `permissions.ask` ignored for MCP tools on Bedrock (#58289)

**🟡 Platform Parity**
- Agent View hard-disabled on Bedrock/Vertex/Foundry backends (#58284)
- Remote Control broken for Pro subscribers on WSL (#28792)
- Plugin marketplace wrongly shows Co-Work plugins in Desktop app (#38008)

**🟡 Usage & Monitoring**
- Usage dashboard displays incorrect token counts for 7-day period (#58287)
- No meaningful session titles — only last message shown in activity (#36164)

---

*Digest generated for 2026-05-12 from data on github.com/anthropics/claude-code. 50 issues updated in the last 24 hours; 1 PR; 1 new release.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-05-12

---

## Today's Highlights

Four new Rust alpha releases (v0.131.0-alpha.6 through .9) landed in the last 24 hours, signalling active iteration on the experimental Rust toolchain. On the community side, a long-standing phone verification bug was finally closed after 112 comments, while new reports of model capacity failures hitting Pro users and a massive MCP zombie process leak continue to dominate discussion. The team also merged a flurry of PRs focusing on permissions migration, MCP file encoding, and code‑mode execution improvements.

---

## Releases

- **rust-v0.131.0-alpha.9** – Latest Rust alpha.
- **rust-v0.131.0-alpha.8**
- **rust-v0.131.0-alpha.7**
- **rust-v0.131.0-alpha.6**

All four are minor version bumps in the Rust CLI variant. No changelog details provided; likely bug fixes or internal infrastructure updates.  
_See the [releases page](https://github.com/openai/codex/releases) for details._

---

## Hot Issues

1. **[#20161 – Phone number verification doesn't work](https://github.com/openai/codex/issues/20161)**  
   *CLOSED* — After 112 comments and 84 👍, this auth bug blocking SSO login was resolved. The community reaction highlights how critical seamless authentication is for adoption.

2. **[#16088 – Starting a thread in a project without .codex leaves behind an empty .codex file](https://github.com/openai/codex/issues/16088)**  
   *OPEN* — A regression affecting WSL users. 37 comments, 89 👍. The empty file causes confusion and breaks project‑based workflows.

3. **[#17014 – Codex CLI recommends gpt-5.4, then fails with 'Selected model is at capacity'](https://github.com/openai/codex/issues/17014)**  
   *CLOSED* — 30 comments. Despite the report being closed, the underlying capacity issue keeps reappearing (see #22277).

4. **[#10726 – Codex CLI Scroll issue](https://github.com/openai/codex/issues/10726)**  
   *OPEN* — Windows/WSL terminal scrolling broken in the TUI. 29 comments, 12 👍. Affects daily usability for Windows developers.

5. **[#12491 – MCP child processes not reaped after task completion — 1300+ zombies, 37GB memory leak](https://github.com/openai/codex/issues/12491)**  
   *OPEN* — A critical memory/process leak in the GUI app. 20 comments, 3 👍. Underreported but severe for anyone running long‑lived MCP sessions.

6. **[#13018 – Allow to delete threads in the Codex app](https://github.com/openai/codex/issues/13018)**  
   *OPEN* — 16 comments, 85 👍. The highest‑voted feature request currently open. Users find archive‑only management inadequate.

7. **[#13025 – Codex Desktop ignores project .codex/config.toml MCP server and only loads ~/.codex/config.toml](https://github.com/openai/codex/issues/13025)**  
   *OPEN* — 15 comments, 30 👍. A configuration priority bug that makes per‑project MCP setups impossible with the desktop app.

8. **[#22277 – 'Selected model is at capacity' for Pro users ($200/month)](https://github.com/openai/codex/issues/22277)**  
   *OPEN* — Created today. 6 comments, 2 👍. Paying users visibly frustrated; the issue suggests capacity management is failing even at the highest tier.

9. **[#20536 – Document the /goal CLI command and Goals lifecycle](https://github.com/openai/codex/issues/20536)**  
   *OPEN* — 5 comments, 10 👍. A documentation gap: `/goal` exists but is undiscoverable. Community wants better CLI help surfaces.

10. **[#17265 – Codex does not auto-refresh routed MCP OAuth tokens](https://github.com/openai/codex/issues/17265)**  
    *OPEN* — 8 comments, 12 👍. Refresh tokens are stored but never used, causing silent MCP failures after token expiry. Important for third‑party MCP integrations.

---

## Key PR Progress

1. **[#22193 – fix: drop underscored id headers](https://github.com/openai/codex/pull/22193)**  
   *OPEN* — Removes duplicate `session_id`/`thread_id` headers that were rejected by some proxies. Small but critical for network compatibility.

2. **[#22267 – permissions: move workspace roots onto thread state](https://github.com/openai/codex/pull/22267)**  
   *OPEN* — Part of a permissions migration split from a larger PR. Moves writable workspace roots from `SandboxPolicy` to thread state, unblocking future policy changes.

3. **[#22266 – core: box multi-agent handler futures](https://github.com/openai/codex/pull/22266)**  
   *OPEN* — Stack‑safety fix for async futures in multi‑agent scenarios. Prevents potential stack overflows during deep agent recursion.

4. **[#22280 – code-mode: Add pending-aware code mode execution](https://github.com/openai/codex/pull/22280)**  
   *OPEN* — Introduces `execute_to_pending`/`wait_to_pending` APIs for freezing and resuming code‑mode runtimes. Enables more controlled execution flows.

5. **[#22289 – add sep2356 file input encoder](https://github.com/openai/codex/pull/22289)**  
   *OPEN* — Adds a broker‑side encoder for SEP‑2356 data URIs (MCP file‑input standard). Prepares for upcoming MCP file‑input compatibility.

6. **[#22288 – accept env file refs for app uploads](https://github.com/openai/codex/pull/22288)**  
   *OPEN* — Allows `env://current/` file references in `openai/fileParams`. Bridges code‑mode file materialization with existing upload APIs.

7. **[#22287 – add code mode io.write helper](https://github.com/openai/codex/pull/22287)**  
   *OPEN* — A V8‑hosted `io.write(value, path)` helper for code mode. Keeps filesystem access out of the runtime while enabling file output.

8. **[#22270 – Support inheritable permissions profiles](https://github.com/openai/codex/pull/22270)**  
   *OPEN* — Allows named permission profiles to inherit from a base profile. Reduces duplication for enterprise policies that need slight variations.

9. **[#22278 – Invalidate model window after thread rollback](https://github.com/openai/codex/pull/22278)**  
   *OPEN* — Fixes #21986 where rolled‑back turns could still influence the model because the model window ID was reused. Prevents context leakage.

10. **[#22273 – Fix code-mode deferred app tool routing](https://github.com/openai/codex/pull/22273)**  
    *OPEN* — Routes code‑mode nested tool calls through the correct router, fixing `ALL_TOOLS` advertisement mismatches that blocked nested MCP/app calls.

---

## Feature Request Trends

- **Thread lifecycle management**: The most upvoted request (#13018) is the ability to *delete* threads rather than only archive them. Users find archived threads clutter the filesystem and are hard to purge.
- **Poorly documented slash commands**: `/goal` exists but is invisible to users. Community wants comprehensive docs and discoverability for all built‑in CLI commands (#20536).
- **Agent access to built‑in commands**: Several requests (e.g., #15124) ask for slash commands like `/review` to be callable programmatically by sub‑agents.
- **Plugin marketplace localization**: A new request (#22274) asks for Traditional Chinese (Taiwan) translations in the plugin marketplace UI.
- **Configuration parity**: Users want the desktop app to respect project‑level `.codex/config.toml` the same way the CLI does (#13025).

---

## Developer Pain Points

- **Model capacity errors**: Repeated incidents (#17014, #19583, #22277) where Codex recommends a model (gpt‑5.4/5.5) and then rejects requests with “at capacity” — even for Pro subscribers. Causes workflow interruptions and trust erosion.
- **MCP process management**: Zombie processes and memory leaks (#12491) when using the GUI app with MCP servers, along with OAuth token refresh failures (#17265) that silently break integrations.
- **Configuration confusion**: Project‑level configs are ignored by the desktop app (#13025), and per‑project `.codex` directories are silently created (#16088), leading to inconsistent sandbox behaviour.
- **Chat history instability**: Disappearing messages (#20303, #22068) and session load failures (#20895) undermine confidence in long‑running conversations.
- **UI/UX regressions**: Scroll issues in the TUI on Windows (#10726), text overlapping in the VS Code extension (#20758), and the footer overflow bug (#22292) degrade daily experience.
- **Token burning on status checks**: CLI burns subscription tokens when polling `/status` (#22040), a subtle cost leak for Plus users.

---

*Digest generated from GitHub data for openai/codex. All links point to the corresponding issue or pull request.*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-05-12

## Today’s Highlights
A nightly release fixes a PATH preservation bug in Git environments, while the community’s most vocal issue today concerns unexplained automatic quota consumption (#26860). Separately, progress continues on session-based subagent protocols and terminal paste handling, but multiple agent reliability bugs (false “GOAL” success, unused skills, stuck shell commands) remain high-priority concerns.

## Releases
**v0.42.0-nightly.20260511** — Nightly build with a single fix:  
- `fix(core): preserve system PATH in Git environment to fix ENOENT` (#26587 by @cocosheng-g). Resolves a scenario where the CLI lost the user’s PATH when spawning Git commands, causing “command not found” errors.  
No stable release in the last 24 hours.

## Hot Issues (Top 10 by Community Attention)

1. **[#26860] Automatic quota consumption without user activity** — P1 bug filed by @Neinndall. Reports that Gemini CLI uses quota automatically (15% → 28%) with no explicit requests. High emotional tone; forces urgent investigation into background processes (e.g., Auto Memory, subagent polling).  
   [Link](https://github.com/google-gemini/gemini-cli/issues/26860)

2. **[#22323] Subagent recovery after MAX_TURNS reported as GOAL success** — P1 bug with 6 comments, 2 👍. The `codebase_investigator` subagent reports `status: "success"` even when it hit the turn limit without doing analysis, masking interruptions.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22323)

3. **[#21968] Gemini does not use skills and sub-agents enough** — P2 bug with 6 comments. Users report the CLI rarely invokes custom skills or sub-agents unless explicitly instructed, despite relevant task context.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21968)

4. **[#25166] Shell command execution gets stuck with “Waiting input”** — P2 bug, 3 comments, 3 👍. After a shell command finishes, the CLI hangs showing “Awaiting user input”. Happens with trivial commands (e.g., `ls`).  
   [Link](https://github.com/google-gemini/gemini-cli/issues/25166)

5. **[#26563] Tool “save_memory” not found** — P2 bug, 5 comments. Running `/memory add` fails with `Tool "save_memory" not found` even though the memory feature is enabled. Likely a regression in tool registration.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/26563)

6. **[#21983] Browser subagent fails in Wayland** — P1 bug, 4 comments, 1 👍. The browser agent crashes on Wayland displays, terminating with GOAL but no useful output.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21983)

7. **[#24246] 400 error with > 128 tools** — P2 bug, 2 comments. CLI sends tool declarations exceeding API limits (400 → 400 error). Users expect smarter tool filtering.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/24246)

8. **[#21823] [CLOSED] Feature Request: Increase MCP tool limit from 100 to 500** — 7 comments. The limit is too low for setups with 5–7 MCP servers (e.g., Antigravity). Closed but indicates strong demand.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/21823)

9. **[#22267] Browser Agent ignores settings.json overrides** — P2 bug, 3 comments. The browser subagent does not respect `maxTurns` or other config from `settings.json`, making it hard to customize.  
   [Link](https://github.com/google-gemini/gemini-cli/issues/22267)

10. **[#22672] Agent should stop/discourage destructive behavior** — P2 feature/bug, 2 comments, 1 👍. The agent occasionally runs `git reset --force` when safer alternatives exist, risking data loss.  
    [Link](https://github.com/google-gemini/gemini-cli/issues/22672)

## Key PR Progress (Top 10 by Impact)

1. **[#26912] fix(core): detect zsh from $SHELL to prevent shopt errors** — Detects the user’s actual shell instead of hardcoding `bash`, preventing `shopt` errors on systems where `bash` is not the default.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/26912)

2. **[#26771] fix: preserve refresh token on oauth refresh** — P1 security fix. Uses a merge strategy instead of overwrite when rotating Google OAuth tokens, keeping long-running sessions valid.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/26771)

3. **[#26905] fix(cli): synthesize bracketed-paste markers for unbracketed multi-line pastes** — P1 fix for Windows Terminal / PowerShell / WSL2 where paste sequences are missing; inserts synthetic markers to prevent premature submission.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/26905)

4. **[#26361] fix(core): externalize https-proxy-agent to fix proxy support** — P1 draft PR that moves `https-proxy-agent` outside the esbuild bundle to fix `TypeError: HttpsProxyAgent is not a constructor`.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/26361)

5. **[#24736] feat(core): union-find context compaction for AgentHistoryProvider** — Introduces union-find clustering as an alternative compression strategy, moving semantically similar messages into a “cold forest” for better context management.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/24736)

6. **[#26665] feat(core): add LocalSessionInvocation and SubagentProtocols** — Adds session-based local subagent invocation and wraps A2A client / LocalAgentExecutor behind a unified `AgentProtocol` interface.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/26665)

7. **[#26770] fix(core): improve Alpine shell compatibility** — Uses `pgrep -P $$` instead of `pgrep -g 0` for BusyBox compatibility; wraps shell config lines with `[ -z ... ]` guards.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/26770)

8. **[#21963] fix(core): strip $schema from MCP tool parameters for API compatibility** — Removes `$schema` from Draft 2020-12 JSON schemas sent to the Gemini API, preventing intermittent failures while preserving local validation.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/21963)

9. **[#25444] Fix EISDIR warnings and Max Stack Size errors** — Addresses two critical modes: EISDIR when glob returns directory paths, and stack overflow when large tool results cause deep recursion.  
   [Link](https://github.com/google-gemini/gemini-cli/pull/25444)

10. **[#26420] fix(core): ignore GOOGLE_CLOUD_PROJECT for LOGIN_WITH_GOOGLE** — P2 security fix. Prevents `403 Permission Denied` errors when users have `GOOGLE_CLOUD_PROJECT` set in their `.env`.  
    [Link](https://github.com/google-gemini/gemini-cli/pull/26420)

## Feature Request Trends
- **MCP tool limit increase** – The 100-tool ceiling is repeatedly too low for multi-server setups.  
- **AST-aware file operations** – Requests for AST-based file reads, search, and codebase mapping to reduce token waste and improve navigation precision (#22745, #22746).  
- **Browser agent resilience & configuration** – Need for automatic session takeover, lock recovery, and respect for `settings.json` overrides (#22232, #22267).  
- **Progressive reading DSL for workflows** – Alternative workflow model that doesn’t expect the agent to have read all previous steps (#22424).  
- **Memory system hardening** – Stronger deduplication, invalid patch quarantine, and stop retrying low-signal sessions (#26516, #26522, #26523).  
- **Component-level evaluations** – An epic to scale behavioral eval tests beyond the current 76 and improve evaluator reliability (#24353).

## Developer Pain Points
1. **Agent autonomy failures** – Subagents either run without permission (#22093), ignore custom skills (#21968), or mask turn-limit interruptions as success (#22323).
2. **Quota and rate-limit confusion** – Unexplained automatic consumption (#26860) and 429 errors even with <10% usage (#26911) frustrate users.
3. **Shell execution instability** – Commands hang on “Waiting input” (#25166), aliases are unsupported (#21461), and Alpine/BusyBox environments break (#26770).
4. **Terminal UI glitches** – Flicker on resize (#21924), corruption after external editor (#24935), and incomplete paste handling on Windows (#26905).
5. **Configuration bypass** – Browser agent and memory settings ignored (#22267, #26525).
6. **Memory system bugs** – Invalid patches silently skipped, low-signal sessions retried forever, and secrets potentially logged (#26523, #26522, #26525).

*Digest generated from [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) activity on 2026-05-12.*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-05-12

## Today's Highlights
Version 1.0.45 shipped yesterday, introducing the `/autopilot` slash command for toggling interactive/autopilot modes and improving Windows PowerShell fallback. However, a widely anticipated `/fork` command appears to be missing from the released binary despite being listed in changelogs, sparking immediate bug reports. Model-related errors continue to dominate the issue tracker, with Claude Sonnet 4.5 and GPT sessions returning 400/transient errors.

---

## Releases
**[v1.0.45](https://github.com/github/copilot-cli/releases/tag/v1.0.45)** – *2026-05-11*  
- Added `/autopilot` slash command to switch between interactive and autopilot modes.  
- Fall back to Windows PowerShell (`powershell.exe`) when PowerShell 7+ (`pwsh`) is unavailable.  
- OpenTelemetry output now aligns with GenAI semantic conventions (MCP tool calls use standard `tool_call`).

*Note: Several users reported that the `/fork` command (listed in the changelog) is absent from this release — see Hot Issues #3252.*

---

## Hot Issues (10 notable)

1. **[#2597](https://github.com/github/copilot-cli/issues/2597) – Claude Sonnet 4.5 Listed in `/models` but returns 400 error**  
   A previously working model stopped mid-session; `CAPIError: 400 The requested model...` persists. 15 comments, high urgency for Claude users.

2. **[#2630](https://github.com/github/copilot-cli/issues/2630) – Custom agent MCP servers not connected in sub-agent or `--prompt` contexts**  
   Custom agents with `mcp-servers` in their YAML lose MCP tool access when used as sub-agents. Core agent interoperability issue.

3. **[#1148](https://github.com/github/copilot-cli/issues/1148) – CRLF line endings forced on all edited files (Windows)**  
   Long-standing bug (since 0.0.395) – any file Copilot touches gets converted to CRLF, breaking LF-only projects. 5 👍, frequent complaint.

4. **[#2058](https://github.com/github/copilot-cli/issues/2058) – Request: `/fork` command to branch sessions**  
   Top feature request (7 👍) asking for session forking to avoid derailing main objectives during side quests. Now partially addressed by v1.0.45 changelog, but release appears broken.

5. **[#98](https://github.com/github/copilot-cli/issues/98) – Integrate with `prompts/*.md`**  
   Wanted reusability of prompt files similar to VS Code Copilot custom prompts. 28 👍, one of the most upvoted feature requests.

6. **[#891](https://github.com/github/copilot-cli/issues/891) – Why is Copilot “stupider” than Claude Code with the same model?**  
   User compares Copilot CLI vs Claude Code using Opus 4.5, noting missing “plan mode” and erratic behavior. 4 comments, reflects broader quality perception.

7. **[#3181](https://github.com/github/copilot-cli/issues/3181) – Remove automatic co-author from commits**  
   Closed quickly after release, but sparked debate: many developers object to personifying AI in commit metadata.

8. **[#2338](https://github.com/github/copilot-cli/issues/2338) – Permissions from `.claude/settings.json` not honoured**  
   Despite v1.0.12 claiming support, permission blocks from settings files are ignored. Configuration regression.

9. **[#2736](https://github.com/github/copilot-cli/issues/2736) – `posix_spawnp failed` then misdiagnoses command as missing**  
   Tool execution fails with a spawn error, then Copilot incorrectly tells user the command isn’t installed. 4 👍, frustrating false negatives.

10. **[#3242](https://github.com/github/copilot-cli/issues/3242) – GPT sessions getting transient API error for PLAN features**  
    Since last week, GPT-based sessions fail to create or update plans with “Transient API error”. Model-specific regression.

---

## Key PR Progress
No pull requests were updated in the last 24 hours.

---

## Feature Request Trends

- **Session management** – `/fork` ( [#2058](https://github.com/github/copilot-cli/issues/2058) ) and rewind without git ( [#1381](https://github.com/github/copilot-cli/issues/1381) ) are the most requested session improvements.
- **Custom prompts & agents** – Reusable prompt files ( [#98](https://github.com/github/copilot-cli/issues/98) ), better MCP integration for custom agents ( [#2630](https://github.com/github/copilot-cli/issues/2630) ), and hooks for sub-agents ( [#3013](https://github.com/github/copilot-cli/issues/3013) ) are top-of-mind.
- **Transparency** – Display remaining premium usage ( [#3243](https://github.com/github/copilot-cli/issues/3243) ) and open-sourcing the CLI ( [#3241](https://github.com/github/copilot-cli/issues/3241) ) show desire for more visibility and community trust.
- **Terminal UX** – Cursor style conventions ( [#2507](https://github.com/github/copilot-cli/issues/2507) ), Vietnamese input support ( [#3251](https://github.com/github/copilot-cli/issues/3251) ), and cleaner edit diffs ( [#3249](https://github.com/github/copilot-cli/issues/3249) ) highlight platform polish gaps.

---

## Developer Pain Points

- **Model reliability** – Frequent 400 errors for specific models (Claude Sonnet 4.5, DeepSeek-V4) and transient failures for GPT plans erode trust. Users feel Copilot CLI lags behind Claude Code in quality even when using the same underlying models ( #891 ).
- **Tool execution fragility** – `posix_spawnp` failures ( [#2736](https://github.com/github/copilot-cli/issues/2736) ), orphaned `tool_use` blocks ( [#3183](https://github.com/github/copilot-cli/issues/3183) ), and the `edit` tool’s disorganised diffs ( [#3249](https://github.com/github/copilot-cli/issues/3249) ) hamper productivity.
- **Windows friction** – Forced CRLF line endings ( [#1148](https://github.com/github/copilot-cli/issues/1148) ) and native crashes with parallel sub-agents ( [#3250](https://github.com/github/copilot-cli/issues/3250) ) persist.
- **Missing or broken features** – The `/fork` command announced in v1.0.45 is non-functional ( [#3252](https://github.com/github/copilot-cli/issues/3252) ), and permission persistence across sessions is broken ( [#3253](https://github.com/github/copilot-cli/issues/3253) ).
- **Agent isolation** – Sub-agents bypass permission hooks ( [#3013](https://github.com/github/copilot-cli/issues/3013) ), and MCP token expiry mid-workflow ( [#2779](https://github.com/github/copilot-cli/issues/2779) ) causes silent failures.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the Kimi Code CLI community digest for 2026-05-12.

---

## Kimi Code CLI Community Digest | 2026-05-12

### 1. Today's Highlights
Today's activity focuses heavily on infrastructure hardening and compatibility. Key PRs address critical memory and connection leaks, while several concurrent fixes target a blocking bug for vLLM users. The community is pushing for greater extensibility, with a strong theme around making Kimi better-integratable with existing tools and workflows.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Hot Issues
- **#778 [bug] API Error: 400 "Invalid request Error"** - A persistent bug on Windows (v2.1.23) causing a 400 error. Despite 15 comments and being open since January, it remains unresolved and is a top friction point for users on that platform.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/778)

- **#2121 [enhancement] Shift + Enter for newlines** - A highly-requested UX improvement. Users find the current `Ctrl+J` shortcut unintuitive compared to the industry standard `Shift+Enter`, with one 👍 indicating support.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2121)

- **#2218 [enhancement] Support `/goal` command similar to Codex** - Seeks a command to handle long-running tasks without losing context, a common need for complex, multi-step coding sessions.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2218)

- **#2208 [enhancement] OpenAI-compatible API** - A request to expose Kimi's K2.6 model as an OpenAI-compatible endpoint for direct use in tools like Cursor. This is a significant ask for ecosystem integration.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2208)

- **#2203 [bug] AuthlibDeprecationWarning on startup** - A warning printed every time MCP servers are configured, cluttering the user's terminal. Fixed today by PR #2241.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2203)

- **#2240 [enhancement] Keep interactive mode after passing initial prompt** - Requests the `-p` option to open a shell after executing the prompt, instead of exiting. Highlights a gap between "single query" and "interactive session" workflows.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2240)

- **#2233 [bug] Empty tools array sent to vLLM during /compact** - A critical compatibility issue where `/compact` sends an empty `tools` array, which vLLM rejects. This is being addressed by multiple PRs today.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2233)

- **#2232 [enhancement] Configurable background task timeout** - Users report background tasks are killed due to overly aggressive timeout estimates, forcing them to restart. A clear request for more user control.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2232)

- **#2204 [bug] /clear command has irreversible context rotation** - The `/clear` command rotates context files but offers no way to restore them. This is a confusing user experience for those who accidentally clear their session.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2204)

- **#2234 [enhancement] Support for `extra_body` in openai_legacy provider** - Requests the ability to pass model-specific parameters (e.g., `preserve_thinking` for Qwen) through the config file, showing a need for deeper customization.
    [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2234)

### 4. Key PR Progress
- **#2242 [feat] Tool call deduplication** - Prevents redundant execution of identical tool calls within and across turns, improving stability and reducing wasted API calls.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2242)

- **#2236 [fix] Bound broadcast queues and cap web store cache** - Fixes memory leaks by limiting unbounded queues and session caches, which could cause OOM with slow consumers or high session counts.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2236)

- **#2231 [fix] Reuse TCP connectors** - Fixes connection leaks by introducing a connection pool, reducing file-descriptor exhaustion and overhead from repeated SSL handshakes.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2231)

- **#2187 [fix] Bump pillow to 12.2.0** - A security fix to resolve CVE-2026-25990, unblocking installations in security-tight environments.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2187)

- **#2241 [fix] Upgrade FastMCP OAuth storage** - Fixes the `AuthlibDeprecationWarning` by upgrading FastMCP, and updates the OAuth handling to work with the new API.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2241)

- **#2237 [feat] Add extra generation kwargs config & fix vLLM empty tools error** - Dual-purpose PR addressing issue #2233 by omitting the empty tools field for vLLM, and adds support for extra generation kwargs in the config file.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2237)

- **#2235 [fix] Omit empty tools in OpenAI legacy requests** - Another fix for issue #2233, ensuring an empty `tools` list is not serialized in requests to OpenAI-compatible APIs.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2235)

- **#2239 [fix] Continue latest persisted session** - Fixes the `--continue` flag by making it fall back to the newest non-empty session if the stored reference is stale.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2239)

- **#2226 [feat] Polish telemetry event schema** - Adds richer observability by unifying tool call events, adding lifecycle tracking for compaction, and enriching API error data.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2226)

- **#2230 [feat] Improve shell spacing, link highlighting, and notification duration** - UI polish including improved spacing, better hyperlink highlighting, and task duration displayed in notifications.
    [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2230)

### 5. Feature Request Trends
- **OpenAI/Codex Compatibility**: There is a strong desire to make Kimi CLI interoperable with the broader developer ecosystem (e.g., Cursor, Codex), including requests for OpenAI-compatible APIs and the `/goal` command.
- **Long-Running Task Management**: Users need better tools for managing complex, multi-step sessions, including configurable timeouts for background tasks and commands to persist context.
- **Enhanced Interactive Mode**: The community is asking for a more flexible interactive shell, with support for initial prompts leading into a session (`-p + interactive`) and more intuitive shortcuts (`Shift+Enter`).
- **Contextual Safety**: Users want more control over their session state, as seen in requests for reversible `/clear` commands and better session restoration workflows.

### 6. Developer Pain Points
- **API & Model Incompatibility**: Significant frustration stems from issues like the 400 error on Windows (#778) and the empty tools array bug with vLLM (#2233), which directly block productivity.
- **Lack of Configuration Depth**: Power users are hitting limits with static configurations, needing to pass custom, model-specific `extra_body` parameters and to set custom timeouts.
- **Noisy Errors & Warnings**: Deprecation warnings (#2203) and other non-fatal errors create friction, cluttering the terminal and eroding developer trust in the tool's polish.
- **Inconsistent CLI Behavior**: The behavior of flags like `-p` (exits vs. enters shell) and commands like `/clear` (irreversible rotation) creates a disconnect between user expectations and actual tool operation.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-05-12

Generated from [anomalyco/opencode](https://github.com/anomalyco/opencode)

---

## Today's Highlights

The community is grappling with model compatibility issues (Opus 4.6 prefill errors and double compaction for Opus 4.7) and persistent Bun crashes on Windows. Several patches landed to fix CJK text handling in the TUI and resolve startup hangs caused by symlinked `.git` directories. A new background job service was proposed to improve async reliability, while ecosystem docs gained another project (Legax) and a new MiniMax OAuth provider integration.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

Picked 10 noteworthy issues based on comment activity, severity, and community resonance.

### 1. [#13768 – Opus 4.6 prefill error](https://github.com/anomalyco/opencode/issues/13768)
**Comments: 63 | 👍: 27**  
Users of Opus 4.6 via GitHub Copilot consistently hit `This model does not support assistant message prefill`. The model’s API constraints are not properly handled, forcing frequent session restarts. High upvotes indicate a wide impact.

### 2. [#8785 – Bun has crashed (Windows)](https://github.com/anomalyco/opencode/issues/8785)
**Comments: 39 | 👍: 7**  
A persistent internal assertion failure in Bun (v1.3.5) on Windows x64. The crash occurs randomnly during normal session use. Multiple duplicates exist; the team has been investigating for months.

### 3. [#1735 – `max_tokens` defaults to 32,000 when using custom provider](https://github.com/anomalyco/opencode/issues/1735)
**Comments: 15 | 👍: 10**  
Users of OpenAI-compatible gateways report that `max_tokens` defaults to 32,000 regardless of the model’s true limit, causing excessive token consumption. The community wants per-provider overrides.

### 4. [#23628 – Square Root Boundary for Context Compression Loss Detection](https://github.com/anomalyco/opencode/issues/23628)
**Comments: 15 | 👍: 0**  
A feature request to add simple numeric indicators (compression loss boundary, task redundancy) to monitor context window health. Though low upvotes, it triggered thoughtful discussion on context management.

### 5. [#25270 – Model generates identical response twice](https://github.com/anomalyco/opencode/issues/25270)
**Comments: 13 | 👍: 1**  
A bug where the model outputs the exact same assistant message twice, wasting tokens and confusing the conversation flow. Likely related to retry logic or streaming deduplication.

### 6. [#26230 – Double compaction for Copilot Opus 4.7](https://github.com/anomalyco/opencode/issues/26230)
**Comments: 7 | 👍: 1**  
With Opus 4.7 via Copilot, OpenCode recently started triggering compaction twice, causing sudden token usage jumps from 100K to over 200K. The issue appears in 1.14.x builds.

### 7. [#26321 – Desktop shell tool uses minimal PATH (macOS)](https://github.com/anomalyco/opencode/issues/26321)
**Comments: 7 | 👍: 3**  
When using the Desktop app on macOS, the shell tool sees only `/usr/bin:/bin:/usr/sbin:/sbin` instead of the full zsh PATH. Homebrew tools and other user-installed binaries become invisible. The CLI mode works fine.

### 8. [#26716 – CJK and unicode symbols preceding `@` break mention autocomplete](https://github.com/anomalyco/opencode/issues/26716)
**Comments: 5 | 👍: 0**  
In the TUI, `@` mention autocomplete fails when preceded by Chinese characters or emoji. The bug affects all wide-character locales and has been fixed in [PR #27017](#27017) and [PR #26922](#26922).

### 9. [#27037 – Auto-compaction is invisible to the model → duplicate summaries](https://github.com/anomalyco/opencode/issues/27037)
**Comments: 1 | 👍: 0**  
A newly filed issue (today) highlighting that automatic compaction sends a prompt as a regular user message with no marking. The model treats it as a genuine question, generating a summary that duplicates existing context. This wastes tokens and breaks continuity.

### 10. [#26981 – TUI hangs when `.git` is a symlink (Android `repo` tool)](https://github.com/anomalyco/opencode/issues/26981)
**Comments: 2 | 👍: 0**  
OpenCode TUI goes completely blank when launched inside a project where `.git` is a symlink (common in AOSP/repo workspaces). The issue is addressed in [PR #27016](#27016).

---

## Key PR Progress

Picked 10 important PRs covering bug fixes, new features, and infrastructure improvements.

### 1. [#27017 – Fix cursor math for wide characters](https://github.com/anomalyco/opencode/pull/27017)
**Closed**  
Replaces `String.length` with `Bun.stringWidth` to correctly measure display columns for CJK characters and emoji. Fixes the `@` mention bug and misaligned cursors. A direct fix for #26716.

### 2. [#26922 – Fix TUI CJK mention autocomplete offsets](https://github.com/anomalyco/opencode/pull/26922)
**Closed**  
Another CJK fix, adjusting `cursorOffset` after wide characters. Closes #26816, #26889, and #20852 – a comprehensive patch for east-Asian text input.

### 3. [#27029 – Remember selected model variant when switching sessions/projects](https://github.com/anomalyco/opencode/pull/27029)
**Closed**  
Improves model resolution logic so that a manually selected variant (e.g., "Opus 4.7 Fast") persists across session/project switches instead of falling back to the default.

### 4. [#27033 – Add background job service](https://github.com/anomalyco/opencode/pull/27033)
**Open**  
Introduces a per-instance Effect-based background job service with `start/get/list/wait/cancel`. Covers completion, timeout, failure, cancellation, and snapshot immutability. A foundational change for async plugin operations.

### 5. [#19961 – Fire `system.transform` before `messages.transform`](https://github.com/anomalyco/opencode/pull/19961)
**Open**  
Reorders plugin hooks so that system transforms (e.g., system prompt modifications) run before message transforms. Fixes a class of plugin compatibility bugs where order of operations mattered.

### 6. [#25706 – Add FastRouter as an LLM provider](https://github.com/anomalyco/opencode/pull/25706)
**Open**  
Adds FastRouter, an OpenAI-compatible routing gateway, following the same integration pattern as OpenRouter. Increases provider diversity for users behind routing proxies.

### 7. [#23299 – Prevent subagent type hallucination with validation guard](https://github.com/anomalyco/opencode/pull/23299)
**Open**  
The Task tool prompt contained fictional example agents (`code-reviewer`, `greeting-responder`) that models copied verbatim. This PR adds a validation guard to reject hallucinated subagent types.

### 8. [#27011 – Add MiniMax OAuth device code flow plugin](https://github.com/anomalyco/opencode/pull/27011)
**Open**  
A new provider integration for MiniMax (api.minimax.io) with OAuth device code flow, supporting global and China domains. Valuable for users of MiniMax models.

### 9. [#27016 – Fix watcher: resolve symlinked `.git` path before subscribing](https://github.com/anomalyco/opencode/pull/27016)
**Open**  
Fixes the file watcher to call `realpath()` on `.git` before `inotify_add_watch`, preventing the TUI hang when `.git` is a symlink (Android repo tool). Closes #26981.

### 10. [#27034 – Filter archived sessions from per-project session list](https://github.com/anomalyco/opencode/pull/27034)
**Open**  
The per-project session listing was returning all sessions including archived ones. This PR applies a filter to hide archived sessions, matching the expected behavior from the global session list.

---

## Feature Request Trends

Distilled from all recent issues, the most requested feature directions are:

- **Web/Desktop UX enhancements** – Configurable browser launch behavior, mobile touch optimization, animated auto-follow during streaming, and copy image from clipboard to model.
- **Subagent & workflow customization** – Allowing `subagent_type` to accept user-defined agents (custom subagents via Task tool) and improving Task tool reliability (hallucination guard, model validation).
- **Context window introspection** – Tools to detect compression loss and task redundancy (e.g., square root boundary), and making auto-compaction visible to the model to avoid duplicate summaries.
- **Provider flexibility** – More OAuth providers (MiniMax, FastRouter) and fixing provider-specific issues (custom provider defaults, missing models in subagent context).
- **Internationalization** – Fixes for CJK/wide character handling in the TUI (already being addressed).

---

## Developer Pain Points

Recurring frustrations from high-frequency or high-comment-count issues:

- **Model compatibility** – Opus 4.6/4.7 prefill errors, double compaction, and duplicate responses plague users who rely on state-of-the-art models.
- **Bun crashes on Windows** – Random internal assertion failures that crash the entire application, undoing session progress.
- **Environment inconsistency** – Desktop app uses a minimal `PATH` (macOS) and installer duplicates to `APPDATA` instead of custom install directories.
- **Poor CJK/unicode support** – Broken `@` mentions, misaligned cursors, and offset errors in the TUI for non-Latin scripts.
- **Symlink-related startup hangs** – Projects using Android `repo` tool or NFS-mounted directories become unusable because of unresolved symlinks in file watchers and skill discovery.
- **Provider errors** – `ProviderModelNotFoundError` for models that work via CLI, validation failures for whitespace-only content, and missing `max_tokens` overrides.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-05-12

## Today’s Highlights
Activity surged ahead of an imminent major refactor (tagged `closed-because-bigrefactor`/`closed-because-refactor`), with a high volume of bug reports and feature requests being triaged. The most critical news is a **compromised Mistral package (v2.2.4)** affecting users on pi-mono’s dependency chain, though the project itself pins to v2.2.1. Meanwhile, the **Anthropic SSE parser bug** (#4381) and a **stale Azure OpenAI api-version** (#2528) continue to block enterprise deployments, and a **big refactor** of the TUI and provider layers is clearly underway, closing dozens of issues.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (10 most noteworthy)

1. **#4381 [CLOSED] Anthropic SSE parser ignores events when `event:` line is missing**  
   *Why it matters*: Blocks custom AI gateways that conform to SSE spec but omit optional `event:` fields; affected users report silent stream drops. Community: 7 comments, high engagement.  
   [Link](https://github.com/earendil-works/pi/issues/4381)

2. **#2528 [CLOSED] Azure OpenAI endpoints return 404 (missing api-version)**  
   *Why it matters*: Azure users cannot use the standard `openai-completions` provider because the client omits the required `?api-version=` parameter. Stalled since March despite 1 👍.  
   [Link](https://github.com/earendil-works/pi/issues/2528)

3. **#4210 [OPEN] Bedrock converse-stream: empty end_turn with 0 tokens treated as successful stop**  
   *Why it matters*: Causes silent agent halts on AWS Bedrock; user built a custom extension to remediate locally. 6 comments, suggests widespread frustration.  
   [Link](https://github.com/earendil-works/pi/issues/4210)

4. **#4406 [OPEN] tui.input.newLine has no working default binding on GNOME Terminal**  
   *Why it matters*: Core usability issue on Ubuntu/Linux; users cannot insert new lines in input. 4 comments, no resolution yet.  
   [Link](https://github.com/earendil-works/pi/issues/4406)

5. **#4180 [CLOSED] Links not clickable anymore**  
   *Why it matters*: Recent update (likely from the big refactor) broke URL clickability in TUI, a regression for many developers. 5 comments.  
   [Link](https://github.com/earendil-works/pi/issues/4180)

6. **#4408 [CLOSED] Writing long files fails with “The file was truncated”**  
   *Why it matters*: Affects users with local models (Qwen3.6, Gemma4) when writing large files; the agent prematurely truncates output and retries. 3 comments.  
   [Link](https://github.com/earendil-works/pi/issues/4408)

7. **#4432 [OPEN] Mistral package 2.2.4 compromised**  
   *Why it matters*: Security alert; pi-mono is on v2.2.1 so not directly impacted, but the community must verify dependencies. 1 comment, 1 👍.  
   [Link](https://github.com/earendil-works/pi/issues/4432)

8. **#4399 [CLOSED] Fresh install on Windows fails with no clear error**  
   *Why it matters*: Blocks Windows adoption; users on Node 26.1 get silent exits. 4 comments, still unresolved despite closure.  
   [Link](https://github.com/earendil-works/pi/issues/4399)

9. **#4158 [CLOSED] TUI markdown nested-list double indent never matches shipped truecolor themes**  
   *Why it matters*: Visual bug in markdown rendering that compounds with depth, making nested lists unreadable. 4 comments.  
   [Link](https://github.com/earendil-works/pi/issues/4158)

10. **#4437 [CLOSED] Kitty keyboard protocol breaks IME dead-key composition**  
    *Why it matters*: Breaks input for non-Latin scripts (Greek punctuation, etc.) when Kitty protocol is active. 1 comment, but severe for international users.  
    [Link](https://github.com/earendil-works/pi/issues/4437)

---

## Key PR Progress (all 7 PRs)

1. **#4434 [CLOSED] Codex/focus input on conversation switch**  
   *Summary*: Fixes input focus after switching conversations in the web UI.  
   [Link](https://github.com/earendil-works/pi/pull/4434)

2. **#4383 [OPEN] fix(coding-agent) docs: update tool configuration API in SDK docs**  
   *Summary*: Replaces outdated `readTool`, `bashTool` examples with modern `createAgentSession({ tools })` API. Resolves #4375.  
   [Link](https://github.com/earendil-works/pi/pull/4383)

3. **#4426 [OPEN] fix(coding-agent): restore terminal on uncaught exception**  
   *Summary*: Adds `uncaughtException` handler to restore TUI raw mode and cursor; prevents garbled terminal after crashes.  
   [Link](https://github.com/earendil-works/pi/pull/4426)

4. **#4421 [CLOSED] feat(coding-agent): add gbrain memory extension**  
   *Summary*: Integrates gbrain semantic memory into Pi coding agent lifecycle; before_agent_start injects memories, session_shutdown saves summaries.  
   [Link](https://github.com/earendil-works/pi/pull/4421)

5. **#4419 [CLOSED] fix(ai): restore Vertex AI ADC URL routing for native endpoints**  
   *Summary*: Fixes #3699 – restores routing for Vertex AI Application Default Credentials to native endpoints.  
   [Link](https://github.com/earendil-works/pi/pull/4419)

6. **#4417 [CLOSED] feat(organization-agent): add Agent Company package and product docs**  
   *Summary*: New `packages/organization-agent` with implementation, tests, and npm-packaged docs (`PRODUCT_INTRODUCTION.md`, `PRODUCT_USER_GUIDE.md`).  
   [Link](https://github.com/earendil-works/pi/pull/4417)

7. **#4409 [CLOSED] Sammorrowdrums/cache safe lazy tools**  
   *Summary*: Accidental cross-fork PR; no actual changes. Intended as self-PR.  
   [Link](https://github.com/earendil-works/pi/pull/4409)

---

## Feature Request Trends

- **Enhanced session/resume UX** (#4438): Allow `-r` to accept a session ID directly and skip the interactive picker.
- **Timing metadata per message part** (#4317): Track timing for `thinking`, `text`, and `toolCall` blocks separately.
- **Non-scrolling output while user is reading** (#4403): Prevent automatic cursor jump to bottom when user has scrolled up.
- **TUI rendering profiling** (#4440): Tools to measure CPU usage in rendering pipeline.
- **Symlinked context file dedup** (#4436): Avoid loading symlinked project context twice by canonicalizing paths.
- **OAuth token support for Anthropic** (#3591): Add `CLAUDE_CODE_OAUTH_TOKEN` env var for headless CI.

---

## Developer Pain Points

- **SSE/streaming robustness**: Multiple issues (#4381, #4433, #4210) show that edge cases in SSE parsing, empty events, and premature stream ends cause silent failures or hard crashes.
- **Provider-specific API quirks**: Azure’s `api-version` (#2528), Bedrock’s empty `end_turn` (#4210), and Harmony response format corrupting tool names (#4439) frustrate users of non-standard backends.
- **TUI rendering regressions**: Broken links (#4180), nested-list double indentation (#4158), missing newline keys (#4406), and markdown depth-limit crashes (#4222) degrade the terminal experience.
- **Cross-platform / IME issues**: Windows silent install failure (#4399), GNOME Terminal keybinding gaps (#4406), Kitty protocol breaking IME (#4437), and the `ß` character rendering bug (#4400) highlight incomplete platform testing.
- **Resource exhaustion in long sessions**: `write ENOBUFS` (#4382), maximum call stack (#4222), and file truncation with large content (#4408) indicate memory/stack limits are often hit.
- **Big refactor churn**: Over 15 issues closed with `closed-because-refactor` or `closed-because-bigrefactor` in the last few days alone, creating instability for users on the main branch.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，这是一份基于您提供的GitHub数据生成的Qwen Code社区摘要。

---

## Qwen Code Community Digest - 2026-05-12

### Today's Highlights
The Qwen Code team released two preview versions focusing on core performance improvements through smarter session metadata handling. Simultaneously, the community is actively discussing a major proposal for a `qwen serve` daemon mode and expressing significant frustration over UI regressions, specifically an infinite scroll/refresh loop on terminals and the loss of inline-code highlighting in wrapped tables.

### Releases
- **v0.15.11-preview.0 & v0.15.11-preview.1**: These two preview releases focus on performance and testing. The core `[perf(core)]` change from `@qqqys` optimizes how session list metadata is read. It now reads only the head and tail 64KB of the file, uses a pooled buffer, and computes the message count lazily. This should significantly improve load times for users with long session histories. A change to stabilize end-to-end tests was also included.

### Hot Issues
1.  **[[#3803](https://github.com/QwenLM/qwen-code/issues/3803)] Daemon mode (`qwen serve`): A 24-chapter proposal outlines a complete architecture for a long-running server process. This is a major feature direction, with the community and a dedicated PR already in progress.**
2.  **[[#3838](https://github.com/QwenLM/qwen-code/issues/3838)] Terminal Infinite Scroll/Refresh Loop: A high-pain UI issue causing the terminal to flicker and the scrollbar to grow infinitely when the model outputs code. Users confirm it's a rendering bug, not a model issue, impacting readability.**
3.  **[[#3730](https://github.com/QwenLM/qwen-code/issues/3730)] Auto Stop Task Command: A critical bug where Qwen Code automatically instructs the user to stop long-running tasks without user input. This is a major regression for users working on heavy projects.**
4.  **[[#3548](https://github.com/QwenLM/qwen-code/issues/3548)] Configurable `plansDirectory` for Plan Mode: A popular feature request to align with competitors like Gemini CLI and Claude Code, enabling project-specific plan storage. A PR is already open.**
5.  **[[#4035](https://github.com/QwenLM/qwen-code/issues/4035)] DashScope International Endpoint Failure: A network-level bug where the HTTP client (undici) fails to connect to the international DashScope endpoint, blocking all users in Singapore and other regions.**
6.  **[[#4077](https://github.com/QwenLM/qwen-code/issues/4077)] `read_file` Content Rendering Mismatch: A frustrating tool bug where `read_file` adds its own rendering (e.g., YAML/ Markdown headers) to the file content, causing `edit` tools to fail because they try to match the rendered text instead of the actual file.**
7.  **[[#4055](https://github.com/QwenLM/qwen-code/issues/4055)] Model Stuck in Thinking Loop: A user reports a critical breakdown where Qwen Code enters an infinite "thinking" loop for 15+ minutes on a simple request, making the tool completely unresponsive.**
8.  **[[#4079](https://github.com/QwenLM/qwen-code/issues/4079)] `--quiet-restore` Flag: A high-quality UX request to suppress the verbose printing of entire session history when resuming a conversation, which can cause minutes of scrolling. A PR is already merged.**
9.  **[[#3338](https://github.com/QwenLM/qwen-code/issues/3338)] GLM-5.1 Model Tool Output Hallucination: A cross-model compatibility bug where the GLM-5.1 model claims it received no output from shell commands, even when the session logs clearly show a successful result.**
10. **[[#4063](https://github.com/QwenLM/qwen-code/issues/4063)] Core Architecture Review: A developer-initiated deep-dive issue listing 14 structural problems in the `core` and `cli` packages, including type system contamination from `@google/genai` and high complexity. This signals community interest in long-term maintainability.**

### Key PR Progress
1.  **[[#3889](https://github.com/QwenLM/qwen-code/pull/3889)] `qwen serve` Daemon (Stage 1): Implements the first stage of the daemon mode, creating an HTTP + SSE server and an SDK `DaemonClient`. This is a foundational PR for the new architecture.**
2.  **[[#4064](https://github.com/QwenLM/qwen-code/pull/4064)] Rewind with File Restoration: A major UX enhancement allowing the `/rewind` command to also roll back file changes made by the assistant, not just conversation history. This closes a long-standing gap.**
3.  **[[#4083](https://github.com/QwenLM/qwen-code/pull/4083)] Revert Ink 7 to 6: A critical emergency fix to resolve a TUI-breaking regression caused by a seemingly safe upgrade. This directly addresses the infinite refresh loop reported in issue #3838.**
4.  **[[#3941](https://github.com/QwenLM/qwen-code/pull/3941)] Virtual Viewport for Long Conversations: A performance fix addressing the issue where rendering 1000+ message conversations caused the UI to freeze or lag due to full re-renders.**
5.  **[[#4073](https://github.com/QwenLM/qwen-code/pull/4073)] Generic Git Worktree Support: A significant new feature for agent isolation, allowing the AI to create and work in temporary `git worktrees` for safer, more isolated execution.**
6.  **[[#4085](https://github.com/QwenLM/qwen-code/pull/4085)] `--quiet-restore` Flag: Directly implements the feature requested in issue #4079, providing a much-needed option for a clean, non-scrolling session resume experience.**
7.  **[[#4062](https://github.com/QwenLM/qwen-code/pull/4062)] Configurable Plans Directory: Implements the popular feature from issue #3548, allowing users to store plan mode files in a project-specific directory.**
8.  **[[#4037](https://github.com/QwenLM/qwen-code/pull/4037)] OSC 8 Hyperlinks for Wrapped URLs: A clever fix for a common terminal issue where long URLs break across lines. Wrapping them in OSC 8 escape sequences ensures they remain clickable.**
9.  **[[#4059](https://github.com/QwenLM/qwen-code/pull/4059)] Text Selection & Ctrl+Backspace Fix: Addresses input field usability issues, including a fix for the `Ctrl+Backspace` key combination on Windows MinTTY terminals.**
10. **[[#4082](https://github.com/QwenLM/qwen-code/pull/4082)] Readline Ctrl+P/N for History Navigation: Adds GNU-Readline-style shortcuts (Ctrl+P/N) for navigating input history, improving the experience for Mac/Linux users who prefer Emacs keybindings.**

### Feature Request Trends
- **Daemon/Server Mode:** The most significant feature in development. The community is actively driving a `qwen serve` proposal (`#3803`) to enable Qwen Code to run as a persistent background service.
- **Enhanced Terminal UX:** Users are demanding a smoother, more responsive terminal experience. Requests include a `--quiet-restore` flag (`#4079`), readline/Emacs keybindings (`#3821`), and the virtual viewport for long conversations (`#3941`).
- **Configurability & Competition Parity:** The community wants settings that match established tools like Claude Code and Gemini CLI, including a configurable `plansDirectory` (`#3548`) and `browser-use` tool integration (`#4034`).
- **Session & History Management:** A clear focus on making session handling more robust. Highlights include the `worktree` isolation feature (`#4073`), better rewind support including file restoration (`#4064`), and being able to rewind sessions even after compression (`#4046`).
- **Robust Third-Party Model Support:** There is a recurring theme of issues around using non-Qwen models (e.g., GLM-5.1 from Zhipu AI), indicating a desire for better and more reliable integration with the broader LLM ecosystem.

### Developer Pain Points
- **Regressions from Updates:** One of the most pressing issues is the high frequency of regressions introduced by new releases. The "auto stop task" (`#3730`), infinite scroll loop (`#3838`), and the Ink 7 rendering regression (`#3838`) all point to a need for more robust testing before wider rollout.
- **Third-Party Model Unreliability:** Developers using non-Qwen models face a disproportionate number of frustrating bugs, such as the "tool call output hallucination" (`#3338`, `#4076`) and authentication/connection failures (`#4035`).
- **High Resource Consumption and Crashes:** Users are reporting tools that consume excessive CPU/power while waiting for external processes (`#4033`) and get stuck in "thinking" loops that make Qwen Code completely unusable without manual intervention (`#4055`).
- **Tool Implementation Flaws:** Specific tools like `read_file` and `edit` have subtle but destructive bugs. The `read_file` rendering mismatch (`#4077`) directly breaks the downstream `edit` tool, creating a frustrating chain of failures.
- **Documentation and Credential Confusion:** Errors related to authentication and credentials, such as the `401 invalid access token` error (`#3704`) and the `/login` fallback behavior (`#2795`), suggest that the setup and documentation for different authentication modes could be clearer.
- **Keybinding and Terminal Compatibility:** Issues with missing or broken keybindings (Ctrl+Backspace, Ctrl+P/N) and problems across different terminal emulators (WSL, MinTTY, macOS) are a common source of friction for users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*