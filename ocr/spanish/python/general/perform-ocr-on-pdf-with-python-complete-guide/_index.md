---
category: general
date: 2026-06-25
description: 'Realiza OCR en PDF usando Python: aprende cómo cargar el PDF para OCR,
  extraer texto de las páginas del PDF y previsualizar el texto reconocido de manera
  eficiente.'
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: es
og_description: Realiza OCR en PDF con Python. Esta guía muestra cómo cargar un PDF
  para OCR, extraer texto de las páginas del PDF y previsualizar el texto reconocido
  rápidamente.
og_title: Realiza OCR en PDF con Python – Tutorial paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Realiza OCR en PDF con Python – Guía completa
url: /es/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR en PDF con Python – Guía Completa

¿Alguna vez necesitaste **realizar OCR en archivos PDF** pero no sabías por dónde empezar? Tal vez tengas una montaña de contratos escaneados, o un único manual voluminoso que se niega a cooperar con tu extractor de texto habitual. En resumen, quieres **cargar PDF para OCR**, extraer el texto y obtener una vista previa rápida, todo sin agotar la memoria de tu máquina.

Pues estás en el lugar correcto. En este tutorial recorreremos un script de Python totalmente funcional que **extrae texto de páginas PDF**, te muestra cómo **previsualizar el texto reconocido** y también aborda el clásico problema de **cómo hacer OCR en PDF grandes** de manera eficiente.

Al final tendrás un programa listo para ejecutar, una comprensión clara de cada parámetro de configuración y varios consejos para evitar los errores comunes que tropiezan a los principiantes.

---

## Lo que aprenderás

- Cómo **cargar PDF para OCR** usando la biblioteca `aocr`.
- Los pasos exactos para **realizar OCR en páginas PDF** una a una.
- Formas de **extraer texto de páginas PDF** manteniendo bajo el uso de memoria.
- Cómo **previsualizar el texto reconocido** para validar los resultados.
- Estrategias para manejar **PDF grandes** sin agotar la RAM.

> **Consejo:** Esta guía asume que tienes Python 3.9+ instalado y una familiaridad básica con entornos virtuales. Si eres nuevo en Python, configura primero un `virtualenv`; créeme, te ahorrará dolores de cabeza después.

---

## Requisitos previos

| Requisito | Por qué es importante |
|-----------|-----------------------|
| Paquete Python `aocr` (o cualquier motor OCR compatible) | Proporciona la clase `OcrEngine` usada a lo largo del script. |
| `pip` y un entorno virtual | Mantiene las dependencias aisladas del Python del sistema. |
| Suficiente espacio en disco para extracciones temporales de imágenes | Algunos motores OCR escriben imágenes de página en disco antes de procesarlas. |
| Opcional: `tqdm` para barras de progreso | Mejora la experiencia de usuario al tratar trabajos de **cómo hacer OCR en PDF grandes**. |

Instala lo esencial con:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Si tu PDF está protegido con contraseña, deberás proporcionar la contraseña más adelante—consulta la sección “Casos límite”.

---

## Paso 1: Realizar OCR en PDF – Configurar el motor

Lo primero es crear una instancia del motor OCR. Piensa en él como el cerebro que leerá la imagen de cada página y generará texto plano.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **¿Por qué establecer `max_memory_mb`?**  
> Los motores OCR suelen almacenar en caché las imágenes de página en RAM. Al limitar la memoria evitas que tu script se bloquee con un contrato de 500 páginas.

---

## Paso 2: Cargar PDF para OCR y configurar ajustes

Ahora realmente **cargamos PDF para OCR**. La ruta puede ser absoluta o relativa; solo asegúrate de que el archivo exista.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Si el PDF está cifrado, `engine.load_pdf` normalmente lanzará una excepción. En ese caso puedes llamar a `engine.load_pdf(pdf_path, password="secret")`—más adelante profundizaremos en esto.

---

## Paso 3: Extraer texto de páginas PDF – Bucle principal

Aquí es donde **realizamos OCR en PDF** página por página. También **previsualizaremos el texto reconocido** para los primeros cientos de caracteres, de modo que puedas verificar que todo funciona.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Pro tip:** La barra de progreso `tqdm` te brinda una pista visual, especialmente útil al trabajar con documentos de **cómo hacer OCR en PDF grandes** que tardan varios minutos en procesarse.

---

## Paso 4: Juntándolo todo – Un script listo para ejecutar

A continuación tienes el ejemplo completo y ejecutable. Guárdalo como `pdf_ocr.py` y ejecútalo con `python pdf_ocr.py ruta/a/tu/archivo.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Salida esperada (extracto)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Verás una breve previsualización para cada página, seguida de una confirmación final de que el archivo de texto concatenado ha sido escrito.

---

## Casos límite y consejos prácticos

| Situación | Qué hacer |
|-----------|-----------|
| **PDF cifrado** | Pasa la contraseña: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **PDF muy grande (> 1000 páginas)** | Incrementa `max_memory_mb` con cautela, o procesa en bloques (p. ej., 200 páginas a la vez). |
| **Contenido mixto (impreso + manuscrito)** | Cambia `engine.recognition_mode` a `aocr.RecognitionMode.MIXED` si la biblioteca lo soporta. |
| **Fuentes faltantes o escaneo de baja calidad** | Pre‑procesa las páginas con una biblioteca de mejora de imágenes (p. ej., Pillow) antes de llamar a `recognize()`. |
| **Fallos por falta de memoria** | Reduce `preview_len` o escribe el texto de cada página directamente a disco en lugar de mantenerlo todo en una lista. |

---

## Cómo hacer OCR en PDF grandes de forma eficiente – Estrategias avanzadas

Al abordar **cómo hacer OCR en PDF grandes**, la velocidad y la estabilidad se vuelven críticas. Aquí tienes algunos trucos que puedes incorporar al script:

1. **Paralelizar por página** – Usa `concurrent.futures.ThreadPoolExecutor` si el motor OCR es seguro para hilos.
2. **Cachear imágenes intermedias** – Algunos motores permiten almacenar las páginas rasterizadas en SSD, reduciendo drásticamente la carga de CPU en ejecuciones posteriores.
3. **Escribir la salida por lotes** – En lugar de ir acumulando en una lista de Python, abre el archivo de salida una sola vez y escribe el texto de cada página tan pronto como esté listo.
4. **Ajustar DPI** – Bajar el DPI durante la rasterización reduce la memoria pero puede afectar la precisión; busca un punto medio (usualmente 200‑300 DPI).

A continuación tienes un fragmento rápido que muestra cómo podrías paralelizar el paso de OCR (opcional, descomenta para usar):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Recuerda: el paralelismo puede incrementar el uso de CPU, así que monitorea la temperatura de tu sistema en ejecuciones largas.

---

## Preguntas frecuentes

**P: ¿Puedo usar este script con otras bibliotecas OCR como Tesseract?**  
R: Por supuesto. Sustituye las llamadas a `aocr` por `pytesseract.image_to...

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo hacer OCR de PDF en .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo extraer texto de una imagen desde un stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Cómo extraer texto de una imagen desde URL usando Aspose.OCR para Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}