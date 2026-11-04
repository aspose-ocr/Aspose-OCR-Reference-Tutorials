---
category: general
date: 2026-06-28
description: 'Cómo hacer OCR por lotes en Python: extraer texto de imágenes y convertir
  páginas escaneadas a texto usando procesamiento OCR por lotes.'
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: es
og_description: Aprende a realizar OCR por lotes en Python, extraer texto de imágenes
  y convertir páginas escaneadas a texto con un procesamiento de OCR por lotes eficiente.
og_title: Cómo realizar OCR por lotes en Python – Guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Cómo realizar OCR por lotes en Python – Guía completa para extraer texto de
  imágenes
url: /es/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo hacer OCR por lotes en Python – Guía completa para extraer texto de imágenes

Si te preguntas **cómo hacer OCR por lotes en Python**, estás en el lugar correcto. Este tutorial te muestra una forma rápida de **extraer texto de imágenes** y **convertir páginas escaneadas a texto** usando una única instancia del motor OCR. No más copiar‑pegar archivo por archivo—deja que el código haga el trabajo pesado.

Recorreremos todo lo que necesitas: instalar la biblioteca, cargar una carpeta completa de escaneos, ejecutar el procesamiento OCR por lotes y manejar los resultados de forma elegante. Al final tendrás un script reutilizable que convierte una pila de PNG o JPEG en archivos de texto buscables en segundos.

## Lo que necesitarás

* Python 3.9+ instalado (el código también funciona en 3.8, pero 3.9+ te brinda las funciones de tipado más recientes).
* Una biblioteca OCR moderna—aquí usamos **Aspose.OCR for Python via .NET**, que expone la clase `OcrEngine` mostrada en el fragmento original.  
  ```bash
  pip install aspose-ocr
  ```
* Una carpeta con páginas escaneadas (`page1.png`, `page2.png`, …). Cualquier formato que Pillow pueda abrir funcionará, así que PDFs, TIFF o BMP también son válidos.
* Un poco de curiosidad—si nunca has automatizado la conversión de imagen a texto, estás a punto de ver por qué el OCR por lotes es un cambio de juego.

> **Consejo profesional:** Si prefieres una biblioteca puramente Python, reemplaza `OcrEngine` por `pytesseract.image_to_string`. La lógica circundante permanece idéntica.

## Cómo hacer OCR por lotes en Python – Guía paso a paso

A continuación se muestra el script completo y ejecutable. Cada línea está comentada para que puedas ver *por qué* cada parte es importante, no solo *qué* hace.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Salida esperada

Ejecutar el script contra una carpeta con tres escaneos PNG produce algo como:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

La vista previa muestra los primeros 200 caracteres de cada página, y el texto completo se guarda en el directorio `ocr_output`.

## Extraer texto de imágenes usando un solo motor

¿Por qué creamos **un** `OcrEngine` y lo reutilizamos? Instanciar el motor puede ser costoso porque carga paquetes de idiomas y DLLs nativas. Al compartir la misma instancia en todo el lote, tú:

* **Ahorra memoria** – solo un conjunto de recursos vive en RAM.
* **Acelera la velocidad** – el motor permanece activo, evitando inicializaciones repetidas.
* **Mantiene la consistencia** – los mismos ajustes de reconocimiento se aplican a cada página, lo cual es esencial cuando deseas **extraer texto de imágenes** que comparten el mismo diseño.

Si necesitas ajustar el reconocimiento (p.ej., habilitar la corrección ortográfica o cambiar el idioma), hazlo *antes* de llamar a `recognize_batch`. Todas las páginas subsecuentes heredarán esos ajustes automáticamente.

## Convertir páginas escaneadas a texto de manera eficiente

El núcleo del problema—**convertir páginas escaneadas a texto**—se resuelve con `engine.recognize_batch(images)`. Internamente la biblioteca procesa cada imagen en un pool de hilos en segundo plano, por lo que obtienes una escala casi lineal en máquinas multinúcleo. Algunas cosas a tener en cuenta:

* **La calidad de la imagen importa** – 300 dpi o más brinda los mejores resultados. Si tus escaneos son de baja resolución, considera aumentar la escala con Pillow antes de enviarlos al motor.
* **Color vs. escala de grises** – los motores OCR suelen trabajar más rápido en escala de grises de 8 bits. Puedes añadir un paso de preprocesamiento:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Soporte de idiomas** – Aspose.OCR admite más de 40 idiomas. Configura `engine.language = "eng"` o `"fra"` antes de la llamada por lotes si no trabajas con inglés.

## Mejores prácticas para el procesamiento OCR por lotes

Aunque el código anterior ya es conciso, el OCR por lotes de nivel producción a menudo requiere algunas salvaguardas adicionales:

| Aspecto | Enfoque recomendado |
|---------|----------------------|
| **Lotes grandes ( > 500 archivos )** | Dividir en bloques de 100–200 imágenes para mantener una huella de memoria moderada. |
| **Archivos corruptos o no compatibles** | El ayudante `load_images` ya captura excepciones y registra una advertencia; también puedes escribir una alternativa para omitir o mover archivos dañados. |
| **Monitoreo de progreso** | Envuelve `recognize_batch` en un bucle que produzca resultados después de cada imagen si la biblioteca expone callbacks por imagen. |
| **Post‑procesamiento** | Ejecuta una corrección ortográfica o una limpieza con expresiones regulares en las cadenas resultantes para mejorar la buscabilidad posterior. |
| **Paralelismo** | Si tienes una configuración multinodo, distribuye carpetas entre los workers y fusiona los archivos `.txt` al final. |

Estos consejos te ayudan a escalar el **procesamiento OCR por lotes** de unas pocas páginas a miles sin que tu script se bloquee.

## Preguntas frecuentes

**Q: ¿Puedo usar esto con PDFs directamente?**  
A: Por supuesto. Convierte cada página PDF a una imagen primero (p.ej., usando `pdf2image`) y pasa la lista resultante a `recognize_batch`. El resto del flujo permanece sin cambios

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de una imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraer texto de imágenes usando la operación OCR en carpetas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Cómo extraer texto de archivos ZIP usando Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}