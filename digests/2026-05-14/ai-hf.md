# Hugging Face 热门模型日报 2026-05-14

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-14 09:39 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年5月14日**

#### **今日速览**

今日Hugging Face榜单竞争激烈，**DeepSeek** 凭借其旗舰模型 **DeepSeek-V4-Pro** 以近4000点赞的绝对优势登顶，但其生态位正受到来自 **Qwen3.6** 系列和 **Google Gemma-4** 系列的强力挑战。Qwen3.6家族发布了多个尺寸的基座、MoE及GGUF量化版本，形成了强大的“模型矩阵”，下载量惊人。值得关注的是，**多模态生成** 模型热度飙升，**SulphurAI** 的文本生成视频模型和 **HiDream-ai** 的“思维链”图像生成模型均进入前十。此外，**Unsloth** 社区持续输出高质量量化模型，成为推动模型平民化部署的关键力量。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **deepseek-ai/DeepSeek-V4-Pro** (text-generation)  
  `deepseek-ai` | 👍 3,935 | 📥 2,588,118  
  说明：本周“点赞王”，DeepSeek系列最新旗舰，综合性能达到新高度，代表着开源大模型向顶尖闭源模型发起的最强冲击。

- **deepseek-ai/DeepSeek-V4-Flash** (text-generation)  
  `deepseek-ai` | 👍 1,077 | 📥 1,526,638  
  说明：DeepSeek-V4的“闪电版”，主打快速推理，与旗舰版形成高低搭配，满足不同场景需求。

- **Qwen/Qwen3.6-27B** (image-text-to-text)  
  `Qwen` | 👍 1,276 | 📥 2,940,046  
  说明：Qwen3.6系列的主力型号，27B规模的“视觉语言模型”，性能和实用性兼备，下载量极高。

- **google/gemma-4-31B-it** (image-text-to-text)  
  `google` | 👍 2,630 | 📥 9,793,704  
  说明：Google Gemma-4系列的旗舰指令微调版，31B参数在多项基准上表现出色，下载量逼近千万，是本周最受欢迎的开源模型之一。

- **google/gemma-4-31B-it-assistant** (any-to-any)  
  `google` | 👍 232 | 📥 109,600  
  说明：Gemma-4的“助手”版本，具备任意模态输入输出能力，代表多模态融合的前沿方向。

- **sensenova/SenseNova-U1-8B-MoT** (any-to-any)  
  `sensenova` | 👍 247 | 📥 9,377  
  说明：商汤科技出品，8B多模态MoE模型，在较小参数规模下追求性能与模态兼容性的平衡。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **SulphurAI/Sulphur-2-base** (text-to-video)  
  `SulphurAI` | 👍 865 | 📥 627,368  
  说明：SulphurAI的文本生成视频基础模型，代表了当前AI视频生成的先进水平，下载量巨大，预示视频生成热潮持续。

- **HiDream-ai/HiDream-O1-Image** (image-text-to-image)  
  `HiDream-ai` | 👍 310 | 📥 9,858  
  说明：引入“思维链(CoT)”机制的图像生成模型，突破了传统扩散模型“一次成图”的限制，代表了一种新范式。

- **SeeSee21/Z-Anime** (text-to-image)  
  `SeeSee21` | 👍 352 | 📥 12,061  
  说明：专注于二次元动漫风格生成的社区微调模型，展现了社区在垂类应用上的创造力。

- **TenStrip/LTX2.3-10Eros** (image-to-video)  
  `TenStrip` | 👍 250 | 📥 90,647  
  说明：图像生成视频模型，LTX系列的社区微调版，在图像到视频动效生成领域具有实用价值。

- **Supertone/supertonic-3** (text-to-speech)  
  `Supertone` | 👍 173 | 📥 9,482  
  说明：高质量的文本转语音模型，展现了AI语音合成领域的持续进步。

- **k2-fsa/OmniVoice** (text-to-speech)  
  `k2-fsa` | 👍 872 | 📥 2,224,252  
  说明：零样本、多语言的语音克隆与生成模型，支持多种语言，下载量超两百万，是语音生成领域的现象级模型。

- **RuneXX/LTX-2.3-Workflows** (image-to-video)  
  `RuneXX` | 👍 542 | 📥 0  
  说明：虽是工作流而非模型，但点赞极高，反映了社区对LTX系列视频生成工具链的旺盛需求。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **openai/privacy-filter** (token-classification)  
  `openai` | 👍 1,433 | 📥 219,969  
  说明：OpenAI官方推出的隐私过滤模型，用于识别和标记敏感信息，是AI应用安全合规的重要工具，备受开发者关注。

- **jackxinning/Leanly_AI** (question-answering)  
  `jackxinning` | 👍 102 | 📥 10,668  
  说明：专注于中英文医疗领域的问答模型，基于GGUF格式，方便本地部署，展示了LLM在垂直行业的应用潜力。

- **AngelSlim/Hy-MT1.5-1.8B-1.25bit** (translation)  
  `AngelSlim` | 👍 170 | 📥 17,480  
  说明：极低比特量化（1.25bit）的翻译模型，展示了极致的模型压缩技术，为边缘端部署提供了思路。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **unsloth/Qwen3.6-35B-A3B-GGUF** (image-text-to-text)  
  `unsloth` | 👍 1,026 | 📥 3,001,877  
  说明：Qwen3.6 MoE模型的GGUF量化版，由知名量化社区Unsloth出品。它将350亿参数的MoE模型压缩至可本地运行，是本周下载量最高的量化模型之一。

- **Jiunsong/supergemma4-26b-uncensored-gguf-v2** (text-generation)  
  `Jiunsong` | 👍 576 | 📥 287,048  
  说明：Gemma-4的社区微调“无审查”版，代表了社区对模型“自由化”的持续追求，下载量很高。

- **antirez/deepseek-v4-gguf** (text-generation)  
  `antirez` | 👍 103 | 📥 212,601  
  说明：由知名开发者antirez发布的DeepSeek-V4 GGUF量化版，为想本地体验顶级模型性能的用户提供了便捷入口。

- **DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF** (image-text-to-text)  
  `DavidAU` | 👍 150 | 📥 261,416  
  说明：一个名字超长的社区微调版，集“无审查”、“代码增强”等多重buff于一身，是社区“赛博朋克”式模型改造的典型代表。

- 其他同系列GGUF模型：**unsloth/Qwen3.6-27B-MTP-GGUF** (👍 117)、**unsloth/Qwen3.6-27B-GGUF** (👍 674)、**Jackrong/Qwopus3.6-35B-A3B-v1-GGUF** (👍 121) 等，共同构成了庞大的Qwen量化生态。

---

#### **生态信号**

1.  **“三国鼎立”格局初现**：本周榜单清晰地呈现出 **DeepSeek、Qwen、Google (Gemma-4)** 三大模型家族的统治地位。Qwen 凭借从27B到35B（MoE）的完整产品线，以及Unsloth等社区提供的海量量化版本，构建了最庞大的用户生态；DeepSeek凭借V4系列的技术领先性占据高端；Google Gemma-4则以惊人的下载量证明其开源影响力。

2.  **量化成为必备能力，而非可选**：排名前30的模型中，标注`gguf`标签的超过10个，且下载量普遍高于同型号的Safetensors版本。这印证了“降本增效”已成为当前AI落地的核心诉求。社区的核心工作已从“训练模型”转向“高效部署模型”，量化是其中最关键的一环。

3.  **社区微调趋向“解禁”与“专用”**：“uncensored”（无审查）模型频繁出现，反映出社区对内容限制的普遍需求。同时，大量针对特定领域（如医疗、动漫）或特定任务（如视频生成、语音克隆）的微调模型涌现，表明大模型生态正在从通用走向专业化、个性化。

---

#### **值得探索**

1.  **deepseek-ai/DeepSeek-V4-Pro**: 作为本周的“点赞之巅”，它代表了当前开源大模型的最高水平。无论是进行技术研究、性能评测，还是作为企业级应用的基座模型，它都是本周最不容错过的模型。  [点此探索](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)

2.  **Qwen/Qwen3.6-35B-A3B**: Qwen3.6系列的MoE旗舰。如果你想同时拥有大模型的“容量”（35B总参）和推理的“速度”（仅激活3B参），这个模型是最佳选择。其背后的MoE架构是未来大模型发展的关键方向。  [点此探索](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)

3.  **k2-fsa/OmniVoice**: 如果你对AI语音合成、克隆感兴趣，这个模型绝对值得一试。它完美的体现了“零样本”和“多语言”两大特性，且下载量证明了其强大的实用性。  [点此探索](https://huggingface.co/k2-fsa/OmniVoice)

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*