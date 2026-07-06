---
category: general
date: 2026-06-22
description: 'Jak wyprostować obraz do OCR: poznaj kroki wstępnego przetwarzania obrazu
  w OCR, usuń szum solno‑pieprzowy i zwiększ dokładność.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: pl
og_description: Jak wyrównać obraz pod OCR, usunąć szum solno‑pieprzowy i zastosować
  techniki wstępnego przetwarzania obrazów OCR w kompletnym przykładzie w Javie.
og_title: Jak prostować obraz – Przewodnik po przetwarzaniu obrazu w OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Jak prostować obraz – Przewodnik po przetwarzaniu obrazu w OCR
url: /pl/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak prostować obraz – Przewodnik po przetwarzaniu obrazu OCR

Zastanawiałeś się kiedyś **jak prostować obraz**, aby Twój silnik OCR naprawdę odczytywał tekst? Nie jesteś jedyny. Przechylony skan może zamienić idealny dokument w zniekształcony bałagan, a większość programistów natrafia na ten problem przynajmniej raz.

W tym samouczku przeprowadzimy pełną **image preprocessing OCR** pipeline, która nie tylko koryguje obrót, ale także **usuwa szum solny i pieprzowy** oraz zwiększa kontrast — w zasadzie wszystko, czego potrzebujesz, aby **przetwarzać obrazy w stylu OCR** przed przekazaniem ich do silnika. Po zakończeniu będziesz mieć gotowy do uruchomienia fragment kodu Java oraz jasny model mentalny, dlaczego każdy krok ma znaczenie.

## Jak prostować obraz – Budowanie pipeline przetwarzania wstępnego

Serce każdego przepływu pracy przyjaznego OCR to obiekt **preprocess options**, który łączy szereg filtrów. Pomyśl o nim jak o taśmie produkcyjnej: każdy filtr wykonuje jedną czynność, a następnie przekazuje obraz do kolejnego. Poniżej znajduje się minimalny, ale kompletny przykład używający hipotetycznej biblioteki OCR, która zawiera `DeskewFilter`, `DenoiseFilter` i `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Dlaczego to działa

* **DeskewFilter** analizuje dominujące linie tekstu na obrazie, szacuje kąt i obraca bitmapę z powrotem do poziomu. Większość bibliotek ogranicza korekcję do ±15°, ponieważ większe kąty zazwyczaj wskazują na źle zeskanowaną stronę, wymagającą ręcznej interwencji.
* **DenoiseFilter** usuwa klasyczny wzorzec *salt‑and‑pepper* — te pojedyncze czarne lub białe piksele przypominające szum na telewizorze. Ich usunięcie zapobiega pomyleniu szumu z znakami przez silnik OCR.
* **ContrastBoostFilter** rozciąga histogram, uwydatniając słabe kreski. Mnożnik `1.5f` jest bezpiecznym domyślnym ustawieniem; możesz go zwiększyć, jeśli Twoje skany są szczególnie wyblakłe.

> **Pro tip:** Jeśli wiesz, że Twoje dokumenty nigdy nie przekraczają przechyłu 10°, przekaż tę mniejszą granicę do `DeskewFilter` — algorytm działa szybciej i rzadziej nadmiernie koryguje.

## Przetwarzanie obrazu OCR: Dodawanie filtrów w właściwej kolejności

Kolejność ma znaczenie. Wyobraź sobie, że odszumiasz *przed* prostowaniem; szum może zaburzyć wykrywanie kąta, prowadząc do nieprawidłowego wyniku. Natomiast zastosowanie zwiększenia kontrastu *po* prostowaniu zapewnia, że obrót nie wprowadza nowych artefaktów.

Poniżej znajduje się szybka lista kontrolna, którą możesz skopiować i wkleić do dowolnego projektu:

| Krok | Filtr | Powód |
|------|--------|--------|
| 1 | `DeskewFilter` | Wyrównuje linię bazową tekstu |
| 2 | `DenoiseFilter` | Usuwa izolowany szum pikselowy |
| 3 | `ContrastBoostFilter` | Zwiększa czytelność dla OCR |

Jeśli potrzebujesz wstawić dodatkowe kroki — na przykład filtr **binarization** dla binarnego OCR — umieścisz go **po** zwiększeniu kontrastu, ponieważ czysty, wysokokontrastowy obraz binaryzuje się dokładniej.

## Usuwanie szumu solnego i pieprzowego za pomocą DenoiseFilter

Szum *salt‑and‑pepper* jest notoryczny w niskiej jakości skanach, szczególnie pochodzących z tanich aparatów telefonicznych. `DenoiseFilter` w naszej bibliotece implementuje kernel medianowy, który zastępuje każdy piksel medianą z otaczającego go sąsiedztwa. Efekt? Te plamki znikają bez rozmywania rzeczywistych znaków.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Kiedy zwiększyć rozmiar kernela?* Jeśli Twoje obrazy źródłowe są pełne dużych plamek, większy kernel je oczyści, ale uwaga: zbyt duży może zacząć wymazywać drobne kreski w małych czcionkach.

## Przetwarzanie obrazów OCR – Zastosowanie pipeline

Gdy już zbudujesz łańcuch filtrów, podłączenie go do silnika to jednowierszowy kod (`engine.setPreprocessOptions`). Od tego momentu każde wywołanie `recognizeText` automatycznie przechodzi przez pipeline. Nie musisz ręcznie wywoływać każdego filtra — Twój kod pozostaje schludny, a przyszłe zmiany (dodawanie nowego filtra, dostrajanie parametrów) są scentralizowane.

Oto jak wygląda udane uruchomienie przy przykładowym skanie, który pierwotnie miał przechył 12° i widoczny szum pepper:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Zauważ, że tekst jest czysty, prawidłowo ustawiony i wolny od niechcianych znaków, które w przeciwnym razie pojawiłyby się jako „I n v o i c e” lub „$‑‑‑”.

## Przypadki brzegowe i typowe pułapki

| Sytuacja | Na co zwrócić uwagę | Sugerowane rozwiązanie |
|-----------|-------------------|---------------|
| Obrót > 15° | DeskewFilter może się poddać | Przedobrób ręcznie lub użyj filtra o szerszym zakresie |
| Bardzo niska rozdzielczość ( < 100 dpi ) | Zwiększenie kontrastu nie odzyska szczegółów | Najpierw przeskaluj obraz (np. `ResampleFilter`) |
| Mieszany szum (Gaussian + salt‑pepper) | Sam `DenoiseFilter` nie wystarczy | Dodaj `GaussianBlurFilter` przed `DenoiseFilter` |
| Skanowanie w kolorze z kolorowym tekstem | Wymagana konwersja do odcieni szarości | Wstaw `GrayscaleFilter` przed zwiększeniem kontrastu |

Przewidując te scenariusze, zaoszczędzisz sobie później godziny debugowania.

## Pełny działający przykład (Wszystko w jednym)

Poniżej znajduje się samodzielna klasa Java, którą możesz wkleić do dowolnego projektu Maven lub Gradle zawierającego zależność `com.example.ocr`. Demonstracja **jak prostować obraz**, **usuwać szum solny i pieprzowy** oraz **przetwarzać obrazy w stylu OCR**.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Oczekiwany wynik** (zakładając, że `scanned-document.png` zawiera czytelną fakturę):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Jeśli wymienisz obraz na taki, który jest już idealnie wyrównany, zauważysz, że pipeline nadal działa — nic się nie psuje, a dokładność OCR pozostaje wysoka.

## Podsumowanie

Masz teraz solidne pojęcie o **jak prostować obraz** i dlaczego każdy krok przetwarzania wstępnego — **image preprocessing OCR**, **remove salt pepper** i **preprocess images OCR** — odgrywa kluczową rolę w dostarczaniu czystego, przeszukiwalnego tekstu. Powyższy przykład jest kompletny,

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak używać AspOCR: Filtry przetwarzania obrazu OCR dla .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Obliczanie kąta przechylenia dla przetwarzania obrazu OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Jak ustawić wartość progową w rozpoznawaniu obrazu OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}