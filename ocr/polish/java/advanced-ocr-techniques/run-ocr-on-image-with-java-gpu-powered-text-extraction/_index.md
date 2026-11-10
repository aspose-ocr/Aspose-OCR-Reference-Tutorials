---
category: general
date: 2026-03-07
description: Uruchom OCR na obrazie przy użyciu Javy. Dowiedz się, jak rozpoznawać
  tekst z pliku PNG, wyodrębniać tekst z paragonu oraz ładować obraz do OCR w pełnym
  przykładzie OCR w Javie.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: pl
og_description: Uruchom OCR na obrazie w Javie. Ten przewodnik pokazuje, jak rozpoznawać
  tekst z pliku PNG, wyodrębniać tekst z paragonu oraz ładować obraz do OCR, używając
  pełnego przykładu OCR w Javie.
og_title: Uruchom OCR na obrazie w Javie – Wydobywanie tekstu przy użyciu GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Uruchom OCR na obrazie w Javie – Wydobywanie tekstu z wykorzystaniem GPU
url: /pl/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uruchamianie OCR na obrazie w Javie – przyspieszenie dzięki GPU

Kiedykolwiek potrzebowałeś **uruchomić OCR na plikach obrazu**, ale nie wiedziałeś od czego zacząć w Javie? Nie jesteś sam — wielu programistów napotyka ten sam problem, gdy po raz pierwszy próbują wyodrębnić tekst ze zeskanowanego paragonu lub zrzutu ekranu PNG.  

W tym tutorialu przeprowadzimy Cię przez **kompletny przykład OCR w Javie**, który nie tylko **rozpoznaje tekst z plików PNG**, ale także pokazuje, jak **wyodrębnić tekst z obrazów paragonów**, wykorzystując przy tym przyspieszenie GPU dla większej wydajności. Po zakończeniu będziesz mieć gotowy do uruchomienia program, który wczytuje obraz do OCR, przetwarza go i wypisuje wynik w postaci czystego tekstu.

## Czego się nauczysz

- Jak **wczytać obraz do OCR** przy użyciu prostego `ImageInputStream`.
- Włączanie wsparcia GPU, aby silnik działał szybciej na nowoczesnym sprzęcie.
- Dokładne kroki **rozpoznawania tekstu z PNG** i wyciągania przydatnych ciągów z paragonu.
- Typowe pułapki (np. nieprawidłowy identyfikator urządzenia GPU) oraz wskazówki najlepszych praktyk.
- Pełny, działający fragment kodu, który możesz skopiować i wkleić do swojego IDE.

**Wymagania wstępne**

- Java 17 lub nowsza (kod używa słowa kluczowego `var` dla zwięzłości, ale możesz zamienić je na jawne typy, jeśli używasz Javy 8).
- Biblioteka OCR udostępniająca klasy `OcrEngine`, `ImageInputStream` i `OcrResult` (np. fikcyjny *FastOCR* SDK; zamień na rzeczywistą bibliotekę, której używasz).
- Maszyna z obsługą GPU, jeśli chcesz skorzystać z przyspieszenia (opcjonalnie, ale zalecane).

---

## Krok 1: Uruchom OCR na obrazie – włącz przyspieszenie GPU

Pierwszym krokiem jest stworzenie silnika OCR i poinstruowanie go, aby używał GPU. Ten krok jest kluczowy, ponieważ bez wsparcia GPU silnik przełącza się na CPU, co może być zauważalnie wolniejsze przy wysokiej rozdzielczości paragonów.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Dlaczego to ważne:**  
Przyspieszenie GPU odciąża ciężkie obliczenia macierzowe, które wykonują silniki OCR. Jeśli masz kilka kart graficznych, możesz wybrać tę z największą ilością pamięci, zmieniając wartość `setGpuDeviceId`. Zapomnienie o włączeniu GPU jest częstą przyczyną skarg typu „dlaczego moje OCR jest tak wolne?”.

> **Pro tip:** Jeśli Twój komputer nie ma kompatybilnego GPU, wywołanie `setUseGpu(true)` zostanie po prostu zignorowane — nie spowoduje awarii, tylko wolniejsze przetwarzanie.

---

## Krok 2: Wczytaj obraz do OCR

Teraz, gdy silnik jest gotowy, musimy podać mu obraz. Poniższy przykład pokazuje, jak wczytać paragon w formacie PNG zapisany na dysku. Ścieżkę możesz zamienić na dowolny format obrazu obsługiwany przez Twoją bibliotekę OCR.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Przypadek brzegowy:**  
Jeśli plik nie istnieje lub ścieżka jest nieprawidłowa, `ImageInputStream` rzuci `IOException`. Owiń wywołanie w blok try‑catch i zaloguj pomocny komunikat:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Krok 3: Rozpoznaj tekst z PNG

Po wczytaniu obrazu silnik OCR może wykonać swoją magię. Ten krok faktycznie **rozpoznaje tekst z PNG** (lub dowolnego innego obsługiwanego formatu) i zwraca obiekt `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Co się dzieje pod maską?**  
Silnik wykonuje wstępne przetwarzanie (prostowanie, binaryzację), uruchamia sieć neuronową wykrywającą znaki, a następnie łączy je w linie tekstu. Ponieważ wcześniej włączyliśmy GPU, te obliczenia sieci neuronowej odbywają się na karcie graficznej, co skraca całkowity czas wykonania o kilka sekund.

---

## Krok 4: Wyodrębnij tekst z paragonu

Po rozpoznaniu zazwyczaj potrzebujesz tylko surowego tekstu. Klasa `OcrResult` zazwyczaj udostępnia metodę `getText()`, która zwraca pojedynczy `String`. Następnie możesz go poddać dalszemu przetwarzaniu (np. wyrażeniom regularnym, aby wyciągnąć sumy, daty itp.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typowy wynik paragonu:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Teraz możesz przekazać ten ciąg do własnego parsera, aby wyciągnąć kwotę całkowitą, pozycje zakupów lub informacje o podatku.

---

## Krok 5: Pełny przykład OCR w Javie – gotowy do uruchomienia

Łącząc wszystkie elementy, oto **kompletny przykład OCR w Javie**, który możesz wkleić do pliku `Main.java`. Upewnij się, że biblioteka OCR znajduje się na classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Oczekiwany wynik w konsoli** (przy założeniu przykładowego paragona powyżej):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Jeśli wynik wygląda na zniekształcony, sprawdź, czy obraz jest wyraźny (wysoka DPI) oraz czy pakiet językowy OCR odpowiada językowi Twojego paragona.

---

## Częste pytania i pułapki

| Pytanie | Odpowiedź |
|----------|-----------|
| *Co zrobić, jeśli GPU nie zostanie wykryte?* | Silnik automatycznie przełączy się na CPU. Sprawdź sterowniki i upewnij się, że `setGpuDeviceId` odpowiada istniejącemu urządzeniu (`nvidia-smi` w Linuxie może pomóc). |
| *Czy mogę przetwarzać pliki JPEG lub TIFF?* | Tak — wystarczy zmienić rozszerzenie w `ImageInputStream`. Biblioteka OCR zazwyczaj automatycznie wykrywa format. |
| *Czy istnieje sposób na przetwarzanie wsadowe wielu paragonów?* | Umieść kod rozpoznawania w pętli i ponownie używaj tej samej instancji `OcrEngine`; ponowne inicjowanie przy każdym obrazie marnuje pamięć GPU. |
| *Jak poprawić dokładność przy słabo kontrastowych paragony?* | Przetwórz obraz wstępnie (zwiększ kontrast, konwersja do odcieni szarości) przed przekazaniem go do silnika OCR. Niektóre biblioteki udostępniają API `preprocess`. |

---

## Zakończenie

Teraz wiesz **jak uruchomić OCR na obrazach** w Javie, od wczytania zdjęcia po wyodrębnienie czystego tekstu z paragona. Przewodnik obejmował **rozpoznawanie tekstu z PNG**, **wyodrębnianie tekstu z paragona** oraz pokazał **przykład OCR w Javie**, który możesz dostosować do dowolnego projektu.  

Co dalej? Spróbuj wyłączyć flagę GPU, aby zobaczyć różnicę w wydajności, eksperymentuj z różnymi rozdzielczościami obrazów lub zintegrować parser oparty na wyrażeniach regularnych, aby automatycznie wyciągać sumy. Jeśli interesują Cię bardziej zaawansowane tematy, zajrzyj do **post‑processingu OCR**, **korekcji modelu językowego** lub **pipeline’ów przetwarzania wsadowego**.

Miłego kodowania i niech Twoje paragony zawsze będą czytelne!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}