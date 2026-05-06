---
category: general
date: 2026-05-06
description: Jak używać Aspose OCR do rozpoznawania tekstu z obrazu, włączania automatycznego
  wykrywania języka i zwiększania szybkości OCR w Javie.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: pl
og_description: Jak używać Aspose OCR, aby szybko rozpoznawać tekst z obrazu, włączyć
  automatyczne wykrywanie języka i zwiększyć szybkość OCR w Javie.
og_title: Jak korzystać z Aspose OCR dla obrazów wielojęzycznych
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Jak korzystać z Aspose OCR dla obrazów wielojęzycznych
url: /pl/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Aspose OCR dla obrazów wielojęzycznych

Zastanawiałeś się kiedyś **jak używać Aspose**, aby wyciągnąć tekst z obrazu zawierającego kilka języków jednocześnie? Nie jesteś sam — programiści często napotykają problem, gdy obraz łączy angielski, rosyjski, hindi lub jakikolwiek inny alfabet. Dobrą wiadomością jest to, że Aspose OCR radzi sobie z tym płynnie i możesz nawet **rozpoznawać tekst z obrazu** szybciej, ograniczając zestaw języków.

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład w Javie, który **ładuje obraz do OCR**, włącza **automatyczne wykrywanie języka** i pokazuje prosty trik, aby **zwiększyć szybkość OCR**. Po zakończeniu będziesz mieć samodzielny program, który wypisuje wyodrębniony tekst w konsoli i zrozumiesz, dlaczego każde ustawienie ma znaczenie.

> **Wymagania wstępne** – zainstalowany Java 17+, Maven lub Gradle do zarządzania zależnościami oraz licencja Aspose OCR (bezpłatna wersja próbna działa w ocenie). Nie są wymagane inne biblioteki.

---

## Krok 1 – Dodaj Aspose OCR do swojego projektu

Zanim będziesz mógł **używać Aspose**, potrzebujesz biblioteki w classpath. Z Maven wygląda to tak:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Jeśli wolisz Gradle:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Porada:** Trzymaj się najnowszej stabilnej wersji; nowsze wersje często zawierają ulepszenia wydajności, które bezpośrednio wpływają na **zwiększenie szybkości OCR**.

---

## Krok 2 – Utwórz instancję silnika OCR  

Serce każdego przepływu pracy Aspose OCR to `OcrEngine`. Utworzenie go jest proste, ale warto zauważyć, że silnik przechowuje wewnętrzne pamięci podręczne. Ponowne użycie jednej instancji dla wielu obrazów może faktycznie **zwiększyć szybkość OCR**, ponieważ biblioteka unika powtarzalnej inicjalizacji natywnej.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Krok 3 – **Ładuj obraz do OCR**  

Aspose akceptuje wiele formatów obrazów (PNG, JPEG, TIFF, BMP). Tutaj demonstrujemy ładowanie pliku PNG zawierającego tekst po angielsku, rosyjsku i hindi. Pomocnicza metoda `ImageStream.fromFile` ukrywa szczegóły I/O plików i zapewnia, że obraz jest prawidłowo strumieniowany do silnika.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **Co jeśli obraz jest w pamięci?** Użyj `ImageStream.fromByteArray(byte[])` — idealne dla usług internetowych, które otrzymują obrazy jako strumienie bajtów.

---

## Krok 4 – Włącz automatyczne wykrywanie języka  

Domyślnie Aspose OCR zakłada jeden język, co może prowadzić do zniekształconego wyniku na wielojęzycznych obrazach. Włączenie automatycznego wykrywania nakazuje silnikowi rozpoznać skrypt każdego bloku tekstu przed rozpoznaniem.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Krok 5 – **Zwiększ szybkość OCR** poprzez ograniczenie puli języków  

Pełne automatyczne wykrywanie skanuje każdy język obsługiwany przez Aspose (ponad 70). Jeśli znasz możliwe języki z wyprzedzeniem, możesz dać silnikowi podpowiedź. Dostarczenie mniejszej tablicy zmniejsza przestrzeń przeszukiwania i w konsekwencji **zwiększa szybkość OCR**.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

> **Dlaczego to pomaga?** Silnik pomija modele językowe, których nie potrzebuje, oszczędzając cykle CPU i pamięć. Jeśli później dodasz więcej języków, po prostu zaktualizuj tablicę — nie wymaga to przepisania kodu.

---

## Krok 6 – Wykonaj rozpoznanie i **rozpoznaj tekst z obrazu**

Teraz odbywa się najcięższa część. `recognize()` zwraca obiekt `OcrResult`, który zawiera czysty tekst, oceny pewności oraz nawet informacje o układzie, jeśli będą potrzebne później.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Oczekiwany wynik w konsoli

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Jeśli obraz zawiera dodatkowy szum lub pochylony tekst, możesz zobaczyć niższą pewność dla tych linii. W takim przypadku rozważ wstępne przetworzenie obrazu (prostowanie, binaryzacja) przed przekazaniem go do Aspose.

---

## Częste pytania i przypadki brzegowe

### Co jeśli obraz jest ogromny (np. >10 MP)?

Duże obrazy zużywają więcej pamięci i mogą spowalniać przetwarzanie. Szybkim sposobem na **zwiększenie szybkości OCR** jest zmniejszenie rozmiaru obrazu przy zachowaniu czytelności:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### Jak obsłużyć skrypty od prawej do lewej, takie jak arabski?

Aspose OCR automatycznie respektuje kierunek skryptu, ale możesz chcieć ustawić flagę `RightToLeft` dla przetwarzania po rozpoznaniu:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Czy mogę wyodrębnić tekst z PDF‑ów zamiast obrazów?

Tak — przekonwertuj każdą stronę PDF na obraz (używając Aspose PDF lub dowolnego rasteryzatora) i przekaż wynik do tego samego potoku OCR. Ta sama logika **rozpoznawania tekstu z obrazu** ma zastosowanie.

---

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Zapisz plik jako `MixedLanguageDemo.java`, skompiluj przy użyciu `javac` i uruchom za pomocą `java MixedLanguageDemo`. Jeśli wszystko jest poprawnie skonfigurowane, zobaczysz wielojęzyczny tekst wypisany w konsoli.

---

## Zakończenie

Teraz wiesz **jak używać Aspose**, aby **rozpoznawać tekst z obrazu** zawierającego kilka języków, jak **włączyć automatyczne wykrywanie języka** oraz praktyczną wskazówkę, jak **zwiększyć szybkość OCR** poprzez ograniczenie puli języków. Pełny kod powyżej jest gotowy do kopiowania i wklejania, a wyjaśnienia powinny dać Ci pewność w adaptacji rozwiązania — niezależnie od tego, czy musisz **ładować obraz do OCR** ze strumienia, tablicy bajtów, czy nawet ze zdjęcia z kamery internetowej.

Kolejne kroki? Spróbuj eksperymentować z:

* Dodawanie wstępnego przetwarzania obrazu (odszumianie, binaryzacja) dla skanów niskiej jakości.  
* Eksportowanie `OcrResult` jako JSON dla usług downstream.  
* Integracja silnika z endpointem REST Spring Boot, aby klienci mogli przesyłać obrazy i natychmiast otrzymywać wyodrębniony tekst.

Miłego kodowania i niech Twoje potoki OCR będą szybkie, dokładne i wielojęzyczne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}