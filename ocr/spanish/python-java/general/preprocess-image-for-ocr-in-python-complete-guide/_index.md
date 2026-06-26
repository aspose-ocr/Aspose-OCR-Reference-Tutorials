---
category: general
date: 2026-06-25
description: Preprocesar la imagen para OCR y reconocer el texto de un documento escaneado
  usando Python. Tutorial paso a paso con código completo.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: es
og_description: Preprocesa la imagen para OCR y reconoce el texto de un documento
  escaneado con Python. Sigue este tutorial detallado y ejecutable.
og_title: Preprocesar imagen para OCR en Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Preprocesar imagen para OCR en Python – Guía completa
url: /es/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocesar imagen para OCR en Python – Guía completa

¿Alguna vez te has preguntado cómo **preprocesar imagen para OCR** de modo que el texto salga limpio y fiable? No estás solo: la mayoría de los desarrolladores se topan con el mismo problema cuando la página escaneada está torcida o el contraste es irregular. La buena noticia es que unas cuantas líneas de Python pueden enderezar ese desorden, binarizar la imagen y devolverte texto nítido y buscable.

En este tutorial recorreremos paso a paso los pasos exactos para **preprocesar imagen para OCR** *y* **reconocer texto de documentos escaneados**, usando una biblioteca OCR popular. Al final tendrás un script listo para ejecutar, comprenderás por qué cada configuración es importante y sabrás cómo ajustarla para casos límite complicados.

## Lo que necesitarás

- Python 3.8 o superior (el código también funciona en 3.10+)
- Un paquete OCR que exponga las clases `OcrEngine`, `ImagePreProcessingOptions` y `Image` (por ejemplo, el ficticio módulo `ocr` usado en el ejemplo)
- Un documento escaneado o fotografiado que esté un poco sesgado o con bajo contraste
- Tu IDE favorito o una simple terminal—no se requiere una GUI pesada

Eso es todo. Sin binarios extra, sin gimnasia Docker. Vamos al grano.

## Preprocesar imagen para OCR – Paso a paso

A continuación se muestra el flujo central dividido en cinco etapas claras. Cada etapa incluye **por qué** lo hacemos, el **código** exacto y una breve **explicación** de lo que ocurre tras bambalinas.

### Paso 1: Crear una instancia del motor OCR

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Por qué es importante:*  
El objeto `OcrEngine` es el cerebro de la operación. Contiene configuraciones como paquetes de idioma, umbrales de confianza y—lo más importante para nosotros—banderas de pre‑procesamiento de imagen. Instanciarlo primero nos da una hoja en blanco para habilitar los trucos que siguen.

### Paso 2: Habilitar la corrección automática de sesgo y la binarización

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Por qué es importante:*  
- **Deskewing** (corrección de sesgo) rota la imagen para que las líneas de texto queden horizontales. Los motores OCR tienen dificultades cuando la línea base se inclina más de unos pocos grados.  
- **Binarización** convierte la imagen a puro blanco y negro, eliminando el ruido de fondo que puede confundir a los clasificadores de caracteres.  
Ambas opciones son *automáticas* en muchas bibliotecas modernas, pero aún debes activarlas—de ahí la asignación explícita.

> **Consejo profesional:** Si tus imágenes de origen ya están perfectamente alineadas, puedes establecer `auto_deskew=False` para ahorrar un milisegundo de tiempo de procesamiento.

### Paso 3: Cargar la imagen sesgada que deseas procesar

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Por qué es importante:*  
El método `Image.load` lee el archivo en memoria y lo envuelve en un objeto que el motor OCR entiende. También extrae metadatos como DPI, que pueden influir en el factor de escala predeterminado para la corrección de sesgo.

> **Caso límite:** Si la imagen es un TIFF de varias páginas, deberás iterar sobre cada página o usar un ayudante como `ocr.MultiPageImage.load`. Las mismas configuraciones de pre‑procesamiento se aplican a cada página.

### Paso 4: Ejecutar OCR sobre la imagen pre‑procesada

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Por qué es importante:*  
En este punto el motor aplica los pasos de corrección de sesgo y binarización que habilitamos antes, y luego ejecuta su red neuronal (o la clásica cadena estilo Tesseract) sobre el bitmap limpio. El objeto `result` devuelto suele contener el texto plano, puntuaciones de confianza y, a veces, datos posicionales para cada palabra.

> **¿Y si el texto sigue ilegible?**  
Revisa la resolución de la imagen: OCR funciona mejor a 300 dpi o más. Si tu origen es inferior, considera escalarla antes de cargarla, o solicita el escaneo original a la fuente del documento.

### Paso 5: Mostrar el texto reconocido

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Por qué es importante:*  
`result.text` es una representación en cadena simple de todo lo que el motor pudo leer. Imprimirlo es útil para depuración rápida; en una aplicación real probablemente lo escribirías en un archivo `.txt`, una base de datos o lo alimentarías a una canalización NLP posterior.

---

## Reconocer texto de documentos escaneados – Más allá de lo básico

Ahora que la tubería básica funciona, exploremos algunas variaciones comunes que podrías encontrar al intentar **reconocer texto de documentos escaneados** en entornos reales.

### 1. Manejo de varios idiomas

Si tu documento contiene inglés y francés, configura el motor antes del paso 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

La mayoría de los motores OCR aceptan códigos ISO‑639‑2; cargar paquetes de idioma adicionales añade una pequeña sobrecarga pero mejora drásticamente la precisión en páginas multilingües.

### 2. Ajuste fino de los umbrales de binarización

La binarización automática funciona en la mayoría de los casos, pero algunas fotocopias antiguas necesitan un umbral personalizado:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Experimenta con valores entre 120 y 220 hasta que el fondo desaparezca sin borrar los caracteres tenues.

### 3. Extracción de información de diseño

A veces necesitas más que texto bruto—quieres saber dónde está cada párrafo en la página. Muchos motores exponen una colección `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Esto es invaluable para reconstruir tablas o preservar el orden de columnas.

### 4. Procesar un lote de archivos

Si tienes una carpeta llena de PDFs escaneados convertidos a JPEG, envuelve todo el flujo en un bucle:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

El bucle reutiliza la misma instancia `engine`, lo que es más eficiente que crear una nueva para cada archivo.

### 5. Tratamiento de escaneos de baja resolución

Imágenes de baja resolución (< 150 dpi) suelen producir caracteres borrosos. Un remedio rápido es escalar usando un algoritmo de alta calidad antes de pasar la imagen al motor OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Escalar no creará detalles mágicamente, pero el paso de binarización puede trabajar con bordes más nítidos, ofreciendo una mejora modesta.

---

## Salida esperada

Ejecutar el script original de cinco pasos sobre un escaneo moderadamente sesgado de 300 dpi debería imprimir algo como:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Si ves caracteres extraños, verifica las banderas de pre‑procesamiento, la resolución de la imagen y la configuración de idioma.

---

## Conclusión

Hemos cubierto todo lo que necesitas para **preprocesar imagen para OCR** y **reconocer texto de documentos escaneados** usando Python. Partiendo de una instancia fresca del motor, habilitamos corrección automática de sesgo y binarización, cargamos una imagen sesgada, ejecutamos el reconocimiento y mostramos el texto limpio. En el camino exploramos soporte multilingüe, ajustes manuales de umbrales, extracción de diseño, procesamiento por lotes y soluciones para baja resolución.

Prueba el script con tus propios escaneos—quizá una pila de recibos, un formulario manuscrito o un recorte de periódico antiguo. Una vez que te sientas cómodo, intenta añadir generación de PDF o alimentar la salida a un índice de búsqueda. El cielo es el límite.

**¿Listo para el próximo desafío?** Consulta nuestros tutoriales sobre *“Extraer tablas de PDFs escaneados con Python”* y *“Entrenar modelos OCR personalizados con TensorFlow”* para seguir ampliando tu caja de herramientas de automatización documental.

¡Feliz codificación, y que tu OCR siempre sea nítido!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Extraer texto de imagen con Aspose OCR – Guía paso a paso](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraer texto de imagen – Optimización OCR con Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Cómo usar AspOCR: filtros de preprocesamiento de imagen OCR para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}