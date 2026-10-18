---
category: general
date: 2026-03-26
description: Aprende cómo realizar OCR en Python y reconocer texto de archivos de
  imagen. Esta guía muestra cómo extraer texto de PNG y convertir una imagen a texto
  rápidamente.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: es
og_description: ¿Cómo realizar OCR en Python? Sigue esta guía para reconocer texto
  de una imagen, extraer texto de PNG y convertir una imagen a texto con una licencia
  de prueba.
og_title: Cómo realizar OCR en Python – Tutorial completo
tags:
- OCR
- Python
- Image Processing
title: Cómo realizar OCR en Python – Tutorial completo paso a paso
url: /es/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR en Python – Tutorial completo paso a paso  

¿Alguna vez te has preguntado **cómo realizar OCR** en una foto que acabas de tomar con tu teléfono? No estás solo—desarrolladores de todo el mundo necesitan una forma fiable de reconocer texto a partir de archivos de imagen sin lidiar con bibliotecas nativas complejas.  

En este tutorial recorreremos un ejemplo práctico que muestra **cómo realizar OCR**, **recognize text from image**, y **extract text from PNG** usando un contenedor ligero de Python. Al final podrás **convert image to text** en solo unas pocas líneas de código, y no tendrás que preocuparte por problemas de licencias porque usaremos el modo de prueba incorporado.

## Lo que aprenderás  

* Cómo configurar una licencia de prueba para el motor OCR (no se necesita ruta de archivo).  
* La secuencia exacta de llamadas a objetos **recognize text from image**.  
* Formas de **extract text from PNG** archivos y manejar problemas comunes como fuentes faltantes.  
* Consejos para escalar la solución cuando pases de una licencia de prueba a una licencia de producción.  

**Prerequisitos** – necesitas Python 3.8+ y el paquete `ocr` (instalable vía `pip install ocr`). No se requieren otras herramientas externas.

---  

![ejemplo de cómo realizar OCR](https://example.com/ocr-demo.png "cómo realizar OCR en Python – texto reconocido mostrado")  

*Texto alternativo de la imagen: cómo realizar OCR en Python – ejemplo de salida*  

## Paso 1 – Activar una licencia de prueba (sin ruta de archivo necesaria)  

Antes de que el motor pueda leer cualquier cosa, necesita una licencia válida. El modo de prueba es perfecto para experimentos y proyectos pequeños.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Por qué es importante:* El objeto de licencia indica a la biblioteca OCR que estás operando en un entorno aislado. Si omites este paso, el motor lanzará un `LicenseError` en el momento en que llames a `recognize()`.

**Consejo profesional:** Cuando pases a una licencia paga, reemplaza las dos líneas anteriores con `ocr.License("path/to/your/license.key").apply()`.

## Paso 2 – Crear la instancia del motor OCR  

Ahora que la prueba está activa, instanciamos el motor principal. Piensa en él como el “cerebro” que observará la imagen y decidirá qué caracteres están dónde.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Por qué es importante:* El `OcrEngine` contiene configuraciones como paquetes de idioma y ajustes de DPI. Puedes modificar esos valores más tarde, pero el predeterminado funciona para la mayoría de los PNGs solo en inglés.

## Paso 3 – Cargar el PNG que deseas procesar  

Aquí es donde **recognize text from image**. El método `ocr.Imaging.Image.load()` soporta PNG, JPEG, BMP y algunos otros formatos.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Caso límite:* Si tu PNG usa una paleta indexada (común en capturas de pantalla), el cargador lo convertirá automáticamente a un búfer RGB de 24 bits. Esa conversión puede ser una ligera pérdida de rendimiento, pero garantiza resultados OCR precisos.

## Paso 4 – Ejecutar el OCR y obtener el texto  

Finalmente, le pedimos al motor que haga su trabajo y luego extraemos el resultado en texto plano.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Salida esperada** (ejemplo para una imagen simple que contiene “Hello World”):

```
Hello World
```

Si la imagen contiene varias líneas, la salida preservará los saltos de línea, facilitando su uso en procesos posteriores como analizadores CSV o pipelines de NLP.

## Opcional: Ajuste fino para mayor precisión  

* **Paquetes de idioma:** `ocr_engine.set_language("eng")` (predeterminado) o `"fra"` para francés.  
* **Escalado de DPI:** `ocr_engine.set_dpi(300)` puede mejorar los resultados en escaneos de baja resolución.  
* **Pre‑procesamiento:** Aplicar un umbral binario (`ocr.Imaging.Image.threshold()`) antes de `set_image` suele producir texto más limpio en fondos ruidosos.

Estos ajustes son útiles cuando pasas de una demostración rápida a un **ocr tutorial python** de nivel producción que procesa cientos de archivos al día.

## Script completo – Listo para copiar y pegar  

A continuación se muestra el script completo y ejecutable que combina todos los pasos anteriores. Guárdalo como `run_ocr.py` y reemplaza `YOUR_DIRECTORY/sample1.png` con la ruta a tu propio PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Ejécútalo desde la línea de comandos:

```bash
python run_ocr.py
```

Deberías ver el texto extraído impreso en la consola. Si obtienes una cadena vacía, verifica que la imagen realmente contenga texto claro y de alto contraste y que la licencia de prueba se haya aplicado sin errores.

## Preguntas comunes y trampas  

* **“¿Funciona esto con JPEG?”** – Absolutamente. El método `load()` detecta automáticamente el formato, por lo que puedes cambiar PNG por JPEG sin modificar el código.  
* **“¿Qué pasa si la imagen está rotada?”** – El motor puede detectar automáticamente la orientación, pero para obtener mejores resultados puedes pre‑rotar con `input_image.rotate(90)` antes de `set_image`.  
* **“¿Puedo procesar múltiples imágenes en un bucle?”** – Sí. Simplemente mueve las llamadas de carga y `recognize()` dentro de un bucle `for`; la misma instancia `ocr_engine` puede reutilizarse, lo que ahorra una pequeña cantidad de sobrecarga.  

## Próximos pasos – De la demo a producción  

Ahora que sabes **cómo realizar OCR**, considera estos temas de seguimiento:

* **Procesamiento por lotes** – Combina este script con `os.listdir()` para **extract text from PNG** archivos en masa.  
* **Integrar con PDF** – Usa `pdf2image` para convertir páginas PDF a PNG, y luego introdúcelas en la misma canalización.  
* **Post‑procesamiento** – Aplica expresiones regulares o coincidencia difusa para limpiar errores comunes de reconocimiento OCR (p. ej., “0” vs “O”).  

Cada uno de estos se basa en la idea central de **convert image to text** y amplía la utilidad de tu flujo de trabajo OCR.

---  

### TL;DR  

Hemos cubierto todo lo que necesitas saber para **cómo realizar OCR** en Python: activar una licencia de prueba, crear un motor, cargar un PNG, ejecutar el reconocimiento y imprimir el resultado. Con solo un puñado de líneas puedes **recognize text from image**, **extract text from PNG**, y **convert image to text** para cualquier aplicación posterior.  

Pruébalo, ajusta la configuración de DPI o de idioma, y deja que el motor haga el trabajo pesado. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}