# AI CLI 工具社区动态日报 2026-05-09

> 生成时间: 2026-05-09 07:22 UTC | 覆盖工具: 8 个

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

## 横向对比

好的，作为一名专注于 AI 开发工具生态的资深技术分析师，我为您整理了基于 2026 年 5 月 9 日各主流 AI CLI 工具社区动态的横向对比分析报告。

---

# AI CLI 工具生态横向对比分析报告 (2026-05-09)

## 1. 生态全景

当前 AI CLI 工具生态正处于 **“高速发展、痛点集中”** 的阶段。各工具版本迭代频繁（仅 Claude Code 一日三更），社区极度活跃，但基础设施的稳定性与可靠性是普遍短板。认证 (OAuth)、会话管理、平台兼容性 (尤其 Windows)、以及自定义模型 (BYOK) 的适配成为各工具社区共同的核心痛点。相比于追逐新功能，开发者目前更迫切地希望解决“用起来不卡壳”的基础体验问题，这标志着该领域正从早期的功能探索期，进入到需要打磨产品成熟度的深水区。

## 2. 各工具活跃度对比

| 工具 (Tool) | 今日 Issues (Top 热度) | 今日 PR 进展 | 版本发布 (Releases) | 整体活跃度 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 极高（多个 20+ 评论/赞的 Issue） | 高 (6个) | 高 (3个维护版本) | ★★★★★ |
| **OpenAI Codex** | 高 (10个，含57条评论的Bug) | 非常高 (10个，含核心重构) | 高 (1个正式版 + 多个Alpha) | ★★★★★ |
| **Gemini CLI** | 高 (10个，含16条评论的Bug) | 高 (10个，含安全修复) | 暂无 (主要是PR活动) | ★★★★☆ |
| **GitHub Copilot CLI**| 中 (10个，涵盖多个方向) | 低 (2个) | 中 (2个维护版本) | ★★★☆☆ |
| **Kimi Code CLI** | 中 (10个，集中在Windows) | 高 (10个，含多项修复) | 暂无 | ★★★★☆ |
| **OpenCode** | 高 (10个，含44赞的YOLO模式) | 高 (10个，含多项功能) | 暂无 | ★★★★☆ |
| **Pi** | 高 (10个，含多种终端兼容性) | 高 (10个，含新功能) | 暂无 | ★★★☆☆ |
| **Qwen Code** | 中 (10个，认证与API连接问题多) | 高 (10个，含架构重构) | 中 (4个版本，含Preview) | ★★★★☆ |

**解读**: **Claude Code** 和 **OpenAI Codex** 凭借其庞大的用户基数和活跃的社区讨论，稳居第一梯队。**OpenCode**、**Gemini CLI** 和 **Kimi Code CLI** 社区活跃度极高，呈现出快速迭代和追赶态势。**Pi** 专注于解决特定痛点，**Qwen Code** 则在积极进行内部架构升级。

## 3. 共同关注的功能方向

社区反馈的共性需求高度集中，揭示了当前 AI CLI 工具的基础设施层短板：

- **MCP (Model Context Protocol) 生态的稳定性与易用性**:
    - **工具**: Claude Code, OpenAI Codex, GitHub Copilot CLI, Kimi Code CLI, Qwen Code
    - **具体诉求**: MCP 服务器的认证卡死、配置失效、工具反复要求审批、插件崩溃、重启后消失等问题是重灾区。用户迫切需要“信任一次”的白名单机制和稳定的连接。

- **会话管理 & 上下文持久化**:
    - **工具**: Claude Code, OpenCode, Pi, Gemini CLI
    - **具体诉求**: 会话与项目路径强绑定导致移动后历史丢失 (`/resume` 失效)；TUI 会话列表只显示近期记录；不希望会话数据被自动注入虚假消息（如压缩后恢复）。

- **跳过权限/一键执行 (YOLO模式)**:
    - **工具**: OpenCode (`--dangerously-skip-permissions`), Claude Code (`hard_deny` 的反向需求), GitHub Copilot CLI (BYOK)
    - **具体诉求**: 在自动化脚本或信任环境中，频繁的权限弹窗严重打断工作流。开发者希望有一个全局性的跳过权限、直接执行的模式。

- **本地模型 / BYOK (Bring Your Own Key) 集成堵点**:
    - **工具**: OpenAI Codex (沙箱GPU), Pi (LM Studio), Qwen Code (OpenRouter), GitHub Copilot CLI (Azure, vLLM)
    - **具体诉求**: 本地模型 (如 vLLM, LM Studio) 的工具调用格式不兼容 (`tool_choice` 对象 vs 字符串)、`Reasoning` 字段名称不一致、SDK 自动读取与模型不匹配的环境变量。本地化/自托管方案的适配困难是普遍问题。

- **安全审计与漏洞修复**:
    - **工具**: Gemini CLI (换行注入绕过HITL), GitHub Copilot CLI (PowerShell 触发SIEM告警, `$home` 变量误删用户目录)
    - **具体诉求**: Agent 生成恶意脚本或绕过安全控制的风险是企业用户的核心担忧。更透明的操作日志和更严谨的沙箱/权限策略是持续需求。

## 4. 差异化定位分析

| 工具 (Tool) | 核心定位 | 差异化优势 | 目标用户/场景 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **最强Agent + MCP生态** | 模型能力 (Opus) 领先，自动模式、MCP生态最丰富，企业级功能 (Otel)完善。 | 追求极致代码生成质量和复杂任务自动化、愿意付费的高端开发者。 |
| **OpenAI Codex** | **平台化与安全沙箱** | 强大的沙箱隔离、Python SDK 基础设施扎实（今日重构），强调函数调用和Plugins生态。 | 企业级用户，重视安全合规和组织级管控。 |
| **GitHub Copilot CLI**| **GitHub 生态深度融合** | 深度集成 GitHub Actions、Codespaces、Copilot 市场，主打 BYOK 和自定义 Agent 扩展。 | 重度依赖 GitHub 生态的团队。 |
| **Gemini CLI** | **多Agent协作与长上下文** | 强调 Agent 间的协作与委派 (Subagent)，追求超大上下文（1M token），内置 Browser Agent。 | 需要处理大型代码库、复杂多步骤任务的开发者。 |
| **Kimi / Qwen Code** | **中国本土优化与开源** | 对国内模型 (Moonshot, 通义千问) 友好，社区以中文为主，积极适配 Windows 问题。 | 主要面向中国开发者，使用国产云服务或开源模型的用户。 |
| **OpenCode** | **社区驱动的全能型替代** | 开源，社区驱动力强，功能全面 (Agent、TUI、WebUI)，快速跟进市场趋势 (如YOLO模式)。 | 偏好开源、希望掌控配置、不依赖单一供应商的开发者。 |
| **Pi** | **极简高效与终端兼容** | 追求轻量级、跨终端兼容性最佳，macOS 体验优秀，支持图像粘贴等原生功能。 | 对性能敏感，追求简洁高效，在多种终端环境下工作的开发者。 |

## 5. 社区热度与成熟度

- **成熟度领先**: **Claude Code** 和 **GitHub Copilot CLI** 用户基数最大，社区讨论最前沿，但 Issue 管理也面临挑战（陈年老 Bug 多）。**Claude Code** 的问题更为复杂和深入（如远程控制、OAuth 竞态）。
- **快速迭代期**: **OpenAI Codex**、**OpenCode**、**Kimi Code CLI**、**Qwen Code** 和 **Pi** 正处于功能和架构的快速迭代期，发布和 PR 活动频繁，社区对新功能和 Bug 修复的响应速度很快。**OpenAI Codex** 的 Python SDK 重构标志其平台化野心。**OpenCode** 的 YOLO 模式获得 44 个赞，反应了社区对效率的极致渴望。
- **追赶期**: **Gemini CLI** 虽然活跃，但 Issue 暴露出其在 Agent 行为稳定性和结果报告准确性上的不足，成熟度相对较低，急需解决基础可靠性问题。

## 6. 值得关注的趋势信号

1.  **基础设施问题仍是最大阻碍**: 社区最激烈的讨论并非来自“AI 能做什么”，而是“为什么连不上”、“为什么不执行”、“为什么数据丢失了”。认证、会话、权限、平台兼容性等基础设施的完善度，将是决定工具能否从小众走向主流的**关键胜负手**。
2.  **MCP 成为超级入口，但稳定性堪忧**: MCP 被认为是未来 AI 工具与外部世界交互的“万能插座”，但当前各工具的 MCP 认证、配置、可靠性问题集中爆发。这意味着 MCP 协议本身在走向成熟前，还需要大量的工具链和 SDK 打磨。
3.  **“安全”与“效率”的博弈加剧**: 从 OpenCode 的 `YOLO` 模式到 Gemini CLI 的 HITL 绕过漏洞，社区对“效率优先”和“安全优先”的两种哲学分歧明显。如何设计一个既不打断工作流又能保障安全的**灵活的权限体系**，是所有工具的共同挑战。
4.  **开源 vs 商业化路径分化**: 以 OpenCode 为代表的开源工具在功能创新和社区响应上展现出巨大活力，威胁着商业工具的领跑地位。而 Claude Code 和 Copilot CLI 则通过深度绑定底层模型（如 Opus）和企业级服务（如 BYOK、企业认证）来构建护城河。两种模式各有市场，但**开源社区的快速迭代能力不容小觑**。
5.  **对开发者意味着什么**:
    - **短期**: 如果追求最佳开箱体验和最高代码质量，**Claude Code** 仍是首选，但需忍受其认证和计费流程的阵痛。
    - **中期**: 若身处微软/GitHub 生态，**Copilot CLI** 的集成优势无可比拟；若需要强大的沙箱和安全管控，**OpenAI Codex** 是值得投入的方向。
    - **长期**: **OpenCode** 等开源工具提供了最灵活、最可定制的选择，建议技术实力强的团队持续关注并为其贡献。所有工具的开发者都应重点关注 **MCP 生态** 的标准化进程，并准备好应对 Agent 行为安全和可审计性的挑战。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-05-09）

## 1. 热门 Skills 排行（按评论数排序 Top 8）

### 1️⃣ #514 — `document-typography`：AI 生成文档排版质量控制
- **功能**：防止 AI 生成文档中的常见排版问题（孤字换行、孤段悬挂、编号错位），提升输出专业性。
- **讨论热点**：社区高度认可这一痛点——“所有 Claude 生成的文档几乎都受到影响”，是提升 AI 输出质量的刚需。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/514)

### 2️⃣ #83 — `skill-quality-analyzer` + `skill-security-analyzer`：元技能质量与安全评估
- **功能**：对 Claude Skills 进行质量评级（五维度评分）和安全漏洞检测。属于“自检”型元技能。
- **讨论热点**：社区关注 Skill 标准化治理，自然引发了关于“谁审查 Skill 质量”的深层思考。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/83)

### 3️⃣ #210 — 改进 `frontend-design` 技能清晰度与可操作性
- **功能**：重写前端设计技能，确保每个指令 Claude 都能在单次对话中执行，减少歧义。
- **讨论热点**：社区关注 Skill 的可执行性——不是写给人看的文档，而是 Claude 的真实操作手册。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/210)

### 4️⃣ #486 — 新增 `odt` 技能：OpenDocument 格式处理
- **功能**：支持创建/填充/读取/转换 ODT、ODS 等 ISO 标准开放文档格式，对接 LibreOffice 生态。
- **讨论热点**：从微软 Office 格式到开源生态的扩展，反映了用户对文档格式多样性的需求。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/486)

### 5️⃣ #538 — 修复 `pdf` 技能中大小写敏感的文件引用
- **功能**：解决 SKILL.md 中 8 处大小写不匹配导致的跨平台（Linux/macOS）引用失败问题。
- **讨论热点**：虽然是小修，但暴露了 Skills 仓库在文件引用规范上的隐患，引发对跨平台兼容性的关注。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/538)

### 6️⃣ #541 — 修复 `docx` 技能中 tracked changes 的 ID 冲突
- **功能**：修复 OOXML 文档因 `w:id` 硬编码与已存在的书签冲突导致的文档损坏。
- **讨论热点**：技术深度较高，社区关注文档格式操作中的“边界情况”处理。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/541)

### 7️⃣ #539 — 修复 `skill-creator` 对未引号描述的 YAML 解析预警
- **功能**：在 YAML 加载前检查 `description` 字段中是否含有未引号包裹的冒号，防止静默解析失败。
- **讨论热点**：Skill 自身验证能力的增强，是社区对 Skill 质量工具链的呼声。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/539)

### 8️⃣ #181 — 新增 `SAP-RPT-1-OSS` 企业级预测分析技能
- **功能**：集成 SAP 开源的表格基础模型，对企业 SAP 业务数据进行预测分析。
- **讨论热点**：社区关注企业级 AI 集成，特别是与 SAP 这类大型 ERP 系统的对接。
- **状态**：🟢 OPEN
- [查看 PR](https://github.com/anthropics/skills/pull/181)

---

## 2. 社区需求趋势（从 Issues 提炼）

### 趋势一：技能管理和组织共享
- **核心诉求**：一个组织内的技能应能直接共享，而非手动下载/上传（Issue #228，👍7）。反映团队协作场景的强烈需求。
- **相关 Issue**：[#228](https://github.com/anthropics/skills/issues/228)

### 趋势二：Skill Creator 工具链质量提升
- **核心诉求**：当前 `skill-creator` 效率低下、描述优化依赖 API 密钥、验证不充分。社区要求其从“文档”变为“真正可执行”的工具（Issue #202、#532）。
- **相关 Issue**：[#202](https://github.com/anthropics/skills/issues/202)、[#532](https://github.com/anthropics/skills/issues/532)

### 趋势三：安全与信任边界
- **核心诉求**：社区技能在 `anthropic/` 命名空间下发布，容易冒充官方，存在信任边界被突破的风险（Issue #492）。呼吁安全审查机制。
- **相关 Issue**：[#492](https://github.com/anthropics/skills/issues/492)

### 趋势四：插件安装机制稳定性
- **核心诉求**：`document-skills` 和 `example-skills` 插件安装重复内容（Issue #189）、`run_eval.py` 触发率 0%（Issue #556）等系统级问题频发。
- **相关 Issue**：[#189](https://github.com/anthropics/skills/issues/189)、[#556](https://github.com/anthropics/skills/issues/556)

### 趋势五：技能数据持久性与平台兼容性
- **核心诉求**：技能突然消失（Issue #62）、与 Amazon Bedrock 集成困难（Issue #29）、平台 404/500 错误（Issue #61、#406、#184）。
- **相关 Issue**：[#62](https://github.com/anthropics/skills/issues/62)、[#29](https://github.com/anthropics/skills/issues/29)、[#61](https://github.com/anthropics/skills/issues/61)

### 趋势六：代理治理与安全模式
- **核心诉求**：社区提出了 `agent-governance` 的技能提案（Issue #412），要求建立 AI 代理系统的政策执行、威胁检测、信任评分等治理模式。
- **相关 Issue**：[#412](https://github.com/anthropics/skills/issues/412)

---

## 3. 高潜力待合并 Skills（活跃但未合并的 PR）

这些 PR 讨论热度高、功能明确，有望近期落地：

| PR | Skill | 亮点 | 状态 | 链接 |
|----|-------|------|------|------|
| #514 | `document-typography` | 明显痛点，覆盖所有 AI 文档生成场景 | OPEN | [查看](https://github.com/anthropics/skills/pull/514) |
| #83 | 技能质量/安全分析器 | 元技能，填补治理空白 | OPEN | [查看](https://github.com/anthropics/skills/pull/83) |
| #486 | `odt` 开放文档格式 | 开源生态支持，LibreOffice 用户刚需 | OPEN | [查看](https://github.com/anthropics/skills/pull/486) |
| #181 | SAP 预测分析 | 企业级用户热盼的 ERP 集成能力 | OPEN | [查看](https://github.com/anthropics/skills/pull/181) |
| #723 | `testing-patterns` | 测试 Trophy 模型 + 全栈测试覆盖 | OPEN | [查看](https://github.com/anthropics/skills/pull/723) |
| #568 | ServiceNow 全平台 | 企业 IT 服务管理 AI 化，覆盖 ITSM/ITOM 等 | OPEN | [查看](https://github.com/anthropics/skills/pull/568) |
| #509 | `CONTRIBUTING.md` | 补齐社区健康度工具链 | OPEN | [查看](https://github.com/anthropics/skills/pull/509) |

---

## 4. Skills 生态洞察

> **一句话总结**：当前社区最强烈的诉求并非新增功能 Skill，而是**完善技能治理、工具链稳定性和组织级协作机制**——用户迫切需要一个“可信、稳定、可共享”的 Skills 生态基础，而非单纯的功能扩展。

---

好的，作为一名专注于 AI 开发工具的技术分析师，我为您整理了 2026 年 5 月 9 日的 Claude Code 社区动态日报。

---

# 2026-05-09 Claude Code 社区动态日报

---

## 今日速览

今日版本更新以内部修复和 Windows VSCode 兼容性修补为主。社区最关注的议题集中在 **MCP 服务器认证与配置问题** 以及 **会话管理的路径依赖缺陷** 上。此外，多起关于订阅升级失败的 Bug 显示出计费系统存在反复出现的稳定性问题。

---

## 版本发布

过去 24 小时内密集发布了 3 个维护版本（v2.1.136 - v2.1.138），均为小版本迭代。

### v2.1.138
- **主要更新**：内部修复。
- **链接**: [https://github.com/anthropics/claude-code/releases/tag/v2.1.138](https://github.com/anthropics/claude-code/releases/tag/v2.1.138)

### v2.1.137
- **主要更新**：
    - **[VSCode] 修复了扩展在 Windows 上无法激活的问题。** 此修复解决了 Windows 用户的一个关键阻塞点，确保扩展能正常启动。
- **链接**: [https://github.com/anthropics/claude-code/releases/tag/v2.1.137](https://github.com/anthropics/claude-code/releases/tag/v2.1.137)

### v2.1.136
- **主要更新**：
    - **新增 `CLAUDE_CODE_ENABLE_FEEDBACK_SURVEY_FOR_OTEL` 环境变量**：允许通过 OpenTelemetry 捕获会话质量调查的企业用户重新启用此功能，增强了企业级可观测性。
    - **新增 `settings.autoMode.hard_deny` 设置**：为自动模式分类器提供了无条件阻止的规则，无论用户意图或允许情况如何。此功能增强了安全性和控制力，特别适用于敏感环境。
- **链接**: [https://github.com/anthropics/claude-code/releases/tag/v2.1.136](https://github.com/anthropics/claude-code/releases/tag/v2.1.136)

---

## 社区热点 Issues（Top 10）

以下是过去 24 小时内更新、讨论最热烈或最具代表性的 10 个 Issue。

1.  **#28758: [BUG] 远程控制：手机端无法连接到会话**
    - **重要性**: 高。远程控制是重要的移动办公场景，该问题直接影响了核心功能的可用性。
    - **社区反应**: 28 条评论，36 个赞，用户反馈强烈。问题持续超过 2 个月，目前仍为开放状态。
    - **链接**: [https://github.com/anthropics/claude-code/issues/28758](https://github.com/anthropics/claude-code/issues/28758)

2.  **#24317: [BUG] 多并发会话导致频繁重新认证 (OAuth Refresh Token 竞态)**
    - **重要性**: 极高。影响团队协作和高级用户的工作流，OAuth 令牌竞争是严重的基础设施错误。40 个赞表明了广泛的受影响面。
    - **状态**: 已关闭，但仍有 20 条评论，推测可能已通过其他方式（如版本更新）解决或标记为已知问题。是社区高度关注的历史性问题。
    - **链接**: [https://github.com/anthropics/claude-code/issues/24317](https://github.com/anthropics/claude-code/issues/24317)

3.  **#12531: [BUG] macOS Brew 升级后需要绕过安全设置才能启动**
    - **重要性**: 高。macOS 用户的关键阻塞点，破坏了正常的软件包管理器升级体验，影响开发者对新版本的采用。
    - **社区反应**: 16 条评论，持续超过 5 个月仍未解决，表明这可能是一个复杂的签名或公证问题。
    - **链接**: [https://github.com/anthropics/claude-code/issues/12531](https://github.com/anthropics/claude-code/issues/12531)

4.  **#53872: [BUG] Opus 4.7 [1M] 上下文被服务器端限制在 500K**
    - **重要性**: 高。直接影响付费用户的核心价值——超大上下文能力。6 个赞表明该问题已引起用户对实际可用上下文窗口的质疑。
    - **社区反应**: 12 条评论，用户报告尝试全新安装后问题依旧，问题根因可能在于服务器端缓存了过时的组织级别标识。
    - **链接**: [https://github.com/anthropics/claude-code/issues/53872](https://github.com/anthropics/claude-code/issues/53872)

5.  **#54204: [BUG] Max 5x → Max 20x 升级卡在”无效发票“循环**
    - **重要性**: 高。严重阻碍用户升级订阅，损害收入转化。服务器反复返回已取消的 `PaymentIntent`，表明后端状态处理存在问题。
    - **社区反应**: 16 条评论，用户表示沮丧。
    - **链接**: [https://github.com/anthropics/claude-code/issues/54204](https://github.com/anthropics/claude-code/issues/54204)

6.  **#55266: [BUG] Max 5x → Max 20x 升级失败 "Unable to update subscription"**
    - **重要性**: 高。与 #54204 类似，揭示了订阅升级流程的普遍性问题。已被标记为重复，表明这是一个已知的系统性问题。
    - **社区反应**: 10 条评论。
    - **链接**: [https://github.com/anthropics/claude-code/issues/55266](https://github.com/anthropics/claude-code/issues/55266)

7.  **#25762: [FEAT] 添加环境变量配置 `.claude` 配置目录位置**
    - **重要性**: 中。解决跨机器使用共享主目录场景的特定需求，29 个赞表明具有广泛的需求基础，是提升用户体验的重要改进。
    - **社区反应**: 11 条评论，社区积极讨论方案。
    - **链接**: [https://github.com/anthropics/claude-code/issues/25762](https://github.com/anthropics/claude-code/issues/25762)

8.  **#57365: [BUG] Chrome 扩展 v1.0.70: 无限 OAuth 重试循环导致 403 和侧面板闪烁**
    - **重要性**: 高。Chrome 扩展是重要的客户端形式，无限认证循环和 UI 闪烁严重影响体验，甚至导致强制登出。
    - **社区反应**: 今日新创建的 Issue，很快获得 8 条评论，已引起开发团队的注意。
    - **链接**: [https://github.com/anthropics/claude-code/issues/57365](https://github.com/anthropics/claude-code/issues/57365)

9.  **#41630: [FEAT] 会话身份应与项目路径解耦**
    - **重要性**: 中。这是一个重要的架构或体验改进建议，指出当前的会话 History 绑定在项目目录路径上，路径变更会丢失所有历史记录，严重影响 `/resume` 等功能。
    - **社区反应**: 6 条评论，讨论涉及 git worktree 等高级场景。
    - **链接**: [https://github.com/anthropics/claude-code/issues/41630](https://github.com/anthropics/claude-code/issues/41630)

10. **#36814: [FEAT] 支持 WhatsApp 频道（对标 Telegram/Discord）**
    - **重要性**: 中。在已有的 Telegram 和 Discord 集成基础上，社区提出增加 WhatsApp ，反映出对移动端和泛化沟通渠道的强烈需求。
    - **社区反应**: 6 条评论，8 个赞。
    - **链接**: [https://github.com/anthropics/claude-code/issues/36814](https://github.com/anthropics/claude-code/issues/36814)

---

## 重要 PR 进展

过去 24 小时内有 6 个 PR 被更新，主要集中在 CI/CD 流程维护和文档更新上。

1. **#34735: [OPEN] ci: update actions**
    - **重要性**: 高。持续集成是项目健康发展的基石，更新 actions 有助于提升构建和测试流程的稳定性和安全性。
    - **链接**: [https://github.com/anthropics/claude-code/pull/34735](https://github.com/anthropics/claude-code/pull/34735)

2. **#14842: [OPEN] fix: update documentation links to point to the new Claude Code site**
    - **重要性**: 高。确保用户能访问正确的文档是提升开发者体验的基础，持续更新文档链接体现了对项目发布流程的维护。
    - **链接**: [https://github.com/anthropics/claude-code/pull/14842](https://github.com/anthropics/claude-code/pull/14842)

3. **#56784: [CLOSED] Pin GitHub Actions to commit SHAs**
    - **重要性**: 高。将第三方 GitHub Actions 锁定到不可变的提交 SHA 能显著提升 CI/CD 管道的安全性，防止供应链攻击。
    - **链接**: [https://github.com/anthropics/claude-code/pull/56784](https://github.com/anthropics/claude-code/pull/56784)

4. **#57267: [OPEN] Fix pagination in stale issue auto-close sweep**
    - **重要性**: 中。修复维护 Robot 的分页逻辑，能更有效地关闭过时 Issue，保持 Issue 追踪器的整洁，降低社区噪音。
    - **链接**: [https://github.com/anthropics/claude-code/pull/57267](https://github.com/anthropics/claude-code/pull/57267)

5. **#57333: [OPEN] Update README.md**
    - **重要性**: 低。README 的更新通常涉及项目简介或入门指引的变更，属于常规维护。
    - **链接**: [https://github.com/anthropics/claude-code/pull/57333](https://github.com/anthropics/claude-code/pull/57333)

6. **#57223: [CLOSED] feat(frontend-design): add Superpowers Process Gate before implementation**
    - **重要性**: 低。此 PR 建议在前端设计文档的 SKILL.md 中添加一个”流程关卡“，强制实施超能力方法论中的“头脑风暴 → 计划 → 可视化TDD → 审查”流程，属于流程与文档规范类改进。
    - **链接**: [https://github.com/anthropics/claude-code/pull/57223](https://github.com/anthropics/claude-code/pull/57223)

---

## 功能需求趋势

从今日的 Issue 中，我们可以提炼出社区最关注的几个功能方向：

1.  **MCP (Model Context Protocol) 深度集成与体验优化**：大量关于 MCP 服务器认证、权限、配置和连接的 Bug 与 Feature Request（如 #42359, #45875, #57291, #57496, #36814），说明 MCP 是当前生态发展的核心，但用户体验和稳定性仍亟待加强。
2.  **会话与状态管理的灵活性**：社区强烈希望解决会话历史与工作目录的强绑定问题（#41630），并期望通过环境变量自定义配置目录（#25762），体现了用户对于更灵活、可移植工作流的需求。
3.  **更好的远程控制与协作能力**：移动端远程控制连接失败（#28758）和微信/WhatsApp 等即时通讯渠道的集成请求（#36814），表明社区渴望更强大的跨设备、跨平台工作能力。
4.  **提升使用的可观测性与控制力**：v2.1.136 支持 OpenTelemetry 调查和新增 `hard_deny` 规则，是对企业级用户和管理者需求的回应。社区对工具输出默认展开、影响回顾体验的抱怨（#56423）也反映了对 UI/UX 精细控制的需求。
5.  **订阅与计费系统的稳定性**：多个关于 Max Plan 升级失败的重复 Bug（#54204, #55266），凸显出计费流程是用户体验中的痛点，用户对无法顺利升级感到沮丧。

---

## 开发者关注点

综合来看，开发者在此次社区动态中反馈了以下核心痛点：

- **MCP 相关 Bug 是最大热点**：MCP 服务器的认证（OAuth 流程卡死、令牌刷新问题）、配置（Token 错误、插件崩溃）和状态持久化（每次重启后内置 MCP 服务器消失）是问题重灾区。这严重影响了依赖 MCP 扩展 Claude 能力的开发者。
- **OAuth 和认证问题频发**：从多会话竞争导致频繁重新认证（#24317）到登出命令不生效（#57285），再到 Chrome 扩展的无限重试（#57365），认证系统的健壮性是开发者抱怨的集中点。
- **升级与计费体验不佳**：从 Max 5x 升级到 20x 的过程充满障碍，服务器端逻辑错误导致支付卡死或失败，这直接触及付费用户的利益，影响信任度。
- **对会话管理和配置灵活性的渴望**：`/resume` 功能在路径变更后失效、无法自定义配置目录，这些问题破坏了开发者依赖的“上下文连续性”，降低了工作效率。
- **macOS 和 Windows 平台的兼容性**：macOS brew 升级后的安全问题（#12531）和 Windows VSCode 扩展激活失败（v2.1.137 修复），表明平台特定问题仍然需要持续关注。
- **随机性和不可预测的 Bug**：工具执行挂起（#57550）、Hook 在执行后才触发（#57548）等不易复现的 Bug 让开发者对工具的可靠性产生疑虑。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-05-09）

---

## 今日速览

Codex 发布 **0.130.0 正式版**，带来插件详情增强、远程控制入口等新功能，同时多个 0.131.0 内部 Alpha 版本正在快速迭代。社区对 **远程 compact 任务失败** 和 **沙箱 GPU 支持** 的讨论热度最高；Python SDK 基础架构迎来重要重构，包括依赖锁定、类型生成和 CI 集成。

---

## 版本发布

### rust-v0.130.0 正式版
- **插件详情** 现可展示已绑定的 hooks；插件分享支持链接元数据及可发现性控制。
- 新增 `codex remote-control` 命令，作为启动无头、可远程控制的应用服务器的简化入口。
- 应用服务器客户端功能进一步增强（描述截断，详见 Release 页面）。

此外，过去 24 小时内连续发布了 **rust-v0.131.0-alpha.1/2/4** 及 **0.130.0-alpha.5/7/10** 等预发布版本，表明开发团队正在为 0.131.0 系列进行密集迭代。

GitHub: [Releases 页](https://github.com/openai/codex/releases)

---

## 社区热点 Issues（10 个）

1. **#14860 – Error running remote compact task**  
   - 评论 57 | 👍 38  
   - 影响 Pro 用户使用 `gpt-5.4` 模型进行远程压缩时失败，为当前最活跃的 Bug 报告。  
   - [Issue 链接](https://github.com/openai/codex/issues/14860)

2. **#3141 – Allow GPU access inside sandbox**  
   - 评论 35 | 👍 43  
   - 持续近 8 个月的增强请求，Linux 沙箱阻断 NVIDIA GPU 调用，限制 AI 开发工作流。  
   - [Issue 链接](https://github.com/openai/codex/issues/3141)

3. **#20552 – Toggle File Tree 不可靠**  
   - 评论 28 | 👍 7  
   - macOS 桌面版“视图 > 切换文件树”功能偶尔无法生效，影响日常操作。  
   - [Issue 链接](https://github.com/openai/codex/issues/20552)

4. **#10726 – CLI 滚动问题（Windows/WSL）**  
   - 评论 27 | 👍 12  
   - Windows 下 TUI 终端滚动异常，用户需要频繁手动调整。  
   - [Issue 链接](https://github.com/openai/codex/issues/10726)

5. **#12115 – 动态加载嵌套 AGENTS.md**  
   - 评论 15 | 👍 46  
   - 社区强烈希望 Codex 能像 Claude Code 那样按需加载子目录中的 AGENTS.md，减少初始上下文开销。  
   - [Issue 链接](https://github.com/openai/codex/issues/12115)

6. **#19910 – Goals 功能在中途压缩后丢失提示与审计需求**  
   - 评论 13 | 👍 0  
   - 新 Goals 功能在 mid-turn compaction 后丢失“活跃目标继续提示”和审计要求，影响任务完整性。  
   - [Issue 链接](https://github.com/openai/codex/issues/19910)

7. **#21671 – 0.129.0 /compact 因 `service_tier` 参数失败**  
   - 评论 10 | 👍 3  
   - 升级后 `/compact` 报未知参数错误，属于回归问题，已关闭但值得关注。  
   - [Issue 链接](https://github.com/openai/codex/issues/21671)

8. **#12098 – 标签页式并行聊天会话（IDE 扩展）**  
   - 评论 7 | 👍 21  
   - 用户希望在 VS Code / Cursor 扩展中获得类似浏览器的标签页切换体验，提升多会话效率。  
   - [Issue 链接](https://github.com/openai/codex/issues/12098)

9. **#21527 – Codex 反应缓慢**  
   - 评论 7 | 👍 3  
   - 用户反馈无论是桌面版还是 VS Code 插件，模型响应速度过慢，性能亟待优化。  
   - [Issue 链接](https://github.com/openai/codex/issues/21527)

10. **#16911 – MCP 工具持续要求审批**  
    - 评论 6 | 👍 9  
    - 每次调用 MCP 工具都弹窗确认，打断工作流，用户希望有“信任一次”或白名单机制。  
    - [Issue 链接](https://github.com/openai/codex/issues/16911)

---

## 重要 PR 进展（10 个）

1. **#21812 / #21891 / #21893 / #21895 – Python SDK 基础建设 (栈)**  
   - 锁定 Python SDK 运行时依赖 → 从锁定运行时生成 API 类型 → 在 CI 中运行 SDK 测试。同时发布运行时 wheel。  
   - [PR #21812](https://github.com/openai/codex/pull/21812) | [#21891](https://github.com/openai/codex/pull/21891) | [#21893](https://github.com/openai/codex/pull/21893) | [#21895](https://github.com/openai/codex/pull/21895)

2. **#18202 – Windows 沙箱拒绝读取策略**  
   - 为 Windows 实现与 Linux/macOS 一致的 deny-read 文件系统策略，企业级管控跨平台对齐。  
   - [PR 链接](https://github.com/openai/codex/pull/18202)

3. **#19506 – 根据 CWD 变化刷新 AGENTS.md**  
   - 每次 turn 根据当前工作目录重新加载 AGENTS.md，而非沿用会话开始时的版本。  
   - [PR 链接](https://github.com/openai/codex/pull/19506)

4. **#19471 – Windows 沙箱测试使用 serial_test**  
   - 以 `serial_test` 替代自制互斥体，简化 Windows 沙箱进程测试的序列化逻辑。  
   - [PR 链接](https://github.com/openai/codex/pull/19471)

5. **#19462 – Python SDK 使用独立 codex-app-server 运行时**  
   - 让 Python SDK 直接启动 `codex-app-server` 二进制，而非经过 `codex app-server` 命令，减少依赖。  
   - [PR 链接](https://github.com/openai/codex/pull/19462)

6. **#18431 – macOS 设备密钥提供者**  
   - 为 macOS 添加基于 Secure Enclave 的私钥存储能力，保障设备密钥非导出性。  
   - [PR 链接](https://github.com/openai/codex/pull/18431)

7. **#19377 – 分离 session_id 与 thread_id**  
   - 多智能体 v2 线程需要区分会话级标识和线程级标识，此 PR 重构了 Responses 请求中的身份字段。  
   - [PR 链接](https://github.com/openai/codex/pull/19377)

8. **#21844 – 忽略 /tmp 下的陈旧 .git 标记**  
   - 项目发现阶段忽略 `/tmp` 等 sticky 目录中的 `.git` 文件，避免误判项目根目录。  
   - [PR 链接](https://github.com/openai/codex/pull/21844)

9. **#21870 – TUI 避免因 agent 元数据阻塞**  
   - 修复大型子智能体扇出时 TUI 因等待 metadata 导致冻结的问题，提升交互流畅度。  
   - [PR 链接](https://github.com/openai/codex/pull/21870)

10. **#21854 – 保留工具参数的空 JSON Schema**  
    - 修复 MCP/动态工具中空 JSON Schema `{}` 被错误推断为 `string` 的 bug，确保工具参数约束正确。  
    - [PR 链接](https://github.com/openai/codex/pull/21854)

---

## 功能需求趋势

从过去 24 小时的 Issues 中可提炼出社区最关注的四大方向：

1. **沙箱与权限增强** – GPU 访问（#3141）、Windows 沙箱读写策略、MCP 工具信任机制、writable gitdir 等需求高频出现。
2. **上下文与 AGENTS.md 优化** – 动态加载嵌套 AGENTS.md（#12115）、按目录刷新指令、多 agent 元数据开销等问题持续热议。
3. **IDE 集成与 UI 体验** – 标签页式并行聊天（#12098）、文件树可靠切换（#20552）、目录预览窗口（#13646）等请求受关注。
4. **性能与稳定性** – 整体响应速度（#21527）、远程 compact 失败（#14860）、滚动/闪烁等 TUI Bug 是开发者最直接的痛点。

此外，Windows 平台兼容性（多个 #windows-os 标签 Issue）仍是持续攻坚领域。

---

## 开发者关注点

- **远程 compact 任务失败** 影响 Pro 用户日常压缩操作，评论达 57 条，是当前最紧迫的 Bug。
- **沙箱 GPU 阻断** 严重阻碍依赖 GPU 的 AI 开发场景，获得社区 43 个 👍。
- **Goals 功能丢失提示** 属于新功能副作用，开发者期待快速修复。
- **MCP 工具反复弹窗审批** 破坏自动化工作流，用户呼吁“信任一次”机制。
- **性能抱怨** 集中在模型响应延迟，可能涉及模型选择或后端调度。
- **Windows 特定问题** 包括滚动异常、Chrome 插件不稳定、HTTP 回调被拦截等，Windows 用户群体感受到的摩擦较多。
- **认证与令牌** 刷新令牌失效、Xcode 登录回调被 Safari 阻断等问题仍时有发生。

> **建议关注**：0.131.0 Alpha 版本正在密集发布，可能包含上述许多修复与增强，建议主动跟踪预发布版本以提前验证。

---

*数据来源：GitHub openai/codex，截止 2026-05-09 23:59 UTC。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，这是为您准备的 2026-05-09 Gemini CLI 社区动态日报。

---

## Gemini CLI 社区动态日报 | 2026-05-09

### 今日速览

今日社区动态聚焦于 **Agent 行为稳定性与安全性**。多个高评论数 Issue 指向了 Agent 任务报告误导（如“成功”掩盖了中断）和拒绝调用自定义技能的问题。安全方面，一项已合并的 PR 修复了通过换行注入绕过人工确认的严重漏洞。此外，社区对 **Memory 子系统** 的 Bug 修复和性能优化（如流式读取防止崩溃）也有持续贡献。

### 社区热点 Issues

1.  **#21925: Gemini CLI 显示错误“需要操作”图标**
    - **重要性**: 该问题已开放近两个月，引发最多讨论（16条评论）。它描述了一个非常影响使用体验的Bug：CLI 在执行耗时较长的 Shell 脚本后，会错误地显示等待用户输入的手形图标，导致用户困惑并打断工作流。
    - **链接**: [Issue #21925](https://github.com/google-gemini/gemini-cli/issues/21925)

2.  **#22323: 子Agent达到最大轮次后被误报为“成功”**
    - **重要性**: 一个严重的误导性问题。当子Agent（如 `codebase_investigator`）因达到 `MAX_TURNS` 而被迫中断时，系统向上层报告的结果是“成功”（`status: "success"`）和“目标达成”（`Termination Reason: "GOAL"`），完全掩盖了实际的中断和任务失败。这会严重影响基于该结果的后续决策。
    - **链接**: [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)

3.  **#21968: Gemini 自主使用技能和子Agent的意愿不足**
    - **重要性**: 社区用户反馈的一个核心 Agent 行为问题。用户报告称，即使配置了自定义的 Git 或 Gradle 技能，Gemini 在自主模式下也极少主动调用它们，除非被显式指令要求。这表明 Agent 的自主推理与工具选择能力存在优化空间。
    - **链接**: [Issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)

4.  **#26563: `/memory add` 命令因缺失 `save_memory` 工具失败**
    - **重要性**: 一个最近（5月6日）出现的新Bug，引起了5条评论的关注。用户在 v0.41.1 版本中使用 `/memory add` 命令时，系统报错 `Tool "save_memory" not found`，导致 Memory 功能的核心写入操作失效。
    - **链接**: [Issue #26563](https://github.com/google-gemini/gemini-cli/issues/26563)

5.  **#24916: Gemini CLI 反复要求同一文件的权限**
    - **重要性**: 用户痛点非常明确：“允许”指令（包括“允许所有未来会话”）有时不生效，导致 CLI 反复请求对相同文件的访问权限，严重干扰开发流程。
    - **链接**: [Issue #24916](https://github.com/google-gemini/gemini-cli/issues/24916)

6.  **#25166: Shell 命令执行完毕后卡在“等待输入”状态**
    - **重要性**: 3个 👍 值表明这是一个普遍性问题。即使用户执行一个立即返回的简单 Shell 命令，CLI 有时也会卡死，错误地显示命令仍在执行并等待用户输入，影响后续操作。
    - **链接**: [Issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)

7.  **#26516: Memory 系统的 Bug 与质量改进（追踪）**
    - **重要性**: 这是一个综合性的 Issue，由一位社区贡献者（`SandyTao520`）创建，用于追踪 Memory 子系统的一系列问题。这包括无效补丁处理、低质量会话无限重试、日志泄露等多个细分问题，表明 Memory 系统当前处于集中改进期。
    - **链接**: [Issue #26516](https://github.com/google-gemini/gemini-cli/issues/26516)

8.  **#22203: 提议将“ToDo”重命名为“Tasks”**
    - **重要性**: 一个关于 UI/UX 的简洁改进。社区建议将列表盘中的 `ToDo` 标签改为 `Tasks`，使功能命名更直观、更通用，反映了社区对细节体验的关注。
    - **链接**: [Issue #22203](https://github.com/google-gemini/gemini-cli/issues/22203)

9.  **#23571: 模型频繁在随机位置创建临时脚本**
    - **重要性**: 这是一个开发体验问题。当限制模型只能通过 Shell 执行时，它倾向于在项目目录下生成大量临时编辑脚本，导致工作区杂乱无章，增加了用户提交代码前的清理成本。
    - **链接**: [Issue #23571](https://github.com/google-gemini/gemini-cli/issues/23571)

10. **#24935: 在 `terminalBuffer` 模式下退出外部编辑器后终端内容损坏**
    - **重要性**: 涉及到与外部编辑器集成时的界面渲染问题。用户在使用 CLI 调用外部编辑器（如 Vim）保存退出后，终端屏幕没有正确刷新，导致内容显示混乱。
    - **链接**: [Issue #24935](https://github.com/google-gemini/gemini-cli/issues/24935)

### 重要 PR 进展

1.  **#26657: 修复 JavaScript 堆内存溢出崩溃** (OPEN)
    - **内容**: 使用流式 `fs.opendir` 替代同步文件系统操作，解决了当处理大型目录时因内存耗尽导致的崩溃问题。这是对 CLI 性能与稳定性的重要改进。
    - **链接**: [PR #26657](https://github.com/google-gemini/gemini-cli/pull/26657)

2.  **#23333: 修复通过换行注入绕过人工确认的安全漏洞** (CLOSED)
    - **内容**: 这是一个关键的安全修复。攻击者可以利用 Shell 命令的换行符来隐藏恶意载荷，从而绕过“人在环路”（HITL）权限检查。此 PR 修复了此 UI 劫持漏洞，已被合并。
    - **链接**: [PR #23333](https://github.com/google-gemini/gemini-cli/issues/23433)

3.  **#24320: 修复 `web_fetch` 无法通过 Ctrl+C 中止的问题** (OPEN)
    - **内容**: 当 CLI 正在抓取网页时，用户按 `Ctrl+C` 无法立即中断操作，而是会经历长达约35秒的重试和退避过程。此 PR 旨在修复此问题，提升用户体验。
    - **链接**: [PR #24320](https://github.com/google-gemini/gemini-cli/pull/24320)

4.  **#23543: 为工具执行接入性能指标** (OPEN)
    - **内容**: 该 PR 是提升 CLI 内部可观测性的基础性工作。通过在工具执行流程中集成高精度计时器，未来可以测量单个工具调用的延迟和可靠性，为优化提供数据支撑。
    - **链接**: [PR #23543](https://github.com/google-gemini/gemini-cli/pull/23543)

5.  **#22894 & #25220: 修复 VS Code 调试配置以支持 TypeScript**
    - **内容**: 这两个 PR 都旨在解决 VS Code 下无法直接调试 `.ts` 文件的问题。它们分别通过添加 `ts-node` 或 `tsx` 支持，使得开发者能更方便地在本地环境中调试 CLI 源码。
    - **链接**: [PR #22894](https://github.com/google-gemini/gemini-cli/pull/22894)、[PR #25220](https://github.com/google-gemini/gemini-cli/pull/25220)

6.  **#25920: 修复 Windows 终端误判 TTY 丢失导致意外退出** (CLOSED)
    - **内容**: 针对 Windows 平台的特定修复。解决了在 PowerShell 或 Windows Terminal 中，因窗口调整大小、焦点切换等操作导致 `isTTY` 短暂为 `false`，从而错误触发退出流程的问题。
    - **链接**: [PR #25920](https://github.com/google-gemini/gemini-cli/pull/25920)

7.  **#26420: 修复因环境变量 `GOOGLE_CLOUD_PROJECT` 导致的登录失败** (OPEN)
    - **内容**: 当用户使用 `LOGIN_WITH_GOOGLE` 方式认证时，如果 `.env` 文件中设置了 `GOOGLE_CLOUD_PROJECT` 变量，会导致 403 权限错误。该 PR 修正了认证逻辑以忽略此环境变量。
    - **链接**: [PR #26420](https://github.com/google-gemini/gemini-cli/pull/26420)

8.  **#26692: 支持通过环境变量控制自动更新** (OPEN)
    - **内容**: 新增 `GEMINI_CLI_ENABLE_AUTO_UPDATE` 环境变量，允许用户在 Shell 级别（无需编辑 `settings.json`）控制是否启用自动更新，为无项目目录的临时运行场景提供了便利。
    - **链接**: [PR #26692](https://github.com/google-gemini/gemini-cli/pull/26692)

9.  **#26358: 在 Shell 模式下按退格键退出** (OPEN)
    - **内容**: 一个简单而人性化的改进。在输入 `!` 进入 Shell 模式后，如果用户按退格键清空输入，将自动退出 Shell 模式，符合直觉。
    - **链接**: [PR #26358](https://github.com/google-gemini/gemini-cli/pull/26358)

10. **#26698: 修复 Telemetry 因 `quota_project_id` 注入失败的问题** (OPEN)
    - **内容**: 修复了企业级功能——遥测数据上报的一个 Bug。由于未注入 `quota_project_id`，导致 Cloud Trace API 调用因使用了错误的项目而发生权限拒绝错误。
    - **链接**: [PR #26698](https://github.com/google-gemini/gemini-cli/pull/26698)

### 功能需求趋势

从今日的 Issues 和 PRs 可以提炼出社区关注的几个主要方向：

- **Agent 行为与可靠性**: 这是当前社区的绝对核心关注点。大量 Issue 指向 Agent 的**自主决策**（如何使用工具）、**结果报告**（误导性的“成功”状态）以及**任务执行稳定性**（卡死、权限循环）。
- **UI/UX 与交互体验**: 社区对界面细节有较高要求。包括**信息显示清晰度**（如并行调用布局、层级缩进）、**操作反馈准确性**（错误提示、卡死状态）和 **命名直观性**（ToDo vs. Tasks）。
- **安全性**: 特别是在企业应用场景下。安全相关的 PR 和 Issue 很受重视，从 **HITL 绕过漏洞** 的修复到 **权限管理** 的持续性问题，都表明开发者对安全性的高度担忧。
- **本地开发体验与性能**: 包括解决**内存溢出**、**Shell 集成卡住**、Windows 平台兼容性，以及提供更**便捷的调试配置**等，开发者希望 CLI 能更稳定地融入本地开发环境。
- **Memory 系统**: 近期关于 Memory（记忆）功能的 Bug 修复和特性改进非常集中，表明该功能正在经历密集的开发与打磨期。

### 开发者关注点

开发者反馈中的主要痛点和高频需求可以总结为：

- **Agent 执行过程的不可控与不可预测**: 开发者抱怨 Agent 不按预期调用工具（#21968），或者在失败时报告成功（#22323）。这暴露了 Agent 内部逻辑的不透明性，开发者需要更强的可观察性和控制力。
- **权限系统体验不佳**: 重复询问权限（#24916）是用户反复提及的痛点。当前的权限管理机制在执行效率和用户预期之间存在差距，需要更智能、更持久的授权方案。
- **环境变量干扰与配置冲突**: 多个 Issue 和 PR 都涉及环境变量（如 `GOOGLE_CLOUD_PROJECT`）对 CLI 行为（如登录、Telemetry）的意外干扰。这表明 CLI 需要对外部环境有更健壮的处理和隔离能力。
- **子Agent 行为失控**: 将用户拖入深层次的多Agent交互中，而缺乏必要的透明度和监控手段。`Browser Agent` 的无响应（#21983）和 `Subagent` 的权限失控（#22093）都是典型表现。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-05-09

## 今日速览

1. **两个补丁版本同日发布**：v1.0.44 和 v1.0.44-3 分别修复了路径补全闪烁、斜杠命令中段触发等问题，并新增了 `userPromptSubmitted` 钩子直通响应功能。
2. **BYOK & 自定义代理问题集中爆发**：多个 issue 指出 BYOK 提供商（如 vLLM）的 `reasoning` 字段未被解析、Azure 的 `wire_api: completions` 被忽略、以及自定义代理在子代理模式下无法连接 MCP 服务器，引发社区对模型兼容性和代理扩展性的强烈关注。
3. **终端渲染顽疾再起**：Emoji 表格列对齐问题和 Markdown 链接换行断裂在 v1.0.43 中依然存在，用户抱怨回退前后矛盾。

---

## 版本发布

### v1.0.44 (2026-05-08)
- **修复**：`/add-dir` 中的路径补全不再闪烁，也不被 `@` / `#` 选择器拦截。
- **改进**：斜杠命令现在可出现在输入中间，单条消息可调用多个技能。
- **新增**：`userPromptSubmitted` 钩子可绕过 LLM 直接处理请求并返回响应，实现低成本自定义逻辑。

### v1.0.44-3 (2026-05-08)
- **新增**：`userPromptSubmitted` 钩子可直接处理请求（无需模型调用）。
- **改进**：多账户用户的 `/user list` 和 `/user switch` 执行更快。

> 注意：`copilot update` 可能错误拉取预发布版本（#3203），请关注正式版通道。

---

## 社区热点 Issues（10 条）

### 1. #2630 – 自定义代理的 MCP 服务无法在子代理/`--prompt` 下连接
- **重要性**：核心扩展机制缺陷。自定义 Agent 声明的 `mcp-servers` 在通过 `task` 工具调用子代理或 `--prompt` 模式时完全不可用，仅获得基础工具。
- **社区反应**：评论 6 条，持续关注者多，属于功能阻塞级 Bug。
- [GitHub](https://github.com/github/copilot-cli/issues/2630)

### 2. #3202 – 恶意链接滥用的安全报告（已关闭）
- **重要性**：用户提交了一个 GitHub 子域名链接，可能是钓鱼/垃圾信息，CSIRT 应关注。
- **社区反应**：已标记为 invalid 并关闭，但暴露了平台滥用风险。
- [GitHub](https://github.com/github/copilot-cli/issues/3202)

### 3. #1412 – PowerShell 工具触发安全警报（Windows）
- **重要性**：企业环境中，Copilot CLI 的 PowerShell 行为（如清除 Windows 事件日志）触发 Elastic 等 SIEM 告警，导致 IT 安全团队介入。
- **社区反应**：持续开放 3 个月，用户请求提供更透明的操作日志或可配置的告警白名单。
- [GitHub](https://github.com/github/copilot-cli/issues/1412)

### 4. #1433 – `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` 环境变量无法跨目录工作
- **重要性**：Linux 上无法在 NFS 磁盘或项目外目录加载自定义 AGENTS.md 指令，影响团队共享配置。
- **社区反应**：6 个 👍，多人遇到相同问题，希望支持绝对路径或符号链接解析。
- [GitHub](https://github.com/github/copilot-cli/issues/1433)

### 5. #3189 – `copilot -p` 非交互模式静默退出（macOS）
- **重要性**：1.0.44-1 回归，非交互模式不输出任何内容，不产生日志，直接 exit 1，影响 CI/CD 和自动化脚本。
- **社区反应**：报告者提供了详细复现步骤，需紧急修复。
- [GitHub](https://github.com/github/copilot-cli/issues/3189)

### 6. #3200 – 请求 `/delegate` 支持无需提交推送本地更改
- **重要性**：用户希望在未提交代码时就能委托子代理工作，提升迭代效率。
- **社区反应**：功能请求，评论提示可通过 git stash 变通，但期待原生支持 `uncommitted` 子命令。
- [GitHub](https://github.com/github/copilot-cli/issues/3200)

### 7. #3195 – BYOK 提供商（vLLM）的 `reasoning` 字段未被处理
- **重要性**：Copilot CLI 只检查 `reasoning_content`，而 vLLM 返回 `reasoning`，导致 `AssistantReasoningEvent` 不触发，插件/钩子无法感知模型思考过程。
- **社区反应**：BYOK 用户反馈强烈，影响自定义 UI 和日志功能。
- [GitHub](https://github.com/github/copilot-cli/issues/3195)

### 8. #3208 – Azure BYOK：忽略 `wire_api: completions`，硬编码 api-version 不兼容
- **重要性**：配置为 Azure 本地补全 API 的用户被强制指向 Responses API，且 api-version 被硬编码，导致 400 错误。
- **社区反应**：企业用户依赖 Azure 合规部署，此 Bug 阻止迁移。
- [GitHub](https://github.com/github/copilot-cli/issues/3208)

### 9. #3098 – PowerShell `$home` 变量可能导致用户目录误删（Windows）
- **重要性**：Agent 生成的脚本若使用 `$home` 作为临时路径，由于 PowerShell 变量不区分大小写，会解析为 `$HOME`，执行 `Remove-Item -Recurse -Force` 时可能导致用户目录被清除。严重安全风险。
- **社区反应**：建议增加白名单或使用 `Resolve-Path` 检查。
- [GitHub](https://github.com/github/copilot-cli/issues/3098)

### 10. #3209 – 托管模式（Premium）下 Agent 不会自动调用写/编辑工具
- **重要性**：即使权限已自动允许，Agent 仍不执行 `write`/`edit`/`create_file` 工具，导致 Premium 用户无法在托管模式下生成代码。阻塞核心功能。
- **社区反应**：全新的严重 Bug，暂无评论但影响面大。
- [GitHub](https://github.com/github/copilot-cli/issues/3209)

---

## 重要 PR 进展（共 2 条）

### 1. #2800 – 添加初始 devcontainer 配置
- **功能**：为 copilot-cli 仓库添加 Dev Container 配置，方便贡献者在隔离环境中开发测试。
- **状态**：打开中，更新于 2026-05-08，评论数未提供（约为 0）。
- [GitHub](https://github.com/github/copilot-cli/pull/2800)

### 2. #3199 – 更新 Homebrew 安装命令
- **功能**：修正 Homebrew 安装文档，因为 CLI 工具已迁移到新的 Cask 地址（`copilot-cli` 和 `copilot-cli@prerelease`）。
- **状态**：打开中，更新于 2026-05-08，需要维护者合并。
- [GitHub](https://github.com/github/copilot-cli/pull/3199)

> 说明：当前 PR 仅有 2 条，未达到 10 条的上限。

---

## 功能需求趋势

从近期 Issues 中可以提炼出以下社区最关注的功能方向：

1. **外部模型提供商（BYOK）深度集成**  
   - 半数以上的高热度 Issue 与 BYOK/Azure OpenAI/vLLM 相关，包括字段解析、api-version、路由策略等。
   - 用户希望 CLI 能像 VS Code 插件一样灵活切换模型，并支持 `wire_api` 等配置。

2. **自定义 Agent 与 MCP 生态扩展**  
   - #2630、#3207 均指向自定义 Agent 的 MCP 服务器连接、注册表限制绕过等问题。
   - 社区期望获得更完善的 Agent 生命周期钩子（如 `preAgentStop` #2253）和插件热更新。

3. **安全与权限控制**  
   - Windows 下的 `$home` 变量误删除、PowerShell 安全警报、非交互模式静默退出等表现出对安全审计和沙箱的需求。
   - 企业用户希望 CLI 在操作前能更清晰地提示文件路径变更。

4. **终端渲染与兼容性**  
   - Emoji 表格对齐（#3205）、Markdown 链接换行（#3204）、状态栏自定义命令不生效（#3192）等持续困扰用户，反映出终端渲染引擎仍需打磨。

5. **跨平台输入体验**  
   - Ctrl+Backspace 键绑定丢失（#3206）、`a` 键被跳过（#3211）、符号链接路径错误（#3212）等琐碎问题表明 TUI 与各终端/键盘布局的兼容性有待加强。

---

## 开发者关注点

- **非交互模式可靠性**：`copilot -p` 在 macOS 上静默退出（#3189）导致 CI 管道中断，是当前最急需修复的 P0 问题。
- **自主写代码能力缺失**：Premium 托管模式下 Agent 不自动调用写/编辑工具（#3209），削弱了“自主编程”的核心卖点。
- **BYOK 配置复杂且易出错**：Azure `wire_api` 被忽略、`reasoning` vs `reasoning_content` 不一致，增加了企业用户的运维负担。
- **更新机制不可控**：`copilot update` 拉取预发布版本（#3203），用户希望有稳定版锁定的选项。
- **安全告警疲劳**：PowerShell 操作被 EDR/XDR 监控频繁告警（#1412），开发者希望 CLI 提供可配置的静默模式或操作白名单。
- **代理间协作受限**：`/delegate` 需要提交代码才能委托（#3200），降低了快速原型迭代的效率，社区期待 `--uncommitted` 选项。

---

*数据来源：GitHub `github/copilot-cli` 仓库，截至 2026-05-09 00:00 UTC。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-05-09

---

## 📌 今日速览

Windows 平台成为今日社区关注焦点：多个用户报告了 PowerShell 语法不兼容、`fcntl` 缺失导致终端崩溃、以及 CRLF 文件转换等问题。对应地，社区提交了改用 Git Bash 作为 Shell 后端的 PR（#2186），以及规避 `fcntl` 缺乏的修复方案。同时，WebUI 侧边栏文件名过长遮挡操作按钮的 Bug 已被紧急修复（#2207），Plan 模式乱码问题也引发广泛讨论。全局 `AGENTS.md` 功能需求获得持续关注（#2152），社区对跨项目共享约定的呼声渐高。

---

## 🐛 社区热点 Issues（Top 10）

### 1. [#2152] 支持全局 `~/.kimi/AGENTS.md` 实现多项目共享约定
- **重要性**：开发者同时维护 10+ 项目时需重复编写 AGENTS.md，该请求能极大减少冗余。
- **社区反应**：3 条评论，2 👍，讨论活跃。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2152

### 2. [#2165] 非法工具调用导致整个会话崩溃
- **重要性**：模型输出无效 JSON 后，后续请求被 OpenAI 兼容后端拒绝，会话永久失败，影响使用体验。
- **社区反应**：2 条评论，已有 PR #2196 修复。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2165

### 3. [#2178] Windows 版 kimi.exe v1.41.0 FileVersionInfo 为空，导致 VS Code 扩展拒绝识别
- **重要性**：阻碍 Windows 用户在 VS Code 中更新或使用 CLI，属于安装兼容性严重缺陷。
- **社区反应**：2 条评论，开发者在跟进。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2178

### 4. [#2189] 开启 Plan 模式后下次交互产生乱码
- **重要性**：影响模型输出可读性，且该 Bug 在最新版 VSCode 扩展中复现。
- **社区反应**：1 条评论，尚未有 PR。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2189

### 5. [#2206] WebUI 工作区文件侧边栏：长文件名隐藏操作按钮
- **重要性**：用户无法点击展开目录或下载文件，侧边栏宽度固定不可调整，属 UI 关键缺陷。
- **社区反应**：0 条评论，但已由报告者本人提交修复 PR #2207。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2206

### 6. [#2204] `/clear` 旋转上下文文件后无法恢复历史
- **重要性**：用户希望保留历史备份，但缺少恢复命令，导致可能误删有用对话上下文。
- **社区反应**：0 条评论，功能缺失明显。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2204

### 7. [#2203] 配置 MCP 服务器后每次启动打印 AuthlibDeprecationWarning
- **重要性**：影响启动日志整洁性，可能掩盖更严重错误。
- **社区反应**：0 条评论，属于持续兼容性警告。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2203

### 8. [#2202] Windows 上 `kimi term` 因缺少 `fcntl` 模块崩溃，随后次要错误干扰排错
- **重要性**：基本终端操作无法使用，且错误渲染导致调试困难。
- **社区反应**：0 条评论，Windows 独有 Bug。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2202

### 9. [#2201] WebUI 启动时 afk 选项与 `--no-restrict-sensitive-apis` 互斥
- **重要性**：用户无法同时使用自动断联和敏感 API 豁免，限制了长时间自动任务的执行。
- **社区反应**：0 条评论，逻辑冲突需重新设计。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2201

### 10. [#2195] Shell 工具命令超时固定 60 秒且不可配置
- **重要性**：长时编译、git 操作等任务频繁超时，社区要求支持自适应或可配超时。
- **社区反应**：0 条评论，但已有 PR #2200 提供自适应解决方案。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2195

---

## 🔧 重要 PR 进展（Top 10）

### 1. [#2207] fix(webui): 防止长文件名隐藏工作区文件侧边栏操作按钮
- **内容**：使用 CSS `min-width: 0` + `overflow: hidden` 解决 Radix UI 布局溢出。
- **状态**：OPEN，直接修复 Issue #2206。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2207

### 2. [#2186] refactor(windows): 将 Shell 后端从 PowerShell 切换为 git-bash
- **内容**：解决 Windows 下 Agent 生成 PowerShell 7.x 语法与默认 5.x 不兼容的问题，改为统一使用 POSIX 语义的 bash。
- **状态**：OPEN，关联 #1618、#1855。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2186

### 3. [#2177] fix(soul): 清除 LLM 步骤重试时残留的部分 UI 输出
- **内容**：Stream 出错重试时，之前显示的文本/思考/工具调用不再与后续输出拼接。
- **状态**：OPEN，提升交互体验。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2177

### 4. [#2205] fix(shell): 注册 `/btw` 斜杠命令
- **内容**：使已文档化的侧问功能 `/btw` 在 agent 模式下可作为 shell 斜杠命令正常使用。
- **状态**：OPEN，小修复（<100 行）。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2205

### 5. [#2190] feat(telemetry): 在上下文中添加 app_name 和 build_sha 远程来源追踪
- **内容**：区分 `/compact` 手动触发与带提示触发，添加构建来源信息，提升遥测可观察性。
- **状态**：OPEN。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2190

### 6. [#2200] fix(shell): 为长命令自适应超时
- **内容**：对 git submodule cleanup、clone/fetch、包安装、构建等常用慢操作自动延长超时；常规命令保持 60s 默认。
- **状态**：OPEN，解决 Issue #2195。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2200

### 7. [#2199] fix(kaos): Windows 执行时避免创建控制台窗口
- **内容**：对 Windows 本地 exec 子进程添加 `CREATE_NO_WINDOW` 标志，修复 #2197。
- **状态**：OPEN。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2199

### 8. [#2198] fix(acp): 延迟更新可用命令列表防止竞态
- **内容**：v1.41.0 中斜杠命令有时不显示，原因是 `new_session` 中过早发送命令列表。
- **状态**：OPEN。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2198

### 9. [#2196] fix(kosong): 清理历史中的非法工具调用
- **内容**：历史中模型输出的非法 JSON 导致后续请求被拒，PR 在 provider 层做健壮性处理，修复 #2165。
- **状态**：OPEN。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2196

### 10. [#2183] fix(shell): 主动处理拖入的图片路径
- **内容**：用户拖入的本地图片路径不再依赖后续 `ReadMediaFile`，直接读取并转化为 `ImageURLPart`，提高可靠性。
- **状态**：OPEN，修复 #2182。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2183

---

## 📈 功能需求趋势

1. **全局配置与约定**：要求支持 `~/.kimi/AGENTS.md` 全局规则文件，跨项目共享。
2. **Shell 工具灵活性**：超时可配置/自适应、完整支持 POSIX 语义（Windows 用户强烈需求）。
3. **上下文管理**：`/clear` 后能恢复历史备份；提供显式恢复命令。
4. **WebUI 体验**：侧边栏宽度可调、文件名溢出不遮挡操作按钮。
5. **Windows 兼容性**：主流趋势是改用 git-bash 替代 PowerShell，统一 Unix 管道语法。
6. **安全与策略**：afk 与敏感 API 豁免的逻辑冲突需重新设计。

---

## 👨‍💻 开发者关注点

- **Windows 平台痛点集中爆发**：同一用户 `lNeverl` 连续提交 5 个 Windows 相关缺陷（#2191 ~ #2195），涵盖 PowerShell 语法不兼容、CRLF 自动转换、命令超时固定、Agent 生成 Unix 管道等多方面。社区期待全面转向 git-bash 的 PR #2186 能尽快合入。
- **Shell 超时硬编码**：60 秒固定超时对编译、git 克隆等操作不够，社区希望支持自适应或用户自定义。
- **上下文旋转无恢复机制**：`/clear` 备份文件未提供 CLI 恢复命令，用户可能丢失有用会话。
- **Plan 模式乱码**：影响正常使用模型推理，目前尚无 PR，需官方定位。
- **遥测信息缺失**：构建版本号和触发来源信息不明确，社区希望增强可追踪性。
- **MCP 服务器废弃警告**：对生产环境部署有干扰，需尽快升级依赖。

---

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-05-09）

> 由 AI 开发工具技术分析师整理，基于 GitHub 数据 `anomalyco/opencode`。

---

## 今日速览

今日社区最关注的是 **Agent 市场（Marketplace）** 提案与 **“YOLO 模式”** 跳过权限提示的功能请求，两者均获得大量赞同与讨论。同时，**会话压缩导致虚假用户消息注入** 的 Bug 和 **TUI 会话列表仅显示最近记录** 的反馈持续引发共鸣，跨平台兼容性问题（Windows PATH、WSL 路径）也在加速修复。

---

## 社区热点 Issues（10 个）

### 1. [FEATURE] GitHub-based Agent Marketplace for Sharing and Discovering Agents
- **🔖 #7467** | 评论: 14 | 👍: 8  
- **摘要**: 提出构建基于 GitHub 的 Agent 市场，解决用户间手动复制 Agent 文件的低效问题。社区反响强烈，认为这是生态发展的关键一步。  
- [查看详情](https://github.com/anomalyco/opencode/issues/7467)

### 2. [FEATURE] Add `--dangerously-skip-permissions` (YOLO mode)
- **🔖 #8463** | 评论: 7 | 👍: 44  
- **摘要**: 高达 44 个赞！自动化工作流或可信环境中权限提示频繁打断流程，期望通过 CLI 参数一键跳过所有权限确认。  
- [查看详情](https://github.com/anomalyco/opencode/issues/8463)

### 3. [FEATURE] Save conversations and session data to project folder
- **🔖 #14292** | 评论: 6 | 👍: 10  
- **摘要**: 与会话数据目前保存在 `~/.opencode`，用户期望能保存到项目目录下，便于版本控制和团队协作。  
- [查看详情](https://github.com/anomalyco/opencode/issues/14292)

### 4. Compaction replay injects fake user message "What did we do so far?" causing unwanted summary generation
- **🔖 #13838** | 评论: 11 | 👍: 3  
- **摘要**: 会话压缩后恢复时自动注入虚假用户消息，导致模型生成不必要的内容总结。影响体验且浪费 Token。  
- [查看详情](https://github.com/anomalyco/opencode/issues/13838)

### 5. TUI /sessions picker only shows recent sessions
- **🔖 #13877 / #16270** | 评论: 7+6  
- **摘要**: TUI 会话选择器仅显示最近 ~5 条会话（实际数据库中有数百条），根源在于硬编码了 30 天窗口。用户呼吁支持分页和全量历史加载。  
- [查看 #13877](https://github.com/anomalyco/opencode/issues/13877) | [查看 #16270](https://github.com/anomalyco/opencode/issues/16270)

### 6. Tool execution aborted/terminated（与 LM Studio 本地模型相关）
- **🔖 #26063** | 评论: 7 | 👍: 0  
- **摘要**: 使用本地 LM Studio 部署的 Qwen 模型时，工具执行频繁被终止。反映本地模型兼容性仍需优化。  
- [查看详情](https://github.com/anomalyco/opencode/issues/26063)

### 7. Desktop app shell tool uses minimal PATH while CLI preserves zsh PATH
- **🔖 #26321** | 评论: 4 | 👍: 2  
- **摘要**: macOS 上桌面应用调用 shell 工具时仅使用极简 PATH（`/usr/bin:/bin`），导致 Homebrew 命令找不到。影响使用第三方工具的自动化任务。  
- [查看详情](https://github.com/anomalyco/opencode/issues/26321)

### 8. [FEATURE] Add page-based navigation for browsing conversation history in TUI
- **🔖 #26327** | 评论: 5 | 👍: 0  
- **摘要**: 直接回应当前会话历史浏览痛点，建议引入 Page Up/Down 分页导航，提升长列表浏览效率。  
- [查看详情](https://github.com/anomalyco/opencode/issues/26327)

### 9. /skill-name doesn’t invoke full skill system
- **🔖 #24831** | 评论: 5 | 👍: 0  
- **摘要**: 使用 `/skill-name` 命令时仅复制基础 prompt，未触发完整技能系统（无法加载引用文件等），导致技能失效。  
- [查看详情](https://github.com/anomalyco/opencode/issues/24831)

### 10. Sessions missing from sidebar on Windows due to path separator mismatch
- **🔖 #23864** | 评论: 3 | 👍: 0  
- **摘要**: Windows 平台上子代理创建的会话因路径分隔符（`\` vs `/`）不匹配而无法在 Web UI 侧边栏显示，只能通过直接 URL 访问。  
- [查看详情](https://github.com/anomalyco/opencode/issues/23864)

---

## 重要 PR 进展（10 个）

### 1. fix(session): prevent double compaction after auto-compact
- **🔖 #26484** | 作者: sgfvamll | 状态: Open  
- **摘要**: 修复自动压缩后 `filterCompacted` 保留 stale token 计数，导致第二次压缩的问题。直接关联 #26230、#20621。  
- [查看详情](https://github.com/anomalyco/opencode/pull/26484)

### 2. fix(nix): remove OPENCODE_CHANNEL=local to restore stable backend
- **🔖 #26476** | 作者: Ibn-Hesham | 状态: Open  
- **摘要**: 移除 Nix 包中的 `OPENCODE_CHANNEL=local` 环境变量，修复 NixOS 上 OpenCode 后端无法稳定工作的问题。  
- [查看详情](https://github.com/anomalyco/opencode/pull/26476)

### 3. feat(app): Mobile Touch Optimization
- **🔖 #18767** | 作者: noahbentusi | 状态: Open  
- **摘要**: 针对移动端和触控设备进行交互优化，同时保留桌面体验。包括更大的点击区域、手势支持等。  
- [查看详情](https://github.com/anomalyco/opencode/pull/18767)

### 4. feat(todo): auto-cleanup stale todos + /clear-tasks and /清除任务 commands
- **🔖 #25856** | 作者: LifetimeVip | 状态: Open  
- **摘要**: 社区讨论催生的新功能——自动清理过期的 TODO 条目，并增加 `/clear-tasks` 和中文 `/清除任务` 命令。  
- [查看详情](https://github.com/anomalyco/opencode/pull/25856)

### 5. chore(i18n): complete Chinese translation for zh.ts files
- **🔖 #25800** | 作者: LifetimeVip | 状态: Open  
- **摘要**: 完成 app、ui、desktop 三个模块的简体中文翻译（新增 30+ 键值），提升中文用户界面友好度。  
- [查看详情](https://github.com/anomalyco/opencode/pull/25800)

### 6. feat(permission): extract inner commands from wrappers for permission matching
- **🔖 #16724** | 作者: Chetic | 状态: Closed  
- **摘要**: 解决 `xargs`、`timeout`、`sudo` 等包装命令内部命令无法被权限系统匹配的问题（对应 #9516）。权限规则现在可以精确匹配到内层命令。  
- [查看详情](https://github.com/anomalyco/opencode/pull/16724)

### 7. fix(opencode): unbounded memory growth during active usage
- **🔖 #16346** | 作者: GooseG17 | 状态: Closed  
- **摘要**: 修复活跃使用中虚拟内存无限增长的内存泄漏问题，涉及 #13230、#11399。  
- [查看详情](https://github.com/anomalyco/opencode/pull/16346)

### 8. feat(tui): group timeline messages by date
- **🔖 #15606** | 作者: alexyaroshuk | 状态: Closed  
- **摘要**: TUI 时间线面板现在按日期分组显示消息（“今天”、“昨天”等），提升历史消息浏览体验。  
- [查看详情](https://github.com/anomalyco/opencode/pull/15606)

### 9. fix: use StringDecoder for stdout/stderr to prevent UTF-8 corruption
- **🔖 #15387** | 作者: mfleming | 状态: Closed  
- **摘要**: 修复 `bash` 工具和 session prompt 中 `stdout`/`stderr` 拼接时可能发生的 UTF-8 字符损坏问题，保证非英文输出完整。  
- [查看详情](https://github.com/anomalyco/opencode/pull/15387)

### 10. feat(tui): expose favorite model cycling with Alt+C/Alt+X keybinds
- **🔖 #16802** | 作者: Oerum | 状态: Closed  
- **摘要**: 在 TUI 中为收藏模型切换添加默认快捷键 `Alt+C`/`Alt+X`，并使其在命令面板中可见，方便快速切模型。  
- [查看详情](https://github.com/anomalyco/opencode/pull/16802)

---

## 功能需求趋势

| 需求方向 | 热度 | 典型 Issue |
|----------|------|------------|
| **Agent 市场与分享** | 🔥🔥🔥 | #7467 Agent Marketplace |
| **权限控制简化** | 🔥🔥🔥 | #8463 YOLO mode, #16724 内部命令匹配 |
| **会话管理增强** | 🔥🔥 | #13877 历史会话浏览, #26327 分页导航, #14292 项目目录存储 |
| **跨平台兼容性** | 🔥🔥 | #26321 macOS PATH, #23864 Windows 路径, #26481 WSL UNC |
| **本地模型支持** | 🔥🔥 | #26063 LM Studio 中断, #26221 kiro 崩溃 |
| **技能系统完善** | 🔥🔥 | #24831 技能命令未完整调用 |
| **Web UI 与网络** | 🔥 | #15273 网络 IP 访问, #16788 禁用 Web UI 标志 |
| **性能稳定性** | 🔥 | #13838 压缩注入, #16346 内存泄漏, #15387 UTF-8 损坏 |

社区对于 **Agent 生态（市场）** 和 **减少权限摩擦** 表现出最强渴望；而 **会话历史浏览体验** 和 **跨平台一致性** 是持续高发的痛点。

---

## 开发者关注点

- **会话历史不可见**：TUI 和 Web UI 均存在仅显示近期会话的硬限制，大量历史记录被“隐藏”，用户急需分页或搜索功能。
- **权限弹窗过多**：特别是自动化脚本用户强烈要求“YOLO 模式”，希望一键跳过所有权限确认。
- **本地模型兼容性差**：LM Studio、vLLM 等本地部署模型存在工具执行中断、连接失败等问题，影响离线使用场景。
- **桌面端环境不完整**：macOS 桌面应用 PATH 缺失导致命令找不到，Windows 路径分隔符问题导致会话丢失，严重影响日常开发。
- **发布与更新争议**：部分用户反馈新版砍掉了右键刷新、会话删除等基础操作，且添加 API 后无法直接修改，引发不满。
- **技能系统不完整**：`/skill` 命令仅复制 prompt，未加载引用文件，削弱了技能系统的实用性。
- **插件自动安装困惑**：有开发者询问为何首次打开时会自动安装 `@opencode-ai/plugin`，需要更清晰的安装流程说明。

---

*数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)，统计时间截至 2026-05-09 UTC。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 | 2026-05-09

## 今日速览

过去 24 小时，pi 社区在没有新版本发布的情况下，集中解决了多个影响终端兼容性的关键 bug：窄终端崩溃、Wezterm 键盘失灵、ANTHROPIC_AUTH_TOKEN 密钥泄露等。同时，多个新功能 PR 被合并，包括任务分发模式、图像粘贴支持、DeepSeek/Kimi 模型修复等，社区活跃度维持高位。

## 社区热点 Issues

1. **#4185 – Zsh/tmux 安装后颜色异常（OPEN）**  
   刚安装 pi 的用户在 tmux 中立即遇到颜色对比度问题，影响整体使用体验。社区评论 8 条，持续关注中。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4185)

2. **#4302 – 窄终端渲染过宽行导致 TUI 崩溃（已修复）**  
   20 列 tmux 窗格中渲染超宽行时直接崩溃。用户 lgrossi 不仅报告还提交了 PR#4301 修复，是今日最热门的 bug 之一。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4302)

3. **#4313 – TUI 消息历史虚拟滚动需求**  
   长会话累积大量消息，全量渲染导致内存占用高、导航困难。用户提出虚拟滚动建议，获得社区共鸣。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4313)

4. **#4290 – 因长度被截断的消息被误判为正常停止（OPEN）**  
   用户等待“思考中”状态消失后才发现消息被截断，容易造成误解。需要区分截断与正常结束的显示。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4290)

5. **#4323 – Wezterm 启用 kitty 键盘协议后 Esc 键失效（OPEN）**  
   Wezterm 用户开启 `enable_kitty_keyboard` 后 pi 内 Esc 直接输出转义字符，严重影响基本操作。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4323)

6. **#4279 – 命令行模式 `-p` 运行后不退出（已修复）**  
   `pi -p "say Hi"` 执行结束后进程挂起，需手动 Ctrl+C。影响脚本化使用。已通过后续 PR 修复。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4279)

7. **#4266 – LM Studio 等本地服务因 `tool_choice` 类型被拒（已修复）**  
   OpenAI 兼容的本地服务器只接受字符串 `tool_choice`，但 pi 传递了对象，导致 400 错误。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4266)

8. **#4287 – 原生 PDF/文件输入支持（重新提起）**  
   三大云提供商均已支持文档输入，但 pi 仍只支持图片。社区第三次提出此需求，呼声很高。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4287)

9. **#4293 – 支持 Copilot 订阅内的内部模型**  
   用户希望 pi 能利用 Copilot CLI 提供的 Opus 4.7 等模型，以获取更大上下文和专用模型。  
   [查看 Issue](https://github.com/badlogic/pi-mono/issues/4293)

10. **#3978 – 技能路径显示错误（已修复）**  
    `~/.agents/skills` 下的技能在 `pi config` 中被错误归类为 `~/.pi/agent/`。已通过 PR#4299 修复。  
    [查看 Issue](https://github.com/badlogic/pi-mono/issues/3978)

## 重要 PR 进展

1. **#4301 – 修复窄终端崩溃**  
   在行宽超限时自动截断而非断言崩溃，并增加了 20 列回归测试。直接解决了 #4302。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4301)

2. **#4327 – 列表项缩进换行**  
   改进了 Markdown 列表在窄终端的渲染，增加了缩进和引用标记支持，大幅提升可读性。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4327)

3. **#4331 – 支持 Cmd+V 图片粘贴**  
   macOS 用户在 terminals（Warp/iTerm2/Kitty）按下 Cmd+V 粘贴图片时，通过检测空 bracketed paste 来触发图片上传。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4331)

4. **#4329 – 新增 `--mode worker-loop` 任务分发模式**  
   通过 Unix socket 订阅消息总线，自动消费 `agent_task_request` 任务，为批量/后台处理提供基础。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4329)

5. **#4339 – 修复 ANTHROPIC_AUTH_TOKEN 密钥泄露**  
   使用非 Anthropic 代理（如小米 MiMo）时，SDK 仍会读取环境变量并发送，导致 401。现已清除请求头中的冲突密钥。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4339)

6. **#4335 – 标准化 Copilot API 基础 URL**  
   从 `proxy.business.githubcopilot.com` 统一到 `api.githubcopilot.com`，确保所有 token 正确路由。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4335)

7. **#4299 – 保留技能来源路径元数据**  
   重构技能发现逻辑，使 `pi config` 能正确显示技能的实际位置（如 `~/.agents/skills`），修复 #3978。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4299)

8. **#4312 – DeepSeek/Kimi 工具 schema 与自动检测**  
   修复工具参数为 `null` 时断言失败，并自动识别 Kimi API，大幅扩展了可用模型范围。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/4312)

9. **#3624 – 增加 Together AI 提供商（进行中）**  
   通过 OpenAI 兼容接口集成 Together AI，自动拉取模型列表并设置默认模型。已获得社区关注。  
   [查看 PR](https://github.com/badlogic/pi-mono/pull/3624)

10. **#3887 – 图像内容输出支持（进行中）**  
    让 agent 能生成并显示图像块，已通过简单扩展在 TUI 中测试成功，是对多模态的重要补充。  
    [查看 PR](https://github.com/badlogic/pi-mono/pull/3887)

## 功能需求趋势

- **模型多元化**：Grok 推理、Together AI、Copilot 内部模型、DeepSeek/Kimi、StepFun 等新提供商或模型的集成持续成为热点。
- **终端兼容性与 UI 精细化**：窄终端渲染、颜色主题、列表缩进、虚拟滚动、快捷键 macOS 本地化、点击交互等细节改进不断涌现。
- **扩展 API 完善**：`addFooterProvider`、`Editor.getCursor()`、转录行点击事件等 hooks 被反复请求，社区希望插件生态更灵活。
- **多模态能力**：图片输入/输出、PDF/文档输入、文件附件等需求被多次重提，表明 agent 迈向更丰富的交互形式。

## 开发者关注点

- **终端兼容性痛点**：Wezterm 键盘、iTerm2 按键、tmux 颜色、移动端触控等平台差异问题频繁出现。
- **工具调用可靠性**：本地 LM Studio、DeepSeek、Kimi 等非标准 API 的 `tool_choice` 格式不兼容导致大量用户受阻。
- **命令行行为一致性**：`pi -p` 不退出、环境变量误泄露等问题影响脚本化与 CI 集成。
- **配置与状态分离**：用户希望将设置文件（settings.json）与运行状态（state.json）分开，以便通过 dotfiles 共享配置。
- **会话管理优化**：同步 I/O、全量渲染、缺少虚拟滚动成为长会话用户的主要抱怨点。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 (2026-05-09)

---

## 1. 今日速览

今日社区活跃度较高：发布了 4 个版本（含 v0.16.10-preview.0 和 v0.15.9），重点修复了 CLI 命令验证和 OpenAI 请求日志记录。Issues 方面，认证与 API 连接问题持续为高频故障点，同时大文件编辑死锁、终端闪屏等体验类 Bug 引起关注。PR 方面，流式 delta 修复、窄终端渲染优化、会话持久化等多项改进正在推进中。

---

## 2. 版本发布

### v0.16.10-preview.0
- 修复：`/model` 命令参数验证（PR #3963）
- 修复：记录实际发送的 OpenAI 请求（PR by @tanzhenxin）
- 发布前序版本 v0.15.9 的 chore 提交

### v0.15.9
- 新增：遥测敏感 span 属性 opt-in（PR #3893）
- 新增：基于每文件的 AI 贡献归属（commit attribution）
- 包含 v0.15.8 的 chore 版本发布

### v0.15.9-nightly.20260509
- 同步 v0.15.9 修复内容，提供 nightly 版本用于早期验证

### v0.15.8-preview.0
- 与 v0.15.9 相同的遥测与贡献归属功能（预发布版）

> 完整变更日志：[v0.15.9...v0.16.10-preview.0](https://github.com/QwenLM/qwen-code/compare/v0.15.9...v0.16.10-preview.0)

---

## 3. 社区热点 Issues

### 3.1 🔴 `OPENCODE_GO_API_KEY` 环境变量不被识别
- **#3877**：用户设置了 `~/.qwen/.env` 文件，但启动时仍强制要求选择认证方式，环境变量未生效。4 条评论，开发者尚未确认。
- 链接：[#3877](https://github.com/QwenLM/qwen-code/issues/3877)

### 3.2 🔴 API 连接成功但请求失败（fetch failed）
- **#3914**：OpenRouter 等第三方 API 连接成功，但后续请求报 `Connection error (cause: fetch failed)`。3 条评论，涉及网络层面问题。
- 链接：[#3914](https://github.com/QwenLM/qwen-code/issues/3914)

### 3.3 🟡 俄语文本乱码（字符编码问题）
- **#3936**：界面中俄语文本显示为乱码，可能与终端编码或渲染组件有关。3 条评论，分类为 UI Bug。
- 链接：[#3936](https://github.com/QwenLM/qwen-code/issues/3936)

### 3.4 🟡 启动时覆盖 `settings.json` 配置文件
- **#3843**：每次启动 Qwen Code，用户的 `settings.json` 被完全覆盖，导致自定义配置丢失。2 条评论，已在 v0.15.9+ 中通过修复部分解决（该 issue 已关闭）。
- 链接：[#3843](https://github.com/QwenLM/qwen-code/issues/3843)

### 3.5 🟡 切换模型导致 API 失败（mid-session）
- **#3304**：在推理/思考模型与普通模型之间切换后，后续 API 调用报错。2 条评论，涉及会话中模型切换的兼容性问题。
- 链接：[#3304](https://github.com/QwenLM/qwen-code/issues/3304)

### 3.6 🟡 SDK 升级后 CLI 进程退出（code 1）
- **#3823**：从 `@qwen-code/sdk` 0.1.5 升级到 0.1.6/0.1.7 后，部分调用场景下 CLI 进程随机退出，无详细错误日志。2 条评论，对 SDK 下游开发者影响较大。
- 链接：[#3823](https://github.com/QwenLM/qwen-code/issues/3823)

### 3.7 🟢 输入编辑功能增强请求
- **#3926**：当前输入框不支持 `Ctrl+Backspace` 删除单词、不支持文本选择和剪切粘贴。2 条评论，社区希望提升 CLI 交互编辑体验（welcome-pr）。
- 链接：[#3926](https://github.com/QwenLM/qwen-code/issues/3926)

### 3.8 🟢 大文件编辑死锁：`edit` 工具要求先“完全读取”但 `read_file` 会截断
- **#3945**：编辑工具要求文件必须先被 `read_file`（不带 offset/limit）完全读取，但 `read_file` 对大文件会自动截断，导致编辑操作永远无法执行。2 条评论，属于工具逻辑缺陷。
- 链接：[#3945](https://github.com/QwenLM/qwen-code/issues/3945)

### 3.9 🟢 agent 只说不做（不执行工具）
- **#1242**：Agent 持续回复计划但实际不调用工具，需要用户反复催促。虽然在 0.4.1 中已报告，仍偶发（最近更新于 2026-05-08，可能未完全修复）。2 条评论。
- 链接：[#1242](https://github.com/QwenLM/qwen-code/issues/1242)

### 3.10 🟢 `plan mode` 下 Ghostty 终端闪屏
- **#3979**：在 plan mode 完成回复后，Ghostty 终端出现持续闪屏。1 条评论，影响 terminal UX，需要终端兼容性修复。
- 链接：[#3979](https://github.com/QwenLM/qwen-code/issues/3979)

---

## 4. 重要 PR 进展

### 4.1 🛠 `fix(core): throttle shell tool live text updates` (#3902)
- **功能**：对 Shell 工具的执行输出文本进行节流，避免高频更新导致性能问题。
- **状态**：Open
- 链接：[#3902](https://github.com/QwenLM/qwen-code/pull/3902)

### 4.2 🛠 `fix(core): normalize cumulative OpenAI stream deltas to suffixes` (#3896)
- **功能**：修复部分 OpenAI 兼容提供商（如阿里云百炼）发送累积全文而非增量内容的问题，避免 Gemini 管道重复拼接。
- **状态**：Open
- 链接：[#3896](https://github.com/QwenLM/qwen-code/pull/3896)

### 4.3 🛠 `fix(core): deduplicate geminiChat recovery continuation text` (#3966)
- **功能**：当 Gemini 模型因 MAX_TOKENS 中断并恢复时，去重续写时重复回显的上下文内容。
- **状态**：Open
- 链接：[#3966](https://github.com/QwenLM/qwen-code/pull/3966)

### 4.4 🛠 `refactor(core): TaskBase envelope + foreground subagent persistence` (#3970)
- **功能**：引入通用的 `TaskBase` 基类，统一多种任务注册逻辑，并为前台子 agent 提供持久化支持。
- **状态**：Open（此 PR 为第一阶段，后续将合并注册表）
- 链接：[#3970](https://github.com/QwenLM/qwen-code/pull/3970)

### 4.5 🛠 `fix(cli): replace clearTerminal with targeted repaint on resize` (#3967)
- **功能**：终端窗口尺寸变化时用定向重绘替代全屏清屏，消除可见的闪烁。
- **状态**：Open
- 链接：[#3967](https://github.com/QwenLM/qwen-code/pull/3967)

### 4.6 🛠 `fix(cli): improve rendering on narrow terminals` (#3968)
- **功能**：窄终端（<60 列）时自动切换为竖直表格布局，避免内容溢出。
- **状态**：Open
- 链接：[#3968](https://github.com/QwenLM/qwen-code/pull/3968)

### 4.7 🛠 `feat(base): persist channel sessions across restarts` (#3865)
- **功能**：修复 channel 会话在进程重启后丢失的问题，通过 `AcpBridge.loadSession()` 实现持久化。
- **状态**：Open
- 链接：[#3865](https://github.com/QwenLM/qwen-code/pull/3865)

### 4.8 🛠 `feat: add codebase indexing and hybrid code search` (#2485)
- **功能**：完整的代码库索引与混合检索（SQLite + 向量 + 图），支持增量检测、`/codebase` 命令和 `@codebase{...}` 引用。
- **状态**：Open（设计阶段，持续更新至 2026-05-09）
- 链接：[#2485](https://github.com/QwenLM/qwen-code/pull/2485)

### 4.9 🛠 `feat(telemetry): inject traceId/spanId into debug log files for OTel correlation` (#3847)
- **功能**：在调试日志中注入 `trace_id` 和 `span_id`，便于与 OpenTelemetry 后端关联。
- **状态**：Open
- 链接：[#3847](https://github.com/QwenLM/qwen-code/pull/3847)

### 4.10 🛠 `chore(deps): upgrade ink 6.2.3 → 7.0.2 + bump Node engine to 22` (#3860)
- **功能**：升级 Ink 渲染库至 7.0.2，要求 Node ≥22 和 React ≥19.2，为后续 UI 改进铺路。
- **状态**：Open（计划合并至 0.16.0）
- 链接：[#3860](https://github.com/QwenLM/qwen-code/pull/3860)

---

## 5. 功能需求趋势

从近期 Issues 和 PR 中可以识别出以下社区驱动的功能方向：

- **配置目录与路径自定义**：多个 issue（#2119、#2953）要求支持环境变量 `QWEN_HOME` 或 `QWEN_RUNTIME_DIR`，分离运行时文件与配置目录，适应容器化/企业部署场景。
- **计划模式（Plan Mode）增强**：#3548 请求可配置 `plansDirectory`，类似 Gemini CLI 的计划目录机制。
- **CLI 交互编辑能力**：#3926 要求支持 `Ctrl+Backspace` 删除单词、文本选择等基础文本编辑功能，提升用户输入体验。
- **Markdown 链接可点击（OSC 8）**：#3954 请求在终端输出中嵌入 OSC 8 超转义，使 URL 保持可点击。
- **代码仓库索引与检索**：PR #2485 是长期开发的功能，社区期待高效代码搜索（语义 + 关键词混合）。
- **MCP 服务器管理**：多 issue 涉及 MCP 状态显示、禁用后刷新、认证流程等。
- **大文件/长上下文支持**：#3945 直接暴露了大文件编辑的死锁问题，社区需要更好的大文件处理支持。
- **Windows 平台稳定性**：多次出现 Windows 特定 flaky 测试（如 #3977），社区对跨平台体验有较高要求。

---

## 6. 开发者关注点

- **认证与 API 连接可靠性**：今日有 3 个 issue 直接涉及环境变量不生效（#3877）、API 认证 Token 过期（#3939、#3940）、fetch 失败（#3914）。开发者最希望解决的是：.env 文件正确被读取、Token 过期提示更明确、第三方 API 稳定性增强。
- **配置文件意外覆盖**：#3843 提醒开发者注意启动时不要擅自清空用户配置。虽已修复，但用户仍担心在其他场景（如 SDK 升级）中重演。
- **模型切换与多模型兼容性**：#3304 属于老 bug 但仍有更新，说明切换模型（尤其是带 reasoning 的模型）后会话状态可能损坏。
- **大文件编辑工具矛盾**：#3945 是一个典型的逻辑死锁，编辑工具依赖前置读取，但读取工具对超大文件有限制。这促使需要重新设计工具前置条件，或提供更灵活的文件块操作。
- **终端兼容性与闪烁**：Ghostty 闪屏（#3979）和 resize 闪烁（#3967）反映了对终端模拟器的适配仍需加强，尤其对非标准终端（如 Ghostty、iTerm2）的支持。
- **SDK 稳定性**：#3823 显示 SDK 升级可能引入随机崩溃，影响了依赖 SDK 构建应用的开发者，需要完善错误传递和降级机制。

---

*本期日报由 AI 自动生成，数据截止 2026-05-09 UTC。*

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*