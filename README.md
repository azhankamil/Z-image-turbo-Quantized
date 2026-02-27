# Z-Image-Turbo on GTX 1050 Ti (4GB) – ComfyUI Workflow

This repo shows something simple:

> A 2016 GPU can still generate AI images in 2026.


<img width="1440" height="779" alt="Screenshot 2026-02-27 at 6 45 13 AM" src="https://github.com/user-attachments/assets/697886af-881c-4a2d-8e8d-6b8eb38bd8b7" />

No RTX.  
No 12GB VRAM.  
No fancy AI marketing.  

**Just optimization.**

---

## 🖥️ Hardware Used

- **GPU:** GTX 1050 Ti (4GB, Pascal – 2016)
- **CPU:** i5-9400F
- **RAM:** 16GB
- **UI:** ComfyUI
- **Model:** Z-Image-Turbo (FP8)

---

## 🚀 What’s Happening Here?

Modern diffusion models expect big GPUs.

This setup doesn’t have one.

Instead, it works because of:

- **FP8 quantization** → smaller model memory footprint  
- **VRAM ↔ RAM offloading** → avoids CUDA OOM crashes  
- **512×512 sweet spot** → manageable activation memory  
- **Lean workflow** → no unnecessary nodes  

### Result

- ~2.4GB loaded on GPU  
- Remaining weights offloaded to RAM  
- Stable image generation on 4GB VRAM  

---

## 🎯 Recommended Settings

| Setting        | Value                         |
|---------------|--------------------------------|
| Resolution     | 512×512                        |
| Steps          | 6–8                            |
| Precision      | FP8                            |
| Launch Flags   | `--lowvram --fp8_e4m3fn`        |
| Offloading     | Enabled                        |

> If it crashes:
> - Lower resolution first  
> - Then reduce steps  

---

## 📦 Required Models

### 1️⃣ Z-Image-Turbo (FP8)

Place inside:
Queue prompt.
That’s it.
