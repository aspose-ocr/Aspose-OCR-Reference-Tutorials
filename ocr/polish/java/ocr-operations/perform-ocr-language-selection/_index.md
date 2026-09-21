---
date: 2026-02-12
description: Dowiedz się, jak rozpoznawać tekst na obrazach z wyborem języka przy
  użyciu Aspose.OCR dla Javy. Ten przewodnik krok po kroku obejmuje wyodrębnianie
  tekstu w Javie, korekcję pochylenia OCR i wiele więcej.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Jak wykonać OCR tekstu obrazu z określonym językiem przy użyciu Aspose.OCR
url: /pl/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR tekstu z obrazu z uwzględnieniem języka przy użyciu Aspose.OCR

## Wprowadzenie

Ekstrahowanie tekstu z plików graficznych jest powszechnym wymaganiem, niezależnie od tego, czy digitalizujesz zeskanowane dokumenty, przetwarzasz paragony, czy tworzysz przeszukiwalne archiwa. W tym samouczku przeprowadzimy Cię przez kompletny, praktyczny przykład, który pokazuje **jak wykonać OCR tekstu z obrazu** z określonym ustawieniem języka, abyś mógł dziś zintegrować niezawodne OCR w swoich aplikacjach Java. Zobaczysz także, jak obsługiwać korekcję pochylenia OCR oraz rozpoznawanie oparte na regionach dla optymalnej dokładności.

## Szybkie odpowiedzi
- **Jaka biblioteka obsługuje OCR w Javie?** Aspose.OCR for Java  
- **Które ustawienie wybiera język?** `settings.setLanguage(Language.Eng)` (lub dowolny obsługiwany język)  
- **Czy potrzebna jest licencja do rozwoju?** Darmowa licencja ewaluacyjna działa do testów; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę ograniczyć OCR do regionu obrazu?** Tak, użyj `RecognitionSettings.setRecognitionAreas()` z prostokątami.  
- **Jaki jest typowy czas wykonania?** Kilka sekund na stronę na standardowym laptopie, w zależności od rozmiaru obrazu i złożoności języka.

## Jak wykonać OCR tekstu z obrazu z wyborem języka

W tej sekcji odpowiadamy na podstawowe pytanie **jak wykonać OCR** obrazu, gdy znasz język tekstu. Wybranie właściwego języka znacząco zwiększa dokładność rozpoznawania, ponieważ silnik OCR może zastosować słowniki i modele znaków specyficzne dla języka.

### Dlaczego to ma znaczenie
- **Wyższa dokładność** – modele specyficzne dla języka redukują błędne rozpoznania.  
- **Zwiększenie wydajności** – silnik pomija niepotrzebne kontrole językowe.  
- **Lepsze radzenie sobie z diakrytykami** – francuski, hiszpański, niemiecki itp. są rozpoznawane poprawnie, gdy użyty jest odpowiedni enum `Language`.

## Czym jest „ekstrahowanie tekstu z obrazu”?
Ekstrahowanie tekstu z obrazu (OCR) konwertuje wizualną reprezentację znaków na ciągi czytelne dla maszyny. Umożliwia to wyszukiwanie, analizy i przepływy pracy związane z ekstrakcją danych, które w przeciwnym razie wymagałyby ręcznej transkrypcji.

## Dlaczego warto używać Aspose.OCR z wyborem języka?
- **Wsparcie wielojęzyczne** – Wybierz dokładny język(y) występujące na obrazie, aby zwiększyć dokładność.  
- **Precyzyjna kontrola** – Dostosuj pochylenie, zdefiniuj obszary rozpoznawania i ustaw zachowanie auto‑skew.  
- **Czyste API Java** – Brak zależności natywnych, łatwe do integracji w każdym projekcie Java.  
- **Bogate dane wynikowe** – Uzyskaj zwykły tekst, JSON, prostokąty ograniczające i ostrzeżenia w jednym wywołaniu.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:
- **Java Development Kit (JDK)** zainstalowany (JDK 8 lub nowszy).  
- **Biblioteka Aspose.OCR for Java** – pobierz ją z oficjalnej strony [here](https://reference.aspose.com/ocr/java/).  
- Plik obrazu zawierający tekst, który chcesz wyekstrahować, np. `p3.png`.

## Importowanie pakietów

W swoim pliku źródłowym Java, dołącz wymagane klasy Aspose.OCR oraz standardowe utilitety Java:

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

## Przewodnik krok po kroku

### Krok 1: Skonfiguruj katalog dokumentów

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Zastąp `"Your Document Directory"` absolutną ścieżką, w której znajduje się `p3.png`.

### Krok 2: Zdefiniuj ścieżkę do obrazu

```java
// The image path
String file = dataDir + "p3.png";
```

Upewnij się, że zmienna `file` wskazuje dokładnie na obraz, który zamierzasz przetworzyć.

### Krok 3: Utwórz instancję API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Obiekt `AsposeOCR` zapewnia dostęp do wszystkich operacji OCR.

### Krok 4: Ustaw opcje rozpoznawania (wybór języka)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Tu:
1. Wyłączamy auto‑skew, ponieważ podajemy ręczną wartość pochylenia.  
2. Definiujemy prostokątny region (`RecognitionAreas`), aby ograniczyć OCR do części obrazu, która faktycznie zawiera tekst.  
3. Ustawiamy **język** na angielski (`Language.Eng`). Zmień to na `Language.Fra`, `Language.Spa` itp., w zależności od obrazu źródłowego.

### Krok 5: Wykonaj OCR i pobierz wyniki

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Wywołanie `RecognizePage` uruchamia silnik OCR przy użyciu obrazu i zdefiniowanych ustawień. Wynik jest przechowywany w obiekcie `RecognitionResult`.

### Krok 6: Wyświetl i wykorzystaj wyniki

```java
// Print result
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

Wyjście w konsoli pokazuje:
- Pełny wyekstrahowany tekst (`recognitionText`).  
- Tekst dla każdego zdefiniowanego prostokąta (`recognitionAreasText`).  
- Współrzędne prostokąta ograniczającego.  
- Reprezentację JSON ułatwiającą dalsze przetwarzanie.  
- Wykryty kąt pochylenia oraz ewentualne ostrzeżenia.

Możesz teraz przekazać `result.recognitionText` do swojej logiki biznesowej — przechowywać, indeksować lub przekazać do innej usługi.

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| **Zniekształcone znaki** | Wybrano niewłaściwy język | Ustaw właściwy enum `Language` (np. `Language.Fra` dla francuskiego). |
| **Brak zwróconego tekstu** | Obszar rozpoznawania nie obejmuje tekstu | Dostosuj współrzędne `Rectangle` lub usuń `RecognitionAreas`, aby przetworzyć cały obraz. |
| **Niska wydajność** | Bardzo duży obraz lub wysoka rozdzielczość | Zmniejsz rozmiar obrazu przed OCR lub zwiększ przydział pamięci dla JVM. |
| **Ostrzeżenia o nieobsługiwanym formacie** | Format obrazu nie rozpoznany | Konwertuj obraz do PNG, JPEG lub TIFF przed przetwarzaniem. |

## FAQ

**P: Czy mogę rozpoznawać wiele języków w jednym wywołaniu OCR?**  
O: Tak. Użyj `settings.setLanguage(Language.Eng | Language.Fra)`, aby włączyć rozpoznawanie wielojęzyczne.

**P: Jakie formaty obrazów obsługuje Aspose.OCR?**  
O: PNG, JPEG, BMP, TIFF, GIF i kilka innych. Wystarczy podać poprawną ścieżkę do pliku.

**P: Czy istnieje limit rozmiaru obrazu?**  
O: Nie ma sztywnego limitu, ale bardzo duże obrazy zwiększają zużycie pamięci i czas przetwarzania. Rozważ zmianę rozmiaru dużych plików.

**P: Jak uzyskać licencję produkcyjną?**  
O: Kup licencję na stronie Aspose i zastosuj ją za pomocą klasy `License`, jak pokazano w dokumentacji Aspose.

**P: Czy mogę wyekstrahować tekst z strony PDF bezpośrednio?**  
O: Nie bezpośrednio przy użyciu Aspose.OCR. Najpierw skonwertuj stronę PDF na obraz (np. przy użyciu Aspose.PDF), a następnie uruchom OCR.

## Podsumowanie

Teraz widzisz, jak **wyekstrahować tekst z obrazu** przy użyciu Aspose.OCR dla Java, wybierając odpowiedni język i ograniczając rozpoznawanie do konkretnych regionów. To podejście zapewnia dokładne, wysokowydajne OCR, które można osadzić w dowolnym przepływie pracy opartym na Javie — od systemów zarządzania dokumentami po potoki przechwytywania danych. Gotowy do dalszych kroków? Spróbuj zamienić enum języka, eksperymentuj z różnymi obszarami rozpoznawania i zintegrować wyniki z własną logiką aplikacji.

---

**Ostatnia aktualizacja:** 2026-02-12  
**Testowano z:** Aspose.OCR 24.11 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}