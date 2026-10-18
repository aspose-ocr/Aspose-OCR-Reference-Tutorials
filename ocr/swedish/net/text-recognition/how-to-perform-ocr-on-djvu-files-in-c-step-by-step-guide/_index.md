---
category: general
date: 2026-02-20
description: Hur man utför OCR på DjVu‑filer i C#. Lär dig att känna igen text från
  bild och konvertera DjVu till text snabbt med Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: sv
og_description: Hur man utför OCR på DjVu-filer i C#. Den här handledningen visar
  hur du känner igen text från bild, läser DjVu och konverterar DjVu till text med
  hjälp av Aspose OCR.
og_title: Hur man utför OCR på DjVu-filer i C# – Komplett guide
tags:
- OCR
- C#
- DjVu
- Aspose
title: Hur man utför OCR på DjVu-filer i C# – Steg‑för‑steg‑guide
url: /sv/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på DjVu-filer i C# – Komplett guide

Har du någonsin undrat **hur man utför OCR** på ett DjVu-dokument utan att rycka ur håret? Du är inte ensam. Många utvecklare stöter på problem när de behöver **identifiera text från bild**-källor som finns i DjVu-behållare. Den goda nyheten? Med några rader C# och Aspose OCR-biblioteket kan du extrahera den dolda texten på ett ögonblick.

I den här handledningen går vi igenom allt du behöver för att omvandla en DjVu-sida till vanlig text. I slutet kommer du att veta **hur man läser DjVu**, hur man **extraherar text från bild**-objekt, och till och med hur man **konverterar DjVu till text** för efterföljande bearbetning. Inga externa tjänster, inga vaga referenser – bara ett självständigt, körbart exempel.

## Förutsättningar

Innan vi dyker ner, se till att du har följande tillgängligt:

- .NET 6.0 SDK eller senare (koden fungerar även med .NET Framework 4.8).
- Visual Studio 2022 eller någon editor som stödjer C#.
- En Aspose OCR för .NET-licens (gratis provversion fungerar för testning).
- En exempel DjVu-fil (`sample.djvu`) placerad i en mapp du kan referera till.

Att ha dessa redo håller flödet smidigt – inga överraskningar med “saknad referens” senare.

## Så utför du OCR på en DjVu-sida

Kärnidén är enkel: ladda DjVu-sidan som en bild, skicka den till OCR-motorn och läs den resulterande strängen. Låt oss bryta ner det steg för steg.

### Steg 1: Installera Aspose OCR

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Det här hämtar de senaste Aspose OCR-binärerna och deras beroenden. Om du föredrar NuGet Package Manager UI, sök bara efter **Aspose.OCR** och klicka på **Install**.

### Steg 2: Initiera OCR-motorn

Att skapa en `OcrEngine`-instans är det första du gör när du vill **utföra OCR**. Tänk på det som att slå på skannerns hjärna.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Proffstips:** Att återanvända en enda `OcrEngine` för flera sidor sparar minne och snabbar upp bearbetningen.

### Steg 3: Ladda DjVu-sidan som en bild

DjVu-filer stöds inte direkt av de flesta bild‑API:er, men Aspose kan behandla varje sida som en bitmap. Här använder vi `System.Drawing.Image` för att läsa filen.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Varför detta fungerar:** `Image.FromFile` avkodar automatiskt DjVu‑strömmen till ett rasterformat som OCR‑motorn förstår. Om du behöver bearbeta en specifik sida från en fler‑sidig DjVu, använd Aspose PDF eller Aspose Imaging för att extrahera sidan först.

### Steg 4: Identifiera text från bild

Nu händer magin. Metoden `Recognize` skannar bitmapen och returnerar en sträng som innehåller de upptäckta tecknen.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

Vid den här punkten har du **identifierat text från bild**‑data som ursprungligen fanns i en DjVu-behållare. Strängen kan innehålla radbrytningar, skiljetecken och till och med Unicode‑tecken om källspråket stödjer dem.

### Steg 5: Visa eller lagra resultatet

För en snabb kontroll, skriv bara ut texten till konsolen. I en verklig applikation skulle du troligen skriva den till en fil eller en databas.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

När allt sätts ihop, här är det kompletta, körklara programmet.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Expected output** (truncated for brevity):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Om du ser förvrängda tecken, dubbelkolla att DjVu-filen inte är krypterad och att du har ställt in rätt språk i `ocrEngine.Language`. Som standard antas engelska; du kan byta till franska, tyska osv. genom att tilldela `ocrEngine.Language = Language.French;`.

## Identifiera text från bild – Vanliga fallgropar

Även med ett gediget exempel snubblar utvecklare ofta på några kantfall:

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Blank output** | Bildens upplösning är för låg (<300 dpi). | Använd `ocrEngine.ImageResolution = 300;` innan du anropar `Recognize`. |
| **Wrong language** | OCR använder som standard engelska. | Ställ in `ocrEngine.Language = Language.Spanish;` (eller något annat stödjande språk). |
| **Memory leak** | Stora DjVu‑sidor ligger kvar i minnet efter bearbetning. | Anropa `djvuPage.Dispose();` när du är klar. |
| **Multi‑page DjVu** | Endast den första sidan laddas. | Loopa igenom sidor med Aspose Imaging’s `DjvuImage`-klass. |

Att åtgärda dessa tidigt sparar dig otaliga felsöknings timmar.

## Så läser du DjVu-filer i C# – Utöver enkel OCR

Om ditt projekt kräver mer än en enda sida, måste du först extrahera varje sida som en bild. Aspose Imaging gör det smärtfritt:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Detta mönster låter dig **konvertera DjVu till text** sida för sida, perfekt för batch‑bearbetning av stora arkiv.

## Extrahera text från bild – Finjustera noggrannheten

Standard‑OCR‑inställningarna fungerar bra för rena skanningar, men du kan öka noggrannheten:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Dessa justeringar är särskilt användbara när DjVu‑källan innehåller handskrivna anteckningar eller lågkontrast‑grafik.

## Konvertera DjVu till text – Fullt end‑to‑end‑exempel

Nedan är en kompakt version som samlar allt: laddar en fler‑sidig DjVu, förbehandlar varje sida, utför OCR och sparar resultatet till en `.txt`‑fil.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

När du kör detta skript skapas `sample_extracted.txt` med varje sidas innehåll snyggt separerat. Det är det snabbaste sättet att **konvertera DjVu till text** för indexering, sökning eller arkivering.

## Slutsats

Vi har gått igenom **hur man utför OCR** på DjVu‑filer från början till slut, utforskat sätt att **identifiera text från

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}