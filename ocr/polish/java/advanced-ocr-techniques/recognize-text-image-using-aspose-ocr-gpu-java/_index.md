---
category: general
date: 2026-02-17
description: Szybko rozpoznawaj tekst na obrazie przy użyciu Aspose OCR z obsługą
  GPU w Javie. Dowiedz się, jak wyodrębnić tekst z obrazu i ustawić identyfikator
  urządzenia GPU dla optymalnej wydajności.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: pl
og_description: Szybko rozpoznawaj tekst na obrazie za pomocą Aspose OCR z obsługą
  GPU w Javie. Ten przewodnik pokazuje, jak wyodrębnić tekst z obrazu i ustawić identyfikator
  urządzenia GPU.
og_title: Rozpoznawanie tekstu na obrazie przy użyciu Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Rozpoznawanie tekstu na obrazie przy użyciu Aspose OCR GPU – Java
url: /pl/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu na obrazie przy użyciu Aspose OCR GPU – Java

Kiedykolwiek potrzebowałeś **rozpoznać tekst na obrazie** w aplikacji Java, a CPU nie radziło sobie z dużymi plikami? Nie jesteś sam — wielu programistów napotyka ten problem przy przetwarzaniu skanów wysokiej rozdzielczości. Dobra wiadomość? Aspose OCR pozwala **wyodrębnić tekst z obrazu** przy użyciu GPU, co dramatycznie skraca czas przetwarzania.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład, który pokaże dokładnie, jak skonfigurować licencję, włączyć przyspieszenie GPU oraz **ustawić id urządzenia GPU**, gdy masz kilka kart graficznych. Po zakończeniu będziesz mieć samodzielny program, który wypisze rozpoznany tekst w konsoli — bez dodatkowych kroków.

## Co będzie potrzebne

- **Java 17** lub nowsza (API jest kompatybilne z Java 8+, ale najnowszy LTS zapewnia lepszą wydajność).  
- Biblioteka **Aspose OCR for Java** (pobierz plik JAR ze strony Aspose).  
- Ważny **plik licencji Aspose OCR** (`Aspose.OCR.lic`). Wersja trial działa, ale funkcje GPU są dostępne tylko w licencjonowanej wersji.  
- Plik obrazu (`sample-image.png`) zawierający czytelny, maszynowo odczytywalny tekst.  
- Środowisko z obsługą GPU (najlepiej karta NVIDIA kompatybilna z CUDA).  

Jeśli któryś z elementów jest Ci nieznany, nie martw się — każdy punkt zostanie wyjaśniony w dalszej części.

## Krok 1: Dodaj Aspose OCR do projektu

Najpierw dodaj plik JAR Aspose OCR do classpath. Jeśli używasz Maven, dodaj następującą zależność do `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Dla Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Jeśli wolisz ręczną instalację, umieść JAR w folderze `libs/` i dodaj go do ścieżki modułu w IDE.

> **Pro tip:** Trzymaj numer wersji zgodny z notatkami wydania biblioteki; nowsze wersje często wprowadzają ulepszenia wydajności przy przetwarzaniu na GPU.

## Krok 2: Załaduj licencję Aspose OCR (wymagane dla użycia GPU)

Bez licencji wywołanie `setEnableGpu(true)` przełączy się cicho na tryb CPU. Załaduj licencję na samym początku metody `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Zastąp `YOUR_DIRECTORY` absolutną lub względną ścieżką, w której przechowujesz plik `.lic`. Jeśli ścieżka jest nieprawidłowa, Aspose zgłosi `FileNotFoundException`, więc sprawdź pisownię.

## Krok 3: Utwórz silnik OCR i włącz przyspieszenie GPU

Teraz tworzymy obiekt `OcrEngine` i instruujemy go, aby używał GPU. Metoda `setGpuDeviceId` pozwala wybrać konkretną kartę, gdy dostępnych jest ich więcej niż jedna.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Po co podawać identyfikator urządzenia? W serwerze z wieloma GPU możesz przeznaczyć jedną kartę do wstępnego przetwarzania obrazu, a drugą do OCR. Ustawienie ID zapewnia, że właściwy sprzęt wykona ciężką pracę.

## Krok 4: Przygotuj obraz wejściowy

Aspose OCR obsługuje różne formaty (PNG, JPG, BMP, TIFF). Owiń swój plik w obiekt `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Jeśli potrzebujesz przetworzyć strumień (np. przesłany plik), użyj `ocrInput.add(InputStream)` zamiast tego.

## Krok 5: Uruchom proces rozpoznawania i pobierz wynik

Metoda `recognize` zwraca obiekt `OcrResult`, który zawiera czysty tekst, oceny pewności oraz informacje o układzie, jeśli są potrzebne.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

Konsola wyświetli coś w stylu:

```
Recognized text:
Hello, world!
This is a sample image.
```

Jeśli obraz jest rozmyty lub język nie jest obsługiwany, wynik może być pusty. W takim wypadku sprawdź wartość `ocrResult.getConfidence()` (0‑100), aby zdecydować, czy ponownie przetworzyć obraz po wstępnej obróbce.

## Pełny, gotowy do uruchomienia przykład

Po złożeniu wszystkich elementów otrzymujesz jedną klasę Java, którą możesz skopiować i wkleić do swojego IDE:

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

> **Oczekiwany wynik:** Konsola wypisze dokładny tekst znajdujący się w `sample-image.png`. Jeśli GPU jest aktywne, zauważysz spadek czasu przetwarzania z kilku sekund (CPU) do poniżej sekundy przy typowych skanach 300 dpi.

## Częste pytania i sytuacje brzegowe

### Czy to działa na serwerze bez interfejsu graficznego?

Tak. Wymagany jest zainstalowany sterownik GPU, ale nie jest potrzebny wyświetlacz. Upewnij się jedynie, że zestaw narzędzi `CUDA` (lub odpowiednik dla Twojego GPU) znajduje się w zmiennej systemowej `PATH`.

### Co zrobić, gdy mam więcej niż jeden GPU i chcę użyć GPU 1?

Zmień identyfikator urządzenia:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Jak wyodrębnić tekst z obrazu w innym języku?

Ustaw język przed wywołaniem `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose obsługuje ponad 30 języków; pełną listę znajdziesz w dokumentacji API.

### Co zrobić, gdy obraz zawiera wiele stron (np. PDF przekonwertowany na obrazy)?

Utwórz osobny wpis `OcrInput` dla każdej strony lub iteruj po plikach:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Silnik połączy wyniki w kolejności.

### Jak radzić sobie z wynikami o niskiej pewności?

Sprawdź współczynnik pewności:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Typowe kroki wstępnej obróbki to binaryzacja, redukcja szumów lub skalowanie do 300 dpi.

## Wskazówki dotyczące wydajności

- **Przetwarzanie wsadowe:** Dodanie wielu obrazów do jednego `OcrInput` zmniejsza narzut związany z wielokrotnym inicjowaniem kontekstu GPU.  
- **Rozgrzewka:** Po uruchomieniu JVM wykonaj jednorazowe „dummy” rozpoznanie; pierwsze wywołanie obejmuje opóźnienie inicjalizacji sterownika.  
- **Zarządzanie pamięcią:** Usuń duże obiekty `OcrInput` (`ocrInput.clear()`) po zakończeniu, aby zwolnić pamięć GPU.  

## Zakończenie

Teraz wiesz, jak **rozpoznawać tekst na obrazie** efektywnie przy użyciu silnika GPU Aspose OCR w Javie, jak **wyodrębnić tekst z obrazu** w dowolnym obsługiwanym języku oraz jak **ustawić id urządzenia GPU** przy pracy z wieloma kartami graficznymi. Pełny, uruchamialny kod powyżej powinien działać od razu — wystarczy podmienić ścieżki do licencji i obrazu.

Gotowy na kolejny krok? Spróbuj przetworzyć folder ze skanowanymi PDF‑ami, eksperymentuj z różnymi opcjami `setLanguage` lub połącz OCR z modelem uczenia maszynowego do dalszej obróbki. Możliwości są nieograniczone, a zyski wydajnościowe dzięki przyspieszeniu GPU czynią nawet duże projekty wykonalnymi.

Miłego kodowania i śmiało zostaw komentarz, jeśli napotkasz problemy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}