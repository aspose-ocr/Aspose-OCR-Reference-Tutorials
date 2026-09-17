---
category: general
date: 2026-01-02
description: Konwertuj obrazy na tekst w Javie przy użyciu Aspose OCR. Opanuj przetwarzanie
  wsadowe OCR, odczytuj obrazy z folderu i filtruj pliki według rozszerzenia.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: pl
og_description: Szybko konwertuj obrazy na tekst w Javie. Ten samouczek obejmuje przetwarzanie
  wsadowe OCR, odczytywanie obrazów z folderu oraz filtrowanie plików według rozszerzenia.
og_title: Konwertuj obrazy na tekst w Javie – Kompletny przewodnik po wsadowym OCR
tags:
- OCR
- Java
- Aspose
title: Konwertowanie obrazów na tekst w Javie – przewodnik po przetwarzaniu wsadowym
  OCR
url: /pl/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie obrazów na tekst w Javie – Przewodnik przetwarzania wsadowego OCR

Kiedykolwiek potrzebowałeś **konwertować obrazy na tekst**, ale nie wiedziałeś, jak poradzić sobie z dziesiątkami plików jednocześnie? Nie jesteś sam — programiści nieustannie walczą z wyciąganiem danych z PNG, JPG i innych skanów. Dobre wieści? Dzięki Aspose OCR możesz w kilka minut uruchomić potok przetwarzania wsadowego OCR, odczytywać obrazy ze struktury folderów i nawet filtrować pliki po rozszerzeniu, aby pracować tylko z tym, co istotne.

W tym samouczku zbudujemy samodzielny program w Javie, który przegląda katalog, wybiera każdy `.png` lub `.jpg`, wysyła każde zdjęcie do Aspose OCR asynchronicznie i wypisuje wyodrębniony tekst w oryginalnej kolejności. Po zakończeniu będziesz mieć wielokrotnego użytku fragment kodu, który możesz wkleić do dowolnego projektu potrzebującego **konwertować obrazy na tekst** w dużej skali.

---

![Przykład konwertowania obrazów na tekst](https://example.com/convert-images-to-text.png "Zrzut ekranu konsoli Java pokazujący przekonwertowany tekst z plików PNG")

## Co zbudujesz

- Jeden silnik `AsposeOCR` współdzielony pomiędzy wątkami (wydajny i bezpieczny wątkowo).  
- `ParallelRecognizer`, który uruchamia zadania OCR równolegle, idealny do **przetwarzania wsadowego OCR**.  
- Logikę, która **odczytuje obrazy z folderu** przy użyciu `java.nio.file.Files`.  
- Proste filtry do **wyodrębniania tekstu z plików PNG**, jednocześnie obsługujące JPG‑y.  
- Czyste zamknięcie wewnętrznego puli wątków, aby uniknąć wycieków zasobów.

### Wymagania wstępne

- Java 17 (lub dowolna nowsza wersja LTS).  
- Maven lub Gradle do pobrania biblioteki Aspose OCR.  
- Folder pełen obrazów PNG/JPG, które chcesz przetworzyć.  
- Podstawowa znajomość strumieni w Javie — nic skomplikowanego nie jest potrzebne.

> **Wskazówka:** Jeśli nie masz jeszcze licencji, Aspose oferuje darmowy tymczasowy klucz, którego możesz użyć do testów.

---

## Krok 1 – Konfiguracja projektu i dodanie Aspose OCR

Najpierw utwórz nowy projekt Maven (lub Gradle, jak wolisz). Dodaj zależność Aspose OCR do pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Dlaczego to ważne:** Zadeklarowanie zależności z góry zapewnia, że kompilator zobaczy `AsposeOCR`, `ParallelRecognizer` i powiązane klasy. Gwarantuje to także, że ta sama wersja będzie używana na wszystkich maszynach, co jest kluczowe dla powtarzalnego **przetwarzania wsadowego OCR**.

Po zakończeniu budowania odśwież IDE i powinieneś zobaczyć pakiety Aspose w sekcji `External Libraries`.

---

## Krok 2 – Konwertowanie obrazów na tekst – Inicjalizacja silnika OCR

Potrzebujemy tylko **jednej** instancji silnika OCR na cały przebieg. Udostępnianie go wątkom oszczędza pamięć i przyspiesza działanie, ponieważ silnik ładuje pakiety językowe tylko raz.

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

> **Wyjaśnienie:** `ParallelRecognizer` opakowuje silnik w pulę wątków. Gdy zgłaszasz wiele plików, każdy otrzymuje własny wątek roboczy, co umożliwia prawdziwe równoległe przetwarzanie na procesorach wielordzeniowych.

---

## Krok 3 – Odczyt obrazów z folderu – Przeglądanie drzewa katalogów

Teraz musimy **odczytać obrazy z folderu** i zebrać każdy plik PNG lub JPG. API `Files.walk` pozwala zrobić to w jednej linii, ale dodamy filtr, aby **wyodrębniać tekst z PNG** tylko wtedy, gdy jest to potrzebne.

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

> **Dlaczego filtrujemy tutaj:** Użycie `filter` pozwala **filtrować pliki po rozszerzeniu** już na wstępie, co ogranicza niepotrzebny I/O później. Dzięki temu kod pozostaje czytelny — nie potrzebujemy skomplikowanych wyrażeń regularnych.

---

## Krok 4 – Przetwarzanie wsadowe OCR – Asynchroniczne zgłaszanie zadań

Mając gotową listę plików, przekazujemy każdą ścieżkę do `ParallelRecognizer`. Metoda `recognizeAsync` zwraca `Future<OcrResult>`, które przechowujemy do późniejszego pobrania.

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

> **Co się dzieje w tle?** Każde wywołanie umieszcza zadanie w wewnętrznej usłudze wykonawczej rozpoznawacza. Zadania uruchamiają się równolegle, więc folder ze 100 obrazami może zostać przetworzony w ułamku czasu, jaki zajęłaby jednowątkowa pętla.

---

## Krok 5 – Pobieranie wyników w oryginalnej kolejności – Zachowanie kolejności plików

Ponieważ przechowujemy `Future`‑y w tej samej kolejności co `imagePaths`, możemy po prostu iterować po liście i wywoływać `get()`. Wywołanie blokuje tylko do momentu zakończenia przetwarzania konkretnego obrazu, zachowując kolejność bez dodatkowego zarządzania.

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

**Przykładowe wyjście konsoli** (skrócone dla przejrzystości):

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

> **Obsługa przypadków brzegowych:** Jeśli konkretny obraz zgłosi wyjątek (uszkodzony plik, nieobsługiwany format), przechwytujemy go i kontynuujemy przetwarzanie pozostałych — to niezbędny nawyk w niezawodnych **potokach przetwarzania wsadowego OCR**.

---

## Krok 6 – Sprzątanie – Zamykanie rozpoznawacza

Nigdy nie zapominaj zamknąć wewnętrznej puli wątków; w przeciwnym razie JVM może nie zakończyć się poprawnie.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

To wszystko! Program będzie teraz przeglądał dowolny katalog, filtrował pliki PNG/JPG, uruchamiał OCR równolegle i wypisywał wyniki.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do skopiowania i wklejenia kod klasy Java. Zamień `"YOUR_DIRECTORY"` na ścieżkę do folderu z obrazami i uruchom ją w IDE lub z wiersza poleceń.

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

Uruchom klasę, obserwuj, jak konsola wypełnia się wyodrębnionymi ciągami znaków i ciesz się faktem, że właśnie **konwertowałeś obrazy na tekst** bez pisania żadnej pętli blokującej I/O.

---

## Najczęściej zadawane pytania (FAQ)

**P: Czy mogę również przetwarzać pliki PDF lub TIFF?**  
**O:** Oczywiście. Aspose OCR obsługuje wiele formatów — wystarczy dodać odpowiednie rozszerzenia plików do filtru w Kroku 2.

**P: Co zrobić, jeśli potrzebuję innego języka, np. hiszpańskiego?**  
**O:** Zmień `RecognitionLanguage.ENGLISH` na `RecognitionLanguage.SPANISH`. Upewnij się, że pakiet językowy jest zainstalowany (Aspose zawiera większość głównych języków od razu).

**P: Mój folder zawiera podfoldery — czy będą skanowane?**  
**O:** Tak. `Files.walk` przeszukuje całe drzewo rekurencyjnie, więc każdy zagnieżdżony PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}