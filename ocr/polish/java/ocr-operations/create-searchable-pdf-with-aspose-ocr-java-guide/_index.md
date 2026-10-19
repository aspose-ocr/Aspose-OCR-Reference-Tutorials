---
category: general
date: 2026-03-26
description: Utwórz przeszukiwalny PDF przy użyciu Aspose.OCR Java – dowiedz się,
  jak wczytać obraz OCR, ustawić język podstawowy, wyodrębnić tekst z obrazu i zapisać
  PDF z OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: pl
og_description: Utwórz przeszukiwalny PDF za pomocą Aspose.OCR Java. Przewodnik krok
  po kroku, jak załadować obraz OCR, ustawić główny język, wyodrębnić tekst z obrazu
  i zapisać PDF z OCR.
og_title: Utwórz przeszukiwalny PDF przy użyciu Aspose.OCR – przewodnik Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Utwórz przeszukiwalny PDF przy użyciu Aspose.OCR – przewodnik Java
url: /pl/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz przeszukiwalny PDF przy użyciu Aspose.OCR – przewodnik Java

Czy kiedykolwiek potrzebowałeś **create searchable pdf** z zeskanowanego dokumentu, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam — wielu programistów napotyka tę przeszkodę, gdy po raz pierwszy zajmuje się OCR w Javie. Dobrą wiadomością jest to, że Aspose.OCR upraszcza cały proces — od wczytania obrazu, przez ustawienie głównego języka, po zapisanie PDF‑a z włączonym OCR — i jest to dość proste. W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który **extracts text from image**, pozwala **set primary language**, i kończy się **save OCR pdf**, który możesz otworzyć w dowolnym czytniku.

Omówimy także kilka praktycznych wskazówek, takich jak włączenie przyspieszenia GPU dla szybszego przetwarzania oraz obsługa dokumentów wielojęzykowych (Tamil + English w naszym przypadku). Po zakończeniu będziesz mieć solidny, gotowy do produkcji fragment kodu, który możesz wstawić do swojego projektu.

## Czego będziesz potrzebować

- **Java 17** (lub dowolny nowszy JDK; Aspose.OCR obsługuje Java 8+)
- **Aspose.OCR for Java** library (pobierz ze strony oficjalnej lub dodaj przez Maven)
- Plik **license file** (lub 30‑dniowa wersja próbna)
- Plik obrazu zawierający tekst (demo używa `sample-mixed-tamil-eng.jpg`)

Bez dodatkowych frameworków, bez natywnych zależności — po prostu czysta Java i pliki Aspose.JAR.

## Krok 1: Utwórz przeszukiwalny PDF — przygotowanie projektu

Zanim przejdziemy do kodu, upewnijmy się, że projekt jest gotowy do **create searchable pdf**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Utrzymuj numer wersji aktualny; nowsze wydania często zawierają poprawki wydajności dla użycia GPU.

Teraz utwórz prostą klasę Java o nazwie `RecentFeaturesDemo`. Klasa będzie zawierać całą logikę potrzebną do **load image OCR**, konfiguracji ustawień językowych i ostatecznie **save OCR pdf**.

## Krok 2: **Load Image OCR** i inicjalizacja silnika

Pierwszym rzeczywistym krokiem w pipeline jest **load image OCR**. To informuje Aspose.OCR, który plik ma analizować.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Why this matters:** Włączenie GPU (`setUseGpu(true)`) może skrócić czas przetwarzania nawet o 70 % na nowoczesnym sprzęcie, a przetwarzanie równoległe zapewnia, że CPU nie jest bezczynne, gdy GPU jest zajęte.

## Krok 3: Ustaw główny język (i język dodatkowy)

Jeśli pominiesz ten krok, Aspose.OCR spróbuje odgadnąć język, co jest wolniejsze i mniej dokładne. Oto jak **set primary language** na Tamil i dodać English jako język zapasowy.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Główny język wpływa na zestaw znaków i słownik używany podczas rozpoznawania. Dodanie języka dodatkowego jest kluczowe dla dokumentów mieszanych (np. paragon z tekstem w Tamil i English).  
> **Edge case:** Jeśli Twój dokument zawiera więcej niż dwa języki, możesz wywołać `addAdditionalLanguage(...)` dla każdego dodatkowego.

## Krok 4: Pre‑process obrazu — prostowanie i odszumianie

Zeskanowane obrazy często cierpią na rotację lub szumy tła. Pre‑processing pomaga silnikowi OCR **extract text from image** bardziej niezawodnie.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Jeśli wiesz, że obraz jest już czysty, możesz pominąć `setDenoise(true)`, aby zaoszczędzić kilka milisekund.

## Krok 5: Wczytaj plik obrazu

Teraz, gdy silnik jest gotowy, wskazujemy go na plik, który chcemy przeanalizować.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **What if the path is wrong?** Aspose.OCR rzuca wyraźny `FileNotFoundException`. Owiń wywołanie w try‑catch, jeśli potrzebujesz łagodnego obsługi błędów.

## Krok 6: Uruchom OCR i **extract Text from Image**

Po skonfigurowaniu wszystkiego, nadszedł czas, aby faktycznie uruchomić rozpoznawanie. Ten krok zarówno **extracts text from image**, jak i przygotowuje dane potrzebne do tworzenia PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Typowy output konsoli dla obrazu demo wygląda tak:

```
வணக்கம் World
This is a mixed language sample.
```

Zauważysz, że linia w języku Tamil jest poprawnie wyświetlana, a następnie English. To efekt prawidłowego **set primary language**.

## Krok 7: **Save OCR PDF** — ostatni element

Ostatnim elementem układanki jest **save OCR pdf**. Aspose.OCR może osadzić niewidzialną warstwę tekstu na oryginalnym obrazie, czyniąc PDF przeszukiwalnym.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Otwórz `searchable.pdf` w Adobe Reader, naciśnij **Ctrl + F**, i możesz wyszukiwać zarówno słowa w Tamil, jak i w English — dokładnie to, co obiecuje workflow **create searchable pdf**.

## Pełny działający przykład (kopiuj‑wklej)

Poniżej znajduje się kompletny program, który możesz skompilować i uruchomić bez zmian. Zamień ścieżki zastępcze na własne katalogi.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Uruchom go za pomocą:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli, a następnie potwierdzenie, że **searchable pdf** został zapisany na dysku.

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję **load image OCR** z tablicy bajtów?

Możesz zamienić `ImageStream.fromFile(imagePath)` na `ImageStream.fromBytes(byteArray)`. Jest to przydatne, gdy obraz pochodzi z bazy danych lub usługi webowej.

### Jak obsłużyć PDF‑y, które już zawierają obrazy?

Aspose.OCR może pracować bezpośrednio na stronach PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Silnik rasteryzuje każdą stronę wewnętrznie przed rozpoznaniem.

### Mój GPU nie jest wykrywany — czy powinienem zostawić `setUseGpu(true)`?

Jeśli `setUseGpu(true)` nie powiedzie się, Aspose.OCR automatycznie przełączy się na CPU. Możesz sprawdzić `ocrEngine.getEngineSettings().isGpuAvailable()` przed włączeniem.

### Czy mogę **save OCR pdf** z własnymi metadanymi?

Tak. Po rozpoznaniu użyj `ocrEngine.getPdfSaveOptions().setTitle("My Document")` lub `setAuthor("John Doe")` przed wywołaniem `save`.

## Wskazówki wydajnościowe dla dużych partii

- **Batch processing:** Ponownie używaj tej samej instancji `OcrEngine` dla wielu obrazów. Wywołuj `ocrEngine.clear()` tylko pomiędzy uruchomieniami.
- **Thread pool:** Owiń każde zadanie obrazu w `Callable` i zgłoś do `ExecutorService`. Ponieważ włączono przetwarzanie równoległe, każdy wątek skorzysta z wielordzeniowego użycia.
- **Memory management:** Dla obrazów o rozdzielczości gigapikselowej rozważ down‑sampling przy użyciu `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)`, aby utrzymać zużycie RAM w ryzach.

## Zakończenie

Przeszliśmy właśnie pełny workflow **create searchable pdf** przy użyciu Aspose.OCR dla Javy. Zaczynając od **load image OCR**, ...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}