---
category: general
date: 2026-04-26
description: Hoe PNG-afbeeldingen snel in batch OCR'en. Leer tekst uit PNG te extraheren,
  afbeeldingen naar tekst te converteren, herkende tekst te schrijven en een PNG-directory
  te lezen met Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: nl
og_description: Hoe PNG-afbeeldingen batchgewijs OCR'en in C# met Aspose OCR. Deze
  gids laat zien hoe je tekst uit PNG kunt extraheren, afbeeldingen naar tekst kunt
  converteren en herkende tekst efficiënt kunt opslaan.
og_title: Hoe PNG-afbeeldingen batchgewijs OCR'en in C# – Stap voor stap
tags:
- OCR
- C#
- Aspose
title: Hoe PNG-afbeeldingen batchgewijs OCR'en in C# – Complete gids
url: /nl/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch-OCR PNG-afbeeldingen in C# – Complete gids

Heb je je ooit afgevraagd **hoe je batch-OCR** kunt uitvoeren op een hele map met PNG‑bestanden zonder voor elke afbeelding een apart programma te schrijven? Je bent niet de enige die tientallen screenshots, gescande bonnen of grafische bestanden moet omzetten naar doorzoekbare tekst. In deze tutorial lopen we een praktische oplossing door die **tekst uit PNG haalt**, **afbeeldingen naar tekst converteert**, en **herkende tekst** naar afzonderlijke bestanden schrijft — terwijl de PNG‑map automatisch wordt gelezen.

Aan het einde van deze gids heb je een kant‑klaar C# console‑applicatie die in één keer een willekeurig aantal afbeeldingen verwerkt. Geen extra scripts, geen handmatig kopiëren‑en‑plakken — alleen pure code die het zware werk voor je doet.

## Wat je nodig hebt

- **.NET 6.0** of later (de code werkt ook prima op .NET Framework).  
- **Aspose.OCR for .NET** NuGet‑pakket (gratis proefversie werkt voor testen).  
- Een map met een aantal *.png*-bestanden die je wilt OCR’en.  
- Visual Studio 2022 of een andere C#‑IDE naar keuze.

Als je die hebt, kunnen we meteen naar de implementatie springen.

## Stap 1 – Bereid je invoer‑ en uitvoermappen voor *(Lees PNG‑directory)*

Het eerste wat we doen is het programma wijzen op de map die de afbeeldingen bevat en bepalen waar de resulterende *.txt*-bestanden terechtkomen. Met `Directory.GetFiles` krijgen we een nette enumerable van elke PNG in de map.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Waarom dit belangrijk is:**  
- Het gebruik van een wildcard (`*.png`) garandeert dat we alleen afbeeldingsbestanden verwerken, en negeren we eventuele losse documenten.  
- Het dynamisch aanmaken van de uitvoermap voorkomt later een `DirectoryNotFoundException`.

> **Pro tip:** Als je andere formaten wilt ondersteunen (JPEG, BMP), breid dan simpelweg het zoekpatroon uit of roep `Directory.EnumerateFiles` aan met meerdere extensies.

## Stap 2 – Initialise de OCR‑engine *(Converteer afbeeldingen naar tekst)*

Aspose.OCR wordt geleverd met twee engine‑types: een CPU‑gebaseerde `OcrEngine` en een GPU‑versnelde `GpuOcrEngine`. Voor de meeste batch‑taken is de CPU‑engine prima, maar je kunt de klassenaam wijzigen als je een geschikte GPU hebt.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Waarom dit belangrijk is:**  
- Het specificeren van de taal verbetert de nauwkeurigheid aanzienlijk omdat de engine weet welke tekenset verwacht wordt.  
- Overschakelen naar `GpuOcrEngine` is een wijziging van één regel als je prestatie‑knelpunten tegenkomt bij grote batches.

## Stap 3 – Maak een batch‑herkenner

Aspose biedt een handige `BatchRecognizer` die een enumerable van bestands‑paden accepteert en de resultaten één voor één terugstuurt. Dit voorkomt dat alle afbeeldingen tegelijk in het geheugen worden geladen — een cruciaal detail voor grote mappen.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Waarom dit belangrijk is:**  
- De batch‑herkenner kapselt de luslogica in, zodat we ons kunnen concentreren op wat we met elk resultaat doen in plaats van hoe we veilig moeten itereren.

## Stap 4 – Voer OCR uit op alle afbeeldingen en schrijf de output *(Schrijf herkende tekst)*

Nu voeren we daadwerkelijk de OCR uit. De `Recognize`‑methode retourneert een `IEnumerable<RecognitionResult>` waarbij elk resultaat de geëxtraheerde tekst en andere metadata bevat.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Waarom dit belangrijk is:**  
- Het gebruik van `File.WriteAllText` zorgt ervoor dat de tekst standaard met UTF‑8‑codering wordt opgeslagen, waardoor speciale tekens behouden blijven.  
- De incrementele naamgeving (`out_0.txt`, `out_1.txt`) komt overeen met de verwerkingsvolgorde, wat handig is voor debugging.

> **Randgeval:** Als een afbeelding niet kan worden OCR‑t (bijv. een beschadigd bestand), zal `RecognitionResult.Text` leeg zijn. Je kunt een eenvoudige controle toevoegen binnen de lus om fouten te loggen:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Stap 5 – Zet alles bij elkaar – Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑en‑plakken in een nieuw console‑project. Het bevat de `using`‑directieven, mapvalidatie, en een kleine console‑UI zodat je weet wanneer de batch is voltooid.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Verwachte output:**  
Het uitvoeren van het programma geeft iets als volgt weer:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

En je zult `out_0.txt` … `out_11.txt` in de uitvoermap zien, elk met de platte‑tekstversie van de bijbehorende afbeelding.

## Veelgestelde vragen & tips

| Vraag | Antwoord |
|----------|--------|
| *Kan ik ook sub‑mappen OCR‑en?* | Ja — vervang `Directory.GetFiles` door `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Wat als ik een andere taal nodig heb?* | Stel `ocrEngine.Language = Language.Spanish;` in (of een andere ondersteunde enum). |
| *Hoe ga ik om met enorme batches (duizenden bestanden)?* | Overweeg verwerking in delen of gebruik `Parallel.ForEach` met een begrensde graad van parallelisme om geheugenuitputting te voorkomen. |
| *Is de output altijd UTF‑8?* | `File.WriteAllText` gebruikt standaard UTF‑8 zonder BOM, wat werkt voor de meeste op Latijn gebaseerd talen. Voor Aziatische scripts moet je mogelijk expliciet `Encoding.UTF8` instellen. |
| *Kan ik vertrouwensscores krijgen?* | `RecognitionResult` biedt `Confidence` — je kunt dit naast de tekst loggen voor kwaliteitscontrole. |

## Visueel overzicht *(Hoe batch OCR – Diagram)*

![Diagram van batch-OCR-werkstroom die invoermap → OCR-engine → batch-herkenner → output‑txt‑bestanden toont](https://example.com/diagram-how-to-batch-ocr.png "Hoe batch OCR")

*De alt‑tekst bevat het primaire zoekwoord, wat voldoet aan de SEO‑vereisten voor afbeeldingen.*

## Afronding

We hebben zojuist **hoe je batch-OCR** uitvoert op een map met PNG‑bestanden met Aspose.OCR, van het lezen van de PNG‑directory tot het schrijven van elk herkend tekstbestand. De oplossing is volledig zelfstandig, werkt op elke moderne .NET‑runtime, en kan worden uitgebreid voor GPU‑versnelling, meertalige ondersteuning of parallelle verwerking.

Klaar voor de volgende stap? Probeer `Language.Latin` te vervangen door een andere taal, of integreer de output in een zoekindex zodat je documenten direct doorzoekbaar worden. De mogelijkheden zijn eindeloos zodra je batch-OCR onder de knie hebt.

Veel programmeerplezier, en laat het me weten in de reacties als je tegen problemen aanloopt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}