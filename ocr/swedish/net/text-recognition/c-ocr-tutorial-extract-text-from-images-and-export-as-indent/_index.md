---
category: general
date: 2026-05-02
description: c# ocr‑handledning som visar hur man extraherar text från bild i c# och
  känner igen png‑text, sedan skriver indenterad json med JsonSerializer i c#. Steg‑för‑steg‑guide
  för utvecklare.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: sv
og_description: c# OCR-handledning som demonstrerar hur man extraherar text från en
  bild i c# och känner igen png‑text, sedan skriver indenterad JSON med JsonSerializer
  c#. Komplett, körbart exempel.
og_title: c# OCR-handledning – Extrahera text och exportera som indenterad JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR-handledning – Extrahera text från bilder och exportera som indenterad
  JSON
url: /sv/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Extrahera text från bilder och exportera som indenterad JSON

Har du någonsin behövt en **c# ocr tutorial** som går från en bild av text direkt till en snyggt formaterad JSON‑fil? Du är inte ensam. I många projekt – tänk fakturaskanning, kvitto‑parsing eller till och med enkel meme‑textutdragning – slutar du med en PNG‑fil och undrar hur du får ut orden utan att skriva en egen igenkännare.  

Den här guiden ger dig en praktisk lösning: vi kommer **extract text image c#** med Aspose.OCR, **recognize png text**, och sedan **write indented json** med `JsonSerializer` i C#. I slutet har du en fristående konsolapp som du kan släppa in i vilken .NET‑lösning som helst. Inga vaga “se dokumentationen”-länkar, bara ett komplett, kopiera‑och‑klistra‑klart exempel.

## Vad du behöver

- **.NET 6** (eller någon nyare .NET‑version). Äldre ramverk fungerar, men syntaxen som visas riktar sig mot .NET 6+.
- **Aspose.OCR for .NET** – installera via NuGet: `dotnet add package Aspose.OCR`.
- En exempel‑PNG‑bild (`text.png`) som innehåller klar, maskinläsbar text.
- En IDE eller editor du föredrar – Visual Studio, VS Code, Rider, etc.

> **Pro tip:** Om du planerar att bearbeta många bilder, överväg att återanvända en enda `OcrEngine`‑instans istället för att skapa en ny för varje fil. Det minskar overhead och förbättrar genomströmning.

## Steg 1: Skapa ett c# ocr tutorial‑projekt

Först, skapa ett konsolprojekt. Följande kommandon skapar strukturen och hämtar OCR‑biblioteket:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Öppna nu den genererade `Program.cs`. Vi kommer att ersätta dess innehåll med hela exemplet senare, men för tillfället se bara till att projektet bygger:

```bash
dotnet build
```

Om du inte får några fel är du redo att gå vidare.

## Steg 2: Känn igen PNG‑text från en bild

Kärnan i varje **c# ocr tutorial** är OCR‑motorn själv. Aspose.OCR döljer de lågnivådetaljerna och ger dig en ren `OcrEngine`‑klass. Nedan skapar vi motorn, pekar den på en PNG‑fil och ber den att känna igen texten.

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

### Varför detta fungerar

- **`RecognizeImage`** accepterar många format (PNG, JPEG, BMP). Vi **recognize png text** specifikt eftersom PNG bevarar förlustfri detalj, vilket är idealiskt för OCR.
- Det returnerade `OcrResult` innehåller inte bara ren text utan även ett för‑glyph förtroendescore, användbart om du senare behöver filtrera lågt förtroende‑tecken.

## Steg 3: Skriv indenterad JSON med JsonSerializer c#

Nu när vi har `ocrResult` är nästa logiska steg i vår **c# ocr tutorial** att omvandla det objektet till mänskligt läsbar JSON. Den inbyggda `System.Text.Json`‑serialisatorn klarar jobbet, och vi kommer att konfigurera den för att **write indented json** för tydlighet.

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

### Använda `JsonSerializer` korrekt

- `WriteIndented`‑flaggan är det enklaste sättet att **write indented json** utan att ta in tredjepartsbibliotek.
- Om du någonsin behöver camel‑case egenskapsnamn, lägg till `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` i alternativen.
- `jsonOutput`‑strängen kan sparas med `File.WriteAllText("result.json", jsonOutput);` – ett praktiskt knep för verkliga pipelines.

## Steg 4: Kör och verifiera resultatet

Kompilera och kör programmet:

```bash
dotnet run
```

Om vi antar att `text.png` innehåller frasen *“Hello, OCR World!”*, bör du se något liknande:

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

Den JSON‑en är **indented**, vilket gör den lätt att läsa i loggar eller att överlämna till nedströms tjänster.

### Särskilda fall & Tips

| Situation | Vad man ska göra |
|-----------|-------------------|
| **Image is blurry** | Öka `ocrEngine.Config.Dpi` (t.ex. `ocrEngine.Config.Dpi = 300`) innan du anropar `RecognizeImage`. |
| **Non‑English language** | Sätt `ocrEngine.Config.Language = OcrLanguage.German` (eller något annat stödjert språk). |
| **Large batch of files** | Loopa över en katalog, återanvänd samma `OcrEngine`‑instans; spara varje JSON‑resultat med ett unikt filnamn. |
| **Need only high‑confidence text** | Filtrera `ocrResult.Lines` där `Confidence` ≥ 0.95 innan serialisering. |

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

Nedan är hela programmet, redo att klistras in i `Program.cs`. Det inkluderar alla steg, felhantering och kommentarer som gör koden självförklarande.

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

Kör koden, inspektera konsolen eller den genererade `.json`‑filen, och du kommer att se den extraherade texten tillsammans med förtroendescore, allt snyggt **indented**.

## Slutsats

Du har nu ett gediget **c# ocr tutorial** som visar hur man **extract text image c#**, **recognize png text**, och **write indented json** med `JsonSerializer`. Exemplet är komplett, körbart och innehåller praktiska tips för verkliga scenarier.  

Nästa steg? Prova att byta ut Aspose.OCR mot en annan motor (t.ex. Tesseract) och se hur `OcrResult`‑strukturen förändras, eller skicka JSON‑en till ett nedströms API som lagrar OCR‑data i en databas. Du kan också experimentera med **use jsonserializer c#**‑alternativ som anpassade konverterare för datumformat eller enum‑hantering.

Lycklig kodning, och må dina OCR‑pipelines alltid vara exakta!  

---  

![c# ocr tutorial diagram](image.png "Diagram som illustrerar OCR-flöde")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}