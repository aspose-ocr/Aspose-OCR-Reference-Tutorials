---
category: general
date: 2026-06-16
description: Define la región de interés en OCR para extraer texto en español de tarjetas
  de identificación. Aprende cómo cargar la imagen para OCR y especificar la ROI de
  manera eficiente.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: es
og_description: Define la región de interés en OCR para extraer texto en español de
  tarjetas de identificación. Guía paso a paso sobre cómo cargar imágenes y especificar
  la ROI.
og_title: Definir región de interés en OCR – Tutorial completo de Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Definir región de interés en OCR – Tutorial completo de Python
url: /es/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir región de interés en OCR – Tutorial completo de Python

¿Alguna vez te has preguntado cómo **definir región de interés en OCR** para leer solo la parte de una imagen que realmente necesitas? En este tutorial te guiaremos paso a paso, además de mostrarte cómo **cargar imagen para OCR** y extraer texto en español de una tarjeta de identificación con solo unas pocas líneas de Python.  

Si alguna vez has mirado un escaneo ruidoso y pensado, “Debe haber una forma más limpia de obtener el campo del nombre”, estás en el lugar correcto. Al final podrás extraer el texto de la tarjeta de identificación que te interesa sin tropezar con el desorden de fondo.

## Lo que aprenderás

- Por qué deberías **definir región de interés** antes de ejecutar OCR.  
- Los pasos exactos para **cargar imagen para OCR** usando un popular wrapper de OCR en Python.  
- Cómo **especificar ROI** con coordenadas de píxeles.  
- Formas de **extraer texto de tarjeta de identificación** de manera fiable, incluso cuando el idioma de origen es español.  
- Consejos para manejar casos extremos como tarjetas rotadas o escaneos de bajo contraste.  

No se requiere dominio previo de OCR, solo un entorno Python 3 funcional y un JPEG de una tarjeta de identificación que quieras probar.

---

![Define region of interest illustration](placeholder.png){alt="Ejemplo de definición de región de interés que muestra un rectángulo resaltado en una imagen de tarjeta de identificación"}

## Paso 1: Instalar e Importar la Biblioteca OCR

Lo primero es que necesitas una biblioteca que exponga una clase `OcrEngine` similar al fragmento que viste. Para esta guía usaremos el paquete ficticio `ocr`, pero los mismos conceptos se aplican a `pytesseract`, `easyocr`, o cualquier wrapper que permita establecer un idioma y una ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Consejo profesional:* Si estás usando `pytesseract`, la clase `Rectangle` se convierte en una simple tupla `(left, top, width, height)`. El resto del flujo permanece idéntico.

## Paso 2: Cargar Imagen para OCR

Ahora **cargamos imagen para OCR**. El motor espera un objeto `ocr.Image`, así que lo apuntamos al archivo que contiene la tarjeta de identificación. Asegúrate de que la ruta sea absoluta o relativa al directorio de trabajo de tu script.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Si la imagen es muy grande, considera redimensionarla primero; los motores OCR funcionan más rápido con imágenes de menos de 1500 px de ancho.

## Paso 3: Cómo Especificar ROI (Definir Región de Interés)

Aquí está el corazón del tutorial: **cómo especificar ROI**. Una región de interés es simplemente un rectángulo que le indica al motor OCR, “Solo mira dentro de estos límites de píxeles”. Piensa en ello como dibujar un cuadro alrededor del campo de nombre en una tarjeta de identificación.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

¿Por qué esos números? En nuestra imagen de ejemplo, el nombre está aproximadamente a 120 px del borde izquierdo y 80 px del borde superior. Ajústalos para que coincidan con el diseño de las tarjetas que estás procesando.  

*Caso extremo:* Si la tarjeta está rotada 90°, intercambia `width` y `height` y ajusta `left`/`top` en consecuencia, o pre‑rota la imagen con Pillow antes de pasarla al motor.

## Paso 4: Realizar OCR Dentro del ROI

Con el ROI definido, el motor ignorará todo lo que esté fuera del rectángulo. Esto no solo acelera el procesamiento sino que también reduce falsos positivos causados por gráficos de fondo.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

La llamada `recognize()` devuelve un objeto que contiene el texto reconocido, puntuaciones de confianza y cajas delimitadoras para cada palabra.

## Paso 5: Extraer Texto de la Tarjeta de Identificación (y Verificar Salida en Español)

Finalmente, **extraemos texto de la tarjeta de identificación** del resultado del ROI y lo imprimimos. Como establecimos el idioma a español antes, el motor OCR aplicará diccionarios específicos del idioma, mejorando la precisión para caracteres acentuados como “ñ” o “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Salida Esperada

```
ROI text: JUAN PÉREZ GARCÍA
```

Si ves caracteres distorsionados, verifica que la imagen esté realmente en español y que los archivos de datos de idioma de la biblioteca OCR estén instalados.

## Errores Comunes y Cómo Evitarlos

| Síntoma | Causa Probable | Solución |
|---------|----------------|----------|
| Cadena vacía devuelta | ROI no intersecta ningún texto | Verifica las coordenadas con un visor de imágenes; usa `engine.debug_draw_roi()` si está disponible. |
| Muchos caracteres basura | Paquete de idioma incorrecto | Reinstala los datos de idioma español o cambia a `ocr.Language.AUTO`. |
| Puntuaciones de confianza bajas | La imagen está borrosa o con bajo contraste | Preprocesa con OpenCV – aplica `cv2.GaussianBlur` y `cv2.threshold`. |
| OCR se ejecuta en toda la imagen a pesar del ROI | Uso de una versión antigua de la biblioteca | Actualiza al último paquete `ocr`; versiones anteriores ignoraban el ROI. |

## Extender el Ejemplo: Múltiples ROIs

A veces necesitas extraer más de un campo (p.ej., nombre y número de identificación). El patrón sigue siendo el mismo: cambia `engine.region_of_interest` y llama a `recognize()` nuevamente.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

También puedes procesar por lotes una lista de rectángulos si la biblioteca lo permite, lo que ahorra una ida y vuelta al motor OCR.

## Script Completo Funcional

Juntando todo, aquí tienes un script listo para ejecutar que **define región de interés**, **carga imagen para OCR**, y **extrae texto en español** de una tarjeta de identificación.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Ejecuta el script y deberías ver el nombre impreso en la consola. Cambia los valores del rectángulo para apuntar a otros campos, y tendrás una utilidad reutilizable para cualquier documento tipo tarjeta de identificación.

## Próximos Pasos

- **Procesamiento por lotes:** Recorrer una carpeta de tarjetas de identificación y guardar cada nombre extraído en un archivo CSV.  
- **Detección de idioma:** Permitir que el usuario elija el idioma dinámicamente; `ocr.Language.AUTO` puede ser útil.  
- **Post‑procesamiento:** Aplicar patrones regex para limpiar errores comunes de OCR (p.ej., reemplazar “0” por “O” cuando aparece en nombres).  

Al dominar cómo **definir región de interés** has desbloqueado una forma poderosa de **extraer texto de tarjetas de identificación** de manera rápida y precisa, especialmente al trabajar con documentos en español.

---

### TL;DR

Te mostramos cómo **definir región de interés en OCR**, **cargar imagen para OCR**, y **cómo especificar ROI** para **extraer texto en español** de una tarjeta de identificación. El ejemplo completo se ejecuta en menos de un minuto y puede adaptarse a cualquier diseño con algunos ajustes de coordenadas. Pruébalo, modifica el rectángulo y observa cómo el OCR se enfoca como un láser.

¡Feliz codificación!

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo extraer texto de una imagen preparando rectángulos en OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extraer texto de imagen C# con selección de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extraer texto de imagen – Optimización OCR con Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}