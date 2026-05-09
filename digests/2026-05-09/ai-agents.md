# OpenClaw 生态日报 2026-05-09

> Issues: 464 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-09 07:22 UTC

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

好的，请看为您生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 — 2026-05-09

## 1. 今日速览

今日项目活跃度极高，社区反馈和开发活动均处于峰值状态。过去24小时内，项目共处理了 **464 条 Issue** 和 **500 个 Pull Request (PR)**，显示出庞大的用户基础和密集的开发协作。Issue 的关闭率为 **41.2%**，但 PR 的待合并率高达 **71.6%**，表明合并流程可能存在瓶颈。今日未发布新版本，但大量针对 **2026.5.4/5.5/5.6** 版本的回归问题 (Regression) 报告涌来，指向最近一次大版本更新可能引入了显著的稳定性问题。社区焦点集中在 **集成稳定性**（特别是微信/飞书/Telegram/Discord）、**基础功能故障**（文件系统、模型调用）以及 **用户体验瑕疵**（文本泄漏、回复错位）。

## 2. 版本发布

*（无）*

## 3. 项目进展

尽管合并的 PR 数量（142个）远少于待处理数量（358个），但今日关闭的 PR 仍包含了若干重要修复，推动了项目在特定领域的进展：

- **核心功能修复**：重要的 PR **#50955** 已被合并，它统一了 ACP（Agent Communication Protocol）中的线程绑定和投递路由，这解决了在不同会话模式下（如 `sessions_spawn` 和 `/acp spawn`）的行为不一致性，增强了多Agent协作的根基。
- **用户界面与诊断优化**：PR **#77221** 被合并，改善了 CLI 的错误提示，在用户错误输入工具名时提供更明确的指引。同时，PR **#79691** 虽为开启状态，但旨在修复 OTel 诊断插件无法正常捕获模型调用内容的问题，该修复将极大地增强可观测性。
- **持续重构**：**#79693** 和 **#77221** 等PR的合并表明，团队仍在持续优化代码清晰度和错误提示，这是一项长期的工程健康投资。

## 4. 社区热点

今日讨论热度最高的议题集中体现了用户对产品稳定性和核心体验的关切：

- **问题 #14593** ([链接](openclaw/openclaw Issue #14593))：**Docker 容器内安装技能失败**。该 Issue 累计获得 **29条评论** 和 **17个👍**，是社区最关注的痛点。用户抱怨官方 Docker 镜像未预装 `brew`，导致依赖 Homebrew 的技能无法使用，这直接影响新用户的开箱即用体验。
- **问题 #34810** ([链接](openclaw/openclaw Issue #34810))：**Agent 突然丧失文件系统操作能力**。同样有 **29条评论**，描述了一个严重的回归现象：Agent 在没有任何预兆的情况下失去创建文件、运行命令的能力。这触及到 AI Agent 的核心能力，引发了用户的强烈不安和讨论。
- **问题 #25592** ([链接](openclaw/openclaw Issue #25592))：**工具调用间的文本泄漏至消息频道**。虽然只有0个赞，但 **26条评论** 表明这是一个颇具争议性的UX问题。用户认为 Agent 的内部处理输出（如错误信息、处理状态）不应被直接发送到 Slack、iMessage 等外部聊天频道，请求更严格的输出过滤。

**分析**：社区情绪呈现两极分化。一方面，用户对 OpenClaw 的强大功能抱有信心，积极尝试各种集成和技能；另一方面，近期版本引入的稳定性问题（尤其是 Agent 基础能力丧失）严重打击了用户的信任感。社区的核心诉求已从“增加功能”转向“保证核心功能的可靠性”。

## 5. Bug 与稳定性

今日 Bug 报告数量激增，且多为回归问题。以下是按严重程度排列的关键项：

- **【严重-行为错误】Agent 功能丧失**：
    - **#34810** ([链接](openclaw/openclaw Issue #34810))：Agent 突然无法执行文件和系统命令。*（无关联 Fix PR）*
    - **#32296** ([链接](openclaw/openclaw Issue #32296))：Agent 回复错位，回复上一条消息而非当前消息。*（无关联 Fix PR）*
- **【严重-回归】插件/通道集成故障**：主要影响近期版本 (2026.5.4/5.5/5.6)。
    - **微信插件**：**#78434**, **#77837**, **#77779**, **#78376** 等多个 Issue 报告微信插件在升级后出现 `TypeError: fetch failed` 或初始化超时。
    - **飞书/Feishu**：**#77869**, **#78949** 报告飞书群聊中 Agent 无回复，**#78262** 报告会话键值对不匹配导致会话分裂。
    - **Telegram**：**#79455** 报告私聊话题回复失败。
    - **Discord**：**#78572** 报告 Discord 的 `message` 工具发送失败，**#77254** 报告投递适配器丢失。
- **【重要-网关稳定性】**：
    - **#78402** ([链接](openclaw/openclaw Issue #78402))：网关因事件循环饥饿导致 WebSocket 连接反复断开。
    - **#71127** ([链接](openclaw/openclaw Issue #71127))：网关检测到卡住的会话但无法自动中止，需要外部重启才能恢复。
    - **#79596** ([链接](openclaw/openclaw Issue #79596))：网关过早发出“ready”信号，此时插件尚未完成注册。*（被标记为 Beta release blocker）*
- **【中等-模型兼容性】**：**#67158**、**#78000**、**#78502**、**#78962** 等报告了多种模型（如 Codex、Gemini、Cloudflare AI Gateway）在特定配置下无法使用或超时。
- **【低-体验/功能缺陷】**：
    - **#12590** ([链接](openclaw/openclaw Issue #12590))：`memoryFlush` 内存刷新功能不可靠。
    - **#77260** ([链接](openclaw/openclaw Issue #77260))：群聊中命令回复消失。

## 6. 功能请求与路线图信号

尽管Bug频发，社区对新功能的讨论并未停止。以下需求可能被纳入后续版本：

- **核心能力增强**：
    - **#18160** ([链接](openclaw/openclaw Issue #18160))：请求为Cron作业增加“直接执行模式”，避免每次都经过LLM，以提高效率和可靠性。该诉求获得 **9个👍**，表明用户对提高自动化任务性能有明确需求。
    - **#22438** ([链接](openclaw/openclaw Issue #22438))：请求实现层级化的引导文件加载，以节省LLM Token和上下文窗口。这是一个成熟的功能提议，与优化成本和性能直接相关。
    - **#22358** ([链接](openclaw/openclaw Issue #22358))：请求增加 `post_subagent_complete` 扩展钩子，用于在子Agent完成后自动生成报告，增强可追溯性。
- **集成与平台扩展**：
    - **#20786** ([链接](openclaw/openclaw Issue #20786))：请求支持 Telegram Business Bot 功能（获得 **3个👍**），以扩展在商业场景下的应用。
    - **#17925** ([链接](openclaw/openclaw Issue #17925))：请求为 ZAI (GLM) 和 Google (Gemini) 提供商添加原生 `web_search` 工具透传支持（获得 **5个👍**），表明用户期望在更多模型上实现联网搜索能力。

**路线图信号**：从大量针对 PR **#78595** (Refactor runtime state into SQLite) 和 **#79703** (feat(training-export)) 的讨论和提交来看，项目团队正蓄力进行重大的**底层架构重构**和**数据训练能力扩展**。虽然这些PR合并尚需时日，但它们代表了项目未来的长期演进方向。

## 7. 用户反馈摘要

从 Issues 评论中可以提炼出以下真实用户反馈：

- **“为什么要重启我的机器人？我的一切都乱套了！”**：多位用户抱怨升级到新版本后，自动运行的 `openclaw doctor --fix` 命令（如 #78407）会修改关键的配置文件，导致模型引用、API认证等设置被覆盖，迫使用户需要手动修复。这暴露了自动修复功能过于激进而缺乏用户确认机制的隐患。
- **“我以为自己买了一个AI超级大脑，结果它连个文件都建不了”**：针对 #34810 等核心功能丧失的 Bug，用户的失望和困惑情绪溢于言表。这表明任何影响Agent基础生存能力（读写、执行）的Bug都是致命的，优先级必须最高。
- **“我升级只是为了修复上一个Bug，结果引入了更多Bug”**：这是社区对近期版本更新最普遍的负面评价。多个用户在报告回归问题时都提到了“升级自XXXX版本后出现问题”，这种“修一个坏一片”的更新模式正在削弱用户的升级意愿。

## 8. 待处理积压

以下 Issue 和 PR 虽非今日热点，但长期未得到解决，值得维护者关注：

- **问题 #12590** ([链接](openclaw/openclaw Issue #12590))：创建于 **2026-02-09**，关于 `memoryFlush` 不可靠的 Bug 已持续3个月未关闭，影响 Agent 的长期记忆功能。其问题表述清晰且有复现路径，但迟迟未有进展。
- **问题 #8295** ([链接](openclaw/openclaw Issue #8295))：创建于 **2026-02-03**，一个关于 Telegram 群组 `allowBots` 支持的功能请求，已开放超过3个月且获得 **4个👍**。考虑到 Telegram 是热门渠道，此差异化功能的缺失可能让部分用户转向竞品。
- **问题 #14344** ([链接](openclaw/openclaw Issue #14344))：创建于 **2026-02-12**，请求为 WhatsApp 增加消息撤回功能。同样是一个明确的用户体验功能，但积压至今。

**提醒**：以上积压项若不处理，会逐步积累为技术债务，并降低社区对项目维护力度的整体评价。

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域开源项目分析师，基于2026年5月9日各项目的详细动态，现提供横向对比分析报告如下。

---

# 个人AI助手与自主智能体开源生态横向对比报告（2026-05-09）

## 1. 生态全景

当前个人AI助手/自主智能体开源生态整体呈现 **“高产出、高压力、分化明显”** 的态势。以OpenClaw、ZeroClaw、IronClaw为代表的头部项目单日处理数百个Issue和PR，代码迭代速度惊人，但伴随而来的是**回归Bug密集爆发**（如OpenClaw Agent功能丧失、PicoClaw图片识别回归）和**PR积压严重**（Hermes Agent 47/50待合、NanoBot 110/143待合），暴露出社区推动力与核心维护能力之间的错配。与此同时，中等规模的NanoBot、LobsterAI、CoPaw等通过聚焦WebUI、会话持久化、工具协议兼容性等具体痛点到快速修复，形成了稳定的发布节奏。此外，Moltis、ZeptoClaw等小型项目或处于架构重构期（Moltis）或近乎停滞，体现了生态内部梯队差距正持续扩大。整体而言，**稳定性与可靠性成为社区最强烈的底层诉求**，而“多Agent协作”、“MCP协议”、“持久化会话”、“可观测性”则是跨项目的共性技术延伸方向。

## 2. 各项目活跃度对比

| 项目 | 当日新Issues (活跃) | 当日PR总数 (合并/关闭) | 待合PR数 | 版本发布 | 健康度评估 |
|------|----------------------|------------------------|----------|----------|------------|
| **OpenClaw** | 464 | 500 (142) | 358 | 无 | ⚠️ 极高活跃但稳定性崩塌，回归问题严重，PR合并瓶颈明显 |
| **ZeroClaw** | 50 | 50 (18) | 32 | 无 | 🟢 极高活跃，修复快速，批量频道与配置增强 |
| **IronClaw** | 12 | 45 (18) | 27 | 无 | 🟢 高活跃，Reborn架构推进有力，测试可靠性好 |
| **CoPaw** | 36 | 42 (16) | 26 | v1.1.6-beta.1 | 🟢 高活跃，版本迭代快，社区反馈闭环好 |
| **LobsterAI** | 2 | 16 (16) | 0 | 无 | 🟢 高活跃，交付力极强，集中在UI与核心修复 |
| **NanoBot** | 7 | 143 (33) | 110 | 无 | 🟡 高活跃但PR大量积压，会话稳定性改善明显 |
| **Hermes Agent** | 50 | 50 (3) | 47 | 无 | 🔴 高活跃但合并极慢，Gemini/Codex 429等严重Bug未修复 |
| **PicoClaw** | 8 | 23 (5) | 18 | 1 nightly | 🟢 中等活跃，exec安全修复和图片回归已修复 |
| **NanoClaw** | 2 | 5 (5) | 12 | 无 | 🟢 中等活跃，SIGTERM优雅关闭修复受好评 |
| **NullClaw** | 2 | 2 (1) | 1 | 1 nightly | 🟡 低活跃，两个关键Bug（Telegram配置 & 安全审批缺失） |
| **Moltis** | 0 | 5 (2) | 3 | 1 (20260508.01) | 🟡 低活跃，功能推进（语音、国际化）但社区互动少 |
| **ZeptoClaw** | 0 | 1 (0) | 1 | 无 | 🔴 极低活跃，唯一PR#571搁置5天无review |
| **TinyClaw** | 0 | 0 | 0 | 无 | 无活动 |

> *健康度评估：🟢 活跃健康 / 🟡 有风险 / 🔴 严重问题*

## 3. OpenClaw在生态中的定位

OpenClaw是当前生态的**核心参照项目**（本报告以OpenClaw为基准），其社区规模（单日464条Issue、500个PR）远超其他所有项目之和，体现了**绝对的用户基数优势**。其优势在于：
- **通道与插件生态最丰富**：微信、飞书、Telegram、Discord、WhatsApp等全覆盖，社区贡献量最大。
- **Agent协议（ACP）与运行时底座最成熟**：统一了线程绑定、投递路由等关键机制，为多Agent协作奠定基础。
- **功能最全面**：从Cron任务、文件系统、记忆管理到网关，几乎涵盖所有个人助手能力。

然而，**规模效应也带来了稳定性悬崖**：2026.5.4/5.5/5.6版本的回归问题（Agent功能丧失、文件操作失效）引发社区强烈不满，修复速度（PR合并效率71.6%待合）跟不上问题爆发速度。相较之下，NanoBot和PicoClaw虽然规模小，但每个版本更新后回归问题数量少且修复快，体现了**小规模团队的敏捷优势**。

**技术路线差异**：OpenClaw走“大而全”的集成路线，而NanoBot、PicoClaw更侧重**CPU/GPU本地推理**与**轻量级部署**，Moltis则专注**多智能体对话编排**。OpenClaw的架构复杂度远高于后者，导致其维护成本成倍增加。

## 4. 共同关注的技术方向

多个项目不约而同聚焦以下方向（按热度排序）：

1. **会话持久化与稳定性**  
   - 涉及项目：OpenClaw (#14593 Docker技能安装失败)、NanoBot (#3680 会话文件损坏、#3712 加强校验)、CoPaw (#4145 多智能体配置持久化)、ZeroClaw (#6309 `upsert_agent`覆盖设置)  
   - 共同诉求：确保进程重启/升级后会话、配置、记忆不丢失，避免“修一个Bug引入更多Bug”的恶性循环。

2. **工具与模型调用可靠性**  
   - 涉及项目：OpenClaw (#34810 Agent文件系统功能丧失)、Hermes Agent (#20465 CLI未自动回退Codex 429)、ZeroClaw (#6298 空tool_calls导致400错误)、PicoClaw (#1042 exec安全守卫误报)  
   - 共同诉求：消除跨轮次工具调用的死循环、限流误判、参数校验失败，建立统一的故障转移与重试策略。

3. **MCP (Model Context Protocol) 协议增强**  
   - 涉及项目：PicoClaw (#2782 MCP Streamable HTTP传输)、CoPaw (#3149 MCP工具列表支持)、IronClaw (PR #3346 MCP工具过滤)、ZeroClaw (多项目涉及MCP路由)  
   - 共同诉求：支持新一代MCP规范、多Agent间工具发现与权限控制、通过MCP桥接不同提供商模型。

4. **企业级渠道与精细管控**  
   - 涉及项目：Discord/飞书/企业微信的频道隔离（ZeroClaw #6378、PicoClaw #2785飞书通知）、Telegram Business Bot（OpenClaw #20786）、企业微信（IronClaw #2394）、Nextcloud Talk（ZeroClaw #6048）、Discord多频道（ZeroClaw#6378）  
   - 共同诉求：通过白名单/黑名单、频道级别配置、审批卡片等技术手段，将AI Agent从个人玩具升级为可治理的企业工具。

5. **可观测性（Observability）**  
   - 涉及项目：OpenClaw (#79691 OTel诊断插件修复)、Hermes Agent (#22342 Langfuse追踪缺失)、PicoClaw (工具体系支持SSE事件 #3698)  
   - 共同诉求：提供模型调用内容、工具执行过程、Agent内部状态的完整可追溯性，支持调试与合规审计。

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 全功能通用个人助手 | 开发者、进阶用户、企业团队 | 多通道+ACP协议+插件市场，集成最广；配置复杂度高 |
| **NanoBot** | 轻量级命令行+WebUI助手 | 个人开发者、本地推理爱好者 | 极简部署（Python），偏好Olama/LM Studio等本地模型；WebUI原生 |
| **Hermes Agent** | Agent协作框架 | 多Agent系统开发者 | 以MCP和“spawn”机制为核心，特别关注ACP协议生命周期 |
| **PicoClaw** | 开源嵌入式AI Agent | 嵌入式/IoT开发者（Sipeed） | 支持硬件加速（K210等），极低资源消耗；原生C语言核心 |
| **NanoClaw** | 容器化部署AI助手 | DevOps、K8s用户 | 原生Docker/Kubernetes支持，强调优雅关闭与卷持久化 |
| **NullClaw** | 最小化可验证Agent框架 | 安全研究者、审计人员 | 极简代码库，侧重数据治理层（PR#885）、监督模式合规性 |
| **IronClaw** | 高可靠性企业Agent | 企业级自动化团队 | “Reborn”架构聚焦持久化凭证、加密层、循环驱动；强测试门禁 |
| **LobsterAI** | 聊天增强与知识管理 | 知识工作者 | 深度集成CodeMirror、书签、Mermaid图表；侧重前端交互体验 |
| **CoPaw** | 多智能体协作平台 | 团队协作（企业微信/飞书） | “项目组+多角色”群聊模式，浏览器工具批量操作 |
| **Moltis** | 多模型对话编排 | AI应用开发者 | 强调国际化和语音（OpenAI STT），Web Composer全新UI |
| **ZeptoClaw** | 微内存Agent | 研究者 | 极简内存工具定义，几乎无维护活动 |
| **ZeroClaw** | 高性能生产级Agent | 高并发服务团队 | Rust/Python混合，Matrix/Nextcloud等重型通道，多智能体运行时（v0.8.0） |

## 6. 社区热度与成熟度

根据活跃度、PR合并效率、版本发布频率、Bug修复速度，可将项目分为四个梯队：

- **第一梯队（极高活跃、生态主导）**：**OpenClaw**、**ZeroClaw**、**IronClaw**  
  特征：单日处理数十甚至数百条Issue/PR，功能迭代最前沿，但需承受稳定性压力（OpenClaw最突出）。IronClaw虽活跃但测试门禁严格，Bug率相对较低。

- **第二梯队（高活跃、快速迭代）**：**NanoBot**、**CoPaw**、**LobsterAI**、**PicoClaw**  
  特征：日处理10~40条Issue/PR，版本发布频繁（CoPaw beta、PicoClaw nightly），修复速度快（LobsterAI合并率100%），社区反馈闭环佳。

- **第三梯队（中等活跃、局部活跃）**：**NanoClaw**、**NullClaw**、**Moltis**  
  特征：核心贡献者少（NanoClaw主要1~2人），功能推进稳健但社区互动不足，有长期悬而未决的重要Issues。

- **第四梯队（低活跃/停滞）**：**Hermes Agent**（极高PR积压）、**ZeptoClaw**、**TinyClaw**  
  特征：PR合并速度极慢（Hermes 3/50）、或几乎无活动（Zero活动为零但之前有积累）。贡献者可能流失。

**成熟度简评**：OpenClaw虽规模最大但稳定性处于**早期成长期**的典型阵痛；NanoBot、PicoClaw等中小项目反而在质量上更成熟；IronClaw因企业级定位和强质量门禁是最接近“生产就绪”的项目之一。

## 7. 值得关注的趋势信号

**趋势一：从“功能竞赛”转向“可靠性基建”**  
多个项目同时出现回归问题（OpenClaw Agent丧失、PicoClaw图片识别回退、ZeroClaw Matrix编译失败），社区情绪从“期待新功能”转变为“请先修好基础功能”。**对AI智能体开发者而言**：在集成新通道或增加复杂工具前，优先建立回归测试套件和自动化CI门禁将成为生存关键。

**趋势二：对话持久化与状态管理成为“硬需求”**  
NanoBot (#3680)、CoPaw (#4145)、OpenClaw (#12590 memoryFlush) 等多项目用户明确要求会话、配置、记忆在重启和升级后不丢失。**这预示者：** 个人AI助手将逐渐从“临时聊天工具”转型为“长期数字伙伴”，持久化数据层（SQLite、RocksDB等）的健壮性会决定用户黏性。

**趋势三：MCP与多Agent协作从概念走向工程化**  
PicoClaw请求Streamable HTTP传输、CoPaw合并了MCP工具列表、IronClaw打磨工具过滤、ZeroClaw多智能体运行时即将并入主线。**对架构师而言**：MCP将成为下一代AI Agent互联的“HTTP协议”，提前投入兼容性设计和降级策略（如空tool_calls处理）将获得竞争优势。

**趋势四：企业级管控需求快速渗透**  
Discord频道隔离、飞书审批卡片、Telegram Business Bot、Nextcloud Talk流式推送——这些需求不再是“有更好”，而是“必须有”。**AI Agent开发者应重视**：每个通道的准入、限流、审批、审计能力需要一开始就设计为插件化配置，否则后期重构成本极高。

**趋势五：中文语言与文化偏好正在塑造项目演进**  
CoPaw大量用户用中文提交Issue（超多轮对话、LM Studio配置）、LobsterAI添加了中文完整本地化PR（#21997）、PicoClaw飞书通道优化得到中国用户强烈呼应。**信号**：具备中文社区运营和本地化集成（企业微信、飞书、阿里云DashScope等）的项目，在中国市场将获得天然优势。

---

*报告基于2026年5月9日各项目公开数据生成，所有指标统计截止UTC时间当日。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-05-09

## 今日速览

过去 24 小时 NanoBot 保持高度活跃：共处理 18 条 Issue（新开/活跃 7 条，关闭 11 条），以及 143 条 PR（其中 33 条已合并/关闭，110 条待合并）。社区围绕 WebUI 原生需求、会话稳定性和平台兼容性的讨论持续升温，多个关键 Bug 修复已通过 PR 落地。尽管暂无新版本发布，但代码库正在经历密集的架构重构与缺陷修正，项目健康度良好。

---

## 版本发布

无新版本发布。

---

## 项目进展

今日关闭/合并的 PR 覆盖了多个核心领域：

- **会话持久化与稳定性**：`#3685` 修复了 `_last_summary` 在进程重启后丢失的问题（后续被 `#3710` 撤销，原因待确认）；`#3680` 修复了会话文件损坏时 `last_consolidated` 超出消息数量的崩溃；`#3712` 进一步增强了该场景的保护。
- **WebSocket 通道**：`#3673` 修复了 `_dispatch_envelope` 静默丢弃媒体附件的问题，确保图片/文件路径正确传递给 Agent。
- **CLI 与交互体验**：`#3697` 修复了 Windows 下输入 emoji 导致 `json.dumps` 崩溃的 surrogate 编码问题；`#3705` 修复了交互重试时 spinner 与进度消息的终端混乱。
- **Web UI / BYOK**：`#3709` 在设置页面新增了 Web Search 密钥配置的分段控件；另有多项历史 Web UI PR 被标记为已关闭（`#3030`、`#1707`、`#2050`、`#1650`、`#2972`、`#1047`），表明官方正在整合社区贡献。
- **MCP 与 Provider**：`#3706` 新增了 CRM 报表助手的 mock stdio 服务器；`#3707`（新开）提供了 NVIDIA NIM Provider 支持。
- **贡献指南**：`#3534` 添加了 `CLAUDE.md` 和 `.agent/` 目录，方便 AI 编码助手协作。

**整体进展**：项目在会话可靠性、通道兼容性、平台适配三个维度均有实质性推进，架构层面开始引入 `AgentLoop.from_config()` 等统一初始化方法（`#3708`），为后续多模型预设功能奠定基础。

---

## 社区热点

1. **WebUI 原生需求（#2949、#1922、#3059）**  
   - `#2949`（👍 13，评论 10）和 `#1922`（👍 10，评论 9）是社区持续呼吁官方内置 WebUI 的集中体现。`#2949` 发起功能讨论，`#1922` 展示了社区自建面板 `nanobot-webui`。今日多个相关 PR 被关闭，暗示官方可能正在采纳或重构。  
   - 链接：https://github.com/HKUDS/nanobot/issues/2949  
   - 链接：https://github.com/HKUDS/nanobot/issues/1922

2. **“nanobot update” 命令提议（#3421）**  
   - 用户期望一条命令完成版本检查与升级，减少手动 `pip install` 的碎片化操作。4 条评论，总体支持。  
   - 链接：https://github.com/HKUDS/nanobot/issues/3421

3. **重复工具调用防护（#3699、#3700）**  
   - 由贡献者提出的逻辑缺陷：本地工具调用（如 `exec`）未像外部搜索一样设置重复调用防护，可能导致无限循环。两天内提出 Issue 并跟进策略讨论，反映出开发社区对稳定性的重视。  
   - 链接：https://github.com/HKUDS/nanobot/issues/3699  
   - 链接：https://github.com/HKUDS/nanobot/issues/3700

---

## Bug 与稳定性

| 严重程度 | 问题描述 | 状态 / 修复 |
|----------|----------|------------|
| **高** | **重复相同本地工具调用导致无限推理循环（#3699）**：本地工具（如 `exec`）缺乏去重保护，Agent 可能陷入死循环。 | Issue 已关闭，关联 PR `#3700` 仍在 open，建议继续观察。 |
| **高** | **WebSocket 通道静默丢弃媒体附件（#3674）**：客户端发送的图片/文件路径被忽略，Agent 无法获取。 | 已通过 `#3673` 修复。 |
| **中** | **Windows 下输入 emoji 引起 json.dumps 崩溃（#3697）**：prompt_toolkit 产生 surrogate 字符，导致消息序列化失败。 | 已通过 `#3697` 修复。 |
| **中** | **会话文件损坏后丢失全部历史（#3680）**：`last_consolidated` 超过实际消息数时 bot 遗忘上下文。 | 已通过 `#3680` 修复，`#3712` 加强校验。 |
| **中** | **飞书群组中发送多个文件时部分文件错发到主群而非 topic（#3694）** | 已关闭（可能被修复，暂未找到对应 PR）。 |
| **低** | **转录配置不透明（#3637）**：Groq 语音转写采用错误的 API base 导致无效设置，配置体验不佳。 | Open，暂无修复 PR。 |
| **低** | **中断 Agent 导致上一轮会话上下文丢失（#3689）**：用户打断循环任务后 Agent 无法记忆之前步骤。 | Open，用户反馈典型，涉及进度状态持久化。 |

---

## 功能请求与路线图信号

- **官方 WebUI**：社区多次提议（#2949、#1922、#3059），且今日大量 Web UI 相关 PR 被标记关闭，结合 `#3709` BYOK 搜索配置的加入，推测官方 WebUI 正在加速建设中。
- **`nanobot update` 命令（#3421）**：用户期待度较高，属于 CLI 易用性提升，可能在下一个小版本实现。
- **配置 Bot 名称与图标（#3650）**：用户希望在 agent 模式下自定义显示名称和头像，已有 config.json 方案讨论。
- **Dream 模块可禁用（#3652）**：已关闭（大概率已实现），但未见到明确文档更新。
- **Subagent 个性化配置（#1012）**：希望不同子代理可设置不同的工具/模型，属于架构级增强，长期关注。
- **NVIDIA NIM 支持（#3707）**：今日新开 PR，表明 Provider 生态持续扩展。
- **SSE 工具事件注入（#3698）**：请求在 API Server 的 streaming 中输出工具调用进度，便于前端展示，对应 Hermes Agent 模式。

---

## 用户反馈摘要

- **WebUI 等待官方支持**：用户在 `#2949` 中表示“希望官方正式支持 WebUI，而不是依赖社区方案”，多位用户回复赞同，累计 13 个 👍。
- **配置语义不够直白**：`#3637` 用户反映转录 Provider 配置容易写错，文档与默认值应更清晰。
- **中断 Agent 的体验差**：`#3689` 用户描述“我发消息打断它，让它重新开始测试，但它似乎忘记了之前的会话和任务”，期望打断应保持上下文，而非重置。
- **飞书多文件发送异常**：`#3694` 用户报告在飞书 topic 中发送 2 个文件，一个发到 topic、另一个错发到 group，影响协作场景。
- **Docker 部署用户对端口绑定困惑**：`#510`（已关闭）曾反映 gateway 在 Docker 内打印绑定端口但实际未监听，虽已修复，但类似基础设施问题仍需关注。

---

## 待处理积压

以下 Issue 或 PR 长期未得到响应或解决，提醒维护者关注：

- **#1012** (2026-02-22)：Subagent 个性化工具/模型配置，已积压 2 个月，仅 1 条评论，属于中度功能请求。  
  https://github.com/HKUDS/nanobot/issues/1012
- **#1412** (2026-03-02)：允许来自另一个 Bot 的处理请求（HomeAssistant 触发），用户尝试配置 ID 未成功，缺乏反馈。  
  https://github.com/HKUDS/nanobot/issues/1412
- **#3637** (2026-05-06)：转录配置不透明，文档与配置验证改进。  
  https://github.com/HKUDS/nanobot/issues/3637
- **#3689** (2026-05-08)：中断 Agent 后上下文丢失，对交互体验影响大。  
  https://github.com/HKUDS/nanobot/issues/3689
- **#3692** (2026-05-08)：飞书 topic 隔离可配置开关，用户需要按场景启用。  
  https://github.com/HKUDS/nanobot/issues/3692
- **#3698** (2026-05-08)：API Server SSE 工具事件注入，适合与前端协作。  
  https://github.com/HKUDS/nanobot/issues/3698
- **#3700** (2026-05-08)：重复工具调用的循环升级策略，仍在 open 阶段。  
  https://github.com/HKUDS/nanobot/issues/3700
- **新开 PR #3711**（fix 摘要持久化）与 **#3712**（fix 会话损坏）已提交，需尽快合并以稳定近期回归问题。  
  https://github.com/HKUDS/nanobot/pull/3711  
  https://github.com/HKUDS/nanobot/pull/3712

---

*数据来源：GitHub HKUDS/nanobot 仓库，统计截至 2026-05-09 UTC。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，现根据您提供的Hermes Agent项目数据，为您呈上2026年5月9日的项目动态日报。

---

### Hermes Agent 项目日报 | 2026年5月9日

**数据快照时间：** 2026-05-09

---

#### 1. 今日速览

今日项目社区活跃度极高，单日产生 **50条Issue** 和 **50条PR**，表明用户参与度和开发者贡献意愿强烈。但值得注意的是，**PR积压严重**（47条待合并），而合并/关闭的仅3条，说明项目维护团队在代码审查和合并环节面临较大压力。同时，**无新版本发布**，且大量报告P1/P2级别的严重Bug，项目短期内的稳定性可能面临挑战。整体来看，项目处于 **“高活跃度、高贡献、低发布、低合并”** 状态，需要更多维护资源投入以加速产出转化。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展 (今日合并/关闭的PR)

今日主要进展是修复了ACP（Agent Communication Protocol）协议的生命周期管理问题，对依赖此协议的集成场景至关重要。

- **[已关闭] Fix ACP shutdown and resumed-session lifecycle (#22348)**
  - **标题:** Fix ACP shutdown and resumed-session lifecycle
  - **摘要:** 修复了ACP进程关闭时内存提供者（memory providers）未刷新的问题，确保短期运行的任务能保存工作状态；同时修复了恢复已结束会话时的会话ID保留问题。
  - **影响评估:** 增强了ACP协议的鲁棒性，对使用短生命周期或容器化ACP运行器的用户是重要的稳定性改进。
  - **链接:** https://github.com/NousResearch/hermes-agent/pull/22348

#### 4. 社区热点

今日社区讨论主要集中在两大痛点：**Gemini OAuth认证导致429限流**和**OpenAI Codex凭证池的健壮性**。这些是用户实际使用中的高频阻塞点。

- **🔥 热点 Issue: [Bug]: google-gemini-cli causing 429 but gquota ok (#15895)**
  - **评论数:** 8 (最多)
  - **核心诉求:** 用户反馈使用`google-gemini-cli` OAuth方式调用时，即使API配额充足（`/gquotas`显示正常），仍然遭遇HTTP 429（速率限制）错误。用户已排除API Key方式（也不工作），问题指向OAuth认证流程中的限速处理。
  - **分析:** 这是影响Gemini用户核心体验的严重问题。8条评论显示其影响范围广且用户急于解决。需关注`token`刷新策略或请求频率控制是否存在Bug。
  - **链接:** https://github.com/NousResearch/hermes-agent/issues/15895

- **🔥 热点 Issue: feat(terminal): Multi-backend terminal — local + N named remotes with persistent shell (#1855)**
  - **评论数:** 5
  - **核心诉求:** 用户提议打破当前只能使用一个终端后端的限制，支持同时连接本地和多个远程命名终端，并保持持久化会话（persistent shell）。这源于对多环境并行开发和管理的高阶需求。
  - **分析:** 这是一个极具前瞻性的功能需求，获得了4个👍。反映出用户对Hemes Agent作为统一开发工作台（unified workstation）的真实渴望。虽然短期内实现复杂，但其高点赞数表明这是路线图中的重要信号。
  - **链接:** https://github.com/NousResearch/hermes-agent/issues/1855

- **🔥 热点 Issue: [Bug]: Interactive CLI session does not auto-fallback on Codex 429 'usage_limit_reached', while cron jobs with the same fallback chain do (#20465)**
  - **评论数:** 4
  - **核心诉求:** 用户发现一个严重的行为不一致Bug：当OpenAI Codex主模型遇到429限流时，Cron任务能正常自动回退到备用模型，但在交互式CLI中却无法自动回退，导致用户交互中断。
  - **分析:** 这是一个非常专业的Bug报告，直指项目架构问题。P1的严重等级和1个👍表明该问题对日常使用影响大。用户暗示了Cron和CLI的故障转移代码路径不同，是一个需要优先修复的架构缺陷。
  - **链接:** https://github.com/NousResearch/hermes-agent/issues/20465

#### 5. Bug与稳定性

今日Bug报告数量众多，主要集中在**认证/限流**、**多平台/后端兼容性**、**核心功能挂起**等方面。以下按严重程度排列：

**P1 (严重)**
- **[Bug]: session_search can hang for 5+ minutes after upgrading (#7725)** - 核心的会话搜索功能在升级后频繁挂起超5分钟，严重影响使用。 | [View Issue](https://github.com/NousResearch/hermes-agent/issues/7725)
- **[BUG] Telegram media path escaping broken (#21527)** - Telegram消息中媒体文件路径处理失败，导致文件发送功能完全失效。 | [View Issue](https://github.com/NousResearch/hermes-agent/issues/21527)

**P2 (较高)**
- **[Bug]: OpenAI-Codex credential pool can drop newly added credential (#19566)** - Codex凭证池可能丢失刚添加的凭证，是身份认证的严重缺陷。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/19566)
- [Bug]: send_message ignores WhatsApp group target (#18646) - 发送消息到WhatsApp群组时被错误路由到个人频道。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/18646)
- [Bug]: vision_analyze 工具无法读取任何本地文件 (#22328) - 视觉分析工具对本地文件和截图均无效。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/22328)
- Discord gateway connect timeout is too short (#19776) - Discord网关默认30秒连接超时过短，导致启动失败。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/19776)
- bug: DeepSeek Anthropic-compatible API — HTTP 400 (#22313) - 与DeepSeek Anthropic API的多轮对话因`thinking`块处理问题而断开。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/22313)
- [Bug]: provider: ollama not recognized by auxiliary_client.py (#21352) - Ollama用作主模型时，辅助任务（如标题生成）会静默回退到OpenRouter。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/21352)
- [security] fix(gateway): harden Yuanbao URL downloads (PR #22340) - 针对Yuanbao媒体下载的SSRF漏洞修复PR已提交。| [View PR](https://github.com/NousResearch/hermes-agent/pull/22340) **（已有修复PR）**

**P3 (一般)**
- [Bug]: Banner title ignores skin agent_name (#6768) - 版本回归：自定义皮肤的标题名称显示错误。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/6768)
- [Bug]: custom-tools plugin tool results cause KeyError (#19814) - 自定义工具插件执行后总是报`KeyError`。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/19814)
- [Bug]: Langfuse traces missing LLM input/output and tool output (#22342) - 可观测性插件Langfuse数据缺失，且**已有修复PR (#22345)**。| [View PR](https://github.com/NousResearch/hermes-agent/pull/22345) **（已有修复PR）**

#### 6. 功能请求与路线图信号

社区对**Discord平台的深化集成**和 **“多技能/插件”的自动管理**表现出强烈兴趣，这可能是下一版本的重点方向。

- **[Feature]: Discord channel management tools (#22352)** - 要求实现Discord频道管理工具（创建/编辑/删除），与其官方文档不符。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/22352)
- [Feature]: Discord - customize reaction emoji (#22365) - 要求允许用户自定义Discord消息的默认表情符号，增强个性化和品牌化。| [View Issue](https://github.com/NousResearch/hermes-agent/issues/22365)
- **feat(skills): add session-level automatic skill preloading (PR #22341)** - 提交了一个新PR，旨在实现**会话级技能自动预加载**，减少手动指定`--skills`的操作摩擦。这是对用户痛点的直接响应。| [View PR](https://github.com/NousResearch/hermes-agent/pull/22341)
- **feat(api_server): emit hermes.reasoning.delta SSE event (PR #22364)** - 为兼容OpenAI API新增了独立的推理过程SSE事件，让前端能清晰区分“思考中”和“最终答案”，对构建更好的用户交互体验至关重要。| [View PR](https://github.com/NousResearch/hermes-agent/pull/22364)
- feat(chinese): 中文界面完整本地化 (PR #21997) - 一个大型PR提交，旨在为CLI、Banner、飞书等提供完整的中文界面支持，表明对中文社区和市场的重视。| [View PR](https://github.com/NousResearch/hermes-agent/pull/21997)

#### 7. 用户反馈摘要

从今日的Issue评论和报告中，可以提炼出用户的真实声音：

- **挫败感 (频繁的429限流):** 用户`herbalizer404`在#15895中描述“即便配额充足也遭遇429”，表达了因认证/限流机制不完善导致的挫败感。
- **理解与困惑并存 (凭证丢失、行为不一致):** 用户`arsitekberotot`在#19566中详细描述Codex凭证丢失的复杂场景，显示了用户对系统内部运作有一定理解，但对其不稳定感到困惑。用户`ddoKx`在#20465中发现CLI和Cron的故障转移行为不一致，这种“偶发性”Bug最令用户头疼。
- **强烈诉求 (工具功能缺失):** 用户`btorresgil`在#22352中指出，`discord_admin`工具集在文档中声称有“创建/编辑/删除频道”功能，但实际上并未实现。这种“承诺与兑现”的差距是用户不满的常见来源。
- **务实痛点 (特定平台集成):** 来自中国用户`qiyin-code`的#7266描述了阿里云（DashScope）端点的验证警告问题，虽然功能可用，但每次切换模型都看到警告，体验极差。

#### 8. 待处理积压 (呼吁维护者关注)

以下是一些长期存在、至今未有明确解决方案或进展停滞的重要Issue，可能影响项目信誉，建议项目维护者优先关注。

- **[Critical] [Bug]: Interactive CLI session does not auto-fallback on Codex 429 (#20465)**（创建时间: 2026-05-05）
  - **理由:** P1严重等级，揭示核心架构的路径问题，且至今无PR关联。用户社区对此关注度高。
  - **链接:** https://github.com/NousResearch/hermes-agent/issues/20465
- **[Major] [Bug]: google-gemini-cli causing 429 but gquota ok (#15895)**（创建时间: 2026-04-26）
  - **理由:** 评论数最多的问题，直接影响Gemini用户的正常使用。缺乏维护者的明确响应或解决方案。
  - **链接:** https://github.com/NousResearch/hermes-agent/issues/15895
- **[Major] [Bug]: Path.home() / ".hermes" bypasses get_hermes_home() in 23 production files (#18060)**（创建时间: 2026-04-30）
  - **理由:** 这是一个会破坏Docker部署和自定义`HERMES_HOME`环境的系统性Bug，涉及23个文件。虽然评论不多，但其严重性极高。需要维护者评估并统一修复。
  - **链接:** https://github.com/NousResearch/hermes-agent/issues/18060
- **[Warning] 大量PR积压（47条待合并）**
  - **理由:** 合并速度为(3/50)，长期积压一方面会打击贡献者热情，另一方面会使社区迭代的Bug修复（如已有PR的#22345和#22340）无法及时落地。**这可能成为项目的瓶颈。**
  - **示例链接 (待合并PR):** https://github.com/NousResearch/hermes-agent/pull/22345
  - **示例链接 (待合并PR):** https://github.com/NousResearch/hermes-agent/pull/21997

---

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 | 2026-05-09

---

## 1. 今日速览

过去 24 小时内，项目活跃度较高：共处理 **21 条 Issue**（新开/活跃 8，关闭 13）和 **23 条 PR**（待合并 18，合并/关闭 5），并发布了 1 个 nightly 版本。社区焦点集中在 **LM Studio 易用性需求**、**exec 工具安全守卫误报** 以及 **MCP Streamable HTTP 传输协议支持** 三大话题上。多个长期存在的 Bug（如图片识别、WhatsApp 通道缺陷）已通过 PR 修复或关闭，整体版本正向 **v0.2.9** 推进。

---

## 2. 版本发布

**nightly 构建 (v0.2.8-nightly.20260509.8508f806)**

- **变更日志**：https://github.com/sipeed/picoclaw/compare/v0.2.8...main
- **说明**：此版本为自动构建，可能不稳定，请谨慎使用。包含了自 v0.2.8 以来的 main 分支最新改动，涵盖 bug 修复和功能增强（如添加 Gemini Web Search Provider、MCP Web UI 配置等，详见下文项目进展）。
- **破坏性变更**：无标注，建议用户关注 [CHANGELOG] 及相应 PR 说明。

---

## 3. 项目进展

今日合并/关闭的 5 个 PR 推动了多个关键修复与功能增强：

| PR | 说明 | 关联 Issue |
|----|------|-------------|
| [#2655](https://github.com/sipeed/picoclaw/pull/2655) | **fix: restore verified unified kernel baseline** — 修复 unified-kernel 运行时的不变量，包括 securebus 执行一次语义、重做安全持久化、单行步骤记账等，由 @ZanzyTHEbar 提交 | — |
| [#2522](https://github.com/sipeed/picoclaw/pull/2522) | **fix(openai_compat): request stream usage** — 为 OpenAI 兼容提供商添加流式用量支持，仅对原生 OpenAI 底座启用 `stream_options.include_usage` | — |
| [#2128](https://github.com/sipeed/picoclaw/pull/2128) | **fix(tools): ensure tool parameters have valid JSON Schema properties field** — 修复严格 OpenAI 兼容 API（如 LM Studio）因缺少 `properties` 字段导致的工具架构验证错误 | [#2139](https://github.com/sipeed/picoclaw/issues/2139) |

此外，今日新提交的 PR 中，以下两个尤为关键：
- **[#2830](https://github.com/sipeed/picoclaw/pull/2830) fix(spawn): add async delivery policy for specialist results** — 为异步工具结果引入显式传递策略，避免子 agent 的结果被错误地重新注入父 agent，修复了 [#2829](https://github.com/sipeed/picoclaw/issues/2829)。
- **[#2826](https://github.com/sipeed/picoclaw/pull/2826) fix: resolve relative paths correctly in exec tool safety guard** — 修正 exec 工具中相对路径的解析逻辑，解决 `guardCommand` 误报问题（如 `curl wttr.in/Beijing?T` 被错误拦截），关联 [#2749](https://github.com/sipeed/picoclaw/issues/2749)。

项目整体在 **Agent 交互流程**、**Provider 兼容性**、**工具安全机制** 和 **Web UI 配置** 四个维度均有实质性推进。

---

## 4. 社区热点

| Issue | 标题 | 评论数 | 👍 | 关键诉求 |
|-------|------|--------|----|----------|
| [#28](https://github.com/sipeed/picoclaw/issues/28) | Feat Request: LM Studio Easy Connect | **18** | 2 | 用户希望提供一键式连接 LM Studio 的方法，降低非技术用户接入成本。 |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | [BUG] exec 工具的 guardCommand 方法问题 | **10** | 2 | 设置 `restrict_to_workspace=true` 后，不涉及路径的命令（如 `curl`）被误拦截，影响正常使用。已由 PR #2826 修复。 |
| [#2376](https://github.com/sipeed/picoclaw/issues/2376) | [Feature] Option to disable 'Enter' key from sending messages | **5** | 1 | Android 用户要求分离 Enter 键换行与发送功能，提升移动端输入体验。 |

**分析**：LM Studio 作为本地推理方案用户群体庞大，社区对其集成需求迫切（Issue 已存在约 3 个月，评论持续）。exec 工具安全守卫的误报问题严重干扰日常使用，因其影响范围广（涉及所有使用 bash 工具的自动化任务），获得快速修复。移动端输入体验的改进虽属小功能，但能显著提升 Android 用户满意度。

---

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug（含已关闭/修复的）：

| 严重性 | Issue | 摘要 | 状态 |
|--------|-------|------|------|
| **高** | [#2738](https://github.com/sipeed/picoclaw/issues/2738) | v0.2.8 升级后无法识别上传的图片（图片识别回归） | **已关闭**（修复已包含于 nightly 构建） |
| **高** | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | exec 工具安全守卫误报非路径命令（如 `curl`） | **有 fix PR #2826** |
| **中** | [#2674](https://github.com/sipeed/picoclaw/issues/2674) | OpenAI Codex OAuth 提供商返回空响应（ChatGPT 后端流式传输时） | **未修复** |
| **中** | [#2744](https://github.com/sipeed/picoclaw/issues/2744) | Android v0.2.8 无法访问任何标签页数据 | **未修复** |
| **中** | [#2785](https://github.com/sipeed/picoclaw/issues/2785) | ToolFeedbackAnimator 导致飞书通知中心仅显示第一个工具调用消息 | **未修复** |
| **低** | [#2540](https://github.com/sipeed/picoclaw/issues/2540) | whatsapp_native 通道因 LID 迁移导致消息静默丢失 | **已关闭**（含细节报告） |

**说明**：图片识别 Bug 已在 v0.2.8 发布后被快速定位并修复，体现了维护者对回归问题的响应速度。exec 工具安全守卫的 PR #2826 正在审查，预计很快合入。Codex OAuth 和 Android 标签页问题尚未有修复方案，需社区进一步协助排查。

---

## 6. 功能请求与路线图信号

| 方向 | Issue | 描述 | 关联 PR/状态 |
|------|-------|------|--------------|
| **Provider 扩展** | [#28](https://github.com/sipeed/picoclaw/issues/28) | LM Studio 一键连接 | 未有具体 PR，但社区讨论热烈，可能纳入后续版本 |
| **MCP 协议增强** | [#2782](https://github.com/sipeed/picoclaw/issues/2782) | MCP 客户端支持 Streamable HTTP 传输 | 无对应 PR，是新提出的需求，属于新一代 MCP 规范必备 |
| **Agent 交互改进** | [#2829](https://github.com/sipeed/picoclaw/issues/2829) | 异步工具结果显式传递策略 | **已有 fix PR #2830**，基本确定进入下一版本 |
| **WhatsApp 编译支持** | [#2625](https://github.com/sipeed/picoclaw/issues/2625) | 为 arm64 默认构建包含 WhatsApp 支持 | 无 PR，但社区呼声较高（1 👍） |
| **飞书通道优化** | [#2580](https://github.com/sipeed/picoclaw/issues/2580) | 流式输出、状态显示、提供商/模型信息 | 已关闭，但用户期望强烈（2 👍），可能成为后续迭代方向 |

**路线图信号**：从近期 PR 可以看出，项目组正在积极完善 **Agent 异步流程**（spawn 策略）、**Provider 兼容性**（Gemini Web Search、Bedrock 流式）、**Web UI 配置**（MCP 管理、模型配置工作流）等模块。社区对 **LM Studio**、**飞书**、**MCP Streamable HTTP** 的诉求是明显的空白点，预计会在 v0.3.x 中重点考虑。

---

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实声音：

- **@icyfire**（[#1042](https://github.com/sipeed/picoclaw/issues/1042)）：_“查询北京的天气，执行 `curl -s "wttr.in/Beijing?T"` 被安全守卫拦截，报 `../../../../Beijing?T` 相对路径错误，而这个命令根本不涉及任何路径。”_ → 暴露了路径正则判断过于粗暴的问题。
- **@axwfae**（[#2738](https://github.com/sipeed/picoclaw/issues/2738)）：_“升级到 v0.2.8 后，上传的图片无法被识别！”_ → 回归问题严重影响图像多模态场景。
- **@xpader**（[#2785](https://github.com/sipeed/picoclaw/issues/2785)）：_“设置 `separate_messages=false` 时，飞书通知中心只显示第一个工具调用消息。”_ → 工具反馈动画的逻辑缺陷影响用户体验。
- **@stl3**（[#2744](https://github.com/sipeed/picoclaw/issues/2744)）：_“Android v0.2.8 无法从任何标签页访问数据。”_ → 移动端基本功能受阻，需紧急排查。
- **@wowowowowowowowonojieba**（[#2580](https://github.com/sipeed/picoclaw/issues/2580)）：_“中国用户占比很大，希望优化飞书插件，参考飞书官方 OpenClaw 插件，实现流式输出、显示用时和模型信息。”_ → 体现了对极简本地化体验的期待。

---

## 8. 待处理积压

以下为长期未被关闭或长时间无官方回应的重要 Issue/PR，建议维护者重点关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 说明 |
|------|------|------|----------|----------|------|
| Issue | [#28](https://github.com/sipeed/picoclaw/issues/28) | Feat Request: LM Studio Easy Connect | 2026-02-11 | 2026-05-08 | 评论 18 条，社区需求强烈，但长期无开发进展 |
| Issue | [#1042](https://github.com/sipeed/picoclaw/issues/1042) | exec 工具 guardCommand 方法问题 | 2026-03-04 | 2026-05-08 | 尽管已有 PR #2826，但尚未合入 main 分支 |
| Issue | [#2674](https://github.com/sipeed/picoclaw/issues/2674) | Codex OAuth: empty assistant response | 2026-04-26 | 2026-05-08 | 影响 ChatGPT 后端用户，3 个 👍，无修复 PR |
| PR | [#2158](https://github.com/sipeed/picoclaw/pull/2158) | feat(agent): Multi-agent discovery prompt | 2026-03-29 | 2026-05-09 | 已有 30+ 天未合入，涉及多 Agent 发现机制 |
| PR | [#2270](https://github.com/sipeed/picoclaw/pull/2270) | fix(config): handle non-addressable SecureString | 2026-04-02 | 2026-05-08 | 修复配置序列化 panic，等待审查 |
| PR | [#2239](https://github.com/sipeed/picoclaw/pull/2239) | modify docker compose with privileged | 2026-04-01 | 2026-05-08 | Docker 部署权限优化，低优先级但可提升易用性 |

**建议**：优先推进 **LM Studio 连接**的讨论形成设计方案，合并 **exec 安全守卫** 和 **Config panic** 修复，并评估 **Codex OAuth** 空响应问题的排查路径。

---

*本日报基于 GitHub 公开数据自动生成，所有链接直接指向对应 Issue/PR。项目地址：[sipeed/picoclaw](https://github.com/sipeed/picoclaw)*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于提供的 GitHub 数据生成的 NanoClaw 项目动态日报。

---

### **NanoClaw 项目动态日报 | 2026-05-09**

**分析师点评：** 项目处于高活跃度状态。今日修复工作围绕核心的**服务稳定性**与**部署体验**展开，社区贡献活跃，尤其体现在对 SIGTERM 优雅关闭问题的快速响应上。同时，基础设施层面的 **Kubernetes 集成**和**配置管理数据库化**等特性 PR 正在推进，表明项目正从单机部署向更大规模、更健壮的方向演进。

---

### 1. **今日速览**

今日 NanoClaw 项目维护活动非常活跃。核心开发者在**24小时内合并了5个重要 PR**，其中紧急修复了**SIGTERM 信号导致会话回复丢失**的关键 Bug，显著提升了服务在高频重启/升级场景下的可靠性。社区贡献方面，已有**12个 PR 处于待合并状态**，涵盖 Kubernetes 运行时、数据库化配置等重要特性。同时，两个用户报告的 Bug (`#2360` 脚本静默删文件、`#2355` 升级后 CLI 不在 PATH) 直接暴露了当前版本在**用户体验**和**安全防护**上的短板，需要团队优先关注。

### 2. **版本发布**

*无新版本发布。*

### 3. **项目进展**

今日项目在 **稳定性、可部署性和基础设施**方面取得了显著进展。

- **核心稳定性修复**：社区成员 `Joi` 贡献了两个关键的优雅关闭修复，并被迅速合并：
    - **`[已合并] fix(shutdown): drain in-flight dispatchResponse on SIGTERM (#2359)`**：修复了另一个由 SIGTERM 信号导致的“即发即忘”动作未完成的竞态条件问题。
    - **`[已合并] fix(shutdown): drain in-flight routeInbound before exit (#2358)`**：解决了 SIGTERM 信号会在处理消息过程中导致回复被丢弃的根本性 Bug。这是继 2月版本后，对服务优雅关闭机制的重要补充。
- **基础设施现代化**：
    - **`[已合并] feat(intake): 用 `messaging_groups` 表的 `auto_url_intake` 列替换环境变量白名单 (#2357)`**：将 URL 摄入功能的权限控制从环境变量迁移到了数据库，为更细粒度的、基于频道组的配置管理铺平了道路。
    - **`[已合并] feat(cli): 添加 `ncl` 管理 CLI (#2350)`**：新增了 `ncl` 命令行工具，允许管理员通过 Unix Socket 直接查询和修改中央数据库，极大方便了运维管理和调试。

### 4. **社区热点**

今日社区讨论的焦点集中在 **部署体验缺陷**和 **功能请求**上。

- **`#2360 - [OPEN] Setup script silently deletes existing groups/*/CLAUDE.md`**：该 Issue 虽仅有0条评论，但性质严重。用户 `alexli-77` 指出 `bash nanoclaw.sh` 脚本会静默删除用户自定义的代理配置文件，且无任何备份或警告。此问题极易导致用户数据丢失，引发社区强烈不满是迟早的事。
- **`#2355 - [OPEN] bug(update-nanoclaw): `ncl` not added to PATH`**：用户 `glifocat` 提出了一个关于升级流程的 Bug。通过 `/update-nanoclaw` 升级到 2.0.45+ 版本后，新安装的 `ncl` CLI 工具并未被添加到 `~/.local/bin` 路径下，导致用户无法直接使用。社区成员已提交了对应的修复 PR (`#2356`)，展现了快速响应能力。
- **`#2354 - [OPEN] feat: Kubernetes container runtime for agent spawning`**：用户 `netadmincmh-hash` 提出的功能请求获得了关注。该需求旨在支持将代理容器直接调度到 Kubernetes 集群上，而非仅限本地 Docker，这反映了企业级用户对容器编排和资源管理的需求。

### 5. **Bug 与稳定性**

今日报告的 Bug 主要影响数据持久化和部署流畅度，部分已有修复方案。

- **严重：数据持久化**
    - **`#2194 - [OPEN] WhatsApp LID→phone JID mapping not persisted across restarts`**：这是一个影响 WhatsApp 通道路由的长期 Bug。重启服务后，LID 到手机号的映射丢失，导致基于 LID 的消息路由失败。**目前仍在开放中，未有修复 PR。**
- **高危：数据丢失**
    - **`#2360 - [OPEN] Setup script silently deletes existing groups/*/CLAUDE.md without warning or backup`**：设置脚本会静默删除用户自定义配置文件。此 Bug 可能导致用户数小时的配置工作付诸东流。**暂无修复 PR。**
- **中危：功能缺陷**
    - **`#2355 - [OPEN] bug(update-nanoclaw): `ncl` not added to PATH`**：升级后 CLI 工具不可用，影响运维。**已有对应修复 PR (`#2356`)。**
    - **`#2196 - [已关闭] host-sweep: deleteOrphanProcessingClaims crashes with 'attempt to write a readonly database'`**：清扫任务因只读数据库连接而崩溃的问题已在今日被修复关闭。
- **稳健性增强**
    - 今日合并的 **`#2358`** 和 **`#2359`** 修复了 SIGTERM 信号竞态问题，属于高价值的稳定性改进。
    - 待合并的 **`#2352`** 提升了构建超时时间（5分钟 → 15分钟），避免慢网络环境下的构建失败。

### 6. **功能请求与路线图信号**

今日涌现的功能请求和提交的 PR 清晰地描绘了项目向**基础设施即代码**和**企业级部署**演进的路线图。

- **Kubernetes 集成**：`#2354` 请求支持 Kubernetes 运行时，这可能是下一个小版本的**最大亮点特性**。它标志着 NanoClaw 从一个“个人助理”工具向可管理的“平台服务”转变的重要一步。
- **配置管理数据库化**：多个 PR (如 `#2357`、`#2351`) 正在将容器配置和功能开关从文件系统/环境变量迁移到数据库。这暗示了项目下一阶段将提供**更灵活的、可编程的、运行时可调整的配置能力**，为未来的 Web UI 或管理 API 铺平道路。
- **未知命令处理优化**：`#2346 PR` 修复了未知斜杠命令被静默丢弃的问题。这表明项目正在打磨与 Claude Code 的交互细节，提升用户的命令行使用体验。

### 7. **用户反馈摘要**

从 Issue 和 PR 的评论中可以提炼出以下用户痛点：

- **“我的配置去哪了？”**：`#2360` 的提交者 `alexli-77` 显然经历了痛苦，他/她直接指出了 `nanoclaw.sh` 脚本在重新运行时会破坏用户已有的精心配置。这反映了用户对开发环境稳定性和数据安全性的基本诉求。
- **“升级后 CLI 用不了？”**：`#2355` 的用户 `glifocat` 反馈了升级后的尴尬处境，他/她虽然提供了解决方案的 PR，但也暗示了当前的升级流程缺乏充分的自动化测试，容易遗漏对 `PATH` 等系统环境变量的处理。
- **“慢网络下容器构建总失败”**：`#2352` 的 PR 作者 `Shlomog` 通过提升超时时间来修复 `install_packages` 在慢网络下的 `ETIMEDOUT` 错误。这反映了用户在不同网络环境下部署时面临的现实挑战。

### 8. **待处理积压**

以下为长期未更新时间较长，但仍具有重要价值的问题或 PR，值得维护者关注：

- **`[开放] #1917, #1913 - fix: rename @Andy trigger references`**：这两个 PR 由 `boskodev790` 于4月22日提交，旨在修复 `@Andy` 触发词在修改助手名称时未被更新的问题。尽管需要代码审查，但对多代理、自定义命名的用户场景至关重要。
- **`[开放] #1916 - fix: guard numeric config env vars against NaN`**：同样是 `boskodev790` 提交的，为 `CONTAINER_TIMEOUT` 等环境变量增加了数值有效性校验。这是一个提升配置健壮性的好实践，应尽快合并。
- **`[开放] #1912 - fix: handle empty container stdout with clear error`**：旨在提供更清晰的错误信息。该 PR 虽有清晰的描述，但自4月22日以来未有任何评论或活动，可能需要维护者主动推进。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 NullClaw 项目的 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 2026-05-09 项目动态日报。

---

# NullClaw 项目动态日报 | 2026-05-09

## 1. 今日速览

今日 NullClaw 项目处于**中等活跃**状态。项目发布了最新的 Nightly 构建版本，持续进行自动化交付迭代。社区提交了 2 个新的 Issue，均指向较为关键的 Bug，特别是 Telegram 频道配置识别错误和安全监督模式的回退问题，可能影响用户的核心体验和安全策略。Pull Request 方面，一个关于数据治理层的重要特性 PR 仍在等待审查，而一个关于自动化发布流程的 CI 改进 PR 已被合并，显示出项目在基础设施上的持续优化。

- **活跃度评估**：中等。Issue 和 PR 数量正常，但 Bug 报告指向关键路径，需要维护者重点关注。
- **关键动态**：发现两个影响核心功能和安全模型的 Bug；CI 自动化流程取得进展。

## 2. 版本发布

### nullclaw Nightly 2026-05-09
- **版本号**: `nightly-20260509-5d533da`
- **发布时间**: 2026-05-09 03:34:22 UTC
- **关联 Commit**: `5d533da90dd0986edf190247c27655f969bdcb7d`
- **变更摘要**: 本次 Nightly 发布由 CI 流程自动触发，实际上包含了对上一个 CI 改进 PR (#899) 的成果验证。该版本主要目标是为用户提供最新的开发中构建，供测试和验证。
- **破坏性变更**: 无。Nightly 版本为滚动预发布版，不保证稳定性和向后兼容性，仅供测试用途。
- **迁移注意事项**: Nightly 版本不建议用于生产环境。请谨慎更新，并在更新前备份配置文件。

## 3. 项目进展

今日合并了一个重要的 CI 流程优化 PR，推动了项目的持续交付能力：

- **✅ [CLOSED] PR #899 - ci: publish nightly prerelease**
  - **作者**: DonPrus
  - **摘要**: 此 PR 启用了 Nightly 构建的自动发布功能。它修改了可复用的 `nullbuilder` 工作流，使其在调度触发时能自动将构建产物发布为一个名为 “NullClaw Nightly” 的预发布版本。
  - **项目意义**: 标志着 NullClaw 的**自动化发布流程已经跑通**。从今日发布的 Nightly 版本来看，该 PR 已成功生效。这为未来实现更频繁、更稳定的版本迭代奠定了基础，减少了手动发布的工作量和出错风险。

此外，一个关于数据治理层的特性 PR (#885) 仍在开放中，未取得实质性进展。

## 4. 社区热点

今日新提交的两个 Issue 虽然暂无评论反馈，但因其问题的严重性，预计将成为社区关注的焦点：

- **Issue #901 - `channel list` always shows "not configured" for telegram**
  - **链接**: [Issue #901](https://github.com/nullclaw/nullclaw/issues/901)
  - **核心诉求**: 用户报告了一个**严重的功能阻断性 Bug**。即使 `config.json` 中 Telegram 配置正确且 `nullclaw config` 命令也能正确显示，但 `nullclaw channel list` 和 `nullclaw channel start telegram` 命令均无法识别此配置，导致 Telegram 频道完全无法使用。这直接影响了依赖 Telegram 进行交互的用户。
  - **分析**: 该 Bug 疑似出现在配置加载与频道状态检测之间的逻辑层，可能是解析或缓存机制存在缺陷。这种“配置显示正确但功能检测失败”的现象是典型的配置验证问题，需要立即排查。

- **Issue #900 - `approval_request` defined in spec but never emitted**
  - **链接**: [Issue #900](https://github.com/nullclaw/nullclaw/issues/900)
  - **核心诉求**: 用户指出，在 `webchannel_v1` 规范中定义的、用于高风险命令审批的“请求-响应”双向通信机制，其核心的 `approval_request` 事件**从未被实际发出**。这导致监督模式在遇到风险命令时，不是弹出审批窗口，而是直接静默失败。
  - **分析**: 这是一个**安全模型上的严重设计实现缺陷**。规范有定义，安全策略层也为此预留了接口，但核心逻辑却“忘记”了触发该流程。这不仅是一个 Bug，也是一个潜在的合规与安全问题，因为用户期望的“审批”护城河实际上不存在。

## 5. Bug 与稳定性

今日报告了 2 个新 Bug，均未关联修复 PR。

| 严重程度 | Issue | 描述 | 状态 | 潜在影响 |
| :--- | :--- | :--- | :--- | :--- |
| **严重** | [#901](https://github.com/nullclaw/nullclaw/issues/901) | Telegram 频道配置无法被 `channel list` 和 `channel start` 命令正确识别。 | 未修复 | 核心功能阻断，Telegram 用户完全无法使用。 |
| **中等** | [#900](https://github.com/nullclaw/nullclaw/issues/900) | 监督模式下的审批请求 (`approval_request`) 事件从未被发出。 | 未修复 | 安全特性失效，高风险命令在监督模式下可能被静默拒绝或执行非预期操作。 |

**总结**: 今日无稳定性和崩溃类 Bug，但两个功能性 Bug 一个影响核心使用路径（Telegram），一个影响安全保障机制，均需优先处理。

## 6. 功能请求与路线图信号

- **数据治理层 (Data Governance Layer)**: PR [#885](https://github.com/nullclaw/nullclaw/pull/885) 作为 Hackathon 项目提交，旨在为 NullClaw 增加一个数据治理层。虽然该 PR 仍在 Draft 状态且待审查，但它反映了社区对**数据隐私、合规和控制**的需求。如果被合并，这将是项目路线图中一个重要的里程碑，可能为记忆管理等功能提供更精细的权限和生命周期控制。

- **监督模式完善**: Issue [#900](https://github.com/nullclaw/nullclaw/issues/900) 的提出，本质上是用户对**安全功能完整性和可用性**的强烈需求。解决此问题后，监督模式才能真正发挥作用，这将增强用户对 AI Agent 执行高风险操作的信心。可以预见，该功能将是下一个版本的重点。

## 7. 用户反馈摘要

由于今日报告的 Issue 尚无评论，我们从描述中提取了用户的核心反馈：

- **痛点 (Issue #901)**: “我的配置明明是正确的，工具也验证通过了，为什么核心功能就是不能用？” 这暴露了**配置验证与功能模块之间的状态不同步**问题，给用户带来极大的困惑和挫败感。用户可能因此怀疑是自身配置问题，从而浪费大量调试时间。
- **痛点 (Issue #900)**: “按照规范，应该有个审批弹窗，但它完全没有出现，命令直接就失败了。” 这说明**用户期望的交互流程与实际的代码实现存在巨大落差**。对于依赖监督模式来管理风险的专业用户来说，这是一个无法接受的安全疏漏，可能会降低他们对整个项目安全设计的信任度。

## 8. 待处理积压

- **PR #885 - feat(memory): Add NullClaw Data Governance Layer**
  - **链接**: [PR #885](https://github.com/nullclaw/nullclaw/pull/885)
  - **状态**: OPEN (Draft)
  - **创建时间**: 2026-05-04
  - **最近更新**: 2026-05-09
  - **问题**: 此 PR 已开放 **6 天**，且为 Draft 状态，未收到维护者的评审意见。这是一个来自 Hackathon 的、规模较大的特性提交，长期处于无人响应的状态可能会打击贡献者的积极性。如果该项目有意义，建议维护者尽快安排审查，明确是否采纳及后续修改方向。

- **Issue #900 - `approval_request` defined in spec but never emitted**
  - **链接**: [Issue #900](https://github.com/nullclaw/nullclaw/issues/900)
  - **状态**: OPEN
  - **创建时间**: 2026-05-09
  - **问题**: 虽然该 Issue 是今日新提交的，但因为其直接关系到项目的**安全核心逻辑**，维护者应将其视为高优先级事项。如果未能在下一个版本或 Hotfix 中修复，随着更多用户采用监督模式，该问题可能成为项目的一个负面口碑点。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，各位关注 IronClaw 项目的朋友们，早上好。今天是 2026 年 5 月 9 日，欢迎阅读今日的项目动态日报。

过去 24 小时，项目代码与讨论极为活跃。核心开发团队围绕代号“Reborn”的新一代架构展开了密集攻关，提交了大量 PR 并创建了紧密耦合的追踪 Issues。与此同时，社区贡献者也在积极完善功能与修复 Bug，展现了项目生态的蓬勃活力。

---

### **IronClaw 项目动态日报 — 2026-05-09**

#### **1. 今日速览**

过去 24 小时，项目处于高强度开发状态，核心聚焦于“Reborn”新架构的落地。共有 12 个新 Isssues 被创建，其中 11 个直接服务于 Reborn 架构的深度开发。PR 活动尤为密集，共处理 45 个 PR，其中 18 个已被合并或关闭，显示了出色的交付力。尽管 Nightly E2E 测试出现一次失败，但团队已迅速响应。总体上，项目正以前所未有的速度向下一阶段迈进，健康度极高。

#### **2. 版本发布**

无新版本发布。

#### **3. 项目进展**

今日合并/关闭的关键 PR 显著推进了项目核心架构，尤其是在“Reborn”模块的底层能力建设上：

- **Reborn 运行时与持久化层**：
    - [PR #3401](https://github.com/nearai/ironclaw/pull/3401) 与 [PR #3408](https://github.com/nearai/ironclaw/pull/3408) 被合并，为 Reborn 子项目增加了**持久化凭证存储**和**加密功能**，这是支撑安全可靠 Agent 运行的关键基础。
    - [PR #3405](https://github.com/nearai/ironclaw/pull/3405) 被合并，添加了**循环驱动注册表与就绪性校验**层，为不同类型的 Agent 运行模式提供了可插拔的驱动框架。
    - [PR #3403](https://github.com/nearai/ironclaw/pull/3403) 被合并，实现了**生产级循环模型网关**，完成了 Reborn 中 LLM 调用路径的核心适配。
    - [PR #3397](https://github.com/nearai/ironclaw/pull/3397) 被合并，开始在循环支持端口中**发射模型与转录里程碑事件**，为后续的监控和调试铺平了道路。

- **修复与完善**：
    - [PR #3366](https://github.com/nearai/ironclaw/pull/3366) 被合并，这是一个大型修复，实现了**在授权门解决后自动恢复暂停的 Mission**，显著提升了用户体验，解决了用户长期反馈的痛点。
    - [PR #3413](https://github.com/nearai/ironclaw/pull/3413) 被合并，为 Reborn 的循环检查点状态**添加了暂存存储**，是状态管理的重要一环。

这些合并操作标志着 Reborn 架构中“凭证管理”、“循环驱动”和“状态管理”三大基石已经初步成型，项目整体正在稳步地从概念验证走向生产可用。

#### **4. 社区热点**

今日的讨论焦点高度集中在 **Reborn 架构的实现细节**与**核心功能 Bug**上。

- **最受关注 Issue**：
    - **[#3067](https://github.com/nearai/ironclaw/issues/3067) [Reborn] 添加垂直切片集成测试套件**：以 32 条评论领先，开发者社区正在热烈讨论如何为 Reborn 设计全面且有效的集成测试，以确保新架构的稳定性。这体现了社区对代码质量的严谨追求。
    - **[#3016](https://github.com/nearai/ironclaw/issues/3016) [Reborn] 添加 AgentLoopHost 门面**：评论 11 条，是 Reborn 架构中的核心组件，其设计直接影响到 Agent 的执行模型，讨论热度不减。

- **最受关注 PR**：
    - **[PR #3331](https://github.com/nearai/ironclaw/pull/3331) feat(web): 优化非图片附件 UI 并持久化用户附件**：由社区贡献者 `italic-jinxin` 提交，虽无评论数，但其“UX”和“agent”标签表明这是增强 Web 网关用户体验的重要功能，社区期待度较高。
    - **[PR #2394](https://github.com/nearai/ironclaw/pull/2394) feat: 企业微信渠道**：由 `hanakannzashi` 贡献，持续超过一个月，正在逐步完善。这表明社区对**多渠道商业应用场景**有强烈需求。

**分析**：社区的核心注意力集中在两条线上：一是核心开发者主导的、决定项目未来的 Reborn 架构；二是社区贡献者驱动的、直接影响用户日常体验的功能（如 UI 优化、新渠道接入）。两者并行发展，项目生态健康。

#### **5. Bug 与稳定性**

今日报告了一个系统级 Bug 和一个功能性 Bug：

- **【严重】** **[Issue #3323](https://github.com/nearai/ironclaw/issues/3323) Nightly E2E 测试失败**：由自动化机器人报告，涉及 `Full E2E / E2E (web-regressions)` 工作流。这是一个关键的代码质量门禁失败，优先级高，维护者需立即调查。
- **【重要】** **[Issue #3415](https://github.com/nearai/ironclaw/issues/3415) Bug: Mission 结果发布到错误的会话**：由用户 `sunglow666` 报告，属于典型的业务逻辑 Bug，会严重影响用户对 Mission 功能的信任度。目前无关联 PR 和评论，需尽快确认。

#### **6. 功能请求与路线图信号**

今日的功能请求几乎完全被 Reborn 架构的推进所覆盖，这本身就是最强烈的路线图信号。

- **核心路线图信号**：大量以 `[reborn]` 标签创建的 Issues，如 [#3410](https://github.com/nearai/ironclaw/issues/3410) (V2引擎驱动模型适配器)、[#3409](https://github.com/nearai/ironclaw/issues/3409) (循环提示包)、[#3407](https://github.com/nearai/ironclaw/issues/3407) (纯文本AgentLoopDriverHost工厂) 等，清晰地勾勒出 Reborn 作为未来架构的完整技术路径。这证实了 Reborn 是项目当前和未来一段时间内的绝对核心任务。
- **社区功能请求**：
    - **[PR #1378](https://github.com/nearai/ironclaw/pull/1378) feat(routing): 按渠道的 MCP 和内置工具过滤**：这个大型 PR 已开放近两个月，仍在更新中。它旨在解决多渠道部署下的工具可见性问题，是一个重要的企业级功能，预计会与 Reborn 架构结合。
    - **[PR #2394](https://github.com/nearai/ironclaw/pull/2394) feat: 企业微信渠道**：如前所述，社区对集成中国企业通信软件有强烈需求，该功能是项目拓展中国市场的重要一步。

**判断**：下一版本（可能代号 `v0.29.0`）预计将深度集成 Reborn 架构的核心组件，同时很可能包含 Web UI 优化、企业微信渠道等社区贡献的功能。

#### **7. 用户反馈摘要**

从社区讨论中可以提炼出以下几点用户声音：

- **正面反馈**：对项目的高速迭代表示赞赏，社区贡献者积极参与 Reborn 等核心功能的讨论，体现了对项目前景的信心。
- **痛点反馈**：用户 `sunglow666` 报告的 **[#3415](https://github.com/nearai/ironclaw/issues/3415)** 问题直接指向了 Mission 功能的严重逻辑错误，这是目前用户最迫切的痛点。此外，Nightly E2E 测试的失败也可能成为开发者的阻塞点。
- **使用场景**：从 PR [#3331](https://github.com/nearai/ironclaw/pull/3331) (非图片附件) 和 [#2394](https://github.com/nearai/ironclaw/pull/2394) (企业微信) 可以看出，用户正在将 IronClaw 应用于更丰富的交互场景（文件处理）和更严苛的商业环境（企业IM）。

#### **8. 待处理积压**

以下是为长期开放或未响应的重要 Issue/PR，建议维护团队关注：

- **长期未合入的社区贡献**：
    - **[PR #1378](https://github.com/nearai/ironclaw/pull/1378) feat(routing): 按渠道的 MCP 和内置工具过滤**：此大型 PR 开放已超 1.5 个月，作者 `nick-stebbings` 持续更新。鉴于 Reborn 架构可能对路由模块有影响，需要核心团队评估其与 Reborn 的集成方案，避免社区工作与主线脱节。
    - **[PR #2394](https://github.com/nearai/ironclaw/pull/2394) feat: 企业微信渠道**：同样是一个长期开放的 PR，需要推动代码审查，确保其与核心 `channel` 模块的兼容性。

- **高优先级未处理 Bug**：
    - **[Issue #3415](https://github.com/nearai/ironclaw/issues/3415) Bug: Mission 结果发布到错误的会话**：作为影响核心业务逻辑的 Bug，应尽快分配资源进行复现和修复。

---
**总结**：IronClaw 正处于一个关键的架构升级期，开发节奏快，协作有序。对于社区用户而言，建议关注 Reborn 相关讨论和随后的版本发布；对于潜在的贡献者而言，修复 Bug [#3415](https://github.com/nearai/ironclaw/issues/3415) 或推进 PR [#1378](https://github.com/nearai/ironclaw/pull/1378) 将是极佳的切入点。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 LobsterAI GitHub 数据，为您生成 2026-05-09 的项目动态日报。

---

## LobsterAI 项目动态日报 | 2026-05-09

### 1. 今日速览

今日项目处于 **高活跃度** 状态。核心开发团队正紧锣密鼓地将多个待合并的功能与修复推入主分支，过去24小时内高效合并/关闭了 **16个** Pull Request，显示出强大的交付能力。尽管新版本发布暂歇，但社区反馈的两个UI体验问题（#1920, #1921）受到了关注，并已有对应的PR（#1769, #1770）在等待合并，反馈闭环高效。整体项目健康度良好，代码库正在经历一波集中的质量改进与功能增强。

### 2. 版本发布

- 无最新版本发布。

### 3. 项目进展

今日项目取得了显著进展，一系列重要功能与修复已完成合并，标志着项目正从功能开发阶段向稳定性和体验优化阶段迈进。

**主要合并/关闭 PR 回顾：**

- **重大功能重构**：
    - **代码块渲染升级**：`#1922` 将 #1306 的 `CodeMirror 6` 重写方案合并至版本分支。这是一个里程碑式的PR，全面替换了旧的 `react-syntax-highlighter`，为代码块带来了语法高亮、搜索、行号、折叠、全屏查看等强大能力，极大提升了开发者在聊天中阅读代码的体验。
    - **收藏功能落地**：`#1664`（书签功能）被合并。该功能允许用户为聊天消息添加星标收藏，并通过侧边栏独立页面快速跳转，提升了信息管理与检索效率。
    - **UI一致性增强**：
        - `#1919` 将表单必填字段标记功能（红色 `*` 标记）合并至版本分支，解决了用户因不清楚必填项而提交失败的痛点。
        - `#1931` 更新了文件列表图标，`#1926` 调整了预览中文件列表的显示样式，共同优化了界面细节。

- **关键Bug修复**：
    - **重要稳定性修复**：`#1923` 合并了一个关键的conwork修复，该PR解决了用户点击“停止”会话后，爬虫等工具仍被“自动审批”机制继续执行的严重问题。这是一个对用户体验和资源控制至关重要的修复。
    - **其他修复**：
        - `#1918` 修复了会话中错误显示“NO_REPLY”文本的问题。
        - `#1925` 修复了预览文件重复和有效性的问题。
        - `#1927` 修复了当缓存读取值为零时仍会显示无关信息的问题。

- **其他优化**：
    - `#1924` 完成了Agent列表布局的优化。
    - `#1928` 优化了侧边栏UI。
    - `#1929` 完成了本地Agent头像的清理工作。
    - `#1930` 升级了 `penclaw-weixin` 依赖版本。

### 4. 社区热点

今日社区讨论主要围绕新提交的 UI 反馈，虽然评论数不多，但指向明确，反映了用户对用户体验细节的一致性追求。

- **最活跃 Issue**：
    - **#1920 [UI] Cowork initialization shows blank loading state instead of skeleton screen**：用户 `xiaoye5200` 指出，在Cowork初始化时，应用显示静态的“Loading...”文本，相比于项目其他地方的骨架屏动画，体验糟糕。这是一个明确的体验优化诉求，已获得开发者的关注。
        - [Issue #1920](https://github.com/netease-youdao/LobsterAI/issues/1920)

- **最受关注 PR**：
    - **#1769 [area: renderer, area: cowork] feat(ui): add skeleton loading screen for cowork initialization**：该PR正是为了解决 #1920 问题而提出。它已经存在了近三周，是一个待合并的状态。今天用户再次提出Issue，实际是对该PR尽快合并的一种侧面呼吁。
        - [PR #1769](https://github.com/netease-youdao/LobsterAI/pull/1769)

**分析**：社区用户对UI细节的一致性有很高要求，不希望项目中出现“参差不齐”的体验。`xiaoye5200` 连续提交两个关于“空状态”和“加载状态”的Issue，表明该用户对项目UI有深入使用和观察，其诉求代表了要求更高的用户体验诉求。

### 5. Bug 与稳定性

今日未报告新的严重Bug，但合并了几个对稳定性影响较大的修复。

| 严重程度 | 问题摘要 | Issue/PR 链接 | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | 停止会话后，爬虫等工具仍可能被“自动审批”继续执行 | [PR #1923](https://github.com/netease-youdao/LobsterAI/pull/1923) | **已合并** |
| **中** | 会话中错误显示“NO_REPLY”文本 | [PR #1918](https://github.com/netease-youdao/LobsterAI/pull/1918) | **已合并** |
| **低** | 缓存读取值为零时，UI上显示无关信息 | [PR #1927](https://github.com/netease-youdao/LobsterAI/pull/1927) | **已合并** |
| **低** | 预览文件列表出现重复和无效项 | [PR #1925](https://github.com/netease-youdao/LobsterAI/pull/1925) | **已合并** |

### 6. 功能请求与路线图信号

今日新提交的Issue明确指向了UI体验的进一步优化，且与已有PR高度吻合，说明社区反馈正有效转化为开发任务。

- **信号：UI 体验一致性**
    - **Issue #1920**（空白加载状态）和 **Issue #1921**（空状态占位符）共同指向一个核心诉求：提升UI细节的一致性，消除“毛坯感”。
    - **路线图判断**：由于这两个Issue均有对应的 **待合并PR**（#1769, #1770），可以判断这些改进很可能被纳入下一个正式版本中。这表明项目短期内的优化重点之一是UI交互细节。

### 7. 用户反馈摘要

- **对空白加载状态的反馈**：用户 `xiaoye5200` 通过Issue #1920 表达了使用Cowork初始化时，看到静态“Loading...”文字感到不适。用户认为这种“空白加载”体验是“刺眼的”，与项目通常采用的动态骨架屏风格不一致，是“感觉未完成”的表现。
- **对空状态占位符的反馈**：用户 `xiaoye5200` 在Issue #1921 中批评了 Skills Manager 和 TaskRunHistory 页面的空状态。这些页面在无内容时仅显示极简文本，没有图标和描述性副标题，用户认为这看起来“未完成”，与其他页面（如会话列表）的丰富空状态设计形成鲜明对比。

### 8. 待处理积压

以下是对项目发展有重要影响，但尚未得到响应的 PR，值得项目维护者重点关注。

- **[OPEN] [area: renderer] feat(ui): enhance empty states for skills and task run history (PR #1770)**
    - **关联 Issue**: #1921
    - **积压时间**: 19天
    - **分析**: 该PR与今日新提交的Issue #1921 直接相关，旨在为Skills Manager和TaskRunHistory页面添加更丰富的空状态。用户再次提交Issue，表明社区对此功能有较高期待。建议尽快审查并合并。
    - [PR #1770](https://github.com/netease-youdao/LobsterAI/pull/1770)

- **[OPEN] [area: renderer, area: cowork] feat(ui): add skeleton loading screen for cowork initialization (PR #1769)**
    - **关联 Issue**: #1920
    - **积压时间**: 19天
    - **分析**: 与上一条类似，该PR直接对应今日新提交的Issue #1920。这是一个典型的用户体验优化，且社区呼声很高。建议优先安排审查和合并。
    - [PR #1769](https://github.com/netease-youdao/LobsterAI/pull/1769)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

## Moltis 项目动态日报（2026-05-09）

### 1. 今日速览

过去24小时内，Moltis项目未处理新的Issue，但Pull Request活跃度较高，共有5条PR更新，其中2条已合并/关闭（主要为功能优化和本地化更新），另有一条新版本发布。项目核心贡献者 `penso` 动作密集，同时推进了Web UI重构、文档站点替换和外部代理持久化会话等多项功能。整体来看，项目处于**开发活跃期**，社区反馈信号偏弱，但功能推进节奏稳健。

### 2. 版本发布

- **20260508.01**  
  新版本于2026-05-08发布，版本号对应日期标记。目前发布信息较为简略，推测为日常滚动发布，包含近期合并的PR改进（如zh-TW本地化更新、语音模型引导、Web Composer相关修正）。  
  ⚠️ **破坏性变更/迁移注意事项**：当前未披露显著的破坏性变更。请开发者注意，若使用自定义Web Composer样式或Docs部署方案，可能需要适配新的Astro站点和UI组件。

### 3. 项目进展

过去24小时合并/关闭的PR推动了以下方向的进展：

- **国际化全面升级** —— `PR #986 [CLOSED]` 由社区贡献者 `PeterDaveHello` 提交，完善了台湾繁体中文（zh-TW）的UI翻译，尤其在“AI 助理”、术语一致性等方面做了系统梳理。表明项目开始对社区地区化进行精细打磨。
- **语音功能向产品化迈进** —— `PR #984 [CLOSED]` 由 `penso` 贡献，增加了OpenAI STT模型（包括whisper）和Realtime模式提示，并引入了Playwright测试覆盖。语音配置的用户引导和健壮性得到显著提升。
- **Web Composer重新设计进行中** —— `PR #985 [OPEN]` 对聊天输入框进行了完全重设计，以居中圆角Composer为核心，集成了模型选择、推理、附件、语音及发送按钮，并加入了token/上下文状态指示。UI/UX设计进入新阶段。
- **文档基础设施迁移** —— `PR #987 [OPEN]` 计划将mdBook部署路径替换为Astro站点，并保留原有Markdown源文件和URL结构。这将是项目文档系统的一次彻底升级，提升可维护性与用户体验。
- **外部代理持久会话进展** —— `PR #566 [OPEN]` 持续活跃（前一天刚更新），致力于为ACP、Codex CLI和Claude Code提供持久的外部代理会话绑定，实现跨轮对话上下文保持。这是Moltis多智能体协作能力的关键补强。

前三项已合并/关闭，意味着项目在**国际化、语音配置、测试覆盖**等方面实现了实质性交付。后两项正处在开发流程中，预计将进入后续版本。

### 4. 社区热点

今日没有热评或高赞的Issue/PR互动，所有PR当前评论和 👍 均为 0。即便如此，以下两条PR因其重要性和潜在影响值得关注：

- **`PR #986`** —— 更新zh-TW本地化。虽然没有激烈讨论，但社区贡献者PeterDaveHello独立完成大面积字符串重写，表明项目已开始吸引 **非英语母语贡献者**，对用户基础扩展有积极意义。
- **`PR #985`** —— Web Chat Composer重设计。这是直接面向终端用户交互的模块，重新设计将极大改善聊天输入体验，预计上线后将引发用户反馈高峰。建议维护者在合并后主动收集社区对布局变化的反馈。

总体而言，社区参与度偏低（评论量0），项目仍以核心开发者 **penso** 输出为主。建议运营团队或维护者加强对开放PR的呼声引导，拉动社区测试和意见。

### 5. Bug与稳定性

过去24小时 **未报告任何新的Bug、崩溃或回归问题**。  
目前无紧急稳定性质疑。上周的语音模块 `PR #984` 已加入Playwright测试覆盖，表明团队正在主动提升测试覆盖率并预防语音相关bug。

### 6. 功能请求与路线图信号

- **外部代理持久会话（PR #566）**：该PR自4月6日提出，持续开放至今且仍有更新。它对应多智能体场景中跨平台、跨对话会话绑定的核心需求，是Moltis作为“AI智能体中心”愿景的重要拼图。该功能有大概率被纳入下一版本。
- **Web Composer重新设计 + Astro文档站点**：虽然分别属于UI和文档域，但关联性强——表明项目在近期专注于 **产品化层面打磨**，为下一波大规模用户引入做准备。语音设置引导（PR #984）也属于同一范畴。
- **实时语音/Realtime模型引导（PR #984 已合入）**：虽已合入，但Realtime模式结合语音的完整方案仍在演化中，预计后续将增添更多多模态交互功能。

整体路线图信号指向 **交互体验升级** 和 **多智能体持久化** 两个方向。

### 7. 用户反馈摘要

过去24小时 **未产生真实的用户评论或Issue讨论**，反馈数据缺失。  
基于已合入PR的内容推测：
- **zh-TW地区用户** 可能从UI一致性提升中直接受益；
- 语音配置引导改进有望降低对开发者提示模板的依赖，提升非技术用户的可配置性；
- Composer重设计尚未面向用户，暂时无法评估满意/不满意。

**潜在担忧**：若社区参与持续低迷，新功能可能与其真实需求脱节。建议组织试用反馈计划或设计用户调研流程。

### 8. 待处理积压

| 条目 | 状态 | 说明 | 持续时间 |
|---|---|---|---|
| **PR #566** (Open) | 活跃，但待合并 | 外部代理持久会话，核心功能但功能范围和与现有会话机制的兼容性未定 | 超过30天（自2026-04-06起） |
| **PR #985** (Open) | 刚提交，待审查 | Web Composer重设计，依赖团队设计评审与测试验证 | 1天（可接受） |
| **PR #987** (Open) | 刚提交，待审查 | 文档站点迁移至Astro，需注意与现有自动化流程的兼容性，尤其是URL兼容声明是否完整 | 1天（可接受） |

**重点关注**：**PR #566** 已开放超过一个月，尽管有核心开发者参与，但长期未合并可能意味着存在设计或兼容性难题。建议维护者或代码仓库管理员明确标记期待的下一步动作，避免这类大型功能分支长期悬停导致代码 drift 或社区失望。

> 所有PR链接格式：`moltis-org/moltis PR #586`，请在GitHub上替换为完整URL。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的CoPaw（GitHub: agentscope-ai/CoPaw）项目数据，生成2026年5月9日的项目动态日报。

---

# CoPaw 项目动态日报 | 2026-05-09

## 1. 今日速览

今日项目维持较高活跃度，社区反馈与开发迭代节奏紧凑。过去24小时内，共产生36条Issue和42条PR，其中新发布的 `v1.1.6-beta.1` 版本侧重于集成测试与稳定性修复。社区讨论焦点集中在长对话性能、版本升级兼容性以及多智能体配置持久化等问题上。整体来看，项目开发与社区响应形成良性互动，但部分长期存在的Bug和功能需求仍需维护者优先关注。

## 2. 版本发布

- **v1.1.6-beta.1**：
  - **发布说明**：此版本主要包含非功能性变更和关键修复。
    - **测试**: 新增了应用启动和环境配置的集成测试（smoke tests），以提升版本发布的健壮性。
    - **修复**: 修复了控制台中可能因服务器发送事件（SSE）导致的崩溃问题 (`fix(console): avoid SSE crash`)。
  - **破坏性变更**：无
  - **迁移注意事项**：本次为小版本更新，通常可无损升级。建议在更新后重启服务以应用新配置和修复。

## 3. 项目进展

- **智能体配置与持久化**：PR `#4140` (fix(agent): replace hardcoded agent name with config-driven value) 已关闭并合并。该PR解决了会话中智能体名称被硬编码为“Friday”的长期问题，现在将根据用户配置的 `agent.json` 动态读取，提升了配置的灵活性。同时，为解决Docker环境下密钥恢复问题，PR `#3916` (fix(backup): restore secrets on Docker volume mount points) 也已合并，修复了在挂载卷上因重命名失败导致的恢复错误。
- **控制台与前端体验**：PR `#4146` (feat(console): support mermaid graph) 已关闭，为控制台新增了对Mermaid图表的原生渲染支持，修复了图表显示为空白的问题。PR `#4148` (perf(console): Immediately stop polling and clear the status after closing...) 合并，优化了面板关闭后的性能，避免无效请求。PR `#4130` (perf(console): skip chat history lookup for non-arrow keys) 的合并，通过优化键盘事件处理逻辑，提升了聊天输入框的响应速度。
- **消息通道兼容性**：PR `#4119` (fix(channels): keep markdown tables renderable across split_text chunks) 已合并，确保长Markdown表格在跨消息分片发送后仍能正确渲染，解决了微信等渠道的显示问题。PR `#4112` (feat(WeCom): tool-guard interactive approval card) 为企业微信渠道增加了工具调用的交互式审批卡片，用户可直接在聊天窗口点击按钮审批，提升了工程化体验。
- **核心能力扩展**：PR `#3149` (feat(mcp): support listing tools for mcp) 已关闭，为MCP（Model Context Protocol）添加了工具列表支持，为更复杂的Agent间交互奠定了基础。PR `#4143` (feat(settings): add pt-BR language support) 已合并，新增了对巴西葡萄牙语的支持，扩大了全球用户群。
- **Bug修复**：PR `#4092` (fix(cli): bypass proxies for loopback API checks) 和 PR `#4144` (fix(cli): use loopback for desktop wildcard readiness checks) 已合并，解决了Windows系统下因代理干扰和地址绑定问题导致的CLI命令错误。PR `#4126` (fix(tool_schema): add sanitize tool function schemas) 已合并，对工具函数Schema进行了清理，修复了与某些模型（如DeepSeek）的工具调用兼容性问题。

## 4. 社区热点

- **#3350 (CLOSED): [Question] 页面进行超多轮对话后页面滚动变得特别卡 | [链接](https://github.com/agentscope-ai/QwenPaw/issues/3350)**
  - 该Issue被评为今日最受关注问题（11条评论）。用户反馈在超过200轮对话后，页面滚动变得极其卡顿。这直接反映了当前长上下文对话管理的核心痛点，用户期望获得官方的方法论指导或前端组件优化。该诉求代表了大量进行项目级代码迭代的深度用户。

- **#4133 (OPEN): [Question] 升级到 v1.1.5.post2 后，opencode模型提供商不能正常使用 | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4133)**
  - 这是一个典型的版本升级导致的兼容性问题（10条评论）。用户报告使用`opencode`提供商的模型在升级后报错，而旧版本正常。这表明在小版本迭代中，对于特定第三方服务的间接兼容性测试可能存在盲区，需要开发团队优先排查。

- **#2382 (CLOSED): [Question] 每次更新后venv会重置？所有skill相关的依赖都会失效 | [链接](https://github.com/agentscope-ai/QwenPaw/issues/2382)**
  - 虽然是已关闭问题，但评论数仍高达10条，说明该问题在用户群体中引起的共鸣和讨论相当广泛。用户对于更新流程中虚拟环境被重置、自定义Skill依赖丢失的体验表达了不满，这关乎项目核心更新策略，是影响用户升级意愿的重要信号。

## 5. Bug 与稳定性

- **严重程度：高**
  - **[Bug] #4145 (OPEN): 存在多个智能体时，智能体的运行配置无法持久保存** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4145)
    - **分析**：涉及多Agent场景下的配置管理核心问题，可能导致用户配置混乱，严重影响多Agent系统的可用性。**目前尚无Fix PR**。
  - **[Bug] #4149 (OPEN): Failed model calls persist user messages and replay them on the next chat turn** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4149)
    - **分析**：模型调用失败后，用户消息被持久化并在下一轮重复发送。这是一个可能导致消息混乱和Token浪费的严重数据一致性问题。**目前尚无Fix PR**。

- **严重程度：中**
  - **[Bug] #4147 (OPEN): 配置LM Studio作为本地模型服务时，Internal Server Error** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4147)
    - **分析**：特定本地模型配置（LM Studio）出现服务器内部错误，影响需要私有化部署的用户。**目前尚无Fix PR**。
  - **[Bug] #4123 (OPEN): Windows: execute_shell_command flashes a console window on every call** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4123)
    - **分析**：Windows用户执行Shell命令时弹出控制台窗口，影响用户体验和自动化场景。该问题已有PR `#4041` 尝试部分解决，但尚未被采纳为全面修复。
  - **[Bug] #4099 (CLOSED): 会话初始化中的 agent name "Friday" 被硬编码** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4099)
    - **分析**：该Bug已被PR `#4140` 修复，今日已关闭，问题已解决。

- **严重程度：低**
  - **[Bug] #4137 (CLOSED): can't show mermaid graph in reply** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4137)
    - **分析**：Mermaid图表无法渲染的问题已被PR `#4146` 修复，今日已关闭。
  - **[Bug] #4128 (CLOSED): MiMo-V2.5/V2.5Pro、DeepSeek-V4-Pro出现重复响应问题** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4128)
    - **分析**：特定模型出现重复响应的问题。该Issue状态为CLOSED，但未明确关联到具体的Fix PR，需关注后续是否有回归。

## 6. 功能请求与路线图信号

- **已有关联PR，可能纳入下个版本**:
  - **#4138 (OPEN): [Feature]: add batch action support to browser_use tool** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4138)
    - 请求为浏览器工具增加批量操作支持。同名的PR `#4139` 处于开放审查状态，表明该功能可能已在开发中，有望进入后续版本。
  - **#4124 (OPEN): [Feature Request] Support OAuth login for OpenAI / Codex** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4124)
    - 请求支持OAuth登录。虽然没有直接匹配的PR，但此功能是提升安全性和便捷性的重要方向，社区有强烈需求。
  - **#4131 (OPEN): [Feature]: 构建项目组，每个项目一个群，多角色入群** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4131)
    - 提出了“项目组”和多角色群聊的深入协作模式。此功能复杂度高，但符合长期路线图，是构建“工程级别”协作能力的强信号。

- **未来潜在方向**:
  - **#4113 (OPEN): [Feature]: 希望能增加对话删除功能** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/4113)
    - 允许用户删除中间对话，以避免上下文中混入低质量回答。这是一个小而精的功能建议，实现成本相对较低，但能显著提升用户体验。
  - **#3111 (CLOSED): [Feature]:定时任务无法清空会话的问题** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/3111)
    - 曾是一个紧急需求，虽然已关闭，但其核心诉求（管理定时任务会话）依然存在，未来可能以更完善的形式回归。

## 7. 用户反馈摘要

- **痛点**:
  - **长对话性能瓶颈**: 多轮对话（>200轮）后出现严重卡顿 (#3350)，这是用户进行大型项目迭代时的主要障碍。
  - **更新体验不佳**: 用户对更新后配置丢失（#2382）、特定模型失效（#4133）等问题感到困扰，期望能有无损、平滑的版本升级体验。
  - **配置持久化问题**: 多Agent场景下，配置无法保存（#4145），导致用户需要反复配置，影响了自动化工作流和复杂Agent系统的搭建。
  - **上下文管理不合理**: 用户反映截图和视觉内容被无差别塞入上下文，消耗Token且效果不佳（#4102），希望有更智能的上下文管理策略，如OCR工具。

- **优点与期望**:
  - 用户对Agent间的协作（如A2A）和复杂功能（如项目构建、多角色协作）有强烈的探索欲望和期待（#4131）。
  - 社区对新功能的接纳度高，同时积极贡献代码，如为浏览器工具添加批量动作（#4138）、为聊天增加OAuth登录（#4124）等。

## 8. 待处理积压

- **长期未响应的Issue**:
  - **[Bug] #2165 (OPEN): 无标题Bug** | [链接](https://github.com/agentscope-ai/QwenPaw/issues/2165)
    - 创建于2026-03-24，近期有更新但无官方回复。用户报告了切换模型后出现的API报错，可能是一个潜在的回归问题或边界情况。
  - **[Feature] #3117 (OPEN): Feat/semantic skill routing** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/3117)
    - 这是一个PR，而非Issue。它提出了一个革新的语义技能路由功能，能显著减少Token消耗，但自2026-04-08创建以来，一直处于`Under Review`和`need discussions`状态，至今已超过一个月，进展缓慢。这可能是一个非常有价值但复杂的功能，需要维护者重新评估优先级和投入资源。

- **待关注的PR**:
  - **[PR] #4041 (OPEN): feat(cli-desktop): System tray startup item function** | [链接](https://github.com/agentscope-ai/QwenPaw/pull/4041)
    - 该PR为Windows用户添加了系统托盘功能，并已部分解决了`#4123`中的控制台窗口闪烁问题，但自2026-05-05起仍未合并。考虑到社区对Windows端体验的持续反馈（如#4123），建议维护者加快此PR的审查与合并进程。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw 项目动态日报 | 2026-05-09

## 今日速览
过去24小时项目活跃度较低，未出现新的Issue或版本发布。唯一动态是Pull Request #571（描述长期记忆工具的触发短语）仍处于待合并状态，该PR于5月3日创建后已5天未获得Review或合并。整体来看，社区互动冷清，但PR内容本身具有明确的功能改进意图，后续合并可增强工具使用的规范性。

## 版本发布
无新版本发布。

## 项目进展
**今日无合并/关闭的PR**。唯一值得关注的待处理PR是：
- **PR #571** (feat(tools): trigger-phrase nudges in longterm_memory description)  
  作者：qhkm，创建于5月3日，最后更新于5月8日。该PR重写了`longterm_memory`工具的`description()`，明确枚举了“Use when”与“Do NOT use when”触发短语，并添加了配套的文档测试`test_tool_description_has_trigger_phrases`，以防止未来编辑破坏触发块。该改动借鉴了Hermes Agent的`memory_tool.py`模式，有助于提升工具接口的一致性和用户引导的清晰度。

项目整体向前迈进的步伐缓慢，但该PR若合并可带来可维护性的微改进。

## 社区热点
今日无活跃讨论。唯一PR #571没有评论（评论数undefined），无社区互动可分析。

## Bug 与稳定性
今日未报告新的Bug、崩溃或回归问题。

## 功能请求与路线图信号
**PR #571** 虽未合并，但可视为一个功能增强信号：社区（主要是作者qhkm）正在推动为工具描述提供更明确的触发条件引导，类似Hermes Agent的做法。这种“提示短语”机制可能成为后续工具规范化的模板，有望被纳入下一版本（若当前没有版本发布计划，则可能进入下一个发布周期）。暂无其他明确的新功能请求。

## 用户反馈摘要
今日无来自Issue评论的用户反馈。

## 待处理积压
| 项目 | 链接 | 状态 | 说明 |
|------|------|------|------|
| PR #571 | [GitHub](https://github.com/qhkm/zeptoclaw/pull/571) | 待合并 | 自5月3日创建至今已6天，无Review，无合并进展。该PR内容清晰且附带测试，维护者可考虑尽快Review并合并，避免堆积。 |

> **注**：由于当前数据覆盖时段内（2026-05-08 至 2026-05-09 24小时）无其他待处理Issue或PR，此处仅列出唯一积压项。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报 | 2026-05-09

## 1. 今日速览

过去 24 小时内，ZeroClaw 社区提交了 **50 条新 Issue** 和 **50 条新 Pull Request**，其中 **18 个 PR 已被合并或关闭**，**32 个 PR 处于待合并状态**。本周无新版本发布。项目整体活跃度极高，修复类 PR 频繁（如矩阵频道广播、Gemini CLI 参数修复、历史剪枝防相邻 assistant 消息等），同时有多个增强型 Issue（多智能体运行时、Discord 频道隔离、自定义提供商支持）处于高优先级待处理状态。尽管构建与稳定性问题仍较突出（如 SDK 递归溢出、空 tool_calls 导致 400 错误），但社区贡献者响应迅速，多个关键 Bug 已获得修复 PR。

---

## 2. 版本发布

**无**（过去 24 小时内没有新 Release 发布）。

---

## 3. 项目进展

过去 24 小时内共有 **18 个 PR 被合并或关闭**，以下为其中影响较大的几项：

- **#6191** `fix(channels): guard reply-intent classifier against meta-instruction echo` — 修复回复意图分类器偶尔将自身规则作为不回复原因回显的问题，提升了配对身份频道的判断准确性。
- **#6178** `feat(providers/ollama): add num_ctx/num_predict/temperature tuning` — 为 Ollama 提供商增加 `num_ctx`、`num_predict` 及可选 `temperature_override` 参数，用户现可直接在 `config.toml` 中微调推理行为。
- **#6536** `fix(gateway): return onboarding error from ws chat` — 当当前配置无可用模型时，WebSocket 聊天端点提前返回结构化的 `needs_onboarding` 错误，改善新用户引导体验。
- **#6048** `feat(channels,config): add draft-update streaming to Nextcloud Talk#5718` — 在 Nextcloud Talk 通道中增加 `stream_mode` 与 `draft_update_interval_ms` 配置，允许按通道启用增量响应推送。

这些合并使项目在**通道稳定性、提供商可配置性、网关错误处理**方面均向前迈进了一步。

---

## 4. 社区热点

当日讨论最活跃的 Issue 包括：

- **#6530** `[Bug]: Build failure with matrix-sdk v0.16.0: recursion limit overflow when building with channel-matrix feature`  
  **3 条评论** | 用户报告使用 Matrix SDK v0.16.0 编译时出现递归极限溢出。该构建失败直接阻塞了所有启用 Matrix 通道的用户，属于 **高风险阻断性 Bug**。

- **#6378** `[Feature]: Discord Bot respond only in specific Discord channels`  
  **3 条评论** | 希望 Discord 频道支持 `allowed_channels` 配置，与 Matrix 和 Nextcloud Talk 的 `allowed_rooms` 模式对齐。社区对此需求呼声较高，反映出用户对多频道精细管控的迫切需求。

- **#6298** `[Bug]: Empty tool_calls array sent to provider API, causing 400 on strict validators (DeepSeek, NVIDIA NIM)`  
  **3 条评论** | 启用 `use_native_tools` 且模型无工具调用时，构建的空 `tool_calls: []` 被严格验证的提供商（DeepSeek、NVIDIA NIM）拒绝。该问题已获 **P1 优先级**，且有明确修复方向（见下方 PR #6544）。

社区焦点**集中在**：① **构建兼容性**（Matrix SDK 升级带来回归）；② **提供商交互细节**（空 tool_calls、证书信任、Gemini CLI 参数）；③ **通道配置灵活度**（Discord 允许频道、Matrix 线程行为）。

---

## 5. Bug 与稳定性

以下按严重程度（S0 > S1 > S2 > S3）排列当日报告的 Bug，并标注是否已有修复 PR：

| 严重程度 | Issue ID | 标题摘要 | 状态 | 修复 PR |
|----------|----------|----------|------|---------|
| S0 - 数据丢失/安全风险 | #6419 | WorkspaceManager 在运行时启动时无法加载 profile | accepted | 无 |
| S1 - 工作流阻塞 | #6433 | 心跳与 Matrix 通道组合不工作 | in-progress | ✅ #6509 已提交 |
| S2 - 行为降级 | #6530 | 编译 Matrix SDK v0.16.0 时递归极限溢出 | blocked | 无 |
| S2 - 行为降级 | #6298 | 空 tool_calls 数组导致 DeepSeek/NVIDIA NIM 返回 400 | accepted | ✅ #6544 已提交 |
| S2 - 行为降级 | #6528 | 自定义提供商使用自签名证书时不受信任 | needs-maintainer-review | 无 |
| S2 - 行为降级 | #6520 | Gemini CLI 提供商因 `--print` vs `--prompt` 语法过时崩溃 | accepted | ✅ #6519 已提交 |
| S2 - 行为降级 | #6309 | `model_routing_config` 的 `upsert_agent` 操作覆盖 schema_version=2 设置 | accepted | 无 |
| S2 - 行为降级 | #6524 | Matrix 根时间线消息被错误地创建为线程会话 | in-progress | ✅ #6525 已提交 |
| S3 - 次要问题 | #6280 | Windows Full 构建在 `zeroclaw-hardware` 编译失败 | in-progress | 无 |

*注：另有 #6254（WASM 插件安装路径与扫描路径不一致）已有评论但尚未有 PR。*

---

## 6. 功能请求与路线图信号

以下为当日具有一定优先级（P1/P2）且已被 `accepted` 或 `in-progress` 的功能请求，结合已有 PR 判断其纳入下一版本的可能性：

| Issue ID | 标题 | 优先级 | 当前状态 | 纳入 v0.8.0 可能性 |
|----------|------|--------|----------|---------------------|
| #6272 | 多智能体运行时：按别名的独立工作区、权限与共享资源 | P1 | accepted | **高**，已有对应 PR #6545 提交至 `integration/v0.8.0` |
| #6378 | Discord 频道仅允许特定频道回复 | P2 | accepted | **中**，与现有 Matrix/Nextcloud 模式对等，社区需求强烈 |
| #6422 | `cron_add` 的 schedule 参数错误信息改进 | P2 | accepted | **高**，属于小但易用性改进，预计短期内会实现 |
| #6518 | 自定义/OpenAI 兼容提供商（如 Kimi K2.5）的一等支持 | P2 | needs-maintainer-review | **中**，需维护者确认设计方向 |
| #6510 | cron `delivery.mode = "announce"` 选项仅发送最终助手消息 | P2 | accepted | **中**，属于细粒度控制，适合后续迭代 |
| #6345 | 每个通道的回复最小间隔（节流） | P1 | in-progress | **高**，已有 PR 候选 |
| #6339 | macOS 桌面应用通用二进制（arm64 + x86_64） | P2 | accepted | **中高**，CI 工作量较大但社区已有人开始 |
| #6260 | 可配置 LM Studio 服务器 URL（聊天、嵌入、配置界面） | P2 | accepted | **中**，依赖于提供商重构 |

此外，#6271（V3 SwarmConfig 模式）、#6270（V3 嵌套配置宏支持）、#6273（类型化家族拆分）等 Issue 均来自同一个贡献者 `singlerider`，且有对应的 PR 积累在 `integration/v0.8.0` 分支，表明下一大版本将集中交付**多智能体运行时**与**配置模式重构**。

---

## 7. 用户反馈摘要

从 Issues 评论与描述中提炼的典型用户场景与痛点：

- **“编译风险阻碍了采用”**（#6530）：用户试图在项目中使用 Matrix 频道，但 `matrix-sdk v0.16.0` 导致编译失败。提示项目对上游依赖的升级兼容性测试不足。
- **“不同提供商间的行为差异令人困惑”**（#6298、#6520、#6528）：DeepSeek/NVIDIA NIM 拒绝空 `tool_calls`，Gemini CLI 参数格式过时，自定义提供商 TLS 证书不受信任。反映出**提供商交互层缺乏统一验证机制**。
- **“配置灵活性不足”**（#6378、#6255）：Discord 无法限制频道、命名提供商（kind 字段被忽略）等，用户需要更细粒度的管控。
- **“长对话后模型开始幻觉/偏题”**（#6517）：上下文溢出导致响应质量下降，用户希望有更好的上下文压缩或告警机制。
- **“Windows 构建体验差”**（#6280）：`setup.bat` Full build 在 Windows 上失败，影响平台生态。

正面反馈：用户对新增的 `cron` 和 `delivery.mode` 特性表示期待（#6510），对多智能体运行时（#6272）表现出强烈兴趣，认为这是 ZeroClaw 区别于其他 AI 助手的关键能力。

---

## 8. 待处理积压

以下为长时间未获得响应或明显停滞的重要 Issue/PR，需维护者关注：

| 项目 | ID | 标签 | 停滞时间 | 影响 |
|------|----|------|----------|------|
| Issue | #6074 | audit/ci | 15 天 | 追踪 153 个丢失的提交，对代码历史完整性有长期影响，需制定恢复计划 |
| Issue | #6528 | needs-maintainer-review | 1 天（但属高风险） | 系统 CA 信任缺失会阻塞所有自签名证书场景，需尽快指定 reviewer |
| Issue | #6518 | needs-maintainer-review | 2 天 | 用户要求一等支持 Kimi 等 OpenAI 兼容提供商，设计决策需维护者介入 |
| Issue | #6345 | needs-maintainer-review | 6 天 | 通道节流功能已被标记为 in-progress 但仍需 maintainer 审核 PR |
| Issue | #6279 | needs-maintainer-review | 7 天 | Release 里程碑选择标准的改进建议，直接影响发版效率 |
| PR | #6513 | 无 review | 2 天 | 新提供商 `atomic-chat` 的添加，简单但未获得 maintainer 回应 |
| PR | #6545 | 无 review | 0 天（新） | 多智能体运行时核心 PR，代码量大（约 70% 实现），需尽早进入 code review 流程 |

*注：`needs-maintainer-review` 标签意味着该 Issue/PR 等待核心维护者做出技术决策或代码审核，长时间搁置可能导致贡献者流失。*

---

> **总结**：ZeroClaw 项目今日活动量极大，社区贡献踊跃，修复和增强 PR 数量刷新近期纪录。关键 Bug（Matrix 构建、空 tool_calls）已快速获得修复方案，多智能体运行时（v0.8.0 核心）已被推进到代码合并阶段。需关注长期积压的审计任务和若干等待维护者拍板的设计问题，以保持社区正向循环。

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*