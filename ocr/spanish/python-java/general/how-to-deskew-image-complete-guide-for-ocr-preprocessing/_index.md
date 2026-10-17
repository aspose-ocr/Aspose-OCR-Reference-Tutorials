---
category: general
date: 2026-07-05
description: Cómo enderezar una imagen rápidamente. Aprende a preprocesar la imagen
  para OCR, corregir la rotación de la imagen y convertir el escaneo a texto con Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: es
og_description: Cómo corregir la inclinación de una imagen y preprocesarla para OCR.
  Esta guía muestra cómo corregir la rotación de la imagen y extraer texto de la imagen
  usando Python.
og_title: Cómo corregir la inclinación de una imagen – Preprocesamiento OCR paso a
  paso
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Cómo enderezar una imagen – Guía completa para el preprocesamiento OCR
url: /es/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo corregir la inclinación de una imagen – Guía completa para el preprocesamiento OCR

¿Alguna vez te has preguntado **cómo corregir la inclinación de una imagen** que parece haber sido escaneada con el escáner torcido? No eres el único. En muchos proyectos del mundo real lo primero que debes hacer antes de **extraer texto de una imagen** es enderezar esa distorsión.

En este tutorial recorreremos un ejemplo práctico, de extremo a extremo, que **preprocesa la imagen para OCR**, corrige la rotación y, finalmente, **convierte el escaneo a texto** usando una biblioteca OCR de Python. Sin referencias vagas, solo un script funcional que puedes copiar‑pegar, más consejos sobre los errores más comunes.

## Lo que lograrás

Al final de esta guía podrás:

* Cargar cualquier JPEG o PNG escaneado que esté ligeramente inclinado.  
* Aplicar un filtro de corrección de inclinación y un paso de binarización para mejorar la precisión del OCR.  
* Ejecutar el motor OCR y **extraer texto de una imagen** de forma fiable.  
* Entender por qué **la rotación correcta de la imagen** es importante para la extracción de texto posterior.  

### Requisitos previos

* Python 3.9+ instalado en tu máquina.  
* Un paquete OCR instalable con pip que imite el espacio de nombres `ocr` usado en el ejemplo (por ejemplo, un contenedor ligero alrededor de Tesseract).  
* Familiaridad básica con funciones de Python y conceptos de procesamiento de imágenes.  

Si ya cuentas con eso, vamos a sumergirnos.

![ejemplo de cómo corregir la inclinación de la imagen](deskew_before_after.png){alt="cómo corregir la inclinación de la imagen – antes y después de la corrección"}

## Paso 1: Configurar el motor OCR – Cómo corregir la inclinación de una imagen usando Python

Lo primero: necesitas un motor OCR que pueda entender el idioma de tu documento. El fragmento a continuación muestra el boilerplate mínimo para crear el motor y decirle que trabajas con texto en inglés.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Por qué es importante:* La configuración de idioma del motor influye en el conjunto de caracteres y el diccionario que utiliza. Omitir este paso puede hacer que el OCR interprete mal palabras comunes, especialmente después de **corregir la rotación de la imagen**.

## Paso 2: Cargar la imagen escaneada que deseas enderezar

Ahora traemos el archivo a la memoria. Reemplaza `"YOUR_DIRECTORY/skewed_scan.jpg"` con la ruta a tu propia imagen.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Si la imagen ya está en un array de NumPy o en un `Mat` de OpenCV, puedes adaptar el cargador en consecuencia; lo esencial es que el objeto exponga el método `apply_filter` que se usará más adelante.

## Paso 3: Preprocesar la imagen para OCR – Corregir inclinación y binarizar

Aquí es donde ocurre la magia. Encadenamos dos filtros:

1. **Deskew** – detecta automáticamente la línea base de texto dominante y rota la imagen de nuevo a la horizontal.  
2. **Binarize (Otsu)** – convierte la foto a puro blanco y negro, lo que mejora drásticamente las tasas de reconocimiento.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Consejo profesional:* Si notas que el texto sigue viéndose borroso después de la binarización, prueba a ajustar el contraste o usar un método de umbralizado diferente. El módulo `ocr.Filter` suele incluir `adaptive_threshold()` para casos más difíciles.

## Paso 4: Ejecutar OCR – Extraer texto de la imagen

Con un lienzo limpio y recto, entregamos la imagen al motor. El objeto de resultado contiene la cadena reconocida, puntuaciones de confianza e incluso cajas delimitadoras si las necesitas más adelante.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Una salida típica se ve así:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

¿Ves cómo los saltos de línea quedan perfectamente alineados? Ese es el beneficio de **la rotación correcta de la imagen**: el OCR ya no tiene que adivinar la orientación de las líneas.

## Paso 5: Unir todo – Un script de un solo archivo para convertir escaneos a texto

A continuación tienes el script completo y ejecutable que combina cada pieza que hemos discutido. Guárdalo como `deskew_ocr.py` y ejecuta `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Por qué funciona

* **Deskew primero** – rotar la imagen antes de la binarización asegura que el algoritmo de umbralado trabaje sobre un horizonte nivelado.  
* **Binarizar después del deskew** – el método de Otsu asume un histograma bimodal; una página inclinada rompería esa suposición.  
* **Modelo de idioma inglés** – indica al OCR qué caracteres esperar, reduciendo falsos positivos.  

Si necesitas manejar otros idiomas, simplemente sustituye `ocr.Language.ENGLISH` por el enum correspondiente.

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si el escaneo está al revés?* | El filtro `deskew()` suele detectar también rotaciones de 180°. Si falla, llama a `apply_filter(ocr.Filter.rotate(180))` antes de aplicar `deskew()`. |
| *Mi documento tiene gráficos en color – ¿la binarización los eliminará?* | Sí. Para contenido mixto, considera usar solo `ocr.Filter.deskew()`, luego ejecutar OCR sobre la imagen a color. Aún puedes extraer texto mientras preservas los gráficos. |
| *¿Puedo procesar un lote de archivos?* | Envuelve la lógica en un bucle, lee cada ruta de archivo desde una lista y guarda cada `result.text` en un archivo `.txt` separado. |
| *¿Cómo mejorar la precisión en escaneos de baja resolución?* | Escala la imagen con un filtro bicúbico **antes** de deskew, luego aplica un filtro de nitidez. Más píxeles le dan al motor OCR más pistas. |

## Bonus: Verificación visual del deskew

Si quieres ver el antes y después lado a lado, añade un fragmento rápido de Matplotlib:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Ver la alineación corregida puede ser reconfortante, sobre todo cuando estás depurando un lote complicado de escaneos.

## Conclusión

Hemos cubierto **cómo corregir la inclinación de una imagen**, por qué **preprocesar la imagen para OCR** es esencial y cómo **extraer texto de una imagen** para finalmente **convertir el escaneo a texto**. El flujo de trabajo — cargar → deskew → binarizar → reconocer — garantiza que el OCR vea una página limpia y recta, lo que se traduce en mayor precisión y menos correcciones manuales.

¿Qué sigue en tu viaje OCR? Prueba a experimentar con:

* Diferentes paquetes de idioma (`ocr.Language.FRENCH`, etc.).  
* Añadir un paso de análisis de diseño para detectar columnas o tablas.  
* Exportar los resultados OCR a PDFs buscables usando una biblioteca PDF.

No dudes en dejar un comentario si encuentras algún obstáculo, o compartir tus propios ajustes para manejar escaneos especialmente rebeldes. ¡Feliz codificación, y que tus imágenes siempre permanezcan perfectamente niveladas!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo usar AspOCR: filtros de preprocesamiento de imagen OCR para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extraer texto de imagen en C# con selección de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cómo hacer OCR a una imagen – Realizar OCR en imagen en reconocimiento de imágenes OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}