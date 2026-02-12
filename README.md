**Dermatology Clinical LoRA – Stable Diffusion Inference Pipeline**
**Overview**

This repository demonstrates the deployment of a custom-trained Dermatology LoRA integrated with Stable Diffusion v1.5 using ComfyUI.

The objective is to generate high-fidelity synthetic dermatological pathology images using a lightweight LoRA adapter while maintaining reproducibility and modular experimentation.

**System Configuration**

Python Version: 3.10.11
PyTorch: 2.3.1 + CUDA 12.1
Framework: ComfyUI
Base Model: Stable Diffusion v1.5 (pruned)
LoRA Adapter: derm_clin_lora.safetensors

**Why ComfyUI Instead of WebUI?**

ComfyUI provides:

Graph-based modular architecture

Explicit diffusion pipeline control

Conditioning transparency

Exportable JSON workflows

Production-grade reproducibility

For research workflows, node-based architecture ensures better traceability than UI slider-based systems.

Pipeline Architecture

**Workflow:**

Load Stable Diffusion v1.5 checkpoint

Inject Dermatology LoRA

Encode Positive & Negative Prompts

Generate Latent via KSampler

Decode using VAE

Save output image

Core Parameters

Resolution: 512 × 512
Sampler: DPM++ 2M Ancestral
Steps: 35
CFG Scale: 11
LoRA Strength: 1.5
Denoise: 1.0

**Engineering Challenges & Solutions**
Python & Dependency Conflicts

Multiple Python installations caused setuptools and CLIP installation failures.

**Solution:**

Standardized environment to Python 3.10.11

Rebuilt isolated virtual environment

Aligned pip and setuptools versions

LoRA Weak Influence

**Initial outputs were unrelated to dermatology.**

**Solution:**

Increased LoRA strength

Tuned CFG scale

Refined prompt specificity

Switched to DPM++ sampler

Unrealistic / Cartoon Outputs

**Base SD bias toward artistic outputs.**

**Solution:**

Aggressive negative prompting

Medical realism tokens

Increased diffusion steps

Reproducibility Concerns

**UI-based experimentation lacked traceability.
**
**Solution:**

Migrated to ComfyUI

Exported workflow.json

Modular graph-based inference

Installation

1️⃣ **Install ComfyUI**

git clone https://github.com/comfyanonymous/ComfyUI.git

cd ComfyUI

2️⃣** Create Virtual Environment**
python -m venv venv

venv\Scripts\activate

pip install -r requirements.txt

3️⃣ Place Models

Checkpoint → ComfyUI/models/checkpoints/

LoRA → ComfyUI/models/loras/

**Running**

python main.py

**Open:**

http://127.0.0.1:8188

Load workflow.json.

**Ethical Disclaimer**

This project generates synthetic dermatological imagery for research purposes only.

No identifiable patient data is used or distributed.

Some outputs may be visually intense due to medical realism.
