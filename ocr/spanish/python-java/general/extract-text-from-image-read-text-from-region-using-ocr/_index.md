---
category: general
date: 2026-07-05
description: Extrae texto de una imagen usando OCR en Python. Aprende cómo cargar
  la imagen para OCR, leer texto de una región y extraer texto de una factura con
  unas pocas líneas de código.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: es
og_description: Extrae texto de una imagen con OCR en Python. Esta guía muestra cómo
  cargar la imagen para OCR, leer texto de una región y extraer texto de una factura
  rápidamente.
og_title: Extraer texto de una imagen – Leer texto de una región usando OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extraer texto de la imagen – Leer texto de una región usando OCR
url: /es/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de una imagen – Leer texto de una región usando OCR

¿Alguna vez necesitaste **extraer texto de una imagen** pero solo una parte específica importa, como el total de una factura? No eres el único. En muchos proyectos del mundo real te encontrarás necesitando **leer texto de una región** en lugar de analizar toda la imagen. Afortunadamente, con unas pocas líneas de Python puedes cargar una imagen para OCR, definir una región de interés (ROI) y obtener exactamente los caracteres que necesitas.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra cómo **cargar imagen para OCR**, configurar una ROI y finalmente **extraer texto de una factura**. Al final tendrás un fragmento listo para usar que funciona con cualquier biblioteca OCR popular que admita reconocimiento basado en regiones.

---

## Lo que necesitarás

- Python 3.8+ (el código también funciona en 3.10)  
- Un paquete OCR que exponga una clase `OcrEngine` (para la demo usaremos un módulo ficticio `ocr`; sustitúyelo por `pytesseract`, `easyocr` o cualquier biblioteca que ofrezca soporte ROI)  
- Una imagen de ejemplo —p. ej., `invoice.png`— que contenga texto impreso y claro  
- Familiaridad básica con funciones y clases de Python (no se requiere experiencia en deep learning)

Si ya tienes todo, genial —¡vamos al grano! Si no, descarga la última versión de Python desde python.org e instala el paquete OCR con `pip install your-ocr-lib`.

---

![Ejemplo de extracción de texto de una imagen](extract-text-from-image.png "Extracción de texto de una imagen – demostración de OCR basada en regiones")

*La imagen anterior ilustra la región (rectángulo rojo) que apuntaremos para **extraer texto de una imagen**.*

---

## Paso 1: Instalar e importar la biblioteca OCR

Primero, asegúrate de que la biblioteca OCR esté disponible en tu entorno. El patrón de importación a continuación funciona para la mayoría de los paquetes que exponen una clase de alto nivel `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Consejo:** Si usas `pytesseract`, deberás instalar el binario de Tesseract por separado y establecer `pytesseract.pytesseract.tesseract_cmd` con su ruta.

---

## Paso 2: Crear el motor OCR y establecer el idioma

Crear el motor es sencillo, pero especificar el idioma mejora drásticamente la precisión, especialmente en facturas que contienen números y palabras en inglés.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

¿Por qué hacemos esto? El motor OCR utiliza modelos de idioma para predecir caracteres; indicarle que espere inglés reduce falsos positivos como confundir “0” con “O”.

---

## Paso 3: Cargar la imagen para OCR

Ahora realmente **cargamos la imagen para OCR**. La mayoría de las bibliotecas aceptan una ruta de archivo o un objeto de imagen Pillow. Aquí usamos el cargador incorporado de la biblioteca por simplicidad.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Asegúrate de que la ruta apunte al directorio correcto; un error común es olvidar la ruta relativa cuando el script se ejecuta desde un directorio de trabajo diferente.

---

## Paso 4: Definir la región de interés (ROI)

Definir la ROI es el corazón de **leer texto de una región**. Piensa en ello como dibujar un rectángulo alrededor de la parte de la factura que contiene el total.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` y `top` representan las coordenadas X e Y de la esquina superior izquierda del rectángulo.  
- `width` y `height` establecen el tamaño del cuadro.  
- Puedes experimentar con diferentes valores usando un visor de imágenes que muestre coordenadas de píxeles.

> **Por qué la ROI importa:** Ejecutar OCR en toda la página desperdicia ciclos de CPU y a menudo introduce ruido de texto, tablas o gráficos no relacionados. Al enfocarte en una región, obtienes resultados más limpios y un procesamiento más rápido.

---

## Paso 5: Realizar OCR en la región especificada

Con todo configurado, finalmente **extraemos texto de la imagen**, pero solo dentro de la ROI que definimos.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

El método `recognize` devuelve un objeto que típicamente contiene la cadena cruda, puntuaciones de confianza y, a veces, cajas delimitadoras para cada palabra. Para nuestro propósito solo necesitamos el texto plano.

---

## Paso 6: Mostrar el texto extraído

Imprimamos el resultado y veamos qué obtuvimos. Este paso demuestra **extraer texto de una factura** en un escenario real.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Salida esperada

```
Text inside ROI:
Total Amount: $1,245.67
```

Si tu factura usa un diseño diferente, verás cualquier texto que se encuentre dentro del rectángulo —quizá un número de factura, fecha o referencia de orden de compra.

---

## Paso 7: Encapsular todo en una función reutilizable (Opcional)

Para que la solución sea reutilizable en múltiples facturas, encapsula la lógica en una función. Esto también ilustra **ocr on region** como una utilidad genérica.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Ahora puedes llamar a la función con cualquier factura:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Salida en blanco** | La ROI no cubre realmente ningún texto (coordenadas incorrectas). | Verifica los valores de píxeles con un editor de imágenes; añade una superposición visual de depuración. |
| **Caracteres basura** | Baja resolución de la imagen o bajo contraste. | Preprocesa la imagen: conviértela a escala de grises, aplica umbralado (`cv2.threshold`). |
| **Idioma incorrecto** | El motor usa por defecto un idioma que no contiene el conjunto de caracteres necesario. | Establece explícitamente `ocr_engine.language` a `ENGLISH` o la localidad apropiada. |
| **Retardo de rendimiento** | Ejecutar OCR en imágenes grandes repetidamente. | Redimensiona la imagen antes de cargarla, o procesa solo la ROI recortándola primero. |

---

## Extender el ejemplo: Múltiples ROIs

A veces una factura contiene varios campos que necesitas —por ejemplo, **extraer texto de una factura** tanto para el total como para la fecha. Puedes iterar sobre una lista de rectángulos:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Este patrón mantiene tu código limpio y facilita añadir más regiones más adelante.

---

## Conclusión

Acabamos de cubrir un flujo de trabajo completo, de extremo a extremo, para **extraer texto de una imagen** usando OCR en Python, centrándonos en una región específica. Al **cargar la imagen para OCR**, definir una **región de interés** y llamar al motor, puedes leer texto de manera fiable desde una región —ideal para extraer totales de facturas, fechas de recibos o cualquier otro dato localizado.

Siéntete libre de experimentar


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de una imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraer texto de una imagen – Optimización OCR con Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Cómo extraer texto de una imagen preparando rectángulos en OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}