# Hugging Face Trending Models Digest 2026-05-03

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-05-03 03:50 UTC

---

Here is the structured Hugging Face Trending Models Digest based on the provided data.

---

## Hugging Face Trending Models Digest (2026-05-03)

### 1. Today's Highlights

This week’s trending models signal a decisive shift toward MoE (Mixture-of-Experts) architectures, with **Qwen’s Qwen3.6-35B-A3B** leading the charge in both community engagement and download volume. **DeepSeek-V4-Pro** remains the dominant pure language model, while **Google’s Gemma-4-31B-it** posts staggering download numbers (7.7M+), underscoring its broad appeal as a powerful open-weight vision-language model. Notably, a strong "uncensored" sub-trend has emerged, with finetunes based on both Gemma-4 and Qwen3.6 attracting significant attention, reflecting a community push toward less-restrictive model behavior. Finally, **OpenAI’s privacy-filter** stands out as a unique entry, signaling growing interest in on-device safety and data protection tools.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* | Likes: 3,420 | Downloads: 381,587  
  The top trending model of the week; a powerful conversational LLM leading the new DeepSeek-V4 generation.
- **[XiaomiMiMo/MiMo-V2.5-Pro](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro)** — *XiaomiMiMo* | Likes: 382 | Downloads: 9,914  
  Xiaomi's latest agent-focused long-context LLM, gaining traction as a capable "Pro" variant.
- **[ibm-granite/granite-4.1-8b](https://huggingface.co/ibm-granite/granite-4.1-8b)** — *ibm-granite* | Likes: 133 | Downloads: 16,079  
  IBM’s efficient 8B enterprise language model, part of the growing Granite 4.1 family.
- **[ibm-granite/granite-4.1-30b](https://huggingface.co/ibm-granite/granite-4.1-30b)** — *ibm-granite* | Likes: 79 | Downloads: 3,072  
  The larger 30B sibling in the Granite 4.1 lineup, targeting more demanding enterprise text-generation tasks.
- **[talkie-lm/talkie-1930-13b-it](https://huggingface.co/talkie-lm/talkie-1930-13b-it)** — *talkie-lm* | Likes: 204 | Downloads: 0  
  An instruction-tuned 13B conversational model; notable for zero downloads despite high likes, suggesting a very recent release.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — *google* | Likes: 2,481 | Downloads: 7,776,034  
  Google's flagship open-weight vision-language model; the highest download count on the list, indicating massive real-world deployment.
- **[Qwen/Qwen3.6-27B](https://huggingface.co/Qwen/Qwen3.6-27B)** — *Qwen* | Likes: 1,081 | Downloads: 1,070,778  
  A popular 27B vision-language model from the Qwen3.6 series, widely used for conversational image-text tasks.
- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — *Qwen* | Likes: 1,574 | Downloads: 2,397,446  
  The standout MoE model of the week; 35B total parameters with 3B active, offering strong performance at lower inference cost.
- **[moonshotai/Kimi-K2.6](https://huggingface.co/moonshotai/Kimi-K2.6)** — *moonshotai* | Likes: 1,183 | Downloads: 699,348  
  A compressed, feature-extraction-focused vision-language model from Moonshot AI, likely optimized for efficiency.
- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-BF16)** — *nvidia* | Likes: 199 | Downloads: 37,418  
  Nvidia's "any-to-any" reasoning model (30B, 3B active), enabling cross-modal input and output.
- **[nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4](https://huggingface.co/nvidia/Nemotron-3-Nano-Omni-30B-A3B-Reasoning-NVFP4)** — *nvidia* | Likes: 71 | Downloads: 180,012  
  A 4-bit NVFP4 quantized version of the same Nemotron-3 Omni model, making it deployable on smaller hardware.
- **[XiaomiMiMo/MiMo-V2.5](https://huggingface.co/XiaomiMiMo/MiMo-V2.5)** — *XiaomiMiMo* | Likes: 192 | Downloads: 28,323  
  Xiaomi’s multimodal base model supporting both vision and audio inputs.
- **[sensenova/SenseNova-U1-8B-MoT](https://huggingface.co/sensenova/SenseNova-U1-8B-MoT)** — *sensenova* | Likes: 120 | Downloads: 1,308  
  An 8B "Mixture of Tasks" multimodal model, designed for any-to-any generation across modalities.

#### 🔧 Specialized Models (code, math, medical, embeddings)
- **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — *openai* | Likes: 1,212 | Downloads: 99,399  
  OpenAI’s unique token-classification model for detecting and filtering private data; trending due to growing privacy and compliance needs.
- **[ibm-granite/granite-embedding-97m-multilingual-r2](https://huggingface.co/ibm-granite/granite-embedding-97m-multilingual-r2)** — *ibm-granite* | Likes: 68 | Downloads: 1,598  
  A compact multilingual embedding model (97M) supporting multiple export formats (ONNX, OpenVINO) for retrieval tasks.
- **[AngelSlim/Hy-MT1.5-1.8B-1.25bit](https://huggingface.co/AngelSlim/Hy-MT1.5-1.8B-1.25bit)** — *AngelSlim* | Likes: 78 | Downloads: 487  
  An aggressively quantized (1.25-bit) 1.8B translation model, pushing the boundary of extreme compression.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)
- **[unsloth/Qwen3.6-27B-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-GGUF)** — *unsloth* | Likes: 545 | Downloads: 983,535  
  Unsloth’s GGUF quantization of the Qwen3.6-27B vision model, enabling local inference on consumer GPUs.
- **[unsloth/Qwen3.6-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen3.6-35B-A3B-GGUF)** — *unsloth* | Likes: 895 | Downloads: 2,001,316  
  The most downloaded GGUF model this week; makes the powerful MoE variant accessible on CPU/edge hardware.
- **[unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF](https://huggingface.co/unsloth/NVIDIA-Nemotron-3-Nano-Omni-30B-A3B-Reasoning-GGUF)** — *unsloth* | Likes: 92 | Downloads: 37,663  
  A GGUF version of Nvidia's Omni reasoning model for local multimodal inference.
- **[HauhauCS/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-27B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | Likes: 264 | Downloads: 303,358  
  An "uncensored" and "aggressive" finetune of Qwen3.6-27B, reflecting strong community demand for less-filtered models.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* | Likes: 530 | Downloads: 766,075  
  The MoE version of the same uncensored finetune; highly popular for its combination of efficiency and reduced alignment.
- **[dealignai/Gemma-4-31B-JANG_4M-CRACK](https://huggingface.co/dealignai/Gemma-4-31B-JANG_4M-CRACK)** — *dealignai* | Likes: 1,444 | Downloads: 199,500  
  An "abliterated" (uncensored) finetune of Google’s Gemma-4-31B, showing the scale of community modification of large open models.
- **[z-lab/Qwen3.6-27B-DFlash](https://huggingface.co/z-lab/Qwen3.6-27B-DFlash)** — *z-lab* | Likes: 206 | Downloads: 17,016  
  A specialized finetune or adaptation of Qwen3.6-27B, tagged with "dflash" for optimized text generation.

### 3. Ecosystem Signal

The current ecosystem is defined by a **bimodal battle between dense models and MoE architectures**. The Qwen3.6 series perfectly illustrates this: its dense 27B variant is popular, but the MoE 35B-A3B variant has double the downloads and significantly more quick community adoption. **DeepSeek-V4** continues to dominate the pure language model space, while **Gemma-4** has become the de-facto standard for accessible vision-language work, evidenced by its enormous download count and active finetuning community. The **uncensored sub-community is a major force**—models like the "JANG_4M-CRACK" Gemma-4 finetune rival their base models in engagement, suggesting a persistent market for reduced alignment. On the deployment front, **Unsloth’s GGUF ecosystem is the primary vehicle for democratization**, converting nearly every major release into a locally-run format. Notably, **corporate participation is high**: Google, Nvidia, IBM, Xiaomi, Moonshot, and even OpenAI (with a specialized tool) are all actively open-sourcing, indicating a maturing competitive landscape where open-weight release is now the standard.

### 4. Worth Exploring

1. **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** — This model represents the current best balance of performance, efficiency, and community support. Its MoE design (35B total, 3B active) makes it a critical model to study for anyone interested in serving high-quality vision-language models at scale without prohibitive hardware costs.

2. **[openai/privacy-filter](https://huggingface.co/openai/privacy-filter)** — As one of the few non-generative models from OpenAI on the hub, this token-classification tool is worth examining for its approach to responsible AI deployment. It signals a shift from purely capability-focused releases toward tooling that addresses real deployment risks like data leakage.

3. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — With 7.7 million downloads, this is the most used open-weight vision-language model on the platform. It is essential for anyone studying open-weight model adoption, enterprise deployment, or the impact of permissive licensing (Gemma license) on community growth.

---
*This digest is auto-generated by [agents-radar](https://github.com/lib182071-prog/agents-radar).*