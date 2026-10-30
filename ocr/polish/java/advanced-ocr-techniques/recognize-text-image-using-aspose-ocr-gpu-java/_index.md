---
category: general
date: 2026-10-30
description: Dowiedz się, jak szybko wyodrębnić tekst z obrazu przy użyciu Aspose
  OCR GPU w Javie. Ten przewodnik pokazuje, jak ustawić GPU device ID i osiągnąć wysokowydajny
  OCR.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Dowiedz się, jak szybko wyodrębnić tekst z obrazu przy użyciu Aspose
  OCR GPU w Javie. Ten przewodnik pokazuje, jak ustawić GPU device ID dla optymalnej
  wydajności.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Jak wyodrębnić tekst z obrazu przy użyciu Aspose OCR GPU w Javie
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Jak wyodrębnić tekst z obrazu przy użyciu Aspose OCR GPU w Javie
url: /pl/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst z obrazu przy użyciu Aspose OCR GPU w Javie

Jeśli kiedykolwiek próbowałeś **wyodrębnić tekst z obrazu** w aplikacji Java i zauważyłeś, że CPU nie radzi sobie z wysokiej rozdzielczości skanami, nie jesteś sam. Wielu programistów napotyka wąskie gardła wydajności przy przetwarzaniu dużych dokumentów. Aspose OCR dla Javy usuwa tę przeszkodę, umożliwiając uruchomienie OCR na GPU, co dramatycznie skraca czas przetwarzania. W tym samouczku zobaczysz kompletny, gotowy do uruchomienia przykład, który pokazuje, jak ustawić licencję, włączyć przyspieszenie GPU oraz **ustawić identyfikator urządzenia GPU**, gdy dostępnych jest wiele kart graficznych.

## Szybkie odpowiedzi
- **Jaki jest najszybszy sposób wyodrębnienia tekstu z obrazu w Javie?** Użyj Aspose OCR z przyspieszeniem GPU i ustaw odpowiedni identyfikator urządzenia GPU.  
- **Która wersja Javy jest wymagana?** Java 17 lub nowsza jest zalecana dla najlepszej wydajności.  
- **Czy potrzebuję licencji na obsługę GPU?** Tak — funkcje GPU są odblokowywane tylko przy ważnej licencji Aspose OCR.  
- **Czy mogę uruchomić to na serwerze bez interfejsu graficznego?** Oczywiście; wymagany jest jedynie sterownik GPU i zestaw narzędzi CUDA.  
- **Ile języków jest obsługiwanych?** Ponad 30 języków, w tym angielski, chiński, arabski i hindi.

## Co to jest wyodrębnianie tekstu z obrazu?
Wyodrębnianie tekstu z obrazu oznacza konwersję wizualnej reprezentacji znaków przechowywanych w formatach bitmapowych, takich jak PNG, JPG czy TIFF, na edytowalny, przeszukiwalny tekst Unicode. Proces ten, znany jako rozpoznawanie znaków optycznych (OCR), umożliwia dalsze zadania, takie jak indeksowanie, tłumaczenie i ekstrakcja danych.

## Dlaczego używać Aspose OCR GPU?
Aspose OCR wykorzystuje przyspieszenie GPU do obsługi dużych, wysokiej rozdzielczości obrazów znacznie wydajniej niż przetwarzanie wyłącznie na CPU. Obsługuje ponad 30 formatów wejściowych i może przetwarzać obrazy do 5000 × 5000 px przy niskim zużyciu pamięci, zapewniając do pięciu razy szybsze rozpoznawanie na nowoczesnych kartach NVIDIA GPU.

## Czego będziesz potrzebować
- **Java 17** lub nowsza (kompatybilna z Java 8+, ale wydania LTS zapewniają lepszą wydajność JIT).  
- **Biblioteka Aspose OCR dla Javy** (pobierz plik JAR ze strony Aspose).  
- Ważny **plik licencji Aspose OCR** (`Aspose.OCR.lic`). Bezpłatna wersja próbna działa, ale funkcje GPU wymagają licencjonowanej wersji.  
- Plik obrazu (`sample-image.png`) zawierający wyraźny, maszynowo czytelny tekst.  
- Kompatybilny z CUDA GPU NVIDIA (lub równoważny) z odpowiednim sterownikiem zainstalowanym.

Jeśli któreś z tych pojęć jest Ci nieznane, nie martw się — każdy punkt zostanie wyjaśniony w trakcie.

## Krok 1: dodaj Aspose OCR do swojego projektu
Najpierw dołącz plik JAR Aspose OCR do classpath. Jeśli używasz Maven, dodaj następującą zależność do `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Dla Gradle użyj:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Jeśli wolisz ręczną metodę, umieść JAR w folderze `libs/` i dodaj go do ścieżki modułu w IDE.

> **Wskazówka:** Trzymaj numer wersji zgodny z notatkami wydania; nowsze wersje często zawierają ulepszenia wydajności dla przetwarzania GPU.

## Krok 2: załaduj licencję Aspose OCR (wymagane do użycia GPU)
Bez licencji wywołanie `setEnableGpu(true)` cicho przełączy się na tryb CPU. Załaduj licencję na samym początku `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Zastąp `YOUR_DIRECTORY` absolutną lub względną ścieżką, w której przechowujesz plik `.lic`. Nieprawidłowa ścieżka wywoła `FileNotFoundException`, więc sprawdź pisownię.

## Krok 3: utwórz silnik OCR i włącz przyspieszenie GPU
Klasa `OcrEngine` jest podstawowym komponentem wykonującym operacje OCR na obrazach.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Po co używać identyfikatora urządzenia? W środowisku z wieloma GPU możesz przeznaczyć jedną kartę do wstępnego przetwarzania, a drugą do OCR. Ustawienie ID zapewnia, że ciężkie operacje będą wykonywane na wybranym sprzęcie.

## Krok 4: przygotuj obraz wejściowy
Klasa `OcrInput` reprezentuje kolekcję obrazów, które chcesz przetworzyć.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Jeśli musisz przetworzyć strumień (np. przesłany plik), użyj `ocrInput.add(InputStream)`.

## Krok 5: uruchom proces rozpoznawania i pobierz wynik
Klasa `OcrResult` zawiera zwykły tekst, wyniki pewności oraz opcjonalne informacje o układzie zwracane przez silnik.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

Konsola wyświetli coś podobnego do:

```
Recognized text:
Hello, world!
This is a sample image.
```

Jeśli obraz jest rozmyty lub język nie jest obsługiwany, wynik może być pusty. W takim przypadku sprawdź wartość `ocrResult.getConfidence()` (0‑100), aby zdecydować, czy ponowić próbę po wstępnym przetworzeniu.

## Pełny, gotowy do uruchomienia przykład
Połączenie wszystkich elementów daje jedną klasę Java, którą możesz skopiować i wkleić do swojego IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Oczekiwany wynik:** Konsola wypisuje dokładny tekst, który pojawia się w `sample-image.png`. Gdy GPU jest aktywne, czas przetwarzania zazwyczaj spada z kilku sekund (CPU) do poniżej jednej sekundy przy typowym skanie 300 dpi.

## Częste pytania i przypadki brzegowe

### Czy to działa na serwerze bez interfejsu graficznego?
Tak. Sterownik GPU musi być zainstalowany, ale wyświetlacz nie jest wymagany. Upewnij się, że zestaw narzędzi `CUDA` (lub równoważny dla Twojego GPU) jest dostępny w systemowej zmiennej `PATH`. Takie ustawienie pozwala OCR działać w środowiskach chmurowych lub konteneryzowanych bez interfejsu graficznego.

### Co zrobić, jeśli mam więcej niż jeden GPU i chcę użyć GPU 1?
Change the device ID as shown:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Ustawienie ID na `1` kieruje silnik OCR do użycia drugiego GPU w systemie, co może być przydatne, gdy pierwszy GPU jest zarezerwowany dla innych zadań.

### Jak wyodrębnić tekst z obrazu w innym języku?
Set the language before calling `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR obsługuje **ponad 30 języków**, w tym skrypty od prawej do lewej, takie jak arabski i hebrajski. Wybranie właściwego języka znacznie zwiększa dokładność.

### Co zrobić, jeśli obraz zawiera wiele stron (np. PDF przekonwertowany na obrazy)?
Create a separate `OcrInput` entry for each page, or loop over the files:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Silnik łączy wyniki w kolejności, zachowując kolejność stron w ostatecznym wyniku.

### Jak obsłużyć wyniki o niskiej pewności?
Check the confidence score:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Typowe kroki wstępnego przetwarzania obejmują binaryzację, redukcję szumów lub zmianę rozmiaru do 300 dpi. Ponowne uruchomienie OCR po takim przetworzeniu często podnosi poziom pewności.

## Wskazówki dotyczące wydajności
- **Przetwarzanie wsadowe:** Dodanie wielu obrazów do jednego `OcrInput` zmniejsza narzut związany z wielokrotnym inicjowaniem kontekstu GPU.  
- **Rozgrzewka:** Uruchom jednorazowo rozpoznanie testowe po uruchomieniu JVM; pierwsze wywołanie powoduje opóźnienie inicjalizacji sterownika.  
- **Zarządzanie pamięcią:** Usuń duże obiekty `OcrInput` (`ocrInput.clear()`) po zakończeniu, aby zwolnić pamięć GPU.  

## Zakończenie
Teraz wiesz, jak efektywnie **wyodrębnić tekst z obrazu** przy użyciu silnika GPU Aspose OCR w Javie, jak **ustawić identyfikator urządzenia GPU** przy pracy z wieloma kartami graficznymi oraz jak radzić sobie z wielojęzycznymi scenariuszami. Pełny, gotowy do uruchomienia kod powyżej powinien działać od razu — wystarczy podmienić licencję i ścieżki do obrazów.

Gotowy na kolejny krok? Spróbuj przetworzyć cały folder zeskanowanych PDF‑ów, eksperymentuj z różnymi opcjami `setLanguage` lub połącz wynik OCR z modelem uczenia maszynowego w celu dalszego przetwarzania. Korzyści wydajnościowe płynące z przyspieszenia GPU czynią projekty na dużą skalę wykonalnymi.

Miłego kodowania i zachęcam do pozostawienia komentarza, jeśli napotkasz jakiekolwiek problemy!

## Najczęściej zadawane pytania

**P: Czy mogę używać tego w aplikacji komercyjnej?**  
O: Tak — wystarczy zainstalować ważną licencję Aspose OCR. Bezpłatna wersja próbna służy wyłącznie do oceny.

**P: Czy wersja GPU działa na serwerach Linux?**  
O: Absolutnie; pod warunkiem, że sterownik NVIDIA i zestaw narzędzi CUDA są zainstalowane, biblioteka działa w środowiskach Linux bez interfejsu graficznego.

**P: Jaki jest maksymalny obsługiwany rozmiar obrazu?**  
O: Aspose OCR może przetwarzać obrazy do **5000 × 5000 px** bez wczytywania całego pliku do pamięci.

**P: Jak zaktualizować do najnowszej wersji Aspose OCR?**  
O: Zamień stary plik JAR na nowy i zaktualizuj numer wersji zależności w Maven/Gradle.

**P: Czy istnieje sposób na uzyskanie współrzędnych ramki ograniczającej dla każdego słowa?**  
O: Tak — `OcrResult` dostarcza informacje o układzie, w tym ramki ograniczające na poziomie słowa, gdy włączysz opcję `setIncludeLayout(true)`.

---

**Ostatnia aktualizacja:** 2026-10-30  
**Testowano z:** Aspose OCR for Java 24.11  
**Autor:** Aspose

## Powiązane samouczki

- [Rozpoznaj tekst z obrazu Java OCR z przyspieszeniem GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Jak włączyć GPU dla OCR w Javie i wyodrębnić tekst z obrazu](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Wyodrębnij tekst z obrazu przy użyciu Aspose OCR Java – szybki przewodnik](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}