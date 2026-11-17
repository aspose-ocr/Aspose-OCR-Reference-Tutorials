---
category: general
date: 2026-03-26
description: Cómo extraer texto de PDF usando OCR. Aprende a cargar el PDF como imagen,
  reconocer el texto del PDF y extraer texto del PDF con un sencillo ejemplo en Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: es
og_description: Cómo extraer texto de PDF usando OCR. Esta guía te muestra cómo cargar
  un PDF como imagen, reconocer el texto del PDF y extraer texto del PDF en Python.
og_title: Cómo extraer texto de PDF con OCR – Tutorial completo
tags:
- OCR
- Python
- PDF processing
title: Cómo extraer texto de PDF con OCR – Guía completa paso a paso
url: /es/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer texto de PDF con OCR – Guía completa paso a paso

¿Alguna vez te has preguntado **cómo extraer PDF** que en realidad son solo imágenes escaneadas? No estás solo—muchos desarrolladores se topan con este obstáculo cuando necesitan contenido buscable pero solo tienen PDFs de solo imágenes. ¿La buena noticia? Unas pocas líneas de código y una biblioteca OCR sólida pueden convertir esos PDFs de imágenes en texto plano en un instante.  

En este tutorial recorreremos **cómo usar OCR** para cargar un PDF como imagen, reconocer texto en PDF y finalmente **extraer texto de PDF** de documentos de cualquier longitud. Al final tendrás un script ejecutable, una explicación clara de cada paso y varios consejos para evitar los problemas habituales.

## Lo que necesitarás

- Python 3.9 o superior (el código también funciona en 3.10+)  
- El paquete Python `ocr` (o cualquier biblioteca OCR compatible que exponga `OcrEngine`, `OcrEngineMode` y `Imaging.Image`)  
- Un PDF multipágina que quieras procesar (para la demo lo llamaremos `multi_page.pdf`)  
- Familiaridad básica con entornos virtuales (opcional pero recomendado)

> **Pro tip:** Si estás en Windows, considera usar el Anaconda Prompt; en macOS/Linux, un simple `python -m venv venv && source venv/bin/activate` hace el truco.

## Paso 1: Instalar la biblioteca OCR

Primero, descarga el paquete OCR desde PyPI. El ejemplo a continuación usa un paquete ficticio `ocr` que refleja la API mostrada en el fragmento de código, pero la mayoría de las bibliotecas reales (como `pytesseract` + `pdf2image`) siguen el mismo patrón.

```bash
pip install ocr
```

Si estás usando un motor diferente, reemplaza `ocr` con el nombre apropiado (p. ej., `pip install pytesseract pdf2image`).

## Paso 2: Inicializar el motor OCR

Crear una instancia del motor es la base de **cómo extraer texto de PDF**. Piensa en el motor como el cerebro que interpretará los píxeles dentro de cada página del PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Por qué importa:** `set_engine_mode` te permite equilibrar velocidad y precisión. `DEFAULT` es una opción equilibrada; si necesitas mayor precisión, cambia a `HIGH_ACCURACY` (si la biblioteca lo soporta).

## Paso 3: Cargar el PDF como un objeto Imagen

OCR funciona sobre imágenes, no sobre contenedores PDF, por lo que primero debemos convertir el PDF a una representación de imagen. El método `Imaging.Image.load` maneja PDFs multipágina automáticamente.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Caso límite:** Algunas bibliotecas solo aceptan una imagen de una sola página. En ese caso, deberías iterar sobre cada página usando `pdf2image.convert_from_path`. Nuestra llamada a `load` abstrae eso, convirtiendo **cargar pdf como imagen** en una sola línea.

## Paso 4: Reconocer texto en todas las páginas

Ahora llega el núcleo de **reconocer texto en PDF**. El motor escanea cada página, devolviendo una lista de objetos de resultado—uno por página.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Cada `page_result` contiene métodos como `get_text()` (texto plano) y `get_confidence()` (métrica opcional de calidad).  

> **Consejo:** Si solo necesitas la primera página, llama a `recognize(pdf_image[0])` en lugar del ayudante multipágina.

## Paso 5: Iterar a través de los resultados y mostrar el texto extraído

Finalmente, iteramos sobre los resultados, imprimiendo el texto de cada página. Esto completa el flujo de **extraer texto de PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Salida esperada

Si `multi_page.pdf` contiene tres páginas con las palabras “Hello”, “World” y “Python”, verás:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Eso es todo—tu PDF ahora es completamente buscable y el texto está listo para procesamiento posterior (indexación, análisis de sentimientos, lo que necesites).

## Paso 6: Manejo de problemas comunes

| Problema | Por qué ocurre | Solución rápida |
|----------|----------------|-----------------|
| **Salida en blanco** | Las páginas del PDF están escaneadas a bajo DPI, lo que hace que los caracteres sean indistinguibles. | Escala la imagen antes de OCR: `pdf_image = pdf_image.resize(300)` (300 DPI es un buen punto medio). |
| **Caracteres basura** | Los alfabetos no latinos requieren paquetes de idioma. | Carga el modelo de idioma apropiado: `ocr_engine.load_language('spa')` para español, etc. |
| **Desbordamiento de memoria en PDFs enormes** | Cargar todas las páginas a la vez consume RAM. | Procesa las páginas en lotes: `for img in pdf_image.split(batch=10): …` (pseudocódigo). |
| **Rendimiento lento** | Usar `DEFAULT` en un documento masivo puede ser lento. | Cambia a modo `FAST` o ejecuta OCR en paralelo usando `concurrent.futures`. |

## Bonus: Guardar el texto extraído en un archivo

La mayoría de los flujos de trabajo reales necesitan persistir el texto. Aquí tienes un pequeño helper que escribe todo en `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Ahora puedes alimentar `output.txt` a un motor de búsqueda, una base de datos o cualquier modelo de NLP.

## Juntándolo todo – Script completo

A continuación tienes el programa completo, listo para ejecutar. Copia‑pega, ajusta las rutas de archivo y listo.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Ejecuta:

```bash
python extract_pdf_ocr.py
```

Deberías ver el contenido de cada página impreso en la consola, seguido de una confirmación de que el archivo `extracted_text.txt` fue creado.

## Conclusión

Hemos cubierto **cómo extraer texto de PDF** de documentos solo de imágenes usando un motor OCR, desde la instalación de la biblioteca hasta el manejo de resultados multipágina y el guardado de la salida. Ahora sabes **cómo usar OCR**, cómo **cargar PDF como imagen** y cómo **reconocer texto en PDF** de forma fiable.  

¿Próximos pasos? Prueba cambiar el modo de motor predeterminado a una configuración de alta precisión, experimenta con paquetes de idioma para PDFs multilingües, o canaliza el texto extraído a un índice de búsqueda completa como Elasticsearch. El cielo es el límite una vez que domines los fundamentos de la extracción de texto de archivos PDF.

---

![ejemplo de cómo extraer pdf](images/ocr_flowchart.png){alt="diagrama de flujo de extracción de pdf"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}