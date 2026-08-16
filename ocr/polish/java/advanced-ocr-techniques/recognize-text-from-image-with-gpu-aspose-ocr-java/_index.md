---
category: general
date: 2026-04-26
description: Dowiedz się, jak rozpoznawać tekst z obrazu przy użyciu Aspose OCR z
  przyspieszeniem GPU w Javie. Zawiera ustawienie limitu pamięci GPU oraz kroki ładowania
  obrazu do OCR.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: pl
og_description: Odkryj, jak szybko rozpoznawać tekst z obrazu przy użyciu przyspieszonego
  GPU Aspose OCR w Javie. Przewodnik krok po kroku z ustawieniem limitu pamięci GPU
  i wczytywaniem obrazu do OCR.
og_title: Rozpoznaj tekst z obrazu przy użyciu GPU Aspose OCR (Java)
tags:
- OCR
- Java
- GPU
- Aspose
title: Rozpoznawanie tekstu z obrazu przy użyciu GPU Aspose OCR (Java)
url: /pl/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rozpoznawanie tekstu z obrazu przy użyciu GPU Aspose OCR (Java)

Czy kiedykolwiek potrzebowałeś szybko **rozpoznawać tekst z obrazu** w backendzie Java? Dzięki przyspieszeniu GPU w Aspose OCR możesz zaoszczędzić sekundy przy każdym skanowaniu — koniec z czekaniem, aż CPU przetworzy megabajty pikseli. W tym samouczku przeprowadzimy Cię przez włączenie GPU, opcjonalne **ustawienie limitu pamięci GPU**, oraz w końcu **załadowanie obrazu do OCR**, abyś otrzymał czysty ciąg tekstowy w zaledwie kilku linijkach kodu.

Omówimy wszystko, co potrzebne do uruchomienia demonstracji na karcie obsługującej CUDA, wyjaśnimy, dlaczego każde ustawienie ma znaczenie, i pokażemy kompletny, gotowy do uruchomienia przykład. Po zakończeniu będziesz mógł wstawić OCR przyspieszone GPU do dowolnej usługi Java, niezależnie od tego, czy jest to potok ingestii dokumentów, czy backend w czasie rzeczywistym dla aplikacji mobilnej.

## Czego będziesz potrzebować

- **Java 17** lub nowszy (plik JAR Aspose OCR jest przeznaczony dla nowoczesnych JVM)  
- **GPU kompatybilne z CUDA** z co najmniej 2 GB VRAM (demo ogranicza użycie do 1024 MB)  
- Biblioteka **Aspose.OCR for Java** (pobierz ze strony Aspose lub z Maven)  
- Plik obrazu, który chcesz przetworzyć – najlepiej skan lub zdjęcie w wysokiej rozdzielczości  

Brak zewnętrznych usług, brak kluczy w chmurze, tylko lokalna instalacja. Jeśli nie masz jeszcze GPU, nadal możesz uruchomić kod; wywołanie `setUseGpu(true)` automatycznie przełączy się na CPU.

## Krok 1: Dodaj Aspose OCR do swojego projektu i rozpoznaj tekst z obrazu

Najpierw upewnij się, że plik JAR Aspose OCR znajduje się w classpath. Jeśli używasz Maven, dodaj:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Gdy biblioteka jest dostępna, utwórz instancję `OcrEngine`. Ten obiekt jest punktem wejścia dla operacji **rozpoznawania tekstu z obrazu**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Dlaczego najpierw tworzymy `OcrEngine`? Przechowuje wszystkie ustawienia rozpoznawania (flagi GPU, pakiety językowe itp.) i izoluje każde skanowanie, dzięki czemu możesz bezpiecznie ponownie używać tego samego silnika dla wielu obrazów, nie powodując wycieków pamięci.

## Krok 2: Włącz przyspieszenie GPU i opcjonalnie **ustaw limit pamięci GPU**

Przyspieszenie GPU to tajny składnik, który umożliwia OCR na dużą skalę. Aspose pozwala przełączać je jednym wywołaniem:

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

Jeśli Twój GPU jest współdzielony z innymi obciążeniami, możesz chcieć ograniczyć ilość VRAM, jaką silnik może zająć. Wtedy przydaje się **ustawienie limitu pamięci GPU**:

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

Ustawienie limitu pamięci zapobiega awariom z powodu braku pamięci przy przetwarzaniu wielu wysokiej rozdzielczości obrazów równocześnie. Wartość podawana jest w megabajtach, więc `1024` oznacza „użyj maksymalnie 1 GB VRAM”.

> **Wskazówka:** Na karcie 4 GB limit 2 GB jest zazwyczaj bezpiecznym wyborem; możesz eksperymentować z wyższymi wartościami, jeśli zauważysz, że GPU jest bezczynne.

## Krok 3: **Załaduj obraz do OCR** – wskaż silnikowi swój plik

Teraz, gdy silnik jest gotowy, musimy powiedzieć mu, który obraz zeskanować. Aspose akceptuje ścieżkę do pliku, `java.io.File` lub nawet `java.awt.image.BufferedImage`. Dla prostoty użyjemy ścieżki:

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

Zastąp `YOUR_DIRECTORY/high_res_photo.jpg` rzeczywistą lokalizacją obrazu testowego. Jeśli obraz znajduje się w folderze zasobów, możesz zamiast tego użyć `getClass().getResource("/images/sample.png").getPath()`.

Dlaczego ładowanie ma znaczenie? Silnik wykonuje krok wstępnego przetwarzania (prostowanie, binaryzacja), który jest silnie zależny od GPU. Dostarczenie czystego, wysokiej rozdzielczości pliku pozwala GPU pracować wydajnie i poprawia dokładność **rozpoznawania tekstu z obrazu**.

## Krok 4: Uruchom rozpoznawanie i pobierz wyodrębniony ciąg znaków

Po włączeniu GPU i załadowaniu obrazu, ostatnie wywołanie jest proste:

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

Metoda `recognize()` blokuje, dopóki GPU nie zakończy, a następnie `getText()` zwraca zwykły `String`. W tle Aspose używa modelu deep‑learningowego działającego na rdzeniach CUDA, więc opóźnienie jest zazwyczaj ułamkiem tego, co potrzebowałby OCR działający wyłącznie na CPU.

## Krok 5: Wyświetl wynik

Wydrukujmy wynik OCR w konsoli, abyś mógł zweryfikować, że działa:

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

Jeśli wszystko jest poprawnie podłączone, zobaczysz transkrybowany tekst natychmiast. Na przyzwoitej karcie RTX 2060, obraz 3000 × 2000 px przetwarza się w mniej niż sekundę.

![rozpoznawanie tekstu z obrazu przy użyciu GPU Aspose OCR](/images/gpu-ocr-demo.png "Demo OCR przyspieszonego GPU")

*Tekst alternatywny obrazu:* **rozpoznawanie tekstu z obrazu** – zrzut ekranu wyjścia konsoli po OCR na GPU.

## Oczekiwany wynik

Uruchomienie pełnego programu na przykładowym paragonie daje coś w rodzaju:

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

Twój rzeczywisty tekst będzie się różnił w zależności od obrazu źródłowego, ale powyższy format pokazuje, że silnik prawidłowo wyodrębnia podziały wierszy i liczby.

## Częste problemy i praktyczne wskazówki

| Problem | Dlaczego się pojawia | Jak naprawić |
|---------|----------------------|--------------|
| **GPU nie wykryto** | brak sterownika CUDA lub niekompatybilna wersja JAR | Zainstaluj najnowszy sterownik NVIDIA, sprawdź, czy działa `nvidia-smi`, i użyj Aspose OCR 23.12 lub nowszego |
| **Błąd braku pamięci** | Obraz zbyt duży dla ograniczonej pamięci VRAM | Zwiększ `setGpuMemoryLimit` lub zmniejsz rozmiar obrazu przed załadowaniem |
| **Zniekształcone znaki** | Obraz jest rozmyty lub ma niski kontrast | Wstępnie przetwórz używając `ocrEngine.getPreprocessingSettings().setBinarization(true)` |
| **Wolna wydajność przy pierwszym uruchomieniu** | koszt inicjalizacji kontekstu GPU | Rozgrzej silnik, przetwarzając mały obraz testowy przed właściwym obciążeniem |

Pamiętaj, że **set gpu memory limit** jest opcjonalny, ale

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}