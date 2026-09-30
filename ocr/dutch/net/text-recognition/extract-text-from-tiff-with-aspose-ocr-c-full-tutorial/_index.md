---
category: general
date: 2026-01-09
description: Haal tekst uit TIFF‑bestanden met Aspose OCR in C#. Leer hoe je de eerste
  50 tekens van elk resultaat krijgt in deze stapsgewijze tutorial.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: nl
og_description: Tekst extraheren uit TIFF met Aspose OCR in C#. Deze gids laat stap
  voor stap zien hoe je de eerste 50 tekens van elk OCR‑resultaat krijgt.
og_title: Tekst extraheren uit TIFF met Aspose OCR – Complete C#‑gids
tags:
- Aspose OCR
- C#
- TIFF processing
title: Tekst extraheren uit TIFF met Aspose OCR C# – Volledige tutorial
url: /nl/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit TIFF – Complete Aspose OCR C# Tutorial

Heb je ooit **tekst uit TIFF**‑afbeeldingen moeten extraheren, maar wist je niet welke bibliotheek je kunt vertrouwen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze doorzoekbare tekst uit multi‑page TIFF‑bestanden proberen te halen, vooral wanneer prestaties belangrijk zijn.

In deze **aspose ocr c# tutorial** lopen we een kant‑klaar voorbeeld door dat niet alleen de volledige tekst extraheert, maar je ook laat zien hoe je **de eerste 50 tekens** van elke pagina kunt krijgen voor snelle previews. Aan het einde heb je een zelfstandige applicatie die je in elk .NET‑project kunt plaatsen.

## Wat je nodig hebt

- .NET 6 (of een recente .NET‑versie) – de code compileert zowel met .NET Core als .NET Framework.  
- Een actieve Aspose.OCR for .NET‑licentie (je kunt starten met een gratis proefversie).  
- Een map die één of meer `.tif`‑bestanden bevat die je wilt verwerken.  
- Visual Studio, VS Code of een andere IDE naar keuze – het voorbeeld is puur C#, dus de editor maakt niet uit.

> **Pro tip:** Als je op een CI‑server werkt, voeg dan het Aspose.OCR NuGet‑pakket (`Aspose.OCR`) toe aan je projectbestand; de bibliotheek is volledig beheerd en heeft geen native afhankelijkheden.

## Stap 1: Installeer het Aspose OCR NuGet‑pakket

Allereerst halen we de OCR‑engine in het project. Open een terminal in je solution‑map en voer uit:

```bash
dotnet add package Aspose.OCR
```

Dit commando haalt de nieuwste stabiele versie op (vanaf jan 2026 is dat 23.9) en werkt je `.csproj` automatisch bij. Geen handmatig DLL‑beheer nodig.

## Stap 2: Initialiseert de OCR‑engine

Nu maken we een instantie van `OcrEngine`. Beschouw het als het “brein” dat elke TIFF‑pagina zal lezen.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

Waarom maken we de engine maar één keer aan? Omdat `RecognizeImages` een collectie bestands‑paden kan accepteren, waardoor de engine interne buffers kan hergebruiken en batch‑verwerking aanzienlijk versnelt.

## Stap 3: Verzamel alle TIFF‑bestanden in één oproep

In plaats van zelf over de map te loopen, laten we .NET het zware werk doen. De methode `Directory.GetFiles` retourneert een `IEnumerable<string>` die we direct aan de OCR‑aanroep kunnen doorgeven.

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **Wat als mijn afbeeldingen JPEG of PNG zijn?** Verander gewoon het zoekpatroon (`"*.jpg"` of `"*.*"`). Aspose OCR werkt met alle gangbare rasterformaten.

## Stap 4: Voer OCR uit op de volledige collectie

Hier is de magische regel die elk bestand in één verzoek verwerkt. De methode retourneert een dictionary waarbij de sleutel het bestandspad is en de waarde een `OcrResult`‑object met de herkende tekst.

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

Waarom batch‑verwerken? Het vermindert de overhead van het herhaaldelijk laden van de OCR‑engine, en op multi‑core machines paralleliseert Aspose intern het werk, waardoor je een merkbare snelheidswinst krijgt.

## Stap 5: Toon een preview – Haal de eerste 50 tekens op

De meeste UI‑scenario's hebben alleen een fragment nodig, niet het volledige document. We halen de eerste 50 tekens (of minder als de pagina kort is) op en printen ze naast de bestandsnaam.

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

De regel `Math.Min(50, fullText.Length)` garandeert dat we nooit buiten de string‑grenzen gaan – een kleine beveiliging die een `ArgumentOutOfRangeException` voorkomt wanneer het OCR‑resultaat korter is dan 50 tekens.

### Verwachte console‑output

Stel dat je twee TIFF‑bestanden hebt (`invoice1.tif` en `receipt2.tif`), dan kan de console het volgende weergeven:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

Elke regel eindigt met een ellipsis (`...`) om aan te geven dat de preview slechts het begin van een langer tekstblok is.

## Stap 6: Afhandelen van randgevallen en veelvoorkomende valkuilen

### Lege of corrupte bestanden

Als een bestand niet gelezen kan worden, retourneert `RecognizeImages` nog steeds een entry met een lege `Text`‑eigenschap. Je kunt die filteren:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### Grote batches

Het verwerken van duizenden TIFF‑bestanden kan veel geheugen verbruiken. Gebruik in dat geval de overload die een `Stream` per afbeelding accepteert, of verwerk de lijst in kleinere delen:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### Taal‑ en lettertype‑ondersteuning

Bevat je document niet‑Latijnse tekens, stel dan de taal in vóór het aanroepen van `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

Deze kleine aanpassing kan de nauwkeurigheid drastisch verhogen.

## Stap 7: Volledig werkend voorbeeld (klaar om te kopiëren)

Hieronder staat het complete programma dat je kunt plakken in een nieuw console‑project (`dotnet new console`) en direct kunt uitvoeren (vervang `YOUR_DIRECTORY/Batch` door het echte pad).

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

Voer het programma uit met `dotnet run`. Je zou een beknopte preview voor elk TIFF‑bestand moeten zien, waarmee je hebt bevestigd dat je succesvol **tekst uit TIFF**‑afbeeldingen hebt geëxtraheerd met Aspose OCR.

## Veelgestelde vragen (FAQ)

**Q: Werkt dit met multi‑page TIFF‑bestanden?**  
A: Ja. Aspose OCR behandelt elke pagina intern als een aparte afbeelding, dus een multi‑page TIFF levert één samengevoegde string per bestand op. Je kunt die later desgewenst splitsen.

**Q: Hoe nauwkeurig is de OCR out of the box?**  
A: Voor schone, hoge‑resolutie scans (300 DPI of hoger) kun je >95 % nauwkeurigheid verwachten voor Engelse tekst. Voorbewerking (deskew, binarisatie) kan dit nog hoger maken.

**Q: Kan ik de resultaten naar een CSV‑bestand exporteren?**  
A: Absoluut. Vervang de `Console.WriteLine` door een `StreamWriter` en schrijf `fileName,preview`‑rijen. Vergeet niet komma’s in de preview‑tekst te escapen.

## Volgende stappen en gerelateerde onderwerpen

- **OCR‑resultaten opslaan** – Bewaar de volledige tekst in een database voor doorzoekbare archieven.  
- **Combineren met PDF‑conversie** – Gebruik Aspose.PDF om de geëxtraheerde tekst terug in doorzoekbare PDF‑bestanden te embedden.  
- **Batch‑verwerking op Azure Functions** – Schaal de OCR‑taken uit zonder eigen servers te beheren.  

Al deze uitbreidingen bouwen voort op het kernidee van **tekst extraheren uit TIFF** op een efficiënte manier, terwijl je nog steeds **de eerste 50 tekens** kunt ophalen voor snelle UI‑previews.

---

*Happy coding! Als je tegen vreemde problemen aanloopt, laat dan een reactie achter – ik help je graag de OCR‑pipeline verder te verfijnen.* 

![Tekst extraheren uit TIFF met Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Tekst extraheren uit TIFF met Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}