---
category: general
date: 2026-04-08
description: Leer hoe je OCR op een afbeelding uitvoert en een JSON‑bestand schrijft
  in C# met Aspose OCR. Deze Aspose OCR C#‑tutorial toont de conversie van OCR‑afbeelding
  naar JSON met vertrouwenswaarden.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: nl
og_description: Voer OCR uit op een afbeelding en exporteer de resultaten naar een
  JSON‑bestand in C#. Deze tutorial behandelt de volledige Aspose OCR C#‑workflow,
  inclusief vertrouwensscores.
og_title: OCR uitvoeren op afbeelding naar JSON in C# – Aspose OCR-gids
tags:
- Aspose
- OCR
- C#
- JSON
title: Voer OCR uit op afbeelding naar JSON in C# met Aspose
url: /nl/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding naar JSON in C# met Aspose

Heb je ooit **OCR op afbeelding** moeten uitvoeren maar wist je niet hoe je de resultaten in een gestructureerd formaat kon krijgen? Je bent niet de enige—ontwikkelaars vragen voortdurend: “Hoe zet ik een gescande foto om in bruikbare gegevens?” Het goede nieuws is dat Aspose.OCR dit een eitje maakt, en je zelfs **JSON‑bestand schrijven C#**‑stijl kunt doen met meegeleverde confidence‑scores.

In deze gids lopen we een volledige **aspose OCR C# tutorial** door die alles behandelt, van het laden van een afbeelding tot het exporteren van de herkende tekst als JSON. Aan het einde heb je een uitvoerbare console‑app die **OCR op afbeelding** uitvoert, de output naar JSON converteert (inclusief confidence‑waarden) en deze met één regel code opslaat. Geen verborgen stappen, geen externe scripts—gewoon pure C#.

## Vereisten

- .NET 6.0 SDK of later (de code werkt ook met .NET Core en .NET Framework)
- Visual Studio 2022 (of elke editor die je prettig vindt)
- Een geldige **Aspose.OCR for .NET**‑licentie of een gratis tijdelijke licentie (de gratis trial werkt voor testen)
- Een afbeeldingsbestand (`input.png`) dat je wilt verwerken (elke gangbare indeling—PNG, JPG, BMP—doet het)

Dat is alles. Als je iets mist, haal het dan nu; de rest van de tutorial gaat ervan uit dat alles al aanwezig is.

## Stap 1: Installeer het Aspose.OCR NuGet‑pakket

Allereerst—voeg de bibliotheek toe aan je project. Open een terminal in de projectmap en voer uit:

```bash
dotnet add package Aspose.OCR
```

Dit haalt de nieuwste versie op (vanaf april 2026 is dat 23.12) en voegt de benodigde DLL’s toe aan de `bin`‑map. Geen extra configuratie nodig.

## Stap 2: Initialiseer de OCR‑engine (OCR op afbeelding uitvoeren)

Nu maken we een `OcrEngine`‑instantie aan en geven we aan welke taal gebruikt moet worden. Engels (`"en"`) is het meest gebruikelijk, maar je kunt het vervangen door `"fr"`, `"de"` of een andere ondersteunde taal.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Waarom we hier initialiseren:** De `OcrEngine` bevat alle configuratie die nodig is voor het herkenningsproces. Het vooraf instellen van de taal zorgt ervoor dat de engine de juiste tekenset gebruikt, wat de nauwkeurigheid aanzienlijk verbetert.

## Stap 3: Herken de afbeelding en leg confidence vast

Met de engine klaar, voeren we het afbeeldingsbestand in. De methode `RecognizeImage` retourneert een `OcrResult`‑object dat zowel de geëxtraheerde tekst als een confidence‑score voor elk woord bevat.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Wat er onder de motorkap gebeurt:** Aspose draait een op neurale netwerken gebaseerde recognizer die elk pixelblok analyseert, vergelijkt met het taalmodel en een confidence‑waarde (0‑100) toevoegt die aangeeft hoe zeker het over elk woord is.

## Stap 4: Converteer het resultaat naar JSON (OCR afbeelding naar JSON)

Aspose maakt de conversie moeiteloos. Door `includeConfidence: true` mee te geven, krijgen we een JSON‑payload die er als volgt uitziet:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Hier is de code die de JSON‑string genereert:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Waarom confidence opnemen?** Als je de data wilt doorsturen naar downstream‑processen (bijv. validatie, UI‑highlighting), laat het weten welke woorden onzeker zijn, zodat je kunt bepalen of je de gebruiker om bevestiging vraagt.

## Stap 5: Schrijf het JSON‑bestand in C#‑stijl

Nu schrijven we daadwerkelijk **JSON‑bestand C#**. De methode `File.WriteAllText` is atomair en werkt platform‑onafhankelijk, waardoor hij perfect is voor console‑apps.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Dat is de volledige workflow—vijf beknopte stappen die **OCR op afbeelding** uitvoeren, de output naar JSON transformeren en deze vervolgens opslaan.

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je kunt kopiëren‑plakken in `Program.cs`. Zorg dat `input.png` zich in dezelfde map bevindt als het gecompileerde binaire bestand of pas de paden aan.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Verwachte uitvoer

Wanneer je het programma draait (`dotnet run`), zie je iets als:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

En `output.json` zal de gestructureerde JSON bevatten die eerder werd getoond, compleet met confidence‑percentages voor elk woord.

## Pro‑tips & randgevallen

- **Missing file handling:** Plaats de `RecognizeImage`‑aanroep in een `try/catch` voor `FileNotFoundException` als je dynamische paden verwacht.
- **Different languages:** Stel `ocrEngine.Language = "fr"` in voor Frans, of laad een aangepast taalpakket via `ocrEngine.LoadLanguage("custom.lang")`.
- **Large documents:** Voor multi‑page PDF’s, converteer elke pagina eerst naar een afbeelding (bijv. met `Aspose.PDF`) en loop door de OCR‑stappen.
- **Performance tuning:** Als je alleen snelle resultaten nodig hebt, schakel over naar `RecognitionMode.Fast`—je verliest een beetje nauwkeurigheid maar wint snelheid.
- **JSON formatting:** Wil je mooi opgemaakte JSON? Gebruik `JsonConvert.SerializeObject` van Newtonsoft met `Formatting.Indented` na het deserialiseren van de Aspose‑JSON‑string.

## Veelgestelde vragen

**Q: Werkt dit met .NET Framework?**  
A: Absoluut. Hetzelfde NuGet‑pakket richt zich op .NET Standard 2.0, dus je kunt het refereren vanuit .NET Framework 4.6.1 en nieuwer.

**Q: Wat als ik de confidence voor het hele document nodig heb, niet per woord?**  
A: Het `OcrResult` biedt ook `OverallConfidence`. Je kunt dit handmatig aan de JSON toevoegen:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: Kan ik de JSON direct streamen naar een web‑API?**  
A: Ja. Vervang `File.WriteAllText` door een `HttpClient`‑POST die `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}