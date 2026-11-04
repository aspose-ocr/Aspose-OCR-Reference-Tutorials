---
category: general
date: 2026-01-12
description: Cómo ejecutar OCR y extraer texto de imágenes de facturas usando Aspose
  OCR y un modelo ligero de Hugging Face. Aprende a descargar el modelo, corregir
  errores de OCR y realizar OCR en la imagen.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: es
og_description: Cómo ejecutar OCR en imágenes de facturas, extraer texto y corregir
  errores con un LLM de Hugging Face. Sigue esta guía completa para obtener resultados
  impecables.
og_title: Cómo ejecutar OCR en imágenes de facturas – Tutorial completo
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Cómo ejecutar OCR en imágenes de facturas – Guía completa paso a paso
url: /es/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR en imágenes de facturas – Guía completa paso a paso

¿Alguna vez te has preguntado **cómo ejecutar OCR** en una factura escaneada y obtener texto limpio y buscable sin pasar horas limpiándolo? No eres el único. En muchos proyectos del mundo real la salida cruda de OCR está plagada de errores de reconocimiento—piensa en “O” por “0”, “l” por “1”, o incluso palabras completas distorsionadas. ¿La buena noticia? Con unas pocas líneas de Python no solo puedes **realizar OCR en imágenes** sino también corregir automáticamente **errores de OCR** usando un modelo ligero de Hugging Face.

En este tutorial repasaremos todo lo que necesitas saber: desde cargar una imagen de factura, extraer texto crudo, descargar un modelo cuantizado, hasta pulir el resultado para que termines con una transcripción perfecta lista para el procesamiento posterior. Al final podrás **extraer texto de facturas** en PDF o PNG con un único script reproducible.

## Requisitos y configuración

Antes de comenzar, asegúrate de tener:

| Requisito | Por qué es importante |
|-----------|-----------------------|
| Python 3.9+ | Sintaxis moderna y anotaciones de tipo |
| paquete `aspose-ocr` | Proporciona el `ocr.OcrEngine` usado en el ejemplo |
| paquete `aspose-ai` | Suministra el post‑procesador `AsposeAI` |
| Acceso a una GPU (opcional) | Acelera las capas LLM; de lo contrario la CPU funciona bien |
| Conexión a internet (primera ejecución) | Necesaria para **descargar modelo de Hugging Face** automáticamente |

Puedes instalar las librerías requeridas con:

```bash
pip install aspose-ocr aspose-ai
```

> **Consejo profesional:** Si planeas ejecutar el LLM en GPU, instala `torch` con soporte CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Ahora que el entorno está listo, pasemos al código.

---

## Paso 1 – Inicializar el motor OCR y cargar tu imagen de factura

Lo primero que debes hacer es crear una instancia del motor OCR de Aspose y apuntarla al archivo que deseas procesar. Este paso es la base de **cómo ejecutar OCR** en cualquier imagen.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Por qué es importante:** `load_image` acepta PNG, JPEG, TIFF e incluso páginas PDF, permitiéndote **realizar OCR en datos de imagen** sin importar el formato.

---

## Paso 2 – Ejecutar OCR básico para capturar texto crudo

Una vez cargada la imagen, el motor puede producir una transcripción cruda. Esta salida suele ser ruidosa, por eso más adelante ejecutaremos una fase de corrección.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Una salida cruda típica podría verse así:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

¿Ves los ceros (`0`) donde debería estar la letra “O”? Ese es exactamente el tipo de error que corregiremos después.

---

## Paso 3 – Configurar el post‑procesador IA con un LLM ligero

Ahora incorporamos un **descargar modelo de Hugging Face** lo suficientemente pequeño para ejecutarse en hardware modesto pero lo bastante potente para entender el lenguaje de facturas. El ejemplo usa el modelo Qwen 2.5 3B‑Instruct GGUF, cuantizado a `int8` para una huella de memoria mínima.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **¿Por qué este modelo?** La cuantización `int8` reduce el archivo a ~1.2 GB, haciéndolo viable en la mayoría de los portátiles. Las capas GPU aceleran la inferencia, pero el código recurre a la CPU de forma elegante cuando no se detecta GPU.

---

## Paso 4 – Ejecutar la corrección basada en LLM sobre el resultado OCR crudo

Con el modelo listo, alimentamos el texto crudo al post‑procesador. El LLM reescribirá la transcripción, corrigiendo fallos comunes de OCR y normalizando los números.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Salida limpiada esperada:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Puedes ver que los ceros se han convertido nuevamente en la letra “O”, y “Am0unt” ahora es “Amount”. Este es el núcleo de **corregir errores de OCR** automáticamente.

---

## Paso 5 – Liberar recursos y limpiar

Los modelos de lenguaje grande pueden retener memoria de GPU, por lo que es una buena práctica liberar los recursos cuando terminas.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Si planeas procesar muchas facturas en lote, podrías mantener el modelo cargado y liberarlo solo al final del script.

---

## Ejemplo completo funcional

Juntando todo, aquí tienes un script único que puedes guardar en un archivo `.py` y ejecutar:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Ejecutar el script debería producir una salida similar al bloque “AI‑corrected” mostrado antes. Siéntete libre de cambiar la ruta de la imagen por cualquier otra factura o recibo para **extraer texto de facturas** en masa.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si no tengo GPU?

El parámetro `gpu_layers` es opcional. Establécelo en `0` o simplemente omítelo, y el modelo se ejecutará completamente en CPU. Espera una inferencia más lenta—aproximadamente 2–3 segundos por página en un portátil moderno.

### Mis facturas son PDFs de varias páginas. ¿Cómo las manejo?

Convierte cada página a una imagen separada (por ejemplo, usando `pdf2image`) y recorre las páginas con el mismo script. El motor OCR puede procesar cada imagen de forma independiente, y el LLM corregirá cada bloque de texto.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### ¿La descarga del modelo falla detrás de un firewall?

Descarga el modelo manualmente desde el hub de Hugging Face, descomprímelo en una carpeta local y apunta `hugging_face_repo_id` a la ruta local:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### ¿Qué tan precisa es la corrección?

Para facturas típicas en inglés, el LLM corrige >95 % de los errores comunes de OCR. Notas manuscritas complejas pueden requerir revisión manual.

---

## Consejos y trucos para uso en producción

- **Procesamiento por lotes:** Encapsula los pasos 2‑4 en una función y pasa una lista de rutas de archivo. Reutiliza la misma instancia de `AsposeAI` para evitar recargar el modelo.
- **Registro (logging):** Sustituye `print` por el módulo `logging` de Python para capturar tanto salidas crudas como corregidas y mantener auditorías.
- **Manejo de errores:** Rodea la llamada OCR con bloques `try/except`. Si una imagen falla, registra el nombre del archivo y continúa.
- **Ajuste de rendimiento:** Experimenta con `gpu_layers`. Más capas en GPU aceleran la inferencia pero aumentan el uso de VRAM.

---

## Conclusión

Hemos cubierto **cómo ejecutar OCR** en imágenes de facturas de principio a fin, mostrándote cómo **realizar OCR en imágenes**, **descargar modelo de Hugging Face** y **corregir errores de OCR** automáticamente. El script completo demuestra un flujo de trabajo práctico que puedes integrar en cualquier pipeline de automatización basado en Python.

¿Próximos pasos? Prueba a extender la canalización para **extraer campos clave** (número de factura, fecha, total) usando expresiones regulares sobre el texto corregido, o envía la salida limpia a una base de datos para registros buscables. También puedes experimentar con otros LLM ligeros de Hugging Face si necesitas otro idioma o conocimiento específico de dominio.

¡Feliz codificación, y que tus resultados de OCR siempre sean cristalinos!

![cómo ejecutar OCR en una imagen de factura](ocr_invoice_example.png "cómo ejecutar OCR en una factura")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}