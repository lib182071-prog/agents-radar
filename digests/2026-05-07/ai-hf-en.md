# Hugging Face Trending Models Digest 2026-05-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-07 09:44 UTC

---

# Hugging Face Trending Models Digest — 2026-05-07

## Today’s Highlights

DeepSeek-V4-Pro claims the top spot with over 3,600 weekly likes and nearly 1M downloads, solidifying its position as the leading open‑weight LLM. The Qwen3.6 family continues to dominate the ecosystem: four entries (including GGUF variants) appear in the top 25, with the MoE‑based **Qwen3.6‑35B‑A3B** alone exceeding 3.2M downloads this week. Google’s **Gemma‑4‑31B‑it** sees explosive adoption (8.6M downloads, 2,500+ likes), while uncensored fine‑tunes and quantized variants of these flagship models—such as `dealignai/Gemma‑4‑31B-JANG_4M-CRACK` and `unsloth/Qwen3.6-35B-A3B-GGUF`—reflect the community’s appetite for customizable, locally deployable AI. Additionally, new video‑generation models (`SulphurAI/Sulphur-2-base`, `TenStrip/LTX2.3-10Eros`) and an any‑to‑any assistant from NVIDIA (`Nemotron-3-Nano-Omni-30B-A3B-Reasoning`) signal a broadening of the multimodal frontier.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction‑tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* · 3,688 likes · 946k downloads  
  The week’s most‑liked model, a state‑of‑the‑art conversational LLM powering the next generation of open‑weight chat systems.

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — *deepseek-ai* · 969 likes · 751k downloads  
  A faster, distilled variant of DeepSeek‑V4 for lightweight deployment without sacrificing quality.

- **[mistralai/Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)** — *mistralai* · 286 likes · 18k downloads  
  A 128B‑parameter medium‑sized flagship from Mistral, optimized for bilingual English/French tasks with vLLM support.

- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)** — *XiaomiMiMo* · 465 likes · 21k downloads  
  A long‑context agent‑friendly LLM designed for extended reasoning and tool‑use scenarios.

- **[poolside/Laguna-XS.2](https://huggingface.co/poolside/Laguna-XS.2)** — *poolside* · 229 likes · 17k downloads  
  A compact yet capable text‑generation model from the Laguna family, built for efficient code‑centric applications.

- **[ibm-granite/granite-4.1-8b](https://huggingface.co/ibm-granite/granite-4.1-8b)** — *ibm-granite* · 161 likes · 24k downloads  
  IBM’s latest 8B Granite model, offering a balanced trade‑off between performance and resource requirements.

- **[ibm-granite/granite-4.1-30b](https://huggingface.co/ibm-granite/granite-4.1-30b)** — *ibm-granite* · 103 likes · 9k downloads  
  The larger 30B sibling of Granite 4.1, targeting enterprise‑grade text generation.

- **[inclusionAI/Ling-2.6-1T](https://huggingface.co/inclusionAI/Ling-2.6-1T)** — *inclusionAI* · 424 likes · 1.6k downloads  
  A massive 1T‑parameter hybrid conversational model from inclusionAI, demonstrating the race toward trillion‑scale open LLMs.

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** — *Zyphra* · 115 likes · 539 downloads  
  An Apache‑2.0 licensed 8B model with published evaluation results, designed for transparent research use.

- **[talkie-lm/talkie-1930-13b-it](https://huggingface.co/talkie-lm/talkie-1930-13b-it)** — *talkie-lm* · 239 likes · 0 downloads  
  A fine‑tuned 13B instruction‑tuned model optimized for conversational settings.

- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** — *z-lab* · 252 likes · 29k downloads  
  A distilled, flash‑attention enabled variant of Qwen3.6‑27B for faster inference.

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X)

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — *SulphurAI* · 322 likes · 71k downloads  
  A leading text‑to‑video diffusion model (GGUF compatible) bringing professional video generation to the open‑source community.

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** — *SeeSee21* · 202 likes · 4.5k downloads  
  A text‑to‑image model specialized in anime/manga stylization, leveraging diffusers and GGUF for broad accessibility.

- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** — *TenStrip* · 141 likes · 28k downloads  
  An image‑to‑video model that transforms still frames into seamless short video clips.

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — *Qwen* · 1,164 likes · 1.8M downloads  
  A vision‑language flagship that understands images and text jointly, powering advanced multimodal chatbots.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — *Qwen* · 1,653 likes · 3.2M downloads  
  A Mixture‑of‑Experts vision‑language model achieving high efficiency (3B active params) while rivaling dense 35B performance.

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — *google* · 2,545 likes · 8.6M downloads  
  Google’s most popular Gemma‑4 release this week, a 31B multimodal model that handles both image and text inputs.

- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** — *google* · 130 likes · 20k downloads  
  An “any‑to‑any” assistant variant of Gemma‑4, capable of processing and generating across multiple modalities.

- **[google/gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)** — *google* · 80 likes · 13k downloads  
  A more efficient Gemma‑4 assistant using MoE (26B total, 4B active) for multimodal tasks.

- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** — *nvidia* · 256 likes · 65k downloads  
  NVIDIA’s any‑to‑any MoE model (30B total, 3B active) with explicit reasoning capabilities, optimized for BF16.

- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** — *sensenova* · 168 likes · 2.7k downloads  
  A multimodal “Mixture of Tokens” model that integrates vision, language, and audio understanding.

- **[XiaomiMiMo/MiMo-V2.5](https://huggingface.co/XiaomiMiMo/MiMo-V2.5)** — *XiaomiMiMo* · 218 likes · 65k downloads  
  Xiaomi’s multimodal foundation model supporting vision‑language and audio tasks in a unified framework.

### 🔧 Specialized Models (code, math, medical, embeddings, privacy)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — *openai* · 1,332 likes · 165k downloads  
  A token‑classification model (ONNX compatible) that detects and redacts personally identifiable information in text.

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** — *AngelSlim* · 102 likes · 17k downloads  
  An extremely quantized (1.25‑bit) translation model based on Hunyuan, enabling multilingual MT on ultra‑low‑resource devices.

### 📦 Fine‑tunes & Quantizations (community fine‑tunes, GGUF, AWQ)

- **[dealignai/Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** — *dealignai* · 1,484 likes · 170k downloads  
  An abliterated, uncensored fine‑tune of Gemma‑4‑31B that removes safety filters while retaining core capabilities.

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** — *unsloth* · 603 likes · 1.3M downloads  
  A widely‑used GGUF quantization of Qwen3.6‑27B, enabling local inference on consumer hardware via llama.cpp.

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** — *unsloth* · 948 likes · 2.4M downloads  
  GGUF quant of the MoE Qwen3.6‑35B‑A3B, making it accessible for edge and personal deployments.

- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)** — *DavidAU* · 85 likes · 127k downloads  
  An extensively uncensored, code‑optimized GGUF fine‑tune of Qwen3.6‑27B with multiple quantization matrix variants.

- **[Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF](https://huggingface.co/Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF)** — *Jackrong* · 98 likes · 105k downloads  
  A merged GGUF model combining Qwen3.5‑9B and DeepSeek‑V4‑Flash, targeting efficient multimodal text generation.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* · 572 likes · 973k downloads  
  An uncensored, “aggressive” fine‑tune of Qwen3.6‑35B‑A3B (GGUF) that pushes the model’s creative and adversarial boundaries.

## Ecosystem Signal

The current landscape is defined by three converging trends:

**1. Mixture‑of‑Experts (MoE) becomes the norm.** Nearly every major family now offers an MoE variant: Qwen3.6‑35B‑A3B, Gemma‑4‑26B‑A4B, and Nemotron‑3‑Nano‑Omni‑30B‑A3B. These models achieve dense‑scale performance with a fraction of the active parameters, driving the democratization of large models on consumer GPUs.

**2. Unfiltered / uncensored model proliferation.** The community is actively “abliterating” safety layers from flagship models (Gemma‑4, Qwen3.6) to create unrestricted variants. While ethically contentious, this trend reflects a strong demand for creative and investigative model use—particularly in role‑play, fiction, and code generation.

**3. Quantization as a first‑class citizen.** GGUF variants of the week’s top models (DeepSeek‑V4‑Pro, Qwen3.6, Gemma‑4) consistently see download counts in the millions, outpacing the original float‑weight versions. The unsloth team leads in providing optimized, easy‑to‑deploy quantizations, and the ecosystem now expects every new release to ship with a GGUF companion.

Open‑weight models continue to dominate the trending list, with proprietary guardrails largely circumvented through fine‑tuning. The rise of video‑generation models (Sulphur‑2, LTX2.3) and any‑to‑any architectures (Gemma‑4‑assistant, SenseNova‑U1) hints at the next frontier: unified multimodal agents that can see, hear, speak, and create.

## Worth Exploring

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — As the week’s top‑ranked model by likes and downloads, it represents the current ceiling of open‑weight LLM performance. Study its architecture and conversational capabilities to understand what drives state‑of‑the‑art chat.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — With 3.2M downloads and an efficient MoE design, this model is the most practical multimodal workhorse. It offers a rare combination of vision‑language understanding, low inference cost, and strong community support via GGUF.

- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** — The “any‑to‑any” label is unique to this model, promising a unified interface for text, images, and potentially audio/video outputs. It is a glimpse into the future of truly universal AI assistants and merits hands‑on evaluation.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*