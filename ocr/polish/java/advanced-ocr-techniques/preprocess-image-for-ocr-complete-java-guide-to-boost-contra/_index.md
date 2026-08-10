---
category: general
date: 2026-02-17
description: Wstępne przetwarzanie obrazu do OCR za pomocą Aspose OCR w Javie. Dowiedz
  się, jak zwiększyć kontrast obrazu, ustawić poziom kontrastu i rozpoznać tekst z
  obrazu w zaledwie kilka minut.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: pl
og_description: Wstępne przetwarzanie obrazu do OCR przy użyciu Aspose OCR Java. Ten
  przewodnik pokazuje, jak zwiększyć kontrast obrazu, ustawić poziom kontrastu i szybko
  rozpoznać tekst z obrazu.
og_title: Przetwarzanie obrazu pod OCR – Samouczek Java zwiększający kontrast i wyodrębniający
  tekst
tags:
- Java
- OCR
- Image Processing
title: Przetwarzanie obrazu pod OCR – Kompletny przewodnik Java zwiększający kontrast
  i wyodrębniający tekst
url: /pl/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

kontrastu". Ensure proper.

Also translate table content.

Translate headings, paragraphs, bullet points, etc.

Do not translate code block placeholders.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Przetwarzanie obrazu pod OCR – Kompletny przewodnik w Javie

Czy kiedykolwiek potrzebowałeś **przetworzyć obraz pod OCR**, ale nie byłeś pewien, które ustawienia naprawdę mają znaczenie? Nie jesteś sam. Większość programistów po prostu podaje obraz silnikowi OCR i liczy na magię, otrzymując jedynie zniekształcony wynik. W tym tutorialu przeprowadzimy praktyczny, kompletny przykład, który **zwiększa kontrast obrazu**, dostosowuje **poziom kontrastu**, a na koniec **rozpoznaje tekst z obrazu** przy użyciu Aspose OCR for Java.

Po zakończeniu będziesz mieć gotowy fragment kodu, który **wyodrębnia tekst przy użyciu OCR** niezawodnie, nawet w przypadku zaszumionych skanów. Bez ukrytych sztuczek, tylko jasne kroki i uzasadnienie każdego z nich.

## Czego będziesz potrzebował

- Java 17 lub nowsza (kod kompiluje się z dowolnym aktualnym JDK)
- Biblioteka Aspose OCR for Java (pobierz ze strony Aspose)
- Ważny plik licencji Aspose OCR (`Aspose.OCR.lic`)
- Obraz wejściowy (`input.jpg`), który chcesz odczytać
- Ulubione IDE lub prosta konfiguracja wiersza poleceń

Jeśli masz już wszystko gotowe, świetnie — przechodzimy do działania.

## Krok 1: Załaduj licencję Aspose OCR (Podstawowa konfiguracja)

Zanim silnik OCR zrobi cokolwiek, musi wiedzieć, że masz licencję. W przeciwnym razie pojawi się znak wodny wersji próbnej.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Dlaczego to ważne:** Bez prawidłowej licencji silnik działa w trybie ewaluacyjnym, co może przycinać wyniki lub dodawać znaki wodne. Ustawienie licencji na początku zapewnia, że wszystkie późniejsze opcje przetwarzania wstępnego będą stosowane w trybie pełnych funkcji.

## Krok 2: Zainicjuj silnik OCR

Utworzenie instancji `OcrEngine` daje dostęp zarówno do rozpoznawania, jak i do potoków przetwarzania wstępnego.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Wskazówka:** Trzymaj silnik jako singleton, jeśli planujesz przetwarzać wiele obrazów w partii; buforuje on zasoby wewnętrzne i przyspiesza kolejne wywołania.

## Krok 3: Skonfiguruj przetwarzanie wstępne – prostowanie, odszumianie i zwiększanie kontrastu

Tutaj **przetwarzamy obraz pod OCR**. Trzy „gałki”, które ustawimy, to:

1. **Deskew** – koryguje niewielkie obroty.
2. **Denoise** – usuwa plamki, które mylą segmentację znaków.
3. **Contrast enhancement** – sprawia, że ciemny tekst wyróżnia się na tle.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Dlaczego warto dostosować poziom kontrastu?

Zwiększenie poziomu kontrastu rozciąga histogram obrazu, czyniąc ciemne piksele ciemniejszymi, a jasne jaśniejszymi. W praktyce **poziom kontrastu** `1.3f` często daje najlepszy balans dla dokumentów drukowanych, podczas gdy wartość powyżej `1.5f` może prześwietlić cienkie kreski. Śmiało eksperymentuj; zmiana tego ustawienia jest tania, a może dramatycznie poprawić skuteczność **rozpoznawania tekstu z obrazu**.

## Krok 4: Przygotuj obraz wejściowy

Klasa `OcrInput` abstrahuje obsługę plików. Możesz dodać wiele obrazów, jeśli potrzebujesz przetwarzania wsadowego.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Przypadek brzegowy:** Jeśli Twój obraz jest w niestandardowym formacie (np. TIFF z wieloma stronami), możesz załadować każdą stronę osobno lub najpierw przekonwertować go na PNG/JPEG.

## Krok 5: Wykonaj rozpoznawanie

Teraz silnik uruchamia skonfigurowany wcześniej potok przetwarzania wstępnego, a następnie przekazuje wyczyszczony obraz do rdzenia algorytmu OCR.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Co się dzieje pod maską?** Aspose OCR najpierw stosuje transformację deskew, potem filtr denoise, a na końcu dostosowuje kontrast przed przekazaniem obrazu do rozpoznawacza opartego na sieci neuronowej. Kolejność jest zamierzona; zmiana jej może prowadzić do suboptymalnych wyników.

## Krok 6: Wyświetl rozpoznany tekst

Na koniec wypisujemy wyodrębniony ciąg znaków w konsoli. W prawdziwej aplikacji możesz zapisać go do pliku lub wysłać przez sieć.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Oczekiwany wynik

Jeśli `input.jpg` zawiera frazę „Hello World!”, konsola powinna wyświetlić:

```
Hello World!
```

Jeśli wynik wygląda na zniekształcony, sprawdź ponownie wartości przetwarzania wstępnego — szczególnie **poziom kontrastu** i **tryb odszumiania** — oraz spróbuj innego formatu obrazu.

## Bonus: Wizualizacja przetworzonego obrazu (opcjonalnie)

Czasami warto zobaczyć, co silnik „widzi” po prostowaniu, odszumianiu i zwiększeniu kontrastu. Aspose OCR umożliwia wyeksportowanie pośredniego bitmapa:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Otwórz `processed.png` obok oryginału; zauważysz prostszą linię horyzontu i wyraźniejszy tekst. Ten krok jest przydatny przy diagnozowaniu, dlaczego konkretny skan się nie udaje.

![przykład przetwarzania obrazu dla OCR](/images/ocr-preprocess-example.png "przetwarzanie obrazu dla OCR – przed i po zwiększeniu kontrastu")

*Powyższy obraz ilustruje, jak zwiększenie kontrastu i odszumianie zamienia rozmyty skan w czysty, gotowy do OCR obraz.*

## Typowe pułapki i jak ich unikać

| Pułapka | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Zbyt duży kontrast** (`setContrastLevel` za wysoki) | Jasne tło staje się białe, wymazując słabe znaki | Utrzymuj poziom między 1.1 a 1.4 dla większości drukowanego tekstu |
| **Zbyt niska tolerancja prostowania** | Małe obroty pozostają niekorygowane | Zwiększ `setDeskewAngleTolerance` do 0.2 lub 0.3 dla skanowanych książek |
| **Użycie GAUSSIAN denoise na obrazach binarnych** | Rozmywa krawędzie, łącząc znaki | Trzymaj się `DenoiseMode.MEDIAN` dla skanów czarno‑białych |
| **Brak licencji** | Silnik przechodzi w tryb próbny, przycinając wynik | Zweryfikuj ścieżkę do `Aspose.OCR.lic` i upewnij się, że plik jest czytelny |

## Kolejne kroki: Wyjście poza podstawowe przetwarzanie wstępne

Teraz, gdy potrafisz **przetworzyć obraz pod OCR** i **wyodrębnić tekst przy użyciu OCR**, rozważ następujące rozszerzenia:

- **Pakiety językowe** – załaduj specyficzne słowniki językowe, aby zwiększyć dokładność dla tekstów nieangielskich.
- **Przycinanie regionu zainteresowania (ROI)** – skup się na podsekcji obrazu, jeśli potrzebujesz tylko części strony.
- **Przetwarzanie wsadowe** – iteruj po katalogu obrazów, ponownie używając tej samej instancji `OcrEngine` dla szybkości.
- **Integracja z PDF** – połącz Aspose OCR z Aspose PDF, aby w jednej linii przetworzyć zeskanowane PDF‑y na przeszukiwalne PDF‑y.

Każdy z tych tematów naturalnie wykorzystuje nasze drugorzędne słowa kluczowe: wciąż **zwiększysz kontrast obrazu**, **ustawisz poziom kontrastu** i będziesz **rozpoznawał tekst z obrazu** w różnych scenariuszach.

## Podsumowanie

Omówiliśmy wszystko, co potrzebne, aby **przetworzyć obraz pod OCR** przy użyciu Aspose OCR for Java: ładowanie licencji, konfigurację prostowania, odszumiania i zwiększania kontrastu, podanie obrazu oraz ostateczne **rozpoznawanie tekstu z obrazu**. Dzięki kompletnemu, gotowemu do uruchomienia przykładowi możesz teraz **wyodrębniać tekst przy użyciu OCR** z dowolnego odpowiednio przygotowanego zdjęcia.

Wypróbuj kod, dostosuj **poziom kontrastu** i zobacz, jak rośnie dokładność. Gdy będziesz gotowy, eksploruj modele językowe lub potoki wsadowe, aby przekształcić tę jednopunktową demonstrację w rozwiązanie gotowe do produkcji.

*Miłego kodowania i niech Twoje skany zawsze będą ostre!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}