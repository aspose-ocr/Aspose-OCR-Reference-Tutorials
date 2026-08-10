---
category: general
date: 2026-05-25
description: herken tekst van een afbeelding met Aspose OCR in C#. Leer hoe je een
  afbeelding laadt voor OCR, de OCR-taal instelt, een OCR-engine maakt en tekst uit
  een TIFF extraheert.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: nl
og_description: herken tekst van afbeelding met Aspose OCR in C#. Deze tutorial laat
  zien hoe je een OCR‑engine maakt, een afbeelding laadt voor OCR, de OCR‑taal instelt
  en tekst uit een TIFF extraheert.
og_title: herken tekst uit afbeelding met Aspose OCR – Complete C#-gids
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Tekst herkennen van afbeelding met Aspose OCR – Complete C#-gids
url: /nl/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit afbeelding met Aspose OCR – Complete C# Gids

Heb je ooit **tekst herkennen uit afbeelding** moeten doen, maar wist je niet welke bibliotheek zowel snelheid als nauwkeurigheid biedt? Je bent niet de enige. In veel factuur‑verwerkings- of archiveringsprojecten is het grootste pijnpunt het verkrijgen van schone, doorzoekbare tekst uit TIFF‑bestanden zonder een aangepaste parser te schrijven.

Het punt is: Aspose OCR voor .NET maakt die hele pijplijn een eitje. In deze gids lopen we alles door wat je nodig hebt—het installeren van het pakket, **een OCR‑engine maken**, een TIFF laden, de OCR‑taal instellen, en uiteindelijk **tekst uit TIFF extraheren**. Aan het einde heb je een kant‑klaar console‑applicatie die **tekst herkennen uit afbeelding**‑bestanden in een handomdraai kan.

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework)
- Visual Studio 2022 (of een IDE naar keuze)
- Aspose.OCR NuGet‑pakket (GPU‑ondersteuning vereist de `Aspose.OCR.Gpu` add‑on)
- Een GPU met CUDA‑ondersteuning als je extra snelheid wilt (optioneel maar aanbevolen)

> **Pro tip:** Als je geen GPU hebt, laat dan gewoon de `GpuDevice`‑regel weg en de engine schakelt automatisch terug naar de CPU.

## Stap 1: Installeer Aspose OCR en Maak OCR‑Engine

Eerst, voeg de benodigde pakketten toe via NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Nu kunnen we **een OCR‑engine maken**. Dit object is het hart van het proces; het bevat configuratie zoals het apparaat waarop het draait en geheugenlimieten.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Waarom dit belangrijk is:** Door de engine aan een GPU te binden, verkort je de tijd die nodig is om **tekst te herkennen uit afbeelding** drastisch, vooral bij grote batches van hoge‑resolutie TIFF‑bestanden.

## Stap 2: Afbeelding Laden voor OCR

Vervolgens moeten we **een afbeelding laden voor OCR**. Aspose.OCR werkt met `System.Drawing.Image`, dus elk formaat dat door GDI+ wordt ondersteund (inclusief multi‑page TIFF) is geschikt.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Als je met een multi‑page TIFF werkt, kun je door de pagina's loopen met `image.SelectActiveFrame`, maar voor de meeste scenario's is één enkele aanroep voldoende.

## Stap 3: OCR‑Taal Instellen

De engine weet niet vanzelf welke taal je scant. **Stel de OCR‑taal in** voordat je de herkenner uitvoert; anders krijg je veel onleesbare output.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Wist je dat?** Het wisselen van talen tijdens runtime is goedkoop—je kunt zelfs een document met meerdere talen verwerken door deze eigenschap tussen pagina's te wijzigen.

## Stap 4: Voer de Herkenning Uit – Tekst Herkennen uit Afbeelding

Nu het leuke gedeelte: daadwerkelijk **tekst herkennen uit afbeelding**. De `Recognize`‑methode retourneert een eenvoudige string met alle gedetecteerde tekens.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Als je vertrouwensscores of begrenzingskaders nodig hebt, kun je de overload gebruiken die een `OcrResult`‑object retourneert, maar voor de meeste extractietaken is de eenvoudige string voldoende.

## Stap 5: Tekst Extraheren uit TIFF (en multi‑page bestanden afhandelen)

Wanneer de bron een TIFF met meerdere pagina's is, wil je stappen 2‑4 voor elk frame herhalen. Hier is een snelle lus die **tekst uit TIFF** pagina voor pagina **extraheert**:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

De bovenstaande code print de geëxtraheerde tekst voor elke pagina, waardoor het eenvoudig is om de resultaten naar een database of een zoekindex te sturen.

## Stap 6: Toon of Sla de Geëxtraheerde Tekst Op

Ten slotte, laten we **de geëxtraheerde tekst tonen** en optioneel naar een bestand schrijven voor latere verwerking.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Het uitvoeren van het programma moet de herkende tekens weergeven en `extracted_text.txt` naast je bron‑TIFF aanmaken.

---

## Veelgestelde Vragen & Randgevallen

- **Wat als mijn GPU niet wordt gedetecteerd?**  
  Verwijder de `GpuDevice`‑regel; de engine schakelt automatisch over naar CPU‑modus. De prestaties zullen trager zijn, maar de resultaten blijven nauwkeurig.

- **Kan ik PNG‑ of JPEG‑bestanden verwerken?**  
  Zeker—`Image.FromFile` werkt met elk formaat dat door System.Drawing wordt ondersteund, dus je kunt **een afbeelding laden voor OCR** ongeacht de extensie.

- **Hoe ga ik om met scans met lage resolutie?**  
  Verhoog `ocrEngine.PreprocessOptions.Dpi` vóór het aanroepen van `Recognize`. Een hogere DPI geeft de engine meer pixels om mee te werken, waardoor de nauwkeurigheid verbetert.

- **Is er een limiet aan de grootte van de TIFF?**  
  De eigenschap `GpuMemoryLimit` beperkt het GPU‑gebruik. Als je de limiet bereikt, schakelt de engine over naar CPU voor de resterende pagina's.

## Conclusie

Je hebt nu een volledige, productie‑klare code‑fragment dat **tekst herkent uit afbeelding**‑bestanden met Aspose OCR in C#. De tutorial behandelde hoe je **een OCR‑engine maakt**, **een afbeelding laadt voor OCR**, **de OCR‑taal instelt**, en **tekst uit TIFF extraheert**—alles terwijl je GPU‑versnelling benut voor snelheid.

Van hieruit kun je:

- Experimenteer met verschillende talen (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified`, enz.).
- Integreer de output in een doorzoekbare ElasticSearch‑index.
- Voeg post‑processing toe (spellingcontrole, regex‑opschoning) om de gegevenskwaliteit te verbeteren.

Probeer het op je eigen factuurbatch, pas de geheugenlimieten aan, en zie de OCR‑prestaties stijgen. Veel programmeerplezier!

## Gerelateerde Tutorials

- [Afbeeldingstekst extraheren C# met taalkeuze met Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Hoe Tekst uit Afbeelding te Extraheren door Rechthoeken Voor te Bereiden in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Tekst uit Afbeelding Extraheren – Regel Herkennen met Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}