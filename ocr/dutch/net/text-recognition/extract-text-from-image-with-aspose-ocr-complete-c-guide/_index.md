---
category: general
date: 2026-05-28
description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Leer hoe je OCR‑tekst
  kunt extraheren, een afbeelding kunt laden voor OCR, en snel tekst uit TIF‑bestanden
  kunt herkennen.
draft: false
keywords:
- extract text from image
- how to extract ocr text
- load image for ocr
- recognize text from tif
language: nl
og_description: Tekst extraheren uit afbeelding met Aspose OCR in C#. Deze tutorial
  laat zien hoe je OCR‑tekst kunt extraheren, een afbeelding voor OCR kunt laden en
  tekst uit TIF‑bestanden kunt herkennen.
og_title: Tekst uit afbeelding extraheren met Aspose OCR – Complete C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  headline: Extract Text from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  name: Extract Text from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
    text: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
  - name: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
    text: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
  - name: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
    text: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Tekst extraheren uit afbeelding met Aspose OCR – Complete C#‑gids
url: /nl/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeelding met Aspose OCR – Complete C# Gids

Tekst extraheren uit een afbeelding is een veelvoorkomend obstakel wanneer je gescande documenten, bonnen of zelfs een foto van een whiteboard wilt digitaliseren. Als je je afvraagt **hoe je OCR-tekst kunt extraheren** in een .NET‑project, ben je op de juiste plek—deze gids leidt je door het volledige proces, van het laden van de afbeelding tot het ophalen van de herkende tekens uit een TIF‑bestand.

We behandelen alles wat je moet weten: het maken van de OCR‑engine, het laden van de afbeelding voor OCR, het uitvoeren van een asynchrone herkenning, en tenslotte het afdrukken van de geëxtraheerde tekst naar de console. Aan het einde heb je een uitvoerbare codefragment dat werkt met elke TIFF (of andere ondersteunde formaten) en een goed begrip van waarom elk onderdeel belangrijk is.

## Wat je nodig hebt

- .NET 6 of later (de code compileert ook op .NET Core 3.1+)
- Een Aspose.OCR NuGet‑pakket (`Aspose.OCR`) geïnstalleerd in je project
- Een voorbeeld‑TIFF‑afbeelding (`page1.tif`) geplaatst op een locatie die je kunt refereren
- Een code‑editor of IDE (Visual Studio, VS Code, Rider—wat je maar wilt)

Geen extra configuratiebestanden, geen zware OCR‑engines die lokaal geïnstalleerd moeten worden—Aspose doet het zware werk voor je.

---

## Tekst extraheren uit afbeelding – Stap 1: Initialiseer de OCR‑engine

Voordat een afbeelding kan worden verwerkt, heb je een instantie van `OcrEngine` nodig. Beschouw de engine als het brein dat weet hoe tekens gelezen moeten worden; zonder deze heeft de rest van de pijplijn niets om aan te sturen.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();
```

> **Waarom dit belangrijk is:** `OcrEngine` bevat de herkenningsalgoritmen en taalpakketten. Het één keer per bewerking instantieren houdt het geheugenverbruik laag en geeft je een duidelijk punt om later instellingen aan te passen (bijv. taal, DPI).

---

## Hoe OCR‑tekst te extraheren – Stap 2: Afbeelding laden voor OCR

Nu de engine klaar is, moeten we hem wijzen naar de afbeelding die we willen lezen. Aspose biedt `ImageStream.FromFile`, die het bestand streamt zonder de volledige bitmap in het geheugen te laden—een mooie prestatie‑winst voor grote TIFF‑bestanden.

```csharp
        // Step 2: Load the image to be recognized
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/page1.tif");
```

> **Pro tip:** Vervang `YOUR_DIRECTORY` door het absolute of relatieve pad naar je afbeelding. Als je de app vanuit de projectmap uitvoert, werkt `@"./page1.tif"` prima.  
> **Randgeval:** TIFF‑bestanden kunnen meerdere pagina's bevatten. `ImageStream.FromFile` leest standaard de eerste pagina; als je een andere pagina nodig hebt, gebruik dan `ImageStream.FromFile(path, pageNumber)`.

---

## Tekst herkennen uit TIF – Stap 3: Asynchrone OCR uitvoeren

Het blokkeren van de aanroepende thread terwijl de OCR‑engine werkt, kan UI‑apps bevriezen of serverbronnen verspillen. Het gebruik van `RecognizeAsync` laat de operatie op de achtergrond draaien en retourneert een `Task<string>` die oplost naar de geëxtraheerde tekst.

```csharp
        // Step 3: Perform OCR asynchronously (does not block the calling thread)
        string extractedText = await engine.RecognizeAsync();
```

> **Waarom async?** In een web‑API of desktop‑app wil je dat de thread‑pool responsief blijft. `await` geeft de controle terug aan de aanroeper totdat de OCR voltooid is, waardoor de UI soepel blijft of de request‑thread vrij is voor ander werk.

---

## Uitvoer van de geëxtraheerde tekst – Stap 4: Afdrukken of opslaan

Tot slot schrijven we het resultaat simpelweg naar de console. In real‑world scenario's kun je het naar een database, een bestand schrijven, of de string doorgeven aan een andere service.

```csharp
        // Step 4: Output the recognized text
        Console.WriteLine(extractedText);
    }
}
```

### Verwachte uitvoer

Als `page1.tif` de tekst *“Hello, Aspose OCR!”* bevat, zal de console weergeven:

```
Hello, Aspose OCR!
```

Als de afbeelding ruis bevat, kun je extra regeleinden of verkeerd herkende tekens zien—pas de `Options` van de engine aan (bijv. `engine.Options.DetectLanguage = true`) om de nauwkeurigheid te verbeteren.

---

## Veelvoorkomende valkuilen bij het laden van een afbeelding voor OCR

1. **Verkeerd bestandspad** – Een typefout leidt tot een `FileNotFoundException`. Controleer het pad nogmaals of gebruik `Path.Combine` voor cross‑platform veiligheid.  
2. **Niet‑ondersteund formaat** – Aspose OCR ondersteunt PNG, JPEG, BMP en TIFF. Direct een PDF proberen zal een `UnsupportedFormatException` veroorzaken. Converteer eerst indien nodig.  
3. **Grote afbeeldinggrootte** – Zeer hoge resolutie TIFF‑bestanden kunnen veel geheugen verbruiken. Overweeg down‑scaling met `engine.Options.Dpi = 300` vóór herkenning.

---

## Verder gaan: Herkenningsinstellingen aanpassen

Aspose.OCR wordt geleverd met een handvol opties die je kunt aanpassen:

```csharp
engine.Options.Language = Language.English;      // Force English if you know the language
engine.Options.Dpi = 200;                       // Reduce DPI for faster processing
engine.Options.IsAutoRotate = true;            // Auto‑rotate skewed pages
```

Experimenteer hiermee om een balans te vinden tussen snelheid en nauwkeurigheid.

---

## Volledig, uitvoerbaar voorbeeld (Klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma dat je in een nieuw console‑project kunt plaatsen. Het bevat de optionele instellingen die hierboven zijn besproken.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Create the OCR engine
        var engine = new OcrEngine();

        // Optional: fine‑tune recognition
        engine.Options.Language = Language.English;
        engine.Options.Dpi = 200;
        engine.Options.IsAutoRotate = true;

        // Load the image (replace with your actual path)
        engine.Image = ImageStream.FromFile(@"./page1.tif");

        // Run OCR asynchronously
        string extractedText = await engine.RecognizeAsync();

        // Show the result
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

Sla het bestand op als `Program.cs`, voer `dotnet add package Aspose.OCR` uit, en daarna `dotnet run`. Je zou de geëxtraheerde tekst in de console moeten zien.

---

## Samenvatting

We hebben zojuist **hoe je OCR‑tekst kunt extraheren** uit een TIFF‑afbeelding met Aspose OCR in C# gedemonstreerd. De stappen—de engine initialiseren, de afbeelding laden voor OCR, tekst asynchroon herkennen uit TIF, en het resultaat weergeven—dekken de volledige levenscyclus van het extraheren van tekst uit afbeeldingsbestanden.  

Als je klaar bent om verder te gaan dan platte tekst, verken dan Aspose’s `PdfConverter` om de OCR‑output in doorzoekbare PDF’s te embedden, of gebruik `engine.Options` om meertalige documenten te verwerken.

---

## Wat is het volgende?

- **Batchverwerking:** Loop over een map met TIFF‑bestanden en sla elk resultaat op in een database.  
- **Afbeelding voorverwerking:** Gebruik `System.Drawing` of `ImageSharp` om ruisvolle scans op te schonen voordat je ze aan de OCR‑engine voert.  
- **Integreren met ASP.NET Core:** Maak een endpoint beschikbaar dat een geüploade afbeelding accepteert en de herkende tekst als JSON retourneert.

Voel je vrij om te experimenteren, dingen kapot te maken, en daarna terug te komen naar deze gids voor een opfrisser. Als je tegen problemen aanloopt, is de Aspose OCR‑documentatie een goede metgezel, maar het kernpatroon blijft hetzelfde: **tekst uit afbeelding extraheren**, **afbeelding laden voor OCR**, **tekst uit TIF herkennen**, en het resultaat verwerken.

Veel plezier met coderen, en moge je afbeeldingen altijd kristalhelder zijn!

## Related Tutorials

- [Tekst uit afbeelding extraheren C# met taalkeuze met Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Tekst uit afbeelding extraheren – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)
- [Hoe tekst uit afbeelding te extraheren door rechthoeken voor te bereiden in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}