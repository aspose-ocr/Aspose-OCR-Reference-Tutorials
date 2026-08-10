---
category: general
date: 2026-02-14
description: Cómo usar OCR en C# para extraer texto de archivos PNG rápidamente. Aprende
  OCR por lotes de imágenes, procesa múltiples imágenes y utiliza Aspose OCR C# en
  una única guía.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: es
og_description: Cómo usar OCR en C# con Aspose OCR C#. Este tutorial muestra cómo
  extraer texto de archivos PNG, procesar OCR por lotes de imágenes y manejar múltiples
  imágenes de manera eficiente.
og_title: Cómo usar OCR en C# – Extracción de texto de PNG por lotes
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cómo usar OCR en C# – Procesamiento por lotes de imágenes PNG con Aspose OCR
url: /es/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR en C# – Procesamiento por lotes de imágenes PNG con Aspose OCR

¿Alguna vez te has preguntado **cómo usar OCR** para extraer texto de un montón de archivos PNG sin escribir una rutina separada para cada uno? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan **extraer texto PNG** de recursos a gran escala, especialmente cuando las imágenes están en una carpeta y tienes que iniciar el motor OCR para cada archivo.  

En esta guía recorreremos una solución completa y lista‑para‑ejecutar que **procesa OCR por lotes**, **procesa múltiples imágenes** en paralelo, y aprovecha la potente biblioteca **Aspose OCR C#**. Al final tendrás un único ejecutable que lee cualquier número de PNG, extrae su texto y muestra los resultados en la consola, todo con solo unas pocas líneas de código.

## Requisitos previos

- .NET 6.0 o posterior (el código funciona también con .NET Core y .NET Framework)  
- Una licencia válida de Aspose.OCR para .NET (o la prueba gratuita) – puedes obtenerla en el sitio web de Aspose.  
- Una carpeta que contenga los archivos PNG que deseas leer.  
- Visual Studio 2022 (o cualquier IDE compatible con C#).  

- No se requieren paquetes NuGet adicionales más allá de `Aspose.OCR`.

## Paso 1: Cómo usar OCR – Inicializar el motor Aspose OCR

Lo primero que necesitas es una instancia de la clase `Engine`. Este objeto abstrae la tecnología OCR subyacente y puede ejecutarse en CPU o GPU, según tu hardware y licencia.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Por qué es importante:* Inicializar el motor una sola vez y reutilizarlo entre hilos ahorra memoria y evita la sobrecarga de cargar repetidamente los modelos OCR. También garantiza configuraciones consistentes para todas las imágenes.

## Paso 2: Extraer texto PNG – Recopilar las rutas de imagen

A continuación, necesitamos una colección de rutas de archivo. En un proyecto real podrías leer el directorio de forma dinámica, pero para mayor claridad listaremos algunos archivos de ejemplo.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Consejo:* Reemplaza `YOUR_DIRECTORY` con la ruta absoluta o relativa a tus imágenes. Si tienes docenas de archivos, puedes sustituir la lista manual por `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Paso 3: OCR por lotes de imágenes – Ejecutar reconocimiento en paralelo

Procesar imágenes una tras otra es simple pero lento. Usando `Parallel.ForEach` podemos **procesar múltiples imágenes** simultáneamente, aprovechando CPUs multinúcleo.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*¿Por qué en paralelo?* Cada llamada a OCR es intensiva en CPU pero independiente, por lo que ejecutarlas concurrentemente puede reducir drásticamente el tiempo total de ejecución, especialmente en una máquina de 4 núcleos o más.

## Paso 4: Procesar múltiples imágenes – Mostrar el texto extraído

Ahora que tenemos una colección de objetos `OcrResult`, podemos iterar sobre ellos e imprimir el texto reconocido. Aquí es donde normalmente almacenarías la salida en una base de datos o escribirías a archivos, pero la salida en consola mantiene el ejemplo conciso.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Salida esperada en consola (ejemplo):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Si alguna imagen no se puede cargar, Aspose lanza una excepción; puedes envolver la llamada `engine.Recognize` en un bloque try/catch para registrar errores sin abortar todo el lote.

## Paso 5: Ejemplo completo – Todas las piezas juntas

A continuación se muestra el programa completo que puedes copiar y pegar en un nuevo proyecto de consola C#. Incluye todo, desde las declaraciones `using` hasta el bucle de salida final.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Ejecutando el ejemplo

1. Crea un nuevo proyecto **Console App** en Visual Studio.  
2. Añade el paquete NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Reemplaza `YOUR_DIRECTORY` con la ruta que contiene tus archivos PNG.  
4. Compila y ejecuta – deberías ver el texto extraído impreso en la consola.

## Consejos profesionales y casos límite

- **Aceleración GPU:** Si tienes una GPU compatible y una licencia de Aspose OCR, habilítala mediante `EngineSettings` antes de crear el motor. Esto puede ahorrar segundos por cada imagen.  
- **Archivos grandes:** Para imágenes mayores de 10 MB, considera reducir su escala primero para disminuir la presión de memoria.  
- **Soporte de idioma:** Por defecto el motor asume inglés. Configura `engine.Language = Language.French;` (o cualquier idioma soportado) para mejorar la precisión en texto que no sea inglés.  
- **Manejo de errores:** El `try/catch` dentro del bucle paralelo garantiza que un archivo corrupto no aborta todo el lote. También puedes registrar los fallos en un archivo para revisarlos después.  
- **Almacenamiento de resultados:** En lugar de imprimir, podrías escribir `result.Text` a un archivo `.txt` usando `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Conclusión

Ahora sabes **cómo usar OCR** en C# para **extraer texto PNG** de archivos, **procesar OCR por lotes** de imágenes y **procesar múltiples imágenes** de manera eficiente con Aspose OCR C#. La solución es completamente autónoma, se ejecuta en paralelo y puede ampliarse para manejar cientos o miles de archivos con cambios mínimos.

¿Listo para el siguiente paso? Prueba cambiar la salida de consola por un informe CSV, experimenta con la aceleración GPU, o alimenta el texto OCR a un índice de búsqueda. Las posibilidades son infinitas, y el patrón central—inicializar una vez, ejecutar en paralelo, manejar errores con elegancia—te será útil en cualquier canal de procesamiento de imágenes.

¡Feliz codificación, y que tus trabajos de OCR sean rápidos y sin errores!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}