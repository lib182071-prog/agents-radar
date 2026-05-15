# Hugging Face 热门模型日报 2026-05-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-05-15 10:00 UTC

---

# Hugging Face 热门模型日报 (2026-05-15)

## 今日速览
本周 Hugging Face 生态持续火热：**DeepSeek-V4-Pro** 以近 4000 周赞登顶，正式宣告 DeepSeek V4 系列进入主流视野；**Google Gemma-4-31B-it** 凭借 2642 赞和千万下载量成为最受欢迎的多模态开源模型；**Qwen3.6 系列**（35B-A3B/27B）继续霸榜多模态榜单，社区量化版本（unsloth 出品）下载量惊人；**OpenAI 的 privacy-filter** 意外跻身前十，显示安全工具需求上升；此外，**HiDream-O1-Image**、**LTX2.3 视频模型**等生成类新品也收获大量关注。整体趋势：多模态与视频生成加速，开源社区量化活动空前活跃。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai, 赞3,962, 下载277万。DeepSeek V4 旗舰版，融合 MoE 与长上下文技术，对话与推理能力达到新高度，本周热度第一。
2. **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai, 赞1,084, 下载162万。V4 的快速推理版本，兼顾性能与效率，适合线上部署。
3. **[supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)** — Jiunsong, 赞590, 下载28万。基于 Gemma-4 的 26B 无审查 GGUF 量化版，社区对“开放”模型的偏好明显。
4. **[ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** — Zyphra, 赞494, 下载14万。轻量级 8B 语言模型，附带推理优化基座，适合资源受限场景。
5. **[antirez/deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf)** — antirez, 赞110, 下载23万。DeepSeek V4 的 GGUF 版本，由知名程序员社区贡献，推动本地部署。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — Qwen, 赞1,764, 下载494万。Qwen3.6 系列的 MoE 版本（35B 总参，3B 激活），领先的多模态对话模型，兼顾效率与性能。
2. **[Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen, 赞1,282, 下载310万。Qwen3.6 的密集 27B 版，多模态指令遵循能力强，社区热捧。
3. **[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI, 赞946, 下载78万。文本到视频生成模型，基于 diffusers，领跑本周视频生成新秀。
4. **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** — k2-fsa, 赞880, 下载219万。零样本、多语言、声音克隆 TTS 模型，合成质量极高，下载量巨大。
5. **[MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** — openbmb, 赞543, 下载2万。端侧多模态模型（4.6B），支持图像文本理解，适合手机端部署。
6. **[Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** — SeeSee21, 赞371, 下载1万。动漫风格文本到图像生成模型，社区驱动的精细化微调作品。
7. **[HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — HiDream-ai, 赞328, 下载1万。结合“思考”能力的图像生成模型（基于 Qwen3-VL），质量优异。
8. **[LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** — TenStrip, 赞261, 下载10万。图像到视频生成，LTX 系列新版本，视频质量显著提升。
9. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google, 赞2,642, 下载983万。本周下载之王，31B 多模态对话模型，开放权重且性能接近闭源竞品。
10. **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** — google, 赞236, 下载13万。Gemma-4 的“助理”变体，支持任意输入任意输出（any-to-any）。
11. **[SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** — sensenova, 赞256, 下载1万。商汤出品，any-to-any 多模态模型，支持文本/图像/语音的混合理解与生成。
12. **[LTX2.3-ICEdit-Insight](https://huggingface.co/joyfox/LTX2.3-ICEdit-Insight)** — joyfox, 赞72, 下载5千。视频到视频编辑模型，基于 LTX 框架，适合后期处理。
13. **[Pixal3D](https://huggingface.co/TencentARC/Pixal3D)** — TencentARC, 赞65, 下载0。图像到 3D 生成，腾讯 ARC 实验室作品，新技术探索。
14. **[HiDream-O1-Image-Dev](https://huggingface.co/HiDream-ai/HiDream-O1-Image-Dev)** — HiDream-ai, 赞94, 下载3千。O1-Image 的开发预览版，社区早期体验。
15. **[Supertonic-3](https://huggingface.co/Supertone/supertonic-3)** — Supertone, 赞203, 下载1万。高质量文本到语音，支持 ONNX 部署，音色自然。
16. **[Dramabox](https://huggingface.co/ResembleAI/Dramabox)** — ResembleAI, 赞67, 下载0。情感化 TTS，适合有声书/戏剧内容生成。
17. **[Anima](https://huggingface.co/circlestone-labs/Anima)** — circlestone-labs, 赞1,300, 下载47万。单文件扩散模型（很可能为图像生成），ComfyUI 生态，社区分享活跃。

### 🔧 专用模型（代码、数学、医疗、嵌入、安全）

1. **[privacy-filter](https://huggingface.co/openai/privacy-filter)** — openai, 赞1,441, 下载23万。OpenAI 开源的隐私过滤 token 分类模型，用于检测和移除 PII，需求爆发。
2. **[Leanly_AI](https://huggingface.co/jackxinning/Leanly_AI)** — jackxinning, 赞111, 下载1万。医疗领域问答模型，支持中英文，基于 GGUF 量化。
3. **[Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric, 赞200, 下载0。修复 Qwen 系列聊天模板的特殊工具（Jinja），推动兼容性。
4. **[LTX-2.3-Workflows](https://huggingface.co/RuneXX/LTX-2.3-Workflows)** — RuneXX, 赞554, 下载0。为 LTX2.3 视频模型定制的 ComfyUI 工作流集合，降低使用门槛。

### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **[Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** — unsloth, 赞1,032, 下载308万。MoE 版本的 GGUF 量化，unsloth 出品，兼顾推理速度与精度，下载量极高。
2. **[Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth, 赞150, 下载11万。27B 版的带 MTP（多 token 预测）的 GGUF 版本。
3. **[Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** — unsloth, 赞135, 下载10万。MoE + MTP 的 GGUF 量化，极致压缩。
4. **[Qwen3.6-27B-MTP-UD-GGUF](https://huggingface.co/havenoammo/Qwen3.6-27B-MTP-UD-GGUF)** — havenoammo, 赞93, 下载6万。社区贡献的 27B MTP 量化变体，支持用户自定义参数。
5. **[supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)** — （已在语言模型列出，此处提及）该模型同时属于量化类，因其 GGUF 格式和 uncesored 微调属性，社区关注度高。
6. **[antirez/deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf)** — （已在语言模型列出）GGUF 量化版，显示社区对 DeepSeek 本地运行的强烈需求。

## 生态信号

- **模型家族势头**：DeepSeek V4 系列（Pro + Flash）成为本周绝对主角，周赞合计超 5000，下载量逼近 450 万；Google Gemma-4 系列（31B 多模态）以 983 万下载量证明开放权重的竞争力；Qwen3.6 家族（35B/27B）则凭借 MoE 和多模态能力形成完整矩阵，周边量化版本（unsloth 等）贡献了大部分下载。
- **开源权重 vs 闭源**：本周 Top 5 模型全部为开源（或部分开源），社区对开放权重的偏好持续加深，尤其 Gemma-4 的开放策略使其在下载量上超越多数闭源竞品。
- **量化与微调**：unsloth 主导了 Qwen3.6 的 GGUF 量化生态；Gemma-4 的 uncensored 微调版本（Jiunsong）引起关注，体现用户对内容限制的敏感；视频模型（LTX2.3）也衍生出 workflow 和量化变体，显示生态正从纯语言向多模态扩展。

## 值得探索

1. **[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — 本周最强 text-to-video 新秀，基于 diffusers 构建，周获 946 赞，值得研究其视频质量和可控性。
2. **[HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — 首次将“思考链”引入图像生成，借鉴 O1 思路，可能代表新一代生成范式。
3. **[privacy-filter](https://huggingface.co/openai/privacy-filter)** — OpenAI 罕见的开源安全模型，token 级 PII 检测，对 AI 部署合规有重要参考价值。

---
*本日报由 [agents-radar](https://github.com/lib182071-prog/agents-radar) 自动生成。*