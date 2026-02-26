# Z-Image-Turbo on GTX 1050 Ti (4GB) – ComfyUI Workflow

This repository demonstrates running **Z-Image-Turbo (FP8)** on modest consumer hardware using ComfyUI:

- **GPU:** GTX 1050 Ti (4GB VRAM, Pascal, 2016)
- **CPU:** Intel Core i5-9400F
- **RAM:** 16GB
- **Frontend:** ComfyUI

The workflow uses FP8 weight quantization and VRAM/RAM offloading to make image generation viable on GPUs with as little as 4GB of VRAM.

---

## Why This Matters

Most modern diffusion models are designed with high-end GPUs in mind (RTX 3090, A100, etc.). The GTX 1050 Ti represents a large segment of users who cannot afford to upgrade their hardware.

Z-Image-Turbo with FP8 quantization significantly reduces the memory footprint of the model weights. Combined with ComfyUI's built-in CPU offloading, it becomes possible to generate images on 4GB VRAM cards by:

- **FP8 weights** – halving the memory used by model parameters compared to FP16.
- **VRAM offloading** – moving tensors to RAM when VRAM is exhausted, preventing out-of-memory crashes.
- **Reduced resolution** – working at 512×512 keeps activation memory low enough to fit within 4GB.

This makes the setup accessible to users with Pascal-generation (2016–2018) GPUs that are otherwise left behind by newer model releases.

---

## Recommended Settings

| Setting | Value |
|---|---|
| Resolution | 512×512 |
| Steps | 6–8 |
| Model precision | FP8 weights |
| VRAM offloading | Enabled (ComfyUI `--lowvram` or `--cpu-vae`) |
| RAM offloading | Enabled (move layers to CPU when VRAM is full) |

> **Tip:** In ComfyUI, launch with `--lowvram` and `--fp8_e4m3fn` flags to activate low-VRAM mode and FP8 inference automatically.

---

## How to Use

1. **Install ComfyUI** following the [official instructions](https://github.com/comfyanonymous/ComfyUI).
2. **Download the Z-Image-Turbo FP8 checkpoint** and place it in `ComfyUI/models/checkpoints/`.
3. **Import the workflow:**
   - Open ComfyUI in your browser (default: `http://127.0.0.1:8188`).
   - Click the **Load** button (or drag-and-drop `workflow.json` onto the canvas).
   - Select `workflow.json` from this repository.
4. **Verify node connections** – make sure the checkpoint loader points to your downloaded Z-Image-Turbo FP8 model file.
5. **Queue the prompt** and monitor VRAM usage. If you encounter OOM errors, lower the resolution or increase offloading aggressiveness via ComfyUI launch flags.