---
category: general
date: 2026-03-26
description: 'cómo realizar OCR por lotes de manera eficiente con Python: aprende
  a extraer texto de imágenes y conversión OCR de PDF con procesamiento paralelo.'
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: es
og_description: cómo hacer OCR por lotes de forma eficiente—guía paso a paso para
  extraer texto de imágenes, conversión OCR de PDF y procesamiento por lotes de OCR
  usando Python.
og_title: 'cómo hacer OCR por lotes: extracción de texto rápida y paralela'
tags:
- OCR
- Python
- Parallel Computing
title: 'Cómo hacer OCR por lotes: extracción rápida de texto en paralelo'
url: /es/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo hacer OCR por lotes: extracción de texto paralela rápida

¿Alguna vez te has preguntado **cómo hacer OCR por lotes** cuando tienes docenas de páginas escaneadas, capturas de pantalla y PDFs por ahí? No eres el único—la mayoría de los desarrolladores se topan con la misma pared: procesar cada archivo uno por uno se vuelve un cuello de botella doloroso.  

La buena noticia es que puedes lanzar un puñado de hilos de trabajo, alimentarles todos tus archivos y observar cómo el motor OCR procesa el lote en paralelo. En este tutorial recorreremos un ejemplo completo, listo para ejecutar, que muestra **extraer texto de imágenes**, realizar **conversión OCR de PDF**, y aprovechar **procesamiento OCR paralelo** para velocidad.

> **Lo que obtendrás**  
> * Un script Python totalmente funcional que procesa una lista mixta de archivos PNG, TIFF, PDF y JPG de una sola vez.  
> * Comprensión de por qué un pool de hilos acelera las tareas OCR con I/O limitado.  
> * Consejos para manejar errores, PDFs grandes y recuentos de hilos personalizados.  

## Requisitos previos

| Requisito | Razón |
|-------------|--------|
| Python 3.8+ | Sintaxis moderna y `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Proporciona `OcrBatchProcessor` y objetos de resultado |
| A handful of sample files (PNG, TIFF, PDF, JPG) | Para ver la **extraer texto de imágenes** en acción |
| Basic familiarity with threads (optional) | Útil pero no obligatorio |

Si aún no has instalado el paquete `ocr`, ejecuta:

```bash
pip install ocr-lib   # replace with the actual package name
```

Ahora que el entorno está listo, desglosaremos el problema.

## Paso 1: Importar auxiliares e instanciar el procesador por lotes

Lo primero que necesitamos es un lugar para recopilar todos los trabajos OCR. La clase `OcrBatchProcessor` hace exactamente eso: encola elementos de trabajo y te devuelve una lista de objetos `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Por qué es importante*: Importar `as_completed` nos permite reaccionar a cada trabajo terminado al instante, en lugar de esperar al archivo más lento. Esto es el núcleo del **procesamiento OCR por lotes**.

## Paso 2: Ajustar el pool de hilos para ejecución paralela

Por defecto, el procesador podría usar un solo hilo, lo que anula el propósito del procesamiento por lotes. Pedimos explícitamente cuatro trabajadores—siéntete libre de aumentar este número hasta el número de núcleos de CPU que tengas.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Consejo profesional*: Para tareas limitadas por I/O como OCR, a menudo obtienes rendimientos decrecientes después de `CPU cores * 2`. Prueba algunos valores y elige el punto óptimo.

## Paso 3: Encolar cada archivo que quieras OCR

Aquí añadimos una mezcla de archivos de imagen y PDF. El método `add` simplemente registra la ruta; el trabajo real no comenzará hasta que enviemos el lote.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Si necesitas procesar una carpeta completa, un rápido bucle `glob` hace el truco:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Paso 4: Lanzar los trabajos y recopilar futures

Llamar a `submit_all` le da luz verde al procesador. Devuelve una lista de objetos `Future`—piensa en ellos como marcadores de posición para resultados que aparecerán más tarde.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

En este punto el motor OCR está ocupado en segundo plano, cada hilo masticando un archivo.

## Paso 5: Obtener resultados tan pronto como terminen

Usando `as_completed` iteramos sobre los futures en el orden en que terminan, no en el orden en que los enviamos. Esto mantiene nuestro script responsivo, especialmente cuando algunos PDFs tardan más que PNG simples.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Salida esperada** (truncada por brevedad):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Cada bloque corresponde a la representación en texto plano del archivo original. Si estás realizando **conversión OCR de PDF**, el texto incluirá todo lo que el motor OCR pudo descifrar de cada página.

## Manejo de casos límite y errores comunes

| Situación | Qué observar | Solución rápida |
|-----------|--------------|-----------------|
| Una imagen corrupta | `future.result()` lanza `OSError` | Envolver en `try/except` (ver código arriba) |
| PDFs muy grandes ( > 100 MB ) | Presión de memoria, hilos más lentos | Incrementar `thread_count` modestamente o dividir el PDF en capítulos primero |
| Documentos multilingües | El modelo OCR predeterminado puede detectar mal | Pasar indicaciones de idioma a `OcrBatchProcessor` si la biblioteca lo soporta |
| Necesidad de preservar el diseño | `get_text()` simple pierde columnas | Usar `ocr_result.get_hocr()` o método similar consciente del diseño |

### Consejo profesional: Recuento de hilos personalizado según tipo de archivo

Si sabes que la mayor parte de tu carga de trabajo son PDFs, podrías asignar más hilos para esos y menos para PNG pequeños. Algunas bibliotecas permiten pasar una `priority` por trabajo; de lo contrario, puedes crear dos lotes separados—uno para imágenes, otro para PDFs—y ejecutarlos concurrentemente.

## Visión general visual (opcional)

![diagrama del flujo de OCR por lotes](https://example.com/ocr-workflow.png "flujo de OCR por lotes")

*El diagrama ilustra el flujo desde el descubrimiento de archivos → creación del lote → ejecución paralela → agregación de resultados.*

## Script completo que puedes copiar y pegar

A continuación está el programa completo, listo para colocar en un archivo `.py`. Incluye todos los fragmentos anteriores, más un pequeño ayudante que descubre automáticamente los archivos compatibles en un directorio.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Guarda esto como `batch_ocr.py`, apunta a una carpeta que contenga tus escaneos y observa la consola llenarse de texto extraído.  

### Por qué funciona esto

* **Thread pool** – OCR es mayormente una espera de I/O de disco y llamadas al motor externo, por lo que varios hilos mantienen la CPU ocupada.  
* **`as_completed`** – Obtienes resultados tan pronto como están listos, lo cual es ideal para retroalimentación UI o pipelines de streaming.  
* **Error isolation** – Un archivo defectuoso no derribará todo el lote; el bloque `try/except` aísla los fallos.

## Conclusión

En resumen, ahora sabes **cómo hacer OCR por lotes** usando `concurrent.futures` de Python junto con una biblioteca OCR que soporta procesamiento por lotes. Configurando un modesto pool de hilos, encolando cada archivo compatible y obteniendo resultados a medida que terminan, logras un **procesamiento OCR paralelo** rápido sin sacrificar fiabilidad.  

A partir de aquí podrías:

* Conectar la salida a un índice de búsqueda para una recuperación rápida de documentos.  
* Extender el script para escribir cada resultado en un archivo `.txt` junto al original.  
* Reemplazar el pool de hilos incorporado por `asyncio` si tu biblioteca OCR ofrece APIs asíncronas.  

Sigue experimentando—cambia a Tesseract, Azure Cognitive Services o Google Vision, y verás que el mismo patrón se aplica. ¡Feliz OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}