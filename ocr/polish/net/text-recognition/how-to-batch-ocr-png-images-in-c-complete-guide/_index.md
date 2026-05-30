---
category: general
date: 2026-04-26
description: Jak szybko przeprowadzić OCR wielu obrazów PNG. Dowiedz się, jak wyodrębnić
  tekst z PNG, konwertować obrazy na tekst, zapisywać rozpoznany tekst oraz odczytywać
  katalog PNG przy użyciu Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: pl
og_description: Jak przetwarzać wsadowo obrazy PNG za pomocą OCR w C# z Aspose OCR.
  Ten przewodnik pokazuje, jak wyodrębnić tekst z PNG, konwertować obrazy na tekst
  i efektywnie zapisywać rozpoznany tekst.
og_title: Jak wykonać wsadowe OCR obrazów PNG w C# – krok po kroku
tags:
- OCR
- C#
- Aspose
title: Jak wykonać wsadowe OCR obrazów PNG w C# – Kompletny przewodnik
url: /pl/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przetwarzać wsadowo obrazy PNG OCR w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak przetwarzać wsadowo OCR** całego folderu plików PNG bez pisania osobnego programu dla każdego obrazu? Nie jesteś jedynym, który żongluje dziesiątkami zrzutów ekranu, zeskanowanych paragonów czy grafik, które trzeba przekształcić w tekst przeszukiwalny. W tym samouczku przeprowadzimy praktyczne rozwiązanie, które **wyodrębnia tekst z PNG**, **konwertuje obrazy na tekst** i **zapisuje rozpoznany tekst** do poszczególnych plików — wszystko przy automatycznym odczytywaniu katalogu PNG.

Do końca tego przewodnika będziesz mieć gotową do uruchomienia aplikację konsolową C#, która przetwarza dowolną liczbę obrazów jednorazowo. Bez dodatkowych skryptów, bez ręcznego kopiowania‑wklejania — po prostu czysty kod, który wykona ciężką pracę za Ciebie.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod działa również na .NET Framework).  
- Pakiet NuGet **Aspose.OCR for .NET** (darmowa wersja próbna wystarczy do testów).  
- Folder z kilkoma plikami *.png*, które chcesz poddać OCR.  
- Visual Studio 2022 lub dowolne inne IDE dla C#.

Jeśli masz te elementy, możemy od razu przejść do implementacji.

## Krok 1 – Przygotuj foldery wejściowe i wyjściowe *(Odczyt katalogu PNG)*

Pierwsze, co robimy, to wskazujemy programowi folder zawierający obrazy i decydujemy, gdzie będą przechowywane wynikowe pliki *.txt*. Użycie `Directory.GetFiles` daje nam czystą kolekcję wszystkich plików PNG w katalogu.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Dlaczego to ma znaczenie:**  
- Użycie maski (`*.png`) gwarantuje, że przetwarzamy wyłącznie pliki graficzne, pomijając przypadkowe dokumenty.  
- Tworzenie folderu wyjściowego w locie zapobiega późniejszemu `DirectoryNotFoundException`.

> **Pro tip:** Jeśli potrzebujesz obsługi innych formatów (JPEG, BMP), po prostu rozszerz wzorzec wyszukiwania lub wywołaj `Directory.EnumerateFiles` z wieloma rozszerzeniami.

## Krok 2 – Zainicjalizuj silnik OCR *(Konwertuj obrazy na tekst)*

Aspose.OCR dostarcza dwa typy silników: oparty na CPU `OcrEngine` oraz przyspieszany GPU `GpuOcrEngine`. Dla większości zadań wsadowych silnik CPU jest w zupełności wystarczający, ale możesz zamienić nazwę klasy, jeśli dysponujesz odpowiednim GPU.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Dlaczego to ma znaczenie:**  
- Określenie języka znacząco podnosi dokładność, ponieważ silnik wie, jakiego zestawu znaków się spodziewać.  
- Przejście na `GpuOcrEngine` wymaga tylko jednej linii, jeśli napotkasz wąskie gardła wydajności przy dużych partiach.

## Krok 3 – Utwórz rozpoznawacz wsadowy

Aspose udostępnia wygodny `BatchRecognizer`, który przyjmuje kolekcję ścieżek plików i strumieniuje wyniki jeden po drugim. Dzięki temu nie musimy ładować wszystkich obrazów do pamięci jednocześnie — kluczowy detal przy dużych folderach.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Dlaczego to ma znaczenie:**  
- Rozpoznawacz wsadowy enkapsuluje logikę pętli, pozwalając nam skupić się na tym, co zrobić z każdym wynikiem, zamiast na tym, jak bezpiecznie iterować.

## Krok 4 – Uruchom OCR na wszystkich obrazach i zapisz wynik *(Zapisz rozpoznany tekst)*

Teraz faktycznie wykonujemy OCR. Metoda `Recognize` zwraca `IEnumerable<RecognitionResult>`, gdzie każdy wynik zawiera wyodrębniony tekst oraz dodatkowe metadane.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Dlaczego to ma znaczenie:**  
- Użycie `File.WriteAllText` zapewnia, że tekst jest zapisywany domyślnie w kodowaniu UTF‑8, zachowując znaki specjalne.  
- Numeracja inkrementalna (`out_0.txt`, `out_1.txt`) odpowiada kolejności przetwarzania, co jest przydatne przy debugowaniu.

> **Edge case:** Jeśli którykolwiek obraz nie zostanie rozpoznany (np. uszkodzony plik), `RecognitionResult.Text` będzie pusty. Możesz dodać prostą kontrolę wewnątrz pętli, aby logować niepowodzenia:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Krok 5 – Połącz wszystko – pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować‑wkleić do nowego projektu konsolowego. Zawiera on dyrektywy `using`, walidację folderów oraz mały interfejs konsolowy, dzięki któremu wiesz, kiedy partia się zakończyła.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Oczekiwany wynik:**  
```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Zobaczysz pliki `out_0.txt` … `out_11.txt` w folderze wyjściowym, każdy zawierający wersję tekstową odpowiadającego mu obrazu.

## Częste pytania i wskazówki

| Pytanie | Odpowiedź |
|----------|--------|
| *Czy mogę przetwarzać również podfoldery?* | Tak — zamień `Directory.GetFiles` na `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Co zrobić, jeśli potrzebuję innego języka?* | Ustaw `ocrEngine.Language = Language.Spanish;` (lub dowolny obsługiwany enum). |
| *Jak radzić sobie z ogromnymi partiami (tysiące plików)?* | Rozważ przetwarzanie w partiach lub użycie `Parallel.ForEach` z ograniczoną liczbą równoległych wątków, aby nie wyczerpać pamięci. |
| *Czy wynik zawsze jest UTF‑8?* | `File.WriteAllText` domyślnie zapisuje w UTF‑8 bez BOM, co działa dla większości języków opartych na alfabecie łacińskim. Dla skryptów azjatyckich może być konieczne jawne ustawienie `Encoding.UTF8`. |
| *Czy mogę uzyskać wyniki pewności (confidence scores)?* | `RecognitionResult` udostępnia właściwość `Confidence` — możesz ją logować razem z tekstem w celu kontroli jakości. |

## Przegląd wizualny *(Jak przetwarzać wsadowo OCR – diagram)*

![Diagram przepływu wsadowego OCR pokazujący folder wejściowy → silnik OCR → rozpoznawacz wsadowy → pliki wyjściowe txt](https://example.com/diagram-how-to-batch-ocr.png "Jak przetwarzać wsadowo OCR")

*Tekst alternatywny zawiera główne słowo kluczowe, spełniając wymagania SEO dla obrazów.*

## Podsumowanie

Właśnie omówiliśmy **jak przetwarzać wsadowo OCR** katalogu plików PNG przy użyciu Aspose.OCR, od odczytu katalogu PNG po zapis każdego rozpoznanego pliku tekstowego. Rozwiązanie jest w pełni samodzielne, działa na każdym nowoczesnym środowisku .NET i może być rozszerzone o przyspieszenie GPU, obsługę wielu języków lub przetwarzanie równoległe.

Gotowy na kolejny krok? Spróbuj zamienić `Language.Latin` na inny język lub zintegrować wynik z indeksem wyszukiwania, aby Twoje dokumenty stały się od razu przeszukiwalne. Nie ma granic, gdy opanujesz wsadowe OCR.

Miłego kodowania i daj znać w komentarzach, jeśli napotkasz jakiekolwiek problemy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}