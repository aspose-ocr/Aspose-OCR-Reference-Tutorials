---
category: general
date: 2026-01-01
description: Hur man batch-OCR med Aspose OCR Engine i C#. Lär dig att känna igen
  text från bilder och extrahera text från TIFF-filer med GPU-acceleration.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: sv
og_description: Hur man batch-OCR i C# med Aspose OCR Engine. Denna guide visar hur
  du kan känna igen text från bilder och extrahera text från TIFF-filer på ett effektivt
  sätt.
og_title: Hur man batchar OCR i C# – Komplett Aspose‑guide
tags:
- OCR
- C#
- Aspose
- GPU
title: Hur man batchar OCR i C# med Aspose OCR-motorn
url: /sv/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch-OCR i C# med Aspose OCR Engine

Har du någonsin undrat **hur man batch-OCR** när du har dussintals skannade dokument liggande i en mapp? Du är inte ensam—många utvecklare stöter på den muren när de går från enstaka bildigenkänning till att bearbeta en hel samling. Den goda nyheten är att Aspose OCR gör det till en barnlek, oavsett om du kör på en CPU eller utnyttjar GPU-acceleration.

I den här handledningen går vi igenom ett komplett, körbart exempel som **läser av text från bilder** och även **extraherar text från TIFF**‑filer i bulk. Inga vaga “se dokumentationen”-genvägar—bara en självständig lösning som du kan kopiera‑klistra in och köra idag.

## Förutsättningar

* .NET 6.0 eller senare installerat (koden riktar sig mot .NET 6, men .NET 5 fungerar också).
* Aspose.OCR för .NET NuGet‑paket (både CPU‑ och GPU‑versioner finns tillgängliga; installera den som matchar din hårdvara).
* En mapp med några exempel‑TIFF‑ eller PNG‑filer som du vill bearbeta.
* Visual Studio 2022 eller någon annan IDE du föredrar.

> **Proffstips:** Om du planerar att använda GPU‑versionen, kontrollera att din grafikdrivrutin är uppdaterad och att CUDA 11+ är installerat. Motorn kommer automatiskt att falla tillbaka till CPU om den inte hittar ett kompatibelt GPU.

## Steg 1 – Ställ in projektet och installera Aspose.OCR

### H2: Skapa en ny konsolapp och lägg till Aspose.OCR

Öppna en terminal (eller Package Manager Console i Visual Studio) och kör:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Om du har en GPU‑aktiverad licens, lägg till GPU‑paketet istället:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Klart—ditt projekt refererar nu till OCR‑biblioteket som vi kommer att använda för **batch-OCR**.

## Steg 2 – Initiera OCR‑motorn (CPU eller GPU)

### H2: Hur man batch-OCR – Motorinitiering

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Varför detta är viktigt:** Genom att växla `UseGpu` låter du Aspose bestämma den snabbaste vägen. Om GPU inte är tillgänglig byter motorn tyst tillbaka till CPU, så ditt batch‑jobb kraschar aldrig på grund av saknad hårdvara.

## Steg 3 – Samla filerna du vill bearbeta

### H2: Läs av text från bilder – Bygg fillistan

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Obs på kantfall:** Om du har en blandning av format, ändra sökmönstret till `"*.*"` och filtrera efter filändelse i loopen. Detta håller batchen flexibel.

## Steg 4 – Bearbeta varje bild och visa en förhandsgranskning

### H2: Extrahera text från TIFF – Loopa igenom filerna

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Vad du kommer att se:** För varje TIFF skriver konsolen ut något i stil med:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Den förhandsgranskningen bekräftar att batchen lyckades utan att du behöver öppna varje fil manuellt.

## Steg 5 – Spara resultat (valfritt men praktiskt)

### H3: Spara OCR‑utdata till textfiler

Om du behöver hela texten för efterföljande bearbetning, lägg till detta inuti `foreach`‑loopen:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Nu får varje TIFF en tillhörande `.txt`‑fil som innehåller hela OCR‑utdata—perfekt för indexering, sökning eller för att mata in i en språkmodell.

## Steg 6 – Kör demon och verifiera

1. Bygg projektet: `dotnet build`.
2. Kör: `dotnet run --project GpuBatchDemo.csproj`.

Du bör se förhandsgranskningsraderna skrivas ut i konsolen, och (om du lade till det valfria steget) en serie `.txt`‑filer bredvid dina källbilder.

### H3: Vanliga fallgropar & hur man åtgärdar dem

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **Empty `ocrResult.Text`** | Bilden är för mörk eller låg DPI | Förprocessa bilder (öka kontrast, skala upp) eller sätt `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Föråldrad drivrutin | Uppdatera GPU‑drivrutin, eller sätt `UseGpu = false` för att tvinga CPU. |
| **Exception “File not found”** | Fel sökvägsseparator på Linux/macOS | Använd `Path.Combine` eller framåtsnedstreck (`/`). |

## Steg 7 – Skala upp (utöver några filer)

När du går från ett fåtal TIFF‑filer till tusentals, överväg:

* **Parallell bearbetning:** Inslå `foreach` i `Parallel.ForEach` (se till att motorinstansen är trådsäker; annars skapa en per tråd).
* **Chunkad I/O:** Läs bilder i batcher för att undvika att RAM tar slut.
* **Loggning:** Skriv framsteg till en loggfil; det hjälper att återuppta efter en krasch.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Kom ihåg:** GPU‑minnet delas, så att starta för många parallella GPU‑jobb kan faktiskt göra det långsammare. Testa med några trådar först.

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Att köra detta program kommer att **läsa av text från bilder**, **extrahera text från TIFF**, och demonstrera **hur man batch-OCR** effektivt.

## Slutsats

Du har nu ett gediget, end‑to‑end‑exempel på **hur man batch-OCR** i C# med Asposes OCR‑motor. Handledningen täckte allt från att sätta upp projektet, växla GPU‑acceleration, bygga en fillista, bearbeta varje bild och spara resultat. Oavsett om du extraherar text från TIFF‑filer eller något annat bildformat, gäller samma mönster—byt bara filändelserna.

Redo för nästa steg? Prova att integrera OCR‑utdata med ett sökindex, mata in texten i en stor språkmodell, eller experimentera med parallell bearbetning för att spara minuter på massiva batcher. Himlen är gränsen, och du har grunden att bygga vidare på.

Har du frågor eller vill dela dina egna batch‑OCR‑tips? Lämna en kommentar nedan—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}