---
category: general
date: 2026-04-03
description: Leer hoe je batch‑OCR kunt uitvoeren met Aspose.OCR in C#. Deze gids
  laat zien hoe je tekst uit PNG‑afbeeldingen kunt extraheren en afbeeldingen efficiënt
  naar tekst kunt converteren.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: nl
og_description: Ontdek hoe je batch‑OCR in C# kunt gebruiken om tekst uit PNG‑afbeeldingen
  te halen en afbeeldingen naar tekst te converteren met Aspose.OCR. Complete code
  inbegrepen.
og_title: Hoe batch‑OCR in C# uit te voeren – Snelle gids
tags:
- OCR
- C#
- Aspose
title: Hoe batch-OCR in C# uitvoeren – Snelle manier om tekst uit PNG‑bestanden te
  extraheren
url: /nl/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch-OCR uit te voeren in C# – Snelle manier om tekst uit PNG‑bestanden te extraheren

Heb je je ooit afgevraagd **hoe je batch‑OCR** kunt uitvoeren op een hele map met screenshots zonder voor elk bestand een lus te schrijven? Je bent niet de enige. In veel projecten—denk aan factuurdigitalisering of archivering van gescande bonnetjes—kom je tientallen, soms honderden, PNG‑bestanden tegen waarvan de tekst moet worden geëxtraheerd. Het goede nieuws? Met Aspose.OCR kun je **tekst uit PNG**‑afbeeldingen parallel extraheren, en het hele proces kan worden afgerond in slechts een paar regels C#.

In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat laat zien hoe je **afbeeldingen naar tekst** kunt **converteren** met behulp van een batch‑processor. We behandelen de vereisten, leggen uit waarom elke regel belangrijk is, en geven zelfs een paar pro‑tips zodat je later geen veelvoorkomende valkuilen tegenkomt.

## Vereisten

- **.NET 6.0** (of later) geïnstalleerd op je machine. Oudere runtimes werken, maar de nieuwste biedt betere prestaties en async‑ondersteuning.
- **Aspose.OCR for .NET**‑pakket. Je kunt het ophalen via NuGet: `dotnet add package Aspose.OCR`.
- Een map vol **PNG**‑afbeeldingen die je wilt verwerken. We zullen er gedurende de gids naar verwijzen als `YOUR_DIRECTORY`.
- Een bescheiden hoeveelheid RAM—batch‑OCR kan veel geheugen verbruiken als je de paralleliteit opvoert, maar met `Environment.ProcessorCount` blijft het veilig.

> **Pro tip:** Als je een CI/CD‑pipeline gebruikt, voeg dan het Aspose‑licentiebestand toe als geheim om de 20‑pagina‑limiet van de gratis evaluatie te omzeilen.

Laten we nu de handen uit de mouwen steken.

## Stap 1: De Batch‑OCR‑processor instellen (Primair trefwoord in koptekst)

Het eerste wat je nodig hebt is een instantie van `BatchOcrProcessor`. Deze klasse abstraheert de threading‑logica en laat je focussen op wat je met elke afbeelding moet doen.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Waarom dit belangrijk is:**  
- `Engine = new OcrEngine()` geeft je een verse OCR‑engine voor elke thread, waardoor concurrentie wordt voorkomen.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` schaalt automatisch naar het aantal cores, waardoor je de best mogelijke doorvoer krijgt zonder handmatige afstemming.

## Stap 2: Aansluiten op voortgangs‑events (Helpt bij het volgen van extractie)

Het zien van voortgang is essentieel bij het verwerken van honderden bestanden. Het `ProgressChanged`‑event wordt geactiveerd nadat elk bestand is voltooid, zodat je de status kunt loggen.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Waarom je het geweldig zult vinden:**  
- Realtime‑feedback voorkomt dat je je afvraagt of de app vastloopt.  
- Als je ooit moet pauzeren of annuleren, heb je al een hook om `e.Current` versus `e.Total` te inspecteren.

## Stap 3: Definieer de map‑scan en bestands‑patroon (Tekst uit PNG extraheren)

Nu vertellen we de processor waar hij moet zoeken en welk type bestanden hij moet oppikken. Het patroon `"*.png"` zorgt ervoor dat we alleen PNG‑afbeeldingen verwerken.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Waarom dit cruciaal is:**  
- Het gebruik van een glob‑patroon houdt de code flexibel; wijzig `*.png` naar `*.jpg` als je later JPEG‑bestanden moet verwerken.  
- De callback ontvangt zowel het afbeeldingspad als de herkende tekst, waardoor je volledige controle hebt over wat je vervolgens doet.

## Stap 4: Sla de herkende tekst op naast de bron (Afbeeldingen naar tekst converteren)

Binnen de callback schrijven we de OCR‑output naar een `.txt`‑bestand dat direct naast de originele PNG staat. Dit is de eenvoudigste manier om **afbeeldingen naar tekst** te **converteren** voor verdere verwerking.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Waarom we kiezen voor een naast‑gelegen `.txt`‑bestand:**  
- Het houdt de relatie duidelijk—open de PNG, open de TXT, vergelijk.  
- Geen behoefte aan een database of extra opslaglaag in kleinschalige projecten.

## Stap 5: Afronden met een vriendelijke voltooiings‑bericht

Een nette console‑melding vertelt je wanneer alles voltooid is.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Wanneer je het programma uitvoert, zie je output zoals:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Elke PNG heeft nu een verwant `.txt`‑bestand dat de geëxtraheerde tekst bevat.

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het volledige programma dat je kunt kopiëren‑en‑plakken in een nieuw console‑project. Er ontbreken geen delen—vervang gewoon `YOUR_DIRECTORY` door het absolute pad naar je afbeeldingen.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Verwacht resultaat

- Voor elke `image.png` in `C:\MyImages` verschijnt er een `image.txt` ernaast.  
- De console print voortgangslijnen, waardoor het eenvoudig is om grote batches te monitoren.  
- Geen handmatige lussen of thread‑beheer—`BatchOcrProcessor` regelt alles.

## Veelgestelde vragen & randgevallen

### Wat als mijn afbeeldingen geen PNG's zijn?

Verander gewoon het tweede argument in `ProcessFolder` naar `"*.jpg"` of `"*.*"` om alle bestanden op te nemen. De OCR‑engine werkt met de meeste rasterformaten.

### Hoeveel geheugen verbruikt dit?

`BatchOcrProcessor` laadt één afbeelding per thread. Met `Environment.ProcessorCount` ingesteld op bijvoorbeeld 8 cores, heb je tegelijk acht afbeeldingen in het geheugen. Als je OutOfMemory‑exceptions krijgt, verlaag dan de paralleliteit:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Kan ik de OCR‑taal aanpassen?

Zeker. Nadat je de engine hebt gemaakt, stel je de `Language`‑eigenschap in:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose ondersteunt veel talen; voeg gewoon het juiste NuGet‑pakket toe indien nodig.

### Hoe zit het met foutafhandeling?

Omring de callback met een try/catch‑blok en log de fouten. De processor gaat door met het volgende bestand, waardoor een enkel corrupt bestand de hele uitvoering niet afbreekt.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Pro‑tips voor opschalen

- **Verdeel de map**: Als je tienduizenden bestanden hebt, splits ze dan in submappen en voer meerdere batch‑taken opeenvolgend uit.  
- **Gebruik een cloud‑VM**: Een machine met meer cores (bijv. 32‑core) zal veel sneller klaar zijn. Vergeet alleen niet de licentielimieten aan te passen.  
- **Post‑process de tekst**: Na extractie wil je misschien regexes uitvoeren om factuurnummers of data te halen. De `.txt`‑bestanden zijn perfecte invoer voor dergelijke pipelines.

## Conclusie

Je hebt nu een solide, productie‑klaar recept voor **hoe je batch‑OCR** uitvoert op een map met PNG's, **tekst uit PNG‑bestanden** extraheren, en **afbeeldingen naar tekst** converteren met Aspose.OCR in C#. Het voorbeeld is zelfstandig, legt het “waarom” achter elke regel uit, en bevat tips voor het omgaan met grotere workloads of verschillende bestandstypen.

Klaar voor de volgende stap? Probeer de callback te vervangen zodat de resultaten naar een database worden gepusht, of voeg beeld‑pre‑processing toe (bijv. kanteling corrigeren) vóór OCR. Het patroon schaalt goed, zodat je het kunt aanpassen aan elk batch‑verwerkingsscenario dat je tegenkomt.

Veel plezier met coderen, en moge je OCR‑pipelines snel en foutloos zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}