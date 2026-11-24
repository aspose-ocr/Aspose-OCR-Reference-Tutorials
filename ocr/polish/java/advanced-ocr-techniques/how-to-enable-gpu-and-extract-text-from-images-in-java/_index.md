---
category: general
date: 2026-09-16
description: Dowiedz się, jak włączyć GPU, aby przyspieszyć OCR w Javie, rozpoznawać
  tekst z plików graficznych i konwertować obraz na tekst przy użyciu Aspose OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: pl
lastmod: 2026-09-16
og_description: Jak włączyć GPU dla OCR w Javie, rozpoznawać tekst z plików graficznych
  i konwertować obraz na tekst przy użyciu Aspose OCR – kompletny przewodnik krok
  po kroku.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: Jak włączyć GPU i wyodrębnić tekst z obrazów w Javie
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Jak włączyć GPU i wyodrębnić tekst z obrazów w Javie
url: /pl/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU i wyodrębnić tekst z obrazów w Javie

Jeśli potrzebujesz **jak włączyć GPU** dla rozpoznawania znaków optycznych, ten przewodnik pokaże Ci dokładne kroki. Włączając przyspieszenie GPU możesz **rozpoznawać tekst z obrazów** o kilka razy szybciej niż przy przetwarzaniu wyłącznie na CPU. Przykład używa Aspose OCR dla Javy, ale koncepcje mają zastosowanie do każdej biblioteki OCR kompatybilnej z GPU.

W tym samouczku dowiesz się, jak:

* Włączyć przyspieszenie GPU w silniku OCR.  
* Wczytać obraz i **wyodrębnić tekst z obrazów**.  
* **Konwertować obraz na tekst** przy użyciu kilku linii kodu.  

Żadne zewnętrzne usługi nie są wymagane — wszystko działa lokalnie na Twoim komputerze. Podstawowe środowisko programistyczne Javy oraz biblioteka Aspose OCR dla Javy to jedyne wymagania wstępne.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

| Wymaganie | Wersja / Szczegóły |
|-------------|------------------|
| Java Development Kit (JDK) | 8 lub nowszy |
| Maven or Gradle (for dependency management) | Dowolna nowsza wersja |
| GPU with CUDA support (optional but recommended) | NVIDIA GPU with driver ≥ 450 |
| Aspose OCR for Java library | 23.9 lub nowsza (pobierz ze strony Aspose) |

Jeśli nie masz GPU, kod nadal działa; po prostu będzie uruchamiany na CPU.

## Step 1: Add Aspose OCR to your project

Dla Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Dla Gradle, umieść to w `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Te wpisy automatycznie pobierają silnik OCR oraz natywne binaria GPU.

## Step 2: How to enable GPU for the OCR engine

Podstawowym zadaniem jest poinstruowanie `OcrEngine`, aby używał GPU. Aspose OCR udostępnia prostą flagę:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**Dlaczego to ważne:** Gdy wywołasz `setGpuEnabled(true)`, biblioteka ładuje kernele oparte na CUDA, które równolegle przetwarzają wstępne przygotowanie obrazu i segmentację znaków. Na nowoczesnej karcie NVIDIA możesz zauważyć przyspieszenie 2‑4× w porównaniu z domyślną ścieżką CPU.

> **Pro tip:** Zweryfikuj, czy GPU jest wykryte, uruchamiając `SystemInfo.isCudaSupported()` przed włączeniem flagi. Jeśli metoda zwróci `false`, silnik automatycznie przełączy się na CPU.

## Step 3: Load the image you want to process

Możesz podać silnikowi OCR dowolny format obrazu obsługiwany przez Aspose (JPEG, PNG, BMP, TIFF itp.). Oto jak wczytać plik JPEG:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**Edge case:** Jeśli obraz jest duży (powyżej 5 MB), rozważ najpierw jego zmniejszenie, aby ograniczyć zużycie pamięci. Silnik OCR działa najlepiej przy obrazach o rozdzielczości około 300 dpi.

## Step 4: Perform OCR and **recognize text from image**

Teraz, gdy silnik jest skonfigurowany, a obraz wczytany, możesz uruchomić rozpoznawanie:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

Metoda `recognize()` zwraca zwykły `String`. Wewnątrz silnik przechodzi przez kilka etapów:

1. **Pre‑przetwarzanie** – prostowanie, binaryzacja i zwiększanie kontrastu (przyspieszone przez GPU).  
2. **Segmentacja** – wykrywanie linii tekstu, słów i znaków.  
3. **Klasyfikacja** – dopasowywanie każdego znaku do wbudowanego modelu językowego.

Ponieważ GPU jest aktywne, kroki 1 i 2 korzystają najbardziej z równoległego wykonania.

## Step 5: Display or store the extracted text

Na koniec wyświetl wynik w konsoli, zapisz do pliku lub przekaż do dowolnego dalszego przetwarzania:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**Typical output** (dla przykładowego obrazu zawierającego „Hello World”):

```
Recognized text:
Hello World
```

Jeśli OCR nie wykryje żadnych znaków, `recognizedText` będzie pustym ciągiem. W takim wypadku sprawdź jakość obrazu lub wyłącz GPU, aby porównać wydajność.

## Handling common pitfalls

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|-----|
| **GPU nie wykryte** | Brak sterownika CUDA lub nieobsługiwane GPU | Zainstaluj najnowszy sterownik NVIDIA i zweryfikuj przy pomocy `nvidia-smi`. |
| **Niepoprawne znaki** | Niski kontrast lub zaszumione tło | Wstępnie przetwórz obraz (np. zwiększ kontrast) przed przekazaniem go do silnika. |
| **Błąd braku pamięci** | Bardzo duże obrazy przy ograniczonej pamięci GPU | Zmień rozmiar obrazu do ≤ 2000 px szerokości lub przetwarzaj w kafelkach. |
| **Niezgodność języka** | Domyślny model językowy jest angielski, ale tekst jest w innym języku | Wywołaj `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (lub odpowiedni enum) przed `recognize()`. |

## Full, runnable example

Poniżej znajduje się samodzielna klasa Javy, która łączy wszystkie kroki. Zapisz ją jako `GpuEnabledOcrExample.java`, dostosuj ścieżkę do obrazu i uruchom przy pomocy `javac`/`java` lub w IDE.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### Expected result

Uruchomienie programu wypisuje wyodrębniony tekst w konsoli i zapisuje tę samą treść do `recognized_output.txt`. Przy włączonym GPU całkowity czas wykonania dla obrazu 2 MP wynosi zazwyczaj poniżej 200 ms na karcie NVIDIA RTX 3060, w porównaniu z ~500 ms przy samym CPU.

## Conclusion

Teraz wiesz **jak włączyć GPU** dla Aspose OCR w Javie, **rozpoznawać tekst z obrazów** oraz **konwertować obraz na tekst** przy użyciu kilku prostych linii kodu. Wykorzystując przyspieszenie GPU, osiągasz szybsze przetwarzanie, co jest kluczowe w aplikacjach batch‑owych lub w czasie rzeczywistym, takich jak skanowanie faktur, przetwarzanie paragonów i digitalizacja dokumentów.

**Next steps**

* Eksperymentuj z różnymi modelami językowymi (`ocrEngine.setLanguage`), aby **wyodrębnić tekst z obrazów** w języku francuskim, niemieckim lub chińskim.  
* Połącz wynik OCR z Apache Tika, aby automatycznie indeksować wyodrębnioną treść.  
* Zbadaj strumieniowanie dużych plików PDF strona po stronie, jeśli potrzebujesz **rozpoznawać tekst z obrazów** w ramach dokumentu PDF.

Śmiało dostosowuj przykład, integruj go ze swoimi usługami i dziel się wynikami. Szczęśliwego kodowania!

## What Should You Learn Next?

Następujące samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak odczytać tekst z obrazu w Javie przy użyciu Aspose OCR – Kompletny przewodnik](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [rozpoznaj tekst obrazu z Aspose OCR – Pełny samouczek OCR w Javie](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [obraz na tekst java: Konwertuj obraz na tekst przy użyciu Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}