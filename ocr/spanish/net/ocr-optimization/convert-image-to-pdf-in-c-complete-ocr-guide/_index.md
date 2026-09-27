---
category: general
date: 2026-09-13
description: Aprenda cómo convertir una página escaneada a PDF en C# usando Aspose
  OCR. Esta guía muestra el preprocesamiento, el reconocimiento de texto coreano y
  la creación de un PDF searchable.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Aprenda cómo convertir una página escaneada a PDF en C# con Aspose
  OCR. El tutorial cubre el preprocesamiento de imágenes, OCR acelerado por GPU para
  texto coreano y la generación de un PDF searchable en minutos.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Cómo convertir una página escaneada a PDF en C# con OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Cómo convertir una página escaneada a PDF en C# con OCR
url: /es/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo convertir una página escaneada a PDF en C# con OCR

Si necesitas **convertir una página escaneada a PDF** manteniendo el texto buscable, estás en el lugar correcto. Este tutorial te guía a través del uso de Aspose OCR para **preprocess image for OCR**, **recognize Korean text image**, y finalmente **create searchable PDF image** – todo desde una sencilla aplicación de consola en C#.

## Respuestas rápidas
- **¿Qué biblioteca maneja OCR?** Aspose.OCR for .NET  
- **¿Puedo usar la GPU?** Sí – habilita la aceleración GPU para un procesamiento hasta 2× más rápido  
- **¿Necesito un paquete de idioma coreano?** Se descarga automáticamente en el primer uso  
- **¿El resultado será buscable?** El PDF generado contiene una capa de texto invisible  
- **¿Qué versiones de .NET son compatibles?** .NET 6.0 y posteriores (incluyendo .NET Core y .NET Framework)

## Requisitos

- **.NET 6.0 o posterior** – funciona en .NET Core, .NET Framework y .NET 5/6+  
- **Aspose.OCR for .NET** paquete NuGet (`Aspose.OCR`) – las claves de prueba son gratuitas en el sitio de Aspose  
- Una imagen de muestra con caracteres coreanos, por ejemplo, `korean_book_page.jpg`  
- Tu IDE favorito (Visual Studio 2022, VS Code, Rider, etc.)

> **Consejo profesional:** Guarda las imágenes en una carpeta `Resources/` para que las rutas permanezcan consistentes entre máquinas.

## Visión general del proceso

1. Inicializa el motor OCR con soporte GPU.  
2. Añade filtros de **preprocess image for OCR** como deskew y denoise.  
3. Descarga y carga el modelo de idioma coreano (manejado automáticamente).  
4. Ejecuta el OCR sobre la imagen.  
5. Exporta el resultado con **SearchablePdfExporter** para **create searchable PDF image**.  
6. (Opcional) Serializa la salida OCR a JSON para canalizaciones posteriores.

A continuación ampliamos cada paso, explicamos *por qué* es importante y te damos el código exacto que puedes copiar y pegar.

## ¿Cómo funciona la conversión de página escaneada a PDF?

`OcrEngine` es la clase principal en Aspose.OCR que realiza reconocimiento óptico de caracteres en imágenes.  
`SearchablePdfExporter` crea un PDF que contiene la imagen original y una capa de texto invisible para búsqueda.  
`RecognitionResult` contiene el texto y los datos de confianza devueltos por el motor OCR.

Carga tu imagen con `new OcrEngine()` y llama a `engine.Recognize("korean_book_page.jpg")`, luego pasa el `RecognitionResult` a `SearchablePdfExporter.Export`. Este flujo de dos pasos lee el bitmap, extrae texto Unicode y los incrusta ambos en un único PDF donde la capa de texto es invisible pero buscable. La aceleración GPU reduce el tiempo de reconocimiento aproximadamente a la mitad, mientras que los filtros deskew y denoise aumentan la precisión hasta un 15 % en escaneos ruidosos.

## Convertir imagen a PDF – flujo completo

El siguiente fragmento es el programa *completo*. Crea un nuevo proyecto de consola (`dotnet new console -n OcrPdfDemo`) y reemplaza el `Program.cs` autogenerado con el código mostrado en el marcador de posición.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Por qué funciona esto

- **Aceleración GPU** reduce el tiempo de reconocimiento aproximadamente a la mitad comparado con el modo solo CPU.  
- **Deskew** y **Denoise** son técnicas clásicas de *preprocess image for OCR*; corrigen defectos de escaneo comunes que de otro modo hacen que el motor omita caracteres.  
- **Carga del modelo de idioma** es esencial para **recognize Korean text image** – sin el modelo coreano el motor recurriría a un alfabeto latino genérico y produciría basura.  
- El **SearchablePdfExporter** combina el bitmap original y una superposición de texto invisible, dándote un resultado de **create searchable pdf image** que puedes indexar en cualquier visor de PDF.

## Por qué funciona esto

- **Aceleración GPU** reduce el tiempo de reconocimiento aproximadamente a la mitad comparado con el modo solo CPU.  
- **Deskew** y **Denoise** son técnicas clásicas de *preprocess image for OCR*; corrigen defectos de escaneo comunes que de otro modo hacen que el motor omita caracteres.  
- **Carga del modelo de idioma** es esencial para **recognize Korean text image** – sin el modelo coreano el motor recurriría a un alfabeto latino genérico y produciría basura.  
- El **SearchablePdfExporter** combina el bitmap original y una superposición de texto invisible, dándote un resultado de **create searchable pdf image** que puedes indexar en cualquier visor de PDF.

## Preprocess image for OCR – consejos y trucos

`DeskewFilter` corrige la rotación de las páginas escaneadas.  
`ContrastFilter` ajusta el contraste de la imagen para mejorar la precisión del OCR.  
`BinarizationFilter` convierte la imagen a blanco y negro basado en un umbral, reduciendo el ruido de fondo.  
`OrientationFilter` detecta y corrige páginas con orientación mixta (retrato y paisaje).  

| Problema | Filtro adicional | Cómo añadir |
|----------|------------------|--------------|
| Bajo contraste | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Ruido de fondo intenso | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Orientación mixta (retrato y paisaje) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Nota:** Añadir demasiados filtros puede ralentizar el procesamiento. Prueba cada cambio en una sola página antes de escalar.

## Recognize Korean text image – problemas comunes

Los guiones coreanos contienen sílabas Hangul que son visualmente densas. Si notas una salida distorsionada:

1. **Asegúrate de que el modelo de idioma esté completamente descargado** – verifica la consola para un mensaje como “Downloading Korean model…”.  
2. **Incrementa el `MaxAngle`** en `DeskewFilter` si tus escaneos están rotados más de 12°.  
3. **Aumenta la memoria GPU** estableciendo `ocrEngine.GpuMemoryLimit = 2048;` (valor en MB).  

`LanguageModel.Korean` carga los datos del idioma coreano para OCR, permitiendo un reconocimiento preciso de Hangul.  

Estos ajustes influyen directamente en el éxito de **recognize Korean text image**.

## Create searchable PDF image – verificando el resultado

Después de que el programa termine, abre `korean_page.pdf` en cualquier lector de PDF (Adobe Acrobat Reader, Foxit, incluso Chrome). Deberías poder:

- **Seleccionar texto** con el ratón como si fuera un PDF nativo.  
- **Buscar** palabras coreanas usando el cuadro de búsqueda incorporado.  

Si la capa de texto aparece en blanco, verifica que el método `Export` haya recibido la ruta de imagen correcta y que el resultado OCR contenga un `RecognitionResult.Text` no vacío.

## Salida JSON completa – qué esperar

La consola imprime una carga JSON bien formateada. Un ejemplo recortado se ve así:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Solución de problemas y preguntas frecuentes

**Q: My PDF is huge compared to the original image.**  
R: El exportador incrusta el bitmap original a su resolución nativa. Si el tamaño es un problema, reduce la escala de la imagen *antes* del reconocimiento:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: The OCR returns empty strings.**  
R: Verifica que la ruta de la imagen sea correcta y que el archivo no esté corrupto. Además, asegúrate de que el controlador GPU esté actualizado; los controladores antiguos pueden causar fallas silenciosas.

**Q: Can I process multiple pages in a loop?**  
R: Por supuesto. Envuelve los pasos 4‑6 en un bucle `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` y cambia la ruta del PDF de salida en consecuencia.

## Conclusión

Acabamos de **convertir imagen a PDF** mientras preservamos texto buscable, todo gracias a la potente canalización de Aspose OCR. Al **preprocess image for OCR**, aumentas la precisión; al **recognize Korean text image**, manejas scripts complejos; y al **create searchable pdf image**, obtienes un documento portátil e indexable.

Obtén el código, apúntalo a tus propios escaneos y experimenta con filtros o modelos de idioma adicionales. El mismo patrón funciona para chino, japonés o cualquier idioma basado en alfabeto latino—simplemente cambia `LanguageModel.Korean` por el enum correspondiente.

¿Tienes más preguntas? Deja un comentario, ¡y feliz codificación!

---

**Last Updated:** 2026-09-13  
**Tested with:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose

## Tutoriales relacionados

- [Crear PDF buscable a partir de archivos escaneados usando Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline de preprocesamiento OCR: cómo reconocer texto de una imagen](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Reconocer texto de una imagen con Aspose Ocr Guía completa en C](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}