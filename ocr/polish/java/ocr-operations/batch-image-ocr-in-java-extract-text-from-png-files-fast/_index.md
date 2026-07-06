---
category: general
date: 2026-02-14
description: 'Łatwe wsadowe OCR obrazów: dowiedz się, jak wyodrębnić tekst z plików
  PNG przy użyciu Aspose OCR z równoległym przetwarzaniem w Javie.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: pl
og_description: Poradnik dotyczący wsadowkiego OCR obrazów, pokazujący, jak wyodrębnić
  tekst z plików PNG przy użyciu asynchronicznego API Aspose OCR w Javie.
og_title: Wsadowkie OCR obrazów w Javie – szybkie wyodrębnianie tekstu z PNG
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Wsadowkie OCR obrazów w Javie – szybkie wyodrębnianie tekstu z plików PNG
url: /pl/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

PNG](/images/batch-ocr-diagram.png){: .center alt="Diagram przetwarzania batch image OCR"}

Now close shortcodes as original.

Proceed to output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch OCR obrazów w Javie – szybkie wyodrębnianie tekstu z plików PNG

Czy kiedykolwiek musiałeś uruchomić **batch image OCR** na folderze skanów PNG, ale obawiałeś się o szybkość? Nie jesteś sam. W wielu rzeczywistych projektach — digitalizacja faktur, archiwizacja zeskanowanych książek czy przetwarzanie paragonów — programiści muszą **extract text from PNG** obrazy szybko i niezawodnie.  

Dobre wieści? Dzięki asynchronicznemu API Aspose OCR możesz uruchomić równoległy potok OCR w zaledwie kilku linijkach Javy. W tym przewodniku przeprowadzimy Cię przez kompletną, gotową do uruchomienia rozwiązanie, wyjaśnimy, dlaczego każdy element ma znaczenie, i pokażemy, jak zweryfikować wyniki. Po zakończeniu będziesz mieć samodzielny program, który przetwarza całą partię plików PNG równolegle, dostarczając czysty, sprawdzony pod kątem pisowni tekst.

## Czego się nauczysz

- Jak wymienić pliki PNG do przetwarzania wsadowego  
- Konfigurowanie Aspose `OcrEngine` dla języka angielskiego i korekty pisowni  
- Uruchamianie OCR asynchronicznie za pomocą `processAsync` i obsługa wyniku `Future`  
- Odczytywanie i wyświetlanie rozpoznanego tekstu dla każdego obrazu  
- Wskazówki dotyczące skalowania, obsługi błędów i optymalizacji wydajności  

### Wymagania wstępne

- Zainstalowana Java 8 lub nowsza (kod używa standardowego pakietu `java.util.concurrent`)  
- Licencja Aspose OCR for Java lub darmowa wersja próbna (pobierz ze strony Aspose)  
- Folder zawierający kilka zrzutów ekranu PNG lub zeskanowanych stron, które chcesz przetestować  

Zaczynajmy.

## Krok 1 – Zbierz pliki PNG do przetwarzania wsadowego

Zanim silnik OCR będzie mógł wykonać jakąkolwiek pracę, musi wiedzieć, które obrazy przetworzyć. Najprostszym sposobem jest stworzenie `List<String>` z absolutnymi lub względnymi ścieżkami do plików.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Dlaczego to jest ważne:**  
Utworzenie listy z góry pozwala silnikowi planować każdy plik niezależnie, co jest podstawą prawdziwego przetwarzania wsadowego. Jeśli później będziesz musiał skanować katalog dynamicznie, po prostu zamień statyczne `Arrays.asList` na strumień `Files.walk`.

## Krok 2 – Zainicjalizuj i dostrój silnik Aspose OCR

`OcrEngine` Aspose jest wysoce konfigurowalny. Tutaj ustawiamy język na angielski i włączamy korektę pisowni — dwie opcje, które dramatycznie poprawiają jakość wyodrębnionego tekstu, szczególnie z zaszumionych skanów PNG.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Dlaczego te ustawienia:**  
- **Wybór języka** informuje silnik, jaki zestaw znaków i słownik używać, zmniejszając liczbę błędnych rozpoznawań.  
- **Korekta pisowni** łapie typowe błędy OCR (np. „1” vs „l”) bez konieczności późniejszej obróbki wyniku.  

> **Pro tip:** Jeśli Twoje obrazy zawierają wiele języków, możesz przekazać listę taką jak `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Krok 3 – Rozpocznij asynchroniczne przetwarzanie wsadowe

Ciężka praca odbywa się w `processAsync`. Zwraca ona `Future<List<OcrResult>>`, co pozwala głównemu wątkowi wykonywać inne zadania, podczas gdy OCR działa w tle.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Dlaczego asynchronicznie:**  
Uruchamianie OCR kolejno może być bardzo wolne — każdy PNG może zająć sekundę lub więcej. Przekazując pracę do puli wątków, wykorzystujesz wiele rdzeni CPU i znacząco skracasz całkowity czas wykonania.

## Krok 4 – Pobierz wyniki, gdy będą gotowe

Gdy jesteś gotowy, aby wykorzystać wynik, po prostu wywołaj `get()` na obiekcie `Future`. To wywołanie blokuje jedynie do momentu zakończenia OCR, a następnie zwraca listę obiektów `OcrResult` w takiej samej kolejności jak lista wejściowa.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Obsługa limitów czasu:**  
Jeśli chcesz uniknąć nieokreślonego blokowania, użyj `ocrFuture.get(60, TimeUnit.SECONDS)` i przechwyć `TimeoutException`, aby zaimplementować rozwiązanie awaryjne.

## Krok 5 – Wyświetl rozpoznany tekst dla każdego PNG

Teraz, gdy masz wyniki, przeiteruj je i wydrukuj wyodrębniony tekst wraz z oryginalną nazwą pliku. To właśnie miejsce, w którym w końcu **extract text from PNG** pliki.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Przykładowy oczekiwany wynik**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Jeśli silnik OCR nie może rozpoznać strony, odpowiadające `getText()` zwróci pusty ciąg znaków — zawsze warto to sprawdzić w kodzie produkcyjnym.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program, który łączy wszystkie elementy. Skopiuj i wklej go do pliku o nazwie `ParallelOcrDemo.java`, zamień `YOUR_DIRECTORY` na ścieżkę do swojego folderu PNG i uruchom `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Uruchamianie demonstracji

1. **Kompilacja** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Uruchomienie** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Powinieneś zobaczyć nazwę każdego pliku PNG, po której następuje wyodrębniony tekst, oddzielony myślnikami.  

> **Uwaga:** Jeśli napotkasz `LicenseException`, upewnij się, że załadowałeś licencję Aspose przed utworzeniem silnika:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Skalowanie – Wskazówki dla rzeczywistego Batch OCR

| Sytuacja | Zalecenie |
|-----------|----------------|
| **Setki PNG** | Zwiększ rozmiar puli wątków za pomocą `ocrEngine.setThreadPoolSize(8)` (lub większy, dopasowany do liczby rdzeni CPU). |
| **Ograniczenia pamięci** | Przetwarzaj pliki w mniejszych partiach (np. po 50) i zwalniaj listę `OcrResult` po każdej partii. |
| **Zmienna jakość obrazu** | Włącz `setPreprocessingOptions`, aby automatycznie obracać, prostować lub zwiększać kontrast przed rozpoznaniem. |
| **Wiele języków** | Wywołaj `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` i opcjonalnie ustaw własny słownik. |
| **Obsługa błędów** | Umieść `ocrFuture.get()` w bloku try‑catch dla `ExecutionException`, aby logować nieudane pliki bez przerywania całej partii. |

## Najczęściej zadawane pytania

**Q:** Czy to działa z plikami JPEG lub TIFF?  
**A:** Zdecydowanie tak. Metoda `processAsync` akceptuje każdy format obsługiwany przez Aspose OCR (PNG, JPEG, TIFF, BMP, itp.). Wystarczy zmienić rozszerzenia plików w swojej liście.

**Q:** Co zrobić, jeśli muszę zachować układ (tabele, kolumny)?  
**A:** Aspose OCR udostępnia metodę `getLayoutResult()`, która zwraca dane pozycyjne. Możesz odtworzyć tabele, analizując ramki ograniczające każde słowo.

**Q:** Czy mogę uruchomić to na platformie serverless?  
**A:** Tak — wystarczy spakować JAR z biblioteką Aspose i wdrożyć go na AWS Lambda, Azure Functions lub Google Cloud Functions. Pamiętaj, aby przydzielić funkcji wystarczającą ilość pamięci dla puli wątków OCR.

## Zakończenie

Masz teraz kompletną, samodzielną **batch image OCR** rozwiązanie, które efektywnie **extracts text from PNG** pliki przy użyciu asynchronicznego API Aspose OCR w Javie. Samouczek obejmował wszystko, od przygotowania listy plików, przez konfigurację języka i korekty pisowni, uruchomienie równoległego przetwarzania, obsługę wyników, po skalowanie potoku dla obciążeń produkcyjnych.  

Gotowy na kolejny krok? Spróbuj zamienić język na francuski, eksperymentuj z własnymi słownikami lub zintegrować wynik z przeszukiwalnym indeksem ElasticSearch. Nie ma granic, gdy połączysz szybkie batch OCR z nowoczesną współbieżnością Javy.  

Szczęśliwego kodowania i niech Twoje wyodrębnianie tekstu będzie szybkie i precyzyjne! 

![Diagram przedstawiający równoległych pracowników OCR obsługujących wiele plików PNG](/images/batch-ocr-diagram.png){: .center alt="Diagram przetwarzania batch image OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}