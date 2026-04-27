---
category: general
date: 2026-04-26
description: cómo usar OCR en PDFs escaneados, extraer texto de un PDF, ejecutar OCR
  en un PDF y convertir un PDF escaneado en archivos buscables en unos pocos pasos.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: es
og_description: 'cómo usar OCR en Python: aprende a extraer texto de PDF, ejecutar
  OCR en PDF y convertir PDF escaneados en documentos buscables.'
og_title: cómo usar OCR – Guía rápida para extraer texto de PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Cómo usar OCR – Extraer texto de PDF con Python
url: /es/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo usar OCR – Extraer texto de PDF con Python

¿Alguna vez te has preguntado **cómo usar OCR** para extraer texto de un contrato, recibo o libro electrónico escaneado? No estás solo. En muchos proyectos del mundo real el PDF que recibes es solo una imagen, y sin OCR no puedes buscar, indexar o analizar su contenido.  

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra **cómo usar OCR**, cómo **extraer texto de PDF**, y por qué podrías querer **convertir PDF escaneado** en documentos buscables. También cubriremos el sutil arte de **cargar PDF como imagen** para que el motor OCR pueda ver cada página con claridad.

> **Vista rápida:** Al final tendrás un script que carga un PDF multipágina, ejecuta OCR en cada página y muestra el texto reconocido, sin necesidad de servicios externos.

## Lo que necesitarás

- Python 3.9+ (cualquier versión reciente funciona)
- paquete `aocr` (o cualquier biblioteca OCR compatible que proporcione `OcrEngine` y `Image.load`)
- Un archivo PDF escaneado que quieras procesar (p. ej., `contract.pdf`)
- Una cantidad moderada de RAM (≈ 200 MB por PDF de 100 páginas suele ser suficiente)

Si aún no has instalado la biblioteca OCR, ejecuta:

```bash
pip install aocr
```

> **Consejo profesional:** Usa un entorno virtual para mantener tus dependencias ordenadas.

## Paso 1: Cargar PDF como Imagen – La primera pieza del rompecabezas

Antes de que pueda ocurrir cualquier OCR, el PDF debe estar representado como una imagen. Aquí es donde entra en juego la palabra clave secundaria **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Por qué importa:* `aocr.Image.load` rasteriza internamente cada página del PDF en un mapa de bits que el motor OCR puede entender. Si omites este paso y alimentas el PDF crudo, el motor generará un error porque espera datos de píxeles, no datos vectoriales.

> **Nota:** La ruta puede ser absoluta o relativa. Asegúrate de que el archivo sea legible; de lo contrario obtendrás un `FileNotFoundError`.

## Paso 2: Ejecutar OCR en PDF – Convertir píxeles en caracteres

Ahora que el PDF vive como una imagen, finalmente podemos **run OCR on PDF**. El siguiente fragmento procesa todas las páginas de una sola vez:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*¿Qué ocurre bajo el capó?* `process_all_pages` recorre las páginas rasterizadas, aplica el modelo OCR y devuelve una lista de objetos de resultado—uno por página. Cada resultado contiene el texto reconocido, puntuaciones de confianza y cajas delimitadoras (si las necesitas más adelante).

## Paso 3: Extraer texto de PDF – Sacar las cadenas

Con los resultados OCR en mano, extraer el texto plano se vuelve trivial. Iteraremos sobre las páginas e imprimiremos la salida, demostrando la palabra clave secundaria **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Salida esperada** (truncada por brevedad):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Si necesitas el texto en una sola cadena, simplemente concatena:

```python
full_text = "\n".join(r.text for r in page_results)
```

Ahora has **extracted text from PDF** usando OCR con éxito.

## Paso 4: Convertir PDF escaneado – Hacerlo buscable

Muchas herramientas posteriores (como Elasticsearch o SharePoint) esperan un PDF buscable en lugar de un volcado de texto plano. Puedes incrustar la salida OCR de nuevo en el PDF original, efectivamente **convert scanned PDF** en una versión buscable.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*¿Por qué molestarse?* Un PDF buscable conserva el diseño y las imágenes originales mientras permite la selección e indexación de texto, una solución ganadora tanto para humanos como para máquinas.

## Problemas comunes y casos límite

### PDFs multipágina más grandes que la memoria

Si tu PDF tiene cientos de páginas, cargar todo de una vez puede agotar la RAM. La biblioteca `aocr` soporta carga diferida:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Luego procesa las páginas una por una:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Escaneos de baja calidad

La precisión del OCR disminuye drásticamente con escaneos borrosos o de bajo contraste. Antes de alimentar la imagen al motor, considera pre‑procesarla:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Soporte de idioma

Por defecto el motor asume inglés. Para **run OCR on PDF** en otro idioma, establece el código de idioma:

```python
ocr_engine.language = "spa"  # Spanish
```

Asegúrate de que el modelo de idioma correspondiente esté instalado.

## Ejemplo completo y funcional

Juntando todo, aquí tienes un script autónomo que puedes guardar como `ocr_pdf.py` y ejecutar inmediatamente:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Ejecuta así:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Verás el texto impreso en la consola, y si proporcionaste `-o`, aparecerá un PDF buscable junto al archivo original.

## Consejos profesionales y buenas prácticas

- **Procesamiento por lotes:** Cuando manejes decenas de PDFs, envuelve la lógica anterior en un bucle y registra el éxito/fracaso de cada archivo.
- **Filtrado por confianza:** Cada `page_result` incluye una métrica de confianza. Descarta o marca las páginas con baja confianza para revisión manual.
- **Paralelismo:** Si tu CPU tiene varios núcleos, considera usar `concurrent.futures` para procesar páginas en paralelo—solo ten cuidado con el uso de memoria.
- **Bloqueo de versión:** La API de `aocr` puede evolucionar. Fija la versión en `requirements.txt` (p. ej., `aocr==2.3.1`) para evitar cambios inesperados.

## Conclusión

Hemos recorrido **cómo usar OCR** para **extraer texto de PDF**, **run OCR on PDF**, **load PDF as image**, e incluso **convert scanned PDF** en un formato buscable. El código está completo, las explicaciones cubren tanto el *qué* como el *por qué*, y ahora dispones de un patrón reutilizable para cualquier proyecto que maneje PDFs basados en imágenes.

¿Qué sigue? Prueba alimentar el texto extraído a una canalización de procesamiento de lenguaje natural, indexa los PDFs buscables con Elasticsearch, o experimenta con diferentes back‑ends OCR como Tesseract o Azure Computer Vision. El cielo es el límite, y las herramientas están a tu alcance.

¡Feliz codificación, y que tus PDFs siempre sean buscables! 

![cómo usar OCR ejemplo](/images/ocr_workflow.png "cómo usar OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}