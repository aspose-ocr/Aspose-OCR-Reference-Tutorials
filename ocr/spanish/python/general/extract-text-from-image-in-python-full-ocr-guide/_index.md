---
category: general
date: 2026-06-25
description: Extrae texto de una imagen usando OCR en Python. Aprende cómo cargar
  la imagen para OCR, realizar OCR en Python y convertir el recibo a JSON en unos
  simples pasos.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: es
og_description: Extrae texto de una imagen usando OCR con Python. Este tutorial te
  guía paso a paso para cargar una imagen para OCR, realizar OCR en Python y convertir
  un recibo a JSON.
og_title: Extraer texto de una imagen en Python – Guía completa de OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Extraer texto de una imagen en Python – Guía completa de OCR
url: /es/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer Texto de una Imagen en Python – Guía Completa de OCR

¿Alguna vez necesitaste **extraer texto de una imagen** pero no sabías por dónde empezar? En este tutorial te guiaremos paso a paso para **cargar la imagen para OCR**, **realizar OCR en Python** y **convertir el recibo a JSON**, todo con solo unas pocas líneas de código.

Si alguna vez has creado una aplicación de escaneo de recibos, un rastreador de gastos, o simplemente quieres automatizar la entrada de datos, verás por qué dominar este flujo es un cambio de juego. Al final tendrás un script funcional que lee una foto de un recibo y genera una carga JSON limpia lista para los servicios posteriores.

## Lo Que Aprenderás

Cubriremos cada paso, desde instalar la biblioteca `aocr` hasta manejar el resultado bruto. Específicamente aprenderás a:

1. **Crear una instancia del motor OCR** – el punto de entrada para todo el trabajo de reconocimiento.  
2. **Cargar una imagen para OCR** – indicar al motor qué archivo leer.  
3. **Elegir el formato de exportación** – JSON o XML, elegiremos JSON porque es más fácil de consumir.  
4. **Ejecutar el reconocimiento** – realizar realmente el OCR en Python.  
5. **Imprimir o almacenar el resultado** – convertir el recibo a JSON y ver la salida.

No se requiere experiencia previa con OCR; solo una configuración básica de Python y un archivo de imagen (un recibo, un volante, lo que necesites).  

---

![Diagrama que muestra el flujo de extracción de texto de una imagen usando OCR de Python](extract-text-from-image-python-ocr.png){alt="extraer texto de una imagen usando OCR de Python"}

## Extraer Texto de una Imagen – OCR en Python Paso a Paso

A continuación tienes el script completo, listo para ejecutar. Siéntete libre de copiar‑pegarlo en un archivo llamado `receipt_ocr.py` y ejecutar `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Por Qué Funciona Esto

- **Instancia del motor** – `aocr.OcrEngine()` encapsula todo el trabajo pesado (carga del modelo, preprocesamiento, etc.).  
- **Cargar la imagen** – `engine.load_image()` le dice a la biblioteca exactamente qué bitmap analizar; puedes usar JPEG, PNG o incluso PDFs multipágina.  
- **Formato de exportación** – Configurar `engine.export_format` a `aocr.ExportFormat.JSON` convierte el resultado en una cadena estructurada, perfecta para APIs que esperan JSON.  
- **Llamada de reconocimiento** – `engine.recognize()` ejecuta la inferencia de la red neuronal detrás de escena; devuelve una cadena JSON que contiene bloques de texto detectados, puntuaciones de confianza e información de diseño.  

---

## Cargar Imagen para OCR con aocr

Si te preguntas si la imagen necesita algún preprocesamiento especial, la respuesta corta es **no**—`aocr` maneja la mayoría de los casos comunes (ajuste de contraste, corrección de inclinación) automáticamente. Sin embargo, puedes mejorar la precisión al:

- Asegurarte de que la imagen tenga al menos 300 dpi.  
- Recortar bordes irrelevantes.  
- Convertir a escala de grises antes de cargarla (opcional, `engine.load_image()` lo hará por ti).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Consejo profesional:* Si el recibo contiene mucho ruido, el paso adicional anterior puede aumentar la **precisión al realizar OCR en Python** de manera notable.

---

## Elegir Formato de Exportación y Convertir Recibo a JSON

Podrías preguntar, “¿Por qué no obtener solo texto plano?” Porque JSON preserva la estructura jerárquica (líneas, palabras, cajas delimitadoras). Esto facilita mucho mapear campos como *monto total* o *fecha* más adelante.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Cuando ejecutes el script, `json_result` tendrá un aspecto similar a este (recortado por brevedad):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Ahora tienes una carga **convertir recibo a JSON** que puedes enviar directamente a una base de datos, un endpoint REST o un modelo de aprendizaje automático.

---

## Ejecutar Reconocimiento y Recuperar Resultados

El paso final—realizar el OCR—es tan simple como llamar a `recognize()`. Detrás de escena la biblioteca:

1. Envía la imagen a través de una red convolucional preentrenada.  
2. Decodifica la salida de la red en caracteres legibles.  
3. Empaqueta todo en el formato seleccionado (JSON en nuestro caso).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Si necesitas almacenar la salida en lugar de imprimirla, simplemente escríbela en un archivo:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Caso límite:* Algunos recibos contienen caracteres no ASCII (p. ej., “€”). Asegúrate de abrir el archivo con codificación UTF‑8, como se muestra arriba, para evitar texto corrupto.

---

## Ejemplo Completo (Todos los Pasos en un Solo Script)

Juntando todo, aquí tienes el script final que puedes ejecutar de principio a fin:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Ejecuta con:

```bash
python receipt_ocr.py
```

Deberías ver una línea de confirmación y, en la misma carpeta, un archivo `receipt_output.json` que contiene los datos estructurados.

---

## Conclusión

Ahora sabes **cómo extraer texto de una imagen** usando Python, cómo **cargar la imagen para OCR**, cómo **realizar OCR en Python** y cómo **convertir el recibo a JSON** para consumo posterior. Este flujo de extremo a extremo es liviano, solo requiere el paquete `aocr` y puede integrarse en cualquier canal de automatización.

¿Qué sigue? Prueba cambiar el formato de exportación a XML, experimenta con diferentes técnicas de preprocesamiento de imágenes, o crea una pequeña API Flask que acepte un recibo cargado y devuelva la carga JSON al instante. El cielo es el límite una vez que domines los conceptos básicos.

¿Tienes preguntas o encontraste algún obstáculo? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué Deberías Aprender a Continuar?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}