---
category: general
date: 2026-08-28
description: Dowiedz się, jak wyodrębnić tekst z obrazów png w Javie przy użyciu Aspose
  OCR. Ten tutorial obejmuje przetwarzanie batch OCR, odczytywanie obrazów z folderu
  oraz filtrowanie plików po rozszerzeniu.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Dowiedz się, jak wyodrębnić tekst z obrazów png w Javie przy użyciu
  Aspose OCR. Ten tutorial obejmuje przetwarzanie batch OCR, odczytywanie obrazów
  z folderu oraz filtrowanie plików po rozszerzeniu.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Jak wyodrębnić tekst z png w Javie – przewodnik batch OCR
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Jak wyodrębnić tekst z png w Javie – przewodnik batch OCR
url: /pl/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst z pliku png w Javie – przewodnik po przetwarzaniu wsadowym OCR

Jeśli kiedykolwiek musiałeś **wyodrębnić tekst z png** i nie wiedziałeś, jak skalować operację poza kilka obrazów, jesteś we właściwym miejscu. Wielu programistów zaczyna od jednorazowego wywołania OCR dla jednego obrazu i szybko napotyka bariery wydajności, gdy katalog rośnie do dziesiątek lub setek plików. Dzięki Aspose OCR for Java możesz uruchomić solidny potok wsadowego OCR, który przegląda katalog, filtruje tylko interesujące Cię typy obrazów, wykonuje rozpoznawanie równolegle i zwraca wyniki w takiej samej kolejności jak pliki źródłowe. Po przeczytaniu tego przewodnika będziesz mieć gotowy fragment kodu Java, który obsługuje **przetwarzanie wsadowe OCR** niezawodnie i wydajnie.

![Przykład konwersji obrazów na tekst](https://example.com/convert-images-to-text.png "Zrzut ekranu konsoli Java pokazujący przekonwertowany tekst z plików PNG")

## Szybkie odpowiedzi
- **Jaką bibliotekę obsługuje OCR?** Aspose OCR for Java.
- **Czy mogę przetwarzać PNG i JPG razem?** Tak – przykład filtruje oba rozszerzenia.
- **Czy silnik OCR jest bezpieczny wątkowo?** Pojedyncza współdzielona instancja `AsposeOCR` jest bezpieczna dla równoczesnego użycia.
- **Czy potrzebuję licencji do testowania?** Darmowy tymczasowy klucz jest dostępny od Aspose.
- **Czy podfoldery będą skanowane automatycznie?** `Files.walk` przegląda całe drzewo rekurencyjnie.

## Co to jest wyodrębnianie tekstu z png?

`extract text from png` odnosi się do procesu zastosowania optycznego rozpoznawania znaków (OCR) do plików Portable Network Graphics, tak aby widoczne znaki stały się przeszukiwalnymi, edytowalnymi ciągami. Silnik Aspose OCR odczytuje dane pikseli, identyfikuje kształty glifów i zwraca tekst Unicode w jednym wywołaniu metody.

## Dlaczego warto używać Aspose OCR dla Javy?

Aspose OCR obsługuje **ponad 30 języków**, przetwarza do **500 obrazów na minutę** na standardowym serwerze 8‑rdzeniowym i może obsługiwać pliki do **200 MB** bez ładowania całego obrazu do pamięci. Te zmierzone możliwości oznaczają, że możesz niezawodnie uruchamiać duże zadania wsadowe na zwykłym sprzęcie, nie napotykając limitów pamięci.

## Wymagania wstępne
- Java 17 (lub dowolna nowsza wersja LTS).
- Maven lub Gradle do zarządzania zależnościami.
- Katalog zawierający obrazy PNG/JPG, które chcesz przetworzyć.
- Podstawowa znajomość strumieni Java oraz pakietu `java.nio.file`.
- (Opcjonalnie) Tymczasowy klucz licencyjny Aspose OCR do oceny.

> **Wskazówka:** Darmowy tymczasowy klucz wygasa po 30 dniach, ale zapewnia pełny dostęp do API do testów.

## Jak potok wsadowego OCR utrzymuje kolejność?

`Future<OcrResult>` reprezentuje oczekujący wynik OCR, który można pobrać po zakończeniu przetwarzania. Potok zachowuje pierwotną kolejność plików, przechowując obiekty `Future<OcrResult>` w liście odzwierciedlającej kolejność wejściowej kolekcji `Path`. Gdy później iterujesz po futures i wywołujesz `get()`, każde wywołanie blokuje się tylko na odpowiadającym mu obrazie, więc sekwencja wyjściowa zgadza się z sekwencją wejściową bez dodatkowej logiki sortowania.

## Co to jest Aspose OCR dla Javy?

`AsposeOCR` jest klasą centralną biblioteki Aspose OCR, która kapsułkuje wszystkie pakiety językowe, ustawienia rozpoznawania i wewnętrzne zasoby natywne. Została zaprojektowana do jednorazowego utworzenia w czasie życia aplikacji i bezpiecznego współdzielenia między wieloma wątkami. Ponieważ ładuje dane językowe tylko raz, ponowne użycie tej samej instancji zmniejsza narzut inicjalizacji i zwiększa przepustowość przy operacjach wsadowych.

## Jak skonfigurować projekt i dodać Aspose OCR

Najpierw utwórz projekt Maven (lub Gradle) i dodaj zależność Aspose OCR do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Dlaczego to ważne:** Deklaracja zależności z góry zapewnia, że kompilator widzi `AsposeOCR`, `ParallelRecognizer` i powiązane klasy. Gwarantuje to także, że ta sama wersja jest używana na wszystkich maszynach, co jest kluczowe dla odtwarzalnego **przetwarzania wsadowego OCR**.

Odśwież IDE po zakończeniu budowania; powinieneś teraz widzieć pakiety Aspose w sekcji **External Libraries**.

## Jak zainicjalizować silnik OCR – udostępnić jedną instancję

`AsposeOCR` jest główną klasą silnika OCR dostarczaną przez bibliotekę Aspose OCR. Potrzebujemy tylko **jednej** instancji silnika OCR na cały przebieg. Udostępnianie jej wątkom oszczędza pamięć i przyspiesza działanie, ponieważ silnik ładuje pakiety językowe tylko raz.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` jest bezpieczna wątkowo, więc możesz bez obaw przekazać ją do `ParallelRecognizer`, który zarządza pulą wątków pracowników.

> **Wyjaśnienie:** `ParallelRecognizer` otacza silnik w puli wątków. Gdy zgłaszasz wiele plików, każdy otrzymuje własny wątek pracownika, co umożliwia prawdziwe równoległe przetwarzanie na wielordzeniowych CPU.

## Jak odczytać obrazy z folderu – przejść po drzewie katalogów

`Files.walk` jest metodą Java NIO, która rekurencyjnie przegląda drzewo plików i zwraca strumień obiektów `Path`. Teraz musimy **odczytać obrazy z folderu** i zebrać każdy PNG lub JPG. API `Files.walk` umożliwia to w jednej linii, ale dodamy filtr, aby **wyodrębniać tekst z png** tylko w razie potrzeby.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Dlaczego filtrujemy tutaj:** Użycie `filter` pozwala **filtrować pliki po rozszerzeniu** już na wstępie, co eliminuje niepotrzebny I/O później. Zachowuje to także czytelność kodu — nie potrzebujemy skomplikowanych wyrażeń regularnych.

## Jak zgłaszać zadania OCR asynchronicznie

`recognizeAsync` zgłasza obraz do silnika OCR do przetwarzania asynchronicznego i zwraca `Future<OcrResult>` reprezentujący oczekujący wynik. Mając gotową listę plików, przesyłamy każdą ścieżkę do `ParallelRecognizer`. Metoda `recognizeAsync` zwraca `Future<OcrResult>`, które przechowujemy do późniejszego pobrania.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Co się dzieje pod maską?** Każde wywołanie umieszcza zadanie w wewnętrznym executor service rozpoznawacza. Zadania uruchamiają się równolegle, więc katalog z 100 obrazami może zostać przetworzony w ułamku czasu, jaki zajęłaby pętla jednowątkowa.

## Jak pobrać wyniki zachowując kolejność plików

`Future<OcrResult>` przechowuje wynik asynchronicznego zadania OCR i udostępnia metodę `get()`, aby uzyskać rozpoznany tekst. Ponieważ futures zostały zapisane w tej samej kolejności co `imagePaths`, możemy po prostu iterować po liście i wywoływać `get()`. Wywołanie blokuje się tylko do momentu zakończenia przetwarzania konkretnego obrazu, zachowując kolejność bez dodatkowego zarządzania.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Przykładowy output konsoli** (skrócony dla przejrzystości):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Obsługa przypadków brzegowych:** Jeśli konkretny obraz zgłosi wyjątek (uszkodzony plik, nieobsługiwany format), przechwytujemy go i kontynuujemy przetwarzanie pozostałych — to niezbędny nawyk w niezawodnych **potokach przetwarzania wsadowego OCR**.

## Jak zwolnić zasoby – zamknąć rozpoznawacz

`ParallelRecognizer.shutdown()` zatrzymuje wewnętrzną pulę wątków, zapewniając, że wszystkie zadania OCR zakończą się przed zamknięciem aplikacji. Nigdy nie zapominaj zamknąć wewnętrznej puli wątków; w przeciwnym razie JVM może nie zakończyć się poprawnie.

```java
recognizer.shutdown();
```

To wszystko! Program teraz przegląda dowolny katalog, filtruje pliki PNG/JPG, wykonuje OCR równolegle i wypisuje wyniki w pierwotnej kolejności.

---

## Pełny działający przykład (kopiuj‑i‑wklej)

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java. Zamień `"YOUR_DIRECTORY"` na ścieżkę do folderu z obrazami i uruchom go w IDE lub z linii poleceń.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Uruchom klasę, obserwuj jak konsola wypełnia się wyodrębnionymi ciągami i ciesz się faktem, że właśnie **przekonwertowałeś obrazy na tekst** bez pisania pojedynczej pętli blokującej I/O.

---

## Najczęściej zadawane pytania (FAQ)

**Q: Czy mogę przetwarzać także PDF‑y lub TIFF‑y?**  
A: Oczywiście. Aspose OCR obsługuje ponad 30 formatów — w tym PDF, TIFF, BMP i GIF — więc wystarczy dodać pożądane rozszerzenia do filtru w kroku przeglądania katalogu.

**Q: Co zrobić, jeśli potrzebuję języka innego niż angielski, np. hiszpańskiego?**  
A: Zmień `RecognitionLanguage.ENGLISH` na `RecognitionLanguage.SPANISH` (lub dowolny obsługiwany język). Pakiety językowe są dołączone do biblioteki, więc nie ma potrzeby dodatkowego pobierania.

**Q: Mój folder zawiera podfoldery — czy będą skanowane?**  
A: Tak. `Files.walk` przegląda całe drzewo rekurencyjnie, więc każdy zagnieżdżony PNG/J

**Q: Jak obsłużyć bardzo duże obrazy przekraczające 200 MB?**  
A: Włącz tryb strumieniowy, wywołując `ocrEngine.setUseStreaming(true)`. Dzięki temu silnik czyta obraz w fragmentach, znacząco zmniejszając szczytowe zużycie pamięci.

**Q: Czy można ograniczyć liczbę jednoczesnych wątków OCR?**  
A: Tak. Przy tworzeniu `ParallelRecognizer` przekaż żądaną maksymalną liczbę wątków jako drugi argument (np. `new ParallelRecognizer(ocrEngine, 4)`).

---

**Last Updated:** 2026-08-28  
**Tested with:** Aspose OCR for Java 24.10  
**Author:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Powiązane samouczki

- [Konwertuj obrazy na tekst w Javie – przewodnik po przetwarzaniu wsadowym OCR](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Odczytaj tekst z obrazu w Javie – kompletny przewodnik Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Wyodrębnij tekst z obrazów przy użyciu Aspose.OCR – dozwolone znaki](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}