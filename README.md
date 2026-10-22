# Awesome-LLM-Serving-Inference

## Top LLM Serving & Inference Ecosystem



**Curated List of SaaS Products & Open-Source GitHub Projects**  

*Focused on High-Throughput Inference, Managed Endpoints & Self-Hosted Serving Engines*  

**Last updated: October 2026**



This repository tracks notable **SaaS platforms** and **open-source projects** for **LLM Serving & Inference**. These tools enable teams to deploy language models behind APIs—ranging from managed endpoints that abstract away GPU operations to open-source serving engines that maximize throughput on your own hardware.



**Examples** include Together AI, Fireworks AI, Groq, DeepInfra, Baseten, Modal, and vLLM (the category leaders).



**Open-source emphasis**: This section is heavily expanded with every major active serving engine for self-hosting, avoiding per-token vendor lock-in, and controlling your inference stack—ideal for teams that need data sovereignty, predictable costs, or maximum throughput. The open-source landscape is anchored by **vLLM** (the PagedAttention standard with the broadest model coverage), **SGLang** (the structured generation and prefix-caching specialist), and **TensorRT-LLM** (NVIDIA's peak-performance engine), with **llama.cpp** and **Ollama** serving local and edge deployments.



Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.



## Table of Contents

- [SaaS/Hosted Platforms](#saas-hosted-platforms)

- [Open-Source GitHub Projects](#open-source-github-projects)

- [How to Contribute](#how-to-contribute)

- [Disclaimer](#disclaimer)



## SaaS/Hosted Platforms

| Platform | Valuation / Company Size | Pricing | Free Tier Limits | Key Highlights & Best For |
| :--- | :--- | :--- | :--- | :--- |
| **[Fireworks AI](https://fireworks.ai/)** | $17.5B valuation ($1B+ ARR) | Serverless starting at $0.14/M input, $0.28/M output (DeepSeek V4 Flash); $0.15/$0.60 (GPT-OSS 120B); Dedicated H100 at $7.00/hr, B200 at $10.00/hr | $1 one-time starter credit (~1M tokens on 70B models); 10 RPM rate limit without payment method (6,000 RPM with payment method) | Per-token serverless with fast inference, fine-tuning workflows, prompt caching (50% off), and batch discounts. |
| **[Modal](https://modal.com/)** | $15.75B valuation ($1B+ ARR) | Serverless starting at $0.000694/sec (~$2.50/hr) for A100 80GB, $0.001097/sec (~$3.95/hr) for H100 SXM5; 1 TiB/mo egress included | $30/month ongoing compute credits on Starter plan (up to 3 seats, max 10 concurrent GPUs, 100 containers) | Serverless containerized GPU platform with per-second billing, GPU-memory snapshotting, and scale-to-zero. |
| **[Baseten](https://www.baseten.co/)** | $13.0B valuation (~$600M ARR) | Model APIs starting at $0.10/M input, $0.30/M output; Dedicated instances starting at $0.32/hr (T4) with scale-to-zero | $30 one-time starter credits upon signup; no recurring free tier | Serving engine optimized for agentic workloads with automatic cache token discounts and scale-to-zero model deployment. |
| **[Together AI](https://www.together.ai/)** | $8.3B valuation ($1.15B+ ARR/bookings) | Serverless starting at $0.10/M input tokens; Dedicated GPU instances from $5.49/hr (H100) and $8.99/hr (B200) | Strictly prepaid (no ongoing free tier; min deposit $5); up to $50,000 credits via application-only startup program | Serverless and dedicated endpoints for open-weight models with prompt caching and batch discounts (50% off). |
| **[Groq](https://groq.com/)** | $3.5B valuation (~$500M target revenue) | On-demand Developer API starting at $0.075/M input, $0.30/M output (GPT-OSS 20B); $0.15/$0.60 (GPT-OSS 120B) | Free tier included with rate limits: ~30 RPM, 6,000–30,000 TPM, and 100K–500K daily tokens depending on model | LPU-based ultra-low latency inference engine delivering industry-leading generation speeds (~500 tok/s). |
| **[Anyscale](https://www.anyscale.com/)** | $1.65B valuation (acquired by Nscale) | Managed Ray compute starting at $0.5682/hr (T4), $1.3635/hr (A10G), $4.9591/hr (A100) | $100 one-time starter credits to evaluate compute and endpoints; no ongoing free tier | Managed distributed computing platform built on Ray for unified model serving, data processing, and fine-tuning. |
| **[Replicate](https://replicate.com/)** | $350M valuation (acquired by Cloudflare) | Per-second compute starting at $0.000100/sec (~$0.36/hr CPU) and $0.000225/sec (~$0.81/hr Nvidia T4 GPU) | Web playground allows limited free trial predictions on select models; API requires prepaid balance; unpaid tier rate-limited to 1 req/sec (6 RPM) | Vast open-source model catalog with pay-per-second API execution for experimentation and rapid prototyping. |
| **[DeepInfra](https://deepinfra.com/)** | $107M funding ($105M ARR) | Pay-as-you-go starting at $0.02/M input, $0.05/M output (Llama 3.1 8B); $0.09/$0.10 (Qwen3-235B); $1.30/$2.60 (DeepSeek V4 Pro) | No ongoing free tier or default credits (min deposit $10); up to 50B free tokens via DeepStart startup program | Price-performance leader on popular open-source models with prompt caching ($0.10/M cached input) and SOC 2 compliance. |

> [!NOTE]
> **OctoAI Discontinued**: Acquired by NVIDIA and all hosted services were terminated on October 31, 2024. Technology migrated to NVIDIA NIM.

## Open-Source GitHub Projects



- **[vLLM](https://github.com/vllm-project/vllm)**  

  **The PagedAttention standard.** 2,000+ contributors. **Key capabilities**: PagedAttention for KV-cache efficiency, continuous batching, chunked prefill, prefix caching, structured outputs via xgrammar/guidance, and tensor/pipeline/expert parallelism . **Model coverage**: 200+ architectures including decoder-only, MoE, hybrid attention, and multimodal. **Hardware**: NVIDIA, AMD (ROCm growing), Intel, TPU, Gaudi. **OpenAI-compatible API** plus Anthropic Messages API and gRPC . **Limitation**: no compilation step means slightly lower peak throughput than TensorRT-LLM on NVIDIA hardware . Best for general-purpose production serving where model breadth and ease of use matter most.



- **[SGLang](https://github.com/sgl-project/sglang)**  

  **The structured generation and prefix-caching specialist.** **RadixAttention** reuses shared prefixes across requests; **compressed FSMs** enable fast structured output (JSON schemas, grammars) . **Performance**: up to ~29% higher throughput in prefix-heavy tests; Day-0 support for new MoE releases (Qwen3.6, Kimi K2.6, MiniMax M2.5) . **Best for**: chatbots with fixed system prompts, agent loops repeating tool schemas, and any workload where >30–40% of prompt content is reused across calls . **Trade-off**: smaller ecosystem than vLLM. Best for structured output and agentic workloads with high prefix reuse.



- **[TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM)**  

  **NVIDIA's peak-performance engine.** Custom kernels, prefill-decode disaggregation, FP4/FP8 support on Blackwell/Hopper, and integration with Triton and Dynamo . **Lowest measured first-token latency**: 235ms vs vLLM's 514ms in one test . **Trade-offs**: NVIDIA-only, complex build process, per-GPU-generation compilation required . Best for latency-critical production on NVIDIA hardware where you have engineering capacity to manage the toolchain.



- **[llama.cpp](https://github.com/ggml-org/llama.cpp)**  

  **The edge and CPU standard.** C/C++ engine with first-class Apple Silicon support, plus CUDA, ROCm, Vulkan, and SYCL backends. 1.5-bit to 8-bit quantization. OpenAI-compatible server (`llama serve`) . Best for CPU-only boxes, mixed CPU/GPU offload, edge devices, and local development.



- **[Ollama](https://github.com/ollama/ollama)**  

  **The simplest local deployment.** Wraps llama.cpp with a one-line install and model library. OpenAI-compatible API at `localhost:11434/v1/`. **Limitations**: less optimized for high-concurrency production serving than vLLM or SGLang . Best for local development, prototyping, and single-user deployments.



### Additional Strong Open-Source Options



- **LMDeploy** — InternVL's serving toolkit with TurboMind engine. Best for multimodal model serving.

- **OpenLLM (BentoML)** — Production serving with observability and adaptive batching. Best for teams already using BentoML.

- **Frameworks for building custom systems**: Use **vLLM** as the default serving backbone. Switch to **SGLang** when prefix reuse exceeds 30–40% or structured output is critical . Use **TensorRT-LLM** when lowest first-token latency justifies the toolchain complexity. Use **llama.cpp** or **Ollama** for local and edge. On Modal, deploy **vLLM** or **SGLang** as your engine with per-second billing .



## How to Contribute



1. Fork the repo.

2. Add/edit entries in `README.md` (follow existing format).

3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.

4. Submit PR with a short explanation.



Star the repo if you find it useful!



## Disclaimer



- This is a **community-curated** list — not exhaustive and not an endorsement.

- **Managed vs. self-hosted economics flip at utilization**: Modal's H100 at ~$3.95/hr costs ~$2,845/month if pinned 24/7, versus serverless per-token pricing that scales with actual usage . Model your traffic shape before committing.

- **"Cheapest per token" depends on the model**: DeepInfra leads on most open models, but prices vary 1.2x–4x across providers for the same model . Always compare the specific model you need.

- **OctoAI is discontinued**: NVIDIA acquired it, terminated hosted services October 2024, and migrated technology to NIM . Do not evaluate for new projects.

- **Engine choice depends on your traffic**: vLLM for breadth and ease; SGLang for prefix reuse and structured output; TensorRT-LLM for peak NVIDIA performance with engineering investment . Benchmark against your own prompt patterns, not generic numbers.



---



**Made for ML engineers, platform teams, and developers deploying LLM inference infrastructure.**  

Let's make LLM serving more open, throughput-efficient, and appropriately scoped.
