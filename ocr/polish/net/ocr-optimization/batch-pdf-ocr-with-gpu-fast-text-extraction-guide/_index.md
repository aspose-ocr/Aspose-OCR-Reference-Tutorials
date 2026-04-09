---
category: general
date: 2026-04-08
description: Batch OCR PDF z GPU umożliwia szybkie wyodrębnianie tekstu z plików PDF.
  Dowiedz się, jak ustawić język OCR i korzystać z przyspieszonego przez GPU OCR w
  C#.
draft: false
keywords:
- batch pdf ocr
- extract text from pdf
- gpu accelerated ocr
- set ocr language
language: pl
og_description: Batch PDF OCR z GPU pozwala szybko wyodrębniać tekst z plików PDF.
  Ten samouczek pokazuje, jak ustawić język OCR i wykorzystać przyspieszenie GPU.
og_title: Wsadowkie OCR PDF z GPU – Przewodnik szybkiego wyodrębniania tekstu
tags:
- Aspose.OCR
- C#
- GPU
title: Wsadowe OCR PDF z GPU – Przewodnik szybkiego wyodrębniania tekstu
url: /pl/net/ocr-optimization/batch-pdf-ocr-with-gpu-fast-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch PDF OCR z GPU – Przewodnik szybkiego wyodrębniania tekstu

Potrzebujesz uruchomić **batch PDF OCR z GPU**, aby przyspieszyć przetwarzanie masywnych dokumentów? W tym przewodniku pokażemy, jak **wyodrębnić tekst z plików PDF** przy użyciu silnika **OCR przyspieszanego przez GPU** firmy Aspose.OCR. Niezależnie od tego, czy przetwarzasz tysiące faktur, czy skanujesz archiwa prawne, możliwość ustawienia języka OCR i uruchomienia GPU może zaoszczędzić minuty — a nawet godziny — w twoim obciążeniu.  

Oto co: większość programistów domyślnie używa OCR tylko na CPU i zastanawia się, dlaczego jest tak wolny. Po zakończeniu tego samouczka zrozumiesz, dlaczego GPU ma znaczenie, jak skonfigurować silnik i jak wyciągnąć czysty tekst z każdej strony PDF w zadaniu wsadowym. Bez zewnętrznych narzędzi, tylko czysty C# i kilka linijek kodu.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod kompiluje się również z .NET Core)  
- Aspose.OCR dla .NET 2024‑R3 (lub nowszy) – pakiet NuGet `Aspose.OCR`  
- Co najmniej jedna karta NVIDIA GPU z obsługą CUDA 11+ (lub kompatybilny AMD, jeśli masz odpowiedni sterownik)  
- Podstawowa znajomość C# async/await (opcjonalna, ale pomocna)  

Jeśli już masz te elementy, świetnie — zanurzmy się. Jeśli nie, krok **set OCR language** działa również na CPU, więc możesz przetestować logikę przed podłączeniem GPU.

## Batch PDF OCR – Inicjalizacja silnika GPU

Pierwszym krokiem jest utworzenie silnika OCR świadomego GPU i włączenie akceleratora. Aspose udostępnia klasę `GpuOcrEngine`, która dziedziczy po standardowym `OcrEngine`. Włączenie GPU jest tak proste, jak przełączenie flagi.

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

/// <summary>
/// Demonstrates batch PDF OCR using a GPU‑accelerated engine.
/// </summary>
public static class PdfBatchOcrDemo
{
    public static void BatchPdfWithGpu()
    {
        // 1️⃣ Create a GPU‑aware OCR engine and enable the GPU.
        var ocrEngine = new GpuOcrEngine
        {
            Options = { EnableGpu = true, GpuDeviceId = 0 } // 0 = first GPU in the system
        };
```

**Dlaczego to ważne:**  
- **EnableGpu = true** informuje Aspose, aby kierował ciężkie zadania przetwarzania obrazu do karty graficznej.  
- **GpuDeviceId = 0** wybiera pierwszą kartę GPU; zmień indeks, jeśli masz wiele kart.  
- Użycie `GpuOcrEngine` zamiast `OcrEngine` zapewnia tę samą powierzchnię API z przyspieszeniem wydajności.

> **Pro tip:** Jeśli uruchamiasz na serwerze bez interfejsu graficznego, upewnij się, że sterownik NVIDIA i środowisko uruchomieniowe CUDA są zainstalowane systemowo; w przeciwnym razie silnik cicho przełączy się na CPU.

## Ustaw język OCR (set OCR language)

Następnie poinformuj silnik, jaki język ma rozpoznawać. Aspose automatycznie pobiera pakiety językowe przy pierwszym żądaniu, więc nie musisz samodzielnie dołączać dużych plików.

```csharp
        // 2️⃣ Set the language for recognition – “en” for English.
        ocrEngine.Language = "en";
```

Możesz zamienić `"en"` na dowolny kod ISO‑639‑1 (`"fr"`, `"de"`, `"es"` itp.). Jeśli potrzebujesz obsługi wielu języków, przekaż listę oddzieloną przecinkami, np. `"en,fr"`.

**Dlaczego warto ustawić język:**  
- Silnik OCR używa słowników specyficznych dla języka, aby poprawić dokładność.  
- Brak ustawienia powoduje domyślny język angielski, co może błędnie interpretować znaki w innych alfabetach.  
- Automatyczne pobieranie zapewnia, że zawsze masz najnowsze modele bez ręcznych aktualizacji.

## Wyodrębnianie tekstu ze stron PDF

Teraz wymieniamy pliki PDF, które chcemy przetworzyć. W rzeczywistym scenariuszu możesz odczytywać nazwy plików z katalogu lub bazy danych; tutaj zakodujemy krótką listę dla przejrzystości.

```csharp
        // 3️⃣ List the PDF pages to be processed.
        var pdfPagePaths = new List<string>
        {
            @"YOUR_DIRECTORY\page1.pdf",
            @"YOUR_DIRECTORY\page2.pdf",
            @"YOUR_DIRECTORY\page3.pdf"
        };
```

> **Uwaga:** Używaj dosłownych literałów ciągów (`@""`) aby uniknąć konieczności escapowania backslashy w Windows.

Gdy lista jest gotowa, iterujemy po każdym pliku, uruchamiamy OCR i wypisujemy liczbę znaków — szybki test, czy silnik faktycznie coś odczytał.

```csharp
        // 4️⃣ Recognize each page and output the character count.
        foreach (var pagePath in pdfPagePaths)
        {
            // RecognizePdf returns an OcrResult containing the extracted text.
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");
        }
    }
}
```

**Oczekiwany wynik (przykład):**

```
Page YOUR_DIRECTORY\page1.pdf → 1284 characters
Page YOUR_DIRECTORY\page2.pdf → 1120 characters
Page YOUR_DIRECTORY\page3.pdf → 1439 characters
```

Jeśli widzisz `0 characters`, sprawdź ponownie, czy PDF faktycznie zawiera wybieralny tekst lub osadzone obrazy; Aspose OCR działa na stronach rasteryzowanych, więc zeskanowane PDF-y są w porządku, ale natywne PDF-y z ukrytym tekstem mogą wymagać innego podejścia.

## Weryfikacja wyników i obsługa przypadków brzegowych

Uruchamianie OCR w zadaniu wsadowym nie zawsze przebiega gładko. Poniżej znajdują się typowe pułapki i sposoby ich obejścia.

| Problem | Objaw | Rozwiązanie |
|-------|----------|-----|
| **Brak sterownika GPU** | `Aspose.Ocr.Exceptions.OcrException: GPU not available` | Zainstaluj najnowszy sterownik NVIDIA oraz zestaw narzędzi CUDA. |
| **Brak pamięci przy dużych PDF-ach** | Proces awaryjnie kończy się po kilku stronach | Zwiększ `Options.MaxMemoryUsage` lub przetwarzaj PDF-y po jednej stronie, używając `RecognizePdfPage`. |
| **Pakiet językowy nie został pobrany** | Tekst jest zniekształcony lub pusty | Upewnij się, że masz dostęp do internetu przy pierwszym ustawieniu `ocrEngine.Language`. |
| **Uszkodzony plik PDF** | `System.IO.IOException: Cannot read file` | Sprawdź integralność pliku przed przekazaniem go do OCR, np. przy użyciu `PdfDocument.Load`. |

Możesz także przechwycić surowy tekst OCR do dalszego przetwarzania — zapisać go w pliku `.txt`, wprowadzić do indeksu wyszukiwania lub do modelu językowego w celu streszczenia.

```csharp
        // Example: Save each OCR result to a .txt file.
        foreach (var pagePath in pdfPagePaths)
        {
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
            System.IO.File.WriteAllText(txtPath, ocrResult.Text);
            Console.WriteLine($"Saved OCR text to {txtPath}");
        }
```

**Dlaczego zapisywanie jest przydatne:**  
- Oddziela ciężki krok OCR od późniejszych analiz, umożliwiając jednorazowe wykonanie ekstrakcji i nieograniczone ponowne użycie plików tekstowych.  
- Pliki tekstowe są małe w porównaniu do PDF‑ów, co czyni je idealnymi do kontroli wersji lub porównywania różnic.

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz wkleić do nowego projektu `.csproj` i uruchomić. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę zawierającą twoje strony PDF.

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

namespace BatchPdfOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            BatchPdfWithGpu();
        }

        /// <summary>
        /// Executes batch PDF OCR using a GPU‑accelerated engine.
        /// </summary>
        public static void BatchPdfWithGpu()
        {
            // Step 1 – Initialize GPU engine.
            var ocrEngine = new GpuOcrEngine
            {
                Options = { EnableGpu = true, GpuDeviceId = 0 }
            };

            // Step 2 – Set the OCR language (auto‑download enabled).
            ocrEngine.Language = "en";

            // Step 3 – Define the PDFs to process.
            var pdfPagePaths = new List<string>
            {
                @"YOUR_DIRECTORY\page1.pdf",
                @"YOUR_DIRECTORY\page2.pdf",
                @"YOUR_DIRECTORY\page3.pdf"
            };

            // Step 4 – Run OCR on each file and write results.
            foreach (var pagePath in pdfPagePaths)
            {
                var ocrResult = ocrEngine.RecognizePdf(pagePath);
                Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");

                // Optional: persist the extracted text.
                var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
                System.IO.File.WriteAllText(txtPath, ocrResult.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }
        }
    }
}
```

Kompiluj przy użyciu:

```bash
dotnet build
dotnet run
```

Powinieneś zobaczyć liczbę znaków oraz wygenerowane pliki `.txt` pojawiające się obok każdego PDF.

![Diagram przetwarzania Batch PDF OCR z GPU](https://example.com/image.png "Batch PDF OCR z GPU")

*Tekst alternatywny obrazu: **Batch PDF OCR z GPU** diagram przetwarzania pokazujący PDF → GPU OCR → Wyjście tekstu.*

## Kolejne kroki i powiązane tematy

- **GPU‑przyspieszone vs. tylko CPU wydajność:** Uruchom szybki benchmark (przetwórz 100 stron) i porównaj czasy. Oczekuj przyspieszenia 2‑5× na nowoczesnych GPU.  
- **Wsady wielojęzyczne:** Ustaw `ocrEngine.Language = "en,fr,es"` aby obsłużyć dokumenty wielojęzyczne w jednym przebiegu.  
- **Strumieniowanie dużych PDF‑ów:** Użyj `RecognizePdfPage`, aby OCR-ować jedną stronę na raz, zmniejszając obciążenie pamięci.  
- **Integracja z Azure Functions lub AWS Lambda:** Przenieś zadanie wsadowe do chmury, wykorzystując instancje z obsługą GPU do skalowania na żądanie.  
- **Indeksowanie wyszukiwania:** Przekaż wyodrębniony tekst do Elasticsearch lub Azure Cognitive Search w celu szybkiego wyszukiwania dokumentów.

## Zakończenie

Właśnie opanowałeś **batch PDF OCR z GPU**, nauczyłeś się efektywnie **wyodrębniać tekst z PDF** oraz odkryłeś właściwy sposób **ustawiania języka OCR** dla optymalnej dokładności. Włączając przyspieszenie GPU, znacząco skracasz czas przetwarzania, a dzięki prostemu API Aspose unikasz szablonowego kodu, który zwykle towarzyszy potokom OCR.  

Wypróbuj to na własnym zestawie danych — dostosuj listę języków, eksperymentuj z różnymi urządzeniami GPU lub opakuj logikę w usługę w tle. Nie ma ograniczeń, gdy łączysz wysokowydajne OCR z nowoczesnym narzędziem .NET.  

Masz pytania lub natrafiłeś na przypadek brzegowy, którego tutaj nie opisano? Dodaj komentarz lub otwórz zgłoszenie na forum Aspose. Szczęśliwego kodowania i niech twoje uruchomienia OCR będą szybkie i wolne od błędów!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}