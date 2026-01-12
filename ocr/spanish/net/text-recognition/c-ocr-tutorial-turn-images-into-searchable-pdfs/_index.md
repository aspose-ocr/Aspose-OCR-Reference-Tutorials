---
category: general
date: 2026-01-12
description: Tutorial de OCR en C# que muestra cómo reconocer imágenes de texto, extraer
  texto de imágenes en C# y generar un archivo OCR de imagen a PDF con puntuaciones
  de confianza.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: es
og_description: Aprende un tutorial completo de OCR en C# para reconocer imágenes
  de texto, extraer texto de imágenes con C# y crear un documento OCR de imagen a
  PDF con puntuaciones de confianza.
og_title: tutorial de OCR en C# – Convertir imágenes a PDFs buscables
tags:
- OCR
- C#
- PDF
title: c# tutorial OCR – Convierte imágenes en PDFs buscables
url: /es/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Convierte imágenes en PDFs buscables

¿Alguna vez te has preguntado cómo **reconocer texto en imágenes** en un proyecto C# sin buscar servicios de terceros? No estás solo. En muchas aplicaciones del mundo real—piensa en escáneres de facturas, rastreadores de recibos o archivos de documentos multilingües—los desarrolladores necesitan un motor OCR confiable, local, que también proporcione puntuaciones de confianza.  

Este **c# ocr tutorial** te guiará paso a paso por todo lo que necesitas: desde cargar una imagen, seleccionar modelos de idioma, activar la aceleración GPU, hasta guardar el resultado como un PDF buscable. Al final tendrás un ejemplo de código listo‑para‑ejecutar que extrae texto, informa la confianza del OCR y, opcionalmente, crea un archivo *image to pdf ocr*, todo en menos de un minuto de codificación.

## Qué construir

- Cargar una imagen multilingüe (`sample_multi_lang.jpg` se usa como marcador de posición).  
- Seleccionar los modelos de idioma Árabe, Hindi y Ruso (puedes añadir más).  
- Activar el procesamiento GPU si tu máquina lo soporta.  
- Obtener el resultado OCR sin procesar **con puntuaciones de confianza**.  
- Serializar el resultado a JSON con formato **o** escribir un PDF buscable.  

## Requisitos previos

- .NET 6.0 o posterior (el código compila en .NET Core y .NET Framework).  
- Visual Studio 2022 (o cualquier IDE que prefieras).  
- Una licencia de Aspose.OCR para .NET (la prueba gratuita funciona para pruebas).  
- Opcional: una GPU compatible con CUDA si deseas acelerar el reconocimiento.

> **Consejo profesional:** Si no tienes una GPU, simplemente establece `UseGpu = false` y el motor volverá a usar la CPU sin cambios en el código.

## Paso 1: Instala los paquetes NuGet requeridos

Abre la **Package Manager Console** y ejecuta:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Estos tres paquetes te proporcionan el motor OCR, la aceleración GPU y un buen serializador JSON para la salida de confianza.

## Paso 2: Configura la estructura del proyecto

Crea un nuevo proyecto de consola (`dotnet new console -n AsposeOcrDemo`) y reemplaza el `Program.cs` generado con el código a continuación.  
Toda la lógica reside dentro de la clase `Program`; el único tipo adicional es un pequeño método de extensión que formatea el resultado OCR para JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Por qué funciona este código

1. **Alternar GPU** – `GpuOcrEngine` aprovecha los núcleos CUDA; el operador ternario hace que el cambio sea sencillo.  
2. **Descarga automática de idiomas** – `AutoDownloadResources = true` garantiza que los modelos de Árabe, Hindi y Ruso se descarguen la primera vez que ejecutes la aplicación.  
3. **Puntuaciones de confianza** – `result.Words` contiene un `Confidence` para cada palabra reconocida; el método de extensión los formatea en un objeto JSON limpio.  
4. **PDF buscable** – `result.Pdf` ya es un PDF completamente buscable, así que simplemente escribimos el arreglo de bytes en disco. No se necesitan bibliotecas adicionales.

## Paso 6: Ejecuta el ejemplo

Abre una terminal, navega a la carpeta del proyecto y ejecuta:

```bash
dotnet run
```

Si elegiste la salida **JSON**, verás algo como:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Si cambiaste a **PDF**, la consola muestra la ruta y encontrarás un PDF buscable justo al lado de la imagen fuente.

## Preguntas frecuentes y casos límite

- **¿Qué pasa si un modelo de idioma no está disponible?**  
  El motor OCR lanza una clara `ResourceNotFoundException`. Como hemos configurado `AutoDownloadResources = true`, el modelo faltante se descarga automáticamente la primera vez, por lo que la excepción rara vez aparece en producción.

- **¿Puedo procesar un lote de imágenes?**  
  Por supuesto. Envuelve la llamada `engine.Recognize` en un bucle `foreach` sobre un directorio de archivos. El mismo `OcrResultExtensions` funciona para cada imagen.

- **¿Necesito una licencia para GPU?**  
  No. La prueba gratuita funciona tanto para CPU como para GPU. Una licencia completa elimina la marca de agua de prueba y levanta las restricciones de límite de páginas.

- **¿Qué tan precisas son las puntuaciones de confianza?**  
  Las puntuaciones van de 0.0 (sin confianza) a 1.0 (confianza perfecta). En la práctica, cualquier valor superior a 0.90 es fiable para el procesamiento posterior; puedes filtrar palabras con menor confianza si necesitas una validación más estricta.

## Paso 7: Próximos pasos (Amplía tu kit de herramientas OCR)

1. **Añadir más idiomas** – simplemente agrega `LanguageModel.French` (o cualquier modelo soportado) al arreglo `Languages`.  
2. **Combinar OCR con conversión PDF/A** – Aspose.PDF puede incrustar la capa OCR en un documento compatible con PDF/A‑2b para archivado.  
3. **Integrar con Azure Functions** – envuelve la lógica en un endpoint sin servidor para procesar cargas al instante.  
4. **Ajustar los umbrales de confianza** – usa `result.Words.Where(w => w.Confidence < 0.85)` para marcar palabras inciertas para revisión manual.

### TL;DR

Este **c# ocr tutorial** te muestra cómo:

- Cargar una imagen y seleccionar varios modelos de idioma.  
- Activar la aceleración GPU con una única bandera booleana.  
- Recuperar resultados OCR **con puntuaciones de confianza** y serializarlos a JSON.  
- Opcionalmente generar un PDF buscable (**image to pdf ocr**).  

Todo eso es posible con solo unas cuantas líneas, una prueba gratuita de Aspose.OCR y el código anterior. Pruébalo, ajusta la lista de idiomas y tendrás una canalización OCR lista para producción en minutos.

---

![imagen de ejemplo del tutorial c# ocr](https://example.com/placeholder-image.jpg "imagen de ejemplo del tutorial c# ocr")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}