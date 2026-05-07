# OpenClaw 生态日报 2026-05-07

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-07 09:44 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

好的，这是根据您提供的 OpenClaw GitHub 数据生成的 2026-05-07 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026年5月7日

**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师

---

## 1. 今日速览

今日 OpenClaw 项目极其活跃，Issues 和 PR 处理量均高达 500 条，表明社区参与度和项目维护强度均处于高位。尽管合并/关闭了 151 个 PR，但仍有 349 个待合并，维护压力较大。新发布的 v2026.5.6 版本是一个紧急修复版，回滚了可能导致破坏性变更的 Codex OAuth 路由重写逻辑，体现了团队对稳定性的重视。目前项目健康度总体良好，但需持续关注因频繁迭代引发的回归问题，尤其是在插件兼容性和 WebSocket 稳定性方面。

**活跃度评估:** ⭐⭐⭐⭐⭐ (极高)

## 2. 版本发布

**发布版本:** v2026.5.6

**更新内容:** 
此版本是一个紧急修复版，重点回滚了上一个版本 (v2026.5.5) 中 `doctor --fix` 对 Codex OAuth 路由的自动重写。

**破坏性变更 & 迁移注意事项:**
- **核心变更**: 回滚了 `doctor --fix` 中的一个修复，该修复错误地将 `openai-codex/*` 的 OAuth 路由重写为 `openai/*`。
- **潜在影响**: 如果用户已经在 v2026.5.5 上运行过 `doctor --fix`，可能会导致 GPT-5.5 等 OAuth-only 设置的中断，或错误地将用户迁移到 API-key 路由。
- **行动建议**: 所有已升级到 v2026.5.5 且使用了 `openai-codex` OAuth 配置的用户，应立即考虑升级到 v2026.5.6。如果已出现问题，此版本可恢复正常的 OAuth 路由。

**链接:** [OpenClaw v2026.5.6 Release](https://github.com/openclaw/openclaw/releases/tag/v2026.5.6)

## 3. 项目进展

今日合并/关闭了大量修复和功能类 PR，以下为关键进展：

- **插件 SDK 与兼容性修复:**
    - `PR #78810` feat(realtime-voice): 为语音桥接合约增加了可选的视频帧发送能力，支持插件扩展。
    - `PR #78610` fix(Tavily tool): 将 Tavily 工具凭据解析改为运行时配置，提升了 SecretRef 的可靠性和灵活性。

- **核心性能与工具链优化:**
    - `PR #77187` fix(sessions list): 修复了会话列表缓存问题，显著降低了拥有大量会话时的 CPU 消耗（从 88.9 秒大幅降低）。
    - `PR #78852` perf(agents): 在工具准备阶段复用媒体工具可用性检查，减少了不必要的性能开销。

- **文档与稳定性增强:**
    - `PR #78456` feat(channels): 重构了 `openclaw channels list` 命令，明确区分了聊天频道和模型提供商认证信息。

## 4. 社区热点

以下是今日讨论最热烈、反响最大的议题：

1.  **长期 Feature Request (Issue #75)**: “Linux/Windows Clawdbot Apps” 是社区长期关注的痛点。至今已有 104 条评论和 74 个👍，反映了用户对跨平台桌面客户端（尤其是在非 Apple 生态）的强烈需求。开发团队已标记为 `help wanted`，但进度缓慢。
    - **链接:** [Issue #75](https://github.com/openclaw/openclaw/issues/75)

2.  **微信插件兼容性问题 (** `**Issue #78232**`**,** `**#77837**`**,** `**#78434**` **)**: 围绕 `openclaw-weixin` 插件的兼容性问题是今日最密集的 Bug 集合。多个用户报告在升级到 v2026.5.4 后，插件因 `channelRuntime` API 变更、`fetch` 调用失败等问题无法正常工作。这直接推动了社区对插件 API 稳定性的讨论。
    - **链接:** [Issue #78232](https://github.com/openclaw/openclaw/issues/78232)
    - **链接:** [Issue #77837](https://github.com/openclaw/openclaw/issues/77837)
    - **链接:** [Issue #78434](https://github.com/openclaw/openclaw/issues/78434)

3.  **“safe/unsafe ClawdBot” 概念 (Issue #6731)**: 用户提出借鉴 Rust 的 `unsafe` 概念来重构 ClawdBot，启用“安全模式”以在沙箱中运行。虽然评论数不多，但提案本身具有前瞻性，指向了对 AI Agent 安全性和内存管理的高度关注。
    - **链接:** [Issue #6731](https://github.com/openclaw/openclaw/issues/6731)

4.  **Gateway 连接稳定性 (** `**Issue #78402**` **)**: 用户报告在升级到 2026.5.5 后，Gateway 因事件循环饥饿导致 WebSocket 连接反复断开。该问题被标记为回归，且与“卡住的工具调用”相关，暴露出工具执行机制的脆弱性。
    - **链接:** [Issue #78402](https://github.com/openclaw/openclaw/issues/78402)

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在**回归问题**，表明最近的迭代频繁引入了新的不稳定因素。

**严重等级: 高**
- **Gateway 反复断开连接** (`Issue #78402`): 由于工具调用卡死导致事件循环饥饿，使 WebSocket 连接失败。**严重**，影响所有用户。无直接 fix PR。
    - **链接:** [Issue #78402](https://github.com/openclaw/openclaw/issues/78402)

**严重等级: 中**
- **微信插件大规模不兼容**: 至少三个独立报告 (`#78232`, `#77837`, `#78434`) 指出 `openclaw-weixin` 在 v2026.5.4 上完全失效，原因是内部 API (`channelRuntime`, `fetch`) 变更。**严重**切影响特定用户群（微信插件使用者）。
    - **链接:** [Issue #78232](https://github.com/openclaw/openclaw/issues/78232)

- **Gemini 推理泄露** (`Issue #41494`): Gemini 模型的内部思维链内容仍会泄露到用户体验中，这是一个旧 Bug 的回归。
    - **链接:** [Issue #41494](https://github.com/openclaw/openclaw/issues/41494)

**严重等级: 低**
- **Telegram 话题回复静默失败** (`Issue #77248`): LLM 生成的回复未被发送到 Telegram 话题中。可能导致用户困惑。
    - **链接:** [Issue #77248](https://github.com/openclaw/openclaw/issues/77248)

- **高 CPU 与 RPC 延迟** (`Issue #76562`): 从 v2026.4.24 升级后，部分环境出现控制面 RPC 延迟飙升和 CPU 100% 占用的问题。
    - **链接:** [Issue #76562](https://github.com/openclaw/openclaw/issues/76562)

## 6. 功能请求与路线图信号

今日涌现了多个对未来发展有指导意义的功能请求：

1.  **MCP 工具调用审批** (`Issue #78308`): 提议让 MCP 工具调用共享已有的 `/approve <id>` 审批流水线，实现对敏感操作（如发邮件、写数据）的渠道内授权。这将是提升 Agent 安全性的重要功能。
    - **链接:** [Issue #78308](https://github.com/openclaw/openclaw/issues/78308)

2.  **安全配置文件 v1.1** (`Issue #8719`): 用户提出了一个更全面的、以数据为中心的安全模型蓝图，旨在不牺牲用户体验的前提下防止钱包盗窃、数据库擦除等重大安全风险。如果采纳，将是一次重大的架构性改动。
    - **链接:** [Issue #8719](https://github.com/openclaw/openclaw/issues/8719)

3.  **Sub-agent 完成通知路由** (`Issue #27445`): 提议允许子 Agent 的完成通知以用户消息的形式路由回父会话，而非直接发送到频道。这将为主 Agent 编排复杂多步骤工作流提供支撑。
    - **链接:** [Issue #27445](https://github.com/openclaw/openclaw/issues/27445)

4.  **Session 侧边栏管理** (`Issue #50404`): 用户请求一个功能完整的会话侧边栏，以解决当前 Control UI 无法妥善管理和切换对话历史的问题。此功能直接关系到用户体验，已有关联 PR 被讨论。
    - **链接:** [Issue #50404](https://github.com/openclaw/openclaw/issues/50404)

**路线图信号:** “Permission” (权限控制) 和 “Cross-platform App” (跨平台应用) 是今日呼声最高的两个方向。

## 7. 用户反馈摘要

- **痛点: 版本升级带来的“阵痛”**
    - 多位用户表达了对快速迭代中，插件 API 频繁变更导致兼容性问题（特别是微信插件）的挫败感。
    - 用户 `najef1979-codex` (Issue `#78402`) 描述了升级后 Gateway 完全不可用的糟糕体验。
    - 用户 `mogglemoss` (Issue `#75739`) 详细报告了在迁移到 Codex harness 设置时遇到的复杂路由 Bug，显示了迁移路径的不清晰。

- **诉求: 对底层安全与稳定性的更高要求**
    - 用户 `aaroneden` (Issue `#6615`) 期望更精细的命令执行控制（如特定命令的 denylist）。
    - 用户 `Ar3ss12` (Issue `#8719`) 主动提出了一整套安全模型，表明高级用户对安全风险有深刻认识并希望项目能提供更强大的内置保护。

- **满意点:**
    - 从多个已关闭的 PR 和 Issue 来看，开发团队对 Bug 的响应和修复速度非常快 (如 v2026.5.6 紧急回滚)，社区对此保持积极反馈。

## 8. 待处理积压

以下为长期未解决或近期需重点关注的项目：

1.  **跨平台桌面客户端** (`Issue #75`): 创建于 2026-01-01，已存在 4 个多月，需求强烈但进展不明。这是项目走向更广泛普及的关键障碍。
    - **链接:** [Issue #75](https://github.com/openclaw/openclaw/issues/75)

2.  **通用 Denylist 支持** (`Issue #6615`): 获得 7 个👍，已开启近 3 个月，是社区对安全控制精细化诉求的直接体现。
    - **链接:** [Issue #6615](https://github.com/openclaw/openclaw/issues/6615)

3.  **Codex harness 迁移路径 Bug** (`Issue #75739`): 这是一个涉及 `agentRuntime` 和 `openai-codex` OAuth 路由的复杂 Bug，直接影响用户向新架构迁移。虽然 v2026.5.6 回滚了部分相关修改，但根本问题可能仍未解决。
    - **链接:** [Issue #75739](https://github.com/openclaw/openclaw/issues/75739)

4.  **跟踪 Issue: 运行时解析迁移** (`Issue #77700`): 这是一个内部架构优化的跟踪问题，旨在减少运行时信息的重复发现。其成功与否会直接影响到未来版本的性能表现。维护者 `mcaxtr` 正在跟进。
    - **链接:** [Issue #77700](https://github.com/openclaw/openclaw/issues/77700)

---

## 横向生态对比

好的，作为您的资深技术分析师，我已综合了2026年5月7日各项目的社区动态数据，并为您呈现这份横向对比分析报告。

---

### 个人AI助手开源生态横向对比分析报告 (2026-05-07)

#### 1. 生态全景

当前个人AI助手与自主智能体开源生态呈现出 **“高活跃、快迭代、分化初显”** 的态势。各大项目均处于功能密集开发期，社区贡献热情高涨。一方面，通用型框架（如OpenClaw、PicoClaw）正全力构建复杂的多Agent协作、外部记忆和工具调用体系；另一方面，细分赛道已经出现，如侧重**隐私与轻量化**的Nano系列、专注**企业级部署**的Hermes和**跨平台服务网格**的Moltis。一个核心趋势是，**稳定性与安全性**已成为所有项目需共同面对的挑战，例如长对话记忆丢失、插件API兼容性断裂、WebSocket连接不稳等问题频发，说明行业正从“能用”向“好用、可靠”转变。技术路线上，**MCP（Model Context Protocol）** 正成为连接Agent与外部工具的事实标准，而**跨Agent身份与信任协议**则成为下一阶段的热点探索方向。

#### 2. 各项目活跃度对比

| 项目 | 新Issues (24h) | 新/合并PRs (24h) | 今日Release | 健康度评估 | 社区活跃度 (估算评论/互动) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 / 151 | v2026.5.6 (紧急修复) | 极高，但维护压力大 | 极高 (日均500+条) |
| **PicoClaw** | 22 | 54 / 11 | v0.2.8-nightly | 高，但合并瓶颈明显 | 高 (关键Issue有13条评论) |
| **Hermes Agent** | 50 | 50 / 11 | 无 | 高，Bug修复密集 | 高 (多议题有5-17条评论) |
| **CoPaw (QwenPaw)** | - | 26 / 26 | v1.1.5.post2 | 非常高，迭代高效 | 高 (长时间讨论议题) |
| **NanoBot** | 14 | 43 / 19 | 无 | 良好，社区协作高效 | 中等 |
| **NanoClaw** | - | 25 / 6 | 无 | 良好，新技能贡献活跃 | 中等 (架构讨论成焦点) |
| **Moltis** | 4 | 12 / 12 | 无 | 高，核心架构推进快 | 中等 (RFC与特性讨论) |
| **ZeroClaw** | - | - / ~10 | 无 | 高，功能生态爆发式增长 | 高 (大量新渠道请求) |
| **NullClaw** | 1 | 2 / 1 | 无 | 中等，活跃度下降 | 低 (仅一个热点Issue) |
| **IronClaw** | 34 | 50 / ~15 | 无 | 高，核心重构期 | 高 (架构接口定义讨论) |
| **LobsterAI** | 1 | - / 29 | 无 | 高，Bug修复高效 | 低 (社区讨论较少) |
| **TinyClaw/ZeptoClaw** | 0 | 0 | 无 | 静默 | 无 |

#### 3. OpenClaw 在生态中的定位

OpenClaw 作为生态中的 **核心参照系**，拥有最庞大的社区规模和极高的迭代速度，这使其成为事实上的“大本营”。

- **优势**：社区规模与贡献者数量远超其他项目，Issue和PR处理量是其他项目的数倍至数十倍。这带来了最丰富的功能、最广泛的模型和插件支持。其“Plugin”生态和Agent编排能力是核心壁垒。
- **技术路线差异**：相较于追求极致轻量化的Nano系列，OpenClaw更倾向于做一个“全能型”框架，功能全面但复杂度也随之增加。与PicoClaw相比，OpenClaw的社区驱动特征更明显，有时会因快速迭代导致兼容性回退（如v2026.5.5的事件），而PicoClaw则在技术决策上更显主动。
- **社区规模对比**：从数据上看，OpenClaw的单日Issue/PR处理量（500+）接近所有其他活跃项目（PicoClaw、Hermes、CoPaw等）的总和，充分体现了其绝对领先的社区规模。

#### 4. 共同关注的技术方向

多个项目在同一维度上出现类似的需求或问题，揭示了当前生态的核心技术主线：

- **跨Agent身份与信任协议**：
  - **涉及项目**: ZeroClaw (RFC #5890), Moltis (PR #979), NullClaw (PR #783 - 定时任务的安全报告)。
  - **具体诉求**: 构建可验证、安全的Agent间通信机制，实现多实例互操作与任务编排。

- **MCP集成深化与标准化**：
  - **涉及项目**: OpenClaw (MCP工具调用审批 #78308), PicoClaw (MCP Streamable HTTP #2782), Hermes Agent (MCP客户端重连Bug #19559), ZeroClaw (MCP/插件融合提议 #6489)。
  - **具体诉求**: 不仅是支持MCP，更要求对MCP工具调用进行权限控制、客户端稳定性增强，以及将MCP无缝融入自身API体系。

- **多渠道与跨平台扩展**：
  - **涉及项目**: ZeroClaw (10+新渠道请求), PicoClaw (DingTalk SDK Bug), OpenClaw (微信插件兼容性问题), Hermes Agent (Telegram、WhatsApp Bug)。
  - **具体诉求**: 连接一切通信触点（SMS、聊天、社交），并确保在这些渠道上体验稳定，不被静默丢消息。

- **安全与权限控制**：
  - **涉及项目**: PicoClaw (exec工具路径检查), OpenClaw (MCP审批, 安全配置文件v1.1), Hermes Agent (密钥脱敏), CoPaw (自定义工作区隔离)。
  - **具体诉求**: 从简单的沙箱到细粒度的资源访问控制，再到跨Agent的信任模型，安全治理正从“附加功能”变为“核心架构”。

- **性能与可观测性**：
  - **涉及项目**: OpenClaw (CPU消耗优化), IronClaw (E2E超时修复), CoPaw (日志轮转), PicoClaw (高CPU/RPC延迟)。
  - **具体诉求**: 解决长对话、多工具调用场景下的性能瓶颈，并提供更好的监控、日志和调试工具。

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 通用框架、全能型Agent、生态集成 | AI应用开发者、高级用户 | 插件架构、高度社区驱动、功能全面但复杂度高 |
| **PicoClaw** | 低资源设备、本地优先、边缘计算 | IoT开发者、嵌入式、隐私敏感用户 | 轻量级设计、WASM沙箱、最大化上游社区协同 |
| **Hermes Agent** | 企业级部署、渠道网关、稳定与安全 | 企业IT团队、SRE | 强化的渠道管理、网关模式、重视文档与配置管理 |
| **NanoBot/NanoClaw** | 极致轻量、模块化、快速集成 | 个人开发者、独立研究者 | 代码量极简、技能（Skill）机制、强调“零摩擦”体验 |
| **Moltis** | 去中心化Agent网络、服务网格 | P2P开发者、去中心化应用构建者 | 基于Ed25519的节点身份、TOFU信任模型、Vault加密 |
| **IronClaw** | 大型项目重构、现代化、API规范化 | 核心贡献者、架构师 | 正在经历“Reborn”架构重写，专注内部解耦与契约定义 |
| **CoPaw (QwenPaw)** | 前端体验、用户交互、多模型适配 | 普通个人用户、轻度开发者 | 前端性能优化（虚拟化）、对话管理、国内模型深度集成 |
| **ZeroClaw** | “万物皆插件”、开放式生态、渠道为王 | 社区贡献者、渠道集成商 | 统一插件目录、支持无数通信渠道、桌面端原生应用 |

#### 6. 社区热度与成熟度

- **第一梯队 (快速迭代期)**: **OpenClaw, PicoClaw, CoPaw, ZeroClaw**。这些项目处于功能爆炸式增长的阶段，社区提交和Bug报告都非常活跃。它们不断探索新边界（如OpenClaw的MCP审批、ZeroClaw的“万物皆插件”），但同时也面临因快速变化带来的稳定性挑战和兼容性碎片化问题。

- **第二梯队 (质量巩固期)**: **Hermes Agent, NanoBot, IronClaw, Moltis**。这些项目已越过初期的功能铺开期，转而关注架构稳定性、安全加固和用户体验打磨。它们更多是在修复Bug、优化性能、画好API边界。社区讨论更具深度（如RFC、架构提案）。

- **第三梯队 (早期探索期)**: **NullClaw, LobsterAI, NanoClaw**。这些项目社区规模相对较小，贡献者以核心团队或少量外部贡献者为主。功能积累中，但尚未形成大规模社区效应，关键功能（如NullClaw的低资源搜索）和Bug修复效率相对较低。

- **静默项目**: **TinyClaw, ZeptoClaw**。过去24小时无任何可观测活动，可能存在开发者精力转移或项目停顿的风险。

#### 7. 值得关注的趋势信号

1.  **“代理网络”架构萌芽**: 从ZeroClaw的RFC和Moltis的实践来看，社区已不满足于单个Agent，而是开始探索“可信任的、去中心化的Agent网络”。这是个人助手迈向“数字孪生”和“集体智能”的关键一步。**开发者应关注身份认证（如Ed25519）和服务发现协议的演进。**

2.  **MCP作为“工具箱”标准的基本确立**: MCP已不再是创新概念，而是成为几乎所有主流项目的基础设施。当前的重点已从“是否支持MCP”转向“如何安全、高效、可观测地管理MCP工具”。**对开发者而言，学习MCP协议并关注其安全扩展（如审批流）是必选项。**

3.  **从“对话”到“全能操作”的范式转变**: 大量请求和修复集中在“Agent能帮我发消息、打电话、操作浏览器、分析股票、转录语音”。这表明个人助手的定位正从“聊天机器人”转变为“桌面/移动端的数字操作员”。**这意味着开发重点将从NLP转向API编排、系统集成和沙箱安全。**

4.  **安全性是通往“生产级”的门槛**: 从密钥泄露、工具权限滥用、配置文件篡改到跨Agent信任，安全问题几乎在所有项目中都被反复提及。**企业级和个人敏感场景的落地，首先需要解决的是信任和隔离问题。** 安全配置文件和审批流水线将成为标配。

5.  **桌面端成为新的竞争焦点**: ZeroClaw、Nano系列等都在积极建设macOS/Windows原生客户端。这表明开发者希望超越Web界面，获得更强大的本地硬件控制能力（截图、文件、自动化脚本）。**这意味着项目架构需要考虑从“云端服务”向“本地原生应用+云端大脑”的混合模式演进。**

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据 NanoBot 项目 2026-05-07 的 GitHub 数据生成的每日项目动态日报。

---

## NanoBot 项目日报 | 2026-05-07

### 1. 今日速览

今日项目活跃度极高，社区在Bug修复和功能增强方面均有显著贡献。过去24小时内，虽然未有新版本发布，但处理了14条Issue和43条Pull Request，显示出强大的社区协作能力。多个高价值PR已合并，并针对WebSocket和WeChat通道的稳定性问题提出了修复方案。总体来看，项目正处于快速迭代周期，健康度良好。

### 2. 版本发布

无

### 3. 项目进展

今日有19个Pull Request被合并或关闭，标志着项目在多个方面取得实质性进展：
- **代码质量与CI**：PR #3672 通过启用完整的 Ruff F 规则检查并修复相关错误，提升了代码库的整体质量。PR #3678 则完成了日志规范的收尾工作，确保所有异常块都能保留完整的堆栈跟踪。
- **核心Bug修复**：PR #3657 和 PR #3665 相关的Bug已关闭，分别解决了 “Dream restore” 功能的状态回滚问题和 DeepSeek-v4-flash 在推理模式下的API调用问题。
- **关键功能修复**：PR #3671 和已关闭的 PR #3669 专注于解决运行时上下文提示词（Runtime Context）泄露到持久化聊天历史中的回归问题，这对维护对话的一致性和数据安全性至关重要。
- **通道改进**：WeChat通道的修复PR #3684 正在待合并中，旨在解决因轮询异常和过期上下文令牌导致的静默丢消息问题。Matrix 通道的相似修复也在PR #3664 中。

这些进展表明项目正在积极解决社区反馈的稳定性问题，并持续优化代码基础设施。

### 4. 社区热点

- **Issue #3639: 跨Agent信任的身份与接入协议提案**
  - **链接**: [HKUDS/nanobot Issue #3639](https://github.com/HKUDS/nanobot/issues/3639)
  - **分析**: 此提案讨论了为超轻量级NanoBot Agent建立可验证的身份协议（基于Ed25519），是项目向去中心化Agent生态迈出的重要一步。虽然不是最活跃的讨论，但其提出的Layer 2身份概念极具前瞻性，反映了社区对Agent间安全互信的深度思考。

- **WebSocket 相关问题集中爆发**
  - **Issue #3682** 和 **#3683**: 用户 [NewAlice] 报告了在Linux服务器部署时，Windows和Mac浏览器访问WebSocket服务失败的兼容性问题，这揭示了多平台部署时的潜在挑战。
  - **Issue #3674**: 用户 [ivelin] 报告WebSocket通道静默丢弃入站消息中的媒体附件。该问题由 **PR #3673** 直接跟进修复。
  - **分析**: WebSocket通道成为今日的讨论焦点，跨平台兼容性和媒体数据处理是用户最关心的痛点。

### 5. Bug 与稳定性

- **严重: WebSocket 通道静默丢弃媒体文件** ([#3674](https://github.com/HKUDS/nanobot/issues/3674))
  - 当通过WebSocket发送带有图片/文件的消息时，附件被静默忽略。
  - **状态**: 已有修复PR **#3673** 待合并。

- **严重: WeChat 通道消息丢失** ([#3684](https://github.com/HKUDS/nanobot/pull/3684) - PR)
  - 因轮询异常处理和上下文令牌过期导致消息被静默吞掉。
  - **状态**: 已有修复PR **#3684** 待合并。

- **中等: LLM 调用超时** ([#3681](https://github.com/HKUDS/nanobot/issues/3681))
  - 用户频繁遇到300秒超时错误，可能是网络问题或模型本身响应慢。
  - **状态**: Issue已关闭，但根因可能需要用户排查网络或LLM服务提供商。

- **中等: 100% CPU 泄露 (MCP streamable_http_client)** ([#3638](https://github.com/HKUDS/nanobot/issues/3638))
  - 因取消范围不匹配导致 `AgentLoop.close_mcp()` 无法清理连接，造成CPU空转。
  - **状态**: 已关闭，表明已有修复或解决方案被采纳。

### 6. 功能请求与路线图信号

- **增强Agent自定义能力**:
  - `[enhancement] Configure bot name and icon` ([#3650](https://github.com/HKUDS/nanobot/issues/3650)): 用户希望能在config.json中自定义Bot的名称和图标，替换默认的“nanobot”和猫图标。这表明用户期望在后端进行更多品牌化或个性化配置。
  - `[enhancement] Can Dream be disabled?` ([#3652](https://github.com/HKUDS/nanobot/issues/3652)): 请求为“Dream”功能增加一个启用/禁用开关。这暗示该功能并非所有用户都需要，提供选项可以减少不必要的计算开销。
  - **趋势判断**: 这些请求指向用户对“可配置性”和“模块化”的强烈需求，未来版本可能提供更细粒度的功能开关。

- **Agent身份与信任**:
  - `Identity + Onboarding protocols` ([#3639](https://github.com/HKUDS/nanobot/issues/3639)): 该提案虽已关闭，但它提出的Agent身份层概念，与项目长期路线图（Agent互信）高度相关，值得跟进。

- **市场分析与代码分析扩展**:
  - `Add some enhancement for using bot to analysis stock market` ([#1219](https://github.com/HKUDS/nanobot/pull/1219)): 这个长期打开的PR为NanoBot增加了股票分析、代码性能分析和测试用例生成等新技能。如果被合并，将极大地扩展NanoBot的应用范围。

### 7. 用户反馈摘要

- **对“Dream”功能的争议** ([#3652](https://github.com/HKUDS/nanobot/issues/3652)): 用户 [skyline75489] 明确表示“I want to disable Dream completely.”，表明该特性对某些用户场景（如生产环境）可能是不必要甚至是有干扰的。
- **对WeChat通道的强烈需求与痛点** ([#3684](https://github.com/HKUDS/nanobot/pull/3684)): 贡献者 [chengyongru] 一次性修复了WeChat通道的两个问题。从PR描述来看，用户可能遇到过“消息发送成功但无响应”或“机器人答非所问”的情况，这直接影响了使用体验。
- **对默认行为变更的关注** ([#3670](https://github.com/HKUDS/nanobot/issues/3670), [#3671](https://github.com/HKUDS/nanobot/pull/3671)): 用户 [T3chC0wb0y] 对nightly分支中运行时上下文提示词泄露到聊天历史的问题非常关注。这表明核心用户会仔细审视版本回归问题，并希望保持行为的可预测性。
- **对DeepSeek-v4-flash的支持** ([#3665](https://github.com/HKUDS/nanobot/issues/3665)): 用户在尝试使用最新的DeepSeek模型时遇到兼容性问题，Bug关闭迅速，显示出项目对主流模型支持的高优先级。

### 8. 待处理积压

- **功能增强PR长期未合并**: **PR #1219** (`Add some enhancement for using bot to analysis stock market`) 自2026-02-26创建以来，至今已有两个多月。虽然内容庞大，但涉及的工具扩展（如股票分析）对社区很有吸引力。建议项目维护者评估其成熟度，决定是否合并或提供进一步修改指导。
- **心跳相关的长期PR**: **PR #1939** (`feat: skip heartbeat before llm call`) 旨在节省Token和避免行为限制，但长期处于待合并状态。此功能对API成本敏感的用户至关重要，建议优先评估。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 | 2026-05-07

## 今日速览

过去 24 小时内，Hermes Agent 项目共处理了 50 条 Issue 和 50 条 Pull Request，其中关闭/合并的 Issue 8 条、PR 11 条，显示出较高的社区活跃度与维护响应速度。无新版本发布，但大量关于稳定性、跨平台支持和新功能（如外部内存、原生 Windows 支持）的讨论仍在激烈推进。项目整体状态健康，但部分 P2 级 Bug（如 Telegram 网关、Windows 路径处理）尚未完全解决，需持续关注。

---

## 版本发布

本日报周期内无新版本发布。

---

## 项目进展

本日合并/关闭了 11 条 PR，均为 Bug 修复与稳定性改进：

- **#21093** [已合并] – 修复截断工具调用重试逻辑，避免模型在两次重试后仍失败的问题。
- **#10078** [已合并] – 修复 Discord `/skill` 命令因负载超过 8000 字节导致失效，并增强辅助客户端崩溃恢复。
- **#20993** [已合并] – 强化子代理在工具调用输出截断时的处理，增加 `delegation.max_tokens` 配置文档。
- **#20795** [已关闭] – 修复 WSL2 下 `web_extract` 将公网 URL 误判为私有网络地址的问题。
- **#21028** [已关闭] – 修复 Telegram 网关模式下 `clarify` 工具不可用的回调接线缺失。
- **#21102** [已关闭] – 修复全息记忆中因查询含 FTS5 操作符（如连字符）导致搜索结果被静默返回 0 条的问题。
- **#21011** [已关闭] – 修复企业微信/iLink 发送消息时的限流错误缺少内置重试与退避机制。
- **#19767** [已关闭] – 修复 TUI 模式下调整窗口大小（SIGWINCH）自动生成多条空对话记录的问题。
- **#18485** [已关闭] – 降低 Slack 网关日志噪音。

这些修复覆盖了 **跨平台兼容性、网关稳定性、记忆模块、辅助工具** 等多个组件，项目在持续提升健壮性。

---

## 社区热点

以下 Issue/PR 获得了最高评论热度与关注度，反映了社区的核心诉求：

1. **#6323** [Open, 17 评论, 25 👍] – 提议集成 `mempalace` 外部内存模块，实现持久化、可查询的内存，支持长周期任务与会话延续。这是目前社区呼声最高的功能请求之一。
2. **#2512** [Open, 7 评论, 6 👍] – 请求原生 Windows 支持。大量 Windows 开发者希望直接使用 CMD/PowerShell 而非 WSL，相关讨论已持续一个多月。
3. **#5257** [Open, 5 评论, 8 👍] – 提议泛化 ACP 客户端，使 Hermes 能编排其他 ACP 兼容代理（如 Claude Code、Copilot），扩展多代理协同能力。
4. **#18529** [Open, 4 评论] – 报告会话标题生成器直接读取 `response.choices[0].message.content` 而未使用 `extract_content_or_reasoning()`，导致思考模型在标题中泄露思维链。
5. **#19559** [Open, 4 评论] – 指出 MCP 客户端在启动窗口关闭后不再重试连接 HTTP 服务器，影响需要延迟启动的服务（如 TouchDesigner）。

**分析**：社区需求集中在 **外部记忆持久化、原生 Windows 支持、多代理互操作、工具稳定性** 四个方向，其中记忆与 Windows 支持已分别有初步解决方案（`mempalace` 库、`feature` 标签 PR）等待评估。

---

## Bug 与稳定性

按严重程度排列，标注是否已有修复 PR：

### P1（紧急）
- **#21044** [Open, 有 PR] – 修复代理输出未正确脱敏密钥。PR #21044 已在审查中，强制在输出边界脱敏流式增量、中间注释、存储内容等。

### P2（高）
- **#18529** [Open, 无 PR] – 标题生成器使用思考模型导致思维链泄露。
- **#18870** [Open, 无 PR] – `/fork` 仅复制约 15 条消息而非全部历史。
- **#20143** [Open, 无 PR] – WhatsApp 自聊模式下，用户在群组中发送的消息被静默丢弃。
- **#20927** [Open, 有 PR #21027] – Windows 下 `write_file` 路径处理错误，且会话中断后工具调用失效。
- **#20899** [Open, 无 PR] – Telegram 入站图片对模型可见但未暴露给工具的本地文件句柄。
- **#21058** [Open, 无 PR] – `hermes doctor` 对 Gemini 健康检查因 Bearer-token 认证不兼容导致假阳性。
- **#21026** [Open, 无 PR] – 多平台 WebSocket 共享单一事件循环，导致级联断开。
- **#19195** [Open, 无 PR] – Discord 缓存的 .webp 图片被 Anthropic 拒绝（media_type 不匹配）。
- **#21032** [Open, 有 PR #21028 但已关闭，可能未完全解决] – Telegram 网关下 `clarify` 工具仍报错。
- **#21049** [Open, 无 PR] – 回归问题：v0.12.0 后 Discord 图片附件转发到 Anthropic 均被 400 拒绝。
- **#21050** [Open, 无 PR] – 辅助模型上下文长度追踪仍在压缩/网页提取路径中分散。
- **#21105** [Open, 无 PR] – 重命名的根配置别名未被 CLI/Profile API 识别。
- **#20743** [Open, 有 PR] – 新增 Pocket TTS 供应商（Kyutai Labs）的 PR 仍在开放，但未报告为 Bug。

### P3（中低）
- **#19559** [Open] – MCP 客户端启动后不重连。
- **#20939** [Open] – MemOS 内存提供者在每轮对话中生成新进程，消耗大量 RAM。
- **#21121** [Open] – Dashboard 中 “use as” 复制 base_url 却未复制 api_key，导致 401 错误。
- **#21086** [Open] – Dashboard 看板任务抽屉中事件 JSON 背景高亮使文字不可读。
- **#21038** [Open] – Dashboard Cron 标签页显示空白。
- **#20637** [Open] – `AIAgent` 应接受自定义 platform_hint，第三方 WebUI 无法描述自身。
- **#17962** [Open, 有 PR] – 终端工具未检测反向 shell 两阶段攻击模式。

**总结**：本日 Bug 报告集中于 **网关稳定性**（Telegram、Discord、WhatsApp）、**Windows 兼容性**、**记忆模块**及 **配置/工具错误**。多数 P2 问题尚无对应修复 PR，项目需优先分配资源解决。

---

## 功能请求与路线图信号

以下新功能请求获得了社区显著关注，部分已有对应 PR 或设计文档：

| Issue/PR | 标题 | 类型 | 评论/投票 | 路线图可能性 |
|----------|------|------|-----------|--------------|
| #6323 | `mempalace` 外部内存支持 | Feature | 17 评论, 25 👍 | 高（已有外部仓库，社区呼声极高） |
| #2512 | 原生 Windows 支持 | Feature | 7 评论, 6 👍 | 中（相关修复 PR 正在推进，但完全原生支持需重构 CLI 与工具） |
| #5257 | 泛化 ACP 客户端多代理编排 | Feature | 5 评论, 8 👍 | 高（扩展了 Hermes 在 Agent 生态中的角色） |
| #10771 | 自动内存合并（Auto Dream） | Feature | 3 评论, 1 👍 | 中（与 #6323 互补，可考虑合并实现） |
| #21074 | 原生 Windows Terminal 支持（与 #2512 重复） | Feature（Duplicate） | 3 评论 | 低（已标记为重复） |
| #20743 | 新增 Pocket TTS（Kyutai Labs） | PR | 无评论 | 中（PR 已提交，待审查） |
| #21125 | Borge Agent 下一代代理设计文档 | PR（Docs） | 无评论 | 低（概念性设计，非直接功能） |

**潜在纳入下版本的信号**：
- 多个关于外部内存的请求（#6323、#10771）和修复 PR（#21102）表明记忆模块是近期重点优化方向。
- 泛化 ACP 客户端（#5257）能让 Hermes 成为多代理协调枢纽，与当前 ACP 服务端定位互补。
- 对于 P2 Bug 的修复 PR（如 #21027 Windows 路径、#21044 密钥脱敏、#21036 重启排重）预计将优先合并。

---

## 用户反馈摘要

从 Issues 评论中提炼的真实用户痛点：

- **Telegram 网关体验差**：多个用户反映 `clarify` 工具不可用（#21032, #21028）；Markdown 表格在移动端显示糟糕（#14160）；图片无法被工具访问（#20899），限制了文件编辑场景。
- **Windows 用户被边缘化**：用户 wx528 在 #21074 中详细描述了因缺乏原生 CLI 支持而被迫使用 WSL 的痛点，包括路径转换、信号处理等问题。
- **记忆系统不稳定**：用户 fayenix (#20939) 报告 MemOS 每轮对话生成新进程，导致 RAM 飙升；用户 castaples (#21102) 发现 FTS5 特殊字符导致静默失败，严重削弱了记忆检索的可靠性。
- **配置复制不完整**：用户 mk0116 (#21121) 发现 Dashboard 的 “use as” 功能漏掉 API key，导致自定义端点认证失败，降低了 Dashboard 配置效率。
- **日语/德语用户报告 UI 问题**：Flipsi85 (#21086) 指出 Dashboard 看板中事件背景高亮使文字无法阅读，影响了非英语用户的可用性。
- **标题生成泄露敏感内容**：KSroido (#18529) 指出使用思考模型生成的会话标题包含模型内部推理过程，可能暴露业务逻辑或隐私信息。

**满意点**：用户对社区响应速度表示肯定（多个 Bug 在打开后迅速被标记、有 PR 甚至已合并），例如 #21028 在几小时内被识别并关闭。此外，对 `web_extract` 在 WSL2 上的修复（#20795）获得了感谢。

---

## 待处理积压

以下 Issue/PR 长期未响应或处于停滞状态，需维护者重点关注：

- **#2512**（原生 Windows 支持，2026-03-22 创建，41 天无官方回应） – 尽管有重复 #21074 和新开的 Windows 相关 Bug，但该大 Feature 仍未获得路线图明确回复。
- **#17962**（终端工具反制两阶段攻击 PR，2026-04-30 创建，已开放 7 天） – 安全相关 PR #17962 尚未被 Review，需加速以防潜在安全漏洞。
- **#10771**（自动内存合并 Feature，2026-04-16 创建，21 天无评论） – 社区仅有 3 条评论，但该功能与 #6323 互补，值得标注为 “awaiting triage”。
- **#19195**（Discord PNG-as-.webp 图片错误，2026-05-03 创建，4 天无动态） – 影响所有使用 Anthropic 的 Discord 用户，且与新增的 #21049 回归问题相关，应合并调查。
- **#18870**（`/fork` 只复制 15 条消息，2026-05-02 创建，5 天无讨论） – 功能性 Bug 影响用户迁移会话，优先级应提升。

**建议**：维护者应在本周内对上述积压议题进行标记与初步反馈，尤其优先处理安全 PR #17962 和 Windows 支持的大型 Feature Request。

---

*本日报由 AI 自动生成，数据来源：Hermes Agent GitHub Issues & Pull Requests（过去 24 小时，截至 2026-05-07 UTC）。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已根据PicoClaw项目2026年5月7日的GitHub数据，生成了以下项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-05-07

### 1. 今日速览

本周项目活跃度极高。过去24小时内，社区提交了22条新Issue和54个Pull Request，显示出开发者对项目的高度关注和贡献热情。**Issue与PR的“已关闭/合并”与“待处理”比例严重失衡**（Issues: 7/22关闭，PR: 11/54合并），社区提交的代码修复和功能请求大量积压，项目维护团队的合并效率可能面临瓶颈。此外，一个名为`nightly`的自动构建版本发布，但明确指出可能不稳定。整体来看，项目处于一个“高吞吐、低合并”的活跃发展阶段，社区贡献的热潮与维护团队的响应速度之间存在显著张力。

### 2. 版本发布

- **最新版本**: `v0.2.8-nightly.20260507.788cda5c`
- **下载地址**: [GitHub Releases 页面](https://github.com/sipeed/picoclaw/releases/tag/v0.2.8-nightly.20260507.788cda5c)
- **更新内容**: 这是一个自动化构建的**每日构建版本**，基于`main`分支的最新提交。
- **破坏性变更与迁移注意事项**: 发布说明明确标记为“unstable”，且是自动构建。变更日志指向了自 v0.2.8 以来的所有 `main` 分支改动，范围过大，无法在此判断具体内容。**强烈建议生产环境和稳定用途的用户**不要使用此版本，仅作尝鲜或测试用途。

### 3. 项目进展

今日共有 **54个PR被提出，其中11个被成功合并或关闭**。以下为今日合并的重点PR，标志着项目在关键功能上的推进：

- **跨Agent任务协作 (已完成并合并)**: PR [#2531](https://github.com/sipeed/picoclaw/pull/2531) 实现了`delegate`工具，允许一个Agent将任务委托给另一个特定的命名Agent并等待结果。这标志着**项目路线图中规划的多Agent协作体系（Phase 2）取得了里程碑式的进展**。
- **Web搜索提供者回退优化 (已完成并合并)**: PR [#2629](https://github.com/sipeed/picoclaw/pull/2629) 集中并优化了Web搜索提供者的选择和回退逻辑，现在可以更智能地利用模型的内置搜索能力，提高了搜索功能的稳定性和灵活性。
- **OpenAI兼容性嵌入支持 (已完成并合并)**: PR [#2624](https://github.com/sipeed/picoclaw/pull/2624) 在提供者层增加了对OpenAI兼容嵌入API的支持，这对于使用vLLM等向量化服务端的用户来说意义重大。
- **CI/CD流程优化 (已完成并合并)**: PR [#2610](https://github.com/sipeed/picoclaw/pull/2610) 优化了发布工作流，支持从已存在的Git标签进行发布，释放了CI流程的灵活性。
- **多用户群组聊天属性 (已合并)**: PR [#2715](https://github.com/sipeed/picoclaw/pull/2715) 为历史消息添加了发送者属性，这对于在Discord、Telegram等群组聊天的场景中，让AI更好地理解消息上下文至关重要。

### 4. 社区热点

今日社区讨论聚焦于几个核心痛点：

1.  **LLM调用失败与重试机制 (热度最高)**：[Issue #629](https://github.com/sipeed/picoclaw/issues/629) 作为一个自2月22日被提出的“陈年旧Bug”，今日仍有13条评论。用户`manhnt9`反馈当LLM服务端返回HTTP 500时，PicoClaw会直接挂起而不重试，这是一个严重影响长任务稳定性的问题，社区对此关注度极高。
2.  **exec工具的安全路径检查过于粗暴**：[Issue #1042](https://github.com/sipeed/picoclaw/issues/1042) 获得了2个👍。用户`icyfire`提出的`guardCommand`方法正则过于简单，导致诸如`curl "wttr.in/Beijing"`这类不涉及文件路径的命令被误判为路径穿越而阻止。这反映出安全性与工具易用性之间的平衡问题。
3.  **浏览器自动化路线图**：[Issue #293](https://github.com/sipeed/picoclaw/issues/293) 获得了8个👍，虽然今日无新评论，但其高赞数表明社区对“让AI能像人一样操作浏览器”这一高级功能寄予厚望，这是一个强烈的产品方向信号。

### 5. Bug 与稳定性

今日报告的Bug数量和严重性均较高，部分问题已有修复PR在跟进。

| 严重程度 | 关键问题 | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | **[BUG] DingTalk SDK 导致网关崩溃** | [Issue #2704](https://github.com/sipeed/picoclaw/issues/2704) 报告了`dingtalk-stream-sdk-go`库中的并发竞态问题，会导致Gateway进程panic崩溃。这是一个直接影响生产环境稳定性的严重问题。 | 未修复，待处理 |
| **严重** | **[BUG] 跨提供商认证失败 (401)** | [Issue #2769](https://github.com/sipeed/picoclaw/issues/2769) 报告了用户在多个提供商（Groq, OpenRouter, Nvidia）均遇到`401 Invalid API Key`错误，但密钥本身是有效的。此问题涉及核心的认证模块。 | 未修复，待处理 |
| **中** | **[BUG] DeepSeek v4 思考模型格式错误** | [Issue #2706](https://github.com/sipeed/picoclaw/issues/2706) 报告了PicoClaw不支持和回传`reasoning_content`字段，导致调用DeepSeek新模型时返回400错误。 | 未修复，待处理 |
| **中** | **[BUG] 对话历史记录丢失** | [Issue #2796](https://github.com/sipeed/picoclaw/issues/2796) 和 [Issue #2795](https://github.com/sipeed/picoclaw/issues/2795) 都反馈了一个相同的问题：在查看历史会话时，只能看到最后一条用户消息。该问题影响用户体验和基本的数据可追溯性。 | 未修复，新报告 |
| **低** | **[BUG] README中百度搜索免费额度信息有误** | [Issue #2784](https://github.com/sipeed/picoclaw/issues/2784) 指出README文档中关于百度搜索免费额度信息与百度官方文档不符。 | 未修复，新报告，轻微 |

### 6. 功能请求与路线图信号

今日社区提出的功能请求主要集中在：

- **协议支持**: **MCP Streamable HTTP**: [Issue #2782](https://github.com/sipeed/picoclaw/issues/2782) 请求PicoClaw的MCP客户端支持新一代的“Streamable HTTP”传输协议。鉴于已有PR [#2770](https://github.com/sipeed/picoclaw/pull/2770) 正致力于在WebUI中添加MCP管理界面，并且该项目MCP集成是当前活跃发展的方向，**该功能请求极有可能在下一版本中得到实现**。
- **子Agent角色隔离**: [Issue #2775](https://github.com/sipeed/picoclaw/issues/2775) 提出了一个多Agent架构下的核心问题：被`spawn`出来的子Agent会继承父Agent的`AGENT.md`，导致角色混淆。结合今日合并的`delegate`工具(PR #2531)，**解决子Agent系统提示继承问题是完善多Agent架构体验的关键下一步**。
- **更多提供商支持**: [Issue #2671](https://github.com/sipeed/picoclaw/issues/2671) 请求支持`opencode`模型提供商。这表明社区对PicoClaw适配更多样化模型源的需求非常强烈。

### 7. 用户反馈摘要

从今日的讨论中，可以提炼出以下几个核心的用户声音：

- **“又慢又容易挂”**：这是对长任务执行（Issue #629）和API调用（Issue #2704）稳定性的直接抱怨。用户期望PicoClaw在面对后端错误时能有更健壮的恢复和重试机制。
- **“为什么我上次说了什么，这次看不到了？”**：这是对对话历史记录（Issue #2795, #2796）丢失的典型反馈。这表明会话管理功能是用户体验的基石，其稳定性直接影响了用户对产品的信任度。
- **“我配置了个新模型，但界面上说我没配置”**：这是针对Android App模型配置问题（Issue #2368）的困惑。配置流程的bug或UI未正确刷新，严重阻碍了普通用户的使用。
- **“安全防护太蠢了”**：这是对`exec`工具路径检查（Issue #1042）的反馈。用户希望安全机制能更智能，而不是简单粗暴地阻止合法的命令。

### 8. 待处理积压

以下是一些长期未更新、但重要性高的Issue和PR，值得项目维护者重点关注：

- **[Issue #629] [BUG] Didn't retry if meet LLM call failed**: 严重性高，且自2月份以来已积压3个月，持续有用户关注。
    - 链接: https://github.com/sipeed/picoclaw/issues/629
- **[Issue #293] Feature: Autonomous Browser Operations**: 社区呼声极高（8个👍），是项目提升能力的标志性功能，但进度不明。
    - 链接: https://github.com/sipeed/picoclaw/issues/293
- **[PR #2413] refactor(line): use official LINE Bot SDK v8**: 一个重要的代码重构，用于消除潜在的签名验证等bug，已开放1个月未见更新或合并。
    - 链接: https://github.com/sipeed/picoclaw/pull/2413
- **大量待合并PR**: 当前有**43个PR**处于待合并状态，这对社区贡献者的积极性是一个潜在的打击。建议项目维护团队优先评估并处理一批高质量、低风险的PR，例如修复类（如#2791, #2793）和提升性能的（如#2781），以提振社区士气。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 NanoClaw 项目 GitHub 数据，现为您生成 2026-05-07 的项目动态日报。

---

## NanoClaw 项目动态日报 | 2026-05-07

### 1. 今日速览

今日项目活跃度极高，Pull Request（PR）数量达到 25 条，显示社区贡献热情高涨。核心亮点是多位贡献者聚焦于 **新技能 (Skill) 的快速构建**（如语义记忆、语音转录）以及 **用户体验的打磨**（特别是 Slack 和 iMessage 的安装流程）。值得关注的是，项目存在一个由配置文件引发的“脏工作树”问题（#2312），以及针对 V2 架构不兼容的旧技能废弃提议（#2311），这两个议题对项目健康度和演进方向有直接影响。尽管 PR 众多，但 New Release 数为 0，项目正处于功能快速累积的迭代周期中。

### 2. 版本发布

无新版本发布。

### 3. 项目进展 (合并/关闭的 PR)

今天有 6 个 PR 被合并或关闭，主要集中在 **稳定性修复** 和 **安装流程优化** 上，标志着项目在这两个维度上取得了实质性进展。

-   **[#2302] fix(whatsapp): allow self-chat messages through fromMe filter** (已合并)
    -   **摘要**: 修复了 WhatsApp 频道中，用户无法与自己对话（Self-Chat）的 Bug，原先的过滤逻辑误将用户自己的消息当做 Echo 丢弃。
    -   **状态**: ✅ 已修复，提升了日志/调试体验。
    -   **链接**: [PR #2302](https://github.com/qwibitai/nanoclaw/pull/2302)

-   **[#2308] fix(prompts): tighten approval-card flow + drop ghost tool ref** (已合并)
    -   **摘要**: 修复了审批流程中的 Prompt 问题，包括删除了指向不存在工具的引用，并精简了审批待定状态的反馈文本。这是一个审计 P0 级的修复。
    -   **状态**: ✅ 已修复，提升了 Agent 行为准确性与用户反馈清晰度。
    -   **链接**: [PR #2308](https://github.com/qwibitai/nanoclaw/pull/2308)

-   **[#2309] fix(skills): replace sqlite3 CLI with in-tree better-sqlite3 wrapper** (已合并)
    -   **摘要**: 修复了一个根本原因是 `sqlite3` 命令行工具缺失导致迁移脚本报错的 Bug。通过改用项目内嵌的 `better-sqlite3` 包装器，消除了此系统依赖。
    -   **状态**: ✅ 已修复，直接解决了 Issue #2191 中描述的误导性错误问题，提升了迁移流程的鲁棒性。
    -   **链接**: [PR #2309](https://github.com/qwibitai/nanoclaw/pull/2309)

-   **[#2297] setup: tidy Slack app-creation card** (已合并)
    -   **摘要**: 对 Slack 应用的创建指引卡片进行了界面优化，将链接前置到显眼位置，并优化了 OAuth 权限作用域的显示格式，使其更易于阅读。
    -   **状态**: ✅ 已改进，降低了 Slack 设置的准入门槛。
    -   **链接**: [PR #2297](https://github.com/qwibitai/nanoclaw/pull/2297)

-   **[#2244] feat(channel): Sentry, delivery receipts, celebrate endpoint, outbound media** (已合并)
    -   **摘要**: 为 Telegram 频道增加了 Sentry 错误监控、发送回执、庆祝端点以及出站媒体文件支持。这是一个较大的功能合入，显著增强了 Telegram 通道的可观测性和功能完整性。
    -   **状态**: ✅ 功能已上线。
    -   **链接**: [PR #2244](https://github.com/qwibitai/nanoclaw/pull/2244)

-   **[#2313] setup: add back-to-channels exit at every Teams step gate** (已合并)
    -   **摘要**: 在复杂的 Teams 设置流程的每一个步骤中都增加了“返回频道选择”的选项，用户不必再依赖 `Ctrl+C` 强制退出，极大地改善了设置体验。
    -   **状态**: ✅ 已改进，解决了团队协作工具设置中的用户“被困”痛点。
    -   **链接**: [PR #2313](https://github.com/qwibitai/nanoclaw/pull/2313)

### 4. 社区热点

今日最受关注的议题集中在 **新功能的提出** 与 **Architectural 兼容性问题** 的讨论上。

-   **新功能火花：语义记忆与语音转录**
    -   **热点链接**: [PR #2318](https://github.com/qwibitai/nanoclaw/pull/2318) (feat(skills): add /add-mnemon skill)
    -   **热点链接**: [PR #2317](https://github.com/qwibitai/nanoclaw/pull/2317) (feat(skills): add /add-voice-transcription-free-whisper skill)
    -   **分析**: PR #2318 提出的 `/add-mnemon` 技能，为 Agent 添加了持久化的语义记忆功能，使其能跨重启和上下文压缩调用知识图谱，这直接响应了 Agent 记忆持久化的核心需求。PR #2317 则增加了本地免费的语音转录能力，支持 GPU 和纯 CPU 方案，扩大了 NanoClaw 在多样化硬件上的可用场景。这两个 PR 热度高，表明社区对 **增强 Agent 的“大脑”（记忆）和“感官”（语音）** 有强烈渴望。

-   **架构风暴：`/claw` 技能的存废与 V2 兼容性**
    -   **热点链接**: [Issue #2311](https://github.com/qwibitai/nanoclaw/issues/2311) (Deprecate `/claw` skill)
    -   **分析**: 这是今日最尖锐的讨论。作者 @JayFarei 直接指出旧技能 `/claw` 在底层设计（DB、传输层、容器模型、密钥管理）上与 V2 架构完全不兼容，并建议废弃。这个议题不仅仅是提 Bug，更是对项目 **技术债务清理和架构演进路线** 的强信号。如果采纳，将是项目一个重大的方向性决策。

-   **用户体验陷阱：CLAUDE.md 导致“脏工作树”**
    -   **热点链接**: [Issue #2312](https://github.com/qwibitai/nanoclaw/issues/2312) (groups/global/CLAUDE.md is unconditionally deleted)
    -   **分析**: 该 Issue 报告了一个严重 UX 问题：一个提交到仓库的文件每次启动都被强制删除，导致任何拉取代码并重启的用户都会看到“脏工作树”。这虽然不直接致命，但会 **严重干扰开发者的 Git 工作流**，并可能隐藏其他潜在问题。评论数 1，表明这是明确的、值得优先处理的 Bug。

### 5. Bug 与稳定性

今日报告的 Bug 数量不多，但质量较高，涉及架构和启动稳定性。

-   **严重: Issue #2312 `groups/global/CLAUDE.md` 导致启动后工作树被污染**
    -   **状态**: OPEN，暂无关联 Fix PR
    -   **影响**: 所有从仓库拉取代码并重启服务的开发者。虽然是“非功能性”Bug，但会造成持续的工作烦恼和潜在风险。
    -   **链接**: [Issue #2312](https://github.com/qwibitai/nanoclaw/issues/2312)

-   **严重: Issue #2311 `/claw` 技能与 V2 架构不兼容**
    -   **状态**: OPEN，建议废弃
    -   **影响**: 使用 `/claw` 技能的旧版用户或工作流。
    -   **链接**: [Issue #2311](https://github.com/qwibitai/nanoclaw/issues/2311)

-   **中危: PR #2291 修复容器内 TLS 信任问题** (OPEN)
    -   **摘要**: 修复了通过 OneCLI 网关的路由可能导致容器内 HTTPS 证书验证失败的问题。
    -   **状态**: 已有修复 PR #[2291](https://github.com/qwibitai/nanoclaw/pull/2291) 待合并。
    -   **链接**: [PR #2291](https://github.com/qwibitai/nanoclaw/pull/2291)

-   **低危: PR #2310 Chat-SDK Bridge 在处理非标准消息 Block 时失败** (OPEN)
    -   **摘要**: 当消息包含无效的 Block 时，Bridge 会失败，新增的修复将其回退到纯文本格式。
    -   **状态**: 已有修复 PR #[2310](https://github.com/qwibitai/nanoclaw/pull/2310) 待合并。
    -   **链接**: [PR #2310](https://github.com/qwibitai/nanoclaw/pull/2310)

### 6. 功能请求与路线图信号

今日社区贡献的新技能（Skill）功能可以视为“用代码投票”的功能请求，对未来版本有很强指导意义。

-   **Agent 持久化记忆**: **PR #2318** (`/add-mnemon`) 极大概率被纳入下一版本，它解决了 Agent 长期运行的基石问题。
-   **本地免费语音转录**: **PR #2317** (`/add-voice-transcription`) 体现了社区对“隐私优先”、“零成本”多媒体处理的需求，被接受的可能性很高。
-   **GitHub 无端口轮询模式**: **PR #2301** 提出的 Mode B 是对无法开放端口的用户（如 NAT/防火墙环境下的 Operator）的福音，是提升产品覆盖面的关键功能。
-   **Agent 工具调用可视化**: **PR #2211** (feat: add tool-visibility skill) 是一个创新功能，让用户能实时看到 Agent 在调用哪些工具，对理解 Agent 行为和调试非常有帮助，虽然有 PR 但待合并时间较长，值得关注。
-   **YouTube 下载支持**: **PR #2306** (feat(yt-dlp-mcp)) 通过 MCP 集成了强大的 yt-dlp，为 Agent 增加了媒体获取能力。

### 7. 用户反馈摘要

从今日的 Issues 和 PR 评论中，可以提炼出以下用户声音：

-   **痛点 - “智性”负担**: 用户在 Issue #2315 和 #2316 的 PR 中反映了设置向导存在“学术/技术黑话”过多的问题（如“E.164”），以及设置流程中存在“死胡同”（如选“其他”后无法返回）。这表明 **项目在降低新手使用门槛方面仍有提升空间**。
-   **痛点 - 无声的失败**: Issue #2312 描述的问题（`CLAUDE.md` 被删除）虽然不导致服务 crash，但会给所有开发者带来持续的困扰和“我的代码是脏的？”的困惑感。这是一个典型的 **“无声的可用性问题”**。
-   **需求 - 对 Agent 能力的抽象**: 从 `mnemon` 和 `voice-transcription` 等技能的快速涌现来看，用户不仅满足于 Agent 能聊天，更希望 Agent 能 **“记住”** 和 **“听见”**。这表明社区正推动 Agent 向更复杂的、类人的通用助手演进。

### 8. 待处理积压

-   **PR #2187** (fix(platform-id): don't namespace CLI bare platform ids): 一个从 5月2日 起待处理的简单修复，用于解决 CLI 通道的平台 ID 命名问题。此 PR 获得“-follows-guidelines”标签，说明是一个高质量的小修复，合并优先级不应太低。
    -   **链接**: [PR #2187](https://github.com/qwibitai/nanoclaw/pull/2187)

-   **PR #2211** (feat: add tool-visibility skill for live tool-call previews): 这是一个非常吸引眼球的功能：实时工具调用预览。从 5月3日 起待合并至今，已有较长时间。如果项目方认可该方向的价值，建议尽快 review 以决定是否合并，避免社区贡献者流失。
    -   **链接**: [PR #2211](https://github.com/qwibitai/nanoclaw/pull/2211)

-   **PR #2291** (fix(container): trust OneCLI gateway CA inside agent container): 这是对 Agent 容器网络稳定性的一个关键修复，已待处理两天，与核心功能“OneCLI”的可靠性直接相关。
    -   **链接**: [PR #2291](https://github.com/qwibitai/nanoclaw/pull/2291)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报 | 2026-05-07

---

## 1. 今日速览

- 项目过去24小时活跃度中等：1条新Issue、2条PR更新，其中1个PR已合并关闭，1个PR仍待处理。
- 核心bug #871 引发社区关注，讨论聚焦于低资源设备上web_search功能的可用性，评论数达7条，是目前最主要的技术争议点。
- 长期未合入的cron子代理功能PR #783 仍停留在“Open”状态，已持续一个月未获合并，项目进度存在一定积压风险。
- 整体来看，项目在稳定性修复（PR #790合并）和功能扩展（cron功能）方面均有推进，但社区对资源受限场景的体验改善呼声较高。

---

## 2. 版本发布

无（过去24小时无新版本发布）。

---

## 3. 项目进展

### ✅ 已合并/关闭的重要PR

- **#790 [已关闭] fix(providers): Responses API tool schema and null error handling**  
  作者：fakhriaunur  
  链接：https://github.com/nullclaw/nullclaw/pull/790  
  **说明**：修复了OpenAI兼容提供商在Responses API模式下的两个关键bug：一是工具schema格式错误（使用了不兼容Chat Completions格式的嵌套结构），二是对null值的错误处理。该修复确保了`api_mode=responses`路径的正常运行，减少了因格式错误导致的API调用失败。  
  **意义**：解决了与OpenAI最新API兼容性的技术障碍，属于基础设施稳定性的重要补丁。

### 🔄 待合并的PR

- **#783 [开启] feat(cron): cron subagent, run history, JSON output, security hardening**  
  作者：yanggf8  
  链接：https://github.com/nullclaw/nullclaw/pull/783  
  **状态**：已开启30天，尚未合入主线。  
  **内容**：包括DB持久化的cron调度器、支持cron子代理、任务运行历史记录、JSON CLI输出以及安全强化（如权限控制、操作告警）。若合并，将大幅增强NullClaw在自动化运维场景下的能力。

---

## 4. 社区热点

**Issue #871**：`[bug] Critical: web_search is impractical on low-resource devices without direct DuckDuckGo support`  
作者：uMendex | 评论数：7  
链接：https://github.com/nullclaw/nullclaw/issues/871

**分析**：该Issue是目前讨论最热烈的单一话题。作者指出**web_search**功能在弱/廉价设备上无法实际使用，因为当前仅支持Brave Search API（需外部API key）和可能涉及其他复杂配置。用户普遍希望NullClaw能内置对DuckDuckGo等零配置搜索接口的直接支持，以降低在受限设备上的使用门槛。评论区中多名用户表达了类似需求，并讨论了可能的替代方案（如使用免费公共API或轻量级搜索引擎）。这表明**低资源设备用户体验**是当前社区的核心关切之一。

---

## 5. Bug 与稳定性

| 严重程度 | Bug 简述 | Issue/PR 链接 | 是否有修复PR |
|----------|----------|---------------|--------------|
| **Critical** | `web_search`在低资源设备上不可用，缺乏免配置的搜索引擎支持（如DuckDuckGo） | [#871](https://github.com/nullclaw/nullclaw/issues/871) | 无 |
| **Medium** | OpenAI Responses API工具schema格式错误与null handling问题（已修复） | [#790](https://github.com/nullclaw/nullclaw/pull/790) | ✅ 已合并 |

**说明**：#871描述的虽然是一个功能缺陷（非崩溃），但因其直接影响最小化设备上的核心搜索能力，被作者标注为Critical。目前尚无对应的修复PR提交，维护团队需尽快评估并规划解决方案（例如集成SimpleDuckDuckGo或允许配置多个搜索引擎）。

---

## 6. 功能请求与路线图信号

### 明确的新功能需求

- **Cron子代理与自动化调度**：PR #783 实现了完整的cron调度系统，包括任务历史记录、JSON输出和安全增强。该功能已开发完毕并经过讨论，一旦合入将被列入下一版本的核心能力。
- **轻量级搜索引擎硬编码支持**：从Issue #871的评论中，用户强烈建议在核心代码中直接集成DuckDuckGo或其他无需API key的搜索引擎，作为`web_search`的默认fallback。该需求可能影响下一版本的配置架构。

### 路线图信号

- 上述两项需求分别代表了**自动化运维**与**低门槛部署**两个方向，维护者若希望提升项目在IoT/边缘设备及家庭助手场景的竞争力，应优先将PR #783合并，并对#871提出正式改进计划。

---

## 7. 用户反馈摘要

从Issue #871的评论中可提取以下真实用户痛点：

- **痛点**：用户uMendex提到“Brave Search API密钥需要额外注册，且不适合低功耗设备”；另一用户补充“在树莓派Zero上运行时，每次搜索都要加载外置API，延迟高且易失败”。
- **使用场景**：家庭自动化助手、学生实验用的廉价平板、离线调试环境。用户希望NullClaw能“开机即用”地执行简单网页搜索，而不依赖外部服务。
- **满意点**：评论区用户对NullClaw的整体思路表示认可，认为它适配弱设备的方向正确；但**web_search当前实现与该定位相悖**，是主要不满来源。
- **建议**：有用户提出“可参考Copilot的Bing搜索集成方式，但更轻量”，或“默认内置DuckDuckGo Lite”（免费且无接口限制）。

---

## 8. 待处理积压

**PR #783**（feat(cron)）：  
- 状态：Open（自2026-04-07起已30天）  
- 未合并原因：可能涉及DB schema变更、设计评审或与其他模块的兼容性测试。  
- 风险：长期悬置会导致分支与主线产生冲突，增加合并难度。建议维护者在本周内抽出时间复审，或标记为“pending review”明确等待项。

**Issue #871**：  
- 虽然提交时间仅4月25日，但已获得7条评论且无任何维护者回应标记（如`triage`、`needs-discussion`）。建议维护者主动打标，给出初步处理方向（例如“计划在v0.9.2中集成DuckDuckGo”），避免社区挫败感。

---

**总结**：项目在API兼容性修复上取得进展，但低资源设备体验与长期功能PR的合并效率是当前健康的隐患。社区对“零配置搜索”的呼声强烈，值得优先回应。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 IronClaw (github.com/nearai/ironclaw) 数据源生成的 2026-05-07 项目动态日报。

---

# IronClaw 项目动态日报 — 2026-05-07

## 1. 今日速览

项目目前正处于核心服务（`TurnCoordinator`, `SessionThreadService`）的“Reborn”架构重构关键期，吞吐量极高。过去24小时内，Issues（34条）和PRs（50条）更新量均处于活跃状态。**Reborn** 相关契约定义与迁移工作是绝对主线，大量“定义API边界”的Issue被关闭，标志着团队已从设计阶段快速切入具体实现。同时，社区反馈的P1级Bug（Telegram/Gmail集成问题）也已上报，稳定性工作开始跟进。**项目健康度：高活跃度，风险可控。**

## 2. 版本发布

无

## 3. 项目进展

今日项目在 **Reborn架构落地**和 **工程基建优化** 方面取得显著进展。

- **核心契约落定与实现**：多份关键的Reborn服务契约被合并，标志着从“设计”到“代码”的实质性迁移。
  - **会话与线程契约**：PR #3315 (closed) 合并了`ironclaw_threads` crate，定义了规范化的线程/对话数据模型和`SessionThreadService`接口。
  - **对话绑定服务**：PR #3314 (open) 虽然尚开放，但已合并了`ConversationBindingService`和`SessionThreadService`的契约与内存实现。
  - **事件投影服务**：PR #3212 (closed) 合并了`ironclaw_event_projections` crate，实现了基于可持久化事件日志的事件投影机制，为UI和外部推送提供了稳定数据源。

- **工程体验与稳定性优化**：
  - **E2E测试门禁**：PR #3251 (closed) 合并了专门的Reborn E2E测试门禁，允许对架构变更进行独立验证，降低合并风险。
  - **CI自动化增强**：PR #3318 (closed) 合并了“夜间失败归因”脚本，能在夜间测试失败时自动@相关合并人，极大提高了问题定位效率。
  - **夜间E2E超时修复**：PR #3329 (closed) 将E2E超时阈值从30分钟提升至90分钟，直接修复了因超时而导致的夜间测试失败问题（见 #3323）。

- **长期功能维护**：社区贡献的**WeChat支持**PR #1666 仍在更新，持续追踪集成进展。

## 4. 社区热点

今日讨论热度集中于 **Reborn架构的细节接口定义**，表明核心贡献者正在集体攻克复杂的设计问题。

- **[#3198] Define TurnCoordinator public API shape** (已关闭)：该Issue评论数高达5条，被团队视为 **#3013** 和 **#3195** 的关键前置依赖。其关闭标志着“Turn Coordinator”（负责线程/会话准入与执行的核心仲裁者）的公共API形状最终确定，是架构设计的一个里程碑。
- **[#3093] Add EventProjectionService** (已关闭)：4条评论，涉及E2E测试、持久化存储等多项依赖，其完成标志着事件驱动架构在Reborn中的关键组件已就绪。

**分析**：社区的活跃讨论集中在如何优雅地定义新老系统（Reborn vs. 现有系统）的边界，以及如何通过纯粹的接口定义来降低未来集成的风险和复杂度。

## 5. Bug 与稳定性

今日上报了多个影响用户体验的Bug，主要集中在**Telegram通道**和**核心配置**上。

| 严重程度 | Issue ID | 摘要 | 状态 | 对应修复PR |
| :--- | :--- | :--- | :--- | :--- |
| **Critical** | #3323 | 夜间E2E测试因超时被取消 (v2-engine) | 已修复 (Closed) | #3329 (已合并) |
| **P1** | #3320 | Telegram 中 Gmail 认证失败后，对话卡死无法继续 | 待处理 | 无 |
| **P1** | #3319 | Gmail 认证在 Telegram 中报 400 错误 | 待处理 | 无 |
| **P1** | #3317 | Telegram 设置无法与本地 IronClaw 配合工作 | 待处理 | 无 |
| **Critical** | #3229 | LLM提供商配置因启动时的fallback逻辑被错误持久化，导致配置永久失效 | 待处理，争议中 | 无 |
| Medium | #3132 | 任务创建因 `cooldown_secs` 字段类型问题失败 | 已关闭 | #3206 (待合并) |

**稳定性快照**：
- **成功修复**：`Gemini SSE thought_signature` 错误 (#3214) 的修复 PR #3215 仍在等待合并。
- **待修复**：Telegram 通道的一连串问题 (#3317, #3319, #3320) 与 LLM 配置的严重 Bug (#3229) 是当前最大的稳定性隐患。

## 6. 功能请求与路线图信号

今日新功能请求信号明确，主要围绕 **用户体验** 和 **平台实用性**。

- **LLM 推理过程可视化**：Issue #3327 请求端到端地呈现LLM的“思考”过程（`reasoning_content`, `thought_signature`）。对应修复 PR #3326 已经提交，该功能很可能在 #3326 被合并后随下一版本发布，是提升高级用户调试体验的关键功能。
- **多Slack工作区支持**：Issue #3334 提出了一个清晰的企业级需求：一个 IronClaw 实例服务于多个 Slack 工作区。该功能已有前期基础（PR #3253），且提交者 `PierreLeGuen` 是该功能的核心贡献者，极可能在后续版本（如 v0.28）中被实现。此功能对“通道中继（channel-relay）”服务的架构演进有直接推动作用。
- **UI附件支持**：PR #3331 提供了非图片附件（如文件、PDF）的支持，后端逻辑已就绪，此PR将完成全流程体验。

## 7. 用户反馈摘要

从Issues评论中提炼的用户声音，反映了使用中的实际痛点：

- **集成稳定性是第一诉求**：Telegram用户报告了严重的体验断层问题。认证失败后“画地为牢”（#3320），导致整个对话不可用，严重影响了Telegram作为渠道的核心使用场景。
- **配置盲目修改令人困扰**：用户 `thomasmaerz` 报告了一个系统级Bug (#3229)：项目启动时，LLM提供商的`fallback`配置会错误地覆盖用户已有的精确配置并持久化。这种行为对有特定模型偏好和要求的企业用户是“灾难性的”，因为他们无法通过重启来恢复配置。
- **对“黑箱”推理的好奇与需求**：Issue #3327 显示，有用户希望看到模型“推理”的中间输出，这表明用户已不满足于最终答案，追求更深层次的模型理解与调试能力。

## 8. 待处理积压

以下是一些长期未解决或等待核心团队确认的重要Issue/PR，需维护者关注：

- **WeChat渠道集成**：PR #1666 开放已超过40天，虽然社区在持续贡献，但仍处于开放状态。核心团队应考虑是否投入资源加速合并或给出明确的下步计划，以避免社区贡献者的热情受挫。
- **Script HTTP Egress 安全加固**：Issue #3138 提议将脚本的HTTP出口统一通过共享运行时代理，并关注网络隔离问题（Docker中已实现），目前已关闭。但问题本身对安全架构具有重要意义，建议团队在版本迭代中持续关注并给出最终实施计划。
- **多工作区支持设计讨论**：Issue #3334 虽然新开，但其描述中涉及对“通道中继”服务的重大更改。核心团队应尽早介入讨论，确保其设计与现有的“Reborn”架构保持一致，避免后续出现大规模重构。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

## LobsterAI 项目动态日报 — 2026-05-07

---

### 1. 今日速览

今日项目整体保持高活跃度，过去24小时内共处理了29个合并/关闭的PR，同时新开11个待合并PR，社区提交活跃。唯一的新Issue聚焦于会员登录失败，尚未有对应PR修复。功能侧持续推动多模型适配（DeepSeek V4、ChatGPT OAuth、小米mimo、百度千帆）以及协作（cowork）和Agent独立工作目录等新特性。项目健康度良好，但会员登录故障的优先级需关注。

---

### 2. 版本发布

无新版本发布。

---

### 3. 项目进展

今日合并/关闭的PR共29条，主要集中在以下方向：

- **稳定性修复**：修复了cowork模块中Markdown表格持久化截断问题（PR #1900）、Windows下删除skill目录时的EPERM错误（PR #1891）、Qwen 3.6 Plus回答后触发Gateway重启（PR #1870）、IM消息在任务记录中顺序错乱（PR #1871）等。
- **多模型适配**：修复DeepSeek V4默认开启思考时的reasoning_content参数问题（PR #1819）、自定义模型供应商使用DeepSeek V4（PR #1847）、新增ChatGPT OAuth登录支持（PR #1830）、支持小米mimo和百度千帆的Coding Plan（PR #1862、#1859）。
- **Gateway/OpenClaw优化**：修复Gateway因套餐模型列表更新强制重启（PR #1872）、修复ChatGPT OAuth导致`/models`命令结果不全（PR #1886）、为Qwen Vision添加OpenClaw运行时回退（PR #1889）。
- **Agent体验优化**：优化Agent相关文案和体验（PR #1852）、改进cowork引导文本区域高度（PR #1873）。

这些修复和功能推进了LobsterAI在模型兼容性、协作稳定性以及跨平台部署层面的成熟度，共涉及renderer、main、openclaw、skills、cowork等多个核心区域。

---

### 4. 社区热点

今日唯一的新Issue **#1903** _(会员登录频繁失败)_ 成为社区焦点。该问题由用户 `zhahongan-ctrl` 报告，指出使用网易付费模型时因登录失败无法正常使用，并附有截图。虽然目前评论数和点赞数均为0，但该问题直接关系到付费用户的核心体验，预计会引发后续讨论。

相关链接：[Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903)

此外，PR **#1904**（每个Agent支持独立工作目录）为开放状态且涉及多个模块，可能承载了用户对多Agent隔离性的进一步需求。

---

### 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|----------|----------|------|------|
| **高** | [Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903) | 会员登录频繁失败，无法使用网易付费模型 | 新开，无对应PR |
| 中 | [PR #1900](https://github.com/netease-youdao/LobsterAI/pull/1900) | 修复cowork中Markdown表格持久化截断（已在同日合并） | 已修复 ✔️ |
| 中 | [PR #1891](https://github.com/netease-youdao/LobsterAI/pull/1891) | 修复Windows下删除skill目录时的EPERM错误 | 已合并 ✔️ |
| 中 | [PR #1870](https://github.com/netease-youdao/LobsterAI/pull/1870) | 修复Qwen 3.6 Plus回答后触发Gateway重启 | 已合并 ✔️ |
| 低 | [PR #1871](https://github.com/netease-youdao/LobsterAI/pull/1871) | IM消息在任务记录中顺序错乱 | 已合并 ✔️ |

目前尚未有PR直接关联到会员登录失败问题，需要维护者优先排查登录流程中的鉴权或网络代理环节。

---

### 6. 功能请求与路线图信号

- **独立Agent工作目录**：PR #1904 _(OPEN, 标签: feature, 涉及多个area)_ 提出为每个Agent分配独立的工作目录，这符合多用户/多场景隔离的进阶需求，有可能被纳入下一个小版本。
- **ChatGPT OAuth登录**：PR #1830 已在今日合并，已正式支持ChatGPT的OAuth认证方式，拓展了第三方模型接入能力。
- **小米mimo & 百度千帆 Coding Plan**：PR #1862、#1859 均已合并，表明项目正加速集成国产模型及更多平台的代码规划功能。
- **会员登录改进**：Issue #1903 虽为Bug报告，但用户明确要求“改进会员登录方式”，这本质是一个功能优化需求，开发者可评估是否纳入立即修复或产线调整。

---

### 7. 用户反馈摘要

基于今日唯一的新Issue #1903，用户反馈的核心痛点：

> **“会员登录不进去，无法使用网易付费的模型”**  
> 用户提供了详细的错误截图（显示登录界面），并明确表达“需要改进会员登录方式”。这表明当前登录流程可能存在与网易账号体系的兼容性问题（如OAuth token刷新、代理配置、或服务端校验），且直接影响了付费用户的使用意愿。

其余PR中暂无新增的用户评论，但从PR的高合并率（29/40）看，社区对维护者的响应速度总体满意。

---

### 8. 待处理积压

- **[OPEN] PR #1904** — “每个Agent支持独立的工作目录” (创建于2026-05-07，评论量为 undefined，推测为0)。该PR横跨6个area，审核工作量较大，建议维护者尽快分配reviewer以避免功能长期悬置。
- **[OPEN] Issue #1903** — 会员登录失败，无任何回复。建议在24小时内给出初步响应（如确认问题、请求更多日志信息或提供临时规避方案），避免用户流失。

链接：[PR #1904](https://github.com/netease-youdao/LobsterAI/pull/1904) | [Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903)

---

*报告生成时间：2026-05-07 UTC*  
*数据来源：LobsterAI GitHub Issues & Pull Requests*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是为您生成的 Moltis 项目动态日报。

---

# Moltis 项目动态日报 — 2026-05-07

## 今日速览

今日项目活跃度极高，社区与核心开发团队均表现出强劲的交付能力。过去24小时内合并/关闭了12个PR和4个Issue，远超新开数量，显示了高效的维护节奏。关键进展包括：核心贡献者 `penso` 提交了基于 Ed25519 的节点身份认证（TOFU）和电话通话支持（Twilio）两个重量级特性PR；同时修复了多个影响Docker部署和DeepSeek集成的关键Bug。**总体来看，Moltis 在核心架构（身份、沙箱、安全）与扩展性（电话、远程沙箱）方面迈出了坚实步伐，项目健康状况良好。**

## 版本发布

今日无新版本发布。

## 项目进展

过去24小时合并/关闭的12个PR推进了多个重要功能与修复，显示了项目向更安全、更稳定、更易部署的方向演进。

- **核心架构与安全性**：
    - **[PENDING]** PR [#979](https://github.com/moltis-org/moltis/pull/979) 提出用**Ed25519挑战-响应机制**取代基于令牌的节点认证，遵循 SSH 的信任首次使用（TOFU）模型。这为未来多代理间安全通信奠定了坚实基础。
    - PR [#974](https://github.com/moltis-org/moltis/pull/974) 实现了**Vault的自动解封功能**，支持从环境变量或文件读取密钥，提升了服务在重启场景下的自动化运维能力。
    - PR [#970](https://github.com/moltis-org/moltis/pull/970) 修复了代理环境下（如Docker端口转发）的登录问题，通过检查`X-Forwarded-Proto`头来决定Cookie的`Secure`属性，提升了部署友好性。

- **沙箱与稳定性**：
    - PR [#942](https://github.com/moltis-org/moltis/pull/942) 合并了**远程和多后端沙箱支持**（Vercel, Daytona, Firecracker），解决了云部署环境中Docker-in-Docker不可用的问题，极大扩展了Moltis的部署场景。
    - PR [#971](https://github.com/moltis-org/moltis/pull/971) 修复了并行工具调用导致的**Docker沙箱名称冲突问题**，通过序列化同一会话的容器启动操作，增强了系统在高并发下的稳定性。

- **集成与依赖**：
    - PR [#961](https://github.com/moltis-org/moltis/pull/961) 修复了DeepSeek模型在“思考”模式下的内容回传错误，确保了与该流行模型的兼容性。
    - PR [#976](https://github.com/moltis-org/moltis/pull/976) 新增了Agent身份和入门协议的集成文档，为社区开发者理解和实现跨服务器信任提供了指导。
    - 多个依赖更新PR（如 `wasmtime`, `openssl`, `gix`）被合并，保持了项目技术栈的现代性与安全。

## 社区热点

今日最引人注目的讨论源于两个开放的功能性PR和一份社区提案，反映了社区对Moltis网络化、智能化和可用性的高度期待。

1.  **[PR #979](https://github.com/moltis-org/moltis/pull/979): feat(nodes): Ed25519 challenge-response node identity (TOFU)**
    - **分析**：该PR由核心维护者提出，引入基于TOFU的节点身份验证。这不仅是技术升级，更是Moltis走向“可信任的代理网络”的关键一步。它回应了社区对多个代理实例间如何安全交互的长期疑问，是解决[Issue #973](#)中提出的“互操作性”问题的具体方案。社区对此关注度极高，预计将引发关于身份验证、密钥管理和P2P网络的深度讨论。

2.  **[PR #920](https://github.com/moltis-org/moltis/pull/920): feat(telephony): add phone call support via Twilio**
    - **分析**：这是另一个重量级特性PR，将Moltis的能力从文字/代码扩展到**语音通话领域**。这表明项目正在向一个全能型的个人助理演进。社区对此反响热烈，因为它打开了自动化客服、语音交互等全新应用场景。评论讨论集中在Twilio集成细节、音频处理以及未来是否支持SIP等开源协议。

3.  **[Issue #973](https://github.com/moltis-org/moltis/issues/973): Proposal: Onboarding + Identity protocols for interoperable personal agent servers**
    - **分析**：这是一个由社区成员发起的、极具前瞻性的提案。它精准地指出了当前Moltis作为独立代理的局限，并提出了 **“互操作性协议”** 这一概念。该提案与PR #979的方向不谋而合，表明社区思考已领先于当前代码实现。它代表了用户从“使用工具”到“构建生态”的诉求转变，是项目未来路线图中的重要信号。

## Bug 与稳定性

今日报告的Bug数量不多，且集中于特定部署场景，其中2个已有修复PR被合并。项目整体稳定性控制良好。

- **高严重性**：
    - **[Bug] Docker环境下的浏览器沙箱失败** — [Issue #977](https://github.com/moltis-org/moltis/issues/977) (开放中，未关联PR)
        - **摘要**：在Docker内运行Moltis时，浏览器沙箱工具初始化失败。
        - **潜在影响**：这会阻止在容器化部署中使用浏览器相关功能。目前无修复PR，需要紧急评估。

- **中等严重性（已修复）**：
    - **[Bug] 并行工具执行导致Docker沙箱名称冲突** — [Issue #964](https://github.com/moltis-org/moltis/issues/964)
        - **修复**：该Bug已在今日被修复，并由PR [#971](https://github.com/moltis-org/moltis/pull/971) 合并。
    - **[Bug] DeepSeek思考模式内容回传错误** — [Issue #959](https://github.com/moltis-org/moltis/issues/959)
        - **修复**：该Bug已在今日被修复，并由PR [#961](https://github.com/moltis-org/moltis/pull/961) 合并。

- **低严重性（已修复）**：
    - **[Bug] 登录失败** — [Issue #968](https://github.com/moltis-org/moltis/issues/968)
        - **修复**：该Bug由PR [#970](https://github.com/moltis-org/moltis/pull/970) 合并，与代理环境下的Cookie安全属性有关。
    - **[Docs] 语音服务TTS文档链接失效** — [Issue #958](https://github.com/moltis-org/moltis/issues/958)
        - **修复**：文档问题已通过PR [#962](https://github.com/moltis-org/moltis/pull/962) 合并修复，指导用户连接至维护中的仓库。

## 功能请求与路线图信号

1.  **多代理互操作协议** — [Issue #973](https://github.com/moltis-org/moltis/issues/973)
    - 这是今日最强的路线图信号。项目已通过PR [#979](https://github.com/moltis-org/moltis/pull/979) 和 [#976](https://github.com/moltis-org/moltis/pull/976) 做出回应，可以预见“节点身份”和“Agent发现”将成为下一个开发周期的核心主题。
2.  **电话通话支持** — [PR #920](https://github.com/moltis-org/moltis/pull/920) **(Open)**
    - 该功能特性已进入实质性开发阶段，有望在未来几个版本中正式发布。
3.  **远程沙箱支持** — [PR #942](https://github.com/moltis-org/moltis/pull/942) **(Closed)**
    - 已合并，将成为下一版本的亮点功能，标志着Moltis从纯本地部署向混合云部署迈出关键一步。

## 用户反馈摘要

- **痛点**：
    - 容器化部署（如Proxmox LXC）是用户的热点部署场景，但[浏览器沙箱在Docker内失败](https://github.com/moltis-org/moltis/issues/977)是一个常见的阻碍性问题。
    - 用户对于配置某些服务（如DeepSeek）的细节非常敏感，[工具使用的并发问题](https://github.com/moltis-org/moltis/issues/964)也暴露了早期用户的真实压力挑战。
- **正面反馈**：
    - 社区对项目积极响应用户反馈并迅速修复Bug（如登录失败、文档链接、DeepSeek问题）表示赞赏，这反映了项目的健康度。
    - 社区对于**“让个人代理互联”** 的愿景充满热情，[提案](https://github.com/moltis-org/moltis/issues/973)获得了积极反响，表明用户不再满足于单一工具，而希望构建一个去中心化的代理网络。

## 待处理积压

1.  **[PR #920] 电话通话支持（Twilio）** — [链接](https://github.com/moltis-org/moltis/pull/920)
    - 状态：**开放中**（自2026-04-29起）
    - 重要性：这是一个大型功能特性，虽然仍在开发中，但其复杂性可能导致较长的审查周期。提醒维护者关注，避免长期停滞。
2.  **[Issue #977] Docker环境下的浏览器沙箱失败** — [链接](https://github.com/moltis-org/moltis/issues/977)
    - 状态：**开放中**（2026-05-06创建）
    - 重要性：这是一个直接影响Docker用户的关键Bug，目前无评论或关联PR。建议维护者尽快响应。
3.  **[PR #358] 修复企业版Copilot令牌路由** — [链接](https://github.com/moltis-org/moltis/pull/358)
    - 状态：**已关闭**（自2026-03-08，本周被合并）
    - 备注：虽然是历史遗留问题，但该PR历经两个月才被处理，建议回顾此类长期悬而未决的PR的响应流程。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的 CoPaw 项目 GitHub 数据，我为您生成了以下项目动态日报（2026-05-07）。

---

# CoPaw 项目动态日报 | 2026年5月7日

## 1. 今日速览

今日项目整体保持高速迭代与社区高度活跃的态势。过去24小时内，共关闭/处理了24个Issue和26个PR，代码库以极高效率向前推进。社区讨论焦点集中在内置技能/MCP的扩展性（#280）与长对话场景下的稳定性问题，也反映出用户从尝鲜转向生产级应用的需求。版本发布方面，v1.1.5.post2 主要是一个小版本修正，重点优化了聊天体验和文档同步。整体来看，项目健康度非常高，社区贡献活跃，但需要持续关注因对话过长或特定模型引发的稳定性Bug。

## 2. 版本发布

- **新版本：v1.1.5.post2**
  - **更新内容**：
    1.  **文档同步**：更新网站文档至v1.1.5版本。
    2.  **特性优化**：支持通过LLM异步生成会话标题，提升了大模型对话的交互体验。
    3.  **Bug修复**：涉及消息处理流程的修复，旨在提升消息处理的稳健性。
  - **破坏性变更**：无。
  - **迁移注意事项**：此版本为常规小版本迭代，预计无特殊迁移要求。

## 3. 项目进展

今日项目共有26个PR被合并或关闭，进度显著。以下是推动项目向前迈进的关键工作：

- **前端性能与体验优化**：多个PR聚焦于提升前端交互流畅性。
  - `#4052` 通过使用 `JSON.stringify` 进行数据对比，解决了因轮询导致的不必要重新渲染问题。
  - `#3912` 通过 `react-window` 实现了聊天会话列表的虚拟化，预期能显著改善超长会话列表下的性能。
  - `#3934` / `#3943` 修复了会话重命名时无法输入中文等细节问题，并优化了会话列表样式。
- **功能与修复**：
  - **日志系统优化**：`#4076` 引入了 `RotatingFileHandler`，解决了 `qwenpaw.log` 文件长期运行后无限增长的问题。
  - **默认Agent命名**：`#4073` 修复了默认Agent忽略用户自定义名的Bug，提升了配置一致性。
  - **文件预览修复**：`#4089` 移除了文件预览路径中冗余的URL前缀，初步修复了文件链接过期相关的部分问题（关联Issue #4047）。
  - **渠道迁移**：`#3605` 完成了微信渠道（WeChat/Weixin）重命名后的数据迁移工作，通过集中的初始化步骤替换了分散的懒加载，提升了数据一致性。
- **新功能探索**：`#3999`（由首次贡献者提交）新增了 `qwenpaw skills test` 命令，允许用户在部署前验证技能配置，这是对开发者工具链的有益补充。

## 4. 社区热点

今日讨论最热烈的 Issue 与分析如下：

- **`#280` [讨论] 哪些技能和MCP可以作为内置功能？**
  - **链接**: `agentscope-ai/QwenPaw Issue #280`
  - **热度**: 评论27条，且从3月2日持续至今。
  - **分析**: 这是社区对“开箱即用”体验的强烈呼声。用户希望项目不仅能支持自定义扩展，还应预先集成一些通用、热门的技能和MCP，以降低新用户的使用门槛。此讨论反映了项目在从开发者工具向更通用平台演进过程中的核心痛点。

- **`#4059` [已关闭] 对话内容过长后无法正常回复**
  - **链接**: `agentscope-ai/QwenPaw Issue #4059`
  - **热度**: 评论8条，一天内从创建到关闭。
  - **分析**: 这是另一个版本的长对话稳定性问题，与 `#3350` 类似。用户反馈即使使用 `/compact` 指令也无法解决，需开启新对话。此问题获得快速响应并被关闭，表明团队已意识到并可能已通过新版本或配置调整修复。这凸显了该问题的普遍性和高优先级。

- **`#3753` [已关闭] 何时支持火山引擎的 coding plan 模型？**
  - **热度**: 评论8条。
  - **分析**: 用户持续关注对特定国内云计算平台模型的原生支持。这不仅是功能请求，更是对项目在国内生产环境落地的迫切需求，与 `#1502` 中提到的火山引擎Bug相关联。

## 5. Bug 与稳定性

今日报告的Bug主要集中于长对话、模型兼容性和渠道稳定性，按严重程度排列如下：

- **严重**
  - **[Bug] 流式模型（如MiMo/DeepSeek）导致ReAct循环重复调用工具和输出 (`#4034`)**：这是一个严重的逻辑Bug，会导致工具调用错误和响应混乱。已指明是特定模型的streaming响应触发了重复处理。目前暂无直接fix PR。
  - **[Bug] 微信渠道在正常网络下会丢失消息 (`#4056`)**：Agent会突然停止响应，影响核心功能。这是一个严重的影响用户体验的Bug。目前暂无直接fix PR。
  - **[Question] 长对话无法回复 (`#4059`)**：虽已关闭，但问题本身严重，反映了长期对话管理的痛点。

- **中等**
  - **[Bug] 文件/图片链接一天后过期 (`#4047`)**：后端令牌过期策略导致前端交互失败，严重影响历史消息查看。相关PR `#4089` 已合并，仅修复了文件预览路径问题，但根本问题（Token过期）仍需关注。
  - **[Bug] Windows版打包冲突 (`#3988`)**：打包工具 `conda-pack` 与 `pip install` 动作冲突，影响Windows用户部署。`#4093` 已提交修复PR，旨在修复此问题。
  - **[Bug] Reasoning内容在OpenAI兼容提供商中未被过滤 (`#4006`)**：特定于MiniMax等第三方提供商，可能导致信息泄露或格式错误。
  - **[Bug] MCP Client `timeout` 不可配置 (`#3997`)**：Pydantic模型未暴露 `timeout` 字段，导致用户无法调整超时，影响长时间运行的任务。

## 6. 功能请求与路线图信号

从今日活跃的Issues和PR中，可以解析出以下可能影响未来版本走向的需求信号：

- **高优先级潜力**：
  - **简化模型配置流程 (`#4036`)**：用户反映添加新模型需要的步骤太多，这是提升用户体验的显著痛点。
  - **批量管理技能 (`#4091`)**：关联PR `#4091` 旨在为技能添加“启用/禁用”的批量操作按钮，对应了社区对高效管理技能的需求。
  - **优化技能选择UI (`#4078`)**：用户建议用交互式下拉菜单取代纯文本技能列表，这将是UI体验的重要改进。

- **中期规划可能性**：
  - **自适应/自我进化技能 (`#2473`)**：已有PR提交了自我进化的AI Agent能力，虽然该Issue已关闭，但反映了社区对更高级Agent模式的探索。
  - **任务规划Notebook (`#3238`)**：该PR处于“Under Review”状态，旨在为Agent增加任务分解与执行能力，是向更复杂、结构化任务处理演进的重要一步。
  - **自定义工作区路径 (`#3967` & `#4067`)**：用户强烈希望将核心配置与用户工作区分离，这对生产环境的安全性、数据管理至关重要。
  - **引入Hermes机制 (`#4024`)**：社区开始讨论借鉴更优秀的框架（如Hermes）来升级CoPaw，表明开发者和用户对核心架构的持续思考。

## 7. 用户反馈摘要

从今日的Issue评论中，可以明确感知到以下用户痛点与使用场景：

- **“对话太长，体验很差”**（`#4059` 作者 `pengliang159`）: 用户在大型代码迭代项目（如从零构建一个工程）中频繁遇到因对话过长而导致回复中断的问题，迫使其频繁开启新窗口，严重破坏了开发流程的连续性。
- **“工作区文件太乱，容易误删”**（`#3967` 作者 `SeoMP`）: 用户（尤其是非开发者）反映Agent工作区混杂了大量用户文档和系统配置，清理时风险高，强烈建议将两者分离。
- **“控制台反应越来越慢”**（`#3830` 作者 `jerry78424`）: 用户在近期更新后反馈Windows桌面版卡顿，尤其在浏览长会话列表时，说明前端性能优化是持续性的需求。
- **“缺乏测评和汇报能力”**（`#4008` 作者 `linhuang0405`）: 用户期望将CoPaw用于生产环境并向领导汇报，但目前缺少完整的聊天记录导出或测评功能，无法量化Agent的工作表现。
- **“微信对话和浏览器过程不同步”**（`#4000` 作者 `git-coinco`）: 用户在使用微信渠道时，无法看到Agent在浏览器中的操作过程，这降低了透明度和可控性。

## 8. 待处理积压

以下是可能被忽略或等待社区回应的长期议题，提醒维护者关注：

- **`#280` [开放] 讨论：哪些技能和MCP可以作为内置功能？**
  - 这个从3月初开始的长期讨论，至今仍有27条评论，是社区最核心的诉求之一。虽然讨论热烈，但尚未看到明确的官方决策或路线图回应。
- **`#2235` [开放] 功能请求：期望可以通过web控制台进行CoPaw的升级**
  - 该提案获得了社区的支持（👍:1），旨在提升远程运维能力。缺乏回应可能导致社区贡献者和使用者感到功能发展瓶颈。
- **`#3238` [开放] 新增任务规划的PlanNotebook支持**
  - 此PR已持续近一个月处于“Under Review”状态。该功能对提升Agent处理复杂任务的能力至关重要，长期的审核状态可能阻碍社区贡献者的积极性。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，根据您提供的 GitHub 数据，以下是为 ZeroClaw 项目生成的 2026-05-07 项目动态日报。

---

## ZeroClaw 项目动态日报 — 2026-05-07

### 1. 今日速览

ZeroClaw 项目在过去24小时内保持了极高的活跃度。基础架构优化与功能扩展并行推进：配置系统的类型安全重构接近尾声（PR #6403 已合并），为 v0.8.0 奠定基础；同时，社区驱动的多通道（SMS、聊天平台）和桌面端（macOS）功能请求集中爆发，成为今日最显著的动态。版本 v0.7.5 的发布流程虽因 CI 问题受阻，但修复已就绪。总体而言，项目处于“基础设施稳中有进，功能生态百花齐放”的高活跃阶段。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

- **配置系统核心重构完成评估**：PR #6403 (`feat(config,providers): typed-family split for model + TTS providers`) 已关闭。该 PR 是通向 v0.8.0 的关键一步，将模型和 TTS 提供商配置拆分到类型安全的族（family）结构中，移除了废弃的 Azure 字段，并规范了命名。此合并为未来的扩展和维护性打下了坚实基础。
- **桌面端（macOS）启动器站稳脚跟**：PR #6506 (`feat(desktop): macOS onboarding wizard, permission primitives, and capability sync`) 已提交。该 PR 为 Tauri 桌面应用增加了 macOS 首次运行引导向导，并为截图、AppleScript 等操作所需的系统权限建立了基础原语。这标志着桌面端从”能运行”向”可用、易用”迈出了关键一步。
- **安装与启动体验优化**：
  - PR #6496 (`fix(install): picker prompts go to stderr so they actually appear`) 已合并，修复了交互式安装脚本中提示信息被隐藏的问题。
  - PR #6493 (`fix(gateway,channels): boot without configured model so /onboard stays reachable`) 已合并，确保网关在未配置模型时仍能正常启动并引导用户访问 `/onboard` 设置页面，显著提升了首次使用体验。
- **文档和 CI 持续改进**：
  - PR #6486 (`fix(docs): generate lang switcher before mdbook sync`) 已合并，解决了文档多语言切换器生成时序问题。
  - PR #6502 (`fix(ci): unblock v0.7.5 release — run gen-api before tsc...`) 已提交，旨在修复阻碍 v0.7.5 发布的 CI 问题。

### 4. 社区热点

- **新 Logo 设计（#4710）**：作为最老的开放 Issue 之一，该帖获得了 10 条评论和 2 个 👍。社区对标志性品牌形象有持续兴趣，这虽非功能性问题，但反映了用户对项目认同感的需求。
- **多智能体交互流程 RFC（#5890）**：该提案在 7 天讨论期结束后，核心团队投票通过，今日仍在接收评论（8条）。这表明社区对高阶代理编排功能有强烈期待，该 RFC 的成功推进是产品路线图上的重要里程碑。
- **v0.7.5 版本发布追踪（#5878）**：作为发布里程碑追踪 Issue，其 8 条评论反映了社区对稳定新版本的期待。由于 CI 问题（#6502）导致的发布延迟，更是放大了这种关注度。

### 5. Bug 与稳定性

- **高风险**：
  - **LLM 重复请求（#6474）**：用户报告在处理用户请求时，LLM 被重复调用。用户提供了详细的 `o1mx` 本地部署环境配置。目前状态为 `in-progress`，无关联 PR。
  - **Postgres 网关崩溃（#6472）**：用户反馈使用 Postgres 后段时，网关因“Cannot start a runtime from within a runtime”错误而 panic，严重性被标记为 S2（降级行为）。目前无关联 PR。
  - **凭证继承失败（#6418 - 已关闭）**：报告了故障转移时，备用提供商无法继承主配置中的凭证问题。此问题被标记为重复（duplicate）并已关闭，但“S0 - 数据丢失/安全风险”的严重性标签表明其影响重大，需关注其解决方案是否已在其他 PR 中妥善处理。
- **中风险**：
  - **WhatsApp 频道自回复（#6413 - 已关闭）**：已修复并关闭。该 Bug 导致代理会回复自己发送的消息。
  - **Cron 任务表格 UI 异常（#6504）**：提交日期就是今日。用户反馈表格头部样式改变后，列对齐和内容截断行为怪异。关联 PR #6505 (`fix(web): cron jobs table behaviour`) 已提交正在修复。

### 6. 功能请求与路线图信号

- **“万物皆插件”架构（#6489）**：这是一个影响深远的**长期路线图提案**，提议将现有的”集成”（频道/提供商）和”插件”（WASM 模块）统一为单一插件目录。这反映了项目向模块化、可扩展生态系统演进的趋势。
- **桌面端能力爆发**：以 `theonlyhennygod` 为主导的贡献者提交了近 10 个关于 macOS 桌面端的功能请求，包括持久化 WebSocket 连接、截图、UI 控制等。结合已提交的 PR #6506 和 #6507，可预见 **v0.7.7 之后的桌面端将是下一阶段的重点**。
- **新渠道需求井喷**：超过 10 个新频道功能请求在同一天提出，涵盖 Twilio、Plivo、Sinch、Telnyx、Vonage 等 SMS 提供商，以及 Zulip、Rocket.Chat、Mastodon、Twitch、Lemmy 等聊天/社交平台。这表明社区强烈希望 ZeroClaw 能连接任何通信触点，**“无处不在”成为核心诉求**。部分请求（如 #6435、#6437）状态已是 `in-progress`，预计将被优先实现。

### 7. 用户反馈摘要

- **对决策过程的热情**：社区对 RFC 和多智能体 UX 流程等架构决策表现出高度参与感，讨论积极。
- **配置复杂性与灵活性**：用户对配置系统的复杂性（如 Fallback 凭证、不同提供商的差异）感到困惑，这推动了 #6273 和已合并的 #6403 等重构工作。
- **期望与主流平台集成**：最响亮的用户声音是希望 ZeroClaw 能与更多通讯渠道集成，特别是国内/国际主流的 SMS、Mastodon、Rocket.Chat 等，反映了用户希望将代理嵌入其现有工作流中的真实需求。
- **对桌面端体验的期待**：用户对 macOS 桌面端的原生截图、自动化等能力表现出浓厚兴趣，认为这能极大地扩展代理的能力边界。

### 8. 待处理积压

- **新 Logo 设计（#4710）**：开放超过 1 个月，仍为开放状态且有多条评论。此类长期未决的”品牌”类 Issue 易导致社区热情消耗，建议维护团队明确表态或建立社区提交流程。
- **自定义推理提供商 TLS 支持（#5797）**：自 4 月 16 日以来，该 PR 因“需要作者操作”（`needs-author-action`）而停滞。对于企业级用户至关重要的功能，长时间未得到推进可能影响项目在主流市场的采用。
- **Slack Bot Token 配置修复（#6287）**：同样标记为“需要作者操作”，涉及 Slack 频道一个已确认的配置缺陷。在 Slack 仍是重要协作工具的背景下，此 PR 的受阻值得关注。

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*