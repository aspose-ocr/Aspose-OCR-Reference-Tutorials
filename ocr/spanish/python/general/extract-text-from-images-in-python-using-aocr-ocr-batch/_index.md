---
category: general
date: 2026-06-25
description: Extrae texto de imágenes con la biblioteca aocr de Python – aprende OCR
  por lotes, establece el modo de reconocimiento impreso y agrega un postprocesador
  de IA.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: es
og_description: Extrae texto de imágenes usando la biblioteca Python aocr. Este tutorial
  muestra OCR por lotes, modo de reconocimiento de texto impreso y un postprocesador
  de IA opcional.
og_title: Extraer texto de imágenes en Python – Guía completa por lotes de OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Extraer texto de imágenes en Python usando aocr OCR por lotes
url: /es/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de imágenes en Python usando lote OCR aocr

¿Alguna vez necesitaste **extraer texto de imágenes** pero te sentiste abrumado por docenas de pequeños pasos? No eres el único. Ya sea que estés digitalizando formularios escaneados, extrayendo datos de recibos o construyendo un archivo searchable, obtener resultados de OCR fiables a escala puede sentirse como escalar una colina empinada.

¿La buena noticia? Con la **biblioteca aocr** puedes crear un **lote OCR de Python** en solo unas pocas líneas. En esta guía recorreremos la creación de un lote OCR, la carga de todas las imágenes compatibles desde una carpeta, la selección del **modo de reconocimiento printed** correcto, e incluso la incorporación de un **postprocesador AI** para ese impulso extra en precisión. Al final tendrás un script listo‑para‑ejecutar que extrae texto de imágenes y te indica cuánto se capturó por archivo.

## Lo que aprenderás

- Cómo instalar e importar el paquete `aocr`.
- Configurar un `OcrBatch` para manejar miles de archivos automáticamente.
- Elegir el modo de reconocimiento óptimo para documentos impresos.
- (Opcional) Conectar un post‑procesador AI para limpiar resultados ruidosos.
- Mostrar cada ruta de archivo junto con la longitud del texto extraído.
- Consejos para manejar casos límite como formatos no compatibles o páginas vacías.

### Requisitos previos

- Python 3.8 o superior instalado en tu máquina.  
- Familiaridad básica con scripting en Python (bucles, importaciones, etc.).  
- Acceso a una carpeta de imágenes escaneadas (PNG, JPG, TIFF, etc.).  

Si tienes eso, vamos a sumergirnos—no se requieren servicios externos.

## Paso 1: Instalar la biblioteca aocr

Lo primero. El paquete `aocr` no forma parte de la biblioteca estándar, así que tendrás que obtenerlo de PyPI.

```bash
pip install aocr
```

> **Consejo profesional:** Usa un entorno virtual (`python -m venv .venv`) para mantener las dependencias aisladas.  

Una vez instalado, puedes importar las clases principales.

```python
# core imports
import aocr
```

## Paso 2: Crear una instancia de OCR Batch

Un `OcrBatch` es la pieza clave que recorrerá tu directorio y llevará registro de cada archivo de imagen. Piensa en él como una cinta transportadora que alimenta imágenes al motor OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

En este punto el lote está vacío, pero lo llenaremos en el siguiente paso.

## Paso 3: Añadir todas las imágenes compatibles desde una carpeta (recursivamente)

Probablemente tienes una estructura de carpetas anidada—quizá una sub‑carpeta por cliente o por mes. El método `add_folder` recorre el árbol por ti, incorporando cada imagen que sabe leer.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Reemplaza `"YOUR_DIRECTORY/scanned_forms/"` con la ruta real en tu sistema. Después de esta llamada `ocr_batch.file_paths` contiene una lista de nombres de archivo absolutos, y el lote sabe exactamente cuántos elementos procesará.

## Paso 4: Elegir el modo de reconocimiento para texto impreso

El motor `aocr` soporta varios modos (handwritten, printed, mixed). Como estamos trabajando con formularios limpios e impresos, establece el modo en consecuencia. Esta pequeña bandera puede mejorar dramáticamente la precisión porque el motor omite las heurísticas pesadas necesarias para scripts cursivos.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Por qué importa:** El texto impreso tiene líneas base y formas de caracteres consistentes, lo que permite al modelo OCR aplicar diccionarios de caracteres más estrictos. Si dejas el modo en “auto” podrías obtener ruido extra en escaneos de baja resolución.

## Paso 5: (Opcional) Adjuntar un post‑procesador AI

Si tus escaneos presentan desenfoque, bajo contraste o fuentes inusuales, un post‑procesador AI puede limpiar la salida OCR cruda antes de entregarla a los sistemas posteriores. El método `set_ai_postprocessor` espera un objeto que implemente una interfaz `process(text: str) -> str`.

A continuación se muestra un ejemplo mínimo usando una clase ficticia `SimpleCleaner`. En la práctica podrías conectar un transformer de HuggingFace, un modelo de lenguaje personalizado o incluso un corrector ortográfico basado en reglas.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Si omites este paso, el lote simplemente devolverá las cadenas OCR crudas.

## Paso 6: Ejecutar OCR en todo el lote y recopilar resultados

Ahora comienza el trabajo pesado. El método `run` itera sobre cada archivo, ejecuta el motor OCR, canaliza la salida a través del post‑procesador AI opcional y devuelve una lista de cadenas—una por imagen.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Como el método devuelve una lista Python simple, puedes tratarla como cualquier otra colección—almacenarla, escribirla a un CSV o insertarla en una base de datos.

## Paso 7: Mostrar cada ruta de archivo con la longitud del texto extraído

Una rápida verificación de sentido común es imprimir cuántos caracteres se extrajeron de cada archivo. Si una página está en blanco o el OCR falló, verás una longitud de `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

La salida típica se ve así:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Ver una bandera `0` te indica al instante qué archivos necesitan una segunda revisión (quizá estén corruptos o no sean una imagen).

## Manejo de casos límite comunes

### 1. Tipos de archivo no compatibles

`aocr` omite silenciosamente los archivos que no puede decodificar. Si sospechas que tienes PDFs o BMPs mezclados, filtéralos antes:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Lotes grandes y consumo de memoria

Ejecutar miles de escaneos de alta resolución puede inflar el uso de memoria. Mitiga esto procesando en bloques:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Páginas vacías o de bajo contraste

Si una página produce menos de 10 caracteres, podrías querer marcarla para revisión manual:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Ejemplo completo en funcionamiento

Uniendo todo, aquí tienes un script que puedes copiar‑pegar y ejecutar de inmediato. Guárdalo como `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Salida esperada** (truncada por brevedad):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Ejecuta con:

```bash
python batch_ocr.py
```

Si todo está configurado correctamente, verás una línea por cada imagen, cada una informando el recuento de caracteres del texto extraído.

## Preguntas frecuentes

**Q: ¿Esto funciona con PDFs?**  
A: No directamente. `aocr` solo maneja imágenes raster. Convierte PDFs a PNG/TIFF primero (p.ej., usando `pdf2image`).

**Q: ¿Puedo cambiar el modo de reconocimiento a manuscrito?**  
A: Por supuesto—simplemente reemplaza `aocr.RecognitionMode.PRINTED` por `aocr.RecognitionMode.HANDWRITTEN`. Espera un tiempo de ejecución más lento pero mejores resultados en notas cursivas.

**Q: ¿Qué pasa si necesito soporte multilingüe?**  
A: La biblioteca incluye paquetes de idioma. Instala el módulo de idioma deseado (`pip install aocr-lang-fr` para francés, etc.) y establece `ocr_batch.language = "fr"` antes de ejecutar.

## Próximos pasos y temas relacionados

- **Procesamiento paralelo:** Envuelve la ejecución del lote en un `concurrent.futures.ThreadPoolExecutor` para utilizar múltiples núcleos de CPU.  
- **Almacenamiento de resultados:** Escribe `ocr_results` a un CSV o base de datos SQLite para análisis posteriores.  
- **Integración con IA en la nube:** Sustituye `SimpleCleaner` por un modelo transformer de HuggingFace para corrección ortográfica de última generación.  
- **Ajuste fino de aocr:** Si tienes un conjunto de fuentes personalizado, explora `aocr.Trainer` para mejorar la precisión del modo impreso.  

---

Eso es todo—ahora tienes una base sólida


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraer texto de imágenes usando operación OCR en carpetas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Cómo procesar OCR por lotes de imágenes con lista en Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}