# OpenClaw 生态日报 2026-05-17

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-17 08:34 UTC

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

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的OpenClaw项目（github.com/openclaw/openclaw）GitHub数据，现为您呈上2026-05-17的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-05-17

### 1. 今日速览

今日OpenClaw项目状态**高度活跃**。过去24小时内，项目共发布了三个Beta版本，推进了安全审计、xAI OAuth认证和CLI Cron功能等关键特性。社区的Bug报告和功能请求依旧踊跃，其中涉及内部文本泄露、Android APK发布和跨平台安全配置等问题的讨论热度极高。尽管社区反馈和修复PR数量众多，但P1级别的安全与稳定性Bug仍存在积压，表明项目在快速迭代的同时，对核心可靠性和安全性的关注度持续提升。

### 2. 版本发布

今日共发布 **3 个版本**，均为`v2026.5.16`的Beta迭代，展示了项目快速的迭代节奏。

- **v2026.5.16-beta.4**: 主要引入了 **安全审计抑制功能** (`security.audit.suppressions`)，允许开发者为可接受的安全审查结果设置白名单，在保持JSON输出中记录的同时，将其从活动摘要中隐藏，**建议所有开发者升级**以优化安全告警管理。此外，代理/子代理模块新增了标签功能。
- **v2026.5.16-beta.3 与 v2026.5.16-beta.2**: 这两个版本内容一致，包含两项重要更新：
    - **xAI Grok OAuth登录**: 为SuperGrok订阅者新增了通过OAuth集成xAI Grok模型的认证方式，允许使用`xai/*`模型及xAI工具而无需手动配置`XAI_API_KEY`。
    - **CLI Cron增强**: `openclaw cron run --wait`命令新增了超时和轮询间隔控制，并支持通过`cron.runs --run-id`进行精确的运行ID过滤。

### 3. 项目进展

尽管过去24小时内没有PR被合并，但从今日发布的内容和新增的PR来看，项目在以下关键方向取得了显著进展：

- **安全与合规**: `v2026.5.16-beta.4`中的安全审计抑制功能，是一项重要的质量与合规性提升。同时，多个针对Feishu、权限管理（如`exec`工具权限继承）和沙箱隔离的修复PR正在推进。
- **平台集成**: xAI Grok的OAuth集成扩展了项目支持的模型生态。对Telegram Business Bot、Slack Block Kit等社区热门集成功能的PR也在活跃开发中。
- **开发者体验**: 新的“简单工具插件创作”PR (#83006) 提出了 `defineToolPlugin` SDK 辅助函数和 `openclaw plugins init/build/validate` 命令，旨在简化插件开发流程，对扩展生态具有潜在的重大意义。
- **用户界与体验**: iOS Liquid Glass UI、Action Button支持等PR显示项目正积极拥抱平台原生特性，提升移动端体验。

### 4. 社区热点

以下是今日讨论热度最高的议题，反映了社区的核心关切：

1.  **内部处理文本泄露 (#25592 - 26条评论)**: 此P1级安全问题持续受到关注。用户反馈当智能体在两轮工具调用之间生成文本（如错误处理、处理确认等）时，这些文本会作为可见消息泄露到通讯频道中。这严重影响了用户体验，并可能暴露内部工作逻辑。
2.  **预编译Android APK发布 (#9443 - 24条评论)**: 这是一个长期以来的社区呼声。用户希望能直接从GitHub Releases下载预编译的Android APK，以便于使用OpenClaw的Android伴侣应用，而无需自行搭建编译环境。
3.  **Signal守护进程竞态条件 (#22676 - 17条评论)**: 一个P1级Bug，描述了在SIGUSR1重启过程中，Signal守护进程未等待旧进程完全退出即启动新实例，导致孤儿进程和消息发送失败的问题，影响了系统稳定性。
4.  **控制UI要求HTTPS/本地主机安全上下文 (#32473 - 15条评论)**: 用户在VPS上通过Docker部署时，遇到了控制UI要求设备身份验证（HTTPS或本地主机安全上下文）的问题，导致无法正常访问，这是一个影响部署体验的回归问题。
5.  **分层引导文件加载 (#22438 - 16条评论)**: 社区提出了一个优化token使用的建议，即通过分层、按需加载引导文件，避免在子代理或Cron任务等场景下浪费上下文窗口预算。

**热点链接：**
- [Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592)
- [Request: Prebuilt Android APK releases](https://github.com/openclaw/openclaw/issues/9443)
- [Signal daemon stop() race condition](https://github.com/openclaw/openclaw/issues/22676)
- [Control UI requires device identity](https://github.com/openclaw/openclaw/issues/32473)
- [Tiered bootstrap file loading](https://github.com/openclaw/openclaw/issues/22438)

### 5. Bug 与稳定性

今日报告的Bug以**安全**和**会话状态**相关的最为严重，且不少是回归问题。以下按严重程度排列：

| 严重程度 | Issue / PR 链接 | 关键摘要 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- |
| P1 | [Issue #25592](https://github.com/openclaw/openclaw/issues/25592) | **文本泄漏**: 工具调用间的文本被错误地发送到用户频道。 | 否 (PR待查找) |
| P1 | [Issue #22676](https://github.com/openclaw/openclaw/issues/22676) | **进程竞态**: Signal服务重启导致孤儿进程和发送失败。 | 否 |
| P1 | [Issue #32296](https://github.com/openclaw/openclaw/issues/32296) | **上下文混乱**: 智能体回复上一条消息而非当前消息。 | 否 |
| P1 | [Issue #31583](https://github.com/openclaw/openclaw/issues/31583) | **回归**: `exec`工具不继承 `skills.entries.*.env` 变量。 | 否 |
| P1 | [Issue #29736](https://github.com/openclaw/openclaw/issues/29736) | **路径错误**: `exec-approvals.json` 忽略配置的状态根目录，写入错误路径。 | 否 |
| P2 | [Issue #32473](https://github.com/openclaw/openclaw/issues/32473) | **回归**: 控制UI在非HTTPS/本地环境下无法使用。 | 否 |
| P2 | [Issue #38439](https://github.com/openclaw/openclaw/issues/38439) | **回归**: Webchat头像端点 `404`。 | 否 |
| P2 | [Issue #40540](https://github.com/openclaw/openclaw/issues/40540) | **更新失败**: Windows上 `openclaw update` 命令报 `EBUSY` 错误。 | 否 |
| P2 | [Issue #76552](https://github.com/openclaw/openclaw/issues/76552) | **性能**: Codex运行时任务导致CPU负载过高。 | **CLOSED** (已解决) |

**稳定性总结**: 大量P1级的Bug，尤其是回归问题，显示新版本引入的变动可能带来了连锁反应。代码库的整体稳定性在快速迭代中受到了挑战。

### 6. 功能请求与路线图信号

从今日的社区热度和PR状态看，以下是可能被纳入下一版本的功能方向：

- **安全与权限**: `exec`工具权限细化（[Issue #31583](https://github.com/openclaw/openclaw/issues/31583)）、路径级RWX权限（[Issue #39979](https://github.com/openclaw/openclaw/issues/39979)）、文件系统沙箱配置（[Issue #7722](https://github.com/openclaw/openclaw/issues/7722)）等需求持续被强调，多个相关PR（如[#41204](https://github.com/openclaw/openclaw/pull/41204)、[#41649](https://github.com/openclaw/openclaw/pull/41649)）也集中在安全强化上。
- **平台与集成**: Telegram Business Bot支持（[Issue #20786](https://github.com/openclaw/openclaw/issues/20786)）、Slack Block Kit（[Issue #12602](https://github.com/openclaw/openclaw/issues/12602)）和WhatsApp支持（[PR #41265](https://github.com/openclaw/openclaw/pull/41265)）的呼声很高，表明社区有强烈的多平台、富交互需求。
- **开发者生态**: 简单工具插件创作功能（[PR #83006](https://github.com/openclaw/openclaw/pull/83006)）的提出，预示着项目有意降低生态扩展门槛，这可能会是未来的一个重点发展方向。
- **会话与上下文管理**: 分层的引导文件加载（[Issue #22438](https://github.com/openclaw/openclaw/issues/22438)）、子代理完成通知的优化路由（[Issue #27445](https://github.com/openclaw/openclaw/issues/27445)）等讨论，反映了社区希望更精细地控制LLM会话的成本和行为。

### 7. 用户反馈摘要

从今日的Issue评论中，可以提炼出以下真实用户痛点：

- **“我的内部处理逻辑暴露了！”**：Issue #25592 的用户强烈抱怨，智能体在处理任务时的内部文本（如“正在查询数据库...”）被发送到了群聊，这既干扰了正常对话，又可能泄露敏感的内部处理流程。
- **“编译痛苦，求APK”**：Issue #9443 的用户表达了明显的挫败感，对于只想使用Android应用的普通用户来说，自行编译的门槛过高。他们期望获得像其他成熟项目一样“开箱即用”的体验。
- **“配置太复杂，难以排查”**：Issue #32473 的用户在VPS上部署时遇到了HTTPS上下文问题，这表明项目的部署文档或默认配置可能不够友好，对非专业运维用户构成挑战。
- **“环境变量不继承，技能无法工作”**：Issue #31583 的用户描述了通过`exec`工具运行需要特定环境变量的技能时遭遇失败。这是一个回归问题，严重影响了依赖于环境变量的工作流。
- **“沙箱隔离太死板，工具无法写入”**：Issue #37634 的用户反馈，当设置 `workspaceAccess` 为 “none” 时，沙箱内的 `/workspace` 目录是只读的，导致 `write_file` 等工具无法正常工作，使得想要高度隔离的沙箱环境变得无法使用。

### 8. 待处理积压

以下是一些创建已久但今日仍被更新或讨论的重要Issue，建议项目维护者重点关注：

- **[Issue #9443] Prebuilt Android APK releases** (创建于2026-02-05，今日仍有24条评论): 这是一个持续了三个多月的功能请求，社区呼声极高，是提升用户体验和项目普及度的关键点。
- **[Issue #6615] Add denylist support for exec-approvals** (创建于2026-02-01): 此功能请求已存在超过3个月且获得7个👍，社区希望在“允许所有”和“逐一审批”之间找到一个更灵活的折中方案。目前的`no-new-fix-pr`标签表明尚未有开发者认领。
- **[Issue #7722] Filesystem Sandboxing Config** (创建于2026-02-03): 与Issue #6615类似，社区对更精细的文件系统访问控制需求由来已久。这关系到项目的核心安全模型，值得优先考虑。

---

## 横向生态对比

好的，作为资深技术分析师，我已仔细审阅了您提供的2026-05-17各开源项目社区动态摘要。现在，为您呈上一份聚焦于个人AI助手与自主智能体开源生态的横向对比分析报告。

---

### **个人AI助手与自主智能体开源生态全景分析报告 (2026-05-17)**

#### **1. 生态全景**

2026年5月中旬，个人AI助手与自主智能体开源生态呈现出 **“高活跃度、强分化、快迭代”** 的态势。一方面，以OpenClaw、NanoBot、Hermes Agent为代表的核心项目正经历着功能大版本更新（如长期任务跟踪、基础体验重构）与安全合规性强化，社区贡献者的参与热情极高。另一方面，市场分层已清晰可见：既有追求全面企业级能力的“重型平台”，也有专注特定场景或轻量部署的“敏捷工具”。然而，生态快速发展的同时，**功能扩展与稳定性回归之间的矛盾**成为普遍痛点，几乎所有活跃项目都报告了因快速迭代导致的Bug回归问题，尤其是在上下文管理、渠道集成和安全权限领域。**安全、稳定、易用** 已成为社区共鸣最强的三大核心诉求。

#### **2. 各项目活跃度对比**

| 项目 | 今日活跃 Issue/PR 数 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 高 (50+ Issue/PR) | 3个 (Beta) | **优秀**。迭代节奏最快，安全审计和模型集成进展明显，但P1级Bug积压值得关注。 |
| **NanoBot** | 高 (50+ Issue/PR) | 1个 (正式版 v0.2.0) | **良好**。大版本发布带来核心突破，但新版本的文档和UI回归问题急需修复。 |
| **Hermes Agent** | 极高 (50 Issue, 50 PR) | 1个 (正式版 v0.14.0) | **中等**。社区产出高，但架构抄袭争议和大量未合入PR表明项目管理存在瓶颈。 |
| **PicoClaw** | 中等 (12 Issue/PR) | 1个 (Nightly) | **良好**。功能扩展（多账号、新提供商）积极，社区反馈的问题有讨论但缺少修复PR。 |
| **NanoClaw** | 高 (16 PR) | 无 | **良好**。合并效率高，金融技能和稳定性修复是亮点，但新Issue暴露了部署和数据一致性风险。 |
| **IronClaw** | 高 (50+ Issue/PR) | 无 | **良好**。“Reborn”架构重构进入密集合并期，依赖安全和E2E稳定性问题正被重点处理。 |
| **LobsterAI** | 中等 (16 PR) | 无 | **中等**。内部版本整合活跃，但大量陈旧PR积压，桌面客户端连接稳定性是主要短板。 |
| **NullClaw, TinyClaw, ZeptoClaw** | 低 | 无 | **休眠**。过去24小时无活动，需持续关注其后续更新。 |
| **Moltis** | 低 (5 Issue/PR) | 无 | **中等**。社区有新Bug和功能PR，但无任何合并/关闭，处理节奏慢。 |
| **CoPaw** | 高 (28 Issue/PR) | 无 | **中等偏下**。社区贡献积极，但致命Bug（聊天无响应、指令冻结）和大量积压PR是重大风险。 |
| **ZeroClaw** | 极高 (100 Issue/PR) | 无 | **良好**。社区贡献热情最高，多个关键Bug被修复，大量功能PR待审，处于重大版本（v0.8.0）冲刺期。 |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 在本生态中扮演着 **“标准参照”与“创新引擎”** 的双重角色。

- **优势对比**：
    - **更成熟的社区与治理**：相比于Hermes Agent的抄袭争议和ZeroClaw的积压，OpenClaw的PR合并、版本发布流程更规范，社区反馈能得到系统性响应。
    - **更强的安全与迭代意识**：相比NanoBot在v0.2.0版本后才频繁修复回归Bug，OpenClaw在Beta阶段就主动引入“安全审计抑制”等高级合规功能，体现了更高的工程成熟度。
    - **更广的平台集成**：对xAI Grok的OAuth支持，表明其在接入最新、顶级的模型提供商方面走在前列，与NanoBot和PicoClaw对国内模型的支持形成互补。

- **技术路线差异**：
    - 与追求轻量、去中心化的NanoBot不同，OpenClaw倾向于构建功能全面的 **“统一网关与Agent运行平台”**。
    - 与强调底层架构重构的IronClaw和Hermes Agent相比，OpenClaw的迭代更注重**稳定性与兼容性**，发布的Beta版本多是对现有功能的安全和性能打磨。

- **社区规模对比**：从数据看，OpenClaw的Bug报告（如#25592文本泄露）能在1天内获得26条高质量讨论，其社区参与深度和问题响应质量在生态内属于第一梯队。相较之下，Moltis等小型项目虽能提出高质量特性，但社区互动和问题解决效率明显不足。

#### **4. 共同关注的技术方向**

以下是多个项目“不约而同”聚焦的核心技术点，代表了行业的普遍痛点与演进方向：

1.  **安全与权限控制（涉及：OpenClaw, PicoClaw, ZeroClaw, CoPaw）**：
    - **诉求**：社区强烈要求更细粒度的权限控制，如“工具权限继承”、“文件系统沙箱”、“技能级安全配置”。
    - **代表Issue**: OpenClaw #31583 (`exec`工具不继承环境变量)、PicoClaw #1042 (`restrict_to_workspace`路径误判)、CoPaw #5775 (`per-skill security permissions`)。

2.  **上下文管理与Token优化（涉及：OpenClaw, Hermes Agent, CoPaw, ZeroClaw）**：
    - **诉求**：解决上下文窗口浪费、中间文本泄露、压缩丢失推理内容等核心痛点。
    - **代表Issue**: OpenClaw #22438 (分层引导文件加载)、Hermes Agent #6839 (惰性工具架构加载)、CoPaw #4448 (Context compaction失败)、ZeroClaw #6269 (推理内容被压缩丢弃)。

3.  **平台/渠道集成深化（涉及：NanoBot, Hermes Agent, CoPaw, ZeroClaw）**：
    - **诉求**：超越基础的Telegram/微信接入，向企业级IM（飞书、Slack、Mattermost）和自动化工具（Email、Webhook）深度集成。
    - **代表Issue/PR**: Hermes Agent #27358 (飞书Slash命令)、CoPaw #3246 (QQ频道即时确认)、ZeroClaw #5604 (Mattermost私信)。

4.  **开发者体验与生态共建（涉及：OpenClaw, NanoBot, ZeroClaw）**：
    - **诉求**：简化插件/工具开发流程，降低贡献门槛。
    - **代表PR**: OpenClaw #83006 (`defineToolPlugin` SDK)、NanoBot #3856 (核心模块解耦)、ZeroClaw #5994 (建设官网与端到端文档)。

5.  **多智能体协作（涉及：Hermes Agent, ZeroClaw, Moltis）**：
    - **诉求**：从单个Agent调用工具，走向Agent间的发现、通信与任务分解。
    - **代表Issue/PR**: Hermes Agent #514 (A2A协议支持)、ZeroClaw #6398 (Multi-Agent Runtime and Schema V3)、Moltis #1004 (非阻塞父agent)。

#### **5. 差异化定位分析**

| 维度 | OpenClaw | NanoBot | Hermes Agent | PicoClaw | ZeroClaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全能型个人AI平台，强调安全与合规 | 个人生产力工具，强化长期目标跟踪 | 企业级Agent网关，深厚的IM适配 | 轻量级、社区驱动的AI助手 | 技术先锋，注重多Agent与底层架构创新 |
| **目标用户** | 追求稳定、安全的个人/团队开发者 | 重视效率、希望实现任务自动化的个人用户 | 需要在Slack/飞书等平台集成AI的团队 | 偏好简洁、低配置门槛的社区用户 | 探索前沿架构、愿意尝试新技术的开发者 |
| **技术架构** | 统一、模块化的单体应用 | 功能模块化，核心循环和Provider解耦 | 成熟的Gateway + Worker架构 | 相对简单，功能依赖社区PR扩展 | 激进的Schema迭代，支持OCI工作流 |

#### **6. 社区热度与成熟度**

- **快速迭代阶段 (高活跃、高刷新)**：**OpenClaw**、**ZeroClaw**、**NanoBot (v0.2.0发布期)**、**IronClaw (Reborn重构期)**。这些项目社区讨论活跃，贡献者投入度高，版本迭代速度最快，但也伴有功能不稳定和回归Bug。
- **质量巩固阶段 (在修复中优化)**：**Hermes Agent**、**CoPaw**、**NanoClaw**。这些项目在前一个阶段建成了较为成熟的功能体系，当前重心在于修复重大Bug、清理积压PR，并磨平已有功能的死角（如特定模型兼容性、消息去重逻辑）。社区情绪较为积极，但对稳定性期望值很高。
- **稳定/停滞阶段 (低活跃)**：**LobsterAI**、**Moltis**、**NullClaw/TinyClaw/ZeptoClaw**。这些项目或因为功能完备、或因为维护精力不足，更新频率和社区参与度显著下降。其中LobsterAI内部仍在合并代码，但对外沟通和问题响应不足。

#### **7. 值得关注的趋势信号**

1.  **安全是AI智能体的第一优先级**：从OpenClaw的审计抑制到PicoClaw的路径误判，再到CoPaw的技能级权限诉求，安全不再是可选项，而是决定项目能否被信任并投入生产的**核心基石**。开发者应考虑在设计之初就引入最小权限原则和沙箱机制。
2.  **“配置即代码”与“无配置”的矛盾与平衡**：IronClaw、ZeroClaw等项目在推进TOML/YAML代替JSON和.env，解决复杂性问题。但同时，NanoBot和PicoClaw的社区抱怨“配置太复杂”。这提示**好的项目既要提供声明式配置的强能力，也要有开箱即用的默认值或引导程序**。
3.  **上下文窗口的“通胀”与优化需求齐头并进**：Hermes Agent将最小上下文要求提升至64K，但OpenClaw和NanoBot社区都在呼吁分层加载、惰性加载以优化Token使用。**纯粹的上下文放大已不是万能药，对内容的结构化管理和按需加载能力将成为新常态**。
4.  **Webhook成为“万能胶”**：ZeroClaw对Webhook Agent模式和Webhook transforms的强烈需求，表明用户希望将AI智能体无缝嵌入其现有的CI/CD、业务系统和工作流中。**对外的集成接口（Webhook, Email, SMTP）将是区分平台级与工具级项目的关键能力**。
5.  **AI智能体的“客户端”体验回归**：NanoBot的WebUI显示错乱、LobsterAI的桌面端连接丢失、CoPaw聊天窗口无响应，这些Bug都指向**终端用户直接感知的UI/Chat界面**仍是薄弱环节。在核心Agent能力趋同的背景下，**稳定、流畅、美观的客户端体验将成为吸引和留住用户的关键壁垒**。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我已根据您提供的NanoBot GitHub数据，为您生成了 **2026年5月17日的项目动态日报**。

---

## NanoBot 项目动态日报 (2026-05-17)

### 1. 今日速览

今日项目活跃度极高，标志着 **v0.2.0** 正式发布的重要里程碑。该版本通过 “/goal” 命令引入了持续目标跟踪的核心能力，是项目在智能体长期任务处理上的关键突破。社区修复工作同步密集进行，**22个 PR** 中有 15 个已被合并或关闭，展现了核心团队快速响应和迭代的能力。目前项目处于一个“核心功能大版本发布 + 周边生态与稳定性紧急修复”的并行阶段，整体健康度良好，但新版本的Docker部署文档和WebUI显示等回归问题需要优先解决。

### 2. 版本发布

-   **v0.2.0**：发布说明标题为 “The agent learned to hold a goal.”，这是一个重大功能版本。
    -   **核心特性**: 引入了 `/goal` 命令，允许用户将一个线程标记为长期任务 (`long_task`)。该目标会被固定在每次交互的“运行时上下文(Runtime Context)”中，即使经历上下文压缩或长时间工具调用，目标状态也不会丢失。这意味着NanoBot在实现可持续、有状态的复杂任务代理方面迈出了坚实的一步。
    -   **数据支撑**: 该版本合并了105个PR，并有20位新贡献者参与。
    -   **潜在影响与迁移注意事项**: 由于该版本涉及智能体核心架构的修改（如 `AgentLoop` 的重构），使用旧版本配置或扩展插件的用户可能需要关注兼容性问题。特别是，发布说明中提到移除了旧的“编排器风格的长任务WebUI”，如果您的部署依赖此UI，需要迁移至新的 `/goal` 工作流。同时，文档（`docs/deployment.md`）和 `docker-compose.yml` 与 v0.2.0 的实际配置存在多处不一致，强烈建议Docker用户在升级后参考最新文档核对配置。

### 3. 项目进展

今日项目的核心进展集中在 **智能体核心模块重构** 和 **提供者（Provider）兼容性修复** 两大方向。

-   **智能体核心重构**：
    -   [#3856](https://github.com/HKUDS/nanobot/pull/3856) 将检查点（Checkpoint）和轮次持久化（Turn-writer）逻辑从庞大的 `loop.py` 中提取到独立模块。这大幅降低了核心代码的复杂度，提升了可审查性，是代码架构治理的重要一步。
    -   [#3858](https://github.com/HKUDS/nanobot/pull/3858) 将 `ContextBuilder.build_user_content()` 方法公开，为后续开发者自定义消息构建逻辑提供了更清晰的接口。
    -   [#3859](https://github.com/HKUDS/nanobot/pull/3859) 修复了 `_drain_pending` 中重复注入运行时上下文的问题，消除了每次对话轮次中的token浪费，直接提升了LLM API的调用效率。

-   **提供者兼容性修复**：
    -   [#3851](https://github.com/HKUDS/nanobot/pull/3851) 与 [#3867](https://github.com/HKUDS/nanobot/pull/3867) 联合解决了MiMo模型通过OpenRouter等网关提供商调用时，`reasoning_effort` 参数失效的问题。这确保了用户在使用不同API入口时，对模型思考过程的控制能力是统一的。
    -   [#3864](https://github.com/HKUDS/nanobot/pull/3864) 识别并修复了部分中国国产LLM提供商返回的中文限流错误标记 `‘访问量过大’`，将其正确归入临时错误处理逻辑，提升了调用这些提供商的稳定性。

-   **文档与生态**：
    -   [#3860](https://github.com/HKUDS/nanobot/pull/3860) 更新了 `CLAUDE.md`，使其与当前代码库支持的渠道、提供者和工具列表保持同步，为AI辅助编码和项目新贡献者提供了可靠参考。
    -   [#3461](https://github.com/HKUDS/nanobot/pull/3461) (已关闭) 基于文件系统的“邮箱”频道插件，为多Agent间的进程间通信提供了一种零侵入性的解决方案。

### 4. 社区热点

-   **热点 Issue [#3790](https://github.com/HKUDS/nanobot/issues/3790): `[bug] WebUI会话-打印内容显示错乱。`**
    -   **热度**: 过去24小时内获得13条评论，是今日讨论最活跃的议题。
    -   **诉求分析**: 该问题直接指向用户体验的核心——WebUI界面。用户反馈在更新最新版源码后，会话打印内容显示错乱，需刷新才能恢复。这表明 v0.2.0 在Web前端的渲染或状态管理上可能存在回归问题。高活跃度代表此问题影响了大量用户的日常使用，社区情绪较为迫切。

### 5. Bug 与稳定性

今日报告的Bug从严重到一般排列如下：

-   **严重**:
    -   **[#3790](https://github.com/HKUDS/nanobot/issues/3790) WebUI内容显示错乱**：影响面广，直接破坏核心交互体验。**暂无关联的fix PR**。
    -   **[#3857](https://github.com/HKUDS/nanobot/issues/3857) 启动引导失败 (HTTP 500)**：导致用户完全无法使用WebUI。`nanobot gateway` 服务端返回500错误，初步判断为新版本的配置或服务启动逻辑存在缺陷。**暂无关联的fix PR**。

-   **中等**:
    -   **[#3863](https://github.com/HKUDS/nanobot/issues/3863) 微信无法登录**：用户反馈扫描二维码后提示“微信版本较低”，但用户已更新到最新版。这可能是NanoBot的微信登录协议与微信官方新版本存在兼容性问题。**暂无关联的fix PR**。
    -   **[#3873](https://github.com/HKUDS/nanobot/issues/3873) Docker部署文档与v0.2.0不一致**：文档、`docker-compose.yml`、`Dockerfile` 及 `README` 之间存在至少4处不一致，导致无法正确部署。这是一个典型的发布流程问题，会极大阻碍新用户的尝试。**暂无关联的fix PR**。

-   **已修复**:
    -   **[#3845](https://github.com/HKUDS/nanobot/pull/3851) MiMo在OpenRouter上思考控制失效**：该问题已在 [#3851](https://github.com/HKUDS/nanobot/pull/3851) 和 [#3867](https://github.com/HKUDS/nanobot/pull/3867) 中通过递进式修复得到解决。
    -   **Docker构建失败**：由 [#3870](https://github.com/HKUDS/nanobot/pull/3870) 和 [#3872](https://github.com/HKUDS/nanobot/pull/3872) 两个PR共同修复，包括 `hatch_build.py` 文件缺失和前端端口暴露问题。

### 6. 功能请求与路线图信号

-   **社区强烈需求**:
    -   **多渠道原生接入**: 用户提出了对 **Signal** 渠道的支持 ([#3852](https://github.com/HKUDS/nanobot/pull/3852))，表明社区不满足于现有的微信、钉钉等渠道，希望有更隐私、更开放的通讯工具集成。
    -   **智能体自我纠错与优化**: 提出了 **LoopDetectHook** 和 **ReflectRetryHook** ([#3728](https://github.com/HKUDS/nanobot/pull/3728))，目标是在不消耗额外Token的情况下，自动检测工具调用循环。这对提升Agent部署的可靠性至关重要，很可能会被纳入后续版本。

-   **路线图信号 (潜力功能)**:
    -   **轻量级技能路由器**: [#3865](https://github.com/HKUDS/nanobot/pull/3865) 提出的 **BM25-lite skill router** 能够减少系统提示词约60%的token消耗。这与v0.2.0优化上下文效率的思路一脉相承，极有可能成为下一个版本的核心特性之一。
    -   **跨实例协作**: [#3854](https://github.com/HKUDS/nanobot/pull/3854) 为多个NanoBot实例（Peers）间的发现与通信打下了基础，指向了未来多Agent协作场景。

### 7. 用户反馈摘要

-   **痛点**:
    -   `kxsk-git` (`#3790`): “更新最新的5.13源码版本后，WebUI会话内容打印出来后显示错乱，需刷新页面才可恢复。” 这是一个典型的“更新后反而变差”的体验，会降低用户对版本升级的信任感。
    -   `prakmyl` (`#3857`): “`nanobot gateway` is running and but throws the error message when i try to access the FE (http://127....” 用户在遵循指引操作后仍然遇到500错误，表明新版的启动流程或错误提示不够友好。
    -   `KennethYCK` ( `#3863`): “说目前微信版本较低, 无法使用这功能... 已更新到最新wechat。” 用户发现NanoBot的功能判定与客户端的实际状态不一致，这属于明显的逻辑Bug。
    -   `URD0TH` (`#3873`): 详细列举了Docker部署文档的四处不一致，包括端口冲突、健康检查端点错误等。这表明维护者在发布大版本前，缺乏对文档和示例配置的端到端验证。

### 8. 待处理积压

-   **重要PR**:
    -   **[#3728](https://github.com/HKUDS/nanobot/pull/3728) feat(agent): add LoopDetectHook and ReflectRetryHook for agent self-correction**：该PR自5月10日创建以来，一周内没有新评论，也未合并。考虑到其目标是解决Agent“盲目重试”和“工具调用循环”两大顽疾，价值很高，且与v0.2.0的“长期任务”场景高度互补。**建议维护团队积极评估并推动合并，或给出明确的方向性反馈。**

-   **长期未响应Issue**:
    -   今日数据中未发现明显长期未响应的Issue。但结合社区热点，**目前最需要维护者回应的，是那些关于v0.2.0回归问题的Bug (例如 `#3790`, `#3857`)**，这些问题的解决优先级应高于一切新功能。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 Hermes Agent 项目数据，我为您生成如下项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-05-17

## 1. 今日速览

今日项目活跃度极高，24小时内产生了50条Issue和50条PR，但呈现“高产出、高积压”的健康度矛盾。核心动态围绕**v0.14.0 Foundation Release**发布展开，这是一个里程碑式版本，标志着项目在安装和运行体验上的重大优化。然而，社区反馈主要集中在**多模型/多提供商兼容性**（如Xiaomi、Gemini）和**核心功能的 Bug**（如`delegate_task`配置失效、上下文污染等）上，显示出快速迭代中的稳定性挑战。尽管合并/关闭率较低（PR仅6/50，Issue仅11/50），但项目推进了大量基础架构工作和安全性修补。存在两起关于**架构抄袭**的争议性议题，需要项目方正式回应。

## 2. 版本发布

**Hermes Agent v0.14.0 (v2026.5.16) - “The Foundation Release”**
- **显著变更**：自v0.13.0以来，历经808次提交、633个合并PR、1393个文件变更，关闭了545个Issue（包括12个P0和50个P1），并有215位社区贡献者参与。
- **核心主题**：该版本专注于**基础体验优化**，旨在让Hermes Agent的安装和运行更加简便。虽然发布说明摘要仅为“Hermes installs and runs an”，但结合庞大的代码变更量（+165,061行），这很可能意味着对核心运行栈、依赖管理或默认配置进行了深度重构。
- **潜在破坏性与迁移指南**：
    - **上下文窗口要求提升**：从相关Issue（#24140）推断，v0.14.0可能将**最小上下文窗口要求提升至64,000 tokens**，导致部分旧模型（如32K上下文）被拒绝。用户需检查所有依赖模型的上下文窗口大小。
    - **默认配置变更**：鉴于“Foundation Release”的特性，建议用户仔细审阅 `config.yaml` 模板，尤其是关于 `delegate_task`、`gateway` 和多配置文件管理的部分，以防配置结构或关键参数的默认值发生改变。
    - **部署注意**：对于使用 `hermes update` 的用户，需要注意的是，更新快照中现已包含飞书注释规则文件（`feishu_comment_rules.json`），防止用户自定义的访问控制列表丢失。

## 3. 项目进展 (关键合并/关闭的PR)

尽管当日合并/关闭的PR数量不多，但每一项都关乎项目的关键进展：

- **平台特性对齐**：
    - [#27358](https://github.com/NousResearch/hermes-agent/issues/27358) **飞书适配器 Slash 命令确认**：为飞书添加了交互式卡片按钮，实现了与 Telegram/Discord/Slack 相同的用户确认体验。这是补齐上一版本功能短板的重要一步。
- **稳定性与兼容性修复**：
    - [#27357](https://github.com/NousResearch/hermes-agent/issues/27357) **Gateway 端口配置错误修复**：修复了 `msgraph_webhook` 和 `wecom_callback` 适配器在读取非数字字符串端口时的崩溃问题，提升了 gateway 的健壮性。
    - [#27351](https://github.com/NousResearch/hermes-agent/issues/27351) **Xiaomi 多模态工具修复**：针对 Xiaomi 等不支持多模态工具消息内容的提供商，修复了 agent 运行时传递多模态数据导致的 400 错误。这是解决特定提供商兼容性问题的关键修复。
- **代码质量与安全性**：
    - [#27355](https://github.com/NousResearch/hermes-agent/issues/27355) **性能微优化**：持续进行代码库清理，将元组转换为集合用于成员测试。虽然是微小改动，但体现了对性能的长期关注。
    - [#27353](https://github.com/NousResearch/hermes-agent/issues/27353) **品牌资产更新**：更新了网站 Favicon，标志着项目品牌视觉的规范化。

## 4. 社区热点

- **#514 - [热门] A2A 协议支持请求** (`👍: 4, 评论: 12`)
    - [链接](https://github.com/NousResearch/hermes-agent/issues/514)
    - **诉求分析**：社区对 Google 推出的 A2A（Agent-to-Agent）协议表现出强烈兴趣。这反映出用户已经不满足于“Agent 调用工具”，而是希望不同 Agent 之间能够**发现、通信和协作**。这是构建多智能体系统的未来方向。
- **#6839 - [热门] 惰性工具架构加载** (`👍: 10, 评论: 8`)
    - [链接](https://github.com/NousResearch/hermes-agent/issues/6839)
    - **诉求分析**：这是当日最“得民心”的 Feature Request。用户痛点非常明确：每次 API 调用都注入全部工具（50+）的 Schema，造成巨大的 token 浪费（~3500-5000 tokens）。该提议旨在通过**两阶段注入**，仅在需要时才加载特定工具 schema，能显著降低成本和推理延迟。
- **#10232 - [热门] “.” 问题** (`👍: 16, 评论: 1`)
    - [链接](https://github.com/NousResearch/hermes-agent/issues/10232)
    - **诉求分析**：获赞数最高，但内容仅为“.”。这种“空 Issue”通常代表着社区成员的一种**沉默的抗议或测试**。结合近期关于抄袭的争议，这可能是用户对项目管理或行为不满的一种无声表达。

## 5. Bug 与稳定性

按严重程度排列：

- **P0/P1 - 严重缺陷**：
    - [#24140](https://github.com/NousResearch/hermes-agent/issues/24140) **[已关闭] 所有模型被拒**：由于最小上下文窗口要求提升至 64K，导致 Telegram 服务完全中断。此问题虽已修复，但反映出**版本升级的兼容性风险**。
    - [#27319](https://github.com/NousResearch/hermes-agent/issues/27319) **[P2] 提示注入扫描器缺陷**：`_scan_context_content` 未能检测多词变体的提示注入。已有 PR [#27217](https://github.com/NousResearch/hermes-agent/pull/27217) 和 [#27284](https://github.com/NousResearch/hermes-agent/issues/27284) 处理类似问题，但修复范围可能不够。这是安全风险。
- **P1 - 功能性回归**：
    - [#7833](https://github.com/NousResearch/hermes-agent/issues/7833) `delegate_task` 覆盖自定义端点。这是多代理配置中的关键Bug。
- **P2 - 中等严重性**：
    - [#27344](https://github.com/NousResearch/hermes-agent/issues/27344) Xiaomi provider 400 错误（**已有 Fix PR**）
    - [#26730](https://github.com/NousResearch/hermes-agent/issues/26730) Kanban Worker 上下文污染
    - [#27282](https://github.com/NousResearch/hermes-agent/issues/27282) TUI 模式下 gateway 意外退出
    - [#27294/5/6](https://github.com/NousResearch/hermes-agent/issues/27294) `delegate_task` 忽略 `base_url`（**三个重复提交，问题严重性高**）

## 6. 功能请求与路线图信号

- **高频信号**：
    - **AI 提供商扩展**：新增 [Vertex AI (Anthropic)](https://github.com/NousResearch/hermes-agent/pull/27356)、[Tenstorrent AI](https://github.com/NousResearch/hermes-agent/pull/27348) 提供商。这符合当前“接入更多模型”的大趋势，有望被纳入下一个小版本。
    - **飞书深度适配**：[Slash 确认](https://github.com/NousResearch/hermes-agent/pull/27358)和[中文本地化](https://github.com/NousResearch/hermes-agent/pull/21997) PR 都指向飞书适配的加强。飞书在亚洲市场占有率高，这些功能对吸引中国开发者至关重要。
- **可能的远期方向**：
    - **Agent 间通信 (A2A)**：虽未有关联 PR，但 Issue #514 热度极高，预示着项目可能会在未来路线图中重点考虑。
    - **性能优化**：[惰性工具加载](https://github.com/NousResearch/hermes-agent/issues/6839)和[提示缓存/KV Cache 修复](https://github.com/NousResearch/hermes-agent/issues/27339)都指向减少 token 消耗和延迟，这是所有用户的核心痛点。
- **背离信号**：
    - **“抄袭”争议**：多个关于抄袭 Evolver 架构的 Issue（#17688, #27266）得到社区附和，这是严重的社区信任危机。项目团队需要公开、透明地回应此事，否则会严重影响开源的公信力。

## 7. 用户反馈摘要

- **主要痛点**：
    - **配置复杂性**：`delegate_task` 的 `base_url` 配置完全失效（#27294），导致用户对多代理配置失去信任。
    - **迁移成本高**：v0.14.0 对模型上下文窗口的硬性要求，导致部分用户（特别是使用本地/小众模型的）服务彻底崩溃（#24140）。
    - **Token 浪费**：全量工具 Schema 注入导致的持续 token 消耗是普遍抱怨（#6839）。
- **使用场景**：
    - **WSL 环境问题**：用户尝试在 WSL 上使用 `/browser connect` 失败（#27018），暴露了跨平台兼容性问题。
    - **企业 IM 适配**：大量 Issue 和 PR 围绕 Slack、飞书、Wecom 等企业通讯软件的适配和集成，这是项目的主要落地场景。
- **满意度**：
    - **对功能的热情**：A2A 协议支持收获了远超其它 Feature 的积极反馈，显示创新性功能仍有巨大吸引力。
    - **对开源精神的质疑**：抄袭指控严重损害了项目的 **“社区信任”** 这一核心资产。

## 8. 待处理积压

- **#4402 - `gateway stop` 杀死所有配置文件** (`P2`, 2026-04-01)
    - [链接](https://github.com/NousResearch/hermes-agent/issues/4402)
    - **分析**：已积压 47 天，这是一个明显的功能性 Bug。在多配置文件成为标准操作的当下，一个错误的 `stop` 命令可能导致用户所有 gateway 服务中断，影响面极广。
- **#17688 & #27266 - 架构抄袭争议** (`无优先级`, 2026-04-30, 2026-05-17)
    - [链接](https://github.com/NousResearch/hermes-agent/issues/17688)
    - **分析**：社区讨论激烈，但项目方至今未做任何官方回应。这种沉默是对开源社区声誉的持续消耗，若不及时处理，可能演变为更严重的公关危机。**强烈建议项目维护者尽快介入并给出正式声明。**

---

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报 — 2026-05-17

---

## 1. 今日速览

过去 24 小时项目保持高度活跃：共更新 7 个 Issue（新开/活跃 6 条，关闭 1 条）、5 个 PR（待合并 4 条，合并/关闭 1 条），并发布了一个自动化 nightly 版本。社区讨论集中在 **exec 工具安全守卫误报**、**MCP 传输协议兼容** 以及 **新增 SiliconFlow 提供商** 等方向。整体来看，项目在功能扩展（多账号、新提供商）与稳定性修复（消息发布逻辑、UI 交互）上同步推进，代码库健康度良好。

---

## 2. 版本发布

**nightly: v0.2.8-nightly.20260517.0df050ff**

- 说明：自动化每日构建，可能包含不稳定改动，供早期验证使用。
- 完整变更日志：[v0.2.8…main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)
- 破坏性变更：无特别标注，升级前建议备份配置。

---

## 3. 项目进展

### 今日合并/关闭的 PR

| PR | 状态 | 说明 |
|----|------|------|
| [#2881 feat: 支持微信多账号配置](https://github.com/sipeed/picoclaw/pull/2881) | ✅ 已关闭 | 微信多账号管理的基础前端/后端实现，被新提交的优化版 PR #2883 替代。 |
| [#2885 feat(provider): add SiliconFlow provider support](https://github.com/sipeed/picoclaw/pull/2885) | 🔄 待合并 | 将 SiliconFlow 作为一等 OpenAI 兼容提供商加入，解决用户只能手动配置兼容模式的痛点。 |
| [#2883 feat: 支持微信多账号配置 (改进版)](https://github.com/sipeed/picoclaw/pull/2883) | 🔄 待合并 | 动态识别 `weixin_*` 格式的 config_key，前端支持多账号管理。 |
| [#2882 feat(chat): add independent code block copy and collapse controls](https://github.com/sipeed/picoclaw/pull/2882) | 🔄 待合并 | 增强 Web UI 代码块交互（独立复制/折叠），改进工具调用参数的 JSON 高亮。 |
| [#2835 fix(agent): always publish final reply after interim message](https://github.com/sipeed/picoclaw/pull/2835) | 🔄 待合并 (Stale) | 修复因 `message` 工具发送进度更新而导致最终回复被抑制的问题。 |

**总结**：项目在 **渠道扩展（微信多账号）**、**提供商接入（SiliconFlow）** 和 **前端体验优化** 上取得实质进展。微信多账号功能经过两次迭代已趋完善，SiliconFlow 支持即将落地。

---

## 4. 社区热点

- **#28 [Feat Request: LM Studio Easy Connect](https://github.com/sipeed/picoclaw/issues/28)**  
  评论数 19，👍 2，持续 3 个月未解决。用户请求简化 LM Studio 连接流程，反映对 **本地/自托管模型服务** 的强烈需求。

- **#1042 [[BUG] exec 工具 guardCommand 方法问题](https://github.com/sipeed/picoclaw/issues/1042)**  
  评论数 12，👍 2。`restrict_to_workspace=true` 时，合法命令（如 `curl`）因其路径被正则误判为越界而受阻，严重影响技能执行，社区讨论积极。

- **#2742 [[BUG] gateway starts with no channels in v0.2.8](https://github.com/sipeed/picoclaw/issues/2742)**  
  新近报告，v0.2.8 版本中 gateway 启动后通道列表为空（已启用 Telegram），导致服务不可用，需紧急排查。

---

## 5. Bug 与稳定性

| Issue | 严重程度 | 描述 | 是否有 Fix PR |
|-------|----------|------|---------------|
| [#2742 gateway 启动无通道](https://github.com/sipeed/picoclaw/issues/2742) | 🔴 高 | 配置正确但通道列表为空，v0.2.8 回归问题，影响服务启动。 | 暂无 |
| [#1042 exec 工具路径误判](https://github.com/sipeed/picoclaw/issues/1042) | 🟡 中 | `restrict_to_workspace` 导致 `curl` 等命令被拦截，阻塞天气技能等用例。 | 暂无，社区讨论中 |
| [#2782 MCP 不支持 Streamable HTTP](https://github.com/sipeed/picoclaw/issues/2782) | 🟢 中-（已关闭） | 已通过其他方式解决？该 Issue 已标记为关闭，但未关联具体 PR，需进一步确认。 | 关闭 |

此外，PR #2835 修正了 **agent 最终回复被中间消息抑制** 的 bug，属于影响用户体验的中等严重问题，目前待合并。

---

## 6. 功能请求与路线图信号

- **#2884 [Add siliconflow provider support](https://github.com/sipeed/picoclaw/issues/2884)**  
  用户希望将 SiliconFlow 作为独立提供商，避免手动兼容配置。同日已有 **PR #2885** 实现，预计将纳入下个正式版本。

- **#2421 [Add email as native channel](https://github.com/sipeed/picoclaw/issues/2421)**  
  提议邮件作为原生通道，面向企业/保守环境用户。虽已有 6 条评论，但无对应 PR，可能进入长期规划。

- **#2834 [Update from source](https://github.com/sipeed/picoclaw/issues/2834)**  
  用户请求升级教程，暴露文档缺失。项目可考虑提供 CLI 升级指南或自动更新机制。

- **微信多账号支持**（PR #2883）成熟度较高，预计随下个 nightly 或 v0.2.9 发布。

---

## 7. 用户反馈摘要

- **LM Studio 连接**（#28）：用户表达了强烈的“我做不到但希望有人实现”的诉求，表明社区对 **降低本地模型服务接入门槛** 有真实需求。
- **exec 工具安全误报**（#1042）：用户反映“命令根本不涉及任何路径却被阻止”，使用场景多为 **调用外部 API 获取数据（如天气）**，安全机制过度严格影响可用性。
- **升级困难**（#2834）：新手用户不清楚如何从旧版本升级，项目文档或引导流程尚不完善。
- **MCP 协议兼容**（#2782，已关闭）：用户报告无法连接只支持 Streamable HTTP 的 MCP 服务器，对应 Issue 关闭可能意味着已内部解决或已有替代方案。
- **SiliconFlow 配置繁琐**（#2884）：用户被迫使用 OpenAI 兼容模式，抱怨“不方便”，期待原生支持——已通过 PR #2885 快速响应。

---

## 8. 待处理积压

以下 Issue/PR 长期未获得维护者回应，建议优先关注：

| 编号 | 类型 | 创建时间 | 最后更新 | 现状 |
|------|------|----------|----------|------|
| [#28](https://github.com/sipeed/picoclaw/issues/28) | Enhancement | 2026-02-11 | 2026-05-17 | 3 个月未分配，添加 `stale` 标签但无实质性进展 |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | Bug | 2026-03-04 | 2026-05-17 | 严重安全误报，社区多次讨论仍无 PR |
| [#2421](https://github.com/sipeed/picoclaw/issues/2421) | Feature | 2026-04-08 | 2026-05-16 | 邮件通道需求明确，无排期 |
| [#2835](https://github.com/sipeed/picoclaw/pull/2835) | PR (Bug fix) | 2026-05-09 | 2026-05-16 | 修复 agent 回复抑制，已被标记 stale |

以上项目若继续搁置，可能影响用户信任与社区参与度。建议维护者下周至少评估 #1042 和 #2835 的优先级。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 NanoClaw 项目数据生成的 2026-05-17 项目动态日报。

---

# NanoClaw 项目动态日报 | 2026-05-17

## 1. 今日速览

今日项目活跃度很高，社区贡献积极。过去24小时内处理了11个PR，其中9个已成功合并或关闭，显示出高效的迭代节奏。同时，报告了6个新Issues，主要集中在部署配置、网络连接和消息可靠性等关键稳定性问题上。没有新版本发布，但多项重要修复和功能合并正在进行中，项目整体处于健康且快速迭代的状态。

## 2. 版本发布
无。

## 3. 项目进展

今日合并/关闭的重要 PR 展示了项目在功能扩展、Bug 修复和运维优化上的持续投入，整体向前迈进了一大步。

- **金融功能扩展（Phase 3）：** PR [#2486](https://github.com/nanocoai/nanoclaw/pull/2486)（Schema + Bootstrap）和 [#2487](https://github.com/nanocoai/nanoclaw/pull/2487)（Levis Behavior）均为 Finance Plan 3 改革的一部分，已合并。这标志着项目在构建特定领域的技能模板（Skill Template）方面取得了重要进展，为金融场景的自动化和智能化奠定了基础。
- **关键Bug修复：**
    - **Cron输出丢失修复：** PR [#2481](https://github.com/nanocoai/nanoclaw/pull/2481) 修复了 cron 调度任务的输出被“自我抑制”的严重问题。此前，Lili 和 Lobby 等代理的定时任务看似运行，但产出结果被静默丢弃，导致用户误以为任务未执行。此修复解决了核心调度逻辑的可靠性。
    - **WhatsApp适配器修复：** PR [#2469](https://github.com/nanocoai/nanoclaw/pull/2469) 修复了 WhatsApp 解码失败和 401 登出后的恢复指引，将不准确的 `launchctl kickstart` 建议替换为更有效的数据恢复指导，提升了用户侧的故障自愈能力。
- **新功能与架构实验：**
    - **CLI模式替代Agent SDK：** PR [#2470](https://github.com/nanocoai/nanoclaw/pull/2470) 引入了通过调用 `claude --print --resume` 命令实现的 CLI 模式，以替代原有的 Agent SDK。此改动旨在绕过 SDK 的配额限制，使用交互式配额，是项目在架构层面的一次重要探索。
    - **Telegram扩展支持：** PR [#2515](https://github.com/nanocoai/nanoclaw/pull/2515) 增加了对 Telegram 内联键盘按钮（Inline Keyboard Buttons）的支持，允许用户自定义可交互的按钮消息，显著增强了 Telegram 通道的用户交互体验。
- **运维与文档：**
    - PR [#2476](https://github.com/nanocoai/nanoclaw/pull/2476) 实现了“重启不依赖 NanoClaw”的功能，提升了系统健壮性。
    - PR [#2509](https://github.com/nanocoai/nanoclaw/pull/2509) 对齐了变更日志的版本发布说明格式，规范了文档流程。

## 4. 社区热点

今日社区的讨论焦点集中在 **消息传递的稳定性和去重机制** 上。

- **[OPEN] Issue #2506: send_message dedup silently drops responses when turns complete within 60 seconds of each other** ([链接](https://github.com/nanocoai/nanoclaw/issues/2506))
    - **分析师点评：** 这是今日讨论度最高的议题。用户 `mshirel` 报告的 Bug 描述了在特定时间窗口内（如两次对话结束间隔小于60秒），代理的响应会被静默丢弃，导致客户端超时并报错。该问题直击核心交互逻辑，影响了消息的可靠投递和用户体验。其高关注度反映了社区对 **消息传递零丢失** 的严苛要求。该 Issue 目前尚处于讨论阶段，但已经引起了维护团队的注意。

## 5. Bug 与稳定性

今日报告的Bug主要集中在部署、网络和极端场景下的容错处理，按严重程度排列如下：

- **严重：**
    - `#2512` **OneCLI与Postgres通信失败（已关闭）**：在Ubuntu默认安装下，OneCLI容器无法通过主机名访问同一Docker桥接网络中的Postgres数据库。这是部署基础配置的问题，已修复并关闭。
    - `#2513` **Colima + OneCLI CA证书问题**：在macOS的Colima环境下，绑定挂载的CA证书目录静默地变为空目录，导致容器内所有HTTPS请求失败。这是一个平台相关的严重问题，目前无修复PR，影响macOS用户的正常使用。
- **高：**
    - `#2516` **容器SIGKILL后outbound.db日志恢复**：容器在特定峰值被强制杀死时，可能留下损坏的数据库日志文件，导致主机投递轮询失败。这是一个非正常关闭后的数据一致性问题，需要优雅恢复机制。目前无修复PR。
    - `#2514` **Setup过程卡住（Needrestart Whiptail）**：Setup脚本因后台`needrestart`服务弹出交互式whiptail对话框而长时间挂起。此问题影响新手用户的首次部署体验，`b1rdex`用户已确认，目前无修复PR。
- **中：**
    - `#2517` **MGA引用已归档的agent_groups**：多代理组（MGA）引用了已被归档的代理组，可能导致配置引用失效。项目已发现此问题并提出了“归档时自动解除引用”和“GC清理”的解决方案，目前为开放状态。
    - `#2506` **send_message去重导致响应丢失**：如前文“社区热点”所述，是影响消息可靠性的严重Bug。目前无修复PR，但讨论热烈。

## 6. 功能请求与路线图信号

- **新增LLM提供商支持：** PR [#2518](https://github.com/nanocoai/nanoclaw/pull/2518) (OPEN) 提出新增 **Codex** 作为 LLM Provider，并在Agent容器中集成其CLI工具。这表明社区有意愿摆脱对单一模型提供商的依赖，走向多模型兼容的路线。该PR可能成为下一版本的核心功能之一。
- **架构演进方向：** PR [#2470](https://github.com/nanocoai/nanoclaw/pull/2470) (CLOSED) 的CLI模式，虽然不是直接的用户功能请求，但它反映了项目在 **规避API限制、优化成本** 方面的技术探索，这很可能成为未来平台化的一个关键特性。
- **数据一致性与垃圾回收：** Issue [#2517](https://github.com/nanocoai/nanoclaw/issues/2517) (OPEN) 提出的“归档时自动解除引用”和“GC”，虽然是Bug发现，但其解决方案本身是一个重要的功能需求。这指向项目需要建立更强的引用完整性检查和后台清理机制。

## 7. 用户反馈摘要

从今日的Issues评论中，我们可以提炼出以下用户痛点与场景：

- **痛点：消息可靠性焦虑。** 从Issue #2506的详细描述可以看出，用户对“消息被静默丢弃”这一现象非常敏感，因为这种行为会直接导致客户端超时，造成糟糕的用户体验。用户期望系统能够保证消息的 **原子性** 和 **可追溯性**。
- **痛点：平台兼容性与部署体验。**
    - **macOS用户：** Issue #2513 反映Colima用户面临HTTPS证书问题，部署门槛较高。
    - **新手用户：** Issue #2514 反映Setup过程被外部系统服务阻塞，缺乏静默或后台运行模式，影响“开箱即用”的体验。
- **痛点：灾难恢复能力。** Issue #2516 讨论了容器被SIGKILL后的恢复问题，用户关注的是系统在非正常终止后的 **自愈能力和数据完整性**。
- **满意度：功能认可。** PR [#2515](https://github.com/nanocoai/nanoclaw/pull/2515) 用户 `mkeizer` 贡献的Telegram内联键盘支持，虽然没有直接评论，但此类社区贡献本身即反映了用户对扩展通道交互能力有较高满意度。

## 8. 待处理积压

- **[OPEN] PR #2518: feat: add Codex provider** ([链接](https://github.com/nanocoai/nanoclaw/pull/2518))
    - **状态：** 新提交，待审查和合并。
    - **分析师提醒：** 这是增加新LLM Provider的关键PR，涉及架构变更。请维护者尽快指定Reviewer，评估其对现有Claude Provider的兼容性和资源消耗，以决定是否推进合并。
- **[OPEN] PR #2510: fix(cli): hydrate receiver inbound.db on approval-path destinations add** ([链接](https://github.com/nanocoai/nanoclaw/pull/2510))
    - **状态：** 昨日开放，待合并。
    - **分析师提醒：** 此修复涉及到审批流程相关的数据传输逻辑，可能直接影响用户体验。考虑到Issue #2516（outbound.db）也与数据库状态相关，建议将此PR与#2516的解决方案协同考虑，统一处理数据库的写操作和恢复逻辑。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 IronClaw 项目 GitHub 数据，我已为您生成 2026 年 5 月 17 日的项目动态日报。

---

## IronClaw 项目日报 | 2026-05-17

### 1. 今日速览

项目今日维持**高活跃度**开发状态，共记录 6 条 Issue 更新与 44 条 PR 更新，核心团队与贡献者协同效率高。**“Reborn”架构重构**进入密集合并期，多个重量级 PR（如组成根重构、FS 分发）被合并关闭，同时新提交的 Issues 聚焦于身份上下文、测试框架等关键模块的细节打磨。依赖项安全和 E2E 稳定性问题得到及时响应与修复，项目整体健康度良好，正稳步迈向 Beta 阶段。

### 2. 版本发布

无

### 3. 项目进展

今日共有 **18 个 PR 被合并/关闭**，其中多个关键 PR 推进了 Reborn 架构的落地与稳定性：

- **WebUI 线程范围绑定**：`[CLOSED]` - 通过 `#3724 [feat(reborn): webui turn scope]` 将 WebUI 调用者与线程 ID 绑定，防止 `submit_turn` 隐式创建线程，提升了系统的并发安全性与确定性。
- **安全漏洞修复**：`[CLOSED]` - `#3719 [chore(deps): bump deps to address security advisories]` 针对 `rustls-webpki`、`h2` 和 `tungstenite` 等关键依赖进行了安全更新，及时修复了 CRL 解析崩溃和 HTTP/2 重置风暴等多个 CVE 漏洞。
- **HTTP 工具文档替换**：`[CLOSED]` - `#3723 [[codex] replace agent-loop planning docs]` 移除了长期存在的 Reborn 骨架与规划文档，加入了更精炼的 CLAUDE.md 指引，标志着从规划期向实现期的过渡。
- **其他合并项**：还包括 `[CLOSED]` - 针对 `docs/architecture-video` 的依赖更新 (`#3417`) 等。

这些合并表明项目在**安全加固、模块边界收敛、以及核心模块文档化**方面取得了实质性进展。

### 4. 社区热点

今日讨论最活跃的 Issue 与 PR 均与“Reborn”架构的模块组成和计划紧密相关：

- **[OPEN] Issue #3692 - “Reborn: add policy-gated personal identity and heartbeat prompt context”** - [链接](nearai/ironclaw Issue #3692)
    - **分析**：该 Issue 由核心开发者 `henrypark133` 创建，有 4 条评论。它探讨了如何将用户个人身份和“心跳”上下文纳入提示策略。这反映了社区在推进 Reborn 时，对**细粒度、策略驱动的上下文控制**的深层需求，是构建个性化 Agent 体验的关键一环。

- **[OPEN] Issue #3036 - “[EPIC] Configuration-as-Code for IronClaw Reborn: tenant blueprints and use-case harnesses”** - [链接](nearai/ironclaw Issue #3036)
    - **分析**：作为 EPIC 问题，虽然有 1 个赞和持续讨论，但更新日期为昨天。它代表了社区对**声明式、可审计的配置管理**的长期诉求，旨在摆脱混杂的 `.env` 文件和 JSON 配置。该 EPIC 的最新状态需要项目组内部跟进。

- **[OPEN] PR #3695 - “arch(reborn): consolidate composition root, narrow public surface, ship live binary”** - [链接](nearai/ironclaw PR #3695)
    - **分析**：此 PR 是今日多个其他 Reborn PR（如 #3717, #3721）的前置或依赖。评论数未显示，但其 “XL” 大小和“Core”贡献者标签表明它是推动项目结构从“计划”走向“可运行二进制”的基石，社区对其后续进展高度关注。

### 5. Bug 与稳定性

- **严重 - CI 持续失败**：`[OPEN]` - **Issue #3447** “[Nightly E2E failed]” - [链接](nearai/ironclaw Issue #3447)
    - **描述**：Nightly E2E 测试持续失败，影响 `v2-engine` 作业。该 Issue 已存在一周多 (2026-05-10)，虽今日有更新，但仍未关闭。
    - **关联修复**：新提交的 **PR #3702** ([链接](nearai/ironclaw Issue #3702) ) 正是针对此问题提出了“二进制-E2E测试框架计划”，作为 `#3698` 的后续行动。表明核心团队已将该问题列为高优先级，并通过重构测试框架来解决此根本问题。

- **中等 - E2E 稳定性**：新创建的 **Issue #3702** “[Reborn: revise and implement binary-E2E test framework plan]” - [链接](nearai/ironclaw Issue #3702)
    - **描述**：此 Issue 系统性地规划了如何重写 E2E 测试，旨在解决已有的失败问题，并为 Reborn 架构提供可靠的回归保障。它本身就是对当前缺陷的响应。

- **中低 - 依赖安全**：`[CLOSED]` - **PR #3719** 已成功修复多个依赖安全漏洞。但一个大型的依赖更新 `#3361`（含 43 个包）和 `#3360` (tokio 生态) 仍处于 `[OPEN]` 状态，需要主要维护者审核。

### 6. 功能请求与路线图信号

- **配置即代码**：`[OPEN]` - **Issue #3036** [链接] 所提出的 EPIC 是路线图上的长期目标。虽然尚未关联具体 PR，但新提交的 **PR #3704** ([链接](nearai/ironclaw PR #3704)) “feat(reborn): boot TOML + provider catalog”，通过实现配置文件 `config.toml` 和 `providers.json`，**直接呼应并推进了**该 EPIC 的需求。这强烈表明配置即代码的能力**极有可能被纳入下一个版本**。

- **第一方 HTTP 工具**：`[OPEN]` - **PR #3681** ([链接](nearai/ironclaw PR #3681)) 正在开发中，为 Reborn 提供内置的 HTTP 请求能力。这是一个贴近用户需求的实质功能请求。

- **个人上下文策略**：`[OPEN]` - **Issue #3692** [链接] 和相关的 **PR #3721** ([链接](nearai/ironclaw PR #3721)) 显示了项目对用户隐私和个性化控制平衡的关注。`PR #3721` 通过 `ResolvedRunProfile.personal_context_policy` 实现策略门控，是这一特性落地的第一步。

### 7. 用户反馈摘要

由于今日数据未提供具体评论内容，以下分析基于 Issue/PR 主题和上下文推断：

- **稳定性改善备受好评**：针对 `Nightly E2E` 持续失败，社区（可能通过内部讨论）推动了 `Issue #3702` 的重写测试框架计划，表明用户对 CI 稳定性的**信任恢复**高度期待。
- **对声明式配置的强烈渴望**：`Issue #3036` 的持续关注，结合 `PR #3704` 的落地，暗示用户对“编辑 `.env`”的手动操作感到厌倦，期待**开发体验的现代化升级**。
- **对 WebUI 线程安全性的隐忧**：`PR #3725` 和 `PR #3724` 对 WebUI 线程范围进行的详细绑定与防范，可能源于对并发场景下竞态条件的真实反馈。

### 8. 待处理积压

- **CI 稳定性问题**：`[OPEN]` - **Issue #3447** “[Nightly E2E failed]” - [链接](nearai/ironclaw Issue #3447)
    - **提醒**：该 Issue 已开放超一周，尽管有修复计划，但仍标记为 `[OPEN]`。每日失败的 CI 对团队和外部贡献者的信心均有影响，建议尽快指派优先级。

- **大型依赖更新积压**：`[OPEN]` - **PR #3361** ([链接](nearai/ironclaw PR #3361)) 及 **PR #3360** ([链接](nearai/ironclaw PR #3360)) 等由 `dependabot` 创建的大型群组更新已开放 10 天以上，包含 40+ 个依赖项。这些更新通常包含大量破坏性变更（如 `#3361` 中的 `agent-client-protocol` 从 `0.10.2` 到 `0.11.1`），需要核心维护者投入精力评审与测试，长期积压会增加合并冲突风险。

- **EPIC 问题缺乏进展更新**：`[OPEN]` - **Issue #3036** ([链接](nearai/ironclaw Issue #3036))
    - **提醒**：尽管有相关的 `PR #3704`，但该 EPIC 本身缺乏最近的状态标记更新（如添加 `in-progress` 标签或拆分子任务），建议维护者及时更新，以保持社区对齐。

---

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 LobsterAI GitHub 数据，我为您生成了 2026-05-17 的项目动态日报。

---

### **LobsterAI 项目动态日报 (2026-05-17)**

**分析师点评：** 项目在今日展现出一种“表面平静，内里活跃”的状态。虽然新 Issue 数量不多，但 PR 合并与提交非常频繁，特别是通过一次版本整合集中关闭了多项优化与修复。值得注意的是，长期积压的 PR 多达 9 个，这可能预示着代码评审或 CI 流程存在瓶颈，需要团队关注。

---

### **1. 今日速览**

- **整体活跃度：高**。尽管仅收到 1 条新 Issue，但社区贡献者提交了大量代码，24 小时内共有 16 条 PR 活动，其中一半（8 条）已完成合并或关闭。
- **版本迭代节奏：** 今日无正式版本发布，但通过合并 `release/2026.5.15` 分支，将多个功能优化和 Bug 修复整合进了主分支，为下一个正式版本奠定了坚实基础。
- **合并效率：** 过去 24 小时合并/关闭了 8 个 PR，涵盖了从 UI 优化到核心性能提升等多个方面，项目整体向前迈进了一大步。
- **潜在风险：** 仍有 8 个 PR 处于待合并状态，其中 7 个已标记为“stale”（陈旧），创建时间超过 50 天。这反映出功能合并流程可能存在积压，需要尽快处理以避免分支冲突和社区贡献者流失。

### **2. 版本发布 (2026-05-17)**

- **无**
- 今日无新版本发布。但通过内部版本合并 (PR #1998)，已为下一个版本准备好多项更新。

### **3. 项目进展**

过去 24 小时内，项目通过一系列 PR 的合并，推进了多个核心领域的优化和修复。以下是今日的“版本集成”及其关闭的相关重要更新：

- **核心版本集成 (PR #1998):** 这是一个重要的里程碑。名为 `Release/2026.5.15` 的集成分支被合并到主分支，一次性整合了多项改进。这些改进包括：
    - **产品修复与构建**: 关键 `Keyfrom/channel` 的构建与归因工作。
    - **用户体验增强**: 优化了 **Artifacts** 的多 Tab 预览功能、**IM** 端的新手引导。
    - **功能完善**: 修复了 `mimo` 模型的推理内容问题，并优化了 **Dream UI**。
    - **链接:** [netease-youdao/LobsterAI PR #1998](https://github.com/netease-youdao/LobsterAI/pull/1998)

此外，今日还单独关闭了多项对特定问题的修复和优化：

- **模型缺陷修复**: `fix: reasoning_content returned in multi-turn sessions for mimo model` (#1999， #1994) 解决了多轮对话中 `mimo` 模型推理内容返回异常的问题，这是社区反馈中的关键痛点。
    - **链接:** [PR #1999](https://github.com/netease-youdao/LobsterAI/pull/1999)
- **默认模型更新**: `chore: update default models for providers` (#1997) 更新了提供商的默认模型，确保用户开箱即用体验。
    - **链接:** [PR #1997](https://github.com/netease-youdao/LobsterAI/pull/1997)
- **UI/UX 优化**: `chore: optimize dream ui` (#1996， #1995) 对“梦境”功能界面进行了持续优化。
    - **链接:** [PR #1996](https://github.com/netease-youdao/LobsterAI/pull/1996)
- **性能优化 (已关闭):** 针对 SQLite 数据库写入阻塞主线程的问题，`perf(sqlite)` (#812) 通过防抖和异步写入方案减少了性能瓶颈，目前该 PR 已合并。
    - **链接:** [PR #812](https://github.com/netease-youdao/LobsterAI/pull/812)
- **新功能 (已关闭):** 新增了 **Skill 执行统计** 功能 (#871)，允许用户查看每个 Skill 的调用统计数据。
    - **链接:** [PR #871](https://github.com/netease-youdao/LobsterAI/pull/871)

### **4. 社区热点**

- **单一 Issue 成为唯一焦点：** 今日新增的唯一 Issue (#1993) 成为了社区讨论的绝对中心。
    - **Issue #1993 (打开)**: `AI engine connection lost issue`
    - **热度分析**: 用户 `Shun-Calvin` 报告在桌面应用端持续遭遇“AI 引擎连接丢失”问题，强调在使用 IM Bot 时连接稳定。这引发了对于桌面客户端网络适配性或内部连接机制的讨论。评论区有 1 条回复。
    - **核心诉求**: 用户期望桌面应用具备与 IM Bot 同等的连接稳定性。这可能指向 Electron 底层网络栈的特定问题，或代理/防火墙配置的兼容性不足。
    - **链接:** [Issue #1993](https://github.com/netease-youdao/LobsterAI/issues/1993)

### **5. Bug 与稳定性**

- **[严重] AI 引擎连接丢失 (桌面客户端)**: **Issue #1993 (打开)**。用户反映在桌面应用上频繁断开连接，严重影响核心功能使用。目前暂无关联的修复 PR。
    - **影响面**: 影响所有桌面客户端用户，是新用户流失的潜在风险。
    - **链接**: [Issue #1993](https://github.com/netease-youdao/LobsterAI/issues/1993)

- **[中等] mimo 模型多轮对话推理内容问题 (已修复)**: **PR #1999， #1994 (已关闭)**。针对 `mimo` 模型在延续对话场景下返回的 `reasoning_content` 异常，今日已通过两个 PR 完成修复，并随版本更新合入。
    - **链接**: [PR #1999](https://github.com/netease-youdao/LobsterAI/pull/1999)

### **6. 功能请求与路线图信号**

- **“自动检测” API 格式**: **PR #762 (待合并, 陈旧)**。该 PR 提出了为多个模型提供商（如DeepSeek、智谱）的 API 格式选择增加“自动检测”选项，降低用户配置门槛。此功能在此次版本整合中未提及，但作为待合并的陈旧 PR，显示出社区对此类易用性改进的持续需求。如果被采纳，将是下一版本的潜在亮点。

- **可观测性集成**: **PR #768 (待合并, 陈旧)**。引入了 **Opik** 作为首个可观测性提供商，通过插件形式捕获调试数据。这标志着项目开始重视开发者工具和性能监控，是一个重要的方向性信号。由于处于陈旧状态，其进展取决于维护者对此类功能的优先级判断。

### **7. 用户反馈摘要**

- **痛点反馈 (连接稳定性)**: 来自 Issue #1993。用户核心痛点是桌面应用的连接稳定性远不如 IM Bot。这表明产品的不同模块（桌面端 vs IM）可能使用了不同的网络实现或依赖库，导致体验不一致。用户可能因“被迫重启”而产生挫败感，这在 Copilot 类工具中是致命的体验问题。
    - **用户原话**: “...it always show AI engine connection lost. If I use IM Bot， the connection is stable.”

### **8. 待处理积压 (Call for Attention)**

以下为长期未被合并的重要 Pull Requests，建议维护者优先关注并推动评审与合并：

1.  **PR #762**: `feat(settings): 自定义模型 API 格式新增”自动检测”选项` (2026-03-24 创建)
    - **影响**: 影响所有新用户及非技术用户的模型配置体验。积压 54 天，有较大价值。
    - **链接**: [PR #762](https://github.com/netease-youdao/LobsterAI/pull/762)
2.  **PR #768**: `feat(observability): add Opik observability integration via OpenClaw plugin` (2026-03-24 创建)
    - **影响**: 重要的开发者基础设施功能，能显著提升项目调试和问题定位效率。积压 54 天。
    - **链接**: [PR #768](https://github.com/netease-youdao/LobsterAI/pull/768)
3.  **PR #788**: `fix(scheduled-task): deduplicate tasks before migration` (2026-03-25 创建)
    - **影响**: 修复了应用重启时可能重复创建定时任务的严重问题。积压 53 天。
    - **链接**: [PR #788](https://github.com/netease-youdao/LobsterAI/pull/788)
4.  **PR #1766**: `chore(deps-dev): bump vite from 5.4.21 to 8.0.13` (2026-04-20 创建)
    - **影响**: 构建工具的跨大版本更新，通常包含安全修复和性能改进，但也可能存在兼容性问题。拖得越久，迁移成本越高。积压 27 天。
    - **链接**: [PR #1766](https://github.com/netease-youdao/LobsterAI/pull/1766)

---

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 (2026-05-17)

## 今日速览

项目在过去24小时内保持活跃：共收到3个新Issues（均为Bug报告）和2个新Pull Requests（功能增强），但无任何Issue或PR被关闭/合并，也无新版本发布。整体来看，社区反馈集中在配置序列化缺陷和模型推理标签处理问题上，同时远程访问与API兼容性功能正在稳步推进。项目活跃度中等，但合并及解决积压的节奏有待提升。

---

## 项目进展

今日无已合并或关闭的Pull Requests，因此项目主干代码未发生变更。不过有两个重要的功能PR正处于开放状态，若成功合并将显著增强项目能力：

- **#1002** [feat(remote-access): add NetBird and Cloudflare Tunnel support](https://github.com/moltis-org/moltis/pull/1002)  
  由penso提交，涵盖NetBird私有Mesh网络与Cloudflare Tunnel的配置、CLI命令、REST路由及运行时控制器，并包含WebAuthn主机名更新与令牌处理。该PR将大幅简化远程访问的部署场景。

- **#1005** [feat(openai-codex): add reasoning effort support](https://github.com/moltis-org/moltis/pull/1005)  
  由PeterDaveHello提交，为OpenAI Codex克隆实例传递 `reasoning_effort` 参数，并在Responses API请求中序列化配置的GPT-5 Codex effort值，同时保持对加密推理内容的向后兼容。

这两个PR代表项目在基础设施（远程访问）与核心API兼容性（OpenAI Codex）上的重要进展，建议维护者尽快审阅。

---

## 社区热点

今日讨论活跃度偏低，所有Issue和PR均无评论。但从提交者背景来看：

- **#1004** [Feature: Non-blocking spawn_agent — parent session stays responsive during long sub-agent runs](https://github.com/moltis-org/moltis/issues/1004)  
  由dmitriikeler提出，要求 `spawn_agent` 不阻塞父agent的LLM回合，以便长时间运行的子agent不会挂起整个会话。这是针对多Agent协作场景的核心用户体验需求，虽无评论，但其设计影响到会话响应性，是社区关注的高价值功能请求。

---

## Bug 与稳定性

今日新增两个Bug报告，均无关联修复PR，需优先关注：

- **#1007** [Bug: gemma-4-31b-it reasoning tags (&#x3C;thought&#x3E;) are treated as plain text instead of reasoning blocks](https://github.com/moltis-org/moltis/issues/1007)  
  **严重性：高** – `gemma-4-31b-it` 模型的 &#x3C;thought&#x3E; 标签未被识别为推理块，导致模型输出解析错误，影响所有使用该模型的用户。作者已确认使用最新版Moltis并搜索了已有issue未发现重复。

- **#1006** [Bug: VoiceCoquiTtsConfig defaults are stripped during auto-compact, causing config &#x27;disappearance&#x27;](https://github.com/moltis-org/moltis/issues/1006)  
  **严重性：中** – 自动压缩（auto-compact）过程中错误地剥离了VoiceCoquiTtsConfig的默认值，导致配置项“消失”，影响TTS功能正常使用。作者未勾选“在聊天会话中发生”选项，可能为配置持久化或序列化逻辑缺陷。

---

## 功能请求与路线图信号

- **#1004** [Non-blocking spawn_agent](https://github.com/moltis-org/moltis/issues/1004)  
  作为新增功能请求，若与已存在的 #1002（远程访问）和 #1005（Codex推理努力）结合，可推断项目下一版本将聚焦于**多Agent协作**与**远程访问**两大方向。建议维护者评估该请求与现有架构的兼容性，并考虑纳入后续里程碑。

- **#1005** (PR) 对OpenAI Codex的 `reasoning_effort` 支持，表明项目正在积极跟进OpenAI最新API能力，有助于保持与前沿模型的兼容性。

---

## 用户反馈摘要

今日所有Issue和PR暂无评论，因此无法形成直接的社区反馈摘要。但从Bug描述可以间接看出用户的两类主要痛点：

1. 模型推理标签解析不完整（#1007），影响高级模型的使用体验。
2. 配置自动压缩期间丢失默认值（#1006），表明配置序列化/反序列化逻辑存在边界情况未被覆盖，降低了配置可靠性。

---

## 待处理积压

以下重要Issue或PR尚未取得进展，建议维护者优先关注：

| 链接 | 类型 | 状态 | 提及原因 |
|------|------|------|----------|
| [#1002](https://github.com/moltis-org/moltis/pull/1002) | PR | Open | 远程访问核心功能，已停留2天未审 |
| [#1005](https://github.com/moltis-org/moltis/pull/1005) | PR | Open | OpenAI Codex新能力，等待合并 |
| [#1007](https://github.com/moltis-org/moltis/issues/1007) | Bug | Open | 高严重性，无任何响应 |
| [#1006](https://github.com/moltis-org/moltis/issues/1006) | Bug | Open | 配置功能回归，需快速确认 |

此外，长期未更新的Issue（如发布时间超过两周且无维护者回应的）今日未统计到，建议维护者定期盘点所有Open状态的Issues以清理积压。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目日报 — 2026-05-17

---

## 今日速览

过去 24 小时内，CoPaw 项目保持**高活跃度**：共处理 16 条 Issue（其中新开/活跃 13 条，关闭 3 条）和 12 个 PR（待合并 8 个，已合并/关闭 4 个）。社区贡献者持续发力，既有针对核心功能（如多技能路径、轻量级 Goal 模式）的提案，也有大量前端 E2E 测试基础设施的搭建。然而 **2 个关键 Bug 报告**（聊天无响应、`/mission` 指令冻结）直接影响了用户正常使用，需引起团队紧急关注。整体项目健康度尚可，但稳定性修复急需加速。

---

## 版本发布

**无新版本发布**。上一个稳定版本仍为 v1.1.7，未触发新的 Release。

---

## 项目进展

今日合并/关闭了 **4 个 PR**，涵盖数据迁移清理、工作路径修复、文件抓取 Bug 及 QQ 频道体验优化：

| PR | 标题 | 要点 |
|----|------|------|
| [#3605](https://agentscope-ai/QwenPaw/pull/3605) | `refactor(wechat): centralize legacy weixin → wechat data migrations` | 将微信标识符重命名的遗留数据迁移集中在 `Workspace.start()` 中，消除运行时回退路径，提升启动一致性。 |
| [#1669](https://agentscope-ai/QwenPaw/pull/1669) | `fix(Workspace): handle path separators correctly` | 修复 Windows 系统下工作区路径持续显示 "loading..." 的 bug，路径分隔符检测逻辑已修正。 |
| [#1661](https://agentscope-ai/QwenPaw/pull/1661) | `fix(workspace): fix memory files not being fetched by agent ID` | 每日记忆文件原使用全局 API，未能按当前 Agent/Bot 文件夹获取；现在改为按 Agent ID 正确查询。 |
| [#3246](https://agentscope-ai/QwenPaw/pull/3246) | `feat(qq): add configurable instant acknowledgment message` | 为 QQ 频道增加可配置的即时确认消息（弥补其缺少 typing 指示器的缺陷），提升用户等待感体验。 |

此外，还有 **8 个待合并 PR** 正在评审中，其中 **3 个** 直接修复并发状态泄漏、shell 超时、runner 包轻量化等核心稳定问题，建议优先处理。

---

## 社区热点

1. **[#4455 — feat(skills): support multiple external skill paths via config](https://agentscope-ai/QwenPaw/issues/4455)**  
   - **评论 5 条**，为今日最多讨论的 Issue。  
   - 用户 `xielevi` 提出允许在 `config.json` 中配置多个额外技能目录，使外部工具安装的技能（skill hub、共享目录等）可被发现。  
   - 该需求直指技能生态扩展痛点，得到社区共鸣，很可能被纳入下一版本规划。

2. **[#4453 — 聊天窗口聊天无回应](https://agentscope-ai/QwenPaw/issues/4453)**  
   - 收到 3 条评论，且获得 **1 个 👍**（对问题表示认同）。  
   - 用户 `xiangxinghe` 遇到消息发送后无响应，后端报错 `RuntimeError: Event loop stopped before Future completed`，且切换模型、重启 Docker、回退版本均无效。该问题影响核心使用场景，是今日最严重的用户反馈。

3. **[#4458–#4462 — E2E UI smoke tests 系列 Issue](https://agentscope-ai/QwenPaw/issues?q=is%3Aissue+author%3Ahanson-hex+created%3A2026-05-17)**  
   - 由贡献者 `hanson-hex` 在同一时间批量创建 **5 个 E2E 测试相关 Issue**（#4457 基础设施迁移 + #4458–#4462 各页面烟雾测试）。  
   - 虽单条评论不多，但代表社区主动构建自动化测试体系的意愿，是项目质量提升的积极信号。

---

## Bug 与稳定性

以下为今日报告的 Bug，按严重程度排列：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|----------|-------|------|----------------|
| **🔴 致命** | [#4453](https://agentscope-ai/QwenPaw/issues/4453) | 聊天窗口完全无响应，后端 `Event loop stopped` 错误；切换模型/重启均无效。用户会话瘫痪。 | 无 |
| **🔴 致命** | [#4454](https://agentscope-ai/QwenPaw/issues/4454) | 执行 `/mission` 指令后 Console 界面完全卡死，`/missions/` 目录清空亦无法恢复。进程存活但界面无响应。 | 无 |
| **🟡 高** | [#4448 / #4447](https://agentscope-ai/QwenPaw/issues/4448) | 长对话中 `Context compaction` 频繁失败，报 `invalid format (missing ## header)`。影响上下文管理与对话连贯性。 | 无 |
| **🟡 高** | [#4449](https://agentscope-ai/QwenPaw/issues/4449) | 模型 429 限流 → `zero_downtime_reload` 清空全部 pending 消息队列，导致 Agent 冻结，用户消息永久丢失。 | 无 |
| **🟢 低** | [#4445](https://agentscope-ai/QwenPaw/issues/4445) | `qwenpaw.app.runner.*` 包初始化时臃肿地导入了整个运行栈，带来不必要的依赖耦合。已有 Fix PR [#4446](https://agentscope-ai/QwenPaw/pull/4446) 进行轻量化改造。 | ✅ #4446 |

**提醒**：#4453 和 #4454 两个致命 Bug 尚无任何配套修复 PR，建议核心维护团队优先排查根因。

---

## 功能请求与路线图信号

| Issue/PR | 类型 | 内容 | 路线图契合度 |
|----------|------|------|--------------|
| [#4455](https://agentscope-ai/QwenPaw/issues/4455) | 功能请求 | 支持通过 `config.json` 配置多个外部技能搜索路径，打通第三方技能管理工具 | ⭐⭐⭐⭐ 高价值生态扩展 |
| [#4450](https://agentscope-ai/QwenPaw/issues/4450) | 功能请求 | 简化审批命令：`/approve` / `/deny` + `/session` / `/always` / `/reset` 作用域支持 | ⭐⭐⭐ 提升交互效率 |
| [#4451](https://agentscope-ai/QwenPaw/issues/4451) | 功能请求 | Telegram/QQ 频道中使用按钮形式的交互式工具审批（WebUI 已支持） | ⭐⭐⭐ 跨渠道体验统一 |
| [#4443](https://agentscope-ai/QwenPaw/pull/4443) | 已实现 PR | 轻量级 `/goal` 模式，支持 session 级目标注入与状态管理 | ⭐⭐⭐ 实用性较强的微创新 |
| [#4444](https://agentscope-ai/QwenPaw/pull/4444) | 已实现 PR | xAI OAuth + Grok 提供者 + 图像/视频工具插件 | ⭐⭐⭐⭐ 新模型/能力接入 |

**判断**：上述功能请求大多已有明确实现思路或对应 PR，预计将随下一版本（v1.2.0）一同发布，尤其是外部技能路径和多渠道审批按钮。

---

## 用户反馈摘要

从 Issue 评论中提炼真实用户痛点：

- **“聊天窗口无回应，切换模型也没用，重启 Docker 没用，回退版本也没用”**（#4453）—— 用户已穷尽所有常规排查手段，问题依然存在，表明 Bug 可能在基础运行时（事件循环或信道层）有深层次缺陷。
- **“清空 `~/.copaw/workspaces/default/missions/` 并重置 session 仍然卡死”**（#4454）—— 对于 `/mission` 命令的冻结，用户尝试了数据清理，但问题依然复现，推测是前端事件处理或后端状态机死锁。
- **“Context compaction 在长对话中频繁失败，严重影响使用”**（#4448）—— 用户明显是在持续使用中遇到该错误，高频出现说明 Context compaction 算法在处理用户自定义格式时存在漏洞。
- **“模型 429 限流后消息队列被清空，Agent 冻结，用户消息丢失”**（#4449）—— 这是运维场景下典型的“坑”：限流后的兜底策略（`zero_downtime_reload`）反而更粗暴地清空了消息，用户体验很差。

整体上，**核心聊天与指令功能的可靠性**是最让用户不满的地方；而功能扩展（技能路径、审批按钮）则获得积极期待。

---

## 待处理积压

以下为**长期未响应或处于停滞状态的重要 Issue / PR**，提醒维护者关注：

| 类型 | 编号 | 标题 | 创建时间 | 当前状态 | 备注 |
|------|------|------|----------|----------|------|
| PR | [#2771](https://agentscope-ai/QwenPaw/pull/2771) | `fix(install): restrict mlx-lm to Apple Silicon macOS` | 2026-04-01 | 待合并（Under Review） | **47 天未合并**，首次贡献者，可能因 CI 或评审资源不足而卡住。 |
| PR | [#4041](https://agentscope-ai/QwenPaw/pull/4041) | `feat(cli-desktop): system tray startup item function` | 2026-05-05 | 待合并（Under Review） | 12 天无更新，Windows 系统托盘功能，实用但并非紧急。 |
| PR | [#4173](https://agentscope-ai/QwenPaw/pull/4173) | `fix(shell): Unix 临时文件重定向避免超时挂起` | 2026-05-10 | 待合并 | 修复 `execute_shell_command` 后台进程导致 `communicate()` 挂起的问题，对自动化脚本用户很重要。 |
| PR | [#4303](https://agentscope-ai/QwenPaw/pull/4303) | `fix(cron): isolate non-shared runs` | 2026-05-14 | 待合并 | 确保 Cron 作业非共享会话使用独立 Session ID，避免会话复用导致的上下文混乱。 |
| PR | [#4084](https://agentscope-ai/QwenPaw/pull/4084) | `fix(crons): eliminate concurrency state leaks in CronManager` | 2026-05-07 | 待合并 | 修复并行运行、删除任务、启停循环中的状态泄漏，是 Cron 功能稳定性的关键修复。 |

**建议**：维护团队可优先合并 `#2771`（长期积压的首个贡献者 PR）以及 `#4303` / `#4084`（直接影响 Cron 稳定性的修复），以改善社区贡献体验并降低潜在风险。

---

*以上数据均来自 CoPaw 项目 GitHub 公开活动，截止 2026-05-17 UTC。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为ZeroClaw开源项目的AI分析师，以下是根据您提供的GitHub数据生成的2026年5月17日项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-05-17

## 今日速览

今日ZeroClaw项目活跃度极高。过去24小时内，有50个Issues和50个PR被更新，其中包含45个新开的活跃Issues和44个待合并的PR，显示社区贡献热情高涨。项目正处在关键版本迭代期，高风险Bug（#5600）和大型功能PR（#6398, #6649）的持续讨论是今日焦点。此外，5个Bug被顺利关闭，表明维护团队对关键问题的响应迅速。

## 项目进展

今日有6个PR被合并或关闭，同时5个Issues被关闭，项目在稳定性和功能交付上均有推进。

- **关闭的重要Bug:**
    - **#6123: [Bug]: default_model issue on fresh install** - 一个新安装时的默认模型问题已被确认并修复，解决了用户首次上手的障碍。
    - **#6399: [Bug]: Custom remote provider sends local image file paths instead of data URLs** - 修复了自定义远程提供商错误传递本地图片路径的问题，保障了多模态功能的正常运行。
    - **#6659: [Bug]: No API for pushing notifications into an operator's gateway session** - 为操作员网关会话添加了推送通知的API，增强了平台的可扩展性。
    - **#6132: [Bug]: audit(#5972 follow-up): extend manifest prompt audit** - 作为安全审计的一部分，拓展了提示词注入检测范围，是#5972合并后的重要跟进。
    - **#3542: [Feature]: Webhook endpoint can support agent mode** - 该功能请求已实现，Webhook端点现在可以触发完整的代理工作流。
- **合并的PR:**
    - **#6728: feat(web-dashboard): M5.0** - 合并了Dashboard M5.0更新，新增了概览页面，为项目管理提供了更直观的视图。

这些进展表明项目在修复初期缺陷的同时，正逐步兑现社区期待已久的重要功能（如Webhook Agent模式），并持续强化安全基础设施。

## 社区热点

今日讨论最活跃的Issues反映了用户的核心痛点和对高级功能的迫切需求。

1.  **#5600: [Bug]: Use kimi-code provider in streaming chat call tools, provider API reports an error** (评论: 8)
    - **链接:** [Issue #5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)
    - **分析:** 这是一个自4月10日起就存在的严重Bug，涉及到Kimi-Code提供商在流式调用工具时API报错。该问题被标记为`priority:p1`和`r:needs-repro`，说明维护者已识别其重要性，但复现或根因分析遇到了困难。用户`hvvvvvvv`的持续关注（8条评论）和1个赞，表明这是一个对特定用户群体影响较大的阻塞性问题。

2.  **#2467: [Feature]: Webhook transforms** (评论: 5)
    - **链接:** [Issue #2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467)
    - **分析:** 这是一个创建于3月初的长期功能请求，要求Webhook能支持任意payload的转换。虽然#3542解决了Webhook的Agent模式，但#2467提出的`transforms`功能更为底层和通用。社区用户`MexHigh`给出的使用案例（GitHub Webhook）具有很强的代表性，显示出用户希望将ZeroClaw无缝集成到现有工作流中的强烈诉求。

3.  **#5601: [Feature]: Add subscription-native OAuth support for Ollama Cloud, z.ai (zhipu), Kimi (Moonshot), and MiniMax providers** (评论: 5)
    - **链接:** [Issue #5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)
    - **分析:** 这是一个很强的产品改进信号。用户`dolsol3`提议为多个主流国产和开源云服务商添加原生的OAuth支持，以消除管理静态API密钥的痛点。当前ZeroClaw仅支持少数服务商的OAuth，该Issue获得了1个赞，并引来了5条评论讨论细节，表明社区对简化各项AI提供商接入方式的普遍期待。

## Bug 与稳定性

今日报告了多个影响可用性的Bug，部分已有修复PR提交。

**严重程度高 (S1 - 工作流阻塞):**
- **#5600:** [Bug]: Use kimi-code provider in streaming chat call tools... (状态: `blocked`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)
- **#6399:** [已关闭] 自定义远程提供商的多模态请求Bug。 [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6399)

**严重程度中 (S2 - 行为降级):**
- **#6269:** [Bug]: Context compressor drops reasoning_content from compressed assistant messages (状态: `in-progress`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6269)
- **#6739:** [Bug]: Cron timezone contract is inconsistent across tools, CLI, and API (状态: `OPEN`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6739)
- **#6734:** [Bug]: Qwen 3.6 tool-call envelopes can leak into Matrix replies (状态: `OPEN`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6734) - **已有Fix PR #6736**
- **#6733:** [Bug]: Matrix streaming draft state is keyed only by room (状态: `OPEN`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6733) - **已有Fix PR #6735**
- **#6721:** [Bug]: tool_search not in default_auto_approve... (状态: `OPEN`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6721)
- **#6724:** [Bug]: Channels supervisor crashloops when all configured channels have enabled=false (状态: `OPEN`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6724)
- **#6723:** [Bug]: Native OpenAI provider hardcodes 120s request timeout... (状态: `OPEN`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6723)

**其他Bug:**
- **#6683:** [Bug]: skill_manage `patch` ignores cooldown... (状态: `in-progress`) [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6683)

**总结:** 今日Bug报告聚焦于**流式处理**（#5600）、**上下文压缩**（#6269）、**渠道集成**（#6734, #6733, #6721, #6724）和**配置解析**（#6739, #6723）这几个核心领域。特别是多个关于Matrix和Cron的Bug，显示近期对这些功能的改进可能引入了回归或需要进一步打磨。

## 功能请求与路线图信号

社区对新功能的讨论依然活跃，许多请求指向了下一版本的可能演进方向。

- **开发者体验与平台集成:**
    - **#5994: [Feature]: Build Official Website + End-to-End Documentation** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5994) - 呼声很高，旨在降低新用户上手门槛。
    - **#5604: [Feature]: Add Mattermost private messages** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5604) - 企业IM集成的进一步细化。
    - **#5573: [Feature]: Send Emails via SMTP as a channel** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5573) - 结合Cron任务，打通邮件通知路径，是工作流自动化的关键一环。

- **核心能力与性能:**
    - **#5731: [Feature]: Add manifest as a provider** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5731) - 请求集成Manifest路由器，这与今日提交的PR [#6268] 方向一致，显示该功能已进入准实现阶段。
    - **#5843: [Feature]: Model wise Reasoning Configuration** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5843) - 要求将推理设置细化到每个模型，而非全局，是云成本管理和模型调优的明确需求。
    - **#5882: [Feature]: Ratatui-based agent mode REPL** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5882) - 目标是构建一个类似Claude Code的终端交互界面，将极大提升重度用户的使用体验。

- **安全与权限:**
    - **#5775: [Feature]: per-skill security permissions** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/5775) - 将脚本和命令权限细化到单个技能，是提升平台安全性的重要方向。
    - **#6729: [Feature]: Agent capability flags for shared/ access and workspace escape** [链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6729) - 在v0.8.0引入共享目录后，进一步控制Agent访问权限的需求浮现。

**路线图信号：** 大型功能PR `#6398: v0.8.0: Multi-Agent Runtime and Schema V3` [链接](https://github.com/zeroclaw-labs/zeroclaw/pull/6398) 正在寻求批准，表明团队正全力冲刺下一个大版本。同时，PR `#6649` 关于持久化ACP会话，以及 `#6667` 关于技能自动改进，均为路线图上重要的后端功能和智能化特性。

## 用户反馈摘要

从今日的Issues和PR中，可以提炼出以下真实用户痛点和使用场景：

- **痛点：“一切都取决于提供商”** - 许多Bug和功能请求都围绕特定AI提供商（如Kimi, Qwen, Ollama, Manifest）。用户抱怨提供商兼容性问题（#5600, #6734），希望简化多提供商管理（#5601），并自行集成路由器（#5731）。这反映出社区用户群体多样，对底层AI基础设施的灵活性要求极高。
- **使用场景：工作流自动化** - 用户正在将ZeroClaw嵌入到更复杂的自动化流程中。典型场景包括：通过Cron任务定时生成报告并发送到Email（#5573）、使用Webhook从GitHub等工具触发Agent工作流（#2467, #3542）、以及在Slack等协作工具中抑制不必要的消息通知（PR #6731）。
- **满意/不满意点：**
    - **满意点：** 从合并的PR和关闭的Issues看，用户对团队解决关键Bug（如#6123, #6399）和兑现功能承诺（如#3542, #6132）的响应速度是满意的。
    - **不满意点：** 对Native提供商硬编码超时（#6723）、Cron时区处理分歧（#6739）等“基础但重要”的配置细节不够精细感到失望。此外，技能自动优化功能上线但无生产环境限速（#6683）也引发了用户的关注。

## 待处理积压

- **#5600: [Bug]: Use kimi-code provider in streaming chat call tools... (创建于2026-04-10)**
    - **链接:** [Issue #5600](https://github.com/zeroclaw-labs/zeroclaw/issues/5600)
    - **状态:** 开放，标记为`r:needs-repro`和`status:blocked`
    - **备注:** 这是一个严重级别的Bug，严重阻塞了部分用户使用Kimi提供商的核心功能。尽管标记为需复现，但由于时间较长且讨论活跃，建议维护者投入更多资源进行根因分析和修复。
- **#2467: [Feature]: Webhook transforms (创建于2026-03-02)**
    - **链接:** [Issue #2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467)
    - **状态:** 开放，标记为`status:blocked`
    - **备注:** 这是一个功能请求，与#3542（已关闭）相比更为通用和底层。其长期处于`blocked`状态，可能是在等待特定的架构决策。Webhook作为连接外部世界的桥梁，其灵活性至关重要，建议将其优先级提升至P1，以满足用户的深度集成需求。
- **多个长期“blocked”的功能请求:** 包括 **#5775** (per-skill权限), **#5842** (extra_args验证), **#5843** (模型级推理配置), **#5907** (LSP支持) 在内的高风险、高价值功能请求均处于`status:blocked`和`needs-maintainer-review`状态。这暗示着维护团队可能在人力或技术路线上遇到瓶颈，需要社区和管理层共同关注，以制定明确的开发路线图。

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*