---
category: general
date: 2026-06-19
description: Cómo extraer PDF usando OCR en Python – tutorial paso a paso que cubre
  extraer texto de PDF, reconocer texto de una imagen y un ejemplo de OCR en Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: es
og_description: Cómo extraer PDF usando OCR en Python. Aprende a extraer texto de
  PDF, reconocer texto de una imagen y ver un ejemplo completo de OCR en Python.
og_title: Cómo extraer texto de PDF con OCR en Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Cómo extraer texto de PDF con OCR en Python – Guía completa
url: /es/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer texto de PDF con OCR en Python – Guía completa

¿Alguna vez te has preguntado **cómo extraer PDF** cuando el archivo es solo una imagen escaneada? No eres el único. En muchos proyectos del mundo real —piensa en contratos, facturas o archivos históricos— el PDF que recibes no tiene texto seleccionable. ¿La buena noticia? Unas pocas líneas de Python pueden convertir esas páginas solo de imagen en texto buscable y editable.

En este tutorial recorreremos un **ejemplo de OCR en Python** que lee un PDF, renderiza su primera página como una imagen y luego **extrae texto de PDF** usando un motor OCR. Al final sabrás exactamente cómo **leer PDF con OCR**, por qué cada paso es importante y cómo adaptar el código para documentos multipágina o diferentes idiomas.

## Qué aprenderás

- Instalar y configurar una biblioteca OCR fiable para Python.  
- Convertir páginas PDF a imágenes aptas para OCR.  
- **Reconocer texto de imagen** y obtener cadenas Unicode limpias.  
- Trampas comunes (PDFs de baja resolución, páginas rotadas) y cómo evitarlas.  
- Extender el script para manejar varias páginas o procesamiento por lotes.

**Requisitos previos**: Python 3.8+, pip y un entendimiento básico de entornos virtuales. No se necesita experiencia previa en OCR —solo sigue los pasos.

---

## ## Cómo extraer texto de PDF con OCR en Python

Este encabezado H2 contiene nuestra palabra clave principal justo donde a los motores de búsqueda les encanta verla. Vamos directo al código.

### Paso 1 – Instalar los paquetes requeridos

Primero, necesitamos un motor OCR. El ejemplo a continuación usa el popular paquete **ocr** (un contenedor ligero alrededor de Tesseract). Si prefieres otro backend, los conceptos siguen siendo los mismos.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Consejo profesional:** En Linux, también necesitarás el binario de Tesseract: `sudo apt-get install tesseract-ocr`. Los usuarios de macOS pueden obtenerlo vía Homebrew: `brew install tesseract`.

### Paso 2 – Inicializar el motor OCR y establecer el idioma

Ahora iniciamos el motor y le indicamos que busque caracteres en inglés. Puedes cambiar `ocr.Language.English` por cualquier código de idioma soportado.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Por qué es importante:** Especificar el idioma mejora drásticamente la precisión porque el motor puede aplicar diccionarios y modelos de caracteres específicos del idioma.

### Paso 3 – Cargar una página PDF como imagen

OCR funciona sobre imágenes raster, no sobre objetos PDF. El ayudante `ocr.Image.from_pdf` renderiza la página elegida a un mapa de bits. Ajusta `page_number` para otras páginas (indexado desde 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Caso límite:** Si el PDF contiene gráficos vectoriales en lugar de imágenes escaneadas, podrías obtener un renderizado nítido. Para escaneos de baja resolución, considera aumentar el DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Paso 4 – Reconocer texto de la imagen renderizada

Este es el corazón del **ejemplo de ocr python**. El motor procesa el mapa de bits y devuelve un objeto que contiene la cadena extraída.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

El atributo `ocr_result.text` contiene la salida de texto plano, preservando los saltos de línea donde sea posible.

### Paso 5 – Imprimir o almacenar el texto extraído

Finalmente, mostramos el resultado. En una aplicación real probablemente escribirías a un archivo o a una base de datos.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Ejecutar el script debería mostrar algo como:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Ese es un flujo completo de **extraer texto de pdf** usando OCR.

---

## ## Reconocer texto de imagen – Ajustando la precisión

Si solo te interesa **reconocer texto de imagen** (por ejemplo, un JPEG de un recibo), puedes omitir el paso de conversión PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Consejos para obtener mejores resultados:**

- **Pre‑procesar** la imagen: convertir a escala de grises, aplicar umbralado o corregir la inclinación. Pillow facilita esto.
- **Aumentar DPI** durante el renderizado del PDF: mayor resolución brinda más detalle al motor OCR.
- **Activar la configuración del motor OCR** para segmentación de página (`ocr_engine.config = "--psm 6"` para bloques uniformes).

---

## ## Leer PDF con OCR – Manejo de múltiples páginas

La mayoría de los contratos abarcan varias páginas. Recorrer cada página es sencillo:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Esta función **lee PDF con OCR**, concatena la salida e inserta un marcador de salto de página claro. Luego puedes pasar `full_text` a un índice de búsqueda o guardarlo como archivo `.txt`.

---

## ## Trampas comunes y cómo solucionarlas

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| Caracteres distorsionados, muchos `?` | Idioma incorrecto o faltan archivos de datos del idioma | Instala el paquete de idioma correcto de Tesseract (`tesseract-ocr-<lang>`) y establece `ocr_engine.language`. |
| Falta de líneas o palabras truncadas | DPI bajo (menos de 150) | Renderiza el PDF a 300 DPI o más (`dpi=300`). |
| El texto está rotado o al revés | Página escaneada no está orientada correctamente | Usa `ocr.Image.deskew(page_image)` antes del reconocimiento. |
| Procesamiento lento en PDFs grandes | Procesar páginas secuencialmente en un solo hilo | Paraleliza con `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Extender el ejemplo OCR en Python

- **Exportar a PDF/A**: Después de la extracción, puedes incrustar el texto de nuevo en un PDF buscable usando `reportlab` o `pypdf2`.
- **Detección de idioma**: Usa `langdetect` sobre la salida OCR para cambiar `ocr_engine.language` dinámicamente.
- **Procesamiento por lotes**: Recorre un directorio con `os.listdir` y aplica `extract_all_pages` a cada archivo.

---

## ## Resultado esperado y verificación

Cuando ejecutes el script contra un escaneo claro en inglés, deberías ver un bloque limpio de texto con puntuación correcta. Verifica mediante:

1. Comparar algunas líneas con la imagen escaneada original.  
2. Ejecutar un simple recuento de palabras (`len(ocr_result.text.split())`) para asegurar que la salida no esté vacía.  
3. Opcionalmente, pasar el resultado a un corrector ortográfico como `pyspellchecker` para detectar errores de OCR.

---

## Conclusión

Hemos cubierto **cómo extraer PDF** cuando el análisis tradicional falla, demostrado un **ejemplo completo de ocr python**, y explicado cómo **reconocer texto de imagen** y **leer PDF con OCR** tanto para escenarios de una sola página como multipágina. Con los fragmentos de código anteriores ahora puedes convertir cualquier PDF escaneado en texto buscable y editable—sin necesidad de volver a escribir manualmente.

¿Próximos pasos? Prueba cambiar el idioma a español (`ocr.Language.Spanish`) o experimenta con técnicas de pre‑procesamiento de imágenes para mejorar la precisión. Si estás construyendo un sistema de gestión documental, considera indexar el texto extraído con Elasticsearch para búsquedas ultrarrápidas.

¿Tienes preguntas o te encuentras con un PDF problemático? ¡Deja un comentario y feliz codificación!  

![Cómo extraer PDF usando OCR en Python](image.png "Cómo extraer PDF usando OCR en Python")

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Reconocer texto PDF – Operaciones OCR con Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [Extraer texto de imagen en C# con selección de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}