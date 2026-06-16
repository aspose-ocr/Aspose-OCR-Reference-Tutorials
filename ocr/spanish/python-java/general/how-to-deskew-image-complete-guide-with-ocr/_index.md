---
category: general
date: 2026-03-26
description: Aprende a enderezar imágenes, reconocer texto a partir de una imagen
  y crear una cadena de preprocesamiento para eliminar el ruido del escaneo y convertir
  la imagen escaneada en texto.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: es
og_description: Cómo enderezar una imagen y convertir un escaneo inclinado en texto
  buscable. Sigue esta guía para reconocer texto a partir de una imagen, eliminar
  el ruido del escaneo y convertir la imagen escaneada en texto.
og_title: Cómo enderezar una imagen – Guía paso a paso de OCR
tags:
- OCR
- image-processing
- Python
title: Cómo enderezar una imagen – Guía completa con OCR
url: /es/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo Enderezar una Imagen – Guía Completa con OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** que salió de un escáner barato? No estás solo. Una página torcida se ve poco profesional y, lo que es más importante, la inclinación puede desorientar a cualquier motor OCR que intente **reconocer texto de una imagen**.  

En este tutorial recorreremos una **pipeline de preprocesamiento de imágenes** completa que endereza, binariza y elimina el ruido de un escaneo, y luego lo entrega a un motor OCR para que puedas **convertir una imagen escaneada a texto** con el mínimo esfuerzo. Sin trucos, solo Python puro y una pequeña biblioteca que hace el trabajo pesado.

## Lo que Necesitarás

- Python 3.9+ (el código funciona en 3.10 y versiones más recientes)
- El paquete `ocr` (instálalo con `pip install ocr‑toolkit` – reemplaza con el nombre real de tu biblioteca)
- Un JPEG o PNG escaneado que esté notablemente inclinado (p. ej., `skewed_scan.jpg`)
- Un poco de curiosidad sobre por qué cada paso de preprocesamiento importa

Eso es todo. Sin dependencias pesadas como OpenCV a menos que quieras profundizar más adelante.

## Paso 1: Cargar la Imagen Escaneada

Lo primero es cargar el archivo en memoria. Este paso es sencillo pero crucial: si la ruta es incorrecta, todo lo demás fallará.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **¿Por qué?**  
> Cargar la imagen nos brinda un objeto manipulable con el que `ocr.ImagePreprocessor` puede trabajar. Omitir este paso dejaría a la pipeline sin acceso a los datos reales de los píxeles.

## Cómo Enderezar una Imagen y Prepararla para OCR

Ahora que tenemos la imagen, vamos a enderezarla. El método `deskew()` estima el ángulo de inclinación y rota la foto de vuelta a la horizontal.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Consejo profesional:** Si tus escaneos están solo ligeramente desalineados (≤ 3°), el algoritmo predeterminado suele ser perfecto. Para ángulos extremos puede que necesites ajustar los parámetros internos—consulta la documentación de la biblioteca para `max_angle`.

## Binarizar la Imagen – Convertirla a Blanco y Negro

Los motores OCR adoran entradas de alto contraste. Convertir la foto a una representación binaria (blanco y negro) elimina tonos sutiles que pueden confundir el reconocimiento de caracteres.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **¿Qué está pasando?**  
> Los píxeles más claros que 128 se vuelven blancos; todo lo demás se vuelve negro. Ajusta el umbral si tu escaneo es inusualmente oscuro o claro.

## Eliminar Ruido del Escaneo antes de OCR

Incluso una imagen perfectamente enderezada puede contener manchas, polvo o artefactos de compresión. esos pequeños puntos son la perdición de cualquier motor OCR.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **¿Por qué eliminar el ruido?**  
> El ruido crea bordes falsos que el motor OCR podría interpretar como caracteres. Un radio pequeño funciona para la mayoría de los escaneos; aumentalo para documentos muy granulados.

## Aplicar la Pipeline de Preprocesamiento de Imagen

Toda la configuración está lista—ahora ejecutamos la pipeline sobre la imagen original.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Resultado:** `processed_image` es un mapa de bits limpio, recto y de alto contraste listo para la extracción de texto.

## Reconocer Texto de la Imagen con el Motor OCR

Es hora de leer realmente el texto. Inicializamos el motor OCR, le suministramos nuestra imagen pulida y solicitamos la cadena cruda.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Salida esperada** (ejemplo):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Si ves caracteres distorsionados, verifica nuevamente el paso de enderezado o experimenta con un valor diferente de `threshold`.

## Construir una Pipeline de Preprocesamiento de Imagen – Script Completo

Juntando todo, aquí tienes un script único y ejecutable que puedes colocar en un archivo `.py` y ejecutar:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Consejo:** Envuelve todo en una función (`def ocr_from_file(path): …`) si planeas procesar muchos archivos en lote.

## Preguntas Frecuentes y Casos Extremos

- **¿Qué pasa si la imagen ya está recta?**  
  El método `deskew()` detecta un ángulo cercano a cero y deja la foto sin cambios, por lo que puedes ejecutarlo de forma segura en cada archivo.

- **Mi escaneo está en color—¿debería conservarlo?**  
  El color no aporta valor para la mayoría de tareas OCR. La binarización lo elimina, acelerando el procesamiento y reduciendo el uso de memoria.

- **¿Puedo encadenar varios pasos de preprocesamiento?**  
  Por supuesto. La clase `ImagePreprocessor` está diseñada para pipelines; puedes añadir `sharpen()`, `contrast_enhance()` o filtros personalizados antes de llamar a `apply()`.

- **La salida OCR tiene saltos de línea extraños—¿cómo solucionarlo?**  
  Post‑procesa la cadena con `text.replace("\n", " ").strip()` o usa una biblioteca de análisis de layout más avanzada como los modos `--psm` de Tesseract.

## Próximos Pasos

Ahora que sabes **cómo enderezar una imagen** y tienes una sólida **pipeline de preprocesamiento de imágenes**, podrías explorar:

- Integrar **reconocer texto de una imagen** en una API Flask para cargas de documentos en tiempo real.
- Usar la pipeline para **eliminar ruido del escaneo** de documentos históricos donde la preservación es clave.
- Escalar para procesar por lotes miles de páginas y generar un PDF buscable usando `pdfminer` o `PyMuPDF`.

Siéntete libre de experimentar con diferentes umbrales, radios de eliminación de ruido, o incluso cambiar el backend OCR por Tesseract si necesitas soporte multilingüe. Los fundamentos siguen siendo los mismos: endereza, limpia y luego lee.

---

*¡Feliz codificación! Si tienes problemas, deja un comentario abajo—estaré encantado de ayudarte a afinar la pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}