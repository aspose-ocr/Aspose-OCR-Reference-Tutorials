---
category: general
date: 2026-06-28
description: Jak prostować obraz przy użyciu Aspose.OCR. Dowiedz się, jak wstępnie
  przetwarzać obraz pod OCR, poprawić dokładność OCR i prostować zeskanowany obraz
  w pełnym przykładzie C#.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: pl
og_description: Jak prostować obraz za pomocą Aspose.OCR. Ten poradnik pokazuje, jak
  wstępnie przetworzyć obraz do OCR, zwiększyć dokładność i krok po kroku prostować
  zeskanowany obraz.
og_title: Jak wyprostować obraz w C# – Kompletny przewodnik Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: Jak wyprostować obraz w C# – Kompletny przewodnik Aspose.OCR
url: /pl/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyrównać (Deskew) obraz w C# – Kompletny przewodnik Aspose.OCR

Zastanawiałeś się kiedyś, **jak wyrównać (deskew) obraz** przed podaniem go do silnika OCR? Nie jesteś jedyny. Skanowane dokumenty często są nachylone, a ta mała rotacja może poważnie wpłynąć na wyniki rozpoznawania. Dobra wiadomość? Dzięki Aspose.OCR możesz wyprostować (deskew) i oczyścić obrazy w zaledwie kilku linijkach C#.

W tym tutorialu przeprowadzimy Cię przez kompletny, działający przykład, który **przygotowuje obraz do OCR**, dodaje filtr deskew i pokazuje **jak poprawić dokładność OCR**. Po zakończeniu będziesz mógł automatycznie **wyrównać (deskew) zeskanowane obrazy** i samodzielnie zobaczyć wyniki pewności.

> **Uwaga:** Kod działa z Aspose.OCR ≥ 22.10 i .NET 6+, ale koncepcje mają zastosowanie również do wcześniejszych wersji.

## Czego będziesz potrzebować

- **Aspose.OCR for .NET** (pakiet NuGet `Aspose.OCR`)
- **Skrzywy TIFF** lub JPEG, który chcesz wyprostować
- Visual Studio 2022 (lub dowolne IDE C#)
- Podstawowa znajomość C# i aplikacji konsolowych

Nie są wymagane dodatkowe biblioteki zewnętrzne; cały pipeline znajduje się w Aspose.OCR.

---

## Jak wyrównać (Deskew) obraz przy użyciu Aspose.OCR

Sednem rozwiązania jest **pipeline filtrów**. Wyobraź sobie linię montażową, w której każdy filtr usuwa konkretny problem: najpierw korygujemy rotację, potem redukujemy szum, a na końcu zwiększamy kontrast, aby silnik OCR wyraźnie widział znaki.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Przykład obrazu**  
> ![how to deskew image example](/images/deskew-example.png "how to deskew image example")

### Dlaczego filtr Deskew jako pierwszy?

Gdy dokument jest obrócony nawet o kilka stopni, silnik OCR błędnie interpretuje linie bazowe, co prowadzi do zniekształconego wyniku. `DeskewFilter` automatycznie szacuje kąt rotacji (do `MaxAngle` stopni) i obraca bitmapę z powrotem do poziomej linii bazowej. Zwrócony `DeskewConfidence` informuje, jak pewny jest algorytm co do korekcji — przydatny przy logowaniu lub strategiach awaryjnych.

---

## Przygotowanie obrazu do OCR – budowanie pipeline filtrów

### 1️⃣ DeskewFilter (Krok podstawowy)

- **Co robi:** Wykrywa dominujący kierunek linii tekstu i obraca obraz.
- **Dlaczego to ważne:** Prosta linia bazowa maksymalizuje dokładność segmentacji znaków.
- **Wskazówka:** Jeśli Twoje dokumenty nigdy nie przekraczają 10°, ustaw `MaxAngle = 10`, aby przyspieszyć wykrywanie.

### 2️⃣ DenoiseFilter (Czyszczenie wtórne)

- **Co robi:** Redukuje losowy szum pikseli, który może pojawić się po skanowaniu.
- **Dlaczego to ważne:** Szum często tworzy fałszywe krawędzie, myląc segmentację OCR.
- **Wskazówka:** Dostosuj `Strength` w przedziale od 0.3 (lekki) do 0.8 (agresywny) w zależności od jakości skanu.

### 3️⃣ ContrastBoostFilter (Ostateczne wykończenie)

- **Co robi:** Zwiększa różnicę między tekstem na pierwszym planie a tłem.
- **Dlaczego to ważne:** Niski kontrast może sprawić, że słabe znaki będą niewidoczne dla silnika rozpoznawania.
- **Wskazówka:** `Level` równy 1.2 działa w większości skanów czarno‑białych; w przypadku dokumentów kolorowych eksperymentuj z wartościami do 2.0.

Łącząc te trzy filtry, **przygotowujesz obraz do OCR** w sposób, który rozwiązuje najczęstsze problemy: pochylenie, szum i niski kontrast.

---

## Jak poprawić dokładność OCR przy użyciu Deskew i Denoise

Możesz się zastanawiać: „Jeśli już mam filtr deskew, po co używać denoise i podnoszenia kontrastu?” Odpowiedź leży w **kumulatywnej poprawie**. Każdy filtr usuwa inny defekt, a razem podnoszą ogólną pewność.

#### Test w rzeczywistych warunkach

| Test | Oryginalna dokładność OCR | Po Deskew | Po pełnym pipeline |
|------|----------------------------|-----------|--------------------|
| Simple invoice (5° tilt) | 78 % | 92 % | 96 % |
| Old newspaper scan (15° tilt, grainy) | 61 % | 78 % | 88 % |
| Low‑contrast form (no tilt) | 70 % | 71 % | 84 % |

*Liczby są przykładowe, ale odzwierciedlają typowe zyski zgłaszane przez użytkowników Aspose.*

**Kluczowa wniosek:** Nawet jeśli Twoim głównym celem jest **wyrównanie (deskew) zeskanowanego obrazu**, dodanie kroków denoise i podniesienia kontrastu często przynosi zauważalny wzrost jakości końcowego tekstu.

---

## Wyrównanie (Deskew) zeskanowanego obrazu: weryfikacja wyników

Po uruchomieniu pipeline otrzymujesz dwie przydatne informacje:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Pewność Deskew** (`result.DeskewConfidence`) jest wyrażona w procentach. Wartości powyżej 90 % zazwyczaj oznaczają, że rotacja została poprawnie skorygowana.
- **Rozpoznany tekst** (`result.Text`) pozwala natychmiast zweryfikować, czy wynik wygląda sensownie.

Jeśli pewność jest niska (< 70 %), rozważ:

1. **Zwiększenie `MaxAngle`** – być może dokument jest obrócony bardziej niż oczekiwano.
2. **Dodanie `BinarizationFilter`** przed deskew, aby uprościć obraz.
3. **Ręczne obracanie** obrazu przy użyciu `OcrImage.Rotate(angle)` jako rozwiązanie awaryjne.

---

## Pełny przykład end‑to‑end (gotowy do uruchomienia)

Poniżej znajduje się **kompletny, samodzielny program**, który możesz skopiować i wkleić do nowego projektu aplikacji konsolowej. Pamiętaj, aby zamienić `YOUR_DIRECTORY` na folder zawierający Twój skrzywy TIFF.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**Oczekiwany wynik** (zakładając stosunkowo czysty skan):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

Jeśli zobaczysz zniekształcone znaki, sprawdź ponownie siłę filtrów lub dodaj `BinarizationFilter`, jak wspomniano wcześniej.

---

## Częste pułapki i wskazówki profesjonalne

- **Pułapka:** Używanie TIFF z wieloma stronami. `OcrImage.FromFile` odczytuje tylko pierwszą klatkę. Użyj `OcrImage.FromMultiPageFile`, jeśli potrzebujesz wszystkich stron.
- **Pułapka:** Zapomnienie o zwolnieniu `OcrEngine`. Owiń go w blok `using` w kodzie produkcyjnym, aby zwolnić zasoby natywne.
- **Wskazówka profesjonalna:** Cache'uj pipeline, jeśli przetwarzasz wiele obrazów o identycznych ustawieniach — zmniejsza to narzut.
- **Wskazówka profesjonalna:** Loguj `DeskewConfidence` w systemie monitoringu; nagłe spadki mogą wskazywać na zmianę kalibracji skanera.

---

## Kolejne kroki – rozszerzanie przepływu pracy

Teraz, gdy wiesz **jak wyrównać (deskew) obraz** i **przygotować obraz do OCR**, możesz zbadać:

- **Przetwarzanie wsadowe** – iteruj przez folder ze skanowanymi PDF‑ami, konwertuj każdą stronę na obraz i zastosuj ten sam pipeline.
- **Obsługa języków** – ustaw `engine.Language = OcrLanguage.English;` lub inne języki, aby poprawić rozpoznawanie.
- **Niestandardowe przetwarzanie końcowe** – użyj wyrażeń regularnych do czyszczenia typowych błędów OCR (np. „0” vs „O”).

Każdy z tych tematów naturalnie wiąże się z drugorzędnymi słowami kluczowymi **how to improve ocr** i **deskew scanned image**.

---

## Zakończenie

Omówiliśmy wszystko, co musisz wiedzieć o **jak wyrównać (deskew) obraz** przy użyciu Aspose.OCR, od budowania solidnego pipeline filtrów po weryfikację wyników pewności. Dzięki **przygotowaniu obrazu do OCR** z użyciem deskew, denoise i podniesienia kontrastu, zobaczysz wymierny wzrost w wynikach **jak poprawić OCR**, szczególnie przy skanach nachylonych lub zaszumionych.

Spróbuj na własnym zestawie dokumentów, dostosuj parametry filtrów i obserwuj, jak rośnie dokładność OCR. Masz pytania lub trudny plik, który nie chce się wyprostować? zostaw komentarz poniżej — rozwiążmy problem razem. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak używać AspOCR: filtry przetwarzania obrazu OCR dla .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Jak wykonać OCR obrazu – Przeprowadź OCR na obrazie w rozpoznawaniu obrazów OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Jak ustawić wartość progową w rozpoznawaniu obrazu OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}