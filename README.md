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



- **[Together AI](https://www.together.ai/)**  

  Serverless and dedicated endpoints for open-weight models. **Serverless pricing** starts around $0.10/M tokens for smaller models, with batch inference and prompt caching at 50% discounts . **Dedicated GPU rates**: H100 $5.49/hr, B200 $8.99/hr, billed per ready replica per minute (provisioning not billed) . Best for teams that want to start serverless and graduate to reserved capacity.



- **[Fireworks AI](https://fireworks.ai/)**  

  Per-token serverless with transparent rate limits and fine-tuning. **Published rates**: Kimi K2.6 $0.95/$4.00, DeepSeek V4 Flash $0.14/$0.28, GPT-OSS 120B $0.15/$0.60. Cached input gets 50% off; batch runs at 50% of serverless . **Rate limits**: 10 RPM without a payment method, 6,000 RPM with a card. **Dedicated GPUs**: H100 $7.00/hr, B200 $10.00/hr . Best for teams needing predictable ceilings and fine-tuning workflows.



- **[Groq](https://groq.com/)**  

  **The throughput specialist.** LPU-based inference delivering exceptionally high tokens-per-second (e.g., GPT-OSS 120B at ~500 tok/s) . Fixed model catalog with per-token pricing. Best for latency-sensitive applications where raw generation speed matters more than model breadth.



- **[DeepInfra](https://deepinfra.com/)**  

  **The per-token price leader on open models.** DeepSeek V4 Pro at $1.30/$2.60, Qwen3-235B at $0.09/$0.10, Llama 3.1 8B at $0.02/$0.05 . Cached input for DeepSeek V4 Pro drops to $0.10/M (vs $1.30 uncached). SOC 2 and ISO 27001 certified, zero retention on inference. Best for cost-sensitive production workloads with predictable token volumes.



- **[Baseten](https://www.baseten.co/)**  

  Model serving with **cache token pricing**—cached input tokens billed at a discount automatically, benefiting agentic workloads with reused system prompts. Competitive per-token rates (e.g., Kimi K2.6 $0.95/$4.00) . Best for teams serving agent workloads where prompt caching yields meaningful savings.



- **[Modal](https://modal.com/)**  

  **Serverless GPU platform with per-second billing.** H100 SXM5 at $0.001097/sec (~$3.95/hr); A100 80GB at $0.000694/sec (~$2.50/hr) . **GPU-memory snapshotting** reduced cold start for one model from ~118s to ~12s . **Scale-to-zero** makes it economical for spiky traffic—a 75-GPU peak with 50-GPU average costs less than a fixed fleet despite the higher per-hour rate . **Note**: network egress is billed starting October 2026 (1 TiB/month included on Starter). Best for bursty workloads and teams that want to deploy their own engine (vLLM, SGLang) on serverless GPUs.



- **[Anyscale](https://www.anyscale.com/)**  

  Managed Ray platform with pay-as-you-go compute. **Instance rates**: T4 $0.5682/hr, A10G $1.3635/hr, A100 $4.9591/hr; H/B/GB families quote-based . Best for teams already using Ray for distributed workloads that want a unified serving layer.



- **[Replicate](https://replicate.com/)**  

  Pay-per-second model hosting with a vast catalog. Cold starts of 5–30s are common, with costs accumulating per second . Best for experimentation and running community models without infrastructure management.



- **Note on OctoAI**: **Discontinued.** NVIDIA acquired OctoAI in 2024, terminated all hosted services on October 31, 2024, and the technology was absorbed into NVIDIA NIM . Do not select for new deployments.



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
