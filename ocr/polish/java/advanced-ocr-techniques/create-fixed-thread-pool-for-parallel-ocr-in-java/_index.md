---
category: general
date: 2026-05-03
description: Utwórz stałą pulę wątków w Javie, aby szybko wyodrębniać tekst z obrazów.
  Dowiedz się, jak uruchomić OCR, konwertować obraz na tekst i zwiększyć wydajność
  dzięki równoległemu przetwarzaniu OCR.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: pl
og_description: Utwórz stałą pulę wątków w Javie, aby szybko wyodrębniać tekst z obrazów.
  Dowiedz się, jak uruchomić OCR, konwertować obraz na tekst i zwiększyć wydajność
  dzięki równoległemu przetwarzaniu OCR.
og_title: Utwórz stałą pulę wątków do równoległego OCR w Javie
tags:
- Java
- OCR
- Multithreading
title: Utwórz stałą pulę wątków dla równoległego OCR w Javie
url: /pl/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Fixed Thread Pool for Parallel OCR in Java

Czy kiedykolwiek potrzebowałeś **create fixed thread pool**, aby przyspieszyć zadania OCR, ale nie wiedziałeś, od czego zacząć? Nie jesteś sam. W wielu projektach z dużą liczbą obrazów wąskim gardłem jest jednowątkowe wywołanie OCR, a rozwiązanie jest zaskakująco proste: uruchom pulę wątków pracowników i pozwól im przetwarzać pliki równolegle.  

W tym samouczku dowiesz się, jak **extract text from images** przy użyciu Aspose OCR, jak **run OCR** wydajnie oraz jak **convert image to text** bez nadmiernego obciążania procesora. Po zakończeniu będziesz mieć gotowy do uruchomienia program w Javie, który demonstruje **parallel OCR processing** na kilku przykładowych obrazach.

## Co zbudujesz

Zbudujemy małą aplikację konsolową, która:

* Odczytuje listę ścieżek do obrazów (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** o rozmiarze równym liczbie rdzeni CPU.
* Rozsyła zadanie OCR dla każdego obrazu.
* Zbiera rozpoznany tekst i wypisuje go w konsoli.
* Czyści i zamyka executor.

Bez zewnętrznych narzędzi budujących, bez skomplikowanych frameworków — tylko czysta Java i biblioteka Aspose OCR. Jeśli masz Java 8+ i przyzwoite IDE, jesteś gotowy.

## Wymagania wstępne

* **Java Development Kit (JDK) 8 or newer** – kod używa lambd, więc starsze wersje nie skompilują się.
* **Aspose OCR for Java** – pobierz plik JAR ze strony Aspose lub pobierz go przez Maven (`com.aspose:aspose-ocr`).
* Folder z kilkoma obrazami testowymi (kod odwołuje się do `YOUR_DIRECTORY`).  
* Podstawowa znajomość współbieżności w Javie (resztę wyjaśnimy).

> *Pro tip:* Jeśli używasz Maven, dodaj zależność do swojego `pom.xml` i pozwól IDE obsłużyć classpath.  

---

## Krok 1: Dodaj wymagane importy

Najpierw wprowadź klasy, których potrzebujemy. To nie jest tylko szablon; każdy import informuje JVM, gdzie znaleźć silnik OCR, narzędzia do obsługi obrazów oraz narzędzia współbieżności, które pozwalają nam **create fixed thread pool**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – podstawowe API OCR.  
* `java.util.*` – kolekcje do przechowywania ścieżek do obrazów i wyników.  
* `java.util.concurrent.*` – pakiet współbieżności zawierający `ExecutorService` i `Future`.

## Krok 2: Zdefiniuj obrazy do przetworzenia

Następnie wymieniamy pliki, z których chcemy **extract text from images**. Użycie `Arrays.asList` utrzymuje kod zwięzły i pozwala zamienić własny katalog bez modyfikacji reszty logiki.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Śmiało dodawaj kolejne pozycje; pula wątków automatycznie dopasuje się do liczby rdzeni CPU, które posiadasz.

## Krok 3: **Create Fixed Thread Pool** dopasowany do rdzeni CPU

To serce samouczka. Zapytujemy środowisko, ile rdzeni jest dostępnych i prosimy fabrykę `Executors` o pulę dokładnie tego rozmiaru. Dlaczego stała? Ponieważ przewidywalna liczba wątków zapobiega przerażającemu „wybuchowi wątków”, który może pozbawić system operacyjny zasobów.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` zwraca liczbę logicznych rdzeni (w tym hyper‑threads).  
* `newFixedThreadPool(coreCount)` gwarantuje, że nigdy nie przekroczymy pojemności CPU, co jest najbezpieczniejszym sposobem na **run OCR** równolegle.

## Krok 4: Prześlij zadanie OCR dla każdego obrazu

Teraz zamieniamy każdą ścieżkę pliku w callable, który **runs OCR**, rozpoznaje tekst i zwraca wynik. Zauważ, że tworzymy nowy `OcrEngine` wewnątrz lambdy — zapobiega to niebezpiecznemu współdzieleniu stanu silnika między wątkami.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Każde wywołanie `submit` przekazuje lambdę do puli, która planuje ją na wolnym wątku.  
* Obiekty `Future<String>` pozwalają później pobrać rozpoznany tekst, zachowując kolejność, jeśli jest potrzebna.

## Krok 5: Pobierz i wyświetl rozpoznany tekst

Gdy wszystkie zadania są w kolejce, po prostu iterujemy po liście `Future`, wywołując `get()`, aby zablokować się aż każde zadanie OCR zakończy się. To właśnie w tym miejscu krok **convert image to text** staje się widoczny: wywołanie `engine.getText()` zwraca surowy ciąg znaków.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Typowy wyjściowy tekst w konsoli wygląda tak:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Jeśli plik się nie uda (np. jest uszkodzony), zobaczysz linię zaczynającą się od `Failed:` i ścieżkę — przydatne do szybkiego debugowania.

## Krok 6: Posprzątaj usługę Executor

Nigdy nie zapominaj zamknąć puli; w przeciwnym razie JVM może pozostać aktywna, myśląc, że wciąż są zadania do wykonania. Łagodne zamknięcie pozwala zakończyć wszystkie uruchomione zadania przed zakończeniem procesu.

```java
executor.shutdown();
```

Możesz także wywołać `awaitTermination`, jeśli potrzebujesz wymusić limit czasu, ale dla większości narzędzi wiersza poleceń zwykłe `shutdown()` wystarczy.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program. Skopiuj go do pliku o nazwie `ParallelOcrTutorial.java`, dostosuj ścieżki do obrazów i uruchom `javac` + `java` tak jak zwykle.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Oczekiwany rezultat:** treść tekstowa każdego obrazu wypisana w konsoli, w tej samej kolejności co lista `imagePaths`. Jeśli któryś obraz nie może zostać przetworzony, zobaczysz komunikat o niepowodzeniu zamiast pustej linii.

## Częste pytania i przypadki brzegowe

### Co jeśli mam więcej obrazów niż wątków?

Stała pula wątków automatycznie umieści w kolejce nadmiarowe zadania. Gdy wątek zakończy bieżące zadanie OCR, przejmuje kolejne. To zachowanie kolejki jest istotą **parallel OCR processing** — uzyskujesz maksymalną przepustowość bez przeciążania CPU.

### Czy mogę zmienić język?

Oczywiście. Zastąp `engine.getLanguage().setEnglish(true);` odpowiednią flagą językową, np. `setFrench(true)` lub włącz wiele języków, wywołując kilka setterów przed `recognize()`.

### Jak obsłużyć bardzo duże obrazy?

Duże pliki mogą zużywać dużo pamięci na wątek. Jeśli zauważysz `OutOfMemoryError`, rozważ zmniejszenie obrazu przed przekazaniem go do silnika lub zwiększ rozmiar sterty przy pomocy `-Xmx`. Inne podejście to użycie **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}