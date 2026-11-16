---
category: general
date: 2026-03-17
description: Leer hoe je JSON van OCR-resultaten kunt parseren in C#. Deze tutorial
  behandelt hoe je tekst kunt extraheren, een afbeelding kunt laden voor OCR, OCR-herkenning
  kunt uitvoeren en de OCR-engine in C# efficiënt kunt gebruiken.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: nl
og_description: Hoe JSON van OCR-uitvoer te parseren in C#. Volg onze gids om tekst
  te extraheren, een afbeelding te laden voor OCR, OCR-herkenning uit te voeren en
  de OCR-engine in C# te gebruiken.
og_title: Hoe JSON te parseren met OCR Engine C# – Volledige tutorial
tags:
- C#
- OCR
- JSON
- Image Processing
title: Hoe JSON te parseren met OCR Engine C# – Complete stap‑voor‑stap gids
url: /nl/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe JSON te parseren met OCR Engine C# – Complete Stapsgewijze Gids

Heb je je ooit afgevraagd **how to parse json** die rechtstreeks uit een OCR‑engine komt? Je bent niet de enige. De meeste ontwikkelaars lopen tegen hetzelfde probleem aan—ruwe JSON ontvangen en vervolgens de beste manier vinden om de bruikbare onderdelen zoals confidence‑scores of de eigenlijke tekst te extraheren. In deze gids lopen we door het laden van een afbeelding voor OCR, het uitvoeren van OCR‑herkenning, en uiteindelijk **how to parse json** op een schone, onderhoudbare manier.

Aan het einde van de tutorial kun je:

* Een afbeelding voor OCR laden met slechts een paar regels code.  
* OCR‑herkenning uitvoeren met een C# OCR‑engine.  
* **How to extract text** en andere metadata uit de JSON‑payload halen.  
* Veelvoorkomende randgevallen (ontbrekende velden, onverwachte formaten) afhandelen zonder te crashen.

Geen externe documentatie nodig—alles wat je nodig hebt staat hier.

## Prerequisites

Voordat we beginnen, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code compileert ook op .NET Framework 4.7+).  
* Een referentie naar de OCR‑bibliotheek die je gebruikt (het voorbeeld maakt gebruik van een hypothetische `OcrEngine`‑klasse).  
* Het `Newtonsoft.Json` NuGet‑pakket voor JSON‑verwerking (`Install-Package Newtonsoft.Json`).  
* Een afbeeldingsbestand (bijv. `passport.png`) op een locatie die je app kan lezen.

> **Pro tip:** Als je een commercieel OCR‑SDK gebruikt, controleer dan of het JSON‑outputformaat is ingeschakeld—de meeste leveranciers bieden dit via een configuratie‑eigenschap zoals `ocrEngine.Config.OutputFormat`.

## Step 1 – Create and Configure the OCR Engine (Primary Keyword in Action)

Het eerste wat je moet doen is de OCR‑engine instantieren en aangeven dat deze JSON moet retourneren. Hier verschijnt de frase **how to parse json** voor het eerst in onze code, omdat de engine ons een JSON‑string zal geven die we later gaan parseren.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Waarom dit belangrijk is:** Het instellen van `OutputFormat` op `Json` zorgt ervoor dat de respons zowel de herkende tekst **als** nuttige metadata zoals confidence‑scores bevat. Als je deze stap vergeet, krijg je platte tekst terug en wordt **how to parse json** een overbodige kwestie.

## Step 2 – Load Image for OCR

Nu laden we de afbeelding die we willen analyseren. Dit is precies het moment waarop het secundaire trefwoord **load image for OCR** schittert.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Wat als het bestand er niet is?** Plaats de aanroep in een `try/catch` en toon een vriendelijke melding—je app crasht niet en gebruikers weten wat er mis ging.

## Step 3 – Run OCR Recognition

Met de engine klaar en de afbeelding geladen, is de volgende logische stap het daadwerkelijk uitvoeren van het herkenningsproces. Dit voldoet aan het secundaire trefwoord **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

De eigenschap `ocrResult.Text` bevat nu een JSON‑string. Als je deze naar de console print, zie je iets als:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Step 4 – How to Extract Text (and Other Fields) from the JSON

Hier komt het hart van de tutorial: **how to parse json** en **how to extract text** uit de OCR‑payload. We gebruiken `Newtonsoft.Json.Linq.JObject` vanwege de flexibiliteit.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Waarom `JObject` gebruiken?** Het laat je veilig door de JSON‑boom navigeren zonder een volledige C#‑modelklasse te definiëren. De null‑conditional (`?.`) operators beschermen je tegen `NullReferenceException` als de OCR‑engine ooit een veld weglaten.

### Handling Edge Cases

* **Ontbrekende velden:** Het patroon `?.Value<T>() ?? default` geeft een verstandige fallback.  
* **Meerdere pagina's:** Loop over `jsonObject["Pages"]` als je meer dan één pagina verwacht.  
* **Niet‑numerieke confidence:** Gebruik `double.TryParse` als het SDK soms een string retourneert.

## Step 5 – Wrap It All Up in a Reusable Method

Om te voorkomen dat je steeds dezelfde boilerplate kopieert, kapsel je de hele flow in een helper‑methode. Dit demonstreert ook **use OCR engine C#** op een schone, herbruikbare manier.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Je kunt nu `RunOcrAndParseJson(@"C:\Images\passport.png");` aanroepen vanuit `Main` of een ander deel van je applicatie.

## Full Working Example

Hieronder staat een compleet, zelf‑voorzienend console‑programma dat je kunt kopiëren‑plakken in een nieuw `.csproj`. Het bevat alle besproken onderdelen, plus een klein beetje foutafhandeling.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Verwachte output** (ervan uitgaande dat de OCR geslaagd is):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Als de afbeelding niet gelezen kan worden, gooit het SDK een uitzondering die we in `Main` opvangen, waardoor een vriendelijke foutmelding wordt getoond in plaats van een crash.

## Frequently Asked Questions (FAQs)

**Q: Wat als de OCR‑engine een array van pagina's retourneert?**  
A: Loop over `json["Pages"]` en concateneer elke `["Text"]`‑waarde, of verwerk ze afzonderlijk afhankelijk van je use case.

**Q: Kan ik de JSON deserialiseren naar een getypeerde C#‑klasse?**  
A: Zeker. Definieer een klassestructuur die overeenkomt met het JSON‑schema en gebruik `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Dit geeft je compile‑time veiligheid, maar vereist dat je het model synchroon houdt met de output van het SDK.

**Q: Werkt dit met async OCR‑API's?**  
A: Ja. Vervang `engine.Recognize()` door `await engine.RecognizeAsync()` en maak `RunOcrAndParseJson` `async Task`. Het JSON‑parsen blijft hetzelfde.

**Q: Hoe sla ik de JSON op in een bestand voor latere analyse?**  
A: Nadat `result.Text` is opgehaald, roep je `File.WriteAllText(@"output.json", result.Text);` aan. Je kunt het later herladen met `JObject.Parse(File.ReadAllText(...))`.

## Next

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}