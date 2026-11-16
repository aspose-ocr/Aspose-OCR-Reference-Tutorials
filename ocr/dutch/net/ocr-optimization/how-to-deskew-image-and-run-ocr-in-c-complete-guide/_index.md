---
category: general
date: 2026-03-07
description: Leer hoe je een afbeelding kunt rechtzetten, het contrast kunt verhogen
  en tekst uit een scan kunt extraheren met Aspose OCR. Voer OCR uit op een afbeelding
  met een volledig C#‑voorbeeld en laad de afbeelding eenvoudig voor OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: nl
og_description: Leer hoe je een afbeelding kunt rechtzetten, het contrast kunt verhogen
  en tekst uit een scan kunt extraheren met Aspose OCR in C#. Voer OCR uit op een
  afbeelding met stapsgewijze code.
og_title: Hoe een afbeelding rechtzetten en OCR uitvoeren in C# – Complete gids
tags:
- C#
- OCR
- Image Processing
title: Hoe een afbeelding rechtzetten en OCR uitvoeren in C# – Complete gids
url: /nl/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding rechtzetten en OCR uitvoeren in C# – Complete gids

Als je je ooit hebt afgevraagd **hoe een afbeelding rechtzetten** voordat je OCR uitvoert, ben je hier op de juiste plek. In deze tutorial lopen we door het verhogen van contrast, het laden van een afbeelding voor OCR, en uiteindelijk **tekst extraheren uit een scan** met Aspose OCR.  

Of je nu oude bonnetjes digitaliseert, gescande contracten opschoont, of gewoon een betrouwbare manier nodig hebt om tekst uit een scheve foto te lezen, de onderstaande stappen dekken alles wat je nodig hebt. Geen poespas—alleen een werkend voorbeeld dat je kunt copy‑pasten in Visual Studio.  

## Wat je zult bereiken

Aan het einde van deze gids kun je:

* Scheefstand corrigeren tot 30° (dat is het **hoe een afbeelding rechtzetten**‑deel).  
* Het contrast van de afbeelding verhogen voor scherpere tekenranden (**hoe contrast verhogen**).  
* Je afbeelding in de OCR‑engine laden (**load image for OCR**).  
* Het herkenningsproces uitvoeren en **tekst extraheren uit een scan**.  

Dit alles werkt met het nieuwste Aspose.OCR .NET NuGet‑pakket (v23.11 op het moment van schrijven).  

---

![How to deskew image example](/images/deskew-example.png "how to deskew image")

*De afbeelding hierboven toont een gescand document vóór en na het rechtzetten.*

## Vereisten

* .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).  
* Visual Studio 2022 (of elke C#‑IDE die je wilt).  
* Aspose.OCR NuGet‑pakket – installeer via `dotnet add package Aspose.OCR`.  

Dat is alles. Geen externe services, geen API‑sleutels.

---

## Hoe een afbeelding rechtzetten met Aspose OCR

Het eerste wat we doen is een **ImageProcessingPipeline** aanmaken en een `DeskewFilter` toevoegen. Het filter detecteert automatisch de dominante tekstlijnhoek en roteert de afbeelding terug naar horizontaal.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Waarom dit belangrijk is:**  
Een scheve scan verwart de OCR‑engine omdat tekens niet langer uitgelijnd zijn met de basislijn. De `DeskewFilter` analyseert het histogram van de afbeelding, vindt de hoek, en roteert deze, waardoor de herkenningsnauwkeurigheid drastisch verbetert.

> **Pro‑tip:** Als je weet dat je documenten nooit meer dan 15° kantelen, stel `MaxAngle = 15` in om de verwerking te versnellen.

---

## Hoe contrast verhogen voor betere herkenning

Na het rechtzetten is de volgende stap om de tekst te laten opvallen. De `ContrastBoostFilter` strekt het bereik van de pixelintensiteit uit, wat vooral nuttig is voor vervaagde afdrukken.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Waarom het helpt:**  
Scans met laag contrast produceren grijzige tekens die de binarisator kan interpreteren als achtergrond. Het verhogen van contrast maakt donkere pixels donkerder en lichte pixels lichter, waardoor de daaropvolgende `BinarizationFilter` een schoner canvas krijgt.

---

## OCR uitvoeren op afbeelding – Het bestand laden

Nu de afbeelding is voorbewerkt, moeten we **load image for OCR**. Aspose biedt een handige `ImageStream.FromFile`‑helper.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Als je afbeelding zich in een stream bevindt (bijv. geüpload via een web‑API), kun je in plaats daarvan `ImageStream.FromStream(yourStream)` gebruiken. De engine accepteert BMP, JPEG, PNG, TIFF en vele anderen.

---

## Het herkenningsproces uitvoeren en tekst uit scan extraheren

Met alles aangesloten voert het aanroepen van `Recognize()` het zware werk uit. Na de aanroep is de herkende tekst beschikbaar via `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Verwachte output** (voorbeeld voor een eenvoudige factuur):

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Als de output er rommelig uitziet, controleer dan de volgorde van de pipeline—eerst deskew, dan denoise, contrast boost, en tenslotte binarisatie. Het verwisselen hiervan kan de resultaten verslechteren.

---

## Veelvoorkomende valkuilen en randgevallen

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Leeg resultaat** | Afbeelding is te donker of te licht voor de standaard binarisatiemethode. | Verhoog `ContrastBoostFilter.Strength` of schakel over naar `BinarizationMethod.Otsu`. |
| **Gedeeltelijke tekst ontbreekt** | Ruis blijft na het denoisen. | Gebruik `DenoiseLevel.Medium` voor minder ruwe afbeeldingen, of voeg een tweede `DenoiseFilter` toe. |
| **Verkeerde rotatierichting** | Het document heeft gemengde oriëntatie (bijv. een foto van een gedraaide pagina). | Stel handmatig `DeskewFilter.MaxAngle` lager in en roteer de afbeelding vooraf met `ImageProcessor.Rotate`. |
| **Prestatie‑vertraging** | Grote batch van hoge‑resolutie afbeeldingen. | Verklein afbeeldingen (`ImageProcessor.Resize`) vóór de pipeline, of verwerk ze parallel (`Parallel.ForEach`). |

---

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Sla dit op als `Program.cs`, voer `dotnet run` uit, en zie de console het resultaat van **extract text from scan** afdrukken.  

---

## Volgende stappen & gerelateerde onderwerpen

* **Batchverwerking** – Plaats de bovenstaande logica in een lus om tientallen bestanden te verwerken.  
* **Aangepaste taalpakketten** – Als je niet‑Latijnse scripts moet lezen, laad een taalmodel via `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **PDF‑output** – Combineer Aspose.PDF met OCR om doorzoekbare tekst direct in een PDF‑bestand te embedden.  
* **Prestatie‑afstemming** – Experimenteer met de volgorde van `ImageProcessingPipeline`; soms levert denoising vóór deskew snellere resultaten op bij ruisvolle foto’s.  

Al deze bouwen voort op de kernconcepten die we hebben behandeld: **how to deskew image**, **how to boost contrast**, **load image for OCR**, **perform OCR on image**, en uiteindelijk **extract text from scan**.

---

## Samenvatting

We hebben zojuist een complete, productie‑klare manier getoond om **how to deskew image** uit te voeren en OCR in C# te gebruiken. Door een deskew‑filter, een denoise‑stap, een contrast‑boost en een binarisator te combineren, krijg je een schone invoer die Aspose OCR betrouwbaar **extract text from scan** laat uitvoeren.  

Probeer de code, pas de filterparameters aan voor je eigen documenten, en je zult zien hoe snel de herkenningsnauwkeurigheid verbetert. Vragen? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}