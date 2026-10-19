---
category: general
date: 2026-05-31
description: Aprende a usar la región de interés de OCR para cargar una imagen y extraer
  texto de un rectángulo, ideal para reconocer el monto en una factura.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: es
og_description: Domina la región de interés OCR para cargar la imagen, extraer texto
  del rectángulo y reconocer el texto de una factura en un único tutorial.
og_title: OCR Región de Interés – Guía paso a paso en Python
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR de Región de Interés – Extraer texto de un rectángulo en Python
url: /es/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Región de Interés OCR – Extraer Texto de un Rectángulo en Python

¿Alguna vez te has preguntado cómo **ocr region of interest** una parte específica de una factura escaneada sin alimentar toda la página al motor? No eres el primero que mira un recibo borroso y piensa: “¿Cómo extraigo el importe que está en alguna parte de la esquina inferior derecha?” La buena noticia es que puedes indicarle a la biblioteca OCR exactamente dónde buscar, lo que aumenta drásticamente la velocidad y la precisión.

En esta guía recorreremos un ejemplo completo y ejecutable que muestra cómo **load image for OCR**, definir una **region of interest**, y luego **extract text from rectangle** para finalmente **recognize text from invoice** y responder la clásica pregunta “cómo extraer el importe”. Sin referencias vagas—solo código concreto, explicaciones claras y algunos consejos profesionales que desearías haber sabido antes.

---

## Qué Construirás

Al final de este tutorial tendrás un pequeño script en Python que:

1. Carga una imagen de factura desde el disco.  
2. Marca una ROI rectangular donde se encuentra el importe total.  
3. Ejecuta OCR solo dentro de esa ROI.  
4. Imprime la cadena del importe limpiada.  

Todo esto funciona con cualquier biblioteca OCR que soporte ROI—aquí usaremos un paquete ficticio pero representativo `SimpleOCR` que imita herramientas populares como Tesseract o EasyOCR. Si lo deseas, puedes cambiarlo; los conceptos siguen siendo los mismos.

---

## Requisitos Previos

- Python 3.8+ instalado (`python --version` debe mostrar ≥3.8).  
- Un paquete OCR instalable con pip (p. ej., `pip install simpleocr`).  
- Una imagen de factura (PNG o JPEG) colocada en una carpeta a la que puedas referenciar.  
- Familiaridad básica con funciones y clases de Python (nada sofisticado).

Si ya tienes todo eso, genial—¡vamos al grano! Si no, consigue la imagen primero; el resto de los pasos es independiente del contenido real del archivo.

---

## Paso 1: Load Image for OCR

Lo primero que necesita cualquier flujo de trabajo OCR es un mapa de bits del que leer. La mayoría de las bibliotecas exponen un método simple `load_image` que acepta una ruta de archivo. Así es como lo haces con nuestro motor `SimpleOCR`:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Usa rutas absolutas o `os.path.join` para evitar sorpresas de “archivo no encontrado” al ejecutar el script desde un directorio de trabajo diferente.

---

## Paso 2: Define OCR Region of Interest

En lugar de dejar que el motor escanee toda la página, le decimos *exactamente* dónde se encuentra el importe. Este es el paso **ocr region of interest**, y es la clave para una extracción fiable, especialmente cuando el documento contiene encabezados o pies de página ruidosos.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

¿Por qué esos números? `x` e `y` son desplazamientos en píxeles desde la esquina superior izquierda, mientras que `width` y `height` describen el tamaño del cuadro. Si no estás seguro, abre la imagen en cualquier editor, habilita una regla y anota las coordenadas. Muchos IDE incluso permiten imprimir la posición del cursor al pasar el ratón.

---

## Paso 3: Extract Text from Rectangle

Ahora que la ROI está definida, le pedimos al motor **recognize text from invoice** pero limitado al rectángulo que acabamos de añadir. La llamada devuelve un objeto de resultado que típicamente contiene la cadena cruda, puntuaciones de confianza y, a veces, cajas delimitadoras.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Detrás de escena, `recognize()` itera sobre cada ROI, recorta esa porción, ejecuta el modelo OCR y une los resultados. Por eso definir una región **extract text from rectangle** ajustada puede ahorrar segundos en el tiempo de procesamiento para trabajos por lotes.

---

## Paso 4: How to Extract Amount – Clean the Output

OCR no es perfecto; a menudo obtendrás espacios extra, saltos de línea o incluso caracteres mal leídos (p. ej., “S” vs “5”). Un rápido `strip()` y una pequeña expresión regular suelen ser suficientes para valores monetarios.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Por qué importa:** Si planeas enviar el importe a una base de datos o a una pasarela de pagos, necesitas un formato predecible. Eliminar espacios en blanco y filtrar caracteres no numéricos previene errores posteriores.

---

## Paso 5: Recognize Text from Invoice – Script Completo

Juntándolo todo, aquí tienes el script completo, listo para ejecutar. Guárdalo como `extract_amount.py` y ejecuta `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Salida Esperada

```
Amount: 1,245.67
```

Si la ROI está desalineada, podrías ver algo como `Amount: 1245.6S`—nota la “S” extra. Ajusta las coordenadas del rectángulo y vuelve a ejecutar hasta que la salida se vea limpia.

---

## Problemas Comunes & Casos Límite

| Problema | Por Qué Ocurre | Solución |
|----------|----------------|----------|
| **ROI demasiado pequeña** | El texto del importe se corta, lo que lleva a un reconocimiento parcial. | Amplía `width`/`height` en ~10‑20 % y vuelve a probar. |
| **DPI incorrecto** | Escaneos de baja resolución (≤150 dpi) reducen la precisión del OCR. | Remuestrea la imagen a 300 dpi antes de cargarla, o solicita al escáner una DPI mayor. |
| **Múltiples monedas** | La regex captura el primer grupo numérico, que podría ser el número de factura. | Refina la regex para buscar símbolos de moneda (`$`, `€`, `£`) antes de los dígitos. |
| **Facturas rotadas** | Los motores OCR asumen texto vertical; las páginas rotadas rompen el reconocimiento. | Aplica una corrección de rotación (`ocr_engine.rotate(90)`) antes de añadir la ROI. |
| **Ruido de fondo** | Sombras o sellos confunden al modelo. | Pre‑procesa con un umbral simple (`cv2.threshold`) o usa un filtro de reducción de ruido. |

Abordar estos casos límite temprano te ahorrará horas de depuración más adelante.

---

## Consejos Profesionales para Proyectos Reales

- **Procesamiento por Lotes:** Recorre una carpeta de facturas, calcula la ROI dinámicamente (p. ej., basándote en detección de plantillas) y guarda los resultados en CSV.  
- **Coincidencia de Plantillas:** Si manejas varios diseños de factura, mantén un mapa JSON de `template_id → coordenadas ROI`. Cambia la ROI según un clasificador rápido de diseño.  
- **Ejecución Paralela:** Usa `concurrent.futures.ThreadPoolExecutor` para ejecutar múltiples instancias OCR concurrentemente—ideal para pipelines de back‑office de alto volumen.  
- **Filtrado por Confianza:** La mayoría de los resultados OCR incluyen una puntuación de confianza. Descarta resultados por debajo de un umbral (p. ej., 85 %) y márcalos para revisión manual.

---

## Conclusión

Hemos cubierto todo lo que necesitas para **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, y finalmente **recognize text from invoice** para responder la clásica pregunta **how to extract amount**. El script es compacto, pero lo suficientemente flexible como para adaptarse a diferentes formatos de documentos, idiomas y back‑ends OCR.

Ahora que dominas lo básico, considera ampliar el flujo de trabajo: añadir escaneo de códigos de barras, integrar con un parser de PDF, o enviar el importe extraído a una API contable. El cielo es el límite, y con una ROI bien definida siempre obtendrás resultados más rápidos y limpios.

Si encuentras algún problema, deja un comentario abajo—¡feliz OCR!

![ejemplo de región de interés OCR](https://example.com/ocr_roi_example.png "ejemplo de región de interés OCR")


## ¿Qué Deberías Aprender Después?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}