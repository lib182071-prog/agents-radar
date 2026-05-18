# OpenClaw 生态日报 2026-05-18

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-18 12:51 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 OpenClaw 项目数据，生成了 2026-05-18 的项目动态日报。

---

### OpenClaw 项目动态日报 | 2026-05-18

---

#### **1. 今日速览**

今日 OpenClaw 项目社区活动**异常活跃**，24小时内新增/更新了 500 条 Issue 和 500 条 PR，显示出极高的社区参与度。然而，PR 合并率较低（~28.6%），大量 PR 处于“待审核”或“等待作者”状态，表明维护者资源可能成为瓶颈。版本更新集中在 Mac 应用的 UI 重构和依赖更新上。安全性与会话状态管理是当前社区最核心的关注点，多个高优先级（P1）Bug 正待解决，项目整体处于**高强度迭代与稳定化并重**的阶段。

#### **2. 版本发布**

今日发布了 3 个 Beta 版本，主要内容为迭代式改进与依赖更新。

-   **v2026.5.16-beta.5 & v2026.5.16-beta.6**
    -   **核心更新**：针对 Mac 应用进行了重大 UI 重构，重新设计了“设置”页面，采用统一的卡片式布局、缓存导航，并优化了权限、语音、技能等多个设置面板。
    -   **技能重命名**：将仓库本地的 `Codex closeout review skill` 重命名为 `autoreview`。这属于内部 API 变更，如果用户自定义脚本依赖了原始名称，需注意迁移。

-   **v2026.5.16-beta.7**
    -   **依赖更新**：更新了核心依赖 `@openclaw/proxyline` 至 0.3.3 版本，并更新了 Pi 包至 0.75.1 版本，将最低支持的 Node.js 版本提升至 22.19 行（可能为 22.19.0 的笔误）。
    -   **新增特性**：在 Docker/Podman 镜像构建中新增 `OPENCLAW_IMAGE_APT_PACKAGES` 运行时无关的环境变量，允许用户为容器镜像安装额外的 apt 包，增强了部署灵活性。
    -   **迁移注意**：最低 Node.js 版本要求提升，请确保部署环境 Node.js 版本 >= 22.19。

#### **3. 项目进展**

尽管合并率不高，但今日仍有一些关键 PR 被合并，推动了特定领域的进展。

-   **消息可见性修复**：PR [#83571](https://github.com/openclaw/openclaw/pull/83571) (`fix(messages): keep Codex source replies tool-gated`) 已合并。此 PR 修复了 Codex 源回复的消息传递问题，默认将其保持在工具网关层级，并提供了显式选项来控制可见性。这是一个重要的稳定性修复，直接关系到用户体验。
-   **Cron 认证修复**：PR [#83587](https://github.com/openclaw/openclaw/pull/83587) (`fix(cron): use resolveApiKeyForProvider for preflight probe auth`) 已合并。此 PR 修复了 cron 任务的预检认证问题，解决了因未携带 `Authorization` 头而导致代理日志中出现大量 `401` 错误的问题。

这些合并表明项目正在积极解决关键的运行时稳定性问题，尤其是在消息传递和自动化任务方面。

#### **4. 社区热点**

今日社区讨论高度集中在几个核心议题上：

1.  **跨平台支持（#75）**：[Issue #75](https://github.com/openclaw/openclaw/issues/75) “Linux/Windows Clawdbot Apps” 以 104 条评论和 75 个 👍 成为绝对热点。用户强烈要求官方为 Linux 和 Windows 提供与 macOS 功能对等的桌面客户端。这反映了社区对更广泛平台支持的迫切渴望。

2.  **消息泄露与上下文混乱（#25592, #32296）**：这两个 P1 级别的 Bug 引发了热烈讨论（评论共 38 条）。
    -   [#25592](https://github.com/openclaw/openclaw/issues/25592) “Text between tool calls leaks to messaging channels”：描述了工具调用之间的处理文本（如错误、确认信息）被错误地发送到外部聊天频道（如 Slack）的重大 UX 问题。
    -   [#32296](https://github.com/openclaw/openclaw/issues/32296) “Agent replies to previous message instead of current message”：描述了代理会回复上一条消息而非当前消息的上下文混乱问题。
    -   **分析**：这两个问题共同指向**会话管理与上下文隔离**的薄弱环节，是影响用户核心体验的关键障碍。

3.  **安全与权限控制（#75, #10659, #32473）**：安全相关的讨论贯穿多个高热度 Issue。
    -   [#10659](https://github.com/openclaw/openclaw/issues/10659) 关于“Masked Secrets”的请求有 12 条评论和 4 个 👍，用户希望防止代理直接访问明文 API Key。
    -   [#32473](https://github.com/openclaw/openclaw/issues/32473) 关于控制 UI 的 HTTPS/localhost `secure context` 问题，讨论也很活跃。

**小结**：社区渴望更强大的桌面客户端体验，同时，会话管理的准确性和安全性是用户当前最关心、最影响日常使用的痛点。

#### **5. Bug 与稳定性**

今日报告的 Bug 数量众多，按严重程度排列如下：

-   **高严重性 (P1, Diamond Lobster 或 Platinum Hermit 评级)**：
    -   **消息泄漏**：[#25592](https://github.com/openclaw/openclaw/issues/25592) （Text between tool calls leaks）。**已有合并的修复 PR #83571**，值得关注其效果。
    -   **进程死锁与崩溃**：[#22676](https://github.com/openclaw/openclaw/issues/22676) （Signal daemon stop() race condition），[#71127](https://github.com/openclaw/openclaw/issues/71127) （Stuck sessions never aborted）。后者虽已关闭，但根本原因分析表明其影响持续存在。
    -   **会话状态错误**：[#32296](https://github.com/openclaw/openclaw/issues/32296) （Agent replies to previous message）。
    -   **关键功能回归**：[#38327](https://github.com/openclaw/openclaw/issues/38327) （"Cannot convert undefined or null to object" with google-vertex/gemini），[#32473](https://github.com/openclaw/openclaw/issues/32473) （Control UI requires secure context）。这些回归问题表明近期更新引入了一些兼容性问题。
    -   **安全漏洞**：[#29387](https://github.com/openclaw/openclaw/issues/29387) （Bootstrap files ignored），[#29736](https://github.com/openclaw/openclaw/issues/29736) （Exec approvals writes wrong path），[#31331](https://github.com/openclaw/openclaw/issues/31331)（Docker Sandbox workspace binding fails）。
    -   **已有关联修复 PR**：除 #25592 外，#22676、#32296、#32473 等严重 Bug 均有 `clawsweeper:linked-pr-open` 标签，表明社区正在积极贡献修复，但尚未合并。

-   **中严重性 (P2)**：
    -   **功能缺失**：[#9443](https://github.com/openclaw/openclaw/issues/9443) （Prebuilt Android APK），[#29387](https://github.com/openclaw/openclaw/issues/29387) （Bootstrap files in agentDir ignored），[#40540](https://github.com/openclaw/openclaw/issues/40540) （`openclaw update` EBUSY error on Windows）等。
    -   **性能与可靠性**：[#40611](https://github.com/openclaw/openclaw/issues/40611) （Heartbeat blocks Telegram），[#80520](https://github.com/openclaw/openclaw/issues/80520) （Telegram messages silently dropped）。这些 Bug 直接影响了 Telegram 等核心渠道的稳定性，对日常用户干扰极大。
    -   **低严重性 (P3)**：如 [#33329](https://github.com/openclaw/openclaw/issues/33329)（Document implicit discovery mechanisms）等，更偏向于文档完善和体验优化。

#### **6. 功能请求与路线图信号**

-   **高概率候选功能（有对应的活跃 PR）**：
    -   **Slack Block Kit 支持** ([#12602](https://github.com/openclaw/openclaw/issues/12602))：有相关 PR [#82258](https://github.com/openclaw/openclaw/pull/82258) “Render Slack progress drafts as plan cards” 推进中，表明该项目很可能被纳入后续版本。
    -   **子代理工具允许列表**：PR [#78441](https://github.com/openclaw/openclaw/pull/78441) “feat(subagents): forward toolsAllow from sessions_spawn” 已准备就绪，等待维护者审核，这将增强子代理的安全控制。
    -   **Telegram 消息设置**：PR [#39905](https://github.com/openclaw/openclaw/pull/39905) “feat(telegram): scope reply and streaming settings per conversation” 已提出，旨在增强 Telegram 频道个性化。
    -   **直接执行模式**：Issue [#18160](https://github.com/openclaw/openclaw/issues/18160) “Direct Exec Mode for Cron Jobs” 获得 9 个 👍，用户需求强烈，尚无关联 PR。

-   **长期愿景信号**：
    -   **多代理协作增强** ([#35203](https://github.com/openclaw/openclaw/issues/35203))：提出了能力画像、共享黑板、分层记忆等 RFC，标志着社区对更复杂的多代理工作流产生了浓厚兴趣。
    -   **原生秘密管理** ([#13610](https://github.com/openclaw/openclaw/issues/13610))：与 AWS Secrets Manager、Vault 等集成，这是向企业级应用发展的重要迹象。
    -   **安全/非安全 ClawdBot** ([#6731](https://github.com/openclaw/openclaw/issues/6731))：讨论用 Rust 重写以增强安全性的激进建议，表达了部分社区成员对安全和内存安全的深度关切。

#### **7. 用户反馈摘要**

-   **积极反馈**：
    -   用户对 Mac 应用 UI 的重设计表示赞赏，beta.5/6 的更新日志中提到“重建设置页面...更稳定的间距”，说明内部测试收到了积极反馈。
    -   社区贡献者非常活跃，愿意承担关键 Bug 的修复（如 `steipete`、`stainlu` 等），显示出强大的社区力量。

-   **核心痛点**：
    -   **消息泄漏/上下文混乱**：用户反映“代理发错了消息”、“工具调用中间的处理过程被公开”，感到非常困扰。这是**影响日常使用流畅度的头号问题**。
    -   **稳定性问题**：“Telegram 消息静默丢弃”、“网关重启后子进程残留”等问题严重影响了用户对一个全天候运行的个人助手的信任。
    -   **初始配置复杂**：[#16670](https://github.com/openclaw/openclaw/issues/16670) 指出 Onboarding Wizard 未包含 Memory/Embedding 配置，导致新用户配置缺失，无法使用核心功能。用户认为“Memory 是 OpenClaw 最重要的特性之一”。
    -   **沙箱限制**：[#37634](https://github.com/openclaw/openclaw/issues/37634) 指出当 `workspaceAccess` 设为 `none` 时，用户的隔离工作空间竟然是只读的，导致部分工具无法正常工作，用户表示“这出乎意料”。
    -   **Windows 支持**：[#40540](https://github.com/claw/openlaw/issues/40540) 报告了 Windows 上 `openclaw update` 命令的 EBUSY 错误，表明 Windows 平台的稳定性仍有待提升。

#### **8. 待处理积压**

-   **长期未解决的高关注度 Issue**：
    -   [#75](https://github.com/openclaw/openclaw/issues/75) Linux/Windows 桌面应用。自 2026-01-01 创建以来已活跃 138 天，评论数 104，是社区关注度最高的 Issue。目前仍处于 `needs-product-decision` 和 `needs-maintainer-review` 状态，**项目维护者应尽快澄清或更新路线图**。
    -   [#6731](https://github.com/openclaw/openclaw/issues/6731) 关于使用 Rust 重写以实现“安全/不安全”模式的讨论，虽然较为激进，但代表了部分核心用户对安全性的深度关切，已创建 106 天。

-   **长期未解决的 PR**：
    -   PR [#40522](https://github.com/openclaw/openclaw/pull/40522) “fix(gateway): redirect / to control UI basePath” 创建于 2026-03-09，已等待审核 70 天。这是一个小但有意义的 UI 改进，长期未合并可能会打击贡献者的积极性。
    -   PR [#42223](https://github.com/openclaw/openclaw/pull/42223) “Fix sidebar tree collapse not hiding child items” 创建于 2026-03-10，也已等待多日。

以上即为 2026-05-18 的 OpenClaw 项目日报。

---

## 横向生态对比

好的，作为 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我已整合您提供的所有项目动态数据，现呈上横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态横向对比报告 | 2026-05-18

#### 1. 生态全景

今日，个人 AI 助手与自主智能体开源生态呈现出 **“繁花似锦”与“根基未稳”并存的局面**。一方面，社区贡献极度活跃，以 OpenClaw 系为首的多个项目每日产生数百条 Issue/PR，推动着功能边界快速扩展；另一方面，**“会话状态管理”** 与 **“模型兼容性”** 成为普遍性的阵痛。大量高优先级 Bug 集中在消息泄漏、上下文混乱、限流崩溃以及与新模型 API（如 DeepSeek-V4、Gemini）的适配延迟上。这表明生态正从“能用”向“好用”过渡，稳定性与模型适配的精细度已成为赢得用户信赖的关键。同时，多模态（图像/视频生成）和安全控制（工具隔离、秘密管理）的需求在多项目中同时涌现，指明了下一阶段的技术攻坚方向。

#### 2. 各项目活跃度对比

| 项目名称 | 今日 Issues 数 | 今日 PR 数 | **今日Release** | **活跃度评级** | **健康度评估** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | 3 (Beta) | 极高 (爆发期) | 中危 (维护瓶颈，大量待审PR) |
| **ZeroClaw** | 15 | 50 | 无 | 极高 (密集开发) | 中危 (PR积压严重，高优Bug待解) |
| **CoPaw** | 26 | 28 | 无 | 极高 (密集开发) | 中危 (PR积压，RCE漏洞待处理) |
| **NanoBot** | 5 | 26 | 无 | 高 (高速迭代) | 健康 (合并效率高，架构优化期) |
| **Hermes Agent** | 50 | 50 | 无 | 高 (社区活跃) | 中危 (P1 Bug集中，平台兼容问题多) |
| **IronClaw** | 5 | 8 | 无 | 高 (核心开发) | 健康 (架构重构期，但版本回归需警惕) |
| **PicoClaw** | 13 | 21 | 1 (Nightly) | 高 | 健康 (团队响应迅速，功能/修复并进) |
| **Moltis** | 6 | 8 | 1 | 高 (社区响应快) | 优秀 (Bug修复效率极高) |
| **NanoClaw** | 8 | 29 | 无 | 中 (PR积压, Issue不均衡) | 亚健康 (审查瓶颈，数据库Bug多) |
| **LobsterAI** | 0 | 17 | 无 | 中 (整合期) | 健康 (开发目标明确，Release分支合并) |
| **NullClaw** | 2 | 0 | 无 | 低 | 基础指数 (核心功能Bug待解) |
| **TinyClaw** | 0 | 0 | 无 | 无活动 | 休眠 |
| **ZeptoClaw** | 0 | 0 | 无 | 无活动 | 休眠 |

---

#### 3. OpenClaw 在生态中的定位

**OpenClaw 无疑是当前生态的“参照系”与“最大社区”，但其庞大社区正带来显著的管理挑战。**

- **优势**：
    - **社区规模与贡献量绝对领先**：单日500条/500 PR的数据在其他项目中罕见，这带来了最丰富的技能生态、最多的Bug发现者和最活跃的功能讨论。
    - **功能广度与深度并重**：从 UI 重构、会话管理到安全策略，OpenClaw 的覆盖面是生态中最广的，是众多项目（如 NanoClaw, PicoClaw）的灵感来源或核心依赖。
- **技术路线差异**：OpenClaw 趋向于**通用、全功能的一体化架构**，以支持最复杂的个人助手场景（多渠道、多Agent、复杂工作流），但也因此面临更高的复杂度与维护成本。相比之下，NanoBot 等更侧重**模块化与可扩展性**。
- **社区对比**：OpenClaw 的日均贡献量是 NanoBot 的 20倍，是 Moltis 的 60倍。但其 PR 合并率（~28.6%）远低于 Moltis（75%），表明“社区爆炸式增长”正带来“团队资源瓶颈”，这成为其当前最核心的风险。**其积累的大量“待解决 Bug”与“未合入 PR”构成了生态的脆弱环节。**

---

#### 4. 共同关注的技术方向

多项目同时涌现的共同议题，揭示了行业的普遍困境与未来方向。

| 共同痛点/方向 | 涉及项目 | 具体诉求/根因 |
| :--- | :--- | :--- |
| **会话状态与上下文混乱** | **OpenClaw**, **Hermes Agent**, **ZeroClaw**, **CoPaw**, **PicoClaw** | 消息泄漏、回复错乱、长会话丢失、上下文指针错误。这是当前**影响用户体验的第一大障碍**。根因在于代理循环与多渠道间的状态同步设计。 |
| **模型兼容性与前沿模型适配** | **ZeroClaw**, **Hermes Agent**, **CoPaw**, **NullClaw** | 对 DeepSeek-V4、Gemini“思维/推理”模式、Kimi 流式调用等新模型 API 特性兼容不及时，导致崩溃或逻辑错误。**模型快速迭代与Agent框架缓慢适配的矛盾愈发尖锐**。 |
| **安全与细粒度控制** | **OpenClaw**, **NanoBot**, **NanoClaw**, **ZeroClaw** | 工具隔离（子代理允许列表）、秘密/API密钥管理、基于角色的权限控制、危险命令误报与绕过。**从开放走向可控**是应对多用户和企业级场景的必然要求。 |
| **多模态生成能力扩展** | **NanoBot**, **NanoClaw**, **Moltis** | 集成本地或云端图像/视频生成模型（如 Gemini, MiniMax, Veo），并完善流程（如视频拼接、结果回传）。智能体的“创造力”正成为差异化竞争点。 |
| **跨平台与部署优化** | **PicoClaw**, **NanoClaw**, **IronClaw**, **ZeroClaw** | 支持 RISC-V 架构、Linux/Windows 原生客户端（Tauri）、Docker 配置优化、容器化沙箱。**生态正在突破开发者的“舒适区”，向更广阔的硬件和部署环境蔓延**。 |

---

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全功能个人 AI 助手，侧重多渠道通信与复杂工作流 | 高级个人用户、社区贡献者 | 功能大而全，社区驱动，灵活配置，但复杂度高 |
| **NanoBot** | 高度模块化、可重用的 AI 核心库 | 下游开发者、项目集成者 | **模块化架构**，关注核心执行抽象 (`AgentRunner`) 与 Provider 解耦，强调架构质量 |
| **Hermes Agent** | 专注 Discord/Telegram 等社区平台集成，技能生态丰富 | 社群运营者、Bot开发者 | **网关优先级最高**，社区技能市场机制成熟，但平台兼容性（如 API 认证）存在短板 |
| **CoPaw** | 面向企业的自动化助手，尤其侧重 WeChat 生态 | 企业用户、技术运营 | 企业级通道（WeChat/飞书）深度优化，插件分发体系完善，但存在安全漏洞 |
| **IronClaw** | 企业级、高安全（TEE）的自主 Agent 框架 | 企业安全团队、基础设施开发者 | **TEE 原生支持**，强调“Reborn”架构升级，资源消耗优化（slim mode），但版本回归风险高 |
| **PicoClaw** | 轻量化、高可玩性的开源助手，多平台适配强 | 技术爱好者、轻量部署用户 | **与硬件（RISC-V）结合紧密**，注重易用性（LM Studio 支持）、界面交互优化 |
| **Moltis** | 快速迭代、问题响应速度极快的代理框架 | 追求稳定性的开发者 | **项目健康度最高**，Bug 报告到修复的周期短，聚焦记忆管理与钩子系统可靠性 |
| **NanoClaw** | OpenClaw 的轻量替代，强调 Agent 独立配置和私有化部署 | 对自定义和本地部署有需求的用户 | 功能与 OpenClaw 高度相关，但提供 **per-agent 独立配置**，数据库操作简洁性有待提升 |

---

#### 6. 社区热度与成熟度

- **第一梯队（爆发期/极高热度，但存在管理阵痛）**: **OpenClaw**, **ZeroClaw**, **CoPaw**。这些项目吸引了海量社区关注，贡献量惊人，但维护团队成为瓶颈，大量 PR 和严重 Bug 积压，处于“野蛮生长”阶段。
- **第二梯队（高速迭代期，社区健康度好）**: **NanoBot**, **IronClaw**, **PicoClaw**, **Moltis**, **Hermes Agent**。这些项目社区活跃，但贡献量更为可控，团队响应迅速，正积极进行架构重构或功能扩展，处于“有序扩张”阶段。其中 Moltis 的健康度最佳。
- **第三梯队（质量巩固或调整期）**: **LobsterAI**, **NanoClaw**。这些项目社区规模适中，主导权更集中地掌握在核心团队手中，正聚焦于特定版本的功能整合或稳定性修复。
- **第四梯队（低活跃/沉默）**: **NullClaw**, **TinyClaw**, **ZeptoClaw**。这些项目可能处于实验性阶段、维护者精力不足或已停止更新。

---

#### 7. 值得关注的趋势信号

从今日反馈中，可以提炼出对 AI 智能体开发者有重要价值的行业趋势：

1.  **“会话即操作系统”**：Agent 框架的深层竞争已演变为**会话上下文管理与状态持久化**之争。谁能稳、准、久地维护长对话与跨渠道状态，谁就能赢得用户。多项目反馈的混乱 Bug 表明，**这块基础性能力远未成熟**。

2.  **“模型驱动的自适应”时代到来**：新模型（如推理模型、思维链模式）的爆发式迭代，要求 Agent 框架不再是简单的 API 封装，而必须**具备对模型能力（如思维过程、工具调用格式）的“感知”与“适配”能力**。无法快速适配新模型的框架将快速被边缘化。

3.  **“治理”成为核心能力**：随着 Agent 能力增强，**权限、安全、元成本控制**从“可选”变为“必选”。`NanoBot` 的“工具隔离”，`OpenClaw` 的“秘密屏蔽”，`ZeroClaw` 的“严格解析模式”等，都指向 Agent 系统需要具备类似操作系统的“进程隔离与权限管理”能力。

4.  **生态丛林化，开源既是机会也是挑战**：OpenClaw 的爆发证明，一个强大、灵活的开源框架能迅速聚集生态。但其 PR 审查瓶颈也表明，**成功的开源项目需要一套高效的、自动化的贡献管理和代码审查流水线**，否则会被自身的社区热度所反噬。

**对开发者的建议**：如果你的应用强调**稳定、长会话和复杂逻辑集成**，建议深入研究 **Moltis** 或 **NanoBot** 的架构思路。如果你的目标是**对接前沿模型并快速验证**，务必评估框架的 Provider 抽象层设计是否足够灵活（如 `NanoBot` 的 `ImageGenerationProvider`）。如果你的场景属于**企业内部自动化（特别是通过 WeChat 集成）**，**CoPaw** 是不二之选，但需特别关注其安全更新。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，以下是为您生成的 NanoBot 项目动态日报。

---

# NanoBot 项目动态日报 | 2026-05-18

## 1. 今日速览

项目今日活跃度极高。共计 26 个 PR 更新，其中 11 个已被合并或关闭，显示社区贡献效率高；Issues 新增/活跃 5 个，关闭 3 个。核心进展集中在 WebUI 的稳定性修复、图像生成能力的扩展（新增 Gemini 和 MiniMax 支持）以及底层代码的架构重构（Agent Runner 与 Image Generation Provider 的解耦）。尽管没有新版本发布，但大量的代码合入表明项目正在为下一个里程碑做准备。当前社区活跃度评分为：**高**。

- **关键指标**: 过去 24 小时 PR 合并数 (11) 显著高于关闭的 Issues 数 (3)，说明项目合并速度快于问题解决速度，开发者精力主要集中在新功能整合与架构优化上。
- **值得关注**: 多个 WebUI 相关的 Bug 报告（如会话显示错乱、会话提前关闭）和修复 PR 同时出现，显示用户界面稳定性是目前亟待解决的核心痛点。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日项目在功能扩展、架构优化和文档完善方面均有显著推进，共合并/关闭 11 个 PR，关键进展如下：

- **图像生成能力扩展**:
    - [**#3886**](https://github.com/HKUDS/nanobot/pull/3886) **[CLOSED]**: 新增 **Gemini** 图像生成 provider，支持 Imagen 4 和 Gemini Flash 模型。
    - [**#3879**](https://github.com/HKUDS/nanobot/pull/3879) **[CLOSED]**: 新增 **MiniMax** 图像生成 provider，支持图像参考功能。
    - **意义**: 图像生成生态快速丰富，从一个 provider 扩展到多个，为用户提供了更多底层模型选择。

- **核心架构优化**:
    - [**#3892**](https://github.com/HKUDS/nanobot/pull/3892) **[OPEN]**: 重构 `AgentRunner.run()` 方法，将其从 330 行单块逻辑拆分为 9 个专注的方法，引入 `RunContext` 数据类和 `LoopAction` 枚举。这显著提升了核心执行逻辑的可读性和可维护性。
    - [**#3893**](https://github.com/HKUDS/nanobot/pull/3893) **[OPEN]**: 引入 `ImageGenerationProvider` 基类和模块级注册机制，使添加新的图像生成 provider 无需再修改 8 个文件，极大降低了未来扩展的响应成本。

- **文档与部署**:
    - [**#3875**](https://github.com/HKUDS/nanobot/pull/3875) **[CLOSED]**: 修复了 Docker 部署文档与 v0.2.0 的多处不一致，并补充了 WebUI 和 `bwrap` 沙箱的安全配置说明，解决了用户从文档直接部署会遇阻的问题。

- **WebUI 修复**:
    - [**#3889**](https://github.com/HKUDS/nanobot/pull/3889) **[CLOSED]**: 修复 WebUI 中 Markdown 渲染将单换行符折叠的问题，提升了 `/help` 等命令输出的可读性。
    - [**#3894**](https://github.com/HKUDS/nanobot/pull/3894) **[OPEN]**: 修复 WebUI 在 Agent 执行后不显示工具调用事件的 Bug，确保工具执行的完整生命周期可被用户追踪。

## 4. 社区热点

今日社区讨论热度最高的议题集中在 **WebUI 体验** 和 **核心功能（微信）兼容性** 上。

- **议题 #3790: [BUG] WebUI 会话打印内容显示错乱**
    - **热度**: 14 条评论，是今日讨论最热烈的 Issue。
    - **链接**: [HKUDS/nanobot Issue #3790](https://github.com/HKUDS/nanobot/issues/3790)
    - **诉求**: 用户在更新到最新源码后，WebUI 的对话内容在打印后显示错乱，必须刷新页面才能恢复。这严重影响了 WebUI 的正常使用，是 Top 级别的体验问题。已有一个相关的 PR [#3894](https://github.com/HKUDS/nanobot/pull/3894) 在尝试解决类似问题，但 #3790 指出的“错乱”问题可能更复杂。

- **议题 #3863: [BUG] 微信不能 Login**
    - **热度**: 5 条评论，直接关联核心渠道功能。
    - **链接**: [HKUDS/nanobot Issue #3863](https://github.com/HKUDS/nanobot/issues/3863)
    - **诉求**: 用户使用最新版微信却被告知“版本较低，无法使用功能”。这暴露了微信渠道底层协议版本耦合度过高，或者腾讯端对协议进行了调整。用户对此感到困惑和不满，因为核心的“登录”功能无法使用。

- **PR #3898: feat(agent): add restricted mode tool isolation**
    - **热度**: 作为今日新开的 PR，其提出的“工具隔离”和“受限模式”概念在安全方面具有突破性，预计将引发社区对多用户安全和权限管理的讨论。
    - **链接**: [HKUDS/nanobot PR #3898](https://github.com/HKUDS/nanobot/pull/3898)

## 5. Bug 与稳定性

今日报告的 Bug 严重影响了用户体验，主要集中在前端 WebUI 和后端渠道兼容性。

- **严重**:
    - **#3790 [OPEN]**: **WebUI 会话打印显示错乱**。影响所有 WebUI 用户，需刷新页面才能恢复，属于界面回归。建议维护者优先关联相关 PR #3894 进行排查。 [链接](https://github.com/HKUDS/nanobot/issues/3790)
    - **#3863 [OPEN]**: **微信登录失败**。导致核心功能（微信渠道）不可用，属于渠道中断故障。 [链接](https://github.com/HKUDS/nanobot/issues/3863)
    - **#3884 [OPEN]**: **WebUI 对话在第一轮回复后自动关闭**。这是一个严重的流程 Bug，使用户无法完成多轮对话。 [链接](https://github.com/HKUDS/nanobot/issues/3884)

- **中等**:
    - **#3873 [CLOSED]**: **Docker 部署文档与 v0.2.0 不一致**。已通过 PR #3875 修复，文档导致的部署失败问题已解决。 [链接](https://github.com/HKUDS/nanobot/issues/3873)

- **提议的优化点 (已由 Bug 引发)**:
    - **#3885 [OPEN]**: 因后台总是在启动时注册 `Dream` 任务，用户请求加入全局开关。这虽不算是 Bug，但反映了当前设计缺乏灵活性，不符合用户按需使用的预期。 [链接](https://github.com/HKUDS/nanobot/issues/3885)
    - **#3882 [CLOSED]**: 明确指出微信渠道基于 v1.0.3 的底层协议存在兼容性风险，与 #3863 暴露的问题吻合。 [链接](https://github.com/HKUDS/nanobot/issues/3882)

## 6. 功能请求与路线图信号

今日的社区需求信号指向了**更细粒度的安全控制**、**更好的多智能体持久化能力**以及**更灵活的配置**。

- **可能被纳入下一版本的功能**:
    - **基于角色的工具权限隔离 (#3898)**: 此 PR 提出在通道层面增加 `sender_id` 和 `is_privileged` 上下文，并筛选工具为“管理员工具”，将大模型能力限制给特定用户。这是对 #3887 提出的“危险命令授权”请求的强力响应，且已提交代码，很有可能被纳入。
    - **Mnemon 持久记忆集成 (#3888)**: 用户请求为 Agent 添加长期记忆。社区贡献者已提交集成方案，链接了第三方工具 `mnemon`，表明这个需求已具备可落地的解决方案。 [链接](https://github.com/HKUDS/nanobot/issues/3888)
    - **Dream 任务全局开关 (#3885)**: 提供了一个明确的配置来实现禁用内存整理任务。开发方向明确，改动量小，优先级较高。

- **长期路线图信号**:
    - **架构规范化 (#3892, #3893)**: `AgentRunner` 和 `ImageGeneration` 的架构重构 PR 虽然还处于开放状态，但它们指示了项目正朝着**高内聚、低耦合**的方向演进，这对于项目的长期可维护性和插件生态建设至关重要。
    - **跨平台部署优化 (#3891)**: 为 WebUI `/bootstrap` 端点增加 `bootstrap_allow_from` 配置，解决了 Docker/远程部署的访问问题，显示出项目对非本地部署场景的重视。

## 7. 用户反馈摘要

- **来自 #3863 (微信登录问题)**：用户 `KennethYCK` 感到非常困惑，因为“已更新到最新微信”却依然被告知版本低。这表明协议端的版本检测可能过于严格或存在误判，对用户技术和耐心都是考验。
- **来自 #3790 (WebUI 显示问题)**：用户 `kxsk-git` 报告“更新最新 5.13 源码版本后”出现问题，显示新版本引入了显性的回归 Bug，这会动摇用户对新版本的信任。没有人点赞该 Issue，表明问题尚未被广泛确认，但对于提出者已是痛点。
- **来自 #3873 (文档不一致)**：用户 `URD0TH` 非常细致地列举了 Docker 部署文档中 5 处“不一致和局限性”，这份报告显示社区中存在一批对文档质量要求高的专业用户，他们愿意花时间反馈细节，对项目质量建设有益。

## 8. 待处理积压

以下为长期存在的、但未被解决的 Issue 或 PR，可能对项目发展方向有重要影响，建议维护者审阅。

- **PR #3568 [OPEN]**: 添加 `Manifest` LLM 路由器支持，创建于 2026-04-30，已停留 18 天。此 PR 引入的“网关”概念与项目现有的 provider 架构强相关，需评估是否与正在进行的架构重构兼容。 [链接](https://github.com/HKUDS/nanobot/pull/3568)
- **PR #2060 [OPEN]**: 为 `shell` 工具添加可配置的特定路径白名单功能，创建于 2026-03-15，已存在超过 2 个月。此请求关乎 Agent 的安全沙箱能力，是用户安全诉求的直接体现。 [链接](https://github.com/HKUDS/nanobot/pull/2060)
- **PR #3621 [OPEN]**: 实现生产级的、面向 Hugging Face Spaces 的多角色 Agent 小队部署方案，创建于 2026-05-04。此 PR 涉及复杂的多 Agent 编排，虽然提交较早，但其功能与项目“多智能体”的目标高度契合。 [链接](https://github.com/HKUDS/nanobot/pull/3621)
- **PR #3762 [OPEN]**: 修复 Codex provider 的空白失败重试问题，创建于 2026-05-12。这是一个 provider 稳定性修复，停留较长时间。 [链接](https://github.com/HKUDS/nanobot/pull/3762)
- **Issue #2761 (如存在)**: 请检查是否存在该 Issue，如无法确认，则可省略此条。**注意**：根据提供的数据，未找到 #2761。
- **PR #2867 [OPEN]**: Telegram 群组 Allowlist，回退 Agent 和流式 thought 标签修复，创建于 2026-04-06。此 PR 功能丰富，涉及渠道安全和用户体验，存在合并冲突风险，需维护者投入时间处理。 [链接](https://github.com/HKUDS/nanobot/pull/2867)

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据提供的 Hermes Agent 项目数据，为您生成 2026年5月18日的项目动态日报。

---

# Hermes Agent 项目日报 | 2026-05-18

## 1. 今日速览

过去24小时，Hermes Agent 项目热度维持在高位，社区互动与代码贡献均十分活跃。**共处理 50 条 Issue 和 50 个 PR**，标志着项目正处于密集的开发与迭代阶段。尽管新的 Bug 报告数量较多（45个新开/活跃），但团队响应迅速，关闭了 5 个 Issue 并合并/关闭了 11 个 PR。目前 **P1 级别的严重 Bug 较为集中**，主要涉及网关稳定性、核心 Agent 循环错误及核心模块缺失，需团队优先关注。整体来看，项目发展势头强劲，但稳定性和兼容性问题是当前社区关注的核心焦点。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日共合并/关闭了 **11 个 Pull Requests**，展现了项目在多条线上同时推进。主要进展包括：

- **社区技能生态扩展**：合并了添加**韩语写作编辑器技能** (#27981) 和**并行代理对工作流技能** (#27956) 的 PR，丰富了社区贡献的技能库。
- **Discord 集成增强**：合并了允许 Discord 自由响应频道（free-response channels）选择性地开启自动线程化的 PR (#27969)，解决了之前“自由响应必为内联回复”的教条式设计，提升了灵活性。
- **UI/UX 优化**：合并了修复 TUI 时代理状态栏被`/goal`指令的详细判决信息覆盖的 PR (#27971)，改善了用户界面体验。
- **核心稳定性修复**：合并了修复**Bootstrap 脚手架**中 pip/uvx 安装后浏览器设置失败及 Windows 依赖缺失的 PR (#27826)，优化了跨平台的开箱即用体验。

## 4. 社区热点

今日讨论最为活跃的 Issue 揭示了用户在使用特定前端或网关时面临的深层问题：

- **[#15895] Google Gemini CLI 429 限流问题** (14条评论): 这是评论数最高的 Issue。用户报告即使配额（quota）显示正常，使用 Google Gemini CLI OAuth 时仍频繁遭遇 HTTP 429 限流错误。这表明问题可能不在 API 层面，而是 Hermes 客户端侧对 Gemini 的认证或请求管理逻辑存在问题，引发了社区的广泛讨论和困惑。
  - 链接: [NousResearch/hermes-agent Issue #15895](https://github.com/NousResearch/hermes-agent/issues/15895)

- **[#27339] 动态工具重排导致提示缓存/KV缓存失效** (6条评论): 这是一个高级性能问题。用户使用兼容 OpenAI 的后端时，发现动态工具打乱（Dynamic Tool Shuffling）功能会破坏 Prompt Cache，导致后续消息无法利用缓存，显著增加延迟和成本。该问题直指 Agent 框架核心的缓存策略设计，是影响长会话体验的关键瓶颈。
  - 链接: [NousResearch/hermes-agent Issue #27339](https://github.com/NousResearch/hermes-agent/issues/27339)

- **[#20500] Docker Dashboard Tab 因文件权限崩溃 (EACCES)** (5条评论): 这是一个典型的部署环境问题。在 Docker 容器中，`/opt/hermes/ui-tui` 目录为 root 所有，而 Dashboard 进程以普通用户`hermes`运行，导致权限不足。这反映了容器化部署配置的疏漏，影响了 Docker 用户的核心功能体验。
  - 链接: [NousResearch/hermes-agent Issue #20500](https://github.com/NousResearch/hermes-agent/issues/20500)

## 5. Bug 与稳定性

今日报告的 Bug 在数量和质量上都较为突出，严重性分布如下：

- **P1 (严重)**:
    - **`NameError` 导致 Agent 循环崩溃** (`#27370`): 在遇到 429 限流错误时，`conversation_loop.py` 尝试调用一个未定义的函数 `_pool_may_recover_from_rate_limit`，导致 Agent 进程直接崩溃。这是一个非常明显且应被迅速修复的 bug。
      - 链接: [NousResearch/hermes-agent Issue #27370](https://github.com/NousResearch/hermes-agent/issues/27370)
    - **Discord 网关会话提前终止** (`#27881`): 在自主工作流中，Discord 网关会错误地提前结束对话回合，导致回复不完整或任务执行中断。
      - 链接: [NousResearch/hermes-agent Issue #27881](https://github.com/NousResearch/hermes-agent/issues/27881)
    - **网关重启导致长会话丢失** (`#27856`): 在优雅关闭等待 Agent 完成时，如果超时未结束，进程被强制杀掉，会导致正在进行的长时间运行会话无法恢复。
      - 链接: [NousResearch/hermes-agent Issue #27856](https://github.com/NousResearch/hermes-agent/issues/27856)
    - **`hermes proxy` 子命令模块缺失** (`#27938`): 从源码打包的 wheel 文件缺少 `hermes_cli.proxy` 子包，导致所有 proxy 相关命令（如`hermes proxy start`）都无法使用。这是一个严重的打包/分发问题。
      - 链接: [NousResearch/hermes-agent Issue #27938](https://github.com/NousResearch/hermes-agent/issues/27938)

- **P2 (中高) & 其他值得关注的 Bug**:
    - **文件权限与路径问题**: `#20500` (Docker EACCES) 和 `#27941` (Kanban 工作区只读文件系统错误)，反映出在生产环境或特定工具链下的路径与权限处理仍有待完善。
    - **网络与代理兼容性**: `#15895` (Gemini 429) 、`#25666` (Raspberry Pi SIGSEGV) 和 `#27038` (Codex Responses API 长 ID 拒绝) 显示了不同后端、网络环境下的兼容性问题。
    - **Telegram 特定 Bug 集群**: 如 `#27970` (语音回复降级为MP3附件)、`#27942` (群组编辑流式回复不完整)、`#27139` (DM话题消息泄漏)，表明 Telegram 网关的稳定性与功能完整性是持续需要投入精力的地方。
    - **技能与工具集成 Bug**: `#26326` (技能策展人删除技能未清理引用的Cron任务) 和 `#27924` (Kanban Worker 协议违规阻塞下游任务) 反映了自动化系统内部状态管理的一致性不足。

**已有关联修复 PR**: 针对 `#27826` (Bootstrap 问题) 和 `#27969` (Discord 自动线程化) 的 PR 已被合并。对于 `#25836` (Telegram 打字指示器中断) 和 `#26388` (Codex 429重试) 的修复 PR 也已关闭。

## 6. 功能请求与路线图信号

用户提出的新功能需求呈现多样化，其中部分已有对应 PR 在推进：

- **用户界面与体验**:
    - **添加会话删除按钮** (`#27953`): 呼声较高的 UI 小需求，希望能在 Web Dashboard 界面直接执行`hermes sessions delete`的操作。已有对应 Issue 被标记为 `type/feature`。
    - **优化每轮全量加载体验** (`#27855`): 用户希望引入滑动窗口等增量机制，减轻长会话中每次都要“从头到尾刷新整个上下文”的体验问题。
    - **配置化 Discord 语音超时** (`#17790`): 希望将硬编码的 5 分钟语音不活动超时变为可配置项。

- **平台与集成**:
    - **飞书表格支持** (`#26658`): 飞书现已支持表格消息，希望移除旧的强制降级为文本的 Workaround。
    - **Kanban Worker 本地型号适配** (`#25041`): 用户社区积极询问 24GB VRAM 的本地模型运行 Kanban Worker 的实际效果，表明用户对本地化、低成本部署有着旺盛需求。

- **PR 中体现的潜在路线图信号**:
    - **自动化与治理**: `#27954` (记忆治理执行器) 和 `#27977` (单个辅助任务开关) 的提出，暗示项目正朝着更精细化的用户控制和内部状态管理迈进。
    - **技能生态深化**: `#27980` (自动生成变更日志技能) 等大量新技能的提交，表明社区驱动的技能生态正在快速形成。
    - **新平台支持**: `#27978` 正在扩展 SimpleX 聊天协议的支持。

## 7. 用户反馈摘要

从今天的 Issues 和 PR 评论中，可以提炼出以下真实用户痛点：

- **开箱即用/环境兼容性**: 用户在使用非主流后端（如 ik_llama.cpp）、特定平台（如 Raspberry Pi）或容器化部署（Docker）时，频繁遭遇兼容性和配置问题。这些问题从权限、网络到架构不一而足，是降低新用户满意度的最大障碍。
- **稳定性焦虑**: 多个 P1 Bug（如 NameError 崩溃、Discord 提前终止）直接导致 Agent 失效或回复不完整。用户对这类“服务中断”式的体验感到沮丧，尤其是在进行自主或长时间任务时，稳定性是硬性需求。
- **功能承诺的落差**: 在某些场景（如 Telegram 语音回复、Codex OAuth 集成）下，功能未能如预期般工作，或者存在奇怪的边界行为（如降级为附件、会话泄漏到错误位置），使用户感到困惑和不便。
- **对灵活性和控制的渴望**: 用户希望通过简单的配置文件就能控制更多行为，例如调整特定超时、禁用有问题的辅助任务等。这反映出项目从“功能全开”到“可精细化控制”的演进需求。

## 8. 待处理积压

以下为今日发现的、需维护者重点关注的历史遗留或长期未响应的重要项：

- **[#5326] Gateway 崩溃 (UnboundLocalError)** (P1, 创建日期: 2026-04-05): 这是一个存在超过一个月的严重网关 Bug，会导致所有平台（Discord/Telegram）的消息处理全部失效。该 Issue 依然处于 Open 状态，且今日有更新，但尚未有修复 PR。鉴于其严重性和影响范围，需尽快排期处理。
  - 链接: [NousResearch/hermes-agent Issue #5326](https://github.com/NousResearch/hermes-agent/issues/5326)

- **[#12058] OpenAI Codex OAuth 在 Telegram 网关上失效** (创建日期: 2026-04-18): 该问题反馈了 CLI 能用的 Codex 凭证，在 Telegram 网关上被提示“未存储”的问题。这暴露了网关与服务之间的认证状态同步问题，已存在一个月仍为开放状态，影响用户体验。
  - 链接: [NousResearch/hermes-agent Issue #12058](https://github.com/NousResearch/hermes-agent/issues/12058)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，这是根据您提供的 PicoClaw 项目数据生成的 2026-05-18 项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-05-18

## 1. 今日速览

PicoClaw 在 2026-05-18 迎来了一个高度活跃的开发日。社区提交量显著，尤其在功能和 Bug 修复领域。过去 24 小时内，共有 13 条 Issue 更新和 21 条 PR 更新，其中 9 个 PR 被合并或关闭，标志着多个关键问题已得到解决。**项目健康度：优秀**。社区互动热烈，尤其在“连接 LM Studio”等功能请求和“RISC-V 支持”等兼容性问题上展现了强烈的需求信号。新发布的夜间构建版本在功能迭代（如 `load_image` 配置化、SiliconFlow 提供商支持）和稳定性修复（如 PowerShell 安全、路径验证）方面均有显著推进。

## 2. 版本发布

- **版本**: `v0.2.8-nightly.20260518.0df050ff`
- **类型**: Nightly Build (不稳定的自动构建)
- **重点**: 这是一个版本周期中的夜间构建，旨在收集用户反馈并及时集成最新的代码修改。虽然标注为不稳定，但它包含了从 v0.2.8 到 main 分支间的全部变更。
- **关键内容前瞻**: 此次构建已包含今日合并的多个重要修复，例如 `load_image` 工具的可配置化、SiliconFlow 提供商的原生支持。用户升级后，可以测试到这些新特性。
- **⚠️ 迁移注意事项**: 使用该版本需谨慎。如果 `load_image` 工具之前被默认禁用，更新后可能需要手动在 `config.json` 中配置以启用或禁用，因为 `ToolsConfig.IsToolEnabled()` 的默认行为已从“总是启用”变为“可配置的默认启用/禁用”。
- **详情**: [查看完整变更日志](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)

## 3. 项目进展

今日合并/关闭了 8 个 Issue 和 9 个 PR，主要集中在用户体验和平台兼容性的改善。

- **核心功能可配置化**: 合并了 PR #2879，修复了 `load_image` 工具无法通过 `config.json` 配置启用/禁用的 Bug。这解决了 Issue #2878 提出的痛点，提升了系统的灵活性和安全性。
- **新提供商支持**: 合并了 PR #2885（关闭 Issue #2884），正式添加了对 **SiliconFlow** 提供商的原生支持。用户无需再通过 OpenAI 兼容模式进行非标准配置，简化了使用流程。
- **用户体验优化**:
    - 合并了 PR #2886，为 Web 聊天界面增加了推理过程（reasoning）和工具调用（tool call）的可见性选择器，用户可以更清晰地追踪 AI 的思考过程。
    - 合并了 PR #2882，为代码块添加了独立的复制和折叠控件，并在工具调用参数区域实现了 JSON 高亮显示，提升了阅读和交互体验。
- **安全性与平台修复**:
    - 合并了 PR #2833，为 Web UI 和 API 添加了模型连接测试功能，用户可以在配置时即时验证连通性。
    - 合并了 PR #2836，修复了 Windows 环境下 PowerShell 的安全漏洞（`iex` 注入防护）。
- **模型配置工作流**: 合并了 PR #2752（作为系列改进的一部分），优化了模型配置工作流，包括自动拉取模型列表、提供商感知的校验等功能。

## 4. 社区热点

- **Issue #28: “Feat Request: LM Studio Easy Connect”**
    - **热度**：⭐️⭐️⭐️⭐️⭐️ (评论: 19，👍: 2)
    - **分析**：这是社区对易用性强烈渴望的典型代表。用户强烈希望简化与本地推理框架 LM Studio 的连接流程，反映出许多开发者希望将 PicoClaw 与本地模型结合使用，以降低使用门槛和成本。此请求虽提出已久，但持续获得关注，是社区呼声极高的功能。

- **Issue #2887: “[BUG] .deb version on RISC-V is not functional with OpenAI model”**
    - **热度**：⭐️⭐️⭐️ (新开，评论: 2)
    - **分析**：该项目标为“新建”，但触及了关键的架构兼容性问题。RISC-V 是新兴的指令集架构，用户尝试在 Debian RISC-V 系统上运行 .deb 包并连接 OpenAI 时遭遇失败。这表明项目在 RISC-V 平台上的兼容性测试有待加强，也反映出社区技术生态的多样性。

- **Issue #1042: “[BUG] exec工具的guardCommand方法问题”**
    - **热度**：⭐️⭐️⭐️⭐️ (长期问题，评论: 12，👍: 2)
    - **分析**：这是一个关于 `exec` 工具路径安全检查的 Bug，属于高影响力问题。当使用 `restrict_to_workspace` 时，即使是 `curl wttr.in/Beijing` 这样的无害命令也会被误判为路径穿越而拦截。此问题积压已久但未解决，可能影响大量依赖 `exec` 工具执行命令的场景，社区关注度高。

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 | Fix PR |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | [#2887](https://github.com/sipeed/picoclaw/issues/2887) | **RISC-V .deb 包无法与 OpenAI 模型配合使用**。影响新架构上的基础功能，需紧急排查。 | 开放 | 无 |
| **高** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | `exec` 工具的路径安全保护 (`guardCommand`) 过于简单粗暴，存在误杀合法命令的回归。影响范围大。 | 开放 | 无 |
| **中** | [#2839](https://github.com/sipeed/picoclaw/issues/2839) | Steering-chain 输入后，最终回复被错误地编入前一个提示 (`Working...`) 中，导致对话上下文混乱。 | 开放 | 无 |
| **低** | [#2745](https://github.com/sipeed/picoclaw/issues/2745) | OpenRouter 的推理模型会将思考过程泄露到最终回复中，影响对话的整洁性。 | 已关闭 | 已标记关闭，但未在日报PR中找到明确修复，可能是重复或已解决。 |

## 6. 功能请求与路线图信号

- **高优先级候选**:
    - **SiliconFlow 原生支持** (Issue #2884 / PR #2885): 已合并，将出现在下一版本中。
    - **“恢复出厂设置”** (PR #2891): 提供配置损坏时的恢复路径，这是一个重要的运维安全特性，很可能被纳入下个稳定版。
- **中等优先级候选**:
    - **流式（Streaming）输出** (PR #2892, #2853): 多个 PR 致力于为不同通道（如 pico 通道）添加流式传输支持。这是提升用户体验的重要功能，其代码实现活跃，表明开发团队正在积极推进。
    - **Server酱³ Bot通道支持** (PR #2893): 为中国用户常用的Server酱服务提供通道支持，表明项目正在扩展其渠道生态。
- **长期诉求 (待确认)**:
    - **LM Studio Easy Connect** (Issue #28): 呼声极高但开发复杂度待评估。

## 7. 用户反馈摘要

- **痛点**:
    - **配置困难**: 用户 `coolyu0916` 在 Issue #2878 中直接指出 `load_image` 工具无法通过配置开关，这是对系统不够灵活的直接抱怨。
    - **无形成本**: 用户 `myourscom` 在 Issue #2884 中表示，使用 OpenAI 兼容模式连接 SiliconFlow“很不方便”（inconvenient to configure），这代表了用户为支持新平台所付出的无形成本。
    - **功能缺失**: 用户 `Franzferdinan51` 在 Issue #28 中坦诚自己技术能力有限，希望有人能开发“LM Studio Easy Connect”，体现了普通用户与高级用户之间的门槛。
- **使用场景**:
    - **本地与云端混合**: 既有用户使用 Ollama Cloud (Issue #2225)，也有用户尝试本地 LLM (LM Studio, Issue #28)，还有用户使用 OpenRouter 等云端路由 (Issue #2745)，表明用户场景非常多元化。
    - **多平台与多架构**: 用户尝试在 RISC-V 架构 (Issue #2887) 和 Windows 系统 (PR #2836) 上使用，展现了 PicoClaw 作为个人 AI 助手的广泛适用潜力。

## 8. 待处理积压

以下指经过一段时间后仍然开放且未得到维护者充分响应的 Issue 或 PR，可能影响社区参与度。

- **Issue #1042: `exec`工具的`guardCommand`方法问题**：这是一个开放约 2 个半月的严重 Bug，评论活跃（12条），但尚无明确的进展。长时间悬而未决可能削弱用户对 `exec` 工具的安全信心。
- **PR #2239: modify docker compose with privileged**：这个 PR 已经开放超过 1.5 个月，且被打上 `stale` 标签。如果这个改动是合理的，建议维护者尽快 review 并合并或拒绝，避免 PR 无限期堆积。
- **PR #2788: feat(session): add per-message created_at timestamps**：开放近 2 周，标签为 `stale`。该功能看似简单但实用，能为前端渲染和时间线管理提供基础数据。拖延处理可能会让贡献者的积极性受挫。

> 建议：项目维护者可优先关注这些积压的 Issue/PR，给予明确回复（如“已排期”、“需要更多信息”、“暂时不考虑”等），以维持社区的健康活力。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-05-18

---

## 1. 今日速览

项目过去24小时保持活跃：共处理 **8 条 Issue**（新开/活跃 7，关闭 1）和 **29 条 Pull Request**（待合并 22，已合并/关闭 7）。没有新版本发布，但代码库上有多项修复和功能 PR 在同时推进。核心团队正在集中解决数据库外键约束、容器配置丢失等高频 Bug，同时社区贡献者也在提交新技能（如 Veo 视频生成、CalDAV 工具）。待合并 PR 数量较多（22 条），审查积压是当前项目健康度的主要瓶颈。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

过去24小时有 **4 条 PR 被合并/关闭**，集中在会话管理、CI 工具链和文档警告：

- **[PR #867]** `fix: allow scheduled-task agents to send_message to their task output JID`  
  修复了调度任务容器无法向共享频道发送消息的问题（已关闭，实际合并时间较早但状态今日更新）。
- **[PR #2375]** `fix(sessions): exclude per-thread sessions from agent-shared lookup`  
  解决了 GitHub PR 会话活跃时，Signal/Telegram 消息被错误路由到 PR 线程的问题（已关闭）。
- **[PR #1874]** `chore: add pre-commit hooks (prettier, eslint, typecheck, vitest)`  
  为项目引入提交前代码检查和测试钩子，提升代码质量（已关闭）。
- **[PR #2376]** `docs(manage-channels): warn against agent-shared with per-thread channels`  
  在文档中增加警告，提醒用户不要在同一个 agent group 上同时使用 `agent-shared` 和 `per-thread` 频道（已关闭）。

此外，多个关键修复 PR 已处于待合并状态（见下文 Bug 部分），整体项目在 **会话隔离、数据库事务完整性、频道适配器** 等核心模块持续完善。

---

## 4. 社区热点

- **Issue #1984** [OPEN] *Provider support for custom/local OpenAI-compat endpoints (Codex + OpenCode)*  
  [链接](nanocoai/nanoclaw Issue #1984)  
  创建于 2026-04-24，今日仍有更新，共 6 条评论，是当前评论最多的 Issue。用户期待 NanoClaw 能正式支持自建 OpenAI 兼容端点（如本地推理、私有部署），目前的实验性路径在实际路由时无法正常工作。该诉求涉及两个主流 Provider（Codex 和 OpenCode），反映了社区对模型私有化部署的强烈需求。

- **PR #2532** [OPEN] *feat: Edna video generation and stitching via Veo 3.1*  
  [链接](nanocoai/nanoclaw PR #2532)  
  今日新开的重量级功能 PR，由社区贡献者实现 Google Veo 3.1 视频生成、扩展和拼接，并集成到 Edna 工作流 + Slack 交付。虽然评论数尚未积累，但从动效看很可能成为下一个迭代的热点功能。

---

## 5. Bug 与稳定性

按严重程度排列（均附链接）：

| 优先级 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| **High** | [#2525](nanocoai/nanoclaw Issue #2525) | `ncl groups delete` 因缺少级联删除，在非空 group 上触发 `FOREIGN KEY constraint failed` | 已有 fix PR [#2526](nanocoai/nanoclaw PR #2526) 待合并 |
| **High** | [#2535](nanocoai/nanoclaw Issue #2535) | WhatsApp 群组消息加密失同步，机器人看到“Waiting for this message”无法处理 | 新开，无 fix |
| **Medium** | [#2528](nanocoai/nanoclaw Issue #2528) | Signal 频道发送的图片/PDF 附件在 agent 容器内无法访问 | 新开，无 fix |
| **Medium** | [#2415](nanocoai/nanoclaw Issue #2415) | `ncl groups create` 未插入 `container_configs` 行，首次 spawn 失败 | 已有 fix PR？状态待查 |
| **Low** | [#2522](nanocoai/nanoclaw Issue #2522) | `transformOutboundText` 在 `ask_question` 和 `card` 路径被跳过，导致 Telegram 卡片格式损坏 | 无 fix |
| — | [#2533](nanocoai/nanoclaw Issue #2533) | 部署重启后 `sessions.container_status` 残留 `running` 状态（已关闭） | 已通过某种方式修复 |

其中 **#2525** 影响所有非空 group 的删除操作，修复 PR [#2526](nanocoai/nanoclaw PR #2526) 已提交（添加了级联删除），建议尽快合并。**#2535** 涉及 WhatsApp 底层加密协议，需要深入 debug，目前无对应 fix。

---

## 6. 功能请求与路线图信号

多个功能 PR 正等待审查和合并，可能成为下一版本（v2.0.65 或 v2.1）的候选：

- **#1968** [OPEN] *End-to-end per-agent provider and model configuration*  
  [链接](nanocoai/nanoclaw PR #1968)  
  实现每个 Agent 独立选择 LLM 提供商和模型，支持聊天驱动配置。创建于 4 月 24 日，至今已迭代多个 commit，是社区呼声最高的功能之一。
- **#2301** [OPEN] *feat(add-github): polling mode, git access question, safe OneCLI secret merge*  
  [链接](nanocoai/nanoclaw PR #2301)  
  为 GitHub 集成增加无端口轮询模式（适合 NAT/防火墙环境），并提供安全凭据合并。
- **#2317** [OPEN] *feat(skills): add /add-voice-transcription-free-whisper skill*  
  [链接](nanocoai/nanoclaw PR #2317)  
  免费本地方案（Whisper / whisper.cpp）的语音转录技能。
- **#2532** [OPEN] *feat: Edna video generation and stitching via Veo 3.1*  
  [链接](nanocoai/nanoclaw PR #2532)  
  Google Veo 3.1 视频生成技能（见社区热点）。
- **#2530** [OPEN] *[PR: Skill] feat(skill): add /add-caldav-tool*  
  [链接](nanocoai/nanoclaw PR #2530)  
  CalDAV 日历工具技能。
- **#2089** [OPEN] *feat(telegram): implement setReaction for status-tracker compatibility*  
  [链接](nanocoai/nanoclaw PR #2089)  
  Telegram 频道适配 `setReaction` 方法，支持状态跟踪器兼容。
- **#2345** [OPEN] *feat(claude-md-compose): auto-import per-group CLAUDE.role.md*  
  [链接](nanocoai/nanoclaw PR #2345)  
  自动加载每个 group 的 `CLAUDE.role.md` 角色文件。

综合来看，**私有化部署（自定义端点 #1984）** 和 **多模态生成（视频 #2532、语音 #2317）** 是当前路线图上的两个最强信号。

---

## 7. 用户反馈摘要

从 Issues 评论和描述中提炼的真实痛点：

- **“自建端点无法使用”**（#1984）：多位用户反馈 NanoClaw 文档中声称支持自定义 OpenAI 兼容端点，但实际路由到私有服务器时失败。社区希望将其从“实验性”升级为正式功能。
- **“删除 group 永远报外键错误”**（#2525）：用户 glifocat 指出任何使用过的 group 都无法通过 CLI 删除，必须手动执行多条 SQL 语句才能清理，严重影响操作体验。
- **“group create 后容器无法启动”**（#2415）：同样由 glifocat 报告，`ncl groups create` 只插入 group 主记录而遗漏了 `container_configs`，导致第一次 spawn 时直接崩溃。
- **“WhatsApp 群组消息不可见”**（#2535）：用户 nikki-assistant 在添加机器人到 WhatsApp 群组后，所有成员消息均显示“Waiting for this message”，机器人无法参与群聊交互。
- **“Signal 附件容器内不可达”**（#2528）：用户 brentkearney 发现图片/PDF 文件存储在宿主机但容器内 agent 无权限访问，导致文件类任务完全不可用。
- **“UUID 不符合 OneCLI 规则”**（#2386）：`ncl groups create` 生成的 UUID 以数字开头，被 OneCLI 拒绝，用户 alexli-77 认为应更换为字母开头的标识符。

这些反馈集中反映了 **数据库操作不完整、频道附件路由缺陷、标识符兼容性** 等基础模块的稳定性问题，用户在期待更严谨的 CRUD 实现和跨平台兼容性。

---

## 8. 待处理积压

以下为创建时间较早但仍未合并或未解决的 Issue/PR，提醒维护者关注：

- **Issue #1984** (2026-04-24) «Provider support for custom/local OpenAI-compat endpoints» — 讨论持续近一个月，尚无实质修复/设计文档。
- **PR #1968** (2026-04-24) «End-to-end per-agent provider and model configuration» — 大功能 PR，至今未合并，可能需要对齐代码风格或测试。
- **Issue #2386** (2026-05-10) «UUID violates OneCLI agent identifier rules» — 影响 `groups create` 命令与 OneCLI 的兼容性，简单修复但未推进。
- **Issue #2415** (2026-05-11) «ncl groups create skips container_configs row» — 中等严重性，已有一段时间无活动。
- **PR #2082** (2026-04-28) «v2 docs: clarify upstream developer references» — 文档类 PR，未收到 review。
- **PR #2184** (2026-05-02) «fix(poll-loop): retry immediately on stale session» — 影响所有使用轮询模式的频道，待合并时间较长。

建议项目维护者优先处理 **#2525 / #2526**（High Prio 修复）和 **#1968 / #1984**（社区高关注度功能），以缓解用户痛点和审查积压。

---

*数据来源：GitHub NanoClaw 仓库 (github.com/qwibitai/nanoclaw)*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现在根据 NullClaw 项目在 2026-05-18 的 GitHub 数据，为您生成今日动态日报。

---

## NullClaw 项目日报 | 2026-05-18

**数据来源:** github.com/nullclaw/nullclaw  
**分析师:** AI 开源项目分析师

### 1. 今日速览

项目今日整体处于低活跃度状态，过去24小时内无新Pull Request提交或合并，也无新版本发布。社区讨论主要聚焦于两个新提交的Issue，分别涉及核心功能“调度器”的故障报告和“自动记忆回拉”功能的可配置性需求。尽管代码提交层面平静，但社区提出的问题指向了项目在稳定性与灵活性方面的关键痛点，值得维护团队关注。整体活跃度评级：**低** (待合并PR: 0，新版本: 0，新增活跃讨论: 2)。

### 2. 版本发布

**无**。过去24小时内无新版本发布。

### 3. 项目进展

**无明显进展**。过去24小时内无Pull Request被合并或关闭。代码库在功能推进和Bug修复方面处于沉默状态。

### 4. 社区热点

**唯一活跃议题:**
- **[Bug] Problem with scheduler unauthorized (Issue #915)**  
  链接: https://github.com/nullclaw/nullclaw/issues/915  
  这是过去24小时内最受关注的议题，也是目前唯一的活跃讨论。该Issue报告了调度器在Telegram聊天及控制台中均无法工作的问题。虽然仅有一条评论，但该问题直接关联到项目计划任务执行的核心功能，属于高优先级议题。背后的核心诉求是：**当项目依赖外部LLM服务（如Ollama）时，调度功能在跨网络、跨环境下的稳定性与授权机制需要得到验证和修复。**

### 5. Bug 与稳定性

根据严重程度排列：

1.  **[严重] 调度器未经授权故障 (Issue #915)**
    - **状态**: 未修复
    - **链接**: https://github.com/nullclaw/nullclaw/issues/915
    - **描述**: 用户在Ubuntu环境下运行NullClaw，连接同一网络的外部Ollama主机（RTX 3090）。LLM和通用工具调用正常，但调度器功能完全失效（包括在Telegram和CLI中）。用户未提供明确错误日志，但“unauthorized”字样暗示可能存在权限或会话认证问题。目前**无修复PR**。

2.  **[功能相关] 自动记忆回拉不可配置 (Issue #919)**
    - **状态**: 功能请求，非直接Bug
    - **链接**: https://github.com/nullclaw/nullclaw/issues/919
    - **描述**: 用户指出 `enrichMessageWithRuntime()` 函数对每条消息强制进行FTS5+BM25记忆召回，且参数（召回数量、上下文大小等）全部硬编码。虽然不属于运行时崩溃，但严格的默认行为可能会导致对小上下文或无上下文的任务产生不必要的开销，影响性能与隐私。**无修复PR**。

### 6. 功能请求与路线图信号

- **提出功能**: 允许按消息粒度禁用自动记忆回拉 (Issue #919)  
  **链接**: https://github.com/nullclaw/nullclaw/issues/919  
  **信号分析**: 这是一个强烈的信号，表明部分高级用户或特定场景（如简单查询、指令遵循类任务）用户，希望对项目的**默认增强行为**有更精细的控制权。该功能与“灵活的记忆策略”以及“性能和资源优化”相关。结合项目特性，如果被采纳，可能会作为新的配置项（如环境变量或每条消息的元数据字段）加入下一版本，具备较高采纳可能性。

### 7. 用户反馈摘要

从今日的两个Issue评论中，可以提炼出以下用户反馈：

- **痛点（来自 #915）**: 用户对“调度器”这一核心自动化功能的失效感到困扰。问题描述清晰但缺乏关键错误日志。评论中项目维护者已要求提供日志，这表明**用户对问题诊断的配合度不高或不清晰**，同时也反映出项目在启动时需要更强的错误提示和诊断信息产出功能。
- **满意/不满意（来自 #919）**: 用户对项目的FTS5记忆功能本身是认可的，但对**强制执行的硬编码行为**感到不满。用户希望项目赋予其“关闭或减少开销”的权利，属于对高级功能的控制力诉求。

### 8. 待处理积压

- **积压议题**: **[Bug] Problem with scheduler unauthorized (Issue #915)**  
  **链接**: https://github.com/nullclaw/nullclaw/issues/915  
  **创建于**: 2026-05-15  
  **最新更新**: 2026-05-17  
  **建议**: 该议题处于“等待日志”状态已超过24小时。若用户长时间不提供日志，建议维护者主动复现或尝试通过代码审查定位问题（例如检查最新代码对调度器认证模块的改动）。考虑到调度器的核心地位，此Issue应尽快推进，否则会影响新用户信任度。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，以下是基于您提供的 IronClaw 项目数据生成的 2026-05-18 项目动态日报。

---

# IronClaw 项目动态日报 | 2026-05-18

## 今日速览

今日项目状态为 **密集开发**，活跃度 **高**。核心开发团队正全力推进 “Reborn” 重大架构重构，今日合并/关闭的8个 PR 中，有多个直接服务于 Reborn 的 WebUI 层、策略层和产品工作流。社区贡献持续活跃，共提交了 34 个待合入的 PR。同时，v0.28.2 版本被发现两处回归问题，已由贡献者提交修复 PR。整体上，项目在主功能开发和稳定性维护上呈现双线并行的健康态势。

## 版本发布

无

## 项目进展

今日合并/关闭了 8 个 PR，其中包含多项关键进展，主要集中在 Reborn 架构的落地和基础设施重构。

- **Reborn 产品工作流推进**：
    - **[PR #3735]** 合入 `feat(product_workflow): expose get_run_state on RebornServicesApi facade`。该 PR 为 M2 工作流增加了第四个 facade 方法，使 WebUI 路由能够直接获取运行状态，无需直接引入 `TurnCoordinator` 等底层组件。
    - **[PR #3744]** 合入 `refactor(registry): address product adapter review follow-ups`。对产品适配器进行了审查后的代码清理和文档工作，提升了代码健壮性。
    - **[PR #3632]** 合入了 Reborn 的 `BeforeInboundPolicy` 策略层，这是一个重要的里程碑，为未来在 WebUI/WebChat 中实现消息检查、重写或拒绝提供了标准接口。

- **关键基础设施与工具链优化**：
    - **[PR #2506]** 合入 `feat(orchestrator): ORCHESTRATOR_HOST env var for worker callback address`。该PR修复了在Linux (非Docker Desktop)环境下，编排器内 Worker 容器回调地址硬编码的问题，提升了多平台部署兼容性。
    - **[PR #2418]** 合入 `feat: slim mode runtime, Dockerfiles, and /health route`。该大型 PR 引入了轻量级运行模式，并提供了相应的 Dockerfile 和健康检查端点，旨在降低多租户高密度部署场景下的单实例资源占用。
    - **[PR #3681]** 合入 `feat:[extensions] Add first-party HTTP egress tool`。为 Reborn 增加了一个内置的 HTTP 出站工具 `builtin.http`，增强了 Reborn 的扩展能力。

- **长期挂起的重大 PR 被接纳**：
    - `feat(slack): fetch thread history when bot is mentioned in any thread` (PR #2066, #2457) 等长期开放的 PR 今日被标记为合并/关闭，表明项目维护者正在清理长期积压的社区贡献。

## 社区热点

今日讨论最活跃的议题体现了社区对 **Reborn 架构进展** 和 **用户体验（UX）问题** 的高度关注。

1. **[Issue #3692: Reborn: add policy-gated personal identity and heartbeat prompt context]**
   - **舆情看点**：该 Issue 由核心开发者 `henrypark133` 创建，是 Reborn “个人身份与心跳提示上下文” 工作的一部分，目前有 **5 条评论**。讨论焦点在于如何将用户身份策略融入到上下文管理中，是 Reborn 迈向更个性化智能体的关键议题。社区（主要是核心团队）正在深入探讨技术实现方案。

2. **[Issue #3259: Publish 0.25.0–0.27.0 to crates.io]**
   - **舆情看点**：这是一个来自社区的长期呼声，今日仍有更新。**5 条评论** 反映了依赖 `ironclaw` 库的下游项目因 crates.io 版本滞后而无法获取最新功能和关键修复（如 wasmtime CVE）。该 Issue 虽非技术讨论，但直接关系到项目的生态健康和社区信任。

3. **[Issue #3729: [bug] Failed `tool_install` calls are shown as successful after page refresh]**
   - **舆情看点**：这是一个明显的 UI/UX Bug，可能导致用户对操作结果产生误判。虽只有 **1 条评论**，但问题描述清晰，复现步骤明确，属于高优先级需要修复的线上缺陷。用户 `sunglow666` 活跃在 QA 一线，连续报告了多个 Bug。

## Bug 与稳定性

今日共报告 5 个 Bug/回归问题，其中 **2 个** 已被判定为 v0.28.2 的回归。维护者响应迅速，部分已有修复 PR。

1. **[高] [Issue #3734: v0.28.2 regression: provider config missing API Key and Fetch available models controls]**
   - **描述**：在非 TEE 环境下的 v0.28.2 版本中，代理的推理 API 提供商配置界面缺少了“API Key”输入框和“Fetch available models”按钮，而在 v0.28.1 版本中正常。
   - **状态**：已提交 **修复 PR #3742**，定位为 PR #3416 重构引入的回归问题。
   - **链接**: [Issue #3734](https://github.com/nearai/ironclaw/issues/3734) | [PR #3742](https://github.com/nearai/ironclaw/pull/3742)

2. **[高] [Issue #3729: Failed `tool_install` calls are shown as successful after page refresh]**
   - **描述**：用户拒绝 `tool_install` 调用后，页面显示失败（红色 ❌）。但刷新页面后，失败的操作被错误地显示为成功（绿色 ✅）。
   - **状态**：已有社区贡献者介入，但尚未有确定的修复方案。
   - **链接**: [Issue #3729](https://github.com/nearai/ironclaw/issues/3729)

3. **[中] [Issue #3736: v0.28.2 regression: unconfigured providers still show Use button in TEE agents]**
   - **描述**：在 TEE 版本的生产代理中，未配置 API Key 的提供商仍在推理设置中显示“Use”按钮，可能误导用户。
   - **状态**：已标记为问题，仍在讨论中。
   - **链接**: [Issue #3736](https://github.com/nearai/ironclaw/issues/3736)

4. **[低] [Issue #3743: Settings Telegram pairing approval shows duplicate success toasts]**
   - **描述**：Telegram 频道配对成功后，UI 中会弹出两个重复的成功提示。
   - **状态**：新报告，尚未有回应。
   - **链接**: [Issue #3743](https://github.com/nearai/ironclaw/issues/3743)

5. **[低] [Issue #3733: Invalid Gmail token shows success/activated toast]**
   - **描述**：输入无效的 Gmail OAuth Token 后，系统错误地显示配置成功并激活了 Gmail 工具，随后立即再次弹窗要求认证。
   - **状态**：新报告，尚未有回应。
   - **链接**: [Issue #3733](https://github.com/nearai/ironclaw/issues/3733)

## 功能请求与路线图信号

今日提交的功能请求主要集中在 **Reborn 架构的完善** 和 **测试覆盖** 上。

- **Reborn 核心功能**：`#3696` 和 `PR #3717` 要求将 Reborn 的“运行计划配置文件解析器”接入生产环境组合工厂，这是 Reborn 从开发测试走向生产部署的关键一步。`PR #3720` 和 `PR #3722` 则分别关注了支持长期运行任务的“工具结果引用”（Taskable tool result refs）。这些信号表明 Reborn 架构正在快速向“生产就绪”目标迈进。

- **测试与验证**：`#3702`、`PR #3730` 和 `PR #3741` 都在推动为 Reborn 建立更全面的端到端 (E2E) 和单元测试框架。这不仅是质量控制，也表明项目团队有信心为该重大重构建立完整的测试保护网。

- **潜在纳入下一版本的功能**：
    - **HTTP 出站工具** (`PR #3681`) 已合并，是 Reborn 能力集的重要补充。
    - **模块化重构**：`PR #3739` 提出的提取 `ironclaw_embeddings` crate，以及 `PR #3679` 提出的统一文件系统调度，都是架构模块化、解耦的重要步骤，可能会在后续版本中持续演进。

## 用户反馈摘要

从 Issue 和 PR 评论中，提炼出以下用户反馈与痛点：

- **对版本更新与兼容性的高要求**：`#3734` 和 `#3729` 报告的回归问题都出现在小版本 v0.28.2，表明用户对功能稳定性敏感，任何 UI/UX 的退步都会被快速发现并报告。
- **TEE 环境的特殊性**：`#3736` 提及的问题专门发生在 TEE 环境，说明 TEE 版本有独立的配置和体验问题，需要维护者投入专项关注。这是企业级用户非常看重的场景。
- **UI 体验细节**：`#3743`（重复 Toast）和 `#3733`（无效 Token 却显示成功）这类 Bug 虽小，但直接影响了用户的认知和操作满意度。社区用户 `sunglow666` 频繁报告此类边缘案例，是项目提升用户满意度的重要信息源。
- **对 Reborn 新功能的期待与测试**：从 `#3622`、`#3620` 等 Reborn 相关 Issue 的互动来看，核心贡献者对 Reborn 的内部机制（如工具调用回传、结果引用）讨论热烈，表明团队正朝着更复杂的自动化工作流方向深度探索。

## 待处理积压

以下为过去一周内尚未收到维护者响应的重要 Issue 或 PR，建议优先关注：

1. **[Issue #3447: Nightly E2E failed]**
   - **简述**：自 2026-05-10 起，Nightly E2E 测试持续失败，最新失败为 2026-05-18。
   - **链接**: [Issue #3447](https://github.com/nearai/ironclaw/issues/3447)
   - *建议：这是关键的质量门禁，持续失败将导致无法发现新的退化，需立即指定负责人排查。*

2. **[Issue #3259: Publish 0.25.0–0.27.0 to crates.io]**
   - **简述**：发布版本严重滞后的社区呼声，至今仍无官方回应。
   - **链接**: [Issue #3259](https://github.com/nearai/ironclaw/issues/3259)
   - *建议：这是一个关键的生态问题，长期未回复可能影响下游合作伙伴的信心。*

3. **[Issue #3622 & #3620: Reborn: verify/convert provider tool calls]**
   - **简述**：这两项是 Reborn 工具调用循环的核心任务，已开放数日且讨论热度高。
   - **链接**: [Issue #3622](https://github.com/nearai/ironclaw/issues/3622) | [Issue #3620](https://github.com/nearai/ironclaw/issues/3620)
   - *建议：考虑到它们是生产工作流（M2/M3 模块）的前置依赖，建议加速推进 PR 进度。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 项目的分析师，根据您提供的 2026-05-18 GitHub 数据，我为您生成以下项目动态日报。

---

### LobsterAI 项目日报 (2026-05-18)

**数据快照**: 过去24小时，项目在PR合并方面非常活跃，共处理了17条PR（12条已合并/关闭），未收到新的Issue报告，也无新版本发布。

---

#### 1. 今日速览

今日 LobsterAI 项目处于 **高活跃度的整合期**。尽管社区没有提出新的问题，但开发团队集中合并了大量代码，成功推进了一个涵盖多项核心功能的 Release 分支（`release/2026.5.18`）。这包括**支持按模型独立配置上下文窗口**的重要新功能，以及针对 OpenClaw 组件的**中文字符兼容性修复**。同时，多个界面重构任务被合并，表明项目在积极优化代码结构的同时，也关注用户体验的打磨。

---

#### 2. 版本发布
无新版本发布。但今日合并的 Release 分支 `release/2026.5.18`（见下方 `#2010`）暗示未来几日内可能会有正式的版本发布。

---

#### 3. 项目进展

今日合并/关闭的 12 条 PR 标志着项目在其核心功能与协作能力上迈出了一大步。主要进展如下：

- **核心功能里程碑**: **合并了 Release 分支 `release/2026.5.18`**。
  > `fisherdaddy` 的 PR #2010 整合了本周期内的所有新功能、重构和修复，是今日工作的集大成者。这通常标志着开发周期的结束和发布周期的开始。
  > [PR #2010](https://github.com/netease-youdao/LobsterAI/pull/2010)

- **新功能落地**:
  - **模型上下文窗口可配置**: `btc69m979y-dotcom` 的 PR #2001 正式合入，用户现在可以为每个独立的模型设置上下文窗口大小，上限提升至 2M tokens，极大提升了模型配置的灵活性。
  > [PR #2001](https://github.com/netease-youdao/LobsterAI/pull/2001)

- **关键Bug修复**:
  - **修复非ASCII字符兼容性**: `btc69m979y-dotcom` 的 PR #2006 解决了 OpenClaw 组件因不支持中文字符导致 MCP 服务器名称无法识别的问题，这是国际化支持的重要一步。
  > [PR #2006](https://github.com/netease-youdao/LobsterAI/pull/2006)
  - **修复UI回归**: `btc69m979y-dotcom` 的 PR #2007 修复了“新建任务”页面背景色被误改的问题，确保了UI主题的一致性。
  > [PR #2007](https://github.com/netease-youdao/LobsterAI/pull/2007)
  - **修复Markdown预览**: `liugang519` 的 PR #2002 解决了 Markdown 文件预览时，本地图片等资源路径无法正确解析的问题。
  > [PR #2002](https://github.com/netease-youdao/LobsterAI/pull/2002)

- **代码质量与重构**:
  - `btc69m979y-dotcom` 通过 PR #2004 将庞大的 `Settings.tsx` 中的模型设置部分拆分为独立组件，大幅提升了代码可维护性。
  > [PR #2004](https://github.com/netease-youdao/LobsterAI/pull/2004)
  - PR #2005 统一了 UI 组件样式，将“梦境”功能的开关替换为标准滑动开关。
  > [PR #2005](https://github.com/netease-youdao/LobsterAI/pull/2005)

- **自动化与依赖更新**:
  - PR #2003 和 #2008 分别进行了插件升级和图标更新，体现了项目对基础组件的持续维护。
  > [PR #2003](https://github.com/netease-youdao/LobsterAI/pull/2003) | [PR #2008](https://github.com/netease-youdao/LobsterAI/pull/2008)

---

#### 4. 社区热点

今日社区讨论较为平静，没有出现评论数异常高的 Issue 或 PR。主要工作集中在开发团队的代码提交上。未关闭的多个“陈旧”PR（如 `#748`, `#749`, `#755`）自上次更新以来（3月24日）至今没有新的互动，表明社区对这些功能存在潜在需求，但缺乏进一步的推动和讨论。

> **洞察**: 合并的 `Release/2026.5.18` 分支是今日最大的“热点”，它直接反映了项目近期的开发方向和重点。

---

#### 5. Bug 与稳定性

今日修复了多个Bug，按严重程度排列如下：

1. **严重 - 功能兼容性Bug**:
   - **问题**: OpenClaw 组件对非ASCII字符(MCP服务器名称)处理不当，导致中文字符被识别为无效字符。
   - **修复**: 已通过 PR #2006 合并修复，通过 MD5 哈希生成了稳定的 ASCII 别名。
   > [PR #2006](https://github.com/netease-youdao/LobsterAI/pull/2006)

2. **中等 - UI回归Bug**:
   - **问题**: 设置页面的“新建任务”页面背景色被错误地改为白色。
   - **修复**: 已通过 PR #2007 合并修复，恢复为正确的主题色。
   > [PR #2007](https://github.com/netease-youdao/LobsterAI/pull/2007)

3. **中等 - 功能Bug**:
   - **问题**: Markdown 预览功能无法正确解析和显示本地的相对路径图片。
   - **修复**: 已通过 PR #2002 合并修复，将本地路径映射为 `localfile://`。
   > [PR #2002](https://github.com/netease-youdao/LobsterAI/pull/2002)

---

#### 6. 功能请求与路线图信号

- **已确认纳入路线图的功能**: PR #2001 实现了“按模型独立配置上下文窗口”功能，这不仅是一个新功能，也反映了社区对模型精细化控制的需求。该功能已合入 `release/2026.5.18`，几乎确定会出现在下个版本中。
  > [PR #2001](https://github.com/netease-youdao/LobsterAI/pull/2001)

- **可能被纳入下一版本的潜在功能**: 仍处于开放状态的 PR #755 (导出聊天记录) 需求明确且实用。虽然其状态已“陈旧”，但其功能价值很高，很可能会在未来的某个开发周期中被重新评估并整合。
  > [PR #755](https://github.com/netease-youdao/LobsterAI/pull/755)

---

#### 7. 用户反馈摘要

从今天关闭的 PR 修订内容中，我们可以间接提炼出用户痛点：

- **“[Revert] 新任务页面背景色是白色的，和对话页面的暖色调不一致”**：通过 PR #2007 的修复，可以推断用户对 UI 主题的一致性有要求，任何突然的颜色变化都会造成不好的使用体验。
- **“[OpenClaw] 输入中文MCP服务器名称后，功能无法工作”**：PR #2006 的修复明确指出中文名被替换成“------”，这说明有核心用户在使用非英语环境（中文）的 MCP 功能，这是一个非常具体的国际化反馈。
- **“我设置了很大的上下文窗口，但每个模型似乎不生效”**：PR #2001 的推出，正是为了响应用户希望按模型（而非全局）单独设置上下文窗口的需求。

---

#### 8. 待处理积压

以下是从 2026年3月24日 起就处于“开放”状态的 PR，期间无新的实质性评论或更新，但开发者在今日对其进行了同步更新。这些 PR 涉及到 IM 平台配置重构、渲染性能优化、会话压缩、聊天记录导出等对项目长期健康至关重要的能力，值得维护者重新审视优先级。

- **PR #748**: `refactor(im): extract platform config handlers` (重构IM配置)
  > [PR #748](https://github.com/netease-youdao/LobsterAI/pull/748)
- **PR #749**: `perf(cowork): memoize ToolCallGroup...` (Cowork性能优化)
  > [PR #749](https://github.com/netease-youdao/LobsterAI/pull/749)
- **PR #752**: `Feat/compact` (聊天记录压缩)
  > [PR #752](https://github.com/netease-youdao/LobsterAI/pull/752)
- **PR #755**: `feat: 支持将聊天记录导出为 Markdown/JSON 格式` (数据导出)
  > [PR #755](https://github.com/netease-youdao/LobsterAI/pull/755)
- **PR #760**: `fix(cowork): remove duplicate session status update` (移除冗余状态更新)
  > [PR #760](https://github.com/netease-youdao/LobsterAI/pull/760)
- **PR #811**: `perf(cowork): 使用索引表优化流式消息更新查找性能` (流式消息查找性能优化)
  > [PR #811](https://github.com/netease-youdao/LobsterAI/pull/811)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 | 2026-05-18

## 1. 今日速览

过去 24 小时项目保持高活跃度，共处理 **6 个 Issue**（1 个新功能提议，5 个已关闭）和 **8 个 PR**（6 个已合并/关闭，2 个开放中）。核心稳定性修复集中到位：此前在四月重构中丢失的 `BeforeAgentStart` 和 `BeforeLLMCall` 钩子已恢复；Gemma‑4 推理标签误渲染为普通文本的问题得到修复；危险命令扫描的误报（heredoc 体）以及 TTS 配置被自动压缩的缺陷均已解决。新版本 `20260517.03` 已发布，项目整体向更健壮的代理路由与记忆管理方向迈进。

## 2. 版本发布

- **`20260517.03`** — 发布日志暂无明细，但根据今日合并的 PR 可确认该版本包含以下修复：
  - 修复 Gemma/Google 模型 `<thought>` 推理标签未被识别的问题（PR #1016）
  - 修复 `BeforeAgentStart` 钩子在流式/非流式循环中未触发的问题（PR #1017）
  - 修复 `BeforeLLMCall` 钩子对消息体的修改被静默丢弃的问题（PR #1018）
  - 修复危险命令正则对 heredoc 体内容误报的问题（PR #1019）
  - 修复 `VoiceCoquiTtsConfig` 默认值在启动时被自动压缩丢失的问题（PR #1015）
  - 新增 NetBird 与 Cloudflare Tunnel 远程接入选项（PR #1008）

**破坏性变更**：无  
**迁移注意事项**：建议用户升级后检查自定义钩子逻辑是否按预期生效；若启用了危险命令扫描，注意 heredoc 体内容不再被误拦截。

## 3. 项目进展

今日合并/关闭的 **6 个 PR** 涵盖了多项关键修复与功能增强：

| PR | 标题 | 类型 | 影响模块 | 关联 Issue |
|---|---|---|---|---|
| [#1019](https://github.com/moltis-org/moltis/pull/1019) | fix(tools): ignore heredoc bodies in dangerous command scan | bugfix | 工具执行 | #1014 |
| [#1018](https://github.com/moltis-org/moltis/pull/1018) | fix(agents): honor BeforeLLMCall hook modifications | bugfix | 代理钩子系统 | #1013 |
| [#1017](https://github.com/moltis-org/moltis/pull/1017) | fix(agents): dispatch before agent start hooks | bugfix | 代理钩子系统 | #1012 |
| [#1016](https://github.com/moltis-org/moltis/pull/1016) | fix(providers): parse thought reasoning tags | bugfix | 提供商解析 | #1007 |
| [#1015](https://github.com/moltis-org/moltis/pull/1015) | fix(config): preserve explicit defaults on startup | bugfix | 配置管理 | #1006 |
| [#1008](https://github.com/moltis-org/moltis/pull/1008) | Add NetBird and Cloudflare Tunnel to onboarding | feature | 远程接入/入门指南 | – |

此外，两个开放 PR 正在推进新功能：
- [#1010](https://github.com/moltis-org/moltis/pull/1010) 支持内存文件保存至嵌套子目录（面向 QMD 集合）
- [#1009](https://github.com/moltis-org/moltis/pull/1009) 修复 `run_with_timeout` 超时后未杀死 QMD 子进程的泄漏问题

项目在代理钩子可靠性、配置稳定性、工具安全扫描、模型兼容性以及远程接入体验上均有实质性提升。

## 4. 社区热点

当日无明显超高评论的议题，但 **dmitriikeler** 用户贡献突出，独自提交了 3 个 Bug 报告（#1012、#1013、#1014）和 1 个功能请求（#1011）。所有 Bug 均在提交后数小时内被作者 **penso** 以对应 PR 修复并关闭，体现了社区极高的响应效率。  
功能请求 [#1011](https://github.com/moltis-org/moltis/issues/1011) 提出“每轮工具选择 + 活跃工具过滤”以解决小型廉价 LLM（如 Claude Haiku 4‑5）无法可靠遵循全工具列表的问题，反映了开发者在多代理路由场景中的实际痛点，可能成为下一版本路线图中的亮点。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug（所有均已关闭并有对应 PR）：

| ID | 标题 | 严重程度 | 状态 | 修复 PR |
|---|---|---|---|---|
| [#1012](https://github.com/moltis-org/moltis/issues/1012) | BeforeAgentStart hook 事件从未触发（四月重构导致） | **严重** — 核心钩子系统失效 | 已关闭 | [#1017](https://github.com/moltis-org/moltis/pull/1017) |
| [#1013](https://github.com/moltis-org/moltis/issues/1013) | BeforeLLMCall hook 的 modify 返回值被静默丢弃 | **严重** — 违反文档承诺的“可修改”能力 | 已关闭 | [#1018](https://github.com/moltis-org/moltis/pull/1018) |
| [#1014](https://github.com/moltis-org/moltis/issues/1014) | 危险命令正则对 heredoc 体内容误报（如 `rm -r` 出现在文档中） | **中等** — 影响正常 heredoc 使用 | 已关闭 | [#1019](https://github.com/moltis-org/moltis/pull/1019) |
| [#1007](https://github.com/moltis-org/moltis/issues/1007) | Gemma‑4‑31b‑it 推理标签 `<thought>` 被当作普通文本 | **中等** — 影响 Gemma/Google 模型体验 | 已关闭 | [#1016](https://github.com/moltis-org/moltis/pull/1016) |
| [#1006](https://github.com/moltis-org/moltis/issues/1006) | VoiceCoquiTtsConfig 默认值在启动时被自动压缩丢失 | **中等** — 导致配置“消失”，用户需重新设置 | 已关闭 | [#1015](https://github.com/moltis-org/moltis/pull/1015) |

所有严重及以上级别 Bug 均在当日完成修复，项目稳定性显著回升。

## 6. 功能请求与路线图信号

- **[#1011](https://github.com/moltis-org/moltis/issues/1011)** [Feature] **每轮工具选择 + 活跃工具过滤**（作者 dmitriikeler）  
  诉求：小型 LLM 无法可靠跟随完整工具列表导致“路线漂移”，希望提供每轮 `tool_choice` 控制及 `active_tools` 过滤，以在成本与准确性间取得平衡。作者已承诺可贡献实现，该功能有较大概率被纳入下一版本。

- **[#1010](https://github.com/moltis-org/moltis/pull/1010)** [PR] **内存支持嵌套子目录与集合感知写入**（作者 gmoigneu）  
  开放中 PR，扩展 `memory_save`/`memory_delete` 以支持 `memory/**`、`agents/**` 等任意用户定义集合路径，适配 QMD 后端。若合入，将极大提升知识管理灵活性。

- **[#1009](https://github.com/moltis-org/moltis/pull/1009)** [PR] **修复 `run_with_timeout` 超时后子进程泄漏**（作者 gmoigneu）  
  当前超时仅丢弃 Future，底层 QMD/Node 进程继续运行导致资源泄漏。该 PR 添加 `kill_on_drop` 逻辑，对长时间运行的任务（如知识检索）至关重要。

## 7. 用户反馈摘要

Issues 中暂无长篇讨论，但从 Bug 描述可提炼出以下用户痛点：

- **配置丢失问题**（#1006）：用户 `maop` 反映 `VoiceCoquiTtsConfig` 中显式设置的 `http://localhost:5002` 地址在每次启动后被自动压缩掉，导致 TTS 服务必须重新配置，严重影响使用流程。
- **钩子系统不可靠**（#1012、#1013）：用户 `dmitriikeler` 指出文档宣称 `BeforeAgentStart` 和 `BeforeLLMCall` 钩子具有修改能力，但实际上修改未生效或事件从未触发，导致自定义验证、日志、消息预处理等依赖钩子的工作流完全失效。
- **工具安全过度拦截**（#1014）：同一用户报告 `DANGEROUS_PATTERN_DEFS` 正则对 heredoc 体内的代码示例（如 `rm -r`）也报危险，迫使开发者在文档中规避此类示例，降低开发体验。
- **模型兼容性**（#1007）：用户 `maop` 发现 Gemma‑4‑31b‑it 的 `<thought>` 推理标签未被识别为推理块，而是作为普通文本暴露，破坏了模型的思考/输出分离期望。

上述问题均在当日得到修复，用户满意度有望提升。

## 8. 待处理积压

以下开放项暂无明显超期，但值得维护者优先审视：

| ID | 标题 | 类型 | 已开放时间 | 建议处理 |
|---|---|---|---|---|
| [#1011](https://github.com/moltis-org/moltis/issues/1011) | Per-turn tool_choice + active_tools filtering | Feature | 1 天 | 已有作者表示可贡献，可尽早分配里程碑 |
| [#1010](https://github.com/moltis-org/moltis/pull/1010) | feat(memory): allow nested subfolders and collection-aware writes | PR | 1 天 | 功能影响面较大，需 review 合并冲突或测试覆盖 |
| [#1009](https://github.com/moltis-org/moltis/pull/1009) | fix(qmd): kill child process when run_with_timeout expires | PR | 1 天 | 资源泄漏修复，建议尽快合入以避免生产环境内存/进程膨胀 |

当前无长期无人响应的议题，项目维护者响应迅速，社区健康度良好。

---

*本日报由 AI 分析师自动生成，基于 GitHub 公开数据，仅供参考。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，这是根据您提供的 CoPaw 项目数据生成的 2026-05-18 项目动态日报。

---

# CoPaw 项目动态日报 | 2026-05-18

## 1. 今日速览

今日 CoPaw 项目社区活跃度**极高**，24小时内产生 26 条 Issue 和 28 条 PR，是近期的峰值水平。Issue 中 Bug 报告与功能请求各占一定比例，反映了社区既在积极使用又在寻求创新。PR 队列增长迅速，22 条待合并，显示出大量新功能与修复等待审核，项目维护团队的合并效率或需成为关注重点。尽管没有发布新版本，但多项围绕稳定性（如 LLM 限流、连接泄漏）的修复提案已进入流程，为下一个版本奠定了坚实基础。

## 2. 版本发布

**无**

## 3. 项目进展

今日无 PR 被正式合并，但有多项关键修复和功能提案进入关闭状态或获得重大推进。

**关键修复要点（已关闭的PR）：**

*   **`providers`: 修复全局 LLM 限流器为按模型实例处理 (#4487)**。这是一个重要的 Bug 修复，旨在解决“三个点闪烁 / 聊天无响应”这一社区高频痛点，其底层原因在于全局限流器在多模型使用场景下容易误判。
*   **`fix(console/chat)`: 修复页面导航时的 SSE 连接泄漏 (#4488)**。通过升级前端聊天库，解决了切换页面后浏览器连接数占满的问题，能有效改善长对话和不间断体验的稳定性。
*   **`fix(openai_provider)`: 增加 min max_tokens 至 20 以适配模型 API 约束 (#4489)**。针对特定模型（如 `qwen3.5-omni-plus`）对 `max_tokens` 的最低要求，修正了默认值。
*   **`fix(token_usage)`: 增加按模型 Token 用量聚合 (#4476)**。增强了 Token 用量统计的精确度，为开发者提供更细粒度的成本分析。
*   **新增模型供应商** (#4479)：一位贡献者新增了 `octoken` 模型供应商支持（尽管 PR 描述存在歧义）。

**功能进展（待合并的中大型PR）：**

*   **插件分发系统 (#4482)**：为核心插件提供端到端分发机制，包括打包、CDN发布及控制台内浏览安装，这将极大提升生态建设效率。
*   **Tauri 2.x 桌面应用支持 (#3813)**：旨在将前端打包为桌面应用，标志着 CoPaw 向原生客户端迈出的重要一步，目前仍在审核中。
*   **轻量级目标模式 (#4443)**：为会话添加 `/goal` 命令，支持设定和跟踪阶段性目标，这是面向高级用户和自动化场景的重要功能。
*   **2026 世界杯技能插件 (#4407)**：提供了比赛日程、实时比分和预测等内置技能，展示了 CoPaw 技能生态的丰富性和时效性。

## 4. 社区热点

今日社区讨论热点集中在**用户体验**和**通道稳定性**上。

1.  **“聊天窗口无回应 / 三个点闪烁”讨论串**
    *   **[Issue #4469 已关闭]**: 多达 16 条评论，用户描述了在不同版本、重装 Docker 后仍无法对话的极端情况。同时有 **Issue #4453 (已关闭)** 作为相似问题的报告。这显示该问题是目前影响用户面最广的痛点，社区贡献者已在 PR #4487 中提出了解决方案。

2.  **WeChat 通道定时任务推送失败**
    *   **[Issue #4477]**: 7条评论，用户报告了微信 iLink 在企业环境中定时任务的痛点，核心问题包括 `context_token` 过期后无重试逻辑、图片/文件发送失败没有日志。这表明企业用户对 B 端通道的稳定性和可观测性有较高期待。PR #4490 正在尝试解决其崩溃问题。

3.  **模型兼容性疑问：ChatGPT-5.5 与 deepseek 解析问题**
    *   **[Issue #4474]**: 6条评论，用户尝试配置最新模型 `chatgpt-5.5` 时遇到困难，反映了社区对新模型快速接入的渴望。
    *   **[Issue #4051 已关闭]**: 8条评论，讨论了 deepseek 模型 `think` 标签解析错误导致回复为空。这些讨论体现了 LLM 迭代速度快，对底层 Provider 的兼容性提出了挑战。

## 5. Bug 与稳定性

以下为今日报告的 Bug 按严重程度排列：

*   **严重 (Critical)**:
    *   **[插件接口存在未经授权的远程代码执行 (RCE) 漏洞 (#4470)]**: 安全问题需立即关注。
    *   **[聊天窗口无回应 (#4469)]**: 已通过 PR #4487 修复限流器问题，根因已定位。
    *   **[Console 流式生成中途卡死，显示“您打断了我的回答” (#4494)]**: 影响长对话和工具调用密集型任务，暂无关联 PR。
    *   **[插件工具写入 agent.json 后未注入 Toolkit (#4485)]**: 导致功能型插件完全不可用，属于功能性瘫痪级 Bug。
    *   **[WeChat iLink 定时任务推送失败 (#4477)]**: 影响企业微信用户的核心自动化任务。

*   **中等 (Major)**:
    *   **[Context Compaction 频繁因 “无效格式 (missing ## header)” 失败 (#4448)]**: 长对话的核心稳定性体验问题。同质 Issue #4447 已关闭。
    *   **[LLM 执行过于频繁，需要等待 300 秒 (#4468 / #4478)]**: 多通道用户（飞书）也遇到此限流错误，与 PR #4487 相关。
    *   **[get_token_usage 工具无法运行 (#4473)]**: 影响基础统计功能，已关闭。

*   **其他 (Minor/Low)**:
    *   **[Windows GBK 编码问题系统性解决方案 (#4481)]**: 用户建议从零散修复转向系统性解决，虽非阻塞但影响面广。
    *   **[Chromadb Rust Binding 段错误 ({SIGSEGV}) 致命错误 (#3854)]**: 该长期遗留问题（4月27日报告）在当前会话中仍处于Open状态，影响使用该向量库的用户。

## 6. 功能请求与路线图信号

今日功能请求呈现明显“社区前驱”和“企业级深化”趋势：

*   **前沿模型支持**: 社区对 `chatgpt-5.5` (#4474) 等最新模型的支持需求旺盛，这将成为 provider 层持续适配的重点。
*   **开发者体验优化**: 提议使用 `typer` 替换 `click` 以获得更好的现代 CLI 体验 (#4472)，以及 Flathub 打包安装 (#4486)，体现了社区对更流畅开发部署流程的期待。
*   **企业级特性的呼声**: 除了上文提到的 WeChat 通道稳定性（PR #4490），还涉及**子代理 (sub-agent) 是否继承全局 MCP/ACP 配置** (#4491) 的讨论，表明用户正在利用多代理架构构建更复杂的自动化流程。
*   **测试基础设施的完善**: Issue #4461 (Login 页面 E2E 测试) 和 #4462 (CI 工作流) 表明社区正在系统性地提升代码质量，这是项目长期健康发展的积极信号。

**可能纳入下个版本的功能**：待合并的 Tauri 2.x桌面应用 (#3813)、轻量级目标模式 (#4443)、插件官方分发系统 (#4482) 和三方 PR #4418 的宠物插件，这些是重磅且有潜力的功能。

## 7. 用户反馈摘要

*   **稳定性是最大痛点**：多个 Issues (#4469、#4453) 中用户反复提及重启、重装 Docker、回退版本均无法解决聊天无声或停滞问题，并伴有负面情绪（如“受不了了，这阿里技术也不行” #4475）。这凸显了目前基础运行时稳定性的用户体验亟待提升。
*   **对深度功能有渴望**：用户期望插件能无缝工作 (#4485)、支持最新最强模型 (#4474)、拥有良好的长对话管理机制 (#4448)，表明用户群体已不满足于基础聊天功能，而是要求更复杂、可靠的 Agent 能力。
*   **Windows 生态仍是短板**：Windows GBK 编码问题 (#4481) 被定性为“一天能看到无数次”的日常痛点，其频率与影响面远超单个功能 Bug。
*   **对企业级通道的信赖搭建**：用户对微信、飞书等通道 (Issues #4477、#4478) 的定时任务、容错机制提出明确需求，这是从个人工具转向团队协作工具的关键信任门槛。

## 8. 待处理积压

以下为项目中的长期未响应或重要待办事项，需要维护团队关注：

*   **严重 Bug**：
    *   **[Chromadb Rust binding segfault (#3854)]**：已有多人提及，自4月27日以来一直处于 Open 状态，没有关联的合并 PR，是当前最危险、影响最恶劣的潜在基础设施 Bug 之一。
*   **重要/大型功能PR**：
    *   **[Tauri 2.x 桌面应用支持 (#3813)]**：自4月24日提交，至今仍在审核中。这是项目从 Web 应用走向桌面客户端的战略级 PR，长时间未合并可能会影响社区贡献者的积极性。
    *   **[前端单元测试里程碑 (#4332)]**：这是提升项目可维护性的关键工单，已开启并关联多个子任务，建议在下一个版本前加快合并进度。
*   **长期 Open Issue**：
    *   **[🐾 Help Wanted: Open Tasks (#2291)]**：作为社区贡献指南，长期处于开放状态可鼓励外部贡献，但目前需确保其指向的任务列表是及时更新的。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据 ZeroClaw (github.com/zeroclaw-labs/zeroclaw) 的 GitHub 数据，为您呈上 2026-05-18 的项目动态日报。

---

## ZeroClaw 项目动态日报 | 2026-05-18

### 1. 今日速览

ZeroClaw 项目今日处于**高度活跃**状态。社区贡献和问题反馈数量依然庞大（50条PR，15条Issue），显示出极强的生态活力。然而，项目也面临严峻挑战：与此前记录的“疯狂合并”期不同，今日PR积压（43条待合并）严重，且多个高优先级（P1）的Bug（特别是针对新模型API的兼容性问题）悬而未决。项目团队正集中精力解决关键的兼容性和稳定性问题，尤其是DeepSeek-V4和小米推理模型等新兴模型的接入，这已成为制约用户体验的核心瓶颈。

### 2. 版本发布

无。过去24小时内无新版本发布。

### 3. 项目进展

过去24小时内，有7个PR被合并或关闭，主要集中在问题修复和文档的即时更新上：

- **修复技能工具命名兼容性**：[PR #6732](https://github.com/zeroclaw-labs/zeroclaw/pull/6732) 被合并，修复了Skill工具在与OpenAI兼容接口交互时，因使用 `.` 分隔符导致API报错的问题，解决了 OpenAI/OpenRouter/Gemini 等模型调用特定代理技能时的阻塞性Bug。
- **修复MiniMax 提供商文档**：[PR #6755](https://github.com/zeroclaw-labs/zeroclaw/pull/6755) 被合并，更新了过时的MiniMax API端点和模型信息。
- **修复CRON在Windows上的问题**：[PR #6750](https://github.com/zeroclaw-labs/zeroclaw/pull/6750) 和 [Issue #6705](https://github.com/zeroclaw-labs/zeroclaw/issues/6705) 关闭，修复了Windows上因快照TTL设置不合理导致的性能问题以及CRON因 `sh` 硬编码导致无法执行的问题。
- **渠道运行时的本地化问题**：[Issue #6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548) 被关闭，修复了部分渠道回复未遵循Fluent本地化设置的问题。
- **并发启动的Schema初始化问题**：[Issue #6431](https://github.com/zeroclaw-labs/zeroclaw/issues/6431) 被关闭，修复了SQLite内存Schema在并发启动时可能失败的问题。

这些合并表明项目正在积极消化社区贡献，并快速响应高优先级的Bug修复。

### 4. 社区热点

- **DeepSeek-V4 API 兼容性问题（#6059）**：[Issue #6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059) 持续成为焦点，获得了9条评论和4个👍。用户强烈希望ZeroClaw能与DeepSeek最新的V4-Pro/V4-Flash模型（特别是其推理模式）兼容，但目前遇到了API格式错误的障碍。这反映出社区迫切需要一个稳定、兼容主流前沿模型的 Agent 框架。
- **Kimi 代码流式调用错误（#5600）**：另一引发广泛讨论的是[Issue #5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)。用户在使用Kimi的“thinking”模式进行流式工具调用时遇到工作流阻塞（S1级别）的严重错误。该问题也获得了9条评论，表明大型语言模型的“推理/思维”模式在Agent框架中的工具调用链条上存在普遍性的集成难题。
- **v0.8.0 大版本合并与反馈（#6398）**：尽管未在24小时内合并，但[PR #6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)（v0.8.0: 多智能体运行时）仍是社区讨论的核心。这个巨大的PR（影响600多个文件）决定着项目未来方向，用户和贡献者正在对其进行深入审查，反馈中包含了大量具体建议和截图，显示出社区对下一版本的高度期待。

### 5. Bug 与稳定性

按严重程度排列：

- **S0 - 数据丢失 / 安全风险**：
    - **[Issue #6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672)**: 在使用小米Mimo模型（mimo-v2.5, mimo-v2.5-pro）的思维模式下进行工具调用时，`reasoning_content` 无法传递到后续循环，可能导致代理行为错误。
    - **[Issue #6747](https://github.com/zeroclaw-labs/zeroclaw/issues/6747)**: `amannn/action-semantic-pull-request` CI 工具因未加入允许列表而无法运行，导致PR标题检查流程失效。

- **S1 - 工作流阻塞**：
    - **[Issue #5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)**: 使用Kimi代码提供商时，流式调用工具失败。以上两问题均无明确的快速修复PR，风险较高。

- **S2 - 性能退化**：
    - **[Issue #6059](https://github.com/zeroclaw-labs/zeroclaw/issues/6059)**: 与DeepSeek-V4 API不兼容。但已有[PR #6753](https://github.com/zeroclaw-labs/zeroclaw/pull/6753) 尝试修复base_url覆盖问题，这是解决此兼容性问题的一步。
    - **[Issue #6431](https://github.com/zeroclaw-labs/zeroclaw/issues/6431)**: SQLite并发启动Schema失败（已关闭）。

- **S3 - 小问题**：
    - **[Issue #6548](https://github.com/zeroclaw-labs/zeroclaw/issues/6548)**: 渠道回复绕过本地化设置（已关闭）。

### 6. 功能请求与路线图信号

- **ACP网桥改进**：用户 [Issue #6754](https://github.com/zeroclaw-labs/zeroclaw/issues/6754) 指出ACP网桥的自动配对方式过于依赖一次性代码，建议采用更健壮的令牌缓存机制。对应地，有 [PR #6649](https://github.com/zeroclaw-labs/zeroclaw/pull/6649) 正在实现ACP会话持久化，这可能涵盖或解决此问题，表明该功能有很高概率进入下一版本。
- **技能系统增强**：社区对 `zeroclaw skills` 的讨论仍在继续。[Issue #6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253) 作为v0.7.6版本的跟踪器，广泛收集了关于技能CLI、加载、审计、沙箱等方面的反馈。这明确是项目发力的重点。
- **更严格的工具解析模式**：[PR #6675](https://github.com/zeroclaw-labs/zeroclaw/pull/6675) 提出通过 `agent.strict_tool_parsing` 配置项，让用户能够选择使用原生API的工具调用，而不是允许模型生成格式不标准的文本。这有助于提高代理行为的确定性，可能成为下一个版本的重要特性。

### 7. 用户反馈摘要

- **对前沿模型支持的迫切需求**：用户在对DeepSeek-V4 (#6059) 和 小米Mimo (#6672) 模型的反馈中，表达了强烈且具体的失望情绪。他们测试了最新模型，却因ZeroClaw未能完全适配其API格式（尤其是“思维模式”）而导致代理循环断裂。这揭示了ZeroClaw当前的最大痛点：**对新兴模型API特性的适配滞后于模型发布速度**。
- **跨平台兼容性的持续挑战**：Windows用户再次成为易受影响群体。[Issue #6705](https://github.com/zeroclaw-labs/zeroclaw/issues/6705)（CRON执行失败）被修复，但暴露了代码中对特定Shell (`sh`) 的硬编码依赖问题。FreeBSD用户[Issue #1924](https://github.com/zeroclaw-labs/zeroclaw/issues/1924) 则在近期才获得关闭确认，显示出用户对更广泛平台预编译二进制文件的期待。
- **CI/DevOps 环节的摩擦**：用户 [Issue #6747](https://github.com/zeroclaw-labs/zeroclaw/issues/6747) 和 [Issue #6751](https://github.com/zeroclaw-labs/zeroclaw/issues/6751) 报告了CI流程（PR标题检查）自引入以来就从未正确运行。这并非功能性问题，但暴露了项目在引入CI规范时，缺乏充分的测试和配置步骤，导致工具形同虚设。

### 8. 待处理积压

- **[PR #6398](https://github.com/zeroclaw-labs/zeroclaw/pull/6398)**: **v0.8.0 大版本合并**。这是当前影响最大、风险最高的待办事项。其庞大的规模和广泛的修改让审核变得异常困难，但它的完成也标志着项目进入一个全新阶段。任何关于此PR的新偏差、讨论或进展都值得高度关注。
- **[Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)**: **审计153个丢失的提交**。这是一个遗留问题，需要持续追踪以确保早期开发的成果被妥善找回和整合。虽然标记为“in-progress”，但状态在积压中较为显眼。
- **[PR #6688](https://github.com/zeroclaw-labs/zeroclaw/pull/6688)**: **修复委托代理的提示词注入模式**。此PR解决了委托代理硬编码设置的问题，对系统安全性和模型效率至关重要，但已等待3天未被合并，需提醒维护者关注。

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*