---
title: Wykonywanie OCR z wyborem języka w Aspose.OCR
linktitle: Wykonywanie OCR z wyborem języka w Aspose.OCR
second_title: Aspose.OCR API Java
description: Odblokuj precyzyjną ekstrakcję tekstu z obrazów za pomocą Aspose.OCR dla Java. Postępuj zgodnie z naszym przewodnikiem krok po kroku, aby uzyskać dokładny OCR z wyborem języka.
type: docs
weight: 11
url: /pl/java/ocr-operations/perform-ocr-language-selection/
---
## Wstęp

W stale rozwijającym się środowisku technologicznym optyczne rozpoznawanie znaków (OCR) odgrywa kluczową rolę w wydobywaniu znaczących informacji z obrazów. Aspose.OCR for Java wyróżnia się jako potężne narzędzie, które umożliwia programistom bezproblemową integrację funkcji OCR z aplikacjami Java. W tym przewodniku krok po kroku odkryjemy, jak wykonać OCR z wyborem języka za pomocą Aspose.OCR, odblokowując potencjał precyzyjnego przetwarzania różnorodnych treści.

## Warunki wstępne

Zanim przejdziesz do samouczka, upewnij się, że spełniasz następujące wymagania wstępne:

- Środowisko programistyczne Java: Upewnij się, że masz zainstalowaną Javę w swoim systemie i środowisko programistyczne jest skonfigurowane.

-  Biblioteka Aspose.OCR: Pobierz i zainstaluj bibliotekę Aspose.OCR dla języka Java. Można znaleźć bibliotekę i powiązaną dokumentację[Tutaj](https://reference.aspose.com/ocr/java/).

- Plik obrazu: Przygotuj plik obrazu zawierający tekst, który chcesz wyodrębnić. Na przykład użyjmy pliku o nazwie „p3.png”.

## Importuj pakiety

W swoim projekcie Java zaimportuj niezbędne pakiety, aby wykorzystać funkcjonalność Aspose.OCR. Dodaj następujące wiersze na początku pliku Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Krok 1: Skonfiguruj katalog dokumentów

```java
// Ścieżka do katalogu dokumentów.
String dataDir = "Your Document Directory";
```

Zastąp „Twój katalog dokumentów” rzeczywistą ścieżką do katalogu, w którym znajduje się plik obrazu.

## Krok 2: Zdefiniuj ścieżkę obrazu

```java
// Ścieżka obrazu
String file = dataDir + "p3.png";
```

Dostosuj zmienną pliku, aby wskazywała konkretny plik obrazu.

## Krok 3: Utwórz instancję API Aspose.OCR

```java
// Utwórz instancję API
AsposeOCR api = new AsposeOCR();
```

Zainicjuj obiekt AsposeOCR, aby uzyskać dostęp do jego funkcji.

## Krok 4: Ustaw opcje rozpoznawania

```java
// Ustaw opcje rozpoznawania
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Dostosuj ustawienia rozpoznawania w oparciu o swoje wymagania. Dostosuj parametry, takie jak pochylenie, język i obszary rozpoznawania.

## Krok 5: Wykonaj OCR i pobierz wyniki

```java
// Pobierz obiekt wynikowy
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Wykonaj operację OCR, korzystając z określonego pliku obrazu i ustawień. Przechwyć wynik w obiekcie RecognitionResult.

## Krok 6: Wydrukuj i wykorzystaj wyniki

```java
// Wydrukuj wynik
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Wydrukuj wyodrębniony tekst, rozpoznawane obszary, reprezentację JSON, kąt pochylenia i wszelkie ostrzeżenia. Użyj wyników w razie potrzeby w swojej aplikacji.

## Wniosek

W tym samouczku zagłębiliśmy się w płynną integrację Aspose.OCR dla Java w celu wykonywania OCR z wyborem języka. Ta potężna biblioteka otwiera świat możliwości dla programistów, którzy chcą dokładnie wyodrębnić tekst z obrazów.

## Często zadawane pytania

### P1: Czy mogę używać Aspose.OCR dla wielu języków w jednym procesie rozpoznawania?

O1: Tak, możesz ustawić wiele języków w Ustawieniach rozpoznawania, aby zwiększyć dokładność rozpoznawania treści wielojęzycznych.

### P2: Jak mogę obsługiwać różne formaty obrazów za pomocą Aspose.OCR?

O2: Aspose.OCR obsługuje różne formaty obrazów, w tym PNG, JPEG i TIFF. Po prostu podaj poprawną ścieżkę pliku w zmiennej ścieżki obrazu.

### P3: Czy istnieje ograniczenie rozmiaru obrazu, który może przetworzyć Aspose.OCR?

O3: Aspose.OCR może obsługiwać obrazy o różnych rozmiarach, ale większe obrazy mogą wymagać więcej czasu przetwarzania i zasobów.

### P4: Czy mogę dostosować ustawienia rozpoznawania dla określonych obszarów obrazu?

A4: Absolutnie. Skorzystaj z funkcji RecognitionAreas, aby zdefiniować określone prostokąty w obrazie w celu ukierunkowanego rozpoznania.

### P5: Czy Aspose.OCR nadaje się zarówno do projektów osobistych, jak i komercyjnych?

Odpowiedź 5: Tak, Aspose.OCR oferuje elastyczne opcje licencjonowania, dzięki czemu nadaje się zarówno do użytku osobistego, jak i komercyjnego.