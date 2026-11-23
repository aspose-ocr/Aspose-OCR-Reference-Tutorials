---
category: general
date: 2026-07-05
description: Kompresuj obrazy PDF podczas konwertowania PNG do PDF przy użyciu Javy.
  Naucz się wstępnego przetwarzania obrazów dla OCR, rozpoznawania tekstu w JPG oraz
  wsadowego OCR do PDF w jednym samouczku.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: pl
og_description: Kompresuj obrazy PDF i konwertuj PNG do PDF przy użyciu Javy. Ten
  przewodnik obejmuje wstępne przetwarzanie obrazów dla OCR, rozpoznawanie tekstu
  w JPG oraz wsadowe OCR do PDF.
og_title: Kompresuj obrazy PDF w Javie – Kompletny samouczek OCR wsadowego
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Kompresja obrazów PDF w Javie – Kompletny przewodnik po wsadowym OCR do PDF
url: /pl/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kompresja obrazów PDF w Javie – Kompletny przewodnik Batch OCR do PDF

Czy kiedykolwiek potrzebowałeś **skompresować obrazy PDF**, jednocześnie zamieniając folder PNG‑ów w przeszukiwalne PDF‑y? Nie jesteś jedyny. W wielu pipeline’ach automatyzacji największym problemem jest jednoczesne balansowanie jakością obrazu, dokładnością OCR i ostatecznym rozmiarem PDF — wszystko naraz.  

W tym samouczku przeprowadzimy praktyczne rozwiązanie, które **konwertuje PNG do PDF**, stosuje **przetwarzanie wstępne obrazu dla OCR**, a na końcu **kompresuje obrazy PDF**, aby wynikowy plik był lekki. Po zakończeniu będziesz wiedział, jak **rozpoznawać tekst w plikach JPG**, skonfigurować **wsadowe OCR do PDF** oraz utrzymać porządek w swoich PDF‑ach.

## Czego się nauczysz

- Konfiguracja Aspose OCR dla Java i zastosowanie licencji.
- Ustawienie silnika pod kątem wielowątkowości, przyspieszenia GPU i korekcji pisowni.
- Budowanie wielokrotnego użytku **przetwarzania wstępnego obrazu dla OCR** (odszumianie, kontrast, binaryzacja).
- Użycie **PdfSaveOptions** do **kompresji obrazów PDF** bez utraty czytelności.
- Przeglądanie katalogu w celu **konwersji PNG do PDF** i **rozpoznawania tekstu JPG** hurtowo.
- Kompletny, gotowy do uruchomienia program w Javie, który możesz wkleić do dowolnego projektu.

> **Wymagania wstępne**: Java 8+, Maven lub Gradle, licencja Aspose OCR dla Java oraz folder z obrazami PNG/JPG, które chcesz przetworzyć.

---

## Krok 1: Zastosowanie licencji Aspose OCR (kluczowe dla produkcji)

Zanim wywołasz jakiekolwiek API OCR, musisz załadować ważną licencję; w przeciwnym razie będziesz ograniczony do wersji trial.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Dlaczego to ważne*: Licencjonowany silnik odblokowuje wsparcie GPU, wyższą dokładność i usuwa znaki wodne, które w przeciwnym razie zwiększałyby rozmiar Twoich plików PDF.

---

## Krok 2: Konfiguracja silnika OCR – wątki, GPU i korekcja pisowni

Szybki silnik OCR jest podstawą każdego zadania **batch OCR to PDF**. Uruchomimy tyle wątków, ile pozwala CPU hosta, włączymy przyspieszenie GPU (jeśli masz kompatybilną kartę) i zacieśnimy korekcję pisowni, aby wyeliminować błędy OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: Jeśli uruchamiasz na serwerze bez interfejsu graficznego i bez GPU, po prostu ustaw `gpu.setEnabled(false)` – kod będzie działał, choć nieco wolniej.

---

## Krok 3: Budowa pipeline’u przetwarzania wstępnego obrazu

Surowe skany często cierpią na szumy, niski kontrast lub nierównomierne oświetlenie. **Przetwarzanie wstępne obrazu dla OCR** dramatycznie podnosi wskaźniki rozpoznawania, szczególnie w scenariuszach **rozpoznawania tekstu JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Dlaczego łączymy te kroki*: Odszumianie jako pierwsze zapobiega wzmocnieniu drobnych plam przez binaryzator; kontrast zapewnia wyraźne znaki; na końcu binaryzacja daje silnikowi OCR czysty obraz binarny do analizy.

---

## Krok 4: Przygotowanie opcji zapisu PDF – **kompresja obrazów PDF** efektywnie

Aspose pozwala precyzyjnie dostroić wyjście PDF. Włączymy kompresję obrazu i ustawimy poziom jakości, który balansuje rozmiar i czytelność.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Rezultat*: Każdy przeszukiwalny PDF będzie zauważalnie mniejszy — idealny do archiwizacji lub wysyłania mailem.

---

## Krok 5: Przetwarzanie katalogu – **konwersja PNG do PDF** i **rozpoznawanie tekstu JPG** w jednej pętli

Teraz łączymy wszystko. Pętla przechodzi przez katalog wejściowy, wykonuje OCR na każdym PNG lub JPG i zapisuje przeszukiwalny PDF do katalogu wyjściowego. Nazwa PDF‑a odzwierciedla nazwę źródłowego obrazu.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje linię dla każdego obrazu, np.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Otwórz dowolny wygenerowany PDF w przeglądarce i zobaczysz zaznaczalny, przeszukiwalny tekst, przy czym rozmiar pliku jest zazwyczaj **o 30‑50 % mniejszy** niż w wersji nie‑skompresowanej.

---

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli mój serwer nie ma GPU?
Po prostu ustaw `gpuSettings.setEnabled(false)`. Reszta pipeline’u pozostaje niezmieniona, a Ty nadal otrzymujesz przetwarzanie wielowątkowe na CPU.

### Moje PDF‑y wciąż są za duże — czy mogę jeszcze bardziej obniżyć jakość?
Tak. Dostosuj `options.setImageQuality(70)` lub nawet `50`. Niższe wartości jeszcze bardziej zmniejszają rozmiar, ale mogą rozmywać drobne glify. Przetestuj na reprezentatywnej próbce.

### Jak obsłużyć inne formaty obrazów (TIFF, BMP)?
Dodaj rozszerzenia do lambdy filtru:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Ten sam pipeline przetwarzania wstępnego działa dla większości formatów rastrowych.

### Czy mogę zachować oryginalne obrazy kolorowe zamiast binaryzować?
Zastąp `.addBinarize()` przez `.addGrayscale()` w konstruktorze preprocesora, jeśli potrzebujesz zachować kolory do dalszej analizy.

---

## Pro Tips dla produkcyjnego Batch OCR

- **Zarządzanie pamięcią**: Ponownie używaj jednej instancji `OcrEngine` (jak pokazano), aby uniknąć kosztów tworzenia/usuwania obiektów przy każdym obrazie.
- **Obsługa błędów**: Owiń blok per‑plik w `try/catch`, aby logować niepowodzenia bez przerywania całej partii.
- **Logowanie**: Używaj prawdziwego frameworka logowania (SLF4J, Log4j) zamiast `System.out.println` w rozwiązaniach skalowalnych.
- **Równoległość**: Przy ogromnych katalogach rozważ przetwarzanie podkatalogów strumieniami równoległymi, ale monitoruj konkurencję o zasoby GPU.
- **Bezpieczeństwo**: Przechowuj plik licencji poza repozytorium i zabezpiecz go odpowiednimi uprawnieniami systemu plików.

---

## Zakończenie

Pokazaliśmy, jak **kompresować obrazy PDF** podczas wykonywania **wsadowego OCR do PDF**, które **konwertuje PNG do PDF**, **rozpoznaje tekst JPG** i stosuje solidny **pipeline przetwarzania wstępnego obrazu dla OCR**. Pełny program w Javie jest samodzielny, działa na dowolnym nowoczesnym JDK i generuje lekkie, przeszukiwalne PDF‑y gotowe do archiwizacji lub dalszej analizy.

Co dalej? Eksperymentuj z różnymi parametrami przetwarzania wstępnego, wypróbuj języki OCR inne niż angielski lub zintegrować workflow z mikrousługą Spring Boot, która monitoruje katalog i przetwarza pliki w locie. Podstawowe koncepcje — ładowanie licencji, konfiguracja silnika, przetwarzanie wstępne i kompresja PDF — pozostają takie same, dając solidną bazę dla każdego projektu opartego na OCR.

Masz pytania lub chcesz podzielić się własnymi usprawnieniami? zostaw komentarz poniżej i powodzenia w kodowaniu!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## Co powinieneś nauczyć się dalej?


Poniższe samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każde z nich zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Rozpoznawanie tekstu PDF – Operacje OCR z Aspose.OCR dla Java](/ocr/english/java/ocr-operations/)
- [rozpoznawanie obrazu tekstowego z Aspose OCR – Pełny samouczek OCR w Javie](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Konwersja obrazu na tekst w Javie przy użyciu Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}