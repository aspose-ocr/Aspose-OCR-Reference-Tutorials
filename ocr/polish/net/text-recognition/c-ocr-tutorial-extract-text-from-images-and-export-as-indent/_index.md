---
category: general
date: 2026-05-02
description: samouczek c# ocr, który pokazuje, jak wyodrębnić tekst z obrazu w c#
  i rozpoznać tekst w pliku png, a następnie zapisać wcięty JSON przy użyciu JsonSerializer
  c#. Przewodnik krok po kroku dla programistów.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: pl
og_description: samouczek OCR w C#, który pokazuje, jak wyodrębnić tekst z obrazu
  w C# i rozpoznać tekst w pliku PNG, a następnie zapisać sformatowany JSON przy użyciu
  JsonSerializer w C#. Kompletny, gotowy do uruchomienia przykład.
og_title: samouczek OCR w C# – wyodrębnianie tekstu i eksport jako wcięty JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: samouczek OCR w C# – wyodrębnianie tekstu z obrazów i eksport jako wcięty JSON
url: /pl/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Wyodrębnianie tekstu z obrazów i eksport jako sformatowany JSON

Kiedykolwiek potrzebowałeś **c# ocr tutorial**, który przechodzi od zdjęcia tekstu prosto do ładnie sformatowanego pliku JSON? Nie jesteś sam. W wielu projektach – myśl o skanowaniu faktur, parsowaniu paragonów czy nawet prostym wyciąganiu tekstu z memów – kończysz z plikiem PNG i zastanawiasz się, jak wyciągnąć słowa bez pisania własnego rozpoznawacza.  

Ten przewodnik daje praktyczne rozwiązanie: **wyodrębnimy tekst z obrazu c#** używając Aspose.OCR, **rozpoznamy tekst png**, a następnie **zapiszemy sformatowany json** przy pomocy `JsonSerializer` w C#. Po zakończeniu będziesz mieć samodzielną aplikację konsolową, którą możesz wrzucić do dowolnego rozwiązania .NET. Bez niejasnych odnośników „zobacz dokumentację”, tylko kompletny przykład gotowy do skopiowania i wklejenia.

## What You’ll Need

- **.NET 6** (lub dowolna nowsza wersja .NET). Starsze frameworki działają, ale składnia w przykładzie skierowana jest do .NET 6+.
- **Aspose.OCR for .NET** – zainstaluj przez NuGet: `dotnet add package Aspose.OCR`.
- Przykładowy obraz PNG (`text.png`) zawierający wyraźny, maszynowo czytelny tekst.
- IDE lub edytor według własnego wyboru – Visual Studio, VS Code, Rider itp.

> **Pro tip:** Jeśli planujesz przetwarzać wiele obrazów, rozważ ponowne użycie jednej instancji `OcrEngine` zamiast tworzenia nowej dla każdego pliku. Redukuje to narzut i zwiększa przepustowość.

## Step 1: Set Up a c# ocr tutorial Project

Najpierw utwórz projekt konsolowy. Poniższe polecenia tworzą szkielet i pobierają bibliotekę OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Teraz otwórz wygenerowany plik `Program.cs`. Zastąpimy jego zawartość pełnym przykładem później, ale na razie upewnij się, że projekt się kompiluje:

```bash
dotnet build
```

Jeśli nie pojawiły się żadne błędy, możesz przejść dalej.

## Step 2: Recognize PNG Text from an Image

Serce każdego **c# ocr tutorial** to sam silnik OCR. Aspose.OCR ukrywa szczegóły niskiego poziomu i udostępnia czystą klasę `OcrEngine`. Poniżej tworzymy silnik, wskazujemy plik PNG i prosimy go o rozpoznanie tekstu.

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

### Why This Works

- **`RecognizeImage`** akceptuje wiele formatów (PNG, JPEG, BMP). Specjalnie **recognize png text**, ponieważ PNG zachowuje bezstratne szczegóły, co jest idealne dla OCR.
- Zwrócony `OcrResult` zawiera nie tylko czysty tekst, ale także współczynnik pewności dla każdego glifu, przydatny, jeśli później chcesz odfiltrować znaki o niskiej pewności.

## Step 3: Write Indented JSON with JsonSerializer c#

Mając już `ocrResult`, kolejnym logicznym krokiem w naszym **c# ocr tutorial** jest przekształcenie tego obiektu w czytelny JSON. Wbudowany serializer `System.Text.Json` robi robotę, a my skonfigurujemy go, aby **write indented json** dla przejrzystości.

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

### Using `JsonSerializer` Correctly

- Flaga `WriteIndented` to najprostszy sposób na **write indented json** bez użycia zewnętrznych bibliotek.
- Jeśli kiedykolwiek potrzebujesz nazw właściwości w stylu camelCase, dodaj `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` do opcji.
- Łańcuch `jsonOutput` można zapisać przy pomocy `File.WriteAllText("result.json", jsonOutput);` – przydatna sztuczka w rzeczywistych pipeline’ach.

## Step 4: Run and Verify the Output

Skompiluj i uruchom program:

```bash
dotnet run
```

Zakładając, że `text.png` zawiera frazę *„Hello, OCR World!”*, powinieneś zobaczyć coś w rodzaju:

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

Ten JSON jest **indented**, co ułatwia czytanie w logach lub przekazywanie go do kolejnych usług.

### Edge Cases & Tips

| Situation | What to Do |
|-----------|------------|
| **Image is blurry** | Increase `ocrEngine.Config.Dpi` (e.g., `ocrEngine.Config.Dpi = 300`) before calling `RecognizeImage`. |
| **Non‑English language** | Set `ocrEngine.Config.Language = OcrLanguage.German` (or any supported language). |
| **Large batch of files** | Loop over a directory, reusing the same `OcrEngine` instance; store each JSON result with a unique filename. |
| **Need only high‑confidence text** | Filter `ocrResult.Lines` where `Confidence` ≥ 0.95 before serialization. |

## Full Working Example (Copy‑Paste Ready)

Poniżej znajduje się *cały* program, gotowy do wklejenia do `Program.cs`. Zawiera wszystkie kroki, obsługę błędów i komentarze, które czynią kod samowyjaśniającym się.

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

Uruchom kod, sprawdź konsolę lub wygenerowany plik `.json`, a zobaczysz wyodrębniony tekst wraz z oceną pewności, wszystko ładnie **indented**.

## Conclusion

Masz teraz solidny **c# ocr tutorial**, który pokazuje, jak **extract text image c#**, **recognize png text**, oraz **write indented json** przy użyciu `JsonSerializer`. Przykład jest kompletny, uruchamialny i zawiera praktyczne wskazówki dla rzeczywistych scenariuszy.  

Co dalej? Spróbuj zamienić Aspose.OCR na inny silnik (np. Tesseract) i zobacz, jak zmienia się struktura `OcrResult`, albo podłącz JSON do downstream API, które przechowuje dane OCR w bazie danych. Możesz też poeksperymentować z **use jsonserializer c#** – np. własnymi konwerterami dla formatowania dat lub obsługi enumów.

Happy coding, and may your OCR pipelines be ever accurate!  

---  

![c# ocr tutorial diagram](image.png "Diagram ilustrujący przepływ OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}