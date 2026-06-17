---
category: general
date: 2026-03-17
description: Hoe PNG-afbeeldingen in batch OCR'en in C# snel. Leer tekst uit PNG-bestanden
  te extraheren, PNG naar tekst te converteren en afbeeldingen uit een map te lezen
  met een eenvoudig script.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: nl
og_description: Hoe batch‑OCR uit te voeren op PNG‑afbeeldingen in C# met stap‑voor‑stap
  code. Tekst uit PNG‑bestanden extraheren, PNG naar tekst converteren en afbeeldingen
  moeiteloos uit een map lezen.
og_title: Hoe PNG-afbeeldingen batchgewijs OCR'en in C# – Complete gids
tags:
- OCR
- C#
- Image Processing
title: Hoe PNG-afbeeldingen batchgewijs OCR'en in C# – Complete gids
url: /nl/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

Check table formatting: need to keep markdown table with pipes.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PNG-afbeeldingen batch-OCR'en in C# – Complete gids

Heb je je ooit afgevraagd **hoe je batch-OCR** kunt uitvoeren op een map vol screenshots zonder elk bestand handmatig te openen? Je bent niet de enige—ontwikkelaars vragen voortdurend hoe ze grote collecties PNG's batch-OCR'en, vooral wanneer het doel is om tekst‑PNG‑bestanden te extraheren voor downstream‑analyse.  

In deze tutorial lopen we een kant‑en‑klaar C#‑voorbeeld door dat **extraheert tekst‑PNG**‑bestanden, **converteert PNG naar tekst**, en je de beste manier laat zien om **afbeeldingen uit een map te lezen**. Aan het einde heb je een enkel script dat een `.txt` naast elke afbeelding plaatst, waardoor je uren handmatig kopiëren‑plakken bespaart.

## Wat je zult bereiken

- Initialiseer één OCR‑engine en hergebruik deze voor de hele batch.  
- Scan elk `*.png` in een opgegeven map zonder zelf een lus te schrijven.  
- Schrijf elk OCR‑resultaat naar een eigen tekstbestand, behoudende de oorspronkelijke bestandsnaam.  
- Verwerk veelvoorkomende randgevallen zoals lege mappen of niet‑afbeeldingsbestanden op een nette manier.

### Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Core en .NET Framework).  
- Een OCR‑bibliotheek die de types `OcrEngine`, `ImageStream` en `OcrResult` exposeert (bijvoorbeeld de fictieve **FastOCR** SDK die in de fragmenten wordt gebruikt).  
- Basiskennis van C#—geen geavanceerde patronen vereist.

---

## Hoe PNG-afbeeldingen batch-OCR'en – Overzicht

Hieronder staat het **volledige, uitvoerbare programma**. Voel je vrij om het te copy‑pasten in een nieuw console‑project, vervang de placeholder‑paden, en druk op **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Verwachte output:** Voor elke `image01.png` vind je een `image01.txt` met de herkende tekens. De console zal elk bestand vermelden zodra het is weggeschreven.

![Diagram batch OCR](how-to-batch-ocr-diagram.png "Diagram dat laat zien hoe je PNG-afbeeldingen batch-OCR't met C#")

---

## Stap‑voor‑stap uitleg

### 1. Initialiseer de OCR‑engine – het hart van het proces  

De regel `var ocrEngine = new OcrEngine();` maakt een enkele engine‑instantie aan die voor de hele batch wordt hergebruikt. Het hergebruiken van de engine is **cruciaal** omdat de meeste OCR‑bibliotheken zware bronnen (zoals taalmodellen) bij constructie toewijzen. Eenmalig initialiseren verbetert de prestaties drastisch—vooral wanneer je tientallen of honderden PNG's hebt.  

> **Pro tip:** Als je een andere taal dan Engels nodig hebt, stel dan `ocrEngine.Config.Language = Language.Spanish;` in (of een andere ondersteunde enum).  

### 2. Lees afbeeldingen uit een map – vind elke PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` doet precies wat het secundaire zoekwoord *afbeeldingen uit een map lezen* belooft. Het retourneert een array van absolute paden, die we later aan de OCR‑engine voeren.  

> **Waarom niet `SearchOption.AllDirectories` gebruiken?** Als je afbeeldingen genest zijn, kun je overschakelen naar `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Houd er echter rekening mee dat diepere scans ongewenste bestanden kunnen opleveren, dus filter dienovereenkomstig.  

### 3. Converteer bestands‑paden naar ImageStream‑objecten  

De meeste OCR‑SDK's verwachten een stream in plaats van een ruwe pad. De LINQ‑expressie `Select(path => ImageStream.FromFile(path)).ToList()` bouwt een **lijst van streams** die de batch‑herkenner in één oproep kan verwerken. Deze stap zorgt er ook voor dat bestands‑handles slechts één keer worden geopend, waardoor I/O‑overhead wordt verminderd.  

> **Randgeval:** Als een bestand corrupt is, kan `ImageStream.FromFile` een uitzondering werpen. Omhul de conversie in een `try/catch` als je veerkracht nodig hebt.  

### 4. Herken tekst in de volledige batch  

`ocrEngine.RecognizeBatch(imageStreams)` is de ideale oplossing voor *hoe je batch-OCR* uitvoert. In plaats van over elke afbeelding te loopen en een single‑image‑methode aan te roepen, geven we de volledige collectie aan de engine. Intern kan de bibliotheek het werk paralleliseren, waardoor je een snelheidsboost krijgt op multi‑core machines.  

> **Tip:** Als je OCR‑bibliotheek geen batch‑methode exposeert, kun je toch vergelijkbare prestaties behalen door `Parallel.ForEach` te gebruiken rond de single‑image‑`Recognize`‑aanroep.  

### 5. Schrijf elk OCR‑resultaat – PNG naar tekst converteren  

De laatste `for`‑lus schrijft `ocrResults[i].Text` naar een `.txt`‑bestand waarvan de naam de oorspronkelijke PNG weerspiegelt. Dit is precies wat het secundaire zoekwoord *PNG naar tekst converteren* beschrijft. De `Path.Combine`‑aanroep garandeert dat de uitvoermap bestaat en voorkomt pad‑traversal‑bugs.  

> **Veelvoorkomend valkuil:** Als je de uitvoermap niet eerst aanmaakt, krijg je een `DirectoryNotFoundException`. De regel `Directory.CreateDirectory(outputFolder);` lost dat proactief op.  

## Omgaan met variaties in de praktijk

| Situatie | Wat te wijzigen | Waarom |
|----------|----------------|--------|
| **Lege invoermap** | Behoud de vroege `if (imagePaths.Length == 0)` guard | Voorkomt een onnodige OCR‑aanroep en geeft een vriendelijke melding |
| **Gemengde bestandstypen** | Gebruik `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Garandeert dat je alleen PNG's verwerkt, waardoor tekst‑PNG extraheren zonder fouten wordt voldaan |
| **Grote afbeeldingen ( > 5 MB )** | Verklein voordat je naar OCR stuurt: `ImageStream.FromFile(path).Resize(1920, 1080)` (indien de API dit ondersteunt) | Vermindert geheugenbelasting en verbetert vaak de herkenningsnauwkeurigheid |
| **Andere OCR‑taal** | Stel `ocrEngine.Config.Language = Language.French;` in | Stemmt de engine af op de taal van de bronafbeeldingen |

## Veelgestelde vragen (FAQ)

**Q: Werkt dit met JPEG- of TIFF‑bestanden?**  
A: De kernlogica blijft hetzelfde; verander gewoon het zoekpatroon naar `"*.jpg"` of `"*.tif"` en zorg ervoor dat de OCR‑bibliotheek die formaten kan decoderen.

**Q: Hoe kan ik duizenden afbeeldingen verwerken zonder geheugen op te raken?**  
A: Vervang de batch‑aanroep door een streaming‑aanpak—verwerk bijvoorbeeld een blok van 50 afbeeldingen tegelijk, en sluit daarna de streams voordat je de volgende blok laadt.

**Q: Ik heb de OCR‑vertrouwensscore nodig. Waar vind ik die?**  
A: De meeste `OcrResult`‑objecten bieden een `Confidence`‑eigenschap. Je kunt de schrijf‑stap uitbreiden:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

## Samenvatting

We hebben zojuist **hoe je batch-OCR** uitvoert op PNG‑afbeeldingen in C# van begin tot eind behandeld. Door één engine te initialiseren, afbeeldingen uit een map te lezen, ze naar streams te converteren, de volledige batch te herkennen, en tenslotte elk resultaat naar een tekstbestand te schrijven, heb je nu een solide, productie‑klaar patroon voor **tekst‑PNG extraheren**, **PNG naar tekst converteren**, en **afbeeldingen uit een map lezen** taken.  

Wat nu? Probeer de OCR‑provider te wisselen, voeg multi‑threaded post‑processing toe (bijv. spell‑checking), of voer de `.txt`‑bestanden in een zoekindex. De mogelijkheden zijn eindeloos zodra je de batch‑workflow onder de knie hebt.  

Heb je een twist die je wilt delen? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}