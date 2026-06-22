---
category: general
date: 2026-06-22
description: Aprende a hacer OCR a archivos PDF en Python, extraer texto de PDF y
  convertir PDF a texto usando un enfoque basado en flujos. Pasos simples para procesar
  PDF escaneados.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: es
og_description: ¿Cómo hacer OCR a archivos PDF en Python? Sigue esta guía para extraer
  texto de PDF, convertir PDF a texto y procesar PDF escaneado usando un flujo.
og_title: Cómo hacer OCR a PDF en Python – Guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Cómo hacer OCR a PDFs en Python – Guía completa para extraer texto de PDFs
url: /es/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo hacer OCR de PDF en Python – Guía completa para extraer texto de PDFs

¿Alguna vez te has preguntado **cómo hacer OCR de PDF** sin luchar con herramientas de escritorio pesadas? No eres el único. En muchos proyectos del mundo real —piense en la automatización de facturas o la digitalización de escaneos de archivo— necesitas una forma fiable de convertir un PDF escaneado en texto buscable y editable.

En este tutorial recorreremos un ejemplo limpio y de extremo a extremo que **extrae texto de PDF** de las páginas usando un motor OCR ligero de Python. Al final sabrás exactamente cómo **convertir PDF a texto**, cómo **cargar PDF desde un flujo**, y cómo **procesar PDF escaneado** de manera eficiente. Sin magia, solo código Python sencillo que puedes incorporar a tu proyecto hoy.

## Lo que aprenderás

- Instalar y configurar una biblioteca OCR de Python que entienda la entrada PDF.  
- Habilitar el modo de reconocimiento PDF y establecer el formato de salida como texto plano.  
- Cargar un PDF de varias páginas desde un flujo de archivo (el patrón clásico “load pdf from stream”).  
- Ejecutar OCR en todas las páginas y recuperar el contenido textual.  
- Imprimir o almacenar los resultados para el procesamiento posterior.  

**Prerequisitos**  
- Python 3.8+ instalado en tu máquina.  
- Familiaridad básica con pip y entornos virtuales.  
- Un archivo PDF escaneado (llamado `multipage.pdf` en el ejemplo) colocado en un directorio conocido.  

Si alguno de esos conceptos te resulta desconocido, no te preocupes — cada paso se explica en lenguaje sencillo, y proporcionaremos los comandos exactos que necesitas.

---

## Paso 1: Instalar el motor OCR (cómo hacer OCR de PDF)

Lo primero — necesitas un motor OCR que pueda manejar entradas PDF. Para esta guía usaremos el paquete hipotético `ocr` (la API refleja los SDK comerciales populares, pero el mismo patrón funciona con Tesseract‑OCR, ABBYY o Google Vision cuando se envuelve adecuadamente).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Consejo profesional:** Si estás en Windows y encuentras errores de permiso, prueba `pip install --user ocr` en su lugar.

Una vez instalado el paquete, puedes importarlo en tu script y crear una instancia del motor — este es el corazón de **cómo hacer OCR de PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

El objeto `OcrEngine` contiene todas las configuraciones que ajustaremos más adelante, como el idioma, DPI y —crucialmente— el modo PDF.

## Paso 2: Habilitar el reconocimiento PDF y elegir la salida (extraer texto de PDF)

Por defecto, muchos SDK OCR asumen que les estás proporcionando imágenes. Para que el motor trate el flujo entrante como un PDF, habilitamos la bandera de reconocimiento PDF y solicitamos salida en texto plano.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

¿Por qué molestarse en especificar el formato de salida? Porque algunos motores pueden devolver PDF con capas de texto ocultas, PDFs buscables o JSON con cajas delimitadoras. Para la mayoría de los flujos de extracción de datos, **extraer texto de PDF** como cadenas simples es el formato posterior más limpio.

## Paso 3: Cargar el PDF desde un flujo de archivo (cargar PDF desde un flujo)

Cargar un PDF desde un flujo es un patrón eficiente en memoria —evitas cargar todo el archivo en RAM de una vez. Esto es especialmente útil al trabajar con documentos grandes de varias páginas.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **¿Qué pasa si el archivo está en S3 u otro bucket en la nube?**  
> Simplemente reemplaza `from_file` con un método que acepte un búfer de bytes (p. ej., `ImageStream.from_bytes(s3_object.read())`). El resto del pipeline permanece idéntico.

## Paso 4: Ejecutar OCR en todas las páginas (procesar PDF escaneado)

Ahora comienza el trabajo pesado. El motor iterará por cada página, ejecutará el motor de reconocimiento y devolverá una lista de objetos página —cada uno exponiendo su contenido textual.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Detrás de escena, la biblioteca OCR descomprime cada página PDF, la rasteriza al DPI configurado y alimenta el mapa de bits a través de su modelo de red neuronal. ¿El resultado? Una colección de objetos `Page` listos para la extracción.

## Paso 5: Recuperar y mostrar el texto reconocido (convertir PDF a texto)

Finalmente, iteramos sobre las páginas devueltas e imprimimos el texto reconocido. Este es el momento en que **convertir PDF a texto** realmente ocurre.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Salida esperada

Si `multipage.pdf` contiene tres páginas escaneadas, verás algo como:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Observa la separación clara entre páginas —útil si necesitas almacenar el texto de cada página en una base de datos o alimentarlo a un modelo NLP posterior.

## Manejo de casos límite comunes

### 1. PDFs con capas mixtas de imagen y texto

Algunos PDFs ya contienen una capa de texto oculta (p. ej., exportado desde Word). Si deseas que el motor OCR **ignore el texto existente** y vuelva a procesar la imagen, establece:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Archivos grandes que superan los límites de memoria

Al trabajar con PDFs de varios gigabytes, considera procesarlos en fragmentos:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Soporte de idioma y tipografía

Si tus documentos escaneados están en francés o contienen caracteres especiales, indica al motor qué modelo de idioma usar:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Script completo – listo para ejecutar

A continuación se muestra el ejemplo completo y ejecutable que une todas las piezas. Guárdalo como `ocr_pdf.py` y ejecuta `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Ejecutar el script** imprimirá el texto de cada página en la consola, exactamente como se muestra en la sección “Salida esperada”. Desde aquí puedes redirigir la salida a un archivo:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Conclusión

Acabamos de cubrir **cómo hacer OCR de PDF** en Python de principio a fin. Configurando el motor, cargando el documento mediante un flujo e iterando sobre cada página reconocida, puedes **extraer texto de PDF**, **convertir PDF a texto** y **procesar PDF escaneado** con solo unas cuantas líneas. El enfoque escala desde pequeñas facturas de dos páginas hasta enormes archivos de cientos de páginas.

¿Qué sigue? Intenta alimentar las cadenas extraídas a un índice de búsqueda, a un resumidor de modelo de lenguaje o a un pipeline de validación de datos. También puedes experimentar con formatos de salida como JSON para conservar metadatos posicionales para análisis avanzado de documentos.

¿Tienes preguntas sobre cómo manejar PDFs encriptados o integrar con almacenamiento en la nube? Deja un comentario abajo — ¡feliz codificación! 

![Diagrama que muestra el flujo de trabajo OCR PDF – cómo hacer OCR de PDF, cargar PDF desde un flujo, reconocer páginas y extraer texto](ocr-pdf-workflow.png "diagrama del flujo de trabajo cómo hacer OCR de PDF")

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo hacer OCR de PDF en .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo extraer texto de una imagen usando Aspose.OCR para .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Cómo extraer texto de archivos ZIP usando Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}