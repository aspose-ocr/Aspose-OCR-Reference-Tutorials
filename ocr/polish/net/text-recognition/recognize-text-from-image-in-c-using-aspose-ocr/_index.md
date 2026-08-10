---
category: general
date: 2026-05-31
description: Dowiedz się, jak rozpoznawać tekst z obrazu w C# przy użyciu Aspose OCR,
  w tym jak wyodrębniać tekst z plików TIFF i efektywnie ładować obraz do OCR.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: pl
og_description: Przewodnik krok po kroku, jak rozpoznawać tekst z obrazu przy użyciu
  Aspose OCR, obejmujący ekstrakcję z plików TIFF oraz prawidłowe ładowanie obrazu
  do OCR.
og_title: Rozpoznawanie tekstu z obrazu w C# przy użyciu Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: rozpoznawanie tekstu z obrazu w C# przy użyciu Aspose OCR
url: /pl/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z obrazu w C# przy użyciu Aspose OCR

Kiedykolwiek potrzebowałeś **rozpoznać tekst z obrazu**, ale nie wiedziałeś, od czego zacząć w C#? Nie jesteś sam — wielu programistów napotyka ten problem przy pracy ze skanowanymi dokumentami lub wielostronicowymi plikami TIFF. W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **rozpoznaje tekst z obrazu** przy użyciu biblioteki Aspose OCR, a także pokażemy, jak **wyodrębnić tekst z tiff** i najlepszy sposób na **załadowanie obrazu do OCR** bez utraty włosów.

Omówimy wszystko, od instalacji pakietu NuGet po obsługę przyspieszenia GPU i przejście na CPU w razie potrzeby. Po zakończeniu tego tutorialu będziesz mieć aplikację konsolową, która wypisuje rozpoznany tekst oraz czas przetwarzania — bez brakujących elementów, bez niejasnych odniesień.

## Co zbudujesz

- Prostą aplikację konsolową .NET, która ładuje obraz (w tym wielostronicowy TIFF)  
- Silnik OCR skonfigurowany do użycia GPU, z eleganckim przejściem na CPU  
- Wyodrębnienie czystego tekstu z obrazu, wypisane w konsoli  
- Informacje o czasie, abyś mógł zobaczyć wpływ wydajności GPU vs. CPU  

**Wymagania wstępne**

- .NET 6 SDK lub nowszy (kod działa z .NET Core i .NET Framework)  
- Podstawowa znajomość C# oraz wiersza poleceń  
- Dostęp do Internetu w celu pobrania pakietu NuGet Aspose.OCR  

Jeśli masz to wszystko, zanurzmy się.

![Kod C# rozpoznający tekst z obrazu przy użyciu Aspose OCR](image.png "Kod C# rozpoznający tekst z obrazu przy użyciu Aspose OCR")

## Krok 1 – Rozpoznawanie tekstu z obrazu: Konfiguracja silnika OCR

Na początek potrzebujemy instancji `OcrEngine`. Aspose OCR pozwala wybrać urządzenie przetwarzające — GPU dla szybkości, CPU jako zabezpieczenie. Silnik przyjmuje także podpowiedź limitu pamięci, co może być przydatne na współdzielonych maszynach.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Dlaczego to ważne:**  
Wybranie `OcrDevice.Gpu` może zaoszczędzić sekundy przy rozpoznawaniu dużych obrazów, szczególnie wielostronicowych TIFF‑ów. `GpuMemoryLimit` zapobiega zagarnięciu całej pamięci GPU na współdzielonym stanowisku pracy.

## Krok 2 – Załadowanie obrazu do OCR (w tym obsługa TIFF)

Teraz przekazujemy silnikowi obraz. `ImageStream.FromFile` od Aspose akceptuje **dowolny** format obsługiwany przez bibliotekę — TIFF, PNG, JPEG, cokolwiek. Ten krok bezpośrednio spełnia wymaganie **load image for OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Wskazówka:** Jeśli pracujesz z wielostronicowym TIFF‑em, Aspose automatycznie traktuje każdą stronę jako osobną klatkę, a silnik przetworzy je kolejno. Nie potrzebny jest dodatkowy kod.

## Krok 3 – Uruchomienie rozpoznawania i **wyodrębnienie tekstu z tiff**

Gdy silnik jest gotowy, a obraz załadowany, uruchamiamy operację OCR. Metoda `Recognize` zwraca `OcrResult`, który zawiera czysty tekst, wyniki pewności i szczegóły czasowe.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Obsługa przypadków brzegowych:**  
Jeśli GPU nie jest dostępne, `engine.Recognize()` nadal działa, ponieważ silnik cicho przełącza się na CPU. Możesz sprawdzić `engine.Device` po rozpoznaniu, jeśli potrzebujesz zalogować, które urządzenie faktycznie zostało użyte.

## Krok 4 – Pobranie rozpoznanego czystego tekstu

Wyodrębnienie tekstu jest proste — odczytaj właściwość `Text`. To właśnie tutaj **wyodrębniasz tekst z tiff** (lub dowolnego innego obrazu) i prezentujesz go użytkownikowi.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Zobaczysz surowe znaki, a znaki końca linii zostaną zachowane tak, jak występują w źródłowym obrazie. Dla bardziej ustrukturyzowanego wyjścia (np. JSON lub CSV) możesz zagłębić się w `result.Regions` i `result.Lines`, ale czysty tekst zazwyczaj wystarcza w szybkich skryptach.

## Krok 5 – Pomiar czasu przetwarzania i obsługa przejścia na GPU

Wydajność ma znaczenie, zwłaszcza przy przetwarzaniu dziesiątek stron. Właściwość `ProcessingTime` podaje dokładnie, ile czasu zajęło OCR, niezależnie od tego, czy działało na GPU czy CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Dlaczego to istotne:**  
Jeśli zauważysz, że czas rośnie, możesz dostosować `GpuMemoryLimit` lub przełączyć się wyraźnie na CPU (`Device = OcrDevice.Cpu`). Z kolei wynik poniżej sekundy przy dużym TIFF‑ie oznacza, że przyspieszenie GPU spełnia swoją rolę.

## Pełny, gotowy do uruchomienia przykład

Skopiuj poniższy kod do nowego projektu konsolowego (`dotnet new console -n OcrDemo`) i uruchom `dotnet add package Aspose.OCR`. Następnie zamień `YOUR_DIRECTORY/sample_multi_page.tif` na ścieżkę do swojego obrazu.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Oczekiwany wynik (skrócony dla przejrzystości):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Jeśli Twój komputer nie posiada wydajnego GPU, czas może być kilka sekund dłuższy, ale tekst i tak zostanie poprawnie wyodrębniony.

## Częste pytania i pułapki

- **Co zrobić, gdy obraz jest ogromny (powyżej 10 MB)?**  
  Zmniejsz jego rozdzielczość przed przekazaniem do silnika lub zwiększ `GpuMemoryLimit`, jeśli masz wystarczającą ilość VRAM.  
- **Czy mogę przetwarzać wiele obrazów w pętli?**  
  Oczywiście. Wystarczy ponownie używać tej samej instancji `OcrEngine` i przypisywać nowy `ImageStream` w każdej iteracji.  
- **Czy muszę coś zwalniać?**  
  `OcrEngine` implementuje `IDisposable`. Umieść go w bloku `using`, aby zapewnić czyste zarządzanie zasobami, szczególnie przy pracy z zasobami GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **A co z językami innymi niż angielski?**  
  Ustaw `engine.Language = OcrLanguage.Spanish` (lub dowolny obsługiwany język) przed wywołaniem `Recognize()`.  

## Podsumowanie

Masz teraz kompletną, end‑to‑end rozwiązanie, które **rozpoznaje tekst z obrazu** w C# przy użyciu Aspose OCR. Tutorial pokazał, jak **załadować obraz do OCR**, jak **wyodrębnić tekst z tiff**, oraz jak mierzyć wydajność przy eleganckim przejściu na GPU.

Od tego momentu możesz:

- Eksperymentować z różnymi formatami obrazów (BMP, PDF), aby zobaczyć, jak Aspose je obsługuje.  
- Zagłębić się w `result.Regions`, aby uzyskać dane o ramkach ograniczających, jeśli potrzebujesz analizy układu


## Co powinieneś się nauczyć dalej?

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}