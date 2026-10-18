---
category: general
date: 2026-03-26
description: Cómo ejecutar OCR en un archivo PNG y extraer texto de la imagen con
  un diccionario personalizado para mejorar la precisión del OCR. Aprende a cargar
  la imagen para OCR rápidamente.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: es
og_description: Cómo ejecutar OCR en un archivo PNG y extraer texto de la imagen con
  un diccionario personalizado para mejorar la precisión del OCR. Guía paso a paso.
og_title: Cómo ejecutar OCR – Extraer texto de una imagen en Python
tags:
- OCR
- Python
- Image Processing
title: Cómo ejecutar OCR – Extraer texto de una imagen en Python
url: /es/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR – Extraer texto de una imagen en Python

¿Alguna vez te has preguntado **cómo ejecutar OCR** en una factura escaneada o una captura de pantalla y obtener texto limpio y buscable? No estás solo. En muchos proyectos el cuello de botella es simplemente cargar la imagen para OCR y luego convencer al motor de que entienda palabras específicas del dominio.  

En este tutorial recorreremos un ejemplo completo y listo‑para‑ejecutar que **extrae texto de imágenes**, te muestra cómo **reconocer texto de archivos PNG** y, incluso, demuestra trucos para **mejorar la precisión de OCR** con diccionarios personalizados y caracteres especiales. Al final tendrás un script autónomo que podrás incorporar a cualquier base de código Python.

## Lo que necesitarás

- Python 3.8+ (el código usa anotaciones de tipo pero funciona en versiones anteriores de 3.x)
- La biblioteca `ocr` que viene con el motor OCR que estás utilizando (instálala con `pip install ocr‑engine` – reemplaza con el nombre real del paquete)
- Un archivo de imagen (`input.png`) que deseas procesar
- Opcional: un archivo de texto plano (`invoice_terms.txt`) con palabras específicas del dominio, una por línea

Sin dependencias externas pesadas, sin claves de API en la nube, solo un motor OCR local.

---

## Paso 1: Instalar e importar la biblioteca OCR

Primero, asegúrate de que el paquete OCR esté instalado. Si estás usando el paquete hipotético `ocr-engine`, ejecuta:

```bash
pip install ocr-engine
```

Ahora importa las clases que necesitarás:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Consejo profesional:** Si estás en un entorno virtual, actívalo antes de instalar para mantener tu Python global limpio.

## Paso 2: Crear una instancia del motor OCR

Crear un objeto motor es el punto de entrada para cada tarea de OCR. Piensa en ello como encender el hardware del escáner mediante software.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Por qué es importante: el motor almacena configuraciones como paquetes de idioma, modos de reconocimiento y cualquier recurso personalizado que adjuntes después. Sin él, no puedes **cargar la imagen para OCR** ni ejecutar la cadena de reconocimiento.

## Paso 3: Cargar la imagen que deseas reconocer

Aquí realmente **cargamos la imagen para OCR**. El método `Imaging.Image.load()` lee el archivo y lo convierte al formato interno de mapa de bits que el motor espera.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Si tienes un JPEG o TIFF, el mismo método funciona—solo cambia la extensión. El motor detecta automáticamente el formato.

> **Caso límite:** Imágenes muy grandes (más de 5 MP) pueden provocar picos de memoria. Considera reducir la escala con Pillow antes de cargar si encuentras problemas de rendimiento.

## Paso 4: Proveer un diccionario personalizado para mejorar la precisión

La mayoría de los motores OCR vienen con modelos de idioma genéricos. Para facturas, recibos o documentos legales a menudo se pierden palabras. Proveer una lista de palabras personalizada indica al motor que “estos términos son válidos, trátalos como correctos”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Entradas típicas podrían ser:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Agregar estos mejora la métrica de **mejorar la precisión de OCR** dramáticamente—especialmente para símbolos no ASCII.

## Paso 5: Añadir caracteres especiales que no están en el conjunto predeterminado

Si tu dominio usa símbolos como el signo de Euro (€) o la Ø escandinava, puedes añadirlos explícitamente:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

El motor ahora tratará esos glifos como válidos durante la fase de reconocimiento, reduciendo la probabilidad de obtener salida “basura”.

## Paso 6: Ejecutar el proceso OCR y obtener el texto

Finalmente, invoca el reconocedor y extrae el resultado en texto plano. La llamada `recognize()` devuelve un objeto rico; solo necesitamos la cadena cruda para la mayoría de los casos de uso.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Salida esperada** (truncada por brevedad):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Si la salida se ve desordenada, verifica que tu diccionario personalizado y los caracteres especiales estén cargados correctamente.

---

## Visión general visual

![diagrama de cómo ejecutar OCR](ocr-workflow.png){alt="diagrama de cómo ejecutar OCR"}

El diagrama anterior ilustra el flujo desde cargar una imagen hasta obtener texto limpio, resaltando dónde puedes inyectar diccionarios personalizados y conjuntos de caracteres.

---

## Preguntas frecuentes y trampas

### ¿Esto funciona con PDFs de varias páginas?

Sí—simplemente convierte cada página a PNG (usando `pdf2image` o similar) y aliméntalas secuencialmente a la misma instancia `ocr_engine`. El motor procesa cada imagen de forma independiente, por lo que obtendrás una lista de cadenas que puedes concatenar.

### ¿Qué pasa si la imagen está rotada?

La mayoría de los motores OCR modernos detectan automáticamente la orientación, pero puedes forzar una rotación con:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### ¿Cómo manejar idiomas diferentes al inglés?

Cambia el modelo de idioma antes de cargar la imagen:

```python
ocr_engine.set_language("de")  # German
```

Asegúrate de que el paquete de idioma correspondiente esté instalado.

---

## Script completo – Listo para copiar y pegar

A continuación está el programa completo, listo para ejecutarse después de que reemplaces las rutas de marcador de posición.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Ejecuta con:

```bash
python run_ocr.py
```

Deberías ver el texto extraído impreso en la consola. Desde allí puedes escribirlo en un archivo, enviarlo a una base de datos o pasarlo a pipelines de NLP posteriores.

---

## Recapitulación y próximos pasos

Hemos cubierto **cómo ejecutar OCR** en un PNG, cómo **extraer texto de una imagen**, y mostrado formas prácticas de **reconocer texto de PNG** mientras **mejoramos la precisión de OCR** con diccionarios y caracteres personalizados.  

A continuación, considera:

- **Procesamiento por lotes:** Recorrer un directorio de imágenes.
- **Post‑procesamiento:** Usa expresiones regulares para extraer números de factura o fechas.
- **Integración:** Conecta el script a una API Flask para servicios OCR bajo demanda.

Si tienes curiosidad por temas más avanzados, revisa tutoriales sobre **cargar imagen para OCR** con preprocesamiento OpenCV, o profundiza en modelos OCR basados en deep‑learning como Tesseract 4+ con capas LSTM.

### ¡Sigue experimentando!

Intenta reemplazar `invoice_terms.txt` con una lista de terminología médica, añade caracteres griegos, o alimenta el motor con una foto de baja resolución para ver hasta dónde puede llegar la precisión. Cuanto más juegues, mejor comprenderás los compromisos entre preprocesamiento, vocabularios personalizados y configuraciones del motor.

¡Feliz codificación, y que tus resultados de OCR sean siempre nítidos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}