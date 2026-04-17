---
category: general
date: 2026-03-28
description: Dowiedz się, jak rozpoznawać tekst na obrazach w Javie przy użyciu Aspose
  OCR, wyodrębniać pliki PNG z tekstem i korzystać z przyspieszenia GPU, aby szybko
  przeprowadzać OCR dużych obrazów.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: pl
og_description: Odkryj, jak rozpoznawać tekst na obrazach w Javie, wyodrębniać tekst
  z plików PNG i korzystać z przyspieszenia GPU przy OCR dużych obrazów.
og_title: Rozpoznawanie tekstu na obrazie w Java OCR – przykład przyspieszony GPU
tags:
- OCR
- Java
- GPU
title: Rozpoznawanie tekstu na obrazie w Java OCR – przykład przyspieszony GPU
url: /pl/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu na obrazie przy użyciu Java OCR – przykład przyspieszony GPU

Czy kiedykolwiek potrzebowałeś **rozpoznawać tekst na obrazie** z ogromnego pliku PNG, ale wersja CPU działała jak w żółw? Nie jesteś jedyny. W wielu rzeczywistych przepływach pracy — pomyśl o skanowaniu faktur lub archiwizacji dokumentów historycznych — rozmiar obrazu może się rozrosnąć, a domyślny silnik OCR po prostu nie nadąża.  

Dobre wieści: Aspose OCR for Java pozwala **używać przyspieszenia GPU**, aby przyspieszyć proces, a kod jest zaskakująco zwięzły. W tym samouczku zobaczysz kompletny, gotowy do uruchomienia przykład Java OCR, który **wyodrębnia tekst z plików PNG**, wykorzystuje GPU z obsługą CUDA i obsługuje **duży obraz OCR** przy użyciu kilku linijek kodu. Po zakończeniu dokładnie wiesz, jak podłączyć to do własnego projektu Java i dlaczego każde ustawienie ma znaczenie.

## Czego się nauczysz

- Jak skonfigurować Aspose OCR w projekcie Maven lub Gradle.  
- Krok po kroku proces **rozpoznawania tekstu na obrazie** na GPU.  
- Dlaczego konfigurowanie liczby strumieni GPU może zwiększyć przepustowość.  
- Jak zweryfikować wynik i rozwiązywać typowe problemy.  

> **Wymagania wstępne** – Java 17 (lub nowsza), GPU kompatybilne z CUDA z najnowszym sterownikiem oraz ważna licencja Aspose OCR for Java (bezpłatna wersja próbna działa w celach oceny). Nie są wymagane żadne inne zewnętrzne biblioteki.

## Krok 1: Dodaj zależność Aspose OCR

Najpierw dodaj bibliotekę Aspose OCR do swojego projektu. Jeśli używasz **Maven**, dodaj następujący fragment do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Dla **Gradle**, umieść to w `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Porada:** Najnowsza wersja (stan na marzec 2026) zawiera ulepszenia wydajności dla obciążeń GPU, więc zawsze pobieraj najnowsze wydanie.

## Krok 2: Zainicjalizuj silnik OCR i włącz GPU

Utworzenie silnika OCR jest proste. Kluczową częścią jest włączenie flagi GPU — w przeciwnym razie silnik przełącza się w tryb CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Dlaczego włączyć GPU?

Gdy włączysz `setUseGpu(true)`, Aspose przenosi ciężkie obliczenia sieci neuronowej konwolucyjnej na kartę graficzną. Może to zaoszczędzić sekundy w czasie przetwarzania **dużego obrazu OCR**, szczególnie gdy obraz przekracza 4000 × 4000 px. Jeśli w twoim środowisku brakuje kompatybilnego GPU, wywołanie po prostu nie robi nic i silnik kontynuuje pracę na CPU — bez awarii, tylko wolniej.

## Krok 3: Rozpoznaj obraz PNG i wyodrębnij jego tekst

Teraz wskaż silnik na plik, który chcesz przetworzyć. Przykład używa `sample-large.png`, ale możesz go zamienić na dowolny plik PNG lub JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Po uruchomieniu programu powinieneś zobaczyć coś podobnego do:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Ten wynik potwierdza, że operacja **rozpoznawania tekstu na obrazie** zakończyła się sukcesem i że pomyślnie **wyodrębniłeś tekst z PNG**.

## Krok 4: Zweryfikuj wykorzystanie GPU (Opcjonalne, ale przydatne)

Jeśli jesteś ciekawy, czy GPU jest naprawdę używane, otwórz narzędzie monitorujące GPU w systemie (np. `nvidia-smi` na Linux). Podczas działania procesu Java powinieneś zauważyć niewielki wzrost zużycia pamięci i wykorzystania obliczeń.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Jeśli nie widzisz żadnej aktywności, sprawdź ponownie, czy:

1. Sterownik CUDA odpowiada modelowi GPU.  
2. Wywołanie `setUseGpu(true)` nie jest nadpisywane później w kodzie.  
3. Plik licencji (jeśli go masz) nie ogranicza użycia GPU.

## Krok 5: Obsługa typowych przypadków brzegowych

### Duże obrazy przekraczające pamięć GPU

Gdy obraz jest ogromny (np. 8000 × 8000 px), GPU może nie mieć wystarczającej pamięci. Szybkim obejściem jest zmniejszenie rozmiaru obrazu przed przekazaniem go do Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Następnie przekaż `"sample-resized.png"` do `recognizeImage`. To utrzymuje dokładność OCR, jednocześnie mieszcząc się w limitach GPU.

### Wielostronicowe PDF-y

Aspose OCR może także obsługiwać PDF-y strona po stronie. Przejdź w pętli po każdej stronie, skonwertuj ją na obraz i przekaż do silnika. Ta sama flaga **use gpu acceleration** obowiązuje, zapewniając szybki pipeline PDF‑do‑tekst.

## Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się pełna klasa Java, gotowa do kompilacji i uruchomienia. Zastąp `YOUR_DIRECTORY` ścieżką do swojego pliku PNG.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Oczekiwany wynik** – tekstowa reprezentacja wszystkiego, co silnik mógł odczytać z obrazu. Jeśli obraz zawiera tabelę, otrzymasz zawartość komórek połączoną znakami nowej linii; Aspose nie zachowuje układu, ale możesz przetworzyć ciąg znaków w razie potrzeby.

## Najczęściej zadawane pytania

| Question | Answer |
|----------|--------|
| **Czy potrzebuję płatnej licencji?** | Wersja próbna działa do 200 stron i wyłącza znak wodny dla OCR. W produkcji licencja usuwa ograniczenia i odblokowuje pełny stos GPU. |
| **Co jeśli mój GPU jest starszy (np. GTX 750)?** | Starsze GPU mogą nadal działać, ale z mniejszą prędkością; upewnij się, że masz co najmniej Compute Capability 3.0. |
| **Czy mogę przetwarzać pliki JPG lub BMP?** | Oczywiście — `recognizeImage` akceptuje każdy format obsługiwany przez Java ImageIO. |
| **Czy istnieje sposób na przetwarzanie wsadowe wielu obrazów?** | Umieść wywołanie OCR w pętli i rozważ zwiększenie `setGpuStreams`, aby dopasować liczbę równoczesnych strumieni. |
| **Co jeśli muszę zachować układ?** | Użyj `LayoutOptions` z Aspose OCR, aby uzyskać ramki ograniczające; to wykracza poza zakres tego krótkiego przewodnika, ale jest udokumentowane w API. |

## Zakończenie

Masz teraz zwięzły, kompleksowy **przykład java ocr**, który **rozpoznaje tekst na obrazie**, **wyodrębnia tekst z PNG** i **używa przyspieszenia GPU**, aby przyspieszyć przetwarzanie **dużego obrazu OCR**. Poprzez dostosowanie liczby strumieni GPU oraz, w razie potrzeby, zmniejszanie rozmiaru przerośniętych obrazów, możesz dopasować rozwiązanie do praktycznie każdej konfiguracji sprzętowej.

Gotowy na kolejny krok? Spróbuj podać folder ze skanowanymi paragonami do tego samego pipeline'u lub poeksperymentuj z API `TextRegion` Aspose, aby zachować oryginalny układ. Jeśli napotkasz problemy, fora Aspose i Javadoc są świetnymi źródłami — pamiętaj tylko o podstawach, które tutaj omówiliśmy.

Miłego kodowania i niech Twój OCR będzie błyskawiczny!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}