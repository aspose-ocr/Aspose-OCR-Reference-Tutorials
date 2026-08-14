---
category: general
date: 2026-02-20
description: Jak wykonać OCR na plikach DjVu w C#. Dowiedz się, jak rozpoznawać tekst
  z obrazu i szybko konwertować DjVu na tekst przy użyciu Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: pl
og_description: Jak przeprowadzić OCR na plikach DjVu w C#. Ten samouczek pokazuje,
  jak rozpoznawać tekst z obrazu, odczytywać DjVu i konwertować DjVu na tekst przy
  użyciu Aspose OCR.
og_title: Jak wykonać OCR w plikach DjVu w C# – Kompletny przewodnik
tags:
- OCR
- C#
- DjVu
- Aspose
title: Jak wykonać OCR w plikach DjVu w C# – Przewodnik krok po kroku
url: /pl/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR na plikach DjVu w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak wykonać OCR** na dokumencie DjVu, nie tracąc przy tym włosów? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy muszą **rozpoznać tekst z obrazu** znajdującego się w kontenerach DjVu. Dobra wiadomość? Kilka linijek C# i biblioteka Aspose OCR pozwolą Ci w mig wyodrębnić ukryty tekst.

W tym tutorialu przejdziemy krok po kroku przez wszystko, co potrzebne, aby zamienić stronę DjVu w zwykły tekst. Po zakończeniu będziesz wiedział **jak odczytać DjVu**, **jak wyodrębnić tekst z obrazu** oraz **jak przekonwertować DjVu na tekst** do dalszego przetwarzania. Bez zewnętrznych usług, bez niejasnych odwołań — tylko samodzielny, gotowy do uruchomienia przykład.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz pod ręką:

- .NET 6.0 SDK lub nowszy (kod działa także z .NET Framework 4.8).
- Visual Studio 2022 lub dowolny edytor obsługujący C#.
- Licencję Aspose OCR for .NET (bezpłatna wersja próbna wystarczy do testów).
- Przykładowy plik DjVu (`sample.djvu`) umieszczony w folderze, do którego możesz odwołać się w kodzie.

Posiadanie tych elementów zapewni płynny przebieg — bez niespodziewanych „brakujących referencji”.

## Jak wykonać OCR na stronie DjVu

Podstawowa idea jest prosta: wczytaj stronę DjVu jako obraz, przekaż go silnikowi OCR i odczytaj zwrócony ciąg znaków. Rozbijmy to na poszczególne kroki.

### Krok 1: Zainstaluj Aspose OCR

Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.OCR
```

Spowoduje to pobranie najnowszych binarek Aspose OCR oraz ich zależności. Jeśli wolisz interfejs UI Menedżera Pakietów NuGet, po prostu wyszukaj **Aspose.OCR** i kliknij **Install**.

### Krok 2: Zainicjalizuj silnik OCR

Utworzenie instancji `OcrEngine` to pierwsza rzecz, którą robisz, gdy chcesz **wykonać OCR**. Pomyśl o tym jak o włączeniu „mózgu” skanera.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Ponowne użycie jednego `OcrEngine` dla wielu stron oszczędza pamięć i przyspiesza przetwarzanie.

### Krok 3: Wczytaj stronę DjVu jako obraz

Pliki DjVu nie są bezpośrednio obsługiwane przez większość API obrazów, ale Aspose może traktować każdą stronę jako bitmapę. Tutaj używamy `System.Drawing.Image`, aby odczytać plik.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Dlaczego to działa:** `Image.FromFile` automatycznie dekoduje strumień DjVu do formatu rastrowego, który rozumie silnik OCR. Jeśli musisz przetworzyć konkretną stronę z wielostronicowego DjVu, użyj Aspose PDF lub Aspose Imaging, aby najpierw wyodrębnić tę stronę.

### Krok 4: Rozpoznaj tekst z obrazu

Teraz dzieje się magia. Metoda `Recognize` skanuje bitmapę i zwraca ciąg znaków zawierający wykryte litery.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

W tym momencie **rozpoznałeś tekst z obrazu**, który pierwotnie znajdował się w kontenerze DjVu. Ciąg może zawierać podziały linii, interpunkcję, a nawet znaki Unicode, jeśli język źródłowy je obsługuje.

### Krok 5: Wyświetl lub zapisz wynik

Na szybki test po prostu wypisz tekst w konsoli. W rzeczywistej aplikacji prawdopodobnie zapiszesz go do pliku lub bazy danych.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Oczekiwany wynik** (skrócony dla przejrzystości):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Jeśli zobaczysz nieczytelne znaki, sprawdź, czy plik DjVu nie jest zaszyfrowany oraz czy ustawiłeś prawidłowy język w `ocrEngine.Language`. Domyślnie przyjmuje angielski; możesz przełączyć na francuski, niemiecki itp., przypisując `ocrEngine.Language = Language.French;`.

## Rozpoznawanie tekstu z obrazu – typowe pułapki

Nawet przy solidnym przykładzie programiści często natrafiają na kilka przypadków brzegowych:

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Pusty wynik** | Rozdzielczość obrazu jest zbyt niska (<300 dpi). | Ustaw `ocrEngine.ImageResolution = 300;` przed wywołaniem `Recognize`. |
| **Zły język** | OCR domyślnie używa angielskiego. | Ustaw `ocrEngine.Language = Language.Spanish;` (lub dowolny obsługiwany język). |
| **Wycieki pamięci** | Duże strony DjVu pozostają w pamięci po przetworzeniu. | Wywołaj `djvuPage.Dispose();` po zakończeniu. |
| **Wielostronicowy DjVu** | Ładowana jest tylko pierwsza strona. | Iteruj po stronach używając klasy `DjvuImage` z Aspose Imaging. |

Rozwiązanie tych problemów na wczesnym etapie oszczędza mnóstwo godzin debugowania.

## Jak odczytać pliki DjVu w C# – poza prostym OCR

Jeśli Twój projekt wymaga więcej niż jednej strony, najpierw musisz wyodrębnić każdą stronę jako obraz. Aspose Imaging ułatwia to zadanie:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Ten wzorzec pozwala **konwertować DjVu na tekst** strona po stronie, idealny do przetwarzania wsadowego dużych archiwów.

## Wyodrębnianie tekstu z obrazu – dopasowanie dokładności

Domyślne ustawienia OCR działają dobrze przy czystych skanach, ale możesz zwiększyć dokładność:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Te drobne zmiany są szczególnie przydatne, gdy źródło DjVu zawiera odręczne notatki lub grafiki o niskim kontraście.

## Konwersja DjVu na tekst – pełny przykład end‑to‑end

Poniżej znajduje się kompaktowa wersja, która łączy wszystko: wczytywanie wielostronicowego DjVu, wstępne przetwarzanie każdej strony, wykonywanie OCR i zapisywanie wyniku do pliku `.txt`.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

Uruchomienie tego skryptu tworzy `sample_extracted.txt` z zawartością każdej strony oddzieloną w przejrzysty sposób. To najszybszy sposób na **konwersję DjVu na tekst** w celu indeksowania, wyszukiwania lub archiwizacji.

## Podsumowanie

Omówiliśmy **jak wykonać OCR** na plikach DjVu od początku do końca, przedstawiliśmy sposoby **rozpoznawania tekstu z obrazu** oraz **konwersji DjVu na tekst**. Teraz masz wszystkie niezbędne narzędzia, aby efektywnie przetwarzać dokumenty DjVu w swoich aplikacjach.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}