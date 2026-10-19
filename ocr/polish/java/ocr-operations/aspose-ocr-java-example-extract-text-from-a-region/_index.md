---
category: general
date: 2026-05-03
description: Przykład Aspose OCR Java pokazuje, jak wczytać obraz do OCR i wyodrębnić
  tekst z regionu w zaledwie kilku linijkach kodu.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: pl
og_description: Przykład Aspose OCR w Javie demonstruje ładowanie obrazu do OCR oraz
  wyodrębnianie tekstu z określonego regionu, co jest idealne do przetwarzania faktur.
og_title: Przykład Aspose OCR w Javie – Ekstrakcja tekstu z regionu
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Przykład Aspose OCR w Javie: Wyodrębnianie tekstu z obszaru'
url: /pl/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przykład Aspose OCR Java: Wyodrębnianie tekstu z regionu

Szukasz **przykładu Aspose OCR Java**, który pozwala pobrać tylko potrzebną część obrazu? W tym przewodniku przeprowadzimy Cię przez **ładowanie obrazu do OCR** oraz **wyodrębnianie tekstu z regionu**, co jest idealne dla numerów faktur, pól formularzy lub dowolnych danych ukrytych w większym obrazie.

Możesz się zastanawiać, dlaczego warto ograniczyć OCR do prostokąta zamiast skanować całą stronę. Krótkie wyjaśnienie: szybkość i precyzja. Gdy silnik analizuje tylko określony fragment, pomija nieistotny szum, działa szybciej i często daje czystsze wyniki. Po zakończeniu tego samouczka będziesz mieć samodzielny program w Javie, który robi dokładnie to, a także kilka wskazówek, jak uniknąć typowych pułapek, które napotykają nowicjusze.

## Czego będziesz potrzebować

- **Java Development Kit (JDK) 11** lub nowszy, zainstalowany.
- Biblioteka **Aspose.OCR for Java** (możesz pobrać najnowszy JAR z repozytorium Maven Central lub portalu pobierania Aspose).
- Plik obrazu zawierający tekst, który chcesz odczytać – w naszym demo użyjemy `invoice.png`, który zawiera numer faktury w pobliżu prawego górnego rogu.
- Ulubione IDE lub prosty edytor tekstu wraz z terminalem; dowolne narzędzie budujące (Maven, Gradle lub zwykły `javac`) wystarczy.

To wszystko. Bez dodatkowych silników OCR, bez natywnych binarek, tylko czysta Java i Aspose.

![Zrzut ekranu przykładu Aspose OCR Java](/images/aspose-ocr-java-example.png "Przykład Aspose OCR Java pokazujący wyodrębnianie regionu")

## Przykład Aspose OCR Java – Inicjalizacja silnika OCR

Pierwszą rzeczą, której potrzebuje każdy przepływ pracy OCR, jest instancja silnika. Aspose udostępnia lekką klasę `OcrEngine`, która obsługuje wszystko, od ładowania obrazu po wybór języka.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Dlaczego to ważne:** Utworzenie silnika z góry daje czysty obiekt do konfiguracji. Możesz ponownie używać tego samego `OcrEngine` dla wielu obrazów, jeśli przetwarzasz partię, co oszczędza pamięć i czas inicjalizacji.

## Ładowanie obrazu do OCR

Następnie informujemy silnik, który obraz ma zeskanować. Aspose udostępnia pomocniczą metodę `ImageStream.fromFile`, która ukrywa niskopoziomowy kod szkieletowy `FileInputStream`.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Wskazówka:** Zastąp `YOUR_DIRECTORY` ścieżką bezwzględną lub względną wskazującą miejsce, w którym przechowujesz `invoice.png`. Jeśli plik nie zostanie znaleziony, Aspose zgłasza `IOException`, więc warto otoczyć to blokiem try‑catch w kodzie produkcyjnym.

## Definiowanie i wyodrębnianie tekstu z regionu

Teraz pojawia się gwiazda programu: prostokąt, który określa silnikowi, gdzie patrzeć. Konstruktor `java.awt.Rectangle` przyjmuje `(x, y, width, height)` – wszystkie wartości w pikselach.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Jak to działa:** Wywołując `setRegion`, ograniczasz skanowanie OCR do fragmentu o szerokości 300 pikseli, zaczynającego się 120 pikseli od lewej krawędzi i 250 pikseli od góry. Dostosuj te liczby do własnego układu; szybki sposób na ich znalezienie to otworzyć obraz w dowolnym edytorze graficznym, który wyświetla współrzędne pikseli.

## Włączenie języka i uruchomienie rozpoznawania

Aspose OCR obsługuje dziesiątki języków, ale dla numeru faktury potrzebujemy tylko angielskiego. Włączenie właściwego języka znacząco zmniejsza liczbę fałszywych trafień.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Dlaczego włączać tylko angielski?** Silnik OCR będzie próbował dopasować znaki ze wszystkich włączonych zestawów językowych, co może go zmylić, gdy tekst składa się z prostych znaków alfanumerycznych. Zawężenie zakresu językowego poprawia zarówno szybkość, jak i precyzję.

### Oczekiwany wynik

Gdy wszystko się zgadza, zobaczysz coś w rodzaju:

```
Extracted region text: INV-12345
```

Jeśli prostokąt jest przesunięty o kilka pikseli, wynik może być zniekształcony lub pusty. To prosty test poprawności: uruchom program, spójrz na konsolę i sprawdź, czy tekst odpowiada temu, co widzisz na obrazie.

## Uruchomienie kodu i weryfikacja wyniku

Zakładając, że używasz Maven, dodaj zależność Aspose OCR do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Skompiluj i uruchom:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Albo, jeśli wolisz zwykły `javac`:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Powinieneś zobaczyć w konsoli linię **Extracted region text**. Jeśli otrzymasz komunikat „OCR recognition failed”, sprawdź ponownie ścieżkę do pliku i upewnij się, że region faktycznie zawiera czytelne znaki.

## Przypadki brzegowe i typowe wariacje

| Situation | What to Change |
|-----------|----------------|
| **Wiele języków** (np. angielski + hiszpański) | Wywołaj `ocrEngine.getLanguage().setSpanish(true);` wraz z angielskim. |
| **Region poza granicami obrazu** | Aspose cicho przytnie prostokąt, ale utracisz dane. Użyj `ImageInfo` (`ocrEngine.getImage().getWidth()`) aby zweryfikować wymiary przed ustawieniem regionu. |
| **Dynamiczne faktury** (różne układy) | Rozważ wykonanie lekkiego wstępnego skanowania całego obrazu w celu znalezienia słów kluczowych, takich jak „Invoice #”, a następnie oblicz prostokąt programowo. |
| **Obrazy o wyższej rozdzielczości DPI** | Zwiększ `ocrEngine.getImage().setResolution(300);` aby uzyskać lepszą dokładność w zeskanowanych dokumentach. |
| **Dostrajanie wydajności** | Wyłącz niepotrzebne języki, utrzymuj region jak najmniejszy i ponownie używaj jednej instancji `OcrEngine` dla wielu plików. |

## Profesjonalne wskazówki z frontu

- **Pro tip:** Jeśli potrzebujesz tylko cyfr (częste w numerach faktur), włącz tryb numeryczny za pomocą `ocrEngine.getLanguage().setDigits(true);`. To eliminuje szum alfabetowy.
- **Uwaga:** Przezroczyste PNG‑y. Aspose czasami błędnie interpretuje kanał alfa; konwersja obrazu do JPEG z jednolitym tłem może rozwiązać dziwne puste wyniki.
- **Pamiętaj:** Prostokąt używa natywnego systemu współrzędnych obrazu, a nie skalowania UI, które możesz widzieć na ekranie. Zawsze testuj na dokładnym pliku, który będziesz przetwarzać w produkcji.

## Co dalej?

Teraz, gdy masz solidny **przykład Aspose OCR Java** dla wyodrębniania opartego na regionie, możesz go rozwinąć w kilku przydatnych kierunkach:

- **Przetwarzanie wsadowe:** Przeglądaj folder z fakturami, ponownie używając tego samego `OcrEngine`, aby zwiększyć przepustowość.
- **Walidacja danych:** Przekaż wyodrębniony tekst przez wyrażenie regularne, np. `INV-\\d{5}`, aby upewnić się, że przechwycono prawidłowy numer faktury.
- **Integracja z PDF:** Użyj Aspose.PDF, aby nałożyć wyodrębniony tekst z powrotem na oryginalny dokument w celach audytu.
- **Wdrożenie w chmurze:** Owiń kod w lekki serwis REST (Spring Boot), aby inne systemy mogły wywoływać go na żądanie.

Każdy z tych kroków naturalnie obejmuje te same podstawowe koncepcje — **ładowanie obrazu do OCR**, **wyodrębnianie tekstu z regionu** oraz obsługę wyników — więc przejście będzie bezproblemowe.

*Miłego kodowania! Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź fora Aspose, gdzie społeczność dzieli się praktycznymi poprawkami dla trudnych układów.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}