---
category: general
date: 2026-01-12
description: samouczek OCR w C#, który pokazuje, jak rozpoznawać tekst na obrazie,
  wyodrębniać tekst z obrazu w C# oraz generować plik OCR z obrazu do PDF z ocenami
  pewności.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: pl
og_description: Poznaj kompletny samouczek OCR w C#, aby rozpoznawać obrazy tekstu,
  wyodrębniać tekst z obrazu w C# oraz tworzyć dokument OCR z obrazu do PDF z ocenami
  pewności.
og_title: c# OCR tutorial – Konwertuj obrazy na przeszukiwalne PDFy
tags:
- OCR
- C#
- PDF
title: samouczek OCR w C# – zamień obrazy w przeszukiwalne pliki PDF
url: /pl/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Zamień obrazy w przeszukiwalne PDFy

Zastanawiałeś się kiedyś, jak **rozpoznawać obrazy z tekstem** w projekcie C# bez poszukiwania usług firm trzecich? Nie jesteś sam. W wielu rzeczywistych aplikacjach — pomyśl o skanerach faktur, monitorowaniu paragonów czy wielojęzycznych archiwach dokumentów — programiści potrzebują niezawodnego, lokalnego silnika OCR, który dodatkowo zwraca wyniki z oceną pewności.  

Ten **c# ocr tutorial** przeprowadzi Cię przez wszystko, czego potrzebujesz: od wczytania obrazu, wyboru modeli językowych, przełączania przyspieszenia GPU, po zapisanie wyniku jako przeszukiwalny PDF. Po zakończeniu będziesz mieć gotowy do uruchomienia przykład kodu, który wyodrębnia tekst, raportuje pewność OCR i opcjonalnie tworzy plik *image to pdf ocr* — wszystko w mniej niż minutę kodowania.

## Co zbudujesz

- Wczytaj obraz wielojęzyczny (`sample_multi_lang.jpg` jest używany jako placeholder).  
- Wybierz modele językowe arabskiego, hindi i rosyjskiego (można dodać więcej).  
- Włącz przetwarzanie GPU, jeśli Twój komputer je obsługuje.  
- Uzyskaj surowy wynik OCR **z ocenami pewności**.  
- Serializuj wynik do ładnie sformatowanego JSON **lub** zapisz przeszukiwalny PDF.  

Bez zewnętrznych usług webowych, bez ukrytej magii — tylko Aspose.OCR dla .NET, kilka linii C# i jasne wyjaśnienie **dlaczego** każda linia ma znaczenie.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod kompiluje się na .NET Core i .NET Framework).  
- Visual Studio 2022 (lub dowolne IDE, które lubisz).  
- Licencja Aspose.OCR dla .NET (bezpłatna wersja próbna działa do testów).  
- Opcjonalnie: GPU kompatybilne z CUDA, jeśli chcesz przyspieszyć rozpoznawanie.

> **Pro tip:** Jeśli nie masz GPU, po prostu ustaw `UseGpu = false`, a silnik przełączy się na CPU bez żadnych zmian w kodzie.

## Krok 1: Zainstaluj wymagane pakiety NuGet

Otwórz **Package Manager Console** i uruchom:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Te trzy pakiety dostarczają silnik OCR, przyspieszenie GPU oraz wygodny serializer JSON dla wyników pewności.

## Krok 2: Skonfiguruj strukturę projektu

Utwórz nowy projekt konsolowy (`dotnet new console -n AsposeOcrDemo`) i zamień wygenerowany plik `Program.cs` na kod poniżej.  
Cała logika znajduje się w klasie `Program`; jedynym dodatkiem jest mała metoda rozszerzająca, która formatuje wynik OCR do JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Dlaczego ten kod działa

1. **Przełącznik GPU** – `GpuOcrEngine` wykorzystuje rdzenie CUDA; operator warunkowy umożliwia łatwe przełączanie.  
2. **Automatyczne pobieranie języków** – `AutoDownloadResources = true` zapewnia, że modele arabskiego, hindi i rosyjskiego zostaną pobrane przy pierwszym uruchomieniu aplikacji.  
3. **Oceny pewności** – `result.Words` zawiera `Confidence` dla każdego rozpoznanego słowa; metoda rozszerzająca formatuje je do czystego obiektu JSON.  
4. **Przeszukiwalny PDF** – `result.Pdf` jest już w pełni przeszukiwalnym PDF, więc po prostu zapisujemy tablicę bajtów na dysk. Nie potrzebne są dodatkowe biblioteki.

## Krok 6: Uruchom przykład

Otwórz terminal, przejdź do folderu projektu i wykonaj:

```bash
dotnet run
```

Jeśli wybrałeś wyjście **JSON**, zobaczysz coś podobnego:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Jeśli przełączyłeś się na **PDF**, konsola wypisze ścieżkę i znajdziesz przeszukiwalny PDF tuż obok obrazu źródłowego.

## Częste pytania i przypadki brzegowe

- **Co jeśli model językowy nie jest dostępny?**  
  Silnik OCR rzuca wyraźny `ResourceNotFoundException`. Ponieważ ustawiliśmy `AutoDownloadResources = true`, brakujący model jest pobierany automatycznie przy pierwszym uruchomieniu, więc wyjątek rzadko pojawia się w środowisku produkcyjnym.

- **Czy mogę przetwarzać wsadowo obrazy?**  
  Oczywiście. Owiń wywołanie `engine.Recognize` w pętlę `foreach` po katalogu z plikami. Ta sama klasa `OcrResultExtensions` działa dla każdego obrazu.

- **Czy potrzebna jest licencja na GPU?**  
  Nie. Bezpłatna wersja próbna działa zarówno na CPU, jak i GPU. Pełna licencja usuwa znak wodny wersji próbnej i znosi ograniczenia liczby stron.

- **Jak dokładne są oceny pewności?**  
  Oceny wahają się od 0.0 (brak pewności) do 1.0 (pewność idealna). W praktyce wszystko powyżej 0.90 jest wiarygodne dla dalszego przetwarzania; możesz odfiltrować słowa o niższej pewności, jeśli potrzebujesz bardziej rygorystycznej weryfikacji.

## Krok 7: Kolejne kroki (rozbuduj swój zestaw OCR)

1. **Dodaj więcej języków** – po prostu dodaj `LanguageModel.French` (lub dowolny obsługiwany model) do tablicy `Languages`.  
2. **Połącz OCR z konwersją PDF/A** – Aspose.PDF może osadzić warstwę OCR w dokumencie zgodnym z PDF/A‑2b do archiwizacji.  
3. **Zintegruj z Azure Functions** – opakuj logikę w endpoint bezserwerowy, aby przetwarzać przesyłane pliki w locie.  
4. **Dostosuj progi pewności** – użyj `result.Words.Where(w => w.Confidence < 0.85)`, aby oznaczyć niepewne słowa do ręcznej weryfikacji.

---

### TL;DR

Ten **c# ocr tutorial** pokazuje, jak:

- Wczytać obraz i wybrać wiele modeli językowych.  
- Włączyć przyspieszenie GPU przy użyciu jednego flagi boolowskiej.  
- Pobrać wyniki OCR **z ocenami pewności** i serializować je do JSON.  
- Opcjonalnie zapisać przeszukiwalny PDF (**image to pdf ocr**).  

Wszystko to jest osiągalne przy użyciu kilku linii kodu, darmowej wersji próbnej Aspose.OCR i powyższego przykładu. Wypróbuj, zmodyfikuj listę języków i w kilka minut będziesz mieć gotowy do produkcji potok OCR.

---

![przykładowy obrazek c# ocr tutorial](https://example.com/placeholder-image.jpg "przykładowy obrazek c# ocr tutorial")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}