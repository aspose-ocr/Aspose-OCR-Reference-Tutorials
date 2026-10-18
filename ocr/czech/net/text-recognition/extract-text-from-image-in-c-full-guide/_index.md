---
category: general
date: 2026-03-23
description: Extrahujte text z obrázku pomocí Aspose OCR v C# a naučte se přidat konzolový
  logger pro zpětnou vazbu v reálném čase.
draft: false
keywords:
- extract text from image
- add console logger
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR a přidejte konzolový logger
  pro sledování procesu. Krok za krokem C# tutoriál.
og_title: Extrahování textu z obrázku v C# – Kompletní programovací průvodce
tags:
- OCR
- C#
- logging
title: Extrahování textu z obrázku v C# – Kompletní průvodce
url: /cs/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku v C# – Kompletní průvodce

Potřebujete **extrahovat text z obrázku** rychle a spolehlivě? S Aspose OCR to můžete udělat během několika řádků C#. Také vám ukážeme, jak **přidat konzolový logger**, abyste mohli sledovat, jak OCR engine tiše oznamuje svůj postup přímo ve vašem terminálu.

Představte si, že máte naskenovaný účtenku, ručně psanou poznámku nebo stránku PDF uloženou jako PNG. Chcete získat surové znaky bez otevírání těžkopádného UI. Tento tutoriál vás provede kompletním řešením, které můžete zkopírovat a vložit, a funguje dnes s .NET 6+ a nejnovější knihovnou Aspose OCR.

Do konce tohoto průvodce budete schopni:

* Načíst soubor s obrázkem a spustit OCR pro **extrahování textu z obrázku**.  
* Připojit konzolový logger k Aspose AI, abyste viděli, co knihovna dělá v pozadí.  
* Použít vestavěný post‑processor pro kontrolu pravopisu k vyčištění chyb OCR.  

> **Předpoklady** – Fungující vývojové prostředí .NET (Visual Studio 2022, VS Code nebo Rider), .NET 6 SDK nebo novější a licence Aspose OCR (nebo bezplatná zkušební verze). Žádné další třetí balíčky nejsou vyžadovány.

---

## Co budete potřebovat

| Položka | Proč je důležité |
|------|----------------|
| **Aspose.OCR** NuGet package | Poskytuje třídu `OcrEngine`, která skutečně čte obrázek. |
| **Aspose.OCR.AI** NuGet package | Poskytuje framework `AsposeAI` post‑processor, včetně kontroly pravopisu. |
| **Microsoft.Extensions.Logging** (optional) | Poskytuje rozhraní `ILogger` pro krok **přidat konzolový logger**. |
| **Vstupní obrázek** (`input.png`) | Zdrojový soubor, ze kterého budeme **extrahovat text z obrázku**. |

Balíčky můžete nainstalovat přes terminál:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Krok 1 – Extrahovat text z obrázku pomocí Aspose OCR

Prvním krokem je předat obrázek OCR engine. Tento blok provádí těžkou práci a vrací surový řetězec, který může stále obsahovat pravopisné chyby.

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

**Proč to funguje:** `OcrEngine` abstrahuje veškeré nízkoúrovňové předzpracování obrazu (binarizaci, korekci sklonu atd.). Když `Recognize()` vrátí `true`, vlastnost `Text` již obsahuje nejlepší odhad znaků.  

> **Tip:** Pokud je váš obrázek velký, zvažte jeho změnu velikosti na ≤ 2000 px na delší straně před předáním engine. Zrychlí to zpracování, aniž by to poškodilo přesnost.

---

## Krok 2 – Přidat konzolový logger pro náhled v reálném čase

Nyní přidáváme část **přidat konzolový logger**. Logování není jen pro ladění; poskytuje vám přehled o stahování modelů, krocích AI‑procesoru a všech varováních, která knihovna může vypsat.

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

Nyní můžete tento logger zapojit do Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Co uvidíte:** Když je model pro kontrolu pravopisu automaticky stažen, konzole vytiskne řádek jako:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

To je výhoda **přidat konzolový logger** – už se nebudete ptát, zda operace na pozadí uspěla.

---

## Krok 3 – Konfigurace a registrace post‑processoru pro kontrolu pravopisu

Aspose AI obsahuje užitečný post‑processor pro kontrolu pravopisu, který odstraňuje běžné chyby OCR (např. „rec0gn1ze“ → „recognize“). Nakonfigurujeme jej, volitelně řekneme knihovně, kde model uložit, a poté jej zaregistrujeme.

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

**Proč byste mohli chtít vlastní cestu:** V CI/CD pipelinech často chcete kešovat modely v známém adresáři, aby se předešlo opakovaným stahováním. Příznak `AllowAutoDownload` zajišťuje, že model bude stažen při prvním spuštění kódu.

---

## Krok 4 – Spustit post‑processor na výsledku OCR

S OCR textem v ruce a připraveným procesorem pro kontrolu pravopisu předáme surový řetězec do `AsposeAI`. Engine spustí model a procesor interně uloží opravený text.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Po tomto volání `spellProcessor` obsahuje kolekci objektů `RecognitionResult`, z nichž každý má vlastnost `RecognitionText` obsahující vyčištěnou verzi.

---

## Krok 5 – Získat a zobrazit opravený text

Nakonec vytáhneme opravený řetězec z procesoru a vytiskneme jej. To je okamžik, kdy skutečně uvidíte výhodu jak OCR, tak workflow **přidat konzolový logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Očekávaný výstup** (předpokládáme, že obrázek obsahuje frázi „Aspose OCR demo“ s několika OCR chybami):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Všimněte si, že logger nám řekl, že model je připraven, a opravená řádka je čitelná.

---

## Krok 6 – Vyčistit zdroje

Jak `AsposeAI`, tak `OcrEngine` implementují `IDisposable`. Uvolněním se uvolní nativní paměť a souborové handle, což je zvláště důležité v dlouho běžících službách.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Kompletní funkční příklad

Níže je celý program, který můžete zkopírovat a vložit do nového konzolového projektu (`dotnet new console`). Nahraďte `"YOUR_DIRECTORY"` skutečnou složkou na vašem počítači.

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