---
category: general
date: 2026-03-28
description: Realiza OCR en la imagen y obtén texto limpio con coordenadas de los
  cuadros delimitadores. Aprende cómo extraer OCR, limpiar OCR y mostrar los resultados
  paso a paso.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: es
og_description: Realiza OCR en la imagen, limpia la salida y muestra las coordenadas
  de los cuadros delimitadores en un tutorial conciso.
og_title: Realizar OCR en una imagen – resultados limpios y cajas delimitadoras
tags:
- OCR
- Computer Vision
- Python
title: Realizar OCR en la imagen – Resultados limpios y mostrar coordenadas del cuadro
  delimitador
url: /es/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR en Imagen – Resultados Limpios y Mostrar Coordenadas de Cuadro Delimitador

¿Alguna vez necesitaste **realizar OCR en archivos de imagen** pero obtuviste texto desordenado y no sabías dónde se encuentra cada palabra en la foto? No estás solo. En muchos proyectos—digitalización de facturas, escaneo de recibos o extracción simple de texto—obtener la salida bruta de OCR es solo el primer obstáculo. ¿La buena noticia? Puedes limpiar esa salida y ver instantáneamente las coordenadas del cuadro delimitador de cada región sin escribir mucho código repetitivo.

En esta guía recorreremos **cómo extraer OCR**, ejecutar un **cómo limpiar OCR** post‑procesador y, finalmente, **mostrar coordenadas de cuadro delimitador** para cada región limpia. Al final tendrás un único script ejecutable que convierte una foto borrosa en texto estructurado y ordenado listo para el procesamiento posterior.

## Lo que Necesitarás

- Python 3.9+ (la sintaxis a continuación funciona en 3.8 y versiones posteriores)
- Un motor OCR que soporte `recognize(..., return_structured=True)` – por ejemplo, una biblioteca ficticia `engine` usada en el fragmento. Reemplázala con Tesseract, EasyOCR o cualquier SDK que devuelva datos de regiones.
- Familiaridad básica con funciones y bucles en Python
- Un archivo de imagen que quieras escanear (PNG, JPG, etc.)

> **Consejo profesional:** Si usas Tesseract, la función `pytesseract.image_to_data` ya te proporciona cuadros delimitadores. Puedes envolver su resultado en un pequeño adaptador que imite la API `engine.recognize` mostrada a continuación.

---

![perform OCR on image example](image-placeholder.png "ejemplo de realizar OCR en imagen")

*Texto alternativo: diagrama que muestra cómo realizar OCR en una imagen y visualizar las coordenadas del cuadro delimitador*

## Paso 1 – Realizar OCR en Imagen y Obtener Regiones Estructuradas

Lo primero es pedirle al motor OCR que devuelva no solo texto plano sino una lista estructurada de regiones de texto. Esta lista contiene la cadena cruda y el rectángulo que la encierra.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Por qué es importante:**  
Cuando solo solicitas texto plano pierdes el contexto espacial. Los datos estructurados te permiten más tarde **mostrar coordenadas de cuadro delimitador**, alinear texto con tablas o proporcionar ubicaciones precisas a un modelo posterior.

## Paso 2 – Cómo Limpiar la Salida de OCR con un Post‑Procesador

Los motores OCR son excelentes detectando caracteres, pero a menudo dejan espacios sobrantes, artefactos de saltos de línea o símbolos mal reconocidos. Un post‑procesador normaliza el texto, corrige errores comunes de OCR y elimina espacios en blanco.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Si construyes tu propio limpiador, considera:

- Eliminar caracteres no ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Colapsar múltiples espacios en uno solo
- Aplicar un corrector ortográfico como `pyspellchecker` para errores evidentes

**Por qué deberías preocuparte:**  
Una cadena ordenada hace que la búsqueda, indexación y los pipelines de NLP posteriores sean mucho más fiables. En otras palabras, **cómo limpiar OCR** suele ser la diferencia entre un conjunto de datos utilizable y un dolor de cabeza.

## Paso 3 – Mostrar Coordenadas de Cuadro Delimitador para Cada Región Limpia

Ahora que el texto está ordenado, iteramos sobre cada región, imprimiendo su rectángulo y la cadena limpiada. Esta es la parte donde finalmente **mostramos coordenadas de cuadro delimitador**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Salida de ejemplo**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Ahora puedes pasar esas coordenadas a una biblioteca de dibujo (p. ej., OpenCV) para superponer cuadros sobre la imagen original, o almacenarlas en una base de datos para consultas posteriores.

## Script Completo y Listo para Ejecutar

A continuación tienes el programa completo que une los tres pasos. Sustituye las llamadas de marcador `engine` por tu SDK OCR real.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Cómo Ejecutar

```bash
python perform_ocr.py sample_invoice.jpg
```

Deberías ver una lista de cuadros delimitadores emparejados con texto limpio, exactamente como la salida de ejemplo anterior.

## Preguntas Frecuentes y Casos Extremos

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si el motor OCR no soporta `return_structured`?** | Escribe un contenedor ligero que convierta la salida cruda del motor (usualmente una lista de palabras con coordenadas) en objetos con atributos `text` y `bounding_box`. |
| **¿Puedo obtener puntuaciones de confianza?** | Muchos SDK exponen una métrica de confianza por región. Añádela a la instrucción de impresión: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **¿Cómo manejar texto rotado?** | Pre‑procesa la imagen con `cv2.minAreaRect` de OpenCV para desinclinar antes de llamar a `recognize`. |
| **¿Qué pasa si necesito la salida en JSON?** | Serializa `processed_result.regions` con `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **¿Hay una forma de visualizar los cuadros?** | Usa OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` dentro del bucle, luego `cv2.imwrite("annotated.jpg", img)`. |

## Conclusión

Acabas de aprender **cómo realizar OCR en imagen**, limpiar la salida cruda y **mostrar coordenadas de cuadro delimitador** para cada región. El flujo de tres pasos—reconocer → post‑procesar → iterar—es un patrón reutilizable que puedes incorporar en cualquier proyecto Python que necesite extracción de texto fiable.

### ¿Qué Sigue?

- **Explora diferentes back‑ends OCR** (Tesseract, EasyOCR, Google Vision) y compara precisión.
- **Integra con una base de datos** para almacenar datos de regiones y crear archivos buscables.
- **Añade detección de idioma** para encaminar cada región al corrector ortográfico adecuado.
- **Superpone cuadros sobre la imagen original** para verificación visual (consulta el fragmento de OpenCV arriba).

Si encuentras particularidades, recuerda que la mayor ventaja proviene de un sólido paso de post‑procesamiento; una cadena limpia es mucho más fácil de manejar que un volcado bruto de caracteres.

¡Feliz codificación, y que tus pipelines de OCR siempre estén ordenados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}