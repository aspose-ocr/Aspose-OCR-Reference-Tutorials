---
category: general
date: 2026-04-06
description: Wyodrębnij tekst z obrazu przy użyciu Aspose OCR GPU w C#. Dowiedz się,
  jak wczytać obraz z pliku i ustawić limit pamięci GPU w tym przewodniku krok po
  kroku.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: pl
og_description: Wyodrębnij tekst z obrazu przy użyciu Aspose OCR GPU w C#. Dowiedz
  się, jak wczytać obraz z pliku i ustawić limit pamięci GPU w tym przewodniku krok
  po kroku.
og_title: Wyodrębnianie tekstu z obrazu przy użyciu Aspose OCR GPU – Pełny przewodnik
  C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Wyodrębnianie tekstu z obrazu przy użyciu Aspose OCR GPU – Pełny przewodnik
  C#
url: /pl/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu przy użyciu Aspose OCR GPU – pełny przewodnik C#

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale utknąłeś w miejscu, gdzie liczy się wydajność? Nie jesteś sam — wielu programistów napotyka ten sam problem, gdy OCR staje się wąskim gardłem. W tym tutorialu pokażemy dokładnie, jak wyodrębnić tekst z obrazu przy użyciu silnika GPU Aspose OCR, wczytać obraz z pliku i nawet ustawić limit pamięci GPU dla lepszej kontroli zasobów.

Przejdziemy przez kompletny, gotowy do uruchomienia przykład w C#, wyjaśnimy, dlaczego każda linijka ma znaczenie, i wskażemy typowe pułapki, na które możesz natrafić. Po zakończeniu będziesz mieć solidne podstawy do budowania szybkich, skalowalnych potoków OCR działających na GPU.

## Co obejmuje ten przewodnik

- **Wymagania wstępne**: .NET 6+ (lub .NET Framework 4.6+), pakiet NuGet Aspose.OCR, kompatybilny sterownik GPU.
- **Kod krok po kroku**, który wczytuje obraz z pliku, konfiguruje silnik GPU Aspose OCR i wyodrębnia tekst.
- **Dlaczego** warto ustawić limit pamięci GPU i jak zrobić to bezpiecznie.
- **Obsługa przypadków brzegowych**: obrazy o niskiej rozdzielczości, brak GPU oraz rozwiązywanie problemów z wynikami pewności.
- **Kolejne kroki**: przetwarzanie wsadowe, integracja z ASP.NET Core oraz przełączanie z powrotem na CPU w razie potrzeby.

> **Pro tip:** Jeśli nie masz pewności, czy GPU jest wykorzystywane, sprawdź monitor aktywności GPU (np. NVIDIA‑SMI) podczas działania OCR. Zobaczysz skok zużycia pamięci, który odpowiada ustawionemu limitowi.

---

![Diagram przedstawiający przepływ wyodrębniania tekstu z obrazu przy użyciu silnika Aspose OCR GPU](extract-text-from-image-aspose-ocr-gpu.png "wyodrębnianie tekstu z obrazu przy użyciu Aspose OCR GPU")

## Krok 1: Inicjalizacja silnika Aspose OCR do przetwarzania na GPU

Pierwszą rzeczą, której potrzebujesz, jest instancja `OcrEngine`, która wie, że ma działać na GPU. Aspose udostępnia przejrzysty obiekt `OcrEngineSettings`, w którym możesz określić środowisko wykonawcze.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Dlaczego to ważne:** Domyślnie Aspose OCR przełącza się na CPU, co jest w porządku dla małych obrazów, ale może być bardzo wolne dla zdjęć o wysokiej rozdzielczości. Jawne ustawienie `Runtime = OcrRuntime.Gpu` przenosi ciężkie obliczenia na kartę graficzną, dając zauważalny przyrost prędkości.

## Krok 2: (Opcjonalnie) Ustaw limit pamięci GPU

Jeśli pracujesz na współdzielonym stanowisku lub w kontenerze z ograniczonymi zasobami GPU, możesz ograniczyć ilość pamięci, jaką zużywa silnik OCR. Zapobiega to awariom z powodu braku pamięci i pozwala innym procesom działać płynnie.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Kiedy to stosować:**  
- **Środowiska wielodzierżawcze**, w których kilka usług współdzieli to samo GPU.  
- **Potoki CI/CD**, które przydzielają stałą ilość pamięci GPU na zadanie.  

Jeśli pominiesz tę linię, Aspose użyje tyle pamięci, ile potrzebuje, co jest w porządku na dedykowanym stanowisku.

## Krok 3: Wczytaj obraz z pliku

Teraz musimy wczytać obraz do pamięci. Aspose OCR pracuje z `System.Drawing.Image`, więc użyjemy `Image.FromFile`. Upewnij się, że ścieżka wskazuje na istniejący plik; w przeciwnym razie zostanie zgłoszony wyjątek.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Dlaczego wczytywanie z pliku ma znaczenie:** Wielu programistów próbuje podać bezpośrednio tablicę bajtów, co działa, ale dodaje niepotrzebny krok konwersji. Użycie `Image.FromFile` jest proste, a konstrukcja `using` zapewnia szybkie zwolnienie uchwytu pliku.

## Krok 4: Uruchom OCR i pobierz wynik

Po skonfigurowaniu silnika i wczytaniu obrazu możemy w końcu wyodrębnić tekst. Metoda `Recognize` zwraca `OcrResult` zawierający zarówno surowy tekst, jak i współczynnik pewności.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Zrozumienie wyniku:**  
- `Confidence` to wartość od 0 do 1. Pewność 0,95 (czyli 95 %) zazwyczaj oznacza, że OCR jest bardzo trafny.  
- `Text` zawiera podziały linii tak, jak występują na obrazie, co jest przydatne przy dalszym przetwarzaniu.

## Krok 5: Zweryfikuj wynik i obsłuż przypadki brzegowe

### Sprawdzanie poziomu pewności

Jeśli pewność spadnie poniżej, powiedzmy, 80 %, możesz przełączyć się na przetwarzanie CPU lub zastosować wstępne przetwarzanie obrazu (np. binaryzację).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Radzenie sobie z brakiem GPU

Nie każdy komputer ma kompatybilne GPU. Aspose zgłosi `OcrException`, jeśli nie uda się zainicjować środowiska GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Obrazy o wysokiej rozdzielczości

Bardzo duże obrazy (np. > 4000 px szerokości) mogą zużywać dużo pamięci GPU. Jeśli przekroczysz wcześniej ustawiony limit, Aspose przerwie przetwarzanie. W takich przypadkach najpierw zmniejsz rozmiar obrazu:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego. Zawiera wszystkie kroki, obsługę błędów oraz opcjonalną logikę przełączania.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Oczekiwany wynik

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Jeśli pewność spadnie poniżej progu, zobaczysz dodatkowe komunikaty o przełączeniu na CPU.

---

## Zakończenie

Teraz wiesz, **jak wyodrębnić tekst z obrazu** przy użyciu silnika GPU Aspose OCR, **jak wczytać obraz z pliku** oraz dlaczego warto **ustawić limit pamięci GPU** w środowiskach produkcyjnych. Powyższy przykład to w pełni funkcjonalne, gotowe do cytowania rozwiązanie, które możesz wstawić do dowolnego projektu .NET.

Co dalej? Rozważ:

- **Przetwarzanie wsadowe**: iteracja po folderze z obrazami i zapisywanie wyników do pliku CSV.  
- **Integracja z ASP.NET Core**: udostępnienie endpointu API, który przyjmuje przesłany obraz i zwraca tekst OCR.  
- **Optymalizacja wydajności**: eksperymentowanie z różnymi wartościami `GpuMemoryLimit` i monitorowanie wykorzystania GPU w poszukiwaniu optymalnego punktu.

Śmiało dostosuj kod do własnych potrzeb — niezależnie od tego, czy budujesz pipeline digitalizacji dokumentów, aplikację do tłumaczenia w czasie rzeczywistym, czy usługę skanowania paragonów. Fundamenty pozostają takie same: inicjalizuj silnik GPU, zarządzaj pamięcią rozsądnie i zawsze weryfikuj pewność.

Masz pytania lub napotkałeś problem? zostaw komentarz poniżej, a wspólnie znajdziemy rozwiązanie. Powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}