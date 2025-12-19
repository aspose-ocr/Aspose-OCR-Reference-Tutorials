---
date: 2025-12-06
description: Dowiedz się, jak używać Aspose.OCR dla Javy do przeprowadzania rozpoznawania
  tekstu OCR, wyodrębniania tekstu z obrazów i przygotowywania prostokątów do ukierunkowanego
  rozpoznawania.
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Przygotowywanie prostokątów do rozpoznawania tekstu OCR w Aspose.OCR
url: /pl/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przygotowywanie prostokątów do rozpoznawania tekstu OCR w Aspose.OCR

## Wprowadzenie

W dzisiejszym świecie napędzanym danymi, **ocr text recognition** jest podstawą do przekształcania zeskanowanych dokumentów, zrzutów ekranu i zdjęć w treść możliwą do przeszukiwania i edycji. Aspose.OCR for Java sprawia, że proces ten jest szybki i niezawodny, szczególnie gdy musisz skupić się na konkretnych obszarach obrazu. W tym samouczku przeprowadzimy Cię przez każdy krok niezbędny do przygotowania prostokątów, które ograniczają OCR do interesujących Cię regionów, dając precyzyjną kontrolę i lepszą wydajność.

## Szybkie odpowiedzi
- **Jaką bibliotekę obsługuje rozpoznawanie tekstu OCR w Javie?** Aspose.OCR for Java.  
- **Czy potrzebna jest licencja do użytku produkcyjnego?** Tak – ważna licencja Aspose.OCR odblokowuje pełną funkcjonalność.  
- **Czy mogę ograniczyć OCR do określonych części obrazu?** Oczywiście; definiujesz prostokąty, które ograniczają docelowe strefy.  
- **Jakie są główne wymagania wstępne?** JDK 17+, Aspose.OCR for Java oraz środowisko IDE Java.  
- **Czy to podejście nadaje się do wyodrębniania tekstu z obrazów?** Tak, jest to efektywny sposób na **extract text image java** projekty.

## Czym jest rozpoznawanie tekstu OCR?
OCR (Optical Character Recognition) text recognition konwertuje obrazy pikselowe na znaki czytelne dla maszyny. Umożliwia to wyszukiwanie, edytowanie i analizowanie treści, które pierwotnie istnieją wyłącznie jako obrazy.

## Dlaczego przygotowywać prostokąty do rozpoznawania tekstu OCR?
Definiowanie prostokątów skupia silnik na regionach, które faktycznie zawierają tekst, co:
* Zmniejsza czas przetwarzania.
* Poprawia dokładność, ignorując szum tła.
* Umożliwia wyodrębnienie tylko potrzebnych danych — idealne dla formularzy, faktur i paragonów.

## Prerequisites

Before you start, make sure you have:

- **Java Development Kit (JDK)** – Aspose.OCR for Java działa z JDK 17 lub nowszym. Pobierz go ze strony Oracle.
- **Aspose.OCR for Java library** – Pobierz najnowszy plik JAR z oficjalnej strony pobierania [tutaj](https://releases.aspose.com/ocr/java/). Postępuj zgodnie z przewodnikiem instalacji [tutaj](https://reference.aspose.com/ocr/java/).
- **Środowisko programistyczne** – Każde IDE Java (IntelliJ IDEA, Eclipse, VS Code itp.) będzie odpowiednie.

## Import Packages

In your Java source file, import the required Aspose.OCR classes and standard Java utilities:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *Importujemy `java.awt.Rectangle`, ponieważ API OCR oczekuje prostokątów definiujących obszary do skanowania.*

## Krok 1: Konfiguracja licencji

```java
SetLicense.main(null);
```

Wywołanie `SetLicense` aktywuje Twoją licencję Aspose.OCR, usuwając ograniczenia wersji próbnej i umożliwiając pełne rozpoznawanie tekstu OCR.

## Krok 2: Definiowanie katalogu dokumentu i ścieżki obrazu

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

Zastąp `"Your Document Directory"` absolutną ścieżką, w której znajduje się Twój obraz (`p.png`). To jest obraz, który zostanie przetworzony.

## Krok 3: Utworzenie instancji AsposeOCR

```java
AsposeOCR api = new AsposeOCR();
```

Instancjonowanie `AsposeOCR` zapewnia dostęp do metody `RecognizePage`, która wykonuje rzeczywiste OCR.

## Krok 4: Przygotowanie prostokątów z tekstem

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Każdy `Rectangle(x, y, width, height)` informuje AsposeOCR dokładnie, gdzie szukać tekstu. Dostosuj współrzędne, aby pasowały do układu Twojego obrazu źródłowego.

## Krok 5: Wykonanie rozpoznawania OCR

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

Wywołanie `RecognizePage` przetwarza tylko zdefiniowane prostokąty i zwraca wyodrębniony ciąg znaków. Wyjście w konsoli pozwala natychmiast zweryfikować wynik **ocr text recognition**.

## Typowe problemy i wskazówki

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| **Brak wyjścia** | Nieprawidłowe współrzędne prostokątów lub ścieżka obrazu | Sprawdź ponownie wartość `dataDir` i upewnij się, że prostokąty rzeczywiście obejmują obszary z tekstem. |
| **Zniekształcone znaki** | Obraz o niskiej rozdzielczości lub nieobsługiwana czcionka | Użyj obrazu o wyższej rozdzielczości lub zastosuj wstępne przetwarzanie obrazu (np. binaryzację). |
| **Licencja nie zastosowana** | `SetLicense` nie został wywołany przed OCR | Upewnij się, że `SetLicense.main(null);` uruchamia się przed jakimikolwiek wywołaniami API. |
| **Spowolnienie wydajności** | Zbyt wiele dużych prostokątów | Ogranicz liczbę prostokątów i utrzymuj je jak najściślej wokół tekstu. |

## Zakończenie

Nauczyłeś się teraz, jak zintegrować Aspose.OCR for Java, skonfigurować licencję, zdefiniować ścieżki do obrazów oraz — co najważniejsze — przygotować prostokąty, aby skupić **ocr text recognition** na konkretnych częściach obrazu. Ta technika jest idealna dla każdego **java ocr tutorial**, który wymaga precyzyjnego, wysokowydajnego wyodrębniania tekstu.

## Najczęściej zadawane pytania

**P: Czy Aspose.OCR jest kompatybilny z innymi językami programowania?**  
O: Tak, Aspose.OCR obsługuje także .NET, C++ i Pythona. Sprawdź oficjalną dokumentację, aby zobaczyć przykłady specyficzne dla języka.

**P: Czy mogę używać Aspose.OCR w projekcie komercyjnym?**  
O: Oczywiście. Kup licencję komercyjną poprzez [sklep Aspose](https://purchase.aspose.com/buy).

**P: Czy dostępna jest darmowa wersja próbna?**  
O: Tak, możesz pobrać wersję próbną [tutaj](https://releases.aspose.com/).

**P: Jak uzyskać tymczasową licencję do oceny?**  
O: Tymczasowe licencje są dostępne poprzez [portal tymczasowych licencji Aspose](https://purchase.aspose.com/temporary-license/).

**P: Gdzie mogę uzyskać wsparcie społeczności?**  
O: Odwiedź [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16), aby zadawać pytania, uzyskać wskazówki i przykłady kodu.

---

**Ostatnia aktualizacja:** 2025-12-06  
**Testowano z:** Aspose.OCR for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
