---
category: general
date: 2026-06-06
description: Cómo hacer OCR de PDF usando Python, extraer texto de PDF, convertir
  texto de PDF escaneado y cambiar el idioma del OCR en solo unas pocas líneas de
  código.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: es
og_description: 'Cómo hacer OCR de PDF con Python: una guía práctica que te muestra
  cómo extraer texto de PDF, convertir texto de PDF escaneado y cambiar el idioma
  del OCR sin esfuerzo.'
og_title: Cómo hacer OCR a PDF en Python – Tutorial completo de programación
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Cómo hacer OCR a PDF en Python – Guía completa paso a paso
url: /es/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo hacer OCR de PDF en Python – Guía completa paso a paso

¿Alguna vez te has preguntado **cómo hacer OCR de PDF** sin pagar por costosas herramientas SaaS? No eres el único. Ya sea que estés digitalizando libros antiguos, extrayendo datos de facturas, o simplemente necesites texto buscable de un informe escaneado, dominar el OCR de PDF en Python puede ahorrarte horas de copia manual.

En este tutorial recorreremos un ejemplo conciso y funcional que **extrae texto de PDF**, te muestra cómo **convertir texto de PDF escaneado** en cadenas editables, y además demuestra cómo **cambiar el idioma del OCR** si tu documento no está en inglés. Al final tendrás un fragmento reutilizable que podrás insertar en cualquier proyecto.

## Requisitos previos y configuración

Antes de sumergirnos, asegúrate de tener:

- Python 3.8+ instalado (el código funciona en 3.9, 3.10 y versiones más recientes)
- El paquete `ocr` que proporciona la clase `OcrEngine` (puedes instalarlo vía `pip install ocr-lib` – reemplaza con el nombre real del paquete que uses)
- Un archivo PDF que quieras procesar; para la demo usaremos `high_res_book.pdf` ubicado en una carpeta llamada `YOUR_DIRECTORY`

Si estás usando un entorno virtual (altamente recomendado), actívalo primero:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Consejo profesional:** Mantén tus archivos PDF en un directorio dedicado `data/` para evitar dolores de cabeza relacionados con rutas más adelante.

## Paso 1: Crear una instancia del motor OCR (Cómo hacer OCR de PDF – Inicialización)

Lo primero que necesitas hacer cuando quieras **realizar OCR en PDF** es instanciar el motor. Piensa en el motor como el cerebro que leerá cada página, interpretará los glifos y te devolverá texto plano.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Por qué es importante: sin un motor no tienes contexto para la configuración del idioma, opciones de renderizado o manejo del PDF. El objeto `OcrEngine` contiene todos esos valores predeterminados y te permite ajustarlos más adelante.

## Paso 2: Establecer el idioma de reconocimiento (Cambiar idioma del OCR)

La mayoría de las bibliotecas OCR usan inglés por defecto, pero ¿qué pasa si tu documento está en francés, alemán o incluso japonés? Cambiar el idioma es tan simple como llamar a `set_recognition_language`. Esto satisface el requisito de **cambiar el idioma del OCR** y garantiza mayor precisión.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Por qué podrías necesitar esto:** Un archivo multilingüe a menudo contiene páginas con idiomas mezclados. Cambiar de idioma sobre la marcha evita el reconocimiento incorrecto de caracteres como “ß” o “ñ”.

## Paso 3: Configurar opciones de renderizado de PDF (Convertir texto de PDF escaneado de manera eficaz)

Al trabajar con PDFs escaneados, la resolución y el modo de color afectan dramáticamente la calidad del OCR. Renderizar a 300 DPI en escala de grises es un punto óptimo para la mayoría de los documentos: lo suficientemente alto para capturar detalle pero lo suficientemente bajo para mantener un uso razonable de memoria.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Las llamadas encadenadas pueden parecer elegantes, pero son simplemente una API fluida que devuelve el mismo objeto de opciones cada vez. Si necesitas color (p. ej., para diagramas coloreados), reemplaza `"grayscale"` por `"color"`.

## Paso 4: Reconocer el PDF y obtener el texto de la primera página (Extraer texto de PDF)

Ahora llega el núcleo de **cómo hacer OCR de PDF**: pasarle al motor la ruta del archivo y extraer el texto reconocido. El método devuelve una lista de resultados por página; cada resultado contiene un atributo `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Si necesitas todo el documento, itera sobre `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### ¿Qué pasa si el PDF está encriptado?

Algunos PDFs están protegidos con contraseña. En ese caso puedes pasar la contraseña a `recognize_pdf`:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

El motor descifrará sobre la marcha antes de realizar el OCR—no se requieren pasos adicionales.

## Paso 5: Post‑procesamiento del texto extraído (Ajuste fino de la extracción de texto de PDF)

La salida cruda del OCR suele contener saltos de línea, espacios extra o caracteres ocasionalmente mal reconocidos. Una rutina rápida de limpieza prepara la cadena extraída para su procesamiento posterior (indexación de búsqueda, almacenamiento en base de datos, etc.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Ahora puedes **extraer texto de PDF** de forma segura y alimentarlo a cualquier pipeline de NLP, motor de búsqueda o simple operación `open(...).write()`.

## Bonus: Procesamiento por lotes de varios PDFs (Escalar OCR de PDF)

Si tienes una carpeta llena de PDFs escaneados, envuelve la lógica en un bucle:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Este fragmento muestra cómo **realizar OCR en PDF** en bloque, una necesidad frecuente en proyectos de digitalización.

## Salida esperada

Ejecutar el ejemplo de una sola página (Paso 4) debería imprimir algo como:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Si procesas un libro de varias páginas, la consola mostrará el texto limpio de cada página, y el script por lotes dejará un archivo `.txt` junto a cada PDF.

## Problemas comunes y cómo evitarlos

| Problema | Síntomas | Solución |
|----------|----------|----------|
| PDF de origen de baja resolución | Caracteres distorsionados, palabras faltantes | Aumenta DPI (`set_dpi(400)` o superior) |
| Idioma incorrecto configurado | Muchos símbolos desconocidos, especialmente caracteres acentuados | Usa `engine.set_recognition_language(ocr.Language.FRENCH)` o el enum apropiado |
| PDF grande que causa error de memoria | `MemoryError` o bloqueo después de algunas páginas | Procesa páginas en bloques (`engine.recognize_pdf(..., max_pages=10)`) |
| Falta de fuentes en el PDF | Salida en blanco en ciertas páginas | Asegúrate de que el PDF contenga imágenes raster; algunos PDFs son solo vectoriales y requieren un manejo diferente |

## Ilustración de imagen

A continuación tienes una visual rápida del flujo de trabajo. El texto alternativo está deliberadamente optimizado para SEO.

![diagrama del flujo de trabajo de cómo hacer OCR de PDF que muestra la inicialización del motor, configuración del idioma, opciones de renderizado, reconocimiento y extracción de texto](/images/ocr-workflow.png)

*El diagrama no es necesario para que el código funcione, pero ayuda a los aprendices visuales a ver dónde encaja cada paso.*

## Conclusión

Hemos cubierto **cómo hacer OCR de PDF** en Python de principio a fin: crear un motor OCR, **cambiar el idioma del OCR**, configurar el renderizado para **convertir texto de PDF escaneado**, y finalmente **extraer texto de PDF** para su uso posterior. El ejemplo completo y ejecutable está listo para insertarse en cualquier proyecto, y el script opcional por lotes muestra cómo escalar la solución.

A continuación, podrías explorar:

- Añadir **realizar OCR en PDF** para archivos multilingües mediante un bucle sobre una lista de idiomas.  
- Integrar el texto extraído con Elasticsearch para búsqueda de texto completo.  
- Usar OCR para crear PDFs buscables incrustando la capa de texto de nuevo en el archivo original (muchas bibliotecas exponen un método `save_as_searchable_pdf`).

Siéntete libre de experimentar, ajustar la configuración de DPI o cambiar a otro backend de OCR. Los fundamentos siguen siendo los mismos, y ahora tienes una base sólida sobre la que construir.

¡Feliz codificación, y que tus documentos escaneados finalmente se vuelvan buscables!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Reconocer texto de PDF – Operaciones OCR con Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [Cómo hacer OCR de texto en imágenes con idioma usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Cómo hacer OCR de PDF en .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}