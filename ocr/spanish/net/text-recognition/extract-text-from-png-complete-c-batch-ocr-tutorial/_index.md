---
category: general
date: 2026-04-26
description: Extrae texto de archivos PNG rápidamente con C#. Aprende cómo convertir
  imágenes a texto, leer archivos PNG, recorrer imágenes y procesar OCR por lotes
  en minutos.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: es
og_description: Extrae texto de archivos PNG rápidamente con C#. Esta guía muestra
  cómo convertir imágenes a texto, leer archivos PNG, recorrer imágenes y procesar
  OCR por lotes.
og_title: Extraer texto de PNG – Tutorial completo de OCR por lotes en C#
tags:
- C#
- OCR
- Aspose
title: Extraer texto de PNG – Tutorial completo de OCR por lotes en C#
url: /es/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de PNG – Tutorial completo de OCR por lotes en C#

¿Alguna vez necesitaste **extraer texto de PNG** pero no sabías por dónde empezar? No estás solo—muchos desarrolladores se topan con ese obstáculo cuando intentan OCR por primera vez en una carpeta de capturas de pantalla. La buena noticia es que con unas pocas líneas de C# y Aspose OCR puedes convertir imágenes a texto, leer archivos PNG, iterar sobre imágenes y procesar todo por lotes de una sola vez.  

En este tutorial caminaremos a través de una aplicación de consola lista‑para‑ejecutar que hace exactamente eso. Al final tendrás una solución autosuficiente que extrae texto de cada PNG en un directorio y crea un archivo `.txt` correspondiente al lado de cada imagen. Sin scripts extra, sin copiar‑pegar manual—solo código puro.

## Lo que necesitarás

- **.NET 6 SDK** (o cualquier versión más reciente de .NET). Es gratuito, rápido y funciona en todas partes.  
- **Aspose.OCR for .NET** (el paquete NuGet). La biblioteca incluye aceleración GPU si dispones de una GPU compatible, pero también recurre a la CPU automáticamente.  
- Una carpeta con un puñado de **imágenes PNG** que quieras procesar.  
- Un editor de texto o IDE—Visual Studio, VS Code, Rider—lo que prefieras.  

Eso es todo. Si ya tienes eso, estás listo para comenzar.

![extraer texto de png ejemplo](image.png "captura de pantalla de demostración de extracción de texto de png")

*Texto alternativo de la imagen: “extraer texto de png usando OCR por lotes en C#”*

## Paso 1 – Configurar el proyecto e instalar Aspose.OCR

Primero, crea un nuevo proyecto de consola e incluye el paquete Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

¿Por qué usamos una aplicación de consola? Es el host más sencillo para trabajos por lotes, y puedes ejecutarla desde la línea de comandos o programarla con un planificador de tareas. Si más adelante necesitas una UI, simplemente puedes mover la lógica central a una biblioteca de clases.

## Paso 2 – Inicializar un motor OCR acelerado por GPU (o respaldo en CPU)

Aspose ofrece un `GpuOcrEngine` que detecta automáticamente una GPU compatible. Si no se encuentra ninguna, vuelve al motor CPU regular—no se necesita código adicional.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Consejo profesional:** Si estás en un servidor sin cabeza sin GPU, puedes reemplazar `GpuOcrEngine` por `OcrEngine` y el código se comportará exactamente igual.

## Paso 3 – Recorrer imágenes en el directorio objetivo

Necesitamos **recorrer imágenes** y seleccionar solo archivos PNG. El método `Directory.GetFiles` hace el trabajo pesado, y protegeremos contra una carpeta vacía.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Observa el uso de `SearchOption.TopDirectoryOnly`. Si más adelante necesitas recursividad en sub‑carpetas, simplemente cambia a `AllDirectories`. Ese pequeño cambio te permite **convertir imágenes a texto** en todo un árbol con una sola línea.

## Paso 4 – Realizar OCR y guardar el resultado

Ahora llega el núcleo del flujo de trabajo de **batch OCR images**. Cargamos cada PNG, ejecutamos `Recognize()`, y escribimos la cadena extraída en un archivo `.txt` que comparte el mismo nombre base.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**¿Por qué envolverlo en try/catch?** Los lotes de imágenes del mundo real a menudo contienen un archivo dañado o un PNG que usa un perfil de color poco común. Capturar la excepción evita que toda la ejecución se caiga y te permite seguir procesando los archivos restantes.

## Paso 5 – Ejecutar la aplicación y verificar la salida

Compila y lanza la aplicación:

```bash
dotnet run
```

Deberías ver un registro en consola similar a:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Abre cualquiera de los archivos `.txt` generados—ahí está tu texto extraído. Si un archivo está vacío, verifica la calidad de la imagen; OCR funciona mejor con texto claro y de alto contraste.

### Script de verificación rápida (opcional)

Si quieres asegurarte de que cada PNG obtuvo un archivo de texto correspondiente, ejecuta este pequeño one‑liner de PowerShell:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Variaciones comunes y casos límite

| Situación | Qué cambiar |
|-----------|-------------|
| **Idiomas no latinos** (p.ej., cirílico) | Set `ocrEngine.Language = Language.Cyrillic;` |
| **Conjunto grande de imágenes (>10 000 archivos)** | Use `Parallel.ForEach` to speed up processing, but watch GPU memory usage. |
| **Necesitas mantener el orden original de las imágenes** | Sort `pngFiles` before the `foreach` (`Array.Sort(pngFiles);`). |
| **Ejecutando en un servidor CI sin GPU** | Replace `GpuOcrEngine` with `OcrEngine` to avoid GPU initialization errors. |
| **Solo deseas procesar archivos que contengan una palabra clave específica** | After `result.Text` is retrieved, check `result.Text.Contains("Invoice")` before writing the file. |

Estos ajustes te permiten adaptar la tubería de **convert images to text** a casi cualquier escenario que puedas encontrar.

## Código fuente completo (listo para copiar y pegar)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Guarda esto como `Program.cs`, ejecuta `dotnet run`, y observa la magia suceder.

## Conclusión

Ahora tienes una **solución completa y lista para producción para extraer texto de PNG** usando C#. El tutorial cubrió todo—desde configurar el proyecto, inicializar un motor OCR acelerado por GPU, **recorrer imágenes**, hasta **batch OCR images** y guardar los resultados como texto plano.  

Si tienes curiosidad por los siguientes pasos, prueba:

- **Convert images to text** for other formats (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}