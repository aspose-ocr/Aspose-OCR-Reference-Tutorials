---
category: general
date: 2026-06-28
description: Cómo hacer OCR por lotes usando Python. Aprende a hacer OCR en múltiples
  imágenes, extraer texto de PNG y convertir una imagen a texto con un tutorial completo
  de OCR en Python.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: es
og_description: Cómo hacer OCR por lotes en Python explicado en la primera frase.
  Sigue este tutorial de OCR en Python para extraer texto de archivos PNG de manera
  eficiente.
og_title: Cómo procesar OCR por lotes en Python – Guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Cómo realizar OCR por lotes en Python – Guía completa paso a paso
url: /es/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo hacer OCR por lotes en Python – Guía completa paso a paso

¿Alguna vez te has preguntado **cómo hacer OCR por lotes** a una pila de páginas escaneadas sin escribir un bucle que bloquee tu UI? No eres el único. Procesar docenas de archivos PNG uno por uno puede sentirse como ver secar la pintura, sobre todo cuando cada imagen tarda uno o dos segundos en decodificarse.  

En este tutorial te mostraremos una forma limpia y sin bloqueo de **realizar OCR en múltiples imágenes** a la vez, **extraer texto de archivos PNG** y **convertir imagen a texto** usando un motor OCR moderno de Python. Al final tendrás un script listo para ejecutar que puedes incorporar a cualquier proyecto – perfecto para un rápido *python ocr tutorial* o un trabajo por lotes de nivel producción.

## Lo que vas a construir

- Inicializar un motor OCR y establecer su idioma a Latin (o cualquier idioma que necesites).  
- Alimentar una lista de rutas de imágenes (PNG en nuestro ejemplo) al motor.  
- Lanzar una operación por lotes que devuelve un objeto similar a Future.  
- Obtener todos los resultados concurrentemente con un pool de hilos, manteniendo libre tu hilo principal.  
- Imprimir el texto reconocido para cada página, separado de forma clara.

Sin trucos ocultos, solo Python puro y una biblioteca OCR de terceros (usaremos el ficticio paquete `pyocr` para ilustrar).  

**Requisitos previos**  
- Python 3.8+ instalado.  
- Familiaridad básica con funciones de Python y `concurrent.futures`.  
- Acceso a una biblioteca OCR que exponga una clase `OcrEngine` (p. ej., `pip install pyocr`).  

Si te falta alguno de estos, consíguelos ahora – es más fácil de lo que piensas.

---

## Cómo hacer OCR por lotes en Python – Conceptos clave

Antes de sumergirnos en el código, respondamos el “por qué” detrás de cada paso.

1. **¿Por qué establecer el idioma?**  
   La precisión del OCR se dispara cuando el motor sabe qué caracteres esperar. Latin funciona para inglés, francés, español, etc. Cambia a `Language.Japanese` o `Language.Arabic` si lo necesitas.

2. **¿Por qué usar una operación por lotes?**  
   Una llamada por lotes permite que el motor programe el trabajo internamente, a menudo aprovechando hilos nativos o aceleración GPU. Devuelve un manejador que puedes consultar más tarde, lo que significa que no bloqueas mientras se procesa cada imagen.

3. **¿Por qué un ThreadPoolExecutor?**  
   El objeto Future que obtenemos es *perezoso* – solo comienza a extraer resultados cuando lo solicitamos. Al pasar un pool de hilos a `getAll`, dejamos que Python recupere el texto de cada página en paralelo, reduciendo drásticamente el tiempo total de ejecución.

4. **¿Por qué enumerar los resultados?**  
   El orden de los resultados coincide con el orden de las rutas de entrada, por lo que podemos etiquetar de forma segura cada número de página.

Entender estos “por qué” te ayuda a adaptar el patrón a otras bibliotecas o a conjuntos de datos más grandes.

---

## Paso 1: Instalar e importar los paquetes requeridos

Primero, asegúrate de que la biblioteca OCR esté instalada. El ejemplo usa un paquete genérico `pyocr`; reemplázalo con la biblioteca real que prefieras (p. ej., `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Ahora importa todo lo que necesitamos.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Consejo profesional:** Usar `Path` de `pathlib` hace que tu script sea independiente del SO y más fácil de leer.

---

## Paso 2: Crear el motor OCR y establecer el idioma

Crear el motor es sencillo. Lo bloquearemos a Latin para esta demostración.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

La llamada `setLanguage` es opcional para algunos motores, pero es una buena práctica. Indica al modelo OCR que se centre en el conjunto de caracteres que te interesan, mejorando tanto la velocidad como la precisión.

---

## Paso 3: Listar los archivos de imagen a procesar (Extraer texto de PNG)

Recopila todos los archivos PNG que deseas convertir. Usar `Path.glob` permite que simplemente coloques una carpeta completa sin editar el script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Por qué es importante:** Al ordenar la lista garantizamos un orden determinista, que luego alinea cada resultado con el número de página correcto.

---

## Paso 4: Lanzar una operación OCR por lotes (Convertir imagen a texto)

Ahora entregamos la lista al motor. El método devuelve un contenedor similar a Future que consultaremos más adelante.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Detrás de escena el motor puede iniciar sus propios hilos de trabajo o incluso una canalización GPU. Lo único que nos importa es que tenemos un manejador (`batch_future`) que sabe cómo obtener los resultados individuales.

---

## Paso 5: Recuperar todos los resultados concurrentemente (OCR de múltiples imágenes)

Aquí es donde realmente *loteamos* el trabajo. Al pasar un `ThreadPoolExecutor` a `getAll`, el texto de cada página se obtiene en su propio hilo.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Puedes ajustar `max_workers` según la cantidad de núcleos de CPU o las recomendaciones de la biblioteca OCR. Más workers ≠ siempre más rápido – vigila el uso de tu CPU.

---

## Paso 6: Mostrar el texto reconocido (Final del tutorial Python OCR)

Finalmente, imprime el texto de cada página. El objeto `Result` expone `getText()` – ajústalo si tu biblioteca usa un nombre de método diferente.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Salida esperada (ejemplo)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Si alguna imagen falla, la mayoría de los motores insertan una cadena vacía o lanzan una excepción – puedes envolver el bucle en un bloque `try/except` para manejar los casos límite de forma elegante.

---

## Script completo – Listo para ejecutar

A continuación tienes el script completo y autónomo. Cópialo y pégalo en un archivo llamado `batch_ocr.py`, ajusta `YOUR_DIRECTORY` y ejecuta `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Guárdalo, ejecútalo y observa cómo la consola se llena con el texto extraído. Simple, rápido y totalmente asíncrono.

---

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Sin salida** – cadenas vacías | El motor OCR no encontró texto (imagen demasiado ruidosa) | Pre‑procesa las imágenes: binariza, corrige la inclinación o aumenta DPI |
| **`FileNotFoundError`** | Ruta de directorio incorrecta o faltan archivos PNG | Verifica `YOUR_DIRECTORY` y asegura que los archivos terminen en `.png` |
| **Alto uso de CPU** | `max_workers` configurado demasiado alto para tu máquina | Reduce `max_workers` o habilita aceleración GPU si está soportada |
| **Texto Unicode corrupto** | El motor usó un idioma diferente por defecto | Llama `engine.setLanguage(Language.Latin)` (o el apropiado) antes del OCR por lotes |

Abordar estos puntos temprano te ahorra horas de depuración.

---

## Extender el tutorial – Próximos pasos

- **OCR de múltiples imágenes** en otros formatos (JPEG, TIFF) – solo cambia el patrón de glob.  
- **Extraer texto de PNG** y alimentarlo a un índice de búsqueda (p. ej., Elasticsearch).  
- **Convertir imagen a texto** para generación de PDF usando `reportlab` o `PyPDF2`.  
- **Paralelizar entre máquinas** con `multiprocessing` o una cola de tareas como Celery para conjuntos de datos masivos.  

Cada uno de estos temas se construye de forma natural sobre el **python ocr tutorial** que acabas de completar.

---

## Conclusión

Hemos recorrido **cómo hacer OCR por lotes** en una colección de archivos PNG, demostrado el poder de una API orientada a lotes y mostrado cómo **extraer texto de PNG** con un enfoque basado en pool de hilos. El script completo anterior está listo para producción, y ahora tienes una base sólida para cualquier proyecto Python intensivo en OCR.

Pruébalo, ajusta la configuración de idioma y quizá incluso reemplaza `pyocr` por `pytesseract` – el patrón sigue igual. ¿Tienes preguntas o quieres compartir un caso de uso interesante? Deja un comentario y sigamos la conversación.

*¡Feliz codificación!*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}