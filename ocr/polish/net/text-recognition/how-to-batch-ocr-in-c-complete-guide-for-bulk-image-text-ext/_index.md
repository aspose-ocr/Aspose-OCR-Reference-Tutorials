---
category: general
date: 2026-04-04
description: Jak wykonywać OCR wsadowo przy użyciu Aspose.OCR w C#. Dowiedz się, jak
  wyodrębniać tekst z obrazów, eksportować podsumowania w formacie CSV oraz efektywnie
  obsługiwać masowe OCR obrazów.
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: pl
og_description: Jak wykonywać OCR wsadowo w C# z Aspose.OCR. Uzyskaj pełne rozwiązanie
  do wyodrębniania tekstu z obrazów i eksportowania podsumowań CSV.
og_title: Jak wykonać OCR wsadowo w C# – Pełny poradnik krok po kroku
tags:
- OCR
- C#
- Aspose
- Automation
title: Jak wykonywać OCR wsadowo w C# – Kompletny przewodnik po masowym wyodrębnianiu
  tekstu z obrazów
url: /pl/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać OCR wsadowo – Pełny samouczek C#

Zastanawiałeś się kiedyś **jak wykonywać OCR wsadowo** na całym folderze zdjęć bez pisania osobnej procedury dla każdego pliku? Nie jesteś jedyny. W wielu rzeczywistych projektach — pomyśl o przetwarzaniu faktur, archiwizacji zeskanowanych książek lub masowym digitalizowaniu paragonów — programiści potrzebują szybkiego, niezawodnego sposobu na wyodrębnienie tekstu z dziesiątek, a nawet tysięcy obrazów.  

W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje **jak wykonywać OCR wsadowo**, **wyodrębniać tekst z obrazów** oraz **eksportować podsumowanie CSV** przy użyciu Aspose.OCR. Po zakończeniu będziesz mieć pojedynczy program C#, który może przyjąć dowolny katalog ze zdjęciami, przekształcić je w przeszukiwalne pliki tekstowe i dostarczyć schludny raport CSV z operacji. Bez tajemnic, tylko przejrzysty kod i praktyczne wskazówki.

## Czego się nauczysz

- Skonfiguruj silnik Aspose.OCR dla języka angielskiego (lub dowolnego obsługiwanego języka).  
- Przetwarzaj cały folder obrazów jednorazowo — idealne do wsadowego OCR obrazów.  
- Zapisz każdy wynik OCR jako plik `.txt`, opcjonalnie generując plik CSV, który wymienia każdy obraz źródłowy i długość wyodrębnionego tekstu.  
- Obsłuż typowe przypadki brzegowe, takie jak nieobsługiwane typy plików, puste foldery i znaki Unicode.  

**Wymagania wstępne** – Potrzebujesz .NET 6+ (lub .NET Framework 4.7.2+), Visual Studio 2022 lub dowolnego ulubionego IDE oraz ważnej licencji Aspose.OCR (bezpłatna wersja próbna działa w demonstracjach). Nie są wymagane żadne inne biblioteki zewnętrzne.

![how to batch ocr diagram](https://example.com/ocr-flow.png "how to batch ocr flow diagram")

## Krok 1: Zainstaluj Aspose.OCR i utwórz nowy projekt konsolowy

Aby rozpocząć, dodaj pakiet NuGet Aspose.OCR do swojego projektu:

```bash
dotnet add package Aspose.OCR
```

> **Wskazówka:** Jeśli używasz Visual Studio, możesz także kliknąć prawym przyciskiem projektu → *Zarządzaj pakietami NuGet* → wyszukać *Aspose.OCR* → zainstalować.

Utwórz nową aplikację konsolową (`dotnet new console -n BulkOcrDemo`) i otwórz `Program.cs`. To będzie miejsce dla całego naszego kodu.

## Krok 2: Zainicjalizuj silnik OCR – wybierz właściwy język

Silnik OCR musi wiedzieć, jakiego języka szukać. Angielski jest najczęstszy, ale możesz zamienić go na hiszpański, francuski itp., zmieniając `Language.English`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**Dlaczego to ważne:** Określenie języka zwiększa dokładność, ponieważ silnik może zastosować słowniki i zestawy znaków specyficzne dla języka. Jeśli to pominiesz, otrzymasz model generyczny, który może błędnie interpretować znaki.

## Krok 3: Zdefiniuj ścieżki źródłowe, wyjściowe i opcjonalny CSV

Potrzebujemy trzech folderów:

| Ścieżka | Cel |
|------|---------|
| `sourceFolder` | Gdzie znajdują się oryginalne obrazy. |
| `outputFolder` | Gdzie zostanie zapisany każdy wynik OCR (`.txt`). |
| `csvSummaryPath` | (Opcjonalnie) Plik CSV, który rejestruje nazwę każdego obrazu i długość wyodrębnionego tekstu. |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **Wskazówka:** Używaj `Path.Combine` dla kompatybilności międzyplatformowej; automatycznie wstawia właściwy separator katalogów.

## Krok 4: Uruchom przetwarzanie wsadowe

Aspose.OCR dostarcza przydatny `BatchProcessor`, który wykonuje najcięższą pracę. Przegląda wszystkie obsługiwane obrazy (`.png`, `.jpg`, `.tif` itp.), wykonuje OCR i zapisuje wynik.

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### Co dzieje się w tle?

1. **Wykrywanie plików** – Procesor skanuje `sourceFolder` w poszukiwaniu plików obrazów.  
2. **Wykonanie OCR** – Każdy obraz jest przekazywany do `ocrEngine`.  
3. **Zapisywanie tekstu** – Rozpoznany tekst jest zapisywany do pliku `.txt` o tej samej nazwie bazowej w `outputFolder`.  
4. **Logowanie CSV** – Jeśli podano `csvSummaryPath`, procesor dopisuje wiersz: `ImageName,CharactersExtracted,ProcessingTimeMs`.  

## Krok 5: Dodaj obsługę błędów i wsparcie przypadków brzegowych

Solidne zadanie wsadowe powinno radzić sobie z brakującymi plikami, nieobsługiwanymi formatami i pustymi katalogami. Owiń wywołanie przetwarzania w blok `try/catch` i najpierw zwaliduj dane wejściowe.

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**Dlaczego to dodać?** Bez walidacji program może cicho się nie powieść, pozostawiając pusty folder wyjściowy bez żadnego wyjaśnienia. Jawne komunikaty ułatwiają debugowanie.

## Krok 6: Zweryfikuj wyniki – czego się spodziewać

Po zakończeniu uruchomienia otwórz `outputFolder`. Powinieneś zobaczyć plik `.txt` dla każdego obrazu:

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

Każdy plik zawiera surowy wynik OCR — zwykły tekst, który możesz wprowadzić do indeksów wyszukiwania, baz danych lub dalszych potoków NLP.

Jeśli podałeś `csvSummaryPath`, otwórz `summary.csv`. Będzie wyglądał mniej więcej tak:

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

Plik CSV ułatwia generowanie raportów, wykrywanie wyjątkowo krótkich wyników (możliwe niepowodzenia skanowania) lub przekazywanie metryk do pulpitów monitorujących.

## Krok 7: Rozszerz rozwiązanie – typowe warianty

### 7.1 Zmiana formatu wyjściowego

Zamiast zwykłego `.txt`, możesz chcieć PDF lub JSON. `BatchProcessor` pozwala podać własne wywołanie zwrotne:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 Przetwarzanie wielu języków

Jeśli Twój folder zawiera dokumenty w różnych językach, możesz wykrywać język dla każdego obrazu lub wykonać dwa przebiegi:

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 Eleganckie pomijanie uszkodzonych plików

Dodaj filtr wewnątrz pętli (lub użyj przeciążenia akceptującego predykat), aby ignorować pliki, które generują wyjątek:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## Pełny działający przykład

Poniżej znajduje się kompletny `Program.cs`, który możesz skopiować i wkleić do nowego projektu konsolowego. Zamień ścieżki folderów na własne.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Oczekiwany wynik w konsoli

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

Otwórz jeden z wygenerowanych plików `.txt` i powinieneś zobaczyć wyodrębniony tekst, gotowy do dalszego przetwarzania.

## Najczęściej zadawane pytania

**Czy to działa z plikami PDF?**  
Aspose.OCR może obsługiwać strony PDF, jeśli najpierw przekonwertujesz je na obrazy (np. przy użyciu Aspose.PDF). Sam procesor wsadowy szuka wyłącznie formatów obrazów rastrowych.

**Co zrobić, jeśli muszę przetworzyć 10 000 obrazów?**  
Wbudowany `BatchProcessor` przetwarza każdy plik kolejno, więc zużycie pamięci pozostaje niskie. Przy bardzo dużych obciążeniach możesz równolegle przetwarzać podfoldery, ale pamiętaj, że OCR jest intensywny pod względem CPU — zwróć uwagę na liczbę rdzeni w maszynie.

**Czy mogę zmienić ustawienia dokładności OCR?**  
Tak. `ocrEngine` udostępnia właściwości takie jak `Resolution` i `PreprocessOptions`. Dostosowanie ich może poprawić wyniki przy niskiej jakości skanach, kosztem szybkości.

**Jak licencjonować Aspose.OCR w produkcji?**  
Umieść plik licencji (`Aspose.OCR.lic`) w katalogu wykonywalnym i wczytaj go przy starcie:

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## Podsumowanie

Masz teraz **kompletne, gotowe do produkcji rozwiązanie, jak wykonywać OCR wsadowo** przy użyciu C#. Samouczek obejmował wszystko od instalacji Aspose.OCR, inicjalizacji silnika, przetwarzania całego folderu, po eksport podsumowania CSV

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}