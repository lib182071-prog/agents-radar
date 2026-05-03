# OpenClaw 生态日报 2026-05-03

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-03 03:50 UTC

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

好的，这是根据您提供的OpenClaw项目数据生成的2026年5月3日项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-05-03

### 1. 今日速览

今日项目活跃度 **极高**。过去24小时内，社区提交了超过500条Issue和500个Pull Request，显示出巨大的社区参与度。然而，Issue和PR的增量中，待处理（开放/待合并）的比例极高（Issue开放率90.4%，PR待合率87.4%），这表明项目正面临大量待办事项积压，社区反馈响应与代码合并速度可能跟不上社区贡献的热情。新版本 v2026.5.2 的发布确认了项目在插件外部化架构上的进展，并修复了多个通道稳定性问题。整体来看，项目处于快速迭代期，但Bug和回归问题报告数量较多，稳定性和技术债务需要高度关注。

### 2. 版本发布

今日发布了三个版本：一个正式版和两个Beta版。

- **v2026.5.2**：一个主要功能发布。
  - **亮点**: 涵盖**npm-first 迁移**，即外部插件安装、更新、诊断、依赖报告和构件元数据等操作已切换为主要通过npm进行。@vincentkoc 为此版本做出重要贡献。
  - **亮点**: 优化了**Gateway 和 Agent 的热路径**，旨在提升核心链路的性能。
  - **亮点**: 新增了对**陈旧配置**、**缺失包数据**以及**Beta频道插件回退**的处理能力。

- **v2026.5.2-beta.3 & v2026.5.2-beta.2**：两个相同的Beta版。
  - **亮点**: 与正式版类似，聚焦于外部插件安装的诊断、初始化、修复、通道设置和记录，并**确保首批裸包安装仍通过npm进行**。

- **破坏性变更与迁移注意事项**：
  - **npm-first 迁移**: `openclaw plugins install`等命令的行为可能发生变化。如果您的环境无法访问npm或配置了私有注册源，插件安装可能会失败。请确保您的网络和npm配置正确。
  - **brave插件安装失败**（见Bug #76373）：在v5.2中，brave插件的稳定版（0.0.9）缺少 `openclaw.extensions` 配置，且beta频道不存在该插件。这可能是迁移过程中的一个疏漏。**建议**: 升级至 v2026.5.2 后，若遇到brave插件安装问题，需等待官方发布新修复版本或手动调整配置。

### 3. 项目进展

今日合并/关闭了63个PR，以下是一些重要的进展，表明项目正向更安全、更健壮的方向迈进：

- **命令行健壮性**: PR #73554 已被合并，修复了 `openclaw plugins enable/disable` 命令接受无效插件ID的问题，防止了无效配置写入。
- **消息可靠性**: PR #75893 解决了Telegram通道在markdown模式下，消息超过4096字符发送失败的问题。
- **系统安全**: PR #76423 修复了Agent可以通过 `exec` 工具执行 `openclaw message` 命令向用户发送非跟踪消息的漏洞，防止了潜在的会话污染和混淆。
- **开发者体验**: PR #76409 放宽了UI主题ID的校验，允许接受更短的ID（如“twitter”）。
- **依赖管理**: PR #75819 阻止了在Gateway进程树内部执行 `openclaw update` 命令，避免了更新过程中的冲突。

### 4. 社区热点

今日讨论最热烈的话题集中在**稳定性退化**和**用户体验**上。

- **[Issue #65302] “Your Updates Are Killing Your Product”** (评论: 9, 👍: 6) - 这是社区对产品频繁更新引入不稳定性的强烈批评。作者“邵小红”以AI Agent的身份，用充满情绪化的语言表达了对OpenClaw近几个版本持续破坏核心功能的不满。该Issue获得了极高的点赞，反映了社区对版本质量的普遍担忧。
  - **诉求**: 社区渴望一个稳定、可靠的版本，而非频繁的“破坏性更新”。维护者需重视回归测试，尤其是核心会话、消息投递和插件兼容性。
- **[Issue #72808] “Silently lost connection to Slack”** (评论: 11, 👍: 2) - 一个典型的可靠性问题，Slack连接在无任何错误提示下静默断开，直到用户实际演示时才被发现。这直接损害了用户对产品的信任。
  - **诉求**: 改善网络连接的监控和自动重连机制，并在连接丢失时向用户提供清晰的警告。
- **[Issue #73232] “Gateway runtime degradation”** (评论: 15, 👍: 1) - 用户报告了一个在Windows 11 + Node 24环境下，跨多个版本存在的性能退化问题，表现为多个子系统（定价获取、Telegram轮询、RPC）同时出现超时。
  - **诉求**: 社区希望维护者关注Windows平台和特定Node版本下的长期运行稳定性，并提供可操作的排查方向。

### 5. Bug 与稳定性

今日Bug报告密集，需重点关注以下问题：

- **严重 - 关键功能失效**：
  - **[Issue #76174]** (5星): 所有 `openai/*` 模型嵌入运行超时，但直接curl调通。**风险极高**，可能导致所有用户的核心对话功能瘫痪。该Issue已被关闭，推测有紧急修复PR。
  - **[Issue #76371]** (4星): `@openclaw/discord` 插件在v5.2版中，当Token配置为SecretRef时启动崩溃。这是影响最新版本的回归问题。
  - **[Issue #74907]** (6星): 长时间运行的会话在压缩后，多工具调用重播产生“孤立tool_use块”，导致Anthropic API 400错误。这是一个影响核心会话管理的回归问题。
- **中度 - 功能异常/性能退化**：
  - **[Issue #75824]** (5星): Web UI聊天后对话气泡消失，但直接API调用正常。影响前端用户核心体验。
  - **[Issue #74886]** (5星): 2026.4.27版本引入回归，WhatsApp会话不稳定，泄漏思维链，并回退到性能较差的模型。
  - **[Issue #73323]** (15条评论): 多版本长期存在的网关性能退化，影响多平台用户。
- **轻度 - 体验与配置问题**：
  - **[Issue #73814]** (5星): `curl | bash` 安装脚本因stdin消耗而挂起，影响新用户入门。
  - **[Issue #76373]** (5星): 5.2版brave插件安装失败，影响搜索引擎集成。

**已有关联修复PR的Bug**: 未见今日提交的直接修复PR，但Issue #76174已被关闭，推测已有修复方案落地。

### 6. 功能请求与路线图信号

- **对高性能/定制化的需求**：
  - **[Issue #63990]** “Multi-index embedding memory”：用户提出多索引嵌入记忆功能，支持不同模型间的弹性故障切换，而不会导致向量空间冲突。这与PR #73674（修复QMD Windows兼容性）和PR #69608（对齐日常记忆处理）等方向相关，表明社区对记忆系统的鲁棒性和性能有更高要求。
- **对PII保护和配置管理的需求**：
  - **[Issue #74271]** (4星, 👍:1): 用户建议 `doctor/status` 命令应警告 `~/.openclaw/.env` 中的环境变量覆盖了配置文件中的 `gateway.auth.token`。这反映了对配置优先级透明化的需求。
- **成本优化**：
  - **[Issue #72629]** (4星): 用户提出对话式多Agent协调中的Token成本呈二次方增长问题，并寻求设计输入。这表明社区开始关注大规模、商业化部署下的成本模型。
- **用户体验提升**：
  - **[PR #75004]** : 添加了Shell命令解释器功能，能够分析Agent可能执行的命令的风险等级。这标志着项目在安全Agent行为方面的重要进展，可能成为未来版本的一个亮点。

### 7. 用户反馈摘要

- **性能退化是核心痛点**: 大量用户反馈（如 #73232, #74886, #76174）集中在升级后性能（如超时、延迟）出现严重倒退，导致实际使用中断。
- **“不破不修”的更新模式令人沮丧**: 用户“邵小红”在 #65302中的长篇反馈代表了相当一部分用户的情绪。他们认为项目过度追求新功能而忽视了核心稳定性和向后兼容性，每一次更新都可能引入新的破坏性问题。
- **连接稳定性是信任基石**: 多个报告（#72808, #75346）表明，与Slack、Discord等平台的连接在不稳定的情况下会静默失效。用户将此视为“重大Bug”，因为它直接摧毁了“助手”随时随地可用的承诺。
- **配置复杂性成为壁垒**: 用户对配置导致的Bug反馈较多，如SecretRef解析失败（#76371）、Token替换崩溃（#67366）、环境变量与配置文件冲突（#74271）等。这表明配置系统的体验有待优化。

### 8. 待处理积压

以下为长期未关闭但讨论活跃的重要Issue，需维护者关注：

- **[Issue #43284] Feature Request: Add MathJax/LaTeX Support to Control UI** (创建于2026-03-11，6条评论，👍:4): 一个呼声较高的功能请求，核心用户希望支持数学公式渲染，但两个月来无实质性进展。
- **[Issue #38501] TUI Ctrl+C 取消与继续运行混淆** (创建于2026-03-07，5条评论): 长期存在影响终端用户体验的UX问题，但优先级似乎不高。
- **[Issue #43480] macOS app pinwheels due to SwiftUI infinite render loop** (创建于2026-03-11，4条评论): 影响macOS原生应用的性能Bug，可能因团队资源或优先级原因被搁置。
- **[PR #57276] 支持系统级别的systemd gateway服务** (创建于2026-03-29，未合并): 一个对Linux用户友好的PR，旨在让Gateway能通过systemd系统服务管理，但已经等待了一个多月。

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的各项目2026-05-03动态数据生成的横向对比分析报告。

---

### 个人AI助手/自主智能体开源生态横向分析报告（2026-05-03）

#### 1. 生态全景

当前，个人AI助手与自主智能体开源生态呈现出**高热度、快迭代、强分化**的态势。社区贡献热情空前高涨，尤其在以OpenClaw、ZeroClaw为核心的项目中，每日Issue与PR数量动辄数百，表明开发者群体正积极涌入。生态焦点已从单一的模型对话能力，转向**多平台信道集成、长期记忆与状态管理、多智能体协作架构、以及Agent自主性与安全性**的深度融合。然而，生态的快速膨胀也带来了显著的**稳定性挑战**，多个项目（如OpenClaw、ZeroClaw）均出现因版本更新频繁而导致核心功能退化的用户抱怨，如何在创新速度与产品质量间取得平衡，是所有项目面临的共同课题。

#### 2. 各项目活跃度对比

| 项目名称 | 今日Issues (新增/活跃) | 今日PRs (新增/活跃) | 新版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500+ (开放率90.4%) | 500+ (待合率87.4%) | v2026.5.2 | **警告**：社区极度活跃，但维护者响应与合并能力严重滞后，技术债务高，面临稳定性失控风险。 |
| **NanoBot** | 3 (新增) | 19 (8合并) | 无 | **良好**：活跃度适中，合并率高，Bug修复和功能迭代节奏稳健，项目健康度较好。 |
| **Hermes Agent** | 100+ (更新) | - | 无 | **良好**：讨论热度极高，尤其在A2A协议等前瞻性功能上，社区参与深度好，代码合并虽不多但聚焦关键问题。 |
| **PicoClaw** | 7 | 8 | Nightly v0.2.8 | **健康**：活动量适中，Bug修复与功能开发并行，社区反馈得到及时响应（如PR #2746）。 |
| **NanoClaw** | 13 | 18 (7合并) | 无 | **健康**：修复效率高，社区贡献（如abbyshekit）积极，项目在稳定性和功能扩展上双向发力。 |
| **NullClaw** | - | 15 (合并) | 无 | **健康**：核心维护者交付能力强，集中在安全加固和核心稳定性修复，项目演进方向明确。 |
| **IronClaw** | 20 | 43 (6合并) | 无 | **良好**：活跃度极高，受Reborn架构重构驱动，同时外部贡献者大量涌现，协作生态初步形成。 |
| **LobsterAI** | 0 | 4 (待合并) | 无 | **稳定**：活跃度偏低，但多个关键修复PR处于待合并状态，一旦合入能显著提升用户体验。 |
| **Moltis** | 4 | 3 | 无 | **稳定**：活跃度中等，国际化取得进展，但在核心模型兼容性上存在待解决的严重Bug。 |
| **CoPaw** | 13 | 14 (4合并) | 无 | **健康**：功能迭代速度与Bug发现速度均较快，模型回退等社区呼声较高的功能仍未采纳，但存在路线图信号。 |
| **ZeroClaw** | 50 | 33 (6合并) | 无 | **警告**：活跃度极高，但合并率偏低，大量P1/P2级别Bug报告凸显稳定性测试不足，项目处于v8大重构前的动荡期。 |
| **TinyClaw** | 0 | 0 | - | **静默**：无任何活动，项目可能已暂停或进入维护模式。 |
| **ZeptoClaw** | 0 | 0 | - | **静默**：无任何活动。 |

#### 3. OpenClaw 在生态中的定位

OpenClaw 是当前生态中**毫无争议的核心参照项目**。其优势在于：

- **社区规模与影响力**：每日500+的Issue和PR数量远超其他项目，是生态中开发者参与度最高的项目。
- **功能广度**：作为“核心参照”，其功能覆盖了Agent的通用框架、多通道集成（Slack, Discord, Telegram等）、插件系统、网关管理等，定义了该领域的基本技术栈。

然而，OpenClaw 的技术路线与同类项目存在显著差异：

- **“功能聚合，以量取胜” vs “精雕细琢，追求稳定”**：OpenClaw 倾向于快速集成大量新功能和插件，生态极其丰富。但这导致了严重的技术债务和稳定性问题，用户反馈“每次更新都可能引入新Bug”。相比之下，**NullClaw、NanoBot** 等项目更专注于核心稳定性和安全性，通过更严格的代码审查和测试流程，牺牲部分功能迭代速度以换取用户体验的可靠性。
- **插件系统：npm-first vs 原生集成**：OpenClaw 正在进行“npm-first”迁移，将插件生态完全外部化，依赖npm。而像 **PicoClaw、CoPaw** 等项目则更倾向于将流行的Provider和工具作为内置功能提供，以减少用户的配置依赖和兼容性风险。

**社区规模与成熟度**：OpenClaw 的社区规模是生态中最大的，但“大”不等同于“成熟”。其高Issue开放率和大量回归Bug表明社区处于“野蛮生长”的早期阶段。相较之下，**IronClaw、NullClaw** 等项目虽然Issues和PR绝对数量不及OpenClaw，但核心维护者与贡献者之间的协作更为紧密，PR的讨论和审查质量更高，显示出更成熟的社区治理模式。

#### 4. 共同关注的技术方向

多个项目不约而同地涌现出以下需求，构成了生态的“共同语言”：

- **记忆系统的增强与鲁棒性**：**OpenClaw** (Multi-index embedding memory)、**Hermes Agent** (Richer local memory)、**ZeroClaw** (Dream Mode: 记忆巩固)、**CoPaw** (MemoryHook) 均表现出对更智能、更持久、更抗干扰的记忆方案的需求。社区不满足于简单的历史消息存储，而是要求语义搜索、结构化事实提取和自主学习能力。
- **渠道连接的稳定性与可靠性**：**OpenClaw** (Slack静默断连)、**NanoClaw** (WhatsApp LID映射丢失)、**Hermes Agent** (Telegram轮询冲突)、**CoPaw** (微信不同步) 共同指向了一个痛点：与外部平台（Slack、Telegram、WhatsApp等）的连接状态不稳定，缺乏有效的监控和自动恢复机制。
- **多模型兼容性与故障转移**：**OpenClaw** (模型嵌入超时)、**ZeroClaw** (DeepSeek/Bedrock 400错误)、**Hermes Agent** (DeepSeek/OpenRouter崩溃)、**Moltis** (DeepSeek推理内容错误)、**CoPaw** (Model fallback chain请求) 均反映出对**多模型提供商的兼容性**和**服务降级/故障转移**的强烈需求。社区希望Agent能灵活切换模型以保障服务可用性，而不是绑定在某一个特定模型上。
- **配置管理的易用性与透明性**：**OpenClaw** (环境变量覆盖)、**NanoBot** (支持`{env:VAR}`)、**Hermes Agent** (配置丢失)、**ZeroClaw** (Token配置问题) 共同表明，用户希望配置系统更灵活（支持环境变量）、更透明（明确优先级）、且更稳定（升级后不丢失）。
- **Agent的自主性与自我认知**：**ZeroClaw** (Agent不知自己有cron功能)、**Hermes Agent** (Curator背景技能维护)、**NullClaw** (反欺骗边界) 体现了生态对Agent“智障”行为的不满，以及对Agent理解自身能力、主动维护技能、并能抵御提示注入等安全威胁的更高期待。

#### 5. 差异化定位分析

| 维度 | 功能侧重 | 目标用户 | 技术架构 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | “全能战士”：插件生态最丰富，通道覆盖最广 | 高级开发者、希望探索最多可能性的“极客” | 模块化、插件化（npm-first），配置复杂 |
| **NullClaw / NanoBot**| “稳定守护者”：聚焦核心交互稳定与安全 | 对服务可靠性要求高的个人/小团队 | 简洁、安全优先，代码库更紧凑，易于维护 |
| **Hermes Agent** | “前瞻探索者”：聚焦Agent间通信(A2A)与自主进化 | 对Agent未来形态感兴趣的研究者/开发者 | 面向未来的架构设计，重视Agent自主性和互操作性 |
| **IronClaw** | “重架构重构者”：正在大规模重构核心Reborn架构 | 对Agent底层架构有深刻理解的核心贡献者 | 强调事件驱动、持久化、多执行模型，架构较重 |
| **PicoClaw / NanoClaw**| “平台集成者”：深度集成特定平台（微信、飞书、Signal） | 希望Agent融入特定工作流的企业/团队 | 注重平台渠道的深度适配和独特功能（如飞书线程隔离） |
| **CoPaw / ZeroClaw** | “中国开源双雄”：响应国内模型/平台生态，迭代迅速 | 国内开发者、企业级POC需求方 | Provider丰富，国际化与本地化并行，社区驱动特征明显 |
| **Moltis** | “多模态探索者”：已开始集成图像生成能力（gpt-image-2） | 对多模态交互有早期需求的用户 | 在文本处理基础上，积极拓展多模态能力边界 |

#### 6. 社区热度与成熟度

- **高速迭代期（伴有稳定性风险）**：
    - **OpenClaw**、**ZeroClaw**、**CoPaw**：这些项目具有最高的社区活跃度（每日数十至数百Issue/PR），功能迭代极快。但同时也伴随着最显著的稳定性问题、高频的Bug报告和较大的技术债务。社区“野蛮生长”特征明显。
    - **IronClaw**：同样非常活跃，但受架构重构驱动，社区讨论更聚焦于设计层面。外部贡献者大量提交PR，表明项目吸引力强，但核心架构仍在变动中。

- **质量巩固期**：
    - **NanoBot**、**NullClaw**、**NanoClaw**、**PicoClaw**：这些项目活跃度中等偏高，但合并率高，Bug修复和功能增强的节奏稳健。社区反馈响应及时，项目健康度良好。它们代表了“在稳定中求发展”的另一条路径。

- **功能探索期**：
    - **Hermes Agent**、**Moltis**：活跃度中等，但社区讨论的议题具有很高前瞻性（如A2A协议、图像生成）。这些项目是行业趋势的“风向标”，但核心功能的成熟度和用户规模可能相对较小。

- **稳定/维护期**：
    - **LobsterAI**：活跃度偏低，主要在处理一些积累的PR。项目可能进入了稳定维护阶段，或正待下一个功能爆发点。**TinyClaw** 和 **ZeptoClaw** 则处于静默状态。

#### 7. 值得关注的趋势信号

1.  **从“工具调用”到“能力发现”**：ZeroClaw的Bug报告（Agent不知自己能cron）是一个典型信号。未来智能体的核心竞争力不再是“能调用多少工具”，而是“能否理解自身能力边界并在恰当场景主动、智能地使用它们”。这指向了**自我认知模型**和**意图驱动的调度引擎**将成为下一个技术高地。

2.  **A2A协议是下一波浪潮的“入场券”**：Hermes Agent对A2A协议的热烈讨论（明确被视为MCP的“完美补充”）和IronClaw的Curator功能，表明构建**多智能体协作网络**的共识正在形成。下一个阶段的竞争焦点，将是智能体之间如何像人类一样“找人帮忙”、“协商任务”和“交换信息”。

3.  **安全与信任成为社区核心焦虑**：OpenClaw的“会话污染漏洞”、NullClaw的“反欺骗边界加固”、Hermes Agent的“品牌信息过度暴露”，以及大量关于提示注入的担忧，都反映出：**在Agent拥抱更多自主性的同时，其安全边界、行为可信度以及对用户数据的保护，正在从“可选功能”演变为“核心生存技能”**。信任，将成为区分优秀Agent与平庸Agent的关键。

4.  **“降本增效”的部署与运行需求兴起**：IronClaw对ARM64的支持、ZeroClaw对WASM插件的支持、多个项目对更低Token消耗的需求，以及用户对在“弱、便宜、低资源设备”上运行Agent的渴望（如NullClaw的Issue #871），共同预示着一个趋势：**智能体的部署将从“数据中心”下沉到“边缘设备”**。轻量化、低开销的Agent方案，将能触达更广阔的用户群体。

5.  **用户体验从“可配置”转向“可依赖”**：OpenClaw用户“Your Updates Are Killing Your Product”的愤怒呐喊，是生态从“极客工具”走向“大众产品”过程中必须跨越的鸿沟。这警示所有项目：**早期用户可能容忍繁琐的配置和不稳定的体验，但AI Agent若想成为“个人助手”而非“开发玩具”，就必须把“稳定性”和“可靠性”提升到与“功能丰富度”同等的战略高度。**

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026‑05‑03

---

## 今日速览

- 过去24小时活跃度中等偏高：新增3个Issue（均为活跃状态），19个Pull Request中有8个被合并或关闭，项目在安全、功能扩展和稳定性方面持续迭代。
- 合并的PR覆盖了WhatsApp媒体支持、环境变量引用、DeepSeek thinking模式修复、WebUI远程部署等多个关键功能，项目功能完整度显著提升。
- 新出的Bug集中在“安全卫士误报”和“工作目录访问异常”两个方向，均已获得初步定位，社区响应较快。
- 无新版本发布，但一批重要PR已合并，下一个版本可能会包含WhatsApp集成、安全策略优化和飞书线程隔离等特性。

---

## 版本发布

无

---

## 项目进展

今日共有 **8 个 Pull Request 被合并/关闭**，其中多数为功能增强和关键修复，推动项目向更稳定、更功能完备的方向迈进。

| PR | 标题 | 说明 |
|----|------|------|
| [#3594](https://github.com/HKUDS/nanobot/pull/3594) | fix: allow_patterns take priority over deny_patterns in ExecTool | **紧急安全修复** – 将 `allow_patterns` 的优先级提升到 `deny_patterns` 之上，使白名单真正可覆盖内置黑名单。 |
| [#3456](https://github.com/HKUDS/nanobot/pull/3456) | feat(skills): add create-instance built-in skill + webui remote backend | **新功能** – 允许运行中的 Agent 通过内置 skill 创建新 Bot 实例，并支持 WebUI 远程部署（GitHub Pages + 密钥认证）。 |
| [#2010](https://github.com/HKUDS/nanobot/pull/2010) | feat(whatsapp): add media send/receive support | **新渠道** – 完整实现 WhatsApp 媒体收发（图片、语音、视频、文档），统一 `sendMessage()` API。 |
| [#2218](https://github.com/HKUDS/nanobot/pull/2218) | feat(security): support `{env:VAR}` syntax for environment variable references | **安全增强** – 允许在 `config.json` 中使用 `{env:VAR}` 引用环境变量，敏感信息不再明文配置。 |
| [#3419](https://github.com/HKUDS/nanobot/pull/3419) | fix(provider): preserve reasoning_content when merging consecutive assistant messages | **修复** – 解决 DeepSeek 思考模式因合并消息时丢弃 `reasoning_content` 导致的 400 错误。 |
| [#3414](https://github.com/HKUDS/nanobot/pull/3414) | fix(agent): cap recent history section in system prompt | **性能优化** – 限制系统提示中“最近历史”部分为 32K 字符，防止长期运行后 prompt 膨胀。 |
| [#3176](https://github.com/HKUDS/nanobot/pull/3176) | feat(feishu): thread-scoped sessions, reply_in_thread, non-blocking reaction | **渠道增强** – 飞书机器人支持线程级会话隔离、主题内回复、非阻塞表情反应。 |
| [#3247](https://github.com/HKUDS/nanobot/pull/3247) | fix(memory): fall back to raw_archive on LLM error response | **修复** – 当 `/new` 后的 LLM 归档调用失败（如模型过载）时，回退到原始存档，避免会话数据丢失。 |

> 以上 PR 中 #3594、#3419、#3414、#3247 属于修复类，其余为功能增强。WhatsApp 和飞书的渠道完善使 NanoBot 在办公协作场景的覆盖更广。

---

## 社区热点

今日讨论最集中的是 **Bug 报告** 和 **功能请求**，但评论数均为0，社区主要通过 Issue 和 PR 描述表达诉求。

- **#3599 – [bug] 升级 v0.1.5.post3 后经常提示 Command blocked by safety guard**  
  用户报告在工作目录内执行命令被安全卫士误杀，且重试后功能正常。该问题反映出安全模式在路径判断上可能存在边界条件。  
  [Issue链接](https://github.com/HKUDS/nanobot/issues/3599)

- **#3597 – [bug] NanoBot confused and couldn't access workspace root**  
  用户测试日常写作任务（每日草稿文章）时，Agent 无法将文件保存到工作目录根路径，怀疑与上下文或路径解析有关。  
  [Issue链接](https://github.com/HKUDS/nanobot/issues/3597)

- **#3595 – [enhancement] 移除 exec 超时 600 秒硬编码上限**  
  用户希望允许更长超时以支持下载、长时间脚本等任务，并定位了三层硬编码位置。该需求已由 **#3596** 对应 PR 响应，**受到关注**。  
  [Issue链接](https://github.com/HKUDS/nanobot/issues/3595) | [PR链接](https://github.com/HKUDS/nanobot/pull/3596)

---

## Bug 与稳定性

### 已修复（今日合并）

| 严重程度 | 问题 | 修复PR |
|---------|------|--------|
| 🔴 高 | `allow_patterns` 无法覆盖 `deny_patterns`，导致白名单失效 | [#3594](https://github.com/HKUDS/nanobot/pull/3594) 已合并 |
| 🟡 中 | DeepSeek 思考模式因消息合并导致 400 错误 | [#3419](https://github.com/HKUDS/nanobot/pull/3419) 已合并 |
| 🟡 中 | `/new` 后 LLM 失败导致归档数据丢失 | [#3247](https://github.com/HKUDS/nanobot/pull/3247) 已合并 |
| 🟢 低 | 系统提示中“最近历史”无限膨胀 | [#3414](https://github.com/HKUDS/nanobot/pull/3414) 已合并 |

### 待修复（今日新增）

| 严重程度 | 问题 | 对应 Issue |
|---------|------|------------|
| 🟡 中 | 升级后安全卫士误报工作目录内命令 | [#3599](https://github.com/HKUDS/nanobot/issues/3599) |
| 🟡 中 | Agent 无法正确访问工作目录根路径 | [#3597](https://github.com/HKUDS/nanobot/issues/3597) |

### 活跃修复 PR（尚未合并）

| 严重程度 | 问题 | 修复PR |
|---------|------|--------|
| 🟡 中 | `reasoningEffort: null` 未按预期禁用推理（关联 #3585） | [#3587](https://github.com/HKUDS/nanobot/pull/3587) |
| 🟢 低 | 自托管 Whisper 后端（whisper.cpp）因音频格式不兼容失败 | [#3588](https://github.com/HKUDS/nanobot/pull/3588) |

---

## 功能请求与路线图信号

- **exec 超时灵活化**（#3595 → #3596）  
  用户要求移除 600 秒硬上限，PR #3596 提出了双层超时方案（**硬超时** + **活动超时**），更适应长时间任务，很可能进入下一版本。

- **Discord 交互组件**（#3589 open）  
  为 Discord 频道增加按钮、选择菜单和模态框支持，使 Agent 能提供更丰富的交互体验。

- **CLI 体验优化**（#3592、#3593 open）  
  - `Ctrl+C` 在输入非空时清空行而非直接退出（#3592）  
  - 子命令无参数时显示帮助而非报错（#3593）  
  这两个 PR 显著降低用户误操作风险，预计会快速合入。

- **Dream（自动合并）范围控制**（#3591 open）  
  允许用户禁用 Dream 或限制其作用域（仅内存/上下文更新），避免自动合并导致技能漂移。

- **Heartbeat 手动触发**（#3590 open）  
  提供按需心跳命令，方便用户调试 Phase 1 决策或立即执行心跳。

- **统一转录提供者 + 本地 Whisper**（#3513 open）  
  解决当前转录存在静默失败、提供者重复、无本地 Whisper 路径等问题，长期来看将提升语音场景可靠性。

---

## 用户反馈摘要

- **#3599 用户（jermeyhu）**：  
  升级后遇到安全卫士对工作目录内 `rm` 命令的误拦截，而重试后功能正常。用户认为“操作的是工作目录内的内容，应该是被允许的”。反映了后续版本中安全规则应更精确匹配实际路径，避免挫伤用户体验。

- **#3597 用户（fablau）**：  
  正在测试 NanoBot 能否稳定用于日常工作（每日撰写推文草稿），但 Agent 无法将文件保存到工作目录根路径。该场景表明路径上下文对 Agent 行为影响大，期望项目加强工作目录的显式管理。

- **#3595 用户（MARJORIESHA-pBAD）**：  
  明确要求移除 exec 的 600 秒硬编码上限，并详细列出了三个约束位置（schema 校验、运行时及配置）。显示出高级用户希望自由调整超时以适应不同任务（下载、长时间脚本），社区对 Agent 控制力的需求增强。

---

## 待处理积压

以下为 **开放超过 3 天** 且仍未合并的 Pull Request，建议维护者关注：

| PR | 标题 | 创建日期 | 备注 |
|----|------|----------|------|
| [#3513](https://github.com/HKUDS/nanobot/pull/3513) | feat(audio): unify transcription providers and add local Whisper support | 2026-04-28 | 统一转录架构，涉及面较大，目前仍为 WIP？实际状态为 open 且无 draft 标记。建议 reviewer 评估其与 [#3588](https://github.com/HKUDS/nanobot/pull/3588) 的关系。 |
| [#3583](https://github.com/HKUDS/nanobot/pull/3583) | [WIP] Improve beta WebUI turn completion and chat isolation | 2026-05-01 | 明确标记为 WIP，但已有一定完成度，加上前端问题对 Beta 用户影响较大，可考虑优先推进。 |
| [#3589](https://github.com/HKUDS/nanobot/pull/3589) | feat(discord): interactive components | 2026-05-02 | 新功能，但需注意与现有 `message` 工具的兼容性，已有部分讨论（虽评论显示 undefined，但内容较丰富）。 |

另，**Issue #3599 和 #3597** 目前无任何 assignee 或 label，建议维护者尽快确认并分配负责人，以免用户失望。

---

*本日报由 NanoBot 项目数据自动分析生成，数据截止 2026-05-03。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，以下是为您生成的 Hermes Agent 项目动态日报，日期为 2026-05-03。

---

# Hermes Agent 项目动态日报 | 2026-05-03

## 1. 今日速览

今日项目活跃度**极高**，过去24小时内产生了100条Issue与PR更新。社区讨论热点主要集中在**A2A（Agent-to-Agent）协议支持**这一重大功能请求上，同时有多个针对网关延迟、配置持久化和特定Provider兼容性的Bug报告。尽管新合并的代码数量不多，但项目在问题发现和功能讨论上异常活跃，表明社区参与度与项目本身的功能迭代需求都在快速增长。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日项目在代码合并和问题关闭上取得了具体进展，主要聚焦于**平台适配性修复**、**核心功能完善**和**安全性提升**。

- **PR #2531 [已合并] 修复 `/stop` 命令绕过重放路径的问题**：该PR修复了 `/stop` 命令在停止代理后，其输入文本被错误地当作新用户提示重放的严重Bug。此修复显著改善了用户体验，确保了停止操作的即时性和预期性。
- **PR #2524 [已关闭] 修复 Telegram 轮询与流式编辑冲突**：解决了启用流式输出时，Telegram适配器因共享连接池导致 `httpx.ReadError` 而崩溃的问题。通过隔离轮询与流式编辑的连接，提升了Telegram平台的稳定性。
- **PR #2536 [已关闭] 修复 Discord 持续打字状态问题**：修复了Discord机器人在响应完成后，`正在输入...`指示器不会自动关闭的Bug，改善了用户体验。
- **PR #2522 [已关闭] 修复自定义 Provider 上下文长度自动检测**：解决了用户在通过 `/model` 命令保存自定义Provider时，若不指定上下文长度，系统会静默失败的问题。现在系统会尝试自动检测并反馈给用户。
- **Issue #16077 [已关闭]  Curator 背景技能维护功能评审**：这是一个重要的RFC（请求评审），讨论并关闭了关于“Curator”（一个自动维护代理自创技能的背景任务）功能的实现。这标志着项目在**自我演进代理**能力上迈出了重要一步。

## 4. 社区热点

今日社区讨论的核心是**智能体间通信与互操作性**。

- **Issue #514 [A2A协议支持]**：这是今日评论数最多（11条）的Issue，提出了支持Google的A2A（Agent-to-Agent）协议的功能请求。社区对此表现出极大热情，认为这是MCP协议（解决“我能用什么工具？”）的完美补充，用于解决“谁能帮我？”的问题。此需求反映了社区对构建多智能体协作网络和开放式生态的强烈渴望。
- **Issue #16077 [Curator功能RFC]**：拥有5条评论，讨论热度紧随其后。社区对“代理自我维护技能”这一概念非常感兴趣，讨论涉及了该功能的实现细节、潜在影响以及对代理自主性提升的价值。

## 5. Bug 与稳定性

今日报告了多个Bug，涉及不同优先级和组件。部分关键问题已有修复PR。

**严重 / 高优先级**

- **#16677 [P1] DeepSeek V4 Pro 通过 OpenRouter 导致网关崩溃循环**：这是一个影响Telegram机器人可用性的严重Bug。用户反馈使用特定模型会导致网关持续重启，完全无法使用。**已有PR #16701 提出修复方案**。
- **#19045 [P2] 网关非流式模式存在 ~5秒固定延迟**：这是一个性能回归问题，影响所有非流式响应场景。根因是 `wait_for` 操作在没有消费者注册时依然等待。**该Issue已被关闭，表明修复可能已合并或确认**。
- **#17199 [P2] DeepSeek Provider 的自定义端点配置被破坏**：当用户尝试通过“deepseek” provider配置兼容OpenAI的自定义端点（如火山引擎ARK）时，由于模型名称的过度规范化和 `base_url` 被覆盖导致功能失效。

**中等优先级**

- **#19043 [P2] `pyproject.toml` 中的 `exclude-newer` 设置阻止依赖解析**：该问题阻碍了包含“setuptools”在内的稳定包的安装，影响了项目搭建和新手体验。
- **#19036 [P2] Kanban 数据库与 Profile 绑定，破坏多代理工作流**：由于不同Profile拥有独立的Kanban数据库，导致Orchestrator无法访问Worker的Kanban数据，破坏了多代理协作流程。
- **#19003 [P2] 上下文压缩器忽略推理字段**：在使用思考类模型（如DeepSeek R1）时，上下文压缩器因只读取 `content` 字段而忽略了 `reasoning` 字段，导致摘要为空，影响长对话管理。

**低优先级 / 其他**

- **#19046 [Bug] Anthropic API 检测到过度品牌标识**：用户抱怨向Anthropic API发送的请求中包含了大量关于“第三方封装”的品牌信息，可能导致API使用受限或警告。
- **#19039 [P3] CLI TUI 在浅色背景下难以阅读**：默认主题在白天使用时对比度不足，影响用户体验。

## 6. 功能请求与路线图信号

社区提出的新功能需求显示出对代理**自主性、互操作性**和**数据持久化**的更高要求。

- **#514 A2A协议支持**：如前所述，这是目前最强烈的信号，可能会成为接下来几个版本的重点方向。它与项目定位“The Agent That Grows With You”高度契合。
- **#2704 定时任务结果写回对话记忆**：用户期望定时任务的结果能被记录在对话记忆中，以便用户随时查询调度任务的执行情况。这体现了对**持久化、可追溯背景**的需求，已有4条评论和2个赞，关注度较高。
- **#2653 `delegate_task` ACP 传输覆写**：允许非ACP的父代理生成ACP子代理，这对于构建灵活的多代理拓扑结构至关重要。已有1个赞，表明这是一个细分但专业的需求。
- **#2667 当前会话上下文缓冲区**：提议创建一个可搜索的压缩消息归档，以避免长会话中历史信息丢失。这与记忆管理（如#2184）的长期目标一致。
- **#2184 更丰富的本地记忆**：用户不满足于基于平面文件的简单记忆，要求语义搜索和结构化事实提取，这代表了从“存储”向“智能检索”的演进方向。
- **#2919 集成 x402 / Agent-to-Payment（MCP）**：提议集成支付功能，允许代理在需要时为用户执行支付操作。这触及了代理链上经济活动的核心，是一个极具前瞻性的需求。
- **#16796 支持星期几的会话重置计划**：用户需要在“每日重置”和“闲置重置”之外，增加“每周特定时间重置”的灵活性。

## 7. 用户反馈摘要

从今日的Issues中，我们可以提炼出真实的用户痛点：

- **配置丢失**：用户 `manuelschipper` 在 #2293 中反馈，每次执行 `hermes update` 后，自定义的配置（如 `docker_volumes`）会丢失，需要反复手动添加，体验不佳。
- **集成失败**：用户 `yalding8` 在 #17199 中详细描述了配置火山引擎ARK自定义端点的困难，显示在处理特定第三方API兼容性时，项目存在过度规范化和参数覆盖的问题。
- **平台兼容性**：用户 `shiping430` 在 #19035 中报告，发送到飞书的代码块无法展开，这是一个平台特定渲染问题。用户 `liweiwp` 在 #19039 中则指出默认颜色方案在浅色背景下难以阅读。
- **期望更智能的记忆**：用户 `benfrank241` 在 #2184 中明确表示，当前的平面文件记忆“没有检索智能”，希望获得语义搜索和事实提炼能力，这是对代理“学习能力”更高的期望。
- **对过度品牌化的反感**：用户 `Many0therFunctions` 在 #19046 中批评项目向Anthropic API发送过多的品牌信息，语气中透露着不满和困惑，认为此举可能影响API的正常使用。

## 8. 待处理积压

以下是一些长期未解决或需要维护者关注的重要议题：

- **#2184 功能请求：Richer local memory（更丰富的本地记忆）**：自2026-03-20创建，已有一个多月，至今有1条评论，但尚未被分配或标记为路线图优先级。
- **#2293 Bug：自定义配置文件在更新后丢失**：自2026-03-21报告，历时一个半月仍未解决，对用户的持续使用造成困扰。
- **#2604 Bug：ResponseStore 在驱逐/删除后留下陈旧对话映射**：自2026-03-23报告，这是一个数据一致性问题，随着项目运行时间增长可能会造成更大的数据污染。
- **#2743 [安全] Bug：`shell=True` 在 subprocess 调用中存在命令注入风险**：自2026-03-24报告，这是一个明确的安全风险，虽未报告具体攻击案例，但应尽快修复。
- **#16077 RFC: Curator 背景技能维护**：该RFC**已于今日关闭**，但其所讨论的“Curator”功能的实际代码实现尚未进入主分支，需要持续跟踪。
- **#17199 Bug: DeepSeek Provider 破坏自定义端点**：这是一个影响特定用户群的P2级别Bug，虽然已经有PR #16701修复了其相关的网关崩溃问题，但该配置本身的Bug仍需专门的修复。
- **#19036 Bug: Kanban 数据库与 Profile 绑定，破坏多代理工作流**：这是一个直接影响多代理功能可用性的P2 Bug，需要维护者评估并分配修复任务。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，这是基于您提供的PicoClaw项目数据生成的2026-05-03项目动态日报。

---

# PicoClaw 项目动态日报 | 2026-05-03

## 1. 今日速览

今日PicoClaw项目活跃度较高，共处理7条Issue和8条PR，社区贡献者积极参与。项目发布了最新的Nightly构建版本，持续集成前沿功能。当日最显著的特点是Bug修复活跃，特别是针对路径处理、流式输出和模型兼容性等核心问题有了明确的PR跟进，同时新功能请求（如OAuth 2.1支持、邮件通道）保持热度，反映出项目在稳定性和功能扩展上的双重进展。整体来看，项目维护者与社区响应及时，项目健康度良好。

## 2. 版本发布

- **Nightly Build (v0.2.8-nightly.20260503.a94ba821)**
  - **内容**: 本次为自动构建的Nightly版本，可能包含未稳定测试的最新代码。
  - **变更日志**: [v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)
  - **注意**: 此版本为不稳定版本，仅供尝鲜和测试，不建议用于生产环境。

## 3. 项目进展

今日有2个PR被合并/关闭，主要聚焦于文档完善和社区维护：

- **[已关闭] #2747: 更新微信群二维码**：由贡献者BeaconCat提交，更新了社区微信群二维码，有效期至5月9日。此操作表明项目在持续维护其社区沟通渠道。
- **[已关闭] #2746: 修复OpenRouter推理抑制预设文档**：由贡献者DonaldKundert提交，针对OpenRouter推理模型（如`nvidia/nemotron-3-super-120b-a12b:free`）在输出中泄露推理过程的问题，新增了抑制推理输出的示例preset和文档说明。此PR与今日报告的Bug #2745直接相关，快速响应并提供了解决方案。

此外，仍有6个PR处于待合并状态，涵盖了从Bug修复（如DeepSeek流式推理、路径安全问题）到新功能（如xAI提供者支持）等重要改进，这些PR的合并将是项目下一步迈进的关键。

## 4. 社区热点

- **[Feature] #2421: 添加邮件为原生通道 (4条评论)**
  - **链接**: [#2421](https://github.com/sipeed/picoclaw/issues/2421)
  - **分析**: 此Issue自4月8日创建以来，持续收获关注。用户提出将电子邮件作为PicoClaw的原生通道，主要面向企业、科研机构等以邮件为主要沟通渠道的用户群体。这是一项具有明确应用场景和用户基础的需求，反映了社区对扩展PicoClaw连接能力的强烈愿望。

- **[Feature] #2546: 支持从仪表盘添加OAuth 2.1 + PKCE保护的MCP服务器 (3条评论)**
  - **链接**: [#2546](https://github.com/sipeed/picoclaw/issues/2546)
  - **分析**: 用户建议为非技术用户提供一个更简便的途径来集成受OAuth保护的MCP（模型上下文协议）服务器，思路类似于Claude.ai的“添加连接器”。这项功能对于降低MCP服务器的使用门槛、扩大PicoClaw的生态系统至关重要，是社区对增强连接性和易用性的明确信号。

## 5. Bug 与稳定性

今日报告了3个新Bug，并有一个关联PR已提交修复。按严重程度排列如下：

- **[Bug #2720] 单例PID检查不验证进程身份，导致崩溃循环 (高优先级)**
  - **链接**: [#2720](https://github.com/sipeed/picoclaw/issues/2720)
  - **问题**: Gateway启动失败，因为PID文件中的PID被其他无关进程（如`systemd-resolved`）重用。单例检查仅验证PID存在，未验证其是否为真正的PicoClaw实例，导致启动崩溃循环。
  - **关联PR**: 目前暂无直接关联的修复PR。
  - **分析**: 此Bug导致服务不可用，影响极大，需要维护者优先处理。

- **[Bug #2668] Gemini API对复杂JSON Schema返回HTTP 400错误 (1个👍)**
  - **链接**: [#2668](https://github.com/sipeed/picoclaw/issues/2668)
  - **问题**: 当MCP工具（如Notion集成）包含`$ref`, `anyOf`等复杂JSON Schema时，Gemini模型的函数调用验证失败，导致PicoClaw崩溃。
  - **分析**: 该问题影响了一部分使用Gemini模型并依赖复杂MCP工具的用户，属于兼容性问题。获得了一个👍，表明有一定的用户关注度。

- **[Bug #2749] Bash将相对路径评估为绝对路径**
  - **链接**: [#2749](https://github.com/sipeed/picoclaw/issues/2749)
  - **问题**: Bash通道在处理相对路径时，会将其错误地解析为根目录绝对路径，导致路径安全检查失败。
  - **关联PR**: [#2750](https://github.com/sipeed/picoclaw/pull/2750) 已提交修复PR。该PR修正了路径扫描器的正则表达式，避免误将相对路径解析为根路径。

- **[Bug #2665] Android端Anthropic模型下拉菜单使用错误的模型ID**
  - **链接**: [#2665](https://github.com/sipeed/picoclaw/issues/2665)
  - **问题**: Anthropic提供者的模型选择下拉菜单中，模型ID使用了点号（如`claude-sonnet-4.6`），但Anthropic API要求使用连字符（`claude-sonnet-4-6`），导致API调用失败。

- **[Bug #2745] OpenRouter推理模型泄露推理内容到助手消息中**
  - **链接**: [#2745](https://github.com/sipeed/picoclaw/issues/2745)
  - **问题**: 使用OpenRouter的推理模型时，本应仅显示最终答案，但输出中包含了模型的“推理前导语”，导致信息泄露。
  - **关联PR**: [#2746](https://github.com/sipeed/picoclaw/pull/2746) 已提供修复文档和示例preset。

## 6. 功能请求与路线图信号

- **新功能请求**:
    - [#2421 **邮件原生通道**](https://github.com/sipeed/picoclaw/issues/2421): 需求明确，目标用户群体清晰，是扩展PicoClaw作为统一通信中枢的重要一步。
    - [#2546 **MCP服务器OAuth 2.1+PKCE支持**](https://github.com/sipeed/picoclaw/issues/2546): 对标主流AI服务，旨在降低MCP服务器集成门槛。虽然尚无直接的实现PR，但此功能若实现，将对PicoClaw的生态建设产生积极影响。

- **路线图信号**:
    - **多模型兼容性成为焦点**：无论是Gemini的Schema兼容性问题 (#2668)，还是OpenRouter的推理泄漏 (#2745)，以及Anthropic的模型ID问题 (#2665)，都指向了项目在支持多种AI提供者时的适配挑战。维护者正在通过PR (#2740, #2746) 积极应对。
    - **安全与健壮性被重视**：PID检查 (#2720) 和路径解析 (#2749) 的Bug被高亮，且后者已有PR，说明项目对服务稳定性和底层安全机制越来越关注。

## 7. 用户反馈摘要

- **痛点**:
    - **服务不可靠**: 单例PID检查的Bug (#2720) 直接导致服务启动失败，是当前最严重的用户痛点，会极大打击自部署用户的信心。
    - **功能使用障碍**: Gemini和Anthropic模型的问题 (#2668, #2665) 使得特定用户无法正常使用这些强大的模型，影响了他们的使用体验。
    - **输出异常**: OpenRouter推理泄漏 (#2745) 和DeepSeek流式输出问题 (PR #2740) 导致模型返回内容不符合预期，属于用户可见的质量问题。

- **满意/采纳部分**:
    - 社区提交的Bug报告和修复PR被快速关注和回应，例如对OpenRouter推理泄漏问题的文档修复 (PR #2746) 和对路径问题的修复 (PR #2750)，体现了项目对用户反馈的重视和敏捷的响应能力。

## 8. 待处理积压

- **[Stale PR #2163] 修复Google Antigravity令牌刷新时的OAuth作用域问题 (已打开35天)**
  - **链接**: [#2163](https://github.com/sipeed/picoclaw/pull/2163)
  - **状态**: 自3月29日创建以来未有实质性更新，Label已标注`stale`。
  - **分析**: 此PR修复了一个特定场景（Google Antigravity/Cloud Code Assist）下的认证问题。虽然场景小众，但长期未合入可能导致相关用户无法正常使用服务。建议维护者在有精力时评估并处理，避免代码分歧加剧。

- **[Stale PR #2260] 添加xAI兼容支持 (已打开31天)**
  - **链接**: [#2260](https://github.com/sipeed/picoclaw/pull/2260)
  - **状态**: 自4月2日创建后更新为`stale`。
  - **分析**: 这是一个功能性的增强PR，旨在支持xAI的API。xAI是社区关注的新兴模型提供者，支持它对吸引新用户有益。此PR长期积压，可能会让期待此功能的贡献者和用户感到失望。建议维护者审查并决定是否合并还是需要改进。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目日报 — 2026-05-03

## 今日速览
过去24小时项目保持高度活跃：共处理 **13 条 Issues**（新开/活跃 11，关闭 2）和 **18 条 PR**（待合并 11，合并/关闭 7）。社区贡献集中解决了多个关键 Bug（如 `host-sweep` 读库崩溃、OneCLI 标识符冲突、Slash 命令静默失效），同时有 **Signal 反应支持**、**OpenCode 提供商** 等新功能 PR 提交。OpenRC 系统兼容性问题（Telegram 连接、Docker 启动失败）成为当日社区关注焦点。整体项目健康度良好，修复节奏快，功能演进清晰。

## 版本发布
无新版本发布。

## 项目进展
今日合并/关闭了 **7 个重要 PR**，显著提升了稳定性与功能覆盖面：

- **#2179** `fix: sanitize OneCLI agent identifiers` — 修复了 `container-runner.ts` 中下划线替换为连字符的问题，解决 #2046 中 “Not logged in” 异常。  
- **#2178** `Andy ops fixes: 10 issues` — 一次性修复了浏览器故障、Maps 403、Twitter token 缺失、容器超时、LinkedIn 0/天、邮件发送为零、线索评分卡住、Mahindra 投诉、Facebook 队列不发布、CLI 自启不稳定等 10 个运营问题。  
- **#2181** `fix(poll-loop): slash commands silently broken on warm containers` — 修复了 `follow-up poller` 过滤 `/clear` 并静默失效的 Bug，确保所有 Slash 命令在温容器中正常执行。  
- **#2183** `fix(host-sweep): reopen outbound DB as writable for orphan claim cleanup` — 解决 #2151 引入的只读数据库写入崩溃，Sweep 不再因 `processing_ack` 孤行而阻塞消息投递。  
- **#2190** `fix: Atom フィード（YouTube等）の link 要素をオブジェクト形式で正しくパースする` — 修复 `fast-xml-parser` 导致 Atom 轮询崩溃的问题，新增 `extractLink()` 统一处理 `string`/对象/数组格式。  
- **#1931** `feat: v1 → v2 migration to setup flow (experimental)` — 合并实验性集成迁移脚本，支持从 v1 安装自动端口到 v2 环境。  
- **#2192** `Add DeltaChat channel adapter` — 新增 DeltaChat 通道适配器（Feature Skill），扩展消息渠道矩阵。

> 上述合并修复覆盖了 **数据库写入、路由标识、容器轮询、频道解析、迁移流程** 等核心模块，项目整体向更稳定、更易用的方向迈出坚实一步。

## 社区热点
今日讨论热度分散，但以下议题吸引了最大关注：

- **#2188** `host-sweep: "attempt to write a readonly database" every tick` — 在关闭前（已由 #2183 修复）该 Issue 引发用户共鸣，突出展示了生产环境下的稳定性痛点。  
- **#2185** `claude-md-compose.ts builds CLAUDE.md without importing CLAUDE.local.md` — 用户指出代码注释声称 `CLAUDE.local.md` 会被“Claude Code 自动加载”，但实际上在构建时未加入 `@` 引用，导致每个 Agent 组的本地记忆从未被加载。该讨论揭示了文档与实现之间的不一致。  
- **#2200** / **#2199** `Telegram connection initialisation with OpenRC is failing` & `installation script - Docker failed to start in OpenRC` — 用户在非 systemd 系统（OpenRC）上连续报告安装与配对失败，反馈集中在 **初始化脚本的 init 系统兼容性** 上，预计后续会增加针对性的支持或文档说明。

## Bug 与稳定性
按严重程度排列当日报告的 Bug（附已存在 Fix PR 的标注）：

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| **Critical** | #2188, #2196 | `host-sweep` 因试图写入只读数据库 (`outbound.db`) 导致每次 tick 崩溃，阻塞消息投递 | 已由 **#2183** 修复并合并 |
| **Critical** | #2046 | OneCLI agent identifier 含下划线被拒绝（400），导致凭据获取失败 | 已由 **#2179** 修复并合并 |
| **High** | #2181 | 温容器上所有 Slash 命令（`/clear` 等）静默失效 | 已由 **#2181** 修复并合并 |
| **High** | #2186 | CLI 通道 `namespacedPlatformId` 产生 `cli:local`，导致路由器查找失败、无回复 | 有 PR **#2187** 修复中（添加 CLI 通道特例） |
| **Medium** | #2194 | WhatsApp LID→phone JID 映射在服务重启后丢失，导致基于 LID 的发送者路由失败 | 待处理（无 Fix PR） |
| **Medium** | #2193 | `init-first-agent` 存储带 `whatsapp:` 前缀的平台 ID，原生适配器发出的 JID 无前缀，造成静默路由失败 | 待处理 |
| **Medium** | #2191 | `migrate-v2.sh` 在 `sqlite3` CLI 未安装时显示误导性“registered_groups missing”错误 | 待处理 |
| **Low** | #2185 | `CLAUDE.md` 未导入 `CLAUDE.local.md`，导致每组 agent 的本地记忆从未被 SDK 加载 | 待处理（需更新文档或修改组装配逻辑） |
| **Low** | #2200, #2199 | OpenRC 系统下 Telegram 配对挂起、Docker 启动失败 | 待处理（可能需增加 init 系统支持） |
| **Low** | #2195 | `add-gmail-tool` 不支持多 Gmail 账户且无文档或变通方案 | 待处理 |

## 功能请求与路线图信号
当日提交的新功能需求与已有 PR 共同描绘了下一版本的演进方向：

- **Signal Reactions** — PR #2203 同时支持入站/出站 Signal 反应（基于 `content.operation === 'reaction'`），与现有 `add_reaction` MCP 工具联动，预计很快可合并。  
- **Voice Transcription V2** — PR #2003（长期开放）将转录移至 agent 容器，PR #2202 为其添加上游 Signal 适配器 emit，标志着语音处理走向“主权模式”。  
- **自定义模型/提供商** — PR #2201 新增 OpenCode provider 并支持通过环境变量配置 Claude 自定义模型，社区对模型灵活性的需求持续高涨。  
- **DeltaChat 频道** — PR #2192 已合并，扩展了去中心化通信能力。  
- **Matrix E2EE 频道** — PR #1624（自 4 月 4 日开放）仍待审核，但已包含完整 Matrix 加密通道 + 每 group 模型/effort 配置，是路线图中重量级功能。  
- **Home Assistant MCP 集成** — PR #1327（自 3 月 22 日开放）悬浮已久，是智能家居控制的重要诉求。  
- **Token 性能优化** — Issue #2189 用户提交多项 token 效率改进建议（如减少前缀引导、合并动态提示等），并主动表示“Happy to submit PRs”，可能在未来版本中吸收。

## 用户反馈摘要
从 Issues 和 PR 评论中提炼的真实痛点与使用场景：

- **“`host-sweep` 每 tick 崩溃”**（#2188, #2196）：在 session 容器未运行时，Sweep 瞬间写入只读库 → 崩溃 → 遗留 `processing_ack` 行 → 后续消息被阻塞。**用户原话**：“sweep crashes with `SqliteError`，stalled sessions never cleared”。  
- **“OneCLI agent identifier rejected”**（#2046）：迁移后发现 agent group ID 中的下划线导致 `container-runner.ts` 中所有容器启动凭据失败。**用户** dr-pabs 通过 `replace(/_/g, '-')` 自行修复并提交 PR。  
- **“OpenRC 系统完全无法安装/使用”**（#2200, #2199）：用户 markhawrylak 在 Alpine 上运行 `bash nanoclaw.sh` 时 Docker 启动失败，Telegram 配对脚本等待 service 启动也因无 systemd 而永久挂起。**用户** 希望增加对 OpenRC 的支持说明。  
- **“CLAUDE.md 不加载本地记忆”**（#2185）：用户 tianglim 发现 `claude-md-compose.ts` 虽然注释声称 `CLAUDE.local.md` 会被自动加载，但实际从未在生成的 `CLAUDE.md` 中添加 import。**用户** 认为这导致 per-group 记忆配置完全失效。  
- **“Token 效率太低”**（#2189）：用户 mnolet 经测试发现 NanoClaw 在非编码场景下 token 消耗过大，**用户** 表示 “found nanoclaw very token inefficient & had a few easy wins”。  
- **“WhatsApp 路由静默失败”**（#2193, #2194）：用户 mshirel 报告了因平台 ID 前缀不一致、LID 映射未持久化导致的消息路由问题，**用户** 描述场景真实且影响范围大。

## 待处理积压
以下开放时间较长或对核心功能影响重大的 Issue/PR 需维护者关注：

| 编号 | 类型 | 内容 | 开放时间 | 备注 |
|------|------|------|----------|------|
| **#1017** | Issue | badge 应显示百分比（如 `50%`） | 2026-03-13 | 低优先级 `good first issue`，至今无人认领 |
| **#1327** | PR | Home Assistant MCP 集成技能 | 2026-03-22 | 长期未合入，可能因设计讨论停滞 |
| **#1624** | PR | Matrix E2EE 频道 + per-group 模型配置 | 2026-04-04 | 功能完整但一直未通过 review |
| **#2003** | PR | Voice Transcription V2（容器端） | 2026-04-25 | 重提交版本，依赖 #2202 的上游适配器，需一并审核 |
| **#2184** | PR | 轮询检测到过期 session 时立即重试而非发送错误 | 2026-05-02 | 已提交但待合并，对用户体验提升明显 |
| **#2182** | PR | `openInboundDb` 应识别内存测试 DB | 2026-05-02 | 测试基础设施修复，可加速 CI |
| **#2187** | PR | CLI 通道 `namespacedPlatformId` 修复 | 2026-05-02 | 已关联 #2186，等待合并 |
| **#2194** | Issue | WhatsApp LID→phone 映射不持久 | 2026-05-02 | 无关联 PR，长期存在可能影响生产用户 |
| **#2193** | Issue | `init-first-agent` 存储带前缀的平台 ID | 2026-05-02 | 与 #2194 相关，需统一处理 |
| **#2191** | Issue | `migrate-v2.sh` 错误提示误导 | 2026-05-02 | 小型 DX 问题，建议早日修复 |

---
*数据来源：GitHub Issues & PRs · 生成时间：2026-05-03*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是基于 NullClaw 项目数据的动态日报。

---

## NullClaw 项目动态日报 | 2026-05-03

### 1. 今日速览

项目今日活跃度极高，在过去 24 小时内合并了 **15 个 Pull Requests**，显示出强大的交付能力。核心贡献者主要集中在 **安全加固**（anti-spoofing、Sandbox 优化）和 **Zig 0.16 迁移后的稳定性修复** 上，特别是修复了导致 Mattermost 连接失败及 100% CPU 占用的高严重性回归问题。此外，社区关注点逐渐从功能开发转向 **低资源设备部署** 和 **基础兼容性** 问题，预示着项目可能正在吸引更多对轻量级运行环境有需求的用户。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

过去 24 小时是项目近期最活跃的合并日，共合入了 **15 个 PR**，涵盖了安全、核心 API、平台兼容性和 Bug 修复等多个方面，项目在稳定性和功能完备性上迈出了坚实的一步。

- **安全加固 (Security Hardening)**：
    - `#880 [CLOSED]` **PR: feat(security): wrap web_fetch and web_search output with anti-spoofing boundaries** - 通过对 `web_fetch` 和 `web_search` 的输出添加反欺骗边界（随机 ID、Unicode 同形异义字折叠），提升了针对提示注入攻击的防御能力。
    - `#875 [CLOSED]` **PR: security: add 3-tier risk classification and exec-prefix stripping** - 引入了中等风险等级，允许 `curl` 等网络命令在监督模式下使用，解决了用户反馈的痛点。同时增加了 `exec-prefix` 剥离功能以增强安全性。

- **核心稳定性与兼容性**：
    - `#873` & `#872 [CLOSED]` **PR: fix: Zig 0.16 Mattermost empty-body POST and gateway accept-loop CPU spin** - **高优先级修复**。解决了 Zig 0.16 迁移引起的关键回归问题，包括 Mattermost 消息发送失败和网关线程的 100% CPU 占用。**注意：这可能是两个相同或基于同一分支的 PR，建议维护者确认是否 PR #873 是最终合并的版本。**
    - `#877 [CLOSED]` **PR: fix(channels/mattermost): finalize allocating writer body before curlPost** - 修复了 Zig 0.16 下 HTTP POST 请求体缓冲区未正确刷新的问题，是修复 Mattermost 问题的关键一步。
    - `#876 [CLOSED]` **PR: fix(compat): replace readSliceShort with readVec in Stream.read to unblock HTTP/1.1 keep-alive clients** - 修复了 HTTP/1.1 keep-alive 客户端（如 `curl`）在读取响应时阻塞的问题，提升了协议兼容性。

- **API 与平台支持**：
    - `#780`, `#771`, `#770 [CLOSED]` **PRs: feat(api): REST Admin API** - 一系列大型 PR 最终合并，标志着 REST Admin API 的完整功能落地，包括运行时状态、会话管理、配置读写、渠道管理等。这为构建更轻量级的客户端（如 Mac 菜单栏应用、iOS/iPadOS 应用）提供了坚实基础。
    - `#856 [CLOSED]` **PR: fix(service): harden SysVinit script for RTC-less hardware** - 强化了 SysVinit/OpenRC 服务脚本，使其能在没有实时时钟（RTC）的硬件上更可靠地运行，体现了对嵌入式/低资源平台的关注。

### 4. 社区热点

今日社区讨论的焦点集中在 **低资源设备上的实用性** 问题上。

- **Issue #871 [OPEN]：`web_search` 在低资源设备上不可用**
  - **链接**: [Issue #871](https://github.com/nullclaw/nullclaw/issues/871)
  - **分析**: 该 Issue 获得了社区共鸣，指出 `web_search` 功能在低端设备上因缺乏内置 DuckDuckGo 支持而难以使用。用户 `uMendex` 提出了当前主流方案（使用 Brave API）的局限性，暗示项目应优先考虑离线或轻量级的搜索方案。这表明项目的用户画像正在向低功耗、低成本设备扩展，对项目的依赖和功能设计提出了新的要求（例如，是否有计划支持本地化或更轻量的搜索索引？）。

### 5. Bug 与稳定性

今日报告的 Bug 数量不多，但 Zig 0.16 迁移带来的一系列稳定性问题正在被快速修复，这极大地增强了项目的健康度。

- **严重**：Zig 0.16 迁移导致的 **Mattermost 通信失败** 与 **100% CPU 占用**。这是生产环境中的关键问题，PR `#873` 已将其修复并合并。
- **中等**：`curl` 在 `allowlist` 下仍然 `post` 失败（Issue #866）。这是一个安全隐患与功能灵活性之间的冲突，在早期版本中被归类为高风险而禁止。PR `#875` 已通过引入**中等风险等级**解决了此问题，允许 `curl` 在监督模式下使用。
- **遗留问题**：
    - **CLI 控制字符显示错误（Issue #865）**：CLI 中方向键等按键显示为控制字符垃圾。仍处于开放状态，尚无关联的修复 PR。这是 CLI 体验不佳的直接表现，可能会影响新用户的初次使用印象。
    - **线程休眠问题（PR #878，开放中）**：`thread.sleep` 在 POSIX 上未能真正挂起线程，导致在低负载时 CPU 占用偏高。这是对系统资源管理的一个精细优化。

### 6. 功能请求与路线图信号

- **低资源设备支持**：Issue `#871` 揭示了用户对在“弱、便宜、低资源设备”上运行 NullClaw 的强烈需求。
- **强化内建 Sandbox**：Issue `#882` 提议默认使用 Linux 的 Landlock LSM 作为沙箱后端，并停止启动时探测外部工具。这表明社区倾向于更 **零配置、更原生、更可靠** 的安全方案。该提案由核心贡献者 `mark-os` 提出，同时也是一个正在活跃讨论的 Issue，很可能被纳入下个版本的路线图。
- **安装与文档**：Issue `#820` 询问如何在 Debian 上安装 Zig。虽然看似基础问题，但反映了项目文档中可能缺少对基础依赖安装的引导，尤其是对于 Linux 新手。

### 7. 用户反馈摘要

- **痛点**：
    - **Web 搜索功能受限**（Issue #871）：社区成员表达了在资源受限设备上无法有效使用 `web_search` 的挫败感，认为当前依赖外部 API 的方案不切实际。
    - **CLI 体验不佳**（Issue #865）：用户报告 CLI 原生按键绑定失效，显示乱码，这严重影响了命令行环境下的基本交互体验。
    - **工具白名单策略僵化**（Issue #866）：用户发现即使将 `curl` 加入了 Allowlist，某些功能（如 POST 请求）仍无法正常使用，这与“已授权”的预期相悖。PR `#875` 的合入应能解决此问题。

### 8. 待处理积压

- **重要 Issue 待跟进**：
    - **Issue #820**：用户询问 Debian 上安装 Zig 的指南。创建近三周，虽有 4 条评论，但未被官方标记或分配。对于希望开始使用项目的新用户来说，这是一个明显的障碍。
    - **Issue #865** (`CLI shows ctrl characters`)：创建已逾 10 天，目前无关联的修复 PR。考虑到其对基础 CLI 体验的影响，建议给予更高优先级。
- **待合并 PR**：
    - **PR #878** (`fix(compat): use nanosleep on POSIX...`)：一个重要的性能优化 PR，旨在解决线程休眠机制在 POSIX 上不够高效的问题。已开放 3 天，建议尽快审核并合并，以优化系统资源占用。

---

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目日报 — 2026-05-03

## 1. 今日速览
项目整体活跃度极高：过去24小时内共处理20条Issue、43条PR，其中新开/活跃Issue 15条，新提交PR 37条（待合并）。**Reborn架构重构**依然是主线，serrrfirat密集提交了6个新的`[reborn]`设计Issue，定义turn协调、持久化、执行模型等核心边界；与此同时，社区新贡献者**abbyshekit**（独立贡献者）单日提交了14个PR，覆盖CLI备份、邀请系统、arm64 Docker支持、LLM修复等多个领域，表明项目在开源社区中的吸引力和协作效率正在快速提升。无新版本发布。

## 2. 版本发布
无。

## 3. 项目进展
今日共关闭5个Issue，合并/关闭6个PR，重点项目推进如下：

- **关键Bug修复**
  - [#3214] (thoughtSignature在Cloud Code SSE处理中丢失) **已关闭** — 此前两次修复（#1565、#1752）未能彻底解决Gemini 3.x的`INVALID_ARGUMENT`错误，本次通过[PR #3215](https://github.com/nearai/ironclaw/pull/3215)在SSE层补上了遗漏的序列化逻辑。
  - [#2818] (v0.26.0安装器在x86_64 Linux上失败) **已关闭** — 与Docker镜像发布流程相关，已通过更新工具链修复。
  - [#3144] [#3147] [#3145] (Reborn资源上限、审计记录、后台进程义务生命周期) **已关闭** — 三个`[reborn]`任务完成设计/定义，为后续实现扫清障碍。

- **社区贡献功能（待合并）**
  - [PR #3208](https://github.com/nearai/ironclaw/pull/3208) — **添加linux/arm64 Docker构建**（关闭#3168），被阻塞的Apple Silicon、AWS Graviton用户将能原生运行。
  - [PR #3178](https://github.com/nearai/ironclaw/pull/3178) — 新增`ironclaw backup --quick`便携式状态快照命令，配合[PR #3186](https://github.com/nearai/ironclaw/pull/3186)的`import backup`实现迁移闭环。
  - [PR #3187](https://github.com/nearai/ironclaw/pull/3187) — 添加魔法链接邀请系统，支持管理员生成一次性邀请URL，为试点用户提供免密登录。
  - [PR #3212](https://github.com/nearai/ironclaw/pull/3212)（核心贡献者zmanian）— 添加Reborn事件投影服务，实现从`DurableEventLog`派生出`ThreadTimeline`和`RunStatusProjection`，是Reborn持久层的关键组件。

**总体评估**：项目在“修复遗留问题+重构核心架构+吸引外部贡献”三条线上并行推进，代码库健康度良好。

## 4. 社区热点
- **最热Issue**：[#3016](https://github.com/nearai/ironclaw/issues/3016) — Reborn cutover blocker: add reference AgentLoopHost facade（3条评论）。作为Reborn过渡阻塞器之一，该Issue定义了主机层AgentLoopHost门面，是协调多执行模型（交互式聊天 vs 后台任务）的第一步，核心开发者与架构师在此讨论接口契约细节。
- **最热PR（讨论量）**：无单一PR评论数突出，但**abbyshekit**贡献者今天提交的14个PR在多个领域引发关注，其中[PR #3218](https://github.com/nearai/ironclaw/pull/3218)（NEAR Intents trial mode）和[PR #3207](https://github.com/nearai/ironclaw/pull/3207)（NEAR Intents trading agent foundation）显示了社区对DeFi集成方向的高度兴趣。
- **用户诉求分析**：社区对LLM兼容性（Gemini、DeepSeek）和跨平台支持（ARM64）反应强烈，多个PR快速跟进表明维护者重视用户反馈。

## 5. Bug 与稳定性

| 严重程度 | Issue | 摘要 | 修复状态 |
|---------|-------|------|----------|
| **严重** | [#3214](https://github.com/nearai/ironclaw/issues/3214) | Gemini 3.x SSE handler丢失thoughtSignature，导致工具调用HTTP 400错误 | **已关闭**，[PR #3215](https://github.com/nearai/ironclaw/pull/3215)待合并 |
| **高** | [#3201](https://github.com/nearai/ironclaw/issues/3201) | DeepSeek工具调用不工作，`deepseek-v4-flash`查询新闻时报错 | **开放中**，暂无关联PR |
| **中** | [#2344](https://github.com/nearai/ironclaw/issues/2344) | Staging Web UI页面加载时出现TypeError、ReferenceError和CSP违规（已存在22天） | **开放中**，待定位 |
| **低** | [#3132](https://github.com/nearai/ironclaw/issues/3132) | LLM将数字参数序列化为字符串导致`strict_u64`拒绝 | [PR #3206](https://github.com/nearai/ironclaw/pull/3206)待合并 |
| **低** | [#3083](https://github.com/nearai/ironclaw/issues/3083) | Admin UI用户创建表单无防抖，快速点击导致重复创建 | [PR #3209](https://github.com/nearai/ironclaw/pull/3209)待合并 |
| **低** | [#3011](https://github.com/nearai/ironclaw/issues/3011) | `ironclaw run`不输出stderr日志，即使在`RUST_LOG=debug`下 | [PR #3216](https://github.com/nearai/ironclaw/pull/3216)待合并 |
| **低** | [#3035](https://github.com/nearai/ironclaw/issues/3035) | Agent忽略用户配置的显示名称（始终自称“IronClaw”） | [PR #3213](https://github.com/nearai/ironclaw/pull/3213)待合并 |

**注意**：DeepSeek工具调用故障（#3201）是唯一尚无修复PR的活跃严重Bug，需优先关注。

## 6. 功能请求与路线图信号
- **ARM64支持**（#3168）已被[PR #3208](https://github.com/nearai/ironclaw/pull/3208)响应，预计在下一版本（v0.28.0）中合入。
- **NEAR Intents集成**：[PR #3207](https://github.com/nearai/ironclaw/pull/3207)和[PR #3218](https://github.com/nearai/ironclaw/pull/3218)分别定义了交易代理基础和试用模式，结合已存在的portfolio工具，表明项目正将AI能力扩展到DeFi场景。
- **用户邀请系统**（#3187）暗示产品化推进，可能为即将到来的付费或试点功能铺路。
- **音频管道**（#90）虽有更新但仍无实质代码，优先级可能已被Reborn压后，需社区推动。

**路线图信号**：Reborn重构仍然是最高优先级，但从社区PR分布看，CLI工具、跨平台部署、DeFi集成正在成为第二梯队热点。

## 7. 用户反馈摘要
- **thomasmaerz**（#3214）：“两次关闭声称修复了Gemini 3.x错误，但HEAD上依然复现，请重新开放。” 表明用户对修复完整性要求高，开发者已响应并在SSE层彻底修复。
- **joe-rlo**（#2344）：“Staging环境每次加载都有红色错误，影响开发体验。” 该问题已存在三周无实质性进展，可能会影响外部贡献者的信心。
- **CaveNightingale**（#3201）：“用DeepSeek查询新闻，工具调用直接报错，无法使用。” 报告清晰，但目前无维护者留言。
- **thisisjoshford**（#2818）：“v0.26.0安装器损坏，无法在Linux x86_64上通过curl安装。” 该问题已在v0.26.1中修复（今日关闭）。
- **magnusviri**（#2963）：“按文档拉取Docker镜像得到`pull access denied`，因为文档写的是`nearai/ironclaw`而不是`nearaidev/ironclaw`。” 已被[PR #3217](https://github.com/nearai/ironclaw/pull/3217)修复。

总体用户情绪：对LLM兼容性敏感，对安装/配置体验要求高，对CLI工具和Docker多架构支持有明确需求。

## 8. 待处理积压
- [#90](https://github.com/nearai/ironclaw/issues/90)（音频管道）— 自2026-02-14提出，至今无实质性PR。虽标记P1-P2，但被Reborn及其他高优任务挤压。建议维护者明确是否推迟至Reborn完成后。
- [#2344](https://github.com/nearai/ironclaw/issues/2344)（Web UI控制台错误）— 三周未更新，影响外部QA测试。建议至少标注预期修复版本或临时解决方案。
- [#2700](https://github.com/nearai/ironclaw/pull/2700)（显示对话标题而非UUID）— 核心贡献者zmanian提交已两周，至今未合并。该PR解决了长期UX痛点，请维护者安排review。

---

*日报基于GitHub数据自动生成，分析截止时间2026-05-03 00:00 UTC。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 LobsterAI 开源项目分析师，以下是基于 2026-05-03 数据的项目动态日报。

---

# LobsterAI 项目动态日报 | 2026-05-03

## 1. 今日速览

今日项目整体活跃度中等偏上。虽然过去24小时无新的 Issue 提交或 PR 合并，但项目维护者与社区贡献者正在积极推进 4 个待合并的 Pull Request (PR)，主要集中在配置同步、模型支持和用户体验修复方面。其中 #1879 修复了一个可能导致用户手动配置丢失的关键数据持久化问题，意义重大。项目目前暂无新版本发布，代码库处于稳定的功能增强与 bug 修复周期。

## 2. 版本发布

**无**

过去24小时内没有新版本发布。

## 3. 项目进展

今天暂无 PR 被合并或关闭，但以下 4 个 PR 处于待合并状态，标志着项目在多个维度取得了显著进展。一旦合并，将直接提升项目稳定性与用户体验。

- **#1879 [OPEN]：修复配置同步时手动添加的插件路径被清除的问题** - 这是一个重要的稳定性修复。它解决了当 LobsterAI 执行配置同步时，会清空用户手动添加的第三方插件路径的 bug。修复后，用户通过 `pm install` 等工具安装的社区插件配置将得到保留。**项目健康度提升信号**。
- **#813 [OPEN]：为小米渠道新增 MiMo V2 Pro 和 V2 Omni 模型** - 这是一个面向用户的特性增强。它扩展了小米渠道的模型支持，使项目能更好地与小米最新的大模型生态对接。
- **#1181 [OPEN]：修复 OpenClaw 主代理会话在会话列表中错误显示的问题** - 这是一个显著的 UX 优化。它将内用于心跳/定时任务路由的主代理会话隐藏起来，避免了普通用户在选择会话时产生困惑。
- **#1191 [OPEN]：修复定时任务通知渠道选择器的体验缺陷** - 这是一个用户反馈驱动的体验修复。它修复了 POPO、企业微信渠道不显示、微信渠道被错误标记为“暂不支持”以及渠道显示为原始技术编码等问题。

## 4. 社区热点

今日无特别活跃的讨论或高评论数的 Issue/PR。所有 PR 的评论数均为 `undefined`，表明这些改进可能由核心团队或活跃贡献者直接提交，尚未引发广泛的社区讨论。

- **潜在热点分析**：PR #1879 (netease-youdao/LobsterAI PR #1879) 修复了一个“静默”删改用户数据的问题，这通常是用户最为敏感的。虽然评论数不高，但该问题的解决对于维护社区信任至关重要，属于“高影响力，低讨论度”的技术修复。

## 5. Bug 与稳定性

今日无新的 Bug 报告。以下为针对已有问题的修复 PR，按严重程度排列：

1.  **（高）数据丢失风险 - PR #1879 (netease-youdao/LobsterAI PR #1879)**: 配置同步时，用户手动添加的第三方插件路径被静默删除。这是一个严重的配置持久化问题，可能导致用户自定义的插件环境失效。现已有修复 PR。
2.  **（中）功能缺陷 - PR #1191 (netease-youdao/LobsterAI PR #1191)**: 定时任务通知渠道选择存在多项缺陷，包括部分渠道不显示、标签错误、展示编码而非友好名称。这降低了定时任务功能的可用性。现已有修复 PR。

## 6. 功能请求与路线图信号

今日无新功能请求。但从已存在的 PR 可以分析出项目路线图的一些潜在方向：

- **硬件/平台兼容性**：PR #813 (netease-youdao/LobsterAI PR #813) 表明团队在持续跟进并支持主流大模型厂商的最新产品，这是维持项目竞争力的关键。
- **内部代理体验优化**：PR #1181 (netease-youdao/LobsterAI PR #1181) 和 #1879 (netease-youdao/LobsterAI PR #1879) 都聚焦于 **OpenClaw** 代理框架，一个优化其内部代理对用户的可见性，另一个保障其插件的配置稳定性。这表明团队正在对内部 Agent 机制进行雕琢，为更复杂的 Agent 工作流打下基础，这很可能是一个重要的路线图方向。

## 7. 用户反馈摘要

今日无直接的用户评论数据。但从 PR 的描述中，我们可以推断出用户的真实痛点：

- **痛点：配置被覆盖**：用户通过命令行或脚本等手动方式安装插件后，LobsterAI 的同步操作会不打招呼地将其清除，导致用户困惑和重复劳动（源自 PR #1879）。
- **痛点：功能缺失与错误信息**：用户在尝试配置定时任务通知时，发现已启用的渠道（如 POPO、企业微信）不可选，而可选项（微信）却被错误地标记为不支持。这种不一致的功能状态给用户带来挫败感（源自 PR #1191）。
- **痛点：UI 可读性差**：渠道选择器和技术设置区域直接显示 `moltbot-popo` 这样的内部编码，普通用户难以理解和使用，增加了学习成本（源自 PR #1191）。

## 8. 待处理积压

以下 PR 已开启超过一个月且未标记为“待回应”（stale），提醒维护者关注并推动其进展：

- **PR #813 - [stale] - 小米渠道新增模型** (netease-youdao/LobsterAI PR #813) - 开启于 2026-03-25，最后一次更新是 2026-05-02。此 PR 功能明确，风险较低，主要涉及配置文件变更。等待时间较长，建议尽快确认并合并。
- **PR #1191 - 修复定时任务通知渠道缺陷** (netease-youdao/LobsterAI PR #1191) - 开启于 2026-04-01。此 PR 解决了多个明确的用户体验 Bug，建议优先 Review 并进行代码审查。

这些积压 PR 的长期搁置可能影响社区贡献者的积极性，并让用户继续忍受这些已知问题。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 Moltis 项目动态日报。

---

# Moltis 项目动态日报 | 2026-05-03

## 1. 今日速览

过去24小时内，Moltis 项目整体活跃度中等。社区共提交了4条新的 Issues，其中包含1个关键的功能使用 Bug 和1个文档问题，反映了用户在生产环境中遇到的具体障碍。Pull Request 方面有3条更新，其中一项关于沙箱支持的重大功能 PR（#942）持续收到关注，显示出项目在云端部署能力上的探索。项目虽未发布新版本，但在核心功能优化与国际化方面有持续的代码贡献。

## 2. 版本发布

无

## 3. 项目进展

- **PR #339 [CLOSED] feat(i18n): add zh-TW Traditional Chinese locale support** - 经过近两个月的开发与审查，该 PR 已于今日合并，为项目正式添加了繁体中文（台湾）语言支持。这意味着 Moltis 的 macOS 和 Web 应用现在支持完整的繁体中文界面，包括 UI 字符串、区域检测和语言选择。这是项目国际化进程中的一个重要里程碑，特别是在大中华区市场拓展方面迈出了实质性一步。
  - 链接：[#339](https://github.com/moltis-org/moltis/pull/339)

## 4. 社区热点

- **Issue #959 [Bug]: DeepSeek - Error: The reasoning_content in the thinking mode must be passed back to the API.** - 该 Bug 报告是目前社区关注的焦点。用户在使用 DeepSeek 推理模式时遇到 API 错误，要求必须回传 `reasoning_content`。这是影响核心对话功能的严重问题，虽然评论数不高，但直接关联到模型的可用性，预计会引起更多用户的共鸣。
  - 链接：[#959](https://github.com/moltis-org/moltis/issues/959)

- **PR #942 [OPEN] feat(sandbox): remote & multi-backend sandbox support** - 该 PR 虽不是今日新开，但其讨论热度持续。它旨在解决在各类云平台（如 DigitalOcean, Fly.io, Render）上无法使用 Docker-in-Docker 的痛点，通过引入远程和多后端沙箱支持来提升项目的部署灵活性。这表明社区对 Moltis 在云端环境下的稳健运行有着强烈诉求。
  - 链接：[#942](https://github.com/moltis-org/moltis/pull/942)

## 5. Bug 与稳定性

- **严重 Bug: Issue #959 [Bug]: DeepSeek - Error: The reasoning_content in the thinking mode must be passed back to the API.**
  - **描述**: 用户在使用 DeepSeek 模型并开启“思考模式”时，API 强制要求回传 `reasoning_content`，否则报错。这导致对话过程中断，是影响用户体验的核心 Bug。
  - **严重程度**: 高（影响核心功能）
  - **Fix PR**: 无
  - 链接：[#959](https://github.com/moltis-org/moltis/issues/959)

- **文档问题: Issue #958 [Docs]: Voice Services > Local TTS Provider Setup - Documentation links to unmaintained/archived repos**
  - **描述**: 文档中关于本地 TTS 提供商的设置指南链接到了已不再维护或归档的仓库。这会使用户在配置本地语音功能时遇到困难或使用过时软件。
  - **严重程度**: 中（影响配置体验，但不影响核心运行）
  - **Fix PR**: 无
  - 链接：[#958](https://github.com/moltis-org/moltis/issues/958)

## 6. 功能请求与路线图信号

- **Issue #960 [Enhancement]: Add SwarmScore — Portable Trust Rating for AI Agents** - 社区成员提议将 SwarmScore 作为 AI Agent 的可移植信任评级系统。这反映了用户对 AI 代理的**声誉管理与可信度验证**有了明确需求，希望能够在不同平台间衡量 Agent 的可靠性。尽管该项目由外部提出，但其与自治代理框架的理念高度契合，值得项目维护者评估作为未来安全或质量评估机制的可能性。
  - 链接：[#960](https://github.com/moltis-org/moltis/issues/960)

- **Issue #956 [Feature]: Add image generation support (gpt-image-2) via OpenAI Codex OAuth** - 用户请求通过 OpenAI Codex OAuth 集成 `gpt-image-2` 模型，支持图像生成功能。这表明用户已经不满足于单纯的文本处理，对**多模态能力（图像生成）** 有强烈期待。结合项目已有的 `penso` 等核心贡献者动态，这有可能成为下一个小版本迭代的候选方向。
  - 链接：[#956](https://github.com/moltis-org/moltis/issues/956)

## 7. 用户反馈摘要

- **对 DeepSeek 推理模式的困惑**: 在 Issue #959 中，用户详细描述了使用 DeepSeek 思考模式时遇到的 API 约束，并明确提到了这是未预料到的行为。用户的痛点在于**必须手动回送 `reasoning_content`**，这可能打破了 Moltis 作为对话助手“即开即用”的体验，用户期待该项目能自动处理此类模型内部逻辑。
- **对文档维护的期待**: Issue #958 的用户指出了文档链接失效的问题，这反映出用户对文档的准确性和时效性有较高要求。用户希望项目能确保参考资料的可用性，避免因外部依赖库的变动而导致配置失败。

## 8. 待处理积压

- **重要功能 PR (PR #942)**: **feat(sandbox): remote & multi-backend sandbox support** 已开放3天，获得了社区的关注，但尚未合并。此 PR 解决了在无 Docker-in-Docker 环境下部署 Moltis 的痛点，对于项目的云原生部署至关重要。维护者应加快审查，以提升项目在不同云平台的可用性和鲁棒性。
  - 链接：[#942](https://github.com/moltis-org/moltis/pull/942)

- **长期待评估 PR (PR #339)**: 尽管 PR #339（繁体中文支持）已于今日合并，但值得注意的是，它从创建到合并耗时近两个月（2026-03-05 至 2026-05-02）。这表明项目维护者对于非核心功能（如本地化）的审查周期较长。其他类似的、非紧急的本地化或小功能 PR 可能会面临同样的问题。维护者应考虑优化此类贡献的处理流程。
  - 链接：[#339](https://github.com/moltis-org/moltis/pull/339)

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的CoPaw (github.com/agentscope-ai/CoPaw) 项目数据，现为您生成2026年5月3日的项目动态日报。

---

# CoPaw 项目动态日报 | 2026-05-03

## 1. 今日速览

过去24小时内，CoPaw 项目社区活跃度极高，尤其在 issue 和 PR 的提交方面表现强劲，共产生13条 Issue 和14条 PR。大量新功能请求和 Bug 报告集中在模型稳定性、多平台交互体验和开发者工具链优化上。尽管没有新版本发布，但多个关键功能（如火山引擎Provider、长期记忆、巴西葡萄牙语支持）的PR已处于审核阶段，显示了项目在功能扩展和国际化方面的积极进展。整体而言，项目处于高热度的社区驱动发展阶段，稳定性修复与功能创新并行。

## 2. 版本发布

无。

## 3. 项目进展

今日共有4个PR被合并/关闭，标志着项目在代码质量和社区贡献整合上的稳步推进。
- **#4012 [CLOSED] chore(version): bumping version to 1.1.6b1**：版本号已提升至 `1.1.6b1`，预示着下一个预发布版本即将到来。
- **#1642 [CLOSED] feat(error code): add error code**：实现了错误码系统，将极大地提升开发者进行错误排查和系统稳定性监控的效率。
- **#1055 [CLOSED] feat: add MiniMax as a built-in provider**：MiniMax 正式被集成为内置Provider，丰富了模型的多样性，尤其利好中国区用户。
- **#559 [CLOSED] fix: remove failed user messages from memory**：修复了因用户输入格式错误导致会话记忆“中毒”的Bug，增强了对话系统的鲁棒性。

此外，多个高质量PR处于“审核中”状态，显示项目功能正在快速演进：
- **#3994 [OPEN] Feat/volcengine provider**：新增火山引擎及其coding plan provider支持。
- **#4007 [OPEN] fix: 修复 #3182 和 #3828，新增 MemoryHook 长期记忆增强**：修复了长期记忆相关的关键Bug，并新增 `MemoryHook` 机制以增强记忆能力。
- **#4009 [OPEN] feat(i18n): add Brazilian Portuguese (pt-BR) locale support**：添加巴西葡萄牙语支持，项目国际化迈出重要一步。

## 4. 社区热点

今日社区讨论焦点高度集中在**模型的可靠性与可用性**上，背后体现了用户在生产环境中对稳定性的核心诉求。

- **#1327 [Feature]: Model fallback chain for automatic rate limit handling**：该Issue共获得5条评论，是社区长期关注的自动模型故障转移机制。用户希望当主模型遭遇限流或服务中断时，系统能自动切换到备用模型，是保障服务连续性的关键需求。
- **#3640 [Bug]: MCP client 内部 TaskGroup 异常导致 Agent 假死**：获得6条评论，是今日讨论最激烈的问题。用户报告了Agent假死的严重Bug，该问题导致系统无响应且不报错，严重影响了使用体验，社区的反馈集中在排查这类静默失败的原因。

## 5. Bug 与稳定性

今日报告的Bug问题严重性分级如下，多数问题在社区中获得了初步讨论或已有对应的修复PR。

- **严重**：
    - **#3640 [Bug]: MCP client 内部 TaskGroup 异常导致 Agent 假死**：Agent 假死且无日志，属于静默失败问题，排查和修复难度高。目前尚无对应 Fix PR。
- **中等**：
    - **#4006 [Bug]: Reasoning Content Not Filtered in OpenAI-Compatible Provider**：MiniMax（中国区）API provider 未过滤推理过程内容，可能导致输出异常。
    - **#3991 [Bug]: Ollama 频道无法携带对话历史，导致会话记忆丢失**：Ollama 频道功能存在缺陷，无法正确传递对话上下文。与#4007 PR（修复长期记忆）有部分关联。
    - **#4005 [PR] fix(#3041): WSL2 NAT网络环境下 agent error**：已有对应 PR (#4005) 正在修复WSL2网络环境下的超时问题。
- **低影响**：
    - **#4000 [Bug]: 微信对话与浏览器操作不同步 + 网页版语音输入功能缺失**：属于功能缺失和UI/UX层面问题。

## 6. 功能请求与路线图信号

社区新提出的功能请求集中体现了用户对**生产级能力**（如高可用性、可测评性）和**协作体验**（如可视化交互）的渴望。

| 功能请求 | 对应Issue | 关联PR/讨论 | 可能纳入路线的信号 |
| :--- | :--- | :--- | :--- |
| 模型故障转移/回退 | #1327， #4011， #3789 | 无直接关联PR | **强信号**。这是最强烈的社区呼声（多个issue重复提出），是提升系统可靠性的必备功能。 |
| Agent测评功能 | #4008 | 无 | **中等信号**。用户希望在汇报POC成果时获得量化数据，是推动企业级采用的刚需。 |
| 可视化共享交互区域 | #4002 | 无 | **弱信号**。功能描述详细，属于前瞻性的用户体验创新，短期内进入路线的可能性较低。 |
| 对话中删除单条消息 | #4001 | 无 | **弱信号**。属于基础UX优化，实现成本较低，但社区优先级可能不高。 |
| 多平台渠道对话中止 | #4010 | #3525 (Discord线程隔离PR) | **中等信号**。与PR#3525的理念相通，旨在增强对多平台对话的控制力。 |

值得注意的是，`max_input_length` 自动推导 (#4004) 和 `MemoryHook` (#4007) 这两个由社区贡献者提交的PR，直接回应了困扰用户已久的模型配置和记忆问题，极有可能被优先合入。

## 7. 用户反馈摘要

从今日的Issue中，可以提炼出几个典型的用户痛点和期望场景：

- **稳定性与可靠性是用户第一痛点**：一位用户 (@wxfvf) 报告了Agent假死的严重问题，并详细描述了自行排查的过程，体现了用户对系统稳定性的高要求和对排查难的无奈。另一位用户 (@fsls) 连续提交了关于“模型回退”和“打断/终止”功能的请求，揭示了用户在使用中“无法控制”的无力感。
- **多平台体验一致性是核心诉求**：用户 (@git-coinco) 反馈微信对话与Web端操作不同步，这暴露了多入口项目在信息同步上的重要挑战。
- **企业对测评能力存在刚性需求**：用户 (@linhuang0405) 明确提出，缺少测评功能导致无法向领导汇报 CoPaw 作为生产环境Agent平台的优势，这直接影响了项目的企业级推广。
- **Ollama/本地模型用户对记忆功能特别敏感**：用户 (@emptFF) 详细描述了自己在Ollama频道遇到的“会话记忆丢失”问题，并排除了模型本身的问题，将焦点定位在客户端代码，展现了深度用户的技术素养。

## 8. 待处理积压

以下为需要维护者关注的长期未响应或瓶颈式Issue/PR：

- **#1327 [Feature]: Model fallback chain**：创建于38天前，社区讨论热烈，但长期未获得官方响应或纳入开发计划。这是社区呼声最高的功能之一，其进度直接影响社区信心。
- **#3640 [Bug]: Agent 假死**：创建于12天前，是今日社区讨论的中心，但问题严重（导致无响应）且无对应Fix PR，需优先定位。
- **#3525 [PR] feat(cron): create Discord thread**：该PR自4月17日打开，已超过两周处于“审核中”状态，可能因需求复杂或存在冲突而停滞。这是提升Discord频道使用体验的重要功能，建议尽快推进审核或提供反馈。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，根据您提供的 ZeroClaw 项目数据，我为您生成了 2026 年 5 月 3 日的项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-05-03

## 今日速览
今日项目活跃度极高，社区提交了大量 Issues（50条）和 Pull Requests（33条），但合并率偏低（仅6/33），尤其是未发布新版本，反映出项目正处于大量功能开发与缺陷修复的并行阶段。社区焦点集中在 **DeepSeek 兼容性**、**8.0 版本配置重构** 以及 **技能（Skills）生态建设** 上。同时，大量 P1/P2 级别的 Bug 被报告，表明稳定性测试仍需加强，但核心维护团队响应迅速，已为多个关键 Bug 提交了修复 PR。

## 项目进展
今日有 **6 个 PR 被合并或关闭**，主要集中在配置和CI方面，推进了项目的稳定性和开发体验。
- **[#6087] fix(config): support env var overrides for channel tokens** - 已关闭：允许通过环境变量覆盖 Slack、Discord、Telegram 等渠道的令牌配置，增强了配置的灵活性和安全性。
- **[#5256] fix(ci): remove stale main.py dep, upgrade rumqttc, suppress RUSTSEC-2026-0049** - 已关闭：清理了过时的 CI 依赖并升级了核心库，修复了预存的 CI 错误，为后续贡献者扫清了障碍。

这些改动虽然不涉及用户侧的新功能，但提升了项目的可维护性和安全性，有助于吸引更多社区贡献。

## 社区热点
今日社区讨论热度最高的议题集中在 **自我认知缺陷** 与 **长期记忆** 两大主题上。有两个 Issue 获得了最高的 9 条评论，它们代表了用户深层需求：

1.  **[#5862] [Bug]: zeroclaw does not know it can add cron**
    - **链接**: [Issue #5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862)
    - **分析**: 用户反映，尽管 ZeroClaw 具备 `cron` 功能，但在被要求定时执行任务时，AI Agent 自身却不知道可以使用该工具。这揭示了 AI Agent 的“自我认知”缺陷——它无法有效地将自己的能力与用户的自然语言需求进行匹配，导致看似“愚笨”的行为。这不仅仅是Bug，更是影响用户体验的严重设计问题。

2.  **[#5849] [Feature]: Dream Mode — Periodic Memory Consolidation & Reflective Learning**
    - **链接**: [Issue #5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)
    - **分析**: 该功能请求虽然来自10天前，但今日讨论依然热烈。用户希望 ZeroClaw 在空闲时段能像人类一样“做梦”，通过后台进程进行记忆巩固和反思学习。这反映了用户对 **智能化、自主化 AI 助手** 的更高期待，已经从“能够执行任务”进阶到“能够自我进化”。该 Issue 标签 `priority:p1` 和 `status:no-stale`，说明维护团队已将其视为高优先级的长期任务。

## Bug 与稳定性
今日报告的 Bug 数量较多，涉及多个核心组件。按照严重程度排列如下：

- **S1 - 工作流受阻**:
    - **[#6095] [Bug]: Bedrock 400: claude-opus-4-7 模型“temperature”字段废弃** - 此问题涉及主流商业模型适配，影响面广。暂未见直接修复 PR。
    - **[#5654] [Bug]: Telegram token 加密配置后无法工作** - 导致 Telegram 渠道完全不可用。标签为 `status:in-progress`，但未见今日提交的FIX PR。
    - **[#6259] [Bug]: OpenAI兼容层导致Gemini 3的 tool_calls 失败** - 导致Gemini 3思考模型无法使用。此 Issue 今日已关闭，预计修复已随某次提交合并。

- **S2 - 功能降级**:
    - **[#6233] [Bug]: chat_messages_to_native() 对纯文本助手消息丢失 reasoning_content** - 导致 DeepSeek V4 多轮对话失败。**已有对应 FIX PR [#6284](https://github.com/zeroclaw-labs/zeroclaw/pull/6284)**，预计很快修复。
    - **[#5722] [Bug]: 默认 Shell 沙箱配置阻止常规 Python 技能模式** - 阻碍了核心“技能”生态的发展，长期未决，是社区严重关切的问题之一。标签为 `status:in-progress`，但进展缓慢。
    - **[#6269] [Bug]: 上下文压缩器丢弃 reasoning_content** - 与 #6233 类似，同样是 DeepSeek 兼容性问题。**已有对应 FIX PR [#6285](https://github.com/zeroclaw-labs/zeroclaw/pull/6285)**。
    - **[#6254] [Bug]: WASM 插件安装路径与运行时扫描路径不一致** - 导致已安装的 WASM 插件对 Agent 不可见，使 WASM 插件生态几乎不可用。暂未见直接修复 PR。

- **其他值得注意的 Bug**:
    - **[#6298] 空 tool_calls 数组导致 400 错误** - 今日新提交，影响 DeepSeek 和 NVIDIA NIM 等严格校验的提供商，严重性可能升级。
    - **[#6245] Tavily 搜索提供商仅为存根** - 流行搜索 API 功能缺失，影响用户体验。
    - **[#6227] 具名实例的`status`命令报告错误状态** - 多实例部署场景下的可用性Bug。
    - **[#6280] Windows 全量构建失败** - 影响跨平台用户。

## 功能请求与路线图信号
今日提交的 Feature Requests 清晰地指向了即将到来的 **v8.0 版本大重构**。

- **v8.0 架构准备**: 核心维护者 `singlerider` 今日提交了多个功能请求，均与 v8.0 版本新架构相关：
    - **[#6271] V3 SwarmConfig 模式实现** - 重构集群配置。
    - **[#6272] Agent 文件系统布局重构** - 更清晰的文件管理。
    - **[#6273] ModelProviderConfig 拆分** - 按提供商族拆分配置，提高可维护性。
    - 以上三个 Issue 与今日提交的大型 PR **[#6266]** 共同构成了 v8.0 配置迁移的核心。

- **技能生态深化**:
    - **[#6253] v0.7.6: 提升 Skills 支持和用户体验** - 官方将技能使用体验作为下一版本核心主题。相关大型 PR **[#6274]** 和 **[#6143]** 今日仍在活跃更新，涉及将第一方技能整合进主仓库和引入通用技能注册中心。
    - **[#6140] 混合技能插件：SKILL.md + WASM** - 将指令与编译型工具结合，代表了未来技能开发的先进方向。

**路线图信号**: 项目正经历从 v7 到 v8 的版本跨越，配置文件、集群、提供商架构将有显著变化。
**链接**: [PR #6266: schema v3 migration](https://github.com/zeroclaw-labs/zeroclaw/pull/6266)

## 用户反馈摘要
- **“太死板”**: 用户抱怨 Agent 无法理解自身能力（#5862），以及在1对1对话中不必要地判断“是否应该回复”（#5674）。这表明当前的指令遵循机制过于机械，缺乏对人类意图的智能推断能力。
- **“门槛高”**: 默认Shell沙箱配置（#5722）和 WASM 插件路径问题（#6254）提高了用户参与插件/Skill开发的成本，对生态建设不利。用户期望开箱即用。
- **“不稳定”**: DeepSeek 和 Gemini 等多款主流模型的兼容性问题（#6233, #6259, #6269）反复出现，严重影响了使用这些模型的用户群，反映出适配测试的覆盖度和回归测试有待加强。
- **“配置麻烦”**: 用户抱怨 Telegram 和 Slack 的 Token 配置问题（#5654, #6237），以及对 LM Studio 服务器地址硬编码的不满（#6260）。这些问题均表现出用户对更灵活、更易用的配置方式的强烈需求。

## 待处理积压
以下为长期未解决或进展缓慢的重大问题，需维护者重点关注：

1.  **[#5862] [Bug]: zeroclaw 不知道自己能创建 Cron 任务** - 标签 `(r:needs-repro)`，但为体验层面的核心问题，社区讨论度高，已开放半月，亟待解决。
2.  **[#5849] [Feature]: Dream Mode** - `priority:p1` 功能，代表着社区对 AI 智能化的期望，已开放超两周，目前仍无实施 PR。
3.  **[#5722] [Bug]: Shell 沙箱配置问题** - 严重阻碍技能生态发展，已开放三周，标签 `status:in-progress` 但未见明显进展。
4.  **[#5674] [Feature]: 使回复意图分类可配置** - `priority:p2` 但获得 3 个高赞，反映了广泛存在的体验问题，已开放超三周。
5.  **[#5628] [Bug]: 守护进程自启动导致端口冲突** - 基础服务稳定性问题，已开放三周，影响日常使用。

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*