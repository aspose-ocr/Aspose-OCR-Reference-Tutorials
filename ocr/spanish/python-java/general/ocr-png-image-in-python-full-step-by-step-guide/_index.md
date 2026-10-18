---
category: general
date: 2026-06-06
description: OCR de imagen PNG con Python – aprende cómo extraer texto de una imagen,
  ejecutar un ejemplo de OCR en Python e incluso leer texto en griego antiguo fácilmente.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: es
og_description: OCR de imágenes PNG en Python explicado. Esta guía muestra cómo extraer
  texto de una imagen, ejecutar un ejemplo de OCR en Python y leer griego antiguo
  con facilidad.
og_title: OCR de imagen PNG en Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR de imagen PNG en Python – Guía completa paso a paso
url: /es/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image en Python – Guía Completa Paso a Paso

¿Alguna vez te has preguntado cómo **OCR PNG image** archivos directamente desde un script de Python? Tal vez tengas una carpeta llena de manuscritos antiguos escaneados y necesites **extract text from image** archivos sin tener que escribir todo manualmente. La buena noticia es que no necesitas un doctorado en visión por computadora—solo unas pocas líneas de código y la biblioteca adecuada, y estarás leyendo griego antiguo en segundos.

En este tutorial recorreremos un **python OCR example** que reconoce texto de un PNG, establece el idioma a Greek polytonic y muestra el resultado. Al final sabrás exactamente cómo **recognize image text**, manejar problemas comunes y adaptar el script a otros idiomas o formatos de imagen.

## Lo Que Aprenderás

- Instalar y configurar una biblioteca OCR para Python (pytesseract + Tesseract OCR)
- Crear una instancia del motor OCR y cargar un archivo PNG
- Establecer el idioma de reconocimiento a Greek polytonic para que puedas **read ancient greek**
- Mostrar el texto reconocido y solucionar problemas típicos
- Extender el script para procesar por lotes varios PNGs o cambiar a otro idioma

### Requisitos Previos

| Requisito | Por qué es importante |
|-------------|----------------|
| Python 3.8+ | Sintaxis moderna y anotaciones de tipo |
| `pytesseract` package | Pequeña capa alrededor del motor Tesseract |
| Tesseract OCR binaries (≥ 5.0) | El motor real que realiza el trabajo pesado |
| Greek language data (`grc.traineddata`) | Necesario para **read ancient greek** correctamente |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Nuestro objetivo para la demostración **ocr png image** |

Puedes instalar la parte de Python con:

```bash
pip install pytesseract Pillow
```

Y en Ubuntu/macOS agregarías el motor en sí:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

No olvides descargar los datos entrenados Greek polytonic:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(La ruta puede variar; ajusta `TESSDATA_PREFIX` si es necesario.)*

## OCR PNG Image: Crear la Instancia del Motor

Lo primero que necesitamos es un objeto que se comunique con Tesseract. En `pytesseract` el motor se accede mediante funciones a nivel de módulo, pero para mayor claridad lo envolveremos en una pequeña clase. Esto refleja el concepto de “engine” que viste en el fragmento original.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**¿Por qué envolverlo?**  
- Mantiene la API pública idéntica al fragmento con el que comenzaste, facilitando la migración.  
- Nos permite añadir registro o manejo de errores más tarde sin tocar el flujo principal.  
- Demuestra una buena práctica de OOP—algo que los desarrolladores senior aprecian.

## Extraer Texto de la Imagen: Establecer el Idioma a Greek Polytonic

Ahora que tenemos un motor, necesitamos indicarle qué idioma esperar. Greek polytonic usa diacríticos que no están cubiertos por los datos estándar “greek”, así que apuntamos Tesseract al archivo entrenado `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Si alguna vez deseas **extract text from image** archivos en otro idioma, simplemente reemplaza `"grc"` por `"eng"` para inglés, `"fra"` para francés, etc. La misma línea funciona para cualquier idioma que tengas instalado.

## Reconocer Texto de Imagen: Ejecutar el OCR en un PNG

Con el idioma configurado, alimentamos el PNG al motor. El ejemplo original usaba una ruta codificada; lo haremos un poco más flexible usando objetos `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Consejos y Casos Límite**

- **File not found** – envuelve la llamada en un `try/except FileNotFoundError` para dar un mensaje amigable.  
- **Low‑resolution PNG** – considera pre‑procesar (p. ej., redimensionar, binarizar) con Pillow antes del OCR.  
- **Non‑Greek text** – Tesseract seguirá intentando decodificar, pero la precisión disminuye drásticamente. Siempre coincide con el idioma.

## Mostrar el Texto Reconocido

Finalmente, imprimimos el resultado. En un proyecto real podrías escribir a una base de datos, un CSV, o incluso alimentarlo a una canalización de traducción.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Cuando ejecutes el script contra un escaneo claro de una inscripción griega antigua, deberías ver algo como:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Si la salida se ve desordenada, verifica que el archivo **greek.traineddata** esté en la carpeta correcta y que el PNG no sea demasiado ruidoso.

## Ejemplo Completo Funcional (Todos los Pasos en un Solo Script)

A continuación se muestra el programa completo, listo para ejecutar. Guárdalo como `ocr_greek.py` y ejecuta `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Salida esperada** (truncada por brevedad):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Si ves los caracteres griegos correctos, ¡felicitaciones—has realizado con éxito una operación **ocr png image** en Python!

## Preguntas Comunes y Consejos Profesionales

### ¿Cómo mejoro la precisión en un PNG ruidoso?

- Convierte la imagen a escala de grises: `img = img.convert('L')`
- Aplica un umbral binario: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Aumenta la escala con `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Estos pasos a menudo convierten una pesadilla de **recognize image text** en un resultado limpio.

### ¿Puedo procesar una carpeta completa de PNGs?

Absolutamente. Envuelve la llamada `recognize_image` en un bucle `for` sobre `Path.glob("*.png")`. Guarda cada resultado en un diccionario o escríbelo a un CSV para análisis posterior.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### ¿Qué pasa si solo necesito extraer números?

Pasa una cadena **config** personalizada a `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

De esa manera puedes **extract text from image** archivos que contengan tablas, números de serie o marcas de tiempo.

### ¿Hay una forma de obtener puntuaciones de confianza?

Sí—usa `pytesseract.image_to_data` que devuelve un TSV con la confianza por palabra. Puedes filtrar los tokens de baja confianza antes de ensamblar la cadena final.

## Extender el Tutorial

Ahora que dominas los conceptos básicos, considera explorar estos temas relacionados:

- **Batch OCR with multiprocessing** – acelera grandes corpora de PNGs.  
- **Hybrid OCR + NLP pipelines** – traduce automáticamente el griego antiguo extraído al inglés moderno.  
- **Alternative engines** – prueba `easyocr` o métodos basados en `opencv` para casos de uso específicos.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision o AWS Textract para escalado sin servidor.  

Cada uno de estos se basa en el núcleo **python ocr example** que acabamos de cubrir, por lo que te sentirás cómodo profundizando más.

## Conclusión

Hemos tomado un fragmento simple y lo hemos convertido en un flujo de trabajo robusto **ocr png image** en Python. Al crear un `OcrEngine`, establecer el idioma a Greek polytonic, alimentar un PNG y imprimir el resultado, ahora sabes cómo **extract text from image** archivos, **recognize image text**, e incluso **read ancient greek**.

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer Texto de Imagen con Aspose OCR – Guía Paso a Paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cómo Establecer el Valor de Umbral en el Reconocimiento OCR de Imagen](/ocr/english/net/ocr-settings/set-threshold-value/)
- [reconocer texto de imagen con Aspose OCR para varios idiomas](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}