---
category: general
date: 2026-05-31
description: Leer hoe je tekst uit een afbeelding herkent in C# met Aspose OCR, inclusief
  hoe je tekst uit tiff‑bestanden extraheert en afbeeldingen efficiënt laadt voor
  OCR.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: nl
og_description: Stapsgewijze handleiding voor het herkennen van tekst uit een afbeelding
  met Aspose OCR, met uitleg over extractie uit TIFF en correcte afbeeldinglading
  voor OCR.
og_title: tekst herkennen uit afbeelding in C# met Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: herken tekst uit een afbeelding in C# met Aspose OCR
url: /nl/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit afbeelding in C# met Aspose OCR

Heb je ooit **tekst uit een afbeelding moeten herkennen** maar wist je niet waar je moest beginnen in C#? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan bij het verwerken van gescande documenten of multi‑page TIFF‑bestanden. In deze gids lopen we stap voor stap door een compleet, kant‑klaar voorbeeld dat **tekst uit een afbeelding herkent** met de Aspose OCR‑bibliotheek, en we laten ook zien hoe je **tekst uit tiff kunt extraheren** en de beste manier om **een afbeelding te laden voor OCR** zonder je haar uit te trekken.

We behandelen alles, van het installeren van het NuGet‑pakket tot het afhandelen van GPU‑versnelling en het terugvallen op CPU wanneer dat nodig is. Aan het einde van deze tutorial heb je een console‑applicatie die de herkende tekst en de verwerkingstijd afdrukt—geen ontbrekende stukjes, geen vage verwijzingen.

## Wat je gaat bouwen

- Een eenvoudige .NET console‑applicatie die een afbeelding laadt (inclusief multi‑page TIFF)  
- Een OCR‑engine geconfigureerd voor GPU‑gebruik, met een soepele CPU‑fallback  
- Extractie van platte tekst uit de afbeelding, afgedrukt in de console  
- Timing‑informatie zodat je de prestatie‑impact van GPU versus CPU kunt zien  

**Prerequisites**

- .NET 6 SDK of later (de code werkt met .NET Core en .NET Framework)  
- Basiskennis van C# en de commandoregel  
- Internettoegang om het Aspose.OCR NuGet‑pakket te downloaden  

Als je dat hebt, laten we beginnen.

![C# code om tekst uit afbeelding te herkennen met Aspose OCR](image.png "C# code om tekst uit afbeelding te herkennen met Aspose OCR")

## Stap 1 – Tekst uit afbeelding herkennen: OCR‑engine instellen

Allereerst hebben we een `OcrEngine`‑instantie nodig. Aspose OCR laat je het verwerkingsapparaat kiezen—GPU voor snelheid, CPU als vangnet. De engine accepteert ook een geheugen‑limiet hint, wat handig kan zijn op gedeelde machines.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Waarom dit belangrijk is:**  
Kiezen voor `OcrDevice.Gpu` kan seconden schelen in de herkentijd voor grote afbeeldingen, vooral bij multi‑page TIFF‑bestanden. De `GpuMemoryLimit` voorkomt dat je app al het GPU‑geheugen op een gedeelde workstation opeist.

## Stap 2 – Afbeelding laden voor OCR (inclusief TIFF‑ondersteuning)

Nu voeren we de engine een afbeelding toe. Aspose’s `ImageStream.FromFile` accepteert **elke** indeling die de bibliotheek ondersteunt—TIFF, PNG, JPEG, wat je maar wilt. Deze stap beantwoordt direct de **load image for OCR**‑vereiste.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Pro tip:** Als je werkt met een multi‑page TIFF, behandelt Aspose automatisch elke pagina als een apart frame, en de engine verwerkt ze opeenvolgend. Geen extra code nodig.

## Stap 3 – De herkenning uitvoeren en **tekst uit tiff extraheren**

Met de engine klaar en de afbeelding geladen, starten we de OCR‑bewerking. De `Recognize`‑methode retourneert een `OcrResult` die de platte tekst, confidence‑scores en timing‑details bevat.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Afhandeling van randgevallen:**  
Als de GPU niet beschikbaar is, werkt `engine.Recognize()` nog steeds omdat de engine stilletjes overschakelt naar CPU. Je kunt `engine.Device` na de herkenning controleren als je wilt loggen welk apparaat daadwerkelijk is gebruikt.

## Stap 4 – De herkende platte tekst ophalen

De tekst extraheren is eenvoudig—lees gewoon de `Text`‑property. Hier extraheren we eindelijk **tekst uit tiff** (of elke andere afbeelding) en presenteren we die aan de gebruiker.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Je ziet de ruwe tekens, met regeleinden behouden zoals ze in de bronafbeelding staan. Voor meer gestructureerde output (zoals JSON of CSV) kun je `result.Regions` en `result.Lines` verkennen, maar de platte tekst is meestal voldoende voor snelle scripts.

## Stap 5 – Verwerkingstijd meten en GPU‑fallback afhandelen

Prestaties zijn belangrijk, vooral wanneer je tientallen pagina’s verwerkt. De `ProcessingTime`‑property vertelt je precies hoe lang de OCR duurde, ongeacht of deze op GPU of CPU draaide.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Waarom je hier om zou moeten geven:**  
Als je merkt dat de tijd stijgt, kun je `GpuMemoryLimit` aanpassen of expliciet naar CPU overschakelen (`Device = OcrDevice.Cpu`). Omgekeerd betekent een sub‑seconde resultaat op een grote TIFF dat je GPU‑versnelling zijn werk doet.

## Volledig, kant‑klaar voorbeeld

Kopieer de code hieronder naar een nieuw console‑project (`dotnet new console -n OcrDemo`) en voer `dotnet add package Aspose.OCR` uit. Vervang vervolgens `YOUR_DIRECTORY/sample_multi_page.tif` door het pad naar jouw afbeelding.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Verwachte output (ingekort voor beknoptheid):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Als je machine geen capabele GPU heeft, kan de verstreken tijd een paar seconden langer zijn, maar de tekst wordt nog steeds correct geëxtraheerd.

## Veelgestelde vragen & valkuilen

- **Wat als de afbeelding enorm is (meer dan 10 MB)?**  
  Verlaag de resolutie voordat je deze aan de engine geeft, of verhoog `GpuMemoryLimit` als je voldoende VRAM hebt.  
- **Kan ik meerdere afbeeldingen in een lus verwerken?**  
  Zeker. Hergebruik dezelfde `OcrEngine`‑instantie en wijs elke iteratie een nieuwe `ImageStream` toe.  
- **Moet ik iets expliciet vrijgeven?**  
  `OcrEngine` implementeert `IDisposable`. Plaats het in een `using`‑block voor nette resource‑beheer, vooral bij GPU‑resources.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Wat als ik andere talen dan Engels wil gebruiken?**  
  Stel `engine.Language = OcrLanguage.Spanish` (of een andere ondersteunde taal) in vóór het aanroepen van `Recognize()`.  

## Conclusie

Je hebt nu een complete, end‑to‑end oplossing die **tekst uit een afbeelding herkent** in C# met Aspose OCR. De tutorial behandelde hoe je **een afbeelding laadt voor OCR**, hoe je **tekst uit tiff extrahert**, en hoe je de prestaties meet terwijl je soepel GPU‑fallback afhandelt. 

Vanaf hier kun je:

- Experimenteren met verschillende afbeeldingsformaten (BMP, PDF) om te zien hoe Aspose ze verwerkt.  
- Duiken in `result.Regions` voor bounding‑box‑data als je lay‑aware informatie nodig hebt  

## Wat moet je hierna leren?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}