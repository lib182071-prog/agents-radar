# Hugging Face Trending Models Digest 2026-05-08

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-08 06:18 UTC

---

# 🤗 Hugging Face Trending Models Digest – 2026-05-08

## Today's Highlights

This week’s trending models are dominated by the **Qwen3.6** family, with multiple variants (27B and 35B-A3B MoE) amassing millions of downloads each, alongside a surge of **GGUF quantizations** by unsloth and community finetuners like DavidAU and HauhauCS. **Google’s Gemma-4** series continues to gain traction, especially the 31B-instruction model and its uncensored derivative from dealignai. In the multimodal space, **Sulphur-2-base** (text-to-video) and **OmniVoice** (zero-shot voice cloning) represent notable new capabilities. Meanwhile, **DeepSeek-V4-Pro** and **V4-Flash** maintain strong momentum as leading open-weight LLMs.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek-ai (3,731 likes, 946k downloads) – Core flagship LLM from DeepSeek, leading in conversational quality and steep adoption curve.
- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** – deepseek-ai (987 likes, 751k downloads) – Faster, distilled variant of V4-Pro for efficient inference, extremely popular for deployment.
- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)** – Zyphra (217 likes, 539 downloads) – Apache-2.0 licensed 8B base model with strong evaluation results, gaining early community interest.
- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)** – XiaomiMiMo (477 likes, 21k downloads) – Long-context agent-oriented LLM optimized for tool use and reasoning tasks.
- **[Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)** – mistralai (295 likes, 18k downloads) – Large 128B parameter Mistral model with bilingual (EN/FR) support and vLLM compatibility.
- **[poolside/Laguna-XS.2](https://huggingface.co/poolside/Laguna-XS.2)** – poolside (232 likes, 17k downloads) – Code-oriented text-generation model from poolside, targeting software engineering use cases.
- **[talkie-lm/talkie-1930-13b-it](https://huggingface.co/talkie-lm/talkie-1930-13b-it)** – talkie-lm (245 likes, 0 downloads) – Instruction-tuned 13B model based on the Talkie-1930 base, focused on conversational fluency.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** – SulphurAI (395 likes, 71k downloads) – Text-to-video diffusion model with GGUF support, emerging as a community favorite for video generation.
- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)** – SeeSee21 (228 likes, 4k downloads) – Anime-style text-to-image model built with diffusers, popular for creative AI art.
- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)** – TenStrip (154 likes, 28k downloads) – Image-to-video model, gaining traction for dynamic scene generation.
- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)** – google (147 likes, 20k downloads) – Any-to-any assistant variant of Gemma-4, designed for multimodal interaction.
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** – Qwen (1,181 likes, 1.77M downloads) – Image-text-to-text 27B model, a workhorse for vision-language tasks.
- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – Qwen (1,662 likes, 3.21M downloads) – MoE variant of Qwen3.6 with 35B total / 3B active parameters, balancing efficiency and quality.
- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** – sensenova (190 likes, 2.7k downloads) – Any-to-any multimodal model with “Mixture of Transformers” architecture, promising new fusion techniques.
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** – google (2,560 likes, 8.59M downloads) – The most downloaded Gemma-4 variant, a powerful image-text-to-text model with massive adoption.
- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** – nvidia (262 likes, 65k downloads) – Nvidia’s compact 30B MoE reasoning model for any-to-any tasks, optimized for edge and cloud.
- **[google/gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)** – google (85 likes, 13k downloads) – Smaller 26B assistant with 4B active parameters, complementing the 31B variant.
- **[google/gemma-4-E4B-it](https://huggingface.co/google/gemma-4-E4B-it)** – google (946 likes, 5.49M downloads) – Extreme-scale 4B active parameter model (likely 1T+ total?), showcasing Gemma-4 architecture at massive scale.
- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – k2-fsa (802 likes, 2.24M downloads) – Zero-shot multilingual voice cloning text-to-speech model, gaining traction for its realistic synthesis.

### 🔧 Specialized Models (code, math, medical, embeddings, utilities)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** – openai (1,351 likes, 165k downloads) – Token classification model for detecting/redacting personal information, widely used for privacy compliance.
- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** – AngelSlim (120 likes, 17k downloads) – Extreme low-bit quantization (1.25-bit) of a translation model, pushing boundaries of compression.
- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** – froggeric (98 likes, 0 downloads) – Utility model providing corrected chat templates for Qwen models, essential for proper inference.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[dealignai/Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** – dealignai (1,487 likes, 170k downloads) – Abliterated/uncensored fine-tune of Gemma-4-31B, highly popular for unrestricted use.
- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** – unsloth (620 likes, 1.26M downloads) – GGUF quantized version of Qwen3.6-27B, optimized for local inference with llama.cpp.
- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** – unsloth (956 likes, 2.42M downloads) – GGUF quant of the 35B MoE model, enabling efficient on-device deployment.
- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** – z-lab (263 likes, 29k downloads) – Specialized text-generation fine-tune of Qwen3.6-27B with DFlash technique, improving reasoning speed.
- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)** – Jackrong (73 likes, 4.8k downloads) – Community GGUF quantization of Qwen3.6-35B-A3B with custom naming “Qwopus.”
- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)** – DavidAU (94 likes, 127k downloads) – Uncensored, code-oriented GGUF finetune with extreme compression (IMatrix MAX).
- **[Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF](https://huggingface.co/Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF)** – Jackrong (103 likes, 105k downloads) – GGUF quantization merging Qwen3.5-9B with DeepSeek V4 Flash capabilities.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS (576 likes, 973k downloads) – Aggressive uncensored fine-tune of Qwen3.6 MoE, among the most downloaded community variants.

## Ecosystem Signal

The **Qwen3.6 family** has become the single most dominant ecosystem force this week, with the 35B-A3B MoE model alone amassing over 3.2 million downloads. The rapid production of GGUF quantizations by **unsloth** and numerous community finetuners reflects a strong demand for local, private, and efficient deployment. Meanwhile, **Google’s Gemma-4** series—particularly the 31B-it model (8.6M downloads) and its uncensored derivative—shows that open-weight models from Big Tech continue to attract massive interest, often rivaled only by community-abliterated variants. The rise of **any-to-any** pipelines (Gemma-4 assistant variants, SenseNova, Nvidia Nemotron) signals a convergence toward truly multimodal foundation models beyond simple text or image. **OpenAI’s privacy-filter** stands out as a rare non-generative tool, indicating growing demand for guardrails and compliance in model deployment. Quantization and fine-tuning activity remain intensely concentrated on the Qwen and Gemma lineages, with limited diversification into other families (e.g., Mistral, DeepSeek, and poolside are present but less active in community derivations).

## Worth Exploring

1. **[Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – The MoE architecture achieving competitive quality with much lower active parameters makes this a critical model to study for efficient deployment and scaling research.

2. **[OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** – With zero-shot multilingual voice cloning and high download velocity, this model represents a new frontier in open-source speech synthesis worth experimenting with for product integration.

3. **[dealignai/Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** – The most popular uncensored Gemma fine-tune offers a case study in the tension between safety alignment and community demand for unrestricted capabilities; understanding its training recipe (abliteration) is valuable.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*