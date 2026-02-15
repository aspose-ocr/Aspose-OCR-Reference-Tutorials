---
category: general
date: 2026-02-14
description: Jak włączyć GPU w Aspose OCR Java, aby szybko wyodrębniać tekst z obrazu.
  Dowiedz się, jak konwertować TIFF na tekst, ustawić identyfikator urządzenia GPU
  i odczytywać tekst z plików TIFF.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: pl
og_description: Jak włączyć GPU w Aspose OCR Java, aby szybko wyodrębnić tekst z obrazu.
  Postępuj zgodnie z tym przewodnikiem, aby przekonwertować TIFF na tekst, ustawić
  identyfikator urządzenia GPU i odczytać tekst z pliku TIFF.
og_title: Jak włączyć GPU dla OCR – wyodrębnić tekst z pliku TIFF
tags:
- OCR
- Java
- GPU acceleration
title: Jak włączyć GPU dla OCR i wyodrębnić tekst z pliku TIFF
url: /pl/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak włączyć GPU dla OCR i wyodrębnić tekst z pliku TIFF

Zastanawiałeś się kiedyś, **jak włączyć GPU** podczas wykonywania OCR na dużych plikach TIFF? Nie jesteś jedyny — programiści nieustannie poszukują dodatkowego przyspieszenia, szczególnie gdy źródłowy obraz to wielomegabajtowy TIFF. Dobra wiadomość? Dzięki Aspose OCR for Java możesz przełączyć przełącznik, wskazać odpowiednie GPU i obserwować, jak silnik przyspiesza przetwarzanie obrazu.

W tym samouczku przejdziemy przez cały proces: wczytanie TIFF, włączenie przyspieszenia GPU, opcjonalny wybór konkretnego urządzenia GPU, uruchomienie OCR oraz **wyodrębnienie tekstu z obrazu**. Po zakończeniu będziesz w stanie **konwertować TIFF na tekst** w kilku linijkach kodu oraz zobaczysz, jak **czytać tekst z plików TIFF** na dowolnej obsługiwanej platformie.

## Czego będziesz potrzebować

- Java 17 lub nowsza (kod działa również z Java 8+)
- Aspose OCR for Java 23.10 (lub najnowsza wersja w momencie pisania)
- GPU kompatybilne z CUDA oraz najnowszy sterownik
- Przykładowy wielostronicowy TIFF (nazwijmy go `sample_large.tif`)

Brak Maven? Żaden problem — po prostu wrzuć plik JAR do classpath i gotowe.

![Jak włączyć GPU tutorial](gpu-ocr.png)

*Tekst alternatywny obrazu: Jak włączyć GPU dla OCR w Javie*

## Krok 1: Wczytaj obraz TIFF do OCR

Na początek potrzebujesz instancji `OcrEngine` oraz obrazu źródłowego. Aspose OCR potrafi odczytać praktycznie każdy format rastrowy, ale TIFF jest powszechny w dokumentach skanowanych.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Dlaczego to ważne:** Wywołanie `setImage` opakowuje plik w `ImageStream`, co pozwala silnikowi obsługiwać wielostronicowe TIFF‑y bez ręcznego dzielenia ich na poszczególne strony. Jeśli plik nie zostanie znaleziony, otrzymasz wyraźny `FileNotFoundException` — więc sprawdź dwukrotnie ścieżkę.

## Krok 2: Włącz przyspieszenie GPU

Teraz dzieje się magia. Włączenie GPU to tylko flaga boolowska, ale może zaoszczędzić sekundy — a nawet minuty — czasu przetwarzania.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Porada:** Jeśli Twój komputer ma wiele GPU, domyślnie używane jest zazwyczaj pierwsze (urządzenie 0). Możesz pozwolić Aspose wybrać najlepsze urządzenie automatycznie, ale podanie konkretnego ID może zapobiec niespodziankom na stacjach roboczych z wieloma kartami.

## Krok 3: Ustaw ID urządzenia GPU (opcjonalnie)

Czasami wiesz dokładnie, które GPU chcesz użyć — np. druga karta jest przeznaczona wyłącznie do zadań AI. Wtedy przydaje się metoda `setGpuDeviceId`.

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Przypadek brzegowy:** Jeśli przekażesz nieprawidłowe ID, silnik rzuci `IllegalArgumentException`. Szybkie `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` wyświetli dostępne identyfikatory.

## Krok 4: Przetwórz obraz i **wyodrębnij tekst z obrazu**

Po skonfigurowaniu silnika czas uruchomić OCR. Obiekt wyniku zwraca surowy ciąg znaków oraz, w razie potrzeby, oceny pewności.

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Oczekiwany wynik

Jeśli TIFF zawiera frazę „Hello, World!”, powinieneś zobaczyć coś w stylu:

```
Recognized text:
Hello, World!
```

Silnik radzi sobie z podziałem linii, interpunkcją i nawet podstawowym wykrywaniem układu. Jeśli potrzebujesz bardziej szczegółowej kontroli (np. wyodrębniać tekst po stronach), zapoznaj się z `ocrResult.getPages()`.

## Krok 5: Zweryfikuj wynik i radź sobie z typowymi problemami

### Dlaczego GPU może nie być używane?

- **Niezgodność sterownika:** Sterownik GPU musi mieć co najmniej wersję zalecaną przez Aspose (sprawdź notatki wydania).
- **Niewystarczająca pamięć:** Bardzo duże obrazy mogą przekroczyć pamięć VRAM GPU. W takim wypadku silnik automatycznie przełącza się na CPU — szukaj ostrzeżenia w konsoli.
- **Nieobsługiwany sprzęt:** Zintegrowane układy graficzne często nie spełniają wymaganego poziomu możliwości obliczeniowych.

### Jak przełączyć się na CPU programowo

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Czytanie tekstu z TIFF w pętli

Jeśli masz folder pełen plików TIFF, możesz iterować:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Ten fragment pokazuje, jak **czytać tekst z plików TIFF** masowo, jednocześnie korzystając z przyspieszenia GPU.

## Najczęściej zadawane pytania (FAQ)

**P: Czy to działa na Linuxie?**  
O: Absolutnie — Aspose OCR jest wieloplatformowy. Upewnij się tylko, że zainstalowano zestaw narzędzi CUDA oraz sterowniki.

**P: Co zrobić, jeśli nie mam GPU?**  
O: Ustaw `setUseGpu(false)` lub po prostu pomiń to wywołanie. Silnik domyślnie używa CPU.

**P: Czy mogę wyodrębnić tekst z innych formatów?**  
O: Tak, ta sama metoda `setImage` przyjmuje JPEG, PNG, BMP, a nawet strumienie PDF.

**P: Jak dokładny jest OCR przy niskiej rozdzielczości TIFF?**  
O: Dokładność spada poniżej 300 dpi. Rozważ wstępne przetworzenie obrazu (binaryzacja, prostowanie) przed przekazaniem go do silnika.

## Podsumowanie

Teraz wiesz, **jak włączyć GPU** dla Aspose OCR Java, jak **ustawić ID urządzenia GPU**, a co najważniejsze — **jak wyodrębnić tekst z plików obrazu**, szczególnie **konwertować TIFF na tekst** i **czytać tekst z TIFF** efektywnie. Przełączając jedną flagę i ewentualnie wybierając konkretne urządzenie, uzyskasz ogromne przyspieszenie bez konieczności przepisywania logiki OCR.

Gotowy na kolejny krok? Wypróbuj:

- **Przetwarzanie wsadowe** setek plików TIFF w równoległych wątkach.
- **Niestandardowe pakiety językowe**, aby poprawić rozpoznawanie w specjalistycznych dokumentach.
- **Post‑processing** wyodrębnionego ciągu przy użyciu wyrażeń regularnych w celu oczyszczenia formatowania.

Zostaw komentarz, jeśli napotkasz problemy, i powodzenia w kodowaniu!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}