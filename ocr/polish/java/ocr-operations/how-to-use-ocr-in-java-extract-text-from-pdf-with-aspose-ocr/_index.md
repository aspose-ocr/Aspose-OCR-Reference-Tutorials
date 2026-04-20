---
category: general
date: 2026-02-17
description: Jak używać OCR w Javie do wyodrębniania tekstu z PDF, konwertowania PDF
  na obrazy oraz wykonywania OCR na zeskanowanych plikach PDF przy użyciu Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: pl
og_description: Jak używać OCR w Javie do wyodrębniania tekstu z plików PDF. Dowiedz
  się, jak konwertować PDF na obrazy i rozpoznawać zeskanowane PDF za pomocą Aspose.OCR.
og_title: Jak używać OCR w Javie – kompletny przewodnik
tags:
- OCR
- Java
- Aspose
title: Jak używać OCR w Javie – wyodrębnianie tekstu z PDF przy użyciu Aspose.OCR
url: /pl/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w Javie – wyodrębnić tekst z PDF za pomocą Aspose.OCR

Zastanawiałeś się kiedyś **jak używać OCR**, aby zamienić zeskanowany PDF na przeszukiwalny tekst? Nie jesteś sam. Większość programistów napotyka problem, gdy PDF przychodzi jako zbiór obrazów, a tradycyjne ekstraktory tekstu po prostu nic nie zwracają. Dobre wieści? Kilka linii Javy i Aspose.OCR pozwala **wyodrębnić tekst z PDF**, **przekonwertować PDF na obrazy** oraz **rozpoznać zeskanowany PDF** w jednym, prostym procesie.

W tym tutorialu przejdziemy krok po kroku przez wszystko, co musisz wiedzieć – od licencjonowania biblioteki po wypisanie ostatecznego wyniku. Na końcu będziesz mieć gotowy do uruchomienia program, który wyciąga czysty tekst z dowolnego zeskanowanego raportu, faktury czy ebooka. Bez zewnętrznych usług, bez magii – tylko czysty kod Javy, którym sam sterujesz.

## Czego będziesz potrzebować

- **Java Development Kit (JDK) 8+** – dowolna współczesna wersja.
- **Aspose.OCR for Java** JAR (pobierz ze strony Aspose).  
- **Ważny plik licencji Aspose.OCR** (`Aspose.OCR.lic`). Bezpłatna wersja próbna działa, ale licencja odblokowuje pełną dokładność.
- **Przykładowy zeskanowany PDF** (np. `scanned-report.pdf`).  
- IDE lub prosty edytor tekstu oraz terminal.

To wszystko. Bez Maven, bez Gradle, bez dodatkowych zależności – tylko JAR Aspose.OCR w classpath.

![przykład użycia OCR](image-placeholder.png "przykład użycia OCR")

## Krok 1 – Załaduj licencję Aspose.OCR (Dlaczego to ważne)

Zanim silnik będzie działał pełną prędkością, musisz wskazać, gdzie znajduje się twoja licencja. Pominięcie tego kroku powoduje, że biblioteka działa w trybie ewaluacyjnym, dodając znak wodny do wyników i potencjalnie ograniczając dokładność.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Dlaczego to działa:** Klasa `License` odczytuje plik `.lic` i rejestruje go globalnie. Po ustawieniu, każdy utworzony `OcrEngine` automatycznie korzysta z licencjonowanych funkcji.

## Krok 2 – Utwórz silnik OCR (Silnik stojący za magią)

Instancja `OcrEngine` to główny element, który skanuje obrazy i zwraca tekst. Myśl o niej jak o mózgu interpretującym wzorce pikseli.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Wskazówka:** Możesz dostosować język, progi pewności lub nawet włączyć przyspieszenie GPU poprzez właściwości silnika. Dla większości angielskich PDF‑ów domyślne ustawienia są wystarczające.

## Krok 3 – Przygotuj wejście: dodaj swój PDF (Konwersja PDF na obrazy w tle)

Aspose.OCR traktuje każdą stronę PDF jako obraz. Gdy wywołujesz `addPdf`, biblioteka cicho rasteryzuje każdą stronę – dokładnie to, czego potrzebujesz, aby **przekonwertować PDF na obrazy** przed rozpoznaniem.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Co się dzieje:**  
- PDF zostaje otwarty.  
- Każda strona jest renderowana w 300 dpi (wartość domyślna), aby zachować szczegóły znaków.  
- Renderowane obiekty bitmap są przechowywane w kolekcji `OcrInput`.

Jeśli kiedykolwiek potrzebujesz surowych obrazów (do debugowania lub własnego przetwarzania), wywołaj `ocrInput.getPages()` po tym kroku.

## Krok 4 – Uruchom proces OCR (Wykonaj OCR na PDF)

Teraz zaczyna się ciężka praca. Metoda `recognize` iteruje po każdym obrazie, uruchamia algorytm rozpoznawania i zbiera wyniki w obiekcie `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Dlaczego to istotne:** `OcrResult` zawiera nie tylko czysty tekst, ale także wyniki pewności, ramki ograniczające i odniesienie do oryginalnego obrazu. W większości przypadków wystarczy metoda `getText()`.

## Krok 5 – Pobierz i wyświetl wyodrębniony tekst

Na koniec wyciągnij ciąg znaków z wyniku i wypisz go. Możesz także zapisać go do pliku, przekazać do indeksu wyszukiwania lub użyć w kolejnej fazie przetwarzania NLP.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Oczekiwany wynik

Jeśli `scanned-report.pdf` zawiera prosty akapit, zobaczysz coś w stylu:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Dokładne formatowanie odzwierciedla oryginalny układ, zachowując podziały linii tam, gdzie to możliwe.

## Obsługa typowych przypadków brzegowych

### 1. PDF‑y wielojęzyczne

Jeśli dokument zawiera tekst po francusku lub hiszpańsku, ustaw język przed wywołaniem `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Możesz podać tablicę języków, aby silnik automatycznie wykrywał język.

### 2. Skanowanie o niskiej rozdzielczości

Przy skanach 150 dpi zwiększ wewnętrzne DPI renderowania:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

Wyższe DPI poprawia czytelność znaków, ale zużywa więcej pamięci.

### 3. Duże PDF‑y (zarządzanie pamięcią)

W przypadku PDF‑ów z dziesiątkami stron przetwarzaj je partiami:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Takie podejście zapobiega nadmiernemu wzrostowi sterty JVM.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program – łącznie z importami i obsługą licencji – gotowy do skopiowania i natychmiastowego uruchomienia.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Uruchom go za pomocą:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Powinieneś zobaczyć wyodrębniony tekst wypisany w konsoli.

## Podsumowanie – co omówiliśmy

- **Jak używać OCR** w Javie z Aspose.OCR.  
- Przebieg pracy **wyodrębniania tekstu z PDF**.  
- Wewnątrz biblioteka **konwertuje PDF na obrazy** przed rozpoznaniem znaków.  
- Wskazówki dotyczące **przeprowadzania OCR na PDF** z wieloma językami, niską rozdzielczością i dużymi dokumentami.  
- Kompletny, uruchamialny fragment kodu, który możesz wstawić do dowolnego projektu Javy.

## Kolejne kroki i powiązane tematy

Teraz, gdy potrafisz **rozpoznać zeskanowany PDF**, rozważ następujące pomysły:

- **Generowanie przeszukiwalnego PDF** – nałóż tekst OCR z powrotem na oryginalny PDF, tworząc dokument przeszukiwalny.  
- **Usługa przetwarzania wsadowego** – opakuj kod w mikroserwis Spring Boot, który przyjmuje PDF‑y przez REST.  
- **Integracja z Elasticsearch** – indeksuj wyodrębniony tekst, aby uzyskać szybkie wyszukiwanie pełnotekstowe w repozytorium dokumentów.  
- **Wstępne przetwarzanie obrazu** – użyj OpenCV do prostowania lub odszumiania stron przed OCR, aby uzyskać jeszcze wyższą dokładność.

Każdy z tych tematów bazuje na podstawowych koncepcjach, które omówiliśmy, więc śmiało eksperymentuj i pozwól silnikowi OCR wykonać ciężką pracę.

---

*Miłego kodowania! Jeśli napotkasz problemy – np. błędy licencji lub nieoczekiwane wyniki null – zostaw komentarz poniżej. Chętnie pomogę w debugowaniu.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}