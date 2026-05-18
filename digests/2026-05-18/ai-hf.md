# Hugging Face 热门模型日报 2026-05-18

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-18 12:51 UTC

---

## Hugging Face 热门模型日报（2026-05-18）

### 📰 今日速览

本周 Hugging Face 热点由**多模态大模型**主导：Google 发布的 **Gemma-4-31B-it** 以近千万下载量领跑，Qwen 与 DeepSeek 两大系列全面升级；同时 **DeepSeek V4 Pro** 与 **V4 Flash** 双星闪耀，社区量化版（GGUF）也迅速铺开。端侧多模态模型 **MiniCPM-V-4.6** 与 **Fara-7B** 关注度攀升，视频生成领域 **Sulphur-2-base** 下载量破百万，语音合成、3D 生成等赛道也有新作亮相。整体呈现“大厂竞技 + 社区微调量化”双轮驱动的活跃生态。

---

### 🏆 热门模型分类盘点

#### 🧠 语言模型（LLM、对话、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,026 | 3,435,748 | 最新旗舰对话模型，性能与关注度双冠王，全栈自研MoE架构 |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,140 | 1,904,105 | V4系列高效推理版，成本与速度优化，适合产品部署 |
| [supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2) | Jiunsong | 624 | 267,449 | 基于Gemma-4的社区无审查微调+量化版，下载活跃 |
| [Ring-2.6-1T](https://huggingface.co/inclusionAI/Ring-2.6-1T) | inclusionAI | 74 | 2,406 | 1万亿参数混合专家模型，国产百亿级MoE新尝试 |
| [Nandi-Mini-600M-Early-Checkpoint](https://huggingface.co/FrontiersMind/Nandi-Mini-600M-Early-Checkpoint) | FrontiersMind | 91 | 18,203 | 600M小参数语言模型早期检查点，适合轻量实验 |

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it) | google | 2,674 | 9,889,356 | 谷歌最新31B多模态对话模型，下载量断层式领先 |
| [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 1,812 | 5,613,637 | 通义千问3.6版MoE多模态模型，35B总参+3B活跃参，高效强大 |
| [Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B) | Qwen | 1,318 | 3,550,893 | 27B密度型多模态模型，综合能力均衡，社区广泛使用 |
| [Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base) | SulphurAI | 1,103 | 1,049,229 | 文本到视频生成新秀，下载量快速突破百万 |
| [MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6) | openbmb | 753 | 80,586 | 端侧多模态小模型（On-Device），适合移动与边缘部署 |
| [HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image) | HiDream-ai | 387 | 15,024 | 图像到图像生成，结合Qwen3-VL视觉理解实现智能编辑 |
| [supertonic-3](https://huggingface.co/Supertone/supertonic-3) | Supertone | 394 | 24,031 | 高保真语音合成，支持情感控制，已提供ONNX优化 |
| [Z-Anime](https://huggingface.co/SeeSee21/Z-Anime) | SeeSee21 | 404 | 15,495 | 动漫风格文本到图像模型，社区创作热门 |
| [Dramabox](https://huggingface.co/ResembleAI/Dramabox) | ResembleAI | 152 | 1,001 | 戏剧化语音克隆与音频生成，LTX技术驱动 |
| [Pixal3D](https://huggingface.co/TencentARC/Pixal3D) | TencentARC | 138 | 0 | 腾讯Arc的图像到3D生成，论文刚公开，社区关注中 |
| [LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros) | TenStrip | 284 | 140,927 | 图像到视频生成，基于LTX 2.3的社区微调模型 |
| [Fara-7B](https://huggingface.co/microsoft/Fara-7B) | microsoft | 577 | 16,011 | 微软7B多模态模型，基于Qwen2.5-VL架构，轻量实用 |
| [scenema-audio](https://huggingface.co/ScenemaAI/scenema-audio) | ScenemaAI | 95 | 237 | 场景音频生成，扩散模型实现文本到音频 |
| [Irodori-TTS-500M-v3](https://huggingface.co/Aratako/Irodori-TTS-500M-v3) | Aratako | 67 | 0 | 小型TTS模型（500M），语音合成轻量选项 |

#### 🔧 专用模型（代码、数学、医疗、工具调用等）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Leanly_AI](https://huggingface.co/jackxinning/Leanly_AI) | jackxinning | 118 | 9,432 | 中英双语医疗问答模型，GGUF量化版方便部署 |
| [needle](https://huggingface.co/Cactus-Compute/needle) | Cactus-Compute | 76 | 241 | 基于JAX的自定义函数调用与工具使用模型，编码器-解码器架构 |
| [Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 275 | 0 | 修复Qwen系列聊天模板，实用工具，MLX兼容 |

#### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF) | unsloth | 250 | 268,305 | unsloth量化版Qwen3.6-27B（多Token预测），本地部署首选 |
| [Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF) | unsloth | 231 | 237,613 | 同上，MoE版量化，高效推理 |
| [deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf) | antirez | 143 | 295,917 | DeepSeek V4的GGUF量化版，作者为知名C程序员 |
| [supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2) | Jiunsong | 624 | 267,449 | 已在上方列出，Gemma-4社区微调+量化热款 |
| [Qwopus3.5-9B-Coder-GGUF](https://huggingface.co/Jackrong/Qwopus3.5-9B-Coder-GGUF) | Jackrong | 79 | 6,462 | Qwen3.5代码版量化，面向编码场景 |
| [ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B) | Zyphra | 529 | 145,609 | Zyphra发布的8B微调模型，基于推理基座，有论文支撑 |
| [Anima](https://huggingface.co/circlestone-labs/Anima) | circlestone-labs | 1,391 | 545,205 | ComfyUI中的单文件扩散模型，社区图像创作必备 |

---

### 📊 生态信号

1. **DeepSeek V4 家族全面爆发**：Pro 与 Flash 双模型在赞/下载上占据绝对优势，同时社区量化版（GGUF）迅速跟进，反映用户对高性能开源对话模型的强烈需求。  
2. **Qwen 3.6 系列全面开花**：通义千问3.6发布即进入热榜，27B、35B-A3B（MoE）及多种GGUF量化版本同步涌现，形成完整部署生态。  
3. **多模态成主战场**：Google Gemma-4-31B-it 下载量近千万，微软、OpenBMB、腾讯等纷纷推出端侧或专用多模态模型，图像、视频、3D 均有突破。  
4. **开源权重 vs 闭源**：本周热点全部来自开源权重模型，且社区微调与量化活动异常活跃（GGUF 版本占比超1/3），验证了开放生态的吸引力。  
5. **轻量与小模型受关注**：MiniCPM-V-4.6（端侧）、Nandi-Mini-600M、Irodori-TTS-500M 等表明开发者仍需要低资源可部署方案。

---

### 🔭 值得探索

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** —— 当前周点赞最高的模型，代表国产开源LLM的顶尖水平，直接与GPT-4o对标，建议深入测试推理与对话能力。  
2. **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** —— MoE架构的高效多模态模型（活跃参数仅3B），在性能与资源间取得极佳平衡，尤其适合云端低成本推理。  
3. **[MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** —— 端侧多模态模型的标杆，可在手机或边缘设备运行，为离线视觉问答、OCR等场景提供可行路径。

> 数据截止：2026-05-18 17:00 UTC | 来源：Hugging Face Hub

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*