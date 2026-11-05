---
category: general
date: 2026-06-22
description: Realiza OCR en una imagen usando Python en solo unas pocas líneas. Aprende
  cómo cargar la imagen para OCR, reconocer texto de un PNG y usar el motor OCR de
  manera eficiente.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: es
og_description: Realiza OCR en una imagen rápidamente con Python. Este tutorial muestra
  cómo cargar la imagen para OCR, reconocer texto de un PNG y usar el motor OCR con
  confianza.
og_title: Realiza OCR en una imagen con Python – Guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Realizar OCR en una imagen con Python – Guía completa
url: /es/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR en Imagen con Python – Guía Completa

¿Alguna vez necesitaste **realizar OCR en una imagen** archivos pero te quedaste atascado en la primera línea de código? No estás solo. En este tutorial te mostraremos exactamente cómo **cargar imagen para OCR**, configurar un **OCR engine** liviano y, finalmente, **reconocer texto de PNG** con solo unas pocas instrucciones.

Cubrirémos todo, desde la instalación de la biblioteca hasta ajustar la lista blanca para que solo los dígitos y las letras mayúsculas pasen el escaneo. Al final tendrás un script listo‑para‑ejecutar que podrás incorporar en cualquier proyecto—sin misterios, sin contenido extra.

## Lo Que Aprenderás

- Cómo **use OCR engine** programáticamente en Python.  
- Los pasos exactos para **cargar imagen para OCR** desde una carpeta local.  
- Por qué y cómo restringir el reconocimiento a un conjunto de caracteres personalizado.  
- Cómo **reconocer texto de PNG** y manejar el resultado de forma segura.  

**Prerequisitos:** Python 3.7+ instalado, una terminal con la que te sientas cómodo, y una imagen (p. ej., `serial-number.png`) que quieras leer. No se requiere experiencia previa en OCR.

---

## Realizar OCR en Imagen – Inicializar el OCR Engine

Lo primero que debes hacer es crear una instancia del OCR engine. Piensa en el motor como el cerebro que analizará los píxeles y los convertirá en caracteres.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Por qué es importante:* Sin un motor no hay nada que procese la imagen. La clase `OcrEngine` agrupa todo el trabajo pesado—pre‑procesamiento, segmentación y clasificación de caracteres—en un único objeto que puedes reutilizar.

---

## Cargar Imagen para OCR – Proveer el Archivo PNG

Ahora que el motor existe, necesitas alimentarlo con la imagen que deseas leer. La biblioteca espera un objeto `ImageStream`, que puedes crear directamente a partir de una ruta de archivo.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Consejo profesional:* Mantén la imagen en un formato de alto contraste (texto negro sobre fondo blanco) y evita artefactos de compresión; pueden confundir al algoritmo OCR.

---

## Restringir Caracteres – Lista Blanca de Dígitos y Letras Mayúsculas

A menudo solo te interesan un subconjunto de caracteres—por ejemplo, un número de serie que contiene solo A‑Z y 0‑9. Al establecer una lista blanca le indicas al motor que ignore todo lo demás, lo que mejora drásticamente la precisión.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*¿Qué ocurre internamente?* El motor construye un filtro que descarta cualquier glifo que no esté presente en la lista blanca antes de la etapa final de clasificación. Esto es especialmente útil cuando la imagen contiene ruido o texto decorativo que no necesitas.

---

## Reconocer Texto de PNG – Ejecutar el Proceso OCR

Con el motor preparado y la imagen cargada, finalmente puedes **realizar OCR en una imagen**. La llamada `recognize()` ejecuta todo el pipeline y devuelve un objeto de resultado.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Si tienes curiosidad por el rendimiento, el método suele terminar en unos pocos cientos de milisegundos para un PNG de 300 × 200 px en un portátil moderno.

---

## Salida y Verificación – Obtener el Texto Reconocido

El último paso es extraer el texto plano del objeto de resultado. Cualquier cosa que no coincida con la lista blanca se descarta automáticamente, por lo que obtienes una cadena limpia lista para procesamiento adicional.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Salida típica:* `AB12C3D4E5` (suponiendo que la imagen contenía ese número de serie exacto).  

Si la salida está vacía o distorsionada, verifica la calidad de la imagen y la lista blanca; una trampa común es omitir accidentalmente los caracteres necesarios.

---

## Casos Límite y Errores Comunes

| Situación | Qué Verificar | Solución Sugerida |
|-----------|---------------|-------------------|
| **Archivo no encontrado** | Error tipográfico en la ruta o archivo faltante | Usa `os.path.abspath` para verificar la ruta completa antes de llamar a `set_image`. |
| **Imagen de bajo contraste** | El texto se mezcla con el fondo | Aplica un umbral simple (`Pillow` o `OpenCV`) antes de pasar la imagen al motor. |
| **Caracteres inesperados** | Lista blanca demasiado restrictiva | Añade los caracteres faltantes a la cadena de la lista blanca. |
| **Imágenes grandes** | Reconocimiento lento | Redimensiona la imagen a un ancho máximo de 1024 px; la calidad del OCR suele mantenerse alta. |

---

## Script Completo – Listo para Ejecutar

A continuación se muestra el script completo y autónomo que une todas las piezas. Guárdalo como `ocr_demo.py`, reemplaza `YOUR_DIRECTORY` con la carpeta real y ejecuta `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Salida esperada en consola* (cuando el PNG contiene `SN12345`):

```
Recognized text: SN12345
```

---

## Conclusión

Ahora sabes exactamente cómo **realizar OCR en una imagen** archivos en Python, desde **cargar imagen para OCR** hasta **reconocer texto de PNG** y finalmente extraer un resultado limpio usando un **OCR engine** personalizable. El enfoque es sencillo, extensible y funciona listo‑para‑usar para la mayoría de escaneos de tipo número de serie.

¿Qué sigue? Prueba cambiar la lista blanca por letras minúsculas, experimenta con diferentes formatos de imagen (JPEG, BMP), o integra el script en una canalización de procesamiento por lotes. El mismo patrón—engine → image → settings → recognize → output—se aplica a prácticamente cualquier tarea de OCR que encuentres.

¿Tienes preguntas o una imagen curiosa que se niega a cooperar? Deja un comentario abajo, ¡y feliz codificación! 

![Diagrama que ilustra los pasos para realizar OCR en una imagen usando Python](https://example.com/ocr-flow.png "Diagrama que muestra cómo realizar OCR en una imagen con un motor OCR de Python")


## ¿Qué Deberías Aprender Después?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convertir Imagen a Texto – Realizar OCR en Imagen desde URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Cómo Usar AspOCR: Filtros de Preprocesamiento de Imagen OCR para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Cómo Extraer Texto de Imagen Preparando Rectángulos en OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}