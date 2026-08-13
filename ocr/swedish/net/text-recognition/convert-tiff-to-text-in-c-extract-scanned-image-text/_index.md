---
category: general
date: 2026-03-05
description: Konvertera TIFF till text i C# med Aspose OCR—extrahera snabbt text från
  skannade bildfiler och lär dig hur du laddar bildfil i C# för OCR‑behandling.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: sv
og_description: Konvertera TIFF till text i C# med Aspose OCR. Lär dig hela arbetsflödet
  för att extrahera text från skannade bilder och ladda bildfiler effektivt.
og_title: Konvertera TIFF till text i C# – Extrahera text från skannad bild
tags:
- OCR
- C#
- Aspose
title: Konvertera TIFF till text i C# – Extrahera text från skannad bild
url: /sv/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera TIFF till text i C# – Extrahera text från skannade bilder

Behöver du **konvertera TIFF till text i C#**? Du är inte ensam som kämpar med flersidiga skannade bilder som envisas med att inte bli sökbara strängar.  
I den här guiden går vi igenom en komplett, färdigkörbar lösning som tar en TIFF‑fil, skickar den till Aspose OCR och ger dig ren text—utan extra tjänster, utan gömd magi.

> **Proffstips:** Om du arbetar med högupplösta skanningar kan aktivering av GPU‑bearbetning spara sekunder per sida.

Vi kommer också att visa hur du **extraherar text från skannade bild**‑filer och det bästa sättet att **ladda bildfil i C#** i OCR‑motorn, så att du kan integrera denna logik i vilket .NET‑projekt som helst idag.

---

## Vad du behöver

Innan vi dyker ner, se till att du har följande på din maskin:

| Krav | Orsak |
|------|-------|
| .NET 6.0+ (eller .NET Framework 4.7.2+) | Modern runtime, stödjer `Span<T>` och async I/O |
| Aspose.OCR för .NET (NuGet‑paket `Aspose.OCR`) | OCR‑motorn vi kommer att använda |
| En giltig Aspose OCR‑licensfil (`Aspose.OCR.lic`) | Utan den kommer du att träffa utvärderingsgränser |
| En TIFF‑fil (en‑ eller flersidig) för testning | Exempel som används: `scanned_multi_page.tif` |
| GPU med CUDA 11+ (valfritt) | Snabbar upp igenkänning när `EngineMode = Gpu` |

Om du saknar någon av dessa, hämta NuGet‑paketet nu:

```bash
dotnet add package Aspose.OCR
```

---

## Steg 1: Ställ in projektet och importera namnrymder

Skapa en ny konsolapp (eller lägg till koden i ett befintligt projekt). Det första vi gör är att importera de klasser vi behöver.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Varför detta är viktigt:** Att importera `Aspose.OCR.Image` ger oss `ImageStream`‑fabriken, som kan läsa TIFF‑filer direkt från disk eller en ström. Att hoppa över detta steg kommer att orsaka ett kompileringsfel.

---

## Steg 2: Initiera OCR‑motorn och välj bearbetningsläge

OCR‑motorn måste konfigureras **innan** du tilldelar någon bild. Här bestämmer vi om vi ska köra på CPU eller utnyttja GPU:n.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Om du kör på en huvudlös server utan grafikkort, ändra `Gpu` till `Cpu` eller `Auto`.*  
Motorns läge påverkar minnesallokering och hastighet; GPU‑läge kan vara 2‑3× snabbare på stora, högupplösta TIFF‑filer.

---

## Steg 3: Använd din Aspose OCR‑licens

Att köra utan licens begränsar dig till några få sidor och vattenstämplar. Ladda din licens tidigt så att varje efterföljande operation är obegränsad.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Vanligt fallgropp:** Att placera `SetLicense` efter `Recognize()` får motorn att återgå till provläget för det anropet.

---

## Steg 4: Ladda TIFF‑filen – hantera en- och flersidiga bilder

Aspose OCR kan läsa flersidiga TIFF‑filer direkt, men du måste mata in rätt ström. Här är ett robust mönster som fungerar för båda scenarierna.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Varför använda `ImageStream.FromFile`?

- Den abstraherar bort den underliggande `FileStream`, hanterar TIFF‑sidnumrering internt.  
- Den fungerar även med `MemoryStream`, så att du kan ladda bilder från en databas eller ett webb‑API utan att röra filsystemet.

### Särskilt fall: Mycket stora TIFF‑filer

Om din TIFF överstiger 200 MB, överväg att ladda den sida‑för‑sida för att undvika minnesutrymmes‑undantag:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Steg 5: Verifiera resultatet

När du kör programmet bör du se något liknande:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Om texten ser förvrängd ut, dubbelkolla:

1. **Upplösning** – OCR fungerar bäst med 300 dpi eller högre.  
2. **EngineMode** – Byt till `Cpu` om GPU‑drivrutinen är föråldrad.  
3. **Licens** – Säkerställ att licensfilens sökväg är korrekt och att filen är läsbar.

---

## Vanliga frågor (FAQ)

### Fungerar detta med andra bildformat?

Absolut. `ImageStream.FromFile` stödjer JPEG, PNG, BMP och till och med PDF (via Aspose.PDF). Byt bara filändelsen.

### Vad händer om jag behöver bearbeta bilder lagrade i en databas?

Läs BLOB‑en till en `MemoryStream` och skicka den till `ImageStream.FromStream(memoryStream)`. OCR‑motorn behandlar den på samma sätt som en fil‑baserad ström.

### Kan jag köra detta på Linux?

Ja—Aspose OCR är plattformsoberoende. Installera rätt .NET‑runtime och se till att de nödvändiga inhemska biblioteken för GPU (om de används) finns tillgängliga.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är hela programmet, redo att kompileras. Ersätt `YOUR_DIRECTORY` och licensfilens sökväg med dina faktiska platser.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Spara detta som `Program.cs`, kör `dotnet run` och se texten

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}