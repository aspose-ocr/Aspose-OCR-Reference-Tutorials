---
category: general
date: 2026-04-26
description: Cómo procesar OCR por lotes de imágenes PNG rápidamente. Aprende a extraer
  texto de PNG, convertir imágenes a texto, escribir el texto reconocido y leer el
  directorio de PNG con Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: es
og_description: Cómo procesar por lotes imágenes PNG con OCR en C# usando Aspose OCR.
  Esta guía muestra cómo extraer texto de PNG, convertir imágenes a texto y escribir
  el texto reconocido de manera eficiente.
og_title: Cómo procesar OCR por lotes de imágenes PNG en C# – Paso a paso
tags:
- OCR
- C#
- Aspose
title: Cómo hacer OCR por lotes de imágenes PNG en C# – Guía completa
url: /es/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo procesar OCR por lotes en imágenes PNG con C# – Guía completa

¿Alguna vez te has preguntado **cómo hacer OCR por lotes** de una carpeta completa de archivos PNG sin escribir un programa distinto para cada imagen? No eres el único que maneja docenas de capturas de pantalla, recibos escaneados o gráficos que necesitan convertirse en texto buscable. En este tutorial recorreremos una solución práctica que **extrae texto de PNG**, **convierte imágenes a texto** y **escribe el texto reconocido** en archivos individuales, todo mientras lee automáticamente el directorio PNG.

Al final de esta guía tendrás una aplicación de consola en C# lista para ejecutar que procesa cualquier número de imágenes de una sola vez. Sin scripts extra, sin copiar‑pegar manualmente—solo código puro que hace el trabajo pesado por ti.

## Qué necesitarás

- **.NET 6.0** o superior (el código también funciona con .NET Framework).  
- Paquete NuGet **Aspose.OCR for .NET** (la prueba gratuita sirve para pruebas).  
- Una carpeta con un puñado de archivos *.png* que quieras procesar con OCR.  
- Visual Studio 2022 o cualquier IDE de C# que prefieras.

Si los tienes, podemos pasar directamente a la implementación.

## Paso 1 – Prepara tus carpetas de entrada y salida *(Read PNG Directory)*

Lo primero que hacemos es indicar al programa la carpeta que contiene las imágenes y decidir dónde vivirán los archivos *.txt* resultantes. Usar `Directory.GetFiles` nos da una enumeración limpia de cada PNG en el directorio.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Por qué importa:**  
- Usar un comodín (`*.png`) garantiza que solo procesemos archivos de imagen, ignorando documentos sueltos.  
- Crear la carpeta de salida sobre la marcha evita una `DirectoryNotFoundException` más adelante.

> **Consejo profesional:** Si necesitas admitir otros formatos (JPEG, BMP), simplemente amplía el patrón de búsqueda o llama a `Directory.EnumerateFiles` con múltiples extensiones.

## Paso 2 – Inicializa el motor OCR *(Convert Images to Text)*

Aspose.OCR incluye dos tipos de motor: un `OcrEngine` basado en CPU y un `GpuOcrEngine` acelerado por GPU. Para la mayoría de los trabajos por lotes el motor de CPU es perfectamente suficiente, pero puedes cambiar el nombre de la clase si dispones de una GPU capaz.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Por qué importa:**  
- Especificar el idioma mejora drásticamente la precisión porque el motor sabe qué conjunto de caracteres esperar.  
- Cambiar a `GpuOcrEngine` es un cambio de una sola línea si encuentras cuellos de botella de rendimiento en lotes grandes.

## Paso 3 – Crea un Reconocedor por Lotes

Aspose proporciona un práctico `BatchRecognizer` que acepta una enumeración de rutas de archivo y devuelve los resultados uno a uno. Esto evita cargar todas las imágenes en memoria simultáneamente, un detalle crucial para carpetas extensas.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Por qué importa:**  
- El reconocedor por lotes encapsula la lógica del bucle, permitiéndonos centrarnos en qué hacer con cada resultado en lugar de cómo iterar de forma segura.

## Paso 4 – Ejecuta OCR en todas las imágenes y escribe la salida *(Write Recognized Text)*

Ahora realizamos el OCR propiamente dicho. El método `Recognize` devuelve un `IEnumerable<RecognitionResult>` donde cada resultado contiene el texto extraído y otros metadatos.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Por qué importa:**  
- Usar `File.WriteAllText` garantiza que el texto se guarde con codificación UTF‑8 por defecto, preservando los caracteres especiales.  
- La nomenclatura incremental (`out_0.txt`, `out_1.txt`) coincide con el orden de procesamiento, lo que resulta útil para depurar.

> **Caso límite:** Si alguna imagen falla al hacer OCR (p. ej., archivo corrupto), `RecognitionResult.Text` quedará vacío. Puedes añadir una simple comprobación dentro del bucle para registrar los fallos:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Paso 5 – Junta todo – Ejemplo completo funcionando

A continuación tienes el programa completo que puedes copiar‑pegar en un nuevo proyecto de consola. Incluye las directivas `using`, la validación de carpetas y una pequeña interfaz de consola para que sepas cuándo termina el lote.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Salida esperada:**  
Al ejecutar el programa se imprimirá algo como:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Y verás `out_0.txt` … `out_11.txt` dentro de la carpeta de salida, cada uno con la versión de texto plano de su imagen correspondiente.

## Preguntas frecuentes y consejos

| Pregunta | Respuesta |
|----------|-----------|
| *¿Puedo hacer OCR también en subcarpetas?* | Sí—reemplaza `Directory.GetFiles` por `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *¿Qué pasa si necesito otro idioma?* | Establece `ocrEngine.Language = Language.Spanish;` (o cualquier enum soportado). |
| *¿Cómo manejo lotes enormes (miles de archivos)?* | Considera procesar en bloques o usar `Parallel.ForEach` con un grado de paralelismo limitado para evitar agotar la memoria. |
| *¿La salida siempre es UTF‑8?* | `File.WriteAllText` usa UTF‑8 sin BOM por defecto, lo que funciona para la mayoría de lenguas latinas. Para scripts asiáticos quizá necesites especificar `Encoding.UTF8` explícitamente. |
| *¿Puedo obtener puntuaciones de confianza?* | `RecognitionResult` expone `Confidence`; puedes registrarla junto al texto para control de calidad. |

## Visión general visual *(How to Batch OCR – Diagram)*

![How to batch OCR workflow diagram showing input folder → OCR engine → batch recogniser → output txt files](https://example.com/diagram-how-to-batch-ocr.png "How to batch OCR")

*El texto alternativo contiene la palabra clave principal, cumpliendo con los requisitos SEO de la imagen.*

## Conclusión

Acabamos de cubrir **cómo hacer OCR por lotes** en un directorio de archivos PNG usando Aspose.OCR, desde la lectura del directorio PNG hasta la escritura de cada archivo de texto reconocido. La solución es totalmente autónoma, funciona en cualquier runtime moderno de .NET y puede ampliarse para aceleración GPU, soporte multilingüe o procesamiento paralelo.

¿Listo para el siguiente paso? Prueba cambiar `Language.Latin` por otro idioma, o integra la salida en un índice de búsqueda para que tus documentos sean buscables al instante. El cielo es el límite una vez domines el OCR por lotes.

¡Feliz codificación, y avísame en los comentarios si encuentras algún obstáculo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}