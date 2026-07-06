---
category: general
date: 2026-01-12
description: Cómo realizar OCR de forma rápida y precisa. Aprende a ejecutar OCR en
  un documento, extraer texto de un TIFF, cargar una imagen para OCR y establecer
  el idioma de OCR en Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: es
og_description: Cómo realizar OCR en Python. Este tutorial te muestra cómo ejecutar
  OCR en un documento, extraer texto de un tiff, cargar una imagen para OCR y establecer
  el idioma del OCR.
og_title: Cómo realizar OCR en un documento TIFF – Guía completa
tags:
- OCR
- Python
- Image Processing
title: Cómo realizar OCR en un documento TIFF – Guía paso a paso
url: /es/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR en un documento TIFF – Guía completa

¿Alguna vez te has preguntado **cómo realizar OCR** en un archivo TIFF escaneado sin pasar horas buscando la biblioteca adecuada? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan extraer texto de imágenes TIFF, especialmente cuando el rendimiento y la configuración de idioma son importantes.

En este tutorial recorreremos todo lo que necesitas saber: desde instalar el paquete OCR, cargar la imagen para OCR, establecer el idioma del OCR, hasta **ejecutar OCR en el documento** y obtener texto limpio. Al final tendrás un script listo‑para‑ejecutar que podrás incorporar en cualquier proyecto.

> **Consejo:** Aunque el ejemplo usa un módulo genérico `ocr`, los mismos conceptos se aplican a Tesseract, EasyOCR o cualquier motor OCR moderno que exponga una API de Python.

---

## Lo que necesitarás

- Python 3.8+ (cualquier versión reciente funciona)
- Una biblioteca OCR que proporcione una clase `OcrEngine` (el ejemplo usa un paquete ficticio `ocr`; reemplázalo por el que realmente uses)
- Un archivo TIFF multipágina que quieras procesar (lo llamaremos `big_document.tif`)
- Una máquina con al menos 4 núcleos de CPU si planeas establecer el número de hilos

Sin servicios externos, sin claves de nube — solo código local que se ejecuta en segundos.

---

![cómo realizar OCR en un documento TIFF – vista previa del texto extraído](/images/ocr-example.png "cómo realizar OCR en un documento TIFF")

*Texto alternativo de la imagen: cómo realizar OCR en un documento TIFF – vista previa del texto extraído.*

---

## Paso 1: Instalar e importar la biblioteca OCR

Lo primero: obtener la biblioteca en tu máquina. La mayoría de los paquetes OCR están en PyPI, así que un simple `pip install` basta.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Ahora importa las clases que necesitarás. Si usas Tesseract, la línea de importación será diferente, pero el resto del código permanece igual.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Por qué importa:* Importar los símbolos correctos desde el principio evita colisiones de espacio de nombres más adelante y hace que el script sea más fácil de leer.

---

## Paso 2: Crear y configurar el motor OCR (establecer idioma OCR)

Configurar el motor es donde **estableces el idioma OCR** para un reconocimiento preciso. El inglés es el predeterminado, pero puedes cambiar a francés, alemán o incluso modo multilingüe con una sola línea.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **¿Por qué 4 hilos?** La mayoría de los portátiles modernos tienen al menos cuatro núcleos, y limitar el número de hilos evita que el proceso OCR consuma toda la máquina — especialmente útil cuando el script se ejecuta en un servidor compartido.

Si necesitas otro idioma, simplemente reemplaza `ocr.Language.ENGLISH` por `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, etc.

---

## Paso 3: Cargar la imagen para OCR (Load Image for OCR)

Ahora **cargamos la imagen para OCR**. El método `Image.load` lee el archivo TIFF en memoria, manejando documentos multipágina automáticamente.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Caso límite:* Si el archivo es muy grande, podrías quedarte sin RAM. En ese escenario, considera cargar una página a la vez con `Image.load_page(page_number)` (si la biblioteca lo soporta).

---

## Paso 4: Ejecutar OCR en el documento

Con el motor listo y la imagen cargada, es momento de **ejecutar OCR en el documento**. El método `process` realiza el trabajo pesado y devuelve un objeto de resultado.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Detrás de escena, el motor divide la imagen en bloques de texto, ejecuta el modelo de reconocimiento y une los resultados. La llamada es bloqueante, lo que significa que el script espera hasta que todo el TIFF se procese — perfecto para trabajos por lotes.

---

## Paso 5: Extraer texto del TIFF y verificar la salida

Finalmente, **extraemos texto del TIFF** accediendo al atributo `text` del resultado. Imprimamos los primeros 200 caracteres como una rápida comprobación de sanidad.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Salida esperada (ejemplo):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Si necesitas el texto completo, simplemente usa `ocr_result.text`. Para procesamiento posterior quizá quieras escribirlo en un archivo `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Ejemplo completo y funcional

Juntando todo, aquí tienes un script listo‑para‑ejecutar. Sustituye el nombre del paquete ficticio por el que realmente instalaste.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Ejecuta el script con:

```bash
python ocr_tiff_example.py
```

Deberías ver una vista previa impresa en la consola y un archivo llamado `extracted_text.txt` que contiene la transcripción completa.

---

## Preguntas frecuentes y casos límite

- **¿Qué pasa si el TIFF contiene varias páginas?**  
  La mayoría de los motores OCR tratan cada página como una imagen separada internamente. `ocr_result.text` incluirá un salto de línea entre páginas. Si necesitas manejar cada página por separado, itera con `Image.load_page(page_number)`.

- **¿Puedo procesar un PNG o JPEG en lugar de TIFF?**  
  Por supuesto. El método `Image.load` suele aceptar cualquier formato soportado por Pillow o la biblioteca subyacente. Sólo cambia la extensión del archivo.

- **Mi texto sale distorsionado — ¿debería cambiar el idioma?**  
  Sí. El paso **establecer idioma OCR** es crucial para documentos que no están en inglés. Asegúrate de que el paquete de idioma esté instalado (por ejemplo, `tesseract‑lang‑fra` para francés).

- **¿Se me agota la memoria?**  
  Reduce `set_memory_limit` o procesa las páginas una a una. Algunos motores también permiten reducir la escala de la imagen antes del reconocimiento.

---

## Conclusión

Ahí lo tienes: una guía concisa y totalmente funcional sobre **cómo realizar OCR** en un archivo TIFF usando Python. Cubrimos todo, desde la instalación de la biblioteca, la configuración del motor (incluyendo **establecer idioma OCR**), **cargar la imagen para OCR**, **ejecutar OCR en el documento**, y finalmente **extraer texto del TIFF**.  

Siéntete libre de experimentar: ajusta el número de hilos, cambia de idioma o alimenta la salida OCR a una canalización de procesamiento de lenguaje natural. El cielo es el límite una vez que domines los conceptos básicos.

¿Tienes más preguntas? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}