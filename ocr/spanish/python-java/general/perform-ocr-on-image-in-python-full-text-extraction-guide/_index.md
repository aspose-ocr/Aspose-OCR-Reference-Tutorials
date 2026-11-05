---
category: general
date: 2026-06-19
description: Realiza OCR en una imagen usando la biblioteca OCR de Python. Aprende
  cómo detectar texto en una imagen, reconocer texto de un JPEG y extraer texto de
  una imagen escaneada de manera eficiente.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: es
og_description: Realiza OCR en imágenes con Python y extrae texto de archivos escaneados.
  Esta guía te lleva paso a paso por la carga de imágenes, la corrección de inclinación
  y el reconocimiento de texto.
og_title: Realiza OCR en una imagen con Python – Guía completa de extracción de texto
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Realizar OCR en una imagen con Python – Guía completa de extracción de texto
url: /es/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR en Imagen con Python – Guía Completa de Extracción de Texto

¿Alguna vez necesitaste **realizar OCR en imagen** archivos pero te encontraste con un muro porque el código parecía críptico? No eres el único. Ya sea que estés convirtiendo una pila de recibos escaneados en PDFs buscables o extrayendo subtítulos de un JPEG para un proyecto de ciencia de datos, la capacidad de reconocer texto de JPEGs y otros formatos es una habilidad imprescindible para cualquier desarrollador hoy.

En este tutorial recorreremos un ejemplo completo y ejecutable que te muestra cómo **detect text from image** archivos, **extract text from scanned image** documentos, e incluso **load image for OCR** en solo unas cuantas líneas. Al final, tendrás un fragmento sólido y listo para producción que puedes insertar en tus propios proyectos—sin importaciones faltantes, sin atajos vagos de “ver docs”.

## Lo Que Construirás

- Un pequeño script de Python que crea un motor OCR, habilita auto‑deskew, carga un JPEG (o cualquier formato compatible) y muestra el texto reconocido.  
- Explicaciones de **por qué** cada configuración importa, no solo de **cómo** escribirla.  
- Consejos para manejar PDFs de varias páginas, idiomas no ingleses y trampas comunes como escaneos borrosos.

### Requisitos Previos

- Python 3.8+ instalado (el ejemplo usa el paquete `ocr` disponible vía `pip install ocr-lib` – reemplaza con el nombre real de tu biblioteca).  
- Familiaridad básica con funciones de Python y entornos virtuales.  
- Un archivo de imagen (JPEG, PNG, TIFF) que quieras procesar; usaremos `skewed_page.jpg` como ejemplo.

> **Pro tip:** Si estás en Windows, ejecuta tu terminal como Administrador al instalar la biblioteca OCR para evitar problemas de permisos.

## Realizar OCR en Imagen – Configuración y Preparación

Lo primero que necesitas es una instancia limpia del motor OCR. Piensa en ella como el cerebro detrás de la operación; sin una configuración adecuada, incluso la imagen más nítida devolverá basura.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Por qué esto importa:**  
Configurar `engine.language` reduce el conjunto de caracteres que el motor OCR espera, aumentando drásticamente la precisión. Si omites esto, el motor intentará adivinar, a menudo malinterpretando palabras simples.

## Habilitar Deskew Automático – Corregir Escaneos Inclinados

Las páginas escaneadas rara vez están perfectamente planas. Una ligera inclinación puede desorientar la segmentación de caracteres, convirtiendo “Hello” en “H3llo”. La bandera `auto_deskew` hace el trabajo pesado por ti.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Caso límite:** Si sabes que tus imágenes ya están rectas, desactivar el deskew puede ahorrar unos milisegundos de tiempo de procesamiento—útil cuando manejas miles de páginas en un trabajo por lotes.

## Cargar Imagen para OCR – Compatibilidad con JPEG, PNG, TIFF

Ahora realmente **load image for OCR**. El método `ocr.Image.load` es flexible; acepta una ruta a cualquier formato raster compatible.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Por qué este paso es crucial:** La biblioteca lee el archivo a un bitmap interno, aplicando cualquier conversión de espacio de color necesaria. Omitir esto y pasar un flujo de bytes crudo provocaría un `FileNotFoundError` o, peor aún, produciría resultados vacíos sin advertencia.

Si necesitas **recognize text from JPEG** específicamente, solo asegúrate de que la extensión del archivo sea `.jpeg` o `.jpg`. La misma llamada funciona para PNG (`.png`) o TIFF (`.tif`) sin modificaciones.

## Realizar OCR en Imagen – Ejecutando el Motor

Con el motor preparado y la imagen en memoria, es momento de **perform OCR on image** datos. Esta única línea hace el trabajo pesado: pre‑procesamiento, segmentación, clasificación y ensamblado de texto.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**¿Qué ocurre bajo el capó?**  
- El motor aplica la transformación de deskew (si está habilitada).  
- Ejecuta una red neuronal o backend Tesseract para identificar caracteres.  
- Finalmente, une los caracteres en palabras y líneas, devolviendo un objeto `result` rico.

## Extraer Texto de Imagen Escaneada – Mostrar los Resultados

El paso final es **extract text from scanned image** y mostrarlo. El atributo `result.text` contiene la representación de texto plano.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Una salida típica se ve así:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Si el motor OCR no encuentra ningún carácter, `result.text` será una cadena vacía. En ese caso, verifica la calidad de la imagen o considera ajustar la propiedad `engine.confidence_threshold` (si tu biblioteca lo soporta).

## Manejo de Variaciones Comunes

### Reconocer Texto de JPEG vs PNG

Ambos formatos son compatibles, pero la compresión JPEG puede introducir artefactos que confunden al motor. Si notas errores frecuentes de reconocimiento, intenta convertir el JPEG a PNG primero:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Detectar Texto de Imagen con Múltiples Idiomas

Si tu documento mezcla inglés y español, establece un modo multilingüe:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

El motor considerará ambos alfabetos durante el reconocimiento.

### Extraer Texto de PDFs Escaneados

Para PDFs, primero debes rasterizar cada página en una imagen. Bibliotecas como `pdf2image` hacen esto sin complicaciones:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

## Ejemplo Completo Funcional

A continuación tienes el script completo que puedes copiar‑pegar en un archivo `ocr_demo.py`. Incluye manejo de errores y un pequeño ayudante para medir el tiempo de ejecución.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Salida esperada** (asumiendo un escaneo claro):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

## Preguntas Frecuentes

**Q: ¿Puedo ejecutar esto en un servidor sin interfaz gráfica?**  
A: Absolutamente. La biblioteca funciona sin GUI; solo asegúrate de que los binarios nativos necesarios (p. ej., Tesseract) estén instalados en el servidor.

**Q: ¿Qué pasa si la imagen está borrosa?**  
A: Considera añadir un filtro de enfoque antes de `engine.recognize`. Muchas bibliotecas OCR exponen `image_preprocessing.sharpen = True` o puedes usar `cv2.GaussianBlur` de OpenCV en sentido inverso.

**Q: ¿El script soporta procesamiento por lotes?**  
A: Sí. Envuelve `perform_ocr` en un bucle sobre una lista de rutas de archivo,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}