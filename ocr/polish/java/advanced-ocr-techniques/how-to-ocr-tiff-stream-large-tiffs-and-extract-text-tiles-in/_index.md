---
category: general
date: 2026-04-29
description: Dowiedz się, jak wykonywać OCR plików TIFF przy użyciu trybu strumieniowego
  Aspose OCR. Ten przewodnik pokazuje, jak efektywnie wyodrębniać fragmenty tekstu
  z podzielonych na kafelki obrazów TIFF.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: pl
og_description: jak wykonać OCR pliku TIFF przy użyciu strumieniowego Aspose OCR.
  Krok po kroku kod do wyodrębniania fragmentów tekstu z dużych obrazów TIFF.
og_title: Jak zrobić OCR TIFF – Kompletny przewodnik po strumieniowaniu
tags:
- OCR
- Java
- Aspose
- TIFF
title: Jak zrobić OCR TIFF – strumieniowanie dużych plików TIFF i wyodrębnianie tekstowych
  kafelków w Javie
url: /pl/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak wykonać OCR TIFF – Strumieniowanie dużych plików TIFF i wyodrębnianie fragmentów tekstu w Javie

Zastanawiałeś się kiedyś **jak wykonać OCR TIFF** dla plików, które są zbyt duże, aby załadować je jednocześnie do pamięci? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy ich obrazy TIFF są podzielone na dziesiątki kafelków, a zwykłe wywołanie `ocrEngine.recognize()` po prostu się zacina.  

Dobre wieści? Tryb strumieniowy Aspose OCR pozwala podawać każdy kafelek jako osobny strumień, dzięki czemu możesz **wyodrębniać fragmenty tekstu** bez przepełniania sterty. W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład w Javie, wyjaśnimy, dlaczego każda linia ma znaczenie, i wskażemy pułapki, których warto unikać.

> **Co otrzymasz:** program uruchamialny, który łączy kafelkowane pliki TIFF w locie, wypisuje połączony tekst i pokazuje, jak dostosować kod do innych języków lub formatów obrazu.

## Wymagania wstępne

- **Java 17** lub nowszy (kod używa try‑with‑resources, więc JDK 8+ działa, ale JDK 17 jest aktualnym LTS).
- **Aspose.OCR for Java** library (v23.10 lub nowsza). Dodaj ją przez Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Folder zawierający poszczególne kafelki TIFF (np. `tile_0.tif`, `tile_1.tif`, …).  
- Opcjonalnie: IDE takie jak IntelliJ IDEA lub VS Code – ale prosty edytor tekstu również się sprawdzi.

## Krok 1 – Przygotowanie ścieżek do kafelków (Dlaczego to ważne)

Zanim silnik OCR będzie mógł cokolwiek zrobić, musi wiedzieć, gdzie znajduje się każdy fragment obrazu. Hard‑kodowanie ścieżek jest w porządku dla demonstracji, ale w produkcji prawdopodobnie zeskanujesz katalog lub odczytasz plik manifestu.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** trzymaj kafelki w kolejności leksykalnej (0, 1, 2…), ponieważ silnik połączy rozpoznany tekst w takiej samej kolejności, w jakiej podajesz strumienie.

## Krok 2 – Włączenie trybu strumieniowego w silniku OCR (Primary Keyword)

Teraz tworzymy instancję `OcrEngine` i włączamy tryb strumieniowy. To jest sedno **jak wykonać OCR TIFF** bez ładowania całego obrazu do RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Dlaczego strumieniowanie?**  
Gdy wywołasz `setEnableStreaming(true)`, silnik traktuje każdy przychodzący `ImageStream` jako kontynuację poprzedniego. Tworzy wewnętrzne wirtualne płótno, wirtualnie łączy kafelki i uruchamia OCR raz na końcu. Dzięki temu unika się błędu „OutOfMemoryError”, który wystąpiłby przy próbie załadowania wielogigabajtowego pliku TIFF jednorazowo.

## Krok 3 – Dodawanie każdego kafelka jako strumienia wejściowego (Secondary Keyword)

Oto pętla, która podaje każdy kafelek do silnika. Blok `try‑with‑resources` zapewnia szybkie zamknięcie uchwytu pliku, co jest kluczowe przy obsłudze dziesiątek plików.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Zauważ, że fraza **wyodrębnia fragmenty tekstu** jest naturalnie wbudowana: każda iteracja *wyodrębnia* tekst z kafelka i dodaje go do rosnącego zestawu wyników.

## Krok 4 – Uruchomienie rozpoznawania i wyświetlenie połączonego tekstu (Primary Keyword)

Po zakolejkowaniu wszystkich kafelków, pojedyncze wywołanie wykonuje OCR na wirtualnym obrazie. Wynik zawiera pełny tekst, tak jakbyś miał jeden ogromny plik TIFF.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Oczekiwany wynik** (zakładając, że kafelki zawierają frazę „Hello World” podzieloną pomiędzy nimi):

```
=== OCR Output ===
Hello World
```

Jeśli Twoje kafelki zawierają więcej linii, pojawią się w takiej samej kolejności, w jakiej je podałeś. Możesz także zapisać `ocrResult.getText()` do pliku w celu dalszego przetwarzania.

## Krok 5 – Pełny, uruchamialny przykład (Wszystkie kroki w jednym miejscu)

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do `StreamingExample.java`. Zawiera wszystkie importy, komentarze i obsługę błędów.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Zapisz, skompiluj i uruchom:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Powinieneś zobaczyć połączony tekst OCR wydrukowany w konsoli.

## Zaawansowane wskazówki i typowe pułapki (Dlaczego to działa)

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Błędy Out‑of‑memory** | Ładowanie pełnowymiarowego TIFF do `BufferedImage` zużywa całą stertę. | Użyj trybu strumieniowego (`setEnableStreaming(true)`) – silnik nigdy nie materializuje całego obrazu. |
| **Niezgodność kolejności kafelków** | Pliki sortowane alfabetycznie zamiast numerycznie (np. `tile_10.tif` przed `tile_2.tif`). | Uzupełnij liczby zerami (`tile_00.tif`, `tile_01.tif`) lub sortuj programowo przy użyciu `Comparator`. |
| **Nieprawidłowy język** | OCR domyślnie używa języka angielskiego; tekst nieangielski staje się zniekształcony. | Wywołaj `ocrEngine.getLanguageSettings().setLanguage("fr")` (lub dowolny obsługiwany kod ISO). |
| **Częściowe awarie** | Jeden uszkodzony kafelek zatrzymuje cały proces. | Przechwyć `IOException` dla każdego kafelka, zaloguj i zdecyduj, czy kontynuować, czy przerwać. |
| **Wąskie gardło wydajności** | Operacje dyskowe dominują przy odczycie wielu małych plików. | Spakuj kafelki do ZIP i strumieniuj z pamięci, lub użyj szybkiego SSD. |

## Kiedy używać trybu strumieniowego vs. OCR pojedynczego obrazu

- **Strumieniowanie** jest idealne dla:
  - Wielostronicowe TIFF lub skany gigapikselowe.
  - Sytuacji, w których pamięć jest ograniczona (np. kontenery Docker, urządzenia mobilne).
  - Potoków, które już otrzymują fragmenty obrazu (np. strumienie z kamery).

- **OCR pojedynczego obrazu** sprawdza się dla:
  - Małych plików PNG/JPEG (< 5 MB).
  - Jednorazowych skanów, gdzie prostota przewyższa wydajność.

## Podsumowanie

Masz teraz solidne pojęcie o **jak wykonać OCR TIFF** przy użyciu możliwości strumieniowych Aspose OCR i wiesz, jak **wyodrębniać fragmenty tekstu** efektywnie. Kompletny rozwiązanie — inicjalizacja silnika, włączenie trybu strumieniowego, dodawanie każdego kafelka i ostateczne rozpoznanie wirtualnego płótna — obejmuje „co”, „dlaczego” i „jak” potrzebne do kodu gotowego do produkcji.

Kolejne kroki? Spróbuj zamienić `"en"` na inny język lub poeksperymentuj z różnymi formatami obrazów (`.png`, `.jpg`). Możesz także przekazać wynik OCR bezpośrednio do indeksu wyszukiwania lub generatora PDF. Wzorzec pozostaje ten sam: strumieniuj, łącz, rozpoznawaj.

Masz pytania dotyczące skalowania do setek kafelków lub potrzebujesz pomocy z obsługą błędów? zostaw komentarz poniżej i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}