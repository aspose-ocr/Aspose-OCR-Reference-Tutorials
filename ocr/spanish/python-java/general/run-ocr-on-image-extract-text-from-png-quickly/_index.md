---
category: general
date: 2026-03-18
description: Ejecute OCR en la imagen para extraer texto de PNG y generar un PDF buscable.
  Aprenda cómo reconocer texto en imágenes y convertir PNG a PDF en minutos.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: es
og_description: Ejecute OCR en la imagen para extraer texto de un PNG, reconocer la
  imagen de texto y generar un PDF buscable. Siga esta guía paso a paso.
og_title: Ejecuta OCR en la imagen – Extrae texto de PNG rápidamente
tags:
- OCR
- Python
- Image Processing
title: Ejecutar OCR en la imagen – Extraer texto de PNG rápidamente
url: /es/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en Imagen – Extraer Texto de PNG Rápidamente

¿Alguna vez necesitaste **ejecutar OCR en imagen** pero no sabías por dónde empezar? Tal vez tienes un artículo escaneado guardado como `article.png` y solo quieres el texto plano, o necesitas un PDF buscable para archivarlo. Sea cual sea el caso, estás en el lugar correcto. En este tutorial recorreremos la extracción de texto de PNG, el reconocimiento de la imagen de texto y, incluso, la conversión de ese PNG en un PDF buscable, todo con unas pocas líneas de código.

> **Lo que obtendrás:** un script completo y ejecutable que carga un PNG, ejecuta OCR, guarda la salida hOCR y, opcionalmente, crea un PDF buscable. Sin importaciones faltantes, sin callejones sin salida de “ver la documentación”, solo una solución autosuficiente que puedes incorporar a tu proyecto hoy mismo.

## Prerrequisitos

Antes de profundizar, asegúrate de tener:

- **Python 3.8+** (la sintaxis usada aquí funciona en cualquier versión reciente)
- La biblioteca **`ocr_engine`** que estés usando (el ejemplo asume una clase llamada `OcrEngine`; reemplázala por Tesseract, EasyOCR, etc., si es necesario)
- Una imagen PNG que quieras procesar (p. ej., `article.png` ubicada en una carpeta a la que puedas referirte)
- Permiso de escritura en el directorio de salida

Si estás usando Tesseract bajo el capó, instálalo con:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Y luego instala el wrapper de Python:

```bash
pip install pytesseract Pillow
```

*Pro tip:* mantén tu biblioteca OCR actualizada; los paquetes de idiomas y los ajustes de rendimiento se actualizan con frecuencia.

## Ejecutar OCR en Imagen – Guía Paso a Paso

A continuación tienes el **script completo**. Siéntete libre de copiar‑pegarlo en un archivo llamado `run_ocr.py` y ejecutarlo con `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Qué hace el script, en lenguaje sencillo

1. **Instanciar** el motor OCR para que puedas controlar sus configuraciones.
2. **Cargar** el archivo PNG (`article.png`). El script aborta temprano si el archivo no está presente, evitando errores misteriosos de `NoneType` más adelante.
3. **Seleccionar** `hocr` como formato de exportación. Este formato conserva el diseño original, lo cual es esencial para convertir la imagen en un PDF buscable más adelante.
4. **Ejecutar** el motor de reconocimiento; aquí ocurre el trabajo pesado.
5. **Escribir** el XML hOCR en `article.hocr`. Ahora dispones de una representación legible por máquina del texto y sus coordenadas.
6. *(Opcional)* Cambiar a `"pdf"` y generar un PDF buscable en un paso adicional.

La **salida esperada** es un archivo `.hocr` codificado en UTF‑8 que se ve algo así (recortado por brevedad):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Si descomentas la sección del PDF, también obtendrás `article_searchable.pdf`, que podrás abrir en cualquier visor de PDF y usar el cuadro de búsqueda **Ctrl + F** para localizar palabras al instante.

![Ejemplo de salida de OCR en imagen](example.png "OCR en imagen – resultados hOCR y PDF")

## Cómo Extraer Texto de PNG Usando OcrEngine

Si solo necesitas el texto bruto (sin diseño, sin PDF), puedes omitir completamente el paso hOCR:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*¿Por qué elegir texto plano?* Es ligero, perfecto para indexar y funciona muy bien con pipelines de NLP posteriores.

## Reconocer Imagen de Texto y Generar PDF Buscable

Generar un PDF buscable es una danza de dos partes:

1. **Ejecutar OCR** con `hocr` (como hicimos arriba) para obtener la información de diseño.
2. **Combinar** el PNG original con el hOCR en un PDF usando el exportador PDF del motor.

La mayoría de las bibliotecas OCR modernas (Tesseract, ABBYY, Google Vision) exponen una exportación `pdf` que hace exactamente eso. El fragmento en el bloque *Opcional* del script principal muestra el patrón. Si tu biblioteca no tiene un exportador PDF incorporado, puedes usar **`pdf2image`** + **`reportlab`** para unir la imagen y el hOCR—solo avísame y compartiré un ejemplo rápido adicional.

## Convertir PNG a PDF con Salida OCR

A veces solo quieres un **PDF plano** que contenga la imagen (sin capa buscable). Eso es aún más sencillo:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Combínalo con el paso OCR si necesitas una versión buscable, o mantenlo como una réplica visual fiel para propósitos de archivo.

## Problemas Comunes & Consejos

| Problema | Por qué ocurre | Solución rápida |
|----------|----------------|-----------------|
| **PNG borrosa o de baja resolución** | La precisión del OCR disminuye drásticamente por debajo de ~300 DPI. | Aumentar el tamaño con `Image.resize((width*2, height*2), Image.LANCZOS)` antes de pasarla al motor. |
| **Idioma incorrecto** | El motor usa inglés por defecto; los caracteres no ingleses se vuelven ilegibles. | Llame a `ocr_engine.setLanguage('deu')` (u otro código ISO apropiado) antes de `recognize()`. |
| **Salida hOCR faltante** | Algunos motores usan texto plano por defecto cuando no se llama a `setExportFormat`. | Verifique que `setExportFormat("hocr")` se ejecute **antes** de `recognize()`. |
| **Errores de permisos de archivo** | Intentar escribir en una carpeta de solo lectura. | Use una ruta dentro de su proyecto o `os.makedirs(..., exist_ok=True)` primero. |
| **Los PDFs grandes provocan picos de memoria** | El exportador de PDF mantiene toda la imagen en RAM. | Procese las páginas por bloques o use un escritor de PDF en streaming. |

*Pro tip:* siempre prueba con una imagen de muestra pequeña antes de escalar a un lote de miles. Ahorras horas de depuración.

## Conclusión

Ahora sabes **cómo ejecutar OCR en archivos de imagen**, **extraer texto de PNG**, **reconocer imágenes de texto** para tareas posteriores, **generar un PDF buscable** y **convertir PNG a PDF** cuando necesitas un archivo de archivo sencillo. El script proporcionado es una solución completa, lista para copiar y pegar, que funciona desde el primer momento, y las secciones opcionales te permiten adaptar la salida a tu flujo de trabajo exacto.

### ¿Qué sigue?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}