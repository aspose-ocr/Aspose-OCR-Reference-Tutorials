---
category: general
date: 2026-06-22
description: Obtén las coordenadas del cuadro delimitador de imágenes usando Python.
  Aprende cómo extraer texto de una imagen con Python, Aspose OCR y análisis de JSON
  en minutos.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: es
og_description: Obtén las coordenadas de la caja delimitadora de imágenes usando Python.
  Esta guía muestra cómo extraer texto de una imagen con Python usando Aspose OCR
  y analizar los datos de diseño.
og_title: Obtén las coordenadas del cuadro delimitador del OCR en Python – Tutorial
  completo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Obtén las coordenadas del cuadro delimitador del OCR en Python – Guía completa
url: /es/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtén las coordenadas del cuadro delimitador (Bounding Box) desde OCR en Python – Guía completa

¿Alguna vez necesitaste **obtener las coordenadas del cuadro delimitador** para cada palabra en una factura escaneada, pero no sabías por dónde empezar? No eres el único. En muchos proyectos de automatización, tienes que localizar texto en una imagen para resaltarlo, censurarlo o enviarlo a análisis posteriores. ¿La buena noticia? Con unas pocas líneas de Python y Aspose.OCR puedes extraer tanto el texto **como** su posición exacta en una sola pasada.

En este tutorial recorreremos un ejemplo práctico que muestra cómo **extraer texto de una imagen al estilo python**, luego profundizaremos en los datos de diseño JSON para obtener esos cuadros delimitadores. Sin rodeos, solo un script funcional, explicaciones de por qué cada paso es importante y consejos para evitar errores comunes.

---

## Lo que construirás

Al final de esta guía tendrás un script de Python listo‑para‑ejecutar que:

1. Carga una imagen (p. ej., un PNG de factura) en Aspose OCR.  
2. Configura el motor para emitir información de diseño en JSON.  
3. Analiza el JSON a un diccionario de Python.  
4. Recorre cada palabra reconocida, imprimiendo su texto **y** sus coordenadas del cuadro delimitador.

También verás cómo adaptar el código para PDFs de varias páginas, diferentes formatos de imagen y sistemas de coordenadas personalizados.

### Requisitos previos

- Python 3.8+ instalado en tu máquina.  
- Una licencia activa de Aspose.OCR para Python o una prueba gratuita (la biblioteca funciona sin licencia pero añade una marca de agua).  
- `pip install aspose-ocr` (el nombre del paquete en PyPI).  
- Una imagen de ejemplo llamada `invoice.png` colocada en una carpeta a la que puedas referenciar.

Eso es todo—sin frameworks pesados, sin servicios externos. Vamos al código.

---

## Paso 1: Instala e importa las bibliotecas requeridas

Primero, asegúrate de que el paquete Aspose OCR y el módulo incorporado `json` estén disponibles. El módulo `json` viene con Python, así que solo necesitamos instalar Aspose.

```bash
pip install aspose-ocr
```

Ahora impórtalos en tu script:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Por qué es importante:** Importar `aspose.ocr` te da acceso al motor OCR de alto rendimiento, mientras que `json` te permite convertir la cadena de diseño cruda en un diccionario nativo de Python para una fácil navegación.

---

## Paso 2: Crea el motor OCR y carga tu imagen

El motor es el corazón del proceso. Lo instancias y luego le indicas la imagen que deseas escanear.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Consejo profesional:** Reemplaza `"YOUR_DIRECTORY/invoice.png"` con una ruta absoluta o relativa que apunte a tu archivo real. Si el archivo no se encuentra, Aspose lanzará un `FileNotFoundError`, así que verifica la ortografía.

---

## Paso 3: Configura el motor para que devuelva datos de diseño en JSON

Aspose OCR puede devolver texto plano, JSON solo de OCR o un JSON completo de diseño que incluye coordenadas para palabras, líneas e incluso caracteres individuales. Para **obtener coordenadas del cuadro delimitador**, necesitamos el JSON de diseño.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **¿Por qué JSON?** JSON es independiente del lenguaje, legible por humanos y se mapea limpiamente a diccionarios de Python. El JSON de diseño contiene un arreglo `"words"` donde cada entrada guarda el texto y un arreglo `boundingBox` de ocho números (los cuatro puntos de la esquina).

---

## Paso 4: Ejecuta el reconocimiento y captura la cadena JSON cruda

Ahora ejecutamos realmente el OCR. El método `recognize()` devuelve un objeto `OcrResult`, del cual podemos extraer la cadena JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Si imprimes `layout_json` verás algo como:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Caso límite:** Algunas imágenes pueden producir arreglos `"words"` vacíos si el motor OCR no logra detectar texto. En ese caso, verifica la calidad de la imagen (contraste, resolución) antes de continuar.

---

## Paso 5: Analiza el JSON a un diccionario de Python

Trabajar con estructuras nativas de Python es mucho más sencillo que manipular cadenas. Usa la función `json.loads()` para convertir la cadena.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Ahora `layout_data["words"]` es una lista de diccionarios, cada uno representando una palabra y su cuadro delimitador.

---

## Paso 6: Recorre las palabras y **obtén las coordenadas del cuadro delimitador**

Este es el núcleo de nuestro tutorial: iterar sobre cada palabra, extraer el texto y imprimir las coordenadas. Aquí es donde **obtenemos las coordenadas del cuadro delimitador**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Salida de ejemplo** (tus números serán diferentes según la imagen):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **¿Por qué el formato de ocho puntos?** Las cuatro esquinas (superior‑izquierda, superior‑derecha, inferior‑derecha, inferior‑izquierda) te permiten dibujar un polígono alrededor de la palabra, incluso si el texto está inclinado. Si solo necesitas un rectángulo simple, puedes calcular `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` y `height = max(y…) - y_min`.

---

## Mejoras opcionales

### 1. Convertir cuadros delimitadores a rectángulos simples

Si tu herramienta posterior espera `(x, y, width, height)` en lugar de ocho puntos, agrega un ayudante:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Manejar PDFs de varias páginas

Aspose OCR puede aceptar flujos PDF. Reemplaza la línea de carga de imagen con:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Itera `set_page_number` para cada página, recopilando coordenadas por página.

### 3. Visualizar los cuadros delimitadores

Si deseas ver los cuadros dibujados sobre la imagen original, usa Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Ahora verás contornos rojos alrededor de cada palabra reconocida—perfecto para depuración o superposiciones en UI.

---

## Preguntas frecuentes y trampas comunes

- **¿Qué pasa si el JSON es enorme?** Para documentos grandes, considera transmitir el JSON o procesar página por página para mantener bajo el uso de memoria.  
- **¿Por qué faltan algunas palabras?** Bajo contraste o texto manuscrito suele confundir a los motores OCR. Pre‑procesa la imagen (aumenta contraste, binariza) antes de enviarla a Aspose.  
- **¿Puedo obtener coordenadas a nivel de carácter?** Sí—establece `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` para recibir un arreglo `"characters"` con su propio `boundingBox`.  
- **¿El sistema de coordenadas es cero‑basado?** Exactamente. (0, 0) es la esquina superior izquierda de la imagen.

---

## Script completo – Listo para copiar y ejecutar

A continuación tienes el ejemplo completo y ejecutable que combina todos los pasos. Guárdalo como `extract_bboxes.py` y ejecuta `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}