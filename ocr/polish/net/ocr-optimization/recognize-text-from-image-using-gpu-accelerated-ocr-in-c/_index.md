---
category: general
date: 2026-02-25
description: Rozpoznawaj tekst z obrazu szybko, korzystając z przyspieszonego GPU
  OCR. Dowiedz się, jak ustawić tryb GPU, wczytać obraz do OCR i wyodrębnić tekst
  z pliku TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: pl
og_description: Rozpoznawaj tekst z obrazu natychmiast, korzystając z przyspieszonego
  GPU OCR. Szczegółowy samouczek C# opisujący ustawienie trybu GPU, wczytanie obrazu
  do OCR oraz wyodrębnienie tekstu z pliku TIFF.
og_title: Rozpoznaj tekst z obrazu przy użyciu OCR przyspieszonego GPU – przewodnik
  C#
tags:
- Aspose OCR
- C#
- GPU computing
title: Rozpoznawanie tekstu z obrazu przy użyciu przyspieszonego GPU OCR w C#
url: /pl/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z obrazu przy użyciu przyspieszonego GPU‑accelerated OCR w C#

Czy kiedykolwiek potrzebowałeś **rozpoznać tekst z obrazu**, ale Twój procesor nie radził sobie z wysoką rozdzielczością skanu? Nie jesteś sam. W wielu rzeczywistych projektach — pomyśl o digitalizacji faktur lub archiwizacji starych gazet — pojedynczy plik TIFF może zatrzymać Twój pipeline na minuty. Dobra wiadomość? Aspose.OCR pozwala przełączyć tryb i przekazać ciężką pracę swojemu GPU, zamieniając wolną operację w prawie natychmiastową.

W tym samouczku przeprowadzimy Cię przez cały proces: jak **ustawić tryb GPU**, jak **wczytać obraz do OCR** oraz jak **wyodrębnić tekst z plików TIFF**. Po zakończeniu będziesz mieć samodzielny, gotowy do produkcji przykład, który możesz wstawić do dowolnego projektu .NET 6+.

## Wymagania wstępne

- .NET 6 SDK (lub nowszy) zainstalowany.
- Visual Studio 2022 lub dowolny edytor, którego preferujesz.
- Pakiet NuGet Aspose.OCR (`Aspose.OCR`) dodany do Twojego projektu.
- GPU obsługujące DirectX 11 lub nowszy (większość nowoczesnych kart graficznych spełnia wymagania).  
  *Jeśli nie masz GPU, nadal możesz uruchomić kod z `GpuMode.Auto` — biblioteka automatycznie przełączy się na CPU.*

> **Wskazówka:** Sprawdź, czy sterownik GPU jest aktualny; przestarzałe sterowniki mogą powodować niejasne błędy inicjalizacji.

## Krok 1 – Utwórz silnik OCR i ustaw tryb GPU

Pierwszą rzeczą, której potrzebujesz, jest instancja `OcrEngine`. Ten obiekt przechowuje wszystkie ustawienia, w tym to, czy silnik ma używać GPU.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Dlaczego to ważne:** Włączenie trybu GPU przenosi intensywne obliczeniowo przetwarzanie obrazu (binaryzacja, usuwanie szumów itp.) na kartę graficzną. Na średniej klasy RTX 3060 możesz zauważyć **3‑5× przyspieszenie** w porównaniu z czystym przetwarzaniem na CPU.

## Krok 2 – Wczytaj obraz do OCR (przykład TIFF)

Aspose.OCR obsługuje wiele formatów, ale TIFF jest powszechny w dokumentach skanowanych, ponieważ zachowuje jakość bezstratną. Użyj `ImageStream.FromFile`, aby wczytać plik do pamięci.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Przypadek brzegowy:** Niektóre pliki TIFF zawierają wiele stron. `ImageStream.FromFile` odczyta tylko pierwszą stronę. Jeśli musisz przetworzyć każdą stronę, iteruj po `ImageInfo.Pages` i przekazuj każdą z nich osobno do silnika.

## Krok 3 – Wykonaj rozpoznawanie

Gdy silnik jest skonfigurowany, a obraz wczytany, wywołaj `Recognize()`. Metoda zwraca obiekt `OcrResult` zawierający wynik w postaci zwykłego tekstu oraz dodatkowe metadane.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**Co zrobić, gdy tekst jest zniekształcony?**  
- Upewnij się, że obraz ma prawidłową orientację (obróć w razie potrzeby).  
- Dostosuj opcje przetwarzania wstępnego, np. `ocrEngine.Config.DeskewEnabled = true;`.  
- Dla dokumentów wielojęzycznych ustaw `ocrEngine.Config.Language = Language.English;` lub odpowiedni enum.

## Krok 4 – Zweryfikuj wynik i obsłuż błędy

Solidna implementacja sprawdza, czy wynik nie jest null i przechwytuje potencjalne wyjątki (np. brak sterowników GPU).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**Dlaczego to opakować?** Inicjalizacja GPU może rzucić `DllNotFoundException`, jeśli wymagane natywne biblioteki nie są dostępne. Blok catch zapewnia elegancki sposób degradacji.

## Pełny, gotowy do uruchomienia przykład

Łącząc wszystko razem, oto kompletny program, który możesz skompilować i uruchomić od razu. Zamień ścieżkę pliku na rzeczywisty plik TIFF na swoim komputerze.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Oczekiwany wynik**

Jeśli TIFF zawiera czytelny tekst po angielsku, zobaczysz coś w rodzaju:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

Jeśli obraz jest pusty lub nieczytelny, konsola zasugeruje sprawdzenie pliku źródłowego.

## Częste pytania i warianty

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę przetwarzać JPEG lub PNG zamiast TIFF?** | Oczywiście. `ImageStream.FromFile` działa z każdym formatem obsługiwanym przez Aspose.OCR (PNG, JPEG, BMP itp.). |
| **Co zrobić, jeśli w jednym TIFF jest wiele stron?** | Iteruj po `ImageInfo.Pages` i przypisz każdą stronę do `ocrEngine.Image` przed wywołaniem `Recognize()`. |
| **Czy potrzebna jest licencja na Aspose.OCR?** | Darmowa wersja ewaluacyjna działa do 100 stron. W środowisku produkcyjnym zakup licencję, aby usunąć znak wodny wersji ewaluacyjnej. |
| **Jak zmienić model językowy?** | Ustaw `ocrEngine.Config.Language = Language.Spanish;` (lub dowolny obsługiwany enum). |
| **Czy istnieje sposób na uzyskanie współczynników pewności?** | Włącz `ocrEngine.Config.EnableConfidence = true;` i sprawdzaj `result.Confidence` dla każdej linii. |

## Zakończenie

Teraz wiesz, jak **rozpoznawać tekst z obrazu** przy użyciu **przyspieszonego GPU OCR** w C#. Dzięki **ustawieniu trybu GPU**, **wczytaniu obrazu do OCR** i **wyodrębnieniu tekstu z plików TIFF**, stworzyłeś szybkie, skalowalne rozwiązanie gotowe do rzeczywistych obciążeń.

Kolejne kroki? Spróbuj połączyć ten kod z generatorem PDF, aby tworzyć przeszukiwalne PDF-y, lub przekazać wyodrębnione ciągi do pipeline przetwarzania języka naturalnego. Możesz także eksperymentować z `GpuMode.Auto`, aby aplikacja była dostosowana do środowisk bez GPU.

Miłego kodowania i niech Twoje operacje OCR będą błyskawiczne! 

![recognize text from image example](https://example.com/ocr-demo.png "recognize text from image using GPU‑accelerated OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}