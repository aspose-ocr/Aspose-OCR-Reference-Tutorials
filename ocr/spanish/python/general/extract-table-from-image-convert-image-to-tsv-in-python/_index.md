---
category: general
date: 2026-07-05
description: Extrae una tabla de una imagen usando OCR en Python. Aprende cómo extraer
  la tabla, convertir la imagen a TSV y domina las técnicas de OCR de tablas en Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: es
og_description: Extrae una tabla de una imagen con OCR en Python. Esta guía muestra
  cómo extraer la tabla, convertir la imagen a TSV y usar herramientas de OCR de tablas
  en Python.
og_title: Extraer tabla de una imagen – Convertir imagen a TSV en Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Extraer tabla de una imagen – Convertir imagen a TSV en Python
url: /es/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer tabla de imagen – Convertir imagen a TSV en Python

¿Alguna vez te has preguntado cómo extraer una tabla de una imagen sin volverte loco? En este tutorial recorreremos **cómo extraer una tabla** datos de una foto usando la biblioteca `aocr`, y luego convertir esos datos en un archivo TSV ordenado. No hay magia, solo unas pocas líneas de Python y un poco de post‑procesamiento impulsado por IA.

Si alguna vez intentaste copiar‑pegar una tabla de una factura escaneada o una captura de pantalla y terminaste con un desastre desordenado, apreciarás por qué un enfoque basado en OCR vale la pena dominar. Al final, podrás alimentar cualquier imagen de una tabla a Python y obtener valores separados por tabulaciones limpios, listos para hojas de cálculo o bases de datos.

---

## Lo que necesitarás

| Requisito | Por qué es importante |
|-------------|----------------|
| Python 3.9+ | El paquete `aocr` está dirigido a entornos modernos de Python. |
| `aocr` library (`pip install aocr`) | Proporciona el motor OCR y el post‑procesador de IA que utilizaremos. |
| Un archivo de imagen que contiene una tabla (PNG, JPG, etc.) | Los datos fuente que extraeremos. |
| Opcional: un entorno virtual | Mantiene las dependencias aisladas—altamente recomendado. |

Tener todo listo te evita interrupciones a mitad de la guía.

---

## Instalar las dependencias

Primero, instalemos las herramientas OCR. Abre una terminal y ejecuta:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Consejo profesional:** Si encuentras errores de permiso, agrega `--user` al comando `pip install` o usa `pipx` para una instalación global.

---

## Paso 1 – Inicializar el motor OCR

El motor es el corazón del proceso. Piensa en él como el “cerebro” que observa cada píxel y decide qué carácter pertenece a cada posición.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

¿Por qué instanciamos un motor en lugar de llamar a una única función? El objeto motor nos permite adjuntar post‑procesadores personalizados más adelante, dándonos un control granular sobre la salida—esencial cuando necesitas **ocr table image python** precisión.

---

## Paso 2 – Adjuntar el post‑procesador de IA

`aocr` incluye un post‑procesador de IA ligero que limpia los resultados OCR crudos mientras preserva los bordes de las celdas. No se requieren argumentos adicionales, lo que mantiene el código ordenado.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Si omites este paso, aún obtendrás texto crudo, pero la estructura de la tabla será ruidosa—piensa en una hoja de cálculo donde cada celda es un misterio. El post‑procesador realiza el trabajo pesado de alinear el texto a su cuadrícula original.

---

## Paso 3 – Cargar la imagen de tu tabla

Puedes cargar una imagen desde cualquier ruta, pero para mayor claridad usaremos un directorio de marcador de posición. Reemplaza `"YOUR_DIRECTORY/invoice_table.png"` con la ruta real a tu archivo.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Nota:** `aocr.Image` detecta automáticamente el formato de la imagen y normaliza los canales de color, por lo que no necesitas pre‑procesar el archivo a menos que esté gravemente degradado.

---

## Paso 4 – Realizar OCR estructurado

Ahora el motor escanea la imagen y devuelve un objeto de tabla crudo. Este objeto contiene filas, columnas y el texto crudo de cada celda.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

¿Por qué usar `recognize_structured` en lugar de una llamada genérica `recognize`? La variante estructurada intenta inferir los límites de filas/columnas, dándote un resultado tipo matriz que es mucho más fácil de convertir a TSV después.

---

## Paso 5 – Limpiar los datos con el post‑procesador de IA

Ejecutar el post‑procesador refina la salida cruda: elimina caracteres sueltos, fusiona fragmentos divididos y asegura que el texto de cada celda esté correctamente alineado.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Si inspeccionas `processed_table.table`, verás una lista de filas, cada fila siendo una lista de objetos `Cell`. Cada `Cell` tiene un atributo `.text` que contiene la cadena limpiada.

---

## Paso 6 – Exportar la tabla como TSV

El paso final es convertir los datos procesados en un archivo de valores separados por tabulaciones (TSV)—exactamente lo que necesitas cuando quieres **convertir imagen a TSV** para Excel o Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Ejecutar el script imprime cada fila en la consola (si lo prefieres) y escribe un archivo TSV limpio que puedes abrir en cualquier programa de hojas de cálculo.

### Verificación rápida

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Deberías ver columnas alineadas ordenadamente, como:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Si la salida se ve desordenada, verifica la calidad de la imagen (nitidez, contraste) y considera ajustar la configuración del motor OCR—`engine.set_config(...)` te permite modificar los modelos de idioma y los umbrales de confianza.

---

## Manejo de casos límite comunes

| Situación | Solución sugerida |
|-----------|-------------------|
| **Imagen sesgada** | Pre‑rota usando `Pillow` (`Image.rotate`) antes de pasarla a `aocr`. |
| **Bajo contraste** | Aplica ecualización de histograma (`cv2.equalizeHist`) para mejorar la legibilidad. |
| **Celdas fusionadas** | Post‑procesa el TSV para dividir celdas basándote en delimitadores conocidos o usa la bandera `merge_cells=False` si está disponible. |
| **PDFs de varias páginas** | Convierte cada página a una imagen primero (`pdf2image`) y ejecuta la canalización en un bucle. |

Estos ajustes mantienen tu flujo de trabajo **ocr table image python** robusto frente a material fuente variado.

---

## Script completo – Solución todo en uno

A continuación tienes el script completo, listo para ejecutar, que agrupa cada paso discutido. Guárdalo como `extract_table.py` y ejecuta `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de una imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cómo extraer tabla de una imagen usando Aspose.OCR para .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Cómo extraer texto de una imagen preparando rectángulos en OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}