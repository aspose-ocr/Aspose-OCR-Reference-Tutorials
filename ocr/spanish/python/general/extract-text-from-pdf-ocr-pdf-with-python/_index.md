---
category: general
date: 2026-04-29
description: Extrae texto de PDF usando Aspose OCR en Python. Aprende el procesamiento
  por lotes de OCR en PDF, convierte texto de PDF escaneado y maneja páginas de baja
  confianza.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: es
og_description: Extrae texto de PDF con Aspose OCR en Python. Esta guía muestra el
  procesamiento por lotes de OCR en PDF, la conversión de texto de PDF escaneado y
  el manejo de resultados de baja confianza.
og_title: Extraer texto de PDF – OCR de PDF con Python
tags:
- OCR
- Python
- PDF processing
title: Extraer texto de PDF – OCR PDF con Python
url: /es/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de PDF – OCR PDF con Python

¿Alguna vez necesitaste **extraer texto de PDF** pero el archivo es solo una imagen escaneada? No estás solo—muchos desarrolladores se topan con ese obstáculo al intentar convertir PDFs en datos buscables. ¿La buena noticia? Con Aspose OCR para Python puedes convertir texto de PDF escaneado en unas pocas líneas, e incluso ejecutar **procesamiento por lotes de OCR en PDF** cuando tienes docenas de archivos que manejar.

En este tutorial recorreremos todo el flujo de trabajo: configurar la biblioteca, ejecutar OCR en un PDF único, escalar a un lote y manejar páginas con baja confianza para que sepas cuándo se requiere una revisión manual. Al final tendrás un script listo para ejecutar que extrae texto de cualquier PDF escaneado, y comprenderás el porqué de cada paso.

## Lo que necesitarás

Antes de sumergirnos, asegúrate de contar con:

- Python 3.8 o superior (el código usa f‑strings, por lo que 3.6+ funciona, pero se recomienda 3.8+)
- Una licencia de Aspose OCR para Python o una clave de prueba gratuita (puedes obtener una en el sitio web de Aspose)
- Una carpeta con uno o más PDFs escaneados que deseas procesar
- Una cantidad moderada de espacio en disco para los informes *.txt* generados

Eso es todo—sin dependencias externas pesadas, sin trucos de OpenCV. El motor Aspose OCR hace el trabajo pesado por ti.

## Configurando el entorno

Primero, instala el paquete Aspose OCR desde PyPI:

```bash
pip install aspose-ocr
```

Si tienes un archivo de licencia (`Aspose.OCR.lic`), colócalo en la raíz de tu proyecto y actívalo de la siguiente manera:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Consejo profesional:** Mantén el archivo de licencia fuera del control de versiones; añádelo a `.gitignore` para evitar su exposición accidental.

## Realizando OCR en un PDF único

Ahora extraigamos texto de un PDF escaneado único. Los pasos principales son:

1. Crear una instancia de `OcrEngine`.
2. Apuntarlo al archivo PDF.
3. Obtener un `OcrResult` para cada página.
4. Escribir la salida de texto plano en disco.
5. Liberar el motor para liberar recursos nativos.

Aquí tienes el script completo y ejecutable:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Lo que verás:** Para cada página el script imprime algo como `Page 1: confidence 97.45%`. Si una página está por debajo del umbral del 80 %, aparece una advertencia, indicándote que el OCR podría haber omitido caracteres.

### Por qué funciona esto

- `OcrEngine` es la puerta de enlace a la biblioteca nativa Aspose OCR; maneja todo, desde el preprocesamiento de imágenes hasta el reconocimiento de caracteres.
- `extract_from_pdf` rasteriza automáticamente cada página del PDF, por lo que no necesitas convertir el PDF a imágenes tú mismo.
- Los puntajes de confianza te permiten automatizar verificaciones de calidad—crítico cuando procesas documentos legales o médicos donde la precisión es importante.

## Procesamiento por lotes de OCR en PDF con Python

La mayoría de los proyectos del mundo real involucran más de un archivo. Extendamos el script de un solo archivo a una canalización de **procesamiento por lotes de OCR en PDF** que recorra un directorio, procese cada PDF y almacene los resultados en una subcarpeta correspondiente.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Cómo ayuda esto

- **Escalabilidad:** La función recorre la carpeta una vez, creando una subcarpeta de salida dedicada para cada PDF. Esto mantiene todo ordenado cuando tienes docenas de documentos.
- **Reusabilidad:** `ocr_pdf_file` puede ser llamado desde otros scripts (p. ej., un servicio web) porque es una función pura.
- **Manejo de errores:** El script imprime un mensaje amigable si la carpeta de entrada está vacía, evitándote un fallo silencioso.

## Conversión de texto de PDF escaneado – Manejo de casos límite

Aunque el código anterior funciona para la mayoría de los PDFs, podrías encontrar algunos inconvenientes:

| Situación | Por qué ocurre | Cómo mitigar |
|-----------|----------------|--------------|
| **PDFs encriptados** | El PDF está protegido con contraseña. | Pasa la contraseña a `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Documentos multilingües** | Aspose OCR usa inglés por defecto. | Establece `ocr_engine.language = "spa"` para español, o proporciona una lista para idiomas mixtos. |
| **PDFs muy grandes (>500 páginas)** | El uso de memoria se dispara porque cada página se carga en RAM. | Procesa el PDF en bloques usando `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` y repite en un bucle. |
| **Calidad de escaneo pobre** | Baja DPI o mucho ruido reduce la confianza. | Pre‑procesa el PDF con `engine.image_preprocessing = True` o aumenta la DPI mediante `engine.dpi = 300`. |

> **¡Cuidado!** Activar el preprocesamiento de imágenes puede aumentar notablemente el tiempo de CPU. Si ejecutas un lote nocturno, programa suficiente tiempo o lanza un trabajador separado.

## Verificando la salida

Después de que el script termine, encontrarás una estructura de carpetas como:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Abre cualquier archivo `.txt`; deberías ver texto limpio codificado en UTF‑8 que refleja el contenido escaneado original. Si notas caracteres distorsionados, verifica la configuración de idioma del PDF y asegúrate de que los paquetes de fuentes correctos estén instalados en la máquina.

## Liberando recursos

Aspose OCR depende de DLLs nativas, por lo que es esencial llamar a `engine.dispose()` una vez que hayas terminado. Olvidar este paso puede provocar fugas de memoria, especialmente en trabajos por lotes de larga duración.

```python
# Always the last line of your script
engine.dispose()
```

## Ejemplo completo de extremo a extremo

Juntando todo, aquí tienes un único

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}