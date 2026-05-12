# Hugging Face Trending Models Digest 2026-05-12

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-12 09:49 UTC

---

# Hugging Face Trending Models Digest — 2026-05-12

## Today’s Highlights

The week is dominated by **open-weight multimodal models** and **quantized community variants**. DeepSeek’s **V4-Pro** and **V4-Flash** lead text-generation with a combined 4.9K likes and over 3M downloads, while Google’s **Gemma-4** family expands rapidly — the 31B-it alone has 9M downloads. The **Qwen3.6** series (27B and 35B-A3B MoE) continues to surge, with the unsloth GGUF quantizations already racking up millions of downloads. In the audio space, **OmniVoice** (zero-shot voice cloning) hits 854 likes and 2.2M downloads, and OpenAI releases a **privacy-filter** token-classification model. Video generation is also gaining traction with **Sulphur-2-base** (text-to-video) and **LTX2.3-10Eros** (image-to-video).

---

## Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  *deepseek-ai* · 3,870 likes · 2,017,835 downloads  
  Flagship text-generation model with state-of-the-art conversational ability, driving heavy adoption.

- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  *deepseek-ai* · 1,051 likes · 1,162,290 downloads  
  Optimized faster variant of DeepSeek V4, balancing performance and efficiency.

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)**  
  *Zyphra* · 436 likes · 66,119 downloads  
  8B reasoning model fine-tuned from a base via reinforcement learning, accompanied by an arxiv paper.

- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)**  
  *XiaomiMiMo* · 511 likes · 41,654 downloads  
  Long-context agent model from Xiaomi, designed for complex multi-turn tasks.

- **[z-lab/gemma-4-31B-it-DFlash](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash)**  
  *z-lab* · 78 likes · 6,423 downloads  
  Speculative-decoding variant of Gemma-4-31B-it for faster inference.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  *SulphurAI* · 671 likes · 157,648 downloads  
  Text-to-video model using diffusers, one of the top trending video generation entries.

- **[MiniCPM-V-4.6](https://huggingface.co/openbmb/MiniCPM-V-4.6)**  
  *openbmb* · 339 likes · 0 downloads  
  Latest multimodal vision-language model from OpenBMB (newly released, no downloads yet).

- **[HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)**  
  *HiDream-ai* · 256 likes · 3,418 downloads  
  Image generation model built on a Qwen3 vision backbone, producing images from text+image prompts.

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)**  
  *SeeSee21* · 314 likes · 9,477 downloads  
  Text-to-image model specialized for anime art, available with GGUF and diffusers.

- **[LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)**  
  *TenStrip* · 227 likes · 64,008 downloads  
  Image-to-video generation model, region-locked to the US.

- **[Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
  *Qwen* · 1,245 likes · 2,446,478 downloads  
  Flagship multimodal (image-text-to-text) model from Qwen, highly performant and widely downloaded.

- **[gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)**  
  *google* · 212 likes · 66,561 downloads  
  Assistant-tuned variant of Gemma-4 with any-to-any (image, audio, text) capability.

- **[gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)**  
  *google* · 117 likes · 47,749 downloads  
  MoE assistant variant of Gemma-4, offering efficient multimodal processing.

- **[gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**  
  *google* · 2,607 likes · 9,119,339 downloads  
  Base instruction-tuned multimodal Gemma-4, the most downloaded model in this digest.

- **[gemma-4-26B-A4B-it](https://huggingface.co/google/gemma-4-26B-A4B-it)**  
  *google* · 932 likes · 7,179,265 downloads  
  MoE multimodal variant of Gemma-4, balancing quality and efficiency.

- **[gemma-4-E4B-it-assistant](https://huggingface.co/google/gemma-4-E4B-it-assistant)**  
  *google* · 68 likes · 51,766 downloads  
  Ultra-compact 4B-parameter assistant variant for resource-constrained deployment.

- **[SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)**  
  *sensenova* · 236 likes · 4,528 downloads  
  Any-to-any multimodal model using Mixture-of-Transformers (MoT) architecture.

- **[OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)**  
  *k2-fsa* · 854 likes · 2,224,595 downloads  
  Zero-shot, multilingual voice cloning text-to-speech model, highly trended.

- **[HiDream-O1-Image-Dev](https://huggingface.co/HiDream-ai/HiDream-O1-Image-Dev)**  
  *HiDream-ai* · 81 likes · 1,367 downloads  
  Developer release of HiDream image generation model.

- **[moonshotai/Kimi-K2.6](https://huggingface.co/moonshotai/Kimi-K2.6)**  
  *moonshotai* · 1,264 likes · 1,423,653 downloads  
  Kimi’s latest multimodal model with compressed-tensors and strong community traction.

- **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  *Qwen* · 1,728 likes · 3,858,503 downloads  
  MoE multimodal model, extremely popular for its strong performance and low active parameter count.

- **[supertone-3](https://huggingface.co/Supertone/supertonic-3)**  
  *Supertone* · 107 likes · 1,837 downloads  
  Text-to-speech model with ONNX support for high-quality speech synthesis.

### 🔧 Specialized Models (privacy, templates, translation)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**  
  *openai* · 1,417 likes · 190,993 downloads  
  Token-classification model from OpenAI for detecting privacy-sensitive content in text.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
  *froggeric* · 149 likes · 0 downloads  
  Corrected Jinja chat templates for Qwen models, a utility gaining popularity.

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)**  
  *AngelSlim* · 166 likes · 17,260 downloads  
  Extremely aggressive 1.25-bit quantization of a translation model (Hy-MT) for memory-constrained use.

### 📦 Fine-tunes & Quantizations (GGUF, community variants)

- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)**  
  *Jackrong* · 114 likes · 67,205 downloads  
  GGUF quantized version of the Qwen3.6-35B-A3B MoE model.

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)**  
  *unsloth* · 1,000 likes · 2,733,708 downloads  
  Community GGUF quantization of Qwen3.6 MoE, extremely popular due to unsloth’s reputation.

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)**  
  *unsloth* · 658 likes · 1,468,142 downloads  
  GGUF quantization of Qwen3.6-27B, widely used for local inference.

- **[havenoammo/Qwen3.6-27B-MTP-UD-GGUF](https://huggingface.co/havenoammo/Qwen3.6-27B-MTP-UD-GGUF)**  
  *havenoammo* · 80 likes · 43,428 downloads  
  Specialized GGUF variant of Qwen3.6-27B with multi-token prediction support.

- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  *DavidAU* · 134 likes · 197,110 downloads  
  Community uncensored fine-tune of Qwen3.6-27B in GGUF format, optimized for code and uncensored outputs.

---

## Ecosystem Signal

Open‑source multimodal models are **cementing their dominance**: almost every leading family (DeepSeek, Qwen, Gemma, Kimi) now ships image‑text‑to‑text or any‑to‑any capabilities, making pure text‑only LLMs increasingly rare. **Mixture‑of‑Experts (MoE)** architectures are particularly hot — the Qwen3.6‑35B‑A3B and Gemma‑4‑26B‑A4B variants achieve strong performance with much lower inference costs, driving massive adoption. **Quantization and community fine‑tuning** activity is at an all‑time high; unsloth’s GGUF conversions alone have accumulated over 4.2M downloads this week, and niche fine‑tunes (uncensored, code‑focused) are gaining traction. The **audio‑generation** sector is also maturing: OmniVoice’s zero‑shot multilingual voice cloning sees rapid uptake, while text‑to‑speech and voice cloning are branching into production‑ready ONNX models. OpenAI’s release of a **privacy filter** indicates a growing emphasis on safety tooling alongside model releases. Overall, the ecosystem is converging on **unified multimodal models**, with a strong community tail enabling flexible deployment (quantized, fine‑tuned, speculative‑decoded) for every use case.

---

## Worth Exploring

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – The highest‑liked text‑generation model this week, representing the cutting edge in open‑weight conversational AI. Worth studying for its architecture and scaling approach.

2. **[OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – Impressive zero‑shot voice cloning across languages, with 854 likes and 2.2M downloads. A must‑try for anyone working on TTS or speech synthesis.

3. **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – The MoE multimodal model with the highest download count (3.8M) and strong community support. Its efficiency‑performance trade‑off makes it a prime candidate for deployment and further fine‑tuning.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*