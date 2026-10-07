---
category: general
date: 2026-01-02
description: Utwórz przeszukiwalny PDF ze zeskanowanego PDF‑a obrazu przy użyciu Aspose
  OCR. Dowiedz się, jak ustawić język OCR, osadzić warstwę tekstową w PDF i zastosować
  opcje wysokiej kompresji PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: pl
og_description: Szybko twórz przeszukiwalne PDF. Ten przewodnik pokazuje, jak przekonwertować
  zeskanowany PDF jako obraz, osadzić warstwę tekstową, ustawić język OCR i włączyć
  wysoką kompresję PDF.
og_title: Utwórz przeszukiwalny PDF za pomocą Aspose OCR – Kompletny przewodnik
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Tworzenie przeszukiwalnego PDF za pomocą Aspose OCR – Przewodnik krok po kroku
url: /pl/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie przeszukiwalnego PDF – Kompletny samouczek programistyczny

Czy kiedykolwiek potrzebowałeś **tworzyć przeszukiwalne pliki PDF** ze zeskanowanych obrazów, ale nie wiedziałeś od czego zacząć? Nie jesteś sam. W wielu procesach opartych na dokumentach, zwykły PDF zawierający tylko obrazy jest ślepą uliczką dla wyszukiwania i indeksowania.  

Dobrą wiadomością jest to, że dzięki Aspose OCR możesz **konwertować zeskanowany obraz PDF** na w pełni przeszukiwalny dokument w zaledwie kilku linijkach Javy. Ten samouczek przeprowadzi Cię przez każdy krok — inicjalizację silnika OCR, konfigurację ustawień PDF o wysokiej kompresji, osadzenie ukrytej warstwy tekstowej oraz wybór odpowiedniego języka OCR.

Po zakończeniu tego przewodnika będziesz mieć działający program, który generuje przeszukiwalny PDF, plik, który możesz bez problemu wrzucić do dowolnej wyszukiwarki lub systemu zarządzania dokumentami.

---

## Tworzenie przeszukiwalnego PDF – Przegląd

Zanim zanurkujemy w kod, wyjaśnijmy, co tak naprawdę oznacza „tworzenie przeszukiwalnego PDF”. Przeszukiwalny PDF zawiera dwie równoległe warstwy:

1. **Warstwa wizualna** – oryginalny zeskanowany obraz (lub renderowana strona).  
2. **Warstwa tekstowa** – niewidoczna, ale maszynowo odczytywalna, wyodrębniona przez OCR.

Kiedy otwierasz taki PDF w Adobe Reader i zaznaczasz tekst, w rzeczywistości interakcja odbywa się z ukrytą warstwą tekstową, a nie z obrazem. To podejście dwuwarstwowe umożliwia funkcję **embed text layer PDF**.

## Konwersja zeskanowanego obrazu PDF przy użyciu Aspose OCR

Pierwszą rzeczą, której potrzebujesz, jest zeskanowany obraz (PNG, JPEG, TIFF), który chcesz przekształcić w PDF. Aspose OCR potrafi odczytać ten obraz, wykonać OCR i przekazać wynik do generatora PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Dlaczego to działa:**  
- `setCreateSearchablePdf(true)` mówi Aspose, aby wygenerował ukrytą warstwę tekstową, spełniając wymaganie **embed text layer pdf**.  
- `setCompressionLevel(9)` wprowadza plik w zakres **high compression pdf**, zmniejszając ostateczny rozmiar bez utraty dokładności OCR.  
- Argument `RecognitionLanguage.ENGLISH` pokazuje, jak **set OCR language**; możesz go zamienić na francuski, niemiecki itp., w zależności od materiału źródłowego.

## Ustawienia PDF o wysokiej kompresji

Duże zeskanowane PDF‑y mogą szybko rozrosnąć się do setek megabajtów. Aspose oferuje prosty interfejs API kompresji działający na poziomie PDF. Metoda `setCompressionLevel` przyjmuje wartości od 0 (brak kompresji) do 9 (maksymalna kompresja).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Kilka wskazówek:

- **Używaj formatów obrazu bezstratnego** (PNG) dla skanów zawierających dużo tekstu; JPEG jest lepszy dla zdjęć.  
- **Włącz podzestaw czcionek** jeśli osadzasz własne czcionki — Aspose robi to automatycznie przy tworzeniu przeszukiwalnego PDF.  
- **Testuj rozmiar wyjściowy** po każdej zmianie; czasami kompresja poziomu 8 daje 10 % redukcję rozmiaru przy znikomej utracie jakości w porównaniu do poziomu 9.

## Osadzenie warstwy tekstowej PDF dla możliwości wyszukiwania

Jeśli pominiesz wywołanie `setCreateSearchablePdf(true)`, otrzymany plik będzie wyglądał dobrze, ale nie będziesz mógł przeszukiwać jego zawartości. Ukryta warstwa tekstowa jest tworzona poprzez mapowanie każdego rozpoznanego znaku na jego położenie na stronie.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Na co zwrócić uwagę:**  

- **Dokumenty wielojęzyczne** – może być konieczne dwukrotne uruchomienie OCR, raz dla każdego języka, a następnie połączenie warstw tekstowych.  
- **Złożone układy** (tabele, wielokolumnowe) – Aspose radzi sobie przyzwoicie, ale sprawdź wynik w przeglądarce PDF, która wyświetla ukryty tekst (np. tryb „Edit PDF” w Adobe Acrobat).

## Ustaw język OCR dla dokładnego rozpoznawania

Dokładność silnika OCR zależy od języka, którego się spodziewa. Aspose dostarcza zestaw wbudowanych języków, a także możesz dodać własne pakiety językowe.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Kiedy zmienić język:**  

- Dokumenty zawierają **skrypty nielatyniczne** (cyrylica, arabski) – przełącz na odpowiedni `RecognitionLanguage`.  
- Strony wielojęzyczne – możesz wywołać `recognizeImageAndSave` dwukrotnie, za każdym razem z innym językiem, a następnie połączyć PDF‑y.

## Uruchomienie pełnego przykładu

Poniżej znajduje się pełny, gotowy do uruchomienia program. Zamień ścieżki zastępcze na rzeczywiste lokalizacje plików, upewnij się, że plik JAR Aspose OCR znajduje się w classpath i uruchom.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Oczekiwany wynik:** Po uruchomieniu programu konsola wypisuje:

```
Searchable PDF created.
```

Otwórz `searchable.pdf` w dowolnej przeglądarce PDF, spróbuj zaznaczyć tekst i zobaczysz działanie niewidzialnej warstwy. Pomyślnie **utworzyłeś przeszukiwalny pdf** ze zeskanowanego obrazu.

![przykład tworzenia przeszukiwalnego pdf](image-placeholder.png "przykład tworzenia przeszukiwalnego pdf")

*Powyższy zrzut ekranu (placeholder) zazwyczaj pokazuje przeglądarkę PDF z możliwością zaznaczania tekstu na zeskanowanej stronie.*

## Podsumowanie

Omówiliśmy wszystko, co potrzebne do **tworzenia przeszukiwalnych plików PDF** przy użyciu Aspose OCR:

- Zainicjalizuj silnik OCR.  
- **Konwertuj zeskanowany obraz PDF** podając PNG/JPEG do `recognizeImageAndSave`.  
- Użyj `setCreateSearchablePdf(true)`, aby **embed text layer PDF**.  
- Zastosuj `setCompressionLevel(9)` dla **high compression PDF**, który pozostaje lekki.  
- Wybierz odpowiedni `RecognitionLanguage`, aby **set OCR language** dla maksymalnej dokładności.

Od tego momentu możesz eksperymentować z przetwarzaniem wsadowym, różnymi językami lub nawet połączyć wiele zeskanowanych stron w jeden przeszukiwalny PDF. Ten sam schemat działa dla innych języków, takich jak hiszpański czy japoński — wystarczy zamienić enum `RecognitionLanguage`.

Śmiało zostaw komentarz, jeśli napotkasz problemy, i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}