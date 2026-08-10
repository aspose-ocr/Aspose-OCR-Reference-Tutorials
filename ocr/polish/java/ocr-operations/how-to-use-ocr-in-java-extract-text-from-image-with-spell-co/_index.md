---
category: general
date: 2026-05-06
description: Jak używać OCR do wyodrębniania tekstu z obrazu w Javie. Dowiedz się,
  jak konwertować obraz na tekst przy użyciu OCR, korygować błędy OCR i ładować obraz
  do OCR za pomocą Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: pl
og_description: Jak używać OCR w Javie do wyodrębniania tekstu z obrazu, korygowania
  błędów OCR i ładowania obrazu do OCR przy użyciu Aspose OCR.
og_title: Jak używać OCR w Javie – kompletny przewodnik
tags:
- OCR
- Java
- Aspose
title: Jak używać OCR w Javie – wyodrębnić tekst z obrazu z korektą ortograficzną
url: /pl/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w Javie – wyodrębnić tekst z obrazu z korektą pisowni

Zastanawiałeś się kiedyś **jak używać OCR**, aby zamienić rozmyte zdjęcie paragonu w czysty, przeszukiwalny tekst? Nie jesteś sam. W wielu projektach — aplikacje do śledzenia wydatków, pipeline'y cyfryzacji faktur, czy nawet szybki skrypt do notatek — uzyskanie wiarygodnego tekstu z obrazu jest pierwszą przeszkodą.  

Ten tutorial pokazuje dokładnie, jak używać OCR w Javie, obejmując wszystko od wczytywania obrazu do OCR po korektę błędów OCR, tak aby wynik wyglądał jak tekst wpisany przez człowieka. Po zakończeniu będziesz w stanie **wyodrębnić tekst z obrazu**, wykonać konwersję **OCR image to text** i automatycznie naprawić typowe błędy rozpoznawania.

## Co zbudujesz

Stworzymy mały program konsolowy w Javie, który:

1. Wczytuje PNG (lub dowolny obsługiwany format) do silnika Aspose OCR.  
2. Włącza wbudowaną funkcję korekty pisowni, aby **poprawić błędy OCR**.  
3. Uruchamia proces rozpoznawania i wypisuje wyczyszczony tekst.  

Bez zewnętrznych usług, bez ciężkich frameworków — tylko pojedynczy JAR i kilka linii kodu.

### Wymagania wstępne

- Java Development Kit (JDK) 8 lub nowszy.  
- Maven (lub dowolne narzędzie budujące), aby pobrać bibliotekę Aspose OCR.  
- Plik obrazu (np. `receipt.png`), który chcesz przeanalizować.  

Jeśli brakuje Ci JAR-a Aspose OCR, dodaj tę zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Wskazówka:** Darmowa wersja ewaluacyjna działa do testów, ale licencja usuwa znak wodny wersji ewaluacyjnej.

## Krok 1 – Inicjalizacja silnika OCR (Główne słowo kluczowe w akcji)

Pierwszą rzeczą, którą musisz zrobić, jest stworzenie instancji `OcrEngine`. Pomyśl o niej jak o mózgu, który odczyta piksele i przekształci je w znaki.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Dlaczego to ważne:* Inicjalizacja silnika ustawia wewnętrzne zasoby (modele językowe, słowniki itp.). Pominięcie tego kroku spowodowałoby `NullPointerException` później, gdy spróbujesz wczytać obraz.

## Krok 2 – Wczytaj obraz do OCR

Teraz faktycznie **wczytujemy obraz do OCR**. Aspose udostępnia wygodny pomocnik `ImageStream.fromFile`, ale możesz także podać `byte[]`, jeśli wolisz.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Typowy problem:* Ścieżka do pliku musi być absolutna lub względna względem katalogu roboczego. Jeśli obraz nie zostanie znaleziony, silnik zgłosi `IOException`. Sprawdź dokładnie ścieżkę, szczególnie przy uruchamianiu z IDE w porównaniu do spakowanego JAR-a.

## Krok 3 – Włącz korektę pisowni, aby **poprawić błędy OCR**

Domyślny OCR może być hałaśliwy — np. „l0ve” zamiast „love” lub „0” zamiast „O”. Włączenie korekty pisowni nakazuje silnikowi wykonać etap post‑procesingu, który naprawia typowe błędy.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Dlaczego warto to zrobić:* Bez korekty pisowni możesz musieć ręcznie oczyszczać wynik, co podważa sens automatyzacji. Wbudowany słownik dobrze działa dla języka angielskiego i kilku innych języków.

## Krok 4 – Przeprowadź rozpoznawanie (**OCR Image to Text**)

Po wczytaniu obrazu i włączeniu korekty pisowni możemy w końcu poprosić silnik o rozpoznanie tekstu.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Przypadek brzegowy:* Jeśli obraz ma niską kontrastowość lub jest mocno przechylony, wynik może nadal zawierać bełkot. Rozważ wstępne przetwarzanie (np. binaryzację, prostowanie) przed podaniem go do silnika.

## Krok 5 – Wyświetl wyczyszczony tekst

Ostatni krok to po prostu wypisanie wyniku. W prawdziwej aplikacji możesz zapisać go do bazy danych lub pliku, ale dla tej demonstracji `System.out` wystarczy.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Oczekiwany wynik

Zakładając, że `receipt.png` zawiera czytelną listę pozycji, możesz zobaczyć coś takiego:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Zauważ, że „Qty” i „Price” są poprawnie zapisane, nawet jeśli oryginalne skanowanie miało przypadkowe „Qy”.

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do pliku o nazwie `SpellCorrectDemo.java`. Upewnij się, że JAR Aspose OCR znajduje się na Twojej ścieżce klas.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Uruchom go za pomocą:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Powinieneś teraz zobaczyć wyczyszczony tekst wypisany w konsoli.

## Bonus: Dostosowywanie ustawień dla lepszej dokładności

Chociaż domyślna konfiguracja działa dla większości drukowanych dokumentów, możesz potrzebować dostosować kilka parametrów w specjalistycznych scenariuszach:

| Ustawienie | Co robi | Kiedy zmienić |
|------------|---------|----------------|
| `setLanguage(OcrLanguage.English)` | Wymusza słownik angielski (redukuje fałszywe trafienia) | Jeśli Twój obraz zawiera wyłącznie tekst po angielsku. |
| `setResolution(300)` | Informuje silnik o DPI źródłowego obrazu | Dla skanów wysokiej rozdzielczości. |
| `setEnableAutoSkewCorrection(true)` | Automatycznie obraca lekko przechylone strony | Gdy obrazy są robione telefonem. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Najczęściej zadawane pytania

**Q: Czy to działa z PDF‑ami?**  
A: Tak. Konwertuj każdą stronę PDF na obraz (np. przy użyciu Aspose PDF) i podaj obraz silnikowi OCR.

**Q: Co jeśli mój obraz jest w formacie BMP?**  
A: `ImageStream.fromFile` obsługuje PNG, JPEG, BMP, TIFF i GIF od razu. Wystarczy zmienić rozszerzenie pliku.

**Q: Czy mogę wyłączyć korektę pisowni?**  
A: Oczywiście — ustaw `setEnableSpellCorrection(false)`, jeśli potrzebujesz surowego wyniku OCR do dalszego przetwarzania.

## Zakończenie

Teraz wiesz **jak używać OCR** w Javie, aby **wyodrębnić tekst z obrazu**, automatycznie **poprawić błędy OCR** i prawidłowo **wczytać obraz do OCR** przy użyciu Aspose OCR. Pięcioetapowy przepływ — inicjalizacja, wczytanie, włączenie korekty pisowni, rozpoznanie i wyjście — obejmuje większość codziennych zadań OCR.  

Od tego momentu rozważ połączenie tej logiki z zapisem do bazy danych, endpointem REST lub przetwarzaniem wsadowym, aby obsłużyć jednocześnie dziesiątki paragonów. Eksperymentuj z dodatkową tabelą ustawień powyżej, aby wycisnąć z każdego znaku maksymalną precyzję.

Szczęśliwego kodowania i niech wyniki OCR będą zawsze czystsze niż Twoje paragonowe plamy po kawie! 

![diagram jak używać OCR pokazujący obraz → silnik OCR → poprawiony tekst flow]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}