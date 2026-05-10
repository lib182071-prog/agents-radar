# Hugging Face Trending Models Digest 2026-05-10

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-10 07:48 UTC

---

# 🧠 Hugging Face Trending Models Digest  
*2026-05-10* | Source: 30 most-liked models (weekly likes)

---

## 1. Today’s Highlights

This week is defined by a massive push toward **multimodal and MoE (Mixture-of-Experts) architectures**. Google’s **Gemma-4** family dominates with three entries, including the dense 31B and the efficient 26B-A4B MoE, while **Qwen3.6** models (27B dense and 35B-A3B MoE) continue to set download records—over 3.6M for the MoE variant. **DeepSeek-V4** also sees strong traction with both a Pro and a Flash version. In the visual generation space, **SulphurAI’s text-to-video base model** and **TenStrip’s image-to-video model** signal growing interest in video synthesis. Notably, **OpenAI’s privacy filter** silently gained 1.4K likes, and the community is actively producing uncensored and GGUF-quantized variants of leading models.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  Author: deepseek-ai | Likes: 3,793 | Downloads: 1,339,144  
  *The latest flagship from DeepSeek, a conversational text-generation model with massive adoption (3.8K weekly likes) and strong inference performance.*

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  Author: deepseek-ai | Likes: 1,012 | Downloads: 1,068,871  
  *A faster, distilled variant of DeepSeek-V4 optimized for lower latency, trending as a practical alternative to the Pro version.*

- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)**  
  Author: XiaomiMiMo | Likes: 501 | Downloads: 40,104  
  *Xiaomi's latest long-context agent-oriented LLM, gaining attention for its extended context window and agent capabilities.*

- **[Zyphra/ZAYA1-8B](https://huggingface.co/Zyphra/ZAYA1-8B)**  
  Author: Zyphra | Likes: 338 | Downloads: 44,834  
  *An 8B open-weight model with published evaluation results and Apache-2.0 license, noted for its research transparency.*

- **[mistralai/Mistral-Medium-3.5-128B](https://huggingface.co/mistralai/Mistral-Medium-3.5-128B)**  
  Author: mistralai | Likes: 309 | Downloads: 40,551  
  *Mistral's 128B-parameter dense model supporting English and French, popular among enterprise users for its vLLM compatibility.*

- **[z-lab/gemma-4-31B-it-DFlash](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash)**  
  Author: z-lab | Likes: 69 | Downloads: 5,193  
  *A speculative decoding variant of Gemma-4 31B using the DFlash technique, offering faster inference at lower cost.*

- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)**  
  Author: z-lab | Likes: 273 | Downloads: 33,487  
  *Qwen3.6 27B fine-tuned with DFlash for speculative decoding, illustrating the community's focus on inference speed.*

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
  Author: froggeric | Likes: 128 | Downloads: 0  
  *A utility model providing corrected Jinja chat templates for Qwen models, popular despite zero downloads (likely meta/model card).*

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  Author: SulphurAI | Likes: 500 | Downloads: 144,251  
  *A text-to-video diffusion model with Diffusers support and GGUF compatibility, trending as a strong open-source video generation contender.*

- **[SeeSee21/Z-Anime](https://huggingface.co/SeeSee21/Z-Anime)**  
  Author: SeeSee21 | Likes: 277 | Downloads: 8,994  
  *An anime-focused text-to-image model built on diffusers, capitalizing on the growing anime generation niche.*

- **[google/gemma-4-31B-it-assistant](https://huggingface.co/google/gemma-4-31B-it-assistant)**  
  Author: google | Pipeline: any-to-any | Likes: 178 | Downloads: 56,628  
  *A "any-to-any" variant of Gemma-4 31B — accepts and outputs text, images, and more — signaling Google’s multimodal direction.*

- **[google/gemma-4-26B-A4B-it-assistant](https://huggingface.co/google/gemma-4-26B-A4B-it-assistant)**  
  Author: google | Pipeline: any-to-any | Likes: 97 | Downloads: 40,881  
  *The MoE counterpart to the 31B assistant, offering 26B total parameters with 4B active for efficient multimodal inference.*

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**  
  Author: google | Pipeline: image-text-to-text | Likes: 2,579 | Downloads: 8,965,984  
  *The flagship multimodal Gemma-4 model for image-text-to-text tasks, with nearly 9 million downloads and huge community interest.*

- **[google/gemma-4-E4B-it](https://huggingface.co/google/gemma-4-E4B-it)**  
  Author: google | Pipeline: any-to-any | Likes: 961 | Downloads: 5,585,425  
  *An extreme MoE variant (E4B) of Gemma-4, pushing efficiency boundaries with extremely sparse activation.*

- **[google/gemma-4-E4B-it-assistant](https://huggingface.co/google/gemma-4-E4B-it-assistant)**  
  Author: google | Pipeline: any-to-any | Likes: 53 | Downloads: 47,012  
  *The assistant-tuned version of the E4B MoE model, completing Google’s multimodal MoE lineup.*

- **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)**  
  Author: HiDream-ai | Pipeline: image-text-to-image | Likes: 130 | Downloads: 692  
  *A novel "O1-style" image reasoning model that takes both text and image as input and produces images, inspired by chain-of-thought for vision.*

- **[TenStrip/LTX2.3-10Eros](https://huggingface.co/TenStrip/LTX2.3-10Eros)**  
  Author: TenStrip | Pipeline: image-to-video | Likes: 193 | Downloads: 58,647  
  *An image-to-video diffusion model, trending as video generation from static images becomes more accessible.*

- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)**  
  Author: sensenova | Pipeline: any-to-any | Likes: 208 | Downloads: 3,666  
  *An 8B multimodal "Mixture-of-Thoughts" model from SenseTime, supporting any input/output modality.*

- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)**  
  Author: nvidia | Pipeline: any-to-any | Likes: 267 | Downloads: 126,335  
  *Nvidia’s latest MoE reasoning model (30B total, 3B active) optimized for multimodal tasks, highlighting enterprise-grade sparse models.*

- **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)**  
  Author: k2-fsa | Pipeline: text-to-speech | Likes: 826 | Downloads: 2,212,436  
  *A zero-shot multilingual voice cloning model with over 2.2M downloads, demonstrating strong demand for open-source TTS.*

- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)**  
  Author: Qwen | Pipeline: image-text-to-text | Likes: 1,209 | Downloads: 2,273,063  
  *Qwen’s 27B dense multimodal model, trailblazing the Qwen3.6 family with high-quality image understanding and generation.*

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  Author: Qwen | Pipeline: image-text-to-text | Likes: 1,694 | Downloads: 3,668,376  
  *The MoE variant of Qwen3.6 with 35B total/3B active parameters, the most downloaded model this week — a perfect blend of quality and efficiency.*

### 🔧 Specialized Models (code, math, medical, embeddings, audio, privacy)

- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)**  
  Author: openai | Pipeline: token-classification | Likes: 1,384 | Downloads: 185,884  
  *OpenAI’s token-classification model for detecting and filtering private/PII content, trending due to rising privacy awareness.*

- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)**  
  Author: AngelSlim | Pipeline: translation | Likes: 156 | Downloads: 17,223  
  *An aggressively quantized (1.25-bit) translation model based on Hy-MT, pushing the boundaries of extreme compression.*

- **[circlestone-labs/Anima](https://huggingface.co/circlestone-labs/Anima)**  
  Author: circlestone-labs | Pipeline: N/A | Likes: 1,224 | Downloads: 458,911  
  *A diffusion single-file model for ComfyUI, trending among the creative community for its ease of use and artistic output.*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)**  
  Author: unsloth | Likes: 633 | Downloads: 1,412,778  
  *Unsloth’s GGUF quantized version of Qwen3.6-27B, making the multimodal model accessible on consumer hardware.*

- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)**  
  Author: unsloth | Likes: 977 | Downloads: 2,657,295  
  *The GGUF variant of the MoE Qwen3.6, enabling massive model deployment with tiny memory footprint.*

- **[Jackrong/Qwopus3.6-35B-A3B-v1-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-v1-GGUF)**  
  Author: Jackrong | Likes: 95 | Downloads: 53,096  
  *Another community GGUF of Qwen3.6 MoE, with Unsloth optimization, showing the high demand for quantized MoE.*

- **[DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Heretic-Uncensored-FINETUNE-NEO-CODE-Di-IMatrix-MAX-GGUF)**  
  Author: DavidAU | Likes: 116 | Downloads: 181,147  
  *An uncensored, code-focused fine-tune of Qwen3.6 27B with extreme GGUF quantization, popular for creative and unrestricted use.*

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  Author: HauhauCS | Likes: 597 | Downloads: 1,090,203  
  *An uncensored MoE fine-tune of Qwen3.6 with an "aggressive" tone, showing strong community demand for unfiltered multimodal models.*

---

## 3. Ecosystem Signal

This week’s trends paint a clear picture of an ecosystem that has embraced **Mixture-of-Experts (MoE)** as the dominant architecture for balancing quality and efficiency. The Qwen3.6 35B-A3B model and its GGUF variants alone account for over 6.3M downloads, while Google’s Gemma-4 family adds multiple MoE variants (26B-A4B, E4B). **Multimodality** is no longer optional — nearly all leading models now support image-text-to-text or any-to-any pipelines. **Video generation** is gaining serious traction with dedicated base models (Sulphur-2, LTX2.3) that support Diffusers and GGUF quantization.

On the **open-weight vs. proprietary** front, the top models are almost entirely open-weight (Gemma-4, Qwen3.6, DeepSeek-V4, Mistral), indicating a strong community preference for transparency and modifiability. Proprietary players like OpenAI are only present with a niche privacy filter, not a general-purpose model.

**Quantization and fine-tuning** activity is explosive: every major model spawns multiple GGUF variants (Unsloth, Jackrong, DavidAU) within days of release. Uncensored fine-tunes (HauhauCS, DavidAU) remain highly popular, reflecting a persistent desire for unrestricted capabilities. Additionally, **speculative decoding** techniques (DFlash from z-lab) are emerging as a new frontier for inference efficiency, suggesting the community is moving beyond simple quantization to more sophisticated acceleration methods.

---

## 4. Worth Exploring

1. **[HiDream-ai/HiDream-O1-Image](https://huggingface.co/HiDream-ai/HiDream-O1-Image)** — This model is small (692 downloads) but conceptually novel: it brings chain-of-thought reasoning to image generation by accepting both text and image inputs. It’s a glimpse into the next generation of "thinking" vision models.

2. **[k2-fsa/OmniVoice](https://huggingface.co/k2-fsa/OmniVoice)** — With over 2.2M downloads and strong zero-shot multilingual voice cloning capabilities, this is the go-to open-source TTS model. Its quality and versatility make it a must-try for any audio or speech project.

3. **[z-lab/gemma-4-31B-it-DFlash](https://huggingface.co/z-lab/gemma-4-31B-it-DFlash)** — While still experimental, this DFlash speculative decoding variant of Gemma-4 31B represents a promising approach to reducing inference latency without sacrificing output quality. It’s worth studying for anyone optimizing large model deployment.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*