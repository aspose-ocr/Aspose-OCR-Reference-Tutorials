---
category: general
date: 2026-04-26
description: Cómo crear OCR de forma rápida y fiable. Aprende a extraer texto de una
  imagen, cargar la imagen para OCR y ejecutar OCR en PNG con un diccionario personalizado.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: es
og_description: Cómo crear OCR en Python y extraer texto de una imagen. Esta guía
  muestra cómo cargar una imagen para OCR, ejecutar OCR en PNG y usar un diccionario
  personalizado.
og_title: Cómo crear OCR en Python – Extracción rápida de texto
tags:
- OCR
- Python
- Image Processing
title: Cómo crear OCR en Python – Extraer texto de una imagen
url: /es/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear OCR en Python – Guía paso a paso

¿Alguna vez te has preguntado **cómo crear OCR** que pueda leer tus PDFs escaneados, capturas de pantalla o notas manuscritas? No estás solo. En muchos proyectos del mundo real necesitamos *extraer texto de imágenes*, pero los motores listos para usar a menudo tropiezan con palabras específicas de dominio.  

En este tutorial verás un ejemplo completo y ejecutable que carga una imagen para OCR, aplica un diccionario personalizado y, finalmente, **ejecuta OCR en archivos PNG**. Al terminar podrás extraer texto de cualquier imagen y adaptar el motor a tu propia terminología.

## Qué cubre este tutorial

Recorreremos cada paso que necesitas:

* Instalar el pequeño pero potente paquete `aocr` (o cualquier biblioteca compatible).  
* Configurar un **diccionario personalizado** para que términos como `aspocorp` o `licensekey` sean reconocidos.  
* **Cargar una imagen para OCR**, ya sea PNG, JPEG o una página de PDF escaneada.  
* Ejecutar el proceso OCR e imprimir el resultado.  

Sin enlaces a documentación externa, solo una solución autocontenida que puedes copiar‑pegar y ejecutar hoy.

### Requisitos previos

* Python 3.8 o superior (el código usa f‑strings).  
* Familiaridad básica con la línea de comandos – escribirás un par de comandos `pip install`.  
* Un archivo de imagen (`technical_doc.png` en el ejemplo) colocado en una ubicación a la que puedas referenciar.  

Si cumples con esos tres puntos, estás listo para comenzar.  

---

## Paso 1: Instalar la biblioteca OCR

Primero, necesitamos un motor OCR que soporte un objeto de configuración programable. El paquete `aocr` es un contenedor ligero alrededor de un motor OCR nativo y funciona bien para demostraciones.

```bash
# Install the library (run once)
pip install aocr
```

> **Consejo profesional:** Si estás en Windows y encuentras un error de compilación, prueba `pip install aocr‑binary` que incluye ruedas precompiladas.

### ¿Por qué instalar esta biblioteca?

`aocr` nos da acceso directo a un objeto `config` donde podemos inyectar un **diccionario personalizado**. Esa es la clave para mejorar la precisión en vocabularios especializados.

---

## Paso 2: Crear la instancia del motor OCR y añadir un diccionario personalizado

Ahora iniciamos el motor y le indicamos qué palabras debe tratar como conocidas.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Por qué importa un diccionario personalizado

Los modelos OCR estándar se entrenan con corpus genéricos. Cuando el modelo ve “aspocorp”, podría dividirlo en “aspo corp” o eliminar letras por completo. Al proporcionar una lista personalizada, sesgamos el reconocedor hacia la ortografía exacta que necesitamos, reduciendo drásticamente el esfuerzo de post‑procesamiento.

---

## Paso 3: Cargar la imagen que deseas procesar

Aquí es donde **cargamos la imagen para OCR**. El método `Image.load` acepta una cadena de ruta y determina automáticamente el tipo de archivo.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Caso límite:** Si tu fuente es un PDF de varias páginas, conviértelo primero a PNG (por ejemplo, con `pdf2image`) y aliméntalo página por página al motor.

### Consejos para una mejor calidad de imagen

* Mantén la resolución al menos en 300 dpi.  
* Asegúrate de que la imagen esté orientada correctamente; rota con `Pillow` si es necesario.  
* Convierte escaneos en color a escala de grises para reducir ruido.

---

## Paso 4: Ejecutar el proceso OCR en el archivo PNG

Con el motor configurado y la imagen cargada, finalmente **ejecutamos OCR en PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

La llamada `process()` devuelve un objeto que contiene el texto reconocido, puntuaciones de confianza y cajas delimitadoras para cada palabra.

---

## Paso 5: Mostrar el texto reconocido

La forma más sencilla de ver lo que el motor encontró es imprimir el atributo `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Salida esperada

Si `technical_doc.png` contiene la frase *“The Aspocorp licensekey expires on 2025‑12‑31.”*, la consola debería mostrar:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Observa cómo el diccionario personalizado mantuvo el nombre de la marca intacto—algo que un OCR convencional podría haber distorsionado.

---

## Ejemplo completo funcional (listo para copiar y pegar)

A continuación tienes el script completo, listo para guardarse como `run_ocr.py`. Solo reemplaza la ruta de ejemplo por la ubicación de tu imagen.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Ejecuta desde la terminal:

```bash
python run_ocr.py
```

Deberías ver el texto extraído impreso en la consola, exactamente como se mostró en el ejemplo anterior.

---

## Preguntas frecuentes (FAQ)

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo extraer texto de un PDF escaneado?** | Sí. Convierte cada página a PNG (o TIFF) primero, luego alimenta las imágenes al mismo script. |
| **¿Qué pasa si mi imagen es JPEG en lugar de PNG?** | El método `Image.load` soporta JPEG, BMP, TIFF y PNG de forma nativa. Simplemente cambia la extensión del archivo. |
| **¿Cómo mejoro la precisión en escaneos de bajo contraste?** | Pre‑procesa con `Pillow`: aumenta el contraste, aplica binarización o usa `opencv` para corregir la inclinación. |
| **¿Hay forma de obtener puntuaciones de confianza para cada palabra?** | `ocr_result` incluye `words`; cada palabra tiene un atributo `confidence` que puedes iterar. |
| **¿Puedo ejecutar esto en un servidor sin interfaz gráfica?** | Absolutamente. `aocr` no tiene dependencias GUI, lo que lo hace perfecto para pipelines CI. |

---

## Próximos pasos y temas relacionados

Ahora que sabes **cómo crear OCR** y **extraer texto de imágenes**, considera explorar:

* **Técnicas de pre‑procesamiento** – `load image for OCR` es solo el primer paso; usa `opencv` para desruido o enfoque.  
* **Procesamiento por lotes** – recorre un directorio de PNGs para generar un archivo archivado buscable.  
* **Soporte multilingüe** – añade paquetes de idioma al motor si necesitas leer documentos en francés o alemán.  
* **Integración con Elasticsearch** – indexa el texto extraído para búsquedas de texto completo en activos escaneados.  

Cada una de estas extensiones se basa en el patrón central que acabamos de cubrir, por lo que la transición será fluida.

---

## Conclusión

En unos minutos hemos respondido **cómo crear OCR** que extrae de forma fiable **texto de imágenes**, especialmente PNGs, y te hemos mostrado cómo **cargar imagen para OCR**, aplicar un **diccionario personalizado** y **ejecutar OCR en PNG** sin servicios externos.  

Prueba el script, ajusta el diccionario a tu propio vocabulario y tendrás una base sólida para cualquier proyecto de digitalización de documentos.  

Si encontraste algún problema, deja un comentario abajo—estamos felices de ayudar. Y no olvides compartir tus historias de éxito; la comunidad aprende mejor con ejemplos del mundo real.  

**¿Listo para automatizar tu papeleo?** Obtén el código, adáptalo y comienza a convertir píxeles en texto buscable hoy mismo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}