---
category: general
date: 2026-02-22
description: Dowiedz się, jak włączyć GPU w Java OCR, aby rozpoznawać tekst z obrazu
  i szybko wyodrębniać tekst z faktury przy użyciu Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: pl
og_description: Jak włączyć GPU w Java OCR, rozpoznawać tekst z obrazu i wyodrębniać
  tekst z faktury w kompletnym przykładzie Java OCR.
og_title: Jak włączyć GPU dla Java OCR – szybki przewodnik
tags:
- Java
- OCR
- GPU
- Aspose
title: Jak włączyć GPU w Java OCR – rozpoznawanie tekstu z obrazu
url: /pl/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU dla Java OCR – Rozpoznawanie tekstu z obrazu

Zastanawiałeś się kiedyś **jak włączyć GPU** przy wykonywaniu OCR w Javie? Nie jesteś sam — wielu programistów napotyka na ograniczenia wydajności przy przetwarzaniu dużych, wysokiej rozdzielczości dokumentów, takich jak faktury. Dobra wiadomość? Dzięki Aspose OCR możesz przełączyć jedną opcję i pozwolić karcie graficznej wykonać ciężką pracę. W tym poradniku przeprowadzimy **przykład java ocr**, który wczytuje obraz, włącza przetwarzanie GPU i w mgnieniu oka wyodrębnia tekst z faktury.

Omówimy wszystko, od instalacji biblioteki po obsługę przypadków brzegowych, takich jak brak sterowników GPU. Po zakończeniu będziesz w stanie **rozpoznawać tekst z obrazu** w locie i będziesz mieć solidny szablon do przyszłych projektów OCR. Nie są potrzebne żadne zewnętrzne odwołania — tylko czysty, działający kod.

## Prerequisites

- **Java Development Kit (JDK) 11** lub nowszy zainstalowany na twoim komputerze.  
- **Maven** (lub Gradle) do zarządzania zależnościami.  
- System **z obsługą GPU** z aktualnymi sterownikami (NVIDIA, AMD lub Intel).  
- Plik obrazu faktury (np. `large_invoice_300dpi.png`).  

Jeśli czegoś brakuje, najpierw to załatw; dalsza część poradnika zakłada, że wszystko jest gotowe.

## Krok 1: Dodaj Aspose OCR do swojego projektu

Pierwszą rzeczą, której potrzebujemy, jest biblioteka Aspose OCR. Z Mavenem po prostu wstaw poniższy fragment do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Porada:** Numer wersji zmienia się regularnie; sprawdź Maven Central, aby uzyskać najnowsze wydanie.

Jeśli wolisz Gradle, odpowiednik wygląda tak:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Gdy zależność zostanie rozwiązana, możesz napisać kod, który komunikuje się z silnikiem OCR.

## Krok 2: Jak włączyć GPU w silniku Aspose OCR

Teraz przychodzi gwiazda programu — włączenie przetwarzania GPU. Aspose OCR oferuje trzy tryby przetwarzania:

| Mode | Description |
|------|-------------|
| `CPU_ONLY` | Tylko CPU, bezpieczne dla każdego komputera. |
| `GPU_ONLY` | Wymusza GPU, niepowodzenie, jeśli brak kompatybilnego urządzenia. |
| `AUTO_GPU` | Wykrywa GPU i używa go, gdy jest dostępny, w przeciwnym razie przełącza się na CPU. |

W większości scenariuszy zalecamy **`AUTO_GPU`**, ponieważ daje najlepsze z obu światów. Oto jak to włączyć:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Dlaczego to ważne:** Włączenie GPU może skrócić czas przetwarzania faktury 300 dpi z kilku sekund do poniżej sekundy, w zależności od sprzętu.

## Krok 3: Wczytaj obraz do OCR – Rozpoznaj tekst z obrazu

Zanim silnik będzie mógł coś odczytać, musisz dostarczyć mu obraz. Klasa `OcrInput` z Aspose OCR akceptuje ścieżki plików, strumienie lub nawet obiekty `BufferedImage`. Dla prostoty użyjemy ścieżki pliku:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Przypadek brzegowy:** Jeśli obraz jest większy niż 5 MB, rozważ najpierw jego zmniejszenie, aby uniknąć błędów braku pamięci na GPU.

## Krok 4: Wykonaj OCR i wyodrębnij tekst z faktury

Teraz prosimy silnik o wykonanie magii. Metoda `recognize` zwraca obiekt `OcrResult`, który zawiera wyodrębniony tekst, wyniki pewności i informacje o układzie.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Po uruchomieniu programu powinieneś zobaczyć coś podobnego do:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Jeśli wynik wygląda na zniekształcony, sprawdź dwukrotnie, czy obraz jest wyraźny i czy język OCR jest ustawiony poprawnie (Aspose domyślnie używa angielskiego, ale możesz go zmienić za pomocą `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` itd.).

## Krok 5: Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się kompletny, samodzielny klas Java. Wklej go do swojego IDE, dostosuj ścieżkę obrazu i naciśnij **Run**.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Oczekiwany wynik

Uruchomienie kodu na wyraźnej fakturze 300 dpi zazwyczaj daje tekstową reprezentację każdej linii dokumentu. Dokładny wynik zależy od układu faktury, ale zobaczysz pola takie jak *Invoice Number*, *Date*, *Total Amount* oraz opisy pozycji.

## Częste problemy i jak je naprawić

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError`** | Brak sterownika GPU lub niekompatybilny | Zainstaluj najnowszy sterownik od NVIDIA/AMD/Intel. |
| **Bardzo wolne przetwarzanie** | GPU cicho przełącza się na CPU | Sprawdź, czy `ocrEngine.getProcessingMode()` zwraca `AUTO_GPU` oraz czy `SystemInfo.isGpuAvailable()` jest prawdziwe. |
| **Pusty wynik** | Obraz zbyt ciemny lub o niskim kontraście | Wstępnie przetwórz obraz (zwiększ kontrast, binaryzuj) przed przekazaniem go do OCR. |
| **Brak pamięci** | Bardzo duży obraz (>10 MP) | Zmień rozmiar lub podziel obraz na kafelki; przetwarzaj każdy kafelek osobno. |

## Podsumowanie krok po kroku (szybka referencja)

| Step | Co zrobiłeś |
|------|--------------|
| 1 | Dodano zależność Aspose OCR |
| 2 | Utworzono `OcrEngine` i ustawiono `AUTO_GPU` |
| 3 | Wczytano obraz faktury za pomocą `OcrInput` |
| 4 | Wywołano `recognize` i wydrukowano `ocrResult.getText()` |
| 5 | Obsłużono typowe błędy i zweryfikowano wynik |

## Co dalej – kolejne kroki

- **Przetwarzanie wsadowe:** Przejdź przez folder faktur i zapisz każdy wynik w bazie danych.  
- **Obsługa języków:** Zmien `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` dla wielojęzycznych faktur.  
- **Post‑processing:** Użyj wyrażeń regularnych, aby wyodrębnić pola takie jak *Invoice Number* lub *Total Amount* z surowego tekstu.  
- **Dostrajanie GPU:** Jeśli masz wiele GPU, sprawdź `ocrEngine.setGpuDeviceId(int id)`, aby wybrać najszybsze.

## Zakończenie

Pokazaliśmy **jak włączyć GPU** dla Java OCR, przedstawiliśmy czysty **przykład java ocr** i przeprowadziliśmy przez cały proces od **wczytania obrazu do OCR** po **wyodrębnienie tekstu z faktury**. Korzystając z trybu `AUTO_GPU` Aspose uzyskujesz przyspieszenie wydajności bez utraty kompatybilności — idealne zarówno dla maszyn deweloperskich, jak i serwerów produkcyjnych.

Wypróbuj to, dostosuj wstępne przetwarzanie obrazu i eksperymentuj z zadaniami wsadowymi. Nie ma granic, gdy połączysz przyspieszenie GPU z solidną biblioteką OCR.

---

![Diagram przedstawiający pipeline OCR przyspieszonego GPU – jak włączyć GPU dla Java OCR](https://example.com/images/gpu-ocr-pipeline.png "jak włączyć gpu dla Java OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}