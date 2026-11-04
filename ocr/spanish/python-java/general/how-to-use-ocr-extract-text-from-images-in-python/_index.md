---
category: general
date: 2026-03-18
description: Cómo usar OCR para extraer texto de imágenes – una guía rápida para reconocer
  texto de archivos PNG y cargar imágenes para OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: es
og_description: Cómo usar OCR para extraer texto de imágenes – aprende a reconocer
  texto de PNG, cargar la imagen para OCR y extraer texto con un sencillo script de
  Python.
og_title: 'Cómo usar OCR: extraer texto de imágenes en Python'
tags:
- OCR
- Python
- Image Processing
title: 'Cómo usar OCR: extraer texto de imágenes en Python'
url: /es/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR: Extraer texto de imágenes en Python

¿Alguna vez te has preguntado **cómo usar OCR** cuando tienes una captura de pantalla desordenada o un recibo escaneado? No estás solo—los desarrolladores necesitan constantemente extraer texto legible de imágenes, especialmente PNGs que provienen de aplicaciones móviles o cargas web. En este tutorial recorreremos un ejemplo completo y ejecutable que te muestra cómo **extraer texto de una imagen**, **reconocer texto de PNG** y hasta **cargar imagen para OCR** con solo unas pocas líneas de Python.

Cubrirémos todo, desde instalar la biblioteca adecuada hasta manejar documentos multilingües, de modo que al final sepas exactamente *cómo extraer texto* de cualquier imagen que le pases al motor. Sin referencias vagas, solo una solución clara, paso a paso, que puedes copiar‑pegar y ejecutar.

## Lo que aprenderás

En las siguientes secciones:

1. Configurar un motor OCR ligero (sin dependencias pesadas).  
2. Cargar un archivo de imagen—específicamente un PNG—en el motor.  
3. Habilitar la detección automática de idioma para que el motor pueda manejar contenido multilingüe.  
4. Ejecutar el proceso de reconocimiento y obtener el resultado en texto plano.  
5. Ajustar el flujo de trabajo para casos límite como archivos faltantes o formatos no compatibles.

Si te sientes cómodo con Python básico, estás listo. No se necesita experiencia previa en OCR, aunque una rápida mirada a la documentación de la biblioteca nunca está de más.

---

![Cómo usar OCR en una imagen PNG](placeholder.png "Cómo usar OCR en una imagen PNG – guía paso a paso")

## Cómo usar OCR – Cargar imagen y reconocer texto {#how-to-use-ocr}

### Paso 1: Instalar la biblioteca OCR

Lo primero, necesitas un paquete de Python que proporcione una clase `OcrEngine`. Para el propósito de este tutorial usaremos el paquete ficticio pero ilustrativo **SimpleOCR**, que puedes instalar vía pip:

```bash
pip install simple-ocr
```

> **Consejo profesional:** Si trabajas en un entorno virtual (altamente recomendado), actívalo antes de ejecutar el comando de instalación. Esto mantiene ordenadas las dependencias de tu proyecto.

### Paso 2: Importar el motor y crear una instancia

Crear el motor es tan fácil como llamar a su constructor. Piensa en el motor como el “cerebro” que más tarde procesará la imagen que le proporciones.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

¿Por qué creamos una nueva instancia cada vez? Aislamiento. Un motor nuevo garantiza que ningún estado residual de una ejecución anterior contamine el reconocimiento actual, lo cual es crucial cuando procesas muchos archivos en lote.

### Paso 3: Cargar la imagen que deseas procesar

Ahora realmente **cargamos la imagen para OCR**. El método `setImageFromFile` acepta una ruta a cualquier imagen raster; apuntaremos a un PNG llamado `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Si el archivo no se encuentra, `SimpleOCR` lanza un claro `FileNotFoundError`. Puedes capturarlo para proporcionar un mensaje de error amigable:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Paso 4: Habilitar la detección automática de idioma

La mayoría de los motores OCR modernos vienen con paquetes de idiomas. Al pasar `"multilingual"` le indicamos al motor que detecte el texto y seleccione automáticamente el modelo de idioma correcto. Esto es especialmente útil cuando tu PNG contiene una mezcla de inglés y español, por ejemplo.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Si conoces el idioma de antemano, puedes reemplazar `"multilingual"` con una localidad específica como `"eng"` o `"spa"` para acelerar el procesamiento.

### Paso 5: Ejecutar el proceso de reconocimiento

El trabajo pesado ocurre aquí. `recognize()` escanea la imagen, aplica segmentación, ejecuta la red neuronal y construye internamente un búfer de texto.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Detrás de escena el motor realiza:

- **Pre‑processing** (deskewing, binarization)  
- **Layout analysis** (detecting columns, tables)  
- **Character classification** (using a deep‑learning model)  

Todo eso está abstraído, por eso solo necesitas una línea.

### Paso 6: Recuperar e imprimir el texto reconocido

Finalmente, obtenemos el objeto de resultado y extraemos la cadena simple. Esta es la parte donde realmente **extraes texto de una imagen**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Salida esperada** (truncada por brevedad):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Si la imagen no contiene caracteres reconocibles, `text` será una cadena vacía. Puedes protegerte contra eso:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Extraer texto de imagen – Manejo de casos límite comunes

### Múltiples idiomas en un archivo

Cuando un documento mezcla idiomas, la configuración `"multilingual"` suele hacer lo correcto. Sin embargo, si notas errores de reconocimiento, puedes especificar manualmente una lista de respaldo:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Formatos no PNG

Aunque nuestro enfoque es **reconocer texto de PNG**, `SimpleOCR` también acepta JPEG, BMP y TIFF. Simplemente cambia la extensión del archivo en `setImageFromFile`. Para pilas de TIFF, puede que necesites seleccionar una página específica:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Archivos grandes y uso de memoria

Si estás procesando escaneos de gigapíxeles, considera redimensionar antes del OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Redimensionar reduce la presión de memoria mientras preserva suficiente detalle para un reconocimiento preciso.

### Depuración de cargas fallidas

A veces una imagen parece correcta a simple vista pero está corrupta internamente. Habilita el registro detallado para ver lo que el motor detecta:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Script completo, listo para ejecutar

A continuación está el programa completo que une todas las piezas. Cópialo en un archivo llamado `ocr_demo.py`, ajusta el marcador `YOUR_DIRECTORY` y ejecuta `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Ejecutar este script debería imprimir la versión de texto plano de lo que sea que esté dentro de `mixed_doc.png`. Siéntete libre de cambiar el archivo por cualquier otra imagen—**cómo extraer texto** funciona de la misma manera.

---

## Conclusión

Acabamos de repasar **cómo usar OCR** en Python para **extraer texto de archivos de imagen**, enfocándonos específicamente en **reconocer texto de PNG** y los pasos prácticos para **cargar imagen para OCR**. El fragmento anterior es una solución autónoma: instala el paquete, alimenta un archivo, habilita la detección multilingüe, ejecuta el motor y obtén el resultado.

Desde aquí podrías:

- Integrar el script en un servicio web que acepte cargas de usuarios.  
- Procesar por lotes una carpeta de PDFs convertidos a PNG.  
- Agregar post‑procesamiento (p. ej., limpieza con expresiones regulares, corrección ortográfica) para mejorar la precisión.

Recuerda, la calidad del OCR depende de la claridad de la imagen, los paquetes de idioma adecuados y, a veces, un poco de pre‑procesamiento—así que experimenta

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}