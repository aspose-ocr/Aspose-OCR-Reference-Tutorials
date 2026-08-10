---
category: general
date: 2026-02-14
description: Hoe OCR in C# te gebruiken om snel tekst uit PNG‑bestanden te extraheren.
  Leer batch‑OCR van afbeeldingen, verwerk meerdere afbeeldingen en gebruik Aspose
  OCR C# in één gids.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: nl
og_description: Hoe OCR te gebruiken in C# met Aspose OCR C#. Deze tutorial laat zien
  hoe je tekst uit PNG‑bestanden kunt extraheren, batch‑OCR op afbeeldingen kunt uitvoeren
  en meerdere afbeeldingen efficiënt kunt verwerken.
og_title: Hoe OCR te gebruiken in C# – Batch PNG-tekstextractie
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Hoe OCR te gebruiken in C# – Batchverwerking van PNG-afbeeldingen met Aspose
  OCR
url: /nl/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in C# – Batchverwerking van PNG‑afbeeldingen met Aspose OCR

Heb je je ooit afgevraagd **hoe je OCR** kunt gebruiken om tekst uit een heleboel PNG‑bestanden te halen zonder voor elk bestand een aparte routine te schrijven? Je bent niet de enige. Veel ontwikkelaars lopen tegen problemen aan wanneer ze **PNG‑tekst moeten extraheren** op grote schaal, vooral wanneer de afbeeldingen zich in een map bevinden en je voor elk bestand de OCR‑engine moet starten.  

In deze gids lopen we stap voor stap door een complete, kant‑klaar oplossing die **batch OCR‑afbeeldingen** uitvoert, **meerdere afbeeldingen** parallel verwerkt, en gebruikmaakt van de krachtige **Aspose OCR C#**‑bibliotheek. Aan het einde heb je één uitvoerbaar bestand dat een willekeurig aantal PNG’s inleest, hun tekst extraheert en de resultaten naar de console print – allemaal met slechts een paar regels code.

## Prerequisites

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework)  
- Een geldige Aspose.OCR for .NET‑licentie (of de gratis proefversie) – deze kun je verkrijgen via de Aspose‑website.  
- Een map met de PNG‑bestanden die je wilt lezen.  
- Visual Studio 2022 (of een andere C#‑compatible IDE).  

Er zijn geen extra NuGet‑pakketten nodig naast `Aspose.OCR`.

## Step 1: How to Use OCR – Initialize the Aspose OCR Engine

Het eerste wat je nodig hebt is een instantie van de `Engine`‑klasse. Dit object abstraheert de onderliggende OCR‑technologie en kan draaien op CPU of GPU, afhankelijk van je hardware en licentie.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Waarom dit belangrijk is:* Het eenmalig initialiseren van de engine en deze hergebruiken over threads heen bespaart geheugen en voorkomt de overhead van het telkens opnieuw laden van OCR‑modellen. Het garandeert bovendien consistente instellingen voor alle afbeeldingen.

## Step 2: Extract Text PNG – Gather the Image Paths

Vervolgens hebben we een collectie van bestands‑paden nodig. In een echt project zou je de map dynamisch lezen, maar voor de duidelijkheid vermelden we een paar voorbeeldbestanden.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Tip:* Vervang `YOUR_DIRECTORY` door het absolute of relatieve pad naar je afbeeldingen. Als je tientallen bestanden hebt, kun je de handmatige lijst vervangen door `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Step 3: Batch OCR Images – Run Recognition in Parallel

Afbeeldingen één voor één verwerken is simpel maar traag. Door `Parallel.ForEach` te gebruiken kunnen we **meerdere afbeeldingen** gelijktijdig verwerken, waardoor we profiteren van multi‑core CPU’s.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Waarom parallel?* Elke OCR‑aanroep is CPU‑intensief maar onafhankelijk, dus gelijktijdig uitvoeren kan de totale uitvoeringstijd drastisch verkorten, vooral op een machine met 4 cores of meer.

## Step 4: Process Multiple Images – Display the Extracted Text

Nu we een collectie `OcrResult`‑objecten hebben, kunnen we erover itereren en de herkende tekst afdrukken. Normaal zou je de output opslaan in een database of naar bestanden schrijven, maar console‑output houdt het voorbeeld beknopt.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Verwachte console‑output (voorbeeld):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Als een afbeelding niet geladen kan worden, gooit Aspose een uitzondering; je kunt de `engine.Recognize`‑aanroep omhullen met een try/catch‑blok om fouten te loggen zonder de hele batch te onderbreken.

## Step 5: Full Working Example – All Pieces Together

Hieronder vind je het volledige programma dat je kunt copy‑pasten in een nieuw C#‑consoleproject. Het bevat alles van de `using`‑statements tot de uiteindelijke output‑lus.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Running the Sample

1. Maak een nieuw **Console App**‑project aan in Visual Studio.  
2. Voeg het **Aspose.OCR** NuGet‑pakket toe (`Install-Package Aspose.OCR`).  
3. Vervang `YOUR_DIRECTORY` door het pad dat je PNG‑bestanden bevat.  
4. Build en run – je zou de geëxtraheerde tekst in de console moeten zien.

## Pro Tips & Edge Cases

- **GPU‑versnelling:** Als je een compatibele GPU en een gelicentieerde Aspose OCR hebt, schakel deze in via `EngineSettings` vóór het aanmaken van de engine. Dit kan enkele seconden per afbeelding besparen.  
- **Grote bestanden:** Voor afbeeldingen groter dan 10 MB, overweeg ze eerst te verkleinen om geheugenbelasting te verminderen.  
- **Taalondersteuning:** Standaard gaat de engine uit van Engels. Stel `engine.Language = Language.French;` (of een andere ondersteunde taal) in om de nauwkeurigheid bij niet‑Engelse tekst te verbeteren.  
- **Foutafhandeling:** De `try/catch` binnen de parallelle lus zorgt ervoor dat een corrupt bestand de hele batch niet onderbreekt. Je kunt fouten ook naar een logbestand schrijven voor later onderzoek.  
- **Resultaatopslag:** In plaats van af te drukken, kun je `result.Text` naar een `.txt`‑bestand schrijven met `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Conclusion

Je weet nu **hoe je OCR** in C# kunt gebruiken om **PNG‑bestanden** te **extraheren**, **batch OCR‑afbeeldingen** uit te voeren en **meerdere afbeeldingen** efficiënt te verwerken met Aspose OCR C#. De oplossing is volledig zelfstandig, draait parallel en kan eenvoudig worden uitgebreid om honderden of duizenden bestanden te verwerken met minimale aanpassingen.

Klaar voor de volgende stap? Vervang de console‑output door een CSV‑rapport, experimenteer met GPU‑versnelling, of voer de OCR‑tekst in een zoekindex. De mogelijkheden zijn eindeloos, en het kernpatroon — eenmalig initialiseren, parallel uitvoeren, fouten netjes afhandelen — zal je goed van pas komen in elke beeldverwerkings‑pipeline.

Happy coding, and may your OCR jobs be fast and error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}