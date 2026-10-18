---
category: general
date: 2025-12-30
description: Konwertuj obraz na PDF przy użyciu Aspose OCR w C#. Dowiedz się, jak
  wstępnie przetworzyć obraz pod OCR, rozpoznać obraz z koreańskim tekstem i szybko
  utworzyć przeszukiwalny plik PDF.
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: pl
og_description: Konwertuj obraz na PDF za pomocą Aspose OCR. Ten samouczek pokazuje,
  jak przygotować obraz do OCR, rozpoznać koreański tekst na obrazie oraz utworzyć
  przeszukiwalny obraz PDF.
og_title: Konwertuj obraz na PDF w C# – Kompletny przewodnik po OCR
tags:
- C#
- OCR
- Aspose
- PDF
title: Konwertuj obraz na PDF w C# – Kompletny przewodnik OCR
url: /pl/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie obrazu do PDF w C# – Kompletny przewodnik OCR

Czy kiedykolwiek potrzebowałeś **konwertować obraz do PDF**, ale jednocześnie chciałeś, aby tekst wewnątrz był przeszukiwalny? Nie jesteś jedyny. Wielu programistów napotyka ten sam problem przy pracy ze zeskanowanymi stronami, szczególnie tymi napisanymi po koreańsku. Dobrą wiadomością jest to, że z Aspose OCR możesz **przygotować obraz do OCR**, **rozpoznać obraz z tekstem koreańskim** i w końcu **utworzyć przeszukiwalny obraz PDF** w zaledwie kilku linijkach.

W tym samouczku przeprowadzimy Cię przez cały proces — od załadowania surowego pliku JPEG z koreańską stroną książki, jej oczyszczenia, wyodrębnienia tekstu i spakowania wszystkiego jako przeszukiwalny PDF. Po zakończeniu będziesz mieć gotową do uruchomienia aplikację konsolową C#, którą możesz wkleić do dowolnego projektu .NET.

## Czego będziesz potrzebować

- **.NET 6.0 lub nowszy** (kod działa zarówno na .NET Core, jak i .NET Framework)  
- **Aspose.OCR for .NET** pakiet NuGet (`Aspose.OCR`) – klucze trial dostępne na stronie Aspose.  
- Przykładowy obraz zawierający tekst koreański (np. `korean_book_page.jpg`).  
- Środowisko programistyczne według własnego wyboru (Visual Studio, VS Code, Rider — używam VS 2022).

> **Wskazówka:** Przechowuj pliki obrazów w dedykowanym folderze, takim jak `Resources/`, aby ścieżka była spójna na wszystkich maszynach.

## Przegląd procesu

1. **Zainicjalizuj silnik OCR** z obsługą GPU dla większej szybkości.  
2. **Dodaj filtry wstępnego przetwarzania** (prostowanie, odszumianie), aby poprawić dokładność rozpoznawania.  
3. **Pobierz i załaduj koreański model językowy** – Aspose robi to automatycznie w razie potrzeby.  
4. **Uruchom rozpoznawanie** na obrazie wejściowym.  
5. **Wyeksportuj wynik jako przeszukiwalny PDF** przy użyciu wbudowanego eksportera.  
6. **Opcjonalnie, serializuj wynik do JSON** w celu dalszej analizy lub logowania.

Poniżej rozłożymy każdy krok, wyjaśnimy *dlaczego* jest ważny i podamy dokładny kod, który możesz skopiować i wkleić.

---

## ## Konwertowanie obrazu do PDF – Pełny przepływ pracy

Poniższy fragment to *kompletny* program. Śmiało utwórz nowy projekt konsolowy (`dotnet new console -n OcrPdfDemo`) i zamień wygenerowany automatycznie `Program.cs` tym kodem.

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

- **Przyspieszenie GPU** skraca czas rozpoznawania mniej więcej o połowę w porównaniu do trybu wyłącznie CPU.  
- **Deskew** i **Denoise** to klasyczne techniki *przygotowania obrazu do OCR*; korygują typowe wady skanowania, które w przeciwnym razie powodują, że silnik pomija znaki.  
- **Ładowanie modelu językowego** jest niezbędne do **rozpoznania obrazu z tekstem koreańskim** – bez koreańskiego modelu silnik przejdzie na ogólny alfabet łaciński i wygeneruje bezużyteczne wyniki.  
- **SearchablePdfExporter** łączy oryginalny bitmap oraz niewidoczną warstwę tekstową, dając wynik **tworzenia przeszukiwalnego obrazu PDF**, który możesz indeksować w dowolnej przeglądarce PDF.

---

## ## Przygotowanie obrazu do OCR – Porady i triki

Choć dwa dodane filtry zazwyczaj wystarczają, możesz napotkać uparte obrazy. Oto kilka dodatkowych kroków, które możesz wypróbować:

| Problem | Dodatkowy filtr | Jak dodać |
|-------|-------------------|------------|
| Niski kontrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Silny szum tła | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mieszana orientacja (portret i krajobraz) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Uwaga:** Dodanie zbyt wielu filtrów może spowolnić przetwarzanie. Testuj każdą zmianę na jednej stronie przed skalowaniem.

## ## Rozpoznawanie obrazu z tekstem koreańskim – Typowe pułapki

Koreański skrypt zawiera sylaby Hangul, które są wizualnie gęste. Jeśli zauważysz zniekształcony wynik:

1. **Upewnij się, że model językowy został w pełni pobrany** – sprawdź konsolę pod kątem komunikatu takiego jak „Downloading Korean model…”.  
2. **Zwiększ `MaxAngle`** w `DeskewFilter`, jeśli Twoje skany są obrócone o więcej niż 12°.  
3. **Zwiększ pamięć GPU** ustawiając `ocrEngine.GpuMemoryLimit = 2048;` (wartość w MB).

Te korekty bezpośrednio wpływają na powodzenie **rozpoznania obrazu z tekstem koreańskim**.

## ## Tworzenie przeszukiwalnego obrazu PDF – Weryfikacja wyniku

Po zakończeniu programu otwórz `korean_page.pdf` w dowolnej przeglądarce PDF (Adobe Acrobat Reader, Foxit, nawet Chrome). Powinieneś móc:

- **Zaznaczyć tekst** myszą tak, jakby to był natywny PDF.  
- **Wyszukiwać** koreańskie słowa przy użyciu wbudowanego pola wyszukiwania.

Jeśli warstwa tekstowa jest pusta, sprawdź ponownie, czy metoda `Export` otrzymała poprawną ścieżkę obrazu oraz czy wynik OCR zawiera niepusty `RecognitionResult.Text`.

## ## Pełny wynik JSON – Czego się spodziewać

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

## ## Rozwiązywanie problemów i FAQ

**P: Mój PDF jest ogromny w porównaniu do oryginalnego obrazu.**  
O: Eksporter osadza oryginalny bitmap w jego natywnej rozdzielczości. Jeśli rozmiar jest problemem, zmniejsz obraz *przed* rozpoznaniem:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**P: OCR zwraca puste ciągi znaków.**  
O: Zweryfikuj, czy ścieżka obrazu jest poprawna i czy plik nie jest uszkodzony. Upewnij się także, że sterownik GPU jest aktualny; starsze sterowniki mogą powodować ciche awarie.

**P: Czy mogę przetwarzać wiele stron w pętli?**  
O: Oczywiście. Otocz kroki 4‑6 w pętlę `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` i odpowiednio zmień ścieżkę wyjściowego PDF.

## ## Zakończenie

Właśnie **konwertowaliśmy obraz do PDF**, zachowując przeszukiwalny tekst, wszystko dzięki potężnemu potokowi Aspose OCR. Poprzez **przygotowanie obrazu do OCR** zwiększasz dokładność; poprzez **rozpoznanie obrazu z tekstem koreańskim** obsługujesz złożone skrypty; a dzięki **tworzeniu przeszukiwalnego obrazu PDF** otrzymujesz przenośny, indeksowalny dokument.

Pobierz kod, skieruj go na własne skany i eksperymentuj z dodatkowymi filtrami lub modelami językowymi. Ten sam wzorzec działa dla chińskiego, japońskiego lub dowolnego języka opartego na alfabecie łacińskim — wystarczy zamienić `LanguageModel.Korean` na odpowiedni enum.

Masz więcej pytań? zostaw komentarz i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}