# Hugging Face Trending Models Digest 2026-05-17

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-17 08:34 UTC

---

# Hugging Face Trending Models Digest — 2026-05-17

## Today's Highlights

This week's top trend is the explosive growth of the **DeepSeek V4** family, with both the Pro and Flash variants earning thousands of likes and millions of downloads. **Google’s Gemma 4** (31B-it) continues to dominate multimodal reasoning, while the **Qwen3.6** series (especially the 35B-A3B MoE) sees massive community adoption via quantized GGUF releases from Unsloth. Meanwhile, **voice and video generation** models are surging — **Sulphur-2-base** (text-to-video) and **OmniVoice** (zero-shot TTS) both crossed the 1M download mark. OpenAI also surprised the ecosystem with a dedicated **privacy filter** model, signaling growing safety and compliance focus.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek-ai | 4,001 likes, 3.1M downloads  
  Flagship conversational LLM from DeepSeek, setting a new bar for open-weight reasoning.  
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** – deepseek-ai | 1,116 likes, 1.8M downloads  
  Faster distillation of DeepSeek V4 for high-throughput text generation tasks.  
- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** – Zyphra | 515 likes, 144K downloads  
  A fine-tuned 8B reasoning model built on a custom base, drawing attention for its arxiv publication.  
- **[FrontiersMind/Nandi-Mini-600M-Early-Checkpoint](https://huggingface.co/FrontiersMind/Nandi-Mini-600M-Early-Checkpoint)** – FrontiersMind | 82 likes, 16.7K downloads  
  Compact early checkpoint for efficient text generation experimentation.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** – openbmb | 659 likes, 56.5K downloads  
  On-device multimodal model (image+text to text), optimized for edge deployment.  
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** – SulphurAI | 1,045 likes, 970K downloads  
  Diffusion-based text-to-video model, leading the video generation trend.  
- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** – Supertone | 329 likes, 20.2K downloads  
  High-quality neural text-to-speech with ONNX export support.  
- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** – HiDream-ai | 367 likes, 14.3K downloads  
  Image-text-to-image model leveraging Qwen3 VL architecture for editing and generation.  
- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)** – circlestone-labs | 1,362 likes, 524K downloads  
  Single-file diffusion model designed for ComfyUI workflows, highly popular among creators.  
- **[ResembleAI/Dramabox](https://huggingface.co/ResembleAI/Dramabox)** – ResembleAI | 115 likes, 936 downloads  
  LTX-Audio-based TTS with voice cloning capabilities.  
- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** – SeeSee21 | 387 likes, 14.9K downloads  
  Anime-focused text-to-image model with both Diffusers and GGUF support.  
- **[TencentARC/Pixal3D](https://huggingface.co/TencentARC/Pixal3D)** – TencentARC | 107 likes, 0 downloads (new)  
  Image-to-3D generation model from Tencent, published with arxiv paper.  
- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – Qwen | 1,788 likes, 5.5M downloads  
  MoE multimodal model (image+text) balancing efficiency and quality, a community favorite.  
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** – Qwen | 1,308 likes, 3.4M downloads  
  Dense multimodal model in the Qwen3.6 line, highly downloaded.  
- **[ScenemaAI/scenema-audio](https://huggingface.co/ScenemaAI/scenema-audio)** – ScenemaAI | 80 likes, 209 downloads  
  Diffusion-based text-to-audio and voice cloning model.  
- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** – TenStrip | 274 likes, 135K downloads  
  Image-to-video model using the LTX2.3 architecture.  
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** – google | 2,661 likes, 9.8M downloads  
  Google’s flagship multimodal instruct model, with massive community adoption.  
- **[microsoft/Fara-7B](https://huggingface.co/microsoft/Fara-7B)** – microsoft | 567 likes, 17.1K downloads  
  Microsoft’s 7B multimodal model based on Qwen2.5 VL architecture.  
- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** – google | 246 likes, 168K downloads  
  Any-to-any assistant variant of Gemma 4, supporting text, images, audio, and video.  
- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – k2-fsa | 891 likes, 2.1M downloads  
  Zero-shot multilingual voice cloning and TTS model, rapidly gaining traction.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** – froggeric | 249 likes, 0 downloads (resource)  
  Community-provided corrected Jinja chat templates for Qwen models, essential for proper inference.  
- **[jackxinning/Leanly_AI](https://huggingface.co/jackxinning/Leanly_AI)** – jackxinning | 116 likes, 9.4K downloads  
  Medical question-answering model (GGUF) supporting English and Chinese.  
- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** – openai | 1,453 likes, 248K downloads  
  Token classification model from OpenAI for detecting and filtering private information.  
- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** – Cactus-Compute | 60 likes, 221 downloads  
  JAX-based encoder-decoder optimized for function calling and tool use.  
- **[RuneXX/LTX-2.3-Workflows](https://huggingface.co/RuneXX/LTX-2.3-Workflows)** – RuneXX | 568 likes, 0 downloads (resource)  
  Collection of ComfyUI workflows for LTX2.3 image-to-video, enabling easier creative use.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** – unsloth | 209 likes, 185K downloads  
  GGUF quantized version of Qwen3.6-27B using MTP (Multi-Token Prediction) for faster inference.  
- **[unsloth/Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** – unsloth | 190 likes, 181K downloads  
  GGUF quantized MoE version of Qwen3.6-35B-A3B with MTP optimizations.  
- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** – unsloth | 1,046 likes, 2.7M downloads  
  Most downloaded Qwen3.6 GGUF variant, making large MoE accessible on consumer hardware.  
- **[Jiunsong/supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)** – Jiunsong | 608 likes, 268K downloads  
  Uncensored fine-tune of Gemma 4 in GGUF format, popular for unfiltered generation.  
- **[antirez/deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf)** – antirez | 130 likes, 283K downloads  
  Community quantized GGUF of DeepSeek V4/Flash for llama.cpp usage.

---

## Ecosystem Signal

The current landscape is dominated by **three major open-weight families**: DeepSeek V4, Qwen3.6, and Google Gemma 4. Each has spawned a rich ecosystem of quantized variants (especially GGUF) and fine-tunes, with **Unsloth** acting as a key infrastructure provider. Multimodal models now represent the majority of trending repos, reflecting the shift from pure language to **vision-language and generation pipelines**. Video generation (Sulphur-2-base, LTX2.3) and voice cloning (OmniVoice, Dramabox) are rapidly maturing. Notably, OpenAI’s release of a **privacy filter** model suggests growing demand for guardrails in deployed systems. **Function-calling and tool-use models** (like Needle) are also emerging as a distinct specialty. The open-weight vs. proprietary dynamic remains strongly pro–open, with all top models available for download and fine-tuning.

---

## Worth Exploring

1. **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – The most-buzzed LLM of the week. With 4k likes and 3M downloads, it sets a new performance standard for open-weight conversational AI. Study its architecture and compare to earlier V3 releases.

2. **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – A zero-shot, multilingual voice cloning model with 2M+ downloads. It’s a strong candidate for real-world TTS applications and highlights the growing maturity of open-source speech synthesis.

3. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – The most downloaded multimodal model this period (5.5M). Its MoE design enables strong performance at a fraction of the compute cost, making it ideal for both research and deployment. The active community around GGUF quantization further lowers the barrier to entry.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*