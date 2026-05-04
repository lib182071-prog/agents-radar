# Hugging Face 热门模型日报 2026-05-04

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-04 08:44 UTC

---

# 🤗 Hugging Face 热门模型日报 | 2026-05-04

## 今日速览

本周 Hugging Face 榜单亮点频出：**DeepSeek-V4-Pro** 以 3,492 赞登顶，延续 DeepSeek 旗舰系列的强势地位；**Google Gemma-4-31B-it** 下载量突破 800 万，多模态能力备受青睐；**Qwen 3.6 系列**（27B/35B-A3B）与 **NVIDIA Nemotron-3 Nano Omni** 展现了 MoE 与 any-to-any 推理的进化方向。社区层面，**unsloth** 的 GGUF 量化版本下载量巨大，**dealignai** 的 uncensored 微调模型也引发关注。此外，小米的 **MiMo-V2.5-Pro** 主打长上下文智能体，值得留意。

---

## 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 👍 3,492 | 📥 534,942  
  DeepSeek 最新旗舰文本生成模型，延续 V4 架构，对话与指令跟随能力突出，本周热度最高。

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai | 👍 934 | 📥 489,465  
  V4 系列的轻量快速版本，适合部署，下载量接近 50 万。

- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)** — XiaomiMiMo | 👍 416 | 📥 11,812  
  小米出品，主打长上下文与智能体能力，是 MiMo V2.5 的 Pro 增强版，为 agent 场景优化。

- **[mistralai/Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)** — mistralai | 👍 248 | 📥 11,950  
  Mistral 中规模 128B 模型，支持英文和法文，兼容 vLLM。

- **[talkie-lm/talkie-1930-13b-it](https://huggingface.co/talkie-lm/talkie-1930-13b-it)** — talkie-lm | 👍 216 | 📥 0  
  基于 talkie-1930-13b-base 的指令微调版本，Apache-2.0 许可，适合研究。

- **[inclusionAI/Ling-2.6-flash](https://huggingface.co/inclusionAI/Ling-2.6-flash)** — inclusionAI | 👍 271 | 📥 1,141  
  Ling 2.6 的快速推理版，bailing_hybrid 架构，对话能力出色。

- **[inclusionAI/Ling-2.6-1T](https://huggingface.co/inclusionAI/Ling-2.6-1T)** — inclusionAI | 👍 219 | 📥 747  
  Ling 2.6 的 1T 参数超大模型，专注于文本生成与对话。

- **[poolside/Laguna-XS.2](https://huggingface.co/poolside/Laguna-XS.2)** — poolside | 👍 200 | 📥 10,357  
  poolside 的代码生成模型（推测，标签 laguna），XS 轻量版，支持 vLLM。

- **[ibm-granite/granite-4.1-8b](https://huggingface.co/ibm-granite/granite-4.1-8b)** — ibm-granite | 👍 144 | 📥 18,310  
  IBM Granite 4.1 系列 8B 语言模型，企业级文本生成，注重安全与可解释性。

- **[ibm-granite/granite-4.1-30b](https://huggingface.co/ibm-granite/granite-4.1-30b)** — ibm-granite | 👍 88 | 📥 4,094  
  Granite 4.1 的 30B 版本，语言能力更强。

---

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — Qwen | 👍 1,598 | 📥 2,726,360  
  Qwen 3.6 系列 MoE 多模态模型（35B 总参数，3B 激活），支持图文理解，下载量极高。

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen | 👍 1,105 | 📥 1,334,241  
  Qwen 3.6 的 27B 密集多模态模型，兼顾对话与图文能力。

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | 👍 2,496 | 📥 8,042,257  
  Google Gemma 4 的指令微调版，31B 参数、多模态（图文），下载量突破 800 万，是目前最受欢迎的开源多模态模型之一。

- **[moonshotai/Kimi-K2.6](https://huggingface.co/moonshotai/Kimi-K2.6)** — moonshotai | 👍 1,192 | 📥 825,320  
  月之暗面 Kimi K2.6，图文多模态模型，支持压缩张量，下载量超 82 万。

- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** — nvidia | 👍 210 | 📥 40,403  
  NVIDIA 最新 any-to-any 模型（30B 总参数，3B 激活），支持文本、图像、音频等多模态推理。

- **[XiaomiMiMo/MiMo-V2.5](https://huggingface.co/XiaomiMiMo/MiMo-V2.5)** — XiaomiMiMo | 👍 201 | 📥 51,554  
  小米 MiMo V2.5 基础版，多模态（视觉-语言-音频），通用感知能力。

- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** — sensenova | 👍 131 | 📥 1,714  
  商汤 SenseNova 8B MoT（混合Transformer），any-to-any 多模态模型，neo_chat 对话。

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI | 👍 138 | 📥 20,187  
  文本生成视频的基础模型，基于 diffusers，支持 GGUF 量化，可用于视频生成研究。

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** — SeeSee21 | 👍 120 | 📥 2,622  
  动漫风格文生图模型，支持 diffusers 和 GGUF 格式。

---

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — openai | 👍 1,241 | 📥 132,595  
  OpenAI 发布的隐私过滤模型，用于 token 级分类（如识别 PII），标签包含 ONNX、safetensors，社区关注度高。

- **[ibm-granite/granite-embedding-97m-multilingual-r2](https://huggingface.co/ibm-granite/granite-embedding-97m-multilingual-r2)** — ibm-granite | 👍 75 | 📥 2,191  
  IBM 的多语言嵌入模型（97M），基于 ModernBERT，用于特征提取。

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** — AngelSlim | 👍 83 | 📥 16,307  
  机器翻译模型，1.8B 参数，采用 1.25bit 极致量化，适合低资源部署。

---

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[dealignai/Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** — dealignai | 👍 1,460 | 📥 203,362  
  基于 Gemma-4-31B 的未审查（uncensored）微调版，采用 abliterated 技术，社区热度极高。

- **[HauhauCS/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 👍 273 | 📥 350,841  
  Qwen3.6-27B 的未审查激进微调版，GGUF 格式，下载量超 35 万。

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** — unsloth | 👍 561 | 📥 1,092,141  
  unsloth 对 Qwen3.6-27B 的 GGUF 量化版本，下载超百万，适合本地推理。

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** — unsloth | 👍 904 | 📥 2,174,698  
  Qwen3.6-35B-A3B 的 GGUF 量化版，下载量超 217 万，表现亮眼。

- **[unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF](https://huggingface.co/unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF)** — unsloth | 👍 98 | 📥 44,790  
  Nemotron-3 Omni 的 GGUF 量化版，便于多模态模型本地运行。

- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** — z-lab | 👍 219 | 📥 23,407  
  Qwen3.6-27B 的 DFlash 蒸馏/量化版本，优化推理速度，特征提取可用。

---

## 生态信号

- **模型家族势头**：**Qwen 3.6 系列**（27B/35B-A3B）成为本周最活跃的族系，加上 unsloth 的 GGUF 量化版，总下载量超 700 万。**Gemma 4** 凭借 Google 背书与开源规模，下载量突破 800 万。**DeepSeek V4** 系列虽下载量不如前两者，但点赞数领先，表明社区关注度高。**Nemotron-3 Nano Omni** 系列则代表了 any-to-any 多模态推理的新方向。
- **开源 vs 闭源**：本周除 OpenAI 发布了一个小型隐私过滤模型外，主流大模型（DeepSeek、Qwen、Gemma、Mistral、NVIDIA、小米）均为开源权重，显示开源社区生态持续繁荣。闭源厂商如 Google、Mistral 等也在积极开源权重，竞争白热化。
- **量化与微调活动**：**unsloth** 几乎同步为所有热门模型提供 GGUF 版本，极大降低了本地部署门槛；社区 **uncensored** 微调（如 dealignai、HauhauCS）下载量可观，反映用户对内容无限制的偏好。此外，**1.25bit 量化**（AngelSlim）作为极致压缩尝试也值得关注。

---

## 值得探索

1. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**  
   理由：Google 最新多模态模型，31B 参数，下载量突破 800 万，性能平衡且生态支持完善（已有大量微调与量化版本），适合作为多模态应用的起点。

2. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
   理由：Qwen 3.6 的 MoE 多模态版本，3B 激活参数实现高效推理，下载量超 270 万，是低成本部署多模态能力的理想选择。

3. **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)**  
   理由：NVIDIA 的 any-to-any 多模态推理模型，支持文本、图像、音频统一理解，代表下一代多模态 agent 的发展方向，值得研究测试。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*