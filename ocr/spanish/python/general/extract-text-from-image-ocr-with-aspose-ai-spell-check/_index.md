---
category: general
date: 2026-05-03
description: extraer texto de una imagen usando Aspose OCR y corrección ortográfica
  con IA. aprende cómo hacer OCR a una imagen, cargar la imagen para OCR, reconocer
  texto de una factura y liberar los recursos de GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: es
og_description: extrae texto de una imagen con Aspose OCR y corrección ortográfica
  AI. Guía paso a paso que cubre cómo hacer OCR a una imagen, cargar la imagen para
  OCR y liberar los recursos de GPU.
og_title: extraer texto de una imagen – Guía completa de OCR y corrección ortográfica
tags:
- OCR
- Aspose
- AI
- Python
title: extraer texto de una imagen – OCR con Aspose AI Spell‑Check
url: /es/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraer texto de imagen – Guía completa de OCR y corrección ortográfica

¿Alguna vez necesitaste **extraer texto de imagen** pero no estabas seguro de qué biblioteca te ofrecería tanto velocidad como precisión? No eres el único. En muchos proyectos del mundo real —piense en procesamiento de facturas, digitalización de recibos o escaneo de contratos— obtener texto limpio y buscable a partir de una foto es el primer obstáculo.

La buena noticia es que Aspose OCR combinado con un modelo ligero de Aspose AI puede manejar esa tarea en unas pocas líneas de Python. En este tutorial recorreremos **cómo hacer OCR a una imagen**, cargaremos la foto correctamente, ejecutaremos un post‑procesador de corrección ortográfica incorporado y, finalmente, **liberaremos los recursos de GPU** para que tu aplicación sea amigable con la memoria.

Al final de esta guía podrás **reconocer texto de facturas** en imágenes, corregir automáticamente errores comunes de OCR y mantener tu GPU limpia para el siguiente lote.

---

## Lo que necesitarás

- Python 3.9 o superior (el código usa anotaciones de tipo pero funciona en versiones 3.x anteriores)
- paquetes `aspose-ocr` y `aspose-ai` (instalar mediante `pip install aspose-ocr aspose-ai`)
- Una GPU con soporte CUDA es opcional; el script recurrirá a la CPU si no se detecta ninguna.
- Una imagen de ejemplo, por ejemplo `sample_invoice.png`, ubicada en una carpeta a la que puedas hacer referencia.

Sin frameworks de ML pesados, sin descargas masivas de modelos —solo un pequeño modelo cuantizado Q4‑K‑M que cabe cómodamente en la mayoría de las GPUs.

---

## Paso 1: Inicializar el motor OCR – extraer texto de imagen

Lo primero que haces es crear una instancia de `OcrEngine` y especificar el idioma que esperas. Aquí elegimos inglés y solicitamos salida en texto plano, lo cual es ideal para el procesamiento posterior.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Por qué es importante:** Establecer el idioma reduce el conjunto de caracteres, mejorando la precisión. El modo de texto plano elimina la información de diseño que normalmente no necesitas cuando solo deseas extraer texto de una imagen.

---

## Paso 2: Cargar imagen para OCR – cómo hacer OCR a una imagen

Ahora alimentamos al motor con una imagen real. El asistente `Image.load` reconoce formatos comunes (PNG, JPEG, TIFF) y abstrae las peculiaridades de la entrada/salida de archivos.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Consejo:** Si tus imágenes de origen son grandes, considera redimensionarlas antes de enviarlas al motor; dimensiones más pequeñas pueden reducir el uso de memoria de la GPU sin perjudicar la calidad del reconocimiento.

---

## Paso 3: Configurar el modelo Aspose AI – reconocer texto de facturas

Aspose AI incluye un pequeño modelo GGUF que puedes descargar automáticamente. El ejemplo usa el repositorio `Qwen2.5‑3B‑Instruct‑GGUF`, cuantizado a `q4_k_m`. También indicamos al tiempo de ejecución que asigne 20 capas en la GPU, lo que equilibra velocidad y uso de VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Detrás de cámaras:** El modelo cuantizado ocupa aproximadamente 1.5 GB en disco, una fracción de un modelo de precisión completa, pero aún captura suficiente matiz lingüístico para detectar errores típicos de OCR.

---

## Paso 4: Inicializar AsposeAI y adjuntar el post‑procesador de corrección ortográfica

Aspose AI incluye un post‑procesador de corrección ortográfica listo para usar. Al adjuntarlo, cada resultado de OCR se limpiará automáticamente.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**¿Por qué usar el post‑procesador?** Los motores OCR a menudo leen “Invoice” como “Invo1ce” o “Total” como “T0tal”. La corrección ortográfica ejecuta un modelo de lenguaje ligero sobre la cadena cruda y corrige esos errores sin que tengas que escribir un diccionario personalizado.

---

## Paso 5: Ejecutar el post‑procesador de corrección ortográfica sobre el resultado OCR

Con todo conectado, una sola llamada produce el texto corregido. También imprimimos tanto la versión original como la limpiada para que puedas ver la mejora.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Una salida típica para una factura podría verse así:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Observa cómo “Invo1ce” se convirtió en la palabra correcta “Invoice”. Ese es el poder de la corrección ortográfica AI incorporada.

---

## Paso 6: Liberar recursos de GPU – liberar recursos de GPU de forma segura

Si ejecutas esto en un servicio de larga duración (por ejemplo, una API web que procesa decenas de facturas por minuto), debes liberar el contexto de GPU después de cada lote. De lo contrario verás fugas de memoria y eventualmente obtendrás errores de “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Consejo profesional:** Llama a `free_resources()` dentro de un bloque `finally` o un gestor de contexto para que siempre se ejecute, incluso si ocurre una excepción.

---

## Ejemplo completo funcional

Unir todas las piezas te brinda un script autocontenido que puedes incorporar en cualquier proyecto.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Guarda el archivo, ajusta la ruta a tu imagen y ejecuta `python extract_text_from_image.py`. Deberías ver el texto de la factura limpiado impreso en la consola.

---

## Preguntas frecuentes (FAQ)

**Q: ¿Funciona en máquinas solo CPU?**  
A: Absolutamente. Si no se detecta GPU, Aspose AI recurre a la ejecución en CPU, aunque será más lento. Puedes forzar la CPU estableciendo `model_cfg.gpu_layers = 0`.

**Q: ¿Qué pasa si mis facturas están en un idioma distinto al inglés?**  
A: Cambia `ocr_engine.language` al valor enum apropiado (por ejemplo, `aocr.Language.Spanish`). El modelo de corrección ortográfica es multilingüe, pero puedes obtener mejores resultados con un modelo específico para el idioma.

**Q: ¿Puedo procesar múltiples imágenes en un bucle?**  
A: Sí. Simplemente mueve los pasos de carga, reconocimiento y post‑procesamiento dentro de un bucle `for`. Recuerda llamar a `ocr_ai.free_resources()` después del bucle o después de cada lote si reutilizas la misma instancia AI.

**Q: ¿Qué tamaño tiene la descarga del modelo?**  
A: Aproximadamente 1.5 GB para la versión cuantizada `q4_k_m`. Se almacena en caché después de la primera ejecución, por lo que ejecuciones posteriores son instantáneas.

---

## Conclusión

En este tutorial demostramos cómo **extraer texto de imagen** usando Aspose OCR, configurar un pequeño modelo AI, aplicar un post‑procesador de corrección ortográfica y liberar de forma segura los **recursos de GPU**. El flujo de trabajo cubre todo, desde cargar la foto hasta limpiar después de ti, brindándote una canalización confiable para escenarios de **reconocer texto de facturas**.

¿Próximos pasos? Intenta reemplazar la corrección ortográfica por un modelo personalizado de extracción de entidades

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}