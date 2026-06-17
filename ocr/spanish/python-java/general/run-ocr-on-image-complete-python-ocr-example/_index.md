---
category: general
date: 2026-03-18
description: Ejecuta OCR en una imagen rápidamente con Python. Aprende cómo reconocer
  texto de un PNG, cargar la imagen para OCR y extraer palabras de la imagen en una
  guía paso a paso.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: es
og_description: Ejecuta OCR en una imagen usando Python. Este tutorial muestra cómo
  reconocer texto de un PNG, cargar la imagen para OCR y extraer palabras de la imagen
  con un ejemplo de código completo.
og_title: Ejecutar OCR en Imagen – Guía de Python
tags:
- OCR
- Python
- Image Processing
title: Ejecutar OCR en una imagen – Ejemplo completo de OCR en Python
url: /es/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en Imagen – Ejemplo Completo de OCR en Python

¿Alguna vez necesitaste **ejecutar OCR en archivos de imagen** pero no sabías por dónde empezar? No estás solo; muchos desarrolladores se topan con esa barrera al intentar extraer texto de documentos escaneados por primera vez. En este tutorial recorreremos un **ejemplo de OCR en Python** que te permite **reconocer texto de archivos PNG**, **cargar imagen para OCR**, y **extraer palabras de la imagen** con puntuaciones de confianza, todo en unas pocas líneas de código.

Cubriremos todo lo que necesitas: la biblioteca requerida, cómo configurar el motor, por qué cada paso es importante y cómo se ve la salida. Al final, podrás insertar este fragmento en tu propio proyecto y comenzar a extraer texto de cualquier imagen al instante. Sin rodeos, solo una solución práctica y ejecutable.

## Lo que Necesitarás

Antes de sumergirnos, asegúrate de tener:

- Python 3.8 o superior instalado  
- El paquete `ocrengine` (o cualquier biblioteca que proporcione una clase `OcrEngine`). Puedes instalarlo con `pip install ocrengine` – ajusta el nombre si usas otra biblioteca OCR como `pytesseract`.  
- Un archivo de imagen (PNG, JPG, etc.) que quieras procesar – para esta guía usaremos `invoice.png`.  

Eso es todo. Sin dependencias pesadas, sin servicios externos, solo Python puro.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Texto alternativo: ejemplo de ejecutar OCR en imagen – factura escaneada siendo procesada*

## Paso 1 – Instalar e Importar la Biblioteca OCR

Lo primero, vamos a obtener el motor OCR en nuestro entorno e importarlo. Si estás usando el paquete hipotético `ocrengine`, la importación se ve así:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Por qué es importante:** Importar la clase correcta te da acceso a los métodos que llamaremos más adelante, como `setImageFromFile` y `recognize`. Si omites este paso, Python lanzará un `ModuleNotFoundError` y quedarás atascado antes de cargar una imagen.

## Paso 2 – Crear una Instancia del Motor OCR

Ahora que la biblioteca está lista, necesitamos un objeto motor que mantenga la configuración y el estado del proceso de reconocimiento.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Consejo profesional:* Algunos motores OCR te permiten ajustar modelos de idioma o configuraciones de DPI en este punto. Para un **ejemplo de OCR en python** básico, los valores predeterminados funcionan bien, pero si trabajas con escaneos de baja resolución, considera ajustarlos aquí.

## Paso 3 – Cargar la Imagen que Deseas Procesar

El siguiente paso lógico es **cargar imagen para OCR**. Apuntas el motor a la ruta del archivo PNG (o cualquier formato compatible) que deseas analizar.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**¿Qué ocurre tras bambalinas?** El motor lee los datos de píxeles, los convierte a un formato que el algoritmo de reconocimiento puede entender y los almacena internamente. Si la ruta del archivo es incorrecta, obtendrás un `FileNotFoundError`, así que verifica que la imagen exista.

## Paso 4 – Ejecutar el Algoritmo de Reconocimiento

Con la imagen cargada, finalmente **ejecutamos OCR en la imagen** para extraer el contenido textual.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

En este punto el motor escanea el mapa de bits, aplica coincidencia de patrones y devuelve un objeto que contiene cada palabra detectada, línea y métrica de confianza.

## Paso 5 – Recorrer las Palabras Reconocidas y Mostrar la Confianza

La parte más útil de cualquier flujo OCR es ver **la confianza** de cada token extraído. Indica cuán seguro está el motor sobre cada palabra, permitiéndote filtrar resultados de baja confianza si es necesario.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Salida esperada** (ejemplo):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Ahora puedes ver exactamente **qué palabras fueron extraídas de la imagen** y cuán fiable es cada detección. Este es el núcleo de cualquier pipeline de **extraer palabras de la imagen**.

## Manejo de Casos Límite Comunes

### ¿Qué pasa si la imagen es en escala de grises?

Algunos motores OCR funcionan mejor con imágenes en color. Si notas una confianza baja en general, intenta convertir el PNG a una versión en blanco y negro de mayor contraste antes de enviarlo al motor. Pillow puede ayudar:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Trabajando con Múltiples Idiomas

Si tu documento contiene tanto inglés como español, querrás **reconocer texto de PNG** usando un modelo multilingüe. La mayoría de los motores permiten establecer la lista de idiomas durante la inicialización:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrar Palabras de Baja Confianza

A veces solo necesitas palabras con confianza superior, por ejemplo, al 90 %. Un filtro rápido se ve así:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Script Completo, Listo para Ejecutar

Uniendo todo, aquí tienes un script único que puedes copiar‑pegar y ejecutar inmediatamente (solo reemplaza la ruta a tu PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Ejecuta con:

```bash
python run_ocr_on_image.py
```

Deberías ver la lista de palabras y porcentajes de confianza impresos en la consola, exactamente como se mostró antes.

## Preguntas Frecuentes

**¿Esto funciona con archivos JPG o TIFF?**  
Claro. El método `setImageFromFile` acepta cualquier formato que la biblioteca subyacente pueda decodificar, así que puedes **ejecutar OCR en archivos de imagen** de tipo JPG, TIFF, BMP, etc.

**¿Puedo procesar varias imágenes en un bucle?**  
Por supuesto. Envuelve los pasos de carga y reconocimiento dentro de un `for` que recorra una lista de rutas de archivo. Solo recuerda volver a inicializar el motor si la biblioteca requiere una nueva instancia por imagen.

**¿Qué pasa si necesito el texto en una sola cadena en lugar de por palabra?**  
La mayoría de los objetos de resultado OCR exponen un método `getText()` que devuelve todo el documento. Ejemplo:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Próximos Pasos y Temas Relacionados

Ahora que sabes **cómo ejecutar OCR en imagen**, considera explorar:

- **Post‑procesamiento**: Usa expresiones regulares para limpiar fechas, montos o IDs extraídos de facturas.  
- **Procesamiento por lotes**: Combina el script con `os.listdir()` para manejar carpetas completas de documentos escaneados.  
- **Bibliotecas alternativas**: `pytesseract` es una opción de código abierto popular; el flujo de trabajo es similar—solo reemplaza las llamadas al motor.  
- **Exportar resultados**: Escribe las palabras extraídas y sus puntuaciones de confianza a CSV para análisis posteriores.

Cada una de estas extensiones se basa directamente en la base que hemos creado aquí, permitiéndote transformar datos OCR crudos en información accionable.

---

### TL;DR

Hemos mostrado un **ejemplo conciso de OCR en python** que demuestra cómo **cargar imagen para OCR**, **ejecutar OCR en imagen**, y **extraer palabras de la imagen** mientras se informa la confianza. El script completo está listo para ejecutarse, y ahora tienes el conocimiento para adaptarlo a cualquier proyecto que necesite **reconocer texto de PNG** (u otros formatos). Pruébalo, ajusta los umbrales de confianza y observa cómo tus aplicaciones se vuelven conscientes del texto en minutos. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}