---
category: general
date: 2026-05-21
description: Voer OCR uit op een afbeelding met C#. Leer hoe je een afbeelding laadt
  voor OCR, tekst uit een PNG extraheert en tekst uit een afbeelding herkent met een
  klein codevoorbeeld.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: nl
og_description: Voer snel OCR uit op een afbeelding in C#. Deze gids laat zien hoe
  je een afbeelding laadt voor OCR, tekst uit een PNG extraheert en tekst uit een
  afbeelding herkent met lay-outbewuste HTML-output.
og_title: Voer OCR uit op een afbeelding met C# – Volledige programmeertutorial
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Voer OCR uit op een afbeelding met C# – Complete stap‑voor‑stap gids
url: /nl/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding met C# – Complete stapsgewijze handleiding

Heb je je ooit afgevraagd hoe je **OCR op afbeelding** kunt uitvoeren zonder te worstelen met zware GUI's? Je bent niet de enige. Of je nu bonnen digitaliseert, gegevens uit gescande formulieren haalt, of gewoon een PNG wilt omzetten naar doorzoekbare tekst, een paar regels C# kunnen de klus klaren.

In deze tutorial lopen we stap voor stap door het laden van een afbeelding voor OCR, het herkennen van tekst uit een afbeelding, en uiteindelijk het extraheren van tekst uit een PNG als schone HTML. Aan het einde heb je een kant‑klaar console‑applicatie die **OCR op afbeelding uitvoert** en de oorspronkelijke lay-out behoudt.

## Wat je gaat bouwen

- Een minimaal console‑programma dat een PNG (of elke ondersteunde afbeelding) leest  
- Gebruikt een OCR‑engine om **tekst uit afbeelding te herkennen**  
- Slaat het resultaat op als lay-out‑bewuste HTML, waarbij de oorspronkelijke afbeelding wordt ingebed  
- Toont hoe je **afbeelding laadt voor OCR**, **tekst uit PNG extraheert**, en veelvoorkomende randgevallen afhandelt  

> **Prerequisites**  
> - .NET 6.0 SDK of later (je kunt ook targeten op .NET Framework 4.7+)  
> - Een NuGet‑compatibele OCR‑bibliotheek – het voorbeeld gebruikt *Aspose.OCR* maar elke bibliotheek met een vergelijkbare API werkt  
> - Basiskennis van C# (niets geavanceerd)  

Heb je die? Geweldig—laten we erin duiken.

## OCR uitvoeren op afbeelding – Volledige code‑overzicht

Hieronder staat het **volledige, uitvoerbare** programma. Kopieer‑en‑plak het in een nieuw console‑project (`dotnet new console`) en druk op **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Expected output**  
> ```
> HTML with layout saved.
> ```  
> Na het uitvoeren vind je `form.html` naast je PNG. Open het in een browser en je ziet exact dezelfde lay-out, maar nu is de tekst selecteerbaar en doorzoekbaar.

### Afbeelding laden voor OCR

De regel `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` is waar we **afbeelding laden voor OCR**. De `ImageStream`‑helper abstraheert de bestandsformaatdetails, zodat je JPEG, BMP of TIFF kunt invoeren zonder de code aan te passen.  

**Waarom niet gewoon een `Bitmap` doorgeven?**  
Omdat veel OCR‑SDK's een stream verwachten die ook DPI‑metadata bevat. Het gebruik van de ingebouwde loader van de bibliotheek garandeert dat de engine de afbeelding precies ziet zoals deze op het scherm verschijnt, wat de nauwkeurigheid verbetert.

#### Pro tip
Als je een batch bestanden verwerkt, wikkel dan de laadstap in een `try/catch` en log eventuele `FileNotFoundException`. Dat voorkomt dat de hele batch crasht omdat één bestand ontbreekt.

### Tekst extraheren uit PNG

Zodra `engine.Recognize()` voltooid is, bevat de OCR‑engine de herkende tekst intern. Je kunt deze als een string ophalen als je alleen ruwe tekst nodig hebt:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Dit is de snelste manier om **tekst uit PNG te extraheren** wanneer je niet om de lay-out geeft. Voor de meeste data‑invoertaken is platte tekst voldoende—onthoud alleen om regeleinden te trimmen als je van plan bent te importeren in een CSV.

### Tekst herkennen uit afbeelding

De `Recognize()`‑aanroep doet het zware werk. Intern:

1. Normaliseert de afbeelding (corrigeert scheefstand, verwijdert ruis)  
2. Segmenteert deze in regels en woorden  
3. Voert een neurale‑netwerk‑classifier uit die getraind is op miljoenen glyphs  

Omdat we `Language = OcrLanguage.English` hebben ingesteld, past de engine Engels‑specifieke woordenboeken toe, wat valse positieven sterk vermindert. Als je meertalige ondersteuning nodig hebt, geef dan simpelweg een array van talen door:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Layout‑bewuste HTML‑output verwerken

De meeste ontwikkelaars stoppen bij platte tekst, maar de `HtmlSaveOptions` die we gebruikten laten je **OCR op afbeelding uitvoeren** en de visuele structuur behouden. Twee vlaggen zijn belangrijk:

- `PreserveLayout = true` – behoudt kolommen, tabellen en spatiëring.  
- `EmbedImages = true` – voegt de originele PNG in als een Base64‑gecodeerd `<img>`‑element, zodat de HTML zelf‑voorzienend is.

Als je een lichter bestand wilt, stel dan `EmbedImages = false` in en de HTML zal in plaats daarvan naar de originele PNG op schijf verwijzen.

#### Randgeval: Grote bestanden

Voor afbeeldingen groter dan 5 MB kan het insluiten de HTML‑grootte enorm doen toenemen. In zulke gevallen, schakel over naar externe afbeeldingsreferenties en overweeg de PNG vooraf te comprimeren met `ImageProcessor.Compress`.

## Veelvoorkomende valkuilen en pro‑tips

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Vervormde tekens | Verkeerde taal ingesteld of ontbrekend taalpakket | Installeer de juiste taaldatabestanden en stel `engine.Language` correct in |
| Geen tekst in output | Afbeelding is te donker of heeft lage resolutie | Pre‑process met `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Lay‑out kapot in HTML | `PreserveLayout` staat op standaard `false` | Stel `PreserveLayout = true` in `HtmlSaveOptions` in |
| Trage verwerking bij veel pagina's | Engine initialiseert opnieuw per bestand | Herbruik dezelfde `OcrEngine`‑instantie en wijzig alleen `engine.Image` in elke lus |

### Schalen naar meerdere bestanden

Als je **OCR op afbeelding** moet uitvoeren voor bestanden in een map, wikkel dan de kernlogica in een eenvoudige lus:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Merk op dat we **afbeelding laden voor OCR** binnen de lus doen, maar dezelfde `engine`‑ en `htmlOptions`‑objecten behouden. Dit vermindert geheugen‑churn en versnelt batch‑taken.

## Verder gaan: Exporteren naar PDF of DOCX

Dezelfde `engine` kan opslaan naar andere formaten:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Als je downstream‑systeem doorzoekbare PDF's verwacht, is dit een wijziging van één regel—geen aparte conversiepijplijn nodig.

## Conclusie

We hebben je zojuist laten zien hoe je **OCR op afbeelding** kunt uitvoeren met C#, van het laden van de afbeelding tot **tekst uit PNG extraheren** en uiteindelijk **tekst uit afbeelding herkennen** in een layout‑bewuste HTML‑bestand. Het volledige voorbeeld is klaar om te draaien, en je begrijpt nu waarom elke stap belangrijk is, hoe je het kunt afstemmen voor verschillende talen, en op welke valkuilen je moet letten.

Probeer nu de Engelse taal te vervangen door een andere locale, experimenteer met `PreserveLayout = false` om een slankere HTML te krijgen, of stuur de platte‑tekstoutput naar een database voor doorzoekbare archieven. De mogelijkheden zijn eindeloos wanneer je een krachtige OCR‑engine combineert met een paar regels C#.

Heb je vragen over het verwerken van multi‑page TIFF's, of wil je weten hoe je dit integreert in een ASP.NET Core API? Laat een reactie achter hieronder, en happy coding!

## Gerelateerde tutorials

- [Afbeeldingstekst extraheren met C# en taalkeuze met Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hoe tekst uit afbeelding extraheren door rechthoeken voor te bereiden in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Tekst uit afbeelding extraheren – Regel herkennen met Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}