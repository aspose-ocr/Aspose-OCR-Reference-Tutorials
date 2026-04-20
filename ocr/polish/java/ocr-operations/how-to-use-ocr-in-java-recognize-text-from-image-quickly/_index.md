---
category: general
date: 2026-02-17
description: Dowiedz się, jak używać OCR w Javie do rozpoznawania tekstu z plików
  graficznych, wyodrębniać tekst z paragonów w formacie PNG oraz konwertować paragon
  na JSON przy użyciu Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: pl
og_description: Przewodnik krok po kroku, jak używać OCR w Javie do rozpoznawania
  tekstu z obrazu, wyodrębniać tekst z paragonów w formacie PNG i konwertować paragon
  na JSON.
og_title: Jak używać OCR w Javie – Rozpoznawanie tekstu z obrazu
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Jak używać OCR w Javie – szybko rozpoznawaj tekst z obrazu
url: /pl/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać OCR w Javie – Szybko rozpoznawać tekst z obrazu

Zastanawiałeś się kiedyś **jak używać OCR**, aby wyciągnąć tekst ze zdjęcia paragonu? Być może próbowałeś kilku narzędzi online, tylko po to, by otrzymać zniekształcone znaki lub format, którego nie możesz przetworzyć. Dobra wiadomość jest taka, że przy kilku linijkach kodu Java możesz **rozpoznawać tekst z obrazu**, **wyodrębniać tekst z plików PNG** paragonów i nawet **konwertować paragon na JSON** do dalszego przetwarzania.  

W tym samouczku przeprowadzimy Cię przez kompletny przepływ pracy — od licencjonowania biblioteki Aspose OCR po uzyskanie czystego ładunku JSON, który możesz wprowadzić do bazy danych lub modelu uczenia maszynowego. Bez zbędnych ozdobników, tylko praktyczny, gotowy do uruchomienia przykład, który możesz skopiować i wkleić do swojego IDE. Po zakończeniu będziesz mieć samodzielny program, który przyjmuje `receipt.png` i zwraca gotowy do użycia ciąg JSON.

## Czego będziesz potrzebować

- **Java Development Kit (JDK) 8+** – dowolna nowsza wersja działa.
- **Aspose OCR for Java** library (artefakt Maven to `com.aspose:aspose-ocr`).
- **ważny plik licencji Aspose OCR** (`Aspose.OCR.lic`). Darmowa wersja próbna działa do testów, ale prawidłowa licencja usuwa ograniczenia wersji ewaluacyjnej.
- Plik obrazu (PNG, JPEG itp.), który zawiera tekst, który chcesz odczytać — nazwijmy go `receipt.png` i umieść w znanym folderze.
- Twoje ulubione IDE (IntelliJ IDEA, Eclipse, VS Code…) – wybór należy do Ciebie.

> **Pro tip:** Trzymaj plik licencji poza folderem źródłowym i odwołuj się do niego za pomocą ścieżki bezwzględnej lub względnej, aby nie commitować go do kontroli wersji.

Teraz, gdy wymagania są jasne, zanurzmy się w rzeczywisty kod.

## Jak używać OCR – Główne kroki

Poniżej znajduje się przegląd wysokiego poziomu działań, które wykonamy:

1. **Załaduj bibliotekę Aspose OCR** i zastosuj swoją licencję.  
2. **Utwórz instancję `OcrEngine`** – to silnik, który wykonuje ciężką pracę.  
3. **Przygotuj obiekt `OcrInput`** wskazujący na obraz, który chcesz przetworzyć.  
4. **Wywołaj `recognize` z `ResultFormat.JSON`**, aby uzyskać reprezentację JSON wyodrębnionego tekstu.  
5. **Obsłuż wynik JSON** – wydrukuj go, zapisz do pliku lub przetwórz dalej.

Każdy krok jest wyjaśniony szczegółowo w kolejnych sekcjach.

## Krok 1 – Zainstaluj Aspose OCR i zastosuj swoją licencję

Najpierw dodaj zależność Aspose OCR do swojego `pom.xml`, jeśli używasz Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Teraz, w kodzie Java, załaduj licencję. Ten krok jest niezbędny; bez niego biblioteka działa w trybie ewaluacyjnym i może wstawiać znaki wodne w wyniku.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Dlaczego to ważne:** Obiekt `License` informuje silnik OCR, że jesteś uprawniony do korzystania z pełnego zestawu funkcji, w tym rozpoznawania o wysokiej dokładności i eksportu JSON. Pominięcie tego kroku nadal pozwoli Ci **rozpoznawać tekst z obrazu**, ale wyniki mogą być ograniczone.

## Krok 2 – Utwórz instancję silnika OCR

Klasa `OcrEngine` jest punktem wejścia dla wszystkich operacji OCR. Traktuj ją jak „mózg”, który odczytuje piksele i decyduje, jakie znaki one reprezentują.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Możesz dostosować silnik (np. ustawić język, włączyć prostowanie) później, jeśli Twoje paragony zawierają skrypty niełacińskie lub są zeskanowane pod kątem. Dla większości paragonów z USA domyślne ustawienia działają doskonale.

## Krok 3 – Załaduj obraz, który chcesz przetworzyć

Teraz skierujemy silnik OCR na plik zawierający paragon. Klasa `OcrInput` może przyjmować wiele obrazów, ale w tym samouczku uprościmy to do jednego pliku PNG.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Jeśli kiedykolwiek będziesz musiał **wyodrębniać tekst z plików PNG** masowo, po prostu wywołaj `input.add()` wielokrotnie lub przekaż listę ścieżek do plików.

## Krok 4 – Rozpoznaj tekst i konwertuj paragon na JSON

Oto serce samouczka. Prosimy silnik o rozpoznanie tekstu i zwrócenie wyniku w formacie JSON. Flaga `ResultFormat.JSON` wykonuje całą ciężką pracę za nas.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Ładunek JSON zawiera każdą rozpoznaną linię, jej ramkę ograniczającą, współczynnik pewności oraz surowy tekst. Ta struktura sprawia, że **konwersja paragonu na JSON** jest trywialna i można go przekazać do dowolnego API downstream.

## Krok 5 – Połącz wszystko i uruchom program

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java, który łączy wszystko razem. Zapisz go jako `JsonExportDemo.java` (lub dowolną nazwę) i uruchom w swoim IDE lub z wiersza poleceń.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje ciąg JSON podobny do poniższego (dokładna zawartość zależy od Twojego paragonu):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Teraz możesz przekazać ten JSON do bazy danych, punktu końcowego REST lub potoku analizy danych. Krok **konwersji paragonu na JSON** jest już dla Ciebie wykonany.

## Często zadawane pytania i przypadki brzegowe

### Co zrobić, jeśli obraz jest obrócony?

Aspose OCR automatycznie wykrywa i koryguje niewielkie obroty. W przypadku mocno przechylonych obrazów, wywołaj `engine.getImagePreprocessingOptions().setDeskew(true)` przed rozpoznaniem.

### Jak obsłużyć wiele języków?

Użyj `engine.getLanguage()`, aby ustawić żądany język, np. `engine.setLanguage(Language.FRENCH)`. Jest to przydatne, gdy musisz **rozpoznawać tekst z obrazu**, który zawiera wielojęzyczne paragony.

### Czy mogę wyjść w formacie zwykłego tekstu zamiast JSON?

Oczywiście. Zastąp `ResultFormat.JSON` na `ResultFormat.TEXT` i wywołaj `result.getText()`.

### Czy istnieje sposób, aby ograniczyć OCR do konkretnego regionu?

Tak — użyj `ocrInput.add(imagePath, new Rectangle(x, y, width, height))`, aby skupić się na obszarze paragonu, co może poprawić szybkość i dokładność.

## Pro tipy dla OCR gotowego do produkcji

- **Cache'uj obiekt licencji** jeśli przetwarzasz wiele plików w pętli; wielokrotne tworzenie go zwiększa narzut.
- **Przetwarzanie wsadowe**: załaduj wszystkie ścieżki paragonów do jednego `OcrInput` i wywołaj `recognize` raz. JSON będzie zawierał tablicę stron, każda ze swoimi liniami.
- **Waliduj JSON**: po otrzymaniu ciągu, sparsuj go przy pomocy biblioteki takiej jak Jackson, aby upewnić się, że jest poprawny przed zapisaniem.
- **Monitoruj pewność**: JSON zawiera pole `confidence` dla każdej linii. Filtruj linie poniżej progu (np. 0,85), aby uniknąć nieprawidłowych danych.
- **Zabezpiecz swoją licencję**: przechowuj `Aspose.OCR.lic` w bezpiecznym magazynie lub zmiennej środowiskowej, szczególnie w wdrożeniach w chmurze.

## Podsumowanie

Omówiliśmy **jak używać OCR** w Javie, aby **rozpoznawać tekst z obrazu**, **wyodrębniać tekst z plików PNG** paragonów i **konwertować paragon na JSON** — wszystko w zwięzłym, kompletnym przykładzie. Kroki są proste, kod w pełni uruchamialny, a wynikowy JSON zapewnia ustrukturyzowaną reprezentację gotową do dowolnego systemu downstream.  

Następnie możesz zbadać bardziej zaawansowane scenariusze: przesyłanie JSON do Apache Kafka w celu przetwarzania w czasie rzeczywistym, stosowanie wyrażeń regularnych do wyciągania sum pozycji, lub integrację z usługą OCR w chmurze w celu skalowalności. Cokolwiek wybierzesz, podstawy, które właśnie poznałeś, pozostaną niezmienne.  

Masz pytania lub napotkałeś problem podczas próby? Dodaj komentarz poniżej, a wspólnie rozwiążemy problem. Szczęśliwego kodowania i ciesz się przekształcaniem nieuporządkowanych zdjęć paragonów w czyste, przeszukiwalne dane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}