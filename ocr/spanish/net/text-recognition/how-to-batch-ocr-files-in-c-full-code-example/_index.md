---
category: general
date: 2026-02-17
description: Cómo procesar OCR por lotes varios PDFs e imágenes en C# usando Aspose
  OCR. Aprende a extraer texto de PDF, convertir PDF a texto y reconocer texto de
  imágenes.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: es
og_description: Cómo procesar OCR por lotes varios documentos en C# con Aspose OCR.
  Obtén código paso a paso para extraer texto de PDF, convertir PDF a texto y reconocer
  texto de imágenes.
og_title: Cómo procesar por lotes archivos OCR en C# – Guía completa
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Cómo procesar por lotes archivos OCR en C# – Ejemplo completo de código
url: /es/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo procesar OCR por lotes en C# – Guía completa

¿Alguna vez te has preguntado **cómo procesar OCR por lotes** una pila de PDFs y escaneos de imágenes sin escribir un bucle separado para cada archivo? No estás solo. La mayoría de los desarrolladores se topan con este obstáculo cuando necesitan extraer texto de decenas de páginas de una sola vez. ¿La buena noticia? Con Aspose OCR puedes alimentar una colección de archivos a un único motor y dejar que haga el trabajo pesado.  

En este tutorial recorreremos una solución práctica que te permite **extraer texto de pdf**, **convertir pdf a texto** y **reconocer texto de imágenes** todo en una ejecución por lotes. Al final tendrás una aplicación de consola lista‑para‑ejecutar que imprime el resultado del OCR para cada página, y comprenderás el porqué de cada paso para que puedas adaptarlo a tus propios proyectos.

## Requisitos previos – Lo que necesitas antes de comenzar

- **.NET 6.0 o posterior** (el código también funciona en .NET Framework, pero se recomienda .NET 6+)
- **Paquete NuGet Aspose.OCR** – instálalo con `dotnet add package Aspose.OCR`
- Un par de archivos de muestra: un PDF multipágina (`doc1.pdf`) y un TIFF escaneado (`doc2.tif`). Colócalos en una carpeta a la que puedas referenciar, por ejemplo, `C:\OCRSamples`.
- Conocimientos básicos de C# – deberías estar cómodo con sentencias `using` y colecciones.

> Pro tip: Si no tienes una licencia, Aspose ofrece una clave temporal gratuita que elimina el límite de 100 páginas durante el desarrollo.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Primero, crea un nuevo proyecto de consola (o añádelo a uno existente) y trae los espacios de nombres requeridos.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Por qué es importante:** Importar `Aspose.OCR.Image` te brinda el método conveniente `ImageStream.FromFile`, que divide automáticamente las páginas del PDF en flujos de imagen separados. Esa es la salsa secreta que hace que el procesamiento por lotes sea sencillo.

## Paso 2: Inicializar el motor OCR

El motor es el caballo de batalla que se comunica con el motor OCR subyacente. Solo necesitas una instancia para todo el lote.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Explicación:** Reutilizar el mismo `OcrEngine` reduce el consumo de memoria y acelera el procesamiento porque las bibliotecas nativas permanecen cargadas entre páginas.

## Paso 3: Construir una lista de flujos de imagen

Aquí reunimos cada documento que queremos procesar. `ImageStream.FromFile` es lo suficientemente inteligente como para dividir un PDF en páginas individuales, de modo que un PDF de tres páginas se convierta en tres flujos separados detrás de escena.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Caso límite:** Si tienes una mezcla de PDFs, TIFFs, JPEGs o PNGs, simplemente añádelos a la misma lista – Aspose detecta el formato automáticamente.

## Paso 4: Ejecutar la operación OCR por lotes

Ahora entregamos la lista al motor. `RecognizeBatch` devuelve una colección de objetos `OcrResult`, uno por página.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **¿Por qué por lotes?** Ejecutar OCR página a página en un bucle manual obliga al motor a reinicializarse cada vez, lo que puede duplicar el tiempo de procesamiento. `RecognizeBatch` mantiene el motor activo y devuelve los resultados a medida que están disponibles.

## Paso 5: Mostrar el texto reconocido

Finalmente, recorremos los resultados y escribimos el texto de cada página en la consola. Aquí puedes reemplazar `Console.WriteLine` por escrituras a archivo, inserciones en base de datos o cualquier otra acción posterior.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Salida esperada en la consola

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Si ejecutas el programa con los archivos de muestra, deberías ver un bloque de texto para cada página, demostrando que has **extraído texto de pdf escaneado** con éxito en una sola pasada.

## Manejo de problemas comunes

| Problema | Por qué ocurre | Solución rápida |
|----------|----------------|-----------------|
| **Errores de falta de memoria** | Los PDFs grandes generan muchas imágenes de alta resolución. | Limita el DPI al cargar PDFs: `ocrEngine.Settings.ImageDpi = 200;` |
| **Caracteres extraños** | El escaneo de origen es de baja calidad o usa un idioma no compatible. | Establece el idioma explícitamente: `ocrEngine.Language = Language.English;` |
| **Resultados parciales** | La lista por lotes contiene un archivo corrupto. | Envuelve `RecognizeBatch` en un try/catch y registra `e.Message` del archivo problemático. |
| **Cuello de botella de rendimiento** | Ejecutándose en un solo hilo en una máquina multinúcleo. | Usa `Parallel.ForEach` con instancias separadas de `OcrEngine` por hilo (avanzado). |

## Bonus: Guardar resultados OCR en archivos de texto

Si prefieres mantener un archivo `.txt` separado por página, solo agrega un pequeño bloque de escritura dentro del bucle:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Ahora has convertido **convert pdf to text** en una carpeta ordenada de archivos de texto plano—perfecto para indexación o búsqueda posterior.

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para copiar y pegar. Sin dependencias ocultas, sin scripts externos.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Ejecuta `dotnet run` desde la carpeta del proyecto y observa cómo la consola se llena con el texto extraído. Así es **cómo procesar OCR por lotes** una colección de documentos en solo unas pocas líneas de C#.

## Lo que cubrimos – Resumen rápido

- Configuraste una aplicación de consola .NET e instalaste Aspose.OCR.  
- Creaste una única instancia de `OcrEngine` para mantener el proceso eficiente.  
- Construiste una lista de objetos `ImageStream` que divide automáticamente los PDFs en páginas.  
- Ejecutaste `RecognizeBatch` para **extraer texto de pdf** y otros formatos de imagen de una sola vez.  
- Imprimes los resultados y, opcionalmente, los guardas como archivos `.txt` individuales, completando el flujo **convert pdf to text**.  

## Próximos pasos y temas relacionados

- **Escalar**: Usa `Parallel.ForEach` con un pool de objetos `OcrEngine` para procesar cientos de archivos concurrentemente.  
- **Paquetes de idioma**: Cambia `Language.English` por `Language.French` o carga un diccionario personalizado cuando necesites **reconocer texto de imágenes** en otros idiomas.  
- **Post‑procesamiento**: Canaliza la salida del OCR a través de un corrector ortográfico o un analizador de lenguaje natural para mejorar la precisión en contratos escaneados.  
- **Bibliotecas alternativas**: Compara Aspose OCR con Tesseract.NET si buscas una opción de código abierto—ambas pueden **extraer texto de pdf escaneado** pero difieren en licenciamiento y precisión out‑of‑the‑box.

---

![ejemplo de cómo procesar OCR por lotes](alt="ejemplo de cómo procesar OCR por lotes")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}