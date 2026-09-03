---
date: 2026-02-20
description: Dowiedz się, jak wyodrębniać tekst z obrazów przy użyciu Aspose.OCR dla
  Javy, ustawiać dozwolone znaki i stosować tymczasową licencję – kompletny samouczek
  Aspose OCR w Javie.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Wyodrębnianie tekstu z obrazów przy użyciu Aspose.OCR – Dozwolone znaki
url: /pl/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazów przy użyciu Aspose.OCR – Dozwolone znaki

## Wprowadzenie

Wyodrębnianie tekstu z obrazów jest powszechnym wymaganiem we współczesnych aplikacjach — niezależnie od tego, czy przetwarzasz faktury, skanujesz paragony, czy digitalizujesz wydrukowane dokumenty. W tym tutorialu przeprowadzimy Cię przez kompletny **aspose ocr java tutorial**, który pokazuje, jak **extract text from images** przy użyciu Aspose.OCR dla Java, ustawić dozwolone znaki oraz zastosować tymczasową licencję podczas testowania biblioteki.

## Szybkie odpowiedzi
- **Co robi Aspose.OCR?** Wyodrębnia tekst z obrazów z wysoką dokładnością i obsługuje niestandardowe zestawy znaków.  
- **Czy potrzebuję licencji?** Tymczasowa lub stała licencja jest wymagana do użytku produkcyjnego.  
- **Która wersja JDK jest obsługiwana?** Najnowsze wydania JDK są w pełni kompatybilne.  
- **Czy mogę ograniczyć rozpoznawane znaki?** Tak — użyj API `setAllowedCharacters`, aby ograniczyć wynik.  
- **Jak długo trwa konfiguracja?** Około 10‑15 minut dla podstawowej implementacji.

## Co to jest „wyodrębnianie tekstu z obrazów”?
Wyodrębnianie tekstu z obrazów odnosi się do procesu konwersji wizualnego tekstu (np. drukowanego lub odręcznego) na ciągi znaków czytelne dla maszyny. Umożliwia to dalsze zadania, takie jak wyszukiwanie, indeksowanie czy analiza danych.

## Dlaczego używać Aspose.OCR dla Java?
- **Wysoka dokładność** w wielu językach i czcionkach.  
- **Proste API** integrujące się z każdym projektem Java.  
- **Konfigurowalne** zestawy znaków, pakiety językowe i przetwarzanie wstępne obrazu.  
- **Brak zewnętrznych zależności** — biblioteka jest samodzielna.

## Prerequisites

Before you start, make sure you have the following:

### Java Development Kit (JDK)

Upewnij się, że masz zainstalowany najnowszy Java Development Kit na swoim systemie. Możesz go pobrać [tutaj](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Pobierz i zainstaluj bibliotekę Aspose.OCR for Java z [linku do pobrania](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

Aby uzyskać pełny potencjał Aspose.OCR, zdobądź ważną licencję. Możesz ją uzyskać [tutaj](https://purchase.aspose.com/buy) lub wypróbować [tymczasową licencję](https://purchase.aspose.com/temporary-license/) na okres próbny.

## Jak zastosować tymczasową licencję

Podczas oceny produktu tymczasowa licencja usuwa znak wodny oceny i odblokowuje pełną funkcjonalność na ograniczony czas. Utwórz ciąg licencji w portalu Aspose, a następnie przekaż go do konstruktora `AsposeOCR`, jak pokazano w przykładzie kodu poniżej. Dla wdrożeń produkcyjnych zamień tymczasowy klucz na swoją stałą licencję.

## Porady dotyczące wstępnego przetwarzania obrazu OCR

Dobra jakość obrazu dramatycznie poprawia wyniki rozpoznawania. Przed wywołaniem silnika OCR rozważ:

- Konwertowanie obrazu na skalę szarości.  
- Zwiększanie kontrastu, aby znaki były wyraźniejsze.  
- Usuwanie szumu tła przy użyciu filtru binarizacji.  
- Zmiana rozmiaru obrazów o niskiej rozdzielczości do co najmniej 300 dpi.

These steps are part of **ocr image preprocessing** and can be performed with any standard Java imaging library before invoking Aspose.OCR.

## Importowanie pakietów

Once the prerequisites are ready, import the necessary packages into your Java project:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Przewodnik krok po kroku

### Krok 1: Ustaw katalog dokumentu

Zdefiniuj folder, w którym będziesz przechowywać wyniki przetworzone przez OCR. Ścieżka ta będzie użyta później do zlokalizowania pliku obrazu.

```java
String dataDir = "Your Document Directory";
```

### Krok 2: Określ ścieżkę do obrazu

Wskaż API na obraz, który chcesz analizować.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Krok 3: Utwórz instancję Aspose.OCR

Zainicjuj silnik OCR przy użyciu klucza licencyjnego. Klucz może być tymczasowym lub stałym ciągiem licencji.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Krok 4: Przeprowadź rozpoznawanie OCR

Wywołaj metodę `RecognizeLine`, aby wyodrębnić linię tekstu z obrazu. Wynik to zwykły ciąg znaków, który możesz dalej przetwarzać lub przechowywać.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Wskazówka:** Jeśli potrzebujesz ograniczyć wynik do określonego zestawu znaków (np. tylko cyfry), użyj metody `setAllowedCharacters` na instancji `AsposeOCR` przed wywołaniem `RecognizeLine`. To zapewnia, że silnik ignoruje wszystkie znaki spoza zdefiniowanego zestawu.

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| **Brak wyniku lub pusty ciąg** | Nieprawidłowa ścieżka do obrazu lub nieobsługiwany format obrazu | Sprawdź `imagePath` i użyj obsługiwanego formatu (JPEG, PNG, BMP) |
| **Błędy rozpoznawania** | Obraz o niskiej rozdzielczości lub zaszumione tło | Wstępnie przetwórz obraz (zwiększ kontrast, binarizuj) przed OCR |
| **Licencja nie zastosowana** | Brak lub nieprawidłowy klucz licencji | Upewnij się, że ciąg licencji jest poprawny i umieszczony w konstruktorze `AsposeOCR` |

## Najczęściej zadawane pytania

**P: Jak mogę uzyskać tymczasową licencję dla Aspose.OCR?**  
A: Odwiedź [stronę tymczasowej licencji](https://purchase.aspose.com/temporary-license/), aby zamówić licencję próbną.

**P: Gdzie mogę znaleźć wsparcie dla Aspose.OCR?**  
A: Dołącz do społeczności na [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby uzyskać pomoc i dyskusje.

**P: Czy mogę określić dozwolone znaki w Aspose.OCR?**  
A: Tak, możesz dostosować zestaw znaków przy użyciu API `setAllowedCharacters`. Zapoznaj się z oficjalną dokumentacją po szczegóły.

**P: Czy Aspose.OCR jest kompatybilny z najnowszymi wersjami JDK?**  
A: Absolutnie — Aspose.OCR jest regularnie aktualizowany, aby pozostać kompatybilnym z najnowszymi wydaniami Java.

**P: Czy istnieją dodatkowe funkcje OCR poza rozpoznawaniem linii?**  
A: Tak, biblioteka obsługuje rozpoznawanie bloków, akapitów i pełnych stron, a także pakiety językowe i opcje przetwarzania wstępnego obrazu.

## Zakończenie

Postępując zgodnie z tym **aspose ocr java tutorial**, masz teraz działające rozwiązanie do **extract text from images** oraz kontrolowania, które znaki są rozpoznawane. Zapoznaj się z pełną [dokumentacją](https://reference.aspose.com/ocr/java/), aby odkryć zaawansowane funkcje, takie jak obsługa wielu języków, niestandardowe przetwarzanie wstępne i przetwarzanie wsadowe.

---

**Ostatnia aktualizacja:** 2026-02-20  
**Testowano z:** Aspose.OCR for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}