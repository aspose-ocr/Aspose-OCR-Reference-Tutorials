---
category: general
date: 2026-04-26
description: Cómo procesar OCR por lotes tus documentos y extraer texto de escaneos
  en Python. Aprende el procesamiento por lotes paso a paso con OcrEngine para obtener
  salida JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: es
og_description: Cómo hacer OCR por lotes de tus archivos escaneados y extraer texto
  de los escaneos en un solo script. Código completo, consejos y manejo de casos límite.
og_title: Cómo hacer OCR por lotes – Guía rápida de Python
tags:
- OCR
- Python
- Automation
title: Cómo hacer OCR por lotes – Extraer texto de escaneos de manera eficiente
url: /es/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo hacer OCR por lotes – Extraer texto de escaneos de forma eficiente

¿Alguna vez te has preguntado **cómo hacer OCR por lotes** a una montaña de PDFs escaneados sin perder la cordura? No eres el único—los desarrolladores preguntan constantemente, *“¿Cómo puedo extraer texto de escaneos de una sola vez?”* La buena noticia es que unas pocas líneas de Python pueden convertir esa tarea tediosa en una canalización automatizada y fluida.

En este tutorial recorreremos una solución completa, lista‑para‑ejecutar que **extrae texto de escaneos**, guarda los resultados como JSON y te brinda una rápida verificación al final. Sin servicios externos, sin magia—solo Python puro, la clase `OcrEngine` y un poco de manejo de carpetas.

## Qué obtendrás al final

- Un script completamente funcional que **realiza OCR por lotes** sobre cualquier carpeta de imágenes.  
- Explicaciones claras de *por qué* existe cada línea, no solo de *qué* hace.  
- Consejos para manejar carpetas vacías, archivos que no son imágenes y lotes grandes.  
- Una forma de verificar que la salida JSON realmente contiene el texto extraído.  

### Prerrequisitos (lo mínimo indispensable)

| Requisito | Por qué es importante |
|-----------|-----------------------|
| Python 3.8+ | Sintaxis moderna y anotaciones de tipo |
| `OcrEngine` library (or a compatible wrapper) | Biblioteca `OcrEngine` (o un wrapper compatible) |
| A directory with scanned image files (PNG, JPG, TIFF) | Un directorio con archivos de imágenes escaneadas (PNG, JPG, TIFF) |
| Write permissions for the output folder | Permisos de escritura para la carpeta de salida |

Si ya tienes esto, genial—¡vamos al grano!

![how to batch OCR workflow](image-placeholder.png){alt="how to batch OCR workflow"}

## Paso 1 – Inicializar el motor OCR (cómo hacer OCR por lotes)

Antes de poder procesar cualquier cosa, necesitamos una instancia del motor OCR. Piensa en ella como el “cerebro” que leerá cada imagen y producirá texto. Inicializarla una sola vez y reutilizarla a lo largo de todo el lote es el patrón más eficiente.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **¿Por qué reutilizar la misma instancia?**  
> Crear un nuevo motor para cada archivo cargaría repetidamente modelos pesados en memoria, ralentizando drásticamente el lote. Una única instancia mantiene el modelo en RAM y te permite procesar miles de imágenes sin una desaceleración notable.

## Paso 2 – Apuntar a la carpeta de escaneos (extraer texto de escaneos)

Tus escaneos están en algún lugar del disco. Indiquemos al script dónde encontrarlos. Usar rutas absolutas evita sorpresas de “archivo no encontrado” cuando el script se ejecuta desde un directorio de trabajo diferente.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Consejo profesional:**  
> Si estás en Windows, las barras diagonales (`/`) funcionan perfectamente con `os.path.abspath`, así que no tienes que escapar las barras invertidas.

## Paso 3 – Elegir dónde deben ir los resultados JSON

Probablemente quieras una carpeta ordenada para los resultados OCR. Mantener la salida separada de la fuente facilita la limpieza posterior o alimentar el JSON a otra canalización.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **¿Por qué crear la carpeta programáticamente?**  
> Garantiza que el script no se bloquee si el directorio falta, y `exist_ok=True` hace que la operación sea idempotente—ejecuta el script varias veces sin errores.

## Paso 4 – Ejecutar el proceso por lotes (cómo hacer OCR por lotes)

Ahora lo esencial: indicarle a `ocr_engine` que recorra cada archivo en `input_dir`, ejecute OCR y volque JSON en `output_dir`. La bandera `format="json"` le dice al motor que serialice el resultado de forma estructurada, lo que encantará a las herramientas posteriores.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### ¿Qué está sucediendo bajo el capó?

1. **Descubrimiento de archivos** – El motor escanea `input_folder` de forma recursiva, ignorando archivos ocultos.  
2. **Validación de archivos** – Solo se envían al modelo OCR las extensiones de imagen soportadas (`.png`, `.jpg`, `.tif`, etc.).  
3. **Ejecución de OCR** – Cada imagen se envía al motor OCR; se capturan texto, puntuaciones de confianza y datos de diseño.  
4. **Serialización a JSON** – El resultado se escribe en un archivo con el mismo nombre base pero con extensión `.json` en `output_folder`.  

> **Manejo de casos límite:**  
> - **Carpeta vacía:** El motor registra “No files found” y retorna sin problemas.  
> - **Imagen corrupta:** Omite el archivo, registra una entrada de error en `batch_errors.log` y continúa.  
> - **Lote enorme (más de 10k archivos):** El uso de memoria se mantiene bajo porque cada imagen se procesa de forma independiente.

## Paso 5 – Confirmar que la conversión finalizó

Una simple instrucción `print` brinda retroalimentación inmediata en la consola. Para canalizaciones de producción podrías reemplazarla por una llamada a un logger o una notificación por correo.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Cuando veas esa línea, puedes inspeccionar con seguridad la carpeta `json_output`. Cada archivo JSON tendrá una estructura similar a esta:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Ahora puedes alimentar estos archivos JSON a una base de datos, un índice de búsqueda o cualquier herramienta de análisis posterior.

## Preguntas frecuentes (y respuestas rápidas)

**P: ¿Qué pasa si necesito procesar PDFs en lugar de imágenes?**  
**R:** Convierte cada página del PDF a una imagen primero (p. ej., usando `pdf2image`) y coloca los archivos PNG/JPG resultantes en `input_dir`. La lógica de OCR por lotes permanece sin cambios.

**P: ¿Puedo cambiar el formato de salida a texto plano?**  
**R:** Por supuesto. Reemplaza `format="json"` por `format="txt"` y el motor escribirá un archivo `.txt` que contiene solo el texto extraído.

**P: Mis escaneos están en múltiples subcarpetas—¿el script recursará?**  
**R:** Sí. `batch_process` recorre el árbol de directorios por defecto. Si deseas una salida plana, establece `flatten=True` (si la biblioteca lo soporta) o procesa los nombres de archivo JSON después.

**P: ¿Cómo manejo scripts no latinos?**  
**R:** Inicializa `OcrEngine` con un parámetro de idioma, por ejemplo, `OcrEngine(lang="spa+eng")`. El bucle por lotes en sí no necesita cambios.

## Consejos profesionales y errores comunes

- **El tamaño del lote importa:** Si notas picos de CPU, regula el proceso con un simple `time.sleep(0.1)` entre archivos.  
- **Registro:** Cambia la llamada `print` por el módulo `logging` de Python para capturar marcas de tiempo y niveles de error.  
- **Colisiones de nombres de archivo:** Si dos escaneos comparten el mismo nombre base pero están en diferentes subcarpetas, los archivos JSON se sobrescribirán. Añade un hash de la ruta relativa al nombre de salida para evitarlo.  
- **Fugas de memoria:** Algunos back‑ends de OCR retienen recursos nativos. Llama a `ocr_engine.close()` al final de tu script si la biblioteca ofrece un método de limpieza.

## Script completo – Listo para copiar y pegar

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Salida esperada en consola**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Puedes verificar el JSON abriendo cualquier archivo en `json_output` con un editor de texto o cargándolo en Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Deberías ver el texto extraído por OCR impreso en la consola.

## Conclusión

Acabamos de cubrir **cómo hacer OCR por lotes** en todo un directorio de imágenes escaneadas y **extraer texto de escaneos** en archivos JSON limpios y legibles por máquinas. El enfoque es deliberadamente simple: configurar el motor una vez, apuntarlo a una carpeta y dejar que la biblioteca haga el trabajo pesado. Desde aquí puedes:

- Conectar el JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}