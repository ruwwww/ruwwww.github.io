---
layout: page
title: Diffusion LoRAs
description: Collection of custom-trained character, style, and concept LoRA models for Anima DiT, Illustrious SDXL, and modern diffusion pipelines
img: assets/img/art/demon_green_flame.png
importance: 3
category: Machine Learning & Generative Models
github: https://github.com/ruwwww/anima-fastpath-recipe
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0 d-flex gap-2 align-items-center">
        <a href="https://huggingface.co/ruwwww/diffusion_loras" target="_blank" rel="noopener" class="btn btn-primary btn-sm">
            <i class="fa-solid fa-cube mr-1"></i> Hugging Face Model Repository
        </a>
        <a href="https://github.com/ruwwww/anima-fastpath-recipe" target="_blank" rel="noopener" class="btn btn-outline-secondary btn-sm">
            <i class="fa-brands fa-github mr-1"></i> Training Recipe & Code
        </a>
        <a href="{{ '/gallery/' | relative_url }}" class="btn btn-outline-info btn-sm">
            <i class="fa-solid fa-images mr-1"></i> View Visual Gallery
        </a>
    </div>
</div>

<hr>

### Overview

This repository hosts a curated collection of **Low-Rank Adaptation (LoRA)** weights, fine-tuned checkpoints, and training datasets targeting state-of-the-art diffusion architectures, including **Anima DiT** and **Illustrious SDXL**.

All models are trained with high-efficiency pipelines using direct FP8 backward passes, persistent latent caching in system RAM, Prodigy adaptive optimization, and precision Danbooru/PixAI tagging.

### Key Highlights & Features

- **Architectures Supported:** Native DiT (Diffusion Transformer) modules and SDXL cross-attention/residual projections.
- **Fastpath Training Pipeline:** Prodigy adaptive optimizer (`d_coef=1.0`), single-block checkpointing, and Triton FP8 matrix kernels maximizing effective TFLOP/s on modern NVIDIA GPUs.
- **Curated Dataset Engineering:** Tagged via unified multi-stage vision models (PixAI v1.0 + WD14) with strict character trait isolation and minimal trigger leakage.
- **Production-Ready Artifacts:** Safetensors format compatible with ComfyUI, WebUI, and diffusers.

### Model Hub & Visual Outputs

You can download weights directly from the [Hugging Face Repository](https://huggingface.co/ruwwww/diffusion_loras), or inspect full-resolution outputs and character studies generated with these checkpoints in the [Portfolio Visual Gallery]({{ '/gallery/' | relative_url }}).
