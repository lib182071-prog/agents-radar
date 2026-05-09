# Hugging Face Trending Models Digest 2026-05-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-09 07:22 UTC

---

# Hugging Face Trending Models Digest — 2026-05-09

## 🏆 Today’s Highlights

This week’s trending list is dominated by **multimodal MoE models** and their **GGUF quantizations**, with Qwen’s Qwen3.6-35B-A3B and Google’s Gemma-4-31B-it leading in downloads (3.4M and 8.7M, respectively). DeepSeek-V4-Pro and DeepSeek-V4-Flash continue to draw massive community interest, while **uncensored and abliterated fine-tunes** of Gemma-4 and Qwen3.6 see explosive traction. Notably, OpenAI released a **privacy-filter** classification model, and **OmniVoice** (815 weekly likes) signals growing demand for zero-shot multilingual TTS. Quantization activity from unsloth and others shows the community is eager to run these 30B+ models locally.

---

## 🧠 Language Models

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai • 3,764 likes • 1,061,344 downloads  
  The latest flagship LLM from DeepSeek, trending for its strong conversational performance and vast parameter scale.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — deepseek-ai • 1,009 likes • 848,696 downloads  
  A more efficient sibling of V4-Pro, optimized for fast inference without sacrificing quality.

- **[MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)** — XiaomiMiMo • 489 likes • 26,600 downloads  
  Xiaomi’s long-context agent model, gaining attention for its agentic capabilities and extended context window.

- **[Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)** — mistralai • 305 likes • 21,300 downloads  
  Mistral’s 128B multilingual model supporting English and French, valued for its open-weight, vLLM-compatible release.

- **[ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** — Zyphra • 294 likes • 6,810 downloads  
  A research-focused 8B model with an accompanying arxiv paper (2605.05365), intriguing the research community.

- **[Laguna-XS.2](https://huggingface.co/poolside/Laguna-XS.2)** — poolside • 234 likes • 18,863 downloads  
  A code-generation model from Poolside, likely fine-tuned for software engineering tasks.

---

## 🎨 Multimodal & Generation

- **[Gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google • 2,572 likes • 8,731,301 downloads  
  Google’s top multimodal model (image-text-to-text), by far the most downloaded model this week.

- **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — Qwen • 1,682 likes • 3,363,621 downloads  
  A **MoE** version of Qwen3.6 with 35B total parameters and 3B active, striking a balance between performance and efficiency.

- **[Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — Qwen • 1,195 likes • 1,958,217 downloads  
  Dense variant of Qwen3.6, widely used for image-text-to-text tasks and conversational AI.

- **[OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** — k2-fsa • 815 likes • 2,242,587 downloads  
  Zero-shot, multilingual text-to-speech with voice cloning, trending for its production-ready quality.

- **[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — SulphurAI • 457 likes • 92,968 downloads  
  A text-to-video diffusion model, reflecting the rising interest in generative video.

- **[Nemotron-3-Nano-Omni-30B-A3B-Reasoning](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** — nvidia • 265 likes • 89,837 downloads  
  NVIDIA’s any-to-any MoE reasoning model, notable for its Omni architecture and reasoning capabilities.

- **[SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** — sensenova • 203 likes • 2,947 downloads  
  A multimodal any-to-any model from SenseTime, interesting for its “Mixture of Tasks” design.

- **[Gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** — google • 167 likes • 33,314 downloads  
  An assistant-tuned variant of Gemma-4-31B, optimizing for interactive use.

- **[Gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)** — google • 94 likes • 22,723 downloads  
  A smaller MoE assistant (26B total, 4B active) from the Gemma-4 family.

- **[Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** — SeeSee21 • 244 likes • 5,077 downloads  
  A text-to-image anime model, popular among creative communities.

- **[LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** — TenStrip • 172 likes • 42,529 downloads  
  An image-to-video model, likely a fine-tune of the LTX pipeline for specific aesthetics.

---

## 🔧 Specialized Models

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — openai • 1,373 likes • 173,110 downloads  
  OpenAI’s token-classification model for detecting private information, trending due to its practical safety use case.

- **[Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** — AngelSlim • 142 likes • 16,778 downloads  
  An extremely quantized (1.25-bit) translation model based on Hunyuan, pushing the boundaries of model compression.

- **[talkie-1930-13b-it](https://huggingface.co/talkie-lm/talkie-1930-13b-it)** — talkie-lm • 253 likes • 0 downloads  
  A fine-tuned conversational model built on the talkie-1930-13b-base, likely optimized for dialogue.

- **[Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric • 114 likes • 0 downloads  
  Not a model but a utility repository fixing Jinja chat templates for Qwen3.5, demonstrating community maintenance.

---

## 📦 Fine-Tunes & Quantizations

- **[Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** — dealignai • 1,491 likes • 156,146 downloads  
  An abliterated, uncensored fine-tune of Gemma-4-31B-it, extremely popular for removing safety guardrails.

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** — unsloth • 966 likes • 2,500,343 downloads  
  The GGUF quantized version of Qwen3.6-35B-A3B, enabling local deployment via llama.cpp.

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** — unsloth • 627 likes • 1,312,422 downloads  
  Similarly quantized dense 27B variant, popular for its lower resource footprint.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS • 588 likes • 996,892 downloads  
  An uncensored, “aggressive” MoE vision fine-tune of Qwen3.6, reflecting demand for less restricted models.

- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)** — DavidAU • 105 likes • 143,853 downloads  
  A heavily modified uncensored GGUF with code emphasis and advanced quantization techniques.

- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** — z-lab • 270 likes • 30,478 downloads  
  A speculative-decoding variant of Qwen3.6-27B, optimizing inference speed.

- **[z-lab/gemma-4-31B-it-DFlash](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash)** — z-lab • 66 likes • 2,155 downloads  
  Speculative-decoding variant of Gemma-4-31B-it, a niche but technically interesting fine-tune.

- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)** — Jackrong • 87 likes • 18,981 downloads  
  Another GGUF of the Qwen3.6-35B-A3B, with unsloth integration.

- **[Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF](https://huggingface.co/Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF)** — Jackrong • 108 likes • 128,635 downloads  
  A creative merge of Qwen3.5-9B with DeepSeek-V4-Flash flavors, quantized to GGUF.

---

## 🌐 Ecosystem Signal

The ecosystem is clearly pivoting to **multimodal MoE architectures**: Qwen3.6-35B-A3B, Gemma-4-26B-A4B, and Nemotron-3-Nano-Omni all use mixture-of-experts to keep active parameters low while total capacity high. **GGUF quantization** remains the dominant format for local inference, with unsloth’s releases amassing millions of downloads—the community is hungry for accessible, runnable models. There is also a notable surge in **uncensored/abliterated fine-tunes**: both Gemma-4 and Qwen3.6 have multiple such variants scoring high likes, indicating a demand for models without safety guardrails. Meanwhile, **open-weight releases** from DeepSeek, Google, Qwen, and Mistral continue to dominate top spots, while proprietary players like OpenAI (privacy-filter) and Xiaomi (MiMo) join the open ecosystem. The rise of **speculative-decoding fine-tunes** (DFlash) suggests optimization for speed is becoming a core community activity.

---

## 🔍 Worth Exploring

1. **[Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** — The highest-liked fine-tune this week (1,491 likes). Studying its abliteration technique can reveal how safety mechanisms are removed, a controversial but technically significant direction in model customization.

2. **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — A cornerstone MoE multimodal model. With 3.4M downloads, it represents the state of the art in efficient vision-language reasoning. Its architecture is likely to influence future model designs.

3. **[OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** — A zero-shot TTS model with 2.2M downloads and multilingual support. For developers building voice interfaces, this is a ready-to-use, high-quality solution worth evaluating immediately.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*