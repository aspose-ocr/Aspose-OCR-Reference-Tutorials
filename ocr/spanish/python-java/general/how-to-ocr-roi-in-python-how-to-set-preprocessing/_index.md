---
category: general
date: 2026-03-28
description: Cómo hacer OCR de ROI en Python – Aprende a configurar opciones de preprocesamiento
  para una extracción de texto precisa de regiones específicas de la imagen.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: es
og_description: Cómo hacer OCR de ROI en Python – Esta guía muestra cómo configurar
  el preprocesamiento para una extracción de texto fiable de regiones de imagen definidas.
og_title: Cómo hacer OCR de ROI en Python – Cómo configurar el preprocesamiento
tags:
- OCR
- Python
- Aspose
title: Cómo hacer OCR de ROI en Python – Cómo establecer el preprocesamiento
url: /es/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo hacer OCR de ROI en Python – Cómo configurar el preprocesamiento

¿Alguna vez te has preguntado **cómo hacer OCR de ROI** en una imagen de factura ruidosa sin cargar toda la página en memoria? No eres el único. En muchos proyectos del mundo real solo necesitamos un puñado de campos—nombre del cliente, dirección, totales—por lo que escanear el documento completo es excesivo.  

¿La buena noticia? Con Aspose OCR puedes indicarle al motor exactamente **dónde buscar** e incluso decirle que limpie la imagen primero. En este tutorial recorreremos **cómo configurar el preprocesamiento**, definir Regiones de Interés (ROIs) y extraer texto limpio en solo unas pocas líneas de Python.

Al final de esta guía tendrás un script listo‑para‑ejecutar que extrae bloques específicos de cualquier factura, recibo o formulario. No se requieren herramientas adicionales, solo Aspose OCR y un poco de lógica en Python.

---

## Lo que necesitarás

- **Python 3.8+** (el código funciona en cualquier versión reciente)  
- **Aspose OCR for Python via .NET** – instálalo con `pip install aspose-ocr`  
- Una imagen de ejemplo (p. ej., `invoice.png`) colocada en una carpeta a la que puedas referenciar  
- Familiaridad básica con funciones de Python y sintaxis orientada a objetos  

Si ya tienes esto, genial—¡pasemos directamente al código.

![Diagrama de cómo hacer OCR de ROI](ocr-roi.png "Ejemplo de cómo hacer OCR de ROI")

*Texto alternativo: diagrama de cómo hacer OCR de ROI mostrando cajas de ROI en una imagen de factura*

## Paso 1 – Inicializar el motor OCR (Cómo hacer OCR de ROI)

Antes de poder indicarle al motor *dónde* buscar, necesitamos una instancia del procesador OCR. Este objeto contiene toda la configuración y ejecuta la pasada de reconocimiento.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Por qué es importante*: La clase `OcrEngine` abstrae el trabajo pesado (detección de fuentes, análisis de diseño, etc.). Al crear un solo motor evitas volver a inicializar recursos intensivos para cada imagen, lo que mantiene el rendimiento ágil.

## Paso 2 – Cargar tu imagen fuente (Cómo hacer OCR de ROI)

Aspose Storage hace que la carga de imágenes sea sencilla. Apúntalo a la ruta del archivo y obtendrás un objeto `Image` listo para procesar.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Consejo*: Si trabajas con flujos (p. ej., imágenes subidas mediante una API web), puedes pasar un objeto `BytesIO` a `Image.load` en lugar de una ruta de archivo.

## Paso 3 – Definir las Regiones de Interés (ROIs)

Ahora respondemos la pregunta central **cómo hacer OCR de ROI**: le indicamos al motor los rectángulos exactos que contienen los datos que nos interesan. Cada ROI se define por su esquina superior izquierda (`x`, `y`) y su tamaño (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*¿Por qué usar ROIs?*  
- **Velocidad** – El motor omite partes irrelevantes de la imagen.  
- **Precisión** – Al enfocarse en un área pequeña, el ruido en otras partes no puede confundir al reconocedor.  
- **Flexibilidad** – Puedes añadir tantas ROIs como necesites; el motor devuelve una lista de resultados en el mismo orden.

## Paso 4 – Cómo configurar el preprocesamiento para una mejor precisión OCR

Las imágenes directamente de escáneres o teléfonos a menudo presentan sesgo, bajo contraste o iluminación desigual. Aspose OCR ofrece un objeto `PreprocessingOptions` que permite habilitar correcciones comunes antes de que se ejecute el reconocimiento.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Cómo ayuda esto*:  
- **Deskew** elimina la inclinación que hace que las formas de los caracteres sean ambiguas.  
- **Binarize** reduce el ruido de color, proporcionando al motor OCR una imagen binaria limpia.  
- **Contrast** amplifica los trazos débiles, lo que es especialmente útil para recibos descoloridos.

Puedes experimentar con estas banderas—desactiva una y observa si la salida cambia. Ese es el espíritu de **cómo configurar el preprocesamiento** de manera eficaz.

## Paso 5 – Realizar OCR solo dentro de las ROIs definidas

Con el motor, la imagen, las ROIs y el preprocesamiento listos, es hora de llamar a `recognize`. El método devuelve un objeto `OcrResult` que contiene una colección `regions`—cada entrada coincide con el orden de ROI que suministramos.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Detrás de escena*: El motor recorta cada ROI, aplica la cadena de preprocesamiento y ejecuta el modelo de reconocimiento sobre el fragmento limpiado. Como pasamos una lista, el resultado mantiene el mismo orden, lo que hace que el post‑procesamiento sea sencillo.

## Paso 6 – Leer y usar el texto extraído (Cómo hacer OCR de ROI)

Finalmente, itera sobre la lista `regions` y muestra—o guarda—las cadenas reconocidas. El objeto `Region` expone una propiedad `text` que contiene el resultado Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Salida esperada (ejemplo)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Si el texto se ve distorsionado, revisa **cómo configurar el preprocesamiento**: tal vez aumenta `contrast` o desactiva `binarize` para logotipos coloreados.

## Errores comunes y consejos profesionales

| Problema | Por qué ocurre | Solución (Cómo configurar el preprocesamiento) |
|----------|----------------|-----------------------------------------------|
| El texto inclinado aparece como garabatos | `deskew` deshabilitado o imagen demasiado rotada | Activar `preprocessing_options.deskew = True` |
| Los números se convierten en puntos o marcas errantes | Bajo contraste o binarización agresiva | Reducir `contrast` (p. ej., `1.2`) o establecer `binarize = False` |
| Las coordenadas de ROI están desfasadas unos píxeles | DPI diferente o escala del escáner | Usa una herramienta (p. ej., Paint.NET) para medir posiciones exactas de píxeles, o agrega un pequeño margen (`+5` píxeles) a cada ROI |
| Resultado vacío para una región | ROI fuera de los límites de la imagen | Verifica las dimensiones de la imagen: `source_image.width`, `source_image.height` |

## Extender la solución (Cómo hacer OCR de ROI en diferentes escenarios)

- **ROIs dinámicas**: Si tus facturas tienen diseños variables, puedes primero ejecutar un OCR rápido de página completa para localizar palabras clave (“Customer:”, “Address:”) y luego calcular las ROIs al vuelo.  
- **Procesamiento por lotes**: Encapsula los pasos anteriores en una función y recorre una carpeta de imágenes. Recuerda reutilizar la misma instancia `ocr_engine` para mantener bajo el uso de memoria.  
- **Exportar a JSON**: En lugar de imprimir, construye un diccionario y viértelo con `json.dumps`; esto hace que la integración posterior (p. ej., alimentar a un sistema ERP) sea trivial.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

## Conclusión

Ahora tienes un ejemplo completo y ejecutable que muestra **cómo hacer OCR de ROI** en Python mientras dominas **cómo configurar el preprocesamiento** para una precisión óptima. Al limitar el motor a los rectángulos exactos que te interesan y limpiar la imagen previamente, obtienes resultados más rápidos y limpios—perfectos para la automatización de facturas, la digitalización de formularios o cualquier escenario donde solo una parte de la página sea relevante.

¿Listo para el siguiente paso? Prueba ajustando las coordenadas de ROI para un tipo de documento diferente, o experimenta con banderas de preprocesamiento adicionales como `sharpen` o `noise_reduction`. La flexibilidad de Aspose OCR significa que puedes adaptar la canalización a prácticamente cualquier calidad de imagen.

Si encuentras un problema, revisa la salida de la consola para regiones vacías y vuelve a revisar la configuración de preprocesamiento. ¡Feliz codificación, y que tu OCR sea siempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}