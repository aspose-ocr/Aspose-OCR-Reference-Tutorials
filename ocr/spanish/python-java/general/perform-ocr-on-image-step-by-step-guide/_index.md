---
category: general
date: 2026-03-18
description: Realiza OCR en una imagen para extraer texto rápidamente. Aprende cómo
  cargar la imagen para OCR, crear el motor OCR y mejorar la precisión del OCR con
  opciones de idioma.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: es
og_description: Realiza OCR en una imagen con esta guía detallada. Aprende a cargar
  la imagen para OCR, crear el motor OCR y mejorar la precisión del OCR para una extracción
  de texto fiable.
og_title: Realiza OCR en una imagen – Tutorial completo de programación
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Realizar OCR en una imagen – Guía paso a paso
url: /es/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR en Imagen – Tutorial de Programación Completo

¿Alguna vez necesitaste **perform OCR on image** pero no estabas seguro de qué biblioteca elegir o cómo obtener resultados fiables? No estás solo. En esta guía repasaremos todo lo que necesitas para **extract text from image**, desde cargar la foto hasta ajustar las opciones de idioma para que puedas **improve OCR accuracy** en cada paso.

Cubriremos cómo **load image for OCR**, cómo **create OCR engine**, y por qué cada configuración es importante. Al final tendrás un script listo‑para‑ejecutar que imprime el texto reconocido, y entenderás el “por qué” detrás de cada línea—sin atajos vagos de “ver la documentación”. ¡Vamos allá!

## Lo que necesitarás

- Python 3.8+ (el código usa f‑strings y anotaciones de tipo)
- El paquete hipotético `ocr_lib` – instálalo con `pip install ocr_lib`
- Un archivo de imagen que contenga texto impreso claro (p.ej., `lab_report.png`)
- Un editor de texto básico o IDE (VS Code, PyCharm, lo que prefieras)

Si ya tienes todo eso, genial—estás listo. Si no, descarga Python desde python.org y ejecuta el comando pip; solo te tomará un minuto.

![ejemplo de realizar OCR en imagen](/images/ocr-example.png)

*Texto alternativo: perform OCR on image – muestra de salida con texto extraído.*

## Paso 1: Crear motor OCR – Cómo **create OCR engine** en Python

Antes de que pueda ocurrir cualquier reconocimiento, la biblioteca necesita un objeto motor que mantenga la configuración y el estado en tiempo de ejecución. Piensa en el motor como el cerebro detrás de la operación.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Why this matters:** Instanciar el motor temprano te permite adjuntar opciones de idioma más tarde, y también almacena en caché los modelos internos para llamadas posteriores más rápidas.

## Paso 2: Cargar imagen para OCR – La forma correcta de **load image for OCR**

Ahora que tenemos un motor, debemos darle algo que leer. El método `setImageFromFile` acepta una ruta del sistema de archivos; la ruta puede ser absoluta o relativa al directorio de trabajo del script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** Usa una ruta absoluta o `os.path.join` para evitar sorpresas de “archivo no encontrado” cuando el script se ejecute desde una carpeta diferente.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Paso 3: Mejorar la precisión del OCR – Ajustando **language options** para **improve OCR accuracy**

El OCR listo para usar funciona, pero los vocabularios específicos de dominio (como la jerga de laboratorio) a menudo lo confunden. Al proporcionar un diccionario personalizado y una lista negra reduces los errores de reconocimiento, como confundir “0” con “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Why this helps:** El diccionario le indica al modelo OCR que “HPLC” es un token válido, evitando que divida la palabra en sin sentido. La lista negra le dice al modelo que trate los símbolos ambiguos como ruido, lo que **improves OCR accuracy** directamente.

## Paso 4: Realizar OCR en Imagen – La llamada central **perform OCR on image**

Con el motor preparado y la imagen adjunta, es hora de reconocer realmente el texto. Este paso devuelve un objeto `OcrResult` que puedes consultar para obtener texto sin procesar, puntuaciones de confianza o cajas delimitadoras.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Si la imagen está borrosa, verás números de confianza más bajos en el resultado. Eso es una señal para pre‑procesar la imagen (p.ej., aumentar el contraste) antes de enviarla al motor.

## Paso 5: Extraer texto de la imagen – Sacando la cadena final

Finalmente, solicitamos al `OcrResult` su representación textual. El método `getText()` devuelve una cadena de texto plano lista para procesamiento posterior (guardarla en un archivo, enviarla a una base de datos, etc.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Expected output:** Suponiendo que `lab_report.png` contenga una tabla simple, podrías ver algo como:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Eso completa la parte de **extract text from image**.

## Ejemplo completo funcionando – Junta todo

A continuación tienes un script único que une las piezas de las secciones anteriores. Puedes copiar‑pegarlo en `run_ocr.py` y ejecutar `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Lista de verificación rápida

| ✅ | Elemento |
|---|------|
| ✔️ | El motor está creado (`create OCR engine`) |
| ✔️ | La imagen está cargada (`load image for OCR`) |
| ✔️ | Las opciones de idioma están configuradas (`improve OCR accuracy`) |
| ✔️ | Se realiza OCR (`perform OCR on image`) |
| ✔️ | El texto está extraído (`extract text from image`) |

Ejecuta el script y observa la consola. Si ves el bloque “OCR Output” con el contenido de tu informe, has **performed OCR on image** con éxito.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Entrada borrosa** | El modelo OCR no puede distinguir los caracteres | Pre‑procesar con OpenCV: `cv2.GaussianBlur` o aumentar DPI |
| **Idioma incorrecto** | El idioma predeterminado puede estar configurado a algo distinto del inglés | Llamar a `engine.setLanguage("eng")` antes de `recognize()` |
| **Términos de diccionario faltantes** | Las palabras específicas del dominio se vuelven ilegibles | Añadirlas mediante `setDictionary` como se muestra en el Paso 3 |
| **Los caracteres en la lista negra causan |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}