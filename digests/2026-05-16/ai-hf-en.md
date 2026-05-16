# Hugging Face Trending Models Digest 2026-05-16

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-16 07:32 UTC

---

# Hugging Face Trending Models Digest — 2026-05-16

## 🚀 Today’s Highlights
DeepSeek-V4-Pro and DeepSeek-V4-Flash dominate the language model landscape with massive download volumes and strong weekly likes, signaling continued dominance of DeepSeek's architecture. Google’s Gemma‑4‑31B‑it has become the most‑downloaded multimodal model this week, while the Qwen3.6 family (especially the MoE 35B‑A3B variant) sees broad adoption across both official releases and community GGUF quantizations by unsloth. Emerging modalities are also making noise: Sulphur‑2‑base for text‑to‑video and k2‑fsa/OmniVoice for zero‑shot multilingual TTS reflect growing demand for generation beyond text. Community fine‑tuning and quantization activity remains intense, with uncensored and efficiency‑focused variants of Gemma‑4, DeepSeek‑V4, and Qwen3.6 drawing hundreds of thousands of downloads.

---

## 📈 Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

- **deepseek-ai/DeepSeek-V4-Pro** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro))  
  *Author: deepseek-ai | Likes: 3,980 | Downloads: 2,766,621*  
  State‑of‑the‑art conversational LLM with transformer architecture, trending as the top‑liked model on the Hub this week.

- **deepseek-ai/DeepSeek-V4-Flash** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash))  
  *Author: deepseek-ai | Likes: 1,098 | Downloads: 1,624,247*  
  A faster, lighter sibling to V4‑Pro optimized for low‑latency inference, gaining traction alongside the flagship.

- **Zyphra/ZAYA1-8B** ([link](https://huggingface.co/Zyphra/ZAYA1-8B))  
  *Author: Zyphra | Likes: 507 | Downloads: 141,203*  
  8B reasoning‑oriented base model with arXiv publication; used as a foundation for fine‑tuned variants.

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X)

- **google/gemma-4-31B-it** ([link](https://huggingface.co/google/gemma-4-31B-it))  
  *Author: google | Likes: 2,652 | Downloads: 9,827,416*  
  Google’s latest 31B multimodal instruction model supporting image+text input and conversational output, driving massive adoption.

- **Qwen/Qwen3.6-35B-A3B** ([link](https://huggingface.co/Qwen/Qwen3.6-35B-A3B))  
  *Author: Qwen | Likes: 1,781 | Downloads: 4,938,568*  
  35B MoE multimodal model (image‑text‑to‑text) offering high performance with efficient activation, a key trend this week.

- **Qwen/Qwen3.6-27B** ([link](https://huggingface.co/Qwen/Qwen3.6-27B))  
  *Author: Qwen | Likes: 1,298 | Downloads: 3,099,139*  
  Dense 27B variant of the Qwen3.6 family, widely used for multimodal conversations and image understanding.

- **k2-fsa/OmniVoice** ([link](https://huggingface.co/k2-fsa/OmniVoice))  
  *Author: k2-fsa | Likes: 890 | Downloads: 2,189,655*  
  Zero‑shot multilingual text‑to‑speech with voice cloning, trending for its high‑quality audio generation across languages.

- **SulphurAI/Sulphur-2-base** ([link](https://huggingface.co/SulphurAI/Sulphur-2-base))  
  *Author: SulphurAI | Likes: 1,000 | Downloads: 783,564*  
  Open text‑to‑video diffusion model (Diffusers) that gained 1k likes, marking a significant step in open‑source video generation.

- **circlestone-labs/Anima** ([link](https://huggingface.co/circlestone-labs/Anima))  
  *Author: circlestone-labs | Likes: 1,336 | Downloads: 465,511*  
  Diffusion single‑file model optimized for ComfyUI, popular for high‑quality image generation with easy integration.

- **openbmb/MiniCPM-V-4.6** ([link](https://huggingface.co/openbmb/MiniCPM-V-4.6))  
  *Author: openbmb | Likes: 610 | Downloads: 22,483*  
  Lightweight on‑device multimodal model with strong vision‑language capabilities, trending for edge deployment.

- **microsoft/Fara-7B** ([link](https://huggingface.co/microsoft/Fara-7B))  
  *Author: microsoft | Likes: 556 | Downloads: 17,425*  
  Multimodal 7B model based on Qwen2.5‑VL, gaining interest for its strong performance in a compact size.

- **HiDream-ai/HiDream-O1-Image** ([link](https://huggingface.co/HiDream-ai/HiDream-O1-Image))  
  *Author: HiDream-ai | Likes: 347 | Downloads: 11,725*  
  Image‑text‑to‑image model using Qwen3‑VL backbone, pushing the envelope for conditional image generation.

### 🔧 Specialized Models (medical, privacy, utilities)

- **openai/privacy-filter** ([link](https://huggingface.co/openai/privacy-filter))  
  *Author: openai | Likes: 1,448 | Downloads: 229,377*  
  Token‑classification model for detecting sensitive information in text; trending as a practical safety tool.

- **jackxinning/Leanly_AI** ([link](https://huggingface.co/jackxinning/Leanly_AI))  
  *Author: jackxinning | Likes: 113 | Downloads: 10,822*  
  Bilingual (EN/ZH) medical question‑answering GGUF model, highlighting niche healthcare LLM interest.

- **froggeric/Qwen-Fixed-Chat-Templates** ([link](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates))  
  *Author: froggeric | Likes: 219 | Downloads: 0*  
  Corrected Jinja chat templates for Qwen3.5/3.6, a utility asset for developers using MLX and local inference.

### 📦 Fine‑tunes & Quantizations (GGUF, community variants)

- **unsloth/Qwen3.6-35B-A3B-GGUF** ([link](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF))  
  *Author: unsloth | Likes: 1,041 | Downloads: 3,075,105*  
  GGUF quantized version of Qwen3.6‑35B‑A3B from unsloth, enabling efficient local inference on consumer hardware.

- **Jiunsong/supergemma4-26b-uncensored-gguf-v2** ([link](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2))  
  *Author: Jiunsong | Likes: 600 | Downloads: 279,744*  
  Uncensored fine‑tune of Gemma‑4 in GGUF format, trending for its “fast” tag and popularity among users seeking less‑restricted outputs.

- **antirez/deepseek-v4-gguf** ([link](https://huggingface.co/antirez/deepseek-v4-gguf))  
  *Author: antirez | Likes: 114 | Downloads: 230,548*  
  GGUF quant of DeepSeek‑V4‑Flash, widely downloaded for running DeepSeek locally via llama.cpp.

- **unsloth/Qwen3.6-27B-MTP-GGUF** ([link](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF))  
  *Author: unsloth | Likes: 175 | Downloads: 105,097*  
  Multi‑token prediction (MTP) quantized variant of Qwen3.6‑27B, offering alternative inference speedups.

---

## 🌐 Ecosystem Signal

The past week shows a clear pivot toward **multimodal foundation models** with strong language capabilities — Gemma‑4 and Qwen3.6 families dominate both original and quantized forms. **Efficient Mixture‑of‑Experts (MoE) architectures** like Qwen3.6‑35B‑A3B are gaining traction, balancing performance with lower compute. **DeepSeek‑V4** remains the top pure‑text LLM, with both Pro and Flash variants seeing heavy downloads and community quantization efforts (GGUF). In generation, **text‑to‑video** is an emerging frontier, with Sulphur‑2‑base leading open‑source efforts. **Zero‑shot voice cloning** (OmniVoice) and **multilingual TTS** (Dramabox, Scenema) reflect growing demand for audio generation. Open‑weight models from Google, DeepSeek, Qwen, and Microsoft continue to drive the ecosystem, while proprietary players like OpenAI contribute targeted safety tools (privacy‑filter). Community fine‑tuning is vibrant, especially **uncensored variants** (supergemma4) and **quantization for on‑device deployment** (unsloth GGUF series). The high number of “region:us” tags suggests cloud‑ready deployment is a key use case.

---

## 🔍 Worth Exploring

1. **deepseek-ai/DeepSeek-V4-Pro** — The highest‑liked model this week, representing the cutting edge of open‑weight conversational LLMs. Its performance and community support make it a must‑test for any LLM‑based application.

2. **Qwen/Qwen3.6-35B-A3B** — The best of both worlds: multimodal understanding with an efficient MoE architecture. Perfect for studying how to combine vision and language while keeping inference costs manageable.

3. **k2-fsa/OmniVoice** — For anyone interested in audio generation, this zero‑shot multilingual TTS model with voice cloning capabilities is both innovative and practical, with nearly 2.2M downloads in its first week.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*