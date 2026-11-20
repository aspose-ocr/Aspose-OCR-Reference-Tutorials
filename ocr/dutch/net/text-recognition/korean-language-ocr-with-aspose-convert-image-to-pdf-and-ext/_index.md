---
category: general
date: 2026-05-28
description: Koreaans OCR-tutorial met Aspose in C#. Leer hoe je een afbeelding vanuit
  een stream laadt, platte tekst extraheert, de afbeelding naar PDF converteert en
  een doorzoekbare PDF exporteert.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: nl
og_description: Koreaans OCR in C# met Aspose. Stapsgewijze handleiding om een afbeelding
  vanuit een stream te laden, platte tekst te extraheren, afbeelding naar PDF te converteren
  en een doorzoekbare PDF te exporteren.
og_title: Koreaanse Taal OCR – Converteer afbeelding naar PDF & extraheer tekst (C#‑gids)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'Koreaans Taal OCR met Aspose: Converteer afbeelding naar PDF en extraheer
  tekst in C#'
url: /nl/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Korean Language OCR met Aspose: Afbeelding naar PDF converteren en tekst extraheren in C#

Heb je je ooit afgevraagd hoe je **Korean Language OCR** op een foto kunt uitvoeren zonder iets naar de cloud te sturen? Je bent niet de enige. Of je nu straatborden digitaliseert, bonnetjes verwerkt of een meertalige zoekindex bouwt, het lokaal kunnen herkennen van Koreaanse tekens kan je tijd, geld en privacy‑problemen besparen.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien hoe je **image from stream laadt**, **platte tekst extraheert**, **afbeelding naar PDF converteert**, en uiteindelijk **searchable PDF exporteert**—alles met Aspose.OCR en een paar regels C#. Geen externe services, geen verborgen magie—gewoon pure .NET‑code die je in elke console‑app kunt stoppen.

## Wat je na afloop kunt doen

- Een werkend console‑programma dat een JPEG‑bestand leest via een bestands‑stream.  
- Koreaanse tekst geëxtraheerd als platte Unicode‑strings.  
- Een gedetailleerd JSON‑rapport van de OCR‑run voor debugging of analyse.  
- Een searchable PDF die je in elke PDF‑lezer kunt openen en waar je de Koreaanse woorden daadwerkelijk kunt selecteren.  

**Prerequisites**  
- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).  
- Aspose.OCR for .NET NuGet‑package geïnstalleerd (`Install-Package Aspose.OCR`).  
- Een map die `korean_sign.jpg` bevat en een schrijfbare locatie voor de output‑bestanden.  

Als je deze onderdelen al klaar hebt, geweldig—laten we de handen uit de mouwen steken.

## Stap 1: Initialiseer de OCR‑engine voor Korean Language OCR

Het eerste wat je nodig hebt is een `OcrEngine`‑instance. Het inschakelen van de GPU (als je die hebt) versnelt de herkenning enorm, en het uitschakelen van automatische resource‑download dwingt de bibliotheek om de offline taalpakketten te gebruiken die je levert.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Waarom dit belangrijk is:**  
> *GPU‑versnelling* kan de verwerkingstijd van seconden naar milliseconden verkorten voor grote batches. Het instellen van `AutomaticResourceDownload` op `false` zorgt ervoor dat de demo offline werkt—een cruciale eis voor veel enterprise‑omgevingen.

## Stap 2: Afbeelding laden vanuit een stream

Het lezen van de afbeelding via een stream geeft je flexibiliteit: je kunt bestanden van schijf, netwerkschijven of zelfs geheugen‑gecachede blobs halen. Hier openen we een lokale JPEG‑file, maar hetzelfde patroon werkt voor elke `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tip:** Als je ooit afbeeldingen moet verwerken die via een web‑API zijn geüpload, vervang dan `File.OpenRead` door de binnenkomende `IFormFile.OpenReadStream()`—de rest blijft identiek.

## Stap 3: Kies Korean Language en pas Pre‑Processing filters toe

Aspose.OCR ondersteunt een handvol preprocessing‑stappen die de afbeelding opschonen vóór herkenning. Voor Koreaanse borden zijn meestal deskewing en denoising voldoende.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Wat gebeurt er onder de motorkap?**  
> Het `Deskew`‑filter maakt gedraaide tekst recht, terwijl `Denoise` korrel verwijdert die de karakter‑classifier kan verwarren. Het overslaan van deze stappen leidt vaak tot onleesbare output, vooral bij foto’s met lage resolutie.

## Stap 4: Platte tekst asynchroon extraheren

Nu volgt het moment van de waarheid—de engine vragen de tekens te herkennen en ons een schone string te geven. Het gebruik van `RecognizeAsync` houdt de UI responsief als je dit in een desktop‑ of web‑app embedt.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Wanneer je het programma uitvoert, zie je ongeveer het volgende:

```
OCR complete. Extracted text:
서울시청
```

> **Waarom async?**  
> OCR kan CPU‑intensief zijn. Asynchrone uitvoering voorkomt dat je thread blokkeert, wat vooral handig is in ASP.NET Core waar thread‑starvation een reëel probleem is.

## Stap 5: Verkrijg een gedetailleerd herkenningsresultaat en sla op als JSON

Soms heb je meer nodig dan alleen de ruwe string—misschien wil je confidence‑scores, bounding boxes, of de originele afbeeldingsdata. De `RecognizeDetailed`‑methode retourneert een `RecognitionResult`‑object dat naar JSON kan worden geserialiseerd voor latere analyse.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

Het openen van `korean_ocr.json` onthult een structuur die er ongeveer zo uitziet:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Wanneer gebruik je dit?**  
> Als je een zoekindex bouwt, laten de confidence‑waarden je low‑quality resultaten filteren. Als je tekst in een UI wilt highlighten, zijn de bounding boxes je kaart.

## Stap 6: Afbeelding naar PDF converteren en searchable PDF exporteren

Aspose maakt de sprong van raster naar vector moeiteloos. Door `OutputFormat` in te stellen op `SearchablePdf` embeddeert de bibliotheek de originele afbeelding en legt een onzichtbare tekstlaag met de OCR‑output erover. De resulterende PDF kan worden doorzocht, gekopieerd en geïndexeerd net als elke native PDF.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Open `korean_searchable.pdf` in Adobe Reader of een andere PDF‑viewer, druk op **Ctrl+F**, typ een Koreaans woord, en zie hoe het direct naar de juiste plek op de pagina springt. Dat is de kracht van een searchable PDF.

> **Extra tip:** Als je alleen een visuele PDF zonder de verborgen tekstlaag nodig hebt, verander `OutputFormat` naar `Pdf`.

## Volledig werkend voorbeeld

Hieronder staat het complete programma—kopieer, plak, vervang `YOUR_DIRECTORY` door een echt pad, en druk op **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Verwachte console‑output

```
OCR complete. Extracted text:
서울시청
```

En je vindt drie nieuwe bestanden naast je bron‑afbeelding:

- `korean_ocr.json` – volledige herkenningsdata.  
- `korean_searchable.pdf` – een PDF die je kunt doorzoeken.  
- (optioneel) eventuele tussen‑logbestanden die je toevoegt.

## Veelgestelde vragen & randgevallen

**Wat als ik geen GPU heb?**  
Stel `EnableGpu = false`; de CPU‑fallback is prima voor kleine batches.

**Kan ik meerdere afbeeldingen in één run verwerken?**  
Zeker. Plaats de kernlogica in een `foreach (var file in Directory.GetFiles(...))`‑loop en wijs `ocrEngine.Image` elke iteratie opnieuw toe.

**Hoe verwerk ik andere talen samen met Koreaans?**  
Aspose.OCR laat je `Language = Language.AutoDetect` instellen of talen combineren met de bitwise OR‑operator (bijv. `Language.Korean | Language.English`).

**Wat als de OCR‑confidence laag is?**  
Inspecteer `detailedResult.Pages[0].Words` en filter items met `Confidence < 0.7`. Je kunt ook de preprocessing‑filters aanpassen—probeer `PreprocessFilter.ContrastEnhancement` toe te voegen.

## Afronden

Je hebt zojuist gezien hoe je **Korean Language OCR** end‑to‑end uitvoert, van **image from stream laden** tot **plain text extraheren**, vervolgens **image naar PDF converteren** en uiteindelijk **searchable PDF exporteren**. De aanpak is modulair, zodat je de afbeeldingsbron kunt vervangen, het output‑formaat kunt wijzigen, of de JSON in elke downstream‑pipeline kunt injecteren.

Wat volgt


## Gerelateerde tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}