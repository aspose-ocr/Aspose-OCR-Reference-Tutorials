---
category: general
date: 2026-01-01
description: Jak wykonywać OCR wsadowo przy użyciu silnika Aspose OCR w C#. Dowiedz
  się, jak rozpoznawać tekst z obrazów i wyodrębniać tekst z plików TIFF przy użyciu
  przyspieszenia GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: pl
og_description: Jak wykonywać OCR wsadowo w C# przy użyciu silnika Aspose OCR. Ten
  przewodnik pokazuje, jak rozpoznawać tekst z obrazów i efektywnie wyodrębniać tekst
  z plików TIFF.
og_title: Jak wykonać wsadowe OCR w C# – Kompletny przewodnik Aspose
tags:
- OCR
- C#
- Aspose
- GPU
title: Jak przeprowadzić wsadowe OCR w C# przy użyciu silnika Aspose OCR
url: /pl/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonywać OCR wsadowo w C# przy użyciu silnika Aspose OCR Engine

Zastanawiałeś się kiedyś **jak wykonywać OCR wsadowo**, gdy masz dziesiątki zeskanowanych dokumentów leżących w folderze? Nie jesteś sam — wielu programistów napotyka ten problem, przechodząc od rozpoznawania pojedynczych obrazów do przetwarzania całej kolekcji. Dobra wiadomość jest taka, że Aspose OCR sprawia, że to bułka z masłem, niezależnie od tego, czy działasz na CPU, czy korzystasz z przyspieszenia GPU.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **rozpoznaje tekst z obrazów** i nawet **wyodrębnia tekst z plików TIFF** hurtowo. Bez niejasnych skrótów typu „zobacz dokumentację” — po prostu samodzielne rozwiązanie, które możesz skopiować‑wkleić i uruchomić już dziś.

## Wymagania wstępne

* .NET 6.0 lub nowszy zainstalowany (kod jest skierowany na .NET 6, ale .NET 5 również działa).
* Pakiet NuGet Aspose.OCR dla .NET (dostępne wersje CPU i GPU; zainstaluj tę, która pasuje do Twojego sprzętu).
* Folder z kilkoma przykładowymi plikami TIFF lub PNG, które chcesz przetworzyć.
* Visual Studio 2022 lub dowolne IDE, którego używasz.

> **Porada:** Jeśli planujesz używać wersji GPU, upewnij się, że sterownik graficzny jest aktualny i że zainstalowano CUDA 11+. Silnik automatycznie przełączy się na CPU, jeśli nie znajdzie kompatybilnego GPU.

## Krok 1 – Konfiguracja projektu i instalacja Aspose.OCR

### H2: Utwórz nową aplikację konsolową i dodaj Aspose.OCR

Otwórz terminal (lub konsolę Package Manager w Visual Studio) i uruchom:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Jeśli masz licencję z obsługą GPU, zamiast tego dodaj pakiet GPU:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Gotowe — Twój projekt teraz odwołuje się do biblioteki OCR, której użyjemy do **wsadowego OCR**.

## Krok 2 – Inicjalizacja silnika OCR (CPU lub GPU)

### H2: Jak wykonywać OCR wsadowo – Inicjalizacja silnika

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Dlaczego to ważne:** Przełączając `UseGpu`, pozwalasz Aspose wybrać najszybszą ścieżkę. Jeśli GPU nie jest dostępne, silnik cicho przełącza się z powrotem na CPU, więc Twoje zadanie wsadowe nigdy nie zawiedzie z powodu brakującego sprzętu.

## Krok 3 – Zbierz pliki, które chcesz przetworzyć

### H2: Rozpoznawanie tekstu z obrazów – Tworzenie listy plików

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Uwaga o przypadkach brzegowych:** Jeśli masz mieszankę formatów, zmień wzorzec wyszukiwania na `"*.*"` i filtruj po rozszerzeniu wewnątrz pętli. To utrzymuje elastyczność wsadu.

## Krok 4 – Przetwarzaj każdy obraz i pokaż podgląd

### H2: Wyodrębnianie tekstu z TIFF – Pętla po plikach

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Co zobaczysz:** Dla każdego TIFF, konsola wypisuje coś w rodzaju:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Ten podgląd potwierdza, że wsad zakończył się sukcesem, bez konieczności ręcznego otwierania każdego pliku.

## Krok 5 – Zapisz wyniki (opcjonalnie, ale przydatne)

### H3: Zachowaj wynik OCR w plikach tekstowych

Jeśli potrzebujesz pełnego tekstu do dalszego przetwarzania, dodaj to wewnątrz pętli `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Teraz każdy TIFF otrzymuje towarzyszący plik `.txt` zawierający pełny wynik OCR — idealny do indeksowania, wyszukiwania lub podawania do modelu językowego.

## Krok 6 – Uruchom demo i zweryfikuj

1. Zbuduj projekt: `dotnet build`.
2. Uruchom: `dotnet run --project GpuBatchDemo.csproj`.

Powinieneś zobaczyć linie podglądu wypisane w konsoli oraz (jeśli dodałeś opcjonalny krok) serię plików `.txt` obok Twoich obrazów źródłowych.

### H3: Typowe pułapki i jak je naprawić

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| **Pusty `ocrResult.Text`** | Obraz zbyt ciemny lub o niskiej rozdzielczości DPI | Wstępnie przetwórz obrazy (zwiększ kontrast, skaluj) lub ustaw `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Nieaktualny sterownik | Zaktualizuj sterownik GPU lub ustaw `UseGpu = false`, aby wymusić CPU. |
| **Exception “File not found”** | Nieprawidłowy separator ścieżki w Linux/macOS | Użyj `Path.Combine` lub ukośników (`/`). |

## Krok 7 – Skalowanie (poza kilkoma plikami)

When you move from a handful of TIFFs to thousands, consider:

* **Parallel processing:** Owiń `foreach` w `Parallel.ForEach` (upewnij się, że instancja silnika jest bezpieczna wątkowo; w przeciwnym razie utwórz jedną na wątek).
* **Chunked I/O:** Czytaj obrazy w partiach, aby nie wyczerpać pamięci RAM.
* **Logging:** Zapisuj postęp do pliku logu; pomaga to wznowić po awarii.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Pamiętaj:** Pamięć GPU jest współdzielona, więc uruchamianie zbyt wielu równoległych zadań GPU może faktycznie spowolnić działanie. Przetestuj najpierw kilka wątków.

## Pełny działający przykład (gotowy do kopiowania‑wklejania)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Uruchomienie tego programu **rozpozna tekst z obrazów**, **wyodrębni tekst z TIFF** i pokaże **jak wykonywać OCR wsadowo** efektywnie.

## Zakończenie

Masz teraz solidny, kompleksowy przykład **jak wykonywać OCR wsadowo** w C# przy użyciu silnika OCR od Aspose. Samouczek obejmował wszystko, od konfiguracji projektu, przełączania przyspieszenia GPU, budowania listy plików, przetwarzania każdego obrazu, po zachowywanie wyników. Niezależnie od tego, czy wyodrębniasz tekst z plików TIFF, czy z innego formatu obrazu, ten sam schemat ma zastosowanie — wystarczy zamienić rozszerzenia plików.

Gotowy na kolejny krok? Spróbuj zintegrować wynik OCR z indeksem wyszukiwania, podać tekst do dużego modelu językowego lub poeksperymentować z przetwarzaniem równoległym, aby zaoszczędzić minuty przy masowych wsadach. Nie ma granic, a Ty masz już fundament, na którym możesz budować.

Masz pytania lub chcesz podzielić się własnymi trikami dotyczącymi OCR wsadowego? zostaw komentarz poniżej — szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}