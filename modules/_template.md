# Per-Module Development Template

Use this template to develop each module with technical rigor and a prompt-to-code approach. Fill it in inside the module's `notes/` (or as the module README), then build the folders in this order: `theory/` → `notebooks/` → `exercises/` → `reports/`.

## Module Header
- **Module:** `[NUMBER] - [NAME]`
- **Main topics:** `[TOPIC LIST]`
- **Measurable technical goal:** `[target metric: latency/accuracy/memory]`

## 1) Mathematical and Geometric Rigor (No filler)
- LaTeX equations (minimum 3, with defined variables and units):
  - $...$
  - $$...$$
- Direct impact on tensors/matrices:
  - Input shape: `[H, W, C]` or `[N, C, H, W]`
  - Shape transformation: `[...] -> [...]`
  - Estimated memory cost: `bytes = num_elements × type_size`
- Geometric/vectorial intuition focused on system behavior (no repetitive drills).

## 2) Visual and Interactive View (complete runnable code)
- Deliverable: a single file (`.html` with Canvas/WebGPU) or a lightweight app (`streamlit_app.py` / `gradio_app.py`).
- Required controls:
  - Sliders for key parameters (kernel, threshold, learning rate, quantization bits, etc.).
  - Toggles to enable/disable pipeline stages.
- Immediate visual result over the image/matrix/activations.

## 3) Prompt Engineering for Code
### 3.1 Master Prompt (copy/paste into an LLM)
```text
You are a senior computer vision engineer.
Generate runnable, production-ready code for module [NUMBER-NAME].
Strict requirements:
1) Typed input and output with explicit shapes.
2) Tensor validations with asserts.
3) Controlled dtype (float32/int8 depending on the stage).
4) Target latency constraint: [X] ms/frame on CPU.
5) Modular code with pure functions and a run script.
6) Include memory and time measurement per stage.
Deliver: complete files and the run command.
```

### 3.2 Verification criteria for the generated code
- Shape asserts (`NCHW`, `HWC`) and value range.
- dtype verification (`float32` for training, `int8` for quantized inference).
- Basic profiling:
  - Time per frame (ms)
  - Average and p95 FPS
  - RAM/VRAM

## 4) Practical Micro-Project (<= 15 min)
- **Scenario:** laptop webcam or a lightweight public dataset.
- **Step-by-step flow:**
  1. Run the master prompt and generate the code.
  2. Run the script with a base example.
  3. Open the interactive interface and tune parameters.
  4. Record the key metrics.
  5. Save evidence (`captures`, `metrics`, `configuration`).
- **Success criterion:** working output + target metric reached, or a diagnosed bottleneck.

## 5) Low-Level Optimization and Deployment
- Graph export (e.g., PyTorch -> ONNX).
- Main strategy (choose one or both):
  - PTQ INT8 with range calibration.
  - Teacher-student distillation with:
    $$L_{distill}=\alpha L_{CE} + (1-\alpha)T^2L_{KL}$$
- Mandatory comparative measurement:
  - FP32 vs FP16/INT8 on latency, model size, and accuracy.

## 6) Production Critical Analysis
- Document **3 real failures** of the module in an industrial/commercial environment.
  - Examples: aliasing, JPEG artifacts, extreme lighting, CPU bottleneck.
- Justify real trade-offs:
  - Precision (`mAP/IoU/SSIM`) vs Latency (`FPS`) vs Size (`MB`).
- Final deployment decision based on metrics, not intuition.
