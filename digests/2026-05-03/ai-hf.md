# Hugging Face 热门模型日报 2026-05-03

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-03 03:50 UTC

---

# Hugging Face 热门模型日报（2026-05-03）

## 今日速览

本周 Hugging Face 榜单呈现三大亮点：**DeepSeek-V4 Pro** 以 3,420 点赞登顶，延续 DeepSeek 系列在文本生成领域的强势地位；**Google Gemma-4-31B-it** 凭借 7.7M 下载量成为社区最活跃多模态模型，同时被社区快速制作 uncensored 版；**Qwen3.6 家族**（27B/35B-A3B MoE）展现极强生态渗透力，官方与量化版（GGUF、DFlash）包揽多个高位。此外，**NVIDIA Nemotron-3 Nano Omni** 以“any-to-any”全模态架构亮相，**小米 MiMo-V2.5**、**月之暗面 Kimi-K2.6** 等国产多模态模型也跻身热门。社区微调（uncensored、abliterated）和量化（GGUF、NVFP4）活动持续活跃，成为模型传播的重要加速器。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

1. **deepseek-ai/DeepSeek-V4-Pro**  
   [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)  
   **作者**：deepseek-ai | **点赞**：3,420 | **下载**：381,587  
   *当前周赞最高的模型，DeepSeek V4 旗舰版，专注文本生成与对话，权重完全开源。*

2. **deepseek-ai/DeepSeek-V4-Flash**  
   [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)  
   **作者**：deepseek-ai | **点赞**：921 | **下载**：345,885  
   *V4 系列的快速推理变体，兼顾性能与效率，下载量紧随 Pro 之后。*

3. **mistralai/Mistral-Medium-3.5-128B**  
   [链接](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)  
   **作者**：mistralai | **点赞**：224 | **下载**：8,492  
   *Mistral 中量级 128B 模型，支持英法双语，面向企业级部署。*

4. **poolside/Laguna-XS.2**  
   [链接](https://huggingface.co/poolside/Laguna-XS.2)  
   **作者**：poolside | **点赞**：192 | **下载**：7,573  
   *专注代码生成的语言模型，Laguna 系列轻量版，标签含 vLLM 优化。*

5. **inclusionAI/Ling-2.6-1T**  
   [链接](https://huggingface.co/inclusionAI/Ling-2.6-1T)  
   **作者**：inclusionAI | **点赞**：101 | **下载**：535  
   *1T 参数级别的超大语言模型，Ling 系列新一代旗舰，采用 hybrid 架构。*

6. **inclusionAI/Ling-2.6-flash**  
   [链接](https://huggingface.co/inclusionAI/Ling-2.6-flash)  
   **作者**：inclusionAI | **点赞**：146 | **下载**：943  
   *Ling-2.6 的快速推理版本，bailing_hybrid 架构，适合低延迟场景。*

7. **ibm-granite/granite-4.1-8b**  
   [链接](https://huggingface.co/ibm-granite/granite-4.1-8b)  
   **作者**：ibm-granite | **点赞**：133 | **下载**：16,079  
   *IBM Granite 4.1 系列 8B 版本，专注企业级文本生成与语言理解。*

8. **ibm-granite/granite-4.1-30b**  
   [链接](https://huggingface.co/ibm-granite/granite-4.1-30b)  
   **作者**：ibm-granite | **点赞**：79 | **下载**：3,072  
   *Granite 4.1 的 30B 中量级模型，兼顾能力与部署成本。*

9. **talkie-lm/talkie-1930-13b-it**  
   [链接](https://huggingface.co/talkie-lm/talkie-1930-13b-it)  
   **作者**：talkie-lm | **点赞**：204 | **下载**：0  
   *新晋对话模型，13B 指令微调版，尽管下载数暂为 0，但关注度较高。*

10. **talkie-lm/talkie-1930-13b-base**  
    [链接](https://huggingface.co/talkie-lm/talkie-1930-13b-base)  
    **作者**：talkie-lm | **点赞**：67 | **下载**：0  
    *同一系列的基座模型，Apache-2.0 许可，聚焦英文场景。*

---

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **google/gemma-4-31B-it**  
   [链接](https://huggingface.co/google/gemma-4-31B-it)  
   **作者**：google | **点赞**：2,481 | **下载**：7,776,034  
   *Google 最新多模态指令模型，30B 级参数，下载量碾压全场，社区热度极高。*

2. **Qwen/Qwen3.6-35B-A3B**  
   [链接](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)  
   **作者**：Qwen | **点赞**：1,574 | **下载**：2,397,446  
   *Qwen3.6 系列的 MoE 版本（35B 总参/3B 激活），图像+文本对话，效率与能力平衡的标杆。*

3. **moonshotai/Kimi-K2.6**  
   [链接](https://huggingface.co/moonshotai/Kimi-K2.6)  
   **作者**：moonshotai | **点赞**：1,183 | **下载**：699,348  
   *月之暗面 Kimi 多模态升级版，图像-文本任务，支持压缩张量等优化。*

4. **Qwen/Qwen3.6-27B**  
   [链接](https://huggingface.co/Qwen/Qwen3.6-27B)  
   **作者**：Qwen | **点赞**：1,081 | **下载**：1,070,778  
   *Qwen3.6 标准 27B 模型，image-text-to-text 任务，下载数破百万。*

5. **XiaomiMiMo/MiMo-V2.5-Pro**  
   [链接](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)  
   **作者**：XiaomiMiMo | **点赞**：382 | **下载**：9,914  
   *小米 MiMo 系列 Pro 版，主打长上下文与 Agent 能力，多模态理解增强。*

6. **XiaomiMiMo/MiMo-V2.5**  
   [链接](https://huggingface.co/XiaomiMiMo/MiMo-V2.5)  
   **作者**：XiaomiMiMo | **点赞**：192 | **下载**：28,323  
   *小米多模态基座模型，支持视觉-语言和音频输入，家族化发展。*

7. **nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16**  
   [链接](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)  
   **作者**：nvidia | **点赞**：199 | **下载**：37,418  
   *NVIDIA 第三代全模态（any-to-any）模型，30B A3B MoE 架构，支持推理。*

8. **nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4**  
   [链接](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4)  
   **作者**：nvidia | **点赞**：71 | **下载**：180,012  
   *同上模型的 4-bit 浮点量化版，推理效率大幅提升，下载量已超原版。*

9. **sensenova/SenseNova-U1-8B-MoT**  
   [链接](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)  
   **作者**：sensenova | **点赞**：120 | **下载**：1,308  
   *商汤 SenseNova 8B 全模态模型（MoT），支持多种输入输出。*

10. **SeeSee21/Z-Anime**  
    [链接](https://huggingface.co/SeeSee21/Z-Anime)  
    **作者**：SeeSee21 | **点赞**：73 | **下载**：859  
    *文本到图像生成模型，专注动漫风格，支持 diffusers 和 GGUF。*

---

### 🔧 专用模型（代码、数学、医疗、嵌入）

1. **openai/privacy-filter**  
   [链接](https://huggingface.co/openai/privacy-filter)  
   **作者**：openai | **点赞**：1,212 | **下载**：99,399  
   *OpenAI 发布的隐私过滤模型（token-classification），用于识别和屏蔽敏感信息，ONNX 优化。*

2. **ibm-granite/granite-embedding-97m-multilingual-r2**  
   [链接](https://huggingface.co/ibm-granite/granite-embedding-97m-multilingual-r2)  
   **作者**：ibm-granite | **点赞**：68 | **下载**：1,598  
   *IBM 多语言嵌入模型，97M 参数，基于 ModernBERT 架构，支持 Sentence-Transformers、ONNX。*

3. **AngelSlim/Hy-MT1.5-1.8B-1.25bit**  
   [链接](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)  
   **作者**：AngelSlim | **点赞**：78 | **下载**：487  
   *1.8B 参数翻译模型，1.25bit 极致量化（Hunyuan 架构），适合边缘部署。*

---

### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **unsloth/Qwen3.6-35B-A3B-GGUF**  
   [链接](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)  
   **作者**：unsloth | **点赞**：895 | **下载**：2,001,316  
   *Qwen3.6 MoE 的 GGUF 量化版，由 unsloth 制作，下载量已超 200 万，社区最热量化模型之一。*

2. **unsloth/Qwen3.6-27B-GGUF**  
   [链接](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)  
   **作者**：unsloth | **点赞**：545 | **下载**：983,535  
   *Qwen3.6 27B 的 GGUF 版，与 MoE 版形成高低搭配，广泛用于本地推理。*

3. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**  
   [链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)  
   **作者**：HauhauCS | **点赞**：530 | **下载**：766,075  
   *Qwen3.6 MoE 的去限制（uncensored）微调版，GGUF 格式，下载近 77 万。*

4. **HauhauCS/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive**  
   [链接](https://huggingface.co/HauhauCS/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive)  
   **作者**：HauhauCS | **点赞**：264 | **下载**：303,358  
   *同上，27B 版本的 uncensored 版，GGUF 量化。*

5. **dealignai/Gemma-4-31B-JANG_4M-CRACK**  
   [链接](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)  
   **作者**：dealignai | **点赞**：1,444 | **下载**：199,500  
   *Gemma-4-31B 的 uncensored/abliterated 微调版，同时提供 MLX 和 safetensors 格式，周赞超 1,400。*

6. **z-lab/Qwen3.6-27B-DFlash**  
   [链接](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)  
   **作者**：z-lab | **点赞**：206 | **下载**：17,016  
   *Qwen3.6 27B 的 DFlash 蒸馏+量化版，优化推理速度。*

7. **unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF**  
   [链接](https://huggingface.co/unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF)  
   **作者**：unsloth | **点赞**：92 | **下载**：37,663  
   *NVIDIA Nemotron-3 全模态模型的 GGUF 量化版，方便本地部署。*

8. **nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4**  
   [链接](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4)  
   **作者**：nvidia | **点赞**：71 | **下载**：180,012  
   *官方提供的 4-bit 浮点量化版本，已在上面多模态中列出，此处再次强调其量化属性。*

---

## 生态信号

- **家族势头**：**Qwen3.6** 家族（27B、35B-A3B）和 **Gemma-4** 是本周两大爆款生态。Qwen 凭借官方+社区微调+量化多版本覆盖，形成“原版→GGUF→uncensored→DFlash”全链条；Gemma-4 则以超高下载量（7.7M）和 uncensored 版高热（点赞 1,444）成为开源多模态新标杆。**DeepSeek V4** 虽在点赞数领先，但下载量相对平稳，生态拓展潜力待观察。
- **开源 vs 闭源**：除 OpenAI 发布轻量级隐私过滤器外，头部模型均为开源权重。Google、NVIDIA、小米、月之暗面等大厂继续拥抱开源，且模型规模和能力持续升级（1T 参数、MoE、全模态）。闭源模型（如 GPT 系列）缺席榜单，开源生态加速侵蚀商业模型的关注度。
- **量化与微调**：**unsloth** 成为众望所归的量化引擎，其制作的 GGUF 版下载量总和超过 300 万。**HauhauCS** 和 **dealignai** 则以 uncensored/abliterated 作为差异化切入点，迅速积累人气。值得注意的是，**NVFP4** 量化（NVIDIA 官方）已出现在 large-scale 模型上，预示未来硬件级量化将成为新趋势。

---

## 值得探索

1. **deepseek-ai/DeepSeek-V4-Pro** — 本周点赞王，代表 DeepSeek 最新文本生成能力，适合评测基准或作为对话系统的基座。
2. **Qwen/Qwen3.6-35B-A3B** — MoE 架构 + 多模态 + 高下载量（240 万），是研究高效多模态融合和 MoE 稀疏推理的优质样本。
3. **nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16** — 全模态（any-to-any）新范式，30B MoE 结构，探索多模态融合的边界，官方同时提供量化版方便实验。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*