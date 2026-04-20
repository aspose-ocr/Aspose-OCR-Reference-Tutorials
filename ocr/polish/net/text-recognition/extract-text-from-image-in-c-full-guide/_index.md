---
category: general
date: 2026-03-23
description: Wyodrębnij tekst z obrazu przy użyciu Aspose OCR w C# i dowiedz się,
  jak dodać loggera konsoli dla informacji zwrotnych w czasie rzeczywistym.
draft: false
keywords:
- extract text from image
- add console logger
language: pl
og_description: Wyodrębnij tekst z obrazu przy użyciu Aspose OCR i dodaj logger konsoli,
  aby monitorować proces. Krok po kroku tutorial C#.
og_title: Wyodrębnianie tekstu z obrazu w C# – Kompletny przewodnik programistyczny
tags:
- OCR
- C#
- logging
title: Wyodrębnianie tekstu z obrazu w C# – pełny przewodnik
url: /pl/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnij tekst z obrazu w C# – Pełny przewodnik

Potrzebujesz **wyodrębnić tekst z obrazu** szybko i niezawodnie? Z Aspose OCR możesz zrobić to w kilku linijkach C#.  
Pokażemy także, jak **dodać logger konsoli**, abyś mógł obserwować, jak silnik OCR szepcze o postępie bezpośrednio w terminalu.

Wyobraź sobie, że masz zeskanowany paragon, odręczną notatkę lub stronę PDF zapisaną jako PNG. Chcesz uzyskać surowe znaki bez otwierania ciężkiego interfejsu UI. Ten tutorial przeprowadzi Cię przez kompletną, gotową do skopiowania i wklejenia rozwiązanie, które działa już dziś z .NET 6+ i najnowszą biblioteką Aspose OCR.

Po zakończeniu tego przewodnika będziesz w stanie:

* Załadować plik obrazu i uruchomić OCR, aby **wyodrębnić tekst z obrazu**.  
* Podłączyć logger konsoli do Aspose AI, aby zobaczyć, co biblioteka robi w tle.  
* Zastosować wbudowany post‑processor sprawdzania pisowni, aby oczyścić błędy OCR.  

> **Wymagania wstępne** – Działające środowisko programistyczne .NET (Visual Studio 2022, VS Code lub Rider), .NET 6 SDK lub nowszy oraz licencja Aspose OCR (lub darmowa wersja próbna). Nie są potrzebne żadne inne pakiety zewnętrzne.

---

## Czego będziesz potrzebować

| Element | Dlaczego jest ważny |
|------|----------------|
| **Aspose.OCR** pakiet NuGet | Dostarcza klasę `OcrEngine`, która faktycznie odczytuje obraz. |
| **Aspose.OCR.AI** pakiet NuGet | Udostępnia framework post‑processor `AsposeAI`, w tym sprawdzanie pisowni. |
| **Microsoft.Extensions.Logging** (opcjonalnie) | Dostarcza interfejs `ILogger` potrzebny w kroku **dodaj logger konsoli**. |
| **Obraz wejściowy** (`input.png`) | Plik źródłowy, z którego **wyodrębnimy tekst z obrazu**. |

Pakiety możesz zainstalować w terminalu:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Krok 1 – Wyodrębnij tekst z obrazu przy użyciu Aspose OCR

Pierwszą rzeczą, którą robimy, jest przekazanie obrazu do silnika OCR. Ten blok wykonuje ciężką pracę i zwraca surowy ciąg znaków, który może nadal zawierać literówki.

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

**Dlaczego to działa:** `OcrEngine` ukrywa wszystkie niskopoziomowe operacje wstępnego przetwarzania obrazu (binaryzacja, korekcja pochylenia itp.). Gdy `Recognize()` zwróci `true`, właściwość `Text` już zawiera najlepiej odgadnięte znaki.  

> **Wskazówka:** Jeśli Twój obraz jest duży, rozważ zmniejszenie go do ≤ 2000 px po najdłuższym boku przed przekazaniem do silnika. Przyspieszy to przetwarzanie bez utraty dokładności.

---

## Krok 2 – Dodaj logger konsoli dla podglądu w czasie rzeczywistym

Teraz wprowadzamy element **dodaj logger konsoli**. Logowanie nie służy wyłącznie do debugowania; daje wgląd w pobieranie modeli, kroki procesora AI oraz wszelkie ostrzeżenia generowane przez bibliotekę.

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

Teraz możesz podłączyć ten logger do Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Co zobaczysz:** Gdy model sprawdzania pisowni zostanie automatycznie pobrany, konsola wypisze linię podobną do:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

To właśnie zaleta **dodaj logger konsoli** – nigdy nie będziesz się zastanawiać, czy operacja w tle się powiodła.

---

## Krok 3 – Skonfiguruj i zarejestruj post‑processor sprawdzania pisowni

Aspose AI dostarcza przydatny post‑processor sprawdzania pisowni, który usuwa typowe błędy OCR (np. „rec0gn1ze” → „recognize”). Skonfigurujemy go, opcjonalnie podamy bibliotece miejsce do przechowywania modelu, a następnie zarejestrujemy.

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

**Dlaczego możesz chcieć własną ścieżkę:** W pipeline’ach CI/CD często chce się buforować modele w znanym katalogu, aby uniknąć wielokrotnych pobrań. Flaga `AllowAutoDownload` zapewnia, że model zostanie pobrany przy pierwszym uruchomieniu kodu.

---

## Krok 4 – Uruchom post‑processor na wyniku OCR

Mając już tekst OCR i gotowy procesor sprawdzania pisowni, przekazujemy surowy ciąg do `AsposeAI`. Silnik uruchamia model, a procesor wewnętrznie przechowuje poprawiony tekst.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Po tym wywołaniu `spellProcessor` zawiera kolekcję obiektów `RecognitionResult`, z których każdy ma właściwość `RecognitionText` zawierającą wyczyszczoną wersję.

---

## Krok 5 – Pobierz i wyświetl poprawiony tekst

Na koniec wyciągamy poprawiony ciąg z procesora i wypisujemy go. To moment, w którym naprawdę widać korzyść płynącą zarówno z OCR, jak i z workflow **dodaj logger konsoli**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Oczekiwany wynik** (zakładając, że obraz zawiera frazę „Aspose OCR demo” z kilkoma błędami OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Zauważ, że logger poinformował nas, że model jest gotowy, a poprawiona linia jest czysta.

---

## Krok 6 – Posprzątaj zasoby

Zarówno `AsposeAI`, jak i `OcrEngine` implementują `IDisposable`. Ich zwolnienie zwalnia pamięć natywną i uchwyty plików, co jest szczególnie ważne w długotrwale działających usługach.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Pełny działający przykład

Poniżej znajduje się cały program, który możesz skopiować‑wkleić do nowego projektu konsolowego (`dotnet new console`). Zamień `"YOUR_DIRECTORY"` na rzeczywistą ścieżkę na swoim komputerze.

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