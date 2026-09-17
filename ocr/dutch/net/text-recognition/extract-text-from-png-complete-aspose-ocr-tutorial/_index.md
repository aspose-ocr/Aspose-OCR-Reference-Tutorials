---
category: general
date: 2026-01-09
description: Haal snel tekst uit PNG met Aspose OCR. Leer hoe je tekst uit afbeeldingen
  leest, de OCR-nauwkeurigheid verbetert en schone resultaten krijgt in C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: nl
og_description: Haal snel tekst uit PNG met Aspose OCR. Leer hoe je tekst uit afbeeldingen
  kunt lezen, de OCR-nauwkeurigheid kunt verbeteren en schone resultaten krijgt in
  C#.
og_title: Tekst extraheren uit PNG – Complete Aspose OCR‑tutorial
tags:
- Aspose OCR
- C#
- Image Processing
title: Tekst extraheren uit PNG – Complete Aspose OCR‑tutorial
url: /nl/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PNG – Complete Aspose OCR Tutorial

Heb je ooit **tekst uit PNG** bestanden moeten extraheren, maar waren de resultaten vol onzin? Je bent niet de enige. In veel real‑world projecten – facturen, bonnetjes of gescande formulieren – kan de kwaliteit van de OCR‑output automatiseringspijplijnen maken of breken.  

In deze gids laten we je een **stap‑voor‑stap** manier zien om afbeeldings‑tekst te lezen met Aspose OCR, een aangepaste woordenlijst toe te voegen om **OCR‑nauwkeurigheid te verbeteren**, de ruis op te schonen en uiteindelijk een nette string af te drukken. Aan het einde heb je een kant‑klaar C# console‑applicatie die betrouwbaar tekst uit PNG‑afbeeldingen extraheert.

> **Wat je mee krijgt**  
> * Een compleet, uitvoerbaar code‑voorbeeld.  
> * Inzicht in waarom een aangepaste woordenlijst belangrijk is.  
> * Tips voor het omgaan met randgevallen zoals scans met weinig contrast.  

## Vereisten

- .NET 6 SDK of later (de code richt zich op .NET 6, maar .NET 5 werkt ook).  
- Visual Studio 2022 of een editor naar keuze.  
- Een **PNG**‑afbeelding die je wilt verwerken – bijvoorbeeld `invoice.png`.  
- Het **Aspose.OCR** NuGet‑pakket (`dotnet add package Aspose.OCR`).  

Er zijn geen extra configuratiebestanden nodig; alles bevindt zich in één enkel `.cs`‑bestand.

## Stap 1 – Installeer en referentieer Aspose OCR

Eerst haal je de bibliotheek in je project. Open een terminal in je solution‑map en voer uit:

```bash
dotnet add package Aspose.OCR
```

Die ene regel haalt de nieuwste stabiele versie op (vanaf jan 2026, versie 23.9). Het pakket bevat de `OcrEngine`‑klasse die we door de hele tutorial heen zullen gebruiken.

## Stap 2 – Initialiseer de OCR‑engine

Het maken van een `OcrEngine`‑instance is de basis. Beschouw het als het inschakelen van een scanner die klaar is om pixels te interpreteren.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Pro tip:** Als je van plan bent om veel afbeeldingen in een lus te verwerken, hergebruik dan dezelfde `OcrEngine`‑instance. Deze cachet interne bronnen en versnelt opeenvolgende aanroepen.

## Stap 3 – Verhoog de nauwkeurigheid met een aangepaste woordenlijst

Standaard OCR is goed, maar kan struikelen over domeinspecifieke woorden zoals “Aspose”, “OCR” of “SDK”. Het toevoegen van die termen aan een **aangepaste woordenlijst** vertelt de engine dat die strings geldig zijn, waardoor mis‑herkenningen worden verminderd.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Waarom een aangepaste woordenlijst helpt

- **Statistische modellen** achter OCR wegen veelvoorkomende taalpatronen zwaar. Ongebruikelijke woorden krijgen een lage waarschijnlijkheid en kunnen worden vervangen door op elkaar lijkende tekens.  
- Door ze expliciet te vermelden, overschrijf je de gok van het model.  
- Het is vooral handig voor **afbeeldingstekst lezen** die productcodes, afkortingen of merknamen bevat.

## Stap 4 – Herken tekst uit het PNG‑bestand

Nu geven we de engine het pad naar de afbeelding. De `RecognizeImage`‑methode retourneert een ruwe string die nog onbekende tokens bevat (bijv. “#@!”) die de engine niet kon toewijzen.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Randgeval:** Als het bestand niet wordt gevonden, gooit `RecognizeImage` een `FileNotFoundException`. Plaats de aanroep in een try‑catch‑blok voor productiecodel.

## Stap 5 – Reinig het resultaat met `CleanText`

Aspose OCR wordt geleverd met een helper die tekens verwijdert die het markeert als “unknown”. Deze stap is cruciaal voor **tekst uit afbeelding extraheren** projecten waarbij downstream‑parsers alleen alfanumerieke tekens en basisinterpunctie verwachten.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

De `CleanText`‑methode normaliseert ook regeleinden, waardoor de output veilig kan worden opgeslagen in databases of doorgegeven aan andere services.

## Stap 6 – Geef de gereinigde tekst weer

Tot slot, toon of sla het resultaat op. In een console‑app doet `Console.WriteLine` het werk.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Wanneer je het programma uitvoert, zou je een net blok tekst moeten zien dat de inhoud van `invoice.png` weerspiegelt. Als de afbeelding het woord “Aspose” bevat, zorgt de aangepaste woordenlijst ervoor dat het correct verschijnt in plaats van iets als “A5p0se”.

## Volledig werkend voorbeeld

Alles samengevoegd, hier is de volledige `Program.cs` die je kunt kopiëren‑en‑plakken in een nieuw console‑project:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Verwachte output** (ervan uitgaande dat de PNG een eenvoudige factuur bevat):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Als je vreemde symbolen ziet, controleer dan de beeldkwaliteit opnieuw of breid de aangepaste woordenlijst uit met meer termen.

## Bonus: Omgaan met scans van lage kwaliteit

Soms worden PNG's gescand op 72 dpi of hebben ze zware compressie‑artefacten. Hier zijn een paar snelle trucjes om **OCR‑nauwkeurigheid te verbeteren** zonder C# te verlaten:

1. **Pre‑process de afbeelding** met een bibliotheek zoals `SixLabors.ImageSharp` – verhoog het contrast, converteer naar grijswaarden, of pas een lichte vervaging toe om ruis te verminderen.  
2. **Stel de `Resolution`‑eigenschap** in op de `OcrEngine` (bijv. `ocrEngine.Resolution = 300;`) om de engine te laten behandelen alsof de afbeelding een hogere resolutie heeft.  
3. **Schakel taalpakketten in** als je met niet‑Engelse tekst werkt (`ocrEngine.Language = Language.English;`).  

Alle drie de benaderingen kunnen worden toegevoegd vóór de `RecognizeImage`‑aanroep.

## Veelgestelde vragen

- **Werkt dit met andere afbeeldingsformaten?**  
  Ja. `RecognizeImage` accepteert JPEG, BMP, TIFF en zelfs PDF (als een afbeeldingscontainer). Dezelfde stappen zijn van toepassing.

- **Kan ik tekst extraheren uit meerdere PNG's in een map?**  
  Absoluut. Plaats de kernlogica in een `foreach (var file in Directory.GetFiles(folder, "*.png"))`‑lus en sla elk resultaat op in een lijst of schrijf naar afzonderlijke bestanden.

- **Wat als ik de tekstcoördinaten nodig heb?**  
  Aspose OCR biedt ook `OcrResult`‑objecten die begrenzingskaders bevatten. Gebruik `ocrEngine.RecognizeImageToResult(imagePath)` voor dat geavanceerde scenario.

## Conclusie

We hebben een **volledige, end‑to‑end** oplossing doorlopen voor **het extraheren van tekst uit PNG**‑bestanden met Aspose OCR. Door de engine te initialiseren, een **aangepaste woordenlijst** te voeden, de ruwe output te reinigen en een paar veelvoorkomende valkuilen te behandelen, kun je betrouwbaar **afbeeldingstekst lezen** en **OCR‑nauwkeurigheid verbeteren** in je eigen C#‑applicaties.

Klaar voor de volgende stap? Probeer de PNG te vervangen door een gescande bon, voeg meer domeinspecifieke woorden toe aan de woordenlijst, of integreer de output met een database voor geautomatiseerde factuurverwerking. De mogelijkheden zijn onbeperkt wanneer je Aspose OCR combineert met het rijke .NET‑ecosysteem.

Veel plezier met coderen, en moge je OCR altijd perfect zijn! 

![Extract text from png example](/images/extract-text-from-png.png "extract text from png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}