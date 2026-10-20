---
category: general
date: 2026-03-28
description: Wykonaj OCR obrazu w Javie przy użyciu Aspose OCR, aby przekształcić
  obraz w tekst, szybko i niezawodnie wyodrębnić tajski tekst z pliku PNG.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: pl
og_description: Wykonaj OCR na obrazie przy użyciu Javy i Aspose OCR. Dowiedz się,
  jak konwertować obraz na tekst, wyodrębniać tajski tekst z PNG i radzić sobie z
  typowymi pułapkami.
og_title: Uruchom OCR na obrazie w Javie – Szybko wyodrębnij tajski tekst
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Uruchom OCR na obrazie w Javie – wyodrębnij tajski tekst z PNG
url: /pl/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchom OCR na obrazie w Javie – Pełny poradnik

Zastanawiałeś się kiedyś, jak **uruchomić OCR na obrazie** bezpośrednio z kodu Java? Być może masz kolekcję tajskich paragonów, zeskanowanych dokumentów lub zrzutów ekranu i potrzebujesz tekstu bez ręcznego przepisywania. To częsty problem, zwłaszcza gdy źródłem jest PNG, a język nie‑łaciński.  

W tym przewodniku pokażemy dokładnie, jak **uruchomić OCR na obrazie** przy użyciu biblioteki Aspose OCR, przekształcić obraz w zwykły tekst i niezawodnie wyodrębnić tajskie znaki. Po zakończeniu będziesz w stanie **konwertować obraz na tekst**, **wyodrębniać tekst z PNG** i nawet **rozpoznawać tajski tekst** za pomocą kilku linii kodu.

## Co obejmuje ten poradnik

* Dodanie zależności Aspose OCR do projektu Maven/Gradle.  
* Inicjalizacja `OcrEngine` i skonfigurowanie go pod język tajski.  
* Uruchomienie OCR na pliku PNG oraz obsługa ewentualnych błędów.  
* Wyświetlenie wyniku w konsoli i weryfikacja wyjścia.  

Wcześniejsze doświadczenie z Aspose nie jest wymagane — wystarczy podstawowe IDE Java oraz plik obrazu, który chcesz przetworzyć.

## Wymagania wstępne

* Java 8 lub nowsza (biblioteka działa również z Java 11+).  
* Narzędzie do budowania — Maven lub Gradle (pokażemy fragment Maven).  
* Licencja Aspose OCR (bezpłatna wersja próbna wystarczy do testów, ale licencja usuwa ograniczenia wersji ewaluacyjnej).  
* PNG zawierający tekst tajski, np. `input.png` umieszczony w folderze zasobów projektu.

---

## Krok 1: Dodaj Aspose OCR do projektu

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Wskazówka:** Utrzymuj wersję biblioteki zgodną z oficjalnymi notatkami wydania Aspose; nowsze wersje dodają pakiety językowe i usprawnienia wydajności.

Po rozwiązaniu zależności IDE powinno automatycznie zaimportować wymagane klasy.

## Krok 2: Zainicjalizuj silnik OCR

Silnik jest sercem procesu – można go porównać do „mózgu”, który analizuje wzorce pikseli. Dodatkowo poinformujemy go, że interesują nas wyłącznie znaki tajskie.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Dlaczego ustawiamy język explicite? Ponieważ podanie `"th"` zawęża zestaw znaków, co przyspiesza rozpoznawanie i zmniejsza liczbę pomyłek w rozpoznawaniu podobnie wyglądających glifów.

## Krok 3: Uruchom OCR na pliku PNG

Teraz przekazujemy silnikowi obraz, który chcemy zdekodować. Metoda `recognizeImage` zwraca obiekt `OcrResult`, zawierający wyodrębniony ciąg znaków oraz oceny pewności.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Jeśli plik nie zostanie znaleziony, Aspose rzuca `FileNotFoundException`. Warto otoczyć wywołanie blokiem `try‑catch` w kodzie produkcyjnym, ale w tym poradniku pozostaniemy przy prostym podejściu.

## Krok 4: Wyświetl rozpoznany tekst

Na koniec wypisujemy wynik. Metoda `getText()` zwraca zwykły `String` w Javie, który możesz zapisać, przesłać przez sieć lub zapisać do pliku.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Po uruchomieniu programu powinieneś zobaczyć coś podobnego do:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Jeśli wyjście jest nieczytelne, sprawdź, czy źródłowy PNG ma wysoką rozdzielczość (co najmniej 300 dpi) oraz czy kod języka `"th"` odpowiada docelowemu językowi.

### Pełny listing

Poniżej znajduje się kompletny, gotowy do uruchomienia plik Java. Skopiuj go do swojego IDE, ewentualnie zmień ścieżkę do obrazu i naciśnij **Run**.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![przykład uruchomienia OCR na obrazie](image.png "przykład uruchomienia OCR na obrazie – kod Java wyodrębniający tajski tekst z PNG")

## Krok 5: Typowe warianty i przypadki brzegowe

### Konwersja obrazu na tekst w innych formatach

Jeśli potrzebujesz **konwertować obraz na tekst** dla JPEG lub BMP, po prostu zmień rozszerzenie w `imagePath`. Aspose OCR obsługuje PNG, JPEG, BMP, TIFF oraz nawet strony PDF.

### Wyodrębnianie tekstu z PNG w wielu językach

Możesz poprosić silnik o wykrycie kilku języków jednocześnie:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Wynik będzie zawierał mieszankę znaków tajskich i angielskich, co jest przydatne przy dwujęzycznych paragonach.

### Obsługa niskiej jakości obrazów

W przypadku rozmytych skanów rozważ włączenie wstępnego przetwarzania:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Spowoduje to uruchomienie wbudowanych algorytmów odszumiania i zwiększania kontrastu, poprawiając krok **wyodrębniać tekst z PNG**.

### Aktywacja licencji

Bez licencji Aspose wstawia linię znaku wodnego w wyniku po przetworzeniu 100 stron. Aktywuj licencję jak najwcześniej:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

Umieść plik `.lic` obok swojego JAR‑a lub odwołaj się do niego za pomocą ścieżki bezwzględnej.

## Najczęściej zadawane pytania

**P: Czy to działa na Linuksie?**  
O: Zdecydowanie tak. Aspose OCR jest czystą Javą, więc każdy system operacyjny kompatybilny z JVM jest w porządku.

**P: Co jeśli PNG zawiera odręczny tajski tekst?**  
O: Rozpoznawanie odręcznego pisma jest ograniczone; może być potrzebny dedykowany model sieci neuronowej. Aspose OCR radzi sobie świetnie z drukowanym tekstem.

**P: Czy mogę przetwarzać wsadowo folder obrazów?**  
O: Owiń wywołanie `recognizeImage` w pętlę po `Files.list(Paths.get("folder"))`. Pamiętaj, aby ponownie używać tej samej instancji `OcrEngine` dla lepszej wydajności.

## Podsumowanie

Przeszliśmy przez kompletny, end‑to‑end przykład, jak **uruchomić OCR na obrazie** w Javie, konkretnie aby **wyodrębnić tajski tekst** z PNG. Inicjalizując `OcrEngine`, ustawiając język, wywołując `recognizeImage` i wypisując wynik, masz teraz niezawodny sposób na **konwertowanie obrazu na tekst** bez korzystania z usług zewnętrznych.

Od tego momentu możesz:

* **wyodrębniać tekst z PNG** masowo w projektach data‑miningowych.  
* Połączyć wynik OCR z API tłumaczeniowym, aby uzyskać angielskie odpowiedniki.  
* Eksplorować inne języki wspierane przez Aspose, takie jak chiński czy arabski, zmieniając kod języka.

Wypróbuj to na własnych obrazach — dostosuj ustawienia wstępnego przetwarzania, eksperymentuj z różnymi formatami plików i zobacz, jak solidne jest rozwiązanie w Twoim rzeczywistym przepływie pracy.

Miłego kodowania i niech Twoje potoki OCR będą zawsze precyzyjne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}