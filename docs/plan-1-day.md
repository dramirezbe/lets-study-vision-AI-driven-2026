# General Plan — "From Pixels to Low-Level Optimization: Computer Vision Driven by LLMs"

## One-Day Route Overview (7.5 effective hours)

- **09:00–09:45 (0.75 h):** Module 1 — Mathematical foundations and image representation
- **09:45–11:00 (1.25 h):** Module 2 — Convolution, classical filtering, and edge detection
- **11:00–12:15 (1.25 h):** Module 3 — Features, segmentation, and robust classical pipelines
- **12:15–13:15 (1.0 h):** Module 4 — Deep learning for vision (CNNs) + minimal training
- **13:15–14:15:** Lunch
- **14:15–15:30 (1.25 h):** Module 5 — VLMs and production-oriented multimodal prompting
- **15:30–17:00 (1.5 h):** Module 6 — Low-level optimization (ONNX, PTQ/QAT, distillation) and deployment
- **17:00–17:30 (0.5 h):** Closing — Technical postmortem, real failures, and production checklist

## Module Summary

### Module 1 — Operational mathematics of the digital image
- **Key Mathematical Concepts**
  - Image as a tensor: $I \in \mathbb{R}^{H\times W\times C}$
  - Normalization: $$I' = \frac{I - \mu}{\sigma}$$
  - Reconstruction error: $$\text{MSE} = \frac{1}{HWC}\sum_{h,w,c}(I_{h,w,c}-\hat{I}_{h,w,c})^2$$
- **Interactive Component / Simulator to Build**
  - Streamlit app with brightness, contrast, gamma, and Gaussian noise sliders; original vs. transformed view and error heatmap.
- **Prompting Pattern to Master**
  - Structured prompt with contracts: shapes (`H,W,C`), types (`uint8` input, `float32` processing), per-frame latency limit.
- **Express Practical Project (Webcam/Dataset)**
  - "Image quality inspector" over webcam to measure exposure and noise in real time.
- **Optimization / Performance Metric Evaluated**
  - ms/frame on CPU, luminance histogram, MSE/SSIM between raw and corrected frame.

### Module 2 — Convolution and classical filtering
- **Key Mathematical Concepts**
  - Discrete 2D convolution: $$Y(i,j)=\sum_{m=-k}^{k}\sum_{n=-k}^{k}K(m,n)\,I(i-m,j-n)$$
  - Sobel gradient: $$G=\sqrt{G_x^2+G_y^2}$$
- **Interactive Component / Simulator to Build**
  - Widget with sliders for kernel size, sigma, Canny threshold, and a padding selector.
- **Prompting Pattern to Master**
  - "Prompt-to-code" prompt to generate an OpenCV pipeline with shape tests and safe clipping.
- **Express Practical Project (Webcam/Dataset)**
  - Edge detector robust to lighting for documents captured by webcam.
- **Optimization / Performance Metric Evaluated**
  - FPS, false-edge rate due to noise, and temporary memory cost per intermediate buffer.

### Module 3 — Segmentation and classical vision under real conditions
- **Key Mathematical Concepts**
  - Adaptive thresholding and morphology: $$I_{bin}(x,y)=\mathbb{1}[I(x,y)>T(x,y)]$$
  - Opening/closing operations for mask cleanup.
- **Interactive Component / Simulator to Build**
  - App with sliders for adaptive block size, C, morphological iterations, and structuring-element size.
- **Prompting Pattern to Master**
  - Prompt with robustness constraints (color-temperature changes, shadows, and JPEG compression).
- **Express Practical Project (Webcam/Dataset)**
  - Main-object segmenter on a table with variable background using a webcam.
- **Optimization / Performance Metric Evaluated**
  - Mask IoU, p95 latency, and sensor-noise sensitivity.

### Module 4 — CNNs and minimal inference-oriented training
- **Key Mathematical Concepts**
  - Convolutional layer and activation: $$A^{(l)}=\phi(W^{(l)}*A^{(l-1)}+b^{(l)})$$
  - Cross-Entropy: $$L_{CE}=-\sum_i y_i\log(\hat{y}_i)$$
  - Update: $$\theta_{t+1}=\theta_t-\eta\nabla_\theta L$$
- **Interactive Component / Simulator to Build**
  - Dashboard with sliders for learning rate, batch size, and augmentations; live loss/accuracy curves.
- **Prompting Pattern to Master**
  - Prompt to generate a complete PyTorch script with NCHW dimension asserts and `float32` control.
- **Express Practical Project (Webcam/Dataset)**
  - Fast binary classifier (e.g., object present/absent) with a lightweight dataset.
- **Optimization / Performance Metric Evaluated**
  - Accuracy, per-image inference latency, and RAM/VRAM during minimal training.

### Module 5 — VLMs and multimodal prompting in production
- **Key Mathematical Concepts**
  - Text-image embedding similarity: $$s = \frac{v\cdot t}{\|v\|\|t\|}$$
  - Attention (conceptual): $$\text{Attn}(Q,K,V)=\text{softmax}(QK^T/\sqrt{d_k})V$$
- **Interactive Component / Simulator to Build**
  - Interface to compare multimodal prompts, top-k results, and confidence maps.
- **Prompting Pattern to Master**
  - Master prompt with strict JSON format, rejection criteria, and latency/cost limits.
- **Express Practical Project (Webcam/Dataset)**
  - "Visual assistant": scene description + semantic classification from webcam.
- **Optimization / Performance Metric Evaluated**
  - Semantic top-1/top-5, tokens per inference, and end-to-end latency.

### Module 6 — Low-level optimization and deployment
- **Key Mathematical Concepts**
  - Affine INT8 quantization: $$q = \text{round}(x/s)+z,\quad x \approx s(q-z)$$
  - Distillation: $$L_{distill}=\alpha L_{CE} + (1-\alpha)T^2L_{KL}$$
- **Interactive Component / Simulator to Build**
  - Simulator with sliders for bits (FP32/FP16/INT8), batch size, and backend (CPU/ORT) to compare precision/latency.
- **Prompting Pattern to Master**
  - Prompt to export PyTorch→ONNX, run ONNX Runtime, and log reproducible metrics.
- **Express Practical Project (Webcam/Dataset)**
  - Export the trained model to ONNX + PTQ INT8 and compare against the FP32 baseline on webcam.
- **Optimization / Performance Metric Evaluated**
  - Latency (ms/frame), FPS, model size (MB), memory consumption, and accuracy drop.

## Transversal Production Critical Analysis (applies to every module)
- Evaluate failures caused by **sensor noise**, **lighting variation**, **motion blur**, and **JPEG compression**.
- Report real trade-offs: **Precision (mAP/IoU/SSIM) vs. Latency (FPS/ms) vs. Size (MB)**.
- Include bottleneck measurements: memory bandwidth, CPU saturation, and pre/post-processing cost.
