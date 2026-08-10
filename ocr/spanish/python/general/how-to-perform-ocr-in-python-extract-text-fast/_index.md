---
category: general
date: 2026-03-26
description: Aprende a realizar OCR en Python y extrae fácilmente texto de una imagen,
  lee texto de un escaneo o extrae texto de una factura usando un OcrEngine sencillo.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: es
og_description: ¿Cómo realizar OCR en Python? Esta guía te muestra cómo extraer texto
  de una imagen, leer texto de un escaneo y extraer texto de una factura en minutos.
og_title: Cómo realizar OCR en Python – Extraer texto rápidamente
tags:
- OCR
- Python
- Image Processing
title: Cómo realizar OCR en Python – Extraer texto rápido
url: /es/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR en Python – Extraer texto rápidamente

¿Alguna vez te has preguntado **cómo realizar OCR** en un recibo escaneado o en un PDF borroso? No estás solo. En muchos proyectos la necesidad de **extraer texto de una imagen** aparece antes que tarde, y el enfoque habitual de “escribir todo a mano” simplemente no es escalable.  

En este tutorial verás un ejemplo completo, listo‑para‑ejecutar, que muestra **cómo usar OCR** para leer texto de un escaneo, extraer datos de una factura y, incluso, manejar la corrección automática de inclinación, todo con solo unas pocas líneas de Python.

## Lo que aprenderás

* Las dependencias exactas y las importaciones requeridas.
* Cómo crear y configurar una instancia de `OcrEngine`.
* Formas de **extraer texto de una imagen**, **leer texto de un escaneo** y **extraer texto de una factura** usando el mismo motor.
* Errores comunes (idioma incorrecto, archivos faltantes, imágenes grandes) y cómo evitarlos.
* Salida esperada para que puedas verificar que el OCR tuvo éxito.

No se necesitan enlaces a documentación externa; todo está contenido, por lo que puedes copiar‑pegar el código y ver los resultados de inmediato.

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

* Python 3.8+ instalado (el paquete `ocr` funciona con cualquier versión reciente).
* La biblioteca `ocr` disponible (`pip install ocr‑engine` – reemplaza con el nombre real del paquete si es diferente).
* Un archivo de imagen que deseas procesar – para la demostración usaremos `invoice.png` ubicado en una carpeta llamada `YOUR_DIRECTORY`.

Eso es todo. Si ya tienes esto, estás listo para continuar.

## Paso 1: Instalar e Importar el Módulo OCR

Lo primero: necesitamos la biblioteca OCR. Si aún no la has instalado, ejecuta el siguiente comando en tu terminal:

```bash
pip install ocr-engine
```

Ahora importamos el módulo en nuestro script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Consejo profesional:** Mantén tu entorno virtual ordenado; evita conflictos de versiones cuando más adelante añadas otros paquetes de procesamiento de imágenes.

## Paso 2: Crear y Configurar el Motor OCR

Crear el motor es tan simple como llamar a su constructor, pero el verdadero poder reside en configurarlo correctamente. Estableceremos el idioma a English y activaremos la corrección automática de inclinación, lo cual es esencial al trabajar con facturas escaneadas que no están perfectamente alineadas.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

¿Por qué habilitar `auto_skew`? Muchos escáneres generan imágenes con unos grados de desviación. Sin corrección, el motor podría perder caracteres, convirtiendo una factura perfectamente legible en un galimatías.

## Paso 3: Realizar OCR en tu Imagen Objetivo

Ahora alimentamos el archivo de imagen al motor. El método `recognize_image` devuelve un objeto que contiene el texto bruto así como puntuaciones de confianza (si la biblioteca las proporciona).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Si estás trabajando con un escenario de **leer texto de un escaneo**, simplemente reemplaza la ruta con el PDF escaneado convertido a PNG o JPEG. La misma llamada funciona para cualquier formato de imagen que soporte la biblioteca subyacente.

## Paso 4: Inspeccionar y Usar el Texto Extraído

Imprimamos la salida OCR cruda. En una canalización real de procesamiento de facturas probablemente analizarías esta cadena, extraerías líneas de artículos, totales y fechas, pero por ahora una mirada rápida confirmará que el OCR tuvo éxito.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Salida esperada (truncada por brevedad):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Si la salida se ve desordenada, verifica que la imagen sea clara y que `engine.language` coincida con el idioma del documento.

## Paso 5: Manejo de Casos Límite Comunes

### Imágenes Grandes

Procesar un escaneo de 5000 × 5000 píxeles puede consumir mucha memoria. Una forma rápida de mitigar esto es reducir la escala de la imagen antes de enviarla al motor:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Múltiples Idiomas

Si necesitas **extraer texto de una imagen** que contiene tanto inglés como español, puedes establecer una lista de idiomas:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

El motor intentará reconocer caracteres de ambos conjuntos.

### Manejo de Errores

Nunca asumas que el archivo existe. Envuelve la llamada en un bloque try‑except para proporcionar un mensaje amigable:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Referencia Visual

Below is a screenshot of the sample invoice we used in the demo. Notice the slight tilt—exactly what `auto_skew` fixes.

![cómo realizar OCR en una factura](/images/ocr-example.png)

*Texto alternativo:* cómo realizar OCR en una imagen de factura mostrando la corrección automática de inclinación.

## Ejemplo Completo y Ejecutable

Juntando todo, aquí tienes un script único que puedes ejecutar desde la línea de comandos. Cubre instalación, configuración, manejo de errores y un paso simple de post‑procesamiento que escribe el texto extraído en un archivo llamado `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Ejecutar `python full_ocr_demo.py` imprimirá el texto extraído en la consola y lo guardará en `output.txt`. Desde allí puedes aplicar expresiones regulares, escritores CSV o cualquier otra lógica que necesites para la automatización de **extraer texto de una factura**.

## Conclusión

Ahora tienes una solución sólida, de extremo a extremo, a **cómo realizar OCR** en Python. Creando un `OcrEngine`, configurando el idioma y la corrección de inclinación, y manejando algunos casos límite prácticos, puedes extraer de forma fiable **texto de una imagen**, **leer texto de un escaneo** y **extraer texto de una factura** sin buscar en documentación dispersa.

¿Qué sigue? Intenta procesar un lote de archivos en un bucle, experimenta con diferentes idiomas o conecta la salida a una biblioteca de generación de PDFs para crear PDFs buscables. El cielo es el límite, y el código que acabas de ver es una base sólida.

¿Tienes preguntas sobre un formato de archivo específico o necesitas ayuda ajustando los umbrales de confianza? Deja un comentario abajo—¡feliz de ayudarte a afinar tu canalización OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}