---
category: general
date: 2026-06-16
description: Samouczek OCR z ramką ograniczającą w Javie pokazuje, jak wyodrębnić
  tekst z obrazu, odczytać tekst z obrazu oraz uzyskać wynik pewności OCR dla plików
  JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: pl
og_description: OCR bounding box w Javie pozwala rozpoznawać tekst z plików JPG, wyodrębniać
  tekst z obrazu i wyświetlać wyniki pewności OCR — wszystko w prostym przykładzie
  kodu.
og_title: Ramka ograniczająca OCR w Javie – Wyodrębnij tekst z obrazu
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Ramka ograniczająca OCR w Javie – Wyodrębnij tekst z obrazu
url: /pl/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box w Javie – Wyodrębnianie tekstu z obrazu

Zastanawiałeś się kiedyś, jak uzyskać **ocr bounding box** dla każdego fragmentu tekstu na obrazie w Javie? W tym samouczku pokażemy, jak **extract text from image** plików, **read text from image**, a także zobaczyć **ocr confidence score** podczas **recognize text from jpg** plików. Krótką odpowiedzią jest: kilka linii kodu z użyciem nowoczesnej biblioteki OCR oraz krótkie wyjaśnienie, dlaczego każde wywołanie ma znaczenie.

Poniżej znajdziesz kompletny, gotowy do uruchomienia przykład, szczegółowy podział krok po kroku oraz garść praktycznych wskazówek, które możesz od razu skopiować do swojego projektu. Na końcu będziesz w stanie wyświetlić coś takiego:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Czego będziesz potrzebować

- **Java 11** lub nowszy (składnia poniżej używa słowa kluczowego `var` dla zwięzłości, ale możesz je pominąć w starszych JDK).
- Biblioteka OCR udostępniająca API w Javie – w tym przewodniku użyjemy **[Tesseract4J](https://github.com/nguyenq/tess4j)**, lekkiego wrappera wokół popularnego silnika Tesseract.
- Obraz JPEG (`.jpg`) zawierający wyraźny, drukowany tekst.
- Twoje ulubione IDE (IntelliJ IDEA, Eclipse, VS Code…) – dowolne będzie odpowiednie.

Jeśli brakuje Ci biblioteki, po prostu dodaj tę zależność Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Zanurzmy się.

![Przykład ramki OCR](ocr-bounding-box.png "Przykład ramki OCR")

## OCR Bounding Box: Konfiguracja silnika

Pierwszą rzeczą, którą musisz zrobić, jest utworzenie instancji silnika OCR. Pomyśl o tym jak o włączeniu skanera, który później odczyta piksele.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Dlaczego to ma znaczenie:**  
Bez ustawienia `datapath` Tesseract nie będzie wiedział, gdzie znajdują się pakiety językowe i otrzymasz niejasny błąd „Failed loading language”. Wywołanie `setLanguage` jest opcjonalne, jeśli potrzebujesz tylko domyślnego pakietu angielskiego, ale jawne określenie zwiększa czytelność kodu dla przyszłych czytelników.

## Ładowanie obrazu do przetworzenia

Następnie podaj silnikowi JPEG, który chcesz przeanalizować. Biblioteka akceptuje `File` lub `BufferedImage`; użyjemy `File` dla prostoty.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Wskazówka:**  
Jeśli Twój obraz znajduje się w zasobach (np. wewnątrz pliku JAR), użyj `getResourceAsStream` i otocz go `ImageIO.read`. Dzięki temu samouczek działa zarówno lokalnie, jak i w aplikacji spakowanej.

## Wykonywanie rozpoznawania OCR

Teraz naprawdę prosimy silnik o odczytanie obrazu. Wynikiem jest zwykły ciąg tekstowy, ale chcemy także **ocr confidence score** oraz **ocr bounding box** dla każdej linii.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Dlaczego używamy `getWords` zamiast zwykłego `doOCR`:**  
`doOCR` zwraca surowy ciąg, ale pomija informacje przestrzenne. Wywołując `getWords` z `RIL_WORD` (lub `RIL_TEXTLINE`, jeśli wolisz ramki na poziomie linii), otrzymujemy listę obiektów `Word`, z których każdy zawiera tekst, pewność i prostokąt ograniczający. To jest sedno funkcji **ocr bounding box**.

## Zrozumienie wyniku

Uruchomienie powyższego fragmentu kodu na czystym obrazie JPEG daje wynik podobny do:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – rozpoznane znaki.  
- **Confidence** – wartość zmiennoprzecinkowa od 0 do 1; wyższa oznacza większą pewność silnika.  
- **Box** – prostokąt otaczający słowo w współrzędnych pikseli (x, y, szerokość, wysokość).  

Możesz teraz **read text from image** i jednocześnie dokładnie wiedzieć, gdzie każdy fragment znajduje się na płótnie — idealne do podświetlania, przycinania lub przekazywania do dalszych potoków NLP.

## Przypadki brzegowe i typowe pułapki

| Sytuacja | Na co zwrócić uwagę | Rozwiązanie / obejście |
|----------|---------------------|------------------------|
| Obraz jest rozmyty lub o niskim kontraście | Wartości confidence spadają dramatycznie (często poniżej 0.6). | Wstępna obróbka za pomocą OpenCV: zwiększ kontrast, zastosuj progowanie. |
| JPEG zawiera obrócony tekst | Ramki ograniczające są pochyłe lub brakujące. | Użyj `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)`, aby Tesseract automatycznie wykrył orientację. |
| Duże obrazy powodują OutOfMemoryError | Pamięć heap Javy zapełnia się przy ładowaniu dużych obrazów. | Zredukuj rozmiar obrazu przed OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Potrzebujesz ramek na poziomie linii zamiast słowa | `RIL_WORD` zwraca ramki per słowo. | Przełącz na `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Znaki nie‑angielskie wyświetlają się jako � | Dane językowe nie zostały załadowane. | Pobierz odpowiedni plik `.traineddata` i wskaż `setDatapath` na jego folder. |

Rozwiązanie tych problemów na wczesnym etapie oszczędza godziny debugowania później.

## Pełny działający przykład (wszystkie kroki w jednym pliku)

Poniżej znajduje się samodzielna klasa Java, którą możesz skopiować do folderu `src/main/java` i uruchomić za pomocą `mvn exec:java`. Łączy ona wszystkie omówione elementy.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Wyodrębnianie tekstu z obrazu Java z Aspose.OCR Tryb wykrywania obszarów](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Wyodrębnianie tekstu z obrazów – Podstawy OCR z Aspose.OCR dla Java](/ocr/english/java/ocr-basics/)
- [Jak rozpoznawać tekst na obrazie z językiem przy użyciu Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}