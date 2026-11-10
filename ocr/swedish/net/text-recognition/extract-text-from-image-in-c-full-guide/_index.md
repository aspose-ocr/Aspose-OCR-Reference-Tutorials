---
category: general
date: 2026-03-23
description: Extrahera text från bild med Aspose OCR i C# och lär dig hur du lägger
  till en konsolloggare för realtidsfeedback.
draft: false
keywords:
- extract text from image
- add console logger
language: sv
og_description: Extrahera text från bild med Aspose OCR och lägg till en konsolloggare
  för att övervaka processen. Steg‑för‑steg C#‑handledning.
og_title: Extrahera text från bild i C# – Komplett programmeringsguide
tags:
- OCR
- C#
- logging
title: Extrahera text från bild i C# – Fullständig guide
url: /sv/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i C# – Fullständig guide

Behöver du **extrahera text från bild** snabbt och pålitligt? Med Aspose OCR kan du göra exakt det på några rader C#.  
Vi visar också hur du **lägger till en konsolloggare** så att du kan se OCR‑motorn viska sin framsteg direkt i din terminal.

Föreställ dig att du har ett skannat kvitto, en handskriven anteckning eller en PDF‑sida sparad som PNG. Du vill ha de råa tecknen utan att öppna ett tungt UI. Denna handledning guidar dig genom en komplett, kopiera‑och‑klistra‑lösning som fungerar idag med .NET 6+ och det senaste Aspose OCR‑biblioteket.

I slutet av den här guiden kommer du att kunna:

* Ladda en bildfil och kör OCR för att **extrahera text från bild**‑data.  
* Anslut en konsolloggare till Aspose AI så att du ser vad biblioteket gör bakom kulisserna.  
* Använd den inbyggda stavningskontroll‑postprocessorn för att rensa upp OCR‑fel.  

> **Förutsättningar** – En fungerande .NET‑utvecklingsmiljö (Visual Studio 2022, VS Code eller Rider), .NET 6 SDK eller nyare, och en Aspose OCR‑licens (eller en gratis provversion). Inga andra tredjepartspaket krävs.

---

## Vad du behöver

| Objekt | Varför det är viktigt |
|--------|-----------------------|
| **Aspose.OCR** NuGet package | Tillhandahåller `OcrEngine`‑klassen som faktiskt läser bilden. |
| **Aspose.OCR.AI** NuGet package | Ger dig `AsposeAI`‑postprocess‑ramverket, inklusive stavningskontroll. |
| **Microsoft.Extensions.Logging** (optional) | Tillhandahåller `ILogger`‑gränssnittet för steget **lägg till konsolloggare**. |
| **An input image** (`input.png`) | Källfilen som vi kommer att **extrahera text från bild** från. |

Du kan installera paketen via terminalen:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Steg 1 – Extrahera text från bild med Aspose OCR

Det första vi gör är att ge bilden till OCR‑motorn. Detta block utför det tunga arbetet och returnerar en rå sträng som fortfarande kan innehålla stavfel.

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

**Varför detta fungerar:** `OcrEngine` abstraherar bort all låg‑nivå bildförbehandling (binarisering, skevkorrektion osv.). När `Recognize()` returnerar `true` innehåller `Text`‑egenskapen redan de bästa gissade tecknen.  

> **Tips:** Om din bild är stor, överväg att ändra storlek till ≤ 2000 px på den längsta sidan innan du matar den till motorn. Det snabbar upp bearbetningen utan att försämra noggrannheten.

---

## Steg 2 – Lägg till konsolloggare för realtidsinsikt

Nu introducerar vi delen **lägg till konsolloggare**. Loggning är inte bara för felsökning; den ger dig insyn i modellnedladdningar, AI‑processorsteg och eventuella varningar som biblioteket kan ge.

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

Du kan nu ansluta denna logger till Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Vad du kommer att se:** När stavningskontrollmodellen automatiskt laddas ner, skriver konsolen ut en rad som:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Det är fördelen med **lägg till konsolloggare** – du undrar aldrig om en bakgrundsoperation lyckades.

---

## Steg 3 – Konfigurera och registrera stavningskontroll‑postprocessorn

Aspose AI levereras med en praktisk stavningskontroll‑postprocessor som rensar upp vanliga OCR‑fel (t.ex. “rec0gn1ze” → “recognize”). Vi kommer att konfigurera den, eventuellt ange för biblioteket var modellen ska lagras, och sedan registrera den.

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

**Varför du kanske vill ha en anpassad sökväg:** I CI/CD‑pipelines vill du ofta cache‑lagra modeller i en känd katalog för att undvika upprepade nedladdningar. `AllowAutoDownload`‑flaggan säkerställer att modellen hämtas första gången du kör koden.

---

## Steg 4 – Kör postprocessorn på OCR‑resultatet

Med OCR‑texten i handen och stavningskontrollprocessorn klar, ger vi den råa strängen till `AsposeAI`. Motorn kör modellen och processorn lagrar den korrigerade texten internt.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Efter detta anrop innehåller `spellProcessor` en samling av `RecognitionResult`‑objekt, var och en med en `RecognitionText`‑egenskap som innehåller den rensade versionen.

---

## Steg 5 – Hämta och visa den korrigerade texten

Till sist drar vi den korrigerade strängen ur processorn och skriver ut den. Detta är ögonblicket då du verkligen ser fördelen med både OCR och arbetsflödet **lägg till konsolloggare**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Förväntad output** (förutsatt att bilden innehåller frasen “Aspose OCR demo” med några OCR‑fel):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Observera hur loggern meddelade att modellen var klar, och den korrigerade raden läses tydligt.

---

## Steg 6 – Rensa upp resurser

Både `AsposeAI` och `OcrEngine` implementerar `IDisposable`. Att disponera dem frigör native minne och filhandtag, vilket är särskilt viktigt i långvariga tjänster.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Fullständigt fungerande exempel

Nedan är hela programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt (`dotnet new console`). Ersätt `"YOUR_DIRECTORY"` med en faktisk mapp på din maskin.

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