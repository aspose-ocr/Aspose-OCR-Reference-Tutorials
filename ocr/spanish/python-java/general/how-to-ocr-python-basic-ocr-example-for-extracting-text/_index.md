---
category: general
date: 2026-04-26
description: 'cómo hacer OCR en Python: aprende a extraer texto de una imagen y a
  leer archivos TIFF con Python usando un ejemplo básico de OCR. Código rápido y ejecutable
  incluido.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: es
og_description: 'cómo hacer OCR en Python: una guía paso a paso que muestra cómo extraer
  texto de una imagen, leer archivos TIFF con Python y convertir texto de imágenes
  escaneadas con un script simple y ejecutable.'
og_title: cómo hacer OCR en Python – Ejemplo básico de OCR para extraer texto
tags:
- OCR
- Python
- Image Processing
title: Cómo hacer OCR en Python – Ejemplo básico de OCR para extraer texto
url: /es/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo hacer OCR con Python – Ejemplo básico de OCR para extraer texto

¿Alguna vez te has preguntado **how to ocr python** cuando tienes un archivo TIFF escaneado sobre tu escritorio? No eres el único que mira una serie de archivos de imagen y se pregunta: “¿Cómo saco las palabras de esto?” La buena noticia es que convertir una foto en texto plano es pan comido con la biblioteca adecuada y unos pocos pasos claros.

En este tutorial recorreremos un **basic OCR example** que lee un archivo TIFF, extrae el texto y lo imprime en la consola. Al final sabrás exactamente cómo **extract text from image** archivos, cómo manejar las particularidades de los formatos TIFF y qué ajustar si necesitas **convert scanned image text** a algo más útil. Sin magia oculta—solo Python directo que puedes copiar‑pegar y ejecutar hoy.

## What You’ll Need

Antes de sumergirnos, asegúrate de tener:

- Python 3.9+ instalado (la última versión estable es la mejor).
- Una biblioteca OCR instalable con pip. Para esta guía usaremos un paquete ficticio `aocr` que imita herramientas populares como Tesseract; puedes reemplazarlo con `pytesseract` o `easyocr` más adelante.
- Una imagen TIFF que quieras procesar – nómbrala `input.tiff` y colócala en una carpeta que referenciarás en el código.
- Familiaridad básica con la línea de comandos (solo para instalar el paquete).

Eso es todo. Sin dependencias pesadas, sin contenedores Docker, solo unas pocas líneas de código.

## Step 1 – Install and Import Dependencies (how to ocr python)

Primero, obtén el paquete OCR. Abre una terminal y ejecuta:

```bash
pip install aocr
```

Si prefieres una biblioteca del mundo real, cambia `aocr` por `pytesseract` e instala el motor Tesseract por separado.

Ahora importa lo que necesitamos. La clase `Path` de `pathlib` nos brinda una forma limpia de trabajar con rutas de archivo en diferentes sistemas operativos.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*¿Por qué usar `Path`?* Porque abstrae las barras (`/` vs `\`) y te permite unir directorios sin preocuparte por el SO subyacente. Ese pequeño detalle suele ahorrar dolores de cabeza cuando luego mueves el script a un servidor CI.

## Step 2 – Create the OCR Engine Instance (basic ocr example)

A continuación, inicia el motor OCR. Piensa en `OcrEngine` como el cerebro que leerá la imagen y devolverá caracteres.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

La mayoría de las bibliotecas OCR te permiten ajustar idioma, DPI o umbrales de confianza aquí. Para este **basic OCR example** nos quedaremos con los valores predeterminados, pero puedes explorar `ocr_engine.config` más adelante si necesitas manejar documentos multilingües.

## Step 3 – Load Your TIFF Image (read tiff file python)

Aquí es donde entra la parte de **read tiff file python**. Los TIFF pueden ser de varias páginas, pero `Image.load` tomará la primera página por defecto—perfecto para un escaneo de una sola página.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Reemplaza `"YOUR_DIRECTORY"` con la carpeta real que contiene `input.tiff`. Si no estás seguro de dónde se ejecuta el script, `Path.cwd()` imprime el directorio de trabajo actual—útil para depurar problemas de rutas.

## Step 4 – Run the OCR Process (extract text from image)

Ahora ocurre la magia. Llamar a `process()` envía la imagen a través del pipeline OCR y devuelve un objeto de resultado.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Detrás de escena el motor podría estar convirtiendo la imagen a escala de grises, aplicando umbralizado y alimentándola a una red neuronal. No necesitas gestionar esos pasos; la biblioteca los abstrae.

## Step 5 – Print the Recognized Text (convert scanned image text)

Finalmente, muestra el texto. En proyectos reales probablemente lo escribirías en un archivo o base de datos, pero imprimir mantiene el ejemplo ordenado.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Al ejecutar el script, deberías ver algo como:

```
Hello, world!
This is a sample scanned document.
```

Si la salida se ve distorsionada, verifica que la imagen fuente sea clara y que el idioma OCR coincida con el texto.

## Full Working Script

Juntándolo todo, aquí tienes el programa completo, listo para ejecutar:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Expected Output

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Si necesitas **convert scanned image text** a un PDF buscable, puedes canalizar `ocr_result.text` a un generador de PDF como `reportlab`—pero eso es un tutorial aparte.

## Common Pitfalls & Pro Tips

- **Escaneos de baja resolución**: OCR tiene problemas por debajo de 150 DPI. Si tu TIFF está borroso, aumenta la resolución primero con Pillow (`Image.open(...).resize(...)`).
- **Múltiples páginas**: Para TIFF de varias páginas, itera sobre `Image.load_multi_page()` (si tu biblioteca lo soporta) y concatena los resultados.
- **Soporte de idioma**: Muchos motores usan inglés por defecto. Configura `ocr_engine.language = "spa"` para español, por ejemplo.
- **Manejo de espacios en blanco**: OCR suele añadir saltos de línea extraños. Usa `str.splitlines()` o expresiones regulares para limpiar la salida.
- **Rendimiento**: Para procesamiento masivo, reutiliza una única instancia de `OcrEngine` en lugar de crear una nueva por archivo.

## Extending the Example

Ahora que dominas **how to ocr python** para una sola imagen, considera los siguientes pasos:

1. **Procesamiento por lotes** – Recorre un directorio de TIFFs y escribe cada resultado en un archivo `.txt`.
2. **Integración con Pandas** – Almacena el texto extraído junto con metadatos para análisis rápido.
3. **Enfoque híbrido** – Combina OCR con bibliotecas NLP como `spaCy` para extraer entidades (nombres, fechas, montos) de facturas escaneadas.
4. **Formatos de archivo alternativos** – Cambia `Image.load` por `Image.from_bytes` para manejar imágenes provenientes de una API o base de datos.

Todos estos se basan en la idea central de **extract text from image** y **convert scanned image text** en algo que las máquinas puedan entender.

## Conclusion

Hemos recorrido un **basic OCR example** claro, de extremo a extremo, que muestra **how to ocr python**, cómo **read tiff file python**, y cómo **extract text from image** archivos con solo unas cuantas líneas. El script es autónomo, incluye manejo de errores y muestra el resultado directamente, constituyendo una base sólida para cualquier proyecto que necesite convertir documentos escaneados en texto editable.

Siéntete libre de experimentar—cambia el backend OCR, ajusta el preprocesamiento o conecta la salida a un flujo de trabajo posterior. El cielo es el límite cuando puedes **convert scanned image text** en datos buscables y utilizables.

¿Tienes preguntas sobre casos límite, paquetes de idioma o afinación de rendimiento? Deja un comentario abajo, ¡y feliz codificación! 

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}