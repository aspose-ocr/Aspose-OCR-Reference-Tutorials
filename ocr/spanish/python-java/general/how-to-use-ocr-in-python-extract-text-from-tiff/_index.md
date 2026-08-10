---
category: general
date: 2026-07-05
description: Cómo usar OCR en Python para convertir TIFF a texto rápidamente. Aprende
  los pasos de la biblioteca OCR en Python para extraer texto de imágenes TIFF y crear
  un motor OCR en Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: es
og_description: ¿Cómo usar OCR en Python? Esta guía te muestra paso a paso cómo convertir
  TIFF a texto usando un motor OCR en Python y la biblioteca ocr python.
og_title: Cómo usar OCR en Python – Extracción completa de texto de TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Cómo usar OCR en Python – Extraer texto de TIFF
url: /es/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR en Python – Extraer texto de TIFF

¿Alguna vez te has preguntado **cómo usar OCR en Python** para convertir un libro escaneado en texto editable? No eres el único: desarrolladores, investigadores y aficionados se encuentran con este obstáculo al trabajar con imágenes TIFF de varias páginas. ¿La buena noticia? Con la **ocr library python** puedes lanzar un pequeño motor OCR, apuntarlo a un archivo TIFF y obtener texto limpio y buscable en segundos.

En este tutorial recorreremos todo lo que necesitas: instalar el paquete correcto, cargar un TIFF de varias páginas, ejecutar el motor OCR y, finalmente, imprimir el contenido de cada página. Al final podrás **convertir TIFF a texto** y **extraer texto de TIFF** sin salir de tu entorno Python.

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

- Python 3.9 o superior (el ejemplo se probó en 3.11)
- Una versión reciente de la biblioteca `ocr` (o cualquier `python ocr engine` compatible que prefieras)
- Un archivo TIFF de varias páginas que deseas procesar (lo llamaremos `scanned_book.tif`)
- Familiaridad básica con scripts de Python y entornos virtuales

No se requieren herramientas externas pesadas, solo pip y unas cuantas líneas de código.

## Instalar la OCR Library Python

Lo primero es contar con un backend OCR sólido. Para esta guía usaremos el ficticio paquete `ocr` que incluye una API de alto nivel sencilla, pero el mismo patrón funciona con envoltorios basados en Tesseract como `pytesseract` o SDKs comerciales.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Si estás en Windows y el paquete depende de binarios nativos, asegúrate de tener instalado el redistributable de Visual C++ apropiado. El instalador normalmente te advertirá si falta algo.

## Cómo usar el motor OCR en Python

Ahora que la biblioteca está lista, vamos a lanzar un motor OCR y apuntarlo a nuestro archivo TIFF. El siguiente fragmento crea una instancia del motor, establece el idioma a inglés y lo prepara para el procesamiento de varias páginas.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**¿Por qué establecer el idioma?**  
La mayoría de los motores OCR utilizan modelos de idioma para mejorar la precisión. Si omites este paso, el motor recurre a un modelo genérico que podría reconocer mal la puntuación o los caracteres especiales.

## Cargar la imagen TIFF de varias páginas

La siguiente pieza es cargar el documento escaneado. El ayudante `ocr.Image.load` entiende pilas TIFF de forma nativa, devolviendo un objeto que representa cada página internamente.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** Si tu TIFF usa compresión (CCITT Group 4, LZW, etc.) y la biblioteca lanza un error, intenta convertirlo a una versión sin compresión con ImageMagick primero:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Realizar OCR en todas las páginas – Convertir TIFF a texto

Con el objeto de imagen en mano, el motor puede procesar todas las páginas a la vez. Este método devuelve una lista donde cada elemento contiene el resultado OCR de una sola página.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**¿Qué está sucediendo bajo el capó?**  
La función `recognize_multi_page` itera sobre cada página rasterizada, ejecuta el reconocedor de redes neuronales y empaqueta la salida de texto plano junto con puntuaciones de confianza. Es esencialmente una operación por lotes que te ahorra escribir un bucle manual.

## Iterar a través de los resultados – Extraer texto de TIFF

Finalmente, mostramos el texto reconocido. Puedes escribir la salida en archivos `.txt` separados, enviarla a una base de datos o alimentarla a un índice de búsqueda, lo que mejor se ajuste a tu flujo de trabajo.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Salida esperada

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Cada cadena `result.text` contiene la salida OCR cruda de esa página. Si necesitas preservar los saltos de línea, la mayoría de los motores exponen `result.lines` como una lista de cadenas.

## Manejo de archivos TIFF grandes – Consejos y trucos

Procesar un TIFF de 500 páginas puede consumir mucha memoria. Aquí tienes algunas estrategias para mantener todo fluido:

1. **Dividir las páginas** – En lugar de `recognize_multi_page`, llama a `engine.recognize(page)` dentro de un generador que devuelva una página a la vez.  
2. **Ajustar DPI** – Reducir la resolución de la imagen (p. ej., de 300 DPI a 200 DPI) disminuye la carga de CPU mientras afecta mínimamente la precisión para la mayoría del texto impreso.  
3. **Paralelizar** – Si tu motor OCR es seguro para hilos, crea un `concurrent.futures.ThreadPoolExecutor` para ejecutar el reconocimiento en varias páginas simultáneamente.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Guardar el texto extraído en archivos

La mayoría de los flujos de trabajo reales necesitan almacenamiento persistente. A continuación se muestra una forma concisa de volcar el texto de cada página en su propio archivo, preservando el orden de las páginas.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Ahora tienes un directorio limpio de archivos `.txt` listo para indexar o para procesamiento NLP adicional.

## Vista previa de la imagen – Cómo usar visualmente los resultados de OCR

Si deseas ver la superposición OCR sobre la imagen original (útil para depuración), muchas bibliotecas permiten dibujar cuadros delimitadores. Aquí tienes un ejemplo rápido usando Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Cómo usar OCR en Python – superposición OCR en una página TIFF](ocr_overlay_example.png)

*Texto alternativo:* Cómo usar OCR en Python – superposición visual del texto reconocido en una página TIFF.

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Caracteres distorsionados | Modelo de idioma incorrecto | Establecer `engine.language` al enum correcto |
| Páginas faltantes | Compresión TIFF no soportada | Convertir a TIFF sin compresión primero |
| Rendimiento lento | DPI alto + procesamiento de un solo hilo | Reducir DPI o habilitar multihilo |
| Salida vacía | La imagen es demasiado oscura/bajo contraste | Pre‑procesar con estiramiento de contraste (`opencv` o `Pillow`) |

Abordar estos problemas desde el principio te ahorra horas de depuración más adelante.

## Próximos pasos – Más allá de la extracción básica

Ahora que dominas los fundamentos de **cómo usar OCR en Python**, considera explorar:

- **Generación de PDF** – Combina el texto extraído con `reportlab` para reconstruir PDFs buscables.  
- **Detección de idioma** – Cambia automáticamente `engine.language` usando `langdetect`.  
- **Extracción de datos estructurados** – Usa expresiones regulares o spaCy para extraer fechas, nombres o tablas del texto bruto.  
- **Backends OCR alternativos** – Sustituye `ocr` por `pytesseract` o `easyocr` si necesitas soporte multilingüe.

Cada uno de estos temas se enlaza naturalmente con las palabras clave secundarias **ocr library python**, **convert tiff to text**, **extract text from tiff** y **python ocr engine**, dándote una base sólida para proyectos más avanzados.

---

### Conclusión

Hemos cubierto **cómo usar OCR en Python** desde la instalación hasta el procesamiento de múltiples páginas, mostrándote exactamente cómo **convertir TIFF a texto** y **extraer texto de TIFF** usando un **python OCR engine** sencillo. El ejemplo completo y ejecutable anterior debería funcionar directamente con la mayoría de los archivos TIFF estándar, y los consejos proporcionados te ayudarán a escalar a documentos más grandes o a integrar OCR en pipelines más extensos.

Pruébalo con tus propios libros escaneados, recibos o imágenes de archivo, y luego experimenta con las ideas de siguiente nivel enumeradas en la sección “Próximos pasos”. ¡Feliz codificación y que tus resultados OCR sean siempre precisos!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cómo extraer texto de TIFF con Aspose.OCR para Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Cómo realizar extracción de texto de imagen desde stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}