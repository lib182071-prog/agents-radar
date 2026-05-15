# OpenClaw 生态日报 2026-05-15

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-15 10:00 UTC

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

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已基于您提供的 OpenClaw 项目数据，为您生成今日（2026-05-15）的项目动态日报。

---

### OpenClaw 项目动态日报 (2026-05-15)

---

#### 1. 今日速览

今日项目活跃度极高，共处理 500 条 Issue 和 500 条 PR，但存在明显的“待办积压”现象：**待合并的 PR 占比高达 93%**，而合并/关闭的 PR 仅 34 条。这表明社区贡献意愿强烈，但代码审查与合并流程可能存在瓶颈。核心团队今日发布了 3 个新版本（包含修复与优化），并重点推进了 **Codex 运行时** 的兼容性与 **插件审批机制** 的用户体验优化。一个值得关注的高风险 Bug 是 **WebSocket 链接失败** 的回归问题，已导致部分 MacOS 用户升级后无法连接。

- **活跃度评估**: 🟢 **非常活跃**
- **健康度信号**: 🟡 **高产出，但审查/合并流程存在阻塞风险**

---

#### 2. 版本发布

今日发布了 **3 个新版本**，均为小版本更新与 Beta 版：

- **v2026.5.14-beta.1** (`latest`)
  - **主要变更**:
    - **依赖精简**: 将根级 Node 代理相关的依赖移至 `@openclaw/proxyline` 包中，减少核心包的依赖体积。
    - **i18n 改进**: 新增 `pnpm ui:i18n:report` 命令，用于生成硬编码文本和地区回退元数据的基线报告，方便开发者识别和修正 UI 国际化问题。
  - **迁移注意事项**: 对于手动配置了代理的用户，需检查配置是否与新的 `@openclaw/proxyline` 包兼容，避免代理服务中断。

- **v2026.5.12** (`stable`)
  - **主要变更**:
    - **依赖瘦身**: 将 WhatsApp、Slack、Amazon Bedrock 等供应商及插件的依赖链移出核心运行时，实现“按需安装”，显著减少安装体积。
    - **Telegram 健壮性提升**: 引入了隔离轮询、持久化本地假脱机（spooling）机制，并优化了群组媒体处理逻辑。
    - **破坏性变更**: 非核心供应商依赖被移除，若用户使用任何被外移的供应商（WhatsApp, Slack 等），**必须**显式安装对应插件后才能正常运行，否则相关功能将失效。
    - **迁移注意事项**: 强烈建议用户在升级后，运行 `openclaw doctor` 检查配置完整性，并根据提示安装所需的供应商/插件包。请参考 [官方迁移指南](https://docs.openclaw.ai/)。

- **v2026.5.12-beta.8** (早期内部测试版)
  - 类似于 v2026.5.12 的早期迭代，重点在 Amazon Bedrock、Slack、OpenShell sandbox 等供应商的外部化。

---

#### 3. 项目进展 (今日合并/关闭的关键 PR)

尽管合并率较低，但以下已合并/关闭的 PR 体现了项目的核心进展：

- **用户体验优化**: [**PR #81864**](https://github.com/openclaw/openclaw/pull/81864) 被合并，该 PR 完全重写了插件审批提示文案，将之前令人困惑的“调试输出”风格改为用户易于理解的“自然语言”描述。这是对社区长期反馈的积极响应，显著降低了用户的使用门槛。

- **Codex 兼容性修复**: [**Issue #81941**](https://github.com/openclaw/openclaw/issues/81941) 和 [**Issue #46080**](https://github.com/openclaw/openclaw/issues/46080) 被关闭，分别修复了 Codex 认证失败和 Anthropic 工具调用后返回空内容的问题。这标志着团队正在积极解决向 **Codex 运行时** 迁移过程中遇到的兼容性问题，是项目架构演进的关键一步。

- **功能推进**: [**PR #82063**](https://github.com/openclaw/openclaw/pull/82063) (新增网关方法描述注册表) 和 [**PR #82095**](https://github.com/openclaw/openclaw/pull/82095) (修复 Discord 语音转码) 的合并，表明网关协议的标准化和多渠道功能完善仍在稳步推进。

---

#### 4. 社区热点

今日最受关注的话题集中在 **运行时切换（Codex vs. Pi）** 和 **核心配置管理** 上：

1.  **[Issue #80171 - Codex-vs-Pi 运行时质量保证（QA）](https://github.com/openclaw/openclaw/issues/80171)**
    - **状态**: 打开中 | **评论**: 13 | **作者**: 100yenadmin
    - **话题焦点**: 该 Issue 作为一个 RFC 和追踪议题，系统性地讨论了将 Codex 设为 OpenAI agent 默认运行时的计划。评论区引发了关于两种运行时（Pi vs. Codex）优劣、迁移风险和兼容性测试的深度技术讨论。这直接关系到项目的未来架构走向，因此吸引了核心开发者 `@pash` 等人的参与。

2.  **[Issue #53628 - `$XDG_CONFIG_HOME` 环境变量未正确处理](https://github.com/openclaw/openclaw/issues/53628)**
    - **状态**: 打开中 | **评论**: 12 | **作者**: Devattom
    - **话题焦点**: 这是一个环境变量处理 Bug，但讨论热度高可能是因为它触及了 Docker 部署和跨平台兼容性的一个普遍痛点。用户发现通过 `.env` 文件设置 `XDG_CONFIG_HOME` 后，`clawhub` 命令在安装技能时无法正确解析该变量，导致配置安装到错误路径。

3. **[Issue #50096 - 长期记忆与知识管理（长期议题）](https://github.com/openclaw/openclaw/issues/50096)**
    - **状态**: 已关闭 | **评论**: 12 | **作者**: ocdlmv1
    - **话题焦点**: 虽然已关闭，但今日仍有 12 条评论，这表明“长期记忆”能力是用户最核心的诉求之一。该 Issue 详细描述了当前 Driftnet 记忆系统的问题，并提出了改进建议。它的高热度反映了用户对“智能体持续学习”的强烈期待。

---

#### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **严重 / 阻塞级**:
  - **[Issue #82037 - MacOS 26.5 更新后 WebSocket 连接失败](https://github.com/openclaw/openclaw/issues/82037)**
    - **描述**: 升级到 v2026.5.12 后，MacOS 用户报告 Web 和 App 端 WebSocket 链接失败，日志显示“wrong protocol”错误。这是影响所有前端用户的关键回归。
    - **状态**: **已有 Fix PR？** 暂未发现直接修复的 PR，但此问题优先级应为最高。

  - **[Issue #50630 - Tailscale 暴露内网网关未鉴权](https://github.com/openclaw/openclaw/issues/50630)**
    - **描述**: 当使用 `auth.mode=none` 且通过 Tailscale 暴露服务时，整个 Tailnet 内的设备均可未经授权访问网关，CVSS 评分高达 9.3。
    - **状态**: 暂时无对应 fix PR。

- **高 / 回归问题**:
  - **[Issue #81941 - Codex OAuth 认证失败](https://github.com/openclaw/openclaw/issues/81941)**
    - **描述**: 新登录的 Codex OAuth 配置文件认证失败，报 `token_expired` 错误。
    - **状态**: ✅ **已关闭**。已在最新版本中修复。

  - **[Issue #51429 - 工作路径被硬编码为 `wangtao` 用户路径](https://github.com/openclaw/openclaw/issues/51429)**
    - **描述**: 代码中出现了名为 `wangtao` 开发者的个人工作路径 `~/Users/wangtao` 的硬编码，导致新用户工作区被错误设置。
    - **状态**: **严重代码质量问题**，待修复。

- **中 / 行为 Bug**:
  - **[Issue #54253 - RISC-V64 系统 LLM 请求失败](https://github.com/openclaw/openclaw/issues/54253)**
    - **描述**: 在 RISC-V64 平台上安装成功，但 API 调用时一直报 `LLM Request Failed`。
    - **状态**: 待排查架构兼容性问题。

  - **[Issue #48573 - Zombie Agents 状态泄漏](https://github.com/openclaw/openclaw/issues/48573)**
    - **描述**: `embedded-run` 生成的子 agent 在父 agent 终止后，其会话状态仍残留在存储中，导致后续运行混淆。
    - **状态**: 待修复。

---

#### 6. 功能请求与路线图信号

- **高优先级/可能纳入下一版**:
  - **[Issue #45550 - Anthropic 1M 上下文迁移](https://github.com/openclaw/openclaw/issues/45550)**: 跟随 Anthropic API 变化，获得 1M 超长上下文支持，对处理大型代码库或文档的用户至关重要。
  - **[Issue #45608 - 预重置 Agentic Memory Flush](https://github.com/openclaw/openclaw/issues/45608)**: 在 `/new` 或 `/reset` 时执行记忆刷新，避免用户主动重置时丢失有价值的工作记忆。该请求直接提升用户体验，被合并的可能性高。
  - **[Issue #52640 - 长任务持久化状态面板](https://github.com/openclaw/openclaw/issues/52640)**: 为耗时长的渠道任务（如 Discord）提供持久化状态展示，用户不再需要猜测后台是否还在运行。

- **低优先级/观察中**:
  - **[Issue #45758 - 支持 YAML 配置文件](https://github.com/openclaw/openclaw/issues/45758)**: 获得较多 👍 和讨论，但并非核心功能阻塞点，可能会在未来版本中作为可选特性加入。
  - **[Issue #45565 - 网关生命周期警告路由到专用频道](https://github.com/openclaw/openclaw/issues/45565)**: 系统警告消息不应干扰主聊天频道，这是一个非常好的运维优化建议，可能在未来引入配置项。

---

#### 7. 用户反馈摘要

- **痛点**:
  - **配置陷阱**: 大量用户（如 #51429, #45765 等）反映配置路径、环境变量处理存在硬编码或逻辑 Bug，严重影响了首次使用体验。这表明代码审查流程在配置处理相关的改动上需要加强。
  - **运行时切换阵痛**: 向 Codex 运行时迁移导致了兼容性问题（#81941）和用户困惑（#80171），社区需要更清晰的迁移指南。
  - **性能焦虑**: 用户反馈 `sessions.json` 无限增长（#55334）和内存泄漏（#45698），表明会话管理的长期稳定性仍待优化。

- **满意点**:
  - **功能深度受认可**: 用户对 `gh-issues` 技能（#45740）、`browser tool`（#44431）等高级工具的功能深度表示肯定，认为其功能强大，但在安全性和易用性上有所不足。
  - **社区响应快**: 虽然有积压，但核心团队对高优先级 Bug（如 Codex 认证失败）的响应和修复速度还是得到了用户的注意。

---

#### 8. 待处理积压

以下为长期未更新或今日评论量激增，但尚无对应 fix PR 的高风险 Issue，建议维护团队重点关注：

1.  **[Issue #54463 - QMD 内存索引的 Symlink 循环问题](https://github.com/openclaw/openclaw/issues/54463)**
    - **更新于**: 2026-05-15 | **评论**: 6
    - **概要**: QMD 记忆索引在处理包含符号链接循环的临时 monorepo 时，会抛出 `ENAMETOOLONG` 错误。这影响在复杂项目中运行的 agent 的稳定性。

2.  **[Issue #53399 - 浏览器控制服务器挂起](https://github.com/openclaw/openclaw/issues/53399)**
    - **更新于**: 2026-05-15 | **评论**: 6
    - **概要**: npx `chrome-devtools-mcp` 启动后，有时会卡在 Gateway 进程内，导致浏览器控制不可用。该 Issue 创建于 3 月，至今未解决，严重影响了重度 Browser Tool 使用者。

3.  **[Issue #51871 - Control UI 中 Cron 作业不显示](https://github.com/openclaw/openclaw/issues/51871)**
    - **更新于**: 2026-05-15 | **评论**: 10
    - **概要**: 2026.3.13 版本后，Dashboard 无法显示已配置的 Cron 作业，用户只能通过命令行查看。这是一个影响广泛的 Dashboard 功能回归。

4.  **[PR #70864 - 新增限定提及模式策略](https://github.com/openclaw/openclaw/pull/70864)**
    - **更新于**: 2026-05-15 | **评论**: 0
    - **概要**: 这是一个旨在解决群聊中“@所有人”或模式化提及造成干扰的纯新功能 PR，涵盖几乎所有渠道。功能本身非常实用，但该 PR 自 4 月 24 日打开至今已近一个月，仍无任何评论或合并，处于严重停滞状态。

---

## 横向生态对比

# AI 智能体/个人 AI 助手开源生态横向对比分析报告（2026-05-15）

---

## 1. 生态全景

当前个人 AI 助手开源生态呈现**高速迭代、社区高度活跃**的态势。核心参照项目 OpenClaw 日处理超 500 个 Issue/PR，但合并率仅 7%，反映出社区贡献意愿强而审查瓶颈突出。多个衍生项目（NanoBot、Hermes、PicoClaw、IronClaw、CoPaw、ZeroClaw 等）同步密集推进功能开发和 Bug 修复，普遍围绕**运行时兼容性、多平台 IM 集成、安全加固、长期记忆与 Cron 可靠性**等方向展开。生态整体处于**功能扩张与稳定性巩固并存的阶段**，模型兼容性（尤其国产模型 `reasoning_content` 字段）成为跨项目共性痛点，安全与运维需求随用户规模增长迅速浮现。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|------|-------------|-----------|----------|-------------|
| **OpenClaw** | 500（新开+活跃） | 500（待合并 466，合并/关闭 34） | 3 个（stable/beta） | 🟡 产需旺盛但合并阻塞严重 |
| **NanoBot** | 51（关闭） | 23（合并/关闭 13，待合并 10） | 无 | 🟢 高效维护，响应快 |
| **Hermes Agent** | 50（新开+活跃 16，关闭 34） | 50（待合并 27，合并/关闭 23） | 无 | 🟢 稳步推进，修复密集 |
| **PicoClaw** | >40 | >40（合并多条） | v0.2.8-nightly | 🟢 快速迭代，多线并进 |
| **NanoClaw** | 新开约 5 | 25（合并/关闭 13） | 无 | 🟡 PR 活跃，但关键 Bug 未修 |
| **IronClaw** | ~100（含更新） | ~100 | v0.28.2（补丁） | 🟢 架构重构关键期，发布及时 |
| **LobsterAI** | 40（含新开） | 50（合并 33） | v2026.5.14 | 🟡 高合并量但模型绑定投诉 |
| **CoPaw** | 40 | 50（合并/关闭 33） | 无 | 🟢 高产出，安全加固显著 |
| **ZeroClaw** | 31 | 50（待合并 35，合并/关闭 15） | 无 | 🟡 需求旺盛但 S1 Bug 待解 |
| **Moltis** | 1（新 Bug） | 0 | 无 | 🔴 低活跃，关键 TLS Bug 未响应 |
| **NullClaw / TinyClaw / ZeptoClaw** | 0 | 0 | 无 | ⚫ 停滞 |

---

## 3. OpenClaw 在生态中的定位

**优势：**
- **社区规模最大**：日处理 500+ Issue/PR，远超其他项目（通常 50-100）。
- **功能最全面**：双运行时（Pi / Codex）切换、丰富的插件市场、i18n、长期记忆（Driftnet）等，是生态功能标杆。
- **版本迭代最频繁**：同日发布 3 个版本（含稳定版），快速响应社区。

**技术路线差异：**
- **双运行时架构**是 OpenClaw 独特优势，但正面临向 Codex 迁移的阵痛（如 OAuth 认证失败，#81941）。
- **插件审批机制**（自然语言提示重写）体现对人机交互体验的重视。
- 相较之下，NanoBot、Hermes 等更依赖单一运行时，但轻量且简化配置；IronClaw 自行开发 Reborn 架构，强调安全与可观测性。

**隐患：**
- **合并流程瓶颈**：93% PR 待合并，远超其他项目（如 NanoBot 待合并占比 43%，Hermes 54%），长期可能抑制贡献者热情。
- **稳定性回归**：MacOS WebSocket 连接失败（#82037）等 P0 Bug 未及时修复，影响核心用户信任。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/表现 |
|----------|----------|---------------|
| **模型兼容性（尤其是 `reasoning_content` 字段）** | OpenClaw (#81941)、PicoClaw (#2859, #2706)、IronClaw (#3673)、CoPaw (#4314)、ZeroClaw (#6672) | 国产模型（DeepSeek、MiMo）的思考内容未正确回传，导致多轮工具调用失败或 400 错误。 |
| **多平台 IM 集成（飞书/Telegram/钉钉）** | NanoBot (#3772, #3786)、Hermes (#16084, #26174)、PicoClaw (#2798)、CoPaw (#3957, #3109)、ZeroClaw (#6646, #6229) | 飞书卡片渲染、Telegram 语音转录、钉钉 @ 事件处理、频道路由等存在功能缺陷或配置未生效。 |
| **安全加固（插件审批/权限/SHELL 注入）** | OpenClaw (#50630 网关未鉴权)、NanoBot (#3842 本地附件访问)、Hermes (#26003 chmod)、PicoClaw (#2877 Tirith)、IronClaw (#3638 默认拒绝)、CoPaw (#4409 备份签名, #4421 配置明文)、ZeroClaw (#5952 技能审计) | 安全意识提升，涵盖网关鉴权、路径遍历、配置文件泄露、Shell 命令预扫描等。 |
| **长期记忆与会话上下文管理** | OpenClaw (#50096)、NanoBot (#3689)、PicoClaw (#2795, #2787)、ZeroClaw (#6105 Cron 上下文) | Agent 持续学习、会话历史完整、中断恢复能力是用户核心诉求，但多数项目尚未完善。 |
| **Cron 任务可靠性** | OpenClaw (#51871 不显示)、Hermes (#26125 MCP 重连)、NanoClaw (#2481 输出抑制)、ZeroClaw (#6647 路由失败) | Cron 任务的执行结果可见性、输出路由、上下文连贯性是多项目的薄弱环节。 |
| **可观测性/运维** | ZeroClaw (#6641 OTel, #6642 Prometheus)、CoPaw (#4114 链路追踪) | 随用户规模扩大，对分布式追踪、指标暴露的需求开始涌现。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|-----------------|
| **OpenClaw** | 全能型 AI 助手，插件市场、双运行时、长期记忆 | 开发者/高级用户 | Pi/Codex 双运行时，高度模块化，配置复杂 |
| **NanoBot** | 轻量高效，侧重中文 IM（飞书/微信） | 企业内团队协作 | 单运行时，配置简单（JSON/TOML 辩论），社区响应快 |
| **Hermes Agent** | 企业级集成，Dashboard/MCP/Cron/ACL | 运维/企业 IT | 强调安全审计、配置即代码、macOS launchd 支持 |
| **PicoClaw** | 嵌入式/边缘设备，轻量化 | 物联网/边缘计算 | 最小化依赖，C 语言核心（？），提供商适配层较薄 |
| **NanoClaw** | 社区运营（LinkedIn/Reddit/社交媒体） | 营销/社区经理 | 复合式社交监听、网站审计自托管，强 CIS 功能 |
| **IronClaw** | 底层框架，架构重构（Reborn） | 高级开发/架构师 | Rust 实现，强调安全默认、可观测性、事件驱动 |
| **LobsterAI** | 协同编辑/插件管理，网易背景 | 中文用户/团队协作 | 内置网易服务，但存在模型强制绑定争议 |
| **CoPaw** | 钉钉/企业微信深度集成，Agent 身份管理 | 企业/中文办公 | 计划模式门控、Agent 工作空间分离，身份混淆修复 |
| **ZeroClaw** | 高功能密度，技能系统完善 | 进阶开发者 | 技能审计（仅结构）、Cron 上下文缺失、严格工具解析 |

---

## 6. 社区热度与成熟度分层

**快速迭代阶段（功能扩张为主）：**
- **OpenClaw**、**NanoBot**、**Hermes**、**PicoClaw**、**IronClaw**、**CoPaw**、**ZeroClaw**：大量新功能 PR 和 Issue 涌入，版本发布频繁，社区讨论活跃。但各项目均存在待解决的高优 Bug（如 OpenClaw 的 WebSocket、ZeroClaw 的 Cron 路由），稳定性尚未达到“生产可用”标准。

**质量巩固阶段（Bug 清理与性能优化为主）：**
- **LobsterAI**：集中合并 33 个积压 PR，涵盖安全修复、性能优化，但模型绑定问题引发信任危机。
- **NanoClaw**：Docker 部署问题（#2480）为阻塞性 Bug，其余 PR 多为功能平移，处于质量巩固与功能扩展的过渡期。

**低活跃/停滞项目：**
- **Moltis**：仅 1 个 TLS Bug 未修复，无 PR/版本，可能为个人项目或维护者精力有限。
- **NullClaw、TinyClaw、ZeptoClaw**：连续无活动，项目可能已废弃或处于休眠。

**社区成熟度信号：**
- **LobsterAI** 用户公开质疑强制服务绑定（#1988），反映社区对“开源可控”底线的严格要求。
- **ZeroClaw** 用户报告配置未按预期工作（#6229 `mention_only`），暴露文档与实现偏差。

---

## 7. 值得关注的趋势信号

1. **国产模型兼容性成为生态入口必备能力**：OpenClaw、PicoClaw、IronClaw、CoPaw、ZeroClaw 均在修复 `reasoning_content` 字段错误。开发者若依赖国产模型（DeepSeek、MiMo、GLM），需特别关注项目对该字段的处理逻辑。

2. **多 IM 渠道不再是“锦上添花”而是核心竞争力**：飞书、Telegram、钉钉的 Bug 数量和用户投诉频率高居不下。企业用户对“开箱即用”的渠道集成要求极高，项目需从“支持”转向“深度适配”（如飞书流式卡片、Telegram 语音转录）。

3. **安全左移趋势明显**：从插件审批（OpenClaw）到 Shell 预扫描（PicoClaw）、备份签名（CoPaw）、默认拒绝策略（IronClaw），安全正从“事后修复”变为“架构成分”。建议开发者在新项目中默认启用最小权限原则。

4. **Cron 任务可见性成关键体验缺口**：多个项目报告 Cron 输出“静默失败”或无法路由到正确频道。用户期望 Cron 结果能通过 Agent 本身主动通知，而非依赖手动检查面板。实现“Cron 结果的智能推送”可能是下一个差异化方向。

5. **可观测性开始从“开发者偏好”变为“运维刚需”**：ZeroClaw 明确提出 OpenTelemetry 集成，CoPaw 用户询问链路追踪。随着 Agent 在部署中承担更关键任务，运维团队需要类似传统微服务的监控能力。

6. **“配置即代码”呼声渐起**：NanoBot 社区讨论转向 TOML 格式（#3402），ZeroClaw 有 YAML 配置请求（#45758），CoPaw 用户希望工作目录整洁化（#4408）。声明式、版本可控的配置管理将提升项目的企业可采纳性。

7. **社区对“开源本质”敏感度提高**：LobsterAI 的“强制模型绑定”事件是对社区信任的警示。任何试图在开源软件中隐含服务商绑定的行为都可能引发用户反弹。开源项目应坚守用户配置优先、本地可控的原则。

---

*报告基于 2026-05-15 各项目 GitHub 公开数据自动生成，仅供参考。数据采集截止时间 UTC 23:59。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目的分析师，根据您提供的NanoBot GitHub数据，我为您生成了2026年5月15日的项目动态日报。

---

### **NanoBot 项目动态日报 | 2026-05-15**

#### **1. 今日速览**

今日项目活跃度极高，社区贡献与维护者响应均处于繁忙状态。**关键指标显示项目进入高强度迭代期**：过去24小时内关闭了51个Issue，合并/关闭了13个PR，体现出高效的维护节奏。同时，新开了10个待合并PR，表明项目正在积极接纳新功能。特别值得注意的是，一位核心贡献者（`xianqiangfu`）集中提交了超20个关于**文档、教程、代码注释和架构图**的Issue，并在短时间内全部关闭，这标志着项目在**提升可维护性和开发者体验**方面迈出了坚实的一大步。

#### **2. 版本发布**

无新版本发布。

#### **3. 项目进展**

今日项目在**稳定性、跨平台兼容性和安全加固**方面取得了显著进展，核心功能模块得到强化。关键合并/关闭的PR如下：

- **【安全加固】**
    - **本地附件访问限制**：PR [#3842](https://github.com/HKUDS/nanobot/pull/3842) 修复了在启用工作区限制时，`message` 工具可能被LLM利用来访问本地文件的安全漏洞。
    - **飞书媒体文件路径安全**：PR [#3789](https://github.com/HKUDS/nanobot/pull/3789) 修复了飞书通道在下载媒体文件时的路径遍历风险，确保文件名被安全处理。

- **【飞书 & 其他通道兼容性】**
    - **飞书群聊被@错误修复**：PR [#3775](https://github.com/HKUDS/nanobot/pull/3775) 为飞书WebSocket模式中未被处理的事件类型（如机器人被其他机器人在群组中添加/移除）添加了空操作处理器，消除了“processor not found”的报错，直接解决了社区热点Issue [#3772](https://github.com/HKUDS/nanobot/issues/3772) 和 [#3787](https://github.com/HKUDS/nanobot/issues/3787)。
    - **Telegram语音转录修复**：PR [#3786](https://github.com/HKUDS/nanobot/pull/3786) 修复了Telegram通道中语音转录配置不生效的问题，现在用户可以自定义转录服务。
    - **WhatsApp语音消息残留修复**：PR [#3752](https://github.com/HKUDS/nanobot/pull/3752) 修复了WhatsApp语音转录成功后，`.ogg`文件路径仍被发送给LLM的问题。

- **【核心功能与体验】**
    - **快捷指令持久化**：PR [#3779](https://github.com/HKUDS/nanobot/pull/3779) 修复了使用如 `/help` 等快捷指令后，聊天记录不保存的Bug，改善了WebUI的用户体验。
    - **DM发送者批准流程**：PR [#3774](https://github.com/HKUDS/nanobot/pull/3774) 为私有助理部署场景增加了聊天原生配对流程，允许管理员在对话中批准DM发送者。
    - **Windows UNC路径支持**：PR [#3764](https://github.com/HKUDS/nanobot/pull/3764) 增强了Shell工具在Windows环境下对UNC路径的支持。
    - **CLIENT Proxy SSL支持**：PR [#3783](https://github.com/HKUDS/nanobot/pull/3783) 为`web`工具增加了`ssl_verify`配置，解决了企业代理SSL拦截导致的问题。

- **【性能优化】**
    - **推理控制修复**：PR [#3734](https://github.com/HKUDS/nanobot/pull/3734) 修复了小米MiMo API中 `reasoning_effort` 配置不生效的问题。

#### **4. 社区热点**

- **配置格式迁移讨论**：[Issue #3402](https://github.com/HKUDS/nanobot/issues/3402) (已关闭) 关于将JSON配置文件替换为TOML的讨论引发了最多评论（9条）。尽管该Issue最终被关闭，但反映了社区对**更好的人类可编辑配置文件**的强烈诉求，是项目未来演进的一个重要信号。

- **飞书群聊兼容性Bug**：[Issue #3772](https://github.com/HKUDS/nanobot/issues/3772) 和 [Issue #3787](https://github.com/HKUDS/nanobot/issues/3787) 汇报了飞书机器人在群聊中“被其他机器人@”时会报错。该Bug迅速被识别为事件处理器缺失，并在PR [#3775](https://github.com/HKUDS/nanobot/pull/3775) 中得到修复。这展现了社区洞察敏锐，且项目响应速度极快。

- **会话上下文丢失**：[Issue #3689](https://github.com/HKUDS/nanobot/issues/3689) (已关闭) 用户反馈在中断处于循环中的Agent任务时，会丢失上下文。该问题获得了5条评论并已关闭，体现了社区对Agent**会话连续性与鲁棒性**的高要求。

#### **5. Bug 与稳定性**

| 严重程度 | Issue / PR | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#3790](https://github.com/HKUDS/nanobot/issues/3790) | **[新报]** WebUI会话内容打印显示错乱，刷新页面才能恢复。最新版本（0.1.5.post3.2026.05.13）引入的回归问题。 | **Open** |
| **重要** | [#3689](https://github.com/HKUDS/nanobot/issues/3689) | Agent陷入循环时，用户中断会丢失会话上下文。 | **Closed** |
| **重要** | [#3772](https://github.com/HKUDS/nanobot/issues/3772) | 飞书群聊中，被其他机器人@时导致Agent出错。 | **已修复** (PR [#3775](https://github.com/HKUDS/nanobot/pull/3775)) |
| **中等** | [#3783](https://github.com/HKUDS/nanobot/pull/3783) | 企业代理SSL MITM拦截导致网页工具操作失败。 | **已修复** |
| **中等** | [#3786](https://github.com/HKUDS/nanobot/pull/3786) | Telegram通道语音转录配置不生效的Bug及修复。 | **已修复** |
| **中等** | [#3752](https://github.com/HKUDS/nanobot/pull/3752) | WhatsApp语音消息转录后，文件路径残留在回复中。 | **已修复** |

#### **6. 功能请求与路线图信号**

- **任务分解与规划能力 (High Signal)**: PR [#3791](https://github.com/HKUDS/nanobot/pull/3791) 新增`plan`工具，允许Agent在执行前将复杂任务分解为多步骤，并支持进度追踪。此功能与PR [#3460](https://github.com/HKUDS/nanobot/pull/3460) (长任务工具) 和 [#3788](https://github.com/HKUDS/nanobot/pull/3788) (目标状态流式传输) 共同指向了项目**强化Agent的自主规划和执行能力**的明确方向，可能是下一个版本的核心特性。

- **新LLM提供商支持**：PR [#3785](https://github.com/HKUDS/nanobot/pull/3785) 拟增加对OpenCode Go网关的支持，以整合多种国产模型（如GLM、Kimi、DeepSeek等），反映出社区对**扩大模型生态**的持续需求。

#### **7. 用户反馈摘要**

- **痛点**：
    - **会话中断体验不佳**：用户 `lyh161` 抱怨打断Agent循环后，它“忘记”了之前的任务和进度，期望Agent能记住对话历史并从中断处恢复。（[#3689](https://github.com/HKUDS/nanobot/issues/3689)）
    - **WebUI回归问题**：用户 `kxsk-git` 在更新到最新版本后，立即遇到了打印内容错乱的问题，需要手动刷新页面，这严重影响了使用体验。（[#3790](https://github.com/HKUDS/nanobot/issues/3790)）
- **使用场景**：用户 `bigsinger` 将NanoBot部署在飞书群聊中，证明了其在**团队协作场景**下的应用价值，同时也暴露出对其他机器人交互的兼容性不足。（[#3772](https://github.com/HKUDS/nanobot/issues/3772)）

#### **8. 待处理积压**

- **长期待合并PR - 长任务系统**：PR [#3460](https://github.com/HKUDS/nanobot/pull/3460) (`feat(long-task): add LongTaskTool`) 自4月26日开启，至今仍在Open状态。考虑到今日合并了多个相关PR（如#3774，#3779）并提交了新的`plan`工具（#3791），这个PR的后续整合策略可能需要维护者关注和决策。
- **网关生命周期通知PR**：PR [#3792](https://github.com/HKUDS/nanobot/pull/3792) (`feat: add gateway lifecycle notification hooks in feishu`) 已提交但尚未合并，该功能请求在社区中（#3279）有一定呼声，需要关注其审核进展。
- **Brave搜索速率限制**：PR [#3840](https://github.com/HKUDS/nanobot/pull/3840) (`fix(web): back off Brave search rate limits`) 针对Brave搜索速率限制提出了修复方案，这是一个常见的实际问题，建议维护者优先审查与合并。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

## Hermes Agent 项目动态日报 — 2026-05-15

### 1. 今日速览
过去24小时项目活跃度较高，共处理 **50 条 Issue**（新开/活跃 16 条，关闭 34 条）和 **50 个 PR**（待合并 27 个，已合并/关闭 23 个）。虽然无新版本发布，但合并了大量关键 Bug 修复（特别是视觉相关、CLI/Dashboard 体验、MCP/Cron 稳定性）和部分功能增强。社区讨论集中于飞书平台体验优化、输出截断、视觉模型兼容性等痛点，核心维护者响应迅速（@zccyman 贡献了多个修复 PR）。

### 2. 版本发布
无

### 3. 项目进展 — 今日合并/关闭的重要 PR
| PR | 简要描述 | 状态 |
|----|---------|------|
| [#26253](https://github.com/NousResearch/hermes-agent/pull/26253) | 修复 macOS launchd 重启时清理超时导致的网关停止 | 已合并 |
| [#17652](https://github.com/NousResearch/hermes-agent/pull/17652) | ACP（Agent Control Protocol）会话加载时重放历史消息 | 已合并 |
| [#26266](https://github.com/NousResearch/hermes-agent/pull/26266) | 修复 cron 存储时非 ASCII 字符（如中文）被转义为 `\uXXXX` | 已合并 |
| [#26164](https://github.com/NousResearch/hermes-agent/pull/26164) | 修复 terminal 工具中 `~` 和 `$VAR` 在工作目录中未展开 | 已合并 |
| [#26125](https://github.com/NousResearch/hermes-agent/pull/26125) | 修复 cron 作业调用 MCP 工具时的连接失效问题，实现惰性重连 | 已合并 |
| [#25949](https://github.com/NousResearch/hermes-agent/pull/25949) | 支持通过 `config.yaml` 自定义 API 请求 HTTP 头（如 `User-Agent`），帮助绕过 Cloudflare WAF | 已合并 |
| [#25316](https://github.com/NousResearch/hermes-agent/pull/25316) | 修复 OpenRouter 辅助模型 fallback 时丢失 `:free` 后缀的问题 | 已合并 |
| [#26003](https://github.com/NousResearch/hermes-agent/pull/26003) | 安全修复：`os.chmod` 调用防止意外修改根目录权限 | 已合并 |
| [#26002](https://github.com/NousResearch/hermes-agent/pull/26002) | 修复辅助视觉 fallback 时对 5xx 服务器错误的检测缺失 | 已合并 |
| [#26001](https://github.com/NousResearch/hermes-agent/pull/26001) | 限制图片最大像素为 8000px，防止 Anthropic API 返回 400 错误 | 已合并 |
| [#25948](https://github.com/NousResearch/hermes-agent/pull/25948) | 修复 CLI 中 `/clear`、`/reset` 后欢迎横幅显示乱码 OSC-8 超链接 | 已合并 |

此外还有多个待合并功能 PR（如账户限额状态栏 [#16652](https://github.com/NousResearch/hermes-agent/pull/16652)、会话平台过滤器 [#20242](https://github.com/NousResearch/hermes-agent/pull/20242)），项目推进节奏稳健。

### 4. 社区热点
- **[#7237](https://github.com/NousResearch/hermes-agent/issues/7237)** — **最热 Issue（28 评论，4 👍）**：`Error: Response truncated due to output length limit`。当 Hermes 在 CLI 或 IM 网关生成超长回答时，输出被截断且无法恢复，影响所有长文场景。用户期望支持流式续写或自动分段。该 Issue 已关闭，但未关联具体修复 PR，可能已内部解决或文档说明。
- **[#16084](https://github.com/NousResearch/hermes-agent/issues/16084)**（6 评论）— 飞书平台流式输出改用卡片渲染，避免“已编辑”标记和速率限制。用户 @xiangyizengdev 详细分析了当前方案缺陷，并建议使用飞书 CardKit 流式卡片。该 Issue 仍开放，热度较高。
- **[#25594](https://github.com/NousResearch/hermes-agent/issues/25594)**（5 评论）— 自定义提供商使用视觉工具时，非视觉模型被错误发送 image_url 导致 HTTP 400。该问题影响了大量使用自有 API 的企业用户，已有 PR [#23750](https://github.com/NousResearch/hermes-agent/pull/23750) 待合并修复。

### 5. Bug 与稳定性
| 严重程度 | Issue/PR | 描述 | 修复状态 |
|---------|---------|------|---------|
| **P1** | [#26003](https://github.com/NousResearch/hermes-agent/pull/26003) | `os.chmod("/", 0o700)` 破坏系统服务 | 已合并 |
| **P2** | [#25594](https://github.com/NousResearch/hermes-agent/issues/25594) | 自定义提供商的视觉工具发送 image_url 给非视觉模型 | 有 PR [#23750](https://github.com/NousResearch/hermes-agent/pull/23750) 待合并 |
| **P2** | [#26174](https://github.com/NousResearch/hermes-agent/issues/26174) | 飞书平台 Markdown 渲染失败 | 已关闭，可能与 [#16084](https://github.com/NousResearch/hermes-agent/issues/16084) 重复 |
| **P2** | [#26042](https://github.com/NousResearch/hermes-agent/issues/26042) 通过 [#26125](https://github.com/NousResearch/hermes-agent/pull/26125) | cron 调用 MCP 工具时连接失效 | 已合并 |
| **P2** | [#26264](https://github.com/NousResearch/hermes-agent/issues/26264) | Dashboard 在特定网络绑定下“Resume in Chat”显示 session ended | 开放，已有 PR [#26265](https://github.com/NousResearch/hermes-agent/pull/26265) |
| **P2** | [#26210](https://github.com/NousResearch/hermes-agent/issues/26210) | `delegate_task` 在 DeepSeek 供应商下返回 404 | 开放，待排查 |
| **P2** | [#26198](https://github.com/NousResearch/hermes-agent/issues/26198) | macOS launchd 重启网关可能进入停止状态 | 已合并修复 PR [#26253](https://github.com/NousResearch/hermes-agent/pull/26253) |
| **P3** | [#2747](https://github.com/NousResearch/hermes-agent/issues/2747) | 本地模型自动检测异常被静默吞掉 | 已关闭，可能已修复 |
| **P3** | [#2744](https://github.com/NousResearch/hermes-agent/issues/2744) | `asyncio.gather` 未使用 `return_exceptions=True` 导致结果丢失 | 已关闭 |

### 6. 功能请求与路线图信号
- **飞书平台深度优化**：多个 Issue（[#16084](https://github.com/NousResearch/hermes-agent/issues/16084)、[#26236](https://github.com/NousResearch/hermes-agent/issues/26236)、[#26239](https://github.com/NousResearch/hermes-agent/issues/26239)）要求飞书采用流式卡片、平台感知格式化。社区对飞书体验诉求强烈，相关 PR 或可进入下一版本。
- **非阻塞委托任务**：[#1599](https://github.com/NousResearch/hermes-agent/issues/1599) 提出的 `background=true` 模式已被关闭，但 [#23060](https://github.com/NousResearch/hermes-agent/issues/23060) 提供零代码替代方案（独立 Hermes 会话），表明社区仍有异步 delegation 需求。
- **终端 UX 增强**：[#26202](https://github.com/NousResearch/hermes-agent/issues/26202) 提议鼠标感知输入、可点击文件路径、智能方向键，灵感来自 Claude Code。目前无关联 PR，但可能被采纳为 P3 长期改进。
- **用户时区配置**：[#26255](https://github.com/NousResearch/hermes-agent/issues/26255) 要求在 cron 及时间输出中使用用户本地时区而非 UTC，属于常见企业需求。
- **可配置默认 HTTP 头** 已通过 PR [#25949](https://github.com/NousResearch/hermes-agent/pull/25949) 实现，即将进入发布。

### 7. 用户反馈摘要
- **飞书用户** 对 Markdown 渲染不满：表格和粗体在飞书上显示为纯文本或错误格式（[#26174](https://github.com/NousResearch/hermes-agent/issues/26174)）；用户希望 Agent 能感知所在平台并调整输出格式（[#26239](https://github.com/NousResearch/hermes-agent/issues/26239)）。
- **企业集成用户** 抱怨 `delegate_task` 在 DeepSeek 供应商下完全不可用（[#26210](https://github.com/NousResearch/hermes-agent/issues/26210)），影响多模型工作流。
- **长文档用户** 多次遇到输出截断错误（[#7237](https://github.com/NousResearch/hermes-agent/issues/7237)），该 Issue 虽然关闭但用户仍在评论中要求更优雅的处理方式。
- **运维用户** 感谢修复 macOS launchd 重启问题（[#26253](https://github.com/NousResearch/hermes-agent/pull/26253)），对安全权限类修复（[#26003](https://github.com/NousResearch/hermes-agent/pull/26003)）给予积极反馈。

### 8. 待处理积压
以下为长期未响应或待维护者关注的重要 Issue/PR：
- **[#23750](https://github.com/NousResearch/hermes-agent/pull/23750)**（开放 4 天）— 修复视觉工具对非视觉模型的图片剥离。该 PR 对应热门 Bug [#25594](https://github.com/NousResearch/hermes-agent/issues/25594)，但尚未合并，需维护者评审。
- **[#16084](https://github.com/NousResearch/hermes-agent/issues/16084)**（开放 19 天）— 飞书流式卡片支持，社区讨论积极但无分配 assignee。建议在下一个大版本规划中优先考虑。
- **[#26268](https://github.com/NousResearch/hermes-agent/pull/26268)**（今日新开）— cron 投递失败重试队列，目前无 Review。若合入将显著提升 cron 可靠性。
- **[#26265](https://github.com/NousResearch/hermes-agent/pull/26265)**（今日新开）— Dashboard resume 问题修复，对应 Issue [#26264](https://github.com/NousResearch/hermes-agent/issues/26264)，需尽快审核。
- **[#20242](https://github.com/NousResearch/hermes-agent/pull/20242)**（开放 10 天）— WebUI 会话平台过滤器，功能完整但被大量 Label 标记影响范围，考虑简化后合并。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 PicoClaw 项目数据生成的 2026 年 5 月 15 日项目动态日报。

---

## PicoClaw 项目动态日报 | 2026-05-15

### 1. 今日速览

**项目状态：高度活跃，处于快速迭代期**

今日项目活跃度极高，共计处理了超过 40 个议题和合并请求。社区贡献者积极参与，成功解决了多个长期存在的稳定性与兼容性问题，特别是围绕 **OpenAI 兼容提供商** 的 `reasoning_content`（思考内容）处理、**MiMo 模型**的多轮对话适配，以及 **Web 聊天前端**的流式加载体验。虽然仍有许多待处理的 Bug 和功能需求，但今日的修复节奏表明项目正朝着更稳定的方向发展。新版本 `v0.2.8-nightly` 的发布也暗示了下一个正式版本的临近。

### 2. 版本发布

- **nightly (v0.2.8-nightly.20260515.794eb04f)**
  - **详情**：这是自动构建的夜间版本，定位为不稳定版本，仅供测试。它包含了截至 `main` 分支的所有最新提交。
  - **更新内容**：完整变更日志可 [查看此处](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)。由于是夜间构建，没有破坏性变更或迁移指南。

### 3. 项目进展

今日项目在多条战线上取得实质性进展，主要集中在提供商兼容性、UI/UX 体验和依赖项更新上。

- **修复 MiMo 模型多轮对话 Bug**：PR [#2862](https://github.com/sipeed/picoclaw/pull/2862) 已合并，解决了小米 MiMo 模型在多轮对话中因 `reasoning_content` 字段处理不当导致的 400 错误。这个修复直接对应 Issue [#2859](https://github.com/sipeed/picoclaw/issues/2859)，是用户反馈驱动的快速响应。
- **强化 OpenAI 兼容提供商流式响应解析**：PR [#2741](https://github.com/sipeed/picoclaw/pull/2741) 被关闭，它深入加固了所有 OpenAI 兼容 API 的流式响应解析，确保 `reasoning_content` 字段被正确累积和返回。
- **推进图片附件支持**：PR [#2874](https://github.com/sipeed/picoclaw/pull/2874) 被合并，修复了在 Pico 客户端中传递图片媒体时丢失的问题，改进了多模态交互体验。
- **升级 Slack 集成**：PR [#2875](https://github.com/sipeed/picoclaw/pull/2875) 合并，将 Slack Go SDK 从 v0.17.3 升级到 v0.23.1，以适配最新的 Slack API。
- **Web 前端功能增强**：
  - PR [#2587](https://github.com/sipeed/picoclaw/pull/2587) 已合并，为 Pico Web 聊天增加了端到端的流式响应支持，并优化了前端的聊天渲染和滚动体验。
  - PR [#2833](https://github.com/sipeed/picoclaw/pull/2833) (Open) 提出了 Web 和 API 层面的连接测试功能，目前正在审核中。
- **安全能力增强提议**：PR [#2877](https://github.com/sipeed/picoclaw/pull/2877) 重新发起了关于集成 `Tirith` 预执行安全扫描的提议，旨在检测 Shell 工具中的高级威胁（如同形异义字 URL）。

### 4. 社区热点

今日社区讨论热度一般，但有几个关键问题获得了较多关注。

- **高票 Bug：LLM 调用失败未重试**：Issue [#629](https://github.com/sipeed/picoclaw/issues/629) 获得了 14 条评论。用户报告长期运行的任务在遇到服务器 `HTTP 500` 时，系统直接挂起而不进行重试，这直接影响了生产可用性。虽然该 Issue 创建于 2 月，但频繁的讨论和`stale`标签表明这是一个反复被提及的核心稳定性问题。
- **核心功能提案：迁移至 OpenAI Responses API**：Issue [#2171](https://github.com/sipeed/picoclaw/issues/2171) 虽已关闭，但其 11 条评论说明社区对保持与 OpenAI 最新 API 标准的兼容性有强烈共识。关闭意味着该重构任务很可能已被规划或在幕后进行中。
- **用户痛点：DeepSeek v4 思考模型兼容性**：Issue [#2706](https://github.com/sipeed/picoclaw/issues/2706) 近期关闭，它深刻反映了国产模型（如 DeepSeek、MiMo）带来的适配挑战。问题关键在于正确处理 `reasoning_content` 字段的回传，社区对此既有解决方案的讨论，也有“我不会”的无奈，揭示了提供商兼容性仍是核心痛点。

### 5. Bug 与稳定性

今日报告的 Bug 主要集中在会话管理和模型兼容性上，多数已有对应的修复 PR。

| 严重程度 | Bug 描述 | 相关 Issue | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | **Anthropic Messages API 的 `tool_use_id` 竞争条件仍未修复**。用户报告在 `v0.2.5` 版本中依然可复现。 | [#2721](https://github.com/sipeed/picoclaw/issues/2721) | **已关闭**（可能是通过其他 PR 修复，但无直接指向） |
| **中** | **小米 MiMo 模型多轮对话超 3 轮后报 400 错误**。问题根因是 `reasoning_content` 未正确回传。 | [#2859](https://github.com/sipeed/picoclaw/issues/2859) | **已关闭**（被 PR [#2862](https://github.com/sipeed/picoclaw/pull/2862) 修复） |
| **中** | **对话历史只能看到最后一条用户消息**。用户查看历史会话时，只看到最后一条消息，前面的内容丢失。 | [#2795](https://github.com/sipeed/picoclaw/issues/2795) | **待处理** |
| **中** | **Telegram 机器人上传 PDF 后流式处理中断**。用户在 Telegram 中发送 PDF 文件后，后续对话失效。 | [#2798](https://github.com/sipeed/picoclaw/issues/2798) | **待处理** |
| **低** | **多用户群组聊天历史缺乏发送者归属**。在默认会话范围下，历史消息无法区分是哪个用户发送的。 | [#2702](https://github.com/sipeed/picoclaw/issues/2702) | **待处理** |

### 6. 功能请求与路线图信号

- **安全增强：Shell 命令预执行扫描**：用户 `sheeki03` 提出的集成 `Tirith` 扫描器的 PR [#2877](https://github.com/sipeed/picoclaw/pull/2877) 提交了最新版本，增强了安全态势。这可能是下一阶段安全功能的重要方向。
- **子 Agent 角色分离**：Issue [#2775](https://github.com/sipeed/picoclaw/issues/2775) 指出子 Agent 会错误继承根 Agent 的 `AGENT.md`，导致角色混淆。这是一个核心的多 Agent 架构问题，有 2 条评论，说明用户对此有迫切需求，但尚无对应的 PR。
- **文档全面更新至 V3 配置格式**：PR [#2766](https://github.com/sipeed/picoclaw/pull/2766) 正在更新 26 个文件以匹配 V3 配置格式（`api_key` → `api_keys` 等）。这暗示项目正在进行一次配置体系的重构，该 PR 很可能会被合并到下一个版本。

### 7. 用户反馈摘要

- **对稳定性有较高期待**：来自 Issue [#629](https://github.com/sipeed/picoclaw/issues/629) 的用户反馈，他们在长时间运行任务时遭遇 `HTTP 500` 错误，而系统缺乏优雅的重试机制，导致任务失败。这表明在生产环境中，应用的容错能力是用户的重点关注项。
- **对多用户场景下的体验不满**：Issue [#2702](https://github.com/sipeed/picoclaw/issues/2702) 反映了在 Discord 等群组场景下，所有用户共享同一会话，导致历史消息不区分发送者，这给多用户协作带来了混乱。
- **对国产模型的支持存在摩擦**：从 Issue [#2706](https://github.com/sipeed/picoclaw/issues/2706) 和 [#2859](https://github.com/sipeed/picoclaw/issues/2859) 可以看出，用户在尝试适配像 DeepSeek v4 和 小米 MiMo 这样的新兴国产模型时，遇到了字段不兼容的问题。用户希望项目能提供更好的抽象层来平滑支持这些模型。
- **对会话历史的完整性和准确性有要求**：Issue [#2795](https://github.com/sipeed/picoclaw/issues/2795) 和 [#2787](https://github.com/sipeed/picoclaw/issues/2787) 的提出者明确指出，当前会话的历史查看功能和消息时间戳显示存在缺陷，影响了他们对聊天记录的可信度。

### 8. 待处理积压

- **长期未解决的高活跃 Bug**：Issue [#629](https://github.com/sipeed/picoclaw/issues/629) (**[BUG] Didn't retry if meet LLM call failed**)。自 2026-02-22 创建以来，一直有 14 条评论，且已标记为 `stale`。这是一个影响核心可用性的稳定性问题，需要维护者优先考虑排期修复。
- **多用户群组会话归属问题**：Issue [#2702](https://github.com/sipeed/picoclaw/issues/2702) (**[BUG] Multi-user group channels: conversation history lacks sender attribution**)。虽创建于 4 月 28 日，但已超过两周无新进展。随着社区规模扩大，此类协作特性将变得愈发重要。
- **子 Agent 角色继承问题**：Issue [#2775](https://github.com/sipeed/picoclaw/issues/2775) (**[Feature]子 Agent 继承根 Agent 的 AGENT.md 导致角色身份混淆**)。这是一个核心的多 Agent 架构缺陷，直接影响 Agent 的能力和正确性。目前有 2 条评论，表明用户关注但尚无解决方案。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据 nanoqwibitai/nanoclaw 项目在 2026-05-15 的 GitHub 数据生成的每日动态报告。

---

### NanoClaw 项目日报 | 2026-05-15

**项目名称:** NanoClaw
**数据采集时间:** 2026-05-15 23:59 UTC
**分析师:** AI Analyst

---

### 1. 今日速览

今日项目活跃度极高，尤其是 **PR 活动** 非常密集。过去 24 小时内共有 25 条 PR 被提出或更新，其中 13 条已完成合并或关闭，显示出项目团队正在快速推进功能开发和修复。合并的 PR 主要集中在 **社区功能整合**（如 LinkedIn、Reddit）和 **基础设施本地化**（如网站审计工具）。与此同时，一个关键的新 Issue 报告了 **Docker Desktop on Linux 下的三个 Bug**，可能会阻碍部分用户的新部署，需重点关注。整体来看，项目正在经历快速的功能扩展和迭代，社区贡献活跃，但稳定性方面也面临着新的挑战。

### 2. 版本发布

**无**

过去 24 小时内无新版本发布。

### 3. 项目进展

今日项目在功能和工具生态上取得了显著进展，主要体现在以下方面：

- **社交媒体与社区运营功能矩阵建立:** 多个与外部平台集成的 Skill 被合并。这标志着 NanoClaw 的 Agent 能力从简单的聊天回复扩展到了更复杂的社交平台运营。
  - [PR #2447](https://github.com/nanocoai/nanoclaw/pull/2447) ✅ **已关闭**: 新增 Reddit 集成 Skill (`/reddit-research`) 和只读 MCP，可进行市场研究。
  - [PR #2448](https://github.com/nanocoai/nanoclaw/pull/2448) ✅ **已关闭**: 新增复合式社交舆情监听 Skill (`/social-listening`)，聚合多个搜索源。
  - [PR #2449](https://github.com/nanocoai/nanoclaw/pull/2449) ✅ **已关闭**: 新增 LinkedIn 社区管理 Skill (`/linkedin-community`)，可自动发布、评论和管理连接请求。
  - [PR #2450](https://github.com/nanocoai/nanoclaw/pull/2450) ✅ **已关闭**: 新增 LinkedIn 广告投放 Skill 集，为广告运营提供 Playbook。

- **网站审计自托管工具链构建:** 项目移除了依赖外部第三方服务（squirrelscan）的审计方式，转而构建了自托管的审计工具链，增强了自主性和可靠性。
  - [PR #2451](https://github.com/nanocoai/nanoclaw/pull/2451) ✅ **已关闭**: 从上游本地化 `audit-website` Skill。
  - [PR #2452](https://github.com/nanocoai/nanoclaw/pull/2452) ✅ **已关闭**: 在容器内集成 Lighthouse CLI。
  - [PR #2455](https://github.com/nanocoai/nanoclaw/pull/2455) ✅ **已关闭**: 完成使用 Lighthouse + axe + linkinator 的复合本地审计栈。

- **文档与代码清理:**
  - [PR #2453](https://github.com/nanocoai/nanoclaw/pull/2453) ✅ **已关闭**: 本地化了 `copy-grader` Skill。
  - [PR #2454](https://github.com/nanocoai/nanoclaw/pull/2454) ✅ **已关闭**: 新增了 OneCLI 密钥管理的文档。
  - [PR #2473](https://github.com/nanocoai/nanoclaw/pull/2473) ✅ **已关闭**: 修复了关于 `<internal>` 标签的误导性描述。

**总结:** 项目今日在社区功能扩展和基础能力自建上迈出了一大步，表明项目正朝着功能更丰富、更独立的 Agent 平台演进。

### 4. 社区热点

今日社区焦点集中在 **cron 任务交付故障** 和 **Docker 部署障碍** 两个核心问题上。

1.  **#2480: Docker Desktop Linux 启动故障 [热度最高]**
    - **链接:** [#2480](https://github.com/nanocoai/nanoclaw/issues/2480)
    - **诉求:** 这是一个全新的 Issue，报告了在 Linux 上通过 Docker Desktop 新安装时，Agent 容器因三个叠加 Bug 而立即崩溃。这是 **新用户上手的阻塞性问题**，对项目吸引新用户影响巨大。尽管目前零评论，但其严重性使其成为社区关注的焦点。

2.  **#2481: Cron 输出被静默抑制 [讨论焦点]**
    - **链接:** [#2481](https://github.com/nanocoai/nanoclaw/pull/2481)
    - **诉求:** 这是一个旨在修复长期存在的 cron 任务“假死”问题的 PR。用户报告的“cron 不工作”实际上是 Agent 处理了任务但“输出了但没发出去”。这暴露了 Agent 在处理异步任务时，输出管道存在缺陷，影响所有依赖定时任务的自动化场景。

### 5. Bug 与稳定性

- **严重: Docker Desktop on Linux 新安装启动崩溃 [新报告，暂无修复]**
  - **链接:** [#2480](https://github.com/nanocoai/nanoclaw/issues/2480)
  - **描述:** 最新 Issue，报告了在 Linux 新安装环境下，Agent 容器因三个 Bug 连续爆发而崩溃，返回退出码 1。用户会收到 `Claude Code native binary not found at /pnpm/claude` 等错误。**这是当前最严重的稳定性问题，因为其阻止了新用户的正常使用。**

- **中等: Agent Cron 输出自抑制 [已有修复方案]**
  - **链接:** [#2481](https://github.com/nanocoai/nanoclaw/pull/2481) (待合并)
  - **描述:** 两个独立的 Bug 导致 Lili 和 Lobby 两个 Agent 的 cron 任务输出被静默丢弃或自我静音。虽然 Agent 在执行，但用户收不到任何结果反馈，严重影响了 cron 功能的可靠性。**该 PR 正在等待合并以解决此问题。**

- **低: WhatsApp 解密失败恢复指引错误 [已有修复方案]**
  - **链接:** [#2469](https://github.com/nanocoai/nanoclaw/pull/2469) (待合并)
  - **描述:** 当 WhatsApp 适配器出现解密失败或 401 登出时，系统给出的恢复指引是无效的（`launchctl kickstart`），无法真正解决问题。**这是一个用户体验 Bug，会误导运维人员做出无效操作。**

### 6. 功能请求与路线图信号

从今日活跃的 PR 可以明确看到项目的功能发展方向：

- **多云/多模型支持:** [PR #2475](https://github.com/nanocoai/nanoclaw/pull/2475) 提案让 Agent 对 Codex 的支持与 Claude Code 一致，[PR #2474](https://github.com/nanocoai/nanoclaw/pull/2474) 则设想在 setup 阶段就允许用户选择 Claude Code 或 Codex。这表明项目正在积极拥抱多云时代的趋势，降低供应商锁定风险。
- **精细化的权限与安全控制:** [PR #2478](https://github.com/nanocoai/nanoclaw/pull/2478) 加强了审批响应路径的安全性，要求审批人必须是 admin 角色。这反映了项目在向企业级应用迈进时，对安全性的重视。
- **Agent 间的网络访问控制:** [PR #2477](https://github.com/nanocoai/nanoclaw/pull/2477) 提出了让 Skill 能够调控 Agent 的互联网访问权限。这是一个极具创新性的功能，允许不同 Skill 在执行时为 Agent 创建隔离或受限的网络环境，增强了安全性和可控性。
- **更好的聊天体验:** [PR #2472](https://github.com/nanocoai/nanoclaw/pull/2472) 和 [PR #2471](https://github.com/nanocoai/nanoclaw/pull/2471) 都在致力于优化 Slack 的 `per-thread` 会话模式，修复了同一线程内消息混乱的问题，提升了用户体验。

这些 PR 均处于待合并状态，很可能会被纳入下一个版本中。

### 7. 用户反馈摘要

从有限的信息中，可以提炼出以下核心用户反馈和痛点：

- **新用户部署阻力大:** [#2480](https://github.com/nanocoai/nanoclaw/issues/2480) 的提交者（AlonMiz）在 Linux 新环境中遇到了严重的部署问题，反映了当前开箱即用体验不佳的现状。
- **关键任务可靠性受质疑:** [#2481](https://github.com/nanocoai/nanoclaw/pull/2481) 的提交者（zoryon-dev）揭示了 cron 任务输出“假死”的问题，这种“静默失败”模式对信任破坏极大，用户可能因此怀疑 Agent 是否真的在执行任务。
- **适配器恢复路径不友好:** [#2469](https://github.com/nanocoai/nanoclaw/pull/2469) 的提交者指出，WhatsApp 适配器在故障时给用户提供的是无效的恢复指南，这显示部分模块的诊断和自我修复能力不足。

### 8. 待处理积压

经过对近期数据的扫描，未发现长期无响应的 Issue 或 PR。项目的活跃度极高，几乎所有的讨论和贡献都在短时间内得到了响应。需要注意 [#2469](https://github.com/nanocoai/nanoclaw/pull/2469) (WhatsApp 修复) 虽然创建于 5月14日，但仍在更新中，不属于长期积压。目前项目维护响应及时，无严重积压问题。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，以下是为您生成的 IronClaw 项目动态日报。

---

# IronClaw 项目动态日报 — 2026-05-15

## 1. 今日速览

过去24小时内，IronClaw 项目保持极高的活跃度，共计有100项 Issues 和 PR 被更新。其中，核心团队正全力推进 **“Reborn”架构的落地**，大量相关 issues 和 pull requests 被创建和更新。一个重要的里程碑是 `v0.28.2` 补丁版本正式发布，紧急修复了关键的 chat-driven `tool_install` 回归问题。同时，一个大型基础设施重构PR（通用 FS 分发）进入最终合并阶段，显示了项目在架构统一方面的坚定步伐。整体来看，项目正处于一个密集交付与架构转型并行的高速发展期。

## 2. 版本发布

### ironclaw-v0.28.2
- **发布日期**: 2026-05-14
- **类型**: 补丁版本
- **Release Notes**: [查看详情](https://github.com/nearai/ironclaw/releases/tag/ironclaw-v0.28.2)
- **主要更新**:
    - **修复**: 恢复了 chat-driven `tool_install` 功能；修复了工具调用时的双重调用（double-invoke）问题；修复了 auto-approve 功能中的 `footgun` 安全问题。 (PR [#3559](https://github.com/nearai/ironclaw/pull/3559))
    - **变更**: 将提供商特定的认证、模型抓取和嵌入配置隐藏到外观模式（Facades）之后，提升了 LLM 模块的架构清晰度和模块化。(PR [#3416](https://github.com/nearai/ironclaw/pull/3416))
- **破坏性变更**: 无。
- **迁移注意事项**: 此版本主要修复 Bug，无重大配置或 API 变更，建议所有用户尽快升级。

## 3. 项目进展

今日有多个重要 PR 被合并或关闭，标志着项目在多个关键路径上取得进展：

- **重构与基础设施**: `ilblackdragon` 合并了系列重构 PR，将多个消费者 crate（如 `run-state`, `authorization`, `outbound`）的文件系统操作迁移至统一的 `RootFilesystem` 分发架构（PR [#3679](https://github.com/nearai/ironclaw/pull/3679)），并最终关闭了过渡性 PR `#3678`, `#3672`, `#3671`, `#3670`。这显著提升了项目在底层存储抽象上的一致性和可维护性。
- **安全加固**: `serrrfirat` 合并了 PR [#3638](https://github.com/nearai/ironclaw/pull/3638)，修复了 Reborn 默认主机策略的安全隐患，使其默认明确拒绝（fail-closed），而非依赖模糊的默认值。
- **Bug 修复**: `nickpismenkov` 提交的 PR [#3682](https://github.com/nearai/ironclaw/pull/3682) 修复了金丝雀测试流程中的假阴性问题，确保未来的回归能被准确捕捉。
- **架构文档**: `hanakannzashi` 提交了 PR [#3683](https://github.com/nearai/ironclaw/pull/3683)，为 Reborn 架构定义了清晰的宿主自有入口边界契约，是 WebUI Beta 版本的关键前置工作。
- **功能开发**: 多组“工作流（Workstream）”PR（如 `#3645`, `#3644`）开始落地“代理循环”规范中的检查点存储与恢复、能力宿主端口等基础功能。

## 4. 社区热点

- **#2987 [EPIC] Track Reborn architecture landing strategy and grouped PR plan** ([链接](https://github.com/nearai/ironclaw/issues/2987))
    - **评论: 44 | 👍: 0**
    - **分析**: 作为 Reborn 架构落地的总协调 Issue，今日吸引了最多的社区讨论（44条）。核心贡献者在此 Issue 中持续更新架构落地路线图，讨论分组 PR 的策略。这反映了社区对 Reborn 这一重大架构转型的高度关注和积极参与。

- **#3022 [Reborn] cutover blocker: add event substrate integration tests** ([链接](https://github.com/nearai/ironclaw/issues/3022))
    - **评论: 9 | 👍: 0**
    - **分析**: 作为 Reborn 架构切换的阻塞项，此 Issue 讨论了事件子系统的集成测试方案，旨在验证新的生产者能否正确输出更安全、可重放的事件。社区讨论的核心诉求是确保新旧架构切换过程中的稳定性和数据完整性。

- **#3259 Publish 0.25.0–0.27.0 to crates.io** ([链接](https://github.com/nearai/ironclaw/issues/3259))
    - **评论: 4 | 👍: 0**
    - **分析**: 用户报告了 crates.io 上 `ironclaw` 包的版本严重落后于 GitHub 仓库（最大为 0.24.0，但仓库已发到 0.27.0），导致下游用户因 wasmtime 漏洞而被迫锁定在旧版。此 Issue 反映了社区对版本发布流程滞后的不满，并请求尽快同步。

## 5. Bug 与稳定性

按严重程度排列：

- **高**: [Nightly E2E 测试失败](https://github.com/nearai/ironclaw/issues/3447)
    - 自动化报告：Nightly E2E 定时运行失败。这是持续集成稳定性预警，需排查失败作业原因。
- **高**: [OpenAI 兼容提供商 `reasoning_content` 丢失导致 DeepSeek 多轮工具调用失败](https://github.com/nearai/ironclaw/issues/3673)
    - 严重度：高，影响特定模型（如 DeepSeek v4-pro）的多轮工具调用功能。目前尚在报告阶段，未关联修复 PR。
- **中**: [TUI 无法正确渲染 Markdown 表格](https://github.com/nearai/ironclaw/issues/3675)
    - 严重度：中，影响终端用户的使用体验。目前尚无关联修复 PR。
- **中**: [Telegram 在 NEAR Foundation 实例上无法工作](https://github.com/nearai/ironclaw/issues/2902)
    - 严重度：中，影响特定部署场景用户。自4月23日创建以来，已有1条评论但未关闭，需关注。
- **低**: [Chat-driven `tool_install` 回归问题已在 `v0.28.2` 修复](https://github.com/nearai/ironclaw/pull/3559)
    - 该严重回归问题已被隔离并通过补丁版本解决。

## 6. 功能请求与路线图信号

- **Reborn WebUI Beta (P0)**: 大规模功能请求集中在 Reborn Beta 版本，尤其是 WebUI 界面。一系列高优（P0）Issue（如 `#3623`, `#3611`, `#3612`, `#3607`）被创建，规划了从“输入策略层”、“入口 DTO 契约”到“RebornServices 外观”等关键功能。相应的 PR（如 `#3632`, `#3664`)也已提交，表明这些功能很可能纳入下一版本。
- **“配置即代码” (Epic)**: Issue [#3036](https://github.com/nearai/ironclaw/issues/3036) 提出了一个长远的、呼声很高的功能——为 Reborn 架构提供声明式配置能力，以解决当前配置散乱、无审计等问题。虽然目前评论不多，但作为 Epic Issue，其指向的路线图信号非常明确。
- **全功能钩子框架 (P2)**: 多个 Issue (`#3524`, `#3523`) 和 PR (`#3573`, `#3633`, `#3636`, `#3637`) 旨在为 Reborn 代理循环添加一级钩子（Hook）支持，用于实现策略、审批、授权等。这是一个特性丰富的功能，目标版本可能不会在WebUI Beta之前，但已进入详细设计阶段。

## 7. 用户反馈摘要

- **痛点**:
    - **版本发布滞后**: 从 Issue [#3259](https://github.com/nearai/ironclaw/issues/3259) 可以看出，用户对 crates.io 上版本严重滞后感到困扰，无法及时获取安全更新和新功能。
    - **特定模型兼容性**: Issue [#3673](https://github.com/nearai/ironclaw/issues/3673) 的提交者报告了使用 DeepSeek 模型时遇到的功能阻塞问题，反映出用户对多模型支持有较高期待，且对回归问题敏感。
- **使用场景**:
    - 用户 `sergeiest` 在 [#2902](https://github.com/nearai/ironclaw/issues/2902) 中报告了 Telegram 集成失效，表明 Telegram 是其托管服务的重要渠道。
    - 用户 `chenyulue` 在 [#3675](https://github.com/nearai/ironclaw/issues/3675) 中提交了 TUI 渲染问题，这表明有一批用户是通过终端界面来使用、测试项目功能的。
- **不满**: 主要通过 Issue `#3259` 表达了对发布流程和速度的不满。

## 8. 待处理积压

- **P0/P1 阻塞项**: 作为 Reborn 架构切换的关键阻塞项，Issue [#3022](https://github.com/nearai/ironclaw/issues/3022)（事件子系统的集成测试）自4月28日创建以来，虽有讨论但无实质性进展。这是通往 Reborn 正式版道路上必须清除的路障，值得维护者优先关注。
- **长期未决问题**: Issue [#3036](https://github.com/nearai/ironclaw/issues/3036)（配置即代码Epic）虽然创建于4月底，也有关注者（1个👍），但目前评论较少，可能因优先级问题被暂时搁置。维护者或可考虑在路线图讨论中澄清其预期时间线。
- **发布的 PR**: 多个大型 PR 如 `#3590` (Telegram v2), `#3633`, `#3573` (钩子框架), 以及 `#3645`, `#3644` (代理循环子组件) 均处于开放状态，且已有多日无新活动或评论。社区期待这些关键功能的合并进展。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 LobsterAI 项目数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

## LobsterAI 项目动态日报 — 2026-05-15

### 今日速览

今日项目活跃度极高，主要源于对历史积压工作（`stale` 标签 PR）的集中清理与合并。过去24小时内，共有 **33 条 PR 被合并或关闭**，表明维护团队正在进行大规模的代码库维护与稳定性提升工作。一个高优 Bug（模型调用强制绑定网易服务）被社区用户报告，已引起关注。同时，`v2026.5.14` 版本发布，引入了关键的插件管理功能和底层协作优化。**整体来看，项目虽处于高强度的维护与修复周期，但核心功能改进与社区反馈处理正稳步推进。**

### 版本发布

- **发布版本**：[LobsterAI 2026.5.14](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.5.14) | 发布日期: 2026-05-14
- **更新内容**：
    - `feat(cowork)`: 改进了 OpenClaw 上下文压缩（Context Compaction）处理逻辑，可能影响长对话的性能与稳定性。
    - `feat(plugins)`: 新增了插件管理系统，支持高级配置（Advanced Config）。这是一个重要的架构性新增，允许用户通过插件扩展核心功能。
- **破坏性变更评估**：公告中未明确列出破坏性变更，但 **`feat(plugins)` 的引入意味着项目整体架构发生变动**，用户需注意：
    - **配置迁移**：旧的配置文件可能与新版不兼容，特别是涉及自定义配置项的用户。建议备份旧配置文件后升级。
    - **插件兼容性**：若用户此前已通过手动方式集成插件，新版可能需要迁移至新的插件管理框架。
- **迁移注意事项**：
    1.  升级前务必备份 `cowork_config` 及其他关键配置文件。
    2.  仔细检查新版本提供的插件设置页面，确保所有之前依赖的自定义功能都能在新的插件体系下正常工作。
    3.  关注后续官方文档中关于插件管理的说明。

### 项目进展

今日项目取得了显著进展，主要体现在对大量历史遗留 PR 的修复与合并上，覆盖了安全、性能、功能性和用户体验等多个方面：

- **IM 功能完善**：PR [#1987](https://github.com/netease-youdao/LobsterAI/pull/1987) 已合并，为 Telegram、Discord、QQ、POPO 平台添加了“配对码”输入框，解决了在特定权限策略下的配对审批流程缺陷，显著提升了跨平台IM的可用性。
- **协同编辑稳定性**：PR [#1986](https://github.com/netease-youdao/LobsterAI/pull/1986) 修复了 `managed session` 中的字符丢失问题（如 `file:///` 变为 `file://`），通过更精确的文本替换逻辑，解决了会话同步中的内容损坏Bug，增强了协同功能的可靠性。
- **安全性与性能增强**：
    - 多项针对安全性的修复被合并：
        - [PR #822](https://github.com/netease-youdao/LobsterAI/pull/822): 统一令牌刷新锁，消除了潜在的竞态条件。
        - [PR #826](https://github.com/netease-youdao/LobsterAI/pull/826): 为 `shell.openExternal` 增加了URL协议白名单验证，防止恶意协议注入。
        - [PR #828](https://github.com/netease-youdao/LobsterAI/pull/828): 修复了 `localfile://` 协议处理器的路径遍历漏洞，防御任意文件读取攻击。
    - 性能优化方面也有关键合并：
        - [PR #830](https://github.com/netease-youdao/LobsterAI/pull/830): 优化了 SQLite 数据库核心参数（如 `journal_mode`, `cache_size`），预期将大幅提升日常操作的读写性能。
        - [PR #1186](https://github.com/netease-youdao/LobsterAI/pull/1186): 优化了流式响应渲染性能，通过 `React.memo` 和 `createSelector` 消除了全量重渲染，解决了长对话场景下的UI卡顿问题。
- **功能性与用户体验优化**：
    - [PR #827](https://github.com/netease-youdao/LobsterAI/pull/827): 新增了技能重复安装检测。
    - [PR #835](https://github.com/netease-youdao/LobsterAI/pull/835): 为 MCP 服务器管理增加了 JSON 粘贴模式，支持批量创建服务器，提升了高级用户的配置效率。
    - [PR #1185](https://github.com/netease-youdao/LobsterAI/pull/1185): 为已安装的技能卡片增加了“打开文件夹”按钮，便利了用户手动编辑技能文件。

### 社区热点

- **热点 Issue**：[#1988 模型调用问题](https://github.com/netease-youdao/LobsterAI/issues/1988)
    - **诉求分析**：用户 `nee207` 报告在升级后，系统会强制将 `qwen3.6-plus` 等第三方模型（阿里百炼）的调用强制更改/路由到网易自有的服务，导致用户因没有网易额度而无法使用，即便手动修改配置文件也无法覆盖。**这触及了用户对模型选择自由度的核心关切。** 用户期望一个开源项目能够完全遵循用户的本地配置，而非在后台进行强制性的服务路由或配置修改。该 Issue 虽只有 1 条评论，但涉及核心功能与用户信任，是今日社区最突出的声音。

### Bug 与稳定性

- **严重 (P0) - 模型调用强制绑定**：
    - **报告**：[Issue #1988](https://github.com/netease-youdao/LobsterAI/issues/1988) - 升级后，系统强制将第三方模型调用指向网易自带服务，导致用户无法使用。
    - **状态**：新开，未分配，无关联 PR。该Bug严重影响用户对模型使用的自主权，需优先处理。

- **中/低等 (P1/P2) - 已修复会话丢失/字符丢失**：
    - **报告**：[PR #1986](https://github.com/netease-youdao/LobsterAI/pull/1986) 修复了 `managed session` 中的字符重复/丢失问题。该 Bug 会导致协同编辑时内容错乱，已通过 PR 修复并合并。

- **中等 (P2) - 历史性能问题修复**：
    - **报告**：[PR #806](https://github.com/netease-youdao/LobsterAI/pull/806) 和 [PR #830](https://github.com/netease-youdao/LobsterAI/pull/830) 分别解决了大量会话的性能瓶颈和SQLite性能问题，相关 PR 已合并，稳定性修复将在下一个版本中体现。

### 功能请求与路线图信号

- **已在路线图上**：`feat(cowork):` 的持续改进（如上下文压缩）和 `feat(plugins):` 的引入，表明官方正在强化项目的协同能力与架构的可扩展性。
- **潜在新功能**：[PR #1985](https://github.com/netease-youdao/LobsterAI/pull/1985) 新增了“思考级别控制”（Thinking Level Control），这是一项用于精细控制AI推理深度的强大功能。目前为开放状态，鉴于其完整的前后端实现，有很大概率被合并到下一版本中。
- **社区信号**：Issue #1988 的用户诉求（拒绝强制服务绑定）是一个非常强烈的信号。它暗示社区希望 LobsterAI 保持纯粹的“开源、可配置、本地优先”特性。若未来版本不能妥善解决此问题，可能会引发更多类似反馈。

### 用户反馈摘要

- **痛点**：当前最突出的用户痛点来自 **[Issue #1988](https://github.com/netease-youdao/LobsterAI/issues/1988)**。用户明确表达了以下不满：
    > “修改配置文件也没用，系统会强制改成错误的。”

    这体现了用户在失去对工具控制权时的挫败感。用户期望配置文件的优先级高于任何软件的硬编码逻辑。

### 待处理积压

尽管今日合并了大量积压PR，但仍有问题的悬而未决，需要维护团队关注：

- **长期未响应的重要 Issue/PR**：
    - **回归性问题**：[PR #807](https://github.com/netease-youdao/LobsterAI/pull/807) (`executionMode` 配置不生效，更新于 2026-05-15)：对用户配置不生效问题的修复，虽然再次被标记为开放，但长期未收到进一步推进，可能是一个需要关注的回归点。
    - **性能优化**：[PR #806](https://github.com/netease-youdao/LobsterAI/pull/806) (会话列表性能：更新于 2026-05-15)：与已被合并的性能优化PR (#830) 相关联，同为内核性能改进，但其提出的索引方案尚未合并，可能需要协调以避免冲突。

**建议**：维护团队可优先审查并处理 **Issue #1988**，评估其严重性并给出明确的回应或修复计划，以恢复社区对项目“开源可控”特性的信心。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 2026-05-15

---

## 1. 今日速览

过去24小时项目活跃度较低，仅产生1条新的Bug报告，无任何Pull Requests或版本发布。社区讨论沉寂，未出现高互动议题。当前核心问题集中在TLS证书生成仅支持localhost的文档-实现不一致，可能影响用户的生产环境部署体验。整体来看项目进入短期平稳期，但该Bug值得维护团队优先关注。

---

## 2. 版本发布

无

---

## 3. 项目进展

- **24小时内无 Pull Requests 被合并或关闭**，项目没有新增功能、重构或修复推进。代码库状态保持前一日水平。

---

## 4. 社区热点

- **#996 [Bug]: Generated TLS certificates only work for localhost, contrary to the docs**  
  [前往 Issue](https://github.com/moltis-org/moltis/issues/996)  
  作者：IlyaBizyaev  
  这是过去24小时唯一的社区活动，虽无评论，但问题本质触及用户对文档信任的核心矛盾：用户按照文档预期使用TLS证书功能，却只能用于localhost。该问题若未及时澄清或修复，可能引发更多用户困惑，甚至导致对项目安全性与文档质量的质疑。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 状态 | 是否有 Fix PR |
|----------|-------|------|---------------|
| **高**   | #996 – TLS证书仅对localhost生效，与文档描述不符 | 开放，0评论，0👍 | 否 |

**分析**：该Bug直接影响用户在生产或非本地环境中启用HTTPS的能力，属于功能行为与文档严重不一致。尽管暂无证据表明崩溃或回归，但其对信任度的潜在损害较大。维护者应尽快确认是文档过时、配置遗漏还是代码缺陷，并给出回应。

---

## 6. 功能请求与路线图信号

无新功能请求被提出。考虑到当前唯一活跃Issue为Bug报告，下一版本很可能优先修复此TLS证书范围问题，而非引入新特性。

---

## 7. 用户反馈摘要

从Issue #996 的预检查清单中可提取到以下用户行为特征：
- 用户已遵循 **搜索现有Issues** 流程，表明其具备一定开源协作素养，非随意报Bug。
- 用户声明正在使用 **最新版本**，排除了旧版本已知问题。
- 用户未提供聊天会话上下文（checkbox未勾选），说明该问题可能独立于特定会话场景出现，更具普遍性。

核心痛点：**文档承诺的能力与软件实际行为存在偏差**，这类问题对用户信任的伤害往往比纯功能缺失更严重。

---

## 8. 待处理积压

截至本日报生成时，**无长期未响应的重要Issue或PR**。项目积压情况健康，唯一开放Issue #996 尚处于刚创建阶段，建议维护者在48小时内给予初步回应或标记优先级。

---

*本日报基于Moltis GitHub仓库公开数据自动生成，仅供项目健康度参考。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 CoPaw 项目 GitHub 数据，为您生成 2026 年 5 月 15 日的项目动态日报如下。

---

# CoPaw 项目动态日报 | 2026-05-15

## 1. 今日速览

今日 CoPaw 项目整体**高度活跃**，共有 40 条 Issue 更新和 50 条 PR 更新。社区讨论热烈，主要集中在多项关键 Bug 的修复（如 Agent 身份混淆、MiMo 模型思考模式冲突、write_file 循环报错），以及**安全性**（备份导入/恢复加固、Channel 配置明文写入风险）和**代码质量**（后端单元测试覆盖率专项提升）两大主题上。项目维护者响应迅速，当日关闭了 11 个 Issue 并合并/关闭了 33 个 PR，体现了良好的项目维护效率和健康发展态势。此外，社区贡献活跃，涌现出多个新功能 PR。

## 2. 版本发布

**无。**

## 3. 项目进展

今日项目在安全性、稳定性、功能完善和代码质量方面均取得显著进展。以下为已合并或关闭的关键 PR：

- **安全性加固：**
    - **备份导入/恢复信任控制加固 (#4409)**：对备份文件的创建、导入和恢复过程增加了 HMAC 签名和验证，阻止未经认证的远程访问，解决了报告的备份安全漏洞。这是提升项目安全等级的关键一步。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4409)
    - **反垃圾信息门控 (#4422)**：引入 CI 自动化机制，当用户开启的 Issue/PR 数量超过 10 个时，自动关闭新提交，以应对大量未经核实的 AI 生成内容，维护社区讨论质量。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4422)
- **核心稳定性修复：**
    - **钉钉频道消息处理重构 (#4420)**：移除了旧有的同步回复路径，将所有消息处理统一到基类事件循环中，并支持 AI 卡片模式的流式输出，提升了钉钉渠道的稳定性和响应体验。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4420)
    - **计划模式门控强化 (#4198)**：修复了用户在确认 Plan 之前，Agent 即可执行非计划工具（如 `execute_shell_command`）的绕过漏洞，强化了计划模式的执行约束。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4198)
    - **依赖升级与代码清理 (#4419)**：将底层依赖 `agentscope` 升级至 `1.0.20`，移除了不再需要的 MCP JSON schema 猴子补丁，改善了工具的兼容性和维护性。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4419)
- **功能增强与新范式：**
    - **模型配置灵活化 (#4417)**：允许用户为每个模型单独配置 `max_tokens` 和 `max_input_length`，增强了模型控制的粒度，并包含向后兼容的迁移逻辑。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4417)
    - **提供商自定义 URL 支持 (#4387)**：移除 Anthropic 提供商的 URL 限制，用户现可自由配置兼容 Anthropic API 的自定义基础 URL，如使用代理或第三方服务。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/4387)
    - **插件生态扩展 (#4418, #4423)**：社区贡献了新的 `qwenpaw pet plugin`，同时官方修复了 Alibaba Cloud Plugin (`CloudPaw`) 的集成问题，增强了远程 Agent 托管能力。 [详情1](https://github.com/agentscope-ai/QwenPaw/pull/4418) [详情2](https://github.com/agentscope-ai/QwenPaw/pull/4423)
    - **开发者体验优化 (#3787)**：修复了侧边栏 Plan 面板在重新打开后未能同步最新状态的问题。 [详情](https://github.com/agentscope-ai/QwenPaw/pull/3787)

## 4. 社区热点

今日社区讨论焦点集中，主要围绕以下三个议题：

1.  **后端单元测试覆盖率提升 (#4342, #4339, #4340, #4341)**
    - **热度**：累计评论超 21 条。用户 `hanson-hex` 提交了一系列 Issue，目标是将后端单元测试覆盖率提升至目标水平，涉及 app、cli、config、local_models 等多个模块。
    - **分析**：这表明社区中有活跃成员正在系统性地进行代码质量加固工作。这不仅是维护者的需求，也反映了用户对项目长期稳定性和可靠性的重视。维护者应对此给予充分肯定并积极审核相关 PR。

2.  **`write_file()` 死循环报错 (#4299)**
    - **热度**：7 条评论。
    - **分析**：该 Bug 影响广泛，只要输出内容较长就会触发，严重依赖文件输出功能的用户影响较大。用户 `wellhi` 提供了清晰的复现步骤。**这是一个需要优先处理的稳定性问题**，好消息是今日合并的 PR #4417 可能从内存配置角度缓解此问题，但根因还需进一步排查。

3.  **Agent 身份混淆与工作空间错误切换 (#3957)**
    - **热度**：8 条评论。已关闭。
    - **分析**：这是一个严重的身份混淆问题：当主控 Agent 通过钉钉频道接收消息时，其工作空间会被错误切换到发送消息的 Agent 的 workspace，导致逻辑错误。此 Bug 来源于真实生产环境（钉钉集成），代表了 Agent 通信模型中的核心缺陷。该 Issue 今日被关闭，表明维护者已修复此严重问题，值得关注其修复方案。

## 5. Bug 与稳定性

今日报告的 Bug 较多，按严重程度排列如下：

- **严重 - 配置明文写入风险 (#4421)**：Channel 配置（如 Token、Secret）以明文形式写入 Agent 可读的工作目录，存在信息泄露风险。**已有 PR #4409 进行关联的备份加固，但根因需进一步修复。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4421)
- **严重 - Agent 身份混淆 (#3957)**：主控 Agent 通过钉钉频道接收消息时工作空间被错误切换。**已关闭，表示已修复。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/3957)
- **中 - `write_file()` 死循环报错 (#4299)**：输出内容较长时循环报错。**已有 PR #4417 从模型配置角度缓解此问题，但根因定位仍需跟进。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4299)
- **中 - MiMo 思考模式+工具调用冲突 (#4314)**：开启 MiMo 模型思考模式后，多轮对话中涉及工具调用会报 400 错误。**已关闭。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4314)
- **中 - 浏览器 CDP 模式在 Ubuntu 26.04 下超时 (#4360)**：`browser_use.start()` 的 CDP 模式在特定系统环境下持续超时。**已关闭，可能在今日合并的 PR #4362 等中被附带修复。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4360)
- **中 - 浏览器 CDP 超时导致 Agent 无响应 (#4309)**：CDP 端口不可用时 Agent 会卡死 5 分钟，缺乏超时处理。**已关闭。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4309)
- **低 - chromadb Rust 绑定段错误 (#3854)**：`chromadb` 的原生库段错误会直接杀死整个进程，缺乏优雅的降级处理。**仍为 OPEN 状态，需持续关注。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/3854)
- **低 - 更新后 embedding 配置被重置 (#4018)**：`qwenpaw update` 后向量搜索配置丢失。**已关闭。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4018)

## 6. 功能请求与路线图信号

今日涌现多个有价值的功能请求，暗示了项目的未来发展方向：

- **插件生态发现与安装 (#4406)**：用户 `ekzhu` 提出希望能在产品内直接发现和安装官方内置插件（如 `cloudpaw`），提升用户体验。结合已合并的 #4418 和 #4423，**项目可能正在走向“插件市场”模式，这将是下个版本的重要特性。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4406)
- **工作目录整洁化 (#4408)**：用户 `verup` 建议将项目的默认配置文件统一放到 `.qwenpaw` 文件夹中，以保持工作目录的整洁。这反映了用户对**项目管理体验**的更高要求。 [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4408)
- **链路追踪机制 (#4114)**：用户 `ysj2018` 询问项目是否具备或计划实现链路追踪能力。对于构建复杂、多步执行的 Agent 应用，运维监控能力是成熟度的关键标志。 [Issue](https://github.com/agentscope-ai/QwenPaw/issues/4114)
- **钉钉群聊读取引用消息 (#3109)**：用户希望 Agent 能读取钉钉群聊中被引用的消息内容，这是一个针对特定渠道的精细功能需求，能显著增强钉钉集成的实用性。 **该问题已开放超过一个月，建议维护团队评估其优先级。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/3109)
- **支持可配置的基础路径 (#1853)**：当项目被部署在反向代理的子路径下时，前端和后端路由出现问题。该需求已开放数月，是影响企业级部署的关键问题。 **[信号不强] 建议在 1.2 版本规划中评估。** [Issue](https://github.com/agentscope-ai/QwenPaw/issues/1853)

## 7. 用户反馈摘要

从今日的 Issues 中，可以提炼出以下真实用户反馈：

- **“使用体验尚可，但特定场景下 Bug 很烦”**：用户 `danielhansaiday` 反馈在 Ubuntu 26.04 下 CDP 模式 20 多次测试全部失败，显示特定环境下的兼容性问题。用户 `wellhi` 和 `mqqss` 报告的 `write_file` 和 MiMo 问题也反映了类似痛点。
- **“安全是我们的底裤”**：用户 `Real-Simplicity` 报告了配置明文写入的安全风险，语气严肃。这表明随着项目应用场景深入，用户对安全性的敏感度正在提升。
- **“我们想要一个更像 IDE 的体验”**：用户 `verup` 提出工作目录整洁化的建议，用户 `ekzhu` 提出插件管理需求，都指向用户希望 CoPaw 能提供更规范、更易管理的项目结构和扩展系统，类似于成熟的开发平台。
- **“希望能顺利整合到我正在用的服务中”**：用户 `xy-xiong-bear` 和 `JunpengMa` 分别咨询企业微信和 QQ 的配置问题，用户 `JobJobovich` 报告了 Telegram 对语音消息的不支持。这表明跨平台渠道的**易用性和功能性**是用户采纳的关键因素。

## 8. 待处理积压

以下是一些长期未响应的重要 Issue 或 PR，建议维护团队关注：

- **Issue #1516：Telegram 频道不支持 AudioContent（已存在 2 个月）**：严重影响 Telegram 用户的语音消息交互体验。**已有用户提供了详细的 Bug 复现路径和截图中可能的修复方向，建议安排开发资源。** [链接](https://github.com/agentscope-ai/QwenPaw/issues/1516)
- **Issue #2751：`send_file_to_user` 后 Anthropic API 报错（已存在 1.5 个月）**：影响使用 Anthropic 模型用户的功能完整性。 **这是一个跨模型的问题，可能导致工具链断裂。** [链接](https://github.com/agentscope-ai/QwenPaw/issues/2751)
- **Issue #3854：chromadb Rust binding 段错误 (SIGSEGV) 杀死进程（已存在 18 天）**：这是一个严重的崩溃问题，可能因为使用频率较低而被忽视。**建议将其列为更高优先级，或至少给出一个临时解决方案（如优雅降级至纯 Python 实现）。** [链接](https://github.com/agentscope-ai/QwenPaw/issues/3854)
- **Issue #3178：Session 列表损坏导致 500 错误（已存在 1 个月）**：用户报告 `chats.json` 文件损坏会导致后端 500 错误，且缺乏备份和校验机制。**这关系到数据持久化和系统健壮性，建议添加相关防御逻辑。** [链接](https://github.com/agentscope-ai/QwenPaw/issues/3178)
- **Issue #3259：模型检测错误分类（已存在 1 个月）**：将 `glm-4.6v-flash` 模型错误识别为纯文本模型，导致用户无法使用其多模态能力。**这是一个影响模型配置准确性的 Bug。** [链接](https://github.com/agentscope-ai/QwenPaw/issues/3259)

---
*数据生成于：2026-05-15 | 数据源：GitHub*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我根据您提供的 ZeroClaw 项目数据，为您呈上 2026 年 5 月 15 日的项目动态日报。

---

# ZeroClaw 项目动态日报 | 2026-05-15

## 今日速览

ZeroClaw 项目今日处于高度活跃的开发状态，社区参与度极高。 **过去24小时内，项目共产生了31条Issue和50条PR的更新，其中待合并的PR数量（35条）远超已合并/关闭的数量（15条），显示出维护者和贡献者正在积极处理大量待办事项。**  尽管没有新版本发布，但多个高优先级（P1）的 Bug 被快速关闭，同时针对技能系统、运行时和可观测性等核心领域提出了大量增强请求（`enhancement`）。 **项目整体呈现“高问题涌入、高解决效率、同时伴生大量新功能需求”的繁荣态势。**  值得关注的是，关于 Cron 任务和 Telegram 频道的 Bug 修复和新功能请求同时涌现，成为今日的社区热点。

## 版本发布

-  **无。**  过去24小时内无新版本发布。

## 项目进展

在过去24小时内，项目在稳定性和功能完善方面取得了一定进展，主要体现在以下几个关键 PR 的合并：

- **技能系统审计与安全：**  PR [#5952](https://github.com/zeroclaw-labs/zeroclaw/pull/5952) (由 RyanHoldren 合并) 被合并，该 PR 将技能审计（`audit`）的范围限定为结构性检查，并将命令内容安全的责任委托给运行时策略，这是一个重要的架构决策。对应 Issue [#5956](https://github.com/zeroclaw-labs/zeroclaw/issues/5956) 也随之关闭。
- **Cron 功能优化与修复：** 贡献者 `drbparadise` 表现活跃，合并了多个 Cron 相关的 PR：
    - PR [#6656](https://github.com/zeroclaw-labs/zeroclaw/pull/6656): 优化了 Cron 运行结果的持久化性能，将其放入单次 SQL 事务中。
    - PR [#6655](https://github.com/zeroclaw-labs/zeroclaw/pull/6655): 修复了 Cron 的只读查询操作不会错误地触发数据库初始化路径的问题，对应 Issue [#6654](https://github.com/zeroclaw-labs/zeroclaw/issues/6654) 随之关闭。
    - PR [#6525](https://github.com/zeroclaw-labs/zeroclaw/pull/6525): 修复了 Matrix 频道中根时间线消息被错误地视为线程的问题。
- **运行时稳定性修复：** PR [#6552](https://github.com/zeroclaw-labs/zeroclaw/pull/6552) (由 drbparadise 合并) 修复了系统消息在聊天历史中位置错乱的问题，确保其始终位于对话头部。
- **安全依赖更新：** CI 发现了一个依赖漏洞，Issue [#6657](https://github.com/zeroclaw-labs/zeroclaw/issues/6657) 已被关闭，表明项目对安全问题的响应迅速。

总体来看，**项目在 Cron 调度、技能审计和运行时消息处理这三个关键环节上取得了实质性进展，提升了系统的稳定性和可预测性。**

## 社区热点

今日最受关注的是高严重性 Bug 的集中反馈，特别是与 Cron 和 Telegram 频道相关的问题。讨论焦点并非单个 PR，而是围绕特定功能模块的集体性问题。

- **1. [Bug]: Cron Job Output Not Routed to Configured Channels / Tool Execution Not Firing via Telegram**
    - **Issue [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647)** (4条评论) 和 **Issue [#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646)** (1条评论) 共同反映了一个核心痛点：在 Telegram 频道中，Cron 任务和网络搜索工具的执行结果无法正确路由到用户界面。用户 `icemann521` 描述为“S1 - workflow blocked”（工作流阻塞），严重影响了核心功能。
    - **诉求分析：** 社区用户期待 ZeroClaw 作为一个“AI助手”，能在其配置的目标频道（如 Telegram）中提供一个完整的交互闭环。目前的 Bug 打破了这一闭环，使得结果只能通过 Web 仪表盘查看，降低了实时性和易用性。这暴露出 `runtime` 层在处理不同频道（特别是 Telegram）的消息路由和工具调用反馈时存在缺陷。

- **2. [Bug]: Agent Doesn't Have Context of the Cron Job It's Run**
    - **Issue [#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105)** (2条评论) 指出了 Cron 功能的另一个逻辑问题：即使任务成功执行，触发该任务的 Agent 也无法访问该任务自身的上下文（如触发的消息）。
    - **诉求分析：** 用户 `radther` 提出了一个高级场景：Agent 应该能在 Cron 任务执行后，基于任务本身的上下文做出响应。例如，Agent 发送了一条提醒消息，它应当知道这个提醒是什么。目前的实现割裂了任务执行和 AI 感知，限制了 Cron 功能的智能化潜力。

## Bug 与稳定性

今日报告的 Bug 严重程度较高，主要集中在运行时核心功能。

| 严重程度 | Issue 链接 | 描述 | 是否有 Fix PR |
| :--- | :--- | :--- | :--- |
| **S1 - 工作流阻塞** | [#6647](https://github.com/zeroclaw-labs/zeroclaw/issues/6647) | Cron 任务输出无法路由到已配置的频道 (如 Telegram) | 否 |
| **S1 - 工作流阻塞** | [#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646) | 通过 Telegram 频道使用 `web_search_tool` 和 `web_fetch` 时失败 | 否 |
| **S0 - 数据丢失/安全风险** | [#6672](https://github.com/zeroclaw-labs/zeroclaw/issues/6672) | 在小米思维模型 (mimo-v2.5) 的 Tool-Call 循环中，`reasoning_content` 未回传给后续轮次 | 否 |
| **S2 - 降级行为** | [#6105](https://github.com/zeroclaw-labs/zeroclaw/issues/6105) | Agent 执行 Cron 任务时缺乏自身任务的上下文 | 否 |
| **S2 - 降级行为** | [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) | `web_fetch` 的 `allowed_private_hosts` 配置对解析为私有IP的域名失效 | 否 |
| **S2 - 降级行为** | [#6651](https://github.com/zeroclaw-labs/zeroclaw/issues/6651) | Matrix 频道在 `/admin/reload` 后内存泄漏约 1 MB Pss | 否 |

**值得注意的是，所有 S1 级别的 Bug 目前均无修复性 PR。** 这表明项目团队可能还在评估影响范围或寻找最佳解决方案，社区需持续关注。

**已修复的 Bug：**
- [Resolved] PR [#6655](https://github.com/zeroclaw-labs/zeroclaw/pull/6655) 已修复 Cron 数据库写路径误入只读操作的问题 (Issue [#6654](https://github.com/zeroclaw-labs/zeroclaw/issues/6654))。
- [Resolved] 依赖安全警报 (Issue [#6657](https://github.com/zeroclaw-labs/zeroclaw/issues/6657)) 已在 CI 中被标记为已关闭。

## 功能请求与路线图信号

今日涌现了大量新功能请求，与项目现有 PR 形成呼应，暗示了 v0.7.6 或后续版本的发展方向。

- **技能系统 (Skills) 成熟化：** 这是今日信号最强的方向。
    - **诊断先行：** Issue [#6645](https://github.com/zeroclaw-labs/zeroclaw/issues/6645) 指出 `SkillImprover` 工具无法处理 `manifest.toml` 格式的技能。
    - **修复跟进：** PR [#6674](https://github.com/zeroclaw-labs/zeroclaw/pull/6674) 和 Issue [#6670](https://github.com/zeroclaw-labs/zeroclaw/issues/6670) 计划将技能安装输出本地化，PR [#6676](https://github.com/zeroclaw-labs/zeroclaw/pull/6676) 则旨在为 Agent 添加“建议缺失技能”的能力。
    - **路线图信号：** 这与 **v0.7.6 的主题“改进技能支持与UX”** (Issue [#6253](https://github.com/zeroclaw-labs/zeroclaw/issues/6253)) 高度一致，**技能系统正从一个基础功能向更完善、更友好、更智能的生态系统演进。** PR [#6054](https://github.com/zeroclaw-labs/zeroclaw/pull/6054) 尝试从技能配置文件中读取超时参数，进一步印证了技能系统的精细化。

- **可观测性 (Observability) 增强：** 由贡献者 `JordanTheJet` 和 `Audacity88` 提出的多个 Issue（[#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641), [#6642](https://github.com/zeroclaw-labs/zeroclaw/issues/6642), [#6669](https://github.com/zeroclaw-labs/zeroclaw/issues/6669)）和已存在的 PR [#5652](https://github.com/zeroclaw-labs/zeroclaw/pull/5652) 都指向了 **OpenTelemetry (OTel) 和 Prometheus 的深度集成**。这预示着项目将为开发者提供更强大的调试和运营能力。

- **工具链与API扩展：**
    - **通知推送 API：** Issue [#6659](https://github.com/zeroclaw-labs/zeroclaw/issues/6659) 请求一个将通知推送到操作者网关会话的公开 API，这对构建外部集成非常关键。
    - **严格工具解析：** PR [#6675](https://github.com/zeroclaw-labs/zeroclaw/pull/6675) 引入了 `strict_tool_parsing` 配置，可要求使用原生 Provider 工具调用，减少解析错误，这标志 ZeroClaw 在与 Provider 的兼容性上走向成熟。
    - **SearXNG / 网络搜索改进：** Issue [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) 提议支持 SearXNG 搜索引擎并提升网络搜索的稳健性，该 Issue 已存在近一个月，社区维护者可能需要回应。

## 用户反馈摘要

从今日的 Issue 评论中，我们可以提炼出以下真实用户痛点：

1.  **配置与预期的偏差：**
    - 用户 `hirscr` 报告 [#6229](https://github.com/zeroclaw-labs/zeroclaw/issues/6229)，在 Telegram 群组中设置 `mention_only=true` 后，机器人仍然会响应图片/媒体消息。**这表明配置逻辑存在边界情况，未完全覆盖用户期望的“仅 @提及 才响应”**。
    - 用户 `icemann521` 报告 [#6646](https://github.com/zeroclaw-labs/zeroclaw/issues/6646)，使用 LM Studio 的 OpenAI 兼容模式时，通过 Telegram 频道无法触发网络搜索和抓取工具，**说明在特定 Provider+Model 组合下，工具调用与频道的集成存在兼容性问题。**

2.  **通用性与兼容性挑战：**
    - 用户 `allenmagic` 报告 [#6658](https://github.com/zeroclaw-labs/zeroclaw/issues/6658)，在 aarch64 架构的 Alpine Linux（使用 musl libc）上安装时，安装脚本下载了错误的 glibc 版本。**这表明项目的跨平台安装体验仍需打磨，以支持更广泛的非标准 Linux 发行版。**
    - 用户 `KundKMC` 报告 [#6678](https://github.com/zeroclaw-labs/zeroclaw/issues/6678)，当加载自定义 Shell 技能时，工具名生成违反 Anthropic API 的命名规范（`^[a-zA-Z0-9_-]{1,128}$`），导致请求失败。**这暴露了技能工具命名模块与特定 Provider（如 Anthropic）API 约束之间的严格兼容性问题。**

## 待处理积压

以下 Issue 和 PR 长期未得到明确处理或响应，提醒维护者及社区关注：

- **超高关注的老 Bug：** Issue [#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) “web_fetch allowed_private_hosts list is essentially useless...” 创建于 3 月 29 日，至今已超过一个半月且无进展，被标记为 `status:no-stale`。这涉及一个重要的安全配置缺陷。
- **阻塞的功能请求：**
    - Issue [#5833](https://github.com/zeroclaw-labs/zeroclaw/issues/5833) “session ownership model for destructive operations” (创建于 4月17日) 和 Issue [#5316](https://github.com/zeroclaw-labs/zeroclaw/issues/5316) “Propose SearXNG search support...” (创建于 4月5日) 均处于 `needs-maintainer-review` 状态，等待维护者的决策反馈。这两者对 Agent 安全性和工具生态扩展至关重要。
- **等待与更新：** 大型 PR [#5652](https://github.com/zeroclaw-labs/zeroclaw/pull/5652) “feat(provider): add native extended thinking...” 自 4月11日开启以来，作为一个 XL 大小的特性 PR，其进展缓慢。鉴于其对推理能力的重要性，社区应关注其动态。

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*