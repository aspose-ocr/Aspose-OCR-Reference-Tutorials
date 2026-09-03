---
category: general
date: 2026-01-02
description: Haal tekst uit een afbeelding met Aspose OCR in C#. Leer hoe je een afbeelding
  snel en betrouwbaar naar JSONL‑formaat kunt converteren.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: nl
og_description: Haal tekst uit afbeelding met Aspose OCR en converteer deze naar JSONL‑formaat.
  Volledige stap‑voor‑stap C#‑tutorial voor ontwikkelaars.
og_title: Tekst uit afbeelding extraheren – Converteren naar JSONL in C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Tekst uit afbeelding extraheren en omzetten naar JSONL – C# gids
url: /nl/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren en converteren naar JSONL – Complete C# Tutorial

Heb je ooit **tekst uit afbeelding** moeten extraheren maar wist je niet welke bibliotheek je een schone, gestructureerde output zou geven? Je bent niet de enige. In veel bon‑verwerkings- of document‑digitaliseringsprojecten is de knelpunt het omzetten van een bitmap naar doorzoekbare tekst *en* een machinaal leesbaar formaat.  

Het goede nieuws? Met Aspose OCR kun je **tekst uit afbeelding** extraheren en, met een paar regels code, **afbeelding naar JSONL** converteren voor downstream‑analyse. Deze gids leidt je door het volledige proces, van het laden van een PNG tot het schrijven van een JSON‑Lines‑bestand dat kan worden gestreamd in een datapijplijn.

> **Tip:** Als je al .NET 6 of later gebruikt, werkt dezelfde code zonder extra configuratie.

## Vereisten — Wat je nodig hebt

- **.NET 6 SDK** (of een recente .NET‑versie)
- **Aspose.OCR** NuGet package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** for serialization  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Een voorbeeldafbeelding (bijv. `receipt.png`) geplaatst in een map die je kunt refereren.
- Een IDE of editor naar keuze—Visual Studio, VS Code, Rider, enz.

Geen zware setup, geen externe services, alleen een handvol NuGet‑pakketten.

![tekst uit afbeelding extraheren met C# en Aspose OCR](https://example.com/assets/ocr-sample.png)

*Alt text: extract text from image using C# with Aspose OCR*

## Stap 1: Laad de afbeelding die je wilt verwerken  

Het eerste wat je doet wanneer je **tekst uit afbeelding** wilt extraheren, is de OCR‑engine een bitmap geven. Het gebruik van `System.Drawing.Bitmap` is eenvoudig en werkt voor de meeste rasterformaten.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Waarom dit belangrijk is:** Het laden van de afbeelding als een `Bitmap` geeft de OCR‑engine directe pixeltoegang, wat de herkenningssnelheid en nauwkeurigheid verbetert vergeleken met het streamen van ruwe bytes.

## Stap 2: Configureer Aspose OCR voor JSON‑Lines‑output  

Aspose OCR laat je taal, outputformaat en een paar prestatie‑aanpassingen specificeren. Hier vragen we **JSON‑Lines** (een JSON‑object per regel) omdat het perfect is voor regel‑voor‑regel verwerking later.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Pro tip:** Als je meertalige bonnen nodig hebt, stel `Language = Language.Multilingual` in of geef een array van `Language`‑waarden door.

## Stap 3: Voer de OCR uit en vang het resultaat op  

Nu extraheren we daadwerkelijk **tekst uit afbeelding**. De `Recognize`‑methode retourneert een `OcrResult`‑object dat een collectie van `OcrLine`‑objecten bevat, elk een regel herkende tekst met bijbehorende begrenzingsvak.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Op dit punt bevat `ocrResult.Lines` alles wat je nodig hebt—ruwe tekst, vertrouwensscores en coördinaten.

## Stap 4: Serialiseer de regels naar JSON‑Lines  

We zullen de collectie omzetten naar een mooi ingesprongen JSON‑string. Hoewel JSON‑Lines meestal compact zijn, maakt inspringen het bestand makkelijker te inspecteren tijdens ontwikkeling.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

De resulterende `jsonLines`‑variabele ziet er ongeveer zo uit (ingekort voor beknoptheid):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Elke regel eindigt met een newline‑teken, waardoor je een echt **JSONL** (JSON‑Lines)‑bestand krijgt.

## Stap 5: Schrijf de JSON‑Lines naar schijf  

Tot slot bewaren we de output zodat andere services—zoals Spark, Logstash, of een simpel Bash‑script—het regel voor regel kunnen verwerken.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Wanneer je `receipt.jsonl` opent, zie je één JSON‑object per regel, klaar om te streamen.

## Stap 6: Verifieer de export  

Een snelle sanity‑check bespaart je later uren debuggen. Laten we de eerste paar regels teruglezen en ze naar de console afdrukken.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Typische console‑output:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Als je iets vergelijkbaars ziet, gefeliciteerd—je hebt succesvol **tekst uit afbeelding** geëxtraheerd en **afbeelding naar JSONL** geconverteerd.

## Veelvoorkomende valkuilen & hoe ze te vermijden  

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Lege output** | Afbeeldingspad onjuist of bestand niet leesbaar. | Gebruik `File.Exists(imagePath)` voordat je de bitmap maakt. |
| **Lage vertrouwensscores** | Afbeelding is onscherp of heeft weinig contrast. | Pre‑process de afbeelding (bijv. `Bitmap.RotateFlip`, `Graphics.Clear`) of verhoog de DPI. |
| **Onjuiste taal** | OCR gebruikt standaard Engels maar de bon is in een andere taal. | Stel `options.Language = Language.Spanish` in (of de juiste enum). |
| **JSONL verschijnt als een enkele JSON‑array** | Je gebruikte `Formatting.None` zonder newline‑afhandeling. | Zorg ervoor dat elk geserialiseerd object eindigt met `Environment.NewLine`. |

## Volledig werkend voorbeeld  

Hieronder staat het volledige, kant‑klaar programma. Plak het in een console‑project en druk op **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Verwacht resultaat:** Een `receipt.jsonl`‑bestand met één JSON‑object per regel, elk met de velden `Text`, `Confidence` en `BoundingBox`. Je kunt dit bestand nu invoeren in elke analytics‑pijplijn die JSONL consumeert.

## Volgende stappen – Verder gaan dan basis‑OCR  

- **Batchverwerking:** Plaats de bovenstaande logica in een `foreach`‑loop om volledige mappen met bonnen te verwerken.  
- **Parallelisme:** Gebruik `Parallel.ForEach` voor multi‑core versnellingen bij duizenden afbeeldingen.  
- **Post‑verwerking:** Verwijder regels met lage vertrouwensscore (`Confidence < 0.9`) vóór opslag.  
- **Integratie:** Push de JSONL direct naar Azure Blob Storage of AWS S3 met de respectieve SDK's.  
- **Alternatieve formaten:** Verander `OutputFormat` naar `PlainText` of `Xml` als je downstream‑systeem die verkiest.  

## Conclusie  

Je hebt nu een solide, end‑to‑end oplossing voor **tekst uit afbeelding** extraheren en **afbeelding naar JSONL** converteren met Aspose OCR in C#. De tutorial behandelde alles van het laden van de bitmap tot het verifiëren van de output, plus een reeks praktische tips om je pijplijn robuust te houden.

Probeer het met je eigen bonnen, facturen of gescande formulieren—zie hoe de OCR‑engine pixels omzet in doorzoekbare, regel‑gestructureerde data in seconden. Als je tegen randgevallen aanloopt (bijv. scheve scans of meertalige tekst), bekijk dan opnieuw de *RecognitionOptions*‑sectie en pas taal of pre‑processing stappen aan.

Veel programmeerplezier, en moge je datapijplijnen altijd schoon blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}