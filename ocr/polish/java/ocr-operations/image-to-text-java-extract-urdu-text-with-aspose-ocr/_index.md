---
category: general
date: 2026-02-17
description: 'samouczek Java: obraz na tekst – dowiedz się, jak wyodrębnić tekst w
  języku urdu z obrazu przy użyciu Aspose OCR. Dołączony kompletny przykład OCR w
  Javie.'
draft: false
keywords:
- image to text java
- how to extract text
- extract urdu text
- java ocr example
- load image ocr
language: pl
og_description: Poradnik Java konwertujący obraz na tekst pokazuje, jak wyodrębnić
  tekst w języku urdu z obrazu przy użyciu Aspose OCR. Postępuj zgodnie z kompletnym
  przykładem Java OCR krok po kroku.
og_title: 'Obraz na tekst Java: wyodrębnij tekst urdu przy użyciu Aspose OCR'
tags:
- OCR
- Java
- Aspose
title: 'z obrazu na tekst java: wyodrębnij tekst urdu przy użyciu Aspose OCR'
url: /pl/java/ocr-operations/image-to-text-java-extract-urdu-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image to text java: Wyodrębnij tekst w języku Urdu przy użyciu Aspose OCR

Jeśli potrzebujesz konwersji **image to text java** dla dokumentów w języku Urdu, jesteś we właściwym miejscu. Zastanawiałeś się kiedyś *jak wyodrębnić tekst* z obrazu odręcznej notatki lub zeskanowanej strony gazety? Ten przewodnik poprowadzi Cię przez **java ocr example**, które wyciąga znaki Urdu bezpośrednio z obrazu przy użyciu Aspose OCR.

Omówimy wszystko, od licencjonowania biblioteki po wyświetlenie wyniku w konsoli. Po zakończeniu będziesz w stanie **load image ocr** pliki, ustawić język na Urdu i uzyskać czysty output Unicode — bez dodatkowych narzędzi.  

## Co będzie potrzebne

- **Java Development Kit (JDK) 8+** – kod działa na dowolnym nowoczesnym JDK.
- **Aspose.OCR for Java** JAR (pobierz ze strony Aspose).  
- Ważny plik licencji **Aspose OCR** (`Aspose.OCR.lic`).  
- Obraz zawierający tekst w języku Urdu, np. `urdu-sample.png`.  

Posiadanie tych podstaw pozwala od razu przejść do kodu, bez konieczności szukania brakujących zależności.

## image to text java – Konfiguracja Aspose OCR

Najpierw musimy poinformować Aspose, że posiadamy licencję. Bez niej biblioteka działa w trybie ewaluacyjnym i doda znak wodny do wyniku.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Dlaczego to ważne:** Licencjonowanie usuwa 5‑sekundowy limit przetwarzania i odblokowuje pełny pakiet języka Urdu, który został dodany w Q3 2025. Jeśli pominiesz ten krok, silnik OCR nadal będzie działał, ale w wynikach pojawi się mały znacznik „Evaluation”.

## Jak wyodrębnić tekst – Inicjalizacja silnika OCR

Teraz tworzymy silnik i wyraźnie informujemy go, że interesuje nas język Urdu. Stała `OcrLanguage.URDU` aktywuje odpowiedni zestaw znaków i reguły segmentacji.

```java
        // Step 2: Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3
```

**Wskazówka:** Jeśli kiedykolwiek będziesz musiał przetwarzać wiele języków w jednym uruchomieniu, możesz przekazać listę oddzieloną przecinkami, np. `OcrLanguage.ENGLISH, OcrLanguage.URDU`. Silnik automatycznie wykryje każdy region.

## Ładowanie obrazu OCR – Przygotowanie danych wejściowych

Aspose pracuje z obiektem `OcrInput`, który może przechowywać jeden lub wiele obrazów. Tutaj **load image ocr** dane z lokalnego pliku.

```java
        // Step 3: Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");
```

> **Uwaga:** Zastąp `YOUR_DIRECTORY` ścieżką bezwzględną lub względną względem katalogu głównego projektu. Jeśli plik nie zostanie znaleziony, Aspose rzuci `FileNotFoundException`. Szybka weryfikacja przy pomocy `new File(path).exists()` może zaoszczędzić wiele czasu debugowania.

## Rozpoznawanie tekstu – Uruchamianie procesu OCR

Po skonfigurowaniu silnika i załadowaniu obrazu, w końcu wywołujemy `recognize`. Metoda zwraca `OcrResult`, który zawiera wyodrębniony ciąg znaków.

```java
        // Step 4: Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Co się dzieje pod maską?** Silnik OCR dzieli obraz na linie, a następnie na znaki, stosując specyficzne dla Urdu reguły kształtowania (np. łączenie form). Dlatego ustawienie języka na początku jest kluczowe; w przeciwnym razie otrzymasz zniekształcone zastępniki łacińskie.

## Drukowanie rozpoznanego tekstu w języku Urdu

Ostatnim krokiem jest po prostu wydrukowanie wyniku. Ponieważ Urdu używa skryptu od prawej do lewej, upewnij się, że Twoja konsola obsługuje Unicode (większość nowoczesnych terminali tak robi).

```java
        // Step 5: Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

**Oczekiwany wynik (przykład):**

```
Urdu text:
یہ ایک مثال کا متن ہے جو تصویر سے نکالا گیا ہے۔
```

Jeśli widzisz znaki zapytania lub puste ciągi, sprawdź, czy kodowanie konsoli jest ustawione na UTF‑8 (`chcp 65001` w Windows lub uruchom Java z `-Dfile.encoding=UTF-8`).

## Pełny działający przykład – Wszystkie kroki w jednym miejscu

Poniżej znajduje się kompletny, gotowy do skopiowania program. Bez zewnętrznych odwołań, tylko pojedynczy plik Java.

```java
import com.aspose.ocr.*;

public class UrduDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Create the OCR engine and set the language to Urdu
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU); // added in 2025‑Q3

        // Load the image that contains Urdu text
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/urdu-sample.png");

        // Recognize the text from the image
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Print the recognized Urdu text
        System.out.println("Urdu text:\n" + ocrResult.getText());
    }
}
```

Uruchom go za pomocą:

```bash
javac -cp "aspose-ocr-23.10.jar" UrduDemo.java
java -cp ".:aspose-ocr-23.10.jar" UrduDemo
```

Zastąp wersję JAR (`23.10`) tą, którą pobrałeś. Konsola powinna wyświetlić zdanie w języku Urdu wyodrębnione z Twojego pliku PNG.

## Częste pułapki i przypadki brzegowe

| Problem | Dlaczego się pojawia | Jak naprawić |
|-------|----------------|------------|
| **Empty output** | Obraz jest zbyt ciemny lub ma niską rozdzielczość. | Wstępnie przetwórz obraz (zwiększ kontrast, binaryzuj) używając `BufferedImage` przed przekazaniem go do Aspose. |
| **Garbage characters** | Ustawiono niewłaściwy język (domyślnie English). | Upewnij się, że wywołano `ocrEngine.getLanguage().setLanguage(OcrLanguage.URDU);` przed `recognize`. |
| **License not found** | Błąd w ścieżce lub brak pliku. | Użyj ścieżki bezwzględnej lub umieść plik `.lic` w classpath i wywołaj `license.setLicense("Aspose.OCR.lic");`. |
| **Out‑of‑memory on large images** | Duże pliki PNG zużywają pamięć heap. | Wywołaj `ocrEngine.setMaxImageSize(2000);` aby wewnętrznie zmniejszyć rozmiar, lub samodzielnie zmień rozmiar obrazu. |

## Rozszerzanie demo

- **Przetwarzanie wsadowe:** Iteruj po folderze, dodaj każdy plik do tego samego `OcrInput` i zbieraj wyniki w pliku CSV.  
- **Różne języki:** Zamień `OcrLanguage.URDU` na `OcrLanguage.ARABIC` lub połącz kilka języków.  
- **Zapisywanie do pliku:** Użyj `Files.write(Paths.get("output.txt"), ocrResult.getText().getBytes(StandardCharsets.UTF_8));`.  

Wszystkie te pomysły opierają się na **java ocr example**, które właśnie zbudowaliśmy, pozwalając Ci dostosować rozwiązanie do projektów w rzeczywistym świecie.

## Zakończenie

Masz teraz solidny **image to text java** przepływ pracy, który wyodrębnia znaki Urdu z obrazu przy użyciu Aspose OCR. Poradnik obejmował każdy krok — od licencjonowania i wyboru języka po ładowanie obrazu i drukowanie wyniku — więc możesz wkleić kod do dowolnego projektu Java i zobaczyć, jak działa.

Następnie spróbuj eksperymentować z większymi plikami PDF, różnymi skryptami lub nawet zintegrować krok OCR z endpointem REST w Spring Boot. Te same zasady — **how to extract text**, **load image o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}