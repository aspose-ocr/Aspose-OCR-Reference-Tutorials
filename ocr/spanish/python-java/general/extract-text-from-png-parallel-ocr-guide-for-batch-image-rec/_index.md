---
category: general
date: 2026-03-18
description: Extraer texto de PNG usando Python y Aspose OCR. Aprende cómo cargar
  la imagen para OCR, ejecutar OCR en varios archivos y lograr OCR por lotes de imágenes
  con reconocimiento de imágenes en paralelo.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: es
og_description: Extrae texto de PNG con Aspose OCR en Python. Este tutorial muestra
  cómo cargar una imagen para OCR, procesar OCR en varios archivos y ejecutar OCR
  por lotes en imágenes utilizando reconocimiento de imágenes en paralelo.
og_title: Extraer texto de PNG – Guía de OCR paralela
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Extraer texto de PNG – Guía de OCR paralelo para reconocimiento de imágenes
  por lotes
url: /es/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de PNG – Guía de OCR paralelo para reconocimiento de imágenes por lotes

¿Alguna vez necesitaste **extraer texto de PNG** pero te quedaste atascado en el punto donde una sola imagen tarda una eternidad en procesarse? No estás solo. En muchos proyectos del mundo real —piensa en escáneres de facturas, digitalizadores de recibos o herramientas de archivo— la velocidad importa, y procesar cada PNG una a una simplemente no sirve.  

En esta guía recorreremos una solución completa y lista para ejecutar que **carga imagen para OCR**, ejecuta **ocr multiple files** en un modo de **batch OCR images**, y aprovecha el **reconocimiento de imágenes paralelo** con el módulo `threading` de Python. Al final tendrás un script que extrae texto de cualquier número de PNGs en segundos, no en minutos.

## Lo que necesitarás

- Python 3.8 o superior (la sintaxis mostrada también funciona en 3.10+).  
- El paquete Aspose OCR para Java/Python (`aspose-ocr`). Puedes instalarlo mediante `pip`.  
- Una carpeta con un puñado de archivos PNG que deseas procesar.  
- Una cantidad modesta de RAM —cada hilo mantiene una pequeña instancia del motor OCR, por lo que incluso una laptop puede lanzar decenas de workers.

Sin servicios externos, sin claves de nube y sin archivos de configuración misteriosos. Solo código Python puro que puedes copiar‑pegar y ejecutar.

## ¿Por qué extraer texto de PNG en paralelo?

Procesar un PNG es intensivo en CPU: el motor OCR ejecuta una serie de algoritmos de análisis de imágenes que consumen datos de píxeles. Cuando tienes diez, veinte o cien imágenes, el tiempo total de ejecución es esencialmente la suma de cada ejecución individual.

Al crear un hilo por cada archivo, permitimos que el sistema operativo programe esos trabajos intensivos en CPU de forma concurrente. En una máquina multinúcleo esto a menudo reduce a la mitad —o incluso a un cuarto— el tiempo de reloj. La contrapartida es una huella de memoria ligeramente mayor, pero para la mayoría de los trabajos por lotes el aumento de velocidad vale la pena.

> **Consejo profesional:** Si estás manejando cientos de megabytes de imágenes, considera usar `concurrent.futures.ProcessPoolExecutor` en lugar de `threading`. Los procesos te brindan paralelismo real en el intérprete CPython limitado por el GIL, a costa de un poco más de sobrecarga.

## Paso 1: Instalar Aspose OCR para Python

Primero lo primero—pongamos la biblioteca OCR en tu sistema.

```bash
pip install aspose-ocr
```

Esa única línea descarga los últimos binarios de Aspose OCR y sus enlaces para Python. Si encuentras un error de permisos, intenta añadir `--user` o usar un entorno virtual.

## Paso 2: Cargar imagen para OCR – la función worker

Ahora definimos la rutina central que se ejecutará en cada hilo. **Carga la imagen para OCR**, ejecuta el reconocimiento y muestra una vista previa del texto extraído.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Algunas cosas a tener en cuenta:

- **¿Por qué un nuevo `OcrEngine` por hilo?** El motor mantiene buffers internos; compartir una única instancia provocaría condiciones de carrera y salida desordenada.  
- **¿Por qué eliminar saltos de línea?** Cuando registramos en la consola mantiene la línea ordenada.  
- **¿Manejo de errores?** En producción envolverías el cuerpo en un `try/except` y quizá registrarías en un archivo—algo que cubriremos más adelante.

## Paso 3: Listar los archivos PNG que deseas procesar

Podrías codificar la lista, pero un enfoque más flexible es escanear un directorio. A continuación listamos manualmente tres archivos para mayor claridad; reemplaza las rutas con tu propia carpeta.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Si prefieres un descubrimiento automático:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Ese pequeño ajuste te permite **extraer texto de PNG** en bloque sin tocar el código fuente cada vez.

## Paso 4: Configurar ocr multiple files con batch OCR images

Ahora creamos un hilo para cada imagen. Este es el corazón del patrón **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

La comprensión de lista mantiene el código conciso, y cada objeto `Thread` almacena la función objetivo y su argumento (`image_path`).  

> **Nota al margen:** El módulo `threading` de Python usa hilos nativos del SO, por lo que en una laptop de 4 núcleos típicamente verás hasta cuatro hilos ejecutándose realmente a la vez; el resto se programará a medida que los núcleos queden libres.

## Paso 5: Ejecutar reconocimiento de imágenes en paralelo

Iniciar los workers es sencillo: iterar sobre la lista y llamar a `start()`. Después esperamos a que cada hilo termine usando `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Cuando el script termine, verás una serie de líneas como:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Esa salida confirma que cada PNG fue procesado y el texto extraído está disponible para un manejo posterior (p. ej., guardarlo en una base de datos o alimentarlo a una canalización NLP).

## Paso 6: Verificar los resultados y manejar casos límite

### Verificando resultados vacíos

A veces una imagen está demasiado ruidosa, o el motor OCR no detecta ningún carácter. Una rápida verificación de sanidad puede salvarte de errores posteriores.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Limitar el número de hilos concurrentes

Si ejecutas esto en una VM modesta, crear cientos de hilos podría saturar el programador. Puedes limitar la concurrencia con un semáforo:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Guardar resultados en un archivo

En lugar de imprimir, podrías querer un CSV con el nombre de archivo y el texto extraído:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Asegúrate de abrir el CSV **una sola vez** fuera de la función del hilo para evitar condiciones de carrera; el escritor del módulo `csv` es seguro para hilos en escrituras simples.

## Ejemplo completo funcional

Juntando todo, aquí tienes un script único que puedes colocar en un archivo llamado `batch_ocr.py` y ejecutar:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}