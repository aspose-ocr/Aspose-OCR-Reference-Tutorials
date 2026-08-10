---
category: general
date: 2026-02-27
description: Aspose OCR GPU umożliwia szybkie rozpoznawanie tekstu przy użyciu GPU
  w C#. Dowiedz się krok po kroku, jak skonfigurować, uruchomić i zweryfikować OCR
  z przyspieszeniem GPU.
draft: false
keywords:
- aspose ocr gpu
- gpu text recognition
- aspose ocr c#
- ocr gpu acceleration
- high‑resolution OCR
language: pl
og_description: Aspose OCR GPU umożliwia szybkie rozpoznawanie tekstu na GPU w C#.
  Skorzystaj z tego kompletnego przewodnika, aby uruchomić się w kilka minut.
og_title: 'Aspose OCR GPU: Szybkie rozpoznawanie tekstu w C#'
tags:
- Aspose
- OCR
- C#
- GPU
title: 'Aspose OCR GPU: Szybkie rozpoznawanie tekstu w C#'
url: /pl/net/ocr-optimization/aspose-ocr-gpu-fast-text-recognition-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU: Szybkie rozpoznawanie tekstu w C#

Zastanawiałeś się kiedyś, jak sprawić, by Twój potok OCR działał z prędkością GPU? **Aspose OCR GPU** sprawia, że rozpoznawanie tekstu na GPU o wysokiej przepustowości jest dziecinnie proste dla każdego programisty .NET. W tym samouczku uruchomimy silnik Aspose OCR, włączymy przyspieszenie GPU i wyodrębnimy tekst z ogromnego zeskanowanego pliku TIFF — wszystko w kilku zwięzłych krokach.

Omówimy wszystko, co musisz wiedzieć: wymagane pakiety NuGet, obsługę awaryjną, gdy GPU nie jest dostępne, oraz wskazówki dotyczące optymalizacji wydajności przy dużych obrazach. Po zakończeniu będziesz mieć działającą aplikację konsolową, która wypisuje liczbę znaków rozpoznanego tekstu, oraz zrozumiesz **dlaczego** każda linia kodu ma znaczenie.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa również na .NET Core i .NET Framework)  
- Visual Studio 2022 lub dowolne IDE, które preferujesz  
- Karta graficzna NVIDIA z CUDA 11+ (opcjonalnie – silnik automatycznie przełącza się na CPU)  
- Pakiety NuGet Aspose.OCR i Aspose.OCR.Gpu  

Jeśli nie masz GPU, nie panikuj – przykład nadal działa, choć nieco wolniej.

## Krok 1: Zainicjalizuj silnik Aspose OCR GPU

Pierwszą rzeczą, którą robimy, jest utworzenie instancji `OcrEngine` i poinformowanie jej, że chcemy używać GPU. Flaga `EnableGpu` wewnętrznie sprawdza dostępność kompatybilnego urządzenia; jeśli nie zostanie znalezione, cicho przełącza się w tryb CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class Program
{
    static void Main()
    {
        // Step 1 – create the OCR engine with GPU enabled
        var ocrEngine = new OcrEngine
        {
            EnableGpu = true               // true → try GPU first, fallback to CPU if unavailable
        };
```

**Dlaczego to ważne:** Włączenie GPU może zaoszczędzić sekundy (a nawet minuty) czasu przetwarzania przy skanach wysokiej rozdzielczości. Mechanizm awaryjny zapobiega poważnym awariom na systemach bez sterowników CUDA.

> **Wskazówka:** Wywołaj `OcrEngine.IsGpuAvailable` po konstrukcji, jeśli chcesz zalogować, czy GPU zostało faktycznie użyte.

## Krok 2: Wybierz język rozpoznawania

Aspose OCR obsługuje dziesiątki języków, ale musisz ustawić ten, którego oczekujesz na obrazie. Tutaj pozostajemy przy języku angielskim, który obejmuje większość dokumentów biznesowych.

```csharp
        // Step 2 – set the language (English in this example)
        ocrEngine.Language = OcrLanguage.English;
```

**Dlaczego to ważne:** Określenie języka zawęża zestaw znaków, którego silnik szuka, zwiększając zarówno szybkość, jak i dokładność. Jeśli potrzebujesz obsługi wielu języków, możesz przekazać listę oddzieloną przecinkami, np. `OcrLanguage.English | OcrLanguage.Spanish`.

## Krok 3: Uruchom rozpoznawanie tekstu na GPU na dużym obrazie

Teraz przekazujemy silnikowi plik TIFF o wysokiej rozdzielczości. Metoda `RecognizeFromFile` zwraca zwykły ciąg znaków ze wszystkimi wykrytymi znakami.

```csharp
        // Step 3 – recognize text from a high‑resolution scanned image
        string imagePath = @"YOUR_DIRECTORY\large_page.tif";

        // Wrap the call in a try/catch to handle possible I/O issues
        string recognizedText;
        try
        {
            recognizedText = ocrEngine.RecognizeFromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            return;
        }
```

**Dlaczego to ważne:** Metoda `RecognizeFromFile` automatycznie używa GPU, jeśli `EnableGpu` zakończyło się sukcesem. Dla ogromnych plików (10 000 × 10 000 px lub większych) równoległość GPU błyszczy, zamieniając potencjalnie minutową pracę CPU w kilka sekund.

> **Przypadek brzegowy:** Jeśli Twój obraz jest większy niż pamięć VRAM GPU, silnik podzieli pracę na kafelki i przetworzy je kolejno. Ta awaryjna metoda jest przejrzysta, ale możesz kontrolować rozmiar kafelka za pomocą `OcrEngine.GpuOptions.TileSize`.

## Krok 4: Zweryfikuj wynik i obsłuż awarie

Po zakończeniu OCR po prostu wypisujemy długość rozpoznanego ciągu znaków. W rzeczywistym projekcie prawdopodobnie zapiszesz tekst do pliku lub przekażesz go do dalszej logiki.

```csharp
        // Step 4 – display a short summary of the result
        Console.WriteLine($"GPU OCR completed. Characters recognized: {recognizedText.Length}");
        // Optional: write the full text to a file for later inspection
        System.IO.File.WriteAllText("recognized_output.txt", recognizedText);
    }
}
```

**Dlaczego to ważne:** Znajomość liczby znaków pozwala szybko zweryfikować, że silnik rzeczywiście przetworzył obraz. Jeśli liczba jest podejrzanie niska, możesz mieć do czynienia z przejściem na CPU na słabym komputerze lub nieobsługiwanym formacie obrazu.

### Szybka kontrola poprawności

Uruchom program z znanym przykładem (np. stroną wydrukowanego tekstu). Powinieneś zobaczyć wyjście podobne do:

```
GPU OCR completed. Characters recognized: 4872
```

Jeśli liczba jest znacznie niższa, sprawdź ponownie, czy ścieżka do obrazu jest poprawna i czy sterowniki GPU są aktualne.

## Opcjonalnie: Sprawdź, czy GPU zostało użyte

Czasami potrzebne jest wyraźne potwierdzenie, że GPU zostało użyte. Poniższy fragment kodu wypisuje tryb:

```csharp
        // After recognition, query the runtime mode
        string mode = ocrEngine.IsGpuEnabled ? "GPU" : "CPU";
        Console.WriteLine($"Recognition performed on: {mode}");
```

**Dlaczego to ważne:** W pipeline'ach CI lub środowiskach chmurowych możesz nie mieć GPU, a ten wpis w logu pomaga wykryć regresje wydajności.

## Typowe pułapki i jak ich uniknąć

| Pułapka | Co się dzieje | Rozwiązanie |
|---------|--------------|-----|
| **Brak sterownika CUDA** | `EnableGpu` cicho przełącza się na CPU, ale możesz sądzić, że używasz GPU. | Wywołaj `OcrEngine.IsGpuAvailable` i zaloguj wynik. |
| **Brak pamięci na GPU** | Duże obrazy powodują `CudaException`. | Zmniejsz rozdzielczość obrazu lub zwiększ `GpuOptions.TileSize`. |
| **Nieprawidłowy kod języka** | OCR zwraca zniekształcone znaki. | Sprawdź, czy wyliczenie `OcrLanguage` odpowiada językowi dokumentu. |
| **Błąd w ścieżce pliku** | `FileNotFoundException`. | Użyj `Path.Combine` i zweryfikuj za pomocą `File.Exists`. |

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się kompletny program, gotowy do wstawienia w nowym projekcie konsolowym.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with GPU support (fallback to CPU if needed)
        var ocrEngine = new OcrEngine
        {
            EnableGpu = true
        };

        // Choose the language for recognition
        ocrEngine.Language = OcrLanguage.English;

        // Path to the high‑resolution image
        string imagePath = @"YOUR_DIRECTORY\large_page.tif";

        // Perform OCR and capture any errors
        string recognizedText;
        try
        {
            recognizedText = ocrEngine.RecognizeFromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            return;
        }

        // Output a concise summary
        Console.WriteLine($"GPU OCR completed. Characters recognized: {recognizedText.Length}");

        // Optional: write full text to a file
        System.IO.File.WriteAllText("recognized_output.txt", recognizedText);

        // Show which processing mode was actually used
        string mode = ocrEngine.IsGpuEnabled ? "GPU" : "CPU";
        Console.WriteLine($"Recognition performed on: {mode}");
    }
}
```

Zapisz to jako `Program.cs`, przywróć pakiety NuGet (`dotnet add package Aspose.OCR` oraz `dotnet add package Aspose.OCR.Gpu`), i uruchom `dotnet run`. Powinieneś zobaczyć liczbę znaków oraz tryb (GPU/CPU) wypisany w konsoli.

## Podsumowanie wizualne

![Przykład Aspose OCR GPU pokazujący wyjście konsoli z liczbą znaków](aspose-ocr-gpu-example.png "aspose ocr gpu")

*Tekst alternatywny obrazu zawiera główne słowo kluczowe dla SEO.*

## Podsumowanie

Właśnie nauczyłeś się wykorzystywać **Aspose OCR GPU** do błyskawicznego *gpu text recognition* w C#. Inicjalizując silnik za pomocą `EnableGpu`, wybierając odpowiedni język i obsługując scenariusze awaryjne, otrzymujesz solidne rozwiązanie, które działa niezależnie od tego, czy karta graficzna jest obecna.

From here you might explore:

- **Przetwarzanie wsadowe** dziesiątek plików TIFF przy użyciu `Parallel.ForEach` (wciąż bezpieczne, ponieważ silnik jest świadomy wątków).  
- **Niestandardowe słowniki OCR** dla słownictwa specyficznego dla domeny.  
- **Dostosowywanie pamięci GPU** za pomocą `OcrEngine.GpuOptions` dla ekstremalnie dużych skanów.  

Wypróbuj kod, dostosuj opcje i obserwuj, jak rośnie wydajność Twojego OCR. Miłego kodowania i zachęcam do zostawienia komentarza, jeśli napotkasz jakiekolwiek problemy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}