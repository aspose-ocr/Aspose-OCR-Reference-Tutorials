---
date: 2026-05-24
description: Dowiedz się, jak używać OCR z Aspose.OCR dla Javy, wyodrębniać tekst
  z obrazów, ustawiać dozwolone znaki i zastosować tymczasową licencję w kilka minut.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Określanie dozwolonych znaków w Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Jak korzystać z OCR – wyodrębniaj tekst z obrazów za pomocą Aspose.OCR
url: /pl/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR – Wyodrębniaj tekst z obrazów za pomocą Aspose.OCR

W nowoczesnych aplikacjach Java, **jak używać OCR** to częste pytanie, szczególnie gdy trzeba zamienić zeskanowane faktury, paragony lub wydrukowane formularze na przeszukiwalny tekst. Ten samouczek przeprowadzi Cię przez kompletny przykład **Aspose.OCR for Java**: wyodrębnianie tekstu z obrazów, ograniczanie wyniku do własnego zestawu znaków oraz zastosowanie tymczasowej licencji do szybkiej oceny.

## Szybkie odpowiedzi
- **Co robi Aspose.OCR?** Wyodrębnia tekst z obrazów z wysoką dokładnością i pozwala ograniczyć rozpoznawane znaki.  
- **Czy potrzebna jest licencja?** Tymczasowa lub stała licencja jest wymagana do użytku produkcyjnego; tymczasowy klucz usuwa znaki wodne.  
- **Jaką wersję JDK obsługuje?** Biblioteka działa z najnowszymi wersjami JDK (JDK 17, 19, 21).  
- **Czy mogę ograniczyć rozpoznawane znaki?** Tak — użyj metody `setAllowedCharacters`, aby ograniczyć wynik.  
- **Jak długo trwa konfiguracja?** Około 10‑15 minut dla podstawowej implementacji end‑to‑end.

## Co to jest „wyodrębnianie tekstu z obrazów”?
Wyodrębnianie tekstu z obrazów, znane również jako optyczne rozpoznawanie znaków (OCR), konwertuje wizualne znaki — drukowane, odręczne lub wpisane — na ciągi znaków czytelne dla maszyny. Ta transformacja umożliwia aplikacjom wyszukiwanie, indeksowanie, edytowanie i analizowanie treści programowo, wspierając przepływy pracy takie jak przetwarzanie faktur, archiwizacja dokumentów i automatyzacja wprowadzania danych.

## Dlaczego warto używać Aspose.OCR dla Javy?
Aspose.OCR obsługuje **ponad 60 języków**, może przetwarzać obrazy do **10 MB** bez ładowania całego pliku do pamięci i zapewnia **>95 % dokładności** przy czystych skanach. Biblioteka jest samodzielna, nie wymaga zewnętrznych silników OCR, co upraszcza wdrożenie i zmniejsza koszty licencjonowania.

## Wymagania wstępne

### Java Development Kit (JDK)

Upewnij się, że masz zainstalowany najnowszy Java Development Kit. Możesz go pobrać [tutaj](https://www.oracle.com/java/technologies/javase-downloads.html).

### Biblioteka Aspose.OCR dla Javy

Pobierz i zainstaluj bibliotekę Aspose.OCR dla Javy z [linku do pobrania](https://releases.aspose.com/ocr/java/).

### Licencja Aspose.OCR

Aby odblokować pełną funkcjonalność, zdobądź licencję. Możesz ją kupić [tutaj](https://purchase.aspose.com/buy) lub poprosić o [tymczasową licencję](https://purchase.aspose.com/temporary-license/) do celów testowych.

## Jak używać OCR z Aspose.OCR dla Javy?

Załaduj obraz, skonfiguruj silnik OCR i wywołaj metodę rozpoznawania — wszystko w kilku prostych linijkach. Ten bezpośredni akapit podpowiada, co zrobić: utwórz instancję `AsposeOCR` z ciągiem licencji, ustaw ewentualne dozwolone znaki i wywołaj `RecognizeLine` na docelowym obrazie, aby otrzymać wyodrębniony tekst. API obsługuje wstępne przetwarzanie obrazu wewnętrznie, więc otrzymujesz czyste wyniki bez dodatkowego kodu.

### Importowanie pakietów

Klasa `AsposeOCR` znajduje się w pakiecie `com.aspose.ocr`. Zaimportuj wymagane klasy przed rozpoczęciem kodowania.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Przewodnik krok po kroku

### Krok 1: Ustaw katalog dokumentów

Wybierz folder, w którym będą przechowywane wyniki OCR i pliki tymczasowe. Ścieżka ta będzie później używana do lokalizacji obrazu, który chcesz przetworzyć.

```java
String dataDir = "Your Document Directory";
```

### Krok 2: Określ ścieżkę do obrazu

Podaj pełną ścieżkę systemową lub lokalizację zasobu w class‑path, wskazującą na obraz, który chcesz przeanalizować.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Krok 3: Utwórz instancję Aspose.OCR

`AsposeOCR` to rdzeniowy silnik wykonujący rozpoznawanie optyczne. Utwórz go, podając tymczasowy lub stały ciąg licencji.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Krok 4: Wykonaj rozpoznawanie OCR

`RecognizeLine` wyodrębnia pojedynczą linię tekstu z podanego obrazu i zwraca ją jako zwykły `String` w Javie. Możesz wywoływać tę metodę wielokrotnie dla dokumentów wieloliniowych.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Wskazówka:** Jeśli potrzebujesz ograniczyć wynik tylko do cyfr (np. dla numerów faktur), wywołaj `setAllowedCharacters("0123456789")` na instancji `AsposeOCR` przed wywołaniem `RecognizeLine`. To zmusza silnik do ignorowania wszelkich znaków nie‑numerycznych.  
> `setAllowedCharacters` jest metodą `AsposeOCR`, która ogranicza wynik OCR do określonej białej listy znaków.

## Typowe problemy i rozwiązania

| Problem | Powód | Rozwiązanie |
|-------|--------|-----|
| **Brak wyniku lub pusty ciąg** | Nieprawidłowa ścieżka do obrazu lub nieobsługiwany format | Zweryfikuj `imagePath` i użyj obsługiwanego formatu (JPEG, PNG, BMP) |
| **Błędy rozpoznawania** | Obraz o niskiej rozdzielczości lub hałaśliwe tło | Przetwórz obraz wstępnie (zwiększ kontrast, binaryzuj) przed OCR |
| **Licencja nie zastosowana** | Brak lub nieprawidłowy klucz licencyjny | Upewnij się, że ciąg licencji jest poprawny i przekazany do konstruktora `AsposeOCR` |

## Najczęściej zadawane pytania

**P:** Jak mogę uzyskać tymczasową licencję dla Aspose.OCR?  
**O:** Odwiedź [stronę tymczasowej licencji](https://purchase.aspose.com/temporary-license/), aby poprosić o klucz próbny, który usuwa znaki wodne wersji ewaluacyjnej.

**P:** Gdzie mogę znaleźć wsparcie dla Aspose.OCR?  
**O:** Dołącz do społeczności na [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby uzyskać pomoc i dyskusje.

**P:** Czy mogę określić dozwolone znaki w Aspose.OCR?  
**O:** Tak, użyj API `setAllowedCharacters`, aby zdefiniować własną białą listę znaków. Jest to idealne dla pól zawierających wyłącznie liczby.

**P:** Czy Aspose.OCR jest kompatybilny z najnowszymi wersjami JDK?  
**O:** Zdecydowanie — Aspose.OCR jest regularnie aktualizowany, aby pozostawać kompatybilnym z najnowszymi wydaniami Javy.

**P:** Czy istnieją dodatkowe funkcje OCR poza rozpoznawaniem linii?  
**O:** Biblioteka obsługuje także rozpoznawanie bloków, akapitów i pełnych stron, pakiety językowe oraz zaawansowane przetwarzanie obrazu.

## Podsumowanie

Postępując zgodnie z tym **samouczkiem Aspose OCR Java**, teraz wiesz **jak używać OCR** do wyodrębniania tekstu z obrazów, ograniczania zestawu znaków i stosowania tymczasowej licencji do szybkiego testowania. Zagłęb się w pełną [dokumentację](https://reference.aspose.com/ocr/java/), aby poznać obsługę wielu języków, przetwarzanie wsadowe i własne potoki przetwarzania.

---

**Ostatnia aktualizacja:** 2026-05-24  
**Testowano z:** Aspose.OCR for Java 24.11  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Powiązane samouczki

- [Jak ustawić licencję i zweryfikować licencję Aspose.OCR w Javie](/ocr/java/ocr-basics/set-license/)
- [Konwertuj obraz na tekst w Javie przy użyciu Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Przykład Aspose OCR Java – Rozpoznawanie linii na obrazach](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}