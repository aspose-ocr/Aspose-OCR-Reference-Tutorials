---
category: general
date: 2026-02-28
description: Skapa sökbar PDF i C# genom att kombinera bilder vertikalt. Lär dig hur
  du staplar bilder vertikalt och konverterar skannade sidor till PDF med Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: sv
og_description: Skapa sökbar PDF i C# genom att kombinera bilder vertikalt. Denna
  guide visar hur du staplar bilder vertikalt och konverterar skannade sidor till
  PDF med Aspose OCR.
og_title: Skapa sökbar PDF i C# – Kombinera bilder vertikalt
tags:
- Aspose OCR
- C#
- PDF generation
title: Skapa sökbar PDF i C# – Kombinera bilder vertikalt
url: /sv/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa sökbar PDF i C# – Kombinera bilder vertikalt

Har du någonsin behövt **create searchable PDF** från ett fåtal skannade PNG-filer men var osäker på var du skulle börja? Du är inte ensam. I många dokument‑automationsprojekt är den största smärtan att omvandla en hög med bildfiler till en prydlig, sökbar PDF som du kan indexera och dela.

I den här handledningen går vi igenom ett komplett, färdigt‑att‑köra exempel som visar dig **how to stack images vertically**, **combine images vertically**, och slutligen **convert scanned pages PDF** till ett enda sökbart dokument med Aspose.OCR:s GPU‑accelererade motor. I slutet har du ett självständigt program som du kan släppa in i vilken .NET‑lösning som helst.

> **Vad du kommer att lära dig**
> - Initiera en OCR-motor med GPU‑stöd.
> - Bearbeta en batch av bilder parallellt.
> - **Combine images vertically** för att efterlikna en flersidig skanning.
> - Exportera en sökbar PDF och en detaljerad JSON‑rapport för efterföljande analys.

## Förutsättningar

- .NET 6+ (koden kompileras med .NET 6, .NET 7 eller .NET 8)
- Aspose.OCR NuGet‑paket (`Install-Package Aspose.OCR`)
- En GPU‑aktiverad maskin om du vill behålla `ProcessingMode.Gpu`‑inställningen (CPU‑fallback fungerar också)
- En mapp med några skannade PNG/JPEG‑filer (demot använder `page1.png`, `page2.png`, `page3.png`)

Inga externa tjänster, inga dolda konfigurationsfiler—bara ren C#.

## Steg 1 – Ställ in OCR‑motorn för att **Create Searchable PDF**

Först skapar vi en `OcrEngine`, slår på GPU‑acceleration, väljer engelska som språk och lägger till ett par förbehandlingsfilter. Dessa filter förbättrar noggrannheten genom att räta upp snedvridna sidor (`DeskewFilter`) och ta bort brus (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Varför detta är viktigt:** OCR‑motorn gör det tunga arbetet med att känna igen text. Att aktivera `ProcessingMode.Gpu` kan halvera igenkänningstiden på ett modernt grafikkort, medan filtren minskar vanliga skanningsartefakter som annars skulle ge förvrängd output.

## Steg 2 – Konfigurera en batch‑processor för att **Convert Scanned Pages PDF** effektivt

Att bearbeta varje sida en efter en är okej för ett par bilder, men i verkliga projekt involverar man ofta dussintals eller hundratals sidor. Aspose.OCR:s `OcrBatchProcessor` låter oss köra igenkänningar parallellt, vilket dramatiskt snabbar upp steget **convert scanned pages pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro tip:** Om du kör på en enbart CPU‑maskin, sätt `ProcessingMode = ProcessingMode.Cpu`. Batch‑processorn kommer fortfarande att respektera `MaxDegreeOfParallelism`, så du kan justera den för att undvika att överbelasta maskinen.

## Steg 3 – Kör OCR på batchen och samla resultat

Nu känner vi faktiskt igen texten. Metoden `Recognize` returnerar en lista med `OcrResult`‑objekt, där varje innehåller både originalbilden och den extraherade texten.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Vid detta tillfälle har du allt du behöver för att **create searchable PDF**: bilderna (fortfarande i minnet) och de associerade textlagren.

## Steg 4 – **Combine Images Vertically** och generera den sökbara PDF‑en

De flesta skannade dokument är flersidiga PDF‑er, så vi måste sy ihop de enskilda sidbilderna till en hög bild som speglar en fysisk stapel. Aspose.OCR tillhandahåller `Image.CombineVertical` just för det ändamålet.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Den resulterande filen (`combined_searchable.pdf`) innehåller markerbar, sökbar text under varje sidbild—precis vad du behöver för att **create searchable PDF** från skannade källor.

![Exempel på skapa sökbar PDF](/images/create-searchable-pdf.png "exempel på skapa sökbar pdf")

*Bildtext: exempel på skapa sökbar pdf som visar en kombinerad PDF med sökbar text.*

**Varför vertikal stapling?** Många OCR‑bibliotek behandlar varje bild som en separat sida. Genom att stapla dem behåller vi PDF‑ens sidordning intakt samtidigt som vi utnyttjar ett enda OCR‑pass för hela dokumentet.

## Steg 5 – Exportera detaljerad JSON för den första sidan (Perfekt för efterföljande arbetsflöden)

Ibland behöver du mer än en PDF; kanske vill du mata OCR‑data i en databas eller en maskininlärningspipeline. Aspose.OCR låter dig serialisera varje `OcrResult` till JSON, vilket bevarar avgränsningsrutor, förtroendescore och mer.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Förväntat JSON‑utdrag (trunkerat):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Du kan nu mata in denna JSON i vilket efterföljande system som helst—oavsett om du indexerar texten i Elasticsearch eller matar den till en anpassad analysdashboard.

---

## Hur man **Stack Images Vertically** – En snabb sammanfattning

Om du undrar **how to stack images vertically** utan Aspose, kan du använda `System.Drawing` för att skapa en ny bitmap och rita varje sida efter varandra. Dock hanterar Aspose:s inbyggda `Image.CombineVertical` DPI, pixelformat och minneshantering åt dig, vilket gör det till det mest pålitliga valet för produktionskod.

### Alternativ: Använda `System.Drawing` (bara av nyfikenhet)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Den manuella metoden fungerar, men du förlorar bekvämligheten med automatisk DPI‑hantering och möjligheten att direkt mata resultatet tillbaka i `RecognizeToPdf`. Håll dig till `CombineVertical` om du inte har ett mycket specifikt krav.

## Vanliga fallgropar & hur man undviker dem

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑memory errors** vid bearbetning av dussintals högupplösta skanningar | Varje bild förblir i minnet tills PDF‑en skrivs | Disposera `Image`‑objekt så snart du är klar (`using`‑block) eller skala ner bilder innan sammanslagning |
| **Garbage text** efter OCR | Snedvridna skanningar eller låg kontrast | Behåll `DeskewFilter` och `DenoiseFilter`; överväg att lägga till `ContrastFilter` om det behövs |
| **Missing searchable layer** | Använde `Recognize` istället för `RecognizeToPdf` | Se till att du anropar `ocrEngine.RecognizeToPdf` på den kombinerade bilden |
| **GPU fallback fails** på maskiner utan rätt drivrutiner | `ProcessingMode.Gpu` kastar ett undantag | Omslut motorinstansiering i ett try/catch‑block och falla tillbaka till `ProcessingMode.Cpu` |

## Nästa steg – Utöka arbetsflödet

Nu när du vet hur man **create searchable PDF**, kanske du vill:

- **Batch‑process entire folders** med `Directory.GetFiles` och en `foreach`‑loop.
- **Add watermarks** till varje sida före sammanslagning (använd `ImageProcessor` från Aspose.Imaging).
- **Split the searchable PDF back into individual pages** om du senare behöver enskilda PDF‑sidor (`PdfDocument.Split` från Aspose.PDF).
- **Integrate with Azure Blob Storage** för att hämta bilder från molnet och skicka tillbaka den slutgiltiga PDF‑en.

Alla dessa tillägg involverar naturligtvis samma grundkoncept: OCR‑uppsättning, bildhantering och PDF‑export.

---

## Slutsats

Vi har gått igenom allt du behöver för att **create searchable PDF** från en samling skannade bilder i C#. Genom att initiera en GPU‑aktiverad `OcrEngine`, köra en parallell batch med `OcrBatchProcessor`, **combining images vertically**, och slutligen anropa `RecognizeToPdf`, får du ett prydligt, sökbart dokument redo för arkivering eller indexering. Den extra JSON‑exporten ger dig full insyn i OCR‑resultaten, vilket öppnar dörrar för analys eller anpassade arbetsflöden.

Prova det, experimentera med olika filter, och se hur ditt dokument‑automationspipeline blir mycket smidigare. Om du stöter på några konstigheter, lämna en kommentar—lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}