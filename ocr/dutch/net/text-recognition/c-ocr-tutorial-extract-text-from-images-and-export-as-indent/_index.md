---
category: general
date: 2026-05-02
description: c# ocr‑tutorial die laat zien hoe je tekst uit een afbeelding haalt met
  c# en png‑tekst herkent, en vervolgens ingesprongen json schrijft met JsonSerializer
  c#. Stapsgewijze gids voor ontwikkelaars.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: nl
og_description: c# OCR-tutorial die laat zien hoe je tekst uit een afbeelding haalt
  met c# en png‑tekst herkent, en vervolgens ingesprongen JSON schrijft met JsonSerializer
  c#. Volledig, uitvoerbaar voorbeeld.
og_title: c# OCR-tutorial – Tekst extraheren en exporteren als ingesprongen JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR-tutorial – Tekst uit afbeeldingen extraheren en exporteren als ingesprongen
  JSON
url: /nl/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Tekst uit afbeeldingen extraheren en exporteren als ingesprongen JSON

Heb je ooit een **c# ocr tutorial** nodig gehad die van een foto van tekst direct naar een netjes opgemaakte JSON‑bestand gaat? Je bent niet de enige. In veel projecten – denk aan factuurscanning, bon‑parsing, of zelfs eenvoudige meme‑tekstextractie – eindig je met een PNG‑bestand en vraag je je af hoe je de woorden eruit haalt zonder een eigen recognizer te schrijven.  

Deze gids biedt een praktische oplossing: we gaan **extract text image c#** gebruiken met Aspose.OCR, **recognize png text**, en vervolgens **write indented json** met `JsonSerializer` in C#. Aan het einde heb je een zelfstandige console‑app die je in elke .NET‑oplossing kunt plaatsen. Geen vage “zie de docs”‑links, maar een compleet, copy‑and‑paste‑klaar voorbeeld.

## Wat je nodig hebt

- **.NET 6** (of een recente .NET‑versie). Oudere frameworks werken ook, maar de getoonde syntax richt zich op .NET 6+.
- **Aspose.OCR for .NET** – installeer via NuGet: `dotnet add package Aspose.OCR`.
- Een voorbeeld‑PNG‑afbeelding (`text.png`) met duidelijke, machinaal leesbare tekst.
- Een IDE of editor naar keuze – Visual Studio, VS Code, Rider, etc.

> **Pro tip:** Als je veel afbeeldingen wilt verwerken, overweeg dan om één enkele `OcrEngine`‑instantie te hergebruiken in plaats van voor elk bestand een nieuwe te maken. Dat vermindert overhead en verbetert de doorvoersnelheid.

## Stap 1: Een c# ocr tutorial‑project opzetten

Maak eerst een console‑project. De volgende commando’s creëren de basisstructuur en halen de OCR‑bibliotheek binnen:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Open nu het gegenereerde `Program.cs`. We zullen later de volledige voorbeeldcode hier invoegen, maar zorg er nu voor dat het project bouwt:

```bash
dotnet build
```

Als er geen fouten verschijnen, kun je doorgaan.

## Stap 2: PNG‑tekst herkennen uit een afbeelding

Het hart van elke **c# ocr tutorial** is de OCR‑engine zelf. Aspose.OCR verbergt de low‑level details en biedt een nette `OcrEngine`‑klasse. Hieronder maken we de engine, wijzen we naar een PNG‑bestand, en laten we hem de tekst herkennen.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Waarom dit werkt

- **`RecognizeImage`** accepteert vele formaten (PNG, JPEG, BMP). We **recognize png text** specifiek omdat PNG verliesvrije details behoudt, wat ideaal is voor OCR.
- Het geretourneerde `OcrResult` bevat niet alleen de platte tekst maar ook een confidence‑score per glyph, handig als je later tekens met lage confidence wilt filteren.

## Stap 3: Ingesprongen JSON schrijven met JsonSerializer c#

Nu we `ocrResult` hebben, is de logische volgende stap in onze **c# ocr tutorial** om dat object om te zetten naar mens‑leesbare JSON. De ingebouwde `System.Text.Json`‑serializer doet het werk, en we configureren hem om **write indented json** voor duidelijkheid.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### `JsonSerializer` correct gebruiken

- De `WriteIndented`‑vlag is de eenvoudigste manier om **write indented json** te realiseren zonder externe bibliotheken.
- Als je ooit camel‑case eigenschapsnamen nodig hebt, voeg dan `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` toe aan de opties.
- De `jsonOutput`‑string kun je opslaan met `File.WriteAllText("result.json", jsonOutput);` – een handige tweak voor real‑world pipelines.

## Stap 4: Uitvoeren en de output verifiëren

Compileer en voer het programma uit:

```bash
dotnet run
```

Als `text.png` de zin *“Hello, OCR World!”* bevat, zie je zoiets als:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Die JSON is **ingesprongen**, waardoor hij makkelijk leesbaar is in logs of voor downstream services.

### Randgevallen & Tips

| Situatie | Wat te doen |
|-----------|------------|
| **Afbeelding is onscherp** | Verhoog `ocrEngine.Config.Dpi` (bijv. `ocrEngine.Config.Dpi = 300`) vóór het aanroepen van `RecognizeImage`. |
| **Niet‑Engelse taal** | Stel `ocrEngine.Config.Language = OcrLanguage.German` in (of een andere ondersteunde taal). |
| **Grote batch bestanden** | Loop over een map, hergebruik dezelfde `OcrEngine`‑instantie; sla elk JSON‑resultaat op met een unieke bestandsnaam. |
| **Alleen hoge‑confidence tekst nodig** | Filter `ocrResult.Lines` waar `Confidence` ≥ 0.95 vóór serialisatie. |

## Volledig werkend voorbeeld (Klaar om te kopiëren)

Hieronder staat het *complete* programma, klaar om in `Program.cs` te plakken. Het bevat alle stappen, foutafhandeling en commentaar die de code zelf‑verklarend maken.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Voer de code uit, bekijk de console of het gegenereerde `.json`‑bestand, en je ziet de geëxtraheerde tekst met confidence‑scores, allemaal netjes **ingesprongen**.

## Conclusie

Je hebt nu een degelijke **c# ocr tutorial** die laat zien hoe je **extract text image c#**, **recognize png text**, en **write indented json** kunt uitvoeren met `JsonSerializer`. Het voorbeeld is compleet, uitvoerbaar, en bevat praktische tips voor real‑world scenario’s.  

Volgende stappen? Vervang Aspose.OCR door een andere engine (bijv. Tesseract) en kijk hoe de structuur van `OcrResult` verandert, of stuur de JSON door naar een downstream API die OCR‑data in een database opslaat. Je kunt ook experimenteren met **use jsonserializer c#**‑opties zoals custom converters voor datum‑formattering of enum‑handling.

Happy coding, en moge je OCR‑pipelines altijd accuraat zijn!  

---  

![c# ocr tutorial diagram](image.png "Diagram dat OCR‑stroom illustreert")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}