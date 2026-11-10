---
category: general
date: 2026-06-16
description: Dowiedz się, jak wykonać OCR na plikach graficznych w Javie. Ten samouczek
  obejmuje rozpoznawanie tekstu z PNG, wyodrębnianie tekstu z obrazu, konwertowanie
  obrazu na tekst oraz ładowanie obrazu do OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: pl
og_description: Wykonaj OCR na obrazie przy użyciu Javy. Ten przewodnik pokazuje,
  jak rozpoznawać tekst z pliku PNG, wyodrębniać tekst z obrazu i konwertować obraz
  na tekst przy użyciu gotowego przykładu do uruchomienia.
og_title: Wykonaj OCR na obrazie w Javie – Pełny poradnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Wykonaj OCR na obrazie w Javie – Kompletny przewodnik krok po kroku
url: /pl/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wykonaj OCR na obrazie w Javie – Kompletny przewodnik krok po kroku

Kiedykolwiek potrzebowałeś **wykonać OCR na obrazie**, ale nie wiedziałeś, którą bibliotekę Java wybrać? Nie jesteś sam. Niezależnie od tego, czy tworzysz skaner paragonów, archiwizator dokumentów, czy po prostu jesteś ciekawy, jak zamienić zdjęcia w przeszukiwalny tekst, nauka **wykonywania OCR na obrazie** w Javie to przydatna umiejętność.

W tym samouczku przejdziemy przez wszystko, co potrzebne, aby **wykonać OCR na obrazie**: wczytanie obrazu, skonfigurowanie silnika, rozpoznanie tekstu i w końcu wydrukowanie wyniku. Po zakończeniu będziesz w stanie **rozpoznać tekst z plików PNG**, **wyodrębnić tekst z obrazu** oraz **przekształcić obraz w tekst** przy użyciu kilku linijek kodu.

## Wymagania wstępne

- Java 17 lub nowsza (kod kompiluje się na dowolnym aktualnym JDK)
- Zainstalowany Maven (lub ulubione narzędzie budowania)
- Podstawowa znajomość składni Javy
- Plik PNG, którym chcesz przetestować (nazwijmy go `hello.png`)

> **Wskazówka:** Jeśli nie masz pod ręką pliku PNG, utwórz go, robiąc zrzut ekranu dowolnego tekstu i zapisując go jako `hello.png` w folderze o nazwie `resources`.

## Co zbudujemy

Małą aplikację konsolową o nazwie `OcrDemo`, która:

1. **Wczytuje obraz do OCR** – odczytuje PNG z dysku.
2. **Wykonuje OCR na obrazie** – używa silnika Tesseract poprzez Tess4J.
3. **Wyodrębnia tekst z obrazu** – zwraca `String` z rozpoznaną treścią.
4. Drukuje wynik w konsoli.

Zanurzmy się.

## Krok 1: Konfiguracja projektu i dodanie Tess4J

Najpierw utwórz nowy projekt Maven (lub Gradle, jeśli wolisz). Dodaj zależność Tess4J, która opakowuje popularny silnik Tesseract OCR.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Dlaczego Tess4J?** Jest aktywnie utrzymywany, działa na wielu platformach i zapewnia czyste API Javy do **wykonywania OCR na obrazie**.

## Krok 2: Przygotowanie logiki wczytywania obrazu

Teraz napiszemy metodę pomocniczą, która **wczytuje obraz do OCR**. Metoda używa `ImageIO` z Javy, aby odczytać PNG do `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Zauważ, że nazwa metody wyraźnie odzwierciedla zamiar **wczytywania obrazu do OCR**, co czyni kod samodokumentującym się.

## Krok 3: Konfiguracja silnika OCR do **wykonywania OCR na obrazie**

Mając obraz w ręku, tworzymy instancję `Tesseract`, włączamy automatyczne wykrywanie języka i wywołujemy `doOCR`. To jest sedno tego, jak **wykonywać OCR na obrazie**.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Dlaczego włączyć auto‑detekcję?** Pozwala silnikowi wybrać najlepszy model językowy dla obrazu, co jest szczególnie przydatne, gdy **przekształcasz obraz w tekst** z źródeł mieszających angielski i inne skrypty.

## Krok 4: Połączenie wszystkiego – główna aplikacja

Oto punkt wejścia, który **rozpoznaje tekst z PNG**, **wyodrębnia tekst z obrazu**, a na końcu drukuje wynik. To kompletny, gotowy do uruchomienia przykład.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Oczekiwany wynik

Jeśli `hello.png` zawiera frazę „Hello, OCR world!”, konsola wyświetli coś w rodzaju:

```
=== Recognized Text ===
Hello, OCR world!
```

Dokładny wynik może nieco się różnić w zależności od jakości obrazu, ale powinieneś zobaczyć tekst umieszczony w PNG.

## Krok 5: Obsługa typowych przypadków brzegowych

### 5.1 Radzenie sobie z obrazami o niskiej rozdzielczości

Jeśli źródłowy PNG jest rozmyty, dokładność OCR spada. Szybkim rozwiązaniem jest zwiększenie rozdzielczości obrazu przed przekazaniem go silnikowi:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Wywołaj `upscale(image, 2)` przed `engine.recognize(image)`, aby poprawić wyniki.

### 5.2 Dokumenty wielojęzyczne

Jeśli spodziewasz się francuskiego lub niemieckiego tekstu, po prostu dodaj kody językowe do `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Silnik spróbuje wtedy **wyodrębnić tekst z obrazu** przy użyciu połączonych modeli językowych.

### 5.3 Pomijanie pustych stron

Czasami zeskanowana strona PDF renderuje się jako pusty PNG. Wykrycie pustego obrazu oszczędza czas przetwarzania:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Krok 6: Pakowanie i uruchamianie aplikacji

1. **Kompilacja:** `mvn clean compile`
2. **Uruchomienie:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Upewnij się, że folder `tessdata` (zawierający pliki językowe) znajduje się obok skompilowanego JAR‑a lub podaj jego bezwzględną ścieżkę w `OcrEngine`.

## Zakończenie

Masz teraz solidny, gotowy do produkcji wzorzec do **wykonywania OCR na obrazie** przy użyciu Javy. Od **wczytywania obrazu do OCR** po **rozpoznawanie tekstu z PNG**, omówiliśmy, jak **wyodrębnić tekst z obrazu**, **przekształcić obraz w tekst** oraz radzić sobie z trudnymi scenariuszami, takimi jak skany o niskiej rozdzielczości czy treści wielojęzyczne.

Następnie możesz zbadać:

- **Przetwarzanie wsadowe** – iteracja po katalogu PNG i zapisywanie każdego wyniku do pliku `.txt`.
- **Generowanie PDF** – osadzenie wyodrębnionego tekstu w przeszukiwalnych PDF‑ach.
- **Usługi OCR w chmurze** – porównanie wydajności lokalnego Tesseract z API, takimi jak Google Vision czy Azure Cognitive Services.

Śmiało eksperymentuj, dostosowuj parametry i dziel się swoimi odkryciami. Miłego kodowania i niech Twoje obrazy zawsze zamieniają się w czysty, przeszukiwalny tekst! 

![Diagram przedstawiający przepływ pracy OCR do wykonywania OCR na obrazie](https://example.com/ocr-workflow.png "przykład wykonywania OCR na obrazie")


## Co powinieneś nauczyć się dalej?


Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletny, działający kod wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}