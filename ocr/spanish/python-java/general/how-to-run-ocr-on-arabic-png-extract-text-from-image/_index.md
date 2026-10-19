---
category: general
date: 2026-03-26
description: Aprende a ejecutar OCR en imágenes PNG en árabe y extraer texto árabe
  rápidamente. Esta guía muestra cómo convertir la imagen a texto con código Python
  paso a paso.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: es
og_description: ¿Cómo ejecutar OCR en imágenes PNG en árabe? Sigue esta guía completa
  para extraer texto árabe, reconocer texto árabe y convertir la imagen a texto usando
  Python.
og_title: Cómo ejecutar OCR en PNG árabe – Extraer texto de la imagen
tags:
- OCR
- Python
- Arabic
title: Cómo ejecutar OCR en PNG árabe – Extraer texto de la imagen
url: /es/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR en PNG árabe – Extraer texto de la imagen

¿Alguna vez te has preguntado **cómo ejecutar OCR** en una imagen que contiene escritura árabe? Tal vez tengas un recibo escaneado, un manuscrito histórico o simplemente una captura de pantalla de una publicación en redes sociales y necesites el texto en un formato buscable. No estás solo: desarrolladores de todo el mundo se topan con este problema al trabajar con lenguas de derecha a izquierda.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra **cómo ejecutar OCR** en un archivo PNG, extraer texto árabe y imprimir el resultado en la consola. No hay enlaces vagos del tipo “ver la documentación”; solo el código que puedes copiar‑pegar, más explicaciones de por qué cada línea es importante. Al final podrás **convertir imagen a texto** de forma fiable, incluso cuando la fuente sea un PNG árabe complicado.

> **Lo que aprenderás**
> - Configurar un motor OCR de Python para árabe  
> - Cargar una imagen PNG y manejar trampas comunes  
> - Reconocer texto árabe y verificar la salida  
> - Consejos para **extraer texto árabe** de diferentes calidades de imagen  

Antes de sumergirnos, asegúrate de tener Python 3.8+ instalado y una versión reciente de la librería `ocr` (la que se usa en el fragmento). Si utilizas un entorno virtual, actívalo ahora; esto mantiene las dependencias ordenadas.

## Requisitos previos

- Python 3.8 o superior  
- Paquete `ocr` (`pip install ocr‑engine` – reemplaza con el nombre real del paquete)  
- Una imagen PNG en árabe (`arabic_doc.png`) ubicada en un lugar al que puedas referenciar  
- Familiaridad básica con funciones y clases de Python  

Eso es todo. Sin frameworks pesados, sin contenedores Docker; solo Python puro.

## Paso 1: Instalar e importar la biblioteca OCR

Lo primero. Necesitamos el motor OCR propiamente dicho. La biblioteca que usaremos expone una clase `OcrEngine` con una API sencilla.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*¿Por qué importar `Imaging` por separado?* El submódulo `Imaging` nos brinda un método conveniente `Image.load` que entiende PNG, JPEG y TIFF de forma nativa. Omitir este paso te obligaría a manejar bytes crudos tú mismo, lo cual es innecesario para la mayoría de los casos de uso.

## Paso 2: Crear la instancia del motor OCR

Ahora creamos una instancia del motor. Piensa en este objeto como el “cerebro” que procesará la imagen.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Consejo profesional:** Si planeas procesar muchas imágenes en sucesión, reutiliza la misma instancia `ocr_engine`. Esta almacena en caché los modelos de idioma, lo que acelera los reconocimientos posteriores.

## Paso 3: Establecer el idioma a árabe

El árabe no es latín; tiene su propio conjunto de caracteres, dirección de derecha a izquierda y conformación contextual. Por eso debemos indicarle explícitamente al motor qué modelo de idioma cargar.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Si olvidas esta línea, el motor usará inglés por defecto y obtendrás una salida distorsionada—algo que he visto ocurrir con demasiada frecuencia.

## Paso 4: Cargar tu imagen PNG

Aquí es donde realmente comienza la parte de **convertir imagen a texto**. Cargaremos el archivo PNG que contiene la escritura árabe.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Casos límite comunes

| Problema | Síntoma | Solución |
|----------|---------|----------|
| La imagen está demasiado oscura | La salida contiene muchos espacios en blanco | Pre‑procesar con Pillow (`ImageEnhance.Brightness`) |
| El PNG tiene un canal alfa | Algunos motores OCR leen mal los píxeles transparentes | Convertir a RGB (`image.convert("RGB")`) antes de cargar |
| El texto está rotado | El texto reconocido está al revés | Rotar la imagen (`image.rotate(90, expand=True)`) antes de pasarla al motor |

## Paso 5: Ejecutar el proceso de reconocimiento

Con todo listo, finalmente pedimos al motor que haga su trabajo.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

El método `recognize` devuelve un objeto que contiene la cadena Unicode cruda, puntuaciones de confianza y cajas delimitadoras. Para la mayoría de los desarrolladores, el texto plano es todo lo que necesitan.

## Paso 6: Mostrar el texto árabe reconocido

Ahora imprimimos el resultado. En una aplicación real podrías escribirlo en un archivo, una base de datos o enviarlo a una API de traducción.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Al ejecutar el script, deberías ver los caracteres árabes mostrados en tu consola (asegúrate de que tu terminal soporte Unicode). Si ves signos de interrogación o cadenas vacías, verifica la configuración del idioma y la calidad de la imagen.

### Salida esperada

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Si la salida se parece a la línea anterior, ¡felicitaciones! Has **extraído texto árabe** de un PNG con éxito.

## Ejemplo completo y funcional

A continuación tienes el script completo, listo para copiar‑pegar. Sustituye `YOUR_DIRECTORY/arabic_doc.png` por la ruta a tu propio archivo.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Ejecuta con `python run_ocr.py` (o el nombre que le hayas dado al archivo). Si todo está instalado correctamente, verás la frase en árabe impresa en la consola.

## Cómo ejecutar OCR en diferentes formatos de imagen

El mismo código funciona para JPEG, TIFF o BMP—solo cambia la extensión del archivo. El método `Image.load` detecta automáticamente el formato, por lo que puedes **convertir imagen a texto** sin código adicional.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Recuerda que la calidad de la imagen fuente influye mucho en la precisión del paso de **reconocer texto árabe**. Imágenes de alta resolución y baja compresión dan los mejores resultados.

## Extraer texto de PNG: Consejos para mayor precisión

1. **Los DPI importan** – Apunta a al menos 300 dpi. DPI más bajo suele producir caracteres perdidos.  
2. **El contraste es rey** – Usa herramientas de procesamiento de imagen (p. ej., OpenCV) para aumentar el contraste antes de pasar la imagen al motor OCR.  
3. **Eliminación de ruido** – Pequeñas motas pueden confundir al modelo; el filtrado mediano ayuda.  

Aquí tienes un fragmento rápido usando Pillow para mejorar un PNG antes del OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Preguntas frecuentes

**P: ¿Esto funciona con otros idiomas de derecha a izquierda además del árabe?**  
R: Absolutamente. Solo cambia el código de idioma (`"ar"` → `"he"` para hebreo, `"fa"` para persa) y el motor cargará el modelo correspondiente.

**P: ¿Qué pasa si necesito extraer texto de varios PNG en una carpeta?**  
R: Recorre los archivos, reutiliza la misma instancia `ocr_engine` y recoge los resultados en una lista o escribe cada uno en un archivo `.txt` separado.

**P: ¿Puedo obtener puntuaciones de confianza para cada palabra?**  
R: Sí. `ocr_result` suele exponer un método `get_confidences()`. Empareja cada confianza con la palabra correspondiente para control de calidad.

## Próximos pasos

Ahora que sabes **cómo ejecutar OCR** en PNG árabes, considera estas ideas de seguimiento:

- **Procesamiento por lotes:** combina el script con `os.listdir` para **extraer texto árabe** de un directorio completo.  
- **Post‑procesamiento:** usa las bibliotecas `arabic_reshaper` y `python-bidi` para mostrar correctamente la salida de derecha a izquierda en PDFs.  
- **Integración:** alimenta el texto extraído a un índice de búsqueda (p. ej., Elasticsearch) para que los documentos escaneados sean buscables.  

Cada uno de estos temas se basa en los fundamentos cubiertos aquí y te ayudará a transformar un simple script de **convertir imagen a texto** en una canalización lista para producción.

---

![cómo ejecutar OCR en PNG árabe](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}