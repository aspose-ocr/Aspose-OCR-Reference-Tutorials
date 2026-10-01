---
category: general
date: 2026-01-07
description: Cómo ejecutar OCR y extraer texto de una imagen para el procesamiento
  de facturas. Aprende a mejorar la precisión del OCR, cargar la imagen para OCR y
  procesar OCR de facturas de manera eficiente.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: es
og_description: Cómo ejecutar OCR en facturas paso a paso. Extraer texto de la imagen,
  mejorar la precisión del OCR y cargar la imagen para OCR usando Aspose AI.
og_title: Cómo ejecutar OCR en facturas – Guía completa de Python
tags:
- OCR
- Python
- Image Processing
title: Cómo ejecutar OCR en facturas – Extraer texto de una imagen con Python
url: /es/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR en facturas – Extraer texto de una imagen con Python

¿Alguna vez te has preguntado **cómo ejecutar OCR** en una factura escaneada y obtener texto limpio y buscable? No estás solo. Muchos desarrolladores se topan con un muro cuando la salida cruda del OCR está llena de errores ortográficos, saltos de línea rotos y puntuación ausente. En este tutorial recorreremos una solución full‑stack que no solo **extrae texto de la imagen**, sino que también **mejora la precisión del OCR** mediante un post‑procesamiento con un modelo AI de Aspose.

Verás cómo **cargar la imagen para OCR**, ejecutar el motor incorporado y luego aplicar una corrección ortográfica ligera que hace que el resultado esté listo para análisis posteriores. Al final, tendrás un script reutilizable que puedes insertar en cualquier pipeline de procesamiento de facturas.

> **Lo que necesitarás**  
> * Python 3.9 o superior  
> * Paquetes `aspose-ocr` y `aspose-ai` (instalados vía `pip`)  
> * Una imagen de factura (PNG, JPEG o TIFF) – usaremos `sample_invoice.png` como ejemplo  
> * Opcional: una GPU con al menos 4 GB de VRAM para una inferencia de modelo más rápida (el script también funciona en CPU)

---

## Paso 1: Instalar paquetes requeridos y preparar el entorno

Antes de poder **cargar la imagen para OCR**, debemos asegurarnos de que las bibliotecas necesarias estén disponibles. El motor OCR de Aspose se entrega con un simple wrapper de Python, mientras que el post‑procesador AI depende de un modelo cuantizado de Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Consejo profesional:** Si planeas usar aceleración GPU, instala `torch` con soporte CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Paso 2: Cargar la imagen de la factura

Cargar la imagen es sencillo, pero vale la pena mencionar por qué establecemos explícitamente la ruta como una cadena cruda (`r"..."`). Esto evita errores accidentales de caracteres de escape en rutas de Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Por qué importa:* Usar `ocr.Image.load` garantiza que la imagen se pre‑procese (binarización, corrección de inclinación) según los valores predeterminados óptimos de Aspose, lo que ya **mejora la precisión del OCR** antes de que ocurra cualquier magia AI.

---

## Paso 3: Ejecutar el motor OCR incorporado

Ahora realmente **ejecutamos OCR** y capturamos el texto crudo. Este paso muestra la salida típica que obtendrías de una ejecución OCR básica—a menudo un desastre de saltos de línea y errores ortográficos ocasionales.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Salida cruda típica** (truncada por brevedad):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Podrías notar que “Invoice” aparece como “Invo1ce” o que falta puntuación. Ahí es donde entra el post‑procesador AI.

---

## Paso 4: Configurar el modelo AI de Aspose

El modelo AI que usaremos es **Qwen2.5‑3B‑Instruct‑GGUF**, un LLM ligero ajustado por instrucción que funciona cómodamente en una GPU de gama media. La configuración a continuación indica a Aspose dónde obtener el modelo, cuántas capas mantener en GPU y el tamaño de contexto para manejar párrafos largos.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **¿Por qué esta configuración?**  
> * `gpu_layers=30` equilibra velocidad y memoria—la mayor parte de la inferencia ocurre en la GPU, mientras que las capas restantes permanecen en CPU para evitar errores OOM.  
> * `context_size=4096` asegura que el modelo pueda ver toda la factura de una vez, evitando que se trunque información importante.

---

## Paso 5: Crear un post‑procesador de corrección ortográfica simple

Envolvemos la llamada AI en una pequeña función llamada `simple_spell_check`. El prompt es deliberadamente conciso: “Correct spelling and punctuation:” seguido del texto OCR crudo. El modelo devuelve una versión limpiada.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Cómo funciona:** `ai.run_prompt` envía el prompt al LLM cargado localmente, que luego devuelve una única cadena con ortografía corregida, puntuación adecuada y un diseño de saltos de línea más natural.

---

## Paso 6: Aplicar el post‑procesador al texto OCR crudo

Ahora ocurre la magia. Alimentamos la salida OCR cruda a nuestro post‑procesador y mostramos el resultado mejorado.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Salida mejorada de ejemplo**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Observa la corrección de la palabra “Invoice”, el uso correcto de dos puntos y los saltos de línea consistentes—exactamente lo que necesitas para un análisis posterior fiable.

---

## Paso 7: Liberar recursos

Tanto el motor OCR como el modelo AI asignan recursos nativos. Es una buena práctica liberarlos cuando terminas, sobre todo en servicios de larga ejecución.

```python
ai.free_resources()
engine.dispose()
```

---

## Script completo – Listo para copiar

A continuación tienes el script completo y ejecutable que une todos los pasos. Guárdalo como `invoice_ocr.py`, reemplaza `YOUR_DIRECTORY` con la carpeta que contiene tu imagen de factura y ejecútalo con `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Ejecuta el script y verás tanto el volcado OCR crudo y ruidoso como la versión pulida, **mejorada en precisión OCR**, una al lado de la otra.

---

## Preguntas frecuentes y casos límite

### 1. ¿Qué pasa si mi imagen de factura es un PDF de varias páginas?

Aspose OCR puede cargar directamente páginas PDF. Sustituye la línea de carga de imagen por:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Itera `page_index` para procesar cada página secuencialmente.

### 2. Mi GPU se queda sin memoria—¿puedo usar solo CPU?

Absolutamente. Establece `gpu_layers=0` en el `AsposeAIModelConfig`. El modelo se ejecutará completamente en CPU, lo que es más lento pero seguro para hardware de bajo nivel.

### 3. ¿Cómo manejo facturas que no están en inglés?

Cambia el ID del repositorio del modelo por uno específico de idioma, por ejemplo, `"mistralai/Mistral-7B-Instruct-v0.2"` para soporte multilingüe. El resto del pipeline permanece sin cambios.

### 4. ¿Puedo encadenar varios post‑procesadores (p. ej., formatear fechas, extraer totales)?

Sí. `ai.set_post_processor` acepta una lista de callables. Por ejemplo:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

La salida será primero corregida ortográficamente y luego se le extraerán los totales.

---

## Consejos de rendimiento y buenas prácticas

| Consejo | Por qué ayuda |
|-----|---------------|
| **Procesar varias facturas en lote** – cargarlas en una lista y procesarlas en un bucle. | Reduce la sobrecarga del intérprete Python y mantiene el modelo AI caliente en memoria. |
| **Cachear el modelo** – evitar llamar a `initialize` repetidamente en un servicio web. | La carga del modelo puede tardar ~30 segundos; el caching brinda respuestas instantáneas. |
| **Redimensionar imágenes grandes** a 1500 px de ancho antes del OCR. | Imágenes más pequeñas aceleran tanto OCR como inferencia AI sin sacrificar precisión. |
| **Establecer `allow_auto_download="false"` en producción** – empaqueta el modelo con tu despliegue. | Garantiza tiempos de arranque deterministas y evita interrupciones de red. |

---

## Conclusión

Hemos cubierto **cómo ejecutar OCR** en facturas, desde cargar la imagen hasta pulir el resultado con una corrección ortográfica impulsada por IA. Siguiendo estos pasos puedes **extraer texto de la imagen** de forma fiable, **mejorar la precisión del OCR** y procesar OCR de facturas sin problemas en cualquier flujo de trabajo basado en Python.

Pruébalo con diferentes diseños de facturas—quizá un recibo manuscrito o un contrato escaneado. El mismo pipeline se adapta con mínimas modificaciones, demostrando que una combinación bien estructurada de OCR + IA es una herramienta versátil para cualquier proyecto de automatización documental.

Si te resultó útil esta guía, considera compartirla con tus compañeros o darle una estrella al repositorio que aloja los paquetes Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}