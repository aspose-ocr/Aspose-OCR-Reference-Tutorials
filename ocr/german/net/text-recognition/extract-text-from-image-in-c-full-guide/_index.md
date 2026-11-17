---
category: general
date: 2026-03-23
description: Extrahieren Sie Text aus einem Bild mit Aspose OCR in C# und lernen Sie,
  wie Sie einen Konsolen‑Logger für Echtzeit‑Feedback hinzufügen.
draft: false
keywords:
- extract text from image
- add console logger
language: de
og_description: Extrahieren Sie Text aus einem Bild mit Aspose OCR und fügen Sie einen
  Konsolen‑Logger hinzu, um den Vorgang zu überwachen. Schritt‑für‑Schritt C#‑Tutorial.
og_title: Text aus Bild in C# extrahieren – Vollständiger Programmierleitfaden
tags:
- OCR
- C#
- logging
title: Text aus Bild in C# extrahieren – Vollständiger Leitfaden
url: /de/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in C# extrahieren – Vollständige Anleitung

Möchten Sie **extract text from image** schnell und zuverlässig? Mit Aspose OCR können Sie das in wenigen Zeilen C# erledigen.  
Wir zeigen Ihnen außerdem, wie Sie **add console logger** hinzufügen können, damit Sie den Fortschritt der OCR‑Engine direkt in Ihrem Terminal verfolgen können.

Stellen Sie sich vor, Sie haben einen gescannten Kassenbon, eine handschriftliche Notiz oder eine PDF‑Seite, die als PNG gespeichert ist. Sie wollen die rohen Zeichen, ohne ein umständliches UI zu öffnen. Dieses Tutorial führt Sie Schritt für Schritt durch eine komplette Copy‑and‑Paste‑Lösung, die heute mit .NET 6+ und der neuesten Aspose OCR‑Bibliothek funktioniert.

Am Ende dieses Leitfadens können Sie:

* Eine Bilddatei laden und OCR ausführen, um **extract text from image**‑Daten zu erhalten.  
* Einen Console Logger in Aspose AI einbinden, sodass Sie sehen, was die Bibliothek im Hintergrund macht.  
* Den integrierten Spell‑Check‑Post‑Processor anwenden, um OCR‑Fehler zu bereinigen.  

> **Prerequisites** – Eine funktionierende .NET‑Entwicklungsumgebung (Visual Studio 2022, VS Code oder Rider), .NET 6 SDK oder neuer und eine Aspose OCR‑Lizenz (oder ein kostenloser Test). Keine weiteren Drittanbieter‑Pakete sind erforderlich.

---

## What You’ll Need

| Item | Why it matters |
|------|----------------|
| **Aspose.OCR** NuGet package | Provides the `OcrEngine` class that actually reads the image. |
| **Aspose.OCR.AI** NuGet package | Gives you the `AsposeAI` post‑processor framework, including spell‑check. |
| **Microsoft.Extensions.Logging** (optional) | Supplies the `ILogger` interface for the **add console logger** step. |
| **An input image** (`input.png`) | The source file from which we’ll **extract text from image**. |

Sie können die Pakete über das Terminal installieren:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Step 1 – Extract Text from Image with Aspose OCR

Der erste Schritt besteht darin, das Bild an die OCR‑Engine zu übergeben. Dieser Block übernimmt die schwere Arbeit und liefert einen Roh‑String zurück, der noch Rechtschreibfehler enthalten kann.

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

**Why this works:** `OcrEngine` abstracts away all the low‑level image preprocessing (binarisation, skew correction, etc.). When `Recognize()` returns `true`, the `Text` property already contains the best‑guess characters.  

> **Tip:** Wenn Ihr Bild groß ist, sollten Sie es auf ≤ 2000 px auf der längsten Seite verkleinern, bevor Sie es an die Engine übergeben. Das beschleunigt die Verarbeitung, ohne die Genauigkeit zu beeinträchtigen.

---

## Step 2 – Add Console Logger for Real‑Time Insight

Jetzt bringen wir das **add console logger**‑Element ein. Logging dient nicht nur der Fehlersuche; es verschafft Ihnen Einblick in Modell‑Downloads, AI‑Processor‑Schritte und alle Warnungen, die die Bibliothek ausgeben könnte.

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

Sie können diesen Logger nun in Aspose AI einbinden:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**What you’ll see:** Wenn das Spell‑Check‑Modell automatisch heruntergeladen wird, gibt die Konsole eine Zeile wie folgt aus:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Das ist der Vorteil von **add console logger** – Sie wissen immer, ob ein Hintergrundvorgang erfolgreich war.

---

## Step 3 – Configure and Register the Spell‑Check Post‑Processor

Aspose AI liefert einen praktischen Spell‑Check‑Post‑Processor, der gängige OCR‑Fehler bereinigt (z. B. “rec0gn1ze” → “recognize”). Wir konfigurieren ihn, geben optional an, wo das Modell gespeichert werden soll, und registrieren ihn anschließend.

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

**Why you might want a custom path:** In CI/CD‑Pipelines möchten Sie Modelle häufig in einem bekannten Verzeichnis cachen, um wiederholte Downloads zu vermeiden. Das Flag `AllowAutoDownload` sorgt dafür, dass das Modell beim ersten Ausführen des Codes heruntergeladen wird.

---

## Step 4 – Run the Post‑Processor on the OCR Result

Mit dem OCR‑Text in der Hand und dem Spell‑Check‑Processor bereit, übergeben wir den Roh‑String an `AsposeAI`. Die Engine führt das Modell aus, und der Processor speichert den korrigierten Text intern.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Nach diesem Aufruf enthält `spellProcessor` eine Sammlung von `RecognitionResult`‑Objekten, jedes mit einer `RecognitionText`‑Eigenschaft, die die bereinigte Version enthält.

---

## Step 5 – Retrieve and Display the Corrected Text

Zum Schluss holen wir den korrigierten String aus dem Processor und geben ihn aus. Das ist der Moment, in dem Sie den Nutzen sowohl von OCR als auch vom **add console logger**‑Workflow wirklich sehen.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Expected output** (assuming the image contains the phrase “Aspose OCR demo” with a few OCR glitches):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Beachten Sie, wie der Logger uns mitteilte, dass das Modell bereit war, und die korrigierte Zeile sauber erscheint.

---

## Step 6 – Clean Up Resources

Sowohl `AsposeAI` als auch `OcrEngine` implementieren `IDisposable`. Durch das Dispose‑Verfahren werden nativer Speicher und Dateihandles freigegeben, was besonders in langlaufenden Diensten wichtig ist.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Full Working Example

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolenprojekt (`dotnet new console`) kopieren‑und‑einfügen können. Ersetzen Sie `"YOUR_DIRECTORY"` durch einen tatsächlichen Ordner auf Ihrem Rechner.

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