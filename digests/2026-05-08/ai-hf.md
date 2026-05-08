# Hugging Face 热门模型日报 2026-05-08

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-08 06:18 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的2026年5月8日数据生成的《Hugging Face 热门模型日报》。

---

### 📅 Hugging Face 热门模型日报 | 2026-05-08

#### 1. 今日速览

本周Hugging Face生态呈现出“巨头争霸、多模态爆发”的态势。**DeepSeek-V4-Pro** 以绝对优势领跑热度榜，但**Google Gemma-4** 系列凭借其庞大的下载量（尤其是31B版本）证明了其作为基础设施级模型的地位。与此同时，**Qwen3.6** 家族异军突起，特别是其MoE变体（35B-A3B）在下载量上超越众多对手，成为新一代“性价比之王”。此外，围绕这些主力模型的社区微调、量化（主要是GGUF）以及“无审查”版本异常活跃，显示出强大的下游生态活力。

#### 2. 热门模型分类解析

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者: deepseek-ai | 点赞: 3,731 | 下载: 946,264  
  **一句话**: DeepSeek最新旗舰级文本生成模型，以绝对优势领跑本周热度榜，下载量接近百万，代表了当前开源LLM的顶尖水平。

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  作者: deepseek-ai | 点赞: 987 | 下载: 751,333  
  **一句话**: DeepSeek-V4的快速推理版本，在保持高性能的同时优化了推理速度，是Pro版的有力补充，同样获得了社区的高度关注。

- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)**  
  作者: XiaomiMiMo | 点赞: 477 | 下载: 20,905  
  **一句话**: 小米发布的新一代长上下文模型，主打Agent能力，是端侧与云端协同部署的有力竞争者。

- **[poolside/Laguna-XS.2](https://huggingface.co/poolside/Laguna-XS.2)**  
  作者: poolside | 点赞: 232 | 下载: 16,792  
  **一句话**: 专注于软件工程场景的代码生成模型，在特定垂直领域展现出强大潜力。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**  
  作者: google | 点赞: 2,560 | 下载: 8,594,149  
  **一句话**: Google的旗舰多模态模型，下载量超过850万，是本周当之无愧的“下载之王”，证明了其强大的通用性与社区信赖度。

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  作者: Qwen | 点赞: 1,662 | 下载: 3,211,156  
  **一句话**: 通义千问3.6系列的MoE版本，以35B总参和3B激活的“高能效比”策略，在图像理解与对话任务上表现突出，下载量超320万。

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
  作者: Qwen | 点赞: 1,181 | 下载: 1,771,851  
  **一句话**: Qwen3.6系列的Dense版本，与MoE版本形成互补，是图像理解领域的另一款热门选择。

- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)**  
  作者: k2-fsa | 点赞: 802 | 下载: 2,238,817  
  **一句话**: 一款支持零样本、多语言嗓音克隆的语音合成模型，引爆了语音生成领域，下载量超过220万。

- **[google/gemma-4-E4B-it](https://huggingface.co/google/gemma-4-E4B-it)**  
  作者: google | 点赞: 946 | 下载: 5,494,056  
  **一句话**: Gemma-4的极致轻量版，通过极低的参数量实现了“any-to-any”能力，吸引了大量资源有限的开发者，下载量接近550万。

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  作者: SulphurAI | 点赞: 395 | 下载: 71,149  
  **一句话**: 本周表现最亮眼的文生视频基础模型之一，标志着视频生成领域正在加速追赶图像生成。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**  
  作者: openai | 点赞: 1,351 | 下载: 165,240  
  **一句话**: OpenAI开源的隐私过滤模型，用于识别和屏蔽敏感信息，是AI应用合规部署的关键组件，关注度极高。

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)**  
  作者: Zyphra | 点赞: 217 | 下载: 539  
  **一句话**: 一款Apache-2.0许可的8B模型，虽尚在早期，但已进入热门榜，背后可能预示着新的高效架构或训练方法。

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)**  
  作者: AngelSlim | 点赞: 120 | 下载: 16,631  
  **一句话**: 一款极端量化的翻译模型，展示了将大模型压缩到极小体积（1.25bit）以在边缘设备运行的可能性。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)**  
  作者: unsloth | 点赞: 956 | 下载: 2,417,319  
  **一句话**: Qwen3.6-35B-A3B的官方推荐GGUF量化版，下载量超过240万，是本地部署和低资源场景下的首选。

- **[dealignai/Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)**  
  作者: dealignai | 点赞: 1,487 | 下载: 169,511  
  **一句话**: 基于Gemma-4-31B的“去对齐”无审查微调版，社区对此类追求开放性的模型需求旺盛。

- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  作者: DavidAU | 点赞: 94 | 下载: 126,660  
  **一句话**: 社区对Qwen3.6-27B进行极致量化与“无审查”微调的产物，名称虽长但反映了社区当前的核心玩法：量化+个性微调。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  作者: HauhauCS | 点赞: 576 | 下载: 973,262  
  **一句话**: 基于Qwen3.6-35B-A3B的“激进”风格无审查版本，下载量接近百万，显示了MoE模型在社区微调中的巨大潜力。

#### 3. 生态信号

本周模型生态呈现以下趋势：
- **模型家族三分天下**: 热度与下载量被 **Qwen 3.6**、**Google Gemma-4** 和 **DeepSeek V4** 三大系列高度集中。这标志着开源大模型已进入头部巨头“拼生态、秀肌肉”的阶段。
- **开源已成主流共识**: 榜单前五名完全被开源模型占据，且权重完全开放（safetensors/gguf）。未见闭源或API-only模型，说明社区对可控、可私有化部署的开源权重有强烈偏好。
- **量化与“去审查”是社区核心驱动力**: 围绕GGUF的量化版本占据了榜单大量位置，体现了本地部署的旺盛需求。同时，多个“uncensored”微调版获得了极高关注，表明社区对模型输出自由度的追求强烈。

#### 4. 值得探索

1.  **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**： **理由**: 本周下载量冠军，最全面的多模态基础模型之一。极高的下载量意味着最丰富的社区资源、教程和下游微调版本，是搭建高级应用的基础底座。
2.  **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**： **理由**: “高性价比”的MoE架构旗舰。在保持与Dense模型相近总参数量的同时，大幅度降低激活参数，实现了推理成本和性能的理想平衡，是未来大模型的重要发展方向。
3.  **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)**： **理由**: 新一代语音合成标杆。零样本、多语言、嗓音克隆的结合极具吸引力，有望改变内容创作、虚拟角色、无障碍访问等众多领域的范式，值得所有相关领域的研究者深入测试。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*