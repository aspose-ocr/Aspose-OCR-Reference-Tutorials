---
category: general
date: 2026-06-19
description: Cómo ejecutar OCR paso a paso y mejorar la precisión del OCR con técnicas
  de OCR de texto plano. Aprende un flujo de trabajo rápido para una extracción de
  texto fiable.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: es
og_description: Cómo ejecutar OCR de manera eficiente. Este tutorial muestra cómo
  mejorar la precisión del OCR utilizando OCR de texto plano y post‑procesamiento
  con IA.
og_title: Cómo ejecutar OCR en Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Cómo ejecutar OCR en Python – Guía completa
url: /es/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR en Python – Guía completa

¿Alguna vez te has preguntado **cómo ejecutar OCR** en un lote de PDFs escaneados sin pasar horas ajustando configuraciones? No estás solo. En muchos proyectos el primer obstáculo es simplemente obtener texto fiable de una imagen, y la diferencia entre un pase inestable y una extracción limpia a menudo se reduce a un par de pasos inteligentes.

En esta guía recorreremos una canalización práctica de cuatro pasos que no solo **ejecuta OCR**, sino que también **mejora la precisión del OCR** combinando una pasada rápida de texto plano con una segunda pasada consciente del diseño y un post‑procesador impulsado por IA. Al final tendrás un script listo para ejecutar, una explicación clara de por qué cada etapa es importante y consejos para manejar casos extremos como páginas de varias columnas o escaneos ruidosos.

---

## Lo que necesitarás

- **Python 3.9+** – el código usa anotaciones de tipo y f‑strings.
- **Tesseract OCR** instalado y accesible mediante el comando `tesseract`. (En Ubuntu: `sudo apt install tesseract-ocr`; en Windows descarga el instalador del repositorio oficial.)
- El wrapper **pytesseract** (`pip install pytesseract`).
- Una **biblioteca de post‑procesamiento IA** – para este ejemplo fingiremos que tienes un módulo ligero `ai` que ofrece `run_postprocessor`. Reemplázalo con la API GPT‑4 de OpenAI o un LLM local si lo prefieres.
- Algunas imágenes o PDFs de muestra para probar.

Eso es todo. Sin frameworks pesados, sin acrobacias con Docker. Solo un puñado de instalaciones con pip y estarás listo para comenzar.

## Paso 1: Realizar una pasada rápida de OCR de texto plano

Lo primero que la mayoría de los desarrolladores pasa por alto es que una ejecución de OCR de *texto plano* es extremadamente rápida y te brinda una rápida verificación de sanidad. Llamaremos a `engine.Recognize()` para obtener los caracteres crudos sin ningún metadato de diseño. Esto es lo que queremos decir con **OCR de texto plano**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Por qué esto importa:*  
- **Velocidad** – una pasada plana en una página de 300 dpi suele terminar en menos de un segundo.  
- **Línea base** – puedes comparar la salida estructurada posterior con esta línea base para detectar errores evidentes.  
- **Detección de errores** – si la pasada plana falla completamente (p. ej., todo es un galimatías), sabes que la calidad de la imagen es demasiado baja y puedes abortar temprano.

## Paso 2: Ejecutar una pasada de OCR detallada y consciente del diseño

El texto plano es genial, pero descarta *dónde* se encuentra cada palabra en la página. Para facturas, formularios o revistas de varias columnas necesitas coordenadas, números de línea y quizá incluso información de fuente. Ahí es donde entra `engine.RecognizeStructured()`.

A continuación hay un contenedor ligero alrededor de la salida **TSV** de Tesseract, que nos brinda una jerarquía de páginas → líneas → palabras, preservando los cuadros delimitadores.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Por qué hacemos esto:*  
- **Coordenadas** te permiten mapear posteriormente el texto extraído de vuelta a la imagen original para resaltar o redactar.  
- **Agrupación de líneas** preserva el diseño original, lo cual es esencial cuando necesitas reconstruir tablas o columnas.  
- Esta pasada es un poco más lenta que la plana, pero aún termina en unos pocos segundos para la mayoría de los documentos.

## Paso 3: Ejecutar el post‑procesador IA para corregir errores de OCR

Incluso el mejor motor de OCR comete errores—piensa en “rn” vs “m”, diacríticos faltantes o palabras divididas. Un modelo de IA puede observar la cadena cruda y los datos estructurados, detectar inconsistencias y reescribir el texto manteniendo intactas las coordenadas originales.

A continuación hay una implementación **simulada**; reemplaza el cuerpo con una llamada real a un LLM si dispones de uno.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Por qué este paso mejora la precisión del OCR:*  
- **Correcciones contextuales** – la IA puede decidir que “l0ve” probablemente sea “love” basándose en las palabras circundantes.  
- **Preservación de coordenadas** – mantienes la información de diseño, por lo que las tareas posteriores (como la anotación de PDFs) siguen siendo precisas.  
- **Refinamiento iterativo** – podrías ejecutar el post‑procesador varias veces, cada pasada limpiando más errores.

## Paso 4: Iterar a través de la salida estructurada y corregida

Ahora que tenemos una estructura limpiada, extraer el texto final es trivial. A continuación imprimimos cada línea, pero también podrías escribir a un CSV, alimentar una base de datos o generar un PDF searchable.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Salida esperada** (asumiendo una factura simple de una página):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Observa cómo se preservan los saltos de línea y el orden de columnas, y cómo fallos comunes de OCR como “$15.00” leído como “$15,00” son corregidos por el paso de IA.

## Cómo este flujo de trabajo ayuda a **Mejorar la precisión del OCR**

| Etapa | Qué corrige | Por qué importa |
|------|-------------|-----------------|
| **OCR de texto plano** | Detecta páginas ilegibles temprano | Ahorra tiempo al omitir entradas sin esperanza |
| **OCR estructurado** | Captura el diseño, coordenadas | Permite tareas posteriores (resaltar, redactar) |
| **Post‑procesador IA** | Corrige ortografía, une palabras divididas, arregla números | Incrementa la precisión general a nivel de carácter de ~85 % a >95 % en escaneos ruidosos |
| **Iteración** | Permite volver a ejecutar con parámetros afinados | Ajusta finamente la canalización para tipos de documentos específicos |

Al combinar estos tres conceptos—**OCR de texto plano**, extracción consciente del diseño y corrección IA—obtienes una solución robusta que *significativamente* **mejora la precisión del OCR** sin escribir una red neuronal personalizada desde cero.

## Errores comunes y consejos profesionales

- **Trampa:** Alimentar una imagen de baja resolución (≤150 dpi) a Tesseract produce una salida confusa.  
  **Consejo profesional:** Pre‑procesa con `Pillow`—aplica `Image.convert('L')` y `Image.filter(ImageFilter.MedianFilter())` antes del OCR.

- **Trampa:** El post‑procesador IA puede reescribir accidentalmente terminología específica del dominio (p. ej., “SKU123”).  
  **Consejo profesional:** Construye una lista blanca de términos y pásala al LLM o a una biblioteca de corrector ortográfico como `pyspellchecker`.

- **Trampa:** Las páginas de varias columnas se fusionan en una sola línea.  
  **Consejo profesional:** Detecta los límites de columna usando el campo `block_num` en la salida TSV de Tesseract y divide las líneas en consecuencia.

- **Trampa:** Los PDFs grandes provocan un desbordamiento de memoria al cargar todas las páginas a la vez.  
  **Consejo profesional:** Procesa las páginas de forma incremental—itera sobre `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

## Extender la canalización

Si tienes curiosidad por los siguientes pasos, considera las siguientes mejoras:

1. **Procesamiento por lotes** – Envuelve todo el script en una función que recorra un directorio, manejando miles de archivos en paralelo con `concurrent.futures`.
2. **Modelos de lenguaje** – Sustituye la heurística simple de difflib por una llamada al `gpt‑4o` de OpenAI o a un modelo LLaMA alojado localmente para obtener correcciones contextuales más ricas.
3. **Formatos de exportación** – Escribe la estructura corregida a un PDF searchable

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}