---
category: general
date: 2026-03-26
description: Extrae tablas de una imagen y convierte la imagen en una hoja de cálculo
  usando OCR de Python. Aprende cómo cargar la imagen para OCR, leer tablas y extraer
  los datos de la tabla.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: es
og_description: Extrae tablas de una imagen con OCR en Python. Esta guía muestra cómo
  cargar la imagen para OCR, leer las tablas y convertirlas en una hoja de cálculo.
og_title: Extraer tablas de una imagen – Tutorial completo de OCR
tags:
- OCR
- Python
- Data Extraction
title: Extraer tablas de una imagen – Guía OCR paso a paso
url: /es/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer tablas de una imagen – Tutorial completo de OCR

¿Alguna vez necesitaste **extraer tablas de una imagen** pero no sabías por dónde comenzar? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando un PDF o captura de pantalla contiene datos tabulares que deben convertirse en filas y columnas editables. ¿La buena noticia? Unas pocas líneas de código Python, combinadas con un motor OCR sólido, pueden convertir esa imagen en una hoja de cálculo utilizable en segundos.

En este tutorial recorreremos la carga de una imagen para OCR, la ejecución del motor de reconocimiento y la extracción de cada fila de la tabla una por una. Al final podrás **convertir imagen a hoja de cálculo**, y también verás cómo **ocr read tables** y **ocr extract table data** para procesamiento posterior. No hay magia oculta, solo código claro y ejecutable que puedes incorporar a tu proyecto hoy.

---

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener lo siguiente a mano:

- **Python 3.9+** – la última versión estable funciona mejor.
- La biblioteca **`ocr`** (o cualquier SDK OCR compatible que exponga `OcrEngine`, `Image` y métodos relacionados con tablas). Instálala con `pip install ocr‑sdk` (reemplaza con el nombre real del paquete).
- Un archivo de imagen (`.png`, `.jpg`, etc.) que contenga una tabla claramente impresa.  
- Opcional: **pandas** si deseas escribir los datos extraídos directamente a un archivo CSV o Excel (`pip install pandas`).

¿Todo listo? Genial—¡comencemos.

## Paso 1: Importar el SDK OCR y preparar tu entorno

Lo primero: necesitamos traer las clases OCR a nuestro script y configurar un pequeño asistente que más adelante convertirá los datos de tabla sin procesar en un DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Por qué es importante:** Importar `ocr` nos da acceso a `OcrEngine`, `Imaging.Image` y los objetos de tabla que iteraremos. `pandas` no es necesario para la extracción, pero facilita la parte de “convertir imagen a hoja de cálculo”.

## Paso 2: Cargar la imagen que deseas procesar

Ahora realmente **cargamos la imagen para OCR**. El SDK espera un objeto `Image`, así que envolveremos la ruta de nuestro archivo con el método auxiliar `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Consejo profesional:** Mantén tus archivos de imagen en una carpeta dedicada (`assets/` o `data/`) y usa rutas relativas. Así el script permanece portátil entre máquinas.

## Paso 3: Ejecutar el proceso de reconocimiento

Con la imagen adjunta, finalmente podemos indicarle al motor que **ocr read tables**. La llamada `recognize()` devuelve un objeto de resultado que contiene todo lo que el motor descubrió: bloques de texto, líneas y, lo más importante para nosotros, tablas.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Por qué lo verificamos:** Algunas imágenes pueden ser ruidosas o los bordes de la tabla débiles, lo que hace que el motor los omita. Registrar una advertencia te brinda retroalimentación temprana sin romper el script.

## Paso 4: Extraer las filas y celdas de cada tabla

Aquí es donde ocurre la verdadera magia. Iteraremos sobre cada tabla detectada, extraeremos cada fila y luego el texto de cada celda. La comprensión de listas interna hace que el código sea conciso, pero aún así explicaremos el flujo.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**¿Qué está pasando?**  

- `enumerate(..., start=1)` nos da un número de tabla amigable para el registro.  
- `row_obj.get_cells()` devuelve cada objeto celda; `cell.get_text()` obtiene la cadena decodificada por OCR.  
- Guardamos las filas en `rows_data`, luego las pasamos a `pandas.DataFrame` que alinea automáticamente las columnas.  
- El bloque `print` refleja la **salida esencial** mostrada en el fragmento original, para que puedas verificar los resultados al instante.

**Manejo de casos límite:** Si una fila tiene un número diferente de celdas que las demás, `pandas` rellenará los espacios faltantes con `NaN`. Puedes limpiar el DataFrame más tarde con `df.fillna('')` si prefieres cadenas vacías.

## Paso 5: Guardar las tablas extraídas en una hoja de cálculo

Ahora que tenemos una lista de DataFrames, convertirlas en un libro de Excel (o archivos CSV) es muy fácil. Esto cumple el objetivo de “convertir imagen a hoja de cálculo”.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**¿Por qué Excel?** La mayoría de los usuarios empresariales prefieren `.xlsx`. Si prefieres CSV, reemplaza el bucle con `df.to_csv(f"table_{idx}.csv", index=False)`.

## Script completo, listo para ejecutar

Juntando todo, aquí tienes el programa completo que puedes copiar y pegar para ejecutar.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Salida esperada en consola** (asumiendo una tabla simple de 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Y encontrarás `extracted_tables.xlsx` en la carpeta del script, cada tabla en su propia hoja.

## Preguntas frecuentes y consejos

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo usar una biblioteca OCR diferente?** | Absolutamente. El patrón sigue siendo el mismo: cargar imagen → reconocer → iterar sobre `get_tables()`. Simplemente reemplaza las importaciones y los nombres de los objetos. |
| **¿Qué pasa si mi imagen es ruidosa?** | Pre‑procesa con OpenCV (umbralizado, corrección de inclinación) antes de pasarla al motor OCR. La reducción de ruido suele mejorar la precisión de **ocr extract table data**. |
| **¿Necesito instalar `openpyxl`?** | Sí, `pandas` lo utiliza internamente para la salida a Excel. Instálalo con `pip install openpyxl`. |
| **¿Cómo manejo celdas combinadas?** | Algunos SDK exponen `cell.is_merged()`; puedes detectar y propagar el valor a través del rango combinado manualmente. |
| **¿Hay una forma de extraer solo tablas específicas?** | Filtra por `table_obj.get_confidence()` o verificando palabras clave en el encabezado antes de procesar. |

## Conclusión

Ahora tienes una solución completa, de extremo a extremo, para **extraer tablas de una imagen**, convertir el resultado en una hoja de cálculo ordenada y manejar incluso múltiples tablas en una sola imagen. El script muestra cómo **load image for OCR**, **ocr read tables**, y **ocr extract table data** manteniéndose lo suficientemente flexible para variaciones del mundo real.

¿Qué sigue? Prueba alimentar al motor OCR con una página PDF renderizada como imagen, o experimenta con diferentes idiomas y fuentes. También podrías canalizar los DataFrames directamente a una base de datos o a una herramienta de informes—tu imaginación es el límite.

Si encontraste útil esta guía, siéntete libre de compartirla, dar una estrella al repositorio que aloja el SDK, o dejar un comentario con tus propios trucos. ¡Feliz codificación, y que tus tablas siempre se analicen perfectamente!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}