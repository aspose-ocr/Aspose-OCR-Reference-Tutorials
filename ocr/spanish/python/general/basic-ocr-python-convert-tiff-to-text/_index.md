---
category: general
date: 2026-03-18
description: El tutorial básico de OCR en Python muestra cómo convertir TIFF a texto,
  cargar OCR de imagen, configurar capas GPU y corregir ceros iniciales con Aspose
  AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: es
og_description: El tutorial básico de OCR en Python te guía a través de la conversión
  de archivos TIFF a texto limpio, la carga de imágenes, la configuración de capas
  GPU y la corrección de ceros iniciales.
og_title: OCR básico en Python – convertir TIFF a texto
tags:
- OCR
- Python
- AI
- Aspose
title: OCR básico en Python – convertir TIFF a texto
url: /es/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Convertir TIFF a Texto con Post‑procesamiento de IA

¿Buscas una forma de hacer **basic ocr python** en tus documentos escaneados? En esta guía recorreremos el proceso de convertir un archivo TIFF en texto limpio y buscable usando Aspose OCR y un post‑procesador de IA.  

Si alguna vez has tenido problemas para **convertir TIFF a texto** porque la salida cruda está llena de errores tipográficos o símbolos extraños, no estás solo. También te mostraremos cómo **cargar imagen OCR**, ajustar el motor para **establecer capas GPU**, y hasta **corregir ceros iniciales** que aparecen con frecuencia en números de facturas.

## Lo que aprenderás

- Cómo inicializar el motor Aspose OCR para documentos impresos.  
- Los pasos exactos para **cargar imagen OCR** desde un archivo TIFF y obtener texto crudo.  
- Configurar un modelo de IA, descargarlo automáticamente y **establecer capas GPU** para una inferencia más rápida.  
- Añadir corrección ortográfica incorporada más una función personalizada que **corrige ceros iniciales**.  
- Limpiar el resultado OCR y liberar recursos correctamente.  

Al final de este tutorial tendrás un único script de Python reutilizable que convierte cualquier TIFF en texto pulido y buscable—sin necesidad de copiar‑pegar manualmente.  

### Requisitos previos

- Python 3.8+ instalado en tu máquina.  
- Paquete `aspose-ocr` (`pip install aspose-ocr`).  
- Opcional: una GPU con al menos 4 GB de VRAM si deseas **establecer capas GPU**; de lo contrario el código recurre automáticamente a la CPU.  

---

## basic ocr python – cargar imagen y reconocer texto

Lo primero que debemos hacer es **cargar imagen OCR** para que el motor pueda leer los píxeles. El `OcrEngine` de Aspose maneja muchos formatos, pero aquí nos centramos en TIFF porque es el más común para facturas escaneadas.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Consejo profesional:** Si trabajas con TIFF de varias páginas, Aspose procesa automáticamente cada página en secuencia, por lo que no necesitas bucles adicionales.

Una vez que la imagen está cargada, ejecutemos una pasada básica de reconocimiento.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Verás algo como:

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

¿Notas los *ceros* antes de las letras? Ese es un artefacto clásico del OCR que limpiaremos más adelante.

![flujo de trabajo de basic ocr python](/images/ocr-workflow.png "diagrama del flujo de trabajo de basic ocr python")

---

## Paso 2: Convertir TIFF a texto – preparar el post‑procesador de IA

El OCR crudo es útil, pero la mayoría de los pipelines de producción necesitan una versión pulida. Aspose ofrece un wrapper `AsposeAI` que puede descargar un modelo desde Hugging Face, ejecutarlo en la GPU y aplicar corrección ortográfica automáticamente.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Por qué importa `establecer capas GPU`

El parámetro `gpu_layers` indica al modelo GGUF subyacente cuántas capas del transformador mantener en la GPU. Más capas = inferencia más rápida pero mayor consumo de VRAM. Si usas un portátil modesto, reduce el valor a `10` o elimínalo por completo para quedarte en la CPU.

---

## Paso 3: Aplicar corrección ortográfica y **corregir ceros iniciales**

Aspose AI incluye un corrector ortográfico incorporado, que detecta la mayoría de los errores en inglés. Sin embargo, correcciones específicas del dominio—como transformar un `0` inicial en una `O` para códigos de factura—requieren un post‑procesador personalizado.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Por qué funciona:** La expresión regular busca un límite de palabra (`\b`), un cero y luego exactamente tres letras mayúsculas. Luego sustituye el cero por la letra “O”. Puedes ampliar el patrón para otras particularidades (p. ej., `0[0-9]{2}` para números mal leídos).

---

## Paso 4: Limpiar el resultado OCR con el post‑procesador de IA

Ahora combinamos todo: la cadena cruda de **basic ocr python**, la corrección ortográfica y nuestra corrección de ceros. El método `run_postprocessor` devuelve una versión limpiada lista para los sistemas posteriores.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Salida típica después del post‑procesador:

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Puedes ver que el cero inicial se ha convertido en una `O`, y los errores ortográficos comunes están corregidos. El texto ya es apto para indexarse en un motor de búsqueda o alimentarse a una canalización de extracción de datos.

---

## Paso 5: Liberar recursos de IA – mantener feliz a tu GPU

Si ejecutas múltiples trabajos OCR en un servicio de larga duración, es buena práctica liberar la memoria GPU del modelo cuando termines.

```python
ocr_ai.free_resources()
```

Omitir este paso puede provocar errores de “out‑of‑memory” en llamadas posteriores, especialmente cuando **estableces capas GPU** a un valor alto.

---

## Variaciones opcionales y casos límite

| Situación | Qué cambiar |
|-----------|-------------|
| **Documentos manuscritos** | Usa `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` en lugar de `PRINTED`. |
| **Sin GPU disponible** | Establece `gpu_layers=0` o omite el argumento; el modelo se ejecutará en CPU (más lento pero seguro). |
| **Idioma diferente** | Cambia el ID del repositorio de Hugging Face a un modelo específico del idioma, por ejemplo `microsoft/Florence-2-base`. |
| **Procesamiento por lotes** | Envuelve los pasos en un bucle `for file in glob("*.tif"):` y acumula los resultados en una lista o CSV. |
| **Patrones de ceros más complejos** | Amplía `invoice_fix` con expresiones regulares adicionales, como `r"\b0+([A-Z]{2,})\b"` para varios ceros iniciales. |

---

## Conclusión

Acabamos de completar una pipeline de **basic ocr python** que carga un TIFF, extrae texto crudo y luego lo limpia usando un modelo de IA mientras **establece capas GPU** para mejorar el rendimiento. El post‑procesador personalizado muestra cómo **corregir ceros iniciales**, un detalle pequeño pero a menudo pasado por alto que puede romper análisis posteriores.

Siéntete libre de experimentar: prueba una cuantización diferente (`float16` para mayor precisión), sustituye la corrección ortográfica por un diccionario específico del dominio, o encadena varias correcciones personalizadas. El patrón sigue siendo el mismo—cargar, reconocer, configurar IA, post‑procesar y limpiar.

**Próximos pasos** que podrías explorar incluyen:

- Integrar la salida limpia con una base de datos o un índice de Elasticsearch.  
- Usar el mismo enfoque para **convertir TIFF a texto** en PDFs multilingües.  
- Añadir una interfaz UI con Flask o FastAPI para que usuarios no técnicos puedan subir archivos y recibir texto limpio al instante.  

¡Feliz codificación, y que tus resultados OCR siempre sean nítidos y sin ceros!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}