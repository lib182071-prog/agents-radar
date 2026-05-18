# Hugging Face Trending Models Digest 2026-05-18

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-18 12:51 UTC

---

# Hugging Face Trending Models Digest — 2026-05-18

## Today's Highlights

The week is dominated by massive multimodal releases: **Qwen**’s Qwen3.6 family (27B and 35B-A3B) and **Google**’s Gemma-4-31B-it have each surpassed **5 million and 9 million downloads** respectively, cementing vision-language models as the primary growth vector. **DeepSeek-V4-Pro** (4k+ likes, 3.4M downloads) and its Flash sibling remain the top pure text-generation choices. On the generation front, **SulphurAI**’s text-to-video model Sulphur-2-base crossed 1M downloads, while audio TTS models from **Supertone** and **ResembleAI** show increasing sophistication. Quantization and community fine-tuning are booming, with unsloth’s Qwen3.6 GGUF variants and the uncensored Gemma4 GGUF from Jiunsong gaining strong traction.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | Likes: 4,026 | Downloads: 3,435,748  
  Top-tier conversational LLM with massive community adoption, trending due to its strong reasoning and open-weight availability.

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai | Likes: 1,140 | Downloads: 1,904,105  
  Faster, smaller variant of DeepSeek-V4, widely used for efficient deployment.

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** — Zyphra | Likes: 529 | Downloads: 145,609  
  A reasoning-focused 8B model fine-tuned on a specialized base, gaining interest for its arxiv-backed methodology.

- **[inclusionAI/Ring-2.6-1T](https://huggingface.co/inclusionAI/Ring-2.6-1T)** — inclusionAI | Likes: 74 | Downloads: 2,406  
  A 1T-parameter hybrid text-generation model (Bailing architecture), notable for its scale despite early-stage adoption.

- **[FrontiersMind/Nandi-Mini-600M-Early-Checkpoint](https://huggingface.co/FrontiersMind/Nandi-Mini-600M-Early-Checkpoint)** — FrontiersMind | Likes: 91 | Downloads: 18,203  
  Lightweight 600M checkpoint for efficient text generation, popular for edge and research use.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | Likes: 2,674 | Downloads: 9,889,356  
  Instruction-tuned multimodal model from Google, leading downloads this week with strong vision-language capabilities.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — Qwen | Likes: 1,812 | Downloads: 5,613,637  
  Qwen’s latest MoE vision-language model (35B total, 3B active), trending for its efficiency in image-text-to-text tasks.

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen | Likes: 1,318 | Downloads: 3,550,893  
  Dense 27B vision-language model, a go-to choice for high-quality multimodal reasoning.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI | Likes: 1,103 | Downloads: 1,049,229  
  Text-to-video generation model with over 1M downloads, reflecting growing demand for video synthesis.

- **[microsoft/Fara-7B](https://huggingface.co/microsoft/Fara-7B)** — microsoft | Likes: 577 | Downloads: 16,011  
  Microsoft’s 7B vision-language model built on Qwen2.5-VL, attracting enterprise attention.

- **[openbmb/MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)** — openbmb | Likes: 753 | Downloads: 80,586  
  On-device multimodal model optimized for mobile deployment, trending for its small footprint.

- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — HiDream-ai | Likes: 387 | Downloads: 15,024  
  Image generation model that applies O1‑style reasoning to image synthesis, a novel approach.

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** — SeeSee21 | Likes: 404 | Downloads: 15,495  
  Anime-style text-to-image model with GGUF support, popular among content creators.

- **[Supertone/supertonic-3](https://huggingface.co/Supertone/supertonic-3)** — Supertone | Likes: 394 | Downloads: 24,031  
  High-quality text-to-speech model with ONNX support, leading the TTS category.

- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** — TenStrip | Likes: 284 | Downloads: 140,927  
  Image-to-video model based on LTX 2.3, popular for short video creation.

- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)** — circlestone-labs | Likes: 1,391 | Downloads: 545,205  
  Single-file diffusion model for image generation, widely used in ComfyUI workflows.

- **[TencentARC/Pixal3D](https://huggingface.co/TencentARC/Pixal3D)** — TencentARC | Likes: 138 | Downloads: 0  
  Image-to-3D generation model from Tencent, fresh release with an arxiv paper (2605.10922).

- **[internlm/Intern-S2-Preview](https://huggingface.co/internlm/Intern-S2-Preview)** — internlm | Likes: 69 | Downloads: 1,168  
  Preview of InternLM’s next‑gen vision-language model, gaining early community interest.

- **[ResembleAI/Dramabox](https://huggingface.co/ResembleAI/Dramabox)** — ResembleAI | Likes: 152 | Downloads: 1,001  
  Audio TTS with voice cloning, a niche tool for dramatic audio generation.

- **[ScenemaAI/scenema-audio](https://huggingface.co/ScenemaAI/scenema-audio)** — ScenemaAI | Likes: 95 | Downloads: 237  
  Diffusion-based text-to-audio and voice cloning model, emerging in the audio space.

- **[Aratako/Irodori-TTS-500M-v3](https://huggingface.co/Aratako/Irodori-TTS-500M-v3)** — Aratako | Likes: 67 | Downloads: 0  
  Compact 500M Japanese TTS model, popular in the voice synthesis community.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | Likes: 76 | Downloads: 241  
  An encoder-decoder model for function calling and tool‑use tasks, built with JAX.

- **[jackxinning/Leanly_AI](https://huggingface.co/jackxinning/Leanly_AI)** — jackxinning | Likes: 118 | Downloads: 9,432  
  Medical question‑answering model supporting English and Chinese, trending for healthcare AI.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric | Likes: 275 | Downloads: 0  
  Utility repo providing corrected chat templates for Qwen models (MLX/Jinja), essential for proper model interaction.

- **[RuneXX/LTX-2.3-Workflows](https://huggingface.co/RuneXX/LTX-2.3-Workflows)** — RuneXX | Likes: 576 | Downloads: 0  
  Collection of ComfyUI workflows for LTX-2.3 video generation, highly liked for empowering creators.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth | Likes: 250 | Downloads: 268,305  
  Quantized GGUF version of Qwen3.6-27B with multi‑token prediction (MTP), enabling fast local inference.

- **[unsloth/Qwen3.6-35B-A3B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-MTP-GGUF)** — unsloth | Likes: 231 | Downloads: 237,613  
  GGUF quant of the MoE Qwen3.6‑35B‑A3B with MTP, widely downloaded for efficient multimodal use.

- **[antirez/deepseek-v4-gguf](https://huggingface.co/antirez/deepseek-v4-gguf)** — antirez | Likes: 143 | Downloads: 295,917  
  Community GGUF quantization of DeepSeek-V4 models by legendary programmer antirez, popular for local deployment.

- **[Jiunsong/supergemma4-26b-uncensored-gguf-v2](https://huggingface.co/Jiunsong/supergemma4-26b-uncensored-gguf-v2)** — Jiunsong | Likes: 624 | Downloads: 267,449  
  Uncensored fine‑tune of Gemma-4-26B in GGUF format, trending for its unrestricted conversational style.

- **[Jackrong/Qwopus3.5-9B-Coder-GGUF](https://huggingface.co/Jackrong/Qwopus3.5-9B-Coder-GGUF)** — Jackrong | Likes: 79 | Downloads: 6,462  
  GGUF quantized code‑focused variant of Qwen3.5, tailored for programming tasks.

---

## Ecosystem Signal

The current landscape reveals a clear **multimodal convergence**: the top‑downloaded models (Gemma‑4‑31B‑it, Qwen3.6‑35B‑A3B, Qwen3.6‑27B) all combine vision and language, signaling that pure text LLMs are no longer the sole priority. **DeepSeek‑V4** continues to dominate the text‑only segment, but even it is increasingly used alongside vision models. In generation, **text‑to‑video** is the breakout modality—Sulphur‑2‑base and LTX2.3 models are drawing millions of downloads, while audio generation matures with production‑ready TTS like supertonic‑3.

On the **open‑weight** front, all top models are fully open, with no proprietary gatekeeping. The **quantization ecosystem** is explosive: unsloth, antirez, and community finetuners are producing GGUF versions within days of base model releases, enabling local inference at scale. Notable is the rise of **uncensored fine‑tunes** (supergemma4) and **specialized reasoning models** (ZAYA1‑8B). We also see architectural experimentation—**HiDream‑O1‑Image** applies chain‑of‑thought to image generation, and **inclusionAI’s Ring** introduces a novel hybrid transformer at 1T scale. Finally, utility repos (fixed chat templates, ComfyUI workflows) are gaining significant likes, reflecting a maturing ecosystem where community tooling matters as much as model weights.

---

## Worth Exploring

1. **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — Combines O1‑style step‑by‑step reasoning with image generation, a promising direction for controllable visual synthesis. Ideal for researchers interested in neuro‑symbolic image models.

2. **[TencentARC/Pixal3D](https://huggingface.co/TencentARC/Pixal3D)** — Freshly released image‑to‑3D model from Tencent with an accompanying arxiv paper. With zero downloads but 138 likes, it’s a prime candidate for early‑stage experimentation in 3D asset generation.

3. **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** — A reasoning‑base model fine‑tuned from a specialized foundation, with published methodology (arxiv:2605.05365). It offers a unique chance to study reasoning distillation in the 8B parameter range.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*