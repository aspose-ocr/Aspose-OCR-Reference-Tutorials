---
category: general
date: 2026-03-13
description: Jak szybko i niezawodnie przeprowadzić OCR wsadowe, ucząc się jednocześnie
  wyodrębniać tekst z plików TIFF przy użyciu Aspose.OCR. Postępuj zgodnie z tym samouczkiem
  krok po kroku.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: pl
og_description: Dowiedz się, jak przeprowadzić OCR wsadowe w C# i wyodrębnić tekst
  z plików TIFF przy użyciu Aspose.OCR. Ten przewodnik obejmuje konfigurację, kod
  oraz wskazówki dotyczące najlepszych praktyk.
og_title: Jak przetwarzać OCR wsadowo w C# – Kompletny przewodnik programistyczny
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Jak przetwarzać OCR wsadowo w C# – Kompletny przewodnik programistyczny
url: /pl/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać batch OCR w C# – Kompletny przewodnik programistyczny

Zastanawiałeś się kiedyś, **jak wykonać batch OCR** na górach zeskanowanych faktur, nie pisząc osobnego skryptu dla każdego pliku? Nie jesteś sam. W wielu rzeczywistych projektach problemem nie jest sama dokładność OCR, lecz ogromna liczba obrazów — często plików TIFF — które trzeba przekształcić w przeszukiwalny tekst.  

Ten tutorial pokazuje, **jak wykonać batch OCR** przy użyciu `BatchProcessor` z Aspose.OCR, a jednocześnie uczy, **jak wyodrębnić tekst z tiff** w jednym, czystym przebiegu. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która przetwarza cały folder, wykorzystuje opcjonalne przyspieszenie GPU i zapisuje wyniki w formie zwykłego tekstu tam, gdzie ich potrzebujesz.

## Co będzie potrzebne

- **.NET 6+** (lub .NET Framework 4.7.2, jeśli wolisz klasyczny runtime)  
- **Aspose.OCR for .NET** – możesz pobrać pakiet NuGet poleceniem `dotnet add package Aspose.OCR`.  
- Folder z obrazami **TIFF**, które chcesz odczytać (w tutorialu używamy przykładu `Invoices`).  
- Opcjonalnie: GPU obsługujące DirectX 11 lub CUDA, jeśli chcesz przyspieszyć przetwarzanie.  

Bez dodatkowych usług, bez kluczy w chmurze — tylko lokalny projekt C# i biblioteka Aspose.

## Krok 1: Utwórz projekt i zainstaluj Aspose.OCR

Najpierw utwórz aplikację konsolową.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Jeśli pracujesz w systemie Windows i planujesz używać przyspieszenia GPU, upewnij się, że masz zainstalowany najnowszy sterownik graficzny. W przeciwnym razie flaga `UseGpu = true` automatycznie przełączy się na CPU.

## Krok 2: Utwórz konfigurację BatchProcessor

Teraz skonfigurujemy `BatchProcessor`. To serce **jak wykonać batch OCR** — mówisz Aspose, jakiego języka się spodziewać, które filtry wstępne zastosować i czy korzystać z GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Dlaczego te ustawienia?**  
- `Language = Language.English` informuje silnik, aby użył modelu języka angielskiego, który jest znacznie dokładniejszy niż model generyczny.  
- `UseGpu` może skrócić czas przetwarzania o połowę na przyzwoitym GPU, ale możesz zostawić `false`, jeśli pracujesz na laptopie bez takiego sprzętu.  
- Potok filtrów odzwierciedla to, co zrobiłby człowiek: prostowanie strony i usuwanie plam przed przekazaniem obrazu do silnika OCR.

## Krok 3: Wskaż folder z plikami TIFF

Kolejny element **jak wykonać batch OCR** to poinformowanie biblioteki, gdzie znajdują się pliki źródłowe. Obsługiwane są maski, więc możesz jednorazowo pobrać wszystkie pliki `.tif`.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Edge case:** Jeśli Twoje obrazy mają mieszane rozszerzenia (`.tiff`, `.tif`, `.png`), wywołaj `AddFolder` wielokrotnie lub użyj `*.*` i odfiltruj je później w kodzie.

## Krok 4: Wybierz miejsce docelowe wyników OCR

Możesz się zastanawiać: „Gdzie trafia wyodrębniony tekst?” To trzeci filar **jak wykonać batch OCR** — określenie lokalizacji i formatu wyjścia. Zapiszemy pliki tekstowe obok oryginałów.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Jeśli potrzebujesz JSON lub XML zamiast zwykłego tekstu, po prostu zamień `OutputFormat.PlainText` na `OutputFormat.Json` lub `OutputFormat.Xml`. Biblioteka zajmie się konwersją.

## Krok 5: Uruchom zadanie batch i zgłoś wyniki

Na koniec uruchom zadanie. Metoda `Execute` blokuje działanie, dopóki każdy plik nie zostanie przetworzony, a potem możesz sprawdzić `ProcessedCount`, aby potwierdzić sukces.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Oczekiwany wynik

Po uruchomieniu programu konsola wyświetli coś podobnego do:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

W folderze `Output` znajdziesz po jednym pliku `.txt` dla każdego źródłowego TIFF, nazwanym tak jak oryginalny obraz (np. `Invoice_001.txt`). Otwórz dowolny plik, a zobaczysz surowy tekst OCR — idealny do wprowadzenia do indeksu wyszukiwania lub dalszego potoku ekstrakcji danych.

## Rozwiązywanie typowych problemów

### 1. GPU niedostępne

Jeśli `UseGpu = true`, ale nie wykryto kompatybilnego urządzenia, Aspose automatycznie przełączy się na CPU. Aby być tego pewnym, możesz przechwycić `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Pliki nie‑TIFF w tym samym folderze

Gdy masz mieszany folder, filtruj programowo:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Duże pliki przekraczające pamięć

Dla ogromnych wielostronicowych TIFF‑ów włącz streaming:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Pro Tips dla lepszej dokładności przy **wyodrębnianiu tekstu z tiff**

- **Rozdzielczość ma znaczenie** – Celuj w 300 dpi lub wyżej. Poniżej tego silnik OCR może pomijać znaki.  
- **Kolor vs. odcienie szarości** – Przed OCR konwertuj skany kolorowe na odcienie szarości; `DeskewFilter` robi to automatycznie, ale możesz dodać `ColorDepthReductionFilter` dla dodatkowej prędkości.  
- **Post‑processing** – Po uzyskaniu tekstu zwykłego uruchom sprawdzanie pisowni lub czyszczenie regexem, aby naprawić typowe błędy OCR (np. „0” vs „O”).

## Pełny działający przykład (Gotowy do kopiowania)

Poniżej znajduje się cały program, który możesz skompilować i uruchomić. Wystarczy podmienić ścieżki placeholderów na własne katalogi.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Kompiluj i uruchom:

```bash
dotnet run
```

Teraz powinieneś mieć uporządkowany zestaw plików `.txt` — każdy z nich jest wynikiem **wyodrębniania tekstu z tiff** przy użyciu w pełni zautomatyzowanego procesu batch.

## Podsumowanie

Przeszliśmy przez **jak wykonać batch OCR** w C# od początku do końca, omawiając wszystko, co potrzebne, aby **wyodrębnić tekst z tiff** efektywnie. Najważniejsze wnioski:

1. Używaj `BatchProcessor` z Aspose.OCR, aby uniknąć pisania powtarzalnych pętli.  
2. Wykorzystuj filtry wstępne (deskew, despeckle) dla wyższej dokładności.  
3. Włącz przyspieszenie GPU, gdy to możliwe, ale zawsze miej fallback na CPU.  
4. Przechowuj wyniki w przewidywalnej strukturze folderów, aby kolejne zadania mogły je automatycznie pobierać.

Od tego momentu możesz rozważyć:

- Przekazanie tekstu do **indeksu wyszukiwania** (np. Elasticsearch), aby faktury stały się przeszukiwalne.  
- Konwersję wyjścia do **JSON** i podanie go modelowi uczenia maszynowego, który wyodrębnia pozycje faktury.  
- Dodanie **obsługi błędów** dla uszkodzonych plików TIFF lub problemów z uprawnieniami.

Spróbuj sam,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}