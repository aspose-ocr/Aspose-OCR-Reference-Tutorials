---
category: general
date: 2026-04-26
description: Extrahera text från PNG‑filer snabbt med C#. Lär dig hur du konverterar
  bilder till text, läser PNG‑filer, loopar igenom bilder och batchar OCR‑bilder på
  några minuter.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: sv
og_description: Extrahera text från PNG-filer snabbt med C#. Den här guiden visar
  hur du konverterar bilder till text, läser PNG-filer, loopar igenom bilder och utför
  batch‑OCR på bilder.
og_title: Extrahera text från PNG – Komplett C# batch‑OCR‑handledning
tags:
- C#
- OCR
- Aspose
title: Extrahera text från PNG – Komplett C# batch‑OCR‑handledning
url: /sv/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från PNG – Komplett C# batch-OCR‑handledning

Har du någonsin behövt **extrahera text från PNG**‑filer men varit osäker på var du ska börja? Du är inte ensam—många utvecklare stöter på samma problem när de först provar OCR på en mapp med skärmdumpar. Den goda nyheten är att med några rader C# och Aspose OCR kan du konvertera bilder till text, läsa PNG‑filer, loopa igenom bilder och batch‑processa allt på en gång.  

I den här handledningen går vi igenom en färdig‑att‑köra konsolapp som gör exakt det. När du är klar har du en självständig lösning som hämtar text från varje PNG i en katalog och placerar en motsvarande `.txt`‑fil bredvid varje bild. Inga extra skript, ingen manuell kopiering‑och‑klistring—bara ren kod.

## Vad du behöver

- **.NET 6 SDK** (eller någon nyare .NET‑version). Den är gratis, snabb och fungerar överallt.
- **Aspose.OCR for .NET** (NuGet‑paketet). Biblioteket inkluderar GPU‑acceleration om du har ett kompatibelt GPU, men faller automatiskt tillbaka till CPU om inget finns.
- En mapp med ett fåtal **PNG‑bilder** som du vill bearbeta.  
- En textredigerare eller IDE—Visual Studio, VS Code, Rider—vad du än föredrar.

Det är allt. Om du redan har detta är du redo att köra.

![extract text from png example](image.png "extract text from png demo screenshot")

*Bildtext: “extrahera text från png med C# batch OCR”*

## Steg 1 – Skapa projektet och installera Aspose.OCR

Först skapar du ett nytt konsolprojekt och hämtar Aspose OCR‑paketet.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Varför använder vi en konsolapp? Det är den enklaste värden för batch‑jobb, och du kan köra den från kommandoraden eller schemalägga den med en task‑runner. Om du senare behöver ett UI kan du bara flytta kärnlogiken till ett klassbibliotek.

## Steg 2 – Initiera en GPU‑accelererad OCR‑motor (eller CPU‑fallback)

Aspose erbjuder en `GpuOcrEngine` som automatiskt upptäcker ett stödjande GPU. Om inget hittas återgår den till den vanliga CPU‑motorn—ingen extra kod behövs.

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

**Pro‑tips:** Om du kör på en huvudlös server utan GPU kan du ersätta `GpuOcrEngine` med `OcrEngine` och koden fungerar exakt likadant.

## Steg 3 – Loopa igenom bilder i mål‑katalogen

Vi måste **loopa igenom bilder** och bara plocka PNG‑filer. Metoden `Directory.GetFiles` gör det tunga arbetet, och vi skyddar mot en tom mapp.

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

Observera användningen av `SearchOption.TopDirectoryOnly`. Om du senare behöver gå rekursivt igenom undermappar, byt bara till `AllDirectories`. Den lilla förändringen låter dig **konvertera bilder till text** i ett helt träd med en enda rad.

## Steg 4 – Utför OCR och spara resultatet

Nu kommer kärnan i **batch OCR‑bilder**‑arbetsflödet. Vi laddar varje PNG, kör `Recognize()` och skriver den extraherade strängen till en `.txt`‑fil som har samma basnamn.

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

**Varför omsluta med try/catch?** Verkliga bildbatcher innehåller ofta en trasig fil eller en PNG med en ovanlig färgprofil. Att fånga undantaget förhindrar att hela körningen kraschar och låter dig fortsätta bearbeta resterande filer.

## Steg 5 – Kör applikationen och verifiera utdata

Bygg och starta appen:

```bash
dotnet run
```

Du bör se en konsollogg liknande:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Öppna någon av de genererade `.txt`‑filerna—där är den extraherade texten. Om en fil är tom, dubbelkolla bildkvaliteten; OCR fungerar bäst med klar, högkontrasttext.

### Snabb verifierings‑script (valfritt)

Om du vill försäkra dig om att varje PNG fick en motsvarande textfil, kör detta lilla PowerShell‑enradsskript:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Vanliga variationer & kantfall

| Situation | Vad som ska ändras |
|-----------|--------------------|
| **Icke‑latinska språk** (t.ex. kyrilliska) | `ocrEngine.Language = Language.Cyrillic;` |
| **Stort bildset (>10 000 filer)** | Använd `Parallel.ForEach` för att snabba upp bearbetningen, men håll koll på GPU‑minnesanvändning. |
| **Behöver behålla originalordning på bilder** | Sortera `pngFiles` innan `foreach` (`Array.Sort(pngFiles);`). |
| **Kör på en CI‑server utan GPU** | Ersätt `GpuOcrEngine` med `OcrEngine` för att undvika GPU‑initieringsfel. |
| **Du vill bara bearbeta filer som innehåller ett specifikt nyckelord** | Efter att `result.Text` hämtats, kontrollera `result.Text.Contains("Invoice")` innan du skriver filen. |

Dessa justeringar låter dig anpassa **konvertera bilder till text**‑pipen till nästan alla scenarier du kan stöta på.

## Fullständig källkod (kopiera‑klistra‑redo)

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

Spara detta som `Program.cs`, kör `dotnet run`, och se magin hända.

## Slutsats

Du har nu ett **komplett, produktionsklart sätt att extrahera text från PNG**‑filer med C#. Handledningen täckte allt—from att sätta upp projektet, initiera en GPU‑accelererad OCR‑motor, **loopa igenom bilder**, till **batch OCR‑bilder** och spara resultaten som ren text.  

Om du är nyfiken på nästa steg, prova:

- **Konvertera bilder till text** för andra format (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}