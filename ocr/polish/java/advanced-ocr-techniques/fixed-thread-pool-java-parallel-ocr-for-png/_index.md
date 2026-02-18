---
category: general
date: 2026-02-17
description: Dowiedz się, jak używać stałej puli wątków w Javie do wyodrębniania tekstu
  z obrazów PNG przy równoległym przetwarzaniu OCR i prawidłowo zamykać usługę wykonawczą.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: pl
og_description: Odkryj, jak stała pula wątków w Javie może równolegle wyodrębniać
  tekst z obrazów PNG, konwertować tekst zeskanowanych stron i bezpiecznie zamykać
  usługę wykonawczą.
og_title: Stała pula wątków w Javie – równoległe OCR dla PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Stała pula wątków w Javie – równoległe OCR dla PNG
url: /pl/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# stała pula wątków Java – równoległe OCR dla PNG

Zastanawiałeś się kiedyś, jak przyspieszyć OCR na zestawie plików PNG przy użyciu **fixed thread pool java**? W tym samouczku przeprowadzimy Cię przez **extract text from PNG** obrazy równolegle, **convert scanned pages text** w edytowalne ciągi znaków oraz bezpiecznie **shut down executor service**, gdy praca zostanie zakończona.

Jeśli kiedykolwiek wpatrywałeś się w jednowątkową pętlę, która ciągnie się minutami, znasz frustrację czekania, aż każda strona się zakończy, zanim zacznie się kolejna. Dobra wiadomość? Kilka linijek Javy i Aspose OCR pozwoli Ci wykorzystać moc wszystkich rdzeni CPU, zamienić zeskanowane strony w przeszukiwalny tekst i utrzymać aplikację responsywną.  

Poniżej znajdziesz kompletny, gotowy do uruchomienia przykład, wraz z wyjaśnieniami, dlaczego każdy element ma znaczenie, typowymi pułapkami i wskazówkami, które możesz zastosować w dowolnej bibliotece OCR.

---

## Co będziesz potrzebować

- **Java 17** (lub dowolny nowoczesny JDK) – kod używa nowoczesnej składni `var` oszczędnie, ale działa również na starszych wersjach.  
- **Aspose.OCR for Java** library – możesz ją pobrać z Maven Central lub ściągnąć wersję trial z Aspose.  
- Zestaw plików **PNG**, które chcesz przetworzyć – np. zeskanowane paragony, strony książek lub zrzuty ekranu.  
- Podstawowa znajomość współbieżności w Javie – nie jest wymagana, ale przydatna.

To wszystko. Brak zewnętrznych usług, brak Dockera, tylko czysta Java i odrobina magii wielowątkowości.

## Krok 1: Dodaj zależność Aspose OCR i licencję (opcjonalnie)

Najpierw upewnij się, że JAR Aspose OCR znajduje się na classpathie. Jeśli używasz Maven, dodaj:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Jeśli nie masz licencji, biblioteka będzie działać w trybie ewaluacyjnym; kod działa tak samo. Aby załadować licencję (zalecane w produkcji), umieść `Aspose.OCR.lic` w folderze resources i użyj:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Trzymaj plik licencji poza kontrolą wersji, aby uniknąć przypadkowego ujawnienia.

## Krok 2: Utwórz wątkowo‑bezpieczną instancję `OcrEngine`

`OcrEngine` z Aspose OCR jest wątkowo‑bezpieczny, o ile używasz tej samej instancji we wszystkich zadaniach. Utworzenie jej raz oszczędza pamięć i eliminuje narzut ponownego inicjowania silnika dla każdego obrazu.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Dlaczego warto ponownie używać? Wyobraź sobie silnik jako ciężkiego pracownika, który ładuje modele językowe do pamięci. Tworzenie nowego silnika dla każdego obrazu byłoby jak zatrudnianie nowego specjalisty do każdej drobnej pracy – kosztowne i niepotrzebne.

## Krok 3: Skonfiguruj stałą pulę wątków Java

Teraz przychodzi gwiazda programu: **fixed thread pool java**. Ustawimy jego rozmiar na liczbę logicznych procesorów, aby każdy rdzeń otrzymał pracę bez nadmiernego przydzielania.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Użycie *stałej* puli (zamiast cached) daje przewidywalne zużycie zasobów i zapobiega niechcianym skokom „out‑of‑memory”, gdy nagle pojawi się setki obrazów.

## Krok 4: Wypisz pliki PNG, które chcesz przetworzyć (Extract Text from PNG)

Zbierz ścieżki do obrazów, które chcesz poddać OCR. W prawdziwym projekcie możesz przeszukać katalog lub odczytać je z bazy danych; tutaj zakodujemy kilka przykładów na sztywno.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note:** Rozszerzenie pliku **png** jest ważne, ponieważ Aspose OCR automatycznie wykrywa format, ale możesz podać także JPEG lub TIFF.

## Krok 5: Zgłoś zadania OCR – równoległe przetwarzanie OCR

Każdy obraz staje się obiektem `Callable`, który zwraca rozpoznany tekst. Ponieważ `OcrEngine` jest współdzielony, wystarczy przekazać ścieżkę pliku do zadania.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Dlaczego opakowujemy to w `Future`? Pozwala nam natychmiast uruchomić wszystkie zadania, a później zebrać wyniki w kolejności ich zgłoszenia – idealne do zachowania kolejności stron przy **convert scanned pages text** z powrotem do dokumentu.

## Krok 6: Pobierz wyniki i wyświetl (Convert Scanned Pages Text)

Teraz czekamy, aż każdy `Future` zakończy się i wypisujemy wynik. Wywołanie `get()` blokuje tylko do momentu zakończenia konkretnego zadania, nie całej puli.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Typowy output w konsoli wygląda tak:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Jeśli wolisz zapisywać wyniki do plików, zamień `System.out.println` na wywołanie `Files.writeString`.

## Krok 7: Czyść zamknięcie usługi Executor

Gdy wszystkie zadania zostaną wykonane, kluczowe jest **shut down executor service**; w przeciwnym razie JVM może utrzymywać wątki nie‑daemonowe, uniemożliwiając eleganckie zakończenie.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Wzorzec `awaitTermination` daje puli szansę na dokończenie bieżącej pracy przed wymuszeniem zamknięcia. Pomijanie tego kroku jest częstą przyczyną wycieków pamięci w długotrwale działających aplikacjach.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować‑wkleić do `ParallelBatchDemo.java` i uruchomić:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}