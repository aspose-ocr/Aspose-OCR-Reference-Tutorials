---
category: general
date: 2026-02-28
description: Maak een doorzoekbare PDF in C# door afbeeldingen verticaal te combineren.
  Leer hoe je afbeeldingen verticaal stapelt en gescande PDF‑pagina's converteert
  met Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: nl
og_description: Maak een doorzoekbare PDF in C# door afbeeldingen verticaal te combineren.
  Deze gids laat zien hoe je afbeeldingen verticaal stapelt en gescande pagina's converteert
  naar PDF met Aspose OCR.
og_title: Maak doorzoekbare PDF in C# – Combineer afbeeldingen verticaal
tags:
- Aspose OCR
- C#
- PDF generation
title: Maak doorzoekbare PDF in C# – Combineer afbeeldingen verticaal
url: /nl/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zoekbare PDF maken in C# – Afbeeldingen verticaal combineren

Heb je ooit **zoekbare PDF** moeten maken van een handvol gescande PNG's, maar wist je niet waar je moest beginnen? Je bent niet de enige. In veel document‑automatiseringsprojecten is het grootste pijnpunt het omzetten van een stapel afbeeldingsbestanden naar één nette, doorzoekbare PDF die je kunt indexeren en delen.  

In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat je laat zien **hoe je afbeeldingen verticaal stapelt**, **afbeeldingen verticaal combineert**, en uiteindelijk **gescande pagina's PDF converteert** naar één doorzoekbaar document met de GPU‑versnelde engine van Aspose.OCR. Aan het einde heb je een zelfstandige applicatie die je in elke .NET‑oplossing kunt gebruiken.

> **Wat je zult leren**
> - Een OCR‑engine initialiseren met GPU‑ondersteuning.
> - Een batch afbeeldingen parallel verwerken.
> - **Afbeeldingen verticaal combineren** om een meer‑pagina scan na te bootsen.
> - Een doorzoekbare PDF exporteren en een gedetailleerd JSON‑rapport voor downstream‑analyse.

## Vereisten

- .NET 6+ (de code compileert met .NET 6, .NET 7 of .NET 8)
- Aspose.OCR NuGet‑pakket (`Install-Package Aspose.OCR`)
- Een GPU‑enabled machine als je de `ProcessingMode.Gpu` instelling wilt behouden (CPU‑fallback werkt ook)
- Een map met een paar gescande PNG/JPEG‑bestanden (de demo gebruikt `page1.png`, `page2.png`, `page3.png`)

Geen externe services, geen verborgen configuratiebestanden—alleen pure C#.

## Stap 1 – OCR‑engine instellen om **Zoekbare PDF maken**

Eerst maken we een `OcrEngine`, schakelen we GPU‑versnelling in, kiezen we Engels als taal, en voegen we een paar preprocessing‑filters toe. Deze filters verbeteren de nauwkeurigheid door scheve pagina's recht te zetten (`DeskewFilter`) en ruis te verwijderen (`DenoiseFilter`).

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

**Waarom dit belangrijk is:** De OCR‑engine doet het zware werk van het herkennen van tekst. Het inschakelen van `ProcessingMode.Gpu` kan de herkenningstijd halveren op een moderne grafische kaart, terwijl de filters veelvoorkomende scan‑artefacten verminderen die anders onleesbare output zouden opleveren.

## Stap 2 – Een batch‑processor configureren om **Convert Scanned Pages PDF** efficiënt te verwerken

Het verwerken van elke pagina één voor één is prima voor een paar afbeeldingen, maar real‑world projecten omvatten vaak tientallen of honderden pagina's. De `OcrBatchProcessor` van Aspose.OCR laat ons herkenningen parallel uitvoeren, waardoor de stap **convert scanned pages pdf** drastisch wordt versneld.

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

**Pro tip:** Als je op een alleen‑CPU machine werkt, stel dan `ProcessingMode = ProcessingMode.Cpu` in. De batch‑processor respecteert nog steeds `MaxDegreeOfParallelism`, zodat je het kunt afstemmen om overbelasting van de machine te voorkomen.

## Stap 3 – OCR uitvoeren op de batch en resultaten verzamelen

Nu herkennen we daadwerkelijk de tekst. De `Recognize`‑methode retourneert een lijst van `OcrResult`‑objecten, elk met zowel de originele afbeelding als de geëxtraheerde tekst.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Op dit punt heb je alles wat je nodig hebt om **zoekbare PDF te maken**: de afbeeldingen (nog in het geheugen) en de bijbehorende tekstlagen.

## Stap 4 – **Afbeeldingen verticaal combineren** en de zoekbare PDF genereren

De meeste gescande documenten zijn multi‑page PDF's, dus moeten we de afzonderlijke pagina‑afbeeldingen aan elkaar plakken tot één lange afbeelding die een fysieke stapel nabootst. Aspose.OCR biedt `Image.CombineVertical` precies voor dat doel.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Het resulterende bestand (`combined_searchable.pdf`) bevat selecteerbare, doorzoekbare tekst onder elke pagina‑afbeelding—precies wat je nodig hebt om **zoekbare PDF te maken** van gescande bronnen.

![Voorbeeld van zoekbare PDF maken](/images/create-searchable-pdf.png "voorbeeld van zoekbare pdf")

*Afbeeldings‑alt‑tekst: voorbeeld van zoekbare pdf toont een gecombineerde PDF met doorzoekbare tekst.*

**Waarom verticale stapeling?** Veel OCR‑bibliotheken behandelen elke afbeelding als een aparte pagina. Door ze te stapelen behouden we de paginavolgorde van de PDF intact, terwijl we toch één OCR‑pass voor het hele document gebruiken.

## Stap 5 – Gedetailleerde JSON exporteren voor de eerste pagina (handig voor downstream‑workflows)

Soms heb je meer nodig dan een PDF; misschien wil je de OCR‑gegevens in een database of een machine‑learning‑pipeline voeren. Aspose.OCR laat je elk `OcrResult` serialiseren naar JSON, waarbij bounding boxes, confidence‑scores en meer behouden blijven.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Verwacht JSON‑fragment (afgekapt):**

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

Je kunt deze JSON nu in elk downstream‑systeem voeren—of je nu de tekst indexeert in Elasticsearch of het naar een aangepast analytics‑dashboard stuurt.

---

## Hoe **Afbeeldingen verticaal stapelen** – Een snelle samenvatting

Als je je afvraagt **hoe je afbeeldingen verticaal stapelt** zonder Aspose, kun je `System.Drawing` gebruiken om een nieuwe bitmap te maken en elke pagina achter elkaar te tekenen. Echter, Aspose’s ingebouwde `Image.CombineVertical` regelt DPI, pixel‑formaat en geheugenbeheer voor je, waardoor het de meest betrouwbare keuze is voor productiecodel.

### Alternatief: `System.Drawing` gebruiken (alleen uit nieuwsgierigheid)

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

De handmatige aanpak werkt, maar je verliest het gemak van automatische DPI‑afhandeling en de mogelijkheid om het resultaat direct terug te voeren naar `RecognizeToPdf`. Blijf bij `CombineVertical` tenzij je een zeer specifieke eis hebt.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Out‑of‑memory errors** bij het verwerken van tientallen scans met hoge resolutie | Elke afbeelding blijft in het geheugen tot de PDF is geschreven | Dispose van `Image`‑objecten zodra je klaar bent (`using`‑blokken) of schaal afbeeldingen naar beneden voordat je combineert |
| **Garbage text** na OCR | Scheve scans of laag contrast | Behoud de `DeskewFilter` en `DenoiseFilter`; overweeg `ContrastFilter` toe te voegen indien nodig |
| **Ontbrekende doorzoekbare laag** | `Recognize` gebruikt in plaats van `RecognizeToPdf` | Zorg ervoor dat je `ocrEngine.RecognizeToPdf` aanroept op de gecombineerde afbeelding |
| **GPU fallback mislukt** op machines zonder juiste drivers | `ProcessingMode.Gpu` gooit een uitzondering | Omring engine‑creatie met try/catch en val terug op `ProcessingMode.Cpu` |

## Volgende stappen – Workflow uitbreiden

Nu je weet hoe je **zoekbare PDF** maakt, wil je misschien:

- **Batch‑verwerk volledige mappen** met `Directory.GetFiles` en een `foreach`‑lus.
- **Watermerken toevoegen** aan elke pagina vóór het combineren (gebruik `ImageProcessor` van Aspose.Imaging).
- **De zoekbare PDF splitsen in afzonderlijke pagina's** als je later per‑pagina PDF's nodig hebt (`PdfDocument.Split` van Aspose.PDF).
- **Integreren met Azure Blob Storage** om afbeeldingen uit de cloud te halen en de uiteindelijke PDF terug te plaatsen.

Al deze uitbreidingen maken natuurlijk gebruik van dezelfde kernconcepten: OCR‑configuratie, afbeeldingverwerking en PDF‑export.

---

## Conclusie

We hebben alles behandeld wat je nodig hebt om **zoekbare PDF** te maken van een verzameling gescande afbeeldingen in C#. Door een GPU‑enabled `OcrEngine` te initialiseren, een parallelle batch uit te voeren met `OcrBatchProcessor`, **afbeeldingen verticaal te combineren**, en uiteindelijk `RecognizeToPdf` aan te roepen, krijg je een nette, doorzoekbare document klaar voor archivering of indexering. De extra JSON‑export geeft volledige inzage in de OCR‑resultaten, waardoor mogelijkheden ontstaan voor analytics of aangepaste workflows.

Probeer het, experimenteer met verschillende filters, en zie hoe je document‑automatiseringspipeline veel soepeler wordt. Als je tegen problemen aanloopt, laat een reactie achter—veel plezier met coderen!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}