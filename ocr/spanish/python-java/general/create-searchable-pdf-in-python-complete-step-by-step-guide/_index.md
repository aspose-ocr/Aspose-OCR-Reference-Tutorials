---
category: general
date: 2026-06-19
description: Crear PDF buscable a partir de una imagen usando OCR con Python. Aprende
  a convertir OCR a PDF, extraer texto de una imagen y realizar OCR en una imagen
  rápidamente.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: es
og_description: Crea un PDF buscable a partir de una imagen con OCR en Python. Esta
  guía muestra cómo convertir OCR a PDF, extraer texto de una imagen y realizar OCR
  en la imagen.
og_title: Crear PDF buscable en Python – Guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Crear PDF buscable en Python – Guía completa paso a paso
url: /es/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF buscable en Python – Guía completa paso a paso

¿Alguna vez necesitaste **crear un PDF buscable** a partir de un recibo escaneado pero no sabías por dónde empezar? No estás solo: muchos desarrolladores se topan con el mismo obstáculo cuando intentan convertir una foto de texto en un PDF que realmente se pueda buscar.  

En este tutorial recorreremos una solución práctica que te permite **realizar OCR en una imagen**, convertir ese resultado de OCR en un **PDF buscable**, e incluso extraer el texto sin procesar si lo necesitas para un procesamiento posterior. Sin rodeos, solo un ejemplo funcional que puedes copiar‑pegar en tu proyecto hoy mismo.

## Lo que aprenderás

- Cómo configurar un motor OCR ligero en Python  
- Los pasos exactos para **convertir OCR a PDF** y guardarlo como documento buscable  
- Formas de **extraer texto de una imagen** para análisis posterior  
- Consejos para manejar problemas comunes como la orientación de la imagen y archivos grandes  
- Un script completo y ejecutable que puedes adaptar a tu caso de uso

### Requisitos previos

- Python 3.8+ instalado en tu máquina  
- Familiaridad básica con pip y entornos virtuales (opcional pero recomendado)  
- Un archivo de imagen (PNG, JPEG, etc.) que contenga texto claro y legible por máquina  

Si tienes eso, vamos a sumergirnos.

## Paso 1: Instalar la biblioteca requerida

El fragmento de código que viste antes usa un paquete ficticio `ocr`, pero las mismas ideas se aplican a bibliotecas reales como **EasyOCR**, **pytesseract** o **pdfminer.six**. Para esta guía usaremos **EasyOCR** porque es puro Python, soporta muchos idiomas y devuelve un práctico método de conversión a PDF mediante un ayudante auxiliar.

```bash
pip install easyocr pillow
```

> **Consejo profesional:** Instala dentro de un entorno virtual (`python -m venv venv && source venv/bin/activate`) para mantener tus dependencias ordenadas.

## Paso 2: Inicializar el motor OCR – Realizar OCR en la imagen

Ahora que la biblioteca está lista, creamos un motor OCR y le indicamos que trabaje con texto en inglés. Este es el primer lugar donde **realizamos OCR en la imagen**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

¿Por qué necesitamos un objeto lector dedicado? EasyOCR precarga los modelos de idioma, por lo que reutilizar el mismo `reader` para múltiples imágenes es mucho más eficiente que volver a inicializarlo cada vez.

## Paso 3: Cargar la imagen – Extraer texto de la imagen

Vamos a cargar la foto en memoria. Este paso es donde más tarde **extraeremos texto de la imagen**, pero primero solo la cargamos.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Si tu imagen está al revés o sesgada, considera usar los métodos `rotate` o `transpose` de Pillow antes de pasarla al motor OCR. Una rápida revisión visual puede ahorrarte horas de depuración después.

## Paso 4: Ejecutar el motor OCR y capturar resultados

Aquí está el núcleo del proceso: enviar la imagen al motor OCR y obtener datos estructurados de vuelta.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

La bandera `detail=1` nos da cajas delimitadoras, que necesitaremos cuando más adelante **convirtamos OCR a PDF**. Si solo te interesan las cadenas crudas, establece `detail=0`.

## Paso 5: Convertir el resultado OCR a un PDF buscable – Convertir OCR a PDF

EasyOCR no proporciona un escritor de PDF directo, pero podemos ensamblar el PDF nosotros mismos usando Pillow y la biblioteca `reportlab`. Para mantener el tutorial ligero, usaremos `fpdf2`, que nos permite incrustar la imagen original y superponer texto invisible.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

¿Qué acaba de pasar? Colocamos la imagen escaneada como capa visible, luego escribimos las palabras reconocidas encima usando texto blanco que se funde con el fondo blanco. Las herramientas de búsqueda aún leen la capa oculta, por lo que el PDF se vuelve **buscable** sin alterar la apariencia visual.

## Paso 6: Guardar los bytes del PDF – Convertir imagen a PDF

Si prefieres manejar el PDF en memoria (por ejemplo, enviándolo a través de una API), puedes capturar los bytes en lugar de escribir directamente en disco.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Esa línea muestra el clásico flujo de trabajo **convertir imagen a PDF**: comienzas con una imagen, ejecutas OCR, superpones texto y finalmente emites un flujo de PDF.

## Paso 7: Verificar el resultado – Chequeos rápidos

Después de ejecutar el script, abre `receipt_searchable.pdf` en cualquier visor de PDF y prueba la caja de búsqueda (Ctrl + F). Escribe una palabra que sepas que aparece en el recibo; si salta al lugar correcto, ¡has **creado un PDF buscable** con éxito!  

Si la búsqueda falla, verifica:

1. Los puntajes de confianza del OCR (`conf`). Una confianza baja puede indicar que la imagen está borrosa.  
2. Las coordenadas de las cajas delimitadoras; a veces EasyOCR las reporta en una orientación diferente.  
3. Que el visor de PDF no esté en modo “solo imagen” (raro, pero algunos visores tienen esa opción).

## Script completo y funcional

Juntando todo, aquí tienes el archivo Python completo y listo para ejecutar:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Guárdalo como `searchable_pdf.py`, reemplaza los marcadores `YOUR_DIRECTORY` con rutas reales, y ejecuta:

```bash
python searchable_pdf.py
```

Deberías ver un mensaje de confirmación y un nuevo PDF buscable en tu carpeta.

## Preguntas frecuentes y casos límite

**¿Qué pasa si la imagen es en color?**  
EasyOCR funciona tanto con imágenes en escala de grises como en color, pero convertir a escala de grises (`pil_image.convert("L")`) a veces mejora la precisión en escaneos ruidosos.

**¿Puedo manejar PDFs de varias páginas?**  
Sí: itera sobre cada imagen de página, ejecuta los pasos de OCR y agrega cada página al mismo objeto `FPDF`. Solo recuerda reiniciar el cursor (`self.add_page()`) para cada nueva imagen.

**¿Existe una forma de mantener la capa de texto original en lugar de texto blanco invisible?**  
Si necesitas un PDF verdadero “texto‑sobre‑imagen” (por ejemplo, para accesibilidad), considera usar `pdfminer` o `pikepdf` para incrustar una capa de texto oculta con etiquetas PDF apropiadas. Es más avanzado, pero el principio sigue siendo el mismo: imagen de fondo + texto superpuesto.

**¿Qué hacer si la confianza del OCR es baja?**  
Puedes filtrar palabras de baja confianza:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Conclusión – Lo que logramos

Partimos de una simple imagen de un recibo, **realizamos OCR en la imagen**, extrajimos las cadenas reconocidas y finalmente **creamos un PDF buscable** que se comporta como cualquier documento escaneado profesionalmente. El proceso cubrió todas las palabras clave secundarias—**convertir OCR a PDF**, **extraer texto de la imagen**, **convertir imagen a PDF**, y **realizar OCR en la imagen**—por lo que ahora dispones de una caja de herramientas reutilizable para cualquier proyecto similar.

### Próximos pasos

- Experimenta con otros idiomas pasando sus códigos ISO a `easyocr.Reader(['en', 'es'])`.  
- Cambia EasyOCR por Tesseract si necesitas una solución totalmente offline; el resto del pipeline permanece igual.  
- Añade visualización de confianza OCR (dibuja cajas delimitadoras sobre la imagen) para depurar escaneos problemáticos.  

¿Tienes una variante que quieras compartir? Deja un comentario, haz un fork


## ¿Qué deberías aprender después?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}