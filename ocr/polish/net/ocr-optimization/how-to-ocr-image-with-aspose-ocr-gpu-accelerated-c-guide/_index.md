---
category: general
date: 2026-02-17
description: Dowiedz się, jak przeprowadzić OCR obrazu przy użyciu Aspose OCR na GPU.
  Krok po kroku kod rozpoznający tekst z obrazu, ładowanie obrazu wysokiej rozdzielczości,
  ustawianie identyfikatora urządzenia GPU i wyodrębnianie tekstu przy użyciu Aspose.
draft: false
keywords:
- how to ocr image
- recognize text from image
- load high resolution image
- set gpu device id
- extract text using aspose
language: pl
og_description: Jak wykonać OCR obrazu przy użyciu Aspose OCR na GPU. Śledź kompletny
  samouczek C#, aby rozpoznać tekst z obrazu, załadować obraz o wysokiej rozdzielczości,
  ustawić identyfikator urządzenia GPU i wyodrębnić tekst za pomocą Aspose.
og_title: Jak wykonać OCR obrazu przy użyciu Aspose OCR – przewodnik C# przyspieszony
  GPU
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Jak wykonać OCR obrazu przy użyciu Aspose OCR – przewodnik C# przyspieszony
  GPU
url: /pl/net/ocr-optimization/how-to-ocr-image-with-aspose-ocr-gpu-accelerated-c-guide/
---

produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR obrazu przy użyciu Aspose OCR – przewodnik przyspieszony GPU w C#

Zastanawiałeś się kiedyś **jak wykonać OCR obrazu**, gdy plik jest ogromnym skanem 300 DPI i potrzebujesz wyników w kilka sekund? Nie jesteś sam — programiści nieustannie walczą z wolnymi silnikami OCR działającymi wyłącznie na CPU, szczególnie przy obrazach wysokiej rozdzielczości. Dobra wiadomość? Aspose OCR pozwala wykorzystać GPU, dramatycznie skracając czas przetwarzania przy zachowaniu wysokiej dokładności.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **rozpoznaje tekst z obrazu**, pokazuje, jak **załadować obraz wysokiej rozdzielczości**, pozwala **ustawić identyfikator urządzenia GPU**, a na końcu **wyodrębnić tekst przy użyciu Aspose**. Po zakończeniu będziesz mieć samodzielny program, który możesz wkleić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod działa również na .NET Framework 4.7+)
- **Aspose.OCR for .NET** pakiet NuGet (wersja 23.11 lub nowsza)
- Maszyna z obsługą GPU i CUDA 11+ (opcjonalnie, ale zalecane)
- Obraz JPEG/PNG wysokiej rozdzielczości, który chcesz poddać OCR (np. `highres_scan.jpg`)

Jeśli brakuje Ci któregoś z powyższych, pobierz pakiet NuGet za pomocą:

```bash
dotnet add package Aspose.OCR
```

Nie są wymagane dodatkowe biblioteki natywne; Aspose dołącza środowisko uruchomieniowe CUDA za Ciebie.

![diagram jak wykonać OCR obrazu](image-placeholder.png "Diagram ilustrujący przyspieszoną GPU pipeline OCR – jak wykonać OCR obrazu")

## Krok 1: Utwórz silnik OCR i ustaw identyfikator urządzenia GPU  

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie Aspose, aby działał na GPU. To właśnie **set GPU device ID** wchodzi w grę — jeśli masz wiele GPU, możesz wybrać to, które najlepiej pasuje do Twojego obciążenia.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine with GPU processing mode
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    ProcessingMode = ProcessingMode.Gpu, // Enable GPU acceleration
    GpuDeviceId = 0                     // Choose GPU #0 (change if you have several)
});
```

> **Dlaczego to ważne:** Przetwarzanie na GPU odciąża ciężką pracę analizy obrazu do równoległych rdzeni, dając przyspieszenie 3‑5× w typowych skanach. Jeśli nie ustawisz `GpuDeviceId`, Aspose domyślnie użyje pierwszego urządzenia, co jest w porządku przy jednowyposażonych w GPU systemach.

## Krok 2: Załaduj obraz wysokiej rozdzielczości  

Następnie **load high resolution image** dane w formacie, który rozumie silnik OCR. Aspose udostępnia `ImageStream.FromFile`, który odczytuje plik do pamięci bez niepotrzebnych konwersji.

```csharp
// Path to your high‑resolution scan (300 DPI or more)
string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";

// Load the image; ImageStream handles large files efficiently
var image = ImageStream.FromFile(imagePath);
```

> **Wskazówka:** Jeśli Twój obraz znajduje się w chmurze, możesz również podać bezpośrednio `Stream` — po prostu zamień `FromFile` na `FromStream(yourStream)`. Silnik nadal potraktuje go jako źródło wysokiej rozdzielczości.

## Krok 3: Rozpoznaj tekst z obrazu  

Teraz, gdy silnik jest gotowy, a obraz załadowany, możemy **recognize text from image**. Metoda `Recognize` zwraca obiekt `OcrResult` zawierający czysty tekst, wyniki pewności oraz ewentualne ramki ograniczające, jeśli będą potrzebne później.

```csharp
// Perform OCR; this call is where the GPU does its magic
OcrResult recognitionResult = ocrEngine.Recognize(image);

// For debugging, you can also inspect recognitionResult.Regions
```

> **Przypadek brzegowy:** Jeśli obraz jest zbyt ciemny lub zawiera dużo szumu, rozważ wstępne przetworzenie (np. zwiększenie kontrastu) przed wywołaniem `Recognize`. Aspose oferuje API `Preprocess`, ale w większości czystych skanów domyślne ustawienia działają dobrze.

## Krok 4: Wyodrębnij tekst przy użyciu Aspose i wyświetl go  

Na koniec **extract text using Aspose** po prostu odczytując właściwość `Text` wyniku. Wypiszmy go w konsoli, ale możesz również zapisać do pliku lub bazy danych.

```csharp
// Output the plain‑text result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognitionResult.Text);
```

**Oczekiwany wynik** (przykład dla zeskanowanej faktury):

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,254.00
Thank you for your business!
```

Jeśli zobaczysz zniekształcone znaki, sprawdź ponownie, czy obraz jest naprawdę wysokiej rozdzielczości oraz czy poprawny język jest ustawiony w `OcrEngineSettings` (np. `Language = Language.English`).

## Pełny działający przykład  

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego:

```csharp
// ------------------------------------------------------------
// Full OCR example – Aspose OCR with GPU acceleration
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            ProcessingMode = ProcessingMode.Gpu, // GPU acceleration
            GpuDeviceId = 0                      // Change if you have multiple GPUs
        });

        // 2️⃣ Load a high‑resolution image
        string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";
        var image = ImageStream.FromFile(imagePath);

        // 3️⃣ Recognize text from the image
        OcrResult result = ocrEngine.Recognize(image);

        // 4️⃣ Extract and display the plain text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

Uruchom program poleceniem `dotnet run`. Na przyzwoitym GPU powinieneś zobaczyć wynik OCR w mniej niż sekundę, nawet dla skanu 5 MB, 300 DPI.

## Częste pytania i wskazówki profesjonalne  

### Co zrobić, jeśli nie mam GPU?  
Możesz nadal używać Aspose OCR na CPU, ustawiając `ProcessingMode = ProcessingMode.Cpu`. API pozostaje identyczne; zmienia się tylko wydajność.

### Jak obsługiwać wiele języków?  
Dodaj `Language = Language.Multilingual` (lub konkretny enum, np. `Language.French`) wewnątrz `OcrEngineSettings`. Aspose automatycznie załaduje odpowiednie pakiety językowe.

### Czy mogę przetwarzać PDF‑y bezpośrednio?  
Tak — Aspose OCR może najpierw wyodrębnić obrazy z PDF‑ów, a następnie wykonać OCR na każdej stronie. Połącz `Aspose.PDF` z tym samym `OcrEngine`, aby uzyskać płynną pipeline.

### Kiedy powinienem dostosować `GpuDeviceId`?  
Jeśli Twój serwer obsługuje jednocześnie przetwarzanie obrazów i zadania uczenia maszynowego, możesz przeznaczyć GPU 1 do OCR (`GpuDeviceId = 1`) i zostawić GPU 0 wolne dla zadań inferencyjnych.

### Jak poprawić dokładność przy szumnych skanach?  
Wstępnie przetwórz obraz:  
```csharp
image = image.AdjustContrast(1.2f).ApplyThreshold(0.5f);
```
Te metody są częścią narzędzi przetwarzania obrazu Aspose.

## Zakończenie  

Teraz wiesz **jak wykonać OCR obrazu** przy użyciu Aspose OCR z przyspieszeniem GPU, **jak rozpoznawać tekst z obrazu**, **jak prawidłowo załadować obraz wysokiej rozdzielczości**, **jak ustawić identyfikator urządzenia GPU**, oraz **jak wyodrębnić tekst przy użyciu Aspose** w czystym, gotowym do produkcji programie C#.  

Wypróbuj kod na kilku różnych plikach — spróbuj rozmazanego paragonu, błyszczącej ulotki lub nawet odręcznej notatki. Eksperymentuj z ustawieniami języka i krokami wstępnego przetwarzania, aby zobaczyć, jak zmienia się dokładność.  

Następnie możesz zbadać **batch processing** (pętla po folderze skanów) lub zintegrować wynik OCR z **indeksem wyszukiwania** dla szybkiego odnajdywania dokumentów. Oba tematy naturalnie rozwijają koncepcje przedstawione w tym przewodniku i są doskonałymi projektami następnymi.

Powodzenia w kodowaniu i niech Twoje pipeline’y OCR będą szybkie i bezbłędne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}