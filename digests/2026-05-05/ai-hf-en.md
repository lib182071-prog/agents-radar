# Hugging Face Trending Models Digest 2026-05-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-05 07:32 UTC

---

# Hugging Face Trending Models Digest — 2026-05-05

## 1. Today's Highlights

This week's top trends are dominated by **large-scale multimodal and language models** from major players. **DeepSeek V4** leads the chart with both a Pro variant and a Flash variant, while **Google’s Gemma 4‑31B‑it** continues to see massive adoption (over 8 million downloads). The **Qwen 3.6** series (including a 35B MoE) shows high community engagement, with several quantization variants appearing in the top 30. Notably, **NVIDIA’s Nemotron‑3 Nano Omni** brings an any-to-any pipeline (text, image, audio, video), signaling a shift toward unified multimodal models. Meanwhile, **OpenAI’s privacy filter** is an interesting new addition for token‑level PII detection, and **Xiaomi’s MiMo V2.5** and **InclusionAI’s Ling 2.6** further diversify the landscape with agent‑focused and hybrid architectures.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, Chat, Instruction‑Tuned)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [**DeepSeek-V4-Pro**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 3,536 | 534,942 | Flagship conversational LLM from DeepSeek, topping the chart with massive community interest. |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 946 | 489,465 | A faster, lighter sibling of V4-Pro, optimized for efficiency while retaining strong conversational capabilities. |
| [**MiMo-V2.5-Pro**](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro) | XiaomiMiMo | 429 | 11,812 | Xiaomi’s long‑context agent‑focused LLM, designed for complex reasoning and tool use. |
| [**Mistral-Medium-3.5-128B**](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B) | mistralai | 259 | 11,950 | Mistral’s latest 128B‑parameter medium model with bilingual (EN/FR) support and vLLM compatibility. |
| [**Laguna-XS.2**](https://huggingface.co/poolside/Laguna-XS.2) | poolside | 214 | 10,357 | A code‑oriented LLM from poolside, optimized for developer workflows and vLLM inference. |
| [**talkie-1930-13b-it**](https://huggingface.co/talkie-lm/talkie-1930-13b-it) | talkie-lm | 229 | 0 | Instruction‑tuned 13B model based on a proprietary base, gaining likes despite zero downloads (likely fresh upload). |
| [**granite-4.1-8b**](https://huggingface.co/ibm-granite/granite-4.1-8b) | ibm-granite | 151 | 18,310 | IBM’s 8B Granite 4.1 language model, targeting enterprise text‑generation tasks. |
| [**granite-4.1-30b**](https://huggingface.co/ibm-granite/granite-4.1-30b) | ibm-granite | 96 | 4,094 | Larger 30B Granite variant for more demanding language understanding and generation. |
| [**Ling-2.6-flash**](https://huggingface.co/inclusionAI/Ling-2.6-flash) | inclusionAI | 456 | 1,141 | A hybrid bailing architecture flash model by InclusionAI, balancing speed and quality. |
| [**Ling-2.6-1T**](https://huggingface.co/inclusionAI/Ling-2.6-1T) | inclusionAI | 407 | 747 | The 1‑trillion‑parameter flagship of InclusionAI’s Ling series, pushing frontier performance. |

### 🎨 Multimodal & Generation (Image, Video, Audio, Any-to-Any)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [**Gemma-4-31B-it**](https://huggingface.co/google/gemma-4-31B-it) | google | 2,508 | 8,042,257 | Google’s instruction‑tuned multimodal model (image‑text‑to‑text) with enormous community adoption. |
| [**Qwen3.6-35B-A3B**](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 1,614 | 2,726,360 | Qwen’s Mixture‑of‑Experts multimodal model (35B total, 3B active) for efficient image‑text tasks. |
| [**Qwen3.6-27B**](https://huggingface.co/Qwen/Qwen3.6-27B) | Qwen | 1,113 | 1,334,241 | A lighter 27B dense multimodal model in the Qwen 3.6 family, widely used for vision‑language applications. |
| [**Kimi-K2.6**](https://huggingface.co/moonshotai/Kimi-K2.6) | moonshotai | 1,199 | 825,320 | Moonshot AI’s image‑text‑to‑text model with compressed‑tensors, gaining strong traction. |
| [**Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16**](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16) | nvidia | 231 | 40,403 | NVIDIA’s any‑to‑any reasoning model (30B MoE, 3B active) processing text, image, audio, and video. |
| [**SenseNova-U1-8B-MoT**](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT) | sensenova | 147 | 1,714 | A small multimodal any‑to‑any model (8B) from SenseNova, suited for edge and fast inference. |
| [**MiMo-V2.5**](https://huggingface.co/XiaomiMiMo/MiMo-V2.5) | XiaomiMiMo | 208 | 51,554 | Xiaomi’s multimodal base model supporting vision, language, and audio, with strong download activity. |
| [**Sulphur-2-base**](https://huggingface.co/SulphurAI/Sulphur-2-base) | SulphurAI | 187 | 20,187 | A text‑to‑video diffusion model available in GGUF format for efficient video generation. |
| [**Z-Anime**](https://huggingface.co/SeeSee21/Z-Anime) | SeeSee21 | 140 | 2,622 | A community text‑to‑image diffusion model tailored for anime‑style generation. |

### 🔧 Specialized Models (Security, Embeddings, Translation, Uncensored)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [**privacy-filter**](https://huggingface.co/openai/privacy-filter) | openai | 1,271 | 132,595 | OpenAI’s token‑classification model for detecting PII, released in ONNX format for easy deployment. |
| [**granite-embedding-97m-multilingual-r2**](https://huggingface.co/ibm-granite/granite-embedding-97m-multilingual-r2) | ibm-granite | 76 | 2,191 | A 97M multilingual embedding model from IBM, supporting sentence‑transformers and OpenVINO. |
| [**Hy-MT1.5-1.8B-1.25bit**](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit) | AngelSlim | 90 | 16,307 | A heavily quantized (1.25‑bit) translation model based on Hunyuan V1, trading quality for extreme compression. |

### 📦 Fine‑tunes & Quantizations (Community Fine‑tunes, GGUF, NVFP4, DFlash)

| Model | Author | Likes | Downloads | Description |
|-------|--------|-------|-----------|-------------|
| [**Qwen3.6-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF) | unsloth | 570 | 1,092,141 | Unsloth’s GGUF quantization of Qwen 3.6 27B, enabling efficient local inference on consumer hardware. |
| [**Qwen3.6-35B-A3B-GGUF**](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF) | unsloth | 911 | 2,174,698 | GGUF version of the MoE Qwen 3.6 35B, extremely popular for its low‑active‑parameter efficiency. |
| [**NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF**](https://huggingface.co/unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF) | unsloth | 100 | 44,790 | Unsloth’s GGUF quant of NVIDIA’s any‑to‑any reasoning model, bringing multimodal to low‑resource setups. |
| [**Qwen3.5-9B-DeepSeek-V4-Flash-GGUF**](https://huggingface.co/Jackrong/Qwen3.5-9B-DeepSeek-V4-Flash-GGUF) | Jackrong | 79 | 55,511 | A merged GGUF combining Qwen 3.5 9B and DeepSeek V4 Flash, mixing vision and language capabilities. |
| [**Qwen3.6-27B-DFlash**](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash) | z-lab | 231 | 23,407 | A community fine‑tune variant of Qwen 3.6 27B with optimized flash attention and feature extraction. |
| [**Gemma-4-31B-JANG_4M-CRACK**](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK) | dealignai | 1,469 | 203,362 | An abliterated / uncensored fine‑tune of Gemma 4 31B, very popular among users seeking fewer content restrictions. |
| [**Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4**](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4) | nvidia | 85 | 276,956 | NVIDIA’s own NVFP4 (4‑bit floating point) quantization of their Omni model, offering a high‑performance compact variant. |

## 3. Ecosystem Signal

The current ecosystem is defined by a **race toward unified multimodal models** that handle text alongside images, video, and audio. NVIDIA’s Nemotron‑3 Nano Omni and Sensenova’s SenseNova‑U1 both adopt an “any‑to‑any” pipeline, while Qwen 3.6, Gemma 4, Kimi K2.6, and MiMo V2.5 all natively support vision‑language tasks. This suggests that text‑only models are no longer the main focus; multimodal capability is becoming a default expectation.

**Open‑weight models continue to dominate** the trending list — all top 30 are publicly released with permissive or open licenses. Meanwhile, **quantization activity is surging**: Unsloth alone accounts for three GGUF entries, and NVIDIA provides its own NVFP4 quant. Community fine‑tunes like the Gemma‑4 uncensored variant (dealignai) attract high interaction, reflecting demand for models with fewer guardrails.

**Size matters, but efficiency is key.** The success of MoE models (Qwen 3.6 35B‑A3B, Nemotron‑3 Nano) and small but capable models (Sulphur‑2 for video, Ling‑2.6‑flash) shows that users want both scale and practical deployability. Xiaomi’s MiMo and InclusionAI’s Ling indicate growing interest from Asian tech giants in the open‑model ecosystem.

## 4. Worth Exploring

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — The top‑liked model of the week. Its combination of classic text‑generation performance and massive community adoption makes it a must‑test for LLM tasks, from chat to complex reasoning. The accompanying Flash variant offers a speed‑oriented alternative.

2. **[Nemotron-3-Nano-Omni-30B-A3B-Reasoning](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** — A frontier any‑to‑any model that processes text, images, audio, and video in a single architecture. It represents the cutting edge of multimodal reasoning, and its MoE design (3B active parameters) makes it accessible on consumer GPUs, especially via the GGUF and NVFP4 quantizations.

3. **[Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** — Despite being an uncensored fine‑tune, it has collected 1,469 likes and 203K downloads, showing strong demand for “abliterated” models. It’s particularly interesting to study how community modifications of safety alignment affect adoption and qualitative output.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*