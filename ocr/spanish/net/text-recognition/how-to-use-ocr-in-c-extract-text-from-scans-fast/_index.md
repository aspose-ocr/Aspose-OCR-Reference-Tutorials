---
category: general
date: 2026-03-13
description: Cómo usar OCR en C# para extraer texto de escaneos. Aprende a convertir
  TIFF a texto con Aspose OCR, aceleración GPU y código paso a paso.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: es
og_description: Cómo usar OCR en C# para extraer texto de escaneos. Esta guía muestra
  cómo convertir TIFF a texto con Aspose OCR y aceleración GPU.
og_title: Cómo usar OCR en C# – Extrae texto de escaneos rápidamente
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Cómo usar OCR en C# – Extrae texto de escaneos rápidamente
url: /es/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar OCR en C# – Extraer texto de escaneos rápidamente

¿Alguna vez te has preguntado **cómo usar OCR** para extraer texto legible de una pila de archivos TIFF escaneados? No eres el único. En muchos proyectos del mundo real —piense en la digitalización de facturas, el archivo de documentos históricos o simplemente hacer que los PDFs sean buscables— los desarrolladores necesitan una forma fiable de **extraer texto de escaneos** sin esfuerzo.

¿La buena noticia? Con Aspose OCR y unas pocas líneas de C# puedes convertir TIFF a texto en cuestión de segundos, incluso en una estación de trabajo modesta. A continuación obtendrás un ejemplo completo, listo para ejecutar, además del razonamiento detrás de cada elección para que puedas adaptarlo a tu propio flujo de trabajo.

## Lo que necesitarás

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | El paquete NuGet de Aspose OCR está dirigido a runtimes .NET modernos. |
| Visual Studio 2022 (or any IDE you like) | Te brinda IntelliSense y depuración sencilla. |
| A CUDA‑compatible GPU & driver (optional) | Permite `ocrEngine.UseGpu = true` para un notable aumento de velocidad en lotes grandes. |
| A folder of TIFF images you want to process | Este tutorial usa archivos `*.tif`, pero puedes adaptar el patrón. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | La biblioteca central que realiza el trabajo pesado. |

Si te falta alguno de estos, consíguelo ahora—no tiene sentido seguir leyendo solo para encontrarte con una dependencia ausente más adelante.

## Visión general de la solución

A grandes rasgos, el programa hace tres cosas:

1. **Crear un motor OCR** y, opcionalmente, activar la aceleración GPU.  
2. **Iterar sobre cada archivo TIFF** en un directorio, ejecutar el reconocimiento y capturar el texto plano resultante.  
3. **Escribir el texto** en un archivo `.txt` que queda junto a la imagen original.

Eso es todo. El código es deliberadamente pequeño, pero muestra buenas prácticas como la selección explícita de idioma, la correcta liberación de recursos y el manejo de errores para los casos límite más comunes.

![Ejemplo de cómo usar OCR en C#](/images/how-to-use-ocr-csharp.png "Ilustración de cómo usar OCR en C# para extraer texto de escaneos")

## Paso 1: Inicializar el motor OCR (Cómo usar OCR)

Lo primero que necesitas es una instancia de `OcrEngine`. Este objeto es la puerta de entrada a toda la funcionalidad de Aspose OCR. Por defecto funciona en la CPU, pero establecer `UseGpu = true` indica a la biblioteca que delegue los cálculos matriciales intensivos a tu tarjeta gráfica, siempre que tengas un controlador compatible con CUDA instalado.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Por qué esto importa:**  
- **Aceleración GPU** puede reducir el tiempo de procesamiento hasta en un 70 % para escaneos de alta resolución.  
- **Selección explícita de idioma** evita que el motor adivine y mejora la precisión, sobre todo para scripts no latinos.

## Paso 2: Apuntar el motor a tus escaneos (Convertir TIFF a texto)

A continuación indicamos al programa dónde buscar las imágenes. Usar `Directory.GetFiles` con un filtro `*.tif` mantiene la lógica simple y evita incluir archivos no relacionados como `.jpg` o `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Nota sobre casos límite:** Si el directorio está vacío, el bucle a continuación simplemente nunca se ejecuta, lo cual es perfectamente aceptable. Verás un mensaje amigable “No files found” más adelante.

## Paso 3: Procesar cada archivo TIFF (Extraer texto de escaneos)

Ahora el corazón del programa: cargar cada imagen, ejecutar OCR y guardar la salida. El ayudante `ImageStream.FromFile` transmite el archivo directamente a la memoria, lo que es más eficiente que cargar primero un `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Por qué envolvemos cada iteración en un `try/catch`:**  
Procesar un lote de documentos es desordenado; un TIFF corrupto o un fallo por falta de memoria no debe abortar toda la ejecución. El bloque `catch` registra el problema y continúa, manteniendo la canalización robusta.

### Salida esperada

Por cada `example.tif` encontrarás un archivo hermano `example.txt` que contiene algo como:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Si el motor OCR no puede leer una línea, simplemente dejará una línea en blanco o un carácter distorsionado—no se producirá ningún bloqueo.

## Paso 4: Limpieza y disposición (Mejor práctica)

`OcrEngine` implementa `IDisposable`, por lo que es cortés liberar los recursos nativos cuando terminas. En una pequeña aplicación de consola podrías confiar en el GC, pero la disposición explícita es un hábito que vale la pena cultivar.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Ejemplo completo funcional (Listo para copiar y pegar)

A continuación tienes el programa completo que puedes pegar en un nuevo proyecto de Console App. Compila tal cual, siempre que hayas añadido el paquete NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Lista de verificación rápida

- **GPU flag** – elimina o establece a `false` si no dispones de un controlador CUDA.  
- **Language** – cambia `Language.English` por cualquier otro idioma soportado.  
- **File pattern** – modifica `"*.tif"` a `"*.png"` o `"*.*"` si tus escaneos están en otro formato.  

## Errores comunes y consejos profesionales (tutorial OCR c#)

| Problema | Cómo evitarlo |
|----------|----------------|
| **Errores de falta de memoria** en lotes enormes | Procesa los archivos en bloques más pequeños o llama a `GC.Collect()` después de cada 50 archivos (rara vez necesario). |
| **GPU no detectada** pero `UseGpu = true` | El motor recurre silenciosamente a la CPU, pero puedes comprobar `ocrEngine.IsGpuAvailable` después de la construcción. |
| **Paquete de idioma incorrecto** que produce salida distorsionada | Siempre establece `ocrEngine.Language` explícitamente; el valor predeterminado puede ser `Language.Unknown`. |
| **La ruta del archivo contiene caracteres Unicode** | Usa `Path.GetFullPath` para normalizar, o antepone `@"\\?\"` en Windows si las rutas exceden |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}