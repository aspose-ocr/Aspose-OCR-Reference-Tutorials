---
category: general
date: 2026-05-28
description: Voer OCR uit op een afbeelding met C# om tekst uit de afbeelding te lezen
  en snel tekst van een bon te extraheren. Leer GPU‑opties en laadtechnieken.
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: nl
og_description: Voer OCR uit op een afbeelding met C#. Deze tutorial laat zien hoe
  je tekst uit een afbeelding leest, tekst van een bon extraheert en het GPU‑gebruik
  optimaliseert.
og_title: OCR uitvoeren op afbeelding – Complete C#-gids
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: OCR uitvoeren op afbeelding – Complete C#‑gids
url: /nl/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR op afbeelding uitvoeren – Complete C#‑gids

Heb je ooit **OCR op afbeelding** bestanden moeten uitvoeren maar wist je niet waar je moest beginnen? Je bent niet de enige; veel ontwikkelaars lopen tegen die muur aan wanneer ze voor het eerst proberen tekst uit afbeeldingsgegevens te lezen. Het goede nieuws is dat je met een paar regels C# tekst kunt extraheren uit kassabon‑scans, PDF‑bestanden of elke foto die je erop loslaat. In deze gids lopen we een volledig, kant‑klaar voorbeeld door dat ook laat zien hoe je **afbeelding voor OCR laadt**, gebruikmaakt van GPU‑versnelling en het geheugen veilig beperkt.

Aan het einde van deze tutorial kun je:

* Een OCR‑engine initialiseren in C#
* **Afbeelding voor OCR laden** vanaf schijf of een stream
* **Tekst uit afbeelding lezen** met optionele GPU‑ondersteuning
* **Tekst uit kassabon extraheren** en naar de console outputten

Geen externe services vereist—alleen een lokale bibliotheek en een voorbeeld‑kassabonafbeelding.

## Wat je nodig hebt

| Voorvereiste | Reden |
|--------------|-------|
| .NET 6.0 SDK or later | Moderne runtime, ondersteunt de nieuwste taalfeatures |
| Een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert (bijv. IronOCR, Tesseract .NET wrapper) | Biedt de `Configuration`‑ en `Recognize`‑methoden die hieronder worden gebruikt |
| Een CUDA‑ondersteunde GPU (optioneel) | Schakelt de `EnableGpu`‑vlag in voor snellere verwerking |
| Een voorbeeld‑kassabonafbeelding (`receipt.jpg`) | Toont de stap **extract text from receipt** |
| Elke C#‑IDE (Visual Studio, Rider, VS Code) | Voor snelle compilatie en debugging |

Als je geen GPU hebt, valt de code simpelweg terug op CPU‑modus—geen zorgen.

![Run OCR on image example output](https://example.com/ocr-output.png "Run OCR on image – sample console output")

*Alt‑tekst: Voorbeeldoutput van OCR op afbeelding die herkende kassabontekst toont.*

## Stap 1: OCR op afbeelding uitvoeren – Engine instellen

Allereerst: maak een instantie van de OCR‑engine aan. Dit object is het hart van het proces; het bevat alle configuratiedetails en voert het zware werk uit.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*Waarom dit belangrijk is:* De `OcrEngine`‑klasse omsluit de native OCR‑engine (Tesseract, IronOCR, enz.). Het één keer instantiëren en hergebruiken voor meerdere afbeeldingen vermindert overhead en geeft je één plek om instellingen aan te passen.

## Stap 2: Afbeelding voor OCR laden

Voordat de engine iets kan lezen, moet je er een afbeelding aan voeren. De `Image`‑eigenschap van de bibliotheek verwacht een stream of een bestandspad, afhankelijk van de implementatie.

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*Tip:* Als je met gebruikers‑uploads werkt, wikkel dit dan in een `try/catch` en valideer eerst het bestandstype. Niet‑ondersteunde formaten zullen een uitzondering veroorzaken die je netjes kunt afhandelen.

## Stap 3: GPU‑versnelling inschakelen (optioneel)

Als je machine een compatibele CUDA‑ of OpenCL‑runtime heeft, kan het inschakelen van GPU‑modus enkele seconden per herkenningspassage besparen.

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*Pro‑tip:* Niet elke GPU is gelijk. Op oudere kaarten kun je een lichte vertraging zien door driver‑overhead. Test beide paden (`EnableGpu = true/false`) om te zien wat het beste werkt voor jouw hardware.

## Stap 4: GPU‑geheugengebruik beperken (optioneel)

Soms wil je niet dat het OCR‑proces al het GPU‑geheugen opslokt, vooral wanneer je de GPU deelt met andere workloads zoals deep‑learning inferentie.

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*Wanneer te gebruiken:* Als je een webservice draait die veel afbeeldingen gelijktijdig verwerkt, voorkomt een geheugenlimiet crashes door geheugen‑tekort.

## Stap 5: Tekst herkennen en tekst uit afbeelding lezen

Nu is de engine klaar om zijn werk te doen. Het aanroepen van `Recognize()` voert de OCR‑pipeline uit en retourneert de geëxtraheerde string.

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*Waarom dit de kern is:* Deze ene regel verbergt een reeks preprocessing‑stappen (binarisatie, deskewing) en de daadwerkelijke karakterclassificatie. De geretourneerde `recognizedText` is platte Unicode, klaar voor verdere verwerking.

## Stap 6: Tekst uit kassabon extraheren – Output

Schrijf tenslotte het resultaat naar de console of sla het op waar je maar wilt. Voor een kassabon kun je later de regels, totalen of datums parseren.

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**Verwachte console‑output (ingekort voor beknoptheid):**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

Als de OCR moeite heeft met een bepaald kassabon‑layout, overweeg dan de preprocessing‑opties aan te passen (bijv. `ocrEngine.Configuration.Deskew = true`) of een afbeelding met hogere resolutie te gebruiken.

## Veelvoorkomende randgevallen & hoe ze op te lossen

| Situatie | Aanbevolen oplossing |
|----------|----------------------|
| **Null‑afbeelding** – `ocrEngine.Image` is `null` | Valideer het bestandspad vóór toewijzing; gooi een duidelijke `ArgumentException` als het ontbreekt. |
| **GPU niet beschikbaar** – `EnableGpu = true` gooit `PlatformNotSupportedException` | Wikkel de GPU‑inschakel‑aanroep in een `try/catch` en val terug op CPU‑modus. |
| **Grote kassabonnen ( > 10 MB )** veroorzaken geheugen‑druk | Gebruik `GpuMemoryLimit` of verwerk de afbeelding in tegels (`ocrEngine.Configuration.TileSize`). |
| **Onjuiste taalherkenning** – output bevat onzin | Stel `ocrEngine.Configuration.Language = "eng"` in (of de juiste ISO‑code) om Engels af te dwingen. |

## Pro‑tips voor productie‑klare OCR

1. **Batchverwerking:** Hergebruik een enkele `OcrEngine`‑instantie voor een batch afbeeldingen; deze cachet taalmodellen en vermindert latentie.  
2. **Voorfilteren:** Pas een eenvoudige grijstinten‑conversie en contrastverhoging toe voordat je de afbeelding aan de engine geeft—veel bibliotheken bieden een `Preprocess`‑methode.  
3. **Foutlogboek:** Leg `ocrEngine.LastError` (indien beschikbaar) vast na elke `Recognize()`‑aanroep om fouten te diagnosticeren zonder je service te laten crashen.  
4. **Thread‑veiligheid:** De meeste OCR‑engines zijn **niet** thread‑veilig. Als je parallelisme nodig hebt, maak dan een aparte engine per thread of gebruik een concurrentie‑wachtrij.  

## Conclusie

We hebben zojuist een volledige **run OCR on image**‑workflow in C# doorlopen. Beginnend met het maken van de engine, **afbeelding voor OCR laden**, het schakelen van GPU‑versnelling, en uiteindelijk **tekst uit kassabon extraheren**, heb je nu een stevige basis om meer geavanceerde document‑verwerkings‑pijplijnen te bouwen.

Volgende stappen kunnen zijn:

* Het parsen van de kassabontekst naar gestructureerde JSON (met regex of een natuurlijke‑taal‑bibliotheek) – ideaal voor **read text from image**‑automatisering.  
* De OCR‑stap integreren in een ASP .NET Core API zodat gebruikers kassabonnen kunnen uploaden via HTTP.  
* Experimenteren met verschillende OCR‑back‑ends (Tesseract vs. commerciële SDK's) om de nauwkeurigheid te vergelijken.  

Probeer het met een paar verschillende kassabon‑layouts, pas de configuratie aan, en je zult zien hoe snel je een wazige foto kunt omzetten in bruikbare data. Veel programmeerplezier, en moge je afbeeldingen altijd scherp zijn!

## Gerelateerde tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}