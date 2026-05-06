---
category: general
date: 2026-05-06
description: Dowiedz się, jak przetwarzać OCR wsadowo w C# i szybko wyodrębniać tekst
  ze skanów przy użyciu Aspose OCR Batch. Skorzystaj z kompletnego przewodnika krok
  po kroku z kodem, wskazówkami i obsługą przypadków brzegowych.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: pl
og_description: Jak przetwarzać OCR wsadowo w C#? Ten przewodnik pokazuje, jak wydajnie
  wyodrębniać tekst ze skanów przy użyciu Aspose OCR, wsparcia GPU i przetwarzania
  równoległego.
og_title: Jak wykonywać OCR wsadowo w C# – wyodrębniaj tekst ze skanów
tags:
- C#
- OCR
- Aspose
title: Jak wykonać wsadowe OCR w C# – wyodrębnić tekst ze skanów
url: /pl/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać wsadowe OCR w C# – Wyodrębnić tekst ze skanów

Zastanawiałeś się kiedyś **jak wykonać wsadowe OCR**, gdy masz folder pełen zeskanowanych PDF‑ów lub JPEG‑ów? Nie jesteś jedyną osobą, która patrzy na góry obrazów i myśli: „Musi istnieć szybszy sposób na wyciągnięcie tekstu”. W tym samouczku przeprowadzimy praktyczne rozwiązanie, które nie tylko pozwala **wyodrębnić tekst ze skanów**, ale także przyspiesza działanie dzięki przyspieszeniu GPU i równoległości.

Rzecz w tym, że wykonywanie OCR pliku po pliku pochłania mnóstwo czasu, szczególnie gdy masz do czynienia z dziesiątkami lub setkami stron. Po zakończeniu tego przewodnika będziesz mieć gotową do uruchomienia aplikację konsolową C#, która przetwarza cały katalog jednym poleceniem, dostarczając czyste pliki tekstowe gotowe do indeksowania, wyszukiwania lub czegokolwiek, co nastąpi dalej.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- **.NET 6.0 lub nowszy** (kod wykorzystuje nowoczesne funkcje C#).
- **Licencję na Aspose.OCR** (bezpłatna wersja próbna wystarczy do testów).
- Maszynę **kompatybilną z GPU**, **jeśli chcesz włączyć `UseGpu`**; w przeciwnym razie biblioteka przełączy się na CPU.
- Podstawową znajomość **aplikacji konsolowych C#**.

Bez zewnętrznych usług, bez ukrytych plików konfiguracyjnych — tylko SDK i folder z obrazami.

## Krok 1: Zainstaluj pakiet NuGet Aspose.OCR

Najpierw dodaj bibliotekę Aspose OCR do swojego projektu. Otwórz terminal w katalogu rozwiązania i uruchom:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Jeśli używasz Visual Studio, możesz również dodać pakiet za pomocą interfejsu NuGet Package Manager UI.

## Krok 2: Utwórz szkielet aplikacji konsolowej

Ustawmy minimalną aplikację konsolową, która będzie hostować nasz procesor wsadowy. Utwórz nowy plik o nazwie `Program.cs` i wklej poniższy szkielet:

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

Dlaczego opakowujemy logikę wewnątrz `Main`? Ponieważ aplikacja konsolowa daje nam natychmiastową informację zwrotną za pomocą `Console.WriteLine`, co jest idealne do szybkiej weryfikacji, że zadanie **wsadowego OCR** rzeczywiście się zakończyło.

## Krok 3: Skonfiguruj OcrBatchProcessor

Teraz najważniejsza część rozwiązania. Utworzymy instancję `OcrBatchProcessor`, wskażemy folder wejściowy, określimy miejsce zapisu wyników i dostosujemy kilka parametrów wydajności.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Dlaczego te ustawienia mają znaczenie

| Ustawienie | Co robi | Kiedy możesz to zmienić |
|------------|---------|--------------------------|
| `InputFolder` | Ścieżka do skanów, które chcesz przetworzyć. | Użyj ścieżki względnej dla przenośności. |
| `OutputFolder` | Miejsce, w którym wyodrębniony tekst z każdego obrazu zostanie zapisany jako plik `.txt`. | Wskaż udział sieciowy, jeśli potrzebujesz centralnego przechowywania. |
| `Language` | Model językowy OCR; wybraliśmy hiszpański, aby pokazać obsługę wielu języków. | Przełącz na `OcrLanguage.English` lub dowolny obsługiwany język. |
| `UseGpu` | Przenosi ciężkie obliczenia macierzowe na GPU. | Ustaw na `false` na serwerach bez GPU. |
| `MaxDegreeOfParallelism` | Kontroluje, ile obrazów jest przetwarzanych jednocześnie. | Zmniejsz na maszynach o niskiej mocy CPU, aby uniknąć przeciążenia. |

## Krok 4: Wykonaj operację wsadową z obsługą błędów

Uruchomienie wsadu jest tak proste, jak wywołanie `Execute()`, ale otoczymy to blokiem try‑catch, aby otrzymać przydatny komunikat w razie problemu (np. brak folderu, nieobsługiwany format obrazu).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

Gdy procesor zakończy działanie, zobaczysz **Batch completed.** w konsoli, a każdy oryginalny obraz będzie miał odpowiadający plik `.txt` w folderze `OcrResults`. Nazwy plików odzwierciedlają oryginały, co ułatwia mapowanie z powrotem do pierwotnego skanu.

## Krok 5: Zweryfikuj wyniki – czego się spodziewać

Po uruchomieniu programu otwórz dowolny plik w `YOUR_DIRECTORY/OcrResults`. Powinieneś zobaczyć zwykły tekst wyodrębniony z odpowiadającego obrazu, na przykład:

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Jeśli wynik wygląda na zniekształcony, sprawdź ponownie, czy `Language` odpowiada językowi Twoich skanów. Aspose OCR obsługuje ponad 100 języków, więc możesz zamienić `OcrLanguage.Spanish` na dowolny potrzebny.

## Obsługa przypadków brzegowych i typowe pułapki

### 1. Brak dostępnego GPU

Jeśli Twoja maszyna nie ma kompatybilnego GPU, `UseGpu = true` cicho przełączy się na tryb CPU, ale utracisz przyspieszenie. Aby być explicite, możesz wykryć możliwości GPU:

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Duże pliki przekraczające pamięć

Przy pracy z ogromnymi plikami TIFF lub PDF rozważ wstępne podzielenie ich na mniejsze obrazy. Aspose OCR radzi sobie z wielostronicowymi PDF‑ami, ale zużycie pamięci rośnie wraz z liczbą stron. Prosty krok wstępnego przetwarzania przy użyciu `Aspose.Imaging` może podzielić dokument na poręczne fragmenty.

### 3. Pliki nie‑obrazowe w folderze wejściowym

Procesor wsadowy ignoruje pliki, których nie potrafi sparsować, ale dobrą praktyką jest utrzymanie folderu w czystości. Możesz filtrować po rozszerzeniu:

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Uwaga: `FileFilter` to hipotetyczna właściwość; zamień ją na rzeczywiste API, jeśli jest dostępne.)*

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania program. Zamień `YOUR_DIRECTORY` na absolutną ścieżkę na swoim komputerze.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Oczekiwany wynik w konsoli

```
Batch completed.
```

A w `C:\OcrResults` znajdziesz plik `.txt` dla każdego obrazu w `C:\MyScans`.

## Zakończenie

Masz teraz solidny, gotowy do produkcji sposób na **jak wykonać wsadowe OCR** w C# i **wyodrębnić tekst ze skanów** bez ręcznego otwierania każdego pliku. Dzięki wykorzystaniu batch API Aspose, przyspieszeniu GPU i konfigurowalnej równoległości rozwiązanie skaluje się od kilku stron do tysięcy.

Co dalej? Wypróbuj te pomysły:

- **Zintegruj z indeksem wyszukiwania** (np. Elasticsearch), aby wyodrębniony tekst był przeszukiwalny.
- **Dodaj przetwarzanie końcowe** takie jak sprawdzanie pisowni lub wykrywanie języka.
- **Opakuj aplikację konsolową w usługę Windows** w celu ciągłego monitorowania folderu docelowego.

Śmiało eksperymentuj, dostosowuj poziom równoległości lub zmieniaj model językowy. Jeśli napotkasz problemy, zostaw komentarz poniżej — powodzenia w OCR‑owaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}