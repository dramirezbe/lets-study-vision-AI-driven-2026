# Plantilla de Desarrollo por Módulo

Usar esta plantilla para desarrollar cada módulo con rigor técnico y enfoque prompt-to-code.

## Encabezado del Módulo
- **Módulo:** `[NÚMERO] - [NOMBRE]`
- **Temas principales:** `[LISTA DE TEMAS]`
- **Objetivo técnico medible:** `[métrica objetivo: latencia/accuracy/memoria]`

## 1) Rigor Matemático y Geométrico (Sin relleno)
- Ecuaciones en LaTeX (mínimo 3, con variables definidas y unidades):
  - $...$
  - $$...$$
- Impacto directo en tensores/matrices:
  - Forma de entrada: `[H, W, C]` o `[N, C, H, W]`
  - Transformación de forma: `[...]->[...]`
  - Coste de memoria estimado: `bytes = num_elementos × tamaño_tipo`
- Intuición geométrica/vectorial enfocada en comportamiento del sistema (sin ejercicios repetitivos).

## 2) Vista Visual e Interactiva (código completo ejecutable)
- Entregable: un archivo único (`.html` con Canvas/WebGPU) o app ligera (`streamlit_app.py` / `gradio_app.py`).
- Controles obligatorios:
  - Sliders para parámetros clave (kernel, umbral, learning rate, bits de cuantización, etc.).
  - Switches para activar/desactivar etapas del pipeline.
- Resultado visual inmediato sobre imagen/matriz/activaciones.

## 3) Ingeniería de Prompts para Código
### 3.1 Prompt Maestro (copiar/pegar en LLM)
```text
Eres un ingeniero senior de visión por computadora.
Genera código ejecutable y listo para producción para el módulo [NÚMERO-NOMBRE].
Requisitos estrictos:
1) Entrada y salida tipadas con shapes explícitos.
2) Validaciones de tensores con asserts.
3) Uso de dtype controlado (float32/int8 según etapa).
4) Restricción de latencia objetivo: [X] ms/frame en CPU.
5) Código modular con funciones puras y script de ejecución.
6) Incluye medición de memoria y tiempo por etapa.
Entrega: archivos completos y comando de ejecución.
```

### 3.2 Criterios de verificación del código generado
- Asserts de forma (`NCHW`, `HWC`) y rango de valores.
- Verificación de dtype (`float32` entrenamiento, `int8` inferencia cuantizada).
- Perfilado básico:
  - Tiempo por frame (ms)
  - FPS promedio y p95
  - Memoria RAM/VRAM

## 4) Micro-Proyecto Práctico (<=15 min)
- **Escenario:** webcam del portátil o dataset público ligero.
- **Flujo paso a paso:**
  1. Ejecutar prompt maestro y generar código.
  2. Ejecutar script con ejemplo base.
  3. Activar interfaz interactiva y ajustar parámetros.
  4. Registrar métricas clave.
  5. Guardar evidencia (`capturas`, `métricas`, `configuración`).
- **Criterio de éxito:** salida funcional + métrica objetivo alcanzada o diagnóstico de cuello de botella.

## 5) Optimización a Bajo Nivel y Despliegue
- Exportación de grafo (ej. PyTorch -> ONNX).
- Estrategia principal (elegir una o ambas):
  - PTQ INT8 con calibración de rangos.
  - Distilación teacher-student con:
    $$L_{distill}=\alpha L_{CE} + (1-\alpha)T^2L_{KL}$$
- Medición comparativa obligatoria:
  - FP32 vs FP16/INT8 en latencia, tamaño de modelo y precisión.

## 6) Análisis Crítico de Producción
- Documentar **3 fallas reales** del módulo en entorno industrial/comercial.
  - Ejemplos: aliasing, artefactos JPEG, iluminación extrema, cuello de botella CPU.
- Justificar trade-offs reales:
  - Precisión (`mAP/IoU/SSIM`) vs Latencia (`FPS`) vs Tamaño (`MB`).
- Decisión final de despliegue basada en métricas, no en intuición.
