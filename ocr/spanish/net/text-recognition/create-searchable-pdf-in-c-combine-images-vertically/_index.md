---
category: general
date: 2026-02-28
description: Crear PDF buscable en C# combinando imágenes verticalmente. Aprende a
  apilar imágenes verticalmente y convertir páginas escaneadas a PDF con Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: es
og_description: Crear PDF buscable en C# combinando imágenes verticalmente. Esta guía
  muestra cómo apilar imágenes verticalmente y convertir páginas escaneadas a PDF
  usando Aspose OCR.
og_title: Crear PDF buscable en C# – Combinar imágenes verticalmente
tags:
- Aspose OCR
- C#
- PDF generation
title: Crear PDF buscable en C# – Combinar imágenes verticalmente
url: /es/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF buscable en C# – Combinar imágenes verticalmente

¿Alguna vez necesitaste **create searchable PDF** a partir de un puñado de PNG escaneados pero no sabías por dónde empezar? No estás solo. En muchos proyectos de automatización de documentos, el mayor dolor es convertir una pila de archivos de imagen en un PDF ordenado y buscable que puedas indexar y compartir.  

En este tutorial recorreremos un ejemplo completo, listo para ejecutar, que te muestra **cómo apilar imágenes verticalmente**, **combinar imágenes verticalmente**, y finalmente **convert scanned pages PDF** en un solo documento buscable usando el motor acelerado por GPU de Aspose.OCR. Al final tendrás un programa autónomo que puedes insertar en cualquier solución .NET.

> **Qué aprenderás**
> - Inicializar un motor OCR con soporte GPU.
> - Procesar un lote de imágenes en paralelo.
> - **Combine images vertically** para imitar un escaneo de varias páginas.
> - Exportar un PDF buscable y un informe JSON detallado para análisis posteriores.

## Requisitos previos

- .NET 6+ (el código compila con .NET 6, .NET 7 o .NET 8)
- Paquete NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Una máquina con GPU habilitada si deseas mantener la configuración `ProcessingMode.Gpu` (el fallback a CPU también funciona)
- Una carpeta con algunos archivos PNG/JPEG escaneados (el demo usa `page1.png`, `page2.png`, `page3.png`)

Sin servicios externos, sin archivos de configuración ocultos—solo C# puro.

## Paso 1 – Configurar el motor OCR para **Create Searchable PDF**

Primero creamos un `OcrEngine`, activamos la aceleración GPU, elegimos inglés como idioma y añadimos un par de filtros de preprocesamiento. Estos filtros mejoran la precisión al enderezar páginas inclinadas (`DeskewFilter`) y eliminar ruido (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Por qué esto importa:** El motor OCR realiza el trabajo pesado de reconocer texto. Habilitar `ProcessingMode.Gpu` puede reducir a la mitad el tiempo de reconocimiento en una tarjeta gráfica moderna, mientras que los filtros reducen artefactos comunes de escaneo que de otro modo producirían una salida ilegible.

## Paso 2 – Configurar un procesador por lotes para **Convert Scanned Pages PDF** de forma eficiente

Procesar cada página una por una está bien para un par de imágenes, pero los proyectos del mundo real a menudo involucran decenas o cientos de páginas. `OcrBatchProcessor` de Aspose.OCR nos permite ejecutar reconocimientos en paralelo, acelerando drásticamente el paso **convert scanned pages pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Consejo profesional:** Si estás en una máquina solo CPU, establece `ProcessingMode = ProcessingMode.Cpu`. El procesador por lotes seguirá respetando `MaxDegreeOfParallelism`, por lo que puedes ajustarlo para evitar sobrecargar la máquina.

## Paso 3 – Ejecutar OCR en el lote y recopilar resultados

Ahora reconocemos realmente el texto. El método `Recognize` devuelve una lista de objetos `OcrResult`, cada uno contiene tanto la imagen original como el texto extraído.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

En este punto tienes todo lo necesario para **create searchable PDF**: las imágenes (todavía en memoria) y las capas de texto asociadas.

## Paso 4 – **Combine Images Vertically** y generar el PDF buscable

La mayoría de los documentos escaneados son PDFs de varias páginas, por lo que necesitamos unir las imágenes de cada página en una sola imagen alta que refleje una pila física. Aspose.OCR ofrece `Image.CombineVertical` para exactamente ese propósito.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

El archivo resultante (`combined_searchable.pdf`) contiene texto seleccionable y buscable debajo de cada imagen de página—exactamente lo que necesitas para **create searchable PDF** a partir de fuentes escaneadas.

![Ejemplo de crear PDF buscable](/images/create-searchable-pdf.png "ejemplo de crear pdf buscable")

*Texto alternativo de la imagen: ejemplo de crear pdf buscable que muestra un PDF combinado con texto buscable.*

**¿Por qué apilar verticalmente?** Muchas bibliotecas OCR tratan cada imagen como una página separada. Al apilarlas, mantenemos el orden de páginas del PDF intacto mientras aprovechamos una sola pasada OCR para todo el documento.

## Paso 5 – Exportar JSON detallado para la primera página (Ideal para flujos de trabajo posteriores)

A veces necesitas más que un PDF; quizás quieras alimentar los datos OCR a una base de datos o a una canalización de aprendizaje automático. Aspose.OCR permite serializar cada `OcrResult` a JSON, preservando cajas delimitadoras, puntuaciones de confianza y más.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Fragmento JSON esperado (truncado):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Ahora puedes enviar este JSON a cualquier sistema posterior—ya sea que estés indexando el texto en Elasticsearch o alimentándolo a un panel de análisis personalizado.

---

## Cómo **Stack Images Vertically** – Un resumen rápido

Si te preguntas **how to stack images vertically** sin Aspose, podrías usar `System.Drawing` para crear un nuevo bitmap y dibujar cada página una tras otra. Sin embargo, `Image.CombineVertical` incorporado de Aspose maneja DPI, formato de píxel y gestión de memoria por ti, siendo la opción más fiable para código de producción.

### Alternativa: Usando `System.Drawing` (solo por curiosidad)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

El enfoque manual funciona, pero pierdes la comodidad del manejo automático de DPI y la capacidad de alimentar directamente el resultado a `RecognizeToPdf`. Quédate con `CombineVertical` a menos que tengas un requisito muy específico.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Errores de falta de memoria** al procesar decenas de escaneos de alta resolución | Cada imagen permanece en memoria hasta que se escribe el PDF | Deseche los objetos `Image` tan pronto como termine (`bloques using`) o reduzca la escala de las imágenes antes de combinar |
| **Texto basura** después del OCR | Escaneos sesgados o bajo contraste | Mantenga los filtros `DeskewFilter` y `DenoiseFilter`; considere añadir `ContrastFilter` si es necesario |
| **Capa buscable faltante** | Se usó `Recognize` en lugar de `RecognizeToPdf` | Asegúrese de llamar a `ocrEngine.RecognizeToPdf` sobre la imagen combinada |
| **Falla de respaldo GPU** en máquinas sin controladores adecuados | `ProcessingMode.Gpu` lanza una excepción | Envuelva la creación del motor en un try/catch y recurra a `ProcessingMode.Cpu` |

## Próximos pasos – Extender el flujo de trabajo

Ahora que sabes cómo **create searchable PDF**, podrías querer:

- **Procesar por lotes carpetas completas** usando `Directory.GetFiles` y un bucle `foreach`.
- **Añadir marcas de agua** a cada página antes de combinar (use `ImageProcessor` de Aspose.Imaging).
- **Dividir el PDF buscable** nuevamente en páginas individuales si necesitas PDFs por página más tarde (`PdfDocument.Split` de Aspose.PDF).
- **Integrar con Azure Blob Storage** para obtener imágenes de la nube y subir el PDF final.

Todas estas extensiones naturalmente implican los mismos conceptos básicos: configuración OCR, manejo de imágenes y exportación PDF.

## Conclusión

Hemos cubierto todo lo que necesitas para **create searchable PDF** a partir de una colección de imágenes escaneadas en C#. Al inicializar un `OcrEngine` habilitado para GPU, ejecutar un lote paralelo con `OcrBatchProcessor`, **combine images vertically**, y finalmente llamar a `RecognizeToPdf`, obtienes un documento ordenado y buscable listo para archivado o indexación. La exportación adicional a JSON te brinda total visibilidad de los resultados OCR, abriendo puertas a análisis o flujos de trabajo personalizados.

Pruébalo, experimenta con diferentes filtros y observa cómo tu canalización de automatización de documentos se vuelve mucho más fluida. Si encuentras algún detalle, deja un comentario—¡feliz codificación!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}