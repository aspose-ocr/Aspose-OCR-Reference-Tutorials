---
category: general
date: 2026-06-06
description: Extrae texto de imágenes PDF usando OCR en Python. Aprende cómo convertir
  documentos escaneados a texto rápidamente con reconocimiento por lotes asíncrono.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: es
og_description: Extrae texto de imágenes PDF con Python. Esta guía paso a paso muestra
  cómo convertir documentos escaneados a texto usando OCR asíncrono.
og_title: Extraer texto de imágenes PDF – Tutorial de OCR en Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extraer texto de imágenes PDF – Guía de Python para convertir documentos escaneados
  a texto
url: /es/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de PDFs de imágenes – Guía de Python para convertir documentos escaneados a texto

¿Alguna vez necesitaste **extraer texto de PDFs de imágenes** sin pasar horas reescribiendo? En esta guía te mostraremos cómo **convertir documentos escaneados a texto** usando un flujo de trabajo OCR asíncrono simple en Python.  

Si alguna vez has mirado una pila de PDFs escaneados y pensado, “Tiene que haber una forma más rápida”, estás en el lugar correcto. Revisaremos cada línea de código, explicaremos por qué cada parte es importante, e incluso cubriremos algunos casos límite que podrías encontrar.

## Lo que aprenderás

- Cómo iniciar un motor OCR y establecer el idioma de reconocimiento.  
- La mecánica de alimentar una lista mixta de PNG y PDFs a un reconocedor por lotes.  
- Ejecutar el trabajo OCR de forma asíncrona para que tu aplicación permanezca receptiva.  
- Recuperar los resultados, emparejarlos con sus archivos de origen y imprimir una salida limpia.  

**Prerequisitos**: Python 3.8+, un entendimiento básico de `asyncio` o `concurrent.futures`, y una biblioteca OCR que exponga una clase `OcrEngine` similar a la del ejemplo (p. ej., Aspose.OCR, wrapper de Tesseract, o un wrapper personalizado). No se requiere una configuración pesada—simplemente instala la biblioteca y estarás listo.

![extraer texto de PDFs de imágenes](https://example.com/placeholder.png "Captura de pantalla del resultado OCR – extraer texto de PDFs de imágenes")

## Extraer texto de PDFs de imágenes – Configuración del motor OCR

Lo primero que necesitas es una instancia del motor OCR configurada para el idioma de tus documentos. En nuestro caso usaremos francés, pero puedes cambiarlo por cualquier idioma soportado.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Por qué es importante**: Configurar el idioma desde el principio mejora drásticamente la precisión. El motor utiliza diccionarios y modelos de caracteres específicos del idioma; alimentarlo con el idioma incorrecto es una causa frecuente de resultados distorsionados.

## Preparar la lista de archivos – Imágenes y PDFs juntos

Nuestro reconocedor por lotes puede manejar tanto imágenes raster (`.png`, `.jpg`) como contenedores PDF. Simplemente pasa una lista Python simple de rutas de archivo.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Consejo**: Mantén la lista plana; el motor desempaquetará internamente cada página PDF en imágenes antes del reconocimiento. Si tienes miles de archivos, considera dividir la lista en lotes más pequeños para evitar picos de memoria.

## Iniciar reconocimiento por lotes asíncrono

En lugar de bloquear el hilo principal, lanzamos el trabajo OCR en segundo plano. El método devuelve un `Future` que eventualmente contendrá una lista de objetos `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Cómo funciona**: Internamente el motor crea un pool de hilos (o una tarea async, según la implementación). Esto te permite seguir realizando otras tareas—como actualizar una UI, obtener más archivos o registrar el progreso—mientras el trabajo pesado se ejecuta en otro lugar.

## Haz algo útil mientras OCR se ejecuta

Un error común es quedarse inactivo y sondear el futuro en un bucle ajustado. En su lugar, puedes realizar cualquier trabajo no relacionado. Para la demostración, simplemente imprimiremos una línea de estado.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Recopilar resultados una vez que el Future se complete

Cuando estés listo para recopilar la salida OCR, usa `as_completed` de `concurrent.futures`. Este patrón funciona tanto si tienes un futuro como varios.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Lo que verás**: Cada ruta de archivo seguida de la representación de texto plano extraído. Para PDFs, `result.text` contiene el texto concatenado de cada página.

### Salida esperada (ejemplo)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Si notas caracteres faltantes, verifica que el idioma que configuraste coincida con el idioma del documento, y considera pre‑procesar las imágenes (corregir inclinación, aumentar contraste) antes de pasárselas al motor.

## Manejo de casos límite y errores comunes

| Situación | Qué hacer |
|-----------|------------|
| **Idiomas mixtos** | Ejecuta primero una detección de idioma, luego instancia motores separados por idioma. |
| **PDFs enormes (> 100 MB)** | Divide el PDF en páginas individuales en disco (p. ej., usando `PyPDF2`) y pásalas como entradas separadas. |
| **Escrituras no latinas** | Asegúrate de que la biblioteca OCR incluya el paquete de idioma necesario; algunas bibliotecas requieren que descargues archivos de datos adicionales. |
| **Cuello de botella de rendimiento** | Aumenta el tamaño del pool de hilos (`engine.set_thread_pool_size(8)`) o cambia a un backend acelerado por GPU si está disponible. |
| **Texto faltante en imágenes de baja resolución** | Pre‑procesa con OpenCV: `cv2.resize`, `cv2.threshold` y `cv2.medianBlur` para mejorar la legibilidad. |

## Ejemplo completo funcional (listo para copiar y pegar)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Guarda esto como `extract_text_async.py`, reemplaza `YOUR_DIRECTORY` con la ruta a tus archivos, instala el paquete OCR (`pip install your-ocr-lib`), y ejecuta `python extract_text_async.py`. Deberías ver la salida de consola ilustrada anteriormente.

## Próximos pasos – Más allá de la extracción básica

- **Post‑procesamiento**: Elimina espacios en blanco extra, normaliza Unicode (`unicodedata.normalize`), o ejecuta un corrector ortográfico para limpiar el ruido del OCR.  
- **Salida estructurada**: Exporta los resultados a CSV, JSON, o directamente a una base de datos para búsquedas posteriores.  
- **Lotes paralelos**: Si tienes cientos de archivos, crea múltiples futures y usa una cola para mantener la CPU ocupada sin saturar la memoria.  
- **Integrar con frameworks web**: Conecta este script a un endpoint de Flask o FastAPI para ofrecer OCR bajo demanda como servicio.

---

### TL;DR

Ahora sabes cómo **extraer texto de PDFs de imágenes** con un script Python mínimo que ejecuta OCR de forma asíncrona, permitiéndote **convertir documentos escaneados a texto** mientras tu programa permanece receptivo. Juega con la configuración de idioma, tamaños de lote y trucos de pre‑procesamiento para exprimir la máxima precisión de caracteres.

¿Tienes alguna variante que quieras compartir—quizá OCR en notas manuscritas o un servicio en la nube? Deja un comentario, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraer texto de imágenes usando la operación OCR en carpetas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extraer texto de imágenes usando Aspose.OCR – Caracteres permitidos](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}