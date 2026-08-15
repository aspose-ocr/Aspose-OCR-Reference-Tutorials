---
category: general
date: 2026-03-26
description: Crea un polígono ROI para ejecutar OCR en el área seleccionada. Aprende
  a definir múltiples regiones, registrarlas y extraer texto con un motor OCR en Python.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: es
og_description: Crea un polígono ROI y ejecuta OCR en el área seleccionada con un
  motor Python. Código completo, explicaciones y consejos incluidos.
og_title: Crear polígono ROI – OCR rápido en el área seleccionada
tags:
- OCR
- Python
- Image Processing
title: Crear polígono ROI – Guía paso a paso para OCR en el área seleccionada
url: /es/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Polígono ROI – Tutorial Completo para OCR en Área Seleccionada

¿Alguna vez necesitaste **crear polígono ROI** para ejecutar OCR solo en la parte de una imagen que importa? Tal vez estés escaneando recibos y solo importen los totales, o tengas un formulario donde solo se necesita leer el campo de firma. En esos casos, **ocr en área seleccionada** ahorra tiempo y mejora la precisión.  

En esta guía recorreremos todo lo que necesitas: desde definir dos polígonos, registrarlos en un motor OCR, hasta extraer el texto reconocido en una única llamada limpia. Al final tendrás un script listo para ejecutar y una comprensión sólida de por qué enfocarse en regiones de interés es importante.

## Lo que aprenderás

- Cómo **crear polígono ROI** usando una biblioteca OCR típica.
- La diferencia entre definir una sola región y múltiples.
- Cómo registrar esas regiones en el motor para que se realice `ocr on selected area`.
- Salida esperada y cómo solucionar problemas comunes (p. ej., ROIs superpuestos, resultados vacíos).

### Requisitos previos

- Python 3.8+ instalado.
- Una biblioteca OCR que exponga los métodos `Polygon`, `Point` y `add_region_of_interest` (el ejemplo usa un módulo ficticio `ocr`; reemplázalo con tu SDK real, como los wrappers de Tesseract‑Python o EasyOCR).
- Un archivo de imagen de muestra (`sample.png`) que contenga texto dentro de las coordenadas mostradas a continuación.

> **Pro tip:** Si estás usando una biblioteca real, asegúrate de que la imagen se cargue en el mismo espacio de coordenadas (origen en la esquina superior izquierda, X aumentando a la derecha, Y aumentando hacia abajo).  

---  

## Paso 1: Importar el Módulo OCR y Cargar tu Imagen  

Primero, trae el paquete OCR al alcance y lee la imagen que deseas procesar.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Por qué es importante:* El motor necesita los datos de la imagen antes de que puedas adjuntar cualquier **polígono ROI**. Algunas bibliotecas también permiten pasar la imagen más tarde, pero inicializar temprano mantiene el flujo de trabajo ordenado.

## Paso 2: Definir el Primer Polígono ROI  

Ahora creamos la primera región de interés. Piensa en ello como dibujar un rectángulo alrededor del encabezado de una tabla.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explicación:*  
- `ocr.Point(x, y)` usa coordenadas en píxeles.  
- La lista de puntos está ordenada en sentido horario, que la mayoría de los motores esperan.  
- Puedes añadir tantos puntos como desees para crear formas irregulares; un rectángulo es solo un caso especial.

## Paso 3: Definir Polígonos ROI Adicionales (Opcional)  

No tienes que detenerte en uno. Aquí tienes un segundo polígono que captura un campo de firma más abajo en la página.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*¿Por qué añadir más?* Ejecutar **ocr on selected area** para múltiples zonas te permite extraer piezas de datos dispares en una sola pasada, lo que es mucho más rápido que recortar y procesar cada fragmento por separado.

## Paso 4: Registrar los ROI en el Motor OCR  

Con los polígonos listos, indica al motor qué áreas inspeccionar.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Nota importante:* Algunos SDK requieren que llames al método `clear_regions()` antes de añadir nuevos si reutilizas el motor para otra imagen.

## Paso 5: Ejecutar OCR y Recuperar el Texto  

Finalmente, dispara el reconocimiento. El motor solo buscará dentro de los polígonos que acabamos de añadir.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Salida esperada** (suponiendo que `sample.png` contiene las palabras “Invoice Total: $123.45” en el primer ROI y “Signature: John Doe” en el segundo):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Si la salida está vacía, verifica que las coordenadas realmente intersecten texto y que la resolución de la imagen coincida con el sistema de coordenadas.

## Casos límite y problemas comunes  

| Situación                               | Qué observar                                   | Solución / Alternativa                         |
|----------------------------------------|------------------------------------------------|-----------------------------------------------|
| **ROIs superpuestos**                  | El texto puede devolverse dos veces.           | Mantén los polígonos disjuntos o deduplica la salida. |
| **ROI fuera de los límites de la imagen** | El motor puede lanzar un error o no devolver nada. | Limita las coordenadas a `0 ≤ x < width`, `0 ≤ y < height`. |
| **ROI muy pequeño**                    | La precisión del OCR disminuye por falta de píxeles. | Expande el polígono unos píxeles o aumenta la resolución de la imagen primero. |
| **Forma no rectangular**               | Algunos motores solo admiten polígonos convexos. | Divide formas complejas en varios ROI convexos. |
| **Cambio de tamaño de la imagen**      | Las coordenadas codificadas pierden validez.   | Calcula las coordenadas del ROI en función de las dimensiones de la imagen (p. ej., porcentajes). |

## Ejemplo completo funcionando  

A continuación tienes el script completo que puedes copiar‑pegar y ejecutar (reemplaza `ocr` con tu biblioteca real).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Ejecuta con `python ocr_roi_example.py` y deberías ver las cadenas extraídas de las dos zonas definidas.

## Próximos pasos  

- **Generación dinámica de ROI:** En lugar de codificar coordenadas, usa procesamiento de imágenes (p. ej., detección de contornos con OpenCV) para localizar automáticamente tablas o campos.  
- **Post‑procesamiento:** Elimina espacios en blanco, aplica expresiones regulares o convierte números a tipos de datos adecuados.  
- **Procesamiento por lotes:** Recorre una carpeta de imágenes, reutilizando las mismas definiciones de ROI si el diseño es consistente.  

Si tienes curiosidad sobre **ocr on selected area** para documentos más complejos —piensa en PDFs multipágina o formularios escaneados— investiga bibliotecas que soporten registro de ROI por página.  

---  

### Visión general visual  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="ejemplo de creación de polígono roi que muestra dos áreas seleccionadas"}

El diagrama ilustra cómo los dos rectángulos (azul y verde) se mapean sobre la imagen subyacente, resaltando exactamente lo que el motor OCR leerá.

---  

## Conclusión  

Acabamos de **crear polígono ROI**, registrarlos en un motor OCR y ejecutar `ocr on selected area` en un script limpio y reproducible. Al limitar el motor a las zonas que te importan, reduces el tiempo de procesamiento, mejoras la precisión y simplificas mucho el manejo de datos posteriores.  

Pruébalo con tus propias imágenes —ajusta las coordenadas, añade más polígonos o conecta la salida a una base de datos. El cielo es el límite una vez que domines el OCR basado en regiones.  

¿Tienes preguntas o quieres compartir un caso de uso interesante? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}