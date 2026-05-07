# Hugging Face 热门模型日报 2026-05-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-07 09:44 UTC

---

# Hugging Face 热门模型日报（2026-05-07）

## 今日速览

- **DeepSeek V4 双雄领跑**：DeepSeek-V4-Pro 和 V4-Flash 周点赞合计超 4600，下载量超 170 万，巩固了国产开源大语言模型的领先地位。
- **多模态模型爆发**：Qwen3.6 系列、Google Gemma 4 系列、NVIDIA Nemotron 3 等多模态模型占据榜单近半数席位，图像/文本/音频/任意模态融合成为主流。
- **量化与“去审查”风潮**：GGUF 量化版模型（如 unsloth 版本）下载量惊人，同时“Uncensored”、“Abliterated”等社区微调版本持续涌现，反映用户对开放式模型的需求。
- **MoE 架构普及**：Qwen3.6-35B-A3B（MoE）、NVIDIA Nemotron-3-Nano-Omni-30B-A3B、Google Gemma-4-26B-A4B 等混合专家模型表现活跃，高效推理与大规模参数兼顾。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 3,688 | 946,264 | 周榜冠军，DeepSeek 最新旗舰对话模型，性能对标闭源前沿，社区追捧热度极高。 |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 969 | 751,333 | 轻量版 V4，主打快速推理，下载量逼近 Pro，适合资源受限场景。 |
| [Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B) | mistralai | 286 | 18,272 | Mistral 的 128B 中型模型，支持英语和法语，意在平衡规模与实用性。 |
| [MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro) | XiaomiMiMo | 465 | 20,905 | 小米 MiMo 升级版，长上下文 + Agent 能力突出，国产手机厂商布局 LLM 的代表。 |
| [Laguna-XS.2](https://huggingface.co/poolside/Laguna-XS.2) | poolside | 229 | 16,792 | Poolside 推出的代码导向文本生成模型，专注于开发者体验。 |
| [Granite-4.1-8b](https://huggingface.co/ibm-granite/granite-4.1-8b) | ibm-granite | 161 | 24,099 | IBM Granite 系列 8B 基础模型，企业级语言建模，强调可部署性。 |
| [Granite-4.1-30b](https://huggingface.co/ibm-granite/granite-4.1-30b) | ibm-granite | 103 | 8,932 | Granite-4.1 的 30B 版本，规模更大，适合复杂推理任务。 |
| [Ling-2.6-1T](https://huggingface.co/inclusionAI/Ling-2.6-1T) | inclusionAI | 424 | 1,589 | 万亿参数级超大语言模型（1T），采用 Bailing Hybrid 架构，代表超大规模开源尝试。 |
| [talkie-1930-13b-it](https://huggingface.co/talkie-lm/talkie-1930-13b-it) | talkie-lm | 239 | 0 | 13B 指令微调模型，基于 talkie 基础版，部分场景零下载但关注度高。 |
| [ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B) | Zyphra | 115 | 539 | 新秀 Zyphra 发布的 8B 通用模型，Apache 2.0 许可，附带评估结果。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 1,653 | 3,211,156 | 阿里 MoE 多模态模型，总参 35B 仅激活 3B，高效处理图文输入，下载量榜首。 |
| [Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B) | Qwen | 1,164 | 1,771,851 | Qwen3.5 系列续作，27B 图文对话模型，兼顾性能与部署成本。 |
| [Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it) | google | 2,545 | 8,594,149 | Google Gemma 4 旗舰指令版，下载超 850 万，图文理解能力强劲，社区最活跃的多模态模型之一。 |
| [Gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant) | google | 130 | 19,908 | Gemma-4 的助手变体，支持任意到任意模态（any-to-any），拓展多模态边界。 |
| [Gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant) | google | 80 | 12,868 | 26B 激活 4B 的 MoE 助手版，兼顾效率与多模态能力。 |
| [Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16) | nvidia | 256 | 65,066 | NVIDIA 最新全模态推理模型，30B 总参/3B 激活，支持文本、图像、音频等任意模态。 |
| [SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT) | sensenova | 168 | 2,724 | 商汤 SenseNova 推出的 8B 多模态 MoT 模型，主打特定任务优化。 |
| [Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base) | SulphurAI | 322 | 71,149 | 文本到视频的基础模型，支持 Diffusers 和 GGUF，视频生成领域新星。 |
| [Z-Anime](https://huggingface.co/SeeSee21/Z-Anime) | SeeSee21 | 202 | 4,460 | 动漫风格文生图模型，融合 GGUF 量化，面向二次元创作社区。 |
| [LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros) | TenStrip | 141 | 28,215 | 图生视频模型，专门优化短视频生成，适合创意内容制作。 |
| [MiMo-V2.5](https://huggingface.co/XiaomiMiMo/MiMo-V2.5) | XiaomiMiMo | 218 | 65,258 | MiMo 2.5 基础版，支持视觉-语言-音频多模态，小米多模态生态核心组件。 |

### 🔧 专用模型（代码、数学、医疗、嵌入等）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [privacy-filter](https://huggingface.co/openai/privacy-filter) | openai | 1,332 | 165,240 | OpenAI 官方发布的隐私过滤模型（token分类），用于检测敏感信息，安全领域刚需。 |
| [Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit) | AngelSlim | 102 | 16,631 | 极低比特（1.25bit）翻译模型，基于 Hunyuan 架构，探索极端量化下的翻译能力。 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF) | unsloth | 948 | 2,417,319 | unsloth 量化的 Qwen3.6 MoE 版，下载量超 240 万，社区部署首选。 |
| [unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF) | unsloth | 603 | 1,264,430 | 27B 图文模型的量化版，极大降低推理门槛，配合 unsloth 的优化工具。 |
| [Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK) | dealignai | 1,484 | 169,511 | Gemma-4 的“去审查”（abliterated）微调版，移除安全限制，下载量极高。 |
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 572 | 973,262 | 基于 Qwen3.6 MoE 的激进去审查 GGUF 版，社区对“无限制”模型需求旺盛。 |
| [Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF) | DavidAU | 85 | 126,660 | 另一款 Qwen3.6 去审查 + 代码增强的极长名 GGUF 模型，体现社区定制化趋势。 |
| [Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash) | z-lab | 252 | 28,767 | 基于 Qwen3.6 的“DFlash”优化版，专注快速推理或特定改进，社区二次创新。 |
| [Qwen3.5-9B-DeepSeek-V4-Flash-GGUF](https://huggingface.co/Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF) | Jackrong | 98 | 104,723 | 跨模型融合作品：将 Qwen3.5-9B 与 DeepSeek V4 Flash 能力结合的量化版，探索混合模型。 |

---

## 生态信号

- **Qwen 与 Gemma 两大生态强势竞争**：Qwen3.6 系列和 Google Gemma 4 系列在总点赞与下载量上遥遥领先，形成围绕中文（Qwen）与英文（Gemma）的多模态双雄格局。DeepSeek 则在纯语言领域保持霸主地位。
- **开源权重全面领先**：所有热门模型均以开放权重形式发布（safetensors 或 GGUF），闭源模型缺席榜单；社区微调和量化活动极其活跃，尤其“Uncensored”版本成为高频关键词，反映用户对内容限制的强烈反拨。
- **量化成为标配**：GGUF 格式的下载量往往数倍于原始模型（如 unsloth 版本下载超 240 万），表明本地部署和边缘计算是主流需求。MoE 模型（Qwen3.6-35B-A3B、Gemma-4-26B-A4B）因其高效激活而备受量化社区欢迎。

---

## 值得探索

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**：当前热度最高的开源语言模型，适合评估国产大模型在复杂推理、长对话方面的最新水平，也是企业级应用的优选。
2. **[Google Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**：多模态领域的标杆，下载量超 850 万，强烈推荐用于图像理解、图文对话等场景，且社区微调版本丰富（如 dealignai 的去审查版）便于二次开发。
3. **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)**：结合 MoE 高效推理与 GGUF 轻量部署的典范，适合在消费级 GPU 上运行强大多模态模型，同时可供对比原版与量化版的精度差异。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*