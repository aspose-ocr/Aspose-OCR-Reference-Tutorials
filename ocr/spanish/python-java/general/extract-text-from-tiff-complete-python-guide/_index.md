---
category: general
date: 2026-06-16
description: Extrae texto de archivos TIFF usando OCR en Python. Aprende cómo convertir
  TIFF a texto paso a paso, manejando documentos multipágina con facilidad.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: es
og_description: Extrae texto de archivos TIFF con OCR en Python. Sigue esta guía para
  convertir TIFF a texto, manejar escaneos multipágina y obtener resultados limpios.
og_title: Extraer texto de TIFF – Guía completa de Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Extraer texto de TIFF – Guía completa de Python
url: /es/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer Texto de TIFF – Guía Completa en Python

¿Alguna vez necesitaste **extraer texto de imágenes TIFF** pero no sabías por dónde empezar? No estás solo: muchos desarrolladores se encuentran con este obstáculo al trabajar con archivos escaneados o documentos heredados. ¿La buena noticia? Con unas pocas líneas de Python puedes **convertir TIFF a texto** en un instante, incluso cuando el archivo contiene docenas de páginas.

En este tutorial recorreremos un ejemplo del mundo real: cargar un TIFF multipágina, establecer el idioma del OCR a francés y obtener el texto reconocido de cada página. Al final tendrás un script listo para ejecutar, comprenderás por qué cada paso es importante y sabrás cómo adaptarlo a otros idiomas o formatos de imagen.

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

- Python 3.8 o superior instalado.
- El paquete `ocr` (o cualquier biblioteca OCR compatible que ofrezca una clase `OcrEngine`). Puedes instalarlo con `pip install ocr-lib`; reemplaza con el nombre real del paquete que estés usando.
- Un archivo TIFF multipágina (p. ej., `french-scans.tif`) que quieras procesar.
- Familiaridad básica con la escritura de scripts en Python.

Sin dependencias pesadas, sin servicios externos: solo Python puro y un motor OCR.

---

## Paso 1: Configurar el Motor OCR para **Extraer Texto de TIFF**

Lo primero es crear una instancia del motor OCR y decirle qué idioma usar. En nuestro caso el material fuente está en francés, así que configuraremos el idioma en consecuencia.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Por qué es importante:**  
La configuración del idioma mejora drásticamente la precisión. Caracteres franceses como “é” o “ç” se leerían como símbolos genéricos si el motor usa inglés por defecto. Al seleccionar explícitamente francés le damos al motor el mapa de caracteres correcto.

> **Consejo profesional:** Si procesas documentos en varios idiomas, puedes cambiar `engine.language` sobre la marcha antes de cada llamada a `recognize()`.

---

## Paso 2: Cargar el TIFF Multipágina que Deseas **Convertir TIFF a Texto**

Un TIFF puede contener varios fotogramas; piensa en cada fotograma como una página distinta. La biblioteca OCR abstrae eso para nosotros, así que simplemente le indicamos el archivo.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Alerta de caso límite:**  
Si la ruta del archivo es incorrecta o el TIFF está corrupto, el método `load_from_file` lanzará una excepción. En código de producción envuélvelo en un bloque `try/except`:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Paso 3: Ejecutar OCR en Todo el Documento – El Núcleo de **Extraer Texto de TIFF**

Ahora dejamos que el motor haga su magia. La llamada `recognize()` procesa todas las páginas de una vez y devuelve un objeto de resultado rico.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**¿Qué ocurre bajo el capó?**  
El motor itera sobre cada fotograma, aplica pre‑procesamiento (desviación, binarización), ejecuta la red neuronal y agrega la salida. Como llamamos a `recognize()` solo una vez, la biblioteca puede compartir recursos entre páginas, lo que es más rápido que iterar manualmente.

---

## Paso 4: Obtener el Texto Reconocido del Resultado JSON – **Convertir TIFF a Texto** Página por Página

El objeto de resultado puede serializarse a JSON. Dentro de ese JSON encontrarás un arreglo `pages`, cada uno con un campo `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Ahora disponemos de una lista de Python limpia donde cada elemento corresponde a la salida OCR de una página.

---

## Paso 5: Imprimir o Guardar el Texto de Cada Página – La pieza final de **Extraer Texto de TIFF**

Recorremos las páginas y mostramos el texto extraído. También podrías escribir cada página en un archivo `.txt` separado si lo prefieres.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Salida esperada (ejemplo)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Si el OCR tuvo éxito, verás un bloque limpio de frases en francés para cada página. Si notas caracteres distorsionados, verifica la configuración del idioma o considera aumentar la resolución de la imagen antes del OCR.

---

## Manejo de Problemas Comunes al **Convertir TIFF a Texto**

| Problema | Por qué ocurre | Solución rápida |
|----------|----------------|-----------------|
| **Arreglo `pages` vacío** | El TIFF no se cargó correctamente o no tiene fotogramas. | Verifica la ruta del archivo y asegura que el TIFF no sea un PNG de una sola página disfrazado de TIFF. |
| **Caracteres basura** | Incompatibilidad de idioma o baja calidad de imagen. | Establece el `engine.language` correcto y pre‑procesa la imagen (p. ej., aumenta DPI). |
| **Consumo excesivo de memoria en TIFF muy grandes** | Cargar todas las páginas a la vez consume RAM. | Procesa en bloques: carga un fotograma, reconoce, descarta y pasa al siguiente. |
| **Errores Unicode al imprimir** | La codificación de la consola no soporta caracteres acentuados. | Usa `print(page["text"].encode('utf-8').decode('utf-8'))` o configura tu terminal para UTF‑8. |

---

## Extender el Script: De **Extraer Texto de TIFF** a Procesamiento por Lotes

Ahora que tienes una base sólida, considera los siguientes pasos:

1. **Conversión por lotes** – Envuelve todo el flujo en una función `def ocr_tiff(path):` y recorre un directorio de archivos TIFF.
2. **Salida a archivos** – En lugar de imprimir, escribe el texto de cada página en `page_{i}.txt` o concatena todo en un solo documento.
3. **Motores OCR alternativos** – Si necesitas mayor precisión, sustituye `ocr.OcrEngine()` por Tesseract (`pytesseract`) o Azure Cognitive Services, manteniendo la misma lógica de “extraer texto de TIFF”.
4. **Post‑procesamiento** – Ejecuta corrector ortográfico, detección de idioma o limpieza con expresiones regulares para pulir la salida OCR cruda.

---

## Script Completo, Listo para Ejecutar

A continuación tienes el código completo, listo para copiar y pegar. Incluye manejo básico de errores y la opción de guardar el texto de cada página en archivos separados.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Ejecuta este script, apunta `tiff_file` a tu documento y observa cómo la consola se llena de frases en francés limpias. Si proporcionas `out_folder`, también encontrarás una serie de archivos `page_#.txt` listos para el procesamiento posterior.

---

## Conclusión

Acabamos de **extraer texto de archivos TIFF** usando un flujo OCR sencillo en Python, y ahora sabes cómo **convertir TIFF a texto** de forma fiable. Desde inicializar el motor con el idioma correcto hasta iterar sobre el resultado JSON de cada página, cada paso se explicó con el “por qué” detrás, para que puedas adaptar el patrón a otros idiomas, formatos de imagen o trabajos por lotes más grandes.

¿Qué sigue? Prueba cambiar el backend OCR por Tesseract, experimenta con diferentes paquetes de idioma o integra la salida en una base de datos searchable. El cielo es el límite cuando puedes transformar imágenes escaneadas en texto buscable.

¡Deja un comentario si encuentras algún obstáculo o tienes ideas para mejoras! ¡Feliz codificación!

## ¿Qué Deberías Aprender a Continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}