# Hugging Face 热门模型日报 2026-05-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-09 07:22 UTC

---

# Hugging Face 热门模型日报（2026-05-09）

## 今日速览

本周 Hugging Face 榜单呈现三大亮点：**DeepSeek-V4 系列**（Pro 与 Flash）双星闪耀，总下载量接近 200 万；**Qwen3.6** 家族（27B 与 35B-A3B MoE）以千万级下载量继续统治多模态赛道；**Google Gemma-4-31B-it** 单模型下载突破 873 万，成为本周最受欢迎的开放权重模型。社区微调与量化活动异常活跃，多款 uncensored / abliterated 变体和 GGUF 版本登上热门，同时 **OmniVoice** 零样本语音克隆与 **OpenAI privacy-filter** 安全标注模型也显示生态向实用工具延伸的趋势。

## 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

1. **DeepSeek-V4-Pro**  
   [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) · 作者：deepseek-ai  
   👍 3,764 · 📥 1,061,344  
   DeepSeek 最新旗舰对话模型，以超高点赞和百万级下载量证明其在文本生成领域的统治力。

2. **DeepSeek-V4-Flash**  
   [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) · 作者：deepseek-ai  
   👍 1,009 · 📥 848,696  
   V4 的轻量蒸馏版，兼顾效率与质量，成为生产部署的热门选择。

3. **Zyphra/ZAYA1-8B**  
   [链接](https://huggingface.co/Zyphra/ZAYA1-8B) · 作者：Zyphra  
   👍 294 · 📥 6,810  
   8B 参数的新型语言模型，附带 arXiv 论文，学术社区关注度高。

4. **XiaomiMiMo/MiMo-V2.5-Pro**  
   [链接](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro) · 作者：XiaomiMiMo  
   👍 489 · 📥 26,600  
   小米推出的长上下文 Agent 模型，专为复杂任务与长期对话设计。

5. **mistralai/Mistral-Medium-3.5-128B**  
   [链接](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B) · 作者：mistralai  
   👍 305 · 📥 21,300  
   Mistral 中规模旗舰，128B 参数支持英法双语，适配 vLLM 高效推理。

6. **poolside/Laguna-XS.2**  
   [链接](https://huggingface.co/poolside/Laguna-XS.2) · 作者：poolside  
   👍 234 · 📥 18,863  
   poolside 发布的新一代代码生成语言模型，定位开发者工具。

7. **z-lab/Qwen3.6-27B-DFlash**  
   [链接](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash) · 作者：z-lab  
   👍 270 · 📥 30,478  
   基于 Qwen3.6-27B 的推测性解码加速版，降低推理延迟。

8. **z-lab/gemma-4-31B-it-DFlash**  
   [链接](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash) · 作者：z-lab  
   👍 66 · 📥 2,155  
   Gemma-4 的 DFlash 加速版本，面向高效推理场景。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **google/gemma-4-31B-it**  
   [链接](https://huggingface.co/google/gemma-4-31B-it) · 作者：google  
   👍 2,572 · 📥 8,731,301  
   本周下载量冠军，Google 的多模态对话模型，支持图像+文本输入，性能强悍。

2. **Qwen/Qwen3.6-35B-A3B**  
   [链接](https://huggingface.co/qwen/Qwen3.6-35B-A3B) · 作者：Qwen  
   👍 1,682 · 📥 3,363,621  
   MoE 架构多模态模型，35B 总参/3B 激活，效率与能力的标杆。

3. **Qwen/Qwen3.6-27B**  
   [链接](https://huggingface.co/qwen/Qwen3.6-27B) · 作者：Qwen  
   👍 1,195 · 📥 1,958,217  
   Qwen3.6 系列的中杯版本，性价比极高的图像+文本模型。

4. **google/gemma-4-31B-it-assistant**  
   [链接](https://huggingface.co/google/gemma-4-31B-it-assistant) · 作者：google  
   👍 167 · 📥 33,314  
   Gemma-4 的 Assistant 变体，专注于对话助手场景。

5. **google/gemma-4-26B-A4B-it-assistant**  
   [链接](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant) · 作者：google  
   👍 94 · 📥 22,723  
   Gemma-4 的小型 MoE 版本，4B 激活参数，适合资源受限环境。

6. **dealignai/Gemma-4-31B-JANG_4M-CRACK**  
   [链接](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK) · 作者：dealignai  
   👍 1,491 · 📥 156,146  
   Gemma-4 的 abliterated（去审查）版本，因“无限制”特性引发社区热议。

7. **nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16**  
   [链接](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16) · 作者：nvidia  
   👍 265 · 📥 89,837  
   NVIDIA 的通用多模态推理模型，30B 总参/3B 激活，强调推理能力。

8. **sensenova/SenseNova-U1-8B-MoT**  
   [链接](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT) · 作者：sensenova  
   👍 203 · 📥 2,947  
   商汤科技的多模态 MoT（Mixture of Tokens）模型，创新架构。

9. **SulphurAI/Sulphur-2-base**  
   [链接](https://huggingface.co/SulphurAI/Sulphur-2-base) · 作者：SulphurAI  
   👍 457 · 📥 92,968  
   文本到视频生成模型，支持 diffusers 和 GGUF，视频生成领域新星。

10. **SeeSee21/Z-Anime**  
    [链接](https://huggingface.co/SeeSee21/Z-Anime) · 作者：SeeSee21  
    👍 244 · 📥 5,077  
    专攻动漫风格的文本到图像模型，创意社区喜爱。

11. **TenStrip/LTX2.3-10Eros**  
    [链接](https://huggingface.co/TenStrip/LTX2.3-10Eros) · 作者：TenStrip  
    👍 172 · 📥 42,529  
    图像到视频模型，10Eros 版本提升生成质量与细腻度。

12. **k2-fsa/OmniVoice**  
    [链接](https://huggingface.co/k2-fsa/OmniVoice) · 作者：k2-fsa  
    👍 815 · 📥 2,242,587  
    零样本多语言语音克隆模型，支持情感控制，实用工具代表。

13. **AngelSlim/Hy-MT1.5-1.8B-1.25bit**  
    [链接](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit) · 作者：AngelSlim  
    👍 142 · 📥 16,778  
    超低比特量化的翻译模型，1.25bit 压缩，极限压缩实验。

### 🔧 专用模型（代码、数学、医疗、嵌入、安全等）

1. **openai/privacy-filter**  
   [链接](https://huggingface.co/openai/privacy-filter) · 作者：openai  
   👍 1,373 · 📥 173,110  
   OpenAI 发布的隐私过滤模型，基于 token-classification，用于识别敏感信息。

2. **froggeric/Qwen-Fixed-Chat-Templates**  
   [链接](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) · 作者：froggeric  
   👍 114 · 📥 0  
   修复 Qwen 系列聊天模板的工具库，社区基础设施贡献。

### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **unsloth/Qwen3.6-35B-A3B-GGUF**  
   [链接](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF) · 作者：unsloth  
   👍 966 · 📥 2,500,343  
   Qwen3.6-35B-A3B 的 GGUF 量化版，配合 unsloth 生态，本地部署首选。

2. **unsloth/Qwen3.6-27B-GGUF**  
   [链接](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF) · 作者：unsloth  
   👍 627 · 📥 1,312,422  
   Qwen3.6-27B 的 GGUF 版本，下载量巨大，社区广泛使用。

3. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
   [链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) · 作者：HauhauCS  
   👍 588 · 📥 996,892  
   Qwen3.6 MoE 的“无审查激进”微调版，兼具 GGUF 量化，人气极高。

4. **Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF**  
   [链接](https://huggingface.co/Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF) · 作者：Jackrong  
   👍 108 · 📥 128,635  
   融合 Qwen3.5 与 DeepSeek-V4 能力的混合 GGUF 模型，小巧实用。

5. **Jackrong/Qwopus3.6-35B-A3B-v1-GGUF**  
   [链接](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF) · 作者：Jackrong  
   👍 87 · 📥 18,981  
   Qwen3.6 MoE 的另一款 GGUF 量化变体，提供更多量化选项。

6. **DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF**  
   [链接](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF) · 作者：DavidAU  
   👍 105 · 📥 143,853  
   Qwen3.6-27B 的极端无限制微调版，名字即说明其定位——完全 uncensored。

7. **Jackrong/Qwen3.6-35B-A3B-v1-GGUF**（原序号16，实际为 Qwopus 变体，已计入）

## 生态信号

- **Qwen3.6 与 Gemma-4 双核驱动**：两大模型家族占据下载量 TOP5，且社区围绕它们迅速衍生出大量量化（GGUF）、微调（uncensored/abliterated）版本，形成生态飞轮。
- **MoE 成为多模态标配**：Qwen3.6-35B-A3B、Gemma-4-26B-A4B、Nemotron-3-Nano-Omni 均采用 MoE 架构，以有限激活参数实现大模型能力，兼顾效率与效果。
- **“去审查”模型持续爆发**：Gemma-4-JANG_4M-CRACK、Qwen3.6 uncensored 变体点赞与下载量均高企，反映社区对内容自由度的强烈需求。
- **开源权重路线稳固**：所有热门模型均提供开放权重（safetensors/GGUF），闭源模型未上榜，开源社区活力持续。
- **量化活动空前活跃**：GGUF 版本占比接近 1/3，unsolth、Jackrong 等团队成为生态基础设施提供者，推动大模型平民化。

## 值得探索

1. **nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16**  
   强推理能力的 3B 激活多模态模型，适合边端设备部署，NVIDIA 出品品质保证。

2. **k2-fsa/OmniVoice**  
   零样本多语言语音克隆，支持情感控制，下载量超 224 万，实用性极强，适合语音合成研究者或产品开发者。

3. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
   最高效 MoE 模型的 uncensored + GGUF 版本，若需探索无限制对话场景，这是当前最佳起点。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*