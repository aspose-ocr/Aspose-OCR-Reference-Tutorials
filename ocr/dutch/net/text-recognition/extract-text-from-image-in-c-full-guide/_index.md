---
category: general
date: 2026-03-23
description: Haal tekst uit een afbeelding met Aspose OCR in C# en leer hoe je een
  consolelogger toevoegt voor realtime feedback.
draft: false
keywords:
- extract text from image
- add console logger
language: nl
og_description: Tekst uit afbeelding extraheren met Aspose OCR en een consolelogger
  toevoegen om het proces te monitoren. Stapsgewijze C#‑tutorial.
og_title: Tekst uit afbeelding extraheren in C# – Complete programmeergids
tags:
- OCR
- C#
- logging
title: Tekst uit afbeelding extraheren in C# – Volledige gids
url: /nl/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren in C# – Volledige gids

Wilt u snel en betrouwbaar **extract text from image**? Met Aspose OCR kunt u dat precies doen in een paar regels C#.  
We laten u ook zien hoe u **add console logger** kunt toevoegen zodat u de voortgang van de OCR-engine rechtstreeks in uw terminal kunt volgen.

Stel je voor dat je een gescande bon, een handgeschreven notitie, of een PDF-pagina opgeslagen als PNG hebt. Je wilt de ruwe tekens zonder een omvangrijke UI te openen. Deze tutorial leidt je door een complete copy‑and‑paste‑oplossing die vandaag werkt met .NET 6+ en de nieuwste Aspose OCR‑bibliotheek.

By the end of this guide you’ll be able to:

* Laad een afbeeldingsbestand en voer OCR uit om **extract text from image** gegevens te verkrijgen.  
* Koppel een console logger aan Aspose AI zodat je ziet wat de bibliotheek op de achtergrond doet.  
* Pas de ingebouwde spell‑check post‑processor toe om OCR‑fouten op te schonen.  

> **Prerequisites** – Een werkende .NET‑ontwikkelomgeving (Visual Studio 2022, VS Code of Rider), .NET 6 SDK of nieuwer, en een Aspose OCR‑licentie (of een gratis proefversie). Er zijn geen andere third‑party pakketten vereist.

## Wat je nodig hebt

| Item | Waarom het belangrijk is |
|------|--------------------------|
| **Aspose.OCR** NuGet package | Biedt de `OcrEngine`‑klasse die de afbeelding daadwerkelijk leest. |
| **Aspose.OCR.AI** NuGet package | Geeft je het `AsposeAI` post‑processor‑framework, inclusief spell‑check. |
| **Microsoft.Extensions.Logging** (optional) | Levert de `ILogger`‑interface voor de **add console logger** stap. |
| **An input image** (`input.png`) | Het bronbestand waaruit we **extract text from image** zullen halen. |

Je kunt de pakketten installeren via de terminal:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

## Stap 1 – Tekst uit afbeelding extraheren met Aspose OCR

Het eerste wat we doen, is de afbeelding aan de OCR-engine geven. Dit blok doet het zware werk en retourneert een ruwe string die nog spelfouten kan bevatten.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Waarom dit werkt:** `OcrEngine` abstracts away all the low‑level image preprocessing (binarisation, skew correction, etc.). When `Recognize()` returns `true`, the `Text` property already contains the best‑guess characters.  

> **Tip:** Als je afbeelding groot is, overweeg dan om deze te verkleinen tot ≤ 2000 px aan de langste zijde voordat je hem aan de engine geeft. Dit versnelt de verwerking zonder de nauwkeurigheid te schaden.

## Stap 2 – Console logger toevoegen voor realtime inzicht

Nu voegen we het **add console logger** onderdeel toe. Loggen is niet alleen voor debugging; het geeft je inzicht in model‑downloads, AI‑processor‑stappen en eventuele waarschuwingen die de bibliotheek kan geven.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Je kunt deze logger nu aansluiten op Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Wat je zult zien:** Wanneer het spell‑check model automatisch wordt gedownload, zal de console een regel afdrukken zoals:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Dat is het voordeel van **add console logger** – je vraagt je nooit af of een achtergrondoperatie geslaagd is.

## Stap 3 – Configureren en registreren van de Spell‑Check post‑processor

Aspose AI wordt geleverd met een handige spell‑check post‑processor die veelvoorkomende OCR‑fouten opruimt (bijv. “rec0gn1ze” → “recognize”). We zullen deze configureren, optioneel de bibliotheek vertellen waar het model moet worden opgeslagen, en vervolgens registreren.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Waarom je een aangepast pad wilt:** In CI/CD‑pipelines wil je vaak modellen cachen in een bekende map om herhaalde downloads te vermijden. De `AllowAutoDownload`‑vlag zorgt ervoor dat het model de eerste keer dat je de code uitvoert, wordt opgehaald.

## Stap 4 – Voer de post‑processor uit op het OCR‑resultaat

Met de OCR‑tekst in de hand en de spell‑check processor klaar, geven we de ruwe string door aan `AsposeAI`. De engine voert het model uit, en de processor slaat de gecorrigeerde tekst intern op.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Na deze aanroep bevat `spellProcessor` een collectie van `RecognitionResult`‑objecten, elk met een `RecognitionText`‑eigenschap die de opgeschoonde versie bevat.

## Stap 5 – Haal de gecorrigeerde tekst op en toon deze

Tot slot halen we de gecorrigeerde string uit de processor en printen deze. Dit is het moment waarop je echt het voordeel van zowel OCR als de **add console logger** workflow ziet.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Verwachte output** (ervan uitgaande dat de afbeelding de zin “Aspose OCR demo” bevat met een paar OCR‑fouten):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Merk op hoe de logger ons vertelde dat het model klaar was, en de gecorrigeerde regel netjes wordt weergegeven.

## Stap 6 – Resources opruimen

Zowel `AsposeAI` als de `OcrEngine` implementeren `IDisposable`. Het vrijgeven ervan maakt native geheugen en bestands‑handles vrij, wat vooral belangrijk is in langdurige services.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt copy‑pasten in een nieuw console‑project (`dotnet new console`). Vervang `"YOUR_DIRECTORY"` door een echte map op je computer.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}