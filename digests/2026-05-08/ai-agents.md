# OpenClaw 生态日报 2026-05-08

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-05-08 06:18 UTC

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

# OpenClaw 项目动态日报 | 2026-05-08

---

## 1️⃣ 今日速览

过去 24 小时，OpenClaw 项目保持极高活跃度：共产生 500 条 Issues 更新、500 条 Pull Requests 更新，并发布了 **v2026.5.7** 补丁版本。社区反馈集中在北京时间 5 月 7–8 日测试版 (2026.5.5/6) 暴露的多项回归问题，特别是 Gateway 稳定性、Doctor 迁移破坏、WebSocket 连接中断等。修复 PR 快速跟进，当日即有多个高优先级 Bug 被关闭，项目整体呈现“高产出 + 高关注”的健康态势，但稳定性欠佳仍需维护侧迅速收敛。

| 指标 | 数值 |
|------|------|
| Issues 更新总数 | **500**（新开/活跃 266，已关闭 234） |
| PR 更新总数 | **500**（待合并 332，已合并/关闭 168） |
| 新版本发布 | **1**（v2026.5.7） |
| 最热 Issue 评论数 | **21**（#77668） |
| 最热 PR 评论数 | -（评论数未提供，但多数 PR 无评论） |

---

## 2️⃣ 版本发布

### v2026.5.7（2026-05-07 发布）

**更新内容**  
- 修复 ClawHub CLI 依赖安装的短暂失败导致插件发布失败的问题，并增加自动重试。
- 当某个预览单元格环境偶发异常时，若该插件此前已通过预览，仍允许发布（不再因单点失败而阻塞发布流程）。
- 发布后主动验证每个期望的 ClawHub 包版本，加快维护版本恢复速度，降低误报风险。

**破坏性变更**  
无破坏性变更。仅影响插件发布流水线（维护者 & CI）。

**迁移注意事项**  
- 插件维护者无需手动操作，但建议在 CI 中更新至 v2026.5.7 以获得更稳健的发布流程。
- 若使用自定义发布脚本，注意命令行重试逻辑可能改变退出码行为，建议更新后做一次全量测试。

---

## 3️⃣ 项目进展

### 当日合并/关闭的重要 PR

| PR | 标题 | 影响 |
|----|------|------|
| [#78679](https://github.com/openclaw/openclaw/pull/78679) `CLOSED` | fix: recognize PI native API provider streams in embedded session stream resolution | 修复嵌入会话流分辨率中 PI 原生 API 提供者流被跳过导致的 token 用量报告为零的回归。 |
| [#79278](https://github.com/openclaw/openclaw/pull/79278) `CLOSED` | perf(status): eliminate duplicate bundled-plugin manifest scans in status --json | `status --json` 调用性能优化，消除两次重复的插件清单扫描，加快命令响应。 |
| [#54606](https://github.com/openclaw/openclaw/pull/54606) `CLOSED` | Followup runner: thread followups using current message | 确保 followup 消息携带原始消息 ID，修复 compaction 通知中回复线程丢失的问题。 |
| [#48971](https://github.com/openclaw/openclaw/pull/48971) `CLOSED` | fix(media): harden MIME type sanitization | 增强 MIME 类型消毒，拒绝尾随垃圾字符，防止参数化恶意输入。 |
| [#78780](https://github.com/openclaw/openclaw/pull/78780) `CLOSED` | Harden browser download output writes | 将浏览器下载路径路由到安全输出写入器，防止符号链接目录输出，提升文件安全。 |
| [#79238](https://github.com/openclaw/openclaw/pull/79238) `OPEN` (进展中) | Keep OpenAI Codex migrations on automatic runtime routing | 重新设计 `openai-codex/*` 迁移逻辑，防止将整个 agent 级别 pin 到 Codex 导致混合提供者变脆弱。 |

**整体进展**：当日至少关闭 6 个中/高影响的 PR，涵盖流分辨率、性能、安全、MIME 消毒等。社区对回归问题的响应速度较快，其中 #78679 直接解决用户报告的 token 用量丢失问题。

---

## 4️⃣ 社区热点

### 评论数 Top 5 Issues

| # | Issue | 评论 | 核心诉求 / 问题 |
|---|-------|------|----------------|
| 1 | [#77668](https://github.com/openclaw/openclaw/issues/77668) `CLOSED` | 21 | **Discord Gateway 挂起**：macOS 上 Carbon 客户端重启后停在 "awaiting gateway readiness"，永不触发 READY。累计 6 个重复问题，用户调查定位到 Carbon 客户端生命周期。 |
| 2 | [#12590](https://github.com/openclaw/openclaw/issues/12590) `OPEN` | 19 | **memoryFlush 不可靠**：memoryFlush 仅在每次交替压缩周期触发，去重逻辑 `shouldRunMemoryFlush` 与 `runMemoryFlushIfNeeded` 互斥条件错误，导致自动压缩时丢失一半刷新。 |
| 3 | [#78407](https://github.com/openclaw/openclaw/issues/78407) `CLOSED` | 16 | **Doctor 重写模型引用锁定用户**：`doctor --fix` 在升级时将所有 `openai-codex/*` 重写为 `openai/*`，导致 ChatGPT OAuth 用户无法使用。已有 PR #79238 解决。 |
| 4 | [#65824](https://github.com/openclaw/openclaw/issues/65824) `CLOSED` | 15 | **11 项平台差距功能捆绑**：重度用户 @smonett 提交了 11 个功能诉求，涵盖日常使用的多个痛点，虽已关闭但作为 meta issue 被关注。 |
| 5 | [#12602](https://github.com/openclaw/openclaw/issues/12602) `OPEN` | 13 | **Slack Block Kit 支持**：要求 agent 可发送富交互的 Block Kit 消息，当前仅支持纯文本 markdown。用户列举了 CRM 摘要、数据库查询等场景。 |

**分析**：Top 5 中 4 个为 Bug/回归，反映社区在当前版本中遇到的稳定性问题；Slack Block Kit 功能请求长期未关闭，说明社区对交互增强有持续刚需。讨论热度表明用户对 Core 体验（Gateway、内存、回复交付）极其敏感。

---

## 5️⃣ Bug 与稳定性

按严重程度排列（Critical 优先，标注是否有 Fix PR）。

### 🔴 Critical / Blocker

| Issue | 问题 | 严重性 | Fix PR |
|-------|------|--------|--------|
| [#77668](https://github.com/openclaw/openclaw/issues/77668) | Discord Gateway 挂起，macOS Carbon 客户端不 READY | 🔴 阻塞大量用户 | `CLOSED` 但未关联 PR（可能标记重复或已在 v2026.5.7 修复） |
| [#78407](https://github.com/openclaw/openclaw/issues/78407) | Doctor 重写模型引用，锁定 ChatGPT OAuth 用户 | 🔴 用户无法使用 | PR [#79238](https://github.com/openclaw/openclaw/pull/79238) 已提交 |
| [#78402](https://github.com/openclaw/openclaw/issues/78402) | Gateway 反复关闭连接 (1000/1005/1006) → 事件循环饥饿 | 🔴 导致 UI 断连 | `CLOSED` 关联 #78601 |
| [#78601](https://github.com/openclaw/openclaw/issues/78601) | Gateway liveness 看门狗每几分钟重启一次 (事件循环冻结 23s) | 🔴 持续重启 | `CLOSED`（疑似已修复在 v2026.5.7） |

### 🟠 High

| Issue | 问题 | 严重性 | Fix PR |
|-------|------|--------|--------|
| [#12590](https://github.com/openclaw/openclaw/issues/12590) | memoryFlush 只工作一半压缩周期 | 🟠 内存管理不可靠 | 无（OPEN 超过 3 个月） |
| [#76990](https://github.com/openclaw/openclaw/issues/76990) | 成功回复未写入活跃会话转录，导致后续重新回答旧问题 | 🟠 UI/UX 数据不一致 | 无 |
| [#76562](https://github.com/openclaw/openclaw/issues/76562) | CPU 100%、控制平面 RPC 延迟、轮询不稳定（升级后） | 🟠 性能退化 | 无 |
| [#76315](https://github.com/openclaw/openclaw/issues/76315) | Linux 下 subagent 负载导致 Gateway 不稳定，WhatsApp 408 断开 | 🟠 平台特定 | 无 |
| [#77374](https://github.com/openclaw/openclaw/issues/77374) | Control UI 中每次新消息后前一条助手回复消失 | 🟠 界面误导 | `CLOSED` 可能已修复在 v2026.5.7 |

### 🟡 Medium

| Issue | 问题 | 严重性 | Fix PR |
|-------|------|--------|--------|
| [#78502](https://github.com/openclaw/openclaw/issues/78502) | Google Gemini 模型在主线会话超时，子代理正常 | 🟡 限模型 | 无 |
| [#77525](https://github.com/openclaw/openclaw/issues/77525) | /status 显示 `?/1.0m` 对于 xAI Grok 模型 | 🟡 信息缺失 | `CLOSED` |
| [#77908](https://github.com/openclaw/openclaw/issues/77908) | 非主 agent 回复在 WebUI 可见但不回送 Telegram/Discord | 🟡 渠道回复丢失 | `CLOSED` 可能已修复 |
| [#78846](https://github.com/openclaw/openclaw/issues/78846) | Mistral 回复中出现 `[object Object]` 垃圾内容 | 🟡 输出异常 | `CLOSED` 快速确认并关闭 |

**总结**：当日修复的回归问题较多（#77668、#78407、#78402、#78601 等均已关闭），但仍有多个长期 Bug（#12590、#76562、#76315）处于 OPEN，且缺乏维护者响应。稳定性指标在 v2026.5.5/5.6 出现明显劣化，v2026.5.7 应为此紧急修复。

---

## 6️⃣ 功能请求与路线图信号

### 候选纳入下一版本的功能

| Issue | Feature | 点赞 | 对应 PR / 信号 |
|-------|---------|------|----------------|
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets 防止 agent 访问原始 API Key | 👍4 | 无直接 PR，但安全团队持续关注 |
| [#12602](https://github.com/openclaw/openclaw/issues/12602) | Slack Block Kit 支持 | 👍0 | 社区多篇讨论，但无实质开发 |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | Pre-response enforcement hooks (硬门控) | 👍2 | 金融/安全用例强烈要求 |
| [#13616](https://github.com/openclaw/openclaw/issues/13616) | 备份/恢复工具 | 👍0 | 企业部署需求 |
| [#13700](https://github.com/openclaw/openclaw/issues/13700) | Session 快照 (save/load checkpoint) | 👍0 | 研发调试场景 |
| [#48874](https://github.com/openclaw/openclaw/issues/48874) | 多会话架构 (共享LLM+隔离会话+知识库) | 👍0 | RFC 阶段 |
| [#45839](https://github.com/openclaw/openclaw/issues/45839) | Telegram inline buttons 审批 | 👍0 | 配对审批需求常见 |
| [#13219](https://github.com/openclaw/openclaw/issues/13219) | 按模型用量日志 (成本追踪) | 👍1 | 运营用户呼声较高 |
| [#13337](https://github.com/openclaw/openclaw/issues/13337) | Voice Call Plugin: Vapi 提供商 | 👍0 | 开放任务声明，有贡献者认领 |
| [#17840](https://github.com/openclaw/openclaw/issues/17840) | 反应触发 agent 轮次 (opt-in) | 👍0 | 交互模式扩展 |

**路线图信号**：开发者团队近期优先聚焦于 **Codex 迁移自动化**（PR #79238）和 **插件发布可靠**（v2026.5.7），功能请求方面的进展不明显。但社区对 **安全（Masked Secrets）**、**成本跟踪**、**Slack 交互** 的需求旺盛，若下一版本能纳入其中 1–2 项将显著提升用户满意度。

---

## 7️⃣ 用户反馈摘要

### 真实用户痛点

> **“Discord gateway hangs silently on macOS after restart. No error, no timeout, just stuck.”**  
> —— @RyanSandoval（#77668）  
> 痛点：关键渠道无法恢复，影响日常使用，且缺乏诊断信息。

> **“After updating from 2026.5.4 to 2026.5.5, doctor --fix rewrote all openai-codex/* refs to openai/*, locking out our ChatGPT OAuth users.”**  
> —— @100yenadmin（#78407）  
> 痛点：自动迁移破坏现有配置，导致部分用户完全不可用，且无回滚提示。

> **“memoryFlush only fires every other compaction cycle. Our agents accumulate stale memories until a manual restart.”**  
> —— @dial481（#12590）  
> 痛点：自动化记忆管理形同虚设，长期运行后性能劣化。

> **“Successful assistant reply is visible in run trajectory but missing from transcript. Next turn ignores it and re-answers old prompt.”**  
> —— @Jackten（#76990）  
> 痛点：会话历史不完整导致重复回答、信息混乱。

### 用户满意点（从评论间接观察）
- 社区对 PR #79238 的 Codex 迁移重新设计表示期待（用户指出“Thanks for fixing the unintended side effect”）。
- v2026.5.7 发布后，多个 Gateway 重启循环问题用户报告已关闭，说明紧急补丁有效。

### 使用场景提及
- 企业用户强烈要求 **审批门控**、**成本追踪** 和 **AWS 部署指南**。
- 开发者希望 **Session 快照** 以便进行 A/B 测试不同模型/提示语。
- 量化/金融团队要求 **Pre-response enforcement hooks** 以防止 agent 绕过工具调用直接回答。

---

## 8️⃣ 待处理积压

### 长期未响应的关键 Issue

| Issue | 日期 | 评论 | 状态 | 说明 |
|-------|------|------|------|------|
| [#12590](https://github.com/openclaw/openclaw/issues/12590) | 2026-02-09 | 19 | OPEN | memoryFlush 不可靠，3 个月无修复，影响所有自动压缩用户。 |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | 12 | OPEN | Masked Secrets 需求明确，4 个点赞，但无 PR 或维护者表态。 |
| [#76562](https://github.com/openclaw/openclaw/issues/76562) | 2026-05-03 | 7 | OPEN | 升级后 CPU 100%、RPC 延迟、轮询不稳，4 个点赞，未分配。 |
| [#76315](https://github.com/openclaw/openclaw/issues/76315) | 2026-05-02 | 6 | OPEN | Linux 下 subagent 负载导致 WhatsApp 断开，1 个点赞。 |
| [#74334](https://github.com/openclaw/openclaw/issues/74334) | 2026-04-29 | 5 | OPEN | Snippet 规范化错误导致 promotion 静默失败。 |

### 长期未合入的 PR

| PR | 日期 | 最后更新 | 说明 |
|----|------|----------|------|
| [#69310](https://github.com/openclaw/openclaw/pull/69310) | 2026-04-20 | 5月8日 | Fix: surface dropped media to users instead of silently swallowing（增加用户可见性，但未合并）。 |
| [#69312](https://github.com/openclaw/openclaw/pull/69312) | 2026-04-20 | 5月8日 | Fix: prevent MEDIA false-positive extraction from indented code blocks（防止代码块误匹配，仍 open）。 |
| [#58808](https://github.com/openclaw/openclaw/pull/58808) | 2026-04-01 | 5月8日 | Feat: pass requesterSenderId and senderIsOwner to ChannelAgentToolFactory（增强权限控制，长期搁置）。 |
| [#74974](https://github.com/openclaw/openclaw/pull/74974) | 2026-04-30 | 5月8日 | Fix: tolerate Paperclip metadata on agent invocation payloads（外部 agent 兼容性修复）。 |

**呼吁**：上述积压项涉及安全性、数据完整性、性能退化等核心问题，建议维护团队在下一迭代周会中评估优先级并分配处理。

---

*报告生成于 2026-05-08，基于 OpenClaw 公开 GitHub 数据。*

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告（2026-05-08）

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于 **高速迭代与分化并行** 的阶段。以 OpenClaw 为代表的旗舰项目日处理 Issue/PR 均超 500 条，社区反馈爆发式增长，但稳定性问题（Gateway 挂起、迁移破坏、会话丢失）频繁暴露，反映出“功能快速堆叠”与“质量收敛”之间的矛盾。与此同时，NanoClaw、PicoClaw、ZeroClaw 等中坚项目在特定方向（A2A 路由、渠道兼容、桌面体验）持续深耕，社区活跃度稳中有升。Hermes Agent、IronClaw 则凭借大版本重构（v0.13.0、v0.28.0）展现对架构卓越的追求。整体呈现 **头部拥挤、腰部加速、尾部静默** 的格局，生态复杂度与成熟度同步提升。

## 2. 各项目活跃度对比

| 项目名称 | Issues 更新数 | PR 更新数 | 新版本发布 | 健康度评估 |
|---------|-------------|----------|-----------|-----------|
| **OpenClaw** | 500 | 500 | v2026.5.7 | ⚠️ 极高活跃，但回归 Bug 集中，紧急补丁频繁 |
| **NanoBot** | 9 | 20 | 无 | ✅ 稳定修复，社区反馈集中（WebSocket、DeepSeek） |
| **Hermes Agent** | 50 | 50 | v0.13.0 | 🔥 大版本后活跃度飙升，macOS 兼容性成短板 |
| **PicoClaw** | 33 | 48 | nightly | ✅ 修复效率高，多 Agent 发现 PR 推进中 |
| **NanoClaw** | 9 | 35 | 无 | ✅ 合并率 63%，A2A 路由是核心修复方向 |
| **NullClaw** | 2（关闭） | 5（合并） | 无 | ✅ 小步快跑，ACP 原生集成是亮点 |
| **IronClaw** | 未明确 | 32（合并） | v0.28.0 | 🔥 架构重构里程碑，LLM 模块抽取为新 crate |
| **LobsterAI** | 2（热点） | 50（43 合并） | v2026.5.7 | ✅ 版本发布冲刺，UI 和用户体验改进密集 |
| **CoPaw** | 36 | 29 | 无 | ⚠️ 社区反馈活跃，内存泄漏 Bug 需紧急处理 |
| **Moltis** | 4（关闭） | 9（合并） | 2个内部版本 | ✅ 极高效率，24h 内完成身份验证、语音、图像功能 |
| **ZeroClaw** | 50 | 50 | v0.7.5 | ⚠️ 版本活跃但 S0/S1 Bug 较多，WhatsApp 协议兼容性中断 |

*注：TinyClaw、ZeptoClaw 过去 24 小时无活动，未计入。*

## 3. OpenClaw 在生态中的定位

**核心优势**：OpenClaw 是社区规模最大、Issue/PR 日均更新量远超其他项目的旗舰项目（约 500 条/日，而其他项目多在 30-50 条）。其插件生态（ClawHub CLI）、多平台集成（Discord/Telegram/微信）和 Pipeline 自动化（自动重试、版本验证）体现了企业级工程投入。

**技术路线差异**：OpenClaw 采用“插件+并发引擎”架构，注重可扩展性，但近期版本中回归问题频发（Gateway 稳定性、Doctor 迁移破坏），暗示快速迭代中测试覆盖不足。相比之下，IronClaw 选择“Reborn 架构重构”，从底层重写以追求长期健壮性；NanoClaw 则聚焦 A2A 路由细粒度控制。

**社区规模对比**：OpenClaw 的 Issue 评论热度（例如 #77668 达 21 条）远高于其他项目（多数在 6-10 条），且贡献者数量、第三方技能数量均为生态第一。但社区情绪存在“高期待 vs 低稳定性”的矛盾，用户对升级后配置被破坏（如 Doctor 重写模型引用）反应强烈。

**总结定位**：OpenClaw 是生态的“风向标”，其技术方案（如 MCP 工具审批、Kanban 调度）常被后续项目借鉴，但稳定性波动可能给其他项目留出差异化空间。

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|------|---------|----------|
| **Agent-to-Agent 路由（A2A）** | NanoClaw, OpenClaw, NullClaw (ACP) | 多 Agent 场景下回复路由错误、会话分裂、线程丢失 |
| **Provider 架构统一与兼容性** | ZeroClaw (#5937), IronClaw (#3387), OpenClaw (#79238) | 消除重复代码，统一模型配置入口，修复 Codex 迁移破坏 |
| **MCP 审批与权限控制** | OpenClaw (审批工具空操作), Hermes Agent (#21563), NanoClaw (#2340) | 工具调用权限管理、MCP 审批 IPC 打通、Bot 命令未授权 |
| **渠道消息一致性与稳定性** | PicoClaw (#2817), CoPaw (#4000), ZeroClaw (#6246) | 语音转文本后未传递、微信/WhatsApp 消息丢失、协议升级中断 |
| **用户体验（Onboarding 简化）** | ZeroClaw (浏览器内 Onboarding), LobsterAI (新手引导), CoPaw (#4036) | 配置文件向导、模型自动发现、跳过强制认证 |
| **记忆/上下文管理** | OpenClaw (#12590 memoryFlush), NanoBot (#3689 会话丢失), PicoClaw (#2721 竞争条件) | 持久化优化、中断恢复、压缩周期正确性 |

## 5. 差异化定位分析

| 维度 | OpenClaw | NanoBot | Hermes Agent | PicoClaw | NanoClaw | NullClaw | IronClaw | LobsterAI | CoPaw | Moltis | ZeroClaw |
|------|----------|---------|--------------|----------|----------|----------|----------|------------|-------|--------|----------|
| **功能侧重** | 全功能企业级 | 轻量部署 | Agent 坚韧性 | 硬件适配（Sipeed） | 多 Agent 路由 | 极致轻量 (Zig) | 大规模企业架构 | 中国用户（网易生态） | 多模态交互 | 去中心化身份 | 桌面+Web 双端 |
| **目标用户** | 开发者/运维 | 个人/小团队 | 高级开发者 | 嵌入式/边缘 | 社群运营 | 性能党 | 企业客户 | 教育/办公 | 多Agent协同 | 隐私/自托管 | 远程工作者 |
| **技术架构** | Golang+插件引擎 | Python+事件驱动 | 模块化（Kanban/MCP） | Go+CLI | 核心路由层 | Zig+ACP | Rust+WASM | TypeScript+Electron | Python+渠道 | Rust+WASM沙箱 | Rust+SQLite |
| **关键差异化** | 最大生态 | ? | ? | 硬件绑定 | ? | 非主流语言 | 企业重构 | 本地化集成 | 视觉+文件 | 节点互信 | 内置Onboarding |

## 6. 社区热度与成熟度

**🔥 快速迭代阶段（功能密集上线，Bug 修复并行）**  
- **OpenClaw**：日 Issue/PR 500+，版本发布频繁，但稳定性波动较大，属于“探索性增长”  
- **Hermes Agent**：v0.13.0 发布后贡献者涌入，P0/P1 Bug 快速修复  
- **ZeroClaw**：v0.7.5 涉及大量新功能，同时 S0/S1 Bug 集中暴露  
- **IronClaw**：Reborn 架构落地，日合并 32 个 PR，工程密度高  

**✅ 质量巩固阶段（修复已有问题，优化体验）**  
- **NanoBot**：WebSocket 修复、SSE 流式改进，社区 demand 以增强为主  
- **PicoClaw**：每日 48 个 PR，28 个合并，高频修复伴随新渠道集成  
- **NanoClaw**：A2A 路由持续修复，新技能有序添加  
- **LobsterAI**：版本冲刺中，修复流式字符、Windows 路径等细节  
- **Moltis**：极高效，24h 内实现多个核心功能，积压极少  

**🧊 静默/低活跃**  
- **TinyClaw**、**ZeptoClaw**：24h 无活动，可能处于维护期或开发停滞  

## 7. 值得关注的趋势信号

1. **多 Agent 协作从实验走向生产**：NanoClaw、NullClaw (ACP)、OpenClaw 均出现 A2A 路由相关 Bug 和 PR，说明跨 Agent 通信不再是概念验证，而是真实用户场景的痛点。

2. **Provider 架构去中心化与统一是刚需**：ZeroClaw、IronClaw、OpenClaw 三大项目不约而同重构 Provider 层（OpenAPI 3.1、独立 crate、统一凭证），暗示社区对模型提供商多样性和切换灵活性的要求日益刚性。

3. **安全与许可成为社区焦虑**：MCP 审批空操作（Hermes）、Bot 命令未授权执行（NanoClaw）、凭证继承漏洞（ZeroClaw）连续被报告，用户对“可控制的能力”的需求超过对“更多能力”的追求。

4. **Onboarding 体验决定留存**：ZeroClaw 推出浏览器内 Onboarding、LobsterAI 新增新手引导、CoPaw 用户抱怨“添加模型步骤太多”——降低首次使用门槛正在成为项目竞争力的关键差异化指标。

5. **本地化/轻量化趋势加速**：PicoClaw 面向嵌入式，NullClaw 用 Zig 追求极致性能，Moltis 强调本地 Whisper 等隐私优先方案——说明生态内部正在为不同场景（边缘、隐私、低资源）提供专业化选择，而非一味追求功能堆叠。

**对 AI 智能体开发者的启示**：建议优先关注 A2A 路由实现方案（可参考 NanoClaw #2267 的修复逻辑）、Provider 凭证管理最佳实践（避免 ZeroClaw #6418 类似漏洞），以及在集成新模型时强制加入回滚/恢复机制（参考 OpenClaw v2026.5.7 的发布重试设计）。生态正在从“能做什么”向“可靠地做什么”转变。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 (2026-05-08)

---

## 1. 今日速览

过去 24 小时项目保持较高活跃度：共处理 9 条 Issue 更新（新开/活跃 3 条，关闭 6 条）和 20 条 PR 更新（待合并 13 条，已合并/关闭 7 条）。社区重点关注 WebSocket 连接问题、DeepSeek 推理模式报错以及会话上下文持久化等方向。7 个 PR 被合并，涉及 onboard 向导输入修复、Dream 游标恢复、SSE 流式传输回退等改进，整体修复效率较高。暂无新版本发布。

---

## 3. 项目进展（今日合并/关闭的重要 PR）

今日共有 7 个 PR 被合并或关闭，主要集中在以下方面：

| PR | 说明 | 状态 |
|---|---|---|
| [#3691](https://github.com/HKUDS/nanobot/pull/3691) | 修复 onboard 向导中空字符串与假值无法在输入字段中处理的问题（cherry-pick 自 #3690） | 合并 |
| [#3690](https://github.com/HKUDS/nanobot/pull/3690) | 同样修复 onboard 输入处理的两个 bug（_input_text 将 “” 误转为 None，_input_multi_select 未正确处理假值） | 合并 |
| [#3221](https://github.com/HKUDS/nanobot/pull/3221) | 新增 `nanobot auth` 命令，支持 OAuth 设备流与 `--auth-key`，自动配置默认 provider/model，注册 gateway 提供者 | 合并 |
| [#3608](https://github.com/HKUDS/nanobot/pull/3608) | 为 Sen agent 添加本地设置文档（AGENTS.md、SEN_LOCAL_SETUP.md 及配置示例） | 合并 |
| [#3660](https://github.com/HKUDS/nanobot/pull/3660) | 修复 Dream 恢复时游标（cursor）未回滚的问题，新增回归测试 | 合并 |
| [#3677](https://github.com/HKUDS/nanobot/pull/3677) | 移除 HTTP 压缩缓冲区，恢复真正的 SSE 流式传输（修复批量输出问题） | 合并 |
| [#1835](https://github.com/HKUDS/nanobot/pull/1835) | 允许向后端 LLM 发送任意额外参数（如 Ollama 的 `stream: false`） | 合并 |

此外，[#3684](https://github.com/HKUDS/nanobot/pull/3684)（微信频道静默丢消息修复）等多个 PR 仍在排队等待合并。

---

## 4. 社区热点

- **#3682 [bug] websocket 导致的报错**（[链接](https://github.com/HKUDS/nanobot/issues/3682)）  
  用户 NewAlice 报告 gateway 因 WebSocket 握手失败报错，共 3 条评论。该 Issue 已在同日关闭，但引发了类似问题 #3683（WebSocket issue），表明该方向是当前部署的热点痛点。

- **#3650 [enhancement] 配置 bot 名称与图标**（[链接](https://github.com/HKUDS/nanobot/issues/3650)）  
  开放 2 天，获得 2 条评论。用户期望通过 `config.json` 自定义 AI 助手的显示名称和图标（替代默认的 “nanobot is thinking...” 和猫图标），反映出社区对品牌化/定制化界面的强烈需求。

- **#3689 [enhancement] 中断会话丢失上一轮聊天记录**（[链接](https://github.com/HKUDS/nanobot/issues/3689)）  
  今日新创建的 Issue（0 条评论），但问题场景具体：用户打断 nanobot 循环执行任务后，bot 丢失了之前的对话上下文，无法记住已执行的步骤。这关系到 Agent 会话持久性与中断恢复能力，可能成为近期开发重点。

---

## 5. Bug 与稳定性

以下为今日报告或关闭的 bug，按影响程度排列：

| 严重程度 | Issue | 描述 | 备注 |
|---|---|---|---|
| **高** | [#3682](https://github.com/HKUDS/nanobot/issues/3682) | WebSocket 握手失败导致 gateway 报错（`opening handshake failed`） | 已关闭，但同类问题 #3683 也存在 |
| **高** | [#3683](https://github.com/HKUDS/nanobot/issues/3683) | WebSocket 端口访问异常（Linux 部署，Windows/Mac 浏览器访问 8765 失败） | 已关闭 |
| **高** | [#3665](https://github.com/HKUDS/nanobot/issues/3665) | DeepSeek-v4-flash 在多次查询后报错 “reasoning_content must be passed back to the API” | 已关闭 |
| **中** | [#3681](https://github.com/HKUDS/nanobot/issues/3681) | LLM 调用超时（`timed out after 300s`），频繁出现 | 已关闭，可能与 LLM 服务有关 |
| **低** | [#3604](https://github.com/HKUDS/nanobot/issues/3604) | WhatsApp 语音消息无法下载 | 已关闭 |

**稳定性改进**：今日合并的 [#3677](https://github.com/HKUDS/nanobot/pull/3677) 修复了 SSE 流式传输被 HTTP 压缩缓冲区阻塞的问题，确保实时输出；[#3660](https://github.com/HKUDS/nanobot/pull/3660) 修复了 Dream 模块恢复时的数据不一致；[#3662](https://github.com/HKUDS/nanobot/pull/3662)（待合并）优化 token 估算避免网络加载，减少离线场景下的故障。

---

## 6. 功能请求与路线图信号

当前开放的多个增强请求表明社区对以下方向有较高期望：

| 功能 | Issue/PR | 状态 | 可能纳入版本 |
|---|---|---|---|
| 自定义 bot 名称与图标 | [#3650](https://github.com/HKUDS/nanobot/issues/3650) | Open，2 评论 | 高可能，配置化趋势 |
| 禁用 Dream 功能 | [#3652](https://github.com/HKUDS/nanobot/issues/3652) | Open，2 评论 | 较易实现（添加 `enabled` 标志） |
| Model Preset（快速切换模型组合） | [#3358](https://github.com/HKUDS/nanobot/pull/3358) | Open，已更新 | 高，已有实现但等待合并 |
| 统一语音转录 + 本地 Whisper 支持 | [#3513](https://github.com/HKUDS/nanobot/pull/3513) | Open | 增强语音通道稳定性 |
| 新消息通道：SimpleX | [#3486](https://github.com/HKUDS/nanobot/pull/3486) | Open | 扩展平台覆盖 |
| CLI 显示模型推理内容 | [#3655](https://github.com/HKUDS/nanobot/pull/3655) | Open | Agent 透明性需求 |
| 会话中断保留上下文 | [#3689](https://github.com/HKUDS/nanobot/issues/3689) | Open | 高优先级，Agent 核心体验 |

此外，PR [#3685](https://github.com/HKUDS/nanobot/pull/3685) 中提出的 `_last_summary` 持久化方案直接回应了会话上下文丢失问题，可能与 #3689 相辅相成。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提炼的关键用户声音：

- **部署稳定性**：多位用户（NewAlice, bigsinger）在 Linux 服务器上遇到 WebSocket 连接和 LLM 超时问题，表明生产环境下的网络/配置兼容性仍需加强。
- **配置灵活性**：用户 mraad 建议允许通过 `config.json` 自定义 bot 名称和图标，以适配品牌需求；skyline75489 希望能够完全禁用 Dream 功能，体现对模块化管理的需求。
- **会话体验**：用户 lyh161 反映在执行长任务时打断 bot 后，上下文丢失且 bot 无法恢复之前的步骤，影响实际使用。该问题在 PR [#3685](https://github.com/HKUDS/nanobot/pull/3685) 中已有修复方案（持久化 `_last_summary`）。
- **DeepSeek 兼容性**：用户 tomjuggler 报告 DeepSeek-v4-flash 在思维模式下必须回传 `reasoning_content`，否则报错，说明与特定模型 API 的适配存在缺口。

---

## 8. 待处理积压

以下为创建时间较早且仍处于开放状态的 PR/Issue，建议维护者关注：

| 编号 | 创建时间 | 标题 | 当前状态 |
|---|---|---|---|
| [#1219](https://github.com/HKUDS/nanobot/pull/1219) | 2026-02-26 | 股票市场分析增强（3 项技能） | 开放，无近期更新 |
| [#1443](https://github.com/HKUDS/nanobot/pull/1443) | 2026-03-02 | 分离心跳推理与通知（`sendReasoning` 配置） | 开放，评论较少 |
| [#1835](https://github.com/HKUDS/nanobot/pull/1835) | 2026-03-10 | 向后端 LLM 发送任意附加参数 | **今日已合并**（已清理） |
| [#3358](https://github.com/HKUDS/nanobot/pull/3358) | 2026-04-21 | Model Preset 快速切换 | 开放，近期有更新 |
| [#3513](https://github.com/HKUDS/nanobot/pull/3513) | 2026-04-28 | 统一转录 + 本地 Whisper | 开放，待审查 |

另外，今日新开的 Issue [#3689](https://github.com/HKUDS/nanobot/issues/3689) 虽未积压，但其关于“中断丢失上下文”的反馈与多个开放 PR 关联，应尽快推进归并。

---

*日报基于 GitHub 数据生成，所有链接均可直接跳转至对应 Issue/PR。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我根据您提供的 Hermes Agent (NousResearch/hermes-agent) GitHub 数据，为您生成 2026-05-08 的项目动态日报。

---

# Hermes Agent 项目日报 | 2026年5月8日 (v0.13.0 发布次日)

## 今日速览

在 `v0.13.0` “坚韧”版本成功发布后的第二天，项目依然维持着极高的活跃度。社区对新版本的热情反馈直接体现在 Issue 和 PR 的数量上（均为 50 条），修复和功能请求呈井喷之势。虽然今日未出现灾难性的“致命错误”，但大量 P2 级别的稳定性 Bug（特别是 macOS 兼容性问题和代理/网关状态不一致问题）暴露了当前版本中存在的关键短板。社区贡献者和维护团队正积极通过 PR 对新版本进行后续修复，项目处于从重大发布到稳定化的关键过渡期。

## 版本发布

**新版本：v2026.5.7 — Hermes Agent v0.13.0 (The Tenacity Release)**

- **发布概述**：这是一个里程碑式的大版本，标题 “Tenacity (坚韧)” 揭示了其核心主题：提升 Agent 的鲁棒性和任务完成能力。自 v0.12.0 以来，项目经历了 **864 次提交、588 个 PR 合并、关闭了 282 个 Issue** (其中包括 13 个 P0 和 36 个 P1 问题)，并有 295 位社区贡献者参与，数据规模巨大。
- **关键特性与变化**：
    - **核心 Agent 韧性**：这是版本主题，重点在于让 Agent 在面对错误、中断和复杂情况时能够更好地自主恢复和完成任务，而非简单地抛出异常。
    - **重大代码基础设施**：合并了 588 个 PR，代码库发生巨变 (829 个文件变更，12.8 万+行新增)。这意味着有大量的重构、新特性和底层改动，接口和稳定性可能发生显著变化。
- **破坏性变更与迁移注意事项**：
    1.  **Kanban 数据库迁移**：一个 **P3 级别**的 Bug (#20842) 明确指出，更新后 Kanban 调度器因 SQLite 迁移错误 ( `no such column spawn_failures` ) 而崩溃。用户可能需要手动干预数据库或等待热修复补丁。
    2.  **Docker 构建兼容性**：**P2 级别**的 Bug (#21656) 指出版本 `v2026.4.30` 的 Dockerfile 使用了 Node 20，但官方安装脚本 (`scripts/install.sh`) 推荐 Node 22，导致 `web/` 资产构建失败。新版本可能仍有此问题，使用 Docker 部署的用户需注意。
    3.  **MCP 审批子系统**：**P2 级别**的 Bug (#21558, #21563) 指出 v0.13.0 中新增的 MCP 审批工具 (`permissions_list_open` / `permissions_respond`) 是“空操作”，因为底层 IPC 通道未打通。在正式修复前，此功能不可用。

## 项目进展

虽然 v0.13.0 于昨日发布，但今日项目的主要进展体现在 **针对该版本的快速修复和功能补强** 上。合并/关闭的 PR 和 Issue 主要集中在解决发布后的回归、填补功能漏洞以及扫除积压的“长期挂起” PR。

- **功能补强**：
    - **Feat: 用户代理头 & 仪表盘端点**：PR #21701 和 #21702 已提交，为 GMI 服务请求添加 `User-Agent` 头，并为 Web UI 增加本地令牌和健康检查端点，增强了可观测性和集成体验。
    - **全新工具集成**：PR #21694 提交了**Google Places API (新版)** 的集成，显著扩展了 Agent 的地理信息处理能力。
- **稳定性与 Bug 修复**：
    - **MCP 工具调用修复**：PR #21696 试图修复 Agent 在调用 MCP 工具时丢失 `mcp_` 前缀的问题，这是导致 MCP 工具调用失败的常见根源。
    - **插件与 Provider 修复**：PR #21695 修复了 v0.13.0 中 API-Key 模型提供方插件未完全集成到运行时的间隙。
    - **长期积压 PR 终获推进**：多个长期挂在外的 PR (如 #14407, #11927, #13909) 今日被“rebased”，这表明维护者正在启动对这些“历史遗留”但重要的修复进行审查和合并工作，对项目是有利的信号。例如 #11927 解决了删除技能文件后缓存未失效的问题。

## 社区热点

今日讨论最热烈的 Issue 揭示了用户在升级和使用 v0.13.0 过程中遇到的核心痛点：

1.  **#20842 [热门] [已关闭] Kanban 迁移失败** (评论: 6)
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/20842
    - **分析**: 这是 **v0.13.0 发布后最直接、影响面最广的回归 Bug**。用户 (emm3ttarmstrong) 在进行自动更新后，关键的 Kanban 功能立即崩溃。虽然该 Issue 已被标记为已关闭，但其高评论数和“已关闭”状态暗示存在一个快速的修复，可能是紧急补丁或回滚方案。它深刻反映了用户对自动更新可能破坏核心流程的担忧。

2.  **#13951 [热门] [长期未决] CLI 审批提示无响应** (评论: 3, 👍: 2)
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/13951
    - **分析**: 这是一个持续了半个月的 **P1** 级别安全性/可用性 Bug。用户抱怨在执行危险命令时，终端的审批提示被背景输出淹没，导致无法进行确认或拒绝操作。用户获得的高点赞数 (2个) 表明这是一个普遍的痛点，使得交互式安全控制形同虚设。

3.  **#21563 / #21558 [热门] MCP 审批工具是空操作** (评论: 2)
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/21563
    - **分析**: 这两个 Issue (一个开放、一个已关闭) 共同指向了 v0.13.0 的一个关键功能缺陷。用户 (chrisworksai) 试图使用新功能来管理 MCP 工具的权限，但发现所有审批请求都是“静默空操作”。这不仅是功能未完成，更是一个安全隐患，因为它可能让用户误以为工具调用是受控的，而实际上并非如此。

## Bug 与稳定性

今日报告的 Bug 集中体现了新版本发布后的“磨合期”阵痛，尤其以 **macOS 平台兼容性** 和 **Gateway 状态管理** 问题最为突出。

- **P1 (严重)**：
    - **Subagent 工具委托不一致** (#21658)：子代理有时会报告缺少 `file` 或 `terminal` 工具。这是对 Agent 核心架构的严重挑战，会影响依赖委托的复杂工作流。**暂无对应修复 PR**。
    - **CLI 审批提示无响应** (#13951)：严重的安全流程 Bug。**无对应修复 PR** (存在近一个月了)。
    - **Provider 解析回退到 OpenRouter** (#16623)：用户明确配置本地模型，但系统仍神秘地回退到 OpenRouter。这涉及核心的 Provider 路由逻辑。**暂无对应修复 PR**。

- **P2 (中等等)**：
    - **macOS 锁文件与 PID 重用问题** (#21596, #21613)：这是**今日报告的最严重平台兼容性问题**。由于 macOS 不支持 Linux 的 `/proc` 文件系统，Gateway 的进程锁检测机制（防止程序重复启动）完全失效。PID 被系统重用会导致 Gateway 永久无法启动。**无直接修复 PR**。
    - **辅助 LLM 调用超时导致重试风暴** (#21566)：当使用慢速本地模型（如 Ollama）进行辅助任务时，30秒的默认超时触发错误的重试逻辑，导致连接风暴和性能下降。**无直接修复 PR**。
    - **Dockerfile Node 版本冲突** (#21656)：影响所有 Docker 用户的构建流程。**无直接修复 PR**。
    - **QQ Bot WebSocket 静默宕机** (#21633)：核心平台适配器无法自动重连，导致 Bot 长期离线。**无直接修复 PR**。
    - **`@` 自动补全在 tmux 中卡死** (#21623)：严重影响 macOS 用户 CLI 体验的 Bug。**无直接修复 PR**。

- **P3 (低优先)**：
    - **MCP Twitter 视频下载超时** (#21091)：对大型视频的超时处理不够优化。
    - **Brain (控制面板) 历史 Issue 批量关闭** (#12345-12350)：今日共有 6 个关于 Brain 功能的历史 Issue 被关闭，推测可能是设计方案已定或进入了新阶段。

## 功能请求与路线图信号

社区在 v0.13.0 的“坚韧”主题下，开始着眼于更智能、更自主的未来：

1.  **上下文感知与技能自动发现** (#21686，评论: 2)：用户 `ddiall` 提出一个深度设计问题：Agent 能否不局限于 `.hermes.md`，而是智能地遍历 `CLAUDE.md`、`AGENTS.md` 等通用项目规则文件来自动学习工程上下文。这展现了社区对更“零配置”和“自适应”Agent 的渴望。

2.  **递归多Agent系统** (#19164，评论: 1)：用户 `yepyhun` 提出的高级功能，希望 Agent 能递归地创建子Agent来处理任务，这被认为是向 “Agent 集群” 和 “自我改进” 方向发展的必然步骤。

3.  **会话式大脑 (Brain) 和可观测性**：来自用户 `inpakeo-ux` 的一系列关于“Brain”功能的提案 (已关闭) 和对 Dashboard Profile 可视化的请求 (#21642) 都表明，社区对 Agent 内部状态 (如错误模式、自主性等级) 的可视化和调试有强烈需求。

**可纳入下个版本的信号**：
- **`SessionFrictionAnalyzer`** (PR #11877) 和 **`ProgressiveAutonomyTracker`** (PR #11879) 这两项“长期挂起”的 PR 今日被 rebased，这是一个强烈的信号。这表明 “学习历史错误” 和 “根据表现赋予自主权” 的两大特性很有可能在未来的 v0.14.0 中落地。
- **TUI 中文翻译** (PR #21704) 和 **Feishu 依赖问题** (#21653) 明确指向了对国际化、对中国市场支持的强化。

## 用户反馈摘要

从今日的 Issues 中，可以清晰地看到真实用户的痛点：

- **对“自动驾驶”更新不信任**：从 `Kanban 迁移失败` (#20842) 可以看出，用户对自动更新可能破坏自己稳定运行的业务感到焦虑。用户希望更新是平滑且可回滚的。
- **期望 MCP 生态是安全的，而不仅仅是好用**：用户 `chrisworksai` 对 MCP 审批工具是空操作表达了强烈不满，这不仅是功能缺失，更是对安全承诺的失信。用户需要的是“可控的能力”。
- **本地/自部署用户被边缘化**：`辅助 LLM 调用超时` (#21566) 和 `Provider 解析回退到 OpenRouter` (#16623) 表明，项目的很多默认值和逻辑似乎是为云端 API 用户设计的，而忽视了使用本地模型（ollama, vLLM）的用户。他们需要一个同样流畅的体验。
- **macOS 不是二等公民**：两个关于 macOS PID 锁的 Issue (#21596, #21613) 和 `tmux 自动补全卡死` (#21623) 都指向一个现实：Hermes 的团队似乎主要基于 Linux 开发，对 macOS 的充分测试有所欠缺。

## 待处理积压

以下是一些长期存在、未得到响应或快速解决的重要 Issue 和 PR，它们可能成为未来稳定性的隐患：

1.  **P1 级核心 Bug**：
    - **#13951** [P1] CLI 审批提示无响应 (已存在17天)
    - **#16623** [P1] 本地配置仍会回退到 OpenRouter (已存在11天)
    - **#14407** [P1，有 PR] 验证工具调用防止 Session 投毒 (PR 已有15天，今日刚被 rebased)

2.  **关键功能 PR 等待审查**：
    - **#11927** [P2，有 PR] 技能文件删除后缓存未失效 (PR 已有 20 天)
    - **#20515** [P3，有 PR] 允许 Tailscale 身份认证登录 Dashboard (PR 已有 2 天)

3.  **待解决的对用户影响大的问题**：
    - **#21596** [P2] macOS 平台锁检测机制完全失效 (新，今日提交)
    - **#21633** [P2] QQ Bot WebSocket 无法自动重连 (新，今日提交)

**点评**：维护者需要**优先处理 #21596**，因为它阻止了所有 macOS 用户在 Gateway 意外退出后的正常启动。同时，建议团队能逐步回应并推进如 #13951 和 #16623 这样的 P1 级长期积压，这些“沉默的定时炸弹”会显著消耗社区对项目的信任。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报  
**日期**: 2026-05-08  
**数据来源**: GitHub Issues / PR / Releases (sipeed/picoclaw)  
**数据时间范围**: 2026-05-07 ～ 2026-05-08

---

## 1. 今日速览

过去 24 小时内，PicoClaw 项目保持极高活跃度：共 33 条 Issue 更新（新开/活跃 11 条，关闭 22 条），48 条 PR 更新（待合并 20 条，合并/关闭 28 条），并发布 1 个 nightly 版本。维护者响应迅速，大量反馈得到及时处理（关闭率约 67%），同时有多个功能增强型 PR 正在推进。项目整体健康，但仍有多项长期存在的 Bug 和功能请求待解决。

---

## 2. 版本发布

**nightly (v0.2.8-nightly.20260508.2834db13)**  
- 自动构建，可能存在不稳定性  
- 完整变更日志：[Compare v0.2.8...main](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)  
- **注意事项**: 此版本为每日工程构建，不建议生产环境直接使用。

---

## 3. 项目进展

### 已合并 / 关闭的重要 PR（过去 24h）

- **[#2413] refactor(line): use official LINE Bot SDK v8**  
  用官方 SDK 替换手写 HTTP/HMAC 代码，降低维护成本并修复签名验证等潜在问题。  
  🔗 [PR #2413](https://github.com/sipeed/picoclaw/pull/2413)

- **[#2809 / #2808 / #2807 / #2806 / #2804 / #2803] 依赖升级**  
  多项前端 (`i18next`, `react-i18next`, `globals`, `@tabler/icons-react`, `shadcn`) 及 Go (`fyne.io/systray`) 依赖更新，保持代码健康。  
  🔗 [PR #2809](https://github.com/sipeed/picoclaw/pull/2809) | [#2808](https://github.com/sipeed/picoclaw/pull/2808) | [#2807](https://github.com/sipeed/picoclaw/pull/2807) | [#2806](https://github.com/sipeed/picoclaw/pull/2806) | [#2804](https://github.com/sipeed/picoclaw/pull/2804) | [#2803](https://github.com/sipeed/picoclaw/pull/2803)

### 正在推进的核心功能 / 修复（开放 PR，高活跃）

| PR 编号 | 方向 | 关键内容 |
|--------|------|----------|
| [#2752](https://github.com/sipeed/picoclaw/pull/2752) | 功能增强 | 改进 Web UI 模型配置工作流：支持上游模型拉取、提供方感知验证、连接测试 |
| [#2759](https://github.com/sipeed/picoclaw/pull/2759) | Bug 修复 | 将 Seahorse 检索工具默认限定在当前会话，减少跨会话干扰 |
| [#2758](https://github.com/sipeed/picoclaw/pull/2758) | Bug 修复 | 处理 Telegram 媒体组（相册）作为单条消息，保留字幕 |
| [#2789](https://github.com/sipeed/picoclaw/pull/2789) | 配置 | 使工具反馈进度节流间隔可配置，废弃硬编码 |
| [#2794](https://github.com/sipeed/picoclaw/pull/2794) | Bug 修复 | 异步工具回调后保留原始路由上下文，避免频道丢失 |
| [#2790](https://github.com/sipeed/picoclaw/pull/2790) | Bug 修复 | `spawn` 子 Agent 时正确传递 `agent_id` 路由 |
| [#2793](https://github.com/sipeed/picoclaw/pull/2793) | Bug 修复 | 修复子 Agent 注册表中隐藏工具被发现时的指针克隆问题 |
| [#2814](https://github.com/sipeed/picoclaw/pull/2814) | Bug 修复 | 修复 `exec` 守卫将 `scripts/xxx.sh` 误判为路径逃逸的问题 |
| [#2791](https://github.com/sipeed/picoclaw/pull/2791) | Bug 修复 | 保留 Telegram 主题上下文，让最终回复正确发布到对应主题 |
| [#2823](https://github.com/sipeed/picoclaw/pull/2823) | Bug 修复 | 当工具已回复时，取消最终输出并向订阅者移除残留的反馈指示器 |
| [#2822](https://github.com/sipeed/picoclaw/pull/2822) | Bug 修复 | 子 Agent 同步完成后清除该会话范围内的子工具反馈 |
| [#2719](https://github.com/sipeed/picoclaw/pull/2719) | 新频道 | 新增 `slack_webhook` 输出频道（仅推送），支持 Block Kit 格式 |
| [#2158](https://github.com/sipeed/picoclaw/pull/2158) | 功能增强 | 多 Agent 发现提示（Layer 1），在系统提示中注入最小 Agent 注册表 |

> **项目整体进度**: 大量 Bug 修复及小增强正在集中合入，多 Agent、渠道兼容性等长期路线图功能也在稳步推进。

---

## 4. 社区热点

按评论区活跃度排序，今日最受关注的 Issue / PR：

1. **[#629] [BUG] Didn't retry if meet LLM call failed**  
   - 评论 13，创建于 2026-02-22，至今未关闭  
   - 核心问题：长时间任务中 HTTP 500 导致挂起，无自动重试。用户期望增加重试机制。  
   - 该 Issue 被标记为 `type: bug, type: enhancement`，已积累 13 条讨论，但尚无对应 Fix PR。  
   🔗 [Issue #629](https://github.com/sipeed/picoclaw/issues/629)

2. **[#2408] [Feature] LLM Account Stacking – 自动 API Key 轮换**  
   - 评论 11，已关闭  
   - 社区对多 API Key 管理与限流自动切换有强烈需求，该 Issue 已被标记为关闭，推测已在 nightly 中实现或路线图规划完毕。  
   🔗 [Issue #2408](https://github.com/sipeed/picoclaw/issues/2408)

3. **[#2171] [Feature] 迁移所有 OpenAI 端点至 Responses API**  
   - 评论 10，仍开放  
   - OpenAI 官方推荐，用户希望跟进。已有初步调研（To-Do 列表大部分完成），但未合入主分支。  
   🔗 [Issue #2171](https://github.com/sipeed/picoclaw/issues/2171)

4. **[#1042] [BUG] exec 工具 guardCommand 方法问题**  
   - 评论 9，仍开放，获 2 个 👍  
   - 用户报告 `restrict_to_workspace` 误杀合法命令（如 `curl wttr.in/Beijing?T` 被检测为路径逃逸）。社区呼声较高。  
   🔗 [Issue #1042](https://github.com/sipeed/picoclaw/issues/1042)  
   - **好消息**: 今日 PR [#2814](https://github.com/sipeed/picoclaw/pull/2814) 已提交修复，允许相对脚本路径，预计将解决此问题。

**分析**: 社区最关注稳定性和易用性，尤其是 LLM 调用可靠性、API 兼容性及工具安全守卫的准确性。API Key 轮换功能虽已关闭，但仍需观察实际交付版本。

---

## 5. Bug 与稳定性

### 🔴 高严重性（可能影响用户核心体验）

| Issue | 描述 | 状态 | 是否有 Fix PR |
|-------|------|------|---------------|
| [#629](https://github.com/sipeed/picoclaw/issues/629) | LLM 调用失败不重试，任务挂起 | 开放 | ❌ 无 |
| [#2721](https://github.com/sipeed/picoclaw/issues/2721) | Session 历史竞争条件仍可在 v0.2.5 复现（`tool_use_id` 400） | 开放（标记高优先级） | ❌ 无 |
| [#2817](https://github.com/sipeed/picoclaw/issues/2817) | 语音转录成功后未传递给 LLM，收到 `[voice]` | 开放（今日新开） | ❌ 无 |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | exec guard 误杀合法命令（阻塞工作流） | 开放 | ✅ [#2814](https://github.com/sipeed/picoclaw/pull/2814) |
| [#2468](https://github.com/sipeed/picoclaw/issues/2468) | 定时任务由于“内部频道限制”执行失败 | 已关闭 | ✅ 已修复 |
| [#2377](https://github.com/sipeed/picoclaw/issues/2377) | exec 和日志泄露 ANSI / Unicode 控制字符 | 已关闭 | ✅ 已修复 |
| [#2472](https://github.com/sipeed/picoclaw/issues/2472) | Windows 上 `list_dir` 因路径分隔符问题返回 `invalid argument` | 已关闭 | ✅ 已修复 |

### 🟡 中低严重性

| Issue | 描述 | 状态 |
|-------|------|------|
| [#2447](https://github.com/sipeed/picoclaw/issues/2447) | 同一频道连续发送消息只处理最后一条 | 已关闭 |
| [#2446](https://github.com/sipeed/picoclaw/issues/2446) | 多频道环境下消息回显 | 已关闭 |
| [#2478](https://github.com/sipeed/picoclaw/issues/2478) | 多次 `/use` 装备技能导致覆盖 | 已关闭 |
| [#2280](https://github.com/sipeed/picoclaw/issues/2280) | 硅基流动 API 导致服务无法启动 / QQ 无 AppSecret 配置项 | 已关闭 |
| [#2482](https://github.com/sipeed/picoclaw/issues/2482) | Open Weights 模型 + OpenAI 后端工具调用失败 | 已关闭 |
| [#2302](https://github.com/sipeed/picoclaw/issues/2302) | Web UI 高频要求重新认证 | 已关闭 |
| [#2438](https://github.com/sipeed/picoclaw/issues/2438) | `PICOCLAW_GATEWAY_TOKEN` 环境变量对 `/pico/ws` 无效 | 已关闭 |
| [#2439](https://github.com/sipeed/picoclaw/issues/2439) | Token 覆盖行为未文档化 | 已关闭 |
| [#2440](https://github.com/sipeed/picoclaw/issues/2440) | Docker ReadonlyRootfs 不兼容 | 已关闭 |

**小结**: 过去 24h 修复了大量积累的 Bug，但仍有 3 个高严重性问题（重试、会话竞争、语音转录）待解决。

---

## 6. 功能请求与路线图信号

### 用户新提出的功能

- **[#2820](https://github.com/sipeed/picoclaw/issues/2820)**: 支持非破坏性会话重置（保留 Seahorse 历史记录）。用户需要轻量级 `clear`，而不是删除 SQLite 记录。
- **[#2820 已有关联需求](https://github.com/sipeed/picoclaw/issues/2820)**: 无评论，今日新开。
- **[#2817](https://github.com/sipeed/picoclaw/issues/2817)** 中的语音转录失败本质上也是一个功能缺失：语音消息处理后应回填文本。

### 已有 PR 可能覆盖的功能

- **多 Agent 发现**: [#2158](https://github.com/sipeed/picoclaw/pull/2158) 已提交，正在 review
- **模型配置工作流优化**: [#2752](https://github.com/sipeed/picoclaw/pull/2752) 将改善 Web UI 的模型选择、验证与测试
- **Slack Webhook 频道**: [#2719](https://github.com/sipeed/picoclaw/pull/2719) 新增输出渠道
- **非破坏性会话重置**目前无对应 PR，可能在下个版本规划
- **API Key 轮换**: [#2408](https://github.com/sipeed/picoclaw/issues/2408) 已关闭，但无可见代码合并记录，建议跟进确认。

### 路线图信号

- 长期开放的 **[#348](https://github.com/sipeed/picoclaw/issues/348)** 通用附件支持（文本、多媒体）虽然仅 3 条评论，但被标记为高优先级路线图，尚未有实现 PR。
- **[#2171](https://github.com/sipeed/picoclaw/issues/2171)** Responses API 迁移已有明确 To-Do，说明团队有计划跟进 OpenAI 推荐。

---

## 7. 用户反馈摘要

- **正面**: 多位用户提交的 Bug 获得快速确认或关闭（如 Windows 路径、ANSI 控制字符、技能覆盖等），表明维护者响应积极。
- **痛点**:
  - **重试机制缺失**: #629 用户长时间任务被 HTTP 500 打断，任务挂起无反馈。
  - **文档不透明**: #2439 / #2438 指出环境变量命名误导、Token 覆盖未文档化，导致外部集成困难。
  - **Docker 兼容性**: #2440 用户报告只读根文件系统运行时崩溃。
  - **交互体验**: #2429 用户情绪化评论控制台输入双字符问题（可能为终端或配置问题，已关闭）。
  - **频道消息处理**: #2447 / #2464 用户抱怨连续消息只响应最后一条，虽然已修复，但反映出早期稳定性不足。
- **功能期望**: 社区明确希望支持 SMTP 邮件频道（#2465）、MCP secrets 存储（#2444）、多飞书应用（#2493）等。

---

## 8. 待处理积压

以下为长期未响应或未解决的核心 Issue / PR，建议维护团队优先关注：

### 高优先级开放 Issues

| Issue | 创建时间 | 最后更新 | 优先级 | 简报 |
|-------|----------|----------|--------|------|
| [#629](https://github.com/sipeed/picoclaw/issues/629) | 2026-02-22 | 2026-05-07 | 高 | LLM 调用失败不重试，任务挂起。13 条评论，无 Fix |
| [#2721](https://github.com/sipeed/picoclaw/issues/2721) | 2026-04-30 | 2026-05-07 | 高 | Session 历史竞争条件，Anthropic API 400 错误。标记高优 |
| [#2171](https://github.com/sipeed/picoclaw/issues/2171) | 2026-03-30 | 2026-05-07 | 中 | 迁移至 OpenAI Responses API，已有调研但未合入 |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | 2026-03-04 | 2026-05-08 | 中 | exec guard 误杀命令（已有 Fix PR #2814） |
| [#348](https://github.com/sipeed/picoclaw/issues/348) | 2026-02-17 | 2026-05-07 | 高（路线图） | 通用附件支持，无实现进展 |

### 长期未合并的重要 PR

| PR | 创建时间 | 最后更新 | 简报 |
|----|----------|----------|------|
| [#2158](https://github.com/sipeed/picoclaw/pull/2158) | 2026-03-29 | 2026-05-08 | 多 Agent 发现提示，已超 1 个月未合并，需 review 决策 |

---

**编辑说明**: 本日报基于 2026-05-08 当天 GitHub 数据自动生成，所有结论均源自公开 Issue/PR 内容。部分 Issue 关闭时间可能早于 24h，但更新发生在今日，仍纳入统计。  
**建议**: 团队可优先处理 #629 的重试机制（可参考业界指数退避策略），并评估 #2721 的竞争条件修复方案。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 NanoClaw 项目 2026-05-08 动态日报。

---

# NanoClaw 项目动态日报 | 2026-05-08

## 1. 今日速览

NanoClaw 项目今日活跃度**极高**。过去24小时内，共有 **9 条 Issue 更新**（新开/活跃 5 条，关闭 4 条）和 **35 条 PR 更新**（22 条已合并/关闭，13 条待合并），开发节奏显著加快。重点进展集中在 **A2A 路由修复**、**容器构建稳定性** 以及 **安全加固** 三大方向。值得注意的是，合并的 PR 数量超过新开的 Issue，表明项目团队本周正在进行一轮集中性的 Bug 修复和功能整合，项目健康度表现良好。然而，一个关于**组级凭证管理**的高优长期 Issue (#869) 依然悬而未决，是社区关注的焦点。

## 2. 版本发布

*无新版本发布。*

## 3. 项目进展

今日项目在多个关键领域取得了实质性进展，共有 22 个 PR 被合并/关闭，项目核心能力得到显著增强：

- **A2A (Agent-to-Agent) 路由与稳定性**：这是今日的核心修复方向。
    - **PR #2267** 被合并，修复了 A2A 回复错误地路由到最新会话而非发起会话的问题，这是解决“会话分裂”的关键一步。
    - **PR #2002** 被合并，通过起源会话线程机制，进一步修复了多会话环境下的 A2A 回复路由问题。
    - **PR #2277** 被合并，修复了 Agent Runner 在轮询中仅提取一次路由上下文，导致后续真实消息无法正确路由的 Bug。
    - **PR #2327** 被合并，修复了 SDK 自动压缩上下文后，Agent 丢失“目的地”标记的问题，确保多目的地指令的连贯性。

- **容器与构建系统修复**：
    - **PR #2336** 和 **PR #2335** 被合并，紧急修复了因 `pnpm v11` 导致的 `claude` 二进制文件安装失败问题。通过将容器内 pnpm 版本锁定至 `10.33.0`，解决了代理容器无法启动的根本原因。

- **安全与访问控制**：
    - **PR #2321** (新技能) 和 **PR #2341** (已关闭) 合并，为 `init-onecli gateway` 技能增加了动态凭证获取能力，并修复了两个关键 Bot 命令 (`/restart`, `/build`) 缺乏用户级权限校验的安全漏洞。

- **新技能与集成**：
    - **PR #2321** 合并：新增 `onecli-gateway` 容器技能。
    - **PR #2319** 合并：新增用于 AWS CLI 访问的 `/add-aws` 技能。
    - **PR #2318** 合并：新增用于持久化语义记忆的 `/add-mnemon` 技能。
    - **PR #2320** 合并：更新了多个技能的文档，包括 debug、init-onecli 等。

- **用户体验改进**：
    - **PR #2324** 合并：在 Claude 认证选择器中增加“稍后连接”选项，让首次使用的用户能更轻松地跳过配置，降低了上手门槛。
    - **PR #2316** 合并：改进“其他...”频道选择流程，用户可自由返回上一级菜单，避免流程卡死。

## 4. 社区热点

- **#869 [High Priority] 组级凭证管理**：这是一个讨论热度极高的长期 Feature Request。当前所有群组共享一组 Claude API 凭证，导致配额管理和身份识别混在一起。社区对**独立管理每个群组/频道的API凭证、实现交互式重新认证**的需求非常迫切。这是社区最希望看到的重大功能之一。
    - 链接: [qwibitai/nanoclaw Issue #869](https://github.com/qwibitai/nanoclaw/issues/869)

- **A2A 路由相关问题 (#2331, #2332)**：昨日新开的这两个 Bug 迅速成为焦点，因为它们直接关系到 A2A 通信的核心可靠性。虽然已有 PR (#2267, #2002) 被合并尝试修复，但新 Issue 指出在更复杂的多频道场景下，会话解析仍然可能选错目标，并发现了会导致消息丢失的其他路由 Bug。社区对 A2A 功能的稳定性非常敏感。
    - 链接: [qwibitai/nanoclaw Issue #2331](https://github.com/qwibitai/nanoclaw/issues/2331)
    - 链接: [qwibitai/nanoclaw Issue #2332](https://github.com/qwibitai/nanoclaw/issues/2332)

- **安全命令权限校验 (#2340, #2341)**：`/restart` 和 `/build` 命令的安全漏洞是社区关注的安全热点。虽然 #2341 已关闭，但相关的 #2340 表明了社区对加强 Bot 命令权限控制的强烈共识，任何能发消息到主群组的用户都可能执行危险操作，这是一个严重的潜在风险。
    - 链接: [qwibitai/nanoclaw Issue #2340](https://github.com/qwibitai/nanoclaw/issues/2340)

## 5. Bug 与稳定性

过去24小时报告了多个 Bug，严重程度排列如下：

- **严重 (CRITICAL)**：
    - **A2A 消息路由错乱 (#2331, #2332)**：`findSessionByAgentGroup` 函数在多频道、多会话的 A2A 场景下，会错误地将回复路由到最新创建的会话，而不是原始发送会话。同时发现了另一个导致消息完全丢失的 Bug。这是目前影响最大的稳定性问题。虽然已有修复合并，但该问题需要持续关注。
        - 链接: [qwibitai/nanoclaw Issue #2331](https://github.com/qwibitai/nanoclaw/issues/2331)
        - 链接: [qwibitai/nanoclaw Issue #2332](https://github.com/qwibitai/nanoclaw/issues/2332)

- **高 (HIGH)**：
    - **OAuth 同步告警系统失效 (#2343)**：当凭证文件消失时，告警系统未能在第3次失败后正确触发 `sendSystemAlert`，导致系统在45分钟内无感知。问题已关闭，表明修复已合并。
        - 链接: [qwibitai/nanoclaw Issue #2343](https://github.com/qwibitai/nanoclaw/issues/2343)
    - **Bot 命令未授权执行 (#2340)**：`/restart` 和 `/build` 命令允许主群组的任意用户执行主机重启操作，这是一个严重的安全疏忽。相关修复已合并。
        - 链接: [qwibitai/nanoclaw Issue #2340](https://github.com/qwibitai/nanoclaw/issues/2340)

- **中 (MEDIUM)**：
    - **连接看门狗进程死亡 (#2342)**：`com.nanoclaw.watchdog` 进程自5月1日起因 Qdrant 失败而退出，且未被 launchd 重启，导致系统失去自动恢复能力。该问题已关闭。
        - 链接: [qwibitai/nanoclaw Issue #2342](https://github.com/qwibitai/nanoclaw/issues/2342)
    - **Agent 容器因 pnpm 版本问题无法构建 (#2336)**: 已被 #2335 和 #2336 修复。
    - **TypeScript 构建失败 (由于类型定义不匹配) (#2339, #2344)**: 因多个修改同时合并导致 TS 类型检查失败，已通过 PR #2339 和 #2344 修复。

## 6. 功能请求与路线图信号

- **组级凭证管理 (Must-have)**：`#869` 是社区呼声最高的全新功能，要求实现每个群组拥有独立的 Claude 凭证配置和交互式认证流程。这直接关系到企业级部署和权限隔离，预计将成为下个里程碑版本的核心特性。
- **Web UI 文件附件支持 (Strong candidate)**：`#2334` 提出了 Web UI 文件上传的需求，涵盖上传、粘贴、拖拽等交互，并存储文件供 Agent 处理。这是一个显著提升用户体验的功能，很可能会被纳入下一个路线的规划中。
- **路由安全 (肯定纳入)**：`#2340` 提出的 Bot 命令权限控制虽然是一个 Bug 修复，但其背后的“最小权限原则”需求明确。相关 PR 已合并，该能力已被纳入当前版本。
- **技能系统深化 (路线图清晰)**：
    - `#2337` (PR) 尝试将 Claude Code 的技能目录暴露给非 Claude 提供商，这是一个重要的开放性基础设施信号。
    - `#2345` (PR) 提出了为每个组自动导入 `CLAUDE.role.md` 文件，这指向了更灵活、更细粒度的 Agent 角色定制方向。
    - 多个新技能 (`/add-aws`, `/add-mnemon`) 的加入，表明项目正在系统性地扩展其生态整合能力。

## 7. 用户反馈摘要

- **反映强烈的痛点**：
    - **A2A 通信不稳定**：从 #2331 和 #2332 的快速反馈看，A2A 功能目前“bug 多”、“消息丢失”，用户体验不佳。用户希望“路由解析应该更可靠”，而不是随机指向最新会话。
    - **权限缺失**：用户对 `/restart` 和 `/build` 命令“任何人都能用”感到担忧，认为这是基本的安全隐患。
    - **门槛较高**：首次安装时，Claude 认证步骤的强制性和缺乏跳过选项，让“非技术用户”感到困扰。

- **表达满意的方面**：
    - **修复速度**：从 #2343、#2341、#2342、#2340 等 Issue 的快速关闭可以看出，社区对项目团队响应 Bug 的效率表示认可。
    - **新技能生态**：新加入的 AWS 和 Mnemon 技能受到关注，表明用户对扩展 Agent 能力有强烈兴趣。

## 8. 待处理积压

- **#869 [High Priority] 组级凭证管理**：此 Issue 创建于2026-03-09，虽近期有更新，但仍无实质性进展。作为社区呼声最高、优先级最高的功能需求，它应当被列入下一个开发周期的核心待办事项，以避免社区失望。维护者可以考虑给出初步的设计思路或时间规划。
    - 链接: [qwibitai/nanoclaw Issue #869](https://github.com/qwibitai/nanoclaw/issues/869)

- **#2331 和 #2332 A2A 路由 Bug**：这两个新开的 Critical Bug 虽然已有修复合入，但它们是紧接在新合并的 PR 之后提交的，表明问题并未完全解决。应持续跟踪，确认是否有新的 Regression 出现，或是否需要对在线系统进行 Hotfix。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据 NullClaw 项目 2026-05-08 的 GitHub 数据，为您生成今日项目动态日报。

---

## NullClaw 项目日报 - 2026-05-08

### 1. 今日速览

项目活跃度：**高**

今日 NullClaw 项目保持活跃的开发态势。维护者响应迅速，成功关闭了 2 个 Issue 并合并了 5 个 Pull Request，展现了高效的迭代能力。社区讨论主要聚焦在飞书（Lark）集成配置的灵活性和项目基准测试文档的准确性上。基础设施方面，CI 自动化流程得到显著优化，特别是夜间构建和发布机制已趋成熟。整体来看，项目在功能完善、文档改进和工程效率三个维度均有实质推进。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日有 5 个 PR 被合并/关闭，显著推进了项目的多项能力：

- **基础设施与 CI/CD 自动化**: [#898 - ci: force scheduled nightly builds](https://github.com/nullclaw/nullclaw/pull/898) 被合并。该 PR 通过传递 `force=true` 参数，解决了夜间自动构建因“成功构建的哈希校验”而可能被跳过的问题，确保了每晚都会产出最新的构建产物，提升了开发流水线的可靠性。

- **开发体验与文档**: [#897 - chore(docs): Add docs for quick zig setup](https://github.com/nullclaw/nullclaw/pull/897) 被合并。该 PR 响应了 Issue #820 的请求，为 Debian 等 Linux 发行版提供了 Zig 开发环境的快速搭建指南，降低了新贡献者的入门门槛。

- **核心功能扩展**: [#896 - Add native ACP stdio adapter](https://github.com/nullclaw/nullclaw/pull/896) 被合并。这是一个重要功能更新，在 NullClaw 主程序内原生集成了“Agent Client Protocol (ACP)”的 stdio JSON-RPC 适配器。这使得 NullClaw 可以作为一个标准 ACP 服务端运行，支持与其他 ACP 兼容的客户端或工具进行交互，极大地增强了项目的可集成性。

- **功能集成**: [#893 - feat(toolkit): integrate zig-qm-toolkit](https://github.com/nullclaw/nullclaw/pull/893) 被合并。该项目集成了一个名为 `zig-qm-toolkit` 的工具集，包含 Hooks、Agents、Skills 等功能模块，并引入了四级验证机制，旨在提升代码质量和开发流程的规范化。

- **Bug 修复**: [#790 - fix(providers): Responses API tool schema and null error handling](https://github.com/nullclaw/nullclaw/pull/790) 在经历了一段时间的审查后最终被合并。该 PR 修复了 OpenAI 兼容提供商在“Responses API”模式下的两个关键问题：工具调用格式错误（使用了 Chat Completions API 的格式）和空值处理错误，提升了与新版 OpenAI API 的兼容性。

### 4. 社区热点

- **文档准确性的讨论**: [#473 - README changes](https://github.com/nullclaw/nullclaw/issues/473) 获得了 2 条评论和 1 个 👍。用户指出项目 README 中的基准测试快照数据（如二进制大小、内存占用）已不再准确，并可能引发争议。这反映了社区对项目透明度和宣传材料准确性的要求，维护者需尽快更新相关数据以保持公信力。

- **飞书集成配置扩展**: [#895 - feat(lark): add config option to disable typing placeholder...](https://github.com/nullclaw/nullclaw/issues/895) 和 [#894 - feat(lark): add config option to respond to all group messages...](https://github.com/nullclaw/nullclaw/issues/894) 由同一用户提出，虽无评论，但功能描述详尽且逻辑清晰。前者请求增加禁用“输入中”占位符的配置项，后者请求增加对群组中所有消息（而不仅是 @ 消息）进行响应的配置。这两个 Feature Request 都指向同一个核心诉求：**增强飞书渠道的自定义能力，以适应更多样的用户交互场景**。

### 5. Bug 与稳定性

今日未报告新的严重 Bug、崩溃或回归问题。

- **已修复的 Bug**:
    - **[PR #790]**: 修复了 OpenAI Responses API 的工具格式错误和空值处理 bug。该问题会影响使用新版 OpenAI 模型的用户。*(严重程度：高)*
- **待关注的兼容性问题**:
    - **[PR #887]**: 该 PR 旨在修复在 `Zig v0.16` 版本下的构建问题。目前该 PR 仍处于开放状态，建议维护者尽快审查并合并，以保持项目对最新开发工具链的兼容性。

### 6. 功能请求与路线图信号

今日的新功能请求集中于**飞书（Lark）渠道的配置灵活性**：

- **[#895]**: 请求禁用“输入中”占位符。这是对用户体验的精细化调整，适合通过配置项实现。
- **[#894]**: 请求响应非 @ 消息。这涉及到机器人行为模式的重大改变，可能需要更审慎的设计（如白名单、关键词触发等）。

结合已合并的 **[PR #893]** (`feat(toolkit): integrate zig-qm-toolkit`) 和 **[PR #896]** (`Add native ACP stdio adapter`)，可以看出项目路线图有以下几个清晰信号：
1.  **平台扩展**：通过 ACP 协议，NullClaw 正从一个独立 AI Agent 向一个可被集成的 Agent 服务演进。
2.  **开发工具化**：通过集成 `zig-qm-toolkit`，项目正努力建立一套标准化的开发、测试和验证流程，提升工程质量和效率。
3.  **易用性与配置化**：针对特定渠道（如飞书）的功能增强请求，表明项目正逐步开放更多可配置项以满足细分场景。

### 7. 用户反馈摘要

来自 Issue 评论的真实用户声音：

- **痛点：命令行工具集成与性能**（来源：[#167](https://github.com/nullclaw/nullclaw/issues/167)）
  用户在已关闭的 Issue 中评论道：“`curl` and `wget` commands are hard-coded to use, right”。 这暗示了用户可能希望系统在执行 Shell 命令时有更大的灵活性（例如使用内部函数替代外部命令，或选择不同的工具），以提高跨平台兼容性或性能。

- **满意/体验优化**（来源：[#820](https://github.com/nullclaw/nullclaw/issues/820)）
  用户询问如何在 Debian 上安装 Zig，并疑惑 Docker 是否是必需品。随后 **[PR #897]** 及时响应并增加了相关文档，这说明社区对**清晰、详尽的入门文档**有强烈需求，并且维护者对此类反馈的响应速度令人满意。

### 8. 待处理积压

以下为需维护者重点关注的待处理项目：

1.  **[ISSUE #473] - README changes**：
    - 链接：[https://github.com/nullclaw/nullclaw/issues/473](https://github.com/nullclaw/nullclaw/issues/473)
    - 状态：开放（已开放近 2 个月）
    - 理由：该 Issue 关乎项目对外宣传材料的准确性和可信度，社区已明确表示关注。长期不处理可能影响新用户的信任。

2.  **[PR #885] - [hackathon] feat(memory): Add NullClaw Data Governance Layer**：
    - 链接：[https://github.com/nullclaw/nullclaw/pull/885](https://github.com/nullclaw/nullclaw/pull/885)
    - 状态：开放，Draft 状态（已存在 4 天）
    - 理由：这是一个 Hackathon 团队提交的数据治理层功能，涉及记忆模块。虽然仍处于草稿状态，但这是重要的架构扩展方向。维护者应尽早介入，给予反馈和指导，以确定是否采纳该贡献，避免团队努力因缺乏沟通而白费。

3.  **[PR #887] - Fix build with zig v0.16 for win/linux**：
    - 链接：[https://github.com/nullclaw/nullclaw/pull/887](https://github.com/nullclaw/nullclaw/pull/887)
    - 状态：开放（已存在 4 天）
    - 理由：构建兼容性是项目健康运行的基础。该 PR 解决了对新版 Zig 编译器的支持，应及时合并以避免项目被锁定在旧版本工具链上。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 IronClaw 项目数据，为您生成 2026-05-08 的项目动态日报。

---

### IronClaw 项目动态日报

**日期:** 2026-05-08
**数据统计周期:** 2026-05-07 ~ 2026-05-08

---

### 1. 今日速览

项目开发活动异常活跃，尤其是在 **Reborn 架构重构** 方面取得了重大进展。`v0.28.0` 版本的发布标志着 Reborn 集成基座已合并入主分支，这是一个里程碑式的节点。社区讨论高度集中在 Reborn 相关议题上，同时开发团队也投入了大量精力修复了多个影响用户体验的 Bug，包括 Telegram 集成、LLM 提供商配置持久化等关键问题。项目整体健康度良好，正处于一个高速迭代和架构升级的关键时期。

---

### 2. 版本发布

- **[新版本] ironclaw-v0.28.0** (`0.28.0`) - 发布于 2026-05-07
  - **链接:** [GitHub Release Page](https://github.com/nearai/ironclaw/releases/tag/ironclaw-v0.28.0)
  - **核心更新 (Reborn 集成基座)：** 此版本的发布是 IronClaw 发展的重要里程碑。它将 **`reborn-integration`** 子系统的基座代码合并到了主分支 (`main`)。这引入了大量新架构组件，包括：
    - 主机基础 crate (Host foundation crates)
    - 能力主机 (Capability host)
    - 运行时调度器 (Runtime dispatcher)
    - 进程生命周期管理 (Process lifecycle)
    - 文件系统 (Filesystem)
    - 机密信息管理 (Secrets)
    - 网络 (Network)
    - 扩展清单注册边界 (Extension manifest registry boundaries)
  - **破坏性变更：** 本次发布是架构层面的重大变更，虽然旨在保持对外兼容，但内部 API 和扩展开发接口有根本性变化。
  - **迁移注意事项：**
    1. **二进制文件升级：** 直接从 `v0.27.x` 升级到 `v0.28.0` 是必要的。部分用户报告的 UI 数据延迟加载问题（如 Issue #3274）可能与版本间数据迁移有关，建议在升级后手动刷新页面或重启服务。
    2. **扩展开发者：** 任何基于旧架构编写的扩展、技能或 WASM 模块都需要根据新的 Reborn 架构规范进行适配和重新编译。Releases 中提供了更新的 WASM 工具链。
    3. **配置与存储：** 虽然此版本专注重构，但请注意数据库 schema 可能有细微调整。建议在升级前备份数据。

---

### 3. 项目进展

过去 24 小时内，共有 **32 个 PR 被合并**，开发效率极高。合并的 PR 主要集中在以下几个方面，显示了项目在架构重构、Bug 修复和新功能齐头并进的态势：

- **Reborn 架构深化：**
  - 新增了 `ironclaw_outbound`、`ironclaw_product_adapters`、`ironclaw_wasm_product_adapters` 等多个核心 crate，构建了 Reborn 的出站代理、产品适配器和 WASM 运行时等关键模块。([#3379](https://github.com/nearai/ironclaw/pull/3379), [#3351](https://github.com/nearai/ironclaw/pull/3351), [#3382](https://github.com/nearai/ironclaw/pull/3382))
  - 为 `ironclaw_run_state` 添加了 PostgreSQL 和 libSQL 数据库后端的持久化实现，替换了内存存储，提升了可靠性。([#3349](https://github.com/nearai/ironclaw/pull/3349), [#3378](https://github.com/nearai/ironclaw/pull/3378))
  - 关闭了多个与 Reborn 测试相关的高风险 issue，如 `EventProjectionService` 的添加 ([#3093](https://github.com/nearai/ironclaw/issues/3093)) 和垂直测试套件的推进 ([#3148](https://github.com/nearai/ironclaw/issues/3148))。

- **关键 Bug 修复：**
  - 修复了应用重启挂起、审批流程清晰度等 Web UI 问题 ([#3364](https://github.com/nearai/ironclaw/pull/3364))。
  - 修复了 Gemini API 密钥认证模式下工具调用失败的问题 ([#3225](https://github.com/nearai/ironclaw/issues/3225))。
  - 修复了 LLM 提供商回退机制在启动时错误持久化到数据库，导致用户配置永久丢失的严重 Bug ([#3229](https://github.com/nearai/ironclaw/issues/3229))。
  - 修复了代理循环中审批网关通信的阻塞问题 ([#3365](https://github.com/nearai/ironclaw/pull/3365))。

- **新功能与改进：**
  - 为 WeChat 通道添加了 WASM 构建工件的注册表元数据，简化了部署。([#3386](https://github.com/nearai/ironclaw/pull/3386))
  - 将 Docker 镜像构建为包含 Worker Runtime，支持自托管的沙箱环境。([#3275](https://github.com/nearai/ironclaw/pull/3275))

**总结：** 项目在一天内完成了从架构地基到上层功能的全面迭代，多个核心模块完成了从“山寨”实现到“生产级”数据库持久化的飞跃，并向社区交付了期待已久的 v0.28.0 大版本。

---

### 4. 社区热点

- **最活跃 Issue：** **[#3067 [TEST] Reborn: Add vertical-slice integration test suite**](https://github.com/nearai/ironclaw/issues/3067)
  - **动态：** 作为 Reborn 集成的关键验证项，该 Issue 吸引了 **28 条评论**，社区成员和核心开发者在此深入讨论了测试策略、计划及当前进展。该 Issue 已成为追踪 Reborn 集成稳定性的核心议题。
  - **背后诉求：** 社区渴望证明 Reborn 架构不仅仅在单元测试层面有效，更能在端到端的用户场景下稳定运行。测试用例的完善是社区信心的基石。

- **最大规模 PR：** **[#3387 重构(llm): 将多提供商集成提取到 ironclaw_llm crate**](https://github.com/nearai/ironclaw/pull/3387)
  - **动态：** 由核心开发者 `ilblackdragon` 创建，虽然评论数未显，但这是 **一个 XL 大小、高风险** 的 PR，其核心是将系统中最复杂的 LLM 多提供商逻辑（包括重试、降级、熔断、缓存、路由等）抽取为独立的 `ironclaw_llm` crate。
  - **背后诉求：** 这反映了项目极高的工程追求——模块化、解耦和代码复用。此举将极大降低未来 LLM 相关功能开发和风险控制的复杂度，是架构健康度的重要提升。

- **用户反馈焦点：** **[#3381 修复(auth): 强化 Telegram 配对 UX 和 OAuth 失败恢复**](https://github.com/nearai/ironclaw/pull/3381)
  - **动态：** 该 PR 一次性关闭了 **三个 Bug Bash P1 问题** (#3317, #3319, #3320)，全部指向 Telegram 跨通道 OAuth 流程卡死。
  - **背后诉求：** 暴露出 IronClaw 多通道（Slack, Telegram, Web）集成的复杂性，特别是跨平台认证流程的脆弱性。用户期望的是一个无缝、稳定、且具备良好错误恢复能力的体验。

---

### 5. Bug 与稳定性

- **[严重] #3225 [BUG] Gemini API-Key 后端工具调用失败** ([链接](https://github.com/nearai/ironclaw/issues/3225))
  - **状态：** 已关闭。PR [#3364/3365](https://github.com/nearai/ironclaw/pull/3365) 中包含了修复。
  - **描述：** 在使用 Gemini API Key 认证模式下，`gemini-3.1-flash-lite-preview` 模型在第二次 LLM 调用（即第一次工具调用后）时必然失败，返回 `INVALID_ARGUMENT` 错误。
- **[严重] #3229 [BUG] LLM 提供商回退策略持久化到数据库，永久破坏用户配置** ([链接](https://github.com/nearai/ironclaw/issues/3229))
  - **状态：** 已关闭。修复包含在相关 PR 中。
  - **描述：** 启动时，LLM 提供商的后备策略被错误地持久化到数据库中，导致用户的自定义模型/提供商配置被永久覆盖，重启后无法恢复。此问题影响广泛。
- **[高] #3323 [BUG] 夜间 E2E 测试失败** ([链接](https://github.com/nearai/ironclaw/issues/3323))
  - **状态：** 未合并，自动报告。
  - **描述：** 定时运行的端到端测试 (`Nightly E2E`) 失败，涉及 `v2-engine`，可能需要维护者立即关注。
- **[中] #3274 [BUG] 从 0.26.0 升级到 0.27.0 后 UI 数据丢失/项目标签页显示失败线程警告** ([链接](https://github.com/nearai/ironclaw/issues/3274))
  - **状态：** 已关闭。
  - **描述：** 用户报告升级后聊天页面初始显示无数据，需要手动刷新。这可能与数据迁移或缓存有关。虽已关闭，但对于升级体验仍有参考价值。

---

### 6. 功能请求与路线图信号

- **新功能请求：**
  - **[#3334] 多工作区支持：一个 IronClaw 实例支持多个 Slack 工作区** ([链接](https://github.com/nearai/ironclaw/issues/3334)): 用户提出希望一个 IronClaw 实例能连接多个 Slack 工作区，这表明用户部署场景的复杂化和对多租户、多平台管理的需求。
  - **[#3385] 对话标题自动生成** ([链接](https://github.com/nearai/ironclaw/issues/3385)): 用户提出聊天侧边栏的对话标题应自动总结，而非简单复用第一条用户消息。这是一个提升 Web UI 可用性的小但有效的改进。

- **路线图信号：** 从 **[#3290](https://github.com/nearai/ironclaw/issues/3290)**、**[#3289](https://github.com/nearai/ironclaw/issues/3289)**、**[#3288](https://github.com/nearai/ironclaw/issues/3288)** 和 **[#3287](https://github.com/nearai/ironclaw/issues/3287)** 等多个由 `serrrfirat` 创建的开放性 Issue 来看，**Reborn 迁移计划**非常清晰。开发团队计划系统性地将现有产品功能（如任务/任务、凭据/OAuth、扩展/技能/生命周期、内存/工作空间）逐一迁移到新的 `MissionService`、`SecretService`、`CapabilityCatalog`、`ToolSurfaceService` 等 Reborn 服务上。这预示着未来几个版本的核心工作都将围绕 Reborn 架构的生产化填充和旧功能迁移展开。

---

### 7. 用户反馈摘要

- **痛点：**
  - **升级体验：** 用户 `sunglow666` 报告了升级后 UI 数据延迟加载的问题，表明版本间数据迁移的平滑性有待提升。(#3274)
  - **LLM 集成稳定性：** 用户 `thomasmaerz` 反馈了 Gemini API-Key 认证的失败问题和 LLM 提供商配置被覆盖的严重问题，暴露出 LLM 提供商集成逻辑的健壮性不足。(#3229, #3225)
  - **复杂通道集成：** 用户 `sergeiest` 在多日内多次报告 Telegram 连接的失败问题，凸显了跨平台认证流程的复杂性和对用户的高门槛。(#3317, #2902)
- **使用场景：**
  - **前端能力：** 用户 `sunglow666` 对新 UI 体验提出了精细化要求（如对话标题自动生成），表明 IronClaw 的 Web 界面已经是社区用户的主要交互入口。
  - **部署灵活性：** 用户 `PierreLeGuen` 对多 Slack 工作区的需求，体现了高级用户希望将 IronClaw 作为统一的、跨平台的 Agent 管理中枢。
- **满意点：** Issue 评论中不乏 `👍` 反馈，尤其是在 Bug 被快速修复和关闭时。例如 Issue #3229 获得了一个点赞，表明用户对团队处理关键 Bug 能力的肯定。

---

### 8. 待处理积压

- **重要 Issue:**
  - **[#3259] Publish 0.25.0–0.27.0 to crates.io** ([链接](https://github.com/nearai/ironclaw/issues/3259)): **严重性：高**。下游依赖者被锁定在 0.24.0 版本，无法享受新功能和关键修复。这个问题已存在三天，如不解决，将严重阻碍项目在 Rust 生态中的传播和采用。
  - **[#2902] Telegram is not working for NEAR Foundation instance** ([链接](https://github.com/nearai/ironclaw/issues/2902)): **严重性：高**。这是一个持续了超过两周的问题，尽管有部分针对修复的 PR，但原始 Issue 仍未关闭，说明基础实例的 Telegram 集成可能仍然存疑。

- **重要 PR:**
  - **[#2979] feat(sandbox): support k8s sandbox runtime** ([链接](https://github.com/nearai/ironclaw/pull/2979)): **状态：开放 (11天)**。这是一个功能强大的 PR，引入了 Kubernetes 沙箱支持。但因其规模巨大、风险高，且作者为`新贡献者`，审核周期较长。这是向企业级部署迈出的重要一步，需要维护者加速推动合并。
  - **[#3381] fix(auth): tighten Telegram pairing UX** ([链接](https://github.com/nearai/ironclaw/pull/3381)): **状态：开放 (1天)**。虽然新，但直接回应了 Bug Bash 中最关键的 P1 问题，优先级极高，应尽快合并。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 LobsterAI GitHub 数据，现为您生成 2026-05-08 的项目动态日报。

---

# LobsterAI 项目动态日报 (2026-05-08)

---

### 1. 今日速览

LobsterAI 项目今日活跃度极高，PR 处理量巨大，是近期最繁忙的一天。项目成功发布了 2026.5.7 版本，并合并了大量来自 `release/2026.05.08` 分支的 Cherry-pick PR，这表明团队正在集中进行新版本的集成与发布冲刺。**过去24小时内，共处理了50条PR，其中43条被合并或关闭，合并效率极高。** 在功能推进上，项目迎来了多个重要特性，包括邮件连接失败的 AI 诊断、UI 动画优化、定时任务历史记录筛选、新手引导以及 Token 用量显示等。同时，社区反馈了两个关键问题（IM机器人扫码验证、会员登录），已进入待处理状态。

### 2. 版本发布

**新版本：LobsterAI 2026.5.7**
- **链接：** Releases 页（未提供具体链接，请参考项目主页）
- **主要变更：**
    - **修复**：提升了在 Windows 系统上删除技能的可靠性，并完善了技能导入的用户反馈。
    - **改进**：将 `youdaonote` 技能升级至 1.0.8 版本。
    - **重构**：包含了代码重构，以优化项目结构或性能。
- **破坏性变更**：无。
- **迁移注意事项**：常规升级，无特殊迁移步骤。

### 3. 项目进展

今日项目向前迈出了一大步，大量特性被合并到 `release/2026.05.08` 分支，为下一次发布做准备。以下为关键进展：

- **核心功能增强**：
    - **邮件诊断**：为 IMAP/SMTP 连接失败场景新增了“AI 诊断”按钮，用户可一键将错误信息提交给 AI 进行分析排查。([PR #1527](https://github.com/netease-youdao/LobsterAI/pull/1527), [PR #1916](https://github.com/netease-youdao/LobsterAI/pull/1916))
    - **定时任务管理**：为定时任务的历史记录增加了分页和按状态/时间范围的筛选功能，提升了大型项目的管理效率。([PR #1913](https://github.com/netease-youdao/LobsterAI/pull/1913), [PR #1564](https://github.com/netease-youdao/LobsterAI/pull/1564))
    - **AI 对话体验**：在助理消息下方开始显示 Token 用量统计、上下文窗口占比、模型/智能体名称及时间戳，提高了 AI 交互的透明度和可控性。([PR #1912](https://github.com/netease-youdao/LobsterAI/pull/1912))
    - **会话列表优化**: 实现了会话列表和消息历史的分页加载，解决了数据量大时的内存和渲染性能问题。([PR #1907](https://github.com/netease-youdao/LobsterAI/pull/1907), [PR #924](https://github.com/netease-youdao/LobsterAI/pull/924))

- **用户界面与体验**：
    - **新手引导**：新增基于 driver.js 的首次启动引导和模型配置引导，降低新用户上手门槛。([PR #1577](https://github.com/netease-youdao/LobsterAI/pull/1577))
    - **动画与主题**：合入了主页及对话的入场动画效果，并激活了此前未使用的主题令牌，提升了应用的视觉精致度。([PR #1915](https://github.com/netease-youdao/LobsterAI/pull/1915), [PR #1554](https://github.com/netease-youdao/LobsterAI/pull/1554))
    - **Agent 支持**：为每个 Agent 支持独立的工作目录设定，增强了其个性化和隔离性。([PR #1904](https://github.com/netease-youdao/LobsterAI/pull/1904))

- **平台兼容与稳定性**：
    - **Windows 修复**：修复了 Windows 下文件预览出现重复卡片和路径错误的问题。([PR #1909](https://github.com/netease-youdao/LobsterAI/pull/1909))
    - **修复流式文本**：修复了流式文本合并时重复字符被误删的问题（如 `.pptx` 显示为 `.ptx`）。([PR #1908](https://github.com/netease-youdao/LobsterAI/pull/1908))
    - **启动稳定性**：减少启动时的错误误报，并在错误页面增加了应用内重新启动功能，提升用户恢复能力。([PR #1910](https://github.com/netease-youdao/LobsterAI/pull/1910))

### 4. 社区热点

本期社区讨论不够热烈，但反映了两个影响用户核心使用的关键问题。

1.  **IM机器人微信接口配置问题 (Issue #1878)**
    - **链接**: [Issue #1878](https://github.com/netease-youdao/LobsterAI/issues/1878)
    - **摘要**: 用户 `iwos2610` 报告，在配置微信接口时，微信端要求用户在 OpenClaw 端输入6位数字验证码，但客户端目前没有提供输入界面，导致配置流程卡死，无法完成。
    - **分析**: 这是一个典型的集成流程断裂问题。用户已成功触发了扫码验证，但产品UI未能覆盖后续的输入步骤，导致功能“功亏一篑”。这直接影响 IM 机器人核心能力的可用性，是必须优先解决的阻塞性问题。

2.  **会员登录频繁失败 (Issue #1903)**
    - **链接**: [Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903)
    - **摘要**: 用户 `zhahongan-ctrl` 反馈会员登录频繁失败，导致无法使用网易付费模型。并建议改进登录方式。
    - **分析**: 会员登录问题是高优级的服务稳定性问题。用户付费后无法使用服务，将直接影响用户满意度和付费转化。此问题可能涉及网易账户体系或客户端与服务器的认证流程，需要开发团队紧急排查。

### 5. Bug 与稳定性

今日无新的严重 Bug 被修复，但上述两个社区热点（#1878, #1903）均为用户使用中的功能性 Bug，亟待解决。

- **严重**: **IM机器人 微信接口 配置扫码后无法输入验证码** (`#1878`)
    - 影响核心功能可用性，暂无修复 PR。
    - 链接: [Issue #1878](https://github.com/netease-youdao/LobsterAI/issues/1878)

- **严重**: **会员登录频繁失败** (`#1903`)
    - 影响付费用户核心权益，暂无修复 PR。
    - 链接: [Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903)

- **低严重度**: 本次合并的 PR 修复了**流式文本字符被误吞** ([PR #1908](https://github.com/netease-youdao/LobsterAI/pull/1908)) 和 **Windows文件预览路径错误** ([PR #1909](https://github.com/netease-youdao/LobsterAI/pull/1909)) 两个稳定性问题，对提升整体体验有积极作用。

### 6. 功能请求与路线图信号

- **来自 Issue #1878**: 该问题本质上是一个功能请求：**“为 IM 机器人配置流程增加扫码后的手动验证码输入界面”**。由于该功能是微信接口集成的必要环节，将很可能在下一版本中被紧急修复。
- **来自 Issue #1903**: 用户请求**“改进会员登录方式”**。具体改进方向尚不明确，但可能涉及提高登录成功率、增加错误提示的友好性，或提供备用登录方案。结合项目近期在核心功能方面的增强（如 Token 显示、AI 诊断），加强账户体系的稳定性和可用性可能是项目维护的重点方向之一。

### 7. 用户反馈摘要

从当前的两个 Issue 评论及 PR 摘要中，可以提炼出以下用户痛点：

- **流程不闭环**: 用户能够根据文档进行到某一步，却因 UI 缺失而卡住。这表明在复杂的功能配置流程中，用户测试覆盖仍有不足。 (来源: `#1878`)
- **付费服务不可用**: 用户对无法登录会员感到沮丧，因为这直接关系到他是否能够使用已付费的高级服务（如网易模型）。这表明账户系统和支付环节的稳定性是维系用户的底线。 (来源: `#1903`)
- **对配置复杂度的抱怨**: 用户期待配置过程更“傻瓜化”。例如，#1878 的微信配置场景，用户期望是一个流畅的引导流程，而不是依赖于自行寻找或猜测输入入口。

### 8. 待处理积压

当前项目维护状态良好，但以下两个 Issue 因为阻碍了核心功能使用，已成为重要的积压项。

- **Issue #1878**: IM机器人 微信接口 配置扫码后无法输入验证码
    - **状态**: 已开放 8 天，无分配人，无回复。
    - **链接**: [Issue #1878](https://github.com/netease-youdao/LobsterAI/issues/1878)
    - **提醒**: 该问题比会员登录更早提出，作为影响核心集成的 Bug，建议维护者尽快分配并确认问题，避免用户等待过久。

- **Issue #1903**: 会员登录频繁失败
    - **状态**: 刚提出1天，无分配人，无官方回复。
    - **链接**: [Issue #1903](https://github.com/netease-youdao/LobsterAI/issues/1903)
    - **提醒**: 作为直接影响付费用户的严重问题，建议开发团队优先响应，确认问题范围并给出临时解决方案或修复时间表，以安抚用户情绪。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

好的，遵照您的指示。以下是为您生成的 Moltis 项目日报。

---

## Moltis 项目日报 (2026-05-08)

### 1. 今日速览

过去24小时，Moltis 项目表现出极高的活跃度，完成了大量代码入库和问题解决。项目关闭了4个Issues和9个Pull Requests，并发布了2个版本。核心贡献者（`penso`）主导了多个关键功能的开发，包括**节点身份验证（Ed25519 TOFU）**、**语音功能（STT/Voice）扩展**、**图像生成支持**以及**多个关键Bug修复**。项目正快速向更安全、更开放的 AI 代理服务器演进，尤其在互操作性和本地部署体验方面取得了显著进展。

### 2. 版本发布

项目今日发布了两个版本，均为内部迭代标识，无明确的变更日志或破坏性变更说明。

- **[20260507.05](https://github.com/moltis-org/moltis/releases/tag/20260507.05)**
- **[20260507.04](https://github.com/moltis-org/moltis/releases/tag/20260507.04)**

**分析**：频繁的版本发布表明项目采用持续交付模式，版本号可能对应构建日期和时间。建议维护者在未来发布中添加简短的变更摘要，以便用户和开发者快速了解每个版本的具体内容。

### 3. 项目进展

今日合并/关闭的9个 PR 标志着项目在多个关键领域取得了重大进展：

- **安全性 & 互操作性**：PR [#979](https://github.com/moltis-org/moltis/pull/979) 用 **Ed25519 挑战-响应机制**替换了基于令牌的节点身份验证，实现了类似 SSH 的“首次使用信任”（TOFU）模型。这是建立去中心化、可信代理网络的基础。同时，PR [#976](https://github.com/moltis-org/moltis/pull/976) 添加了相应的集成指南文档。
- **语音功能**：PR [#981](https://github.com/moltis-org/moltis/pull/981) 新增了 `whisper-local` 语音转文字（STT）提供商，满足了注重隐私的用户在本地运行Whisper服务器的需求。PR [#920](https://github.com/moltis-org/moltis/pull/920) 正式合并了通过 **Twilio 实现电话呼叫**的功能。
- **图像生成**：PR [#982](https://github.com/moltis-org/moltis/pull/982) 集成了 OpenAI 的 `gpt-image-2` 模型，通过 **Codex OAuth** 实现了图像生成能力。
- **稳定性与工具修复**：PR [#983](https://github.com/moltis-org/moltis/pull/983) 修复了Issue [#963](https://github.com/moltis-org/moltis/issue/963) 中的工具参数诊断信息丢失问题。PR [#980](https://github.com/moltis-org/moltis/pull/980) 修复了在Docker中运行时的浏览器沙箱问题。
- **基础设施**：PR [#942](https://github.com/moltis-org/moltis/pull/942) 增加了对 Vercel, Daytona, Firecracker 等远程和多后端沙箱的支持。PR [#978](https://github.com/moltis-org/moltis/pull/978) 完成了对 `wasmtime` 依赖的安全更新。

**结论**：过去24小时内，Moltis 从“个人智能工具”向“互联智能代理平台”迈出了坚实的一步，同时在媒体处理（语音、图像）和运行环境兼容性上大幅拓展了能力边界。

### 4. 社区热点

今日社区讨论的热点主要集中在核心架构和用户体验两方面：

1.  **代理互操作协议**：Issue [#973](https://github.com/moltis-org/moltis/issue/973) 提出了为个人代理服务器（如Moltis）建立标准化的“上线和身份协议”，以便它们能相互发现和信任。此提案获得了社区关注，并且立即被 PR [#979](https://github.com/moltis-org/moltis/pull/979) 和 PR [#976](https://github.com/moltis-org/moltis/pull/976) 所响应，这表明项目方对社区提出的架构性需求响应迅速。

2.  **语音功能扩展**：由同一贡献者 `penso` 提出的 PR [#984](https://github.com/moltis-org/moltis/pull/984) 和 [#981](https://github.com/moltis-org/moltis/pull/981) 专注于改善语音设置和本地 STT 支持。PR [#984](https://github.com/moltis-org/moltis/pull/984) 虽未合并，但旨在优化 OpenAI 实时模型的配置引导，并增加 Playwright 测试覆盖。这反映出社区对构建一个平顺、易用且注重隐私的语音交互体验有浓厚兴趣。

### 5. Bug 与稳定性

过去24小时内报告或修复的 Bug 按严重程度排列如下：

- **高**：
    - **[#963](https://github.com/moltis-org/moltis/issue/963) (已关闭)**：模型在执行 `exec` 工具时，如果参数格式异常或为空，会导致“缺少必需字段”的错误，使整个调用失败。此问题严重影响模型工具的可靠性。
        - **Fix PR**：已在PR [#983](https://github.com/moltis-org/moltis/pull/983) 中修复，通过保留和传递更详细的参数诊断信息来解决。
    - **[#977](https://github.com/moltis-org/moltis/issue/977) (已关闭)**：在 Docker 内运行的 Moltis，其浏览器沙箱功能将因配置文件挂载问题而彻底失败。
        - **Fix PR**：已在PR [#980](https://github.com/moltis-org/moltis/pull/980) 中修复，通过解析宿主机可见的数据目录来解决挂载问题。

**分析**：所有报告的 Bug 均在24小时内得到解决，修复高效。Docker 环境的问题修复对希望在不同基础设施上部署 Moltis 的用户至关重要。

### 6. 功能请求与路线图信号

- **图像生成**：Issue [#956](https://github.com/moltis-org/moltis/issue/956) 请求集成 `gpt-image-2` 进行图像生成。该请求已在 PR [#982](https://github.com/moltis-org/moltis/pull/982) 中实现，并确认会被包含在下一个版本中。
- **代理身份与互操作性协议**：Issue [#973](https://github.com/moltis-org/moltis/issue/973) 提出的去中心化代理身份和上线协议，是项目发展为“代理网络”的关键信号。它已被 PR [#979](https://github.com/moltis-org/moltis/pull/979) (核心实现) 和 PR [#976](https://github.com/moltis-org/moltis/pull/976) (文档) 所响应，表明这很可能是下一阶段的核心特性之一。

**分析**：项目路线图信号强烈。社区提出的新的、有远见的功能（如图像生成、代理网络）正被迅速添加到开发计划中并在24小时内实现，体现了项目对用户需求的积极响应和高效的开发执行力。

### 7. 用户反馈摘要

- **稳定性需求**：Issue [#963](https://github.com/moltis-org/moltis/issue/963) 的提交者描述了模型执行指令“间歇性失败”的问题，这暴露出模型工具调用的严谨性问题可能严重影响开发者和AI Agent的使用体验。
- **部署痛点**：Issue [#977](https://github.com/moltis-org/moltis/issue/977) 的用户反馈了在 Docker/Docker-in-Docker 环境下运行浏览工具的具体失败场景，这显示了许多用户在非裸机环境下部署 Moltis 的强烈需求，以及他们遇到的现实挑战。
- **功能期望**：Issue [#956](https://github.com/moltis-org/moltis/issue/956) 简单地请求“添加图像生成支持”，体现用户希望将 Moltis 打造成一个多模态 AI 助手，而不仅仅是一个文本或命令执行平台。

### 8. 待处理积压

- **PR [#984](https://github.com/moltis-org/moltis/pull/984) (待合并)**：为 OpenAI 实时语音模型提供更好的用户配置引导。该 PR 处于开放状态，有1个待合并的改动。考虑到它是对之前 PR [#981](https://github.com/moltis-org/moltis/pull/981) 的完善和补充，建议等待其合并以形成一个完整的语音功能闭环。

**总览**：项目目前积压极少，维护者响应迅速，社区健康度极高。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 CoPaw 项目 2026-05-08 的 GitHub 数据生成的动态日报。

---

# CoPaw 项目动态日报 | 2026-05-08

## 今日速览

今日项目社区活跃度较高，过去 24 小时产生了 36 条 Issue 和 29 条 PR，显示出较强的反馈与贡献意愿。虽然整体处理节奏稳健（PR 合并/关闭率约 69%），但社区对 “易用性”、“多轮对话性能” 及 “稳定性” 三方面的反馈集中爆发，成为今日社区热点。此外，一个关于 MCP 进程导致内存泄漏的严重 Bug 被报告，需高度关注。项目在“技能批量管理”、“飞书渠道优化”和“CLI 功能”等方面有实际推进，但长期存在的“内置技能”讨论 (#280) 仍在持续，显示出社区对核心开箱即用体验的期待。

## 版本发布

**无**

---

## 项目进展

今日合并/关闭了多项重要 PR，推进了功能完善与问题修复，主要集中在渠道优化、CLI 能力增强及后端稳定性方面。

- **渠道优化：**
    - **微信合并缓冲区修复:** PR #4106 修复了 cron 定时任务发送时，因 `_merge_buffer` 无法被刷新而导致消息卡住的问题，改善了定时任务的可靠性。
    - **飞书名称传递:** PR #4098 为飞书渠道增加发送者昵称到 Agent 环境上下文的功能，将影响依赖用户显示名的技能和下游功能。相关修复 PR #4055 也已合并，解决了用户名称无法传递的问题。
- **CLI 功能增强:**
    - **技能测试命令:** PR #3999（首次贡献者）新增 `qwenpaw skills test` 命令，允许在将技能分配给 Agent 前进行验证，提升了开发者调试体验。
- **Backend & 稳定性修复:**
    - **Docker 密钥恢复修复:** PR #3916 修复了 `SECRET_DIR` 作为 Docker 卷挂载点时的备份恢复问题，解决了因 `EBUSY` 错误导致的恢复失败。
    - **Windows 打包修复:** PR #4093 修复了 Windows 桌面版打包时，`conda-pack` 与 `pip install qwenpaw[full]` 的冲突问题 (#3988)，确保了 Windows 分发版本的稳定性。
- **前端体验:**
    - **技能批量管理:** PR #4091 实现了前端技能板块的批量启用/禁用按钮（对应功能请求 #3503），提高了 Agent 配置效率。

---

## 社区热点

1.  **#280 - 讨论：哪些技能和 MCP 该内置？** (27条评论)
    - **诉求分析:** 作为一个元问题，此 Issue 持续获得高关注。核心诉求是用户期望项目能提供更多开箱即用的功能，减少繁琐的自定义配置。这反映了个人 AI 助手用户对“即刻可用”体验的强烈需求，也是项目降低使用门槛、吸引非技术用户的关键。

2.  **#3919 - [Bug] 切换 Agent 后会话丢失** (9条评论)
    - **诉求分析:** 用户报告切换 Agent 再返回时，前端 `lastChatIdByAgent` 功能未实现，导致任务中断、会话丢失。此问题直击多 Agent 协同场景的核心体验，是用户工作流的严重中断。评论中用户明确指出了“功能缺失而非bug”，体现了对多 Agent 管理易用性的高期待。

---

## Bug 与稳定性

| 严重程度 | Issue | 摘要 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | #4105 | **MCP 孤儿进程累积导致内存泄漏** (~18GB/1.5天)。问题报告 `qwenpaw app` 守护进程下，MCP 子进程在会话结束时未被清理，导致内存持续泄露。 | **新开，待处理** |
| **高** | #4108 | 新版本 WebUI 在回复生成时“巨卡”，导致鼠标掉帧、切换窗口缓慢，影响多线程工作。用户反馈“体验越来越差”。 | **新开，待处理** |
| **中** | #4051 | 对 DeepSeek 模型的 think 部分内容解析异常，导致 Agent 没有正常回复。 | **新开，待处理** |
| **中** | #4056 | 微信渠道在正常网络条件下偶发消息丢失，Agent 停止响应。 | **新开，待处理** |
| **低** | #4047 | 聊天记录中的文件/图片链接在一天后过期，导致无法查看。已有相关修复 PR #4089。 | **已关闭** |
| **低** | #4104 | 文件名含中英文数字时（例如 “2026年报告.word”），Agent 获取的文件名会多出空格。 | **新开，待处理** |

---

## 功能请求与路线图信号

- **“添加模型步骤太多” (#4036):** 用户期望简化配置流程。这可能与正在进行的 #3819 PR 相关，该 PR 用可浏览的远程模型列表取代了“自动发现”按钮，支持批量添加。
- **“技能选择器交互优化” (#4078):** 用户希望将 `/` 触发的纯文本技能列表改为交互式下拉菜单，以提升使用效率。
- **“从 Web 控制台升级 CoPaw” (#2235):** 用户期望能在网页端远程升级项目，这是一个提升运维便利性的重要需求。
- **“增强[File]模块能力” (#4087):** 用户希望 File 模块能支持查看 Markdown 以外的更多文件类型，以提升实用性。
- **“添加 Vertex AI Gemini provider” (#4030):** 用户希望支持通过 Google Cloud Vertex AI 使用 Gemini 模型，以满足企业级 IAM 和合规需求。

**路线图信号:** 综合来看，下一版本的重点可能在于**模型管理的易用性优化**、**技能系统的交互升级**，以及**探索 Web 端运维管理能力**。

---

## 用户反馈摘要

- **正面反馈:** 无明确正面反馈，但社区积极提交 Issue 和 PR 本身就是对项目未来发展的肯定。
- **痛点反馈:**
    - **性能退化:** #4108 “新版本的webui一开始工作后，电脑就开始巨卡... 体验上越来越差了。” 此抱怨直接指出了版本迭代带来的性能回退问题。
    - **核心使用场景受阻:**
        - #3919 “切换Agent后返回原agent，发现任务中断且session丢失” 是严重影响多 Agent 工作流用户体验的问题。
        - #4000 “微信对话和浏览器操作不同步” 和“网页版语音输入功能缺失”，表明渠道间的体验一致性仍有差距。
        - #3350 用户在进行超过 200 轮的超长对话后，页面滚动“特别卡”，并请求优化方案。
    - **上下文管理困扰:** #4102 “截图一直在上下文中，不断压缩... 不断消耗token这是何意啊！怎么才能关掉这个？” 用户对视觉模型的图片压缩和上下文管理策略感到困惑和不满，认为不够智能。

---

## 待处理积压

- **#578 - [Meta] OpenClaw 启发的复合 Agent 价值功能:** 创建于 2026-03-04，是一个元问题，追踪一系列旨在提升用户长期粘性的功能需求。该项目已收到 7 条评论且今日仍有更新，但尚未标记明确的实现优先级或里程碑，社区对其进展期待较高。
- **#2235 - [Feature] 期望可以通过web控制台进行copaw的升级:** 创建于 2026-03-25，仅有 2 个评论和 1 个赞，但请求合理且用户明确，反映出对远端运维能力的长期需求。目前没有明确的 PR 或维护者回应。
- **#3238 - [PR] feat: add PlanNotebook support for task planning (experimental):** 创建于 2026-04-10，当前状态为“Under Review”。这是一个实验性的任务规划功能，若能合并，将是 Agent 能力的重要补充，建议维护者评估其合并优先级并给予关注。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目日报

**日期：2026-05-08**  
**数据来源：ZeroClaw GitHub（github.com/zeroclaw-labs/zeroclaw）**

---

## 1. 今日速览

- **项目活跃度极高**：过去24小时内产生了50条Issue更新、50条PR更新，并发布了v0.7.5版本，社区参与和开发节奏均保持强劲。  
- **关键里程碑**：v0.7.5带来了**浏览器内Onboarding和配置**、基于OpenAPI 3.1的Gateway CRUD界面以及三面人格编辑器，显著降低了新用户入门门槛。  
- **社区焦点**：Provider架构重构（#5937）、WhatsApp Web协议升级后消息中断（#6246）以及Fallback凭证继承漏洞（#6418）成为讨论最热烈的话题。  
- **稳定性警讯**：暴露了若干S0/S1级Bug，包括数据安全风险（#6418）和工作流阻塞问题，部分已有对应修复PR（#6432）。  
- **整体健康度**：开发迭代活跃，但高优先级Bug和长期未决PR需维护者优先处理。

---

## 2. 版本发布：v0.7.5

- **版本号**：v0.7.5  
- **发布说明摘要**（从v0.7.4升级）：  
  - **浏览器内Onboarding**：基于schema驱动的`/onboard`流程，用户无需CLI即可完成初始配置。  
  - **Gateway CRUD界面**：基于OpenAPI 3.1规范，支持每个属性的增删改查，並配以类型化CLI。  
  - **三面人格编辑器**：统一在CLI、TUI和Web界面上提供人格设置编辑能力。  
  - **其他改进**：包括Provider配置优化、稳定性修复等（完整Changelog请参阅Release页面）。  
- **迁移注意事项**：  
  - 建议用户运行`zeroclaw onboard --tui`重新检查配置，确保新字段正确设置。  
  - 若使用自定义Provider，请确认`config.toml`中的`kind`和`api_base`与新版本兼容。  
  - 无计划中破坏性变更，但推荐在升级前备份旧配置。

---

## 3. 项目进展

今日共有**2个PR被合并/关闭**（具体未在列表中显示），此外以下关键PR正处于活跃协作状态，代表着项目前进方向：

| PR # | 标题 | 状态 | 影响范围 |
|------|------|------|----------|
| #6502 | fix(ci): unblock v0.7.5 release — run gen-api before tsc | 🔄 待合并 | CI/CD修复，阻塞v0.7.5发布 |
| #6432 | fix(memory): tolerate concurrent sqlite schema migrations | 🔄 待合并 | Memory模块并发安全修复 |
| #6389 | feat(channels): per-recipient reply pacing across 9 channels | 🔄 待合并 | 消息节流新功能 |
| #6247 | Feat/sop webhook dispatch | 🔄 待合并 | 大面积新功能（CI/核心/通道等） |

**项目推进总结**：  
- **CI/CD**：通过#6502解除了v0.7.5的发布阻塞。  
- **内存**：#6432解决了SQLite并发Schema迁移问题，提升了多进程启动稳定性。  
- **通道**：#6389新增9个通道的逐接收者回复节流，增强反垃圾能力。  
- **技能修复**：#6209正在严格化SkillMeta并规范Provenance结构。

---

## 4. 社区热点

以下Issue在过去24小时内获得了最多的讨论和关注：

### 📌 #5937：Unify providers architecture and reqwest client management
- **8条评论**，创建于2026-04-20  
- **诉求**：重构`providers`模块，消除`reqwest`客户端和模型构造参数的重复代码，统一配置入口。  
- **分析**：该项目影响力极大，涉及所有Provider使用者。由于状态为`blocked`，维护者需要考虑优先级和实现方式。  
- 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/5937

### 📌 #6246：WhatsApp Web channel: pair succeeds but messages don't flow after April 2026 server-side protocol bump
- **6条评论**，创建于2026-04-30  
- **诉求**：WhatsApp Web协议在2026-04-24升级后，即使配对成功也无法收发消息，用户alexandme报告工作流完全阻塞。  
- **分析**：严重性S1，影响WhatsApp Web所有用户，急需维护者调查底层`wa-rs`库兼容性或协议适配。  
- 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/6246

### 📌 #6418：Fallback Providers Fail to Inherit Credentials from config.toml
- **4条评论**，创建于2026-05-06，已关闭（标记为duplicate）  
- **诉求**：当主Provider因429等错误触发fallback时，fallback Provider未能继承`config.toml`中的凭证，导致数据泄露风险（S0）。  
- **分析**：被标记为重复，但具体关联Issue未明示。此Bug风险极高，社区强烈关注，需确保正确关闭前已提供永久修复。  
- 链接：https://github.com/zeroclaw-labs/zeroclaw/issues/6418

---

## 5. Bug 与稳定性

按严重程度排列今日报告的Bug（Severity从S0到S3）：

| Issue # | 严重性 | 标题 | 是否已有Fix PR |
|---------|--------|------|----------------|
| #6418 | **S0 – 数据丢失/安全风险** | Fallback Providers Fail to Inherit Credentials from config.toml | 已关闭（Duplicate） |
| #6246 | **S1 – 工作流阻塞** | WhatsApp Web channel: pair succeeds but messages don't flow | 无 |
| #6399 | **S1 – 工作流阻塞** | Custom remote provider sends local image file paths instead of data URLs | 无 |
| #6474 | **S1 – 工作流阻塞** | process 1 user request, invoking the LLM twice repeatedly | 无 |
| #6434 | **S1 – 工作流阻塞** | Shell tool calls refused at autonomy level = "full" | 无 |
| #6516 | **S1 – 工作流阻塞** | ACP "cwd" change can lock agent out of reading its own skill files | 无 |
| #6472 | **S2 – 降级行为** | gateway can not use postgres | 无 |
| #6431 | **S2 – 降级行为** | SQLite memory schema init can fail during concurrent startup | ✅ #6432 |
| #6400 | **S2 – 降级行为** | Docker bind mount shadows pre-built web dashboard | 无 |
| #6373 | **S3 – 次要问题** | Fresh install, web_search doesn't work, web_fetch does | 无 |

**值得关注的修复PR**：  
- #6432（fix memory）直接对应#6431，且已在合并队列。  
- #6502（fix CI）虽非直接修复Bug，但解除了发布阻塞，有助于快速推送修复版本。  
- 对于S0 #6418，因标记为Duplicate，建议维护者提供明确的永久修复链接或说明。

---

## 6. 功能请求与路线图信号

### 可能纳入下一版本（v0.7.6/v0.7.7）的功能

| Issue # | 标题 | 已有PR？ | 理由 |
|---------|------|----------|------|
| #6522 | Web chat — tool approval UI for supervised-mode | 无 | Gateway后端已实现WebSocket approval协议，前端缺失，属于桌面版“必填项” |
| #6371 | WhatsApp Web: per-JID group allowlist (allowed_groups) | 无 | 社区强烈需求，提高运营安全性 |
| #6375 | V3 env-var override mechanism for credentials | 无 | 替换被移除的V1/V2路径，避免用户混淆 |
| #6510 | cron `delivery.mode = "announce"` — option to send only final assistant message | 无 | 改善cron推送体验，减少噪音 |
| #6518 | First-Class Support for Custom / OpenAI-Compatible Providers (e.g. Kimi K2.5) | 无 | 提高生态兼容性，降低用户接入门槛 |
| #6465 | Bundle chat-ui as static assets in the desktop binary | 无 | 桌面版离线可用性基础，与#6320形成完整Onboarding |

### 路线图信号
- 桌面版（Tauri）持续增强，涉及启动流程 (#6320)、托盘菜单 (#6329)、通用二进制 (#6339) 等，表明桌面端是当前重点投入领域。
- Provider架构重构 (#5937) 虽然阻塞，但若落地将极大提升代码质量和可扩展性，建议维护者优先安排设计讨论。

---

## 7. 用户反馈摘要

从Issue评论和描述中提炼的真实用户痛点：

- **WhatsApp Web通信中断（#6246）**：用户alexandme在配对成功后无法收发消息，怀疑是服务器端协议升级导致，手动重新配对不能解决，需维护者深入`wa-rs`库层寻找兼容性方案。
- **自定义Provider图像路径错误（#6399）**：vanbukin在树莓派上运行ZeroClaw，并连接远程vLLM服务器，发送图像时传递的是本地文件路径而非data URL，导致多模态请求失败。该用户同时期望能配置服务器地址而非硬编码。
- **PostgreSQL支持缺失（#6472）**：hjh218尝试通过Gateway使用PostgreSQL作为记忆后端时，遇到运行时panic：“Cannot start a runtime from within a runtime”，表明数据连接层存在异步运行时嵌套问题。
- **Shell工具在高自主权级别被拒绝（#6434）**：sam74S配置了`[autonomy] level = "full"`且未设置任何限制，但Shell调用依然被拒绝。用户对此逻辑感到困惑，怀疑是权限校验代码存在bug。
- **Docker文档错误（#6393）**：alkaid-ops指出官方网站zeroclaws.io上的Docker安装指南完全错误，且GitHub上的容器Compose文件缺少必要说明，导致新用户无法顺利部署。
- **Gemini CLI Provider崩溃（#6520）**：Gihan-1994报告使用`gemini-cli`作为主模型时，agent立即崩溃，原因是使用了错误的参数语法（`--print` vs `--prompt`）。

**整体用户情绪**：高活跃社区积极反馈问题，但也反映出部分关键功能（特别是WhatsApp、PostgreSQL、Provider兼容性）的稳定性不足。文档质量参差不齐。感谢社区用户提供详细日志和复现步骤，有助于快速定位。

---

## 8. 待处理积压

以下为创建时间较早、至今仍开放且具有高重要性的Issue和PR，提醒维护者关注：

| 编号 | 类型 | 创建时间 | 标题 | 积压原因 |
|------|------|----------|------|----------|
| #5937 | Issue | 2026-04-20 | refactor providers and reqwest client management | 风险high且blocked，但需核心架构决策才能推进 |
| #6246 | Issue | 2026-04-30 | WhatsApp Web protocol bump | 无对应修复PR，S1级别影响面广 |
| #5661 | PR | 2026-04-12 | feat(cron): wire CLI delivery flags, clean envelope, add announce + bounds | 规模XL，risk high，依赖其他PR未合并 |
| #6028 | PR | 2026-04-23 | fix(tests): make Windows dev tests portable | 长期未合并，影响Windows贡献者体验 |
| #5075 | PR | 2026-03-29 | docs(channel): clarify WhatsApp Web feature reinstall guidance | 存在近40天未合并，属于文档修复，不应久拖 |
| #5121 | PR | 2026-03-29 | fix(provider): enforce Mistral-compatible tool_call.id serialization | 同样长期未动，且涉及兼容性修复 |

**建议**：  
- 对#5937发起一次架构讨论会议，明确是否纳入v0.8路线图或拆分实施。  
- #6246应优先分配人力，可考虑临时降级WhatsApp Web特性或标注不兼容。  
- 对以上积压PR进行逐项评审，明确合并或关闭理由，减少拥堵。

---

*本日报由AI智能体根据ZeroClaw GitHub数据自动生成，仅供参考。具体细节请以官方仓库公告为准。*

</details>

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*