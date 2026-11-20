---
category: general
date: 2026-10-11
description: Naucz się, jak wykonać OCR na obrazie PNG w Javie, wyodrębnić tekst z
  obrazu i przekształcić obraz w tekst przy użyciu prostego przykładu OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: pl
lastmod: 2026-10-11
og_description: Jak wykonać OCR na obrazie PNG w Javie, wyodrębnić tekst z obrazu
  i przekształcić obraz w tekst, używając zwięzłego, gotowego do uruchomienia przykładu.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Jak wykonać OCR na obrazie PNG w Javie – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Jak wykonać OCR na obrazie PNG w Javie
url: /pl/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR na obrazie PNG w Javie

Jeśli potrzebujesz **perform OCR** na pliku obrazu, nauka **how to perform OCR** w Javie jest niezbędna dla wielu zadań automatyzacji. Niezależnie od tego, czy digitalizujesz paragony, indeksujesz zeskanowane dokumenty, czy tworzysz przeszukiwalny archiwum zdjęć, możliwość **extract text from image** oszczędza niezliczone godziny ręcznej pracy.

Ten tutorial pokazuje kompletną, gotową do uruchomienia rozwiązanie, które wczytuje PNG, uruchamia silnik OCR i **recognize text from PNG** plików. Zobaczysz także, jak **convert image to text** oraz jak radzić sobie z typowymi problemami, takimi jak niska rozdzielczość wejściowa lub znaki nie‑ASCII.

## Co osiągniesz

* **load image java** kod, który odczytuje PNG z dysku,
* zainicjalizuj lekki silnik OCR,
* **extract text from image** i wydrukuj wynik w konsoli,
* dostosuj rozwiązanie do innych formatów obrazów lub przetwarzania wsadowego.

Nie są wymagane żadne zewnętrzne usługi — jedynie jedna otwarto‑źródłowa biblioteka OCR (Tess4J) oraz środowisko uruchomieniowe Java SE.

---

## Wymagania wstępne

* Java 17 lub nowszy (kod kompiluje się przy użyciu JDK 17).
* Maven lub Gradle do zarządzania zależnościami.
* Podstawowa znajomość wiersza poleceń oraz wybranego IDE.
* Biblioteka `tess4j` (opakowanie Java dla Tesseract). Dodaj następującą zależność Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Jeśli używasz Gradle, odpowiednik to:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Potrzebujesz także plików danych Tesseract (`.traineddata`). Pobierz pakiet danych języka angielskiego z oficjalnego repozytorium i umieść go w folderze o nazwie `tessdata` w katalogu głównym projektu.

## Krok 1: Wczytaj obraz w Javie

Wczytanie PNG jest proste przy użyciu standardowej klasy `ImageIO`. Poniższy kod demonstruje **load image java** w bezpieczny, świadomy wyjątków sposób:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Dlaczego to ważne:** `ImageIO.read` automatycznie wykrywa format obrazu, ale wyraźnie sprawdzamy, czy wynik nie jest `null`, aby uniknąć cichych błędów, gdy PNG jest uszkodzony. Ten wzorzec jest dobrą praktyką, gdy **load image java** dla OCR.

## Krok 2: Zainicjalizuj silnik OCR

Tess4J opakowuje natywny binarny Tesseract, udostępniając prostą API Java. Poniższa metoda tworzy instancję `Tesseract`, wskazuje folder `tessdata` i konfiguruje język na angielski:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Dlaczego to robimy:** Inicjalizacja silnika raz i ponowne użycie go dla wielu obrazów zmniejsza narzut startowy. Wywołanie `setOcrEngineMode` wybiera domyślny tryb, który działa dobrze dla większości PNG. Jeśli napotkasz szumy w skanach, możesz eksperymentować z innymi trybami (np. `OEM_LSTM_ONLY`).

## Krok 3: Wykonaj OCR i **recognize text from PNG**

Teraz łączymy wczytywanie obrazu i silnik OCR. Poniższa metoda wykonuje OCR na `BufferedImage` i zwraca wyodrębniony ciąg znaków:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Pełny, gotowy do uruchomienia przykład**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Oczekiwany wynik**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Konsola wyświetli dokładne znaki, które silnik wyodrębnił z `sample.png`. Jeśli PNG zawiera tylko jedno słowo, wynik będzie tym słowem zakończonym znakiem nowej linii.

## Krok 4: Typowe warianty i przypadki brzegowe

### 4.1 Obsługa PNG o niskiej rozdzielczości

Tesseract działa najlepiej na obrazach o rozdzielczości co najmniej 300 DPI. Jeśli źródłowy PNG jest mniejszy, zwiększ jego rozmiar przed OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Zastosuj `upscale(image, 2)` przed wywołaniem `extractText`, aby poprawić dokładność.

### 4.2 Ekstrahowanie tekstu nie‑angielskiego

Aby **extract text from image** zawierającego inne języki, pobierz odpowiednie pliki `.traineddata` i ustaw kod języka:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Przetwarzanie wsadowe wielu PNG

Jeśli potrzebujesz **recognize text from PNG** w folderze, iteruj po katalogu:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Radzenie sobie z błędami OCR

Typowe błędy OCR obejmują mylenie `0` (zero) z `O` lub `1` z `l`. Post‑processing przy użyciu wyrażeń regularnych może oczyścić wynik:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

## Profesjonalne wskazówki dla niezawodnego OCR w Javie

| Tip | Reason |
|-----|--------|
| **Używaj bezstratnego PNG** | Artefakty kompresji w JPEG mogą wprowadzać silnik w błąd. |
| **Przytnij białe krawędzie** | Zbędna biała przestrzeń zwiększa czas przetwarzania i może powodować fałszywe trafienia. |
| **Ustaw `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** tylko gdy układ jest nieznany; w przeciwnym razie wybierz konkretny tryb (np. `PSM_SINGLE_BLOCK`). | |
| **Cache'uj instancję `ITesseract`** | |

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak odczytać tekst z obrazu w Javie przy użyciu Aspose OCR – Kompletny przewodnik](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Jak używać OCR w Javie – Szybkie rozpoznawanie tekstu z obrazu](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Wsadowe OCR obrazów w Javie – Szybkie wyodrębnianie tekstu z plików PNG](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}