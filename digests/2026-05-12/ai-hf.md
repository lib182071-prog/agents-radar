# Hugging Face 热门模型日报 2026-05-12

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-12 09:49 UTC

---

# Hugging Face 热门模型日报 (2026-05-12)

## 今日速览
本周 Hugging Face 榜单迎来多款重磅更新：DeepSeek-V4 系列（Pro 与 Flash）以极高人气领跑，单模型周点赞均超千，下载量总和突破300万；Google Gemma 4 系列持续发力，Gemma-4-31B-it 以 911 万下载量成为本周最热模型之一。多模态模型竞争白热化，Qwen3.6 家族（27B/35B-A3B）凭借 MoE 架构与超大上下文能力斩获数百万下载。量化与微调生态异常活跃，Unsloth 和社区开发者针对 Qwen3.6、Gemma 4 等旗舰模型推出大量 GGUF 版本，推动模型部署门槛进一步降低。

## 热门模型

### 🧠 语言模型 (LLM、对话模型、指令微调)
* **deepseek-ai/DeepSeek-V4-Pro** – deepseek-ai | 👍 3,870 | ⬇ 2,017,835  
  全新 DeepSeek V4 Pro 旗舰对话模型，本周点赞数与下载量双冠，凭借强劲的推理能力与开源权重占据榜单榜首。
* **deepseek-ai/DeepSeek-V4-Flash** – deepseek-ai | 👍 1,051 | ⬇ 1,162,290  
  DeepSeek V4 的快速推理版本，面向实时场景优化，兼顾性能与效率，同样获得大量关注。
* **XiaomiMiMo/MiMo-V2.5-Pro** – XiaomiMiMo | 👍 511 | ⬇ 41,654  
  小米推出的 MoE 架构长上下文语言模型，支持 Agent 任务，在长文本处理上表现出色。
* **z-lab/gemma-4-31B-it-DFlash** – z-lab | 👍 78 | ⬇ 6,423  
  基于 Gemma 4 的投机解码优化版本，通过 DFlash 技术加速推理，适合部署场景。

### 🎨 多模态与生成 (图像、视频、音频、文本到X)
* **openbmb/MiniCPM-V-4.6** – openbmb | 👍 339 | ⬇ 0  
  面壁智能最新多模态对话模型，支持图像与文本输入，推理能力大幅提升，虽下载量暂未统计但热度极高。
* **google/gemma-4-31B-it** – google | 👍 2,607 | ⬇ 9,119,339  
  Google 的 Gemma 4 旗舰多模态对话模型，支持图像+文本输入，本周下载量突破 900 万，社区适配版本极多。
* **google/gemma-4-26B-A4B-it** – google | 👍 932 | ⬇ 7,179,265  
  Gemma 4 的 MoE 变体，以 26B 总参数量、4B 激活参数实现高效推理，占据下载榜前列。
* **Qwen/Qwen3.6-35B-A3B** – Qwen | 👍 1,728 | ⬇ 3,858,503  
  阿里通义千问 Qwen3.6 系列 MoE 版，仅 3B 激活参数即可完成多模态任务，兼具高性能与低资源需求。
* **Qwen/Qwen3.6-27B** – Qwen | 👍 1,245 | ⬇ 2,446,478  
  Qwen3.6 的 Dense 版（27B），支持图像与文本的强对话能力，社区广泛采用。
* **moonshotai/Kimi-K2.6** – moonshotai | 👍 1,264 | ⬇ 1,423,653  
  月之暗面 Kimi 最新多模态模型，支持图像理解与压缩张量技术，在长上下文和多轮对话中表现突出。
* **HiDream-ai/HiDream-O1-Image** – HiDream-ai | 👍 256 | ⬇ 3,418  
  由 HiDream 打造的图像生成模型（文本+图像→图像），结合 Qwen3-VL 视觉理解，可实现精细化图像控制。
* **HiDream-ai/HiDream-O1-Image-Dev** – HiDream-ai | 👍 81 | ⬇ 1,367  
  上述模型的开发者预览版，参数更小，适合快速实验和微调。
* **SulphurAI/Sulphur-2-base** – SulphurAI | 👍 671 | ⬇ 157,648  
  专注文本生成视频的扩散模型，支持 diffusers 全家桶，在视频生成赛道表现亮眼。
* **SeeSee21/Z-Anime** – SeeSee21 | 👍 314 | ⬇ 9,477  
  动漫风格文本到图像模型，同时提供 GGUF 和 diffusers 格式，满足二次元创作需求。
* **TenStrip/LTX2.3-10Eros** – TenStrip | 👍 227 | ⬇ 64,008  
  图像转视频模型，主打高质量短视频生成，适合创意内容生产。
* **google/gemma-4-31B-it-assistant** – google | 👍 212 | ⬇ 66,561  
  Gemma 4 的专用助手版（any-to-any），可处理文本、图像、音频等多种模态输入并输出对应结果。
* **google/gemma-4-26B-A4B-it-assistant** – google | 👍 117 | ⬇ 47,749  
  26B A4B 的助手版，面向多模态通用对话场景。
* **google/gemma-4-E4B-it-assistant** – google | 👍 68 | ⬇ 51,766  
  Gemma 4 的极轻量级助手版（激活参数量仅 4B? E4B 可能指 Expert 4B），进一步降低部署门槛。
* **Supertone/supertonic-3** – Supertone | 👍 107 | ⬇ 1,837  
  新一代文本到语音模型，支持自然多语种合成，适合语音助手和内容生成。
* **k2-fsa/OmniVoice** – k2-fsa | 👍 854 | ⬇ 2,224,595  
  零样本多语言语音克隆模型，支持任意语音样本的实时克隆，下载量超 200 万。
* **sensenova/SenseNova-U1-8B-MoT** – sensenova | 👍 236 | ⬇ 4,528  
  商汤科技 SenseNova 系列多模态 MoT（Mixture of Tuners）模型，支持 any-to-any 任务，主打高效微调。

### 🔧 专用模型 (代码、翻译、嵌入、分类等)
* **openai/privacy-filter** – openai | 👍 1,417 | ⬇ 190,993  
  OpenAI 推出的隐私过滤器（token 分类模型），用于检测和屏蔽敏感信息，企业级应用关注度高。
* **AngelSlim/Hy-MT1.5-1.8B-1.25bit** – AngelSlim | 👍 166 | ⬇ 17,260  
  极低比特量化翻译模型（1.25bit），基于 Hy-MT 架构，在保持翻译质量的同时大幅压缩模型体积。

### 📦 微调与量化 (社区微调、GGUF、AWQ)
* **froggeric/Qwen-Fixed-Chat-Templates** – froggeric | 👍 149 | ⬇ 0  
  修正 Qwen 系列聊天模板的工具项目，虽无下载量但获社区认可，体现开发者对模型部署细节的需求。
* **unsloth/Qwen3.6-35B-A3B-GGUF** – unsloth | 👍 1,000 | ⬇ 2,733,708  
  Unsloth 为 Qwen3.6-35B-A3B 提供的 GGUF 量化版，极大便利本地轻量部署，下载量高企。
* **unsloth/Qwen3.6-27B-GGUF** – unsloth | 👍 658 | ⬇ 1,468,142  
  Qwen3.6-27B 的 GGUF 量化版，配合 Unsloth 工具链，成为社区本地推理首选。
* **Jackrong/Qwopus3.6-35B-A3B-v1-GGUF** – Jackrong | 👍 114 | ⬇ 67,205  
  社区开发者对 Qwen3.6-35B-A3B 的额外 GGUF 版本，提供不同量化精度选项。
* **havenoammo/Qwen3.6-27B-MTP-UD-GGUF** – havenoammo | 👍 80 | ⬇ 43,428  
  基于 Qwen3.6-27B 的 MTP-UD（多token预测？）量化版，探索推理加速。
* **DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF** – DavidAU | 👍 134 | ⬇ 197,110  
  社区对 Qwen3.6-27B 进行无审查+代码增强的微调版本，并量化至 GGUF，面向特定创作与编程场景。
* **Zyphra/ZAYA1-8B** – Zyphra | 👍 436 | ⬇ 66,119  
  基于 ZAYA1-reasoning-base 微调的 8B 推理模型（arXiv:2605.05365），社区关注其推理能力改进。

## 生态信号

1. **模型家族势头**：DeepSeek V4 系列（Pro + Flash）和 Qwen3.6 家族（27B/35B-A3B）成为本周绝对主力，前者代表纯文本大模型的极致能力，后者以 MoE 多模态实现高性价比。Google Gemma 4 系列（31B/26B-A4B）凭借 Google 背书和超量社区适配保持极高下载量，形成“官方模型+海量量化版”的生态循环。  
2. **开源 vs 闭源**：开源权重模型持续主导热门榜，DeepSeek、Qwen、Gemma 均为开源授权，而 OpenAI 仅贡献专用模型（privacy-filter），反映出开源社区对通用型基础模型的强烈需求。  
3. **量化与微调活跃度**：Unsloth 领衔的 GGUF 量化生态全面覆盖头部模型，Qwen3.6 的多个变体（Dense、MoE）均被快速量化。社区微调倾向“无审查”“代码增强”“长上下文”等方向，表明用户对特定场景的定制化需求迫切。此外，极低比特量化（1.25bit）和投机解码（DFlash）等创新技术也开始涌现。

## 值得探索

1. **Qwen/Qwen3.6-35B-A3B** – 3B 激活参数的 MoE 模型实现接近 35B 总参量的多模态能力，性能与效率平衡极佳，适合资源受限设备或高并发服务，且已存在大量 GGUF 社区版本，易用性极强。  
2. **k2-fsa/OmniVoice** – 零样本多语言语音克隆模型，下载量超 200 万，且支持任意音频样本的实时克隆，功能新颖，值得语音交互和内容创作领域的研究者尝试。  
3. **z-lab/gemma-4-31B-it-DFlash** – 将投机解码（Speculative Decoding）应用于 Gemma 4 的尝试，在几乎不损失质量的前提下大幅提速推理，对于需要低延迟部署的生产环境具有重要参考价值。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*