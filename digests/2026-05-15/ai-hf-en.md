# Hugging Face Trending Models Digest 2026-05-15

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-15 10:00 UTC

---

# Hugging Face Trending Models Digest — 2026-05-15

## 1. Today's Highlights

This week’s leaderboard is dominated by **DeepSeek-V4-Pro** (3,962 likes) and the massive **Qwen3.6-35B-A3B** (1,764 likes, 4.9M downloads), signaling strong momentum for both large-scale language models and multimodal MoE architectures. **Google’s Gemma-4-31B-it** (2,642 likes) is the top multimodal model, while **OpenAI’s privacy-filter** (1,441 likes) shows growing enterprise interest in safety tooling. A clear trend is the surge in **text-to-video** (Sulphur-2-base, LTX2.3 variants) and **voice-cloning TTS** (OmniVoice, supertonic-3), alongside active quantization efforts (GGUF) from community players like unsloth and antirez.

## 2. Trending Models by Category

### 🧠 Language Models
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – Author: deepseek-ai | Likes: 3,962 | Downloads: 2,766,621  
  Top‑trending LLM of the week; a conversational, transformer‑based text‑generation model that continues the DeepSeek lineage with enhanced reasoning.
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** – Author: deepseek-ai | Likes: 1,084 | Downloads: 1,624,247  
  A faster, lighter sibling of V4‑Pro, attracting users who need high‑throughput inference.
- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** – Author: Zyphra | Likes: 494 | Downloads: 141,203  
  A reasoning‑base model (arXiv:2605.05365) building on Zyphra’s fine‑tuned pipeline, gaining traction for its specialized reasoning capabilities.

### 🎨 Multimodal & Generation
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** – Author: SulphurAI | Likes: 946 | Downloads: 783,564  
  Leading text‑to‑video diffusion model; trending for high‑quality, fast video generation.
- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** – Author: openbmb | Likes: 543 | Downloads: 22,483  
  On‑device multimodal vision‑language model; popular for efficient edge deployment.
- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** – Author: HiDream-ai | Likes: 328 | Downloads: 11,725  
  Image‑conditioned image generation model; draws attention for its “O1‑style” reasoning in visual tasks.
- **[HiDream-ai/HiDream-O1-Image-Dev](https://huggingface.co/HiDream-ai/HiDream-O1-Image-Dev)** – Author: HiDream-ai | Likes: 94 | Downloads: 3,819  
  Dev variant of the above, offering experimental features for visual reasoning.
- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – Author: Qwen | Likes: 1,764 | Downloads: 4,938,568  
  The flagship Qwen3.6 MoE model (35B total, 3B active), a multimodal powerhouse with top downloads this week.
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** – Author: Qwen | Likes: 1,282 | Downloads: 3,099,139  
  Dense variant of Qwen3.6; strong conversational and image‑text performance.
- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** – Author: SeeSee21 | Likes: 371 | Downloads: 13,998  
  Anime‑focused text‑to‑image model; trending in the creative community.
- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** – Author: TenStrip | Likes: 261 | Downloads: 100,636  
  Image‑to‑video model built on LTX2.3; popular for high‑fidelity video generation from static images.
- **[RuneXX/LTX-2.3-Workflows](https://huggingface.co/RuneXX/LTX-2.3-Workflows)** – Author: RuneXX | Likes: 554 | Downloads: 0  
  ComfyUI workflows for LTX2.3; utility model gaining likes for simplifying video generation pipelines.
- **[joyfox/LTX2.3-ICEdit-Insight](https://huggingface.co/joyfox/LTX2.3-ICEdit-Insight)** – Author: joyfox | Likes: 72 | Downloads: 5,041  
  Video‑to‑video editing and restoration model; niche interest in video post‑production.
- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)** – Author: circlestone-labs | Likes: 1,300 | Downloads: 465,511  
  Single‑file diffusion model for ComfyUI; trending for its ease of use in image generation.
- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** – Author: Supertone | Likes: 203 | Downloads: 12,832  
  High‑quality text‑to‑speech model with ONNX support; rising in the audio generation space.
- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – Author: k2-fsa | Likes: 880 | Downloads: 2,189,655  
  Zero‑shot, multilingual voice‑cloning TTS; huge download count reflects demand for flexible speech synthesis.
- **[ResembleAI/Dramabox](https://huggingface.co/ResembleAI/Dramabox)** – Author: ResembleAI | Likes: 67 | Downloads: 429  
  Narrative‑focused TTS with voice‑cloning; experimental but gaining attention.
- **[TencentARC/Pixal3D](https://huggingface.co/TencentARC/Pixal3D)** – Author: TencentARC | Likes: 65 | Downloads: 0  
  Image‑to‑3D model (arXiv:2605.10922); early‑stage but represents a growing modality.
- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** – Author: sensenova | Likes: 256 | Downloads: 11,417  
  Any‑to‑any multimodal model; notable for its “Mixture of Tasks” architecture.
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** – Author: google | Likes: 2,642 | Downloads: 9,827,416  
  Google’s latest instruction‑tuned multimodal model; top download volume this week.
- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** – Author: google | Likes: 236 | Downloads: 125,005  
  Assistant variant of Gemma‑4, any‑to‑any capabilities; complements the base IT model.

### 🔧 Specialized Models
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** – Author: froggeric | Likes: 200 | Downloads: 0  
  A utility model providing corrected Jinja chat templates for Qwen3.5; trending among developers fixing inference issues.
- **[jackxinning/Leanly_AI](https://huggingface.co/jackxinning/Leanly_AI)** – Author: jackxinning | Likes: 111 | Downloads: 10,822  
  Medical question‑answering model in GGUF format, bilingual (EN/ZH); popular for healthcare applications.
- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** – Author: openai | Likes: 1,441 | Downloads: 229,377  
  Token‑classification model for detecting sensitive data; strong interest in responsible AI tooling.

### 📦 Fine‑tunes & Quantizations
- **[Jiunsong/supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)** – Author: Jiunsong | Likes: 590 | Downloads: 279,744  
  Uncensored GGUF quant of a Gemma‑4 26B variant; popular for unrestricted generations.
- **[antirez/deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf)** – Author: antirez | Likes: 110 | Downloads: 230,548  
  GGUF quantized DeepSeek‑V4 (Flash) for llama.cpp; key for local inference.
- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** – Author: unsloth | Likes: 1,032 | Downloads: 3,075,105  
  GGUF version of Qwen3.6 MoE (35B‑A3B) by unsloth; massive downloads for on‑device deployment.
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** – Author: unsloth | Likes: 150 | Downloads: 105,097  
  GGUF quant of Qwen3.6‑27B with Multi‑Turn Processing; popular for local image‑text chat.
- **[unsloth/Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** – Author: unsloth | Likes: 135 | Downloads: 97,682  
  MoE variant with MTP, quantized for efficiency.
- **[havenoammo/Qwen3.6-27B-MTP-UD-GGUF](https://huggingface.co/havenoammo/Qwen3.6-27B-MTP-UD-GGUF)** – Author: havenoammo | Likes: 93 | Downloads: 62,035  
  Another community GGUF of Qwen3.6‑27B with MTP; highlights the breadth of quantization efforts.

## 3. Ecosystem Signal

The **Qwen3.6 family** (especially the MoE 35B‑A3B) is the clear winner this week, with both base and GGUF versions accumulating millions of downloads. **DeepSeek V4** continues its strong run, now with Pro and Flash variants and community quantizations. **Google’s Gemma‑4** series shows that open‑weight models from big labs are still a major draw, especially for multimodal tasks. The **text‑to‑video** space is heating up: Sulphur‑2‑base leads in likes, while LTX2.3 derivatives (image‑to‑video, workflows, editing) show a rapidly maturing ecosystem. **Voice synthesis** is another booming area—OmniVoice’s 2M+ downloads speak to demand for zero‑shot multilingual TTS. Meanwhile, **OpenAI’s privacy‑filter** is a rare small‑scale open release from a major lab, signaling a focus on safety tooling. Quantization remains a dominant community activity: nearly every major model now has GGUF versions from unsloth, antirez, or others, lowering the barrier for local inference.

## 4. Worth Exploring

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – The week’s most‑liked model; benchmark its reasoning and conversational capabilities, especially for long‑context tasks.  
- **[OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – With over 2.1M downloads, this zero‑shot voice‑cloning TTS is a must‑try for multilingual speech applications and demonstrates the practicality of open‑weight audio models.  
- **[Pixal3D](https://huggingface.co/TencentARC/Pixal3D)** – Although early‑stage (0 downloads), this image‑to‑3D model from TencentARC points to an emerging modality—worth studying for 3D content generation research.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*