---
category: general
date: 2026-06-19
description: Automatyczne prostowanie obrazu przy użyciu Aspose OCR w Javie. Dowiedz
  się, jak skorygować pochylenie, wyodrębnić tekst OCR i uzyskać kąt prostowania w
  kilku prostych krokach.
draft: false
keywords:
- auto deskew image
- extract text ocr
- how to correct skew
- how to get deskew
language: pl
og_description: Automatyczne prostowanie obrazu przy użyciu Aspose OCR w Javie. Dowiedz
  się, jak skorygować pochylenie, wyodrębnić tekst OCR i uzyskać kąt prostowania —
  wszystko w jednym przewodniku.
og_title: Automatyczne prostowanie obrazu w Javie – Pełny samouczek Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Auto deskew image using Aspose OCR in Java. Learn how to correct skew,
    extract text OCR and get deskew angle in a few easy steps.
  headline: Auto Deskew Image in Java – Complete Aspose OCR Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Processing
title: Automatyczne prostowanie obrazu w Javie – Kompletny przewodnik Aspose OCR
url: /pl/java/ocr-operations/auto-deskew-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatyczne prostowanie obrazu w Javie – Kompletny przewodnik Aspose OCR

Zastanawiałeś się kiedyś, jak **auto deskew image** pliki przed uruchomieniem OCR? Być może zrobiłeś zdjęcie paragonu na pochyłym stole, albo zeskanowany formularz przybył z delikatnym pochyleniem, a wyodrębnianie tekstu kończy się zniekształceniem. To powszechny problem, szczególnie gdy potrzebujesz niezawodnych wyników **extract text OCR** do dalszego przetwarzania.

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby **auto deskew image** pliki przy użyciu Aspose OCR dla Javy, pokażemy **how to correct skew**, oraz ujawnimy **how to get deskew** szczegóły po zakończeniu działania silnika. Na końcu będziesz mieć gotowy do uruchomienia program w Javie, który nie tylko automatycznie prostuje obrazy, ale także wyciąga z nich czysty tekst. Bez zbędnych dodatków, tylko praktyczny kod i wyjaśnienia, które możesz skopiować i wkleić już dziś.

## Co się nauczysz

- Załaduj i licencjonuj Aspose OCR w projekcie Java.  
- Włącz automatyczną funkcję prostowania silnika.  
- Ustaw próg pewności, aby uniknąć nadmiernej korekcji.  
- Uruchom OCR na nachylonym obrazie i pobierz zastosowany kąt prostowania.  
- Wyodrębnij rozpoznany tekst z wynikami opartymi na pewności.  

**Wymagania wstępne** – Java 8+ SDK, Maven lub Gradle do zarządzania zależnościami oraz plik licencji Aspose OCR. Jeśli jesteś nowy w Mavenie, nie martw się; omówimy minimalny fragment `pom.xml`, którego potrzebujesz.

---

## ## Automatyczne prostowanie obrazu z Aspose OCR – Krok 1: Konfiguracja projektu

Na początek, dodajmy bibliotekę do Twojego projektu. Dodaj następującą zależność do swojego `pom.xml` (lub odpowiedni wpis Gradle):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Wskazówka:** Zwracaj uwagę na numer wersji; Aspose często wydaje poprawki wydajnościowe dla algorytmów prostowania.

Gdy Maven rozwiąże artefakt, utwórz prostą klasę Java o nazwie `SkewDemo`. Będzie to środowisko, w którym pokażemy **how to correct skew** oraz **how to get deskew** informacje.

## ## Jak skorygować pochylenie – Krok 2: Licencja i inicjalizacja silnika

Zanim wywołasz jakąkolwiek metodę OCR, musisz załadować swoją licencję. W przeciwnym razie biblioteka działa w trybie ewaluacyjnym i ogranicza liczbę stron, które możesz przetworzyć.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // Load the Aspose OCR license (replace with your actual path)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Zauważ, że krok licencji jest wydzielony na początku — odzwierciedla to najlepsze praktyki, w których licencjonowanie jest jednorazową konfiguracją, a nie powtarzane przy każdym obrazie. Jeśli o tym zapomnisz, silnik zgłosi wyjątek licencyjny, co jest częstą przeszkodą dla nowicjuszy.

## ## Jak uzyskać informacje o prostowaniu – Krok 3: Włącz Auto‑Deskew i ustaw pewność

Teraz tworzymy instancję silnika OCR i instruujemy go, aby **auto deskew image** automatycznie. Wywołanie `setAutoDeskew(true)` aktywuje wewnętrzny algorytm, który wykrywa kąt obrotu i obraca bitmapę z powrotem do poziomej linii bazowej.

```java
        // Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic deskewing
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        // Define how confident the engine must be before applying the correction
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // 85% confidence is a safe default
```

Dlaczego próg pewności? Wyobraź sobie zdjęcie billboardu zrobione pod dziwnym kątem; silnik może zgadnąć ogromny obrót i zepsuć tekst. Ustawiając `0.85`, mówimy „zastosuj prostowanie tylko, jeśli jesteśmy przynajmniej w 85 % pewni”. Możesz dostosować tę wartość w górę lub w dół w zależności od tego, jak szumne są Twoje obrazy.

## ## Wyodrębnianie tekstu OCR – Krok 4: Rozpoznaj obraz

Gdy silnik jest gotowy, podaj mu ścieżkę do nachylonego zdjęcia. Metoda `recognizeImage` wykonuje zarówno prostowanie (jeśli włączone), jak i OCR w jednym przebiegu.

```java
        // Recognize text from a skewed image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg");
```

Jeśli plik nie zostanie znaleziony, Java zgłosi `FileNotFoundException`. Szybka kontrola — upewnij się, że ścieżka jest absolutna lub względna względem katalogu roboczego, z którego uruchamiasz program.

## ## Automatyczne prostowanie obrazu – Krok 5: Pobierz kąt prostowania i wyodrębniony tekst

Po rozpoznaniu obiekt `OcrResult` dostarcza dwa cenne elementy: kąt zastosowany przez silnik oraz wyjściowy tekst zwykły.

```java
        // Print the applied deskew angle
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());

        // Print the extracted text
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

Metoda `getAppliedDeskewAngle()` zwraca `double` reprezentujący stopnie (dodatnie dla obrotu zgodnego z ruchem wskazówek zegara). Jeśli obraz był już wypoziomowany, zobaczysz `0.0`. To jest sedno **how to get deskew** informacji, które można logować w ścieżkach audytu lub zwracać do interfejsu UI, aby pokazać użytkownikom korektę wykonaną w tle.

## ## Pełny działający przykład – Wszystkie kroki w jednym pliku

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java. Skopiuj go do swojego IDE, zamień ścieżki licencji i obrazu, i naciśnij *Run*.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // -------------------- Step 1: License --------------------
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic"); // <-- update path

        // -------------------- Step 2: Engine --------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------- Step 3: Auto‑Deskew --------------------
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // high‑confidence only

        // -------------------- Step 4: Recognize --------------------
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg"); // <-- update path

        // -------------------- Step 5: Results --------------------
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Oczekiwany wynik** (przykład):

```
Applied angle: -2.7
Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $89.99
Thank you for your business!
```

Zauważ, że kąt jest małą liczbą ujemną — oznacza to, że oryginalne zdjęcie było nachylone o kilka stopni przeciwnie do ruchu wskazówek zegara, a Aspose skorygował je przed OCR.

## ## Częste pułapki i przypadki brzegowe

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Brak zastosowanego prostowania (angle = 0)** | Obraz już wypoziomowany lub pewność poniżej progu. | Obniż `setDeskewConfidenceThreshold` do `0.6` dla szumnych skanów. |
| **Śmieciowe znaki w wyniku** | Jakość obrazu zbyt niska; szum zakłóca zarówno prostowanie, jak i OCR. | Wstępnie przetwórz obraz filtrem wygładzającym lub zwiększ DPI przed przekazaniem do Aspose. |
| **Licencja nie znaleziona** | Nieprawidłowa ścieżka lub brak pliku. | Użyj ścieżki absolutnej lub umieść plik `.lic` w classpath i wywołaj `license.setLicense("Aspose.OCR.lic");`. |
| **Brak pamięci przy dużych partiach** | Każde wywołanie ładuje cały obraz do pamięci. | Użyj jednej instancji `OcrEngine` i wywołaj `ocrEngine.clear()` po każdym obrazie. |

## ## Idąc dalej – kolejne kroki

- **Przetwarzanie wsadowe:** Przejdź przez katalog obrazów, zbierz każdy `appliedDeskewAngle` i zapisz wyniki w pliku CSV do analizy.  
- **Wybór języka:** Użyj `ocrEngine.setLanguage(OcrLanguage.English);`, aby poprawić dokładność w dokumentach wielojęzycznych.  
- **OCR oparty na regionie:** Jeśli interesuje Cię tylko określony obszar (np. kod kreskowy), wywołaj `ocrEngine.recognizeRegion(rect);`.  

Wszystkie te rozszerzenia nadal korzystają z fundamentu **auto deskew image**, który zbudowaliśmy, ponieważ prawidłowo ustawiona bitmapa jest najważniejszym czynnikiem wpływającym na wysoką jakość OCR.

## ## Zakończenie

Omówiliśmy wszystko, co potrzebne, aby **auto deskew image** pliki w Javie z Aspose OCR, pokazaliśmy **how to correct skew**, zademonstrowaliśmy **how to get deskew** kąty i w końcu wyodrębniliśmy czysty tekst za pomocą **extract text OCR**. Krótki, samodzielny program działa w kilka sekund, a jednocześnie rozwiązuje trudny problem, który w innym wypadku wymagałby osobnej biblioteki przetwarzania obrazów.

Wypróbuj go na własnych zdjęciach, dostosuj próg pewności i obserwuj, jak kąt prostowania pojawia się w konsoli. Gdy poczujesz się pewnie, dodaj logikę wsadową lub zintegrować wynik z pipeline'em zarządzania dokumentami. Nie ma ograniczeń — pamiętaj, że wypoziomowany obraz to kluczowy składnik niezawodnego OCR.

Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź oficjalną dokumentację Java Aspose pod kątem najnowszych zmian API. Szczęśliwego kodowania i niech Twoje skany zawsze będą wypoziomowane! 

![Diagram ilustrujący automatyczne prostowanie nachylonego obrazu przed wyodrębnianiem OCR – proces auto deskew image](auto-deskew-diagram.png "przepływ pracy auto deskew image")

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak obliczyć kąt pochylenia w Javie przy użyciu Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)
- [Rozpoznawanie tekstu na obrazie z Aspose OCR – Pełny samouczek Java OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Wyodrębnianie tekstu z obrazu w Javie z Aspose.OCR w trybie wykrywania obszarów](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}