# Hugging Face Trending Models Digest 2026-05-13

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-13 10:00 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-05-13

---

## 1. Today's Highlights

DeepSeek's **V4-Pro** and **V4-Flash** dominate the top of the charts with 3.9K and 1.1K weekly likes respectively, signaling continued strong community interest in high-performance open-weight LLMs. Google's **Gemma 4** family is surging—the 31B instruction model now has 2.6K likes and 9.7M downloads—while Qwen's **3.6** series (especially the 35B-A3B MoE variant) has exploded with 1.7K likes and 4.3M downloads. A notable new entrant is **HiDream-O1-Image**, an "O1-style" image generation model that applies chain-of-thought reasoning to text-to-image synthesis, marking a shift toward more deliberative multimodal generation. The quantization ecosystem is highly active, with multiple community GGUF variants of Qwen3.6 and DeepSeek-V4 appearing alongside Unsloth's optimized releases. Speech and voice cloning also see strong traction, with **OmniVoice** hitting 862 likes and 2.2M downloads for its zero-shot multilingual capabilities.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | Likes: 3,910 | Downloads: 2,420,384
  Top-trending model this week: a powerful open-weight conversational LLM with strong reasoning and generation capabilities.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — *deepseek-ai* | Likes: 1,066 | Downloads: 1,365,230
  The faster, distilled variant of DeepSeek V4, offering strong performance at lower computational cost.

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — *google* | Likes: 2,614 | Downloads: 9,725,696
  Google's flagship multimodal LLM extremely popular for instruction-following and conversational tasks.

- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** — *google* | Likes: 223 | Downloads: 93,228
  An "any-to-any" assistant variant of Gemma 4, expanding beyond text to handle mixed input/output modalities.

- **[google/gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)** — *google* | Likes: 120 | Downloads: 63,987
  A 26B MoE assistant model from the Gemma 4 family, offering efficiency through sparse activation.

- **[moonshotai/Kimi-K2.6](https://huggingface.co/moonshotai/Kimi-K2.6)** — *moonshotai* | Likes: 1,274 | Downloads: 1,696,084
  A multimodal conversational model with compressed-tensor support, building on the Kimi K2.5 lineage.

- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** — *sensenova* | Likes: 241 | Downloads: 7,734
  An 8B "Mixture of Tasks" multimodal model supporting any-to-any input/output, with feature extraction capabilities.

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** — *Zyphra* | Likes: 458 | Downloads: 110,182
  A reasoning-focused 8B model built on the ZAYA1-reasoning base, with accompanying arXiv paper.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — *SulphurAI* | Likes: 772 | Downloads: 535,069
  A text-to-video diffusion model supporting GGUF quantization, the most popular video generation model this week.

- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** — *openbmb* | Likes: 434 | Downloads: 3,494
  An efficient vision-language model for image-text-to-text tasks, strong on multimodal understanding.

- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — *HiDream-ai* | Likes: 284 | Downloads: 7,747
  A novel "O1-style" image generation model that applies reasoning steps before generating, built on Qwen3-VL.

- **[HiDream-ai/HiDream-O1-Image-Dev](https://huggingface.co/HiDream-ai/HiDream-O1-Image-Dev)** — *HiDream-ai* | Likes: 88 | Downloads: 2,740
  The development variant of HiDream-O1-Image for experimentation and fine-tuning.

- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** — *TenStrip* | Likes: 239 | Downloads: 84,903
  An image-to-video diffusion model, popular for creating short video clips from still images.

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** — *SeeSee21* | Likes: 325 | Downloads: 11,486
  An anime-style text-to-image model available in GGUF format for efficient inference.

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** — *Supertone* | Likes: 143 | Downloads: 4,954
  A text-to-speech model in ONNX format, optimized for speech synthesis and TTS applications.

- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** — *k2-fsa* | Likes: 862 | Downloads: 2,235,518
  A zero-shot multilingual voice cloning and TTS model with huge download numbers.

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — *Qwen* | Likes: 1,262 | Downloads: 2,772,193
  A high-performing multimodal conversational model (image-text-to-text) from the Qwen 3.6 family.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — *Qwen* | Likes: 1,740 | Downloads: 4,293,332
  The flagship MoE variant of Qwen 3.6, achieving strong performance with only 3B active parameters.

---

### 🔧 Specialized Models (code, math, medical, embeddings, safety)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — *openai* | Likes: 1,425 | Downloads: 206,981
  A token classification model from OpenAI for detecting and filtering private information, available in ONNX.

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** — *AngelSlim* | Likes: 168 | Downloads: 17,352
  An extremely quantized (1.25-bit) translation model based on Hunyuan V1, pushing the boundaries of compression.

- **[jackxinning/Leanly_AI](https://huggingface.co/jackxinning/Leanly_AI)** — *jackxinning* | Likes: 67 | Downloads: 10,610
  A bilingual (EN/ZH) medical question-answering model using GGUF quantization.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)** — *Jackrong* | Likes: 117 | Downloads: 96,759
  Community GGUF quantization of Qwen3.6 MoE, optimized for TGI and Unsloth workflows.

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** — *unsloth* | Likes: 1,012 | Downloads: 2,909,275
  Official Unsloth GGUF variant of Qwen 3.6 MoE, extremely popular for on-device deployment.

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** — *unsloth* | Likes: 664 | Downloads: 1,569,380
  The 27B Qwen3.6 model quantized by Unsloth for efficient inference.

- **[unsloth/Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** — *unsloth* | Likes: 73 | Downloads: 15,355
  A multi-token prediction (MTP) variant of Qwen3.6 MoE in GGUF format.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth* | Likes: 85 | Downloads: 25,924
  Multi-token prediction GGUF for the 27B Qwen3.6 model.

- **[havenoammo/Qwen3.6-27B-MTP-UD-GGUF](https://huggingface.co/havenoammo/Qwen3.6-27B-MTP-UD-GGUF)** — *havenoammo* | Likes: 88 | Downloads: 51,213
  Community GGUF with user-defined optimizations for Qwen3.6 MTP.

- **[Jiunsong/supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)** — *Jiunsong* | Likes: 565 | Downloads: 292,889
  An uncensored fine-tune of the Gemma 4 26B model in GGUF format, popular for unrestricted use.

- **[antirez/deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf)** — *antirez* | Likes: 94 | Downloads: 142,595
  GGUF quantizations of DeepSeek-V4 models from well-known developer antirez.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — *froggeric* | Likes: 167 | Downloads: 0
  A useful utility providing corrected Jinja chat templates for Qwen 3.5 models, supporting MLX.

---

## 3. Ecosystem Signal

This week's trending list reveals several clear ecosystem dynamics:

**The Qwen 3.6 family is the week's dominant force**, appearing in 8 of the 30 top models across base releases, MoE (35B-A3B), and multiple quantization variants. The original **Qwen3.6-35B-A3B** (1.7K likes, 4.3M downloads) is a standout—its MoE architecture with only 3B active parameters makes it both powerful and accessible. **Google's Gemma 4** family shows equally strong momentum, with the 31B instruction model seeing massive download numbers (9.7M) and spawning uncensored community fine-tunes like the supergemma4 variant. **DeepSeek V4** remains a powerhouse for pure text-generation, with both Pro and Flash variants showing sustained interest.

A notable trend is the **"reasoning-first" approach to multimodal generation**, exemplified by HiDream-O1-Image. This moves beyond traditional text-to-image by incorporating chain-of-thought reasoning steps, potentially setting a new paradigm. **Speech and voice synthesis** is seeing a revival—OmniVoice's zero-shot multilingual cloning and Supertone's TTS model both trended strongly.

**Quantization activity is at an all-time high**, with Unsloth leading the GGUF ecosystem for Qwen models. The presence of multiple community quantizations (Jackrong, havenoammo, antirez) suggests a healthy open-weight deployment ecosystem. The appearance of privacy and safety models (openai/privacy-filter) alongside uncensored fine-tunes highlights the ongoing tension between accessibility and responsibility in model distribution.

---

## 4. Worth Exploring

1. **[HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — This represents a genuinely novel paradigm: applying step-by-step reasoning before image generation. For researchers and developers interested in the intersection of chain-of-thought and multimodal generation, this is the model to study and experiment with.

2. **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** — With 2.2M downloads and zero-shot multilingual voice cloning, this model is both practically useful and technically impressive. It's worth exploring for anyone working on speech synthesis, accessibility tools, or multilingual applications.

3. **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — OpenAI's first open-weight safety model is a significant ecosystem signal. As privacy regulations tighten, this token-classification model for PII detection could become an essential component in deployment pipelines. Its ONNX support makes it highly portable.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*