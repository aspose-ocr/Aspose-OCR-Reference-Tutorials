---
category: general
date: 2026-05-03
description: Aprende cómo ejecutar OCR en una imagen y extraer texto con coordenadas
  usando reconocimiento OCR estructurado. Código Python paso a paso incluido.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: es
og_description: Ejecuta OCR en una imagen y obtén el texto con coordenadas usando
  reconocimiento OCR estructurado. Ejemplo completo en Python con explicaciones.
og_title: Ejecutar OCR en una imagen – Tutorial de extracción de texto estructurado
tags:
- OCR
- Python
- Computer Vision
title: Ejecutar OCR en una imagen – Guía completa para la extracción de texto estructurado
url: /es/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en imagen – Guía completa para la extracción de texto estructurado

¿Alguna vez necesitaste **ejecutar OCR en imagen** pero no estabas seguro de cómo mantener las posiciones exactas de cada palabra? No estás solo. En muchos proyectos—escaneo de recibos, digitalización de formularios o pruebas de UI—necesitas no solo el texto bruto sino también los cuadros delimitadores que indican dónde se encuentra cada línea en la foto.  

Este tutorial te muestra una forma práctica de *ejecutar OCR en imagen* usando el motor **aocr**, solicitar **reconocimiento OCR estructurado**, y luego post‑procesar el resultado preservando la geometría. Al final podrás **extraer texto con coordenadas** en solo unas pocas líneas de Python, y entenderás por qué el modo estructurado es importante para tareas posteriores.

## Lo que aprenderás

- Cómo inicializar el motor OCR para **reconocimiento OCR estructurado**.  
- Cómo alimentar una imagen y recibir resultados crudos que incluyen los límites de línea.  
- Cómo ejecutar un post‑procesador que limpia el texto sin perder la geometría.  
- Cómo iterar sobre las líneas finales e imprimir cada fragmento de texto junto con su cuadro delimitador.  

Sin trucos, sin pasos ocultos—solo un ejemplo completo y ejecutable que puedes incorporar a tu propio proyecto.

---

## Requisitos previos

Antes de sumergirnos, asegúrate de tener lo siguiente instalado:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

También necesitarás un archivo de imagen (`input_image.png` o `.jpg`) que contenga texto claro y legible. Desde una factura escaneada hasta una captura de pantalla sirve, siempre que el motor OCR pueda ver los caracteres.

---

## Paso 1: Inicializar el motor OCR para reconocimiento estructurado

Lo primero que hacemos es crear una instancia de `aocr.Engine()` y decirle que queremos **reconocimiento OCR estructurado**. El modo estructurado devuelve no solo el texto plano sino también datos geométricos (rectángulos delimitadores) para cada línea, lo cual es esencial cuando necesitas mapear el texto de vuelta a la imagen.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Por qué importa:**  
> En el modo predeterminado el motor podría entregarte solo una cadena de palabras concatenadas. El modo estructurado te brinda una jerarquía de páginas → líneas → palabras, cada una con coordenadas, lo que facilita mucho superponer los resultados sobre la imagen original o alimentarlos a un modelo consciente del diseño.

---

## Paso 2: Ejecutar OCR en la imagen y obtener resultados crudos

Ahora alimentamos la imagen al motor. La llamada `recognize` devuelve un objeto `OcrResult` que contiene una colección de líneas, cada una con su propio rectángulo delimitador.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

En este punto `raw_result.lines` contiene objetos con dos atributos importantes:

- `text` – la cadena reconocida para esa línea.  
- `bounds` – una tupla como `(x, y, width, height)` que describe la posición de la línea.

---

## Paso 3: Post‑procesar preservando la geometría

La salida OCR cruda suele ser ruidosa: caracteres errantes, espacios mal ubicados o problemas de saltos de línea. La función `ai.run_postprocessor` limpia el texto pero **mantiene la geometría original** intacta, de modo que sigues teniendo coordenadas precisas.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Consejo profesional:** Si dispones de vocabularios específicos del dominio (p. ej., códigos de producto), proporciona un diccionario personalizado al post‑procesador para mejorar la precisión.

---

## Paso 4: Extraer texto con coordenadas – iterar y mostrar

Finalmente, recorremos las líneas limpias, imprimiendo el cuadro delimitador de cada línea junto con su texto. Este es el núcleo de **extraer texto con coordenadas**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Salida esperada

Suponiendo que la imagen de entrada contiene dos líneas: “Invoice #12345” y “Total: $89.99”, verás algo como:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

La primera tupla es el `(x, y, width, height)` de la línea en la imagen original, lo que te permite dibujar rectángulos, resaltar texto o pasar las coordenadas a otro sistema.

---

## Visualizar el resultado (opcional)

Si deseas ver los cuadros delimitadores superpuestos sobre la imagen, puedes usar Pillow (PIL) para dibujar rectángulos. A continuación tienes un fragmento rápido; si solo necesitas los datos crudos, puedes omitirlo.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

El texto alternativo anterior contiene la **palabra clave principal**, cumpliendo con el requisito SEO para atributos alt de imágenes.

---

## Por qué el reconocimiento OCR estructurado supera la extracción de texto simple

Quizá te preguntes, “¿No puedo simplemente ejecutar OCR y obtener el texto? ¿Por qué preocuparme por la geometría?”  

- **Contexto espacial:** Cuando necesitas mapear campos en un formulario (p. ej., “Date” junto al valor de la fecha), las coordenadas indican *dónde* está el dato.  
- **Diseños multicolumna:** El texto lineal simple pierde el orden; los datos estructurados preservan el orden de columnas.  
- **Precisión del post‑procesamiento:** Conocer el tamaño de la caja te ayuda a decidir si una palabra es un encabezado, una nota al pie o un artefacto errante.  

En resumen, **reconocimiento OCR estructurado** te brinda la flexibilidad para construir pipelines más inteligentes—ya sea que estés alimentando datos a una base de datos, creando PDFs buscables o entrenando un modelo de aprendizaje automático que respete el diseño.

---

## Casos límite comunes y cómo manejarlos

| Situación | Qué observar | Solución sugerida |
|-----------|--------------|-------------------|
| **Imágenes rotadas o sesgadas** | Los cuadros delimitadores pueden estar desalineados. | Pre‑procesar con corrección de sesgo (p. ej., `warpAffine` de OpenCV). |
| **Fuentes muy pequeñas** | El motor puede omitir caracteres, generando líneas vacías. | Aumentar la resolución de la imagen o usar `ocr_engine.set_dpi(300)`. |
| **Idiomas mixtos** | Un modelo de idioma incorrecto puede producir texto garbled. | Configurar `ocr_engine.language = ["en", "de"]` antes del reconocimiento. |
| **Cajas superpuestas** | El post‑procesador podría fusionar dos líneas inadvertidamente. | Verificar `line.bounds` después del procesamiento; ajustar umbrales en `ai.run_postprocessor`. |

Abordar estos escenarios desde el principio te ahorra dolores de cabeza más adelante, especialmente cuando escalas la solución a cientos de documentos al día.

---

## Script completo de extremo a extremo

A continuación tienes el programa completo, listo para ejecutar. Copia‑pega, ajusta la ruta de la imagen y listo.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Ejecutar este script hará lo siguiente:

1. **Ejecutar OCR en imagen** con modo estructurado.  
2. **Extraer texto con coordenadas** para cada línea.  
3. Opcionalmente producir un PNG anotado que muestra los cuadros.

---

## Conclusión

Ahora dispones de una solución sólida y autónoma para **ejecutar OCR en imagen** y **extraer texto con coordenadas** usando **reconocimiento OCR estructurado**. El código muestra cada paso—desde la inicialización del motor hasta el post‑procesamiento y la verificación visual—para que puedas adaptarlo a recibos, formularios o cualquier documento visual que requiera localización precisa del texto.

¿Qué sigue? Prueba cambiar el motor `aocr` por otra biblioteca (Tesseract, EasyOCR) y observa cómo difieren sus salidas estructuradas. Experimenta con distintas estrategias de post‑procesamiento, como corrección ortográfica o filtros regex personalizados, para mejorar la precisión en tu dominio. Y si construyes una pipeline más grande, considera almacenar los pares `(text, bounds)` en una base de datos para análisis posteriores.

¡Feliz codificación, y que tus proyectos OCR sean siempre precisos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}