---
date: 2026-06-24
description: Dowiedz się, jak wykonywać OCR tekstu na obrazie z wyborem języka przy
  użyciu Aspose.OCR dla Javy. Ten przewodnik krok po kroku obejmuje extract text java,
  OCR skew correction i inne.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Jak wykonać korekcję pochylenia OCR i wybór języka przy użyciu Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Jak wykonać korekcję pochylenia OCR i wybór języka przy użyciu Aspose.OCR
url: /pl/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać korekcję pochylenia OCR i wybór języka przy użyciu Aspose.OCR

## Wprowadzenie

Wyodrębnianie tekstu z plików graficznych to powszechne wymaganie, niezależnie od tego, czy digitalizujesz zeskanowane dokumenty, przetwarzasz paragony, czy budujesz archiwa możliwe do przeszukiwania. W tym samouczku przeprowadzimy kompletny, praktyczny przykład, który pokazuje **jak wykonać OCR tekstu obrazu** z określonym ustawieniem języka, abyś mógł już dziś zintegrować niezawodne OCR w swoich aplikacjach Java. Zobaczysz także, jak obsługiwać **korekcję pochylenia OCR** oraz rozpoznawanie oparte na regionie dla optymalnej dokładności, co razem może **zwiększyć dokładność OCR** nawet o 30 % przy skanach pod kątem.

## Szybkie odpowiedzi
- **Jaka biblioteka obsługuje OCR w Javie?** Aspose.OCR for Java  
- **Które ustawienie wybiera język?** `settings.setLanguage(Language.Eng)` (lub dowolny obsługiwany język)  
- **Czy potrzebna jest licencja do rozwoju?** Darmowa licencja ewaluacyjna działa w testach; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę ograniczyć OCR do regionu obrazu?** Tak, użyj `RecognitionSettings.setRecognitionAreas()` z prostokątami.  
- **Jaki jest typowy czas wykonania?** Kilka sekund na stronę na standardowym laptopie, w zależności od rozmiaru obrazu i złożoności języka.  

`Language` jest wyliczeniem, które wymienia języki OCR obsługiwane przez Aspose.OCR, takie jak angielski, francuski, hiszpański itp.

## Czym jest korekcja pochylenia OCR?

Korekcja pochylenia OCR to proces wykrywania i prostowania nachylonych linii tekstu przed rozpoznawaniem znaków. Poprzez wyrównanie linii bazowej tekstu silnik OCR może skuteczniej zastosować modele językowe, zmniejszając błędy rozpoznawania spowodowane skanami pod kątem. Ten krok poprawia jakość wizualną obrazu wejściowego, pozwalając algorytmom rozpoznawania skupić się na prawdziwych kształtach znaków, a nie na zniekształceniach wprowadzonych przez rotację.

## Dlaczego korekcja pochylenia OCR poprawia dokładność

Gdy tekst jest nachylony, kształty znaków są zniekształcone, co prowadzi do nawet 20 % wyższych wskaźników błędów. Zastosowanie **korekcji pochylenia OCR** usuwa te zniekształcenia, pozwalając silnikowi skupić się na rzeczywistych glifach. W testach wydajnościowych Aspose.OCR osiągnął wzrost dokładności rozpoznawania o 15‑30 % w dokumentach z rotacją 10‑15° po zastosowaniu korekcji pochylenia.

## Dlaczego używać Aspose.OCR z wyborem języka?

Wybór dokładnego języka źródłowego umożliwia silnikowi OCR korzystanie ze słowników i modeli znaków specyficznych dla języka, co dramatycznie podnosi precyzję rozpoznawania i skraca czas przetwarzania. Dodatkowo Aspose.OCR oferuje precyzyjną kontrolę nad korekcją pochylenia, wyborem regionu i formatami wyjściowymi, co czyni go wszechstronnym wyborem dla wielojęzycznych potoków przetwarzania dokumentów.

- **Wsparcie wielojęzyczne** – Wybierz dokładny język(y) występujące na obrazie, aby zwiększyć dokładność.  
- **Precyzyjna kontrola** – Dostosuj pochylenie, zdefiniuj obszary rozpoznawania i ustaw zachowanie auto‑skew.  
- **Czyste API Java** – Brak zależności natywnych, łatwa integracja z dowolnym projektem Java.  
- **Bogate dane wynikowe** – Uzyskaj tekst zwykły, JSON, prostokąty ograniczające i ostrzeżenia w jednym wywołaniu.  
- **Zdolność ilościowa** – Aspose.OCR obsługuje **50+** formatów wejściowych i wyjściowych oraz może przetwarzać **500‑page** partie obrazów bez ładowania całego dokumentu do pamięci.

## Prerequisites

Przed rozpoczęciem upewnij się, że masz:

- **Java Development Kit (JDK)** zainstalowany (JDK 8 lub nowszy).  
- **Aspose.OCR for Java** – pobierz bibliotekę z oficjalnej strony [here](https://reference.aspose.com/ocr/java/).  
- Plik obrazu zawierający tekst, który chcesz wyodrębnić, np. `p3.png`.  

## Importowanie pakietów

Poniższe importy dają dostęp do podstawowych klas OCR oraz standardowych narzędzi Java.  
`import com.aspose.ocr.*;` – wprowadza główny silnik OCR.  
`import com.aspose.ocr.config.*;` – zawiera obiekty konfiguracyjne, takie jak `RecognitionSettings`.  
`import java.awt.Rectangle;` – używany do definiowania obszarów rozpoznawania.  

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

## Jak zastosować korekcję pochylenia OCR w Javie?

Wczytaj obraz, wyłącz automatyczne wykrywanie pochylenia i podaj zmierzone kąt lub pozwól silnikowi obliczyć go przy użyciu `settings.setAutoSkew(false)`. Silnik OCR najpierw wyprostuje obraz na podstawie podanego lub wykrytego kąta, a następnie przystąpi do rozpoznawania znaków. To dwustopniowe podejście zapewnia usunięcie nachylenia przed zastosowaniem modeli językowych, co skutkuje czystszym tekstem wyjściowym i mniejszą liczbą błędów rozpoznawania.

## Przewodnik krok po kroku

### Krok 1: Skonfiguruj katalog dokumentów

Utwórz obiekt `File`, który wskazuje folder zawierający obraz źródłowy. Dzięki temu obsługa ścieżek będzie przenośna między systemami operacyjnymi.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Zastąp `"Your Document Directory"` absolutną ścieżką, w której znajduje się `p3.png`.

### Krok 2: Zdefiniuj ścieżkę obrazu

Utwórz obiekt `File` dla konkretnego obrazu, który chcesz przetworzyć. Korzystanie z obiektu `File` umożliwia łatwy dostęp do metadanych pliku, jeśli będą potrzebne później.

```java
// The image path
String file = dataDir + "p3.png";
```

Upewnij się, że zmienna `file` wskazuje dokładnie na obraz, który zamierzasz przetworzyć.

### Krok 3: Utwórz instancję API Aspose.OCR

Klasa `AsposeOCR` jest punktem wejścia dla wszystkich operacji OCR. Enkapsuluje silnik, zarządza zasobami i udostępnia metodę `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Obiekt `AsposeOCR` daje dostęp do wszystkich operacji OCR.

### Krok 4: Ustaw opcje rozpoznawania (wybór języka)

`RecognitionSettings` jest kontenerem konfiguracji Aspose.OCR, który pozwala precyzyjnie dostroić proces OCR.  

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

Tutaj:

1. Wyłączamy auto‑skew, ponieważ podajemy ręczną wartość pochylenia.  
2. Definiujemy prostokątny region (`RecognitionAreas`), aby ograniczyć OCR do części obrazu, która faktycznie zawiera tekst.  
3. Ustawiamy **język** na angielski (`Language.Eng`). Zmień na `Language.Fra`, `Language.Spa` itp., w zależności od obrazu źródłowego.

### Krok 5: Wykonaj OCR i pobierz wyniki

Wywołanie `recognizePage` uruchamia silnik OCR przy użyciu obrazu i ustawień, które zdefiniowałeś. Wynik jest przechowywany w obiekcie `RecognitionResult`, który agreguje wszystkie przydatne dane.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Wywołanie `RecognizePage` uruchamia silnik OCR przy użyciu obrazu i ustawień, które zdefiniowałeś. Wynik jest przechowywany w obiekcie `RecognitionResult`.

### Krok 6: Wydrukuj i wykorzystaj wyniki

Konsola wyświetla:

- Pełny wyodrębniony tekst (`recognitionText`).  
- Tekst dla każdego zdefiniowanego prostokąta (`recognitionAreasText`).  
- Współrzędne prostokątów ograniczających.  
- Reprezentację JSON dla łatwego dalszego przetwarzania.  
- Wykryty kąt pochylenia oraz ewentualne ostrzeżenia.

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

Konsola wyświetla pełny wyodrębniony tekst, tekst specyficzny dla regionu, prostokąty ograniczające, JSON, kąt pochylenia i ostrzeżenia. Teraz możesz przekazać `result.recognitionText` do swojej logiki biznesowej — zapisać, zindeksować lub przesłać do innego serwisu.

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|---------|-----------|-------------|
| **Garbage characters** | Wrong language selected | Set the correct `Language` enum (e.g., `Language.Fra` for French). |
| **No text returned** | Recognition area does not cover the text | Adjust the `Rectangle` coordinates or remove `RecognitionAreas` to process the whole image. |
| **Slow performance** | Very large image or high resolution | Downscale the image before OCR or increase JVM memory allocation. |
| **Warnings about unsupported format** | Image format not recognized | Convert the image to PNG, JPEG, or TIFF before processing. |

## Najczęściej zadawane pytania

**Q: Czy mogę rozpoznawać wiele języków w jednym wywołaniu OCR?**  
A: Tak. Użyj `settings.setLanguage(Language.Eng | Language.Fra)`, aby włączyć rozpoznawanie wielojęzyczne.

**Q: Jakie formaty obrazów obsługuje Aspose.OCR?**  
A: PNG, JPEG, BMP, TIFF, GIF i kilka innych. Wystarczy podać prawidłową ścieżkę do pliku.

**Q: Czy istnieje limit rozmiaru obrazu?**  
A: Nie ma sztywnego limitu, ale przetwarzanie obrazów większych niż 10 MB może zwiększyć zużycie pamięci i czas wykonania. Rozważ zmianę rozmiaru dużych plików.

**Q: Jak uzyskać licencję produkcyjną?**  
A: Kup licencję na stronie Aspose i zastosuj ją za pomocą klasy `License`, jak pokazano w dokumentacji Aspose.

**Q: Czy mogę bezpośrednio wyodrębnić tekst z strony PDF?**  
A: Nie bezpośrednio przy użyciu Aspose.OCR. Najpierw skonwertuj stronę PDF na obraz (np. przy użyciu Aspose.PDF), a następnie uruchom OCR.

## Zakończenie

Widzisz teraz, jak **wyodrębnić tekst z obrazu** przy użyciu Aspose.OCR dla Java, wybierając odpowiedni język i stosując **korekcję pochylenia OCR**, aby zwiększyć niezawodność. To podejście dostarcza dokładnego, wysokowydajnego OCR, które można osadzić w dowolnym przepływie pracy opartym na Javie — od systemów zarządzania dokumentami po potoki przechwytywania danych. Eksperymentuj z różnymi enumami `Language`, dostosowuj `RecognitionAreas` i integruj wyjście JSON z dalszą analizą, aby uzyskać naprawdę kompleksowe rozwiązanie end‑to‑end.

---

**Ostatnia aktualizacja:** 2026-06-24  
**Testowano z:** Aspose.OCR 24.11 for Java  
**Autor:** Aspose

## Powiązane samouczki

- [Jak obliczyć kąt pochylenia w Javie przy użyciu Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Jak wykonać OCR tekstu obrazu z wyborem języka przy użyciu Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR rozpoznawanie dokumentów PDF w Aspose.OCR dla Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}