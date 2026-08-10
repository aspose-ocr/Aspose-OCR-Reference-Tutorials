---
category: general
date: 2026-02-25
description: Reconocer texto de una imagen rápidamente usando OCR acelerado por GPU.
  Aprende a configurar el modo GPU, cargar la imagen para OCR y extraer texto de un
  TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: es
og_description: Reconoce texto de una imagen al instante usando OCR acelerado por
  GPU. Tutorial paso a paso en C# que cubre cómo establecer el modo GPU, cargar la
  imagen para OCR y extraer texto de un TIFF.
og_title: Reconocer texto de imagen con OCR acelerado por GPU – Guía C#
tags:
- Aspose OCR
- C#
- GPU computing
title: Reconocer texto de una imagen usando OCR acelerado por GPU en C#
url: /es/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

Let's write it.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconocer texto de imagen usando OCR acelerado por GPU en C#

¿Alguna vez necesitaste **reconocer texto de una imagen** pero tu CPU se quedaba sin aliento con un escaneo de alta resolución? No estás solo. En muchos proyectos del mundo real —piense en la digitalización de facturas o el archivo de periódicos antiguos— un solo archivo TIFF puede detener tu canal de procesamiento durante minutos. ¿La buena noticia? Aspose.OCR te permite activar un interruptor y delegar el trabajo pesado a tu GPU, convirtiendo una operación lenta en una casi instantánea.

En este tutorial recorreremos todo el proceso: cómo **establecer el modo GPU**, cómo **cargar la imagen para OCR**, y cómo **extraer texto de archivos TIFF**. Al final tendrás un ejemplo autónomo, listo para producción, que puedes incorporar en cualquier proyecto .NET 6+.

## Requisitos

Antes de comenzar, asegúrate de tener:

- .NET 6 SDK (o posterior) instalado.  
- Visual Studio 2022 o cualquier editor que prefieras.  
- Un paquete NuGet de Aspose.OCR (`Aspose.OCR`) añadido a tu proyecto.  
- Una GPU que soporte DirectX 11 o posterior (la mayoría de GPUs modernas lo cumplen).  
  *Si no dispones de una GPU, aún puedes ejecutar el código con `GpuMode.Auto`; la biblioteca volverá automáticamente a la CPU.*

> **Consejo profesional:** Verifica que el controlador de tu GPU esté actualizado; los controladores obsoletos pueden provocar errores de inicialización difíciles de diagnosticar.

## Paso 1 – Crear el motor OCR y establecer el modo GPU

Lo primero que necesitas es una instancia de `OcrEngine`. Este objeto contiene toda la configuración, incluido si el motor debe usar la GPU.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Por qué es importante:** Activar el modo GPU traslada el preprocesamiento de imágenes intensivo en cómputo (binarización, eliminación de ruido, etc.) a la tarjeta gráfica. En una RTX 3060 de gama media, puedes observar un **incremento de velocidad de 3‑5×** comparado con el procesamiento puro en CPU.

## Paso 2 – Cargar imagen para OCR (ejemplo TIFF)

Aspose.OCR acepta muchos formatos, pero TIFF es común para documentos escaneados porque conserva calidad sin pérdidas. Usa `ImageStream.FromFile` para leer el archivo en memoria.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Caso límite:** Algunos archivos TIFF contienen varias páginas. `ImageStream.FromFile` leerá solo la primera página. Si necesitas procesar todas, recorre `ImageInfo.Pages` y pasa cada una al motor por separado.

## Paso 3 – Realizar el reconocimiento

Ahora que el motor está configurado y la imagen cargada, llama a `Recognize()`. El método devuelve un objeto `OcrResult` que contiene el texto plano y metadatos adicionales.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**¿Qué hacer si el texto se ve distorsionado?**  
- Asegúrate de que la imagen esté en una orientación legible (rota si es necesario).  
- Ajusta opciones de preprocesamiento como `ocrEngine.Config.DeskewEnabled = true;`.  
- Para documentos multilingües, establece `ocrEngine.Config.Language = Language.English;` o el enum correspondiente.

## Paso 4 – Verificar la salida y manejar errores

Una implementación robusta verifica resultados nulos y captura posibles excepciones (p. ej., controladores de GPU faltantes).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**¿Por qué envolverlo?** La inicialización de la GPU puede lanzar `DllNotFoundException` si las bibliotecas nativas requeridas no están presentes. El bloque `catch` te brinda una vía de degradación elegante.

## Ejemplo completo y ejecutable

Juntándolo todo, aquí tienes un programa completo que puedes compilar y ejecutar ahora mismo. Sustituye la ruta del archivo por un TIFF real en tu máquina.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Salida esperada**

Si el TIFF contiene texto legible en inglés, verás algo como:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

Si la imagen está en blanco o es ilegible, la consola te aconsejará revisar el archivo de origen.

## Preguntas frecuentes y variaciones

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo procesar JPEG o PNG en lugar de TIFF?** | Por supuesto. `ImageStream.FromFile` funciona con cualquier formato que Aspose.OCR admita (PNG, JPEG, BMP, etc.). |
| **¿Qué pasa si tengo varias páginas en un TIFF?** | Recorre `ImageInfo.Pages` y asigna cada página a `ocrEngine.Image` antes de llamar a `Recognize()`. |
| **¿Necesito una licencia para Aspose.OCR?** | Una evaluación gratuita funciona hasta 100 páginas. Para producción, adquiere una licencia para eliminar la marca de agua de evaluación. |
| **¿Cómo cambio el modelo de idioma?** | Establece `ocrEngine.Config.Language = Language.Spanish;` (o cualquier enum soportado). |
| **¿Hay forma de obtener puntuaciones de confianza?** | Habilita `ocrEngine.Config.EnableConfidence = true;` y revisa `result.Confidence` por línea. |

## Conclusión

Ahora sabes cómo **reconocer texto de una imagen** usando una **pipeline OCR acelerada por GPU** en C#. Al **establecer el modo GPU**, **cargar una imagen para OCR** y **extraer texto de archivos TIFF**, has creado una solución rápida y escalable lista para cargas de trabajo del mundo real.

¿Próximos pasos? Prueba encadenar este código con un generador de PDF para crear PDFs buscables, o alimenta las cadenas extraídas a una canalización de procesamiento de lenguaje natural. También puedes experimentar con `GpuMode.Auto` para que tu aplicación se adapte a entornos sin GPU.

¡Feliz codificación, y que tus ejecuciones de OCR sean relámpago!

![ejemplo de reconocimiento de texto de imagen](https://example.com/ocr-demo.png "reconocimiento de texto de imagen usando OCR acelerado por GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}