# Hugging Face Trending Models Digest 2026-05-11

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-11 11:46 UTC

---

# Hugging Face Trending Models Digest – 2026-05-11

## Today’s Highlights

The week is dominated by massive open-weight releases from DeepSeek and Qwen, with **DeepSeek-V4-Pro** (3.8K likes, 2M downloads) and **Qwen3.6-35B-A3B** (1.7K likes, 3.9M downloads) leading the pack. Google’s **Gemma-4** family expands aggressively across scales (26B, 31B, and a 4B assistant) and introduces any-to-any multimodal capabilities. Video generation sees a breakout entry with **Sulphur-2-base** (575 likes, 158K downloads), while **OmniVoice** (842 likes, 2.2M downloads) signals strong demand for zero-shot multilingual TTS. Community GGUF quantizations of Qwen and Gemma models are flooding the Hub, with Unsloth and independent finetuners like DavidAU pushing uncensored and code‑optimized variants.

## Trending Models

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek‑ai · 3,841 likes · 2.0M downloads  
  Flagship conversational LLM driving massive adoption; high performance and open weights make it a go‑to for general‑purpose and enterprise use.
- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** – deepseek‑ai · 1,031 likes · 1.2M downloads  
  Faster, lighter sibling of V4‑Pro, optimized for real‑time inference without sacrificing quality.
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** – Qwen · 1,231 likes · 2.4M downloads  
  Multimodal LLM (image‑text‑to‑text) that combines strong vision understanding with conversational fluency.
- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – Qwen · 1,712 likes · 3.9M downloads  
  Mixture‑of‑experts model (35B total, 3B active) delivering large‑model capability at inference‑friendly cost.
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** – google · 2,595 likes · 9.1M downloads  
  Top‑down instruction‑tuned 31B model with image‑text‑to‑text support; the most downloaded model in this digest.
- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** – Zyphra · 402 likes · 66K downloads  
  New 8B LLM with a published arXiv paper (2605.05365); gaining traction among researchers for reproducibility.
- **[mistralai/Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)** – mistralai · 313 likes · 43K downloads  
  Massive 128B model from Mistral, optimized for vLLM and supporting English and French.
- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)** – XiaomiMiMo · 506 likes · 42K downloads  
  Xiaomi’s latest agent‑focused LLM with long‑context capabilities, trending for agentic AI applications.
- **[z-lab/gemma-4-31B-it-DFlash](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash)** – z‑lab · 74 likes · 6.4K downloads  
  Speculative decoding variant of Gemma‑4‑31B, enabling faster generation via draft‑model heads.
- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** – z‑lab · 282 likes · 35K downloads  
  DFlash‑accelerated Qwen3.6‑27B, attracting attention for speed improvements in production settings.

### 🎨 Multimodal & Generation (image, video, audio, any‑to‑any)

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** – SulphurAI · 575 likes · 158K downloads  
  Text‑to‑video model built with Diffusers; one of the first large‑scale video generation models to trend on the Hub.
- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** – HiDream‑ai · 211 likes · 3.4K downloads  
  Image‑text‑to‑image generation leveraging Qwen‑VL; produces high‑quality edits and stylizations.
- **[HiDream-ai/HiDream-O1-Image-Dev](https://huggingface.co/HiDream-ai/HiDream-O1-Image-Dev)** – HiDream‑ai · 74 likes · 1.4K downloads  
  Developer preview of the above, with early‑access weights for testing.
- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** – SeeSee21 · 302 likes · 9.5K downloads  
  Specialized text‑to‑image model for anime styling; popular among creative communities.
- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** – TenStrip · 212 likes · 64K downloads  
  Image‑to‑video model with 10‑frame output; used for short video clip generation.
- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** – google · 203 likes · 67K downloads  
  Any‑to‑any assistant variant of Gemma‑4, capable of processing and generating text, images, and audio.
- **[google/gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)** – google · 108 likes · 48K downloads  
  Smaller 26B MoE assistant with any‑to‑any input/output; balances quality and efficiency.
- **[google/gemma-4-E4B-it-assistant](https://huggingface.co/google/gemma-4-E4B-it-assistant)** – google · 58 likes · 52K downloads  
  Extremely compact 4B‑active‑parameter any‑to‑any assistant, aimed at edge deployment.
- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** – sensenova · 222 likes · 4.5K downloads  
  Multimodal any‑to‑any model (8B) from SenseTime; supports text, image, and audio.
- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** – nvidia · 272 likes · 134K downloads  
  NVIDIA’s MoE omni‑modal model with a reasoning focus; 30B total, 3B active.
- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – k2‑fsa · 842 likes · 2.2M downloads  
  Zero‑shot, multilingual text‑to‑speech model capable of voice cloning; extremely high download count.
- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** – Supertone · 73 likes · 1.8K downloads  
  Lightweight ONNX TTS model; ideal for fast speech synthesis on commodity hardware.

### 🔧 Specialized Models (code, privacy, translation, embeddings)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** – openai · 1,406 likes · 191K downloads  
  Token‑classification model for detecting and redacting personally identifiable information; likely used as a pipeline guard.
- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** – AngelSlim · 161 likes · 17K downloads  
  Extremely quantized (1.25‑bit) translation model based on Hunyuan; pushes the envelope on memory‑efficient multilingual MT.
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** – froggeric · 137 likes · 0 downloads  
  Respository/artifact fixing Jinja chat templates for Qwen models; utility trending among MLX and fine‑tuning users.

### 📦 Fine‑tunes & Quantizations (GGUF, AWQ, community variants)

- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)** – Jackrong · 105 likes · 67K downloads  
  Community GGUF quant of Qwen3.6‑35B‑A3B, enabling local inference on consumer hardware.
- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** – unsloth · 989 likes · 2.7M downloads  
  High‑quality GGUF quant from Unsloth; one of the most downloaded quantized MoE models this week.
- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** – unsloth · 640 likes · 1.5M downloads  
  GGUF version of Qwen3.6‑27B, widely used for local deployment and testing.
- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)** – DavidAU · 123 likes · 197K downloads  
  Unfiltered, code‑focused finetune of Qwen3.6‑27B, packaged as a highly quantized GGUF; popular for “uncensored” use cases.
- **[havenoammo/Qwen3.6-27B-MTP-UD-GGUF](https://huggingface.co/havenoammo/Qwen3.6-27B-MTP-UD-GGUF)** – havenoammo · 65 likes · 43K downloads  
  MTP‑UD (multi‑token prediction) oriented GGUF quant of Qwen3.6‑27B, offering a novel decoding approach.

## Ecosystem Signal

The **DeepSeek V4 family** and **Qwen3.6 MoE** models are clearly the week’s dominant forces, both by community engagement (likes) and raw download volume. Google’s **Gemma-4** series is expanding rapidly with multiple sizes and any‑to‑any assistants, reflecting a strategic push toward omnimodal open‑weight models. The surge in **GGUF quantizations**—especially from Unsloth and independent optimizers—shows that the ecosystem is maturing: users want to run state‑of‑the‑art 30B+ models on consumer GPUs. Meanwhile, video and audio generation models (Sulphur‑2, LTX2.3, OmniVoice) are carving out new categories, attracting creators and researchers alike. The presence of **speculative decoding** (DFlash) variants and **MoE architectures** (A3B, A4B) indicates that inference efficiency is a top priority. Community finetunes like *Heretic Uncensored* highlight the ongoing demand for open, unfiltered models. Overall, the trend is toward **larger, multimodal open-weight models** combined with aggressive quantization and acceleration techniques to democratize access.

## Worth Exploring

1. **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** – As a text‑to‑video model using Diffusers, it marks a significant step beyond image generation. With 575 likes and 158K downloads in a week, it’s a model to benchmark for future video synthesis projects.

2. **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – Zero‑shot, multilingual TTS with voice cloning is a rare combination. Its enormous download count (2.2M) suggests it’s already powering production pipelines; worth studying for speech‑AI applications.

3. **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** – Speculative decoding is a fast‑growing technique for latency reduction. This model (282 likes) provides a practical implementation on Qwen3.6‑27B, making it a great reference for deploying LLMs with lower inference costs.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*