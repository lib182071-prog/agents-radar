# Hugging Face 热门模型日报 2026-05-11

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-11 11:46 UTC

---

# Hugging Face 热门模型日报（2026-05-11）

## 今日速览

DeepSeek-V4-Pro 以 3,841 周点赞登顶，成为当周最受关注的纯文本生成模型，下载量突破 200 万；Google 的 Gemma-4 系列多模态模型（31B-it）以 2,595 点赞紧随其后，下载量超 900 万，反映了社区对**开源多模态大模型**的强烈需求。Qwen 3.6 系列同样表现强劲，尤其是 35B-A3B MoE 版本（1,712 赞），其量化版（GGUF）与微调版占据榜单多个席位，说明 **MoE 架构与量化部署**已成为主流方向。此外，OpenAI 的开源隐私过滤模型（privacy-filter）意外攀升至第四（1,406 赞），展示了对**模型安全/合规工具**的持续关注。语音合成方面，k2-fsa/OmniVoice 零样本语音克隆模型获得 842 赞，预示多语言 TTS 的开源生态正在成熟。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者: deepseek-ai | 点赞: 3,841 | 下载: 2,017,835  
  一句话说明：DeepSeek 第四代旗舰对话模型，性能对标闭源顶级模型，因强大的长上下文与推理能力成为周榜冠军。

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  作者: deepseek-ai | 点赞: 1,031 | 下载: 1,162,290  
  一句话说明：V4 的轻量加速版，兼容 vLLM 部署，适合高吞吐生产场景，社区关注度持续高位。

- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)**  
  作者: XiaomiMiMo | 点赞: 506 | 下载: 41,654  
  一句话说明：小米推出的长上下文 Agent 模型，主打工具调用与复杂任务规划，代表国产手机厂商入局大模型。

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)**  
  作者: Zyphra | 点赞: 402 | 下载: 66,119  
  一句话说明：8B 参数通用语言模型，Apache-2.0 许可，配套 arXiv 论文，学术社区讨论度高。

- **[mistralai/Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)**  
  作者: mistralai | 点赞: 313 | 下载: 43,141  
  一句话说明：Mistral 中端 128B 模型，支持英语/法语，专为 vLLM 优化，适合企业部署。

- **[z-lab/gemma-4-31B-it-DFlash](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash)**  
  作者: z-lab | 点赞: 74 | 下载: 6,423  
  一句话说明：基于 Gemma-4-31B-it 的投机解码（Speculative Decoding）优化版，大幅降低推理延迟。

- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)**  
  作者: z-lab | 点赞: 282 | 下载: 34,966  
  一句话说明：Qwen3.6-27B 的 DFlash 加速版，同样利用投机解码，适合实时推理需求。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
  作者: Qwen | 点赞: 1,231 | 下载: 2,446,478  
  一句话说明：Qwen 3.6 系列多模态对话模型（27B），支持图像+文本输入，下载量超 200 万，社区生态繁荣。

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  作者: Qwen | 点赞: 1,712 | 下载: 3,858,503  
  一句话说明：MoE 架构多模态模型（总参35B，激活3B），性价比极高，成为本周下载量冠军（385万+）。

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**  
  作者: google | 点赞: 2,595 | 下载: 9,119,339  
  一句话说明：Google 最新开源多模态对话模型（31B），下载量近千万，集超长上下文与图像理解于一体。

- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)**  
  作者: google | 点赞: 203 | 下载: 66,561  
  一句话说明：Gemma-4-31B-it 的 Assistant 变体，支持任意输入到任意输出（any-to-any），适合通用 AI 助手场景。

- **[google/gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)**  
  作者: google | 点赞: 108 | 下载: 47,749  
  一句话说明：Gemma-4 的 MoE 版（26B总参，4B激活），兼顾性能与效率，Assistant 版专为交互场景优化。

- **[google/gemma-4-E4B-it-assistant](https://huggingface.co/google/gemma-4-E4B-it-assistant)**  
  作者: google | 点赞: 58 | 下载: 51,766  
  一句话说明：极小型 Gemma-4 变体（约4B参数），适合端侧部署，any-to-any 能力使其成为轻量级多模态入口。

- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)**  
  作者: nvidia | 点赞: 272 | 下载: 134,313  
  一句话说明：NVIDIA 推出的 Omni 推理模型（MoE 30B/3B），专注多模态推理，兼容 transformers 生态。

- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)**  
  作者: sensenova | 点赞: 222 | 下载: 4,528  
  一句话说明：商汤科技的多模态 MoT（Mixture of Tokens）模型，统一特征提取与多模态理解。

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  作者: SulphurAI | 点赞: 575 | 下载: 157,648  
  一句话说明：Sulphur 第二代文生视频基础模型，兼容 diffusers，推动开源视频生成发展。

- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)**  
  作者: HiDream-ai | 点赞: 211 | 下载: 3,418  
  一句话说明：基于 Qwen3-VL 的图像编辑/生成模型，“O1”暗示其类“思维链”图像推理能力。

- **[HiDream-ai/HiDream-O1-Image-Dev](https://huggingface.co/HiDream-ai/HiDream-O1-Image-Dev)**  
  作者: HiDream-ai | 点赞: 74 | 下载: 1,367  
  一句话说明：O1-Image 的开发版，用于测试和自定义训练，吸引研究者尝试。

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)**  
  作者: SeeSee21 | 点赞: 302 | 下载: 9,477  
  一句话说明：社区流行的动漫风格文生图模型，同时提供 GGUF 量化版，降低部署门槛。

- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)**  
  作者: TenStrip | 点赞: 212 | 下载: 64,008  
  一句话说明：图生视频模型，基于 LTX 架构，10 步生成高质量视频（类 Eros 风格），下载量快速增长。

- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)**  
  作者: k2-fsa | 点赞: 842 | 下载: 2,224,595  
  一句话说明：零样本多语言语音克隆/语音合成模型，支持多种语言，下载量超 200 万，TTS 生态标杆。

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)**  
  作者: Supertone | 点赞: 73 | 下载: 1,837  
  一句话说明：轻量级 ONNX 语音合成模型，主打高效推理，适合集成到移动端。

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**  
  作者: openai | 点赞: 1,406 | 下载: 190,993  
  一句话说明：OpenAI 开源的隐私检测/过滤模型（token-classification），用于识别敏感信息，社区关注度高。

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)**  
  作者: AngelSlim | 点赞: 161 | 下载: 17,260  
  一句话说明：基于 Hunyuan 的 1.25bit 量化翻译模型，极致压缩后仍保持翻译质量，代表超低比特量化探索。

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
  作者: froggeric | 点赞: 137 | 下载: 0  
  一句话说明：修复 Qwen 聊天模板的工具模型（无下载量下载），帮助开发者正确使用 Jinja 模板，社区实用工具。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)**  
  作者: unsloth | 点赞: 989 | 下载: 2,733,708  
  一句话说明：官方认可的 Qwen3.6-35B-A3B 的 GGUF 量化版，高下载量表明 MoE 模型在消费级显卡上运行的需求旺盛。

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)**  
  作者: unsloth | 点赞: 640 | 下载: 1,468,142  
  一句话说明：Qwen3.6-27B 的 GGUF 版，支持 llama.cpp 等 CPU/GPU 混合推理，降低多模态模型门槛。

- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)**  
  作者: Jackrong | 点赞: 105 | 下载: 67,205  
  一句话说明：社区对 Qwen3.6-35B-A3B 的另一次 GGUF 重新打包，提供不同量化方案，体现社区二次创作活力。

- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  作者: DavidAU | 点赞: 123 | 下载: 197,110  
  一句话说明：对 Qwen3.6-27B 的“异端”未审查微调版，集成代码能力与 Di-IMatrix 量化，吸引特定用户群。

- **[havenoammo/Qwen3.6-27B-MTP-UD-GGUF](https://huggingface.co/havenoammo/Qwen3.6-27B-MTP-UD-GGUF)**  
  作者: havenoammo | 点赞: 65 | 下载: 43,428  
  一句话说明：另一社区版 Qwen3.6-27B GGUF，加入 UD（Unified Decoding）优化，探索推理加速。

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)**  
  作者: SeeSee21 | 点赞: 302 | 下载: 9,477  
  一句话说明：除原版外，该模型也提供 GGUF 量化版，兼顾图像生成质量与边缘设备部署。

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)**  
  作者: AngelSlim | 点赞: 161 | 下载: 17,260  
  一句话说明：同属量化分类，1.25bit 超低比特翻译专用模型，是量化技术前沿探索的代表。

## 生态信号

- **模型家族三分天下**：DeepSeek V4、Google Gemma-4、Qwen 3.6 形成本周最强势的三大家族，三者覆盖纯文本、多模态、MoE 分支，显示头部厂商开源战略持续发力。
- **MoE + 量化 = 普惠推理**：Qwen3.6-35B-A3B 及其 GGUF 衍生版占据了榜单近 1/3 席位，MoE 架构（总参大、激活小）与量化打包（GGUF）的组合，使大模型在消费级硬件上部署成为可能。社区量化活动（unsloth 及个人贡献者）异常活跃。
- **开源权重模型追赶闭源**：DeepSeek-V4-Pro 与 Gemma-4-31B-it 的表现暗示开源模型在综合能力上已接近甚至部分超越闭源（如 GPT-4 同级），但安全工具（privacy-filter）的爆火也说明开源生态仍需补足合规能力。
- **语音/视频生成走向实用**：OmniVoice 下载超 200 万，Sulphur-2-base 与 LTX2.3-10Eros 各有数万下载，零样本语音克隆和文生/图生视频正从研究走向产品。

## 值得探索

1. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**—— 下载量近千万的“全能型”多模态模型，适合直接用于对话、图像理解、长上下文任务，且 Google 提供了多个尺寸和 assistant 变体，值得作为多模态应用的基础模型。

2. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**—— 高性价比 MoE 多模态模型（激活仅 3B），其 GGUF 版本（[unsloth 版](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)）更是下载量超 270 万。对于想在本地部署多模态助手的研究者或开发者，这是当前最平衡的选择。

3. **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)**—— 零样本、多语言语音克隆模型，开源语音合成的新标杆。结合其高下载量和技术壁垒（支持跨语言克隆），值得在语音应用、实时 TTS 或个性化声音合成方向深入尝试。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*