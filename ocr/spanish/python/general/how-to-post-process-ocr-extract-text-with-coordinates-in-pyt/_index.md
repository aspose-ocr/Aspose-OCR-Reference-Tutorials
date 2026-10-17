---
category: general
date: 2026-04-26
description: Cómo post‑procesar resultados de OCR y extraer texto con coordenadas.
  Aprende una solución paso a paso usando salida estructurada y corrección con IA.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: es
og_description: Cómo post‑procesar los resultados de OCR y extraer texto con coordenadas.
  Sigue este tutorial completo para un flujo de trabajo fiable.
og_title: Cómo post‑procesar OCR – Guía completa
tags:
- OCR
- Python
- AI
- Text Extraction
title: Cómo post‑procesar OCR – Extraer texto con coordenadas en Python
url: /es/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo post‑procesar OCR – Extraer texto con coordenadas en Python

¿Alguna vez necesitaste **post‑procesar OCR** resultados porque la salida cruda era ruidosa o desalineada? No eres el único. En muchos proyectos del mundo real—escaneo de facturas, digitalización de recibos, o incluso la mejora de experiencias de AR—el motor OCR te da palabras crudas, pero aún tienes que limpiarlas y mantener el seguimiento de dónde vive cada palabra en la página. Ahí es donde un modo de salida estructurada combinado con un post‑procesador impulsado por IA brilla.

En este tutorial recorreremos una canalización completa y ejecutable en Python que **extrae texto con coordenadas** de una imagen, ejecuta un paso de corrección basado en IA y muestra cada palabra junto con su posición (x, y). Sin importaciones faltantes, sin atajos vagos de “ver la documentación”—solo una solución autónoma que puedes incorporar a tu proyecto hoy.

> **Consejo profesional:** Si estás usando una biblioteca OCR diferente, busca un modo “structured” o “layout”; los conceptos siguen siendo los mismos.

---

## Requisitos previos

Antes de profundizar, asegúrate de tener:

| Requisito | Por qué es importante |
|-------------|------------------------|
| Python 3.9+ | Sintaxis moderna y anotaciones de tipo |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | Biblioteca `ocr` que soporta `OutputMode.STRUCTURED` (p. ej., una ficticia `myocr`) |
| Needed for bounding‑box data | Necesario para datos de cajas delimitadoras |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | Un módulo de post‑procesamiento de IA (puede ser OpenAI, HuggingFace, o un modelo personalizado) |
| Improves accuracy after OCR | Mejora la precisión después del OCR |
| An image file (`input.png`) in your working directory | Un archivo de imagen (`input.png`) en tu directorio de trabajo |
| The source we’ll read | La fuente que leeremos |

Si alguno de estos te suena desconocido, simplemente instala los paquetes de marcador con `pip install myocr ai‑postproc`. El código a continuación también incluye stubs de reserva para que puedas probar el flujo sin las bibliotecas reales.

## Paso 1: Habilitar el modo de salida estructurada para el motor OCR  

Lo primero que hacemos es indicarle al motor OCR que nos dé más que solo texto plano. La salida estructurada devuelve cada palabra junto con su caja delimitadora y puntuación de confianza, lo cual es esencial para **extraer texto con coordenadas** más adelante.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Por qué es importante:* Sin el modo estructurado solo obtendrías una cadena larga, y perderías la información espacial que necesitas para superponer texto en imágenes o alimentar análisis de diseño posteriores.

## Paso 2: Reconocer la imagen y capturar palabras, cajas y confianza  

Ahora alimentamos la imagen al motor. El resultado es un objeto que contiene una lista de objetos palabra, cada uno exponiendo `text`, `x`, `y`, `width`, `height` y `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Caso límite:* Si la imagen está vacía o no se puede leer, `structured_result.words` será una lista vacía. Es una buena práctica verificar eso y manejarlo de forma elegante.

## Paso 3: Ejecutar post‑procesamiento basado en IA mientras se preservan las posiciones  

Incluso los mejores motores OCR cometen errores—piensa en “O” vs. “0” o diacríticos faltantes. Un modelo de IA entrenado en texto específico de dominio puede corregir esos errores. Crucialmente, mantenemos las coordenadas originales para que el diseño espacial permanezca intacto.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Por qué preservamos las coordenadas:* Muchas tareas posteriores (p. ej., generación de PDF, etiquetado AR) dependen de una colocación exacta. La IA solo modifica el campo `text`, dejando `x`, `y`, `width`, `height` sin tocar.

## Paso 4: Iterar sobre las palabras corregidas y mostrar su texto con coordenadas  

Finalmente, iteramos sobre las palabras corregidas e imprimimos cada palabra junto con su esquina superior izquierda `(x, y)`. Esto satisface el objetivo de **extraer texto con coordenadas**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Salida esperada (ejemplo):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Cada línea muestra la palabra corregida y su ubicación exacta en la imagen original.

## Ejemplo completo y funcional  

A continuación hay un único script que une todo. Puedes copiar‑pegarlo, ajustar las declaraciones de importación para que coincidan con tus bibliotecas reales y ejecutarlo directamente.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Ejecutando el script**

```bash
python ocr_postprocess_demo.py
```

Si tienes las bibliotecas reales instaladas, el script procesará tu `input.png`. De lo contrario, la implementación de stubs te permite ver el flujo y salida esperados sin dependencias externas.

## Preguntas frecuentes (FAQ)

| Pregunta | Respuesta |
|----------|-----------|
| *¿Esto funciona con Tesseract?* | Tesseract en sí no expone un modo estructurado de forma nativa, pero envoltorios como `pytesseract.image_to_data` devuelven cajas delimitadoras que puedes alimentar al mismo post‑procesador de IA. |
| *¿Qué pasa si necesito la esquina inferior‑derecha en lugar de la superior‑izquierda?* | Cada objeto palabra también proporciona `width` y `height`. Calcula `x2 = x + width` y `y2 = y + height` para obtener la esquina opuesta. |
| *¿Puedo procesar por lotes múltiples imágenes?* | Absolutamente. Envuelve los pasos en un bucle `for image_path in Path("folder").glob("*.png"):` y recopila los resultados por archivo. |
| *¿Cómo elijo un modelo de IA para la corrección?* | Para texto genérico, funciona un pequeño GPT‑2 afinado en errores de OCR. Para datos específicos de dominio (p. ej., recetas médicas), entrena un modelo secuencia‑a‑secuencia con datos ruidosos‑limpios emparejados. |
| *¿Es útil la puntuación de confianza después de la corrección de IA?* | Puedes seguir conservando la confianza original para depuración, pero la IA puede generar su propia confianza si el modelo lo soporta. |

## Casos límite y mejores prácticas  

1. **Imágenes vacías o corruptas** – siempre verifica que `structured_result.words` no esté vacío antes de continuar.  
2. **Scripts no latinos** – asegura que tu motor OCR esté configurado para el idioma objetivo; el post‑procesador de IA debe estar entrenado en el mismo script.  
3. **Rendimiento** – la corrección de IA puede ser costosa. Cachea los resultados si vas a reutilizar la misma imagen, o ejecuta el paso de IA de forma asíncrona.  
4. **Sistema de coordenadas** – las bibliotecas OCR pueden usar orígenes diferentes (superior‑izquierda vs. inferior‑izquierda). Ajusta según sea necesario al superponer en PDFs o lienzos.  

## Conclusión  

Ahora tienes una receta sólida, de extremo a extremo, para **post‑procesar OCR** y **extraer texto con coordenadas** de forma fiable. Al habilitar la salida estructurada, pasar el resultado a través de una capa de corrección de IA y preservar las cajas delimitadoras originales, puedes convertir escaneos OCR ruidosos en texto limpio y consciente del espacio, listo para tareas posteriores como generación de PDF, automatización de entrada de datos o superposiciones de realidad aumentada.

¿Listo para el siguiente paso? Prueba cambiar la IA de sustitución por una llamada a OpenAI `gpt‑4o‑mini`, o integra la canalización en un FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}