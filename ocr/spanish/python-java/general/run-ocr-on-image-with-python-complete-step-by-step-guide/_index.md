---
category: general
date: 2026-06-06
description: Ejecuta OCR en una imagen usando Python y observa los puntajes de confianza.
  Aprende cómo filtrar palabras de baja confianza, establecer umbrales y manejar casos
  límite.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: es
og_description: Ejecuta OCR en una imagen con Python, inspecciona los niveles de confianza
  y filtra las palabras de baja confianza. Este tutorial te guía a través de un ejemplo
  completo y ejecutable.
og_title: Ejecuta OCR en una imagen con Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Ejecutar OCR en una imagen con Python – Guía completa paso a paso
url: /es/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en Imagen con Python – Guía Completa Paso a Paso

¿Alguna vez necesitaste **ejecutar OCR en imagen** pero no estabas seguro de cómo obtener texto fiable de ella? No estás solo: muchos desarrolladores se topan con el mismo problema cuando las palabras extraídas se ven temblorosas y la puntuación de confianza es un misterio.  

En esta guía nos sumergiremos directamente en una solución funcional: verás cómo ejecutar OCR en imagen, leer la confianza general y extraer cualquier palabra de baja confianza que pueda requerir revisión manual. Al final tendrás un script reutilizable, comprenderás por qué cada línea es importante y sabrás cómo ajustar el umbral de confianza para tus propios proyectos.

## Qué Cubre este Tutorial

Recorreremos todo el flujo de trabajo—desde cargar una imagen hasta imprimir un informe ordenado de palabras que quedaron por debajo del 80 % de confianza. En el camino hablaremos de:

* Elegir un motor OCR sólido (usaremos **EasyOCR**, una popular biblioteca OCR para Python)  
* Interpretar el atributo `confidence` que devuelve cada resultado OCR  
* Filtrar palabras con un **umbral de confianza OCR** personalizado  
* Extender el script para procesamiento por lotes o motores alternativos como **pytesseract**  

No se requiere experiencia previa en OCR, solo una familiaridad básica con Python y un entorno de trabajo (se recomienda Python 3.9+).  

¿Listo para convertir capturas de pantalla borrosas en texto limpio y buscable? Vamos a comenzar.

---

## ## Cómo Ejecutar OCR en Imagen con Python

El corazón del tutorial es un fragmento de tres pasos que refleja el código que ya viste. A continuación desglosaremos cada línea, explicaremos el porqué y luego te daremos un script completo listo para copiar y pegar.

### Paso 1: Instalar e Importar el Motor OCR

Primero, asegúrate de que la biblioteca OCR esté disponible. **EasyOCR** funciona listo para usar con muchos idiomas y te brinda una puntuación de confianza por palabra.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*¿Por qué EasyOCR?* Incluye un modelo de deep‑learning entrenado con conjuntos de datos diversos, por lo que típicamente obtienes valores de confianza más altos que con el motor más antiguo Tesseract, especialmente en imágenes de calidad mixta.

> **Consejo profesional:** Si trabajas en un entorno con recursos limitados (p. ej., un contenedor Docker pequeño), `pytesseract` podría ser más liviano, pero perderás parte de la precisión moderna que ofrece EasyOCR.

### Paso 2: Ejecutar OCR en la Imagen

Ahora realmente **ejecutamos OCR en imagen**. El método `recognize_image` del ejemplo original se reemplaza con la llamada `readtext` de EasyOCR, que devuelve una lista de tuplas `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Cada entrada en `ocr_results` se ve así:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

El tercer elemento (`0.92` en el ejemplo) es la puntuación de confianza, que varía de 0 a 1.

### Paso 3: Resumir la Confianza General

A diferencia del fragmento anterior que imprimía un solo atributo `confidence`, EasyOCR brinda una confianza por palabra. Para obtener una visión general, promediaremos esas puntuaciones:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*¿Por qué promediar?* Te da una rápida comprobación de salud—si la confianza general está por debajo, digamos, del 70 %, probablemente necesites mejorar la imagen (mejor iluminación, pre‑procesamiento, etc.).

### Paso 4: Listar Palabras de Baja Confianza

Ahora llega la parte que responde directamente al requisito de “listar palabras cuya confianza esté por debajo del umbral deseado”. Estableceremos un **umbral de confianza OCR** de 0.80 (80 %) por defecto, pero puedes ajustarlo.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

El bucle imprime cada palabra que no alcanzó el umbral, junto con su porcentaje de confianza. Este es el análogo exacto del bucle original `for recognized_word in recognition_result.words`, pero ahora funciona con el formato de salida de EasyOCR.

---

## ## Comprendiendo las Puntuaciones de Confianza de OCR

La confianza no es un número mágico; es la estimación del modelo sobre cuán seguro está respecto a una transcripción particular. Ten en cuenta lo siguiente:

| Situación | Confianza Típica | Qué Hacer |
|-----------|-------------------|------------|
| Escaneo claro y de alta resolución | 0.95 – 1.00 | No se necesita trabajo adicional |
| Ligeramente borroso o iluminación desigual | 0.80 – 0.94 | Considera un pre‑procesamiento leve (aumento de contraste) |
| Ruido intenso, texto rotado | < 0.70 | Aplica pre‑procesamiento (deskew, denoise) o cambia a otro motor OCR |

> **Cuidado:** Algunos idiomas (p. ej., escritura cursiva) naturalmente producen puntuaciones más bajas. Ajusta el umbral en consecuencia.

### Casos Límite y Variaciones

1. **Procesamiento por Lotes** – Si necesitas **ejecutar OCR en imagen** en bloque, envuelve la lógica anterior en un bucle que itere sobre un directorio.  
2. **Múltiples Idiomas** – Pasa una lista como `['en', 'fr']` a `easyocr.Reader` y el motor detectará ambos.  
3. **Motores Alternativos** – ¿Quieres probar **pytesseract**? Sustituye el bloque del lector por:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Luego tendrás que agregar las confidencias por carácter en valores por palabra—un poco más de trabajo pero factible.

4. **Trucos de Pre‑procesamiento** – Aplicar filtros de OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) puede aumentar la confianza en escaneos ruidosos.  

---

## ## Script Completo y Listo para Ejecutar

A continuación tienes el archivo Python completo que puedes incorporar a tu proyecto. Guárdalo como `ocr_report.py` y ejecuta `python ocr_report.py`. Asegúrate de que la ruta de la imagen apunte a un archivo real.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Salida esperada** (tus números variarán):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Si cada palabra supera el 80 % verás el mensaje amistoso “All words meet the confidence threshold.” en su lugar.

---

## ## Preguntas Frecuentes (FAQ)

**P: ¿Esto funciona con PDFs?**  
R: No directamente. Convierte cada página del PDF a una imagen primero (p. ej., con `pdf2image`) y luego alimenta el PNG/JPEG al script.

**P: Mis números de confianza son todos bajos—¿qué puedo hacer?**  
R: Prueba el pre‑procesamiento de la imagen: aumenta el contraste, elimina el ruido de fondo o rota la imagen a una línea base horizontal. EasyOCR también acepta un parámetro `contrast_ths` que puedes ajustar.

**P: ¿Puedo exportar los resultados a CSV?**  
R: Por supuesto. Después del bucle de baja confianza, escribe `ocr_results` a un `csv.DictWriter` donde cada fila contenga `text`, `confidence` y las coordenadas del cuadro delimitador.

**P: ¿Existe una versión acelerada por GPU?**  
R: EasyOCR usa CUDA automáticamente si hay una GPU compatible y PyTorch instalado. Verifica con `torch.cuda.is_available()` antes de ejecutar el script.

---

## Conclusión

Acabamos de **ejecutar OCR en imagen** usando Python, inspeccionamos la confianza general y aislamos cualquier palabra de baja confianza que necesite revisión manual.

## ¿Qué Deberías Aprender a Continuar?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye código completo y ejemplos paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}