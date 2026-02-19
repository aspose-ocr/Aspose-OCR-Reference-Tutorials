---
category: general
date: 2026-02-19
description: Dowiedz się, jak wykonywać OCR wsadowo przy użyciu Aspose.OCR w C#. Ten
  przewodnik pokaże Ci, jak wydobywać tekst z obrazów i efektywnie konwertować obrazy
  na pliki txt.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: pl
og_description: Jak przetwarzać OCR wsadowo przy użyciu Aspose.OCR w C#. Wyodrębnij
  tekst z obrazów i konwertuj obrazy na pliki txt w kilku prostych krokach.
og_title: Jak wykonywać OCR wsadowo w C# – szybka konwersja obrazu na tekst
tags:
- OCR
- C#
- Aspose
title: Jak przeprowadzić wsadowe OCR w C# – Szybko wyodrębniaj tekst z obrazów
url: /pl/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przetwarzać OCR wsadowo w C# – Pełny przewodnik krok po kroku

Zastanawiałeś się kiedyś **jak przetwarzać OCR wsadowo** cały folder zdjęć bez pisania osobnego programu dla każdego pliku? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy muszą wyodrębnić tekst z dziesiątek — a nawet tysięcy — zeskanowanych stron, paragonów lub zrzutów ekranu. Dobra wiadomość? Dzięki Aspose.OCR możesz zautomatyzować cały proces, **wyodrębnić tekst z obrazów** i **konwertować obrazy do txt** przy użyciu kilku linii kodu.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje dokładnie, jak skonfigurować przetwarzacz OCR wsadowego, dostosować wstępne przetwarzanie, obsłużyć równoległość i zapisać każdy wynik do pliku `.txt`. Po zakończeniu będziesz mieć samodzielną aplikację konsolową, którą możesz wkleić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również na .NET Core i .NET Framework)
- Pakiet NuGet Aspose.OCR dla .NET (`Aspose.OCR`)  
- Folder pełen plików graficznych (`.png`, `.jpg`, itp.), które chcesz przetworzyć
- Umiarkowana ilość pamięci RAM; demo używa 4 równoległych wątków, ale możesz to dostosować

Bez zewnętrznych usług, bez ukrytych plików konfiguracyjnych — po prostu czysty kod C#, który możesz skompilować i uruchomić już dziś.

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## Krok 1: Zainstaluj Aspose.OCR i skonfiguruj projekt

Najpierw dodaj pakiet Aspose.OCR do swojego projektu:

```bash
dotnet add package Aspose.OCR
```

Dlaczego to ważne: Aspose.OCR zawiera silnik OCR, dane językowe oraz narzędzia wstępnego przetwarzania, więc nie będziesz potrzebować żadnych zewnętrznych binarek. Po zainstalowaniu pakietu utwórz nową aplikację konsolową (lub dodaj kod do istniejącej) i zaimportuj wymagane przestrzenie nazw:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Te instrukcje `using` dają dostęp do klas przetwarzacza wsadowego oraz przydatnych pomocników I/O.

## Krok 2: Skonfiguruj przetwarzacz OCR wsadowego

Teraz utworzymy instancję `OcrBatchProcessor` i określimy, jakiego języka szukać, jak oczyszczać obrazy oraz ile wątków uruchomić równolegle. To jest sedno **jak przetwarzać OCR wsadowo** efektywnie.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Dlaczego włączyć Deskew?** Wiele zeskanowanych dokumentów nie jest idealnie wyrównanych; algorytm deskew obraca je z powrotem do prostej linii bazowej, co często zwiększa współczynnik rozpoznawania o 10‑15 %.

## Krok 3: Podłącz wywołanie zwrotne wyniku, aby zapisywać pliki tekstowe

Przetwarzacz wsadowy wywołuje zdarzenie dla każdego zakończonego obrazu. Zasubskrybujemy `ResultProcessed`, aby móc zapisać każdy wynik OCR do pliku `.txt` — efektywnie **konwertując obrazy do txt** w locie.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Szybka wskazówka: jeśli potrzebujesz zachować pierwotną strukturę folderów, możesz zmodyfikować `txtPath`, aby uwzględniał podfoldery lub osobny katalog wyjściowy.

## Krok 4: Uruchom wsad na folderze z obrazami

Pozostało już tylko skierować przetwarzacz na folder zawierający obrazy, z których chcesz **wyodrębnić tekst z obrazów**. Metoda `ProcessFolder` skanuje podfoldery rekurencyjnie, więc możesz wrzucić całe drzewo skanów i pozwolić bibliotece zająć się resztą.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

Po uruchomieniu programu zobaczysz wyjście w konsoli podobne do:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Każdy obraz ma teraz sąsiadujący plik `.txt` zawierający wyodrębniony tekst.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować‑wkleić do `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Oczekiwany wynik

- Dla każdego `*.png` lub `*.jpg` w katalogu źródłowym pojawia się odpowiadający plik `*.txt` obok niego.
- Konsola wypisuje jedną linię na plik, dając bieżące informacje zwrotne.
- Jeśli obraz nie może zostać odczytany (uszkodzony plik, nieobsługiwany format), Aspose.OCR zapisuje błąd w logu, ale kontynuuje przetwarzanie pozostałych — dzięki wbudowanej odporności silnika wsadowego.

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli muszę przetwarzać PDF-y zamiast obrazów?

Aspose.OCR może przyjąć strony PDF jako obrazy wewnętrznie, ale najpierw musisz przekonwertować PDF na obrazy rastrowe (np. przy użyciu Aspose.PDF). Gdy masz już pliki PNG, ten sam kod wsadowy działa bez zmian.

### Czy mogę zmienić język w locie?

Tak. Właściwość `Language` przyjmuje dowolną wartość enum `Language` (Spanish, French, Chinese, itp.). Jeśli masz dokumenty wielojęzyczne, rozważ wykonanie dwóch przebiegów — po jednym dla każdego języka — lub użyj `Language.AutoDetect`.

### Jak ograniczyć wsad do określonych typów plików?

`ProcessFolder` przyjmuje opcjonalny `SearchOption` oraz `string[] extensions`. Przykład:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### Co z przyspieszeniem GPU?

Aspose.OCR obsługuje GPU poprzez konfigurację `OcrEngine`, ale `MaxDegreeOfParallelism` przetwarzacza wsadowego nadal jest głównym ustawieniem współbieżności. Jeśli masz kompatybilny GPU, włącz go w ustawieniach silnika przed utworzeniem `OcrBatchProcessor`.

### Jak obsłużyć bardzo duże foldery (dziesiątki tysięcy plików)?

- Ostrożnie zwiększ `MaxDegreeOfParallelism`; zbyt wiele wątków może wyczerpać pamięć.
- Użyj dedykowanego folderu wyjściowego, aby uniknąć bałaganu.
- Okresowo opróżniaj logi na dysk, aby zapobiec nadmiernemu zużyciu pamięci.

## Profesjonalne wskazówki dla wysokiej jakości OCR

- **DPI ma znaczenie**: Obrazy o rozdzielczości 300 DPI lub wyższej zapewniają najlepszą dokładność. Jeśli twoje skany są niższe, rozważ zwiększenie rozdzielczości przy użyciu filtru bikubicznego przed przetwarzaniem.
- **Redukcja szumów**: Włącz `Preprocessing.NoiseRemoval`, jeśli źródłowe obrazy są ziarniste.
- **Nazewnictwo plików**: Trzymaj nazwy plików krótkie i alfanumeryczne; znaki specjalne mogą mylić logikę ścieżki w wywołaniu zwrotnym.
- **Logowanie**: Zastąp `Console.WriteLine` odpowiednim loggerem (np. `Serilog`) w środowiskach produkcyjnych.

## Kolejne kroki

Teraz, gdy opanowałeś **jak przetwarzać OCR wsadowo**, możesz chcieć:

- **Wyodrębnić tekst z obrazów** i wprowadzić wynik do indeksu wyszukiwania (np. Elasticsearch) w celu pełnotekstowego przeszukiwania.
- **Konwertować obrazy do txt** i następnie uruchomić przetwarzanie języka naturalnego (NLP), aby automatycznie klasyfikować dokumenty.
- Eksperymentuj z **różnymi pakietami językowymi** lub własnymi słownikami dla terminologii specyficznej dla branży.

Jeśli interesuje Cię przetwarzanie po‑OCR, sprawdź samouczki o „Parsowaniu wyników OCR przy użyciu wyrażeń regularnych” lub „Przechowywaniu wyników OCR w bazie danych SQL”.

---

**Miłego kodowania!** Śmiało dostosowuj równoległość, dodawaj kolejne kroki wstępnego przetwarzania lub opakuj całość w usługę Windows dla ciągłego monitorowania. Nie ma granic, gdy połączysz możliwości wsadowe Aspose.OCR z odrobiną pomysłowości .NET.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}