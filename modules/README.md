# Modules

One folder per module. Every module uses the same layout: `notebooks/`, `reports/`, `notes/`, `theory/`, `exercises/`.

| Folder | Module | Target metric |
| --- | --- | --- |
| `module-01` | Mathematical foundations and image representation | ms/frame on CPU, luminance histogram, MSE/SSIM |
| `module-02` | Convolution, classical filtering, and edge detection | FPS, false-edge rate under noise, temporary buffer memory |
| `module-03` | Features, segmentation, and robust classical pipelines | IoU, p95 latency, sensor-noise sensitivity |
| `module-04` | Deep learning for vision (CNNs) and minimal training | Accuracy, inference latency, RAM/VRAM |
| `module-05` | VLMs and production multimodal prompting | Semantic top-1/top-5, tokens per inference, end-to-end latency |
| `module-06` | Low-level optimization (ONNX, PTQ/QAT, distillation) and deployment | ms/frame, FPS, model size (MB), memory, accuracy drop |

Full scope, timings, and per-module deliverables: `docs/plan-1-day.md`. Authoring template: `modules/_template.md`.
