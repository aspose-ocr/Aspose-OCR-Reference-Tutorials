---
category: general
date: 2026-09-13
description: Dowiedz się, jak przekształcić zeskanowaną stronę na PDF w C# przy użyciu
  Aspose OCR. Ten przewodnik pokazuje wstępne przetwarzanie, rozpoznawanie koreańskiego
  tekstu oraz tworzenie przeszukiwalnego PDF.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Dowiedz się, jak przekształcić zeskanowaną stronę na PDF w C# z Aspose
  OCR. Samouczek obejmuje wstępne przetwarzanie obrazu, przyspieszone GPU‑accelerated
  OCR dla koreańskiego tekstu oraz generowanie przeszukiwalnego PDF w kilka minut.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Jak przekształcić zeskanowaną stronę na PDF w C# z OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Jak przekształcić zeskanowaną stronę na PDF w C# z OCR
url: /pl/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak przekształcić zeskanowaną stronę w PDF w C# przy użyciu OCR

Jeśli potrzebujesz **przekształcić zeskanowaną stronę w PDF** zachowując możliwość wyszukiwania tekstu, jesteś we właściwym miejscu. Ten tutorial przeprowadzi Cię przez użycie Aspose OCR do **preprocess image for OCR**, **recognize Korean text image**, i w końcu **create searchable PDF image** – wszystko z prostą aplikacją konsolową w C#.

## Szybkie odpowiedzi
- **Jaka biblioteka obsługuje OCR?** Aspose.OCR for .NET  
- **Czy mogę używać GPU?** Yes – enable GPU acceleration for up to 2× faster processing  
- **Czy potrzebuję koreańskiego pakietu językowego?** It downloads automatically on first use  
- **Czy wynik będzie przeszukiwalny?** The generated PDF contains an invisible text layer  
- **Jakie wersje .NET są obsługiwane?** .NET 6.0 and later (including .NET Core and .NET Framework)

## Wymagania

- **.NET 6.0 lub nowszy** – działa na .NET Core, .NET Framework oraz .NET 5/6+  
- **Aspose.OCR for .NET** pakiet NuGet (`Aspose.OCR`) – klucze trial są darmowe na stronie Aspose  
- Przykładowy obraz z koreańskimi znakami, np. `korean_book_page.jpg`  
- Twoje ulubione IDE (Visual Studio 2022, VS Code, Rider, itp.)

> **Wskazówka:** Przechowuj obrazy w folderze `Resources/`, aby ścieżki były spójne na różnych maszynach.

## Przegląd procesu

1. Zainicjalizuj silnik OCR z obsługą GPU.  
2. Dodaj filtry **preprocess image for OCR** takie jak deskew i denoise.  
3. Pobierz i załaduj koreański model językowy (obsługiwane automatycznie).  
4. Uruchom OCR na obrazie.  
5. Wyeksportuj wynik przy użyciu **SearchablePdfExporter** do **create searchable PDF image**.  
6. (Opcjonalnie) Serializuj wynik OCR do JSON dla dalszych potoków.

Poniżej rozwijamy każdy krok, wyjaśniamy *dlaczego* ma to znaczenie i podajemy dokładny kod, który możesz skopiować‑wkleić.

## Jak działa konwersja zeskanowanej strony do PDF?

`OcrEngine` jest główną klasą w Aspose.OCR, która wykonuje rozpoznawanie znaków optycznych na obrazach.  
`SearchablePdfExporter` tworzy PDF zawierający oryginalny obraz oraz niewidzialną warstwę tekstu do wyszukiwania.  
`RecognitionResult` przechowuje tekst i dane o pewności zwrócone przez silnik OCR.

Załaduj swój obraz przy pomocy `new OcrEngine()` i wywołaj `engine.Recognize("korean_book_page.jpg")`, następnie przekaż `RecognitionResult` do `SearchablePdfExporter.Export`. Ten dwustopniowy przepływ odczytuje bitmapę, wyodrębnia tekst Unicode i osadza oba w jednym PDF, gdzie warstwa tekstowa jest niewidzialna, ale przeszukiwalna. Przyspieszenie GPU skraca czas rozpoznawania mniej więcej o połowę, podczas gdy filtry deskew i denoise zwiększają dokładność nawet o 15 % przy szumnych skanach.

## Konwersja obrazu do PDF – pełny przepływ pracy

Poniższy fragment to *kompletny* program. Utwórz nowy projekt konsolowy (`dotnet new console -n OcrPdfDemo`) i zamień automatycznie wygenerowany `Program.cs` na kod pokazany w miejscu zastępczym.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Dlaczego to działa

- **GPU acceleration** skraca czas rozpoznawania mniej więcej o połowę w porównaniu z trybem tylko CPU.  
- **Deskew** i **Denoise** to klasyczne techniki *preprocess image for OCR*; korygują typowe wady skanowania, które w przeciwnym razie powodują pomijanie znaków przez silnik.  
- **Language model loading** jest niezbędne dla **recognize Korean text image** – bez koreańskiego modelu silnik użyje ogólnego alfabetu łacińskiego i wygeneruje bezużyteczne wyniki.  
- **SearchablePdfExporter** łączy oryginalną bitmapę i niewidzialną warstwę tekstową, dając wynik **create searchable pdf image**, który możesz indeksować w dowolnym przeglądarce PDF.

## Dlaczego to działa

- **GPU acceleration** skraca czas rozpoznawania mniej więcej o połowę w porównaniu z trybem tylko CPU.  
- **Deskew** i **Denoise** to klasyczne techniki *preprocess image for OCR*; korygują typowe wady skanowania, które w przeciwnym razie powodują pomijanie znaków przez silnik.  
- **Language model loading** jest niezbędne dla **recognize Korean text image** – bez koreańskiego modelu silnik użyje ogólnego alfabetu łacińskiego i wygeneruje bezużyteczne wyniki.  
- **SearchablePdfExporter** łączy oryginalną bitmapę i niewidzialną warstwę tekstową, dając wynik **create searchable pdf image**, który możesz indeksować w dowolnym przeglądarce PDF.

## Preprocess image for OCR – wskazówki i triki

`DeskewFilter` koryguje rotację zeskanowanych stron.  
`ContrastFilter` dostosowuje kontrast obrazu, aby poprawić dokładność OCR.  
`BinarizationFilter` konwertuje obraz na czarno‑biały na podstawie progu, redukując szumy tła.  
`OrientationFilter` wykrywa i koryguje mieszane strony pionowe i poziome.  

| Problem | Dodatkowy filtr | Jak dodać |
|-------|-------------------|------------|
| Niski kontrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Duży szum tła | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mieszana orientacja (portret i krajobraz) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Uwaga:** Dodanie zbyt wielu filtrów może spowolnić przetwarzanie. Testuj każdą zmianę na jednej stronie przed skalowaniem.

## Recognize Korean text image – typowe pułapki

Koreański system pisma zawiera sylaby Hangul, które są wizualnie gęste. Jeśli zauważysz zniekształcony wynik:

1. **Upewnij się, że model językowy jest w pełni pobrany** – sprawdź konsolę pod kątem komunikatu takiego jak „Downloading Korean model…”.  
2. **Zwiększ `MaxAngle`** w `DeskewFilter`, jeśli twoje skany są obrócone o więcej niż 12°.  
3. **Zwiększ pamięć GPU** ustawiając `ocrEngine.GpuMemoryLimit = 2048;` (wartość w MB).  

`LanguageModel.Korean` ładuje dane językowe koreańskiego dla OCR, umożliwiając dokładne rozpoznawanie Hangul.  

Te dostosowania bezpośrednio wpływają na sukces **recognize Korean text image**.

## Create searchable PDF image – weryfikacja wyniku

Po zakończeniu programu otwórz `korean_page.pdf` w dowolnym czytniku PDF (Adobe Acrobat Reader, Foxit, nawet Chrome). Powinieneś móc:

- **Zaznaczyć tekst** myszą tak, jakby to był natywny PDF.  
- **Wyszukać** koreańskie słowa przy użyciu wbudowanego pola wyszukiwania.  

Jeśli warstwa tekstowa jest pusta, sprawdź ponownie, czy metoda `Export` otrzymała poprawną ścieżkę obrazu oraz czy wynik OCR zawiera niepusty `RecognitionResult.Text`.

## Pełny wynik JSON – czego się spodziewać

Konsola wypisuje ładnie sformatowany ładunek JSON. Przykład przycięty wygląda tak:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Rozwiązywanie problemów i FAQ

**Q: Mój PDF jest ogromny w porównaniu do oryginalnego obrazu.**  
A: Eksporter osadza oryginalną bitmapę w jej natywnej rozdzielczości. Jeśli rozmiar jest problemem, zmniejsz rozmiar obrazu *przed* rozpoznaniem:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR zwraca puste ciągi znaków.**  
A: Zweryfikuj, czy ścieżka do obrazu jest poprawna i czy plik nie jest uszkodzony. Upewnij się także, że sterownik GPU jest aktualny; starsze sterowniki mogą powodować ciche awarie.

**Q: Czy mogę przetwarzać wiele stron w pętli?**  
A: Oczywiście. Owiń kroki 4‑6 w pętlę `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` i odpowiednio zmień ścieżkę wyjściowego PDF.

## Zakończenie

Właśnie **przekształciliśmy obraz w PDF** zachowując przeszukiwalny tekst, wszystko dzięki potężnemu potokowi Aspose OCR. Dzięki **preprocess image for OCR** zwiększasz dokładność; dzięki **recognize Korean text image** obsługujesz złożone skrypty; a dzięki **create searchable pdf image** otrzymujesz przenośny, indeksowalny dokument.

Pobierz kod, skieruj go na własne skany i eksperymentuj z dodatkowymi filtrami lub modelami językowymi. Ten sam schemat działa dla chińskiego, japońskiego lub dowolnego języka opartego na alfabecie łacińskim — po prostu zamień `LanguageModel.Korean` na odpowiedni enum.

Masz więcej pytań? Zostaw komentarz i powodzenia w kodowaniu!

---

**Ostatnia aktualizacja:** 2026-09-13  
**Testowano z:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose

## Powiązane tutoriale

- [Utwórz przeszukiwalny PDF z zeskanowanych plików przy użyciu Aspose Ocr](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline przetwarzania wstępnego OCR – jak rozpoznać tekst z obrazu](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Rozpoznaj tekst z obrazu przy użyciu Aspose Ocr – kompletny przewodnik C](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}