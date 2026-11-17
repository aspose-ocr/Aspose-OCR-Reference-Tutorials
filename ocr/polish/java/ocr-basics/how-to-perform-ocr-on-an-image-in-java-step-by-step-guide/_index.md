---
category: general
date: 2026-11-17
description: Dowiedz się, jak wykonać OCR na obrazie w Javie i wyodrębnić tekst ze
  zdjęć, używając prostego przykładu kodu. Zawiera wskazówki dotyczące odczytu obrazu
  w Javie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: pl
lastmod: 2026-11-17
og_description: Jak wykonać OCR na obrazie w Javie i szybko wyodrębnić tekst. Skorzystaj
  z tego przewodnika, aby odczytać obraz w Javie i przekształcić go w tekst przy użyciu
  gotowego przykładu.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Jak wykonać OCR na obrazie w Javie – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Jak wykonać OCR na obrazie w Javie – przewodnik krok po kroku
url: /pl/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wykonać OCR na obrazie w Javie – przewodnik krok po kroku

Jeśli potrzebujesz **how to perform OCR** na zdjęciu, ten tutorial pokazuje kompletną, gotową do uruchomienia rozwiązanie w Javie. Zobaczysz, jak odczytać plik obrazu, skonfigurować silnik OCR i wyodrębnić tekst rozpoznany przez silnik.

Praca ze skanowanymi dokumentami, paragonami lub zrzutami ekranu często wymaga konwersji treści wizualnej na tekst przeszukiwalny. Ten przewodnik przeprowadzi Cię przez każdy krok, od wczytania obrazu po wydrukowanie wyodrębnionego tekstu, a także omówi typowe pułapki, takie jak nieobsługiwane formaty plików i wyniki null.

## Wymagania wstępne

* Zainstalowany Java Development Kit (JDK) 8 lub nowszy.
* Narzędzie budujące (Maven lub Gradle) do pobrania biblioteki OCR.
* Plik obrazu (JPEG, PNG, BMP), który chcesz przetworzyć.

Kod używa **OCR library from the `com.asprise.ocr` package** ponieważ wymaga tylko jednego pliku JAR i działa na wszystkich głównych platformach. Zamień ją na innego dostawcę (Tesseract, Google Vision itp.), zamieniając instrukcje importu i kod inicjalizacji silnika.

## Krok 1: Dodaj zależność OCR

Jeśli używasz Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Dla Gradle, umieść tę linię w `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Te linie zapewniają, że kod **read image Java** może się kompilować i że silnik OCR jest dostępny w czasie wykonywania.

## Krok 2: Odczytaj obraz w Javie

Odczytanie pliku obrazu jest pierwszym konkretnym krokiem w każdym przepływie pracy **extract text image**. Wbudowana w Javę klasa `ImageIO` obsługuje większość popularnych formatów.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Dlaczego to ważne:** `ImageIO.read` zwraca `null` dla nieobsługiwanych formatów lub uszkodzonych plików. Powyższa metoda loguje problem i zwraca `null`, aby kolejny krok mógł zareagować łagodnie.

## Krok 3: Utwórz i skonfiguruj silnik OCR

Silnik OCR musi wiedzieć, jaki język rozpoznawać. Ustawienie języka znacznie zwiększa dokładność, szczególnie w dokumentach nie‑angielskich.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Dlaczego to ważne:** Uruchomienie silnika jest stosunkowo kosztowną operacją, więc powinieneś utworzyć go raz i ponownie używać dla wielu obrazów, jeśli Twoja aplikacja przetwarza partie.

## Krok 4: Wykonaj OCR i przekształć obraz w tekst

Teraz, gdy obraz jest wczytany i silnik gotowy, możesz uruchomić krok rozpoznawania. To jest sedno **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Obsługa przypadków brzegowych:** Jeśli obraz jest `null`, metoda zwraca pusty ciąg zamiast rzucać `NullPointerException`. Dzięki temu otaczający kod jest bardziej odporny przy obsłudze plików dostarczonych przez użytkownika.

## Krok 5: Wyświetl wyodrębniony tekst

Na koniec wydrukuj wynik w konsoli lub przekaż go do innego komponentu (np. bazy danych lub widgetu UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Gdy uruchomisz program poleceniem `java OcrDemo sample.jpg`, konsola wyświetli rozpoznane znaki. To kończy cykl **convert image to text**.

### Oczekiwany wynik

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Jeśli obraz nie zawiera czytelnych znaków, program wypisze `(no text detected)`.

## Częste warianty i jak je dostosować

| Variation | Co się zmienia | Kiedy używać |
|-----------|----------------|--------------|
| **Different language** | Zamień `"eng"` na `"spa"` dla hiszpańskiego, `"fra"` na francuski itd. | Dokumenty napisane w języku innym niż angielski |
| **Batch processing** | Pętla po liście ścieżek plików, ponowne użycie tego samego obiektu `Ocr`. | Duże zestawy zeskanowanych stron |
| **Higher accuracy** | Użyj `Ocr.SPEED_SLOW` lub włącz `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` dla skanów zawierających wyłącznie cyfry. | Gdy jakość OCR jest krytyczna (np. numery faktur) |
| **Tesseract alternative** | Zamień import na `net.sourceforge.tess4j.Tesseract` i dostosuj kod inicjalizacji. | Projekty już zależne od Tesseract |

## Porady profesjonalne

* **Resize large images** przed podaniem ich do silnika; prędkość OCR skaluje się wraz z liczbą pikseli.
* **Pre‑process** obraz (odcienie szarości, zwiększenie kontrastu) używając bibliotek takich jak OpenCV, jeśli źródło jest zaszumione.
* **Cache the OCR engine** jeśli wywołujesz go wiele razy w krótkim czasie—uruchamianie i zatrzymywanie silnika generuje narzut.
* **Validate the result** przy użyciu wyrażeń regularnych, gdy oczekujesz konkretnego formatu (np. daty, numery telefonów).

## Zakończenie

Teraz wiesz **how to perform OCR** na obrazie w Javie, od odczytu pliku po wyświetlenie wyodrębnionego tekstu. Tutorial obejmował techniki **read image Java**, **extract text image**, **convert image to text** oraz **image to text java**, a także dostarczył praktyczne porady dla rzeczywistych scenariuszy.

Od tego momentu możesz:

* Zintegrować krok OCR z usługą webową, która przyjmuje przesyłane pliki.
* Połączyć wynik z indeksem wyszukiwania pełnotekstowego dla zeskanowanych dokumentów.
* Zbadać zaawansowane opcje OCR, takie jak obsługa wielu języków lub własne zestawy znaków.

Miłego kodowania i ciesz się przekształcaniem zdjęć w tekst przeszukiwalny!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}