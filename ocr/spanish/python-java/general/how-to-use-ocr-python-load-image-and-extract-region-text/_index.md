---
category: general
date: 2026-06-25
description: Cómo usar OCR en Python – aprende a cargar una imagen para OCR, reconocer
  texto en una región y extraer rápidamente el texto de la región.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: es
og_description: 'Cómo usar OCR en Python: guía paso a paso para cargar una imagen,
  reconocer texto en una región específica y extraer el número de factura.'
og_title: 'Cómo usar OCR en Python: cargar imagen y extraer texto de la región'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Cómo usar OCR en Python: cargar imagen y extraer texto de la región'
url: /es/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR en Python: Cargar imagen y extraer texto de la región

**Cómo usar OCR en Python** es más sencillo de lo que piensas. ¿Alguna vez has mirado una factura escaneada y te has preguntado cómo obtener solo el número de factura sin analizar toda la página? No estás solo: muchos desarrolladores se topan con ese problema cuando se inician con el reconocimiento óptico de caracteres. En esta guía recorreremos cómo cargar una imagen para OCR, definir un rectángulo, reconocer texto en esa región y, finalmente, extraer el texto de la región. Al final tendrás un script listo‑para‑ejecutar que aísla cualquier fragmento de texto que necesites.

> *Consejo profesional:* Si trabajas con PDFs, conviértelo primero a una imagen página por página; la mayoría de las bibliotecas OCR manejan mejor PNG/JPEG.

## Lo que necesitarás

- Python 3.8+ (se recomienda la última versión estable)  
- Una biblioteca OCR que exponga una clase `OcrEngine` (p. ej., **ocr** de `pip install ocr-lib`)  
- Una imagen de ejemplo—aquí usaremos `invoice.png` ubicada en una carpeta que controles  
- Familiaridad básica con rectángulos (x, y, ancho, alto)  

Sin dependencias pesadas, sin GPU requerida—solo trabajo en CPU, lo que mantiene la portabilidad.

---

## Cómo usar OCR: Inicializar el motor (Paso 1)

Antes de que se pueda leer cualquier texto, necesitas una instancia del motor OCR. Piensa en él como el cerebro que analizará los patrones de píxeles.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Por qué es importante:* Inicializar el motor carga los modelos de idioma y establece configuraciones predeterminadas. Omitir este paso provocaría una excepción en el momento en que llames a `recognize_region`.

---

## Cargar imagen para OCR (Paso 2)

Ahora que el motor está listo, le suministramos una imagen. El método `Image.load` de la biblioteca maneja formatos comunes y normaliza el mapa de bits.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Si el archivo no se encuentra, Python lanzará un `FileNotFoundError`. Asegúrate de que la ruta sea absoluta o relativa al directorio de trabajo de tu script.  

*Caso extremo:* Algunos motores OCR esperan una imagen en escala de grises. Si notas una precisión pobre, convierte la imagen primero:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Reconocer texto en la región (Paso 3)

Definir la región es donde le indicas al motor *dónde* buscar. El `Rectangle` acepta valores de punto flotante para precisión subpíxel, lo cual puede ser útil al trabajar con escaneos de alta resolución.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – esquina superior izquierda del rectángulo (en píxeles)  
- **width, height** – tamaño del cuadro  

Quizás te preguntes cómo obtener esos números. Una forma rápida es abrir la imagen en cualquier editor (p. ej., GIMP o Paint.NET) y usar la herramienta de selección para leer las coordenadas.  

*¿Por qué no OCRizar toda la página?* Limitar el área reduce el ruido, acelera el procesamiento y mejora drásticamente la precisión para campos pequeños como números de factura.

---

## Cómo extraer texto de la región (Paso 4)

Con la región establecida, pide al motor que reconozca solo esa porción. El objeto resultante contiene el texto bruto y las puntuaciones de confianza.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Si el motor OCR admite varios idiomas, puedes pasar un código de idioma opcional:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Trampa común:* Algunos motores devuelven una lista de palabras en lugar de una única cadena. En esos casos, concaténalas:

```python
text = " ".join(region_result.words)
```

---

## Mostrar el número de factura extraído (Paso 5)

Finalmente, imprime—o guarda—el texto extraído. También puedes post‑procesar la cadena para eliminar espacios en blanco sobrantes o caracteres no numéricos.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Ejecutar el script con un rectángulo correctamente alineado debería producir algo como:

```
Invoice number: 20231578
```

Si obtienes caracteres basura, verifica nuevamente las coordenadas del rectángulo o considera aumentar la resolución de la imagen.

---

## Ejemplo completo funcional

Juntando todo, aquí tienes un script autocontenido que puedes copiar‑pegar y ejecutar:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Guarda el archivo como `extract_invoice.py`, reemplaza `YOUR_DIRECTORY` con la carpeta real y ejecuta:

```bash
python extract_invoice.py
```

Deberías ver el número de factura impreso en la consola.

---

## Preguntas frecuentes

**P: ¿Qué pasa si el número de factura está impreso en una tipografía elegante?**  
R: La mayoría de los motores OCR modernos manejan una amplia gama de fuentes, pero puedes mejorar la precisión entrenando un modelo de idioma personalizado o pre‑procesando la imagen (p. ej., aplicando un filtro de umbral).

**P: ¿Puedo extraer varios campos a la vez?**  
R: Claro. Define una lista de objetos `Rectangle`—uno por campo—y recorre la lista, almacenando cada resultado en un diccionario.

**P: ¿Esto funciona con PDFs de varias páginas?**  
R: Convierte cada página a una imagen primero (usando `pdf2image` o similar), luego aplica la misma extracción basada en regiones por página.

---

## Conclusión

En este tutorial cubrimos **cómo usar OCR** en Python para cargar una imagen, reconocer texto en una región específica y extraer el texto de esa región—ideal para obtener números de factura, IDs de orden o cualquier fragmento pequeño de datos de documentos escaneados. Al aislar el área de interés ganas velocidad, precisión y menos trabajo de post‑procesamiento.

¿Listo para el siguiente paso? Prueba a extender el script para manejar **cargar imagen para OCR** desde una carpeta de facturas por lotes, o experimenta con **reconocer texto en la región** para campos diferentes como fechas y totales. El mismo patrón se aplica—solo cambia las coordenadas del rectángulo.

Si encontraste algún problema o tienes ideas de mejora, deja un comentario abajo. ¡Feliz codificación, y que tus pipelines de OCR sean siempre precisas!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de una imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cómo extraer texto de una imagen preparando rectángulos en OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Cómo usar AspOCR: filtros de preprocesamiento de imagen OCR para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}