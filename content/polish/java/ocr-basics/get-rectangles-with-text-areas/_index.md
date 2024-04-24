---
title: Uzyskiwanie prostokątów z obszarami tekstowymi w Aspose.OCR
linktitle: Uzyskiwanie prostokątów z obszarami tekstowymi w Aspose.OCR
second_title: Aspose.OCR API Java
description: Odblokuj moc Aspose.OCR dla Java. Z tego przewodnika krok po kroku dowiesz się, jak płynnie wyodrębniać tekst z obrazów. Pobierz teraz, aby efektywnie rozpoznawać tekst.
type: docs
weight: 12
url: /pl/java/ocr-basics/get-rectangles-with-text-areas/
---
## Wstęp

Czy chcesz zintegrować zaawansowane funkcje optycznego rozpoznawania znaków (OCR) ze swoją aplikacją Java? Aspose.OCR dla Java to idealne rozwiązanie do dokładnego i wydajnego wyodrębniania tekstu z obrazów. Ten samouczek poprowadzi Cię przez proces uzyskiwania prostokątów z obszarami tekstowymi przy użyciu Aspose.OCR, pomagając w wykorzystaniu pełnego potencjału tej biblioteki Java OCR.

## Warunki wstępne

Zanim przejdziesz do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:

- Środowisko programistyczne Java: Upewnij się, że masz zainstalowaną Javę w swoim systemie.
-  Aspose.OCR dla biblioteki Java: Pobierz i skonfiguruj bibliotekę Aspose.OCR. Możesz znaleźć link do pobrania[Tutaj](https://releases.aspose.com/ocr/java/).

## Importuj pakiety

W swoim projekcie Java zaimportuj niezbędne pakiety, aby wykorzystać funkcjonalności Aspose.OCR:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Krok 1: Skonfiguruj swój projekt

Upewnij się, że masz gotowy projekt Java i zintegrowaną bibliotekę Aspose.OCR.

## Krok 2: Zdefiniuj katalog dokumentów i ścieżkę obrazu

```java
// Ścieżka do katalogu dokumentów.
String dataDir = "Your Document Directory";

// Ścieżka obrazu
String imagePath = dataDir + "p3.png";
```

## Krok 3: Utwórz instancję Aspose.OCR

```java
// Utwórz instancję Aspose.OCR
AsposeOCR api = new AsposeOCR();
```

## Krok 4: Rozpoznaj tekst na obrazie

```java
try {
    // Rozpoznaj stronę po pełnej ścieżce do pliku
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Krok 5: Uzyskaj prostokąty z obszarami tekstowymi

```java
// Uzyskaj prostokąty z obszarami tekstowymi na obrazie.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Wydrukuj każdy prostokąt obszaru tekstowego
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Wniosek

W tym samouczku nauczyłeś się, jak zintegrować Aspose.OCR dla Java ze swoim projektem, aby efektywnie wyodrębniać tekst z obrazów. Aspose.OCR upraszcza zadania OCR, zapewniając dokładne wyniki i bezproblemową obsługę użytkownika.

## Często zadawane pytania

### P1: Czy Aspose.OCR jest kompatybilny z Java 11?

O1: Tak, Aspose.OCR jest kompatybilny z Java 11 i nowszymi wersjami.

### P2: Czy mogę używać Aspose.OCR zarówno do projektów osobistych, jak i komercyjnych?

 Odpowiedź 2: Tak, Aspose.OCR może być używany zarówno w projektach osobistych, jak i komercyjnych. Aby uzyskać szczegółowe informacje na temat licencji, odwiedź stronę[Tutaj](https://purchase.aspose.com/buy).

### P3: Jak uzyskać tymczasową licencję na Aspose.OCR?

 Odpowiedź 3: Możesz uzyskać licencję tymczasową[Tutaj](https://purchase.aspose.com/temporary-license/).

### P4: Gdzie mogę znaleźć wsparcie dla Aspose.OCR?

 A4: Aby uzyskać wsparcie i dyskusje, odwiedź stronę[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

### P5: Czy Aspose.OCR obsługuje wielowątkowość?

O5: Tak, Aspose.OCR obsługuje wielowątkowość w celu poprawy wydajności w równoczesnych środowiskach.
