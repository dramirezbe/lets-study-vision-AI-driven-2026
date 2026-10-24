# Plan General — "De los Píxeles a la Optimización de Bajo Nivel: Visión por Computadora Impulsada por LLMs"

## Visión General de la RUTA DE 1 DÍA (8.5 horas efectivas)

- **09:00–09:45 (0.75 h):** Módulo 1 — Fundamentos matemáticos y representación de imagen
- **09:45–11:00 (1.25 h):** Módulo 2 — Convolución, filtrado clásico y detección de bordes
- **11:00–12:15 (1.25 h):** Módulo 3 — Features, segmentación y pipelines clásicos robustos
- **12:15–13:15 (1.0 h):** Módulo 4 — Deep Learning para visión (CNNs) + entrenamiento mínimo
- **14:15–15:30 (1.25 h):** Módulo 5 — VLMs y prompting multimodal orientado a producción
- **15:30–17:00 (1.5 h):** Módulo 6 — Optimización a bajo nivel (ONNX, PTQ/QAT, distilación) y despliegue
- **17:00–17:30 (0.5 h):** Cierre — Postmortem técnico, fallas reales y checklist de producción

## Resumen Ejecutivo de Módulos

### Módulo 1 — Matemática operacional de la imagen digital
- **Conceptos Matemáticos Clave**
  - Imagen como tensor: $I \in \mathbb{R}^{H\times W\times C}$
  - Normalización: $$I' = \frac{I - \mu}{\sigma}$$
  - Error de reconstrucción: $$\text{MSE} = \frac{1}{HWC}\sum_{h,w,c}(I_{h,w,c}-\hat{I}_{h,w,c})^2$$
- **Componente Interactivo / Simulador a construir**
  - App Streamlit con sliders de brillo, contraste, gamma y ruido gaussiano; vista original vs transformada y heatmap de error.
- **Patrón de Prompting a dominar**
  - Prompt estructurado con contratos: shapes (`H,W,C`), tipos (`uint8` entrada, `float32` procesamiento), límite de latencia por frame.
- **Proyecto Práctico Express (Webcam/Dataset)**
  - "Inspector de calidad de imagen" sobre webcam para medir exposición y ruido en tiempo real.
- **Métrica de Optimización / Rendimiento evaluada**
  - ms/frame en CPU, histograma de luminancia, MSE/SSIM entre frame crudo y corregido.

### Módulo 2 — Convolución y filtrado clásico
- **Conceptos Matemáticos Clave**
  - Convolución discreta 2D: $$Y(i,j)=\sum_{m=-k}^{k}\sum_{n=-k}^{k}K(m,n)\,I(i-m,j-n)$$
  - Gradiente Sobel: $$G=\sqrt{G_x^2+G_y^2}$$
- **Componente Interactivo / Simulador a construir**
  - Widget con sliders de kernel size, sigma, umbral de Canny y selector de padding.
- **Patrón de Prompting a dominar**
  - Prompt "prompt-to-code" para generar pipeline OpenCV con pruebas de shape y clipping seguro.
- **Proyecto Práctico Express (Webcam/Dataset)**
  - Detector de bordes robusto a iluminación para documentos capturados por webcam.
- **Métrica de Optimización / Rendimiento evaluada**
  - FPS, tasa de falsos bordes por ruido y costo de memoria temporal por buffers intermedios.

### Módulo 3 — Segmentación y visión clásica en condiciones reales
- **Conceptos Matemáticos Clave**
  - Umbralización adaptativa y morfología: $$I_{bin}(x,y)=\mathbb{1}[I(x,y)>T(x,y)]$$
  - Operaciones de apertura/cierre para limpieza de máscara.
- **Componente Interactivo / Simulador a construir**
  - App con sliders de bloque adaptativo, C, iteraciones morfológicas y tamaño estructurante.
- **Patrón de Prompting a dominar**
  - Prompt con restricciones de robustez (cambios de temperatura de color, sombras y compresión JPEG).
- **Proyecto Práctico Express (Webcam/Dataset)**
  - Segmentador de objeto principal en mesa con fondo variable usando webcam.
- **Métrica de Optimización / Rendimiento evaluada**
  - IoU de máscara, latencia p95 y sensibilidad a ruido sensor.

### Módulo 4 — CNNs y entrenamiento mínimo orientado a inferencia
- **Conceptos Matemáticos Clave**
  - Capa convolucional y activación: $$A^{(l)}=\phi(W^{(l)}*A^{(l-1)}+b^{(l)})$$
  - Cross-Entropy: $$L_{CE}=-\sum_i y_i\log(\hat{y}_i)$$
  - Actualización: $$\theta_{t+1}=\theta_t-\eta\nabla_\theta L$$
- **Componente Interactivo / Simulador a construir**
  - Dashboard con sliders de learning rate, batch size y augmentations; curvas loss/accuracy en vivo.
- **Patrón de Prompting a dominar**
  - Prompt para generar script PyTorch completo con asserts de dimensiones NCHW y control de `float32`.
- **Proyecto Práctico Express (Webcam/Dataset)**
  - Clasificador binario rápido (ej. objeto presente/no presente) con dataset ligero.
- **Métrica de Optimización / Rendimiento evaluada**
  - Accuracy, latencia de inferencia por imagen y memoria RAM/VRAM durante entrenamiento mínimo.

### Módulo 5 — VLMs y prompting multimodal en producción
- **Conceptos Matemáticos Clave**
  - Similaridad embedding texto-imagen: $$s = \frac{v\cdot t}{\|v\|\|t\|}$$
  - Atención (conceptual): $$\text{Attn}(Q,K,V)=\text{softmax}(QK^T/\sqrt{d_k})V$$
- **Componente Interactivo / Simulador a construir**
  - Interfaz para comparar prompts multimodales, top-k resultados y mapas de confianza.
- **Patrón de Prompting a dominar**
  - Prompt maestro con formato JSON estricto, criterios de rechazo y límites de latencia/costo.
- **Proyecto Práctico Express (Webcam/Dataset)**
  - "Asistente visual": descripción + clasificación semántica de escenas de webcam.
- **Métrica de Optimización / Rendimiento evaluada**
  - Top-1/Top-5 semántico, tokens por inferencia y latencia extremo a extremo.

### Módulo 6 — Optimización a bajo nivel y despliegue
- **Conceptos Matemáticos Clave**
  - Cuantización afín INT8: $$q = \text{round}(x/s)+z,\quad x \approx s(q-z)$$
  - Distilación: $$L_{distill}=\alpha L_{CE} + (1-\alpha)T^2L_{KL}$$
- **Componente Interactivo / Simulador a construir**
  - Simulador con sliders de bits (FP32/FP16/INT8), batch y backend (CPU/ORT) para comparar precisión/latencia.
- **Patrón de Prompting a dominar**
  - Prompt para exportar PyTorch→ONNX, ejecutar ONNX Runtime y registrar métricas reproducibles.
- **Proyecto Práctico Express (Webcam/Dataset)**
  - Exportar modelo entrenado a ONNX + PTQ INT8 y comparar contra baseline FP32 en webcam.
- **Métrica de Optimización / Rendimiento evaluada**
  - Latencia (ms/frame), FPS, tamaño del modelo (MB), consumo de memoria y caída de accuracy.

## Análisis crítico transversal de producción (aplicable a todos los módulos)
- Evaluar fallas por **ruido de sensor**, **variación de iluminación**, **desenfoque de movimiento** y **compresión JPEG**.
- Reportar trade-offs reales: **Precisión (mAP/IoU/SSIM) vs Latencia (FPS/ms) vs Tamaño (MB)**.
- Incluir mediciones de cuello de botella: ancho de banda de memoria, saturación CPU y costo de pre/post-procesamiento.
