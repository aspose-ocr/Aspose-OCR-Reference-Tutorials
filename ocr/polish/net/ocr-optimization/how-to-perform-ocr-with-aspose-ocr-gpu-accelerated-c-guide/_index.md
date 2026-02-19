---
category: general
date: 2026-02-19
description: jak szybko wykonać OCR na obrazach TIFF o wysokiej rozdzielczości. Dowiedz
  się, jak wyodrębnić tekst z plików TIFF przy użyciu OCR na GPU w C#.
draft: false
keywords:
- how to perform OCR
- extract text from tiff
- use gpu ocr
- Aspose OCR C#
- high‑resolution image processing
- OCR performance tuning
language: pl
og_description: Jak przeprowadzić OCR na plikach TIFF o wysokiej rozdzielczości przy
  użyciu Aspose OCR i przyspieszenia GPU. Kompletny przewodnik krok po kroku.
og_title: Jak wykonać OCR – przyspieszony GPU tutorial w C#
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Jak przeprowadzić OCR przy użyciu Aspose OCR – przewodnik C# przyspieszony
  GPU
url: /pl/net/ocr-optimization/how-to-perform-ocr-with-aspose-ocr-gpu-accelerated-c-guide/
---

"Post‑przetwarzanie". "Hybrid mode" -> "Tryb hybrydowy". etc.

Also translate bullet points.

Make sure code block placeholders remain.

Now produce final content with shortcodes at top and bottom unchanged.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak wykonać OCR – przyspieszone GPU‑Accelerated C# Tutorial

Kiedykolwiek potrzebowałeś wykonać OCR na ogromnym skanie TIFF i zastanawiałeś się, dlaczego trwa to wiecznie? Nie jesteś jedyny. W tym przewodniku pokażemy Ci **jak wykonać OCR** na obrazie wysokiej rozdzielczości, wykorzystując GPU, a na koniec otrzymasz gotowy do uruchomienia program w C#, który w mgnieniu oka wyodrębnia tekst z plików tiff.

Omówimy wszystko, od instalacji pakietu Aspose OCR po włączenie przetwarzania GPU, i wyjaśnimy, dlaczego każde ustawienie ma znaczenie. Po zakończeniu będziesz mógł wkleić ten kod do dowolnego projektu .NET, wskazać plik .tif i otrzymać czysty, przeszukiwalny tekst — bez dodatkowych usług.

## Prerequisites

- .NET 6.0 lub nowszy (kod jest skierowany do .NET 6, ale .NET 5 również działa)  
- Kompatybilny GPU (NVIDIA CUDA 11+ lub AMD Radeon z obsługą OpenCL)  
- **Aspose.OCR** pakiet NuGet (wersja 23.9 lub nowsza)  
- Plik TIFF wysokiej rozdzielczości, który chcesz odczytać (np. `high_res_page.tif`)  

Jeśli którykolwiek z tych punktów jest Ci nieznany, nie martw się — każdy z nich zostanie wyjaśniony w kolejnych krokach.

## Step 1: Install Aspose OCR and Enable GPU Processing  

Pierwszą rzeczą, którą musisz zrobić, jest dodanie biblioteki Aspose OCR do swojego projektu i włączenie obsługi GPU. Włączenie GPU informuje silnik, aby przeniósł ciężkie obliczenia macierzowe na kartę graficzną, co może skrócić czas przetwarzania o 70 % lub więcej na nowoczesnym GPU.

```csharp
// Install the package via the CLI (run once):
// dotnet add package Aspose.OCR --version 23.9.0

using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // Enable GPU acceleration – requires a compatible GPU driver.
        OcrEngine.EnableGpuProcessing(true);
```

**Dlaczego to ważne:**  
Bez `EnableGpuProcessing(true)` silnik OCR wraca do czysto CPU‑owego wykonania, co jest w porządku dla małych obrazów, ale drastycznie wolne przy wielomegapikselowych TIFF‑ach. Włączenie flagi pozwala bibliotece używać CUDA lub OpenCL pod maską, znacząco redukując `ProcessingTime`, które zobaczysz później.

## Step 2: Configure the OCR Engine for English (or any language you need)  

Następnie tworzymy instancję `OcrEngine` i ustawiamy język. Aspose obsługuje ponad 100 języków; angielski jest tutaj pokazany, ponieważ jest najczęstszy, ale możesz zamienić `Language.English` na `Language.French`, `Language.German` itp.

```csharp
        // Step 2: Create and configure the OCR engine.
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change if you need another language.
        };
```

**Pro tip:**  
Jeśli planujesz przetwarzać dokumenty wielojęzyczne, zainicjuj wiele silników lub przełącz właściwość `Language` pomiędzy wywołaniami. Dzięki temu unikniesz kosztów ponownego tworzenia silnika dla każdej strony.

## Step 3: Perform OCR on a High‑Resolution TIFF  

Teraz najciekawsza część — podaj silnikowi plik TIFF i pozwól mu wykonać ciężką pracę. Metoda `RecognizeImage` zwraca `OcrResult`, który zawiera zarówno wyodrębniony tekst, jak i informacje o czasie.

```csharp
        // Step 3: Run OCR on the TIFF image.
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/high_res_page.tif");
```

**Obsługa przypadków brzegowych:**  
- **Duże pliki:** Jeśli Twój TIFF przekracza 50 MB, rozważ najpierw zmniejszenie go przy pomocy `System.Drawing` lub `ImageSharp`, aby utrzymać zużycie pamięci w rozsądnych granicach.  
- **Wielostronicowe TIFF‑y:** Wywołuj `RecognizeImage` w pętli po każdym indeksie strony; Aspose zwróci tekst dla każdej strony osobno.

## Step 4: Output Processing Time and Extracted Text  

Na koniec wypisujemy czas przetwarzania oraz surowy wynik OCR. To właśnie tutaj zobaczysz korzyść płynącą z przyspieszenia GPU.

```csharp
        // Step 4: Display results.
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Typowy wynik**

```
Time taken: 312 ms
=== Extracted Text ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Na średniej klasy RTX 3060 ten sam TIFF 3000 × 4000 pikseli, który kiedyś zajmował ~1,2 sekundy na CPU, teraz kończy się w ~300 ms — zauważ dramatyczny przyrost prędkości.

## How to Extract Text from TIFF Files Efficiently  

Jeśli interesuje Cię tylko **extract text from tiff** i nie potrzebujesz GPU, możesz pominąć flagę GPU. Reszta kodu pozostaje identyczna, ale stracisz przyspieszenie przy dużych skanach. Oto minimalna wersja:

```csharp
using Aspose.OCR;
using System;

class SimpleTiffOcr
{
    static void Main()
    {
        var engine = new OcrEngine { Language = Language.English };
        var result = engine.RecognizeImage(@"sample.tif");
        Console.WriteLine(result.Text);
    }
}
```

**Kiedy używać tego:**  
- Twoje wdrożenie działa na serwerze bez głowy, który nie posiada GPU.  
- TIFF‑y są małe (< 1 MP) i czas CPU nie jest wąskim gardłem.  

Nawet bez GPU silnik OCR Aspose jest bardzo dokładny dzięki wbudowanym modelom neuronowym.

## Using GPU OCR for Faster Processing – Common Pitfalls  

Choć **use gpu OCR** daje Ci prędkość, kilka pułapek może Cię zaskoczyć:

| Problem | Objaw | Rozwiązanie |
|---------|-------|-------------|
| Brak sterownika CUDA | `EnableGpuProcessing` zgłasza `PlatformNotSupportedException` | Zainstaluj najnowszy sterownik NVIDIA i zestaw narzędzi CUDA |
| Nieobsługiwany GPU | Silnik cicho przełącza się na CPU | Sprawdź, czy Twój GPU pojawia się w `OcrEngine.GetAvailableGpus()` (jeśli go wywołujesz) |
| Brak pamięci przy bardzo dużych obrazach | `System.OutOfMemoryException` | Przetwarzaj obraz w kafelkach (`engine.RecognizeRegion`) |
| Nieprawidłowa orientacja obrazu | Zniekształcony tekst | Wstępnie obróć TIFF przy użyciu `ImageSharp` przed OCR |

**Szybka kontrola poprawności:** Uruchom demo raz z `EnableGpuProcessing(false)`. Porównaj wartości `ProcessingTime`; zdrowe uruchomienie przyspieszone GPU powinno być co najmniej 2‑3× szybsze.

## Full Working Example (Copy‑Paste Ready)

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę do swojego pliku TIFF.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // 1️⃣ Enable GPU acceleration (requires a compatible GPU)
        OcrEngine.EnableGpuProcessing(true);

        // 2️⃣ Create the OCR engine and set the language
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change as needed
        };

        // 3️⃣ Perform OCR on a high‑resolution TIFF
        var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 4️⃣ Show timing and extracted text
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Uruchomienie tego na maszynie z RTX 3070 daje wynik podobny do wcześniejszego przykładu, potwierdzając, że **how to perform OCR** z obsługą GPU działa zgodnie z opisem.

## Next Steps – Going Beyond the Basics  

- **Przetwarzanie wsadowe:** Owiń wywołanie `RecognizeImage` w pętlę `foreach` po folderze z TIFF‑ami.  
- **Post‑przetwarzanie:** Przekaż `ocrResult.Text` do korektora ortograficznego lub parsera języka naturalnego, aby oczyścić artefakty OCR.  
- **Tryb hybrydowy:** Wykryj rozmiar obrazu w czasie wykonywania i zdecyduj, czy włączyć GPU (`if (image.Width * image.Height > 5_000_000) EnableGpuProcessing(true)`).  

Wszystkie te rozszerzenia nadal **use gpu ocr**, gdy ma to sens, utrzymując Twój pipeline szybki i świadomy zasobów.

## Conclusion  

Teraz wiesz **jak wykonać OCR** na plikach TIFF wysokiej rozdzielczości przy użyciu Aspose OCR i przyspieszenia GPU, i możesz pewnie **extract text from tiff** w ułamku czasu, który potrzebowałby jedynie CPU. Pełny, gotowy do kopiowania przykład demonstruje cały przepływ — od włączenia GPU po wypisanie czasu przetwarzania i finalnego tekstu.

Wypróbuj go, dostosuj ustawienia językowe i spróbuj przetworzyć partię stron. Jeśli napotkasz problemy, wróć do tabeli „Using GPU OCR for Faster Processing” — większość kwestii jest tam opisana. Szczęśliwego kodowania i ciesz się przyspieszeniem!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}