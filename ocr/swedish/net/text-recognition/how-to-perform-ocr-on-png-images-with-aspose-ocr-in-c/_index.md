---
category: general
date: 2026-11-26
description: Lär dig hur du utför OCR på PNG-filer, konverterar PNG till text och
  extraherar kyrillisk text med Aspose.OCR – steg‑för‑steg‑guide för utvecklare.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: sv
lastmod: 2026-11-26
og_description: Hur man utför OCR på PNG-filer och extraherar kyrillisk text med Aspose.OCR
  i C#. Följ den här kompletta handledningen för att konvertera PNG till text.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Hur man utför OCR på PNG‑bilder med Aspose.OCR – C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Hur man utför OCR på PNG‑bilder med Aspose.OCR i C#
url: /sv/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på PNG‑bilder med Aspose.OCR i C#

Om du behöver **hur man utför OCR** på en PNG‑fil, visar den här guiden de exakta stegen för att konvertera PNG till text med Aspose.OCR. Oavsett om du extraherar kyrillisk text från skannade dokument eller helt enkelt känner igen text från PNG‑skärmbilder, fungerar lösningen direkt och kräver bara några få rader C#‑kod.

I den här handledningen kommer du att lära dig hur du:

* **ladda bild för OCR** från en lokal mapp,
* konfigurera motorn för att **extrahera kyrillisk text**,
* **känna igen text från PNG** och få en ren sträng,
* hantera vanliga fallgropar såsom saknade språkmoduler och stora bilder.

Ingen förkunskap om Aspose.OCR krävs – bara en .NET‑utvecklingsmiljö och en PNG‑bild du vill bearbeta.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 (eller senare) installerat.
* En licensierad eller provversion av **Aspose.OCR for .NET**. Du kan få en gratis provversion från Aspose‑webbplatsen.
* Visual Studio 2022 (eller någon IDE som stödjer .NET).
* En PNG‑fil som innehåller den text du vill extrahera (exemplet använder `sample_image.png`).

## Steg 1: Installera Aspose.OCR NuGet‑paketet

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.OCR
```

Paketet innehåller OCR‑motorns kärna och alla språkmoduler. När du begär ett språk som inte finns lokalt laddar Aspose.OCR automatiskt ner den nödvändiga modulen.

## Steg 2: Skapa en OCR‑motorsinstans (hur man utför OCR)

Det första praktiska steget i någon OCR‑arbetsflöde är att instansiera motorn. Detta objekt hanterar alla efterföljande operationer såsom att ladda bilden och utföra igenkänning.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Varför detta är viktigt:** Klassen `OcrEngine` kapslar in OCR‑pipelines. Att skapa en enda instans och återanvända den för flera bilder minskar minnesbelastningen och förbättrar prestandan.

## Steg 3: Ladda bild för OCR – ange käll‑PNG‑filen

Att ladda bilden är den punkt där du **ladda bild för OCR**. Aspose.OCR accepterar flera inmatningstyper; den enklaste är `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Proffstips:** Använd en absolut sökväg eller `Path.Combine` för att undvika körningsfel i olika miljöer.

### Hantera stora bilder

Om PNG‑filen är större än 2 MB, överväg att skala ner den innan igenkänning för att snabba upp bearbetningen:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Steg 4: Konfigurera språk – extrahera kyrillisk text

Som standard antar Aspose.OCR engelska. För att **extrahera kyrillisk text**, sätt egenskapen `Language` till `Language.Cyrillic`. Den nödvändiga modulen laddas ner automatiskt första gången du kör koden.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Om du behöver känna igen flera språk (t.ex. engelska och kyrilliska) kan du kombinera dem:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Edge case: Saknad språkmodul

Om nedladdningen misslyckas (t.ex. i en offline‑miljö) kastar motorn ett `OcrException`. Fånga det för att erbjuda en smidig återgång:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Steg 5: Utför igenkänningsoperationen (känna igen text från PNG)

Nu när bilden och språket är inställda kan du **känna igen text från PNG**. Metoden `Recognize` kör OCR‑pipelinesynkron.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Varför det fungerar:** Internt applicerar Aspose.OCR förbehandling (binarisering, brusreducering) innan bilden matas in i en neuronnätsbaserad igenkännare som är fininställd för det valda språket.

## Steg 6: Hämta och visa den igenkända texten (konvertera PNG till text)

Efter igenkänning är den extraherade strängen tillgänglig via egenskapen `Text`. Detta är det sista steget i **konvertera PNG till text**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Förväntad utdata

Om `sample_image.png` innehåller den kyrilliska frasen “Привет мир”, kommer konsolen att visa:

```
=== OCR Result ===
Привет мир
```

Utdata kan innehålla radbrytningar och skiljetecken exakt som de förekommer i bilden. Du kan efterbehandla strängen med `String.Trim()`, `Regex` eller andra verktyg för text‑rengöring om så behövs.

## Steg 7: Valfritt – Spara resultatet till en fil

Att lagra OCR‑resultatet möjliggör efterföljande bearbetning (t.ex. indexering, översättning). Här är ett snabbt sätt att skriva texten till en UTF‑8‑fil:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Vanliga fallgropar och hur man undviker dem

| Problem | Symtom | Lösning |
|-------|----------|-----|
| **Saknad språkmodul** | `OcrException` på `Language = Language.Cyrillic` | Säkerställ internetanslutning första gången eller för‑ladda moduler via Asposes offline‑paket. |
| **Suddig eller lågkontrastbild** | Dålig noggrannhet, många “?”‑tecken | Förbehandla bilden: öka kontrast, applicera skärpning eller konvertera till gråskala innan du skickar den till motorn. |
| **Mycket stor PNG** | Lång bearbetningstid, eventuell `OutOfMemoryException` | Skala ner som visas i Steg 3, eller dela en flersidig bild i separata kakel. |
| **Icke‑UTF‑8‑tecken** | Förvrängd utdata | Verifiera att konsolen eller filskrivaren använder UTF‑8‑kodning (`Encoding.UTF8`). |

## Fullt, körbart exempel

Nedan är det kompletta programmet som inkluderar alla stegen ovan. Kopiera det till ett nytt konsolprojekt och kör det efter att du justerat filsökvägarna.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Hur det fungerar

1. **Motorinstans** – förbereder OCR‑pipelines.  
2. **Bildladdning** – stödjer både rå PNG och nedskalade versioner för prestanda.  
3. **Språkväljning** – demonstrerar **extrahera kyrillisk text** samtidigt som saknade moduler hanteras.  
4. **Igenkänning** – huvudanropet **känna igen text från PNG**.  
5. **Resultathantering** – visar **konvertera PNG till text** och skriver utdata till en fil.

Kör programmet med `dotnet run`. Om allt är korrekt konfigurerat ser du den igenkända texten skriven i konsolen och sparad i `ocr_output.txt`.

## Slutsats

I den här handledningen har du lärt dig **hur man utför OCR** på PNG‑filer med Aspose.OCR för .NET, från **ladda bild för OCR** till **extrahera kyrillisk text** och **konvertera PNG till text**. Det kompletta, körbara exemplet demonstrerar standardarbetsflödet, vanliga edge‑cases och praktiska tips som håller din OCR‑pipeline pålitlig.

**Nästa steg**

* Utforska **känna igen text från PNG** med ytterligare språk (arabiska, kinesiska) genom att kombinera `Language`‑flaggor.  
* Integrera OCR‑resultatet med Azure Cognitive Search för sökbara dokumentarkiv.  
* Experimentera med Aspose.OCR:s `OcrEngine`‑inställningar såsom `Resolution`


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man laddar ner Aspose.OCR‑modell och extraherar text från PNG i C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Hur man utför OCR i C# – känna igen kyrillisk text med Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Hur man batch‑OCR i C# – snabbt sätt att extrahera text från PNG‑filer](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}