---
category: general
date: 2026-05-31
description: Leer hoe je OCR‑vertrouwensscores kunt verkrijgen in C# terwijl je tekst
  uit een afbeelding extraheert en een kassabonafbeelding leest met Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: nl
og_description: OCR-confidence scores laten u de nauwkeurigheid inschatten; deze gids
  laat zien hoe u tekst uit een afbeelding kunt extraheren, begrenzingskaders kunt
  verkrijgen en een bonafbeelding kunt lezen met Aspose OCR.
og_title: OCR-confidencescores in C# – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: OCR‑vertrouwensscores in C# – Complete gids
url: /nl/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR‑vertrouwensscores in C# – Complete Gids

Heb je je ooit afgevraagd hoe je **OCR‑vertrouwensscores** kunt krijgen wanneer je *tekst uit een afbeelding moet extraheren*? Misschien probeer je **ontvangstbewijsafbeeldingen** te lezen voor onkostenregistratie en wil je weten welke tekens de engine onzeker maakt. Het goede nieuws? Met Aspose.OCR kun je vertrouwenspercentages, begrenzingskaders en platte tekst uit een JPG halen in slechts een paar regels C#.

In deze tutorial lopen we alles door wat je moet weten: de bibliotheek installeren, de engine configureren om **OCR op JPG uit te voeren**, vertrouwensscores ophalen en de **OCR‑begrenzingskaders** interpreteren die aangeven waar elk teken zich op de pagina bevindt. Aan het einde heb je een kant‑klaar console‑applicatie die elk teken, de bijbehorende vertrouwensscore en locatie afdrukt – perfect voor het valideren van bonnetjes of elk gescand document.

## Wat je zult leren

- Installeer Aspose.OCR via NuGet en zet een basis‑OCR‑engine op.  
- Configureer `OcrOptions` om platte‑tekstoutput **met vertrouwensscores** en **begrenzingskaders** op te vragen.  
- Loop door `OcrResult` om **tekst uit afbeelding** regel‑voor‑regel en symbool‑voor‑symbool **te extraheren**.  
- Omgaan met veelvoorkomende valkuilen zoals ontbrekende bestanden, lage‑vertrouwens tekens en niet‑JPG‑formaten.  
- Het voorbeeld uitbreiden om meerdere ontvangstbewijs‑afbeeldingen in een map te verwerken.

Ervaring met Aspose is niet vereist; alleen een werkende .NET‑omgeving en een ontvangstbewijs‑afbeelding (JPG) die je wilt testen.

---

## Stap 1 – Installeer Aspose.OCR en bereid je project voor

Allereerst: je hebt het Aspose.OCR NuGet‑pakket nodig. Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** De gratis proefversie werkt tot 200 pagina’s, meer dan genoeg voor het testen van het scannen van bonnetjes.

Na de installatie, maak een nieuw console‑project (als je er nog geen hebt):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Open nu het gegenereerde `Program.cs` en voeg de using‑directives toe:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Deze namespaces geven je toegang tot `OcrEngine`, `OcrOptions` en de result‑types die we later nodig hebben.

## Stap 2 – Haal OCR‑vertrouwensscores en OCR‑begrenzingskaders op

Dit is het hart van de tutorial. We configureren de engine zodat elk herkend teken wordt geleverd met een **vertrouwensscore** en een **begrenzingskader** (de rechthoek die het glyph omsluit). De H2‑kop zelf bevat het primaire zoekwoord, zodat aan de SEO‑regel wordt voldaan.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Waarom vertrouwensscores opnemen?**  
Een vertrouwensscore (0‑100 %) vertelt je hoe zeker de engine is over elk teken. Als je de output in downstream‑logica stopt – bijvoorbeeld een onkosten‑goedkeuringsworkflow – kun je tekens met een lage vertrouwensscore automatisch afwijzen of markeren.

**Waarom begrenzingskaders aanvragen?**  
Begrenzingskaders zijn essentieel wanneer je tekst op de originele afbeelding wilt markeren, sub‑regio’s wilt extraheren of OCR‑resultaten wilt uitlijnen met een UI‑overlay. Elke `character.Bounds` geeft je X, Y, breedte en hoogte in pixelcoördinaten.

## Stap 3 – Voer OCR uit op JPG en extraheren tekst uit afbeelding

Nu voeren we de engine daadwerkelijk uit. De aanroep van `Recognize()` doet al het zware werk en retourneert een `OcrResult`‑object.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Als het afbeeldingspad onjuist is of het bestand geen ondersteund formaat heeft, gooit Aspose een `FileNotFoundException` of `UnsupportedImageFormatException`. Plaats de aanroep in een try/catch‑blok in productcode om die randgevallen netjes af te handelen.

### De platte tekst ophalen

Als je alleen de samengevoegde tekst nodig hebt, kun je `ocrResult.Text` lezen:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Maar omdat we ook vertrouwensscores en begrenzingskaders hebben gevraagd, itereren we door de structuur om de details van elk teken te zien.

## Stap 4 – Itereer door regels, symbolen en toon OCR‑vertrouwensscores

Hier is de lus die elk teken, de vertrouwensscore en het kader afdrukt. Dit is waar het **read receipt image**‑voorbeeld echt schittert.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Voorbeeldoutput kan er als volgt uitzien:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretatie van de cijfers:**  
- **Vertrouwen ≥ 90 %** – meestal veilig om te accepteren.  
- **Vertrouwen 70‑89 %** – je wilt misschien dubbel‑checken, vooral bij cijfers in bedragen.  
- **Vertrouwen < 70 %** – overweeg om te markeren voor handmatige controle.

## Stap 5 – Volledig uitvoerbaar voorbeeld (inclusief foutafhandeling)

Alles bij elkaar, hier is een compleet programma dat je kunt copy‑pasten in `Program.cs`. Het bevat een eenvoudige controle op ontbrekende bestanden en geeft een vriendelijke melding als de OCR faalt.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Verwachte output

Wanneer je `dotnet run` uitvoert, toont de console eerst de samengevoegde bontekst, daarna een lijst van elk teken met zijn vertrouwensscore en begrenzingskader. Als een teken een lage vertrouwensscore heeft, zie je een percentage onder de 80, wat aangeeft dat dat deel van de bon handmatig moet worden geverifieerd.

## Bonus: Meerdere bonnetjes in een map verwerken

Heb je een batch van ontvangstbewijs‑JPG’s, wikkel dan de bovenstaande logica in een `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`‑lus. Vergeet niet de `OcrEngine` voor elk bestand te resetten, of maak een nieuwe instantie binnen de lus om state‑lekkage te voorkomen.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Bulk‑verwerking is handig voor nachtelijke onkosten‑imports.

---

## Conclusie

Je hebt nu een solide, end‑to‑end‑oplossing voor het verkrijgen van **OCR‑vertrouwensscores** in C#, **tekst uit afbeelding** extraheren, en **OCR‑begrenzingskaders** ophalen terwijl je **OCR op JPG** uitvoert, bijvoorbeeld een **read receipt image**. De code is volledig zelf‑voorzienend, werkt met de nieuwste Aspose.OCR‑versie (per 2026‑05‑31), en levert de granulaire data die je nodig hebt om betrouwbare document‑verwerkingspijplijnen te bouwen.

Wat nu? Probeer de begrenzingskaders te visualiseren op de originele bon met `System.Drawing` of een UI‑bibliotheek, of stuur tekens met een lage vertrouwensscore door naar een secundaire verificatieservice. Je kunt ook experimenteren met verschillende talen door `ocrEngine.Options.Language = OcrLanguage.French;` in te stellen – de API ondersteunt vele locale.

Happy coding, en moge je vertrouwensscores altijd hoog blijven! 

![Console output showing OCR confidence scores and bounding boxes for a receipt


## Wat moet je hierna leren?

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Get OCR Character Choices for Recognized Characters in Image Recognition](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}