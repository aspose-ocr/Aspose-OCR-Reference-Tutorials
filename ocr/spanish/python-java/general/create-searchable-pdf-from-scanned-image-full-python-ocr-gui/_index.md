---
category: general
date: 2026-07-05
description: Crea PDF buscable con Python. Aprende cómo hacer OCR a un PNG escaneado,
  convertir un PDF de imagen escaneada y obtener un PDF buscable en minutos.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: es
og_description: Crea PDF buscable rápidamente. Esta guía muestra cómo hacer OCR a
  un PNG, convertir un PDF de imagen escaneada y producir un PDF buscable usando Python.
og_title: Crear PDF buscable a partir de una imagen escaneada – Tutorial de OCR en
  Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Crear PDF buscable a partir de imagen escaneada – Guía completa de OCR en Python
url: /es/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF buscable a partir de una imagen escaneada – Guía completa de OCR en Python

¿Alguna vez te has preguntado cómo **crear un PDF buscable** a partir de una foto escaneada sin pagar por software costoso? No estás solo. En muchas oficinas, los PDFs llegan como imágenes planas—difíciles de buscar, imposibles de copiar‑pegar y una pesadilla para auditorías de cumplimiento. ¿La buena noticia? Con unas pocas líneas de Python puedes convertir ese PNG estático en un PDF completamente buscable, y el proceso es más sencillo de lo que piensas.

En este tutorial recorreremos un **ejemplo completo de reconocimiento OCR**, cubriendo todo desde la instalación de la biblioteca adecuada hasta la escritura del archivo PDF final. Al final sabrás exactamente cómo **convertir PDFs de imágenes escaneadas**, cómo **ocr pdf programáticamente**, y tendrás un script reutilizable que puedes incorporar en cualquier proyecto.

## Lo que aprenderás

- Instalar y configurar una biblioteca OCR para Python (usaremos `pytesseract` y `pdf2image`).
- Inicializar el motor OCR y establecer el idioma.
- Cargar un PNG escaneado (o cualquier imagen) y ejecutar OCR sobre él.
- Convertir el resultado del OCR en un **PDF buscable** (array de bytes) y guardarlo.
- Consejos para manejar documentos multipágina, diferentes idiomas y errores comunes.

No se requiere experiencia previa con OCR—solo un entorno Python 3 funcional y un poco de curiosidad.

---

## Crear PDF buscable – Visión general

A continuación se muestra un diagrama de flujo de alto nivel de los pasos que implementaremos.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: Create searchable PDF workflow diagram showing engine init, image load, OCR recognition, PDF conversion, and file write.*

---

## Paso 1: Inicializar el motor OCR (how to ocr pdf)

¿Por qué necesitamos inicializar algo? El motor OCR es el cerebro que interpreta patrones de píxeles como caracteres. Al crear una instancia del motor y establecer explícitamente el idioma, le decimos a la biblioteca qué alfabeto esperar, lo que mejora drásticamente la precisión.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Consejo profesional:** Si necesitas OCR en varios idiomas, instala los paquetes de idioma correspondientes para Tesseract y pasa una lista como `"eng+spa"` a `ocr_language`.

---

## Paso 2: Cargar la imagen escaneada (convert scanned image pdf)

La siguiente pieza del rompecabezas es obtener los datos de la imagen en Python. Ya sea que tengas un PNG único o un TIFF multipágina, la clase `PIL.Image` puede abrirlo. Si partes de un PDF que ya contiene imágenes escaneadas, `pdf2image` convertirá cada página en una imagen para nosotros.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Por qué importa:** Cargar la imagen como un objeto Pillow nos da acceso a sus datos de píxeles crudos, que el motor OCR necesita. Omitir este paso y alimentar bytes sin procesar provocaría errores.

---

## Paso 3: Realizar reconocimiento OCR en la imagen (ocr recognition example)

Ahora la parte divertida—dejar que el motor lea el texto. `pytesseract.image_to_pdf_or_hocr` devuelve un flujo de bytes PDF que ya contiene una capa de texto invisible, que es exactamente lo que necesitamos para un **PDF buscable**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Caso límite:** Si tu imagen tiene bajo contraste, considera aplicar un umbral simple antes del OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Este pequeño paso de preprocesamiento puede aumentar la precisión de forma notable.

---

## Paso 4: Escribir los bytes PDF en un archivo (convert png searchable pdf)

La biblioteca OCR nos entrega un array de bytes—piénsalo como el contenido crudo de un archivo PDF. Todo lo que necesitamos ahora es escribir esos bytes en disco.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Lo que verás:** Abre el archivo resultante en cualquier visor de PDF y prueba buscar una palabra que sabes que aparece en la imagen original. El resaltado debería saltar directamente a la ubicación, demostrando que la capa de texto invisible funciona.

---

## Paso 5: Extender a documentos multipágina (convert scanned image pdf)

Los contratos del mundo real a menudo abarcan varias páginas. Para **convertir PDFs de imágenes escaneadas** que contienen varias páginas, recorre cada página, realiza OCR y concatena los PDFs resultantes.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Por qué combinar:** Cada llamada a `image_to_pdf_or_hocr` produce un PDF independiente. Fusionarlos asegura que el documento final preserve el orden original de las páginas.

---

## Errores comunes y cómo solucionarlos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| No hay texto buscable al abrir el PDF | Tesseract no encuentra caracteres (salida en blanco) | Verifica la calidad de la imagen, aumenta DPI o aplica preprocesamiento (contraste, binarización). |
| Caracteres corruptos (p. ej., �) | Paquete de idioma incorrecto o fuentes faltantes | Instala los datos de idioma correctos (`tesseract‑lang‑eng`) y asegura que `ocr_language` coincida. |
| Tamaño del archivo PDF enorme (>10 MB para una imagen de una página) | Uso de PNG sin pérdida como fuente; OCR agrega una imagen de alta resolución | Reduce la escala de la imagen antes del OCR (`image.thumbnail((1240, 1754))` para A4). |
| El script falla en Windows con “tesseract.exe not found” | Binario de Tesseract no está en PATH | Añade `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (ajusta la ruta). |

---

## Script completo, listo para ejecutar

Juntando todo, aquí tienes un archivo único que puedes copiar‑pegar y ejecutar:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Guárdalo como `create_searchable_pdf.py`, reemplaza los marcadores de posición con rutas reales y ejecuta:

```bash
python create_searchable_pdf.py
```

Deberías ver un


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo hacer OCR de PDF en .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convertir imágenes a PDF en C# – Guardar resultado OCR multipágina](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Reconocimiento OCR de documentos PDF en Aspose.OCR para Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}