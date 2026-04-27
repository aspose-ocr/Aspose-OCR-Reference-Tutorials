---
category: general
date: 2026-04-26
description: Cómo ejecutar OCR en un formulario escaneado, aprender a preprocesar
  la imagen para reducir el ruido y extraer texto de la imagen rápidamente.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: es
og_description: Cómo ejecutar OCR en documentos escaneados, preprocesar imágenes,
  reducir el ruido y extraer texto de manera eficiente.
og_title: Cómo ejecutar OCR y preprocesar imágenes – Guía rápida
tags:
- OCR
- image processing
- Python
title: Cómo ejecutar OCR y preprocesar imágenes – Extraer texto de formularios escaneados
url: /es/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR – Guía completa para extraer texto de imágenes

¿Alguna vez te has preguntado **cómo ejecutar OCR** en un formulario escaneado desordenado y obtener texto limpio y buscable? No eres el único. En muchos proyectos del mundo real la imagen cruda está llena de manchas, iluminación desigual y otras peculiaridades que hacen que el OCR listo‑para‑usar falle.  

¿La buena noticia? Con solo unas pocas líneas de Python y una tubería de preprocesamiento inteligente, puedes aumentar drásticamente la precisión del reconocimiento, **reducir el ruido**, y extraer las palabras exactas que necesitas. En este tutorial recorreremos cada paso—desde cargar la imagen hasta imprimir la cadena final—para que termines con un fragmento listo‑para‑usar que puedes adaptar a facturas, recibos o cualquier documento escaneado.

## Lo que construirás

- Una instancia de `OcrEngine` que se comunica con la biblioteca OCR subyacente.  
- Una cadena de preprocesamiento que **binariza** la imagen y aplica un **desenfoque mediano** para suavizar las manchas.  
- Una llamada simple a `process()` que devuelve un objeto que expone `text`, la cadena extraída.  

Al final tendrás un script autónomo que puedes ejecutar en cualquier archivo de imagen y ver inmediatamente el texto extraído en la consola.

## Requisitos previos

- Python 3.9+ (la sintaxis usada aquí coincide con la última versión estable).  
- El paquete ficticio `aocr` – piénsalo como una capa ligera alrededor de Tesseract o cualquier motor OCR moderno. Instálalo con `pip install aocr`.  
- Una imagen escaneada (`scanned_form.jpg`) ubicada en una carpeta a la que puedas referenciar.  

Si estás usando una biblioteca OCR real como `pytesseract`, puedes sustituir `OcrEngine` por la clase correspondiente—todo lo demás permanece igual.

![](how-to-run-ocr-example.png "ejemplo de cómo ejecutar OCR mostrando un formulario escaneado y el texto extraído")

*Texto alternativo: cómo ejecutar OCR en un documento escaneado y ver el texto extraído.*

---

## Paso 1: Cómo ejecutar OCR – Inicializar el motor

Antes de que el motor pueda leer algo, necesitamos crear una instancia. Piensa en `OcrEngine` como el cerebro que más tarde interpretará los datos visuales.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Por qué es importante:** Instanciar el motor configura los modelos internos, carga los paquetes de idioma y prepara el entorno de ejecución. Omitir este paso suele resultar en un error `NoneType` cuando luego llamas a `process()`.

---

## Paso 2: Cómo preprocesar la imagen – Cargar tu formulario escaneado

Ahora que el cerebro está listo, le alimentamos con una imagen. La imagen puede estar en cualquier formato compatible con `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Consejo profesional:** Usa rutas absolutas durante el desarrollo para evitar sorpresas de “archivo no encontrado” cuando el script se ejecuta desde un directorio de trabajo diferente.

---

## Paso 3: Cómo reducir el ruido – Aplicar binarización y desenfoque mediano

Los escaneos crudos a menudo contienen puntos sueltos, fondo desigual o sombras tenues. Dos trucos clásicos—**binarización** y **desenfoque mediano**—limpian sin sacrificar los bordes que definen los caracteres.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Profundizando

- **Binarización**: El valor `threshold=180` le indica al algoritmo: “Todo lo que sea más brillante que 180 se vuelve blanco; todo lo demás se vuelve negro.” Ajusta este número si tu escaneo es demasiado oscuro o claro.  
- **Desenfoque mediano**: Un radio de `2` significa que el filtro observa una ventana de 5×5 píxeles y reemplaza el píxel central con el valor mediano. Esto suaviza manchas aisladas mientras mantiene los trazos de las letras intactos.

> **Caso límite:** Si tu documento tiene resaltados de color, un umbral binario simple puede borrarlos. En ese caso, considera usar `aocr.ImageFilters.adaptive_threshold()` en su lugar—esto adapta el corte localmente a lo largo de la imagen.

---

## Paso 4: Cómo extraer texto – Ejecutar el proceso OCR

Con una imagen limpia en mano, finalmente dejamos que el motor haga su magia.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **¿Qué ocurre tras bambalinas?** El motor ejecuta una red neuronal (o un emparejador de patrones heredado) sobre la matriz de píxeles, traduce cada glifo reconocido a caracteres Unicode y los ensambla en líneas y párrafos.

---

## Paso 5: Cómo extraer texto – Imprimir el resultado

El objeto `ocr_result` expone un conveniente atributo `text`. Veamos qué obtuvimos.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Salida esperada

Si el formulario escaneado contiene:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Deberías ver algo como:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Observa cómo el paso de preprocesamiento eliminó los puntos sueltos que antes convertían “Amount” en “Am0unt”. Ese es el poder de **cómo reducir el ruido** antes del OCR.

---

## Problemas comunes y cómo solucionarlos

| Síntoma | Causa probable | Solución rápida |
|---------|----------------|-----------------|
| Caracteres distorsionados (p.ej., “@#%”) | Imagen demasiado oscura o demasiado clara | Ajusta el `threshold` en `binarize()`; prueba `adaptive_threshold`. |
| Palabras faltantes | Ruido aún presente | Aumenta el `radius` para `median_blur` o agrega un filtro `gaussian_blur`. |
| Idioma incorrecto (p.ej., letras en inglés se convierten en chino) | Paquete de idioma incorrecto cargado | Pasa `language="eng"` al crear `OcrEngine()` si la biblioteca lo soporta. |
| Procesamiento lento en archivos grandes | Alta resolución | Reduce la escala de la imagen primero: `aocr.ImageFilters.resize(width=1200)` antes de la binarización. |

---

## Avanzando – Próximos pasos y temas relacionados

- **Procesamiento por lotes**: Envuelve la lógica anterior en un bucle para manejar docenas de archivos automáticamente.  
- **Salida estructurada**: Usa expresiones regulares en `ocr_result.text` para extraer campos como fechas o montos.  
- **Bibliotecas alternativas**: Sustituye `aocr` por `pytesseract`—el código cambia solo en el paso de inicialización del motor.  
- **Cómo preprocesar imágenes para PDFs**: Convierte cada página PDF a una imagen, luego aplica la misma tubería.  

Estas extensiones te permiten escalar la solución desde un solo formulario hasta una canalización de ingestión de documentos de nivel empresarial.

---

## Conclusión

Hemos cubierto **cómo ejecutar OCR** de principio a fin, mostrado **cómo preprocesar la imagen** para **reducir el ruido**, y demostrado **cómo extraer texto de la imagen** con un script limpio y reproducible. ¿La lección clave? Unos pocos filtros simples—binarización y desenfoque mediano—pueden convertir un escaneo ruidoso en una fuente de datos fiable, ahorrándote horas de limpieza manual.

Ejecuta el script con tus propios documentos, ajusta los umbrales y observa cómo aumenta la precisión. Cuando estés listo, explora el procesamiento por lotes o integra la salida en una base de datos para archivos buscables. ¡Feliz codificación, y que tu OCR siempre sea perfecto!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}