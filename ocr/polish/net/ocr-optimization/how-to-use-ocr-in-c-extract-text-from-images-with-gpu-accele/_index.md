---
category: general
date: 2025-12-29
description: Jak używać OCR w C#, aby wyodrębnić tekst z obrazów, wyświetlić liczbę
  znaków i zwiększyć wydajność dzięki przyspieszeniu GPU przy użyciu Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: pl
og_description: Jak używać OCR w C#, aby wyodrębnić tekst z obrazów, wyświetlić liczbę
  znaków i przyspieszyć przetwarzanie przy użyciu GPU z Aspose OCR.
og_title: Jak używać OCR w C# – Szybkie wyodrębnianie tekstu przy użyciu GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Jak używać OCR w C# – wyodrębniaj tekst z obrazów z przyspieszeniem GPU
url: /pl/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś, **jak używać OCR** w projekcie .NET bez pisania tysięcy linii kodu? Może zeskanowałeś ogromny plik TIFF i potrzebujesz tekstu szybko, albo po prostu chcesz policzyć znaki dla pulpitu raportowego. Tak czy inaczej, trafiłeś we właściwe miejsce. W tym tutorialu przeprowadzimy Cię przez proces wyodrębniania tekstu z obrazu, wyświetlania liczby znaków oraz przyspieszenia całego procesu za pomocą **GPU acceleration OCR** – wszystko przy użyciu biblioteki **C# Aspose OCR**.

Dodamy także tematy poboczne, które możesz wyszukiwać: **extract text image**, **display character count**, oraz triki **c# ocr aspose**. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową, która w mgnieniu oka przetworzy duże skany.

---

## Czego się nauczysz

- Konfiguracja Aspose OCR w projekcie C# (bez tajemnic NuGet).
- Włączenie **GPU acceleration OCR** dla dużych plików.
- Ładowanie obrazu i **extract text from the image**.
- **Display character count** oraz czasu przetwarzania.
- Radzenie sobie z typowymi problemami, takimi jak brak sterowników GPU czy nieobsługiwane formaty obrazów.

> **Wymagania wstępne:** .NET 6+ (lub .NET Framework 4.7.2) oraz kompatybilny GPU. Jeśli nie masz GPU, kod automatycznie przełączy się na tryb CPU.

---

![Jak używać OCR z przyspieszeniem GPU w C#](ocr-gpu.png "przykład użycia OCR pokazujący wykorzystanie GPU")

*Tekst alternatywny obrazu: ilustracja pokazująca użycie OCR z przyspieszeniem GPU*

---

## Krok 1: Instalacja Aspose OCR i przygotowanie projektu

### Dlaczego to ważne

Zanim będziesz mógł **use OCR**, biblioteka musi być zreferencjonowana. Aspose OCR dostarcza pojedynczy pakiet NuGet, który zawiera natywne binaria zarówno dla CPU, jak i GPU, więc nie musisz ręcznie szukać DLL‑ów.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **Pro tip:** Jeśli celujesz w .NET Framework, użyj interfejsu NuGet w Visual Studio, aby uniknąć konfliktów wersji.

### Pełny szkielet projektu

Utwórz nową aplikację konsolową i wklej poniższy kod `Program.cs`. Zawiera on wszystkie niezbędne dyrektywy `using`, więc nie będziesz musiał zgadywać, co zaimportować.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

Zapisz plik, przywróć pakiety i jesteś gotowy do kolejnego kroku.

---

## Krok 2: Jak używać silnika OCR z przyspieszeniem GPU

### Dlaczego włączać GPU?

Przetwarzanie wielomegapikselowego TIFF na CPU może trwać sekundy, a nawet minuty. Ścieżka **GPU acceleration OCR** przenosi operacje piksel‑po‑pikselu na kartę graficzną, skracając czas dramatycznie — często do ułamka pierwotnego.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **Dlaczego to działa:** `UseGpu` przełącza wewnętrzny pipeline. `InitializeGpu()` wymusza wczesną weryfikację, dzięki czemu możesz wykryć problemy ze sterownikami przed długotrwałym wywołaniem `Recognize`.

---

## Krok 3: Extract Text Image i wyświetlenie liczby znaków

Teraz, gdy silnik pracuje, **extract text from the image** i pokaż, ile znaków zostało rozpoznanych. To część, którą pomijają większość programistów, a jest kluczowa dla walidacji i dalszej analizy.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**Oczekiwany wynik** (przykład dla skanu 2‑stronicowego):

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

Jeśli GPU nie jest dostępne, zobaczysz ostrzeżenie i ten sam wynik, tylko wolniej.

---

## Krok 4: Obsługa dużych plików i przypadków brzegowych

### Co zrobić, gdy obraz jest ogromny?

Aspose OCR potrafi strumieniować strony, ale nadal potrzebujesz wystarczającej ilości RAM. Dobrą praktyką jest zmniejszenie DPI nieistotnych elementów przed rozpoznaniem:

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### Brak sterowników GPU?

`try/catch` wokół `InitializeGpu()` już przechwytuje większość problemów, ale możesz także zapytać o dostępne urządzenia:

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### Nieobsługiwane formaty obrazów?

Aspose obsługuje TIFF, PNG, JPEG, BMP oraz kilka egzotycznych formatów. Jeśli otrzymasz `UnsupportedFormatException`, najpierw skonwertuj plik przy pomocy narzędzia takiego jak ImageMagick lub wbudowanej metody `Image.Save` do PNG.

---

## Krok 5: Podsumowanie – pełny działający przykład

Skopiuj i wklej cały program poniżej do `Program.cs`. To samodzielna demonstracja, którą możesz uruchomić od razu (wystarczy podmienić ścieżkę).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

Uruchom ją poleceniem `dotnet run` i obserwuj, jak konsola wypisuje **character count** oraz tekst OCR. To cały **how to use OCR** od początku do końca.

---

## Zakończenie

Właśnie omówiliśmy **how to use OCR** w C# do **extract text from images**, **display character count** oraz przyspieszenia całego potoku za pomocą **GPU acceleration OCR** przy użyciu biblioteki **c# ocr aspose**. Najważniejsze wnioski:

1. Zainstaluj Aspose OCR przez NuGet i odwołaj właściwe przestrzenie nazw.  
2. Włącz GPU, ale zawsze zapewnij fallback na CPU.  
3. Załaduj obraz, opcjonalnie zmniejsz rozdzielczość, a następnie wywołaj `Recognize`.  
4. Pobierz `ocrResult.Text` i `ocrResult.ProcessingTime`, aby **display character count** i metryki wydajności.  

Od tego punktu możesz rozbudować projekt — zapisywać tekst w bazie danych, przekazywać go do indeksu wyszukiwania lub uruchamiać wykrywanie języka na wyekstrahowanym ciągu. Jeśli potrzebujesz przetwarzać PDF‑y, po prostu podaj każdą stronę jako obraz; ten sam kod zadziała.

**Kolejne kroki**, które możesz rozważyć:

- Użycie **extract text image** z wielostronicowych PDF‑ów przy pomocy `PdfConverter`.  
- Dostosowanie ustawień OCR (pakiety językowe, redukcja szumów) w celu zwiększenia dokładności.  
- Skalowanie rozwiązania w Azure Functions lub AWS Lambda z instancjami obsługującymi GPU.  

Wypróbuj, popełnij błędy i udoskonalaj. Tak powstają prawdziwe projekty OCR. Powodzenia w kodowaniu i niech Twoje skany zawsze będą czytelne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}