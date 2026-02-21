---
category: general
date: 2026-02-20
description: Rozpoznawaj tekst z obrazu szybko dzięki przyspieszeniu GPU w Aspose
  OCR. Dowiedz się, jak wyodrębnić tekst ze skanu w C# przy użyciu pełnego, gotowego
  do uruchomienia przykładu.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: pl
og_description: Rozpoznawaj tekst z obrazu przy użyciu przyspieszenia GPU. Ten samouczek
  pokazuje, jak wyodrębnić tekst ze skanu w C# przy użyciu Aspose OCR, wraz z kodem
  i wskazówkami.
og_title: rozpoznawanie tekstu z obrazu przy użyciu Aspose OCR GPU – przewodnik C#
tags:
- Aspose
- OCR
- C#
- GPU
title: Rozpoznawanie tekstu z obrazu przy użyciu Aspose OCR GPU w C#
url: /pl/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rozpoznawanie tekstu z obrazu przy użyciu Aspose OCR GPU w C#

Czy kiedykolwiek potrzebowałeś **rozpoznawać tekst z obrazu**, ale plik był ogromny i Twój procesor się dusił? Może próbowałeś zwykłej biblioteki OCR i zajęło to wieki, albo wyniki były niekompletne. Dobre wieści? Dzięki przyspieszeniu GPU w Aspose OCR możesz zamienić masywny zeskanowany plik TIFF w czysty, przeszukiwalny tekst w kilka sekund.

W tym przewodniku przeprowadzimy Cię przez kompletny, gotowy do skopiowania przykład, który pokaże, jak **wyodrębnić tekst ze skanów** na maszynie z obsługą GPU. Bez niejasnych odniesień, tylko kod, którego potrzebujesz, wyjaśnienie, dlaczego każda linia ma znaczenie, oraz kilka pułapek, które uchronią Cię przed wyrywaniem włosów.

## Czego będziesz potrzebować

- **.NET 6+** (lub .NET Framework 4.7+ – API działa tak samo)
- **Aspose.OCR for .NET** pakiet NuGet (wersja 23.12 lub nowsza)
- **GPU** z obsługą CUDA (opcjonalnie, ale znacznie szybsze)
- Wysokiej rozdzielczości zeskanowany obraz (np. `large_doc.tif`)

Jeśli nie masz GPU, silnik automatycznie przełączy się na CPU — więc nadal możesz uruchomić przykład, choć nieco wolniej.

## Krok 1 – Zainstaluj pakiet Aspose.OCR

Otwórz terminal lub konsolę Package Manager i uruchom:

```bash
dotnet add package Aspose.OCR
```

Lub w interfejsie NuGet w Visual Studio wyszukaj **Aspose.OCR** i kliknij *Install*. To pobierze podstawową bibliotekę OCR oraz opcjonalny zestaw przyspieszenia GPU.

> **Wskazówka:** Po instalacji sprawdź folder `packages` pod kątem pliku `Aspose.OCR.Acceleration.dll`. Jest on wymagany do obsługi GPU; jeśli pracujesz na serwerze bez interfejsu graficznego, możesz go pominąć i kod nadal się skompiluje.

## Krok 2 – Zainicjalizuj silnik OCR przyspieszony GPU

Klasa `GpuOcrEngine` automatycznie wykrywa każde kompatybilne GPU. Jeśli masz więcej niż jedno urządzenie, możesz wybrać konkretne, ale większość programistów po prostu pozwala jej zdecydować.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**Dlaczego to ważne:** Inicjalizacja silnika GPU raz utrzymuje niskie narzuty. Jeśli wielokrotnie tworzysz i niszczysz silnik w pętli, stracisz zyski wydajnościowe.

## Krok 3 – Wczytaj swój wysokiej rozdzielczości zeskanowany obraz

Aspose OCR współpracuje z `System.Drawing.Image`. Upewnij się, że ścieżka do pliku wskazuje na rzeczywisty obraz; w przeciwnym razie otrzymasz `FileNotFoundException`.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **Przypadek brzegowy:** Jeśli obraz jest większy niż 10 000 × 10 000 px, rozważ najpierw jego zmniejszenie. Pamięć GPU jest ograniczona, a próba wczytania ogromnego bitmapu może spowodować `OutOfMemoryException`.

## Krok 4 – Wykonaj OCR z domyślnymi ustawieniami języka (łaciński)

Metoda `Recognize` zwraca zwykły ciąg znaków. Możesz przekazać obiekt `OcrOptions`, jeśli potrzebujesz innego języka lub niestandardowego przetwarzania wstępnego.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**Dlaczego domyślne ustawienie działa:** Większość zeskanowanych dokumentów — umowy, faktury, raporty — jest w alfabetach łacińskich. Jeśli potrzebujesz cyrylicy, arabskiego lub chińskiego, ustaw `ocrEngine.Language = "ru"` (lub odpowiedni kod ISO) przed wywołaniem `Recognize`.

## Krok 5 – Wyświetl lub zachowaj wyodrębniony tekst

Dla szybkiego sprawdzenia napiszemy wynik po prostu na konsolę. W prawdziwej aplikacji możesz zapisać go do bazy danych, pliku `.txt` lub wprowadzić do indeksu wyszukiwania.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### Oczekiwany wynik

Jeśli `large_doc.tif` zawiera prosty akapit, np. „Hello, world!”, zobaczysz:

```
Hello, world!
```

W przypadku skanów wielostronicowych silnik konkatenatuje tekst w kolejności czytania. Możesz później podzielić go przy użyciu znaków nowej linii (`\n`), jeśli potrzebujesz granic stron.

## Radzenie sobie z typowymi problemami

| Issue | Symptom | Fix |
|-------|---------|-----|
| **Nie wykryto GPU** | `ocrEngine.Device` jest `null` i przetwarzanie jest wolne. | Zainstaluj najnowszy sterownik NVIDIA oraz zestaw CUDA Toolkit (v11+). Sprawdź przy pomocy `nvidia-smi`. |
| **Opóźnienia w garbage collection** | Wzrost zużycia pamięci po przetworzeniu wielu obrazów. | Wywołaj `scannedImage.Dispose()` po OCR lub umieść obraz w bloku `using`. |
| **Nieprawidłowy język** | Zniekształcone znaki dla tekstu nie‑łacińskiego. | Ustaw `ocrEngine.Language` na właściwy kod ISO 639‑1 przed wywołaniem `Recognize`. |
| **Bardzo duże pliki** | `OutOfMemoryException`. | Zmniejsz rozmiar przy pomocy `Image.GetThumbnailImage` lub podziel skan na kafelki. |

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się cały program — w tym dyrektywy `using`, obsługa błędów oraz schludny blok `using` dla obrazu:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Co robi ten kod

1. **Tworzy** `GpuOcrEngine`, który automatycznie wybiera najlepsze GPU.  
2. **Wczytuje** docelowy plik TIFF w bloku `using`, aby zapewnić jego zwolnienie.  
3. **Wywołuje** `Recognize`, aby przekształcić bitmapę w ciąg znaków.  
4. **Zapisuje** wynik zarówno na konsolę, jak i do pliku `.txt` obok źródłowego obrazu.  
5. **Przechwytuje** wszelkie wyjątki i wyświetla przyjazny komunikat o błędzie.

## Posuwając się dalej – od „rozpoznawania tekstu z obrazu” do pełnoskalowych potoków dokumentów

Teraz, gdy możesz **wyodrębnić tekst ze skanów**, rozważ następujące kolejne kroki:

- **Przetwarzanie wsadowe:** Przejdź przez folder z plikami TIFF i zbierz wyniki w jeden przeszukiwalny indeks.  
- **Wykrywanie języka:** Użyj `ocrEngine.DetectLanguage()` (jeśli dostępne), aby automatycznie przełączać języki.  
- **Post‑processing:** Przetwórz wynik przez korektor ortograficzny lub filtr wyrażeń regularnych, aby usunąć artefakty OCR.  
- **Integracja z Azure Cognitive Search:** Prześlij wyodrębniony tekst do przeszukiwalnego indeksu w chmurze, aby uzyskać natychmiastowe wyszukiwanie.

Każdy z tych kroków opiera się na tym samym podstawowym wzorcu, który właśnie zobaczyłeś — zainicjalizuj raz, podawaj obrazy, zbieraj tekst.

## Podsumowanie

Właśnie nauczyłeś się, jak **rozpoznawać tekst z obrazu** przy użyciu silnika Aspose OCR przyspieszonego GPU w C#. Pełny, gotowy do uruchomienia przykład pokazuje, jak skonfigurować silnik, wczytać wysokiej rozdzielczości skan, wykonać OCR i obsłużyć wynik. Stosując powyższe wskazówki i obsługę przypadków brzegowych, unikniesz typowych problemów i uzyskasz niezawodne rezultaty, niezależnie od tego, czy pracujesz na laptopie dewelopera, czy na serwerze produkcyjnym.

Gotowy, aby przekształcić więcej skanów w przeszukiwalne dane? Spróbuj przetworzyć cały folder, eksperymentuj z językami nie‑łacińskimi lub wprowadź wyniki do silnika wyszukiwania pełnotekstowego. Nie ma granic, a kod, który właśnie napisałeś, jest solidną podstawą, której potrzebujesz.

Miłego kodowania! 🚀

![recognize text from image example](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}