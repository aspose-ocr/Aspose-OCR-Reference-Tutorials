---
category: general
date: 2026-05-25
description: igenkänna text från bild med Aspose OCR i C#. Lär dig hur du laddar bild
  för OCR, ställer in OCR-språk, skapar OCR-motor och extraherar text från TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: sv
og_description: Känn igen text från en bild med Aspose OCR i C#. Denna handledning
  visar hur du skapar en OCR-motor, laddar en bild för OCR, ställer in OCR-språk och
  extraherar text från en TIFF.
og_title: igenkänn text från bild med Aspose OCR – Komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Känn igen text från bild med Aspose OCR – Komplett C#‑guide
url: /sv/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# igenkänna text från bild med Aspose OCR – Komplett C# Guide

Har du någonsin behövt **igenkänna text från bild** men varit osäker på vilket bibliotek som ger både hastighet och noggrannhet? Du är inte ensam. I många fakturahanterings‑ eller arkiveringsprojekt är den största smärtan att få ren, sökbar text ur TIFF‑filer utan att skriva en egen parser.

Här är grejen: Aspose OCR för .NET gör hela pipeline till en barnlek. I den här guiden går vi igenom allt du behöver—installera paketet, **creating OCR engine**, ladda en TIFF, ställa in OCR‑språket och slutligen **extracting text from TIFF**. I slutet har du en färdig konsolapp som kan **recognize text from image**‑filer på ett ögonblick.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Core och .NET Framework)
- Visual Studio 2022 (eller någon IDE du föredrar)
- Aspose.OCR NuGet‑paket (GPU‑stöd kräver `Aspose.OCR.Gpu`‑tillägget)
- Ett GPU med CUDA‑stöd om du vill ha extra hastighet (valfritt men rekommenderas)

> **Pro tip:** Om du inte har ett GPU, hoppa bara över raden `GpuDevice` så kommer motorn automatiskt att falla tillbaka till CPU.

## Steg 1: Installera Aspose OCR och skapa OCR‑motor

Först, lägg till de nödvändiga paketen via NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Nu kan vi **create OCR engine**. Detta objekt är hjärtat i processen; det innehåller konfiguration såsom enheten att köra på och minnesgränser.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Varför detta är viktigt:** Genom att binda motorn till ett GPU minskar du dramatiskt tiden det tar att **recognize text from image**, särskilt för stora batcher av högupplösta TIFF‑filer.

## Steg 2: Ladda bild för OCR

Nästa steg, vi behöver **load image for OCR**. Aspose.OCR fungerar med `System.Drawing.Image`, så alla format som stöds av GDI+ (inklusive flersidiga TIFF) fungerar.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Om du hanterar en flersidig TIFF kan du loopa igenom sidorna med `image.SelectActiveFrame`, men för de flesta scenarier räcker ett enda anrop.

## Steg 3: Ställ in OCR‑språk

Motorn vet inte magiskt vilket språk du skannar. **Set OCR language** innan du kör igenkännaren; annars får du mycket förvrängd output.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Visste du?** Att byta språk vid körning är billigt—du kan till och med bearbeta ett blandat språk‑dokument genom att ändra denna egenskap mellan sidor.

## Steg 4: Utför igenkänning – Recognize Text from Image

Nu det roliga: faktiskt **recognize text from image**. Metoden `Recognize` returnerar en vanlig sträng med alla upptäckta tecken.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Om du behöver förtroendescore eller avgränsningsrutor kan du använda overloaden som returnerar ett `OcrResult`‑objekt, men för de flesta extraktionsuppgifter räcker den vanliga strängen.

## Steg 5: Extrahera text från TIFF (och hantera flersidiga filer)

När källan är en TIFF som innehåller flera sidor vill du upprepa steg 2‑4 för varje ram. Här är en snabb loop som **extracts text from TIFF** sida för sida:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

Koden ovan skriver ut den extraherade texten för varje sida, vilket gör det enkelt att skicka resultaten till en databas eller ett sökindex.

## Steg 6: Visa eller spara den extraherade texten

Till sist, låt oss **display the extracted text** och eventuellt skriva den till en fil för senare bearbetning.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Att köra programmet bör skriva ut de igenkända tecknen och skapa `extracted_text.txt` bredvid din käll‑TIFF.

---

## Vanliga frågor & kantfall

- **What if my GPU isn’t detected?**  
  Ta bort raden `GpuDevice`; motorn kommer automatiskt att växla till CPU‑läge. Prestandan blir långsammare men resultaten förblir korrekta.

- **Can I process PNG or JPEG files?**  
  Absolut—`Image.FromFile` fungerar med alla format som stöds av System.Drawing, så du kan **load image for OCR** oavsett filändelse.

- **How do I handle low‑resolution scans?**  
  Öka `ocrEngine.PreprocessOptions.Dpi` innan du anropar `Recognize`. Högre DPI ger motorn fler pixlar att arbeta med, vilket förbättrar noggrannheten.

- **Is there a limit to the size of the TIFF?**  
  Egenskapen `GpuMemoryLimit` begränsar GPU‑användning. Om du når gränsen kommer motorn att falla tillbaka till CPU för de återstående sidorna.

---

## Slutsats

Du har nu ett komplett, produktionsklart kodexempel som **recognize text from image**‑filer med Aspose OCR i C#. Handledningen täckte hur man **create OCR engine**, **load image for OCR**, **set OCR language** och **extract text from TIFF**—allt medan du utnyttjar GPU‑acceleration för hastighet.

Från och med nu kan du:

- Experimentera med olika språk (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified`, etc.).
- Integrera outputen i ett sökbart ElasticSearch‑index.
- Lägg till efterbearbetning (stavningskontroll, regex‑rengöring) för att förbättra datakvaliteten.

Prova det på din egen fakturabatch, justera minnesgränserna, och se OCR‑prestandan skjuta i höjden. Lycka till med kodningen!

## Relaterade handledningar

- [Extrahera bildtext C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extrahera text från bild – igenkänn rad med Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}