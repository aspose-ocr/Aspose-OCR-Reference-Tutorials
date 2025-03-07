---
title: Wykonywanie OCR na obrazie z adresu URL w Aspose.OCR dla Java
linktitle: Wykonywanie OCR na obrazie z adresu URL w Aspose.OCR dla Java
second_title: Aspose.OCR API Java
description: Odblokuj płynną ekstrakcję tekstu obrazu w Javie za pomocą Aspose.OCR. Wysoka dokładność OCR z łatwą integracją.
weight: 11
url: /pl/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonywanie OCR na obrazie z adresu URL w Aspose.OCR dla Java

## Wstęp

Witamy w naszym przewodniku krok po kroku dotyczącym optycznego rozpoznawania znaków (OCR) na obrazie z adresu URL przy użyciu Aspose.OCR dla Java. Ten samouczek ma na celu pomóc Ci bezproblemowo zintegrować Aspose.OCR z aplikacjami Java, umożliwiając łatwe wyodrębnianie tekstu z obrazów. Aspose.OCR to potężna biblioteka OCR obsługująca różne formaty obrazów, co czyni ją cennym narzędziem do zastosowań wymagających ekstrakcji tekstu.

## Warunki wstępne

Przed przystąpieniem do samouczka upewnij się, że spełniasz następujące wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że na komputerze jest skonfigurowane działające środowisko programistyczne Java.

2.  Biblioteka Aspose.OCR: Pobierz i zainstaluj bibliotekę Aspose.OCR dla Java. Bibliotekę i powiązaną dokumentację można znaleźć na stronie[Witryna Aspose.OCR](https://reference.aspose.com/ocr/java/).

## Importuj pakiety

W swoim projekcie Java zaimportuj niezbędne pakiety dla Aspose.OCR:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Krok 1: Utwórz instancję API

Zainicjuj instancję klasy AsposeOCR:

```java
AsposeOCR api = new AsposeOCR();
```

## Krok 2: Zdefiniuj adres URL obrazu

Podaj adres URL obrazu, z którego chcesz wykonać OCR:

```java
String uri = "https://www.example.com/twój-obrazek.png";
```

## Krok 3: Ustaw opcje rozpoznawania

Skonfiguruj ustawienia rozpoznawania, takie jak wyłączenie automatycznego pochylania i zdefiniowanie obszarów rozpoznawania:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Zdefiniuj obszary rozpoznawania za pomocą prostokątów
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## Krok 4: Wykonaj OCR

Wywołaj proces rozpoznawania OCR:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Krok 5: Wydrukuj wyniki

Wyświetl wyniki rozpoznawania, w tym wyodrębniony tekst, tekst obszarów rozpoznawania, dane wyjściowe JSON i wszelkie ostrzeżenia:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Powtórz te kroki, aby zintegrować Aspose.OCR z aplikacją Java i precyzyjnie wyodrębnić tekst z obrazów.

## Wniosek

Podsumowując, wykorzystanie Aspose.OCR dla Java zapewnia solidne rozwiązanie do zadań OCR, umożliwiając programistom bezproblemowe wyodrębnianie tekstu z obrazów. Przewodnik krok po kroku zapewnia płynny proces integracji, dzięki czemu jest dostępny dla programistów na wszystkich poziomach.

## Często zadawane pytania

### P1: Jak dokładny jest Aspose.OCR w rozpoznawaniu tekstu z obrazów?

O1: Aspose.OCR oferuje wysoką dokładność rozpoznawania tekstu, zwłaszcza gdy jest skonfigurowany z precyzyjnymi obszarami rozpoznawania.

### P2: Czy Aspose.OCR może obsługiwać wiele języków podczas rozpoznawania OCR?

Odpowiedź 2: Tak, Aspose.OCR obsługuje rozpoznawanie tekstu w wielu językach, zapewniając wszechstronność w różnorodnych zastosowaniach.

### P3: Czy istnieją jakieś uwagi licencyjne dotyczące używania Aspose.OCR w projektach komercyjnych?

Odpowiedź 3: Tak, zapewnij zgodność z warunkami licencji Aspose.OCR do użytku komercyjnego. Odnosić się do[zakup.aspose.com](https://purchase.aspose.com/buy) w celu uzyskania szczegółów licencji.

### P4: Jak mogę uzyskać pomoc dotyczącą problemów związanych z Aspose.OCR?

 A4: Odwiedź[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) za wsparcie społeczności i dyskusje. Aby uzyskać wsparcie premium, rozważ zakup tymczasowej licencji od[Licencja tymczasowa](https://purchase.aspose.com/temporary-license/).

### P5: Czy dostępna jest bezpłatna wersja próbna Aspose.OCR dla Java?

 Odpowiedź 5: Tak, poznaj funkcje Aspose.OCR w bezpłatnej wersji próbnej dostępnej pod adresem[releases.aspose.com](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
