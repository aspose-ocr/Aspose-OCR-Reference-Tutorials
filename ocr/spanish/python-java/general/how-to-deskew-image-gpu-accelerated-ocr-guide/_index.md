---
category: general
date: 2026-01-02
description: Aprende a corregir la inclinación de la imagen y a mejorar el contraste
  para obtener texto plano rápidamente. Incluye código Python paso a paso y consejos
  para extraer texto.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: es
og_description: Cómo enderezar una imagen y mejorar el contraste para obtener texto
  plano. Ejemplo completo en Python con extracción de tablas y aceleración GPU.
og_title: Cómo enderezar una imagen – Tutorial completo de OCR con GPU
tags:
- OCR
- Python
- Image Processing
title: Cómo enderezar una imagen – Guía de OCR acelerada por GPU
url: /es/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo **how to deskew image** – Guía OCR acelerada por GPU

¿Alguna vez te has preguntado **how to deskew image** cuando tus recibos llegan en ángulo? No estás solo; una foto inclinada puede convertir un recibo perfectamente legible en un desastre confuso. La buena noticia es que con unas pocas líneas de Python puedes auto‑deskew, aumentar el contraste y extraer texto plano limpio—sin necesidad de Photoshop manual.

En este tutorial recorreremos un ejemplo completo y ejecutable que no solo muestra **how to deskew image**, sino también **how to boost contrast**, cómo **get plain text**, e incluso **how to extract text** de las tablas que descubre el motor OCR. Al final tendrás un script autónomo que puedes incorporar en cualquier proyecto.

## Lo que necesitarás

- Python 3.9+ instalado (el código usa anotaciones de tipo, así que un intérprete reciente ayuda)
- La biblioteca `ocr` que proporciona `OcrEngine`, `EngineMode`, `ImageProcessingOptions` y `OcrResult` (instálala vía `pip install ocr‑sdk` – reemplaza con el nombre real del paquete que uses)
- Una GPU con controladores compatibles si deseas el aumento de velocidad (opcional pero recomendado)
- Un archivo de imagen que esté ligeramente rotado o con bajo contraste, por ejemplo, `receipt_skewed.jpg`

> **Consejo profesional:** Si no tienes una GPU, simplemente cambia `EngineMode.GPU` a `EngineMode.CPU` y el script seguirá funcionando—solo un poco más lento.

## Implementación paso a paso

A continuación dividimos la solución en bloques lógicos. Cada bloque tiene un **H2** descriptivo que contiene la palabra clave principal *how to deskew image* o una de las palabras clave secundarias. El código está completo, comentado y listo para ejecutarse.

### how to deskew image con OCR acelerado por GPU

Lo primero que hacemos es indicarle al motor OCR que se ejecute en la GPU y habilitar la función auto‑deskew. Auto‑deskew analiza la geometría de la imagen y la rota de nuevo a posición vertical.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Por qué es importante:** La aceleración por GPU puede reducir el tiempo de procesamiento de segundos a milisegundos, lo cual es crucial cuando manejas decenas de recibos por minuto.

### Aumentar el contraste de la imagen para un mejor reconocimiento

Un recibo de bajo contraste es una pesadilla para cualquier sistema OCR. Al aumentar el contraste le damos al motor bordes más claros con los que trabajar.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Cómo aumentar el contraste:** El método `set_contrast_boost` acepta un porcentaje; 30 % es un valor predeterminado seguro que funciona para la mayoría de los recibos escaneados. Si tus imágenes son extremadamente oscuras, súbelo al 50 % o experimenta.

### Obtener texto plano de la imagen procesada

Ahora que la imagen está recta y brillante, la enviamos al motor y solicitamos el resultado de texto plano.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Salida esperada (truncada por brevedad):**

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Cómo obtener texto plano:** El método `get_text()` elimina cualquier información de diseño y devuelve una cadena limpia, que puedes almacenar en una base de datos, enviar a una API o alimentar a análisis posteriores.

### how to extract text de tablas detectadas

A menudo los recibos contienen datos tabulares (artículos, cantidades, precios). El SDK OCR puede detectar tablas y permitirte iterar sobre filas y celdas.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Salida de tabla de ejemplo:**

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Por qué extraer tablas:** Los datos estructurados facilitan el cálculo de totales, la generación de informes o su integración en software contable.

### Script completo y funcional

Uniendo todo, aquí tienes el script que puedes copiar‑pegar en `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Ejecuta con:

```bash
python deskew_and_ocr.py
```

Deberías ver el texto limpiado y cualquier tabla detectada impresa en la consola.

## Casos límite comunes y cómo manejarlos

| Situación | Qué hacer |
|-----------|-----------|
| **La imagen está al revés** | Incrementa la confianza de `set_auto_deskew(True)` llamando también a `set_rotation_correction(True)` si el SDK lo ofrece. |
| **El aumento de contraste hace la imagen demasiado brillante** | Reduce el porcentaje pasado a `set_contrast_boost` (p.ej., 15 %). |
| **GPU no disponible** | Cambia `EngineMode.GPU` a `EngineMode.CPU`; el resto del pipeline permanece sin cambios. |
| **Se pierden tablas** | Prueba un escaneo de mayor resolución o habilita `set_table_detection(True)` si la biblioteca lo proporciona. |

## Próximos pasos: De texto plano a datos estructurados

Ahora que sabes **how to deskew image**, **how to boost contrast**, y **how to get plain text**, podrías querer:

- Analizar el texto plano con expresiones regulares para extraer pares clave‑valor (p.ej., `total`, `date`).
- Almacenar los resultados en una base de datos SQLite o PostgreSQL para reportes posteriores.
- Conectar el script a una función serverless (AWS Lambda, Azure Functions) para procesar cargas automáticamente.

Todas esas extensiones se basan en la misma base que cubrimos aquí.

## Conclusión

Hemos recorrido **how to deskew image** usando un motor OCR acelerado por GPU, demostrado **how to boost contrast** para un reconocimiento más nítido, mostrado exactamente **how to get plain text**, e incluso cubierto **how to extract text** de tablas. El script completo y ejecutable une todo, para que puedas incorporarlo en cualquier proyecto Python y comenzar a extraer datos limpios de fotos inclinadas y de bajo contraste de inmediato.

Pruébalo con algunos de tus propios recibos, ajusta el nivel de contraste y deja que el OCR haga el trabajo pesado. Si encuentras peculiaridades, revisa la tabla de casos límite anterior—la mayoría de los problemas se resuelven con un pequeño ajuste.

¡Feliz codificación, y que tus imágenes siempre estén rectas y brillantes!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}