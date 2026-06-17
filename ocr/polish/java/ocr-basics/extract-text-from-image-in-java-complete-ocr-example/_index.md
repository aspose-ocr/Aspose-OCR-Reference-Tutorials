---
category: general
date: 2026-02-19
description: Wyodrębnij tekst z obrazu przy użyciu Java OCR. Poznaj przykład Java
  OCR, który ładuje obraz do OCR i wyodrębnia tekst z plików faktur w kilku prostych
  krokach.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: pl
og_description: Wyodrębnij tekst z obrazu przy użyciu Java OCR. Ten przewodnik pokazuje,
  jak załadować obraz do OCR i pobrać tekst z faktur przy użyciu prostego przykładu
  Java OCR.
og_title: Wyodrębnianie tekstu z obrazu w Javie – kompletny przykład OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Wyodrębnianie tekstu z obrazu w Javie – kompletny przykład OCR
url: /pl/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyodrębnianie tekstu z obrazu w Javie – kompletny przykład OCR

Kiedykolwiek potrzebowałeś **wyodrębnić tekst z obrazu**, ale nie wiedziałeś, którą bibliotekę wybrać? Nie jesteś sam — wielu programistów napotyka ten problem przy automatyzacji przetwarzania faktur lub budowaniu przeszukiwalnych archiwów. Dobra wiadomość? Kilka linijek Javy wystarczy, aby wczytać obraz do OCR, określić obszar zainteresowania i pobrać dokładnie ten tekst, którego potrzebujesz.  

W tym tutorialu przejdziemy przez **przykład java ocr**, który pokazuje, jak **wczytać obraz do OCR**, ustawić ROI i **wyodrębnić tekst z faktur** przy użyciu Aspose.OCR. Po zakończeniu będziesz mieć działający program, który możesz wstawić do dowolnego projektu Java.

## Czego się nauczysz

- Jak utworzyć instancję `OcrEngine` i dlaczego jest to ważne.  
- Prawidłowy sposób **wczytania obrazu do OCR** przy użyciu `ImageStream` Aspose.  
- Ustawianie **obszaru zainteresowania (ROI)**, aby przetwarzać tylko część obrazu zawierającą kwotę faktury.  
- Wyodrębnianie rozpoznanego tekstu i wyświetlanie go w konsoli.  
- Typowe pułapki (np. nieprawidłowe współrzędne prostokąta) oraz szybkie rozwiązania.

**Wymagania wstępne**

- Java 8 lub nowsza.  
- Maven lub Gradle do pobrania biblioteki Aspose.OCR (`com.aspose:aspose-ocr`).  
- Przykładowy obraz faktury (`invoice.png`) umieszczony w znanym katalogu.

Masz wszystko? Świetnie — zanurzmy się.

![Wyodrębnianie tekstu z obrazu przy użyciu Java OCR](/images/extract-text-from-image-java.png "przykład wyodrębniania tekstu z obrazu")

## Wyodrębnianie tekstu z obrazu – krok po kroku przykład Java OCR

Poniżej pełny kod źródłowy. Skopiuj‑wklej go do pliku `RoiOcrExample.java` i uruchom od razu.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Dlaczego każdy krok jest ważny

1. **Tworzenie silnika OCR** – bez silnika nie ma kontekstu dla przetwarzania obrazu. Obiekt pozwala także później dostosować pakiety językowe, jeśli potrzebujesz obsługi wielu języków.  
2. **Wczytywanie obrazu** – `ImageStream.fromFile` ukrywa szczegóły formatu pliku, zapewniając, że silnik odczyta bajty poprawnie. Pominięcie tego spowoduje `NullPointerException`.  
3. **Ustawianie ROI** – przetwarzanie całej strony może być nieefektywne. Ograniczając prostokąt do obszaru z sumą faktury, przyspieszasz rozpoznawanie i redukujesz szumy.  
4. **Wywołanie `recognize()`** – tutaj dzieje się magia. Metoda uruchamia algorytm OCR na ROI i zwraca obiekt wyniku.  
5. **Wyświetlanie wyniku** – w prawdziwych projektach prawdopodobnie zapiszesz tekst w bazie danych, ale `System.out.println` jest idealny do szybkiej demonstracji.

## Wczytywanie obrazu do OCR

Jeśli zastanawiasz się, czy ścieżka ma być bezwzględna czy względna, odpowiedź brzmi: oba rozwiązania działają — ważne, aby proces Java mógł odczytać plik. W systemie Windows odwrotny ukośnik trzeba podwoić (`C:\\images\\invoice.png`) lub użyć ukośników (`C:/images/invoice.png`).  

**Wskazówka:** Jeśli przetwarzasz wiele faktur w pętli, używaj tej samej instancji `OcrEngine`; buforuje ona zasoby wewnętrzne i zwiększa wydajność.

## Definiowanie obszaru zainteresowania (ROI)

Dobór odpowiedniego prostokąta może wymagać kilku prób. Wygodny sposób na uzyskanie współrzędnych to otworzyć obraz w dowolnym edytorze graficznym (np. GIMP lub Paint.NET) i najechać kursorem na interesujący obszar — wartości X/Y pojawią się na pasku statusu.  

Przypadek brzegowy: niektóre faktury mają zmienny układ. W takiej sytuacji możesz najpierw wykonać szybkie skanowanie całego obrazu, znaleźć słowa kluczowe takie jak „Total:” przy pomocy wyrażenia regularnego, a następnie dynamicznie dopasować ROI.

## Wykonanie OCR i pobranie tekstu

Wywołanie `recognize()` jest synchroniczne — wątek blokuje się, dopóki silnik nie zakończy pracy. Przy dużych partiach warto uruchomić pulę wątków i przetwarzać obrazy równolegle. Pamiętaj, że każdy wątek potrzebuje własnej instancji `OcrEngine`; nie są one bezpieczne wątkowo.

## Uruchomienie i weryfikacja wyniku

Kompiluj i uruchom:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Powinieneś zobaczyć coś w stylu:

```
ROI text: $1,254.00
```

Jeśli wynik jest nieczytelny, sprawdź ponownie współrzędne ROI i upewnij się, że jakość obrazu jest wysoka (300 dpi lub więcej daje najlepsze rezultaty).  

### Typowe problemy i ich rozwiązania

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| Pusty ciąg | ROI poza granicami obrazu | Zweryfikuj wartości prostokąta względem wymiarów obrazu |
| Błędne słowa | Niska rozdzielczość | Użyj obrazu o wyższej rozdzielczości lub zastosuj wstępne przetwarzanie (np. binaryzację) |
| `java.lang.NoClassDefFoundError` | Brak JAR‑a Aspose w classpath | Dodaj `aspose-ocr.jar` do `-cp` lub użyj zarządzania zależnościami Maven/Gradle |

## Podsumowanie

Teraz wiesz, jak **wyodrębnić tekst z obrazu** w Javie, korzystając z zwięzłego **przykładu java ocr**. Poprzez prawidłowe wczytanie obrazu, zdefiniowanie skoncentrowanego ROI i wywołanie `recognize()`, możesz niezawodnie **wyodrębniać tekst z faktur** i przekazywać te dane do dalszych systemów.

Co dalej? Spróbuj zmienić ROI na inne pola (data, nazwa dostawcy), poeksperymentuj z pakietami językowymi dla wielojęzycznych faktur lub zintegrować krok OCR z mikrousługą Spring Boot. Ten sam wzorzec sprawdzi się przy paragonach, paszportach czy każdym dokumencie, w którym potrzebne jest precyzyjne wyodrębnianie tekstu.

Masz pytania dotyczące skalowania tego rozwiązania lub obsługi zaszumionych skanów? zostaw komentarz poniżej — powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}