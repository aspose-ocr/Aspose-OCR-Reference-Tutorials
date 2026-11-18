---
category: general
date: 2026-04-03
description: Dowiedz się, jak wykonywać OCR wsadowo przy użyciu Aspose.OCR w C#. Ten
  przewodnik pokazuje, jak wyodrębniać tekst z obrazów PNG i efektywnie konwertować
  obrazy na tekst.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: pl
og_description: Dowiedz się, jak przeprowadzać wsadowe OCR w C#, aby wyodrębniać tekst
  z obrazów PNG i konwertować obrazy na tekst przy użyciu Aspose.OCR. Dołączony pełny
  kod.
og_title: Jak przeprowadzić wsadowe OCR w C# – szybki przewodnik
tags:
- OCR
- C#
- Aspose
title: Jak wykonać OCR wsadowo w C# – szybki sposób na wyodrębnianie tekstu z plików
  PNG
url: /pl/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać wsadowe OCR w C# – Szybki sposób na wyodrębnienie tekstu z plików PNG

Zastanawiałeś się kiedyś **jak wykonać wsadowe OCR** na całym folderze zrzutów ekranu, nie pisząc pętli dla każdego pliku? Nie jesteś sam. W wielu projektach — myśl o cyfryzacji faktur lub archiwizacji zeskanowanych paragonów — kończysz z dziesiątkami, a czasem setkami plików PNG, z których trzeba wyciągnąć tekst. Dobra wiadomość? Dzięki Aspose.OCR możesz **wyodrębnić tekst z obrazów PNG** równolegle, a cały proces zamknąć w kilku linijkach C#.

W tym tutorialu przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokazuje, jak **konwertować obrazy na tekst** przy użyciu procesora wsadowego. Omówimy wymagania wstępne, wyjaśnimy, dlaczego każda linijka ma znaczenie, i podzielimy się kilkoma pro‑tipami, abyś nie natrafił na typowe pułapki.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- **.NET 6.0** (lub nowszy) zainstalowany na komputerze. Starsze runtime’y działają, ale najnowszy zapewnia lepszą wydajność i obsługę async.
- Pakiet **Aspose.OCR for .NET**. Możesz go pobrać przez NuGet: `dotnet add package Aspose.OCR`.
- Folder pełen **obrazów PNG**, które chcesz przetworzyć. Będziemy go nazywać `YOUR_DIRECTORY` w całym przewodniku.
- Umiarkowaną ilość RAM‑u — wsadowe OCR może być pamięcio‑chłonne przy wysokim stopniu równoległości, ale użycie `Environment.ProcessorCount` utrzymuje to w ryzach.

> **Pro tip:** Jeśli pracujesz w pipeline CI/CD, dodaj plik licencji Aspose jako secret, aby uniknąć limitu 20 stron w wersji ewaluacyjnej.

Teraz zabierzmy się do pracy.

## Krok 1: Konfiguracja Batch OCR Processor (Primary Keyword in Header)

Pierwszą rzeczą, której potrzebujesz, jest instancja `BatchOcrProcessor`. Ta klasa ukrywa logikę wątkowania i pozwala skupić się na tym, co zrobić z każdym obrazem.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Dlaczego to ważne:**  
- `Engine = new OcrEngine()` zapewnia świeży silnik OCR dla każdego wątku, eliminując konflikty.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` automatycznie skaluje się do liczby rdzeni, dając maksymalną przepustowość bez ręcznej konfiguracji.

## Krok 2: Podłączenie zdarzeń postępu (Helps Track Extraction)

Śledzenie postępu jest niezbędne przy przetwarzaniu setek plików. Zdarzenie `ProgressChanged` wywołuje się po zakończeniu każdego pliku, umożliwiając logowanie statusu.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Dlaczego to pokochasz:**  
- Informacje w czasie rzeczywistym zapobiegają zastanawianiu się, czy aplikacja się zawiesiła.  
- Jeśli kiedykolwiek będziesz potrzebował wstrzymać lub anulować proces, masz już punkt zaczepienia, aby porównać `e.Current` z `e.Total`.

## Krok 3: Definicja skanowania folderu i wzorca plików (Extract Text PNG)

Teraz informujemy procesor, gdzie szukać i jakie pliki wybrać. Wzorzec `"*.png"` zapewnia, że obsługujemy wyłącznie obrazy PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Dlaczego to kluczowe:**  
- Użycie wzorca globowego utrzymuje kod elastycznym; zmień `*.png` na `*.jpg`, jeśli później będziesz potrzebował obsługi JPEG‑ów.  
- Callback otrzymuje zarówno ścieżkę obrazu, jak i rozpoznany tekst, dając pełną kontrolę nad dalszymi działaniami.

## Krok 4: Zapisz rozpoznany tekst obok źródła (Convert Images to Text)

Wewnątrz callbacku zapisujemy wynik OCR do pliku `.txt`, który znajduje się tuż obok oryginalnego PNG. To najprostszy sposób na **konwertowanie obrazów na tekst** dla dalszych procesów.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Dlaczego wybieramy plik `.txt` obok obrazu:**  
- Relacja jest oczywista — otwierasz PNG, otwierasz TXT, porównujesz.  
- Nie potrzebujesz bazy danych ani dodatkowej warstwy przechowywania w małych projektach.

## Krok 5: Zakończenie przyjaznym komunikatem

Ładna wiadomość w konsoli informuje, kiedy wszystko się skończyło.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Po uruchomieniu programu zobaczysz wyjście podobne do:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Każdy PNG ma teraz towarzyszący plik `.txt` zawierający wyodrębniony tekst.

## Pełny działający przykład (Wszystkie kroki razem)

Poniżej znajduje się cały program, który możesz skopiować i wkleić do nowego projektu konsolowego. Nie brakuje żadnych części — wystarczy podmienić `YOUR_DIRECTORY` na pełną ścieżkę do swoich obrazów.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Oczekiwany rezultat

- Dla każdego `image.png` w `C:\MyImages` pojawia się `image.txt` obok niego.  
- Konsola wypisuje linie postępu, co ułatwia monitorowanie dużych partii.  
- Brak ręcznej pętli czy zarządzania wątkami — `BatchOcrProcessor` robi wszystko za Ciebie.

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli moje obrazy nie są PNG?

Po prostu zmień drugi argument w `ProcessFolder` na `"*.jpg"` lub `"*.*"`, aby objąć wszystkie pliki. Silnik OCR działa z większością formatów rastrowych.

### Ile pamięci to zużywa?

`BatchOcrProcessor` ładuje jeden obraz na wątek. Przy `Environment.ProcessorCount` ustawionym na przykład na 8 rdzeni, w pamięci będzie jednocześnie osiem obrazów. Jeśli napotkasz wyjątki OutOfMemory, zmniejsz równoległość:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Czy mogę dostosować język OCR?

Oczywiście. Po stworzeniu silnika ustaw jego właściwość `Language`:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose obsługuje wiele języków; w razie potrzeby dodaj odpowiedni pakiet NuGet.

### A co z obsługą błędów?

Otocz callback w blok try/catch i loguj niepowodzenia. Procesor przejdzie do kolejnego pliku, zapobiegając przerwaniu całego działania przez jedną uszkodzoną grafikę.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Pro Tipy dla skalowania

- **Podziel folder**: Jeśli masz dziesiątki tysięcy plików, podziel je na podfoldery i uruchamiaj kolejne zadania wsadowe.  
- **Użyj maszyny w chmurze**: Instancja z większą liczbą rdzeni (np. 32‑rdzeniowa) zakończy pracę znacznie szybciej. Pamiętaj tylko o dostosowaniu limitów licencji.  
- **Post‑process tekst**: Po wyodrębnieniu możesz uruchomić wyrażenia regularne, aby wyłuskać numery faktur lub daty. Pliki `.txt` są idealnym wejściem dla takich potoków.

## Podsumowanie

Masz teraz solidny, gotowy do produkcji przepis na **jak wykonać wsadowe OCR** katalogu PNG, **wyodrębnić tekst z plików PNG** i **konwertować obrazy na tekst** przy użyciu Aspose.OCR w C#. Przykład jest samodzielny, wyjaśnia „dlaczego” każdej linijki i zawiera wskazówki dotyczące większych obciążeń oraz innych typów plików.

Gotowy na kolejny krok? Spróbuj zmienić callback, aby zapisywać wyniki w bazie danych, lub dodaj wstępne przetwarzanie obrazu (np. deskew) przed OCR. Wzorzec skaluje się łatwo, więc możesz go dopasować do dowolnego scenariusza przetwarzania wsadowego.

Miłego kodowania i niech Twoje pipeline’y OCR będą szybkie i wolne od błędów!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}