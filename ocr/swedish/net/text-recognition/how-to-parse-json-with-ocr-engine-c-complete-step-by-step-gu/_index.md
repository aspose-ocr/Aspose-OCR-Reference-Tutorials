---
category: general
date: 2026-03-17
description: Lär dig hur du parsar JSON från OCR-resultat i C#. Den här handledningen
  täcker hur du extraherar text, laddar en bild för OCR, kör OCR‑igenkänning och använder
  OCR‑motorn i C# effektivt.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: sv
og_description: Hur man parsar JSON från OCR‑utdata i C#. Följ vår guide för att extrahera
  text, ladda bild för OCR, köra OCR‑igenkänning och använda OCR‑motorn i C#.
og_title: Hur man parsar JSON med OCR‑motorn C# – Fullständig handledning
tags:
- C#
- OCR
- JSON
- Image Processing
title: Hur man parsar JSON med OCR-motorn C# – Komplett steg‑för‑steg‑guide
url: /sv/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man parsar JSON med OCR Engine C# – Komplett steg‑för‑steg guide

Har du någonsin undrat **how to parse json** som kommer direkt från en OCR‑motor? Du är inte ensam. De flesta utvecklare stöter på samma problem—att få rå JSON, och sedan lista ut det bästa sättet att extrahera de användbara delarna som förtroendescore eller själva texten. I den här guiden går vi igenom hur man laddar en bild för OCR, kör OCR‑igenkänning, och slutligen **how to parse json** på ett rent, underhållbart sätt.

Vid slutet av tutorialen kommer du att kunna:

* Ladda en bild för OCR med bara några rader kod.  
* Köra OCR‑igenkänning med en C# OCR‑motor.  
* **How to extract text** och annan metadata från JSON‑payloaden.  
* Hantera vanliga kantfall (saknade fält, oväntade format) utan att krascha.

Ingen extern dokumentation krävs—allt du behöver finns här.

## Förutsättningar

Innan vi dyker ner, se till att du har:

* .NET 6.0 eller senare (koden kompileras även på .NET Framework 4.7+).  
* En referens till OCR‑biblioteket du använder (exemplet använder en hypotetisk `OcrEngine`‑klass).  
* `Newtonsoft.Json` NuGet‑paketet för JSON‑hantering (`Install-Package Newtonsoft.Json`).  
* En bildfil (t.ex. `passport.png`) placerad någonstans där din app kan läsa den.

> **Pro tip:** Om du använder ett kommersiellt OCR‑SDK, kontrollera att JSON‑utdataformatet är aktiverat—de flesta leverantörer exponerar det via en konfigurationsproperty precis som `ocrEngine.Config.OutputFormat`.

## Steg 1 – Skapa och konfigurera OCR‑motorn (Primärt nyckelord i handling)

Det första du behöver göra är att instansiera OCR‑motorn och tala om för den att returnera JSON. Det är här frasen **how to parse json** först dyker upp i vår kod, eftersom motorn kommer att ge oss en JSON‑sträng som vi senare parsar.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Varför detta är viktigt:** Att sätta `OutputFormat` till `Json` säkerställer att svaret innehåller både den igenkända texten **och** användbar metadata som förtroendescore. Om du glömmer detta steg får du vanlig text istället, och **how to parse json** blir en irrelevant fråga.

## Steg 2 – Ladda bild för OCR

Nu laddar vi bilden vi vill analysera. Detta är exakt den plats där det sekundära nyckelordet **load image for OCR** glänser.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Vad händer om filen saknas?** Omslut anropet i ett `try/catch` och visa ett vänligt meddelande—din app kraschar inte och användarna får veta vad som gick fel.

## Steg 3 – Kör OCR‑igenkänning

Med motorn klar och bilden laddad är nästa logiska steg att faktiskt köra igenkänningsprocessen. Detta uppfyller det sekundära nyckelordet **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

`ocrResult.Text`‑egenskapen innehåller nu en JSON‑sträng. Om du skriver ut den i konsolen ser du något i stil med:

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

## Steg 4 – Hur man extraherar text (och andra fält) från JSON

Här är hjärtat i tutorialen: **how to parse json** och **how to extract text** från OCR‑payloaden. Vi använder `Newtonsoft.Json.Linq.JObject` för dess flexibilitet.

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

**Varför använda `JObject`?** Det låter dig säkert navigera i JSON‑trädet utan att definiera en fullständig C#‑modellklass. De null‑villkorliga (`?.`) operatorerna skyddar dig mot `NullReferenceException` om OCR‑motorn någonsin utelämnar ett fält.

### Hantera kantfall

* **Missing fields:** Mönstret `?.Value<T>() ?? default` returnerar ett rimligt reservvärde.  
* **Multiple pages:** Loopa över `jsonObject["Pages"]` om du förväntar dig mer än en sida.  
* **Non‑numeric confidence:** Använd `double.TryParse` om SDK ibland returnerar en sträng.

## Steg 5 – Packa ihop allt i en återanvändbar metod

För att undvika att kopiera samma boilerplate, kapsla in hela flödet i en hjälpfunktion. Detta demonstrerar också **use OCR engine C#** på ett rent, återanvändbart sätt.

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

Du kan nu anropa `RunOcrAndParseJson(@"C:\Images\passport.png");` från `Main` eller någon annan del av din applikation.

## Fullt fungerande exempel

Nedan är ett komplett, självständigt konsolprogram du kan kopiera‑klistra in i ett nytt `.csproj`. Det inkluderar alla delar vi diskuterat, plus en liten mängd felhantering.

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

**Förväntad utdata** (förutsatt att OCR lyckades):

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

Om bilden inte kan läsas, kommer SDK att kasta ett undantag som vi fångar i `Main`, och skriver ut ett vänligt felmeddelande istället för att krascha.

## Vanliga frågor (FAQ)

**Q: What if the OCR engine returns an array of pages?**  
A: Loopa över `json["Pages"]` och konkatenera varje `["Text"]`‑värde, eller behandla dem individuellt beroende på ditt användningsfall.

**Q: Can I deserialize the JSON into a typed C# class?**  
A: Absolut. Definiera en klassstruktur som matchar JSON‑schemat och använd `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Detta ger dig kompileringstidssäkerhet men kräver att du håller modellen i synk med SDK:ns utdata.

**Q: Does this work with async OCR APIs?**  
A: Ja. Byt ut `engine.Recognize()` mot `await engine.RecognizeAsync()` och gör `RunOcrAndParseJson` till `async Task`. JSON‑parsningen förblir densamma.

**Q: How do I save the JSON to a file for later analysis?**  
A: Efter att `result.Text` har hämtats, anropa `File.WriteAllText(@"output.json", result.Text);`. Du kan sedan läsa in den igen med `JObject.Parse(File.ReadAllText(...))`.

## Nästa

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}