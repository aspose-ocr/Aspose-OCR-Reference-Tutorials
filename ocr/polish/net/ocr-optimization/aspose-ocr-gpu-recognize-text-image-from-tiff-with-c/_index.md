---
category: general
date: 2026-05-21
description: Aspose OCR GPU umożliwia szybkie rozpoznawanie tekstu na obrazie. Dowiedz
  się, jak załadować obraz do OCR, wyodrębnić tekst z pliku TIFF i zwiększyć wydajność.
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: pl
og_description: Aspose OCR GPU przyspiesza wyodrębnianie tekstu. Ten przewodnik pokazuje,
  jak załadować obraz do OCR, rozpoznać tekst na obrazie oraz efektywnie wyodrębnić
  tekst z pliku TIFF.
og_title: Aspose OCR GPU – Rozpoznaj tekst z obrazu TIFF w C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: 'Aspose OCR GPU: Rozpoznaj tekst z obrazu TIFF w C#'
url: /pl/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU: Rozpoznawanie Tekstu z Obrazu w formacie TIFF w C#

Zastanawiałeś się kiedyś, jak **rozpoznać tekst z obrazu** w ogromnym pliku TIFF, nie blokując przy tym procesora? Nie jesteś sam. W wielu przepływach przetwarzania dokumentów wąskim gardłem jest krok OCR, szczególnie gdy podajesz gigabajty zeskanowanych stron do zwykłego silnika.  

Dobre wieści? **Aspose OCR GPU** może przyspieszyć ten proces, a poniższy przykład kodu pokazuje dokładnie, jak **wczytać obraz do OCR**, **wyodrębnić tekst z TIFF** i elegancko przejść w tryb CPU, jeśli GPU nie jest dostępne. Zanurzmy się.

## Co obejmuje ten tutorial

Przejdziemy przez kompletny, gotowy do skopiowania i wklejenia program w C#, który:

1. Włącza przyspieszenie GPU (opcjonalnie, z automatycznym przejściem na CPU).  
2. Tworzy `OcrEngine` skonfigurowany dla języka angielskiego.  
3. Wczytuje duży **obraz OCR TIFF** z dysku.  
4. Uruchamia rozpoznawanie i wypisuje wynik.  

Po zakończeniu zrozumiesz **dlaczego** każdy krok ma znaczenie, jak radzić sobie z typowymi przypadkami brzegowymi i będziesz mieć działający przykład, który możesz dostosować do PDF‑ów, wielostronicowych TIFF‑ów lub nawet strumieni z kamery w czasie rzeczywistym.

> **Wymagania wstępne** – .NET 6+ (lub .NET Framework 4.7+), pakiet NuGet Aspose.OCR oraz maszyna z obsługą GPU, jeśli chcesz zobaczyć przyspieszenie. Nie jest wymagana specjalna sprzętowa konfiguracja; kod po prostu użyje CPU, gdy nie wykryje GPU.

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="aspose ocr gpu"}

## Krok 1: Włączenie przyspieszenia GPU (opcjonalnie)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**Dlaczego to ważne:**  
Rdzenie GPU doskonale radzą sobie z masywnym równoległym przetwarzaniem potrzebnym do wstępnej obróbki obrazu (binaryzacja, usuwanie szumów) oraz inferencji sieci neuronowej. Przełączając `EnableGpu(true)` dajesz silnikowi zielone światło do przeniesienia tych zadań. Jeśli maszyna nie posiada karty zgodnej z CUDA, Aspose cicho przełącza się z powrotem na CPU, więc nie nastąpi krytyczny błąd.

**Wskazówka:** Na Windows może być potrzebny najnowszy sterownik NVIDIA oraz zainstalowane narzędzia CUDA. Na Linuxie upewnij się, że `nvidia‑driver` i `libcuda.so` znajdują się w ścieżce bibliotek.

## Krok 2: Utworzenie i skonfigurowanie silnika OCR

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**Dlaczego to ważne:**  
`OcrEngine` jest sercem **Aspose OCR GPU**. Ustawienie `Language` informuje podlegający model neuronowy, jakiego zestawu znaków się spodziewać, co znacząco podnosi dokładność. Możesz także dostosować `Resolution`, `PreprocessOptions` lub `RecognitionMode` dla trudniejszych dokumentów.

## Krok 3: Wczytanie obrazu do OCR

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**Dlaczego to ważne:**  
TIFF może zawierać wiele stron, wysoką rozdzielczość i bezstratną kompresję — idealne do archiwalnych skanów, ale ciężkie dla pamięci. `ImageStream.FromFile` strumieniuje plik, unikając pełnego załadowania do pamięci przy bardzo dużych obrazach.  

**Przypadek brzegowy:** Jeśli musisz przetworzyć wielostronicowy TIFF, wywołaj `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);` w pętli, zwiększając `pageIndex`, aż `ocrEngine.Image.IsNull` zwróci `true`.

## Krok 4: Wykonanie rozpoznawania

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**Dlaczego to ważne:**  
`Recognize()` wykonuje całą ciężką pracę: wstępną obróbkę, analizę układu, segmentację znaków i w końcu inferencję sieci neuronowej. Gdy GPU jest aktywne, krok inferencji odbywa się na GPU, często skracając czas przetwarzania o 50‑80 % dla dużych TIFF‑ów.

## Krok 5: Wyświetlenie wyników

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**Dlaczego to ważne:**  
`ocrEngine.Text` zawiera w pełni połączony ciąg znaków z obrazu, natomiast `ProcessingTime` daje szybki benchmark do porównania uruchomień CPU vs. GPU. Wyjście w konsoli jest przydatne do szybkiego debugowania; w produkcji prawdopodobnie zapiszesz tekst do bazy danych lub pliku.

**Przykładowy wynik (dla 2‑stronicowej faktury):**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

Jeśli GPU nie jest dostępne, czas może wzrosnąć do ~1800 ms na tym samym sprzęcie, co wyraźnie pokazuje korzyść płynącą z **aspose ocr gpu**.

---

## Radzenie sobie z typowymi problemami

| Sytuacja | Na co zwrócić uwagę | Jak naprawić |
|-----------|-------------------|------------|
| **GPU nie wykryte** | `EnableGpu(true)` cicho przełącza się na CPU, ale możesz sądzić, że nadal używa GPU. | Sprawdź `OcrEngine.IsGpuEnabled` po wywołaniu; zaloguj wynik. |
| **Brak pamięci przy ogromnym TIFF** | Wczytanie obrazu 10 000 × 10 000 pikseli może przekroczyć RAM. | Użyj `ImageStream.FromFile(path, pageIndex, maxResolution: 300)`, aby zmniejszyć rozdzielczość przy wczytywaniu. |
| **Nieprawidłowy język** | Model angielski na dokumencie francuskim daje zniekształcony wynik. | Ustaw `Language = OcrLanguage.French` lub włącz tryb wielojęzyczny. |
| **Wielostronicowy TIFF** | Przetwarzana jest tylko pierwsza strona. | Pętla po stronach przy użyciu `ImageStream.FromFile(path, pageNumber)`. |

---

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Zawiera obsługę błędów, logowanie statusu GPU oraz prosty timer do własnych benchmarków.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

Skopiuj, wklej, naciśnij **F5** i obserwuj, jak konsola wypisuje liczbę znaków oraz wyodrębniony tekst. Zamień `OcrLanguage.English` na dowolny inny język obsługiwany przez Aspose, jeśli potrzebujesz **rozpoznać tekst z obrazu** w języku hiszpańskim, niemieckim itp.

---

## Podsumowanie i kolejne kroki

Właśnie omówiliśmy, jak **aspose ocr gpu** może **rozpoznawać tekst z obrazu** w **OCR TIFF**, jak **wczytać obraz do OCR** oraz jak **wyodrębnić tekst z TIFF** efektywnie. Podstawowe pomysły — włączenie GPU, konfiguracja języka, strumieniowanie TIFF i odczyt wyniku — są przenośne na inne formaty plików, takie jak JPEG czy PNG.

### Co wypróbować dalej

- **Przetwarzanie wsadowe**: Przejdź przez folder TIFF‑ów, zapisując każdy `ocrEngine.Text` do pliku `.txt`.  
- **Obsługa wielostronicowa**: Użyj `ImageStream.FromFile(path, pageIndex)` w pętli `while`, aby przetworzyć każdą stronę dokumentu wielostronicowego.  
- **Własna wstępna obróbka**: Dostosuj `ocrEngine.PreprocessOptions` (np. `Denoise`, `Deskew`) dla zaszumionych skanów.  
- **Benchmarkowanie GPU**: Zapisz `ProcessingTime` z i bez `EnableGpu(true)` na tej samej maszynie, aby zmierzyć przyspieszenie.

Śmiało eksperymentuj — przyspieszenie GPU najbardziej błyszczy przy wysokiej rozdzielczości i wielostronicowych TIFF‑ach, ale nawet skromna 1080 Ti znacznie skróci czas rozpoznawania.

Masz pytania dotyczące konkretnego typu dokumentu lub potrzebujesz pomocy przy integracji wyniku z bazą danych? Zostaw komentarz poniżej i powodzenia w kodowaniu!

## Powiązane tutoriale

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}