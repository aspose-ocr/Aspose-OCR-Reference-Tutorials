---
category: general
date: 2026-02-27
description: Dowiedz się, jak używać OCR w Javie do wyodrębniania tekstu z obrazów
  w plikach TIFF i PDF przy użyciu równoległego przetwarzania Aspose OCR. Szybki,
  prosty przewodnik.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: pl
og_description: Dowiedz się, jak używać OCR w Javie do wyodrębniania tekstu z obrazów
  w formatach TIFF i PDF przy użyciu równoległego przetwarzania Aspose OCR.
og_title: Jak używać OCR w Javie – przetwarzanie równoległe z Aspose
tags:
- OCR
- Java
- Aspose
title: Jak używać OCR w Javie – przetwarzanie równoległe z Aspose
url: /pl/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w Javie – Przetwarzanie równoległe z Aspose

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć tekst ze zeskanowanego dokumentu bez wysiłku? Nie jesteś jedyny. Programiści ciągle napotykają problemy, gdy muszą odczytać tekst z obrazów — szczególnie TIFF‑ów i PDF‑ów — przy zachowaniu wydajności.  

W tym tutorialu pokażemy Ci kompletną, gotową do uruchomienia rozwiązanie, które **wyodrębnia tekst z obrazu w Javie** przy użyciu Aspose OCR, włącza przetwarzanie równoległe i pozwala ograniczyć liczbę wątków. Po zakończeniu będziesz mieć jedną klasę, która może **wykonywać OCR na plikach PDF** oraz **wyodrębniać tekst z obrazów TIFF** w ułamku czasu, jaki zajmuje podejście jednowątkowe.

> **Co zyskasz**  
> * Jasne wyjaśnienie, dlaczego OCR równoległe ma znaczenie.  
> * Pełny program w Javie (bez brakujących importów).  
> * Wskazówki dotyczące dostosowywania użycia wątków i radzenia sobie z typowymi pułapkami.  

## Wymagania wstępne

- Java 8 lub nowszy (kod kompiluje się również z JDK 11).  
- Biblioteka Aspose.OCR for Java – możesz pobrać najnowszy JAR z Maven Central (`com.aspose:aspose-ocr`).  
- Plik obrazu (`.tif`, `.tiff`) lub PDF, który chcesz przetworzyć.  
- Umiarkowana ilość RAM‑u — przetwarzanie równoległe uruchomi kilka wątków, ale Aspose jest oszczędny w pamięci.

Jeśli masz to wszystko, zanurzmy się.

![Diagram przedstawiający pipeline OCR – jak używać OCR w Javie z przetwarzaniem równoległym](how-to-use-ocr-pipeline.png)

*Tekst alternatywny obrazu: diagram przykładu użycia OCR*

---

## Krok 1: Skonfiguruj projekt i dodaj Aspose OCR

### Dlaczego to ważne

Zanim będziesz mógł **wykonywać OCR na PDF** lub dowolnym obrazie, biblioteka musi znajdować się na classpathie. Bez niej kompilator wyrzuci `ClassNotFoundException` i utkniesz na drugim kroku.

### Jak to zrobić

Jeśli używasz Maven, dodaj zależność:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Dla Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Utrzymuj numer wersji zgodny z notatkami wydawniczymi Aspose; nowsze wersje często zawierają ulepszenia wydajności dla przetwarzania równoległego.

---

## Krok 2: Utwórz silnik OCR i włącz przetwarzanie równoległe

### Dlaczego to ważne

Domyślnie Aspose OCR działa na jednym wątku. Gdy podasz mu wielostronicowy PDF lub zestaw TIFF‑ów, silnik przetworzy każdą stronę kolejno — wolno i nieefektywnie. Włączenie przetwarzania równoległego pozwala CPU przetwarzać kilka stron jednocześnie, co znacząco skraca czas wykonania.

### Kod

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Wyjaśnienie kluczowych linii**

- `setUseParallelProcessing(true)`: informuje Aspose, aby podzielił obciążenie na dostępne rdzenie CPU.  
- `setMaxThreads(...)`: możesz ograniczyć pulę wątków, jeśli pracujesz na współdzielonym serwerze lub chcesz zostawić zapas dla innych usług.  
- `processImage(inputPath)`: działa zarówno dla plików obrazów, jak i dokumentów PDF, więc to samo wywołanie **wykonywało OCR na PDF** i na TIFF.

## Krok 3: Obsługa różnych typów wejścia – PDF vs. TIFF

### Dlaczego to ważne

Mimo że `processImage` przyjmuje ciąg ścieżki, wewnętrzna obsługa różni się. PDF‑y często zawierają wiele stron, z których każda staje się osobnym zadaniem OCR. TIFF‑y mogą być jednosktronicowe lub wielostronicowe; Aspose traktuje każdą klatkę jako stronę.

### Na co zwrócić uwagę

| Wejście | Typowy problem | Zalecane rozwiązanie |
|---------|----------------|----------------------|
| PDF | Duże PDF‑y mogą wyczerpać pamięć, jeśli wszystkie strony zostaną załadowane jednocześnie. | Użyj `ocrEngine.getConfig().setMemoryOptimization(true);` (dostępne w nowszych wersjach). |
| Wielostronicowy TIFF | Niektóre starsze TIFF‑y używają nieobsługiwanej kompresji. | Najpierw skonwertuj do obsługiwanego formatu lub użyj pomocnika `TiffImage` Aspose. |

Poniżej znajduje się szybki fragment kodu pokazujący, jak wykryć typ pliku i zalogować przyjazny komunikat:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Krok 4: Weryfikacja wyjścia – co powinieneś zobaczyć?

Gdy program zakończy działanie, zobaczysz surowy wyodrębniony tekst wypisany w konsoli. Dla prostego zeskanowanego faktury, wynik może wyglądać tak:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Jeśli OCR ma trudności z konkretną stroną, Aspose wstawia wiersz zastępczy typu `[Unrecognizable]`. Możesz je później odfiltrować, jeśli potrzebujesz czystych danych.

**Szybka kontrola poprawności**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Krok 5: Dostosowywanie wydajności – kiedy zmienić liczbę wątków

### Dlaczego to ważne

Więcej wątków nie zawsze oznacza szybsze wyniki. Na laptopie z 4‑rdzeniowym procesorem uruchomienie 8 wątków może powodować narzut przełączania kontekstu. Natomiast na serwerze z 32 rdzeniami możesz chcieć wykorzystać pełną moc.

### Jak znaleźć optymalny punkt

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Uruchom program z różnymi ustawieniami i zmierz czas:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Zapisz czasy, wybierz konfigurację dającą najlepszą przepustowość i ustal ją na produkcję.

---

## Krok 6: Rozszerzenie demo – przetwarzanie wsadowe wielu plików

Jeśli potrzebujesz **wyodrębnić tekst obrazu w Java** z całego folderu, otocz główną logikę pętlą:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Ten wzorzec skaluje się dobrze, ponieważ silnik już przetwarza strony każdego pliku równolegle. Zewnętrzna pętla działa sekwencyjnie, ale możesz także przekazać każdy plik do `ExecutorService`, jeśli potrzebujesz wykorzystać ogromną farmę CPU.

---

## Typowe pułapki i jak ich unikać

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|-------|--------------------------|-------------|
| `OutOfMemoryError` | Zbyt wiele stron załadowanych jednocześnie (szczególnie przy dużych PDF‑ach). | Włącz optymalizację pamięci (`setMemoryOptimization(true)`) lub przetwarzaj PDF‑y strona po stronie przy użyciu `processPage`. |
| Zniekształcone znaki | Nieprawidłowa konfiguracja języka/zbioru znaków. | Wywołaj `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` lub odpowiedni enum języka. |
| Wolna wydajność mimo włączonego flagi równoległości | System operacyjny ogranicza tworzenie wątków lub JVM działa z małym rozmiarem sterty. | Zwiększ flagę sterty `-Xmx` i sprawdź limity wątków OS (`ulimit -u`). |
| Pusty wynik | Rozdzielczość obrazu wejściowego < 300 dpi. | Zwiększ rozdzielczość obrazu przed OCR lub użyj skanera, który generuje wyższą rozdzielczość. |

---

## Podsumowanie – co omówiliśmy

- **Jak używać OCR** w Javie z `OcrEngine` Aspose.  
- Włączenie **przetwarzania równoległego**, aby przyspieszyć **wykonywanie OCR na PDF** oraz **wyodrębnianie tekstu z TIFF**.  
- Dostosowywanie liczby wątków dla optymalnej wydajności.  
- Obsługa przypadków brzegowych, takich jak duże PDF‑y, wielostronicowe TIFF‑y i ustawienia języka.  
- Rozszerzenie demo jednoplikowego do przetwarzania wsadowego dla rzeczywistych obciążeń.

---

## Kolejne kroki

Teraz, gdy opanowałeś podstawy, rozważ zgłębienie następujących tematów:

- **Wyodrębnić tekst obrazu w Java** z odręcznych notatek (włącz `setHandwritingRecognition(true)`).  
- Integracja wyniku OCR z Apache Tika w celu ekstrakcji metadanych.  
- Przechowywanie wyników w Elasticsearch dla przeszukiwalnych archiwów dokumentów.  
- Użycie OCR Aspose w innych językach, takich jak Python czy .NET — zasady pozostają takie same.

Śmiało eksperymentuj z różnymi limitami wątków, formatami obrazów i pakietami językowymi. Im więcej się bawisz, tym lepiej zrozumiesz kompromisy między szybkością a dokładnością.

---

### Szczęśliwego kodowania!

Jeśli napotkasz problemy lub masz pomysły na dalszą optymalizację, zostaw komentarz poniżej. Zawsze chętnie porozmawiam o trikach OCR — bez wysiłku, tylko kod.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}