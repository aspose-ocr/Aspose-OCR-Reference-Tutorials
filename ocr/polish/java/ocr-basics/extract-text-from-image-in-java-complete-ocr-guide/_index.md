---
category: general
date: 2026-07-21
description: Wyodrębnij tekst z obrazu przy użyciu Java OCR. Dowiedz się, jak przekonwertować
  PNG na tekst, odczytać tekst z PNG, załadować obraz do OCR i wykonać OCR na obrazie
  w kilku prostych krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: pl
lastmod: 2026-07-21
og_description: Wyodrębnij tekst z obrazu w Javie. Ten przewodnik pokazuje, jak konwertować
  PNG na tekst, odczytywać tekst z PNG, ładować obraz do OCR oraz efektywnie wykonywać
  OCR na obrazie.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Wyodrębnianie tekstu z obrazu w Javie – samouczek OCR krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Wyodrębnianie tekstu z obrazu w Javie – Kompletny przewodnik OCR
url: /pl/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu w Javie – Kompletny przewodnik OCR

Czy kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale nie wiedziałeś, którą bibliotekę Java wybrać? Nie jesteś sam. Niezależnie od tego, czy digitalizujesz paragony, skanujesz pliki PDF, czy tworzysz przeszukiwalne archiwum, wyciąganie tekstu z pliku PNG jest codziennym problemem dla wielu programistów.

W tym samouczku przeprowadzimy praktyczne rozwiązanie, które pozwala **konwertować PNG na tekst**, **odczytywać tekst z PNG**, **wczytywać obraz do OCR** oraz **wykonywać OCR na obrazie** — wszystko przy użyciu kilku linii czystego kodu Java. Po zakończeniu będziesz mieć działający program, który możesz wstawić do dowolnego projektu.

## Co zbudujesz

Stworzymy małą aplikację konsolową w Javie, która:

1. Wczytuje plik PNG z dysku.  
2. Wysyła obraz do silnika OCR (Tess4J, wrapper Java dla Tesseract).  
3. Wypisuje rozpoznany tekst w konsoli.

Bez zewnętrznych usług, bez magii — po prostu czysta Java i otwarto‑źródłowy silnik OCR.

## Wymagania wstępne

- **Java 17** lub nowsza (kod kompiluje się również w starszych wersjach, ale Java 17 zapewnia najnowsze udogodnienia językowe).  
- **Maven** lub **Gradle** do zarządzania zależnościami.  
- Przykładowy plik PNG o nazwie `sample.png` umieszczony w folderze, do którego możesz odwołać się (np. `src/main/resources`).  
- Podstawowa znajomość metody `main` w Javie oraz obsługi wyjątków.

Jeśli któreś z tych zagadnień jest Ci nieznane, nie martw się — każdy krok zawiera krótkie podsumowanie.

## Krok 1: Konfiguracja projektu i dodanie biblioteki OCR

Najpierw utwórz nowy projekt Maven (lub Gradle, jeśli wolisz). Dodaj zależność Tess4J, która dostarcza binaria Tesseract.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Wskazówka:** Jeśli używasz Gradle, równoważna linia to `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Dodanie tej biblioteki udostępnia klasę `Tesseract`, która zajmuje się ciężką pracą **wykonywania OCR na danych obrazu**.

## Krok 2: Wczytanie obrazu do OCR

Teraz musimy **wczytać obraz do OCR**. Tess4J współpracuje z `java.awt.image.BufferedImage`, więc wczytamy PNG przy użyciu `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Powyższa metoda czysto izoluje logikę **wczytywania obrazu do OCR**, ułatwiając testowanie reszty kodu. Zwróć uwagę na komentarz — odzwierciedla on oryginalny fragment, jednocześnie rozwijając go dla przejrzystości.

## Krok 3: Wykonanie OCR na obrazie

Mając obraz w pamięci, możemy teraz **wykonać OCR na obrazie**. Instancja `Tesseract` jest naszym silnikiem; skonfigurujemy ją, aby używała domyślnych danych językowych angielskiego dostarczanych z Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Tutaj połączyliśmy oryginalne „Krok 1” i „Krok 4” w jedną metodę, ponieważ obiekt `Tesseract` jest tani w tworzeniu i chcemy, aby kod pozostał zwięzły. Komentarz nadal odnosi się do pierwotnych kroków dla przejrzystości.

## Krok 4: Połączenie wszystkiego — metoda main

Na koniec łączymy wszystko w metodzie `main`. To tutaj **odczytasz tekst z PNG** i zobaczysz wynik wypisany w konsoli.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Gdy uruchomisz `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (lub równoważny w Gradle), powinieneś zobaczyć coś podobnego do:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Ten wynik dowodzi, że pomyślnie **wyodrębniłeś tekst z obrazu**, **przekonwertowałeś PNG na tekst** i **odczytałeś tekst z PNG** w jednym, schludnym programie.

## Obsługa typowych przypadków brzegowych

### Obrazy niskiej jakości

Jeśli PNG jest rozmyty lub ma niski kontrast, dokładność OCR spada. Szybkim rozwiązaniem jest wstępne przetworzenie obrazu:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Obsługa wielu języków

Tess4J obsługuje wiele języków. Wystarczy pobrać odpowiedni plik `.traineddata` i ustawić `tesseract.setLanguage("spa")` dla hiszpańskiego, na przykład.

### Duże pliki PDF lub obrazy wielostronicowe

Jeśli musisz **wyodrębnić tekst z obrazu** znajdującego się w PDF, najpierw podziel każdą stronę na PNG (przy użyciu PDFBox), a następnie przekaż każdy PNG do tej samej procedury OCR.

## Pełny działający przykład (cały kod w jednym miejscu)

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java. Skopiuj i wklej go do `src/main/java/com/example/ocrdemo/OcrDemo.java` i możesz zaczynać.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Uruchomienie klasy wypisuje wynik OCR, potwierdzając, że pomyślnie **wykonałeś OCR na obrazie** i przekształciłeś swój PNG w edytowalny tekst.

## Podsumowanie i kolejne kroki

Zaczęliśmy od **wyodrębniania tekstu z obrazu** przy użyciu lekkiej konfiguracji Java. Teraz wiesz, jak **wczytać obraz do OCR**, **wykonać OCR na obrazie** oraz **odczytać tekst z PNG** — podstawowe elementy każdej ścieżki digitalizacji dokumentów.

Chcesz pójść dalej? Wypróbuj te pomysły:

- **Przetwarzanie wsadowe:** Przejdź przez katalog PNG i zapisz każdy wynik do pliku `.txt`.  
- **Integracja z bazą danych:** Przechowuj wyodrębnione ciągi razem z metadanymi dla przeszukiwalnych archiwów.  
- **Połączenie z NLP:** Przekaż wynik OCR do modelu analizy sentymentu w celu szybkich wniosków.  

Każde z tych rozszerzeń opiera się na tych samych podstawowych koncepcjach, które omówiliśmy, więc jesteś gotowy do eksperymentów.

---

*Sz​częśliwego kodowania! Jeśli napotkasz problemy

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}