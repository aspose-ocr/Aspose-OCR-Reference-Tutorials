---
category: general
date: 2026-01-12
description: Ejecute OCR en archivos PNG rápidamente con Python. Aprenda cómo extraer
  texto de imágenes y facturas, y cargar la imagen para OCR usando Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: es
og_description: Ejecute OCR en PNG al instante. Esta guía muestra cómo extraer texto
  de una imagen y una factura, cargar la imagen para OCR y guardar los resultados
  como JSON y CSV.
og_title: Ejecutar OCR en PNG – Tutorial completo de Python
tags:
- OCR
- Python
- Image Processing
title: Ejecuta OCR en PNG – Guía completa de Python para extraer texto de imágenes
url: /es/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ejecutar OCR en PNG – Guía completa de Python para extraer texto de imágenes

¿Alguna vez necesitaste **run OCR on PNG** archivos pero no estabas seguro de qué biblioteca te daría resultados limpios y estructurados? No estás solo. En muchos proyectos del mundo real—piensa en automatización de facturas o escaneo de recibos—el primer paso es **extract text from image** archivos, y PNG es un formato común porque preserva calidad sin pérdida.

En este tutorial recorreremos un ejemplo práctico usando el paquete Aspose.OCR para Python. Al final de la guía sabrás cómo **load image for OCR**, extraer cada línea de texto, convertir esos datos en un objeto JSON ordenado e incluso volcarlo a CSV para procesamiento posterior. Sin rodeos, solo una solución práctica y lista para ejecutar.

## Lo que aprenderás

- Cómo instalar e importar la biblioteca Aspose.OCR.  
- Los pasos exactos para **run OCR on PNG** y manejar el objeto de resultado.  
- Formas de **extract text from invoice** archivos y formatear la salida como JSON o CSV.  
- Consejos para tratar imágenes de bajo contraste, documentos multilingües y puntuaciones de confianza.  
- Un ejemplo completo de código copiar‑y‑pegar que puedes ejecutar hoy.

> **Prerequisito:** Python 3.8+ y una familiaridad básica con pip. Si nunca has usado Aspose antes, no te preocupes—esta guía cubre todo lo que necesitas para comenzar.

---

## Paso 1 – Instalar Aspose.OCR y preparar tu entorno

Antes de que podamos **run OCR on PNG**, la biblioteca debe estar presente en tu sistema.

```bash
pip install aspose-ocr
```

> **Consejo profesional:** Usa un entorno virtual (`python -m venv venv`) para mantener las dependencias aisladas. Previene conflictos de versiones si manejas varios proyectos.

Una vez instalado, importa los módulos que necesitaremos:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Aquí importamos `asposeocr` para el trabajo pesado y la biblioteca incorporada `json` para la serialización posterior.

## Paso 2 – Crear el motor OCR y establecer el idioma

El motor OCR es el componente central que realmente lee los píxeles. Para la mayoría de facturas en inglés, querrás el paquete de idioma inglés:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Por qué es importante:** Especificar el idioma reduce el conjunto de caracteres, lo que aumenta la precisión y acelera el procesamiento. Si alguna vez necesitas manejar facturas multilingües, simplemente cambia `ocr.Language.ENGLISH` por el enum correspondiente.

## Paso 3 – Cargar la imagen para OCR

Ahora **load image for OCR**. El método `Image.load` acepta una ruta de archivo y funciona con PNG, JPEG, BMP y más.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Caso límite:** Si el PNG es inusualmente grande (más de 5 MB), considera redimensionarlo primero para mantener un uso de memoria razonable. Pillow puede hacerlo en una sola línea:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## Paso 4 – Ejecutar OCR en PNG y capturar el resultado

Con el motor listo y la imagen cargada, es hora de **run OCR on PNG** y obtener el resultado estructurado.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

El objeto `ocr_result` contiene una colección de elementos `OcrRegion`, cada uno con el texto reconocido y una puntuación de confianza (0‑100). Aquí obtienes los datos granulares necesarios para **extract text from invoice** líneas.

## Paso 5 – Convertir el resultado a JSON y formatearlo

La mayoría de los sistemas posteriores aman JSON, así que convertiremos la salida OCR en una cadena bien formateada.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Salida de ejemplo

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Observa cómo cada línea incluye una métrica de confianza—perfecta para filtrar entradas de baja confianza si planeas **extract text from invoice** automáticamente.

## Paso 6 – Guardar los datos OCR como CSV (Una línea por texto + confianza)

CSV es ideal para hojas de cálculo o importaciones rápidas de datos. Aspose ofrece una línea de código para volcar todo en un archivo CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

El CSV generado se verá así:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Ahora puedes abrirlo en Excel, Google Sheets o ingresarlo a una base de datos.

## Bonus – Manejo de texto de baja confianza y PDFs de varias páginas

### Filtrado por confianza

Si solo deseas líneas de alta certeza, filtra el JSON antes de escribirlo:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Documentos multipágina

Aspose.OCR crea automáticamente una nueva entrada `page` para cada página en un PNG o PDF de varias páginas. Recorre `ocr_data["pages"]` para procesarlas todas—no se necesita código extra.

## Ejemplo completo en funcionamiento

A continuación está el **complete script** que puedes copiar, pegar y ejecutar inmediatamente. Reemplaza `YOUR_DIRECTORY` con la carpeta que contiene tu archivo PNG.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Ejecuta el script con `python run_ocr.py` y verás el volcado JSON en la consola, un archivo CSV en disco y una lista filtrada de entradas de alta confianza.

## Preguntas frecuentes

**Q: ¿Puedo usar esto para extraer texto de un recibo escaneado en lugar de una factura?**  
A: Por supuesto. El mismo flujo de trabajo se aplica—simplemente apunta `image_path` a tu PNG de recibo. Si el recibo usa un idioma diferente, cambia `engine.language` en consecuencia.

**Q: ¿Qué pasa si mi PNG contiene texto rotado?**  
A: Aspose.OCR detecta automáticamente la orientación, pero para casos rebeldes puedes rotar manualmente la imagen con Pillow antes de pasarla al motor.

**Q: ¿Necesito una licencia paga para Aspose.OCR?**  
A: La biblioteca ofrece un modo de evaluación gratuito con una marca de agua en la salida. Para uso en producción necesitarás una licencia, que puedes obtener en el sitio web de Aspose.

## Conclusión

Hemos cubierto todo lo que necesitas para **run OCR on PNG** archivos usando Python: instalar el SDK, cargar la imagen, extraer texto estructurado y guardar el resultado como JSON o CSV. Ya sea que busques **extract text from image** para un script sencillo o **extract text from invoice** para una canalización contable automatizada, los pasos anteriores te brindan una base sólida y lista para producción.

Próximamente, podrías explorar:

- Integrar la salida CSV con una base de datos para almacenamiento masivo de facturas.  
- Añadir post‑procesamiento con expresiones regulares para extraer fechas, montos o IDs fiscales.  
- Usar la función `ocr_engine.recognize_barcode` si tus facturas incluyen códigos QR.

Prueba, ajusta los umbrales de confianza y observa cómo tu flujo de procesamiento de documentos se vuelve una brisa. ¿Tienes más preguntas o un caso de uso interesante para compartir? Deja un comentario abajo—¡feliz OCR!

![ejemplo de run OCR en PNG](run-ocr-on-png.png "run OCR on PNG – ejemplo visual del resultado OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}