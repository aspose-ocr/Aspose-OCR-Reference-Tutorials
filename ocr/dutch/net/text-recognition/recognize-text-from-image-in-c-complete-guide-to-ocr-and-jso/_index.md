---
category: general
date: 2026-01-10
description: Leer hoe je tekst uit een afbeelding herkent, tekstcoördinaten extraheert
  en een bon converteert naar JSON met Aspose OCR in C#. Stapsgewijze tutorial.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: nl
og_description: herken tekst van afbeelding in C# met Aspose OCR. Deze gids laat zien
  hoe je tekst kunt extraheren, coördinaten kunt verkrijgen en een bon kunt omzetten
  naar JSON.
og_title: herken tekst uit afbeelding – Volledige C# OCR‑handleiding
tags:
- OCR
- C#
- Aspose
title: tekst herkennen uit afbeelding in C# – Complete gids voor OCR en JSON
url: /nl/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst uit afbeelding herkennen – volledige C# OCR‑tutorial

Heb je ooit tekst uit een afbeelding moeten herkennen maar wist je niet welke bibliotheek je moest kiezen? Je bent niet de enige. In veel real‑world apps—uitgaven trackers, bon scanners, of documentarchieven—het betrouwbaar extraheren van tekst is de eerste hindernis.  

In deze tutorial lopen we stap voor stap door **hoe tekst te extraheren**, halen we de begrenzings‑boxen eruit, en uiteindelijk **bon omzetten naar JSON** met Aspose.OCR voor .NET. Aan het einde heb je een zelf‑containend C#‑project dat een foto van een bon neemt en een nette JSON‑file met confidence scores en coördinaten genereert.

## Wat je nodig hebt

Voordat we beginnen, zorg ervoor dat je het volgende op je machine hebt:

- **.NET 6.0 SDK** (of een latere versie). Oudere frameworks werken ook, maar .NET 6 is de ideale keuze voor moderne bibliotheken.
- **Visual Studio 2022** of VS Code met de C#‑extensie.
- **Aspose.OCR for .NET** NuGet‑package (`Aspose.OCR` en `Aspose.OCR.Output`). Je kunt het installeren via de Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Een voorbeeldbon‑afbeelding (bijv. `receipt.jpg`) geplaatst in een map die je later zult refereren.

Dat is alles—geen extra SDK’s, geen native binaries, alleen pure managed code.

## Stap 1: Maak een nieuw console‑project

Allereerst, maak een console‑app. Het is de snelste manier om OCR te testen zonder UI‑overhead.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Pro tip:** Houd de projectmap netjes; maak een sub‑map genaamd `Resources` en plaats `receipt.jpg` daar. Het maakt pad‑afhandeling moeiteloos.

## Stap 2: Laad de bon‑afbeelding

Nu gaan we daadwerkelijk **tekst uit afbeelding herkennen**. De eerste stap is om de OCR‑engine naar het bestand te wijzen.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Waarom wikkelen we het laden in een eenvoudige bestaan‑check? Omdat je in productie vaak te maken hebt met gebruikers‑uploads die mogelijk ontbreken of corrupt zijn. Het vroegtijdig vangen van het probleem bespaart je later cryptische uitzonderingen.

## Stap 3: Voer OCR uit – **tekst uit afbeelding herkennen**

Met de afbeelding in het geheugen vragen we Aspose om **tekst uit afbeelding te herkennen**. Deze bewerking is synchroon en retourneert een rijk resultaat.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Achter de schermen draait Aspose een neuraal netwerk getraind op miljoenen tekens. De engine vult `ocrEngine.Text`, `ocrEngine.RecognitionResult` en een collectie van `OcrRegion`‑objecten die coördinaten bevatten. Dat is precies wat we nodig hebben voor de volgende stap.

## Stap 4: **Hoe tekst te extraheren** – De ruwe string ophalen

Als je alleen geïnteresseerd bent in de platte tekst (misschien voor een snelle zoekopdracht), kun je deze rechtstreeks uit de engine halen:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Je zult regelbreuken opmerken waar de OCR alinea‑grenzen heeft gedetecteerd. In veel bon‑scan‑scenario's is de ruwe string voldoende om totalen, datums of verkopersnamen te extraheren met eenvoudige regexes.

## Stap 5: **tekstcoördinaten extraheren** – Begrenzings‑boxen voor elk woord

Vaak moet je weten *waar* op de afbeelding een bepaald stuk tekst zich bevindt—bijvoorbeeld om het totaalbedrag in een UI te markeren. Aspose levert dat via `OcrRegion`‑objecten.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Merk op dat we over **tekstcoördinaten extraheren** itereren voor elk herkend segment. De coördinaten zijn relatief ten opzichte van de originele afbeelding, zodat je ze kunt overlayen in een grafisch canvas of HTML `<canvas>`‑element.

## Stap 6: **bon omzetten naar JSON** – Gedetailleerde resultaten opslaan

Nu komt het deel dat alles samenbrengt: we willen een machine‑leesbare structuur die de tekst, confidence scores en de begrenzings‑boxen bevat. Aspose levert `JsonSaveOptions` mee die dit een fluitje‑van‑een‑deurtje maken.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Het resulterende bestand ziet er ongeveer zo uit (ingekort voor beknoptheid):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Je hebt nu een **bon omzetten naar JSON** artefact dat kan worden gevoed aan downstream‑services—denk aan expense‑report API’s, analytics‑pijplijnen, of zelfs een eenvoudige UI die rechthoeken rond elk woord tekent.

## Volledig werkend voorbeeld

Door alle onderdelen samen te voegen, hier is de volledige `Program.cs` die je kunt copy‑pasten in je project:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Voer het programma uit (`dotnet run`) en bekijk de console‑output. Open `Resources/receipt.json` om de structuur te verifiëren.

## Veelgestelde vragen & randgevallen

- **Wat als de afbeelding onscherp is?**  
  Aspose OCR werkt het beste met 300 dpi of hoger. Als je lage confidence scores krijgt, overweeg dan een verscherpingsfilter toe te passen voordat je de afbeelding aan de engine geeft.

- **Kan ik meerdere talen herkennen?**  
  Ja. Stel `ocrEngine.Language = Language.English | Language.Spanish;` in voordat je `Recognize()` aanroept.

- **Hoe beperk ik de output tot alleen cijfers (bijv. totalen)?**  
  Nadat je de platte tekst hebt, voer je een regex uit zoals `\d+\.\d{2}` op `ocrEngine.Text`. Omdat we al coördinaten hebben, kun je de gevonden string terugkoppelen naar zijn regio voor visuele markering.

- **Is het JSON‑formaat aanpasbaar?**  
  De `JsonSaveOptions`‑klasse biedt een aantal vlaggen. Als je een volledig aangepast schema nodig hebt, kun je itereren over `ocrEngine.RecognitionResult.Regions` en de objecten zelf serialiseren met `System.Text.Json`.

## Conclusie

We hebben zojuist laten zien hoe je **tekst uit afbeelding kunt herkennen** in C# met Aspose.OCR, **hoe je tekst kunt extraheren**, **tekstcoördinaten kunt extraheren**, en uiteindelijk **bon kunt omzetten naar JSON**. De volledige flow zit in één eenvoudig‑te‑runnen console‑app, waardoor het perfect is voor prototypes of als bouwsteen in grotere systemen.

Volgende stappen? Probeer de JSON te voeden aan een front‑end dat de begrenzings‑boxen tekent, of koppel de output aan een expense‑report service. Je kunt ook experimenteren met verschillende afbeeldingsformaten (PNG, TIFF) of een map met bonnen batch‑verwerken.

Heb je meer vragen over OCR, Aspose of JSON‑verwerking? Laat een reactie achter hieronder, en happy coding! 

![Voorbeeld van bonafbeelding voor tekst uit afbeelding herkennen](receipt.jpg "Voorbeeld van bonafbeelding")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}